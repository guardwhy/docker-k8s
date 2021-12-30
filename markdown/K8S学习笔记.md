## 1-Kubernetes 是什么？

### 1.1 常见的云平台

**IaaS**【`Infrastructure as a Service`】：基础设施服务，常见平台阿里云。

**PaaS**【`platform as a service`】：平台即服务，常见平台如新浪云。

**SaaS**【`Software as a Service`】：软件即服务，常见平台Office365。

Kubernetes【`PaaS`】是一个可移植的、可扩展的开源平台，用于管理容器化的工作负载和服务，可促进声明式配置和自动化。 Kubernetes 拥有一个庞大且快速增长的生态系统。Kubernetes 的服务、支持和工具广泛可用。**Kubernetes** 这个名字源于希腊语，意为“舵手”或“飞行员”。k8s 这个缩写是因为 k 和 s 之间有八个字符的关系。 Google 在 2014 年开源了 Kubernetes 项目。Kubernetes 建立在 [Google 在大规模运行生产工作负载方面拥有十几年的经验](https://research.google/pubs/pub43438) 的基础上，结合了社区中最好的想法和实践。

### 1.2 为什么 Kubernetes 如此有用？

![](https://img-blog.csdnimg.cn/img_convert/6fbf5d1028679c491a5ce419c987b76a.png)



**1、传统部署**

早期，各个组织机构在物理服务器上运行应用程序。无法为物理服务器中的应用程序定义资源边界，这会导致资源分配问题。 例如，如果在物理服务器上运行多个应用程序，则可能会出现一个应用程序占用大部分资源的情况， 结果可能导致其他应用程序的性能下降。 一种解决方案是在不同的物理服务器上运行每个应用程序，但是由于资源利用不足而无法扩展， 并且维护许多物理服务器的成本很高。

**2、虚拟化部署**

作为解决方案，引入了虚拟化。虚拟化技术允许你在单个物理服务器的 CPU 上运行多个虚拟机【VM】。 虚拟化允许应用程序在 VM 之间隔离，并提供一定程度的安全，因为一个应用程序的信息 不能被另一应用程序随意访问。

虚拟化技术能够更好地利用物理服务器上的资源，并且因为可轻松地添加或更新应用程序 而可以实现更好的可伸缩性，降低硬件成本等等。

每个 VM 是一台完整的计算机，在虚拟化硬件之上运行所有组件，包括其自己的操作系统。

**容器化部署**

容器类似于 VM，但是它们具有被放宽的隔离属性，可以在应用程序之间共享操作系统【OS】。 因此，容器被认为是轻量级的。容器与 VM 类似，具有自己的文件系统、CPU、内存、进程空间等。 由于它们与基础架构分离，因此可以跨云和 OS 发行版本进行移植。容器因具有许多优势而变得流行起来。容器化部署的好处：

- 敏捷应用程序的创建和部署：与使用 `VM` 镜像相比，提高了容器镜像创建的简便性和效率。
- 持续开发、集成和部署：通过快速简单的回滚【由于镜像不可变性】，支持可靠且频繁的 容器镜像构建和部署。
- 关注开发与运维的分离：在构建/发布时而不是在部署时创建应用程序容器镜像， 从而将应用程序与基础架构分离。
- 可观察性不仅可以显示操作系统级别的信息和指标，还可以显示应用程序的运行状况和其他指标信号。
- 跨开发、测试和生产的环境一致性：在便携式计算机上与在云中相同地运行。
- 跨云和操作系统发行版本的可移植性：可在 `Ubuntu`、`RHEL`、`CoreOS`、本地、` Google Kubernetes Engine` 和其他任何地方运行。
- 以应用程序为中心的管理：提高抽象级别，从在虚拟硬件上运行` OS `到使用逻辑资源在` OS `上运行应用程序。
- 松散耦合、分布式、弹性、解放的微服务：应用程序被分解成较小的独立部分， 并且可以动态部署和管理 - 而不是在一台大型单机上整体运行。
- 资源隔离：可预测的应用程序性能，资源利用：高效率和高密度。

## 2-kubernetes vs Docker Swarm 

### 2.1 基本介绍

Docker是一种容器管理服务，帮助开发人员设计应用程序，使用容器能更容易地创建、部署和运行应用程序。Docker有一个用于集群容器的内置机制，称为==集群模式(swarm mode)==。使用集群模式，可以使用Docker引擎在多台机器上启动应用程序。Docker Swarm是Docker自己针对Docker容器的原生集群解决方案，它的优点是紧密集成到Docker的生态系统中，并且使用自己的API。它监视跨服务器集群的容器数量，是创建集群docker应用程序的最方便的方法，不需要额外的硬件。它为Dockerized应用程序提供了一个小型但有用的编排系统。

### 2.1 Docker Swarm优点

**更快的运行速度**

- 使用虚拟环境时，可能已经意识到它需要很长时间，并且包含了启动和启动您想要运行的应用程序的冗长过程。
- 对于`Docker Swarm`来说，这不再是一个问题。`DockerSwarm`不需要启动一个完整的虚拟机，就可以让应用程序在虚拟和软件定义的环境中快速运行，并有助于`DevOps`的实现。

**文档提供了所有的信息**

- `Docker`团队在文档方面非常突出! `Docker`正在快速发展，并且非常受欢迎。如果平台的一个版本在短时间间隔内发布，有些平台可能不维护文档。
- 但是`Docker Swarm`从不这样，如果一些信息只适用于`Docker Swarm`的特定版本，那么相应文档将确保更新了所有信息。

**快速简单的配置** 

- `Docker Swarm`的一个主要优点是它简化了问题。`Docker Swarm`使用户可以自己配置，将其放入代码中并轻松部署。
- 由于`Docker Swarm`可以在各种环境中使用，因此需求不受应用程序环境的约束。

**确保程序独立（容器间低耦合）**

- `Docker Swarm`负责将每个容器与其他容器隔离，并拥有自己的资源。可以部署各种容器，以便在不同的堆栈中运行单独的应用程序。
- 除此之外，`Docker Swarm`将在每个应用程序在自己的容器上运行时清除应用程序的删除。
- 如果不再需要应用程序，可以删除它的容器。它不会在您的主机OS上留下任何临时文件或配置文件。

**版本控制和组件重用**

- 使用`Docker Swarm`，可以跟踪容器的连续版本、检查差异或回滚到前面的版本。
- 容器重用来自前一层的组件，这使得它们非常轻量级。

### 2.2 Docker Swarm缺点

**Docker依赖于平台**:

- `Docker Swarm`是一个为`Linux`设计的平台。虽然`Docker`支持`Window`s和`MacOS X`，但它使用虚拟机在非`linux`平台上运行。
- 设计为在`Windows`上的`Docker`容器中运行的应用程序不能在`Linux`上运行，反之亦然。

**不提供存储选项**

`Docker Swarm`不提供将容器连接到存储的简便方法，这是主要缺点之一。

它的数据量需要对主机和手动配置进行大量的改进，如果想要`Docker Swarm`解决存储问题，也能办到，但是方式并不高效，且这种方式对用户并不友好。

**监控不良**:

`Docker Swarm`提供关于容器的基本信息，如果正在寻找基本的监控解决方案，那么使用Stats命令就足够了。

如果正在寻找先进的监控，那么`Docker`集群不是好的选择。虽然有像`CAdvisor`这样的第三方工具可以提供更多的监控，但是使用`Docker`本身实时收集更多关于容器的数据是不可行的。

==为了避免这些不足，这个时刻Kubernetes横空出世，当在多台机器上的多个容器中使用不同组件开发应用程序时，需要一个工具来管理和协调容器。这个时刻==
==在Kubernetes的帮助下解决问题！！！==

### 2.3 Kubernetes优点

`Kubernetes` 提供了一个可弹性运行分布式系统的框架，`Kubernetes `会满足扩展要求、故障转移、部署模式等。

**服务发现和负载均衡**

- `Kubernetes` 可以使用 `DNS` 名称或自己的 `IP` 地址公开容器，如果进入容器的流量很大，`Kubernetes `可以负载均衡并分配网络流量，从而使部署稳定。

**存储编排**

- `Kubernetes` 允许你自动挂载你选择的存储系统，例如本地存储、公共云提供商等。

**自动部署和回滚**

- 可以使用 `Kubernetes` 描述已部署容器的所需状态，它可以以受控的速率将实际状态 更改为期望状态。
- 可以自动化` Kubernetes `来为你的部署创建新容器， 删除现有容器并将它们的所有资源用于新容器。

**自动完成装箱计算**

- `Kubernetes` 允许你指定每个容器所需 `CPU` 和内存【`RAM`】。 当容器指定了资源请求时，`Kubernetes` 可以做出更好的决策来管理容器的资源。

**自我修复**

- `Kubernetes` 重新启动失败的容器、替换容器、杀死不响应用户定义的 运行状况检查的容器，并且在准备好服务之前不将其通告给客户端。

**密钥与配置管理**

- `Kubernetes` 允许你存储和管理敏感信息，例如密码、`OAuth` 令牌和 `ssh `密钥。 你可以在不重建容器镜像的情况下部署和更新密钥和应用程序配置，也无需在堆栈配置中暴露密钥。

### 2.4 Kubernetes缺点

1、基本介绍

`Kubernetes` 不是传统的、包罗万象的 `PaaS`【平台即服务】系统。 由于 `Kubernetes` 在容器级别而不是在硬件级别运行，它提供了 `PaaS` 产品共有的一些普遍适用的功能， 例如部署、扩展、负载均衡、日志记录和监视。 `Kubernetes` 不是单体系统，默认解决方案都是可选和可插拔的。 `Kubernetes` 提供了构建开发人员平台的基础，但是在重要的地方保留了用户的选择和灵活性。

2、相关缺点

**不限制支持的应用程序类型**。 

- `Kubernetes` 旨在支持极其多种多样的工作负载，包括无状态、有状态和数据处理工作负载。 
- 如果应用程序可以在容器中运行，那么它应该可以在 `Kubernetes `上很好地运行。

**不部署源代码，也不构建应用程序**。 

- 持续集成【`CI`】、交付和部署【`CI/CD`】工作流取决于组织的文化和偏好以及技术要求。

**不提供应用程序级别的服务作为内置服务**。

- 例如中间件【例如，消息中间件】、 数据处理框架【例如，`Spark`】、数据库【例如，`mysql`】、缓存、集群存储系统 【例如，`Ceph`】。
- 这样的组件可以在 `Kubernetes` 上运行，并且/或者可以由运行在 `Kubernetes `上的应用程序通过可移植机制来访问。

**不要求日志记录、监视或警报解决方案**。 

- 它提供了一些集成作为概念证明，并提供了收集和导出指标的机制。

**不提供或不要求配置语言/系统**。

- 它提供了声明性 `API`， 该声明性 `API `可以由任意形式的声明性规范所构成。

**不提供也不采用任何全面的机器配置、维护、管理或自我修复系统**。

- `Kubernetes` 不仅仅是一个编排系统，实际上它消除了编排的需要。 
- 编排的技术定义是执行已定义的工作流程：首先执行 `A`，然后执行 `B`，再执行 `C`。 相比之下`Kubernetes` 包含一组独立的、可组合的控制过程， 这些过程连续地将当前状态驱动到所提供的所需状态。 
- 如何从 `A `到` C `的方式无关紧要，也不需要集中控制，这使得系统更易于使用 且功能更强大、系统更健壮、更为弹性和可扩展。

### 2.5 Swarm vs  Kubernetes 小结

|                              | Docker Swarm                                                 | Kubernetes                                                   |
| ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 开发者                       | Docker 公司                                                  | 谷歌                                                         |
| 发布年份                     | 2013                                                         | 2014                                                         |
| 公司使用                     | Bugsnag，Bluestem Brands，<br/>Hammerhead，Code Picnic，Dialonce。 | Asana，Buffer，CircleCI，<br/>Evernote，Harvest，Intel，<br/>Starbucks，Shopify。 |
| Controller                   | Manager                                                      | Master                                                       |
| Storage                      | Volumes                                                      | Persistent and Epherma                                       |
| 公共云服务提供商             | Google，Azure，AWS，OTC                                      | Azure                                                        |
| 兼容性                       | 不那么广泛和可定制                                           | 更广泛和高度可定制                                           |
| 安装                         | 易于设置                                                     | 需要时间安装                                                 |
| 容差率                       | 低容错性                                                     | 高容错性                                                     |
| 大集群                       | 对于强集群状态考虑速度                                       | 在不考虑速度的情况下，即使在大型<br/>集群中也提供容器部署和扩展 |
| 负载均衡(Loading Balancing） | 当容器中的pod定义为服务时，提供负载平衡                      | 通过集群中的任何节点提供自动的内部负载平衡                   |
| 部署单位                     | Task                                                         | Pod                                                          |
| Port                         | Published Port                                               | Endpoint                                                     |
| 社区                         | 活跃的用户群，定期更新各种应用程序的映像                     | 获得开源社区和谷歌，亚马逊，微软和IBM等大公司的大力支持      |
| 缺点                         | 没有供应商的认证计划。大多数组织需要商业认证版本             | 倾向于开发人员而不是中央IT。                                 |
| 优点                         | 主要由可以决定产品方向的单一供应商控制。                     | 明确的市场领导者 最高的采用率。                              |
| Slave                        | Worker                                                       | Nodes                                                        |
| 容器设置                     | 功能由Docker API提供并受其限制                               | 客户端API和YAML， 在Kubernetes中是唯一的。                   |
| 可扩展性                     | 即使在大型容器中也可以快速部署容器。                         | 以牺牲速度为代价为集群状态提供强有力的保证。                 |

无论选择`Kubernetes`还是`Docker`，两者都被认为是最好的，并且有相当大的差异。在这两者之间做出选择的最好方法可能是考虑哪一个您已经比较熟悉，或者哪一个适合现有的软件堆栈。==如果需要开发复杂的应用程序，请使用Kubernetes==，==如果希望开发小型应用程序，请使用Docker Swarm==。此外，选择正确的项目是一项非常全面的任务，完全取决于项目需求和目标受众。

## 3-Kubernetes组件

1、一个 Kubernetes 集群由一组被称作节点的机器组成。这些节点上运行 Kubernetes 所管理的容器化应用。集群具有至少一个工作节点。

==工作节点托管作为应用负载的组件的 Pod== ，控制平面管理集群中的工作节点和 Pod 。 为集群提供故障转移和高可用性，这些控制平面一般跨多主机运行，集群跨多个节点运行。

![](https://img-blog.csdnimg.cn/img_convert/8cb3b812edba946a315c34965eb7c82c.png)

### 3.1 官方文档

1、kubernetes官网地址：[https://kubernetes.io/](https://kubernetes.io/)

![](https://img-blog.csdnimg.cn/img_convert/150b2bfbe7ff0d6d7e34982084a0768e.png)

2、kubernets中文社区地址：[https://www.kubernetes.org.cn/](https://www.kubernetes.org.cn/)

![](https://img-blog.csdnimg.cn/img_convert/4dfe6fffde0b29deeaa0a0cd35e786a4.png)

### 3.2 控制平面组件

控制平面的组件【`Control Plane Components`】对集群做出全局决策(比如调度)，以及检测和响应集群事件【例如，当不满足部署的replicas 字段时，启动新的 pod】，控制平面组件可以在集群中的任何节点上运行。然而，为了简单起见，设置脚本通常会在同一个计算机上启动所有控制平面组件，并且不会在此计算机上运行用户容器。

1、**kube-apiserver(所有服务访问统一入口)**

- 主节点上负责提供 Kubernetes API 服务的组件，它是 Kubernetes 控制面的前端，kube-apiserver是Kubernetes最重要的核心组件之一。
- 提供集群管理的REST API接口，包括认证授权，数据校验以及集群状态变更等
- 提供其他模块之间的数据交互和通信的枢纽（其他模块通过API Server查询或修改数据，只有API Server才直接操作etcd）
- 生产环境可以为apiserver做LA或LB。在设计上考虑了水平扩缩的需要。 换言之，通过部署多个实例可以实现扩缩。 参见构造高可用集群。

2、**etcd(键值对数据库  储存K8S集群所有重要信息(持久化)**

- etcd 是兼具一致性和高可用性的键值数据库，可以作为保存 Kubernetes 所有集群数据的后台数据库。Kubernetes 集群的 etcd 数据库通常需要有个备份计划，也可以使用外部的ETCD集群。

- kubernetes需要存储很多东西，像它本身的节点信息，组件信息，还有通过kubernetes运行的pod，deployment，service等等。都需要持久化。etcd就是它的数据中心。生产环境中为了保证数据中心的高可用和数据的一致性，一般会部署最少三个节点。
- 这里只部署一个节点在master，etcd也可以部署在kubernetes每一个节点，组成etcd集群。如果已经有etcd外部的服务，kubernetes直接使用外部etcd服务。

3、 **kube-scheduler(负责介绍任务，选择合适的节点进行分配任务)**

- 主节点上的组件，该组件监视那些新创建的未指定运行节点的 Pod，并选择节点让 Pod 在上面运行。
- kube-scheduler负责分配调度Pod到集群内的节点上，它监听kube-apiserver，查询还未分配Node的Pod，然后根据调度策略为这些Pod分配节点。

4、**kube-controller-manager(在主节点上运行控制器的组件)**

- ==Controller Manager由kube-controller-manager和cloud-controller-manager组成，是Kubernetes的大脑==，它通过apiserver监控整个集群的状态，并确保集群处于预期的工作状态。 
- kube-controller-manager由一系列的控制器组成，像`Replication Controller`控制副本，`Node Controller`节点控制，`Deployment Controller`管理`deployment`， `cloud-controller-manager`在Kubernetes启用`Cloud Provider`的时候才需要，用来配合云服务提供商的控制。

5、**云控制器管理器-(cloud-controller-manager)**

- cloud-controller-manager 运行与基础云提供商交互的控制器，cloud-controller-manager 二进制文件是 Kubernetes 1.6 版本中引入的 alpha 功能。
- cloud-controller-manager 仅运行云提供商特定的控制器循环。必须在 kube-controller-manager 中禁用这些控制器循环，可以通过在启动 kube-controller-manager 时将 --cloud-provider 参数设置为external 来禁用控制器循环。
- cloud-controller-manager 允许云供应商的代码和 Kubernetes 代码彼此独立地发展。在以前的版本中，核心的 Kubernetes 代码依赖于特定云提供商的代码来实现功能。在将来的版本中，云供应商专有的代码应由云供应商自己维护，并与运行 Kubernetes 的云控制器管理器相关联。

6、**kubectl(主节点上的组件)**

- kubectl是Kubernetes的命令行工具，是Kubernetes用户和管理员必备的管理工具。
- kubectl提供了大量的子命令，方便管理Kubernetes集群中的各种功能。

### 3.3 Node 组件

节点组件在每个节点上运行，维护运行的 Pod 并提供 Kubernetes 运行环境。

1、**kubelet(直接跟容器引擎交互实现容器的生命周期管理)**

- 一个在集群中每个节点上运行的代理。它保证容器都运行在 Pod 中。
- 一个在集群中每个工作节点上都运行一个kubelet服务进程，默认监听10250端口，接收并执行master发来的指令，管理Pod及Pod中的容器。
- 每个kubelet进程会在API Server上注册节点自身信息，定期向master节点汇报节点的资源使用情况，并通过cAdvisor监控节点和容器的资源。

2、**kube-proxy(负责写入规则至 IPTABLES、IPVS 实现服务映射访问的)**

- 一个在集群中每台工作节点上都应该运行一个kube-proxy服务，它监听API server中service和endpoint的变化情况，并通过iptables等来为服务配置负载均衡，是让我们的服务在集群外可以被访问到的重要方式。

3、 **容器运行环境(Container Runtime)**

- 容器运行环境是负责运行容器的软件。
- Kubernetes 支持多个容器运行环境: Docker、 containerd、cri-o、 rktlet 以及任何实现 `Kubernetes CRI `(容器运行环境接口)。

### 3.4 插件(Addons)

插件使用 Kubernetes 资源 (DaemonSet, Deployment等) 实现集群功能。因为这些提供集群级别的功能，所以插件的命名空间资源属于 kube-system 命名空间。
所选的插件如下所述：有关可用插件的扩展列表，请参见插件 (Addons)。

1、**KUBE-DNS**

`kube-dns`为Kubernetes集群提供命名服务，主要用来解析集群服务名和`Pod的hostname`。目的是让pod可以通过名字访问到集群内服务。它通过添加A记录的方式实现名字和service的解析。普通的service会解析到service-ip，headless service会解析到pod列表。

2、**用户界面(Dashboard)**
Dashboard 是 Kubernetes 集群的通用基于 Web 的 UI。它使用户可以管理集群中运行的应用程序以及集群本身并进行故障排除。

3、**容器资源监控**
容器资源监控将关于容器的一些常见的时间序列度量值保存到一个集中的数据库中，并提供用于浏览这些数据的界面。

4、 **集群层面日志**
集群层面日志 机制负责将容器的日志数据保存到一个集中的日志存储中，该存储能够提供搜索和浏览接口。

## 4-Kubernetes安装与配置

### 4.1 硬件要求

| 序列号 | 硬件 | 基本要求 |
| ------ | ---- | -------- |
| 1      | CPU  | 至少2核  |
| 2      | 内存 | 至少4G   |
| 3      | 硬盘 | 至少40G  |

购买5台阿里云服务器(镜像推荐centos7.8)，推荐按量付费！！！

购买阿里云服务器，参考文档:[https://blog.csdn.net/hxy1625309592/article/details/118062280](https://blog.csdn.net/hxy1625309592/article/details/118062280)

![](https://img-blog.csdnimg.cn/img_convert/ff7faab8c8343f708bb023ebecc3f69a.png)

服务器名称和私服地址

| 主机名       | IP地址         |
| ------------ | -------------- |
| k8s-master01 | 172.21.251.255 |
| harbor-01    | 172.21.251.254 |
| k8s-node01   | 172.21.252.0   |
| k8s-node02   | 172.21.252.1   |
| k8s-node03   | 172.21.252.2   |

### 4.2 CentOS源配置

1、查看centos系统版本命令

```shell
cat /etc/centos-release
```

​	![](https://img-blog.csdnimg.cn/img_convert/23e24f8af3bab9bc91f8d5d747b5e59c.png)

2、配置阿里云yum源

```shell
1.下载安装wget
yum install -y wget

2.备份默认的yum
mv /etc/yum.repos.d /etc/yum.repos.d.backup

3.设置新的yum目录
mkdir -p /etc/yum.repos.d

4.下载阿里yum配置到该目录中，选择对应版本
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

5.更新epel源为阿里云epel源
mv /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel.repo.backup
mv /etc/yum.repos.d/epel-testing.repo /etc/yum.repos.d/epel-testing.repo.backup
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo

6.重建缓存
yum clean all
yum makecache
```

3、升级Linux系统内核。

```shell
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm 
yum --enablerepo=elrepo-kernel install -y kernel-lt 
grep initrd16 /boot/grub2/grub.cfg 
grub2-set-default 0

重启系统: reboot
```

![](https://img-blog.csdnimg.cn/img_convert/c10ecd1fd98ea2a858e83a1e1fadfe91.png)	

4、查看centos系统内核

```shell
uname -r
uname -a
```

5、更新一下软件包

```shell
yum repolist
yum update
```

![](https://img-blog.csdnimg.cn/img_convert/8920e58b71ea5ea20f4a018224de5c33.png)

6、阿里云实例关机以后，内核会从新回到旧内核，所以需要从新设置centos7切换启动内核。

```shell
# 查看当前系统内核
[root@k8smaster01 ~]# uname -r
3.10.0-1160.31.1.el7.x86_64

# 查看可使用的内核列表
[root@k8smaster01 ~]# awk -F\' '$1=="menuentry " {print i++ " : " $2}' /etc/grub2.cfg
0 : CentOS Linux (3.10.0-1160.31.1.el7.x86_64) 7 (Core)
1 : CentOS Linux (5.4.127-1.el7.elrepo.x86_64) 7 (Core)
2 : CentOS Linux (0-rescue-20200914151306980406746494236010) 7 (Core)
# 查看当前默认内核启动项
[root@k8smaster01 ~]# grub2-editenv list

# 即系统当前启动时默认加载的内核是 CentOS Linux (3.10.0-1160.31.1.el7.x86_64) 7 (Core)
saved_entry=CentOS Linux (3.10.0-1160.31.1.el7.x86_64) 7 (Core)

# 更改默认启动内核项
[root@k8smaster01 ~]# grub2-set-default 1

# 再次查看默认内核启动项，发现saved_entry字段变为1
[root@k8smaster01 ~]# grub2-editenv list
saved_entry=1

# 重启系统
[root@k8smaster01 ~]# reboot

## 查看当前系统内核，可以看到当前系统的内核已经更改！！！
[root@k8smaster01 ~]# uname -r
5.4.127-1.el7.elrepo.x86_64
```
![](https://img-blog.csdnimg.cn/img_convert/72fc161eb9407ca85ad063a7359c514f.png)
### 4.3 docker安装前置条件

1、查看内存命令

```shell
free
free -h
```

2、查看硬盘信息

```shell
fdisk -l 
```
![](https://img-blog.csdnimg.cn/img_convert/6945f47654d869f6b25bf33d266050a0.png)
3、关闭防火墙

```shell
systemctl stop firewalld
systemctl disable firewalld
```

4、关闭selinux

```shell
[root@k8smaster01 ~]# sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
[root@k8smaster01 ~]# setenforce 0
setenforce: SELinux is disabled
[root@k8smaster01 ~]# 
```

5、网桥过滤

```shell
vim /etc/sysctl.conf
# 添加以下网桥
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-arptables = 1
net.ipv4.ip_forward=1
net.ipv4.ip_forward_use_pmtu = 0
# 生效命令
sysctl --system
# 查看效果
sysctl -a|grep "ip_forward"
```
![](https://img-blog.csdnimg.cn/img_convert/dbb1008829ab6ad2272536712994450f.png)
6、开启IPVS

```shell
# 安装IPVS
yum -y install ipset ipvsdm

# 编译ipvs.modules文件
vi /etc/sysconfig/modules/ipvs.modules

# 文件内容如下
#!/bin/bash
modprobe -- ip_vs
modprobe -- ip_vs_rr
modprobe -- ip_vs_wrr
modprobe -- ip_vs_sh
modprobe -- nf_conntrack

# 赋予权限并执行
chmod 755 /etc/sysconfig/modules/ipvs.modules && bash /etc/sysconfig/modules/ipvs.modules && lsmod |grep -e ip_vs -e nf_conntrack_ipv4
```
![](https://img-blog.csdnimg.cn/img_convert/6c69ca73671831e2e507ad42e6bebca5.png)

```shell
# 重启电脑，检查是否生效
reboot
# 查看结果
lsmod | grep ip_vs_rr
```
![](https://img-blog.csdnimg.cn/img_convert/c9674849e7e5708fcf8bd55a6eb4db1e.png)
7、同步时间

```shell
#安装软件
yum -y install ntpdate

# 向阿里云服务器同步时间
ntpdate time1.aliyun.com

# 删除本地时间并设置时区为上海
rm -rf /etc/localtime
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# 查看时间
date -R || date
```
![](https://img-blog.csdnimg.cn/img_convert/71e40d4dd11750f632eca4d044c19005.png)
8、命令补全

```shell
#安装bash-completion
yum -y install bash-completion bash-completion-extras

#使用bash-completion
source /etc/profile.d/bash_completion.sh
```
9、关闭swap分区

```shell
# 临时关闭
swapoff -a

# 永久关闭
vi /etc/fstab

# 将文件中的/dev/mapper/centos-swap这行代码注释掉
#/dev/mapper/centos-swap swap swap  defaults    0 0

# 确认swap已经关闭：若swap行都显示 0 则表示关闭成功
free -m
```
![](https://img-blog.csdnimg.cn/img_convert/bc557151f8107e6d60ca545bfbdbe007.png)10、hosts配置

```shell
[root@k8s-master01 ~]# vim /etc/hosts
[root@k8s-master01 ~]#  cat /etc/hosts
::1	localhost	localhost.localdomain	localhost6	localhost6.localdomain6
127.0.0.1		localhost	    	localhost.localdomain	localhost4	localhost4.localdomain4

192.168.50.133	k8s-master01	    k8s-master01
192.168.50.134	k8s-node01          k8s-node01
192.168.50.135	k8s-node02    	    k8s-node02
192.168.50.136	k8s-node03    	    k8s-node03
192.168.50.137	k8s-harbor01  	    k8s-harbor01
192.168.50.138  k8s-jenkinsagent01  k8s-jenkinsagent01
192.168.50.139  k8s-gitlab01  	    k8s-gitlab01
192.168.50.132  k8s-jenkins01 	    k8s-jenkins01

[root@k8s-master01 ~]# 

## 再次重新启动
[root@k8smaster01 ~]# reboot
```
### 4.4 安装docker

1、yum安装gcc相关环境

```shell
yum -y install gcc
yum -y install gcc-c++
```

2、yum 包更新到最新

```shell
yum update
```

3、安装需要的软件包，提供yum-config-manager功能，另外两个是devicemapper驱动依赖的。

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
```

4、添加阿里源

```shell
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

yum makecache fast
```

5、查看docker更新版本

```shell
yum list docker-ce --showduplicates | sort -r 
```

6、安装docker最新版本

```shell
yum -y install docker-ce
```

7、安装后查看docker版本

```shell
docker -v
```

8、启动docker

```shell
systemctl start docker
```

9、开机启动

```shell
systemctl enable docker
```
![](https://img-blog.csdnimg.cn/img_convert/acb81f94e95241b1a879ca4b8229ab13.png)
### 4.5 阿里云镜像加速

1、先注册一个阿里云账号。

2、查看阿里云，官方文档: [https://cr.console.aliyun.com/cn-qingdao/instances/mirrors](https://cr.console.aliyun.com/cn-qingdao/instances/mirrors)

3、进入管理控制台设置密码，开通。

4、查看属于自己的加速器

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606163908.png" style="zoom:80%;" />

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
<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/javaEE/SpringMVC/Test4/20210606201506.png" style="zoom: 80%;" />

7、修改Cgroup Driver

```shell
# 修改daemon.json，新增文件
[root@k8smaster01 ~]# vim /etc/docker/daemon.json 
[root@k8smaster01 ~]# cat /etc/docker/daemon.json 
{
  "registry-mirrors": ["https://5bsomu6l.mirror.aliyuncs.com"],
  "exec-opts": ["native.cgroupdriver=systemd"]
}
[root@k8smaster01 ~]# systemctl daemon-reload
[root@k8smaster01 ~]# systemctl restart docker
[root@k8smaster01 ~]# docker info | grep Cgroup
 Cgroup Driver: systemd
 Cgroup Version: 1
[root@k8smaster01 ~]# docker info
```

注意: **修改cgroupdriver是为了消除安装k8s集群时的告警！！！！**

```css
[WARNING IsDockerSystemdCheck]:
detected “cgroupfs” as the Docker cgroup driver. The recommended driver is “systemd”.
Please follow the guide at https://kubernetes.io/docs/setup/cri/......
```
### 4.6 kubeadm快速安装

1、安装yum源

| 软件名称 | kubeadm                         | kubelet                                                  | kubectl                       | docker-ce              |
| -------- | ------------------------------- | -------------------------------------------------------- | ----------------------------- | ---------------------- |
| 软件版本 | 初始化集群管理集群 版本：1.17.5 | 用于接收api-server指令，对pod生命周期进行管理版本:1.17.5 | 集群命令行管理工具 版本1.17.5 | Docker version 20.10.7 |

新建repo文件

```shell
vim /etc/yum.repos.d/kubernates.repo 
```

2、文件内容

```shell
[root@k8smaster01 ~]# vim /etc/yum.repos.d/kubernates.repo 
[root@k8smaster01 ~]# cat /etc/yum.repos.d/kubernates.repo 
[kubernetes]
name=Kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
	https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
[root@k8smaster01 ~]# 
```

3、更新缓存

```yaml
yum clean all
yum -y makecache
```

4、验证源是否可用

```shell
[root@k8smaster01 ~]# yum list | grep kubeadm
kubeadm.x86_64                           1.21.2-0                      kubernetes
[root@k8smaster01 ~]
```
![](https://img-blog.csdnimg.cn/img_convert/e68f19ce659b1e336fdfa18f31af246c.png)
5、查看k8s版本

```shell
yum list kubelet --showduplicates | sort -r 
```

6、安装k8s-1.17.5

```shell
yum install -y kubelet-1.17.5-0 kubeadm-1.17.5-0 kubectl-1.17.5-0
```

**报错！！！**
![](https://img-blog.csdnimg.cn/img_convert/1d1a69cfee4c402f8c43d026109f6787.png)
7、解决方案

```shell
[root@k8smaster01 ~]# wget https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
--2021-06-22 17:32:32--  https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
Resolving mirrors.aliyun.com (mirrors.aliyun.com)... 14.215.172.221, 14.215.172.219, 14.215.172.216, ...
Connecting to mirrors.aliyun.com (mirrors.aliyun.com)|14.215.172.221|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3516 (3.4K) [application/octet-stream]
Saving to: ‘yum-key.gpg’

100%[=================================================================>] 3,516       --.-K/s   in 0.005s  

2021-06-22 17:32:32 (722 KB/s) - ‘yum-key.gpg’ saved [3516/3516]

[root@k8smaster01 ~]# wget https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
--2021-06-22 17:32:46--  https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
Resolving mirrors.aliyun.com (mirrors.aliyun.com)... 14.215.172.219, 14.215.172.216, 14.215.172.221, ...
Connecting to mirrors.aliyun.com (mirrors.aliyun.com)|14.215.172.219|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 975 [application/octet-stream]
Saving to: ‘rpm-package-key.gpg’

100%[=================================================================>] 975         --.-K/s   in 0s      

2021-06-22 17:32:46 (118 MB/s) - ‘rpm-package-key.gpg’ saved [975/975]

[root@k8smaster01 ~]# rpm --import yum-key.gpg
[root@k8smaster01 ~]# rpm --import rpm-package-key.gpg
```

重新执行命令，安装成功！！！

```shell
yum install -y kubelet-1.17.5 kubeadm-1.17.5 kubectl-1.17.5
```

![](https://img-blog.csdnimg.cn/img_convert/520e7f55bbab619d51f236f58125286a.png)
### 4.7 设置kubelet

1、增加配置信息

注意: ==如果不配置kubelet，可能会导致K8S集群无法启动。为实现docker使用的cgroupdriver与kubelet使用的cgroup的一致性==。

```shell
[root@k8smaster01 ~]# vim /etc/sysconfig/kubelet
[root@k8smaster01 ~]# cat /etc/sysconfig/kubelet
KUBELET_EXTRA_ARGS="--cgroup-driver=systemd"
[root@k8smaster01 ~]# 
```
2、设置开机自行启动

```shell
systemctl enable kubelet 
```
![](https://img-blog.csdnimg.cn/img_convert/4fca3d7200356a5876aec3140b3d3e3c.png)
### 4.8 初始化镜像

1、查看安装集群需要的镜像

```shell
kubeadm config images list
```
![](https://img-blog.csdnimg.cn/img_convert/dbac13981226d935745356acb6f49748.png)
2、编写执行镜像的脚本

```shell
# 创建data文件夹
[root@k8smaster01 home]# mkdir data
[root@k8smaster01 home]# ls
data
[root@k8smaster01 home]# cd data/
# 创建init.h脚本
[root@k8smaster01 data]# vim init.sh
# 给脚本授权
[root@k8smaster01 data]# chmod 777 init.sh 
[root@k8smaster01 data]# ls
init.sh
[root@k8smaster01 data]# cat init.sh
#!/bin/bash
images=(
 kube-apiserver:v1.17.5
 kube-controller-manager:v1.17.5
 kube-scheduler:v1.17.5
 kube-proxy:v1.17.5
 pause:3.1
 etcd:3.4.3-0
 coredns:1.6.5
)
for imageName in ${images[@]} ;
do
 docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName
 docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName k8s.gcr.io/$imageName
 docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName
done
[root@k8smaster01 data]# ls
init.sh
## 执行脚本
[root@k8smaster01 data]# ./init.sh 
```
![](https://img-blog.csdnimg.cn/img_convert/7be1029da40d63112fc04ecb3216cd60.png)

3、打包Kubernetes集群所需的镜像！！！

```shell
[root@k8smaster01 data]# docker save -o k8s.1.17.5.tar \
k8s.gcr.io/kube-proxy:v1.17.5 \
k8s.gcr.io/kube-apiserver:v1.17.5 \
k8s.gcr.io/kube-controller-manager:v1.17.5 \
k8s.gcr.io/kube-scheduler:v1.17.5 \
k8s.gcr.io/coredns:1.6.5 \
k8s.gcr.io/etcd:3.4.3-0 \
k8s.gcr.io/pause:3.1
[root@k8smaster01 data]# ls
init.sh  k8s.1.17.5.tar
[root@k8smaster01 data]# 
```
### 4.9 导入镜像

1、导入`k8s-master01`相关镜像

```shell
[root@k8s-master01 data]# ls
init.sh  k8s.1.17.5.tar
[root@k8s-master01 data]# docker load -i k8s.1.17.5.tar 
Loaded image: k8s.gcr.io/kube-scheduler:v1.17.5
Loaded image: k8s.gcr.io/coredns:1.6.5
Loaded image: k8s.gcr.io/etcd:3.4.3-0
Loaded image: k8s.gcr.io/pause:3.1
Loaded image: k8s.gcr.io/kube-proxy:v1.17.5
Loaded image: k8s.gcr.io/kube-apiserver:v1.17.5
Loaded image: k8s.gcr.io/kube-controller-manager:v1.17.5
[root@k8s-master01 data]# docker images
REPOSITORY                           TAG       IMAGE ID       CREATED         SIZE
k8s.gcr.io/kube-proxy                v1.17.5   e13db435247d   14 months ago   116MB
k8s.gcr.io/kube-controller-manager   v1.17.5   fe3d691efbf3   14 months ago   161MB
k8s.gcr.io/kube-apiserver            v1.17.5   f640481f6db3   14 months ago   171MB
k8s.gcr.io/kube-scheduler            v1.17.5   f648efaff966   14 months ago   94.4MB
k8s.gcr.io/coredns                   1.6.5     70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                      3.4.3-0   303ce5db0e90   20 months ago   288MB
k8s.gcr.io/pause                     3.1       da86e6ba6ca1   3 years ago     742kB
[root@k8s-master01 data]# 
```

2、导入所有node节点相关镜像

- `docker load -i k8s.1.17.5.node.tar`
- 所有node节点只需要`kube-proxy:v1.17.5`和`pause:3.1`这两个镜像。

```shell
[root@k8s-node01 data]# ls
k8s.1.17.5.node.tar
[root@k8s-node01 data]# docker -v
Docker version 20.10.7, build f0df350
[root@k8s-node01 data]# docker load -i k8s.1.17.5.node.tar 
fc4976bd934b: Loading layer  53.88MB/53.88MB
682fbb19de80: Loading layer  21.06MB/21.06MB
2dc2f2423ad1: Loading layer  5.168MB/5.168MB
ad9fb2411669: Loading layer  4.608kB/4.608kB
597151d24476: Loading layer  8.192kB/8.192kB
0d8d54147a3a: Loading layer  8.704kB/8.704kB
b5d12e5fbf44: Loading layer  37.81MB/37.81MB
Loaded image: k8s.gcr.io/kube-proxy:v1.17.5
e17133b79956: Loading layer  744.4kB/744.4kB
Loaded image: k8s.gcr.io/pause:3.1
[root@k8s-node01 data]# docker images
REPOSITORY              TAG       IMAGE ID       CREATED         SIZE
k8s.gcr.io/kube-proxy   v1.17.5   e13db435247d   14 months ago   116MB
k8s.gcr.io/pause        3.1       da86e6ba6ca1   3 years ago     742kB
[root@k8s-node01 data]# 
```
### 4.10 初始化集群

1、calico官网地址

官网下载地址: [https://docs.projectcalico.org/v3.14/manifests/calico.yaml](https://docs.projectcalico.org/v3.14/manifests/calico.yaml)

calico github地址：[https://github.com/projectcalico/calico](https://github.com/projectcalico/calico)

相关镜像下载

```yml
docker pull calico/cni:v3.14.2
docker pull calico/pod2daemon-flexvol:v3.14.2
docker pull calico/node:v3.14.2
docker pull calico/kube-controllers:v3.14.2
```

2、主节点(`k8s-master01`)所需的镜像

```shell
[root@k8s-master01 data]# docker images
REPOSITORY                           TAG       IMAGE ID       CREATED         SIZE
calico/node                          v3.14.2   780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol            v3.14.2   9dfa8f25b51c   11 months ago   22.8MB
calico/cni                           v3.14.2   e6189009f081   11 months ago   119MB
calico/kube-controllers              v3.14.2   4815e4106d26   11 months ago   52.8MB
k8s.gcr.io/kube-proxy                v1.17.5   e13db435247d   14 months ago   116MB
k8s.gcr.io/kube-controller-manager   v1.17.5   fe3d691efbf3   14 months ago   161MB
k8s.gcr.io/kube-apiserver            v1.17.5   f640481f6db3   14 months ago   171MB
k8s.gcr.io/kube-scheduler            v1.17.5   f648efaff966   14 months ago   94.4MB
k8s.gcr.io/coredns                   1.6.5     70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                      3.4.3-0   303ce5db0e90   20 months ago   288MB
k8s.gcr.io/pause                     3.1       da86e6ba6ca1   3 years ago     742kB
[root@k8s-master01 data]#
```

配置hostname

```shell
hostnamectl set-hostname k8s-master01
```

配置ip地址

```shell
[root@k8s-master01 data]# hostnamectl set-hostname k8s-master01
[root@k8s-master01 data]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

192.168.50.133	k8s-master01	k8s-master01
192.168.50.135	k8s-node01      k8s-node01
192.168.50.136	k8s-node02      k8s-node02
192.168.50.134	k8s-node03      k8s-node03
192.168.50.137	k8s-harbor01    k8s-harbor01
[root@k8s-master01 data]# 
```

导入`calico.yaml`文件到`/home/data`目录

![](https://img-blog.csdnimg.cn/img_convert/b55dd48c90e8127423416013b30a79d8.png)
3、初始化集群信息calico网络

```shell
kubeadm init --apiserver-advertise-address=192.168.50.133 \
--kubernetes-version v1.17.5 \
--service-cidr=10.1.0.0/16 \
--pod-network-cidr=10.81.0.0/16
```
<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210704144231.png" style="zoom:80%;" />

4、执行配置命令

```shell
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

5、所有的node节点加入集群信息

```shell
kubeadm join 192.168.50.133:6443 --token 42j7xo.5kqfx7o6q519d7xr \
    --discovery-token-ca-cert-hash sha256:4e803c3a62eba304d9262a79b3544fe5a124b6f32f4589c3f27c1d0987106e9a 
```
<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210704145105.png" style="zoom: 80%;" />

加入成功，查看所有集群节点！！！

```shell
kubectl get nodes
```
![](https://img-blog.csdnimg.cn/img_convert/62c18c101f764c34adde7e14afe491c4.png)
6、初始化网络。

```shell
kubectl  apply -f 
```

查看网络状态

```shell
[root@k8s-master01 data]# kubectl  apply -f  calico.yml 
serviceaccount/calico-kube-controllers created
## 查看节点
[root@k8s-master01 data]# kubectl get nodes
NAME           STATUS   ROLES    AGE    VERSION
k8s-master01   Ready    master   113m   v1.17.5
k8s-node01     Ready    <none>   103m   v1.17.5
k8s-node02     Ready    <none>   98m    v1.17.5
k8s-node03     Ready    <none>   98m    v1.17.5
## 监控状态！！！！
[root@k8s-master01 data]# kubectl get nodes -w
NAME           STATUS   ROLES    AGE    VERSION
k8s-master01   Ready    master   113m   v1.17.5
k8s-node01     Ready    <none>   103m   v1.17.5
k8s-node02     Ready    <none>   98m    v1.17.5
k8s-node03     Ready    <none>   98m    v1.17.5
k8s-node01     Ready    <none>   103m   v1.17.5
```
7、kubectl命令自动补全

```shell
[root@k8s-master01 data]# echo "source <(kubectl completion bash)" >> ~/.bash_profile
[root@k8s-master01 data]# source ~/.bash_profile
[root@k8s-master01 data]# 
```

## 5-什么是NameSpace？

- 俗称命名空间，可以单纯的认为`namespaces`是kubernetes集群中的虚拟化集群。在一个Kubernetes集群中可以拥有多个命名空间，它们在逻辑上彼此隔离。 可以为你提供组织，安全甚至性能方面的帮助！
- Namespace是对一组资源和对象的抽象集合，比如可以用来将系统内部的对象划分为不同的项目组或用户组。==常见的pods, services, replication controllers和deployments等都是属于某一个namespace的（默认是default），而node, persistentVolumes等则不属于任何namespace==。

大多数的Kubernetes中的集群默认会有一个叫default的`namespace`。然而实际上存在4个`namespace`。

- default：资源默认被创建于default命名空间。
- kube-system：kubernetes系统组件使用。
- kube-node-lease: kubernetes集群节点租约状态。
- kube-public：公共资源使用，但实际上现在并不常用。

这个默认(default)的namespace并没什么特别，但是不能删除它。这很适合刚刚开始使用kubernetes和一些小的产品系统。但不建议应用于大型生产系统。因为这种复杂系统中，团队会非常容易意外地或者无意识地重写或者中断其他服务service。相反，创建多个命名空间来把service(服务)分割成更容易管理的块。

**(default)的namespace基本作用**：

多租户情况下，实现资源隔离。
属于逻辑隔离，属于管理边界，不属于网络边界。
可以针对每个namespace做资源配额。

### 5.1 查看命名空间

1、具体命令

```shell
## 查看命名空间
kubectl get namespace

## 查看所有命名空间的pod资源
kubectl get pod --all-namespaces
kubectl get pod -A

## 简写命令(查看命名空间)
kubectl get ns
```

查询结果！！！

```shell
## 1、查看命名空间
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   169m
kube-node-lease   Active   169m
kube-public       Active   169m
kube-system       Active   169m
## 2、查看所有命名空间的pod资源
[root@k8s-master01 data]# kubectl get pod --all-namespaces
NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-6b94766748-pn4l8   1/1     Running   0          78m
kube-system   calico-node-4m62k                          1/1     Running   0          78m
kube-system   calico-node-7bnqj                          1/1     Running   0          78m
kube-system   calico-node-krh64                          1/1     Running   0          78m
kube-system   calico-node-zwvv9                          1/1     Running   0          78m
kube-system   coredns-6955765f44-nwzg6                   1/1     Running   0          169m
kube-system   coredns-6955765f44-rdwnc                   1/1     Running   0          169m
kube-system   etcd-k8s-master01                          1/1     Running   1          169m
kube-system   kube-apiserver-k8s-master01                1/1     Running   1          169m
kube-system   kube-controller-manager-k8s-master01       1/1     Running   1          169m
kube-system   kube-proxy-4vdxm                           1/1     Running   1          159m
kube-system   kube-proxy-5nlqn                           1/1     Running   1          154m
kube-system   kube-proxy-npzs2                           1/1     Running   1          169m
kube-system   kube-proxy-z47rt                           1/1     Running   1          154m
kube-system   kube-scheduler-k8s-master01                1/1     Running   1          169m
## 3、查看命名空间
[root@k8s-master01 data]# kubectl get ns
NAME              STATUS   AGE
default           Active   169m
kube-node-lease   Active   169m
kube-public       Active   169m
kube-system       Active   169m
[root@k8s-master01 data]# 
```

3、命名空间说明

```yaml
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   169m	# 用户创建的pod默认在此命名空间
kube-node-lease   Active   169m # 所有用户均可以访问，包括未认证用户
kube-public       Active   169m # kubernetes集群节点租约状态
kube-system       Active   169m # kubernetes集群在使用
```

### 5.2 NameSpace相关操作

1、创建NameSpace

```shell
kubectl create namespace guardwhy01
-- 简写命令
kubectl create ns guardwhy02
```

2、删除NameSpace

```shell
kubectl delete namespace guardwhy01
-- 简写命令
kubectl delete ns guardwhy02
```

3、执行结果！！！

```shell
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   3h7m
kube-node-lease   Active   3h7m
kube-public       Active   3h7m
kube-system       Active   3h7m
[root@k8s-master01 data]# kubectl create namespace guardwhy01
namespace/guardwhy01 created
[root@k8s-master01 data]# kubectl create ns guardwhy02
namespace/guardwhy02 created
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   3h8m
guardwhy01        Active   36s
guardwhy02        Active   5s
kube-node-lease   Active   3h8m
kube-public       Active   3h8m
kube-system       Active   3h8m
[root@k8s-master01 data]# kubectl delete namespace guardwhy01
namespace "guardwhy01" deleted
[root@k8s-master01 data]# kubectl delete ns guardwhy02
namespace "guardwhy02" deleted
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   3h12m
kube-node-lease   Active   3h12m
kube-public       Active   3h12m
kube-system       Active   3h12m
[root@k8s-master01 data]# 
```

## 6- 什么是pod？

Pod是kubernetes集群能够调度的最小单元，Pod是容器的封装 。在Kubernetes集群中，Pod是所有业务类型的基础，也是K8S管理的最小单位级，它是一个或多个容器的组合。这些容器共享存储、网络和命名空间，以及如何运行的规范。在Pod中，所有容器都被同一安排和调度，并运行在共享的上下文中。对于具体应用而言，Pod是它们的逻辑主机，Pod包含业务相关的多个应用容器。

### 6.1 Pod的基本特点

**网络**:每一个Pod都会被指派一个唯一的Ip地址，在Pod中的每一个容器共享网络命名空间，包括Ip地址和网络端口。在同一个Pod中的容器可以和localhost进行互相通信。当Pod中的容器需要与Pod外的实体进行通信时，则需要通过端口等共享的网络资源。

**存储**:Pod能够被指定共享存储卷的集合，在Pod中所有的容器能够访问共享存储卷，允许这些容器共享数据。存储卷也允许在一个Pod持久化数据，以防止其中的容器需要被重启。

### 6.2 Pod的工作方式

1、K8s一般不直接创建Pod，而是通过控制器和模版配置来管理和调度。

2、**Pod重启**：在Pod中的容器可能会由于异常等原因导致其终止退出，Kubernetes提供了重启策略以重启容器。重启策略对同一个Pod的所有容器起作用，容器的重启由Node上的kubelet执行。Pod支持三种重启策略，在配置文件中通过`restartPolicy`字段设置重启策略。

```shell
Always：只要退出就会重启。
OnFailure：只有在失败退出（exit code不等于0）时，才会重启。
Never：只要退出，就不再重启
```

==注意，这里的重启是指在Pod的宿主Node上进行本地重启，而不是调度到其它Node上==。

3、资源限制

Kubernetes通过cgroups限制容器的CPU和内存等计算资源，包括requests(请求，调度器保证调度到资源充足的Node上)和limits(上限)。

### 6.3 Pod基本操作

1、查看Pod，执行以下命令

```shell
-- 1、查看default命名空间下的pods
kubectl get pods

-- 2、查看kube-system命名空间下的pods
kubectl get pods -n kube-system

-- 3、查看所有命名空间下的pods
kubectl get pod --all-namespaces
kubectl get pod -A
```

2、创建Pod

下载tomcat相关的镜像

```shell
[root@k8s-master01 data]# docker pull tomcat:9.0.37-jdk8-openjdk-slim
[root@k8s-master01 data]# docker pull tomcat:9.0.20-jre8-alpine
[root@k8s-master01 data]# docker pull tomcat:9.0.37-jdk8
[root@k8s-master01 data]# docker images
REPOSITORY                           TAG                        IMAGE ID       CREATED         SIZE
tomcat                               9.0.37-jdk8-openjdk-slim   d60b68827676   9 months ago    305MB
tomcat                               9.0.37-jdk8                9c7be7b021c3   9 months ago    531MB
calico/node                          v3.14.2                    780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol            v3.14.2                    9dfa8f25b51c   11 months ago   22.8MB
calico/cni                           v3.14.2                    e6189009f081   11 months ago   119MB
calico/kube-controllers              v3.14.2                    4815e4106d26   11 months ago   52.8MB
k8s.gcr.io/kube-proxy                v1.17.5                    e13db435247d   14 months ago   116MB
k8s.gcr.io/kube-apiserver            v1.17.5                    f640481f6db3   14 months ago   171MB
k8s.gcr.io/kube-controller-manager   v1.17.5                    fe3d691efbf3   14 months ago   161MB
k8s.gcr.io/kube-scheduler            v1.17.5                    f648efaff966   14 months ago   94.4MB
k8s.gcr.io/coredns                   1.6.5                      70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                      3.4.3-0                    303ce5db0e90   20 months ago   288MB
tomcat                               9.0.20-jre8-alpine         387f9d021d3a   2 years ago     108MB
k8s.gcr.io/pause                     3.1                        da86e6ba6ca1   3 years ago     742kB
[root@k8s-master01 data]# 
```

3、运行Pod

```shell
## 运行pod
[root@k8s-master01 data]# kubectl run tomcat-test --image=tomcat:9.0.20-jre8-alpine --port=8080
kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
deployment.apps/tomcat-test created
## 列出所有的pod
[root@k8s-master01 data]# kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
tomcat-test-76c794f897-xgjt2   1/1     Running   0          86s
## 列出所有的pod,包括附加信息
[root@k8s-master01 data]# kubectl get pods -o wide
NAME                           READY   STATUS    RESTARTS   AGE    IP             NODE         NOMINATED NODE   READINESS GATES
tomcat-test-76c794f897-xgjt2   1/1     Running   0          103s   10.81.58.193   k8s-node02   <none>           <none>
[root@k8s-master01 data]#
```

使用pod的IP访问容器

```shell
 curl 10.81.58.193:8080
```

![](https://img-blog.csdnimg.cn/img_convert/7eafc4ffdc8ab775c84d2ee28d766ea3.png)

==注意：无法使用Pod直接访问外网报错，因为在K8S集群中Pod是最小的单元！！！==

![](https://img-blog.csdnimg.cn/img_convert/9b38f7e872835fe977dcf74f47c10dc1.png)	

4、Pod的删除和添加

deployment作用：作为控制器管理pod，是一个控制器控制资源的。

```shell
#1、获得运行的pod
[root@k8s-master01 ~]# kubectl get pod
NAME                           READY   STATUS    RESTARTS   AGE
tomcat-test-76c794f897-5tg9f   1/1     Running   1          28m
## 2、获取deployment控制器
[root@k8s-master01 ~]# kubectl get deployment
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
tomcat-test   1/1     1            1           75m
# 3、获取所有的pods
[root@k8s-master01 ~]# kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
tomcat-test-76c794f897-5tg9f   1/1     Running   1          29m
# 4、删除pod
[root@k8s-master01 ~]# kubectl delete pod tomcat-test-76c794f897-5tg9f
pod "tomcat-test-76c794f897-5tg9f" deleted
[root@k8s-master01 ~]# kubectl get pod
NAME                           READY   STATUS    RESTARTS   AGE
tomcat-test-76c794f897-qzb26   1/1     Running   0          62s
# 5、每个pod都有不同的Ip
[root@k8s-master01 ~]# kubectl get pod -o wide
NAME                           READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
tomcat-test-76c794f897-qzb26   1/1     Running   0          98s   10.81.58.194   k8s-node02   <none>           <none>
[root@k8s-master01 ~]# 
```

删除deployment

```shell
# 1、获取deployment控制器
[root@k8s-master01 ~]# kubectl get deployment
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
tomcat-test   1/1     1            1           113m

# 2、删除控制器
[root@k8s-master01 ~]# kubectl delete deployment tomcat-test
deployment.apps "tomcat-test" deleted

# 3、删除成功！！！
[root@k8s-master01 ~]# kubectl get pod
No resources found in default namespace.

# 4、重新添加新的pod
[root@k8s-master01 ~]# kubectl run tomcat9-test --image=tomcat:9.0.20-jre8-alpine --port=8080
kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
deployment.apps/tomcat9-test created

# 5、获取pod和控制器
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-nq6qt   1/1     Running   0          6s
[root@k8s-master01 ~]# kubectl get deployment
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
tomcat9-test   1/1     1            1           14s
[root@k8s-master01 ~]# 
```

5、扩容操作

```shell
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          21h

## 1、扩容5个副本
[root@k8s-master01 ~]# kubectl scale --replicas=5 deployment tomcat9-test 
deployment.apps/tomcat9-test scaled
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          77s
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          77s
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          21h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          77s
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          77s

## 2、获取每个pod都有不同的Ip和Node节点
[root@k8s-master01 ~]# kubectl get pod -o wide
NAME                            READY   STATUS    RESTARTS   AGE   IP              NODE         NOMINATED NODE   READINESS GATES
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          94s   10.81.58.195    k8s-node02   <none>           <none>
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          94s   10.81.58.196    k8s-node02   <none>           <none>
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          21h   10.81.85.197    k8s-node01   <none>           <none>
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          94s   10.81.135.129   k8s-node03   <none>           <none>
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          94s   10.81.85.198    k8s-node01   <none>           <none>
[root@k8s-master01 ~]# 
```

6、创建服务SVC

```shell
## 1、创建服务
[root@k8s-master01 ~]# kubectl expose deployment tomcat9-test \
> --name=tomcat9-svc \
> --port=8888 \
> --target-port=8080 \
> --protocol=TCP \
> --type=NodePort
service/tomcat9-svc exposed
## 2、获取服务svc
[root@k8s-master01 ~]# kubectl get service
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          29h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   69s
[root@k8s-master01 ~]# kubectl get svc
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          29h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   7m6s
## 3、服务的详细信息
[root@k8s-master01 ~]# kubectl get svc -o wide
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE     SELECTOR
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          29h     <none>
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   9m59s   run=tomcat9-test
[root@k8s-master01 ~]# 
```

访问服务端口

```shell
curl 10.1.215.214:8888
```

![](https://img-blog.csdnimg.cn/img_convert/82009ccb8df199a5e43edb74bb22f2df.png)

访问集群外端口

```shell
http://8.134.122.211:32502
```

![](https://img-blog.csdnimg.cn/img_convert/f1dcbb00ea86e1995e7e87d863e00e28.png)

## 7- kubectl常用命令

### 7.1 基本语法

```shell
kubectl [command] [TYPE] [NAME] [flags] 
```

1、`command`：对一个或多个资源执行的操作，例如 `create` 、`get` 、`describe` 、`delete`等。

2、`TYPE`：指定资源类型，资源类型不区分大小写，可以指定单数、复数或缩写形式。

```shell
-- 以下命令输出相同的结果
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          66m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          66m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          66m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          66m
[root@k8s-master01 ~]# kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          66m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          66m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          66m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          66m
[root@k8s-master01 ~]# kubectl get po
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          67m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          67m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          67m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          67m
[root@k8s-master01 ~]# 
```

3、`NAME` ：指定资源的名称，名称区分大小写，如果省略名称则显示所有资源的详细信息。

```shell
 kubectl get pods
```

在对多个资源执行操作时，可以按类型和名称指定每个资源，或指定一个或多个文件。

4、`flags`:指定可选的参数，比如可以使用 `-s` 或者`-server` 参数指定 Kubernetes API 服务器的地址和端口。

### 7.2 get常用命令

`kubectl get - `列出一个或多个资源。

```shell
# 1、查看集群状态信息
[root@k8s-master01 ~]# kubectl cluster-info
Kubernetes master is running at https://172.21.252.3:6443
KubeDNS is running at https://172.21.252.3:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
# 2、查看集群状态
[root@k8s-master01 ~]# kubectl get cs
NAME                 STATUS    MESSAGE             ERROR
scheduler            Healthy   ok                  
controller-manager   Healthy   ok                  
etcd-0               Healthy   {"health":"true"}

# 3、查看集群节点信息
[root@k8s-master01 ~]# kubectl get nodes
NAME           STATUS   ROLES    AGE   VERSION
k8s-master01   Ready    master   29h   v1.17.5
k8s-node01     Ready    <none>   29h   v1.17.5
k8s-node02     Ready    <none>   29h   v1.17.5
k8s-node03     Ready    <none>   29h   v1.17.5

# 4、查看集群命名空间
[root@k8s-master01 ~]# kubectl get ns
NAME              STATUS   AGE
default           Active   29h
kube-node-lease   Active   29h
kube-public       Active   29h
kube-system       Active   29h

# 5、查看服务的命名空间
[root@k8s-master01 ~]# kubectl get service
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          31h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   158m
[root@k8s-master01 ~]# kubectl get svc
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          31h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   158m
[root@k8s-master01 ~]# 

# 6、查看指定命名空间的服务
[root@k8s-master01 ~]# kubectl get svc -n kube-system 
NAME       TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)                  AGE
kube-dns   ClusterIP   10.1.0.10    <none>        53/UDP,53/TCP,9153/TCP   29h

# 7、以纯文本输出格式列出所有pod
[root@k8s-master01 ~]# kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          77m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          77m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          77m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          77m

# 8、以纯文本输出格式列出所有pod,并包含附加信息(如节点名)。
[root@k8s-master01 ~]# kubectl get pods -o wide
NAME                            READY   STATUS    RESTARTS   AGE   IP              NODE         NOMINATED NODE   READINESS GATES
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          77m   10.81.58.195    k8s-node02   <none>           <none>
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          77m   10.81.58.196    k8s-node02   <none>           <none>
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h   10.81.85.197    k8s-node01   <none>           <none>
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          77m   10.81.135.129   k8s-node03   <none>           <none>
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          77m   10.81.85.198    k8s-node01   <none>           <none>
[root@k8s-master01 ~]# kubectl get svc
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          30h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   55m

# 9、以纯文本输出格式列出所有副本控制器和服务。
[root@k8s-master01 ~]# kubectl get rc,svc
NAME                  TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
service/kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          31h
service/tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   154m

# 10、列出在节点k8s-node01上运行的所有 pod
[root@k8s-master01 ~]# kubectl get pods --field-selector=spec.nodeName=k8s-node01
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          24h
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          172m
[root@k8s-master01 ~]#  
```

### 7.3 describe常用命令

`kubectl describe - `显示一个或多个资源的详细状态，==默认情况下包括未初始化的资源==。

```shell
# 1、显示名称为k8s-node02的节点的详细信息
[root@k8s-master01 ~]# kubectl describe nodes k8s-node02
Name:               k8s-node02
Roles:              <none>
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=k8s-node02
                    kubernetes.io/os=linux
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    projectcalico.org/IPv4Address: 172.21.252.5/20
                    projectcalico.org/IPv4IPIPTunnelAddr: 10.81.58.192
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sun, 04 Jul 2021 14:52:05 +0800
.........
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                250m (12%)  0 (0%)
  memory             0 (0%)      0 (0%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:              <none>

# 2、获取所有的pod
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          3h12m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          3h12m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          24h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          3h12m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          3h12m

# 3、获取pod tomcat9-test-569b5bf455-fltdd的详细信息！！
[root@k8s-master01 ~]# kubectl describe pod tomcat9-test-569b5bf455-fltdd
Name:         tomcat9-test-569b5bf455-fltdd
Namespace:    default
Priority:     0
Node:         k8s-node02/172.21.252.5
Start Time:   Mon, 05 Jul 2021 19:17:56 +0800
Labels:       pod-template-hash=569b5bf455
              run=tomcat9-test
Annotations:  cni.projectcalico.org/podIP: 10.81.58.195/32
              cni.projectcalico.org/podIPs: 10.81.58.195/32
Status:       Running
IP:           10.81.58.195
..........
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:          <none>
[root@k8s-master01 ~]# 
```

### 7.4 delete常用命令

`kubectl delete - `从文件、stdin 或指定标签选择器、名称、资源选择器或资源中删除资源。

```shell
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   1          14h
tomcat9-test-569b5bf455-mccnc   1/1     Running   1          14h
tomcat9-test-569b5bf455-nq6qt   1/1     Running   3          35h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   1          14h
tomcat9-test-569b5bf455-sn2s8   1/1     Running   1          14h

## 1、删除单个pod
[root@k8s-master01 ~]# kubectl delete pod tomcat9-test-569b5bf455-fltdd
pod "tomcat9-test-569b5bf455-fltdd" deleted
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-mccnc   1/1     Running   1          14h
tomcat9-test-569b5bf455-mlmv8   1/1     Running   0          2m27s
tomcat9-test-569b5bf455-nq6qt   1/1     Running   3          35h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   1          14h
tomcat9-test-569b5bf455-sn2s8   1/1     Running   1          14h

# 2、删除所有pod,包括未初始化的pod
[root@k8s-master01 ~]# kubectl delete pod --all
pod "tomcat9-test-569b5bf455-mccnc" deleted
pod "tomcat9-test-569b5bf455-mlmv8" deleted
pod "tomcat9-test-569b5bf455-nq6qt" deleted
pod "tomcat9-test-569b5bf455-nxhrm" deleted
pod "tomcat9-test-569b5bf455-sn2s8" deleted
[root@k8s-master01 ~]# kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-82cps   1/1     Running   0          75s
tomcat9-test-569b5bf455-fl8zr   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndp67   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndssv   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndxhf   1/1     Running   0          75s
[root@k8s-master01 ~]# 
```

### 7.5 其他命令

1、进入容器命令

`kubectl exec -` 对 pod 中的容器执行命令，与docker的exec命令非常类似。

```shell
[root@k8s-master01 ~]# kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-82cps   1/1     Running   0          75s
tomcat9-test-569b5bf455-fl8zr   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndp67   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndssv   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndxhf   1/1     Running   0          75s
[root@k8s-master01 ~]# kubectl exec -it tomcat9-test-569b5bf455-82cps sh
/usr/local/tomcat # ls
BUILDING.txt     README.md        conf             native-jni-lib
CONTRIBUTING.md  RELEASE-NOTES    include          temp
LICENSE          RUNNING.txt      lib              webapps
NOTICE           bin              logs             work
/usr/local/tomcat # exit
[root@k8s-master01 ~]# 
```

2、打印 Pod 中容器的日志

```shell
# 从 pod <pod-name> 开始流式传输日志。
kubectl logs -f <pod-name>
```

3、格式化输出

将pod信息格式化输出到一个yaml文件

```shell
[root@k8s-master01 ~]# kubectl get pod 
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-82cps   1/1     Running   0          66m
tomcat9-test-569b5bf455-fl8zr   1/1     Running   0          66m
tomcat9-test-569b5bf455-ndp67   1/1     Running   0          66m
tomcat9-test-569b5bf455-ndssv   1/1     Running   0          66m
tomcat9-test-569b5bf455-ndxhf   1/1     Running   0          66m
[root@k8s-master01 ~]# kubectl get pod tomcat9-test-569b5bf455-ndxhf -o yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    cni.projectcalico.org/podIP: 10.81.85.202/32
    cni.projectcalico.org/podIPs: 10.81.85.202/32
  creationTimestamp: "2021-07-06T01:48:47Z"
  generateName: tomcat9-test-569b5bf455-
  ...........
  containerStatuses:
  - containerID: docker://00b5db960a98cd0263c1e9ff5fc02bbafe5ffb0805d587a2b01ae4a83d74e3a8
    image: tomcat:9.0.20-jre8-alpine
    imageID: docker-pullable://tomcat@sha256:17accf0afeeecce0310d363490cd60a788aa4630ab9c9c802231d6fbd4bb2375
    lastState: {}
    name: tomcat9-test
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2021-07-06T01:48:48Z"
  hostIP: 172.21.252.4
  phase: Running
  podIP: 10.81.85.202
  podIPs:
  - ip: 10.81.85.202
  qosClass: BestEffort
  startTime: "2021-07-06T01:48:47Z"
[root@k8s-master01 ~]# 
```

## 8- NameSpace

### 8.1 基本介绍

- 俗称命名空间，可以单纯的认为`namespaces`是kubernetes集群中的虚拟化集群。在一个Kubernetes集群中可以拥有多个命名空间，它们在逻辑上彼此隔离。 可以为你提供组织，安全甚至性能方面的帮助！
- Namespace是对一组资源和对象的抽象集合，比如可以用来将系统内部的对象划分为不同的项目组或用户组。==常见的pods, services, replication controllers和deployments等都是属于某一个namespace的（默认是default），而node, persistentVolumes等则不属于任何namespace==。

大多数的Kubernetes中的集群默认会有一个叫default的`namespace`。然而实际上存在4个`namespace`。

- default：资源默认被创建于default命名空间。
- kube-system：kubernetes系统组件使用。
- kube-node-lease: kubernetes集群节点租约状态。
- kube-public：公共资源使用，但实际上现在并不常用。

这个默认(default)的namespace并没什么特别，但是不能删除它。这很适合刚刚开始使用kubernetes和一些小的产品系统。但不建议应用于大型生产系统。因为这种复杂系统中，团队会非常容易意外地或者无意识地重写或者中断其他服务service。相反，创建多个命名空间来把service(服务)分割成更容易管理的块。

**(default)的namespace基本作用**：

- 多租户情况下，实现资源隔离。
- 属于逻辑隔离，属于管理边界，不属于网络边界。
- 可以针对每个namespace做资源配额。

### 8.2 查看命名空间

1、具体命令

```shell
## 查看命名空间
kubectl get namespace

## 查看所有命名空间的pod资源
kubectl get pod --all-namespaces
kubectl get pod -A

## 简写命令(查看命名空间)
kubectl get ns
```

查询结果！！！

```shell
## 1、查看命名空间
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   169m
kube-node-lease   Active   169m
kube-public       Active   169m
kube-system       Active   169m
## 2、查看所有命名空间的pod资源
[root@k8s-master01 data]# kubectl get pod --all-namespaces
NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-6b94766748-pn4l8   1/1     Running   0          78m
kube-system   calico-node-4m62k                          1/1     Running   0          78m
kube-system   calico-node-7bnqj                          1/1     Running   0          78m
kube-system   calico-node-krh64                          1/1     Running   0          78m
kube-system   calico-node-zwvv9                          1/1     Running   0          78m
kube-system   coredns-6955765f44-nwzg6                   1/1     Running   0          169m
kube-system   coredns-6955765f44-rdwnc                   1/1     Running   0          169m
kube-system   etcd-k8s-master01                          1/1     Running   1          169m
kube-system   kube-apiserver-k8s-master01                1/1     Running   1          169m
kube-system   kube-controller-manager-k8s-master01       1/1     Running   1          169m
kube-system   kube-proxy-4vdxm                           1/1     Running   1          159m
kube-system   kube-proxy-5nlqn                           1/1     Running   1          154m
kube-system   kube-proxy-npzs2                           1/1     Running   1          169m
kube-system   kube-proxy-z47rt                           1/1     Running   1          154m
kube-system   kube-scheduler-k8s-master01                1/1     Running   1          169m
## 3、查看命名空间
[root@k8s-master01 data]# kubectl get ns
NAME              STATUS   AGE
default           Active   169m
kube-node-lease   Active   169m
kube-public       Active   169m
kube-system       Active   169m
[root@k8s-master01 data]# 
```

3、命名空间说明

```yaml
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   169m	# 用户创建的pod默认在此命名空间
kube-node-lease   Active   169m # 所有用户均可以访问，包括未认证用户
kube-public       Active   169m # kubernetes集群节点租约状态
kube-system       Active   169m # kubernetes集群在使用
```

### 8.3 NameSpace相关操作

1、创建NameSpace

```shell
kubectl create namespace guardwhy01
-- 简写命令
kubectl create ns guardwhy02
```

2、删除NameSpace

```shell
kubectl delete namespace guardwhy01
-- 简写命令
kubectl delete ns guardwhy02
```

3、执行结果！！！

```shell
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   3h7m
kube-node-lease   Active   3h7m
kube-public       Active   3h7m
kube-system       Active   3h7m
[root@k8s-master01 data]# kubectl create namespace guardwhy01
namespace/guardwhy01 created
[root@k8s-master01 data]# kubectl create ns guardwhy02
namespace/guardwhy02 created
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   3h8m
guardwhy01        Active   36s
guardwhy02        Active   5s
kube-node-lease   Active   3h8m
kube-public       Active   3h8m
kube-system       Active   3h8m
[root@k8s-master01 data]# kubectl delete namespace guardwhy01
namespace "guardwhy01" deleted
[root@k8s-master01 data]# kubectl delete ns guardwhy02
namespace "guardwhy02" deleted
[root@k8s-master01 data]# kubectl get namespace
NAME              STATUS   AGE
default           Active   3h12m
kube-node-lease   Active   3h12m
kube-public       Active   3h12m
kube-system       Active   3h12m
[root@k8s-master01 data]# 
```

## 9-什么是pod？

Pod是kubernetes集群能够调度的最小单元，Pod是容器的封装 。在Kubernetes集群中，Pod是所有业务类型的基础，也是K8S管理的最小单位级，它是一个或多个容器的组合。这些容器共享存储、网络和命名空间，以及如何运行的规范。在Pod中，所有容器都被同一安排和调度，并运行在共享的上下文中。对于具体应用而言，Pod是它们的逻辑主机，Pod包含业务相关的多个应用容器。

### 9.1 Pod的基本特点

**网络**:每一个Pod都会被指派一个唯一的Ip地址，在Pod中的每一个容器共享网络命名空间，包括Ip地址和网络端口。在同一个Pod中的容器可以和localhost进行互相通信。当Pod中的容器需要与Pod外的实体进行通信时，则需要通过端口等共享的网络资源。

**存储**:Pod能够被指定共享存储卷的集合，在Pod中所有的容器能够访问共享存储卷，允许这些容器共享数据。存储卷也允许在一个Pod持久化数据，以防止其中的容器需要被重启。

### 9.2 Pod的工作方式

1、K8s一般不直接创建Pod，而是通过控制器和模版配置来管理和调度。

2、**Pod重启**：在Pod中的容器可能会由于异常等原因导致其终止退出，Kubernetes提供了重启策略以重启容器。重启策略对同一个Pod的所有容器起作用，容器的重启由Node上的kubelet执行。Pod支持三种重启策略，在配置文件中通过`restartPolicy`字段设置重启策略。

```shell
Always：只要退出就会重启。
OnFailure：只有在失败退出（exit code不等于0）时，才会重启。
Never：只要退出，就不再重启
```

==注意，这里的重启是指在Pod的宿主Node上进行本地重启，而不是调度到其它Node上==。

3、资源限制

Kubernetes通过cgroups限制容器的CPU和内存等计算资源，包括requests(请求，调度器保证调度到资源充足的Node上)和limits(上限)。

### 9.3 Pod基本操作

1、查看Pod，执行以下命令

```shell
-- 1、查看default命名空间下的pods
kubectl get pods

-- 2、查看kube-system命名空间下的pods
kubectl get pods -n kube-system

-- 3、查看所有命名空间下的pods
kubectl get pod --all-namespaces
kubectl get pod -A
```

2、创建Pod

下载tomcat相关的镜像

```shell
[root@k8s-master01 data]# docker pull tomcat:9.0.37-jdk8-openjdk-slim
[root@k8s-master01 data]# docker pull tomcat:9.0.20-jre8-alpine
[root@k8s-master01 data]# docker pull tomcat:9.0.37-jdk8
[root@k8s-master01 data]# docker images
REPOSITORY                           TAG                        IMAGE ID       CREATED         SIZE
tomcat                               9.0.37-jdk8-openjdk-slim   d60b68827676   9 months ago    305MB
tomcat                               9.0.37-jdk8                9c7be7b021c3   9 months ago    531MB
calico/node                          v3.14.2                    780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol            v3.14.2                    9dfa8f25b51c   11 months ago   22.8MB
calico/cni                           v3.14.2                    e6189009f081   11 months ago   119MB
calico/kube-controllers              v3.14.2                    4815e4106d26   11 months ago   52.8MB
k8s.gcr.io/kube-proxy                v1.17.5                    e13db435247d   14 months ago   116MB
k8s.gcr.io/kube-apiserver            v1.17.5                    f640481f6db3   14 months ago   171MB
k8s.gcr.io/kube-controller-manager   v1.17.5                    fe3d691efbf3   14 months ago   161MB
k8s.gcr.io/kube-scheduler            v1.17.5                    f648efaff966   14 months ago   94.4MB
k8s.gcr.io/coredns                   1.6.5                      70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                      3.4.3-0                    303ce5db0e90   20 months ago   288MB
tomcat                               9.0.20-jre8-alpine         387f9d021d3a   2 years ago     108MB
k8s.gcr.io/pause                     3.1                        da86e6ba6ca1   3 years ago     742kB
[root@k8s-master01 data]# 
```

3、运行Pod

```shell
## 运行pod
[root@k8s-master01 data]# kubectl run tomcat-test --image=tomcat:9.0.20-jre8-alpine --port=8080
kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
deployment.apps/tomcat-test created
## 列出所有的pod
[root@k8s-master01 data]# kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
tomcat-test-76c794f897-xgjt2   1/1     Running   0          86s
## 列出所有的pod,包括附加信息
[root@k8s-master01 data]# kubectl get pods -o wide
NAME                           READY   STATUS    RESTARTS   AGE    IP             NODE         NOMINATED NODE   READINESS GATES
tomcat-test-76c794f897-xgjt2   1/1     Running   0          103s   10.81.58.193   k8s-node02   <none>           <none>
[root@k8s-master01 data]#
```

使用pod的IP访问容器

```shell
 curl 10.81.58.193:8080
```

![](https://img-blog.csdnimg.cn/img_convert/7eafc4ffdc8ab775c84d2ee28d766ea3.png)

==注意：无法使用Pod直接访问外网报错，因为在K8S集群中Pod是最小的单元！！！==

![](https://img-blog.csdnimg.cn/img_convert/9b38f7e872835fe977dcf74f47c10dc1.png)	

4、Pod的删除和添加

deployment作用：作为控制器管理pod，是一个控制器控制资源的。

```shell
#1、获得运行的pod
[root@k8s-master01 ~]# kubectl get pod
NAME                           READY   STATUS    RESTARTS   AGE
tomcat-test-76c794f897-5tg9f   1/1     Running   1          28m
## 2、获取deployment控制器
[root@k8s-master01 ~]# kubectl get deployment
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
tomcat-test   1/1     1            1           75m
# 3、获取所有的pods
[root@k8s-master01 ~]# kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
tomcat-test-76c794f897-5tg9f   1/1     Running   1          29m
# 4、删除pod
[root@k8s-master01 ~]# kubectl delete pod tomcat-test-76c794f897-5tg9f
pod "tomcat-test-76c794f897-5tg9f" deleted
[root@k8s-master01 ~]# kubectl get pod
NAME                           READY   STATUS    RESTARTS   AGE
tomcat-test-76c794f897-qzb26   1/1     Running   0          62s
# 5、每个pod都有不同的Ip
[root@k8s-master01 ~]# kubectl get pod -o wide
NAME                           READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
tomcat-test-76c794f897-qzb26   1/1     Running   0          98s   10.81.58.194   k8s-node02   <none>           <none>
[root@k8s-master01 ~]# 
```

删除deployment

```shell
# 1、获取deployment控制器
[root@k8s-master01 ~]# kubectl get deployment
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
tomcat-test   1/1     1            1           113m

# 2、删除控制器
[root@k8s-master01 ~]# kubectl delete deployment tomcat-test
deployment.apps "tomcat-test" deleted

# 3、删除成功！！！
[root@k8s-master01 ~]# kubectl get pod
No resources found in default namespace.

# 4、重新添加新的pod
[root@k8s-master01 ~]# kubectl run tomcat9-test --image=tomcat:9.0.20-jre8-alpine --port=8080
kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
deployment.apps/tomcat9-test created

# 5、获取pod和控制器
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-nq6qt   1/1     Running   0          6s
[root@k8s-master01 ~]# kubectl get deployment
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
tomcat9-test   1/1     1            1           14s
[root@k8s-master01 ~]# 
```

5、扩容操作

```shell
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          21h

## 1、扩容5个副本
[root@k8s-master01 ~]# kubectl scale --replicas=5 deployment tomcat9-test 
deployment.apps/tomcat9-test scaled
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          77s
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          77s
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          21h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          77s
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          77s

## 2、获取每个pod都有不同的Ip和Node节点
[root@k8s-master01 ~]# kubectl get pod -o wide
NAME                            READY   STATUS    RESTARTS   AGE   IP              NODE         NOMINATED NODE   READINESS GATES
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          94s   10.81.58.195    k8s-node02   <none>           <none>
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          94s   10.81.58.196    k8s-node02   <none>           <none>
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          21h   10.81.85.197    k8s-node01   <none>           <none>
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          94s   10.81.135.129   k8s-node03   <none>           <none>
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          94s   10.81.85.198    k8s-node01   <none>           <none>
[root@k8s-master01 ~]# 
```

6、创建服务SVC

```shell
## 1、创建服务
[root@k8s-master01 ~]# kubectl expose deployment tomcat9-test \
> --name=tomcat9-svc \
> --port=8888 \
> --target-port=8080 \
> --protocol=TCP \
> --type=NodePort
service/tomcat9-svc exposed
## 2、获取服务svc
[root@k8s-master01 ~]# kubectl get service
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          29h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   69s
[root@k8s-master01 ~]# kubectl get svc
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          29h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   7m6s
## 3、服务的详细信息
[root@k8s-master01 ~]# kubectl get svc -o wide
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE     SELECTOR
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          29h     <none>
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   9m59s   run=tomcat9-test
[root@k8s-master01 ~]# 
```

访问服务端口

```shell
curl 10.1.215.214:8888
```

![](https://img-blog.csdnimg.cn/img_convert/82009ccb8df199a5e43edb74bb22f2df.png)

访问集群外端口

```shell
http://8.134.122.211:32502
```

![](https://img-blog.csdnimg.cn/img_convert/f1dcbb00ea86e1995e7e87d863e00e28.png)

## 10-kubectl常用命令

### 10.1 基本语法

```shell
kubectl [command] [TYPE] [NAME] [flags] 
```

1、`command`：对一个或多个资源执行的操作，例如 `create` 、`get` 、`describe` 、`delete`等。

2、`TYPE`：指定资源类型，资源类型不区分大小写，可以指定单数、复数或缩写形式。

```shell
-- 以下命令输出相同的结果
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          66m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          66m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          66m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          66m
[root@k8s-master01 ~]# kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          66m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          66m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          66m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          66m
[root@k8s-master01 ~]# kubectl get po
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          67m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          67m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          67m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          67m
[root@k8s-master01 ~]# 
```

3、`NAME` ：指定资源的名称，名称区分大小写，如果省略名称则显示所有资源的详细信息。

```shell
 kubectl get pods
```

在对多个资源执行操作时，可以按类型和名称指定每个资源，或指定一个或多个文件。

4、`flags`:指定可选的参数，比如可以使用 `-s` 或者`-server` 参数指定 Kubernetes API 服务器的地址和端口。

### 10.2 get常用命令

`kubectl get - `列出一个或多个资源。

```shell
# 1、查看集群状态信息
[root@k8s-master01 ~]# kubectl cluster-info
Kubernetes master is running at https://172.21.252.3:6443
KubeDNS is running at https://172.21.252.3:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
# 2、查看集群状态
[root@k8s-master01 ~]# kubectl get cs
NAME                 STATUS    MESSAGE             ERROR
scheduler            Healthy   ok                  
controller-manager   Healthy   ok                  
etcd-0               Healthy   {"health":"true"}

# 3、查看集群节点信息
[root@k8s-master01 ~]# kubectl get nodes
NAME           STATUS   ROLES    AGE   VERSION
k8s-master01   Ready    master   29h   v1.17.5
k8s-node01     Ready    <none>   29h   v1.17.5
k8s-node02     Ready    <none>   29h   v1.17.5
k8s-node03     Ready    <none>   29h   v1.17.5

# 4、查看集群命名空间
[root@k8s-master01 ~]# kubectl get ns
NAME              STATUS   AGE
default           Active   29h
kube-node-lease   Active   29h
kube-public       Active   29h
kube-system       Active   29h

# 5、查看服务的命名空间
[root@k8s-master01 ~]# kubectl get service
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          31h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   158m
[root@k8s-master01 ~]# kubectl get svc
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          31h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   158m
[root@k8s-master01 ~]# 

# 6、查看指定命名空间的服务
[root@k8s-master01 ~]# kubectl get svc -n kube-system 
NAME       TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)                  AGE
kube-dns   ClusterIP   10.1.0.10    <none>        53/UDP,53/TCP,9153/TCP   29h

# 7、以纯文本输出格式列出所有pod
[root@k8s-master01 ~]# kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          77m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          77m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          77m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          77m

# 8、以纯文本输出格式列出所有pod,并包含附加信息(如节点名)。
[root@k8s-master01 ~]# kubectl get pods -o wide
NAME                            READY   STATUS    RESTARTS   AGE   IP              NODE         NOMINATED NODE   READINESS GATES
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          77m   10.81.58.195    k8s-node02   <none>           <none>
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          77m   10.81.58.196    k8s-node02   <none>           <none>
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          22h   10.81.85.197    k8s-node01   <none>           <none>
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          77m   10.81.135.129   k8s-node03   <none>           <none>
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          77m   10.81.85.198    k8s-node01   <none>           <none>
[root@k8s-master01 ~]# kubectl get svc
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          30h
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   55m

# 9、以纯文本输出格式列出所有副本控制器和服务。
[root@k8s-master01 ~]# kubectl get rc,svc
NAME                  TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
service/kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          31h
service/tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   154m

# 10、列出在节点k8s-node01上运行的所有 pod
[root@k8s-master01 ~]# kubectl get pods --field-selector=spec.nodeName=k8s-node01
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          24h
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          172m
[root@k8s-master01 ~]#  
```

### 10.3 describe常用命令

`kubectl describe - `显示一个或多个资源的详细状态，==默认情况下包括未初始化的资源==。

```shell
# 1、显示名称为k8s-node02的节点的详细信息
[root@k8s-master01 ~]# kubectl describe nodes k8s-node02
Name:               k8s-node02
Roles:              <none>
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=k8s-node02
                    kubernetes.io/os=linux
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    projectcalico.org/IPv4Address: 172.21.252.5/20
                    projectcalico.org/IPv4IPIPTunnelAddr: 10.81.58.192
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sun, 04 Jul 2021 14:52:05 +0800
.........
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                250m (12%)  0 (0%)
  memory             0 (0%)      0 (0%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:              <none>

# 2、获取所有的pod
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   0          3h12m
tomcat9-test-569b5bf455-mccnc   1/1     Running   0          3h12m
tomcat9-test-569b5bf455-nq6qt   1/1     Running   2          24h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   0          3h12m
tomcat9-test-569b5bf455-sn2s8   1/1     Running   0          3h12m

# 3、获取pod tomcat9-test-569b5bf455-fltdd的详细信息！！
[root@k8s-master01 ~]# kubectl describe pod tomcat9-test-569b5bf455-fltdd
Name:         tomcat9-test-569b5bf455-fltdd
Namespace:    default
Priority:     0
Node:         k8s-node02/172.21.252.5
Start Time:   Mon, 05 Jul 2021 19:17:56 +0800
Labels:       pod-template-hash=569b5bf455
              run=tomcat9-test
Annotations:  cni.projectcalico.org/podIP: 10.81.58.195/32
              cni.projectcalico.org/podIPs: 10.81.58.195/32
Status:       Running
IP:           10.81.58.195
..........
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:          <none>
[root@k8s-master01 ~]# 
```

### 10.4 delete常用命令

`kubectl delete - `从文件、stdin 或指定标签选择器、名称、资源选择器或资源中删除资源。

```shell
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-fltdd   1/1     Running   1          14h
tomcat9-test-569b5bf455-mccnc   1/1     Running   1          14h
tomcat9-test-569b5bf455-nq6qt   1/1     Running   3          35h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   1          14h
tomcat9-test-569b5bf455-sn2s8   1/1     Running   1          14h

## 1、删除单个pod
[root@k8s-master01 ~]# kubectl delete pod tomcat9-test-569b5bf455-fltdd
pod "tomcat9-test-569b5bf455-fltdd" deleted
[root@k8s-master01 ~]# kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-mccnc   1/1     Running   1          14h
tomcat9-test-569b5bf455-mlmv8   1/1     Running   0          2m27s
tomcat9-test-569b5bf455-nq6qt   1/1     Running   3          35h
tomcat9-test-569b5bf455-nxhrm   1/1     Running   1          14h
tomcat9-test-569b5bf455-sn2s8   1/1     Running   1          14h

# 2、删除所有pod,包括未初始化的pod
[root@k8s-master01 ~]# kubectl delete pod --all
pod "tomcat9-test-569b5bf455-mccnc" deleted
pod "tomcat9-test-569b5bf455-mlmv8" deleted
pod "tomcat9-test-569b5bf455-nq6qt" deleted
pod "tomcat9-test-569b5bf455-nxhrm" deleted
pod "tomcat9-test-569b5bf455-sn2s8" deleted
[root@k8s-master01 ~]# kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-82cps   1/1     Running   0          75s
tomcat9-test-569b5bf455-fl8zr   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndp67   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndssv   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndxhf   1/1     Running   0          75s
[root@k8s-master01 ~]# 
```

2、解决Terminating状态的Pod删不掉的问题

```shell
kubectl delete pods [pod name] --grace-period=0 --force
```

### 10.5 其他命令

1、进入容器命令

`kubectl exec -` 对 pod 中的容器执行命令，与docker的exec命令非常类似。

```shell
[root@k8s-master01 ~]# kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-82cps   1/1     Running   0          75s
tomcat9-test-569b5bf455-fl8zr   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndp67   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndssv   1/1     Running   0          75s
tomcat9-test-569b5bf455-ndxhf   1/1     Running   0          75s
[root@k8s-master01 ~]# kubectl exec -it tomcat9-test-569b5bf455-82cps sh
/usr/local/tomcat # ls
BUILDING.txt     README.md        conf             native-jni-lib
CONTRIBUTING.md  RELEASE-NOTES    include          temp
LICENSE          RUNNING.txt      lib              webapps
NOTICE           bin              logs             work
/usr/local/tomcat # exit
[root@k8s-master01 ~]# 
```

2、打印 Pod 中容器的日志

```shell
# 从 pod <pod-name> 开始流式传输日志。
kubectl logs -f <pod-name>
```

3、格式化输出

将pod信息格式化输出到一个yaml文件

```shell
[root@k8s-master01 ~]# kubectl get pod 
NAME                            READY   STATUS    RESTARTS   AGE
tomcat9-test-569b5bf455-82cps   1/1     Running   0          66m
tomcat9-test-569b5bf455-fl8zr   1/1     Running   0          66m
tomcat9-test-569b5bf455-ndp67   1/1     Running   0          66m
tomcat9-test-569b5bf455-ndssv   1/1     Running   0          66m
tomcat9-test-569b5bf455-ndxhf   1/1     Running   0          66m
[root@k8s-master01 ~]# kubectl get pod tomcat9-test-569b5bf455-ndxhf -o yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    cni.projectcalico.org/podIP: 10.81.85.202/32
    cni.projectcalico.org/podIPs: 10.81.85.202/32
  creationTimestamp: "2021-07-06T01:48:47Z"
  generateName: tomcat9-test-569b5bf455-
  ...........
  containerStatuses:
  - containerID: docker://00b5db960a98cd0263c1e9ff5fc02bbafe5ffb0805d587a2b01ae4a83d74e3a8
    image: tomcat:9.0.20-jre8-alpine
    imageID: docker-pullable://tomcat@sha256:17accf0afeeecce0310d363490cd60a788aa4630ab9c9c802231d6fbd4bb2375
    lastState: {}
    name: tomcat9-test
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2021-07-06T01:48:48Z"
  hostIP: 172.21.252.4
  phase: Running
  podIP: 10.81.85.202
  podIPs:
  - ip: 10.81.85.202
  qosClass: BestEffort
  startTime: "2021-07-06T01:48:47Z"
[root@k8s-master01 ~]# 
```

## 11- K8S资源文件实现

### 11.1 idea安装k8s插件

1、idea插件官网地址：[https://plugins.jetbrains.com/](https://plugins.jetbrains.com/)

![](https://img-blog.csdnimg.cn/img_convert/bda7ab457f10369888fbd46fac32c536.png)

2、kubernetes地址：[https://plugins.jetbrains.com/plugin/10485-kubernetes/versions](https://plugins.jetbrains.com/plugin/10485-kubernetes/versions)

![](https://img-blog.csdnimg.cn/img_convert/101019fe14d0d82f1333b36bc2378d58.png)

2、离线安装k8s插件

特殊原因，在线安装有可能安装失败失败。下载idea对应版本的插件后，进行离线安装。

```shell
help->about->查看idea内部版本信息
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210706112229.png" style="zoom:80%;" />

下载对应的版本！！！

![](https://img-blog.csdnimg.cn/img_convert/a4a147ee957b3e87d64176d283dae2f4.png)

离线安装k8s插件，安装成功！！！

```shell
settings->plugins->Install Plugin from Disk->插件安装目录,安装完成后重启idea
```

![](https://img-blog.csdnimg.cn/img_convert/d013ae2f6db3a185e61bc714d67b133a.png)

### 11.2 idea配置SSH客户端

1、idea配置

```shell
settings->Tools->SSH Configurations->新建 
```

![](https://img-blog.csdnimg.cn/img_convert/546269494c989c2084aaf397a0d4213a.png)

![](https://img-blog.csdnimg.cn/img_convert/3ba5f9bbf652640b159be34f758c890d.png)

2、选择使用SSH客户端。

```shell
Tools->Start SSH session->选择刚刚配置的ssh客户端名称 
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210706121848.png" style="zoom: 80%;" />

3、新建yml类型文件

idea默认没有`yml`文件类型，可以通过`new->file->手工输入*.yml`创建`yml`类型文件。

![](https://img-blog.csdnimg.cn/img_convert/7c12ccfe7b973a19ff9075b685f80036.png)

### 11.3 Remote Host

1、IDEA基本配置

```shell
Tools->Deployment->Configurations->配置Remote Host 
```

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210706124109.png" style="zoom:80%;" />

2、设置服务器名字： `k8s-master01`

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210706135548.png" style="zoom:80%;" />

3、测试连接！！！

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210706174254.png" style="zoom:80%;" />

4、使用Remote Host，将本工程中的文件上传k8s集群 。

![](https://img-blog.csdnimg.cn/img_convert/ac0a0d6f394651d2f2793ab5b7d4d7da.png)

### 11.4 NameSpace相关操作

1、查看自动生成模板信息内容

![](https://img-blog.csdnimg.cn/img_convert/07ac668154e2accdc886162991e07da8.png)

2、创建`namespace01.yml`文件

在文件中输入`kres`，根据模板快速生成yml文件信息。

```yml
apiVersion: v1
kind: Namespace
metadata:
  name: guardwhy
```

![](https://img-blog.csdnimg.cn/img_convert/f99fea839cd75784ee4fd2ae917c169d.png)

3、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

```shell
[root@k8s-master01 data]# ls
calico.yml  init.sh  k8s.1.17.5.tar  pod
[root@k8s-master01 data]# cd pod/
[root@k8s-master01 pod]# ls
namespace01.yml

# 1、创建namespace(guardwhy)
[root@k8s-master01 pod]# kubectl apply -f namespace01.yml 
namespace/guardwhy created
[root@k8s-master01 pod]# kubectl get ns
NAME              STATUS   AGE
default           Active   2d3h
guardwhy          Active   11s
kube-node-lease   Active   2d3h
kube-public       Active   2d3h
kube-system       Active   2d3h

# 2、删除namespace(guardwhy)
[root@k8s-master01 pod]# kubectl delete -f namespace01.yml 
namespace "guardwhy" deleted
[root@k8s-master01 pod]# kubectl get ns
NAME              STATUS   AGE
default           Active   2d3h
kube-node-lease   Active   2d3h
kube-public       Active   2d3h
kube-system       Active   2d3h
[root@k8s-master01 pod]# 
```

### 11.5 pod相关操作

1、在`k8sdemo01`工程创建`tomcatpod.yml`文件，在文件中输入`kpod`，根据模板快速生成yml文件信息。

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210706191837.png" style="zoom:80%;" />

```shell
apiVersion: v1
kind: Pod
metadata:
  name: tomcat-pod
  labels:
    app: tomcat-pod
spec:
  containers:
    - name: tomcat-pod
      image: tomcat:9.0.20-jre8-alpine
      imagePullPolicy: IfNotPresent
  restartPolicy: Always
```

![](https://img-blog.csdnimg.cn/img_convert/06e227f7fdf0c8776f1070ce7f5ae027.png)

2、镜像下载策略、重启策略

**imagePullPolicy**:

-  Always:总是拉取 pull。
-  IfNotPresent:如果本地有镜像，使用本地，如果本地没有镜像，下载镜像。
-  Never:只使用本地镜像，从不拉取。

**restartPolicy**:

- Always：只要退出就重启。
- OnFailure：失败退出时（exit code不为0）才重启。
- Never：永远不重启。

3、运行pod

```shell
## 1、查看deployment控制器
[root@k8s-master01 pod]#  kubectl get deployment
No resources found in default namespace.

## 2.查看所有的pod
[root@k8s-master01 pod]#  kubectl get pod
No resources found in default namespace.

## 3.查看镜像
[root@k8s-master01 pod]# docker images
REPOSITORY                           TAG                        IMAGE ID       CREATED         SIZE
tomcat                               9.0.37-jdk8-openjdk-slim   d60b68827676   9 months ago    305MB
tomcat                               9.0.37-jdk8                9c7be7b021c3   9 months ago    531MB
calico/node                          v3.14.2                    780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol            v3.14.2                    9dfa8f25b51c   11 months ago   22.8MB
calico/cni                           v3.14.2                    e6189009f081   11 months ago   119MB
calico/kube-controllers              v3.14.2                    4815e4106d26   11 months ago   52.8MB
k8s.gcr.io/kube-proxy                v1.17.5                    e13db435247d   14 months ago   116MB
k8s.gcr.io/kube-controller-manager   v1.17.5                    fe3d691efbf3   14 months ago   161MB
k8s.gcr.io/kube-apiserver            v1.17.5                    f640481f6db3   14 months ago   171MB
k8s.gcr.io/kube-scheduler            v1.17.5                    f648efaff966   14 months ago   94.4MB
k8s.gcr.io/coredns                   1.6.5                      70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                      3.4.3-0                    303ce5db0e90   20 months ago   288MB
tomcat                               9.0.20-jre8-alpine         387f9d021d3a   2 years ago     108MB
k8s.gcr.io/pause                     3.1                        da86e6ba6ca1   3 years ago     742kB
[root@k8s-master01 pod]# ls
namespace01.yml  tomcatpod.yml

## 4.资源文件运行pod
[root@k8s-master01 pod]# kubectl apply -f tomcatpod.yml 
pod/tomcat-pod created
[root@k8s-master01 pod]# kubectl get pod
NAME         READY   STATUS    RESTARTS   AGE
tomcat-pod   1/1     Running   0          21s

## 5.查看pod的详细信息
[root@k8s-master01 pod]# kubectl get pod -o wide
NAME         READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
tomcat-pod   1/1     Running   0          80s   10.81.85.212   k8s-node01   <none>           <none>
[root@k8s-master01 pod]# 
```

3、测试pod

```shell
curl 10.81.85.212:8080 
```

![](https://img-blog.csdnimg.cn/img_convert/283219267447b3562235c15a17cc65f5.png)

4、删除pod

```shell
[root@k8s-master01 pod]# kubectl get pods
NAME         READY   STATUS    RESTARTS   AGE
tomcat-pod   1/1     Running   0          15m
[root@k8s-master01 pod]# kubectl delete -f tomcatpod.yml 
pod "tomcat-pod" deleted
[root@k8s-master01 pod]# kubectl get pods
No resources found in default namespace.
[root@k8s-master01 pod]# 
```

==注意：不会创建默认的资源管理器！！！==

```shell
[root@k8s-master01 pod]# kubectl get deployment
No resources found in default namespace.
[root@k8s-master01 pod]#  
```

### 11.6 deployment相关操作

1、在`k8sdemo01`工程创建`tomcatdeployment.yml`文件，在文件中输入`kdep`，根据模板快速生成yml文件信息。

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210706203834.png" style="zoom:80%;" />

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tomcat-deploy
  labels:
    app: tomcat-deploy
spec:
  replicas: 3
  template:
    metadata:
      name: tomcat-deploy
      labels:
        app: tomcat-pod
    spec:
      containers:
        - name: tomcat-deploy
          image: tomcat:9.0.20-jre8-alpine
          imagePullPolicy: IfNotPresent
      restartPolicy: Always
  selector:
    matchLabels:
      app: tomcat-pod
```

![](https://img-blog.csdnimg.cn/img_convert/e263c7fc850f7a99cb5d5d0e7ea76f4a.png)

2、matchLabels

- 在Deployment中必须写`matchLables`。
- 在定义模板的时候必须定义`labels`，因为`Deployment.spec.selector`是必须字段,而他又必须和`template.labels`对应。

3、运行deployment

```shell
[root@k8s-master01 pod]# ls
namespace01.yml  tomcatdeployment.yml  tomcatpod.yml

## 1.获取deployment控制器
[root@k8s-master01 pod]# kubectl get deployment
No resources found in default namespace.

## 2、运行deployment控制器
[root@k8s-master01 pod]# kubectl apply -f tomcatdeployment.yml 
deployment.apps/tomcat-deploy created
[root@k8s-master01 pod]# kubectl get deployment
NAME            READY   UP-TO-DATE   AVAILABLE   AGE
tomcat-deploy   3/3     3            3           31s
[root@k8s-master01 pod]# 
```

4、Deployment控制器

| 控制器名称  | 具体作用                                                     |
| ----------- | ------------------------------------------------------------ |
| Deployment  | 声明式更新控制器，用于发布无状态应用。                       |
| ReplicaSet  | 副本集控制器，用于对Pod进行副本规模 扩大或剪裁。             |
| StatefulSet | 有状态副本集，用于发布有状态应用。                           |
| DaemonSet   | 在k8s集群每一个Node上运行一个副本， 用于发布监控或日志收集类等应用。 |
| Job         | 运行一次性作业任务。                                         |
| CronJob     | 运行周期性作业任务。                                         |

Deployment控制器基本介绍:

具有上线部署、滚动升级、创建副本、回滚到以前某一版本（成功/ 稳定）等功能，Deployment包含ReplicaSet，除非需要自定义升级功能或者根本不需要升级Pod，否则还是建议使用Deployment而不直接使用ReplicaSet 。

5、删除Deployment

```shell
[root@k8s-master01 pod]# kubectl get deployment
NAME            READY   UP-TO-DATE   AVAILABLE   AGE
tomcat-deploy   3/3     3            3           19m

## 1.删除控制器
[root@k8s-master01 pod]# kubectl delete -f tomcatdeployment.yml 
deployment.apps "tomcat-deploy" deleted

[root@k8s-master01 pod]# kubectl get deployment
No resources found in default namespace.
[root@k8s-master01 pod]# 
```

### 11.7 service相关操作

1、在`k8sdemo01`工程创建`tomcatservice.yml`文件，在文件中输入`kser`，根据模板快速生成yml文件信息。

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210706211125.png" style="zoom:80%;" />

```shell
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tomcat-deploy
  labels:
    app: tomcat-deploy
spec:
  replicas: 1
  template:
    metadata:
      name: tomcat-deploy
      labels:
        app: tomcat-pod
    spec:
      containers:
        - name: tomcat-deploy
          image: tomcat:9.0.20-jre8-alpine
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 8088
      restartPolicy: Always
  selector:
    matchLabels:
      app: tomcat-pod

---
apiVersion: v1
kind: Service
metadata:
  name: tomcat-svc
spec:
  selector:
    # 标签选择必须是template.labels.app
    app: tomcat-pod
  ports:
    # 对集群内其他服务暴露端口号
    - port: 8888
      targetPort: 8080
      nodePort: 30088
  type: NodePort
```

![](https://img-blog.csdnimg.cn/img_convert/835c13f3edbf8d53c784e51b000c173f.png)

2、service的selector

`service.spec.selector.app`选择的内容仍然是`template.label.app`内容，而不是`deployment`控制器的`label`内容。

3、Service类型

- `ClusterIP`：默认，分配一个集群内部可以访问的虚拟IP。
- `NodePort`：在每个Node上分配一个端口作为外部访问入口。
- `LoadBalancer`：工作在特定的Cloud Provider上，例如Google Cloud，AWS，OpenStack。
- `ExternalName`：表示把集群外部的服务引入到集群内部中来，即实现了集群内部pod和集群外部的服务进行通信。

4、Service参数

- `port `：访问service使用的端口。
- `targetPort` ：Pod中容器端口。
- `NodePort`： 通过Node实现外网用户访问k8s集群内service(30000-32767) 。

5、运行service

```shell
[root@k8s-master01 pod]# ls
namespace01.yml  tomcatdeployment.yml  tomcatpod.yml  tomcatservice.yml
## 1.运行运行service
[root@k8s-master01 pod]# kubectl apply -f tomcatservice.yml 
deployment.apps/tomcat-deploy created
service/tomcat-svc created

## 2.获取service服务
[root@k8s-master01 pod]# kubectl get svc
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.1.0.1       <none>        443/TCP          2d6h
tomcat-svc    NodePort    10.1.156.209   <none>        8888:30088/TCP   29s
tomcat9-svc   NodePort    10.1.215.214   <none>        8888:32502/TCP   25h
[root@k8s-master01 pod]# 
```

测试访问

```shell
curl 10.1.156.209:8888
```

![](https://img-blog.csdnimg.cn/img_convert/be808cdc34df7e62e37059b4499a0f56.png)

访问集群外端口

```shell
http://8.134.125.116:30088
```

![](https://img-blog.csdnimg.cn/img_convert/276a0d8169bd6cf7e4787ca6dace665d.png)

## 12- 资源清单

### 12.1 资源清单格式

1、基本介绍

资源清单有5个字段组成：`apiVersion`、`kind`、`metadata`、`spec`、`status`。

```shell
apiVersion: group/apiversion # 如果没有给定 group 名称，那么默认为 core，可以使用
kubectl apiversions # 获取当前 k8s 版本上所有的 apiVersion 版本信息(每个版本可能不同)
kind: #资源类别
metadata: #资源元数据
 name
 namespace
 lables
 annotations # 主要目的是方便用户阅读查找
spec: # 期望的状态（disired state）
status:# 当前状态，本字段有 Kubernetes 自身维护，用户不能去定义
```

2、使用kubectl命令可以查看apiVersion的各个版本信息

```shell
[root@k8s-master01 pods]# kubectl api-versions 
admissionregistration.k8s.io/v1
admissionregistration.k8s.io/v1beta1
apiextensions.k8s.io/v1
apiextensions.k8s.io/v1beta1
apiregistration.k8s.io/v1
apiregistration.k8s.io/v1beta1
.........
rbac.authorization.k8s.io/v1beta1
scheduling.k8s.io/v1
scheduling.k8s.io/v1beta1
storage.k8s.io/v1
storage.k8s.io/v1beta1
v1
[root@k8s-master01 pods]# 
```

3、字段配置格式类型

资源清单中大致可以分为以下类型

```shell
apiVersion <string> #表示字符串类型
metadata <Object> #表示需要嵌套多层字段
labels <map[string]string> #表示由k:v组成的映射
finalizers <[]string> #表示字串列表
ownerReferences <[]Object> #表示对象列表
hostPID <boolean> #布尔类型
priority <integer> #整型
name <string> -required- #如果类型后面接 -required-，表示为必填字段
```

### 12.2 pod生命周期

1、环境所需要镜像

```shell
docker pull busybox:1.32.0
```

![](https://img-blog.csdnimg.cn/img_convert/69883b83d725b31804aa0b38555ef2af.png)

2、注意事项:

-  `readiness`探测成功后，Pod才会改变成Ready或者Running等状态！！
-  `Liveness`探测主容器已经损坏，不能正常工作，就会执行相应的策略！！

#### 12.2.1 深入理解initC

1、initC基本特点

- `initC`总是运行到成功完成为止，每个`initC`容器都必须在下一个`initC`启动之前成功完成。
- 如果`initC`容器运行失败，K8S集群会不断的重启该`pod`，直到`initC`容器成功为止。
- 如果pod对应的`restartPolicy`为`never`，它就不会重新启动。

2、在`k8sdemo01`工程创建`initcpod.yml`文件

```yml
apiVersion: v1
kind: Pod
metadata:
  name: initcpod-test
  labels:
    app: initcpod-test
spec:
  containers:
    - name: initcpod-test #相位
      image: busybox:1.32.0
      imagePullPolicy: IfNotPresent
      command: ['sh','-c','echo The app is running! && sleep 3600']
  initContainers:
    - name: init-myservice
      image: busybox:1.32.0
      imagePullPolicy: IfNotPresent
      command: ['sh','-c','until nslookup myservice; do echo waitting for myservice; sleep 2; done;']
    - name: init-mydb
      imagePullPolicy: IfNotPresent
      image: busybox:1.32.0
      command: ['sh','-c','until nslookup mydb; do echo waitting for mydb; sleep 2; done;']
  restartPolicy: Always
```

3、获取节点

```shell
[root@k8s-master01 pods]# ls
initcpod.yml 
[root@k8s-master01 pods]# kubectl apply -f initcpod.yml 
pod/initcpod-test created
[root@k8s-master01 pods]# kubectl get pod
NAME            READY   STATUS     RESTARTS   AGE
initcpod-test   0/1     Init:1/2   0          22s
[root@k8s-master01 pods]# kubectl get pod -o wide
NAME            READY   STATUS     RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
initcpod-test   0/1     Init:1/2   0          38s   10.81.85.228   k8s-node01   <none>           <none>
[root@k8s-master01 pods]# 
```

4、在`k8sdemo01`工程创建`initcservice1.yml`和`initcservice2.yml`文件

**initcservice1.yml**

```yml
apiVersion: v1
kind: Service
metadata:
  name: myservice
spec:
  selector:
    app: myservice
  ports:
    - port: 80
      targetPort: 9376
      protocol: TCP
```

**initcservice2.yml**

```yml
apiVersion: v1
kind: Service
metadata:
  name: mydb
spec:
  selector:
    app: mydb
  ports:
    - port: 80
      targetPort: 9377
      protocol: TCP
```

5、使用Remote Host，将本工程中的文件上传k8s集群 

![](https://img-blog.csdnimg.cn/img_convert/d1d2a4d559bd01379c3ae27ac5539247.png)

6、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

```shell
[root@k8s-master01 pods]# ls
initcpod.yml       initcservice2.yml
initcservice1.yml  
# 1、运行initcservice1服务
[root@k8s-master01 pods]# kubectl apply -f initcservice1.yml
service/myservice created
# 2、运行initcservice2服务
[root@k8s-master01 pods]# kubectl apply -f initcservice2.yml
service/mydb created

# 3、查看服务运行情况
[root@k8s-master01 pods]# kubectl get svc
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.1.0.1       <none>        443/TCP   4d2h
mydb         ClusterIP   10.1.100.194   <none>        80/TCP    30s
myservice    ClusterIP   10.1.176.237   <none>        80/TCP    50s
[root@k8s-master01 pods]# kubectl apply -f initcpod.yml 
pod/initcpod-test created
# 4、发现pod的两个init已经就绪，pod状态为ready
[root@k8s-master01 pods]# kubectl get pod -w
NAME            READY   STATUS     RESTARTS   AGE
initcpod-test   0/1     Init:1/2   0          32s
initcpod-test   0/1     PodInitializing   0          2m32s
initcpod-test   1/1     Running           0          2m33s
```

#### 12.2.2 readinessProbe(就绪检测)

1、环境所需的镜像。

```shell
docker pull nginx:1.17.10-alpine
```

2、在`k8sdemo01`工程创建`readinessProbe.yml`文件

```yml
aapiVersion: v1
kind: Pod
metadata:
  name: readinesspod-test
  labels:
    app: readinesspod-test
spec:
  containers:
    - name: readinesspod-test
      image: nginx:1.17.10-alpine
      imagePullPolicy: IfNotPresent
      readinessProbe:
        httpGet:
          port: 80
          path: /index1.html
        initialDelaySeconds: 2
        periodSeconds: 3
  restartPolicy: Always
```

3、使用Remote Host，将本工程中的文件上传k8s集群 

![](https://img-blog.csdnimg.cn/img_convert/1e8d834e8ac6e5493a2d06de44f96111.png)

 4、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

```shell
[root@k8s-master01 pods]# ls
initcpod.yml  initcservice1.yml  initcservice2.yml  readinessProbe.yml
# 1、创建pod
[root@k8s-master01 pods]# kubectl apply -f readinessProbe.yml 
pod/readinesspod-test created
# 2、检查pod状态，虽然pod状态显示running但是ready显示0/1，因为就绪检查未通过
[root@k8s-master01 pods]# kubectl get pod
NAME                READY   STATUS    RESTARTS   AGE
readinesspod-test   0/1     Running   0          5m57s
# 3、进入pod内部
[root@k8s-master01 pods]# kubectl exec -it readinesspod-test sh

# 4、进入容器内目录
/ # cd /usr/share/nginx/html/

# 5、追加一个index1.html文件
/usr/share/nginx/html # echo "hello k8s" >> index1.html
/usr/share/nginx/html # ls
50x.html     index.html   index1.html
# 6、退出容器，再次查看pod状态，pod已经正常启动
/usr/share/nginx/html # exit
[root@k8s-master01 pods]# kubectl get pod
NAME                READY   STATUS    RESTARTS   AGE
readinesspod-test   1/1     Running   0          7m38s
[root@k8s-master01 pods]# 
```

#### 12.2.3 livenessProbe(存活检测)

1、环境所需要镜像

```shell
docker pull busybox:1.32.0
```

2、在`k8sdemo01`工程创建`livenessprobe1.yml`文件

```yml
apiVersion: v1
kind: Pod
metadata:
  name: livenessprobepod1-test
  labels:
    app: livenessprobepod1-test
spec:
  containers:
    - name: livenessprobepod1-test
      image: busybox:1.32.0
      imagePullPolicy: IfNotPresent
      command: ['/bin/sh','-c','touch /tmp/livenesspod;sleep 30; rm -rf /tmp/livenesspod; sleep 3600']
      livenessProbe:
        exec:
          command: ['test','-e','/tmp/livenesspod']
        initialDelaySeconds: 1
        periodSeconds: 3
  restartPolicy: Always
```

3、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://img-blog.csdnimg.cn/img_convert/5ae07b444ea18b8a6a13592ac80d2b1d.png)

```shell
[root@k8s-master01 pods]# ls
initcpod.yml  initcservice1.yml  initcservice2.yml  livenessprobe1.yml  readinessProbe.yml
# 1、创建pod
[root@k8s-master01 pods]# kubectl apply -f livenessprobe1.yml 
pod/livenessprobepod1-test created
# 2、监控pod状态变化,容器正常启动
[root@k8s-master01 pods]# kubectl get pod -w
NAME                     READY   STATUS    RESTARTS   AGE
livenessprobepod1-test   1/1     Running   0          23s
readinesspod-test        1/1     Running   0          48m
# 3、等待30秒后，发现pod的RESTARTS值从0变为1.说明pod已经重启一次
livenessprobepod1-test   1/1     Running   1          70s
livenessprobepod1-test   1/1     Running   2          2m19s
livenessprobepod1-test   1/1     Running   3          3m27s
livenessprobepod1-test   1/1     Running   4          4m36s
livenessprobepod1-test   1/1     Running   5          5m46s
^C[root@k8s-master01 pods]# 
```

3、环境所需要镜像

```shell
docker pull nginx:1.17.10-alpine
```

4、在`k8sdemo01`工程创建`livenessprobe2.yml`文件

```yml
apiVersion: v1
kind: Pod
metadata:
  name: livenesspod2-test
  labels:
    app: livenesspod2-test
spec:
  containers:
    - name: livenesspod2-test
      image: nginx:1.17.10-alpine
      imagePullPolicy: IfNotPresent
      livenessProbe:
        httpGet:
          port: 80
          path: /index.html
        initialDelaySeconds: 3
        timeoutSeconds: 5
  restartPolicy: Always
```

5、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210707213708.png" style="zoom:80%;" />

```shell
[root@k8s-master01 pods]# ls
initcpod.yml       initcservice2.yml   livenessprobe2.yml
initcservice1.yml  livenessprobe1.yml  readinessProbe.yml

# 1、创建pod
[root@k8s-master01 pods]# kubectl apply -f livenessprobe2.yml 
pod/livenesspod2-test created
# 2、查看pod状态
[root@k8s-master01 pods]# kubectl get pod
NAME                READY   STATUS    RESTARTS   AGE
livenesspod2-test   1/1     Running   0          10s

# 3、查看容器IP，访问index.html页面，index.html页面可以正常访问
[root@k8s-master01 pods]# kubectl get pod -o wide
NAME                READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
livenesspod2-test   1/1     Running   0          19s   10.81.85.223   k8s-node01   <none>           <none>
[root@k8s-master01 pods]# curl 10.81.85.223
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

# 4、进入容器内部
[root@k8s-master01 pods]# kubectl exec -it livenesspod2-test sh

# 5、删除index.html文件,退出容器
/ # rm -rf //usr/share/nginx/html/index.html
/ # exit

# 6、再次监控pod状态，等待一段时间后，发现pod的RESTARTS值从0变为1.说明pod已经重启一次。
[root@k8s-master01 pods]# kubectl get pod -w
NAME                READY   STATUS    RESTARTS   AGE
livenesspod2-test   1/1     Running   0          92s
livenesspod2-test   1/1     Running   1          97s
^C[root@k8s-master01 pods]# kubectl get pods -o wide
NAME                READY   STATUS    RESTARTS   AGE    IP             NODE         NOMINATED NODE   READINESS GATES
livenesspod2-test   1/1     Running   1          113s   10.81.85.223   k8s-node01   <none>           <none>
[root@k8s-master01 pods]# curl 10.81.85.223
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
# 7、进入容器删除文件一条命令执行rm -rf命令后退出容器。
[root@k8s-master01 pods]# kubectl exec -it livenesspod2-test -- rm -rf /usr/share/nginx/html/index.html

# 8、再次监控pod状态，等待一段时间后，发现pod的RESTARTS值从1变为2.说明pod已经重启一次。
[root@k8s-master01 pods]# kubectl get pod -w
NAME                READY   STATUS    RESTARTS   AGE
livenesspod2-test   1/1     Running   1          2m43s
livenesspod2-test   1/1     Running   2          2m57s
^C
[root@k8s-master01 pods]# 
```

小结: `liveness`监控`index.html`页面已经被删除，所以pod需要重新启动，重启后又重新创建nginx镜像，nginx镜像中默认有`index.html`页面。

6、环境所需要镜像

```shell
docker pull nginx:1.17.10-alpine
```

7、在`k8sdemo01`工程创建`livenessprobe3.yml`文件

```yml
apiVersion: v1
kind: Pod
metadata:
  name: livenesspod3-test
  labels:
    app: livenesspod3-test
spec:
  containers:
    - name: livenesspod3-test
      image: nginx:1.17.10-alpine
      imagePullPolicy: IfNotPresent
      livenessProbe:
        tcpSocket:
          port: 8080
        initialDelaySeconds: 6
        periodSeconds: 3
        timeoutSeconds: 5
  restartPolicy: Always
```

8、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://img-blog.csdnimg.cn/img_convert/9ccecce22e90bde431365c6527e67458.png)

```shell
# 1、创建pod
[root@k8s-master01 pods]# kubectl apply -f livenessprobe3.yml 
pod/livenesspod3-test created
# 2、查看pod状态，存活检测监听8080端口，8080端口没有反馈信息后重启pod，RESTARTS值从0变为1。
[root@k8s-master01 pods]# kubectl get pod -w
NAME                READY   STATUS              RESTARTS   AGE
livenesspod3-test   1/1     Running             0          31s
livenesspod3-test   1/1     Running             1          45s
livenesspod3-test   1/1     Running             2          57s
livenesspod3-test   1/1     Running             3          69s
livenesspod3-test   0/1     CrashLoopBackOff    3          80s
livenesspod3-test   1/1     Running             4          110s
livenesspod3-test   1/1     Running             5          2m2s
livenesspod3-test   0/1     CrashLoopBackOff    5          2m14s
^C
[root@k8s-master01 pods]# 
```

#### 12.2.4 postStart函数

1、环境所需要镜像

```shell
docker pull busybox:1.32.0
```

2、在`k8sdemo01`工程创建`poststart.yml`文件

```yml
apiVersion: v1
kind: Pod
metadata:
  name: lifecle-test
  labels:
    app: lifecle-test
spec:
  containers:
    - name: poststart-test
      image: busybox:1.32.0
      imagePullPolicy: IfNotPresent
      command: ['sh','-c','sleep 2000']
      lifecycle:
        postStart:
          exec:
            command: ['mkdir','-p','/k8s/index.html']
  restartPolicy: Always
```

3、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://img-blog.csdnimg.cn/img_convert/f0800c755c241dcde71b8342268674fd.png)

```shell
[root@k8s-master01 pods]# ls
initcpod.yml       initcservice2.yml   livenessprobe2.yml  poststart.yml
initcservice1.yml  livenessprobe1.yml  livenessprobe3.yml  readinessProbe.yml
# 1、创建pod
[root@k8s-master01 pods]# kubectl apply -f poststart.yml 
pod/poststart-test created
# 2、查看pod状态
[root@k8s-master01 pods]# kubectl get pod
NAME             READY   STATUS    RESTARTS   AGE
poststart-test   1/1     Running   0          13s
# 3、进入容器内部，查看是否创建了/k8s/index.html文件
[root@k8s-master01 pods]# kubectl exec -it poststart-test sh
/ # ls
bin   dev   etc   home  k8s   proc  root  sys   tmp   usr   var
/ # cd /k8s/
/k8s # ls
index.html
/k8s # cd index.html/
/k8s/index.html # ls
/k8s/index.html # exit
[root@k8s-master01 pods]# 
```

### 12.3 pod周期总结

==pod对象自从创建开始至终止退出的时间范围称为生命周期==，在这段时间中，pod会处于多种不同的状态，并执行一些操作；其中，创建主容器为必须的操作，其他可选的操作还包括运行【初始化容器(init container)】、【容器启动后钩子(start hook)】、【容器的存活性探测(liveness probe)】、【就绪性探测(readiness probe)】、【容器终止前钩子(pre stop hook)】等，这些操作是否执行则取决于pod的定义 。

#### 12.3.1 pod相位

使用 `kubectl get pods `命令,`STATUS`被称之为相位(phase)。
无论是手动创建还是通过控制器创建pod，pod对象处于生命进程中以下相位：

- `pending`：**apiserver**创建了pod资源对象并存入etcd中，但它尚未被调度完成或者仍处于下载镜像的过程中。
- `running`：pod已经被调度至某节点，并且所有容器都已经被kubelet创建完成。
- `succeeded`：pod中的所有容器都已经成功终止并且不会被重启。
- `failed`：所有容器都已经终止，但至少有一个容器终止失败，即容器返回了非0值的退出状态或已经被系统终止。
- `unknown`：apiserver无法正常获取到pod对象的状态信息，通常是由于其无法于所在工作节点的kubelet通信所致。

注意: ==pod的相位是在其生命周期中的宏观概念，而非对容器或pod对象的综合汇总，而且相位的数量和含义被严格界定==。

#### 12.3.2 pod创建过程

pod是k8s的基础单元，以下为一个pod资源对象的典型创建过程：

- 用户通过kubectl或其他api客户端提交pod spec给api server
- api server尝试着将pod对象的相关信息存入etcd中，待写入操作执行完成，api server即会返回确认信息至客户端。
- api server开始反映etcd中的状态变化，所有的k8s组件均使用watch机制来跟踪检查api server上的相关变动。
- kube-scheduler通过其watch觉察到api server创建了新的pod对象但尚未绑定至任何工作节点。
- kube-scheduler为pod对象挑选一个工作节点并将结果信息更新至api server。
- 调度结果信息由api server更新至etcd，而且api server也开始反映此pod对象的调度结果。
- pod被调度到目标工作节点上的kubelet尝试在当前节点上调用docker启动容器，并将容器的结果状态回送至api server。
- api server将pod状态信息存入etcd中，在etcd确认写入操作成功完成后，api server将确认信息发送至相关的kubelet。

#### 12.3.3 pod生命周期重要行为

用户可以为pod对象定义其生命周期中的多种行为，如==初始化容器、存活性探测及就绪性探测==等。

1、初始化容器

初始化容器即应用程序的主容器启动之前要运行的容器，常用于为主容器执行一些预置操作，它们具有两种典型特征：

- 初始化容器必须运行完成直至结束，若某初始化容器运行失败，那么k8s需要重启它直到成功完成。
- 每个初始化容器都必须按定义的顺序串行运行。

2、有不少场景都需要在应用容器启动之前进行部分初始化操作，例如，等待其他相关联组件服务可用、基于环境变量或配置模板为应用程序生成配置文件、从配置中心获取配置等。初始化容器的典型应用需求具体包含如下几种方式:

- 用于运行特定的工具程序，出于安全等反面的原因，这些程序不适于包含在主容器镜像中。

- 提供主容器镜像中不具备的工具程序或自定义代码。

- 为容器镜像的构建和部署人员提供了分离、独立工作的途径，使得它们不必协同起来制作单个镜像文件。

- 初始化容器和主容器处于不同的文件系统视图中，因此可以分别安全地使用敏感数据。

注意: pod资源的`spec.initContainers`字段以列表的形式定义可用的初始容器，其嵌套可用字段类似于`spec.containers`。

#### 12.3.4 生命周期钩子函数

1、容器生命周期钩子使它能够感知其自身生命周期管理中的事件，并在相应的时刻到来时运行由用户指定的处理程序代码。

2、k8s为容器提供了两种生命周期钩子:

- `postStart`：于容器创建完成之后立即运行的钩子处理器`(handler)`，不过k8s无法确保它一定会于容器中的entrypoint之前运行。
- `preStop`：于容器终止操作之前立即运行的钩子处理器，它以同步的方式调用，因此在其完成之前会阻塞删除容器的操作调用。

3、钩子处理器的实现方法由Exec和HTTP两种，前一种在钩子事件触发时直接在当前容器中运行由用户定义的命令，后一种则是在当前容器中向某url发起http请求。`postStart`和`preStop`处理器定义在`spec.lifecycle`嵌套字段中。

#### 12.3.5 容器探测

1、容器探测时pod对象生命周期中的一项重要的日常任务，它是kubelet对容器周期性执行的健康状态诊断，诊断操作由容器的处理器进行定义。

2、k8s支持三种容器探针用于pod探测:

- `ExecAction`：在容器中执行一个命令，并根据其返回的状态码进行诊断的操作称为Exec探测，状态码为0表示成功，否则即为不健康状态。
- `TCPSocketAction`：通过与容器的某TCP端口尝试建立连接进行诊断，端口能够成功打开即为正常，否则为不健康状态。
- `HTTPGetAction`：通过向容器IP地址的某指定端口的指定path发起HTTP GET请求进行诊断，响应码大于等于200且小于400时即为成功。

3、任何一种探测方式都可能存在三种结果：

- `success(成功)`：容器通过了诊断。
- `failure(失败)`：容器未通过了诊断。
- `unknown(未知)`：诊断失败，因此不会采取任何行动。

4、kubelet可在活动容器上执行两种类型的检测：

- **(livenessProbe)存活性检测**：用于判定容器是否处于运行状态，一旦此类检测未通过，kubelet将杀死容器并根据`restartPolicy`决定是否将其重启；未定义存活性检测的容器的默认状态未`success`。
- **(readinessProbe)就绪性检测**：用于判断容器是否准备就绪并可对外提供服务；未通过检测的容器意味着尚未准备就绪，端点控制器会将其IP从所有匹配到此pod对象的`service`对象的端点列表中移除；检测通过之后，会再次将其IP添加至端点列表中。

#### 12.3.6 容器重启策略

容器程序发生奔溃或容器申请超出限制的资源等原因都可能会导致pod对象的终止，此时是否应该重建该pod对象则取决于其重启策略（restartPolicy）属性的定义:

- Always：但凡pod对象终止就将其重启，此为默认设定。
- OnFailure：尽在pod对象出现错误时方才将其重启。
- Never：从不重启。

restartPolicy适用于pod对象中的所有容器，而且它仅用于控制在同一节点上重新启动pod对象的相关容器。首次需要重启的容器，将在其需要时立即进行重启，随后再次需要重启的操作将由kubelet延迟一段时间后进行，且反复的重启操作的延迟时长以此为10s、20s、40s、80s、160s和300s，300s是最大延迟时长。==事实上，一旦绑定到一个节点，pod对象将永远不会重新绑定到另一个节点，它要么被重启，要么终止，直到节点发生故障或被删除。==

#### 12.3.7 pod终止过程

1、当用户提交删除请求之后，系统就会进行强制删除操作的宽限期倒计时，并将TERM信息发送给pod对象的每个容器中的主进程。宽限期倒计时结束后，这些进程将收到强制终止的KILL信号，pod对象随即也将由api server删除，如果在等待进程终止的过程中，kubelet或容器管理器发生了重启，那么终止操作会重新获得一个满额的删除宽限期并重新执行删除操作。

2、一个典型的pod对象终止流程具体如下：

- 用户发送删除pod对象的命令，api服务器中的pod对象会随着时间的推移而更新，在宽限期内(默认30s)，pod被视为`dead`。
- 将pod标记为`terminating`状态，kubelet在监控到pod对象转为`terminating`状态的同时启动pod关闭过程。
- 将pod标记为`terminating`状态，端点控制器监控到pod对象的关闭行为时将其从所有匹配到此端点的service资源的端点列表中移除。
- 如果当前pod对象定义了`preStop`钩子处理器，则在其标记为`terminating`后即会以同步的方式启动执行，若宽限期结束后，`preStop`仍未执行结束，则第二步会被重新执行并额外获取一个时长为`2s`的小宽限期。
- pod对象中的容器进程收到`TERM`信号，宽限期结束后，若存在任何一个仍在运行的进程，那么`pod`对象即会收到`SIGKILL`信号。
- kubelet请求`api server`将此pod资源的宽限期设置为0从而完成删除操作，它变得对用户不再可见。

3、注意事项

默认情况下，所有删除操作的宽限期都是`30s`，不过，kubectl delete命令可以使用`--grace-period=`选项自定义其时长，若使用0值则表示直接强制删除指定的资源，不过此时需要同时使用命令`--forece`选项。

## 13-资源控制器

### 13.1 什么是资源控制器

1、**Controller Manager(资源控制器)**由`kube-controller-manager` 和 `cloud-controller-manager `组成， 是Kubernetes 的大脑，它通过 apiserver 监控整个集群的状态， 并确保集群处于预期的工作状态。

2、**kube-controller-manager** 

[kube-controller-manager](https://kubernetes.io/docs/admin/kube-controller-manager)运行管理控制器，它们是集群中处理常规任务的后台线程，逻辑上，每个控制器是一个单独的进程，但为了降低复杂性，它们都被编译成单个二进制文件，并在单个进程中运行。

这些控制器包括：

- [节点（Node）控制器](http://docs.kubernetes.org.cn/304.html)。
- 副本（Replication）控制器：负责维护系统中每个副本中的pod。
- 端点（Endpoints）控制器：填充Endpoints对象（即连接Services＆Pods）。
- [Service Account](http://docs.kubernetes.org.cn/84.html)和Token控制器：为新的[Namespace](http://docs.kubernetes.org.cn/242.html) 创建默认帐户访问API Token。

3、**cloud-controller-manager**

- 云控制器管理器负责与底层云提供商的平台交互。云控制器管理器是Kubernetes版本1.6中引入的，目前还是Alpha的功能。
- 云控制器管理器仅运行云提供商特定的（controller loops）控制器循环。可以通过将`--cloud-provider` flag设置为external。
- 启动`kube-controller-manager` 来禁用控制器循环。

cloud-controller-manager 具体功能

- 节点(Node Controller)控制器
- 路由(Route Controller)控制器
- Service(Service Controller)控制器
- 卷(VolumeController)控制器

### 13.2  常见Pod控制器

1、**ReplicaSet**:适合无状态的服务部署

```yml
用户创建指定数量的pod副本数量，确保pod副本数量符合预期状态，并且支持滚动式自动扩容和缩容功能。ReplicaSet主要三个组件组成：
```

- 用户期望的pod副本数量。
- 标签选择器，判断哪个pod归自己管理。
- 当现存的pod数量不足，会根据pod资源模板进行新建。

注意点：

帮助用户管理无状态的pod资源，精确反应用户定义的目标数量，但是RelicaSet不是直接使用的控制器，而是使用Deployment。

2、**deployment**：适合无状态的服务部署，工作在ReplicaSet之上，用于管理无状态应用，目前来说最好的控制器。

支持滚动更新和回滚功能，还提供声明式配置。

3**、StatefullSet**：适合有状态的服务部署。需要学完存储卷后进行系统学习。

4、**DaemonSet**：一次部署，所有的node节点都会部署，一些典型的应用场景：

- 运行集群存储 daemon，例如在每个Node上运行 glusterd、ceph。
- 在每个Node上运行日志收集 daemon，例如 fluentd、 logstash
- 在每个Node上运行监控 daemon，例如 Prometheus Node Exporter
- **注意点**: 用于确保集群中的每一个节点只运行特定的pod副本，通常用于实现系统级后台任务。
- **特性**：服务是无状态的服务必须是守护进程

5、**Job**：一次性的执行任务，只要完成就立即退出，不需要重启或重建。

6、**Cronjob**：周期性的执行任务，周期性任务控制，不需要持续后台运行。

### 13.3 Replication Controller

#### 13.3.1 基本概念

replication controller简称RC，是kubernetes系统中的核心概念之一，简单来说，它其实定义了一个期望的场景，即声明某种pod的副本数量在任意时刻都复合某个预期值，所以RC的定义包含以下部分

- pod期待的副本数量。
- 用于筛选目标pod的Label Selector。
- 当pod的副本数量小于期望值时，用于创建新的pod的pod模板(template)。

#### 13.3.2 ReplicaSet

1、基本简介

- `ReplicationController`用来确保容器应用的副本数始终保持在用户定义的副本数，即如果有容器异常退出，会自动创建新的Pod来替代，而如果异常多出来的容器也会自动回收。
- ==在新版本的Kubernetes中建议使用ReplicaSet来取代ReplicationController==。ReplicaSet跟ReplicationController没有本质的不同，只是名字不一样，并且ReplicaSet支持集合式的selector。
- 虽然ReplicaSet可以独立使用，但一般还是建议使用 Deployment 来自动管理ReplicaSet，这样就无需担心跟其他机制的不兼容问题（比如ReplicaSet不支持rolling-update但Deployment支持）。

2、环境所需镜像

```yml
docker pull nginx:1.17.10-alpine
docker pull nginx:1.18.0-alpine
docker pull nginx:1.19.2-alpine
```

3、ReplicaSet模板说明

```yml
apiVersion: apps/v1 #api版本定义
kind: ReplicaSet #定义资源类型为ReplicaSet
metadata: #元数据定义
 name: guardwhy
 namespace: default
spec: #ReplicaSet的规格定义
 replicas: 2 #定义副本数量为2个
 selector: #标签选择器，定义匹配pod的标签
   matchLabels:
     app: guardwhy
     release: canary
 template: #pod的模板定义
   metadata: #pod的元数据定义
     name: guardwhy-pod #自定义pod的名称
     labels: #定义pod的标签，需要和上面定义的标签一致，也可以多出其他标签
       app: guardwhy
       release: canary
       environment: qa
   spec: #pod的规格定义
     containers: #容器定义
     - name: guardwhy-container #容器名称
      image: nginx:1.17.10-alpine #容器镜像
      ports: #暴露端口
      - name: http
       containerPort: 80
```

#### 13.3.3 部署ReplicaSet

1、在`k8sdemo01`工程创建`replicasetdemo.yml`文件

```yml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicasetdemo
  labels:
    app: replicasetdemo
spec:
  replicas: 1
  template:
    metadata:
      name: replicasetdemo
      labels:
        app: replicasetdemo
    spec:
      containers:
        - name: replicasetdemo
          image: nginx:1.17.10-alpine
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 80
      restartPolicy: Always
  selector:
    matchLabels:
      app: replicasetdemo
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210708223817.png)

```shell
[root@k8s-master01 controller]# ls
replicasetdemo.yml
# 1、运行ReplicaSet
[root@k8s-master01 controller]# kubectl apply -f replicasetdemo.yml 
replicaset.apps/replicasetdemo created
# 2、查看rs控制器
[root@k8s-master01 controller]# kubectl get rs
NAME             DESIRED   CURRENT   READY   AGE
replicasetdemo   1         1         1       25s
# 3、查看pod信息
[root@k8s-master01 controller]# kubectl get pod
NAME                   READY   STATUS    RESTARTS   AGE
replicasetdemo-2gllp   1/1     Running   0          34s

# 4、查看pod详细信息
[root@k8s-master01 controller]# kubectl describe pod replicasetdemo-2gllp 
Name:         replicasetdemo-2gllp
Namespace:    default
Priority:     0
Node:         k8s-node01/172.21.252.4
Start Time:   Thu, 08 Jul 2021 22:43:10 +0800
Labels:       app=replicasetdemo
Annotations:  cni.projectcalico.org/podIP: 10.81.85.230/32
              cni.projectcalico.org/podIPs: 10.81.85.230/32
Status:       Running
IP:           10.81.85.230
IPs:
  IP:           10.81.85.230
Controlled By:  ReplicaSet/replicasetdemo
.....................
Events:
  Type    Reason     Age        From                 Message
  ----    ------     ----       ----                 -------
  Normal  Scheduled  <unknown>  default-scheduler    Successfully assigned default/replicasetdemo-2gllp to k8s-node01
  Normal  Pulled     67s        kubelet, k8s-node01  Container image "nginx:1.17.10-alpine" already present on machine
  Normal  Created    67s        kubelet, k8s-node01  Created container replicasetdemo
  Normal  Started    67s        kubelet, k8s-node01  Started container replicasetdemo
  
# 5、测试controller控制器下的pod删除、重新被controller控制器拉起
[root@k8s-master01 controller]# kubectl delete pod --all
pod "replicasetdemo-2gllp" deleted
[root@k8s-master01 controller]# kubectl get pod
NAME                   READY   STATUS    RESTARTS   AGE
replicasetdemo-6kbdn   1/1     Running   0          110s
[root@k8s-master01 controller]# kubectl get pod -o wide
NAME                   READY   STATUS    RESTARTS   AGE    IP             NODE         NOMINATED NODE   READINESS GATES
replicasetdemo-6kbdn   1/1     Running   0          2m2s   10.81.58.214   k8s-node02   <none>           <none>
[root@k8s-master01 controller]# curl 10.81.58.214
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
..............
</html>

# 6、修改pod的副本数量:通过命令行方式
[root@k8s-master01 controller]# kubectl scale replicaset replicasetdemo --replicas=3
replicaset.apps/replicasetdemo scaled
[root@k8s-master01 controller]# kubectl get pod
NAME                   READY   STATUS    RESTARTS   AGE
replicasetdemo-6kbdn   1/1     Running   0          14m
replicasetdemo-g5664   1/1     Running   0          22s
replicasetdemo-t8ksq   1/1     Running   0          22s
# 7、修改pod的副本数量:通过资源清单方式
[root@k8s-master01 controller]# kubectl edit replicasets.apps replicasetdemo 

# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"apps/v1","kind":"ReplicaSet","metadata":{"annotations":{},"labels":{"app":"replicasetdemo"},"name":"replicasetdemo","namespace":"default"},"spec":{"replicas":1,"selector":{"matchLabels":{"app":"replicasetdemo"}},"template":{"metadata":{"labels":{"app":"replicasetdemo"},"name":"replicasetdemo"},"spec":{"containers":[{"image":"nginx:1.17.10-alpine","imagePullPolicy":"IfNotPresent","name":"replicasetdemo","ports":[{"containerPort":80}]}],"restartPolicy":"Always"}}}}
  creationTimestamp: "2021-07-08T14:43:10Z"
  generation: 5
  labels:
    app: replicasetdemo
  name: replicasetdemo
  namespace: default
  resourceVersion: "294582"
  selfLink: /apis/apps/v1/namespaces/default/replicasets/replicasetdemo
"/tmp/kubectl-edit-6ttin.yaml" 52L, 1886C
[root@k8s-master01 controller]# kubectl get pod
NAME                   READY   STATUS    RESTARTS   AGE
replicasetdemo-47672   1/1     Running   0          11s
replicasetdemo-6kbdn   1/1     Running   0          19m
replicasetdemo-g5664   1/1     Running   0          5m39s
replicasetdemo-smddx   1/1     Running   0          11s
replicasetdemo-t8ksq   1/1     Running   0          5m39s
[root@k8s-master01 controller]# 
```

3、显示Pod标签

```shell
# 1、显示pod的标签
[root@k8s-master01 controller]# kubectl get pod --show-labels 
NAME                   READY   STATUS    RESTARTS   AGE   LABELS
replicasetdemo-47672   1/1     Running   0          13m   app=replicasetdemo
replicasetdemo-6kbdn   1/1     Running   0          32m   app=replicasetdemo
replicasetdemo-g5664   1/1     Running   0          18m   app=replicasetdemo
replicasetdemo-smddx   1/1     Running   0          13m   app=replicasetdemo
replicasetdemo-t8ksq   1/1     Running   0          18m   app=replicasetdemo
# 2、修改pod标签(label)
[root@k8s-master01 controller]# kubectl label pod replicasetdemo-g5664  app=guardwhy --overwrite=True
pod/replicasetdemo-g5664 labeled
# 3、再次显示pod的标签
[root@k8s-master01 controller]# kubectl get pod --show-labels 
NAME                   READY   STATUS    RESTARTS   AGE   LABELS
replicasetdemo-47672   1/1     Running   0          15m   app=replicasetdemo
replicasetdemo-6kbdn   1/1     Running   0          34m   app=replicasetdemo
replicasetdemo-g5664   1/1     Running   0          21m   app=guardwhy
replicasetdemo-hsbx5   1/1     Running   0          4s    app=replicasetdemo
replicasetdemo-smddx   1/1     Running   0          15m   app=replicasetdemo
replicasetdemo-t8ksq   1/1     Running   0          21m   app=replicasetdemo
# 4、查看rs控制器
[root@k8s-master01 controller]# kubectl get rs
NAME             DESIRED   CURRENT   READY   AGE
replicasetdemo   5         5         5       40m
# 4、查看控制器
[root@k8s-master01 controller]# kubectl delete rs replicasetdemo
replicaset.apps "replicasetdemo" deleted
[root@k8s-master01 controller]# kubectl get rs
No resources found in default namespace.
[root@k8s-master01 controller]# 
```

#### 13.3.4 ReplicaSet小结

1、kubectl命令行工具适用于RC的绝大部分命令同样适用于ReplicaSet，当前很少单独适用`ReplicaSet`，它主要被`Deployment`这个更高层的资源对象所使用，从而形成一整套Pod创建，删除，更新的编排机制，在使用`Deployment`时无需关心它是如何维护和创建`ReplicaSet`的，这一切都是自动发生的。

2、总结一下`RC(ReplicaSet)`特性和作用

- 在绝大多数情况下，通过定义一个RC实现Pod的创建及副本数量的自动控制。
- 在RC里包括完整的Pod定义模板，RC通过Label Selector机制实现对Pod副本的自动控制。
- 通过改变RC里的Pod副本数量，可以实现Pod的扩容和缩容。
- 通过改变RC里Pod模板中的镜像版本，可以实现滚动升级。

### 13.4 Deployment

#### 13.4.1 基本概念

1、Deployment是kubernetes在1.2版本中引入的新概念，用于更好的解决Pod的编排问题，keployment在内部使用了ReplicaSet来实现目的，可以把Deployment理解为ReplicaSet的一次升级。

2、Deployment的使用过程

- 创建一个`Deployment`对象来生成对应的`ReplicaSet`并完成Pod副本的创建。
- 检查`Deployment`的状态来看部署动作是否完成(Pod副本数量是否达到了预期的值)。
- 更新`Deployment`以创建新的Pod(比如镜像升级)，如果当前`Deployment`不稳定，可以回滚到一个早先的`Deployment`版本。
- 暂停`Deployment`以便于一次性修改多个`PodTemplateSpec`的配置项，之后在恢复`Deployment`，进行新的发布。
- 扩展`Deployment`以应对高负载，查看`Deployment`的状态，以此作为发布是否成功的标志，清理不在需要的旧版本`ReplicaSet`。

#### 13.4.2 部署Deployment

1、可以通过`kubectl`命令行方式获取更加详细的信息

```shell
kubectl explain deploy
kubectl explain deploy.spec
```

2、在`k8sdemo01`工程创建`deploymentdemo.yml`文件

Deployment除了API生命与Kind类型有区别，Deployment的定义与Replica Set的定义很类似。

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deploymentdemo
  labels:
    app: deploymentdemo
spec:
  replicas: 3
  template:
    metadata:
      name: deploymentdemo
      labels:
        app: deploymentdemo
    spec:
      containers:
        - name: deploymentdemo
          image: nginx:1.17.10-alpine
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 80
      restartPolicy: Always
  selector:
    matchLabels:
      app: deploymentdemo
```

3、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210709095715.png)

```shell
[root@k8s-master01 controller]# ls
deploymentdemo.yml  replicasetdemo.yml
# 1、运行Deployment
[root@k8s-master01 controller]# kubectl apply -f deploymentdemo.yml 
deployment.apps/deploymentdemo created
# 2、查看deployment
[root@k8s-master01 controller]# kubectl get deploy
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
deploymentdemo   3/3     3            3           22s
# 3、查看rs控制器
[root@k8s-master01 controller]# kubectl get rs
NAME                       DESIRED   CURRENT   READY   AGE
deploymentdemo-cff9d5c4d   3         3         3       35s
# 4、查看pod
[root@k8s-master01 controller]# kubectl get pod
NAME                             READY   STATUS    RESTARTS   AGE
deploymentdemo-cff9d5c4d-csq4d   1/1     Running   0          42s
deploymentdemo-cff9d5c4d-kdl6w   1/1     Running   0          42s
deploymentdemo-cff9d5c4d-zjhn9   1/1     Running   0          42s
[root@k8s-master01 controller]# kubectl exec -it deploymentdemo-cff9d5c4d-csq4d sh
/ # nginx -v
nginx version: nginx/1.17.10
/ # exit
[root@k8s-master01 controller]# 
```

#### 13.4.3 镜像更新升级

1、命令行方式

```yml
# 1、升级nginx镜像版本为1.18.0
[root@k8s-master01 controller]# kubectl set image deployment deploymentdemo deploymentdemo=nginx:1.18.0-alpine
deployment.apps/deploymentdemo image updated
# 2、查看pod
[root@k8s-master01 controller]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
deploymentdemo-795cbd9bbd-d4vml   1/1     Running   0          2m2s
deploymentdemo-795cbd9bbd-nzs8w   1/1     Running   0          62s
deploymentdemo-795cbd9bbd-qlcvc   1/1     Running   0          94s
# 3、进去某一个pod内部，查看nginx升级版本信息
[root@k8s-master01 controller]# kubectl exec -it deploymentdemo-795cbd9bbd-d4vml sh
/ # nginx -v
nginx version: nginx/1.18.0
/ # exit
[root@k8s-master01 controller]# 
```

2、yml文件方式

```shell
[root@k8s-master01 controller]# ls
deploymentdemo.yml  replicasetdemo.yml
# 1、升级nginx镜像版本为1.19.2-alpine
[root@k8s-master01 controller]# kubectl edit deployments.apps deploymentdemo

# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "2"
    kubectl.kubernetes.io/last-applied-configuration: |
  creationTimestamp: "2021-07-09T02:04:24Z"
  ..........
    spec:
      containers:
      - image: nginx:1.19.2-alpine
        imagePullPolicy: IfNotPresent
deployment.apps/deploymentdemo edited
# 2、查看pod升级情况
[root@k8s-master01 controller]# kubectl get pod
NAME                              READY   STATUS        RESTARTS   AGE
deploymentdemo-56fb57bf59-7lxp9   1/1     Running       0          87s
deploymentdemo-56fb57bf59-9lcz7   1/1     Running       0          43s
deploymentdemo-56fb57bf59-cjzd2   1/1     Running       0          2s
deploymentdemo-795cbd9bbd-d4vml   0/1     Terminating   1          3h55m
deploymentdemo-795cbd9bbd-qlcvc   0/1     Terminating   1          3h54m

# 3、进去某一个pod内部，查看nginx升级版本信息
[root@k8s-master01 controller]# kubectl exec -it deploymentdemo-56fb57bf59-7lxp9 sh
/ # nginx -v
nginx version: nginx/1.19.2
/ # exit
[root@k8s-master01 controller]# 
```

#### 13.4.4 Deployment扩容

1、命令行方式

```shell
[root@k8s-master01 ~]# cd /home/data/controller/
[root@k8s-master01 controller]# ls
deploymentdemo.yml  replicasetdemo.yml
[root@k8s-master01 controller]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
deploymentdemo-56fb57bf59-7lxp9   1/1     Running   1          137m
deploymentdemo-56fb57bf59-9lcz7   1/1     Running   1          137m
deploymentdemo-56fb57bf59-cjzd2   1/1     Running   1          136m
[root@k8s-master01 controller]# kubectl scale deployment deploymentdemo --replicas=6
deployment.apps/deploymentdemo scaled
[root@k8s-master01 controller]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
deploymentdemo-56fb57bf59-576x6   1/1     Running   0          3s
deploymentdemo-56fb57bf59-7lxp9   1/1     Running   1          138m
deploymentdemo-56fb57bf59-9lcz7   1/1     Running   1          137m
deploymentdemo-56fb57bf59-cjzd2   1/1     Running   1          136m
deploymentdemo-56fb57bf59-ptbxq   1/1     Running   0          3s
deploymentdemo-56fb57bf59-xb2zh   1/1     Running   0          3s
[root@k8s-master01 controller]# 
```

2、yml文件方式

```shell
[root@k8s-master01 controller]# kubectl edit deployments.apps deploymentdemo

# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "3"
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"labels":{"app":"deploymentdemo"},"name":"deploymentdemo","namespace":"default"},"spec":{"replicas":3,"selector":{"matchLabels":{"app":"deploymentdemo"}},"template":{"metadata":{"labels":{"app":"deploymentdemo"},"name":"deploymentdemo"},"spec":{"containers":[{"image":"nginx:1.17.10-alpine","imagePullPolicy":"IfNotPresent","name":"deploymentdemo","ports":[{"containerPort":80}]}],"restartPolicy":"Always"}}}}
  creationTimestamp: "2021-07-09T02:04:24Z"
  generation: 4
  labels:
    app: deploymentdemo
  name: deploymentdemo
  namespace: default
  resourceVersion: "336158"
  selfLink: /apis/apps/v1/namespaces/default/deployments/deploymentdemo
  uid: 9d7ed144-738c-4e6f-a0e0-d1727a1e7c37
spec:
  progressDeadlineSeconds: 600
  replicas: 4
  revisionHistoryLimit: 10
  selector:
deployment.apps/deploymentdemo edited
[root@k8s-master01 controller]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
deploymentdemo-56fb57bf59-576x6   1/1     Running   0          4m13s
deploymentdemo-56fb57bf59-7lxp9   1/1     Running   1          142m
deploymentdemo-56fb57bf59-9lcz7   1/1     Running   1          141m
deploymentdemo-56fb57bf59-cjzd2   1/1     Running   1          141m
[root@k8s-master01 controller]# 
```

#### 13.4.5 滚动更新

1、基本概述

微服务部署种类：蓝绿部署、滚动部署、灰度发布、金丝雀发布。

- **蓝绿部署**: 是不停老版本，部署新版本然后进行测试，确认以后，将流量切到新版本，然后老版本同时也升级到新版本。 蓝绿部署无需停机，并且风险较小。
- **滚动发布**：一般是取出一个或者多个服务器停止服务，执行更新，并重新将其投入使用。周而复始，直到集群中所有的实例都更新成新版本。 这种部署方式相对于蓝绿部署，更加节约资源，它不需要运行两个集群、两倍的实例数。我们可以部分部署，例如每次只取出集群的20%进行升级。
- **灰度发布**: 是指在黑与白之间，能够平滑过渡的一种发布方式。AB test就是一种灰度发布方式，让一部分用户继续用A，一部分用户开始用B，如果用户对B没有什么反对意见，那么逐步扩大范围，把所有用户都迁移到B上面来。灰度发布可以保证整体系统的稳定，在初始灰度的时候就可以发现、调整问题，以保证其影响度，==平常所说的金丝雀部署也就是灰度发布的一种方式==。

2、金丝雀发布

Deployment控制器支持自定义控制更新过程中的滚动节奏，如`暂停(pause)`或`继续(resume)`更新操作。比如等待第一批新的Pod资源创建完成后立即暂停更新过程，此时，仅存在一部分新版本的应用，主体部分还是旧的版本。再筛选一小部分的用户请求路由到新版本的Pod应用，继续观察能否稳定地按期望的方式运行，确定没问题之后再继续完成余下的Pod资源滚动更新，否则立即回滚更新操作**这就是所谓的金丝雀发布（`Canary Release`）**

```shell
# 1、查看deployment
[root@k8s-master01 ~]# kubectl get deploy
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
deploymentdemo   4/4     4            4           10h
[root@k8s-master01 ~]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
deploymentdemo-56fb57bf59-576x6   1/1     Running   1          3h18m
deploymentdemo-56fb57bf59-7lxp9   1/1     Running   2          5h36m
deploymentdemo-56fb57bf59-9lcz7   1/1     Running   2          5h35m
deploymentdemo-56fb57bf59-cjzd2   1/1     Running   2          5h35m
[root@k8s-master01 ~]# kubectl exec -it deploymentdemo-56fb57bf59-576x6 sh
/ # nginx -v
nginx version: nginx/1.19.2
/ # exit
[root@k8s-master01 controller]# ls
deploymentdemo.yml  replicasetdemo.yml
# 2、更新deployment的nginx:1.18.0-alpine版本，并配置暂停deployment
[root@k8s-master01 controller]# kubectl set image deployment deploymentdemo deploymentdemo=nginx:1.18.0-alpine  && kubectl rollout pause deployment deploymentdemo
deployment.apps/deploymentdemo image updated
deployment.apps/deploymentdemo paused
[root@k8s-master01 controller]# kubectl get pod -w
NAME                              READY   STATUS    RESTARTS   AGE
deploymentdemo-56fb57bf59-576x6   1/1     Running   1          3h31m
deploymentdemo-56fb57bf59-9lcz7   1/1     Running   2          5h49m
deploymentdemo-56fb57bf59-cjzd2   1/1     Running   2          5h48m
deploymentdemo-795cbd9bbd-rxn9c   1/1     Running   0          40s
deploymentdemo-795cbd9bbd-xdlh5   1/1     Running   0          40s
^C
# 3、观察更新状态
[root@k8s-master01 controller]# kubectl rollout resume deployment deploymentdemo
deployment.apps/deploymentdemo resumed
# 4、监控更新的过程，可以看到已经新增了一个资源，但是并未删除一个旧的资源，就是因为使用了pause暂停命令
[root@k8s-master01 controller]# kubectl get pod -w
NAME                              READY   STATUS    RESTARTS   AGE
deploymentdemo-795cbd9bbd-fs75g   1/1     Running   0          21s
deploymentdemo-795cbd9bbd-rxn9c   1/1     Running   0          6m46s
deploymentdemo-795cbd9bbd-vwvn4   1/1     Running   0          21s
deploymentdemo-795cbd9bbd-xdlh5   1/1     Running   0          6m46s
^C[root@k8s-master01 controller]# 
[root@k8s-master01 controller]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
deploymentdemo-795cbd9bbd-fs75g   1/1     Running   0          43s
deploymentdemo-795cbd9bbd-rxn9c   1/1     Running   0          7m8s
deploymentdemo-795cbd9bbd-vwvn4   1/1     Running   0          43s
deploymentdemo-795cbd9bbd-xdlh5   1/1     Running   0          7m8s
# 5、进去某一个pod内部，查看nginx更新版本信息
[root@k8s-master01 controller]# kubectl exec -it deploymentdemo-795cbd9bbd-fs75g sh
/ # nginx -v
nginx version: nginx/1.18.0
/ # exit
[root@k8s-master01 controller]# 
```

#### 13.4.6 Deployment版本回退

1、默认情况下，kubernetes 会在系统中保存前两次的 Deployment 的 rollout 历史记录，以便可以随时回退【可以修改 `revision history limit `来更改保存的revision数】。

2、只要 Deployment 的 `rollout `被触发就会创建一个` revision`，当且仅当Deployment 的` Pod template`被更改，例如更新template 中的 label 和容器镜像时，就会创建出一个新的 revision。

3、其他的更新，比如扩容 Deployment 不会创建 `revision`。因此可以很方便的手动或者自动扩容。这意味着当回退到历史 revision 时，只有 Deployment 中的 `Pod template`部分才会回退。

4、rollout常见命令

| 常见命令 | 功能具体说明                 |
| -------- | ---------------------------- |
| history  | 查看rollout操作历史。        |
| pause    | 将提供的资源设定为暂停状态。 |
| restart  | 重启某资源。                 |
| resume   | 将某资源从暂停状态恢复正常。 |
| status   | 查看rollout操作状态。        |
| undo     | 回滚前一rollout。            |

```shell
# 1、history历史操作
[root@k8s-master01 controller]# kubectl rollout history deployment deploymentdemo 
deployment.apps/deploymentdemo 
REVISION  CHANGE-CAUSE
1         <none>
3         <none>
4         <none>
# 2、回滚版本信息
[root@k8s-master01 controller]# kubectl rollout undo deployment deploymentdemo
deployment.apps/deploymentdemo rolled back
# 3、查看pod回滚情况
[root@k8s-master01 controller]# kubectl get pod -w
NAME                              READY   STATUS        RESTARTS   AGE
deploymentdemo-56fb57bf59-729m2   1/1     Running       0          11s
deploymentdemo-56fb57bf59-fldk5   1/1     Running       0          12s
deploymentdemo-56fb57bf59-msl9r   1/1     Running       0          12s
deploymentdemo-56fb57bf59-wmrlw   1/1     Running       0          10s
deploymentdemo-795cbd9bbd-rxn9c   0/1     Terminating   0          43m
deploymentdemo-795cbd9bbd-rxn9c   0/1     Terminating   0          43m
deploymentdemo-795cbd9bbd-rxn9c   0/1     Terminating   0          43m
^C[root@k8s-master01 controller]# 
[root@k8s-master01 controller]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
deploymentdemo-56fb57bf59-729m2   1/1     Running   0          30s
deploymentdemo-56fb57bf59-fldk5   1/1     Running   0          31s
deploymentdemo-56fb57bf59-msl9r   1/1     Running   0          31s
deploymentdemo-56fb57bf59-wmrlw   1/1     Running   0          29s
# 4、进去某一个pod内部，查看nginx回滚版本信息
[root@k8s-master01 controller]# kubectl exec -it deploymentdemo-56fb57bf59-729m2 sh
/ # nginx -v
nginx version: nginx/1.19.2
/ # exit
[root@k8s-master01 controller]# 
```

#### 13.4.7 Deployment 更新策略

1、Deployment 可以保证在升级时只有一定数量的 Pod 是 down 的。默认的，它会确保至少有比期望的Pod数量少，一个是up状态(最多一个不可用）

2、Deployment 同时也可以确保只创建出超过期望数量的一定数量的 Pod。默认的，它会确保最多比期望的Pod数量多一个的Pod 是up的(最多1个 surge)。

```shell
[root@k8s-master01 controller]# kubectl describe deployments.apps deploymentdemo 
Name:                   deploymentdemo
Namespace:              default
CreationTimestamp:      Fri, 09 Jul 2021 10:04:24 +0800
Labels:                 app=deploymentdemo
Annotations:            deployment.kubernetes.io/revision: 5
                        kubectl.kubernetes.io/last-applied-configuration:
                          {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"labels":{"app":"deploymentdemo"},"name":"deploymentdemo","namesp...
Selector:               app=deploymentdemo
Replicas:               4 desired | 4 updated | 4 total | 4 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
## 1、Kuberentes 版本v1.17.5中，从1-1变成25%-25%
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=deploymentdemo
  Containers:
  ..........
  Normal  ScalingReplicaSet  48m   deployment-controller  Scaled up replica set deploymentdemo-56fb57bf59 to 4
  Normal  ScalingReplicaSet  48m   deployment-controller  Scaled down replica set deploymentdemo-795cbd9bbd to 0
[root@k8s-master01 controller]# 
```

#### 13.4.8 Deployment小结

Deployment为Pod和Replica Set【下一代Replication Controller】提供声明式更新，只需要在 Deployment 中描述想要的目标状态是什么。`Deployment controller `就会帮将 Pod 和ReplicaSet 的实际状态改变到目标状态。也可以通过定义一个全新的 Deployment 来创建 ReplicaSet或者删除已有的 Deployment 并创建一个新的来替换。

### 13.5 DaemonSet

#### 13.5.1 基本介绍

1、DaemonSet 确保全部Node 上运行一个 Pod 的副本，当有 Node 加入集群时，也会为它们新增一个 Pod 。当有 Node 从集群移除时，这些 Pod 也会被回收删除 DaemonSet 将会删除它创建的所有Pod。

2、在每一个node节点上只调度一个Pod，因此无需指定replicas的个数，比如在每个node上都运行一个日志采集程序，负责收集node节点本身和node节点之上的各个Pod所产生的日志。在每个node上都运行一个性能监控程序，采集该node的运行性能数据。

#### 13.5.2 部署DaemonSet

1、在`k8sdemo01`工程创建`daemonsetdemo.yml`文件

```yml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: daemonsetdemo
  labels:
    app: daemonsetdemo
spec:
  template:
    metadata:
      name: daemonsetdemo
      labels:
        app: daemonsetdemo
    spec:
      containers:
        - name: daemonsetdemo
          image: nginx:1.17.10-alpine
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 80
      restartPolicy: Always
  selector:
    matchLabels:
      app: daemonsetdemo
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210710105831.png)

```shell
[root@k8s-master01 controller]# ls
daemonsetdemo.yml  deploymentdemo.yml  replicasetdemo.yml
# 1、运行demonset
[root@k8s-master01 controller]# kubectl apply -f daemonsetdemo.yml 
daemonset.apps/daemonsetdemo created
[root@k8s-master01 controller]# kubectl get daemonset
NAME            DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonsetdemo   2         2         2       2            2           <none>          20s
[root@k8s-master01 controller]# kubectl get pod -o wide
NAME                  READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
daemonsetdemo-7pm5f   1/1     Running   0          40s   10.81.85.252   k8s-node01   <none>           <none>
daemonsetdemo-d2crz   1/1     Running   0          40s   10.81.58.238   k8s-node02   <none>           <none>
[root@k8s-master01 controller]# kubectl delete pod daemonsetdemo-7pm5f
pod "daemonsetdemo-7pm5f" deleted
# 2、查看pod详细信息：只有工作节点创建pod，master节点并不会创建。
[root@k8s-master01 controller]# kubectl get pod -o wide
NAME                  READY   STATUS    RESTARTS   AGE     IP             NODE         NOMINATED NODE   READINESS GATES
daemonsetdemo-4pgc9   1/1     Running   0          2m40s   10.81.85.253   k8s-node01   <none>           <none>
daemonsetdemo-d2crz   1/1     Running   0          4m20s   10.81.58.238   k8s-node02   <none>           <none>
[root@k8s-master01 controller]# 
```

#### 13.5.3 DaemonSet滚动更新

1、DaemonSet有两种更新策略类型

- `OnDelete`：这是向后兼容性的默认更新策略。使用`OnDelete`更新策略，在更新`DaemonSet`模板后，只有在手动删除旧的`DaemonSet pod`时才会创建新的`DaemonSet pod`。这与Kubernetes1.5或更早版本中`DaemonSet`的行为相同。
- RollingUpdate：使用`RollingUpdate`更新策略，在更新`DaemonSet`模板后，旧的`DaemonSet pod`将被终止，并且将以受控方式自动创建新的`DaemonSet pod`。

### 13.6 Job控制器

#### 13.6.1 基本介绍

1、使用基本镜像

```shell
docker pull perl:slim 
```

2、具体简介

- 一次性执行任务，类似Linux中的job。
- 应用场景：如离线数据处理，视频解码等业务。

#### 13.6.2 部署Job

1、在`k8sdemo01`工程创建`jobdemo.yml`文件

```yml
apiVersion: batch/v1
kind: Job
metadata:
  name: jobdemo
  labels:
    app: jobdemo
spec:
  template:
    metadata:
      name: jobdemo
      labels:
        app: jobdemo
    spec:
      containers:
        - name: jobdemo
          image: perl:slim
          imagePullPolicy: IfNotPresent
          command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(6000)"]
      restartPolicy: Never
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210710114728.png)

```shell
[root@k8s-master01 controller]# ls
daemonsetdemo.yml  deploymentdemo.yml  jobdemo.yml  replicasetdemo.yml
[root@k8s-master01 controller]# kubectl apply -f jobdemo.yml 
job.batch/jobdemo created
[root@k8s-master01 controller]# kubectl get pod -w
NAME            READY   STATUS              RESTARTS   AGE
jobdemo-cc5wr   0/1     ContainerCreating   0          29s
jobdemo-cc5wr   1/1     Running             0          32s
jobdemo-cc5wr   0/1     Completed           0          81s
^C[root@k8s-master01 controller]# 
[root@k8s-master01 controller]# kubectl delete -f jobdemo.yml 
job.batch "jobdemo" deleted
[root@k8s-master01 controller]# kubectl get pod
No resources found in default namespace.
[root@k8s-master01 controller]# 
```

#### 13.6.3 StatefulSet产生

1、在kubernetes系统中，Pod的管理对象`RC`，`Deployment`，`DaemonSet`，`Job`都面向无状态的服务，但现实中有很多服务时有状态的，集群有这四个特点：

- 每个节点都是有固定的身份ID，集群中的成员可以相互发现并通信。
- 集群的规模是比较固定的，集群规模不能随意变动。
- 集群中的每个节点都是有状态的，通常会持久化数据到永久存储中。
- 如果磁盘损坏，则集群里的某个节点无法正常运行，集群功能受损。

2、通过`RC`或`Deployment`控制Pod副本数量来实现上述有状态的集群，发现第一点是无法满足的，因为Pod名称和ip是随机产生的，并且各Pod中的共享存储中的数据不能都动，因此StatefulSet在这种情况下就派上用场了。StatefulSet具有以下特性：

- StatefulSet里的每个Pod都有稳定，唯一的网络标识，可以用来发现集群内的其它成员。假设，StatefulSet的名称为k8s，那么第1个Pod叫k8s-0，第2个叫k8s-1，以此类推！！
- StatefulSet控制的Pod副本的启停顺序是受控的，操作第N个Pod时，前N-1个Pod已经是运行且准备状态。
- StatefulSet里的Pod采用稳定的持久化存储卷，通过PV或PVC来实现，删除Pod时默认不会删除与StatefulSet相关的存储卷(为了保证数据的安全)。

3、结论

StatefulSet除了要与`PV卷`捆绑使用以存储Pod的状态数据，还要与`Headless`，`Service`配合使用，每个`StatefulSet`定义中都要生命它属于哪个`Handless Service`，`Handless Service`与普通`Service`的关键区别在于，它没有`Cluster IP`。

### 13.7 statefuleSet

#### 13.7.1 基本简介

1、statefuleSet产生前提

`deployment`来管理pod容器的副本数量，如果挂掉之后容器再次启动就可以了，但是如果要是启动的是mysql集群、zookeeper集群、etcd这种集群，里面都有id号，这种有关联的，如果一旦挂掉之后，在启动之后，集群id是否会变化呢？答案是肯定会变的。那有没有另外的一种控制器模式吗？这时候【statefulset】控制器横空出世

2、使用场景

部署的应用满足以下一个或多个部署需求，则建议使用StatefulSet。

- 稳定的、唯一的网络标识。稳定的、持久的存储。
- 有序的、优雅的部署和伸缩。有序的、优雅的删除和停止。
- 有序的、自动的滚动更新。

#### 13.7.2 两者区别

1、statefulset和deployment特点比较

| 特性                                  | Deployment                                                   | StatefulSet                                                  |
| ------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 是否暴露到外网                        | 可以                                                         | 一般不                                                       |
| 请求面向的对象                        | serviceName                                                  | 指定pod的域名                                                |
| 灵活性                                | 只能通过`service/serviceIp`访问到k8s自动转发的pod            | 可以访问任意一个自定义的pod                                  |
| 易用性                                | 只需要关心Service的信息即可                                  | 需要知道要访问的pod启动的名称、`headlessService`名称         |
| PV/PVC绑定关系的稳定性(多个replicas） | (pod挂掉后重启)无法保证初始的绑定关系                        | 可以保证                                                     |
| pod名称稳定性                         | 不稳定，因为是通过template创<br/>建，每次为了避免重复都会后缀<br/>一个随机数 | 稳定，每次都一样                                             |
| 启动顺序(多个replicas）               | 随机启动，如果pod宕掉重启，<br/>会自动分配一个node重新启动   | pod按`app-0、app-1...app-(n-1)`，如果pod宕掉重启，还会在之前的node上重新启动。 |
| 停止顺序(多个replicas）               | 随机停止                                                     | 倒序停止                                                     |
| 集群内部服务发现                      | 只能通过service访问到随机的pod                               | 可以打通pod之间的通信(主要是被发现）                         |
| 性能开销                              | 无需维护pod与node、pod与PVC 等关系                           | 比deployment类型需要维护额外的关系信息                       |

2、分类

K8s状态应用部署分为两步

- Headless Service: `Headless Service` 其实和service差不多，只不过定义的这个叫无头服务，它们之间唯一的区别就是将`Cluster ip` 设置为了none，不会帮你配置ip
- StatefulSet：需要在pod模板中定义servicename。

**Headless Service案例**

```yaml
apiVersion: v1
kind: Service
metadata:
name: my-service
spec:
clusterIP: None
selector:
 app: nginx
ports:
 - protocol: TCP
  port: 80
  targetPort: 9376
```

**部署Service**

怎么去访问？我们给它定义一个标识。创建完之后会有这个标识符，它会使用这个DNS来解析这个名称，来相互的访问，headless就不会通过ip去访问了，必须通过名称去访问。

```shell
kubectl create -f headless-svc.yamlkubectl get svc
```

**statefulSet案例**

```yaml
apiVersion: apps/v1beta1
kind: StatefulSet
metadata:
name: nginx-statefulset
namespace: default
spec:
serviceName: my-service
replicas: 3
selector:
 matchLabels:
  app: nginx
template:
 metadata:
  labels:
   app: nginx
 spec:
  containers:
  - name: nginx
   image: nginx:latest
   ports:
   - containerPort: 80
```

#### 13.7.3  statefulset小结

**1、Pod会被顺序部署和顺序终结**

- StatefulSet中的各个 Pod会被顺序地创建出来，每个Pod都有一个唯一的ID，在创建后续 Pod 之前，首先要等前面的 Pod 运行成功并进入到就绪状态。
- 删除会销毁StatefulSet 中的每个 Pod，并且按照创建顺序的反序来执行，只有在成功终结后面一个之后，才会继续下一个删除操作。

**2、Pod具有唯一网络名称**

- Pod具有唯一的名称，而且在重启后会保持不变。通过Headless服务，基于主机名，每个 Pod 都有独立的网络地址，这个网域由一个Headless 服务所控制。
- 这样每个Pod会保持稳定的唯一的域名，使得集群就不会将重新创建出的Pod作为新成员。

**3、Pod能有稳定的持久存储**

- StatefulSet中的每个Pod可以有其自己独立的`PersistentVolumeClaim`对象。
- 即使Pod被重新调度到其它节点上以后，原有的持久磁盘也会被挂载到该Pod，Pod能被通过Headless服务访问到。
- 客户端可以通过服务的域名连接到任意Pod。

## 14 service网络

### 14.1 什么是service?

#### 14.1.1 service简介

1、存在问题

通过Deployment来创建一组Pod来提供具有高可用性的服务。虽然每个Pod都会分配一个单独的Pod IP，然而却存在如下两问题。

- Pod IP仅仅是集群内可见的虚拟IP，外部无法访问。
- Pod IP会随着Pod的销毁而消失，当Deployment对Pod进行动态伸缩时，Pod IP可能随时随地都会变化，这样对于访问这个服务带来了难度。

2、解决方案

Service能够提供负载均衡的能力，但是在使用上有以下限制。只提供 4 层负载均衡能力，而没有7 层功能，但有时可能需要更多的匹配规则来转发请求，这点上 4 层负载均衡是不支持的，因此，Kubernetes中的Service对象就是解决以上问题的实现服务发现核心关键。

#### 14.1.2 Service类型

1、**ClusterIp**

- 默认类型，自动分配一个仅 Cluster 内部可以访问的虚拟 IP。

2、**NodePort**

- 在 ClusterIP 基础上为 Service 在每台机器上绑定一个端口，这样就可以通过 :NodePort 来访问该服务。

3、**LoadBalancer**

- 在 NodePort 的基础上，借助 cloud provider 创建一个外部负载均衡器，并将请求转发到NodePort。是付费服务，而且价格不菲。

4、**ExternalName**

- 把集群外部的服务引入到集群内部来，在集群内部直接使用。没有任何类型代理被创建，这只有 kubernetes 1.7 或更高版本的 kube-dns 才支持。

### 14.2 Service 类型详解

#### 14.2.1 Services和Pods简介

1、基本介绍

- Kubernetes的Pods是有生命周期的，它们可以被创建，而且销毁不会再启动。如果使用Deployment来运行应用程序，则它可以动态创建和销毁Pod。
- 一个Kubernetes的Service是一种抽象，它定义了一组Pods的逻辑集合和一个用于访问它们的策略有的时候被称之为微服务。
- 一个Service的目标Pod集合通常是由Label Selector 来决定的。

#### 14.2.2 代理模式

kube-proxy支持三种代理模式: 用户空间，iptables和IPVS，它们各自的操作略有不同。

**1、Userspace代理模式**

- Client Pod要访问Server Pod时,它先将请求发给本机内核空间中的service规则，由它再将请求,转给监听在指定套接字上的kube-proxy，kube-proxy处理完请求，并分发请求到指定Server Pod后,再将请求递交给内核空间中的service,由service将请求转给指定的Server Pod。由于其需要来回在用户空间和内核空间交互通信，因此效率很差 。
- 当一个客户端连接到一个 VIP，iptables 规则开始起作用，它会重定向该数据包到 Service代理 的端口。Service代理 选择一个 backend，并将客户端的流量代理到 backend 上。
- 这意味着 Service 的所有者能够选择任何他们想使用的端口，而不存在冲突的风险。客户端可以简单地连接到一个 IP 和端口，而不需要知道实际访问了哪些 Pod。

**2、iptables代理模式**

当一个客户端连接到一个 VIP，iptables 规则开始起作用。一个 backend 会被选择，数据包被重定向到这个 backend。不像 userspace 代理，数据包从来不拷贝到用户空间，kube-proxy 不是必须为该 VIP 工作而运行，并且客户端 IP 是不可更改的。当流量打到 Node 的端口上，或通过负载均衡器，会执行相同的基本流程，但是在那些案例中客户端 IP 是可以更改的。

**3、IPVS代理模式**

- 在大规模集群中，iptables 操作会显着降低速度。IPVS 专为负载平衡而设计，并基于内核内哈希表。可以通过基于 IPVS 的 kube-proxy 在大量服务中实现性能一致性。基于 IPVS 的 kube-proxy 具有更复杂的负载平衡算法(最小连接，局部性，加权，持久性）。

- 在 Kubernetes 集群中，每个 Node 运行一个 kube-proxy 进程，kube-proxy 负责为 Service 实现了一种VIP(虚拟 IP)的形式，而不是 `ExternalName` 的形式。 在 Kubernetes v1.0 版本，代理完全在`userspace`，在Kubernetes v1.1 版本，新增了 iptables 代理，但并不是默认的运行模式，从 Kubernetes v1.2 起，默认就是`iptables` 代理。 在 Kubernetes v1.8.0中，添加了 ipvs 代理，在 Kubernetes 1.14 版本开始默认使用 ipvs 代理。在 Kubernetes v1.0 版本， 默认Service 是`4层`(TCP/UDP over IP）服务，在Kubernetes v1.1 版本，新增了Ingress API，用来表示`7层HTTP`服务 。
- kube-proxy 会监视 Kubernetes Service 对象和 Endpoints ，调用 netlink 接口以相应地创建，ipvs 规则并定期与 Kubernetes Service 对象和 Endpoints 对象同步 ipvs 规则，以确保 ipvs 状态与期望一致。访问服务时，流量将被重定向到其中一个后端 Pod与 iptables 类似，ipvs 于 netfilter 的 hook 功能，但使用哈希表作为底层数据结构并在内核空间中工作。这意味着 ipvs 可以更快地重定向流量，并且在同步代理规则时具有更好的性能，ipvs 为负载均衡算法提供了更多选项。

#### 14.2.3 ClusterIP

1、ClusterIP简介

- 类型为ClusterIP的service，这个service有一个Cluster-IP，其实就一个VIP。具体实现原理依靠kubeproxy组件，通过iptables或是ipvs实现。
- clusterIP 主要在每个 node 节点使用 iptables，将发向 clusterIP 对应端口的数据，转发到 kube-proxy中。kube-proxy 自己内部实现有负载均衡的方法，并可以查询到这个 service 下对应 pod 的地址和端口，进而把数据转发给对应的 pod 的地址和端口。
- 注意，这种类型的service 只能在集群内访问。

2、环境所需的基本镜像

```shell
docker pull tomcat:9.0.20-jre8-alpine 
```

3、部署service

在`k8sdemo01`工程创建`nodeportdemo.yml`文件

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: clusteripdemo
  labels:
    app: clusteripdemo
spec:
  replicas: 1
  template:
    metadata:
      name: clusteripdemo
      labels:
        app: clusteripdemo
    spec:
      containers:
        - name: clusteripdemo
          image: tomcat:9.0.20-jre8-alpine
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 8080
      restartPolicy: Always
  selector:
    matchLabels:
      app: clusteripdemo
---
apiVersion: v1
kind: Service
metadata:
  name: clusterip-svc
spec:
  selector:
    app: clusteripdemo
  ports:
    - port: 8080
  type: ClusterIP
```

4、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210710190517.png)

```shell
[root@k8s-master01 service]# ls
clusteripdemo.yml
# 1、运行服务
[root@k8s-master01 service]# kubectl apply -f clusteripdemo.yml 
deployment.apps/clusteripdemo created
service/clusterip-svc created
# 2、获取pod
[root@k8s-master01 service]# kubectl get pod
NAME                             READY   STATUS    RESTARTS   AGE
clusteripdemo-657fcf787c-4rz4l   1/1     Running   0          11s
# 3、获取deploy控制器
[root@k8s-master01 service]# kubectl get deploy
NAME            READY   UP-TO-DATE   AVAILABLE   AGE
clusteripdemo   1/1     1            1           29s
# 4、查看服务
[root@k8s-master01 service]# kubectl get svc
NAME            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
clusterip-svc   ClusterIP   10.1.190.208   <none>        8080/TCP   36s
kubernetes      ClusterIP   10.1.0.1       <none>        443/TCP    6d4h
[root@k8s-master01 service]# curl 10.1.190.208:8080

<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>Apache Tomcat/9.0.20</title>
        <link href="favicon.ico" rel="icon" type="image/x-icon" />
        <link href="favicon.ico" rel="shortcut icon" type="image/x-icon" />
        <link href="tomcat.css" rel="stylesheet" type="text/css" />
    </head>

    <body>
        <div id="wrapper">
            <p class="copyright">Copyright &copy;1999-2021 Apache Software Foundation.  All Rights Reserved</p>
        </div>
    </body>
</html>
# 5、删除服务
[root@k8s-master01 service]# kubectl delete -f clusteripdemo.yml 
deployment.apps "clusteripdemo" deleted
service "clusterip-svc" deleted
[root@k8s-master01 service]# 
```

#### 14.2.4 NodePort

1、NodePort简介

开发的场景不全是集群内访问，也需要集群外业务访问。那么ClusterIP就满足不了了，NodePort是其中的一种实现方案。nodePort 的原理在于在 node 上开了一个端口，将向该端口的流量导入到`kube-proxy`，然后由`kube-proxy` 进一步到给对应的 pod 。

2、环境所需的镜像

```shell
docker pull tomcat:9.0.20-jre8-alpine 
```

3、部署service

在`k8sdemo01`工程创建`nodeportdemo.yml`文件

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nodeportdemo
  labels:
    app: nodeportdemo
spec:
  replicas: 1
  template:
    metadata:
      name: nodeportdemo
      labels:
        app: nodeportdemo
    spec:
      containers:
        - name: nodeportdemo
          image: tomcat:9.0.20-jre8-alpine
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 8080
      restartPolicy: Always
  selector:
    matchLabels:
      app: nodeportdemo
---
apiVersion: v1
kind: Service
metadata:
  name: nodeporttomcat-svc
spec:
  selector:
    app: nodeportdemo
  ports:
    - port: 8080
      targetPort: 8080
      nodePort: 30088
  type: NodePort
```

4、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210710195840.png)

```shell
[root@k8s-master01 service]# ls
clusteripdemo.yml  nodeportdemo.yml
# 1、运行服务
[root@k8s-master01 service]# kubectl apply -f nodeportdemo.yml 
deployment.apps/nodeportdemo created
service/nodeporttomcat-svc created
[root@k8s-master01 service]# kubectl get pod
NAME                           READY   STATUS    RESTARTS   AGE
nodeportdemo-9cbf46469-gnbwk   1/1     Running   0          20s
[root@k8s-master01 service]# kubectl get deploy
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
nodeportdemo   1/1     1            1           8m7s
# 2、查看服务
[root@k8s-master01 service]# kubectl get svc
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)          AGE
kubernetes           ClusterIP   10.1.0.1     <none>        443/TCP          6d6h
nodeporttomcat-svc   NodePort    10.1.88.2    <none>        8080:30088/TCP   8m23s
[root@k8s-master01 service]# 
```

5、浏览器访问服务

```shell
http://8.134.125.62:30088/
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210710210301.png)

6、删除服务

```shell
[root@k8s-master01 service]# ls
clusteripdemo.yml  nodeportdemo.yml
[root@k8s-master01 service]# kubectl delete -f nodeportdemo.yml 
deployment.apps "nodeportdemo" deleted
service "nodeporttomcat-svc" deleted
[root@k8s-master01 service]# kubectl get svc
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.1.0.1     <none>        443/TCP   6d6h
[root@k8s-master01 service]# 
```

### 14.3 ingress网络

#### 14.3.1 什么是Ingress?

1、`ingress`由`ingress controller`和`ingress服务`两部分组成，其中`ingress controller`目前主要有两种基于nginx服务的`ingress controller`和基于`traefik的ingress controller`，其中traefik的`ingress controller`，支持http和https协议。

2、在kubernetes集群中，知道service和pod的ip仅在集群内部访问。如果外部应用要访问集群内的服务，集群外部的请求需要通过负载均衡转发到service在Node上暴露的`NodePort`上，然后再由`kube-proxy`组件将其转发给相关的pod。

3、`Ingress`就是为进入集群的请求提供路由规则的集合，通俗点就是提供外部访问集群的入口，将外部的HTTP或者HTTPS请求转发到集群内部service上。

#### 14.3.2 Ingress-nginx组成

本次实验中使用的就是nginx，Ingress-nginx一般由三个组件组成：

- 反向代理负载均衡器：通常以service的port方式运行，接收并按照ingress定义的规则进行转发，常用的有nginx，Haproxy，Traefik等。
- Ingress Controller：监听APIServer，根据用户编写的ingress规则(编写ingress的yaml文件），动态地去更改nginx服务的配置文件，并且reload重载使其生效，此过程是自动化的（通过lua脚本来实现）。
- Ingress：将nginx的配置抽象成一个Ingress对象，当用户每添加一个新的服务，只需要编写一个新的ingress的yaml文件即可。

#### 14.3.3 Ingress-nginx工作原理

1、`ingress controller`通过和`kubernetes api`交互，动态的去感知集群中`ingress`规则变化。然后读取它按照自定义的规则，规则就是写明了那个域名对应哪个service，生成一段nginx配置。

2、再写到`nginx-ingress-controller`的pod里，这个`Ingress controller`的pod里运行着一个Nginx服务，控制器会把生成的nginx配置写入`/etc/nginx.conf`文件中，然后reload一下使配置生效，以此达到分配和动态更新问题。

#### 14.3.4 下载资源文件

1、下载ingrees-controller

[https://github.com/kubernetes/ingress-nginx/blob/nginx-0.30.0/deploy/static/mandatory.yaml](https://github.com/kubernetes/ingress-nginx/blob/nginx-0.30.0/deploy/static/mandatory.yaml)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711085738.png)

**mandatory.yaml**

```yml
apiVersion: v1
kind: Namespace
metadata:
  name: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx

---

kind: ConfigMap
apiVersion: v1
metadata:
  name: nginx-configuration
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx

---
kind: ConfigMap
apiVersion: v1
metadata:
  name: tcp-services
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx

---
kind: ConfigMap
apiVersion: v1
metadata:
  name: udp-services
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx

---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: nginx-ingress-serviceaccount
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx

---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  name: nginx-ingress-clusterrole
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
rules:
  - apiGroups:
      - ""
    resources:
      - configmaps
      - endpoints
      - nodes
      - pods
      - secrets
    verbs:
      - list
      - watch
  - apiGroups:
      - ""
    resources:
      - nodes
    verbs:
      - get
  - apiGroups:
      - ""
    resources:
      - services
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - ""
    resources:
      - events
    verbs:
      - create
      - patch
  - apiGroups:
      - "extensions"
      - "networking.k8s.io"
    resources:
      - ingresses
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - "extensions"
      - "networking.k8s.io"
    resources:
      - ingresses/status
    verbs:
      - update

---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: Role
metadata:
  name: nginx-ingress-role
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
rules:
  - apiGroups:
      - ""
    resources:
      - configmaps
      - pods
      - secrets
      - namespaces
    verbs:
      - get
  - apiGroups:
      - ""
    resources:
      - configmaps
    resourceNames:
      # Defaults to "<election-id>-<ingress-class>"
      # Here: "<ingress-controller-leader>-<nginx>"
      # This has to be adapted if you change either parameter
      # when launching the nginx-ingress-controller.
      - "ingress-controller-leader-nginx"
    verbs:
      - get
      - update
  - apiGroups:
      - ""
    resources:
      - configmaps
    verbs:
      - create
  - apiGroups:
      - ""
    resources:
      - endpoints
    verbs:
      - get

---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: RoleBinding
metadata:
  name: nginx-ingress-role-nisa-binding
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: nginx-ingress-role
subjects:
  - kind: ServiceAccount
    name: nginx-ingress-serviceaccount
    namespace: ingress-nginx

---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: nginx-ingress-clusterrole-nisa-binding
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: nginx-ingress-clusterrole
subjects:
  - kind: ServiceAccount
    name: nginx-ingress-serviceaccount
    namespace: ingress-nginx

---

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-ingress-controller
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app.kubernetes.io/name: ingress-nginx
      app.kubernetes.io/part-of: ingress-nginx
  template:
    metadata:
      labels:
        app.kubernetes.io/name: ingress-nginx
        app.kubernetes.io/part-of: ingress-nginx
      annotations:
        prometheus.io/port: "10254"
        prometheus.io/scrape: "true"
    spec:
      # wait up to five minutes for the drain of connections
      terminationGracePeriodSeconds: 300
      serviceAccountName: nginx-ingress-serviceaccount
      nodeSelector:
        kubernetes.io/os: linux
      containers:
        - name: nginx-ingress-controller
          image: registry.cn-hangzhou.aliyuncs.com/google_containers/nginx-ingress-controller:0.30.0
          args:
            - /nginx-ingress-controller
            - --configmap=$(POD_NAMESPACE)/nginx-configuration
            - --tcp-services-configmap=$(POD_NAMESPACE)/tcp-services
            - --udp-services-configmap=$(POD_NAMESPACE)/udp-services
            - --publish-service=$(POD_NAMESPACE)/ingress-nginx
            - --annotations-prefix=nginx.ingress.kubernetes.io
          securityContext:
            allowPrivilegeEscalation: true
            capabilities:
              drop:
                - ALL
              add:
                - NET_BIND_SERVICE
            # www-data -> 101
            runAsUser: 101
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: POD_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
          ports:
            - name: http
              containerPort: 80
              protocol: TCP
            - name: https
              containerPort: 443
              protocol: TCP
          livenessProbe:
            failureThreshold: 3
            httpGet:
              path: /healthz
              port: 10254
              scheme: HTTP
            initialDelaySeconds: 10
            periodSeconds: 10
            successThreshold: 1
            timeoutSeconds: 10
          readinessProbe:
            failureThreshold: 3
            httpGet:
              path: /healthz
              port: 10254
              scheme: HTTP
            periodSeconds: 10
            successThreshold: 1
            timeoutSeconds: 10
          lifecycle:
            preStop:
              exec:
                command:
                  - /wait-shutdown

---

apiVersion: v1
kind: LimitRange
metadata:
  name: ingress-nginx
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
spec:
  limits:
    - min:
        memory: 90Mi
        cpu: 100m
      type: Container
```

2、下载ingress服务

下载地址: [https://github.com/kubernetes/ingress-nginx/blob/nginx-0.30.0/deploy/static/provider/baremetal/service-nodeport.yaml](https://github.com/kubernetes/ingress-nginx/blob/nginx-0.30.0/deploy/static/provider/baremetal/service-nodeport.yaml)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711090344.png)

**nodeport.yaml**

```yml
apiVersion: v1
kind: Service
metadata:
  name: ingress-nginx
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
spec:
  type: NodePort
  ports:
    - name: http
      port: 80
      targetPort: 80
      protocol: TCP
    - name: https
      port: 443
      targetPort: 443
      protocol: TCP
  selector:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx

---
```

3、下载相关镜像

```shell
[root@k8s-master01 ingress]# docker images
REPOSITORY                           TAG                  IMAGE ID       CREATED         SIZE
calico/node                          v3.14.2              780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol            v3.14.2              9dfa8f25b51c   11 months ago   22.8MB
calico/cni                           v3.14.2              e6189009f081   11 months ago   119MB
calico/kube-controllers              v3.14.2              4815e4106d26   11 months ago   52.8MB
k8s.gcr.io/kube-proxy                v1.17.5              e13db435247d   15 months ago   116MB
k8s.gcr.io/kube-apiserver            v1.17.5              f640481f6db3   15 months ago   171MB
k8s.gcr.io/kube-controller-manager   v1.17.5              fe3d691efbf3   15 months ago   161MB
k8s.gcr.io/kube-scheduler            v1.17.5              f648efaff966   15 months ago   94.4MB
k8s.gcr.io/coredns                   1.6.5                70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                      3.4.3-0              303ce5db0e90   20 months ago   288MB
tomcat                               9.0.20-jre8-alpine   387f9d021d3a   2 years ago     108MB
k8s.gcr.io/pause                     3.1                  da86e6ba6ca1   3 years ago     742kB
# 1、nginx-ingress-controller镜像
[root@k8s-master01 ingress]# docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/nginx-ingress-controller:0.30.0
0.30.0: Pulling from google_containers/nginx-ingress-controller
c9b1b535fdd9: Pull complete 
45ba4c948320: Pull complete 
70c24c20a569: Pull complete 
58acda238271: Pull complete 
7873cb07ba91: Pull complete 
3572b831a7ad: Pull complete 
2e4b94d88c7a: Pull complete 
73d054fe6162: Pull complete 
72107c0475b3: Pull complete 
0920fa00bdaf: Pull complete 
bbc4231b0eed: Pull complete 
1a0d8e7b84e8: Pull complete 
Digest: sha256:b312c91d0de688a21075078982b5e3a48b13b46eda4df743317d3059fc3ca0d9
Status: Downloaded newer image for registry.cn-hangzhou.aliyuncs.com/google_containers/nginx-ingress-controller:0.30.0
registry.cn-hangzhou.aliyuncs.com/google_containers/nginx-ingress-controller:0.30.0
# 2、替换操作
[root@k8s-master01 ingress]# docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/nginx-ingress-controller:0.30.0 quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.30.0

# 3、删除操作
[root@k8s-master01 ingress]# docker rmi -f registry.cn-hangzhou.aliyuncs.com/google_containers/nginx-ingress-controller:0.30.0
Untagged: registry.cn-hangzhou.aliyuncs.com/google_containers/nginx-ingress-controller:0.30.0
Untagged: registry.cn-hangzhou.aliyuncs.com/google_containers/nginx-ingress-controller@sha256:b312c91d0de688a21075078982b5e3a48b13b46eda4df743317d3059fc3ca0d9
[root@k8s-master01 ingress]# docker images
REPOSITORY                                                       TAG                  IMAGE ID       CREATED         SIZE
calico/node                                                      v3.14.2              780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol                                        v3.14.2              9dfa8f25b51c   11 months ago   22.8MB
calico/cni                                                       v3.14.2              e6189009f081   11 months ago   119MB
calico/kube-controllers                                          v3.14.2              4815e4106d26   11 months ago   52.8MB
k8s.gcr.io/kube-proxy                                            v1.17.5              e13db435247d   15 months ago   116MB
k8s.gcr.io/kube-apiserver                                        v1.17.5              f640481f6db3   15 months ago   171MB
k8s.gcr.io/kube-controller-manager                               v1.17.5              fe3d691efbf3   15 months ago   161MB
k8s.gcr.io/kube-scheduler                                        v1.17.5              f648efaff966   15 months ago   94.4MB
quay.io/kubernetes-ingress-controller/nginx-ingress-controller   0.30.0               89ccad40ce8e   16 months ago   323MB
k8s.gcr.io/coredns                                               1.6.5                70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                                                  3.4.3-0              303ce5db0e90   20 months ago   288MB
tomcat                                                           9.0.20-jre8-alpine   387f9d021d3a   2 years ago     108MB
k8s.gcr.io/pause                                                 3.1                  da86e6ba6ca1   3 years ago     742kB
[root@k8s-master01 ingress]# 
```

#### 14.3.5 两者对比

1、**ingress**

- 指的是k8s中的一个api对象，一般用yaml配置。作用是定义请求如何转发到service的规则，可以理解为配置模板。
- ingress是一个API对象，和其他对象一样，通过yaml文件来配置。ingress通过http或https暴露集群内部service，给service提供外部URL、负载均衡、SSL/TLS能力以及基于host的方向代理。ingress要依靠ingress-controller来具体实现以上功能。

2、**ingress-controller**

- 具体实现反向代理及负载均衡的程序，对ingress定义的规则进行解析，根据配置的规则来实现请求转发。
- `ingress-controller`并不是k8s自带的组件，实际上`ingress-controller`只是一个统称，用户可以选择不同的ingress-controller实现，目前，由k8s维护的`ingress-controller`只有google云的`GCE`与`ingress-nginx`两个。
- 但是不管哪一种`ingress-controller`，实现的机制都大同小异，只是在具体配置上有差异。一般来说，`ingress-controller`的形式都是一个pod，里面跑着`daemon`程序和反向代理程序。`daemon`负责不断监控集群的变化，根据ingress对象生成配置并应用新配置到反向代理，比如`nginx-ingress`就是动态生成nginx配置，动态更新`upstream`并在需要的时候reload程序应用新配置。

3、小结

简单来说`ingress-controller`是负责具体转发的组件，通过各种方式将它暴露在集群入口，外部对集群的请求流量会先到`ingress-controller`而ingress对象是用来告诉`ingress-controller`该如何转发请求，比如哪些域名哪些path要转发到哪些服务。

## 15 ingress案例实现

### 15.1 网络实验1

#### 15.1.1 运行ingress-controller

1、在`k8sdemo01`工程创建`mandatory.yaml`文件，在`mandatory.yaml`文件的Deployment资源中增加属性`sepc.template.sepc.hostNetWork`。

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711104753.png" style="zoom:80%;" />

`hostNetwork`网络是一种直接定义Pod网络的方式，如果在Pod中使用`hostNetwork:true`配置网络，那么Pod中运行的应用程序可以直接使用node节点的端口。

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711111001.png)

#### 15.1.2 运行ingress服务

1、在`k8sdemo01`工程创建`service-nodeport.yml`文件

```yml
apiVersion: v1
kind: Service
metadata:
  name: ingress-nginx
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
spec:
  type: NodePort
  ports:
    - name: http
      port: 80
      targetPort: 80
      protocol: TCP
    - name: https
      port: 443
      targetPort: 443
      protocol: TCP
  selector:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
---
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711111932.png)

#### 15.1.3 部署tomcat服务

1、在`k8sdemo01`工程创建`tomcat-service.yml`文件

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tomcat-deployment
  labels:
    app: tomcat-deployment
spec:
  replicas: 1
  template:
    metadata:
      name: tomcat-deployment
      labels:
        app: tomcat-deployment
    spec:
      containers:
        - name: tomcat-deployment
          image: tomcat:9.0.20-jre8-alpine
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 8080
      restartPolicy: Always
  selector:
    matchLabels:
      app: tomcat-deployment
---
apiVersion: v1
kind: Service
metadata:
  name: tomcat-svc
spec:
  selector:
    app: tomcat-deployment
  ports:
    - port: 8080
      targetPort: 8080
      nodePort: 30088
  type: NodePort
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711113109.png)

#### 15.1.4 部署ingress规则文件

1、在`k8sdemo01`工程创建`ingress-tomcat.yml`文件

```shell
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: nginx-ingress-test
spec:
  backend:
    serviceName: tomcat-svc
    servicePort: 8080  #是pod容器的端口
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711114323.png)

#### 15.1.5 集体测试

```shell
[root@k8s-master01 ingress]# ls
ingress-tomcat.yml  mandatory.yml  service-nodeport.yml  tomcat-service.yml

# 1、运行所有的yml文件
[root@k8s-master01 ingress]# kubectl apply -f .
ingress.extensions/nginx-ingress-test created
namespace/ingress-nginx created
configmap/nginx-configuration created
configmap/tcp-services created
configmap/udp-services created
serviceaccount/nginx-ingress-serviceaccount created
clusterrole.rbac.authorization.k8s.io/nginx-ingress-clusterrole created
role.rbac.authorization.k8s.io/nginx-ingress-role created
rolebinding.rbac.authorization.k8s.io/nginx-ingress-role-nisa-binding created
clusterrolebinding.rbac.authorization.k8s.io/nginx-ingress-clusterrole-nisa-binding created
deployment.apps/nginx-ingress-controller created
limitrange/ingress-nginx created
service/ingress-nginx created
deployment.apps/tomcat-deployment created
service/tomcat-svc created

# 2、查看所有命名空间的pod
[root@k8s-master01 ingress]# kubectl get pods -A
NAMESPACE       NAME                                        READY   STATUS        RESTARTS   AGE
default         tomcat-deployment-5ff64fdb6f-sgbzf          1/1     Terminating   0          139m
default         tomcat-deployment-5ff64fdb6f-xt8qt          1/1     Running       0          29s
ingress-nginx   nginx-ingress-controller-6ffc8fdf96-kpkwv   1/1     Running       0          29s
kube-system     calico-kube-controllers-6b94766748-pn4l8    1/1     Running       24         6d23h
kube-system     calico-node-4m62k                           1/1     Running       23         6d23h
kube-system     calico-node-7bnqj                           1/1     Running       24         6d23h
kube-system     calico-node-krh64                           1/1     Running       26         6d23h
kube-system     calico-node-zwvv9                           1/1     Running       8          6d23h
kube-system     coredns-6955765f44-nwzg6                    1/1     Running       24         7d
kube-system     coredns-6955765f44-rdwnc                    1/1     Running       24         7d
kube-system     etcd-k8s-master01                           1/1     Running       25         7d
kube-system     kube-apiserver-k8s-master01                 1/1     Running       32         7d
kube-system     kube-controller-manager-k8s-master01        1/1     Running       25         7d
kube-system     kube-proxy-4vdxm                            1/1     Running       26         7d
kube-system     kube-proxy-5nlqn                            1/1     Running       24         7d
kube-system     kube-proxy-npzs2                            1/1     Running       25         7d
kube-system     kube-proxy-z47rt                            1/1     Running       9          7d
kube-system     kube-scheduler-k8s-master01                 1/1     Running       25         7d

# 3、查看ingress-controller运行在那个node节点
[root@k8s-master01 ingress]# kubectl get pod -n ingress-nginx 
NAME                                        READY   STATUS    RESTARTS   AGE
nginx-ingress-controller-6ffc8fdf96-kpkwv   1/1     Running   0          43s

# 4、查看ingress-controller运行在那个node节点的详细信息
[root@k8s-master01 ingress]# kubectl get pod -n ingress-nginx -o wide
NAME                                        READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
nginx-ingress-controller-6ffc8fdf96-kpkwv   1/1     Running   0          54s   172.21.252.4   k8s-node01   <none>           <none>
# 5、查看ingress服务:查看service的部署端口号
[root@k8s-master01 ingress]# kubectl get svc -n ingress-nginx
NAME            TYPE       CLUSTER-IP    EXTERNAL-IP   PORT(S)                      AGE
ingress-nginx   NodePort   10.1.243.69   <none>        80:31276/TCP,443:32220/TCP   64s
[root@k8s-master01 ingress]# 
```

通过ingress访问tomcat

```shell
http://8.134.130.129:31276/
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711160745.png" style="zoom: 80%;" />

### 15.2 网络实验2

网络实验1部署方式只能通过`ingress-controller`部署的节点访问，集群内其他节点无法访问`ingress`规则。通过修改`mandatory.yml`文件的控制类类型，让集群内每一个节点都可以正常访问`ingress`规则。

#### 15.2.1 运行ingress-controller

1、在`k8sdemo01`工程创建`mandatory.yaml`文件

```yml
将Deployment类型控制器修改为：DaemonSet
删除replicas: 1 这一行
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711162511.png" style="zoom:80%;" />

#### 15.2.2 运行ingress服务

1、在`k8sdemo01`工程创建`service-nodeport.yml`文件

```yml
apiVersion: v1
kind: Service
metadata:
  name: ingress-nginx
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
spec:
  type: NodePort
  ports:
    - name: http
      port: 80
      targetPort: 80
      nodePort: 31188
      protocol: TCP
    - name: https
      port: 443
      targetPort: 443
      nodePort: 30443
      protocol: TCP
  selector:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
```

#### 15.2.3 部署ingress规则文件

1、在`k8sdemo01`工程创建`ingress-tomcat.yml`文件

```yml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: nginx-ingress-test
spec:
  rules:
    - host: ingress-tomcat.guardwhy.com
      http:
        paths:
          - path: /
            backend:
              serviceName: tomcat-svc
              servicePort: 8080  #是pod容器的端口
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711165103.png)

#### 15.2.4 修改宿主机hosts

1、进入Windows的C盘目录，修改`C:\Windows\System32\drivers\etc\hosts`文件

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711171913.png)

2、配置域名

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711205255.png" style="zoom:80%;" />

#### 15.2.5 部署服务

1、集体部署服务

```shell
[root@k8s-master01 ingress]# ls
ingress-tomcat.yml  mandatory.yml  service-nodeport.yml  tomcat-service.yml
[root@k8s-master01 ingress]# kubectl apply -f .
ingress.extensions/nginx-ingress-test created
namespace/ingress-nginx created
configmap/nginx-configuration created
configmap/tcp-services created
configmap/udp-services created
serviceaccount/nginx-ingress-serviceaccount created
clusterrole.rbac.authorization.k8s.io/nginx-ingress-clusterrole created
role.rbac.authorization.k8s.io/nginx-ingress-role created
rolebinding.rbac.authorization.k8s.io/nginx-ingress-role-nisa-binding created
clusterrolebinding.rbac.authorization.k8s.io/nginx-ingress-clusterrole-nisa-binding created
daemonset.apps/nginx-ingress-controller created
limitrange/ingress-nginx created
service/ingress-nginx created
deployment.apps/tomcat-deployment created
service/tomcat-svc created
[root@k8s-master01 ingress]# 
```

2、浏览器测试

```shell
http://ingress-tomcat.guardwhy.com:31188/
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210711210701.png)

## 16-volume存储

### 16.1安装mariaDB

#### 16.1.1 环境所需镜像

k8s集群每个node节点需要下载镜像

```shell
docker pull mariadb:10.5.2 
```

#### 16.1.2 部署service

1、在`k8sdemo01`工程创建`mariadb.yml`文件

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mariadb-deploy
  labels:
    app: mariadb-deploy
spec:
  replicas: 1
  template:
    metadata:
      name: mariadb-deploy
      labels:
        app: mariadb-deploy
    spec:
      containers:
        - name: mariadb-deploy
          image: mariadb:10.5.2
          imagePullPolicy: IfNotPresent
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: admin #这是mysqlroot用户的密码
            - name: TZ
              value: Asia/Shanghai
          args:
            - "--character-set-server=utf8mb4"
            - "--collation-server=utf8mb4_unicode_ci"
          ports:
            - containerPort: 3306
      restartPolicy: Always
  selector:
    matchLabels:
      app: mariadb-deploy
---
apiVersion: v1
kind: Service
metadata:
  name: mariadb-svc
spec:
  selector:
    app: mariadb-deploy
  ports:
    - port: 3306
      targetPort: 3306
      nodePort: 30036
  type: NodePort
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210712162344.png)

```shell
[root@k8s-master01 maria]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
[root@k8s-master01 maria]# kubectl get pod -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-5cf7cf58b6-xv9vp   1/1     Running   0          28s   10.81.58.247   k8s-node02   <none>           <none>
[root@k8s-master01 maria]# 
```

#### 16.1.3 客户端测试

```shell
IP主机:8.134.125.62
username:root
password:admin
prot: 30036
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210712172156.png" style="zoom:80%;" />

#### 16.1.4 删除service

```yaml
kubectl delete -f mariadb.yml
```

### 16.2 Secret

#### 16.2.1 基本概述

1、基本介绍

- **Secret** 解决了密码、`token`、密钥等敏感数据的配置问题，而不需要把这些敏感数据暴露到镜像或者 `Pod Spec`中。
- `Secret` 可以以` Volume `或者环境变量的方式使用 。

2、Secret 有三种类型

- Service Account :用来访问 `Kubernetes API`，由 Kubernetes 自动创建，并且会自动挂载到 Pod的`/run/secrets/kubernetes.io/serviceaccount `目录中。
- Opaque ：base64编码格式的Secret用来存储密码、密钥等。
- `kubernetes.io/dockerconfigjson` ：用来存储私有 docker registry 的认证信息。

#### 16.2.2 Service Account

1、基本介绍

- `Service Account`简称sa， `Service Account `用来访问 Kubernetes API，由 Kubernetes 自动创建。
- 并且会自动挂载到 Pod的`/run/secrets/kubernetes.io/serviceaccount` 目录中。

2、查看具体信息

```shell
# 查询命名空间为kube-system的pod信息
[root@k8s-master01 maria]# kubectl get pod -n kube-system
NAME                                       READY   STATUS    RESTARTS   AGE
calico-kube-controllers-6b94766748-pn4l8   1/1     Running   27         8d
calico-node-4m62k                          1/1     Running   25         8d
calico-node-7bnqj                          1/1     Running   27         8d
calico-node-krh64                          1/1     Running   28         8d
calico-node-zwvv9                          1/1     Running   12         8d
coredns-6955765f44-nwzg6                   1/1     Running   27         8d
coredns-6955765f44-rdwnc                   1/1     Running   27         8d
etcd-k8s-master01                          1/1     Running   28         8d
kube-apiserver-k8s-master01                1/1     Running   36         8d
kube-controller-manager-k8s-master01       1/1     Running   28         8d
kube-proxy-4vdxm                           1/1     Running   28         8d
kube-proxy-5nlqn                           1/1     Running   26         8d
kube-proxy-npzs2                           1/1     Running   28         8d
kube-proxy-z47rt                           1/1     Running   13         8d
kube-scheduler-k8s-master01                1/1     Running   28         8d

# 进入pod: kube-proxy-5nlqn,查看具体信息
[root@k8s-master01 maria]# kubectl exec -it kube-proxy-5nlqn -n kube-system sh
# cd /run/secrets/kubernetes.io/serviceaccount
# ls
ca.crt	namespace  token
# cat ca.crt
-----BEGIN CERTIFICATE-----
MIICyDCCAbCgAwIBAgIBADANBgkqhkiG9w0BAQsFADAVMRMwEQYDVQQDEwprdWJl
cm5ldGVzMB4XDTIxMDcwNDA2MzYyOVoXDTMxMDcwMjA2MzYyOVowFTETMBEGA1UE
AxMKa3ViZXJuZXRlczCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAL0V
3D/VEJhT326XWC0Rs1I/j4/AdidXF1cH/WsoCBl8swK7QYJwWTbBN+boF7VKQOKA
FM2JIqY3NHUXTmU5/vxtmThWQHHPlkXtnW8UzoEaf/KnGu/lY1V7eHZN6ElO8pSz
BFEZ5rBe/9SR4KDMdXiI2CvV+zbZut64Fq4QJFGcjey4H3FWsZqyBT3EiTA5xnIF
xRHm+3wBHDNIRg6tB0PLyrmQvCnA1oWzZIxyTZ00TKhiQEiKH331yl5OA9f5ukZi
hpto2NP/pwafLqthdYvY2Y10LHt81VbscbsVjFDKH8ljWQiB0MQWUej0RoQlHRAS
ih9q8KgIpLRCycoHpLcCAwEAAaMjMCEwDgYDVR0PAQH/BAQDAgKkMA8GA1UdEwEB
/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAGICNb3Y63Yy6TEqmtBoBgTwYS3W
MjvGGVObSXhXU6tQBIWMUYSi+GgWUyEJAcnCNV4S4/0c8zZ0OTL09oYpX2qzYPK+
SVB3m42XwGxE4cAvWWXTe23/7sEri8AsJ/OqiK8f9z+vJaITJBzFchj7OKiFgTz3
DtGLLYQT5ytKx/oqtCAbV0hIxQ+z95vUlWzA1gQsfJGBtJUNCMc2R5m3x+a6dyTm
RMhpOGCusq0ytpmGJNP1BSbvmQJ3eH9DDzAlgfOYsWJR2XU79wd7w79772qIRH6+
lXRMW5BbXZTOmHFHZZkejut3ld8zs5ob2nrDMApI68VlCozWltUTxRO+pqs=
-----END CERTIFICATE-----
# cat namespace
kube-system# cat token
eyJhbGciOiJSUzI1NiIsImtpZCI6ImJobzhHZEVCSDA4RXlENzR5dzFHY21BSHVvdDg2WmI0VlVocUUtLWpXbkUifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJrdWJlLXByb3h5LXRva2VuLWN2dGJtIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6Imt1YmUtcHJveHkiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiJjOTIxMDc3ZS1lZDBiLTRiOGItYTliMy05MThlYzg3YTkyZWEiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06a3ViZS1wcm94eSJ9.sPLCPCri4n2--gGR6WoXpQrKCo0-3WCZB9AqoJXUGET6FUuYbkhtvHP_CiNSbtJJDbjjvzsMYWnwW4l-zcCIpVgk4ZhUwqIE6FkMv6oM6t-pb2Dp-7Q4xac8PjajtJC0OsDRCkcmyx_BVsyOvr94ZKnTwpjBT_UiAtBXj7wdS7hrpjN7VlWfLu3wr_qhquac-Y5D0ORSH2BhtpKDziaNkeReiJVgScNZaCDGc4rZNZcSX1jm0Rrpmh4BjWJcJ4kNLhXZ-Cm0J5_CC1W1idyRUNjJWk3iFk_JYbbS2L3ieQjQrHIx4YS7VrVViKQInZGxdF7bh9naSNLrxz1Hp3Cmxw# 
# exit
command terminated with exit code 127
[root@k8s-master01 maria]# 
```

#### 16.2.3 Opaque Secret

Opaque 类型的数据是一个 map 类型，要求 value 是 base64 编码格式。

1、 加密、解密

使用命令行方式对需要加密的字符串进行加密，比如说mysql数据库的密码。

```shell
# 1、对admin字符串进行base64加密
[root@k8s-master01 maria]# echo -n "admin" | base64
YWRtaW4=

# 2、base64解密：对加密后的字符串进行解密
[root@k8s-master01 maria]# echo -n "YWRtaW4=" | base64 -d
admin[root@k8s-master01 maria]# 
```

#### 16.2.4 部署service

1、在`k8sdemo01`工程创建`mariadbsecret.yml`文件，对mariadb数据库密码进行加密。

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mariadbsecret
type: Opaque
data:
  password: YWRtaW4=
```

2、在`k8sdemo01`工程创建`mariadb.yml`文件

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mariadb-deploy
  labels:
    app: mariadb-deploy
spec:
  replicas: 1
  template:
    metadata:
      name: mariadb-deploy
      labels:
        app: mariadb-deploy
    spec:
      containers:
        - name: mariadb-deploy
          image: mariadb:10.5.2
          imagePullPolicy: IfNotPresent
          env:
            - name: MYSQL_ROOT_PASSWORD
              #这是mysqlroot用户的密码
              valueFrom:
                secretKeyRef:
                  key: password
                  name: mariadbsecret
            - name: TZ
              value: Asia/Shanghai
          args:
            - "--character-set-server=utf8mb4"
            - "--collation-server=utf8mb4_unicode_ci"
          ports:
            - containerPort: 3306
      restartPolicy: Always
  selector:
    matchLabels:
      app: mariadb-deploy
---
apiVersion: v1
kind: Service
metadata:
  name: mariadb-svc
spec:
  selector:
    app: mariadb-deploy
  ports:
    - port: 3306
      targetPort: 3306
      nodePort: 30036
  type: NodePort
```

3、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210712230411.png)

```shell
root@k8s-master01 secrets]# ls
mariadbsecret.yml  mariadb.yml
[root@k8s-master01 secrets]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
secret/mariadbsecret created
[root@k8s-master01 secrets]# kubectl get secrets 
NAME                  TYPE                                  DATA   AGE
default-token-m2ckh   kubernetes.io/service-account-token   3      8d
mariadbsecret         Opaque                                1      27s
[root@k8s-master01 secrets]# kubectl get pod -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP              NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-7cbb7855f5-2fzwq   1/1     Running   0          22s   10.81.135.136   k8s-node03   <none>           <none>
[root@k8s-master01 secrets]# 
```

4、客户端测试

```shell
IP主机:8.134.125.62
username:root
password:admin
prot: 30036
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210712230552.png" style="zoom:80%;" />

### 16.3 harbor私服操作

#### 16.3.1 安装docker compose

1、购买1核4G内存服务器，安装`docker`和`docker compose`

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210713101726.png)

docker compose下载地址:  [https://github.com/docker/compose/releases/tag/1.29.0](https://github.com/docker/compose/releases/tag/1.29.0)

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210614182756.png" style="zoom:80%;" />

2、通过Xftp上传到`linux`服务器中。

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210614182922.png" style="zoom:80%;" />

3、给予授权

```shell
[root@harbor-01 ~]# cd /data/
[root@harbor-01 ~]# cd /home/data/
[root@harbor-01 data]# ls
docker-compose-Linux-x86_64
[root@harbor-01 data]# pwd
/home/data
[root@harbor-01 data]# mv /home/data/docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
mv：是否覆盖"/usr/local/bin/docker-compose"？ y
[root@harbor-01 data]# chmod 777 /usr/local/bin/docker-compose
```

4、检查安装情况以及版本

```shell
docker-compose -v
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210713102207.png)

#### 16.3.2 安装私服

1、下载harbor

官方地址: [https://goharbor.io/](https://goharbor.io/)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617214307.png)

github官网地址：[https://github.com/goharbor/harbor](https://github.com/goharbor/harbor)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617214509.png)

官方帮助文档：[https://github.com/goharbor/harbor/blob/v1.9.4/docs/installation_guide.md](https://github.com/goharbor/harbor/blob/v1.9.4/docs/installation_guide.md)

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210617214659.png)

3、安装harbor开发环境大部分采用http方式进行安装，推荐使用离线安装！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618104517.png)

通过`Xftp`上传到`\home\data`目录中，然后解压软件。

```shell
[root@harbor-01 data]# ls
harbor-offline-installer-v1.9.4.tgz
[root@harbor-01 data]# tar zxvf harbor-offline-installer-v1.9.4.tgz 
harbor/harbor.v1.9.4.tar.gz
harbor/prepare
harbor/LICENSE
harbor/install.sh
harbor/harbor.yml
[root@harbor-01 data]# ll
total 624500
drwxr-xr-x 2 root root      4096 Jun 17 21:53 harbor
-rw-r--r-- 1 root root 639477963 Jun 17 21:11 harbor-offline-installer-v1.9.4.tgz
```

5、进入安装目录，修改` harbor.yml`文件

修改私服镜像地址

```shell
hostname: 192.168.50.137
```

修改镜像地址访问端口号

```shell
port: 5000
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210717195201.png)

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

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210713103249.png)

安装成功！！！

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210618110603.png)

6、使用Chrome 浏览器访问harbor私服，点击链接: [http://192.168.50.137:5000/harbor/projects](http://192.168.50.137:5000/harbor/projects)，输入用户名和默认的密码

```shell
用户名:admin密码: Harbor12345
```

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210713103748.png" style="zoom:80%;" />

#### 16.3.3 配置私服

1、在主机`k8s-master01`中配置私服。

```shell
[root@k8s-master01 data]# vim /etc/docker/daemon.json
[root@k8s-master01 data]# cat /etc/docker/daemon.json
{
  "registry-mirrors": ["https://5bsomu6l.mirror.aliyuncs.com"],
  "insecure-registries":["192.168.50.137:5000"],
  "exec-opts": ["native.cgroupdriver=systemd"]
}
[root@k8s-master01 data]# systemctl daemon-reload
[root@k8s-master01 data]# systemctl restart docker
[root@k8s-master01 data]# 
```

2、在`harbor`界面中新建项目：`guardwhy_cms`

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210717195533.png)

3、登录和退出私服

```shell
## 登录私服
docker login -u admin -p Harbor12345 192.168.50.137:5000

## 退出私服
docker logout 192.168.50.137:5000
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210717200141.png)

4、查看当前镜像

```shell
[root@k8s-master01 data]# docker images
REPOSITORY                           TAG       IMAGE ID       CREATED         SIZE
calico/node                          v3.14.2   780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol            v3.14.2   9dfa8f25b51c   11 months ago   22.8MB
calico/cni                           v3.14.2   e6189009f081   11 months ago   119MB
calico/kube-controllers              v3.14.2   4815e4106d26   11 months ago   52.8MB
mariadb                              10.5.2    fd055a110f74   14 months ago   360MB
k8s.gcr.io/kube-proxy                v1.17.5   e13db435247d   15 months ago   116MB
k8s.gcr.io/kube-controller-manager   v1.17.5   fe3d691efbf3   15 months ago   161MB
k8s.gcr.io/kube-apiserver            v1.17.5   f640481f6db3   15 months ago   171MB
k8s.gcr.io/kube-scheduler            v1.17.5   f648efaff966   15 months ago   94.4MB
k8s.gcr.io/coredns                   1.6.5     70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                      3.4.3-0   303ce5db0e90   20 months ago   288MB
k8s.gcr.io/pause                     3.1       da86e6ba6ca1   3 years ago     742kB
[root@k8s-master01 data]# 
```

4、上传镜像

```shell
[root@k8s-master01 data]# docker tag mariadb:10.5.2 192.168.50.137:5000/guardwhy_cms/mariadb:10.5.2
[root@k8s-master01 data]# docker images
REPOSITORY                               TAG       IMAGE ID       CREATED         SIZE
calico/node                              v3.14.2   780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol                v3.14.2   9dfa8f25b51c   11 months ago   22.8MB
calico/cni                               v3.14.2   e6189009f081   11 months ago   119MB
calico/kube-controllers                  v3.14.2   4815e4106d26   11 months ago   52.8MB
8.134.33.142:5000/guardwhy_cms/mariadb   10.5.2    fd055a110f74   14 months ago   360MB
mariadb                                  10.5.2    fd055a110f74   14 months ago   360MB
k8s.gcr.io/kube-proxy                    v1.17.5   e13db435247d   15 months ago   116MB
k8s.gcr.io/kube-apiserver                v1.17.5   f640481f6db3   15 months ago   171MB
k8s.gcr.io/kube-controller-manager       v1.17.5   fe3d691efbf3   15 months ago   161MB
k8s.gcr.io/kube-scheduler                v1.17.5   f648efaff966   15 months ago   94.4MB
k8s.gcr.io/coredns                       1.6.5     70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                          3.4.3-0   303ce5db0e90   20 months ago   288MB
k8s.gcr.io/pause                         3.1       da86e6ba6ca1   3 years ago     742kB
[root@k8s-master01 data]# docker push 192.168.50.137:5000/guardwhy_cms/mariadb:10.5.2
The push refers to repository [182.92.126.166:5000/guardwhy_cms/mariadb]
2a75ca7bbb37: Pushed 
ab30662e1c24: Pushed 
dfce0ddc1750: Pushed 
d0abe7e5ebab: Pushed 
2df470f82b36: Pushed 
e0b9a9a4c57f: Pushed 
78452794b5bd: Pushed 
8179bbf82947: Pushed 
fadf5ecbe4d4: Pushed 
28ba7458d04b: Pushed 
838a37a24627: Pushed 
a6ebef4a95c3: Pushed 
b7f7d2967507: Pushed 
10.5.2: digest: sha256:5d8f0d6ef1de0d626fc26355f2ed8965f91f7eb91273087d89e3321e27f16dd7 size: 3034
[root@k8s-master01 data]#
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210713120533.png)

#### 16.3.4 注册私服

1、使用 Kuberctl 创建 docker registry 认证的 secret。

```shell
语法规则：
kubectl create secret docker-registry myregistrykey --docker-
server=REGISTRY_SERVER --docker-username=DOCKER_USER --docker-
password=DOCKER_PASSWORD --docker-email=DOCKER_EMAIL
```

2、具体操作

```shell
[root@k8s-master01 data]# docker rmi -f 192.168.50.137:5000/guardwhy_cms/mariadb:10.5.2
Untagged: 8.134.33.142:5000/guardwhy_cms/mariadb:10.5.2
Untagged: 8.134.33.142:5000/guardwhy_cms/mariadb@sha256:5d8f0d6ef1de0d626fc26355f2ed8965f91f7eb91273087d89e3321e27f16dd7
[root@k8s-master01 data]# docker images
REPOSITORY                           TAG       IMAGE ID       CREATED         SIZE
calico/node                          v3.14.2   780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol            v3.14.2   9dfa8f25b51c   11 months ago   22.8MB
calico/cni                           v3.14.2   e6189009f081   11 months ago   119MB
calico/kube-controllers              v3.14.2   4815e4106d26   11 months ago   52.8MB
mariadb                              10.5.2    fd055a110f74   14 months ago   360MB
k8s.gcr.io/kube-proxy                v1.17.5   e13db435247d   15 months ago   116MB
k8s.gcr.io/kube-apiserver            v1.17.5   f640481f6db3   15 months ago   171MB
k8s.gcr.io/kube-controller-manager   v1.17.5   fe3d691efbf3   15 months ago   161MB
k8s.gcr.io/kube-scheduler            v1.17.5   f648efaff966   15 months ago   94.4MB
k8s.gcr.io/coredns                   1.6.5     70f311871ae1   20 months ago   41.6MB
k8s.gcr.io/etcd                      3.4.3-0   303ce5db0e90   20 months ago   288MB
k8s.gcr.io/pause                     3.1       da86e6ba6ca1   3 years ago     742kB
[root@k8s-master01 data]# clear
[root@k8s-master01 data]# kubectl create secret docker-registry guardwhyharbor \
--docker-server=:5000 --docker-username=admin \
--docker-password=Harbor12345 \
--docker-email=harbor@guardwhy.com
secret/guardwhyharbor created
[root@k8s-master01 data]# systemctl daemon-reload
[root@k8s-master01 data]# systemctl restart docker
[root@k8s-master01 data]# 
```

3、启动和关闭私服

```shell
关闭私服: docker-compose stop
启动私服: docker-compose start
```

#### 16.3.5 secret升级mariadb

1、将mariadb镜像修改为harbor私服地址，在创建 Pod 的时候，通过`imagePullSecrets`来引用刚创建的`myregistrykey`。

```yml
spec:
      imagePullSecrets:
        - name: guardwhyharbor
      containers:
        - name: mariadb-deploy
          image: 192.168.50.137:5000/guardwhy_cms/mariadb:10.5.2
```

2、在`k8sdemo01`工程创建`mariadbsecret.yml`文件，对mariadb数据库密码进行加密。

```yml
apiVersion: v1
kind: Secret
metadata:
  name: mariadbsecret
type: Opaque
data:
  password: YWRtaW4=
```

3、在`k8sdemo01`工程创建`mariadb.yml`文件

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mariadb-deploy
  labels:
    app: mariadb-deploy
spec:
  replicas: 1
  template:
    metadata:
      name: mariadb-deploy
      labels:
        app: mariadb-deploy
    spec:
      imagePullSecrets:
        - name: guardwhyharbor
      containers:
        - name: mariadb-deploy
          image: 192.168.50.137:5000/guardwhy_cms/mariadb:10.5.2

          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 3306
          env:
            - name: MYSQL_ROOT_PASSWORD
              #这是mysqlroot用户的密码
              valueFrom:
                secretKeyRef:
                  key: password
                  name: mariadbsecret
            - name: TZ
              value: Asia/Shanghai
          args:
            - "--character-set-server=utf8mb4"
            - "--collation-server=utf8mb4_unicode_ci"
      restartPolicy: Always
  selector:
    matchLabels:
      app: mariadb-deploy
---
apiVersion: v1
kind: Service
metadata:
  name: mariadb-svc
spec:
  selector:
    app: mariadb-deploy
  ports:
    - port: 3306
      targetPort: 3306
      nodePort: 30036
  type: NodePort
```

4、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210713132140.png)

```shell
[root@k8s-master01 secrets]# ls
mariadbsecret.yml  mariadb.yml
[root@k8s-master01 secrets]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
secret/mariadbsecret created
[root@k8s-master01 secrets]# kubectl get pods -o wide
NAME                             READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-bd846d74f-mlbl2   1/1     Running   0          39s   10.81.58.248   k8s-node02   <none>           <none>
[root@k8s-master01 secrets]# 
```

查看结果

```shell
[root@k8s-node02 ~]# docker images
REPOSITORY                               TAG       IMAGE ID       CREATED         SIZE
calico/node                              v3.14.2   780a7bc34ed2   11 months ago   262MB
calico/pod2daemon-flexvol                v3.14.2   9dfa8f25b51c   11 months ago   22.8MB
calico/cni                               v3.14.2   e6189009f081   11 months ago   119MB
8.134.33.142:5000/guardwhy_cms/mariadb   10.5.2    fd055a110f74   14 months ago   360MB
mariadb                                  10.5.2    fd055a110f74   14 months ago   360MB
k8s.gcr.io/kube-proxy                    v1.17.5   e13db435247d   15 months ago   116MB
k8s.gcr.io/pause                         3.1       da86e6ba6ca1   3 years ago     742kB
[root@k8s-node02 ~]# 
```

5、客户端测试

```shell
IP主机:8.134.127.211
username:root
password:admin
prot: 30036
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210713133855.png" style="zoom:80%;" />

### 16.4 configmap

==ConfigMap是用于保存配置数据的键值对，可以用来保存单个属性，也可以保存配置文件==。ConfigMaps允许你将配置构件与映像内容解耦，以保持容器化应用程序的可移植性。configmap 可以从文件、目录或者 key-value 字符串创建等创建 ConfigMap，也可以通过 kubectl create -f从描述文件创建，还可以使用 kubectl create创建命令。

#### 16.4.1 命令行方式

直接在命令行中指定`configmap`参数创建，即`--from-literal`，从`key-value`字符串创建，从字面值中创建ConfigMap。

1、基本语法

```css
kubectl create configmap【map的名字】 --from-literal=key=value

如果有多个key，value,直接在后边继续写
kubectl create configmap【map的名字】
  --from-literal=key1=value1
  --from-literal=key2=value2
  --from-literal=key3=value4
```

2、案例说明

```shell
# 1、创建configmap
[root@k8s-master01 data]# kubectl create configmap helloconfigmap --from-literal=guardwhy.hello=world
[root@k8s-master01 data]# kubectl get configmaps
NAME             DATA   AGE
helloconfigmap   1      99s
# 2、查看configmap
[root@k8s-master01 data]# kubectl get configmap helloconfigmap -o go-template='{{.data}}'
map[guardwhy.hello:world]
[root@k8s-master01 data]# kubectl delete configmaps helloconfigmap
configmap "helloconfigmap" deleted
[root@k8s-master01 data]#  kubectl get configmaps
No resources found in default namespace.
[root@k8s-master01 data]# 
```

#### 16.4.2 配置文件方式

1、基本语法

当 `--from-file`指向一文件，key的名称是文件名称，value的值是这个文件的内容。

```shell
kubectl create configmap cumulx-test --from-file=xxxx
```

2、案例说明

创建一个配置文件:`jdbc.properties`

```properties
jdbc.driverclass=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/test
jdbc.username=root
jdbc.password=admin
```

3、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210713183450.png)

```shell
[root@k8s-master01 data]# ls
calico.yml  init.sh  jdbc.properties  k8s.1.17.5.tar  secrets
[root@k8s-master01 data]# kubectl create configmap myjdbcmap --from-file=jdbc.properties 
configmap/myjdbcmap created
[root@k8s-master01 data]# kubectl describe configmaps myjdbcmap 
Name:         myjdbcmap
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
jdbc.properties:
----
jdbc.driverclass=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/test
jdbc.username=root
jdbc.password=admin
Events:  <none>
[root@k8s-master01 data]# kubectl delete  configmaps myjdbcmap 
configmap "myjdbcmap" deleted
[root@k8s-master01 data]# 
```

#### 16.4.3 目录方式

指定目录创建，即将一个目录下的所有配置文件创建为一个ConfigMap，--from-file=<目录>

1、基本语法

```shell
语法规则如下: --from-file指向一个目录，每个目录中的文件直接用于填充ConfigMap中的key,key的名称是文件名称，value的值是这个文件的内容。
下面的命令读取/data目录下的所有文件kubectl create configmap cumulx-test --from-file=/data/
```

2、案例说明

```shell
[root@k8s-master01 home]# cd data/
[root@k8s-master01 data]# ls
calico.yml  init.sh  jdbc.properties  k8s.1.17.5.tar  secrets
[root@k8s-master01 data]# pwd
/home/data
# 3、创建configmap
[root@k8s-master01 data]# kubectl create configmap  myjdbcconfigmap --from-file=/home/data/jdbc.properties 
configmap/myjdbcconfigmap created
# 2、查看configmap详细信息
[root@k8s-master01 data]# kubectl describe configmaps myjdbcconfigmap 
Name:         myjdbcconfigmap
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
jdbc.properties:
----
jdbc.driverclass=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/test
jdbc.username=root
jdbc.password=admin
Events:  <none>
[root@k8s-master01 data]# kubectl delete  configmaps myjdbcconfigmap 
configmap "myjdbcconfigmap" deleted
[root@k8s-master01 data]#  
```

#### 16.4.4 资源文件方式

先写好标准的`configmap`的`yaml`文件，然后`kubectl create -f`创建

1、在`k8sdemo01`工程创建`myjdbc.yml`文件

```yml
apiVersion: v1
kind: ConfigMap
metadata:
  name: myjdbcconfigmap
data:
  driverclass: com.mysql.jdbc.Driver
  url: jdbc:mysql://localhost:3306/test
  username: root
  password: admin
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210714103348.png)

```shell
[root@k8s-master01 configmap]# ls
myjdbc.yml
[root@k8s-master01 configmap]# kubectl apply -f .
configmap/myjdbcconfigmap created
[root@k8s-master01 configmap]# kubectl describe configmaps myjdbcconfigmap 
Name:         myjdbcconfigmap
Namespace:    default
Labels:       <none>
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"v1","data":{"driverclass":"com.mysql.jdbc.Driver","password":"admin","url":"jdbc:mysql://localhost:3306/test","username":"r...

Data
====
driverclass:
----
com.mysql.jdbc.Driver
password:
----
admin
url:
----
jdbc:mysql://localhost:3306/test
username:
----
root
Events:  <none>
[root@k8s-master01 configmap]# kubectl delete -f .
configmap "myjdbcconfigmap" deleted
[root@k8s-master01 configmap]# 
```

#### 16.4.5 configmap实践

通过configmap升级mariadb！！！！

1、获得my.cnf文件

```shell
# 1、登录harbor私服
[root@harbor-01 harbor]# docker login -u admin -p Harbor12345 192.168.50.137:5000
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
# 2、运行和下载镜像
[root@harbor-01 harbor]# docker run --name mymariadb -e MYSQL_ROOT_PASSWORD=my-secret-pw -d 192.168.50.137:5000/guardwhy_cms/mariadb:10.5.2
Unable to find image '192.168.50.137:5000/guardwhy_cms/mariadb:10.5.2' locally
10.5.2: Pulling from guardwhy_cms/mariadb
23884877105a: Pull complete 
bc38caa0f5b9: Pull complete 
2910811b6c42: Pull complete 
36505266dcc6: Pull complete 
e69dcc78e96e: Pull complete 
222f44c5392d: Pull complete 
efc64ea97b9c: Pull complete 
9912a149de6b: Pull complete 
7ef6cf5b5697: Pull complete 
8a05be3688e0: Pull complete 
2646a5747ebf: Pull complete 
89e136edbb1e: Pull complete 
2c75ff2ed459: Pull complete 
Digest: sha256:5d8f0d6ef1de0d626fc26355f2ed8965f91f7eb91273087d89e3321e27f16dd7
Status: Downloaded newer image for 8.134.129.140:5000/guardwhy_cms/mariadb:10.5.2
5093724c84b390f4dbce6c311f51087454650ec5ebdf0d1c72c68026f755743a
# 3、将my.cnf文件从容器中复制到/home/data目录
[root@harbor-01 harbor]# docker cp mymariadb:/etc/mysql/my.cnf /home/data
[root@harbor-01 harbor]# ls
ca_download  database            harbor.v1.9.4.tar.gz  install.sh  LICENSE  psc    registry
common       docker-compose.yml  harbor.yml            job_logs    prepare  redis  secret
[root@harbor-01 harbor]# cd ../
[root@harbor-01 data]# ls
harbor  harbor-offline-installer-v1.9.4.tgz  k8s.1.17.5.tar  my.cnf
[root@harbor-01 data]# 
```

2、更改`my.cnf`文件中的端口号为：3307

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210714152758.png)

3、生成`configmap`文件

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210714153813.png)

```shell
[root@k8s-master01 data]# ls
calico.yml  init.sh  jdbc.properties  k8s.1.17.5.tar  my.cnf
[root@k8s-master01 data]# kubectl create configmap mysqlini --from-file=my.cnf
configmap/mysqlini created
[root@k8s-master01 data]# kubectl get configmap mysqlini -o yaml > mariadbconfigmap.yml
[root@k8s-master01 data]# ls
calico.yml  init.sh  jdbc.properties  k8s.1.17.5.tar  mariadbconfigmap.yml  my.cnf
[root@k8s-master01 data]# 
```

4、创建资源文件清单

**mariadbconfigmap.yml**

```yaml
apiVersion: v1
data:
  my.cnf: "# MariaDB database server configuration file.\n#\n# You can copy this file
    to one of:\n# - \"/etc/mysql/my.cnf\" to set global options,\n# - \"~/.my.cnf\"
    to set user-specific options.\n# \n# One can use all long options that the program
    supports.\n# Run program with --help to get a list of available options and with\n#
    --print-defaults to see which it would actually understand and use.\n#\n# For
    explanations see\n# http://dev.mysql.com/doc/mysql/en/server-system-variables.html\n\n#
    This will be passed to all mysql clients\n# It has been reported that passwords
    should be enclosed with ticks/quotes\n# escpecially if they contain \"#\" chars...\n#
    Remember to edit /etc/mysql/debian.cnf when changing the socket location.\n[client]\nport\t\t=
    3307\nsocket\t\t= /var/run/mysqld/mysqld.sock\n\n# Here is entries for some specific
    programs\n# The following values assume you have at least 32M ram\n\n# This was
    formally known as [safe_mysqld]. Both versions are currently parsed.\n[mysqld_safe]\nsocket\t\t=
    /var/run/mysqld/mysqld.sock\nnice\t\t= 0\n\n[mysqld]\n#\n# * Basic Settings\n#\n#user\t\t=
    mysql\npid-file\t= /var/run/mysqld/mysqld.pid\nsocket\t\t= /var/run/mysqld/mysqld.sock\nport\t\t=
    3307\nbasedir\t\t= /usr\ndatadir\t\t= /var/lib/mysql\ntmpdir\t\t= /tmp\nlc_messages_dir\t=
    /usr/share/mysql\nlc_messages\t= en_US\nskip-external-locking\n#\n# Instead of
    skip-networking the default is now to listen only on\n# localhost which is more
    compatible and is not less secure.\n#bind-address\t\t= 127.0.0.1\n#\n# * Fine
    Tuning\n#\nmax_connections\t\t= 100\nconnect_timeout\t\t= 5\nwait_timeout\t\t=
    600\nmax_allowed_packet\t= 16M\nthread_cache_size       = 128\nsort_buffer_size\t=
    4M\nbulk_insert_buffer_size\t= 16M\ntmp_table_size\t\t= 32M\nmax_heap_table_size\t=
    32M\n#\n# * MyISAM\n#\n# This replaces the startup script and checks MyISAM tables
    if needed\n# the first time they are touched. On error, make copy and try a repair.\nmyisam_recover_options
    = BACKUP\nkey_buffer_size\t\t= 128M\n#open-files-limit\t= 2000\ntable_open_cache\t=
    400\nmyisam_sort_buffer_size\t= 512M\nconcurrent_insert\t= 2\nread_buffer_size\t=
    2M\nread_rnd_buffer_size\t= 1M\n#\n# * Query Cache Configuration\n#\n# Cache only
    tiny result sets, so we can fit more in the query cache.\nquery_cache_limit\t\t=
    128K\nquery_cache_size\t\t= 64M\n# for more write intensive setups, set to DEMAND
    or OFF\n#query_cache_type\t\t= DEMAND\n#\n# * Logging and Replication\n#\n# Both
    location gets rotated by the cronjob.\n# Be aware that this log type is a performance
    killer.\n# As of 5.1 you can enable the log at runtime!\n#general_log_file        =
    /var/log/mysql/mysql.log\n#general_log             = 1\n#\n# Error logging goes
    to syslog due to /etc/mysql/conf.d/mysqld_safe_syslog.cnf.\n#\n# we do want to
    know about network errors and such\n#log_warnings\t\t= 2\n#\n# Enable the slow
    query log to see queries with especially long duration\n#slow_query_log[={0|1}]\nslow_query_log_file\t=
    /var/log/mysql/mariadb-slow.log\nlong_query_time = 10\n#log_slow_rate_limit\t=
    1000\n#log_slow_verbosity\t= query_plan\n\n#log-queries-not-using-indexes\n#log_slow_admin_statements\n#\n#
    The following can be used as easy to replay backup logs or for replication.\n#
    note: if you are setting up a replication slave, see README.Debian about\n#       other
    settings you may need to change.\n#server-id\t\t= 1\n#report_host\t\t= master1\n#auto_increment_increment
    = 2\n#auto_increment_offset\t= 1\n#log_bin\t\t\t= /var/log/mysql/mariadb-bin\n#log_bin_index\t\t=
    /var/log/mysql/mariadb-bin.index\n# not fab for performance, but safer\n#sync_binlog\t\t=
    1\nexpire_logs_days\t= 10\nmax_binlog_size         = 100M\n# slaves\n#relay_log\t\t=
    /var/log/mysql/relay-bin\n#relay_log_index\t= /var/log/mysql/relay-bin.index\n#relay_log_info_file\t=
    /var/log/mysql/relay-bin.info\n#log_slave_updates\n#read_only\n#\n# If applications
    support it, this stricter sql_mode prevents some\n# mistakes like inserting invalid
    dates etc.\n#sql_mode\t\t= NO_ENGINE_SUBSTITUTION,TRADITIONAL\n#\n# * InnoDB\n#\n#
    InnoDB is enabled by default with a 10MB datafile in /var/lib/mysql/.\n# Read
    the manual for more InnoDB related options. There are many!\ndefault_storage_engine\t=
    InnoDB\ninnodb_buffer_pool_size\t= 256M\ninnodb_log_buffer_size\t= 8M\ninnodb_file_per_table\t=
    1\ninnodb_open_files\t= 400\ninnodb_io_capacity\t= 400\ninnodb_flush_method\t=
    O_DIRECT\n#\n# * Security Features\n#\n# Read the manual, too, if you want chroot!\n#
    chroot = /var/lib/mysql/\n#\n# For generating SSL certificates I recommend the
    OpenSSL GUI \"tinyca\".\n#\n# ssl-ca=/etc/mysql/cacert.pem\n# ssl-cert=/etc/mysql/server-cert.pem\n#
    ssl-key=/etc/mysql/server-key.pem\n\n#\n# * Galera-related settings\n#\n[galera]\n#
    Mandatory settings\n#wsrep_on=ON\n#wsrep_provider=\n#wsrep_cluster_address=\n#binlog_format=row\n#default_storage_engine=InnoDB\n#innodb_autoinc_lock_mode=2\n#\n#
    Allow server to accept connections on all interfaces.\n#\n#bind-address=0.0.0.0\n#\n#
    Optional setting\n#wsrep_slave_threads=1\n#innodb_flush_log_at_trx_commit=0\n\n[mysqldump]\nquick\nquote-names\nmax_allowed_packet\t=
    16M\n\n[mysql]\n#no-auto-rehash\t# faster start of mysql but no tab completion\n\n[isamchk]\nkey_buffer\t\t=
    16M\n\n#\n# * IMPORTANT: Additional settings that can override those from this
    file!\n#   The files must end with '.cnf', otherwise they'll be ignored.\n#\n!include
    /etc/mysql/mariadb.cnf\n!includedir /etc/mysql/conf.d/\n"
kind: ConfigMap
metadata:
  name: mariadbconfigmap
```

**mariadbsecret.yml**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mariadbsecret
type: Opaque
data:
  password: YWRtaW4=
```

**mariadb.yml**

**注意**：修改pod的端口号为3307，service的`targetPort`端口号为3307

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mariadb-deploy
  labels:
    app: mariadb-deploy
spec:
  replicas: 1
  template:
    metadata:
      name: mariadb-deploy
      labels:
        app: mariadb-deploy
    spec:
      imagePullSecrets:
        - name: guardwhyharbor
      containers:
        - name: mariadb-deploy
          image: 192.168.50.137:5000/guardwhy_cms/mariadb:10.5.2
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 3307
          env:
            - name: MYSQL_ROOT_PASSWORD
              #这是mysqlroot用户的密码
              valueFrom:
                secretKeyRef:
                  key: password
                  name: mariadbsecret
            - name: TZ
              value: Asia/Shanghai
          args:
            - "--character-set-server=utf8mb4"
            - "--collation-server=utf8mb4_unicode_ci"
          volumeMounts:
          	#容器内的挂载目录
            - mountPath: /etc/mysql/mariadb.conf.d/
            #随便给一个名字,这个名字必须与volumes.name一致
              name: guardwhy-mariadb 
      restartPolicy: Always
      volumes:
        - name: guardwhy-mariadb
          configMap:
            name: mariadbconfigmap
  selector:
    matchLabels:
      app: mariadb-deploy
---
apiVersion: v1
kind: Service
metadata:
  name: mariadb-svc
spec:
  selector:
    app: mariadb-deploy
  ports:
    - port: 3307
      targetPort: 3307
      nodePort: 30036
  type: NodePort
```

5、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210717205131.png)

```shell
[root@k8s-master01 data]# ls
calico.yml  configmap  k8s.1.17.5.tar  mariadbconfigmap.yml  my.cnf
[root@k8s-master01 data]# cd configmap/
[root@k8s-master01 configmap]# ls
mariadbconfigmap.yml  mariadbsecret.yml  mariadb.yml
[root@k8s-master01 configmap]# ls
mariadbconfigmap.yml  mariadbsecret.yml  mariadb.yml
[root@k8s-master01 configmap]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
configmap/mariadbconfigmap created
secret/mariadbsecret created
[root@k8s-master01 configmap]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
mariadb-deploy-686b78c486-nxx42   1/1     Running   0          15s
[root@k8s-master01 configmap]# kubectl get secrets 
NAME                  TYPE                                  DATA   AGE
default-token-2qdss   kubernetes.io/service-account-token   3      3h52m
guardwhyharbor        kubernetes.io/dockerconfigjson        1      3h6m
mariadbsecret         Opaque                                1      18m
[root@k8s-master01 configmap]# kubectl get configmaps 
NAME               DATA   AGE
mariadbconfigmap   1      18m
mysqlini           1      25m
[root@k8s-master01 configmap]# kubectl get pod -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-686b78c486-nxx42   1/1     Running   0          19m   10.81.58.193   k8s-node02   <none>           <none>
[root@k8s-master01 configmap]# 
```

5、客户端测试，数据库连接

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210717205405.png" style="zoom:80%;" />

#### 16.4.6 查看mariadb容器日志

查看mariadb容器日志：mariadb启动port是否为3307

```shell
kubectl logs -f mariadb-deploy-686b78c486-nxx42
```

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210717205905.png)

### 16.5 label操作

在某些特殊情况下，需要将某些服务固定在一台宿主机上, k8s可以使用label给node节点打上标签来满足这种需求。

#### 16.5.1 添加label语法

1、基本语法格式 : `kubectl label nodes <node-name> <label-key>=<label-value>`

```shell
# 1、给k8s-node02添加标签
[root@k8s-master01 configmap]# kubectl label nodes k8s-node02 mariadb=mariadb10.5.2
node/k8s-node02 labeled
# 2、查看node节点label值
[root@k8s-master01 configmap]# kubectl get nodes --show-labels 
NAME           STATUS   ROLES    AGE     VERSION   LABELS
k8s-master01   Ready    master   5h30m   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-master01,kubernetes.io/os=linux,node-role.kubernetes.io/master=
k8s-node01     Ready    <none>   5h29m   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node01,kubernetes.io/os=linux
k8s-node02     Ready    <none>   5h29m   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node02,kubernetes.io/os=linux,mariadb=mariadb10.5.2
k8s-node03     Ready    <none>   5h29m   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node03,kubernetes.io/os=linux
[root@k8s-master01 configmap]# 
```

#### 16.5.2 修改label的值

1、基本语法: `kubectl label nodes <node-name> <label-key>=<label-value> --overwrite`

```shell
# 1、修改k8s-node02节点label值标签
[root@k8s-master01 configmap]# kubectl label nodes k8s-node02 mariadb=mariadb --overwrite 
node/k8s-node02 labeled
# 2、查看node节点label值
[root@k8s-master01 configmap]# kubectl get nodes --show-labels 
NAME           STATUS   ROLES    AGE     VERSION   LABELS
k8s-master01   Ready    master   5h36m   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-master01,kubernetes.io/os=linux,node-role.kubernetes.io/master=
k8s-node01     Ready    <none>   5h35m   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node01,kubernetes.io/os=linux
k8s-node02     Ready    <none>   5h35m   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node02,kubernetes.io/os=linux,mariadb=mariadb
k8s-node03     Ready    <none>   5h34m   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node03,kubernetes.io/os=linux
[root@k8s-master01 configmap]# 
```

#### 16.5.3 删除label语法

1、基本语法: `kubectl label nodes <node-name> <label-key>-`

```shell
[root@k8s-master01 data]# ls
calico.yml  configmap  k8s.1.17.5.tar  label
[root@k8s-master01 data]# cd configmap/
[root@k8s-master01 configmap]# ls
mariadbconfigmap.yml  mariadbsecret.yml  mariadb.yml
[root@k8s-master01 configmap]# kubectl label nodes k8s-node02 mariadb-
node/k8s-node02 labeled
[root@k8s-master01 configmap]# kubectl get nodes --show-labels 
NAME           STATUS   ROLES    AGE   VERSION   LABELS
k8s-master01   Ready    master   17h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-master01,kubernetes.io/os=linux,node-role.kubernetes.io/master=
k8s-node01     Ready    <none>   17h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node01,kubernetes.io/os=linux
k8s-node02     Ready    <none>   17h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node02,kubernetes.io/os=linux
k8s-node03     Ready    <none>   17h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node03,kubernetes.io/os=linux
[root@k8s-master01 configmap]# 
```

#### 16.5.4 部署service

通过指定node节点`label`，将mariaDB部署到指定节点。

1、指定`k8s-node02`节点

```shell
# 1、给k8s-node02添加标签
[root@k8s-master01 configmap]# kubectl label nodes k8s-node02 mariadb=mariadbSQL
node/k8s-node02 labeled
# 2、查看node节点label值
[root@k8s-master01 configmap]# kubectl get nodes --show-labels 
NAME           STATUS   ROLES    AGE   VERSION   LABELS
k8s-master01   Ready    master   17h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-master01,kubernetes.io/os=linux,node-role.kubernetes.io/master=
k8s-node01     Ready    <none>   17h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node01,kubernetes.io/os=linux
k8s-node02     Ready    <none>   17h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node02,kubernetes.io/os=linux,mariadb=mariadbSQL
k8s-node03     Ready    <none>   17h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node03,kubernetes.io/os=linux
[root@k8s-master01 configmap]# 
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718102505.png)

```shell
[root@k8s-master01 label]# ls
mariadbconfigmap.yml  mariadbsecret.yml  mariadb.yml
[root@k8s-master01 label]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
configmap/mariadbconfigmap created
secret/mariadbsecret created
[root@k8s-master01 label]# kubectl get pods -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-59745d48ff-cjj4x   1/1     Running   0          21s   10.81.58.195   k8s-node02   <none>           <none>
[root@k8s-master01 label]# 
```

3、客户端测试，数据库连接

```yaml
IP主机:192.168.50.135
username:root
password:admin
prot: 30036
```

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718110127.png" style="zoom:80%;" />

### 16.6 hostPath

hostPath类型的存储卷: ==是指将工作节点上某文件系统的目录或文件挂载于Pod中的一种存储卷==。把宿主机上的目录挂载到容器，但是在每个节点上都要有，因为不确定容器会分配到哪个节点。也是把存储从宿主机挂载到k8s集群上，但它有许多限制，例如只支持单节点（Node），而且只支持`ReadWriteOnce`模式。

#### 16.6.1 指定node节点

```shell
[root@k8s-master01 label]# ls
mariadbconfigmap.yml  mariadbsecret.yml  mariadb.yml
# 1、给k8s-node02添加标签
[root@k8s-master01 label]# kubectl label nodes k8s-node02 mariadb=mariadb
node/k8s-node02 labeled
# 2、查看node节点label值
[root@k8s-master01 label]# kubectl get nodes --show-labels
NAME           STATUS   ROLES    AGE   VERSION   LABELS
k8s-master01   Ready    master   20h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-master01,kubernetes.io/os=linux,node-role.kubernetes.io/master=
k8s-node01     Ready    <none>   20h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node01,kubernetes.io/os=linux
k8s-node02     Ready    <none>   20h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node02,kubernetes.io/os=linux,mariadb=mariadb
k8s-node03     Ready    <none>   20h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node03,kubernetes.io/os=linux
[root@k8s-master01 label]# 
```

#### 16.6.2 挂载卷

1、基本语法

```shell
volumeMounts为containers下级key，containers.volumeMounts, volumes与 containers平级。

containers.volumeMounts.name与volumes.name值一致。

containers.volumeMounts.mountPath是容器内目录,volumes.hostPath.path是宿主机挂载目录。

volumes.hostPath.type值必须为"Directory"。
```

#### 16.6.3 部署service

1、修改`mariadb.yml`，添加以下内容	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718145528.png" style="zoom:80%;" />

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718145721.png)

```shell
[root@k8s-master01 data]# ls
calico.yml  configmap  hostpath  k8s.1.17.5.tar  label
[root@k8s-master01 data]# cd hostpath/
[root@k8s-master01 hostpath]# ls
mariadbconfigmap.yml  mariadbsecret.yml  mariadb.yml
[root@k8s-master01 hostpath]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
configmap/mariadbconfigmap created
secret/mariadbsecret created
[root@k8s-master01 hostpath]# kubectl get pod -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-554dbc5f45-42kx7   1/1     Running   0          18s   10.81.58.194   k8s-node02   <none>           <none>
[root@k8s-master01 hostpath]#
```

3、客户端测试，数据库连接

```shell
IP主机:192.168.50.135username:rootpassword:adminprot: 30036
```

<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718110127.png" style="zoom:80%;" />

4、通过Navicat工具，创建新的`guardwhy_cms`数据库

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718163025.png" style="zoom:80%;" />

5、进入`k8s-node02`节点，查看具体挂载点

```shell
[root@k8s-node02 ~]# ls
anaconda-ks.cfg
[root@k8s-node02 ~]# mkdir /home/data/mariadb
[root@k8s-node02 ~]# ls
anaconda-ks.cfg
[root@k8s-node02 ~]# cd /home/data/mariadb/
[root@k8s-node02 mariadb]# ls
[root@k8s-node02 mariadb]# ls
aria_log.00000001  guardwhy_cms    ibdata1      ibtmp1             mysql
aria_log_control   ib_buffer_pool  ib_logfile0  multi-master.info  performance_schema
[root@k8s-node02 mariadb]# 
```

## 17- PV&&PVC

### 17.1存储机制介绍

在 Kubernetes 中，存储资源和计算资源(CPU、Memory)同样重要，Kubernetes 为了能让管理员方便管理集群中的存储资源，同时也为了让使用者使用存储更加方便，所以屏蔽了底层存储的实现细节，将存储抽象出两个 API 资源`PersistentVolume` 和 `PersistentVolumeClaim`对象来对存储进行管理。

### 17.2 PV(持久化卷)

#### 17.2.1 基本概念

**PersistentVolume(持久化卷)**：`PersistentVolume` 简称 PV ，是对底层共享存储的一种抽象，将共享存储定义为一种资源，它属于集群级别资源，不属于任何  `Namespace` 用户使用 PV需要通过 PVC 申请，PV 是由管理员进行创建和配置，它和具体的底层的共享存储技术的实现方式有关，比如说 `Ceph`、`GlusterFS`、`NFS` ，都是通过插件机制完成与共享存储的对接，且根据不同的存储 PV 可配置参数也是不相同。

#### 17.2.2 PV生命周期

命令行会显示绑定到 PV 的 PVC 的名称：`kubectl get pv`

PV 生命周期总共四个阶段 ：

- Available（可用）—— 可用状态，尚未被 PVC 绑定。
- Bound（已绑定）—— 绑定状态，已经与某个 PVC 绑定。
- Released（已释放）—— 与之绑定的 PVC 已经被删除，但资源尚未被集群回收。
- Failed（失败）—— 当删除 PVC 清理资源，自动回收卷时失败，所以处于故障状态。

#### 17.2.3 PV常用配置参数

1、存储能力(capacity）

- PV 可以通过配置`capacity`中的`storage`参数，对`PV`挂多大存储空间进行设置，目前`capacity`只有一个设置存储大小的选项，未来可能会增加。

2、存储卷模式(volumeMode)

PV 可以通过配置  volumeMode 参数，对存储卷类型进行设置，可选项包括：

- Filesystem： 文件系统，默认是此选项。
- Block： 块设备
- 目前 Block 模式只有 AWSElasticBlockStore、AzureDisk、FC、GCEPersistentDisk、iSCSI、LocalVolume、RBD、VsphereVolume支持。

3、访问模式(accessModes)

PV 可以通过配置`accessModes`参数，设置访问模式来限制应用对资源的访问权限，有以下机制访问模式：

- `ReadWriteOnce`——该卷可以被单个节点以读/写模式挂载。
- `ReadOnlyMany`——该卷可以被多个节点以只读模式挂载。
- `ReadWriteMany`——该卷可以被多个节点以读/写模式挂载。

==PersistentVolume 可以以资源提供者支持的任何方式挂载到主机上==。供应商具有不同的功能，每个PV的访问模式都将被设置为该卷支持的特定模式。例如，NFS 可以支持多个读/写客户端，但特定的 NFS，PV 可能以只读方式导出到服务器上，每个 PV 都有一套自己的用来描述特定功能的访问模式。

**注意事项**: 在命令行中，访问模式缩写为

- RWO - `ReadWriteOnce`。
- ROX - `ReadOnlyMany`。
- RWX - `ReadWriteMany`。

4、挂载参数(mountOptions）

PV 可以根据不同的存储卷类型，设置不同的挂载参数，每种类型的存储卷可配置参数都不相同。如 NFS存储，可以设置 NFS 挂载配置，如下

```yaml
mountOptions:
- hard
- nfsvers=4
```

5、存储类(storageClassName）

PV可以通过配置`storageClassName`参数指定一个存储类`StorageClass`资源，具有特定`StorageClass`的PV只能与指定相同`StorageClass`的 PVC 进行绑定，没有设置`StorageClass`的PV 也是同样只能与没有指定`StorageClass`的PVC 绑定。

6、回收策略(persistentVolumeReclaimPolicy）

PV 可以通过配置`persistentVolumeReclaimPolicy`参数设置回收策略，可选项如下：

- Retain(保留)：保留数据，需要由管理员手动清理。
- Recycle(回收):  删除数据，即删除目录下的所有文件，比如说执行 `rm -rf /thevolume/* `命令，目前只有`NFS` 和`HostPath`支持。
- Delete(删除)：删除存储资源，仅仅部分云存储系统支持，比如删除 AWS EBS 卷，目前只有AWS EBS，GCE PD，Azure 磁盘和 Cinder 卷支持删除。

### 17.3 PVC【持久化卷声明】

#### 17.3.1 基本概念

**PersistentVolumeClaim(持久化卷声明)**: `PersistentVolumeClaim`简称 PVC，是用户存储的一种声明，类似于对存储资源的申请，它属于一个 `Namespace` 中的资源可用于向`PV`申请存储资源。PVC和 Pod 比较类似Pod 消耗的是 Node节点资源而 PVC 消耗的是 PV 存储资源，`Pod `可以请求 `CPU` 和 `Memory`而 `PVC` 可以请求特定的存储空间和访问模式。

#### 17.3.2 PVC常用参数

1、筛选器（selector）

PVC 可以通过在`Selecter` 中设置 `Laberl` 标签，筛选出带有指定`Label` 的PV 进行绑定。`Selecter` 中可以指定`matchLabels` 或 `matchExpressions` ，如果两个字段都设定了就需要同时满足才能匹配。

```yaml
selector:
matchLabels:
 release: "stable"
matchExpressions:
 - key: environment
  operator: In
  values: dev
```

2、存储类(storageClass）

1、PVC 要想绑定带有特定`StorageClass`的 PV 时，也必须设定`storageClassName` 参数，且名称也必须要和`PV `中的`storageClassName` 保持一致。如果要绑定的  PV 没有设置`storageClassName` 则PVC 中也不需要设置。

2、当 PVC 中如果未指定`storageClassName`参数或者指定为空值，则还需要考虑  Kubernetes 中是否设置了默认的`StorageClass` 

- 未启用`DefaultStorageClass`：等于`storageClassName`值为空。
- 启用`DefaultStorageClass`：等于`storageClassName`值为默认的`StorageClass`。
- 如果设置`storageClassName=""`，则表示该 PVC 不指定 `StorageClass`。

3、访问模式(accessModes）

PVC 中可设置的访问模式与 PV 种一样，用于限制应用对资源的访问权限。

注意:

- 上面两种资源`PV`和`PVC`的存在很好的解决了存储管理的问题，不过这些存储每次都需要管理员手动创建和管理，如果一个集群中有很多应用，并且每个应用都要挂载很多存储，那么就需要创建很多`PV`和 `PVC` 与应用关联。为了解决这个问题 Kubernetes 在 1.4 版本中引入了 `StorageClass`对象。
- 当创建`PVC`时指定对应的`StorageClass`就能和`PV`的`StorageClass`关联，`StorageClass` 会交由与他关联 Provisioner 存储插件来创建与管理存储，它能帮你创建对应的`PV` 和在远程存储上创建对应的文件夹，并且还能根据设定的参数，删除与保留数据。所以管理员只要在`StorageClass`中配置好对应的参数就能方便的管理集群中的存储资源。

#### 17.3.3 PV&PVC 小结

- `PV`就好比是一个仓库，需要先购买一个仓库，即定义一个PV存储服务，例如`CEPH`、`NFS`、`LocalHostpath`。`PVC`就好比租户，`pv`和`pvc`是一对一绑定的，挂载到`POD`中，一个`pvc`可以被多个`pod`挂载。

### 17.4 资源文件清单

1、在`k8sdemo01`工程创建`mariadbpv.yml`文件

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: data-mariadb-pv
  labels:
    app: mariadb-pv
spec:
  # 存储方式
  accessModes:
    #hostpath模式只支持 ReadWriteOnce
    - ReadWriteOnce
    # 分配大小
  capacity:
    storage: 10Gi
    # 挂载目录
  hostPath:
    path: /data/mariadb
    # 文件存储系统
    type: DirectoryOrCreate
  # 回收策略
  persistentVolumeReclaimPolicy: Retain
  # 配置绑定
  storageClassName: standard
  # 创建类型
  volumeMode: Filesystem
```

2、在`k8sdemo01`工程创建`mariadbpvc.yml`文件

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mariadb-pvc
  labels:
    app: mariadb-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: standard
  # 申请资源
  resources:
    requests:
      storage: 5Gi
```

3、修改`mariadb.yml`文件
<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718182451.png" style="zoom:80%;" />

### 17.5 部署service

1、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718202622.png)

```shell
[root@k8s-master01 pvandpvchostpath]# ls
mariadbconfigmap.yml  mariadbpvc.yml  mariadbpv.yml  mariadbsecret.yml  mariadb.yml
[root@k8s-master01 pvandpvchostpath]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
configmap/mariadbconfigmap created
persistentvolume/data-mariadb-pv created
persistentvolumeclaim/mariadb-pvc created
secret/mariadbsecret created
[root@k8s-master01 pvandpvchostpath]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
mariadb-deploy-5b7d6cd497-v58fb   1/1     Running   0          12s
[root@k8s-master01 pvandpvchostpath]# kubectl get pods -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-5b7d6cd497-v58fb   1/1     Running   0          22s   10.81.58.195   k8s-node02   <none>           <none>
[root@k8s-master01 pvandpvchostpath]# kubectl get pv
NAME              CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                 STORAGECLASS   REASON   AGE
data-mariadb-pv   10Gi       RWO            Retain           Bound    default/mariadb-pvc   standard                42s
[root@k8s-master01 pvandpvchostpath]# kubectl get pvc
NAME          STATUS   VOLUME            CAPACITY   ACCESS MODES   STORAGECLASS   AGE
mariadb-pvc   Bound    data-mariadb-pv   10Gi       RWO            standard       53s
[root@k8s-master01 pvandpvchostpath]# 
```

2、通过Navicat工具，创建新的`k8s-test`数据库

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718204956.png)

3、进入`k8s-node02`节点，查看具体挂载点

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210718204844.png)

## 18-NFS存储卷

### 18.1 NFS基本概念

1、NFS是`Network FileSystem`的缩写，顾名思义就是网络文件存储系统，分为服务端(Server)和客户端(Client)，最早由 sun 公司开发，是类 unix 系统间实现磁盘共享的一种方法。它允许网络中的计算机之间通过 TCP/IP 网络共享资源，通过 NFS，本地 NFS 的客户端应用可以透明地读写位于服务端 NFS 服务器上的文件，就像访问本地文件一样方便。简单的理解，NFS 就是可以透过网络，让不同的主机、不同的操作系统可以共享存储的服务。

2、NFS 在文件传送或信息传送过程中依赖于 RPC(`Remote Procedure Call`） 协议，即远程过程调用，NFS 的各项功能都必须要向 RPC 来注册，如此一来 RPC 才能了解 NFS 这个服务的各项功能 `Port`、`PID`、`NFS` 在服务器所监听的` IP `等，而客户端才能够透过 RPC 的询问找到正确对应的端口，所以，NFS必须要有`RPC` 存在时才能成功的提供服务，简单的理解二者关系：==NFS是 一个文件存储系统，而 RPC是负责信息的传输==。

### 18.2 NFS基本操作

1、NFS共享存储方式

- 手动方式静态创建所需要的PV和PVC。
- 通过创建PVC动态地创建对应PV，无需手动创建PV。

2、NFS安装

k8s集群所有节点都需要安装NFS服务，选用k8s的master节点作为NFS服务的server端。

所有的节点都需要安装NFS服务！！！

```shell
yum install -y nfs-utils rpcbind 
```

3、创建共享项目

```shell
[root@k8s-master01 pvandpvchostpath]# cd 
# 1、在master节点创建目录
[root@k8s-master01 ~]# mkdir -p /nfs/mariadb
[root@k8s-master01 ~]# cd /nfs/mariadb/
[root@k8s-master01 mariadb]# ls
[root@k8s-master01 mariadb]# chmod 777 /nfs/mariadb
# 2、更改归属组与用户
[root@k8s-master01 mariadb]# chown nfsnobody /nfs/mariadb

# 3、添加相关的参数
[root@k8s-master01 mariadb]# vim /etc/exports
[root@k8s-master01 mariadb]# cat /etc/exports
/nfs/mariadb *(rw,no_root_squash,no_all_squash,sync)
```

4、启动NFS服务

k8s集群所有节点启动NFS服务

```shell
# 1、所有节点都启动NFS服务
[root@k8s-node02 ~]# systemctl start rpcbind
[root@k8s-node02 ~]# systemctl start nfs

# 2、设置开启启动
[root@k8s-node02 ~]# systemctl enable rpcbind
[root@k8s-node02 ~]# systemctl enable nfs
Created symlink from /etc/systemd/system/multi-user.target.wants/nfs-server.service to /usr/lib/systemd/system/nfs-server.service.
[root@k8s-node02 ~]# 
```

5、测试NFS服务

```shell
# 1、在客户端创建挂在目录
[root@k8s-node03 home]# mkdir -p /home/data/mariad
[root@k8s-node03 ~]# cd /home/data/mariad
[root@k8s-node03 mariad]# pwd
/home/data/mariad
[root@k8s-node03 mariad]# 
# 2、挂载远端目录到服务器(master01服务器) /data/mariadb 目录
[root@k8s-node03 mariad]# mount 192.168.50.133:/nfs/mariadb /home/data/mariad
[root@k8s-node03 mariad]# 

# 3、在服务器(k8s-master01)NFS服务端写入nfs.yml文件
[root@k8s-master01 mariadb]# cd /nfs/mariadb/
[root@k8s-master01 mariadb]# vim nfs.yml
[root@k8s-master01 mariadb]# cat nfs.yml 
This is NFS Server!!!
[root@k8s-master01 mariadb]# 

# 4、客户端读取数据
[root@k8s-node03 data]# cd mariad/
[root@k8s-node03 mariad]# ls
nfs.yml
[root@k8s-node03 mariad]# cat nfs.yml 
This is NFS Server!!!
[root@k8s-node03 mariad]# 
```

6、客户端卸载 NFS 挂载目录

```shell
[root@k8s-node03 mariad]# umount /home/data/mariad 
umount.nfs4: /home/data/mariad: device is busy
# 强制卸载
[root@k8s-node03 mariad]# umount -l /home/data/mariad 
[root@k8s-node03 mariad]# 
```

7、安装NFS4服务

使用NFS4协议方式进行多共享目录配置，所有共享目录的根目录为`/nfs/data`。

K8S的静态NFS服务PV的`nfs:path`的值不用写共享根目录，直接写`/mariadb`即可，K8S会自动配置成`/nfs/data/mariadb`目录。

```shell
[root@k8s-master01 ~]# vim /etc/exports
[root@k8s-master01 ~]# cat /etc/exports
/nfs/data *(rw,fsid=0,sync,no_wdelay,insecure_locks,no_root_squash)
[root@k8s-master01 ~]# systemctl restart rpcbind
[root@k8s-master01 ~]# systemctl restart nfs
[root@k8s-master01 ~]# 
```

### 18.3 部署service

1、在所有的节点创建`/nfs/data/mariadb`文件夹。

```shell
[root@k8s-master01 nfs]# cd /nfs/data/mariadb
[root@k8s-master01 mariadb]# pwd
/nfs/data/mariadb
[root@k8s-master01 mariadb]#
```

2、修改`mariadbpv.yml`文件

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: data-mariadb-pv
  labels:
    app: mariabd-pv
spec:
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 10Gi
  mountOptions:
    - hard
    - nfsvers=4.1
  nfs:
    path: /mariadb
    server: 192.168.50.133
  persistentVolumeReclaimPolicy: Retain
  storageClassName: standard
  volumeMode: Filesystem
```

3、修改`mariadb.yml`文件

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720042218.png)

4、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720042515.png)

```shell
[root@k8s-master01 nfs]# ls
mariadbconfigmap.yml  mariadbpvc.yml  mariadbsecret.yml  mariadb.yml
[root@k8s-master01 nfs]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
configmap/mariadbconfigmap created
persistentvolume/data-mariadb-pv created
persistentvolumeclaim/mariadb-pvc created
secret/mariadbsecret created
[root@k8s-master01 nfs]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
mariadb-deploy-548d7f6846-r54qb   1/1     Running   0          13s
[root@k8s-master01 nfs]# kubectl get pods -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-548d7f6846-r54qb   1/1     Running   0          15m   10.81.58.199   k8s-node02   <none>           <none>
[root@k8s-master01 nfs]# kubectl get pv
NAME              CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                 STORAGECLASS   REASON   AGE
data-mariadb-pv   10Gi       RWO            Retain           Bound    default/mariadb-pvc   standard                15m
[root@k8s-master01 nfs]# kubectl get pvc
NAME          STATUS   VOLUME            CAPACITY   ACCESS MODES   STORAGECLASS   AGE
mariadb-pvc   Bound    data-mariadb-pv   10Gi       RWO            standard       15m
[root@k8s-master01 nfs]# kubectl get configmaps 
NAME               DATA   AGE
mariadbconfigmap   1      15m
[root@k8s-master01 nfs]# kubectl get secrets 
NAME                  TYPE                                  DATA   AGE
default-token-2qdss   kubernetes.io/service-account-token   3      2d11h
guardwhyharbor        kubernetes.io/dockerconfigjson        1      36h
mariadbsecret         Opaque                                1      16m
[root@k8s-master01 nfs]# 
```

5、客户端测试，数据库连接

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720043319.png" style="zoom:80%;" />

6、查看`guardwhy_cms`数据库内容

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720043647.png" style="zoom:80%;" />

```shell
[root@k8s-master01 nfs]# cd /nfs/data/mariadb
[root@k8s-master01 mariadb]# ls
aria_log.00000001  guardwhy_cms    ibdata1      ibtmp1             mysql
aria_log_control   ib_buffer_pool  ib_logfile0  multi-master.info  performance_schema
[root@k8s-master01 mariadb]# 
```

## 19- 集群调度

### 19.1 基本介绍

1、k8s内pod由scheduler调度，scheduler的任务是把pod分配到合适的node节点上。scheduler调度时会考虑到node节点的资源使用情况、port使用情况、volume使用情况，都是在此基础之上，也可以控制pod的调度。

2、Scheduler 是 kubernetes 调度器，主要的任务是把定义的 pod 分配到集群的节点上，但要很多要考虑的问题

- 公平：如何保证每个节点都能被合理分配资源，不要造成一个节点忙死，一个节点闲死局面。
- 资源高效利用：集群所有资源最大化被使用。内存、硬盘、CPU等因素。
- 效率：调度的性能要好，能够尽快地对大批量的 pod 完成调度工作。
- 灵活：允许用户根据自己的需求控制调度的逻辑。

3、`Sheduler` 是作为单独的程序运行，启动之后会一直与 `API Server`保持通讯，获取`PodSpec.NodeName`为空的`pod`，对每个`pod`都会创建一个`binding`，表明该 pod 应该放到哪个节点上 。

### 19.1 固定节点

1、方式一：给某一节点打上标签

```yaml
1.给某一个节点打标签
kubectl label nodes k8s-node01 mariadb=mariadb

2.pod的控制器中增加配置属性
...
spec:
  nodeSelector:
   mariadb: mariadb
...
```

2、方式二：直接修改pod控制器

```yaml
1、删除k8s-node01节点mariadb的label
kubectl label nodes k8s-node02 mariadb-

2、修改pod控制器
spec:
  nodeName: k8s-node02
```

3、修改`mariadb.yml`文件

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720054407.png)

4、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720042515.png)

```shell
[root@k8s-master01 nfs]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
configmap/mariadbconfigmap created
persistentvolume/data-mariadb-pv created
persistentvolumeclaim/mariadb-pvc created
secret/mariadbsecret created
[root@k8s-master01 nfs]# kubectl get pods -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-7698f9d4c8-hjgnm   1/1     Running   0          31s   10.81.85.196   k8s-node01   <none>           <none>
[root@k8s-master01 nfs]# 
```

### 19.2 调度策略

#### 19.2.1 Scheduler调度步骤

1、首先用户在通过 Kubernetes 客户端 Kubectl 提交创建 Pod 的 `Yaml `的文件，向Kubernetes 系统发起资源请求，该资源请求被提交到Kubernetes 系统。

2、Kubernetes 系统中，用户通过命令行工具 Kubectl 向 Kubernetes 集群即 `APIServer` 用 的方式发送`POST`请求，即创建 Pod 的请求。

3、`APIServer` 接收到请求后把创建 `Pod` 的信息存储到 `Etcd` 中，从集群运行那一刻起，资源调度系统Scheduler 就会定时去监控 `APIServer`。

4、通过`APIServer`得到创建 Pod 的信息，`Scheduler`采用 watch 机制，一旦`Etcd`存储 Pod 信息成功便会立即通知`APIServer`。

5、APIServer会立即把Pod创建的消息通知Scheduler，Scheduler发现 Pod 的属性中 Dest Node 为空时(`Dest Node=""`）便会立即触发调度流程进行调度。

6、而这一个创建Pod对象，在调度的过程当中有3个阶段：==节点预选、节点优选、节点选定，从而筛选出最佳的节点==。

- 节点预选：基于一系列的预选规则对每个节点进行检查，将那些不符合条件的节点过滤，从而完成节点的预选。
- 节点优选：对预选出的节点进行优先级排序，以便选出最合适运行Pod对象的节点。
- 节点选定：从优先级排序结果中挑选出优先级最高的节点运行Pod，当这类节点多于1个时，则进行随机选择。

#### 19.2.2 集群调度策略

Kubernetes调度器作为集群的大脑，在如何提高集群的资源利用率、保证集群中服务的稳定运行中也会变得越来越重要Kubernetes的资源分为两种属性。

1. 可压缩资源(例如CPU循环，Disk I/O带宽)都是可以被限制和被回收的，对于一个Pod来说可以降低这些资源的使用量而不去杀掉Pod。
2. 不可压缩资源(例如内存、硬盘空间)一般来说不杀掉Pod就没法回收。未来Kubernetes会加入更多资源，如网络带宽，存储IOPS的支持。

#### 19.2.3 常用预选策略

| 预选策略                        | 作用                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| CheckNodeCondition              | 检查是否可以在节点报告磁盘、网络不可用或未准备好时将Pod调度其上。 |
| HostName                        | 如果Pod对象拥有spec.hostname属性，则检查节点名称字符串是否和该属性值匹配。 |
| PodFitsHostPorts                | Pod的spec.hostPort属性时，检查端口是否被占用。               |
| MatchNodeSelector               | Pod的spec.nodeSelector属性时，检查节点标签。                 |
| NoDiskConflict                  | Pod依赖的存储卷在此节点是否可用，默认没有启用                |
| PodFitsResources                | 检查节点上的资源(CPU、内存)可用性是否满足Pod对象的运行需求。 |
| PodToleratesNodeTaints          | Pod的spec.tolerations属性，仅关注NoSchedule和NoExecute两个效用标识的污点 |
| PodToleratesNodeNoExecuteTaints | Pod的spec.tolerations属性，是否能接纳节点的NoExecute类型污点,默认没有启用 |
| CheckNodeLabelPresence          | 仅检查节点上指定的所有标签的存在性,默认没有启用              |
| CheckServiceAffinity            | 将相同Service的Pod对象放置在同一个或同一类节点上以提高效率,默认没有启用 |
| MaxEBSVolumeCount               | 检查节点已挂载的EBS存储卷数量是否超过设置的最大值，默认为39。 |
| CheckVolumeBinding              | 检查节点上已绑定和未绑定的PVC是否满足需求。                  |
| NoVolumeZoneConflict            | 在给定区域zone限制下，检查此节点部署的Pod对象是否存在存储卷冲突。 |
| CheckNodeMemoryPressure         | 检查节点内存压力，如果压力过大，那就不会讲pod调度至此        |
| CheckPodePIDPressure            | 检查节点PID资源压力                                          |
| CheckNodeDiskPressure           | 检查节点磁盘资源压力                                         |
| MatchInterPodAffinity           | 检查节点是否满足Pod对象亲和性或反亲和性条件                  |

### 19.3 节点硬策略

#### 19.3.1 节点亲和性规则

1、required(硬亲和性、不能商量，必须执行) 、preferred(软亲和性，可以商量，选择执行)。

- 硬亲和性规则不满足时，Pod会置于Pending状态，软亲和性规则不满足时，会选择一个不匹配的节点。
- 当节点标签改变而不再符合此节点亲和性规则时，不会将Pod从该节点移出，仅对新建的Pod对象生效。

#### 19.3.2 节点硬亲和性

1、`requiredDuringSchedulingIgnoredDuringExecution`

方式一：Pod使用 `spec.nodeSelector` (基于等值关系)，Pod使用`spec.nodeName`。
方式二：Pod使用 `spec.affinity` 支持`matchExpressions`属性 (复杂标签选择机制)。

2、键值运算关系

```yaml
In：label 的值在某个列表中
NotIn：label 的值不在某个列表中
Gt：label 的值大于某个值
Lt：label 的值小于某个值
Exists：某个 label 存在
DoesNotExist：某个 label 不存在
```

#### 19.3.3 部署service

1、修改`mariadb.yml`文件，删除`spec.selectNode`或者`spec.nodeName`信息。

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mariadb-deploy
  labels:
    app: mariadb-deploy
spec:
  replicas: 1
  template:
    metadata:
      name: mariadb-deploy
      labels:
        app: mariadb-deploy
    spec:
      imagePullSecrets:
        - name: guardwhyharbor
      affinity:
        # 节点的亲和性
        nodeAffinity:
          # 硬亲和性
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
              # 表达式属性
              - matchExpressions:
                  # 某一个node节点标签的key
                  - key: kubernetes.io/hostname
                    operator: In
                    values:
                      # key对应的值
                      - k8s-node01
      containers:
        - name: mariadb-deploy
          image: 192.168.50.137:5000/guardwhy_cms/mariadb:10.5.2
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 3307
          env:
            - name: MYSQL_ROOT_PASSWORD
              #这是mysqlroot用户的密码
              valueFrom:
                secretKeyRef:
                  key: password
                  name: mariadbsecret
            - name: TZ
              value: Asia/Shanghai
          args:
            - "--character-set-server=utf8mb4"
            - "--collation-server=utf8mb4_unicode_ci"
          volumeMounts:
            - mountPath: /etc/mysql/mariadb.conf.d/   #容器内的挂载目录
              name: guardwhy-mariadb #随便给一个名字,这个名字必须与volumes.name一致
      restartPolicy: Always
      volumes:
        - name: guardwhy-mariadb
          configMap:
            name: mariadbconfigmap
  selector:
    matchLabels:
      app: mariadb-deploy
---
apiVersion: v1
kind: Service
metadata:
  name: mariadb-svc
spec:
  selector:
    app: mariadb-deploy
  ports:
    - port: 3307
      targetPort: 3307
      nodePort: 30036
  type: NodePort
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720082909.png)

```shell
[root@k8s-master01 ~]# ls
anaconda-ks.cfg
[root@k8s-master01 ~]# cd /home/data/
[root@k8s-master01 data]# ls
calico.yml  configmap  hostpath  k8s.1.17.5.tar  label  nfs  pvandpvchostpath
[root@k8s-master01 data]# cd label/
[root@k8s-master01 label]# ls
mariadbconfigmap.yml  mariadbsecret.yml  mariadb.yml
[root@k8s-master01 label]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
configmap/mariadbconfigmap created
secret/mariadbsecret created
[root@k8s-master01 label]# kubectl get pods -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-7c56957b57-vz2bn   1/1     Running   0          16s   10.81.85.197   k8s-node01   <none>           <none>
[root@k8s-master01 label]# 
```

#### 19.3.4 节点软亲和性

1、`preferredDuringSchedulingIgnoredDuringExecution`

- 柔性控制逻辑，当条件不满足时，能接受被编排于其他不符合条件的节点之上。
- 权重 weight 定义优先级，1-100 值越大优先级越高。

2、键值运算关系

```yaml
In：label 的值在某个列表中
NotIn：label 的值不在某个列表中
Gt：label 的值大于某个值
Lt：label 的值小于某个值
Exists：某个 label 存在
DoesNotExist：某个 label 不存在 
```

#### 19.3.5 部署service

1、使用命令获得节点标签及真实节点名称

```shell
[root@k8s-master01 label]# kubectl get nodes --show-labels
NAME           STATUS   ROLES    AGE     VERSION   LABELS
k8s-master01   Ready    master   2d21h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-master01,kubernetes.io/os=linux,node-role.kubernetes.io/master=
k8s-node01     Ready    <none>   2d21h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node01,kubernetes.io/os=linux
k8s-node02     Ready    <none>   2d21h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node02,kubernetes.io/os=linux
k8s-node03     Ready    <none>   2d21h   v1.17.5   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s-node03,kubernetes.io/os=linux
[root@k8s-master01 label]# 
```

2、修改`mariadb.yml`文件，删除`spec.selectNode`或者`spec.nodeName`信息。

​	<img src="https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720140817.png" style="zoom:80%;" />

3、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720141042.png)

```shell
[root@k8s-master01 label]# kubectl apply -f .
deployment.apps/mariadb-deploy created
service/mariadb-svc created
configmap/mariadbconfigmap created
secret/mariadbsecret created
[root@k8s-master01 label]# kubectl get pod
NAME                              READY   STATUS    RESTARTS   AGE
mariadb-deploy-7c56957b57-dftkf   1/1     Running   0          26s
[root@k8s-master01 label]# kubectl get pod -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
mariadb-deploy-7c56957b57-dftkf   1/1     Running   0          35s   10.81.85.198   k8s-node01   <none>           <none>
[root@k8s-master01 label]# 
```

### 19.4 污点

#### 19.4.1 基本概念

1、污点`taints`是定义在node节点 上的键值型属性数据，用于让节点拒绝将Pod调度运行于其上，除非Pod有接纳节点污点的容忍度。容忍度`tolerations`是定义在Pod 上的键值属性数据，用于配置可容忍的污点，且调度器将Pod调度至其能容忍该节点污点的节点上或没有污点的节点上 。

2、对于`nodeAffinity`无论是硬策略(硬亲和)还是软策略(软亲和)方式，都是调度 pod 到预期节点上，而`Taints`恰好与之相反，如果一个节点标记为`Taints` ，除非 pod 也被标识为可以容忍污点节点，否则该Taints 节点不会被调度 pod。

3、节点亲和性，是 pod 的一种属性(偏好或硬性要求)，它使 pod 被吸引到一类特定的节点。Taint 则相反，它使节点能够 排斥 一类特定的 `pod Taint `和 `toleration`相互配合，可以用来避免 pod 被分配到不合适的节点上。每个节点上都可以应用一个或多个`taint` ，这表示对于那些不能容忍这些 `taint` 的 pod，是不会被该节点接受的，如果将`toleration`应用于pod上，则表示这些 pod 可以（但不要求）被调度到具有匹配`taint`的节点上。

#### 19.4.2 定义污点和容忍度

1、污点定义于`nodes.spec.taints`属性，容忍度定义于`pods.spec.tolerations`属性。使用`kubectl taint`命令可以给某个 Node 节点设置污点，Node 被设置上污点之后就和 Pod 之间存在了一种相斥的关系，可以让 Node 拒绝 Pod 的调度执行，甚至将 Node 已经存在的 Pod 驱逐出去 。

2、语法：`key=value:effect`

```yaml
# 1、查看node节点名称
[root@k8s-master01 ~]# kubectl get nodes
NAME           STATUS   ROLES    AGE     VERSION
k8s-master01   Ready    master   2d22h   v1.17.5
k8s-node01     Ready    <none>   2d22h   v1.17.5
k8s-node02     Ready    <none>   2d22h   v1.17.5
k8s-node03     Ready    <none>   2d22h   v1.17.5

# 2、查看master节点详细信息：通过观taints察属性，发现master节点默认被打上一个污点。
[root@k8s-master01 ~]# kubectl describe nodes k8s-master01
Name:               k8s-master01
Roles:              master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=k8s-master01
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    projectcalico.org/IPv4Address: 192.168.50.133/24
                    projectcalico.org/IPv4IPIPTunnelAddr: 10.81.32.128
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sat, 17 Jul 2021 16:43:52 +0800
Taints:             node-role.kubernetes.io/master:NoSchedule
........................
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                1 (50%)     0 (0%)
  memory             140Mi (1%)  340Mi (4%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:              <none>
[root@k8s-master01 ~]# 
```

#### 19.4.3 effect定义排斥等级

1、`NoSchedule`不能容忍但仅影响调度过程，已调度上去的pod不受影响，仅对新增加的pod生效。解释说明：表示 k8s 将不会将 Pod 调度到具有该污点的 Node 上 。
2、`PreferNoSchedule` 柔性约束节点现存Pod不受影响，如果实在是没有符合的节点，也可以调度上来。 解释说明：表示 k8s 将不会将 Pod 调度到具有该污点的 Node 上 。
3、`NoExecute` 不能容忍当污点变动时，Pod对象会被驱逐。解释说明：表示 k8s 将不会将 Pod 调度到具有该污点的 Node 上，同时会将 Node 上已经存在的
Pod 驱逐出去。

#### 19.4.4 部署service

1、污点语法

```shell
创建污点:语法规则
kubectl taint nodes node1 key1=value1:NoSchedule

删除污点:语法规则
kubectl taint nodes node1 key1:NoSchedule-
```

2、创建`deploymentdemo.yml`文件

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deploymentdemo
  labels:
    app: deploymentdemo
spec:
  replicas: 5
  template:
    metadata:
      name: deploymentdemo
      labels:
        app: deploymentdemo
    spec:
      containers:
        - name: deploymentdemo
          image: nginx:1.17.10-alpine
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 80
      restartPolicy: Always
  selector:
    matchLabels:
      app: deploymentdemo
```

3、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720163502.png)

```shell
[root@k8s-master01 controller]# ls
deploymentdemo.yml
[root@k8s-master01 controller]# kubectl apply -f .
deployment.apps/deploymentdemo created
# 1、观察每个节点pod运行情况
[root@k8s-master01 controller]# kubectl get pods -o wide
NAME                             READY   STATUS    RESTARTS   AGE   IP              NODE         NOMINATED NODE   READINESS GATES
deploymentdemo-cff9d5c4d-5fq8t   1/1     Running   0          8s    10.81.135.139   k8s-node03   <none>           <none>
deploymentdemo-cff9d5c4d-hptpg   1/1     Running   0          8s    10.81.85.220    k8s-node01   <none>           <none>
deploymentdemo-cff9d5c4d-rsxmt   1/1     Running   0          8s    10.81.58.224    k8s-node02   <none>           <none>
deploymentdemo-cff9d5c4d-t9cqw   1/1     Running   0          8s    10.81.135.140   k8s-node03   <none>           <none>
deploymentdemo-cff9d5c4d-txvsc   1/1     Running   0          8s    10.81.85.221    k8s-node01   <none>           <none>
deploymentdemo-cff9d5c4d-w7qbq   1/1     Running   0          8s    10.81.58.223    k8s-node02   <none>           <none>
# 2、在某一个节点创建污点并驱逐pod
[root@k8s-master01 controller]# kubectl taint nodes k8s-node01 offline=testtaint:NoExecute
node/k8s-node01 tainted
# 3、查看pod被驱逐过程
[root@k8s-master01 controller]# kubectl get pods -o wide
NAME                             READY   STATUS    RESTARTS   AGE   IP              NODE         NOMINATED NODE   READINESS GATES
deploymentdemo-cff9d5c4d-5fq8t   1/1     Running   0          71s   10.81.135.139   k8s-node03   <none>           <none>
deploymentdemo-cff9d5c4d-l9sct   1/1     Running   0          12s   10.81.135.141   k8s-node03   <none>           <none>
deploymentdemo-cff9d5c4d-rsxmt   1/1     Running   0          71s   10.81.58.224    k8s-node02   <none>           <none>
deploymentdemo-cff9d5c4d-t9cqw   1/1     Running   0          71s   10.81.135.140   k8s-node03   <none>           <none>
deploymentdemo-cff9d5c4d-tnlrj   1/1     Running   0          12s   10.81.58.225    k8s-node02   <none>           <none>
deploymentdemo-cff9d5c4d-w7qbq   1/1     Running   0          71s   10.81.58.223    k8s-node02   <none>           <none>
# 4、查看节点污点信息
[root@k8s-master01 controller]# kubectl describe node k8s-node01
Name:               k8s-node01
Roles:              <none>
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=k8s-node01
                    kubernetes.io/os=linux
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    projectcalico.org/IPv4Address: 192.168.50.134/24
                    projectcalico.org/IPv4IPIPTunnelAddr: 10.81.85.192
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sat, 17 Jul 2021 16:44:42 +0800
Taints:             offline=testtaint:NoExecute
Unschedulable:      false
...................
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                250m (25%)  0 (0%)
  memory             0 (0%)      0 (0%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:              <none>
# 5、删除污点
[root@k8s-master01 controller]# kubectl taint nodes k8s-node01 offline=testtaint:NoExecute-
node/k8s-node01 untainted
# 6、删除控制器
[root@k8s-master01 controller]# kubectl delete -f .
deployment.apps "deploymentdemo" deleted
[root@k8s-master01 controller]# 
```

### 19.5 pod容忍度

#### 19.5.1 在Pod定义容忍度

1、等值比较 容忍度与污点在`key`、`value`、`effect`三者完全匹配。

2、存在性判断`key`、`effect`完全匹配，`value`使用空值。

3、一个节点可配置多个污点，一个Pod也可有多个容忍度。

#### 19.5.2 设置污点

```shell
1、在某一个节点创建污点
kubectl taint node k8s-node03 offline=testtaint:NoSchedule

2、查看节点污点信息
kubectl describe nodes k8s-node03
```

#### 19.5.3 部署service

1、创建`deploymentdemo.yml`文件

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deploymentdemo
  labels:
    app: deploymentdemo
spec:
  replicas: 6
  template:
    metadata:
      name: deploymentdemo
      labels:
        app: deploymentdemo
    spec:
      tolerations:
        - key: "offline"
          value: "testtaint"
          effect: "NoSchedule"
          operator: "Equal"
      containers:
        - name: deploymentdemo
          image: nginx:1.17.10-alpine
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 80
      restartPolicy: Always
  selector:
    matchLabels:
      app: deploymentdemo
```

2、通过idea的Remote Host快速将yml文件上传k8s集群进行测试

![](https://guardwhy.oss-cn-beijing.aliyuncs.com/img/docker/images01/20210720163502.png)

```shell
[root@k8s-master01 controller]# ls
deploymentdemo.yml
# 1、部署控制器
[root@k8s-master01 controller]# kubectl apply -f .
deployment.apps/deploymentdemo created
# 2、查看pod详细信息
[root@k8s-master01 controller]# kubectl get pods -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP              NODE         NOMINATED NODE   READINESS GATES
deploymentdemo-7dbdbd5848-7ckk6   1/1     Running   0          12s   10.81.85.224    k8s-node01   <none>           <none>
deploymentdemo-7dbdbd5848-ddftq   1/1     Running   0          12s   10.81.85.225    k8s-node01   <none>           <none>
deploymentdemo-7dbdbd5848-mhxtx   1/1     Running   0          12s   10.81.58.229    k8s-node02   <none>           <none>
deploymentdemo-7dbdbd5848-mwmsq   1/1     Running   0          12s   10.81.58.228    k8s-node02   <none>           <none>
deploymentdemo-7dbdbd5848-sghvv   1/1     Running   0          12s   10.81.135.144   k8s-node03   <none>           <none>
deploymentdemo-7dbdbd5848-tgxfp   1/1     Running   0          12s   10.81.135.145   k8s-node03   <none>           <none>
[root@k8s-master01 controller]# kubectl describe nodes k8s-node03
Name:               k8s-node03
Roles:              <none>
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=k8s-node03
                    kubernetes.io/os=linux
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    projectcalico.org/IPv4Address: 192.168.50.136/24
                    projectcalico.org/IPv4IPIPTunnelAddr: 10.81.135.128
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sat, 17 Jul 2021 16:45:02 +0800
Taints:             offline=testtaint:NoExecute
                    offline=testtaint:NoSchedule
Unschedulable:      false
.....................
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                250m (25%)  0 (0%)
  memory             0 (0%)      0 (0%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:              <none>
# 3、设置污点
[root@k8s-master01 controller]#  kubectl taint nodes k8s-node03 offline=testtaint:NoExecute
node/k8s-node03 tainted
# 4、查看pod详细信息
[root@k8s-master01 controller]# kubectl get pods -o wide
NAME                              READY   STATUS    RESTARTS   AGE   IP             NODE         NOMINATED NODE   READINESS GATES
deploymentdemo-7dbdbd5848-7ckk6   1/1     Running   0          60s   10.81.85.224   k8s-node01   <none>           <none>
deploymentdemo-7dbdbd5848-7k7c7   1/1     Running   0          4s    10.81.85.226   k8s-node01   <none>           <none>
deploymentdemo-7dbdbd5848-ddftq   1/1     Running   0          60s   10.81.85.225   k8s-node01   <none>           <none>
deploymentdemo-7dbdbd5848-j26jh   1/1     Running   0          4s    10.81.58.230   k8s-node02   <none>           <none>
deploymentdemo-7dbdbd5848-mhxtx   1/1     Running   0          60s   10.81.58.229   k8s-node02   <none>           <none>
deploymentdemo-7dbdbd5848-mwmsq   1/1     Running   0          60s   10.81.58.228   k8s-node02   <none>           <none>
# 5、删除污点
[root@k8s-master01 controller]# kubectl taint nodes k8s-node03 offline=testtaint:NoSchedule-
node/k8s-node03 untainted
# 6、删除控制器
[root@k8s-master01 controller]# kubectl delete -f .
deployment.apps "deploymentdemo" deleted
[root@k8s-master01 controller]# 
```



