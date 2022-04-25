# はじめに

python-pptxとPySimpleGUIを使って、PowerPointで指定したフォーマットに画像を貼り付ける事ができるツールを作ったので紹介します。

## 開発の経緯

現職では主に製品の実証試験的な業務を担当しています。
業務の性質上、エビデンスとして画像を撮影 → PowerPoint(報告用)に貼り付ける という作業が多く発生します。。

そういった作業が多くあるので既に効率化は図られていて、「枚数を指定すると定間隔で画像を貼り付けてくれるツール」は存在します。(他部署が作成)

しかし、実際に報告資料を作成する際に欲しいのは**決まったフォーマット・画像の配置**であることが多いです。
そのため、定間隔で貼り付けることが出来たとしてもそれをそのまま報告に使うことはほとんど出来ず、結局手作業でパワポに画像をペタペタしている人が多くいます。

そこで、上司に相談して時間をもらい、

①フォーマットを自由に指定出来る
②PowerPointを使って(=誰でも使える)フォーマットを指定できる
③テキストをデータ名に置換出来たりすると嬉しい

という要素を持つツールを作成しました。

基本機能 3日 + リファクタリング 1日で完成させました。

## 作ったもの

PowerPointで作成したフォーマットを使用して画像貼り付け・テキスト置換を行います。

