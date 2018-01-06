# docker安装mysql



* 获得镜像(mysql/mysql-server)  [DockerHub地址](https://hub.docker.com/r/mysql/mysql-server/)
<pre><code>
$ docker pull mysql/mysql-server
</code></pre>
* 创建容器
<pre><code>
$ docker run --name mysql -dit  -p 3307:3306 \
-v $(pwd)/docker_mysql:/var/lib/mysql \
-e MYSQL_ROOT_HOST=% \
-e MYSQL_ROOT_PASSWORD=cloudy \
mysql/mysql-server
</code></pre>
 