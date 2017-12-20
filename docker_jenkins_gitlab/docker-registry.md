#Docker私有仓库创建 #
宿机系统为centos7，宿机环境请看[Centos下Docker安装(Centos7)](centos-docker-install.md)

* 拉取仓库镜像
<pre><code>
docker pull registry
</code></pre>
* 容器运行
<pre><code>
docker run -d -p 5000:5000 --restart=always --name registry registry
</code></pre>
* 仓库放到宿机中
<pre><code>
docker run -d -p 5000:5000 --name registry -v /opt/data/registry:/var/lib/registry registry
</code></pre>
* 宿机仓库地址配置，不同系统配置不一样
	* 使用 upstart 的系统(ubuntu12.04,Ubuntu 14.04, Debian 7 Wheezy) ,编辑 /etc/default/docker,增加如下内容
	<pre><code>
	DOCKER_OPTS="--registry-mirror=https://registry.docker-cn.com --insecure-registries=192.168.16.103:5000"
	</code></pre>
	* 使用 systemd 的系统(Ubuntu 16.04+, Debian 8+, centos 7),在 /etc/docker/daemon.json中增加如下内容（文件不存在可创建）
	<pre><code>
	{
	   "registry-mirror": [
          "https://registry.docker-cn.com"
       ],
       "insecure-registries": [
          "192.168.199.100:5000"
      ]
	}
	</code></pre>
	* 重启docker 

