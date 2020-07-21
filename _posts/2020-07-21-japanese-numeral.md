---
layout: post
title: 漢数字と数字を相互変換する NPM モジュールを公開しました！
background: /img/20200721/header.jpg
excerpt: NPM モジュール @geolonia/japanese-numeral 公開のお知らせ
author: miya
---

<p style="text-align: right;">Photo by <a href="https://unsplash.com/@charlesdeluvio">Charles Deluvio</a> on <a href="https://unsplash.com/">Unsplash</a></p>

たとえば `二千二十` を `2020` に変換するなど、漢数字と数字を相互変換する NPM モジュールを公開しました。

[https://github.com/geolonia/japanese-numeral](https://github.com/geolonia/japanese-numeral)

## 主な機能

### kanji2number()

`n千兆` 以下の漢数字を数字に変換します。

* `二千二十`（String 型）を `2020`（Number 型）に変換します。
* `二〇二〇` のように `〇`（漢数字の `0`）を使うパターンにも対応しています。
* `千百` と `一千一百` のように `一` を省略したパターンにも対応しています。

### number2kanji()

`n千兆` 以下の数字を漢数字に変換します。

* `1111113111111111` を `千百十一兆千百三十一億千百十一万千百十一` に変換します。
* `2020` を `二千二十` に変換します。

### findKanjiNumbers()

テキストの中から `n千兆` 以下の漢数字を抽出し、配列で返します。

* `今日は二千二十年十一月二十日です。` のようなテキストから漢数字を抽出し `[ '二千二十', '十一', '二十' ]` という配列を返します。
* `今日は二〇二〇年十一月二十日です。` のような漢数字の `0` を使ったパターンの数字も抽出します。

## インストール方法

```
$ npm install @geolonia/japanese-numeral --save
```

## 使い方

[README を御覧ください。](https://github.com/geolonia/japanese-numeral/blob/master/README.md)
