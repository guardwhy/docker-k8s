## 1-容器化和虚拟化

Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中,然后发布到任何流行的Linux机器或Windows 机器上,也可以实现虚拟化。

### 1.1 虚拟化

1、在最早的时候，我们想要在线上部署一个应用。我们需要先购买服务器，然后安装操作系统及各种依赖环境，最后进行应用的部署。

2、存在问题

- 部署应用上线应用过程时间非常长
- 购买服务器的花费不菲
- 物理服务器的资源容易浪费
- 迁移和扩展比较困难

3、解决方案:

通过虚拟化技术，可以解决以上问题，==虚拟化技术就是在操作系统上多加了一个虚拟化层(Hypervisor），可以将物理机的CPU、内存、硬盘、网络等资源进行虚拟化，再通过虚拟化出来的空间上安装操作系统，构建虚拟的应用程序执行环境==，这就是通常说的虚拟机，比如：VMware 、VirtualBox等软件。

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606123000.png" style="zoom:80%;" />

4、虚拟化技术的优点

- 提升IT效率，降低运维成本。
- 更快地部署工作负责，提高应用性能。
- 提高服务器可用性，消除服务器梳理剧增情况和复杂性。

5、虚拟机的缺点

- 占用资源较多，性能较差。
- 扩展能力较差，环境迁移能力较差。

因此，结合以上特点，容器化技术诞生了。

### 1.2 容器化

容器化起源集装箱。集装箱 ——全球物流系统中一个非常重要的发明。在运输之前一次性将货物封装好到集装箱里面，之后的集装箱直接放到卡车、火车、货轮上，而且集装箱是统一标准的，自然容易机械化，因此集装箱的革命，节省了大量的资源、物流成本大大降低。

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606124018.png)

容器不是模拟一个完整的操作系统，而是对进程进行隔离。有了容器，就可以将软件运行所需的所有资源打包到一个隔离的容器中。容器与虚拟机不同，不需要捆绑一整套操作系统，只需要软件工作所需的库资源和设置。系统因此而变得高效轻量并保证部署在任何环境中的软件都能始终如一地运行。

容器特点: 

- 容器共享宿主机内核。
- 容器使用内核的功能对进程进行分组和资源限制。
- 容器通过命名空间保证隔离。
- 容器像是轻量级的VM（占用空间更少，速度更快），但不是虚拟机。

> 容器化和传统虚拟化对比

传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整操作系统，在该系统上再运行所需应用进程。
而容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核，而且也没有进行硬件虚拟。
因此容器要比传统虚拟机更为轻便。每个容器之间互相隔离，每个容器有自己的文件系统 ，容器之间进程不会相互影响，能区分计算资源。

## 2- Docker概述

### 2.1 什么是Docker

