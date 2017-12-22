
#Ubuntu下Docker安装 #
核心概念：
--------

镜像（ Image ）和容器（ Container ）的关系，就像是面向对象程序设计中的 类 和 实例
一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删
除、暂停等。


* 卸载原有的docker  
<pre><code>
$ sudo apt-get remove docker docker-engine docker.io
</code></pre>
*  使用国内源
<pre><code>
$ curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
$ sudo apt-get update
$ sudo apt-get install docker-ce
</code></pre>
*  启动 Docker CE
<pre><code>
$ sudo systemctl enable docker
$ sudo systemctl start docker
</code></pre>
* 建立 docker 用户组
<pre><code>	
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
</code></pre>
* 运行hello-word
<pre><code>	
$ docker run hello-world
</code></pre>
 若出现下面的错误
<pre><code>	
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.32/containers/create: dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
</code></pre>
执行下面的命令
<pre><code>	
$ sudo service docker restart
$ newgrp - docker
</code></pre>
* 显示下面的信息说明安装成功
<pre><code>
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
ca4f61b1923c: Pull complete 
Digest: sha256:be0cd392e45be79ffeffa6b05338b98ebb16c87b255f48e297ec7f98e123905c
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images/docker_jenkins_gitlab, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
</code></pre>
* 列出镜像
<pre><code>
$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              f2a91732366c        3 weeks ago         1.85kB
</code></pre>
* 搜索镜像（官方和第三方的镜像）搜索centos镜像
<pre><code>
$  docker search centos
</code></pre>
* 查看启动了容器
<pre><code>
$  docker ps
</code></pre>
