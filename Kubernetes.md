#  Kubernetes简介

##  来源

bilibili尚硅谷K8S视频：[https://www.bilibili.com/video/BV1GT4y1A756](https://gitee.com/link?target=https%3A%2F%2Fwww.bilibili.com%2Fvideo%2FBV1GT4y1A756)

##  介绍

K8S主要讲的就是Kubernetes，首先Kubernetes首字母为K，末尾为s，中间一共有8个字母，所以简称K8s

##  K8S概念和特性

###  部署发展历程

我们的项目部署也在经历下面的这样一个历程

`传统部署 -> 虚拟化部署时代 -> 容器部署时代`

- **传统部署时代**：早期，组织在物理服务器上运行应用程序。无法为物理服务器中的应用程序定义资源边界，这会导致资源分配问题。例如，如果在物理服务器上运行多个应用程序，则可能会出现-一个应用程序占用大部分资源的情况，结果可能导致其他应用程序的性能下降。--种解决方案是在不同的物理服务器上运行每个应用程序，但是由于资源利用不足而无法扩展，并且组织维护许多物理服务器的成本很高。
- **虚拟化部署时代**：作为解决方案，引入了虚拟化功能，它允许您在单个物理服务器的CPU.上运行多个虚拟机（VM）。虚拟化功能允许应用程序在VM之间隔离，并提供安全级别，因为一一个应用程序的信息不能被另一应用程序自由地访问。因为虚拟化可以轻松地添加或更新应用程序、降低硬件成本等等，所以虚拟化可以更好地利用物理服务器中的资源，并可以实现更好的可伸缩性。每个VM是一台完整的计算机，在虚拟化硬件之上运行所有组件，包括其自己的操作系统。
- **容器部署时代**：容器类似于VM，但是它们具有轻量级的隔离属性，可以在应用程序之间共享操作系统 （OS），因此，容器被认为是轻量级的。容器与VM类似，具有自己的文件系统、CPU、内存、进程空间等。由于它们与基础架构分离，因此可以跨云和OS分发进行移植。

容器因具有许多优势而变得流行起来。下面列出了容器的一些好处：

- 敏捷应用程序的创建和部署：与使用VM镜像相比，提高了容器镜像创建的简便性和效率。
- 持续开发、集成和部署：通过简单的回滚（由于镜像不可变性），提供可靠且频繁的容器镜像构建和部署。
- 关注开发与运维的分离：在构建/时而不是在部署时创建应用程序容器镜像，将应用程序与基础架构分离。
- 可观察性：不仅可以显示操作系统级别的信息和指标，还可以显示应用程序的运行状况和其他指标信号。
- 跨开发、测试和生产的环境一致性：在便携式计算机上与在云中相同地运行。
- 云和操作系统分发的可移植性：可在Ubuntu、RHEL、RHEL、CoreOS、本地、Google Kubernetes Engine和其它任何其它地方运行。
- 以应用程序为中心的管理：提高抽象级别，从在虚拟硬件上运行OS到使用逻辑资源在OS上运行应用程序。
- 松散耦合、分布式、弹性、解放的微服务：应用程序被分解成较小的独立部分，并且可以动态部署和管理-而不是在一台大型单机上器体运行。
- 资源隔离：可预测的应用程序性能。

###  K8S概述

kubernetes，简称K8s，是用8 代替8 个字符“ubernete”而成的缩写。是一个开源的，用于管理云平台中多个主机上的容器化的应用，Kubernetes 的目标是让部署容器化的应用简单并且高效（powerful）,Kubernetes 提供了应用部署，规划，更新，维护的一种机制。

传统的应用部署方式是通过插件或脚本来安装应用。这样做的缺点是应用的运行、配置、管理、所有生存周期将与当前操作系统绑定，这样做并不利于应用的升级更新/回滚等操作，当然也可以通过创建虚拟机的方式来实现某些功能，但是虚拟机非常重，并不利于可移植性。

新的方式是通过部署容器方式实现，每个容器之间互相隔离，每个容器有自己的文件系统，容器之间进程不会相互影响，能区分计算资源。相对于虚拟机，容器能快速部署，由于容器与底层设施、机器文件系统解耦的。

> 总结：
>
> - K8s是谷歌在2014年发布的容器化集群管理系统
> - 使用k8s进行容器化应用部署
> - 使用k8s利于应用扩展
> - k8s目标实施让部署容器化应用更加简洁和高效

Kubernetes 是一个轻便的和可扩展的开源平台，用于管理容器化应用和服务。通过Kubernetes 能够进行应用的自动化部署和扩缩容。在Kubernetes 中，会将组成应用的容器组合成一个逻辑单元以更易管理和发现。

Kubernetes 积累了作为Google 生产环境运行工作负载15 年的经验，并吸收了来自于社区的最佳想法和实践。

###  K8S功能

####  自动装箱

基于容器对应用运行环境的资源配置要求自动部署应用容器

#### 自我修复(自愈能力)

当容器失败时，会对容器进行重启

当所部署的Node节点有问题时，会对容器进行重新部署和重新调度

当容器未通过监控检查时，会关闭此容器直到容器正常运行时，才会对外提供服务

如果某个服务器上的应用不响应了，Kubernetes会自动在其它的地方创建一个

#### 水平扩展

通过简单的命令、用户UI 界面或基于CPU 等资源使用情况，对应用容器进行规模扩大或规模剪裁

> 当我们有大量的请求来临时，我们可以增加副本数量，从而达到水平扩展的效果

#### 服务发现

用户不需使用额外的服务发现机制，就能够基于Kubernetes 自身能力实现服务发现和负载均衡

> 对外提供统一的入口，让它来做节点的调度和负载均衡

####  滚动更新

可以根据应用的变化，对应用容器运行的应用，进行一次性或批量式更新

> 添加应用的时候，不是加进去就马上可以进行使用，而是需要判断这个添加进去的应用是否能够正常使用

#### 版本回退

可以根据应用部署情况，对应用容器运行的应用，进行历史版本即时回退

> 类似于Git中的回滚

#### 密钥和配置管理

在不需要重新构建镜像的情况下，可以部署和更新密钥和应用配置，类似热部署。

#### 存储编排

自动实现存储系统挂载及应用，特别对有状态应用实现数据持久化非常重要

存储系统可以来自于本地目录、网络存储(NFS、Gluster、Ceph 等)、公共云存储服务

#### 批处理

提供一次性任务，定时任务；满足批量数据处理和分析的场景

##  K8S架构组件

###  完整架构图

![](https://img-blog.csdnimg.cn/f38ae8addf8d45709626e5432ae88b44.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/89b2ea4225f74c198af14b44316b6679.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  架构细节

K8S架构主要包含两部分：Master（主控节点）和 node（工作节点）

master节点架构图

![](https://img-blog.csdnimg.cn/136ac533e3d14edebb16e53bbc00ebd9.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

Node节点架构图

![](https://img-blog.csdnimg.cn/e030b8990c5c4deba9d5e0b002599c2e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

k8s 集群控制节点，对集群进行调度管理，接受集群外用户去集群操作请求；

- **master**：主控节点
  - API Server：集群统一入口，以restful风格进行操作，同时交给etcd存储
    - 提供认证、授权、访问控制、API注册和发现等机制
  - scheduler：节点的调度，选择node节点应用部署
  - controller-manager：处理集群中常规后台任务，一个资源对应一个控制器
  - etcd：存储系统，用于保存集群中的相关数据
- **Work node**：工作节点
  - Kubelet：master派到node节点的代表，管理本机容器
    - 一个集群中每个节点上运行的代理，它保证容器都运行在Pod中
    - 负责维护容器的生命周期，同时也负责Volume(CSI) 和 网络(CNI)的管理
  - kube-proxy：提供网络代理，负载均衡等操作
- 容器运行环境【**Container Runtime**】
  - 容器运行环境是负责运行容器的软件
  - Kubernetes支持多个容器运行环境：Docker、containerd、cri-o、rktlet以及任何实现Kubernetes CRI (容器运行环境接口) 的软件。
- fluentd：是一个守护进程，它有助于提升 集群层面日志

##  K8S核心概念

### Pod

- Pod是K8s中最小的单元
- 一组容器的集合
- 共享网络【一个Pod中的所有容器共享同一网络】
- 生命周期是短暂的（服务器重启后，就找不到了）

### Volume

- 声明在Pod容器中可访问的文件目录
- 可以被挂载到Pod中一个或多个容器指定路径下
- 支持多种后端存储抽象【本地存储、分布式存储、云存储】

### Controller

- 确保预期的pod副本数量【ReplicaSet】
- 无状态应用部署【Deployment】
  - 无状态就是指，不需要依赖于网络或者ip
- 有状态应用部署【StatefulSet】
  - 有状态需要特定的条件
- 确保所有的node运行同一个pod 【DaemonSet】
- 一次性任务和定时任务【Job和CronJob】

### Deployment

- 定义一组Pod副本数目，版本等
- 通过控制器【Controller】维持Pod数目【自动回复失败的Pod】
- 通过控制器以指定的策略控制版本【滚动升级、回滚等】

![](https://img-blog.csdnimg.cn/7eb85139074c417f8f7f6077fc6569d8.png)

###  Service

- 定义一组pod的访问规则
- Pod的负载均衡，提供一个或多个Pod的稳定访问地址
- 支持多种方式【ClusterIP、NodePort、LoadBalancer】

![](https://img-blog.csdnimg.cn/565c5d9537a646e4bc71649f601797f5.png)

可以用来组合pod，同时对外提供服务

### Label

label：标签，用于对象资源查询，筛选

![](https://img-blog.csdnimg.cn/94ec7d0e62214fad9fda2d82259cb495.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_15,color_FFFFFF,t_70,g_se,x_16)

###  Namespace

命名空间，逻辑隔离

- 一个集群内部的逻辑隔离机制【鉴权、资源】
- 每个资源都属于一个namespace
- 同一个namespace所有资源不能重复
- 不同namespace可以资源名重复

### API

我们通过Kubernetes的API来操作整个集群

同时我们可以通过 kubectl 、ui、curl 最终发送 http + json/yaml 方式的请求给API Server，然后控制整个K8S集群，K8S中所有的资源对象都可以采用 yaml 或 json 格式的文件定义或描述

如下：使用yaml部署一个nginx的pod

![](https://img-blog.csdnimg.cn/0c54b8a2dd214bdbb5b9f5493803fdce.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  完整流程

![](https://img-blog.csdnimg.cn/6ca27fa7ba08463b85f6af9fd9c561e4.png)

- 通过 Kubectl 提交一个创建RC（Replication Controller）的请求，该请求通过APlserver写入etcd
- 此时Controller Manager通过API Server的监听资源变化的接口监听到此RC事件
- 分析之后，发现当前集群中还没有它所对应的Pod实例
- 于是根据RC里的Pod模板定义一个生成Pod对象，通过APIServer写入etcd
- 此事件被Scheduler发现，它立即执行执行一个复杂的调度流程，为这个新的Pod选定一个落户的Node，然后通过API Server讲这一结果写入etcd中
- 目标Node上运行的Kubelet进程通过APiserver监测到这个"新生的Pod.并按照它的定义，启动该Pod并任劳任怨地负责它的下半生，直到Pod的生命结束
- 随后，我们通过Kubectl提交一个新的映射到该Pod的Service的创建请求
- ControllerManager通过Label标签查询到关联的Pod实例，然后生成Service的Endpoints信息，并通过APIServer写入到etod中，
- 接下来，所有Node上运行的Proxy进程通过APIServer查询并监听Service对象与其对应的Endponts信息，建立一个软件方式的负载均衡器来实现Service访问到后端Pod的流量转发功能

#  搭建K8S集群

##  搭建k8s环境平台规划

### 单master集群

单个master节点，然后管理多个node节点

![](https://img-blog.csdnimg.cn/292cc802a0134b7b94127d4e713129f1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 多master集群

多个master节点，管理多个node节点，同时中间多了一个负载均衡的过程

![](https://img-blog.csdnimg.cn/cdd2f315bc3a48c4a9cf3614d30e71ca.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  服务器硬件配置要求

### 测试环境

master：2核 4G 20G

node： 4核 8G 40G

### 生产环境

master：8核 16G 100G

node： 16核 64G 200G

目前生产部署Kubernetes集群主要有两种方式

###  kubeadm

kubeadm是一个K8S部署工具，提供kubeadm init 和 kubeadm join，用于快速部署Kubernetes集群

官网地址：[点我传送](https://gitee.com/link?target=https%3A%2F%2Fkubernetes.io%2Fzh%2Fdocs%2Fsetup%2Fproduction-environment%2Ftools%2Fkubeadm%2Finstall-kubeadm%2F)

### 二进制包

从github下载发行版的二进制包，手动部署每个组件，组成Kubernetes集群。

Kubeadm降低部署门槛，但屏蔽了很多细节，遇到问题很难排查。如果想更容易可控，推荐使用二进制包部署Kubernetes集群，虽然手动部署麻烦点，期间可以学习很多工作原理，也利于后期维护。

##  Kubeadm部署集群

kubeadm 是官方社区推出的一个用于快速部署kubernetes 集群的工具，这个工具能通过两条指令完成一个kubernetes 集群的部署：

- 创建一个Master 节点kubeadm init
- 将Node 节点加入到当前集群中$ kubeadm join <Master 节点的IP 和端口>

## 安装要求

在开始之前，部署Kubernetes集群机器需要满足以下几个条件

- 一台或多台机器，操作系统为Centos7.X
- 硬件配置：2GB或更多GAM，2个CPU或更多CPU，硬盘30G
- 集群中所有机器之间网络互通
- 可以访问外网，需要拉取镜像
- 禁止swap分区

##  准备环境

| 角色   | IP              |
| ------ | --------------- |
| master | 192.168.208.100 |
| node1  | 192.168.208.101 |
| node2  | 192.168.208.102 |

然后开始在每台机器上执行下面的命令

```
# 关闭防火墙
systemctl stop firewalld
systemctl disable firewalld

# 关闭selinux
# 永久关闭
sed -i 's/enforcing/disabled/' /etc/selinux/config  
# 临时关闭
setenforce 0  

# 关闭swap
# 临时
swapoff -a 
# 永久关闭
sed -ri 's/.*swap.*/#&/' /etc/fstab

# 根据规划设置主机名【master节点上操作】
hostnamectl set-hostname k8smaster
# 根据规划设置主机名【node1节点操作】
hostnamectl set-hostname k8snode1
# 根据规划设置主机名【node2节点操作】
hostnamectl set-hostname k8snode2

# 在master添加hosts
cat >> /etc/hosts << EOF
192.168.208.100 k8smaster
192.168.208.101 k8snode1
192.168.208.102 k8snode2
EOF


# 将桥接的IPv4流量传递到iptables的链
cat > /etc/sysctl.d/k8s.conf << EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
# 生效
sysctl --system  

# 时间同步
yum install ntpdate -y
ntpdate time.windows.com
```

##  安装Docker/kubeadm/kubelet

所有节点安装Docker/kubeadm/kubelet ，Kubernetes默认CRI（容器运行时）为Docker，因此先安装Docker

###  安装Docker

**首先安装wget**

每台虚拟机都需要

```
yum install wget
```

每台机器执行以下命令

```
wget https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo -O /etc/yum.repos.d/docker-ce.repo
yum -y install docker-ce
systemctl enable docker && ststemctl start docker
docker --version
```

配置docker的镜像源

```
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://m5m8ek6r.mirror.aliyuncs.com"]
}
EOF
systemctl daemon-reload
systemctl restart docker
```

配置一下Docker的阿里yum源

```
cat >/etc/yum.repos.d/docker.repo<<EOF
[docker-ce-edge]
name=Docker CE Edge - \$basearch
baseurl=https://mirrors.aliyun.com/docker-ce/linux/centos/7/\$basearch/edge
enabled=1
gpgcheck=1
gpgkey=https://mirrors.aliyun.com/docker-ce/linux/centos/gpg
EOF
```

然后重启docker

```
systemctl restart docker
```

###  添加kubernetes软件源

然后我们还需要配置一下yum的k8s软件源,也要重启

```
cat > /etc/yum.repos.d/kubernetes.repo << EOF
[kubernetes]
name=Kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF
```

### 安装kubeadm，kubelet和kubectl

由于版本更新频繁，这里指定版本号部署：

```
# 安装kubelet、kubeadm、kubectl，同时指定版本
yum install -y kubelet-1.18.0 kubeadm-1.18.0 kubectl-1.18.0
# 设置开机启动
systemctl enable kubelet
```

##  部署Kubernetes Master【master节点】

在 192.168.208.100 执行，也就是master节点

```
kubeadm init --apiserver-advertise-address=192.168.208.100 --image-repository registry.aliyuncs.com/google_containers --kubernetes-version v1.18.0 --service-cidr=10.96.0.0/12  --pod-network-cidr=10.244.0.0/16
```

由于默认拉取镜像地址k8s.gcr.io国内无法访问，这里指定阿里云镜像仓库地址，【执行上述命令会比较慢，因为后台其实已经在拉取镜像了】，我们 docker images 命令即可查看已经拉取的镜像

![](https://img-blog.csdnimg.cn/93475121cedd4a1c82c5da5584d1ad71.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

当我们出现下面的情况时，表示kubernetes的镜像已经安装成功

![](https://img-blog.csdnimg.cn/fca6ac9371e148c0bd522b3b89257379.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

使用kubectl工具 【master节点操作】

根据其给的提示复制命令

![](https://img-blog.csdnimg.cn/0a7b9d80d02b4485b47027560c31c331.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

执行完成后，我们使用下面命令，查看我们正在运行的节点

```
kubectl get nodes
```

![](https://img-blog.csdnimg.cn/872d5b6c4f344ce69e44616833a1e27e.png)

能够看到，目前有一个master节点已经运行了，但是还处于未准备状态

下面我们还需要在Node节点执行其它的命令，将node1和node2加入到我们的master节点上

## 加入Kubernetes Node【Slave节点】

下面我们需要到 node1 和 node2服务器，执行下面的代码向集群添加新节点

执行在kubeadm init输出的kubeadm join命令：

> 注意，以下的命令是在master初始化完成后，每个人的都不一样！！！需要复制自己生成的

```
kubeadm join 192.168.208.100:6443 --token 1xlp7w.3aog2r84s8rwb9m6 \
    --discovery-token-ca-cert-hash sha256:56274fb557b1fe349a7a38a93f930b51c3a0a1c229f5c8e360fd9dc9414d39c6
```

默认token有效期为24小时，当过期之后，该token就不可用了。这时就需要重新创建token，操作如下：

```
kubeadm token create --print-join-command
```

当我们把两个节点都加入进来后，我们就可以去Master节点 执行下面命令查看情况

```
kubectl get node
```

![](https://img-blog.csdnimg.cn/4cfd9c4510534b81bad32284eeffa369.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  部署CNI网络插件

上面的状态还是NotReady，下面我们需要网络插件，来进行联网访问

```
# 下载网络插件配置
wget https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

默认镜像地址无法访问，sed命令修改为docker hub镜像仓库。

```
# 添加
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml

# 查看状态 【kube-system是k8s中的最小单元】
kubectl get pods -n kube-system
```

运行后的结果

![](https://img-blog.csdnimg.cn/760d64760e154554b1e6de8e4cb447c2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/359fc4fccfd747d6a0fb336971df6065.png)

如果上述操作完成后，还存在某个节点处于NotReady状态，可以在Master将该节点删除

```
# master节点将该节点删除

##20210223 yan 查阅资料添加###kubectl drain k8snode1 --delete-local-data --force --ignore-daemonsets

kubectl delete node k8snode1
 
# 然后到k8snode1节点进行重置
 kubeadm reset
# 重置完后在加入
kubeadm join 192.168.177.130:6443 --token 8j6ui9.gyr4i156u30y80xf     --discovery-token-ca-cert-hash sha256:eda1380256a62d8733f4bddf926f148e57cf9d1a3a58fb45dd6e80768af5a500
```

## 测试kubernetes集群

我们都知道K8S是容器化技术，它可以联网去下载镜像，用容器的方式进行启动

在Kubernetes集群中创建一个pod，验证是否正常运行：

```
# 下载nginx 【会联网拉取nginx镜像】
kubectl create deployment nginx --image=nginx
# 查看状态
kubectl get pod
```

如果我们出现Running状态的时候，表示已经成功运行了

![](https://img-blog.csdnimg.cn/3dbbd3a544734df68f9e5766f08a66b7.png)

下面我们就需要将端口暴露出去，让其它外界能够访问

```
# 暴露端口
kubectl expose deployment nginx --port=80 --type=NodePort
# 查看一下对外的端口
kubectl get pod,svc
```

能够看到，我们已经成功暴露了 80端口 到 30529上

![](https://img-blog.csdnimg.cn/7f0b144560e1486985ce800542dbd51b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们到我们的宿主机浏览器上，访问如下地址

```
http://192.168.208.100:30477/
```

发现我们的nginx已经成功启动了

![](https://img-blog.csdnimg.cn/557296d59427435d8351d359115eaebd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

到这里为止，我们就搭建了一个单master的k8s集群

#  使用二进制方式搭建K8S集群

## 注意

**【暂时没有使用二进制方式搭建K8S集群，因此本章节内容不完整... 欢迎小伙伴能补充~】**

## 准备工作

在开始之前，部署Kubernetes集群机器需要满足以下几个条件

- 一台或多台机器，操作系统CentOS 7.x
- 硬件配置：2GB ，2个CPU，硬盘30GB
- 集群中所有机器之间网络互通
- 可以访问外网，需要拉取镜像，如果服务器不能上网，需要提前下载镜像导入节点
- 禁止swap分区

##  准备虚拟机

首先我们准备了两台虚拟机，来进行安装测试

| 主机名       | ip              |
| ------------ | --------------- |
| k8s_2_master | 192.168.208.103 |
| k8s_2_node   | 192.168.208.104 |

## 操作系统的初始化

然后我们需要进行一些系列的初始化操作

```
# 关闭防火墙
systemctl stop firewalld
systemctl disable firewalld

# 关闭selinux
# 永久关闭
sed -i 's/enforcing/disabled/' /etc/selinux/config  
# 临时关闭
setenforce 0  

# 关闭swap
# 临时
swapoff -a 
# 永久关闭
sed -ri 's/.*swap.*/#&/' /etc/fstab

# 根据规划设置主机名【master节点上操作】
hostnamectl set-hostname k8s_2_master
# 根据规划设置主机名【node1节点操作】
hostnamectl set-hostname k8s_2_node1


# 在master添加hosts
cat >> /etc/hosts << EOF
192.168.208.103 k8s_2_master
192.168.208.104 k8s_2_node1
EOF


# 将桥接的IPv4流量传递到iptables的链
cat > /etc/sysctl.d/k8s.conf << EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
# 生效
sysctl --system  

# 时间同步
yum install ntpdate -y
ntpdate time.windows.com
```

## 部署Etcd集群

Etcd是一个分布式键值存储系统，Kubernetes使用Etcd进行数据存储，所以先准备一个Etcd数据库，为了解决Etcd单点故障，应采用集群方式部署，这里使用3台组建集群，可容忍一台机器故障，当然也可以使用5台组件集群，可以容忍2台机器故障

### 自签证书

提到证书，我们想到的就是下面这个情况

![](https://img-blog.csdnimg.cn/dde1888e036e4f2e9df2207d0bab9f0c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

这个https证书，其实就是服务器颁发给网站的，代表这是一个安全可信任的网站。

而在我们K8S集群的内部，其实也是有证书的，如果不带证书，那么访问就会受限

![](https://img-blog.csdnimg.cn/af34a6bbb0f64f9c97d8821e67f608bc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

同时在集群内部 和 外部的访问，我们也需要签发证书

![](https://img-blog.csdnimg.cn/bec54752a9b147f89d62e33136fcfdb4.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

如果我们使用二进制的方式，那么就需要自己手动签发证书。

自签证书：我们可以想象成在一家公司上班，然后会颁发一个门禁卡，同时一般门禁卡有两种，一个是内部员工的门禁卡，和外部访客门禁卡。这两种门禁卡的权限可能不同，员工的门禁卡可以进入公司的任何地方，而访客的门禁卡是受限的，这个门禁卡其实就是自签证书

![](https://img-blog.csdnimg.cn/29a64225a8824525b95b28b80b99e7e1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_18,color_FFFFFF,t_70,g_se,x_16)

###  准备cfssl证书生成工具

cfssl是一个开源的证书管理工具，使用json文件生成证书，相比openssl 更方便使用。找任意一台服务器操作，这里用Master节点。

```
yum install wget
```

```
wget https://pkg.cfssl.org/R1.2/cfssl_linux-amd64
wget https://pkg.cfssl.org/R1.2/cfssljson_linux-amd64
wget https://pkg.cfssl.org/R1.2/cfssl-certinfo_linux-amd64
chmod +x cfssl_linux-amd64 cfssljson_linux-amd64 cfssl-certinfo_linux-amd64
mv cfssl_linux-amd64 /usr/local/bin/cfssl
mv cfssljson_linux-amd64 /usr/local/bin/cfssljson
mv cfssl-certinfo_linux-amd64 /usr/bin/cfssl-certinfo
chmod +x /usr/bin/cfssl*
```

#### 生成 Etcd 证书 （1）自签证书颁发机构（CA） 创建工作目录：

```
mkdir -p ~/TLS/{etcd,k8s}

cd TLS/etcd
```

#### 自签 CA

```
cat > ca-config.json << EOF
{
  "signing": {
    "default": {
      "expiry": "87600h"
    },
    "profiles": {
      "www": {
         "expiry": "87600h",
         "usages": [
            "signing",
            "key encipherment",
            "server auth",
            "client auth"
        ]
      }
    }
  }
}
EOF
```

```
cat > ca-csr.json << EOF
{
    "CN": "etcd CA",
    "key": {
        "algo": "rsa",
        "size": 2048
    },
    "names": [
        {
            "C": "CN",
            "L": "Beijing",
            "ST": "Beijing"
        }
    ]
}
EOF
```

#### 生成证书：

```
cfssl gencert -initca ca-csr.json | cfssljson -bare ca -

ls *pem
```

#### 使用自签 CA 签发 Etcd HTTPS 证书 创建证书申请文件：(修改对应的master和[node](https://so.csdn.net/so/search?q=node&spm=1001.2101.3001.7020)的IP地址)



**到此发现生成证书一直失败，无法解决：Failed to parse input: unexpected end of JSON input**

#  Kubeadm和二进制方式对比

## Kubeadm方式搭建K8S集群

- 安装虚拟机，在虚拟机安装Linux操作系统【3台虚拟机】
- 对操作系统初始化操作
- 所有节点安装Docker、kubeadm、kubelet、kubectl【包含master和slave节点】
  - 安装docker、使用yum，不指定版本默认安装最新的docker版本
  - 修改docker仓库地址，yum源地址，改为阿里云地址
  - 安装kubeadm，kubelet 和 kubectl
    - k8s已经发布最新的1.19版本，可以指定版本安装，不指定安装最新版本
    - `yum install -y kubelet kubeadm kubectl`
- 在master节点执行初始化命令操作
  - `kubeadm init`
  - 默认拉取镜像地址 K8s.gcr.io国内地址，需要使用国内地址
- 安装网络插件(CNI)
  - `kubectl apply -f kube-flannel.yml`
  - 
- 在所有的node节点上，使用join命令，把node添加到master节点上
- 测试kubernetes集群

## 二进制方式搭建K8S集群

- 安装虚拟机和操作系统，对操作系统进行初始化操作
- 生成cfssl 自签证书
  - `ca-key.pem`、`ca.pem`
  - `server-key.pem`、`server.pem`
- 部署Etcd集群
  - 部署的本质，就是把etcd集群交给 systemd 管理
  - 把生成的证书复制过来，启动，设置开机启动
- 为apiserver自签证书，生成过程和etcd类似
- 部署master组件，主要包含以下组件
  - apiserver
  - controller-manager
  - scheduler
  - 交给systemd管理，并设置开机启动
  - 如果要安装最新的1.19版本，下载二进制文件进行安装
- 部署node组件
  - docker
  - kubelet
  - kube-proxy【需要批准kubelet证书申请加入集群】
  - 交给systemd管理组件- 组件启动，设置开机启动
- 批准kubelet证书申请 并加入集群
- 部署CNI网络插件
- 测试Kubernets集群【安装nginx测试】

#  Kubernetes集群管理工具kubectl

## 概述

kubectl是Kubernetes集群的命令行工具，通过kubectl能够对集群本身进行管理，并能够在集群上进行容器化应用的安装和部署

## 命令格式

命令格式如下

```
kubectl [command] [type] [name] [flags]
```

参数

- command：指定要对资源执行的操作，例如create、get、describe、delete
- type：指定资源类型，资源类型是大小写敏感的，开发者能够以单数 、复数 和 缩略的形式

例如：

```
kubectl get pod pod1
kubectl get pods pod1
kubectl get po pod1
```

![](https://img-blog.csdnimg.cn/35ee8f7557d343859c672a550b158912.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_12,color_FFFFFF,t_70,g_se,x_16)

- name：指定资源的名称，名称也是大小写敏感的，如果省略名称，则会显示所有的资源，例如

```
kubectl get pods
```

- flags：指定可选的参数，例如，可用 -s 或者 -server参数指定Kubernetes API server的地址和端口

## 常见命令

### kubectl help 获取更多信息

通过 help命令，能够获取帮助信息

```
# 获取kubectl的命令
kubectl --help

# 获取某个命令的介绍和使用
kubectl get --help
```

### 基础命令

常见的基础命令

| 命令    | 介绍                                           |
| ------- | ---------------------------------------------- |
| create  | 通过文件名或标准输入创建资源                   |
| expose  | 将一个资源公开为一个新的Service                |
| run     | 在集群中运行一个特定的镜像                     |
| set     | 在对象上设置特定的功能                         |
| get     | 显示一个或多个资源                             |
| explain | 文档参考资料                                   |
| edit    | 使用默认的编辑器编辑一个资源                   |
| delete  | 通过文件名，标准输入，资源名称或标签来删除资源 |

### 部署命令

| 命令           | 介绍                                               |
| -------------- | -------------------------------------------------- |
| rollout        | 管理资源的发布                                     |
| rolling-update | 对给定的复制控制器滚动更新                         |
| scale          | 扩容或缩容Pod数量，Deployment、ReplicaSet、RC或Job |
| autoscale      | 创建一个自动选择扩容或缩容并设置Pod数量            |

### 集群管理命令

| 命令         | 介绍                           |
| ------------ | ------------------------------ |
| certificate  | 修改证书资源                   |
| cluster-info | 显示集群信息                   |
| top          | 显示资源(CPU/M)                |
| cordon       | 标记节点不可调度               |
| uncordon     | 标记节点可被调度               |
| drain        | 驱逐节点上的应用，准备下线维护 |
| taint        | 修改节点taint标记              |
|              |                                |

### 故障和调试命令

| 命令         | 介绍                                                         |
| ------------ | ------------------------------------------------------------ |
| describe     | 显示特定资源或资源组的详细信息                               |
| logs         | 在一个Pod中打印一个容器日志，如果Pod只有一个容器，容器名称是可选的 |
| attach       | 附加到一个运行的容器                                         |
| exec         | 执行命令到容器                                               |
| port-forward | 转发一个或多个                                               |
| proxy        | 运行一个proxy到Kubernetes API Server                         |
| cp           | 拷贝文件或目录到容器中                                       |
| auth         | 检查授权                                                     |

### 其它命令

| 命令         | 介绍                                                |
| ------------ | --------------------------------------------------- |
| apply        | 通过文件名或标准输入对资源应用配置                  |
| patch        | 使用补丁修改、更新资源的字段                        |
| replace      | 通过文件名或标准输入替换一个资源                    |
| convert      | 不同的API版本之间转换配置文件                       |
| label        | 更新资源上的标签                                    |
| annotate     | 更新资源上的注释                                    |
| completion   | 用于实现kubectl工具自动补全                         |
| api-versions | 打印受支持的API版本                                 |
| config       | 修改kubeconfig文件（用于访问API，比如配置认证信息） |
| help         | 所有命令帮助                                        |
| plugin       | 运行一个命令行插件                                  |
| version      | 打印客户端和服务版本信息                            |

### 目前使用的命令

```
# 创建一个nginx镜像
kubectl create deployment nginx --image=nginx

# 对外暴露端口
kubectl expose deployment nginx --port=80 --type=NodePort

# 查看资源
kubectl get pod, svc
```

#  Kubernetes集群YAML文件详解

## 概述

k8s 集群中对资源管理和资源对象编排部署都可以通过声明样式（YAML）文件来解决，也就是可以把需要对资源对象操作编辑到YAML 格式文件中，我们把这种文件叫做资源清单文件，通过kubectl 命令直接使用资源清单文件就可以实现对大量的资源对象进行编排部署了。一般在我们开发的时候，都是通过配置YAML文件来部署集群的。

YAML文件：就是资源清单文件，用于资源编排

## YAML文件介绍

### YAML概述

YAML ：仍是一种标记语言。为了强调这种语言以数据做为中心，而不是以标记语言为重点。

YAML 是一个可读性高，用来表达数据序列的格式。

### YAML 基本语法

- 使用空格做为缩进
- 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可
- 冒号逗号后面也要有空格，一般一个
- 低版本缩进时不允许使用Tab 键，只允许使用空格
- 使用#标识注释，从这个字符一直到行尾，都会被解释器忽略
- 使用 --- 表示新的yaml文件开始

###  YAML 支持的数据结构

#### 对象

键值对的集合，又称为映射(mapping) / 哈希（hashes） / 字典（dictionary）

```
# 对象类型：对象的一组键值对，使用冒号结构表示
name: Tom
age: 18

# yaml 也允许另一种写法，将所有键值对写成一个行内对象
hash: {name: Tom, age: 18}
```

#### 数组

```
# 数组类型：一组连词线开头的行，构成一个数组
People
- Tom
- Jack

# 数组也可以采用行内表示法
People: [Tom, Jack]
```

## YAML文件组成部分

主要分为了两部分，一个是控制器的定义 和 被控制的对象

###  控制器的定义

![](https://img-blog.csdnimg.cn/3cd3b4ffc8f640d5b01254f81806ef94.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  被控制的对象

包含一些 镜像，版本、端口等

![](https://img-blog.csdnimg.cn/59d642a61fcc48088bad7363fb1ae00a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  属性说明

在一个YAML文件的控制器定义中，有很多属性名称

| 属性名称   | 介绍       |
| ---------- | ---------- |
| apiVersion | API版本    |
| kind       | 资源类型   |
| metadata   | 资源元数据 |
| spec       | 资源规格   |
| replicas   | 副本数量   |
| selector   | 标签选择器 |
| template   | Pod模板    |
| metadata   | Pod元数据  |
| spec       | Pod规格    |
| containers | 容器配置   |

###  使用kubectl create命令

这种方式一般用于资源没有部署的时候，我们可以直接创建一个YAML配置文件

```
# 尝试运行,并不会真正的创建镜像
kubectl create deployment web --image=nginx -o yaml --dry-run
```

或者我们可以输出到一个文件中

```
kubectl create deployment web --image=nginx -o yaml --dry-run > hello.yaml
ls
```

然后我们就在文件中直接修改即可

![](https://img-blog.csdnimg.cn/fc4cef7304694298869dec70fa9bea46.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  使用kubectl get命令导出yaml文件

使用于已经部署好的项目

可以首先查看一个目前已经部署的镜像

```
kubectl get deploy
```

![](https://img-blog.csdnimg.cn/df00ee51bf2342959a06e3c13e071b36.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

然后我们导出 nginx的配置

```
kubectl get deploy nginx -o=yaml --export > my2.yaml
```

然后会生成一个 `my2.yaml` 的配置文件

#  Kubernetes核心技术Pod

## Pod概述

Pod是K8S系统中可以创建和管理的最小单元，是资源对象模型中由用户创建或部署的最小资源对象模型，也是在K8S上运行容器化应用的资源对象，其它的资源对象都是用来支撑或者扩展Pod对象功能的，比如控制器对象是用来管控Pod对象的，Service或者Ingress资源对象是用来暴露Pod引用对象的，PersistentVolume资源对象是用来为Pod提供存储等等，K8S不会直接处理容器，而是Pod，Pod是由一个或多个container组成。

Pod是Kubernetes的最重要概念，每一个Pod都有一个特殊的被称为 “根容器”的Pause容器。Pause容器对应的镜像属于Kubernetes平台的一部分，除了Pause容器，每个Pod还包含一个或多个紧密相关的用户业务容器。

![](https://img-blog.csdnimg.cn/ed623794c2ba4b1baca6e0a7cb217bc5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  Pod基本概念

- 最小部署的单元
- Pod里面是由一个或多个容器组成【一组容器的集合】
- 一个pod中的容器是共享网络命名空间
- Pod是短暂的
- 每个Pod包含一个或多个紧密相关的用户业务容器

### Pod存在的意义

- 创建容器使用docker，一个docker对应一个容器，一个容器运行一个应用进程
- Pod是多进程设计，运用多个应用程序，也就是一个Pod里面有多个容器，而一个容器里面运行一个应用程序（可以有多个应用程序，只是目前这样设计方便管理）

![](https://img-blog.csdnimg.cn/fcb736244a294bf3889f78cd66a75165.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- Pod的存在是为了亲密性应用
  - 两个应用之间进行交互
  - 网络之间的调用【通过127.0.0.1 或 socket】
  - 两个应用之间需要频繁调用

Pod是在K8S集群中运行部署应用或服务的最小单元，它是可以支持多容器的。Pod的设计理念是支持多个容器在一个Pod中共享网络地址和文件系统，可以通过进程间通信和文件共享这种简单高效的方式组合完成服务。同时Pod对多容器的支持是K8S中最基础的设计理念。在生产环境中，通常是由不同的团队各自开发构建自己的容器镜像，在部署的时候组合成一个微服务对外提供服务。

Pod是K8S集群中所有业务类型的基础，可以把Pod看作运行在K8S集群上的小机器人，不同类型的业务就需要不同类型的小机器人去执行。目前K8S的业务主要可以分为以下几种

- 长期伺服型：long-running
- 批处理型：batch
- 节点后台支撑型：node-daemon
- 有状态应用型：stateful application

上述的几种类型，分别对应的小机器人控制器为：Deployment、Job、DaemonSet 和 StatefulSet (后面将介绍控制器)

##  Pod实现机制

主要有以下两大机制

- 共享网络
- 共享存储

### 共享网络

容器本身之间相互隔离的，一般是通过 **namespace** 和 **group** 进行隔离，那么Pod里面的容器如何实现通信？

关于Pod实现原理，首先会在Pod会创建一个根容器： `pause容器(也叫做info容器)`，然后我们在创建业务容器 【nginx，redis 等】，在我们创建业务容器的时候，会把它添加到 `info容器` 中

通过Pause容器，把其他业务容器加入到 Pause 容器中，让所有业务容器在同一个命名空间内，可以实现网络共享

![](https://img-blog.csdnimg.cn/a60ff990065f4480b14ad130e2798940.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  共享存储

Pod持久化数据，专门存储到某个地方中

![](https://img-blog.csdnimg.cn/7aa30500d4934fafb3324854365fc252.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

使用 Volumn数据卷进行共享存储，案例如下所示

![](https://img-blog.csdnimg.cn/365fa7cdc47d4a5b9a27723805947aed.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  Pod镜像拉取策略

我们以具体实例来说，拉取策略就是 `imagePullPolicy`

![](https://img-blog.csdnimg.cn/17489752c987457e826712789eb1f9d8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_18,color_FFFFFF,t_70,g_se,x_16)

拉取策略主要分为了以下几种

- IfNotPresent：默认值，镜像在宿主机上不存在才拉取
- Always：每次创建Pod都会重新拉取一次镜像
- Never：Pod永远不会主动拉取这个镜像

## Pod资源限制

也就是我们Pod在进行调度的时候，可以对调度的资源进行限制，例如我们限制 Pod调度是使用的资源是 2C4G，那么在调度对应的node节点时，只会占用对应的资源，对于不满足资源的节点，将不会进行调度

本身还是由 Docker 做到

![](https://img-blog.csdnimg.cn/d72964336d4d4e0ab0fd07eec3531edd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 示例

我们在下面的地方进行资源的限制

![](https://img-blog.csdnimg.cn/ccefc105ce2e4e5bbab53dfdc4f03dfb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_15,color_FFFFFF,t_70,g_se,x_16)

这里分了两个部分

- request：表示调度所需的资源
- limits：表示最大所占用的资源

## Pod重启机制

因为Pod中包含了很多个容器，假设某个容器出现问题了，那么就会触发Pod重启机制

![](https://img-blog.csdnimg.cn/3deac433f1fb4ae19030f47f3487f67d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_19,color_FFFFFF,t_70,g_se,x_16)

重启策略主要分为以下三种

- Always：当容器终止退出后，总是重启容器，默认策略 【nginx等，需要不断提供服务】
- OnFailure：当容器异常退出（退出状态码非0）时，才重启容器。
- Never：当容器终止退出，从不重启容器 【批量任务】

##  Pod健康检查

通过容器检查，原来我们使用下面的命令来检查

```
kubectl get pods
```

但是有的时候，程序可能出现了 **Java** 堆内存溢出，程序还在运行，但是不能对外提供服务了，这个时候就不能通过 容器检查来判断服务是否可用了

这个时候就可以使用应用层面的检查

```
# 存活检查，如果检查失败，将杀死容器，根据Pod的restartPolicy【重启策略】来操作
livenessProbe

# 就绪检查，如果检查失败，Kubernetes会把Pod从Service endpoints中剔除
readinessProbe
```

![](https://img-blog.csdnimg.cn/e6c26278754d4728aaa77712109ca44e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_17,color_FFFFFF,t_70,g_se,x_16)

Probe支持以下三种检查方式

- http Get：发送HTTP请求，返回200 - 400 范围状态码为成功
- exec：执行Shell命令返回状态码是0为成功
- tcpSocket：发起TCP Socket建立成功

##  Pod调度策略

```
kubectl get pods  查看
kubectl get pods -o wide  详细查看
```

###  创建Pod流程

- 首先创建一个pod，然后创建一个API Server 和 Etcd【把创建出来的信息存储在etcd中】
- 然后创建 Scheduler，监控API Server是否有新的Pod，如果有的话，会通过调度算法，把pod调度某个node上
- 在node节点，会通过 `kubelet -- apiserver `读取etcd 拿到分配在当前node节点上的pod，然后通过docker创建容器

![](https://img-blog.csdnimg.cn/4226ba276eeb44c58a877548ecb718e7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 影响Pod调度的属性

Pod资源限制对Pod的调度会有影响

#### 根据request找到足够node节点进行调度

![](https://img-blog.csdnimg.cn/8d4233b1338b435e88b7c86a42e4ed00.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_15,color_FFFFFF,t_70,g_se,x_16)

####  节点选择器标签影响Pod调度

![](https://gitee.com/moxi159753/LearningNotes/raw/master/K8S/8_Kubernetes%E6%A0%B8%E5%BF%83%E6%8A%80%E6%9C%AFPod/images/image-20201114202456151.png)

关于节点选择器，其实就是有两个环境，然后环境之间所用的资源配置不同

![](https://img-blog.csdnimg.cn/870dfae6a3f34fdbb464b586db49ba9a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们可以通过以下命令，给我们的节点新增标签，然后节点选择器就会进行调度了

```
kubectl label node k8snode1 env_role=prod

kubectl get nodes k8snode1 --show-labels  查看
```

####  节点亲和性

节点亲和性 **nodeAffinity** 和 之前nodeSelector 基本一样的，根据节点上标签约束来决定Pod调度到哪些节点上

- 硬亲和性：约束条件必须满足
- 软亲和性：尝试满足，不保证

![](https://img-blog.csdnimg.cn/4ad8fc4ef13b4ad1a2cf36c141ed844d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

operator : 支持常用操作符：in、NotIn、Exists、Gt、Lt、DoesNotExists

反亲和性：就是和亲和性刚刚相反，如 NotIn、DoesNotExists等

##  污点和污点容忍

### 概述

nodeSelector 和 NodeAffinity，都是Pod调度到某些节点上，是属于Pod的属性，是在调度的时候实现的。

Taint 污点：节点不做普通分配调度，是节点属性

### 场景

- 专用节点【限制ip】
- 配置特定硬件的节点【固态硬盘】
- 基于Taint驱逐【在node1不放，在node2放】

###  查看污点情况

```
kubectl describe node k8smaster | grep Taint
```

![](https://img-blog.csdnimg.cn/fb8323f8ed824b3d9029acea1cee232b.png)

污点值有三个

- NoSchedule：一定不被调度
- PreferNoSchedule：尽量不被调度【也有被调度的几率】
- NoExecute：不会调度，并且还会驱逐Node已有Pod，比如从node1驱逐到node2

### 为节点添加污点

```
kubectl taint node [node] key=value:污点的三个值
```

举例：

```
kubectl taint node k8snode1 env_role=yes:NoSchedule
```

### 删除污点

```
kubectl taint node k8snode1 env_role:NoSchedule-
```

![](https://img-blog.csdnimg.cn/c4aef7e44ca64b3a9644c19594685dde.png)

###  演示

我们现在创建多个Pod，查看最后分配到Node上的情况

首先我们创建一个 nginx 的pod

```
kubectl create deployment web --image=nginx
```

然后使用命令查看

```
kubectl get pods -o wide
```

![](https://img-blog.csdnimg.cn/96916ffa45fb4d7b9185d0f095dca834.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们可以非常明显的看到，这个Pod已经被分配到 k8snode1 节点上了

下面我们把pod复制5份，在查看情况pod情况

```
kubectl scale deployment web --replicas=5
```

我们可以发现，因为master节点存在污点的情况，所以节点都被分配到了 node1 和 node2节点上

![](https://img-blog.csdnimg.cn/ef7df0b156d344bdac965b91c6f63bf3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们可以使用下面命令，把刚刚我们创建的pod都删除

```
kubectl delete deployment web
kubectl get pods  查看web已经全部删掉
```

现在给了更好的演示污点的用法，我们现在给 node1节点打上污点

```
kubectl taint node k8snode1 env_role=yes:NoSchedule
```

然后我们查看污点是否成功添加

```
kubectl describe node k8snode1 | grep Taint
```

![](https://img-blog.csdnimg.cn/5e3b1278a4e8465c8c5f3e0fde7e0863.png)

然后我们在创建一个 pod

```
# 创建nginx pod
kubectl create deployment web --image=nginx
# 复制五次
kubectl scale deployment web --replicas=5
```

然后我们在进行查看

```
kubectl get pods -o wide
```

我们能够看到现在所有的pod都被分配到了 k8snode2上，因为刚刚我们给node1节点设置了污点

![](https://img-blog.csdnimg.cn/a44144abe46f4e2fa3459dd711de8067.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

最后我们可以删除刚刚添加的污点

```
kubectl taint node k8snode1 env_role:NoSchedule-
kubectl describe node k8snode1 | grep Taint
```

### 污点容忍

污点容忍就是某个节点可能被调度，也可能不被调度

![](https://img-blog.csdnimg.cn/6efda845027e4e169cb4146079fa921f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_12,color_FFFFFF,t_70,g_se,x_16)

这里的key是刚才设置的，比如 key 是 env_role ，而 value 是yes

#  Kubernetes核心技术-Controller

## 内容

- 什么是Controller
- Pod和Controller的关系
- Deployment控制器应用场景
- yaml文件字段说明
- Deployment控制器部署应用
- 升级回滚
- 弹性伸缩

## 什么是Controller

Controller是在集群上管理和运行容器的对象，Controller是实际存在的，Pod是虚拟机的

## Pod和Controller的关系

Pod是通过Controller实现应用的运维，比如弹性伸缩，滚动升级等

Pod 和 Controller之间是通过 label 和 selector 标签来建立关系，同时Controller又被称为控制器工作负载

![](https://img-blog.csdnimg.cn/c750a9599cb247629d8edfe8c6a2c6cc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  Deployment控制器应用

- Deployment控制器可以部署无状态应用
- 管理Pod和ReplicaSet
- 部署，滚动升级等功能
- 应用场景：web服务，微服务

Deployment表示用户对K8S集群的一次更新操作。Deployment是一个比RS( Replica Set, RS) 应用模型更广的 API 对象，可以是创建一个新的服务，更新一个新的服务，也可以是滚动升级一个服务。滚动升级一个服务，实际是创建一个新的RS，然后逐渐将新 RS 中副本数增加到理想状态，将旧RS中的副本数减少到0的复合操作。

这样一个复合操作用一个RS是不好描述的，所以用一个更通用的Deployment来描述。以K8S的发展方向，未来对所有长期伺服型的业务的管理，都会通过Deployment来管理。

##  Deployment部署应用

之前我们也使用Deployment部署过应用，如下代码所示

```
kubectrl create deployment web --image=nginx
```

但是上述代码不是很好的进行复用，因为每次我们都需要重新输入代码，所以我们都是通过YAML进行配置

但是我们可以尝试使用上面的代码创建一个镜像【只是尝试，不会创建】

```
kubectl create deployment web --image=nginx --dry-run -o yaml > web.yaml
```

然后输出一个yaml配置文件 `web.yml` ，配置文件如下所示

```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: web
  name: web
spec:
  replicas: 1
  selector:
    matchLabels:
      app: web
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: web
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```

我们看到的 selector 和 label 就是我们Pod 和 Controller之间建立关系的桥梁

![](https://img-blog.csdnimg.cn/1ad3d92fa00b4edda62c1e71a342c3c7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_11,color_FFFFFF,t_70,g_se,x_16)

###  使用YAML创建Pod

通过刚刚的代码，我们已经生成了YAML文件，下面我们就可以使用该配置文件快速创建Pod镜像了

```
kubectl apply -f web.yaml
```

![](https://img-blog.csdnimg.cn/85b7ff9e8f7b4c6ba760651d43a14118.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

但是因为这个方式创建的，我们只能在集群内部进行访问，所以我们还需要对外暴露端口

```
kubectl expose deployment web --port=80 --type=NodePort --target-port=80 --name=web1
```

关于上述命令，有几个参数

- --port：就是我们内部的端口号
- --target-port：是pod上的端口
- --name：名称
- --type：类型

指定了 --type=NodePort，随机分配30000 以上的端口号

同理，我们一样可以导出对应的配置文件

```
kubectl expose deployment web --port=80 --type=NodePort --target-port=80 --name=web1 -o yaml > web1.yaml
```

得到的web1.yaml如下所示

```
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: "2020-11-16T02:26:53Z"
  labels:
    app: web
  managedFields:
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:metadata:
        f:labels:
          .: {}
          f:app: {}
      f:spec:
        f:externalTrafficPolicy: {}
        f:ports:
          .: {}
          k:{"port":80,"protocol":"TCP"}:
            .: {}
            f:port: {}
            f:protocol: {}
            f:targetPort: {}
        f:selector:
          .: {}
          f:app: {}
        f:sessionAffinity: {}
        f:type: {}
    manager: kubectl
    operation: Update
    time: "2020-11-16T02:26:53Z"
  name: web2
  namespace: default
  resourceVersion: "113693"
  selfLink: /api/v1/namespaces/default/services/web2
  uid: d570437d-a6b4-4456-8dfb-950f09534516
spec:
  clusterIP: 10.104.174.145
  externalTrafficPolicy: Cluster
  ports:
  - nodePort: 32639
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: web
  sessionAffinity: None
  type: NodePort
status:
  loadBalancer: {}
```

然后我们可以通过下面的命令来查看对外暴露的服务

```
kubectl get pods,svc
```

![](https://img-blog.csdnimg.cn/d7ce4c2c00ac45439a5e9f9e16efe398.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

然后我们访问对应的url，即可看到 nginx了 `http://192.168.208.100:30044/`

##  升级回滚和弹性伸缩

- 升级： 假设从版本为1.14 升级到 1.15 ，这就叫应用的升级【升级可以保证服务不中断】
- 回滚：从版本1.15 变成 1.14，这就叫应用的回滚
- 弹性伸缩：我们根据不同的业务场景，来改变Pod的数量对外提供服务，这就是弹性伸缩

### 应用升级和回滚

首先删掉所有创建的pod。我们先创建一个 1.14版本的Pod

打开之前创建的 web.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: web
  name: web
spec:
  replicas: 1
  selector:
    matchLabels:
      app: web
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: web
    spec:
      containers:
      - image: nginx:1.14
        name: nginx
        resources: {}
status: {}
```

指定nginx版本为1.14，然后开始创建我们的Pod

![](https://img-blog.csdnimg.cn/3f5df926722f4983b8b0b46e798f7d32.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```
kubectl apply -f nginx.yaml
```

同时，我们使用docker images命令，就能看到我们成功拉取到了一个 1.14版本的镜像

![](https://img-blog.csdnimg.cn/4e7b9638a195451faf2aad2afcc185c5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

随机分配的节点

我们使用下面的命令，可以将nginx从 1.14 升级到 1.15

```
kubectl set image deployment web nginx=nginx:1.15
```

在我们执行完命令后，能看到升级的过程

```
kubectl get pods（master节点）
docker images(在对应节点)
```

![](https://img-blog.csdnimg.cn/31c2ffd5d61b470e9d4a99df0ae058ba.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

此时镜像拉取到node1节点

- 首先是开始的nginx 1.14版本的Pod在运行，然后 1.15版本的在创建
- 然后在1.15版本创建完成后，就会暂停1.14版本
- 最后把1.14版本的Pod移除，完成我们的升级

我们在下载 1.15版本，容器就处于ContainerCreating状态，然后下载完成后，就用 1.15版本去替换1.14版本了，这么做的好处就是：升级可以保证服务不中断

![](https://img-blog.csdnimg.cn/9d0cbbac471a402c8014c5c675747e83.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们到我们的node1节点上，查看我们的 docker images;

能够看到，我们已经成功拉取到了 1.15版本的nginx了

####  查看升级状态

下面可以，查看升级状态

```
kubectl rollout status deployment web
```

![](https://img-blog.csdnimg.cn/8c04f4f3add74b1992634cfcbc6680fb.png)

#### 查看历史版本

我们还可以查看历史版本

```
kubectl rollout history deployment web
```

#### 应用回滚

我们可以使用下面命令，完成回滚操作，也就是回滚到上一个版本

```
kubectl rollout undo deployment web
```

然后我们就可以查看状态

```
kubectl rollout status deployment web
```

![](https://img-blog.csdnimg.cn/f98104f6890f438a99cb13b33e1a732a.png)

同时我们还可以回滚到指定版本

```
kubectl rollout history deployment web
kubectl rollout undo deployment web --to-revision=2
```

![](https://img-blog.csdnimg.cn/45a600ee35e74d8891ae532c470fca51.png)

### 弹性伸缩

弹性伸缩，也就是我们通过命令一下创建多个副本

```
kubectl scale deployment web --replicas=10
```

能够清晰看到，我们一下创建了10个副本

![](https://img-blog.csdnimg.cn/ed04afd8625b4d98803f57731bfefc9d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_19,color_FFFFFF,t_70,g_se,x_16)

#  Kubernetes核心技术Service

## 前言

前面我们了解到 Deployment 只是保证了支撑服务的微服务Pod的数量，但是没有解决如何访问这些服务的问题。一个Pod只是一个运行服务的实例，随时可能在一个节点上停止，在另一个节点以一个新的IP启动一个新的Pod，因此不能以确定的IP和端口号提供服务。

要稳定地提供服务需要服务发现和负载均衡能力。服务发现完成的工作，是针对客户端访问的服务，找到对应的后端服务实例。在K8S集群中，客户端需要访问的服务就是Service对象。每个Service会对应一个集群内部有效的虚拟IP，集群内部通过虚拟IP访问一个服务。

在K8S集群中，微服务的负载均衡是由kube-proxy实现的。kube-proxy是k8s集群内部的负载均衡器。它是一个分布式代理服务器，在K8S的每个节点上都有一个；这一设计体现了它的伸缩性优势，需要访问服务的节点越多，提供负载均衡能力的kube-proxy就越多，高可用节点也随之增多。与之相比，我们平时在服务器端使用反向代理作负载均衡，还要进一步解决反向代理的高可用问题。

## Service存在的意义

###  防止Pod失联【服务发现】

因为Pod每次创建都对应一个IP地址，而这个IP地址是短暂的，每次随着Pod的更新都会变化，假设当我们的前端页面有多个Pod时候，同时后端也多个Pod，这个时候，他们之间的相互访问，就需要通过注册中心，拿到Pod的IP地址，然后去访问对应的Pod

![](https://img-blog.csdnimg.cn/0e0849967c634e93877378d863ec3fd4.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  定义Pod访问策略【负载均衡】

页面前端的Pod访问到后端的Pod，中间会通过Service一层，而Service在这里还能做负载均衡，负载均衡的策略有很多种实现策略，例如：

- 随机
- 轮询
- 响应比

![](https://img-blog.csdnimg.cn/1930d20612a044efa1fd8db67667cb30.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_15,color_FFFFFF,t_70,g_se,x_16)

## Pod和Service的关系

这里Pod 和 Service 之间还是根据 label 和 selector 建立关联的 【和Controller一样】

![](https://img-blog.csdnimg.cn/1a7f691fc9494c6bab4cf43dfb2e6cf1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们在访问service的时候，其实也是需要有一个ip地址，这个ip肯定不是pod的ip地址，而是 虚拟IP `vip`

##  Service常用类型

Service常用类型有三种

- ClusterIp：集群内部访问
- NodePort：对外访问应用使用
- LoadBalancer：对外访问应用使用，公有云

### 举例

我们可以导出一个文件 包含service的配置信息

```
kubectl expose deployment web --port=80 --target-port=80 --dry-run -o yaml > service.yaml
```

service.yaml 如下所示

```
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: web
  name: web
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: web
status:
  loadBalancer: {}
```

如果我们没有做设置的话，默认使用的是第一种方式 ClusterIP，也就是只能在集群内部使用，我们可以添加一个type字段，用来设置我们的service类型,名字也改为web1

```yaml
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: web
  name: web1
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: web
  type: NodePort
status:
  loadBalancer: {}
```

修改完命令后，我们使用创建一个pod

```
kubectl apply -f service.yaml
```

然后能够看到，已经成功修改为 NodePort类型了

```yaml
kubectl get svc
```

最后剩下的一种方式就是LoadBalanced：对外访问应用使用公有云

node一般是在内网进行部署，而外网一般是不能访问到的，那么如何访问的呢？

- 找到一台可以通过外网访问机器，安装nginx，反向代理
- 手动把可以访问的节点添加到nginx中

如果我们使用LoadBalancer，就会有负载均衡的控制器，类似于nginx的功能，就不需要自己添加到nginx上

#  Kubernetes控制器Controller详解

## Statefulset

Statefulset主要是用来部署有状态应用

对于StatefulSet中的Pod，每个Pod挂载自己独立的存储，如果一个Pod出现故障，从其他节点启动一个同样名字的Pod，要挂载上原来Pod的存储继续以它的状态提供服务。

### 无状态应用

我们原来使用 deployment，部署的都是无状态的应用，那什么是无状态应用？

- 认为Pod都是一样的
- 没有顺序要求
- 不考虑应用在哪个node上运行
- 能够进行随意伸缩和扩展

### 有状态应用

上述的因素都需要考虑到

- 让每个Pod独立的
- 让每个Pod独立的，保持Pod启动顺序和唯一性
- 唯一的网络标识符，持久存储
- 有序，比如mysql中的主从

适合StatefulSet的业务包括数据库服务MySQL 和 PostgreSQL，集群化管理服务Zookeeper、etcd等有状态服务

StatefulSet的另一种典型应用场景是作为一种比普通容器更稳定可靠的模拟虚拟机的机制。传统的虚拟机正是一种有状态的宠物，运维人员需要不断地维护它，容器刚开始流行时，我们用容器来模拟虚拟机使用，所有状态都保存在容器里，而这已被证明是非常不安全、不可靠的。

使用StatefulSet，Pod仍然可以通过漂移到不同节点提供高可用，而存储也可以通过外挂的存储来提供 高可靠性，StatefulSet做的只是将确定的Pod与确定的存储关联起来保证状态的连续性。

### 部署有状态应用

需要一个无头service， ClusterIP：none（类似Mysql主从的主）

这里就需要使用 StatefulSet部署有状态应用

![](https://img-blog.csdnimg.cn/c46c141685f847c49c261e40a7591fdc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_11,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/030cba3a9ff940d89f76a984db1b0671.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_16,color_FFFFFF,t_70,g_se,x_16)

创建pod

```
kubectl apply -f sys.yaml
kubectl get pods
```

然后通过查看pod，能否发现每个pod都有唯一的名称

![](https://img-blog.csdnimg.cn/fcff0fb3feb14c1b84a0e0c87d0a48fd.png)

然后我们在查看service，发现是无头的service

```
kubectl get svc
```

![](https://img-blog.csdnimg.cn/c14c9120e4d24e98b557468376edd1c1.png)

statefulset 与 deployment 的区别：

- statefulset：根据主机名 + 按照一定规则生成域名

每个pod有唯一的主机名，并且有唯一的域名

- 格式：主机名称.service名称.名称空间.svc.cluster.local
- 举例：nginx-statefulset-0.default.svc.cluster.local

##  DaemonSet

DaemonSet 即后台支撑型服务，主要是用来部署守护进程

长期伺服型和批处理型的核心在业务应用，可能有些节点运行多个同类业务的Pod，有些节点上又没有这类的Pod运行；而后台支撑型服务的核心关注点在K8S集群中的节点(物理机或虚拟机)，要保证每个节点上都有一个此类Pod运行。节点可能是所有集群节点，也可能是通过 nodeSelector选定的一些特定节点。典型的后台支撑型服务包括：存储、日志和监控等。在每个节点上支撑K8S集群运行的服务。

守护进程在我们每个节点上，运行的是同一个pod，新加入的节点也运行同一个pod

- 例子：在每个node节点安装数据采集工具

首先删掉前面的，可以不删

![](https://img-blog.csdnimg.cn/d3e32aff98894301b272bb46239cfe38.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_14,color_FFFFFF,t_70,g_se,x_16)

这里是一个FileBeat镜像，主要是为了做日志采集工作

![](https://img-blog.csdnimg.cn/a9a58a02cf564acf82ef16d1e5cb6606.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_18,color_FFFFFF,t_70,g_se,x_16)

进入某个 Pod里面，进入

```
kubectl exec -it ds-test-cbk6v bash
```

通过该命令后，我们就能看到我们内部收集的日志信息了

![](https://img-blog.csdnimg.cn/3fe6ea8184a941aa9268b5358efdc047.png)

##  Job和CronJob

一次性任务 和 定时任务

- 一次性任务：一次性执行完就结束
- 定时任务：周期性执行

Job是K8S中用来控制批处理型任务的API对象。批处理业务与长期伺服业务的主要区别就是批处理业务的运行有头有尾，而长期伺服业务在用户不停止的情况下永远运行。Job管理的Pod根据用户的设置把任务成功完成就自动退出了。成功完成的标志根据不同的 spec.completions 策略而不同：单Pod型任务有一个Pod成功就标志完成；定数成功行任务保证有N个任务全部成功；工作队列性任务根据应用确定的全局成功而标志成功。

### Job

Job也即一次性任务

![](https://img-blog.csdnimg.cn/cf982b154b9445d0bd72b3cb5deeeb47.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

使用下面命令，能够看到目前已经存在的Job

```
kubectl create -f job.yaml
kubectl get jobs
docker pull perl（在对应节点）
```

![](https://img-blog.csdnimg.cn/da494194924d4ce7a902a4f3ac9ba751.png)

在计算完成后，通过命令查看，能够发现该任务已经完成

![](https://img-blog.csdnimg.cn/4c2525d82e3d49dfb1b20865d3b5cf69.png)

我们可以通过查看日志，查看到一次性任务的结果

```
kubectl logs pi-qpqff
```

![](https://img-blog.csdnimg.cn/5591a32f59144bd98f17a2d4991df915.png)

然后将这个文件删掉

```
kubectl delete -f job.yaml
kubectl get jobs  查看
```

###  CronJob

定时任务，cronjob.yaml如下所示

![](https://img-blog.csdnimg.cn/ebeba7e012c1430ca44feccee2cf48f6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

这里面的命令就是每个一段时间，这里是通过 cron 表达式配置的，通过 schedule字段

然后下面命令就是每个一段时间输出

我们首先用上述的配置文件，创建一个定时任务

```
kubectl apply -f cronjob.yaml
```

创建完成后，我们就可以通过下面命令查看定时任务

```
kubectl get cronjobs
```

![](https://img-blog.csdnimg.cn/7883416d7e46439b889909f8aa9a249c.png)

我们可以通过日志进行查看

```
kubectl logs hello-1599100140-wkn79
```

![](https://img-blog.csdnimg.cn/0894d890a21649edb55bcf8d82dc1979.png)

然后每次执行，就会多出一个 pod

![](https://img-blog.csdnimg.cn/b8e0fa6be13c423cbe027478735238d4.png)

##  删除svc 和 statefulset

使用下面命令，可以删除我们添加的svc 和 statefulset

```
kubectl delete svc web

kubectl delete statefulset --all
```

#  Kubernetes配置管理

## Secret

Secret的主要作用就是加密数据，然后存在etcd里面，让Pod容器以挂载Volume方式进行访问

场景：用户名 和 密码进行加密

一般场景的是对某个字符串进行base64编码 进行加密

```
echo -n 'admin' | base64
```

![](https://img-blog.csdnimg.cn/7cd075a35bb04f08a0083d84db4923ea.png)

### 变量形式挂载到Pod

- 创建secret加密数据的yaml文件 secret.yaml

![](https://img-blog.csdnimg.cn/74bf7a6ed6b24631bec89954ba6547db.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_12,color_FFFFFF,t_70,g_se,x_16)

然后使用下面命令创建一个pod

```
kubectl create -f secret.yaml
```

通过get命令查看

```
kubectl get pods
```

实际上是叫mysecret

![](https://img-blog.csdnimg.cn/9e0fe49fc43e435a8618abaff4558ac8.png)

另一个yaml文件，里面对应了前面的mysecret

![](https://img-blog.csdnimg.cn/4b192fd6b26f42a89f555b8c8381e71c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_15,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/d80dcbf6f8dc48dda7ac65540bb55c62.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_14,color_FFFFFF,t_70,g_se,x_16)

创建 secret-val.yaml 文件，复制内容，注意不要少了字母

```
kubectl apply -f secret-val.yaml
kubectl get pods
```

![](https://img-blog.csdnimg.cn/9e0fe49fc43e435a8618abaff4558ac8.png)

然后我们通过下面的命令，进入到我们的容器内部

```
kubectl exec -it mypod bash
```

然后我们就可以输出我们的值，这就是以变量的形式挂载到我们的容器中

```
# 输出用户
echo $SECRET_USERNAME
# 输出密码
echo $SECRET_PASSWORD
```

最后如果我们要删除这个Pod，就可以使用这个命令

```
kubectl delete -f secret-val.yaml
kubectl delete secret --all
```

###  数据卷形式挂载

首先我们创建一个 secret-val.yaml 文件

![](https://img-blog.csdnimg.cn/0fb8da958e0d407aa28a8ebef7fa807b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_16,color_FFFFFF,t_70,g_se,x_16)

然后创建我们的 Pod

```
# 根据配置创建容器
kubectl apply -f secret-val.yaml
# 进入容器
kubectl exec -it mypod bash
# 查看
ls /etc/foo
```

![](https://img-blog.csdnimg.cn/7396351ecf0848cbbc255cf87a2fab3e.png)

![](https://img-blog.csdnimg.cn/e880044a12674047815e4aa611615d9d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  ConfigMap

ConfigMap作用是存储不加密的数据到etcd中，让Pod以变量或数据卷Volume挂载到容器中

应用场景：配置文件

### 创建配置文件

首先我们需要创建一个配置文件 `redis.properties`

```
redis.port=127.0.0.1
redis.port=6379
redis.password=123456
```

### 创建ConfigMap

我们使用命令创建configmap

```
kubectl create configmap redis-config --from-file=redis.properties
```

然后查看详细信息

```
kubectl get cm
kubectl describe cm redis-config
```

![](https://img-blog.csdnimg.cn/8ff00ce2ec6442479cb5f84990acb668.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  Volume数据卷形式挂载

首先我们需要创建一个 `cm.yaml`

![](https://img-blog.csdnimg.cn/22406d706dc84f858c19634b55c1a4fe.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

然后使用该yaml创建我们的pod

```
# 创建
kubectl apply -f cm.yaml
# 查看
kubectl get pods
```

![](https://img-blog.csdnimg.cn/39daa74e3c2b4e5fb9919fff7c8f0420.png)

最后我们通过日志就可以查看结果输出了

```
kubectl logs mypod
```

![](https://img-blog.csdnimg.cn/790a572fa5c941bc94de066c20d549d4.png)

###  以变量的形式挂载Pod

首先我们也有一个 myconfig.yaml文件，声明变量信息，然后以configmap创建

![](https://img-blog.csdnimg.cn/e8945dd0299a4080b13b443b4d547505.png)

然后我们就可以创建我们的配置文件

```
# 创建pod
kubectl apply -f myconfig.yaml
# 获取
kubectl get cm
```

![](https://img-blog.csdnimg.cn/b33260fcd84e4d94be4b6a9cac042599.png)

然后我们创建完该pod后，我们就需要在创建一个 config-var.yaml 来使用我们的配置信息

![](https://img-blog.csdnimg.cn/3e24e14c6d954db9908f3d48efd35545.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```
kubectl apply -f config-var.yaml
kubectl get cm
kubectl get pods
```

最后我们查看输出

```
kubectl logs mypod
```

![](https://img-blog.csdnimg.cn/145e7837610d4229b3948ebb8f1b94cd.png)

#  Kubernetes集群安全机制

## 概述

当我们访问K8S集群时，需要经过三个步骤完成具体操作

- 认证
- 鉴权【授权】
- 准入控制

进行访问的时候，都需要经过 apiserver， apiserver做统一协调，比如门卫

- 访问过程中，需要证书、token、或者用户名和密码
- 如果访问pod需要serviceAccount

![](https://img-blog.csdnimg.cn/dfedb05971a04936bc6975b42bfe0c60.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  认证

对外不暴露8080端口，只能内部访问，对外使用的端口6443

客户端身份认证常用方式

- https证书认证，基于ca证书
- http token认证，通过token来识别用户
- http基本认证，用户名 + 密码认证

### 鉴权

基于RBAC进行鉴权操作

基于角色访问控制

### 准入控制

就是准入控制器的列表，如果列表有请求内容就通过，没有的话 就拒绝

## RBAC介绍

基于角色的访问控制，为某个角色设置访问内容，然后用户分配该角色后，就拥有该角色的访问权限

![](https://img-blog.csdnimg.cn/d7feef77da6e4f3db1f0b411245fee60.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

k8s中有默认的几个角色

- role：特定命名空间访问权限
- ClusterRole：所有命名空间的访问权限

角色绑定

- roleBinding：角色绑定到主体
- ClusterRoleBinding：集群角色绑定到主体

主体

- user：用户
- group：用户组
- serviceAccount：服务账号

## RBAC实现鉴权

- 创建命名空间

### 创建命名空间

我们可以首先查看已经存在的命名空间

```
kubectl get namespace
```

![](https://img-blog.csdnimg.cn/010c630924034ec885430cd120ef734c.png)

然后我们创建一个自己的命名空间 roledemo

```
kubectl create ns roledemo
```

### 命名空间创建Pod

为什么要创建命名空间？因为如果不创建命名空间的话，默认是在default下

```
kubectl run nginx --image=nginx -n roledemo
```

### 创建角色

我们通过 rbac-role.yaml进行创建,把这里面的namespace改为刚刚创建的roledemo

![](https://img-blog.csdnimg.cn/8a6ccd1b6cf64008a72ad1e0f26ce19e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

tip：这个角色只对pod 有 get、list，watch权限

然后通过 yaml创建我们的role

```
# 创建
kubectl apply -f rbac-role.yaml
# 查看
kubectl get role -n roledemo
```

![](https://img-blog.csdnimg.cn/27c4d1a69d734dedbdf003ca1374a6da.png)

###  创建角色绑定

我们还是通过 role-rolebinding.yaml 的方式，来创建我们的角色绑定

namespace改为刚刚创建的roledemo

![](https://img-blog.csdnimg.cn/ac5ec2911c42415db462e8c7120597e9.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

然后创建我们的角色绑定

```
# 创建角色绑定
kubectl apply -f rbac-rolebinding.yaml
# 查看角色绑定
kubectl get role, rolebinding -n roledemo
```

![](https://img-blog.csdnimg.cn/f42967257d894f159ab3fcab5b588b6b.png)

###  使用证书识别身份

```
创建目录
mkdir mary
```

我们首先得有一个 rbac-user.sh 证书脚本

这个脚本文件复制到mary目录下，vi查看

![](https://img-blog.csdnimg.cn/3e43a89bf0f14b7d965f806a676d8bca.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_10,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/95477a3293524f06b3cce9cf98aa76a3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

这里面的 IP 需要更改为自己的 IP

这里包含了很多证书文件，在TSL目录下，需要复制过来

```
cp /root/TLS/k8s/ca* ./   可能没有，因为没有用二进制搭建集群
```

![](https://img-blog.csdnimg.cn/721ec45f533f4d64a1aa9c0299c2a6ed.png)

通过下面命令执行我们的脚本

```
base rbac-user.sh
```

最后我们进行测试

```
# 用get命令查看 pod 【有权限】
kubectl get pods -n roledemo
# 用get命令查看svc 【没权限】
kubectl get svc -n roledmeo
```

![](https://img-blog.csdnimg.cn/2d00686efb3e4ea3bec81bc4e565f9b5.png)

#  Kubernetes核心技术Ingress

## 前言

原来我们需要将端口号对外暴露，通过 ip + 端口号就可以进行访问

原来是使用Service中的NodePort来实现

- 在每个节点上都会启动端口
- 在访问的时候通过任何节点，通过ip + 端口号就能实现访问

但是NodePort还存在一些缺陷

- 因为端口不能重复，所以每个端口只能使用一次，一个端口对应一个应用
- 实际访问中都是用域名，根据不同域名跳转到不同端口服务中

## Ingress和Pod关系

pod 和 ingress 是通过service进行关联的，而ingress作为统一入口，由service关联一组pod中

![](https://img-blog.csdnimg.cn/4acaf25211e540a484983affd06518d6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 首先service就是关联我们的pod
- 然后ingress作为入口，首先需要到service，然后发现一组pod
- 发现pod后，就可以做负载均衡等操作

## Ingress工作流程

在实际的访问中，我们都是需要维护很多域名， a.com 和 b.com

然后不同的域名对应的不同的Service，然后service管理不同的pod

![](https://img-blog.csdnimg.cn/a89234a1f7794685aed0ce1f2bd315fd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

需要注意，ingress不是内置的组件，需要我们单独的安装

## 使用Ingress

步骤如下所示

- 部署ingress Controller【需要下载官方的】
- 创建ingress规则【对哪个Pod、名称空间配置规则】

### 创建Nginx Pod

创建一个nginx应用，然后对外暴露端口

```
# 创建pod
kubectl create deployment web --image=nginx
# 查看
kubectl get pods
kubectl get deploy
```

对外暴露端口

```
kubectl expose deployment web --port=80 --target-port=80 --type:NodePort
```

### 部署 ingress controller

下面我们来通过yaml的方式，部署我们的ingress，配置文件如下所示(不完整)

![](https://img-blog.csdnimg.cn/24d445e442f9401db6a213b9bc140539.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

这个文件里面，需要注意的是 hostNetwork: true，改成ture是为了让后面访问到

通过这种方式，其实我们在外面就能访问，这里还需要在外面添加一层

```
kubectl apply -f ingress-con.yaml
```

![](https://img-blog.csdnimg.cn/3cddfb7bf5314f83a5b721851c2b6939.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

最后通过下面命令，查看是否成功部署 ingress

```
kubectl get pods -n ingress-nginx
```

![](https://img-blog.csdnimg.cn/f5f57a6bfa714ed3b860c92a607ab743.png)

### 创建ingress规则文件

创建ingress规则文件，ingress-h.yaml

```
kubectl apply -f ingress-h.yaml
```

![](https://img-blog.csdnimg.cn/7c6f416585284db6a161333b0e2140e5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  添加域名访问规则

在windows 的 hosts文件，添加域名访问规则【因为我们没有域名解析，所以只能这样做】

![](https://img-blog.csdnimg.cn/d866a2b15d6648758143bab030d105d9.png)

最后通过域名就能访问

```
kubectl get ing
```

![](https://img-blog.csdnimg.cn/2539312c028a42bbb2c7d8e38527b2f6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

#  Kubernetes核心技术Helm

Helm就是一个包管理工具【类似于npm】

![](https://img-blog.csdnimg.cn/02c663dc80da4ed5a9ac0130aae4ec18.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  为什么引入Helm

首先在原来项目中都是基于yaml文件来进行部署发布的，而目前项目大部分微服务化或者模块化，会分成很多个组件来部署，每个组件可能对应一个deployment.yaml,一个service.yaml,一个Ingress.yaml还可能存在各种依赖关系，这样一个项目如果有5个组件，很可能就有15个不同的yaml文件，这些yaml分散存放，如果某天进行项目恢复的话，很难知道部署顺序，依赖关系等，而所有这些包括

- 基于yaml配置的集中存放
- 基于项目的打包
- 组件间的依赖

但是这种方式部署，会有什么问题呢？

- 如果使用之前部署单一应用，少数服务的应用，比较合适
- 但如果部署微服务项目，可能有几十个服务，每个服务都有一套yaml文件，需要维护大量的yaml文件，版本管理特别不方便

Helm的引入，就是为了解决这个问题

- 使用Helm可以把这些YAML文件作为整体管理
- 实现YAML文件高效复用
- 使用helm应用级别的版本管理

## Helm介绍

Helm是一个Kubernetes的包管理工具，就像Linux下的包管理器，如yum/apt等，可以很方便的将之前打包好的yaml文件部署到kubernetes上。

Helm有三个重要概念

- helm：一个命令行客户端工具，主要用于Kubernetes应用chart的创建、打包、发布和管理
- Chart：应用描述，一系列用于描述k8s资源相关文件的集合
- Release：基于Chart的部署实体，一个chart被Helm运行后将会生成对应的release，将在K8S中创建出真实的运行资源对象。也就是应用级别的版本管理
- Repository：用于发布和存储Chart的仓库

## Helm组件及架构

Helm采用客户端/服务端架构，有如下组件组成

- Helm CLI是Helm客户端，可以在本地执行
- Tiller是服务器端组件，在Kubernetes集群上运行，并管理Kubernetes应用程序
- Repository是Chart仓库，Helm客户端通过HTTP协议来访问仓库中Chart索引文件和压缩包

![](https://img-blog.csdnimg.cn/dde55480e88741eea3accc8a1ea9f165.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  Helm v3变化

2019年11月13日，Helm团队发布了Helm v3的第一个稳定版本

该版本主要变化如下

- 架构变化
  - 最明显的变化是Tiller的删除
  - V3版本删除Tiller
  - relesase可以在不同命名空间重用

V3之前

![](https://img-blog.csdnimg.cn/af02b51cfbc64463a5eb7cc263c9c0af.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

V3版本

![](https://img-blog.csdnimg.cn/1390d2c3f6f34cd89e8fd438594eeebe.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  helm配置

首先我们需要去 [官网下载](https://gitee.com/link?target=https%3A%2F%2Fhelm.sh%2Fdocs%2Fintro%2Fquickstart%2F)

- 第一步，[下载helm](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Fhelm%2Fhelm%2Freleases)安装压缩文件，上传到linux系统中（此处使用v3.3.3）

- 第二步，解压helm压缩文件，把解压后的helm目录复制到 usr/bin 目录中

  ![](https://img-blog.csdnimg.cn/df7455b456e44b3281a221479efe4a60.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  ```
  mv helm /usr/bin
  ```

- 使用命令：helm

我们都知道yum需要配置yum源，那么helm就就要配置helm源

## helm仓库

添加仓库

```
helm repo add 仓库名  仓库地址
```

例如

```
# 配置微软源
helm repo add stable http://mirror.azure.cn/kubernetes/charts
# 配置阿里源
helm repo add aliyun https://kubernetes.oss-cn-hangzhou.aliyuncs.com/charts

# 更新
helm repo update
```

然后可以查看我们添加的仓库地址

```
# 查看全部
helm repo list
# 查看某个
helm search repo stable
```

![](https://img-blog.csdnimg.cn/5b47a0abfdaf4f9398e96c30ee8bb86a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

或者可以删除我们添加的源,现在就保留stable

```
helm repo remove aliyun
```

## helm基本命令

- chart install
- chart upgrade
- chart rollback

## 使用helm快速部署应用

### 使用命令搜索应用

首先我们使用命令，搜索我们需要安装的应用

```
# 搜索 weave仓库
helm search repo weave
```

![](https://img-blog.csdnimg.cn/5fe890b62e214727991d9cc7a62a23eb.png)

###  根据搜索内容选择安装

搜索完成后，使用命令进行安装

```
helm install 安装之后名称 搜索之后应用名称
helm install ui stable/weave-scope
```

可以通过下面命令，来下载yaml文件【如果】

```
kubectl apply -f weave-scope.yaml
```

安装完成后，通过下面命令即可查看

```
查看安装之后的状态
helm list
```

![](https://img-blog.csdnimg.cn/298d71c7572744c8a71f55fd7dcc4e1c.png)

同时可以通过下面命令，查看更新具体的信息

```
helm status 安装之后的名称
helm status ui
```

但是我们通过查看 svc状态，发现没有对象暴露端口

![](https://img-blog.csdnimg.cn/1837c3a6f9a449bb9d2763f62119b3f3.png)

所以我们需要修改service的yaml文件，添加NodePort

```
kubectl edit svc ui-weave-scope
```

![](https://img-blog.csdnimg.cn/f540eea17bb84185b0c07d7680cd0713.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_16,color_FFFFFF,t_70,g_se,x_16)

这样就可以对外暴露端口了

![](https://img-blog.csdnimg.cn/641d9f74eddf43269d8fec3e252699bb.png)

然后我们通过 ip + 32185 即可访问

### 如果自己创建Chart

使用命令，自己创建Chart

```
helm create chart名称
helm create mychart
```

创建完成后，进入mychart文件夹，我们就能看到在当前文件夹下，创建了一个 mychart目录

![](https://img-blog.csdnimg.cn/c0348c1d65fe4be2b613847608358781.png)

####  目录格式

- templates：编写yaml文件存放到这个目录
- values.yaml：存放的是全局的yaml文件
- chart.yaml：当前chart属性配置信息

### 在templates文件夹创建两个文件

先把里面所有内容删掉

```
cd templates
ls
rm -rf *
```

我们创建以下两个

- deployment.yaml
- service.yaml

我们可以通过下面命令创建出yaml文件

```
# 导出deployment.yaml
kubectl create deployment web1 --image=nginx --dry-run -o yaml > deployment.yaml
# 导出service.yaml 【可能需要创建 deployment，不然会报错】
kubectl expose deployment web1 --port=80 --target-port=80 --type=NodePort --dry-run -o yaml > service.yaml
因为没有deployment web1，所以service.yaml里面是没东西的
创建web1
kubectl create deployment web1 --image=nginx
kubectl get pods
kubectl expose deployment web1 --port=80 --target-port=80 --type=NodePort --dry-run -o yaml > service.yaml
再删掉web1
kubectl delete deployment web1
```

### 安装mychart

执行命令创建

```
cd  先到最外层目录
helm install web1 mychart
kubectl get pods
kubectl get svc  web1的service也有了
```

![](https://img-blog.csdnimg.cn/d7004c3bf44747c8a504a95238504bb1.png)

###  应用升级

当我们修改了mychart中的东西后，就可以进行升级操作

```
helm upgrade web1 mychart
```

## chart模板使用

通过传递参数，动态渲染模板，yaml内容动态从传入参数生成

![](https://img-blog.csdnimg.cn/b8a5a9e31eec436598fe2b5037ca5065.png)

刚刚我们创建mychart的时候，看到有values.yaml文件，这个文件就是一些全局的变量，然后在templates中能取到变量的值，下面我们可以利用这个，来完成动态模板

- 在values.yaml定义变量和值
- 具体yaml文件，获取定义变量值
- yaml文件中大题有几个地方不同
  - image
  - tag
  - label
  - port
  - replicas 副本数

### 定义变量和值

在values.yaml定义变量和值

![](https://img-blog.csdnimg.cn/f8b85bc4e6c3458a92d6289cb3ff89b9.png)

###  获取变量和值

我们通过表达式形式 使用全局变量 `{{ .Values.变量名称}}`

还有一种比较常见的：`{{ .Release.Name}}` 表示取到当前版本的名称 ，每次生成名字都不一样

修改templates目录中的 deployment.yaml

![](https://img-blog.csdnimg.cn/3fb1bde2585b4f56a53779fd877b6647.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_14,color_FFFFFF,t_70,g_se,x_16)

修改templates 目录中的 service.yaml

![](https://img-blog.csdnimg.cn/30f0d1e7685c4e43a9ac2f084989316c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  安装应用

在我们修改完上述的信息后，就可以尝试的创建应用了

```
cd 要在最外面的目录
helm install --dry-run web2 mychart
真正运行
helm install web2 mychart
kubectl get pods
kubectl get svc
```

![](https://img-blog.csdnimg.cn/953b3b3c27344f1caf53c6a6231e2dc1.png)

#  Kubernetes持久化存储

## 前言

之前我们有提到数据卷：`emptydir` ，是本地存储，pod重启，数据就不存在了，需要对数据持久化存储

对于数据持久化存储【pod重启，数据还存在】，有两种方式

- nfs：网络存储【通过一台服务器来存储】

##  步骤

### 持久化服务器上操作

- 找一台新的服务器nfs服务端，安装nfs，此处使用k8s_2_node
- 设置挂载路径

使用命令安装nfs

```
yum install -y nfs-utils
```

首先创建存放数据的目录

```
mkdir -p /data/nfs
```

设置挂载路径

```
# 打开文件
vim /etc/exports
# 添加如下内容
/data/nfs *(rw,no_root_squash)
```

执行完成后，即部署完我们的持久化服务器

### Node节点上操作

然后需要在k8s集群node节点上安装nfs，这里需要在 node1 和 node2节点上安装

```
yum install -y nfs-utils
```

执行完成后，会自动帮我们挂载上

### 启动nfs服务端

下面我们回到nfs服务端，启动我们的nfs服务

```
# 启动服务
systemctl start nfs
# 或者使用以下命令进行启动
service nfs-server start
查看
ps -ef | grep nfs
```

![](https://img-blog.csdnimg.cn/34db8f843d1242d48603f06a2105bea6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_19,color_FFFFFF,t_70,g_se,x_16)

###  K8s集群部署应用

最后我们在k8s集群上部署应用，使用nfs持久化存储，在master节点

```
# 创建一个pv文件
mkdir pv
# 进入
cd pv
vi nfs-nginx.yaml
```

然后创建一个yaml文件 `nfs-nginx.yaml`

![](https://img-blog.csdnimg.cn/934ef7c0ca544eaab526df867b77525a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_18,color_FFFFFF,t_70,g_se,x_16)

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-dep1
spec:
  replicas: 1
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
        image: nginx
        volumeMounts:
        - name: wwwroot
          mountPath: /usr/share/nginx/html
        ports:
        - containerPort: 80
      volumes:
        - name: wwwroot
          nfs:
            server: 192.168.208.104
            path: /data/nfs
```

通过这个方式，就挂载到了刚刚我们的nfs数据节点下的 /data/nfs 目录

最后就变成了： /usr/share/nginx/html -> 192.168.208.104/data/nfs 内容是对应的

我们通过这个 yaml文件，创建一个pod

```
kubectl apply -f nfs-nginx.yaml
```

创建完成后，我们也可以查看日志

```
kubectl describe pod nginx-dep1-6bf4f64bbc-8zdnf
```

![](https://img-blog.csdnimg.cn/de43b7d776b444c79f21ea13a70196e4.png)

可以看到，我们的pod已经成功创建出来了，同时下图也是出于Running状态

![](https://img-blog.csdnimg.cn/d2f9680c49084f26a8272ef38a866ec3.png)

下面我们就可以进行测试了，比如现在nfs服务节点上添加数据，然后在看数据是否存在 pod中

```
# 进入pod中查看
kubectl exec -it nginx-dep1-6bf4f64bbc-8zdnf bash
```

刚开始  ls  /usr/share/nginx/html（设置的挂载目录），刚开始为空

接着我们去nfs服务端，到 /data/nfs 目录下新建 index.html，此时再回到master查看就有了

![](https://img-blog.csdnimg.cn/5eb7bc25b42243a995911ed3c85cb858.png)

接下来暴露端口

```
刚开始看service没有
kubectl get svc
kubectl expose deployment nginx-dep1 --port=80 --target-port=80 --type=NodePort
此时通过端口访问，本来是默认nginx的页面，但是现在我们更改为了index.html
要对应节点和端口号
```



## PV和PVC

对于上述的方式，我们都知道，我们的ip 和端口是直接放在我们的容器上的，这样管理起来可能不方便

![](https://img-blog.csdnimg.cn/27386a35ec374d529645cb697876eb52.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_18,color_FFFFFF,t_70,g_se,x_16)

所以这里就需要用到 pv 和 pvc的概念了，方便我们配置和管理我们的 ip 地址等元信息

PV：持久化存储，对存储的资源进行抽象，对外提供可以调用的地方【生产者】

PVC：用于调用，不需要关心内部实现细节【消费者】

PV 和 PVC 使得 K8S 集群具备了存储的逻辑抽象能力。使得在配置Pod的逻辑里可以忽略对实际后台存储 技术的配置，而把这项配置的工作交给PV的配置者，即集群的管理者。存储的PV和PVC的这种关系，跟 计算的Node和Pod的关系是非常类似的；PV和Node是资源的提供者，根据集群的基础设施变化而变 化，由K8s集群管理员配置；而PVC和Pod是资源的使用者，根据业务服务的需求变化而变化，由K8s集 群的使用者即服务的管理员来配置。

### 实现流程

- PVC绑定PV
- 定义PVC
- 定义PV【数据卷定义，指定数据存储服务器的ip、路径、容量和匹配模式】

### 举例

在master节点 pv 目录创建一个 pvc.yaml

![](https://img-blog.csdnimg.cn/b2f533f4def146d08bf411b0578c2254.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_19,color_FFFFFF,t_70,g_se,x_16)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-dep1
spec:
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
        image: nginx
        volumeMounts:
        - name: wwwroot
          mountPath: /usr/share/nginx/html
        ports:
        - containerPort: 80
      volumes:
        - name: wwwroot
          persistentVolumeClaim:
            claimName: my-pvc
```

第一部分是定义一个 deployment，做一个部署

- 副本数：3
- 挂载路径
- 调用：是通过pvc的模式

然后定义pvc

![](https://img-blog.csdnimg.cn/59c0ece16670427a99b619affbcd454a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_19,color_FFFFFF,t_70,g_se,x_16)

```yaml
---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage:  5Gi
```

然后执行

```
kubectl apply -f pvc.yaml
kubectl get pods
```

![](https://img-blog.csdnimg.cn/78d0996404654acea10cbe281cac14b2.png)

然后在创建一个 `pv.yaml`

![](https://img-blog.csdnimg.cn/5860f108c48f45a6a738d9f1acdc0967.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_17,color_FFFFFF,t_70,g_se,x_16)

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteMany
  nfs:
    path: /data/nfs
    server: 192.168.208.104
```

然后就可以创建pod了

```
kubectl apply -f pv.yaml
```

然后我们就可以通过下面命令，查看我们的 pv 和 pvc之间的绑定关系

```
kubectl get pv, pvc
kubectl get pods
```

![](https://img-blog.csdnimg.cn/aae31741f15849f482e05f296fe97505.png)

到这里为止，我们就完成了我们 pv 和 pvc的绑定操作，通过之前的方式，进入pod中查看内容

```
kubect exec -it nginx-dep1-xxx bash  随便选一个进去试试
```

然后查看 /usr/share/nginx.html

![](https://img-blog.csdnimg.cn/de44f25ce2c742bdbd66df5fc0da5a59.png)

也同样能看到刚刚的内容，其实这种操作和之前我们的nfs是一样的，只是多了一层pvc绑定pv的操作

#  Kubernetes集群资源监控

## 概述

### 监控指标

一个好的系统，主要监控以下内容

- 集群监控
  - 节点资源利用率
  - 节点数
  - 运行Pods
- Pod监控
  - 容器指标
  - 应用程序【程序占用多少CPU、内存】

### 监控平台

使用普罗米修斯【prometheus】 + Grafana 搭建监控平台

- prometheus【定时搜索被监控服务的状态】
  - 开源的
  - 监控、报警、数据库
  - 以HTTP协议周期性抓取被监控组件状态
  - 不需要复杂的集成过程，使用http接口接入即可
- Grafana
  - 开源的数据分析和可视化工具
  - 支持多种数据源

![](https://img-blog.csdnimg.cn/8ba2e157bd154c6990f27e5c09610f44.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  部署prometheus

首先在master节点创建一个文件夹

```
mkdir pgmonitor
cd pgmonitor
mkdir grafana
mkdir prometheus
```

![](https://img-blog.csdnimg.cn/471bd1b6b0df4076a69b9edf254e7e0f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

首先需要部署一个守护进程

创建一个node-exporter.yaml

```
vi node-exporter.yaml
```

```yaml
---
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: node-exporter
  namespace: kube-system
  labels:
    k8s-app: node-exporter
spec:
  selector:
    matchLabels:
      k8s-app: node-exporter
  template:
    metadata:
      labels:
        k8s-app: node-exporter
    spec:
      containers:
      - image: prom/node-exporter
        name: node-exporter
        ports:
        - containerPort: 9100
          protocol: TCP
          name: http
---
apiVersion: v1
kind: Service
metadata:
  labels:
    k8s-app: node-exporter
  name: node-exporter
  namespace: kube-system
spec:
  ports:
  - name: http
    port: 9100
    nodePort: 31672
    protocol: TCP
  type: NodePort
  selector:
    k8s-app: node-exporter
```

然后执行下面命令部署

```
kubectl create -f node-exporter.yaml
```

执行完，发现会报错

![](https://img-blog.csdnimg.cn/d82fba5907f04656a678c3c24b0e7e4a.png)

这是因为版本不一致的问题，因为发布的正式版本，而这个属于测试版本

所以我们找到第一行，然后把内容修改为如下所示

```
# 修改前
apiVersion: extensions/v1beta1
# 修改后 【正式版本发布后，测试版本不能使用】
apiVersion: apps/v1
```

创建完成后的效果

![](https://img-blog.csdnimg.cn/f9e8be41ae02416b8b32efd1e8d4d152.png)

然后通过yaml的方式部署prometheus

![](https://img-blog.csdnimg.cn/bb55ce6385844555911204b0d661da4e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_13,color_FFFFFF,t_70,g_se,x_16)

- configmap：定义一个configmap：存储一些配置文件【不加密】
- prometheus.deploy.yaml：部署一个deployment【包括端口号，资源限制】
- prometheus.svc.yaml：对外暴露的端口
- rbac-setup.yaml：分配一些角色的权限

### rbac文件

```yaml
# cat rbac-setup.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: prometheus
rules:
- apiGroups: [""]
  resources:
  - nodes
  - nodes/proxy
  - services
  - endpoints
  - pods
  verbs: ["get", "list", "watch"]
- apiGroups:
  - extensions
  resources:
  - ingresses
  verbs: ["get", "list", "watch"]
- nonResourceURLs: ["/metrics"]
  verbs: ["get"]
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: prometheus
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: prometheus
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: prometheus
subjects:
- kind: ServiceAccount
  name: prometheus
  namespace: kube-system
```

### 以configmap的形式管理prometheus组件的配置文件

```yaml
# cat configmap.yaml 
apiVersion: v1
kind: ConfigMap
metadata:
  name: prometheus-config
  namespace: kube-system
data:
  prometheus.yml: |
    global:
      scrape_interval:     15s
      evaluation_interval: 15s
    scrape_configs:

    - job_name: 'kubernetes-apiservers'
      kubernetes_sd_configs:
      - role: endpoints
      scheme: https
      tls_config:
        ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
      relabel_configs:
      - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_service_name, __meta_kubernetes_endpoint_port_name]
        action: keep
        regex: default;kubernetes;https

    - job_name: 'kubernetes-nodes'
      kubernetes_sd_configs:
      - role: node
      scheme: https
      tls_config:
        ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
      relabel_configs:
      - action: labelmap
        regex: __meta_kubernetes_node_label_(.+)
      - target_label: __address__
        replacement: kubernetes.default.svc:443
      - source_labels: [__meta_kubernetes_node_name]
        regex: (.+)
        target_label: __metrics_path__
        replacement: /api/v1/nodes/${1}/proxy/metrics

    - job_name: 'kubernetes-cadvisor'
      kubernetes_sd_configs:
      - role: node
      scheme: https
      tls_config:
        ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
      relabel_configs:
      - action: labelmap
        regex: __meta_kubernetes_node_label_(.+)
      - target_label: __address__
        replacement: kubernetes.default.svc:443
      - source_labels: [__meta_kubernetes_node_name]
        regex: (.+)
        target_label: __metrics_path__
        replacement: /api/v1/nodes/${1}/proxy/metrics/cadvisor

    - job_name: 'kubernetes-service-endpoints'
      kubernetes_sd_configs:
      - role: endpoints
      relabel_configs:
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_scrape]
        action: keep
        regex: true
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_scheme]
        action: replace
        target_label: __scheme__
        regex: (https?)
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_path]
        action: replace
        target_label: __metrics_path__
        regex: (.+)
      - source_labels: [__address__, __meta_kubernetes_service_annotation_prometheus_io_port]
        action: replace
        target_label: __address__
        regex: ([^:]+)(?::\d+)?;(\d+)
        replacement: $1:$2
      - action: labelmap
        regex: __meta_kubernetes_service_label_(.+)
      - source_labels: [__meta_kubernetes_namespace]
        action: replace
        target_label: kubernetes_namespace
      - source_labels: [__meta_kubernetes_service_name]
        action: replace
        target_label: kubernetes_name

    - job_name: 'kubernetes-services'
      kubernetes_sd_configs:
      - role: service
      metrics_path: /probe
      params:
        module: [http_2xx]
      relabel_configs:
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_probe]
        action: keep
        regex: true
      - source_labels: [__address__]
        target_label: __param_target
      - target_label: __address__
        replacement: blackbox-exporter.example.com:9115
      - source_labels: [__param_target]
        target_label: instance
      - action: labelmap
        regex: __meta_kubernetes_service_label_(.+)
      - source_labels: [__meta_kubernetes_namespace]
        target_label: kubernetes_namespace
      - source_labels: [__meta_kubernetes_service_name]
        target_label: kubernetes_name

    - job_name: 'kubernetes-ingresses'
      kubernetes_sd_configs:
      - role: ingress
      relabel_configs:
      - source_labels: [__meta_kubernetes_ingress_annotation_prometheus_io_probe]
        action: keep
        regex: true
      - source_labels: [__meta_kubernetes_ingress_scheme,__address__,__meta_kubernetes_ingress_path]
        regex: (.+);(.+);(.+)
        replacement: ${1}://${2}${3}
        target_label: __param_target
      - target_label: __address__
        replacement: blackbox-exporter.example.com:9115
      - source_labels: [__param_target]
        target_label: instance
      - action: labelmap
        regex: __meta_kubernetes_ingress_label_(.+)
      - source_labels: [__meta_kubernetes_namespace]
        target_label: kubernetes_namespace
      - source_labels: [__meta_kubernetes_ingress_name]
        target_label: kubernetes_name

    - job_name: 'kubernetes-pods'
      kubernetes_sd_configs:
      - role: pod
      relabel_configs:
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
        action: keep
        regex: true
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
        action: replace
        target_label: __metrics_path__
        regex: (.+)
      - source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
        action: replace
        regex: ([^:]+)(?::\d+)?;(\d+)
        replacement: $1:$2
        target_label: __address__
      - action: labelmap
        regex: __meta_kubernetes_pod_label_(.+)
      - source_labels: [__meta_kubernetes_namespace]
        action: replace
        target_label: kubernetes_namespace
      - source_labels: [__meta_kubernetes_pod_name]
        action: replace
        target_label: kubernetes_pod_name
```

### Prometheus deployment 文件

```yaml
# cat prometheus.deploy.yml 
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    name: prometheus-deployment
  name: prometheus
  namespace: kube-system
spec:
  replicas: 1
  selector:
    matchLabels:
      app: prometheus
  template:
    metadata:
      labels:
        app: prometheus
    spec:
      containers:
      - image: prom/prometheus:v2.0.0
        name: prometheus
        command:
        - "/bin/prometheus"
        args:
        - "--config.file=/etc/prometheus/prometheus.yml"
        - "--storage.tsdb.path=/prometheus"
        - "--storage.tsdb.retention=24h"
        ports:
        - containerPort: 9090
          protocol: TCP
        volumeMounts:
        - mountPath: "/prometheus"
          name: data
        - mountPath: "/etc/prometheus"
          name: config-volume
        resources:
          requests:
            cpu: 100m
            memory: 100Mi
          limits:
            cpu: 500m
            memory: 2500Mi
      serviceAccountName: prometheus    
      volumes:
      - name: data
        emptyDir: {}
      - name: config-volume
        configMap:
          name: prometheus-config
```

### Prometheus service文件

```yaml
# cat prometheus.svc.yml 
---
kind: Service
apiVersion: v1
metadata:
  labels:
    app: prometheus
  name: prometheus
  namespace: kube-system
spec:
  type: NodePort
  ports:
  - port: 9090
    targetPort: 9090
    nodePort: 30003
  selector:
    app: prometheus
```

下面我们进入目录下，首先部署 rbac-setup.yaml

```
cd prometheus
kubectl create -f rbac-setup.yaml
```

![](https://img-blog.csdnimg.cn/66b32207c1744f25acb30c0e88f0fe69.png)

然后分别部署

```
# 部署configmap
kubectl create -f configmap.yaml
# 部署deployment
kubectl create -f prometheus.deploy.yml
# 部署svc
kubectl create -f prometheus.svc.yml
```

部署完成后，我们使用下面命令查看

```
kubectl get pods -n kube-system
```

![](https://img-blog.csdnimg.cn/09dba6e882a8419495582b6216d508c3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_16,color_FFFFFF,t_70,g_se,x_16)

在我们部署完成后，即可看到 prometheus 的 pod了，然后通过下面命令，能够看到对应的端口

```
kubectl get svc -n kube-system
```

![](https://img-blog.csdnimg.cn/35e9a47b2477467ab8896228d0609469.png)

通过这个，我们可以看到 `prometheus` 对外暴露的端口为 30003，访问页面即可对应的图形化界面

```
http://192.168.208.101:30003
```

![](https://img-blog.csdnimg.cn/03f8324027e946c6a3a43ef5b68ca8a5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

在上面我们部署完prometheus后，我们还需要来部署grafana

### grafana deployment配置文件\

```yaml
# cat grafana-deploy.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-core
  namespace: kube-system
  labels:
    app: grafana
    component: core
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
      component: core
  template:
    metadata:
      labels:
        app: grafana
        component: core
    spec:
      containers:
      - image: grafana/grafana:4.2.0
        name: grafana-core
        imagePullPolicy: IfNotPresent
        # env:
        resources:
          # keep request = limit to keep this container in guaranteed class
          limits:
            cpu: 100m
            memory: 100Mi
          requests:
            cpu: 100m
            memory: 100Mi
        env:
          # The following env variables set up basic auth twith the default admin user and admin password.
          - name: GF_AUTH_BASIC_ENABLED
            value: "true"
          - name: GF_AUTH_ANONYMOUS_ENABLED
            value: "false"
          # - name: GF_AUTH_ANONYMOUS_ORG_ROLE
          #   value: Admin
          # does not really work, because of template variables in exported dashboards:
          # - name: GF_DASHBOARDS_JSON_ENABLED
          #   value: "true"
        readinessProbe:
          httpGet:
            path: /login
            port: 3000
          # initialDelaySeconds: 30
          # timeoutSeconds: 1
        volumeMounts:
        - name: grafana-persistent-storage
          mountPath: /var
      volumes:
      - name: grafana-persistent-storage
        emptyDir: {}
```

### grafana service配置文件

```yaml
# cat grafana-svc.yaml 
apiVersion: v1
kind: Service
metadata:
  name: grafana
  namespace: kube-system
  labels:
    app: grafana
    component: core
spec:
  type: NodePort
  ports:
    - port: 3000
  selector:
    app: grafana
    component: core
```

### grafana ingress配置文件

```yaml
# cat grafana-ing.yaml 
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
   name: grafana
   namespace: kube-system
spec:
  rules:
  - host: k8s.grafana
    http:
      paths:
      - path: /
        backend:
         serviceName: grafana
         servicePort: 3000
```

创建

```
kubectl create -f grafana-deploy.yaml
```

然后执行完后，发现下面的问题

```
error: unable to recognize "grafana-deploy.yaml": no matches for kind "Deployment" in version "extensions/v1beta1"
```

我们需要修改如下内容

```yaml
# 修改
apiVersion: apps/v1

# 添加selector
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
      component: core
```

修改完成后，我们继续执行上述代码

```
# 创建deployment
kubectl create -f grafana-deploy.yaml
# 创建svc
kubectl create -f grafana-svc.yaml
# 创建 ing
kubectl create -f grafana-ing.yaml
```

我们能看到，我们的grafana正在

![](https://img-blog.csdnimg.cn/db21326eed0246f1aa677ece6abbb87f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  配置数据源

下面我们需要开始打开 Grafana，然后配置数据源，导入数据显示模板

```
kubectl get svc -n kube-system
```

![](https://img-blog.csdnimg.cn/f86acd1834c2468ca076358f98fd9c64.png)

我们可以通过 ip + 30431 访问我们的 grafana 图形化页面

![](https://img-blog.csdnimg.cn/f288c8f2a63743b5a6ab96d74df407d6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

然后输入账号和密码：admin admin

进入后，我们就需要配置 prometheus 的数据源,这里的ip 是查看svc的内部IP

![](https://img-blog.csdnimg.cn/cfd2277e8d134690bbef108a86d5de44.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

和 对应的IP【这里IP是我们的ClusterIP】

![](https://img-blog.csdnimg.cn/40b66007e91e466b9d5f878be1c045ac.png)

### 设置显示数据的模板

选择Dashboard，导入我们的模板

![](https://img-blog.csdnimg.cn/968c134138b846e0b9af7bceb3b74368.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_14,color_FFFFFF,t_70,g_se,x_16)

然后输入 315 号模板

![](https://img-blog.csdnimg.cn/89ab805f17594e36b68668ef81021c86.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

然后选择 prometheus数据源 mydb，导入即可

![](https://img-blog.csdnimg.cn/95e36a83b109484281e717759eab493a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

导入后的效果如下所示

![](https://img-blog.csdnimg.cn/5546df691aca43c8a498093586a0a1ec.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

#  Kubernetes搭建高可用集群

## 前言

之前我们搭建的集群，只有一个master节点，当master节点宕机的时候，通过node将无法继续访问，而master主要是管理作用，所以整个集群将无法提供服务

![](https://img-blog.csdnimg.cn/267d4bd79ace4b77a47dc7ff0792ff6b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  高可用集群

下面我们就需要搭建一个多master节点的高可用集群，不会存在单点故障问题

但是在node 和 master节点之间，需要存在一个 LoadBalancer组件，作用如下：

- 负载
- 检查master节点的状态

![](https://img-blog.csdnimg.cn/6e653ec19c2e48f9bf8b540e69e64bf9.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

对外有一个统一的VIP：虚拟ip来对外进行访问

## 高可用集群技术细节

高可用集群技术细节如下所示：

![](https://img-blog.csdnimg.cn/e357d15e50544e588d9b9101c67484ba.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- keepalived：配置虚拟ip，检查节点的状态
- haproxy：负载均衡服务【类似于nginx】
- apiserver：
- controller：
- manager：
- scheduler：

## 高可用集群步骤

我们采用2个master节点，一个node节点来搭建高可用集群，下面给出了每个节点需要做的事情

![](https://img-blog.csdnimg.cn/6260eafc1b334746881a8bb028f2e940.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  初始化操作

我们需要在这三个节点上进行操作

```
# 关闭防火墙
systemctl stop firewalld
systemctl disable firewalld

# 关闭selinux
# 永久关闭
sed -i 's/enforcing/disabled/' /etc/selinux/config
# 临时关闭
setenforce 0  

# 关闭swap
# 临时
swapoff -a
# 永久关闭
sed -ri 's/.*swap.*/#&/' /etc/fstab

# 根据规划设置主机名【master1节点上操作】
hostnamectl set-hostname master1
# 根据规划设置主机名【master2节点上操作】
hostnamectl set-hostname master2
# 根据规划设置主机名【node1节点操作】
hostnamectl set-hostname node1

# 添加hosts（两个master中，node加了也没错）
cat >> /etc/hosts << EOF
192.168.208.158  k8smaster
192.168.208.155 master01.k8s.io master1
192.168.208.156 master02.k8s.io master2
192.168.208.157 node01.k8s.io node1
EOF


# 将桥接的IPv4流量传递到iptables的链【3个节点上都执行】
cat > /etc/sysctl.d/k8s.conf << EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

# 生效
sysctl --system  

# 时间同步
yum install ntpdate -y
ntpdate time.windows.com
```

## 部署keepAlived

下面我们需要在所有的master节点【master1和master2】上部署keepAlive

### 安装相关包

```
# 安装相关工具
yum install -y conntrack-tools libseccomp libtool-ltdl
# 安装keepalived
yum install -y keepalived
```

### 配置master节点

添加master1的配置

```
cat > /etc/keepalived/keepalived.conf <<EOF 
! Configuration File for keepalived

global_defs {
   router_id k8s
}

vrrp_script check_haproxy {
    script "killall -0 haproxy"
    interval 3
    weight -2
    fall 10
    rise 2
}

vrrp_instance VI_1 {
    state MASTER 
    interface ens33 
    virtual_router_id 51
    priority 250
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass ceb1b3ec013d66163d6ab
    }
    virtual_ipaddress {
        192.168.208.158
    }
    track_script {
        check_haproxy
    }

}
EOF
```

添加master2的配置

```
cat > /etc/keepalived/keepalived.conf <<EOF 
! Configuration File for keepalived

global_defs {
   router_id k8s
}

vrrp_script check_haproxy {
    script "killall -0 haproxy"
    interval 3
    weight -2
    fall 10
    rise 2
}

vrrp_instance VI_1 {
    state BACKUP 
    interface ens33 
    virtual_router_id 51
    priority 200
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass ceb1b3ec013d66163d6ab
    }
    virtual_ipaddress {
        192.168.208.158
    }
    track_script {
        check_haproxy
    }

}
EOF
```

### 启动和检查

在两台master节点都执行

```
# 启动keepalived
systemctl start keepalived.service
# 设置开机启动
systemctl enable keepalived.service
# 查看启动状态
systemctl status keepalived.service
```

启动后查看master的网卡信息，刚开始在master1，master1挂掉就飘到master2

```
ip a s ens33
```

![](https://img-blog.csdnimg.cn/9916ef8c12d646fab1715af91ebc3adb.png)

##  部署haproxy

haproxy主要做负载的作用，将我们的请求分担到不同的node节点上

### 安装

在两个master节点安装 haproxy

```
# 安装haproxy
yum install -y haproxy
# 启动 haproxy(先进行下一步的配置)
systemctl start haproxy
# 开启自启
systemctl enable haproxy
systemctl status haproxy
```

启动后，我们查看对应的端口是否包含 16443

```
netstat -lntup|grep haproxy
此处可能需要
yum install net-tools
```

![](https://img-blog.csdnimg.cn/9c0e21de7c98493682e434521a243dc5.png)

### 配置

两台master节点的配置均相同，配置中声明了后端代理的两个master节点服务器，指定了haproxy运行的端口为16443等，因此16443端口为集群的入口

```
cat > /etc/haproxy/haproxy.cfg << EOF
#---------------------------------------------------------------------
# Global settings
#---------------------------------------------------------------------
global
    # to have these messages end up in /var/log/haproxy.log you will
    # need to:
    # 1) configure syslog to accept network log events.  This is done
    #    by adding the '-r' option to the SYSLOGD_OPTIONS in
    #    /etc/sysconfig/syslog
    # 2) configure local2 events to go to the /var/log/haproxy.log
    #   file. A line like the following can be added to
    #   /etc/sysconfig/syslog
    #
    #    local2.*                       /var/log/haproxy.log
    #
    log         127.0.0.1 local2
    
    chroot      /var/lib/haproxy
    pidfile     /var/run/haproxy.pid
    maxconn     4000
    user        haproxy
    group       haproxy
    daemon 
       
    # turn on stats unix socket
    stats socket /var/lib/haproxy/stats
#---------------------------------------------------------------------
# common defaults that all the 'listen' and 'backend' sections will
# use if not designated in their block
#---------------------------------------------------------------------  
defaults
    mode                    http
    log                     global
    option                  httplog
    option                  dontlognull
    option http-server-close
    option forwardfor       except 127.0.0.0/8
    option                  redispatch
    retries                 3
    timeout http-request    10s
    timeout queue           1m
    timeout connect         10s
    timeout client          1m
    timeout server          1m
    timeout http-keep-alive 10s
    timeout check           10s
    maxconn                 3000
#---------------------------------------------------------------------
# kubernetes apiserver frontend which proxys to the backends
#--------------------------------------------------------------------- 
frontend kubernetes-apiserver
    mode                 tcp
    bind                 *:16443
    option               tcplog
    default_backend      kubernetes-apiserver    
#---------------------------------------------------------------------
# round robin balancing between the various backends
#---------------------------------------------------------------------
backend kubernetes-apiserver
    mode        tcp
    balance     roundrobin
    server      master03.k8s.io   192.168.208.155:6443 check
    server      master02.k8s.io   192.168.208.156:6443 check
#---------------------------------------------------------------------
# collection haproxy statistics message
#---------------------------------------------------------------------
listen stats
    bind                 *:1080
    stats auth           admin:awesomePassword
    stats refresh        5s
    stats realm          HAProxy\ Statistics
    stats uri            /admin?stats
EOF
```

## 安装Docker、Kubeadm、kubectl

所有节点安装Docker/kubeadm/kubelet ，Kubernetes默认CRI（容器运行时）为Docker，因此先安装Docker

### 安装Docker

```
yum install wget
```

每台机器执行以下命令

```
wget https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo -O /etc/yum.repos.d/docker-ce.repo
yum -y install docker-ce-19.03.0
systemctl enable docker && systemctl start docker
docker --version
systemctl status docker
```

首先配置一下Docker的阿里yum源

```
cat >/etc/yum.repos.d/docker.repo<<EOF
[docker-ce-edge]
name=Docker CE Edge - \$basearch
baseurl=https://mirrors.aliyun.com/docker-ce/linux/centos/7/\$basearch/edge
enabled=1
gpgcheck=1
gpgkey=https://mirrors.aliyun.com/docker-ce/linux/centos/gpg
EOF
```

配置docker的镜像源

```
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "registry-mirrors": ["https://m5m8ek6r.mirror.aliyuncs.com"]
}
EOF

systemctl daemon-reload
```

然后重启docker

```
systemctl restart docker
```

### 安装kubeadm，kubelet和kubectl

由于版本更新频繁，这里指定版本号部署：

```bash
# 安装kubelet、kubeadm、kubectl，同时指定版本，先进行下面的yum 的k8s 软件源
yum install -y kubelet-1.19.4 kubeadm-1.19.4 kubectl-1.19.4
# 设置开机启动
systemctl enable kubelet
```

### 添加kubernetes软件源

然后我们还需要配置一下yum的k8s软件源

```
cat > /etc/yum.repos.d/kubernetes.repo << EOF
[kubernetes]
name=Kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF
```

## 部署Kubernetes Master【master节点】

### 创建kubeadm配置文件

在具有vip的master上进行初始化操作，这里为master1

```
查看
ip a s ens33
```

```
# 创建文件夹
mkdir /usr/local/kubernetes/manifests -p
# 到manifests目录
cd /usr/local/kubernetes/manifests/
# 新建yaml文件
vi kubeadm-config.yaml

cat >> alik8simages.sh << EOF
#!/bin/bash
list='kube-apiserver:v1.19.4
kube-controller-manager:v1.19.4
kube-scheduler:v1.19.4
kube-proxy:v1.19.4
pause:3.2
etcd:3.4.13-0
coredns:1.7.0'
for item in \$list
  do

    docker pull registry.aliyuncs.com/google_containers/\$item && docker tag registry.aliyuncs.com/google_containers/\$item k8s.gcr.io/\$item && docker rmi registry.aliyuncs.com/google_containers/\$item

  done
EOF

kubeadm init \
--control-plane-endpoint 192.168.208.158:6443 \
--kubernetes-version=v1.19.4 \
--service-cidr=10.96.0.0/12 \
--pod-network-cidr=10.244.0.0/16 \
--upload-certs
```

yaml内容如下所示：注意ip地址和版本和名称

```yaml
apiServer:
  certSANs:
    - master1
    - master2
    - master.k8s.io
    - 192.168.208.158
    - 192.168.208.155
    - 192.168.208.156
    - 127.0.0.1
  extraArgs:
    authorization-mode: Node,RBAC
  timeoutForControlPlane: 4m0s
apiVersion: kubeadm.k8s.io/v1beta1
certificatesDir: /etc/kubernetes/pki
clusterName: kubernetes
controlPlaneEndpoint: "master.k8s.io:6443"
controllerManager: {}
dns: 
  type: CoreDNS
etcd:
  local:    
    dataDir: /var/lib/etcd
imageRepository: registry.aliyuncs.com/google_containers
kind: ClusterConfiguration
kubernetesVersion: v1.19.4
networking: 
  dnsDomain: cluster.local  
  podSubnet: 10.244.0.0/16
  serviceSubnet: 10.1.0.0/16
scheduler: {}
```

然后我们在 master1 节点执行

```
kubeadm init --config kubeadm-config.yaml
```

执行完成后，就会在拉取我们的进行了【需要等待...】

![](https://img-blog.csdnimg.cn/4604a01ddd80475d8f6ad5e9e6a66f35.png)

按照提示配置环境变量，使用kubectl工具

```
# 执行下方命令
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
# 查看节点
kubectl get nodes
# 查看pod
kubectl get pods -n kube-system
```

**按照提示保存以下内容，一会要使用：**

```
kubeadm join master.k8s.io:16443 --token jv5z7n.3y1zi95p952y9p65 \
    --discovery-token-ca-cert-hash sha256:403bca185c2f3a4791685013499e7ce58f9848e2213e27194b75a2e3293d8812 \
    --control-plane 
```

> --control-plane ： 只有在添加master节点的时候才有

查看集群状态

```
# 查看集群状态
kubectl get cs
# 查看pod
kubectl get pods -n kube-system
```

## 安装集群网络

从官方地址获取到flannel的yaml，在master1上执行

```
# 创建文件夹
mkdir flannel
cd flannel
# 下载yaml文件
wget -c https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

安装flannel网络

```
kubectl apply -f kube-flannel.yml 
```

检查

```
kubectl get pods -n kube-system
```

## master2节点加入集群

### 复制密钥及相关文件

从master1复制密钥及相关文件到master2

```
# ssh root@192.168.44.156 mkdir -p /etc/kubernetes/pki/etcd

# scp /etc/kubernetes/admin.conf root@192.168.44.156:/etc/kubernetes
   
# scp /etc/kubernetes/pki/{ca.*,sa.*,front-proxy-ca.*} root@192.168.44.156:/etc/kubernetes/pki
   
# scp /etc/kubernetes/pki/etcd/ca.* root@192.168.44.156:/etc/kubernetes/pki/etcd
```

### master2加入集群

执行在master1上init后输出的join命令,需要带上参数`--control-plane`表示把master控制节点加入集群

```
kubeadm join master.k8s.io:16443 --token ckf7bs.30576l0okocepg8b     --discovery-token-ca-cert-hash sha256:19afac8b11182f61073e254fb57b9f19ab4d798b70501036fc69ebef46094aba --control-plane
```

检查状态

```
kubectl get node

kubectl get pods --all-namespaces
```

## 加入Kubernetes Node

在node1上执行

向集群添加新节点，执行在kubeadm init输出的kubeadm join命令：

```
kubeadm join master.k8s.io:16443 --token ckf7bs.30576l0okocepg8b     --discovery-token-ca-cert-hash sha256:19afac8b11182f61073e254fb57b9f19ab4d798b70501036fc69ebef46094aba
```

**集群网络重新安装，因为添加了新的node节点**

检查状态

```
kubectl get node
kubectl get pods --all-namespaces
```

## 测试kubernetes集群

在Kubernetes集群中创建一个pod，验证是否正常运行：

```
# 创建nginx deployment
kubectl create deployment nginx --image=nginx
# 暴露端口
kubectl expose deployment nginx --port=80 --type=NodePort
# 查看状态
kubectl get pod,svc
```

然后我们通过任何一个节点，都能够访问我们的nginx页面

