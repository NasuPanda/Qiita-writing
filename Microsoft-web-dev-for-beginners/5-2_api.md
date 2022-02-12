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
[③テラリウム構築 【HTML・CSS基礎/DOM操作/クロージャ】](2022-02-09_CSS_HTML_JavaScript_59b8e43d8d6fb609c7d5.md)
[④タイピングゲーム 【JavaScriptのイベント処理】](2022-02-09_JavaScript_340f391ee9f167bf4333.md)
[⑤-1ブラウザ拡張機能 【ブラウザの仕組み/拡張機能作成の導入】](2022-02-10_Web_d0189565d039c2c11383.md)
**⑤-2ブラウザ拡張機能 【API/LocalStorage/BackGround/Performance】 本記事**
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

## 5-Browser-extensionの続き

https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/5-browser-extension

指定された地域の[カーボンフットプリント](https://ja.wikipedia.org/wiki/%E3%82%AB%E3%83%BC%E3%83%9C%E3%83%B3%E3%83%95%E3%83%83%E3%83%88%E3%83%97%E3%83%AA%E3%83%B3%E3%83%88)を表示するブラウザ拡張機能を作っていきます。
その過程でブラウザの仕組みやフォームの構築方法、APIの呼び出し、ローカルストレージの使用方法などについて学びます。

![browser-extension-demo](https://github.com/microsoft/Web-Dev-For-Beginners/raw/main/5-browser-extension/extension-screenshot.png)
> https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/5-browser-extension より

### 学習の目的

* ブラウザの仕組み、歴史、ブラウザ拡張機能の最初の要素の足場の作り方を学ぶ
* ローカルストレージに格納された変数を使用してAPIを呼び出すためのブラウザ拡張機能のJavaScript 要素を構築する
* ブラウザのバックグラウンドプロセスを使用して拡張機能のアイコンを管理する
* Webのパフォーマンスと最適化について学ぶ

## フォームの構築、API の呼び出し、ローカルストレージへの変数の格納

- フォームを構築する。
- APIを呼び出し、結果を表示してみる。
- ローカルストレージの使い方を学ぶ。

`src/index.js` に実装していく。

#### HTMLエレメントへの参照

```js
// querySelector : 指定されたセレクタに一致する最初の要素を返す
const form = document.querySelector('.form-data');
const region = document.querySelector('.region-name');
// 以下省略
```

#### イベントリスナーの追加

```js
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

#### `init` `reset` 関数の実装(localStorageの利用)

初期設定、リセット用の関数を定義する。
特定の要素の表示/非表示は**`display`**を編集することで実装する。

- ユーザーが`APIKey`と**リージョンコード**をローカルストレージに保存しているかどうかチェック
- APIキーかリージョンコードのいずれかが NULL の場合、
  - 入力フォームを表示
  - results、loading、clearBtnを非表示
  - エラーテキストを空文字列に設定
- APIキーとリージョンコードが存在する場合、以下の処理を行う
    - APIを呼び出して炭素使用量データを取得する
    - 結果エリアを隠す
    - フォームを隠す
    - リセットボタンを表示する

今回の例では、データの保存に**LocalStorage**を使用する。

- ブラウザに[キー:値]のペアとしてデータを保存しておくことができる機能
- SessionStorageと異なり期限切れがない
- ブラウザ拡張は独自のローカルストレージを持つ。メインブラウザウィンドウは別のインスタンスであり、別々に動作する。
- `getItem()` `setItem()` `removeItem()`のいずれかを使用して操作する
- 学習用なので平文のままのAPIキーをローカルストレージに保存するが、本来それは避けるべき

```js
function init() {
  //ローカルストレージに保存されているキーを取得
  const storedApiKey = localStorage.getItem('apiKey');
  const storedRegion = localStorage.getItem('regionName');

  if (storedApiKey === null || storedRegion === null) {
    //いずれかのキーが空ならフォームを表示
    form.style.display = 'block';
    results.style.display = 'none';
    loading.style.display = 'none';
    clearBtn.style.display = 'none';
    errors.textContent = '';
  } else {
    //キーがローカルストレージに保存されていれば結果を表示
    displayCarbonUsage(storedApiKey, storedRegion);
    results.style.display = 'none';
    form.style.display = 'none';
    clearBtn.style.display = 'block';
  }
};

function reset(e) {
  e.preventDefault();
  //「地域」をローカルストレージから削除
  localStorage.removeItem('regionName');
  init();
}
```

#### フォーム送信の処理を追加

- `preventDefault` でイベントの伝搬を阻止
  - イベント = `submit` イベント。
  - デフォルトだとフォームの内容をURLに送信=ページが更新されてしまうため、それを阻止している。
    - [参考 - MDN](https://developer.mozilla.org/ja/docs/Web/API/HTMLFormElement/submit_event#examples)
- 新しく追加する `setUpUser` 関数にapiKey, regionを渡す

```js
function handleSubmit(e) {
  e.preventDefault();
  setUpUser(apiKey.value, region.value);
}

// 呼び出される場所
form.addEventListener('submit', (e) => handleSubmit(e));
```

#### `setUpUser`関数でローカルストレージにAPIキーとリージョンの値を設定

- API呼び出し中に表示されるロード画面を設定

```js
function setUpUser(apiKey, regionName) {
  localStorage.setItem('apiKey', apiKey);
  localStorage.setItem('regionName', regionName);
  loading.style.display = 'block';
  errors.textContent = '';
  clearBtn.style.display = 'block';

  displayCarbonUsage(apiKey, regionName);
}
```

#### APIへの問い合わせ、炭素使用量の表示

- **API** Application Programming Interface
  - ソフトウェアの一部機能を共有する仕組みのこと
  - 機能を公開している側⇔利用したい側をつなぐインターフェース
  - RESTAPIが最も一般的で、HTTPリクエスト/URLなどを利用してデータ(一般的にはJSONファイル)をやり取りする
- **async/await** 非同期処理
  - 「データを返す」などの処理が完了するのを待ってから処理を続ける
    - APIの応答速度を制御できないため
- レスポンスの内容を表示する
  - エラー、内容が無い場合はエラーメッセージを表示する

```js
import axios from '../node_modules/axios';

async function displayCarbonUsage(apiKey, region) {
try {
	await axios
		.get('https://api.co2signal.com/v1/latest', {
			params: {
				countryCode: region,
			},
			headers: {
				'auth-token': apiKey,
			},
		})
		.then((response) => {
			let CO2 = Math.floor(response.data.data.carbonIntensity);

			loading.style.display = 'none';
			form.style.display = 'none';
			myregion.textContent = region;
			usage.textContent =
				Math.round(response.data.data.carbonIntensity) + ' grams (grams C02 emitted per kilowatt hour)';
			fossilfuel.textContent =
				response.data.data.fossilFuelPercentage.toFixed(2) +
				'% (percentage of fossil fuels used to generate electricity)';
			results.style.display = 'block';
		});
} catch (error) {
	console.log(error);
	loading.style.display = 'none';
	results.style.display = 'none';
	errors.textContent = 'Sorry, we have no data for the region you have requested.';
}
}
```

この関数は**async キーワード**が使われている。これは、関数が非同期で実行されることを表す。

* データが返されるなどのアクションが完了するのを待ってから処理を続けることを意味する。
* try/catchブロックが含まれており、APIがデータを返したときに`Promise`を返すようになっている。APIが応答する速度を制御できないので（全く応答しないかもしれない）、非同期で呼び出すことによってこの不確実性を処理している。

また、**`axios`**も使われている。[公式](https://github.com/axios/axios)によると、
> Promise based HTTP client for the browser and node.js

直訳するとブラウザや node.js で動く Promise ベースの HTTP クライアント。

* 簡潔にHTTP通信の処理が書けることや、ブラウザ・node.jsに対応していることが利点らしい。
* ここでは`get`メソッドを使って`response`を得ている。
  * [`response.data`の中身](https://github.com/axios/axios#response-schema)

    ```js
    // `data` is the response that was provided by the server
    data: {},
    ```

* `params`や`headers`などに値を渡すことで色々と[設定](https://github.com/axios/axios#request-config)できる。

  ```js
  // `headers` are custom headers to be sent
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` are the URL parameters to be sent with the request
  // Must be a plain object or a URLSearchParams object
  params: {
    ID: 12345
  },
  ```
  * 試しにQiitaにアクセスする時のHTTPヘッダを見てみる
   ![headers](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/03f3abb2-0e0a-b660-7520-347a44e105e5.png)

## `Promise` is 何

**わからないこと**

* `Promise`
* 非同期
* `async/await`

### Promise

> プロミス (Promise) は、非同期処理の最終的な完了もしくは失敗を表すオブジェクトです。
> [プロミスの使用 - MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises)


ふむ。非同期とは・・・

### 非同期

* [非同期プログラミングの一般的概念 - MDN](https://developer.mozilla.org/ja/docs/Learn/JavaScript/Asynchronous/Concepts)

**非同期とは？**

> 通常は、あるプログラムのコードは書かれた順に、一度にひとつのことだけが起こるように実行されます。もしある関数が別の関数の結果に依存するのであれば、その関数は他の関数の処理が完了して結果を返すまで待たなくてはならず、それまでは、ユーザー視点からはプログラム全体は止まっているのと本質的には同じです。

> 例えば、Mac ユーザーは回転する虹色のカーソル（よく「ビーチボール」と呼ばれます）としてこのことを経験することもあるでしょう。このカーソルによってオペレーティングシステムは「現在使用中のプログラムは何かが終わるのを待って停止しており、それが非常に長く掛かっているので何が起こっているのかとご心配をお掛けしているのではないでしょうか」と言っているのです。
> ![RAINBOW](https://mdn.mozillademos.org/files/16577/beachball.jpg)

> これはいら立つような体験であり、コンピューターの処理能力の良い使い方ではありません――特に、マルチコアプロセッサーが利用できる時代においては。他のタスクを別のプロセッサーコアに処理させて、それが終わった時に知らせることができるのに、座って待っているのは意味がありません。このように合間に別の仕事を終わらせる、ということが非同期プログラミングの基本です。非同期にタスクを実行する API は、あなたが使用するプログラミング環境（ウェブ開発であればウェブブラウザー）によって提供されます。

* ある処理をしている間に、他の処理を進めること(=処理が同期していない)を非同期処理と呼ぶ。
* 一方、順次実行していくタイプの処理は同期処理と呼ぶ。
* 同期処理の場合、高負荷な処理に差し掛かった際に全体の処理が止まってしまうという弱点がある。ブラウザでは特にその弱点が問題になるため、非同期処理を使う場面が多い。

#### スレッド

プログラムがタスクを完了させるのに使用できる単一のプロセスのこと。
各スレッドは1度に1つのタスクを実行することしかできない。

    Task A --> Task B --> Task C
この場合、各タスクは順次実行される。

現在多くのコンピューターは複数のコアを持つため、同時に複数のタスクを処理できる。

    Thread 1: Task A --> Task B
    Thread 2: Task C --> Task D

しかし、**JavaScriptはシングルスレッド**なのでメインスレッドと呼ばれる単一のスレッド上でタスクを実行できるだけ。

    Main thread: Task A --> Task B
Web workers によって worker と呼ばれる別個のスレッドに JavaScript の処理の一部を移すことが可能となり、複数のコードを同時に実行できるようになった。(マルチスレッドのこと、非同期処理とは別)

    Main thread: Task A --> Task C
    Worker thread: Expensive task B

workerにはいくつか問題があった(DOM操作ができないなど)ので、その解決のためにブラウザーを利用して特定の処理を非同期に実行する。
具体的には、`Promise`のような機能を利用することで、ある処理（例：サーバーからの画像の取得）を実行し、その結果が返ってくるまで別の処理の実行を待たせる、といったことが可能。

    Main thread: Task A               Task B
    Promise:      |__async operation__|
この Promise の処理はどこか別の場所で行われるため、非同期処理が実行されている間にメインスレッドがブロックされることは無い。

### 改めてPromise

* [プロミスの使用 - MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises)
* [Promise - MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Promise)
*  [【JavaScript】非同期処理 まとめ - Zenn](https://zenn.dev/tentel/articles/8146043d1101b5ea873d#promise-%E3%81%AE%E5%9F%BA%E6%9C%AC%E7%90%86%E8%A7%A3)
*  [【ES6】 JavaScript初心者でもわかるPromise講座](https://qiita.com/cheez921/items/41b744e4e002b966391a)

> プロミス (Promise) は、非同期処理の最終的な完了もしくは失敗を表すオブジェクトです。

* プロミスを使った非同期処理では、本来返したい戻り値の代わりに`Promise`というオブジェクトを返しておき、**本来返したい値**を渡せる状態になったら、そのプロミスオブジェクトを通して呼び出し元に値を渡す。
* 非同期処理に、処理の順番の**約束(=プロミス)を取り付ける**ようなイメージ。

#### 引数

引数には関数を渡し、その関数の引数として`resolve`、`reject`(関数)を渡す。

```js
new Promise(function (resolve, reject){
  // 非同期処理
})
```

それぞれ以下のような役割。

* `resolve`：非同期処理が解決したことを知らせる。
  * `return`の代わりに`resolve`()と記述することで、非同期関数が**解決したこと**を知らせる。
* `reject`：非同期処理が拒否されたことを知らせる。
  * `return`の代わりに`reject`()と記述することで、非同期関数が**拒否されたこと**を知らせる。
  * 任意。

#### 3つの状態

`Promise`には3つの状態がある。

* pending：非同期処理の実行中の状態を表す
* fulfilled：非同期処理が解決した状態を表す
* rejected：非同期処理が拒否された状態を表す

```js
new Promise(function (resolve, reject){
  try {
    resolve(); // ==> fulfilled
  } catch (e) {
    reject(); // ==> rejected
  }
})
```

#### 動作

動作させてみる。
とりあえず`Promise`を利用しないパターン。
`setTimeout`の処理の完了は待たれない。

```js
console.log("1番目");

// 1秒後に実行する処理
setTimeout(() => {
  console.log("2番目(1秒後に実行)");
}, 1000);

console.log("3番目");

// > 1番目
// > 3番目
// > 2番目(1秒後に実行)
```

次に、`Promise`を使ったパターン。
こちらは処理の完了を待つ。

```js
console.log("1番目");

new Promise((resolve) => {
  //1秒後に実行する処理
  setTimeout(() => {
    console.log("2番目(1秒後に実行)");
    resolve();
  }, 1000);
}).then(() => {
  console.log("3番目");
});

// > 1番目
// > 2番目(1秒後に実行)
// > 3番目
```

#### `then/catch`

返り値に対しては`then`(解決された時呼ばれる)`catch`(拒否された時呼ばれる)が使える。

* `pending` → `resolve` なら `then` が呼ばれる。
* `pending` → `reject` なら `catch` が呼ばれる。
* 返り値は`Promise`。
  * `catch`の場合も`fulfilled`な`Promise`が返ってくる。

```js
function asyncFunction() {
  return new Promise((resolve, reject) => {
    try {
      setTimeout(() => {
        console.log("1秒経過")
        resolve();
      }, 1000)
    } catch (e) {
      // 拒否されたときの処理
      reject();
    }
  })
}

asyncFunction().then(() => {
  console.log("resolve後の処理");
}).catch(e => {
  console.log("reject後の処理");
})

// > Promise {<pending>}
// > 1秒経過
// > resolve後の処理
```

#### 非同期処理中に取得した値を使いたい場合

* `then/catch`は引数を取ることができる。
* `resolve/reject`に引数を渡すことで、次に呼ばれる`then/catch`の第1引数に渡すことが出来る。

```js
function asyncFunction() {
  return new Promise((resolve, reject) => {
    try {
      setTimeout(() => {
        console.log("1秒経過")
        const num = 1 // 何らかの値を取得したとする
        resolve(num); // 取得した値をthenに渡す
      }, 1000)
    } catch (e) {
      reject(e);      // キャッチしたエラーを渡す
    }
  })
}

asyncFunction().then( num => {
  console.log(`引数で受け取った値：${num}`);
}).catch(e => {
  console.log(`引数で受け取った値：${e}`);
})

// > Promise {<pending>}
// > 1秒経過
// > 引数で受け取った値：1
```

#### プロミスの連鎖

* 非同期処理の**連鎖**(前の処理が成功したとき、その結果を使って後続の操作を開始)が可能。
  * `then`や`catch`は新しい`Promise`を返すため。
  * 非同期処理.then().catch()といった形でメソッドチェーンを使う事もできる。
* `then`は最大2つの引数を取る。
  * 1番目の引数 プロミスが解決した場合のコールバック関数
  * 2番目の引数 拒否された場合のコールバック関数

```js
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('foo');
  }, 300);
});

myPromise
  .then(handleResolvedA, handleRejectedA)
  .then(handleResolvedB, handleRejectedB)
  .then(handleResolvedC, handleRejectedC)
  .catch(handleRejectedAny);
```

アロー関数で表すとこうなる。

```js
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('foo');
  }, 300);
});
promise1
.then(value => { return value + ' and bar'; })  //resolveに渡した'foo'が引数
.then(value => { return value + ' and bar again'; })
.then(value => { console.log(value) })
.catch(err => { console.log(err) });

// > Promise {<pending>}
// > foo and bar and bar again
```

#### `Promise.all`

配列として`Promise`オブジェクトを渡す。
`all`に渡された全ての`Promise`が`resolve`されたら次の処理に進む。

```js
Promise.all([promise1, promise2]).then(() => {
  console.log("全部終了!");
});
```

#### `Promise.race`

allと同じく配列として`Promise`を渡す。
どれか一つでも`resolve`されたら次に進む。

```js

Promise.race([promise1, promise2]).then(() => {
  console.log("どれか一つ終了!");
});
```

### async/await

* [非同期関数 - MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/async_function)
* [await - MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/await)
* [async/await 入門（JavaScript）](https://qiita.com/soarflat/items/1a9613e023200bbebcb3)

`async / await`は`Promise`の糖衣構文。

糖衣構文(syntax sugar)
> シンタックスシュガーとは、プログラミング言語で、ある構文を別の記法で記述できるようにしたもの。長い構文を簡略に記述できるようにしたり、複雑な構文を読み書きしやくするために用意される。
> [IT用語辞典](https://e-words.jp/w/%E3%82%B7%E3%83%B3%E3%82%BF%E3%83%83%E3%82%AF%E3%82%B9%E3%82%B7%E3%83%A5%E3%82%AC%E3%83%BC.html)

```js
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}

async function asyncCall() {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
}

asyncCall();
// => "calling"
// => "resolved"
```

* `async`から関数式を書き始めることで、**非同期関数**を定義できる。
  * 値を`return`した場合、`Promise`は返り値を`resolve`する。
  * 例外、何かしらの値を`throw`した場合はその値を`reject`する。
* 関数の前に`await`を置くことで、その関数のプロミスが解決するか拒否されるまで処理を一時停止する。
  * `await`は必ず`async function`内で使う。
  * この動作を利用して、プロミスを返す関数をあたかも同期しているかのように動作させることが出来る。

#### 具体例

参考 : [連続した非同期処理](https://qiita.com/soarflat/items/1a9613e023200bbebcb3#%E9%80%A3%E7%B6%9A%E3%81%97%E3%81%9F%E9%9D%9E%E5%90%8C%E6%9C%9F%E5%87%A6%E7%90%86asyncawait%E6%A7%8B%E6%96%87)

* 画像の読み込みなど、前の処理の完了を待つ必要がないような場合には連続した非同期処理を使わない方が良い。

```js
function sampleResolve(value) {
  return new Promise(resolve => {
        setTimeout(() => {
            resolve(value);
        }, 2000);
    })
}

async function sample() {
    return await sampleResolve(5) * await sampleResolve(10) + await sampleResolve(20);

async function sample2() {
    const a = await sampleResolve(5);
    const b = await sampleResolve(10);
    const c = await sampleResolve(20);
    return a * b + c;
}

sample().then((v) => {
    console.log(v); // => 70
});

sample2().then((v) => {
    console.log(v); // => 70
});
```

参考 : [並列の非同期処理](https://qiita.com/soarflat/items/1a9613e023200bbebcb3#%E4%B8%A6%E5%88%97%E3%81%AE%E9%9D%9E%E5%90%8C%E6%9C%9F%E5%87%A6%E7%90%86)

並列の非同期処理（Promise構文）

```js
function sampleResolve(value) {
  return new Promise(resolve => {
        setTimeout(() => {
            resolve(value);
        }, 2000);
    })
}

function sampleResolve2(value) {
  return new Promise(resolve => {
        setTimeout(() => {
            resolve(value * 2);
        }, 1000);
    })
}

function sample() {
    const promiseA = sampleResolve(5);
    const promiseB = sampleResolve(10);
    const promiseC = promiseB.then(value => {
        return sampleResolve2(value);
    });

    return Promise.all([promiseA, promiseB, promiseC])
        .then(([a, b, c]) => {
            return [a, b, c];
        });
}

sample().then(([a, b, c]) => {
    console.log(a, b, c); // => 5 10 20
});
```

並列の非同期処理（async/await構文）

Promise.allにもawaitを利用できるため、以下のように記述できる。

```js
function sampleResolve(value) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(value);
        }, 2000);
    })
}

function sampleResolve2(value) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(value * 2);
        }, 1000);
    })
}

async function sample() {
    const [a, b] = await Promise.all([sampleResolve(5), sampleResolve(10)]);
    const c = await sampleResolve2(b);

    return [a, b, c];
}

sample().then(([a, b, c]) => {
    console.log(a, b, c); // => 5 10 20
});
```

array.map()も利用できる。

```js
function sampleResolve(value) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(value);
        }, 2000);
    })
}

async function sample() {
    const array =[5, 10, 15];
    const promiseAll = await Promise.all(array.map(async (value) => {
        return await sampleResolve(value) * 2;
  }));

    return promiseAll;
}

sample().then(([a, b, c]) => {
    console.log(a, b, c); // => 10 20 30
});
```

### 課題 APIを使ってなにか作ってみる

[無料のAPI](https://github.com/public-apis/public-apis)を使用して拡張機能を構築してみる

## `Emoji-have`を使って拡張機能を作る

[Emoji-have](https://github.com/cheatsnake/emojihub)というAPIを使ってみます。

以下のようなことが出来るAPIです。面白そうですね。

* カテゴリ別に絵文字を取得
* ランダムに取得/全て取得

なにか絵文字を使いたいけど具体例が思いつかない・・・
というときに使える拡張機能を作りました！~~そんな時無いけど~~

### イメージ

カテゴリ別にボタンを用意しておく
→ボタンを押す
→対応するカテゴリの絵文字を表示する
→コピーできる

### 実装

**ボタンを追加**

```html
<div class="btn-field">
	<button class="search-btn">smileys_and_people</button>
	<button class="search-btn">animals_and_nature</button>
	<button class="search-btn">food_and_drink</button>
	<button class="search-btn">travel_and_places</button>
	<button class="search-btn">activities</button>
	<button class="search-btn">objects</button>
	<button class="search-btn">symbols</button>
	<button class="search-btn">flags</button>
</div>
```

**JSからボタン取得**

- 複数なので `getElementByClassName` を使ってみる

```js
const buttons = document.getElementsByClassName("search-btn")

console.log(buttons[0].textContent) // => smileys_and_people
```

**ボタンにイベント追加**

- `forEach` で追加を試みる

```js
buttons.forEach(button => {
	button.addEventListener('click', clickButton)
});
```

![error](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/b4f08ae0-db4c-313c-7269-d95586630a8a.png)

・・・あれ？

[MDN - indexed collection](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections#working_with_array-like_objects)

どうやらHTMLCollectionには `forEach` メソッドがないようです。
代わりに以下のように呼び出します。

```js
Array.prototype.forEach.call(buttons, button => {
	button.addEventListener('click', clickButton)
});
```

**イベントからボタンのテキストを取得**

- `event.target.textContent` でボタンのテキストを取得します。
- ボタンのテキストを絵文字をゲットする関数に渡して何かします。

```js
const clickButton = e => {
	// イベントからボタンのテキストを取得
	const buttonText = e.target.textContent
	// 何かする
	getRandomEmoji(buttonText)
}
```

**絵文字APIを叩く関数**

- ひとまず実行してみます。

```js
const getRandomEmoji = async (buttonText) => {
	try {
		await axios
			.get(`https://emojihub.herokuapp.com/api/random/category_${buttonText}`)
			.then((response) => {
				console.log(response)
				loading.style.display = 'none';
				results.style.display = 'block';
			});
```

レスポンスは以下。
![api-get-result](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/181c03b3-3d3e-7ac7-e92d-79410b720b76.png)
どれが絵文字・・・？

READMEを見に行きます。

![Emoji-have-README](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/ad3b9b38-bd23-d773-c859-8190a5517dc5.png)

どこかに`name`, `htmlCode`などのデータがまとめて入っている感じのようです。
中身を見てみた感じだと、 `data` > `htmlCode/unicode` に入ってるみたいですね。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/90b8461d-5d35-f91d-9e86-b5e393efedc1.png)


試しにHTMLに貼ってみます。

![trying-html-paste](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/4473fa5d-29f0-ed91-3693-48b30579ff91.png)


OK！

実際に表示してみます。

```js
const clickButton = e => {
	// イベントからボタンのテキストを取得
	const buttonText = e.target.textContent
	getRandomEmoji(buttonText)
}

const getRandomEmoji = async (buttonText) => {
	try {
		await axios
			.get(`https://emojihub.herokuapp.com/api/random/category_${buttonText}`)
			.then((response) => {
				loading.style.display = 'none';
				result.style.display = 'block';
				const emoji = response.data.htmlCode[0]
				result.textContent = emoji
			});
	} catch (error) {
		console.log(error);
		loading.style.display = 'none';
		result.style.display = 'none';
		errors.textContent = 'Sorry, something went wrong.';
	}
};
```

![some-failure-emoji-view](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/848dc82a-f6a5-7447-f30e-57a49ae9bd64.png)


あれ？

HTMLを見てみると、以下のようになっていました。

```html
<!-- 表示されていたHTML -->
<p class="emoji" style="display: block;">&#129409;</p>

<!-- 実際のコード（HTMLとして編集を選択） -->
<p class="emoji" style="display: block;">&amp;#129409;</p>
```

### 状況の整理

#### APIから返ってくる値

* `HTMLCode` → [数値文字参照](https://e-words.jp/w/%E6%96%87%E5%AD%97%E5%8F%82%E7%85%A7.html#:~:text=character%20entity%20reference)

  * **数値文字参照**
  表記したい文字をUnicode/ISO 10646の文字番号（コードポイント）で表す方式で、十進数を用いる場合は「&#番号;」、16進数を用いる場合は「&#x番号;」のように表記する。
  * **文字実体参照**
  [MDN - エンティティ](https://developer.mozilla.org/ja/docs/Glossary/Entity)
  仕組みは数値文字参照と一緒。予め言語仕様で定義された文字が使える。

* `unicode` → 絵文字に割り当てられたunicode

|  | HTMLで絵文字表示 | HTMLで絵文字コード表示 | JSから絵文字挿入 | JSから絵文字コード挿入 |
| --- | --- | --- | --- | --- |
| 入力 | 🐩 | `&#128041;` | 🐩 | `&#128041;` |
| 出力 | 🐩 | 🐩 | 🐩 | `&#128041;` |

JSから絵文字コードを挿入すると、 絵文字コード⇔絵文字の変換が行われず、`&` がHTMLに挿入されるときに `&amp:`(文字実体参照)に変換されるみたいですね。

### 解決策 UniCode文字列を絵文字に変換する。

絵文字そのままINが問題ないなら、そもそも絵文字に変換してから挿入すればいいのでは？

U+は16進数を表すらしいので、 U+1F33D → 0x1F33D かな？

```js
> String.fromCharCode(0x1F33D);
''
```

・・・？

#### サロゲートペア

[参考記事 - Qiita](https://qiita.com/YusukeHirao/items/2f0fb8d5bbb981101be0)

Unicode番号が16進数で`10000`以上の文字を、UTF-8(およびUTF-16)では表現できないため、Unicode番号`D800`〜`DBFF`と`DC00`〜`DFFF`の組み合わせで表現した仕組み。

要するに、実際は組み合わせで表されてるよ〜ということらしい。

[fromCodePoint](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCodePoint) というメソッドを使えば解決できそう。

```js
> String.fromCodePoint(0x1F33D);
'🌽'
```

あとは `U+` を `0x`に置換すればOKですね。

```js
emojiUnicode =  emojiUnicode.replace("U+", "0x");
```

[MDN - replace](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

`replace` の返り値は文字列なのですが、 そのまま`String.fromCodePoint` に渡しても普通に動作しました。 `String.fromCodePoint` の引数には [codepoints](https://developer.mozilla.org/en-US/docs/Glossary/Code_point)としか書かれていないので、そういうものなのでしょうか。

最後にボタンを押したら絵文字をクリップボードにコピー出来るようにします。
ボタン押下のアニメーション等は付けていませんが、まぁ良いでしょう。

[クリックしたらコピー 参考](https://qiita.com/butakoma/items/642c0ec4b77f6bb5ebcf)

```js
// クリップボードに絵文字をコピー
const emoji = result.textContent;
navigator.clipboard.writeText(emoji);
```

完成！！

![emoji-demo](https://user-images.githubusercontent.com/85564407/151686789-796abc39-3e3f-45b0-9a88-798e7c1cfd92.gif)

最終的なコード

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<meta http-equiv="X-UA-Compatible" content="ie=edge" />
		<title>My Carbon Trigger</title>
		<link rel="stylesheet" href="./styles.css" />
	</head>

	<body class="container">
		<img alt="emoji" src="images/emoji.jpeg" />
		<div>
			<h1>Welcome to Emoji app!</h1>
		</div>
		<div>
			<h2>To get random emojis 🎲 </h2>
		</div>
		<div class="btn-field">
			<button class="search-btn">smileys_and_people</button>
			<button class="search-btn">animals_and_nature</button>
			<button class="search-btn">food_and_drink</button>
			<button class="search-btn">travel_and_places</button>
			<button class="search-btn">activities</button>
			<button class="search-btn">objects</button>
			<button class="search-btn">symbols</button>
			<button class="search-btn">flags</button>
		</div>

		<div class="result">
			<div class="loading">loading...</div>
			<div class="errors"></div>
			<div class="data"></div>
			<div role="img" aria-label="emoji">
				<p><strong>Emoji</strong></p>
				<p class="emoji"></p>
			</div>
		</div>

		<button id="copy">Copy!</button>

		<script src="main.js"></script>
	</body>
</html>
```

```js
import axios from 'axios';

// ボタン
const searchButtons = document.getElementsByClassName("search-btn");
const copyButton = document.getElementById("copy");
// リザルト
const errors = document.querySelector('.errors');
const loading = document.querySelector('.loading');
const result = document.querySelector('.emoji');

const clickSearch = e => {
	// イベントからボタンのテキストを取得
	const buttonText = e.target.textContent;
	getRandomEmoji(buttonText);
}

const clickCopy = e => {
	// クリップボードに絵文字をコピー
	const emoji = result.textContent;
	navigator.clipboard.writeText(emoji);
}

const getRandomEmoji = async (buttonText) => {
	try {
		await axios
			.get(`https://emojihub.herokuapp.com/api/random/category_${buttonText}`)
			.then((response) => {
				loading.style.display = 'none';
				result.style.display = 'block';
				let emojiUnicode = response.data.unicode[0];
				// unicode の U+ → 16進数リテラルに変換
				emojiUnicode =  emojiUnicode.replace("U+", "0x");
				// unicode → 絵文字へ変換
				const emoji = String.fromCodePoint(emojiUnicode);
				result.textContent = emoji;
			});
	} catch (error) {
		console.log(error);
		loading.style.display = 'none';
		result.style.display = 'none';
		errors.textContent = 'Sorry, something went wrong.';
	}
};

Array.prototype.forEach.call(searchButtons, button => {
	button.addEventListener('click', clickSearch);
});

copyButton.addEventListener("click", clickCopy);
```

### せっかくなのでGithubに上げる

練習も兼ねてGithubに上げる＆READMEを書きました。
READMEに動画を載せたかったので下の記事を参考にしました。

[READMEに動画を載せる](https://qiita.com/i-to-to-to-mi/items/e73eb0a5899f111d0e64)
https://github.com/Westen0511/emoji-app

## 3-バックグラウンドタスクとパフォーマンス

- バックグラウンドタスク
    - 拡張機能のアイコンの色を更新する
- パフォーマンスの改善について

### パフォーマンス

開発者ツールから、パフォーマンスに関する情報を収集してみる

![performance](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/a21cd584-1ab3-30c4-4ba8-cb362404e373.png)

わかりやすいのはここ。

![performance-graf](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/440bd916-0363-29a0-3470-097239edd482.png)


どの処理が表示速度低下に繋がっているのかを可視化できる、という感じ？
パフォーマンスに関しては正直余りイメージが沸かない。ので、今後やるべき時になったらやる。


参考になりそう

* [Chrome DevToolsを用いたメルカリWebのパフォーマンス計測](https://engineering.mercari.com/blog/entry/2018-12-12-090156/)
* [Webパフォーマンス虎の巻 - Qiita](https://qiita.com/usagi-f/items/10f35969f08dd01fa635)
* [Webフロントエンド ハイパフォーマンス チューニング](https://www.amazon.co.jp/dp/B0728K5JZV/ref=dp-kindle-redirect?_encoding=UTF8&btkr=1)

> パフォーマンス向上に対する施策は大別すると以下の２通り
**軽量化** （単純にやりとりするデータ容量を小さくすること）
    ・　圧縮
    ・　削除
**最適化** （その時に最も適している実装・実行をとること）
    ・　経路・順番の変更
    ・　非同期
もっとも遅くしている原因を探して、それを対策するのが原則。「対効果」が絶対的正義である。手段から入るのは愚策。まず先に原因を知ることが重要。

### トピック

- サイトパフォーマンスを正確に把握したい場合キャッシュをクリアすると良い
- 近年Webでは「重たい」アセット(画像など)を扱うことが増えている
    - 画像が最適化され、ユーザにとって適切なサイズ・解像度になっていると良い
- HTML/CSS/JSを最適化しよう
    - ブラウザはHTMLに忠実にDOMを構築するので、使用するタグを最小限に抑えると良い
    - 1つのページでしか使わないスタイルはメインページのCSSに含まないようにしよう
    - JSが読み込まれるタイミングに注意
        - 場合によっては `defer` を検討
- [Site Speed Test の Web サイト](https://www.webpagetest.org/)でサイトパフォーマンスを測る事ができる

### バックグラウンドタスクの実装 色を計算する関数の追加

```js
function calculateColor(value) {
	let co2Scale = [0, 150, 600, 750, 800];
	let colors = ['#2AA364', '#F5EB4D', '#9E4229', '#381D02', '#381D02'];

	let closestNum = co2Scale.sort((a, b) => {
		return Math.abs(a - value) - Math.abs(b - value);
	})[0];
	console.log(value + ' is closest to ' + closestNum);
	let num = (element) => element > closestNum;
	let scaleIndex = co2Scale.findIndex(num);

	let closestColor = colors[scaleIndex];
	console.log(scaleIndex, closestColor);

	chrome.runtime.sendMessage({ action: 'updateIcon', value: { color: closestColor } });
}
```

#### sort

```js
	let closestNum = co2Scale.sort((a, b) => {
		return Math.abs(a - value) - Math.abs(b - value);
	})[0];
```

- [MDN - sort](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
- 比較関数を渡すと、その結果に応じてソートできる
    - 通常は `a-b` のように普通の計算式を使う
- a, bを使った計算で値が負の場合は `a` をより小さいインデックスに移動する
    - つまり `a` を前にソートする
- 例えば40と100を比べる時は compare(40,100)となり、関数は40-100=-60(負の値)を返す
    - 40のほうが小さいため前にソートされる
- 結果が正の場合はその逆に動く
- 降順/昇順を入れ替えたければ比較関数の中身を変えればいい

#### findIndex

```js
let num = (element) => element > closestNum;
let scaleIndex = co2Scale.findIndex(num);
```

以下のコードと同じ動きをする。

```js
let scaleIndex = co2Scale.findIndex( e => e > closestNum )
```

- [MDN - findIndex](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
- JavaScriptの `findIndex` は関数を受け取り、指定のテスト関数に合格する最初の要素を返す。
    - 今回の場合 `value` が300だとすると `closestNum` は150なので返ってくるインデックスは `2`

#### chrome.runtime

```js
chrome.runtime.sendMessage({ action: 'updateIcon', value: { color: closestColor } });
```

[chrome.runtime](https://developer.chrome.com/docs/extensions/reference/runtime/)にはさまざまなバックグラウンドタスクを処理するAPIがある。

ここではアイコンの変更のみ行っているが、以下のようなこともできる。

- バックグラウンドページを取得
- マニフェストの詳細を返す
- アプリや拡張機能のライフサイクルでイベントを監視して応答する
- URL の相対パスを完全修飾 URL に変換する

#### デフォルトアイコン色設定

```js
chrome.runtime.sendMessage({
	action: 'updateIcon',
		value: {
			color: 'green',
		},
});
```

### 関数呼び出し、実行

APIを呼ぶ関数に以下を追加

```js
calculateColor(CO2);
```

`/dist/background.js` でバックグラウンドアクションの呼び出し用リスナーを追加

```js
chrome.runtime.onMessage.addListener(function (msg, sender, sendResponse) {
	if (msg.action === 'updateIcon') {
		chrome.browserAction.setIcon({ imageData: drawIcon(msg.value) });
	}
});

function drawIcon(value) {
	let canvas = document.createElement('canvas');
	let context = canvas.getContext('2d');

	context.beginPath();
	context.fillStyle = value.color;
	context.arc(100, 100, 50, 0, 2 * Math.PI);
	context.fill();

	return context.getImageData(50, 50, 100, 100);
}
```

canvasを使って丸を書いて色を塗っている感じ。(canvasは後で触れるため割愛)

完成！
![carbon-trigger](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/a33e338d-f958-abb8-b241-326e0e74a283.png)


### 学んだこと

- フォームの構築
- ローカルストレージの利用
- APIの呼び出し、`axios`概要
- `Promise`概要
- `async/await`概要
- APIを使った簡単な拡張機能の構築
    - 文字コードの扱い
- パフォーマンスの測定、バックグラウンドタスク
