# 13章 ユーザーのマイクロポスト

### 13.4

`Micropost`モデル(ユーザーに紐付けられた投稿)に対する最初のテストを書きます。

```ruby:spec/models/micropost_spec.rb
RSpec.describe Micropost, type: :model do
  let(:user) { FactoryBot.create(:user) }
  let(:micropost) { Micropost.new(content: "Test post", user_id: user.id) }

  context "with valid attributes" do
    it "is valid" do
      expect(micropost).to be_valid
    end
  end

  context "with invalid attributes" do
    it "is invalid without user_id" do
      micropost.user_id = nil
      expect(micropost).to_not be_valid
    end
  end
end
```

### 13.7

`Micropost`に対するバリデーションのテストを実装します。
`content`は長さに対するバリデーション(141文字以内)があるので、境界値テストを実装しました。

```ruby:spec/models/micropost_spec.rb
require 'rails_helper'

RSpec.describe Micropost, type: :model do
  let(:user) { FactoryBot.create(:user) }
  let(:micropost) { Micropost.new(content: "Test post", user_id: user.id) }

  context "with valid attributes" do
    it "is valid" do
      expect(micropost).to be_valid
    end

    it "is valid with content equal to the boundary value" do
      micropost.content = "a" * 140
      expect(micropost).to be_valid
    end
  end

  context "with invalid attributes" do
    it "is invalid without user_id" do
      micropost.user_id = nil
      expect(micropost).to_not be_valid
    end

    it "is invalid without a content" do
      micropost.content = ""
      expect(micropost).to_not be_valid
    end

    it "is invalid with a too long content" do
      micropost.content = "a" * 141
      expect(micropost).to_not be_valid
    end
  end
end
```

### 13.12

`has_many`されている投稿の作成を慣習的に正しい方法に変更します。

```ruby:spec/models/micropost_spec.rb
RSpec.describe Micropost, type: :model do
  let(:user) { FactoryBot.create(:user) }
  let(:micropost) { user.microposts.build(content: "Test post") }
  # 省略...
```

### 13.14

`Micropost`の順序付けをテストします。
実際のFactoryBotの中身は後で実装していきます。

ついでに`describe`でバリデーションのテストを1まとめにします。

```ruby:spec/models/micropost_spec.rb
RSpec.describe Micropost, type: :model do
  let(:user) { FactoryBot.create(:user) }
  let(:micropost) { FactoryBot.create(:micropost) }

  it "is sorted by newest to oldest" do
    expect(FactoryBot.create(:most_recent_post)).to eq Micropost.first
  end

  describe "validation" do
    context "with valid attributes" do
      it "is valid" do
        expect(micropost).to be_valid
      end
      # 省略...
```

### 13.15

順序付けテスト用のデータを作成します。

素直に投稿時間が違うデータを複数作ります。

```ruby:spec/models/micropost_spec.rb
FactoryBot.define do
  factory :micropost do
    content { "Test post" }
    association :user

    trait :most_recent do
      created_at { Time.zone.now }
    end

    trait :some_time_ago do
      created_at { 30.minutes.ago }
    end

    trait :yesterday do
      created_at { 1.day.ago }
    end

    trait :last_week do
      created_at { 1.week.ago }
    end

    trait :last_month do
      created_at { 1.month.ago }
    end

  end
end
```

ヘルパーメソッドを作り、そこからFactoryBotを呼び出します。

```ruby:spec/support/microposts.rb
module PostSupport
  def create_posts_different_posting_time(test_object: :most_recent)
    FactoryBot.create(:micropost, test_object)
    FactoryBot.create(:micropost, :some_time_ago)
    FactoryBot.create(:micropost, :yesterday)
    FactoryBot.create(:micropost, :last_week)
  end
end

RSpec.configure do |config|
  config.include PostSupport
end
```

定義したヘルパーメソッドをテストで呼び出します。

