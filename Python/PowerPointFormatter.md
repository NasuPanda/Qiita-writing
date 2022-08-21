<!--
title: Pythonでパワポ報告資料作成を効率化する(誰でも使えるように)
tags: Python PowerPoint 業務効率化 Windows
-->

# はじめに

python-pptxとPySimpleGUIを使って**PowerPointで作ったフォーマット位置に画像を貼り付けるツール**を作ったので紹介します。

## 開発の経緯

現職では主に製品の実証試験的な業務を担当しています。
業務の性質上、エビデンスとして画像を撮影 → PowerPoint(報告用)に貼り付ける という作業が多く発生します。

そういった作業が多くあるので既に効率化は図られていて、「枚数を指定すると一定間隔で画像を貼り付けてくれるツール」は存在します。(DXする部署が作成)

しかし、実際に報告資料を作成する際に欲しいのは**決まったフォーマット・画像の配置**であることが多いです。
そのため、一定間隔で貼り付けることが出来たとしてもそれをそのまま報告に使うことはほとんど出来ず、結局手作業で画像の位置を調整している人が多くいます。

そこで、上司に相談したり、職場の方に聞き込みをしたりして、

1. フォーマットを自由に指定出来る
2. PowerPointを使って(=誰でも使える)フォーマットを指定できる
3. テキストをデータ名に置換出来たりすると嬉しい

という要素を持つツールがあれば良さそう、という結論に至ったので作りました。

だいたい3日で完成させました。

## 作ったもの

PowerPointで作成したフォーマットを使用して画像貼り付け・テキスト置換を行います。

