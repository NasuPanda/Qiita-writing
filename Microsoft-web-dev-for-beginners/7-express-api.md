title APIの概要+Node.js/Expressを使用して簡単なWebAPIを構築する
tag api express node.js 初心者

# はじめに

この教材を進めていると、

[銀行API](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project/api/translations/README.ja.md)のページにこのような記載が。

> しかし、このような API の構築方法に興味があるのであれば、このシリーズのビデオを見ることができます: [https://aka.ms/NodeBeginner](https://aka.ms/NodeBeginner) (ビデオ 17 から 21 では、この API を正確にカバーしています)。

> また、こちらのインタラクティブなチュートリアルもご覧ください: [https://aka.ms/learn/express-api](https://aka.ms/learn/express-api)

APIって何なんだ？感があったこともあり、

せっかくなので[JavaScript を Node.js および Express と共に使用して Web API を構築する - Learn | Microsoft Docs](https://docs.microsoft.com/ja-jp/learn/modules/build-web-api-nodejs-express/?WT.mc_id=squirrelbanking-github-yolasors)をやってみることにしました。

## APIって？

そもそもAPIとは何か。

> APIは「Application Programming Interface」の略です。アプリケーションプログラミングインターフェイス。
> 　例えば「AというファイルをBという名前でコピーをして、作業完了したら、ポップアップウィンドウを出して知らせる！」というプログラムを作るとします。実際にどんな動きをするのかパートに分けてみると……、
>
> 1. Aというファイルを選択
> 2. 実行ボタンを押すと3のステップへ
> 3. データをコピーする
> 4. コピーされたデータをBという名前を付け保存
> 5. ポップアップウィンドウを出して作業完了を告げる
>
> 　この1.〜5.の作業をすべて一から作成すると、かなり手間が掛かります（マウスの動きを計算して、ウィンドウのデザインを考えて……）。そこで登場するのがAPIです。
>
> 1. ファイルを選択するAPI
> 2. ボタンを押すとプログラムを動かすAPI
> 3. データをコピーするAPI
> 4. ファイルに名前を付けるAPI
> 5. ウィンドウを出してメッセージを出すAPI
>
> と、いろいろな機能があるAPIから、必要なAPIを探し出し組み合わせるだけで、プログラムができてしまうのです。つまりAPIは「特定の機能を持つプログラム部品」なのです。よく使われる命令をAPIにしてみんなで共有してしまえば、非常に効率的に作業ができますね。
>
> ![API](http://image.itmedia.co.jp/ait/articles/0703/13/r85minapi_01.gif)
> 図1　APIを使えば、細かい作業や無駄を省いてプログラムができる
>
> by [＠IT](http://www.atmarkit.co.jp/ait/articles/0703/13/news095.html)

[Canvas API](https://developer.mozilla.org/ja/docs/Web/API/Canvas_API)など、MDNを見ていると「〇〇な機能を提供するAPI」という記述を見かけることが多くありました。
その度に「APIって何なんだ・・・？」となっていたのですが、「複雑な処理を覆い隠して簡単に使えるようにしたもの」がAPIなんですね。
**機能を提供する側⇔機能を利用したい側**をつなぐインターフェースというわけでしょうか。

### **WebAPI**

HTTPプロトコルを使い外部のWebサービスからデータを取得したり、機能を利用したりすることができるもの。
Webアプリの文脈で「API」が出てきたらコレを指すことが多め。

- HTTPリクエストを使い、データ(JSON,XMLなどの形式、画像も扱う)のやり取りを行う。
- **「機能を公開しているソフトウェア」と「その機能を使いたいソフトウェア」**をつなげる窓口のようなもの。
- アプリケーション⇔他のアプリケーション間でデータをやり取りする方法。

![about-api](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/about-api.png?raw=true)

> 参考 : [APIとは？ - Qiita](https://qiita.com/jonathanh/items/6394ffb5b5ad86ae914f)

### **REST API (RESTful APIとも)**

Web APIのうち、

* Web上にリソースとして公開される
* URLによりリソースを識別
* HTTPメソッドにより操作する

などの特徴を持つ、RESTに従い設計されたAPI

***

ここからは教材の内容です。

## イントロ

このレッスンでは、あなた（私）はオンライン小売業者の開発者という設定。
その小売業者は自社のアプリケーション用にHTTP APIのセットを作成している。アプリケーションはNode.js上に構築されている。

あなた（私）の仕事は、販売する製品の一覧を取得するAPIを作成すること。

Node.jsにはWebアプリの構築を支援するHTTPと呼ばれるコアモジュールがあり、コンテンツを読み取り・書き込み・操作するための要求がサポートされている。

このモジュールでは、**Node.jsでHTTP要求を処理する方法**を学習する。
また、**WebサイトとHTTP APIの構築に役立つExpressフレームワーク**についても学習する。

### 学習の目的

- WebフレームワークExpressの主要な概念について理解する。
- 要求の処理方法を制御するためのミドルウェアを構成する。

## Expressを使用して新しいWebアプリを作成

多くの場合、企業はファイルシステムやDBに大量のデータを格納する。
ユーザがそのデータにアクセスするためには、Webアプリ・APIを利用する事が多い。

WebアプリとAPIを構築する時に考慮する必要がある概念を次に示す。

- **ルーティング** アプリケーションはURLアドレスに基づき、異なるセクションに分割される。
- **さまざまなデータ形式のサポート** 提供するデータは、プレーンテキスト/JSON/HTML/CSVなど様々なファイル形式に対応している必要がある
- **認証と認可** データの中には機密性の高いものもある。ユーザがデータにアクセスするために、サインインや特定のロール・アクセス許可レベルが必要になる場合がある。
- **データの読み書き** 通常、ユーザはシステムのデータ表示/データの追加を両方行う必要がある。データを追加するには、　フォームにデータを入力したり、ファイルをアップロードしたりする。
- **製品化までの時間** WebアプリとAPIを効率的に作成するには、適切なツール・ライブラリを選択する。

### Node.jsのHTTPモジュール

Node.jsには組み込みのHTTPモジュールがある。

> **http.Server**: HTTP サーバーのインスタンスを表します。 特定のポートとアドレスでさまざまなイベントをリッスンするよう、このオブジェクトに指示する必要があります。
> **http.IncomingMessage**: このオブジェクトは、**http.Server** または **http.ClientRequest** によって作成される読み取り可能なストリームです。 状態、ヘッダー、データにアクセスするために使用します。
> **http.ServerResponse**: このオブジェクトは、HTTP サーバーによって内部的に作成されるストリームです。 このクラスには、ヘッダーの種類や応答の内容など、どのような応答にする必要があるかが定義されています。

#### Webアプリの例

```js
const http = require('http');
const PORT = 3000;

const server = http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('hello world');
});

server.listen(PORT, () => {
  console.log(`listening on port ${PORT}`)
})
```

例では以下のことが示されている。

> **サーバーの作成**: **createServer()** を呼び出すと、**http.Server** のインスタンスが作成されます。
> **コールバックの実装**: **createServer()** メソッドには、関数を渡す必要があります。 この関数は、"*コールバック*" と呼ばれます。 それは、呼び出されるときに、**http.IncomingMessage** と **http.ServerResponse** のインスタンスを提供されます。 ここでは、それらは **req** および **res** という名前です。
> 1. **クライアント要求**: **req** インスタンスでは、クライアントの要求でどのヘッダーとデータが送信されたかが調査されます。
> 2. **サーバー応答**: サーバーにおいて、応答する必要があるデータと応答ヘッダーを **res** オブジェクトに渡すことにより、応答が作成されます。
> **要求のリッスンの開始**: ポートの指定時に **listen()** メソッドを呼び出します。 **listen()** を呼び出した後、作成したサーバーはクライアント要求を受け入れられる状態になります。

#### リッスン

> **[TCP/IP](https://e-words.jp/w/TCP-IP.html)**では、コンピュータ上で複数のプログラムが同時に異なる種類の通信ができるよう、**[ポート番号](https://e-words.jp/w/%E3%83%9D%E3%83%BC%E3%83%88%E7%95%AA%E5%8F%B7.html)**（port number）と呼ばれる識別番号が用意されている。外部からの接続を待ち受けて応答する**[サーバソフトウェア](https://e-words.jp/w/%E3%82%B5%E3%83%BC%E3%83%90%E3%82%BD%E3%83%95%E3%83%88%E3%82%A6%E3%82%A7%E3%82%A2.html)**は、自分が通信したいポート番号をオペレーティングシステム（OS）に登録し、そのポートに接続要求があると通知を受けて処理を行う。
> この動作のことを「ポートをリッスンする」のように表現し、そのようなプログラムのことを「**[リスナー](https://e-words.jp/w/%E3%83%AA%E3%82%B9%E3%83%8A%E3%83%BC.html)**」（listener：聞き手、聴取者）という。例えば、Webサーバは**[HTTP](https://e-words.jp/w/HTTP.html)**で通信を行うため、標準では**[TCP](https://e-words.jp/w/TCP.html)**の80番ポートをリッスンし、Webブラウザなどからアクセスされるのを待っている。
> [リッスン - IT用語辞典](https://e-words.jp/w/%E3%83%AA%E3%83%83%E3%82%B9%E3%83%B3.html#:~:text=%E5%A4%96%E9%83%A8%E3%81%8B%E3%82%89%E3%81%AE%E6%8E%A5%E7%B6%9A%E3%82%92,%E8%81%9E%E3%81%8D%E6%89%8B%E3%80%81%E8%81%B4%E5%8F%96%E8%80%85%EF%BC%89%E3%81%A8%E3%81%84%E3%81%86%E3%80%82)

#### 要するに

`createServer` で `http.Server` のインスタンス作成。その時コールバック関数を渡す。

ここで渡されるコールバック関数はそれぞれ、
`req` = **`http.IncomingMessage`** 、`res` = **`http.ServerResponse` 。**
`req` はリクエスト。クライアントの要求を指す。
`res` はレスポンス。サーバ側の動作として、応答の中身となるデータを `res` オブジェクトに渡すことでレスポンスを作成する。

`listen` を呼び出すと、指定したポートを利用してサーバが作成され、クライアントの要求を受けられる状態になる。

### ストリーム

> "*ストリーム*" は、Node.js の概念ではなく、オペレーティング システムの概念です。 ストリームでは、データをやり取りする方法が定義されています。 データは、チャンク単位で、クライアントからサーバーおよびサーバーからクライアントに送信されます。 ストリームにより、サーバーで多数の同時要求を処理できます。
> ストリームは Node.js の基本的なデータ構造であり、データの読み取りと書き込み、メッセージや "*イベント*" の送受信を実行できます。 HTTP モジュールでは、ストリームであるクラスを作成することによって、ストリーミングを実装します。
> この例の **req** パラメーターと **res** パラメーターはストリームです。 クライアント要求からの受信データをリッスンするには、次のように **on()** メソッドを使用します。

```js
req.on('data', (chunk) => {
  console.log('You received a chunk of data', chunk)
})
```

・・・？？？

* ストリームがデータ構造で、データの読み取り/書き込み/イベント送受信ができること。
* `req` `res` はストリームであること。
* `on` メソッドを使ってクライアントのリクエストをリッスンできること

はわかりました。

まず、用語を調べます。

**チャンク :** 大きなデータの塊を分割した断片

**ストリーム**

> プログラミングの分野では、データの入出力全般を扱う抽象的なオブジェクトやデータ型を意味する場合が多い。データが出入りする何らかの対象（メモリ領域やファイル、ネットワークなど）をプログラム中で扱えるように抽象化したもので、接続や切断、書き込みや読み込みなどを簡易な操作で行うことができる。
> 通信ネットワークの分野では、データを送受信する際にデータ全体の受信完了を待たずに受信したデータから順番に処理を行う送受信方式（**[ストリーミング](https://e-words.jp/w/%E3%82%B9%E3%83%88%E3%83%AA%E3%83%BC%E3%83%9F%E3%83%B3%E3%82%B0.html)**）や、そのように送受信される連続的なデータの流れをストリームという。
> [ストリーム - IT用語辞典](https://e-words.jp/w/%E3%82%B9%E3%83%88%E3%83%AA%E3%83%BC%E3%83%A0.html)

そのままですが、

**データが出入りする何か(メモリ領域、ファイル、ネットワーク等)を抽象化してプログラムで扱えるようにすることで、データの入出力操作を簡単にできるようにしたもの**

という理解で良さそうです。

何が利点なのか調べます。

**参考**

- [Node.js Stream を使いこなす](https://qiita.com/masakura/items/5683e8e3e655bfda6756)
- [Node.jsのstreamのしくみまとめ](https://zenn.dev/xxpiyomaruxx/articles/ab10b64fa3b17b)
- [Node.jsストリーム](https://tech-wiki.online/jp/nodejs-streams.html)

> ストリームは、Node.jsアプリケーションを強化する基本的な概念の1つです。
> これらは、ファイルの読み取り/書き込み、ネットワーク通信、またはあらゆる種類のエンドツーエンドの情報交換を効率的な方法で処理する方法です。
> ストリームはNode.jsに固有の概念ではありません。それらは数十年前にUnixオペレーティングシステムで導入され、プログラムはパイプ演算子を介してストリームを介して相互に対話できます（`|`）。

> たとえば、従来の方法では、プログラムにファイルを読み取るように指示すると、ファイルは最初から最後までメモリに読み込まれ、その後処理されます。
> ストリームを使用して、1つずつ読み取り、すべてをメモリに保持せずにコンテンツを処理します。

> ストリームは基本的に、他のデータ処理方法を使用して2つの大きな利点を提供します。
> **メモリ効率**：処理する前に、メモリに大量のデータをロードする必要はありません
> **時間効率**：データペイロード全体が開始できるようになるまで待つのではなく、データを取得したらすぐに処理を開始するのにかかる時間が大幅に短縮されます

- ファイルの読み取り・書き込み・情報交換を効率的に処理する手法。
- Microsoftの方でも書いてあったように、Node.js固有の概念ではない。
- ファイルを一定量だけ読み込んでイベントを発生させる、といったことが可能。
- 以下の4種類がある。
    - `[stream.Readable](https://nodejs.org/api/stream.html#stream_readable_streams)` - 読み取りだけができるストリーム
    - `[stream.Writable](https://nodejs.org/api/stream.html#stream_writable_streams)` - 書き込みだけができるストリーム
    - `[stream.Duplex](https://nodejs.org/api/stream.html#stream_class_stream_duplex)` - 読み取りも書き込みもできるストリーム
    - `[stream.Transform](https://nodejs.org/api/stream.html#stream_class_stream_transform)` - 読み取ったデータを変換して出力するストリーム

### Expressフレームワーク

アプリケーションの規模が大きくなってくると、フレームワークを採用する事が多い。

フレームワークの利用には以下のような利点がある。

- 開発速度の向上
- 複雑さの抽象化
- よく使われる機能（ルート管理、キャッシュ、認証と認可など）の実装を容易に
- 開発者コミュニティによるサポート

#### Expressでのルート管理

クライアントでWebアプリに対して要求を行う時は、特定のサーバーを指すアドレスであるURLを使用する。
URLは次のようになる。

    http://localhost:3000/products

このURLは、
`http://localhost:3000`(=自分自身のコンピュータを指す。なお、通常この位置はmicrosoft.comのようにドメイン名)と
`/products`(=ルート)から構成されている。

Expressではルート管理に**URL、ルート、HTTPメソッド**が使用される。
HTTPメソッドによりクライアントが行いたいことが記述され、ルートの登録・それらを適切なHTTPメソッドと組み合わせることでWebアプリを構成する。
ExpressにはさまざまなHTTPメソッドを処理するための専用メソッドがあり、ルートをコードに関連付けるためのシステムが用意されている。

次の例では`/product` が含まれるルートに対する`GET`要求を処理できる。

```js
app.get('/products', (req, res) => {
  // handle the request
})
```

#### 様々なデータ形式のサポート

Expressでは、呼び出し元のクライアントに返すことが出来る様々なコンテンツ形式がサポートされている。
`res` オブジェクトには、様々な種類のデータを返すためのヘルパー関数のセットが含まれている。

- プレーンテキストを返す

```js
res.send('plain text')
```

- JSONを返す

```js
res.json({ id: 1, name: "Catcher in the Rye" })
```

上のExpressのコードは次のHTTPモジュールのコードに相当する。

```js
res.writeHead(200, { 'Content-Type': 'application/json' });
res.end(JSON.stringify({ id: 1, name: "Catcher in the Rye" }))
```

`res.writeHead`

参考 : [第4回 ＣＤＮの仕組み HTTPヘッダとは | REDBOX Labo](https://blog.redbox.ne.jp/what-is-cdn4.html)

- ここでは、**ステータスコードとレスポンスのヘッダ**を書き込んでいる。
- `200`は成功を意味するステータスコード。
- `Content-type`は出力の[MIMEタイプ](https://developer.mozilla.org/ja/docs/Web/HTTP/Basics_of_HTTP/MIME_types)(後述)。

`res.end`

- HTTPレスポンスのプロセスを終了する関数。これがないと処理が正常に完了しない。
- `send`にはHTTPレスポンスプロセスの終了処理が含まれるため、`end`は不要らしい。

素のHTTPと比べてかなりスッキリ書ける事がわかりますね。

##### Content-Type・MIMEタイプについて

[MIMEタイプ](https://developer.mozilla.org/ja/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

**Multipurpose Internet Mail Extensions または MIME タイプ**。

ファイルの種類を表す概念として通常親しみがあるのは「拡張子」だと思います。
ですが、Webの世界には文書・ファイル・バイト列の性質や形式を表す標準として、「MIMEタイプ」という概念もあるそうです。

> MIME タイプはクライアントに対して、転送するドキュメントの種類を伝える機能です。ウェブにおいて、ファイル名の拡張子は意味を持ちません。従って、サーバーはそれぞれのドキュメントと共に正しい MIME タイプを転送するよう適切に設定することが重要です。ブラウザーはたいてい MIME タイプを、読み込んだリソースに対して行う既定のアクションを決めるために使用します。

**参考**

[Web開発者向けの重要なMIMEタイプ - MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/Basics_of_HTTP/MIME_types#important_mime_types_for_web_developers)
[MIMEタイプってなんだ？ - Qiita](https://qiita.com/NoxGit/items/6808bf539ce8fb713532)

## 実装 Expressを使用して基本的なWebアプリを作成

1. **app.js** ファイルを作成
2. ターミナルに移動し、「**npm init -y**」と入力。このコマンドを実行すると、Node.js プロジェクト用に既定の **package.json** ファイルが作成される。
    - プロジェクトを初期化している。具体的には、`package.json` というインストールしたパッケージ・依存関係等が記述されるファイルが作られる。
    - 確認に対して全てOKする前提なら `-y` オプションをつける。
3. ターミナルで「**npm install express**」と入力。 Express フレームワークがインストールされる。
4. **package.json** ファイルを開くと、 **dependencies** セクションに、**express** というエントリがある。 このエントリは、Express フレームワークがインストールされていることを意味する。
5. 次のコードを **app.js** に追加。

    ```js
    const express = require('express');
    const app = express();
    const port = 3000;

    app.get('/', (req, res) => res.send('Hello World!'));
    app.listen(port, () => console.log(`Example app listening on port ${port}!`));
    ```

    上のコードでは、**`express()`** を呼び出すことによってExpress アプリのインスタンスが作成されている。

    - ルートが `/` に設定されている。

    ```js
    app.get('/', (req, res) => res.send('Hello World!'));
    ```

    - **`listen()`** メソッドを呼び出して Web アプリケーションを開始。

    ```js
    app.listen(port, () => console.log(`Example app listening on port ${port}!`));
    ```

6. ターミナルで次のコマンドを実行して Web アプリケーションを開始する。

    ```bash
    node app.js
    ```
    
    次の出力が表示される。これは `listen` からの出力で、アプリが起動・実行され、要求を受信する準備ができていることを意味する。
    
    ```bash
    Example app listening on port 3000!
    ```
    
7. ブラウザーを開き、`http://localhost:3000` に移動。 ブラウザに**Hello World!** というテキストが表示されればOK。

![Screenshot 2022-02-12 13.15.59.png](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/hello-world.png?raw=true)

### 実装 JSONを返すWebアプリ

新しいルートを追加し、JSONを返す。

1. `app.js` に以下を追加。

    ```js
    app.get("/products", (req,res) => {
      const products = [
      {
        id: 1,
        name: "hammer",
      },
      {
        id: 2,
        name: "screwdriver",
      },
      ,
      {
        id: 3,
        name: "wrench",
      },
     ];
    
     res.json(products);
    });
    ```
    
2. コード全体は以下のようになる。
    
    ```js
    const express = require("express");
    const app = express();
    const port = 3000;
    
    app.get("/", (req, res) => res.send("Hello World!"));
    app.get("/products", (req,res) => {
       const products = [
         {
           id: 1,
           name: "hammer",
         },
         {
           id: 2,
           name: "screwdriver",
         },
         ,
         {
           id: 3,
           name: "wrench",
         },
       ];
    
      res.json(products);
    })
    app.listen(port, () => console.log(`Example app listening on port ${port}!`));
    ```
    

![response](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/json-response.png?raw=true)

OK。

## ミドルウェアを使用して要求ライフサイクルを管理する

**ライフサイクル :** 始まり〜終わりまで、誕生〜消滅までを指す。

場合によっては要求がWebアプリに到達した時、ユーザがログインしていること、または特定のリソースの表示を許可されていることを確認する必要がある。
その仕組みを**ミドルウェア**を用いて実装していく。

### 要求の手順

要求を一連の手順として処理することを考えてみる。

リソース処理のためにユーザがログインする必要がある場合、手順は次のようになる。

1. **要求前** ユーザが要求ヘッダーを使用して適切な資格情報を送信したか調べる。資格情報が検証された場合は次のステップに要求を送信。
2. **応答を作成** DBやエンドポイントなど、何らかの種類のデータソースと通信する。リクエストでリソースが適切に要求されていれば、このステップでリソースが返される。
3. **要求後** 省略可能。ログ記録など。

Expressにはこの方法で要求を処理出来るメソッドが組み込まれている。

要求前後の処理は**ミドルウェア**と呼ばれ、次のようになる。

```js
app.use((req, res, next) => {})
```

Expressのインスタンス化されたオブジェクトで`use`メソッドを実装する。
引数の意味は以下。

> - **req**: このパラメーターは、受信した要求です。 これには、要求ヘッダーと呼び出し元の URL が含まれます。 また、要求でクライアントからデータが送信された場合は、データの本体が含まれることがあります。
> - **res**: このパラメーターは応答ストリームです。 このストリームを使用して、呼び出し元のクライアントに送信するヘッダーやデータなどの情報を書き込みます。
> - **next**: このパラメーターでは、要求に問題がないこと、およびそれを処理する準備ができていることが通知されます。 **next()** が呼び出されない場合、要求の処理は停止します。 また、要求が処理されない理由をクライアントに通知することをお勧めします。たとえば、**res.send('')** を呼び出します。

### ミドルウェアとは結局何か

よくわかっていないので追加で調査します。

**参考**
[Express ミドルウェアの使用](https://expressjs.com/ja/guide/using-middleware.html)
[Express 4.x - API リファレンス](https://expressjs.com/ja/4x/api.html)

この記事、面白いしわかりやすいです。
[expressは一体何をしとるんじゃ・・・ - Qiita](https://qiita.com/ganyariya/items/85e51e718e56e7d128b8)

#### ミドルウェアとは

ミドルウェアは、`req`と`res`を受け取り、任意の処理を行う関数のことです。
`next`にはミドルウェア関数の次に実行したいコールバックを登録します。

「Expressは一連のミドルウェア関数の呼び出し」と言われるように、
次のミドルウェアへの処理を継続するリクエスト/レスポンスサイクルをそこで終了させる
のいずれかを行います。

> (req, res, next ) => {行いたい処理}
>　･･･これがよく、app.getやapp.postなどに記述されるミドルウェア関数なのじゃあ！

> ```js
> app.get('/', (req, res, next) => {
>    res.render('home.hbs',{
>        pageTitle:'Welcome to My ホームページ',
>        titleName:'タイトルなんやで'
>    })
> })
> ```
>
>　上記のような感じで、出て来るはずなのじゃあ･･･
>　reqは「request」の略で、クライアントからのHTTPリクエストに関する情報が格納されているのじゃあ･･･
>　resは「response」の略で、クライアントに送り返すHTTPの情報が格納されているのじゃあ･･･
>　nextは、このミドルウェア関数の次に実行したいコールバック関数が入っているのじゃあ！これはapp.useで設定した関数が格納されているらしいのじゃ･･･
>　　注意点としては、app.useで設定したミドルウェア関数をどんどん連続で実行させたいときは、そのミドルウェア関数の中で必ずnext();と、next関数を実行しないといけないのじゃ！
>　この記述がないとコールバックが実行されないので、途中で処理が止まってしまうらしいのじゃ･･･

`next`は、リクエスト/レスポンスサイクルを継続。
先程ちらっと出てきた`end`や`send`は、リクエスト/レスポンスサイクルをそこで終了させていたんですね。

#### `app = express()`

読み込んだExpressモジュールをインスタンス化しています。
慣習的に`app`という名前にするそうです。
#### `app.use`

構文は`app.use([path,] callback [, callback...])`。

**指定されたミドルウェア関数を指定されたパスで使用できるようにする**メソッドです。
[path]のデフォルトは`/`。
そのため、pathを指定せずに実装したミドルウェアは、アプリへのリクエストごとに実行されます。

[path]に`/user`と記述すると、`/user`リクエストがあった際に実行されるミドルウェア関数を設定できます。

`app.use`で設定した順でミドルウェア関数が実行されるので注意。

#### `app.METHOD`

`app.get`など、GET, PUT, POSTなどのリクエストのHTTPメソッドを小文字で表します。
`app.get`の場合、特定のルートに対してGET要求があった時に実行する処理を定義出来ます。

#### 例

後々でてくるコードですが、何がしたいのかがわかりやすいです。

`app.get`(要求処理)は`isAuthorized`(要求前の処理)を第2引数として受け取り、
パスワードが正しければ`next`により次の処理に進みます。
パスワードが間違っていれば`res`のステータスコードをエラーに設定、メッセージを送ってレスポンスサイクルを終了させます。

```js
function isAuthorized(req,res, next) {
  const auth = req.headers.authorization;
  if (auth === 'secretpassword') {
    next();
  } else {
    res.status(401);
    res.send('Not permitted');
  }
}

app.get('/users', isAuthorized, (req,res) => {
  res.json([{
    id: 1,
    name: 'User Userson'
  }])
  })
```

なんとなく理解出来たので、次に進みます。

## 実装 要求のライフサイクルを管理する

### 基本的な承認を追加する

ほとんどのアプリは誰でもアクセス出来る部分と保護されている部分が存在する。アプリを保護するには様々な方法があるが、この演習ではExpressを使って簡単な保護システムを実装する。

1. まず、次のコマンドを実行して[https://github.com/MicrosoftDocs/node-essentials](https://github.com/MicrosoftDocs/node-essentials)のリポジトリをクローン。
    
    ```bash
    git clone https://github.com/MicrosoftDocs/node-essentials
    ```
    
2. クローンしたリポジトリに移動して、npmパッケージをインストール。
    
    ```bash
    npm install
    ```
    
3. `app.js` `client.js` を調べる。
    
    ```js
    const express = require('express')
    const app = express()
    const port = 3000
    
    app.get('/', (req, res) => res.send('Hello World!'))
    
    app.get('/users', (req,res) => {
      res.json([{
        id: 1,
        name: 'User Userson'
      }])
    })
    
    app.get('/products', (req, res) => {
      res.json([{
        id: 1,
        name: 'The Bluest Eye'
      }])
    })
    
    app.listen(port, () => console.log(`Example app listening on port ${port}!`))
    ```

    ルート `/`、`/users`、`/products`に対する処理が記述されている。

    ```js
    const http = require('http');

    http.get({
      port: 3000,
      hostname: 'localhost',
      path: '/users',
      headers: {}
    }, (res) => {
      console.log("connected");
      res.on("data", (chunk) => {
        console.log("chunk", "" + chunk);
      });
      res.on("end", () => {
        console.log("No more data");
      });
      res.on("close", () => {
        console.log("Closing connection");
      });
    });
    ```

    `http://localhost:3000/users`に接続した後、**chunk**、**end**、**close**などのイベントをリッスンして処理を行う。


4. `node app.js` を実行し、サーバーアプリケーションを実行。
5. `node client.js` を実行し、クライアントを実行。
    
    以下のような出力が得られる。
    
    ```bash
    connected
    chunk [{"id":1,"name":"User Userson"}]
    No more data
    Closing connection
    ```
    
6. `app.js` に次のコードを追加。
    
    ```js
    function isAuthorized(req,res, next) {
      const auth = req.headers.authorization;
      if (auth === 'secretpassword') {
        next();
      } else {
        res.status(401);
        res.send('Not permitted');
      }
    }
    ```
    
7. `app.js` の `get` 部分を置き換え
    
    `isAuthorized` を2番目の引数として渡す。
    
    ```js
    app.get('/users', isAuthorized, (req,res) => {
      res.json([{
        id: 1,
        name: 'User Userson'
      }])
     })
    ```
    
8. `node client.js` 再び
    
    ```bash
    connected
    chunk Not permitted
    No more data
    Closing connection
    ```
    
    `isAuthorized()` が呼び出されたため応答されなかった。
    
    `const auth = req.headers.authorization;` とあるように、ヘッダーに  `authorization` が含まれる、かつ正しいパスワードである必要がある。
    
9. `client.js` に修正を加える。
    
    ```bash
    headers: {
      authorization: 'secretpassword'
    }
    ```
    
10. `node client.js` 再び
    
    ```bash
    connected
    chunk [{"id":1,"name":"User Userson"}]
    No more data
    Closing connection
    ```

    実際には、この例より更に堅牢にする必要がある。

    ハッシュ化(一方向関数により暗号化)したパスワードをDBに保存し、
    DBのハッシュ化されたダイジェスト⇔ユーザの入力したパスワードをハッシュ化して等しければOK、など。

### httpモジュール

唐突すぎる`require('http')`・・・
調べます。

**参考**
[HTTP | Node.js v17.5.0 Documentation](https://nodejs.org/api/http.html)

[公式](https://nodejs.org/api/http.html#httprequestoptions-callback)によると、以下の書き方はどうやら`http.request(options[, callback])`という構文のようです。
今回使用しているoptionsは以下です。

> * `headers` `<Object>` An object containing request headers.
> * `hostname` `<string>` Alias for host. To support url.parse(), hostname will be used if both host and hostname are specified.
> * `method` `<string>` A string specifying the HTTP request method. Default: 'GET'.
> * `path` `<string>` Request path. Should include query string if any. E.G. '/index.html?page=12'. An exception is thrown when the request path contains illegal characters. Currently, only spaces are rejected but that may change in the future. Default: '/'.
> * `port` `<number>` Port of remote server. Default: defaultPort if set, else 80.

```js
http.get({
  port: 3000,
  hostname: 'localhost',
  path: '/users',
  headers: {}
}
```

レスポンスのデータは、`res.on` + イベント名の指定により受け取ります。

イベントについては[http.ClientRequest](https://nodejs.org/api/http.html#class-httpclientrequest)に詳細が記載されています。

また、[http.ClientRequest](https://nodejs.org/api/http.html#httprequestoptions-callback)が、[http.request](https://nodejs.org/api/http.html#httprequestoptions-callback)から返されるオブジェクトであり、

> The only difference between this method and http.request() is that it sets the method to GET and calls req.end() automatically.
> http.request()との唯一の違いは、メソッドをGETに設定し、req.end()を自動的に呼び出す点です。

↑の記述から、[http.get](https://nodejs.org/api/http.html#httpgetoptions-callback)も`http.ClientRequest`を返す事がわかります。（おそらく）

`http.ClientRequest`からレスポンスを取得するには、requestオブジェクトに`response`リスナーを追加します。`response`イベントでは、レスポンスオブジェクトにリスナーを追加することが出来ます。

レスポンスオブジェクトのデータは、`data`ハンドラ呼び出し、`resume`メソッド呼び出しなどにより消費する必要があります。
データを消費しないと`end`イベントが発生しません。
また、データが読み込まれるまではメモリを消費するので、最終的には'process out of memory' エラーになる可能性があります。

コードを再掲します。
`options`で色々と指定、`data`、`end`などのイベント発生時に処理を行っていることがわかります。

```js
const http = require('http');

http.get({
  port: 3000,
  hostname: 'localhost',
  path: '/users',
  headers: {}
}, (res) => {
  console.log("connected");
  res.on("data", (chunk) => {
    console.log("chunk", "" + chunk);
  });
  res.on("end", () => {
    console.log("No more data");
  });
  res.on("close", () => {
    console.log("Closing connection");
  });
});
```

### まとめ

- WebAPIとは外部のWebサービスが提供している機能(関数みたいなもの)をHTTP通信経由で利用する事ができるもの。
- APIに対してはブラウザ/コード/cRULなどのクライアントを利用して要求を送信出来る。
- APIを叩くとレスポンスが返ってくる。JSONであることが多い。
- Node.jsのHTTPコアモジュールを使って要求を処理する方法を学んだ。
- ExpressなどのWebフレームワークを利用する利点を学んだ。
- Expressでは、ルート管理、ファイルのアップロード/ダウンロードの処理、異なる種類の応答の作成、などの処理を実装出来る。
- ミドルウェアにより要求前後の処理を登録、認証情報のログ記録・操作などのタスクを実行する事で、要求のライフサイクルを管理できる。
- HTTPモジュール、Express等のドキュメントをそこそこ読んだ。少しだけ読み方がわかった気がする。