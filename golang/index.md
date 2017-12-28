# golang学习和进阶  

<pre><code>
exec: "gcc": executable file not found in %PATH%
</code></pre>
解决方式：需要安装[MinGW-w64](https://nchc.dl.sourceforge.net/project/mingw-w64/Toolchains%20targetting%20Win32/Personal%20Builds/mingw-builds/installer/mingw-w64-install.exe)

<pre><code>
 imports golang.org/x/net/websocket: unrecognized import path "golang.org/x/net/websocket" (https fetch: Get https://golang.org/x/net/websocket?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)
 </code></pre>
 解决方法以及其他类似包处理：
* 在GOPATH的src下创建golang.org文件夹，并在golang.org中创建x文件夹
* `git clone https://github.com/golang/net.git`
* `git clone https://github.com/golang/tools.git`
* `git clone https://github.com/golang/dep.git`
* `git clone https://github.com/golang/crypto.git`
* `git clone https://github.com/golang/oauth2.git`

## [golang微服务框架goa](goa/index.md)
## [golang微服务框架gokit](gokit/index.md)
## [web框架beego](beego/index.md)


