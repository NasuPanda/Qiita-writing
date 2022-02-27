# Movie Seat Booking

## **概要**

映画の座席予約アプリ。

それぞれの映画には異なるチケット料金が設定されていて、席が選択されると料金が表示される。

### 主な目的

- 良い感じのレイアウト構築方法を学ぶ
- 状態に応じて変化するUIの構築を学ぶ
- ローカルストレージの操作を学ぶ

### **完成イメージ**

([https://user-images.githubusercontent.com/85564407/155833480-b370b29f-afe1-4ac7-baef-28b5614a87db.gif](https://user-images.githubusercontent.com/85564407/155833480-b370b29f-afe1-4ac7-baef-28b5614a87db.gif))

### ✅クラスのセレクタ

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

<aside>
✅ `seat` と `selected` を持つ要素が選択される

</aside>

```css
.seat:not(.occupied):hover {
    cursor: pointer;
    transform: scale(1.2);
}
```

`seat` の `occupied` を持たない要素が選択される

```css
/* showcaseでは無効 */
.showcase .seat:not(.occupied):hover {
    cursor: default;
    transform: scale(1);
}
```

<aside>
✅ `showcase` の子要素、かつ `seat` を持ち、 `occupied` を持たない要素が選択される

</aside>

### ✅ 席のスタイル

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

<aside>
✅ ただの四角 → 左右の上を丸めてシートっぽく→ `margin` で切り離す

</aside>

### ✅ 端2列を少し離す

![seat-child.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e426264-15e5-41f5-8876-85585ee06ede/seat-child.png)

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

### ✅ カーソルされた時に強調

```css
/* ------------------------------------------------------------------------ */
/* カーソルされた時に強調 */
/* ------------------------------------------------------------------------ */
.seat:not(.occupied):hover {
    cursor: pointer;
    transform: scale(1.2);
}
/* showcaseでは無効 */
.showcase .seat:not(.occupied):hover {
    cursor: default;
    transform: scale(1);
}
```

`transform` を利用する。

`showcase` では無効にしておく。

### ✅ スクリーンのスタイルを3D風に

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

回転、遠近なし

![screen-non-perspective.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2528a384-1f99-4a22-b251-7552ed220f82/screen-non-perspective.png)

あり
X軸を基準に若干傾き、3D風になっている。

![screen.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f7c2fed4-9d58-49f8-8a97-8d24f4a97f61/screen.png)

## JavaScript

### ✅ 数値型に変更するEasyな方法

```jsx
const ticketPrice = +movieSelect.value;
```

<aside>
✅ 代入するとき文字列の前に `+` を置くことで数値型に変換できる

</aside>

### ✅ シートにイベント追加

`seats` を `forEach` してイベントを追加していく・・・のかと思いきや、

`container` にイベントを追加する。

```jsx
container.addEventListener("click", (e) => {
    console.log(e.target)
})
```

<aside>
✅ 親要素で発火したクリックイベントに対して、 `event.target` とすることでクリックされた要素を取り出すことが出来る

</aside>