![PowerPointGenerator_特定レイアウト_デモ](https://user-images.githubusercontent.com/85564407/165084584-f053af27-3270-483d-a5b9-ba40b46f37da.gif)

### 主な機能

- 1データに画像が複数存在する場合、指定したラベル位置に画像を貼り付けます。
  - 1データに対して複数のレイアウト(正面、背面、側面...)の画像が存在するイメージです。
- 連番になっているデータ(1データ:1画像)の場合、指定した位置に対して順番に画像を貼り付けます。
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

※ ラベル位置貼り付けの場合はテキスト置換を使う必要が無い(毎回ラベルが同じになるため)ので、置換ラベル(#〇〇)の順序がバラバラです。

**入力画像**

ねずみ_右の場合は「ねずみ」or「右」のどちらかをラベルとして指定します。
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

# 実装

https://github.com/NasuPanda/powerpoint-generator

## 動作環境

- Windows10
  - Macでも動作するとは思いますが、一部機能(主にPySimpleGUI)が使えない、`pathlib`等のOSにより挙動が変わるライブラリにより影響が出る可能性があります。
  - ~~Mac使ってる人にパワポ職人はいないと信じているので大丈夫でしょう~~
- Python 3.10.2
- python-pptx 0.6.21
- PySimpleGUI 4.59.0

必要なライブラリをインストールします。

```shell
pipenv install python-pptx
pipenv install PySimpleGUI
```

## python-pptx

python-pptxはその名の通りPythonからPowerPointを操作出来るライブラリです。

公式ドキュメントに基本的な使い方はだいたい載っています。
[python-pptx — python-pptx 0.6.21 documentation](https://python-pptx.readthedocs.io/en/latest/index.html)

日本語だとこちらのサイトがわかりやすいです。
[【Python×PowerPoint】python-pptxの導入~ファイル・スライド作成方法を徹底解説 | Pythonでもっと自由を](https://www.shibutan-bloomers.com/python-libraly-pptx/988/)

### 基本的な使い方

> ![about-python-pptx](https://www.shibutan-bloomers.com/wp-content/uploads/2021/10/634b5ac5a6b977e5b32c1c9b8ad3c941.png)
> https://www.shibutan-bloomers.com/python-libraly-pptx-5/1188/より

PowerPointの基本的な構成は上のようなイメージになっています。
図形やテキストボックス等の1つ1つの要素はShapeオブジェクトとして管理されています。

#### `Presentation`

まずは`Presentation`オブジェクトにアクセスします。

```python
# 引数として渡したPowerPointを開く
prs = pptx.Presentation("./sample.pptx")

# 空のPresentationを作ることも出来る
prs = pptx.Presentation()

# saveで保存
prs.save('./sample.pptx')
```

#### `Slides`

ファイルを構成する全てのスライドは`Slides`で管理されています。

```python
# Slidesコレクション取得
slides = prs.slides

# 1枚目のスライドを取得
slide = slides[0]

# 末尾にスライドを追加 返り値は追加されたスライド
added_slide = slides.add_slide(side_layouts)
```

#### `SlideLayout`

`SlideLayout`はスライドのプレースホルダです。
`Presentation`からアクセスします。

主に`Slides.add_slide`でスライドを追加する時に使います。

> ![side_layouts](https://www.shibutan-bloomers.com/wp-content/uploads/2020/12/8c1ee537ad885f2763fc43980ffeac44.png)

```python
layout = prs.slide_layouts[0]

# 名前で取得することも可能
layout = prs.slides.get_by_name("白紙")
```

### `Shape`

[Shapes — python-pptx 0.6.21 documentation](https://python-pptx.readthedocs.io/en/latest/api/shapes.html#shape-objects-in-general)

`Shape`オブジェクト(スライドが持つコンテンツ)にアクセスしたい場合、対象のオブジェクト(`Slide`)の`shapes`プロパティにアクセスします。

```python
shapes = slide.shapes
shape = shapes[0]
```

#### shapeの判定

定数として定義されている`MSO_AUTO_SHAPE_TYPE`や`MSO_SHAPE_TYPE`を使いました。

[Enumerations — python-pptx 0.6.21 documentation](https://python-pptx.readthedocs.io/en/latest/api/enum/index.html)

```py
for shape in shapes:
  if shape.shape_type == MSO_SHAPE.RECTANGLE:
      print("コレは四角形")
```

#### shapeの持つ情報

座標やサイズなど。

```py
left = shape.left
top = shape.top
width = shape.width
height = shape.height
text = shape.text

# add〇〇系のメソッドで使う
shapes.add_shape(autoshape_type_id, left, top, width, height)
```

#### 画像の挿入

```python
# image_fileは画像パス
picture = Shapes.add_picture(image_file, left, top, width, height)

# トリミングできる
picture.crop_bottom = 0.25
# 回転もできる
picture.rotation = 45 # +なら時計回り -なら反時計回り
```

#### テキストボックスの挿入

テキストボックスに限りませんが、テキストを扱うためには`text_frame`プロパティにアクセスします。
`TextFrame`は`paragraph`(段落)を持ちます。`paragraph`ごとにフォント・書式などの設定をするイメージです。

```python
txBox = sld0.shapes.add_textbox(left, top, width, height)    #Text Box Shapeオブジェクトの追加

tf = txBox.text_frame		# TextFrameオブジェクトの設定
tf.text = "This is text inside a textbox"            # TextFrameオブジェクトはデフォルトで1つ段落を持つ

p = tf.add_paragraph()		                           # paragraphオブジェクトの追加作成(2段落目)
p.text = "This is a second paragraph that's bold"    # textプロパティによる文字列の設定
p.font.bold = True		                               # font.boldプロパティによる太文字設定
```

### python-pptxの単位

デフォルトではemu(English Metric Units)という単位を使用しています。
1 cm = 360000 emuです。

今回は座標情報の取得 → 図形挿入をするだけなので、デフォルト単位のemuで問題なかったです。
サイズを直接指定したいときなど、人間がわかりやすいように加工する必要があれば`pptx.util`を`import`してきて変換することも出来ます。

* `Cm` : cm単位
* `Inches` : インチ単位
* `Pt` : ポイント単位

```py
from pptx.util import Cm, Inches, Pt

# emu→cmの場合
def emu_to_cm(left, top, width, height):
    """
    emu→cmに変換 (1cm = 360000emu)
    """
    return left/360000, top/360000, width/360000, height/360000

# cm→enumの場合
Cm(enum)
```

### スライドの複製

[Python-pptx: copy slide - Stack Overflow](https://stackoverflow.com/questions/50866634/python-pptx-copy-slide)を参考に。

```py
base_slide = prs.slides[base_slide_index]
duplicate_slide = prs.slides.add_slide(layout)
for shape in base_slide.shapes:
    el = shape.element
    new_el = deepcopy(el)
    duplicate_slide.shapes._spTree.insert_element_before(new_el, "p:extLst")
```

### スライドの削除

```py
xml_slides = prs.slides._sldIdLst
slides = list(xml_slides)
xml_slides.remove(slides[slide_index])
```

### スライドから特定の`shape_type`の要素を削除

[Is there a way to delete a shape with python-pptx - Stack Overflow](https://stackoverflow.com/questions/64700638/is-there-a-way-to-delete-a-shape-with-python-pptx)を参考に。

```py
shapes = prs.slides[slide_index].shapes
for shape in shapes:
    if not shape.shape_type == MSO_SHAPE.RECTANGLE:
        continue
    XML_reference = shape._sp
    XML_reference.getparent().remove(XML_reference)
```

## PySimpleGUI

PySimpleGUIはtkinter(Python標準GUI)のラッパーで、tkinterと比べて直感的にGUIを作る事が出来ます。

PySimpleGUIも使い方は公式ドキュメントにだいたい載っています。
[Call reference - PySimpleGUI](https://pysimplegui.readthedocs.io/en/latest/call%20reference/)
[Cookbook - PySimpleGUI](https://pysimplegui.readthedocs.io/en/latest/cookbook/)

### 基本的な使い方

`Window`の`layout`にリストとしてコンポーネントを配置していくだけで簡単にGUIを作ることが出来ます。
とっても直感的です。

> ```py
> 
> import PySimpleGUI as sg
> 
> sg.theme('DarkAmber')   # デザインテーマの設定
> 
> # ウィンドウに配置するコンポーネント
> layout = [  [sg.Text('ここは1行目')],
>             [sg.Text('ここは2行目：適当に文字を入力してください'), sg.InputText()],
>             [sg.Button('OK'), sg.Button('キャンセル')] ]
> 
> # ウィンドウの生成
> window = sg.Window('サンプルプログラム', layout)
> 
> # イベントループ
> while True:
>     event, values = window.read()
>     if event == sg.WIN_CLOSED or event == 'キャンセル':
>         break
>     elif event == 'OK':
>         print('あなたが入力した値： ', values[0])
> 
> window.close()
> ```
>
> ![PySimpleGUI-demo](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1224564/6933d135-78ac-3f37-fd10-4efbae7f77db.png)
>
> [Pythonでも簡単にGUIは作れる - Qiita](https://qiita.com/konitech913/items/61dc715ddaad54505a29#python%E3%81%A0%E3%81%A3%E3%81%A6gui%E3%82%92%E4%BD%9C%E3%82%8A%E3%81%9F%E3%81%84) より

既にPySimpleGUIの基本的な使い方についての解説記事は多数あるので、あまり見かけなかった使い方だけ書いていきます。

基本的な使い方の参考になりそうな記事

- [Pythonでも簡単にGUIは作れる - Qiita](https://qiita.com/konitech913/items/61dc715ddaad54505a29)
- [Tkinterを使うのであればPySimpleGUIを使ってみたらという話 - Qiita](https://qiita.com/dario_okazaki/items/656de21cab5c81cabe59)
- [マイブームPySimpleGUIを紹介｜eetann｜note](https://note.com/hideharu092/n/n9dc1c1075a7b)

### 要素の動的な更新(`update`)

イベントをキャッチして`update`を呼び出します。

> ```py
> import PySimpleGUI as sg
> 
> sg.theme('BluePurple')
> 
> layout = [[sg.Text('Your typed chars appear here:'), sg.Text(size=(15,1), key='-OUTPUT-')],
>           [sg.Input(key='-IN-')],
>           [sg.Button('Show'), sg.Button('Exit')]]
> 
> window = sg.Window('Pattern 2B', layout)
> 
> while True:  # Event Loop
>     event, values = window.read()
>     print(event, values)
>     if event == sg.WIN_CLOSED or event == 'Exit':
>         break
>     if event == 'Show':
>         # Update the "output" text element to be the value of "input" element
>         window['-OUTPUT-'].update(values['-IN-'])
> 
> window.close()
> ```
>
> ![demo-update](https://user-images.githubusercontent.com/46163555/68633697-df9c0f00-04c0-11ea-9fb3-121a72a87a59.png)
>
> [Cookbook - PySimpleGUI](https://pysimplegui.readthedocs.io/en/latest/cookbook/#recipe-pattern-2b-persistent-window-multiple-reads-using-an-event-loop-updates-data-in-window)より

`update`はキーワードを何も指定しない(上の例)とテキストを更新します。
特定の属性を指定すればその属性を更新することが出来ます。

コレを利用してイベントが発火したときに要素の有効/無効を切り替える、ユーザーの入力を元に要素を書き換える、といったことが可能です。

```py
def disable(self, key):
    """要素を無効にする"""
    window[key].update(disabled=True)

def enable(self, key):
    """要素を有効にする"""
    window[key].update(disabled=False)
```

### `disabled`

`True`にすることで要素を使用不可にできます。

```py
sg.FolderBrowse("フォルダ選択", disabled=True)
```

![disabled_toggle](https://user-images.githubusercontent.com/85564407/165041080-b6edf979-41f2-4533-a357-9314d9559d5a.gif)

普通に要素を隠したい場合は`visible=False`で良いですが、操作して欲しくないけど隠したくもない箇所に対してはこちらを使います。

### `enable_events`

`True`にすることで通常イベントが発火しない要素でイベントを扱う事ができます。

```py
sg.InputText("イベントの有効化", enable_events=True)
```

#### 例 `FolderBrowse`と`InputText`

`enable_events`を使う場面として、`InputText`によりフォルダパスの入力を受け取るというケースが挙げられます。

[FolderBrowse](<https://pysimplegui.readthedocs.io/en/latest/call%20reference/#:~:text=returns%20a%20button-,FolderBrowse,-(button_text%20%3D%20%22Browse%22%2C%0A%20%20%20%20target>)というボタンを使うと、ユーザーが入力したフォルダパスを`InputText`に受け取る事ができます。

`FolderBrowse`自体は非常に便利なのですが、そのままでは「フォルダパスが入力された」というイベントを受け取る事ができません。

そこで、`FolderBrowse`と紐付いている`InputText`の`enable_events`を`True`にします。

下の例では`FolderBrowse`からの入力を`InputText`が受け取ったときにイベント(スライド選択用コンボボックスの更新)が実行されています。
![input_event_eneble](https://user-images.githubusercontent.com/85564407/165041101-734feb6e-bcc8-4d8c-8080-7473de8c378b.gif)

なお、`InputText`の場合はユーザーが1文字でも入力したらイベントが発火するようになるので、入力が有効かチェックする、`disabled=True`にして`FolderBrowse`からの入力以外を受け付けないようにする、などの対策が必要です。

#### その他の例

- `Combo`
  - コンボボックスの選択が更新されたときに発火
- `Radio`
  - ラジオボタンが選択されたときに発火

### スタイルを辞書に切り出す

スタイルなどは、コンポーネントをインスタンス化する際に引数として渡すことで設定します。

小規模なGUIなら良いのですが、ある程度以上の規模になってくるとコンポーネントごとの設定が見にくく、修正も面倒になってきます。

それを解決するために辞書を使います。

Pythonでは`**kwargs`のように`**`をつけて引数を定義すると、その関数は任意の数のキーワード引数を受け取ることが出来るようになります。
関数呼び出し時に辞書オブジェクトに`**`をつけて引数にすることで、`key:value`のペアを`キーワード:引数`のペアとして関数に渡せるのです。

> ```py
> def func_kwargs_positional(arg1, arg2, **kwargs):
>     print('arg1: ', arg1)
>     print('arg2: ', arg2)
>     print('kwargs: ', kwargs)
> 
> d = {'key1': 1, 'key2': 2, 'arg1': 100, 'arg2': 200}
> 
> func_kwargs_positional(**d)
> # arg1:  100
> # arg2:  200
> # kwargs:  {'key1': 1, 'key2': 2}
> ```
> [Pythonの可変長引数（*args, **kwargs）の使い方 | note.nkmk.me](https://note.nkmk.me/python-args-kwargs-usage/)

コレを利用して、`size`, `font`, `disabled`などの設定を辞書に移す事ができます。

```py
# イメージ

WINDOW_STYLES = {
    "title": TITLE,
    "size": WINDOW_SIZE,
    "font": FONT,
    "resizable": True,
}

window = sg.Window(layout=[layout], **WINDOW_STYLES)
```

このようにすることで、似たようなスタイルの場合使い回せる、スタイルの変更が容易になるなどのメリットがあります。

## 実装内容

### PowerPointの情報を管理する

スライドが持つコンテンツの管理については、次のようなイメージで実装しました。

![image_2グループ](https://user-images.githubusercontent.com/85564407/165007671-73ed03f0-e2bf-4bf4-9327-0478dc17cff6.png)

`Slide`クラスがコンテンツを持ち、コンテンツがグループ分けされていて、各コンテンツがサイズ・座標・ラベルなどを持つ、というイメージです。

画像やテキストボックスについては`TypedDict`という通常の辞書よりも厳密に型を定義出来る型ヒントを使いました。

```py:content.py
from typing import TypedDict


class SlideContent(TypedDict):
    """スライドコンテンツ
    """
    coordinates: tuple[int, int]
    size: tuple[int, int]
    label: str


# total=False: 辞書初期化時などにキーが必須で無くなる
class Image(SlideContent):
    """画像
    """
    path: str


class TextBox(SlideContent):
    """テキストボックス
    """
    text: str
```

### PowerPoint読み込み

前述の`shape_type`判定と`shape`のサイズ・座標取得を行うクラスを作りました。

```py:presentation.py
class PresentationReader():
    """PowerPointの情報を読み取る。
    """
    def __init__(self, path: str) -> None:
        self.prs: Presentation = Presentation(path)

    def get_image_templates(self, slide_index=0) -> list[Image]:
        """スライドが持つ画像の情報を取得"""
        try:
            shapes = self.prs.slides[slide_index].shapes
        except IndexError:
            raise IndexError("slide index out of range")

        image_templates = []

        for shape in shapes:
            if shape.shape_type != MSO_SHAPE.RECTANGLE,:
                continue
            if not shape.text:
                continue
            image_templates.append(self.__set_content("image", shape))

        return image_templates

    # 省略...
```

### 出力用のスライド情報をセット

画像パスを元にラベル/データ名⇔画像パスの紐づけを行い、それを更にPowerPointからの入力(座標などの情報)と紐づけることで、データ名/`Image`/`TextBox`等の情報を持つ`Slide`を生成することで、出力用の情報をひとまとめにする形にしました。

ここの実装はもう少し綺麗に出来た気がします。

#### テキストの置換

```py:slide.py
    # 省略...
    def set_textboxes_to_slides(self):
        """スライドに対してテキストボックスをセットする。
        """
        for slide in self.slides:
            template_contents = deepcopy(self.template_slide.contents)
            current_label = 0
            matched_pairs: dict[str, str] = {}

            for template_group, group in zip(template_contents, slide.contents):
                # group数が奇数の場合途中で終了し得るため
                if not group:
                    return

                for textbox in template_group["textbox"]:
                    text = textbox["text"]

                    # group_idを指す文字列が存在すれば置換する
                    text = re.sub('(@|＠).*\d+', group["group_id"], text)
                    # labelを指す文字列が存在すれば置換する
                    if re.search('(#|＃).*\d+', text):
                        # 既にマッチしたlabelを指す文字列が存在する場合それを利用する
                        if text in matched_pairs.keys():
                            text = matched_pairs[text]
                        # matched_pairsに存在しなければペアに追加して置換
                        else:
                            try:
                                replacement_label = group["image"][current_label]["label"]
                            except IndexError:
                                break
                            matched_pairs[text] = replacement_label
                            text = re.sub('(#|＃).*\d+', replacement_label, text)
                            current_label += 1

                    textbox["text"] = text
                group["textbox"] = template_group["textbox"]
```

- `template_slide.contents`(設定用PowerPointの情報)をコピー
- `re`を使い、正規表現で置換対象の文字列を検索・置換
  - 「`@` や `#` に続けて数字を入力してください」と伝えた場合、`@1, ＠2, @_1, @ 1`など、半角/全角が入り混じったり、区切り文字を入れたり入れなかったりするパターンが考えられると思います。どのパターンにも対応出来るように正規表現を使いました。

### PowerPoint書き込み

書き込みは次のような流れで実装しました。

1. 設定用のPowerPointを複製
2. 複製したPowerPointにアクセス
3. ベースとなるスライドの置換対象図形・テキストボックスを削除
4. ベースとなるスライドを必要な枚数複製
5. 各スライドに画像・テキストボックスを出力
6. ベースとなるスライドを削除
7. 複製したPowerPointを保存

何故こんな面倒なことをしたかというと、「表を作ってその中に画像を入れる」ことが多い関係で、置換対象以外の図形は残しておきたいためです。
何故か表の中に画像を配置することが多いのです。見栄えが良いからでしょうか。

### GUI

GUIは次のようになりました。

![GUI-overview](https://user-images.githubusercontent.com/85564407/165257836-e0651fb7-fc15-401c-8996-34e1e3f443cd.png)

イベントの管理にはハンドラーを使いました。

といってもイベントをキーに、関数を値に持つ辞書を定義するだけです。

```py:handler.py
class Handler:
    def __init__(self, controller: Controller) -> None:
        self.controller = controller
        self.functions = {
            "-USER_UTIL_PWT-": self.controller.input_user_util_pwt,
            "-SELECT_FOLDER-": self.controller.select_folder,
            "-SELECT_FILES-": self.controller.select_files,
            "-SRC_FOLDER-": self.controller.input_img_folder,
            "-SRC_FILES-": self.controller.input_img_files,
            "-SUBMIT-": self.controller.click_submit,
        }

    def handle(self, key, values):
        if key not in self.functions:
            return
        event = self.functions[key]
        event(values)
```

```py:main.py
from src.Controllers.controller import Controller
from src.Controllers.handler import Handler
from src.Views.view import InterFace


def main():
    interface = InterFace()
    controller = Controller(interface.window)
    handler = Handler(controller)

    while True:
        event, values = interface.window.read()
        handler.handle(event, values)

        if event is None:
            interface.close_window()
            break


if __name__ == "__main__":
    main()
```

見ての通り、`main.py`がかなりスッキリします。~~上級者っぽくてかっこいい~~

## 工夫点

### 使用までのハードルを下げる

現在所属している部署は非IT系、かつ高齢の方が多く、言うまでもなく効率化への壁が多くあります。
このような環境では、ツール使用へのハードルを極力下げることが必要になってきます。

自身の観測範囲内ではありますが、以下のようなツールが好まれる傾向にあるようです。

① PowerpointやExcel(=**使い慣れている**)で設定ができる
② インストール等の**面倒な作業**が不要、自分のPCにコピーすれば使える

①についてはPowerPointでフォーマットを指定できるようにして対処しました。
また、**慣れている**という点で、データ名とラベルの区切りには慣習的に使われている`_`を採用しました。

②についてはPyinstallerによるexe化がメジャー(?)なようですが、生成されるファイルのサイズが大きすぎるし、動作も安定しないので個人的にあまり好みではありません。
それに、改修の度にexe化するのも面倒です。

- ユーザー視点でexe化と大差ない
- 改修が楽

上2つを満たす配布方法として、今回は**embeddable pythonによる配布**という選択肢を取りました。(Windows限定)

[こちらの記事](https://qiita.com/mm_sys/items/1fd3a50a930dac3db299)が詳しいですが、簡単に言うと最小限のPython実行環境をフォルダごと配布するようなイメージです。

ツールの実体である`main.py`を起動する`bat`ファイルも同じフォルダに入れておいて、`bat`ファイルのショートカットを好きな場所に置いて使ってもらうようにしました。

embeddable python はデフォルトだとtkinter(及びそのラッパーであるPySimpleGUI)が使えないので[Stack Overflow](https://stackoverflow.com/questions/37710205/python-embeddable-zip-install-tkinter)を参考にtkinterを使えるようにしました。

### エラーをちゃんと通知する

前述の他部署が作った画像貼り付けツールは、「入力したフォルダに画像が無い」「結果出力先に設定されているサーバが停止している」などの理由で正常に動作しなかった場合に何も通知してくれませんでした。

問題があったときに何も通知されない~~苛立ち~~不便さは身に沁みていたので、不正な入力があった時は考えうる操作ミスを通知するようにしました。

### 型ヒントの使用・docstringの記述

今までのPython開発では、「どうせ自分しか見ないソースコードだから」と型定義やdocstringは特に書いていませんでした。

しかし、実際の開発現場で個人で作業するということはまずないと思います。
また、よく言われることですが過去の自分も他人のようなもので、「先週書いていたコードの意味がわからない」という場面には結構な割合で遭遇します。

そのため、意識付けも兼ねて型ヒントの使用やdocstringを書くようにしました。

実際に書いてみて、関数呼び出し側を書きやすい、エディタが勝手に型チェックして警告を出してくれるので間違いに気づきやすい、などのメリットを享受出来ました。やってよかったです。

## 改善点

### テストを書いていない

- Pythonのテストフレームワークは扱ったことがない。Web開発学習中のため、新しいテストフレームワークの使い方を覚えたくない。
- 早く完成させたい。

という理由でテストを書かないことにしました。

この選択は開発中に何度も後悔しました。
テストを書かないことのデメリットは挙げるとキリがありませんが、例えば以下のような不便さを感じました。

- エラーがどこで起きているのか理解するまで時間がかかる
- 動作を確認するために軽いスクリプトを書く/GUIを操作する必要があり面倒
- 要件がハッキリしないため(設計の問題でもある)、不要なメソッドを実装してしまうことがあった

今から書くのはちょっと面倒なので書きませんが、今後は何があろうがテストを書こうと決心しました。

### 追加要望があった機能

- 画像のトリミング
  - 貼り付け前に座標で一括トリミング、オブジェクトを認識して「良い感じ」にトリミングしてくれる、など。
- GUI内に説明を表示
  - マニュアルを見に行くのが面倒なときやちょっと確認したいときなど、GUI内に説明が表示されていると嬉しいとの要望がありました。
  - 説明用のポップアップと、それを呼び出すためのボタンでも付けようかと思います。
- Excelから画像を貼り付ける機能が欲しい
  - 試験装置の中にはExcel形式で出力するものもあるので、Excelの画像を取り出す→PowerPointに貼り付けるという機能が欲しいそうです。
  - ~~Excelそのまま使えよ~~

## 参考記事

python-pptx

- [python-pptx — python-pptx 0.6.21 documentation](https://python-pptx.readthedocs.io/en/latest/index.html)
- [【Python×PowerPoint】python-pptxの導入~ファイル・スライド作成方法を徹底解説](https://www.shibutan-bloomers.com/python-libraly-pptx/988/)
- [Python-pptx: copy slide - Stack Overflow](https://stackoverflow.com/questions/50866634/python-pptx-copy-slide)
- [Is there a way to delete a shape with python-pptx - Stack Overflow](https://stackoverflow.com/questions/64700638/is-there-a-way-to-delete-a-shape-with-python-pptx)

PySimpleGUI

- [Call reference - PySimpleGUI](https://pysimplegui.readthedocs.io/en/latest/call%20reference/)
- [Cookbook - PySimpleGUI](https://pysimplegui.readthedocs.io/en/latest/cookbook/)
- [PySimpleGUIでGUIアプリを作ってみた ~その1~](https://it-for-pharma.com/pysimplegui%e3%81%a7gui%e3%82%a2%e3%83%97%e3%83%aa%e3%82%92%e4%bd%9c%e3%81%a3%e3%81%a6%e3%81%bf%e3%81%9f-%e3%81%9d%e3%81%ae1)
  - ハンドラーでイベント管理する、スタイルを辞書に切り出すなどの考え方を参考にさせていただきました。

TypedDict

- [[Python3.8～]ビルトインのTypedDictについて詳しく調べてみた（PEP589） - Qiita](https://qiita.com/simonritchie/items/63218b0a5c4a3d3632a1)
- [[Python]PylanceのVS Code拡張機能をさっそく使ってみた。 - Qiita](https://qiita.com/simonritchie/items/33ca57cdb5cb2a12ae16)
  - VSCodeのデフォルトだと型チェックが効かないことがあるのでこの記事を参考に設定を変更しました。

embeddable python

- [超軽量、超高速な配布用Python「embeddable python」 - Qiita](https://qiita.com/mm_sys/items/1fd3a50a930dac3db299)
- [4. Windows で Python を使う — Python 3.10.4 ドキュメント](https://docs.python.org/ja/3/using/windows.html#the-embeddable-package)
- [Python embeddable zip: install Tkinter - Stack Overflow](https://stackoverflow.com/questions/37710205/python-embeddable-zip-install-tkinter)
  - tkinterの導入

その他
- [製造現場向けの自動化ツールをPythonで作る時に留意すること - Qiita](https://qiita.com/banquet_kuma/items/ab30e69b999c2f451de3)
  - ツールの作成・展開に当たっての留意点を参考にしました。製造現場ではありませんが、現場のレベル感は似たようなものなので。
- 動作サンプルに使用した画像
  - [【フリーアイコン】 フルーツ](https://sozai.cman.jp/icon/food/fruits/)
  - [【フリーアイコン】 矢印（上下左右）](https://sozai.cman.jp/icon/arrow/base1/)