官网地址: [http://www.docker.com](http://www.docker.com)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606134629.png)

文档地址: [https://docs.docker.com/](https://docs.docker.com/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606134842.png)

Docker Hub官网: [https://hub.docker.com/](https://hub.docker.com/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606135102.png)

1、Docker开源项目背景

Docker是基于Go语言实现的开源容器项目，诞生于2013年年初，最初发起者是dotCloud公司(Docker Inc)，Docker项目已加入了Linux基金会，并遵循Apache2.0协议，全部开源代码均在[https://github.com/docker/docker](https://github.com/docker/docker)上进行维护。Docker的构想是要实现“Build，Ship and Run Any App， Anywhere”，即通过对应用的封装(Packaging)，分发(Distribution)，部署(Deployment)，运行（Runtime）生命周期进行管理，达到应用组件==一次封装，到处运行==的目的。这里的应用组件，既可以是一个Web应用、一个编译环境，也可以是一套数据库平台服务，甚至是一个操作系统或集群。
Docker首次为应用的开发、运行和部署提供了“一站式”的实用解决方案。

2、Linux容器技术（LXC）

早期的Docker是基于Linux容器技术（Linux Containers，LXC）的。最早的容器技术可以追溯到1982 年Unix系列操作系统上的chroot工具(直到今天，主流的Unix、Linux操 作系统仍然支持和带有该工具）。早期的容器实现技术包括Sun Solaris 操作系统上的Solaris Containers（2004年发布），FreeBSD操作系统上的 FreeBSD jail（2000年左右出现），以及GNU/Linux上的Linux-VServer和 OpenVZ。

3、从Linux容器到Docker

在LXC的基础上，Docker进一步优化了容器的使用体验，Docker提供了各种容器管理工具（如分发、版本、移植等）让用户无需关注底层的操作，可以更
简单明了地管理和使用容器，Docker通过引入分层文件系统构建（aufs）和高效的镜像机制，降低了迁移难度，极大地提升了用户体验。
自0.9版本开始，Docker 开发了libcontainer项目，作为更广泛的容器驱动实现，从而替换掉了LXC的实现。

### 2.2 Docker的应用场景

快速，一致地交付应用程序、镜像打包环境，避免了环境不一致的问题 Docker可以为开发人员提供 标准化 的本地工作环境给应用程序和服务，从而简化了开发生命周期。容器非常适合持续集成和持续交付(CI / CD)工作流程。

1、响应式部署和扩展

Docker是基于容器的平台允许高度可移植的工作负载。Docker容器可以在开发人员的本地笔记本电脑上，数据中心中的物理或虚拟机上，云提供商上或混合环境中运行。 Docker的可移植性和轻量级的特性还使可以轻松地动态管理工作负载，并根据业务需求指示实时扩展或拆除应用程序和服务。

2、在同一个硬件上运行更多工作负载

Docker轻巧快速。它为基于虚拟机管理程序的虚拟机提供了可行，经济高效的替代方案，因此我们可以利用更多的计算能力来实现业务目标。Docker非常适合于高密度环境以及中小型部署，而需要用更少的资源做更多的事情。

### 2.3 为什么要使用Docker

**更快速的应用交付和部署**：

传统方式: 一堆帮助文档，安装程序！！

Docker : 打包镜像发布测试，一键运行。

**更便捷的升级和扩缩容**：

使用了Docker之后，部署应用就和搭积木一样！！

项目打包为一个镜像，扩展 服务器A，服务器B！

**更简单的系统运维**：

在容器化之后，开发，测试环境都是高度一致的。

**更高效的计算资源利用**：

Docker是内核级别的虚拟化，可以在一个物理机上运行很多的容器实例，服务器的性能可以压榨到极致。

### 2.4 Docker与虚拟机比较

Docker是一种轻量级的虚拟化方式与传统虚拟机技术的特性比较如下表:

| 特 性    | 容 器              | 虚 拟 机   |
| -------- | ------------------ | ---------- |
| 启动速度 | 秒级               | 分钟级     |
| 性能     | 接近原生           | 较弱       |
| 内存代价 | 很小               | 较多       |
| 硬盘使用 | 一般为MB           | 一般为GB   |
| 运行密度 | 单机支持上千个容器 | 一般几十个 |
| 隔离性   | 安全隔离           | 完全隔离   |
| 迁移性   | 优秀               | 一般       |

传统的虚拟机方式提供的是相对封闭的隔离。Docker利用Linux系统上的多种防护技术实现了严格的隔离可靠性，并且可以整合众多安全工具。从 1.3.0版本开始，Docker重点改善了容器的安全控制和镜像的安全机制， 极大提高了使用Docker的安全性。

## 3- Docker快速实战

### 3.1 Docker的基本组成

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606152424.png" style="zoom: 80%;" />

> **Docker引擎**

Docker使用客户端-服务器架构，Docker客户端是用户与Docker交互的主要方式，与Docker守护进程（Docker引擎）进行通信该守护进程完成了构建，运行和分发Docker容器的繁重工作。

Docker客户端和守护程序可以在同一系统上运行，也可以将Docker客户端连接到远程Docker守护程序。Docker客户端和守护程序在UNIX套接字或网络接口上使用REST API进行通信。Docker守护进程侦听Docker API请求并管理Docker对象，例如镜像，容器，网络和卷等。守护程序还可以与其他守护程序通信以管理Docker服务。

> **Docker镜像**

Docker镜像类似于虚拟机镜像，可以将它理解为一个只读的模板。镜像是基于联合（Union）文件 系统的一种层式的结构，由一系列指令一步一步构建出来。

镜像是创建Docker容器的基础。通过版本管理和增量的文件系统， Docker提供了一套十分简单的机制来创建和更新现有的镜像，用户可以从网上下载一个已经做好的应用镜像，并直接使用。

> **Docker容器**

Docker利用容器技术，独立运行一个或者一个组应用，通过镜像来创建的，启动，停止，删除，基本命令！！目前就可以把这个容器理解为就是一个简易的linux系统。

> **Docker仓库**

仓库就是存放镜像的地方，仓库分为公有仓库和私有仓库，目前，最大的公开仓库是 官方提供的Docker Hub，其中存放了数量庞大的镜像供用户下载。国内不少云服务提供商（如时速云、阿里云等）也提供了仓库的本地源，可以提供稳定的国内访问。Docker也支持用户在本地网络内创建一个只能自己访问的私有仓库。

### 3.2 Docker安装前置条件

1、硬件安装要求

| 序号 | 硬件      | 基本要求                               |
| ---- | --------- | -------------------------------------- |
| 1    | cpu       | 推荐2核                                |
| 2    | 内存      | 至少2G                                 |
| 3    | 硬盘      | 至少50G                                |
| 4    | centOS7.8 | docker及K8S集群推荐各使用centos7.8版本 |

2、查看centos系统版本命令

```shell
cat /etc/centos-release
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210613102936.png)

3、配置阿里云yum源

```shell
1.下载安装wget
yum install -y wget

2.备份默认的yum
mv /etc/yum.repos.d /etc/yum.repos.d.backup

3.设置新的yum目录
mkdir -p /etc/yum.repos.d

4.下载阿里yum配置到该目录中，选择对应版本
wget -O /etc/yum.repos.d/CentOS-Base.repo \http://mirrors.aliyun.com/repo/Centos-7.repo

5.更新epel源为阿里云epel源
mv /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel.repo.backup
mv /etc/yum.repos.d/epel-testing.repo /etc/yum.repos.d/epel-testing.repo.backup
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo

6.重建缓存
yum clean all
yum makecache
```

4、升级Linux系统内核

```shell
1、rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm 
2、yum --enablerepo=elrepo-kernel install -y kernel-lt 
3、grep initrd16 /boot/grub2/grub.cfg 
4、grub2-set-default 0
5、重启系统: reboot
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210613110040.png)

5、查看centos系统内核

```shell
uname -r
uname -a
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210613110406.png)

6、使用docker一定需要连接网络才能操作。

```shell
## firewalld的基本使用
启动: systemctl start firewalld

关闭: systemctl stop firewalld

查看状态: systemctl status firewalld 

开机禁用: systemctl disable firewalld

开机启用: systemctl enable firewalld
```

7、yum安装gcc相关环境

```shell
yum -y install gcc
yum -y install gcc-c++
```

### 3.3 安装docker

Docker在主流的操作系统和云平台上都可以使用，包括Linux操作 系统（如Ubuntu、Debian、CentOS、Redhat等）、MacOS操作系统和 Windows操作系统，以及AWS等云平台。

1、卸载旧版本的docker(如果没有安装过，请忽略)

```shell
yum remove docker \
        docker-client \
        docker-client-latest \
        docker-common \
        docker-latest \
        docker-latest-logrotate \
        docker-logrotate \
        docker-engine
```

2、yum 包更新到最新

```shell
yum update
```

3、安装需要的软件包，提供yum-config-manager功能，另外两个是devicemapper驱动依赖的。

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
```

4、设置yum源为阿里云

```shell
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

5、安装docker

```shell
安装最新版：推荐大家安装最新版本
yum -y install docker-ce
安装指定版本：
语法规则：yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING>
containerd.io
yum -y install docker-ce-18.06.3.ce-3.el7 docker-ce-cli.x86_64
yum install -y docker-ce-19.03.9-3.el7 docker-ce-cli-19.03.9-3.el7 
```

6、安装后查看docker版本

```shell
docker -v
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606162555.png" style="zoom:80%;" />

### 3.4 卸载docker

1、查询docker安装过的包：

```shell
yum list installed | grep docker
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210613212904.png)

2、删除安装包：

```shell
systemctl stop docker
yum - y remove docker-ce.x86_64 docker-ce-cli.x86_64 docker-ce-rootless-extras.x86_64  docker-scan-plugin.x86_64 
```

3、删除镜像/容器

```shell
rm -rf /var/lib/docker
```

### 3.5 阿里云镜像加速

1、先注册一个阿里云账号。

2、查看阿里云，官方文档: [https://cr.console.aliyun.com/cn-qingdao/instances/mirrors](https://cr.console.aliyun.com/cn-qingdao/instances/mirrors)

3、进入管理控制台设置密码，开通。

4、查看属于自己的加速器

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606163908.png" style="zoom:80%;" />

5、配置镜像加速

可以通过修改`daemon`配置文件`/etc/docker/daemon.json`来使用加速器。

```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://5bsomu6l.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

6、测试 HelloWorld

```shell
docker run hello-world
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606201506.png" style="zoom: 80%;" />

7、查看`hello world`的镜像

```shell
[root@Linux ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
hello-world   latest    d1165f221234   3 months ago   13.3kB
centos        7         8652b9f0cb4c   6 months ago   204MB
```

8、`run`主要干了啥?

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607083828.png" style="zoom:80%;" />

### 3.6 Docker基本操作

1、启动docker

```shell
systemctl start docker
```

2、停止docker

```shell
systemctl stop docker
```

3、重启docker、

```shell
systemctl restart docker
```

4、查看docker状态

```shell
systemctl status docker
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606165157.png)

5、开机启动

```shell
systemctl enable docker
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606165947.png)

6、开机不自启

```shell
systemctl unenable docker
```

7、查看docker概要信息

```shell
docker info
```

8、查看docker帮助文档

```shell
docker –help
```

9、查看日志

```shell
docker logs -f 镜像名
```

### 3.7 Docker底层原理

> **Docker是怎么工作的**

Docker是一个Client-Server结构的系统，Docker守护进程运行在主机上， 然后通过Socket连接从客户端访问，守护进程从客户端接受命令并管理运行在主机上的容器。 容器，是一个运行时环境，就是我们前面说到的集装箱。

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607085318.png)

> **为什么Docker比较 VM 快？**

1、Docker有着比虚拟机更少的抽象层。

2、docker利用的是宿主机的内核，VM需要是Guest OS。

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607094050.png" style="zoom:80%;" />

所以说，新建一个容器的时候，docker不需要想虚拟机一样重新加载一个操作系统内核，避免引导。虚拟机是加载`Guest OS`分级别的，而docker是利用宿主机的操作系统么？省略了这个复杂的过程，妙极了。。。

## 4-Docker镜像操作

### 4.1 查看镜像信息

1、基本语法

```shell
docker images
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606170803.png)

- `REPOSITORY`：镜像名称 
- `TAG`：镜像标签 （==默认是可以省略的,也就是latest==）
- `IMAGE ID`：镜像ID 
- `CREATED`：镜像的创建日期（不是获取该镜像的日期） 
- `SIZE`：镜像大小 这些镜像都是存储在

注意: Docker宿主机的`/var/lib/docker`目录下

### 4.2 搜素镜像

1、如果你需要从网络中查找需要的镜像，可以通过以下命令搜索

```shell
docker search 镜像名称
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606171302.png)

- `NAME`：仓库名称
- `DESCRIPTION`：镜像描述
- `STARS`：用户评价，反应一个镜像的受欢迎程度
- `OFFICIAL`：是否官方
- `AUTOMATED`：自动构建，表示该镜像由Docker Hub自动构建流程创建的

### 4.3.拉取镜像

1、拉取镜像就是从中央仓库中下载镜像到本地，执行命令`docker pull 镜像名称`

```shell
例如，我要下载centos7镜像
docker pull centos:7
#如果不指定版本号，下载最新版本
docker pull centos 
docker pull centos:latest
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606175043.png)

### 4.4 删除镜像

按镜像ID删除镜像

```shell
docker rmi 镜像ID
docker rmi 镜像名称
docker rmi `docker images -q` 删除所有镜像（谨慎操作）
```

## 5-Docker容器操作

### 5.1 查看容器

1、查看最后一次运行的容器

```shell
docker ps -l
```

2、查看运行容器

```shell
docker ps
```

3、查看所有容器

```shell
docker ps -a
```

4、进入容器，其中字符串为容器ID

```shell
docker exec -it ecc704d85084 /bin/bash
```

5、停用全部运行中的容器

```shell
docker stop $(docker ps -q)
```

6、删除全部容器

```shell
docker rm $(docker ps -aq)
```

7、一条命令实现停用并删除容器

```shell
docker stop $(docker ps -q) & docker rm $(docker ps -aq)
```

8、查看容器的ip地址

```shell
docker inspect --format='{{.NetworkSettings.IPAddress}}' 容器ID
```

### 5.2 创建容器

1、创建容器命令：`docker run`

案例说明: `docker run -di --name myredis2 -p 6666:6379 redis`

```shell
 -i：表示运行容器
 -t：表示容器启动后会进入其命令行。加入这两个参数后，容器创建就能登录进去。即分配一个伪终端。
--name :为创建的容器命名。
-v：表示目录映射关系（前者是宿主机目录，后者是映射到容器上的目录），可以使用多个-v做多个目录或文件映射。注意：最好做目录映射，在宿主机上做修改，然后共享到容器上。
-d：在run后面加上-d参数,则会创建一个守护式容器在后台运行（这样创建容器后不会自动登录容器，如果只加-i -t两个参数，创建后就会自动进去容器）。
-p：表示端口映射，前者是宿主机端口，后者是容器内的映射端口。可以使用多个-p做多个端口映射
```

2、交互式方式创建容器(==创建以后就进入到容器内部了==)

基本语法: `docker run -it --name=容器名称 镜像名称:标签 /bin/bash`

```shell
通过ps命令查看，发现可以看到启动的容器，状态为启动状态
```

3、守护式方式创建容器

基本语法: `docker run -di --name=容器名称 镜像名称:标签`

```shell
登录守护式容器方式：
docker exec -it 容器名称 (或者容器ID)  /bin/bash
```

### 5.3 启动、停止、删除容器

1、停止容器

```shell
docker stop 容器名称(或者容器ID)
docker stop 容器名称(或者容器ID),容器名称(或者容器ID)
```

2、重启容器

```shell
docker restart 容器名称(或者容器ID)
docker restart 容器名称(或者容器ID),容器名称(或者容器ID)
```

3、启动容器

```shell
docker start 容器名称（或者容器ID）  
docker start 容器名称（或者容器ID）容器名称（或者容器ID）
```

 注意事项: 出现如下类似错误

```css
COMMAND_FAILED: '/sbin/iptables -t nat -A DOCKER -p tcp -d 0/0 --dport 8111 -j DNAT --to-destination 172.17.0.6:8111 ! -i docker0' failed: iptables: No chain/target/match by that name.
```

==如果启动容器出错，把网卡重新设置如下：==

```python
pkill docker

iptables -t nat -F

ifconfig docker0 down

brctl delbr docker0

systemctl start docker 

-- 重启docker后解决
```

4、删除容器

注意事项: 如果删除一个容器，==必须这个容器是停止状态，然后删除==，也就说你无法删除一个运行中的容器。

```shell
docker rm 容器名称(或者容器ID)
docker rm 容器名称(或者容器ID) 容器名称(或者容器ID)
docker rm -f $(docker ps -aq) # 删除所有的容器
docker ps -a -q|xargs docker rm #删除所有的容器
```

### 5.4 退出容器

```shell
exit #直接容器停止并且退出
Ctrl + p + Q #容器不停止退出
```

### 5.5 查询启动日志

```shell
docker logs -f -t --tail 容器id(容器名字)
# 显示日志
-tf #显示日志
--tail number #要显示日志条数
```

### 5.6 查询进程信息

```shell
# 基本命令
docker top 容器id
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607112734.png)

### 5.7 查看容器元数据

```shell
# 命令
docker inspect 容器id
```

查看结果

```shell
# 测试
[root@Linux ~]# docker inspect 76add8b5c428
[
    {
    	# 完整的id，有意思啊，这里上面的容器id，就是截取的这个id前几位！
        "Id": "76add8b5c428721e78f270f1cb963e50d170d891da8631965602279fbf868a1b",
        "Created": "2021-06-07T02:46:39.211261839Z",
        "Path": "docker-entrypoint.sh",
        "Args": [
            "redis-server",
            "/usr/local/etc/redis/redis.conf"
        ],
        # 状态
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 4680,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2021-06-07T02:46:40.188362039Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
       // ...........
]
```

### 5.8 进入正在运行的容器

方式一: `docker exec -it 容器id bashShell`

```shell
docker exec -it 76add8b5c428 /bin/bash
```

方式二：`docker attach 容器id`

```shell
docker attach 76add8b5c428
```

两种方式区别: 

exec  是在容器中打开新的终端，并且可以启动新的进程。

attach 直接进入容器启动命令的终端，不会启动新的进程。

### 5.9 拷贝文件

1、从容器内拷贝文件到主机上: `docker cp 容器id:容器内路径 目的主机路径`

```shell
## 进入docker容器内部
[root@Linux ~]# docker exec -it c219f694d74d /bin/bash
[root@c219f694d74d /]# ls
anaconda-post.log  dev  home  lib64  mnt  proc  run   srv  tmp  var
bin                etc  lib   media  opt  root  sbin  sys  usr
[root@c219f694d74d /]# cd /home/
[root@c219f694d74d home]# ls
# 在容器内创建一个文件
spring.java
[root@c219f694d74d home]# exit
exit
# 将这文件拷贝出到主机上
[root@Linux ~]# docker cp c219f694d74d:/home/spring.java /home
[root@Linux ~]# cd /home/
[root@Linux home]# ls
abc.log  abc.txt  guardwhy  james  Java  mycal  my.sh  spring.java
[root@Linux home]# 
```

### 5.10 可视化窗口

1、**Portainer是Docker的图形化管理工具**，提供状态显示面板、应用模板快速部署、容器镜像网络数据卷的基本操作（包括上传下载镜像，创建容器等操作）、事件日志显示、容器控制台操作、Swarm集群和服务等集中管理和操作、登录用户管理和控制等功能。功能十分全面，基本能满足中小型单位对容器管理的全部需求。如果仅有一个docker宿主机，则可使用单机版运行，Portainer单机版运行十分简单，只需要一条语句即可启动容器，来管理该机器上的docker镜像、容器等数据。

```shell
docker run -d -p 8088:9000 \
--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607205455.png)

2、开启8088:9000端口，打开防火墙。

```shell
firewall-cmd --zone=public --add-port=8000/tcp --permanent
firewall-cmd --zone=public --add-port=9000/tcp --permanent
firewall-cmd --reload
```

3、查看所有开启的端口

```shell
firewall-cmd --list-ports
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607210239.png)

4、访问方式: [http://192.168.50.128:8088/](http://192.168.50.128:8088/)

5、首次登陆需要注册用户，给`guardwhy`用户设置密码。

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607210539.png" style="zoom:80%;" />

6、单机版这里选择`local`即可，选择完毕，点击`Connect`即可连接到本地`docker`

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607210709.png" style="zoom:80%;" />

7、登录成功，查看结果！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607213451.png)

## 6-Docker镜像原理

### 6.1 什么是镜像？

镜像是一种轻量级、可执行的独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需的所有内容，包括代码、运行时、库、环境变量和配置文件。所有的应用，直接打包`docker`镜像，就可以直接跑起来！！！

如何得到镜像：

- 从远程仓库进行下载。
- 小伙伴传输给你。
- 自己制作一个镜像DockerFile。

### 6.2 镜像加载原理

> UnionFS(联合文件系统）

UnionFS（联合文件系统）：Union文件系统（UnionFS）是一种分层、轻量级并且高性能的文件系统(类似于Git控制版本)，它支持对文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtual filesystem)。

Union 文件系统是 Docker 镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。
基本特性：一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录。

> Docker镜像加载原理

1、docker的镜像实际上由一层一层的文件系统组成，这个层级的文件系统UnionFS。

2、bootfs(boot file system)【==系统启动需要引导加载==】主要包含bootloader和kernel, bootloader主要是引导加载kernel, Linux刚启动时会加载bootfs文件系统，在==Docker镜像的最底层是bootfs==。这层和典型的Linux/Unix系统是一样的，里面包含boot加载器和内核，当boot加载完成之后整个内核就都在内存中了，这个时候的内存使用权经bootfs转交给内核之后，这个时候系统会卸载bootfs。

3、rootfs (root file system) 在bootfs之上，包含的就是典型 Linux 系统中的`/dev /proc /bin /etc `标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607225652.png)

执行命令：`docker images `，平时安装进虚拟机的`CentOS`都是好几个G，为什么docker images这里才200M？

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210607231017.png)

对于一个精简的OS，rootfs 可以很小，只需要包含最基本的命令，工具和程序库就可以了，因为底层直接用Host的kernel，自己只需要提供rootfs就可以了。由此可见对于不同的linux发行版, bootfs基本是一致的, rootfs会有差别, 因此不同的发行版可以公用bootfs。

==总结：虚拟机是分钟级别的，容器是秒数级别的==。

### 6.3 分层理解

1、分层的镜像

下载一个`MySQL5.7`镜像，观察下载的日志输出，可以看到是一层一层的在下载。

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608100838.png" style="zoom:80%;" />

2、Docker镜像为什么要采用这种分层的结构？

采用这种分层的结构最大的好处是能够资源共享，比如有多个镜像都从相同的Base镜像构建而来，那么宿主机只需在磁盘上保留一份base镜像，同时内存中也只需要加载一份base镜像，这样就可以为所有的容器服务了，而且镜像的每一层都可以被共享。

通过 `docker image inspect` 命令，查看镜像分层！！！

```shell
[root@Linux ~]# docker image inspect mysql:5.7
[
    {
        "Id": "sha256:2c9028880e5814e8923c278d7e2059f9066d56608a21cd3f83a01e3337bacd68",
        "RepoTags": [
            "mysql:5.7"
        ],
        "RepoDigests": [
            "mysql@sha256:a682e3c78fc5bd941e9db080b4796c75f69a28a8cad65677c23f7a9f18ba21fa"
        ],
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:02c055ef67f5904019f43a41ea5f099996d8e7633749b6e606c400526b2c4b33",
                "sha256:14be0d40572c9e789898075dab874a65268de67962d8fd775172b206a9305022",
                "sha256:e82f328cb5e68d3c0fcc6604b3c09a2898d94fde76f589abc5163c85e168a075",
                "sha256:b2abc2ad4a418fb408384c726f800fa1f722cbb38987200cd362bc73f20cc988",
                "sha256:570df12e998cd93e68915a6de7002f9ca1e4b21bbaca3cd1124b7770c800b1b4",
                "sha256:ae477702a51387de5407cbaad4e225c3b3ddfb329cb1b00739b4161fe34d80a6",
                "sha256:3182d4b853f01f95a1cc30cd97c3e5e4d1aa3011ba4cf6273c2d5b38ef1adba0",
                "sha256:940ffd6ceda5ac47aeabf50a3210969f1adce1a78b1dd66dab62c20a2c58caa5",
                "sha256:d329e0888b830d8de863fedf17cb8e600f46ff869b82a43d92499fceb7797bf8",
                "sha256:516d3b88eaf6e98711593913e66d73b14c4438aeec0ca57e6378823e7423ec6d",
                "sha256:8dd710df810d11d75e69cfd8dd0db15ebdd13a667069db0638b9d3168218b3f4"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
```

> **简单说明**

所有的 Docker 镜像都起始于一个基础镜像层，当进行修改或增加新的内容时，就会在当前镜像层之上，创建新的镜像层。

假如基于 Ubuntu 20.04 创建一个新的镜像，这就是镜像的第一层，如果在该镜像中添加 Python3，就会在基础镜像层之上创建第二个镜像层，如果继续添加一个安全补丁，就会创建第三个镜像层。该镜像当前已经包含 3 个镜像层，如下图所示。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608120909.png)

在添加额外的镜像层的同时，镜像始终保持是当前所有镜像的组合，如图所示每个镜像层包含 3 个文件，而镜像包含了来自两个镜像层的 6 个文件。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608140912.png)

下图中展示了一个稍微复杂的三层镜像，在外部看来整个镜像只有 6 个文件，这是因为最上层中的文件7 是文件4的一个更新版本。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608142352.png)

这种情况下，上层镜像层中的文件覆盖了底层镜像层中的文件。这样就使得文件的更新版本作为一个新镜像层添加到镜像当中。Docker 通过存储引擎（新版本采用快照机制）的方式来实现镜像层堆栈，并保证多镜像层对外展示为统一的文件系统

Linux 上可用的存储引擎有 AUFS、Overlay2、Device Mapper、Btrfs 以及 ZFS。每种存储引擎都基于 Linux 中对应的文件系统或者块设备技术，并且每种存储引擎都有其独有的性能特点。Docker 在 Windows 上仅支持 windowsfilter 一种存储引擎，该引擎基于 NTFS 文件系统之上实现了分层和 CoW[1]。

下图展示了与系统显示相同的三层镜像。所有镜像层堆叠并合并，对外提供统一的视图。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608145400.png)

> **特点**

Docker镜像都是只读的，当容器启动时，一个新的可写层被加载到镜像的顶部，这一层就是通常说的容器层，容器之下的都叫镜像层！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608154101.png)

### 6.4 创建镜像

1、docker commit 从容器创建一个新的镜像。

```shell
docker commit 提交容器副本使之成为一个新的镜像！
# 基本语法
docker commit -m="提交的描述信息" -a="作者" 容器id 要创建的目标镜像名:[标签名]
```

2、案例测试

```shell
## 下载tomcat:9.0镜像
[root@Linux ~]# docker pull tomcat:9.0
9.0: Pulling from library/tomcat
d960726af2be: Pull complete 
e8d62473a22d: Pull complete 
8962bc0fad55: Pull complete 
65d943ee54c1: Pull complete 
da20b77f10ac: Pull complete 
8669a096f083: Pull complete 
e0c0a5e9ce88: Pull complete 
f7f46169d747: Pull complete 
42d8171e56e6: Pull complete 
774078a3f8bb: Pull complete 
Digest: sha256:71703331e3e7f8581f2a8206a612dbeedfbc7bb8caeee972eadca1cc4a72e6b1
Status: Downloaded newer image for tomcat:9.0
docker.io/library/tomcat:9.0

## 创建容器
[root@Linux ~]# docker run -di -p 8080:8080 tomcat:9.0
c689c8f890bed8cb67a6f8c5c207013a999a6f97bb16d6e2c928f25d6e0a1329

## 登录守护式容器
[root@Linux ~]# docker exec -it c689c8f890be /bin/bash
root@c689c8f890be:/usr/local/tomcat# ls
BUILDING.txt	 LICENSE  README.md	 RUNNING.txt  conf  logs	    temp     webapps.dist
CONTRIBUTING.md  NOTICE   RELEASE-NOTES  bin	      lib   native-jni-lib  webapps  work
root@c689c8f890be:/usr/local/tomcat# cd webapps
root@c689c8f890be:/usr/local/tomcat/webapps# ls

## 进入tomcat查看cd到webapps下发现全部空的，反而有个webapps.dist里有对应文件，cp -r到webapps下
root@c689c8f890be:/usr/local/tomcat/webapps# cd ../
root@c689c8f890be:/usr/local/tomcat# ls
BUILDING.txt	 LICENSE  README.md	 RUNNING.txt  conf  logs	    temp     webapps.dist
CONTRIBUTING.md  NOTICE   RELEASE-NOTES  bin	      lib   native-jni-lib  webapps  work
root@c689c8f890be:/usr/local/tomcat# cp -r webapps.dist/* webapps
root@c689c8f890be:/usr/local/tomcat# ls
BUILDING.txt	 LICENSE  README.md	 RUNNING.txt  conf  logs	    temp     webapps.dist
CONTRIBUTING.md  NOTICE   RELEASE-NOTES  bin	      lib   native-jni-lib  webapps  work
root@c689c8f890be:/usr/local/tomcat# cd webapps
root@c689c8f890be:/usr/local/tomcat/webapps# ls
ROOT  docs  examples  host-manager  manager
## 退出容器
root@c689c8f890be:/usr/local/tomcat/webapps# exit
exit
##  查看容器的id
[root@Linux ~]# docker ps -l
CONTAINER ID   IMAGE        COMMAND             CREATED          STATUS          PORTS                                       NAMES
c689c8f890be   tomcat:9.0   "catalina.sh run"   15 minutes ago   Up 15 minutes   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   dazzling_chebyshev
[root@Linux ~]# 
```

3、执行结果

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608204629.png)

4、使用容器`c689c8f890be `为模板commit一个tomcat新镜像。

注意：commit的时候，容器的名字不能有大写，否则报错：==invalid reference format==

```shell
docker commit -a="guardwhy" -m="自定义tomcat" c689c8f890be tomcat9:9.1
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608212653.png)

5、关闭以前的tomcat【9.0】，使用新的tomcat【9.1】

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608213620.png)

6、查看执行结果！！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210608204629.png)

## 7-容器数据卷

### 7.1 什么是容器数据卷

1、容器数据卷产生前提

- 将应用和运行的环境打包形成容器运行，运行结果可以伴随着容器，对于数据的要求，我们是希望能够持久化的，假设说你安装一个`redis`，如果把容器删了，就相当于删库跑路，出现以上的问题，我们希望容器之间有可能可以共享数据，Docker容器产生的数据，如果不通过docker commit 生成新的镜像，使得数据作为镜像的一部分保存下来，那么当容器删除后，数据自然也就没有了！
- 为了能保存数据在`Docker`中就可以使用卷！让数据挂载到我们本地！这样数据就不会因为容器删除而丢失了！

2、数据卷基本作用

数据卷就是目录或者文件，存在一个或者多个容器中，由docker挂载到容器，但不属于联合文件系统，因此能够绕过 Union File System ， 提供一些用于持续存储或共享数据的特性。卷的设计目的就是数据的持久化，完全独立于容器的生存周期，因此Docker不会在容器删除时删除其挂载的数据卷。

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210609004317.png)

