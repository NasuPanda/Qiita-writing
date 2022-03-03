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

# Movie Seat Booking

## 概要

映画の座席予約アプリ。

それぞれの映画には異なるチケット料金が設定されていて、席が選択されると料金が表示される。

### 主な目的

- 良い感じのレイアウト構築方法を学ぶ
- 状態に応じて変化するUIの構築を学ぶ
- ローカルストレージの操作を学ぶ

### 完成イメージ

![demo](https://user-images.githubusercontent.com/85564407/155833480-b370b29f-afe1-4ac7-baef-28b5614a87db.gif)

## HTML/CSS

### セレクタの使い方

```html
<ul class="showcase">
    <li>
        <div class="seat"></div>
        <small>N/A</small>
    </li>
    <li>
        <div class="seat selected"></div>
        <small>Selected</small>
    </li>
    <li>
        <div class="seat occupied"></div>
        <small>Occupied</small>
    </li>
</ul>
```

- `seat` と `selected` を持つ要素が選択される

```css
.seat.selected {
    background-color: #6feaf6;
}
```

- `seat` の `occupied` を持たない要素が選択される

```css
.seat:not(.occupied):hover {
    cursor: pointer;
    transform: scale(1.2);
}
```

- `showcase` の子要素、かつ `seat` を持ち、 `occupied` を持たない要素が選択される

```css
/* showcaseでは無効 */
.showcase .seat:not(.occupied):hover {
    cursor: default;
    transform: scale(1);
}
```

### 席のスタイル

```css
.seat {
    background-color: #444451;
    height: 12px;
    width: 15px;
    /* 要素を切り離す */
    margin: 3px;
    /* 左右上側を丸めてシートっぽくする */
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}
```

四角を描く → 左上と右上を丸めてシートっぽく → `margin`で切り離す

✅ ここに画像

### 端2列を少し離す

```css
.seat:nth-of-type(2) {
    margin-right: 18px
}

.seat:nth-last-of-type(2) {
    margin-left: 18px
}
```

**参考**

- [:nth-child() - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/:nth-child)
- [:nth-of-type() - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/:nth-of-type)
- [【CSS】nth-childとnth-of-typeでもう混乱しない。 - Qiita](https://qiita.com/shunsuke227ono/items/6c9916f80d82b73a7025)

**`:nth-of-type()`**
「指定したタグの親要素」の子要素のうち、「指定したタグ」の「N番目」の要素を選択する。

**`:nth-child()`**
「 指定したタグの親要素」の子要素を見て、「タグ関係なし」に「N番目」の要素を選択する。

### スクリーンのスタイルを3D風に

```css
/* ------------------------------------------------------------------------ */
/* スクリーン */
/* ------------------------------------------------------------------------ */
.screen {
    background-color: #fff;
    height: 70px;
    width: 100%;
    margin: 15px 0;
    transform: rotateX(-45deg);
    box-shadow: 0 3px 10px rgba(255, 255, 255, 0.7);
}
.container {
        perspective: 1000px;
        margin-bottom: 30px;
    }
```

`transform` でX軸を基準に-45度回転。
`perspective` で3D配置された子要素に遠近感を与える。

**参考**

- [CSS perspectiveを使ったデザイン - Qiita](https://qiita.com/junya/items/a456e14da4bb2b11806f)

回転・遠近なし

![screen-non-perspective.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2528a384-1f99-4a22-b251-7552ed220f82/screen-non-perspective.png)

回転・遠近あり
X軸を基準に若干傾き、3D風になっている。

![screen.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f7c2fed4-9d58-49f8-8a97-8d24f4a97f61/screen.png)

## JavaScript

### 数値型に変更する簡単な方法

```js
const ticketPrice = +movieSelect.value;
```

代入するとき文字列の前に `+` を置くことで数値型に変換できる

### シートにイベント追加

席にイベントを追加していく・・・のかと思いきや、
`container` にイベントを追加する。

```js
container.addEventListener("click", (e) => {
    console.log(e.target)
})
```

親要素で発火したクリックイベントに対して、 `event.target` とすることでクリックされた要素を取り出すことが出来る。

# Meal Finder

## 概要

様々なカテゴリのレシピを検索出来るアプリを作る。

### 主な目的

- 検索〜結果を表示する流れの実装を学ぶ
- UIの構築方法を学ぶ

### 完成イメージ

![スクリーンショット 2022-02-27 午後15.27.03 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/107a500e-052a-4aa6-99ef-5b99b739a083/スクリーンショット_2022-02-27_午後15.27.03_午後.png)

### 要素

- MealDBを使う
    - [Free Meal API | TheMealDB.com](https://www.themealdb.com/api.php)
- 検索・ランダム検索用のUIを構築
- 検索すると一覧が表示され、それぞれの画像はホバー可能
- レシピの写真をクリックすると、詳細が表示される
- ランダム検索をクリックすると、ランダムにレシピが表示される

## HTML/CSS

HTML全体は以下。

```html
<body>
    <div class="container">
        <h1>Meal Finder</h1>
        <div class="flex">
            <form class="flex" id="submit">
                <input type="text" id="search" placeholder="Search for meals or keywords">
                <button class="search-btn" type="submit">
                    <i class="fas fa-search"></i>
                </button>
                <button class="random-btn" id="random">
                    <i class="fas fa-random"></i>
                </button>
            </form>
        </div>
    </div>

    <div id="result-haaind"></div>
    <div id="meals" class="meals"></div>
    <div id="single-meal"></div>
    <script src="script.js"></script>
</body>
```

### 検索欄を作る方法

完成形
![search-bar.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/25b99cc1-00f6-4c87-9812-e759b989ead9/search-bar.png)

```css
.flex {
    display: flex;
}

input,
button {
    border: 1px solid #dedede;
    border-top-left-radius: 4px;
    border-bottom-left-radius: 4px;
    font-size: 14px;
    padding: 8px 10px;
    margin: 0;
}

input[type="text"] {
    width: 300px;
}
```

![search-process-1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/937bf273-c465-449c-b0a3-59637754ca4c/search-process-1.png)

- `input` 、2つの `button` を `.flex` で囲って横並びに
- 共通で`border` をセット、左側の角を丸める

```css
.search-btn {
    cursor: pointer;
    border-left: 0;
    border-radius: 0;
    border-top-right-radius: 4px;
    border-bottom-right-radius: 4px;
}
```

![search-process-2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d7bc397a-724f-454c-8f3a-50933a09a486/search-process-2.png)

- `.search-btn` は `border` を削除、右側だけ丸める

```css
.random-btn {
    cursor: pointer;
    margin-left: 10px;
    border-top-right-radius: 4px;
    border-bottom-right-radius: 4px;
}
```

- `random-btn` は検索欄から少しだけ離し、右側も丸める

![search-bar.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/25b99cc1-00f6-4c87-9812-e759b989ead9/search-bar.png)

### 検索結果をカード風に表示する

![スクリーンショット 2022-02-27 午後12.54.37 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f8768405-a1d6-4d01-ae4d-c605882b67b9/スクリーンショット_2022-02-27_午後12.54.37_午後.png)

```html
<div class="meal">
    <img src="https://www.themealdb.com/images/media/meals/spswqs1511558697.jpg" alt="Three Fish Pie">
    <div class="meal-info" data-mealid="52882">
        <h3>Three Fish Pie</h3>
    </div>
</div>
```

```css
.meals {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    /* grid 同士の距離 */
    grid-gap: 20px;
    margin-top: 20px;
}
```

- `grid` で4列表示にして、間隔を離す。

```css
.meal {
    cursor: pointer;
    position: relative;
    height: 180px;
    width: 180px;
    text-align: center;
}
```

- 元画像サイズで表示(大きい)されてしまうため、サイズに制限をかける
- `absolute` を子要素で利用するため `relative` にしておく

```css
.meal img {
    width: 100%;
    height: 100%;
    border: 4px #fff solid;
    border-radius: 2px;
}
```

- 画像の周りをボーダーで囲い、丸める → 画像のみ表示よりもカードっぽく
- 幅と高さを親要素 `meal` に対する100％に

```css
.meal-info {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    background: rgba(0, 0, 0, 0.7);
    display: flex;
    align-items: center;
    justify-content: center;
    transition: opacity 0.2s ease-in;
    opacity: 0;
}

.meal:hover .meal-info {
    opacity: 1;
}
```

`meal` の子要素として `img` & `meal-info`があるため、`meal-info` は本来画像の下側に表示される。

今回はホバーしたら `meal-info` が表示される形式にしたいので、 `absolute` を使って親要素の真上に `meal-info` を持ってくる。

さらに、`flex` で中央寄せ。
ホバーされた時に `opacity` が1(不透明)になるようにする。

![meal-info](https://user-images.githubusercontent.com/85564407/155867516-428571b2-8194-45f4-af49-6527ee0b8991.gif)

### メディアクエリ `grid`利用

```js
/* ------------------------------------------------------------------------ */
/* メディアクエリ */
/* ------------------------------------------------------------------------ */

@media(max-width: 800px) {
    .meals {
        grid-template-columns: repeat(3, 1fr);
    }
}
@media(max-width: 700px) {
    .meals {
        grid-template-columns: repeat(2, 1fr);
    }

    .meal {
        height: 200px;
        width: 200px;
    }
}
@media(max-width: 500px) {
    input[type="text"] {
        width: 100%;
    }
    .meals {
        grid-template-columns: repeat(1fr);
    }
    .meal {
        height: 300px;
        width: 300px;
    }
}
```

幅に応じて `grid` 、 `meal` の幅を変更することでレスポンシブに

### クリックされた食事の詳細を表示する

イメージ

![スクリーンショット 2022-02-27 午後13.51.36 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f62b34a7-bcc2-4482-bee5-842e0c7354ec/スクリーンショット_2022-02-27_午後13.51.36_午後.png)

```js
mealsEl.addEventListener("click", e=> {
    const mealInfo = e.path.find(item => {
        if(item.classList) {
            return item.classList.contains("meal-info");
        } else {
            return false;
        }
    });

    if(mealInfo) {
        const mealID = mealInfo.getAttribute("data-mealid");
        getMealByID(mealID);
    }
})
```

[find()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/find)を使って`e.path` の中から`meal-info` を取得する。

✅ `find` は指定した条件に当てはまる最初の要素を取得する。正確には、 `truethy` な値を返せばその値が即座に返され、なければ `undefined` を返す

`e.path` の中身

![スクリーンショット 2022-02-27 午後13.01.38 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/126e5cbb-1753-4186-8b2f-f4c75069ab1f/スクリーンショット_2022-02-27_午後13.01.38_午後.png)

そして、カスタムデータ属性 `data-mealid` を使ってIDを取得、関数に渡す。


# Expense Tracker

## 概要

収支管理アプリ。

### 主な目的

- UIの構築方法を学ぶ

### 完成イメージ

![スクリーンショット 2022-03-01 午後21.18.19 午後.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fbac58b6-7254-49d1-a766-484ff7d88b37/スクリーンショット_2022-03-01_午後21.18.19_午後.png)

### 必要な要素

- UIの構築
- 売買したアイテムを表示する
- 残高・収支の合計を表示
- 新しい売買の追加、反映可能
- アイテム削除可能
- LocalStorageの使用

## HTML/CSS

### income / expenseの表示欄


```html
<div class="inc-exp-container">
  <div>
    <h4>Income</h4>
        <p id="money-plus" class="money plus">+$0.00</p>
    </div>
    <div>
        <h4>Expense</h4>
        <p id="money-minus" class="money minus">-$0.00</p>
    </div>
</div>
```

```css
.inc-exp-container {
  background-color: #fff;
    box-shadow: var(--box-shadow); /* 変数を利用 */
    padding: 20px;
    display: flex;
    justify-content: space-between;
}
```

`flex` + `space-between` でコンテナの両サイドに表示

![スクリーンショット 2022-03-01 午後07.44.30 午前.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e9fd1659-15e4-435a-83b1-4cb778cb8fd5/スクリーンショット_2022-03-01_午後07.44.30_午前.png)


```css
.inc-exp-container div {
  flex: 1;
    text-align: center;
}

.inc-exp-container div:first-of-type {
  border-right: 1px solid #dedede;
}
```

`flex: 1` で隙間を埋めることで中央寄せする

![スクリーンショット 2022-03-01 午後07.50.15 午前.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a7d399d6-cda3-42c3-a75a-bae20ca083ba/スクリーンショット_2022-03-01_午後07.50.15_午前.png)

`flex: 1;` は、`grow` `shrink` `basis` の一括指定プロパティ。
値が一つの場合は `grow` (空いた幅を埋める)を設定したことになる。

- `[flex-grow](https://developer.mozilla.org/ja/docs/Web/CSS/flex-grow)`
- `[flex-shrink](https://developer.mozilla.org/ja/docs/Web/CSS/flex-shrink)`
- `[flex-basis](https://developer.mozilla.org/ja/docs/Web/CSS/flex-basis)`

### `inline-block`

```css
label {
    /* inline-blockにより高さを設定できるように */
    display: inline-block;
    margin: 10px 0;
}
```

![スクリーンショット 2022-03-01 午後08.07.36 午前.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0be48b06-e1c4-4284-8a77-762fe46ab408/スクリーンショット_2022-03-01_午後08.07.36_午前.png)

`inline-block` はブロックのように振る舞う `inline` 要素。
`inline` 要素に高さの設定（ `margin` など）をしたい時使う。
( `inline` の場合、高さは文字の大きさに依存するため)

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

### ボタン

だいたい `cursor: pointer`。

```css
.check-btn:active {
  transform: scale(0.98);
}
```

クリックされた時若干小さくする。

https://user-images.githubusercontent.com/85564407/156666412-67bc0ee4-778b-4018-a404-95a526ee1eeb.gif

### VSCodeの使い方

VSCodeでHTMLを書く時、button.random-btn#randomと入力すると
`<button class=”random-btn” id=”random”>`になる。