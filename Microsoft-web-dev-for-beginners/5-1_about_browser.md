<!--
title:   MicrosoftのWeb開発教材を使ってみた ⑤-1ブラウザ拡張機能 【ブラウザの仕組み/拡張機能作成の導入】
tags:    Web,ブラウザ,初心者,拡張機能
id:      d0189565d039c2c11383
private: false
-->
# はじめに

**「Web Development For Beginners」**というMicrosoftがGithubに公開している教材についての記事です。

<details><summary> 教材の紹介・選んだ理由など </summary><div>

### この教材を選んだ理由

https://github.com/microsoft/Web-Dev-For-Beginners

- HTML/CSS/JavaScriptを触れるいい感じの教材が欲しかった
    - そこそこのボリュームがあり、作りながら学べるタイプの教材
    - 基礎的なトピックが一通り網羅されている
- 質が高そう
    - なにせあのMicrosoftなので、きっと良いものでしょう。
- 題材が**面白そう**
    - 軽く調べた感じだとチュートリアルでよくある題材として「TODOアプリ」「クイズアプリ」などがあるみたいですが、どれもどう実装するのか想像がついてしまって、余り興味がわきませんでした。
    - しかしこの教材は「テラリウム」「タイピングゲーム」「ブラウザ拡張機能」「スペースゲーム」「銀行プロジェクト」と、面白そうなトピックが並んでいます。

#### +α 実際に取り組んで感じたこと

- 提供されるリファレンス・参考サイトの質が高い
    - 一例は**Flexbox Froggy**。🐸 を並べながら `flexbox` の扱いについて学べるサイトです。超わかりやすいです。

https://flexboxfroggy.com/#ja

- 「アクセシビリティ」「ブラウザがどう動くのか」といった知識も学べる
    - 絶対やるべきだけど後回しにしがちなトピックも結構ガッツリ触れます。
    - かゆいところに手が届く感じ。
- 多分、英語全くわからなくてもなんとかなる
    - ほとんどのレッスンは `translations`というフォルダに日本語訳があります。
    - 最悪全部Deeplに突っ込めばなんとかなります。
- Edge推しがすごい
    - Microsoftの教材なので当然ですが、デモでは基本Edgeが使われます。
- スケッチノートがわかりやすい
    - 一部レッスンは最初にスケッチノートというイラストがあるのですが、それがすごくわかりやすいです。それに可愛い。
    - 扱うトピックについてイラストで視覚的に示してくれるので、どんな内容をやるのかざっくり把握してからレッスンに入ることが出来ます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/52789223-13b3-1043-edb6-e26d5828bf35.png)
 > [microsoft/Web-Dev-For-Beginners/tree/main/1-getting-started-lessons/3-accessibility より](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/sketchnotes/webdev101-a11y.png)


### 教材の概要

各レッスンに以下の要素が含まれます。

- スケッチノート(オプション)
    - レッスンの概要がわかりやすくまとまったイラスト
- 補足のビデオ(オプション)
- レッスン前の小テスト
    - 簡単なテスト
- ステップバイステップなレッスン
- 知識のチェック
- レッスン後の小テスト
    - 簡単なテスト
- チャレンジ
- 副読本(サイト)
- 復習と自己学習
- 課題

チャレンジ〜は調べ物や課題をこなします。
課題については必要だと思ったものだけやりました。

#### 教材の構成

1. **getting-started-lessons(はじめに)**
    1. プログラミング言語と開発ツール
    1. アクセシビリティ
    1. Githubの基礎
2. **js-basics(JavaScript基礎)**
    2. データ型
    2. 関数とメソッド
    2. 分岐処理
    2. ループ
3. **terrarium（テラリウム構築）**
    3. HTMLイントロ
    3. CSSイントロ
    3. DOM操作とクロージャ
4. **typing-game（タイピングゲーム）**
    4. タイピングゲームを作る(イベント管理)
