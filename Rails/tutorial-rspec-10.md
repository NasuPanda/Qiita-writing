# 10章 ユーザーの更新・表示・削除

## RSpecで書き換える

### 10.9

無効なユーザーを書く回数が多くなってきたのでFactoryBotで作成するようにします。

```ruby:spec/factories/users/rb
  # 省略...
  factory :invalid_user, class: User do
    name { "" }
    email { "address@invalid" }
    password { "short" }
    password_confirmation { "rack" }
  end
```

編集できないこと、編集に失敗した時に`edit`ビューが描画されていることをテストします。

```ruby:spec/requests/users_spec.rb
describe "#update" do
  let(:user) { FactoryBot.create(:user) }

  context "with valid information" do
    # 後で書く
  end

  context "with invalid information" do
    let(:invalid_user_params) { FactoryBot.attributes_for(:invalid_user) }

    it "doesn't edit a user" do
      patch user_path(user), params: { user: invalid_user_params }
      user.reload
      expect(user.name).to_not eq invalid_user_params[:name]
      expect(user.email).to_not eq invalid_user_params[:email]
      expect(user.password).to_not eq invalid_user_params[:password]
      expect(user.password_confirmation).to_not eq invalid_user_params[:password_confirmation]
    end

    it "redirects to edit page" do
      patch user_path(user), params: { user: invalid_user_params }
      expect(response.body).to include full_title('Edit user')
    end
  end
end
```

### 10.1.3 演習

`"The form contains 4 errors"`というエラーメッセージが表示されていることをテストします。

```ruby:spec/requests/users_spec.rb
it "has correct error messages of 'The form contains 4 errors'" do
  patch user_path(user), params: { user: invalid_user_params }
  expect(response.body).to include "The form contains 4 errors"
end
```

### 10.11

ユーザーの編集に成功するときのテストを書きます。
パスワード欄を空白にした場合の例外処理(`User`モデルのバリデーションに`allow_nil`を追加)を実装しているので、パスワードは空白にしておきます。

```ruby:spec/requests/users_spec.rb
describe "#update" do
  let(:user) { FactoryBot.create(:user) }

  context "with valid information" do
    before do
      @another_user_params = { name: "Another name",
        email: "another@gmail.com",
        password: "",
        password_confirmation: "" }
    end

    it "edits a user" do
      patch user_path(user), params: { user: @another_user_params }
      user.reload
      expect(user.name).to eq @another_user_params[:name]
      expect(user.email).to eq @another_user_params[:email]
    end

    it "redirects to users/id" do
      patch user_path(user), params: { user: @another_user_params }
      expect(response).to redirect_to user
    end

    it "has a flash" do
      patch user_path(user), params: { user: @another_user_params }
      expect(flash).to be_any
    end
  end
  # 省略...
```

### 10.17

`edit`や`update`にログインを要求するよう変更したので、対応出来るようにヘルパーメソッドを実装していきます。
(`log_in_system`と`log_in_request`については後で直します)

```ruby:spec/support/login.rb
module LoginSupport

  def log_in_system(user)
    visit login_path

    fill_in 'Email', with: user.email
    fill_in 'Password', with: user.password
    click_button 'Log in'
  end

  def log_in_request(user)
    post login_path, params: { session: { email: user.email,
      password: user.password } }
  end

  def is_logged_in?
    !session[:user_id].nil?
  end

  def log_in_as(user)
    session[:user_id] = user.id
  end
end

RSpec.configure do |config|
  config.include LoginSupport
end
```

`before`ブロックの中でログインします。
ついでに`patch`も毎回同じことをしているので`before`に入れてしまいます。

```ruby:spec/requests/users_spec.rb
  describe "#update" do
    let(:user) { FactoryBot.create(:user) }

    context "with valid information" do
      before do
        @another_user_params = { name: "Another name",
          email: "another@gmail.com",
          password: "",
          password_confirmation: "" }

        log_in_request(user)
        patch user_path(user), params: { user: @another_user_params }
      end

      it "edits a user" do
        user.reload
        expect(user.name).to eq @another_user_params[:name]
        expect(user.email).to eq @another_user_params[:email]
      end

      it "redirects to users/id" do
        expect(response).to redirect_to user
      end

      it "has a flash" do
        expect(flash).to be_any
      end
    end

    context "with invalid information" do
      before do
        @invalid_user_params = FactoryBot.attributes_for(:invalid_user)

        log_in_request(user)
        patch user_path(user), params: { user: @invalid_user_params }
      end

      it "doesn't edit a user" do
        user.reload
        expect(user.name).to_not eq @invalid_user_params[:name]
        expect(user.email).to_not eq @invalid_user_params[:email]
        expect(user.password).to_not eq @invalid_user_params[:password]
        expect(user.password_confirmation).to_not eq @invalid_user_params[:password_confirmation]
      end

      it "redirects to edit page" do
        expect(response.body).to include full_title("Edit user")
      end

      it "has correct error messages of 'The form contains 3 errors'" do
        expect(response.body).to include "The form contains 3 errors"
      end
    end
  end
```