3、数据卷基本特点

- 数据卷可在容器之间共享或重用数据，卷中的更改可以直接生效。
- 数据卷中的更改不会包含在镜像的更新中。
- 数据卷的生命周期一直持续到没有容器使用它为止。

==总结： 就是容器的持久化，以及容器间的继承和数据共享==！！！

### 7.2 文件拷贝

`docker cp` :用于容器与主机之间的数据拷贝。

1、基本语法

```shell
宿主机文件复制到容器内
docker cp 需要拷贝的文件或目录 容器名称:容器目录

容器内文件复制到宿主机
docker cp 容器名称:容器目录 需要拷贝的文件或目录
```

2、安装`Nginx`镜像

```shell
[root@CentOS ~]# docker pull nginx:1.21.0-alpine
docker.io/library/nginx:1.21.0-alpine

[root@CentOS ~]# docker images
REPOSITORY   TAG             IMAGE ID       CREATED       SIZE
nginx        1.21.0-alpine   a6eb2a334a9f   2 weeks ago   22.6MB
```

3、宿主机文件 copy to 容器内

宿主机的`index.html`页面覆盖容器内的`index.html`页面。

```shell
[root@CentOS ~]# mkdir data
[root@CentOS ~]# cd /home/
[root@CentOS home]# ls
data  guardwhy
[root@CentOS data]# vim index.html 
[root@CentOS data]# cat index.html 
hello,docker!!!!
[root@CentOS data]# pwd
/home/data
[root@CentOS data]# docker cp /home/data/index.html nginx:/usr/share/nginx/html/index.html
[root@CentOS data]# docker ps -a
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                               NAMES
1437f3adacfe   nginx:1.21.0-alpine   "/docker-entrypoint.…"   39 minutes ago   Up 39 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   nginx
[root@CentOS data]# docker exec -it nginx sh
/ # cd /usr/share/nginx/html
/usr/share/nginx/html # ls
50x.html    index.html
/usr/share/nginx/html # cat index.html 
hello,docker!!!!
/usr/share/nginx/html # 
```

执行结果

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210614111909.png)

4、容器内文件`copy to`到宿主机

将容器内的`nginx.cnf`复制到宿主机中。

```shell
[root@CentOS data]# docker cp nginx:/etc/nginx/nginx.conf /home/data
[root@CentOS data]# ls
index.html  nginx.conf
```

将容器内的`nginx`整个目录复制到宿主机中

```shell
[root@CentOS data]# docker cp nginx:/etc/nginx /home/data
[root@CentOS data]# ls
[root@CentOS data]# ls
index.html  nginx  nginx.conf
[root@CentOS data]# cd nginx/
[root@CentOS nginx]# ls
conf.d  fastcgi.conf  fastcgi_params  mime.types  modules  nginx.conf  scgi_params  uwsgi_params
[root@CentOS nginx]# 
```

### 7.3 使用数据卷

> 方式一：直接使用命令挂载 -v

1、基本语法 

```shell
docker run -it -v 宿主机目录:容器内目录 镜像名
```

2、测试容器和宿主机之间数据共享：在容器中，创建的会在宿主机中看到！

```shell
docker run -it -v /home/test:/home centos:7 /bin/bash
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210609015446.png)

3、查看数据卷是否挂载成功: `docker inspect 容器id`

```shell
docker inspect 0fd75c2bddab
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210609020526.png)

4、测试容器停止退出后，主机修改数据是否会同步？

- 停止容器。
- 在宿主机上修改文件，增加些内容。
- 启动刚才停止的容器。
- 然后查看对应的文件，发现数据依旧同步。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210609021332.png)

### 7.4 匿名和具名挂载

#### 7.3.1 匿名卷挂载

1、基本语法`-v 容器内路径`

```shell
docker run -d -P --name nginx01 -v /etc/nginx nginx
```

2、查看卷命令`docker volume ls`， ==匿名挂载的缺点，就是不好维护==。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210609154732.png)

#### 7.3.2 具名卷挂载

1、基本语法: `-v 卷名:/容器内路径`

```shell
docker run -d -P --name nginx02 -v nginxconfig:/etc/nginx nginx
```

2、查看数据卷名

```shell
docker volume ls
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210609162733.png)

3、查看挂载路径

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210609162955.png)

4、总结

所有的docker容器内的卷，没有指定目录的情况下都是在`/var/lib/docker/volumes/????/_data`。

通过具名挂载可以方便的找到自己的数据卷，==大多数情况在使用的是具名挂载==。

```shell
## 如何确定是具名挂载还是匿名挂载，还是指定路径挂载！！
-v 容器内路径 #匿名挂载
-v 卷名:容器内路径 #具名挂载
-v /宿主机路径::容器内路径 #指定路径挂载！！
```

#### 7.3.3 拓展卷挂载

1、通过 `-v`容器内路径， `ro rw`改变读写权限。

```shell
ro:  readonly #只读操作
rw:  readwrite # 可读可写
```

2、一旦这个设置了容器权限，容器对挂载出来的内容就有限定了

```shell
docker run -d -P --name nginx02 -v nginxconfig:/etc/nginx:ro nginx
docker run -d -P --name nginx02 -v nginxconfig:/etc/nginx:rw nginx
```

注意：只要看到`ro`就说明这个路径只能通过宿主机来操作，容器内部是无法操作的。

### 7.5 Docker File初体验

DockerFile 是用来构建Docker镜像的构建文件，是由一些列命令和参数构成的脚本。

1、在宿主机 /home 目录下新建一个 `docker-test-volume`文件夹。

```shell
mkdir docker-test-volume
```

2、进入`docker-test-volume`创建`dockerfile1`

```shell
[root@Linux docker-test-volume]# vim dockerfile1
[root@Linux docker-test-volume]# cat dockerfile1 
FROM centos
# 匿名挂载
VOLUME ["/dockerVolume1", "/dockerVolume2"]
CMD echo "-------end------"
CMD /bin/bash
[root@Linux docker-test-volume]# 
```

3、build后生成镜像，获得一个新镜像 `guardwhy/centos:7`

```shell
docker build -f dockerfile1 -t guardwhy/centos:7 . 
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210609223135.png" style="zoom:80%;" />

4、查看生成的镜像

```shell
[root@Linux docker-test-volume]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
guardwhy/centos     latest              086cf1afb24c        5 minutes ago       209MB
centos              latest              300e315adb2f        6 months ago        209MB
```

5、启动容器

```shell
 docker run -it 086cf1afb24c /bin/bash
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610002318.png" style="zoom:80%;" />

6、在数据卷中新建一个`spring.java`文件

```shell
[root@6c0b413d6544 /]# ls
bin  dockerVolume1  etc   lib	 lost+found  mnt  proc	run   srv  tmp	var
dev  dockerVolume2  home  lib64  media	     opt  root	sbin  sys  usr
[root@6c0b413d6544 /]# cd dockerVolume1
[root@6c0b413d6544 dockerVolume1]# touch spring.java
[root@6c0b413d6544 dockerVolume1]# ls -l
total 0
-rw-r--r--. 1 root root 0 Jun  9 16:36 spring.java
[root@6c0b413d6544 dockerVolume1]# 
```

6、在查看下这个容器的信息，查看卷挂载的路径。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610005141.png)

```shell
[   
    "Mounts": [
    {
    "Type": "volume",
    "Name": "e475a2359f45348bbc991b1518f95d18a9373b8cc878d886b38de35adbf10a22",
    "Source": "/var/lib/docker/volumes/e475a2359f45348bbc991b1518f95d18a9373b8cc878d886b38de35adbf10a22/_data",
    "Destination": "/dockerVolume1",
    "Driver": "local",
    "Mode": "",
    "RW": true,
    "Propagation": ""
    },
    {
    "Type": "volume",
    "Name": "e47420ec9c9fb494119e73eed85e96a8b60f2e66947d0b6cbdf131bf08758ead",
    "Source": "/var/lib/docker/volumes/e47420ec9c9fb494119e73eed85e96a8b60f2e66947d0b6cbdf131bf08758ead/_data",
    "Destination": "/dockerVolume2",
    "Driver": "local",
    "Mode": "",
    "RW": true,
    "Propagation": ""
    }
    ],
]
```

7、测试`spring.java`是否同步！！！

执行命令，查看结果！！！

```shell
cd /var/lib/docker/volumes/e475a2359f45348bbc991b1518f95d18a9373b8cc878d886b38de35adbf10a22/_data
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610010444.png)

### 7.6 数据卷容器

命名的容器挂载数据卷，其他容器通过挂载这个（父容器）实现数据共享，挂载数据卷的容器，称之为数据卷容器。

使用上一步的镜像：`guardwhy/centos` 为模板，运行容器 `centOS01`，`centOS02`，`centOS03`，这些容器都会具有容器卷。

```shell
"/dockerVolume1"
"/dockerVolume2"
```

> **容器间传递共享，多个容器同步数据**

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610123732.png)

1、先启动一个父容器`centOS01`，然后在`dockerVolume1`新增文件。

```shell
docker run -it  --name centOS01 guardwhy/centos
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610014651.png" style="zoom: 67%;" />

退出容器不停止命令：`ctrl+P+Q`

2、创建`centOS02`，让它继承(关键字: `--volumes-from`)`centOS01` 容器，然后在`dockerVolume1`新增文件`spring.java`，分别查看两个容器。

```shell
docker run -it --name centOS02 --volumes-from centOS01 guardwhy/centos
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610113753.png)

进入两个容器中，发现文件同步(实现文件共享)！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610114240.png)

2、创建`centOS03`，让它继承(关键字: `--volumes-from`)`centOS01` 容器，然后在`dockerVolume1`新增文件`SpringMVC.java`，分别查看这三个容器。

```shell
docker run -it --name centOS03 --volumes-from centOS01 guardwhy/centos
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610115530.png)

3、删除容器`centOS1`，查看其它容器还能否访问！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610120626.png)

4、小结

容器之间配置信息的传递，数据卷的生命周期一直持续到没有容器使用它为止，但是一旦持久化到了本地，这个时候本地的数据是不会删除的！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610124917.png)

## 8-DockerFile

### 8.1 什么是DockerFile

`dockerfile`是用来构建Docker镜像的构建文件，是由一系列命令和参数构成的脚本。
构建步骤：

1、编写一个dockerFile文件。

2、docker build 构建成为一个镜像。

3、docker run运行镜像

4、docker push 发布镜像(DockerHub、阿里云镜像仓库)

查看仓库的centOS: [https://hub.docker.com/_/centos](https://hub.docker.com/_/centos)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610141321.png)

点击镜像: [https://github.com/CentOS/sig-cloud-instance-images/blob/b2d195220e1c5b181427c3172829c23ab9cd27eb/docker/Dockerfile](https://github.com/CentOS/sig-cloud-instance-images/blob/b2d195220e1c5b181427c3172829c23ab9cd27eb/docker/Dockerfile)

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610141632.png" style="zoom:80%;" />

小结: ==很多官方镜像都是基础包，很多功能没有，通常我们自己会搭建自己的镜像！！！==

### 8.2 DockerFile构建过程

1、基础知识

- 每条保留字指令都必须为大写字母且后面要跟随至少一个参数。
- 指令按照从上到下，顺序执行
- `#`表示注释。
- 每条指令都会创建一个新的镜像层，并且对镜像进行提交。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610144008.png)

2、步骤流程

- docker从基础镜像运行一个容器，执行一条指令并对容器做出修改。
- 执行类似 docker commit 的操作提交一个新的镜像层。
- Docker再基于刚提交的镜像运行一个新容器。
- 执行dockerfile中的下一条指令直到所有指令都执行完成！

3、具体说明

dockerfile是面向开发的，以后要发布项目，做镜像，就需要编写dockerfile文件。

DockerFile: 构建文件，定义了一切步骤，源代码！！！

DockerImages：在`DockerFile` 定义了一个文件之后，`Docker build` 时会产生一个Docker镜像，当运行Docker 镜像时，会真正开始提供服务。

Docker容器：容器就是镜像运行起来的提供服务器！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610153411.png)

### 8.3 DockerFile指令

**常用指令**

```shell
FROM  # 基础镜像，一切从这里开始构建。
MAINTAINER  # 镜像维护者的姓名混合邮箱地址。
RUN  # 容器构建时需要运行的命令。
ADD  # 步骤，tomcat镜像，这个tomact压缩包！！！添加内容。
WORKDIR  # 镜像的工作目录。
VOLUME # 容器数据卷，用于数据保存和持久化工作，挂载的目录。
EXPOSE # 保留端口配置
CMD # 指定一个容器启动时要运行的命令，只有最后一个会生效，可被替代！！
ENTRYPOINT # 指定一个容器启动时要运行的命令！和CMD一样，可以追加命令！！！
ONBUILD # 当构建一个被继承的DockerFile时运行命令，父镜像在被子镜像继承后，父镜像的ONBUILD被触发。
COPY # 类似ADD，拷贝文件和目录到镜像中！
ENV # 构建的时候设置环境变量。
```

### 8.4 案例说明

Docker Hub 中99% 的镜像都是通过在base镜像(`Scratch`)中安装和配置需要的软件构建出来的。

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610180653.png" style="zoom: 80%;" />

> **自定义一个CentOS镜像**

1、编写DockerFlie文件

查看官方默认的`CentOS`镜像的情况

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610195753.png)

需求实现: 登陆后的默认路径`/home`、安装`vim`编辑器、安装查看网络配置`ifconfig`。

```shell
[root@Linux home]# mkdir dockerfile-test
[root@Linux home]# cd dockerfile-test/
[root@Linux dockerfile-test]# vim mydockerfile-centos # 编辑文件
[root@Linux dockerfile-test]# ls
mydockerfile-centos
[root@Linux dockerfile-test]# cat mydockerfile-centos 
FROM centos
MAINTAINER guardwhy<hxy1625309592@aliyun.com>

ENV MYPATH /home
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools
RUN yum -y install gcc

EXPOSE 80

CMD echo $MYPATH
CMD echo "----------end--------"
CMD /bin/bash
[root@Linux dockerfile-test]# 
```

2、构建镜像

```shell
docker build -f mydockerfile-centos -t centos:7 .
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610220420.png)

3、运行新镜像

```shell
docker run -it centos:7
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610220809.png" style="zoom:80%;" />

可以看到，新镜像已经支持 `vim/ifconfig/gcc`的命令，安装拓展成功！！！

4、列出镜像地的变更历史

基本语法：`docker history 镜像名`

