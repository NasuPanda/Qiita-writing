# 仮想キーボード

## 概要

下の動画を参考にして、画面上で操作出来る仮想キーボードを実装していく。

[https://www.youtube.com/watch?v=N3cq0BHDMOY](https://www.youtube.com/watch?v=N3cq0BHDMOY)

### 主な目的

- 仮想キーボードの作り方を学ぶ
- 仮想キーボードのように複雑なレイアウトをどのように実現するのか学ぶ
- コードの書き方を参考にする

### **完成イメージ**

[https://codepen.io/dcode-software/pen/KYYKxP](https://codepen.io/dcode-software/pen/KYYKxP)

### **必要な要素**

現時点で必要そうな要素を考えてみます。

- キーイベントに反応して値を出力
- キーイベントに反応してアニメーション

コレくらいしか思いつかないな・・・

# 仮想キーボード

## 概要

下の動画を参考にして、画面上で操作出来る仮想キーボードを実装していく。

[https://www.youtube.com/watch?v=N3cq0BHDMOY](https://www.youtube.com/watch?v=N3cq0BHDMOY)

### 主な目的

- 仮想キーボードの作り方を学ぶ
- 仮想キーボードのように複雑なレイアウトをどのように実現するのか学ぶ
- コードの書き方を参考にする

### **完成イメージ**

[https://codepen.io/dcode-software/pen/KYYKxP](https://codepen.io/dcode-software/pen/KYYKxP)

### **必要な要素**

現時点で必要そうな要素を考えてみます。

- キーイベントに反応して値を出力
- キーイベントに反応してアニメーション

コレくらいしか思いつかないな・・・

## HTML実装

早速実装していきます。

とりあえずHTMLを追加。

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> Virtual Keyboard HTML/CSS/JS</title>
    <link rel="stylesheet" href="assets/keyboard.css">
    <link rel="shortcut icon" href="assets/favicon.ico">
</head>

<body>
    <h1>Virtual Keyboard HTML/CSS/JS</h1>
    <h3>Features</h3>

    <ul>
        <li>Easy to integrate</li>
        <li>Responsive</li>
        <li>Vanilla JS( <strong>no libraries required!</strong> )</li>
    </ul>
    <textarea style="position: absolute; top: 130px; right: 30px; width: 300px;"></textarea>

</body>
</html>
```

`textarea` に対してインラインCSSを書き、スタイルを割り当てます。

特殊なキーの表現には[Google Material icon](https://google.github.io/material-design-icons/)を使っていくようです。

HTMLにリンクを追加して使えるようにします。

```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons"
      rel="stylesheet">
```

本来キーボード部分はJavaScriptで作りますが、今は存在しません。

CSS編集のために、ダミーのHTMLを作って行きます。

キーボードのコンテナと、キーボード用の `div` を作ります。

**VSCodeのHTMLファイル編集時、 `.keyboard__keys` と打つと自動的に `div class="keyboard__keys"` が生成されます。**

初めて知りました。

そして、その中にキーボード（ `button type="button"` ）を入れていきます。

```jsx
<div class="keyboard">
  <div class="keyboard__keys">
      <button type="button" class="keyboard__key">a</button>
  </div>
</div>
```

## CSS実装

### キーボードコンテナ

```css
.keyboard {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    padding: 5px 0;
    background-color: #53a6bb;
    box-shadow: 0 0 50px rgba(0, 0, 0, 0.5);
    user-select: none;
    transition: bottom 0.4s;
    height: 100px;
}
```

`position: fixed`

スクロールしてもキーボードが表示され続けるようにする。

`padding: 5px 0;`

[padding - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/padding)

一括指定。この場合は左右5px、上下0。

`background-color: #004134;`

背景色の指定。

`box-shadow: 0 0 50px rgba(0, 0, 0, 0.5);`

[box-shadow - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/box-shadow)

以下のような構文で使用します。

`blur-radius` は値が大きくなるほどぼかしが大きくなり、**影の面積が広く・色が薄く**なります。

```css
/* キーワード値 */
box-shadow: none;

/* offset-x | offset-y | color */
box-shadow: 60px -16px teal;

/* offset-x | offset-y | blur-radius | color */
box-shadow: 10px 5px 5px black;

/* offset-x | offset-y | blur-radius | spread-radius | color */
box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);

/* inset | offset-x | offset-y | color */
box-shadow: inset 5em 1em gold;

/* 複数の影はカンマで区切る */
box-shadow: 3px 3px red, -1em 0 0.4em olive;
```

`user-select: none;`

[user-select - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/user-select)

ユーザーのテキスト範囲選択を禁止します。

`transition: bottom 0.4s;`

キーボードが下から出てくるアニメーション。

### キーボードを隠す

`.keyboard--hidden` という名称のクラスを使う。

✅ BMV block element modifier　CSSのネーミング

```css
.keyboard--hidden {
    bottom: -100%;
}
```

`bottom: -100%` を使用、JSによりクラスを `add/remove` することで見える状態⇔見えない状態を切り替える。

### キー

#### キーのスタイル

キーそれぞれに対してスタイルを追加していきます。

キー全て。

```css
.keyboard__keys {
    text-align: center;
}
```

中心になるように。

それぞれのキーにスタイルを追加します。

```css
.keyboard__key {
    height: 45px;
    width: 6%;
    max-width: 90px;
    margin: 3px;
    border-radius: 4px;
    border: none;
    background: rgba(255, 255, 255, 0.2);
    color: #ffffff;
}
```

`width 6%` `max-width: 90px`

レスポンシブになるように。

また、モニターからはみ出さないように。

`border-radius: 4px;` `border: none;`

角を丸め、線を消す。

`background: rgba(255, 255, 255, 0.2)`

`.keyboard` で設定した**背景色よりも明るい色になるように**。

![keyboard-only-a.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d208391c-0424-46b0-86a3-fbb40428f6cb/keyboard-only-a.png)

更に追加します。

`font-size: 1.05rem`

ルートサイズより5％大きく

`outline: none`

✅　要調査

`inline-flex`

キーの中にアイコンを置くことがあり、それらを中央寄せしたいので。

✅　要調査

#### キーにアイコン表示

Google Material iconを使ってアイコンを置いてみます。

```html
<button type="button" class="keyboard__key">
    <i class="material-icons">backspace</i>
</button>
```

え？これだけ？という感じなのですが、

![keyoboard-backspace.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78c7a12b-3bb9-4439-aa87-f7a442825332/keyoboard-backspace.png)

ちゃんと追加出来てます。すごい。

ただ、見ての通りアイコンの方が若干ずれているので修正していきます。

```css
		・・・
		vertical-align: top;
    padding: 0;
    -webkit-tap-highlight-color: transparent;
}
```

- [vertical-align  | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/vertical-align)

> vertical-align は、2 つの場面で使用することができます。
> 

> 包含する行ボックスの中で、インライン要素のボックスの垂直方向の配置を決める場合。例えば、[テキストの行の中で画像の垂直位置を決める](https://developer.mozilla.org/ja/docs/Web/CSS/vertical-align#vertical_alignment_in_a_line_box)ために使用することができます。
> 

> [表のセルの内容](https://developer.mozilla.org/ja/docs/Web/CSS/vertical-align#vertical_alignment_in_a_table_cell)の垂直方向の配置を決める場合。
> 

> `vertical-align` はインライン要素、インラインブロック要素、表のセル要素だけに適用されることに注意してください。つまり、[ブロックレベル要素](https://developer.mozilla.org/ja/docs/Web/HTML/Block-level_elements)の垂直方向の配置には使用できません。
> 
- [webkit-tap-highlight-color](https://developer.mozilla.org/ja/docs/Web/CSS/-webkit-tap-highlight-color)

標準ではないプロパティです。

Firefox、Safariではサポートされていません。

> **`webkit-tap-highlight-color`** は CSS の標準外のプロパティで、リンクがタップされている間に表示される強調色を設定します。強調は、ユーザーがタップしたことが正常に認識されていることを示し、またどの要素がタップされているかを示します。
> 

> `webkit-tap-highlight-color: red;
-webkit-tap-highlight-color: transparent; /* 強調をなくす */`
> 

最後に、 `position: relative` を追加。

`ralative` は基本位置を基準として移動する。

capslockのアクティブ/非アクティブを示すライトのためらしい。 

`absolute` だと親からの位置になってしまって、上手く配置出来ないのだと思われる。 

#### キーがアクティブなとき

```css
.keyboard__key:active {
    background: rgba(255, 255, 255, 0.12);
}
```

若干暗くする。

#### 特殊なキー

- 若干幅のあるキー
- かなり幅のあるキー
- 色が暗いキー

用のCSSを追加します。

HTMLにアイコン、クラスを追加します。

✅　命名規則

```html
<button type="button" class="keyboard__key keyboard__key--wide">
    <i class="material-icons">backspace</i>
</button>
<button type="button" class="keyboard__key keyboard__key--extra-wide">
	  <i class="material-icons">space_bar</i>
</button>
```

```css
.keyboard__key--wide {
    width: 12%;
}

.keyboard__key--extra-wide {
    width: 36%;
    max-width: 500px;
}
```

`width` を変更します。

`.keyboard__key--extra-wide` ははみ出さないように`max-width` を指定します。

capslockのライトを実装します。

`keyboard__key--activatable` というクラスを持つcapslockキーを実装し、以下のスタイルを追加します。

```css
.keyboard__key--activatable::after {
    content: "";
    top: 10px;
    right: 10px;
    position: absolute;
    width: 8px;
    height: 8px;
    background: rgba(0, 0, 0, 0.4);
    border-radius: 50%;
}
```

絶対位置指定で親(キーボード)の右上に配置し、スタイルを与えます。

また、 `keyboard__key--active` を追加、ライトをアクティブにできるようにします。

```css
.keyboard__key--active::after {
    background : #08ff00;
}
```

暗いキーは以下のように実装。

```css
.keyboard__key--dark {
    background: rgba(0, 0, 0, 0.5);
}
```

## JavaScript実装

### Keyboardオブジェクト

```jsx
const Keyboard = {
    elements: {
        main: null,
        keysContainer: null,
        keys: []
    },

    eventHandlers: {
        oninput: null,
        onclose: null
    },

    properties: {
        // キーボードの入力
        value: "",
        capsLock: false
    }
};
```

キーボードを表すために必要な`Keyboard`オブジェクトを定義していきます。

 

`elements`

メイン要素(キーボード)、キーボードのコンテナ、それぞれのキー

`eventHandlers`

イベントハンドラー

`properties`

キーボードの入力値、capsLockのアクティブ状態

また、このオブジェクトは以下のメソッドを持ちます。

<aside>
✅ `_` から始まるメソッドはプライベートメソッドです。

</aside>

```jsx
init() {

},
_creatKeys() {

},
_triggerEvent(handlerName) {
    console.log("Event Triggered! Event Name:" + handlerName);
},
_toggleCapsLock() {
    console.log("Caps Lock Toggled!");
},
open(initialValue, oninput, onclose) {

},
close() {

}
```

`open`には`、initialVale` を渡します。

これは、 `textarea` に既に入力があった場合、その入力をスタート値にするためです。

### `init`

全てのDOMがロードされたときをトリガーに `init` を実行します。

✅ load との違いは？

[Window: DOMContentLoaded イベント - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/Window/DOMContentLoaded_event)

```jsx
// 全てのDOMがロードされた時
window.addEventListener("DONContentLoaded", function() {
    Keyboard.init();
})
```

```jsx
init() {
        // main要素を作成
        this.elements.main = document.createElement("div");
        this.elements.keysContainer = document.createElement("div");

        // main要素をセットアップ
        this.elements.main.classList.add("keyboard", "1keyboard--hidden");
        this.elements.keysContainer.classList.add("keyboard__keys");

        // DOMの追加
        this.elements.main.appendChild(this.elements.keysContainer);
        document.body.appendChild(this.elements.main);
    },
```

`elements` に生成したDOM要素を代入、 `document` に `appendChild` していく。

なるほど、オブジェクトに生成した要素を持たせる感じなんですね。

`keyboard--hidden` の頭に1をつけているのは、開発用(開発中は見えるようにしておく)だから。

こういった小技は勉強になりますね。

### `_createKeys`

`DocumentFlagment` を使ってHTML要素を追加していきます。

`DocumentFlagment` は仮想的なDOMツリーを生成するようなイメージで使います。

主に大量の要素を一気に追加したい時なんかに使います。

```jsx
_creatKeys() {
    const fragment = document.createDocumentFragment();
    const keyLayout = [
        "1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "backspace",
        "q", "w", "e", "r", "t", "y", "u", "i", "o", "p",
        "caps", "a", "s", "d", "f", "g", "h", "j", "k", "l", "enter",
        "done", "z", "x", "c", "v", "b", "n", "m", ",", ".", "?",
        "space"
    ];

    const createIconHTML = (icon_name) => {
        return `<i class="material-icons>${icon_name}</i>`
    }

    keyLayout.forEach(key => {
        const keyElement = document.createElement("button");
        const insertLineBreak = ["backspace", "p", "enter", "?"].indexOf(key) !==-1;

        // 属性/クラスを追加
        keyElement.setAttribute("type", "button");
        // 全てのキーに必要なクラス
        keyElement.classList.add("keyboard__key");

```

#### 列区切り

```jsx
const insertLineBreak = ["backspace", "p", "enter", "?"].indexOf(key) !==-1;

...

if(insertLineBreak) {
	fragment.appendChild(document.createElement("br"));
            }
```

キーボードの列区切りは`indexOf` を使って判定、 `<br>` タグで改行を入れることで表現します。

[String.prototype.indexOf() - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)

`indexOf` は見つからなければ `-1` を返すので、見つかった場合は `inserLineBreak` が `true` になります。

#### 特殊なキー

`switch-case` を使います。

```jsx
switch(key) {
    case "backspace":
        keyElement.classList.add("keyboard__key--wide");
        keyElement.innerHTML = createIconHTML("backspace");

        keyElement.addEventListener("click", () => {
            this.properties.value = this.properties.value.substring(0, this.properties.length - 1);
            this._triggerEvent("oninput");
        })
        break;

    case "caps":
        keyElement.classList.add("keyboard__key--wide", "keyboard__key--activatable");
        keyElement.innerHTML = createIconHTML("keyboard_capslock");

        keyElement.addEventListener("click", () => {
            this._toggleCapsLock();
            keyElement.classList.toggle("keyboard__key--active", this.properties.capsLock);
        })
        break;

    case "enter":
        keyElement.classList.add("keyboard__key--wide");
        keyElement.innerHTML = createIconHTML("keyboard_return");

        keyElement.addEventListener("click", () => {
            this.properties.value += "\n";
            this._triggerEvent("oninput");
        })
        break;

    case "space":
        keyElement.classList.add("keyboard__key--extra--wide");
        keyElement.innerHTML = createIconHTML("space_bar");

        keyElement.addEventListener("click", () => {
            this.properties.value += " ";
            this._triggerEvent("oninput");
        })
        break;

    case "done":
        keyElement.classList.add("keyboard__key--wide", "keyboard--dark");
        keyElement.innerHTML = createIconHTML("check_circle");

        keyElement.addEventListener("click", () => {
            this.close();
            this._triggerEvent("onclose");
        })
        break;
```

やっていることは単純で、

- 必要なクラスとアイコンを追加
    - アイコンの生成は専用の関数を作っておいて、それを利用します。
- クリックされた時の処理を登録

しているだけです。

#### backspace

`substring` を使って1文字削除しています。

##### caps

`toggle` を使ってアクティブにします。

[DOMTokenList.toggle](https://developer.mozilla.org/ja/docs/Web/API/DOMTokenList/toggle)は渡された `token` をリストから削除、 `false` を返します。

`token` が存在しなかった場合は、追加して `true` を返します。

##### done

入力終了を表すキーです。

`close` を呼びます。

#### 通常のキー

```jsx
	default:
	keyElement.textContent = key.toLowerCase();
	
	keyElement.addEventListener("click", () => {
		this.properties.value += this.properties.capsLock ? key.toUpperCase() : key.toLowerCase();
		this._triggerEvent("oninput");
	})
	break;
```

三項演算子を使って`capsLock` がアクティブなら大文字に、そうでなければ小文字にします。

これでキーボードが完成・・・

![innerHTML-miss.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a1e8e6a-a822-48ae-896d-06db2e87831f/innerHTML-miss.png)

あれ。

`innerHTML` だけ空で、 `createIcon` などの関数は正常に動いているように見えたのでそこそこ解決に時間がかかってしまいましたが、

```jsx
const createIconHTML = (icon_name) => {
    return `<i class="material-icons>${icon_name}</i>`;
}
```

`material-icons` の `”` が足りていないだけでした。

補完頼りはよくないですね・・・

その他クラス名を間違えていてスタイルが適用されていない箇所などあったので修正しました。

結果が以下です。

![innerHTML-ok.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/30c8b37e-ead8-4dc6-be85-db948a4b8aae/innerHTML-ok.png)

OKですね。

### capslockがONになったときの挙動

```jsx
this.elements.keys = this.elements.keysContainer.querySelectorAll(".keyboard__key");
```

`capslock` による制御で使うために、 `Keyboard.keys` に全てのキー要素を追加します。

通常のキーはアイコンを持たない→子要素を持たない

ことを利用して、表示を更新します。

```jsx
_toggleCapsLock() {
	  console.log("Caps Lock Toggled!");
	  this.properties.capsLock = !this.properties.capsLock;
	
	  for (const key of this.elements.keys) {
	      if(key.childElementCount === 0) {
	          key.textContent = this.properties.capsLock ? key.textContent.toUpperCase() : key.textContent.toLowerCase();
	      }
	  }
	}
```

三項演算子は今回のように**ある入力を元にして値がスイッチする場合**に便利そうですね。

### イベントの制御

```jsx
_triggerEvent(handlerName) {
        console.log("Event Triggered! Event Name:" + handlerName);

        if(typeof this.eventHandlers[handlerName] == "function") {
            this.eventHandlers[handlerName](this.properties.value);
        }
    },
```

`_triggerEvent` に渡された引数が `eventHandlers`  に存在する関数であれば、 現在の`value` を渡しつつ呼び出します。

`_triggerEvent` 関数は、入力キーの`click` イベントに登録されています。

```jsx
case "backspace":
    keyElement.classList.add("keyboard__key--wide");
    keyElement.innerHTML = createIconHTML("backspace");

    keyElement.addEventListener("click", () => {
        this.properties.value = this.properties.value.substring(0, this.properties.length - 1);
        this._triggerEvent("oninput");
    })
    break;
```

```jsx
open(initialValue, oninput, onclose) {
    this.properties.value = initialValue || "";
    this.eventHandlers.oninput = oninput;
    this.eventHandlers.onclose = onclose;
    this.elements.main.classList.remove("keyboard--hidden");
},

close() {
    this.value = "";
    this.eventHandlers.oninput = oninput;
    this.eventHandlers.onclose = onclose;
    this.elements.main.classList.add("keyboard--hidden")
}
```

`open` `close` にはキーボードがアクティブ/非アクティブになったときの処理が記述されています。

具体的には、 

- `value` のリセット
- `eventHandlers` のリセット
- `"keyboard--hidden"` クラスの制御

です。

```jsx
document.querySelectorAll(".use-keyboard-input").forEach(element => {
    element.addEventListener("focus", () => {
        this.open(element.value, currentValue => {
            element.value = currentValue;
        });
    });
})
```

最後に `textarea` の `focus` イベントに `open` を登録します。

`focus` された時、`open(initialValue, oninput, onclose`) に対して

- `element.value` (`initialValue`)
- 引数として渡された値を `element.value` に代入する関数

をそれぞれ渡しています。

無事完成です。

([https://user-images.githubusercontent.com/85564407/155619812-c50eadbd-991e-4e2e-8323-4877eaf20c90.gif](https://user-images.githubusercontent.com/85564407/155619812-c50eadbd-991e-4e2e-8323-4877eaf20c90.gif))

![virtual-keyboard-demo.gif](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4f8c778-d187-47bd-bc16-c7461163045a/virtual-keyboard-demo.gif)