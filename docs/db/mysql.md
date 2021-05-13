# mysql
## 目录

- [mysql基础架构](#mysql基础架构)
    - [Docker平台](#Docker平台)
    - [我可以将Docker用于什么](#我可以将Docker用于什么？)
    - [docker架构](#docker架构)
- [获取Docker](#获取Docker)
- [开始吧](#开始吧)
    - [编写Dockerfile的最佳实践](#编写Dockerfile的最佳实践)
    - [实例应用程序](#实例应用程序？)
    - [更新应用程序](#更新应用程序)
    - [共享应用程序](#共享应用程序)
    - [持久化数据库](#持久化数据库)
    - [使用绑定安装](#使用绑定安装)
    - [多容器应用](#多容器应用？)
    - [使用DockerCompose](#使用DockerCompose)
    - [图像构建最佳实践](#图像构建最佳实践)
    - [接下来做什么](#接下来做什么)
- [特定语言指南](#特定语言指南)
- [使用Docker开发](#使用Docker开发)
- [设置CI/CD](#设置CI/CD)
- [将应用部署到云](#将应用部署到云)
- [在生产环境运行应用](#在生产环境运行应用)
- [教育资源](#教育资源)
- [docker开源](#docker开源)


## 目录

mysql架构设计

一个不变的原则：网络连接必须让线程处理
mysql架构的整体设计原理
![img_1.png](image/mysqlshejiyuanli.png)

