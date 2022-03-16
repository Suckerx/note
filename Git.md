# Git教程

- Git 版本：v2.35.1

# Git

## 概述

- Git是一个免费的、开源的分布式版本控制系统 ，可以快速高效地处理从小型到大型的各种项目

- Git易于学习，占地面积小，性能 极快 。 它具有廉价的本地 库 ，方便的暂存区域和多个工作
  流分支等特性。 其性能优于 Subversion、 CVS、 Perforce和 ClearCase等 版本控制 工具。

- 官网地址：http://git-scm.com/
  

## 版本控制

- 版本控制是一种记录文件内容变化，以便将来查阅特定版本修订情况的系统。
- 版本控制其实最重要的是可以记录文件修改历史记录，从而让用户能够查看历史版本，方便版本切换

## 版本控制工具

- 集中式版本控制工具
  - CVS、SVN、VSS
  - 集中化的版本控制系统诸如 CVS、SVN 等，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。多年以来，这已成为版本控制系统的标准做法。
  - 这种做法带来了许多好处，每个人都可以在一定程度上看到项目中的其他人正在做些什么。而管理员也可以轻松掌控每个开发者的权限，并且管理一个集中化的版本控制系统，要远比在各个客户端上维护本地数据库来得轻松容易。
  - 事分两面，有好有坏。这么做显而易见的缺点是中央服务器的单点故障。如果服务器宕机一小时，那么在这一小时内，谁都无法提交更新，也就无法协同工作。

