<!--
title: 【HTML/CSS】Udemyコースで学んだ良い感じなデザインの共通点をまとめてみる
-->

## この記事は何？

Udemyで[20 Web Projects With Vanilla JavaScript | Udemy](https://www.udemy.com/course/web-projects-with-vanilla-javascript/learn/lecture/17843004#overview)というコースを受講しました。
HTML/CSS/VanillaJSで良い感じなデザインのアプリを20個作っていく、フロントエンド初学者向けのコースです。

進めていく中で、デザインに**共通点が多い**事に気が付きました。

そこで、今後の自分の為に良い感じのデザインの共通点をまとめることにしました。

### 注意点

- 初心者向けの記事です。
  - そんなの常識やん、という内容が多々含まれる恐れがあります。
- 細心の注意を払ってはいますが、勘違い・ミスがあるかもしれません。見つけたらそっと指摘していただけると幸いです。
- 「この方法が最適解！」というわけではないです。

## 本題の前に

### VSCodeのTips

いくつか講座内で紹介されていたVSCodeのTipsを紹介します。

#### Auto Rename Tag

https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag

ペアになっているタグを自動でリネームしてくれる拡張機能です。
普通に便利。

#### Lite Server

https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer

VSCode限定というわけではありませんが、VSCodeなら簡単に拡張機能として利用可能なので紹介します。
**ファイルの変更を監視・ブラウザに反映してくれる**軽量なローカルWebサーバです。

- [BrowserSync](https://zenn.dev/yuki0410/articles/8ee3433cfa5b807968d0-2)をSPAに対応出来るようにしたラッパーです。
- HTML/CSS/JSファイルの変更を監視、変更されたら即ブラウザに反映してくれます。
- Liteというだけあって、ロードが超早いです。

拡張機能の検索欄で「Lite Server」と検索、インストールするだけで導入できます。

#### HTMLの入力

VSCodeでHTMLを書くときは下の表のように入力すると効率良く入力出来ます。

| 入力 | 結果 |
| --- | --- |
| .active | <div class="active"></div> |
| button.search-btn#submit | <div class="search-btn" id="submit"></div> |

### Google Fontの利用

[Browse Fonts - Google Fonts](https://fonts.google.com/)から好きなフォントを選んで導入します。

今回はCSSの`@import`により利用します。

```css
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@100&family=Roboto:wght@100&display=swap');
```

導入の参考になりそうな記事

- [Google Fonts を使ってみよう - Qiita](https://qiita.com/eimy9/items/2fdedf840cb551cc83c2)
- [Rails Googleフォント 使い方（初心者） - Qiita](https://qiita.com/iggy-neko/items/b20babb7bf7f5f61ce4e)

### Font Awesomeの利用

[Font Awesome](https://fontawesome.com/)から好きなアイコンを選んで導入します。

`head`に`link`を追加して利用出来るようにします。

```html
<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.10.2/css/all.min.css" rel="stylesheet">
```

下のように書くだけでアイコンが表示されます。

```html
<i class="fas fa-search"></i>
<i class="fas fa-random"></i>
```

導入の参考になりそうな記事

- [Font Awesomeの使い方 - Qiita](https://qiita.com/momo1010/items/0374fb7f0b1d465384b4)

### CSSセレクタ

基本的なセレクタについておさらいします。

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

```css
.seat.selected {
    background-color: #6feaf6;
}
```

`.seat` と `.selected` を持つ要素が選択される

```css
.seat:not(.occupied):hover {
    cursor: pointer;
    transform: scale(1.2);
}
```

`.seat` の内、 `.occupied` を持たない要素が選択される

```css
.showcase .seat:not(.occupied):hover {
    cursor: default;
    transform: scale(1);
}
```

`.showcase` の子要素、かつ `.seat` を持ち、 `.occupied` を持たない要素が選択される

## 本題

前置きが長くなりましたが、本題に入っていきます。

TODO サイト自体の画像を提示→この部分はこうなっている→共通点ここだね〜という感じにする


### 要素内に余白を作りたいときは`padding`を使う

`余白を作りたい時には`padding`を使います。
中にテキストを持つ要素はほとんど`padding`を使っていました。

✅padding.png

`padding`ありの方が圧倒的に良いですね。

### `border-radius`をよく使う

指定した長さを半径として、ブロックの四隅を丸くするプロパティです。

カクカクしたデザインは滅多に無いです。だいたい角を丸めます。

### 要素間を離したい時は`margin`

当然といえば当然ですが、要素サイズの大小に関わらず要素間の距離を開けたい時は`margin`を使います。

✅margin.png

### レイアウトの構成

人によるとは思いますが、この教材の場合`flex`の使用率が圧倒的でした。

レイアウト全体をいくつかの大きめな「ブロック」に分割して構成、`body`に``flex`を適用して中央寄せ。
という流れが多かったです。

この作り方はわかりやすくて好きです。

✅flex.png

### 1番上/下の要素は上/下に余白を作る

1番上/下にいる要素は上/下に`margin`を設定することで、不自然にならない程度の余白を作っていました。

### 開発の流れ

JavaScriptによるDOM操作でレイアウトを作る場合、以下の流れが共通していました。
「チュートリアルでやるような小規模なアプリケーションだとこの方がわかりやすい」という話かもしれませんが、実際この流れだと理解しやすかったです。

1. まずダミーHTML（JavaScriptで作る予定のレイアウト）を書く
2. ダミーHTMLに対してCSSを書いてスタイルを設定
3. 最後にJavaScriptを書き、DOM操作してレイアウトを作っていく

## 使えそうなデザイン

ここからは汎用性の高そうなデザイン達をまとめていきます。