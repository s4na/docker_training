Docker入門 #1 【Dockerとは】
https://qiita.com/wMETAw/items/b9bc643ded4b92bf6add

```s
docker info
docker --version
docker-compose --version

# webserver」という名前でコンテナを立て、nginxのイメージを公式からpullしています
# 公式からイメージのPullも同時に行なっている
docker run -d -p 8080:80 --name webserver nginx

# コンテナ一覧
docker ps
docker kill <Container ID>
docker rm <Container ID>
```
