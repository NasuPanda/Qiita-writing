<!--
title: Everyday Rails まとめ
-->

## 目的

Everyday Rails に取り組んだ目的は以下です。

- テストの手法を学ぶ
- RSpecの扱いを学ぶ
- 「基礎的かつ体系的な教材」による「実践を通した理解」の練習
    - 「例によるその場限りの理解」からの脱却

## 環境

- Rails7.0
- Ruby3.1
- RSpec Rails 5.0 と RSpec3.10

https://github.com/JunichiIto/everydayrails-rspec-jp-2022

# ２.RSpecのセットアップ


## インストール

`rspec-rails` をインストール。

```ruby
group :development, :test do
	gem 'rspec-rails'
end
```
- Rails で RSpecを利用するために必要なパッケージがひとまとめになったライブラリ。
- `rspec-rails` には `rspec-core` とその他独立したgemが含まれる。

## RSpecの命名規則

`app/helpers/projects_helper.rb` をテストする
→ `spec/helpers/projects_helper_spec.rb` を使う

`lib/my_library.rb` をテストする
→ `spec/lib/my_library_spec.rb` を使う

## テストデータベースの作成

テスト実行時に接続するテスト用のデータベースの設定。
`config/database.yml` で設定する。

```ruby
# spliteの場合
test:
<<: *default
database: db/test.sqlite3

# MySQLやPostgreSQLを使っている場合
test:
<<: *default
database: projects_test
```

## RSpecの設定

まず次のようなコマンドを使ってRSpecをインストールする。

```bash
bin/rails generate rspec:install

# 結果
create  .rspec
create  spec
create  spec/spec_helper.rb
create  spec/rails_helper.rb
```

以下のファイルが生成される。

- `.rspec`

RSpec用設定ファイル

- `spec`

スペックファイルを格納するディレクトリ

- `spec_helper.rb`
- `rails_helper.rb`

ヘルパーファイル

✅ RSpecに慣れてきた頃に生成されたファイルのコメントの内容（設定のカスタマイズが書かれている）を精読してみると良い。

### 出力を読みやすく

`.rspec` を以下のように変更する。

```ruby
--require spec_helper
--format documentation
```

この他にも `--warnings` フラグを追加して警告を全て表示する、など出来る。

### `binstub`  を使って短いコマンドで実行出来るようにする

