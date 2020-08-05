# フリマ DB設計
## usersテーブル
|Column|Type|Options|
|------|----|-------|
|email|string|null: false|
|password|string|null: false|
|name|string|null: false|
### Association
- has_many :sells
- has_many :buys   

## sellsテーブル(出品)
|Column|Type|Options|
|------|----|-------|
|title|text|null: false| 
|price|integer|null: false| 
|image|string|null: false|
|text|text|null: false| 
|user_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :user
- has_many :buys
- has_many :sells_categories
- has_many :categories,  through:  :sells_categories

## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|text|text|null: false|
### Association
- has_many :sells_categories
- has_many :sells,  through:  :sells_categories

## sells_categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|sell_id|integer|null: false, foreign_key: true|
|category_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :sell
- belongs_to :category 
- belongs_to :buy

## buysテーブル(購入)
|Column|Type|Options|
|------|----|-------|
|text|text|null: false| 
|price|integer 
|user_id|integer|null: false, foreign_key: true|
|sell_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :sell 
- belongs_to :user  
- has_many :sells_categories
- has_many  :categories,  through:  :sells_categories