```ruby:spec/models/micropost_spec.rb
RSpec.describe Micropost, type: :model do
  let(:user) { FactoryBot.create(:user) }
  let(:micropost) { FactoryBot.create(:micropost) }

  it "is sorted by newest to oldest" do
    create_posts_different_posting_time
    expect(FactoryBot.create(:micropost, :most_recent)).to eq Micropost.first
  end
  # 省略...
```

#### ユーザーの重複

テストを実行したところ、次のようなエラーが出ました。

```bash
Failure/Error: FactoryBot.create(:micropost, :yesterday) # 2番目に作られるデータ

ActiveRecord::RecordInvalid:
  Validation failed: Email has already been taken
```

どうやら毎回違う`User`を作成しているようです。
そのため、`email`のバリデーションによりエラーが発生します。

この問題に対処するため、`User`のファクトリを修正します。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user do
    sequence(:name) { |n| "Example User #{n}" }
    sequence(:email) { |n| "example-#{n}@gmail.com" }
    password { "securePassword" }
    password_confirmation { "securePassword" }
    activated { true }
    activated_at { Time.zone.now }
  # 省略...
```

`name`と`email`に対して、デフォルトでシーケンスを利用するように変更を加えます。
この時`User`ファクトリの他の箇所もリファクタリングしました(後述)。

この変更により、無事テストがパスするようになります。

念の為本当にユーザーが変わっているのか見てみます。

```ruby:spec/models/micropost_spec.rb
it "is sorted by newest to oldest" do
  create_posts_different_posting_time
  Micropost.all.each { |m| puts m.user_id }
  expect(FactoryBot.create(:micropost, :most_recent)).to eq Micropost.first
end

# 出力
1
2
3
4
```

OKですね。

### 13.20

`dependent: :destroy`が正しく動作することをテストします。

```ruby:spec/models/micropost_spec.rb
RSpec.describe Micropost, type: :model do
  let(:user) { FactoryBot.create(:user) }
  let(:micropost) { FactoryBot.create(:micropost) }

  describe "association" do
    it "destroyed when the associated user is destroyed" do
      user = micropost.user
      expect {
        user.destroy
      }.to change(Micropost, :count).by -1
    end
  end
```

### 13.28

マイクロポストが正しく表示されていることをテストします。

まず、複数の投稿を持ったユーザーのトレイトを作成します。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user do
    trait :with_posts do
      after(:create) { |user| create_list(:micropost, 31, user: user) }
    end
```

トレイトを呼び出すことで、複数の投稿を持ったユーザーが作成(=複数の投稿が作成)されます。
これにより、複数の投稿が存在する状態でUIをテストすることが出来ます。

残りは通常のシステムスペックです。

```ruby:spec/system/microposts_spec.rb
RSpec.describe "Microposts", type: :system do
  let(:user) { FactoryBot.create(:user) }

  before do
    driven_by(:rack_test)
  end

  describe "users/id" do
    before do
      @user = FactoryBot.create(:user, :with_posts)
      log_in @user
    end

    it "has a pagination" do
      expect(page).to have_selector "div.pagination"
    end

    it "has 30 posts per page" do
      posts_container = within 'ol.microposts' do
        find_all('li')
      end
      expect(posts_container.length).to eq 30
    end

    it "displays micropost counts" do
      expect(page).to have_content @user.microposts.count.to_s
    end

    it "displays contents of each post" do
      @user.microposts.paginate(page: 1).each do |micropost|
        expect(page).to have_content micropost.content
      end
    end
  end
end
```

`"has 30 posts per page"`では、Capybaraの`within`メソッドを使って「特定のセレクタ内」にスコープを特定しています。
このようにすることで、`ol.microposts`の子要素として存在する投稿の数をカウントすることが出来ます。


### 13.2.3 演習

ページネーションの表示が一度のみ(一箇所のみ?)であることをテストするように変更します。

