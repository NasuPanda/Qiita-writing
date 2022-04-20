# 6章 ユーザーのモデルを作成する

## RSpecで書き換える

### 6.5

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user do
    name { "Example User" }
    email { "example@email.com" }
  end
end
```

```ruby:spec/models/user_spec.rb
require 'rails_helper'

RSpec.describe User, type: :model do
  let (:user) { FactoryBot.build(:user) }

  it "is valid with a name and an email" do
    expect(user).to be_valid
  end
end
```

FactoryBotを利用して`user`を生成、テストします。

### 6.7

```ruby:spec/models/user_spec.rb
RSpec.describe User, type: :model do
  let (:user) { FactoryBot.build(:user) }
  # 省略...
  it "is invalid without a name" do
    user.name = ""
    expect(user).to_not be_valid
  end
end
```

`name`の存在性バリデーションに対するテストを追加します。

### 6.11

```ruby:spec/models/user_spec.rb
RSpec.describe User, type: :model do
  let (:user) { FactoryBot.build(:user) }
  # 省略...
  it "is invalid without an email" do
    user.email = ""
    expect(user).to_not be_valid
  end
end
```

`email`の存在性バリデーションに対するテストを追加します。

### 6.14

```ruby:spec/models/user_spec.rb
RSpec.describe User, type: :model do
  let (:user) { FactoryBot.build(:user) }
  # 省略...
  it "is invalid with too long name" do
    user.name = "a" * 51
    expect(user).to_not be_valid
  end

  it "is invalid with too long email" do
    user.email = "a" * 244
    expect(email).to_not be_valid
  end
end
```

`name`と`email`の長さのバリデーションに対するテストを追加します。

### 6.18

```ruby:spec/models/user_spec.rb
RSpec.describe User, type: :model do
  let (:user) { FactoryBot.build(:user) }

  # 有効なユーザーのテスト
  context "with valid attributes" do
    # 他のテストは省略...
    it "is valid with valid format emails" do
      valid_addresses = %w[user@example.com USER@foo.COM A_US-ER@foo.bar.org
        first.last@foo.jp alice+bob@baz.cn]
      valid_addresses.each do |valid_address|
        user.email = valid_address
        expect(user).to be_valid
      end
    end
  end

  # 無効なユーザーのテスト
  context "with invalid attributes" do
    # 他のテストは省略...

```

`email`のフォーマットが有効なときは`user`が有効であることをテストします。

バリデーションの数が増えてきたので、ユーザーが有効な場合/無効な場合を`context`で分けました。

### 6.19

```ruby:spec/models/user_spec.rb
  # 省略...
  it "is invalid with invalid format emails" do
    invalid_addresses = %w[user@example,com user_at_foo.org user.name@example.
      foo@bar_baz.com foo@bar+baz.com]
    invalid_addresses.each do |invalid_address|
      user.email = invalid_address
      expect(user).to_not be_valid
    end
  end
```

`email`が無効なフォーマットのときは`user`が無効であることをテストします。

### 6.26

```ruby:spec/models/user_spec.rb
  # 省略...
  it "is invalid with a duplicate email" do
    duplicate_user = user.dup
    duplicate_user.email = user.email.upcase
    user.save
    expect(duplicate_user).to_not be_valid
  end
```

`email`のユニークバリデーションをテストしています。

`FactoryBot.build`した状態では`user`はまだインスタンスとしてメモリに存在するだけで、DBには保存されていません。
`user.save`を実行し、`user`がDBに保存されると`email`の値が重複したユーザーがバリデーションで弾かれるようになります。

### 6.33

```ruby:spec/models/user_spec.rb
RSpec.describe User, type: :model do
  let (:user) { FactoryBot.build(:user) }

  it "saves an email as lower case" do
    mixed_case_email = "Foo@ExAmPle.coM"
    user.email = mixed_case_email
    user.save
    expect(mixed_case_email.downcase).to eq user.reload.email
  end

  # 有効なユーザーのテスト
  context "with valid attributes" do
    # 省略...
  # 無効なユーザーのテスト
  context "with invalid attributes" do
    # 省略...
```

`before_save`で`email`が小文字に変換されていることをテストします。
有効な属性/無効な属性の`context`には含まれないので、`context`の外に置きました。

### 6.39

テストに対する直接的な変更はありませんが、`has_secure_password`の導入により仮想的な属性(DB上には存在しない)である`password`と`password_confirmation`へのバリデーションが追加されるので、ファクトリーに変更を加えます。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user do
    name { "Example User" }
    email { "example@email.com" }
    password { "securePassword" }
    password_digest { "securePassword" }
  end
end
```

