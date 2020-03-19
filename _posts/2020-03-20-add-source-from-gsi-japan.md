---
layout: post
title: "国土地理院のベクトルタイルのスタイルを Maputnik でカスタマイズ"
background: /img/20200320/gsi-vector.png
excerpt: Geolonia の JavaScript API が実運用可能なクオリティに達したと判断しまして、ようやく皆様にお試しいただくことができるようになりました。
author: miya
---

昨日、国土地理院のベクトルタイル "地理院地図 Vector" が公開されました。

[ウェブ地図を自分でデザイン！～地理院地図Vector（仮称）を全国データ公開～](https://www.gsi.go.jp/johofukyu/johofukyu200318.html)

国土地理院さんが、公開したベクトルタイルは、Geolonia の地図と同じフォーマットの Mapbox GL JS ベースなので、さっそく取り込んで試してみました。

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="html,result" data-user="miya0001" data-slug-hash="dyoKzEN" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="GSI Japan + OSM">
  <span>See the Pen <a href="https://codepen.io/miya0001/pen/dyoKzEN">
  GSI Japan + OSM</a> by Takayuki Miyauchi (<a href="https://codepen.io/miya0001">@miya0001</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

上の地図の中で、ピンクの部分が地理院地図から取り込んだ「建物」で、黒い輪郭のものが Geolonia の地図に含まれる OpenStreetMap のデータにある建物です。

というわけで、国土地理院の地図のスタイルを Maputnik というツールを使ってブラウザでカスタマイズする方法をご紹介します。

## Maputnik を準備する

Geolonia や 国土地理院の地図は、[Mapbox](https://www.mapbox.com/) 社の [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/) というオープンソースプロジェクトを使用していて、スタイルをカスタマイズするためのツールも、オープンソースプロジェクトが存在しています。それが今回紹介する Maputnik です。

[https://maputnik.github.io/](https://github.com/geolonia/midnight)

Maputnik はブラウザで動作するツールなので、今回は Geolonia のスタイルをベースに Maputnik でごにょごにょやっていきましょう。

以下の GitHub リポジトリは、Geolonia の "Midnight" というスタイルです。

[https://github.com/geolonia/midnight](https://github.com/geolonia/midnight)

Geolonia は、すべてのスタイルを GitHub 上に公開していて、それぞれの README に "DEMO on editor" というリンクがはってあります。

[https://editor.geolonia.com/#0.91/0/0](https://editor.geolonia.com/#0.91/0/0)

そこをクリックすると以下のような画面が開くと思います。

これからこの画面上で、地理院地図のレイヤーを読み込んで、スタイルを適用していきます。

![](https://www.evernote.com/l/ABU_OdhAOZdJfqOl2dWThHcgxwG7-w9uPoMB/image.png)

<div class="alert alert-warning" style="font-size: 80%;">
以降、Geolonia の地図および API をベースにして説明しますが、もちろんどさくさ紛れに使わせたいからというのもありますが（笑）、うちは GitHub ページでは無料なので、サインアップ無しで動く状態ですぐに試せるという理由によるものです。
</div>

## 地理院地図のデータソースを登録する

まず、データソースを登録します。専門用語的なものがちょくちょく出てきますがあまり重要ではないので気にしないでください。

Maputnik の上部にあるメニューの 「Data Sources」をクリックしてください。

![](https://www.evernote.com/l/ABXcCbX7aC1McrmoUEnHyZYQa3aoZxRXRDgB/image.png)

クリックすると、以下のようなウインドウが開きます。

![](https://www.evernote.com/l/ABWiqdKfDr5FdbtNH5U64n9_Atzg0S5DKoQB/image.png)

その中の赤枠の部分に以下のように入力してください。

<table class="table table-bordered table-striped" style="font-size: 80%;">
  <tr><th>Souce ID:</th><td>gsi-japan</td></tr>
  <tr><th>Source Type:</th><td>Vector (XYZ URLs)</td></tr>
  <tr><th>1st Tile URL:</th><td>https://cyberjapandata.gsi.go.jp/xyz/experimental_bvmap/{z}/{x}/{y}.pbf</td></tr>
  <tr><th>Min Zoom:</th><td>0</td></tr>
  <tr><th>Max Zoom:</th><td>16</td></tr>
</table>

入力が終わったら、[Add Source] というボタンをクリックしてください。このウインドウの 「Active Source」というところに `#gsi-japan` という項目が追加されているはずです。

![](https://www.evernote.com/l/ABXpBd9wHAxPArDBzPmvn14-3DFOKYY7BtQB/image.png)

内容を確認したら右上の [x] をクリックしてウインドを閉じましょう。

## レイヤーを追加する

次に地理院地図のデータソースから読み込んだデータを元にレイヤーを追加して、そのレイヤーにデザインを設定するという作業を行います。

今回は、冒頭で紹介した建物のレイヤー `building` を取り込んで、それにデザインを設定しましょう。

まず、メニューの下側にある [Add Layer] というボタンをクリックしてください。

![](https://www.evernote.com/l/ABUtChgVrcFG7p5GYeEhcwGYayJiHuNPBgYB/image.png)

クリックすると以下のようなウインドウが開きます。

![](https://www.evernote.com/l/ABVN1whTp-dKV4eGSI7MOCJbn-OyWBac5usB/image.png)

このウインドウに以下のように入力してください。

<table class="table table-bordered table-striped" style="font-size: 80%;">
  <tr><th>ID:</th><td>building-gsi-japan</td></tr>
  <tr><th>Type:</th><td>Fill</td></tr>
  <tr><th>Source:</th><td>gsi-japan</td></tr>
  <tr><th>Source Layer:</th><td>building</td></tr>
</table>

まず、`ID` は任意の文字列です。ただし、他のレイヤーと重複するとエラーになりますので、あえて末尾に `-gsi-japan` とつけています。

`Type` はそのレイヤーの型（？）のことで、`Fill` は多角形、`Line` は線、`Symbol` は点だと理解すればいいと思います。他にもいろいろありますが、またいつか。今回は建物（多角形）を置きたいので `Fill` であるべきです。

`Source` は、先程登録したデータソースの `Souce ID` と同じ値であるべきです。

Source Layer については、地理院タイルの仕様から `building` と入力されるべきです。建物がなぜ `building` となるかについては、あとで説明しますね。

以上が終わったら [Add Layer] をクリックしてください。

## デザインを設定する

レイヤーを追加すると、左側のレイヤーのリストの中に `building-gsi-japan` という項目が現れます。

![](https://www.evernote.com/l/ABUHm2g4_WlJk6U4o1CPr3gWZQ3ttmxpI5MB/image.png)

まずこれを上の方にある、`building` の中あたりに引っ越してください。

このレイヤーのリストはそのままレンダリングされるレイヤーの階層にもなっていて、一番下にあると一番上にレンダリングされます。

一番上にレンダリングされてしまうと、お店の名前などの文字の上に乗っかってしまうので、以下のようにドラッグアンドドロップして引っ越してください。

![](https://www.evernote.com/l/ABVPi-0p769FwY8w5eMt6lY1pHQYsHyL4k4B/image.png)

次に、`building-gsi-japan` をクリックして、右側の 「Paint Properties」の中にある `Color` をクリックするとカラーパレットが開きますので、そこで色を変えてみてください。

![](https://www.evernote.com/l/ABVIWlgTH-BOppUrNDsNCU6HHdZwiaW9Gm0B/image.png)

すると、地図の中にある建物の色が変わると思います。それらが地理院地図から取り込んだ建物となります。

あと、このままだと、たまにポリゴンの形状がぶっ壊れた建物が出てくると思います。それを防ぐために以下のようにフィルターを設定して、ぶっこわれたポリゴンがレンダリングされないようにしておくといいです。

![](https://www.evernote.com/l/ABWpB3XEb4VFwb0KmJEh7qaNBX-2nDyVtyIB/image.png)

やや説明は長くなりましたが、やってみれば数回の手順なので、10分以内で試すことができると思います。

## 地理院地図の仕様

地理院地図に含まれる Source Layer は、GitHub の 「地理院地図Vector（仮称）提供実験」のリポジトリからリンクされている「地物コード及び表示ズームレベル一覧」に記載されています。

* GitHub リポジトリ: [https://github.com/gsi-cyberjapan/gsimaps-vector-experiment](https://github.com/gsi-cyberjapan/gsimaps-vector-experiment)
* 地物コード及び表示ズームレベル一覧: [https://maps.gsi.go.jp/help/pdf/vector/dataspec.pdf](https://maps.gsi.go.jp/help/pdf/vector/dataspec.pdf)

この PDF 内の表の `source-layer` という列の値が、レイヤーを追加したときに入力した `Source Layer` に入力されるべき値です。

`Type` については、データタイプの中の値を `点` => `Symbol`、`線` => `Line`、`面` => `Fill` のように脳内翻訳して入力してください。

## 作ったスタイルをネットでシェアする

たぶん一番手っ取り早い方法は、つくったスタイルを [Export] でダウンロードして [Gists](https://gist.github.com/) にはりつけて、[Raw] をクリックして得られる生ファイルまでの URL を CodePen 上に作った地図に表示するという方法かなと思います。

冒頭でお見せした地図はこの方法でやっています。

[https://codepen.io/miya0001/pen/dyoKzEN](https://codepen.io/miya0001/pen/dyoKzEN)

Geolonia の地図は、CodePen 上でも無料で使えるという超親切設計なので、ぜひFork して遊んでみてください。

## お問い合わせ

弊社に対するお問い合わせは、以下のフォームからどうぞ。

[https://geolonia.com/contact/](https://geolonia.com/contact/)
