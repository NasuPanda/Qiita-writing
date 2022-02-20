## はじめに

HTML/CSS/JavaScriptで10個(くらい)何かを作ってみるチャレンジの一環として、
〇〇していきます。

リポジトリは以下です。

https://github.com/Westen0511/My-10-Web-Dev-Projects

### 目的

**HTML/CSS/JavaScriptを使ってとりあえずなにか作ること。手を動かすこと。**

これでは曖昧すぎるので、もう少し深掘ります。

**現状**

* HTML/CSS/JavaScriptについて、コードを見ればなんとなく理解出来る。
* チュートリアルと一緒に進めれば何かは作れる。
* 0から何か作ろうと思うと厳しい。Pythonの場合はある程度出来る。

なぜ厳しいのか？を考えた時に、Pythonとの違いは**手を動かしているかどうか**だなと思いました。

プログラミングにおいて手を動かすに勝る学習方法はないと思います。
実感としてもそうですし、色々な方がそうおっしゃっています。

また、質を高めるためにも、まずは絶対的な量が必要とよく言います。

というわけで、色々作ってみることにしました。

### ルール

- 期間は３~４週間くらい。
  - 数を稼ぐために適当になったら本末転倒なので、時間が足りない場合延長する。
- 「何か」の基準は自分の中で人様に見せれるレベルのもの。
- お題はパクリでもOK。
  - ただし、教材に従って進めるだけ、はNG。アイデアは持ってきてもいいし参考にするのは良いが、まずは自分で考える。
- 人のコードを参考にしても良いが、ただのコピペはNG。何をしているのか理解すること。

### 参考

面白そうなお題やネタ切れになった時に参考にします。

