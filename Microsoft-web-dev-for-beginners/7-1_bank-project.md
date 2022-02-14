## はじめに

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

[〜②JavaScript基礎まで【導入/アクセシビリティ/JavaScript の基礎】](https://qiita.com/NasuPanda/items/d78514969191491a4bcd)
[③テラリウム構築 【HTML・CSS基礎/DOM操作/クロージャ】](https://qiita.com/NasuPanda/items/59b8e43d8d6fb609c7d5)
[④タイピングゲーム 【JavaScriptのイベント処理】　本記事](https://qiita.com/NasuPanda/items/340f391ee9f167bf4333)
[⑤-1ブラウザ拡張機能 【ブラウザの仕組み/拡張機能作成の導入】](https://qiita.com/NasuPanda/items/d0189565d039c2c11383)
[⑤-2ブラウザ拡張機能 【API/LocalStorage/BackGround/Performance】](https://qiita.com/NasuPanda/items/4186e6701cd2d4d68bb2)
[⑥スペースシューティングゲーム 【ゲーム開発の基礎/Pub-Sub/Canvas/衝突検出】](https://qiita.com/NasuPanda/items/16ffb297be9b862d2785)
**⑦架空銀行プロジェクト【ログイン/データ管理/状態管理】　本記事**

***

### 記事の目的

- 学習のアウトプット
- 教材を使ってみたところかなり良かったので、その紹介

### 注意点

自身の学習のアウトプットがメインなので、理解できているところ(他言語と共通の箇所など)は省いています。
また、課題やtipsについても結構省きます。
この教材に興味を持った方はぜひご自分で取り組んでみてください。

# 7 Bank-project

https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project

Node.jsを用いて架空の銀行を構築していきます。

![bank-image][https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/bank-result.png?raw=true]

### やること

1. [Web アプリの HTML テンプレートとルート](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project/1-template-route/translations/README.ja.md)
2. [ログインと登録フォームの構築](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project/2-forms/translations/README.ja.md)
3. [データの取得と利用方法](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project/3-data/translations/README.ja.md)
4. [状態管理の概念](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project/4-state-management/translations/README.ja.md)

### 学習の目的

- ルーティングと HTML テンプレートを使ったマルチページサイトのアーキテクチャの足場の作り方を学ぶ
- フォームの構築と検証ルーチンの渡し方について学ぶ
- アプリのデータの出入り、データの取得方法、保存方法、廃棄方法
- アプリの状態を保持する方法とプログラムで管理する方法を学ぶ

## HTMLテンプレートとルート

### イントロ

ブラウザにJavaScriptが登場して以来、Webサイトはこれまで以上にインタラクティブ・複雑になっている。

> **インタラクティブ**とは、相互に作用する、対話的な、双方向の、相乗効果の、などの意味を持つ英単語。ITの分野では、情報の送り手と受け手の関係が固定的ではなく、その場で互いにやり取りできる状態を指す。
> 情報システムやソフトウェアでは、利用者の操作や入力に対してシステムが即座に反応を返し、相互にやり取りをする中で処理を進めていくような操作方式をインタラクティブであるという。
> [インタラクティブ - IT用語辞典]([https://e-words.jp/w/インタラクティブ.html](https://e-words.jp/w/%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%83%96.html))

Webアプリケーションは高度にインタラクティブ（=ユーザとの対話が多く生じる）なので、アクションが実行される度に全ページがリロードされてしまうと、ユーザをを待たせることになってしまう。

そのため、JavaScriptによるDOM操作でHTMLを直接更新し、よりスムーズなUXを提供する。

このレッスンではHTMLテンプレートを使用して、ページ全体をリロードすることなく表示・更新出来る複数の画面を作成、Webアプリ作成の基礎を構築していく。

### 準備

`npx lite-server` コマンドを使用してローカルのWebサーバを作成する。

#### `lite-server`って何？

[lite-serverのリポジトリ](https://github.com/johnpapa/lite-server)

> BrowserSyncは、超高速・軽量の開発サーバーとして、私たちが望むことのほとんどを実現してくれます。静的コンテンツを提供し、変更を検出し、ブラウザをリフレッシュし、多くのカスタマイズを提供します。
> SPA を作成する場合、ブラウザにのみ知られているルートがあります。例えば、/customer/21はAngularアプリのクライアントサイドルートかもしれません。このルートを手動で入力したり、Angularアプリのエントリポイントとして直接リンクした場合（別名ディープリンク）、Angularがまだロードされていないため、静的サーバーはリクエストを受け取ります。サーバーはルートにマッチするものを見つけられず、404を返します。この場合の望ましい動作は、index.html（または定義したアプリの開始ページ）を返すことです。BrowserSyncは、自動的にフォールバックページを許可しません。しかし、カスタムミドルウェアを使用することは可能です。そこで、lite-serverの出番です。

lite-serverは、BrowserSyncの周りをカスタマイズしたシンプルなラッパー。
SPAを簡単に提供することができる。

#### BrowserSyncって何?

> テキストエディターでHTML,CSS,JavaScriptのコードを編集して、結果を確認するのにWebブラウザーにフォーカスを移してF5で更新して……
> というWeb開発のワークフローを簡素化するプログラムです。
> BrowserSyncはファイルの変更を監視して、変更を即座にブラウザーに反映させることができます。
> しかもCSSファイルの編集はページの再読み込みをすることなく反映されます。
> 複数ブラウザーを立ち上げていてもOK！モバイルブラウザーも自動で同期します！

参考 : [BrowserSyncの使い方](https://qiita.com/niusounds/items/a95978f9a1cb328d3021)

#### SPAって何？

> シングルページアプリケーションとは、Webアプリケーションの構成法の一つで、Webブラウザ側でページの移動を行わず、最初に読み込んだWebページ上のスクリプトがサーバとの通信や画面遷移を行う方式。
> Webサービスとして従来のソフトウェアのような高度な機能を実装する選択肢の一つとしてよく知られており、有力なJavaScriptフレームワークの中にもシングルページアプリケーションの構成を基本とするもの（Angular、Vue.js、Reactなど）がある。
> [SPA - IT用語辞典](https://e-words.jp/w/%E3%82%B7%E3%83%B3%E3%82%B0%E3%83%AB%E3%83%9A%E3%83%BC%E3%82%B8%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3.html)

参考 : [SPA(SinglePageApplication)の基本 - Qiita](https://qiita.com/takanorip/items/82f0c70ebc81e9246c7a)

- その名の通り、1つのHTMLで構成されるWebアプリ。
- 最初のリクエストのみWebページ全体を読み込む。
- JavaScriptでDOMを操作して必要な場所(差分)だけ更新する。
- **従来との違い**

    - **従来**(サーバーサイドレンダリング)

    1. ユーザ操作
    2. サーバーにリクエスト
    3. サーバーでWEBページを生成
    4. クライアント側へWEBページを送信
    5. サーバーから受け取ったWEBページを描画

    - **SPA**

    1. 初期ページ読み込み（初期描画）
    2. ユーザ操作
    3. サーバーにリクエスト
    4. サーバーからクライアント側へ差分データを送信
    5. 差分のみを更新

まとめると、

- **BrowserSync**はWebアプリの開発を楽にしてくれる開発サーバー。
- **lite-server**はBrowserSyncをSPAに対応な形にカスタマイズしたラッパー。
- **SPA**は1つのHTMLを読み込み、JavaScriptにより必要な箇所だけページを更新する手法。

#### ボイラープレート

以下のHTMLボイラープレートから実装を始める。

```html
<!DOCTYPE html><html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank App</title>
  </head>
  <body>
    <!-- ここで作業 -->
  </body>
</html>
```

**ボイラープレートとは？**

> コンピュータプログラミングでは、殆ど、または全く変化することなく、複数の場所で繰り返される定型コードのセクションのこと。冗長な言語を使用する場合、プログラマーはコードを少しだけ書くだけでも多くのコードを作成する必要がある。このような定型コードはボイラープレートと呼ばれる。
> [ボイラープレートコード - Wikipedia](https://ja.wikipedia.org/wiki/%E3%83%9C%E3%82%A4%E3%83%A9%E3%83%BC%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%82%B3%E3%83%BC%E3%83%89)

なお、`lang`は日本なら`ja`。
`lang`を設定しておくと自動翻訳の恩恵を受けれる・プログラムが言語を認識してくれる、などのメリットがあるらしい。

### HTMLテンプレート

Webページに複数の画面を作成したい場合、通常は表示したい画面ごとに1つのHTMLファイルを作成する。

この手法の問題点として、以下が挙げられる。

- 画面切り替え時HTML全体を再読み込みする必要があり、非効率
- 画面間のデータ共有が難しい

もう1つのアプローチとして、

**アプリ全体でHTMLファイルを1つだけ**持ち、`<template>`要素を使って複数の[HTMLテンプレート](https://developer.mozilla.org/ja/docs/Web/HTML/Element/template)を定義する手法が考えられる。

テンプレートはブラウザに表示されない**再利用可能なHTMLブロック。
**JavaScriptを使い**実行時にインスタンス化**する。

#### 実装

```html
<div id="app">Loading...</div>
```

この要素の内容が置き換えられる。
そのため、アプリの読み込み中(=置き換えられていない時)に表示される読み込みメッセージやインジケータを入れておくと良い。

ログインページのHTMLテンプレートを追加する。

```html
<template id="login">
  <h1>Bank App</h1>
  <section>
    <a href="/dashboard">Login</a>
  </section>
</template>
```

次に、ダッシュボードページ用のHTMLテンプレートを追加する。

- タイトルとログアウトリンクのあるヘッダー
- 銀行口座の当座預金残高
- 表に表示されるトランザクションのリスト

```html
<template id="dashboard">
  <header>
    <h1>Bank App</h1>
    <a href="/login">Logout</a>
  </header>
  <section>
    Balance: 100$
  </section>
  <section>
    <h2>Transactions</h2>
    <table>
      <thead>
        <tr>
          <th>Date</th>
          <th>Object</th>
          <th>Amount</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </section>
</template>
```

なお、`<template>`をコメントアウトすれば実際にどのように見える確認することが出来る。

### JavaScriptでテンプレートを表示する

`<template>` に設定したHTMLをインスタンス化して表示するためにはJavaScriptのコードを追加する必要がある。

通常次の3ステップで行われる。

1. `document.getElementById`などを利用してDOM内のテンプレート要素を取得
2. `cloneNode` を使用してテンプレート要素のクローンを作成
3. `appendChild` などを利用して、可視要素の下のDOMにアタッチする

#### なぜクローンする必要がある？

**クローンせずに `template` を利用してみる**

* 呼び出す前

`#document-fragment` がいて、中に要素が入っている。
![non-clone-before](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/non-clone-before.png?raw=true)

* 呼んだ後

中身がなくなった。
![non-clone-after](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/non-clone-after.png?raw=true)

[<template> | MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/template)を見てみると、以下の記述が。

> ただし、 `[HTMLTemplateElement](https://developer.mozilla.org/ja/docs/Web/API/HTMLTemplateElement)`の `[content](https://developer.mozilla.org/ja/docs/Web/API/HTMLTemplateElement/content)`プロパティは、読み取り専用の `[DocumentFragment](https://developer.mozilla.org/ja/docs/Web/API/DocumentFragment)` で、テンプレートが表現する DOM サブツリーを保持しています。

`DocumentFragment`について調べてみる。

#### `DocumentFragment`

[DocumentFragment - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/DocumentFragment)

- 直訳すると文書の断片。
- 基本的な使い方として、以下のような流れで利用する。
    1. 空の`DocumentFragment` を作る
    2. その中に独立したDOMツリーを構成
    3.  `appendChild` などを利用してDOMに追加する
- ↑の操作を行うと断片内のノードは**DOMに移動**、空の `DocumentFragment` が残る。
- **大量の要素をDOMに追加したい**時などに利用する。

まとめると、

- `template` 要素の `content` プロパティは `DocumentFragment` を利用している。
- `DocumentFragment` は大量の要素をDOMに一気に追加したい時などに使う。
- 呼び出した際に `DocumentFragment` の中身は移動してしまうため、複数回呼び出したい時はコピーを取って利用するようにする。

#### 実装

```js
function updateRoute(templateId) {
  const template = document.getElementById(templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

- `updateRoute` 関数では上記の3ステップと同じことをしている。
    1. `document.getElementById`などを利用してDOM内のテンプレート要素を取得
    2. `cloneNode` を使用してテンプレート要素のクローンを作成
    3. `appendChild` などを利用して、可視要素の下のDOMにアタッチする
- [node.cloneNode](https://developer.mozilla.org/ja/docs/Web/API/Node/cloneNode)
    - 構文は`var dupNode = node.cloneNode(deep);`
    - 子孫ノードも含めて複製したい場合は`deep`引数に`true`を渡す。

✅ `innerHTML=""` の目的は何？やらないとどうなる？

[Element.innerHTML](https://developer.mozilla.org/ja/docs/Web/API/Element/innerHTML)

主な用途は、**要素の中身の取得・設定。**
つまり、ここでは`””`を設定することで`id=app`の要素の中身を削除している。
これをしないと、要素の中身(`”Loading...”`)が残ったままになってしまう。

### ルートの作成

Webアプリの文脈では、URLを表示すべき画面にマッピングする操作を**ルーティング**と呼ぶ。

複数のHTMLファイルを持つWebサイトではファイルパスがURLに反映されるため、自動的に行われる。

例

    mywebsite/index.html
    mywebsite/login.html
    mywebsite/admin/index.html

ルートに `mywebsite` を指定して Web サーバを作成した場合、URL のマッピングは以下のようになる。

    https://site.com            --> mywebsite/index.html
    https://site.com/login.html --> mywebsite/login.html
    https://site.com/admin/     --> mywebsite/admin/index.html

しかし、今回作成するWebアプリではすべての画面を含む1つのHTMLファイルを使用しているので、このデフォルトの動作は役に立たない。

そのため、マッピングを手動で作成し、JavaScriptにより表示されるテンプレートの更新を実行する必要がある。

#### 実装

URLパスとテンプレート間のマッピングを実装するために、シンプルな[map](https://en.wikipedia.org/wiki/Associative_array)を実装する。

※ [連想配列](https://ja.wikipedia.org/wiki/%E9%80%A3%E6%83%B3%E9%85%8D%E5%88%97)のことをmapと呼ぶこともあるらしい

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard' },
};
```

さらに、`updateRoute`関数を少し修正する。

引数に`templateId`を直接渡すのではなく、現在のURLを見て、`rotes`により対応する`templateId`を取得するようにする。

URLからパス部分だけを取得するには、[window.location](https://developer.mozilla.org/ja/docs/Web/API/Location).pathnameを使う。

```js
// https://qiita.com/settings/profileで使ってみる

console.log(window.location.pathname)
// ==>  /settings/profile
```

```js
/** HTMLテンプレートの表示を更新する */
function updateRoute() {
  const path = window.location.pathname; // ==> /login or /dashboard
  const route = routes[path];

  const template = document.getElementById(route.templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

![login](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/first-login.png?raw=true)


![dashboard](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/first-dashboard.png?raw=true)

動作はOK。

✅ URLに未知のパスを入力するとどうなる？どうすれば対処できる？

未知のパスを入力するとHTMLは当然更新されず、以下のエラーが発生する。

![undefined-url](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/undefined-url-error.png?raw=true)

**対処**

未知のパスが入力された
→`routes`に存在しないキーが渡される
→`route`が`undefined`になる
→`undefined`をキャッチして、エラー用のHTMLテンプレートを表示すれば良いのでは？

- `routes` に `error` を追加

```js
const routes = {
    '/login': { templateId: 'login' },
    '/dashboard': { templateId: 'dashboard' },
    '/error': { templateId: 'error' }
};
```

- `undefined` の時の分岐作成
- ついでに`route`を`let`に変更

```js
let route = routes[path];

if (!route) route = routes['error']
```

- 対応するテンプレートを作成

```js
<template id="error">
    <h1>Error!</h1>
    <p>Sorry, something went wrong.</p>
    <p>Check the url and try again.</p>
</template>
```

![display-error](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/display-error.png?raw=true)

OK。

### ナビゲーションの追加

次のステップとして、URLを手動で変更することなくページ間を移動出来るようにする。
これには、次の2つができる必要がある。

1. 現在のURLを更新
2. 新しいURLに基づいてテンプレートを更新

2番は既に実装したので、1番を実現する方法を考える。

→ `history.pushState` を使う。これはHTMLをリロードせずにURLを更新して、閲覧履歴に新しいエントリを作成できる。

✅ HTMLアンカー要素`<a href>`は単独でハイパーリンクを作る事ができるが、デフォルトではHTMLをリロードさせる。そのため、`preventDefault`を使用する必要がある。

#### 実装

```js
function navigate(path) {
	window.history.pushState({}, path, path);
  updateRoute();
}
```

この関数は与えられたパスに基づいて現在のURLを更新する。
また、履歴レコードに指定したURLを追加する。

パスが定義されたルートにマッチしない場合、ログインページにリダイレクトするようにする。

```js
function updateRoute() {
  const path = window.location.pathname;
  const route = routes[path];

  if (!route) {
    return navigate('/login');
  }

  ...
```

ログインにリダイレクトで良かったのか・・・

リンククリック時の動作。
リンクからURLを取得、デフォルトのリンク動作を防ぐ。

```js
/** リンククリック時に実行される */
function onLinkClick(event) {
    // リンクのデフォルト動作(HTML更新)を防ぐ
    event.preventDefault();
    navigate(event.target.href);
}
```

HTMLにバインディングを追加する。

```html
<a href="/dashboard" onclick="onLinkClick(event)">Login</a>
...
<a href="/login" onclick="onLinkClick(event)">Logout</a>
```

##### `History.pushState()`

- [History.pushState() - MDN](https://developer.mozilla.org/ja/docs/Web/API/History/pushState)
- [JavaScriptでURLを操作するメモ - Qiita](https://qiita.com/PianoScoreJP/items/fa66f357419fece0e531)
- [JavaScriptのhistory.pushState()とは？ – Rainbow Engine](https://rainbow-engine.com/javascript-history-pushstate/)

###### 構文

`history.pushState(state, title[, url])`

履歴に指定したURLを追加する。
ページの再読み込みは発生しない。

###### 引数

**`state`**
`popState` イベント(後述)が持つ `event.state` の値。
履歴レコードとセットで生成されるオブジェクト。

`**title**`
理論上はブラウザのタブタイトルを変更するが、現在ほとんどのブラウザで無視されている。

`**url**`
履歴に指定したURLを追加。

### ブラウザの戻るボタン/進むボタンの扱い

戻るボタンを押して履歴を確認してみると、以下のようになっている。

![history](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/url-history.png?raw=true)

戻るボタンをクリックしてみると、現在のURLは変更されるが、同じテンプレートが表示され続けている。

これは、 `pushState` が呼ばれる度にURLを更新する必要があることは知っているが、
履歴が変わる度に `updateRoute` を呼び出す必要があることを知らないから。

`[history.pushState` のドキュメント](https://developer.mozilla.org/ja/docs/Web/API/History/pushState)を見てみると、**状態が変化した場合には`[popstate](https://developer.mozilla.org/docs/Web/API/Window/popstate_event)`イベントが発生する**ことがわかる。コレを使ってこの問題を解決していく。

#### `popstate` イベントについて

[WindowEventHandlers.onpopstate - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/WindowEventHandlers/onpopstate)

> `popstate` イベントは、同じ文書の2つの履歴項目の間で、アクティブな履歴項目が変わるたびにウィンドウに発行される。
> アクティブな履歴項目が `history.pushState()` を呼び出したことで作成されたり、 `history.replaceState()` を呼び出したことで影響されたりした場合、 `popstate` イベントの `state` プロパティが履歴項目の状態オブジェクトのコピーを保持する。
> メモ : `history.pushState()` 又は `history.replaceState()` を呼び出すことは、 `popstate` イベントのトリガーにはなりません。 `popstate` イベントは、戻るボタンをクリックしたり (又は JavaScript で `history.back()` を呼び出したり)、同じ文書で2つの履歴項目間を移動したりするように、ブラウザーのアクションを実行することのみがトリガーになります。

戻る/進むボタンなどでページ遷移した場合、 `popState` イベントを捕まえてページを更新してやる必要があるということ。

#### 実装

`onpopstate` に `updateRoute` をアタッチするだけ。

```js
/**
 * popstateイベント発生時updateRouteを呼び出し。
 * このイベントは戻る/進むボタンによるページ遷移などで発生する。
*/
window.onpopstate = () => updateRoute();
updateRoute();
```

### 課題 ルーティングの改善

以下の2機能を追加。`routes` 宣言で追加された新しいルートでも動作すること。

- テンプレートが変更された時にタイトルが更新されるようにする
- ダッシュボードページが表示される度にコンソールに「Dashboard is shown」と表示される

#### 新しいルートでも動作するようにする

参考にするコード(`updateRoute`)

```js
/** HTMLテンプレートの表示を更新する */
function updateRoute() {
    const path = window.location.pathname;
    const route = routes[path];
    // 未知のパスが入力された場合ログインページにリダイレクトする
    if (!route) return navigate('/login')

    const template = document.getElementById(route.templateId);
```

`updateRoute` を参考に、 `route.templateId` を参照する。

`route.templateId` を複数回使うので 出来れば`templateId` を変数として参照したい。

だが、存在しない `route` の `templateId` を探しに行くと `Uncaught TypeError: Cannot read properties of undefined (reading 'templateId')` が出る。このエラーをキャッチしてまで `templateId` を変数に入れる必要はない・・・と思う。

#### タイトルの更新

`document.title` で取得・更新出来る。

![document-title](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/documnet-title.png?raw=true)

```js
/** ページタイトルを更新する */
function updateTitle(route) {
    document.title = route.templateId;
}
```

後は `updateRoute` 内で呼び出せば良い。

#### ダッシュボード表示の通知

同じように `route.tempalteId` を利用、 `updateRoute` 内で呼び出す。
関数名は少し迷ったが、「ダッシュボードの表示を通知」とした。

```js
/** ダッシュボード表示時、コンソールに通知 */
function notifyDashboardDisplay(route) {
    if (route.templateId === 'dashboard') console.log('Dashboard is shown.');
}
```

![notify-dashboard](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/notify-dashboard-display.png?raw=true)

OK。