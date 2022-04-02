# はじめに

Rails初学者の定番教材である[Railsチュートリアル](https://railstutorial.jp/)を完走しました。

完走後、[Railsチュートリアルの読み物ガイド](https://railstutorial.jp/reading_guide)に目を通してみて、
次のステップとして実践的なテストフレームワークであるRSpecについて学ぶことにしました。

そして、[Everyday Rails](https://leanpub.com/everydayrailsrspec-jp)を購入し、基本的なスペックが一通り書けるようになるまで進めました。

教材を通読・サンプルコードを書いた程度だとまだ理解が浅いので、
実践を通じてRSpecの使い方を理解するために**RailsチュートリアルのテストをMinitestからRSpecに置き換えてみる**ことにしました。

読み物ガイドで紹介されていた下の記事を答え合わせ的に使っていきます。

https://zenn.dev/fu_ga/books/ff025eaf9eb387

## 意識すること

- 過度にDRYであることよりも可読性を重視する。
    - ただ、ファクトリの扱いには慣れたいのでテストデータの用意はなるべくファクトリで。
- Railsチュートリアルに縛られすぎない。
    - 例えば「Railsチュートリアルがコントローラテストだったからコントローラスペックを書く」のような考え方は避ける。
- まず動かし、次に正しくし、それから速くする([Make it work, make it right, make it fast](http://wiki.c2.com/?MakeItWorkMakeItRightMakeItFast))」を意識する
    - Everyday Railsで紹介されていた格言です。
    - 細かいところや便利なマッチャを使うことにこだわりすぎず、サクッとテストを書いてみる。

## 環境

Railsチュートリアルの環境をそのまま利用します。

- Ruby 2.7.4
- Ruby on Rails 6.0.4

追加でインストールするgem

- rspec-rails 5.1.1
- FactoryBot 6.2.0
- capybara 3.28.0
- selenium-webdriver 3.142.4
- webdrivers 4.1.2

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

## RSpecで書き換え

### `relationship`のファクトリ

テストを書く前に、`relationship`を生成するためのファクトリを用意します。

`relationship`モデルを見ると、`User`の関連が`follower`、`followed`という名前になっていることがわかります。

```ruby:app/models/relationship.rb
class Relationship < ApplicationRecord
  belongs_to :follower, class_name: "User"
  belongs_to :followed, class_name: "User"
end
```

このような場合は、ユーザーのファクトリに対して`aliases`を設定する必要があります。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user , aliases: [:followed, :follower] do
    sequence(:name) { |n| "Example User #{n}" }
    sequence(:email) { |n| "example-#{n}@gmail.com" }
    password { "securePassword" }
    password_confirmation { "securePassword" }
    activated { true }
    activated_at { Time.zone.now }
    # 省略...
```

`aliases`を設定すれば、`relationship`のファクトリからその名前で参照することが出来ます。

```ruby:spec/factories/relationships.rb
FactoryBot.define do
  factory :relationship do
    association :followed
    association :follower
  end
end
```

`relationship`の生成をテストしてみます。

```ruby:spec/models/relationship_spec.rb
RSpec.describe Relationship, type: :model do
  let(:relationship) { FactoryBot.create(:relationship) }
  it "generates associated data" do
    puts relationship.followed_id
    puts relationship.followed.inspect
    puts relationship.follower_id
    puts relationship.follower.inspect
  end
end
```

```bash
1
#<User id: 1, name: "Example User 1", email: "example-1@gmail.com", created_at: "2022-03-26 23:06:12", updated_at: "2022-03-26 23:06:12", password_digest: [FILTERED], remember_digest: nil, admin: nil, activation_digest: "$2a$04$Ct2iBtdpHwOb/THvd94.Xu2JzFu.Jedghn2xC8pri9U...", activated: true, activated_at: "2022-03-26 23:06:12", reset_digest: nil, reset_sent_at: nil>
2
#<User id: 2, name: "Example User 2", email: "example-2@gmail.com", created_at: "2022-03-26 23:06:12", updated_at: "2022-03-26 23:06:12", password_digest: [FILTERED], remember_digest: nil, admin: nil, activation_digest: "$2a$04$F9nRxyV6hus7ReCquet4m.KquGhE8dRP0tyPzVO0WLC...", activated: true, activated_at: "2022-03-26 23:06:12", reset_digest: nil, reset_sent_at: nil>
```

問題無さそうです。

### 14.4

`relationship`のバリデーションに対するテストを書きます。

```ruby:spec/models/relationship_spec.rb
require 'rails_helper'

RSpec.describe Relationship, type: :model do
  describe "validation" do
    let(:relationship) { FactoryBot.create(:relationship) }

    context "with valid attributes" do
      # 後で書く
    end

    context "with invalid attributes" do
      it "is invalid without a follower_id" do
        relationship.follower_id = nil
        expect(relationship).to_not be_valid
      end

      it "is invalid without a followed_id" do
        relationship.followed_id = nil
        expect(relationship).to_not be_valid
      end
    end
  end

end
```

### 14.9

`following`関連のメソッドをテストします。

```ruby:spec/models/user_spec.rb
  describe "#follow and #unfollow" do
    let(:other_user) { FactoryBot.build(:user) }

    it "can follow the other user" do
      expect(user.following?(other_user)).to_not be_truthy
      user.follow(other_user)
      expect(user.following?(other_user)).to be_truthy
    end

    it "can unfollow the other user" do
      user.follow(other_user)
      expect(user.following?(other_user)).to be_truthy
      user.unfollow(other_user)
      expect(user.following?(other_user)).to_not be_truthy
    end
  end
```

### 14.13

`followers`が正しく機能することをテストします。

```ruby:spec/models/user_spec.rb
  describe "#follow and #unfollow" do
    let(:user) { FactoryBot.create(:user) }
    let(:other_user) { FactoryBot.create(:user) }

    it "can follow the other user" do
      expect(user.following?(other_user)).to_not be_truthy

      user.follow(other_user)

      expect(user.following?(other_user)).to be_truthy
      expect(other_user.followers.include?(user)).to be_truthy
    end
```

### 14.2.2 演習

プロフィールページとHomeページに `following`と`followers`の統計情報が正しく表示されていることをテストします。

まずはファクトリでテストデータを用意します。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user , aliases: [:followed, :follower] do
    # 省略...
    trait :with_relationships do
      after(:create) do |user|
        30.times do
          other_user = create(:user)
          user.follow(other_user)
          other_user.follow(user)
        end
      end
    end
```

コールバックを使い、
他のユーザーを生成 → お互いにフォロー
という流れを繰り返しています。

`following`、`followers`のどちらかのみでも同じように実装出来ると思います。

プロフィールページのテストを書きます。
`"#{正しい数} following / followers"`という表示になっていることをテストします。

```ruby:spec/system/users_spec.rb
  describe "GET /users/id" do
    describe "following and followers" do
      let(:user_with_relationships) { FactoryBot.create(:user, :with_relationships) }
      let(:following) { user_with_relationships.following.count }
      let(:followers) { user_with_relationships.followers.count }

      it "displays statistics for following and followers" do
        log_in user_with_relationships
        expect(page).to have_content("#{following} following")
        expect(page).to have_content("#{followers} followers")
      end
    end
  end
```

ホームページのテストを書きます。使い回しです。

```ruby:spec/system/static_pages_spec.rb
  describe "GET /users/id" do
    describe "following and followers" do
      let(:user_with_relationships) { FactoryBot.create(:user, :with_relationships) }
      let(:following) { user_with_relationships.following.count }
      let(:followers) { user_with_relationships.followers.count }

      it "displays statistics for following and followers" do
        log_in user_with_relationships
        expect(page).to have_content("#{following} following")
        expect(page).to have_content("#{followers} followers")
      end
    end
  end
```

### 14.24

フォロー/フォロワーページの認可をテストします。

```ruby:spec/system/users_spec.rb
  describe "GET /users/id/following" do
    let(:user) { FactoryBot.create(:user) }

    context "as a logged in user" do
      # 後で書く
    end

    context "as a non-logged in user" do
      it "redirects to login_path" do
        get following_user_path(user)
        expect(response).to redirect_to login_path
      end
    end
  end

  describe "GET /users/id/followers" do
    let(:user) { FactoryBot.create(:user) }

    context "as a logged in user" do
      # 後で書く
    end

    context "as a non-logged in user" do
      it "redirects to login_path" do
        get followers_user_path(user)
        expect(response).to redirect_to login_path
      end
    end
  end
```

### 14.29

`following`/`follower`ページ(フォローしているユーザー/フォロワーの一覧ページ)に対するテストを書きます。

網羅的に書くのは難しいので、正しい数が表示されていること、正しいリンクが表示されていることのみテストします。

`before`で`@following`/`@followers`を変数に入れておくとテストが読みやすくなると思ったので、そのようにしました。
また、`@following`/`@followers`が空の場合、後のテストが実行されず通ってしまうので、空でないことを確認しています。

```ruby:spec/system/users.rb
  describe "GET /users/id/following" do
    let(:user) { FactoryBot.create(:user) }

    context "as a logged in user" do
      before do
        @user_with_relationships = FactoryBot.create(:user, :with_relationships)
        @following = @user_with_relationships.following
        log_in @user_with_relationships
      end

      it "displays the correct number of following user" do
        visit following_user_path(@user_with_relationships)

        # ここが空の場合後のテストが実行されないため
        expect(@following).to_not be_empty

        expect(page).to have_content("#{@following.count} following")
        @following.paginate(page: 1).each do |follow|
          expect(page).to have_link follow.name, href: user_path(follow)
        end
      end
    end

    # 省略...

  describe "GET /users/id/followers" do
    let(:user) { FactoryBot.create(:user) }

    context "as a logged in user" do
      before do
        @user_with_relationships = FactoryBot.create(:user, :with_relationships)
        @followers = @user_with_relationships.followers
        log_in @user_with_relationships
      end

      it "displays the correct number of followers" do
        visit followers_user_path(@user_with_relationships)

        # ここが空の場合後のテストが実行されないため
        expect(@followers).to_not be_empty

        expect(page).to have_content("#{@followers.count} followers")
        @followers.paginate(page: 1).each do |follower|
          expect(page).to have_link follower.name, href: user_path(follower)
        end
      end
    end
```

### 14.31

リレーションシップのアクセス制御に対するテストを書きます。

```ruby:spec/requests/relationships_spec.rb
RSpec.describe "Relationships", type: :request do
  describe "#create" do
    context "as a logged in user" do
      # 後で
    end
    context "as a non-logged in user" do
      it "redirects to login_path" do
        post relationships_path
        expect(response).to redirect_to login_path
      end

      it "doesn't create a relationship" do
        expect{
          post relationships_path
        }.to_not change(Relationship, :count)
      end
    end
  end

  describe "#destroy" do
    let!(:relationship) { FactoryBot.create(:relationship) }
    context "as a logged in user" do
      # 後で
    end
    context "as a non-logged in user" do
      it "redirects to login_path" do
        delete relationship_path(relationship)
        expect(response).to redirect_to login_path
      end

      it "doesn't delete a relationship" do
        expect{
          delete relationship_path(relationship)
        }.to_not change(Relationship, :count)
      end
    end
  end
end
```

### 14.40

Follow/Unfollowのテストを書きます。
`post`/`delete`メソッドの引数として`xhr: true`を渡すことで、Ajaxでリクエストを発行するようにします。

```ruby:spec/requests/relationships_spec.rb
RSpec.describe "Relationships", type: :request do
  describe "#create" do
    context "as a logged in user" do
      before do
        @user = FactoryBot.create(:user)
        @other_user = FactoryBot.create(:user)
        log_in @user
      end

      it "creates a relationship by the standard way" do
        expect{
          post relationships_path, params: { followed_id: @other_user.id }
        }.to change(Relationship, :count).by 1
      end

      it "creates a relationship by the Ajax" do
        expect{
          post relationships_path, params: { followed_id: @other_user.id }, xhr: true
        }.to change(Relationship, :count).by 1
      end
    end
    # 省略...

  describe "#destroy" do
    context "as a logged in user" do
      before do
        @user = FactoryBot.create(:user)
        @other_user = FactoryBot.create(:user)
        log_in @user
      end

      it "deletes a relationship by the standard way" do
        @user.follow(@other_user)
        created_relationship = @user.active_relationships.find_by(followed_id: @other_user.id)
        expect{
          delete relationship_path(created_relationship)
        }.to change(Relationship, :count).by -1
      end

      it "deletes a relationship by the Ajax" do
        @user.follow(@other_user)
        created_relationship = @user.active_relationships.find_by(followed_id: @other_user.id)
        expect{
          delete relationship_path(created_relationship), xhr: true
        }.to change(Relationship, :count).by -1
      end
    end
```

### 14.42

ステータスフィードのテストを実装します。

自身/フォローしているユーザーの投稿が表示されていること、フォローしていないユーザーの投稿が表示されないことをテストします。

```ruby:spec/models_user_spec.rb
  describe "#feed" do
    let(:user) { FactoryBot.create(:user, :with_posts) }
    let(:user_following) { FactoryBot.create(:user, :with_posts) }
    let(:user_unfollowed) { FactoryBot.create(:user, :with_posts) }
    before do
      user.follow(user_following)
    end

    it "displays user's own posts" do
      user.microposts.each do |post_self|
        expect(user.feed).to be_include(post_self)
      end
    end

    it "displays following user's posts" do
      user_following.microposts.each do |post_following|
        expect(user.feed).to be_include(post_following)
      end
    end

    it "doesn't display unfollowed user's posts" do
      user_unfollowed.microposts.each do |post_unfollowed|
        expect(user.feed).to_not be_include(post_unfollowed)
      end
    end
  end
```

フィードをテストするためには、投稿を持つユーザーを作成する必要があります。
そこで、マイクロポストの表示テストの際に使用した `with_posts`トレイトを再利用しました。

```ruby:spec/factories/users.rb
FactoryBot.define do
  factory :user , aliases: [:followed, :follower] do
  # 省略...
    trait :with_posts do
      after(:create) { |user| create_list(:micropost, 31, user: user) }
    end
  end
end
```

### 14.49

フィードのHTMLをテストします。

```ruby:spec/system/static_pages_spec.rb
RSpec.describe "StaticPages", type: :system do
  describe "root" do
    describe "feed" do
      let(:user) { FactoryBot.create(:user, :with_posts) }
      before do
        log_in user
      end

      it "displays correct feeds" do
        visit root_path
        user.feed.paginate(page: 1).each do |micropost|
          expect(page).to have_content(CGI.escapeHTML(micropost.content))
        end
      end
    end
```

## 答え合わせ

[コード例〜第14章〜｜RailsチュートリアルのテストをRSpecで書き換える](https://zenn.dev/fu_ga/books/ff025eaf9eb387/viewer/18ab0c)

フォロー/フォロワーや、投稿を持つユーザーを用意するファクトリの中身がかなり異なっていました。
個人的にはコールバックで用意してしまう方が好みです。


# リファクタリング

## トレイトによるファクトリの重複解消(13章時点)

下のコードがリファクタリング前の状態です。

必要になる度にとにかく足していったせいで、重複がとても多いです。
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

ちなみにtraitは「特徴・特性」などの意味を持ちます。
「ある特徴・特性を持ったデータ」だからトレイトなんですね。

## スペックの切り出し

フォロー関連のUIテストが`static_pages`にあるのはおかしいかと思い、別のスペックを作成、切り出しました。

```ruby:spec/system/following_spec.rb
require "rails_helper"

RSpec.describe "StaticPages", type: :system do
  before do
    driven_by(:rack_test)
  end

  describe "/root" do
    describe "following and followers" do
      let(:user_with_relationships) { FactoryBot.create(:user, :with_relationships) }
      let(:following) { user_with_relationships.following.count }
      let(:followers) { user_with_relationships.followers.count }

      it "displays statistics for following and followers" do
        log_in user_with_relationships
        expect(page).to have_content("#{following} following")
        expect(page).to have_content("#{followers} followers")
      end
    end

    describe "feed" do
      let(:user) { FactoryBot.create(:user, :with_posts) }
      before do
        log_in user
      end

      it "displays correct feeds" do
        visit root_path
        user.feed.paginate(page: 1).each do |micropost|
          expect(page).to have_content(CGI.escapeHTML(micropost.content))
        end
      end
    end
  end
end
```

## RuboCopの導入

本筋からは逸れますが、いつかやろうと思っていたrubocopの導入もしてみます。

### rubocopとは

Rubyの静的コード解析をしてくれるgem。
これを活用することで、チームのコーディング規約に準拠した開発が可能になる。

### 導入

`Gemfile` に記述、 `bundle install` 実行。

```ruby
group :development do
  gem 'rubocop'
	gem 'rubocop-rails' # rails用
	gem 'rubocop-rspec' # rspec用
	gem 'pre-commit'    # コミット自動実行
end
```

### 基本コマンド

```bash
# 解析を走らせる
$ rubocop
# .rubocop_todo.ymlに警告を退避
$ rubocop --auto-gen-config
# 自動修正
$ rubocop -a
```

### VSCodeと連携する

`settings.json` に以下を追記（Rubyのインストールが必要）

```bash
// rubocop
"ruby.useLanguageServer": true,
"ruby.lint": {
    "rubocop": true
},
"ruby.format": "rubocop"
```

### コミット時に自動で走らせる

`pre-commit` gemを `bundle install` 後、次のコマンドを実行。

```bash
bundle exec pre-commit install
git config pre-commit.checks rubocop # この変更はプロジェクト内にしか影響しない
bundle exec pre-commit list
```

- `pre-commit install` では、 `.git/hooks/pre-commit` というファイルが作成される。
- `git config pre-commit.checks robocop` によりコミット時に実行されるようになる。
- `pre-commit list` によりコミット前に実行されるアクションを確認出来る。

なお、設定を解除したい場合は `.git/hooks/pre-commit` ファイルを削除する。

### 設定周り

ルールが適用されるのは設定用ファイルよりも下の階層。基本ルートに置く。

#### `.rubocop.yml`

- 設定ファイル。
- チームのコーディングスタイルに合ったルールをこのファイルで適用する。

#### `.rubodop_todo.yml`

あまりに警告が多い時に `rubocop --auto-gen-config` を実行することによって自動生成される。
警告内容を全てこのファイル内に移動させることが出来る。それ以降、このファイルに移動した警告は無視される。

### RuboCopを活用した修正の流れ

> ⓪　**`$ rubocop --auto-correct`** を実行して、自動で修正できるものはしてもらう。残りの警告がたくさんある場合> は①へ。警告がそんなに多くない場合(10~20個とか)は③と④を繰り返す。(Railsのコード規則を学ぶのにとても良い教材だと思> うので初めは⓪を飛ばすことをお勧めします。)
> 
> ①　警告がたくさんあると見ずらいので **`$ rubocop --auto-gen-config`**を実行して `.rubocop_todo.yml`を作> 成、そこに全ての警告をいったん移す。(こうすることで **`$ rubocop`**を実行しても今の段階では全ての警告は無視され> ます。)
> 
> ②　`.rubocop_todo.yml` 内の警告の中から一番上の警告をコメントアウトする。(コメントアウトした警告だけが再び> RuboCopに感知されるようになる)
> 
> ③　**`$ rubocop`** を実行して警告を修正する。
> 
> ④　警告のデフォルトを変更したり、特定のファイルを今後RuboCopに警告されないたくないという場合は, `.rubocop.yml`> に設定を書く。
> 
> ⑤　修正し終わったら `.rubocop_todo.yml` に戻り、コメントアウトした警告を削除する。
> 
> ⑥　`.rubocop_todo.yml` 内の全ての警告を修正し終わるまで②~⑤を繰り返す。
> 
> ⑦　テストがある場合はテストを走らせる。
> 
> 参考 : [RuboCop is 何？ - Qiita](https://qiita.com/tomohiii/items/1a17018b5a48b8284a8b)

### 警告例

### [Layout::ArgumentAlignment](https://www.rubydoc.info/gems/rubocop/RuboCop/Cop/Layout/ArgumentAlignment)

複数行に渡るメソッド定義は先頭が揃えてあること。

```ruby
# godd
validates :image,
            content_type: {
              in: %w[image/jpeg image/gif image/png],
              message: "must be a valid image format"
            }

# bad
validates :image,
    content_type: {
      in: %w[image/jpeg image/gif image/png],
      message: "must be a valid image format"
    }
```

### [RuboCop | Style/GuardClause - Qiita](https://qiita.com/tbpgr/items/69c3830586fbe555b374)

メソッド内における`if/unless` 内の処理が1行以上の場合、 `return if hoge` を使うようにすること。

✅ 「処理が4行以上の場合」に変更した。

```ruby
# bad
def test
  if something
    a = 1
    print a
    work
  end
end

# good
def test
  return unless something
  a = 1
  print a
  work
end
```

### Layout/TrailingEmptyLines

ファイルの最後には空行があること。

### Style/MultilineTernaryOperator

- Style/MultilineTernaryOperator: Avoid multi-line ternary operators, use if or unless instead.
    - `condition ? something : else` は複数行で使わない

### Style/RedundantReturn

- Style/RedundantReturn: Redundant return detected.
    - 無駄な `return` 。明示的にあったほうがわかりやすいと思うなら設定外す。

```ruby
# bad
def self.digest(string)
  cost = ActiveModel::SecurePassword.min_cost ? BCrypt::Engine::MIN_COST :
                                                BCrypt::Engine.cost
  BCrypt::Password.create(string, cost: cost)
end

# good
def self.digest(string)
  if ActiveModel::SecurePassword.min_cost
    BCrypt::Password.create(string, cost: BCrypt::Engine::MIN_COST)
  else
    BCrypt::Password.create(string, cost: BCrypt::Engine.cost)
  end
end
```

### [Lint::AmbiguousOperator](https://www.rubydoc.info/gems/rubocop/RuboCop/Cop/Lint/AmbiguousOperator)

メソッドの引数として渡される、曖昧なオペレーターの呼び出しを検知する。

```ruby
# bad
expect {
    user.destroy
	}.to change(Micropost, :count).by -1

# good
expect {
    user.destroy
	}.to change(Micropost, :count).by(-1)
```

# RSpec

### RSpec/ExampleLength

1exampleの行数。デフォルトだと厳しすぎる。

```ruby
# 1exampleの行数
# デフォルトだと厳しすぎる
RSpec/ExampleLength:
  Max: 8
```

### Metrics/BlockLength

1ブロックあたりの行数。専用のDSLで記述する関係上、デフォルトは現実的ではない。

ので、RSpecのみ除外する。

```ruby
# RSpecのみ1ブロックあたりの行数超過を許可
Metrics/BlockLength:
  Exclude:
    - 'spec/**/*'
```

### RSpec/DescribedClass

`described_class` は `describe` で指定したクラスを指す。

クラスをそのまま指定するよりも明示的でわかりやすい。

```ruby
# bad
RSpec.describe User do
  subject {User.new}
end

# good
RSpec.describe User do
  subject {described_class.new}
end
```

### 感想

Railsチュートリアル+RSpec書き換え終了時点で走らせたら警告多すぎてびっくりしました。

「厳しすぎやろ！」と思うものから「なるほどな〜」となるものまで、様々でした。
自分/チームが気持ちよく開発出来るような`.rubocop.yml`を作り上げていきたいです。

### 参考記事

- [RuboCop is 何？ - Qiita](https://qiita.com/tomohiii/items/1a17018b5a48b8284a8b)
- [RuboCopの設定アレコレ - Qiita](https://qiita.com/necojackarc/items/8bc16092bbc69f17a16d)
- [RuboCop設定参考](https://qiita.com/piggydev/items/8a9f5cd4486861819a69#rubocopyml-%E8%A8%AD%E5%AE%9A%E4%BE%8B)
- [VSCodeでRubocopを使う - Qiita](https://qiita.com/d0ne1s/items/a3566aca023d11f2bfc4)
- [styleguide/ruby.ja.md at master · cookpad/styleguide](https://github.com/cookpad/styleguide/blob/master/ruby.ja.md)

## その他

- シンプルなミスの修正
- exampleを具体的に
  - テストの出力を見ただけでは中身がよくわからない箇所を改善しました。
- exampleに一貫性を持たせる
  - 例えば、「ログインしていない」状態のテストはあっても「ログインしている」状態のテストが無いため追加、など。
- 英語の修正
  - 「non-logged in user」は「anonymous user」と呼んだ方が適切([参考](https://www.quora.com/Whats-an-appropriate-word-for-a-non-logged-in-user))なようなので、修正しました。
  - 「gest user」でも良かった？
- 使用するメソッドに一貫性を持たせる
  - 謎に`_path`/`_url`が混在していたので基本`_path`(相対パス)で統一しました。

## 使えていない便利そうな機能達

- `subject`
  - テスト対象のオブジェクトを宣言、再利用出来るように。
- `shared_example`
  - exampleの宣言、再利用。
- `shared_context`
  - `context`の宣言、再利用。
- モックとスタブ
  - モックはDBへアクセスするような処理を減らすために使う。
  - スタブはオブジェクトのメソッドをオーバーライドし、テスト用の結果を返すダミーメソッド。DBやネットワークを使う処理が対象。
  - テストの速度改善や、再現の難しいデータのテストなどに利用すると良いらしい。
- タグ
  - 特定のテストだけ実行/スキップ。
  - 新機能を追加する時、既存のコードのテストをスキップしたい時など。
- shoulda-matchersの利用
  - EverydayRailsで推されている便利マッチャ。

# まとめ

正直、RSpecに書き換えるだけでここまで大変だとは思っていませんでした。

- RSpecとMinitestの構文や使い方の違い
- 各Specの役割
- どのように検証すれば良いのか
  - テストしたい項目はわかっても、どうテストコードに落とし込めば良いのかわからない
- `describe` `context` の粒度
- exampleの名前
  - なかなか一貫性を保てない
- テスト用データの用意

などなど。
挙げるとキリがありませんが、かなり苦戦しました。

ですが、自分なりに試行錯誤しながらそれなりの規模のアプリケーションに対してテストを書いたことで、RSpecに対する理解はもちろん、ソフトウェアテストの片鱗くらいは理解出来た気がします。

RSpecの基礎学習から書き換え時の参照先として、[Everyday Rails](https://leanpub.com/everydayrailsrspec-jp)には非常に助けられました。
RSpecの基礎だけでなく、テストの考え方・原則まで幅広く学ぶことが出来ます。
非常におすすめの教材です。これからRSpecを学ぶ方はぜひ。

また、全体を通して回答例として利用させていただいた記事([RailsチュートリアルのテストをRSpecで書き換える](https://zenn.dev/fu_ga/books/ff025eaf9eb387))も非常に参考になりました。

## 参考記事

答え合わせ用に使用
[RailsチュートリアルのテストをRSpecで書き換える](https://zenn.dev/fu_ga/books/ff025eaf9eb387)

RSpecのREADME.md
[https://github.com/rspec/rspec-rails](https://github.com/rspec/rspec-rails)

システムスペック/フィーチャスペック/リクエストスペックの違い
[System specs, feature specs, request specs–what’s the difference?](https://github.com/rspec/rspec-rails#system-specs-feature-specs-request-specswhats-the-difference)

CapybaraのREADME.md
[capybara/README.md at master · teamcapybara/capybara](https://github.com/teamcapybara/capybara/blob/master/README.md)

使えるRSpec入門
「Everyday Rails」の翻訳者である@jnchitoさんの書いた記事です。
- [使えるRSpec入門・その1「RSpecの基本的な構文や便利な機能を理解する」 - Qiita](https://qiita.com/jnchito/items/42193d066bd61c740612)
- [使えるRSpec入門・その2「使用頻度の高いマッチャを使いこなす」 - Qiita](https://qiita.com/jnchito/items/2e79a1abe7cd8214caa5)
    - 一通り目を通したい。
- [使えるRSpec入門・その3「ゼロからわかるモック（mock）を使ったテストの書き方」 - Qiita](https://qiita.com/jnchito/items/640f17e124ab263a54dd)
    - モックをあまり理解出来ていないのでそのうち読む。
- [使えるRSpec入門・その4「どんなブラウザ操作も自由自在！逆引きCapybara大辞典」 - Qiita](https://qiita.com/jnchito/items/607f956263c38a5fec24)
    - 逆引き的に使う。