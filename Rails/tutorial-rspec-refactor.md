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