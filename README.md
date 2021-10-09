# README

# 概要
売り手と買い手を仲介する、フリーマーケットアプリケーション
 
## 開発環境
Ruby/Ruby on Rails/MySQL/Github/AWS/Visual Studio Code
    
    
# データベース設計
## usersテーブル
-----
| Column             | Type     | Options     |
| ------------------ | ------   | ----------- |
| nickname           | string   | null: false |
| email              | string   | null: false, unique: true |
| encrypted_password | string   | null: false |
| first_name_kanji   | string   | null: false |
| last_name_kanji    | string   | null: false |
| first_name_kana    | string   | null: false |
| last_name_kana     | string   | null: false |
| birth_date         | date     | null: false | 

### Association
- has_many :items
- has_many :orders
- hsd_many :comments



## itemsテーブル
-----
| Column            | Type           | Options                         |
| ----------------- | -------------- | ------------------------------- |
| user              | references     | foreign_key: true  |
| title             | string         | null: false                     |
| detail            | text           | null: false                     |
| category       | integer        | null: false                  |
| quality       | integer        | null: false                  |
| shipping_fee  | integer        | null: false                   |
| prefecture         | integer    | null: false                   |
| shipment_date  | integer        | null: false                  |
| price             | integer        | null: false                     |



### Association
- belongs_to :user
- has_one :order
- belongs_to_active_hash :category
- belongs_to_active_hash :quality
- belongs_to_active_hash :shipping_fee
- belongs_to_active_hash :prefecture
- belongs_to_active_hash :shipment_date
- hsd_many :comments




## ordersテーブル （後日実装予定）
-----
| Column             | Type       | Options     |
| ------------------ | ---------  | ----------- |
| user               | references | foreign_key: true |
| item               | references | foreign_key: true |

### Association
- belongs_to :user
- belongs_to :item
- has_one :address, dependent :destroy

## addressesテーブル
-----
| Column            | Type           | Options                         |
| ----------------- | -------------- | ------------------------------- |
| postal_code        | string     | null: false |
| prefecture         | integer    | null: false                   |
| city_town          | string     | null: false |
| address_number     | string     | null: false |
| building           | string     |             |
| phone_number       | string     | null: false |


### Association
- belongs_to :order
- belongs_to_active_hash :prefecture


## comments テーブル （後日実装予定）
-----
| Column             | Type       | Options     |
| ------------------ | ---------  | ----------- |
| user               | references | foreign_key: true |
| item               | references | foreign_key: true |
| comment            | text       | ull: false |

### Association
- belongs_to :user
- belongs_to :item, dependent :destroy

​