`bundle exec` と binstubについて
[bundle execとbinstubを理解する - Qiita](https://qiita.com/NasuPanda/items/975328eddf4ea22465f8)

RSpecを実行する際は `bundle exec rspec` のように毎回 `bundle exec` を付ける必要がある。

これは、実行ファイルがプロジェクトのコンテキストで実行されるようにするため。
すなわちプロジェクトのgemにインストールされた実行ファイルが実行されるようにするもの。

`binstub` を作成すると少し短く出来る。

```ruby
bundle binstubs rspec-core
```

上のコマンドを実行すると`bin` ディレクトリ内に `rspec` という名前の実行用ファイルが作成される。
この他にも独自のエイリアスを設定してコマンドを短くすることも出来る。

## ジェネレータの設定

`rails g` の時にRSpec用のスペックファイルも一緒に作ってもらうように設定する。

```ruby
require_relative"boot" require"rails/all"
# Rails が最初から書いているコメントは省略 ... Bundler.require(*Rails.groups)
moduleProjects
class Application < Rails::Application
    config.load_defaults 7.0

		config.generators do |g|
			g.test_framework :rspec,
				fixtures: false,
				view_specs: false,
				helper_specs: false,
				routing_specs: false
			end
	end
end
```

`fixture`
fixtureの作成をスキップする

`view_specs`
ビュースペックを作成しない

`helper_specs`
ヘルパーファイル用のスペックを作成しない

`routing_specs`
`routes.rb` 用のスペック。
アプリケーションが大規模になってきたら導入すると良い。

### ジェネレータ設定の注意点

自動生成しないというだけであって

- 手動で追加
- 自動生成されたファイルを削除すること

が禁止されているわけではない。

***

ここからは各章ごとのざっくりまとめのみ

***

# 3.モデルスペック

## テストの意義

> テストを書いている**最中に**モデルが持つべきバリデーションについて考えれば、バリデーションの追加を忘れにくくなる。

➡️ **テストすべき仕様について考慮することで、抜け漏れ無い実装ができる。**TDD的なアプローチ。

## 期待する結果は能動系で明示的に記述する

```ruby
describe User do

  it "is valid with a first name, last name, email, and password"

  it "is invalid without a first name"

  it "is invalid without a last name"

  it "is invalid without a email address"

  it "returns a user's full name as a string"

end
```

上のコードはモデルスペックのアウトライン。
単純な例だが、多くのベストプラクティスを含む。

- 期待する結果を`describe`でまとめて記述する。
  - モデルの`describe`であれば、そのモデルがどんなモデルなのか、どんな振る舞いをするのか説明することになる。
- チェックする結果は example 1つに付き1個だけ。
  - 問題となる箇所を特定しやすい。
- 明示的な example を書く
  - `it`の後に続く文字列は必須ではないが、あると読みやすくなる。
- example は能動系の動詞から始める
  - 可読性は非常に重要。
  - 「it(テスト対象) is ~」というように、テストに望む結果を文章のように表す事ができる。

## 起きてほしい事と、起きてほしくない事をテストする

正常系・異常系どちらもテストする。
`example` を書くときは両方のパスを考え、その考えに沿ってテストする。

## 境界値テストをする

バリデーションが4文字以上10文字以下なら、
3文字と11文字をテストする。

「なぜそのバリデーションなのか？」を自問し、アプリケーションの要件・コードを熟考する良い機会。

## 可読性を上げるためにスペックを整理する

`describe` `context`により `example` を分類、アウトラインを作る。
`before` `after` により重複を取り除く。

ただし、テストの場合**DRYであることよりも可読性を重視する**と良い。



# 4.意味のあるテストデータ

## ファクトリを安全に使うには

### ファクトリの注意点

- ファクトリはサンプルデータの作成を手助けしてくれる。
- セットアップも簡潔になるので、テストの読みやすさを妨げない。

しかし、以下のようなリスクも存在する。

- テスト中に予期しないデータが作成される
- ムダにテストが遅くなる

### 上記のような問題が発生したときの対処

- ファクトリーが必要なことだけを行っていることを確認する
- コールバックは必ずトレイトの中で宣言する
    - ファクトリを使う度に呼び出されないように
- 可能な限り `create` よりも `build` を使う。
- そもそも**ここでファクトリを使う必要はあるのか？**を自問する
    - モデルの `new` や `create` でセットアップ出来るならそれでいい。
    - PORO(Plain Old Ruby Objects)と混在させてもOK。大事なのは可読性。

## PORO・ファクトリ・フィクスチャの比較

一概にどれが良いとは言えない。ケースバイケース。

### PORO（Plain Old Ruby Objects）

- 自己文書的。
- テストをパスさせるために何が必要なのかひと目で分かる。

### ファクトリ

- データの詳細が別のファイルに移動するため、簡潔に書ける。
- 複雑なデータが必要な時でも容易にセットアップ出来る。

### フィクスチャ

- テストとは別のフィクスチャファイル（yml形式）に保存された値を参照する必要がある。
    - テストデータはテストの一部として目に見えたほうがいい。
- 壊れやすいため、アプリケーション・テストのコードに加えてフィクスチャ用のコードの保守が必要になる
- データを読み込む際に `Active Record` を使わない。
    - つまり、モデルのバリデーションのような機能が無視される。
- ファクトリを導入するまでもないが、テスト用データを別ファイルに分けたい時に使う？

## シーケンスの利用

ユニークなデータを生成したい時は**シーケンス**を使う。
シーケンスはオブジェクトが作成される度にインクリメントされるカウンタ。

```ruby
FactoryBot.define do
  factory :user do
    first_name { "Aaron" }
    last_name { "SUmner" }
    sequence(:email) { |n| "tester#{n}@example.com" }
    password { "dottle-nouveau-pacilion-tights" }
  end
end
```

## RSpecの威力

テスト対象のオブジェクトに真偽値を返す〇〇メソッドが存在する場合、
`be_〇〇` というマッチャが利用出来る！

## 関連付けされたオブジェクト

`association`により関連付けを扱う事ができる。

複雑な関連付けがオブジェクト間にある場合、その事をFactory Botに伝える必要がある。

## 重複をなくすために継承、トレイトが使える。

### 継承

次のように入れ子構造にして定義する。
呼び出し時に `project` クラスを指定する必要が無い。

```ruby
factory :project do
	...  
	**factory :project_due_yesterday do**
    due_on { 1.day.ago }
```

### トレイト

`trait` を使って定義する。
トレイトの利点は複数のトレイトを組み合わせて複雑なオブジェクトを構築出来る点。

```ruby

  factory :project do
		...
	  # 昨日が締め切り
	  **trait :due_yesterday do**
	    due_on { 1.day.ago }
```

## コールバック

`create` などの**メソッド実行前後に追加のアクションを実行**出来る。

コールバックを適切に使えば**簡単にセットアップ**出来る。
一方、テストが遅い・ムダに複雑になることもあるので注意。

例
`create_list` メソッドなど。

定義・使い方

```ruby
# 定義（トレイトの中で）
**after(:create)** { |project| **create_list**(:note, 5, project: project) }

# 呼び出し（with_notesという名前）
project = FactoryBot.create(:project, **:with_notes)**
```