![](https://img-blog.csdnimg.cn/f5e24d96fff44af3af782f4b6a8166d2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

------

- 分布式版本控制工具
  - Git、Mercurial、Bazaar、Darcs…
  - 像 Git 这种分布式版本控制工具，客户端提取的不是最新版本的文件快照，而是把代码仓库完整地镜像下来（本地库）。这样任何一处协同工作用的文件发生故障，事后都可以用其他客户端的本地仓库进行恢复。因为每个客户端的每一次文件提取操作，实际上都是一次对整个文件仓库的完整备份。
  - 分布式的版本控制系统出现之后,解决了集中式版本控制系统的缺陷：
    - 服务器断网的情况下也可以进行开发（因为版本控制是在本地进行的）
    - 每个客户端保存的也都是整个完整的项目（包含历史记录，更加安全）

## Git简史

![](https://img-blog.csdnimg.cn/c831b1d58b7940a38c9e5386a830ba6b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## Git工作机制

![](https://img-blog.csdnimg.cn/62cf62f40828486297ed357c4de57cf6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## Git和代码托管中心

代码托管中心是基于网络服务器的远程代码仓库，一般我们简单称为远程库

➢ 局域网 

- ✓ GitLab 

➢ 互联网 

- ✓ GitHub（外网）
- ✓ Gitee 码云（国内网站）

# Git安装

- 官网地址：http://git-scm.com/

最好安装在自己电脑开发或者环境目录下

Git 选项配置，推荐默认设置，然后下一步。

![](https://img-blog.csdnimg.cn/b01f311505cf42e497e0449f54b0498f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

Git安装目录名，不用修改，直接点击下一步。

![](https://img-blog.csdnimg.cn/6d00705bf6be4a98b47bcb23bfc8ef88.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

Git 的默认编辑器，建议使用默认的 Vim 编辑器，然后点击下一步。

![](https://img-blog.csdnimg.cn/29241c690ca6433fa7f3a6609f61074d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

默认分支名设置，选择让Git决定，分支名默认为 master，下一步。

![](https://img-blog.csdnimg.cn/d4e18d4ad1b547b28a68745520268914.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

调整你的 path 环境变量，这里选择的是第二种的推荐方式

第一种是仅从 Git Bash 使用 Git。这个的意思就是你只能通过 Git 安装后的 Git Bash 来使用 Git ，其他的什么命令提示符啊等第三方软件都不行。

第二种是从命令行以及第三方软件进行 Git。这个就是在第一种基础上进行第三方支持，你将能够从 Git Bash，命令提示符(cmd) 和 Windows PowerShell 以及可以从 Windows 系统环境变量中寻找 Git 的任何第三方软件中使用 Git。推荐使用这个。

第三种是从命令提示符使用 Git 和可选的 Unix 工具。选择这种将覆盖 Windows 工具，如 “ find 和 sort ”。只有在了解其含义后才使用此选项。一句话，适合比较懂的人折腾。


![](https://img-blog.csdnimg.cn/e3738cb1d73243958564ca7f4049d124.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

选择后台客户端连接协议，选默认值OpenSSL，然后下一步。

![](https://img-blog.csdnimg.cn/9db60d9b8bb743c9886dc2d6fe04c672.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

配置Git文件的行末换行符， Windows使用 CRLF Linux使用 LF，选择第一个自动转换，然后继续下一步。

![](https://img-blog.csdnimg.cn/f205b161495b48d289aa7573617f9961.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

选择Git终端类型，选择默认的 Git Bash终端，然后继续下一步。

![](https://img-blog.csdnimg.cn/0de44e67d183477184156ce09502e66c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

选择Git pull合并的模式，选择默认，然后下一步。

![](https://img-blog.csdnimg.cn/350b3fd98c894236b3600a44e170ecf7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

选择Git的凭据管理器，选择默认 的跨平台的凭据管理器 ，然后下一步 。

![](https://img-blog.csdnimg.cn/0862357d9e6646eaa4fd73524167b813.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

其他配置，选择默认设置，然后下一步。

![](https://img-blog.csdnimg.cn/37b9e4908d134579b5ab26f12da748ee.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

实验室功能，技术还不成熟， 有已知的 bug，不要勾选，然后点击右下角的 Install按钮，开始安装 Git

![](https://img-blog.csdnimg.cn/6fd52eb3c6a946e892b8567838acaad1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

点击Finsh按钮， Git安装成功！

右键任意位置，在右键菜单里选择Git Bash Here即可打开 Git Bash命令行终端。在Git Bash终端里输入 `git --version`查看 git版本，如图所示，说明 Git安装成功。

![](https://img-blog.csdnimg.cn/4759b4612f524bbf872ce980d9638a5b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_12,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/91467f6568e14e47853ec0808aac7ddc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

# Git常用命令

|               命令名称                |        作用        |
| :-----------------------------------: | :----------------: |
| git config --global user.name 用户名  |    设置用户签名    |
|  git config --global user.email 邮箱  |    设置用户签名    |
|             **git init**              |  **初始化本地库**  |
|            **git status**             | **查看本地库状态** |
|          **git add 文件名**           |  **添加到暂存区**  |
| **git commit -m " 日志信息 " 文件名** |  **提交到本地库**  |
|            **git reflog**             |  **查看历史记录**  |
|      **git reset --hard 版本号**      |    **版本穿梭**    |

## 设置用户签名

基本语法

- `git config --global user.name` 用户名
- `git config --global user.email` 邮箱
- 注意这里要设置和github一样的用户名和邮箱否则没有小绿点

查看

- git config --global user.name
- git config --global user.email

在C:\Users\扶苏目录下下有个 `.gitconfig` 文件，打开里面就是我们设置的用户签名

说明：

签名的作用是区分不同操作者身份。用户的签名信息在每一个版本的提交信息中能够看到，以此确认本次提交是谁做的。Git首次安装必须设置一下用户签名，否则无法提交代码。

注意：这里设置用户签名和将来登录 GitHub（或其他代码托管中心）的账号没有任何关系。

## 初始化本地库

基本语法：`git init`

在项目目录下，右键打开git bash即可进入该目录，使用命令git init可以创建本地库

![](https://img-blog.csdnimg.cn/8b695a176d1343b2b71d384162b2db35.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/e8067b7cb3334bfaa4ccba047f7d559a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 添加暂存区

### 将工作区的文件添加到暂存区

基本语法：`git add 文件名 或者用 git add .`   . 表示全部

![](https://img-blog.csdnimg.cn/96da0a5e8433491e818f2392656da379.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 提交本地库

### 将工作区的文件提交到本地库

基本语法：`git commit -m "日志信息" 文件名`

若是所有文件就不指定文件名

git commit -m "first commit"

![](https://img-blog.csdnimg.cn/955b22525f324341b202f21d3102b64b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

提交完可以使用`git status`查看状态，可以使用`git reflog`查看历史记录（包含版本号的前七位），`git log`查看完整日志信息

## 修改文件

语法：`vim 文件名`

![](https://img-blog.csdnimg.cn/4d36176b05f9491f833c068307d3bc35.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

提交后查看状态

![](https://img-blog.csdnimg.cn/8b7e5d50cdbb45689f4afc0136f19ee0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 历史版本

### 查看历史版本

基本语法：

- `git reflog` 查看版本信息
- `git log` 查看版本详细信息

### 版本穿梭

语法：`git reset --hard 版本号`

![](https://img-blog.csdnimg.cn/245474242856479cbf89eed65c03df98.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 切换版本原理

Git 切换版本，底层其实是移动的HEAD 指针，具体原理如下图所示

HEAD 指针指向 master 分支，master分支指向 first 版本，

![](https://img-blog.csdnimg.cn/e19248de68e64b86840fd780a7b03300.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

之后有了 second 版本，master 指针指向 second 版本

如果我们想穿越回去，只需要让 master 指针指向 first 版本或者 second 版本

# Git分支

## 什么是分支

- 在版本控制过程中，同时推进多个任务，为每个任务，我们就可以创建每个任务的单独分支
- 使用分支意味着程序员可以把自己的工作从开发主线上分离开来，开发自己分支的时候，不会影响主线分支的运行
- 对于初学者而言，分支可以简单理解为副本，一个分支就是一个单独的副本

## 分支的好处

- 同时并行推进多个功能开发，提高开发效率。
- 各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可

## 分支的操作

|      命令名称       |             作用             |
| :-----------------: | :--------------------------: |
|  git branch 分支名  |           创建分支           |
|    git branch -v    |           查看分支           |
| git checkout 分支名 |           切换分支           |
|  git merge 分支名   | 把指定的分支合并到当前分支上 |

### 查看分支

基本语法：`git branch -v`

### 创建分支

基本语法：`git branch 分支名`

### 切换分支

基本语法:`git checkout 分支名`

![](https://img-blog.csdnimg.cn/2896ec03637c4a8fb7107ca11c4e6ad8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 修改分支

![](https://img-blog.csdnimg.cn/d4d95d896c2940f090a04d2271cde4c5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 合并分支

基本语法：`git merge 分支名`,

将指定分支合并到当前分支

#### ①正常合并不冲突

```
git checkout master
git merge hot-fix
cat hello.txt
```

![](https://img-blog.csdnimg.cn/7efd3b1ecdfd43ea906d80e25f317689.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

#### ②合并产生冲突

冲突产生的原因：

- 合并分支时，两个分支在同一个文件的同一个位置有两套完全不同的修改。
- 有两套完全不同的修改。 Git无法替我们决定使用哪一个。必须 人为 决定新代码内容。

例如，我们首先在 master 分支的倒数第二行进行修改，并将其添加到暂存区，再提交到本地库

![](https://img-blog.csdnimg.cn/5bf80557277e4ce1b07f61d54e36993a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

接着，我们去 hot-fix 分支的倒数第一行进行修改，并将其添加到暂存区，再提交到本地库

![](https://img-blog.csdnimg.cn/c26f84a9badd4a1cab022fc1409a5b55.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

之后我们在 master 分支上合并 hot-fix 分支，发现产生冲突

![](https://img-blog.csdnimg.cn/7dbdac180145441eb3a82c981116796b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 解决冲突

1. 编辑有冲突的文件，删除特殊符号，决定要使用的内容

   特殊符号：`<<<<<< HEAD` 当前分支的代码 `=======` 合并过来的代码 `>>>>>>>hot-fix`

![](https://img-blog.csdnimg.cn/31869a48f399461baf094a19d04db162.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/96b25e90535f401c8873e14f5cfbd6ec.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

删除完成之后保存，再次添加到暂存区，并再次提交到本地库(**注意：此时使用 git commit 命令时候不能带文件名**)

![](https://img-blog.csdnimg.cn/c8006d75bce844a189b8a59d4430711b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

创建分支和切换分支图解

![](https://img-blog.csdnimg.cn/b8c94263ea3344f084e7d452fa73c1bb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

master、hot-fix 其实都是指向具体版本记录的指针。当前所在的分支，其实是由 HEAD 决定的。所以创建分支的本质就是多创建一个指针。 

HEAD 如果指向 master，那么我们现在就在 master 分支上。 

HEAD 如果执行 hotfix，那么我们现在就在 hotfix 分支上

# Git团队协作机制

## 团队内协作

![](https://img-blog.csdnimg.cn/f7b89352dcb4491596a8a09baaad8d73.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 跨团队协作

![](https://img-blog.csdnimg.cn/e4081956c0f645a28e2fd1bac08a4efa.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

令狐冲请东方不败改代码，东方不败通过 fork 命令从岳不群的的远程库中拿取代码，再通过 clone 克隆命令到自己的本地库，修改完成后使用 push 推送到在自己的远程库，使用 Pull request 拉取请求给岳不群，岳不群审核完成后使用 merge 命令合并对方的代码到自己的远程库中，再通过 pull 命令到自己的本地库中，这样修改过后的华山剑法岳不群和令狐冲就都可以使用了。

# Github

## 创建远程仓库

### Github远程仓库

GitHub 网址：https://github.com

![](https://img-blog.csdnimg.cn/fbab665edf764b2f87bb8b2f5429292e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/8e0ba70d610f4b0f8d41cef5abbe3bdb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_18,color_FFFFFF,t_70,g_se,x_16)

## 远程仓库操作

|                命令名称                |                             作用                             |
| :------------------------------------: | :----------------------------------------------------------: |
|             git remote -v              |                   查看当前所有远程地址别名                   |
|      git remote add 别名 远程地址      |                            起别名                            |
|         **git push 别名 分支**         |              **推送本地分支上的内容克隆到本地**              |
|         **git clone 远程地址**         |                **将远程仓库的内容克隆到本地**                |
| **git pull 远程库地址别名 远程分支名** | **将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并** |

### 创建远程仓库别名

基本语法：

- `git remote -v` 查看当前所有远程地址别名
- `git remote add 别名 远程地址` 起别名

![](https://img-blog.csdnimg.cn/1b22f7dc319340cb98443a6dba86f5bc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

注意：起的别名最好和本地库的名称一致

![](https://img-blog.csdnimg.cn/ab70750a361a4c5dadfa88bf8fe9c4bc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 推送本地分支到远程仓库

基本语法：`git push 别名 分支`

没有起别名可以直接用链接

![](https://img-blog.csdnimg.cn/24b7dfb3d85d4a978c31c3882d3a0508.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

第一个选项是通过浏览器的账号登录，本次使用第二种方式，with a code

登录成功授权后

![](https://img-blog.csdnimg.cn/bd189092a8314c84a3d7f0cfe11dd1a6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/5d011afd30264e70a73a5f728d8fd659.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 拉取远程库分支到本地库

语法：`git pull 别名 分支`

### 克隆远程仓库到本地

基本语法：`git clone 远程地址`

我们另一台用户需要克隆我们的远程仓库到他的本地库，由于是使用一台电脑模拟，所以在克隆之前需要在 凭据管理器下删除我们之前的 git 凭据

![](https://img-blog.csdnimg.cn/6675e6a38e064fe3ab7f5cae0fee505e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们新建一个文件夹 git-clone，然后在此文件夹下右键 git bash here，之后进行克隆

![](https://img-blog.csdnimg.cn/ba9c4a175a4543898bbbe961c4bc2147.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

克隆完成后初始化本地仓库

clone 会做如下操作。1、拉取代码。2、初始化本地仓库。3、创建别名

![](https://img-blog.csdnimg.cn/faa101c50b3c4202be8651a9f5706b21.png)

## 邀请加入团队

选择邀请合作者

![](https://img-blog.csdnimg.cn/8bbf8b70c51f457a9d39a0bad483efa6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

复 制 地 址 并 通 过 微 信 钉 钉 等 方 式 发 送 给 该 用 户 ， 复 制 内 容 如 下 ： https://github.com/atguiguyueyue/git-shTest/invitations

![](https://img-blog.csdnimg.cn/18ed2a76a45a401a8d33cbd4b0be3420.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

接收邀请的人在自己账号中的地址栏，粘贴链接点击接收邀请

![](https://img-blog.csdnimg.cn/6eb597a1804c404c8399c5a294fdbeb2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_13,color_FFFFFF,t_70,g_se,x_16)

成功之后可以 这个账号上看到 guli_parent1 的远程仓库。

此时可以进行推送代码等操作

## 跨团队协作

将远程仓库的地址复制发给邀请跨团队协作的人，比如东方不败。

在 东方不败的 GitHub账号里的地址栏复制收到的链接，然后点击 Fork将项目叉到自己的仓库

此时东方不败的账号就有一个仓库，此时可以clone后在本地改

东方不败可以在线编辑叉取过来的文件。编辑完毕后，填写描述信息并点击左下角绿色按钮提交。

此时可以点击Pull Request按钮

![](https://img-blog.csdnimg.cn/1da93c14101846bda1f7c24e052757c1.png)

点击new pull request

![](https://img-blog.csdnimg.cn/f9b9d62143a745bbbeed898656cdfbf7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

创建后，在主账号中看到Pull Request按钮中有提示，点开看

![](https://img-blog.csdnimg.cn/e09f043334f64557bcf0570d88fcacb3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

审核后可以合并代码

![](https://img-blog.csdnimg.cn/ac8053c01ad44430ac66b2dc819ba554.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## SSH免密登录

在 C盘 User 自己的账户下右键 git bash here，`ssh-keygen -t rsa -C 自己的邮箱签名`

C:\Users\扶苏

![](https://img-blog.csdnimg.cn/11b4623c5b7c4cdbae0a8716397bc8e6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

这样就会生成 .ssh 文件夹，里面有私钥和公钥

进入.ssh目录复制公钥

![](https://img-blog.csdnimg.cn/6fc55ce67f774d35bfd60767811145c8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

复制公钥，打开github，在设置中，打开SSH

![](https://img-blog.csdnimg.cn/5a00468768364689b52d698f72938feb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

这样我们可以借助 ssh 链接来拉取和推送代码，并且不需要进行登录

![](https://img-blog.csdnimg.cn/654adb5dc53f41ea88f8871da1e2a5fc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

# IDEA集成Git

## 配置Git忽略文件

我们的[Eclipse](https://so.csdn.net/so/search?q=Eclipse&spm=1001.2101.3001.7020) 、IDEA都会生成一些无关文件，如图

![](https://img-blog.csdnimg.cn/e2d35ef9d6c14180a638edfcf455d1b2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_13,color_FFFFFF,t_70,g_se,x_16)

我们之所以要忽略他们，是因为他们与项目的实际功能无关，不参与服务器上部署运行。如何忽略他们？

1. 创建忽略规则文件 xxxx.ignore（前缀名随便起，建议是 git.ignore）

   这个文件的存放位置原则上在哪里都可以，为了便于让~/.gitconfig 文件引用，建议也放在用户家目录下

   C:\Users\扶苏

   ```
   # Compiled class file
   *.class
   
   # Log file
   *.log
   
   # BlueJ files
   *.ctxt
   
   # Mobile Tools for Java (
   .mtj.
   
   # Package Files
   *.jar
   *.war
   *.nar
   *.ear
   *.zip
   *.tar.gz
   *.rar
   
   # virtual machine crash logs, see
   http://www.java.com/en/download/help/error_hotspot.xml
   hs_err_pid*
   
   .classpath
   .project
   .settings
   target
   .idea
   *.iml
   ```

2. 在 .gitconfig 文件中引用忽略配置文件(.gitconfig 在家目录中)

   注意复制路径时要改反斜杠

   ![](https://img-blog.csdnimg.cn/836f824cb85d4babafdf6f152d148d81.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

   ```
   [core]
   	excludesfile = C:/Users/Augenestern/git.ignore
   ```

3. 在 IDEA 里面定位

   ![](https://img-blog.csdnimg.cn/01b113ce1850438793e16dd34e8728e9.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## IDEA初始化本地库

点击VCS

![](https://img-blog.csdnimg.cn/e1917f95f34e4ef5913905b78fb49382.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_10,color_FFFFFF,t_70,g_se,x_16)

默认创建的 git 仓库就是我们打开的项目所在的目录，我们添加了 git 仓库之后

![](https://img-blog.csdnimg.cn/c39e75c7fcc648d99cc20e1f77167ffc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/6e2f58e206fb478cbef4340e628aac4c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

添加到暂存区就变为了绿色，我们可以写些代码，然后将 project 添加到暂存区

![](https://img-blog.csdnimg.cn/622df192010d4764a462709cbf8e736c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们添加到暂存区，再接着进行提交到本地库

![](https://img-blog.csdnimg.cn/f29cd0f9e5664b418739e993db972676.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/3b6a73fd79c74c63958d14a1a8ddc174.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

之后代码文件都会变成正常黑色

## 切换版本

我们修改 GitTest 中的代码，再次添加暂存区（已经追踪过（就是已经添加过暂存区的）的文件也可以不用），提交到本地库

![](https://img-blog.csdnimg.cn/59f949a735ba4a86b9b2a192cd2ecbfe.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

在IDEA的左下角，点击 Git，然后点击 Log查看版本，右键选择要切换的版本，然后在菜单里点击 Checkout Revision

![](https://img-blog.csdnimg.cn/731cde859420453492a4f5813aeb2318.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/29cfa2b3e6cf459d9e12c4e25c636a70.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 创建分支

右键项目 -> Git -> Branches

![](https://img-blog.csdnimg.cn/f122cda9b8a64fe295d73a64b8a38d66.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

在弹出的Git Branches框里 点击 New Branch按钮。

![](https://img-blog.csdnimg.cn/ce8ea12370bb425ca6db8d0ddff26477.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

填写分支名称

![](https://img-blog.csdnimg.cn/5e1badd382534ad1b560d90f1ec3adec.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

然后再 IDEA的右下角看到 hot-fix，说明分支创建成功，并且当前已经切换成 hot-fix

![](https://img-blog.csdnimg.cn/93f9c23912a240949097834ab60e3831.png)

## 切换分支

在IDEA窗口的右下角，切换到 master分支 。

![](https://img-blog.csdnimg.cn/a9236a01f3d84efa9f45a3c7ecc7e833.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 合并分支

在IDEA窗口的右下角，将 hot-fix分支合并到当前 master分支。

![](https://img-blog.csdnimg.cn/f37dda4638a04051b718280e402a02fc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_18,color_FFFFFF,t_70,g_se,x_16)

如果代码没有冲突，分支直接合并成功，分支合并成功以后，代码自动提交，无需手动提交本地库

## 合并分支冲突

如图所示，如果master分支和 hot-fix分支都修改了代码，在合并分支的时候就会发生冲突。

![](https://img-blog.csdnimg.cn/8449ad92a74b411ca4b1ebbaac276ea4.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/5793dd2fde384aab873ccd6dc677a436.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们现在站在master分支上合并 hot-fix分支，就会发生代码冲突。

点击 Conflicts框里的 Merge按钮，进行手动合并代码。

![](https://img-blog.csdnimg.cn/9ff0a2a2964547abaf0b639b0856a778.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/f63b9b055bb64266a7a532369c04cf63.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

点击这两个X后进行合并，手动合并完代码以后，点击右下角的 Apply按钮。代码冲突解决，自动提交本地库。

![](https://img-blog.csdnimg.cn/0c5969326c3c434696c33bc88a3f228c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

# IDEA集成Github

打开设置

![](https://img-blog.csdnimg.cn/e4408d7cd7c64b97afc1745383f397c1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

点击add Acount后弹窗

![](https://img-blog.csdnimg.cn/d2ead230d9314344a72e38637e21f6fe.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

也可以使用Token和账号密码登录，但是一般账号密码登录不进，所以使用Token，在Github的Settings中，找到Developer Settings，点击Personal access tokens，生成新口令，取名，权限拉满，复制口令（刷新就没了）

## 分享项目到Github

![](https://img-blog.csdnimg.cn/a9672075925e49548c16561c8cc9136d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_10,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/af6e7b989b404339a12e27f9c7c4c218.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_14,color_FFFFFF,t_70,g_se,x_16)

## push推送本地库到远程库

右键点击项目，可以将当前分支的内容 push 到 GitHub的远程仓库中 。

先修改，然后提交，再push

![](https://img-blog.csdnimg.cn/86a8c9d6c31f4ece9c8fc42f7fbe456a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

使用ssh进行push

![](https://img-blog.csdnimg.cn/6bdea4f08f854f94ba8d4f7d02b6bb66.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

成功

![](https://img-blog.csdnimg.cn/57d88639c8f04411bf55a31bfa96f087.png)

![](https://img-blog.csdnimg.cn/0323590e3a394e3494ac3d0b6aa14848.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## pull拉取远程库到本地库

注意：push是将本地库代码推送到远程库，如果本地库代码跟远程库代码版本不一致，push的操作是会被拒绝的。也就是说， 要想 push成功，一定要保证本地 库的版本要比远程库的版本高！ 因此一个成熟的程序员在动手改本地代码之前，一定会先检查下远程库跟本地代码的区别！如果本地的代码版本已经落后，切记要先 pull拉取一下远程库的代码，将本地代码更新到最新以后，然后再修改，提交，推送！

- 右键点击项目，可以将远程仓库的内容pull到本地仓库 。

![](https://img-blog.csdnimg.cn/4ae6c3d8b8e2462d9175b0ad0420e42d.png)

## clone克隆远程库到本地库

因为前面push了代码了，现在把本地的代码文件夹直接删掉，然后打开IDEA，选择

![](https://img-blog.csdnimg.cn/4324abb937e243a48432036ec76f69e5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

选择Git，用ssh链接

![](https://img-blog.csdnimg.cn/cb442db12c5e493687fd6735e0e3d50b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

# 国内代码托管中心-码云

## 简介

众所周知，GitHub 服务器在国外，使用 GitHub 作为项目托管网站，如果网速不好的话， 严重影响使用体验，甚至会出现登录不上的情况。针对这个情况，大家也可以使用国内的项 目托管网站-码云

码云是开源中国推出的基于 Git 的代码托管服务中心，网址是 https://gitee.com/ ，使用 方式跟 GitHub 一样，而且它还是一个中文网站，如果你英文不是很好它是最好的选择。

## 登录注册

注册成功后登录

## 码云创建远程库

点击首页右上角的加号，选择下面的新建仓库

填写仓库名称，路径和选择是否开源（共开库或私有库）

最后根据需求选择分支模型，然后点击创建按钮。

# IDEA集成Gitee

## IDEA安装码云插件

Idea 默认不带码云插件，我们第一步要安装 Gitee插件。

![](https://img-blog.csdnimg.cn/67daa7988a944894b371b22247537037.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

安装完成重启 IDEA 即可

Idea连接码云和连接 GitHub几乎一样，首先在 Idea里面创建一个工程，初始化 git工程，然后将代码添加到暂存区，提交到本地库。

![](https://img-blog.csdnimg.cn/6811e8cbd5d44f6eb4425f49513fe41a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 分享项目到Gitee

在上方栏目Git中选择Share

![](https://img-blog.csdnimg.cn/a7b883012e63416f907388358edd3a70.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_15,color_FFFFFF,t_70,g_se,x_16)

## push推送到码云远程库

当然我们也可以自己在码云Gitee上创建远程库，然后获取到远程库的 HTTPS/SSH 链接，将我们的代码 push 即可

自定义远程库链接： Define remote，给远程库链接定义个 name，然后再 URL里面填入码云远程库的 HTTPS链接即可，码云服务器在国内，用 HTTPS 链接即可，没必要用 SSH 免密链接

![](https://img-blog.csdnimg.cn/d779cbf27c8b4a5c84c2512870a56433.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## pull拉取远程库到本地库

我们在远程库修改代码，然后使用本地库 pull 拉取远程库的代码

## clone克隆远程库到本地库

与GitHub一模一样

# 码云复制Github项目

码云提供了直接复制 GitHub 项目的功能，方便我们做项目的迁移和下载 。

![](https://img-blog.csdnimg.cn/b2747f743f3942e3986aa7bab18c9e28.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

将 GitHub的远程库 HTTPS链接复制过来，点击创建按钮即可。

如果GitHub项目更新了以后，在码云项目端可以手动重新同步，进行更新！

![](https://img-blog.csdnimg.cn/b18e24533c0d47ceb3dbe7b6ac33af53.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

