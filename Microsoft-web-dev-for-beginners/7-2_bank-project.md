<!--
title : MicrosoftのWeb開発教材を使ってみた ⑦-2銀行プロジェクト【ログイン/データ管理/状態管理】
tags : API 初心者
-->

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
⑦-1銀行プロジェクト【SPA/'<template>'/HTMLフォーム】
**⑦-2銀行プロジェクト【ログイン/データ管理/状態管理】　本記事**

***

### 記事の目的

- 学習のアウトプット
- 教材を使ってみたところかなり良かったので、その紹介

### 注意点

自身の学習のアウトプットがメインなので、理解できているところ(他言語と共通の箇所など)は省いています。
また、課題やtipsについても結構省きます。
この教材に興味を持った方はぜひご自分で取り組んでみてください。

# 7 Bank-projectの続き

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

## データの取得と利用

### イントロ

全てのWebアプリの中核には、**データ**が有る。

データには様々な形があるが、その目的は「ユーザに情報を表示すること」であることが多い。

Webアプリがますますインタラクティブで複雑になってきているため、ユーザがどのように情報にアクセスして対話するかは、現在のWeb開発では重要な要素になっている。

このレッスンでは、サーバーから非同期にデータを取得し、そのデータを利用してHTMLをリロードせずにWebページに情報を表示する方法を見ていく。

### AJAXとデータ取得

#### 従来のWebサイト

従来のWebサイトは、

- ユーザがリンクをクリックしたり
- フォームを使用してデータを送信したり

する度にページ全体をリロードする(=サーバは新しいHTMLを返す)ことで、表示されるコンテンツを更新する。

リロードの際に、以下のような制限が生じる。

- 現在のユーザのアクションを中断
- リロード中はインタラクションを制限

このワークフローはマルチページアプリケーション/MPAとも呼ばれる。

![mpa]([https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/7-bank-project/3-data/images/mpa.png](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/7-bank-project/3-data/images/mpa.png))

#### SPA

