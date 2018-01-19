# docker jenkins 部署

* 获得镜像(jenkinsci/jenkins)
<pre><code>
$ docker pull jenkinsci/jenkins
</code></pre>
* 创建容器
<pre><code>
$ docker run -u root -dit -p 82:8080 --name jenkinsci \
-v $(pwd)/docker_jenkinsci:/var/jenkins_home \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /usr/local/maven3.5.2:/usr/local/maven3.5.2  \
-v /usr/local/node-v8.4.0/bin:/user/local/node-v8.4.0/bin \
jenkinsci/jenkins
</code></pre>
* 安装插件
	* gitlab plugin
	* gitlab webhook plugin
    * Blue Ocean
    * Publish Over SSH
    * ThinBackup
    * Email Extension Plugin



进入docker容器
<pre><code>
$  docker exec -it jenkins bash
</code></pre>
若出现下面的错误，需要修改容器卷的权限 `$ sudo chown -R 1000 docker_jenkins`
<pre><code>
touch: cannot touch ‘/var/jenkins_home/copy_reference_file.log’: Permission denied
Can not write to /var/jenkins_home/copy_reference_file.log. Wrong volume permissions?
</code></pre>
若命令中没有添加-d，表示未在后台运行，若启动成功会打印出初始密码，复制初始密码

后台运行时的密码在 /your/home/docker_jenkins/secrets/initialAdminPassword中


ps:docker jenkins的时区和本地不一致时需要修改时区
<pre><code>
 docker exec -it jenkinsci bash
 echo Asia/Shanghai > /etc/timezone 
 </code></pre>