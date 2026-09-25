[English](readme.md) · [日本語](readme-ja.md) · [繁體中文](readme-zh-TW.md) · Deutsch · [Français](readme-fr.md)

# Visited-CLI

<!-- Securely collect browsing history over browsers with search capability and extras -->
Browserverlauf über mehrere Browser hinweg sicher sammeln.

## Erste Schritte

Hier ist die Anleitung für den Einstieg.

Zuerst das Repository klonen und in das Verzeichnis wechseln.

```
$ git clone https://github.com/didvc/visited && cd visited
```

Dann die Node-Pakete installieren.

```
$ npm install
```

Als Nächstes ein Client-Programm für den Browser erzeugen. Dazu Folgendes ausführen.

```
$ node visited.js --generate
✔ Port number? [default: 5555] …
File generated: ./visited.user.js
```

Sobald die Datei `visited.user.js` erzeugt ist, ihren Inhalt kopieren und als neues Userscript in den bevorzugten Userscript-Manager einfügen, z. B. [Tampermonkey](https://www.tampermonkey.net/).

Dasselbe lässt sich auch in weitere Browser und Chrome-Profile einfügen, um deren Browserverlauf praktisch an einem Ort zusammenzuführen.

Als Nächstes den Server starten, mit `-s` oder `--server`. `--quiet` ist für den Betrieb im Hintergrund gedacht, `--port` für die Angabe der Portnummer.

```
$ node visited.js --server
```

Jetzt ist alles bereit. Einfach eine beliebige Website aufrufen, etwa youtube.com, und die Seite neu laden (oder sie direkt über die Adressleiste öffnen).

Der Server erkennt den Besuch und speichert URL, Host und Datum automatisch in der Datenbank `visited.db`.

```
$ node visited.js --server
server started...
message: {"url":"https://www.youtube.com/","host":"www.youtube.com"}
```

Nun lässt sich ein SQLite-Client wie [DB Browser for SQLite](https://sqlitebrowser.org/dl/) verwenden, oder die eingebauten Suchoptionen, etwa so:

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

Der Suchbegriff ist regex-kompatibel. Folgendes liefert dasselbe Ergebnis wie oben.

```
$ node visited.js --search --url 'you.*be\.com'
```

## Voraussetzungen

```
git
build-essential
node
sqlite3-pcre (for searching)
```

## Hilfe

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
