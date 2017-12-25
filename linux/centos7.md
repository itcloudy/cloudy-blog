# Centos7 相关操作 #

##　没有ifconfig命令
<pre><code>yum -y install net-tools</code></pre>

## 找不到网卡
* 到 `/etc/sysconfig/network-scripts/` 路径下 
* 执行命令`ls | grep ifcfg`,默认出现两个文件,排除`ifcfg-lo`
* 将另一个文件中的`ONBOOT=no`改为`ONBOOT=yes`
* 重启网卡`/etc/init.d/network restart`

## 当前用户添加到sudoers(root下操作)
*  `su root`
* `chmod u+w /etc/sudoers`   //u 表示所有者， w 表示写权限 + 表示添加

* `vi /etc/sudoers`
在文件中找到这一行：
<pre><code>
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
username ALL=(ALL)ALL  //添加这一行，username为要加入sudoers 的用户
</code></pre>

* 最后记得撤销文件的写权限: `chmod u-w /etc/sudoers`


## 安装ssh服务

* 检查是否安装了相关软件：`rpm -qa|grep -E "openssh"`
<pre><code>
$ rpm -qa|grep -E "openssh"
openssh-server-7.4p1-11.el7.x86_64
openssh-7.4p1-11.el7.x86_64
openssh-clients-7.4p1-11.el7.x86_64
</code></pre>
* 安装缺失的软件：`sudo yum install openssh* `
* 注册使用服务: `sudo systemctl enable sshd  && sudo systemctl start sshd`