---
layout: post
title: "無料で利用できてオープンソースのジオコーディング API （住所から緯度経度を検索）を公開しました。"
background: /img/20200601/header.jpg
excerpt: 静的ファイルによる API サービスかつオープンソースなので安心して利用できます。
author: miya
---

<p style="text-align: right;">Photo by <a href="https://unsplash.com/@hendrikmorkel">Hendrik Morkel</a> on <a href="https://unsplash.com/">Unsplash</a></p>

このたび Geolonia では、オープンソースかつ無料でご利用いただける住所から緯度経度を検索する（専門用語でジオコーディングといいます。）ための API を公開しました。

[https://community-geocoder.geolonia.com/](https://community-geocoder.geolonia.com/)

この API は、経産省のオープンソースプロジェクト [「IMI コンポーネントツール」](https://info.gbiz.go.jp/tools/imi_tools/) をフォークしたライブラリを使用しています。

## 特徴

* オープンソースで、静的ファイルによって GitHub Pages でホストされているので、安心してご利用いただくことができます。
* JavaScript API を使用して、みなさんのウェブサイト上で利用することができます。
* 精度は「大字町丁目」までとなっているため、商用のジオコーディングサービスに比べると精度は低いです。
* たとえば某有名ジオコーディングサービスは、その会社の地図以外の地図上では利用できませんが、このサービスではそのような規約上の制約はありません。

<div class="alert alert-primary">
Geolonia では、もうすこし精度が高く、このサービスと同様に自由度の高いジオコーディングサービスの開発も行っていますのでお楽しみに！
</div>

## 開発までの経緯

先日、公開した [IMI コンポーネントツールに関する記事](https://blog.geolonia.com/2020/05/29/imi-tools.html) がとても大きな反響をいただきましたが、この記事を書いている段階で IMI コンポーネントツールのジオコーディグ機能に興味深い点を発見しました。

### IMI コンポーネントツールのジオコーディングの仕組み

IMI コンポーネントツールの「住所変換コンポーネント」では、以下のようなフローで緯度経度を取得しています。

* 住所を同梱の辞書（JSON）を使用して、都道府県名、市町村名などに分解。
* 分解した住所から「大字町丁目コード」というコードを生成。たとえば「東京都千代田区霞が関1-3-1」は「131010002001」という感じ。
* そのコードを同梱の levelDB ベースのキーバリューのストレージ内で検索して緯度経度を取得。

「住所変換コンポーネント」では、この levelDB にアクセスするために Node.js のサーバーとして起動して利用する仕様になっています。

そこで私たち Geolonia の開発チームは、キーバリューのデータを個々の JSON として静的にホスティングすることで、GitHub Pages 上にサーバーレスで API を設置することができるのではないかというアイディアを思いつきました。

こうすれば、IMI コンポーネントツールをクライアントサイドスクリプトとして利用できるように修正したライブラリを JavaScript API として提供することで、ジオコーディングサービスを提供できます。

ラッキーなことに、以前にプライベートで関わったプロジェクトで郵便番号から住所に変換する API を開発したことがありました。

[https://github.com/madefor/postal-code-api](https://github.com/madefor/postal-code-api)

## 利用方法

本サービスは、JavaScript API を使用して、みなさんのウェブサイト等に組み込むことが可能です。

まず、以下の HTML を組み込みたいページの `</body>` タグ直前に設置してください。

```
<script src="https://cdn.geolonia.com/community-geocoder.js"></script>
```

以下の例のように、API 関数 `getLatLng()` を任意のクリックイベント等でコールしてください。

```
document.getElementById('exec').addEventListener('click', () => {
  if (document.getElementById('address').value) {
    getLatLng(document.getElementById('address').value, (latlng) => {
      map.setCenter(latlng)
    })
  }
})
```

[API 関数の引数などの詳しい情報は README を御覧ください。](https://github.com/geolonia/community-geocoder)

## ライセンス、利用規約

* ソースコードのライセンスは MIT ライセンスです。
* 取得した緯度経度の情報のご利用方法に制限はありません。他社の地図、アプリ、その他ご自由にご利用ください。
* できればソーシャルでのシェア、[Geolonia](https://geolonia.com/) へのリンクの設置、弊社ソーシャルアカウントのフォローなどをしていただけると、開発者たちのモチベーションが上がると思います。
