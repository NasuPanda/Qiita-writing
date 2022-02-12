<!--
title:   MicrosoftのWeb開発教材を使ってみた ④タイピングゲーム 【JavaScriptのイベント処理】
tags:    JavaScript,初心者,初心者向け
id:      340f391ee9f167bf4333
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
**④タイピングゲーム 【JavaScriptのイベント処理】　本記事**
[⑤-1ブラウザ拡張機能 【ブラウザの仕組み/拡張機能作成の導入】](2022-02-10_Web_d0189565d039c2c11383.md)
⑤-2ブラウザ拡張機能 【API/LocalStorage/BackGround/Performance】
⑥スペースシューティングゲーム【JavaScriptによるゲーム開発の基礎】
⑦架空銀行プロジェクト【ログイン/データ管理/状態管理】

***

### 記事の目的

- 学習のアウトプット
- 教材を使ってみたところかなり良かったので、その紹介

### 注意点

自身の学習のアウトプットがメインなので、理解できているところ(多言語と共通の箇所など)は省いています。
また、課題やtipsについても結構省きます。
この教材に興味を持った方はぜひご自分で取り組んでみてください。

# 4-Typing-Game

https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/4-typing-game

> JavaScript、HTML、CSS のスキルを使ってタイピングゲームを作っていただきます。このゲームでは、プレイヤーにランダムな引用文 (シャーロック・ホームズの名言を使用しています) を提示し、それを正確に入力するのにどれくらいの時間がかかるかを競います。

![typing-demo](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/4-typing-game/images/demo.gif)
> https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/4-typing-game より

### 学習の目的

* キーボードイベントを使用してJavaScript アプリのロジックを駆動する方法を学ぶ。
* イベント駆動型のプログラミングについて学ぶ。

### イベント駆動型プログラミングについて

ブラウザベースのアプリケーションを作成する時、開発者はGUIを提供することでユーザがブラウザと**対話**出来るようにする。対話する方法として最も一般的なのは「ボタンをクリック」「テキストを入力」など。

開発者にとっての問題は、それがいつ起こるかわからないこと。イベントは通常の**Procedural Programming : 手続き型プログラミング**と異なり、**イベント**（=何かが起こる）が発生することはわかっているが、それがいつかはわからない。

このようにイベントの発生を待ち、イベントの発生に対応してコードを実行するような実装を **Event-driven Programming : イベント駆動型プログラミング** と呼ぶ。

- イベントを処理するための最も代表的な手法は **`addEventListener` + 無名関数**の利用。
    - **イベントリスナー** イベントの発生を待ち、発生すれば登録された関数を実行する
    - イベントリスナーを作成する方法として、`addEventLister`や`click`プロパティの設定などがある。
- イベントの代表例
    - click
    - contextmenu 右クリックメニュー
    - select ユーザがテキストをハイライト
    - input
    - keydown

### タイピングゲームの流れ

ここからタイピングゲームの実装に入っていきます。
まずは必要な機能の確認。

- スタートボタンを**押したら**ゲーム開始
- 名言の配列を事前に用意しておき、その中からワードを**ランダムに**選んで表示
- 表示されたワード(空白区切りの英文)をタイプしていく
    - 次にタイプすべき単語は**ハイライト**される
- インプットが始まったら入力されているワードを**監視し**、
    - 現在入力されているワードが**正しければそのまま**
    - **間違っていれば**入力エリアを**赤くハイライト**
- 入力文字が**正しく**、ワードのインデックスが**最後まで到達**→終了
    - 経過時間を表示
- 入力文字が**正しく**、**空白で終わる**(単語の区切り)なら次の単語へ移動

####  +α 自分で実装した機能

- 終了時入力エリア無効化
- モーダルダイアログ実装
- 色を好みに合わせていじる

### 実装

#### HTMLの実装

```html
<html>
<head>
  <title>タイピングゲーム</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>タイピングゲーム!</h1>
  <p>シャーロック・ホームズの名言を使ってタイピングの練習をしましょう。**スタート** をクリックしてください。</p>
  <p id="quote"></p> <!-- これで名言が表示されます。 -->
  <p id="message"></p> <!-- これは、すべてのステータスメッセージを表示します。 -->
  <div>
    <input type="text" aria-label="current word" id="typed-value" /> <!-- 入力用のテキストボックス -->
    <button type="button" id="start">スタート</button> <!-- ゲームを開始します -->
  </div>
  <script src="script.js"></script>
</body>
</html>
```

#### [Live Sever](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)の利用

> Visual Studio Code には Live Server と呼ばれる素晴らしい拡張機能があり、アプリケーションをローカルにホストし、保存するたびにブラウザを更新します。

> * リンクを辿り、Install をクリックして、Live Server をインストールします
    * ブラウザで Visual Studio Code を開き、Visual Studioコードでインストールを実行するように促されます
    * プロンプトが表示されたら Visual Studio Code を再起動します
