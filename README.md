# LogicalDOC Enterprise Edition
Official Docker image for LogicalDOC Enterprise.
Note: This image requires to be connected to an external database

## What is LogicalDOC ?
The LogicalDOC is a flexible and highly performant Document Management System platform

![LogicalDOC](https://www.logicaldoc.com/images/assets/LogicalDocWhiteH02-167.png)

* **Manuals**: http://docs.logicaldoc.com
* **Twitter**: https://twitter.com/logicaldoc
* **Blog**: http://blog.logicaldoc.com

### How to use this image

## Start a LogicalDOC instance linked to a MySQL container
### 1) Run the MySQL container
```Shell
docker run -d --name=mysql-ld --env="MYSQL_ROOT_PASSWORD=mypassword" --env="MYSQL_DATABASE=logicaldoc" --env="MYSQL_USER=ldoc" --env="MYSQL_PASSWORD=changeme" mysql
```

### 2) Run the LogicalDOC container
```Shell
docker run -d -p 8080:8080 --env LDOC_USERNO=<your userno> --link mysql-ld logicaldoc/logicaldoc-ee
```

This image includes EXPOSE 8080 (the logicaldoc port). The default LogicalDOC configuration is applied.

The LogicalDOC DMS is accessible at http://${DOCKER_HOST}:8080/ and default User and Password are **admin** / **admin**.

### Your UserNo
You can pass a LogicalDOC activation code (the UserNo) when you launch this image.
That's way when your run the image the first time the activation procedure will be completed automatically and you will have a system completely setted up (ready-to-go).
If you need an activation code, you can get one delivered to your email by filling-out the form at https://www.logicaldoc.com/product/free-trial


## Start a LogicalDOC with some settings
```Shell
docker run -d -p 8080:8080 -p 1000:22 --env LDOC_USERNO=<your userno> --env LDOC_MEMORY=4000 --link mysql-ld logicaldoc/logicaldoc-ee
```
This will run the same image as above but with 4000 MB memory allocated to LogicalDOC, moreover it opens the SSH access through port 1000.

## Environment Variables
The LogicalDOC image uses environment variables that allow to obtain a more specific setup.

* **LDOC_MEMORY**: memory allocated for LogicalDOC expressed in MB (default is 2000)
* **LDOC_USERNO**: your own license activation code
* **SSH_PSWD**: pasword of the **logicaldoc** SSH user (default is 'logicaldoc')
* **DB_ENGINE**: the database type, possible vaues are: mysql(default), mssql, oracle, postgres
* **DB_HOST**: the database server host (default is 'mysql-ld')
* **DB_PORT**: the database communication port (default is 3306)
* **DB_NAME**: the database name (default is 'logicaldoc')
* **DB_INSTANCE**: some databases require the instance specification
* **DB_USER**: the username (default is 'ldoc')
* **DB_PASSWORD**: the password (default is 'changeme')

## Docker-Compose
Some docker-compose examples are available in the repository of this container on GitHub https://github.com/logicaldoc/logicaldoc-ee

