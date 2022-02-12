<!--
title:   MicrosoftのWeb開発教材を使ってみた 〜②JavaScript基礎まで【導入/アクセシビリティ/JavaScript の基礎】
tags:    JavaScript,Microsoft,初心者,初心者向け
id:      d78514969191491a4bcd
private: false
-->
# はじめに

https://qiita.com/ozora/items/9c801d3b0137eccc32fa

こちらの記事で紹介されているのを見て以来、いつか使ってみようと思っていた**「Web Development For Beginners」**というMicrosoftがGithubに公開している教材を使ってみました。

### 記事の目的

* 学習のアウトプット
* 教材を使ってみたところかなり良かったので、その紹介

### 注意点

自身の学習のアウトプットがメインなので、理解できているところ(多言語と共通の箇所など)は省いています。
また、課題やtipsについても結構省きます。
この教材に興味を持った方はぜひご自分で取り組んでみてください。



## この教材を選んだ理由

https://github.com/microsoft/Web-Dev-For-Beginners

- HTML/CSS/JavaScriptを触れるいい感じの教材が欲しかった
    - そこそこのボリュームがあり、作りながら学べるタイプの教材
    - 基礎的なトピックが一通り網羅されていると嬉しい
- 質が高そう
    - なにせあのMicrosoftなので、きっと良いものでしょう。
- 題材が**面白そう**
    - 軽く調べた感じだとチュートリアルでよくある題材として「TODOアプリ」「クイズアプリ」などがあるみたいですが、どれもどう実装するのか想像がついてしまって、余り興味がわきませんでした。
    - しかしこの教材は「テラリウム」「タイピングゲーム」「ブラウザ拡張機能」「スペースゲーム」「銀行プロジェクト」と、面白そうなトピックが並んでいます。

### +α 実際に取り組んで感じたこと

- **提供されるリファレンス・参考サイトの質が高い**
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
- **説明はかなりあっさり**
    - 例えば、`async/await`についての[説明](https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/5-browser-extension/2-forms-browsers-local-storage#display-carbon-usage)には1セクション程度しか割かれておらず、`Promise`とは？の解説もほぼないので、これだけで理解するのは難しい(というか無理)です。
    - この教材を通して学べるのはあくまで「こういう場面ではこんな機能を使う」「このように考えて実装していく」といった点です。
    - 足りない箇所はMDNや記事で補うことで、むしろ**情報収集の練習**になるな、とプラスに考えて取り組みました。
- スケッチノートがわかりやすい
    - 一部レッスンは最初にスケッチノートというイラストがあるのですが、それがすごくわかりやすいです。それに可愛い。
    - 扱うトピックについてイラストで視覚的に示してくれるので、どんな内容をやるのかざっくり把握してからレッスンに入ることが出来ます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/52789223-13b3-1043-edb6-e26d5828bf35.png)
 > [microsoft/Web-Dev-For-Beginners/tree/main/1-getting-started-lessons/3-accessibility より](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/sketchnotes/webdev101-a11y.png)


## 教材の概要

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

### 教材の構成

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


# 1-Getting-started-lessons

https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/1-getting-started-lessons

### 学習の目的

* ほとんどのプログラミング言語の背後にある基本的な基盤と、プロの開発者が仕事をするのに役立つソフトウェアについて学ぶ。
* プロジェクトでの GitHub の使い方、コードベースでの他の人との共同作業の仕方について学ぶ。
* Web アクセシビリティの基礎を学ぶ。

## プログラミング言語と開発ツール

- プログラミングとは何か
    - コードを介してデバイスに命令を出すこと
    - コードを書かずにプログラムを作っていたとしても、実際に解釈されているのはコード
- プログラミング言語について
    - 各言語の簡単な特徴
    - 高級言語 : 人間にとってわかりやすい
    - 低級言語 : 機械にとってわかりやすい
