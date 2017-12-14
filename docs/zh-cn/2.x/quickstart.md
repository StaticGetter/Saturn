# 快速开始
## 1 一键启动
**注意，这种启动方式只适合试玩，不适合用于生产。**

首先，请确保本机环境：

* Java 7.0+
* Maven 3.0.4 +

然后，git克隆本仓库到本地，checkout对应版本分支，进入`quickstart`目录，如果是Windows系统，请运行`quickstart.bat`，如果是Linux/Unix/MacOS系统，请运行`quickstart.sh`。

quickstart脚本将做如下事情：
* 启动内嵌的ZooKeeper
* 启动内嵌的Saturn-Console
* 启动内嵌的Saturn-Executor（包含了一个Java作业的实现）
* 在Saturn-Console添加该Java作业

启动完成后，您可以访问Saturn-Console：[http://localhost:9088](http://localhost:9088)

## 2 Docker启动

```
$ git clone https://github.com/vipshop/Saturn
$ git checkout develop
$ cd saturn-docker
$ chmod +x quickstart-docker.sh
$ ./quickstart-docker.sh
```

quickstart-docker.sh脚本将做如下事情：
* 构建基于OpenJDK7的基础镜像
* 构建基于OpenJDK7的Saturn-Console镜像
* 构建基于OpenJDK7的Saturn-Executor镜像
* 启动一个ZooKeeper集群的容器
* 启动一个Saturn-Console容器
* 启动两个Saturn-Executor容器
* 添加一个Java作业和一个Shell作业

启动成功后，您可以访问Saturn-Console：[http://localhost:9088](http://localhost:9088)

## 3 生产环境（物理机）
* [部署Saturn-Console](zh-cn/2.x/saturn-console-deployment.md)
* [开发Java作业](zh-cn/2.x/saturn-dev-java.md) or [开发Shell作业](zh-cn/2.x/saturn-dev-shell.md)
* [部署Saturn-Executor](zh-cn/2.x/saturn-executor-deployment.md)