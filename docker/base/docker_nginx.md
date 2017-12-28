# Docker容器之nginx(官方使用配置篇)


* 拉取镜像
<pre><code>$ docker pull nginx</code></pre>
* nginx配置文件修改
针对docker可以运行一个nginx镜像，然后从中获得配置文件
<pre><code>
$  docker run -dit --name nginx nginx
$ docker cp nginx:/etc/nginx/nginx.conf nginx.conf
</code></pre>
获得配置文件如下
<pre><code>

user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
</code></pre>
* 删除用户获得配置文件的nginx镜像
 
* 在/opt下建立文件夹artist, 将前端代码上传到服务器命名文件夹为artist-web，并将nginx.conf 复制到/opt/artist中
* 启动容器，指定配置文件
<pre><code>
$ docker run --name nginx -dit -p 80:80 -v /opt/artist/artist-web:/usr/share/nginx/html:ro -v /opt/artist/logs:/var/log/nginx -v /opt/artist/nginx.conf:/etc/nginx/nginx.conf:ro  nginx
</code></pre>


