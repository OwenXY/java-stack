# Java技术栈笔记

[![reading](https://badgen.net/badge/books/read%20together/cyan)]
[![coding](https://badgen.net/badge/leetcode/coding%20together/cyan)]
[![sharing](https://badgen.net/badge/readers/share%20together/cyan)]
[![stars](https://badgen.net/github/stars/doocs/wulimax/reactApp)]
[![forks](https://badgen.net/github/forks/wulimax/reactApp)]
[![contributors](https://badgen.net/github/contributors/wulimax/reactApp)]
[![help-wanted](https://badgen.net/github/label-issues/wulimax/reactApp/help%20wanted/open)]
[![issues](https://badgen.net/github/open-issues/wulimax/reactApp)]
[![PRs Welcome](https://badgen.net/badge/PRs/welcome/green)](http://makeapullrequest.com)

### 内容说明：
左林林个人文档


## 目录

- [java核心知识](#java核心知识)
    - [jvm](#jvm)
    - [security](#security)
    - [并发编程](#并发编程)
    - [基础](#基础)
- [计算机网络](#计算机网络)
    - [IO多路复用分享](#IO多路复用分享)
    - [Linux Epoll原理解析](#LinuxEpoll原理解析)
    - [Socket常见异常](#Socket常见异常)
    - [TCP有限状态机](#TCP有限状态机)
    - [计算机网络教材整理](#计算机网络教材整理)
    - [HTTP2的艺术](#HTTP2的艺术)
    - [HTTPS实践](#HTTPS实践)
    - [当你输入一个网址的时候，实际会发生什么?](#当你输入一个网址的时候，实际会发生什么)
    - [HTTP协议的底层实现](#HTTP协议的底层实现)
    - [BIO\NIO\Epoll\IO复用](#BIO\NIO\Epoll\IO复用)
- [开源框架](#开源框架)
    - [spring](#spring)
    - [spring boot](#第四季-海量数据)
    - [spring cloud netflix](#springcloudnetfli)
    - [spring clond alibaba](#第五季-高性能)
    - [netty](#第六季-高可用)
    - [zookeeper](#zookeeper)
    - [elasticsearch](#elasticsearch)
    - [消息中间件](#消息中间件)
    - [Guava](#Guava)
- [技术方案](#技术方案)
  - [DDD领域驱动](#DDD领域驱动)
  - [异地高活](#异地高活)
  - [网关](#网关)
  - [高并发和高可用](#高并发和高可用)
  - [链路追踪](#链路追踪)
- [数据库](#数据库)
  - [mysql](#mysql)
  - [redis](#redis)
- [微服务](#互联网Java进阶面试训练营)
  - [分布式服务治理](#分布式服务治理)
  - [分布式架构基础](#分布式架构基础)
- [系统设计](#系统设计)
- [内功心法](#内功心法)
  - [软件设计原则](#软件设计原则)
  - [设计模式](#设计模式)
  - [算法与数据结构](#算法与数据结构)
- [日常摘录及问题总结](#日常摘录及问题总结)
  - [第一季:分布式](#第一季-分布式)
  - [第二季:高并发](#第二季-高并发)
  - [第三季:微服务](#第三季-微服务)
  - [第四季:海量数据](#第四季-海量数据)
  - [第五季:高性能](#第五季-高性能)
  - [第六季:高可用](#第六季-高可用)
- [DevOps](#互联网Java进阶面试训练营)
  - [Git](#第一季-分布式)
  - [Maven](#第二季-高并发)
  - [mybaits](#mybaits)
- [面试专栏](#互联网Java进阶面试训练营)
  - [java面试资源整理](#java面试资源整理)
  - [第一季:分布式](#第一季-分布式)
  - [第二季:高并发](#第二季-高并发)
  - [第三季:微服务](#第三季-微服务)
  - [第四季:海量数据](#第四季-海量数据)
  - [第五季:高性能](#第五季-高性能)
  - [第六季:高可用](#第六季-高可用)


## 大纲

### java核心知识
- [jvm](/docs/javacore/jvm.md)
- [security](/docs/javacore/jvm.md)
- [并发编程](/docs/javacore/concurrent.md)
- [基础](/docs/javacore/base.md)
### 计算机网络
- [IO多路复用分享](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484480&idx=1&sn=1c7262d7f185ad6f99b840fb7779a575&chksm=fba6ec43ccd16555d826772a530c280548d8fd9785a9169b87bb4ed82d8b12ad75154c98b957&mpshare=1&scene=1&srcid=0608DxO0IKPDPxNOoN1la590%23rd)
- [Linux Epoll原理解析](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd)
- [Socket常见异常](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484058&idx=1&sn=d5c1533204ea655e65947ec57f924799&chksm=fba6ea99ccd1638f945c585cf3b2df6f4d4112b17ea3648730d50fdb5508555d5f30316f4186&mpshare=1&scene=1&srcid=0608cDtcDBaGNgIU9v4zxS3f%23rd)
- [TCP有限状态机](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484070&idx=1&sn=c1d49bce3c9da7fcc7e057d858e21d69&chksm=fba6eaa5ccd163b3a935303f10a54a38f15f3c8364c7c1d489f0b1aa1b2ef293a35c565d2fda&mpshare=1&scene=1&srcid=0608QzOXG2l0z2QyfVaCKqRH%23rd)
- [计算机网络教材整理](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484094&idx=1&sn=b337161f934b1c27ff1f059350ef5e65&chksm=fba6eabdccd163abc8978b65e155d79a133f20ee8a5bff79a33ed20a050c2bd576581db69fe6&mpshare=1&scene=1&srcid=0608yIcfsyrDG1NIBSsF58jq%23rd)
- [HTTP2的艺术？](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484095&idx=1&sn=aa915ae16d0a550bbe7ae4b6fec99173&chksm=fba6eabcccd163aa2bc0e880d7d3929eee5ff834a73a6ccc3a53237537a4555ef7fd4d9e70d0&mpshare=1&scene=1&srcid=0608QNgPOxWhMZfdNvGvcoUW%23rd)
- [HTTPS实践](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484129&idx=1&sn=d2a95310db5751b152ba070caee4ebae&chksm=fba6eae2ccd163f48aef9d98a4dbb55d578a24af710e1436cc876fe3119b03135532e16d80bc&mpshare=1&scene=1&srcid=06089KYIxoL86LbBEP44hsnV%23rd)
- [当你输入一个网址的时候，实际会发生什么?](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484257&idx=1&sn=e7704f92a1008ab7a292e2826bd079aa&chksm=fba6eb62ccd1627451d439bbc21e46e6fc1d7bfbe2a431fd887cf974a7bd0d9d482697f0e4fd&mpshare=1&scene=1&srcid=0608mcZB6SlZ2JGY46F7giS3%23rd)
- [BIO\NIO\Epoll\IO复用](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484157&idx=1&sn=f4644be2db6b1c230846cb4d62ae5be9&chksm=fba6eafeccd163e817b420d57478829d92251a6a5fd446f81805f0983a0d95cb6853a6735c4b&mpshare=1&scene=1&srcid=06083A6RVW3ZtKQRy6Ttq8tK%23rd)



### 开源框架
- [spring](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484955&idx=1&sn=be39f51e00d78eb7d3a4ae6b7137e62c&chksm=fba6ee18ccd1670ec7dbf62f2c73d65b241cfb6897bac9316981c1e7936e31c1caee5ccee87e&mpshare=1&scene=1&srcid=0608zdpqBAGKWQr6ExuWOvtg%23rd)
- [spring boot](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484908&idx=1&sn=6acc6ff3ce5e2ca1d0c2639868356a5e&chksm=fba6edefccd164f92d15faab6b8f77e4118c299ea5b1c366ac2db2aad9f12c761ef051355600&mpshare=1&scene=1&srcid=0608rMH6pNVzMB7wHy5caCrN%23rd)
- [spring cloud netflix](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484786&idx=1&sn=be07d63f36ee97031031dc455c03e3ca&chksm=fba6ed71ccd164677ef4e94ad64409783ec4a35d0cf8cfc2f2672a58099a382a496db2abf313&mpshare=1&scene=1&srcid=0608FUyrpWhHO2WyA36i9JK9%23rd)
- [spring clond alibaba](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484590&idx=1&sn=9d63dd0c4ab9150f6ac32f327d349d3b&chksm=fba6ecadccd165bb3c96ebd792d677ce25614f1cf48dbbe255534c149fe447c88761077f16b4&mpshare=1&scene=1&srcid=0608MowbddtGYWq6Fa26nPIJ%23rd)
- [netty](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484429&idx=1&sn=d8038c21ecd733b8bb7ff784014243f9&chksm=fba6ec0eccd165189e92a294ab2b7cd6796982c188befe05c27f4e96ae5cd39f2baf436cf37d&mpshare=1&scene=1&srcid=0608ttwG3fBdBUt7pdxL5IhX%23rd)
- [zookeeper](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247485090&idx=1&sn=5502672d9bf52551038b911d7ab623b9&chksm=fba6eea1ccd167b73a542b76dad423da21a2b452f768aac996cb50eeac1adc5d4978afe762ce&mpshare=1&scene=1&srcid=0608mo3eKwh686hXNzvRQfEB%23rd)
- [elasticsearch](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247485010&idx=1&sn=cd158d8358a0758fa81af094d58e2ea2&chksm=fba6ee51ccd1674753d77c8ab2a522cd8e32373b0a104eb9ecd6008cd12b6457eaade77e0514&mpshare=1&scene=1&srcid=0608LIOSiYzoUmlBHC4ZhnnZ%23rd)
- [消息中间件](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484844&idx=1&sn=cfa78df2943567269909f87217fa25c8&chksm=fba6edafccd164b9f6c22162a6386734010aeee9a084de720dacbb72d58bd1c20c0f961f5315&mpshare=1&scene=1&srcid=0608Ufv5zYZu66XnNn89WYEU%23rd)
- [Guava](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484813&idx=1&sn=4c9a43e51e1cf114efcf938e60ad58fd&chksm=fba6ed8eccd16498840a715659b8a29cf3368d28cf67c6fb27255277abe63421bca9ceb2cae7&mpshare=1&scene=1&srcid=06083zOsdotiVg1juwK3MYxZ%23rd)
### 技术方案
- [DDD领域驱动](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484480&idx=1&sn=1c7262d7f185ad6f99b840fb7779a575&chksm=fba6ec43ccd16555d826772a530c280548d8fd9785a9169b87bb4ed82d8b12ad75154c98b957&mpshare=1&scene=1&srcid=0608DxO0IKPDPxNOoN1la590%23rd)
- [异地多活](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd)
- [网关](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484058&idx=1&sn=d5c1533204ea655e65947ec57f924799&chksm=fba6ea99ccd1638f945c585cf3b2df6f4d4112b17ea3648730d50fdb5508555d5f30316f4186&mpshare=1&scene=1&srcid=0608cDtcDBaGNgIU9v4zxS3f%23rd)
- [高并发与高可用](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484070&idx=1&sn=c1d49bce3c9da7fcc7e057d858e21d69&chksm=fba6eaa5ccd163b3a935303f10a54a38f15f3c8364c7c1d489f0b1aa1b2ef293a35c565d2fda&mpshare=1&scene=1&srcid=0608QzOXG2l0z2QyfVaCKqRH%23rd)
- [链路追踪](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484094&idx=1&sn=b337161f934b1c27ff1f059350ef5e65&chksm=fba6eabdccd163abc8978b65e155d79a133f20ee8a5bff79a33ed20a050c2bd576581db69fe6&mpshare=1&scene=1&srcid=0608yIcfsyrDG1NIBSsF58jq%23rd)
### 数据库
- [mysql](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484480&idx=1&sn=1c7262d7f185ad6f99b840fb7779a575&chksm=fba6ec43ccd16555d826772a530c280548d8fd9785a9169b87bb4ed82d8b12ad75154c98b957&mpshare=1&scene=1&srcid=0608DxO0IKPDPxNOoN1la590%23rd)
- [redis](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd)
### 微服务
- [分布式服务治理](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484480&idx=1&sn=1c7262d7f185ad6f99b840fb7779a575&chksm=fba6ec43ccd16555d826772a530c280548d8fd9785a9169b87bb4ed82d8b12ad75154c98b957&mpshare=1&scene=1&srcid=0608DxO0IKPDPxNOoN1la590%23rd)
- [分布式服务架构](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd)    
### 系统设计
- [分布式服务治理](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484480&idx=1&sn=1c7262d7f185ad6f99b840fb7779a575&chksm=fba6ec43ccd16555d826772a530c280548d8fd9785a9169b87bb4ed82d8b12ad75154c98b957&mpshare=1&scene=1&srcid=0608DxO0IKPDPxNOoN1la590%23rd)
- [分布式服务架构](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd)    
### 内功心法
- [软件设计原则](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484480&idx=1&sn=1c7262d7f185ad6f99b840fb7779a575&chksm=fba6ec43ccd16555d826772a530c280548d8fd9785a9169b87bb4ed82d8b12ad75154c98b957&mpshare=1&scene=1&srcid=0608DxO0IKPDPxNOoN1la590%23rd)
- [设计模式](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd)  
- [算法与数据结构](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd)
### 日常摘录及问题总结
- [软件设计原则](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484480&idx=1&sn=1c7262d7f185ad6f99b840fb7779a575&chksm=fba6ec43ccd16555d826772a530c280548d8fd9785a9169b87bb4ed82d8b12ad75154c98b957&mpshare=1&scene=1&srcid=0608DxO0IKPDPxNOoN1la590%23rd)
- [设计模式](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd)  
- [算法与数据结构](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd) 
### DevOps  
- [git](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484480&idx=1&sn=1c7262d7f185ad6f99b840fb7779a575&chksm=fba6ec43ccd16555d826772a530c280548d8fd9785a9169b87bb4ed82d8b12ad75154c98b957&mpshare=1&scene=1&srcid=0608DxO0IKPDPxNOoN1la590%23rd)
- [maven](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd)  
- [docker](https://mp.weixin.qq.com/s?__biz=MzU0OTk3ODQ3Ng==&mid=2247484884&idx=1&sn=ceb798b6e8ef0ee608a992385f7d8568&chksm=fba6edd7ccd164c155271811f7948b476955cab41b23f2333847b8c268b31cc9f3332c2e3926&mpshare=1&scene=1&srcid=0608pIX1L8Fja1H99IyorW2X%23rd) 
### 面试专栏
  - [java面试资源整理](#java面试资源整理)
  - [第一季:分布式](#第一季-分布式)
  - [第二季:高并发](#第二季-高并发)
  - [第三季:微服务](#第三季-微服务)
  - [第四季:海量数据](#第四季-海量数据)
  - [第五季:高性能](#第五季-高性能)
  - [第六季:高可用](#第六季-高可用)