```shell
docker history 70aba9c80bd4
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210610221322.png)

### 8.5 CMD 和 ENTRYPOINT 的区别

**CMD**：指定这个容器的时候要运行的命令，只有最后一个会生效，可被替代。

**ENTRYPOINT**：指定这个容器启动的时候要运行的命令，可以追加命令！！

> **测试CMD**

```shell
# 1、构建dockerfile
[root@Linux dockerfile-test]# vim dockerfile-cmd-test
[root@Linux dockerfile-test]# cat dockerfile-cmd-test 
FROM centos
CMD [ "ls", "-a" ]

# 2、构建镜像
[root@Linux dockerfile-test]# docker build -f dockerfile-cmd-test -t cmdtest .
Sending build context to Docker daemon  3.072kB
Step 1/2 : FROM centos
 ---> 300e315adb2f
Step 2/2 : CMD [ "ls", "-a" ]
 ---> Running in 92d90f5cf57e
Removing intermediate container 92d90f5cf57e
 ---> 31c35ef26b4e
Successfully built 31c35ef26b4e
Successfully tagged cmdtest:latest

# 3、run运行，发现ls -a 命令生效
[root@Linux dockerfile-test]# docker run 31c35ef26b4e
.
..
.dockerenv
bin
dev
etc
home
# 4、希望用 -l 列表展示信息，需要加上 -l参数
[root@Linux dockerfile-test]# docker run 31c35ef26b4e -l
docker: Error response from daemon: OCI runtime create failed: container_linux.go:380: starting container process caused: exec: "-l": executable file not found in $PATH: unknown.
ERRO[0000] error waiting for container: context canceled 

# 5、问题：我们可以看到可执行文件找不到的报错，executable file not found。跟在镜像名后面的是 command，运行时会替换 CMD 的默认值。
# 因此这里的 -l 替换了原来的 CMD，而不是添加在原来的 ls -a 后面。而 -l 根本不是命令，所以自然找不到。

# 6、如果希望加入 -l 这参数，就必须重新完整的输入这个命令：
[root@Linux dockerfile-test]# docker run 31c35ef26b4e ls -al
total 60
drwxr-xr-x.   1 root root 4096 Jun 11 02:36 .
drwxr-xr-x.   1 root root 4096 Jun 11 02:36 ..
-rwxr-xr-x.   1 root root    0 Jun 11 02:36 .dockerenv
lrwxrwxrwx.   1 root root    7 Nov  3  2020 bin -> usr/bin
drwxr-xr-x.   5 root root  340 Jun 11 02:36 dev
drwxr-xr-x.   1 root root 4096 Jun 11 02:36 etc
......
[root@Linux dockerfile-test]# 
```

> **测试ENTRYPOINT**

```shell
# 1、构建dockerfile
[root@Linux dockerfile-test]# vim dockerfile-entrypoint-test
[root@Linux dockerfile-test]# cat dockerfile-entrypoint-test 
FROM centos
ENTRYPOINT [ "ls", "-a" ]

# 2、构建镜像
[root@Linux dockerfile-test]# docker build -f dockerfile-entrypoint-test -t entrypoint-test .
Sending build context to Docker daemon  4.096kB
Step 1/2 : FROM centos
 ---> 300e315adb2f
Step 2/2 : ENTRYPOINT [ "ls", "-a" ]
 ---> Running in a1f66d11b94c
Removing intermediate container a1f66d11b94c
 ---> 5265bb79246a
Successfully built 5265bb79246a
Successfully tagged entrypoint-test:latest

# 3、run运行，发现ls -a 命令生效
[root@Linux dockerfile-test]# docker run 5265bb79246a
.
..
.dockerenv
bin
dev
etc
home
lib
lib64
...
# 4、测试-l参数，发现可以直接使用，这里就是一种追加，可以明显的知道CMD和ENTRYPOINT的区别
[root@Linux dockerfile-test]# docker run 5265bb79246a -l
total 60
drwxr-xr-x.   1 root root 4096 Jun 11 02:43 .
drwxr-xr-x.   1 root root 4096 Jun 11 02:43 ..
-rwxr-xr-x.   1 root root    0 Jun 11 02:43 .dockerenv
lrwxrwxrwx.   1 root root    7 Nov  3  2020 bin -> usr/bin
drwxr-xr-x.   5 root root  340 Jun 11 02:43 dev
drwxr-xr-x.   1 root root 4096 Jun 11 02:43 etc
drwxr-xr-x.   2 root root 4096 Nov  3  2020 home
lrwxrwxrwx.   1 root root    7 Nov  3  2020 lib -> usr/lib
lrwxrwxrwx.   1 root root    9 Nov  3  2020 lib64 -> usr/lib64
.....
[root@Linux dockerfile-test]# 
```

### 8.6 自定义镜像 tomcat

1、创建文件夹，执行以下命令: `mkdir -p guardwhy/tomcat`

2、在上述目录下创建新文件：`touch readme.txt`。

3、将 `jdk` 和 `tomcat` 安装的压缩包拷贝进上一步目录。

4、在`guardwhy/tomcat`目录下新建一个`Dockerfile`文件

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611154608.png)

注意: ==官方命名为`Dockerfile`，build会自动寻找这个文件，就不需要`-f `指定了！！！==

```shell
# vim Dockerfile
FROM centos
MAINTAINER guardwhy<hxy1625309592@aliyun.com>

#把宿主机当前上下文的readme.txt拷贝到容器/usr/local/路径下
COPY readme.txt /usr/local/readme.txt
#把java与tomcat添加到容器中
ADD jdk-8u261-linux-x64.tar.gz /usr/local/
ADD apache-tomcat-9.0.46.tar.gz /usr/local/

#安装vim编辑器
RUN yum -y install vim
#设置工作访问时候的WORKDIR路径，登录落脚点
ENV MYPATH /usr/local
WORKDIR $MYPATH

#配置java与tomcat环境变量
ENV JAVA_HOME /usr/local/jdk1.8.0_261
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.46
ENV CATALINA_BASE /usr/local/apache-tomcat-9.0.46
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin

#容器运行时监听的端口
EXPOSE 8080

#启动时运行tomcat
CMD /usr/local/apache-tomcat-9.0.46/bin/startup.sh && tail -F /usr/local/apache-tomcat-9.0.46/bin/logs/catalina.out
```

5、构建镜像，执行命令` docker build -t diytomcat .`

```shell
[root@Linux tomcat]# docker build -t diytomcat .
Sending build context to Docker daemon  154.6MB
Step 1/15 : FROM centos
 ---> 300e315adb2f
Step 2/15 : MAINTAINER guardwhy<hxy1625309592@aliyun.com>
 ---> Using cache
 ---> 2d8a3df8c6fb
Dependencies resolved.
================================================================================
 Package             Arch        Version                   Repository      Size
================================================================================
Installing:
 vim-enhanced        x86_64      2:8.0.1763-15.el8         appstream      1.4 M
Installing dependencies:
 gpm-libs            x86_64      1.20.7-17.el8             appstream       39 k
 vim-common          x86_64      2:8.0.1763-15.el8         appstream      6.3 M
 vim-filesystem      noarch      2:8.0.1763-15.el8         appstream       48 k
 which               x86_64      2.21-12.el8               baseos          49 k

Transaction Summary
================================================================================
Install  5 Packages

Total download size: 7.8 M
Installed size: 30 M
Downloading Packages:
(1/5): gpm-libs-1.20.7-17.el8.x86_64.rpm        132 kB/s |  39 kB     00:00    
(2/5): vim-enhanced-8.0.1763-15.el8.x86_64.rpm  2.9 MB/s | 1.4 MB     00:00    
(3/5): vim-filesystem-8.0.1763-15.el8.noarch.rp 233 kB/s |  48 kB     00:00    
(4/5): vim-common-8.0.1763-15.el8.x86_64.rpm    9.0 MB/s | 6.3 MB     00:00    
(5/5): which-2.21-12.el8.x86_64.rpm             205 kB/s |  49 kB     00:00    
--------------------------------------------------------------------------------
Total                                           4.7 MB/s | 7.8 MB     00:01     
warning: /var/cache/dnf/appstream-02e86d1c976ab532/packages/gpm-libs-1.20.7-17.el8.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID 8483c65d: NOKEY
CentOS Linux 8 - AppStream                      1.6 MB/s | 1.6 kB     00:00    
Importing GPG key 0x8483C65D:
 Userid     : "CentOS (CentOS Official Signing Key) <security@centos.org>"
 Fingerprint: 99DB 70FA E1D7 CE22 7FB6 4882 05B5 55B3 8483 C65D
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial
Complete!
Successfully built ecc82f059377
Successfully tagged diytomcat:latest
[root@Linux tomcat]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
diytomcat           latest              ecc82f059377        4 minutes ago       638MB
centos              7                   70aba9c80bd4        18 hours ago        451MB
centos              latest              300e315adb2f        6 months ago        209MB
[root@Linux tomcat]# 
```

6、运行启动自定义镜像！

```shell
docker run \
-d -p 9090:8080 --name mydiytomcat \
-v /home/guardwhy/tomcat/test:/usr/local/apache-tomcat-9.0.46/webapps/test \
-v /home/guardwhy/tomcat/tomcat9logs/:/usr/local/apache-tomcat-9.0.46/logs \
--privileged=true diytomcat
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611163103.png)

7、开启端口

开启8080:9000端口，打开防火墙。

```shell
firewall-cmd --zone=public --add-port=8080/tcp --permanent
firewall-cmd --zone=public --add-port=9090/tcp --permanent
firewall-cmd --reload
```

查看所有开启的端口

```shell
firewall-cmd --list-ports
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611162304.png)

8、验证测试访问，链接访问: [http://192.168.50.128:9090/](http://192.168.50.128:9090/)	

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611162556.png)

9、网页发布测试

创建`WEB-INF`文件夹，在文件夹中新建`web.xml`文件

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611172517.png)

**web.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
</web-app>
```

**index.jsp**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>docker</title>
</head>
<body>
    <h3>hello,docker</h3>
    <%
        System.out.println("hello, dockerlogs");
    %>
</body>
</html>
```

执行结果，点击链接: [http://192.168.50.128:9090/test/](http://192.168.50.128:9090/test/)

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611172701.png)

10、查看日志

```shell
[root@Linux tomcat]# ls
apache-tomcat-9.0.46.tar.gz  Dockerfile  jdk-8u261-linux-x64.tar.gz  readme.txt  test  tomcat9logs
[root@Linux tomcat]# cd tomcat9logs/
[root@Linux tomcat9logs]# ls -l
总用量 48
-rw-r-----. 1 root root 16650 6月  11 16:51 catalina.2021-06-11.log
-rw-r-----. 1 root root 16668 6月  11 16:57 catalina.out
-rw-r-----. 1 root root     0 6月  11 16:18 host-manager.2021-06-11.log
-rw-r-----. 1 root root   407 6月  11 16:18 localhost.2021-06-11.log
-rw-r-----. 1 root root  1763 6月  11 16:57 localhost_access_log.2021-06-11.txt
-rw-r-----. 1 root root     0 6月  11 16:18 manager.2021-06-11.log
[root@Linux tomcat9logs]# 
```

### 8.7 发布镜像到阿里云

1、注册阿里云，登录阿里云服务

2、找到容器镜像服务。

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611192435.png" style="zoom:80%;" />

3、创建命名空间

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611192633.png)

4、创建镜像仓库

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611193210.png" style="zoom:80%;" />

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611193248.png" style="zoom:80%;" />

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611193334.png)

5、点击进入这个镜像仓库，可以看到所有的信息

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611193646.png" style="zoom: 67%;" />



> **操作指南**

```shell
1. 登录阿里云Docker Registry
$ docker login --username=tb99****08_88 registry.cn-qingdao.aliyuncs.com
用于登录的用户名为阿里云账号全名，密码为开通服务时设置的密码。

您可以在访问凭证页面修改凭证密码。

2. 从Registry中拉取镜像
$ docker pull registry.cn-qingdao.aliyuncs.com/docker-guardwhy/java-test:[镜像版本号]
3. 将镜像推送到Registry
$ docker login --username=tb99****08_88 registry.cn-qingdao.aliyuncs.com
$ docker tag [ImageId] registry.cn-qingdao.aliyuncs.com/docker-guardwhy/java-test:[镜像版本号]
$ docker push registry.cn-qingdao.aliyuncs.com/docker-guardwhy/java-test:[镜像版本号]
请根据实际镜像信息替换示例中的[ImageId]和[镜像版本号]参数。

4. 选择合适的镜像仓库地址
从ECS推送镜像时，可以选择使用镜像仓库内网地址。推送速度将得到提升并且将不会损耗您的公网流量。

如果您使用的机器位于VPC网络，请使用 registry-vpc.cn-qingdao.aliyuncs.com 作为Registry的域名登录。

5. 示例
使用"docker tag"命令重命名镜像，并将它通过专有网络地址推送至Registry。

$ docker images
REPOSITORY                                                         TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
registry.aliyuncs.com/acs/agent                                    0.7-dfb6816         37bb9c63c8b2        7 days ago          37.89 MB
$ docker tag 37bb9c63c8b2 registry-vpc.cn-qingdao.aliyuncs.com/acs/agent:0.7-dfb6816
使用 "docker push" 命令将该镜像推送至远程。

$ docker push registry-vpc.cn-qingdao.aliyuncs.com/acs/agent:0.7-dfb6816
```

6、测试推送发布

```shell
## 1、登录阿里云
[root@Linux tomcat]# docker login --username=13479915208 registry.cn-qingdao.aliyuncs.com
Password: 
Error response from daemon: Get https://registry.cn-qingdao.aliyuncs.com/v2/: unauthorized: authentication required
[root@Linux tomcat]# clear
[root@Linux tomcat]# docker login --username=13479915208 registry.cn-qingdao.aliyuncs.com
Password: 
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
## 2、设置 tag
[root@Linux tomcat]# docker tag ecc82f059377 registry.cn-qingdao.aliyuncs.com/docker-guardwhy/java-test:v1.0

## 3、推送命令
[root@Linux tomcat]# docker push registry.cn-qingdao.aliyuncs.com/docker-guardwhy/java-test:v1.0
The push refers to repository [registry.cn-qingdao.aliyuncs.com/docker-guardwhy/java-test]
c7510b7d4b11: Pushed 
d6d45250595e: Pushed 
3a1d1e2371ce: Pushed 
70d71810a13c: Pushed 
2653d992f4ef: Pushed 
v1.0: digest: sha256:8baa27772f6fc09c79c5e9d986c397c243c49f601d287b9ee42781e931cae136 size: 1373
[root@Linux tomcat]# 
```

7、小结

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210611223839.png)

## 9-Docker 网络

### 9.1 Docker0初体验

1、清空服务器所有的容器和正在运行的所有镜像

```shell
docker rm -f $(docker ps -a -q)       # 删除所有容器
docker rmi -f $(docker images -qa)      # 删除全部镜像
```

2、查看本地ip，执行命令：`ip addr`

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210612002436.png)

网络端口分析

```shell
1: lo: 127.0.0.1/8  #本机回环地址
2: eth0: 172.17.183.201 #阿里云内网地址
3: docker0: 172.18.0.1 # docker0 地址
```

3、`docker`是如何处理容器间的网络访问的？

```shell
# 启动 mytomcat01
[root@guardwhy ~]# docker run -d -P --name mytomcat01 tomcat
latest: Pulling from library/tomcat
42d8171e56e6: Pull complete 
774078a3f8bb: Pull complete 
Digest: sha256:71703331e3e7f8581f2a8206a612dbeedfbc7bb8caeee972eadca1cc4a72e6b1
Status: Downloaded newer image for tomcat:latest
eb4d1a5d5884ab76d06aaa6b1209d96905f0f822b78ca0ce82bea6a1532c9566

# 查看容器的内部网络地址：ip addr
# 容器启动的时候会得到一个 eth0@if33的IP地址，这是docker分配的！！！
[root@guardwhy ~]# docker exec -it mytomcat01 ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
32: eth0@if33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:12:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.18.0.2/16 brd 172.18.255.255 scope global eth0
       valid_lft forever preferred_lft forever

 
