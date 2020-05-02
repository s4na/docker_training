# EC2: Elastic Compute Cloud
仮想サーバー
OC, CPU, Memory, SSD, NIC
AMI, インスタンスタイプ, EBS, ENI

## AMI
Amazon Machine Image
EC2インスタンスが起動するときに必要となる設定ファイル

- Template
  - どのインスタンスを利用するか
- 起動許可
- Block Device Mapping
  - どのEBSモデルを使用するか

AMIコピーできる
EC2から作ることもできる

- Amazon Linux
  - aws cli, boto3, yum repositoryの設定など、AWSで使うのに最適化されている

### JeOS
Just enough Operating System
AMIの範囲はOSの必要最低限部分に留めようといった考え方

### Hybrid AMI

## AMI Design
https://docs.aws.amazon.com/marketplace/latest/userguide/best-practices-for-building-your-amis.html

## インスタンスタイプ
メモリなどのスペック構成パターン
https://www.bit-drive.ne.jp/managed-cloud/column/column_22.html

### 例
t2.micro
t = テスト向き
2世代 = インスタンスファミリー
micro = インスタンスサイズ

## EBS
EC2のディスクストレージ

大きく分けて2タイプSSD, HSS

IOPS = 1秒あたりにどの程度のデータを読み書きできるかの性能

### スナップショット
EBSのバックアップファイル
S3に保管
増分バックアップ方式

※差分バックアップとは違う

### AZサービスという観点で見ると
AZをまたいだコピーは通常できない
S3をまたいだコピーになる

## 結論
EC2はAMI, EBSのスナップショットを合わせたもの

## キーペア
EC2インスタンスへのログインする鍵
秘密鍵、公開鍵のペア

秘密鍵 = .pem形式のファイル。ダウンロードして使用

## インスタンスメタデータ
EC2インスタンスに埋め込まれている自分の情報

ec2-metadata

## ユーザーデータ
インスタンス起動時に一回だけ実行するスクリプト
- 再起動のタイミングではない
- rootユーザーで実行される
- インタラクティブではない
  - x: yum update
  - o: yum update -y
  - -y = 問い合わせ全てにyと答える

Cloud-init形式でも書ける

## プレイスメントグループ
- 複数のEC2を論理的にグルーピングすること
- AWS、基本的にクラスター処理には向いていない。この欠点を回避できる。
- AZをまたぐことはできない

### 種類
- クラスター
  - スタンダード
  - ハイパフォーマンスコンピューティングに向いている
  - 拡張ネットワークサービスをおすすめ
    - 例えば
      - ENA: Elastic Network Interface
        - ネットワーク速度を上げられる
  - 同じAMIで使うことが推奨
    - 20%程度早くなる
      - https://dev.classmethod.jp/articles/ec2-placement-group/
- パーティション
  - 複数のラックでグルーピングすること
  - 一つのラックに障害が起きても、全滅しない
- スプレッド
  - EC2を独立したラックに配置する
  - 1つのAZにつきEC2を7つまで、1つのリージョンにつきAZを3つまで

## Dedicatedホスト/Dedicatedインスタンス

AWSの物理サーバーのリソースを占有できること

- 違い
  - Dedicatedホストのみ、ライセンスの持ち込みができる