5. **browser-extension（ブラウザ拡張機能）**
    5. ブラウザについて
    5. API呼び出し、ローカルストレージの利用
    5. バックグラウンドタスクとパフォーマンス
6. **space-game（スペースシューティングゲーム）**
    6. イントロ(Pub-Subパターン)
    6. キャンバス
    6. モーションの追加
    6. レーザー追加、衝突検出
    6. スコアの保存
    6. 終了と再起動
7. **bank-project（架空の銀行プロジェクト）**
    7. WebアプリのHTMLテンプレートとルート
    7. ログインと登録フォームの構築
    7. データの取得と利用方法
    7. 状態管理の概念

### 取り組む際に気をつけたこと

* コピペ/写経にならないようにする
    * サンプルコードと実装の解説が一緒になっているので、理解したつもりになってコピペしがちです。
    * まず一通り目を通してから、なるべく自分の頭で考えて実装するようにしました。
* 全部完璧にやろうとしない
    * 「12週間、24レッスンのカリキュラム」と銘打たれているように、出される課題や副教材を全てこなそうと思うとかなりボリュームがあります。
        * そのため、現時点で必要だと思うカリキュラムにのみ取り組みました。
</div></details>

***
[〜②JavaScript基礎まで【導入/アクセシビリティ/JavaScript の基礎】](2022-02-08_JavaScript_Microsoft_d78514969191491a4bcd.md)
[③テラリウム構築 【HTML・CSS基礎/DOM操作/クロージャ】](2022-02-09_CSS_HTML_JavaScript_59b8e43d8d6fb609c7d5.md)
[④タイピングゲーム 【JavaScriptのイベント処理】](2022-02-09_JavaScript_340f391ee9f167bf4333.md)
**⑤-1ブラウザ拡張機能 【ブラウザの仕組み/拡張機能作成の導入】　本記事**
⑤-2ブラウザ拡張機能 【API/LocalStorage/BackGround/Performance】
⑥スペースシューティングゲーム【JavaScriptによるゲーム開発の基礎】
⑦架空銀行プロジェクト【ログイン/データ管理/状態管理】
***

### 記事の目的

- 学習のアウトプット
- 教材を使ってみたところかなり良かったので、その紹介

### 注意点

自身の学習のアウトプットがメインなので、理解できているところ(他言語と共通の箇所など)は省いています。
また、課題やtipsについても結構省きます。
この教材に興味を持った方はぜひご自分で取り組んでみてください。

# 5-Browser-extension

https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/5-browser-extension

