---
layout: post
title: "βテスト開始: Geolonia の地図を GitHub Pages などの環境で無料でお試しいただけます！"
background: /img/20200319/background.jpg
excerpt: Geolonia の JavaScript API が実運用可能なクオリティに達したと判断しまして、ようやく皆様にお試しいただくことができるようになりました。
author: miya
---

<p style="text-align: right; font-size: 80%;">Photo by <a href="https://unsplash.com/@waldemarbrandt67w?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Waldemar Brandt</a> on <a href="https://unsplash.com/">Unsplash</a></p>

ながらくお待たせいたしました！

このたび、Geolonia の JavaScript API が実運用可能なクオリティに達したと判断しまして、ようやく皆様にお試しいただくことができるようになりました。

そこで、一人でも多くのユーザーの皆様にお試しいただくためにβテストを開始いたします。

## Geolonia の地図の特徴

まずはじめに、私たちが提供する地図の特徴についてご紹介させてください。

* ベクトルタイルというフォーマットを採用しており WebGL にてレンダリングされているため、自由度の高いデザインが特徴で、JavaScript API も高機能です。
* OpenStreetMap を基盤としているため、印刷して再配布することが可能であることなど、自由度の高いライセンスになっています。
* Cookie を使用しておらず、地図を閲覧するユーザーの個人情報を取り扱っておりません。
* JavaScript が書けなくても HTML だけで地図を設置することが可能です。

## βテストへの参加条件

以下の条件でご利用頂く場合に限り、無料とさせていただきます。

* [GitHub Pages](https://pages.github.com/) 上の `*.github.io` ドメイン （GitHub Pages であっても独自ドメインは除外とさせていただきます。）
* 以下にあげるコードサンドボックス系のサイト
  * [CodePen](https://codepen.io/)
  * [CodeSandbox](https://codesandbox.io/)
  * [JSFiddle](https://jsfiddle.net/)
* Twitter で Geolonia のアカウント [@geoloniamap](https://twitter.com/geoloniamap) をフォローしてください。

これらのサイトでのご利用に関しましては、本サービス開始後も無料とさせて頂く予定ですので、安心してご利用ください。

### API キーについて

Geolonia の地図をご利用いただくには、API キーが必要です。

ただし、上述のサイトに関しては、テスト用の API キー `YOUR-API-KEY` をご利用いただけますので、ユーザー登録やダッシュボードへのログイン等は必要ありません。

### ご利用条件

* スクリプト等を使用して、地図データを大量にダウンロードするような行為はおやめください。
* `iFrame` 内ではご利用いただけません。
* 地図の下部に表示されている弊社および OpenStreetMap Contributors へのクレジットを消さないでください。
* その他、予告なくなんらかの制限が加わることがありますので、あらかじめご了承ください。

### プライバシーについて

* Geolonia の地図は、Cookie を使用しておりませんので、プライバシーポリシーの変更を行うことなくご利用いただけます。
* 一方で、皆様のご利用状況を把握するために、HTTP Referer や IP アドレスなどの一般的なアクセスログを保存しております。

## 地図の設置方法

地図を設置するには、まず、弊社の API にアクセスするための HTML を記述する必要があります。

以下の HTML をコピーして、`body` 要素の終了タグ `</body>` 直前に貼り付けてください。

```
<script type="text/javascript" src="https://api.geolonia.com/v1/embed?geolonia-api-key=YOUR-API-KEY"></script>
```

次に、地図を表示したい場所に、以下のような HTML を記述してください。

```
<div
  class="geolonia" style="width: 100%; height: 300px;"
  data-lat="35.7101"
  data-lng="139.8107"
  data-zoom="16"
></div>
```

<p class="codepen" style="text-align: right;"><a href="https://codepen.io/geolonia/pen/XWbYMGW">CodePen でサンプルをみる</a></p>

[詳しくは Geolonia の公式ドキュメントを御覧ください。](https://docs.geolonia.com/)

### その他のサンプル

Geolonia では、CodePen にていくつかのサンプルを公開しています。以下に、代表的なものをいくつかご紹介します。

* [JavaScript API を使用した地図のテンプレート](https://codepen.io/geolonia/pen/XWbYMGW)
* [JavaScript で地図のバックグラウンド画像を設定](https://codepen.io/geolonia/pen/LYVmLrK)
* [カラーピッカーで地図の背景色をダイナミックに変更](https://codepen.io/geolonia/pen/jOPzjQz)
* [GeoJSON を読み込んで複数のマーカーを色分け表示](https://codepen.io/geolonia/pen/zYGRgdq)

## 今後の予定

現在ダッシュボードの開発を行っており、独自ドメインでの運用に関しましては、一部のユーザーの皆様に対してのみご提供しております。

ダッシュボードの一般公開に関しましては、もうしばらくお待ち下さい。

あと、弊社のメインのプロダクトである地図に関しても、現在レイヤー構造の設計の見直し等をすすめており、アップデートが遅れがちになっています。

βテスト期間中は、月に1回程度のアップデートで運用していくと思いますが、ご理解のほどよろしくお願いいたします。

## GitHub Pages を無料とさせいただく理由

私たちの製品は、[Mapbox](https://www.mapbox.com/) 社の [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/) というオープンソースプロジェクトに大きく依存しており、地図の基盤も [OpenStreetMap](https://www.openstreetmap.org/) を始めとする様々なオープンソースプロジェクトに依存しています。

そして、私たち自身も同様にオープンソースのエコシステムに貢献していきたいと強く願っています。

さらに、ひとりでも多くの皆様にお試しいただくには、一つでもたくさんのサンプルコードやユースケースを皆さんに作って頂く必要があると感じています。

まだまだ、多くの課題があるサービスではありますが、さいわい JavaScript API に関しましては、プログラミング初心者の皆様にも親しみやすい API になったのではないかと自負しております。

以上、今後とも宜しくお願いいたします。