- 世界初のプログラマは[エイダ・ラブレス](https://ja.wikipedia.org/wiki/%E3%82%A8%E3%82%A4%E3%83%80%E3%83%BB%E3%83%A9%E3%83%96%E3%83%AC%E3%82%B9)という女性らしい
- **Web開発で有用なドキュメントの紹介**
    - [Mozilla Developer Network (MDN)](https://developer.mozilla.org/docs/Web)
    - [Frontend Masters](https://frontendmasters.com/learn/)
    - [Web.dev](https://web.dev/)(Google)
    - [Microsoft 独自の開発者向けドキュメント](https://docs.microsoft.com/microsoft-edge/#microsoft-edge-for-developers) ([Microsoft Edge](https://www.microsoft.com/edge)の場合)

### 課題 ドキュメントを読む

[MDN - Client-side tooling overview](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Overview)
このページからいくつかピックアップして、ツールの概要を調べる

- リンター
    - eslint/csslintなど
    - コード内にエラーが存在しないか教えてくれる
    - チームで共通のスタイルを導入することで生産性を高める事ができる
- ソースコード管理
    - Git/Githubなど
    - ソースコードのバックアップを取ることで、万が一エラーが起きても元に戻せるなどの利点がある
    - チームでコードを共有しながら作業をすすめることが出来る
- バンドラー
    - Webpackなど
    - 開発時は人間にとってわかりやすい(インデントなど)コードを書き、本番環境では最小構成にする(ミニファイリング)、といった事が可能
    - 依存関係をよしなにしてくれる

## Githubの基礎

- Githubの基礎的な使い方
    - ほぼやったことのある内容なので流し読み程度。
- コミットメッセージは `how` ではなく `why` を書こう

### 紹介されていた教材

自分自身まだ理解が浅いトピック(コンフリクトの解消やGitFlowによる開発)があるので、後々触れたいと思います。

- [lab.github](https://lab.github.com/)
- [First Week on Github](https://lab.github.com/githubtraining/first-week-on-github)（Lerning course）

    コンテンツ(全部英語)
    1. **[GitHub Pages](https://lab.github.com/githubtraining/github-pages)** Course
    2. **[Reviewing pull requests](https://lab.github.com/githubtraining/reviewing-pull-requests)** Course
    3. **[Managing merge conflicts](https://lab.github.com/githubtraining/managing-merge-conflicts)** Course
    4. **[Securing your workflows](https://lab.github.com/githubtraining/securing-your-workflows)** Course
- [Gitチートシート](https://training.github.com/downloads/github-git-cheat-sheet/)
    - チートシート=よく使うコマンドなどをまとめたもの

## アクセシビリティ

アクセシビリティについて。

- Webサイトは誰でもアクセス出来ることが重要
- その人の能力・障害に関係なく欲しい情報が得られるようにする必要がある
- そこで、アクセシビリティを念頭に置いてWebサイトを構築するようにする
    - [アクセシビリティを考慮した設計](https://accessibility.umn.edu/your-role/web-developers)

### アクセシビリティに関わるブラウザの主要機能

- スクリーンリーダー
- ズーム機能
- コントラストチェッカー
    - 色覚障害者やコントラストの低い色が見えにくいユーザ向けに
- LightHouse
    - Performance
    - Accessibility
    - Best Practice
    - SEO
        - などの項目を調査できるDevloperツールの機能。
        

### 良いWebサイトの原則

- 正しいHTMLを使う
    - 適切なHTMLを使うことは**セマンティックHTML**と呼ばれる
    - スクリーンリーダーに正しく情報を伝えるため、正しいHTMLを使う。
- カラーセーフパレット
    - 誰でも利用できるような配色を。
    - カラーパレットを生成するためのツール([ColorSafe](http://colorsafe.co/))などを使う。
- 見出しを階層的に作成
    - スクリーンリーダーのユーザはページ内移動の際に見出しに大きく依存している。
    - トピックごとの階層構造を意識する。
- 視覚的な手がかりを上手く使う
    - アウトラインのないテキストボックスやアンダーラインの無いハイパーリンクを作らない。
- アクセシビリティを良くすることで、検索エンジンがサイトをナビゲートする際に役立つ。
    - SEO的にも有利になる。
    
    

### リンクテキストの重要性

- 悪いリンクの例として、「ここをクリック」「URLベタ貼り」等がある。スクリーンリーダーは他のテキストを読むのと同じ方法で読んでしまう。
    - 「Click here」はスクリーンリーダーユーザにとっては「Click here」でしかない。
    - 一般的にURLは人間にとって意味のある情報を伝えない。

- 良いリンクテキストは、リンク先にあるものを簡単に説明する。
    
    > コガタペンギンは、[フェアリーペンギン](https://en.wikipedia.org/wiki/Little_penguin)とも呼ばれ、世界最小のペンギンです。
    > 
- ARIAを使うことでスクリーンリーダーに追加情報を提供することが出来る。

### 画像

- スクリーンリーダーは `alt` 属性から画像の概要を理解する。
    - すべての意味のある画像は `alt` 属性により何であるか説明が必要
    - 純粋に装飾的な画像は `alt=""` とする。（意味を与えない）
    - 検索エンジンも `alt` により画像を認識するのでSEO的にも有利になる。

### 学んだこと

* プログラミング言語/プログラミングについて
* 基本的な開発ツールについて
* Githubについて
    * 副教材は後でやる。
* アクセシビリティの重要性について
    * 適切なHTMLでサイトを構成することが大切。

# 2-js-basics

https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/2-js-basics

### 学習の目的

* JavaScriptのデータ型の基礎を学ぶ
* アプリケーションのロジックフローを管理するための機能とメソッドを学ぶ
* 条件分岐を使って処理を分岐させる方法を学ぶ
* 配列やループを使ってデータを扱う

## 変数とデータ型

変数には使用したり変更したり出来る値が格納されている。
変数の宣言には `var` `let` `const` が使える。
現在`var`はほぼ使われない。

#### const

- ブロックスコープ
    - ブロック (`{}`) 内で参照可能なスコープ
- 宣言後のみ使える
- 再代入不可
- 不変ではなく、参照が再割り当てから保護されている状態
- const = constant

#### let

- ブロックスコープ
- 宣言後のみ使える
- 再代入可能
- ループでよく使う
- [なぜletという名前が選ばれたのか - stack overflow](https://stackoverflow.com/questions/37916940/why-was-the-name-let-chosen-for-block-scoped-variable-declarations-in-javascri)

訳があっているのかわかりませんが・・・

> LetはSchemeやBasicといった初期のプログラミング言語で採用された数学的な構文です。
変数は低レベルの実体であり、より高度な抽象化には適さないと考えられていました。
Clojure、F#、Scalaのような、より強力で類似した概念を導入したいというのが、多くの言語設計者の願いです。
letは値、または代入はできるが変更はできない変数を意味し、これによりコンパイラはより多くのプログラミングエラーを検出し、コードをより最適化することができます。
JavaScript は最初から var を持っていたので、別のキーワードが必要になり、var にできるだけ近い伝統的なキーワードとして let をすでに使っている何十もの他の言語から借用したのですが、JavaScript では let は代わりにブロックスコープのローカル変数を作成します。

### データ型

- 6つのプリミティブデータ型
    - string
    - number
    - bigint
        - 整数の末尾に n を追加するか、コンストラクターを呼び出すことで作成
    - boolean
    - undefined
    - symbol
    - 教材では6種類とされているが、`null`が含まれる場合もある?
        - [Null - MDN](https://developer.mozilla.org/ja/docs/Glossary/Null)
- +α 自分で調べた **プリミティブ型とオブジェクト型の違い**
    - 参考
        - [プリミティブ - MDN](https://developer.mozilla.org/ja/docs/Glossary/Primitive)
        - [JavaScript のデータ型とデータ構造 - MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Data_structures)
        - [ラッパーオブジェクト JavaScript Primer](https://jsprimer.net/basic/wrapper-object/)
    - **オブジェクト型**はプロパティとメソッドの集合
    - **プリミティブ型**は純粋な値で、イミュータブル、メソッドを持たないなどの特徴を持つ
    - プリミティブ型をオブジェクトとして扱うデータ型(`null` `undefined`を除く)が用意されていて、**ラッパーオブジェクト**と呼ばれる。
        - `new String("Hello")`のように書くことで明示的に宣言できる
    - プリミティブ型からメソッドに普通にアクセスできるのは、必要に応じて自動的にラッパーオブジェクトに変換されているから。
- 文字列への変数代入は `` `${myString}` `` のように書く
- [Truthy - MDN](https://developer.mozilla.org/ja/docs/Glossary/Truthy)
    - Java Scriptではfalsyとして定義された値(`false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`)以外はtrueとして扱われる。
    

### チャレンジ

- データ型を扱う際の”gotchas”について（奇妙な挙動）調べてみる
    - [gotchasの意味](https://eigo.plus/englishphrase/gotcha)
        - スラングらしいです。
        - わかった！捕まえた！やった！見たぞー！・・・どれ？
    - [16 Common JavaScript Gotchas](http://www.standardista.com/javascript/15-common-javascript-gotchas/)
    - [暗黙的な型変換](https://jsprimer.net/basic/implicit-coercion/)
    

### 課題

- [Java Scriptの練習問題 (英語)](https://css-tricks.com/snippets/javascript/)を解いてみる
    - 暇つぶしに良さそうですね。

## 関数とメソッド

### 関数について

- 関数はコードの塊を作り、オンデマンドで機能を実行できるもの。
- 定義方法は様々だが、現在は[アロー関数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions/Arrow_functions)が好まれる。
    - MDNの説明がわかりやすかったです。
    - 引数が複数の場合は()が必要。
    - `{}` や `return` は処理が1行の場合省略可能。

```js
// 伝統的な関数
function (a){
  return a + 100;
    }
// アロー関数に分解
// 1. "function" という語を削除し、引数と本体の開始中括弧の間に矢印を配置する
(a) => {
  return a + 100;
}
    
// 2. 本体の中括弧を削除と "return" という語を削除
// return は既に含まれています。
(a) => a + 100;
    
// 3. 引数の括弧を削除
a => a + 100;
```

#### デフォルト引数

引数がデフォルトで取る値を決めておくことが出来る。
    
```jsx
let getFullName = (first, family="tanaka") => {
  return family + " " + first
}
```
    
#### 関数を引数として渡す

- 関数を関数の引数として渡すことが出来る。
- 関数に名前をつけず利用(無名関数)することも出来る。
    
```jsx
// before
function displayDone() {
  console.log('3 seconds has elapsed');
}
setTimeout(displayDone, 3000);
    
// after
setTimeout(() => {
    console.log("3 seconds has slapsed")
}, 3000);
```
    
- 関数とメソッド
    - 関数はそれ単体で動作するコードブロック
    - メソッドはあるオブジェクトに属している関数
    
### 条件分岐

基本的に他の言語とそこまで違いは無いようなので、軽く流す程度で。

- [Operator look up](https://www.joshwcomeau.com/operator-lookup/)
    - 色々なOperator、及びその動作を調べることが出来るサイト
- [MDNレファレンス - 式と演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators)
    - 困ったら見る
- [三項演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
    - `const message = (status===200) ? "OK" : "Error";` 

- `==` 値が等しい
- `===` 値とデータ型が等しい
- Boolean型は [George Boole](https://ja.wikipedia.org/wiki/%E3%82%B8%E3%83%A7%E3%83%BC%E3%82%B8%E3%83%BB%E3%83%96%E3%83%BC%E3%83%AB) (イギリスの数学者、哲学者) が由来らしい
    - ブール代数の人

## 配列とループ

for文が色々あって戸惑いましたが、今は「こんなものがある」程度で良しとします。

- [MDNレファレンス - Array](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array)
- `for` VS `while`
    - ループ処理は基本 `for` でOK
    - 何回ループすればいいかわからない場合（例：ユーザが正しい入力をするまで入力待ち）は`while` のほうがよい。

#### [for](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/for)

**括弧で囲みセミコロンで区切った3つの引数**と、**ループ内で実行される文**から成るループ
    
 `js
let str = '';
    
for (let i = 0; i < 9; i++) {
    str = str + i;
    }
console.log(str); // 012345678
 ` 

#### [for-Each](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

配列の中身をシンプルに取り出す
    
```js
const array1 = ['a', 'b', 'c'];
    
array1.forEach(element => console.log(element));
    
// 出力
    // a
    // b
    // c
```
    
#### [for-of](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/for...of)

反復可能オブジェクトが値を反復処理
    
```js
for (const iterator of object) {
    console.log(iterator);
}
```
    
#### [for-in](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/for...in)

列挙可能プロパティに対して反復処理
    
```js
for (const key in object) {
    if (Object.hasOwnProperty.call(object, key)) {
        const element = object[key];
    }
}
```
    
#### [for-of / for-in 違い](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/for...of#difference_between_for...of_and_for...in)

* `for-of`は[反復可能オブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Iterators_and_Generators#iterables)が定義した順序で値を反復処理する。
    * ループ処理の対象は**値**
* `for-in`はオブジェクトのすべての[列挙可能なプロパティ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)に対して順序不定で繰り返し処理を行う。
    * ループ処理の対象は**プロパティ**
    
```jsx
> const iterable = [3, 5, 7]
 
> for (const i of iterable) { console.log(i); }
3
5
7

> for (const i in iterable) { console.log(i); }
0
1
2
```

### 学んだこと

* 変数宣言
    * `let` `const`の違い
    * ブロックスコープについて
* データ型の概要
* 関数について
    * 色々な定義方法
    * デフォルト引数
    * JavaScriptでは関数を引数として扱える
* 条件分岐について
    * 色々な演算子について
* forループやwhileループ

## 他記事へのリンク

まだ基礎中の基礎なので、特に面白い・難しいところはないです。
③以降少しずつ面白くなります。

* **〜②JavaScript基礎まで【導入/アクセシビリティ/JavaScript の基礎】　本記事**
* [③テラリウム構築 【HTML・CSS基礎/DOM操作/クロージャ】](2022-02-09_CSS_HTML_JavaScript_59b8e43d8d6fb609c7d5.md)
* [④タイピングゲーム 【JavaScriptのイベント処理】](2022-02-09_JavaScript_340f391ee9f167bf4333.md)
* [⑤-1ブラウザ拡張機能 【ブラウザの仕組み/拡張機能作成の導入】](2022-02-10_Web_d0189565d039c2c11383.md)
* ⑤-2ブラウザ拡張機能 【API/LocalStorage/BackGround/Performance】
* ⑥スペースシューティングゲーム【JavaScriptによるゲーム開発の基礎】
* ⑦架空銀行プロジェクト【ログイン/データ管理/状態管理】