Webアプリがより複雑・インタラクティブになり始めた頃、**[AJAX](https://ja.wikipedia.org/wiki/Ajax)**と呼ばれる技術が登場した。

これにより、**HTMLをリロードすることなく**、JavaScriptを使ってサーバから非同期にデータを送受信することが可能になった。

結果として、より高速なページ更新・よりスムーズなユーザのインタラクションを実現する事ができる。

また、サーバから新しいデータを受信すると、DOM API を用いて現在のHTMLページをJavaScriptで更新することも出来る。

このアプローチは現在シングルページアプリケーション/SPAと呼ばれるものに発展してきた。

![spa]([https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/7-bank-project/3-data/images/spa.png](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/7-bank-project/3-data/images/spa.png))

AJAX導入当初はデータを非同期で取得できるAPIは`XMLHttpRequest`のみだった。

しかし、現在はより強力な`FetchAPI`が実装されている。`FetchAPI`はPromiseを使用してJSONデータを操作するのに適している。

- 従来はページ更新=HTMLの再リロードであり、様々な不都合があった。このアプローチはMPAと呼ばれる。
- AJAXと呼ばれる非同期通信により、HTMLをリロードすることなく、JavaScriptを使いサーバからデータを送受信することが出来るようになった。このアプローチはSPAと呼ばれる。

#### 実装

`login` を実装していく。
フォームコントロールは `name` 属性(ここでは`user`)によりアクセスできる。

```js
async function login() {
  const loginForm = document.getElementById('loginForm')
  const user = loginForm.user.value;
}
```

APIを叩いてアカウントデータを取得。

```js
async function getAccount(user) {
  try {
    const response = await fetch('//localhost:5000/api/accounts/' + encodeURIComponent(user));
    return await response.json();
  } catch (error) {
    return { error: error.message || 'Unknown error' };
  }
}
```

- データを問い合わせるだけなのでURL以外の引数は不要。
- `fetch` はデフォルトで `GET` リクエストを作成する。
- [encodeURIComponent](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)でエスケープする。
    - URLではなく**[URI](https://developer.mozilla.org/ja/docs/Glossary/URI)。**MDNによると、

    > **URI** *(Uniform Resource Identifier)*
    は、リソースを示す文字列です。もっとも一般的なものは [URL](https://developer.mozilla.org/ja/docs/Glossary/URL)
     であり、ウェブ上の場所を指定することで、リソースを識別します。

    - **URIはURL(locater)とURN(Name)の総称**。
    - [encodeURI](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/encodeURI)もある。動作が少し違う。

`login` を `getAccount` を使うように変更する。

```js
async function login() {
  const loginForm = document.getElementById('loginForm')
  const user = loginForm.user.value;
  const data = await getAccount(user);

  if (data.error) {
    return console.log('loginError', data.error);
  }

  account = data;
  navigate('/dashboard');
}
```

- `getAccount` は非同期関数なので、 `await` で処理を待つ。
- データをどこかに保存しておく必要がある。変数 `account` はまだ存在しないので、ファイルの先頭でグローバル変数として宣言しておく。

    ```js
    let account = null;
    ```


HTMLを修正してログインフォームが送信された時に `login` 関数が呼び出されるようにする。

```js
<form id="loginForm" action="javascript:login()">
```

`register` に以下を追加することで、

グローバル変数`account`に値を保存
→ユーザ登録が完了したらダッシュボードにリダイレクト

という動作を実現できる。

```js
account = result;
navigate('/dashboard');
```

> ✅ [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/ja/docs/Web/HTTP/CORS)と呼ばれる技術を使用することで、サーバーがレスポンスに特殊なヘッダを追加し、特定のドメインの例外を許可することで、クロスオリジンの HTTP リクエストを実行することが可能になります。

### データの表示

ユーザデータが取得できたので、それを表示するために既存のHTMLを更新する。

DOMから要素を取得、修正したり子要素を追加したりしていく。

- 要素のテキストを変更するには `textContent` プロパティを使用する。
    - この値を変更すると、**全ての子要素が削除**され、指定したテキストに置き換えられる。
    - 空の文字列を代入することで要素全てを削除する効率的な方法でもある。
- 新しい子要素を作成するには `document.createElement` と `append` メソッドを使う。
- `innerHTML` プロパティを使用してHTMLの内容を変更することも出来るが、これは[クロスサイトスクリプティング(XSS)攻撃](https://developer.mozilla.org/ja/docs/Glossary/Cross-site_scripting)に対して脆弱なので避けるべき。
    - 悪意あるコードをWebサイトに挿入する攻撃。
    - バリデーション・エンコーディングにより対策する。

#### 実装

現在、存在しないユーザでログインしようとするとコンソールにはメッセージが表示されるが、HTMLには何も表示されない。

そのため、必要に応じてエラーメッセージを表示できるようにする。

まずはプレースホルダーを追加。

```js
...
<div id="loginError"></div>
<button>Login</button>
...
```

`id` とテキストが与えられると、一致する `id` を持つ要素のテキストを更新する関数。

```js
function updateElement(id, text) {
  const element = document.getElementById(id);
  element.textContent = text;
}
```

`login` 関数のエラーメッセージの代わりに使う。

```js
if (data.error) {
  return updateElement('loginError', data.error);
}
```

`register` 関数にも同様の変更を加える。

これで無効な情報が入力されたときにエラーが表示されるようになった。

(スタイルは別途追加)

![error-messages](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/display-error-messages.png?raw=true)

これで視覚的にはエラーメッセージが表示されるようになったが、スクリーンリーダーには何もアナウンスされない。

動的にページに追加されたテキストをアナウンスするには、[ライブリージョン](https://developer.mozilla.org/ja/docs/Web/Accessibility/ARIA/ARIA_Live_Regions)と呼ばれるものを追加する必要がある。

ここでは、アラートと呼ばれるライブリージョンを使用する。

```js
<!-- role alert はスクリーンリーダーに適切な情報を伝えるためのもの -->

<div id="loginError" role="alert"></div>
...
<div id="registerError" role="alert"></div>
```

#### ARIAライブリージョンについて

- ライブリージョンはブラウザ・支援技術が認識出来るように最初から・かつ空で存在する必要がある。
- あくまで**必要な場合のみ**使用する。HTMLタグのセマンティクスで解決できるのならそれが基本。
- `role` で役割を定義したり、`tab-index`でキーボード操作を可能にしたりする。
- 参考
    - [今日から始める負担にならないWAI-ARIA - Qiita](https://qiita.com/k__watanabe/items/70502233e25b3fa9e8c8)
    - [ARIA ライブリージョン - アクセシビリティ | MDN](https://developer.mozilla.org/ja/docs/Web/Accessibility/ARIA/ARIA_Live_Regions)

### ダッシュボードに情報を表示する

ダッシュボードにアカウント情報を表示してみる。

データは以下のような形。

```js
{
  "user": "test",
  "currency": "$",
  "description": "Test account",
  "balance": 75,
  "transactions": [
    { "id": "1", "date": "2020-10-01", "object": "Pocket money", "amount": 50 },
    { "id": "2", "date": "2020-10-03", "object": "Book", "amount": -10 },
    { "id": "3", "date": "2020-10-04", "object": "Sandwich", "amount": -5 }
  ],
}
```

#### 実装

残高を表示するためのプレースホルダーを追加。

```html
<section>
  Balance: <span id="balance"></span><span id="currency"></span>
</section>
```

アカウント情報を表示するためのセクションを追加。

```html
<h2 id="description"></h2>
```

> ✅ アカウントの説明はその下にあるコンテンツのタイトルとして機能するため、意味的には見出しとしてマークアップされる。****[How to structure headings for web accessibility](https://www.nomensa.com/blog/how-structure-headings-web-accessibility)****を読み、見出し構造がどのように重要であるかを詳しく知ろう。（後述）

プレースホルダーを更新するための関数を実装していく。

```js
function updateDashboard() {
  if (!account) {
    return navigate('/login');
  }

  updateElement('description', account.description);
  updateElement('balance', account.balance.toFixed(2));
  updateElement('currency', account.currency);
}
```

- まずアカウントデータがあるか確認する。
- 次に先程作成した `updateElement` でHTMLを更新する。
    - 残高表示をきれいにするため、`toFixed` を使って小数点以下2桁の値を表示する

ダッシュボードがロードされる度に `updateDashboard` を呼び出す必要がある。

既にレッスン1の課題で「ダッシュボード表示時」の定義はしてあるので、そこから呼び出せばいい。

一応教材の実装も見ていく。

`updateRoute` の最後に以下を追加。

```js
if (typeof route.init === 'function') {
  route.init();
}
```

`routes` の定義を更新。

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard', init: updateDashboard }
};
```

`route.init` はわかりやすくて良いので真似する。

```js
/** ダッシュボード表示時の処理*/
function dashboardDisplay(route) {
    if (route.templateId === 'dashboard') {
        // ダッシュボードの更新
        route.init();
        console.log('Dashboard is shown.');
    }
}
```

ログインするとアカウントの残高・通貨・説明が表示されるようになった。

![display-balance](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/login-display-balance.png?raw=true)

***

### 寄り道・見出し構造について

✅ ****[How to structure headings for web accessibility](https://www.nomensa.com/blog/how-structure-headings-web-accessibility)****を読み、見出し構造がどのように重要なのかについて知る

#### 見出し を使う

- 見出しは単に大きなタイトルをつけるだけでなく、**ページの構造を明確にするもの**。アウトラインと考えることが出来る。
- 見出しでコンテンツを分割する。
    - ユーザはページを簡単に読み進める事ができるようになる。
    - アクセシビリティの観点からは、「目次」としての役割を果たす。
- コンテンツの紹介に見出しを使う。見出しは「ラベル」であり、説明ではない。

#### セクションとサブセクション

![sections-and-sub-sections]([https://static.nomensa.com/heading_levels_609a1f4161.png](https://static.nomensa.com/heading_levels_609a1f4161.png))

- `h1` はページの見出し。ページタイトルに相当する。
- `h2` はコンテンツのセクションを作成する。ページを分割し、コンテンツを整理することに役立つ。
- 次の見出しに移った時、それが新しいセクションなら `h2` が適切。
    - 前回の `h2` のサブセクションなら `h3` が適切。
- アクセシビリティの観点から、見出しのレベルを飛ばす(`h1` から `h3` など)は避けるべき。

#### 良い例

![BBC-website]([https://static.nomensa.com/Optimized_bbc_heading_level_outline_8fa1377f4c.png](https://static.nomensa.com/Optimized_bbc_heading_level_outline_8fa1377f4c.png))

BBCのホームページは良い例。

- `h1` が1つだけ使われている。
- ページの様々なセクションは `h2` として定義されている。これによりユーザが簡単に読むべき関連セクションを見つけることが出来る。
- 各トピックの下にある見出しは `h3` として定義されている。

見出し構造を見てみると、以下のようになっている。

```html
<h1> BBC Homepage </h1>

<h2> Headline Topic </h2>
	<h3> News Headline 1 </h3>
	<h3> News Headline 2 </h3>
	<h3> News Headline 3 </h3>

<h2> Headline Topic </h2>
	<h3> News Headline 1 </h3>
	<h3> News Headline 2 </h3>
	<h3> News Headline 3 </h3>
```

![GOV.UL]([https://static.nomensa.com/gov_heading_level_outline_37958fbf63.png](https://static.nomensa.com/gov_heading_level_outline_37958fbf63.png))

こちらも良い例。

- 「Popular on GOV.UK」は視覚的には普通のテキストのように見えるが、実際にはまったく新しいセクションのため、 `h2` を割り当てるのが適切。
- 「Services and Information」という `h2` が隠されて存在する。スクリーンリーダーのユーザーには読み上げられるようになっている。

BBCとGOV.UKのホームページは大きく異なるが、どちらもページ構造を効果的に伝え、支援技術を使うユーザを満足させる強固な見出し構造を持っている。

**その他紹介されていた参考記事**

- [Using HTML headings](https://www.nomensa.com/blog/2010/using-html-headings)
- [How to write good link text](https://www.nomensa.com/blog/2011/accessibility-how-write-good-link-text)
- [How to write good page titles](https://www.nomensa.com/blog/2013/how-to-write-better-page-titles)

***

### templateを使用してテーブルを動的に作成

`template` は小さく作って、ページの繰り返し部分を動的に埋め込むために使用することも出来る。

#### 実装

新しいテンプレートを追加。

```html
<template id="transaction">
	<tr>
		<td></td>
		<td></td>
		<td></td>
	</tr>
</template>
```

このテンプレートは3つのカラム(日付・オブジェクト・取引額)を持つ。

見つけやすいように、`tbody` に `id` を付与しておく。

```js
<tbody id="transactions"></tbody>
```

`createTransactionRow` を実装していく。

```js
function createTransactionRow(transaction) {
  const template = document.getElementById('transaction');
  const transactionRow = template.content.cloneNode(true);
  const tr = transactionRow.querySelector('tr');
  tr.children[0].textContent = transaction.date;
  tr.children[1].textContent = transaction.object;
  tr.children[2].textContent = transaction.amount.toFixed(2);
  return transactionRow;
}
```

この関数は名前の通りの動作をする。

作成したテンプレートを使って新しいテーブルの行を作成( `tr` )、取引データを使ってその内容を埋める。

以下の処理を `updateDashboard` に追加。

```js
const transactionsRows = document.createDocumentFragment();
for (const transaction of account.transactions) {
  const transactionRow = createTransactionRow(transaction);
  transactionsRows.appendChild(transactionRow);
}
updateElement('transactions', transactionsRows);
```

ここでは `documentFragment` を利用し、DOMフラグメント上で作業、HTMLにアタッチしている。

`updateElement` がテキストコンテンツにのみ対応しているので、コードを少し変更する。

```js
function updateElement(id, textOrNode) {
  const element = document.getElementById(id);
  element.textContent = ''; // 一旦子要素を空にする
  element.append(textOrNode);
}
```

**[append](https://developer.mozilla.org/ja/docs/Web/API/Element/append)** を使用している。

`append`は、テキスト・[DOM Nodes](https://developer.mozilla.org/ja/docs/Web/API/Node)のどちらも親要素にアタッチすることが出来る。

##### `append` と `appendChild` の違い

> `Element.append()` は `[DOMString](https://developer.mozilla.org/ja/docs/Web/API/DOMString)` も追加することができますが、`Node.appendChild()` は`[Node](https://developer.mozilla.org/ja/docs/Web/API/Node)` オブジェクトのみを受け付けます。

> `Element.append()` には返値がありませんが、`Node.appendChild()` は追加された`[Node](https://developer.mozilla.org/ja/docs/Web/API/Node)` オブジェクトを返します。

> `Element.append()` は複数のノードや文字列を追加することができますが、`Node.appendChild()` はノードを 1 つだけしか追加することができせん。

## 処理の振り返り

コードがぐちゃぐちゃになってきたので、一旦整理がてら処理の流れを復習します。

#### ルーティング

```js
// ---------------------------------------------------------------------------
// ルーティング
// ---------------------------------------------------------------------------

const routes = {
    '/login': { templateId: 'login' },
    '/dashboard': { templateId: 'dashboard', init: updateDashboard }
};

/** 入力されたURLに従ってナビゲートを行う */
function navigate(path) {
	  // ブラウザの履歴にURLパスを追加
    window.history.pushState({}, path, path);
    updateRoute();
}

/** クリックされたリンクをnavigateに渡す */
function onLinkClick(event) {
    // リンクのデフォルト動作(HTML更新)を防ぐ
    event.preventDefault();
    navigate(event.target.href);
}

/** HTMLテンプレートの表示を更新する */
function updateRoute() {
    const path = window.location.pathname;
    const route = routes[path];
    // 未知のパスが入力された場合ログインページにリダイレクトする
    if (!route) return navigate('/login');

    // templateを取得
    const template = document.getElementById(route.templateId);
    const view = template.content.cloneNode(true);

    // appにHTML追加
    const app = document.getElementById('app');
    app.innerHTML = '';
    // appendChildはノードのみが対象
    app.appendChild(view);

    updateTitle(route);
    // ダッシュボード表示時の処理
    dashboardDisplay(route);
}

/** ページタイトルを更新する */
function updateTitle(route) {
    document.title = route.templateId;
}
```

- `navigate` では、HTMLをリロードせずにURLを更新、閲覧履歴に新しいエントリを作成して `updateRoute` を呼び出す。
- リンクがクリックされた場合は「HTML更新」を防ぎつつ `navigate` にリンクが持っているパスを渡す。
- `updateRoute` では、現在のパスを参照して処理を行う。
    - 未知のパスが入力された場合`navigate` の呼び出し。
    - `template` を取得、`app`にHTMLを挿入する形でページを更新する。
    - タイトル・ダッシュボードの更新も行う。

#### HTMLの更新

```js
/** 指定した要素の子要素にNodeかテキストを追加 */
function updateElement(id, textOrNode) {
    const element = document.getElementById(id);
    element.textContent = ''; // 一旦子要素を空にする
    element.append(textOrNode);
}
```

- 特定の要素に子要素を追加する形で動的にHTMLを更新する。
- `append` を利用することでテキスト/Nodeどちらも対応できる。

#### ユーザデータのサンプル

```js
/**
 * データのサンプル
{
    "user": "test",
    "currency": "$",
    "description": "Test account",
    "balance": 75,
    "transactions": [
        { "id": "1", "date": "2020-10-01", "object": "Pocket money", "amount": 50 },
        { "id": "2", "date": "2020-10-03", "object": "Book", "amount": -10 },
        { "id": "3", "date": "2020-10-04", "object": "Sandwich", "amount": -5 }
    ],
}
 */
```

#### 登録処理

```js
// ---------------------------------------------------------------------------
// 登録
// ---------------------------------------------------------------------------

/** ユーザを登録する */
async function createAccount(account) {
    try {
        // POSTを使ってユーザ情報を送る
        const response = await fetch('//localhost:5000/api/accounts', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: account
    });
        // response.jsonはレスポンスのbodyを解析してオブジェクトを返す
        return await response.json();
    } catch (error) {
        return { error: error.message || 'Unknown error' };
    }
}

/** ユーザ登録の実行 */
async function register() {
    const registerForm = document.getElementById('registerForm');
    // フォームからキー:値のペアを取得
    const formData = new FormData(registerForm);
    // キー:値のリストをオブジェクトに変換 → JSONに変換
    const jsonData = JSON.stringify(Object.fromEntries(formData));

    const result = await createAccount(jsonData);

    // 登録失敗時
    if (result.error) {
        // エラーテキストを表示
        return updateElement("registerError", result.error);
    }

    console.log('Account created!', result);
    account = result;
    navigate('/dashboard');
}
```

- Fetchを使ってユーザ情報を登録。
    - 引数はURLとリクエストの詳細。
    - `response.json`はJSONという名前ではあるが、`response`オブジェクトの`body`を解析、JavaScriptのオブジェクトとして返すメソッド。
    - 非同期処理なので `async/await` を使う。
- `register` から `createAccount` 呼び出し。
    - フォームから[値:キーのペア]取得→オブジェクトに変換→JSONにシリアライズ。
    - `await` を使って処理を待つ。
    - 登録失敗したらエラーテキストを表示。
    - 成功したらグローバル変数 `account` に `result` を代入し、ダッシュボードへリダイレクト。

#### ログイン

```js
// ---------------------------------------------------------------------------
// ログイン
// ---------------------------------------------------------------------------

/** APIを叩いてユーザをGETする */
async function getAccount(user) {
    try {
        // デフォルトでGETを使うのでURLのみで良い
        const response = await fetch('//localhost:5000/api/accounts/' + encodeURIComponent(user));
        // response.jsonはレスポンスのbodyを解析してオブジェクトを返す
        return await response.json();
    } catch (error) {
        return { error: error.message || 'Unknown error' };
    }
}

/** ログインする */
async function login() {
    // フォームへの入力からユーザ情報を取得
    const loginForm = document.getElementById('loginForm')
    const user = loginForm.user.value;
    const data = await getAccount(user);

    // ログイン失敗時
    if (data.error) {
        // エラーテキストを表示
        return updateElement('loginError', data.error);
    }

    account = data;
    navigate('/dashboard');
}
```

- Fetchを使ってユーザ情報を取得。
    - デフォルトでGETを使うため、引数はURLのみで良い。
    - 登録と同じく `response.json` で結果をオブジェクトに変換。
- `login` から `getAccount` の呼び出し。
    - フォームへの入力からユーザの情報を取得。
    - ログインが失敗したらエラーテキストを表示。
    - ログインに成功したらグローバル変数 `account` に `data`を入れてダッシュボードにリダイレクト。

#### ダッシュボード

```js
// ---------------------------------------------------------------------------
// ダッシュボード
// ---------------------------------------------------------------------------

/** ダッシュボード表示時の処理 updateRouteから呼ばれる */
function dashboardDisplay(route) {
    if (route.templateId === 'dashboard') {
        // updateDashboardの呼び出し
        route.init();
        console.log('Dashboard is shown.');
    }
}

/** ダッシュボードを更新する */
function updateDashboard() {
    // アカウントの存在確認
    if (!account) {
        return navigate('/login');
    }
    // 表示の更新
    updateElement('description', account.description);
    updateElement('balance', account.balance.toFixed(2));
    updateElement('currency', account.currency);

    // テーブルに挿入するDocumentFragmentを作成
    const transactionsRows = document.createDocumentFragment();
    for (const transaction of account.transactions) {
    const transactionRow = createTransactionRow(transaction);
    transactionsRows.appendChild(transactionRow);
}
// 作成したDocumentFragmentを挿入
updateElement('transactions', transactionsRows);
}

/** テーブルデータを作成する */
function createTransactionRow(transaction) {
    // テーブルの取得
    const template = document.getElementById('transaction');
    const transactionRow = template.content.cloneNode(true);
    const tr = transactionRow.querySelector('tr');
    // transactionをテーブルに追加
    tr.children[0].textContent = transaction.date;
    tr.children[1].textContent = transaction.object;
    tr.children[2].textContent = transaction.amount.toFixed(2);
    return transactionRow;
}
```

- ルートがダッシュボードなら `dashboardDisplay` が呼ばれる。
- ダッシュボードを更新する。
    - グローバル変数 `account` を使ってアカウントの存在確認。
    - `updateElement` 、 `account` が持つ情報を使ってダッシュボードの表示を更新。
    - `DocumentFragment`を利用してテーブルに挿入するデータを作成。
- テーブルデータを作成する。
    - テンプレートからテーブルを取得。
    - `account.transactions` のデータを元にテーブルの要素を更新。
    - 作成したノードを返す。

#### 初期化・グローバル変数の宣言

```js
// ---------------------------------------------------------------------------
// グローバル変数の宣言
// ---------------------------------------------------------------------------

/** @global アカウント情報 */
let account = null;

// ---------------------------------------------------------------------------
// 初期化
// ---------------------------------------------------------------------------

// popstateイベント発生時updateRouteを呼び出し。
// このイベントは戻る/進むボタンによるページ遷移などで発生する。
window.onpopstate = (event) => {
    updateRoute()
}
updateRoute()
```

- `account` はグローバル変数なので `@global` を書いておいた。
    - 書き方が合ってるのかは謎。VSCodeだと補完が表示されて、コレなんだっけ？とはならないようになったのでOKとする。
- `popstate` イベント(戻る/進むボタン)発生時に`updateRoute` を呼び出すようにする。
- `updateRote` を呼んでおくことで、ページにアクセスした時に `/login` にリダイレクトするようにする。

## データの取得と利用　続き

### 課題 コードのリファクタとコメント

狙ったわけではないのですが、課題の直前に似たようなことをやってしまいました。

とはいえ、課題の内容によると、まだ以下のようなことが出来ます。

- URL等の定数を抽出
- コードの共通部分をなくす
- その他色々見直す

#### 定数の抽出

複数回呼び出される値は変数に入れておくべきですね。

```js
/** @global ベースURL */
const serverURL = '//localhost:5000/api'
```

#### `**create` と `get` を因数分解**

元々のコード

```js
/** ユーザを登録する */
async function createAccount(account) {
    try {
        // POSTを使ってユーザ情報を送る
        const response = await fetch( serverUrl + '/accounts/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: account
    });
        // response.jsonはレスポンスのbodyを解析してオブジェクトを返す
        return await response.json();
    } catch (error) {
        return { error: error.message || 'Unknown error' };
    }
}

/** APIを叩いてユーザをGETする */
async function getAccount(user) {
    try {
        // デフォルトでGETを使うのでURLのみで良い
        const response = await fetch( serverUrl + "/accounts/" + encodeURIComponent(user));
        // response.jsonはレスポンスのbodyを解析してオブジェクトを返す
        return await response.json();
    } catch (error) {
        return { error: error.message || 'Unknown error' };
    }
}
```

`create`と`get`では、`response` の設定周りが異なりますね。

- create
    - POST
    - headers有り
    - body有り
- get
    - GET

`headers` `body` はPOSTの時に必要な値。

`headers` で利用する値は定数、`body` は変数なので、
`body` がある場合 `headers` をセットする感じで良さそう。

また、`fetch`自体のデフォルトは`GET`なので、デフォルト引数に`GET`を登録しておけば良さそう。

あとはURLを引数として受け取る形で。

```js
async function sendRequest(url, body, method="GET") {
    try {
        const response = await fetch( serverUrl + url, {
            method: method,
            headers: body? { 'Content-Type': 'application/json' } : undefined,
            body: body
        })
        return await response.json();
    } catch (error) {
        return { error: error.message || "Unknown error"};
    }
}
```

`severUrl` + `url` ってわかりにくいな・・・

良い変数名はないでしょうか。 `solution`(模範解答的なコード) を見てみます。

```js:solution/app.js
async function sendRequest(api, method, body) {
  try {
    const response = await fetch(serverUrl + api, {
      method: method || 'GET',
      headers: body ? { 'Content-Type': 'application/json' } : undefined,
      body
    });
    return await response.json();
  } catch (error) {
    return { error: error.message || 'Unknown error' };
  }
}
```

なるほど、`api` か・・・

概ね同じですが、 `method` の渡し方が少し違いますね。

**リファクタリング前**

```js
/** ユーザを登録する */
async function createAccount(account) {
    try {
        // POSTを使ってユーザ情報を送る
        const response = await fetch( serverUrl + '/accounts/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: account
    });
        // response.jsonはレスポンスのbodyを解析してオブジェクトを返す
        return await response.json();
    } catch (error) {
        return { error: error.message || 'Unknown error' };
    }
}

/** APIを叩いてユーザをGETする */
async function getAccount(user) {
    try {
        // デフォルトでGETを使うのでURLのみで良い
        const response = await fetch( serverUrl + "/accounts/" + encodeURIComponent(user));
        // response.jsonはレスポンスのbodyを解析してオブジェクトを返す
        return await response.json();
    } catch (error) {
        return { error: error.message || 'Unknown error' };
    }
}
```

**リファクタリング後**

```js
/** サーバAPIにリクエストを送る */
async function sendRequest(api, body, method="GET") {
    try {
        const response = await fetch( serverUrl + api, {
            method: method,
            headers: body? { 'Content-Type': 'application/json' } : undefined,
            body: body
        })
        return await response.json();
    } catch (error) {
        return { error: error.message || "Unknown error"};
    }
}

/** GET アカウント情報*/
async function getAccount(user) {
    // 引数はURLのみ
    return sendRequest('/accounts/' + encodeURIComponent(user));
}

/** POST アカウント情報 */
async function createAccount(account) {
    return sendRequest('/accounts', account, "POST");
}
```

かなりスッキリしました。

#### タイトルの更新

`solution`をチラ見してみると、 `title` の更新部分の処理で `routes` のプロパティを利用していました。

```js
const routes = {
    '/login': { templateId: 'login', title: "Login" },
    '/dashboard': { templateId: 'dashboard', title: "Account info", init: updateDashboard }
};
...
// タイトルの更新
document.title = route.title;
```

確かにこちらの方がわかりやすいし、わざわざ関数を使うまでもないですね。

### 副教材

- [メディアクエリー](https://developer.mozilla.org/ja/docs/Web/CSS/Media_queries)
    - [メディアクエリー　ガイド](https://developer.mozilla.org/ja/docs/Web/CSS/Media_queries#%E3%82%AC%E3%82%A4%E3%83%89)
    - レスポンシブデザインにするために使われるようです。

***

## 状態管理の概念

### イントロ

Webアプリの規模が大きくなるにつれて、当然ながらすべてのデータの流れを追うことは難しくなる。

どこでデータを取得し、どのページがデータを消費し、どこでいつ更新する必要があるのか・・・

メンテナンスが難しい厄介なコードになりがち。

これは、アプリの異なるページ感でデータを共有する必要がある場合(ユーザデータなど)に特に当てはまる。

このパートでは、**状態の管理方法**を再考するために構築したアプリを見ていく。**任意の時点でのブラウザの更新**をサポートし、**ユーザセッション間でのデータの永続化**を可能にする。

### 状態管理を再考する

現在は、ログインしているユーザの銀行データを含むグローバル変数 `account` を使ってアプリの状態を管理している。

現状、以下の問題がある。

- ブラウザをリフレッシュするとログインに戻るため、**状態は保持されない**。
- **状態を変更する関数が複数**ある。アプリが大きくなるにつれて、変更の追跡が難しくなり、更新を忘れがちになる。
- **状態がリセットされない。**Logoutをクリックしてもログインページになってもアカウントデータが残っている。

ここでの問題の本質は、**データの流れがわかりにくい**こと。

- データフローをわかりやすく保つには？
- データフローを理解しやすい状態に保つには？

これらの問題が解決した時、他の問題は既に解決されているか、簡単に解決できるようになっている。

ここでは、**データとそれを変更する方法**を集中化することで構成される、一般的な解決策を採用する。

![state-management]([https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/7-bank-project/4-state-management/images/data-flow.png](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/7-bank-project/4-state-management/images/data-flow.png))

> https://raw.githubusercontent.com/microsoft/Web-Dev-For-Beginners/main/7-bank-project/4-state-management/images より

SAMパターン、Reduxについて調べてみる。

**SAMパターン**

![SAM](https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/SAM.jpeg?raw=true)

> 構成要素
> Model
> Actionから受け取った計算結果をpresent関数でStoreに送り、現在の状態を更新する。
> 状態が変化することでViewが更新される。
> 現在の状態を保持する(FluxのStore)。
> 永続化の責務も持つ。

> Action
> データを受け取り、そのデータをもとに状態計算をする関数。
> 計算結果は、present関数を介してModelへ送りこまれる。
> ActionはView(ユーザー操作)とState(NAP ※後述)から発火される。

> State
> Modelから受け取ったデータを元にViewで必要となるデータに変換を行う関数。
> モデルの全てがViewに影響する訳ではなく、またViewの形がモデルと一致する訳でもないので、Stateを介して見通しを整える。
> 現在のModelの状態を見て、次に発火する必要のあるActionを呼び出す。これをNAP（Next-Action-Predicate）という。（ex. Modelが持つtimeが0になった時、Modelの状態を見て自動的にTimeUp!と表示する）

参考

- [SAMパターンの大雑把な理解](https://izumisy.work/entry/2017/10/14/184229)
- [【SAM】ゲーマー諸君、コントローラを棄ててアクションを起こせ！MVCのCが消えて、Actionが残った理由 - ゲーム脳でもわかるMVC 本論](https://qiita.com/sasanquaneuf/items/2926555c9f4e7230b84f)
- [Flux, Redux, SAMのデータフローをざっくり理解する](https://qiita.com/aimy-07/items/e252ff3be2f4e7fdc9f5)

**Redux**

状態管理へのアプローチを持つライブラリは多くあるが、[Redux](https://redux.js.org/)は人気の選択肢の一つ。

- Reactが扱うUIの状態を管理するためのフレームワーク。
- 3原則を持つ。
    1. **Single source of truth**アプリケーション内でStoreは1つだけ。
    2. **State is read-only**stateを直接変更することはできない。Actionをstoreへdispatch(送信)することでしかstateは変更できない。
    3. **Mutations are written as pure functions**Reducer(stateを変更する関数)は純粋関数(同じ入力値を渡すたび、決まって同じ出力値が得られる関数)でなければならない。

#### 実装

 `account` 宣言を `state` に置き換える。

```js
let account = null;
```

```js
let state = {
  account: null
};
```

これにより、1つの `state` オブジェクトに全てのデータの状態を集中させることになる。

### データ変更の追跡

データ保存のために `state` オブジェクトを配置したので、次のステップは**更新を一元化**すること。
目的は、「いつ変更があったのか」、「いつ変更が発生したのか」簡単に把握できるようになること。

ここでは、 `state` オブジェクトを不変にする。

これはまた、何かを変更したい場合には新しい `state` を作成する必要があることを意味する。

このようにすることで、望ましくない副作用への保護、デバッグを容易にする、などのメリットを得ることが出来る。

JavaScriptでは、[Object.freeze](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) を使って不変オブジェクトを作ることが出来る。

#### 浅い凍結

[浅い凍結とは - MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze#what_is_shallow_freeze)

`Object.freeze(object)` を呼び出した結果は`object`の直属のプロパティにのみ適用される。

```js
const employee = {
  name: "Mayank",
  designation: "Developer",
  address: {
    street: "Rohini",
    city: "Delhi"
  }
};

Object.freeze(employee);

employee.name = "Dummy"; // 非 strict モードでは暗黙に失敗
employee.address.city = "Noida"; // 子オブジェクトの属性は変更できる

console.log(employee.address.city) // 出力: "Noida"
```

オブジェクトを真に不変にするには、オブジェクト型のプロパティを**再帰的に凍結(深い凍結)させる**必要がある。

凍結させてはいけない `window` のようなオブジェクトを凍結させる危険性があることに注意。

#### 実装

```js
function updateState(property, newData) {
  state = Object.freeze({
    ...state,
    [property]: newData
  });
}
```

この関数では、新しい `state` オブジェクトを作成し、`...`を使用して前のステートからデータをコピーしている。

次に、`[property]`を使用して `state` の特定のプロパティを新しいデータでオーバーライドする。

最後に、`Object.freeze`を使用してオブジェクトをロック、変更を防ぐ。

また、 `state` の初期化を更新、初期状態も凍結されるようにする。

```js
let state = Object.freeze({
  account: null
});
```

それに伴い `login` `register` を更新。

```js
// register
updateState('account', result);

// login
updateState('account', data);
```

新しい関数 `logout` を作成し、ユーザがLogoutをクリックした時にアカウントデータがクリアされない問題を修正する。

```js
function logout() {
  updateState('account', null);
  navigate('/login');
}
```

##### [スプレッド構文](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals)

> スプレッド構文は、オブジェクトや配列のすべての要素を何らかのリストに入れる必要がある場合に使用することができます。

```js
> state
{ key: 'v', key2: 'v2', key3: 'v3' }

# オブジェクトに展開
> state = {...state, "key4": "v4"}
{ key: 'v', key2: 'v2', key3: 'v3', key4: 'v4' }
```

##### ブラケット表記

[オブジェクトでの作業 - MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Working_with_Objects#objects_and_properties)

```js
//ブラケット記法
const obj = new Object();
const propertyName = "01" ;
obj[propertyName] = "テスト"; 
console.log(obj);  // Object { 01="テスト"}

//ドット記法
const obj = new Object();
obj.01 = "テスト";       //SyntaxError
console.log(obj.0123);　 //SyntaxError
```

> JavaScript 識別子として有効ではないプロパティ名 (例えば空白やダッシュを含んでいたり、数字で始まったりするプロパティ名) には、ブラケット (角括弧) 表記法でのみアクセスできます。この表記法はプロパティ名を動的に決める場合 (プロパティ名が実行時に決まる場合) に便利です。

**プロパティ名に変数を使いたい**場合、動的にプロパティ名を変更してアクセスしたい場合などにブラケット記法が有効。

### 状態を維持する

ほとんどのWebアプリでは、データを保持しておかないと正常に動作しない。

すべての重要なデータは通常、**DBに保存**され、サーバーAPIをを介してアクセスされる。

しかし、より良いUXやパフォーマンス向上のため、ブラウザ上で実行されている**クライアントアプリのデータを永続化する**ことも選択肢に上がる。

ブラウザにデータを永続化する場合、いくつか重要な点がある。

- **データは機密性の高いものか？** ユーザパスワードなどの機密性の高いデータをクライアントに保存することは避けるべき。
- **データをどのくらい保存する必要がある？** このデータにアクセスするのは現在のセッションのためだけ？それとも永遠に保存する？

Webアプリ内のデータを保存する方法は目的に応じて複数ある。

例えば、URLを使用して検索クエリを保存し、ユーザー間で共有できるようにすることが出来る。

また、**認証情報**のように、データをサーバーと共有する必要がある場合は、**HTTPクッキー**を使用することも出来る。

もう一つの選択肢は、データを保存するためのブラウザAPIを利用すること。

- **[localStorage](https://developer.mozilla.org/ja/docs/Web/API/Window/localStorage)** : **異なるセッション**にまたがって現在のWebサイトに固有のデータを永続化することが出来る。[Key-Valueストア](https://e-words.jp/w/KVS.html)。
- **[sessionStorage](https://developer.mozilla.org/ja/docs/Web/API/Window/sessionStorage)** : 保存されたデータは**セッションの終了時**(ブラウザが閉じられた時)に消去される。

これらのAPIはどちらも**文字列しか**保存できない。

複雑なオブジェクトを格納したい場合、 `JSON.stringify` を使って `JSON` 形式にシリアライズする必要がある。

✅ サーバーで動作しないWebアプリを作成したい場合、 `IndexedDB` API を使ってクライアント上にDBを作成することも可能。

#### 実装

ユーザが明示的にLogoutボタンをクリックするまではログインしたままにしたい。
そのため、`localStorage`を使ってアカウントデータを保存する。

まず、データを保存するためのキーを定義する。

```js
const storageKey = "savedAccount";
```

そして、 `updateState` に以下を追加。

```js
localStorage.setItem(storageKey, JSON.stringify(state.account));
```

`state`によりすべての状態の更新を一元化していたため、ユーザーアカウントのデータは永続化され、常に最新の状態になる。

データを保存したので、アプリが読み込まれた時に復元されるようにする。

```js
function init() {
  const savedAccount = localStorage.getItem(storageKey);
  if (savedAccount) {
    updateState('account', JSON.parse(savedAccount));
  }

  // 今までの初期化コード
  window.onpopstate = () => updateRoute();
  updateRoute();
}

init();
```

保存されたデータを取得、もしあればそれに応じて状態を更新する。

ページの更新時に状態に依存するコードがあるかもしれないので、ルートを更新する前にこの処理を行うことが重要。

アカウントデータを保持しているため、**ダッシュボードページをアプリケーションのデフォルトページに**することも出来る。

具体的には、`updateRoute`を以下のように変更する。

```js
/** HTMLテンプレートの表示を更新する */
function updateRoute() {
    const path = window.location.pathname;
    const route = routes[path];
    // 変更箇所
    if (!route) return navigate('/dashboard');
```

もしもデータが見つからなければ、ダッシュボード → ログインページにリダイレクトするようになっているため問題ない。

### データの更新

`test` アカウントを使ってダッシュボードに行き、ターミナルで以下のコマンドを実行して新しいトランザクションを作成する。

```jsx
curl --request POST \
     --header "Content-Type: application/json" \
     --data "{ \"date\": \"2020-07-24\", \"object\": \"Bought book\", \"amount\": -20 }" \
     http://localhost:5000/api/accounts/test/transactions
```

この状態でダッシュボードのページを更新してみても、新しいトランザクションは表示されない。この状態は`localStorage`により無期限に保持されるが、ログアウトして再ログインするまで更新されない。

この問題を修正するために考えられる戦略の1つは、ダッシュボードがロードされる度にアカウントデータをリロードすること。

#### 実装

`updateAccountData` を作成する。

```jsx
async function updateAccountData() {
  const account = state.account;
  if (!account) {
    return logout();
  }

  const data = await getAccount(account.user);
  if (data.error) {
    return logout();
  }

  updateState('account', data);
}
```

現在ログインしているかをチェックし、サーバからアカウントデータをリロードする。

`refresh` を作成する。
アカウントデータを更新し、ダッシュボードページのHTMLを更新する処理を行う。

```jsx
async function refresh() {
  await updateAccountData();
  updateDashboard();
}
```

最後に、ルート定義を更新する。

```jsx
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard', init: refresh }
};
```

これで、ダッシュボードをリロードすると更新されたアカウントデータが表示される。

### 課題 「トランザクションの追加」ダイアログの実装

> - ダッシュボードページに「トランザクションの追加」ボタンを追加します
> - HTML テンプレートで新しいページを作成するか、JavaScript を使用してダッシュボード・ページを離れることなくダイアログの HTML を表示/非表示にするかのいずれかを選択します (そのためには `[hidden](https://developer.mozilla.org/ja/docs/Web/HTML/Global_attributes/hidden)` プロパティを使用するか、CSS クラスを使用することができます)
> - ダイアログの[キーボードとスクリーンリーダーのアクセシビリティ](https://developer.paciellogroup.com/blog/2018/06/the-current-state-of-modal-dialog-accessibility/) が適切であることを確認します
> - 入力データを受け取るための HTML フォームを実装します
> - フォームデータから JSON データを作成して API に送ります
> - ダッシュボードページを新しいデータで更新します

#### トランザクションの追加ボタン

```html
<button>Add Transaction</button>
```

#### ダイアログのHTML実装

[HTMLElement.hidden - MDN](https://developer.mozilla.org/ja/docs/Web/API/HTMLElement/hidden)

`true` のときに要素はビューから隠される。`false` のときは要素が見える。

表示/非表示を考える前に、まずフォームを実装する。

```html
<section id="transactionDialog" class="dialog">
    <div class="dialog-content">
        <h2 class="text-center">Add transaction</h2>
        <form id="transactionForm">
        <label for="date">Date</label> 
        <input id="date" name="date" type="date" required>
        <label for="object">Object</label> 
        <input id="object" name="object" type="text" maxlength="50" required>
        <label for="amount">Amount (use negative value for debit)</label> 
        <input id="amount" name="amount" type="number" value="0" step="any" required>
        <div id="transactionError" class="error" role="alert"></div>
        <div class="dialog-buttons">
            <button>Cancel</button>
            <button>OK</button>
        </div>
        </form>
    </div>
</section>
```

ひとまず `template` の中に配置。

CSSを実装する・・・

が、何をしていいかわからないので `solution` を参照。

```css
.dialog {
    display: none;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    left: 0;
    top: 0;
    overflow: auto;
    background-color: rgba(0,0,0,0.4);
    animation: slideFromTop 0.3s ease-in-out;
    justify-content: center;
    align-items: flex-start;
}

@keyframes slideFromTop {
from {
    top: -300px;
    opacity: 0;
}
to {
    top: 0;
    opacity: 1;
}
}
```

- `display: none` 非表示に
- `position` ~ `top` 位置の調整
- `overflow: auto;` [overflow - MDN](https://developer.mozilla.org/ja/docs/Web/CSS/overflow)　要素のオーバーフロー時、すなわち要素の内容が多すぎる時の動作。
    - `auto` はあふれる場合スクロールバーを表示
- `animation` 、`@keyframes`によりアニメーション実装
#### JavaScript実装

```jsx
function addTransaction() {
    const dialog = document.getElementById('transactionDialog');
    dialog.classList.add('show');

    // リセット
    const transactionForm = document.getElementById('transactionForm');
    transactionForm.reset();

    // 日付のセット
    transactionForm.date.valueAsDate = new Date();
}
```

```css
.dialog.show {
    display: flex;
}
```

[Element.classList - MDN](https://developer.mozilla.org/ja/docs/Web/API/Element/classList)

[HTMLFormElement.reset - MDN](https://developer.mozilla.org/ja/docs/Web/API/HTMLFormElement/reset)

- `dialog` に `show` クラスを加えることで表示。
- `reset` によりフォーム要素をリセット

```jsx
/** POST トランザクション */
async function createTransaction(user, transaction) {
    return sendRequest('/accounts/' + user + '/transactions', 'POST', transaction);
}
```

- `/accounts/user/transactions` に POST。
- [銀行API](https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/7-bank-project/api)を参照。

| POST /api/accounts/:user/transactionsAdd a transaction | ex: { date: '2020-07-23T18:25:43.511Z', object: 'Bought a book', amount: -20 } |
| --- | --- |

```jsx
async function confirmTransaction() {
    const dialog = document.getElementById('transactionDialog');
    dialog.classList.remove('show');

    const transactionForm = document.getElementById('transactionForm');

    const formData = new FormData(transactionForm);
    const jsonData = JSON.stringify(Object.fromEntries(formData));
    const data = await createTransaction(state.account.user, jsonData);

    if (data.error) {
        return updateElement('transactionError', data.error);
    }

    // ローカルの状態 更新
    const updateAccount = {
        ...state.account,
        balance: state.account.balance + data.amount,
        transactions: [...state.account.transactions, data]
    }
    updateState('account', updateAccount);

    // 表示の更新
    updateDashboard();
}
```

- `show` クラスを除去して非表示に。
- フォームデータ取り出し→オブジェクトに変換→JSONでにシリアライズ
- `createTransaction` を呼び出し、データをPOST
- 状態・表示の更新

```jsx
async function cancelTransaction() {
    const dialog = document.getElementById('transactionDialog');
    dialog.classList.remove('show');
}
```

- キャンセルされた場合`show`を除去して非表示に

```jsx
<button type="button" class="button-alt" onclick="cancelTransaction()" formnovalidate>Cancel</button>
<button onclick="confirmTransaction()">OK</button>
```

- `require` が設定された状態でもキャンセル出来るように、 `formnonvalidate` を使用。
    - [MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/form#:~:text=%E3%81%8C%E5%8F%AF%E8%83%BD%E3%81%A7%E3%81%99%E3%80%82-,novalidate,-%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%82%92%E9%80%81%E4%BF%A1)

## 学んだこと

* データの取得
* データを利用して表示を更新する
*  データの永続化
*  **データとそれを変更する方法**を統一、集中化することでワークフローがわかりやすくなる
*  ページを表示する前にユーザデータの存在を確認することで、ユーザに合わせて表示することが出来る

## 教材全体を通して

- 楽しかった。
- どのようなアプローチで実装していけば良いのか、概要くらいはつかめた。
- 解説があっさりしている箇所が多く、曖昧な点を自分で調査することが多かった → ドキュメント読みの練習になった。
- ❎ 途中から完走することが目的になっていた
    - 学ぶためというより、完走するためにとにかく進める形になっていた。
    - 記事もまとめというより、やったことの羅列になってしまっている。
- ✅ 今後
    - 教材の完走にこだわらず、合わないと思ったら辞めても良い。
      - この教材自体はやった価値があったと思う。
    - 記事の粒度や内容をもう少し考える。重要だと思った点をまとめる、実装の解説/考え方の解説に重点を置く、など。
    - HTML/CSSについてはまだまだ0から書ける気がしないので、色々作ってみる。