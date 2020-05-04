# Docker

参考
https://www.youtube.com/watch?v=DS5HBTMG1RI


- Docker daemon
  - https://nickjanetakis.com/blog/understanding-how-the-docker-daemon-and-docker-cli-work-together

- Container lifecycle
  - https://medium.com/@BeNitinAgarwal/lifecycle-of-docker-container-d2da9f85959

- Docker daemon install 公式手順
  - https://docs.aws.amazon.com/ja_jp/AmazonECS/latest/developerguide/docker-basics.html

```
docker login
# ファイルの確認
ls -l
docker build -t dockerdemo ./
# 作成したイメージの確認
docker image ls

# -e
# -p 80を8080に
docker run --name dockerdemo -d -e name="kurokawa" -p 80:8080 dockerdemo:latest

# 実行中のコンテナの確認
docker container ls

# localhost/dockerdemo にアクセスで -> wellcome表示される
```

- Dockerに乗っているもの
  - OS
  - python runtime
  - Flask runtime
  - program
  - 実行コード

```
# Docker Hubでrepository 作成

docker image ls
docker tag <Image ID> <Docker Hub ID>/<Repository name>

# Repository作成確認
docker image ls
docker image push <Docker Hub ID>/<Repository name>

docker run -d -p 8080:80 dockerdemo:latest
```

docker image ps # lsの古いバージョンのコマンド

```
docker image build -t dockerdemo2 ./
docker container ls
docker container stop

# 実行されてないことを確認
docker container ls

# 名前を指定して実行
docker run --name dockerdemo -d -p 8080:80 dockerdemo:latest

# IPアドレス:8080でアクセスすると、Docker containerが表示される
```
