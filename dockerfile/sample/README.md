```shell
# docker build -t <Dockerイメージ名> <Dockerfileが存在するディレクトリ>
docker build -t tomcat-1 .
docker images

docker run -it -d --name tomcat-1 -p 8081:8080 tomcat:1
docker logs -f tomcat-1

```
