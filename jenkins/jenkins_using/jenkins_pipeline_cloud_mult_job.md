# Jenkins + Pipeline 分Job实现SpringCloud微服务CI
所有的微服务代码都在一个项目中

思路：先用一个job拉取代码，若存在公共module，为此module建立一个job，为每个微服务创建一个job，暂时不考虑只修改某个微服务代码的情况下只构建该微服务。

## 创建拉取代码job

* 创建job
    ![](images/jenkins_pipeline_cloud_mult_job/artist_server_pull_code_job_create.png)
* 设置代码仓库和构建触发器令牌
    ![](images/jenkins_pipeline_cloud_mult_job/artist_server_pull_code_job_gitlab_setting.png)
* gitlab上System Hooks创建
    ![](images/jenkins_pipeline_cloud_mult_job/artist_server_pull_code_gitlab_hook_create.png)

## 创建公共module的job

* 创建job
    ![](images/jenkins_pipeline_cloud_mult_job/artist_server_common_job_create.png)
* 设置触发
    ![](images/jenkins_pipeline_cloud_mult_job/artist_server_common_job_trigger.png)

