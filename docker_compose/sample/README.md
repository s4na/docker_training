
```shell
> docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:5.7
> docker run --name some-wordpress -e WORDPRESS_DB_PASSWORD=my-secret-pw --link some-mysql:mysql -d -p 8080:80 wordpress
```
