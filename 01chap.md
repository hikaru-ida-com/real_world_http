## 1章
* メソッドとパス
* ヘッダー
* ボディ
* ステータスコード


### 1.4 HTTPの先祖(1)　電子メール
HTTPのヘッダーはリクエスト、レスポンスの両方で使われているが、もともとのアイデアはメールから来ている。  
クライアントがサーバーに送るヘッダーの例
* User-Agent  
クライアントが自分のアプリケーション名を入れるところ。curlコマンドの場合はcurl/7.48.0というような文字が入る。
* Referer  
サーバー側で参考にするための追加情報。クライアントがリクエストを送るときに見ていたページのURLを送る。
* Authorization  
特別なクライアントにできるだけ通信を許可する際、認証情報をサーバーに伝える。
  
サーバーからクライアントに返すときに付与するヘッダーの例
* Content-Type  
ファイルの種類を指定。ここにはMINEタイプと呼ばれる識別子を記述する。
* Content-Length  
ボディのサイズ。圧縮がされている場合は圧縮後のサイズ。
* Content-Encoding  
圧縮の形式。
* Date  
ドキュメントの日時  

これ以外に、X-から始まるヘッダーは各アプリケーションが自由に使ってもいいとされている。



### 1.4.1 ヘッダーの送信
curlコマンドでヘッダーを送るには「--header="ヘッダー行"」もしくは「-H ヘッダー行」オプションを使う。

```
curl --http1.0 -H "X-Text: Hello" http://localhost:18888
```

出力
```
GET / HTTP/1.0
Host: localhost:18888
Connection: close
Accept: */*
User-Agent: curl/7.58.0
X-Text: Hello
```

### 1.4.2 ヘッダーの受信
```
curl --http1.0 -H "X-Text: Hello" http://localhost:18888 -v
```

```
* Rebuilt URL to: http://localhost:18888/
* *   Trying 127.0.0.1...
* * TCP_NODELAY set
* * Connected to localhost (127.0.0.1) port 18888 (#0)
* > GET / HTTP/1.0
* > Host: localhost:18888
* > User-Agent: curl/7.58.0
* > Accept: */*
* > X-text: Hello
* >
* * HTTP 1.0,  assume close after body
* < HTTP/1.0 200 OK
* < Date: Sun,  19 Aug 2018 14:27:25 GMT
* < Content-Length: 32
* < Content-Type: text/html; charset=utf-8
* <
* <html><body>hello</body></html>
* * Closing connection 0
```

### 1.4.3
### 1.4.4
### 1.4.5 電子メールとの違い
* ヘッダー＋本文という構造は同じ
* HTTPのリクエストでは先頭にメソッド＋パスの行が追加される
* HTTPのレスポンスでは先頭にステータスコードが追加される


### 1.5 HTTPの先祖(2)　ニュースグループ
マスタースレーブ構造を持ち、使用されていた通信プロトコルがNNTP.
HTTPはNNTPからメソッドとステータスコードの2つの機能を導入している。

### 1.5.1 メソッド
curlコマンドでメソッドを送るには、--request=<メソッド>もしくは、-X <メソッド>のような書式を用いる。
```
curl --http1.0 -X POST http://localhost:18888/greeting 
```
```
POST /greeting HTTP/1.0
Host: localhost:18888
Connection: close
Accept: */*
User-Agent: curl/7.58.0
```
