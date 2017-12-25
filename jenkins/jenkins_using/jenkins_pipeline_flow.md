
# Jenkins + Pipeline 构建流水线发布
git仓库采用的是gitlab
* gitlab创建项目(需要将gitlab用户jenkins加入到项目中，角色为master)
![](images/jenkins_pipeline/gitlab_project_jenkinsfile_create.png)
* 本地创建代码库
![](images/jenkins_pipeline/local_jenkinsfile_repo.png)
* 使用Pipeline Syntax
  ![](images/jenkins_pipeline/git_pipeline_syntax.png)
* 创建文件`Jenkinsfile`,输入下面的内容
<pre><code>
node {

  stage ('Checkout') {
    git credentialsId: 'c6ec95d8-04b9-4230-acf9-0df64c3ce669', url: 'http://192.168.21.141:9003/artist-server/artist-server.git'
  }

  stage ('Build') {
    sh 'cd server/artist && mvn clean && mvn package'
  }

  
}
</code></pre>

* 创建job
  ![](images/jenkins_pipeline/jenkins_pipeline_create.png)
* Jenkins中pipeline-test中Pipeline设置
  ![](images/jenkins_pipeline/jenkins_pipeline_setting.png) 
* 构建(暂时忽略错误)
  ![](images/jenkins_pipeline/jenkins_pipeline_build_error.png)
* 查看文件结构,说明代码已经被拉取过来
截图经剪切处理，删除其他job
  ![](images/jenkins_pipeline/jenkins_pipeline_file_tree.png) 

* 修改脚本(实际中修改过多次)
<pre><code>
node {

  stage ('Checkout') {
    git credentialsId: 'c6ec95d8-04b9-4230-acf9-0df64c3ce669', url: 'http://192.168.21.141:9003/artist-server/artist-server.git'
  }

  stage ('Build') {
    // sh 'cd server/artist && mvn clean && mvn package' 由于jenkins采用的是docker部署，未设置变量，故需要使用下面的命令
    // /usr/local/maven3在jenkins容器创建是使用 -v 加载宿机的maven(jdk也从宿机加载)
    sh 'cd server/artist && /usr/local/maven3/bin/mvn clean && /usr/local/maven3/bin/mvn package'
    
  } 
  
}
</code></pre>

* 再次构建，成功
![](images/jenkins_pipeline/jenkins_pipeline_build_success.png)

