<!--
title: 要画像追加
 -->

## はじめに

HTML/CSS/JavaScriptで10個(くらい)何かを作ってみるチャレンジの一環として色々作っていきます。
以下のUdemy教材をやっていきます。

https://www.udemy.com/course/javascript-web-projects-to-build-your-portfolio-resume/

量が多いので、「初めて知った」「参考になった」箇所のみ書いていきます。

### 目的

何か作ってみるチャレンジの目的は、
**HTML/CSS/Vanilla JSを使ってとりあえずなにか作ること、手を動かすこと**です。

これでは曖昧すぎるので、もう少し深掘ります。

**現状**

* HTML/CSS/JavaScriptについて、コードを見ればなんとなく理解出来る。
* チュートリアルと一緒に進めれば何かは作れる。
* 0から何か作ろうと思うと厳しい。
    * Python(業務効率化などで使用)の場合はある程度出来る。

なぜ厳しいのか？を考えた時に、
Pythonとの違いは**実際に手を動かしているかどうか**だなと思いました。

プログラミングにおいて手を動かすに勝る学習方法はないと思います。
実感としてもそうですし、そう言っているエンジニアの方も多く感じます。

また、質を高めるためにも、まずは絶対的な量が必要とよく言います。

というわけで、色々作ってみることにしました。

### ルール

- 期間は３週間くらい。
- 数は10個くらい。
- お題はパクリでもOK。
  - ただし、教材に従って進めるだけ、はNG。アイデアは持ってきてもいいし参考にするのは良いが、まずは自分で考える。
- 人のコードを参考にしても良いが、ただのコピペはNG。何をしているのか理解すること。

また、今回のように動画を参考にして作る場合は以下のような流れで進めました。

1. 1セクションごとに自分ならどうするか考える
1. ざっくり実装したり、処理をコメントで書いたりしてみる
1. 動画を見ながら修正

### 参考

以下から面白そうなお題をいくつか参考にします。

