[English](readme.md) · [日本語](readme-ja.md) · [繁體中文](readme-zh-TW.md) · [Deutsch](readme-de.md) · Français

# Visited-CLI

<!-- Securely collect browsing history over browsers with search capability and extras -->
Collecter l’historique de navigation de plusieurs navigateurs, en toute sécurité.

## Prise en main

Voici le guide de prise en main.

Tout d’abord, clonez le dépôt et placez-vous dans le répertoire.

```
$ git clone https://github.com/didvc/visited && cd visited
```

Ensuite, installez les paquets Node.

```
$ npm install
```

Puis générez un programme client pour le navigateur. Exécutez la commande suivante.

```
$ node visited.js --generate
✔ Port number? [default: 5555] …
File generated: ./visited.user.js
```

Une fois le fichier `visited.user.js` généré, copiez son contenu et collez-le comme nouveau userscript dans votre gestionnaire de userscripts préféré, par exemple [Tampermonkey](https://www.tampermonkey.net/).

Notez aussi que vous pouvez coller le même script dans vos autres navigateurs et profils Chrome, et ainsi réunir virtuellement leur historique de navigation en un seul endroit.

Ensuite, démarrez le serveur avec `-s` ou `--server`. Notez aussi que `--quiet` sert à l’exécuter en arrière-plan, et `--port` à indiquer le numéro de port.

```
$ node visited.js --server
```

Tout est prêt. Allez sur n’importe quel site, par exemple youtube.com, et rechargez la page (ou ouvrez-la simplement depuis la barre d’adresse).

Vous verrez le serveur détecter votre visite et enregistrer automatiquement l’URL, l’hôte et la date dans la base de données `visited.db`.

```
$ node visited.js --server
server started...
message: {"url":"https://www.youtube.com/","host":"www.youtube.com"}
```

Vous pouvez maintenant utiliser un client SQLite comme [DB Browser for SQLite](https://sqlitebrowser.org/dl/), ou les options de recherche intégrées, comme ceci.

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

Le terme recherché est compatible avec les expressions régulières. La commande suivante donne le même résultat que ci-dessus.

```
$ node visited.js --search --url 'you.*be\.com'
```

## Prérequis

```
git
build-essential
node
sqlite3-pcre (for searching)
```

## Aide

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
