---
layout: post
title: タイルのデプロイ時間を！ベクトルタイルの動的配信を完全サーバーレス化した話
background: /img/20201203/header.jpg
excerpt: Geolonia のベクトルタイル配信環境をアップデートし、ベクトルタイル開発のフローを効率化しました。
author: kamataryo
---

こんにちは！  
このポストでは、Geolonia のベクトルタイル配信基盤についての技術的な詳細を解説します。

Gelonia のバックエンドは AWS 環境上に構築されていて、完全なサーバーレス構成になっています。従来はベクトルタイルのデータを静的にホスティングして地図の配信を行っていましたが、今回システムのリプレイスを行い、サーバーレスな構成を維持したままベクトルタイルを動的に配信できるようになりました。

## リプレイス前（静的配信）

タイルを静的配信する旧環境は Amazon S3、 及び CloudFront を用いた構成でした。  
地図タイルは `z/x/y.mvt` のようなパスで配信されていることが多いと思いますが、この zxy インデックスをキーに S3 バケットのオブジェクトとして静的なファイルをホスティングしています。このバケットをオリジンに設定した CloudFront からタイルの配信が行われます。

![static tiles](/img/20201203/010_static.png)

ユーザーからタイルのリクエストがあると、CloudFront へのビューワリクエスト及びオリジンレスポンスに伴って [Lambda@Edge](https://docs.aws.amazon.com/ja_jp/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html) が発火し、アクセストークンの検証やキャッシュ制御などを行います。

![lambda edge](/img/20201203/020_lambdaatedge.png)

Lambda@Edge としてデプロイする Lambda 関数の作成やインフラの構成管理については [Serverless Framework](https://www.serverless.com/) をインターフェースとして用いることで DevOps に親和的な開発環境になっています。

### 課題

S3 でのベクトルタイルホスティングにはいくつかの課題があります。

まず、Lambda@Edge のデプロイフローが煩雑であること。関数の更新と反映のためには CloudFront の再デプロイが必要で、更新には 10 分近い時間がかかります。  
また、タイルのデータのデプロイはさらに大変で、直列で処理した場合ですが、例えば日本のエリアを対象に生成した全てのベクトルタイルをデプロイするために日単位の時間がかかります。これは、HTTP で行われる `S3::putObject` の操作を大量のファイルに対して行う必要があるためです。

## リプレイス後（動的配信）

そこで、S3 と Lambda@Edge の利用をやめ、タイルのデータのデプロイは [MBTiles](https://wiki.openstreetmap.org/wiki/MBTiles) 形式のファイルの単位で行うことにし、デプロイにかかる時間の短縮をはかりました。新しい配信環境の構成は以下のようになっています。

![dynamic tiles](/img/20201203/030_dynamic.png)

新環境では、 MBTiles ファイルをパースせず、直接 EFS に保存することにしました。同一の VPC 内に Lambda を配置し EFS をマウントすることでデータへのアクセスが可能になります。MBTiles のファイルは SQLite 形式のデータベースで、Lambda の内部で zxy インデックスを指定してクエリを行うことでベクトルタイルのバイナリデータを直接取得します。

#### メリット

EFS を使うことでデプロイの速度が大幅に改善されました。作業の負担が軽減され、デプロイ・検証・公開のサイクルを短縮したことで、フィードバックをダイレクトに反映しながら製品である地図タイルを改善していくワークフローが整いました。

データの出力時にコンテンツに対して動的な変更を加えることが可能になったのも魅力的です。例えばタイルをリクエストしたユーザーに応じて個別に最適化されたデータを配信することも可能になりました。

新しい配信方式のベクトルタイルの地図は [公式ドキュメント](https://docs.geolonia.com/tutorial/001/) などで体験していただくことができます。CodePen というサービスで好きなようにカスタマイズしながら Geolonia の地図を試していただくことが可能です。この際 API キーは不要です。

また、現在 β 版の段階ですが、独自ドメインで Geolonia の地図を利用する上で必要な API キーを発行するための[ダッシュボード](https://app.geolonia.com)も用意しています。

---

Geolonia ではクラウドや Node.js が好きな開発パートナーさんを募集しています。
ぜひ Geolonia の [Office Hour](https://calendly.com/geolonia/office-hour) に遊びに来てください。
雑談でも大歓迎です！