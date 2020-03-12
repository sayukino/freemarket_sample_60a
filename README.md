# DB設計

## usersテーブル
|Column|Type|Options|
|---------|------|---------|
|nickname|string|null: false| 
|email|string|null: false, unique: true|
|password|string|null: false|
|first_name|string|null: false|
|last_name|string|null: false|
|first_name_kana|string|null;false|
|last_name_kana|string|null: false|
|birth_year|integer|null: false|
|birth_month|integer|null: false|
|birth_day|integer|null: false|
|introduction|text||
|avatar|string||
### Association
- has_one :card,dependent: :destroy
- has_one :buyer,dependent: :destroy
- has_one :comment,dependent: :destroy
- has_many :likes,dependent: :destroy
- has_one :phone,dependent: :destroy
- has_one :address,dependent: :destroy


## Addressテーブル
|Column|Type|Options|
|---------|------|---------|
|postal_code|integer|null: false|
|prefectures|string|null: false|
|city|string|null: false|
|address|string|null: false|
|building|string||
|phone_number|string||
|user_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :user

## sns_credentialsテーブル
|---------|------|---------|
|provider|string||
|uid|string||
|user_id|integer||
### Association
- belongs_to :user

## itemsテーブル
|Column|Type|Options|
|------|----|-------|
|created_at|integer|null: false|
|updated_at|integer|null: false|
|name|string|null: false|
|description|string|null: false|
|condition|string|null: false|
|cover_postage|string|null: false|
|shipping_area|integer|null: false|
|shipping_date|string|null: false|
|price|integer|null: false|
|margin|integer|null: false|
|profit|integer|null: false|
|prefectures|string|null: false|
|category_id|integer|foreign_key: true|
|item_id|integer|null: false, primary_key: true, index: true|
|buyer_id|integer|foreign_key: true|
|seller_id|integer|null: false, foreign_key: true|
|brand_id|integer|null: false, foreign_key: true, index: true|

### Association
- has_many :buyer
- has_one :category
- has_one :brand
- has_many :comments
- has_many: likes,dependent: :destroy
- has_many :images,dependent: :destroy

## imagesテーブル
|Column|Type|Options|
|------|----|-------|
|image|text|null: false|
|item_id|integer|null: false,foreign_key: true|

### Association
- belongs_to: item

## brandsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
### Association
- has_many :items
- has_many :groups, through: :brand_groups

## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|ancestry|string|
### Association
- has_meny :items
- has_ancestry

## cardsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false|
|customer_id|string|null: false|
|card_id|string|null: false|
### Association
- belongs_to :user
- belongs_to :customer
- belongs_to :card