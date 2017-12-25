# Centos下Docker安装(Centos7) #


* 卸载原有的docker  
<pre><code>
$ sudo yum remove docker docker-common docker-selinux docker-engine 
</code></pre>
* 使用 yum 源 安装
<pre><code>
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
$ sudo yum-config-manager --add-repo https://mirrors.ustc.edu.cn/docker-ce/linux/centos/docker-ce.repo
$ sudo yum-config-manager --enable docker-ce-edge //最新版本的 Docker CE
$ sudo yum makecache fast
$ sudo yum install docker-ce
</code></pre>
* 启动 Docker CE
<pre><code>
$ sudo systemctl enable docker
$ sudo systemctl start docker
</code></pre>
* 建立 docker 用户组
<pre><code>
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
</code></pre>
* 测试 Docker 是否安装正确
<pre><code>
$ docker run hello-world
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

*  查看容器的参数:sudo docker inspect 容器id/容器名 `docker inspect hello-world`