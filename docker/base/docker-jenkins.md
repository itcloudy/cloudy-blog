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
	
*  jenkins 宿机生成ssh

当前用户为cloudy非root
<pre><code>
$ ssh-keygen -t rsa
$ pwd
/home/cloudy/.ssh
$ cat id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDYUUeKt/fVBV8CTM647y8ak4CJGjsaUu+iCj9VprQ7y9kp7KM7HtEMKIc+c8hxZ2l6ctPtxXMjLmBcaOFQUa9no4lgpfO2ir9hXyBbRrIvXSIEhbysXiJQez4d9oYnWY1YtbCkWa/t7lVdWXYNZs9l3wTPJXaFLYlQBC6y8Bhh/y3CtUJxtVgDRALZFNnSRtfUwWdkm9i4R//li/XWQePuKqadHPx1EJwwvKmF5vM0FBLvKZYYAhwOKYNgZnIaqh7WM0leglaPRlosX8r3i2PNemnbsKhCPt34qEW5p5nPsFPLyMRWRHfRjRhquaq7ECUWhyJ1w5HfB+JDdlQzMhYL cloudy@localhost.localdomain
</code></pre> 

gitlab的jenkins用户添加sshkey
![](images/docker_jenkins/docker_gitlab_private_key.png)
将私钥添加到jenkins的Credentialsz中
<pre><code>
$ cat id_rsa
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA2FFHirf31QVfAkzOuO8vGpOAiRo7GlLvogo/Vaa0O8vZKeyj
Ox7RDCiHPnPIcWdpenLT7cVzIy5gXGjhUFGvZ6OJYKXztoq/YV8gW0ayL10iBIW8
rF4iUHs+HfaGJ1mNWLWwpFmv7e5VXVl2DWbPZd8EzyV2hS2JUAQusvAYYf8twrVC
cbVYA0QC2RTZ0kbX1MFnZJvYuEf/5Yv11kHj7iqmnRz8dRCcMLyphebzNBQS7ymW
GAIcDimDYGZyGqoe1jNJXoJWj0ZaLF/K94tjzXpp27CoQj7d+KhFuaeZz7BTy8jE
VkR30Y0YarmquxAlFocidcOR3wfiQ3ZUMzIWCwIDAQABAoIBAQDRtaKE4ir6slVU
VoAGm6LvwdXXlL19nK/CSOrzr0SFv+8NjOMGWq7Reaz7p6XIAzgnxJCer1Aa6Ef0
7pyYkEhbUhjJwLjP3B0DWgR1WMk/z6s99SVfeXcMzR4AUFHobhHw0VupSWWcZfUO
Jb+j6GriWN5BsBEBtY6sKxHW2ZrZzI+wHGNoITmNZKta9mVPUaX4kWaJ7RW+7CJM
+AXkP/6Fbfcc43Fm5f6tVVfjAus9tN/Jd3jG1+1Ou8steAwqulexgFNwzpZFDfM0
vXbkPGcaZ8IJ1fRkn9Bw3X0veGZrUwWCnrYJDyGRTLkFSJ1KPOH2AU7qrghbbg4i
KRe9P1YBAoGBAPWVEQreYOhMZjEEq6pnS4CyhwqD3HTCEzqspjToyifHsxnxzrK0
d34LcWX0LetsP/u50ghOJhZixuddQQdjAxy8yu3FdJ5YcY6PGvJMaqLhuBk5RnHk
Xoq/AHG4gNbahYqKUW4UEkoCFmKTAxj1DPLzBgfGHoCINb9th1xpWksLAoGBAOF+
aHHaVMe4IXrxpO8rEMl6yTI28ooXOwXfHrEeoiXlmgzL8uIAS5qxev90+YSWwWag
xw4VWWBWbGm62ySGOBvXyWtT3u5r5VnBnkw5qpkHIWZqD7z0ScyWmWILb5AdBd/n
3cQ8CupINCxxvupwM0fJ1vsCDDaHCZrWtdAknkEBAoGAOHaZgII4jbBjHooQXhF5
zpE9czF2EnI8sZTYcfnD4PmNOD3cZEIR5y0CWYqWtDYjT+EdZUNyhlsXmEJcnTIq
mQTfM2PeuDllgn1smKDxM5nqFgKRK8Zx5jycAYmGNd/wLDY5GrIKsnFgbDGY2Lge
zg0KKednQ+4NTYIFST3/wJkCgYBX9xYLhB6aosv8yBONcYFk989RFXpcQF+4FKhG
dCrRGdaUs2MWowLbX+0Zhqpn/N+Jh6LfbZimKlC0lj4y62EsC2v5wIgw/kpET3HP
TpeshsmSyEFHdwzrELzZMJje4VOPW0Z57OpdJrmjtOPDVO3MTYLd/JiDFP68NpJK
ll5eAQKBgHe1+NzDguNi/Vy9D0gJuJnAxtT144n9ONvhZpu3g+C76ggLsloz4UF5
W/Uouyynv873h8NdASxnTg0vKDQbOm3+Qsy0QBbh8i3FmibsNOvN4l/FE1CN306s
vMK3uBu+4ryUFoBOitOx4NpUk7wkMzgq4h2JsPRGOu8NkkGwRXm3
-----END RSA PRIVATE KEY-----
</code></pre>
![](images/docker_jenkins/docker_jenkin_private_key.png)



首先需要在宿机创建jenkins数据存储的文件夹docker_jenkins，并修改权限使jenkins可以访问

<pre><code>
$ mkdir docker_jenkins
$ docker run \
	-d -p 81:8080 -p 50000:50000  \
	-v /home/cloudy/docker_jenkins:/var/jenkins_home  \
	-v /var/run/docker.sock:/var/run/docker.sock  \
	-v /var/lib/docker:/var/lib/docker \
	-v $(which docker):/usr/bin/docker \
	-v /usr/local/jdk1.8.0_111:/usr/local/jdk1.8.0_111 \
	-v /usr/local/maven3.5.2:/usr/local/maven3.5.2  \
	-v /usr/bin/git:/usr/bin/git \
	-v /home/cloudy/.ssh:/var/jenkins_home/.ssh \
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