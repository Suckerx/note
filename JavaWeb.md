## JavaWeb

## JavaWeb基本概念

### 前言

web开发：

- web，网页，www.baidu.com
- 静态web
  - heml，css
  - 提供给所有人看的数据始终不会发生变化
- 动态web
  - 提供给所有人看的数据始终会发生变化，每个人在不同的时间，不同地点，看到的信息各不相同
  - 技术栈：Servlet/Jsp，ASP，PHP

在Java中，动态web资源开发的技术统称为JavaWeb

### web应用程序

web应用程序：可以提供浏览器访问的程序；

- a.html、b.html...多个web资源，这些web资源可以被外界访问，对外界提供服务
- 能访问的任何一个页面或资源，都存在于这个世界上的某一计算机上
- 通过URL
- 这个统一的web资源会被放在同一个文件夹下就是web应用程序 -> Tomcat：服务器
- 一个web应用由多部份组成（静态web，动态web）
  - html，css，js
  - jsp，servlet
  - java程序
  - jar包
  - 配置文件（Properties）

web应用程序编写完毕后，若想提供给外界访问：需要一个服务器来统一管理；

### 静态web

- `*.htm`，`*.html`这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取。

![](https://img-blog.csdnimg.cn/a971d5965c994483b6e477f9e9ffeac5.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

- 静态web存在的缺点
  - Web页面无法动态更新，所有用户看到的都是同一个页面
    - 轮播图，点击特效：伪动态
    - JavaScript
    - VBScript
  - 它无法和数据库交互（数据无法持久化，用户无法交互）

### 动态web

页面会动态展示：“Web的页面展示效果因人而异”

![](https://img-blog.csdnimg.cn/02ebdeb14aa8471fb107d4c82eaa8723.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

缺点：

- 假如服务器动态web资源出现错误，需要重新编写**后台程序**，重新发布；
  - 停机维护

优点：

- Web页面可以动态更新，所有用户看到的都不是同一个页面
- 它可以和数据库交互（数据持久化：注册，商品信息，用户信息）

![](https://img-blog.csdnimg.cn/22233413a9e74c54aa33ff6d531fade6.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

## Web服务器

### 技术讲解

ASP：

- 微软：国内最早流行的就是ASP
- 在HTML中嵌入了VB的脚本，ASP+COM；
- 在ASP开发中，基本一个页面

PHP：

- PHP开发速度很快，功能很强大，跨平台，代码简单
- 无法承载大访问量的情况（局限性）

JSP/Servlet：

B/S：浏览和服务器

C/S：客户端和服务器

- sun公司主推的B/S架构
- 基于java语言（大公司，开源组件，都是用java写的）
- 可以承载三高问题带来的影响
- 语法像ASP

### web服务器

服务器是一种被动的操作，用来处理用户的一些请求和给用户一些响应信息；

IIS

微软；ASP...Windows中自带

**Tomcat**

![](https://img1.baidu.com/it/u=2749996974,2004673340&fm=26&fmt=auto&gp=0.jpg)

Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现，因为Tomcat 技术先进、性能稳定，而且免费，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用[服务器](https://baike.baidu.com/item/服务器)，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个JavaWeb初学者来说，它是最佳的选择

Tomcat 实际上运行JSP 页面和Servlet。目前Tomcat最新版本为10.0.5**。**

下载Tomcat：

1. 安装 or 解压
2. 了解配置文件及目录结构
3. 这个东西的作用

## Tomcat

### 下载解压

### 	Tomcat启动

文件夹作用：

![](https://img-blog.csdnimg.cn/8cd1428985734b069706c6bfc69018a3.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

**启动/关闭Tomcat**

bin目录下：startup.bat文件双击启动，shutdown.bat关闭

访问测试：http://localhost:8080/

可能遇到的问题：

1. java环境变量未配置
2. 闪退问题：需要配置兼容性
3. 乱码问题：配置文件中设置

### 配置

![](https://img-blog.csdnimg.cn/f6cbbd0449a0408f9dbe2bc834b7df6e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

可以配置启动的端口号

- Tomcat默认端口号：8080
- mysql：3306
- http: 80
- https：443

```xml
<Connector port="8081" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443"
```

可以配置主机的名称

- 默认的主机名为：localhost -> 127.0.0.1
- 默认网站应用存放的位置：webapps

```xml
<Host name="www.Sucker.com"  appBase="webapps"
      unpackWARs="true" autoDeploy="true"></Host>
```

**高难度面试题：**

请你谈谈网站是如何进行访问的！

1. 输入一个域名然后回车

2. 检查本机的 C:\Windows\System32\drivers\etc\hosts配置文件下有没有这个域名映射；

   1. 有：直接返回对应的ip地址，这个地址中，有我们需要访问的web程序，可以直接访问

      ```java
      127.0.0.1        www.Sucker.com
      ```

   2. 没有：去DNS服务器找，找到就返回，找不到就返回找不到

![](https://img-blog.csdnimg.cn/82d7703679dd4144920d883c78218531.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

可以配置环境变量(自由选择)

## 发布一个web网站

模仿

- 将自己写的网站，放到服务器（Tomcat）中指定的web应用的文件夹下（webapps）下就可以访问

网站应该有的结构

```java
--webapps : Tomcat服务器的web目录
    -ROOT
    -suckerstudy : 网站的目录名
        - WEB-INF
        	-classes : java程序
             -lib : web应用所依赖的jar包
        	-web.xml
        - index.html 默认的首页
        - static
            -css
                 -style.css
            -js
            -img
        -....
```

## HTTP

### 概述

超文本传输协议（Hyper Text Transfer Protocol，HTTP）是一个简单的请求-响应协议，它通常运行在[TCP](https://baike.baidu.com/item/TCP/33012)之上。

- 文本：html，字符串,...
- 超文本：图片，音乐，视频，定位，地图....
- 默认端口：80

Https：安全的

- 443

### 两个时代

- http1.0
  - HTTP/1.0：客户端可以与web服务器连接后，只能获得一个web资源后断开连接
- http2.0
  - HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源

### Http请求

- 客户端---发请求---服务器

百度：

```java
Request URL: https://www.baidu.com/
Request Method: GET
Status Code: 200 OK //状态码
Remote Address: 14.215.177.39:443  //远程地址
引用站点策略: unsafe-url
```

```java
Accept: text/html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6 //语言
Cache-Control: max-age=0
Connection: keep-alive
```

请求行：

- 请求行中的请求方式：GET
- 请求方式：**Get，Post**，HEAD,DELETE,PUT,TRACT...
  - get：请求能携带的参数比较少，大小有限制，会在浏览器的URL地址栏显示数据内容，不安全，但高效
  - post：请求能携带的参数没有限制，大小没有限制，不会在浏览器的URL地址栏显示数据内容，安全，但不高效

消息头：

```java
Accept：支持的数据类型
Accept-Encoding：支持的编码格式（GBK，UTF-8，GB2312）
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完是断开还是保持连接
```



### Http响应

- 服务器---响应---客户端

百度：

```java
Cache-Control: private  //缓存控制
Connection: keep-alive  //连接
Content-Encoding: gzip  //编码
Content-Type: text/html;charset=utf-8 //类型
```

响应体：

```java
Accept：支持的数据类型
Accept-Encoding：支持的编码格式（GBK，UTF-8，GB2312）
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完是断开还是保持连接
Refresh：告诉客户端，多久刷新一次
Location：让网页重新定位
```

响应状态码

- 200：请求响应成功
- 3xx：请求重定向
  - 重定向：你重新到我给你的新位置去
- 4xx：找不到资源  404
  - 资源不存在；
- 5xx：服务器代码错误  500  502：网关错误

## Maven

为什么要学习这个技术？

1. 在javaweb开发中，需要使用大量的jar包，需要手动导入

2. 让一个东西自动帮我导入和配置这个jar包

   由此，Maven诞生了！

### Maven项目架构管理工具

我们目前用来方便导入jar包

Maven的核心思想：**约定大于配置**

- 有约束，不要去违反

Maven会规定好你该如何去编写我们的java代码，必须按照这个规范来；

### 下载安装Maven

下载完成后解压即可

### 配置环境变量

在系统环境变量中配置如下配置：

- M2_HOME   maven目录下的bin目录
- MAVEN_HOME   maven的目录
- 在系统的path中配置MAVEN_HOME  %MAVEN_HOME%\bin

测试Maven是否安装成功：在cmd下输入mvn -version

### 修改配置文件为阿里云镜像

- 镜像：mirrors

  - 作用：加速下载

- 国内建议使用阿里云镜像

  ```java
  <mirror>
      <id>alimaven</id>
      <name>aliyun maven</name>
      <url>
      http://maven.aliyun.com/nexus/content/groups/public/
  </url>
      <mirrorOf>central</mirrorOf>        
      </mirror>
  ```

### 本地仓库

有本地仓库和远程仓库

建立一个本地仓库：新建空文件夹或去网上下载本地仓库

```java
<localRepository>D:\maven-localwarehouse\repository</localRepository>
```

### 在IDEA中使用Maven

1. 启动IDEA

2. 创建一个MavenWeb项目

   ![](https://img-blog.csdnimg.cn/8c089084dd024dac9d2d93ea630ebe0b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

   ![](https://img-blog.csdnimg.cn/320f950cb12b4e80bb311cc2fd002d5b.png)

   ![](https://img-blog.csdnimg.cn/98e071c830b146df93f5843d56b21394.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

   ![](https://img-blog.csdnimg.cn/f162a10fff6540fa98ec1e92699b9db3.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

3. 等待项目自动导入包，导入成功后若初始时是建立空文件夹则会出现jar包

4. IDEA中的Maven设置

   IDEA项目创建成功后，注意看Maven的配置，有时在IDEA中会出现一个问题，项目自动创建完成后，它会使用IDEA默认的MAVENHOME，要手动改成本地

### 创建一个普通的Maven项目

![](https://img-blog.csdnimg.cn/e49455abc40f4ac685d848a8a328b25b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/2c56a47c19e944c1a7e0ac015e33822e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

这个只有在web应用下才有

![](https://img-blog.csdnimg.cn/3adc3f46b1d2481da69a84a0c8fba792.png)

### 标记文件夹功能

先把建好的javaweb项目目录补全，加上java和resource文件夹

![](https://img-blog.csdnimg.cn/77fed3e2451841caa221bde645a65ec0.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

将java文件夹标记为源码目录，resource变为资源目录

![](https://img-blog.csdnimg.cn/d4dd22d19dea4ecdb25776d1e788aec6.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

也可以在这里面调文件夹属性

![](https://img-blog.csdnimg.cn/2722c3dd52744230b6e3d6aad248c421.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### 在IDEA中配置Tomcat

![](https://img-blog.csdnimg.cn/68560fab0d17446da9ee21926f2d92d3.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/5fa8b901623d4ed6a23c227c5a335d39.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/d545917eb81d4a7aaef08fb3df600fc6.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

解决warning：新建时选择第一个

![](https://img-blog.csdnimg.cn/4daffb6a69864ebca03c4ca5267f66ad.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/338b22bf95334555a45069abbbf0eaef.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

此时写的是/Sucker

启动Tomcat：

![](https://img-blog.csdnimg.cn/de78b1b8840a464ebf422d552a8adc48.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/d2bb95f199d844d4a1d0544643f40063.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### pom文件

pom.xml 是Maven的核心配置文件

![](https://img-blog.csdnimg.cn/60090ba6b2fe4153a86bc5e028e26031.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--Maven版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!--这里是刚才配置的GAV-->
  <groupId>com.Sucker</groupId>
  <artifactId>javaweb-01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
  <!--Package:项目的打包方式
  jar：java应用
  war：JavaWeb应用
  -->
  <packaging>war</packaging>

  <!--配置-->
  <properties>
    <!--项目的默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--编码版本-->
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <!--项目依赖-->
  <dependencies>
    <!--具体依赖的jar包配置文件-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <!--项目构建用的东西-->
  <build>
    <finalName>javaweb-01-maven</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

![](https://img-blog.csdnimg.cn/8d0614dc734d41f181ccf683f46f5a56.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

Maven由于他的约定大于配置，我们之后可能遇到我们写的配置文件，无法被导出或者生效的问题

在build中配置resources，防止资源导出失败的问题

```xml
    <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>

            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>

            </resource>
        </resources>
    </build>
```

![](https://img-blog.csdnimg.cn/f230c8ea328d4ae19b7de1ef7ff76a6b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### IDEA操作

查看目录树：Maven中jar包的关联图

![](https://img-blog.csdnimg.cn/66ac1dcd192b4fa4924502a2774d13ef.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### 解决遇到的问题

1. Maven 3.6.2：Unable to import maven project：See logs for detailes

   解决方法：降级，目前3.8未发现错误

2. Tomcat闪退

3. IDEA每次都要重复配置Maven

   在IDEA中的全局默认配置中去配置

   ![](https://img-blog.csdnimg.cn/7e4e090960574dc2995359a11cae9621.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

   配置全局

   ![](https://img-blog.csdnimg.cn/3813574f9e7c4bbd9d388918532f1acc.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

4. Maven项目中Tomcat无法配置

5. Maven默认web项目中web.xml版本问题

   ![](https://img-blog.csdnimg.cn/530ef90b7499473f84c58c411de3cfef.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

6. 替换为webapp4.0版本和Tomcat一致  web.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0"
            metadata-complete="true">
   
   </web-app>
   ```

7. Maven仓库的使用

   ![](https://img-blog.csdnimg.cn/0824a2ea133b4a34912b73a10ffed048.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

地址：https://mvnrepository.com/

去官网中搜寻jar包可以下载下来，也可以将对应的<dependency>复制到pom文件的<dependencies>中，可以将provided作用域删掉

8. 一个Servlet

   ```java
   package com.Sucker.servlet;
   
   import javax.servlet.ServletException;
   import javax.servlet.http.HttpServlet;
   import javax.servlet.http.HttpServletRequest;
   import javax.servlet.http.HttpServletResponse;
   import java.io.IOException;
   import java.io.PrintWriter;
   
   public class HelloServlet extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse response) throws ServletException, IOException {
           //响应的类型：html
           response.setContentType("text/html");
           response.setCharacterEncoding("utf-8");
           //获取响应的输出流
           PrintWriter out = response.getWriter();
           out.println("<html>");
           out.println("<head>");
           out.println("<title>Hello World!</title>");
           out.println("</head>");
           out.println("<body>");
           out.println("<h1>你好!</h1>");
           out.println("</body>");
           out.println("</html>");
   
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           super.doPost(req, resp);
       }
   }
   ```

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0"
            metadata-complete="true">
   
       <!--web.xml中是配置我们web的核心应用-->
       <!--注册Servlet-->
       <servlet>
           <servlet-name>helloServlet</servlet-name>
           <servlet-class>com.Sucker.servlet.HelloServlet</servlet-class>
       </servlet>
       <!--一个Servlet对应一个Mapping：映射-->
       <servlet-mapping>
           <servlet-name>helloServlet</servlet-name>
           <!--请求路径-->
           <url-pattern>/aaaa</url-pattern>  // 请求路径
       </servlet-mapping>
   
   
   </web-app>
   ```

   启动Tomcat后在后缀写上aaaa即可跳转到你好！

## Servlet

### Servlet简介

- Servlet是sun公司开发动态web的一门技术
- Sun公司在这些API中提供了一个接口：Servlet，如果你想开发一个Servlet程序，只需要完成两个小步骤：
  - 编写一个类，实现Servlet接口
  - 把开发好的Java类部署到web服务器中

**把实现了Servlet接口的Java程序叫作，Servlet**

### HelloServlet

Servlet接口Sun公司有两个默认的实现类：HttpServlet，GenericServlet

1. 构建一个普通Maven项目，删掉里面的src目录，以后学习就在这个项目里面建立Module；这个空的工程就是Maven主工程；

2. 关于Maven父子工程的理解：

   父项目中会有：

   ```xml
   <modules>
       <module>servlet-01</module>
   </modules>
   ```

   子项目中会有（没有就自己添加）：

   ```xml
   <parent>
       <artifactId>javaweb-02-servlet</artifactId>
       <groupId>com.Sucker</groupId>
       <version>1.0-SNAPSHOT</version>
   </parent>
   ```

   父项目中的java子项目可以直接使用

   ```java
   son extends father
   ```

3. 将web..xml替换为最新版本

4. 构建Maven项目结构：添加java和resource文件夹（main下）

5. 编写一个Servlet程序

   - 编写一个普通类

   - 实现Servlet接口，这里直接继承HttpServlet

     ```java
     package com.Sucker.servlet;
     
     import javax.servlet.ServletException;
     import javax.servlet.http.HttpServlet;
     import javax.servlet.http.HttpServletRequest;
     import javax.servlet.http.HttpServletResponse;
     import java.io.IOException;
     import java.io.PrintWriter;
     
     public class HelloServlet extends HttpServlet {
     
         //由于get或post只是请求实现的不同方式，可以相互调用，业务逻辑都一样
         @Override
         protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
             PrintWriter writer = resp.getWriter(); //响应流
             writer.println("HelloServlet");
     
         }
     
         @Override
         protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
         }
     }
     ```

6. 编写Servlet的映射

   为什么需要映射：我们写的是Java程序，但是需要通过浏览器访问，而浏览器需要连接web服务器，所以需要在web服务中注册我们写的Servlet，还需要给它一个浏览器能够访问的路径；

   ```xml
   <!--注册Servlet-->
   <servlet>
       <servlet-name>hello</servlet-name>
       <servlet-class>com.Sucker.servlet.HelloServlet</servlet-class>
   </servlet>
   <!--Servlet的映射路径（请求路径）-->
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello</url-pattern>
   </servlet-mapping>
   ```

7. 配置Tomcat

   注意配置项目发布路径

8. 启动测试

### Servlet原理

Servlet是由Web服务器调用，web服务器在收到浏览器请求后，会

![](https://img-blog.csdnimg.cn/806712f77afd49afada0ed9650b55ad3.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### Mapping问题

1. 一个Servlet可以指定一个映射路径

   ```xml
   <!--Servlet的映射路径（请求路径）-->
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello</url-pattern>
   </servlet-mapping>
   ```

2. 一个Servlet可以指定多个映射路径

   ```xml
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello</url-pattern>
   </servlet-mapping>
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello2</url-pattern>
   </servlet-mapping>
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello3</url-pattern>
   </servlet-mapping>
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello4</url-pattern>
   </servlet-mapping>
   ```

3. 一个Servlet可以指定通用映射路径

   直接写/hello能进入HelloServlet，后面加/fdhajigj（任意字符都能进入）

   ```xml
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello/*</url-pattern>
   </servlet-mapping>
   ```

4. 默认请求路径

   此时会跳过index.jsp文件的首页HelloWorld直接进入HelloServlet

   ```xml
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/*</url-pattern>
   </servlet-mapping>
   ```

5. 指定一些后缀或者前缀

   ```xml
   <！--可以自定义后缀实现请求映射
    注意点，*前面不能加项目映射路径
    hello/fajnig.Sucker都可以
   -->
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>*.Sucker</url-pattern>
   </servlet-mapping>
   ```

6. 优先级问题

   指定了固有的映射路径优先级最高，如果找不到就会走默认的处理请求；

   ```xml
   <!--404-->
   <servlet>
       <servlet-name>error</servlet-name>
       <servlet-class>com.Sucker.servlet.ErrorServlet</servlet-class>
   </servlet>
   <servlet-mapping>
       <servlet-name>error</servlet-name>
       <url-pattern>/*</url-pattern>
   </servlet-mapping>
   ```

   ```java
   package com.Sucker.servlet;
   public class ErrorServlet extends HttpServlet {
   
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           resp.setContentType("text/html");
           resp.setCharacterEncoding("utf-8");
   
           PrintWriter writer = resp.getWriter();
           writer.print("<h1>404</h1>");
   
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           super.doPost(req, resp);
       }
   }
   ```

   Tomcat的Artifact用哪个打包哪个比较好

   **此时为了修改Tomcat控制台中文乱码问题，将tomcat目录下conf目录下logging文件中的UTF-8改为了GBK，若以后出现问题可修改回来**

### ServletContext

web容器在启动的时候，它会为每个web程序都创建一个对应的ServletContnext对象，它代表了当前的web应用

#### 共享数据

在这个servlet中保存的数据，可以在另一个servlet中拿到

放置数据：

```java
package com.Sucker.servlet;

public class HelloServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

//        this.getInitParameter()  初始化参数
//        this.getServletConfig()  Servlet配置
//        this.getServletContext()  Servlet上下文
        ServletContext context = this.getServletContext();

        String username = "张三"; // 数据
        context.setAttribute("username",username); // 将一个数据保存在ServletContext中，名字为 username ，值为 username

        System.out.println("hello");
    }

}
```

读取数据：

```java
package com.Sucker.servlet;

public class GetServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        String username = (String) context.getAttribute("username");

        resp.setContentType("text/html");
        resp.setCharacterEncoding("utf-8");
        resp.getWriter().print("名字"+username);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //doGet();
    }
}
```

配置web.xml

```xml
<servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>com.Sucker.servlet.HelloServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>

<servlet>
    <servlet-name>getc</servlet-name>
    <servlet-class>com.Sucker.servlet.GetServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>getc</servlet-name>
    <url-pattern>/getc</url-pattern>
</servlet-mapping>
```

测试访问结果：要先访问放置数据的页面才能读取到数据

#### 获取初始化参数

```xml
<!--配置一些web应用初始化参数-->
<context-param>
    <param-name>url</param-name>
    <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
</context-param>
```

```java
package com.Sucker.servlet;

public class ServletDemo03 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();

        String url = context.getInitParameter("url"); // 获得初始化参数
        resp.getWriter().print(url);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //doGet();
    }
}
```

#### 请求转发

转发能携带参数

```java
package com.Sucker.servlet;

public class ServletDemo04 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        System.out.println("进入了ServletDemo04");
//        RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp");//转发的请求路径
//        requestDispatcher.forward(req,resp); // 调用forward 转发请求
        context.getRequestDispatcher("/gp").forward(req, resp);
        // 路径不变

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //doGet();
    }

}
```

```xml
<servlet>
    <servlet-name>sd4</servlet-name>
    <servlet-class>com.Sucker.servlet.ServletDemo04</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>sd4</servlet-name>
    <url-pattern>/sd4</url-pattern>
</servlet-mapping>
```

请求转发：A->B ，B->C，C返回东西给B，B再返回给A，A不知道有C，路径不变，还是B的

而重定向：A->B ，B返回给A让他去找C，A->C，C返回给A，路径变

#### 读取资源文件

Properties

- 在java目录下新建properties，此时需要配置build在当前项目的xml中，避免导入失败
- 在resources目录下新建properties

发现：都被打包到了同一个路径下：target-->项目-->WEB-INF-->classes，俗称类路径classpath；

思路：需要一个文件流

```properties
username = root
password = 123456
```

```java
package com.Sucker.servlet;

public class ServletDemo05 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/db.properties");// / 代表当前web项目

        Properties prop = new Properties();
        prop.load(is);
        String user = prop.getProperty("username");
        String pwd = prop.getProperty("password");

        resp.getWriter().print(user+":"+pwd);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

### HttpServletResponse

web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表响应的HttpServletResponse；

- 如果要获取客户端请求过来的参数：找HttpServletRequest
- 如果要给客户端响应一些信息：找HttpServletResponse

#### 简单分类

**负责向浏览器发送数据的方法**

```java
ServletOutputStream getOutputStream() throws IOException;
PrintWriter getWriter() throws IOException;
```

**负责向浏览器发送响应头的方法**

```java
void setCharacterEncoding(String var1);

void setContentLength(int var1);

void setContentLengthLong(long var1);

void setContentType(String var1);

void setDateHeader(String var1, long var2);

void addDateHeader(String var1, long var2);

void setHeader(String var1, String var2);

void addHeader(String var1, String var2);

void setIntHeader(String var1, int var2);

void addIntHeader(String var1, int var2);
```

响应的状态码

```java
    int SC_CONTINUE = 100;
    int SC_SWITCHING_PROTOCOLS = 101;
    int SC_OK = 200;
    int SC_CREATED = 201;
    int SC_ACCEPTED = 202;
    int SC_NON_AUTHORITATIVE_INFORMATION = 203;
    int SC_NO_CONTENT = 204;
    int SC_RESET_CONTENT = 205;
    int SC_PARTIAL_CONTENT = 206;
    int SC_MULTIPLE_CHOICES = 300;
    int SC_MOVED_PERMANENTLY = 301;
    int SC_MOVED_TEMPORARILY = 302;
    int SC_FOUND = 302;
    int SC_SEE_OTHER = 303;
    int SC_NOT_MODIFIED = 304;
    int SC_USE_PROXY = 305;
    int SC_TEMPORARY_REDIRECT = 307;
    int SC_BAD_REQUEST = 400;
    int SC_UNAUTHORIZED = 401;
    int SC_PAYMENT_REQUIRED = 402;
    int SC_FORBIDDEN = 403;
    int SC_NOT_FOUND = 404;
    int SC_METHOD_NOT_ALLOWED = 405;
    int SC_NOT_ACCEPTABLE = 406;
    int SC_PROXY_AUTHENTICATION_REQUIRED = 407;
    int SC_REQUEST_TIMEOUT = 408;
    int SC_CONFLICT = 409;
    int SC_GONE = 410;
    int SC_LENGTH_REQUIRED = 411;
    int SC_PRECONDITION_FAILED = 412;
    int SC_REQUEST_ENTITY_TOO_LARGE = 413;
    int SC_REQUEST_URI_TOO_LONG = 414;
    int SC_UNSUPPORTED_MEDIA_TYPE = 415;
    int SC_REQUESTED_RANGE_NOT_SATISFIABLE = 416;
    int SC_EXPECTATION_FAILED = 417;
    int SC_INTERNAL_SERVER_ERROR = 500;
    int SC_NOT_IMPLEMENTED = 501;
    int SC_BAD_GATEWAY = 502;
    int SC_SERVICE_UNAVAILABLE = 503;
    int SC_GATEWAY_TIMEOUT = 504;
    int SC_HTTP_VERSION_NOT_SUPPORTED = 505;
```

#### 常见应用

1. 向浏览器输出消息（前面有）
2. 下载文件
   - 要获取下载文件的路径
   - 下载的文件名是啥
   - 设置让浏览器能够支持下载我们需要的东西
   - 获取下载文件的输入流
   - 创建缓冲区
   - 获取OutputStream对象
   - 将FileOutputStream流写入到buffer缓冲区
   - 使用OutputStream将缓冲区中的数据输出到客户端！

```java
package com.Sucker.servlet;

import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.FileInputStream;
import java.io.IOException;
import java.net.URLEncoder;

public class FileServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        - 要获取下载文件的路径,要从target里面找那个图片的路径
        String realPath = "D:\\JavaCode\\JavaWeb\\javaweb-02-servlet\\response\\target\\classes\\加藤惠.png";
        System.out.println("下载的问题路径为："+realPath);
//        - 下载的文件名是啥
        String fileName = realPath.substring(realPath.lastIndexOf("\\") + 1); // 一个/ 需要转义
//        - 设置让浏览器能够支持(Content-Disposition)下载我们需要的东西,中文文件名用URLEncoder.encode(fileName,"utf-8")编码，否则有可能乱码
        resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(fileName,"utf-8"));
//        - 获取下载文件的输入流
        FileInputStream in = new FileInputStream(realPath);
//        - 创建缓冲区
        int len=0;
        byte[] buffer = new byte[1024];
//        - 获取OutputStream对象
        ServletOutputStream out = resp.getOutputStream();
//        - 将FileInputStream流写入到buffer缓冲区 - 使用OutputStream将缓冲区中的数据输出到客户端！
        while((len=in.read(buffer))!=-1){
            out.write(buffer);
        }
        in.close();
        out.close();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

#### 验证码功能

验证怎么来的？

- 前端实现

- 后端实现，需要用到java的图片类，生成一个图片

  ```java
  package com.Sucker.servlet;
  
  import javax.imageio.ImageIO;
  import javax.servlet.ServletException;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import javax.swing.*;
  import java.awt.*;
  import java.awt.image.BufferedImage;
  import java.io.IOException;
  import java.util.Random;
  
  public class ImageServlet extends HttpServlet {
  
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
  
          //如何让浏览器 3 秒自动刷新一次
          resp.setHeader("refresh","3");
  
          //在内存中创建一个图片
          BufferedImage image = new BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);
          //得到图片
          Graphics2D g = (Graphics2D) image.getGraphics(); // 相当于笔
          //设置图片的背景颜色
          g.setColor(Color.white);
          g.fillRect(0,0,80,20); // 从(0，0)到(80，20)
          //给图片写数据
          g.setColor(Color.BLUE);
          g.setFont(new Font(null,Font.BOLD,20));//设置样式
          g.drawString(makeNum(),0,20); // 画一个字符串
  
          //告诉浏览器，这个请求用图片的方式打开
          resp.setContentType("image/jpeg");
          //网站存在缓存，不让浏览器缓存
          resp.setDateHeader("expires",-1);
          resp.setHeader("Cache-Control","no-cache");
          resp.setHeader("Pragma","no-cache");
  
          //把图片写给浏览器
          ImageIO.write(image,"jpg",resp.getOutputStream())
  
      }
  
      //生成随机数
      public String makeNum(){
          Random random = new Random();
          String num = random.nextInt(99999999) + "";
          StringBuffer sb = new StringBuffer();
          for (int i = 0; i < 7 - num.length(); i++) { // 保证7位数
              sb.append("0");
          }
          num = sb.toString()+num;
          return num;
      }
  
  
      @Override
      protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          doGet(req, resp);
      }
  }
  ```

#### 实现重定向

B一个web资源收到客户端A请求后，B会通知A客户端去访问另一个web资源C，这个过程叫重定向

常见场景：

- 用户登录

  ```java
  void sendRedirect(String var1) throws IOException;
  ```

  ```java
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
      /**
           * resp.setHeader("Location","/response_war/img")
           * resp.setStatus(302)
           */
      resp.sendRedirect("/response_war/img");
  }
  ```

面试题：聊聊重定向和转发的区别？

相同点：

- 页面都会跳转

不同点：

- 请求转发的时候，url不会发生变化
- 重定向时，url地址栏会发生变化

用户登录+重定向Success

```java
package com.Sucker.servlet;

public class RequestTest extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //处理请求
        String username = req.getParameter("username");
        String password = req.getParameter("password");

        System.out.println(username+":"+password);

        //重定向时候要注意路径问题，否则404
        resp.sendRedirect("/r/success.jsp");

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

webapp目录下新建jsp文件

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 扶苏
  Date: 2021/8/9
  Time: 11:54
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>

<h1>Success</h1>

</body>
</html>

```

更改首页为登录界面

```jsp
<html>
<body>
<h2>Hello World!</h2>

<%--这里提交的路径，需要寻找到项目的路径--%>
<%--${pageContext.request.contextPath()}代表当前项目路径--%>
<form action="${pageContext.request.contextPath}/login" method="get">
    用户名：<input type="text" name="username"> <br>
    密码：<input type="password" name="password"> <br>
    <input type="submit">
</form>

</body>
</html>

```

注意导入jsp包和web.xml配置

### HttpServletRequest

HttpServletRequest代表客户端的请求，用户通过Http协议访问服务器，Http请求中的所有信息会被封装到HttpServletRequest，通过这个HttpServletRequest的方法，可以获得用户端的所有信息；

#### 获取参数，请求转发

![](https://img-blog.csdnimg.cn/8c501736dbc548b38fe79f580f76365b.png)

```java
package com.Sucker.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Arrays;

public class LoginServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //解决接收和响应中文乱码
        resp.setCharacterEncoding("utf-8");
        req.setCharacterEncoding("utf-8");

        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String[] hobbies = req.getParameterValues("hobbies");
        System.out.println(username);
        System.out.println(password);
        System.out.println(Arrays.toString(hobbies));

        //通过请求转发
        //这里的/代表当前web应用
        req.getRequestDispatcher("/success.jsp").forward(req,resp);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

index.jsp删掉重新建，改为：

```jsp
.<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>登录</title>
</head>
<body>

<h1>登录</h1>

<div>
    <%--这里表单表示的意思：以post方式提交表单，提交到login请求--%>
    <form action="${pageContext.request.contextPath}/login" method="post">
        用户名：<input type="text" name="username"> <br>
        密码：<input type="password" name="password"> <br>
        爱好：
        <input type="checkbox" name="hobbies" value="女孩">女孩
        <input type="checkbox" name="hobbies" value="代码">代码
        <input type="checkbox" name="hobbies" value="唱歌">唱歌
        <input type="checkbox" name="hobbies" value="电影">电影
        <br>
        <input type="submit">
    </form>
</div>

</body>
</html>
```

success.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>

<h1>登录成功</h1>

</body>
</html>
```

注意：这里请求转发不用加/r路径，而前面重定向需要

## Cookie、Session

### 会话

**会话：**用户打开一个浏览器，点击很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话

**有状态会话：**一个同学来过教室，下次再来教室，我们会知道这个同学，曾经来过，称之为有状态会话；

**一个网站，如何证明来过**

客户端      服务端

1. 服务端给客户一个信件，客户端下次访问服务端时带上信件即可；cookie
2. 服务器登记你来过了，下次来的时候匹配；session

### 保存会话的两种技术

**cookie**

- 客户端技术（响应发给客户端，请求带上信件）

**session**

- 服务器技术，利用这个技术，可以保存用户的会话信息？我们可以把信息或者数据放在Session中！

常见场景:网站登录后，下次不用登录就能进入

### Cookie

![](https://img-blog.csdnimg.cn/8f432aef53164467bef31ea00f9edc34.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

1. 从请求中拿到cookie信息
2. 服务器响应给客户端cookie

```java
Cookie[] cookies = req.getCookies(); //获得cookie
cookie.getName();//获得cookie中的键
cookie.getValue();//获得cookie中的值
Cookie cookie = new Cookie("lastLoginTime", System.currentTimeMillis()+"");//新建cookie
cookie.setMaxAge(24*60*60);//设置cookie的有效期
resp.addCookie(cookie);//响应给客户端一个cookie
```

cookie 一般会保存在本地的 用户目录下 appdata；

```java
package com.Sucker.servlet;

public class CookieDemo01 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //服务器，告诉你，你来的时间，把这个时间封装成一个 信件，下次带来就知道是你来了

        //解决中文乱码
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        PrintWriter out = resp.getWriter();

        //Cookie,服务器端从客户端获取
        Cookie[] cookies = req.getCookies();// 这里返回数组，说明cookie可能存在多个

        //判断Cookie是否为控
        if(cookies!=null){
            //如果存在
            out.write("你上一次访问的时间是");

            for (int i = 0; i < cookies.length; i++) {
                Cookie cookie = cookies[i];
                //获取cookie的名字
                if(cookie.getName().equals("lastLoginTime")){
                    //获取cookie中的值
                    long lastLoginTime = Long.parseLong(cookie.getValue());//用包装类转换
                    Date date = new Date(lastLoginTime);
                    out.write(date.toLocaleString());

                }

            }

        }else{
            out.write("这是您第一次访问本站");
        }

        //服务端给客户端响应一个cookie
        Cookie cookie = new Cookie("lastLoginTime", System.currentTimeMillis()+"");

        //cookie的有效期为1天
        cookie.setMaxAge(24*60*60);

        resp.addCookie(cookie);


    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

一点细节问题：

- 一个Cookie只能保存一个信息；
- 一个web站点可以给服务器发送多个cookie，每个站点最多存放20个cookie
- Cookie大小有限制4kb
- 300个cookie浏览器上限

删除Cookie：

- 不设置有效期，关闭浏览器，自动失效；
- 设置有效期为0

中文编码解码：

```java
URLEncoder.encode("青三","utf-8")
URLDecoder.decode(cookie.getValue(),"utf-8");
```

```java
package com.Sucker.servlet;
// 中文数据传递
public class CookieDemo02 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //解决中文乱码
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        PrintWriter out = resp.getWriter();
        Cookie[] cookies = req.getCookies();

        //判断Cookie是否为l
        if(cookies!=null){
            //如果存在
            out.write("你上一次访问的时间是");

            for (int i = 0; i < cookies.length; i++) {
                Cookie cookie = cookies[i];
                //获取cookie的名字
                if(cookie.getName().equals("name")){
                    System.out.println(cookie.getValue());
                    //解码
                    out.write(URLDecoder.decode(cookie.getValue(),"utf-8"));
                }

            }

        }else{
            out.write("这是您第一次访问本站");
        }
        //设置中文编码，这里不设置也能成功，但是设置更好
        Cookie cookie = new Cookie("name", URLEncoder.encode("青三","utf-8"));
        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

### Session（重点）

![](https://img-blog.csdnimg.cn/a391ef6bb594486ca0fdaf5e00bf43a4.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

Session：

- 服务器会给每一个用户(浏览器)创建一个Session对象；
- 一个Session独占一个浏览器，只要浏览器没有关闭，这个Session就存在；
- 用户登录后，整个网站都能访问 --> 保存用户信息，保存购物车的信息...

![](https://img-blog.csdnimg.cn/96670fc9bddc4fe99075d9e8cb09429d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

Session 和 cookie 的区别：

- Cookie是把用户的数据写给浏览器，浏览器保存
- Session把用户的数据写到用户独占的Session中，服务器端保存（保存重要的信息，减少服务器资源的浪费）
- Session对象由服务器创建

使用场景：

- 保存一个登录用户的信息；
- 购物车信息；
- 在整个网站中，经常会使用的数据，保存在Session中

使用Session：

1. ```java
   package com.Sucker.servlet;
   
   public class SessionDemo01 extends HttpServlet {
   
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
   
           //解决乱码问题
           req.setCharacterEncoding("utf-8");
           resp.setCharacterEncoding("utf-8");
           resp.setContentType("text/html");
   
           //得到Session
           HttpSession session = req.getSession();
   
           //给Session中存东西
           session.setAttribute("name",new Person("青三",1));
   
           //获取Session的ID
           String sessionID = session.getId();
   
           //判断Session是不是新创建的
           if(session.isNew()){
               resp.getWriter().write("session创建成功,ID:"+sessionID);
           }else{
               resp.getWriter().write("session已经在服务器中存在，ID："+sessionID);
           }
   
           //Session在创建的时候做了：
   //        Cookie cookie = new Cookie("JSESSIONID",sessionID);
   //        resp.addCookie(cookie);
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           doGet(req, resp);
       }
   }
   ```

2. 得到Session

   ```java
   package com.Sucker.servlet;
   
   public class SessionDemo02 extends HttpServlet {
   
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
   
           //解决乱码问题
           req.setCharacterEncoding("utf-8");
           resp.setCharacterEncoding("utf-8");
           resp.setContentType("text/html");
   
           //得到Session
           HttpSession session = req.getSession();
   
           Person person = (Person) session.getAttribute("name");
           System.out.println(person.toString());
   
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           doGet(req, resp);
       }
   }
   ```

3. 注销

   ```java
   package com.Sucker.servlet;
   
   public class SessionDemo03 extends HttpServlet {
   
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
   
           HttpSession session = req.getSession();
           session.removeAttribute("name");//移除
           session.invalidate();//手动注销session
   
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           doGet(req, resp);
       }
   }
   ```

4. 会话自动过期：web.xml中配置

   ```xml
   <!--设置Session默认的失效时间-->
   <session-config>
       <!--xx分钟后Session自动失效，分钟为单位-->
       <session-timeout>1</session-timeout>
   </session-config>
   ```

## JSP

### JSP概述

Java Server Pages : Java服务器端页面，也和Servlet一样，用于开发动态Web技术

最大的特点：

- 写JSP就像在写HTML
- 区别：
  - HTML只给用户提供静态的数据
  - JSP页面中可以嵌入JAVA代码，为用户提供动态数据

### JSP原理

思路：JSP如何执行

**浏览器向服务器发送请求，不管访问什么资源，其实都是在访问Servlet！**

jsp最终也会转换称为一个java类

```
C:\Users\扶苏\AppData\Local\JetBrains\IntelliJIdea2021.1\tomcat\ca539b0c-3d3f-4bf2-bd95-27c751ac36de\work\Catalina\localhost\ROOT\org\apache\jsp
```

**JSP本质上就是一个Servlet**

```java
//初始化
public void _jspInit(){
    
}
//销毁
public void _jspDestory(){
    
}
//JSPService
public void _jspService(.HttpServletRequest request,HttpServletResponse response)
```

1. 判断请求

2. 内置一些对象

   ```java
   final javax.servlet.jsp.PageContext pageContext; //页面上下文
   javax.servlet.http.HttpSession session = null; //session
   final javax.servlet.ServletContext application; //applicationContext
   final javax.servlet.ServletConfig config; //config 配置
   javax.servlet.jsp.JspWriter out = null; //out 输出
   final java.lang.Object page = this; // page：当前页面
   HttpServletRequest request  //请求
   HttpServletResponse response //响应
   ```

3. 输出页面前增加的代码

```java
response.setContentType("text/html");  //设置响应的页面类型
pageContext = _jspxFactory.getPageContext(this, request, response,
                                          null, true, 8192, true);
_jspx_page_context = pageContext;
application = pageContext.getServletContext();
config = pageContext.getServletConfig();
session = pageContext.getSession();
out = pageContext.getOut();
_jspx_out = out;
```

4. 以上这些对象可以直接在JSP页面中使用！

![](https://img-blog.csdnimg.cn/60cfcf94d4214527a90acd2b23e5bcfb.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

在JSP中：

只要是JAVA代码就直接不变输出

如果是HTML代码，就会被转换为

```java
out.write("<html>\r\n");
```

这样的格式输出到前端

### JSP基础语法

JSP作为Java技术的一种，它拥有一些自己扩充的语法(了解，知道即可！)，java所有语法都支持

#### jsp表达式

```jsp
  <%--JSP表达式
  作用：用来将程序输出，输出到客户端
  <%= 变量或者表达式%>
  --%>
  <%= new java.util.Date()%>
```

#### jsp脚本片段

```jsp
  <%--jsp脚本片段--%>
  <%
    int sum=0;
    for (int i = 0; i < 100; i++) {
      sum+=i;
    }
    out.println("<h1>Sum:"+sum+"</h1>");
  %>
```

#### 脚本代码的再实现

```jsp
  <%
    int x = 10;
    out.println(x);
  %>
  <p>这是一个jsp文档</p>
  <%
    int y = 10;
    out.println(y);
  %>

  <hr>

  <%--在代码中嵌入HTML元素--%>
  <%
    for (int i = 0; i < 5; i++) {
  %>
    <h1>Hello,World  <%=i%> </h1>
  <%
    }
  %>
```

#### JSP声明

```jsp
  <!--在感叹号里面可以写外部代码-->
  <%!
    static {
      System.out.println("Loading Servlet!");
    }

    private int globalVar = 0;

    public void Sucker(){
      System.out.println("进入了方法Scuker");
    }
  %>
```

JSP声明：会被编译到JSP生成的Java的类中！其他的就会被生成到_jspService方法中！

在JSP中嵌入Java代码即可！

```jsp
<%%>
<%=%>
<%！%>

<%--注释--%>
```

JSP的注释，不会在客户端显示源代码里显示，而HTML会

### JSP指令

```jsp
<%--定制错误界面--%>

<%@ page errorPage="error/500.jsp" %>
<%--显示的声明这是一个错误页面--%>
<%@ page isErrorPage="true" %>
<%@page pageEncoding="UTF-8" %>
```

也可以在xml中配置

```xml
    <error-page>
        <error-code>404</error-code>
        <location>/error/404.jsp</location>
    </error-page>
    <error-page>
        <error-code>500</error-code>
        <location>/error/500.jsp</location>
    </error-page>
```

```jsp
<%--这是500.jsp--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%--..代表上级目录--%>
<img src="img/1.png" alt="500">

</body>
</html>

```

```jsp
<%@include file=""%>

<%--<%@ include会将两个页面合二为一--%>
<%@ include file="common/header.jsp"%>
<h1>网页主体</h1>
<%@ include file="common/footer.jsp"%>

<hr>

<%--jsp标签
    jsp:include 拼接页面，本质还是三个
        --%>
<jsp:include page="/common/header.jsp"/>
<h1>网页主体</h1>
<jsp:include page="/common/footer.jsp"/>
```

```jsp
<%--Header.jsp和Footer.jsp--%>

<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<h1>我是Header</h1>

<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<h1>我是Footer</h1>
```

![](https://img-blog.csdnimg.cn/9ea1e3df18a44daeb7d5d03135906af6.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### 9大内置对象

- PageContext   存东西
- Request   存东西
- Response
- Session  存东西
- Application  【ServletContext】 存东西
- config  【ServletConfig】
- out
- page
- exception

request：客户端向服务器发送请求，产生的数据，用户看完就没用了，比如：新闻

session：客户端向服务器发送请求，产生的数据，用户用完过一段时间还有用，比如：购物车；

application：客户端向服务器发送请求，产生的数据，一个用户用完了，其他用户还可能使用，比如：聊天数据；



这是PageContextDemo01

```jsp
<%--内置对象--%>

<%
    pageContext.setAttribute("name1","苏1"); //保存的数据只在一个页面中有效
    request.setAttribute("name2","苏2"); // 保存的数据只在一次请求中有效，请求转发会携带这个数据
    session.setAttribute("name3","苏3"); // 保存的数据只在一次会话中有效，从打开浏览器到关闭浏览器
    application.setAttribute("name4","苏4"); // 保存的数据在服务器中有效，从打开服务器到关闭服务器
%>

<%--脚本片段中的代码，会被原封不动的生成到.JSP.java中
要求：这里面的代码：必须保证Java语法的正确性
--%>
<%
    //通过pageContext取出我们保存的值，通过寻找方式来
    //从底层到高层（作用域）：page-->request-->session-->application
    String name1 = (String) pageContext.findAttribute("name1");
    String name2 = (String) pageContext.findAttribute("name2");
    String name3 = (String) pageContext.findAttribute("name3");
    String name4 = (String) pageContext.findAttribute("name4");
    String name5 = (String) pageContext.findAttribute("name5"); // 不存在
%>

<%--使用EL表达式输出  ${}  --%>
<h1>取出的值为：</h1>
<h3>${name1}</h3>
<h3>${name2}</h3>
<h3>${name3}</h3>
<h3>${name4}</h3>
<h3>${name5}</h3> <%--用这种方式页面不会显示不存在的--%>
<h3> <%=name5%> </h3>  <%--用这种方式会有null--%>
```

从PageDemo02访问01的资源，结果只有苏3和苏4，因为作用域问题

```jsp
<%--脚本片段中的代码，会被原封不动的生成到.JSP.java中
要求：这里面的代码：必须保证Java语法的正确性
--%>
<%
    //通过pageContext取出我们保存的值，通过寻找方式来
    //从底层到高层（作用域）：page-->request-->session-->application
    //JVM: 双亲委派机制 :
    String name1 = (String) pageContext.findAttribute("name1");
    String name2 = (String) pageContext.findAttribute("name2");
    String name3 = (String) pageContext.findAttribute("name3");
    String name4 = (String) pageContext.findAttribute("name4");
    String name5 = (String) pageContext.findAttribute("name5"); // 不存在
%>

<%--使用EL表达式输出  ${}  --%>
<h1>取出的值为：</h1>
<h3>${name1}</h3>
<h3>${name2}</h3>
<h3>${name3}</h3>
<h3>${name4}</h3>
<h3>${name5}</h3> <%--用这种方式页面不会显示不存在的--%>
<h3> <%=name5%> </h3>  <%--用这种方式会有null--%>
```

设置作用域

```jsp
<%--
    public static final int PAGE_SCOPE		= 1;
    public static final int REQUEST_SCOPE	= 2;
    public static final int SESSION_SCOPE	= 3;
    public static final int APPLICATION_SCOPE	= 4;

    //scope :作用域
    public void setAttribute(String name, Object attribute, int scope) {
        switch(scope) {
        case 1:
            this.mPage.put(name, attribute);
            break;
        case 2:
            this.mRequest.put(name, attribute);
            break;
        case 3:
            this.mSession.put(name, attribute);
            break;
        case 4:
            this.mApp.put(name, attribute);
            break;
        default:
            throw new IllegalArgumentException("Bad scope " + scope);
        }

    }
--%>

<%
    pageContext.setAttribute("hello","hello1",PageContext.SESSION_SCOPE);
    //等价于:session.setAttribute("hello","hello1")
%>
```

转发

```jsp
<%
    pageContext.forward("/index.jsp");
    //request.getRequestDispatcher("/index.jsp").forward(request,response);
%>
```

### JSP标签、JSTL标签、EL表达式

```xml
<!--JSTL表达式的依赖-->
<dependency>
    <groupId>javax.servlet.jsp.jstl</groupId>
    <artifactId>jstl-api</artifactId>
    <version>1.2</version>
</dependency>

<!--Standard标签库-->
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```

EL表达式：${ }

- **获取数据**
- **执行运算**
- **获取web开发的常用对象**

**JSP标签**

从第一个页面跳转到第二个页面并携带参数，在第二个页面获取并打印

```jsp
<%--jsp:include--%>

<%--
http://localhost:8080/jsp/jsptag.jsp?name=Sucker&age=18
--%>

<jsp:forward page="/jsptag2.jsp">
    <jsp:param name="name" value="Sucker"/>
    <jsp:param name="age" value="18"/>
</jsp:forward>
```

```jsp
<h1>2</h1>

<%--取出参数--%>

名字:<%=request.getParameter("name")%>
年龄:<%=request.getParameter("age")%>
```

**JSTL表达式**

JSTL标签库的使用就是为了弥补HTML标签的不足；它自定义了许多标签，可以供我们使用，标签的功能和Java代码一样

**格式化标签**

**SQL标签**

**XML标签**

**核心标签（掌握部分）**

引入JSTL核心标签库才能使用JSTL

```jsp
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

![](https://img-blog.csdnimg.cn/05b0de1a393b4091b1555356aa52a23b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

**JSTL标签库使用步骤**

- 引入对应的taglib
- 使用其中的方法
- 在Tomcat中也需要引入jstl的包（还有配合使用的standard包），否则会报错：JSTL解析错误

c:if

注意：要用EL表达式从表单中取值要这样：value="${param.username}

```jsp

<h1>if测试</h1>

<hr>

<%--表单里写的数据提交到本来这个页面再通过本来这个页面获取它--%>
<form action="coreif.jsp" method="get">
    <%--
    EL表达式获取表单中的数据
    ${param.参数名}
    --%>
    <input type="text" name="username" value="${param.username}" >
    <input type="submit" value="登录">
</form>

<%--判断如果提交的用户名是管理员,则登录成功--%>

<%--<%--%>
<%--    if(request.getParameter("username").equals("admin")) out.write("登录成功");--%>
<%--%>--%>
<c:if test="${param.username=='admin'}" var="isAdmin">
    <c:out value="管理员欢迎你!"></c:out>
</c:if>

<c:out value="${isAdmin}"></c:out> <%--这里会判断上面的定义的变量是否是is
    Adimin（var表示定义一个变量）则返回true，否则是false，会在前端页面出现值--%>
```

c:set  c:choose   c:when

```jsp
<%--定义一个变量score.值为85--%>
<c:set var="score" value="85"/>

<c:choose>
  <c:when test="${score>=90}">
    你的成绩为优秀
  </c:when>
  <c:when test="${score>=80}">
    你的成绩为良好
  </c:when>
  <c:when test="${score>=70}">
    你的成绩为一般
  </c:when>
  <c:when test="${score<=60}">
    你的成绩为不及格
  </c:when>
</c:choose>
```

c:forEach   c:out

```jsp
<%
    ArrayList<String> people = new ArrayList<>();
    people.add(0,"张三");
    people.add(1,"赵六");
    people.add(2,"王五");
    people.add(3,"李四");
    request.setAttribute("list",people);

%>

<%--
var  每次遍历出来的变量
items  要遍历的对象
begin  哪里开始
end  到哪里闭区间
step  步长
--%>
<c:forEach var="people" items="${list}">
    <c:out value="${people}"/> <br>
</c:forEach>

<hr>

<c:forEach var="people" items="${list}" begin="1" end="3" step="2">
    <c:out value="${people}"/> <br>
</c:forEach>
```

## JavaBean

JavaBean 是特殊的 Java 类，使用 Java 语言书写，并且遵守 JavaBean API 规范。

实体类

JavaBean有特定的写法：

- 必须要有一个无参构造
- 属性必须私有化
- 必须有对应的get/set方法

一般用来和数据库的字段做映射  ORM

ORM：对象关系映射

- 表-->类
- 字段-->属性
- 行记录-->对象

people表

| id   | name | age  | address |
| ---- | ---- | ---- | ------- |
| 2    | S2   | 3    | a       |
| 1    | S1   | 18   | b       |
| 3    | S3   | 100  | c       |

```java
class People{
    private int id;
    private String name;
    private int id;
    private String address;
}

class A{
    new People(1,"S1",3,"a");
}

```

```jsp

<%
//    People people = new People();
//    people.setAddress();
//    people.setId();
//    people.setName();
//    people.setAge();
%>

<jsp:useBean id="people" class="com.Sucker.pojo.People" scope="page"/>

<jsp:setProperty name="people" property="address" value="aa"/>
<jsp:setProperty name="people" property="age" value="3"/>
<jsp:setProperty name="people" property="name" value="S1"/>
<jsp:setProperty name="people" property="id" value="1"/>

姓名:<jsp:getProperty name="people" property="name"/>z
ID:<jsp:getProperty name="people" property="id"/>z
年龄:<jsp:getProperty name="people" property="age"/>z
地址:<jsp:getProperty name="people" property="address"/>z

```

## MVC三层架构

MVC：Model    view    Controller    模型、视图、控制器

### 往年架构

![](https://img-blog.csdnimg.cn/440e51f15f2445b498b895d1f78fbb9c.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

用户直接访问控制层，控制层就可以直接操作数据库

```java
servlet-->CRUD-->数据库
弊端：程序十分臃肿，不利于维护   
servlet的代码中：处理请求、响应、视图跳转、处理JDBC、处理业务代码、处理逻辑代码
    
架构：没有什么是加一层解决不了的
|
JDBC
|
Mysql  Oracle  SqlServer...
```

### MVC三层架构

![](https://img-blog.csdnimg.cn/b966c0efc5334c0fabc0ab3ecd00326f.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

Model

- 业务处理：业务逻辑（Service）
- 数据持久层：CRUD（Dao）

View

- 展示数据
- 提供链接发起Servlet请求（a，form，img...）

Controller（Servlet）

- 接收用户请求：（req：请求参数、Session信息,,,）

- 交给业务层处理对应的代码

- 控制视图的跳转

  ```
  登录-->接收用户的请求-->处理用户的请求(获取用户登录的参数)-->交给业务层处理登录业务（判断用户名密码是否正确：事务）-->Dao层查询用户名和密码是否正确-->数据库
  ```

## Filter（重点）

Filter：过滤器，用来过滤网站的数据；

- 处理中文乱码
- 登录验证

![](https://img-blog.csdnimg.cn/d63561d2cb1f45a08a0f80e00ac9e8bf.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

Filter开发步骤：

1. 导包（servlet、jsp、jstl、standard）

2. 编写过滤器

   - 导包不能错

     ```java
     import javax.servlet.Filter;
     ```

     ```java
     package com.Sucker.filter;
     
     import javax.servlet.*;
     import java.io.IOException;
     
     public class CharacterEncodingFilter implements Filter {
     
         //初始化 :web服务器启动,就已经初始化了,随时等待过滤对象出现
         public void init(FilterConfig filterConfig) throws ServletException {
             System.out.println("CharacterEncodingFilter已经初始化");
         }
     
         //chain: 链
         /*
         1.过滤器中的所有代码,在过滤特定请求的时候都会执行
         2.必须让过滤器继续通行  chain.doFilter(request,response);
          */
         public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
             request.setCharacterEncoding("utf-8");
             response.setCharacterEncoding("utf-8");
             response.setContentType("text/html;charset=UTF-8");
     
             System.out.println("CharacterEncodingFilter执行前...");
             chain.doFilter(request,response);//让我们的请求继续走,如果不写,程序到这里就被拦截停止!
             System.out.println("CharacterEncodingFilter执行前...");
         }
     
         //销毁:web服务器关闭时 ,过滤会销毁
         public void destroy() {
             System.out.println("CharacterEncodingFilter已经销毁");
         }
     }
     
     ```

     测试乱码的类

     ```java
     package com.Sucker.servlet;
     public class ShowServlet extends HttpServlet {
     
         @Override
         protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
             resp.getWriter().write("你好");//一定乱码
         }
     
         @Override
         protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
             doGet(req, resp);
         }
     }
     
     ```

     配置xml

     ```xml
         <servlet>
             <servlet-name>ShowServlet</servlet-name>
             <servlet-class>com.Sucker.servlet.ShowServlet</servlet-class>
         </servlet>
         <servlet-mapping>
             <servlet-name>ShowServlet</servlet-name>
             <url-pattern>/servlet/show</url-pattern>
         </servlet-mapping>
         <servlet-mapping>
             <servlet-name>ShowServlet</servlet-name>
             <url-pattern>/show</url-pattern>
         </servlet-mapping>
     
         <filter>
             <filter-name>CharacterEncodingFilter</filter-name>
             <filter-class>com.Sucker.filter.CharacterEncodingFilter</filter-class>
         </filter>
         <filter-mapping>
             <filter-name>CharacterEncodingFilter</filter-name>
             <!--只要是/servlet下的任何请求都会j经过这个过滤器-->
             <url-pattern>/servlet/*</url-pattern>
         </filter-mapping>
     ```

## 监听器

实现一个监听器的接口；（有N种）

1. 编写一个监听器

   实现监听器的接口

   ```java
   package com.Sucker.listener;
   
   import javax.servlet.ServletContext;
   import javax.servlet.http.HttpSessionEvent;
   import javax.servlet.http.HttpSessionListener;
   
   //统计网站在线人数 : 统计session
   public class OnlineCountListener implements HttpSessionListener {
   
       //创建session监听 :
       //一旦创建一个session, 就会触发一次这个事件
       public void sessionCreated(HttpSessionEvent se) {
           ServletContext ctx = se.getSession().getServletContext();
           Integer onlineCount = (Integer) ctx.getAttribute("OnlineCount");
   
           if(onlineCount==null){
               onlineCount = new Integer(1); // 加一个在线人数
           }else{
               int count = onlineCount.intValue();
               onlineCount = new Integer(count+1);
           }
   
           ctx.setAttribute("OnlineCount",onlineCount);
   
       }
   
       //一旦销毁一个session, 就会触发一次这个事件
       public void sessionDestroyed(HttpSessionEvent se) {
   
           ServletContext ctx = se.getSession().getServletContext(); // 存到这个上下文中
   
           System.out.println(se.getSession().getId());
   
           Integer onlineCount = (Integer) ctx.getAttribute("OnlineCount");
   
           if(onlineCount==null){
               onlineCount = new Integer(0); // 加一个在线人数
           }else{
               int count = onlineCount.intValue();
               onlineCount = new Integer(count-1);
           }
   
           ctx.setAttribute("OnlineCount",onlineCount);
       }
   
       /*
       Session销毁:
       1.手动销毁  getSession.invalidate();
       2.自动销毁  web.xml中配置自动过期时间
        */
   
   
   }
   
   ```

2. web.xml中配置监听器

   ```xml
       <!--注册监听器-->
       <listener>
           <listener-class>com.Sucker.listener.OnlineCountListener</listener-class>
       </listener>
   
       <session-config>
   <!--        1分钟销毁session-->
           <session-timeout>1</session-timeout>
       </session-config>
   ```

3. 在前端显示：

   ```jsp
   <h1>当前有 <span style="color: blue"><%=this.getServletConfig().getServletContext().getAttribute("OnlineCount")%></span></h1>
   ```

4. 看情况使用

## 过滤器、监听器常见应用

**监听器：GUI编程中经常使用**

窗体小案例

```java
package com.Sucker.listener;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.awt.event.WindowListener;

public class TestPanel {
    public static void main(String[] args) {
        Frame frame = new Frame("中秋节快乐");//新建一个窗口,参数是窗口标题
        Panel panel = new Panel(null);//面板
        frame.setLayout(null);//设置窗体的布局

        frame.setBounds(300,300,500,500);//设置宽高
        frame.setBackground(new Color(0,0,255));//背景颜色

        panel.setBounds(50,50,300,300);
        panel.setBackground(new Color(0,255,0));

        frame.add(panel);
        frame.setVisible(true);

        //监听事件,监听关闭事件
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
            }
        });


    }

}
```

案例：用户登录之后才能进入主页，用户注销后就不能进入主页

1. 用户登录后，向Session中放入用户的数据

2. 进入主页的时候要判断用户是否已经登录（要求：过滤器中实现）（防止用户跳过登录直接进入主页）

   ```java
   package com.Sucker.listener;
   
   public class SysFilter implements Filter {
       public void init(FilterConfig filterConfig) throws ServletException {
   
       }
   
       public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws IOException, ServletException {
           //ServletRequest  HttpServletRequest  父子关系,前面这个拿不到Session所以强转
           HttpServletRequest request = (HttpServletRequest) req;
           HttpServletResponse response = (HttpServletResponse) resp;
   
           if(request.getSession().getAttribute("USER_SESSION")==null){
               response.sendRedirect("/error.jsp");
           }
   
   
           chain.doFilter(request,response);
       }
   
       public void destroy() {
   
       }
   }
   ```

   xml配置：任何访问sys目录下的请求都会被过滤

   ```xml
       <filter>
           <filter-name>SysFilter</filter-name>
           <filter-class>com.Sucker.listener.SysFilter</filter-class>
       </filter>
       <filter-mapping>
           <filter-name>SysFilter</filter-name>
           <url-pattern>/sys/*</url-pattern>
       </filter-mapping>
   ```

3. 用户登录

   ```java
   package com.Sucker.servlet;
   
   public class LoginServlet extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
   
           //获取前端请求的参数
           String username = req.getParameter("username");
           if(username.equals("admin")){ //登录成功
               System.out.println("success");
               req.getSession().setAttribute("USER_SESSION",req.getSession().getId());
               resp.sendRedirect("/sys/success.jsp");//重定向
           }else{ // 登录失败
               resp.sendRedirect("/error.jsp");//重定向
           }
   
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           doGet(req, resp);
       }
   }
   
   ```

   登录前端页面

   ```jsp
   <h1>登录</h1>
   
   <form action="/servlet/login" method="post"> //表单提交到/servlet/login这个请求，去xml中寻找
       <input type="text" name="username" >
       <input type="submit">
   </form>
   ```

   配置xml

   ```xml、
       <servlet>
           <servlet-name>LoginServlet</servlet-name>
           <servlet-class>com.Sucker.servlet.LoginServlet</servlet-class>
       </servlet>
       <servlet-mapping>
           <servlet-name>LoginServlet</servlet-name>
           <url-pattern>/servlet/login</url-pattern>
       </servlet-mapping>
   ```

4. 登录成功进入主页

   ```jsp
   <h1>主页</h1>
   
   <p><a href="/servlet/logout">注销</a></p> //点击注销按钮转到/servlet/logout，在xml中查找对应java
   ```

   配置xml

   ```xml
       <servlet>
           <servlet-name>LogoutServlet</servlet-name>
           <servlet-class>com.Sucker.servlet.LogoutServlet</servlet-class>
       </servlet>
       <servlet-mapping>
           <servlet-name>LogoutServlet</servlet-name>
           <url-pattern>/servlet/logout</url-pattern>
       </servlet-mapping>
   ```

5. 点击注销进入登录页面：判断session是否为空，不为空则要移除（因为点击了注销），然后跳转到登录页面

   ```java
   package com.Sucker.servlet;
   
   public class LogoutServlet extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           Object user_session = req.getSession().getAttribute("USER_SESSION");
   
           if (user_session!=null){
               req.getSession().removeAttribute("USER_SESSION");
               if(req.getSession().getAttribute("USER_SESSION")!=null) System.out.println("US!=null");
               else System.out.println("US=null");
               resp.sendRedirect("/Login.jsp");
           }else{
               System.out.println("user_ession=null");
               resp.sendRedirect("/Login.jsp");//当user_session=null时点注销也要回主页
           }
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           doGet(req, resp);
       }
   }
   
   ```

6. 登录失败进入error界面

   ```jsp
   <h1>错误</h1>
   <h3>没有权限,用户名错误</h3>
   
   <a href="/Login.jsp">返回登录页面</a> //点击返回登录界面
   ```

## JDBC

JDBC：java连接数据库

![](https://img-blog.csdnimg.cn/9a977bca339d40419eb2bbbe0c04456a.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

需要jar包的支持：

- java.sql
- javax.sql
- mysql-connector-java...连接驱动（必须要）

环境搭建：

```sql

CREATE TABLE users(
 id INT PRIMARY KEY, 
 `name` VARCHAR(40), 
 `password` VARCHAR(40),
 email VARCHAR(60), 
 birthday DATE
); 

INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(1,'张三','123456','af@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(2,'李四','123456','ls@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(3,'王五','123456','ww@qq.com','2000-01-01');

SELECT * FROM users;
```

导入数据库依赖jar包

```xml
<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>
</dependencies>
```

IDEA连接数据库

![](https://img-blog.csdnimg.cn/fd82e0617b3a456284671b471b365db5.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

**JDBC固定步骤**

1. 加载驱动
2. 连接数据库
3. 向数据库发送SQL的对象Statement : CRUD
4. 编写SQL（根据业务，不同的SQL）
5. 执行SQL
6. 关闭连接

```java
package com.Sucker.test;

import java.sql.*;

public class TsetJdbc {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //配置信息
        //解决中文乱码：useUnicode=true&characterEncoding=utf8
        String url = "jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf8&useSSL=true";
        String username = "root";
        String password = "123456";

        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
        Connection connection = DriverManager.getConnection(url, username, password);

        //3.向数据库发送SQL的对象Statement : CRUD（这里可以用connection.prepareStatement()）
        Statement statement = connection.createStatement();

        //4.编写SQL
        String sql = "select * from users";
        
        //受影响的行数，增删改都是用executeUpdate即可
        //int i = statement.executeUpdate(sql);

        //5.执行查询SQL,返回一个结果集resultSet
        ResultSet rs = statement.executeQuery(sql);

        while (rs.next()){
            System.out.println("id="+ rs.getObject("id"));
            System.out.println("name="+ rs.getObject("name"));
            System.out.println("password="+ rs.getObject("password"));
            System.out.println("email="+ rs.getObject("email"));
            System.out.println("birthday="+ rs.getObject("birthday"));
        }

        //6. 关闭连接，释放资源（一定要做）
        rs.close();
        statement.close();
        connection.close();

    }
}
```

使用PreparedStatement预编译SQL

```java
public class TestJDBC2 {
    public static void main(String[] args) throws Exception {
        //配置信息
        //解决中文乱码：useUnicode=true&characterEncoding=utf8
        String url = "jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf8&useSSL=true";
        String username = "root";
        String password = "123456";

        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
        Connection connection = DriverManager.getConnection(url, username, password);

        //3.编写SQL
        String sql = "insert into users(id, name, password, email, birthday) values(?,?,?,?,?)";

        //4.预编译
        PreparedStatement preparedStatement = connection.prepareStatement(sql);

        preparedStatement.setInt(1,4);//给第一个占位符？ 赋值为1
        preparedStatement.setString(2,"Sucker");//给第2个占位符？ 赋值为1
        preparedStatement.setString(3,"123456");//给第3个占位符？ 赋值为1
        preparedStatement.setString(4,"24257289@qq.com");//给第4个占位符？ 赋值为1
        preparedStatement.setDate(5,new Date(new java.util.Date().getTime()));//给第5个占位符？ 赋值为1
        //第一个new Date是java.sql包下的

        //5.执行SQL
        int i = preparedStatement.executeUpdate();

        if(i>0) System.out.println("插入成功");

        //6. 关闭连接，释放资源（一定要做）
        preparedStatement.close();
        connection.close();


    }
}
```

**事务**

要么都成功，要么都失败！

ACID原则：保证数据的安全！

```java
开启事务
事务提交   commit()
事务回滚   rollback()
关闭事务
    
转账：
A：1000
B：1000

A(900)   --100-->  B(1100)
```

**Junit单元测试**

依赖jar包

```xml
<!--单元测试-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13</version>
</dependency>
```

简单使用

@Test注解只有在方法上有效，只要加了这个注解的方法就可以直接运行

```java
public class TestJDBC3 {
    @Test
    public void test(){
        System.out.println("hello");
    }
}
```

失败时红色报错

测试JDBC事务

**搭建环境**

建表

```sql
CREATE TABLE account(
    id INT PRIMARY KEY AUTO_INCREMENT,
    `name` VARCHAR(40),
    money FLOAT
);

INSERT INTO account(`name`,money) VALUES('A','1000');
INSERT INTO account(`name`,money) VALUES('B','1000');
INSERT INTO account(`name`,money) VALUES('C','1000');
```

```java
package com.Sucker.test;

public class TestJDBC3 {

    @Test
    public void test() {

//配置信息
        //解决中文乱码：useUnicode=true&characterEncoding=utf8
        String url = "jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf8&useSSL=true";
        String username = "root";
        String password = "123456";

        Connection connection = null;

        //1.加载驱动
        try {
            Class.forName("com.mysql.jdbc.Driver");
            //2.连接数据库,代表数据库
            connection = DriverManager.getConnection(url, username, password);

            //3.数据库开启事务,false是开启
            connection.setAutoCommit(false);

            String sql1 = "update account set money = money-100 where name = 'A';";
            connection.prepareStatement(sql1).executeUpdate();

            //制造错误
            //int i = 1/0;

            String sql2 = "update account set money = money+100 where name = 'B';";
            connection.prepareStatement(sql2).executeUpdate();

            connection.commit();//以上两条SQL都执行成功了，就提交事务！
            System.out.println("成功");
        } catch (Exception e) {
            try {
                //如果出现异常就通知数据库回滚事务
                connection.rollback();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
            e.printStackTrace();
        }finally {
            try {
                connection.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }

    }

}

```

## 文件传输

### 环境搭建

直接新建空项目

![](https://img-blog.csdnimg.cn/20200708012637521.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTE0ODk5Nw==,size_16,color_FFFFFF,t_70#pic_center)

配置Tomcat

**导入jar包**

![](https://img-blog.csdnimg.cn/be0e9275e5af4d95825fcc7327c33cc3.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

注意项目结构里面

![](https://img-blog.csdnimg.cn/82ee4a494b094a8b905d7b93b31b3f56.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### 使用类介绍

#### 文件上传注意事项

![](https://img-blog.csdnimg.cn/ca2e06494c34443fb87a19d2aa460aef.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

#### FileItem类

在HTML页面input必须又name<input type="file" name="filename">

**表单如果包含一个文件上传输入项，这个表单的enctype属性就必须设置为multipart/form-data**

通过上传用户名来用于解决上方四条注意事项

浏览器表单类型如果为 multipart/form-data ，在服务器端想要获取数据就需要通过流

```jsp
  <%--通过表单上传文件
     get: 上传文件大小有限制
     post:上传文件大小没有限制
  --%>
  <form action="${pageContext.request.contextPath}/upload.do" enctype="multipart/form-data" method="post">
    上传用户：<input type="text" name="username"><br/><%--通过上传用户名来用于解决上方四条注意事项--%>
    <p><input type="file" name="file1"></p> <%--选择文件--%>
    <p><input type="file" name="file2"></p> <%--选择文件--%>

    <p><input type="submit"></p> <%--提交按钮--%>
  </form>
```

【常用方法介绍】

```java
//isFormField方法用于判断FileItem类对象封装的数据是一个普通文本表单
//还是一个文件表单，如果是普通表单字段则返回true，否则返回false
boolean isFormField();//即：只要是上传的文件，返回的就是false

//getFieldName方法用于返回表单标签name属性的值。
String getFieldName();//获取这个input的name属性值

//getString方法用于将FileItem对象中保存的数据流内容以一个字符串返回
String getString();//用字符串存储文件的数据流
    
//getName方法用于获得文件上传字段中的文件名
String getName();

//以流的形式返回上传文件的数据内容。
InputStream getInputStream()

//delete方法用来清空FileItem类对象中存放的主体内容
//如果主体内容被保存在临时文件中，delete方法将删除该临时文件。
void delete();
```

#### ServletFileUpload 类

ServletFileUpload负责处理上传的文件数据，并将表单中每个输入项封装成一个FileItem对象中 . 使用其parseRequest(HttpServletRequest) 方法可以将通过表单中每一个HTML标签提交的数据封装成一个FileItem对象，然后以List列表的形式返回，使用该方法处理上传文件简单易用

### 代码实现

```java
package com.Sucker.servlet;

import org.apache.commons.fileupload.FileItem;
import org.apache.commons.fileupload.FileUploadException;
import org.apache.commons.fileupload.ProgressListener;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.List;
import java.util.UUID;

public class FileServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //判断上传的文件是普通表单还是带文件的表单
        if (!ServletFileUpload.isMultipartContent(req)) {//源码限定必须是post方法
            return; //说明这是一个普通表单，直接返回
        }

        //创建上传文件的保存路径，建议在WEB-INF路径下，安全，用户无法直接访问上传的文件
        String uploadPath = this.getServletContext().getRealPath("/WEB-INF/upload");
        File uploadFile = new File(uploadPath);
        if (!uploadFile.exists()){
            uploadFile.mkdir();//创建这个目录
        }

        //缓存，临时文件
        //临时路径，假如文件超过了预期大小，我们就把它放到一个临时文件中，过几天自动删除，或者提醒用户转存为永久
        String tmpPath = this.getServletContext().getRealPath("/WEB-INF/tmp");
        File file = new File(tmpPath);
        if (!file.exists()){
            file.mkdir();//创建这个目录
        }

        //处理上传的文件一般需要通过流来获取，我们可以通过request.getInputstream(),原生态文件上传流获取，十分麻烦
        //但是我们都建议使用Apache的文件上传组件来实现，common-fileupload,它需要依赖于common-io组件；
        try {
            //1、创建DiskFileItemFactory对象，处理文件上传路径或限制文件大小
            DiskFileItemFactory factory = gteDiskFileItemFactory(file);
            //2、获取ServletFileUpload
            ServletFileUpload upload = getServletFileUpload(factory);
            //3、处理上传文件
            String msg = uploadParseRequest(upload,req,uploadPath);
            //Servlet请求转发消息
            req.setAttribute("msg",msg);
            req.getRequestDispatcher("/info.jsp").forward(req,resp);
        }catch (FileUploadException e){
            e.printStackTrace();
        }
    }

    public static DiskFileItemFactory gteDiskFileItemFactory(File file){
        //1、创建DiskFileItemFactory对象，处理文件上传路径或限制文件大小
        DiskFileItemFactory factory = new DiskFileItemFactory();

        //通过这个工厂设置一个缓冲区，当上传的文件大小大于缓冲区的时候，将它放到临时文件中；
        factory.setSizeThreshold(1024 * 1024);//缓冲区大小为1M
        factory.setRepository(file);
        return factory;
    }
    public static ServletFileUpload getServletFileUpload(DiskFileItemFactory factory){
        //2、获取ServletFileUpload
        ServletFileUpload upload = new ServletFileUpload(factory);
        //监听文件上传进度
        upload.setProgressListener(new ProgressListener() {
            public void update(long pBytesRead, long lpContentLenght, int i) {
                //pBytesRead:已读取到的文件大小
                //pContentLenght：文件大小
                System.out.println("总大小："+lpContentLenght+"已上传："+pBytesRead);
            }
        });

        //处理乱码问题
        upload.setHeaderEncoding("UTF-8");
        //设置单个文件的最大值
        upload.setFileSizeMax(1024 * 1024 * 10);
        //设置总共能够上传文件的大小
        //1024 = 1kb * 1024 = 1M * 10 = 10M
        upload.setSizeMax(1024 * 1024 * 10);
        return upload;
    }
    public static String uploadParseRequest(ServletFileUpload upload,HttpServletRequest request,String uploadpath) throws IOException, FileUploadException {
        String msg = "";
        //3、处理上传文件
        //把前端的请求解析，封装成一个FileItem对象
        List<FileItem> fileItems = upload.parseRequest(request);
        for (FileItem fileItem : fileItems) {
            if (fileItem.isFormField()){ //判断是普通表单还是带文件的表单
                //getFieldName指的是前端表单控件的name
                String name = fileItem.getFieldName();
                String value = fileItem.getString("UTF-8");//处理乱码
                System.out.println(name+":"+value);
            }else {//判断它是带文件的表单

                //======================处理文件=======================//

                //拿到文件的名字
                String uploadFileName = fileItem.getName();
                System.out.println("上传的文件名："+uploadFileName);

                if (uploadFileName.trim().equals("") || uploadFileName == null){
                    continue;
                }

                //获得上传的文件名，例如/img/girl/ooa.jpg,只需要ooa，其前面的后面的都不需要
                String fileName = uploadFileName.substring(uploadFileName.lastIndexOf("/") + 1);
                //获得文件的后缀名
                String fileExtName = uploadFileName.substring(uploadFileName.lastIndexOf(".") + 1);
                      /*
                        如果文件后缀名fileExtName不是我们所需要的
                        就直接return，不处理，告诉用户文件类型不对
                     */

                //可以使用UUID(唯一识别的通用码),保证文件名唯一
                //UUID.randomUUID，随机生一个唯一识别的通用码

                //网络传输中的东西，都需要序列化
                //pojo，实体类，如果想要在多个电脑运行，传输--->需要吧对象都序列化了
                //JNI=java Native Interface
                //implements Serializable ：标记接口，JVM--->java栈 本地方法栈 native-->c++

                String uuidPath= UUID.randomUUID().toString();

                System.out.println("文件信息【文件名："+fileName+"文件类型："+fileExtName+"】");

                //可以使用UUID(唯一通用识别码)来保证文件名的统一
                String uuidFileName = UUID.randomUUID().toString();

                // ================处理文件完毕==============

                // 存到哪? uploadPath
                // 文件真实存在的路径realPath
                String realPath = uploadpath + "/" + uuidPath;
                // 给每个文件创建一个对应的文件夹
                File realPathFile = new File(realPath);
                if (!realPathFile.exists()) {
                    realPathFile.mkdir();
                }
                // ==============存放地址完毕==============


                //=======================传输文件=========================//
                //获得文件上传的流
                InputStream inputStream = fileItem.getInputStream();

                //创建一个文件输出流
                FileOutputStream fos = new FileOutputStream(realPath + "/" + uuidFileName +"."+ fileExtName);

                //创建一个缓冲区
                byte[] buffer = new byte[1024 * 1024];

                //判断是否读取完毕
                int len = 0;

                //如果大于0，说明还存在数据
                while ((len=inputStream.read(buffer))>0){
                    fos.write(buffer,0,len);
                }

                //关闭流
                fos.close();
                inputStream.close();

                msg = "文件上传成功！";
                fileItem.delete();//上传成功，清除临时文件
            }
        }

        return msg;
    }

}
```

配置xml中servlet

```xml
    <servlet>
        <servlet-name>FileServlet</servlet-name>
        <servlet-class>com.Sucker.servlet.FileServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>FileServlet</servlet-name>
        <url-pattern>/upload.do</url-pattern>
    </servlet-mapping>
```

更改首页提交表单

```jsp
  <%--通过表单上传文件
     get: 上传文件大小有限制
     post:上传文件大小没有限制
  --%>
  <form action="${pageContext.request.contextPath}/upload.do" enctype="multipart/form-data" method="post">
    上传用户：<input type="text" name="username"><br/><%--通过上传用户名来用于解决上方四条注意事项--%>
    <p><input type="file" name="file1"></p> <%--选择文件--%>
    <p><input type="file" name="file2"></p> <%--选择文件--%>

    <p><input type="submit"></p> <%--提交按钮--%>
  </form>
```

提交成功跳转页面

```jsp
${msg}
```

测试输出

![](https://img-blog.csdnimg.cn/4a46d0b842ec4f22b831a9f31f93358b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

## 邮件发送

要在网络上实现邮件功能，必须要有专门的**邮件服务器**

这些邮件服务器类似于邮局，主要负责接收用户投递的邮件，并把邮件投递到邮件接收者的邮箱中

### 传输协议

**SMTP协议**：发送邮件

我们通常把处理用户smtp请求（邮件发送请求）的服务器称之为SMTP服务器（邮件发送服务器）

**POP3协议**：接收邮件

我们通常把处理用户pop3（邮件接收请求）的服务器称之为pop3服务器（邮件接收服务器）

### 发送原理

![](https://img-blog.csdnimg.cn/2020042419573470.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzk4NjM3Nw==,size_16,color_FFFFFF,t_70)

### 环境搭建

#### 导入jar包

- mail.jar
- activation.jar

#### 环境配置

在文件传输的项目上new Module--->一个空的java项目，因为使用java实现暂时不用web项目

添加lib目录将jar包拷入其中，将其Add as library

### 使用Java实现邮件发送需要使用的类

JavaMail 是sun公司（现以被甲骨文收购）为方便Java开发人员在应用程序中实现邮件发送和接收功能而提供的一套标准开发包，它支持一些常用的邮件协议，如前面所讲的SMTP，POP3，IMAP,还有MIME等。我们在使用JavaMail API 编写邮件时，无须考虑邮件的底层实现细节，只要调用JavaMail 开发包中相应的API类就可以了。

### 简易文本邮件发送的实现

简单邮件： 没有附件和图片，纯文本文件

![](https://img-blog.csdnimg.cn/20200708003918960.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTE0ODk5Nw==,size_16,color_FFFFFF,t_70#pic_center)

#### 步骤：

**1.创建session对象**

**2.创建Transport对象**

**3.使用邮箱的用户名和授权码连上邮件服务器**

**4.创建一个Message对象（需要传递session）**

- **message需要指明发件人、收件人以及文件内容**

**5.发送邮件**

**6.关闭连接**

#### 获取授权码

![](https://img-blog.csdnimg.cn/4651de62da5543f8ba094066ffc4b9c4.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

#### 代码实现

```java
package com.Sucker;

import com.sun.mail.util.MailSSLSocketFactory;

import javax.mail.*;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import java.security.GeneralSecurityException;
import java.util.Properties;

public class MailDemo01 {

    public static void main(String[] args) throws Exception {
        Properties prop=new Properties();
        prop.setProperty("mail.host","smtp.qq.com");///设置QQ邮件服务器
        prop.setProperty("mail.transport.protocol","smtp");///邮件发送协议
        prop.setProperty("mail.smtp.auth","true");//需要验证用户密码

        //QQ邮箱需要设置SSL加密，其他邮箱不需要
        MailSSLSocketFactory sf=new MailSSLSocketFactory();
        sf.setTrustAllHosts(true);
        prop.put("mail.smtp.ssl.enable","true");
        prop.put("mail.smtp.ssl.socketFactory",sf);

        //使用javaMail发送邮件的5个步骤
        //1.创建定义整个应用程序所需要的环境信息的session对象

        //QQ才有！其他邮箱就不用
        Session session=Session.getDefaultInstance(prop, new Authenticator() {
            public PasswordAuthentication getPasswordAuthentication() {
                //发件人邮件用户名、授权码
                return new PasswordAuthentication("XXXX@qq.com","授权码");
            }
        });

        //开启session的debug模式，这样可以查看到程序发送Email的运行状态
        session.setDebug(true);
        //2.通过session得到transport对象
        Transport ts=session.getTransport();

        //3.使用邮箱的用户名和授权码连上邮件服务器
        ts.connect("smtp.qq.com","XXXX@qq.com","授权码");

        //4.创建邮件：写文件
        //注意需要传递session
        MimeMessage message=new MimeMessage(session);
        //指明邮件的发件人
        message.setFrom(new InternetAddress("XXXX@qq.com"));
        //指明邮件的收件人
        message.setRecipient(Message.RecipientType.TO,new InternetAddress("XXXX@qq.com"));
        //邮件标题
        message.setSubject("发送的标题");
        //邮件的文本内容
        message.setContent("<h1 style='color: red'>nihao </h1>","text/html;charset=UTF-8");

        //5.发送邮件
        ts.sendMessage(message,message.getAllRecipients());

        //6.关闭连接
        ts.close();
    }

}
```

### 复杂文件内容的发送

**复杂邮件就是非纯文本的邮件，可能还包含了图片和附件等资源**

先认识两个类一个名词：

 **MIME（多用途互联网邮件扩展类型）**

- **MimeBodyPart类**

 javax.mail.internet.MimeBodyPart类**表示的是一个MIME消息**，它和MimeMessage类一样都是从Part接口继承过来。即一个MIME消息对应一个MimeBodyPart对象，而MimeBodyPart对象就是我们写的邮件内容中的元素

![](https://img2020.cnblogs.com/blog/1747479/202009/1747479-20200909180643256-2120312525.png)

- **MimeMultipart类**

 javax.mail.internet.MimeMultipart是抽象类 Multipart的实现子类，它**用来组合多个MIME消息**。一个MimeMultipart对象可以包含多个代表MIME消息的MimeBodyPart对象。即一个MimeMultipart对象表示多个MimeBodyPart的集合，而一个MimeMultipart表示的就是我们一封邮件的内容

![](https://img2020.cnblogs.com/blog/1747479/202009/1747479-20200909180657427-1563537314.png)

MimeMultipart对象的使用的时候需要设置setSubType()的属性值，一共就下面3种取值

- alternative：表明这个MimeMultipart对象中的MimeMessage对象的数据是纯文本文件
- related：表明这个MimeMultipart对象中的MimeMessage对象的数据包含非纯文本文件
- mixed：表明这个MimeMultipart对象中的MimeMessage对象的数据包含附件

我们在使得的时候如果不知道使用哪一个，直接使用mixed即可，使用这个属性值一定不会报错

![](https://img2020.cnblogs.com/blog/1747479/202009/1747479-20200909181047132-919140240.png)

相较于简单邮件，复杂邮件变化的地方只是在于邮件内容本身会发送变化，而其他的步骤都是一样的

 1、准备一些参数

 2、获取session对象

 3、获取传输对象

 4、登陆授权

 5、写邮件 (和简单邮件相区别)

 6、发送邮件

 7、关闭服务器资源

**包含图片的复杂文件**

```java
package com.Sucker;

import com.sun.mail.util.MailSSLSocketFactory;

import javax.activation.DataHandler;
import javax.activation.FileDataSource;
import javax.mail.*;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeBodyPart;
import javax.mail.internet.MimeMessage;
import javax.mail.internet.MimeMultipart;
import java.security.GeneralSecurityException;
import java.util.Properties;

public class MailDemo01 {

    public static void main(String[] args) throws Exception {
        Properties prop=new Properties();
        prop.setProperty("mail.host","smtp.qq.com");///设置QQ邮件服务器
        prop.setProperty("mail.transport.protocol","smtp");///邮件发送协议
        prop.setProperty("mail.smtp.auth","true");//需要验证用户密码

        //QQ邮箱需要设置SSL加密，其他邮箱不需要
        MailSSLSocketFactory sf=new MailSSLSocketFactory();
        sf.setTrustAllHosts(true);
        prop.put("mail.smtp.ssl.enable","true");
        prop.put("mail.smtp.ssl.socketFactory",sf);

        //使用javaMail发送邮件的5个步骤
        //1.创建定义整个应用程序所需要的环境信息的session对象

        //QQ才有！其他邮箱就不用
        Session session=Session.getDefaultInstance(prop, new Authenticator() {
            public PasswordAuthentication getPasswordAuthentication() {
                //发件人邮件用户名、授权码
                return new PasswordAuthentication("XXXX@qq.com","授权码");
            }
        });

        //开启session的debug模式，这样可以查看到程序发送Email的运行状态
        session.setDebug(true);
        //2.通过session得到transport对象
        Transport ts=session.getTransport();

        //3.使用邮箱的用户名和授权码连上邮件服务器
        ts.connect("smtp.qq.com","XXXX@qq.com","授权码");

        //4.创建邮件：写文件
        //注意需要传递session
        MimeMessage message=new MimeMessage(session);
        //指明邮件的发件人
        message.setFrom(new InternetAddress("XXXX@qq.com"));
        //指明邮件的收件人
        message.setRecipient(Message.RecipientType.TO,new InternetAddress("XXXX@qq.com"));
        //邮件标题
        message.setSubject("发送的标题");

        System.out.println("=============================复杂邮件的邮件内容设置==================================");

        // 准备邮件数据

        // 准备图片数据
        MimeBodyPart image = new MimeBodyPart();//获取一个图片的MimeBodyPart对象
        DataHandler dh = new DataHandler(new FileDataSource("src/1.png"));//由于图片需要字符化才能传输，所以需要获取一个DataHandler对象
        image.setDataHandler(dh);//放入处理的图片数据
        image.setContentID("bz.jpg");//为图片的MimeBodyPart对象设置一个ID，我们在文字中就可以使用它了

        // 准备正文数据
        MimeBodyPart text = new MimeBodyPart();//获取一个文本的MimeBodyPart对象
        text.setContent("这是一封邮件正文带图片<img src='cid:bz.jpg'>的邮件", "text/html;charset=UTF-8");//设置文本内容，注意在里面嵌入了<img src='cid:bz.jpg'>

        // 描述数据关系
        MimeMultipart mm = new MimeMultipart();//获取MimeMultipart
        mm.addBodyPart(text);//将文本MimeBodyPart对象加入MimeMultipart中
        mm.addBodyPart(image);//将图片MimeBodyPart对象加入MimeMultipart中
        mm.setSubType("related");//设置MimeMultipart对象的相对熟悉为related，即发送的数据为文本+非附件资源

        //设置到消息中，保存修改
        message.setContent(mm);//将MimeMultipart放入消息对象中
        message.saveChanges();//保存上面的修改

        System.out.println("===============================================================");

        //5.发送邮件
        ts.sendMessage(message,message.getAllRecipients());

        //6.关闭连接
        ts.close();


    }

}
```

**发送包含附件的复杂邮件**

包装成方法调用即可

```java
System.out.println("=============================复杂邮件的邮件内容设置==================================");

 /*
编写邮件内容
1.图片
2.附件
3.文本
 */

//图片
MimeBodyPart body1 = new MimeBodyPart();
body1.setDataHandler(new DataHandler(new FileDataSource("图片的绝对地址")));
body1.setContentID("yhbxb.png"); //图片设置ID

//文本
MimeBodyPart body2 = new MimeBodyPart();
body2.setContent("请注意，我不是广告<img src='cid:yhbxb.png'>","text/html;charset=utf-8");

//附件
MimeBodyPart body3 = new MimeBodyPart();
body3.setDataHandler(new DataHandler(new FileDataSource("附件1的绝对地址")));
body3.setFileName("test.c"); //附件设置名字

MimeBodyPart body4 = new MimeBodyPart();
body4.setDataHandler(new DataHandler(new FileDataSource("附件2的绝对地址")));
body4.setFileName("test.txt"); //附件设置名字

//拼装邮件正文内容
MimeMultipart multipart1 = new MimeMultipart();
multipart1.addBodyPart(body1);
multipart1.addBodyPart(body2);
multipart1.setSubType("related"); //1.文本和图片内嵌成功！

//new MimeBodyPart().setContent(multipart1); //将拼装好的正文内容设置为主体
MimeBodyPart contentText =  new MimeBodyPart();
contentText.setContent(multipart1);

//拼接附件
MimeMultipart allFile =new MimeMultipart();
allFile.addBodyPart(body3); //附件
allFile.addBodyPart(body4); //附件
allFile.addBodyPart(contentText);//正文
allFile.setSubType("mixed"); //正文和附件都存在邮件中，所有类型设置为mixed；

//设置到消息中，保存修改
message.setContent(allFile);//将MimeMultipart放入消息对象中
message.saveChanges();//保存上面的修改

System.out.println("===============================================================");
```

## JavaWeb网站注册发送邮件

### 环境配置

分析：在我们注册的时候，前端我们填写的就是一个表单，这个表单提交给后端的servlet，这个servlet就向我们填写的那个邮箱中发送一封邮件

所以我们需要创建一个javaweb项目，因为要使用到前端页面+servlet

创建一个普通Maven项目，补全web文件夹（右键Add Framework Support）

配置Tomcat，测试使用

### 前端页面

```xml
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>注册</title>
  </head>
  <body>

    <form action="${pageContext.request.contextPath}/RegisterServlet.do" method="post">
      用户名：<input type="text" name="username"><br/>
      密码：<input type="password" name="password"><br/>
      邮箱：<input type="text" name="email"><br/>

      <input type="submit" value="注册">
    </form>

  </body>
</html>
```

### Servlet

```java
public class RegisterServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String username=req.getParameter("username");
        String password=req.getParameter("password");
        String email=req.getParameter("email");

        User user=new User(username,password,email);
        Sendmail send=new Sendmail(user);
        send.start();
        System.out.println("success");

    }
}
```

### Servlet注册

```xml
<servlet>
    <servlet-name>RegisterServlet</servlet-name>
    <servlet-class>com.Sucker.servlet.RegisterServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>RegisterServlet</servlet-name>
    <url-pattern>/RegisterServlet.do</url-pattern>
</servlet-mapping>
```

### 导包

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
</dependency>
```

### 实体类

```java
package com.Sucker.pojo;

public class User {

    private String username;
    private String password;
    private String email;

    public User() {
    }

    public User(String username, String password, String email) {
        this.username = username;
        this.password = password;
        this.email = email;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    @Override
    public String toString() {
        return "User{" +
                "username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", email='" + email + '\'' +
                '}';
    }

}
```

**注意在项目结构中的Modules中导入lib(2)目录，方便实现项目之间jar包复用**

**注意Artifacts中导包**

![](https://img-blog.csdnimg.cn/4dc640ec3fa740aba924567707a1aa63.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

**注意Tomcat中导包**

![](https://img-blog.csdnimg.cn/95c19d39cf794e83b9c3b82b9fd7ff33.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### 工具类代码

```java
package com.Sucker.utils;

import com.Sucker.pojo.User;
import com.sun.mail.util.MailSSLSocketFactory;

import javax.mail.*;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import java.util.Properties;

//网站三秒原则 : 用户体验
//多线程实现用户体验！  （异步处理）
public class Sendmail extends Thread{

    private String from="XXX@qq.com";

    private String host="smtp.qq.com";

    private User user;

    public Sendmail(User user){
        this.user=user;
    }
    @Override
    public void run() {
        try {
            Properties prop=new Properties();
            prop.setProperty("mail.host",host);///设置QQ邮件服务器
            prop.setProperty("mail.transport.protocol","smtp");///邮件发送协议
            prop.setProperty("mail.smtp.auth","true");//需要验证用户密码
            //QQ邮箱需要设置SSL加密
            MailSSLSocketFactory sf=new MailSSLSocketFactory();
            sf.setTrustAllHosts(true);
            prop.put("mail.smtp.ssl.enable","true");
            prop.put("mail.smtp.ssl.socketFactory",sf);

            //使用javaMail发送邮件的5个步骤
            //1.创建定义整个应用程序所需要的环境信息的session对象
            Session session= Session.getDefaultInstance(prop, new Authenticator() {
                @Override
                protected PasswordAuthentication getPasswordAuthentication() {
                    return new PasswordAuthentication(from,"授权码");
                }
            });
            //开启session的debug模式，这样可以查看到程序发送Email的运行状态
            session.setDebug(true);
            //2.通过session得到transport对象
            Transport ts=session.getTransport();
            //3.使用邮箱的用户名和授权码连上邮件服务器
            ts.connect(host,from,"授权码");
            //4.创建邮件：写文件
            //注意需要传递session
            MimeMessage message=new MimeMessage(session);
            //指明邮件的发件人
            message.setFrom(new InternetAddress(from));
            //指明邮件的收件人
            message.setRecipient(Message.RecipientType.TO,new InternetAddress(user.getEmail()));
            //邮件标题
            message.setSubject("注册通知");
            //邮件的文本内容
            message.setContent("恭喜你("+user.getUsername()+")成功注册！"+"密码："+user.getPassword()
                    ,"text/html;charset=UTF-8");
            //5.发送邮件
            ts.sendMessage(message,message.getAllRecipients());

            //6.关闭连接
            ts.close();
        }catch (Exception e){
            System.out.println(e);
        }

    }

}
```

成功后跳转页面

```jsp
<h1>xxx网站温馨提示</h1>
${message}
```