* インストールしたら、Visual Studio Code で Ctl-Shift-P (または Cmd-Shift-P) をクリックして、コマンドパレットを開きます
* Live Server: Open with Live Server と入力します
    * Live Server がアプリケーションのホスティングを開始します
* ブラウザを開き、https://localhost:5500 に移動します
* これで作成したページが表示されるはずです!

> [https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/4-typing-game　より](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/4-typing-game/typing-game/translations/README.ja.md#%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E8%B5%B7%E5%8B%95)

#### 定数の追加

```js
// すべての名言
const quotes = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
];
// 単語のリストと、プレイヤーが現在入力している単語のインデックスを格納します。
let words = [];
let wordIndex = 0;
// 開始時刻
let startTime = Date.now();
// ページ構成要素
const quoteElement = document.getElementById('quote');
const messageElement = document.getElementById('message');
const typedValueElement = document.getElementById('typed-value');
```

#### スタートボタンを押したら開始

`getElementByID` で要素を参照、イベントを追加

```js
const startElement = document.getElementById("start")
startElement.addEventListener('click', () => {}
```

#### ランダムに選ぶ

`Math.random()`を使う。

```js
const quoteIndex = Math.floor(Math.random() * quotes.length);
const quote = quotes[quoteIndex];
// 名言を空白区切りでワードの配列に入れる
words = quote.split(' ');
// トラッキング用の単語インデックスをリセットする
wordIndex = 0;
```

#### HTMLにワードを表示&ハイライト

* `innerHTML`を更新することでHTMLに文字列を表示することが出来る。
* CSSに`highlight`というclassへの装飾を用意しておき、対象の要素に`highlight`クラスを追加することでハイライトする。

```js
const spanWords = words.map(function(word) {
	return `<span>${word}</span>`
})
quoteElement.innerHTML = spanWords.join(''); // 配列を一つの文字列に
// 事前にCSSで"highlight"を定義しておき、childNodesの最初の要素をハイライト
quoteElement.childNodes[0].className = "highlight";
```

#### 入力中のワード制御&時間の表示

- 単語が空白で区切られることを利用してハイライトを移動
- `startsWith` で現在までの入力が正しいか判定
    - 間違っていれば `error` クラスを追加する
- `wordIndex` により現在のワードを追跡する
- `.trim()`は空白を削除する

```js
typedValueElement.addEventListener('input', () => {
    // 現在のワード取得
    const currentWord = words[wordIndex];
    // 入力されたワード取得
    const typedValue = typedValueElement.value;
    // 入力終了
    if (typedValue === currentWord && wordIndex === words.length - 1) {
        const elapsedTime = new Date().getTime() - startTime;
        const message = `CONGRATULATIONS! You finished in ${elapsedTime / 1000} seconds.`;
        messageElement.innerText = message;
    }
    // 1ワードの終わり
    else if (typedValue.endsWith(' ') && typedValue.trim() === currentWord) {
        typedValueElement.value = '';
          // インデックスをインクリメントし次のワードへ
        wordIndex++;
          // highlightのリセット
        for (const wordElement of quoteElement.childNodes) {
            wordElement.className = '';
        }
          // 次のワードをハイライト
        quoteElement.childNodes[wordIndex].className = 'highlight';
    }
    // 入力が正しい
    else if (currentWord.startsWith(typedValue)) {
        typedValueElement.className = '';
    }
    // 入力ミス 
    else {
        typedValueElement.className = 'error';
    }
});
```

#### 入力エリアの無効化

- `disabled` をtrueにするだけ。
- リセット時にfalseに戻す。

```js
// 入力の無効化
typedValueElement.disabled = true;
```

#### モーダルダイアログの実装

モーダルダイアログとは、それが出ている間他の画面操作をブロックするタイプのウィンドウ。

1. メッセージの親として `div` を追加し、 `modal`クラスを設定しておく
1. `modal` の `display` をNoneにしておく
1. 表示したいタイミングになったら`display`を`block` `flex` 等に変更する
1. `exit`ボタンのイベントに `display: none` にする関数を登録しておく

- `getElementByClassName`
    - IDと違いクラス名の場合は配列で返ってくる

```jsx
// モーダルウィンドウの表示
modalWindowElement.style.display = "flex";
document.getElementById("modal-button").addEventListener("click", () => {
    modalWindowElement.style.display = "none";
})
```

`html
<!-- モーダルウィンドウ -->
<div class="modal">
    <div id="modal-content">
        <p id="message"></p> <!--ここにメッセージ-->
    </div>
    <button id="modal-button">exit!</button>
</div>


```css
/* モーダルウィンドウ */
.modal {
    display: none;
		・
		・
    }
```

### 色を好きにいじる

```css
body {
    background-color: black;
    color: green;
}

.start-text {
    font-weight: bold;
    background-color: aquamarine;
}
.highlight {
    background-color: aquamarine;
}
```

### 最終的なコード

```jsx
const quotes = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
    "Clever is a talent. Kindness is a choice."
];