### 10.20

`before_action`が正しく働いていることをテストするため、ユーザーがログインしていない時の挙動をテストします。

`context`でログインしている時/していない時を分けて書きました。

```ruby:spec/requests/users_spec.rb
  # 省略...
  describe "#edit" do
    let(:user) { FactoryBot.create(:user) }

    context "as a logged in user" do
      before do
        log_in_request(user)
      end

      it "has a correct title" do
        get edit_user_path(user)
        expect(response.body).to include full_title("Edit user")
      end
    end

    context "as a non logged in user" do
      it "has a flash" do
        get edit_user_path(user)
        expect(flash).to be_any
      end

      it "redirects to login_path" do
        get edit_user_path(user)
        expect(response).to redirect_to login_path
      end
    end

  end

  # 省略...
  describe "#update" do
    let(:user) { FactoryBot.create(:user) }

    context "as a logged in user" do
      # 省略...
    end

    context "as a non logged in user" do
        before do
          @another_user_params = { name: "Another name",
            email: "another@gmail.com",
            password: "",
            password_confirmation: "" }

          patch user_path(user), params: { user: @another_user_params }
        end

        it "can't edit" do
          user.reload
          expect(user.name).to_not eq @another_user_params[:name]
          expect(user.email).to_not eq @another_user_params[:email]
        end

        it "redirects to root" do
          expect(response).to redirect_to login_path
        end

        it "has a error flash" do
          expect(flash).to be_any
        end
    end
  end
```

### 10.24

間違ったユーザーが編集しようとした時のテストを実装します。

```ruby:spec/requests/users_spec.rb
  describe "#edit" do
    let(:user) { FactoryBot.create(:user) }

    context "as a wrong user" do
      before do
        wrong_user = FactoryBot.create(:another_user)
        log_in wrong_user
      end

      it "redirects to root" do
        get edit_user_path(user)
        expect(response).to redirect_to root_url
      end
    end

  describe "#update" do
    let(:user) { FactoryBot.create(:user) }

    context "as a wrong user" do
      before do
        wrong_user = FactoryBot.create(:another_user)
        another_user_params = { name: "Another name",
          email: "another@gmail.com",
          password: "",
          password_confirmation: "" }

        log_in wrong_user
        patch user_path(user), params: { user: another_user_params }
      end

      it "redirects to root" do
        expect(response).to redirect_to root_url
      end
    end
```

### 10.29

フレンドリーフォワーディングのテストを書きます。

```ruby:spec/requests/users_spec.rb
describe "#edit" do
  let(:user) { FactoryBot.create(:user) }

  context "as a non logged in user" do
      it "redirects to edit when logged in" do
        get edit_user_path(user)
        log_in user
        expect(response).to redirect_to edit_user_path(user)
      end
  end
```

### 10.2.3 演習

初回のみフレンドリーフォワーディングされ、次回以降はデフォルトのURLにリダイレクトされることをテストします。

ログアウトするヘルパーメソッドを実装します。

```ruby:spec/support/login.rb
module LoginSupport
  # 省略...
  def log_out
    session[:user_id] = nil
  end
```

先程書いたフレンドリーフォワーディングのテストを書き換えます。

> ヒント: `session[:forwarding_url]`が正しい値かどうか確認するテストを追加してみましょう。

と書いてありましたがガン無視してしまいました。

```ruby:spec/requests/users_spec.rb
  it "does friendly forwarding only the first time and redirects the subsequent logins to the default" do
    # 未ログインでeditへアクセス
    get edit_user_path(user)
    # 1回目のログイン(フレンドリーフォワーディングされる)
    log_in user
    expect(response).to redirect_to edit_user_path(user)
    # 2回目のログイン
    log_out
    log_in user
    expect(response).to redirect_to user
  end
```

### 10.34

ログインしていない時に`index`アクションが正しくリダイレクトするかテストします。

```ruby:spec/requests/users_spec.rb
describe "#index" do
  let(:user) { FactoryBot.create(:user) }

  context "as a logged in user" do
    # 後で書く
  end

  context "as a non logged in user" do
    it "redirects to login_path" do
      get users_path
      expect(response).to redirect_to login_path
    end
  end
end
```

