# IAM: Identity & Access Management

ルートユーザー
IAMユーザー

## IAMグループ

複数のユーザーに一度に権限を付与できる

## IAMユーザー

個人、アプリケーション

## IAMロール

AWSアカウント内で作成できる認証情報
短期的な認証情報
アクセスキーといった情報を持たない

- Trustポシリー
- Permissions

MFA: 多要素認証

## IAMポシリー

JSON形式のドキュメント
Principal(IAMユーザー、IAMポシリー)にアタッチする

### 流れ

Principal
-> Authentication
-> Request
- Actions/Operations
- Enviroment data
- Resources
- Request infomation
-> Authorization
-> Actions
-> Resources

## ポシリー

- Identify-based Policies
  - 管理ポシリー
    - AWS管理ポシリー
    - カスタマー管理ポシリー
  - インラインポリシー
    - 現在非推奨
  - Plincipalを記述しない
- Resource-based Policies
- Service Control Policies (SCPs)(組織 SCP)
  - [AWS Organizationsによるマルチアカウント戦略とその実装](https://engineer.crowdworks.jp/entry/2018/07/17/103453)
- IAM Permissions Boundaries (境界)
  - Principalに付与する
  - 権限の適用範囲を狭める
    - つまり、And条件のポシリー
  - Use cases
    - Userにポリシーの権限管理をさせたいとき
- Access Control Policies(ACLs)
  - 他のアカウントのPlincipalがどのリソースにアクセスできるかコントロールできる
  - 自身のアカウント内での制御はできない
  - JSONフォーマットではない
- Session Policies
  - IAMロールやフェデレーションしたUserの、一時的なセッションの認証情報を、パラメータとして渡すもの
    - ？？？

明示的なDeniedの方が強い

### JSON形式

- Statement
  - Principal
  - Action
  - Resource
  - Condition
    - 時間、IPアドレスなど

頭文字をとって、PARCモデルとも呼ばれる

## Principal

認証される主体

IAM User, Role
Federated User(Google, Facebook, Amazon)
Application

※Groupは正式にPrincipalとして認められていない

## クロスアカウントアクセス

IAMロールを利用して、自身のAWSアカウントと第三者の間に信頼関係を築くこと。
一時的な認証情報を付与される。
