<!--
title:   MicrosoftのWeb開発教材を使ってみた ③テラリウム構築  【HTML・CSS基礎/DOM操作/クロージャ】
tags:    CSS,HTML,JavaScript,初心者向け
id:      59b8e43d8d6fb609c7d5
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
**③テラリウム構築 【HTML・CSS基礎/DOM操作/クロージャ】　本記事**
[④タイピングゲーム 【JavaScriptのイベント処理】](2022-02-09_JavaScript_340f391ee9f167bf4333.md)
[⑤-1ブラウザ拡張機能 【ブラウザの仕組み/拡張機能作成の導入】](2022-02-10_Web_d0189565d039c2c11383.md)
⑤-2ブラウザ拡張機能 【API/LocalStorage/BackGround/Performance】
⑥スペースシューティングゲーム【JavaScriptによるゲーム開発の基礎】
⑦架空銀行プロジェクト【ログイン/データ管理/状態管理】

***

### 記事の目的

- 学習のアウトプット
- 教材を使ってみたところかなり良かったので、その紹介

### 注意点

自身の学習のアウトプットがメインなので、理解できているところ(他言語と共通の箇所など)は省いています。
また、課題やtipsについても結構省きます。
この教材に興味を持った方はぜひご自分で取り組んでみてください。

# 3-Terrarium

https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/3-terrarium

