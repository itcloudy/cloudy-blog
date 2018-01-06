# docker安装redis

* 获得镜像(redis:3.2.11) 
<pre><code>
$  docker pull redis:3.2.11
</code></pre>
* 创建容器
<pre><code>
$ docker run --name redis -d redis -p 7379:6379 -v  $(pwd)/docker_redis:/data
</code></pre>
 