### 10.3.1 演習

全てのリンクに対してテストを書いていきます。

`describe`でヘッダー/フッターを分け、`context`でログイン/非ログインを分けて書きました。
リンクの動作検証には`have_current_path`を使いました。

参考 : [Module: Capybara::SessionMatchers — Documentation for capybara (3.36.0)](https://www.rubydoc.info/gems/capybara/Capybara/SessionMatchers#has_current_path%3F-instance_method)

```ruby:spec/system/layouts_spec.rb
RSpec.describe "Layouts", type: :system do
  before do
    driven_by(:rack_test)
  end
  let(:user) { FactoryBot.create(:user) }

  describe "header" do
    context "as a logged in user" do
      before do
        log_in user
        visit root_path
      end

      describe "Account" do
        before do
          click_link "Account"
        end

        it "click the Profile to move to user's profile" do
          click_link 'Profile'
          expect(page).to have_current_path user_path(user)
        end

        it "click the Sessings to move to user's setting" do
          click_link 'Settings'
          expect(page).to have_current_path edit_user_path(user)
        end

        it "click the Log out to move to log out" do
          click_link 'Log out'
          expect(page).to have_current_path root_path
        end
      end

      it "click the sample app to move to root" do
        # rootに遷移することを確認したいのでhelpに移動する
        click_link "Help"
        click_link "sample app"
        expect(page).to have_current_path root_path
      end

      it "click the Home to move to root" do
        # rootに遷移することを確認したいのでhelpに移動する
        click_link "Help"
        click_link "Home"
        expect(page).to have_current_path root_path
      end

      it "click the Help to move to help" do
        click_link "Help"
        expect(page).to have_current_path help_path
      end
    end

    context "as a non logged in user" do
      before do
        visit root_path
      end

      it "click the Log in to move to log in" do
        click_link 'Log in'
        expect(page).to have_current_path login_path
      end

      it "click the sample app to move to root" do
        # rootに遷移することを確認したいのでhelpに移動する
        click_link "Help"
        click_link "sample app"
        expect(page).to have_current_path root_path
      end

      it "click the Home to move to root" do
        # rootに遷移することを確認したいのでhelpに移動する
        click_link "Help"
        click_link "Home"
        expect(page).to have_current_path root_path
      end

      it "click the Help to move to help" do
        click_link "Help"
        expect(page).to have_current_path help_path
      end
    end
  end

  describe "footer" do
    context "as a logged in user" do
      before do
        log_in user
        visit root_path
      end

      it "click the About to move to about" do
        click_link "About"
        expect(page).to have_current_path about_path
      end

      it "click the Contact to move to contact" do
        click_link "Contact"
        expect(page).to have_current_path contact_path
      end
    end

    context "as a non logged in user" do
      before do
        visit root_path
      end

      it "click the About to move to about" do
        click_link "About"
        expect(page).to have_current_path about_path
      end

      it "click the Contact to move to contact" do
        click_link "Contact"
        expect(page).to have_current_path contact_path
      end
    end
  end
end
```

### 10.47

ページネーションのテストのために、FactoryBotで多くのユーザーを作れるようにします。
シーケンスを使うことでユニークな値の重複を無くす事ができます。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :many_users, class: User do
    sequence(:name) { |n| "Example User #{n}" }
    sequence(:email) { |n| "example-#{n}@gmail.com" }
    password { 'password' }
    password_confirmation { 'password' }
  end
```

### 10.48

`index`に対するテストを書きます。
具体的には、ページネーションが存在すること、ユーザーごとのリンクが存在することをテストします。

```ruby:spec/requests/users_spec.rb
  describe "#index" do
    let(:user) { FactoryBot.create(:user) }

    context "as a logged in user" do
      before do
        30.times do
          FactoryBot.create(:many_users)
        end
        log_in user
        get users_path
      end

      it "has a correct title" do
        expect(response.body).to include full_title("All users")
      end

      it "has a pagination" do
        pagination = '<div role="navigation" aria-label="Pagination" class="pagination">'
        expect(response.body).to include pagination
      end

      it "has a link for each user" do
        User.paginate(page: 1).each do |user|
          expect(response.body).to include "<a href=\"#{user_path(user)}\">"
        end
      end
    end

    context "as a non logged in user" do
      it "redirects to login_path" do
        get users_path
        expect(response).to redirect_to login_path
      end
    end
  end
```

### 10.56

`admin`属性を実装したので、変更が禁止されていることをテストします。
後の変更で最初のユーザーは`admin`属性を持つようになるので、他のユーザーを使用します。

```ruby:spec/requests/users_spec.rb
RSpec.describe "Users", type: :request do
  describe "PATCH /users" do
    it "can't change admin attribute via web" do
      # 最初のユーザーはadminなので他のユーザーを使用
      user = FactoryBot.create(:other_user)
      expect(user).to_not be_admin

      log_in user
      patch user_path(user), params: { user: {
          password: "password",
          password_confirmation: "password",
          admin: true
        }
      }
      user.reload
      expect(user).to_not be_admin
    end
  end
```

### 10.61

`destroy`アクションのアクセス制御をテストします。
具体的には、ログインしていないユーザーであればログイン画面にリダイレクトされること、ログイン済であっても管理者でなければルートにリダイレクトされることをテストします。

```ruby:spec/requests/users_spec.rb
  describe "DELETE /users/id" do
    # userはadmin
    let!(:user) { FactoryBot.create(:user) }
    let(:other_user) { FactoryBot.create(:other_user) }

    context "as a non-logged in user" do
      it "redirects to login_path" do
        delete user_path(user)
        expect(response).to redirect_to root_url
      end

      it "can't delete" do
        expect {
          delete user_path(user)
        }.to_not change(User, :count)
      end
    end

    context "as a logged in user" do
      context "as a non-admin user" do
        before do
          log_in other_user
        end

        it "redirects to root" do
          delete user_path(user)
          expect(response).to redirect_to root_url
        end

        it "can't delete a user" do
          expect {
            delete user_path(user)
          }.to_not change(User, :count)
        end
      end

      context "as an admin user" do
        before do
          log_in user
        end
        # 後で書く
      end
    end
  end
```

### 10.62

管理者としてログインした時は`index`に削除リンクが表示されていること、`destroy`でユーザーの削除が出来ることをテストします。

削除リンクが表示されていることのテスト。

```ruby:spec/system/users_spec.rb
describe '#index' do
  let!(:admin) { FactoryBot.create(:user) }
  let!(:non_admin_user) { FactoryBot.create(:other_user) }

  context "as a admin user" do
    it "has a link to delete" do
      log_in admin
      visit users_path

      expect(page).to have_link "delete"
    end
  end

  context "as a non-admin user" do
    it "doesn't have a link to delete" do
      log_in non_admin_user
      visit users_path

      expect(page).to_not have_link "delete"
    end
  end
end
```

`admin`の場合、ユーザーを削除出来るかテスト。

```ruby:spec/requests/users_spec.rb
  describe "DELETE /users/id" do
    # userはadmin
    let!(:user) { FactoryBot.create(:user) }
    let!(:other_user) { FactoryBot.create(:other_user) }
      # 省略...
      context "as an admin user" do
        before do
          log_in user
        end

        it "can delete a user" do
          expect{
            delete user_path(other_user)
          }.to change(User, :count).by -1
        end
      end
```

## 答え合わせ

### `module`のネスト

ログインヘルパーの実装で、例では`module`をネストして書いていました。

> ```ruby:spec/support/login_support.rb
> module LoginSupport
> def logged_in?
>   !session[:user_id].nil?
> end
> module System
>   def log_in(user)
>     visit login_path
>
>     fill_in 'Email', with: user.email
>     fill_in 'Password', with: user.password
>     click_button 'Log in'
>   end
> end
>
> module Request
>   def log_in(user)
>     post login_path, params: { session: { email: user.email,
>                                           password: user.password } }
>   end
>
>   def logged_in?
>     !session[:user_id].nil?
>   end
> end
> end
>
> RSpec.configure do |config|
>  config.include LoginSupport
>  config.include LoginSupport::System, type: :system
>  config.include LoginSupport::Request, type: :request
> end
> ```

このようにすることでシステムスペック用とリクエストスペック用で`module`を分ける事ができます。
実装する時に「コレ`module`の中で分けられないかな・・・」とか思っていたのですが、当然のように出来ました。
ちゃんと調べるべきでした。

# 11章 アカウントの有効化

## RSpecで書き換える

### 11.4

ユーザー有効化のために`activated` `activated_at` 属性をユーザーに追加したので、ファクトリに反映させます。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user do
    name { "Example User" }
    email { "example@email.com" }
    password { "securePassword" }
    password_confirmation { "securePassword" }
    admin { true }
    activated { true }
    activated_at { Time.zone.now }
  end
  # 省略...
```

### 11.20

ユーザー有効化のためにメールを実装したので、そのテストを実装していきます。

`rails g mailer`を実行した時、メイラー用のスペックが自動で生成されていました。

```ruby:spec/mailers/user_mailer_spec.rb
# 自動生成されたスペック
RSpec.describe UserMailer, type: :mailer do
  describe "account_activation" do
    let(:mail) { UserMailer.account_activation }

    it "renders the headers" do
      expect(mail.subject).to eq("Account activation")
      expect(mail.to).to eq(["to@example.org"])
      expect(mail.from).to eq(["from@example.com"])
    end

    it "renders the body" do
      expect(mail.body.encoded).to match("Hi")
    end
  end
```

上のコードをベースに、タイトル・メールの`from`/`to`・本文に含まれるべきテキストなどをテストすれば良さそうです。

```ruby:spec/mailers/user_mailer_spec.rb
RSpec.describe UserMailer, type: :mailer do
  describe "account_activation" do
    let(:user) { FactoryBot.create(:user)}
    let(:mail) { UserMailer.account_activation(user) }
    let(:from_address) { "noreply@example.com" }

    it "sends to the user's email address" do
      expect(mail.to).to eq [user.email]
    end

    it "sends with the correct subject" do
      expect(mail.subject).to eq("Account activation")
    end

    it "sends from the correct email address" do
      expect(mail.from).to eq [from_address]
    end

    describe "body" do
      before do
        user.activation_token = User.new_token
      end
      it "includes the user's name" do
        expect(mail.body.encoded).to match(user.name)
      end

      it "includes the user's email" do
        expect(mail.body.encoded).to match(CGI.escape(user.email))
      end

      it "includes the activation token" do
        expect(mail.body.encoded).to match(user.activation_token)
      end
    end
  end
```

#### エラー

なお、最初にテストを実行したとき、以下のようなエラーを吐きました。

```bash
Failure/Error: <%= link_to "Activate", edit_account_activation_url(@user.activation_token,

ActionView::Template::Error:
  Missing host to link to! Please provide the :host parameter, set default_url_options[:host], or set :only_path to true
```

このエラーに対処するため、次のように設定を追記しました。

```ruby:config/environments/test.rb
# 追記
config.action_mailer.default_url_options = { host: "localhost:3000"}
```

参考
[rspec - Rails: Missing host to link to! Please provide :host parameter or set default_url_options[:host] - Stack Overflow](https://stackoverflow.com/questions/7219732/rails-missing-host-to-link-to-please-provide-host-parameter-or-set-default-ur)
[Action Mailer の基礎 - Railsガイド](https://railsguides.jp/action_mailer_basics.html#action-mailer%E3%81%AE%E3%83%93%E3%83%A5%E3%83%BC%E3%81%A7url%E3%82%92%E7%94%9F%E6%88%90%E3%81%99%E3%82%8B)

### 11.33

ユーザー登録のテストにアカウント有効化を追加していきます。

`User#create`のテスト。

```ruby:spec/requests/users_spec.rb
  describe "#create" do
    let(:user) { FactoryBot.create(:user) }
    let(:valid_user_params) { FactoryBot.attributes_for(:user) }
    let(:invalid_user_params) { FactoryBot.attributes_for(:invalid_user) }

    context "with valid information" do
      before do
        ActionMailer::Base.deliveries.clear
      end

      # 省略...

      it "exists an email" do
        post users_path, params: { user: valid_user_params }
        expect(ActionMailer::Base.deliveries.size).to eq 1
      end

      it "hasn't yet been activated" do
        post users_path, params: { user: valid_user_params }
        expect(User.last).to_not be_activated
      end
```

アカウント有効化のテスト。

```ruby:spec/requests/account_activations_spec.rb
RSpec.describe "AccountActivations", type: :request do
  describe GET "/account_activations/id/edit" do
    let(:valid_user_params) { FactoryBot.attributes_for(:user) }
    before do
      post users_path, params: { user: valid_user_params }
      @user = controller.instance_variable_get(:@user)
    end

    context "with valid token and email" do
      it "activates user" do
        get edit_account_activation_path(@user.activation_token, email: @user.email)
        @user.reload
        expect(@user).to be_activated
      end

      it "redirects to users/id" do
        get edit_account_activation_path(@user.activation_token, email: @user.email)
        expect(response).to redirect_to user_path(@user)
      end

      it "can loge in" do
        get edit_account_activation_path(@user.activation_token, email: @user.email)
        expect(logged_in?).to be_truthy
      end
    end

    context "with invalid attributes" do
      it "doesn't log in with invalid token" do
        get edit_account_activation_path("invalid_token", email: @user.email)
        expect(logged_in?).to_not be_truthy
      end

      it "doesn't log in with invalid email" do
        get edit_account_activation_path(@user.activation_token, email: "wrong email")
        expect(logged_in?).to_not be_truthy
      end
    end
  end
end

```

`UsersController`の`create`アクションで定義されたインスタンス変数にアクセスするために、Railsチュートリアルでは`assigns`メソッドを使っていました。
(DBから逐一ユーザーを取ってくるよりもインスタンス変数が扱えたほうが便利なので)

ここでは`instance_variable_get`というメソッドを使ってアクセスしています。

[Object#instance_variable_get (Ruby 3.1 リファレンスマニュアル)](https://docs.ruby-lang.org/ja/latest/method/Object/i/instance_variable_get.html)

#### エラー

テスト実行時に以下のエラーを吐きました。

```bash
NoMethodError:
      undefined method `signed' for #<Rack::Test::CookieJar:0x00007fe62a914b38>
```

エラーの発生源は`sessions_helper.rb`の`current_user`メソッド(現在のユーザーを取得するメソッド)でした。
`cookies.signed`の呼び出しでエラーが発生しているようです。

[Railsアプリのテスト実行中に cookies.signed がエラー（undefined） になったときの対処法 - Qiita](https://qiita.com/yoshikouki/items/29c39ccccdc3a3814b17)

↑の記事を参考に`spec/support/cookies.rb`を追加、次のコードを追記して対処しました。
`Cookies`クラスの参照元が環境によって異なることが原因のようです。

```spec/support/cookies.rb
# RSpecでcookies.signedがエラーになる対処
class Rack::Test::CookieJar
  def signed
    self
  end
end
```

### 11.3.3

`users`で有効化されていないユーザーが表示されないこと。

```ruby:spec/system/users_spec.rb
  describe "GET /users" do
    let!(:admin) { FactoryBot.create(:user) }
    let!(:non_admin_user) { FactoryBot.create(:other_user) }

    # 省略...

    context "as a non-admin user" do
      it "doesn't display inactivated user" do
        inactivated_user = FactoryBot.create(:inactivated_user)
        log_in non_admin_user
        get users_path
        expect(response.body).to_not include inactivated_user.name
      end
    end
```

有効化していないユーザーの詳細ページにアクセス出来ないこと。

```ruby:spec/requests/users_spec.rb
  describe "GET /users/id" do
    let(:user) { FactoryBot.create(:user) }
    let(:inactivated_user) { FactoryBot.create(:inactivated_user) }

    context "visit inactivated user" do
      it "redirects to root" do
        log_in user
        get user_path(inactivated_user)
        expect(response).to redirect_to root_url
      end
    end
  end
```


## 答え合わせ

[コード例〜第11章〜｜RailsチュートリアルのテストをRSpecで書き換える](https://zenn.dev/fu_ga/books/ff025eaf9eb387/viewer/07a432)

実装はほぼ一緒でした。

# 12章 パスワードの再設定

## RSpecで書き換え

### 12.12

アカウント有効化のときと同様に、パスワードリセット用メールのテストを書きます。

ユーザーリセット用のトークンが無いとメールに含まれるURLを生成出来ないので、`before`で生成します。

```ruby:spec/mailers/user_mailer_spec.rb
RSpec.describe UserMailer, type: :mailer do
  let(:user) { FactoryBot.create(:user)}
  let(:from_address) { "noreply@example.com" }

  describe "password_reset" do
    let(:mail) { UserMailer.password_reset(user) }
    before do
      user.reset_token = User.new_token
    end

    describe "header" do
      it "sends to the user's email address" do
        expect(mail.to).to eq [user.email]
      end

      it "sends with the correct subject" do
        expect(mail.subject).to eq("Password reset")
      end

      it "sends from the correct email address" do
        expect(mail.from).to eq [from_address]
      end
    end

    describe "body" do
      it "includes the user's email" do
        expect(mail.body.encoded).to match(CGI.escape(user.email))
      end

      it "includes the reses token" do
        expect(mail.body.encoded).to match(user.reset_token)
      end
    end
  end
```

### 12.18

パスワードリセットのテストを実装します。
長いので分けて書きます。

#### `new`

`new`のテスト。

`new`のビューでは、`form_with`によって以下のようなHTMLが生成されます。

```html
<!-- form_withにより生成されるinput-->
<input class="form-control" type="email" name="password_reset[email]" id="password_reset_email">
```

そこで、`name="password_reset[email]"`を含むことをテストします。
それにより、`params[:password_reset][:email]`で`email`にアクセス出来ることをテスト出来ます。

```ruby:spec/requests/password_resets_spec.rb
require 'rails_helper'

RSpec.describe "PasswordResets", type: :request do
  let(:user) { FactoryBot.create(:user) }
  before do
    ActionMailer::Base.deliveries.clear
  end

  describe "#new" do
    it "has a correct input form" do
      get new_password_reset_path
      expect(response.body).to include 'name="password_reset[email]"'
    end
  end

  describe "#create" do
  end

  describe "#edit" do
  end

  describe "#update" do
  end
end
```

#### `create`

`create`のテスト。
無効なメールアドレス/有効なメールアドレスの場合をそれぞれテストします。

```ruby:spec/requests/password_resets_spec.rb
  describe "#create" do
    context "with a valid email address" do
      it "creates reset digest" do
        post password_resets_path, params: { password_reset: { email: user.email } }
        user.reload
        expect(user.reset_digest).to_not be_nil
      end

      it "increases one email to sent" do
        expect{
          post password_resets_path, params: { password_reset: { email: user.email } }
        }.to change(ActionMailer::Base::deliveries, :count).by 1
      end

      it "has a success flash" do
        post password_resets_path, params: { password_reset: { email: user.email } }
        expect(flash).to_not be_empty
      end

      it "redirects to root" do
        post password_resets_path, params: { password_reset: { email: user.email } }
        expect(response).to redirect_to root_url
      end
    end

    context "with an invalid email address" do
      it "has a error flash" do
        post password_resets_path, params: { password_reset: { email: "" } }
        expect(flash).to_not be_empty
      end
      it "renders /password_resets/new" do
        post password_resets_path, params: { password_reset: { email: "" } }
        expect(response.body).to include full_title("Forgot password")
      end
      it "doesn't create a reset digest" do
        post password_resets_path, params: { password_reset: { email: "" } }
        user.reload
        expect(user.reset_digest).to be_nil
      end
    end
  end
```

#### `edit`

`edit`のテスト。
`email`、`reset_token`がそれぞれ有効な時/無効な時のテスト、ユーザーが有効化されていない時のテストを書きます。

```ruby:spec/requests/password_resets_spec.rb
  describe "#edit" do
    before do
      post password_resets_path, params: { password_reset: { email: user.email } }
      @user = controller.instance_variable_get(:@user)
    end

    context "with valid attributes" do
      it "accesses successfully" do
        get edit_password_reset_path(@user.reset_token, email: user.email)
        expect(response.body).to include full_title("Reset password")
      end

      it "has a correct hidden form" do
        # メールアドレスを保持するためのフォーム
        form = "<input type=\"hidden\" name=\"email\" id=\"email\" value=\"#{@user.email}\" />"

        get edit_password_reset_path(@user.reset_token, email: user.email)
        expect(response.body).to include form
      end
    end

    context "with invalid attributes" do
      it "redirects to root with an invalid email" do
        get edit_password_reset_path(@user.reset_token, email: "")
        expect(response).to redirect_to root_url
      end

      it "redirects to root with an invalid token" do
        get edit_password_reset_path("Invalid token", email: user.email)
        expect(response).to redirect_to root_url
      end
    end

    context "as an inactivated user" do
      it "redirects to root" do
        @user.toggle!(:activated)
        get edit_password_reset_path(@user.reset_token, email: user.email)
        expect(response).to redirect_to root_url
      end
    end
  end
```

#### `update`

`update`のテスト。
`password`と`password_confirmation`が有効な場合/無効な場合のテストをそれぞれ書きます。

また、Railsチュートリアルで実装されていたテストに加えて、パスワードが変更されていることを確認するテストを追加しました。

```ruby:spec/requests/password_resets_spec.rb
  describe "#update" do
    before do
      post password_resets_path, params: { password_reset: { email: user.email } }
      @user = controller.instance_variable_get(:@user)
    end

    context "with valid attributes" do
      it "will be logged in" do
        patch password_reset_path(@user.reset_token), params: {
          email: @user.email,
          user: { password: "newPassword", password_confirmation: "newPassword" }
        }
        expect(is_logged_in?).to be_truthy
      end

      it "has a success flash" do
        patch password_reset_path(@user.reset_token), params: {
          email: @user.email,
          user: { password: "newPassword", password_confirmation: "newPassword" }
        }
        expect(flash).to_not be_empty
      end

      it "redirects to user's profile" do
        patch password_reset_path(@user.reset_token), params: {
          email: @user.email,
          user: { password: "newPassword", password_confirmation: "newPassword" }
        }
        expect(response).to redirect_to user
      end

      it "changes user's password" do
        patch password_reset_path(@user.reset_token), params: {
          email: @user.email,
          user: { password: "newPassword", password_confirmation: "newPassword" }
        }
        old_password = @user.password_digest
        @user.reload
        expect(@user.authenticated?(:password, old_password)).to_not be_truthy
      end
    end

    context "with invalid attributes" do
      it "has a error message with invalid password and password_confirmation" do
        patch password_reset_path(@user.reset_token), params: {
          email: @user.email,
          user: { password: "newPassword", password_confirmation: "wrongPassword" }
        }
        expect(response.body).to include '<div id="error_explanation">'
      end

      it "has a error message with empty password" do
        patch password_reset_path(@user.reset_token), params: {
          email: @user.email,
          user: { password: "", password_confirmation: "" }
        }
        expect(response.body).to include '<div id="error_explanation">'
      end
    end
  end
```

### 12.21

パスワード再設定用トークンが期限切れになった場合のテストを実装します。

```ruby:spec/requests/password_resets_spec.rb
  describe "#edit" do
    before do
      post password_resets_path, params: { password_reset: { email: user.email } }
      @user = controller.instance_variable_get(:@user)
    end

    context "with expired token" do
      before do
        @user.update_attribute(:reset_sent_at, 3.hours.ago)
      end
      it "redirects to new_password_reset_path" do
        get edit_password_reset_path(@user.reset_token, email: @user.email)
        expect(response).to redirect_to new_password_reset_path
      end
    end
  end



  describe "#update" do
    before do
      post password_resets_path, params: { password_reset: { email: user.email } }
      @user = controller.instance_variable_get(:@user)
    end

    context "with expired token" do
      before do
        @user.update_attribute(:reset_sent_at, 3.hours.ago)
      end

      it "has a correct error message of expired" do
        patch password_reset_path(@user.reset_token), params: {
          email: @user.email,
          user: { password: "newPassword", password_confirmation: "newPassword" }
        }
        follow_redirect!
        expect(response.body).to include "Password reset has expired"
      end

      it "redirects to new_password_reset_path" do
        patch password_reset_path(@user.reset_token), params: {
          email: @user.email,
          user: { password: "newPassword", password_confirmation: "newPassword" }
        }
        expect(response).to redirect_to new_password_reset_path
      end
    end
  end
```

テストの中で`follow_redirect!`というメソッドを使っています。
このメソッドは最後のレスポンスで返されたリダイレクトに従ってリダイレクトを実行するメソッドです。
これにより、リダイレクト後のページに対するテストを実装することが出来ます。

参考 : [follow_redirect! (ActionController::Integration::Session) - APIdock](https://apidock.com/rails/ActionController/Integration/Session/follow_redirect%21)

### 12.3.3 演習

パスワードリセットに成功したら`reset_digest`が`nil`になることをテストします。

```ruby:spec/requests/password_resets_spec.rb
  describe "#update" do
    before do
      post password_resets_path, params: { password_reset: { email: user.email } }
      @user = controller.instance_variable_get(:@user)
    end

    context "with valid attributes" do
      it "sets reset_digest to nil" do
        patch password_reset_path(@user.reset_token), params: {
          email: @user.email,
          user: { password: "newPassword", password_confirmation: "newPassword" }
        }
        @user.reload
        expect(@user.reset_digest).to be_nil
      end
```

## 答え合わせ

[コード例〜第12章〜｜RailsチュートリアルのテストをRSpecで書き換える](https://zenn.dev/fu_ga/books/ff025eaf9eb387/viewer/9012ff)

ほぼ同じでした。

# まとめ

スペックを書くときはだいたい以下を意識しておけば良さそうな気がします。

- 最初にテストのアウトラインを書くと楽。
  - `describe`や`it`、`context`を最初に記述してしまう。
- 認可に対するテストでは、予め`context`や`describe`でテストしたい条件に分割しておく。
- テストコード内に重複する箇所が増えてきたら適度にDRYにする。
  - あくまでも可読性重視。
- 複雑なテストデータはFactoryBot及びトレイトを上手く使う。

また、載せきれていませんが、進めていく中で「こっちの方が英文が自然だな・・・」と感じて直す場面がそこそこありました。

最初の記事で「英語にしたことによってムダなコストが生じない場合英語で書けば良いんじゃね」と書きました。
「どう書けば英文として自然か？」などと考えている時点でムダなコストが生じてしまっているので、日本語で書くべきでした。英語の練習も兼ねていると考えれば別ですが。