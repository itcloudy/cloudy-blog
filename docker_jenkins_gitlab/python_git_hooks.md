# python实现git钩子 #
使用gitlab+jenkins实现CI是可以通过gitlab的System Hooks实现push触发，可参考[Gitlab利用webhook实现push代码后触发Jenkins自动构建](gitlab-webhook-jenkins.md),在spring cloud的微服务中，所有的微服务都在一个工程中，需要实现只构建有代码修改的微服务，而代码未修改的微服务不再次构建，目前没有想到更好的办法，打算用git钩子来实现


## 钩子编写
思路：钩子从钩子配置文件中(自己编写)获得工程下微服务的结构，并计算每个微服务的下每个文件的md5值(一个微服务所有的代码都在一个文件夹下)，和上一次的md5值进行比较，若发生变化则触发jenkins构建，并保存此次md5值，若存在微服务公共模块，功能模块修改所有的微服务都构建

