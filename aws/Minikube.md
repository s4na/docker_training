# Minikube

- Minikube
  - Master, Nodesを一つのサーバーでできるようにするもの
  - 練習用

- EC2
  - ubuntu
  - インスタンスタイプ
    - t3a.micro
  - Subnet
    - Internet接続ができるもの
      - ※ root tableにIGWの設定が必要
  - セキュリティグループ
    - 後から変更

- Minikubeをインストール
  - https://www.radishlogic.com/kubernetes/running-minikube-in-aws-ec2-ubuntu/

- 公式のサンプルコマンド
  - https://github.com/kubernetes/examples/blob/master/staging/simple-nginx.md

- deployment
- pod
  - 1つ上のコンテナのまとまり
  - IDアドレスはpod単位で付与される
  - コンテナ内はportで通信が行われる
    - 別コンテナで同じport番号は使えない
  - メリット
    - 例えばGit sync(local volumeとGitHubのcodeを連携させる)を入れることで、GitHubにPushするだけで簡単に設定変更が行える
    - バラバラな状態だと、Container同士の関連性や関係性がわかりにくい。ContainerがPod単位でまとまることで、関係性をPod単位で管理できるようになる

- pod design pattern
  - https://www.weave.works/blog/container-design-patterns-for-kubernetes/
  - sidecar container
    - 別のサービスと連携できるContainer

- Replica Set
  - Podを作成したり管理したりするもの
    - Containerが1つダウンしても、1つ復活させるなど
  - Deploymentによって作られる
    - 更新が必要になったら、新しいReplica Setを作り入れ替える
    - 問題があっても、Roll backができる
      - CI/CDの関係で、Roll backより、設定を前の状態に更新することが多い

- service
  - Internetにアクセスできるようになる
  - Load barancerの役割を果たしてくれる
  - EC2のPublic IP AddressでServiceのIPAddressにアクセスすることで、Containerと通信できる
    - ？？
  - EC2のセキュリティグループ設定をすること