- [ポートフォリオに役立つJavaScriptプロジェクト40選（動画あり） - Qiita](https://qiita.com/baby-degu/items/33acb94e404feaf58d35)
- [JavaScript 30](https://javascript30.com/)
- [JavaScript Web Projects: 20 Projects to Build Your Portfolio | Udemy](https://www.udemy.com/course/javascript-web-projects-to-build-your-portfolio-resume/)

***

リポジトリ

https://github.com/NasuPands/My-10-Web-Dev-Projects

***

# Infinite Scroll

## 概要

無限スクロール出来るアプリを作る。

### 主な目的

- UIの構築、ロードアニメーションについて学ぶ
- 無限スクロールの実装方法を学ぶ
    - 「どこまでスクロールしたら」はどう判定する？

### 完成イメージ

![infinite-scroll-demo]](https://user-images.githubusercontent.com/85564407/156168031-4a0e3ec8-febd-41fd-ad58-13dd276e9c67.gif)

### 必要な要素

- UIの構築とロードアニメーション
- 最初にアクセスした時はAPIを叩き取得した投稿が表示される
    - 使用するAPI [https://jsonplaceholder.typicode.com/](https://jsonplaceholder.typicode.com/)
- スクロールするとロードされ、次の投稿が表示される

### 投稿の番号を丸数字で表示

```css
.post .number {
    position: absolute;
    top: -15px;
    left: -15px;
    font-size: 15px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: #fff;
    color: #296ca8;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 7px 10px;
}
```

![スクリーンショット 2022-02-28 午後21.14.55 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c7a78cd-33ae-4cb8-bae9-90933246fd43/スクリーンショット_2022-02-28_午後21.14.55_午後.png)

`post` に対して 絶対位置指定 + `-15px` → 左上に固定
`flex` で中央寄せ → `number` の中身を中央に寄せることで中央に表示する

### アニメーション（丸がバウンドする）

![bounce-animation.gif](https://user-images.githubusercontent.com/85564407/156571215-e1a51e7b-4aa4-4e7c-b0f6-43c523b79c55.gif)

やってることは単純。
丸を作る → アニメーションを設定する → 1つずつディレイを入れる

```css
.circle {
    background-color: #fff;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    margin: 5px;
    animation: bounce 0.5s ease-in infinite;
}

.circle:nth-of-type(2) {
    animation-delay: 0.1s;
}

.circle:nth-of-type(3) {
    animation-delay: 0.2s;
}

@keyframes bounce {
    0%,
    100% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-10px);
    }
}
```

### スクロール時の処理

```js
window.addEventListener("scroll", () => {
    // 全ブラウザ対応のため、bodyとhtmlのscrollTopを利用
    const { scrollHTMLTop, scrollHeight, clientHeight } = document.documentElement;
    const scrollBodyTop = document.body.scrollTop;
    const scrollTop = scrollBodyTop || scrollHTMLTop;

    if(scrollTop + clientHeight >= scrollHeight - 5) {
        showLoading();
    }
});
```

#### `documentElement` とは

> `Document.documentElement`は、その[document](https://developer.mozilla.org/ja/docs/Web/API/Document)`のルート要素 (例えば、 HTML 文書の場合は `[<html>](https://developer.mozilla.org/ja/docs/Web/HTML/Element/html)要素) である [Element](https://developer.mozilla.org/ja/docs/Web/API/Element)を返します。
> 
> [Document.documentElement - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/Document/documentElement)

要するにHTML。

#### `scrollTop` `scrollHeight` `clientHeight` の違い

ここで結構詰まりました。



> ⚠ `scrollTop` には罠があって、ページ全体のスクロール量を取得したい場合は **ブラウザによって取得方法が違います**。

> - WebKit 系 ( Safari, Chrome 等) や Edge では `body.scrollTop`
> - IE, Firefox, Opera などでは `html.scrollTop`

> そのため、正しく取得するには以下のように書きます。

> ```js
> var body = document.body;
> var html = document.documentElement;
>
> var scrollTop = body.scrollTop || html.scrollTop;
> ```
> 
> Bodyが長い場合
> 
> ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f88f5dcb-8619-4203-a2a5-04b5e349fc57/Untitled.png)
> 
> Bodyが短い場合
>
> ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4db06c4-a168-4228-835f-d2da8866afe4/Untitled.png)
>
> [結局「下からのスクロール位置」を取得するにはどうすればいいのか - Qiita](https://qiita.com/hoto17296/items/be4c1362647dd241905d) より

まとめ

- `scrollTop` 要素内のスクロール量 （スクロールした量）
- `clientHeight` 要素の高さ
- `scrollHeight` 要素内でスクロールできる高さ

動画では`documentElement.scrollTop`を使っていたので、Chromeでは動作しませんでした。

#### スクロール時に実行する処理

`show` クラスを追加 ⇔ 削除、`page` をインクリメント、投稿の表示。

```js
/** Fetch the post and show loader */
function showLoading() {
    loading.classList.add("show");

    setTimeout(() => {
        loading.classList.remove("show");

        setTimeout(() => {
            page++;
            showPosts();
        }, 3000)

    }, 1000);
}
```

# Memory Cards

## 概要

フラッシュカードを作る。

### 主な目的

- 前のカード/次のカードを表示する手法を学ぶ
- カードを反転させるようなアニメーションについて学ぶ
- カードの追加/削除を学ぶ

### 完成イメージ

![スクリーンショット 2022-03-01 午後21.30.04 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c00693d1-9393-4966-a8ab-09bedf6366e2/スクリーンショット_2022-03-01_午後21.30.04_午後.png)

### 要素

- CSSでカードを作成する
- フォームで「Add new card」オーバーレイフォーム(モーダルダイアログのこと？)を構築
    - `display` による表示制御
- 前のカード/次のカードを表示できる
    - リストを作っておき、全体/現在位置を取得
- 質問カードを表示、カードをアニメーションで反転させて回答表示
    - CSSアニメーション
- ローカルストレージにカードを追加/削除
    - `LocalStorage` の利用

## HTML/CSS

### `absolute` によるモーダルダイアログ

`absolute` は**親に対する絶対位置指定**。
`body` の子要素に `absolute` を適用すると以下のようになり、要素を重ねることが出来る。

`absolute` あり

![スクリーンショット 2022-03-02 午後07.22.22 午前.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e6939dc8-038b-43c7-97d8-e196f1af7a2a/スクリーンショット_2022-03-02_午後07.22.22_午前.png)

なし

![スクリーンショット 2022-03-02 午後07.22.56 午前.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b9979351-0679-44b4-8efc-e1d1442770ca/スクリーンショット_2022-03-02_午後07.22.56_午前.png)

## JavaScript


### `className` によるクラスの上書き

`classList` で `add/remove` する以外に、 `className` で上書きする方法もある。

```js
element.className = "show active";
```

### 三項演算子を使って `null` の時は空の配列を返す

```js
function getCardsData() {
  const cards = JSON.parse(localStorage.getItem("cards"));
  return cards === null ? [] : cards;
}
```

### カード単体を削除するボタンを実装してみる

```js
deleteBtn.addEventListener("click", () => {
  cardsData.splice(currentActiveCard, 1);
  setCardsData(cardsData);
})
```

[splice() - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)を使用。

# プロジェクト名

## 概要

ニューイヤーカウントダウン。

### 主な目的

- おしゃれなページの構築
- JavaScriptを使った時間の計算
- アニメーション作成

### 完成イメージ

![スクリーンショット 2022-03-02 午後22.32.44 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/568670ca-bd0f-4495-b792-9c7953ddf4d7/スクリーンショット_2022-03-02_午後22.32.44_午後.png)

## HTML/CSS

### 背景を画像にする

```css
body {
  background-image: url('https://images.unsplash.com/photo-1467810563316-b5476525c0f9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1349&q=80');
  /* 背景画像を1枚のみにする */
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  height: 100vh;
  color: #fff;
  font-family: "Lato", sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  margin: 0;
  overflow: hidden;
}
```

`repeat` `size` `position` の指定により背景を1枚の画像にしている。


### Overlay(背景を暗く)

```css
/* Add a dark overlay */
body::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}
```

before
![スクリーンショット 2022-03-03 午後06.15.50 午前.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/51c52e4c-e95e-43b6-ad8c-1110eacc18de/スクリーンショット_2022-03-03_午後06.15.50_午前.png)
after
![スクリーンショット 2022-03-03 午後06.18.43 午前.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3fc42683-f379-4992-b31c-167b3855db4b/スクリーンショット_2022-03-03_午後06.18.43_午前.png)

疑似要素に対して `background-color` を割り当てることで実装します。

ただ、現状では文字まで暗くなってしまっています。
`z-index` の指定により背景以外の要素は暗くならないようにします。

```css
body * {
  z-index: 1;
}
```

  ![スクリーンショット 2022-03-03 午後06.16.46 午前.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ced62de1-5d16-4d95-9467-156aab0ab5b6/スクリーンショット_2022-03-03_午後06.16.46_午前.png)

### メディアクエリ

`font-size` 、 `margin` をいじっている。

```css
@media(max-width: 500px) {
  h1 {
    font-size: 45px;
  }

  .time {
    margin: 5px;
  }

  .time h2 {
    font-size: 12px;
    margin: 0;
  }

  .time small {
    font-size: 10px;
  }
}
```

## JavaScript

### 時間の制御

```js
const currentYear = new Date().getFullYear();
const newYearTime = new Date(`January 01 ${currentYear + 1} 00:00:00`);

function updateCountdown() {
  const currentTime = new Date();
  const diff = newYearTime - currentTime;

  // ÷1000 = ms => s
  const d = Math.floor(diff / 1000 / 60 / 60 / 24);
  const h = Math.floor(diff / 1000 / 60 / 60) % 24;
  const m = Math.floor(diff / 1000 / 60) % 60;
  const s = Math.floor(diff / 1000) % 60;

  console.log(d, h, m, s)
  // => 303 17 17 37
}

setInterval(updateCountdown, 1000);
```

`new Date` は引数を渡さずに実行すると現在の時間を元に生成される。
それを利用してカウントダウンする。

### タイマー更新待ちを隠してローディングを表示

`setInterval` を使用している都合上、以下のようにタイマーが表示されるまでラグが生じる。

[lag-gif](https://user-images.githubusercontent.com/85564407/156462289-1056d5e4-da22-4084-ab9f-f95805d1a98b.gif)

それをローディングアニメーションで隠す。

具体的には、以下のようにする。`loading` はただの `.gif` 画像。

```js
// show spinner before countdown
setTimeout(() => {
  loading.remove();
  countdown.style.display = "flex";
}, 1000);
```

`countdown` の `display` を `none` にしておき、 `setTimeout` により `flex` にする。

[loading](https://user-images.githubusercontent.com/85564407/156462643-3a0f58db-bf3d-42ba-847d-836e81019847.gif)

## まとめ

教材全体で共通していた箇所をまとめてみます。

### `padding` は要素の中に余白を作りたい時によく使う

`余白を作りたい時には`padding`を使います。
中にテキストを持つ要素はほとんど`padding`を使っていました。

`padding` なし

![スクリーンショット 2022-02-27 午後14.59.19 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cbc22258-8c19-463c-88e9-b85335f55dc1/スクリーンショット_2022-02-27_午後14.59.19_午後.png)

`padding` あり

![スクリーンショット 2022-02-27 午後14.59.26 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3d7b5216-1c5e-498b-9580-9f5ad6395f04/スクリーンショット_2022-02-27_午後14.59.26_午後.png)

### `border-radius`よく使う

カクカクしたデザインは滅多に無いです。
だいたい角を丸めます。

### 要素間を離したい時は`margin`

当然といえば当然ですが、要素サイズの大小に関わらず要素間の距離を開けたい時は`margin`を使います。

### レイアウトの構成

人によるとは思いますが、この教材の場合`flex`の使用率が圧倒的でした。

レイアウト全体をいくつかの大きめな「ブロック」に分割して構成、`body`に``flex`を適用して中央寄せ。
という流れが多かったです。

この作り方はわかりやすくて好きです。

### 1番上/下の要素は上/下に余白を作る

1番上/下にいる要素は上/下に`margin`を設定することで、不自然にならない程度の余白を作っていました。

### 開発の流れ

JavaScriptによるDOM操作でレイアウトを作る場合、以下の流れが共通していました。
「チュートリアルでやるような小規模なアプリケーションだとこの方がわかりやすい」という話かもしれませんが、実際この流れだと理解しやすかったです。

1. まずダミーHTML（JavaScriptで作る予定のレイアウト）を書く
2. ダミーHTMLに対してCSSを書いてスタイルを設定
3. 最後にJavaScriptを書き、DOM操作してレイアウトを作っていく

### ユーザー入力の扱い

ユーザーの文字列入力は `toUpperCase` で小文字/大文字の差異を吸収することが多めでした。

### VSCodeの使い方

VSCodeでHTMLを書く時、button.random-btn#randomと入力すると
`<button class=”random-btn” id=”random”>`になる。

# ✅ 随時追加