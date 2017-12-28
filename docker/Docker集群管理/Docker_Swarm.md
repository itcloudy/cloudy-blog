# Swarm集群部署实例

参考:[ Docker管理工具-Swarm部署记录](http://www.cnblogs.com/kevingrace/p/6870359.html)
## Swarm介绍

Swarm是Docker公司在2014年12月初发布的一套较为简单的工具，用来管理Docker集群，它将一群Docker宿主机变成一个单一的，虚拟的主机。Swarm使用标准的Docker API接口作为其前端访问入口，换言之，各种形式的Docker Client(docker client in Go, docker_py, docker等)均可以直接与Swarm通信。Swarm几乎全部用Go语言来完成开发，Swarm0.2版本增加了一个新的策略来调度集群中的容器，使得在可用的节点上传播它们，以及支持更多的Docker命令以及集群驱动。Swarm deamon只是一个调度器（Scheduler）加路由器(router)，Swarm自己不运行容器，它只是接受docker客户端发送过来的请求，调度适合的节点来运行容器，这意味着，即使Swarm由于某些原因挂掉了，集群中的节点也会照常运行，当Swarm重新恢复运行之后，它会收集重建集群信息。

Docker的Swarm(集群)模式，集成很多工具和特性，比如：跨主机上快速部署服务，服务的快速扩展，集群的管理整合到docker引擎，这意味着可以不可以不使用第三方管理工具。分散设计，声明式的服务模型，可扩展，状态协调处理，多主机网络，分布式的服务发现，负载均衡，滚动更新，安全（通信的加密）等等,下面就来认识下Swarm（对于Swarm管理的详细操作可以参考：https://www.centos.bz/tag/swarm/page/3/）
## Swarm架构

* 192.168.21.205      swarm的manager节点      manager-node
* 192.168.21.176      swarm的node节点         node1
* 192.168.21.67       swarm的node节点         node2

## 设置主机名

* 在manager节点上:`$ hostnamectl --static set-hostname manager-node`
* 在node1节点上:`$ hostnamectl --static set-hostname node1`
* 在node2节点上:`$ hostnamectl --static set-hostname node2`

## 在三台机器上都要设置hosts，均执行如下命令：

<pre><code>
$  vim /etc/hosts
......
192.168.21.205 manager-node
192.168.21.176 node1
192.168.21.67 node2
</code></pre>
## 关闭三台机器上的防火墙。如果开启防火墙，则需要在所有节点的防火墙上依次放行2377/tcp（管理端口）、7946/udp（节点间通信端口）、4789/udp（overlay 网络端口）端口。

<pre><code>
$ systemctl disable firewalld.service
$ systemctl stop firewalld.service
</code></pre>
## 获得swarm镜像

<pre><code>sudo docker pull swarm</code></pre>
## 创建swarm（要保存初始化后token，因为在节点加入时要使用token作为通讯的密钥）
在manager-node上操作
<pre><code>
$ sdocker swarm init --advertise-addr 192.168.21.205
Swarm initialized: current node (1fqzwbl4qy6stp9aqo6r2j2j3) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-5f5d04wukrj289s835tdxngo82nj5l3w4rwn17rf6litsizs8y-7tob7l24uv2o2blhcj5jflfmf 192.168.21.205:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions
</code></pre>
## 查看信息
<pre><code>
$  docker node ls          
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS
1fqzwbl4qy6stp9aqo6r2j2j3 *   manager-node        Ready               Active              Leader
</code></pre>

## 添加节点到swarm集群中,分别在node1和node2上执行
<pre><code>
$  docker swarm join --token SWMTKN-1-5f5d04wukrj289s835tdxngo82nj5l3w4rwn17rf6litsizs8y-7tob7l24uv2o2blhcj5jflfmf 192.168.21.205:2377
    This node joined a swarm as a worker.
</code></pre>
## 查看节点群
<pre><code>
[cloudy@manager-node ~]$ docker node ls
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS
1fqzwbl4qy6stp9aqo6r2j2j3 *   manager-node        Ready               Active              Leader
5nlvs25m2u13jtoa05ciynxd7     node1               Ready               Active              
6erve3p8x2kf75sealmjdh048     node1               Ready               Active              
</code></pre>
## 更改节点的availablity状态
<pre><code>
[cloudy@node1 ~]$ docker node update --availability drain node1           
</code></pre>
## 在Swarm中部署服务（这里以nginx服务为例）
* 启动容器之前，先来创建一个覆盖网络，用来保证在不同主机上的容器网络互通的网络模式
<pre><code>
[cloudy@manager-node ~]$ docker network create -d overlay ngx_net
z5jpu57nkrltq3rp1dbprizs4
[cloudy@manager-node ~]$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
433588ffc6b7        bridge              bridge              local
40dfe98c9a25        docker_gwbridge     bridge              local
6fe343f18fd0        host                host                local
ut69wggu9nj5        ingress             overlay             swarm
z5jpu57nkrlt        ngx_net             overlay             swarm
d4579190e245        none                null                local
</code></pre>
* 在manager-node节点上使用上面这个覆盖网络创建nginx服务：

其中，--replicas 参数指定服务由几个实例组成。
注意：不需要提前在节点上下载nginx镜像，这个命令执行后会自动下载这个容器镜像（比如此处创建tomcat容器，就将下面命令中的镜像改为tomcat镜像）。
<pre><code>
[cloudy@manager-node ~]$  docker service create --replicas 1 --network ngx_net --name my-test -p 80:80 nginx
</code></pre>
* 查看正在运行服务的列表
<pre><code>
[cloudy@manager-node ~]$ docker service ls
</code></pre>
* 查询Swarm中服务的信息
<pre><code>
[cloudy@manager-node ~]$ docker service inspect --pretty my-test

ID:             n7v8y8y3d8i58oa300kqsa6vb
Name:           my-test
Service Mode:   Replicated
 Replicas:      1
Placement:
UpdateConfig:
 Parallelism:   1
 On failure:    pause
 Monitoring Period: 5s
 Max failure ratio: 0
 Update order:      stop-first
RollbackConfig:
 Parallelism:   1
 On failure:    pause
 Monitoring Period: 5s
 Max failure ratio: 0
 Rollback order:    stop-first
ContainerSpec:
 Image:         nginx:latest@sha256:ed3ccac7b83f0a8eb5341f9968b0c8cb85959eadaab926f336ef9bb9c1358e40
Resources:
Networks: ngx_net 
Endpoint Mode:  vip
Ports:
 PublishedPort = 80
  Protocol = tcp
  TargetPort = 80
  PublishMode = ingress 
</code></pre>