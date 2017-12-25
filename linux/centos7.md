# Centos7 相关操作 #

##　没有ifconfig命令
<pre><code>yum -y install net-tools</code></pre>

## 找不到网卡
* 到`/etc/sysconfig/network-scripts/`路径下
* 执行命令`ls | grep ifcfg`,默认出现两个文件,排除`ifcfg-lo`
* 将另一个文件中的`ONBOOT=no`改为`ONBOOT=yes`
* 重启网卡`/etc/init.d/network restart`