# Docker容器之nginx(官方使用配置篇)


* 拉取镜像
<pre><code>$ docker pull nginx</code></pre>
* 启动容器
<pre><code>
$ docker run --name artistnginx -dit -p 83:80 \
-v $(pwd)/artist_nginx/web:/usr/share/nginx/html \
-v /var/run/docker.sock:/var/run/docker.sock \
-v  $(pwd)/artist_nginx/logs:/var/log/nginx \
nginx 
</code></pre>
 
* ps
在与jenkins集成的过程中，宿机文件用户为root，导致jenkins使用	SSH Publishers时无法将文件push到`$(pwd)/artist_nginx/web`中,修改文件夹的权限即可，push完成后需重启artistnginx