## 宿主机能ping通容器内部！！
[root@guardwhy ~]# ping 172.18.0.2
PING 172.18.0.2 (172.18.0.2) 56(84) bytes of data.
64 bytes from 172.18.0.2: icmp_seq=1 ttl=64 time=0.088 ms
64 bytes from 172.18.0.2: icmp_seq=2 ttl=64 time=0.070 ms
64 bytes from 172.18.0.2: icmp_seq=3 ttl=64 time=0.050 ms
64 bytes from 172.18.0.2: icmp_seq=4 ttl=64 time=0.070 ms
[root@guardwhy ~]# 
```

小结：==docker会给每个容器都分配一个ip，且容器和容器之间是可以互相访问的==。

> **原理分析**

1、每当启动一个`docker`容器，docker就会给docker容器分配一个`ip`，只要安装了docker，就会有一个网卡`docker0`。

2、注意：这是一个桥接模式，使用的技术是`evth-pair`技术。

```shell
## 再次查看主机的 ip addr
[root@guardwhy ~]# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:16:3e:03:c4:87 brd ff:ff:ff:ff:ff:ff
    inet 172.17.183.201/20 brd 172.17.191.255 scope global dynamic eth0
       valid_lft 280172255sec preferred_lft 280172255sec
3: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ff:a3:f7:8a brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.1/16 brd 172.18.255.255 scope global docker0
       valid_lft forever preferred_lft forever
## 本来有三个网络，在启动了1个tomcat容器之后，多了一个if33的网络！！！
33: vethdeea84c@if32: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default 
    link/ether fe:d3:88:7b:b5:85 brd ff:ff:ff:ff:ff:ff link-netnsid 0
[root@guardwhy ~]# 
```

3、每启动一个容器，linux主机就会多了一个虚拟网卡。

```shell
[root@guardwhy ~]# docker run -d -P --name mytomcat02 tomcat
1f2a56ea7754f4c31a7713c840baa5af163a78332bb3a1edcc9e670d3718af3a
[root@guardwhy ~]# docker exec -it mytomcat02 ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
34: eth0@if35: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:12:00:03 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.18.0.3/16 brd 172.18.255.255 scope global eth0
       valid_lft forever preferred_lft forever
## 再次查看主机的 ip addr
[root@guardwhy ~]# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:16:3e:03:c4:87 brd ff:ff:ff:ff:ff:ff
    inet 172.17.183.201/20 brd 172.17.191.255 scope global dynamic eth0
       valid_lft 280169868sec preferred_lft 280169868sec
3: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ff:a3:f7:8a brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.1/16 brd 172.18.255.255 scope global docker0
       valid_lft forever preferred_lft forever
## 本来有三个网络，在启动了2个tomcat容器之后，多了一个if33，if35的网络！！！
33: vethdeea84c@if32: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default 
    link/ether fe:d3:88:7b:b5:85 brd ff:ff:ff:ff:ff:ff link-netnsid 0
35: veth62d856a@if34: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default 
    link/ether 1e:fa:6d:dd:06:12 brd ff:ff:ff:ff:ff:ff link-netnsid 1
[root@guardwhy ~]# 
```

4、小结：

这个容器带来网卡，都是一对一对的。

`veth-pair` 就是一对的虚拟设备接口，它都是成对出现的。一端连着协议栈，一端彼此相连着。

正因为有这个特性，`evth-pair`充当一个桥梁，连接各种虚拟网络设备的。

`OpenStack， Docker`容器之间的连接，OVS的连接，都是使用`evth-pair`的技术。

5、测试mytomcat01和mytomcat02容器间是否可以互相ping通?

```shell
docker exec -it mytomcat02 ping 172.18.0.2
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210612021958.png)

结论：==容器和容器之间是可以互相访问的==。

6、绘制一个网络模型图

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210612104031.png" style="zoom:80%;" />

结论：mytomcat01和tomcat02共用一个路由器(`docker0`)，任何一个容器启动默认都是docker0网络，docker默认会给容器分配一个可用ip。

7、Docker0小结

Docker使用Linux桥接，在宿主机虚拟一个Docker容器网桥(`docker0`)，Docker启动一个容器时会根据Docker网桥的网段分配给容器一个IP地址，称为`Container-IP`，同时Docker网桥是每个容器的默认网关。因为在同一宿主机内的容器都接入同一个网桥，这样容器之间就能够通过容器的Container-IP直接
通信。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210612122123.png)

Docker中的所有网络接口都是虚拟的，虚拟的转发效率高！！(内网传递文件)，只要容器删除，对应网桥一对就没了。。

### 9.2 自定义网络

1、基本命令查看

```shell
docker network --help
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210612134731.png)

2、查看所有网络

```shell
[root@guardwhy ~]# docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
835529da25a3        bridge              bridge              local
12b6d842b3ab        host                host                local
6b4770ba279b        none                null                local
[root@guardwhy ~]# 
```

| 网络模式       | 配置                     | 具体说明                                                     |
| -------------- | ------------------------ | ------------------------------------------------------------ |
| bridge模式     | --net=bridge             | 默认值，在Docker网桥docker0上为容器创建新的网络栈。          |
| none模式       | --net=none               | 不配置网络。                                                 |
| container 模式 | -- net=container:name/id | 容器网络连接！！(用的少！！局限很大)                         |
| host模式       | --net=host               | 容器和宿主机共享Network namespace                            |
| 用户自定义     | --net=自定义网络         | 用户自己使用network相关命令定义网络，创建容器的<br/>时候可以指定为自己定义的网络 |

3、删除原来的所有容器

```shell
[root@guardwhy ~]# docker rm -f $(docker ps -aq)
Remove one or more containers

# 恢复到了最开始的样子
[root@guardwhy ~]# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:16:3e:03:c4:87 brd ff:ff:ff:ff:ff:ff
    inet 172.17.183.201/20 brd 172.17.191.255 scope global dynamic eth0
       valid_lft 280125789sec preferred_lft 280125789sec
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 02:42:ff:a3:f7:8a brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.1/16 brd 172.18.255.255 scope global docker0
       valid_lft forever preferred_lft forever
[root@guardwhy ~]# 
```

注意： 默认创建的容器都是`docker0`网卡

```shell
# docker0网络的特点
1.它是默认的
2.域名访问不通
3.--link 域名通了，但是删了又不行
```

4、使用自定义网络创建容器

查看命令: `docker network create --help`

```shell
[root@guardwhy ~]# docker network create --help

Usage:	docker network create [OPTIONS] NETWORK

Create a network

Options:
      --attachable           Enable manual container attachment
      --aux-address map      Auxiliary IPv4 or IPv6 addresses used by Network driver (default map[])
      --config-from string   The network from which copying the configuration
      --config-only          Create a configuration only network
  -d, --driver string        Driver to manage the Network (default "bridge")
      --gateway strings      IPv4 or IPv6 Gateway for the master subnet
      --ingress              Create swarm routing-mesh network
      --internal             Restrict external access to the network
      --ip-range strings     Allocate container ip from a sub-range
      --ipam-driver string   IP Address Management Driver (default "default")
      --ipam-opt map         Set IPAM driver specific options (default map[])
      --ipv6                 Enable IPv6 networking
      --label list           Set metadata on a network
  -o, --opt map              Set driver specific options (default map[])
      --scope string         Control the network's scope
      --subnet strings       Subnet in CIDR format that represents a network segment
[root@guardwhy ~]# 
```

自定义创建一个网络

```shell
## --driver bridge 桥接
## --subnet 192.168.0.0/16 子网
## --gateway 192.168.0.1  网关
[root@guardwhy ~]# docker network create --driver bridge --subnet 192.168.0.0/16 --gateway 192.168.0.1 mynet
9f140b28095cf395ead5572e3dd5189519380ba3ea8fcd7cdf98e65f25d534f4
[root@guardwhy ~]# docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
835529da25a3        bridge              bridge              local
12b6d842b3ab        host                host                local
9f140b28095c        mynet               bridge              local
6b4770ba279b        none                null                local

