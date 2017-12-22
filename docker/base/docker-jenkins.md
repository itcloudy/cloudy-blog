# docker安装jenkins #

* 搜索jenkins镜像
<pre><code>
$ docker search jenkins
</code></pre>
* 拉取官方的镜像
<pre><code>
$ docker pull jenkins
</code></pre>
* 运行jenkins
<pre><code>
$ docker run -p 8080:8080 -p 50000:50000 jenkins
</code></pre>
* 数据存储在宿机
* Java JDK和Maven包在宿机上
	* [ubuntu上java jdk安装](ubuntu-maven.md)
	* [ubuntu上maven安装](ubuntu-java-jdk.md)
	
首先需要在宿机创建jenkins数据存储的文件夹docker_jenkins，并修改权限使jenkins可以访问

<pre><code>
$ mkdir docker_jenkins
$ docker run \
	-d -p 9001:8080 -p 50000:50000  \
	-v /home/release/docker_jenkins:/var/jenkins_home  \
	-v /var/run/docker.sock:/var/run/docker.sock  \
	-v /var/lib/docker:/var/lib/docker \
	-v $(which docker):/usr/bin/docker \
	-v /usr/local/jdk1.8.0_111:/usr/local/jdk1.8.0_111 \
	-v /usr/local/maven3:/usr/local/maven3  \
	-v /usr/bin/git:/usr/bin/git \
	-v ~/.ssh:/var/jenkins_home/.ssh \
	--name=jenkins jenkins 
</code></pre>  

若出现下面的错误，需要修改容器卷的权限 `$ sudo chown -R 1000 docker_jenkins`
<pre><code>
touch: cannot touch ‘/var/jenkins_home/copy_reference_file.log’: Permission denied
Can not write to /var/jenkins_home/copy_reference_file.log. Wrong volume permissions?
</code></pre>
若命令中没有添加-d，表示未在后台运行，若启动成功会打印出初始密码，复制初始密码

后台运行时的密码在 /your/home/docker_jenkins/secrets/initialAdminPassword中

* 登录jenkins
	* 浏览器进入jenkins服务地址，宿机端口为:9001

* 插件安装
列出的插件会在blog中其他的地方使用到
	* gitlab plugin
	* gitlab webhook plugin
	* Maven Integration plugin
	* Xcode integration 
	* Gradle plugin 
	* Blue Ocean
	* Publish Over SSH
	* CloudBees Docker Build and Publish plugin
	* File Operations Plugin
	* Cobertura Plugin
	* xUnit plugin
	* Performance plugin