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

