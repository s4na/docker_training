# Dockerfile

https://knowledge.sakura.ad.jp/15253/

```Dockerfile
FROM centos:7
RUN yum install -y java
ADD files/apache-tomcat-9.0.6.tar.gz /opt/
CMD [ "/opt/apache-tomcat-9.0.6/bin/catalina.sh", "run" ]
```

FROM ベースとなるDockerイメージの指定
RUN OSのコマンドを実行

CMD コンテナ起動時のコマンド

ADD ローカルでのtarアーカイブ展開（他にもリモートURLのサポートなどある）
COPY ローカルファイルをコンテナの中にコピーする


キャッシュ
