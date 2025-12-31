# cURLでREST APIコールを行う方法

[![Promo](https://github.com/luminati-io/LinkedIn-Scraper/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.jp/) 

このガイドでは、cURLを使用してGET、POST、PUT、DELETEなどのREST APIリクエストを行う方法と、Web Unlockerプロキシを活用して効率を高める方法を解説します。

- [cURL Installation](#curl-installation)
- [How to Use cURL](#how-to-use-curl)
  - [Making a GET Request](#making-a-get-request)
  - [Making a POST Request](#making-a-post-request)
  - [Making a PUT Request](#making-a-put-request)
  - [Making a DELETE Request](#making-a-delete-request)
- [cURL with Web Unlocker](#curl-with-web-unlocker)
- [What Other Options Are There?](#what-other-options-are-there)
- [Conclusion](#conclusion)

## cURL Installation

cURLは現在、Linux、macOS、Windowsを含む主要なオペレーティングシステムのほとんどにプリインストールされています。次のコマンドでcURLのインストール状況を確認できます。

```bash
curl --version
```

cURLが正しくインストールされている場合、cURLのバージョンやビルドに関する情報が表示されます。cURLがインストールされていない場合は、ダウンロードページの[こちら](https://curl.se/download.html)で、お使いのOSに合致するバージョンを見つけられます。

## How to Use cURL

### Making a GET Request

`GET` は、Webブラウザがページを取得するたびに使用する最も一般的なHTTPリクエストです。cURLでは、`GET` フラグを使用してこれを実行します。以下の例では、`https://jsonplaceholder.typicode.com/posts` に `GET` を送信します。

```bash
curl -X GET https://jsonplaceholder.typicode.com/posts
```

以下は、上記リクエストに対するレスポンスの一部です。

```json
{
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
  },
  {
    "userId": 1,
    "id": 2,
    "title": "qui est esse",
    "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"
  },
  {
    "userId": 1,
    "id": 3,
    "title": "ea molestias quasi exercitationem repellat qui ipsa sit aut",
    "body": "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut"
  },
  {
    "userId": 1,
    "id": 4,
    "title": "eum et est occaecati",
    "body": "ullam et saepe reiciendis voluptatem adipisci\nsit amet autem assumenda provident rerum culpa\nquis hic commodi nesciunt rem tenetur doloremque ipsam iure\nquis sunt voluptatem rerum illo velit"
  },
  {
    "userId": 1,
    "id": 5,
    "title": "nesciunt quas odio",
    "body": "repudiandae veniam quaerat sunt sed\nalias aut fugiat sit autem sed est\nvoluptatem omnis possimus esse voluptatibus quis\nest aut tenetur dolor neque"
  },

```

### Making a POST Request

`POST` リクエストは、サーバーに情報を送信してデータベースに保存します。以下の例では、APIを使用して新しい投稿を作成するために `POST` を送信します。

```bash
curl -X POST https://jsonplaceholder.typicode.com/posts \
     -H "Content-Type: application/json" \
     -d '{
           "title": "foo",
           "body": "bar",
           "userId": 1
         }'

```

リクエストに対するレスポンスには、実際の投稿オブジェクトが含まれます。

```json
{
  "title": "foo",
  "body": "bar",
  "userId": 1,
  "id": 101
}
```

### Making a PUT Request

データベースにすでに存在するオブジェクトを編集するには、`PUT` リクエストを使用します。以下の例では、先ほどの投稿本文を `bar` から `updated bar` に更新します。

```bash
curl -X PUT https://jsonplaceholder.typicode.com/posts/1 \
     -H "Content-Type: application/json" \
     -d '{
           "id": 1,
           "title": "foo",
           "body": "updated bar",
           "userId": 1
         }'

```

cURLは、上記リクエストを送信した後、投稿の更新後本文を出力します。

```json
{
  "id": 1,
  "title": "foo",
  "body": "updated bar",
  "userId": 1
}
```

### Making a DELETE Request

`DELETE` リクエストは、一意の識別子（この場合は `1`）を使って、データベースから既存のオブジェクトを削除するために使用します。以下がそのリクエストを実行するコマンドです。

```bash
curl -X DELETE https://jsonplaceholder.typicode.com/posts/1
```
レスポンスは空のJSONオブジェクトで、これは投稿が削除されたことを意味します。

```json
{}
```

## cURL with Web Unlocker

cURLを[Web Unlocker](https://brightdata.jp/products/web-unlocker)と併用する場合、標準のcURLと同じ方法でHTTPリクエストを実行できます。ただし、Web Unlockerは、プロキシ対応、ジオターゲティング、CAPTCHA解決を提供することで機能を強化し、利用可能な中でも特に信頼性の高いプロキシによって支えられています。

Web Unlockerをセットアップしたら、認証のためにusername、zone name、passwordを必ず保存してください。以下の例は、USベースのプロキシを使用するように接続を設定する方法を示しています。

```bash
curl -i --proxy brd.superproxy.io:33335 --proxy-user brd-customer-<YOUR_USERNAME>-zone-<YOUR_ZONE_NAME>-country-us:<YOUR_PASSWORD> -k "https://geo.brdtest.com/mygeo.json"
```

- `-i`: cURLに対し、デバッグ用途に役立つレスポンスのヘッダーを含めるよう指示します。
- `--proxy brd.superproxy.io:33335 --proxy-user brd-customer-<YOUR_USERNAME>-zone-<YOUR_ZONE_NAME>-country-us:<YOUR_PASSWORD>`
  - `--proxy brd.superproxy.io:33335`: 指定されたアドレスにあるプロキシ `brd.superproxy.io:33335` を使用するよう指定します。
  - `--proxy-user brd-customer-<YOUR_USERNAME>-zone-<YOUR_ZONE_NAME>-country-us:<YOUR_PASSWORD>`: `<username>:<password>` 形式の認証文字列を表します。Web Unlockerでは、完全なusernameに次のすべてが含まれます: `brd-customer-<YOUR_USERNAME>-zone-<YOUR_ZONE_NAME>-country-us`。
- `k` は、SSL証明書の検証をバイパスしたいことをcURLに伝えます。

以下はレスポンス例です。場所が `New Jersey` として表示されていることに注意してください。

```json
{"country":"US","asn":{"asnum":20473,"org_name":"AS-VULTR"},"geo":{"city":"Piscataway","region":"NJ","region_name":"New Jersey","postal_code":"08854","latitude":40.5511,"longitude":-74.4606,"tz":"America/New_York","lum_city":"piscataway","lum_region":"nj"}}
```

## What Other Options Are There?

cURLとHTTPを十分に理解できたら、実質的にあらゆる文脈でHTTPを利用できます。一般的なAPIテストには、[Postman](https://www.postman.com/)や[Insomnia](https://insomnia.rest/)のようなGUIツールが優れた選択肢です。

Pythonでは、Requestsのようなライブラリを利用したり、スクリプト内にcURLを直接組み込んだりすることも可能です。JavaScriptでは、Node-FetchやAxiosなどのツールがあり、HTTPリクエストの自動化に利用できます。

コマンドラインツールを好む場合も、検討できる優れた選択肢がいくつかあります。[HTTPie](https://httpie.io/)やwgetのようなツールは、コマンドラインからHTTPリクエストを扱うための強力なユーティリティです。

## Conclusion

cURLは何十年にもわたりコマンドラインの標準であり、近いうちに変わることはないでしょう。しかし、高度なアンチボット保護を回避する必要がある場合は、[Web Unlocker](https://brightdata.jp/products/web-unlocker)をお試しください。お好みのプログラミング言語で使用できるシンプルなAPIを備え、インテリジェントなプロキシ管理も含まれています。