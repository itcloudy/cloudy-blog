# Ubuntu下Java JDK安装

下载JDK [JDK下载地址](http://www.oracle.com/technetwork/java/javase/downloads/index.html),linux 64位


* 解压文件
<pre><code>
$ tar -zxvf jdk-8u111-linux-x64.tar.gz 
$ sudo mv jdk1.8.0_111  /usr/local/jdk1.8.0_111 
</code></pre> 
ps： 若作为docker的宿机，在宿机上启动jenkins容器或tomcat容器，下面的步骤可忽略
* 修改环境变量，在`/etc/profile`中添加以下几行,完成后需要执行`$ source /etc/profile`使环境变量生效
<pre><code>
JAVA_HOME=/usr/local/jdk1.8.0_111
CLASSPATH=.:$JAVA_HOME/lib.tools.jar
PATH=$JAVA_HOME/bin:$PATH
export JAVA_HOME CLASSPATH PATH
</code></pre>