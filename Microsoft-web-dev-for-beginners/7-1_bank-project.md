## はじめに

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

[〜②JavaScript基礎まで【導入/アクセシビリティ/JavaScript の基礎】](https://qiita.com/NasuPanda/items/d78514969191491a4bcd)
[③テラリウム構築 【HTML・CSS基礎/DOM操作/クロージャ】](https://qiita.com/NasuPanda/items/59b8e43d8d6fb609c7d5)
[④タイピングゲーム 【JavaScriptのイベント処理】　本記事](https://qiita.com/NasuPanda/items/340f391ee9f167bf4333)
[⑤-1ブラウザ拡張機能 【ブラウザの仕組み/拡張機能作成の導入】](https://qiita.com/NasuPanda/items/d0189565d039c2c11383)
[⑤-2ブラウザ拡張機能 【API/LocalStorage/BackGround/Performance】](https://qiita.com/NasuPanda/items/4186e6701cd2d4d68bb2)
[⑥スペースシューティングゲーム 【ゲーム開発の基礎/Pub-Sub/Canvas/衝突検出】](https://qiita.com/NasuPanda/items/16ffb297be9b862d2785)
**⑦架空銀行プロジェクト【ログイン/データ管理/状態管理】　本記事**

***

### 記事の目的

- 学習のアウトプット
- 教材を使ってみたところかなり良かったので、その紹介

### 注意点

自身の学習のアウトプットがメインなので、理解できているところ(他言語と共通の箇所など)は省いています。
また、課題やtipsについても結構省きます。
この教材に興味を持った方はぜひご自分で取り組んでみてください。

# 7 Bank-project

https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project

Node.jsを用いて架空の銀行を構築していきます。

![bank-image][https://github.com/Westen0511/Qiita-writing/blob/main/Microsoft-web-dev-for-beginners/images/bank-result.png?raw=true]

### やること

1. [Web アプリの HTML テンプレートとルート](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project/1-template-route/translations/README.ja.md)
2. [ログインと登録フォームの構築](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project/2-forms/translations/README.ja.md)
3. [データの取得と利用方法](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project/3-data/translations/README.ja.md)
4. [状態管理の概念](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/7-bank-project/4-state-management/translations/README.ja.md)

### 学習の目的

- ルーティングと HTML テンプレートを使ったマルチページサイトのアーキテクチャの足場の作り方を学ぶ
- フォームの構築と検証ルーチンの渡し方について学ぶ
- アプリのデータの出入り、データの取得方法、保存方法、廃棄方法
- アプリの状態を保持する方法とプログラムで管理する方法を学ぶ

## HTMLテンプレートとルート