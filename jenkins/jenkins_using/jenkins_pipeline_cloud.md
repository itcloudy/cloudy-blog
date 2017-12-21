# Jenkins + Pipeline实现SpringCloud微服务CI
所有的微服务代码都在一个项目中

思路：先用一个job拉取代码，若存在公共module，为此module建立一个job，为每个微服务创建一个job，暂时不考虑只修改某个微服务代码的情况下只构建该微服务。