ドラッグ＆ドロップで操作可能な[テラリウム](https://ja.wikipedia.org/wiki/%E3%83%86%E3%83%A9%E3%83%AA%E3%82%A6%E3%83%A0)を作っていきます。

### 学習の目的

- レイアウトの構築を中心に、テラリウムを作成するための HTMLを構築する。
- レスポンシブ対応などCSSの基本を中心に、オンラインテラリウムのスタイルを整えるCSSを構築する。
- テラリウムをドラッグ＆ドロップのインターフェイスとして機能させるための JavaScriptを構築する。

![https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/3-terrarium/images/screenshot_gray.png](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/3-terrarium/images/screenshot_gray.png)

> 完成イメージ https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/3-terrarium より
> 

## HTML入門

HTMLの基礎について学んでいきます。

Webページをスケルトンだとすると、HTML/CSS/JavaScriptはそれぞれ以下のようになります。

- HTMLは骨格
- CSSはおしゃれ
- JavaScript は命を吹き込む(動かす)

この例えわかりやすいですね。

### 基本的なHTML

1. `<!DOCTYPE html>` を最初に入れる
2. `<html>` の開き/閉じタグで全体を挟む
3. `<head>` に[metadate](https://developer.mozilla.org/ja/docs/Web/HTML/Element/meta)(Webページそのものの情報)を書く
    
    `html
    <head>
        <title>Welcome to my Virtual Terrarium</title>
        <meta charset="utf-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
    </head>
    `
    - `charset` で文字エンコーディング
    - IE=edge ブラウザがサポートされていることを示す`x-ua-compatible`などのブラウザ情報
    - `viewport`の設定
        - 仮想的な**表示領域**のこと。
        - `initial-scale` 最初にロードされたときのズーム倍率。
        - `content` viewpostのサイズ。特定の値や`device-width`を指定する。
        - 参考記事
            - [Using the viewport meta tag to control layout on mobile browsers - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag)
            - [もう逃げない。HTMLのviewportをちゃんと理解する - Qiita](https://qiita.com/ryounagaoka/items/045b2808a5ed43f96607)
4. `<body>` にHTML要素を書いていく。
    - それぞれのタグは通常`<p>Hello</p>`のように、開閉タグがある。
    - 閉じタグが不要な要素の代表例に `<img>` がある。
    例 : `<img class="plant" alt="plant" src="/images/hoge.png"`
        - これはブラウザが画像を表示するのに `src` 以外の情報を必要としないから。
        - `alt` には画像の内容を示す適切な情報を含める。
    - 装飾用のタグとして主に使われるのは `<div>` と`<span>`
        - `<div>` はブロック要素
        - `<span>` はインライン要素
        - ざっくり言うとブロックは改行あり、インラインは改行なしの要素
5. セマンティックなHTMLを書く
    - [セマンティクス - MDN](https://developer.mozilla.org/ja/docs/Glossary/Semantics)
    - タイトルテキストは`<h1>`、ヘッダーには`<header>`など、適切なHTML要素を使う。

### 非推奨のHTML

[このリスト](https://developer.mozilla.org/ja/docs/Web/HTML/Element#obsolete_and_deprecated_elements)に非推奨のHTMLが載っています。これらは使うべきではないそうです。

ですが、そもそもなぜ非推奨になるのでしょうか？少し調べてみました。
[Why Do Some HTML Elements Become Deprecated?](https://css-tricks.com/why-do-some-html-elements-become-deprecated/)

- HTMLで構造を書くこと/CSSでスタイルを書くことが分離されてきたことで、それらがひとまとめになったようなHTMLは廃止されてきた。
- CSS普及以前はテーブルを使ったレイアウトがよく使われていたが、アクセシビリティ、パフォーマンス、入れ子関係が複雑になりやすいなどの理由から使われなくなった。
    - 弊社の出退勤管理システム(結構古め)を見てみたら確かにテーブルレイアウトでした。~~そもそも使いにくいから更新してほしい~~

### 副教材

- [MicrosoftLearn](https://docs.microsoft.com/ja-jp/learn/modules/build-simple-website/?WT.mc_id=academic-13441-cxa)でHTML、CSSについて学ぶ

## CSS入門

**CSS**は、以下のような役割を持つ。

- Webサイトの見栄えを良くする
- レスポンシブウェブデザインを作成する
- アニメーションをつける

### 基本

```css
ul {
	font-family: helvetica;
}
```

- `ul` : セレクタ
    - **タグ** `ul` `body`のようにタグ名を書く。
    - **id** `#`から始め、IDを書く。`id`は固有の値。
    - **class** `.`から始め、クラス名を書く。
- font-family : プロパティ
    - スタイリングの対象
- helvetica : 値
    - どのようにスタイリングするか指定する
- CSSの読み込み
    - HTMLの`<head>`に `<link rel="stylesheet" href="./style.css">`を含める。
    - HTMLファイルに直接CSSを書く事もでき、その場合外部のCSSを読み込むよりも優先度が高い。

### 継承

```html
<body>
	<h1></h1>
</body>
```

上のような場合を考えると、

- `<h1>`セレクタでスタイルを指定しなかった場合、`<h1>`は`<body>`のスタイルを継承する。
- `<h1>`で指定した場合は`<h1>`のスタイルが優先される。

要するに、より具体的な指定が優先される。
スタイルが「カスケード」するという考え方。

[カスケード - IT用語辞典](https://e-words.jp/w/%E3%82%AB%E3%82%B9%E3%82%B1%E3%83%BC%E3%83%89.html#:~:text=%E3%82%AB%E3%82%B9%E3%82%B1%E3%83%BC%E3%83%89%E3%81%A8%E3%81%AF%E3%80%81%E4%BD%95%E6%AE%B5,%E3%81%8C%E7%94%9F%E3%81%98%E3%82%8B%E6%A7%98%E5%AD%90%E3%82%92%E8%A1%A8%E3%81%99%E3%80%82)

### 今回使うプロパティ

- `width`, `height`
    - タグの高さ、幅の指定
- `right`/`left`, `bottom`/`top`
    - 右/左、下/上からの距離
    - 絶対位置指定の場合は親から、相対の場合は初期位置からの移動

### 絶対位置と相対位置

- 絶対位置指定
    - 最も近い親からの相対的位置に配置される
    - 親がいない場合文書全体を基準として配置される
- 相対位置指定
    - CSSの指示に従い、初期位置から移動

**例1 `.plant` / `.plant-holder`**

```html
	<div id="right-container" class="container">
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant8" src="./images/plant8.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant9" src="./images/plant9.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant10" src="./images/plant10.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant11" src="./images/plant11.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant12" src="./images/plant12.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant13" src="./images/plant13.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant14" src="./images/plant14.png" />
		</div>
	</div>
```

`.plant`に相対、 `.plant-holder`に絶対位置指定
→ `HTML` > `.plant_holder` > `.plant` という構成なので、.plant-holderがHTMLに対する絶対位置に固まってしまう。

![https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/f2e27677-308d-ceb1-9707-e0189b948a28.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/f2e27677-308d-ceb1-9707-e0189b948a28.png)

`.plant`に絶対、 `.plant-holder`に相対位置指定
→ `.plant_holder`が相対的に配置され、その中に `.plant`が絶対位置で配置される。

![https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/6f9d43d2-1a5a-c505-d384-849c41462685.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/6f9d43d2-1a5a-c505-d384-849c41462685.png)

### チャレンジ 反射光の実装

`div`タグにスタイルを指定する形で実装します。

```html
<!-- テラリウム -->
<div id="terrarium">
    <div class="jar-top"></div>
    <div class="jar-walls">
        <!-- 追加箇所 -->
        <div class="jar-glossy-long"></div>
        <div class="jar-glossy-short"></div>
    </div>
    <div class="dirt"></div>
    <div class="jar-bottom"></div>
</div>
```

`css
.jar-glossy-long {
    /* 幅と高さ */
    width: 3%;
    height: 30%;
    /* 色と透明度 */
    background: rgb(224, 255, 255);
		opacity: 0.7;
    /* ポジションは親に対する絶対位置にしておく */
    position: absolute;
    /* 左から、下からの距離 */
    left: 10%;
    bottom: 20%;
    /* 角を丸める */
    border-radius: 1rem;
}
`

![https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/3-terrarium/2-intro-to-css/images/terrarium-final.png](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/3-terrarium/2-intro-to-css/images/terrarium-final.png)

OK？

### 副教材

https://codepip.com/games/

こちらの教材の[Flexbox Froggy](https://flexboxfroggy.com/)と[Grid Garden](https://codepip.com/games/grid-garden/)（無料）が紹介されていました。
超わかりやすいのでオススメです。

### Flex Box

flexboxを利用することでブロック要素を柔軟に並び替えることが出来る。

- 最初に並び替えたいブロック要素の**親要素**に`display: flex`を指定する。
- そこから実現したい操作に応じてプロパティを指定していく。

https://flexboxfroggy.com/#ja

#### `justify-content`

アイテムを**主軸方向**に並べる。

- **`flex-start`**: アイテムはコンテナーの左側に並びます。
- **`flex-end`**: アイテムはコンテナーの右側に並びます。
- **`center`**: アイテムはコンテナーの中央に並びます。
- **`space-between`**: アイテムはその**間に**等しい間隔を空けて表示されます。
- **`space-around`**: アイテムはその**周囲に**等しい間隔を空けて表示されます。

#### `align-items`

アイテムを**直交軸方向**に並べる。

- **`flex-start`**: アイテムはコンテナーの上部に並びます。
- **`flex-end`**: アイテムはコンテナーの下部に並びます。
- **`center`**: アイテムはコンテナーの垂直方向中央に並びます。
- **`baseline`**: アイテムはコンテナーのベースラインに表示されます。
- **`stretch`**: アイテムはコンテナーの大きさに合うよう広がります。

#### `flex-direction`

コンテナ内でアイテムが配置される方向、すなわち**主軸方向**を決定する。

- **`row`**: アイテムは文章と同じ方向に配置されます。
- **`row-reverse`**: アイテムは文章と逆の方向に配置されます。
- **`column`**: アイテムは上から下に向かって配置されます。
- **`column-reverse`**: アイテムは下から上に向かって配置されます。

#### `flex-direction`注意点

主軸の方向が`column`のとき、**`justify-content`**は垂直方向の、**`align-items`**は水平方向の並び方を変えるようになる。

#### `order`

個別のアイテムに順番(配列のインデックスと同じイメージ)を適用。
デフォルトで０を取り、正の値/負の値を設定することが出来る。

```css
.yellow {
    order: 1 /* 他が0なら.yellowの要素が最後へ移動する */
}
```

#### `align-self`

`align-items` と同じ値を受け付け、指定のアイテムの状態だけ変更する。

```css
.yellow {
    align-self: end
}
```

#### `flex-wrap`

- **`nowrap`**: 全てのアイテムは、ひとつの行にフィットします。
- **`wrap`**: アイテムは他の行へ折り返します。
- **`wrap-reverse`**: アイテムは逆順になって他の行へ折り返します。

#### `flex-flow`

- `flex-direction` `flex-wrap` を統合したプロパティ。
- `flex-flow: column wrap;`のように指定

#### `align-content`

- *`align-content`**は行間の余白を決めるもので、**`align-items`*はコンテナーに含まれるアイテム全体としての配置を決めるもの。１行だけの場合 `align-content` は何の意味も持たない。
- **`flex-start`**: 行はコンテナーの上側に詰められます。
- **`flex-end`**: 行はコンテナーの下側に詰められます。
- **`center`**: 行はコンテナーの中央に詰められます。
- **`space-between`**: 行はその間に等しい間隔を空けて表示されます。
- **`space-around`**: 行はその周囲に等しい間隔を空けて表示されます。
- **`stretch`**: 行はコンテナーに合うよう引き延ばされます。

### Grid Layout

`grid`を使うことで格子状のレイアウトを簡単に作ることが出来る。

```css
#garden {
  display: grid;
  /* 行列を５分割する */
  grid-template-columns: 20% 20% 20% 20% 20%;
  grid-template-rows: 20% 20% 20% 20% 20%;
}
```

- `flex`と同じく、親要素に `display: grid` を指定してからプロパティを適用させていく。

https://codepip.com/games/grid-garden/#ja

### `grid-column-start/end`

- Pythonなどで使える配列のスライスのようなイメージ
    - `start`はN番目の**縦線からスタート**
    - `end`はN番目の**縦線で終了**
    - 言葉だけだとわかりにくいと思うので、ぜひ実際に**Grid-Garden**をプレイしてみてください。
- `grid-column-start: 1; grid-column-end: 5;` のような形で書く。
    - `start: 5 end: 2`のような書き方も可能
- 負の数を指定することも出来る
    - start に負の数を指定した時の挙動に注意

#### `span`

- `grid-column: 2 / span 3` のように書く
- その名の通り、幅を指定できる（正の数のみ）
- `start`に`span`を使えば終了位置までの幅を指定できる

#### `grid-column`

- `grid-column: 2 / 4;` のように`/`区切りで値を書くことで開始・終了位置を一度に指定できる。
- `span` キーワードも使える。

#### `grid-row`

- 列方向に働く `grid-column`

#### `grid-area`

- `grid-column` `grid-row` を一度に指定できる
- `grid-area: 1/2 / 4/6` のように書く
- **`grid-row-start`** **`grid-column-start`** **`grid-row-end`** **`grid-column-end`の順で `/` 区切り**

#### `order`

- デフォルトだと `order` は0で、要素が登場する順番に並ぶ。
- `order: 1` のように指定することで正の値/負の値を自由に設定できる。

#### 複数のグリッドアイテム

- 複数のグリッドアイテムを重ねることもできる。

```css
#water-1 {
  grid-area: 1 / 4 / 6 / 5;
}

#water-2 {
grid-area: 2/3 / 5/6
}
```

#### `grid-template-columns`

- `grid-template: 50% 20% 30%` のように書くことで、格子の幅・高さを指定できる
- `%` `px` `em` などを受け取れる
- `fr` を使える
    - 分数(fractional)の省略
    - `1fr` `5fr` と指定したとする
        - まず**残りのスペース**の1/6が計算される。それから、それぞれに1/6、5/6のスペースが与えられる。
    - `%` などによる指定と共存している場合、%などで指定されたスペースの残りが対象。
        - `grid-template-columns: 50px 1fr 1fr 1fr 50px` と書けば、左右 `50px` が割り当てられた後に３分割される。

#### `grid-template`

- `row` `column`を同時に指定できる短縮プロパティ
- `grid-template:1fr 50px / 20% 80%` のように書いたとする
    - 列は下側の`50px` + 上側の残り全て
    - 行は2:8に分かれている

#### `repeat`

- `repeat(8, 12.5%)` のように書くことで `12.5%`を8回分指定できる

## DOM操作とクロージャ

### DOMとは

**Document Object Model**のこと。

> マークアップがなされたリソース（Document）をリソース要素（Object）の木構造（Model）で表現し、操作可能にする。 (Wikipedia)
> 

> XML文書やHTML文書を構成する要素をコンピュータプログラムで参照したり操作したりするための取り決め（API）。 (IT用語辞典)
> 

#### 特徴

- ツリー構造（階層構造）を持つ

![https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/3-terrarium/3-intro-to-DOM-and-closures/images/dom-tree.png](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/3-terrarium/3-intro-to-DOM-and-closures/images/dom-tree.png)

> DOM とそれを参照する HTML マークアップの表現。Olfa Nasraoui より

- HTML文書を**ノード**を最小単位として表現する
- **ノード間の関係**（親子・兄弟関係）が存在し、DOM操作では特定のノードからその親、子などを参照することが出来る
- DOMにアクセスし、編集・変更・再配置・その他管理をすることでWebページを編集することが出来る。

#### 参考

- [DocumentObjectModel - Wilipedia](https://ja.wikipedia.org/wiki/Document_Object_Model)
- [DOM - IT用語辞典](https://e-words.jp/w/DOM.html)
- [DOMの紹介 - MDN](https://developer.mozilla.org/ja/docs/Web/API/Document_Object_Model/Introduction)

#### JavaScriptから操作

```js
dragElement(document.getElementById('plant1'));
```

このように書くことでDOMで操作したい要素への参照を得ることが出来る。

### クロージャとは

MDNによると、

> クロージャは、組み合わされた（囲まれた）関数と、その周囲の状態（レキシカル環境）への参照の組み合わせです。言い換えれば、クロージャは内側の関数から外側の関数スコープへのアクセスを提供します。JavaScript では、関数が作成されるたびにクロージャが作成されます。
> 

よくわからないですね・・・

コードを見てみます。

```js
function makeFunc() {
  let name = 'Mozilla';
  function displayName() {
    alert(name);
  }
  return displayName;
}

let myFunc = makeFunc();
myFunc();
```

- `myFunc` は `makeFunc` の実行結果である `displayName` 関数への参照。
- `displayName` はレキシカル環境への参照を維持するため、 `name` 変数にアクセスできる。

#### レキシカル環境って？

[静的スコープ  - Wikipedia](https://ja.wikipedia.org/wiki/%E9%9D%99%E7%9A%84%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%97)

- レキシカル=字面上の
- レキシカルスコープ=静的スコープで、ソースコードの段階でスコープが確定するようなスコープのこと。

#### つまり？

- 外側の関数のスコープで変数を定義し、
- 外側の関数の中に関数を作り、
- その関数内の関数から外側の関数のスコープで定義した変数を参照できる

Wikipediaによると、

> クロージャ (クロージャー、Closure) は、プログラミング言語において引数以外の変数を実行時の環境ではなく、自身が定義された環境（静的スコープ）において解決する関数のことである。

つまり、変数の参照先が実行時の環境（関数の外側）ではなく、自身が定義された環境（静的スコープ・関数の内側）である。
という感じでしょうか。

クロージャによって、こんな事ができます。

```js
function outer() {

    let x = 10;

    function inner() {
        console.log(x)
        x = x + 1
    }

    return inner;
}
```

`js
let f = outer()

f(); // 10
f(); // 11
f(); // 12
`

#### 参考

- [クロージャ - MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Closures)
- [なぜクロージャというのか？ - Qiita](https://qiita.com/mochizukikotaro/items/7403835a0dbb00ea71ae)
- [クロージャ - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%AF%E3%83%AD%E3%83%BC%E3%82%B8%E3%83%A3#:~:text=%E3%82%AF%E3%83%AD%E3%83%BC%E3%82%B8%E3%83%A3%EF%BC%88%E3%82%AF%E3%83%AD%E3%83%BC%E3%82%B8%E3%83%A3%E3%83%BC%E3%80%81%E8%8B%B1%E8%AA%9E%3A%20closure,%E3%81%93%E3%81%A8%E3%82%92%E7%89%B9%E5%BE%B4%E3%81%A8%E3%81%99%E3%82%8B%E3%80%82)

### ドラッグ&ドロップで植物を自由に動かせるようにする

JavaScriptによるDOM操作を実装していきます。

1. まずDOMで操作したい要素への参照を用意する
    
    `js
    dragElement(document.getElementById('plant1'));
    dragElement(document.getElementById('plant2'));
    dragElement(document.getElementById('plant3'));
    // 以下省略
    `
    
2. `dragElement`関数を作成
    - 関数に渡されたオブジェクトの位置を初期化
    - `pointerdown` イベントを登録
        - `pointerdown` はボタンが押されたとき、あるいはドラッグ可能な要素がタッチされたときに発生。
    
    実装するクロージャの全体像
    
    `js
    // dragElement : 最も外側の関数
    function dragElement(terrariumElement) {
    		let pos1,pos2,pos3,pos4 = 0;
        terrariumElement.onpointerdown = pointerDrag
    
        function pointerDrag() {
    			// マウス押下された時に呼ばれる
        }
        function elementDrag() {
    			// ドラッグされた時
        }
        function stopElementDrag() {
    			// ドロップされた時
        }
    }
    `
    
3. マウスが押下された時に以下を実行
    - デフォルトのイベント(ドラッグが解除されたら元の位置に戻る)を無効化
    - マウスカーソルの初期位置を取得し、`pos3` `pos4`に入れる
        - `evnet.clientX/Y` で取得
    - マウス移動時/停止時のイベントを割り当て
    
    `js
    function dragElement(terrariumElement) {
    
        let pos1,pos2,pos3,pos4 = 0;
        terrariumElement.onpointerdown = pointerDrag
    
        function pointerDrag(e) {
            // デフォルトのイベントを防ぐ
            e.preventDefault
            // マウスカーソルの初期位置を取得
            pos3 = e.clientX
            pos4 = e.clientY
    
    		document.onpointermove = elementDrag;
    		document.onpointerup = stopElementDrag;
        }
    
        function elementDrag() {
    
        }
    
        function stopElementDrag() {
    
        }
    }
    `
    
4. マウス移動時に以下を実行
    - 外側で定義した`pos1~4`を更新
    - `terrariumElement` のスタイル(座標情報)を更新
    
    `js
    function elementDrag() {
        // pos1 = xの[過去の位置-現在の位置] (移動距離)
    	pos1 = pos3 - e.clientX;
    	pos2 = pos4 - e.clientY;
    	//pos3, 4を現在位置にリセット
    	pos3 = e.clientX;
    	pos4 = e.clientY;
    	console.log(pos1, pos2, pos3, pos4);
    	// Elementの新しい位置を設定
    	terrariumElement.style.top = terrariumElement.offsetTop - pos2 + 'px';
    	terrariumElement.style.left = terrariumElement.offsetLeft - pos1 + 'px';
        }
    `
    
5. マウス停止時に `onpointermove/up` のイベントをnullにする
    - こうしないと`pointermove`時に実行される関数が残ってしまう
    
    `js
    function stopElementDrag() {
            document.onpointermove = null;
            document.onpointerup = null;
        }
    `
    

完成！

![https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/3683e3e0-5967-a69d-0bad-90550a7e9481.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/3683e3e0-5967-a69d-0bad-90550a7e9481.gif)

### 副教材

- [WebAPI - MDN](https://developer.mozilla.org/ja/docs/Web/API)
- [Can I use... Support tables for HTML5, CSS3, etc](https://caniuse.com/)
    - 機能がブラウザに対応しているか調べるためのサイト
- [HTML ドラッグ＆ドロップ API - MDN](https://developer.mozilla.org/ja/docs/Web/API/HTML_Drag_and_Drop_API)
    - ドラッグ＆ドロップ操作の詳細
- [Pointer events - MDN](https://developer.mozilla.org/ja/docs/Web/API/Pointer_events)
    - ポインターイベントの詳細

## 学んだこと

- HTMLの基礎について
- CSSの基礎について
    - どの要素にどのプロパティが適用されるのかしっかり把握することが大切。
- **flexbox**について
    - `display: flex`を使えばブロック要素を柔軟に並べることが出来る。
- **Grid Layout**について
    - `display: grid`を使えば格子状のレイアウトを簡単に作ることが出来る。
- 簡単なDOM操作、クロージャについて
    - JavaScriptからWebページを操作する時はDOM操作を多用する。
    - 今回の実装ではアプリ全体を1つの大きなクロージャとして構築することで、複数のドラッグ可能なオブジェクトのそれぞれのスコープを簡単に維持するができた。