# 查看网络，执行命令`docker network inspect mynet`
[root@guardwhy ~]# docker network inspect mynet
[
    {
        "Name": "mynet",
        "Id": "9f140b28095cf395ead5572e3dd5189519380ba3ea8fcd7cdf98e65f25d534f4",
        "Created": "2021-06-12T16:22:33.929558248+08:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {	# 网络
                    "Subnet": "192.168.0.0/16",
                    "Gateway": "192.168.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
[root@guardwhy ~]# 
```

5、自定义两个容器，使用自己的 `mynet`。

```shell
[root@guardwhy ~]# docker run -d -P --name tomcat-net-01 --net mynet tomcat
Digest: sha256:71703331e3e7f8581f2a8206a612dbeedfbc7bb8caeee972eadca1cc4a72e6b1
afa85e96d4f5ded21769674438d3f70b8eda2c1ea229a87e055d23ac49b1a024
[root@guardwhy ~]# docker run -d -P --name tomcat-net-02 --net mynet tomcat
68dabac6d09369bd3f39191bc08b954123cfc177af06aba5263a2e4fd5b6bdaf

## 查看镜像
[root@guardwhy ~]# docker ps 
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS              PORTS                     NAMES
68dabac6d093        tomcat              "catalina.sh run"   About a minute ago   Up About a minute   0.0.0.0:32777->8080/tcp   tomcat-net-02
afa85e96d4f5        tomcat              "catalina.sh run"   About a minute ago   Up About a minute   0.0.0.0:32776->8080/tcp   tomcat-net-01

# 查看网络，执行命令`docker network inspect mynet`
[root@guardwhy ~]# docker network inspect mynet
[
    {
        "Name": "mynet",
        "Id": "9f140b28095cf395ead5572e3dd5189519380ba3ea8fcd7cdf98e65f25d534f4",
        "Created": "2021-06-12T16:22:33.929558248+08:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "192.168.0.0/16",
                    "Gateway": "192.168.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "68dabac6d09369bd3f39191bc08b954123cfc177af06aba5263a2e4fd5b6bdaf": {
                "Name": "tomcat-net-02",
                "EndpointID": "a153fdec599850124a3610716e7e174eb1992079a353cb3903fc00c85465ec20",
                "MacAddress": "02:42:c0:a8:00:03",
                "IPv4Address": "192.168.0.3/16",
                "IPv6Address": ""
            },
            "afa85e96d4f5ded21769674438d3f70b8eda2c1ea229a87e055d23ac49b1a024": {
                "Name": "tomcat-net-01",
                "EndpointID": "0a41c7b5ebf089e9114268891f67df4595e856185543b69c06c3dc39edcbe357",
                "MacAddress": "02:42:c0:a8:00:02",
                "IPv4Address": "192.168.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
[root@guardwhy ~]# 
```

6、测试容器间是否可以互相ping通

```shell
# 1、测试ping连接(ip地址)
[root@guardwhy ~]# docker exec -it tomcat-net-01 ping 192.168.0.3
PING 192.168.0.3 (192.168.0.3) 56(84) bytes of data.
64 bytes from 192.168.0.3: icmp_seq=1 ttl=64 time=0.120 ms
64 bytes from 192.168.0.3: icmp_seq=2 ttl=64 time=0.087 ms
64 bytes from 192.168.0.3: icmp_seq=3 ttl=64 time=0.095 ms
64 bytes from 192.168.0.3: icmp_seq=4 ttl=64 time=0.085 ms

# 2、测试ping连接(容器名)，现在不需要使用--link也可以ping
[root@guardwhy ~]# docker exec -it tomcat-net-01 ping tomcat-net-02
PING tomcat-net-02 (192.168.0.3) 56(84) bytes of data.
64 bytes from tomcat-net-02.mynet (192.168.0.3): icmp_seq=1 ttl=64 time=0.073 ms
64 bytes from tomcat-net-02.mynet (192.168.0.3): icmp_seq=2 ttl=64 time=0.085 ms
[root@guardwhy ~]# 
```

小结: 

自定义的网络docker都已经帮助我们维护好了对应的关系，推荐平时这样使用网络！！！

好处： 

`Redis 、Mysql`- 不同的集群使用不同的网络，保证集群是安全和健康的。

### 9.3 网络连通

1、docker0和自定义网络肯定不通，使用自定义网络的好处就是网络隔离，如何让`tomcat-net-01` 访问 `tomcat1？`

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210612202547.png)

2、案例说明

```shell
# 0、查看现有运行的容器
[root@guardwhy ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
68dabac6d093        tomcat              "catalina.sh run"   4 hours ago         Up 4 hours          0.0.0.0:32777->8080/tcp   tomcat-net-02
afa85e96d4f5        tomcat              "catalina.sh run"   4 hours ago         Up 4 hours          0.0.0.0:32776->8080/tcp   tomcat-net-01

# 1、启动默认的容器，在docker0网络下
[root@guardwhy ~]# docker run -d -P --name tomcat01 tomcat
39506e89093fa3923bfd840d3f9c0223ba09c3a01fce5d000464149b87509563
[root@guardwhy ~]# docker run -d -P --name tomcat02 tomcat
f0a1b251d28519f6360b7340befbd57acb2c974b7cae678b4c0eea6194e7971e

# 2、查看当前的容器
[root@guardwhy ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
f0a1b251d285        tomcat              "catalina.sh run"   8 seconds ago       Up 8 seconds        0.0.0.0:32779->8080/tcp   tomcat02
39506e89093f        tomcat              "catalina.sh run"   18 seconds ago      Up 18 seconds       0.0.0.0:32778->8080/tcp   tomcat01
68dabac6d093        tomcat              "catalina.sh run"   4 hours ago         Up 4 hours          0.0.0.0:32777->8080/tcp   tomcat-net-02
afa85e96d4f5        tomcat              "catalina.sh run"   4 hours ago         Up 4 hours          0.0.0.0:32776->8080/tcp   tomcat-net-01

# 3、查看下network帮助，发现一个命令 connect
[root@guardwhy ~]# docker network --help
Commands:
	# 连接一个容器到一个网络
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks
  
 # 4、测试打通 mynet-docker0，基本语法: `docker network connect [OPTIONS] NETWORK CONTAINER`
[root@guardwhy ~]# docker network connect mynet tomcat01
[root@guardwhy ~]# docker network inspect mynet
[
    {
        "Name": "mynet",
        "Id": "9f140b28095cf395ead5572e3dd5189519380ba3ea8fcd7cdf98e65f25d534f4",
        "Created": "2021-06-12T16:22:33.929558248+08:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "192.168.0.0/16",
                    "Gateway": "192.168.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "39506e89093fa3923bfd840d3f9c0223ba09c3a01fce5d000464149b87509563": {
            	# 连通之后就是将tomcat01放到了mynet网络下面，一个容器有两个IP地址，类似于阿里云服务的公网IP和私网IP。
                "Name": "tomcat01",
                "EndpointID": "6608306aa8fd6144bf8f74451cca8cb5a1dac6ffa314a8cd604253eaeaf84608",
                "MacAddress": "02:42:c0:a8:00:04",
                "IPv4Address": "192.168.0.4/16",
                "IPv6Address": ""
            },
            "68dabac6d09369bd3f39191bc08b954123cfc177af06aba5263a2e4fd5b6bdaf": {
                "Name": "tomcat-net-02",
                "EndpointID": "a153fdec599850124a3610716e7e174eb1992079a353cb3903fc00c85465ec20",
                "MacAddress": "02:42:c0:a8:00:03",
                "IPv4Address": "192.168.0.3/16",
                "IPv6Address": ""
            },
            "afa85e96d4f5ded21769674438d3f70b8eda2c1ea229a87e055d23ac49b1a024": {
                "Name": "tomcat-net-01",
                "EndpointID": "0a41c7b5ebf089e9114268891f67df4595e856185543b69c06c3dc39edcbe357",
                "MacAddress": "02:42:c0:a8:00:02",
                "IPv4Address": "192.168.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
# 5、连通OK，tomcat01可以ping通了
[root@guardwhy ~]# docker exec -it tomcat01 ping tomcat-net-01
PING tomcat-net-01 (192.168.0.2) 56(84) bytes of data.
64 bytes from tomcat-net-01.mynet (192.168.0.2): icmp_seq=1 ttl=64 time=0.114 ms
64 bytes from tomcat-net-01.mynet (192.168.0.2): icmp_seq=2 ttl=64 time=0.103 ms
64 bytes from tomcat-net-01.mynet (192.168.0.2): icmp_seq=3 ttl=64 time=0.106 ms

# tomcat02 依旧ping不通
[root@guardwhy ~]# docker exec -it tomcat02 ping tomcat-net-01
ping: tomcat-net-01: Name or service not known
[root@guardwhy ~]# 
```

3、小结

如果要跨网络操作别人，就需要使用 `docker network connect [OPTIONS] NETWORKCONTAINER` 连接。

## 10-IDEA整合Docker

### 10.1 创建项目

1、构建springboot项目

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210613062803.png)

2、编写一个helloController

```java
package cn.guardwhy.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String hello(){
        return "Hello Spring Boot!!!";
    }
}
```

3、启动测试项目，访问成功！！

### 10.2 将项目打包成jar

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210613063106.png" style="zoom:80%;" />

本地访问项目`jar`包

```shell
 java -jar .\springboot_demo01-0.0.1-SNAPSHOT.jar
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210613063324.png)

### 10.3 打包镜像

1、在项目下编写 `Dockerfile` 文件，将打包好的`jar`包拷贝到`Dockerfile`同级目录

**Dockerfile**

```shell
FROM java:8
# 1、服务器只有dockerfile和jar在同级目录
COPY *.jar /app.jar
CMD ["--server.port=8080"]

# 2、指定容器内要暴露的端口
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app.jar"]
```

2、将Dockerfile 和 项目的 jar 包上传到linux服务器上

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210613064125.png)

### 10.4 构建镜像

```shell
## 0、查看具体文件
[root@guardwhy home]# cd docker-java/
[root@guardwhy docker-java]# ll
total 16664
-rw-r--r-- 1 root root      199 Jun 13 05:52 Dockerfile
-rw-r--r-- 1 root root 17057877 Jun 13 05:52 springboot_demo01-0.0.1-SNAPSHOT.jar

## 1、查看运行的容器
[root@guardwhy docker-java]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@guardwhy docker-java]# ls
Dockerfile  springboot_demo01-0.0.1-SNAPSHOT.jar

## 2、构建镜像
[root@guardwhy docker-java]# docker build -t guardwhy .
Sending build context to Docker daemon  17.06MB
Successfully built 5d986122e10a
Successfully tagged guardwhy:latest
## 3、查看所有的镜像
[root@guardwhy docker-java]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
guardwhy            latest              5d986122e10a        33 minutes ago      660MB
java                8                   d23bdf5b1b1b        4 years ago         643MB
```

### 10.5 发布运行

```shell
## 1、构建镜像
[root@guardwhy docker-java]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
guardwhy            latest              5d986122e10a        33 minutes ago      660MB
java                8                   d23bdf5b1b1b        4 years ago         643MB

## 2、构建容器
[root@guardwhy docker-java]# docker run -d -P --name springboot-web guardwhy
c7fe159cfe3872aecf3b2eae5dd15b3840e1c2e99837e58e2aadc34a3dcf9fd3

## 3、查看运行的容器
[root@guardwhy docker-java]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                     NAMES
c7fe159cfe38        guardwhy            "java -jar /app.jar …"   5 seconds ago       Up 5 seconds        0.0.0.0:32769->8080/tcp   springboot-web

## 4、测试项目
[root@guardwhy docker-java]# curl localhost:32769
{"timestamp":"2021-06-12T23:21:13.290+00:00","status":404,"error":"Not Found","message":"","path":"/"}

## 5、测试成功！！！
[root@guardwhy ~]# curl localhost:32769/hello
Hello Spring Boot!!![root@guardwhy ~]# 
```

小结: ==以后使用docker之后，给别人交付的一个镜像即可运行！！！==





## 11- Docker Compose

### 11.1 基本概述

在实际生产环境中，一个应用往往由许多服务构成，而 docker 的最佳实践是一个容器只运行一个进程，因此运行多个微服务就要运行多个容器。多个容器协同工作需要一个有效的工具来管理他们，定义这些容器如何相互关联。`compose` 应运而生。compose 是用来定义和运行一个或多个容器(通常都是多个)运行和应用的工具。使用 compose 可以简化容器镜像的构建以及容器的运行。
compose 使用 YAML 文件来定义多容器之间的关系。一个 `docker-compose up` 就可以把完整的应用跑起来。 本质上 compose 把 YAML 文件解析成 docker 命令的参数，然后调用相应的 docker 命令行接口，从而将应用以容器化的方式管理起来。它通过解析容器间的依赖关系顺序地启动容器。而容器间的依赖关系由 YAML 文件中的  links 标记指定。

**官方文档**: [https://docs.docker.com/compose/](https://docs.docker.com/compose/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210614181700.png)

### 11.2 什么是docker compose？

compose、machine 和 swarm 是docker 原生提供的三大编排工具。简称docker三剑客。

Docker Compose能够在 Docker 节点上，以单引擎模式（Single-Engine Mode）进行多容器应用的部署和管理。多数的现代应用通过多个更小的微服务互相协同来组成一个完整可用的应用。比如一个简单的示例应用可能由如下 4 个微服务组成。

- Web前端。
- 订单管理。
- 品类管理。
- 后台数据库。

将以上服务组织在一起，就是一个可用的应用。部署和管理繁多的服务是困难的。而这正是 Docker Compose 要解决的问题。Docker Compose 并不是通过脚本和各种冗长的 docker 命令来将应用组件组织起来，而是通过一个声明式的配置文件描述整个应用，从而使用一条命令完成部署。应用部署成功后，还可以通过一系列简单的命令实现对其完整声明周期的管理。甚至，配置文件还可以置于版本控制系统中进行存储和管理。

### 11.3 docker compose安装与卸载

1、下载地址: [https://github.com/docker/compose/releases/tag/1.29.0](https://github.com/docker/compose/releases/tag/1.29.0)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210614182756.png)

2、通过Xftp上传到`linux`服务器中。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210614182922.png)

3、给予授权

```shell
[root@CentOS ~]# cd /data/
[root@CentOS data]# cd /home/data/
[root@CentOS data]# ls
docker-compose-Linux-x86_64
[root@CentOS data]# pwd
/home/data
[root@CentOS data]# mv /home/data/docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
mv：是否覆盖"/usr/local/bin/docker-compose"？ y
[root@CentOS data]# chmod 777 /usr/local/bin/docker-compose
```

4、检查安装情况以及版本

```shell
[root@CentOS data]# docker-compose -v
docker-compose version 1.29.0, build 07737305
[root@CentOS data]# docker-compose version
docker-compose version 1.29.0, build 07737305
docker-py version: 5.0.0
CPython version: 3.7.10
OpenSSL version: OpenSSL 1.1.0l  10 Sep 2019
[root@CentOS data]# 
```

5、docker compose卸载

`docker-compose`卸载只需要删除二进制文件就可以了。

```shell
rm -rf /usr/local/bin/docker-compose

## 重启系统！！！
reboot
```

### 11.4 快速开始

1、为项目创建一个目录`composetest`

```shell
[root@CentOS home]# mkdir composetest
[root@CentOS home]# ls
composetest  data  guardwhy
[root@CentOS home]# cd composetest/
[root@CentOS composetest]# pwd
/home/composetest
[root@CentOS composetest]# 
```

2、创建`app.py`文件

```python
import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)
@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)

if __name__ == "__main__":
        app.run(host="0.0.0.0",debug=True)                           
```

3、创建`requirements.txt`文件

```txt
flask
redis
```

4、创建`Dockerfile `文件，应用打包为镜像

```shell
FROM python:3.6-alpine
ADD . /code
WORKDIR /code
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

5、创建`docker-compose.yml`文件，(定义整个服务，需要的环境。 web、redis)完整的上线服务。

```shell
version: '3.8'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
  redis:
    image: redis:alpine
```

6、启动 compose 项目，执行成功！！！

```shell
docker-compose up
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210615112822.png)

7、查看生成镜像，服务启动成功！！！默认的服务名 都是`文件名_服务名 _ num`。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210615113358.png)

8、查看网络具体信息。

执行命令: `docker network ls`

```shell
[root@CentOS ~]# docker network ls
NETWORK ID     NAME                  DRIVER    SCOPE
f1926299a7da   bridge                bridge    local
366faa05f94f   composetest_default   bridge    local
46eb4e50e96b   host                  host      local
afb8f718984e   none                  null      local
```

项目中的内容都在同个网络下，如果在同一个网络下，可以直接通过域名访问。

```shell
docker network inspect 366faa05f94f 
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210615135432.png" style="zoom: 67%;" />

9、停止`docker-compose`

```shell
docker-compose down 或者ctrl+c
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210615135708.png)

小结: 以前都是单个 `docker run` 启动容器，==现在通过 docker-compose 编写 yaml配置文件、可以通过 compose 一键启动所有或者停止服务！！！==

### 11.5 compose.yml编写规则

1、基本概念

Docker Compose 使用 `YAML` 文件来定义多服务的应用。YAML 是 JSON 的一个子集，因此也可以使用`JSON`。
Docker Compose 默认使用文件名 `docker-compose.yml`。当然，也可以使用` -f` 参数指定具体文件。
Docker Compose 的 `YAML` 文件包含 4 个一级 key：`version、services、networks、volumes`。

- version 是必须指定的，而且总是位于文件的第一行。它定义了 Compose 文件格式（主要是API）的版本，version 并非定义 Docker Compose 或 Docker 引擎的版本号。
- services 用于定义不同的应用服务。Docker Compose 会将每个服务部署在各自的容器中。
- networks 用于指引 Docker 创建新的网络，默认情况下，Docker Compose 会创建 bridge 网络，这是一种单主机网络，只能够实现同一主机上容器的连接。当然，也可以使用 driver 属性来指定不同的网络类型。
- volumes 用于指引 Docker 来创建新的卷。

**官方文档**: [https://docs.docker.com/compose/](https://docs.docker.com/compose/)

```shell
version: '' # 版本
services: # 服务
服务1: web
# 服务配置
images
build
network
.....
服务2: redis
 ....
服务3: redis
# 其他配置 网络/卷、全局规则
volumes:
networks:
configs:
```

2、顺序启动服务(depends_on)

**官方文档**: [https://docs.docker.com/compose/compose-file/](https://docs.docker.com/compose/compose-file/)

Express dependency between services. Service dependencies cause the following behaviors:

- `docker-compose up` starts services in dependency order. In the following example, `db` and `redis` are started before `web`.
- `docker-compose up SERVICE` automatically includes `SERVICE`’s dependencies. In the example below, `docker-compose up web` also creates and starts `db` and `redis`.
- `docker-compose stop` stops services in dependency order. In the following example, `web` is stopped before `db` and `redis`。

**案例说明**:

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210615180903.png)

### 11.6 案例说明

1、安装基础镜像

```shell
[root@CentOS data]# docker pull nginx:1.20.1
docker.io/library/nginx:1.20.1
[root@CentOS data]# docker pull tomcat:9.0.20-jre8-alpine
9.0.20-jre8-alpine: Pulling from library/tomcat
docker.io/library/tomcat:9.0.20-jre8-alpine
[root@CentOS data]# docker images
REPOSITORY   TAG                  IMAGE ID       CREATED       SIZE
nginx        1.20.1               993ef3592f66   2 weeks ago   133MB
tomcat       9.0.20-jre8-alpine   387f9d021d3a   2 years ago   108MB
[root@CentOS data]# 
```

2、创建基础容器

```shell
[root@CentOS data]# mkdir tomcat1 tomcat2 nginx
[root@CentOS data]# ls
nginx  tomcat1  tomcat2
[root@CentOS data]# docker run -itd --name nginx -p 80:80 nginx:1.20.1
ca10564478d2200bf57ceae115e17193cf1ed2a1f642f2df5167b9c988a4dfee
[root@CentOS data]# docker run -itd --name tomcat -p 8080:8080 tomcat:9.0.20-jre8-alpine
683a6fa394e1addef48c8eddd980b0891b9c796c3411f78804fff2a160228b49
[root@CentOS ~]# docker ps -a
CONTAINER ID   IMAGE                       COMMAND                  CREATED         STATUS         PORTS                                       NAMES
683a6fa394e1   tomcat:9.0.20-jre8-alpine   "catalina.sh run"        7 minutes ago   Up 7 minutes   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   tomcat
ca10564478d2   nginx:1.20.0                "/docker-entrypoint.…"   7 minutes ago   Up 7 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp           nginx
[root@CentOS data]#
```

3、文件拷贝

nginx相关操作

```shell
docker cp nginx:/etc/nginx /home/data
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210615213533.png)

tomcat执行命令

```shell
[root@CentOS data]# ls
nginx  tomcat1  tomcat2
[root@CentOS data]# docker cp tomcat:/usr/local/tomcat/webapps /home/data/tomcat1/webapps
[root@CentOS data]# ls
nginx  tomcat1  tomcat2
[root@CentOS data]# cd tomcat1/webapps/
[root@CentOS webapps]# ll
总用量 8
drwxr-xr-x. 14 root root 4096 5月  16 2019 docs
drwxr-xr-x.  6 root root   83 5月  16 2019 examples
drwxr-xr-x.  5 root root   87 5月  16 2019 host-manager
drwxr-xr-x.  5 root root  103 5月  16 2019 manager
drwxr-xr-x.  3 root root 4096 5月  16 2019 ROOT
[root@CentOS webapps]# docker cp tomcat:/usr/local/tomcat/webapps /home/data/tomcat2/webapps
[root@CentOS data]# cd tomcat2/webapps/
[root@CentOS webapps]# ll
总用量 8
drwxr-xr-x. 14 root root 4096 5月  16 2019 docs
drwxr-xr-x.  6 root root   83 5月  16 2019 examples
drwxr-xr-x.  5 root root   87 5月  16 2019 host-manager
drwxr-xr-x.  5 root root  103 5月  16 2019 manager
drwxr-xr-x.  3 root root 4096 5月  16 2019 ROOT
[root@CentOS webapps]# 
```

3、追加操作

```shell
[root@CentOS data]# echo "hello,tomcat1" > /home/data/tomcat1/webapps/ROOT/index.jsp
[root@CentOS data]# cat  /home/data/tomcat1/webapps/ROOT/index.jsp
hello,tomcat1
[root@CentOS data]# echo "hello,tomcat2" > /home/data/tomcat2/webapps/ROOT/index.jsp
[root@CentOS data]# cat  /home/data/tomcat2/webapps/ROOT/index.jsp
hello,tomcat2
[root@CentOS data]# 
```

4、修改`nginx.conf`

在`nginx.conf`文件尾部添加以下内容

```shell
include vhost/*.conf;
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210615221102.png)

5、反向代理配置

```shell
mkdir -p /data/nginx/vhost
[root@CentOS nginx]# cd vhost/
[root@CentOS vhost]# vim guardwhy.cn.conf
[root@CentOS vhost]# cat guardwhy.cn.conf 
upstream nginxguardwhy{
  server 192.168.50.131:8081;
  server 192.168.50.131:8082;
 }

server{
  listen 80;
  server_name 192.168.50.131;
  autoindex on;
  index index.html index.htm index.jsp;
  location / {
    proxy_pass http://nginxguardwhy;
    add_header Access-Control-Allow-Origin *;
  }
}
[root@CentOS vhost]# 
```

6、创建`docker-compose.yml`文件

```shell
version: '3'
services:
  guardwhy-nginx:
    image: nginx:1.20.1
    container_name: guardwhy-nginx
    restart: always
    ports:
    - 80:80
    volumes:
    - /home/data/nginx:/etc/nginx
  guardwhy-tomcat1:
    image: tomcat:9.0.20-jre8-alpine
    container_name: guardwhy-tomcat1
    restart: always
    ports:
    - 8081:8080
    volumes:
    - /home/data/tomcat1/webapps:/usr/local/tomcat/webapps
    depends_on:
      - guardwhy-nginx
  guardwhy-tomcat2:
    image: tomcat:9.0.20-jre8-alpine
    container_name: guardwhy-tomcat2
    restart: always
    ports:
    - 8082:8080
    volumes:
      - /home/data/tomcat2/webapps:/usr/local/tomcat/webapps
    depends_on:
      - guardwhy-nginx
```

7、启动服务，执行以下命令

```shell
docker-compose up 或者 docker-compose up -d
```

浏览器测试，执行成功！！！

```shell
点击链接: http://192.168.50.131:8081/
点击链接: http://192.168.50.131:8082/
点击链接: http://192.168.50.131/
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210616005903.png)

### 11.7 常用命令汇总

注意以下所有的命令要在`docker-compose.yaml`所在的目录中，执行才能生效！！！

1、启动服务

```shell
docker-compose up -d
```

2、列出所有运行容器

```shell
docker-compose ps
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210616010652.png)

3、查看服务日志

```shell
docker-compose logs
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210616010801.png)

4、构建或者重新构建服务

```shell
docker-compose build
```

5、启动服务

```shell
docker-compose start
```

6、停止已运行的服务

```shell
docker-compose stop
```

7、重启服务

```shell
docker-compose restart
```

8、停止服务

```shell
docker-compose down
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210616011152.png)	

## 12-安装Docker私服

在使用maven管理jar包依赖的时候，为了避免每次都从中央仓库拉取依赖包，使用了nexus做了代理仓库。docker镜像仓库与nexus私服仓库作用类似，用于将打包好的镜像保存在仓库中方便开发、测试、生产环境镜像拉取存储，减轻环境部署需要的相应操作。

### 12.1 购买阿里云服务器

1、选择云服务器，创建实例

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617105303.png)

2、自定义购买，按量付费

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617105404.png)

3、选择服务器类型，数量，内存，带宽

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617110016.png)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617110050.png)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617110137.png)

4、自定义登录密码

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617110246.png)

5、创建成功！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617110318.png)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617110437.png)

### 12.2 节点信息

购买两个服务器，服务器的名字为`root`，服务器密码: `Hxy162530`。

| 主机名     | ip地址        | 具体说明     |
| ---------- | ------------- | ------------ |
| guardwhy01 | 8.134.117.200 | docker主机   |
| guardwhy02 | 8.134.113.78  | registry主机 |

### 12.3 官方私服

1、镜像官方地址: [https://hub.docker.com/_/registry](https://hub.docker.com/_/registry)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617133214.png)

2、基础镜像

拉取基本镜像

```shell
docker pull registry:2.7.1
```

运行容器

```shell
docker run -itd --name gegistry -p 5000:5000 --restart always registry:2.7.1
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617155545.png)

访问链接: [http://8.134.113.78:5000/v2/_catalog](http://8.134.113.78:5000/v2/_catalog)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617155940.png)

3、添加私服仓库地址

```shell
编辑配置文件
vim /etc/docker/daemon.json

增加仓库配置信息
{ "insecure-registries":["8.134.113.78:5000"] }

重启docker
systemctl daemon-reload
systemctl restart docker

查看docker信息确认仓库是否添加
docker info
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617165822.png)

4、上传镜像

```shell
docker tag nginx:1.20.1 8.134.113.78:5000/nginx:v1
docker push 8.134.113.78:5000/nginx:v1
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617161942.png)

5、查看镜像版本和信息

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617170143.png)

6、从官方私服中下载镜像

```shell
[root@guardwhy01 ~]# docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
[root@guardwhy01 ~]# docker pull 8.134.113.78:5000/nginx:v1
v1: Pulling from nginx
69692152171a: Pull complete 
94d185f62f0a: Pull complete 
da9d3d3df3e3: Pull complete 
1c11b8f3980d: Pull complete 
541b1d41bb91: Pull complete 
d8f6ef04dfa8: Pull complete 
Digest: sha256:56cbb3c9ada0858d69d19415039ba2aa1e9b357ba9aa9c88c73c30307aae17b0
Status: Downloaded newer image for 8.134.113.78:5000/nginx:v1
8.134.113.78:5000/nginx:v1
[root@guardwhy01 ~]# docker images
REPOSITORY                TAG       IMAGE ID       CREATED       SIZE
8.134.113.78:5000/nginx   v1        993ef3592f66   3 weeks ago   133MB
[root@guardwhy01 ~]# 
```

### 12.4 企业私服

#### 12.4.1 安装私服

1、购买2核8G内存服务器，安装`docker`和`docker compose`

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617213411.png)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617213849.png)

2、下载harbor

官方地址: [https://goharbor.io/](https://goharbor.io/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617214307.png)

github官网地址：[https://github.com/goharbor/harbor](https://github.com/goharbor/harbor)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617214509.png)

官方帮助文档：[https://github.com/goharbor/harbor/blob/v1.9.4/docs/installation_guide.md](https://github.com/goharbor/harbor/blob/v1.9.4/docs/installation_guide.md)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617214659.png)

3、服务器配置

| 硬件资源 | 最小配置 | 推荐配置 |
| -------- | -------- | -------- |
| CPU      | 2CPU     | 4CPU     |
| 内存     | 4GB      | 8GB      |
| 硬盘     | 40GB     | 60GB     |

4、安装harbor开发环境大部分采用http方式进行安装，推荐使用离线安装！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618104517.png)

通过`Xftp`上传到`\home\data`目录中，然后解压软件。

```shell
[root@guardwhy03 data]# ls
harbor-offline-installer-v1.9.4.tgz
[root@guardwhy03 data]# tar zxvf harbor-offline-installer-v1.9.4.tgz 
harbor/harbor.v1.9.4.tar.gz
harbor/prepare
harbor/LICENSE
harbor/install.sh
harbor/harbor.yml
[root@guardwhy03 data]# ll
total 624500
drwxr-xr-x 2 root root      4096 Jun 17 21:53 harbor
-rw-r--r-- 1 root root 639477963 Jun 17 21:11 harbor-offline-installer-v1.9.4.tgz
```

5、进入安装目录，修改` harbor.yml`文件

修改私服镜像地址

```shell
hostname: 8.134.123.77
```

修改镜像地址访问端口号

```shell
port: 5000
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618105934.png)

harbor管理员登录系统密码

```shell
harbor_admin_password: Harbor12345
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618110031.png)

修改harbor映射卷目录

```shell
data_volume: /home/data/harbor
```

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618110140.png)

5、安装harbor

执行启动脚本

```shell
./install.sh
```

准备安装环境：检查docker版本和docker-compose版本

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618110435.png)

安装成功！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618110603.png)

6、使用Chrome 浏览器访问harbor私服，点击链接: [http://8.134.123.77:5000/harbor/projects](http://8.134.123.77:5000/harbor/projects)，输入用户名和默认的密码

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618115832.png)

#### 12.4.2 上传镜像

1、在主机`docker01`中配置私服。

```shell
[root@guardwhy01 data]# vim /etc/docker/daemon.json
[root@guardwhy01 data]# cat /etc/docker/daemon.json
{
  "registry-mirrors": ["https://5bsomu6l.mirror.aliyuncs.com"],
  "insecure-registries":["8.134.123.77:5000"]
}
## 重启docker服务！！！
[root@guardwhy01 data]# systemctl daemon-reload
[root@guardwhy01 data]# systemctl restart docker
```

2、在`harbor`界面中新建项目：`guardwhy_cms`

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618131351.png)

3、登录和退出私服

```shell
## 登录私服
docker login -u admin -p Harbor12345 8.134.123.77:5000

## 退出私服
docker logout 8.134.123.77:5000
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618125514.png)

查看当前镜像

```shell
[root@guardwhy01 data]# docker images
REPOSITORY   TAG                  IMAGE ID       CREATED       SIZE
nginx        1.20.1               993ef3592f66   3 weeks ago   133MB
tomcat       9.0.20-jre8-alpine   387f9d021d3a   2 years ago   108MB
```

4、上传镜像

```shell
docker tag nginx:1.20.1 8.134.123.77:5000/guardwhy_cms/nginx:v1.0
docker tag tomcat:9.0.20-jre8-alpine 8.134.123.77:5000/guardwhy_cms/tomcat:v1.0

## 推送操作
docker push 8.134.123.77:5000/guardwhy_cms/nginx:v1.0
docker push 8.134.123.77:5000/guardwhy_cms/tomcat:v1.0

```

查看镜像

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618131724.png)

上传镜像成功！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618131205.png)

5、通过私服下载镜像，下载成功！！！

```shell
[root@guardwhy01 data]# docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
[root@guardwhy01 data]# docker pull 8.134.123.77:5000/guardwhy_cms/nginx:v1.0
v1.0: Pulling from guardwhy_cms/nginx
69692152171a: Pull complete 
94d185f62f0a: Pull complete 
da9d3d3df3e3: Pull complete 
1c11b8f3980d: Pull complete 
541b1d41bb91: Pull complete 
d8f6ef04dfa8: Pull complete 
Digest: sha256:56cbb3c9ada0858d69d19415039ba2aa1e9b357ba9aa9c88c73c30307aae17b0
Status: Downloaded newer image for 8.134.123.77:5000/guardwhy_cms/nginx:v1.0
8.134.123.77:5000/guardwhy_cms/nginx:v1.0
[root@guardwhy01 data]# docker pull 8.134.123.77:5000/guardwhy_cms/tomcat:v1.0
v1.0: Pulling from guardwhy_cms/tomcat
e7c96db7181b: Pull complete 
f910a506b6cb: Pull complete 
b6abafe80f63: Pull complete 
d8c966ddef98: Pull complete 
15b754e99755: Pull complete 
4227393eb352: Pull complete 
Digest: sha256:490b98379033031e84f9795da326371fdb95c6d9c3f5e3c14e1316ca754e324f
Status: Downloaded newer image for 8.134.123.77:5000/guardwhy_cms/tomcat:v1.0
8.134.123.77:5000/guardwhy_cms/tomcat:v1.0
[root@guardwhy01 data]# docker images
REPOSITORY                              TAG       IMAGE ID       CREATED       SIZE
8.134.123.77:5000/guardwhy_cms/nginx    v1.0      993ef3592f66   3 weeks ago   133MB
8.134.123.77:5000/guardwhy_cms/tomcat   v1.0      387f9d021d3a   2 years ago   108MB
[root@guardwhy01 data]# 
```

## 13-Docker Swarm

### 13.1 购买服务器

购买3台服务器，所有主机都安装`docker`和`docker-compose`

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619101956.png)

### 13.2 Swarm集群产生

compose、machine 和 swarm 是docker 原生提供的三大编排工具。简称docker三剑客。

1、服务器硬件要求

| 硬件资源 | 最小配置 | 推荐配置 |
| -------- | -------- | -------- |
| CPU      | 1 CPU    | 2CPU     |
| 内存     | 1GB      | 2~4GB    |
| 硬盘     | 20 GB    | 40GB     |

2、节点信息

| 主机名   | IP地址        | 具体说明          |
| -------- | ------------- | ----------------- |
| docker01 | 8.134.122.252 | swarm-manager节点 |
| docker02 | 8.134.114.8   | swarm-work01节点  |
| docker03 | 8.134.123.77  | swarm-work02节点  |

3、当前服务器应用状态

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619111429.png)

4、容器化部署存在问题

- 怎么保证数据完整性，怎么去管很多微服容器，怎么去更新容器而不影响客户的业务？
- 如果容器down掉了。怎么自动恢复？

===》解决以上问题，docker-swarm横空出世！！！。

### 13.3 安装docker-swarm

1、基本概述

Docker Swarm 和 Docker Compose 一样，都是 Docker 官方容器编排项目，但不同的是，Docker Compose 是一个在单个服务器或主机上创建多个容器的工具，可以将组成某个应该的多个docker容器编排在一起，同时管理。而 Docker Swarm 则可以在多个服务器或主机上创建容器集群服务，其主要作用是把若干台Docker主机抽象为一个整体，并且通过一个入口（docker stack）统一管理这些Docker主机上的各种Docker资源。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619112803.png)

stack 是构成特定环境中的 service 集合, 它是自动部署多个相互关联的服务的简便方法，而无需单独定义每个服务。stack file 是一种 yaml 格式的文件，类似于 docker-compose.yml 文件，它定义了一个或多个服务，并定义了服务的环境变量、部署标签、容器数量以及相关的环境特定配置等。

2、官方文档：[https://docs.docker.com/engine/swarm/](https://docs.docker.com/engine/swarm/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619115027.png)

3、Docker Swarm由两部分组成

- ==Docker集群==：将一个或多个Docker节点组织起来，用户就能以集群的方式进行管理。
- ==应用编排==：有一套API用来部署和管理容器。

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619121923.png)

### 13.4 管理节点

1、初始化第一个管理节点

advertise-addr和listen-addr这两个参数注解：

- 前者用来指定其他节点连接m0时的地址。
- 后者指定承载swarm流量的IP和端口。
- 创建管理节点，会在本地新建docker网络。

2、manager节点说明

MANAGER STATUS列：

- Leader 意味着该节点是使得群的所有群管理和编排决策的主要管理器节点。
- Reachable 意味着节点是管理者节点正在参与Raft共识。如果管理节点不可用，则该节点有资格被选为新的管理节点。
- Unavailable 意味着节点是不能与其他管理器通信的管理器。如果管理器节点不可用，应该将新的管理器节点加入群集，或者将工作器节点升级为管理器。

AVAILABILITY列：

- Active 意味着调度程序可以将任务分配给节点。
- Pause 意味着调度程序不会将新任务分配给节点，但现有任务仍在运行。
- Drain 意味着调度程序不会向节点分配新任务，调度程序关闭所有现有任务并在可用节点上调度它们。

**docker01服务器**

注意：==IP地址选择的是阿里云服务器的私服！！！==

```shell
[root@guardwhy01 ~]# docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
44443742f9b7   bridge    bridge    local
5f09756231c5   host      host      local
9d85ae8a4d3d   none      null      local
[root@guardwhy01 ~]# docker swarm init --advertise-addr 172.21.251.249:2377 --listen-addr 172.21.251.249:2377
Swarm initialized: current node (ujswj6ys93qhtji45oxszv4zr) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-2js986t4enexu18fpn5dnticbmx0df9qni5nsfsn6ngykl931s-1tattfxbp5ahqz7wk1ha7ycfh 172.21.251.249:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

[root@guardwhy01 ~]# docker network ls
NETWORK ID     NAME              DRIVER    SCOPE
44443742f9b7   bridge            bridge    local
c372c3473958   docker_gwbridge   bridge    local
5f09756231c5   host              host      local
jh4ohdal24uo   ingress           overlay   swarm
9d85ae8a4d3d   none              null      local
[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Leader           20.10.7
[root@guardwhy01 ~]# 
```

3、加入新的节点

Docker Swarm的新节点加入是从管理节点(`docker01服务器`)获取一长串命令，称为`join token`，任何加入集群只要执行`join token`即可加入Swarm集群。

**docker02服务器**

```shell
[root@guardwhy02 ~]# docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
475d6f0e7633   bridge    bridge    local
4212954a0f4f   host      host      local
7fb6fab37bee   none      null      local
[root@guardwhy02 ~]# docker swarm join --token SWMTKN-1-2js986t4enexu18fpn5dnticbmx0df9qni5nsfsn6ngykl931s-1tattfxbp5ahqz7wk1ha7ycfh 172.21.251.249:2377
This node joined a swarm as a worker.
[root@guardwhy02 ~]# 
```

如果有新的work节点需要加入，在m0执行命令`docker swarm join-token worker`即可得到管理work节点的`join token`。

**docker01服务器**

```shell
[root@guardwhy01 ~]# docker swarm join-token worker
To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-2js986t4enexu18fpn5dnticbmx0df9qni5nsfsn6ngykl931s-1tattfxbp5ahqz7wk1ha7ycfh 172.21.251.249:2377

[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Leader           20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active                          20.10.7
[root@guardwhy01 ~]# 
```

如果有新的管理节点需要加入，在m0执行命令`docker swarm join-token manager`即可得到管理manager节点的`join token`。

**docker01服务器**

```shell
[root@guardwhy01 ~]# docker swarm join-token manager
To add a manager to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-2js986t4enexu18fpn5dnticbmx0df9qni5nsfsn6ngykl931s-aw4p1x4xwul0iw1ma2aid49cg 172.21.251.249:2377
[root@guardwhy01 ~]#
```

**docker03服务器**

```shell
[root@guardwhy03 ~]# docker swarm join --token SWMTKN-1-2js986t4enexu18fpn5dnticbmx0df9qni5nsfsn6ngykl931s-aw4p1x4xwul0iw1ma2aid49cg 172.21.251.249:2377
This node joined a swarm as a manager.
[root@guardwhy03 ~]# 
```

在manager查看所有节点。

**docker01服务器**

```shell
[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Leader           20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active                          20.10.7
25wan9kvxtew5m48hvkng8jr5     guardwhy03   Ready     Active         Reachable        20.10.7
[root@guardwhy01 ~]# 
```

### 13.5 节点相关操作

1、验证节点

**master节点**

```shell
[root@guardwhy01 ~]# docker info
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619143128.png)

**work节点**

```shell
[root@guardwhy02 ~]# docker info
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619143459.png)

2、节点权限提升/降低

将`manager`节点降低为`worker`节点，在`manager`节点执行如下命令

```shell
[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Reachable        20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active                          20.10.7
25wan9kvxtew5m48hvkng8jr5     guardwhy03   Ready     Active         Leader           20.10.7
[root@guardwhy01 ~]# docker node demote guardwhy03
Manager guardwhy03 demoted in the swarm.
[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Leader           20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active                          20.10.7
25wan9kvxtew5m48hvkng8jr5     guardwhy03   Unknown   Active                          20.10.7
[root@guardwhy01 ~]# 
```

将worker节点提升为manager节点，在manager节点执行如下命令

```shell
[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Leader           20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active                          20.10.7
25wan9kvxtew5m48hvkng8jr5     guardwhy03   Ready     Active                          20.10.7
[root@guardwhy01 ~]# docker node promote guardwhy02 
Node guardwhy02 promoted to a manager in the swarm.
[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Leader           20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active         Reachable        20.10.7
25wan9kvxtew5m48hvkng8jr5     guardwhy03   Ready     Active                          20.10.7
[root@guardwhy01 ~]# 
```

3、节点脱离集群

**docker03服务器**

在`docker03`服务器中，使用以下命令

```shell
[root@guardwhy03 ~]# docker swarm leave
Node left the swarm.
[root@guardwhy03 ~]# 
```

**docker01服务器**

在`docker01`服务器中，使用以下命令

```shell
[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Reachable        20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active         Leader           20.10.7
25wan9kvxtew5m48hvkng8jr5     guardwhy03   Down      Active                          20.10.7
[root@guardwhy01 ~]# 
```

4、删除脱离集群的节点

删除节点命令: `docker node rm 节点名称|节点ID`

```shell
[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Reachable        20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active         Leader           20.10.7
25wan9kvxtew5m48hvkng8jr5     guardwhy03   Down      Active                          20.10.7
[root@guardwhy01 ~]# docker node rm guardwhy03
guardwhy03
[root@guardwhy01 ~]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Reachable        20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active         Leader           20.10.7
[root@guardwhy01 ~]# 
```

在`manager`中重新添加`worker`节点

```shell
[root@guardwhy01 ~]# docker swarm join-token worker
To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-2js986t4enexu18fpn5dnticbmx0df9qni5nsfsn6ngykl931s-1tattfxbp5ahqz7wk1ha7ycfh 172.21.251.249:2377

[root@guardwhy01 ~]#
```

```shell
[root@guardwhy03 ~]# docker swarm join --token SWMTKN-1-2js986t4enexu18fpn5dnticbmx0df9qni5nsfsn6ngykl931s-1tattfxbp5ahqz7wk1ha7ycfh 172.21.251.249:2377
This node joined a swarm as a worker.
[root@guardwhy03 ~]# 
```

添加成功！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619164358.png)

5、安装图形界面

docker官方地址: [https://hub.docker.com/r/dockersamples/visualizer](https://hub.docker.com/r/dockersamples/visualizer)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619194312.png)

拉取基础镜像

注意：要在`manager`服务器创建容器！！！

```shell
docker pull dockersamples/visualizer:latest
```

运行图形界面镜像

```shell
docker run -itd --name visualizer -p 8091:8080 \
-e HOST=8.134.122.252 \
-e PORT=8080 \
-v /var/run/docker.sock:/var/run/docker.sock dockersamples/visualizer:latest
```

查看运行结果

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619195506.png)

打开浏览器，点击链接: [http://8.134.122.252:8091/](http://8.134.122.252:8091/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619195719.png)

6、Swarm命令小结

| 常用命令                | 具体作用                 |
| ----------------------- | ------------------------ |
| docker swarm init       | 初始化一个 swarm 群集    |
| docker swarm join       | 加入群集作为节点或管理器 |
| docker swarm join-token | 管理用于加入群集的令牌   |
| docker swarm leave      | 离开 swarm 群集          |
| docker swarm unlock     | 解锁 swarm 群集          |
| docker swarm unlock-key | 管理解锁钥匙             |
| docker swarm update     | 更新 swarm 群集          |

7、node命令小结

| 常用命令            | 具体作用                                           |
| ------------------- | -------------------------------------------------- |
| docker node demote  | 从 swarm 群集管理器中降级一个或多个节点            |
| docker node inspect | 显示一个或多个节点的详细信息                       |
| docker node ls      | 列出 swarm 群集中的节点                            |
| docker node promote | 将一个或多个节点推入到群集管理器中                 |
| docker node ps      | 列出在一个或多个节点上运行的任务，默认为当前节点。 |
| docker node rm      | 从 swarm 群集删除一个或多个节点                    |
| docker node update  | 更新一个节点                                       |

### 13.6 Docker service

1、docker service命令小结

| 常用命令                | 具体作用                     |
| ----------------------- | ---------------------------- |
| docker service create   | 创建服务                     |
| docker service inspect  | 显示一个或多个服务的详细信息 |
| docker service logs     | 获取服务的日志               |
| docker service ls       | 列出服务                     |
| docker service rm       | 删除一个或多个服务           |
| docker service scale    | 设置服务的实例数量           |
| docker service update   | 更新服务                     |
| docker service rollback | 恢复服务至update之前的配置   |

2、需求实现

​	![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619220547.png)



2、集群所有的节点都下载`nginx`基础镜像

```shell
docker pull nginx:1.18.0-alpine
docker pull nginx:1.19.3-alpine
```

3、在docker01服务器(`manager节点`)中创建`overlay`网络。

```shell
[root@guardwhy01 data]# docker network ls
NETWORK ID     NAME              DRIVER    SCOPE
0eb90cd90de7   bridge            bridge    local
c372c3473958   docker_gwbridge   bridge    local
5f09756231c5   host              host      local
jh4ohdal24uo   ingress           overlay   swarm
9d85ae8a4d3d   none              null      local
[root@guardwhy01 data]# docker network create -d overlay nginx-net
yoyo8isxn654fmkeygfsi3nlw
[root@guardwhy01 data]# 
```

4、创建`5个nginx`容器的集群

```shell
[root@guardwhy01 data]# docker service create --name nginx --network nginx-net -p 80:80 --replicas 5 nginx:1.18.0-alpine 
u0etuzildau4h931nybmjbgtx
overall progress: 5 out of 5 tasks 
1/5: running   [==================================================>] 
2/5: running   [==================================================>] 
3/5: running   [==================================================>] 
4/5: running   [==================================================>] 
5/5: running   [==================================================>] 
verify: Service converged 
[root@guardwhy01 data]# docker node ls
ID                            HOSTNAME     STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ujswj6ys93qhtji45oxszv4zr *   guardwhy01   Ready     Active         Leader           20.10.7
sq9x6zrg7u2izo4tzmrffbyz1     guardwhy02   Ready     Active                          20.10.7
pu1ykn1mnx0ptbiw7bjwltrq6     guardwhy03   Ready     Active                          20.10.7
[root@guardwhy01 data]# docker ps -a
CONTAINER ID   IMAGE                             COMMAND                  CREATED         STATUS                            PORTS                                       NAMES
f42ef1d0c1e5   nginx:1.18.0-alpine               "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes                      80/tcp                                      nginx.4.qc3yxnwk3zpeurfg3cj6kfy3t
d4c2fa9dbab0   nginx:1.18.0-alpine               "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes                      80/tcp                                      nginx.2.d89kask69omz214ivu14fduo4
3d648fc53506   dockersamples/visualizer:latest   "/sbin/tini -- node …"   6 hours ago     Up 4 seconds (health: starting)   0.0.0.0:8091->8080/tcp, :::8091->8080/tcp   visualizer
[root@guardwhy01 data]# 
```

访问链接: [http://8.134.122.252:8091/](http://8.134.122.252:8091/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619230404.png)

5、命令查看服务情况。

```shell
[root@guardwhy01 data]# docker service ls
ID             NAME      MODE         REPLICAS   IMAGE                 PORTS
u0etuzildau4   nginx     replicated   5/5        nginx:1.18.0-alpine   *:80->80/tcp
[root@guardwhy01 data]#
```

注意: ` docker service ls`命令只能在manager节点使用，在worker节点无法查看

6、查看服务器容器情况

```shell
[root@guardwhy02 home]# docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS     NAMES
a77fba3447f0   nginx:1.18.0-alpine   "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes   80/tcp    nginx.3.haruvjy8v68otk1cxdkc4rs90
e13fb38a0602   nginx:1.18.0-alpine   "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes   80/tcp    nginx.1.hwedkhibak90mzvh7jt9oaaau
[root@guardwhy02 home]# 
```

注意: 在manager或者worker节点都可以执行`docker ps`命令。

7、manager节点只用于管理集群，不部署服务。

```shell
[root@guardwhy01 data]# docker node update --availability drain guardwhy01
guardwhy01
[root@guardwhy01 data]# docker ps
CONTAINER ID   IMAGE                             COMMAND                  CREATED       STATUS                    PORTS                                       NAMES
3d648fc53506   dockersamples/visualizer:latest   "/sbin/tini -- node …"   6 hours ago   Up 14 minutes (healthy)   0.0.0.0:8091->8080/tcp, :::8091->8080/tcp   visualizer
[root@guardwhy01 data]# 
```

访问链接: [http://8.134.122.252:8091/](http://8.134.122.252:8091/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619231752.png)

8、将服务缩减为3个容器

```shell
[root@guardwhy01 data]# docker service scale nginx=3
nginx scaled to 3
overall progress: 3 out of 3 tasks 
1/3: running   [==================================================>] 
2/3: running   [==================================================>] 
3/3:   
verify: Service converged 
[root@guardwhy01 data]# 
```

访问链接: [http://8.134.122.252:8091/](http://8.134.122.252:8091/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619232202.png)

9、升级nginx版本

进入其中一个容器查看nginx的版本信息。

```shell
[root@guardwhy02 home]# docker images
REPOSITORY   TAG             IMAGE ID       CREATED        SIZE
nginx        1.18.0-alpine   684dbf9f01f3   2 months ago   21.9MB
nginx        1.19.3-alpine   4efb29ff172a   8 months ago   21.8MB
[root@guardwhy02 home]# docker ps -a
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS     NAMES
a77fba3447f0   nginx:1.18.0-alpine   "/docker-entrypoint.…"   29 minutes ago   Up 29 minutes   80/tcp  nginx.3.haruvjy8v68otk1cxdkc4rs90
e13fb38a0602   nginx:1.18.0-alpine   "/docker-entrypoint.…"   29 minutes ago   Up 29 minutes   80/tcp    nginx.1.hwedkhibak90mzvh7jt9oaaau
[root@guardwhy02 home]# docker exec -it e13fb38a0602 sh
/ # nginx -v
nginx version: nginx/1.18.0
nginx version: nginx/1.18.0
/ # exit
[root@guardwhy02 home]# 
```

更新镜像

注意：更新镜像只能在`manager节点`使用。

```shell
[root@guardwhy01 data]# docker service update --image nginx:1.19.3-alpine nginx
nginx
overall progress: 3 out of 3 tasks 
1/3: running   [==================================================>] 
2/3: running   [==================================================>] 
3/3: running   [==================================================>] 
verify: Service converged 
[root@guardwhy01 data]# 
```

更新镜像以后，查看结果！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619235159.png)

添加或者更新一个对外端口

```shell
[root@guardwhy01 data]# docker service update --publish-add 8087:80 nginx
nginx
overall progress: 5 out of 5 tasks 
1/5: running   [==================================================>] 
2/5: running   [==================================================>] 
3/5: running   [==================================================>] 
4/5: running   [==================================================>] 
5/5: running   [==================================================>] 
verify: Service converged 
[root@guardwhy01 data]# 
```

访问链接: [http://8.134.122.252:8087/](http://8.134.122.252:8087/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210619235938.png)

10、删除服务

```shell
[root@guardwhy01 data]# docker network ls
NETWORK ID     NAME              DRIVER    SCOPE
0eb90cd90de7   bridge            bridge    local
c372c3473958   docker_gwbridge   bridge    local
5f09756231c5   host              host      local
jh4ohdal24uo   ingress           overlay   swarm
yoyo8isxn654   nginx-net         overlay   swarm
9d85ae8a4d3d   none              null      local
[root@guardwhy01 data]# docker service rm nginx
nginx
[root@guardwhy01 data]# docker network rm nginx-net
nginx-net
[root@guardwhy01 data]# docker service ls
ID        NAME      MODE      REPLICAS   IMAGE     PORTS
[root@guardwhy01 data]# 
```

### 13.7  Docker stack

1、docker stack命令小结

| 常用命令              | 具体作用                   |
| --------------------- | -------------------------- |
| docker stack deploy   | 部署新的堆栈或更新现有堆栈 |
| docker stack ls       | 列出现有堆栈               |
| docker stack ps       | 列出堆栈中的任务           |
| docker stack rm       | 删除一个或多个堆栈         |
| docker stack services | 列出堆栈中的服务           |

2、在`manager`节点中创建`docker-compose.yml`文件

```shell
version: '3'
services:
  nginx-web:
    image: nginx:1.19.3-alpine
    container_name: nginx
    networks:
     - nginx-net
    restart: always
    ports:
      - 80:80
    deploy:
      replicas: 5

networks:
  nginx-net:
    driver: overlay
```

3、运行`nginx`

```shell
[root@guardwhy01 data]# docker stack deploy nginx-stack -c docker-compose.yml
Ignoring unsupported options: restart

Ignoring deprecated options:

container_name: Setting the container name is not supported.

Creating service nginx-stack_nginx-web
[root@guardwhy01 data]# docker service ls
ID             NAME                    MODE         REPLICAS   IMAGE                 PORTS
i8nabdgwztf0   nginx-stack_nginx-web   replicated   5/5        nginx:1.19.3-alpine   *:80->80/tcp
[root@guardwhy01 data]# 
```

访问链接: [http://8.134.122.252:8091/](http://8.134.122.252:8091/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210620003710.png)

4、查看NAME中的服务名为：`nginx-stack_nginx-web`所有容器

```shell
[root@guardwhy01 data]# docker service ps nginx-stack_nginx-web
ID             NAME                      IMAGE                 NODE         DESIRED STATE   CURRENT STATE            ERROR     PORTS
j91t0720gitm   nginx-stack_nginx-web.1   nginx:1.19.3-alpine   guardwhy02   Running         Running 11 minutes ago             
5qooi8nxt1xb   nginx-stack_nginx-web.2   nginx:1.19.3-alpine   guardwhy02   Running         Running 11 minutes ago             
r8cdsibuwsec   nginx-stack_nginx-web.3   nginx:1.19.3-alpine   guardwhy03   Running         Running 11 minutes ago             
ze7d0p8m8wx6   nginx-stack_nginx-web.4   nginx:1.19.3-alpine   guardwhy02   Running         Running 11 minutes ago             
itzy9fa87v50   nginx-stack_nginx-web.5   nginx:1.19.3-alpine   guardwhy03   Running         Running 11 minutes ago             
[root@guardwhy01 data]# 
```

5、删除stack服务，执行以下命令

```shell
[root@guardwhy01 data]# docker stack rm nginx-stack
Removing service nginx-stack_nginx-web
Removing network nginx-stack_nginx-net
[root@guardwhy01 data]# 
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210620004316.png)

6、小结

- networks中也可以不指定`driver:overlay`，因为docker swarm默认网络类型是overlay。
- 整个networks都可以不用配置，stack部署时会默认创建网络。定义网络在docker stack deploy时，会先默认创建一个网络。
- 注意一定要把镜像先拉取到本地然后再执行。

### 13.8 Stack和Compose区别

- Docker stack会忽略了==构建指令==，无法使用stack命令构建新镜像，它是需要镜像是预先已经构建好的。 所以`docker-compose`更适合于开发场景。
- Docker Compose是一个Python项目，它使用Docker API规范来操作容器。所以需要安装Docker -compose，以便与Docker一起在计算机上使用。
- Docker Stack功能包含在Docker引擎中，不需要安装额外的包来使用它。docker stacks 只是swarm mode的一部分。
- Docker stack不支持基于第2版写的`docker-compose.yml `，也就是version版本至少为3。然而Docker Compose对版本为2和3的 文件仍然可以处理。
- docker stack把docker compose的所有工作都做完了，因此docker stack将占主导地位。对于大多数用户来说，切换到使用docker stack既不困难，也不需要太多的开销。如果是Docker新手，或正在选择用于新项目的技术，请使用docker stack。