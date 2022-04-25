#### 図形の追加

```python
Shapes.add_shape(autoshape_type_id, left, top, width, height)
```

* `autoshape_type` : 図形の種類
* `left` : 図形の左上のx座標
* `top` : 図形の左上のy座標
* `width` : 図形の幅
* `height` : 図形の高さ

#### テキストボックスの追加

```python
Shapes.add_textbox(left, top, width, height)
```

[テキスト操作について](https://www.shibutan-bloomers.com/python-libraly-pptx-2/1024/)

##### TextFrame

テキストを書き込める箇所(テキストボックス、図形など)全てに存在するプロパティ。

##### paragraph

段落。TextFrame>paragraphという構成になっており、段落ごとにフォント・書式などの設定ができる。

```python
txBox = sld0.shapes.add_textbox(left, top, width, height)    #Text Box Shapeオブジェクトの追加

tf = txBox.text_frame		# TextFrameオブジェクトの設定
tf.text = "This is text inside a textbox"            # TextFrameオブジェクトにはデフォルトで1つ段落を持つ

p = tf.add_paragraph()		                           # paragraphオブジェクトの追加作成(2段落目)
p.text = "This is a second paragraph that's bold"    # textプロパティによる文字列の設定
p.font.bold = True		                               # font.boldプロパティによる太文字設定
```

#### 画像の追加

```python
# image_fileは画像パス
picture = Shapes.add_picture(image_file, left, top, width, height)

# トリミングできる
picture.crop_bottom = 0.25 # crop_left/right/top
# 回転もできる
picture.rotation = 45 # +なら時計回り -なら反時計回り
```

### 単位指定

```
from pptx.util import Cm, Inches, Pt
```
* `Cm` : cm単位
* `Inches` : インチ単位
* `Pt` : ポイント単位

## pathlibの基本的な使い方

Pathオブジェクトにファイルパスを渡す。

```python
from pathlib import Path

IMAGE_DIRECTORY = "./resources/images"

# Pathオブジェクトを生成
p = Path(IMAGE_DIRECTORY)
```

様々な条件でパスの探索が可能。

```python
# dir_path直下のファイルとディレクトリを取得
# Path.glob(pattern)はジェネレータを返す。結果を明示するためlist化しているが、普段は不要。
paths = list(p.glob("*"))
# 拡張子 条件指定
paths = list(p.glob("*.jpg"))
# 再帰的な検索は[**]を利用する
paths = list(p.glob("**/*.jpg"))
```

ファイル名などを取得出来る便利なメソッドがある。

```python
paths[0].name   # > test.txt
paths[0].stem   # > test
paths[0].parts  # > a/b/c >> ['a', 'b' ,'c']
```