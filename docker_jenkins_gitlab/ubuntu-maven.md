# Ubuntu下Maven安装 #

下载maven：[maven下载地址](http://maven.apache.org/download.cgi)，此处采用的是二进制文件bin.tar.gz文件


* 解压文件
<pre><code>
$ tar -zxvf  apache-maven-3.5.2-bin.tar.gz 
$ sudo mv apache-maven-3.5.2 /usr/local/maven3 
</code></pre> 
ps： 若作为docker的宿机，在宿机上启动jenkins容器或tomcat容器，下面的步骤可忽略
* 修改环境变量，在`/etc/profile`中添加以下几行,完成后需要执行`$ source /etc/profile`使环境变量生效
<pre><code>
MAVEN_HOME=/usr/local/maven3
export MAVEN_HOME
export PATH=${PATH}:${MAVEN_HOME}/bin
</code></pre>