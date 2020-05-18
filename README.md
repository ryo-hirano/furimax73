# README

# アプリ名

- FashionBlog

# 概要

ファッション・グルメ・音楽など、自分のライフスタイルを投稿できます。

# 開発状況

- 開発環境
  開発言語：
    Ruby/Ruby on Rails
  開発ツール：
    Github/Visual Studio Code

- 開発期間

  開発期間：
    10日間(4/10 ~ 4/20)
  平均作業時間：
    1日10時間

# 制作背景

プログラミングに興味を持ち始めた頃から、ファッションを投稿できるSNSを作ってみたいと思っていました。
もっとファッションを好きになる、ファッションに興味を持つきっかけを提供したく思い開発しております。
機能自体は未実装の部分が多々ございますので、引き続きアップデートしていきます。

# このサービスでできること

images.githubusercontent.com/62536923/82183146-66beb980-9920-11ea-84ea-36ec0a9637b1.gif

images.githubusercontent.com/62536923/82183043-3aa33880-9920-11ea-85d7-cb6f7da8a275.gif

images.githubusercontent.com/62536923/82183053-3d059280-9920-11ea-9d5c-e3d98a9c1122.gif

## users_table

|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false, default: ""|
|email|string|null: false, unique: true, index: true, default: ""|
|encrypted_password|string|null: false, default: ""|
|reset_password_token|string||
|reset_password_sent_at|datetime||
|remember_created_at|datetime||
|user_image|string||
|introduction|text|
|family_name|string|null: false, default: ""|
|first_name|string|null: false, default: ""|
|family_name_kana|string|null: false, default: ""|
|first_name_kana|string|null: false, default: ""|
|birth_day|date|null: false|

### Association

- has_one :card
- has_one :destination
- has_many :products


## destination_table

|Column|Type|Options|
|------|----|-------|
|user|references|null: false, foreign_key: true, index: true|
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|post_code|string|null: false|
|prefecture|string|null: false|
|city|string|null: false|
|address|string|null: false|
|building_name|string||
|phone_number|string||

### Association

- belongs_to :user, optional: true


## card_table

|Column|Type|Options|
|------|----|-------|
|user|references|null: false, foreign_key: true, index: true|
|customer_id|string|null: false|
|card_id|string|null: false|

### Association

- belongs_to :user


## category_table

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|ancestry|string||

### Association

- has_many :products
- has_ancestry


## product_table

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|price|string|null: false|
|description|string|null: false|
|status_id|integer|null: false, foreign_key: true|
|size_id|integer|null: false, foreign_key: true|
|shipping_cost_id|integer|null: false, foreign_key: true|
|shipping_days_id|integer|null: false, foreign_key: true|
|prefecture_id|integer|null: false, foreign_key: true|
|category_id|integer|null: false, foreign_key: true|
|brand_id|integer|foreign_key: true|
|shipping_id|integer|null: false, foreign_key: true|
|user_id|integer|null: false, foreign_key: true|
|buyer_id|integer|foreign_key: true|

### Association

- belongs_to :user
- belongs_to :category
- has_many :images, dependent: :destroy
- belongs_to_active_hash :size
- belongs_to_active_hash :status
- belongs_to_active_hash :shippingcost
- belongs_to_active_hash :prefecture
- belongs_to_active_hash :shippingdays
- belongs_to_active_hash :shipping


## image_table

|Column|Type|Options|
|------|----|-------|
|src|string|null: false|
|product|references|null: false, foreign_key: true|

### Association

- belongs_to :product
