---
layout: post
title: "Netlifyでサブドメインをコミュニティに使ってもらうTips"
background: /img/20200503/screenshot.png
excerpt: Netlify でチームを跨いでサブドメインを設定する際のつまりどころを解消する方法について紹介します。
author: kamataryo
---

先日リリースして多くの地域で使い始めていただいている[イエメシ](https://iemeshi.jp)では、`iemeshi.jp`のサブドメイン（`*.iemeshi.jp`）を発行して各地のコミュニティの皆さんに使っていただいています。これは [Code for Kanazawa](https://codeforkanazawa.org/) さんの[5374 ゴミナシ.jp](http://5374.jp/)のプロジェクトを参考にしたもので、イエメシが推奨している[Netlify](https://www.netlify.com/)を使ったホスティング環境に対して簡単にサブドメインを発行できるようになっています。

当初プロジェクトメンバーが作った[kushimoto.iemeshi.jp](https://kushimoto.iemeshi.jp)や[hikone.iemeshi.jp](https://hikone.iemeshi.jp)に対してはこの仕組がはうまく動いていたのですが、早速フォークしていただいた方からカスタムドメインを設定できない、というバグ報告をいただきました。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">ありがとうございます！<br>SSL設定にはカスタムドメイン設定が必要だと思うのですが、カスタムドメイン設定をすると、すでに使われていますと表示されます。<br>方法が間違っていますでしょうか？ <a href="https://t.co/gKH5jiQv0R">pic.twitter.com/gKH5jiQv0R</a></p>&mdash; りょうのすけ (@rnosuke) <a href="https://twitter.com/rnosuke/status/1255777294141935616?ref_src=twsrc%5Etfw">April 30, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## Netlify のチームとドメイン、サブドメイン

どうやら Netlify に Apex ドメイン（`iemeshi.jp`）のサイトが存在すると、チーム外部のユーザーはそのサブドメイン（`*.iemeshi.jp`）を利用することができないようです。当初の構成では、Geolonia チームが`iemeshi.jp`のサイトと全ての`*.iemeshi.jp`を所有している状態でした。リリース後にチームの外部の方に`*.iemeshi.jp`を使って貰おうとして初めて上記のエラーが発生した、というわけです。

![](/img/20200503/01.png)

Netlify で Apex ドメインのサイトをホストしなければこのエラーが発生しないことが分かりましたので、`iemeshi.jp`だけを Netlify ではない別のサービス（今回は GitHub Pages を使っています）に移すことでこの問題を解消しました。

![](/img/20200503/02.png)

Netlify を使ってサブドメインをコミュニティに提供するサービスを作成するときの参考になればと思います。
