# Compose-docker安装
* 二进制安装
<pre><code>
$ sudo curl -L https://github.com/docker/compose/releases/download/1.17.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
</code></pre>
* pip安装
<pre><code>
sudo pip install -U docker-compose
</code></pre>
* bash 补全命令
<pre><code>
curl -L https://raw.githubusercontent.com/docker/compose/1.8.0/contrib/completion/ba
sh/docker-compose > /etc/bash_completion.d/docker-compose
</code></pre>