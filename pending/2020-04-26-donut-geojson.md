---
layout: post
title: "Geolonia の地図で穴あきのポリゴン（ドーナツ）を表現する"
background: /img/20200426/background.jpg
excerpt: Geolonia の地図で穴あきのポリゴン（ドーナツ）を表現する方法について解説します。
author: kamataryo
---

<p style="text-align: right; font-size: 80%;">Photo by <a href="https://www.flickr.com/people/16133272@N00">TownePost Network</a> on <a href="https://www.flickr.com/">flickr</a>, licensed under <a href="hhttp://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a></p>


## GeoJSON を Geolonia の地図で扱う



## 複雑なポリゴン

1つのポリゴン内で複数の領域を使用可能にすると、様々な形のポリゴンを考えることができます。例えば以下のような種類のポリゴンです。

- 複数の領域があるポリゴン
- 重複する領域があるポリゴン
- 穴の空いたポリゴン（ドーナツ）

![いろいろなポリゴン](/img/20200426/polygons.png)

GeoJSONのフォーマットでは、 `geometry.coordinates` の値に複数の領域を指定することでこれらのポリゴンが表現できます。

```json
{
  "type": "Polygon",
  "coordinates": [
    [ /* 領域1の座標 */ ],
    [ /* 領域2の座標 */ ],
    ...
  ]
}
```

<div
  class="geolonia"
  data-navigation-control="off"
  data-geojson="#geojson-sample-2"
></div>
<script type="application/json" id="geojson-sample-2">
{
  "type": "FeatureCollection",
  "features": [
 {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [
              136.78802490234375,
              35.131140628613615
            ],
            [
              137.35107421875,
              35.131140628613615
            ],
            [
              137.35107421875,
              35.36889537510474
            ],
            [
              136.78802490234375,
              35.36889537510474
            ],
            [
              136.78802490234375,
              35.131140628613615
            ]
          ],
          [
            [
              137.02972412109375,
              35.24113278166642
            ],
            [
              137.57904052734375,
              35.24113278166642
            ],
            [
              137.57904052734375,
              35.54787066533268
            ],
            [
              137.02972412109375,
              35.54787066533268
            ],
            [
              137.02972412109375,
              35.24113278166642
            ]
          ]
        ]
      }
    }
  ]
}
</script>

ドーナツについては少しコツがあるため、


## ポリゴン、あるいは穴

私たちが無限の広がりを持つ平面上の空間で生活しているのであれば話は単純なのですが、残念ながら地球は有限です。穴のような図形が存在します。この投稿では、十分に小さい領域で穴とは認識できない領域を単に _ポリゴン_ 、地球のほぼ全てを覆っていて十分に小さい穴を持っている領域を _ホールポリゴン_ と呼ぶことにします。

<figure>
    <img src="/img/20200404/polygon.png"
         alt="ポリゴン">
    <figcaption>ポリゴン</figcaption>
</figure>

<figure>
    <img src="/img/20200404/hole.png"
         alt="ホールポリゴン">
    <figcaption>ホールポリゴン</figcaption>
</figure>

## GeoJSON の

ポリゴンとホールポリゴンは表裏一体で、どんなポリゴンでも 1 対 1 で対応するホールポリゴンを作ることができます。互いに対になるポリゴンとホールポリゴンは、外周のデータを共有します。外周のデータとは、 GeoJSON で言う `geometry.coordinates` を指します。

これは、逆に言うと、1 つのデータからポリゴンとホールポリゴンの 2 通りの解釈が可能と言うことで、これらを区別する仕様が無いかどうか RFC を調べてみました。

## GeoJSON の右手ルール

GeoJSON の RFC である [RFC7946](https://tools.ietf.org/html/rfc7946) を見て見ると、[Polygon の定義](https://tools.ietf.org/html/rfc7946#section-3.1.6)に以下のような記述があります。

> A linear ring MUST follow the right-hand rule with respect to the area it bounds

> 線形リングはその領域に対して右手ルールに従わなければならない

A linear ring とは直線で構成された環、つまりポリゴンやホールの外周を指します。ポリゴンの場合は反時計回りになると言うことです。ホールポリゴンの場合はその外周のデータの順序は半時計回りに、

## ドーナツポリゴン

単体のホールはあまり使い道がありませんし、QGIS などの汎用の
ドーナツを表現する上で重要です。

