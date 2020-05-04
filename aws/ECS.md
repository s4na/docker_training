# ECS: 

コンテナオーケストレーション

- 類似のコンテナオーケストレーションサービス
  - Docker Swarm
  - Kubernetes
  - AWS EKS
    - AWSでKubernetes使えるサービス

- ECS
  - ロードバランサーとオートスケーリングが組み合わさったサービス
  - このサービスを動かすためのEC2インスタンスも自動で追加/削除される
  - AWSでマイクロサービスを展開するにはまず選択肢になる代表的なサービス

- ECSを構成するもの
  - ECSクラスター
    - 複数のECSインスタンスで構成される
  - Task definition

- ECR
  - プライベート版のAWS提供のDocker Hubみたいなもの
  - Docker Registry

# プライベートリポジトリECR

```
AWSでECRリポジトリ作成

EC2にログイン
docker image ls

IAMでロールの作成
EC2選択

付与する権限
Amazon ECS FullAccess
Amazon EC2 ContainerFullaccess

ecsrole

roleをes2に付与する

aws ecr get-login --no-include-email --region us-east-1
# 文字がたくさん出る

# コピペするとログインできる

# ECRにログインできた

ECRからリポジトリを選択
Push commandの表示
指示通りに作業するとpushできる

ECRにアップロードされてることが確認できる

```

ECRからpullする

```
aws ecr describe-repositories --region us-east-1
aws ecr describe-images --repository-name <Repository name> --region us-east-1

docker pull <repository URI>:latest
docker image ls

```

## タスク定義

ECS全体像

クラスターテンプレート
EC2 + ネットワーキング


EC2の管理をAWSに任せるのがFargate
- ECSサービスの使い方
  - EC2タイプ
  - Fargate

## クラスター

クラスターの作成
EC2 Linux + Netrowking

オンデマンドインスタンス

- ecsInstanceRole
  - コンテナインスタンスとして動くために必要な権限

インスタンスはクラウドフォーメーションで作成してくれる

## タスク定義
ECSで辛いところ
パラメーターが膨大

ECSではコンテナがタスク定義通りに起動する
基本的に一つのコンテナにつき、一つのタスク定義が良い

- タスク定義名
  - リビジョン番号
- タスクロール
  - AWSにアクセスする権限
- ネットワークモード
  - Hostネットワークモード
    - コンテナ、ホスト両方が同じポートで待ち受ける
  - bridgeネットワークモード
    - EXPOSE 80
    - -p 80:80
    - 同じホストのポート番号でタスクを定義することができない
  - awsvcpネットワークモード

## タスク配置戦略
タスク配置戦略とは、タスク定義で定めたタスクをどう配置するかということ。
デフォルトだと良い感じに並べてくれる。
知らなくても使える。

- 配置3つのフィルだ
  - cluster constraints
    - 必要なCPU, Memory, Portが開いているか判断
  - placement constraints
    - 特定の条件を満たすEC2のみ配置するようにフィルタリングできる
  - placement strategies
    - 配置する優先順位
      - Binpack
        - 可能な限り一つのインスタンスに配置する
      - Spread
        - 指定された条件でバランスよく配置
      - Random

- Service
  - タスクを配置して管理する機能
  - サービスとタスク定義は1対1
    - サービスでタスクの起動数などを定める

- Load Balancer
  - 種類
    - Elastic Load Balancing
      - Application Load Balancer
      - Network Load Balancer
      - Classic Load Balancer
  - ECSと関連づけしたLoad Balancerはサービスに関連づけたEC2インスタンス全てに対して、バランシングする
  - ホストポートを0にすると、エフェメラルポートが割り当てられる
  - セキュリティグループをアタッチする
  - EC2のセキュリティグループ許可設定で、Load Balancerがアタッチしているセキュリティグループからの通信を許可しておく

- コンテナをアップデートする方法
- ECS Deployment type
  - https://docs.aws.amazon.com/ja_jp/AmazonECS/latest/developerguide/deployment-types.html

  - Rolling Update
    - コンテナを作成して、ECSにpush
    - タスク定義のコンテナURIを指定する場所でバージョンを更新
  - Blue/Green Deployment
    - > このデプロイタイプでは、本番稼働用トラフィックを送信する前にサービスの新しいデプロイメントを検証することができます。詳細については、AWS CodeDeploy User Guideの「CodeDeploy とは」を参照してください。
      - https://docs.aws.amazon.com/ja_jp/AmazonECS/latest/developerguide/deployment-type-bluegreen.html

- Auto Scaling
  - クラウドウォッチアラーム、スケーリングポリシーを利用して、EC2を増減するサービス

- Auto Scaling Group
  - ECSではタスク個別にAuto Scalingする機能がある
  - Reservetion
    - クラスター全体に対して、リソースが予約されているかでAuto Scalingする

サービス機能

- ロードバランサーがコンテナに通信できない理由
  - ECSインスタンスにアタッチされているセキュリティグループの問題
  - セキュリティグループの許可を忘れると、コンテナ大量虐殺になる
