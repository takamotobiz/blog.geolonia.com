---
layout: post
title: "どうしても地元を盛り上げたいと思ったのでベクトルタイルを作って盛り上げた。"
background: /img/20200616/header.jpg
excerpt: ベクトルタイルを作ればあなたの町も必ず盛り上がります。
author: miya
---

<p style="text-align: right;">Photo by <a href="https://unsplash.com/@adityachinchure">Aditya Chinchure</a> on <a href="https://unsplash.com/">Unsplash</a></p>

筆者は和歌山県に住んでいるのですが、先日突然どうしても地元和歌山を盛り上げたい衝動に駆られました。

幸い Mapbox GL JS には、`fill-extrusion` というレイヤータイプがあって、ビル程度ならこんな感じで簡単に盛り上げることができます。

![](/img/20200616/maputnik.png)

しかし、都道府県とか市町村単位で盛り上げることは一筋縄ではいきません。

その理由は、地図上に表示されている都道府県や市区町村などの境界線は、単なる線であって、各地域を表現するポリゴンが実際にそこにあるわけではないからです。

そのため、地域を盛り上げるには、都道府県や市区町村のポリゴンを持つベクトルタイルを作る必要があります。

というわけで実際にベクトルタイルを作って盛り上げてみました。

<p class="codepen" data-height="350" data-theme-id="light" data-default-tab="result" data-user="miya0001" data-slug-hash="XWXjjWL" style="height: 350px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="地元を盛り上げてみた">
  <span>See the Pen <a href="https://codepen.io/miya0001/pen/XWXjjWL">
  地元を盛り上げてみた</a> by Takayuki Miyauchi (<a href="https://codepen.io/miya0001">@miya0001</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

見事に和歌山県が盛り上がっていることがおわかりいただけると思います。やったね！

## 都道府県ベクトルタイルについて

このベクトルタイルは、都道府県ごとに色分け地図を作るなどのデータビジュアライゼーションにご利用いただくことを想定して作りました。

タイルの中には以下の一つのレイヤーしか含まれていません。

レイヤー名: `prefectures`

個々のポリゴンはプロパティに以下の値を持っています。

* `name` - 都道府県名
* `pref` - 都道府県コード

Geolonia の地図は、CodePen 上や GitHub ページでは無料でご利用いただくことができます。

以下の URL でソースコードを編集することができますので、「和歌山県」と書いてある部分を別の都道府県名に書き換えるところから遊んでいただけると幸いです。

とりあえず今回は和歌山を盛り上げた自慢だけですが、後日公式サイトまたはドキュメントでもうすこしちゃんとした情報をお届けします。

## タイルの作成方法について

タイルのビルド方法は以下のリポジトリにあります。

[https://github.com/geolonia/prefecture-tiles](https://github.com/geolonia/prefecture-tiles)

スクリプト等を使用して、弊社のウェブサーバーからバルクダウンロードするような行為は絶対にしないでください。

## 謝辞

都道府県の GeoJSON は地図蔵様からダウンロードさせていただきました。

[https://japonyol.net/editor/article/47-prefectures-geojson.html](https://japonyol.net/editor/article/47-prefectures-geojson.html)
