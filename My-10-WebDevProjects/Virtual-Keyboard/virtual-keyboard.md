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
    <link rel="stylesheet" href="assets/dcode.css">
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

[Google Material icon](https://google.github.io/material-design-icons/)を使っていくようです。

HTMLに以下を追加して使えるようにします。

```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons"
      rel="stylesheet">
```

本来キーボード部分はJavaScriptで作りますが、今は存在しません。

CSS編集のために、ダミーHTMLを作って行きます。

```html
<div class="keyboard">
    <div class="keyboard__keys">

    </div>
</div>
```

キーボードのコンテナと、キーボード用の `div` を作ります。

**VSCode上で `.keyboard__keys` と打つと自動的に `div class="keyboard__keys"` が生成されます。**

初めて知りました。

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

スクロールしてもキーボードが表示され続けるようにする

`padding: 5px 0;`

一括指定。この場合は左右5px、上下0。

`background-color: #004134;`

何気なく使っていた色指定ですが、D codeと言うらしいです。

`box-shadow: 0 0 50px rgba(0, 0, 0, 0.5);`

✅　要調査

`user-select: none;`

ユーザーが選択出来ないように

✅要調査

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

動画17分時点。