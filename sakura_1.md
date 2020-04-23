Docker入門（第一回）～Dockerとは何か、何が良いのか～
https://knowledge.sakura.ad.jp/13265/



Nginxのコンテナを動かす
```
docker run --name some-nginx -d -p 8080:80 nginx
```

WordPressのコンテナを動かす
```
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:5.7
docker run --name some-wordpress -e WORDPRESS_DB_PASSWORD=my-secret-pw --link some-mysql:mysql -d -p 8080:80 wordpress
```