```ruby:spec/system/microposts_spec.rb
  # 省略...
    it "has a pagination" do
      pagination = find_all("div.pagination")
      expect(pagination.length).to eq 1
    end
```

### 13.31

マイクロポストの操作に関するテストを書きます。

```ruby:spec/requests/microposts_spec.rb
require 'rails_helper'

RSpec.describe "Microposts", type: :request do

  describe "POST /microposts" do
    context "as a logged in user" do
      # 後で書く
    end

    context "as a non-logged in user" do
      it "redirects to login_path" do
        post microposts_path, params: { micropost: { content: "Test post" } }
        expect(response).to redirect_to login_path
      end

      it "doesn't create a post" do
        expect{
          post microposts_path, params: { micropost: { content: "Test post" } }
        }.to_not change(Micropost, :count)
      end
    end
  end

  describe "DELETE /microposts/id" do
    let!(:micropost) { FactoryBot.create(:micropost) }

    context "as a logged in user" do
      # 後で書く
    end

    context "as a non-logged in user" do
      it "redirects to login_path" do
        delete micropost_path(micropost)
        expect(response).to redirect_to login_path
      end
      it "doesn't delete a post" do
        expect{
          delete micropost_path(micropost)
        }.to_not change(Micropost, :count)
      end
    end
  end
end
```

### 13.55

自分以外のユーザーのマイクロソフトを削除しようとすると失敗することをテストします。

```ruby:spec/requests/microposts_spec.rb
  describe "DELETE /microposts/id" do
    let!(:micropost) { FactoryBot.create(:micropost) }

    context "as a logged in user" do
      context "as a wrong user" do
        before do
          wrong_user = FactoryBot.create(:user)
          log_in(wrong_user)
        end

        it "redirects to root_url" do
          delete micropost_path(micropost)
          expect(response).to redirect_to root_url
        end

        it "does't delete a post" do
          expect {
            delete micropost_path(micropost)
          }.to_not change(Micropost, :count)
        end
      end
      context "as a correct user" do
        # 後で書く
      end
    end
```

### 13.56

マイクロポストのUIに対するテストを書きます。

```ruby:spec/system/microposts_spec.rb
RSpec.describe "Microposts", type: :system do
  before do
    driven_by(:rack_test)
  end

  describe "/root" do
    before do
      @user = FactoryBot.create(:user, :with_posts)
      log_in @user
      visit root_path
    end

    describe "POST /microposts" do

      context "with valid attributes" do
        it "creates a post" do
          expect {
            fill_in "micropost_content", with: "Test Post"
            click_button "Post"
          }.to change(Micropost, :count).by 1

          expect(page).to have_content "Test Post"
        end
      end

      context "with invalid attributes" do
        it "doesn't create a post without a content" do
          expect {
            fill_in "micropost_content", with: ""
            click_button "Post"
          }.to_not change(Micropost, :count)

          expect(page).to have_selector 'div#error_explanation'
          expect(page).to have_link '2', href: '/?page=2'
        end
      end
    end

    describe "DELETE /micropost/id" do

      context "as a correct user" do
        it "deletes a post" do
          post = @user.microposts.first
          expect(page).to have_link "delete"

          expect {
            click_link "delete", href: micropost_path(post)
          }.to change(Micropost, :count).by -1

          expect(page).to_not have_content post.content
        end
      end

      context "as a wrong user" do
        let(:wrong_user) { FactoryBot.create(:user) }

        it "doesn't delete a post" do
          visit user_path(wrong_user)
          expect(page).to_not have_link "delete"
        end
      end
    end
  end
end
```

### 13.58

サイドバー(マイクロポストの投稿数の表示)のテストを書きます。

投稿の数が0/1の時、単数/複数形が正しく表示されていることをテストします。
投稿を持たない他のユーザーでログインすることも考えましたが、
`destroy_all`で投稿全削除→`visit root_path`でリロードすることで実装しました。