また、テストの一部をパスワードに対応する形に変更します。

```ruby:spec/models/user_spec.rb
  # 有効なユーザーのテスト
  context "with valid attributes" do

    it "is valid with name, email and password" do
      expect(user).to be_valid
    end

  # 省略...
```

exampleに全ての属性を列挙するスタイルはEverydayRailsに習っていますが、冗長だし属性が追加される度に変更が必要なのであまりよろしくない気もします。

### 6.41

```ruby:spec/models/user_spec.rb
  # 省略...
  it "is invalid without a password" do
    user.password = user.password_confirmation = "" * 6
    expect(user).not_to be_valid
  end

  it "is invalid with a too short password" do
    user.password = user.password_confirmation = "abcde"
    expect(user).not_to be_valid
  end
```

パスワードの存在性、最小長さ(6文字)のバリデーションに対するテストを追加します。

## 答え合わせ

[コード例〜第6章〜｜RailsチュートリアルのテストをRSpecで書き換える](https://zenn.dev/fu_ga/books/ff025eaf9eb387/viewer/60fc78#%E3%83%AA%E3%82%B9%E3%83%886.7)

相違点は以下２点くらいです。

- 例はファクトリを使っていない
- 例は`context`を使っていない

`context`はともかく、
ファクトリは慣れるために使っている(現時点では無くても特に問題ない)ので、まぁそうだよね。という感じです。

# 7章 ユーザー登録

## RSpecで書き換える

### 7.23

無効なユーザー登録に対するテストを実装します。
Railsチュートリアルではインテグレーションテスト(`users_signup_test.rb`)として実装していました。
ここでテストしたいのは「無効なデータを送信した時ユーザーが作成されないこと」なので、リクエストスペックで実装していきます。

```ruby:spec/requests/users_spec.rb
RSpec.describe "Users", type: :request do
  # 省略...
  describe "#create" do
    it "doesn't create a user with invalid information" do
      get signup_path
      expect{
        post users_path, params: { user: { name: "",
                                    email: "address@invalid",
                                    password: "short",
                                    password_confirmtion: "rack"}}
      }.to_not change(User, :count)
    end
  end
```

このテストでは無効な`params`をPOSTした時にユーザーが登録されないこと、つまり`User.count`が増減しないことを確認したいです。

`expect`にはブロックを渡すことも出来ます。

> ```ruby
> expect(something)       # => ExpectationTarget wrapping something
> expect { do_something } # => ExpectationTarget wrapping the block
> ```
> 参考 : [Class: RSpec::Expectations::ExpectationTarget — Documentation for rspec-expectations (3.11.0)](https://www.rubydoc.info/gems/rspec-expectations/RSpec/Expectations/ExpectationTarget)

今回は、`to_not`と`change`マッチャを使ってブロック内の処理を実行する前後で`User.count`の値が変わっていない事を確認しています。

### 演習 7.25

エラーメッセージが正しく表示されることをテストします。
Railsチュートリアルではインテグレーションテスト(7.23と同じく)で実装していました。
ここで検証したいのはUIなので、システムスペックを使っていきます。

```ruby:spec/system/users_spec.rb
require "rails_helper"

RSpec.describe "Users", type: :system do
  before do
    driven_by(:rack_test)
  end

  describe "#create" do
    scenario "user posts invalid information" do
      visit signup_path
      fill_in "Name", with: ""
      fill_in "Email", with: "address@invalid"
      fill_in "Password", with: "short"
      fill_in "Confirmation", with: "rack"
      click_button "Create my account"

      expect(page).to have_selector "div#error_explanation"
      expect(page).to have_selector "div.alert-danger"
    end
  end

end
```

システムスペックでは`example`の起点として`scenario`を使う事ができます。(`it`でも可)
このテストでは「ユーザーが無効なデータを送信した」ことによってエラーメッセージが表示されるので、`scenario`の方がわかりやすく感じました。

### 7.31

有効なユーザー登録のテストを実装します。

```ruby:spec/requests/users_spec.rb
  # 省略...
  describe "#create" do
    let(:valid_user_params) { FactoryBot.attributes_for(:user) }

    context "with valid information" do
      it "creates a user" do
        get signup_path
        expect{
          post users_path, params: { user: valid_user_params }
        }.to change(User, :count).by 1
      end

      it "redirects to users/id" do
        post users_path, params: { user: valid_user_params }
        created_user = User.last
        expect(response).to redirect_to created_user
      end
    end

    context "with invalid information" do
      it "doesn't create a user" do
        expect{
          post users_path, params: { user: { name: "",
                                      email: "address@invalid",
                                      password: "short",
                                      password_confirmation: "rack"}}
        }.to_not change(User, :count)
      end
    end
```

#### ユーザーの作成

- すでに無効なデータが送信される場合のテストがあったので、有効/無効を`context`で分けました。
- `FactoryBot.attributes_for`を使って`params`に有効なデータを渡します。
  - 無効なデータの場合のように全ての属性を列挙するよりもスッキリ書けます。

#### ユーザーの詳細ページにリダイレクトされること

`show`アクション、すなわち`users/id`にリダイレクトされることを検証します。

`users/id`はRailsの[resources](https://railsguides.jp/routing.html)を使っている場合、`user_path(user)`という名前付きルートで表せます。
さらに、以下のように`redirect_to`に引数として渡すときは`user_url(user)`を`user`で置き換える事ができます。

```ruby
# どちらも同じ結果になる
redirect_to user_url(user)
redirect_to user
```

つまり、`User.last`で直近に作成されたユーザーを取得、`redirect_to`に渡すことで詳細ページへリダイレクトされることを検証出来ます。

### 7.32

flash(成功時のメッセージ)が表示されていることを確認するテストです。

```ruby:spec/system/users_spec.rb
  scenario "user posts valid information" do
    valid_user_params = FactoryBot.attributes_for(:user)

    visit signup_path
    fill_in "Name", with: valid_user_params[:name]
    fill_in "Email", with: valid_user_params[:email]
    fill_in "Password", with: valid_user_params[:password]
    fill_in "Confirmation", with: valid_user_params[:password_confirmation]
    click_button "Create my account"

    expect(page).to have_selector "div.alert-success"
  end
```

システムスペックを使いました。

## 答え合わせ

[コード例〜第7章〜｜RailsチュートリアルのテストをRSpecで書き換える](https://zenn.dev/fu_ga/books/ff025eaf9eb387/viewer/26b9c7#%E3%83%AA%E3%82%B9%E3%83%887.31)

相違点は以下でした。

- 有効なデータをFactoryBotで用意(自分)
  - FactoryBotの方がスッキリ書けるので僕は好きです。
  - FactoryBotを使わない場合、テストファイルからデータの中身を確認出来るという利点もあります。
- システムスペックで`it`ではなく`scenario`を使っている(自分)
  - コレは好みかと。
- `flash`のテストがシステムスペック(自分)
  - 参考にした記事ではリクエストスペックで書いていました。
  - 正直UIとは言っても`flash`のためだけにシステムスペック書くのはどうだろう・・・と思いましたが、UIのテストはシステムスペックで統一したかったので。

# 8章 基本的なログイン機構

## RSpecで書き換える

### 8.3

```ruby:requests/sessions_spec.rb
require 'rails_helper'

RSpec.describe "Sessions", type: :request do
  describe "#new" do
    it "responds successfully" do
      get login_path
      expect(response).to have_http_status :ok
    end
  end
end

```

### 8.9

ログインに失敗した時にフラッシュメッセージが表示されること、
`root`に戻った後フラッシュメッセージが消えていることをテストします。

```ruby:spec/system/sessions_spec.rb
require 'rails_helper'

RSpec.describe "Sessions", type: :system do
  before do
    driven_by(:rack_test)
  end

  describe "#create" do
    scenario "user login with invalid information" do
      visit login_path
      fill_in "Email", with: ""
      fill_in "Password", with: ""
      click_button "Log in"

      # flashが表示されているかテスト
      expect(page).to have_selector "div.alert.alert-danger"
      # flashが残っていないかテスト
      visit root_path
      expect(page).to_not have_selector 'div.alert.alert-danger'
    end
  end
end
```

### 8.23

Railsチュートリアルではユーザーログインのテストで使うfixtureを実装していました。
テストデータはFactoryBotで実装してあるので割愛します。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user do
    name { "Example User" }
    email { "example@email.com" }
    password { "securePassword" }
    password_confirmation { "securePassword" }
  end
end
```

### 8.24

有効なデータを使ってユーザーがログインした時のUIをテストします。
具体的には、

- ログアウト/ユーザープロフィールへのリンクが含まれること
- ログインリンクが含まれないこと

をテストします。

```ruby:spec/system/sessions_spec.rb
  # 省略...
  describe "#create" do

    context "with valid information" do
      let(:user) { FactoryBot.create(:user) }

      it "hasn't a link to login and has a link to logout, user/id" do
        user = FactoryBot.create(:user)
        visit login_path
        fill_in "Email", with: user.email
        fill_in "Password", with: user.password
        click_button "Log in"

        expect(page).to_not have_link "Log in", href: login_path
        expect(page).to have_link "Log out", href: logout_path
        expect(page).to have_link "Profile", href: user_path(user)
      end
    end

    context "with invalid information" do
      it "has a error message" do
        visit login_path
        fill_in "Email", with: ""
        fill_in "Password", with: ""
        click_button "Log in"

        # flashが表示されているかテスト
        expect(page).to have_selector "div.alert.alert-danger"
        # flashが残っていないかテスト
        visit root_path
        expect(page).to_not have_selector 'div.alert.alert-danger'
      end
    end

  end
end
```

元々システムスペックは`scenario`を使って「どんな操作をするか」を書く形で実装していましたが、
`context`+`it`で「どんな結果を期待するか」を書く形に変更しました。

`system/users_spec.rb`も合わせて変更しました。

```shell
# 出力のみ

Users
  #create
    with valid information
      has a success message
    with invalid information
      has a error message
```

`have_link`マッチャを使ってリンクの有無を検証しています。
参考 : [使えるRSpec入門・その4「どんなブラウザ操作も自由自在！逆引きCapybara大辞典」 - Qiita](https://qiita.com/jnchito/items/607f956263c38a5fec24#%E7%89%B9%E5%AE%9A%E3%81%AE%E3%83%91%E3%82%B9%E3%81%B8%E3%81%AE%E3%83%AA%E3%83%B3%E3%82%AF%E3%82%92%E6%A4%9C%E8%A8%BC%E3%81%99%E3%82%8B%E3%82%AF%E3%83%AA%E3%83%83%E3%82%AF%E3%81%99%E3%82%8B)

### 8.27 演習

`email`が正しく、`password`が間違っている場合のテストを追加します。

```ruby:spec/system/sessions_spec.rb
  # 省略...
  it "has a error massage with valid email and invalid password" do
      visit login_path
      fill_in "Email", with: user.email
      fill_in "Password", with: "invalid"
      click_button "Log in"

      # flashが表示されているかテスト
      expect(page).to have_selector "div.alert.alert-danger"
      # flashが残っていないかテスト
      visit root_path
      expect(page).to_not have_selector 'div.alert.alert-danger'
  end
```

### 8.30

ユーザー登録後にログインされるようにしたので、そのテストをしたいです。
そのために、まずはログインヘルパーを実装します。

`spec/rails_helper.rb` 内の以下の行のコメントアウトを解除します。

```ruby:spec/rails_helper.rb
Dir[Rails.root.join('spec', 'support', '**', '*.rb')].sort.each { |f| require f }
```

こうすることで、RSpec関連の設定ファイルを `spec/support` ディレクトリ配下に配置することが出来るようになります。

ヘルパーメソッドを定義します。

```ruby:spec/support/login.rb
module LoginSupport

  def is_logged_in?
    !session[:user_id].nil?
  end
end

RSpec.configure do |config|
  config.include LoginSupport
end
```

ここでは`Rspec.configure`を使って`LoginSupport`を`include`しています。
テスト毎に明示的に`include`する方法もあります。

### 8.31

ユーザー登録した直後にユーザーがログイン状態になっているかテストします。
先程定義したヘルパーメソッドを使って実装します。

```ruby:spec/requests/users_spec.rb
RSpec.describe "Users", type: :request do
  describe "#create" do
    let(:valid_user_params) { FactoryBot.attributes_for(:user) }

    context "with valid information" do
      it "is logged in" do
        post users_path, params: { user: valid_user_params }
        expect(is_logged_in?).to be_truthy
      end
    end
```

### 8.35

ログアウトのテストを実装します。
Railsチュートリアルではインテグレーションテストで「ログイン→ログイン状態確認→ログアウト→ログアウト状態確認」
としていましたが、ログイン/ログアウトは別で書いてきます。

```ruby:spec/requests/sessions_spec.rb
RSpec.describe "Sessions", type: :request do
  describe "#destroy" do
    it "can log out" do
      user = FactoryBot.create(:user)

      # ログイン
      get login_path
      post login_path params: { session: { email: user.email,
                                          password: user.password } }
      expect(is_logged_in?).to be_truthy

      # ログアウト
      delete logout_path
      expect(is_logged_in?).to_not be_truthy
    end
  end
```

## 答え合わせ

システムスペックによるUIテストの内、リンクの検証方法が違いました。
大差ないですが、自分のテストはリンクのテキストが変わると壊れてしまうので例のテストの方が良いかもしれません。

```ruby:spec/system/sessions_spec.rb
# 例
expect(page).to_not have_selector "a[href=\"#{login_path}\"]"
expect(page).to have_selector "a[href=\"#{logout_path}\"]"
expect(page).to have_selector "a[href=\"#{user_path(user)}\"]"

# 自分の実装
expect(page).to_not have_link "Log in", href: login_path
expect(page).to have_link "Log out", href: logout_path
expect(page).to have_link "Profile", href: user_path(user)
```

# 9章 発展的なログイン機構

## RSpecで書き換える

### 9.14

連続でログアウト(ユーザーが別のタブでログアウト→他のタブで再度ログアウトしようとする、など)出来ることをテストします。

```ruby:spec/requests/sessions_spec.rb
  it "can log out in a row" do
    # ログイン
    get login_path
    post login_path params: { session: { email: user.email,
                                        password: user.password } }
    expect(is_logged_in?).to be_truthy

    # 連続ログアウト出来る
    delete logout_path
    delete logout_path
    expect(response).to redirect_to root_path
  end
```

### 9.17

`authenticated?`メソッドがエラーを返さないことをテストします。

```ruby:spec/models/user_spec.rb
  describe "#authenticated?" do
    it "returns false if digest is nil" do
      expect(user.authenticated?("")).to_not be_truthy
    end
  end
```

### 9.25

remember_meチェックボックスを実装したので、機能をテストします。

```ruby:spec/system/sessions_spec.rb
  describe "remember me" do
    let(:user) { FactoryBot.create(:user) }

    context "login with remember" do
      it "stores the remember token in cookies" do
        post login_path, params: { session: { email: user.email,
                                              password: user.password,
                                              remember_me: "1" }}
        expect(cookies[:remember_token]).to_not be_blank
      end
    end

    context "login without the remember" do
      it "doesn't store the remember token in cookies" do
        post login_path, params: { session: { email: user.email,
                                              password: user.password,
                                              remember_me: "0" } }
        expect(cookies[:remember_token]).to be_blank
      end
    end
  end
```

### 9.31

`sessions_helper.rb`のテストを実装します。

まずはスペックから`SessionsHelper`を使えるようにします。

```ruby:spec/rails_helper.rb
RSpec.configure do |config|
  # 省略...
  include ApplicationHelper
  include SessionsHelper
end
```

次に`SessionsHelper`のメソッド`current_user`に対するテストを書いていきます。

```ruby:app/helpers/sessions_helper.rb
module SessionsHelper
  # 現在のユーザーを返す
  def current_user
    if (user_id = session[:user_id])
      @current_user ||= User.find_by(id: user_id)
    elsif (user_id = cookies.signed[:user_id])
      user = User.find_by(id: user_id)
      if user && user.authenticated?(cookies[:remember_token])
        log_in user
        @current_user = user
      end
    end
  end
```

`current_user`は見ての通り複雑な条件分岐があります。
現状テスト出来ていないのは 「`session`が空の時に正しいユーザーが返ってくるか」「`remember_digest`が間違っている時に現在のユーザーが`nil`になるかどうか」の2通りです。

実装したテストは以下のようになります。

```ruby:spec/helpers/sessions_helper_spec.rb
require 'rails_helper'

RSpec.describe ApplicationHelper, type: :helper do
  describe "#current_user" do
    let(:user) { FactoryBot.create(:user) }
    before do
      remember(user)
    end

    context "sessions is nil" do
      it "returns right user" do
        expect(user).to eq current_user
        expect(is_logged_in?).to be_truthy
      end
    end

    context "remember digest is wrong" do
      it "returns nil" do
        user.update_attribute(:remember_digest, User.digest(User.new_token))
        expect(current_user).to be_nil
      end
    end
  end

end
```

## 答え合わせ

[コード例〜第9章〜｜RailsチュートリアルのテストをRSpecで書き換える](https://zenn.dev/fu_ga/books/ff025eaf9eb387/viewer/09bc4f)

細かい書き方(`describe`や`context`によるテストのグループ化など)以外に大きな違いはありませんでした。

# まとめ

