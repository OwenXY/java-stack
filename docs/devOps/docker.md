# docker
## 目录

- [Docker概述](#Docker概述)
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

## 大纲
## 基础入门
### Docker概述
Docker是基于Go语言实现的开源容器项目。
Docker是一个用于开发，交付和运行应用程序的开放平台。
Docker使您能够将应用程序与基础架构分开，从而可以快速交付软件。
助Docker，您可以以与管理应用程序相同的方式来管理基础架构。通过利用Docker的快速交付，测试和部署代码的方法，您可以显着减少编写代码和在生产环境中运行代码之间的延迟。

#### Docker平台
Docker提供了在松散隔离的环境（称为容器）中打包和运行应用程序的功能。隔离和安全性使您可以在给定主机上同时运行多个容器。容器是轻量级的，包含运行该应用程序所需的所有内容，因此您无需依赖主机上当前安装的内容。您可以在工作时轻松共享容器，并确保与您共享的每个人都能以相同的方式获得相同的容器。

Docker提供了工具和平台来管理容器的生命周期：

- 使用容器开发应用程序及其支持组件。
- 容器成为分发和测试您的应用程序的单元。
- 准备就绪后，可以将应用程序作为容器或协调服务部署到生产环境中。无论您的生产环境是本地数据中心，云提供商还是两者的混合，其工作原理都相同。

#### 我可以将Docker用于什么？
快速，一致地交付您的应用程序

Docker通过允许开发人员使用提供您的应用程序和服务的本地容器在标准化环境中工作，从而简化了开发生命周期。容器非常适合进行持续集成和持续交付（CI / CD）工作流。

考虑以下示例方案：

- 您的开发人员在本地编写代码，并使用Docker容器与同事共享他们的工作。
- 他们使用Docker将其应用程序推送到测试环境中，并执行自动和手动测试。
- 当开发人员发现错误时，他们可以在开发环境中对其进行修复，然后将其重新部署到测试环境中以进行测试和验证。
- 测试完成后，将修补程序推送给生产环境就像将更新的映像推送到生产环境一样简单。
- 响应式部署和扩展

Docker的基于容器的平台允许高度可移植的工作负载。Docker容器可以在开发人员的本地笔记本电脑上，数据中心内的物理或虚拟机上，云提供商上或混合环境中运行。

Docker的可移植性和轻量级的特性还使您可以轻松地动态管理工作负载，并根据业务需求指示实时扩展或拆除应用程序和服务。

在相同的硬件上运行更多的工作负载

Docker轻巧快速。它为基于虚拟机管理程序的虚拟机提供了一种可行的，具有成本效益的替代方案，因此您可以利用更多的计算能力来实现业务目标。Docker非常适合高密度环境以及中小型部署，而您需要用更少的资源做更多的事情。

 **Docker与虚拟化**

虚拟化（virtualization）技术是一个通用的概念，在不同领域有不同的理解。在计算领域，一般指的是计算虚拟化（computing virtualization），或通常说的服务器虚拟化。

虚拟化的核心是对资源的抽象，目标往往是为了在同一个主机上同时运行多个系统或应用，从而提高系统资源的利用率，并且带来降低成本、方便管理和容错容灾等好处。

虚拟化：硬件的虚拟化和软件的虚拟化

软件虚拟化：应用虚拟化和平台虚拟化

平台虚拟化：【完全虚拟化:虚拟机模拟完整底层硬件环境和特权指令的执行过程，客户的操作系统无须进行修改。（例：VMware Workstation、VirtualBox）】

平台虚拟化：【硬件辅助虚拟化：利用硬件（主要是CPU）辅助支持（目前x86体系结构上可用的硬件辅助虚拟化技术包括Intel-VT和AMD-V）处理敏感指令来实现完全虚拟化的功能，客户操作系统无须修改。】

平台虚拟化：【部分虚拟化：只针对部分硬件资源进行虚拟化，客户操作系统需要进行修改。现在有些虚拟化技术的早期版本仅支持部分虚拟化；】

平台虚拟化：【超虚拟化：部分硬件接口以软件的形式提供给客户机操作系统，客户操作系统需要进行修改】

平台虚拟化：【操作系统级虚拟化。内核通过创建多个虚拟的操作系统实例（内核和库）来隔离不同的进程。容器相关技术即在这个范畴】

**Docker以及其他容器技术都属于操作系统虚拟化这个范畴**，操作系统虚拟化最大的特点就是不需要额外的supervisor支持。

![img.png](images/img.png)

传统方式是在硬件层面实现虚拟化，需要有额外的虚拟机管理应用和虚拟机操作系统层。Docker容器是在操作系统层面上实现虚拟化，直接复用本地主机的操作系统，因此更加轻量级。


#### docker架构
Docker使用客户端-服务器架构。Docker客户端与Docker守护进程进行对话，该守护进程完成了构建，运行和分发Docker容器的繁重工作。

Docker客户端和守护程序可以 在同一系统上运行，或者您可以将Docker客户端连接到远程Docker守护程序。

Docker客户端和守护程序在UNIX套接字或网络接口上使用REST API进行通信。

另一个Docker客户端是Docker Compose，它使您可以处理由一组容器组成的应用程序。

以访问Docker官网的Get Docker（https://www.docker.com/get-docker）页面，查看获取Docker的方式，以及Docker支持的平台类型

![img.png](images/dockerjiagou.png)

##### Docker守护程序

Docker守护程序（dockerd）侦听Docker API请求并管理Docker对象，例如图像，容器，网络和卷。守护程序还可以与其他守护程序通信以管理Docker服务。

##### Docker客户端

Docker客户端（docker）是许多Docker用户与Docker交互的主要方式。当您使用诸如之类的命令时docker run，客户端会将这些命令发送到dockerd，以执行这些命令。该docker命令使用Docker API。Docker客户端可以与多个守护程序通信。

##### Docker注册表

Docker注册表存储Docker镜像。Docker Hub是任何人都可以使用的公共注册表，并且默认情况下，Docker已配置为在Docker Hub上查找镜像。您甚至可以运行自己的私人注册表。

使用docker pull或docker run命令时，将从配置的注册表中提取所需的图像。使用该docker push命令时，会将映像推送到已配置的注册表。

##### Docker对象


使用Docker时，您正在创建和使用镜像，容器，网络，卷，插件和其他对象。

###### 镜像

**一个镜像是用于创建一个码头工人容器指令的只读模板**。通常，一个镜像基于另一个镜像，并进行一些其他自定义。例如，您可以基于该ubuntu 镜像构建镜像，但安装Apache Web服务器和您的应用程序，以及运行该应用程序所需的配置详细信息。

您可以创建自己的镜像，也可以仅使用其他人创建并在注册表中发布的镜像。**要构建自己的镜像，您可以 使用简单的语法创建一个Dockerfile**，以定义创建镜像并运行它所需的步骤。Dockerfile中的每条指令都会在镜像中创建一个层。

当您更改Dockerfile并重建镜像时，仅重建那些已更改的层。与其他虚拟化技术相比，这是使镜像如此轻巧，小型和快速的部分原因。

###### 容器

**容器是镜像的可运行实例**。**您可以使用Docker API或CLI创建，启动，停止，移动或删除容器**。您可以将容器连接到一个或多个网络，将存储连接到它，甚至根据其当前状态创建一个新镜像。

默认情况下，容器与其他容器及其主机之间的隔离程度相对较高。您可以控制容器的网络，存储或其他底层子系统与其他容器或与主机的隔离程度。

容器由其镜像在创建或启动时为其提供的任何配置选项定义。删除容器后，未存储在持久性存储中的状态更改将消失。

示例docker run命令
以下命令运行一个ubuntu容器，以交互方式附加到本地命令行会话，然后运行/bin/bash。

$ docker run -i -t ubuntu /bin/bash
当您运行此命令时，会发生以下情况（假设您使用的是默认注册表配置）：

如果您在ubuntu本地没有该映像，则Docker会将其从已配置的注册表中拉出，就像您已docker pull ubuntu手动运行一样。

Docker会创建一个新容器，就像您已docker container create 手动运行命令一样。

Docker将一个读写文件系统分配给容器，作为其最后一层。这允许运行中的容器在其本地文件系统中创建或修改文件和目录。

Docker创建了一个网络接口，将容器连接到默认网络，因为您没有指定任何网络选项。这包括为容器分配IP地址。默认情况下，容器可以使用主机的网络连接连接到外部网络。

Docker启动容器并执行/bin/bash。因为容器是交互式运行的，并且已附加到您的终端（由于-i和-t 标志），所以您可以在输出记录到终端时使用键盘提供输入。

当您键入exit以终止/bin/bash命令时，该容器将停止但不会被删除。您可以重新启动或删除它。
### 底层技术

Docker用Go编程语言编写，并利用Linux内核的多种功能来交付其功能。Docker使用一种称为的技术namespaces来提供称为容器的隔离工作区。运行容器时，Docker会为该容器创建一组 名称空间。

这些名称空间提供了一层隔离。容器的每个方面都在单独的名称空间中运行，并且对其的访问仅限于该名称空间。

### 获取Docker(https://docs.docker.com/engine/)

#### 在CentOS上安装Docker Engine (https://docs.docker.com/engine/install/centos/#prerequisites)

**系统要求**：CentOS 7或8
centos-extras库必须启用。默认情况下，此存储库是启用的
overlay2建议使用存储驱动程序

##### 卸载旧版本
较旧的Docker版本称为docker或docker-engine。如果已安装这些程序，请卸载它们以及相关的依赖项。

    sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

如果yum报告未安装这些软件包，则可以。

的内容（/var/lib/docker/包括图像，容器，卷和网络）被保留。Docker Engine软件包现在称为docker-ce。

##### 安装方法

您可以根据需要以不同的方式安装Docker Engine：

- 大多数用户会 设置Docker的存储库并从中进行安装，以简化安装和升级任务。这是**推荐的方法**。

- 一些用户下载并手动安装RPM软件包， 并完全手动管理升级。这在诸如在无法访问互联网的空白系统上安装Docker的情况下很有用。

- 在测试和开发环境中，一些用户选择使用自动 便利脚本来安装Docker。

**使用存储库安装**

在新主机上首次安装Docker Engine之前，需要设置Docker存储库。之后，您可以从存储库安装和更新Docker。

**设置存储库**

安装**yum-utils**软件包（提供**yum-config-manager** 实用程序）并设置稳定的存储库

    sudo yum install -y yum-utils
    sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo


可选：启用每晚或测试存储库。

这些存储库包含在docker.repo上面的文件中，但默认情况下处于禁用状态。您可以在稳定存储库旁边启用它们。以下命令启用每晚存储库。

    sudo yum-config-manager --enable docker-ce-nightly

要启用测试通道，请运行以下命令：

    sudo yum-config-manager --enable docker-ce-test
您可以通过运行带有标志的命令来禁用每晚或测试存储库 。要重新启用它，请使用该标志。以下命令禁用夜间存储库。yum-config-manager--disable--enable

    sudo yum-config-manager --disable docker-ce-nightly
了解每晚和测试频道。


#####  安装Docker引擎

二选一：

1.安装最新版本的Docker Engine和容器，或转到下一步以安装特定版本：

    sudo yum install docker-ce docker-ce-cli containerd.io

Docker已安装但尚未启动。docker创建该组，但没有用户添加到该组。

2.要安装特定版本的Docker Engine，请在存储库中列出可用版本，然后选择并安装：

一种。列出并排序您存储库中可用的版本。本示例按版本号（从高到低）对结果进行排序，并被截断：

    yum list docker-ce --showduplicates | sort -r

返回的列表取决于启用的存储库，并且特定于您的CentOS版本（.el7此示例中的后缀表示）。

b。通过其完全合格的软件包名称安装特定版本，该软件包名称是软件包名称（docker-ce）加上版本字符串（第二列），从第一个冒号（:）到第一个连字符，以连字符（-）分隔。例如，docker-ce-18.09.1。

sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
Docker已安装但尚未启动。docker创建该组，但没有用户添加到该组。

3.启动Docker。

    sudo systemctl start docker

4.通过运行hello-world 映像来验证是否正确安装了Docker Engine 。

    sudo docker run hello-world

##### 升级Docker引擎

从软件包安装

1.转到https://download.docker.com/linux/centos/ 并选择您的CentOS版本。然后浏览x86_64/stable/Packages/ 并下载.rpm要安装的Docker版本的文件。

    注意：要安装夜间或测试（预发布）软件包，stable请将上述URL中的单词更改为nightly或test。 了解每晚和测试频道。

2.安装Docker Engine，将下面的路径更改为您下载Docker软件包的路径。

    sudo yum install /path/to/package.rpm

Docker已安装但尚未启动。docker创建该组，但没有用户添加到该组。

3.启动Docker。

    sudo systemctl start docker
4.通过运行hello-world 映像来验证是否正确安装了Docker Engine 。

    sudo docker run hello-world

此命令下载测试图像并在容器中运行它。容器运行时，它会打印参考消息并退出。

Docker Engine已安装并正在运行。您需要使用sudo来运行Docker命令。继续执行Linux的安装后步骤，以允许非特权用户运行Docker命令以及其他可选配置步骤。

升级Docker引擎

要升级Docker Engine，请下载更新的软件包文件，并使用 代替重复 安装过程，并指向新文件。
    
    yum -y upgrade yum -y install

##### 卸载Docker

1.卸载Docker Engine，CLI和Containerd软件包：

    sudo yum remove docker-ce docker-ce-cli containerd.io

2,主机上的映像，容器，卷或自定义配置文件不会自动删除。要删除所有图像，容器和卷：

    sudo rm -rf /var/lib/docker
    sudo rm -rf /var/lib/containerd
您必须手动删除所有已编辑的配置文件。

Linux的安装后步骤(https://docs.docker.com/engine/install/linux-postinstall/)

##### 以非root用户管理Docker

Docker守护程序绑定到Unix套接字而不是TCP端口。**默认情况下，Unix套接字由用户拥有root，其他用户只能使用来访问它sudo**。Docker守护程序始终以root用户身份运行。

**如果您不想在docker命令前添加sudo，请创建一个Unix组docker，并将其添加用户。**Docker守护程序启动时，它会创建一个可由该docker组成员访问的Unix套接字。

注意事项：

要在没有root特权的情况下运行Docker，请参阅 以非root用户身份运行Docker守护程序（无根模式）（https://docs.docker.com/engine/security/rootless/）。

###### 要创建docker组并添加您的用户，请执行以下操作

1.创建docker组。

     sudo groupadd docker

2.将您的用户添加到该docker组。

    sudo usermod -aG docker $USER

3.注销并重新登录，以便重新评估您的组成员身份。

如果在虚拟机上进行测试，则可能需要重新启动虚拟机以使更改生效。

在台式机Linux环境（例如X Windows）上，完全注销会话，然后重新登录。

在Linux上，您还可以运行以下命令来激活对组的更改

       newgrp docker

4.确认您可以docker不带命令行运行命令sudo。

     docker run hello-world

###### 配置Docker以在启动时启动

当前大多数Linux发行版（RHEL，CentOS，Fedora，Debian，Ubuntu 16.04及更高版本）用于systemd管理系统引导时启动的服务。在Debian和Ubuntu上，默认情况下，将Docker服务配置为在引导时启动。要在启动时自动启动其他发行版的Docker和Containerd，请使用以下命令：

    sudo systemctl enable docker.service
    sudo systemctl enable containerd.service

若要禁用此行为，请disable改用。

    sudo systemctl disable docker.service
    sudo systemctl disable containerd.service

如果需要添加HTTP代理，为Docker运行时文件设置不同的目录或分区，或进行其他自定义，请参阅 自定义系统的Docker守护程序选项。

###### 配置默认的日志记录驱动程序

Docker提供了通过一系列日志记录驱动程序从主机上运行的所有容器收集和查看日志数据的**功能**。默认的日志记录驱动程序json-file将日志数据写入主机文件系统上的JSON格式的文件中。随着时间的流逝，这些日志文件的大小会扩大，从而可能会耗尽磁盘资源。

为了缓解此类问题，可以将**json-file**日志记录驱动程序配置为启用**日志循环**，使用 **备用日志记录驱动程序**， 例如 默认情况下执行日志循环的**“本地”日志记录驱动程序**，或者使用将日志记录发送到远程日志记录聚合器的日志记录驱动程序。


### 开始吧

    docker run -d -p 80:80 docker/getting-started
    -d -以分离模式运行容器（在后台）
    -p 80:80 -将主机的端口80映射到容器中的端口80
    docker/getting-started -要使用的图像
    可以组合单个字符标志来缩短完整命令
    docker run -dp 80:80 docker/getting-started

什么是容器？

什么是容器？简而言之，容器只是您计算机上的另一个进程，已与主机上的所有其他进程隔离。这种隔离利用了Linux上已有很长时间的内核名称空间和cgroups。

什么是容器镜像

什么是容器图片？🔗
运行容器时，它使用隔离的文件系统。此自定义文件系统由容器映像提供。由于该映像包含容器的文件系统，因此它必须包含运行应用程序所需的所有内容-所有依赖项，配置，脚本，二进制文件等。该映像还包含该容器的其他配置，例如环境变量，要运行的默认命令，和其他元数据。？


#### cli参考(https://docs.docker.com/engine/reference/run/)
- docker version(https://docs.docker.com/engine/reference/commandline/version/)
- docker run(https://docs.docker.com/engine/reference/commandline/run/)
- docker image(https://docs.docker.com/engine/reference/commandline/image/)
- docker container(https://docs.docker.com/engine/reference/commandline/container/)

Command	Description
- docker attach	将本地标准输入，输出和错误流附加到正在运行的容器
- docker build	从Dockerfile构建映像
- docker builder	管理构建
- docker checkpoint	管理检查点
- docker commit	根据容器的更改创建新图像
- docker config	管理Docker配置
- docker container	管理容器
- docker context	管理上下文
- docker cp	在容器和本地文件系统之间复制文件/文件夹
- docker create	创建一个新的容器
- docker diff	检查容器文件系统上文件或目录的更改
- docker events	从服务器获取实时事件
- docker exec	在正在运行的容器中运行命令
- docker export	将容器的文件系统导出为tar存档
- docker history	显示图像的历史记录
- docker image	管理图片
- docker images	列出图片
- docker import	从tarball导入内容以创建文件系统映像
- docker info	显示系统范围的信息
- docker inspect	返回有关Docker对象的低级信息
- docker kill	杀死一个或多个正在运行的容器
- docker load 从tar存档或STDIN加载图像
- docker login	登录Docker注册表
- docker logout	从Docker注册表注销
- docker logs	获取容器的日志
- docker manifest	管理Docker映像清单和清单清单
- docker network	管理网络
- docker node	管理Swarm节点
- docker pause	暂停一个或多个容器中的所有进程
- docker plugin	管理插件
- docker port 列出端口映射或容器的特定映射
- docker ps	列出容器
- docker pull 从注册表中提取图像或存储库
- docker push	将映像或存储库推送到注册表
- docker rename	重命名容器
- docker restart	重新启动一个或多个容器
- docker rm	删除一个或多个容器
- docker rmi	删除一个或多个图像
- docker run	在新容器中运行命令
- docker save	将一个或多个图像保存到tar存档（默认情况下流式传输到STDOUT）
- docker search	在Docker Hub中搜索图像
- docker secret	管理Docker机密
- docker service	管理服务
- docker stack	管理Docker堆栈
- docker start	启动一个或多个已停止的容器
- docker stats	显示容器资源使用情况统计信息的实时流
- docker stop	停止一个或多个运行中的容器
- docker swarm	管理群
- docker system	管理Docker
- docker tag	创建一个引用了SOURCE_IMAGE的标签TARGET_IMAGE
- docker top	显示容器的运行过程
- docker trust	管理对Docker映像的信任
- docker unpause	取消暂停一个或多个容器中的所有进程
- docker update	更新一个或多个容器的配置
- docker version	显示Docker版本信息
- docker volume	管理卷
- docker wait	Block 阻塞直到一个或多个容器停止，然后打印其退出代码


#### DockerFile

Docker可以通过阅读Docker中的指令来自动构建映像 Dockerfile。A Dockerfile是一个文本文档，其中包含用户可以在命令行上调用以组装图像的所有命令。

使用docker build 用户可以创建自动构建，该构建连续执行多个命令行指令。

本页描述您可以在中使用的命令Dockerfile。阅读完此页面后，请参考Dockerfile最佳实践以获取有关技巧的指南

构建上下文是递归处理的。因此，aPATH包括任何子目录，并且a包括URL存储库及其子模块。本示例显示了一个使用当前目录（.）作为构建上下文的构建命令：

    docker build .

构建是由Docker守护程序而不是CLI运行的。构建过程要做的第一件事是将整个上下文（递归）发送到守护程序。在大多数情况下，最好从空目录开始作为上下文，并将Dockerfile保留在该目录中。仅添加构建Dockerfile所需的文件。

**警告**

    不要将根目录/用作PATH构建上下文，因为它会导致构建将硬盘驱动器的全部内容传输到Docker守护程序。

以使用-f标志withdocker build指向文件系统中任何位置的Dockerfile。

    docker build -f /path/to/a/Dockerfile .

如果构建成功，则可以指定存储新映像的存储库和标记：

    docker build -t shykes/myapp .

要在构建后将映像标记到多个存储库中，请在-t运行build命令时添加多个参数：

    docker build -t shykes/myapp:1.0.2 -t shykes/myapp:latest .

默认情况下，构建缓存基于要构建的计算机上先前构建的结果。该--cache-from选项还允许您使用通过映像注册表分发的构建缓存，请参考命令参考 中的“ 指定外部缓存源”部分docker build。

完成构建后，您就可以考虑使用扫描映像docker scan并将其推送到Docker Hub了。

##### DockerFile 格式

    # Comment
    INSTRUCTION arguments
该指令不区分大小写。但是，惯例是将它们大写以更轻松地将它们与参数区分开。

DockerDockerfile按顺序运行指令。
一个Dockerfile
必须以**开始FROM的指令**。

    这可能在解析器指令，注释和全局范围的 ARG之后。该FROM指令指定要从中构建父图像。FROM只能在一个或多个ARG指令之前，这些指令声明在中的FROM行中使用的参数Dockerfile。

docker以#作为注释，  
    除非该行是一个有效的解析器指令。#一行中其他任何地方的标记都被视为参数。这允许如下语句  注释中不支持换行符。

    # Comment
    RUN echo 'we are running some # of cool things'

解析器指令
解析器指令是可选的，并且会影响Dockerfile处理a中后续行的方式。解析器指令不会在构建中添加图层，也不会显示为构建步骤。
解析器指令以形式写为特殊类型的注释**# directive=value**。单个指令只能使用一次。

处理完注释，空行或生成器指令后，Docker不再寻找解析器指令。而是将格式化为解析器指令的任何内容都视为注释，并且不会尝试验证它是否可能是解析器指令。因此，所有解析器指令必须位于的最顶部Dockerfile。

解析器指令不区分大小写。但是，约定是小写的。约定还应在任何解析器指令之后包含一个空白行。解析器指令不支持行继续符。

自定义Dockerfile实现使您能够：

自动获取错误修正，而无需更新Docker守护程序
确保所有用户都使用相同的实现来构建您的Dockerfile
使用最新功能而无需更新Docker守护程序
在将新功能或第三方功能集成到Docker守护程序中之前，先对其进行尝试
使用替代的构建定义，或创建自己的构建定义


##### 编写Dockerfile的最佳实践

Docker映像由只读层组成，每个只读层代表一个Dockerfile指令。这些层是堆叠的，每个层都是与上一层相比变化的增量。感受一下Dockerfile：

    # syntax=docker/dockerfile:1
    FROM ubuntu:18.04
    COPY . /app
    RUN make /app
    CMD python /app/app.py

每条指令创建一层：

- FROM从ubuntu:18.04Docker映像创建一个图层。
- COPY 从Docker客户端的当前目录添加文件。
- RUN使用构建您的应用程序make。
- CMD 指定在容器中运行什么命令。


运行图像并生成容器时，可以 在基础层之上添加一个新的可写层（“**容器层**”）。对运行中的容器所做的所有更改（例如写入新文件，修改现有文件和删除文件）都将写入此薄可写容器层。

有关图像层（以及Docker如何构建和存储图像）的更多信息，请参阅 关于存储驱动程序。

一般准则和建议

您定义的图片Dockerfile应生成尽可能短暂的容器。“短暂”是指可以停止并销毁容器，然后对其进行重建和替换，并采用绝对的最低限度的设置和配置。


##### 为java创建

为应用程序创建Dockerfile的步骤。在工作目录的根目录中，创建一个名为的Dockerfile文件，然后在文本编辑器中打开该文件。

Dockerfile的名称并不重要，但是许多命令的默认文件名都是Dockerfile。因此，在本系列中，我们将其用作文件名




