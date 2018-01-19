# docker安装redis

* 获得镜像(redis:3.2.11) 
<pre><code>
$  docker pull redis:3.2.11
</code></pre>
* 创建容器
<pre><code>
$ docker run --name redis  redis:3.2.11 -p 7379:6379 -v $(pwd)/docker_redis/data:/data 
$  docker run -p 7379:6379 --name test-redis -v $(pwd)/docker_redis/redis.conf:/etc/redis/redis.conf -v $(pwd)/docker_redis/data:/data -d redis:3.2.11  redis-server /etc/redis/redis.conf --appendonly yes
</code></pre>
 