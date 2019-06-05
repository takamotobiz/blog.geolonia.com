---
title: 'TileCloud を使ってオープンデータをビジュアライズしてみよう！'
featured_image: /images/20190604/header.png
excerpt: TileCloud を使ってみる
author: kamataryo
---

TileCloud の特徴的な機能の 1 つが [Embed API](https://docs.tilecloud.io/embed-api/) で、これは簡単な HTML マークアップだけで地図を表示したりカスタマイズするためのものです。Embed API の使い方はとてもシンプルで、例えば次の 3 ステップだけで様々にカスタマイズされた地図を表示できます。

1. 所定の URL から Embed API の JavaScript を読み込む
1. 地図を表示させたい HTML 要素に `.tilecloud` クラスを指定する
1. 地図をカスタマイズするオプションを `data-*` 属性を使って指定する

例えば東京駅を表示する際の HTML のマークアップは次のような形になります。

```html
<html>
  <body>
    <div
      class="tilecloud"
      data-lat="35.6810977"
      data-lng="139.7671707"
      data-zoom="14"
    ></div>
    <script src="https://api.tilecloud.io/dev/embed?tilecloud-api-key=YOUR-API-KEY"></script>
  </body>
</html>
```

<div
  class="tilecloud"
  data-lat="35.6810977"
  data-lng="139.7671707"
  data-zoom="14"
></div>

その他のスタイルやデータを表示するオプションについては[公式ドキュメント](https://docs.tilecloud.io/tutorial/)をご覧ください。

今回は、 Embed API とオープンデータを利用して、簡単なデータビジュアライゼーションを試してみます。

## オープンデータを探そう

アメリカ合衆国の政府の研究機関である U.S. Geological Survey(USGS) が自然災害などに関する全世界の様々なデータをオープンデータとして公開しています。

[U.S. Geological Survey](https://www.usgs.gov/)

データは GeoJSON や KML などの様々な形式でダウンロードできるほか、web API が提供されており、TileCloud を含む様々な Web サービスとマッシュアップして利用することができます。データはパブリックドメインとして利用できます。

[Copyrights and Credits - USGS](https://www.usgs.gov/information-policies-and-instructions/copyrights-and-credits)

今回は、 USGS のウェブサイトから利用できる地震カタログ検索の API から GeoJSON 形式のデータを取得し、TileCloud の地図に表示してみます。

[地震カタログ検索 - USGS](https://earthquake.usgs.gov/earthquakes/search/)

## USGS から GeoJSON のエンドポイントを取得する

[GeoJSON](https://docs.tilecloud.io/tutorial/007/#geojson-%E3%81%A8%E3%81%AF) は、地理空間上の点、ポリゴン（領域）、ポリライン（線）などの**地物**を JSON 形式で表すことができる標準的なデータフォーマットです。
地震カタログ検索から操作して地震の震源地のデータを GeoJSON 形式で取得することができます。

USGS の地震カタログ検索からマグニチュードや期間などのオプションを選択して、

![options](/images/20190604/01_options.png)

データを取得する位置を矩形で選択し、

![rectangle](/images/20190604/02_rectangle.png)

データの出力形式を選択します。

![format](/images/20190604/03_format.png)

`search` というボタンを押すと、例えば以下のような URL に移動します。 この際に GeoJSON のデータが表示されるはずです。このデータは、2019 年 6 月 5 日までの過去 30 日に発生した地震の震源（点データ）の分布を表す GeoJSON です。

```
https://earthquake.usgs.gov/fdsnws/event/1/query.geojson?starttime=2019-05-06%2000:00:00&endtime=2019-06-05%2023:59:59&maxlatitude=53.998&minlatitude=21.028&maxlongitude=161.713&minlongitude=125.151&minmagnitude=-1&orderby=time
```

## TileCloud の地図に GeoJSON を表示する

GeoJSON を TileCloud の地図上に表示するのはとても簡単です。 `<div class="tilecloud"></div>` という要素の `data-geojson` 属性に GeoJSON の URL を指定します。

```html
<div
  class="tilecloud"
  data-geojson="https://earthquake.usgs.gov/fdsnws/event/1/query.geojson?starttime=2019-05-06%2000:00:00&endtime=2019-06-05%2023:59:59&maxlatitude=53.998&minlatitude=21.028&maxlongitude=161.713&minlongitude=125.151&minmagnitude=-1&orderby=time"
></div>
```

<div class="tilecloud" data-geojson="https://earthquake.usgs.gov/fdsnws/event/1/query.geojson?starttime=2019-05-06%2000:00:00&endtime=2019-06-05%2023:59:59&maxlatitude=53.998&minlatitude=21.028&maxlongitude=161.713&minlongitude=125.151&minmagnitude=-1&orderby=time"></div>

日本近海の過去 30 日の震源がクラスター化されて表示されました。
データ配信専用の API を使う以外にも、例えば集めた地物のデータを GeoJSON に変換して GitHub にプッシュし、GitHub Pages などの機能でホストしたりすれば、それらも簡単に表示することができます。

以下の地図では、GitHub のリポジトリ [kamataryo/geojson-samples](https://github.com/kamataryo/geojson-samples/tree/gh-pages) にホストした琵琶湖の島一覧の GeoJSON を読み込んでいます。

```
<div
  class="tilecloud"
  data-geojson="https://kamataryo.github.io/geojson-samples/island-of-biwa-lake.geojson"
>
```

<div
  class="tilecloud"
  data-geojson="https://kamataryo.github.io/geojson-samples/island-of-biwa-lake.geojson"
></div>

TileCloud はオープンデータとの親和性の高いサービスの提供を目指しており、現在はパブリックベータ版サービスの公開を目標に開発を鋭意進めています。公開のあかつきには、ぜひたくさんのフィードバックをいただければと思います。

今後ともよろしくお願いします！