指定された地域の[カーボンフットプリント](https://ja.wikipedia.org/wiki/%E3%82%AB%E3%83%BC%E3%83%9C%E3%83%B3%E3%83%95%E3%83%83%E3%83%88%E3%83%97%E3%83%AA%E3%83%B3%E3%83%88)を表示するブラウザ拡張機能を作っていきます。
その過程でブラウザの仕組みやフォームの構築方法、APIの呼び出し、ローカルストレージの使用方法などについて学びます。

![browser-extension-demo](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/5-browser-extension/extension-screenshot.png)
> https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/5-browser-extension より

### 学習の目的

* ブラウザの仕組み、歴史、ブラウザ拡張機能の最初の要素の足場の作り方を学ぶ
* ローカルストレージに格納された変数を使用してAPIを呼び出すためのブラウザ拡張機能のJavaScript 要素を構築する
* ブラウザのバックグラウンドプロセスを使用して拡張機能のアイコンを管理する
* Webのパフォーマンスと最適化について学ぶ

## ブラウザの全て

ブラウザ拡張機能を作って見る前に、ブラウザがどのように動くのか学んでみましょう！という感じのノリです。

このレッスンをやる前の知識としては↓が何となく分かるくらいです。

- クライアント/サーバ
- IPアドレス/MACアドレスとか、名前解決でやっていることの概要
- RESTの概要
- Cookie/ローカルストレージ/Session
- APIの概要
- HTTPS、SSL/TLSの概要

### ブラウザについて

![all-about-browser](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/sketchnotes/browser.jpg)
> https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/5-browser-extension/1-about-browsers より

このイラストがすごくわかりやすかったので内容について説明があるのかとワクワクしていたのですが、特に説明はなかったです・・・

なので、構成要素について自分で調べました。

#### ざっくりとした処理の流れ

上のイラストにおいて、ユーザがURLを入力してからWebページが表示されるまでの流れはざっくりと以下のようになります。

1. ユーザ(クライアント)がURLを入力して何かを検索
2. DNSを利用して名前解決を行い、IPアドレスを得る
3. TCPによるコネクションの確立
4. HTTP>GETリクエストを発行
5. サーバからレスポンスとしてステータスコード/ファイルなどを受け取る
6. ブラウザが受け取ったファイル(HTML/CSS/JS)を解釈し、表示する

#### 各要素を見ていく

<details><summary> DNS </summary><div>

![DNS](https://manual.iij.jp/dns/help/images/1480649_1803541.png)
> https://manual.iij.jp/dns/help/1480649.html より

* **Domain Name System**のこと。
* ドメイン名、及びそれに関する情報をもつ分散DB。
* ドメイン名を「.」で区切った階層構造で管理している。
    
**ドメイン名からIPアドレスを調べる際の流れ**
ルートサーバに対して、検索したいドメインのトップレベルドメイン(TLD)を管理するDNSサーバの場所を問い合わせる
→次にTLDサーバにセカンドレベルドメイン（SLD）を管理するDNSサーバの場所を問い合わせる・・・
という手順を繰り返す。
    
**ネームサーバ**
権威DNSサーバ/コンテンツDNSサーバとも呼ばれる。
ドメインとIPアドレスを紐付ける台帳を持ったサーバ。
主な役割は、名前解決要求に対して自身が持つ情報を基に名前解決結果を返すこと。

- 内部に**IPアドレスとサーバ名などを対応させるレコード**を持つ
- キャッシュDNSサーバから来る名前解決要求に対して返答を返す
- 自身の保持する台帳にその情報が記載されていない場合、次にどこに情報を聞きに行けばよいか教えてくれる
    
**キャッシュDNSサーバ**
フルリゾルバとも呼ばれる。
PCからの名前解決要求（このドメインのIPアドレスは何？）をとりまとめる。
    
- 各ネームサーバに名前解決要求を出し、返答を得られるまで探す
- 一度確認したIPとドメインの対応を一定期間自身の中に**キャッシュする**ことにより、同じドメインに対して再度ネームサーバに確認しにいくという手順を省いている
</div></details>

<details><summary> ISP </summary><div>
**Internet Service Provider** のこと。
インターネット接続サービスを提供する事業者。
</div></details>

<details><summary> Router </summary><div>
データを2つ以上の異なるネットワーク間に中継する通信機器。

IPアドレス情報を確認して、データをどのルートを通して転送すべきかを判断するルート選択機能を持つ。
</div></details>

<details><summary> ３−way Hanshake </summary><div>

TCPにおいて、通信の信頼性を確認するために実施される手法。
SYN = synchronize
ACK = acknowledge

1．送信元が通信路を確保するため、相手にデータ転送の許可要求を出す。（SYN）
2．宛先側が許可を送信元に知らせると同時に受信側も許可要求を出す。（ACK + SYN）
3.最初にSYNを送った送信元も宛先側に許可を出す。（ACK）

参考 [【TCP】コネクションの確立までの道のり](https://qiita.com/tatsuya4150/items/ae4d5e95e43ce0670bc0)
</div></details>


<details><summary> HTTPリクエスト/レスポンス </summary><div>

**HTTP**

- Webの基盤となる通信プロトコル
- RESTの特徴である統一インターフェース・ステートレスサーバ・キャッシュなどを実現している
- クライアントが出したリクエストをサーバで処理してレスポンスを返す
- 名前はハイパーテキストとなっているが、静止画・動画・JS・pdfなどデータであれば何でも転送できる

**HTTPリクエストメソッド**
リソースに対して実行するアクション。
[MDN - HTTPリクエストメソッド](https://developer.mozilla.org/ja/docs/Web/HTTP/Methods)

- GET リソースの取得
- POST リソースの送信
- DELETE リソースの削除

など。

**HTTPレスポンス**
特定のHTTPリクエストが正常に終了したか示す。

[MDN-HTTPレスポンスステータスコード](https://developer.mozilla.org/ja/docs/Web/HTTP/Status)
</div></details>

<details><summary> Parse </summary><div>
**Parse : 解析**

> ドキュメントの解析とは、ドキュメントを意味のある構造（コード内で解釈し、使用できる形式）に変換することです。解析結果は通常、ドキュメントの構造を表すノードのツリーになります。これを「解析ツリー」または「構文ツリー」といいます。

> [ブラウザの仕組み 解析-概要](https://www.html5rocks.com/ja/tutorials/internals/howbrowserswork/#:~:text=%E8%AA%AC%E6%98%8E%E3%81%97%E3%81%BE%E3%81%97%E3%82%87%E3%81%86%E3%80%82-,%E8%A7%A3%E6%9E%90%20%2D%20%E6%A6%82%E8%A6%81,-%E8%A7%A3%E6%9E%90%E3%81%AF%E3%83%AC%E3%83%B3%E3%83%80%E3%83%AA%E3%83%B3%E3%82%B0)
</div></details>

<details><summary> ブラウザの主な構造 </summary><div>

![browser-structures](https://www.html5rocks.com/ja/tutorials/internals/howbrowserswork/layers.png)
> [ブラウザの仕組み : 最新ウェブブラウザの内部構造](https://www.html5rocks.com/ja/tutorials/internals/howbrowserswork/#:~:text=%E3%82%82%E3%81%A1%E3%82%8D%E3%82%93%E3%81%82%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82-,%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%81%AE%E4%B8%8A%E4%BD%8D%E6%A7%8B%E9%80%A0,-%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%81%AE%E4%B8%BB) より

- User Interface
    - ユーザーからの操作を受け付ける
    - アドレスバー、戻る/進むボタンなど
- Rendering Engine
    - コンテンツの表示を担当
- Networking
    - HTTPリクエストなどの呼び出しに使用
    - プラットフォームに依存しないインターフェースとプラットフォームごとの実装を持つ
- Browser Engine
    - UI⇔レンダリングエンジンをつなぐ
- Data Storage
    - データを保存する領域
- UI Backend
    - コンボボックスやウィンドウなどの基本的なウィジェットの描画に使用
- JavaScript Engine
    - JavaScriptが実行される環境

</div></details>

#### HTML/CSSの解析〜表示について

##### 参考

- [Parse - MDN](https://developer.mozilla.org/ja/docs/Glossary/Parse)
- [ブラウザの仕組み : 最新ウェブブラウザの内部構造](https://www.html5rocks.com/ja/tutorials/internals/howbrowserswork/#The_rendering_engine)

↑のサイトは少し古めですが、かなり詳しく解説されているのでおすすめです。

- [ちいさなWebブラウザをつくろう](https://browserbook.shift-js.info/)
- [Let's build a browser engine! Part 1: Getting started](https://limpet.net/mbrubeck/2014/08/08/toy-layout-engine-1.html)

ブラウザを作ってみるような記事もいくつか有りました。いずれやりたい。

##### HTMLの解析

1. トークナイザー(またはレキサー)によりトークン(開始タグ、終了タグ、属性名、属性値など)に分割する
2. 言語の構文ルールに従ってドキュメントの構造を分析し、解析ツリーを構築する

トークンとは、ここでは**最小の構成単位**のことを指すのだと思います。

>**トークン**とは、証拠、記念品、代用貨幣、引換券、商品券などの意味を持つ英単語。ITの分野では、**長いデータを最小の構成単位に分解したもの**や、何かの証や印になるようなデータや装置、器具などのことをトークンということが多い。
[トークン - IT用語辞典](https://e-words.jp/w/%E3%83%88%E3%83%BC%E3%82%AF%E3%83%B3.html)

解析ツリー = DOMツリーです。

>生成される「解析ツリー」は DOM 要素と属性のノードのツリーです。DOM は「Document Object Model」の略で、HTML ドキュメントや、HTML 要素と JavaScript などの外部世界とのインターフェースをオブジェクトで表現したものです。ツリーのルートは「Document」オブジェクトです。
DOM とマークアップはほぼ 1 対 1 の関係になっています。たとえば、次のようなマークアップがある場合、
    
> `html
<html>
  <body>
   <p>
     Hello World
    </p>
    <div> <img src="example.png"/></div>
  </body>
</html>
`
次のような DOM ツリーに変換されます。

> ![https://www.html5rocks.com/ja/tutorials/internals/howbrowserswork/image015.png](https://www.html5rocks.com/ja/tutorials/internals/howbrowserswork/image015.png)
https://www.html5rocks.com/ja/tutorials/internals/howbrowserswork より

パーサーがトークナイザーにトークンを要求
→構文ルールと一致すればそのトークンに対応するノードが解析ツリーに追加される
→別のトークンを要求
という流れで解析されていきます。


    
##### CSS
解析され、CSS Object Modelに変換されます。
参考になりそう → [ブラウザの仕組み - CSSの解析](https://www.html5rocks.com/ja/tutorials/internals/howbrowserswork/#CSS_parsing)

##### Java Script
JSも解析されます。
ただし、JSが読み込まれた時点でHTMLの解析を中断してJSの解析が開始されます。
また、JSがまだ読み込まれていないスタイルシートの影響を受けそうな特定のスタイルプロパティにアクセスした場合、JSはブロックされます。

参考になりそう → [JavaScriptがブラウザでどのように動くのか - mercari engineering](https://engineering.mercari.com/blog/entry/20220128-3a0922eaa4/)

##### レイアウト

レンダラー（レンダーツリー内の要素）を作成してツリーに追加したとき、それらには位置やサイズがありません。
これらの値を計算することを「レイアウト」または「リフロー」といいます。

##### 解析〜表示の流れ

1. HTML/CSS/JavaScriptに対して↑の処理を行う
1. DOMツリー、CSSOMツリーからレンダーツリー(視覚的な要素を表示順に並べたツリー)を生成。
1. レイアウト（もしくはリフロー）処理によりレンダーツリー内の要素に正確な位置や座標を割り当て
1. 画面に描画する

#### イラストの再掲

![all-about-browser](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/sketchnotes/browser.jpg)
> https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/5-browser-extension/1-about-browsers より

ここまででおおよそこのイラストの構成要素が理解できました。

#### トピック

- ブラウザとは何か？
    - エンドユーザーがサーバーからコンテンツにアクセスしてWebページを表示することを可能にするアプリケーション。
- 最初のブラウザは `Sir Timothy Berners-Lee` によって1990年に作られた `WorldWideWeb`
    - 画像は扱えず、文字だけの文章同士をリンクでたどりながら閲覧できるソフトだった。
- ブラウザは通常、Webコンテンツをキャッシュする機能を持つ。これは毎回サーバからデータを受け取らなくても良いようにするため。
- ユーザアクティビティの記録はCookiesに残される。
- ブラウザは全て少しずつ違う。それぞれ長所/短所があるため、複数のブラウザで正しく動作するようなWebページの作り方を学ぶことが大切。
    - [https://caniuse.com/](https://caniuse.com/) を使うとどのブラウザに何が対応しているか調べることが出来るのでとても便利。

### ブラウザ拡張機能

ブラウザ拡張機能は繰り返し行うことが多い作業に素早くアクセスしたいときなどに便利。例えば色のチェック、パスワードの管理など。

#### 拡張機能作成に必要な要素

- APIキー
    - [APIキー](https://www.co2signal.com/)を取得しておく
- マップに対応する[地域コード](http://api.electricitymap.org/v3/zones)
    ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/f700a2f3-4f47-5003-3fc8-12a2959de681.png)
- npm
    - パッケージ管理ツール。インストールしておく。
    
スタート時点のフォルダ構成は以下。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/0b55d960-5be0-725f-99be-f2c0302b3354.png)

- dist
    - manifest.json
    - index.html (HTML)
    - background.js (バックグラウンドのJavaScript)
    - main.js (ビルド後のJavaScript)
- src
    - index.js (ビルド前のJavaScript、自分が編集する)

<details><summary>manifest.json is 何</summary><div>

```json:manifest.json
{
	"manifest_version": 2,
	"name": "My Carbon Trigger",
	"version": "0.1.0",
	"permissions": ["<all_urls>"],
	"background": {
		"scripts": ["background.js"]
	},
	"browser_action": {
		"default_popup": "index.html"
	}
}
```

[ウェブアプリマニフェスト | MDN](https://developer.mozilla.org/ja/docs/Web/Manifest)

> **ウェブアプリマニフェスト**は、[プログレッシブウェブアプリ](https://developer.mozilla.org/ja/docs/Web/Progressive_web_apps) (PWA) と呼ばれる一連のウェブ技術の一部であり、アプリストアを通さずに端末のホーム画面にインストールすることができるものです。単純なホーム画面リンクやブックマークを持つ通常のウェブアプリとは異なり、 PWA は事前にダウンロードしてオフラインでも動作するだけでなく、通常の [Web API](https://developer.mozilla.org/ja/docs/Web/API) を使用することもできます。

> ウェブアプリマニフェストは、ウェブアプリケーションについて、ウェブアプリをダウンロードしたり、ユーザーにネイティブアプリと同じように見せる（例えば、端末のホーム画面にインストールされ、ユーザーに素早いアクセスと豊かな操作性を提供するなどの）ために必要なの情報を [JSON](https://developer.mozilla.org/ja/docs/Glossary/JSON) テキストファイルで提供します。 PWA のマニフェストには、その名前、作者、アイコン、バージョン、説明、および (他のものの中で特に) 必要なすべてのリソースのリストが含まれています。
</div></details>

#### HTMLの構築

APIキーとリージョンコードの確認、地域の二酸化炭素消費量表示が出来るようにしていきます。

```html
<!--form area-->
	<div>
		<h2>New? Add your information</h2>
	</div>
<form class="form-data" autocomplete="on">
	<div>
		<h2>New? Add your Information</h2>
	</div>
	<div>
		<label for="region">Region Name</label>
		<input type="text" id="region" required class="region-name" />
	</div>
	<div>
		<label for="api">Your API Key from tmrow</label>
		<input type="text" id="api" required class="api-key" />
	</div>
	<button class="search-btn">Submit</button>
</form>
```

`html
<!--result area-->
	<div class="result">
		<div class="loading">loading...</div>
		<div class="errors"></div>
		<div class="data"></div>
		<div class="result-container">
			<p><strong>Region: </strong><span class="my-region"></span></p>
			<p><strong>Carbon Usage: </strong><span class="carbon-usage"></span></p>
			<p><strong>Fossil Fuel Percentage: </strong><span class="fossil-fuel"></span></p>
		</div>
		<button class="clear-btn">Change region</button>
	</div>
`

- ローディング/エラー/データなどのクラスはおそらく状態に応じてレイアウトを変更するために使う。
- [MDN - autocomplete](https://developer.mozilla.org/ja/docs/Web/HTML/Attributes/autocomplete)
    - ユーザの入力支援(自動で候補が表示される機能)
    - `on`で補完ON、`name`で氏名、など
- [MDN - required](https://developer.mozilla.org/ja/docs/Web/HTML/Attributes/required)
    - 入力必須パラメータ
- [MDN - label](https://developer.mozilla.org/ja/docs/Web/HTML/Element/label)

    > <label> 要素と同一の文書内にあるラベル付け可能フォーム関連要素の id。文書中の for 属性の値と合致する id を持つ最初の要素がラベル付け可能な要素であれば、このラベル要素の示すラベル付きコントロールとなります。ラベル付け可能要素でなければ、 for 属性は効果がありません。一致する id 値を持つ他の要素が文書内のその後にあったとしても、考慮されません。 

    - idが同じラベル付け可能要素があればその要素と関連付けられる。
    - [ラベル付け可能要素](https://developer.mozilla.org/ja/docs/Web/Guide/HTML/Content_categories#:~:text=%E3%82%92%E5%90%AB%E3%81%BF%E3%81%BE%E3%81%99%E3%80%82-,%E3%83%A9%E3%83%99%E3%83%AB%E4%BB%98%E3%81%91%E5%8F%AF%E8%83%BD,-%3Clabel%3E%20%E3%81%AB%E9%96%A2%E9%80%A3)は  `<button>`, `<input>`, `<keygen>`, `<meter>`, `<output>`, `<progress>`, `<select>`, `<textarea>` 。


#### 拡張機能のビルド&デプロイ(Chromeの場合)

1. `npm install` で必要なパッケージをインストール(`package.json` を参照してインストールしてくれる。)
2. `npm run build` で `src` をビルド
3. 設定 > 拡張機能 にアクセス
4. 「パッケージ化されていない拡張機能を読み込む」を選択
5. dstフォルダを選択
6. 以降、変更を反映させたい場合は「更新」を押下する。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/747013ac-0508-42ab-1667-0c902d3ab535.png)
デプロイ結果
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/b1f734ae-f7e3-6b38-2dcc-6ab2f1cb28c6.png)
動作も問題なさそう。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/bb688bd6-3402-cf5c-3b90-7535ac519ba8.png)

### 課題

- **インストールした拡張機能のソースコードを見てみる**
    - 普通に見れちゃうんですね。実装の参考的な意味ではありがたいんですが、パクリなどの問題は大丈夫なんでしょうか。
    - [ブラウザ拡張機能のソースコードを確認する](https://www.bugbugnow.net/2021/06/sourcecode-for-extension.html)
    - [Chrome拡張機能のソースコードを見る方法](https://nullnull.dev/blog/how-to-view-the-source-code-of-a-chrome-extension/#%F0%9F%8F%A9%F0%9F%8C%99%F0%9F%9B%8F%F0%9F%92%91)
- **ブラウザの歴史を学んでみる**
    - 今やすっかり邪魔者扱いのIEも覇権を取っていた時期があると思うと何とも言えない気分になりますね・・・
    - [The History of Web Browsers](https://www.mozilla.org/firefox/browsers/browser-history/)
    - [History of the Web](https://webfoundation.org/about/vision/history-of-the-web/)
    - [An interview with Tim Berners-Lee](https://www.theguardian.com/technology/2019/mar/12/tim-berners-lee-on-30-years-of-the-web-if-we-dream-a-little-we-can-get-the-web-we-want)
    - [20年以上にわたるWebブラウザーのシェア推移を可視化したムービーが面白い](https://forest.watch.impress.co.jp/docs/serial/yajiuma/1205144.html)

### 学んだこと

* ブラウザの仕組み、構造などの概要
* Webページが読み込まれる時に起きていることの概要
* `autocomplete` `required`など
* パッケージ化していない状態で拡張機能のデプロイ