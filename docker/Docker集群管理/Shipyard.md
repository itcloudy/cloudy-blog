# Docker集中化web界面管理平台-Shipyard

Shipyard（github）是建立在docker集群管理工具Citadel之上的可以管理容器、主机等资源的web图形化工具,包括core和extension两个版本，core即shipyard主要是把多个 Docker host上的 containers 统一管理（支持跨越多个host），extension即shipyard-extensions添加了应用路由和负载均衡、集中化日志、部署等;Shipyard是在Docker Swarm实现对容器、镜像、docker集群、仓库、节点进行管理的web系统。

---------------------Shipyard---------------------

功能：简化对横跨多个主机的Docker容器集群进行管理

通过Web用户界面，你可以大致浏览相关信息，比如你的容器在使用多少处理器和内存资源、在运行哪些容器，还可以检查所有集群上的事件日志。

其特性主要包括：

* 支持节点动态集群，可扩展节点的规模（swarm、etcd方案）
* 支持镜像管理、容器管理、节点管理等功能
* 可视化的容器管理和监控管理
* 在线容console终端


## 了解Shipyard几个概念
	
* engine

    一个shipyard管理的docker集群可以包含一个或多个engine（引擎），一个engine就是监听tcp端口的docker daemon。

    shipyard管理docker daemon、images、containers完全基于Docker API，不需要做其他的修改。

    另外，shipyard可以对每个engine做资源限制，包括CPU和内存；因为TCP监听相比Unix socket方式会有一定的安全隐患，

    所以shipyard还支持通过SS

    证书与docker后台进程安全通信。
  
* rethinkdb
RethinkDB是一个shipyard项目的一个docker镜像，用来存放账号（account）、引擎（engine）、服务密钥（service key）、
扩展元数据（extension metadata）等信息，但不会存储任何有关容器或镜像的内容。

## Shipyard生态