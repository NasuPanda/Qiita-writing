　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　## はじめに

HTML/CSS/JavaScriptで10個(くらい)何かを作ってみるチャレンジの一環として、
お昼寝用BGM＆アラームツールを作っていきます。

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

### 参考

以下から面白そうなお題をいくつか参考にします。

- [ポートフォリオに役立つJavaScriptプロジェクト40選（動画あり） - Qiita](https://qiita.com/baby-degu/items/33acb94e404feaf58d35)
- [JavaScript 30](https://javascript30.com/)


***

このチャレンジのリポジトリ

https://github.com/NasuPands/My-10-Web-Dev-Projects

***

# Nap-Supporter

## 概要

指定した時間睡眠用BGMを流す→アラームで起こしてくれるツール。

### 主な目的

- 会社でのお昼寝を快適にする
- 音の扱いを学ぶ
- 静的なサイトをスマホから扱える状態にする方法（ホスティング）を学ぶ

### 完成イメージ

Keynoteで簡単なモックアップを作成しました。

([https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/mockup.png?raw=true](https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/%E2%AD%90.png?raw=true))

![mockup.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a15af042-69ec-4531-9c34-5ff58a418235/mockup.png)

ざっくりしたデザインについては、仕事中たまに使っていて、使いやすいと思っていた以下のサイトを参考にしました。

[【WEBツール】ポモドーロ・テクニックタイマー](https://www.oh-benri-tools.com/tools/time/pomodoro)

### 必要な要素

現時点で必要そうな要素を考えてみます。

- フリーの音源を使って自然音を指定した時間流せること
- 指定した時間が経過したらアラームで起こしてくれること
- 時間・音量・音源を選択出来ること
    - 音源:選択された要素をどう紐付ける？
- スマホから使えること

## 調査

### 使用する音源

自然音

[https://vsq.co.jp/plus/sound/category/environment/](https://vsq.co.jp/plus/sound/category/environment/)

アラーム

[https://otologic.jp/free/se/clock01.html](https://otologic.jp/free/se/clock01.html)

これらのサイトの音源を使わせていただきます。

### 音声の扱い

[`<audio>`](https://developer.mozilla.org/ja/docs/Web/HTML/Element/audio)を使えば良さそう。

```js
<audio
    controls
    src="/media/cc0-audio/t-rex-roar.mp3">
    Your browser does not support the
    <code>audio</code> element.
</audio>
```

`controls` でブラウザ規定のインターフェースが生成される。

指定しなかった場合、視覚的な出力は何も無い。

```html
<audio controls>
	<source src="viper.mp3" type="audio/mp3">
	<source src="viper.ogg" type="audio/ogg">
	<p>お使いのブラウザは HTML5 音声をサポートしていません。代わりに<a href="viper.mp3">音声へのリンク</a>があります。</p>
</audio>
```

- `source` に複数のファイルを指定する事ができる。その場合、最初に読み込みに成功したものが利用される。
- `audio` 要素内に配置したテキストは `source` 、 `src` がサポートしていない形式だったときに表示される。

### 音源・時間の選択

今回は音源の選択に[select](https://developer.mozilla.org/ja/docs/Web/HTML/Element/select)、時間の選択に [input type="range"](https://developer.mozilla.org/ja/docs/Web/HTML/Element/input/range)を使っていこうと思います。

その他の選択肢

- `aria-expanded` を使ってアコーディオンメニューを実装
- [オンラインタイマー・Webタイマー](https://timer.onlinealarmkur.com/ja/) のサイトのように、 時間の設定に`a` タグを使う

など。

#### `select`

下のコードはMDNのサンプルです。

`input` のように `label` と `select` を結びつけ、メニューの選択肢を `select` 内の `option` で定義します。

```html
<label for="pet-select">Choose a pet:</label>

<select name="pets" id="pet-select">
    <option value="">--Please choose an option--</option>
    <option value="dog">Dog</option>
		・・・
```

#### `<input type="range">`

以下のようにします。

`min` `max` `step` などが設定可能です。

```html
<input type="range" id="volume" name="volume"
       min="0" max="11">
<label for="volume">Volume</label>
```

#### 選択された要素と音源の紐付け

選択した要素⇔音源の紐付けはどうしたら良いんだろう？

と思い、いくつかサイトを覗いてみると、選択するようなリストに `data-value="alerm1.mp3"` といった記述がありました。

これは[カスタムデータ属性](https://developer.mozilla.org/ja/docs/Web/HTML/Global_attributes/data-*)と呼ばれる仕様で、JavaScriptで値を取得する時に便利なようです。

使ってみたいと思います。

参考

[カスタムデータ属性とは? - Qiita](https://qiita.com/k152744/items/c96fcf0141798bf48dd7)

### ホスティング

スマホから(インターネット経由で)Webアプリを使えるようにするには、ホスティングが必要になります。

Webサイト・Webサービスを公開するには、サーバを用意する必要があります。

自分でサーバを用意するのは難しいので**、一般的にはホスティングサービスが(レンタルサーバ)**利用されます。

代表的なホスティングサービス

参考 : [ホスティングサービスを比較してみた - Qiita](https://qiita.com/mei_9961/items/09b7d8ba7d54b020a081)

- [GitHub Pages](https://pages.github.com/)
    - 無料で独自ドメインを設定できる
    - ブランチへプッシュするだけで公開される
    - 動的なサイトには対応していない
- [Netlify](https://www.netlify.com/)
    - 少ないステップで静的サイトを公開できる。
    - 無料で使える機能が多い
    - フォーム機能など、部分的に動的な機能を使える
- [Heroku](https://jp.heroku.com/)
    - PaaS
    - デプロイが簡単
    - 拡張機能(アドオン)が豊富
- [AWS](https://aws.amazon.com/jp/)
    - プライベートクラウドやネットワークの設定レベルで多様な校正をカスタマイズできる
    - 多様な種類を揃えているため、サービスの選定及び設計ノウハウが必要
    

追加の登録や設定不要で利用出来るようなので、今回は**Github Pages**を利用したいと思います。

## HTML実装

まずは自力で出来るところまで。

```html
<header>
    <h1>Nap Supporter</h1>
    <p>あなたのお昼寝をサポートします。</p>
</header>
<main>
    <div id="timmer"></div>
    <div id="button-container">
        <button id="start-btn" class="highlight-btn">スタート</button>
        <button id="reset-btn" class="normal-btn">リセット</button>
        <button id="stop-btn" class="normal-btn">ストップ</button>
    </div>
</main>
<footer>
    <p>使用音源</p>
    <a href="https://vsq.co.jp/plus/sound/category/environment/">環境音 | フリー音源・効果音 | VSQ plus+</a>
    <a href="https://otologic.jp/free/se/clock01.html">フリー効果音:時計 | OtoLogic</a>
</footer>
```

### `Audio`

後から取得するために `id` を設定しておきます。

特に何も指定していないので `preload` され、画面には表示されません。

```html
<audio src="assets/Nature/fire.mp3" id="nature-fire"></audio>
<audio src="assets/Nature/insect.mp3 " id="nature-insect"></audio>
<audio src="assets/Nature/rain.mp3" id="nature-rain"></audio>
<audio src="assets/Nature/sea.mp3" id="nature-sea"></audio>
<audio src="assets/Nature/water.mp3" id="nature-water"></audio>
<audio src="assets/Nature/wave.mp3" id="nature-wave"></audio>
<audio src="assets/Nature/wind.mp3" id="nature-wind"></audio>
```

### `select`

カスタムデータ属性 `data-bgm` 、 `data-alarm` を設定しておきます。

```html
<label for="nature-bgm-select">好きな自然音を選択</label>
<select name="nature-bgm" id="nature-bgm-select">
    <option value="fire" data-bgm="nature-fire">焚き火の音</option>
    <option value="insect" data-bgm="nature-insect">虫の声</option>
    <option value="rain" data-bgm="nature-rain">雨の音</option>
    <option value="sea" data-bgm="nature-sea">海の音</option>
    <option value="water" data-bgm="nature-water">水の音</option>
    <option value="wave" data-bgm="nature-wave">波の音</option>
    <option value="wind" data-bgm="nature-wind">風の音</option>
</select>
```

### `input type=”range”`

```html
<p>お昼寝時間</p>
<label for="minutes">分</label>
<input type="range" name="minutes" id="minutes" min="0" max="59">
<label for="seconds">秒</label>
<input type="range" name="seconds" id="seconds" min="0" max="59">
```

他にも音量確認用のボタンなどを実装しました。

([https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/minimum-html.png?raw=true](https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/%E2%AD%90.png?raw=true))

これで、最低限のHTMLは実装出来ました。

## CSS実装

### `input type="range"`

**参考**

- [input type=range のスライダーのデザインをCSSでいい感じにする](https://zenn.dev/catnose99/articles/e087d03d03d21b)
- [input type=range タグをカスタマイズするために | g200kg Music & Software](https://www.g200kg.com/archives/2017/12/input-typerange.html)
- [appearance (-moz-appearance, -webkit-appearance) - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/appearance)

`input type="range"` に独自のスタイルを適用させたい場合、[appearance (-moz-appearance, -webkit-appearance)](https://developer.mozilla.org/ja/docs/Web/CSS/appearance)を `none` にする必要があります。

`appearance`は特定の要素だと`auto` が既定値になるプロパティで、 `auto` の場合ブラウザごとに標準的なUIが表示されます。

```css
-webkit-appearance: none;
-moz-appearance: none;
appearance: none;
```

上のようにして `none` にした後、独自のスタイルを設定していきます。

[https://www.g200kg.com/images/2017/20171230range3.png](https://www.g200kg.com/images/2017/20171230range3.png)

> [input type=range タグをカスタマイズするために | g200kg Music & Software](https://www.g200kg.com/archives/2017/12/input-typerange.html)　より
> 

また、上の画像のようにスライダーのツマミのスタイルを変更するためには `::webkit-slider-thimb` を `none` にします。

以上を踏まえて実装してみます。

```css
input[type="range"] {
    /* 独自のスタイルを適用させたい場合、appearanceをnoneにする */
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    cursor: pointer; /* カーソルを見やすく */
    height: 14px;

    background: #BFE9DB; /* バーの背景色 */
    border-radius: 10px; /* バー両端の丸み */
    border: solid 3px #dfefed; /* バー周囲の線 */
}

/* ツマミのスタイル */
input[type=range]::-webkit-slider-thumb{
    -webkit-appearance:none;
    background:#517d99;
    height:20px;
    width:20px;
    border-radius:50%;
}

.time-range {
    width: 80%;
}
```

Before

([https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/range-before.png?raw=true](https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/%E2%AD%90.png?raw=true))

After

([https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/range-after.png?raw=true](https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/%E2%AD%90.png?raw=true))

OKですね。

### レイアウトの調整

幅の調整や、 `flex` の適用など。

```css
label {
    text-align: right;
}

.container {
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-around;
}

/* ------------------------------------------------------------------------ */
/* BGM・アラーム */
/* ------------------------------------------------------------------------ */

select {
    width: 20%;
}

.sound-select-label {
    width: 15%;
}
.volume-select-label {
    width: 15%;
}
.volume-range {
    width: 30%;
}
.volume-check-btn {
    width: 15%;
    background-color: white;
    color: black;
}

#bgm-container,
#alarm-container {
    padding: 10px;
}
```

([https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/pc-layout.png?raw=true](https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/%E2%AD%90.png?raw=true))

一見するとOKなのですが、スマホの表示を見てみると・・・

([https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/smart-phone-layout.png?raw=true](https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/%E2%AD%90.png?raw=true))

だいぶ窮屈な感じになってしまっています。

音量/時間の調整は快適にできてほしいので、レスポンシブ対応していきます。

といってもやることはシンプルで、メディアクエリを使って幅をいじるだけです。

**参考**

[メディアクエリーの初心者向けガイド - ウェブ開発を学ぶ | MDN](https://developer.mozilla.org/ja/docs/Learn/CSS/CSS_layout/Media_queries)

```css
@media screen and (max-width: 480px) {
    #bgm-container,
    #alarm-container {
        flex-wrap: wrap;
    }
    select {
        width: 40%;
    }
    .sound-select-label {
        width: 40%;
        text-align: left;
    }
    .volume-select-label {
        width: 40%;
        padding-top: 10px;
    }
    .volume-range {
        width: 70%;
    }
    .volume-check-btn {
        width: 20%;
    }
}
```

([https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/responsive.png?raw=true](https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/%E2%AD%90.png?raw=true))

これで多少はスマホからも操作しやすくなりました。

## JavaScript実装

### スライダーから値取得

スライダーから値を取得することで色々と操作していくので、まずはスライダーから値を取得していきます。

スライダーでは [input](https://developer.mozilla.org/ja/docs/Web/API/HTMLElement/input_event) イベントと [change](https://developer.mozilla.org/ja/docs/Web/API/HTMLElement/change_event) イベントが発生します。

`input` は値が変更される度(=スライダーが動かされる度)に発生します。

`change` は値の変更が確定した時(=スライダーを離した時)に発生します。

ここでは `input` イベントを使います。

```js
const minutesSlider = document.getElementById("minutes")
const secondsSlider = document.getElementById("seconds")
const bgmVolumeSlider = document.getElementById("bgm-volume")
const alarmVolumeSlider = document.getElementById("alarm-volume")

function sliderChange() {
    console.log(this.value)
}

minutesSlider.addEventListener("input", sliderChange);
secondsSlider.addEventListener("input", sliderChange);
bgmVolumeSlider.addEventListener("input", sliderChange);
alarmVolumeSlider.addEventListener("input", sliderChange);
```

([https://user-images.githubusercontent.com/85564407/155032422-a48b773f-7b83-4884-93e9-0943951e7199.gif](https://user-images.githubusercontent.com/85564407/155032422-a48b773f-7b83-4884-93e9-0943951e7199.gif))

OKですね。

#### `input type="number"` の追加

スライダーだけでなく、数値の表示・入力欄がほしいです。

そのため、 [input type="number](https://developer.mozilla.org/ja/docs/Web/HTML/Element/input/number) を使っていきます。

```html
<div id="minutes-container" class="container">
    <label for="minutes-number"></label>
    <input type="number" name="minutes-number" min="0" max="60"
        value="30" class="time-number" id="minutes-number">
    <label for="minutes-range">分</label>
    <input type="range" name="minutes-range" min="0" max="60"
    value="30" id="minutes-range" class="time-range">
</div>
```

#### `input` range⇔numberの紐付け

`range` と `number` の対応関係が複数あるので、クラスか何かで表したいです。

`range` 用のクラス、 `number` 用のクラスをそれぞれ作っておいて互いに更新し合う、というのはよろしくない気がします。

そこで、対応関係のクラスを作ってみます。

```js
class CorrespondenceInputRangeNumber {
    constructor(inputRange, inputNumber) {
        this.inputRange = inputRange;
        this.inputNumber = inputNumber;

        // rangeとnumberの値を対応させる
        this.inputRange.addEventListener("input", () => {
            this.inputNumber.value = this.inputRange.value
        })
        this.inputNumber.addEventListener("input", () => {
            this.inputRange.value = this.inputNumber.value
        })
    }
}

const correspondenceMinutesInputs = new CorrespondenceInputRangeNumber(minutesInputRange, minutesInputNumber);
const correspondenceSecondsInputs = new CorrespondenceInputRangeNumber(secondsInputRange, secondsInputNumber);
```

([https://user-images.githubusercontent.com/85564407/155036219-46d4e47f-d4e9-41a2-aecd-7d2d69667a98.gif](https://user-images.githubusercontent.com/85564407/155036219-46d4e47f-d4e9-41a2-aecd-7d2d69667a98.gif))

OKですね。

### 入力された値を表示

`input` から入力された分/秒を表示していきます。

`innerHTML` をイベントで変更するようにしたいのですが、先程作った関係クラスのイベントにそのまま追加していくのは不味そうです。

また、今のままだと表示が「0」となってしまっています。

二桁で表示したいです。

そこで、 `range` `number` の関係はオブジェクトで表すことにしました。

```js
/** input⇔分タイマーの紐付け */
const correspondenceInputMinutesTimer = {
    "timer" : document.getElementById("timer-minutes"),
    "range" : document.getElementById("minutes-range"),
    "number" : document.getElementById("minutes-number")
}

/** input⇔秒タイマーの紐付け */
const correspondenceInputSecondsTimer = {
    "timer" : document.getElementById("timer-seconds"),
    "range" : document.getElementById("seconds-range"),
    "number" : document.getElementById("seconds-number")
}
```

若干無理矢理感が否めませんが、関数を使って秒タイマー、分タイマー共通のイベントを登録します。

`number` は入力欄に値が表示されるので、 `padStart` で0埋めしておきます。

```js
function correspondInputTimer(correspond) {
    // numberは値が表示されるため、0埋めしておく
    correspond.number.value = correspond.number.value.padStart(2, "0");
    correspond.timer.innerHTML = correspond.number.value;

    correspond.range.addEventListener("input", () => {
        // rangeの値を0埋めしてnumberに代入する
        correspond.number.value = correspond.range.value.padStart(2, "0");
        correspond.timer.innerHTML = correspond.range.value.padStart(2, "0");
    })

    correspond.number.addEventListener("input", () => {
        // rangeにはそのまま値を代入すればいい
        correspond.range.value = correspond.number.value;
        correspond.number.value = correspond.number.value.padStart(2, "0");
        correspond.timer.innerHTML = correspond.number.value
    })
}

correspondInputTimer(correspondenceInputMinutesTimer);
correspondInputTimer(correspondenceInputSecondsTimer);
```

([https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/result.png?raw=true](https://github.com/NasuPands/Qiita-writing/blob/main/My-10-WebDevProjects/Nap-Supporter/%E2%AD%90.png?raw=true))

#### padStart

参考 : [String.prototype.padStart() - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String/padStart)

構文は以下。

```js
str.padStart(targetLength [, padString])
```

文字列 `str` が指定した長さ `targetLength` に満たなければ、指定文字 `padString` で埋めます。

時間表示など、表示の桁合わせをしたい時に便利です。

### 音声ファイルの選択

**参考**

- [データ属性の使用 - ウェブ開発を学ぶ | MDN](https://developer.mozilla.org/ja/docs/Learn/HTML/Howto/Use_data_attributes)
- [javascript セレクトボックスで選択されたテキストデータを取得する | mebee](https://mebee.info/2020/09/11/post-18616/)
- [HTMLElement.dataset - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/HTMLElement/dataset)

```html
<label for="nature-bgm-select" class="sound-select-label">好きな自然音を選択</label>
<select name="nature-bgm" id="nature-bgm-select">
    <option value="fire" data-bgm="fire">焚き火の音</option>
    <option value="insect" data-bgm="insect">虫の声</option>
    <option value="rain" data-bgm="rain">雨の音</option>
    <option value="sea" data-bgm="sea">海の音</option>
    <option value="water" data-bgm="water">水の音</option>
    <option value="wave" data-bgm="wave">波の音</option>
    <option value="wind" data-bgm="wind">風の音</option>
</select>
```

HTMLに `select` を使用、カスタムデータ属性を指定したので、以下のように取り出します。

```js
let index = natureSelect.selectedIndex
console.log(natureSelect.options[index].dataset.bgm)

// > fire
```

変更が確定した時に取得出来ればいいので、 `change` イベントを使います。

```js
// ------------------------------------------
// 音の選択
// ------------------------------------------

const natureSelect = document.getElementById("nature-bgm-select");
const alarmSelect = document.getElementById("alarm-select");
let selectedBGM = "";
let selectedAlarm = "";

natureSelect.addEventListener("change", () => {
    let index = natureSelect.selectedIndex;
    selectedBGM = natureSelect.options[index].dataset.bgm;
})
alarmSelect.addEventListener("change", () => {
    let index = alarmSelect.selectedIndex;
    selectedAlarm = alarmSelect.options[index].dataset.bgm;
})
```

#### `dataset` 

> [値へのアクセス](https://developer.mozilla.org/ja/docs/Web/API/HTMLElement/dataset#%E5%80%A4%E3%81%B8%E3%81%AE%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9)
> 
> - 属性は dataset のオブジェクトプロパティのようにキャメルケース名 (キー) を使用して、 `element.dataset.keyname` のように設定したり読み取ったりすることができます。
> - 属性はブラケット構文を使用して、 `element.dataset['keyname']` のように設定したり読み取ったりすることもできます。
> - `[in` 演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/in)を使用して、特定の属性が存在するかどうかを確認できます。
> 
> [HTMLElement.dataset - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/HTMLElement/dataset) より
> 

### `audio` の取得

HTMLから対応する `audio` を取得していきます。

HTMLを以下のように書いたため、 `bgm-*` `alarm-*` という形で先程取得した `data-*` の値を指定すれば取得出来ます。

```html
<audio src="assets/Nature/fire.mp3" id="bgm-fire"></audio>
<audio src="assets/Nature/insect.mp3 " id="bgm-insect"></audio>
<audio src="assets/Nature/rain.mp3" id="bgm-rain"></audio>
<audio src="assets/Nature/sea.mp3" id="bgm-sea"></audio>
<audio src="assets/Nature/water.mp3" id="bgm-water"></audio>
<audio src="assets/Nature/wave.mp3" id="bgm-wave"></audio>
<audio src="assets/Nature/wind.mp3" id="bgm-wind"></audio>

<audio src="assets/Alarm/clock-1.mp3" id="alarm-clock-1"></audio>
<audio src="assets/Alarm/clock-2.mp3" id="alarm-clock-2"></audio>
<audio src="assets/Alarm/chicken.mp3" id="alarm-chicken"></audio>
<audio src="assets/Alarm/morning.mp3" id="alarm-morning"></audio>
```

```js
const selectedAudio = document.getElementById(`nature-${selectedBGM}`)
console.log(`bgm-${selectedBGM}`, selectedAudio)

// > bgm-fire <audio src="assets/Nature/fire.mp3" id="nature-fire"></audio>
```

### `audio` 制御 一定時間再生

**参考**

- [HTMLMediaElement - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/HTMLMediaElement)
- [HTMLAudioElement - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/HTMLAudioElement)

`HTMLAudioElement` には固有のプロパティ・メソッドはありません。 `HTMLMediaElement` を継承しています。 

BGM/アラームの音量チェックから実装していきます。

```js
function play(audio, volume) {
    audio.volume = volume;
    audio.play();
}

function pause(audio) {
    audio.pause();
    audio.currentTime = 0;
}

/** 一定時間再生する。 */
function playVolumeCheck(audioId) {
    const selectedAudio = document.getElementById(`${audioId}-${selectedSounds[audioId]}`)
    // 入力レンジが0〜100でボリュームは0〜1なので100で割る
    volume = document.getElementById(`${audioId}-volume`).value / 100;
    play(selectedAudio, volume);
    window.setTimeout(pause, 5000, selectedAudio);
}
```

[setTimeout()](https://developer.mozilla.org/ja/docs/Web/API/setTimeout)でそこそこつまづきました。

`setTimeout(関数, セットしたい時間, [関数に渡したい引数])` とすることで実行したい関数に引数を渡すことが出来ます。

また、再生したい `audio` には `alarm` と `bgm` の2種類があるので、

 `audioId` という変数を使って `audio` や `volume` をそれぞれ選択出来るようにしました。 

#### ボタン無効化

現状では 「BGM音量確認」→「アラーム音量確認」の同時押しが可能です。

`button` の `disabled` を利用して再生中はボタンを無効にします。

```js
// 音量チェック
const bgmCheck = document.getElementById("bgm-volume-check");
const alarmCheck = document.getElementById("alarm-volume-check");
const volumeCheckButtons = [bgmCheck, alarmCheck];

/** 再生する。 */
function play(audio, volume) {
    audio.volume = volume;
    audio.play();
}

/** 一定時間再生する。 */
function playVolumeCheck(audioId, buttons) {
    // 再生中はボタン操作が無効
    buttons.forEach(btn => {
        btn.disabled = true;
    });

    const selectedAudio = document.getElementById(`${audioId}-${selectedSounds[audioId]}`)
    // 入力レンジが0〜100でボリュームは0〜1なので100で割る
    const volume = document.getElementById(`${audioId}-volume`).value / 100;
    play(selectedAudio, volume);

    function pause(audio, buttons) {
        audio.pause();
        audio.currentTime = 0;
        buttons.forEach(btn => {
            btn.disabled = false;
        });
    }
    setTimeout(pause, 5000, selectedAudio, buttons);
}

bgmCheck.addEventListener('click', () => { playVolumeCheck("bgm", volumeCheckButtons) })
alarmCheck.addEventListener('click', () => { playVolumeCheck("alarm", volumeCheckButtons) })
```

### `audio` 制御 指定時間再生

スタート/ストップボタン、時間の取得、BGMの選択により

指定時間、指定した音声を再生します。

今更ですが、リセットボタンはどう考えても不要なので消します。

昼寝リセットとは一体・・・

#### タイマー更新

まず、タイマーの表示を時間の経過とともに更新出来るようにします。

```js
const start = function() {
    let min = correspondenceInputMinutesTimer.number.value
    let sec = correspondenceInputSecondsTimer.number.value
    const minTimer = correspondenceInputMinutesTimer.timer
    const secTimer = correspondenceInputSecondsTimer.timer

    const id = setInterval( () => {
        if (min == 0 && sec == 0) {
            clearInterval(id)
        } else if (sec == 0) {
            sec = 59;
            min -= 1;
            minTimer.textContent = String(min).padStart(2, "0");
            secTimer.textContent = String(sec).padStart(2, "0");
        } else {
            sec -= 1;
            secTimer.textContent = String(sec).padStart(2, "0");
        }
    }, 1000);
}

startBtn.addEventListener("click", start)
```

**発生した問題**

- 時間が `input` の初期値を参照してしまう

最初は以下のように、引数として `input` の値を渡していました。

```js
startBtn.addEventListener("click", start.bind(null,
                                        correspondenceInputMinutesTimer.number.value,
                                        correspondenceInputSecondsTimer.number.value,
                                        correspondenceInputMinutesTimer.timer,
                                        correspondenceInputSecondsTimer.timer
                                        ));
```

しかし、このようにしてしまうと

最初にコードが実行された時の `input` の状態= 時間指定が初期値

を参照してしまいます。

そのため、関数内で変数を定義する形に変更しました。

- HTML更新されない問題

ログを追ってみると値は更新されているのに、HTMLが更新されませんでした。

考えてみれば当然の話で、

 `sec -= 1` などの計算をした時に数値に変換される

→ `padStart` も使えないし、HTMLも更新されない。

`String` で文字列型に変換して対処しました。

また、ストップが押された時に `input` の値が更新されるようにします。

```js
/** タイマーの入力値をセットする */
function setTimerInputs(min, sec) {
    correspondenceInputMinutesTimer.number.value = String(min).padStart(2, "0");
    correspondenceInputMinutesTimer.range.value = min;
    correspondenceInputSecondsTimer.number.value = String(sec).padStart(2, "0");
    correspondenceInputSecondsTimer.range.value = sec;
}
```

#### 指定時間再生

音量チェックと指定時間再生で共通の処理をまとめていきます。

 `audio` を `play` `pause` する関数を作ります。

```js
/** audio要素をplayし、ボタンを無効化する */
function audioPlay(audio, volume) {
    audio.volume = volume;
    audio.loop = true;
    audio.play();
    elementsDisabledPlayback.forEach(btn => {
        btn.disabled = true;
    });
}

/** audio要素をpauseし、ボタンを有効化する */
function audioPause(audio) {
    audio.pause();
    audio.currentTime = 0;
    elementsDisabledPlayback.forEach( btn => btn.disabled = false );
}
```

短時間再生する関数を作ります。

```js
/** 一定時間再生する。 */
function audioPlayShort(audio, volume) {
    audioPlay(audio, volume);
    setTimeout(audioPause, 5000, audio);
}
```

`select` `input` (ボリュームの制御)の定義を変更します。

`bind` で `this` の参照先を固定しておきます。

```js
/** 選択された音声のHTML要素 */
const selectedSounds = {
    "bgm" : document.getElementById("bgm-fire"),
    "alarm" : document.getElementById("alarm-clock-1")
}

/** ボリュームの入力のHTML要素 */
const volumes = {
    "bgm" : document.getElementById("bgm-volume"),
    "alarm" : document.getElementById("alarm-volume")
}

/** 音声が選択された時 */
function selectSound(audioId) {
    // カスタムデータ属性の取得 element.options.index.dataset.key
    const dataValue = this.options[this.selectedIndex].dataset[audioId];
    selectedSounds[audioId] = document.getElementById(`${audioId}-${dataValue}`);
}

bgmSelect.addEventListener("change", selectSound.bind(bgmSelect, "bgm"));
alarmSelect.addEventListener("change", selectSound.bind(alarmSelect, "alarm"));
```

再生時無効にするHTML要素を追加します。

```js
/** 再生時無効にするHTML要素 */
const elementsDisabledPlayback = [
                                startBtn, bgmVolumeCheck, alarmVolumeCheck,
                                correspondenceInputMinutesTimer.range,
                                correspondenceInputMinutesTimer.number,
                                correspondenceInputSecondsTimer.range,
                                correspondenceInputSecondsTimer.number
															];
```

スタートボタンが押された時に `start` から再生・タイマー制御・停止を呼び出します。

```js
function start() {
    // 1. 初期化
    let min = correspondenceInputMinutesTimer.number.value
    let sec = correspondenceInputSecondsTimer.number.value
    const minTimer = correspondenceInputMinutesTimer.timer
    const secTimer = correspondenceInputSecondsTimer.timer
    isStopClick = false;

    /** 再生終了時の処理 */
    function finishPlay() {
        clearInterval(id);
        setTimerInputs(min, sec);
        audioPause(selectedSounds.bgm, elementsDisabledPlayback);
    }

    // 2. 音声を再生する
    audioPlay(selectedSounds.bgm, volumes.bgm.value/100);

    // 3. タイマーを制御しつつ再生
    const id = setInterval( () => {
        if (min == 0 && sec == 0) {
            // 終了 : タイマーで終了
            finishPlay();
            audioPlayShort(selectedSounds.alarm, volumes.alarm.value/100);
        } else if (isStopClick) {
            // 終了 : ストップボタンで終了(アラームは流れない)
            finishPlay();
        } else if (sec == 0) {
            sec = 59;
            min -= 1;
            minTimer.textContent = String(min).padStart(2, "0");
            secTimer.textContent = String(sec).padStart(2, "0");
        } else {
            sec -= 1;
            secTimer.textContent = String(sec).padStart(2, "0");
        }
    }, 1000);
}
```

### 機能追加・リファクタリング

#### `disabled` になった要素のスタイル

使えない要素がわかりやすいように、スタイルを追加します。

```css
input:disabled {
    background-color: #ccc;
}

input:disabled::-webkit-slider-thumb{
    background:#ccc;
}

button:disabled {
    background-color: #ccc;
}
```

そして、ストップボタンの強調/強調の除去を実装します。

```js
function start() {
    // 1. 初期化
    let min = correspondenceInputMinutesTimer.number.value
    let sec = correspondenceInputSecondsTimer.number.value
    const minTimer = correspondenceInputMinutesTimer.timer
    const secTimer = correspondenceInputSecondsTimer.timer
    stopBtn.classList.add("highlight-btn");
    isStopClick = false;
		・・・

startBtn.addEventListener("click", start)
stopBtn.addEventListener("click", () => {
    isStopClick = true
    stopBtn.classList.remove("highlight-btn")
} )
```

([https://user-images.githubusercontent.com/85564407/155314893-b197f8c9-f335-4540-a413-15196c0ce604.gif](https://user-images.githubusercontent.com/85564407/155314893-b197f8c9-f335-4540-a413-15196c0ce604.gif))

OKですね。

#### 音量チェック

音量チェックを実行する関数を書くと、以下のようになりました。

```js
/** 音量チェックを一定時間再生する。 */
function playVolumeCheck(audioId) {
    const selectedAudio = selectedSounds[audioId];
    const volume = volumes[audioId].value / 100;
    audioPlayShort(selectedAudio, volume);
}
```

この関数をイベントリスナーのコールバックに登録したいのですが、この関数は引数が必要です。

そこで、 `bind` を利用します。

`this` の設定が不要な場合は、

`this` には `null` を渡しておいて、関数に引数だけ渡す

という使い方ができます。

```js
bgmVolumeCheck.addEventListener('click', playVolumeCheck.bind(null, "bgm"))
alarmVolumeCheck.addEventListener('click', playVolumeCheck.bind(null, "alarm"))
```

#### `input` ⇔ タイマーの関係

`correspondInputTimer`を関係を表すオブジェクトのメソッドにします。

そして、スプレッド構文で展開しつつプロパティを書き換えることでコピーします。

元となるオブジェクトを作ってそれぞれコピーした方が良いとは思いますが、今回はオブジェクトが2つしかないので・・・

```js
/** input⇔分タイマーの対応 */
const correspondenceInputMinutesTimer = {
    "timer" : document.getElementById("timer-minutes"),
    "range" : document.getElementById("minutes-range"),
    "number" : document.getElementById("minutes-number"),
    /** input ⇔ timerを紐付ける */
    correspondInputTimer() {
        // numberは値が表示されるため、0埋めしておく
        this.number.value = this.number.value.padStart(2, "0");
        this.timer.textContent = this.number.value;

        this.range.addEventListener("input", () => {
            // rangeの値を0埋めしてnumberに代入する
            this.number.value = this.range.value.padStart(2, "0");
            this.timer.textContent = this.range.value.padStart(2, "0");
        })
        this.number.addEventListener("input", () => {
            // rangeにはそのまま値を代入すればいい
            this.range.value = this.number.value;
            this.number.value = this.number.value.padStart(2, "0");
            this.timer.textContent = this.number.value
        })
    }
}
/** input⇔秒タイマーの対応 */
const correspondenceInputSecondsTimer = {
    ...correspondenceInputMinutesTimer,
    "timer" : document.getElementById("timer-seconds"),
    "range" : document.getElementById("seconds-range"),
    "number" : document.getElementById("seconds-number"),
}
```

他にも色々とリファクタリングして、最終的に以下のようになりました。

```js
/** 選択された音声のHTML要素 */
const selectedSounds = {
    "bgm" : document.getElementById("bgm-fire"),
    "alarm" : document.getElementById("alarm-clock-1")
}
/** ボリュームの入力のHTML要素 */
const volumes = {
    "bgm" : document.getElementById("bgm-volume"),
    "alarm" : document.getElementById("alarm-volume")
}

/** input⇔分タイマーの対応 */
const correspondenceInputMinutesTimer = {
    "timer" : document.getElementById("timer-minutes"),
    "range" : document.getElementById("minutes-range"),
    "number" : document.getElementById("minutes-number"),
    /** input ⇔ timerを紐付ける */
    correspondInputTimer() {
        // numberは値が表示されるため、0埋めしておく
        this.number.value = this.number.value.padStart(2, "0");
        this.timer.textContent = this.number.value;

        this.range.addEventListener("input", () => {
            // rangeの値を0埋めしてnumberに代入する
            this.number.value = this.range.value.padStart(2, "0");
            this.timer.textContent = this.range.value.padStart(2, "0");
        })
        this.number.addEventListener("input", () => {
            // rangeにはそのまま値を代入すればいい
            this.range.value = this.number.value;
            this.number.value = this.number.value.padStart(2, "0");
            this.timer.textContent = this.number.value
        })
    }
}
/** input⇔秒タイマーの対応 */
const correspondenceInputSecondsTimer = {
    ...correspondenceInputMinutesTimer,
    "timer" : document.getElementById("timer-seconds"),
    "range" : document.getElementById("seconds-range"),
    "number" : document.getElementById("seconds-number"),
}

const bgmSelect = document.getElementById("bgm-select");
const alarmSelect = document.getElementById("alarm-select");

const startBtn = document.getElementById("start-btn");
const stopBtn = document.getElementById("stop-btn");
const bgmVolumeCheck = document.getElementById("bgm-volume-check");
const alarmVolumeCheck = document.getElementById("alarm-volume-check");

/** 再生時無効にするHTML要素 */
const elementsDisabledPlayback = [
                                startBtn, bgmVolumeCheck, alarmVolumeCheck,
                                correspondenceInputMinutesTimer.range,
                                correspondenceInputMinutesTimer.number,
                                correspondenceInputSecondsTimer.range,
                                correspondenceInputSecondsTimer.number
                            ];

let isStopClick = false;

/** 音声が選択された時 */
function selectSound(audioId) {
    // カスタムデータ属性の取得 element.options.index.dataset.key
    const dataValue = this.options[this.selectedIndex].dataset[audioId];
    selectedSounds[audioId] = document.getElementById(`${audioId}-${dataValue}`);
}

/** audio要素をplayし、ボタンを無効化する */
function audioPlay(audio, volume) {
    audio.volume = volume;
    audio.loop = true;
    audio.play();
    elementsDisabledPlayback.forEach(btn => {
        btn.disabled = true;
    });
}

/** audio要素をpauseし、ボタンを有効化する */
function audioPause(audio) {
    audio.pause();
    audio.currentTime = 0;
    elementsDisabledPlayback.forEach( btn => btn.disabled = false );
}

/** 一定時間再生する。 */
function audioPlayShort(audio, volume) {
    audioPlay(audio, volume);
    setTimeout(audioPause, 5000, audio);
}

/** 音量チェックを一定時間再生する。 */
function playVolumeCheck(audioId) {
    const selectedAudio = selectedSounds[audioId];
    const volume = volumes[audioId].value / 100;
    audioPlayShort(selectedAudio, volume);
}

/** タイマーの入力値をセットする */
function setTimerInputs(min, sec) {
    correspondenceInputMinutesTimer.number.value = String(min).padStart(2, "0");
    correspondenceInputMinutesTimer.range.value = min;
    correspondenceInputSecondsTimer.number.value = String(sec).padStart(2, "0");
    correspondenceInputSecondsTimer.range.value = sec;
}

function start() {
    // 1. 初期化
    let min = correspondenceInputMinutesTimer.number.value
    let sec = correspondenceInputSecondsTimer.number.value
    const minTimer = correspondenceInputMinutesTimer.timer
    const secTimer = correspondenceInputSecondsTimer.timer
    isStopClick = false;

    /** 再生終了時の処理 */
    function finishPlay() {
        clearInterval(id);
        setTimerInputs(min, sec);
        audioPause(selectedSounds.bgm, elementsDisabledPlayback);
    }

    // 2. 音声を再生する
    audioPlay(selectedSounds.bgm, volumes.bgm.value/100);

    // 3. タイマーを制御しつつ再生
    const id = setInterval( () => {
        if (min == 0 && sec == 0) {
            // 終了 : タイマーで終了
            finishPlay();
            audioPlayShort(selectedSounds.alarm, volumes.alarm.value/100);
        } else if (isStopClick) {
            // 終了 : ストップボタンで終了(アラームは流れない)
            finishPlay();
        } else if (sec == 0) {
            sec = 59;
            min -= 1;
            minTimer.textContent = String(min).padStart(2, "0");
            secTimer.textContent = String(sec).padStart(2, "0");
        } else {
            sec -= 1;
            secTimer.textContent = String(sec).padStart(2, "0");
        }
    }, 1000);
}

correspondenceInputMinutesTimer.correspondInputTimer()
correspondenceInputSecondsTimer.correspondInputTimer()

// bindでthisの参照をselect要素にする
bgmSelect.addEventListener("change", selectSound.bind(bgmSelect, "bgm"));
alarmSelect.addEventListener("change", selectSound.bind(alarmSelect, "alarm"));
// thisが不要の場合はbindにnullを渡す
bgmVolumeCheck.addEventListener('click', playVolumeCheck.bind(null, "bgm"))
alarmVolumeCheck.addEventListener('click', playVolumeCheck.bind(null, "alarm"))

startBtn.addEventListener("click", start)
stopBtn.addEventListener("click", () => isStopClick = true )
```

## Github Pages

Github Pagesを使ってホスティングします。

1. Githubのリポジトリを用意
2. Setting → GithubPages → 「Check it out here！」→ ブランチ・フォルダを選択 → 「Save」
3. しばらく待つ

出来ました！超簡単ですね。

[https://NasuPands.github.io/Nap-Supporter/](https://NasuPands.github.io/Nap-Supporter/)

## 学んだこと

- 仕様が固まっていない段階からきれいに書くのは難しい
    - 記事では実装の流れをある程度整えて書いていますが、実際は「あ、ここ重複してる」「ん？こここうした方が良くない？」という感じで実装中に無駄に気づく→修正という流れが多かったです。
    - 実装しながらリファクタリングしてしまうと、どこをいじっていたのかわからなくなりそう。リファクタリングのタイミングも考えたほうが良い。
- どう実装したか、すぐ忘れる
    - 実装時にあまりメモを取らずに進めたのですが、最初はどのように実装していて、どうリファクタリングしたから今の形になったのか、曖昧な箇所が多い印象です。
    - これで困るのは記事を書く時くらいですが、ちょっとした問題でも「どんな問題があって、どう解決したのか？」くらいは残しておくべきだと思いました。
    - ~~Gitのログを追えばいいだけの話なのですが、面倒でした。~~
- まだまだ実装に必要な要素の考慮漏れが多い
- 実装面
    - レスポンシブ対応(さわり程度)
    - `audio` 要素
    - `select` 要素
    - カスタムデータ属性
    - スライダーの実装
    - タイマーの実装
    - `bind`
    - Github Pagesの利用