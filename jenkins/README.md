该文档将会介绍jenkins的相关内容。

# 前沿
首先jenkins是一个持续集成的工具。这里就不对其进行详述了。   
需要了解的同学，可以去jenkins的官网进行了解：https://jenkins.io/index.html   

## Quick Start
1. 下载jenkins
    http://mirrors.jenkins.io/war-stable/latest/jenkins.war
2. 启动jenkins
   ``java -jar jenkins.war``
3. 访问jenkins
    ``http://localhost:8080``   
    此时会提示输入密码，使用一下命令查看密码: ``less ~/.jenkins/secrets/initialAdminPassword``   
    之后开始下载插件，这里使用的是推荐的插件。
    jenkins所有的插件和配置文件，都会在``~/.jenkins``目录中。
    之后创建完帐号以后就可以了。
    
# 目录
