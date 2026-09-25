[English](readme.md) · 日本語 · [繁體中文](readme-zh-TW.md) · [Deutsch](readme-de.md) · [Français](readme-fr.md)

# Visited-CLI

<!-- Securely collect browsing history over browsers with search capability and extras -->
ブラウザをまたいで閲覧履歴を安全に収集します。

## はじめに

はじめ方のガイドです。

まず、リポジトリをクローンしてディレクトリに移動します。

```
$ git clone https://github.com/didvc/visited && cd visited
```

次に、Nodeのパッケージをインストールします。

```
$ npm install
```

続いて、ブラウザ用のクライアントプログラムを生成します。次を実行してください。

```
$ node visited.js --generate
✔ Port number? [default: 5555] …
File generated: ./visited.user.js
```

`visited.user.js` ファイルが生成されたら、その内容をコピーして、お使いのユーザースクリプトマネージャー（例：[Tampermonkey](https://www.tampermonkey.net/)）に新しいユーザースクリプトとして貼り付けます。

同じものをほかのブラウザやChromeのプロファイルにも貼り付ければ、それらの閲覧履歴を事実上1か所にまとめられます。

次に、サーバーを起動します。`-s` または `--server` を使います。なお、`--quiet` はバックグラウンドでの実行用、`--port` はポート番号の指定用です。

```
$ node visited.js --server
```

これで準備完了です。どこかのウェブサイト、たとえば youtube.com にアクセスして、ページを再読み込みしてみてください（またはアドレスバーから開くだけでも構いません）。

サーバーがアクセスを検知し、URL、ホスト、日時を自動的にデータベース `visited.db` に保存するのがわかります。

```
$ node visited.js --server
server started...
message: {"url":"https://www.youtube.com/","host":"www.youtube.com"}
```

あとは、[DB Browser for SQLite](https://sqlitebrowser.org/dl/) のようなSQLiteクライアントか、次のような組み込みの検索オプションを使えます。

```
$ node visited.js --search --host youtube.com
[
    {
        "id": 1,
        "url": "https://www.youtube.com/",
        "host": "www.youtube.com",
        "date": "6/23/2021, 3:52:02 PM",
        "timestamp": 1624431122
    }
]
```

検索語は正規表現に対応しています。次のコマンドでも上と同じ結果になります。

```
$ node visited.js --search --url 'you.*be\.com'
```

## 動作要件

```
git
build-essential
node
sqlite3-pcre (for searching)
```

## ヘルプ

```
$ node visited.js
Usage: visited [options]

Options:
  -s, --server               set command type: server
  -p, --port <port>          (server) specify port number (default: 5555)
  -t, --timezone <timezone>  (server) specify timezone (default: "Asia/Tokyo")
  -q, --quiet                (server) disable log
  -S, --search               set command type: search
  -r, --regex                (search) enable regex extension for search (default: true)
  -u, --url <url>            (search) search by url (default: ".")
  --host <host>              (search) search by host (default: ".")
  --order <order>            (search) set order for search [desc, asc] (default: "desc")
  --limit <number>           (search) set limit for search (default: -1)
  -F, --format <format>      (search) output format [json, url] (default: "json")
  --pcre-path <file>         set sqlite3 pcre file path for search (default: "/usr/lib/sqlite3/pcre.so")
  -d, --database <file>      specify database file for index/search (default: "./visited.db")
  --generate                 generates client side userScript file
  --delete-database          delete database
  -y, --yes                  no confirmation prompt
  -h, --help                 display help for command
```

<!-- BEGIN gh-mutual-linking -->

### Related projects

- [histbak](https://github.com/didvc/histbak): Scheduled, compressed, optionally encrypted backups of your browsing history, plus a viewer that makes it readable. Local only, no network access. Chrome + Firefox, MV3.
- [better-tab-session-manager](https://github.com/didvc/better-tab-session-manager): Tab Session Manager fork with scheduled, incremental session export to disk (hourly/daily/weekly). Upstream only backs up once at browser startup.
- [better-super-simple-highlighter](https://github.com/didvc/better-super-simple-highlighter): Super Simple Highlighter, the text highlighter Chrome extension, super enhanced.
- [astro-html-editor](https://github.com/didvc/astro-html-editor): Self-hosted HTML editor with live preview. Astro SSR + plain JavaScript, server-side file persistence.
- [chatnote](https://github.com/didvc/chatnote): Self-hosted note-to-self chatrooms. Privacy-first by design, infinite rooms, Markdown, ephemeral/incognito room types, image uploads, tags, JSON import/export. Astro SSR + SQLite.
<!-- END gh-mutual-linking -->
