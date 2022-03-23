# Docker简介

## 简介

![](https://img-blog.csdnimg.cn/b57131790c8f42ad8829e5b76a76a9c2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

Docker的出现是为了解决代码在本机可以正常运行，而部署到其他机器不能运行的问题。这是因为代码运行所需要的环境、系统、配置、数据等不同，Docker透过镜像将程序运行所需要的系统环境由下而上打包，达到应用程序跨平台间的无缝接轨运行。

Linux 容器技术的出现就解决了这样一个问题，而 Docker 就是在它的基础上发展过来的。将应用运行在 Docker 容器上面，而 Docker 容器在任何操作系统上都是一致的，这就实现了跨平台、跨服务器。只需要一次配置好环境，换到别的机子上就可以一键部署好，大大简化了操作。

## Docker是什么

Docker是基于Go语言实现的云开源项目

Docker的主要目标是“Build，Ship and Run Any APP，Anywhere”，也就是通过对应用组件的封装、分发、部署、运行等生命周期的管理，使用户的APP及其运行环境能够做到`一次镜像，处处运行`

Linux容器技术的出现就解决了这样一个问题，而Docker就是在它的基础上发展来的。将应用打包成镜像，通过镜像运行在Docker容器上面的实例，而Docker容器在任何操作系统上都是一致的，这就实现了跨平台、跨服务器。只需要一次配置好环境，换到别的机子上就可以一键部署，大大简化了操作。

**Docker是解决了运行环境和配置问题的软件容器，方便做持续集成并有助于整体发布的容器虚拟化技术**



## Docker与传统虚拟化方式的不同

![](https://img-blog.csdnimg.cn/436cb9171efa492f8bf2e3ab4ac49f55.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/72d5aedbcb154dd68e4c9f6e7080e104.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整操作系统，在该系统上再运行所需应用进程
- 而容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核，而且也没有进行硬件虚拟。因此容器要比传统虚拟机更为轻便
- 每个容器之间互相隔离，每个容器有自己的文件系统 ，容器之间进程不会相互影响，能区分计算资源

## Docker安装

CentOS Docker 安装

Docker必须部署在 Linux 内核的系统中，在Windows上部署 Docker 的方法都是先安装一个虚拟机，并在安装 Linux 系统的虚拟机中运行Docker

也可以直接在服务器上安装

## Docker三要素

**docker三要素：镜像、仓库、容器**

Docker 镜像（Image）就是一个`只读`模板，镜像可以用来创建Docker容器，一个镜像可以创建很多容器。

它也相当于是一个root文件系统。比如官方的镜像centos：7就包含了完整的一套centos：7最小系统的root文件系统。

相当于容器的“源代码”，docker镜像文件类似于java的类模板，而docker容器实例类似于java中new出来的实例对象

镜像就是模板，容器就是镜像的一个实例，docker利用容器独立运行一个或一组应用，可以把容器看作是一个简易版的Linux环境和运行在其中的应用程序，仓库是集中存放镜像的地方。

仓库类似于Maven仓库，github仓库，Docker公司提供的官方registry被成为**Docker Hub**，存放各种镜像模板的地方

仓库分为公开仓库(Public) 和 私有仓库 (Private) 两种形式。最大的公开仓库是**Docker Hub（https://hub.docker.com/）**

国内的公开仓库包括阿里云，网易云等

**小结**

Docker 本身是一个容器运行载体或称之为管理引擎。我们把应用程序和配置依赖打包好形成一个可交付的运行环境，这个打包好的运行环境就是`image`镜像文件。只有通过这个镜像文件才能生成Docker容器实例。

## Docker整体架构和通讯原理简述

![](https://img-blog.csdnimg.cn/ab92fe9d660745ceab887a92ae7fee55.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/6d322aa6aa134f74908a6130a029371b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## Docker的安装

1. 确定是Centos7及以上版本

   ```
   cat /etc/redhat-release
   ```

2. 卸载旧版本

   https://docs.docker.com/engine/install/centos/

   ### Uninstall old versions

   Older versions of Docker were called `docker` or `docker-engine`. If these are installed, uninstall them, along with associated dependencies.

   ```
    sudo yum remove docker \
                     docker-client \
                     docker-client-latest \
                     docker-common \
                     docker-latest \
                     docker-latest-logrotate \
                     docker-logrotate \
                     docker-engine
   ```

3. yum 安装 gcc 相关

   ```
   yum -y install gcc
   yum -y install gcc-c++
   ```

4. 安装需要的软件包

   根据官网要求，执行命令

   ```
   yum install -y yum-utils
   ```

5. 设置stable镜像仓库

   不要使用官网的外网地址，使用国内阿里云镜像

   ```
   yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
   ```

6. 更新yum软件包索引

   ```
   yum makecache fast（centos8好像是没有fast？但是用这个似乎也能）
   ```

7. 安装Docker CE

   ```
   yum -y install docker-ce docker-ce-cli containerd.io
   ```

8. 启动Docker

   ```
   systemctl start docker
   ps -ef|grep docker（查看docker）
   docker version
   ```

9. 测试

   ```
   docker run hello-world
   ```

10. 卸载

    docker默认安装目录：/var/lib/docker
    
    ```
    systemctl stop docker
    yum remove docker-ce docker-ce-cli containerd.io
    rm -rf /var/lib/docker
    rm -rf /var/lib/containerd
    ```

## 阿里云镜像加速

1. 注册一个属于自己的阿里云账户(可复用淘宝账号)

2. 登陆阿里云开发者平台

3. 点击控制台

4. 选择容器镜像服务

   ![](https://img-blog.csdnimg.cn/b405a62475144b089ba461291c31b63e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

5. 点击镜像工具-镜像加速器，获取个人加速地址

6. 粘贴脚本直接执行

   ![](https://img-blog.csdnimg.cn/48e096cde1e045b5b8a8461196880eb1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

   ```
   mkdir -p /etc/docker
   tee /etc/docker/daemon.json <<-'EOF'
   {
     "registry-mirrors": ["https://m5m8ek6r.mirror.aliyuncs.com"]
   }
   EOF
   systemctl daemon-reload
   systemctl restart docker
   
   docker run hello-world（测试是否成功）
   ```

![](https://img-blog.csdnimg.cn/c4fef787f13748b09ac914f9defbd94a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

运行镜像的流程

![](https://img-blog.csdnimg.cn/a1b642adf7ac4ec493a58bb7d8cf2174.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

# Docker常用命令

## docker帮助命令

- `docker version`：查看版本信息
- `docker info`：查看docker信息
- 启动docker： systemctl start docker
- 停止docker： systemctl stop docker
- 重启docker： systemctl restart docker
- 查看docker状态： systemctl status docker
- 开机启动： systemctl enable docker
- 查看docker概要信息： docker info
- 查看docker总体帮助文档： docker --help
- 查看docker命令帮助文档： docker 具体命令 --help

## docker镜像命令

### 列出所有镜像

- `docker images`：列出本地主机上的镜像，镜像由镜像名:tag唯一标记，tag可认为是版本号
  - `docker images -a`：列出本地所有的镜像（含中间映像层）
  - `docker images -q`：只显示镜像的id
  - `docker images --digests`：显示镜像的摘要信息
  - `docker images --no-trunc`：显示完整的镜像信息

选项说明：

- `REPOSITORY`：表示镜像的仓库源
- `TAG`：镜像的标签 版本号
- `IMAGE ID`：镜像ID
- `CREATED`：镜像创建时间
- `SIZE`：镜像大小

同一仓库源可以有多个 TAG版本，代表这个仓库源的不同个版本，我们使用 REPOSITORY:TAG 来定义不同的镜像。

如果你不指定一个镜像的版本标签，例如你只使用 ubuntu，docker 将默认使用 ubuntu:latest 镜像

### 在github搜索镜像

- `docker search 镜像名`：在github上搜索某个镜像
  - `docker search -s 30 tomcat`：列出starts数不小于30的镜像
  - `docker search --no-trunc 镜像名`：显示完整的镜像描述
  - `docker --automated 镜像名`：只列出automated build类型的镜像

![](https://img-blog.csdnimg.cn/ca6e53afe2d04045aaf23472ebbc44bc.png)、

![](https://img-blog.csdnimg.cn/4690da0395a34c7f8653ebef37fb6973.png)

- OPTIONS说明：
- --limit : 只列出N个镜像，默认25个
- docker search --limit 5 redis

### 下载镜像

- `docker pull 镜像名`：下载镜像
  - `docker pull 镜像名:TAG`：下载指定TAG的镜像，不加TAG默认为latest

### 查看镜像/容器/数据卷所占的空间

- docker system df 

### 删除未在使用的镜像

- `docker rmi 镜像名`：删除未在使用镜像，若在使用则不能删除，默认删除latest的
  - `docker rmi -f 镜像名`：强制删除
  - `docker rmi -f 镜像名1:TAG 镜像名2:TAG`：删除多个
  - `docker rmi -f $(docker images -qa)`：删除全部

面试题：谈谈docker虚悬镜像是什么？

- 仓库名、标签都是<none>的镜像，俗称虚悬镜像dangling image
- ![](https://img-blog.csdnimg.cn/c8753a23979547ccb2b5b27195d392f3.png)
  

## docker容器命令

**有镜像才能创建容器， 这是根本前提(下载一个CentOS或者ubuntu镜像演示)**

以Ubuntu镜像为例演示，先用`docker pull ubuntu`命令下载相应镜像

![](https://img-blog.csdnimg.cn/ba6220af705f4ac3bf8054e918e38660.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 新建+启动容器

- docker run [OPTIONS] **IMAGE** [COMMAND] [ARG...]

- OPTIONS说明

   OPTIONS说明（常用）：有些是一个减号，有些是两个减号

   

  - --name="容器新名字"    为容器指定一个名称；

  - -d: 后台运行容器并返回容器ID，也即启动守护式容器(后台运行)；

   

  - -i：以交互模式运行容器，通常与 -t 同时使用；

  - -t：为容器重新分配一个伪输入终端，通常与 -i 同时使用；

    也即启动交互式容器(前台有伪终端，等待交互)；

    ```
    docker run -it ubuntu xxxx
    ```

   

  - -P: 随机端口映射，大写P

  - -p: 指定端口映射，小写p

![](https://img-blog.csdnimg.cn/94e90eb368254db6aca5550f168f3743.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 启动交互式容器(前台命令行)

```
docker run -it ubuntu /bin/bash(这里用bash也行)
```

![](https://img-blog.csdnimg.cn/83082fbf9e024346bc08fe5af6ce12b6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

参数说明：

- -i: 交互式操作。

- -t: 终端。

- ubuntu : ubuntu 镜像。

- /bin/bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

- 要退出终端，直接输入 exit:

现在可以直接用linux命令

![](https://img-blog.csdnimg.cn/a0647ad92884432fb9de9fc6ea7b2a44.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 列出当前所有正在运行的容器

新建一个会话，执行  docker ps [OPTIONS]

OPTIONS说明（常用）：（可以不写）

- -a :列出当前所有正在运行的容器+历史上运行过的

- -l :显示最近创建的容器。

- -n：显示最近n个创建的容器。

- -q :静默模式，只显示容器编号。

![](https://img-blog.csdnimg.cn/3f0808cd21e74f1db01d8989c5cae591.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

此时再执行命令  docker run -it --name=myu1 ubuntu bash，表示再创建了一个容器实例

此时再开一个会话

![](https://img-blog.csdnimg.cn/e9fd0c7e8c8b4309bace3e6ef5e96104.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 退出容器

- `exit`：容器停止退出
- `Ctrl+P+Q`：容器不停止退出

### 启动/重启/停止容器

- `docker start 容器名或容器ID`：启动容器
- `docker restart 容器名或容器ID`：重启容器
- `docker stop 容器名或容器ID`：停止容器，类似于电脑关机
- `docker kill 容器名或容器ID`：强制停止，类似于电脑拔电源关机

![](https://img-blog.csdnimg.cn/55ea3bfc66884564be5976b9ba1dab8a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 删除容器

- `docker rm 容器名`：删除已停止的容器，若未停止则不删除

-  docker rm -f 容器名：停止并删除容器

  ```
  docker rm -f bb2077ebcfc4 e37bc8d24e91
  ```

  - `docker rm -f $(docker ps -a -q)`：删除所有容器
  - `docker ps -a -q | xargs docker rm`：删除所有容器

### 启动守护式容器(后台服务器)

在大部分的场景下，我们希望 docker 的服务是在后台运行的， 我们可以过 -d 指定容器的后台运行模式

```
docker run -d 容器名
```

问题：然后docker ps 进行查看, 会发现容器已经退出

很重要的要说明的一点: Docker容器后台运行,就必须有一个前台进程。容器运行的命令如果不是那些一直挂起的命令（比如运行top，tail），就是会自动退出的。

这个是docker的机制问题,比如你的web容器,我们以nginx为例，正常情况下,我们配置启动服务只需要启动响应的service即可。例如service nginx start  但是,这样做,nginx为后台进程模式运行,就导致docker前台没有运行的应用,

这样的容器后台启动后,会立即自杀因为他觉得他没事可做了。

所以，最佳的解决方案是,将你要运行的程序以前台进程的形式运行，

常见就是命令行模式，表示我还有交互操作，别中断。（用 -it ）

### redis 前后台启动演示case

前台交互式启动

```
docker run -it redis:6.0.8
```

这种容易不小心就退出了

后台守护式启动

```
docker run -d redis:6.0.8
```

使用docker ps 可以查看到有

### 容器日志相关

- `docker logs 容器ID`：查看容器日志

### 查看容器内运行的进程

```
docker top 容器ID
```

### 查看容器内部细节

```
docker inspect 容器名：查看容器内部细节，返回是json串
```

### 进入正在运行的容器并以命令行交互

- `docker exec -it 容器ID bash命令`：在容器中打开新的终端，并可以启动新的进程

  ```
  docker exec -it xxxxx /bin/bash
  ```

  ![](https://img-blog.csdnimg.cn/59a657dfa35d40499e9fa49c3e12367e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 重新进入`docker attach 容器ID`

  **上述两者区别：**

  attach 直接进入容器启动命令的终端，不会启动新的进程 用exit退出，会导致容器的停止。

  ![](https://img-blog.csdnimg.cn/055b842f9763414198299ae7489e51dc.png)

  exec 是在容器中打开新的终端，并且可以启动新的进程 用exit退出，不会导致容器的停止。

  ![](https://img-blog.csdnimg.cn/92a4b45a6f994a49ba65dcd0b8509826.png)

  **推荐大家使用** docker exec 命令，因为退出容器终端，不会导致容器的停止。

用之前的redis容器实例进入试试：

- 进入redis服务
  - docker exec -it 容器ID /bin/bash
  - docker exec -it 容器ID redis-cli

一般用 -d 后台启动的程序，再用exec进入对应容器实例

### 拷贝容器内容到本机

- `docker cp 容器ID:容器中文件的路径 本机路径`：从容器内拷贝文件到本机上

![](https://img-blog.csdnimg.cn/55cb1259a00a484686a7d5e4d093d99a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 导入和导出容器

- export 导出容器的内容留作为一个tar归档文件[对应import命令]
- import 从tar包中的内容创建一个新的文件系统再导入为镜像[对应export]

案例：

```
docker export 容器ID > 文件名.tar
```

导出后删掉原来的容器实例

![](https://img-blog.csdnimg.cn/7d62cb80db6f4a0fb7dec7061d48d435.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

再导入进docker

```
cat 文件名.tar | docker import - 镜像用户/镜像名:镜像版本号
```

```
cat abcd.tar | docker import - sucker/ubuntu:3.7
docker images
```

![](https://img-blog.csdnimg.cn/1a989bbf748b4c659be06a2eb85245d5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/1c6e87f38a664baabb52088489e3a169.png)

之前的容器实例就回来了

常用命令：

```
attach    Attach to a running container                 # 当前 shell 下 attach 连接指定运行镜像
build     Build an image from a Dockerfile              # 通过 Dockerfile 定制镜像
commit    Create a new image from a container changes   # 提交当前容器为新的镜像
cp        Copy files/folders from the containers filesystem to the host path   #从容器中拷贝指定文件或者目录到宿主机中
create    Create a new container                        # 创建一个新的容器，同 run，但不启动容器
diff      Inspect changes on a container's filesystem   # 查看 docker 容器变化
events    Get real time events from the server          # 从 docker 服务获取容器实时事件
exec      Run a command in an existing container        # 在已存在的容器上运行命令
export    Stream the contents of a container as a tar archive   # 导出容器的内容流作为一个 tar 归档文件[对应 import ]
history   Show the history of an image                  # 展示一个镜像形成历史
images    List images                                   # 列出系统当前镜像
import    Create a new filesystem image from the contents of a tarball # 从tar包中的内容创建一个新的文件系统映像[对应export]
info      Display system-wide information               # 显示系统相关信息
inspect   Return low-level information on a container   # 查看容器详细信息
kill      Kill a running container                      # kill 指定 docker 容器
load      Load an image from a tar archive              # 从一个 tar 包中加载一个镜像[对应 save]
login     Register or Login to the docker registry server    # 注册或者登陆一个 docker 源服务器
logout    Log out from a Docker registry server          # 从当前 Docker registry 退出
logs      Fetch the logs of a container                 # 输出当前容器日志信息
port      Lookup the public-facing port which is NAT-ed to PRIVATE_PORT    # 查看映射端口对应的容器内部源端口
pause     Pause all processes within a container        # 暂停容器
ps        List containers                               # 列出容器列表
pull      Pull an image or a repository from the docker registry server   # 从docker镜像源服务器拉取指定镜像或者库镜像
push      Push an image or a repository to the docker registry server    # 推送指定镜像或者库镜像至docker源服务器
restart   Restart a running container                   # 重启运行的容器
rm        Remove one or more containers                 # 移除一个或者多个容器
rmi       Remove one or more images       # 移除一个或多个镜像[无容器使用该镜像才可删除，否则需删除相关容器才可继续或 -f 强制删除]
run       Run a command in a new container              # 创建一个新的容器并运行一个命令
save      Save an image to a tar archive                # 保存一个镜像为一个 tar 包[对应 load]
search    Search for an image on the Docker Hub         # 在 docker hub 中搜索镜像
start     Start a stopped containers                    # 启动容器
stop      Stop a running containers                     # 停止容器
tag       Tag an image into a repository                # 给源中镜像打标签
top       Lookup the running processes of a container   # 查看容器中运行的进程信息
unpause   Unpause a paused container                    # 取消暂停容器
version   Show the docker version information           # 查看 docker 版本号
wait      Block until a container stops, then print its exit code   # 截取容器停止时的退出状态值
```

# Docker镜像

## 镜像

是一种轻量级、可执行的独立软件包，它包含运行某个软件所需的所有内容，我们把应用程序和配置依赖打包好形成一个可交付的运行环境(包括代码、运行时需要的库、环境变量和配置文件等)，这个打包好的运行环境就是image镜像文件。

只有通过这个镜像文件才能生成Docker容器实例(类似Java中new出来一个对象)。

**分层的镜像**

以我们的pull为例，在下载的过程中我们可以看到docker的镜像好像是在一层一层的在下载

## UnionFS（联合文件系统）

UnionFS（联合文件系统）：Union文件系统（UnionFS）是一种分层、轻量级并且高性能的文件系统，它支持对文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtual filesystem)。Union 文件系统是 Docker 镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。

特性：一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录

## Docker镜像加载原理

Docker镜像加载原理：

 docker的镜像实际上由一层一层的文件系统组成，这种层级的文件系统UnionFS。

bootfs(boot file system)主要包含bootloader和kernel, bootloader主要是引导加载kernel, Linux刚启动时会加载bootfs文件系统，**在Docker镜像的最底层是引导文件系统bootfs**。这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。

 rootfs (root file system) ，在bootfs之上。包含的就是典型 Linux 系统中的 /dev, /proc, /bin, /etc 等标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等等。

![](https://img-blog.csdnimg.cn/f34aec80f2ce4b2e935ee050bb017338.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

**平时我们安装进虚拟机的CentOS都是好几个G，为什么docker这里才200M？？**

对于一个精简的OS，rootfs可以很小，只需要包括最基本的命令、工具和程序库就可以了，因为底层直接用Host的kernel，自己只需要提供 rootfs 就行了。由此可见对于不同的linux发行版, bootfs基本是一致的, rootfs会有差别, 因此不同的发行版可以公用bootfs。

## 为什么 Docker 镜像要采用这种分层结构呢

镜像分层最大的一个好处就是共享资源，方便复制迁移，就是为了复用。

 比如说有多个镜像都从相同的 base 镜像构建而来，那么 Docker Host 只需在磁盘上保存一份 base 镜像；

同时内存中也只需加载一份 base 镜像，就可以为所有容器服务了。而且镜像的每一层都可以被共享。

## 重点理解

**Docker镜像层都是只读的，容器层是可写的** 

当容器启动时，一个新的可写层被加载到镜像的顶部。 这一层通常被称作“容器层”，“容器层”之下的都叫“镜像层”。

当容器启动时，一个新的可写层被加载到镜像的顶部。这一层通常被称作“容器层”，“容器层”之下的都叫“镜像层”。

所有对容器的改动 - 无论添加、删除、还是修改文件都只会发生在容器层中。只有容器层是可写的，容器层下面的所有镜像层都是只读的。

![](https://img-blog.csdnimg.cn/5230937c75e74e028c760c65206b7e1b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## commit操作

- docker commit  提交容器副本使之成为一个新的镜像

- docker commit -m="提交的描述信息" -a="作者" 容器ID 要创建的目标镜像名:[标签名（版本号）]

案例演示ubuntu安装vim

- 从Hub上下载ubuntu镜像到本地并成功运行

- 原始的默认Ubuntu镜像是不带着vim命令的

- 外网连通的情况下，安装vim

  ```
  先更新包管理工具
  apt-get update
  安装vim
  apt-get install vim
  ```

  docker容器内执行上述两条命令：

![](https://img-blog.csdnimg.cn/3a307e25f96946a28bc36a989273821e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 安装完成后，commit我们自己的新镜像

![](https://img-blog.csdnimg.cn/0aba89a013c04ab999db6d928c1ae8f3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/fa93af4d4be544e8acdfd29c3bd26483.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

官网是默认下载的Ubuntu没有vim命令

我们自己commit构建的镜像，新增加了vim功能，可以成功使用。

## 小总结

Docker中的镜像分层，**支持通过扩展现有镜像，创建新的镜像**。类似Java继承于一个Base基础类，自己再按需扩展。

新镜像是从 base 镜像一层一层叠加生成的。每安装一个软件，就在现有镜像的基础上增加一层

![](https://img-blog.csdnimg.cn/f22a43f6c9cb4d6babd0ccae09a230ad.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 本地镜像发布到阿里云

![](https://img-blog.csdnimg.cn/43e04ea6b58446ff92c56041765021be.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 创建镜像仓库

- 进入阿里云开发者平台，登录后进入控制台，点击容器镜像服务

  ![](https://img-blog.csdnimg.cn/058b7879d2c2492c8c12a4bf422c7d48.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 选择个人实例

  ![](https://img-blog.csdnimg.cn/4d6063059420410db91232b29d21bf11.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 选择命名空间，创建命名空间(相当于包名)

  ![](https://img-blog.csdnimg.cn/3af6bbc16b3b472f82c9da9d06673bc7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 点击镜像仓库，创建镜像仓库

  ![](https://img-blog.csdnimg.cn/0f126c36ef034c1bb48e4111113b3c26.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  ![](https://img-blog.csdnimg.cn/53dea5bd9c5e40fab4589bce64cf8903.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 选择本地仓库创建

- 进入管理界面获得脚本

  ![](https://img-blog.csdnimg.cn/d5f10eda74b1449f8ae73df733164f62.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 使用三条命令

  ```
  $ docker login --username=sucker_苏 registry.cn-heyuan.aliyuncs.com
  $ docker tag [ImageId] registry.cn-heyuan.aliyuncs.com/sucker/myubuntu:[镜像版本号]
  $ docker push registry.cn-heyuan.aliyuncs.com/sucker/myubuntu:[镜像版本号]
  ```

  ![](https://img-blog.csdnimg.cn/9962a4e3855b4c85b454ce6fd5491471.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 将阿里云上镜像下载到本地

![](https://img-blog.csdnimg.cn/5aa7a9c30de3423ab3775164715beb07.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 本地镜像发布到私有库

### 私有库

官方Docker Hub地址：https://hub.docker.com/，中国大陆访问太慢了且准备被阿里云取代的趋势，不太主流。

Dockerhub、阿里云这样的公共镜像仓库可能不太方便，涉及机密的公司不可能提供镜像给公网，所以需要创建一个本地私人仓库供给团队使用，基于公司内部项目构建镜像。

Docker Registry是官方提供的工具，可以用于构建私有镜像仓库

### 本地镜像推送到私有库

- 下载 镜像  Docker Registry

  ```
  docker pull registry
  ```

  ![](https://img-blog.csdnimg.cn/f8e5c346587e4effa8cb57dc2512b4ad.png)

- 运行私有库Registry，相当于本地有个私有Docker hub

  ```
  docker run -d -p 5000:5000  -v /zzyyuse/myregistry/:/tmp/registry --privileged=true registry
  ```

  默认情况，仓库被创建在容器的/var/lib/registry目录下，建议自行用容器卷映射，方便于宿主机联调

- ubuntu 安装 ifconfig 命令

  从Hub上下载ubuntu镜像到本地并成功运行
  原始的Ubuntu镜像是不带着ifconfig命令的

  ![](https://img-blog.csdnimg.cn/48819ab8acf648008113f14e3e799853.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  外网连通的情况下，安装ifconfig命令并测试通过

  docker容器内执行上述两条命令：

  apt-get update

  apt-get install net-tools

  ![](https://img-blog.csdnimg.cn/a8f66885edb747fa8da6522800707c20.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 安装完成后，commit我们自己的新镜像

  公式：

  docker commit -m="提交的描述信息" -a="作者" 容器ID 要创建的目标镜像名:[标签名]

  命令：在容器外执行，记得

  docker commit -m="ifconfig cmd add" -a="sucker" 01adb809e6fa suckerubuntu:1.2

  ![](https://img-blog.csdnimg.cn/e21e5c9877b3479ba77561312f9f6885.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 启动我们的新镜像并和原来的对比

  官网是默认下载的Ubuntu没有ifconfig命令

  我们自己commit构建的新镜像，新增加了ifconfig功能，可以成功使用。

  先停止正在运行的实例

  ![](https://img-blog.csdnimg.cn/8870b16d7f20473eb1337a63bcf4d017.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  测试新镜像

  ![](https://img-blog.csdnimg.cn/f3bd83557ab94ac584e1640091f0e5b2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### curl 验证私服库上有什么镜像

curl -XGET localhost:5000/v2/_catalog

```
curl -XGET localhost:5000/v2/_catalog
```

可以看到，目前私服库没有任何镜像上传过

- 将新镜像suckerubuntu:1.2修改符合私服规范的Tag

  按照公式： docker  tag  镜像:Tag  Host:Port/Repository:Tag

  自己host主机IP地址，填写同学你们自己的，不要粘贴错误，O(∩_∩)O

  使用命令 docker tag 将suckerubuntu:1.2 这个镜像修改为101.43.184.159:5000/suckerubuntu:1.2

  docker tag suckerubuntu:1.2 localhost:5000/suckerubuntu:1.2

![](https://img-blog.csdnimg.cn/d4488002f20f40ac8c6309b8ecc9a9ee.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 修改配置文件使之支持http

  ![](https://img-blog.csdnimg.cn/dfa4ed3085fe4f9c9f4133cbff3e9867.png)

  别无脑照着复制，registry-mirrors 配置的是国内阿里提供的镜像加速地址，不用加速的话访问官网的会很慢。

  **2个配置中间有个逗号 ，别漏了，这个配置是json格式的。**

  vim命令新增如下红色内容：vim /etc/docker/daemon.json

  ```
  {
    "registry-mirrors": ["https://aa25jngu.mirror.aliyuncs.com"],
    "insecure-registries": ["localhost:5000"]
  }
  ```

  上述理由：docker默认不允许http方式推送镜像，通过配置选项来取消这个限制。====> 修改完后如果不生效，建议重启docker

  ```
  systemctl restart docker
  systemctl status docker
  ```

- 重启私服库

  ```
  docker run -d -p 5000:5000  -v /zzyyuse/myregistry/:/tmp/registry --privileged=true registry
  ```

### push 推送到私服库

docker push localhost:5000/suckerubuntu:1.2

![](https://img-blog.csdnimg.cn/64dbedea85fa419b996f6b1b5f028f79.png)

验证私服库上传有什么镜像

curl -XGET localhost:5000/v2/_catalog

删除本地镜像

```
docker rmi -f localhost:5000/suckerubuntu:1.2
```

![](https://img-blog.csdnimg.cn/76e3a57dfab14707884d34273a66c1cd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

**pull到本地运行**

docker pull localhost:5000/suckerubuntu:1.2

![](https://img-blog.csdnimg.cn/5635a4216df647a290ec865651854c1e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

docker run -it 镜像ID /bin/bash 测试

![](https://img-blog.csdnimg.cn/aad6aaf76c1640c6a49d14d8251e2d70.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

# 容器数据卷

## 容器数据卷

### 坑：容器卷记得加入

--privileged=true

Docker挂载主机目录访问如果出现cannot open directory .: Permission denied

解决办法：在挂载目录后多加一个  --privileged=true  参数即可

如果是CentOS7安全模块会比之前系统版本加强，不安全的会先禁止，所以目录挂载的情况被默认为不安全的行为，

在SELinux里面挂载目录被禁止掉了额，如果要开启，我们一般使用--privileged=true命令，扩大容器的权限解决挂载目录没有权限的问题，也即使用该参数，container内的root拥有真正的root权限，否则，container内的root只是外部的一个普通用户权限。

![](https://img-blog.csdnimg.cn/cd14cf9a27d1403994d497f992a6cb15.png)

### 是什么

卷就是目录或文件，存在于一个或多个容器中，由docker挂载到容器，但不属于联合文件系统，因此能够绕过Union File System提供一些用于持续存储或共享数据的特性：

卷的设计目的就是数据的持久化，完全独立于容器的生存周期，因此Docker不会在容器删除时删除其挂载的数据卷

- 一句话：有点类似我们Redis里面的rdb和aof文件

- 将docker容器内的数据保存进宿主机的磁盘中

- 运行一个带有容器卷存储功能的容器实例
  - docker run -it --privileged=true -v /宿主机绝对路径目录:/容器内目录   镜像名

**作用**

将运用与运行的环境打包镜像，run后形成容器实例运行 ，但是我们对数据的要求希望是持久化的

Docker容器产生的数据，如果不备份，那么当容器实例删除后，容器内的数据自然也就没有了。

为了能保存数据在docker中我们使用卷。

**特点：**

1：数据卷可在容器之间共享或重用数据

2：卷中的更改可以直接实时生效

3：数据卷中的更改不会包含在镜像的更新中

4：数据卷的生命周期一直持续到没有容器使用它为止

### 案例

宿主vs容器之间映射添加容器卷

- 直接命令添加

  ```
   公式：docker run -it -v /宿主机目录:/容器内目录 ubuntu /bin/bash
  docker run -it --privileged=true -v /tmp/host_data:/tmp/docker_data --name=u1 ubuntu
  ```

  ![](https://img-blog.csdnimg.cn/14cb7a678e4f4cd897332e83dc167da3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 回到主机目录查看

  ![](https://img-blog.csdnimg.cn/8d16fda131344fd09ecc778c4a3807ec.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

在主机上新建文件

```
touch hostin.txt
```

在容器中也同步了

![](https://img-blog.csdnimg.cn/0d055885f1d049b28d9d7630ba3ed943.png)

容器中写文件

```
echo 'hello docker'>a.txt
ls -l
cat a.txt
```

![](https://img-blog.csdnimg.cn/13b39af5ce0f4a1584721900119c3cee.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

主机中查看并修改

![](https://img-blog.csdnimg.cn/3e1f25f849a44704b336ffdda9c0ab7f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```
ll
vim a.txt
cat a.txt
```

容器中查看也成功保存

```
cat a.txt
```

**查看数据卷是否挂载成功**

```
docker ps
docker inspect 容器ID
```

![](https://img-blog.csdnimg.cn/173594db307c489f8464224fccd19f44.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 容器和宿主机之间数据共享

- docker修改，主机同步获得 

- 主机修改，docker同步获得

- docker容器stop，主机修改，docker容器重启看数据是否同步

主机上修改

![](https://img-blog.csdnimg.cn/0bc0c684bb7a49fab24d148c822ab865.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

重启容器查看，已经同步

![](https://img-blog.csdnimg.cn/725c770cfdf146e999e13db86235856f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 读写规则映射添加说明

**默认是可读可写**

- docker run -it --privileged=true -v /宿主机绝对路径目录:/容器内目录:rw   镜像名

默认同上案例，默认就是rw

**只读：ro**

容器实例内部被限制，只能读取不能写

/容器目录:ro 镜像名        就能完成功能，此时容器自己只能读取不能写 

ro = read only

此时如果宿主机写入内容，可以同步给容器内，容器可以读取到。

 docker run -it --privileged=true -v /宿主机绝对路径目录:/容器内目录:ro   镜像名

**案例**

首先创建一个带容器卷存储功能的容器实例

```
docker run -it --privileged=true -v /mydocker/u:/tmp/u:ro --name u2 ubuntu
```

![](https://img-blog.csdnimg.cn/31a7fd02dff44190bfac2bd51d799262.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

在主机相应目录创建一个a.txt 文件

```
cd /mydocker/u
pwd（输出当前目录）
ll
touch a.txt
vim a.txt
```

容器相应目录查看，无法在容器内写文件

```
cd /tmp/u
pwd
ll
cat a.txt
touch b.txt（结果是：touch: cannot touch 'b.txt': Read-only file system）
```

## 卷的继承和共享

- 容器1完成和宿主机的映射

  ```
  docker run -it  --privileged=true -v /mydocker/u:/tmp/u --name u1 ubuntu
  ```

  ![](https://img-blog.csdnimg.cn/0aae60e759574241bbc23e7becc0d92f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 主机查看

  ```
  ll
  ```

  结果查看到u1data.txt

  主机写文件 host.txt

  ```
  touch host.txt
  ```

- 容器1查看

  ```
  ll
  ```

- 容器2继承容器1的卷规则

  ```
  docker run -it --privileged=true --volumes-from u1 --name u2 ubuntu
  cd /tmp/u
  ls -l（结果查看到host.txt和u1data.txt）
  touch u2data.txt
  ls -l
  ```

- 容器1和主机查看成功

**退出容器1后**

- 主机首先新建host2.txt

  ```
  touch host2.txt
  ```

- 容器 2 查看成功，新建u2datav2.txt

  ```
  touch u2datav2.txt
  ```

- 主机查看成功（ll）

- 此时我们查看最近存在的两个实例

  ```
  docker ps -n 2
  docker start u1
  docker exec -it u1 /bin/bash
  cd /tmp/u
  ls -l
  ```

  结果发现数据同步，表示容器1和容器2谁退出了都无所谓，恢复后仍然会同步

  ![](https://img-blog.csdnimg.cn/dcc094a35264491b8f7b22878e85dd5e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

# Docker 常规安装

## 总体步骤

- 搜索镜像
- 拉取镜像
- 查看镜像
- 启动镜像
- 服务端口映射
- 停止容器
- 移除容器

## 安装tomcat

- docker hub上面查找tomcat镜像

- 或者docker search tomcat

- docker pull tomcat

- docker images  查看是否有拉取到的 tomcat

- 使用tomcat镜像创建容器实例(也叫运行镜像)

  - docker run -it -p 8080:8080 tomcat

  - -p 小写，主机端口:docker容器端口

  - -P 大写，随机分配端口

    ![](https://img-blog.csdnimg.cn/48fe754ad345478ab1fd40b7036fc593.png)

  - i：交互

  - t:终端

  - d:后台

  ![](Docker.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16-16434656671092.png)

- 访问tomcat首页

  ```
  http://101.43.184.159:8080/
  ```

  发现报错404

  解决方法：

  - 可能是没有映射端口或者没有关闭防火墙
  - 将webapps.dist目录换成webapps

- 解决过程

  查看webapps文件夹为空，删除webapps，将webapps.dist修改为webapps

  ```
  docker exec -it b2de30a1ba43 /bin/bash
  ls -l
  rm -r webapps
  mv webapps.dist webapps
  ```

  此时访问成功

- 免修改版说明

  - docker pull billygoo/tomcat8-jdk8
  - 或者直接 docker run -d -p 8080:8080 --name mytomcat8 billygoo/tomcat8-jdk8

## 安装mysql

docker hub上面查找mysql镜像

```
docker search mysql
docker pull mysql:5.7
```

使用mysql5.7镜像创建容器(也叫运行镜像)

### 简单版

- 使用mysql镜像

  ```
  ps -ef|grep mysql(查看3306端口是否被占用)
  docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7
  docker ps
  docker exec -it 容器ID /bin/bash
  mysql -uroot -p
  ```

  ![](https://img-blog.csdnimg.cn/3984f8e46ace4e41b14649e4f2bc0bfc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 建库建表插入数据

  ```
  show databases;
  create database db01;
  use db01;
  create table t1(id int,name varchar(20));
  insert into t1 values(1,'z23');
  select * from t1;
  ```

  ![](https://img-blog.csdnimg.cn/c3f98c9e8b994584806a56b1933f3184.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

**ifconfig 查看本机地址**

这里用的服务器，所以是私网地址

![](https://img-blog.csdnimg.cn/7f6dc44a243f4c3f928f4a1c1bad082d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 外部使用sqlyog 连接成功

  此时，插入中文数据，出错

  ```
  insert into t1 values(2,'王无');
  ```

  - 报错原因是 字符集编码隐患

     docker里面的mysql容器实例查看，内容如下：

     ```
     SHOW VARIABLES LIKE 'character%'
     ```

    ![](https://img-blog.csdnimg.cn/33e212a0104640e1a2ee4880db85c3f6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  - 还有问题就是 此时没有使用数据卷技术，数据备份存在问题，删除容器后，里面的mysql数据如何办

### 实战版

- 新建mysql实例，带数据卷

  ```
  docker run -d -p 3306:3306 --privileged=true -v /zzyyuse/mysql/log:/var/log/mysql -v /zzyyuse/mysql/data:/var/lib/mysql -v /zzyyuse/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456  --name mysql mysql:5.7
  docker ps
  ```

- 主机进入conf目录，新建my.cnf

  ```
  vim my.cnf
  在my.cnf中写入
  [client]
  default_character_set=utf8
  [mysqld]
  collation_server = utf8_general_ci
  character_set_server = utf8
  
  cat my.cnf
  ```

  ![](https://img-blog.csdnimg.cn/a7dd6bb82b7e45358624fb57f3934e2c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 重新启动mysql容器实例再重新进入并查看字符编码

  ```
  docker restart mysql(别名是mysql)
  docker exec -it mysql /bin/bash
  mysql -uroot -p
  SHOW VARIABLES LIKE 'character%'
  结果成功改为utf8
  ```

- 重新建表建库，插入中文数据，成功

- 结论

  之前的DB 无效

  修改字符集操作+重启mysql容器实例

  之后的DB 有效，需要新建

  结论：docker安装完MySQL并run出容器后，建议请先修改完字符集编码后再新建mysql库-表-插数据

- 此时我们将 容器实例 删除

  ```
  docker rm -f mysql
  docker run -d -p 3306:3306 --privileged=true -v /zzyyuse/mysql/log:/var/log/mysql -v /zzyyuse/mysql/data:/var/lib/mysql -v /zzyyuse/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456  --name mysql mysql:5.7
  docker ps
  docker exec -it mysql /bin/bash
  mysql -uroot -p
  use db01;
  select * from t1;
  结果成功，数据成功写回容器
  ```

  

## 安装Redis

### 基础操作

从docker hub上(阿里云加速器)拉取redis镜像到本地标签为6.0.8

- 入门命令

  ```
  docker run -it -d -p 6379:6379 redis:6.0.8
  docker exec -it fcedc1244a45 /bin/bash
  redis-cli
  set k1 v1
  get k1
  ```

  实际上同其他一样，需要加数据卷，先删除这个容器实例

- 在CentOS宿主机下新建目录/app/redis，如果有redis服务器就可以直接用复制命令复制过来，没有就新建用原始来修改

  ```
  mkdir -p /app/redis/
  cd /app/redis
  touch redis.conf
  ```

- 默认出厂的原始redis.conf

  ```
  # Redis configuration file example.
  #
  # Note that in order to read the configuration file, Redis must be
  # started with the file path as first argument:
  #
  # ./redis-server /path/to/redis.conf
   
  # Note on units: when memory size is needed, it is possible to specify
  # it in the usual form of 1k 5GB 4M and so forth:
  #
  # 1k => 1000 bytes
  # 1kb => 1024 bytes
  # 1m => 1000000 bytes
  # 1mb => 1024*1024 bytes
  # 1g => 1000000000 bytes
  # 1gb => 1024*1024*1024 bytes
  #
  # units are case insensitive so 1GB 1Gb 1gB are all the same.
   
  ################################## INCLUDES ###################################
   
  # Include one or more other config files here.  This is useful if you
  # have a standard template that goes to all Redis servers but also need
  # to customize a few per-server settings.  Include files can include
  # other files, so use this wisely.
  #
  # Notice option "include" won't be rewritten by command "CONFIG REWRITE"
  # from admin or Redis Sentinel. Since Redis always uses the last processed
  # line as value of a configuration directive, you'd better put includes
  # at the beginning of this file to avoid overwriting config change at runtime.
  #
  # If instead you are interested in using includes to override configuration
  # options, it is better to use include as the last line.
  #
  # include /path/to/local.conf
  # include /path/to/other.conf
   
  ################################## MODULES #####################################
   
  # Load modules at startup. If the server is not able to load modules
  # it will abort. It is possible to use multiple loadmodule directives.
  #
  # loadmodule /path/to/my_module.so
  # loadmodule /path/to/other_module.so
   
  ################################## NETWORK #####################################
   
  # By default, if no "bind" configuration directive is specified, Redis listens
  # for connections from all the network interfaces available on the server.
  # It is possible to listen to just one or multiple selected interfaces using
  # the "bind" configuration directive, followed by one or more IP addresses.
  #
  # Examples:
  #
  # bind 192.168.1.100 10.0.0.1
  # bind 127.0.0.1 ::1
  #
  # ~~~ WARNING ~~~ If the computer running Redis is directly exposed to the
  # internet, binding to all the interfaces is dangerous and will expose the
  # instance to everybody on the internet. So by default we uncomment the
  # following bind directive, that will force Redis to listen only into
  # the IPv4 loopback interface address (this means Redis will be able to
  # accept connections only from clients running into the same computer it
  # is running).
  #
  # IF YOU ARE SURE YOU WANT YOUR INSTANCE TO LISTEN TO ALL THE INTERFACES
  # JUST COMMENT THE FOLLOWING LINE.
  # ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  #bind 127.0.0.1
   
  # Protected mode is a layer of security protection, in order to avoid that
  # Redis instances left open on the internet are accessed and exploited.
  #
  # When protected mode is on and if:
  #
  # 1) The server is not binding explicitly to a set of addresses using the
  #    "bind" directive.
  # 2) No password is configured.
  #
  # The server only accepts connections from clients connecting from the
  # IPv4 and IPv6 loopback addresses 127.0.0.1 and ::1, and from Unix domain
  # sockets.
  #
  # By default protected mode is enabled. You should disable it only if
  # you are sure you want clients from other hosts to connect to Redis
  # even if no authentication is configured, nor a specific set of interfaces
  # are explicitly listed using the "bind" directive.
  protected-mode no
   
  # Accept connections on the specified port, default is 6379 (IANA #815344).
  # If port 0 is specified Redis will not listen on a TCP socket.
  port 6379
   
  # TCP listen() backlog.
  #
  # In high requests-per-second environments you need an high backlog in order
  # to avoid slow clients connections issues. Note that the Linux kernel
  # will silently truncate it to the value of /proc/sys/net/core/somaxconn so
  # make sure to raise both the value of somaxconn and tcp_max_syn_backlog
  # in order to get the desired effect.
  tcp-backlog 511
   
  # Unix socket.
  #
  # Specify the path for the Unix socket that will be used to listen for
  # incoming connections. There is no default, so Redis will not listen
  # on a unix socket when not specified.
  #
  # unixsocket /tmp/redis.sock
  # unixsocketperm 700
   
  # Close the connection after a client is idle for N seconds (0 to disable)
  timeout 0
   
  # TCP keepalive.
  #
  # If non-zero, use SO_KEEPALIVE to send TCP ACKs to clients in absence
  # of communication. This is useful for two reasons:
  #
  # 1) Detect dead peers.
  # 2) Take the connection alive from the point of view of network
  #    equipment in the middle.
  #
  # On Linux, the specified value (in seconds) is the period used to send ACKs.
  # Note that to close the connection the double of the time is needed.
  # On other kernels the period depends on the kernel configuration.
  #
  # A reasonable value for this option is 300 seconds, which is the new
  # Redis default starting with Redis 3.2.1.
  tcp-keepalive 300
   
  ################################# GENERAL #####################################
   
  # By default Redis does not run as a daemon. Use 'yes' if you need it.
  # Note that Redis will write a pid file in /var/run/redis.pid when daemonized.
  daemonize no
   
  # If you run Redis from upstart or systemd, Redis can interact with your
  # supervision tree. Options:
  #   supervised no      - no supervision interaction
  #   supervised upstart - signal upstart by putting Redis into SIGSTOP mode
  #   supervised systemd - signal systemd by writing READY=1 to $NOTIFY_SOCKET
  #   supervised auto    - detect upstart or systemd method based on
  #                        UPSTART_JOB or NOTIFY_SOCKET environment variables
  # Note: these supervision methods only signal "process is ready."
  #       They do not enable continuous liveness pings back to your supervisor.
  supervised no
   
  # If a pid file is specified, Redis writes it where specified at startup
  # and removes it at exit.
  #
  # When the server runs non daemonized, no pid file is created if none is
  # specified in the configuration. When the server is daemonized, the pid file
  # is used even if not specified, defaulting to "/var/run/redis.pid".
  #
  # Creating a pid file is best effort: if Redis is not able to create it
  # nothing bad happens, the server will start and run normally.
  pidfile /var/run/redis_6379.pid
   
  # Specify the server verbosity level.
  # This can be one of:
  # debug (a lot of information, useful for development/testing)
  # verbose (many rarely useful info, but not a mess like the debug level)
  # notice (moderately verbose, what you want in production probably)
  # warning (only very important / critical messages are logged)
  loglevel notice
   
  # Specify the log file name. Also the empty string can be used to force
  # Redis to log on the standard output. Note that if you use standard
  # output for logging but daemonize, logs will be sent to /dev/null
  logfile ""
   
  # To enable logging to the system logger, just set 'syslog-enabled' to yes,
  # and optionally update the other syslog parameters to suit your needs.
  # syslog-enabled no
   
  # Specify the syslog identity.
  # syslog-ident redis
   
  # Specify the syslog facility. Must be USER or between LOCAL0-LOCAL7.
  # syslog-facility local0
   
  # Set the number of databases. The default database is DB 0, you can select
  # a different one on a per-connection basis using SELECT <dbid> where
  # dbid is a number between 0 and 'databases'-1
  databases 16
   
  # By default Redis shows an ASCII art logo only when started to log to the
  # standard output and if the standard output is a TTY. Basically this means
  # that normally a logo is displayed only in interactive sessions.
  #
  # However it is possible to force the pre-4.0 behavior and always show a
  # ASCII art logo in startup logs by setting the following option to yes.
  always-show-logo yes
   
  ################################ SNAPSHOTTING  ################################
  #
  # Save the DB on disk:
  #
  #   save <seconds> <changes>
  #
  #   Will save the DB if both the given number of seconds and the given
  #   number of write operations against the DB occurred.
  #
  #   In the example below the behaviour will be to save:
  #   after 900 sec (15 min) if at least 1 key changed
  #   after 300 sec (5 min) if at least 10 keys changed
  #   after 60 sec if at least 10000 keys changed
  #
  #   Note: you can disable saving completely by commenting out all "save" lines.
  #
  #   It is also possible to remove all the previously configured save
  #   points by adding a save directive with a single empty string argument
  #   like in the following example:
  #
  #   save ""
   
  save 900 1
  save 300 10
  save 60 10000
   
  # By default Redis will stop accepting writes if RDB snapshots are enabled
  # (at least one save point) and the latest background save failed.
  # This will make the user aware (in a hard way) that data is not persisting
  # on disk properly, otherwise chances are that no one will notice and some
  # disaster will happen.
  #
  # If the background saving process will start working again Redis will
  # automatically allow writes again.
  #
  # However if you have setup your proper monitoring of the Redis server
  # and persistence, you may want to disable this feature so that Redis will
  # continue to work as usual even if there are problems with disk,
  # permissions, and so forth.
  stop-writes-on-bgsave-error yes
   
  # Compress string objects using LZF when dump .rdb databases?
  # For default that's set to 'yes' as it's almost always a win.
  # If you want to save some CPU in the saving child set it to 'no' but
  # the dataset will likely be bigger if you have compressible values or keys.
  rdbcompression yes
   
  # Since version 5 of RDB a CRC64 checksum is placed at the end of the file.
  # This makes the format more resistant to corruption but there is a performance
  # hit to pay (around 10%) when saving and loading RDB files, so you can disable it
  # for maximum performances.
  #
  # RDB files created with checksum disabled have a checksum of zero that will
  # tell the loading code to skip the check.
  rdbchecksum yes
   
  # The filename where to dump the DB
  dbfilename dump.rdb
   
  # The working directory.
  #
  # The DB will be written inside this directory, with the filename specified
  # above using the 'dbfilename' configuration directive.
  #
  # The Append Only File will also be created inside this directory.
  #
  # Note that you must specify a directory here, not a file name.
  dir ./
   
  ################################# REPLICATION #################################
   
  # Master-Replica replication. Use replicaof to make a Redis instance a copy of
  # another Redis server. A few things to understand ASAP about Redis replication.
  #
  #   +------------------+      +---------------+
  #   |      Master      | ---> |    Replica    |
  #   | (receive writes) |      |  (exact copy) |
  #   +------------------+      +---------------+
  #
  # 1) Redis replication is asynchronous, but you can configure a master to
  #    stop accepting writes if it appears to be not connected with at least
  #    a given number of replicas.
  # 2) Redis replicas are able to perform a partial resynchronization with the
  #    master if the replication link is lost for a relatively small amount of
  #    time. You may want to configure the replication backlog size (see the next
  #    sections of this file) with a sensible value depending on your needs.
  # 3) Replication is automatic and does not need user intervention. After a
  #    network partition replicas automatically try to reconnect to masters
  #    and resynchronize with them.
  #
  # replicaof <masterip> <masterport>
   
  # If the master is password protected (using the "requirepass" configuration
  # directive below) it is possible to tell the replica to authenticate before
  # starting the replication synchronization process, otherwise the master will
  # refuse the replica request.
  #
  # masterauth <master-password>
   
  # When a replica loses its connection with the master, or when the replication
  # is still in progress, the replica can act in two different ways:
  #
  # 1) if replica-serve-stale-data is set to 'yes' (the default) the replica will
  #    still reply to client requests, possibly with out of date data, or the
  #    data set may just be empty if this is the first synchronization.
  #
  # 2) if replica-serve-stale-data is set to 'no' the replica will reply with
  #    an error "SYNC with master in progress" to all the kind of commands
  #    but to INFO, replicaOF, AUTH, PING, SHUTDOWN, REPLCONF, ROLE, CONFIG,
  #    SUBSCRIBE, UNSUBSCRIBE, PSUBSCRIBE, PUNSUBSCRIBE, PUBLISH, PUBSUB,
  #    COMMAND, POST, HOST: and LATENCY.
  #
  replica-serve-stale-data yes
   
  # You can configure a replica instance to accept writes or not. Writing against
  # a replica instance may be useful to store some ephemeral data (because data
  # written on a replica will be easily deleted after resync with the master) but
  # may also cause problems if clients are writing to it because of a
  # misconfiguration.
  #
  # Since Redis 2.6 by default replicas are read-only.
  #
  # Note: read only replicas are not designed to be exposed to untrusted clients
  # on the internet. It's just a protection layer against misuse of the instance.
  # Still a read only replica exports by default all the administrative commands
  # such as CONFIG, DEBUG, and so forth. To a limited extent you can improve
  # security of read only replicas using 'rename-command' to shadow all the
  # administrative / dangerous commands.
  replica-read-only yes
   
  # Replication SYNC strategy: disk or socket.
  #
  # -------------------------------------------------------
  # WARNING: DISKLESS REPLICATION IS EXPERIMENTAL CURRENTLY
  # -------------------------------------------------------
  #
  # New replicas and reconnecting replicas that are not able to continue the replication
  # process just receiving differences, need to do what is called a "full
  # synchronization". An RDB file is transmitted from the master to the replicas.
  # The transmission can happen in two different ways:
  #
  # 1) Disk-backed: The Redis master creates a new process that writes the RDB
  #                 file on disk. Later the file is transferred by the parent
  #                 process to the replicas incrementally.
  # 2) Diskless: The Redis master creates a new process that directly writes the
  #              RDB file to replica sockets, without touching the disk at all.
  #
  # With disk-backed replication, while the RDB file is generated, more replicas
  # can be queued and served with the RDB file as soon as the current child producing
  # the RDB file finishes its work. With diskless replication instead once
  # the transfer starts, new replicas arriving will be queued and a new transfer
  # will start when the current one terminates.
  #
  # When diskless replication is used, the master waits a configurable amount of
  # time (in seconds) before starting the transfer in the hope that multiple replicas
  # will arrive and the transfer can be parallelized.
  #
  # With slow disks and fast (large bandwidth) networks, diskless replication
  # works better.
  repl-diskless-sync no
   
  # When diskless replication is enabled, it is possible to configure the delay
  # the server waits in order to spawn the child that transfers the RDB via socket
  # to the replicas.
  #
  # This is important since once the transfer starts, it is not possible to serve
  # new replicas arriving, that will be queued for the next RDB transfer, so the server
  # waits a delay in order to let more replicas arrive.
  #
  # The delay is specified in seconds, and by default is 5 seconds. To disable
  # it entirely just set it to 0 seconds and the transfer will start ASAP.
  repl-diskless-sync-delay 5
   
  # Replicas send PINGs to server in a predefined interval. It's possible to change
  # this interval with the repl_ping_replica_period option. The default value is 10
  # seconds.
  #
  # repl-ping-replica-period 10
   
  # The following option sets the replication timeout for:
  #
  # 1) Bulk transfer I/O during SYNC, from the point of view of replica.
  # 2) Master timeout from the point of view of replicas (data, pings).
  # 3) Replica timeout from the point of view of masters (REPLCONF ACK pings).
  #
  # It is important to make sure that this value is greater than the value
  # specified for repl-ping-replica-period otherwise a timeout will be detected
  # every time there is low traffic between the master and the replica.
  #
  # repl-timeout 60
   
  # Disable TCP_NODELAY on the replica socket after SYNC?
  #
  # If you select "yes" Redis will use a smaller number of TCP packets and
  # less bandwidth to send data to replicas. But this can add a delay for
  # the data to appear on the replica side, up to 40 milliseconds with
  # Linux kernels using a default configuration.
  #
  # If you select "no" the delay for data to appear on the replica side will
  # be reduced but more bandwidth will be used for replication.
  #
  # By default we optimize for low latency, but in very high traffic conditions
  # or when the master and replicas are many hops away, turning this to "yes" may
  # be a good idea.
  repl-disable-tcp-nodelay no
   
  # Set the replication backlog size. The backlog is a buffer that accumulates
  # replica data when replicas are disconnected for some time, so that when a replica
  # wants to reconnect again, often a full resync is not needed, but a partial
  # resync is enough, just passing the portion of data the replica missed while
  # disconnected.
  #
  # The bigger the replication backlog, the longer the time the replica can be
  # disconnected and later be able to perform a partial resynchronization.
  #
  # The backlog is only allocated once there is at least a replica connected.
  #
  # repl-backlog-size 1mb
   
  # After a master has no longer connected replicas for some time, the backlog
  # will be freed. The following option configures the amount of seconds that
  # need to elapse, starting from the time the last replica disconnected, for
  # the backlog buffer to be freed.
  #
  # Note that replicas never free the backlog for timeout, since they may be
  # promoted to masters later, and should be able to correctly "partially
  # resynchronize" with the replicas: hence they should always accumulate backlog.
  #
  # A value of 0 means to never release the backlog.
  #
  # repl-backlog-ttl 3600
   
  # The replica priority is an integer number published by Redis in the INFO output.
  # It is used by Redis Sentinel in order to select a replica to promote into a
  # master if the master is no longer working correctly.
  #
  # A replica with a low priority number is considered better for promotion, so
  # for instance if there are three replicas with priority 10, 100, 25 Sentinel will
  # pick the one with priority 10, that is the lowest.
  #
  # However a special priority of 0 marks the replica as not able to perform the
  # role of master, so a replica with priority of 0 will never be selected by
  # Redis Sentinel for promotion.
  #
  # By default the priority is 100.
  replica-priority 100
   
  # It is possible for a master to stop accepting writes if there are less than
  # N replicas connected, having a lag less or equal than M seconds.
  #
  # The N replicas need to be in "online" state.
  #
  # The lag in seconds, that must be <= the specified value, is calculated from
  # the last ping received from the replica, that is usually sent every second.
  #
  # This option does not GUARANTEE that N replicas will accept the write, but
  # will limit the window of exposure for lost writes in case not enough replicas
  # are available, to the specified number of seconds.
  #
  # For example to require at least 3 replicas with a lag <= 10 seconds use:
  #
  # min-replicas-to-write 3
  # min-replicas-max-lag 10
  #
  # Setting one or the other to 0 disables the feature.
  #
  # By default min-replicas-to-write is set to 0 (feature disabled) and
  # min-replicas-max-lag is set to 10.
   
  # A Redis master is able to list the address and port of the attached
  # replicas in different ways. For example the "INFO replication" section
  # offers this information, which is used, among other tools, by
  # Redis Sentinel in order to discover replica instances.
  # Another place where this info is available is in the output of the
  # "ROLE" command of a master.
  #
  # The listed IP and address normally reported by a replica is obtained
  # in the following way:
  #
  #   IP: The address is auto detected by checking the peer address
  #   of the socket used by the replica to connect with the master.
  #
  #   Port: The port is communicated by the replica during the replication
  #   handshake, and is normally the port that the replica is using to
  #   listen for connections.
  #
  # However when port forwarding or Network Address Translation (NAT) is
  # used, the replica may be actually reachable via different IP and port
  # pairs. The following two options can be used by a replica in order to
  # report to its master a specific set of IP and port, so that both INFO
  # and ROLE will report those values.
  #
  # There is no need to use both the options if you need to override just
  # the port or the IP address.
  #
  # replica-announce-ip 5.5.5.5
  # replica-announce-port 1234
   
  ################################## SECURITY ###################################
   
  # Require clients to issue AUTH <PASSWORD> before processing any other
  # commands.  This might be useful in environments in which you do not trust
  # others with access to the host running redis-server.
  #
  # This should stay commented out for backward compatibility and because most
  # people do not need auth (e.g. they run their own servers).
  #
  # Warning: since Redis is pretty fast an outside user can try up to
  # 150k passwords per second against a good box. This means that you should
  # use a very strong password otherwise it will be very easy to break.
  #
  # requirepass foobared
   
  # Command renaming.
  #
  # It is possible to change the name of dangerous commands in a shared
  # environment. For instance the CONFIG command may be renamed into something
  # hard to guess so that it will still be available for internal-use tools
  # but not available for general clients.
  #
  # Example:
  #
  # rename-command CONFIG b840fc02d524045429941cc15f59e41cb7be6c52
  #
  # It is also possible to completely kill a command by renaming it into
  # an empty string:
  #
  # rename-command CONFIG ""
  #
  # Please note that changing the name of commands that are logged into the
  # AOF file or transmitted to replicas may cause problems.
   
  ################################### CLIENTS ####################################
   
  # Set the max number of connected clients at the same time. By default
  # this limit is set to 10000 clients, however if the Redis server is not
  # able to configure the process file limit to allow for the specified limit
  # the max number of allowed clients is set to the current file limit
  # minus 32 (as Redis reserves a few file descriptors for internal uses).
  #
  # Once the limit is reached Redis will close all the new connections sending
  # an error 'max number of clients reached'.
  #
  # maxclients 10000
   
  ############################## MEMORY MANAGEMENT ################################
   
  # Set a memory usage limit to the specified amount of bytes.
  # When the memory limit is reached Redis will try to remove keys
  # according to the eviction policy selected (see maxmemory-policy).
  #
  # If Redis can't remove keys according to the policy, or if the policy is
  # set to 'noeviction', Redis will start to reply with errors to commands
  # that would use more memory, like SET, LPUSH, and so on, and will continue
  # to reply to read-only commands like GET.
  #
  # This option is usually useful when using Redis as an LRU or LFU cache, or to
  # set a hard memory limit for an instance (using the 'noeviction' policy).
  #
  # WARNING: If you have replicas attached to an instance with maxmemory on,
  # the size of the output buffers needed to feed the replicas are subtracted
  # from the used memory count, so that network problems / resyncs will
  # not trigger a loop where keys are evicted, and in turn the output
  # buffer of replicas is full with DELs of keys evicted triggering the deletion
  # of more keys, and so forth until the database is completely emptied.
  #
  # In short... if you have replicas attached it is suggested that you set a lower
  # limit for maxmemory so that there is some free RAM on the system for replica
  # output buffers (but this is not needed if the policy is 'noeviction').
  #
  # maxmemory <bytes>
   
  # MAXMEMORY POLICY: how Redis will select what to remove when maxmemory
  # is reached. You can select among five behaviors:
  #
  # volatile-lru -> Evict using approximated LRU among the keys with an expire set.
  # allkeys-lru -> Evict any key using approximated LRU.
  # volatile-lfu -> Evict using approximated LFU among the keys with an expire set.
  # allkeys-lfu -> Evict any key using approximated LFU.
  # volatile-random -> Remove a random key among the ones with an expire set.
  # allkeys-random -> Remove a random key, any key.
  # volatile-ttl -> Remove the key with the nearest expire time (minor TTL)
  # noeviction -> Don't evict anything, just return an error on write operations.
  #
  # LRU means Least Recently Used
  # LFU means Least Frequently Used
  #
  # Both LRU, LFU and volatile-ttl are implemented using approximated
  # randomized algorithms.
  #
  # Note: with any of the above policies, Redis will return an error on write
  #       operations, when there are no suitable keys for eviction.
  #
  #       At the date of writing these commands are: set setnx setex append
  #       incr decr rpush lpush rpushx lpushx linsert lset rpoplpush sadd
  #       sinter sinterstore sunion sunionstore sdiff sdiffstore zadd zincrby
  #       zunionstore zinterstore hset hsetnx hmset hincrby incrby decrby
  #       getset mset msetnx exec sort
  #
  # The default is:
  #
  # maxmemory-policy noeviction
   
  # LRU, LFU and minimal TTL algorithms are not precise algorithms but approximated
  # algorithms (in order to save memory), so you can tune it for speed or
  # accuracy. For default Redis will check five keys and pick the one that was
  # used less recently, you can change the sample size using the following
  # configuration directive.
  #
  # The default of 5 produces good enough results. 10 Approximates very closely
  # true LRU but costs more CPU. 3 is faster but not very accurate.
  #
  # maxmemory-samples 5
   
  # Starting from Redis 5, by default a replica will ignore its maxmemory setting
  # (unless it is promoted to master after a failover or manually). It means
  # that the eviction of keys will be just handled by the master, sending the
  # DEL commands to the replica as keys evict in the master side.
  #
  # This behavior ensures that masters and replicas stay consistent, and is usually
  # what you want, however if your replica is writable, or you want the replica to have
  # a different memory setting, and you are sure all the writes performed to the
  # replica are idempotent, then you may change this default (but be sure to understand
  # what you are doing).
  #
  # Note that since the replica by default does not evict, it may end using more
  # memory than the one set via maxmemory (there are certain buffers that may
  # be larger on the replica, or data structures may sometimes take more memory and so
  # forth). So make sure you monitor your replicas and make sure they have enough
  # memory to never hit a real out-of-memory condition before the master hits
  # the configured maxmemory setting.
  #
  # replica-ignore-maxmemory yes
   
  ############################# LAZY FREEING ####################################
   
  # Redis has two primitives to delete keys. One is called DEL and is a blocking
  # deletion of the object. It means that the server stops processing new commands
  # in order to reclaim all the memory associated with an object in a synchronous
  # way. If the key deleted is associated with a small object, the time needed
  # in order to execute the DEL command is very small and comparable to most other
  # O(1) or O(log_N) commands in Redis. However if the key is associated with an
  # aggregated value containing millions of elements, the server can block for
  # a long time (even seconds) in order to complete the operation.
  #
  # For the above reasons Redis also offers non blocking deletion primitives
  # such as UNLINK (non blocking DEL) and the ASYNC option of FLUSHALL and
  # FLUSHDB commands, in order to reclaim memory in background. Those commands
  # are executed in constant time. Another thread will incrementally free the
  # object in the background as fast as possible.
  #
  # DEL, UNLINK and ASYNC option of FLUSHALL and FLUSHDB are user-controlled.
  # It's up to the design of the application to understand when it is a good
  # idea to use one or the other. However the Redis server sometimes has to
  # delete keys or flush the whole database as a side effect of other operations.
  # Specifically Redis deletes objects independently of a user call in the
  # following scenarios:
  #
  # 1) On eviction, because of the maxmemory and maxmemory policy configurations,
  #    in order to make room for new data, without going over the specified
  #    memory limit.
  # 2) Because of expire: when a key with an associated time to live (see the
  #    EXPIRE command) must be deleted from memory.
  # 3) Because of a side effect of a command that stores data on a key that may
  #    already exist. For example the RENAME command may delete the old key
  #    content when it is replaced with another one. Similarly SUNIONSTORE
  #    or SORT with STORE option may delete existing keys. The SET command
  #    itself removes any old content of the specified key in order to replace
  #    it with the specified string.
  # 4) During replication, when a replica performs a full resynchronization with
  #    its master, the content of the whole database is removed in order to
  #    load the RDB file just transferred.
  #
  # In all the above cases the default is to delete objects in a blocking way,
  # like if DEL was called. However you can configure each case specifically
  # in order to instead release memory in a non-blocking way like if UNLINK
  # was called, using the following configuration directives:
   
  lazyfree-lazy-eviction no
  lazyfree-lazy-expire no
  lazyfree-lazy-server-del no
  replica-lazy-flush no
   
  ############################## APPEND ONLY MODE ###############################
   
  # By default Redis asynchronously dumps the dataset on disk. This mode is
  # good enough in many applications, but an issue with the Redis process or
  # a power outage may result into a few minutes of writes lost (depending on
  # the configured save points).
  #
  # The Append Only File is an alternative persistence mode that provides
  # much better durability. For instance using the default data fsync policy
  # (see later in the config file) Redis can lose just one second of writes in a
  # dramatic event like a server power outage, or a single write if something
  # wrong with the Redis process itself happens, but the operating system is
  # still running correctly.
  #
  # AOF and RDB persistence can be enabled at the same time without problems.
  # If the AOF is enabled on startup Redis will load the AOF, that is the file
  # with the better durability guarantees.
  #
  # Please check http://redis.io/topics/persistence for more information.
   
  appendonly no
   
  # The name of the append only file (default: "appendonly.aof")
   
  appendfilename "appendonly.aof"
   
  # The fsync() call tells the Operating System to actually write data on disk
  # instead of waiting for more data in the output buffer. Some OS will really flush
  # data on disk, some other OS will just try to do it ASAP.
  #
  # Redis supports three different modes:
  #
  # no: don't fsync, just let the OS flush the data when it wants. Faster.
  # always: fsync after every write to the append only log. Slow, Safest.
  # everysec: fsync only one time every second. Compromise.
  #
  # The default is "everysec", as that's usually the right compromise between
  # speed and data safety. It's up to you to understand if you can relax this to
  # "no" that will let the operating system flush the output buffer when
  # it wants, for better performances (but if you can live with the idea of
  # some data loss consider the default persistence mode that's snapshotting),
  # or on the contrary, use "always" that's very slow but a bit safer than
  # everysec.
  #
  # More details please check the following article:
  # http://antirez.com/post/redis-persistence-demystified.html
  #
  # If unsure, use "everysec".
   
  # appendfsync always
  appendfsync everysec
  # appendfsync no
   
  # When the AOF fsync policy is set to always or everysec, and a background
  # saving process (a background save or AOF log background rewriting) is
  # performing a lot of I/O against the disk, in some Linux configurations
  # Redis may block too long on the fsync() call. Note that there is no fix for
  # this currently, as even performing fsync in a different thread will block
  # our synchronous write(2) call.
  #
  # In order to mitigate this problem it's possible to use the following option
  # that will prevent fsync() from being called in the main process while a
  # BGSAVE or BGREWRITEAOF is in progress.
  #
  # This means that while another child is saving, the durability of Redis is
  # the same as "appendfsync none". In practical terms, this means that it is
  # possible to lose up to 30 seconds of log in the worst scenario (with the
  # default Linux settings).
  #
  # If you have latency problems turn this to "yes". Otherwise leave it as
  # "no" that is the safest pick from the point of view of durability.
   
  no-appendfsync-on-rewrite no
   
  # Automatic rewrite of the append only file.
  # Redis is able to automatically rewrite the log file implicitly calling
  # BGREWRITEAOF when the AOF log size grows by the specified percentage.
  #
  # This is how it works: Redis remembers the size of the AOF file after the
  # latest rewrite (if no rewrite has happened since the restart, the size of
  # the AOF at startup is used).
  #
  # This base size is compared to the current size. If the current size is
  # bigger than the specified percentage, the rewrite is triggered. Also
  # you need to specify a minimal size for the AOF file to be rewritten, this
  # is useful to avoid rewriting the AOF file even if the percentage increase
  # is reached but it is still pretty small.
  #
  # Specify a percentage of zero in order to disable the automatic AOF
  # rewrite feature.
   
  auto-aof-rewrite-percentage 100
  auto-aof-rewrite-min-size 64mb
   
  # An AOF file may be found to be truncated at the end during the Redis
  # startup process, when the AOF data gets loaded back into memory.
  # This may happen when the system where Redis is running
  # crashes, especially when an ext4 filesystem is mounted without the
  # data=ordered option (however this can't happen when Redis itself
  # crashes or aborts but the operating system still works correctly).
  #
  # Redis can either exit with an error when this happens, or load as much
  # data as possible (the default now) and start if the AOF file is found
  # to be truncated at the end. The following option controls this behavior.
  #
  # If aof-load-truncated is set to yes, a truncated AOF file is loaded and
  # the Redis server starts emitting a log to inform the user of the event.
  # Otherwise if the option is set to no, the server aborts with an error
  # and refuses to start. When the option is set to no, the user requires
  # to fix the AOF file using the "redis-check-aof" utility before to restart
  # the server.
  #
  # Note that if the AOF file will be found to be corrupted in the middle
  # the server will still exit with an error. This option only applies when
  # Redis will try to read more data from the AOF file but not enough bytes
  # will be found.
  aof-load-truncated yes
   
  # When rewriting the AOF file, Redis is able to use an RDB preamble in the
  # AOF file for faster rewrites and recoveries. When this option is turned
  # on the rewritten AOF file is composed of two different stanzas:
  #
  #   [RDB file][AOF tail]
  #
  # When loading Redis recognizes that the AOF file starts with the "REDIS"
  # string and loads the prefixed RDB file, and continues loading the AOF
  # tail.
  aof-use-rdb-preamble yes
   
  ################################ LUA SCRIPTING  ###############################
   
  # Max execution time of a Lua script in milliseconds.
  #
  # If the maximum execution time is reached Redis will log that a script is
  # still in execution after the maximum allowed time and will start to
  # reply to queries with an error.
  #
  # When a long running script exceeds the maximum execution time only the
  # SCRIPT KILL and SHUTDOWN NOSAVE commands are available. The first can be
  # used to stop a script that did not yet called write commands. The second
  # is the only way to shut down the server in the case a write command was
  # already issued by the script but the user doesn't want to wait for the natural
  # termination of the script.
  #
  # Set it to 0 or a negative value for unlimited execution without warnings.
  lua-time-limit 5000
   
  ################################ REDIS CLUSTER  ###############################
   
  # Normal Redis instances can't be part of a Redis Cluster; only nodes that are
  # started as cluster nodes can. In order to start a Redis instance as a
  # cluster node enable the cluster support uncommenting the following:
  #
  # cluster-enabled yes
   
  # Every cluster node has a cluster configuration file. This file is not
  # intended to be edited by hand. It is created and updated by Redis nodes.
  # Every Redis Cluster node requires a different cluster configuration file.
  # Make sure that instances running in the same system do not have
  # overlapping cluster configuration file names.
  #
  # cluster-config-file nodes-6379.conf
   
  # Cluster node timeout is the amount of milliseconds a node must be unreachable
  # for it to be considered in failure state.
  # Most other internal time limits are multiple of the node timeout.
  #
  # cluster-node-timeout 15000
   
  # A replica of a failing master will avoid to start a failover if its data
  # looks too old.
  #
  # There is no simple way for a replica to actually have an exact measure of
  # its "data age", so the following two checks are performed:
  #
  # 1) If there are multiple replicas able to failover, they exchange messages
  #    in order to try to give an advantage to the replica with the best
  #    replication offset (more data from the master processed).
  #    Replicas will try to get their rank by offset, and apply to the start
  #    of the failover a delay proportional to their rank.
  #
  # 2) Every single replica computes the time of the last interaction with
  #    its master. This can be the last ping or command received (if the master
  #    is still in the "connected" state), or the time that elapsed since the
  #    disconnection with the master (if the replication link is currently down).
  #    If the last interaction is too old, the replica will not try to failover
  #    at all.
  #
  # The point "2" can be tuned by user. Specifically a replica will not perform
  # the failover if, since the last interaction with the master, the time
  # elapsed is greater than:
  #
  #   (node-timeout * replica-validity-factor) + repl-ping-replica-period
  #
  # So for example if node-timeout is 30 seconds, and the replica-validity-factor
  # is 10, and assuming a default repl-ping-replica-period of 10 seconds, the
  # replica will not try to failover if it was not able to talk with the master
  # for longer than 310 seconds.
  #
  # A large replica-validity-factor may allow replicas with too old data to failover
  # a master, while a too small value may prevent the cluster from being able to
  # elect a replica at all.
  #
  # For maximum availability, it is possible to set the replica-validity-factor
  # to a value of 0, which means, that replicas will always try to failover the
  # master regardless of the last time they interacted with the master.
  # (However they'll always try to apply a delay proportional to their
  # offset rank).
  #
  # Zero is the only value able to guarantee that when all the partitions heal
  # the cluster will always be able to continue.
  #
  # cluster-replica-validity-factor 10
   
  # Cluster replicas are able to migrate to orphaned masters, that are masters
  # that are left without working replicas. This improves the cluster ability
  # to resist to failures as otherwise an orphaned master can't be failed over
  # in case of failure if it has no working replicas.
  #
  # Replicas migrate to orphaned masters only if there are still at least a
  # given number of other working replicas for their old master. This number
  # is the "migration barrier". A migration barrier of 1 means that a replica
  # will migrate only if there is at least 1 other working replica for its master
  # and so forth. It usually reflects the number of replicas you want for every
  # master in your cluster.
  #
  # Default is 1 (replicas migrate only if their masters remain with at least
  # one replica). To disable migration just set it to a very large value.
  # A value of 0 can be set but is useful only for debugging and dangerous
  # in production.
  #
  # cluster-migration-barrier 1
   
  # By default Redis Cluster nodes stop accepting queries if they detect there
  # is at least an hash slot uncovered (no available node is serving it).
  # This way if the cluster is partially down (for example a range of hash slots
  # are no longer covered) all the cluster becomes, eventually, unavailable.
  # It automatically returns available as soon as all the slots are covered again.
  #
  # However sometimes you want the subset of the cluster which is working,
  # to continue to accept queries for the part of the key space that is still
  # covered. In order to do so, just set the cluster-require-full-coverage
  # option to no.
  #
  # cluster-require-full-coverage yes
   
  # This option, when set to yes, prevents replicas from trying to failover its
  # master during master failures. However the master can still perform a
  # manual failover, if forced to do so.
  #
  # This is useful in different scenarios, especially in the case of multiple
  # data center operations, where we want one side to never be promoted if not
  # in the case of a total DC failure.
  #
  # cluster-replica-no-failover no
   
  # In order to setup your cluster make sure to read the documentation
  # available at http://redis.io web site.
   
  ########################## CLUSTER DOCKER/NAT support  ########################
   
  # In certain deployments, Redis Cluster nodes address discovery fails, because
  # addresses are NAT-ted or because ports are forwarded (the typical case is
  # Docker and other containers).
  #
  # In order to make Redis Cluster working in such environments, a static
  # configuration where each node knows its public address is needed. The
  # following two options are used for this scope, and are:
  #
  # * cluster-announce-ip
  # * cluster-announce-port
  # * cluster-announce-bus-port
  #
  # Each instruct the node about its address, client port, and cluster message
  # bus port. The information is then published in the header of the bus packets
  # so that other nodes will be able to correctly map the address of the node
  # publishing the information.
  #
  # If the above options are not used, the normal Redis Cluster auto-detection
  # will be used instead.
  #
  # Note that when remapped, the bus port may not be at the fixed offset of
  # clients port + 10000, so you can specify any port and bus-port depending
  # on how they get remapped. If the bus-port is not set, a fixed offset of
  # 10000 will be used as usually.
  #
  # Example:
  #
  # cluster-announce-ip 10.1.1.5
  # cluster-announce-port 6379
  # cluster-announce-bus-port 6380
   
  ################################## SLOW LOG ###################################
   
  # The Redis Slow Log is a system to log queries that exceeded a specified
  # execution time. The execution time does not include the I/O operations
  # like talking with the client, sending the reply and so forth,
  # but just the time needed to actually execute the command (this is the only
  # stage of command execution where the thread is blocked and can not serve
  # other requests in the meantime).
  #
  # You can configure the slow log with two parameters: one tells Redis
  # what is the execution time, in microseconds, to exceed in order for the
  # command to get logged, and the other parameter is the length of the
  # slow log. When a new command is logged the oldest one is removed from the
  # queue of logged commands.
   
  # The following time is expressed in microseconds, so 1000000 is equivalent
  # to one second. Note that a negative number disables the slow log, while
  # a value of zero forces the logging of every command.
  slowlog-log-slower-than 10000
   
  # There is no limit to this length. Just be aware that it will consume memory.
  # You can reclaim memory used by the slow log with SLOWLOG RESET.
  slowlog-max-len 128
   
  ################################ LATENCY MONITOR ##############################
   
  # The Redis latency monitoring subsystem samples different operations
  # at runtime in order to collect data related to possible sources of
  # latency of a Redis instance.
  #
  # Via the LATENCY command this information is available to the user that can
  # print graphs and obtain reports.
  #
  # The system only logs operations that were performed in a time equal or
  # greater than the amount of milliseconds specified via the
  # latency-monitor-threshold configuration directive. When its value is set
  # to zero, the latency monitor is turned off.
  #
  # By default latency monitoring is disabled since it is mostly not needed
  # if you don't have latency issues, and collecting data has a performance
  # impact, that while very small, can be measured under big load. Latency
  # monitoring can easily be enabled at runtime using the command
  # "CONFIG SET latency-monitor-threshold <milliseconds>" if needed.
  latency-monitor-threshold 0
   
  ############################# EVENT NOTIFICATION ##############################
   
  # Redis can notify Pub/Sub clients about events happening in the key space.
  # This feature is documented at http://redis.io/topics/notifications
  #
  # For instance if keyspace events notification is enabled, and a client
  # performs a DEL operation on key "foo" stored in the Database 0, two
  # messages will be published via Pub/Sub:
  #
  # PUBLISH __keyspace@0__:foo del
  # PUBLISH __keyevent@0__:del foo
  #
  # It is possible to select the events that Redis will notify among a set
  # of classes. Every class is identified by a single character:
  #
  #  K     Keyspace events, published with __keyspace@<db>__ prefix.
  #  E     Keyevent events, published with __keyevent@<db>__ prefix.
  #  g     Generic commands (non-type specific) like DEL, EXPIRE, RENAME, ...
  #  $     String commands
  #  l     List commands
  #  s     Set commands
  #  h     Hash commands
  #  z     Sorted set commands
  #  x     Expired events (events generated every time a key expires)
  #  e     Evicted events (events generated when a key is evicted for maxmemory)
  #  A     Alias for g$lshzxe, so that the "AKE" string means all the events.
  #
  #  The "notify-keyspace-events" takes as argument a string that is composed
  #  of zero or multiple characters. The empty string means that notifications
  #  are disabled.
  #
  #  Example: to enable list and generic events, from the point of view of the
  #           event name, use:
  #
  #  notify-keyspace-events Elg
  #
  #  Example 2: to get the stream of the expired keys subscribing to channel
  #             name __keyevent@0__:expired use:
  #
    notify-keyspace-events Ex
  #
  #  By default all notifications are disabled because most users don't need
  #  this feature and the feature has some overhead. Note that if you don't
  #  specify at least one of K or E, no events will be delivered.
  #notify-keyspace-events ""
   
  ############################### ADVANCED CONFIG ###############################
   
  # Hashes are encoded using a memory efficient data structure when they have a
  # small number of entries, and the biggest entry does not exceed a given
  # threshold. These thresholds can be configured using the following directives.
  hash-max-ziplist-entries 512
  hash-max-ziplist-value 64
   
  # Lists are also encoded in a special way to save a lot of space.
  # The number of entries allowed per internal list node can be specified
  # as a fixed maximum size or a maximum number of elements.
  # For a fixed maximum size, use -5 through -1, meaning:
  # -5: max size: 64 Kb  <-- not recommended for normal workloads
  # -4: max size: 32 Kb  <-- not recommended
  # -3: max size: 16 Kb  <-- probably not recommended
  # -2: max size: 8 Kb   <-- good
  # -1: max size: 4 Kb   <-- good
  # Positive numbers mean store up to _exactly_ that number of elements
  # per list node.
  # The highest performing option is usually -2 (8 Kb size) or -1 (4 Kb size),
  # but if your use case is unique, adjust the settings as necessary.
  list-max-ziplist-size -2
   
  # Lists may also be compressed.
  # Compress depth is the number of quicklist ziplist nodes from *each* side of
  # the list to *exclude* from compression.  The head and tail of the list
  # are always uncompressed for fast push/pop operations.  Settings are:
  # 0: disable all list compression
  # 1: depth 1 means "don't start compressing until after 1 node into the list,
  #    going from either the head or tail"
  #    So: [head]->node->node->...->node->[tail]
  #    [head], [tail] will always be uncompressed; inner nodes will compress.
  # 2: [head]->[next]->node->node->...->node->[prev]->[tail]
  #    2 here means: don't compress head or head->next or tail->prev or tail,
  #    but compress all nodes between them.
  # 3: [head]->[next]->[next]->node->node->...->node->[prev]->[prev]->[tail]
  # etc.
  list-compress-depth 0
   
  # Sets have a special encoding in just one case: when a set is composed
  # of just strings that happen to be integers in radix 10 in the range
  # of 64 bit signed integers.
  # The following configuration setting sets the limit in the size of the
  # set in order to use this special memory saving encoding.
  set-max-intset-entries 512
   
  # Similarly to hashes and lists, sorted sets are also specially encoded in
  # order to save a lot of space. This encoding is only used when the length and
  # elements of a sorted set are below the following limits:
  zset-max-ziplist-entries 128
  zset-max-ziplist-value 64
   
  # HyperLogLog sparse representation bytes limit. The limit includes the
  # 16 bytes header. When an HyperLogLog using the sparse representation crosses
  # this limit, it is converted into the dense representation.
  #
  # A value greater than 16000 is totally useless, since at that point the
  # dense representation is more memory efficient.
  #
  # The suggested value is ~ 3000 in order to have the benefits of
  # the space efficient encoding without slowing down too much PFADD,
  # which is O(N) with the sparse encoding. The value can be raised to
  # ~ 10000 when CPU is not a concern, but space is, and the data set is
  # composed of many HyperLogLogs with cardinality in the 0 - 15000 range.
  hll-sparse-max-bytes 3000
   
  # Streams macro node max size / items. The stream data structure is a radix
  # tree of big nodes that encode multiple items inside. Using this configuration
  # it is possible to configure how big a single node can be in bytes, and the
  # maximum number of items it may contain before switching to a new node when
  # appending new stream entries. If any of the following settings are set to
  # zero, the limit is ignored, so for instance it is possible to set just a
  # max entires limit by setting max-bytes to 0 and max-entries to the desired
  # value.
  stream-node-max-bytes 4096
  stream-node-max-entries 100
   
  # Active rehashing uses 1 millisecond every 100 milliseconds of CPU time in
  # order to help rehashing the main Redis hash table (the one mapping top-level
  # keys to values). The hash table implementation Redis uses (see dict.c)
  # performs a lazy rehashing: the more operation you run into a hash table
  # that is rehashing, the more rehashing "steps" are performed, so if the
  # server is idle the rehashing is never complete and some more memory is used
  # by the hash table.
  #
  # The default is to use this millisecond 10 times every second in order to
  # actively rehash the main dictionaries, freeing memory when possible.
  #
  # If unsure:
  # use "activerehashing no" if you have hard latency requirements and it is
  # not a good thing in your environment that Redis can reply from time to time
  # to queries with 2 milliseconds delay.
  #
  # use "activerehashing yes" if you don't have such hard requirements but
  # want to free memory asap when possible.
  activerehashing yes
   
  # The client output buffer limits can be used to force disconnection of clients
  # that are not reading data from the server fast enough for some reason (a
  # common reason is that a Pub/Sub client can't consume messages as fast as the
  # publisher can produce them).
  #
  # The limit can be set differently for the three different classes of clients:
  #
  # normal -> normal clients including MONITOR clients
  # replica  -> replica clients
  # pubsub -> clients subscribed to at least one pubsub channel or pattern
  #
  # The syntax of every client-output-buffer-limit directive is the following:
  #
  # client-output-buffer-limit <class> <hard limit> <soft limit> <soft seconds>
  #
  # A client is immediately disconnected once the hard limit is reached, or if
  # the soft limit is reached and remains reached for the specified number of
  # seconds (continuously).
  # So for instance if the hard limit is 32 megabytes and the soft limit is
  # 16 megabytes / 10 seconds, the client will get disconnected immediately
  # if the size of the output buffers reach 32 megabytes, but will also get
  # disconnected if the client reaches 16 megabytes and continuously overcomes
  # the limit for 10 seconds.
  #
  # By default normal clients are not limited because they don't receive data
  # without asking (in a push way), but just after a request, so only
  # asynchronous clients may create a scenario where data is requested faster
  # than it can read.
  #
  # Instead there is a default limit for pubsub and replica clients, since
  # subscribers and replicas receive data in a push fashion.
  #
  # Both the hard or the soft limit can be disabled by setting them to zero.
  client-output-buffer-limit normal 0 0 0
  client-output-buffer-limit replica 256mb 64mb 60
  client-output-buffer-limit pubsub 32mb 8mb 60
   
  # Client query buffers accumulate new commands. They are limited to a fixed
  # amount by default in order to avoid that a protocol desynchronization (for
  # instance due to a bug in the client) will lead to unbound memory usage in
  # the query buffer. However you can configure it here if you have very special
  # needs, such us huge multi/exec requests or alike.
  #
  # client-query-buffer-limit 1gb
   
  # In the Redis protocol, bulk requests, that are, elements representing single
  # strings, are normally limited ot 512 mb. However you can change this limit
  # here.
  #
  # proto-max-bulk-len 512mb
   
  # Redis calls an internal function to perform many background tasks, like
  # closing connections of clients in timeout, purging expired keys that are
  # never requested, and so forth.
  #
  # Not all tasks are performed with the same frequency, but Redis checks for
  # tasks to perform according to the specified "hz" value.
  #
  # By default "hz" is set to 10. Raising the value will use more CPU when
  # Redis is idle, but at the same time will make Redis more responsive when
  # there are many keys expiring at the same time, and timeouts may be
  # handled with more precision.
  #
  # The range is between 1 and 500, however a value over 100 is usually not
  # a good idea. Most users should use the default of 10 and raise this up to
  # 100 only in environments where very low latency is required.
  hz 10
   
  # Normally it is useful to have an HZ value which is proportional to the
  # number of clients connected. This is useful in order, for instance, to
  # avoid too many clients are processed for each background task invocation
  # in order to avoid latency spikes.
  #
  # Since the default HZ value by default is conservatively set to 10, Redis
  # offers, and enables by default, the ability to use an adaptive HZ value
  # which will temporary raise when there are many connected clients.
  #
  # When dynamic HZ is enabled, the actual configured HZ will be used as
  # as a baseline, but multiples of the configured HZ value will be actually
  # used as needed once more clients are connected. In this way an idle
  # instance will use very little CPU time while a busy instance will be
  # more responsive.
  dynamic-hz yes
   
  # When a child rewrites the AOF file, if the following option is enabled
  # the file will be fsync-ed every 32 MB of data generated. This is useful
  # in order to commit the file to the disk more incrementally and avoid
  # big latency spikes.
  aof-rewrite-incremental-fsync yes
   
  # When redis saves RDB file, if the following option is enabled
  # the file will be fsync-ed every 32 MB of data generated. This is useful
  # in order to commit the file to the disk more incrementally and avoid
  # big latency spikes.
  rdb-save-incremental-fsync yes
   
  # Redis LFU eviction (see maxmemory setting) can be tuned. However it is a good
  # idea to start with the default settings and only change them after investigating
  # how to improve the performances and how the keys LFU change over time, which
  # is possible to inspect via the OBJECT FREQ command.
  #
  # There are two tunable parameters in the Redis LFU implementation: the
  # counter logarithm factor and the counter decay time. It is important to
  # understand what the two parameters mean before changing them.
  #
  # The LFU counter is just 8 bits per key, it's maximum value is 255, so Redis
  # uses a probabilistic increment with logarithmic behavior. Given the value
  # of the old counter, when a key is accessed, the counter is incremented in
  # this way:
  #
  # 1. A random number R between 0 and 1 is extracted.
  # 2. A probability P is calculated as 1/(old_value*lfu_log_factor+1).
  # 3. The counter is incremented only if R < P.
  #
  # The default lfu-log-factor is 10. This is a table of how the frequency
  # counter changes with a different number of accesses with different
  # logarithmic factors:
  #
  # +--------+------------+------------+------------+------------+------------+
  # | factor | 100 hits   | 1000 hits  | 100K hits  | 1M hits    | 10M hits   |
  # +--------+------------+------------+------------+------------+------------+
  # | 0      | 104        | 255        | 255        | 255        | 255        |
  # +--------+------------+------------+------------+------------+------------+
  # | 1      | 18         | 49         | 255        | 255        | 255        |
  # +--------+------------+------------+------------+------------+------------+
  # | 10     | 10         | 18         | 142        | 255        | 255        |
  # +--------+------------+------------+------------+------------+------------+
  # | 100    | 8          | 11         | 49         | 143        | 255        |
  # +--------+------------+------------+------------+------------+------------+
  #
  # NOTE: The above table was obtained by running the following commands:
  #
  #   redis-benchmark -n 1000000 incr foo
  #   redis-cli object freq foo
  #
  # NOTE 2: The counter initial value is 5 in order to give new objects a chance
  # to accumulate hits.
  #
  # The counter decay time is the time, in minutes, that must elapse in order
  # for the key counter to be divided by two (or decremented if it has a value
  # less <= 10).
  #
  # The default value for the lfu-decay-time is 1. A Special value of 0 means to
  # decay the counter every time it happens to be scanned.
  #
  # lfu-log-factor 10
  # lfu-decay-time 1
   
  ########################### ACTIVE DEFRAGMENTATION #######################
  #
  # WARNING THIS FEATURE IS EXPERIMENTAL. However it was stress tested
  # even in production and manually tested by multiple engineers for some
  # time.
  #
  # What is active defragmentation?
  # -------------------------------
  #
  # Active (online) defragmentation allows a Redis server to compact the
  # spaces left between small allocations and deallocations of data in memory,
  # thus allowing to reclaim back memory.
  #
  # Fragmentation is a natural process that happens with every allocator (but
  # less so with Jemalloc, fortunately) and certain workloads. Normally a server
  # restart is needed in order to lower the fragmentation, or at least to flush
  # away all the data and create it again. However thanks to this feature
  # implemented by Oran Agra for Redis 4.0 this process can happen at runtime
  # in an "hot" way, while the server is running.
  #
  # Basically when the fragmentation is over a certain level (see the
  # configuration options below) Redis will start to create new copies of the
  # values in contiguous memory regions by exploiting certain specific Jemalloc
  # features (in order to understand if an allocation is causing fragmentation
  # and to allocate it in a better place), and at the same time, will release the
  # old copies of the data. This process, repeated incrementally for all the keys
  # will cause the fragmentation to drop back to normal values.
  #
  # Important things to understand:
  #
  # 1. This feature is disabled by default, and only works if you compiled Redis
  #    to use the copy of Jemalloc we ship with the source code of Redis.
  #    This is the default with Linux builds.
  #
  # 2. You never need to enable this feature if you don't have fragmentation
  #    issues.
  #
  # 3. Once you experience fragmentation, you can enable this feature when
  #    needed with the command "CONFIG SET activedefrag yes".
  #
  # The configuration parameters are able to fine tune the behavior of the
  # defragmentation process. If you are not sure about what they mean it is
  # a good idea to leave the defaults untouched.
   
  # Enabled active defragmentation
  # activedefrag yes
   
  # Minimum amount of fragmentation waste to start active defrag
  # active-defrag-ignore-bytes 100mb
   
  # Minimum percentage of fragmentation to start active defrag
  # active-defrag-threshold-lower 10
   
  # Maximum percentage of fragmentation at which we use maximum effort
  # active-defrag-threshold-upper 100
   
  # Minimal effort for defrag in CPU percentage
  # active-defrag-cycle-min 5
   
  # Maximal effort for defrag in CPU percentage
  # active-defrag-cycle-max 75
   
  # Maximum number of set/hash/zset/list fields that will be processed from
  # the main dictionary scan
  # active-defrag-max-scan-fields 1000
  ```

  vim 命令粘贴进去，以上已经修改好

  - 开启redis验证  可选

    requirepass 123

  - 允许redis外地连接 必须

    注释掉 # bind 127.0.0.1

  - 将daemonize yes注释起来或者 daemonize no设置，因为该配置和docker run中-d参数冲突，会导致容器一直启动失败  必须

  - 开启redis数据持久化 appendonly yes 可选

### 使用redis6.0.8镜像创建容器(也叫运行镜像)

```
docker run  -p 6379:6379 --name myr3 --privileged=true -v /app/redis/redis.conf:/etc/redis/redis.conf -v /app/redis/data:/data -d redis:6.0.8 redis-server /etc/redis/redis.conf
docker ps
docker exec -it kmyr3 /bin/bash
redis-cli
set k1 v1
get k1
ping
```

这一步创建容器的时候，可能出错，名字已经被一个容器占用，可以使用以下命令删除对应的容器

```
docker ps -a
docker rm 3874ac36fb2e
```

- 请证明docker启动使用了我们自己指定的配置文件

  - 修改前

  ```
  select 15
  ```

  ![](https://img-blog.csdnimg.cn/53467e8e5da74305adfc23ac494220bd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  我们用的配置文件，数据库默认是16个

  - 修改后

    我们用vim 修改databases 10

    ![](https://img-blog.csdnimg.cn/1b1b60b23d984f49961eb6c3fb56fe9c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  - 重启redis 服务

    ```
    docker restart myr3
    docker exec -it myr3 /bin/bash
    redis-cli
    get k1
    select 3
    select 15 b
    ```

    ![](https://img-blog.csdnimg.cn/dfda4be8bfc647beb72d7235f478337e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