let words = [];
let wordIndex = 0;

let startTime = 0;

const startElement = document.getElementById("start")
const quoteElement = document.getElementById("quote")
const messageElement = document.getElementById('message')
const typedValueElement = document.getElementById("typed-value")
const modalWindowElement = document.getElementsByClassName("modal")[0];

// スタートを押したら
// 引用文からワードを一つ選びHTMLに挿入する形で表示する
startElement.addEventListener('click', () => {
    const quoteIndex = Math.floor(Math.random() * quotes.length);
    const quote = quotes[quoteIndex];

    // 文字列を空白で区切って配列に
    words = quote.split(' ');

    // リセット
    wordIndex = 0;
    typedValueElement.disabled = false;
    startElement.innerText = "Start!"

    // UIを更新する
    const spanWords = words.map(function(word) { return `<span>${word}</span>`})
    quoteElement.innerHTML = spanWords.join(''); // 配列を一つの文字列に
    quoteElement.childNodes[0].className = "highlight"; // childNodesの最初の要素をハイライト

    messageElement.innerText = '';
    typedValueElement.value = '';
    typedValueElement.focus();

    startTime = new Date().getTime();
})

// インプットが始まったら
// 入力しているワードを監視し、
//     入力文字が正しく、文字のインデックスが最後まで到達すれば経過時間を表示
//     入力文字が正しく、空白で終わる(単語の区切り)なら次の単語へ移動
//     現在入力しているワードが正しければそのまま
//     間違っていれば赤くハイライト
typedValueElement.addEventListener("input", () => {
    const currentWord = words[wordIndex];
    const typedValue = typedValueElement.value;

    if (typedValue === currentWord && wordIndex===words.length -1){
        const elapsedTime = new Date().getTime() - startTime;
		const message = `CONGRATULATIONS! You finished in ${elapsedTime / 1000} seconds.`;
        messageElement.innerText = message;
        startElement.innerText = "restart!"
        // 入力の無効化
        typedValueElement.disabled = true;
        // モーダルウィンドウの表示
        modalWindowElement.style.display = "flex";
        document.getElementById("modal-button").addEventListener("click", () => {
            modalWindowElement.style.display = "none";
        })
    }
    else if (typedValue.endsWith(' ') && typedValue.trim() === currentWord) {
        typedValueElement.value = '';
        wordIndex++;
        for (const wordElement of quoteElement.childNodes) {
            wordElement.className = "";
        }
        quoteElement.childNodes[wordIndex].className = "highlight";
    }
    else if (currentWord.startsWith(typedValue)) {
        typedValueElement.className = "";
    }
    else {
        typedValueElement.className = "error";
    }
});
```

もともとの完成イメージ

![typing-demo](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/4-typing-game/images/demo.gif)
> https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/4-typing-game より

出来たもの

![typing-game.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/bcd69d51-4089-f4c8-8f0a-b1e3af4579e4.gif)

### 課題 キーボードゲームの作成

キーボードのイベントを使って何かを実行するゲームを作ってみる。

- キー入力で愛犬が走るゲーム()を作りました。
- `keydown` イベントを利用。
    - 純粋に入力したKeyを取得できる。
    - 矢印キーなら `AllowLeft` のように使う。
    - 参考 : [keydown - MDN](https://developer.mozilla.org/ja/docs/Web/API/Document/keydown_event)

```js
const dogPictureElement = document.getElementById("dog-image");
const keyCodes = {
    "left":"ArrowLeft",
    "up":"ArrowUp",
    "right":"ArrowRight",
    "down":"ArrowDown"
}

let posX = dogPictureElement.offsetTop;
let posY = dogPictureElement.offsetLeft;

document.body.addEventListener("keydown", e => {
        if (e.code === keyCodes["left"]) {
            posX -= 5;
            dogPictureElement.style.left = posX + "px"
            }
        else if (e.code === keyCodes["right"]) {
            posX += 5;
            dogPictureElement.style.left = posX + "px"
        }
        else if (e.code === keyCodes["up"]) {
            posY -= 5;
            dogPictureElement.style.top = posY + "px"
        }
        else if (e.code === keyCodes["down"]) {
            posY += 5;
            dogPictureElement.style.top = posY + "px"
        }
    });
```

![DogRun.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/2bd0d566-49eb-e482-788a-2acd544d220f.gif)

### 副教材


* [イベントリファレンス - MDN](https://developer.mozilla.org/ja/docs/Web/Events)
    * 主なイベント、そのイベントのドキュメントへのリンクが載っている
* [localStorage - MDN](https://developer.mozilla.org/ja/docs/Web/API/Window/localStorage)

### 学んだこと

* イベント駆動型アプリの実装の流れ
* 簡単な文字列操作・HTMLへの挿入
* モーダルダイアログの実装