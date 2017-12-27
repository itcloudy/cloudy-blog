# Swarm集群部署实例

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

