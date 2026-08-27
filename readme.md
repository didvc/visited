
# Visited-CLI

<!-- Securely collect browsing history over browsers with search capability and extras -->
Securely collect browsing history over browsers.

<!-- BEGIN gh-mutual-linking -->

### Related projects

- [**histbak**](https://github.com/didvc/histbak) — Scheduled, compressed, optionally encrypted backups of your browsing history, plus a viewer that makes it readable. Local only, no network access…
- [**better-super-simple-highlighter**](https://github.com/didvc/better-super-simple-highlighter) — Better Super Simple Highlighter - a Chrome extension (MV3), text highlighting for web pages. The enhanced fork of…
- [**simple-desktop-replay**](https://github.com/didvc/simple-desktop-replay) — Always-on rolling replay buffer for the Windows desktop: a low-overhead RAM DVR that keeps the last few minutes of screen so you can save the…
- [**auto-input**](https://github.com/distrokid-userjs/auto-input) — Userscript that auto-fills the DistroKid upload form from a JSON preset.
- [**discord-data-package-explorer-static**](https://github.com/didvc/discord-data-package-explorer-static) — Pure static, zero-telemetry GitHub Pages version of Discord Data Package Explorer. All processing happens in your browser.
- [**videos-to-tomontage-thumbnails**](https://github.com/didvc/videos-to-tomontage-thumbnails) — Generate thumbnail montages from video files to quickly identify and browse your video collection
- [**mva**](https://github.com/didvc/mva) — mva (mv-archive) - rclone backup/archiving simpler, efficient, and graceful. Just mv files to trigger automatic compression and cloud upload.
- [**core**](https://github.com/URL-Note-Taker/core) — URL Note Taker is a userscript that allows you to take notes on any webpage. Built with Preact, it provides a modern and intuitive user interface.
- [**ytnote**](https://github.com/didvc/ytnote) — A note taking app for YouTube and many more. Fully works on Chrome, Firefox, Safari. Built on React.js.
- [**regex-bookmarks**](https://github.com/didvc/regex-bookmarks) — Regular-expression compatible bookmarks searching capability on Chrome
- [**scrapbook**](https://github.com/didvc/scrapbook) — Collecting images and photos like a pro.
- [**jseval**](https://github.com/didvc/jseval) — Evaluate JavaScript on a URL through headless Chrome browser.
- [**note-cli**](https://github.com/didvc/note-cli) — Markdown Indexing and Pcre Regular Expression Compatible Full Text Searching for Advanced Note Takers.
- [**Google-Search-URL-Filter**](https://github.com/didvc/Google-Search-URL-Filter) — Google Search URL Filter
<!-- END gh-mutual-linking -->

## Getting started  

Here is the getting started guide. 

Firstly, clone the git, and change to the directory.

```
$ git clone [repo url] && cd visited 
```

And install the node packages.

```
$ npm install 
```

Next, generate a client program for browser. Run the following.

```
$ node visited.js --generate
✔ Port number? [default: 5555] …
File generated: ./visited.user.js
```

Now you have `visited.user.js` file generated, copy and paste the file content as your new userscript on your favorite userscript manager e.g. [tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en)

Also note that you can paste the same to your browsers, Chrome profiles, and virtually integrate browsing history at the one place. 

Next, start the server. Use `-s` or `--server`. Also note that `--quiet` for background run, `--port` for specifying the port number. 

```
$ node visited.js --server
```

Now you're ready. Try go to any website, let's say youtube.com, and reload page (or just visit from the omnibox). 

You can see the server detects your visiting and automatically saves the URL, host, date to the database `visited.db`.

```
$ node visited.js --server
server started...
message: {"url":"https://www.youtube.com/","host":"www.youtube.com"}
```

Now you can use a sqlite client such as [DB Browser for SQLite](https://sqlitebrowser.org/dl/), or built-in searching options, just like the following. 

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

The search term is regex compatible. This shows the same result as the above. 

```
$ node visited.js --search --url 'you.*be\.com'
```

## Requirements

```
git
build-essential
node
sqlite3-pcre (for searching)
```

## Help 

```
$ node visited.js
Usage: visited [options]

Options:
  -s, --server               set command type: server
  -p, --port <port>          (server) specify port number (default: 5555)
  -t, --timezone <timezone>  (server) specify timezone (default: "Asia/Tokyo")
  -q, --quiet                (server) disable log
  -s, --search               set command type: search
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