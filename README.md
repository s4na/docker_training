# Docker練習

Docker
Docker Compose
Docker Hub

Docker
Dockerfile

docker-compose.yml

## docker command

run <image>
コンテナを起動状態で作成

-d detached バックグラウンド実行
--name コンテナ名
-p ホストとコンテナのポートフォワード設定
-v ボリュームマウント
-it 擬似TTY(pseudo-TTY)をコンテナの標準入力に接続する。コンテナ内でインタラクティブなbash shellを作成する。http://kz-engineer-scrap.hatenablog.com/entry/2016/03/03/040625

create <image> # コンテナを作成する

ps # コンテナを表示する
-a 停止中のコンテナも表示する

rm <Container name> # コンテナを終了
-f 強制的に終了

exec -it <Container name> bash
start <Container name> # コンテナを起動
stop <Container name> # コンテナを停止

commit <Container name> # コンテナからイメージを作成




## Proxy設定
Proxy配下でDockerを使用する場合は、設定が必要


## Docker間通信


## 参考

https://docs.docker.com/engine/reference/commandline/run/

http://docs.docker.jp/engine/reference/commandline/run.html

