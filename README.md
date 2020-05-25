# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

## usersテーブル
|Column  |Type   |Option|
|--------|-------|------|
|id      |integer|      |
|name    |string |null: false, unique: true|
|email   |string |null: false, unique: true|
|password|string |null: false|
|group_id|integer|null: false, foreign_key: true|
### Association
- has_many :messages
- has_many :groups, through: :groups_users

## groupsテーブル
|Column    |Type   |Options|
|----------|-------|-------|
|id        |integer|       |
|name      |string |null: false, unique: true|
|user_id   |integer|null: false, foreign_key: true|
|message_id|integer|null: false, foreign_key: true|
### Association
- has_many :users, through: :groups_users
- has_many :messages, through: :groups_messages

## messagesテーブル
|Column  |Type   |Options|
|--------|-------|-------|
|id      |integer|       |
|text    |text   |       |
|image   |text   |       |
|user_id |integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :user
- has_many :groups, through: :groups_messages

## groups_usersテーブル
|Column  |Type   |Options|
|--------|-------|-------|
|user_id |integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :group
- belongs_to :user

## groups_messagesテーブル
|Column    |Type   |Options|
|----------|-------|-------|
|message_id|integer|null: false, foreign_key: true|
|group_id  |integer|null: false, foreign_key: true|
### Association
- belongs_to :group
- belongs_to :message