- [ポートフォリオに役立つJavaScriptプロジェクト40選（動画あり） - Qiita](https://qiita.com/baby-degu/items/33acb94e404feaf58d35)
- [JavaScript 30](https://javascript30.com/)

# JSON→CSV変換ツール

## 概要

- JSON文字列を入力したり、JSONファイルをアップロード出来る
- 入力をCSVに変換する
- 変換後のCSVをユーザに表示、ダウンロード出来る

### 主な目的

- Web上のファイルの扱い、アップロードやダウンロードについて学ぶ
- HTML/CSSを使って0から何か作ってみる

### 完成予想図

Keynoteを使って簡単なモックアップを作ってみました。

![mockup](https://github.com/Westen0511/Qiita-writing/blob/main/My-10-WebDevProjects/json-to-csv/mock-up.png?raw=true)

### 必要な要素

現時点で想像がつく範囲で、必要な要素を書き出してみます。

- 文字の入力/ファイルのアップロード
- CSVの出力/ファイルのダウンロード
- ファイル/文字列のどちらかが入力されていることを確認するバリデーション
    - どちらも入力されていなければ❎
    - どちらか入力されていれば⭕
    - どちらも入力されている場合も❎
- タブ切り替え可能な入力ボックスが欲しい

## HTMLの実装

まずは見た目を作っていきます。

### JSON入力ボックス

**参考**

- [<textarea> - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/textarea)
- [<textarea>  in placeholder - MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/textarea#attr-placeholder)

`textarea` を利用します。

また、`placeholder` を利用して入力のヒントを表示してみます。

その際、 `textarea` の閉じタグの前に改行があると「入力値がある」とみなされてしまいヒントが表示されなくなるみたいです。

```html
<label for="input-json">Input JSON:</label>
<textarea id="input-json" name="input-json" rows="5" cols="33" placeholder=" {key : value} "></textarea>
```

### ファイルのアップロード

`<input type="file">` を使えば良さそう。

JSONのMIMEタイプは `application/json` 。

```html
<input id="input-json-file" type='file' accept="application/json">
```

また、**FileAPI** を使えばファイルの読み取りが可能なようです。

### CSV出力ボックス

`table` として実装します。

```html
<table id="color_list"></table>
```

### ファイルのダウンロード

**参考**

- [Webフロントエンドだけでファイルを読み書きしたい - zenn](https://zenn.dev/pirosuke/articles/web-file-io-without-backend)
- [JavaScriptでファイルダウンロード処理を実現する - Qiita](https://qiita.com/wadahiro/items/eb50ac6bbe2e18cf8813)

調べてみたところ、以下のような流れでダウンロード可能なようです。

> 1.リンクの[HTML5のdownload属性](https://developer.mozilla.org/ja/docs/Web/HTML/Element/a#Attributes)を使用してダウンロードファイル名を設定
> 2.[File APIのBlob](https://developer.mozilla.org/ja/docs/Web/API/Blob)を使用してデータを作成
> 3.`window.URL.createObjectURL`でBlobからURLを生成しそれをリンク先に設定
> [JavaScriptでファイルダウンロード処理を実現する - Qiita](https://qiita.com/wadahiro/items/eb50ac6bbe2e18cf8813)

```html
<a id="download" href="#" download="result.csv" onclick="handleDownload()">CSVダウンロード</a>
```

### その他実装

現時点では以下です。

```html
<header>
		<h1>JSON to CSV Online Converter</h1>
</header>
    <h2>JSONファイルをオンラインでCSVファイルに変換出来るツールです。</h2>
    <ol>
        <li>① JSON文字列を入力してください。<br>もしくは<br>JSONファイルをアップロードしてください。</li>
        <li>② CSV変換結果が表示されます。ダウンロードも可能です。</li>
    </ol>

    <!-- タブ切り替え可能な入力ボックス -->
    <div id="input-container">
        <!-- JSON入力-->
        <div id="input-json-container">
            <label for="input-json-text">Input JSON:</label>
            <!-- placeholderを使う場合、改行も入力とみなされるため閉じタグ前で改行しない -->
            <textarea id="input-json-text" name="input-json-text" rows="5" cols="33" placeholder="{key : value}"></textarea>
        </div>
        <!-- ファイルアップロード -->
        <div id="file-upload-container">
            <input id="input-json-file" type='file' accept="application/json">
        </div>
    </div>

    <!-- タブ切り替え可能な出力ボックス -->
    <div id="output-container">
        <!-- CSV出力 -->
        <div id="output-csv-container">
            <table id="csv">
                <thead>
                    <tr>
                        <th>CSV</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>hoge</td>
                        <td>hoge</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <!-- ファイルダウンロード -->
        <div id="file-download-container">
            <a id="download" href="#" download="result.csv" onclick="handleDownload()">CSVダウンロード</a>
        </div>
    </div>
```

![minimum-html](https://github.com/Westen0511/Qiita-writing/blob/main/My-10-WebDevProjects/json-to-csv/html-end.png?raw=true)

***

ひとまず最低限のHTMLは出来たはずなので、
タブ切り替え実装、CSSで装飾していきます。

***

## タブ切り替え実装

```html
<!-- タブ切り替え可能な入力ボックス -->
<div id="input-container">
    <!-- 切り替え用のタブ -->
    <input type="radio" name="tab" id="input-json-tab" checked>
    <label class="tab" for="input-json-tab">JSON入力</label>
    <input type="radio" name="tab" id="upload-json-tab">
    <label class="tab" for="upload-json-tab">JSONアップロード</label>
    <!-- JSON入力-->
    <div id="input-json-container" class="content">
        <label for="input-json-text">Input JSON:</label>
        <!-- placeholderを使う場合、改行も入力とみなされるため閉じタグ前で改行しない -->
        <textarea id="input-json-text" name="input-json-text" rows="5" cols="33" placeholder="{key : value}"></textarea>
    </div>
    <!-- ファイルアップロード -->
    <div id="upload-json-container" class="content">
        <input id="input-json-file" type='file' accept="application/json">
    </div>
</div>

<!-- 同様に出力ボックスも作成 -->
```

```css
/* ------------------------------------------------------------------------ */
/* タブ切り替え */
/* ------------------------------------------------------------------------ */

#input-container {
    margin: auto;
    display: flex; /* デフォルト表示 */
    flex-wrap: wrap;
    justify-content: center;
}
#output-container {
    margin: auto;
    display: none; /* デフォルト非表示 */
    flex-wrap: wrap;
    justify-content: center;
}

input[name="tab"] {
    display: none;
}

input:checked + .tab {
    background-color: aquamarine;
}

.content-container {
    display: none;
}

#input-json-tab:checked ~ #input-json-container,
#upload-json-tab:checked ~ #upload-json-container,
#output-csv-tab:checked ~ #output-csv-container,
#download-csv-tab:checked ~ #download-csv-container {
    display: block;
}
```

`input type="radio"` と `display:none` を利用してラジオボタンを隠すことで、1つだけ選択出来るタブを作成。

`:checked` と `id` により、選択されたタブと紐付けられた `content` のみを表示することで実装しました。

1ページに入出力を表示すると窮屈な感じがしたので、**変換処理を実行したら表示が出力に切り替わる形式**に変更することにしました。

### 補足 `button role="tab"`

今回は実装しませんが、アクセシビリティを考慮するなら `button role="tab"` を使ったほうが良さそうです。
確かにラジオボタンはタブとして適切とは言い難い・・・ですよね。

**参考**

- [ARIA: tab ロール - アクセシビリティ | MDN](https://developer.mozilla.org/ja/docs/Web/Accessibility/ARIA/Roles/Tab_Role)
- [Webアクセシビリティを考慮したチェックボックス・ラジオボタン・セレクトボックス・タブ・アコーディオンの実装 | Will Style Inc.](https://www.willstyle.co.jp/blog/4841/)
- [Example of Tabs with Automatic Activation | WAI-ARIA Authoring Practices 1.1](https://www.w3.org/TR/wai-aria-practices-1.1/examples/tabs/tabs-1/tabs.html)

### `checked`の注意点

![no-checked](https://github.com/Westen0511/Qiita-writing/blob/main/My-10-WebDevProjects/json-to-csv/radio-checked-miss.png?raw=true)

デフォルトでJSON入力が `checked` になるようにしたはずなのですが、何も表示されません。

よくよく考えてみると単純な話で、 入力/出力タブの両方に`checked`を指定していたためでした。

```html
<input type="radio" name="tab" id="input-json-tab" checked>
・・・
<input type="radio" name="tab" id="output-csv-tab" checked>
```

[MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/input/radio#:~:text=selected%20by%20default.-,Note,-%3A%20If%20you%20put) によると、 `checked` が複数ある場合には最も後ろで宣言された `checked` が優先されます。

そのため、隠れている出力コンテナ用のタブが `checked` になっていたようです。

出力タブ側にデフォルトの `checked`がなくなってしまいますが、
それについては変換処理実行時、 `checked` を出力用のタブに付与すれば解決できそうです。

![tab-proto](https://github.com/Westen0511/Qiita-writing/blob/main/My-10-WebDevProjects/json-to-csv/tab-proto.png?raw=true)

切り替えタブはOK。

## CSSでスタイリング

### 色を設定

[こちらのサイト](https://saruwakakun.com/design/gallery/palette)から色を拝借。

```css
#4072B3 濃い青
#6088C6 普通の青
#AEC4E5 薄い青
#C0C0C0 灰色
```

### 入出力欄

タブ切り替えで表示される入/出力欄が中心に来てほしいので、
`flex` を利用して中心に寄せます。

```css
.content-container {
    display: none;
    height: 90%;
    width: 100%;
    /* 位置合わせ */
    align-items: center;
    justify-content: center;
    flex-direction: column;
    /* 配色 */
    background-color: #AEC4E5;
}

#input-json-tab:checked ~ #input-json-container,
#upload-json-tab:checked ~ #upload-json-container,
#output-csv-tab:checked ~ #output-csv-container,
#download-csv-tab:checked ~ #download-csv-container {
    display: flex;
}
```

### 丸数字表示

番号付きリストの数字をなんとなく丸数字にしてみたかったのでやってみました。

**参考**

- [【CSS】リストで①や②などの丸数字を使う方法 | でざなり](https://dezanari.com/css-list-enclosed-alphanumerics/)
- [CSS カウンターの使用 - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Counter_Styles/Using_CSS_counters)


```html
<ol>
	  <li>JSON文字列を入力 or JSONファイルをアップロードしてください。</li>
	  <li>CSV変換結果が表示されます。ダウンロードも可能です。</li>
</ol>
```

```css
/* 順序付きリスト */
ol {
    list-style-type: none;
    counter-reset: number;/* カウンターを初期化 */
}
li {
    position: relative;
}
  /* beforeでカウンターを作成 */
li::before {
    content: counter(number);
    counter-increment: number;
    padding: 0 0.2em;
}
  /* afterで○を作る */
li::after {
    content: '';
    /* 配置を調整 */
    display: block;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: 0;
    /* ○を作る */
    width: 1em;
    height: 1em;
    border: 1px solid #000;
    border-radius: 50%;
}
```

やっていること

- `::before` `::after` 、`content` プロパティを利用して要素に装飾的な内容を追加。
- **CSSカウンター**を使用。CSS が管理する変数のことで、 CSS のルールによって増加・現象させることが出来る。
- `top 50%` で親要素の中央に寄せ、`transform: translateY(-50%)` で子要素の高さの半分を引き戻す。
- `border-radius` で正方形を丸めて○を作る
- `counter-reset` でCSSカウンターを初期化(指定無しの場合0に)
- `counter-increment` でCSSカウンターをインクリメント(指定なしの場合1ずつ)
- `content: counter(カウンター名)` でカウンターを表示

MDNの例。

```css
body {
  counter-reset: section;                      /* 'section' という名前のカウンターを設定し、 0 で初期化する */
}

h3::before {
  counter-increment: section;                  /* section カウンターの値に 1 を加算 */
  content: "第 " counter(section) " 章: ";     /* '第 ' という語、 section カウンターの値、
                                                    ' 章' という語、コロンをそれぞれの
                                                    h3 の内容の前に表示 */
}
```


### フッター追加

フッターを追加して、Githubのリンクを追加してみます。

また、Githubリンクの前にアイコンを表示させたいです。
[DEVICON](https://devicon.dev/)というサイトを利用して、リンクの前にアイコンを表示させてみます。

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.14.0/devicon.min.css">

・・・

<footer>
		<i class="devicon-github-original"></i>
    <a href="https://github.com/Westen0511/My-10-Web-Dev-Projects" id="github-link">Github-link</a>
</footer>
```

`position: relative` を使って右寄せします。

```css
/* ------------------------------------------------------------------------ */
/* フッター */
/* ------------------------------------------------------------------------ */
.devicon-github-original,
.github-link {
    position: relative;
    left: 80%;
}
```

### 出来たもの

![styling-result](https://github.com/Westen0511/Qiita-writing/blob/main/My-10-WebDevProjects/json-to-csv/styling-result.png?raw=true)

かなりカクカクしてますが、とりあえずOKとします！

## JavaScript実装

### 必要な要素

- 「変換実行」を押したら処理実行、ページが更新される
- 文字入力/ファイルアップロードの読み取り
- CSVテーブル/ファイルダウンロードの出力
- JSON→CSV変換
- ファイル/文字列のどちらかが入力されていることを確認するバリデーション
    - どちらも入力されていなければ❎
    - どちらか入力されていれば⭕
    - どちらも入力されている場合も❎
- JSON→CSV変換

### 変換実行を押したら処理実行、ページが更新される

#### ロード画面

ロード画面が必要な気がするので、ロード画面を作っていきます。

**参考** : [Webページのローディング画面 - Qiita](https://qiita.com/tnakagawa/items/13246a6516b61f35d2f9)
色々なローディングパターンのサンプルコードがあって、勉強になりました。

とりあえずボタン要素を取得。

```js
const translateBtn = document.getElementById("translate-btn");
translateBtn.addEventListener("click", (e) => {
    console.log(e);
    // 変換処理開始(ローディングアニメーション表示)
    // 変換処理実行
    // 変換処理終了(ローディングアニメーション終了)
})
```

ローディング用の`div` を置いておきます。

```js
<div class="loading"></div>
```

CSSを設定します。

```css
.loading {
		/* デフォルトはhiddenに */
		visibility: hidden;
    /* 画面最大 */
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    /* 背景色（黒、不透明度80%） */
    background-color: #000000;
    opacity: 0.8;
    /* フレックスコンテナ（縦並べ、横中央、縦中央） */
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* 表示を一番上 */
    z-index: 999;
    /* 選択付加 */
    user-select: none;
}
```

`position: fixed`
要素の位置が固定される。

`user-select: none`
対象要素とその子孫要素は範囲選択できない。

`visibility`
[display:none と visibility:hidden の違い - Qiita](https://qiita.com/rico/items/0f645e84028d4fe00be6)

> `visibility:hidden`は名前の通り、要素はあるけど見えない状態。
> `display:none`は、要素も取得されず、完全にその場にない扱い。

`visibility` で実装してしまいますが、 `display` の方が良さげですね。

JavaScriptでロード用の関数を実装します。

```js
function load() {
    const loading = document.getElementById("conversion-loading");

    function startLoad() {
        loading.style.visibility = "visible";
    };
    function stopLoad() {
        loading.style.visibility = "hidden";
    }

    startLoad();
    setTimeout(stopLoad, 3000);
}

conversionBtn.addEventListener("click", (e) => {
    load()
})
```

`setTimeout` 3秒で試してみる。

![loading-test](https://user-images.githubusercontent.com/85564407/154787072-7b12a776-478a-46d4-8159-6c12a0eb689d.gif)

OK。

アニメーションを実装してみます。

```html
<div class="loading" id="conversion-loading">
    <div class="load-text load-blink">Loading...</div>
    <div class="load-circle"></div>
</div>
```

```css
.load-text {
    color: white;
    font-size: 16pt;
}

.load-circle {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    border: 10px solid #4072b3;
    border-top-color: white;
    animation: rotate 1s linear infinite;
}

@keyframes rotate {
    to {
        transform: rotate(360deg);
    }
}
```

`**border-top**`
要素上側の境界に色を付けている。
`border-top`で色が変わった四角形の角を丸めると、一部色が違う円ができる。

`**animation**`
展開すると以下のようになっている。
![animation-element](https://github.com/Westen0511/Qiita-writing/blob/main/My-10-WebDevProjects/json-to-csv/animation.png?raw=true)

- `**infinite**` 再生回数を無限に
- `**1s**` アニメーションの時間
- `**linear**` `timing-function` のキーワード値。アニメーションがどのように進行するかを設定。
- `**rotate**` `animation-name` を設定している。`@keyframes` でアニメーションを設定するために使われる。

`**@keyframes`**
360°回転させている。

(https://user-images.githubusercontent.com/85564407/154787918-ff28fd35-1d22-41e6-99a6-13bde4fe0eff.gif)

OK!!

#### 表示を出力に切り替え

```js
const outputContainer = document.getElementById("output-container");
const inputContainer = document.getElementById("input-container");
const defaultCheckedOutputTab = document.getElementById("output-csv-tab");
const tabs = document.querySelectorAll("input[name='tab']");

function stopLoad() {
    inputContainer.style.display = "none";
    outputContainer.style.display = "flex";

    for (const tab of tabs) {
        tab.checked = false
    }
    defaultCheckedOutputTab.checked = true;

    loading.style.visibility = "hidden";
};
```

- `input/output-container` の `display` を変更
- `tab` のチェックをすべて外す→デフォルトでチェックが付くタブのみチェック
- `loading` を隠す

`display`を手動で切り替える実装だと混乱しそうなので、`active` `inactive` クラスを作っておいて切り替える形にします。

どっちが良いのかは・・・謎。

```js
/** 要素の表示を切り替える */
function toggleDisplay(element) {
    if (element.classList.value === "active") {
        element.classList.remove("active");
        element.classList.add("inactive");
    } else {
        element.classList.remove("inactive");
        element.classList.add("active");
    }
}
```

### 入力の扱い

#### 文字入力の読み取り

`textarea` の`value` で取得します。

#### ファイルアップロード

**参考**

- [<input type="file"> - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/input/file)
- [ウェブアプリケーションからのファイルの使用 - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/File/Using_files_from_web_applications)
- [JavaScriptでファイルを読む Web.dev](https://web.dev/read-files/)
- [よくあるMIMEタイプ - MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types)

```html
<input id="input-json-file" type='file' accept="application/json">
```

`FileReader` を使います。

```jsx
function uploadFile() {
    const selectedFile = document.getElementById("input-json-file").files[0];
    const reader = new FileReader();

    reader.readAsText(selectedFile)
    reader.onload = () => console.log(reader.result)
}

/*
{
    "config": {
        "key": "value",
        "key2": "value2"
    }
}
*/
```

- `FileReader` をインスタンス化、 `readASText` メソッドでテキストとして読み込む。
- `FileReader` には `result` というプロパティがあり、読み取り結果がそこに保存される。
- `load` イベントでファイルのロード完了を待つことが出来る。

これで入力されたテキストの情報/アップロードされたファイルの情報を扱えるようになりました。

### バリデーション

- どちらも入力されていなければ❎
- どちらか入力されていれば⭕
- どちらも入力されている場合も❎

これらを実装するには、テキスト/JSONファイルを変数に入れ、条件判定する必要があります。

テキストは「実行」が押された時に取得すれば良いのですが、
ファイルの中身に関してはロードを挟む関係上、「実行」が押されてから変数に入れる形だと取得が間に合いません。

そこで、 `input` の `change` を待ち、グローバル変数にファイルロード結果を入れる形にしました。

```js
// ファイル読み込み結果
let readResult = ""

function validateInput() {
    const inputText = document.getElementById("input-json-text").value;

    if (inputText && readResult) {
        window.alert("入力はテキストかファイルのどちらかにしてください。")
        return false
    } else if (inputText) {
        return inputText
    } else if (readResult) {
        return readResult
    } else {
        window.alert("テキストかファイルを入力してください。")
        return false
    }
}

function readFile() {
    const reader = new FileReader();
    reader.readAsText(fileInput.files[0])
    reader.addEventListener("load", () => {
        readResult = reader.result;
    })
}
fileInput.addEventListener("change", readFile);
```

### JSON→CSV変換

参考 : [jsonをcsv(カンマ区切り、項目行あり)に変換する - Qiita](https://qiita.com/_shimizu/items/38e6d75afcacec25eb7e)

```jsx
function jsonToCsv(json) {
    const header = Object.keys(json[0]).join(',') + "\n";

    const body = json.map(function(d){
        return Object.keys(d).map(function(key) {
            return d[key];
        }).join(',');
    }).join("\n");

    return header + body;
}
```

やっていること

- `keys` で渡されたオブジェクトのキーを列挙、 `,` 区切りで結合、最後に改行
  - `[0]`指定をしているのでJSONファイルの形式によっては対応できませんが、良しとします。
- `map` を使い、キー取り出し→ `オブジェクト[キー]` で値取り出し→ `,` 区切りで結合


また、テキストはもちろん、JSONファイルからも入力を受け取った段階では文字列です。

そのため、`JSON.perse` を使ってオブジェクトに変換します。

```jsx
/** 変換処理実行 */
function executeJsonToCsv(input) {
    if (typeof(input) === "string") {
        return jsonToCsv(JSON.parse(input));
    } else {
        return jsonToCsv(input)
    }
}
```

![json-convert-csv](https://github.com/Westen0511/Qiita-writing/blob/main/My-10-WebDevProjects/json-to-csv/json-convert-csv.png?raw=true)

### CSV出力

**参考 :** [JavaScriptでcsvファイルを読み込んで表示 - Qiita](https://qiita.com/hiroyuki-n/items/5786c8fc84eb85944681)

出力は`table` として実装します。

```html
<table id="csv-output"></table>
```

まず、現在CSVデータは文字列なので配列に変換します。

```jsx
/** CSVを配列に変換する */
function csvConvertArray(csvString) {
    const csvArray = [];
    const csvStrings = csvString.split('\n');
    for (let i = 0; i < csvStrings.length; i++) {
        csvArray[i] = csvStrings[i].split(',');
    }
    return csvArray
}
```

次に、配列からテーブル要素を作成します。

列先頭は色を変えておきたいので、無理やりな形になりますが `thead` を挿入します。

ループの最初だけ特別な処理をしたい時、もう少しきれいに書く方法無いかな・・・

```jsx
function createTableContent(csvArray) {
    let tableContent = '';
    let isFirst = true;

    csvArray.forEach( (element) => {
        if (isFirst) tableContent += '<thead>';
        tableContent += '<tr>';

        element.forEach( (childElement) => {

            tableContent += `<td>${childElement}</td>`
        });

        tableContent += '</tr>';

        if (isFirst) {
            tableContent += '</thead>';
            isFirst = false;
        }
    });
    return tableContent;
}
```

(https://github.com/Westen0511/Qiita-writing/blob/main/My-10-WebDevProjects/json-to-csv/csv-table.png?raw=true)

### ファイルのダウンロード

**参考**

- [Webフロントエンドだけでファイルを読み書きしたい - zenn](https://zenn.dev/pirosuke/articles/web-file-io-without-backend)
- [JavaScriptでファイルダウンロード処理を実現する - Qiita](https://qiita.com/wadahiro/items/eb50ac6bbe2e18cf8813)

以下のような流れでダウンロード可能です。

> 1.リンクの[HTML5のdownload属性](https://developer.mozilla.org/ja/docs/Web/HTML/Element/a#Attributes)を使用してダウンロードファイル名を設定
> 2.[File APIのBlob](https://developer.mozilla.org/ja/docs/Web/API/Blob)を使用してデータを作成
> 3.`window.URL.createObjectURL`でBlobからURLを生成しそれをリンク先に設定
> [JavaScriptでファイルダウンロード処理を実現する - Qiita](https://qiita.com/wadahiro/items/eb50ac6bbe2e18cf8813)

```html
<a id="download" href="#" download="result.csv">CSVダウンロード</a>
```

```jsx
/** ダウンロード出来るようにする */
function makeCsvDownloadable(csvString) {
    // 日本語に対応させるため、BOMを付与する
    const bom = new Uint8Array([0xEF, 0xBB, 0xBF]);
    const blob = new Blob([bom, csvString], { "type": "text/csv" });
    document.getElementById("download").href = window.URL.createObjectURL(blob);
}
```

#### BOMとは

> **バイト順マーク**(バイトじゅんマーク、[英](https://ja.wikipedia.org/wiki/%E8%8B%B1%E8%AA%9E): byte order mark) あるいは**バイトオーダーマーク**とは、通称**BOM**（ボム）といわれる[Unicode](https://ja.wikipedia.org/wiki/Unicode)の[符号化形式](https://ja.wikipedia.org/wiki/%E6%96%87%E5%AD%97%E7%AC%A6%E5%8F%B7%E5%8C%96%E6%96%B9%E5%BC%8F)で符号化したテキストの先頭につける数バイトのデータのことである。このデータを元にUnicodeで符号化されていることおよび符号化の種類の判別に使用する。
> [バイト順マーク - Wikipedia](https://ja.wikipedia.org/wiki/%E3%83%90%E3%82%A4%E3%83%88%E9%A0%86%E3%83%9E%E3%83%BC%E3%82%AF)

今回( `[0xEF, 0xBB, 0xBF]` )の場合はUTF-8のようです。

「UTF-8のファイル」だと示すためにファイルの先頭にセットする場合には、これをUint8Arrayでバイナリデータとしてセットするようです。

[CSVファイルを読み込むときはBOM付きUTF-8に気をつける - ペパボテックブログ](https://tech.pepabo.com/2021/03/19/remove-the-bom-when-importing-csv/)　

こちらの記事のように先頭行が上手く読み込まれない、といった問題のもとになることもあるみたいです。

#### BLOBとは

> BLOBとは、データベースのフィールド定義などで用いられるデータ型の一つで、テキスト（文字列）や整数のように既存のデータ型としては用意されていない任意のバイナリデータを格納するためのもの。

> [BLOB（Binary Large OBject）とは - IT用語辞典 e-Words](https://e-words.jp/w/BLOB.html)

バイナリデータを表すオブジェクトで、イミュータブルです。

Web上でクライアント側のファイルにアクセス出来るFile APIでもこのBlobが利用されています。

**参考**

- [Blob - MDN web docs](https://developer.mozilla.org/ja/docs/Web/API/Blob)
- [File - MDN web docs](https://developer.mozilla.org/ja/docs/Web/API/File)
- [Blob - 現代のJavaScriptチュートリアル](https://ja.javascript.info/blob)

#### createObjectURL

[createObjectURL](https://developer.mozilla.org/ja/docs/Web/API/URL/createObjectURL)を使って、指定された FileやBlobなどのオブジェクトを参照することが出来るURLを発行します。

ブラウザを閉じるまではURLが有効です。
つまり、閉じるまではメモリを圧迫するようです。そのため、[URL.revokeObjectURL](https://developer.mozilla.org/ja/docs/Web/API/URL/revokeObjectURL)を使ってメモリを開放してあげる必要があるようです。

### リセットの実装

入力 → 出力のダウンロードが出来た後は、リセット出来たほうが良いですよね。

```jsx
reloadBtn.addEventListener("click", () => location.reload() )
```

リロード用のボタンを追加、 `location.reload` で画面をリロードすることでリセットします。
この方法で合っているんでしょうか。

## 完成形

[json-to-csv-demo](https://user-images.githubusercontent.com/85564407/154802776-56e76150-5a9e-4bc8-bb12-ecb37709e631.gif)

おーちゃんと動いてる！

## 学んだこと

- やっぱりとりあえず作ってみるのが1番良い
    - **やる前 :** HTML/CSSで何かを作る時、何から手を付けて良いのかわからずフリーズしてしまう。
    - **現在** : 今回触れた内容についてはそれなりに理解した。多少手を動かせるようになった。
- 必要だと思った機能でも実際必要無かったりする。
  - ローディングアニメーションは必要だろう、と勝手に思い込んで実装しましたが全く使いませんでした。
  - 今回は学習用なので問題ないですが、しっかり要件を定めておかないとこうなるんだな、というのを少し実感出来た気がします。
- CSSいろいろ
    - まだまだ奥が深い。
- 切り替え可能タブの実装
    - 次実装する時は `role="tab"` を使ってみる。
- ローディングアニメーションの実装
    - ~~機能してないけど~~
- ファイルのアップロード/ダウンロードの扱い