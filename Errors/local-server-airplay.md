<!--
title:   【MacOS Monterey12】ポート5000を利用しようとすると「Address already in use」が発生する
tags:    Mac,エラー,ローカルサーバー,初心者
id:      085bed62158aa987a64c
private: false
-->


# 最初に結論

MacOS Monterey 12以降 、ポート5000を利用しようとすると`Address already in user` が発生することがある。(2022/2 現在)

この現象は、「AirPlayサーバー」がポート5000を利用していることにより発生する。
プロセスを終了しても勝手に再起動されてしまうため、設定 > Airplayから「AirPlayレシーバー」のチェックを外すことで対処できる。

![airplay](./address-already-in-use-solved.png)

## 筆者環境

* MacOS Monterey 12.2.1
* MacBook Air

## 発生した問題

MicrosoftのWeb開発教材に取り組んでいる時、(詳細は[こちらの記事](./../Microsoft-web-dev-for-beginners/6_space_game.md))
`npm start`コマンドを使ってローカルサーバを起動しようとしました。

すると、以下のようなエラーが発生しました。

```js
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! solution@1.0.0 start: `npx http-server -c-1 -p 5000`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the solution@1.0.0 start script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
npm WARN Local package.json exists, but node_modules missing, did you mean to install?

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/westen/.npm/_logs/2022-02-01T13_05_57_743Z-debug.log
```

### エラーの要因を探す

* `npm -v` `node -v` ともに問題なし。

* 以下の記述からエラーログがあることがわかるので見に行ってみる。

```shell
npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/westen/.npm/_logs/2022-02-01T13_05_57_743Z-debug.log
```

* エラーの内容が書いてあったのは↓くらい。

```js
23 error This is probably not a problem with npm. There is likely additional logging output above.
```

* `npm` `node`の問題では無さそうなことだけわかった。


* `npm start` は `npx http-server -c-1 -p 5000`。
  * `npx` は `npm` に内包されているらしい。念の為確認する。
  * `npx -v` → 問題なし。

* `npx http-server -c-1 -p 5000` をそのまま実行してみる。

```bash
$ npx http-server -c-1 -p 5000

events.js:377
        throw er; // Unhandled 'error' event
        ^

Error: listen EADDRINUSE: address already in use 0.0.0.0:5000
    at Server.setupListenHandle [as _listen2] (net.js:1320:16)
    at listenInCluster (net.js:1368:12)
    at doListen (net.js:1505:7)
    at processTicksAndRejections (internal/process/task_queues.js:83:21)
Emitted 'error' event on Server instance at:
    at emitErrorNT (net.js:1347:8)
    at processTicksAndRejections (internal/process/task_queues.js:82:21) {
    code: 'EADDRINUSE',
    errno: -48,
    syscall: 'listen',
    address: '0.0.0.0',
    port: 5000
}
```

- `Error: listen EADDRINUSE: address already in use 0.0.0.0:5000`

それっぽいのが有りました。既にそのアドレスが使われているのが問題っぽい。

### プロセスの確認・終了

以下の記事を参考に、 `lsof -i:ポートNo` で確認してみます。

[ビルド失敗：Error: listen EADDRINUSE: address already in use :::4000](https://ja.stackoverflow.com/questions/52577/%e3%83%93%e3%83%ab%e3%83%89%e5%a4%b1%e6%95%97-error-listen-eaddrinuse-address-already-in-use-4000)
[Address already in use の対処法](https://qiita.com/arashida/items/8b8d9d2f1f040b2aecf1)

```bash
$ lsof -i :5000
COMMAND   PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ControlCe 412 westen   19u  IPv4 0x38c9f786f173e0ff      0t0  TCP *:commplex-main (LISTEN)
ControlCe 412 westen   20u  IPv6 0x38c9f786f18431e7      0t0  TCP *:commplex-main (LISTEN)
```

なんかいますね・・・

- `kill -9 [PID]` を実行してみる
  - `-9`は強制終了のオプション

```bash
$ kill -9 412
$ lsof -i :5000
COMMAND     PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ControlCe 49790 westen   19u  IPv4 0x38c9f786f172f63f      0t0  TCP *:commplex-main (LISTEN)
ControlCe 49790 westen   20u  IPv6 0x38c9f786f182afc7      0t0  TCP *:commplex-main (LISTEN)
```

あれ？

- `-9` を付けずに実行

```bash
$ kill 49838
$ lsof -i :5000
COMMAND     PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ControlCe 49934 westen   19u  IPv4 0x38c9f786f171ab9f      0t0  TCP *:commplex-main (LISTEN)
ControlCe 49934 westen   20u  IPv6 0x38c9f786f1842b07      0t0  TCP *:commplex-main (LISTEN
```

変わらず。

そもそも`lsof`は何を見ているんだ？を調べてみる。

[lsofコマンド入門 - Qiita](https://qiita.com/hypermkt/items/905139168b0bc5c28ef2)
[【ps・kill】実行中のプロセス表示と強制終了](https://qiita.com/shuntaro_tamura/items/4016868bda604baeac3c)
[lsofを使ってプロセスが利用しているポートを確認する。 - Qiita](https://qiita.com/kooohei/items/9e3859e3d1d854c3d163)

* `lsof`はプロセスが開いているファイルを表示するコマンド。
* `-i`オブションをつけることで現在利用されているポートを表示。
  * PIDはプロセスのID。
  * COMMANDは実行コマンド名。
* パイプ`|`、`grep`を利用することで条件を絞って検索できる

再び出力を確認。

```bash
$ lsof -i :5000
COMMAND     PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ControlCe 49934 westen   19u  IPv4 0x38c9f786f171ab9f      0t0  TCP *:commplex-main (LISTEN)
ControlCe 49934 westen   20u  IPv6 0x38c9f786f1842b07      0t0  TCP *:commplex-main (LISTEN
```

コマンド名がControlCe・・・ControlCenter?
「Mac ControlCenter port5000」でググる。

[Port 5000 already in use — MacOS Monterey issue](https://anandtripathi5.medium.com/port-5000-already-in-use-macos-monterey-issue-d86b02edd36c)

それっぽい記事！

要約すると、以下のような事が書かれています。

MacOS Monterey 12 にアップデート後、この現象が起きるようになった。
`kill` コマンドを実行しても再起動されてしまう。
**AirPlay server**によってこのプロセスが実行されているので、それを非アクティブにすればいい。

### 解決策

設定 > Airplayから「AirPlayレシーバー」のチェックを外す。

![airplay](./address-already-in-use-solved.png)

再び実行してみる。

```bash
$ npm start

> solution@1.0.0 start /Users/westen/dev/MS-Web-Dev/6-space-game/3-moving-elements-around/your-work
> npx http-server -c-1 -p 5000

npx: 39個のパッケージを5.534秒でインストールしました。
Starting up http-server, serving ./

http-server version: 14.1.0

http-server settings: 
CORS: disabled
Cache: -1 seconds
Connection Timeout: 120 seconds
Directory Listings: visible
AutoIndex: visible
Serve GZIP Files: false
Serve Brotli Files: false
Default File Extension: none

Available on:
  http://127.0.0.1:5000
  http://192.168.0.5:5000
Hit CTRL-C to stop the server
```

OK!

### 反省点

`Address already in use`の対処のためには`lsof`や`kill`を使えば良さそう。
というところまでは良かった。

その後、`lsof`が何を見ているのか、`kill`は何を終了しているのかを調べてから使うべきだった。
プロセスの確認・終了をするためのコマンドだということがわかっていればもう少し早くコマンド名の違和感にも気づけたはず。