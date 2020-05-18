# README

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