```ruby:spec/system/microposts_spec.rb
  describe "/root" do
    before do
      @user = FactoryBot.create(:user, :with_posts)
      log_in @user
      visit root_path
    end

    describe "sidebar" do
      it "displays micropost counts" do
        expect(page).to have_content @user.microposts.count.to_s
      end

      it "displays 0 microposts with 0 posts" do
        @user.microposts.destroy_all
        visit root_path
        expect(page).to have_content "0 microposts"
      end

      it "displays 1 micropost with a post" do
        @user.microposts.destroy_all
        fill_in "micropost_content", with: "Test Post"
        click_button "Post"
        expect(page).to have_content "1 micropost"
      end
    end
```

### 13.64

画像アップロードのテストを実装します。

まず`spec/fixtures`にテスト用のデータを置きます。
`spec/files`の場合もあるそうです。

```bash
curl -o spec/fixtures/kitten.jpg -OL https://cdn.learnenough.com/kitten.jpg
```

テストを書きます。
`attach_file`でファイルをアップロード、`be_attached`で添付されたことを確認します。

```ruby:spec/system/micro_posts_spec.rb
  describe "/root" do
    describe "POST /microposts" do
      context "with valid attributes" do
        it "uploads an image" do
          expect {
            fill_in "micropost_content", with: "Test Post"
            attach_file "micropost_image", "#{Rails.root}/spec/fixtures/kitten.jpg"
            click_button "Post"
          }.to change(Micropost, :count).by 1

          attached_post = Micropost.first
          expect(attached_post.image).to be_attached
        end
        # 省略...
```

ちなみに、Active Storageではデフォルトで `tmp/storage` にアップロードしたファイルが保存されるようになっているので、何もしないとテストが実行される度にファイルが増えていってしまいます。

```yml:config/storage.yml
test:
  service: Disk
  root: <%= Rails.root.join("tmp/storage") %>

local:
  service: Disk
  root: <%= Rails.root.join("storage") %>
```

そのため、`rails_helper.rb`に設定を追記してアップロードされたファイルはテスト終了時に自動的に削除されるようにしておきます。

```ruby:spec/rails_helper.rb
RSpec.configure do |config|
  # 省略...
  config.after(:suite) do
    FileUtils.rm_rf(ActiveStorage::Blob.service.root)
  end
end
```

## 答え合わせ

