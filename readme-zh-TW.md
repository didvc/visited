[English](readme.md) · [日本語](readme-ja.md) · 繁體中文 · [Deutsch](readme-de.md) · [Français](readme-fr.md)

# Visited-CLI

<!-- Securely collect browsing history over browsers with search capability and extras -->
安全地跨瀏覽器收集瀏覽紀錄。

## 快速上手

以下是入門指南。

首先，clone 儲存庫並切換到該目錄。

```
$ git clone https://github.com/didvc/visited && cd visited
```

接著安裝 Node 套件。

```
$ npm install
```

然後為瀏覽器產生用戶端程式。請執行下列指令。

```
$ node visited.js --generate
✔ Port number? [default: 5555] …
File generated: ./visited.user.js
```

產生 `visited.user.js` 檔案後，將檔案內容複製貼上到你慣用的使用者腳本管理器（例如 [Tampermonkey](https://www.tampermonkey.net/)），作為一個新的使用者腳本。

另外，你也可以把同一份內容貼到其他瀏覽器與 Chrome 設定檔中，實質上將它們的瀏覽紀錄整合到同一個地方。

接下來啟動伺服器。使用 `-s` 或 `--server`。另外，`--quiet` 用於在背景執行，`--port` 用於指定連接埠號碼。

```
$ node visited.js --server
```

這樣就準備完成了。試著前往任何網站，例如 youtube.com，然後重新載入頁面（或直接從網址列造訪）。

你會看到伺服器偵測到你的造訪，並自動將 URL、主機與日期存入資料庫 `visited.db`。

```
$ node visited.js --server
server started...
message: {"url":"https://www.youtube.com/","host":"www.youtube.com"}
```

現在你可以使用 SQLite 用戶端（例如 [DB Browser for SQLite](https://sqlitebrowser.org/dl/)），或是像下面這樣使用內建的搜尋選項。

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

搜尋字串支援正規表示式。下面的指令會得到與上面相同的結果。

```
$ node visited.js --search --url 'you.*be\.com'
```

## 需求

```
git
build-essential
node
sqlite3-pcre (for searching)
```

## 說明

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