![PowerPointGenerator_特定レイアウト_デモ](https://user-images.githubusercontent.com/85564407/165084584-f053af27-3270-483d-a5b9-ba40b46f37da.gif)

**主な機能**

- 1データに画像が複数存在する場合、指定したラベル位置に画像を貼り付ける事ができます。
  - 1データに対して複数のレイアウト(正面、背面、側面、、、)の画像が存在するイメージです。
- 連番になっているデータ(1データ1画像)の場合、指定した位置に対して順番に画像を貼り付ける事ができます。
- 四角形 → 画像 への置換
  - 四角形の配置 = 画像の配置
  - 四角形のテキスト = 画像のラベル
  - 画像はデータ名とラベルを「 _ 」で区切る
- テキストの置換
  - @1 (@ + 数字) = データ名へ置換
  - #1 (# + 数字) = ラベルへ置換

### 1データに複数画像が存在する場合(ラベル位置への貼付け)

1データに画像が複数存在する場合、ラベルの位置を指定することで画像を配置します。

**入力フォーマット**

ラベルを指定します。

- 1枚のスライドに1グループの場合は「ラベル名」のみ指定します。
- 1枚のスライドに複数グループが存在する場合、`_` で「連番」と「ラベル名」を区切って指定します。
- PowerPointで指定するラベル名と画像のラベル名は一致させる必要があります。

下の例では 2データ/1スライド なので、「1_右」, 「2_右」のように `_` で「連番」と「ラベル名」を区切ります。
![ラベリング_フォーマット](https://user-images.githubusercontent.com/85564407/165007818-aa214818-b1c2-4a6d-a8a8-8195f7458766.png)

※ ラベル位置貼り付けの場合はテキスト置換を使う必要が無い(毎回ラベルが同じになるため)ので、置換ラベル(#〇〇)の指定順序がおかしいように思えるのは正しいです。特に順番を指定していないのでこうなっています。

**入力画像**

ねずみ_右の場合は「ねずみ」がデータ名 /「右」がラベルとして扱われます。
![image](https://user-images.githubusercontent.com/85564407/165009884-babf36f4-3558-493b-ad4e-54f3cec36d40.png)

**出力されるPowerPoint**

1枚目
![ラベリング 出力_1](https://user-images.githubusercontent.com/85564407/165007834-7e7db6df-e4a0-432d-ab74-d615ac6f2e33.png)
2枚目
![ラベリング 出力 2](https://user-images.githubusercontent.com/85564407/165009914-4737f8af-1c0d-4c4a-a169-a5156a229505.png)

### 1データに画像が1枚の場合(連番貼り付け)

連番になっているデータの場合、スライドを跨いで順番に画像を貼り付ける事ができます。

**入力フォーマット**

四角形の中に数字を指定します。
![順に貼り付け_フォーマット](https://user-images.githubusercontent.com/85564407/165007744-6061d6e1-22b3-46e7-9d18-9f0f1b865cd8.png)

**入力画像**

fruits_1の場合は「fruits」がデータ名、「1」がラベル(連番)として扱われます。
![image](https://user-images.githubusercontent.com/85564407/165010477-72faaf06-943e-4dda-9170-b9bcca155da9.png)

**出力されるPowerPoint**

連番は0埋めの有無に関係なく、数値の大小で判定されます。

1枚目
![順に貼り付け_出力 1](https://user-images.githubusercontent.com/85564407/165007794-211c05cf-76d9-4563-9d48-42d91bb12728.png)
2枚目
![順に貼り付け_出力 2](https://user-images.githubusercontent.com/85564407/165010628-b2cc1a2c-2767-4cdc-ac12-31311f456887.png)

### 動作サンプルに使用した画像

- [【フリーアイコン】 フルーツ](https://sozai.cman.jp/icon/food/fruits/)
- [【フリーアイコン】 矢印（上下左右）](https://sozai.cman.jp/icon/arrow/base1/)

# 実装

## 動作環境

- Windows10
  - Macでも動作するとは思いますが、一部機能(主にPySimpleGUI)が使えない、`pathlib`等のOSにより挙動が変わるライブラリにより影響が出る可能性があります。
  - ~~Mac使ってる人にパワポ職人はいないと信じているので大丈夫でしょう~~
- Python 3.10.2
- python-pptx 0.6.21
- PySimpleGUI 4.59.0

必要なライブラリをインストールします。
僕はpipenvを使っているのでpipenvでインストールしました。適宜読み替えてください。

```shell
pip install python-pptx
pip install PySimpleGUI
```

## python-pptx

公式ドキュメントに基本的な使い方はだいたい載っています。
[python-pptx — python-pptx 0.6.21 documentation](https://python-pptx.readthedocs.io/en/latest/index.html)

こちらのサイトもわかりやすいです。
[【Python×PowerPoint】python-pptxの導入~ファイル・スライド作成方法を徹底解説 | Pythonでもっと自由を](https://www.shibutan-bloomers.com/python-libraly-pptx/988/)

### 基本的な使い方

> ![about-python-pptx-shape](https://www.shibutan-bloomers.com/wp-content/uploads/2021/10/634b5ac5a6b977e5b32c1c9b8ad3c941.png)
> https://www.shibutan-bloomers.com/python-libraly-pptx-5/1188/より

基本的な構成は上のイメージです。
図形やテキストボックス等の1つ1つの要素はShapeオブジェクトとして管理されています。

#### Presentation

何をするにもまずは`Presentation`オブジェクトにアクセスします。

```python
# 引数として渡したPowerPointを開く
prs = pptx.Presentation("./sample.pptx")

# 空のPresentationを作ることも出来る
prs = pptx.Presentation()
```

`save`にパスを渡すことで保存することが出来ます。

```python
prs.save('./sample.pptx')
```

#### Slides

ファイルを構成する全てのスライドは`Slides`コレクションで管理されています。

```python
# Slidesコレクション取得
slides = prs.slides

# 1枚目のスライドを取得
slide = slides[0]

# 末尾にスライドを追加 返り値は追加されたスライド
added_slide = slides.add_slide(side_layouts)
```

#### slide_layouts

`slide_layouts`は、スライドのプレースホルダ(雛形みたいなもの)です。
`Presentation`オブジェクトからアクセスします。

主に`slides.add_slide`でスライドを追加する時に使います。

> ![side_layouts](https://www.shibutan-bloomers.com/wp-content/uploads/2020/12/8c1ee537ad885f2763fc43980ffeac44.png)

```python
layout = prs.slide_layouts[0]

# 名前で取得することも可能
layout = prs.slides.get_by_name("白紙")
```

#### Shape

`Shape`オブジェクトにアクセスしたい場合、対象のオブジェクト(`Slide`)の`shapes`プロパティにアクセスします。
`shapes`は、スライド内にあるすべての要素を管理するイテラブルオブジェクトです。

```python
shapes = slide.shapes
shape = shapes[0]
```

### 図形の判定

### 図形の持つ情報

### python-pptxの単位

### スライドの複製

### スライドから特定の要素を削除

### 実装内容

書き込みにおける実際の実装は以下のような流れです。

1. 設定用のPowerPointを複製
2. 複製したPowerPointにアクセス
3. ベースとなるスライドの置換対象図形・テキストボックスを削除
4. ベースとなるスライドを必要な枚数複製
5. 各スライドに画像・テキストボックスを出力
6. ベースとなるスライドを削除

何故こんな面倒なことをしたかというと、以下のような制約からです。

- 全く同一の`slide_layouts`だったとしてもファイルを跨いで`slide_layouts`を使用することは出来ない。
  - `add_slide`には`slide_layouts`が必要。
- 表を作ってその中に画像を入れることが多い関係で、置換対象以外の図形は残しておきたい。
  - 何故か表の中に画像を配置することが多いのです。見栄えが良いからでしょうか。

# hoge

TODO どこかに入れる
PowerPointに詳しくなりたいわけではないので、一部面倒な処理はStackOverFlowからコピペしてきました。


## 工夫点

### 使用までのハードルを下げる

非IT系、特に高齢の方が多い部署では自動化への壁が多くあります。
折角便利なツールを作成したとしても、ツールの使い方を覚えなければいけない、導入が面倒などの理由で使ってもらえないことも多くあります。

自身の観測範囲内ではありますが、以下のようなツールが好まれる傾向にあるようです。

① PowerpointやExcel(=**使い慣れている**)で設定ができる
② インストール不要、自分のPCにコピーすれば使える

①についてはPowerPointでフォーマットを指定できるようにして対処しました。
また、**慣れている**という点で、データ名とラベルの区切りには`_`を採用しました。

②についてはPyinstallerによるexe化がメジャー(?)なようですが、生成されるファイルのサイズが大きすぎるし、動作も安定しないので個人的にはあまり好みではありません。
それに、改修の度にexe化するのも面倒です。

- ユーザー視点でexe化と大差ない
- 改修が楽

上2つを満たす選択肢として、今回は**embeddable pythonによる配布**という方法を取りました。(Windows限定)

[こちらの記事](https://qiita.com/mm_sys/items/1fd3a50a930dac3db299)が詳しいですが、簡単に言うと最小限のPython実行環境をフォルダごと配布するようなイメージです。

デフォルトだとtkinter(及びそのラッパーであるPySimpleGUI)が使えないので[Stack Overflow](https://stackoverflow.com/questions/37710205/python-embeddable-zip-install-tkinter)を参考にtkinterを使えるようにしました。

### エラーを通知する

前述の他部署が作った画像貼り付けツールは、「入力したフォルダに画像が無い」「結果出力先に設定されているサーバが停止している」などの理由で正常に動作しなかった場合に何も通知してくれませんでした。

問題があったときに何も通知されない~~苛立ち~~不便さは身に沁みていたので、不正な入力があった時は考えうる操作ミスを通知するようにしました。

### 型ヒントの使用・docstringの記述

今までの開発では、「どうせ自分しか見ないソースコードだから」と型定義やdocstringは特に使用していませんでした。

しかし、実際の開発現場で個人で作業するということはまずないと思います。
他の人が参照する可能性のある変数やメソッドに型ヒント・ドキュメントが無いというのは中々に不便です。

そのため、意識付けも兼ねて型ヒントの使用やdocstring(Numpy記法)を書くことを意識して開発を進めました。

個人開発でも呼び出し側を書きやすい、エディタが型を勝手にチェックして警告を出してくれるので間違いに気づきやすいなどのメリットを享受出来たので、やってよかったです。

## 改善点

### テストを書いていない

- Web開発学習中のため、新しいテストフレームワークの使い方を覚えたくない
- 早く完成させたい

などの理由でテストを書かないことにしました。

この選択を開発中に何度も後悔しました。
テストを書かないことのデメリットは挙げるとキリがありませんが、例えば以下のような不便さを感じました。

- エラーがどこで起きているのか理解するまで時間がかかる
- 動作を確認するために軽いスクリプトを書く/GUIを操作する必要があり面倒
- 要件がハッキリしていないため(設計の問題でもある)、不要なメソッドを実装してしまう

今から書くのはちょっと面倒なので書きませんが、今後は何があろうがテストを書こうと決心しました。

### 設計が雑

主にクラスの役割の話になります。

SlideやImageなどのオブジェクトがあり、それ自体やその集合を持つクラスがあるという関係はそこそこ良い(と思っている)のですが、

- 画像・テキストボックスの整理を担当するクラス
- 「オブジェクトを所有するクラス」のオブジェクトへのアクセスの仕方

など、振り返ってみると雑な点が目に付きます。

設計時にデータの流れや各クラスの役割がハッキリしていなかったことが主な要因だと思います。
もっと綺麗に設計出来るようになりたいです。

### 追加要望があった機能

以下のような要望がありました。随時追加していきます。

- 画像のトリミング
  - トリミングしてから貼ることが多い人もいるため。
- テキストボックスのフォント・サイズ維持
  - フォント情報の取得を忘れていたため置換されるテキストはデフォルト設定になってしまう。

## 参考記事

embeddable python
[超軽量、超高速な配布用Python「embeddable python」 - Qiita](https://qiita.com/mm_sys/items/1fd3a50a930dac3db299)
[4. Windows で Python を使う — Python 3.10.4 ドキュメント](https://docs.python.org/ja/3/using/windows.html#the-embeddable-package)
embeddable python へtkinterを導入
[Python embeddable zip: install Tkinter - Stack Overflow](https://stackoverflow.com/questions/37710205/python-embeddable-zip-install-tkinter)

Python 型定義・ヒント
[[Python3.8～]ビルトインのTypedDictについて詳しく調べてみた（PEP589） - Qiita](https://qiita.com/simonritchie/items/63218b0a5c4a3d3632a1)
[[Python]PylanceのVS Code拡張機能をさっそく使ってみた。 - Qiita](https://qiita.com/simonritchie/items/33ca57cdb5cb2a12ae16)

その他
[製造現場向けの自動化ツールをPythonで作る時に留意すること - Qiita](https://qiita.com/banquet_kuma/items/ab30e69b999c2f451de3)