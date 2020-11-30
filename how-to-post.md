# blog.geolonia.com

## ブログの投稿方法

### はじめに

[blog.geolonia.com](https://blog.geolonia.com) は [Jekyll](https://jekyllrb.com/) という静的ウェブサイトのジェネレーターを使って生成されています。
また、ファイルの配信は [Netlify](https://www.netlify.com/) というサービスを用いています。
新しい投稿や画像の追加、記事の修正などを元データに反映して GitHub に変更をプッシュすると、HTML を含むブログの静的ファイル一式が自動的にサーバー上で生成されサイトが更新される仕組みになっています。

### ファイル構成のルール

以下のディレクトリにマークダウン形式のテキストファイルまたは画像ファイルを追加することで記事や固定ページを追加できます。

| ディレクトリ | 内容     |
| :------------- | :------------- |
| [`_posts`](https://github.com/geolonia/blog.geolonia.com/tree/master/_posts)| 個別のブログ記事のマークダウンファイルを格納する       |
| [`_pages`](https://github.com/geolonia/blog.geolonia.com/tree/master/_pages)| 個別の固定ページのマークダウンファイルを格納する       |
| [`img`](https://github.com/geolonia/blog.geolonia.com/tree/master/img)| 画像ファイルを格納する。ファイルは、 各マークダウンのファイルから絶対パス（例: `/img/image.jpg`) でアクセスできる |

### GitHub の UI からファイルを追加する

ファイルのアップロード、またはブラウザ上のテキストエディタを使ってファイルを追加することができます。当プロジェクトに書き込み権限がない場合は、プロジェクトをフォークすることで同じ操作が可能です。

[テキストエディタを使ってブログ投稿を追加する](https://github.com/geolonia/blog.geolonia.com/new/master/_posts)

![pre commit](./img/_readme/020_precommit.png)

ページ下部の `Commit new file` に表示されているフォームにタイトルや概要を入力することで、今回のブログ投稿に関する変更履歴を Git の機能で記録することができます。

レビューなしでブログを更新する場合は `Commit directly to master branch.` を、プルリクエストのレビュー機能を使う場合は `Create a new branch for this commit and start a pull request.` を選択して任意のブランチ名を指定してください。

### デプロイプレビューを活用する

プルリクエストのレビューの際にデプロイプレビューを利用できます。これは、プレビュー用の URL を発行してプルリクエストがマージされた状態でのウェブサイトを作成し、目視でのレビューを実現するための機能です。master ブランチに対するプルリクエストを作成すると Netlify によって自動的に作成されます。

![deploy preview](./img/_readme/040_deploypreview.png)

GitHub のプルリクエストのページにデプロイプレビューのステータスが表示されます。ステータスが `Deploy preview ready!` になった後でリンクをクリックするとデプロイプレビューにアクセスできます。プルリクエストのレビュワーはこの一時的なウェブサイトにアクセスして表示を確認しながらレビューを進めることができます。
