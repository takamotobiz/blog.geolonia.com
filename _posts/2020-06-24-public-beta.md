---
layout: post
title: パブリックβはじめます！ Geolonia の地図を独自ドメインでご利用いただけるようになりました！
background: /img/20200624/header.jpg
excerpt: ダッシュボードや各種 API の機能が予定していたクオリティに達しましたので、パブリックβを開始いたします！
author: miya
---

<p style="text-align: right;">Photo by <a href="https://unsplash.com/@peterng1618">Peter Nguyen</a> on <a href="https://unsplash.com/">Unsplash</a></p>

たいへん長らくお待たせいたしました。

ダッシュボードや各種 API の機能が予定していたクオリティに達しましたので、パブリックベータを開始いたします！

これまでも GitHub ページなどのサービス上などの特定のドメイン上でのご利用を無料で開放していましたが、本日からみなさんの独自ドメインでご利用いただくことが可能になります！

## Geolonia の地図の特徴

まずはじめに、私たちが提供する地図の特徴についてご紹介させてください。

* [Mapbox](https://www.mapbox.com/) 社の [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/) というオープンソースプロジェクトをベースにしたベクトルタイルというフォーマットを採用しており WebGL にてレンダリングされているため、自由度の高いデザインが特徴で、JavaScript API も高機能です。
* [OpenStreetMap](https://www.openstreetmap.org/) を基盤としているため、印刷して再配布することが可能なことなど、自由度の高いライセンスになっています。
* Cookie を使用しておらず、地図を閲覧するユーザーの個人情報を取り扱っておりません。
* JavaScript が書けなくても HTML だけで地図を設置することが可能です。

![](https://www.evernote.com/l/ABUQQOWud2NOtJlOpTEgbvmTu0FvEJVN-0cB/image.png)

ダッシュボードでは位置情報のデータセットを登録することもできます。

## ご利用料金 & ご利用条件

* βテスト中は無料でご利用できます。ただし月間3万PVを大きく上回る地図アクセスがあるお客様に対してはこちらからコンタクトを取らせていただく場合がございますので、あらかじめご了承ください。
* 予告なく仕様が変わる場合がございますので、あらかじめご了承ください。

## ご利用の開始方法

独自ドメインで弊社の地図をご利用いただくには、サインアップして API キーを取得していただく必要があります。

[https://app.geolonia.com/](https://app.geolonia.com/)

[![](https://www.evernote.com/l/ABVwIak9fDBArJ1jUuMSyGZarYc66gXWBfcB/image.png)](https://app.geolonia.com/)

## ドキュメンテーション

地図の設置方法は公式ドキュメントを御覧ください。

[Geolonia 公式ドキュメント](https://docs.geolonia.com/)

[![](https://www.evernote.com/l/ABWJxDr7ImZG8oSx-dU0sPaVZ2C3qBzzdGEB/image.png)](https://docs.geolonia.com/)

## サンプル

CodePen の Geolonia アカウントにおいてサンプルコードをご覧いただくことができます。

[Geolonia on CodePen](https://codepen.io/geolonia/)

[![](https://www.evernote.com/l/ABUopoaCHX9E_r58CVtSx9yiaR1iyU7xnMoB/image.png)](https://codepen.io/geolonia/)

## フィードバック

フィードバックは以下の GitHub リポジトリの Issue として登録をお願いいたします。

[https://github.com/geolonia/public-beta/issues](https://github.com/geolonia/public-beta/issues)