[コード例〜第13章〜｜RailsチュートリアルのテストをRSpecで書き換える](https://zenn.dev/fu_ga/books/ff025eaf9eb387/viewer/4de804#%E3%83%AA%E3%82%B9%E3%83%8813.64)

### 複数の投稿のテストデータ

「複数の投稿」のテストデータを用意する方法がかなり違っていました。

複数の投稿の用意に定義したメソッドを使う、という点は同じでしたが、定義する場所と中身が異なっていました。

定義する場所
自分の場合 : ヘルパーメソッドとして別ファイルに定義
例 : ファクトリの中で定義。こちらの方が便利そう。

中身についても、そもそも「最新の`microposts`が最初に来ている」=「作成日時が新しい順になっている」ことをテストしたいだけなら作成日時がばらけたデータは不要だった気がします。

> 定義
>
> ```ruby:spec/factories/microposts.rb
> FactoryBot.define do
>   # 省略...
> end
>
> def user_with_posts(posts_count: 5)
>   FactoryBot.create(:user) do |user|
>     FactoryBot.create_list(:orange, posts_count, user: user)
>   end
> end
> ```

このメソッド、`FactoryBot.define do~end`の外で定義されています。
`spec/factories`配下のファイル内で定義されたメソッドは`FactoryBot`で定義されたメソッド扱いになるということ・・・？

> 呼び出し
>
> FactoryBot.send(:user_with_posts)は、リスト13.15で定義するuser_with_postsメソッドを実行しています。
> user_with_postsメソッドはprivateメソッドのためFactoryBot.user_with_postsという風には呼び出せません。
>
> ```ruby:spec/models/micropost_spec.rb
> RSpec.describe Micropost, type: :model do
>  .
>  .
>  it '並び順は投稿の新しい順になっていること' do
>    FactoryBot.send(:user_with_posts)
>    expect(FactoryBot.create(:most_recent)).to eq Micropost.first
>  end
>  .
>  .
> end
> ```

また、30個以上の投稿を作成する際、例ではファクトリの中で定義したメソッドをそのまま使っていました。
自分は複数の投稿を持つ`user`のトレイトを定義、使用していました。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user do
  # 省略...
    trait :with_posts do
      after(:create) { |user| create_list(:micropost, 31, user: user) }
    end
```

こちらについては`with_posts`トレイトを使う方が好みです。

### 13.58

現在のURLのままリロードしたい時、`current_path`が使えるようです。

```ruby
# 自分のコード
  it "displays 0 microposts with 0 posts" do
    @user.microposts.destroy_all
    visit root_path
    expect(page).to have_content "0 microposts"
  end

# 例のコード
  it '0件なら"0 microposts"、1件なら"1 micropost"と表示されること' do
    @user.microposts.destroy_all
    visit current_path
    expect(page).to have_content '0 microposts'
    # 省略...
```

# 14章 フォロー機能

# リファクタリング

## トレイトによるファクトリの重複解消(13章時点)

下のコードがリファクタリング前の状態です。

見ての通り、重複がとても多いです。
そもそも不要なファクトリ(`many_users`、`other_user`など)もあります。

```ruby:spec/factories/users.rb
FactoryBot.define do
  # 管理者
  factory :user do
    name { "Example User" }
    email { "example@email.com" }
    password { "securePassword" }
    password_confirmation { "securePassword" }
    admin { true }
    activated { true }
    activated_at { Time.zone.now }
  end

  factory :other_user ,class: User do
    name { "Other User" }
    email { "other@gmail.com" }
    password { "securePassword" }
    password_confirmation { "securePassword" }
    activated { true }
    activated_at { Time.zone.now }
  end

  factory :invalid_user, class: User do
    name { "" }
    email { "address@invalid" }
    password { "short" }
    password_confirmation { "rack" }
    activated { true }
    activated_at { Time.zone.now }
  end

  factory :many_users, class: User do
    sequence(:name) { |n| "Example User #{n}" }
    sequence(:email) { |n| "example-#{n}@gmail.com" }
    password { 'password' }
    password_confirmation { 'password' }
    activated { true }
    activated_at { Time.zone.now }
  end

  factory :inactivated_user, class: User do
    name { "inactive" }
    email { "inactivated@email.com" }
    password { "password" }
    password_confirmation { "password" }
    activated { false }
  end
end
```

トレイトを使って重複を解消していきます。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user do
    sequence(:name) { |n| "Example User #{n}" }
    sequence(:email) { |n| "example-#{n}@gmail.com" }
    password { "securePassword" }
    password_confirmation { "securePassword" }
    activated { true }
    activated_at { Time.zone.now }

    trait :admin do
      admin { true }
    end

    trait :invalid do
      name { "" }
      email { "address@invalid" }
      password { "short" }
      password_confirmation { "rack" }
    end

    trait :inactivated do
      activated { false }
      activated_at { nil }
    end
  end
end
```

かなりスッキリしました。

トレイトをスペックから呼び出す際は以下のようにします。

```ruby
let(:user) { FactoryBot.create(:user) }
let(:other_user) { FactoryBot.create(:user) }
let(:admin) { FactoryBot.create(:user, :admin) }
```

元となる`user`にシーケンスを追加したので、複数回呼び出した場合、勝手にユニークな値になってくれます。
トレイトとして定義した`hoge`を呼ぶには、`create`メソッドに`(:user, :hoge)`を渡します。

## 変数名の変更

不適切・意味がよくわからない変数名を変更しました。