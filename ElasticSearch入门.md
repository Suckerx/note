## ElasticSearch

版本:ElasticSearch 7.6.1

SQL:  Like%狂神说%，如果是大数据，就十分慢！此时用索引能优化！

ElasticSearch：搜索！（大数据量！）

Lucene 是一套信息检索工具包！ jar包！不包含 搜索引擎系统！

包含：索引结构！读写索引的工具！排序，搜索规则...工具类！

**Lucene 和 ElasticSearch 关系：**

ElasticSearch 是基于 Lucene 做了一些封装和增强

## ElasticSearch概述

**Elaticsearch**，简称为ES，ES是一个开源的**高扩展**的**分布式全文检索引擎**，它可以近乎**实时的存储**、检索数据；本身扩展性很好，可以扩展到上百台服务器，处理 PB 级别（大数据时代）的数据。ES由 Java 语言开发并使用 Lucene 作为其核心来实现所有索引和搜索的功能，但是它的目的是通过简单的**RESTFULL API**来隐藏 Lucene 的复杂性，从而让全文搜索变得简单。据国际权威的数据库产品评测机构 DB Engines 的统计，在2016 年1月，ElasticSearch 已超过 Solr 等，成为排名第一的搜索引擎类应用。

## ES和solr的差别

### Elasticsearch简介

Elasticsearch是一个实时分布式搜索和分析引擎。

它让你以前所未有的速度处理大数据成为可能。

它用于**全文搜索**、**结构化搜索**、**分析**以及将这三者混合使用︰

维基百科使用Elasticsearch提供全文搜索并高亮关键字，以及输入实时搜索(search-asyou-type)和搜索纠错(did-you-mean)等搜索建议功能。

英国卫报使用Elasticsearch结合用户日志和社交网络数据提供给他们的编辑以实时的反馈，以便及时了解公众对新发表的文章的回应。

StackOverflow结合全文搜索与地理位置查询，以及more-like-this功能来找到相关的问题和答案。Github使用Elasticsearch检索1300亿行的代码。

但是Elasticsearch不仅用于大型企业，它还让像DataDog以及Klout这样的创业公司将最初的想法变成可扩展的解决方案。Elasticsearch可以在你的笔记本上运行，也可以在数以百计的服务器上处理PB级别的数据。

Elasticsearch是一个基于Apache Lucene™的开源搜索引擎。无论在开源还是专有领域，Lucene可以被认为是迄今为止最先进、性能最好的、功能最全的搜索引擎库。

但是，Lucene只是一个库。想要使用它，你必须使用ava来作为开发语言并将其直接集成到你的应用中，更糟糕的是, Lucene非常复杂，你需要深入了解检索的相关知识来理解它是如何工作的。

Elasticsearch也使用Java开发并使用Lucene作为其核心来实现所有索引和搜索的功能，但是它的目的是通过简单的RESTful API来隐藏Lucene的复杂性，从而让全文搜索变得简单。

### Solr简介

Solr是Apache下的一个顶级开源项目，采用ava开发，它是基于Lucene的全文搜索服务器。Solr提供了比Lucene更为丰富的查询语言，同时实现了可配置、可扩展，并对索引、搜索性能进行了优化

Solr可以独立运行，运行在)ltty、Tomcat等这些Servlet容器中，Solr索引的实现方法很简单，**用POST方法向Solr服务器发送一个描述Field及其内容的XML文档，Solr根据xml文档添加、删除、更新索引**。Solr搜索只需要发送HTTP GET请求然后对 Solr返回Xml.json等格式的查询结果进行解析，组织页面布局。Solr不提供构建UI的功能，Solr提供了一个管理界面，通过管理界面可以查询Solr的配置和运行情况。

solr是基于lucene开发企业级搜索服务器，实际上就是封装了lucene。

Solr是一个独立的企业级搜索应用服务器，它对外提供类似于**Web-service的APl接口**。用户可以通过http请求，向搜索引擎服务器提衣一定格式的文件，牛成索引:也可以通讨提出杳找请求，并得到返回结果

### Lucene简介

Lucene是apache软件基金会4 jakarta项目组的一个子项目，是一个开放源代码的全文检索引擎工具包，但它不是一个完整的全文检索引擎，而是一个全文检索引擎的架构，提供了完整的查询引擎和索引引擎，部分文本分析引擎（英文与德文两种西方语言)。Lucene的目的是为软件开发人员提供一个简单易用的工具包，以方便的在目标系统中实现全文检索的功能，或者是以此为基础建立起完整的全文检索引擎。Lucene是一套用于全文检索和搜寻的开源程式库，由Apache软件基金会支持和提供。Lucene提供了一个简单却强大的应用程式接口，能够做全文索引和搜寻。在Java开发环境里Lucene是一个成熟的免费开源工具。就其本身而言，Lucene是当前以及最近几年最受欢迎的免费Java信息检索程序库。人们经常提到信息检索程序库，虽然与搜索引擎有关，但不应该将信息检索程序库与搜索引擎相混淆。

Lucene是一个全文检索引擎的架构。那什么是全文搜索引擎?

全文搜索引擎是名副其实的搜索引擎，国外具代表性的有Google、Fast/AliTheWeb、AltaVista、Inktomi、Teoma、WiseNut等，国内著名的有百度(Baidu )。它们都是通过从互联网上提取的各个网站的信息（以网页文字为主）而建立的数据库中，检索与用户查询条件匹配的相关记录，然后按一定的排列顺序将结果返回给用户，因此他们是真正的搜索引擎。

从搜索结果来源的角度，全文搜索引擎又可细分为两种，一种是拥有自己的检索程序(Indexer )，俗称"蜘蛛" ( Spider )程序或"机器人" ( Robot)程序，并自建网页数据库，搜索结果直接从自身的数据库中调用，如上面提到的7家引擎;另一种则是租用其他引擎的数据库，并按自定的格式排列搜索结果，如Lycos引擎。

### ElasticSearch和Solr比较

![](https://img-blog.csdnimg.cn/54598637c40f400897cebeeffd0df6c0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/e60c0fc791f94002b94d743b7a4479a3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/6494e273800243c5badd888854c8bc41.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/deffae585fa94a5fa191115f1ae628d6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 总结

1、es基本是开箱即用，非常简单。Solr安装略微复杂一丢丢!

2、Solr利用Zookeeper进行分布式管理，而Elasticsearch自身带有分布式协调管理功能。

3、polr支持更多格式的数据，比如ISON、XML、CSv，而Elasticsearch仅支持json文件格式。

4、Solr官方提供的功能更多，而Elasticsearch本身更注重于核心功能，高级功能多有第三方插件提供，例如图形化界面需要kibana友好支撑

5、Solr查询快，但更新索引时慢（即插入删除慢），用于电商等查询多的应用；

- ES建立索引快（即查询慢），即实时性查询快，用于facebook新浪等搜索。
- Solr是传统搜索应用的有力解决方案，但Elasticsearch更适用于新兴的实时搜索应用。

6、Solr比较成熟，有一个更大，更成熟的用户、开发和贡献者社区，而Elasticsearch相对开发维护者较少，更新太快，学习使用成本较高。

## ElasticSearch安装

### ElasticSearch安装

下载地址：[Download Elasticsearch Free | Get Started Now | Elastic | Elastic](https://www.elastic.co/cn/downloads/elasticsearch#ga-release)

先在Windows下学习！

放在Environment目录下，解压即可使用

1. 解压

![](https://img-blog.csdnimg.cn/55595abebce645938543f5984831d807.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

2. 目录

   ```
   bin  启动文件
   config  配置文件
       log4j2  日志配置文件
       jvm.options  java 虚拟机相关的配置 注意其中4g表示需要的内存，可自己改小到1g或256M
       elasticsearch.yml  elasticsearch 的配置文件 默认端口9200
   lib     相关jar包
   logs    日志！
   modules 功能模块
   plugins 插件！
   ```

   ![](https://img-blog.csdnimg.cn/c7a6e66fc2fc4bf8a5f944330de2e5fd.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_14,color_FFFFFF,t_70,g_se,x_16)

3. 启动

   bin/elasticsearch.bat启动

   ![](https://img-blog.csdnimg.cn/img_convert/95bc163644221c97388540aa33c13655.png)

4. 访问测试

   ![](https://img-blog.csdnimg.cn/794248d626e84cc6afd8ed5db90a74b8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_14,color_FFFFFF,t_70,g_se,x_16)



### 可视化界面es head插件

下载地址：[Releases · mobz/elasticsearch-head · GitHub](https://github.com/mobz/elasticsearch-head/releases)

启动：在eshead安装包下启动npm run start

```xml
npm install（或者使用镜像 cnpm）
npm run start
```

连接测试发现，存在跨域问题：配置es的yml配置文件，加入

```
http.cors.enabled: true
http.cors.allow-origin: "*"
```

![](https://img-blog.csdnimg.cn/img_convert/3a03cc79cf5ad204cec3c2d466438a66.png)

重启es服务器，再次连接(localhost:9100)

![](https://img-blog.csdnimg.cn/1b2fc8fdcedc4ff693d6e142b4a2b178.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

初学时，将es当作一个数据库！（可以建立索引（库），文档（库中的数据！））

这个head我们把他当作数据展示工具！我们后面所有的查询，使用Kibana来做

### 了解ELK

ELK是Elasticsearch、Logstash、Kibana三大开源框架首字母大写简称。市面上也被成为Elastit Stack。其中Elasticsearch是一个基于Lucene、分布式、通过Restful方式进行交互的近实时搜索平台框架。像类似百度、谷歌这种大数据全文搜索引擎的场景都可以使用Elasticsearch作为底层支持框架，可见Elasticsearch提供的搜索能力确实强大,市面上很多时候我们简称Elasticsearch为es。Logstash是ELK的中央数据流引擎，用于从不同目标（文件/数据存储/MQ）收集的不同格式数据，经过过滤后支持输出到不同目的地(文件/MQ/redis/elasticsearch/kafka等 )。Kibana可以将elasticsearch的数据通过友好的页面展示出来，提供实时分析的功能.

收集清洗数据-->搜索，存储-->Kibana

市面上很多开发只要提到ELK能够一致说出它是一个日志分析架构技术栈总称，但实际上ELK不仅仅适用于日志分析，它还可以支持其它任何数据分析和收集的场景，日志分析和收集只是更具有代表性。并非唯一性。
 ![](https://img-blog.csdnimg.cn/e0ceae1707264bbdbe702ac2c76ca22c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 安装Kibana

Kibana是一个针对Elasticsearch的开源分析及可视化平台，用来搜索、查看交互存储在Elasticsearch索引中的数据。使用Kibana ,可以通过各种图表进行高级数据分析及展示。Kibana让海量数据更容易理解。它操作简单，基于浏览器的用户界面可以快速创建仪表板( dashboard ) 实时显示Elasticsearch查询动态。设置Kibana非常简单。无需编码或者额外的基础架构，几分钟内就可以完成Kibana安装并启动Elasticsearch索引监测。

官网https://www.elastic.co/cn/downloads/kibana

Kibana 版本要和 Es一致 此处都是7.15.0

**好处**:ELK都是基本上拆箱即用

启动测试：

1. 解压后的目录

   ![](https://img-blog.csdnimg.cn/780304556e2f478a9586d430969c4b94.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

2. 启动

   bin/kibana.bat

   默认端口：5601

   ![](https://img-blog.csdnimg.cn/d6c6ba524d7444d492f74996a619783a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

3. 访问测试

   ![](https://img-blog.csdnimg.cn/bf25d680dcfb46a29532e72002acbea9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

4. 开发工具！（Postman、curl、head、谷歌浏览器插件测试）

   左边菜单 Dev Tools

   ![](https://img-blog.csdnimg.cn/3e3921eda55842c5bf70db02649b6fc4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

之后的所有操作都在这里进行编写！

5. 汉化！修改kibana配置即可

   config-->kibana.yml

   i18n.locale: "zh-CN"

   ![](https://img-blog.csdnimg.cn/b4d4488c0ee34daabc389ca21e32be27.png)



## ES核心概念

1. 索引
2. 字段类型（mapping）
3. 文档（documents）

`概述`

在前面的学习中，我们已经掌握了es是什么，同时也把es的服务已经安装启动，那么es是如何去存储数据，数据结构是什么，又是如何实现搜索的呢?我们先来聊聊ElasticSearch的相关概念吧!

**集群，节点，索引，类型，文档，分片，映射是什么?**

`elasticsearch是面向文档,关系行数据库和elasticsearch客观的对比 一切都是JSON`

![](https://img-blog.csdnimg.cn/0706f0d97219484398c7472be84248da.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

elasticsearch(集群)中可以包含多个索引(数据库)，每个索引中可以包含多个类型(表)，每个类型下又包含多个文档行)，每个文档中又包含多个字段(列)。

### 物理设计:

elasticsearch在后台把每个索引划分成多个分片，每分分片可以在集群中的不同服务器间迁移

一个人就是一个集群,默认的集群名称就是ElasticSearch

![](https://img-blog.csdnimg.cn/1c5724f65cde42a7b88b8ba1f89d9797.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 逻辑设计∶

一个索引类型中，包含多个文档，比如说文档1，文档2。当我们索引一篇文档时，可以通过这样的一各顺序找到它:索引》类型文档ID，通过这个组合我们就能索引到某个具体的文档。注意:ID不必是整数，实际上它是个字符串

`文档`

之前说elasticsearch是面向文档的，那么就意味着索引和搜索数据的最小单位是文档，elasticsearch中，文档有几个重要属性︰

- 自我包含，一篇文档同时包含字段和对应的值，也就是同时包含key:value !
- 可以是层次型的，一个文档中包含自文档，复杂的逻辑实体就是这么来的!
- 灵活的结构，文档不依赖预先定义的模式，我们知道关系型数据库中，要提前定义字段才能使用，在elasticsearch中，对于字段是非常灵活的，有时候，我们可以忽略该字段，或者动态的添加一个新的字段。

尽管我们可以随意的新增或者忽略某个字段，但是，每个字段的类型非常重要，比如一个年龄字段类型，可以是字符串也可以是整形。因为elasticsearch会保存字段和类型之间的映射及其他的设置。这种映射具体到每个映射的每种类型，这也是为什么在elasticsearch中，类型有时候也称为映射类型。

`类型`

类型是文档的逻辑容器，就像关系型数据库一样，表格是行的容器。类型中对于字段的定义称为映射，比如name映射为字符串类型。我们说文档是无模式的，它们不需要拥有映射中所定义的所有字段，比如新增一个字段，那么elasticsearch是怎么做的呢?elasticsearch会自动的将新字段加入映射，但是这个字段的不确定它是什么类型，elasticsearch就开始猜，如果这个值是18，那么elasticsearch会认为它是整形。但是elasticsearch也可能猜不对，所以最安全的方式就是提前定义好所需要的映射，这点跟关系型数据库殊途同归了，先定义好字段，然后再使用，别整什么幺蛾子。


`索引`

就是数据库

索引是映射类型的容器，elasticsearch中的索引是一个非常大的文档集合。索引存储了映射类型的字段和其他设置。然后它们被存储到了各个分片上了。我们来研究下分片是如何工作的。

**物理设计︰节点和分片如何工作**

![](https://img-blog.csdnimg.cn/f5729bb927094eb19d2e3b4e38a9658e.png)

一个集群至少有一个节点，而一个节点就是一个elasricsearch进程，节点可以有多个索引默认的，如果你创建索引，那么索引将会有个5个分片( primary shard ,又称主分片)构成的，每一个主分片会有一个副本( replica shard ,又称复制分片)

![](https://img-blog.csdnimg.cn/c9ab6ace1dce4b28a5f3cf7c49894678.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

上图是一个有3个节点的集群，可以看到主分片和对应的复制分片都不会在同一个节点内，这样有利于某个节点挂掉了，数据也不至于丢失。实际上，一个分片是一个Lucene索引，一个包含倒排索引的文件目录，倒排索引的结构使得elasticsearch在不扫描全部文档的情况下，就能告诉你哪些文档包含特定的关键字。不过，等等，倒排索引是什么鬼?

`倒排索引`

elasticsearch使用的是一种称为倒排索引的结构，采用Lucene倒排索作为底层。这种结构适用于快速的全文搜索，一个索引文档中所有不重复的列表构成，对于每一个词，都有一个包含它的文档列表。例如，现在有两个文档，每个文档包含如下内容∶

```
Study every day,good good up to forever # 文档1包含的内容
To forever, study every day, good good up # 文档2包含的内容
```

为了创建倒排索引，我们首先要将每个文档拆分成独立的词(或称为词条或者tokens)，然后创建一个包含所有不重复的词条的排序列表，然后列出每个词条出现在哪个文档:

![](https://img-blog.csdnimg.cn/ecad6756ce054f99bbacbe141a0afd79.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

现在，我们试图搜索to forever，只需要查看包含每个词条的文档

![](https://img-blog.csdnimg.cn/535437eed22147fe94be2a29cb6b85a8.png)

两个文档都匹配，但是第一个文档比第二个匹配程度更高。如果没有别的条件，现在，这两个包含关键字的文档都将返回。再来看一个示例，比如我们通过博客标签来搜索博客文章。那么倒排索引列表就是这样的一个结构:

![](https://img-blog.csdnimg.cn/15307272e1354903afca0dcbefdbc290.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

如果要搜索含有python标签的文章，那相对于查找所有原始数据而言，查找倒排索引后的数据将会快的多。只需要查看标签这一栏，然后获取相关的文章ID即可。完全过滤掉无关的所有数据，提高效率!

**elasticsearch的索引和Lucene的索引对比**

在elasticsearch中，索引（库)这个词被频繁使用，这就是术语的使用。在elasticsearch中，索引被分为多个分片，每份分片是一个Lucene的索引。所以一个elasticsearch索引是由多个Lucene索引组成的。别问为什么，谁让elasticsearch使用Lucene作为底层呢!如无特指，说起索引都是指elasticsearch的索引。

接下来的一切操作都在kibana中Dev Tools下的Console里完成。基础操作!

## IK分词器插件

> 什么是IK分词器

分词︰即把一段中文或者别的划分成一个个的关键字，我们在搜索时候会把自己的信息进行分词，会把数据库中或者索引库中的数据进行分词，然后进行一个匹配操作，默认的中文分词是将每个字看成一个词，比如““我爱狂神"会被分为"我”“爱”“狂”"神”，这显然是不符合要求的，所以我们需要安装中文分词器ik来解决这个问题。

如果要使用中文,建议使用ik分词器

IK提供了两个分词算法: ik smart和ik_max_word，其中ik_smart为最少切分， ik_max_word为最细粒度划分!一会我们测试!

> 1.安装

- 下载https://github.com/medcl/elasticsearch-analysis-ik
- 下载完毕后,放入我们的ElasticSearch插件中即可

- 解压到ElasticSearch-->Plugins

![](https://img-blog.csdnimg.cn/94c03bf011e0417881f987dfa6a1fd20.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 重启观察ES，可以看到ik分词器被加载了

- 可以通过命令行查看加载进来的插件

  ![](https://img-blog.csdnimg.cn/8797b91f80704123ba5a770cb4f24eff.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

> 使用kibana测试

ik_smart为最少切分

![](https://img-blog.csdnimg.cn/322799cc05c74afcae51e0a09a7a2d27.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

ik_max_word为最细粒度划分!

![](https://img-blog.csdnimg.cn/a9ee7e84099b4c85b268d5bec3754d2e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

> 问题

![](https://img-blog.csdnimg.cn/772f3596d6e04a0fb411164a99a50a80.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

发现问题: 阿灰被拆开了

这种需要的词,需要自己加到我们的分词器的字典中

> ik分词器增加自己的配置

![](https://img-blog.csdnimg.cn/fb62f83f07564f18a06cc810145e9b16.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

重启ES

![](https://img-blog.csdnimg.cn/c2083ead498d4104bea944cffef1bf51.png)

重启后再次测试

![](https://img-blog.csdnimg.cn/c61bcd7d478e4aee8f765a5f90e4f0a6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

以后的话,我们需要自己配置分词就在自己定义的dic文件中进行配置即可

## Rest风格说明

一种软件架构风格,而不是标准,只是提供了一组设计原则和约束条件.它主要是用于客户端和服务器交互类的软件.基于这个风格设计的软件可以更简洁,更有层次,更易于实现缓存等机制

基本Rest命令说明:

| method | url地址                                         | 描述                 |
| ------ | ----------------------------------------------- | -------------------- |
| PUT    | localhost:9200/索引名称/类型名称/文档id         | 创建文档(指定文档id) |
| POST   | localhost:9200/索引名称/类型名称                | 创建文档(随机文档id) |
| POST   | localhost:9200/索引名称/类型名称/文档id/_update | 修改文档             |
| DELETE | localhost:9200/索引名称/类型名称/文档id         | 删除文档             |
| GET    | localhost:9200/索引名称/类型名称/文档id         | 查询文档通过文档id   |
| POST   | localhost:9200/索引名称/类型名称/_search        | 查询所有数据         |

## 索引的基本操作

1. 创建第一个索引

   ```
   PUT /索引名/~索引名(未来可能取消不写)~/文档id
   {请求体}
   ```

   ![](https://img-blog.csdnimg.cn/e17fc1a44e7245a7891ad71b90c2106a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

   完成了自动增加了索引!数据也成功的添加了，这就是我说大家在初期可以把它当做数据库学习的原因

   ![](https://img-blog.csdnimg.cn/5549ac96afac4af8888555638449acbc.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

2. 那么name这个字段用不用指定类型呢.毕竟我们关系型数据库时需要指定类型的啊

   - 字符串类型
     - text, keyword

   - 数值类型
     - long, integer, short, byte, double, float, half float, scaled fload

   - 日期类型
     - date

   - 布尔值类型
     - boolean

   - 二进制类型
     - binary

   等等…

3. 指定字段的类型

   ![](https://img-blog.csdnimg.cn/efd812bf3f3d40548e1ae20cf61b834c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

4. 获得这个规则信息, 可以通过GET请求获取具体的信息

   ![](https://img-blog.csdnimg.cn/0a689698436643af8fbf95ae46e0b446.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

5. 查看默认的信息

   ```
   PUT /test3/_doc/1
   {
     "name": "Sucker",
     "age": 13,
     "birth": "1997-01-01"
   }
   
   结果：
   {
     "_index" : "test3",
     "_type" : "_doc",
     "_id" : "1",
     "_version" : 1,
     "result" : "created",
     "_shards" : {
       "total" : 2,
       "successful" : 1,
       "failed" : 0
     },
     "_seq_no" : 0,
     "_primary_term" : 1
   }
   ```

   ```
   GET test3
   
   结果：
   {
     "test3" : {
       "aliases" : { },
       "mappings" : {
         "properties" : {
           "age" : {
             "type" : "long"
           },
           "birth" : {
             "type" : "date"
           },
           "name" : {
             "type" : "text",
             "fields" : {
               "keyword" : {
                 "type" : "keyword",
                 "ignore_above" : 256
               }
             }
           }
         }
       },
       "settings" : {
         "index" : {
           "routing" : {
             "allocation" : {
               "include" : {
                 "_tier_preference" : "data_content"
               }
             }
           },
           "number_of_shards" : "1",
           "provided_name" : "test3",
           "creation_date" : "1633854477972",
           "number_of_replicas" : "1",
           "uuid" : "RNOVq34kTjOzeEXSl-tYQQ",
           "version" : {
             "created" : "7150099"
           }
         }
       }
     }
   }
   
   ```

   如果自己的文档字段类型没有指定，那么es就会给我们默认配置字段类型！

**扩展:**

通过get _cat/ 可以获得当前的很多信息

![](https://img-blog.csdnimg.cn/a8d85b0ca32d491bbcfe770165069a98.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

> **修改** 提交还是使用PUT即可,然后覆盖值,或用新办法

曾经的方法 用PUT覆盖，若某个数据漏了，则原来的数据会消失

![](https://img-blog.csdnimg.cn/762ba4d5edbc444996d3a1a6fea44d0e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

目前的方法

使用post

![](https://img-blog.csdnimg.cn/ae18ddf1914d451695e1e9cd155852de.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

> 删除索引

使用DELETE 命令实现删除，根据你的请求来判断是删除索引还是删除文档记录！

使用RESTFUL 风格是ES推荐使用的!

![](https://img-blog.csdnimg.cn/81605a629cf647c2b8a6767b0d2fe5f6.png)

## 关于文档的基本操作 (重点)

### 基本操作

1. 添加数据

   ```java
   PUT ahui/test/1
   {
     "name": "ahui",
     "age": 21,
     "desc": "愿你拥有大风与烈酒,也能享受孤独与自由",
     "tags": ["二次元","宅男","码农"]
   }
   ```

   ![](https://img-blog.csdnimg.cn/bdbda0bccb324eddb53877e4d0f464b1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

2. 获取数据  GET

   ```java
   GET sucker/user/1
   ```

   ![](https://img-blog.csdnimg.cn/25d61e45d90a46c883dec9e956162a93.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

3. 更新数据 PUT（用POST也行）

   ```java
   PUT /sucker/user/3
   {
     "name": "李四233",
     "age": 23,
     "desc": "八嘎",
     "tags": ["靓女","旅游","渣男"]
   }
   ```

   ![](https://img-blog.csdnimg.cn/90b047ca0ec840f7b14c7603652a5587.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

4. POST _update，推荐使用这种更新方式！

   ```java
   POST sucker/user/1/_update
   {
     "doc":{
       "name":"sucker说java"
     }
   }
   ```

   ![](https://img-blog.csdnimg.cn/d1d177e0a05447a798d1443cc029c6a1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

简单的搜索：

```java
GET sucker/user/1
```

简单的条件查询，可以根据默认的映射规则，产生基本的查询！

### 复杂搜索操作

> 复杂搜索操作   select （排序，分页，高亮，模糊查询，精准查询！）

![](https://img-blog.csdnimg.cn/8b59bd7f4cfa4c028a0be9e38d606c17.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
GET sucker/user/_search
{
  "query":{
    "match": {
      "name": "sucker"
    }
  }
}
```

![](https://img-blog.csdnimg.cn/1fa05b42efc34c81a6fba2e164aebe94.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/c8eafa8a4a2b4e2bba9bdb618a10aeb2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/4bc13cb378234e169b134b43b4b1e7b8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

我们之后使用Java操作ES，所有的方法和对象就是这里面的 key ！ 

### 排序

asc升序，desc降序

```java
GET sucker/user/_search
{
  "query":{
    "match": {
      "name": "sucker"
    }
  },
  "sort": [
    {
      "age" : {
        "order": "asc"
      }
    }
  ]
}
```

![](https://img-blog.csdnimg.cn/66dc24427f3840a48505f5911c2179de.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 分页

```java
  "from": 0,
  "size": 2
```

![](https://img-blog.csdnimg.cn/2dad001394534cf0ac61084bc8d51017.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

数据下标仍然从0开始，与所学数据结构相同！

### 布尔值查询

bool中可以进行多条件查询

must命令相当于and，所有的条件都必须符合  where id = 1 and name = xx

```java
GET sucker/user/_search
{
  "query":{
    "bool": {
      "must": [
        {
          "match": {
            "name": "sucker"
          }
        },
        {
          "match": {
            "age": 13
          }
        }
      ]
    }
  }
}
```

![](https://img-blog.csdnimg.cn/9cd14bf0e3ad42cc89e424398c3fb494.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

should 命令，相当于or，符合一个条件都可以查询出  where id = 1 or name = xx

![](https://img-blog.csdnimg.cn/93ad778ecf794609826208f403d73778.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

must_not命令

![](https://img-blog.csdnimg.cn/5bd5aad6aa3048279363e554fc23401e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

过滤器filter

```java
GET sucker/user/_search
{
  "query":{
    "bool": {
      "must": [
        {
          "match": {
            "name": "sucker"
          }
        }
      ],
      "filter": [
        {
          "range": {
            "age": {
              "gt": 10
            }
          }
        }
      ]
    }
  }
}
```

![](https://img-blog.csdnimg.cn/8a73da51ca2d4095affa0da786852690.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- gt  大于
- gte  大于等于
- lt  小于
- lte  小于等于

![](https://img-blog.csdnimg.cn/27e42f4071034274baf3e5a0b57c840d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 匹配多个条件

```java
GET sucker/user/_search
{
  "query":{
    "match": {
      "tags": "男 技术"
    }
  }
}
```

![](https://img-blog.csdnimg.cn/50be7ec308b34538b9c6a28acfc07d87.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 精确查询！

term 查询是直接通过倒排索引指定的词条进行精确查找的！

**关于分词：**

term，直接查询精确的

match，会使用分词器解析！（先分析文档，然后再通过分析的文档进行查询！）

**两个类型：text  keyword**

```java
PUT testdb
{
  "mappings": {
    "properties": {
      "name" :{
        "type": "text"
      },
      "desc" :{
        "type": "keyword"
      }
    }
  }
}

PUT testdb/_doc/1
{
  "name" : "Sucker说Java name",
  "desc" : "Sucker说Java desc"
}

PUT testdb/_doc/2
{
  "name" : "Sucker说Java name",
  "desc" : "Sucker说Java desc2"
}
```

![](https://img-blog.csdnimg.cn/bde6c66b77dd422eaaa6ce23f3ad40ce.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/b03cfea204fa485e9c3802667ca279e5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/fb57879a7ecf46558ec0631d0377f0d8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

可以看到，当查询狂神说Java desc时，狂神说Java desc2不会被查询出来，因为其类型是keyword的，不会被分词器解析

### 多个值匹配精确查询

```java
PUT testdb/_doc/3
{
  "t1": "22",
  "t2": "2020-4-6"
}

PUT testdb/_doc/4
{
  "t1": "33",
  "t2": "2020-4-7"
}

GET testdb/_search
{
  "query": {
    "bool": {
      "should": [
        {
          "term": {
            "t1": "22"
          }
        },
        {
          "term": {
            "t1": "33"
          }
        }
      ]
    }
  }
}
```

![](https://img-blog.csdnimg.cn/dc992fb42a1b497080fdfcd20e128d4e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 高亮查询

```java
GET sucker/user/_search
{
  "query": {
    "match": {
      "name": "sucker"
    }
  },
  "highlight" :{
    "fields": {
      "name": {}
    }
  }
}
```

![](https://img-blog.csdnimg.cn/30b8947c7d454580b752112bb7ee78a5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
GET sucker/user/_search
{
  "query": {
    "match": {
      "name": "sucker"
    }
  },
  "highlight" :{
    "pre_tags": "<p class='key' style='color:red'>",
    "post_tags": "</p>", 
    "fields": {
      "name": {}
    }
  }
}
```

![](https://img-blog.csdnimg.cn/8758d5ba433e499a8a35b9b0d231451a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

小结：这些其实MySQL也能做，只是MySQL效率较低！

- 匹配
- 按照条件匹配
- 精确匹配
- 区间范围匹配
- 匹配字段过滤
- 多条件查询
- 高亮查询

## 集成SpringBoot

### 找官方文档

![](https://img-blog.csdnimg.cn/5eaf94d19ed3449ab4c9ae4ac7f2adc9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/012587d1223c467f8efa329157c349d6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/02fd2622c22a45a5896b0c49349ca476.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

1. 找到原生依赖

   ```xml
   <repositories>
       <repository>
           <id>es-snapshots</id>
           <name>elasticsearch snapshot repo</name>
           <url>https://snapshots.elastic.co/maven/</url>
       </repository>
   </repositories>
   ```

2. 找对象

   ![](https://img-blog.csdnimg.cn/ee9c43431c2c45fc86ee820cad0c6d31.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

3. 分析这个类中的方法即可

   > 配置基本的项目

- 创建一个空项目，添加Module

  ![](https://img-blog.csdnimg.cn/5ecaf4caf263484d955e5d2d7480cd32.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- 配置环境

  ![](https://img-blog.csdnimg.cn/13f0667f747b4c0da0815216c264f0c2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  ![](https://img-blog.csdnimg.cn/1dc9b00cc70f4c3db705b7f2894c786e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  ![](https://img-blog.csdnimg.cn/206062212b3442e48ad22fb65c6037e7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

  ![](https://img-blog.csdnimg.cn/160717eed65d4b7ea9a36291d48c88c9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

**问题：一定要保证我们导入的依赖和我们使用的ES 版本一致！**

![](https://img-blog.csdnimg.cn/00509b605b9c425582bc8670280b01a2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```xml
<properties>
    <java.version>1.8</java.version>
    <!--自定义ES 版本依赖，保证与本地一致-->
    <elasticsearch.version>7.15.0</elasticsearch.version>
</properties>
```

![](https://img-blog.csdnimg.cn/c45cdff151b34f8c9baaac4874623e3c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

源码中提供的对象：

![](https://img-blog.csdnimg.cn/ae1f8a8b6dd5463ea55375c5373dd08e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 具体的API测试

配置类

![](https://img-blog.csdnimg.cn/1993823ba6f2460bb6b2c174ee17d834.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
@Configuration
public class ElasticSearchClientConfig {

    @Bean
    public RestHighLevelClient restHighLevelClient(){
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(
                        new HttpHost("localhost", 9200, "http")));
        return client;
    }

}
```

1. 创建索引

   ```java
   package com.sucker;
   
   import org.elasticsearch.client.RequestOptions;
   import org.elasticsearch.client.RestHighLevelClient;
   import org.elasticsearch.client.indices.CreateIndexRequest;
   import org.elasticsearch.client.indices.CreateIndexResponse;
   import org.junit.jupiter.api.Test;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.beans.factory.annotation.Qualifier;
   import org.springframework.boot.test.context.SpringBootTest;
   
   import java.io.IOException;
   
   @SpringBootTest
   class SuckerEsApiApplicationTests {
   
       //面向对象操作
       @Autowired
       @Qualifier("restHighLevelClient")
       private RestHighLevelClient client;
   
       // 测试索引的创建  Request  相当于PUT sucker_index
       @Test
       void testCreateIndex() throws IOException {
           //1.创建索引请求
           CreateIndexRequest request = new CreateIndexRequest("sucker_index");
           //2. 客户端执行请求  IndicesClient, 请求后获得相应
           CreateIndexResponse createIndexResponse =
                   client.indices().create(request, RequestOptions.DEFAULT);
           System.out.println(createIndexResponse);
   
       }
   
   }
   ```

   ![](https://img-blog.csdnimg.cn/b28e0441e319408f9f6290cef6c29181.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

2. 判断索引是否存在

3. 删除索引

4. 创建文档

   maven依赖

   ```xml
   <dependency>
       <groupId>com.alibaba</groupId>
       <artifactId>fastjson</artifactId>
       <version>1.2.62</version>
   </dependency>
   ```

5. CRUD文档

```java
package com.sucker;

import com.alibaba.fastjson.JSON;
import com.sucker.pojo.User;
import org.elasticsearch.action.admin.indices.delete.DeleteIndexRequest;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.delete.DeleteRequest;
import org.elasticsearch.action.delete.DeleteResponse;
import org.elasticsearch.action.get.GetRequest;
import org.elasticsearch.action.get.GetResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.index.IndexResponse;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.action.support.master.AcknowledgedResponse;
import org.elasticsearch.action.update.UpdateRequest;
import org.elasticsearch.action.update.UpdateResponse;
import org.elasticsearch.client.Request;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.CreateIndexRequest;
import org.elasticsearch.client.indices.CreateIndexResponse;
import org.elasticsearch.client.indices.GetIndexRequest;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.core.TimeValue;
import org.elasticsearch.index.query.MatchAllQueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.index.query.TermQueryBuilder;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.fetch.subphase.FetchSourceContext;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.boot.test.context.SpringBootTest;

import java.io.IOException;
import java.util.ArrayList;
import java.util.concurrent.TimeUnit;

@SpringBootTest
class SuckerEsApiApplicationTests {

    //面向对象操作
    @Autowired
    @Qualifier("restHighLevelClient")
    private RestHighLevelClient client;

    // 测试索引的创建  Request  相当于PUT sucker_index
    @Test
    void testCreateIndex() throws IOException {
        //1.创建索引请求
        CreateIndexRequest request = new CreateIndexRequest("sucker_index");
        //2. 客户端执行请求  IndicesClient, 请求后获得相应
        CreateIndexResponse createIndexResponse =
                client.indices().create(request, RequestOptions.DEFAULT);
        System.out.println(createIndexResponse);

    }

    // 测试获取索引,判断其是否存在
    @Test
    void testExistIndex() throws IOException {
        GetIndexRequest request = new GetIndexRequest("sucker_index");
        boolean exists = client.indices().exists(request, RequestOptions.DEFAULT);
        System.out.println(exists);
    }

    // 测试删除索引
    @Test
    void testDeleteIndex() throws IOException {
        DeleteIndexRequest request = new DeleteIndexRequest("sucker_index");
        AcknowledgedResponse delete = client.indices().delete(request, RequestOptions.DEFAULT);
        System.out.println(delete.isAcknowledged());
    }

    // 测试添加文档
    @Test
    void testAddDocument() throws IOException {
        //创建对象
        User user = new User("Sucker",3);
        //创建请求
        IndexRequest request = new IndexRequest("sucker_index");

        //规则  put /sucker_index/_doc/1
        request.id("1");
        request.timeout(TimeValue.timeValueSeconds(1));
        //request.timeout("1s");

        // 将我们的数据放入请求  json
        request.source(JSON.toJSONString(user), XContentType.JSON);//发送出去即可

        // 客户端发送请求
        IndexResponse indexResponse = client.index(request, RequestOptions.DEFAULT);
        System.out.println(indexResponse.toString());
        System.out.println(indexResponse.status()); //对应我们命令返回的状态

    }

    // 获取文档，判断是否存在  GET sucker_index/_doc/1
    @Test
    void testIsExists() throws IOException {
        GetRequest getRequest = new GetRequest("sucker_index", "1");
        // 不获取返回的_source 的上下文 这里两个可以不写
        getRequest.fetchSourceContext(new FetchSourceContext(false));
        getRequest.storedFields("_none_");

        boolean exists = client.exists(getRequest, RequestOptions.DEFAULT);
        System.out.println(exists);
    }

    // 获取文档的信息
    @Test
    void testGetDocument() throws IOException {
        GetRequest getRequest = new GetRequest("sucker_index", "1");
        GetResponse getResponse = client.get(getRequest, RequestOptions.DEFAULT);
        System.out.println(getResponse.getSourceAsString());//打印文档的内容
        System.out.println(getResponse);  //返回的全部内容，和命令一样
    }

    // 更新文档的信息
    @Test
    void testUpdateDocument() throws IOException {
        UpdateRequest updateRequest = new UpdateRequest("sucker_index","1");
        updateRequest.timeout("1s");

        User user = new User("Sucker说Java", 18);
        updateRequest.doc(JSON.toJSONString(user),XContentType.JSON);

        UpdateResponse updateResponse = client.update(updateRequest, RequestOptions.DEFAULT);
        System.out.println(updateResponse);
    }

    // 删除文档的记录
    @Test
    void testDeleteDocument() throws IOException {
        DeleteRequest deleteRequest = new DeleteRequest("sucker_index","1");
        deleteRequest.timeout("1s");

        DeleteResponse deleteResponse = client.delete(deleteRequest, RequestOptions.DEFAULT);
        System.out.println(deleteResponse);
    }

    // 特殊的，真实的项目一般会批量插入数据！
    @Test
    void testBulkRequest() throws IOException {
        BulkRequest bulkRequest = new BulkRequest();
        bulkRequest.timeout("10s");

        ArrayList<User> userList = new ArrayList<>();
        userList.add(new User("sucker1",3));
        userList.add(new User("sucker2",3));
        userList.add(new User("sucker3",3));
        userList.add(new User("baga1",3));
        userList.add(new User("baga1",3));
        userList.add(new User("baga1",3));
        userList.add(new User("baga1",3));
        userList.add(new User("baga1",3));

        // 批处理请求
        for (int i = 0; i < userList.size(); i++) {
            // 批量更新和批量删除，就在这里修改对应的请求即可
            bulkRequest.add(
                    new IndexRequest("sucker_index")
                    .id(""+(i+1))//可以不设置ID，会自动生成随机不重复ID
                    .source(JSON.toJSONString(userList.get(i)),XContentType.JSON));
        }

        BulkResponse bulkResponse = client.bulk(bulkRequest, RequestOptions.DEFAULT);
        System.out.println(bulkResponse.hasFailures()); //是否失败
    }

    //查询
    // SearchRequset  搜索请求
    // SearchSourceBuilder  条件构造
    // HighLightBuilder  构建高亮
    // TermQueryBuilder  精确查询
    // MatchAllQueryBuilder
    // xxx  QueryBuilder 对应我们刚才看到的命令

    @Test
    void testSearch() throws IOException {
        SearchRequest searchRequest = new SearchRequest("sucker_index");//正式项目中应该是用常量
        //构建搜索条件
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        //查询条件，我们可以使用  QueryBuilders 工具来实现
        // 精确匹配  QueryBuilders.termQuery()
//         查询所有  QueryBuilders.matchAllQuery()
//        MatchAllQueryBuilder matchAllQueryBuilder = QueryBuilders.matchAllQuery();
        TermQueryBuilder termQueryBuilder = QueryBuilders.termQuery("name", "baga1");
        sourceBuilder.query(termQueryBuilder);
//        sourceBuilder.from();  分页，不写也有默认参数，点进去可以看到默认值
//        sourceBuilder.size();
        sourceBuilder.timeout(new TimeValue(60, TimeUnit.SECONDS));

        searchRequest.source(sourceBuilder);

        SearchResponse searchResponse = client.search(searchRequest, RequestOptions.DEFAULT);
        System.out.println(JSON.toJSONString(searchResponse.getHits()));
        for (SearchHit hit : searchResponse.getHits().getHits()) {
            System.out.println(hit.getSourceAsMap());
        }

    }

}
```



## 实战

### 环境搭建

![](https://img-blog.csdnimg.cn/92f596d2ec3c4a60a20d2f4c113fa8e0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/af5d6e75d28642cbadd4504ef3aa7c8c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

resoucres目录下的application.properties中配置

```properties
server.port=8080
# 关闭 thymeleaf的缓存
spring.thymeleaf.cache=false
```

### 爬虫

> 数据问题？数据库获取，消息队列中获取，都可以成为数据源

爬取数据：（获取请求的页面信息，筛选出我们想要的数据即可！）

jsoup包

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.13.1</version>
</dependency>
```

1. 上JD进行搜索java 复制链接https://search.jd.com/Search?keyword=java&enc=utf-8

![](https://img-blog.csdnimg.cn/53f4ac85297d4ef09fda52fc24afda29.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

每本书下个信息

![](https://img-blog.csdnimg.cn/53f4ac85297d4ef09fda52fc24afda29.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

2. 导入jsoup依赖

3. 创建utils包并建立HtmlParseUtil.java爬取测试

   ```java
   package com.sucker.utils;
   
   import com.sucker.pojo.Content;
   import org.jsoup.Jsoup;
   import org.jsoup.nodes.Document;
   import org.jsoup.nodes.Element;
   import org.jsoup.select.Elements;
   import org.springframework.stereotype.Component;
   
   import java.io.IOException;
   import java.net.MalformedURLException;
   import java.net.URL;
   import java.util.ArrayList;
   import java.util.List;
   
   @Component
   public class HtmlParseUtil {
       public static void main(String[] args) throws Exception {
           new HtmlParseUtil().parseJD("心理学").forEach(System.out::println);
       }
   
       public List<Content> parseJD(String keywords) throws Exception {
           // 获取请求：https://search.jd.com/Search?keyword=java
           //前提需要联网，不能获取到 ajax，除非模拟浏览器
           String url = "https://search.jd.com/Search?keyword="+keywords;
           // 解析网页 (Jsoup 返回的Document就是浏览器Document对象（js页面对象）)
           Document document = Jsoup.parse(new URL(url), 30000);
           // 所有你在js中可以使用的方法，这里都能用！
           Element elements = document.getElementById("J_goodsList");
           //System.out.println(elements.html());
           // 获取所有的 li 元素
           Elements elements_li = elements.getElementsByTag("li");
           // 获取元素中的内容，这里的element 就是没一个li标签了！
   
           ArrayList<Content> goodsList = new ArrayList<>();
   
           for (Element element : elements_li) {
               if(element.attr("class").equalsIgnoreCase("gl-item")){
                   //eq(0)表示获取第一个，attr表示获取的属性
                   String img = element.getElementsByTag("img").eq(0).attr("data-lazy-img");
                   String price = element.getElementsByClass("p-price").eq(0).text();
                   String title = element.getElementsByClass("p-name").eq(0).text();
   
                   Content content = new Content();
                   content.setImg(img);
                   content.setTitle(title);
                   content.setPrice(price);
                   goodsList.add(content);
               }
           }
           return goodsList;
       }
   
   }
   ```

4. 测试结果

   ```xml
   D:\JavaJDK\bin\java.exe "-javaagent:D:\IDEA\IntelliJ IDEA 202rg\apache\logging\log4j\log4j-to-slf4j\2.14.1\log4j-to-slf4j-
   Content(title=蛤蟆先生去看心理医生（年销200万册！英国经典心理咨询入门书，知名心理学家李松蔚强烈推荐） 入围《新京报》、豆瓣2020年度图书榜单；英国亚马逊五星评分、授权10个语言版本，自1997年起长销至今。童话版《自卑与超越》，将心理学知识巧妙融入故事情节　团购电话4006186622, img=//img13.360buyimg.com/n1/s200x200_jfs/t1/187326/14/21041/162870/612c6f9bE7e7a7c82/66803595b28e2b94.jpg, price=￥26.00)
   Content(title=正版全12册心理学书籍 乌合之众鬼谷子微表情心理学读心术九型人格自控力心理学与生活大众心理学入门书籍 新品上架畅销全6册心理学书籍点击购买, img=//img10.360buyimg.com/n1/s200x200_jfs/t1/182444/21/20631/624224/612062d8Eb9519961/35b55ac53adaca9b.png, price=￥52.80)
   Content(title=自卑与超越（完整全译本 心理启蒙书） 与《乌合之众》齐名！抖音100万点赞，销量破百万册！阿德勒、弗洛伊德、荣格并称20世纪三大心理学家！　团购电话4006186622, img=//img11.360buyimg.com/n1/s200x200_jfs/t1/154117/33/18182/181877/602e11e2E3ac470f8/bc09c9746fc2e6a2.jpg, price=￥35.40)
   Content(title=行为心理学1+2+3(套装全3册） 团购电话4006186622, img=//img12.360buyimg.com/n1/s200x200_jfs/t1/85964/8/9435/205220/5e0d9280E1a371d41/007d5e31c774b3c6.jpg, price=￥102.40 ￥100.00)
   Content(title=墨菲定律（百万畅销精装纪念版 为你解读生活表象背后的心理学百科） 大众心理学必读经典图书　团购电话4006186622, img=//img10.360buyimg.com/n1/s200x200_jfs/t1/195680/40/17181/126443/610cf892E8a3dead6/af4010ca2ef170cd.jpg, price=￥35.00 ￥34.30)
   Content(title=乌合之众：群体心理研究（ 附赠思维导图） 社会心理学领域扛鼎之作，一部讲透政治、经济、管理的心理学巨著，入选改变世界的20本书。　团购电话4006186622, img=//img11.360buyimg.com/n1/s200x200_jfs/t1/163319/24/4469/137886/6012745aE45b0f74a/d37a1f68cfe3e377.jpg, price=￥35.40)
   Content(title=儿童创造力发展心理/儿童青少年心理学丛书, img=//img13.360buyimg.com/n1/s200x200_jfs/t1/179517/4/16526/101300/61018472E3a3164b8/7764abaff2f17642.jpg, price=￥27.08)
   Content(title=情绪免疫：真正成熟的人，都懂得情绪免疫 樊登书会、武志红公号、张德芬空间热议话题！学会拒绝、敢于示弱、保持幽默、情绪稳定……读者亲测有效的31个情绪免疫法，轻松解重压之下焦虑、迷茫、抑郁等“都市病”！　团购电话4006186622, img=//img12.360buyimg.com/n1/s200x200_jfs/t1/123582/7/4506/96139/5ee19280Ee93fbeba/369a42482140ebba.jpg, price=￥30.00)
   Content(title=社会心理学（第11版 中文平装版） 曾被翻译成12种语言，全球有800多万人用它来学习社会心理学，中文版曾重印42次，销量逾40万，津巴多和彭凯平联袂推荐！, img=//img12.360buyimg.com/n1/s200x200_jfs/t6037/142/729241766/490719/78a3a9bf/592bf16dN50326aad.jpg, price=￥82.80)
   Content(title=自卑与超越（未删节译本） [What Life Could Means to You] 未删节译本，读个体心理学经典，你比你想象的更优秀！　团购电话4006186622, img=//img13.360buyimg.com/n1/s200x200_jfs/t1/136788/30/5537/432480/5f1fea26Ed3267c61/59f262cbdb5a6eae.jpg, price=￥32.00)
   Content(title=认知心理学 心理学基础入门教材书籍，了解人类社会思维心理学与生活分支，影响决策与判断，北大魏坤琳、北师大心理学教授彭华茂推荐，感知注意力记忆语言推理情绪等认知思维科学　团购电话4006186622, img=//img11.360buyimg.com/n1/s200x200_jfs/t1/134917/16/11222/164400/5f72b3bcEfcde3a1b/6f8bd7278630fa1a.jpg, price=￥128.00)
   Content(title=犯罪心理学（现代犯罪心理学理论奠基之作） 现代犯罪心理学之父汉斯·格罗斯传世经典。现代犯罪心理学理论奠基之作。先后被译成8种文字，二十余个版本。　团购电话4006186622, img=//img11.360buyimg.com/n1/s200x200_jfs/t1/51639/27/1289/214201/5cf09be9E4009804e/75c6c93d363badea.jpg, price=￥59.00)
   Content(title=心理学大全书籍 情绪管理 心理百科 读心术行为销售生活教育人际交往微表情入门基础, img=//img10.360buyimg.com/n1/s200x200_jfs/t1/189672/21/11790/188969/60e54717Eb4eb9d60/de8e916a4734bc64.jpg, price=￥68.00)
   Content(title=《也许你该找个人聊聊》继《蛤蟆先生去看心理医生》之后，又一个关于心理咨询的动人故事 团购电话4006186622, img=//img13.360buyimg.com/n1/s200x200_jfs/t1/191932/17/14239/372509/60f79f13Eb7d25d8b/30b41b6f4f47ebfd.jpg, price=￥44.40)
   Content(title=心理学入门：简单有趣的99个心理学常识 中国纺织出版社有限公司荣誉出版　团购电话4006186622, img=//img12.360buyimg.com/n1/s200x200_jfs/t17098/102/454258189/377467/1b212df7/5a7d0e0eN5f6beea4.jpg, price=￥32.70)
   Content(title=心理学与生活（第19版） 跨越半个多世纪的心理学入门经典，菲利普·津巴多扛鼎之作，第19版中文平装版重磅上市　团购电话4006186622, img=//img14.360buyimg.com/n1/s200x200_jfs/t1/94931/14/12574/311815/5e4b5182E27142c7c/82db72380eedad9a.jpg, price=￥82.80)
   Content(title=内在疗愈（为什么劝自己总比劝别人难） 解读紧张、焦虑、恐惧、抑郁等那些谁都逃不掉的心理问题，由内向外梳理自己，获得自在从容。单品100册以上可致电4006186622, img=//img12.360buyimg.com/n1/s200x200_jfs/t1/88080/7/18028/215872/5e8ea8c0Ed0e7ee91/a40991b8078aa40f.jpg, price=￥25.80)
   Content(title=非暴力沟通 当我们褪去隐蔽的精神暴力，爱将自然流露。该书入选香港大学推荐的50本荐读书籍。　团购电话4006186622, img=//img10.360buyimg.com/n1/s200x200_jfs/t24832/116/985818987/184821/cbf8b009/5b84b02fNa96ea7b7.jpg, price=￥30.40)
   Content(title=正版全4册 中国式应酬+中国式饭局读心术+中国式饭局人脉学+中国式酒局应酬学 应酬交际推荐书籍, img=//img14.360buyimg.com/n1/s200x200_jfs/t1/189585/7/20590/218800/612b2d5cE5474ccb9/6110a36e2693b007.jpg, price=￥65.80)
   Content(title=心理抚养(签章版) 儿童教育专家李玫瑾继《幽微的人性》后新作 心理抚养比物质抚养更重要 心理抚养比物质抚养更重要性格比能力更决定命运父母亲自陪伴孩子成长比只给孩子挣钱更有价值　团购电话4006186622, img=//img13.360buyimg.com/n1/s200x200_jfs/t1/173359/9/12395/96595/60b58afeEb1fc25f6/09a7abc94552f14b.jpg, price=￥44.00)
   Content(title=动机心理学 解读行为逻辑入门书籍，提升成功率和工作效率，时间精力目标管理，掌握生活中说话沟通人际交往，积极认知人格情绪潜意识分析。　团购电话4006186622, img=//img11.360buyimg.com/n1/s200x200_jfs/t1/87847/11/16319/187513/5e7af008Ebf083d35/7cd59d365fac777d.jpg, price=￥98.00)
   Content(title=经典心理学套装：自卑与超越+乌合之众+人性的弱点+人性的优点（套装共4册） 两种封面随机发货。职场必读，处世必备！足本典藏版，抖音150万点赞!　团购电话4006186622, img=//img10.360buyimg.com/n1/s200x200_jfs/t1/14449/4/6727/156030/5c637595Ee34c27c7/bdd4009cfc8d9cb2.jpg, price=￥159.20)
   Content(title=自卑与超越+蛤蟆先生去看心理医生（2本套） 100册以上团购优惠联系电话4006186622, img=//img12.360buyimg.com/n1/s200x200_jfs/t1/163159/32/14451/109547/605c0593E9b449b4f/407a1d2662780a7a.jpg, price=￥70.00)
   Content(title=世界尽头的咖啡馆 心理自助经典，通透生活指南。读完后辞职率超高的一本奇书。被翻译成39种语言　团购电话4006186622, img=//img14.360buyimg.com/n1/s200x200_jfs/t1/174744/27/20492/300379/60fa6eeaE7abad544/cc91dbe49caec718.jpg, price=￥29.90)
   Content(title=心理抚养 儿童教育专家李玫瑾继《幽微的人性》后新作 全2册 心理抚养 +幽微的人性, img=//img13.360buyimg.com/n1/s200x200_jfs/t1/63641/35/16993/171204/613c4e52E695f2d4e/3421aa785a630e1f.jpg, price=￥44.80)
   Content(title=心理学书籍5册读心术+九型人格+微表情心理学墨菲定律正版读心术人际交往心理学与生活社会行为说话心里学 精品好书，正版保证，等您选购，关注店铺领优惠券。书架上的颜值担当：精品绸缎面插盒书, img=//img14.360buyimg.com/n1/s200x200_jfs/t1/118474/28/19570/110670/5f7d1ee2Eeadbf2b6/0df915e938c26960.jpg, price=￥19.80)
   Content(title=自控力：斯坦福大学广受欢迎的心理学课程 只需10周，成功掌握自己的时间和生活！拿回人生主导权！　团购电话4006186622, img=//img14.360buyimg.com/n1/s200x200_jfs/t1/158366/12/12368/50694/60498bbeEe3dea818/19d88c9b93e8bdae.jpg, price=￥37.90)
   Content(title=焦虑症的自救系列 套装全3册 焦虑症患者社群力荐读物！现代焦虑症治疗的先驱克莱尔·威克斯经典代表作，英国、美国、加拿大、澳大利亚等国精神科医生、心理治疗师、全科医生推荐阅读！　团购电话4006186622, img=//img12.360buyimg.com/n1/s200x200_jfs/t1/140845/16/17662/259851/5fcf1d0fEaeec0650/2aef65198291f389.jpg, price=￥157.20)
   Content(title=李玫瑾 幽微的人性+心理抚养（共二册） 李玫瑾，著名犯罪心理学家，中国关心下一代工作委员会委员，中国预防青少年犯罪研究会副会长　团购电话4006186622, img=//img10.360buyimg.com/n1/s200x200_jfs/t1/128779/15/19622/101862/60b6da6eEb3e08635/a9e85a2684761eb3.jpg, price=￥81.50)
   Content(title=正版全2册 做自己的心理医生+静心 自我疗愈情感医生恰如其分的自尊态度改变与社会影响正能量心理学书籍 正版现货品质保证, img=//img13.360buyimg.com/n1/s200x200_jfs/t1/168916/18/12964/121483/60507486Ef255a90c/44fa11b41661514f.jpg, price=￥38.80)
   
   Process finished with exit code 0
   
   ```

   获取结果没有问题后,将此方法封装为一个工具类使用

5. 创建pojo实体类

   ```java
   package com.sucker.pojo;
   
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   
   @Data
   @NoArgsConstructor
   @AllArgsConstructor
   public class Content {
       private String title;
       private String img;
       private String price;
       //可以自己添加属性
   }
   ```

6. 编写业务层代码 (这里就不写接口了)

   ContentService.java

   首先完成一个方法让爬取的数据存入ES中

   ```java
   // 业务编写
   @Service
   public class ContentService {
   
       @Autowired  //不能直接使用@Autowired 因为需要Spring容器
       private RestHighLevelClient restHighLevelClient;
   
       public static void main(String[] args) throws Exception {
           new ContentService().parseContent("java");
       }
   
       public Boolean parseContent(String keyword) throws Exception {
           List<Content> contents = new HtmlParseUtil().parseJD(keyword);
           // 把查询到的数据放入es中
           BulkRequest bulkRequest = new BulkRequest();
           bulkRequest.timeout("2m");
   
           for (int i = 0; i < contents.size(); i++) {
               bulkRequest.add(new IndexRequest("jd_goods")
               .source(JSON.toJSONString(contents.get(i)), XContentType.JSON));
           }
   
           BulkResponse bulk = restHighLevelClient.bulk(bulkRequest, RequestOptions.DEFAULT);
           return !bulk.hasFailures();
   
       }
   }
   ```

7. 在Controller包下建立

   ContentController.java

   ```java
   @RestController
   public class ContentController {
   
       @Autowired
       private ContentService contentService;
   
       @GetMapping("/parse/{keyword}")
       public Boolean parse(@PathVariable("keyword") String keyword) throws Exception {
           return contentService.parseContent(keyword);
       }
   }
   ```

8. 启动Springboot项目,访问是否能将数据爬取至ES

   ![](https://img-blog.csdnimg.cn/9ac6c546b10543e39bf1b0138d2e7d04.png)

   ![](https://img-blog.csdnimg.cn/0ee71a7d8418496b8d60393469822e11.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 实现搜索功能

1. 在ContentService.java中添加

   ```java
   //2. 获取这些数据实现搜索功能
   public List<Map<String ,Object>> searchPage(String keyword,int pageNo,int pageSize) throws IOException {
       if(pageNo<=1) pageNo = 1;
   
       // 条件搜索
       SearchRequest searchRequest = new SearchRequest("jd_goods");
       SearchSourceBuilder searchSourceBuilder = new SearchSourceBuilder();
   
       // 分页
       searchSourceBuilder.from(pageNo);
       searchSourceBuilder.size(pageSize);
   
       //精确匹配
       TermQueryBuilder termQueryBuilder = QueryBuilders.termQuery("title", keyword);
       searchSourceBuilder.query(termQueryBuilder);
       searchSourceBuilder.timeout(new TimeValue(60, TimeUnit.SECONDS));
   
       //执行搜索
       searchRequest.source(searchSourceBuilder);
       SearchResponse searchResponse = restHighLevelClient.search(searchRequest, RequestOptions.DEFAULT);
       // 解析结果
       ArrayList<Map<String, Object>> list = new ArrayList<>();
       for (SearchHit hit : searchResponse.getHits().getHits()) {
           list.add(hit.getSourceAsMap());
       }
       return list;
   }
   ```

2. 在ContentController.java中添加搜索请求,使用RestFul风格

   ```java
   @GetMapping("/search/{keyword}/{pageNo}/{pageSize}")
   public List<Map<String ,Object>> search(@PathVariable("keyword") String keyword,
                                           @PathVariable("pageNo")int pageNo,
                                           @PathVariable("pageSize")int pageSize) throws IOException {
       return contentService.searchPage(keyword,pageNo,pageSize);
   }
   ```

3. 访问访问http://127.0.0.1:8080/search/java/1/10 (查询Java 并从第一条显示到第十条)

   成功显示数据

   到此数据的爬取和搜索都没有问题了,下面就要开始前后端的分离工作了



### 前后端分离

1. 下载vue与axios环境，新建文件夹在environment中，cmd下首先初始化npm

   ```xml
   npm init
   初始化后清空界面 cls
   npm install vue
   npm install axios
   ```

   ![](https://img-blog.csdnimg.cn/d989cbfabcc64ef494a5d57dd1b28b89.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/img_convert/0c4d88be05fc2ef84b6d0888383651ea.png)

前端需要接受数据

用vue接受数据

![](https://img-blog.csdnimg.cn/img_convert/b549c688b0449ab4a18f2ea729916ebb.png)

```js
<!--前端使用vue完成前后端分离-->
<script th:src="@{/js/axios.min.js}"></script>
<script th:src="@{/js/vue.min.js}"></script>

<script>
    new Vue({
        el: '#app',
        data: {
            keyword: '',  //搜索的关键字
            result: []  //搜索的结果
        },
        methods: {
            searchKey() {
                var keyword = this.keyword
                axios.get('search/' + keyword + '/1/210').then(response => {
                    //console.log(response);
                    this.result = response.data;//绑定数据！
                })
            }
        }
    })
</script>
```

然后为按钮绑定点击事件

![](https://img-blog.csdnimg.cn/img_convert/41a6297f8f647dde2311da45ceff07bc.png)

用vue给前端传递数据

![](https://img-blog.csdnimg.cn/img_convert/65f335b61aa466f9c6f0a5f348f04926.png)

访问127.0.0.1:8080 搜索java进行尝试

![](https://img-blog.csdnimg.cn/img_convert/b425899087cc79eecb2d2c7f3a229a62.png)

由此 基本功能实现完成

### 搜索高亮实现

1. 修改`ContentService.java`中的搜索功能

   ```java
       //3. 获取这些数据实现搜索高亮功能
       public List<Map<String ,Object>> HighlightSearch(String keyword,int pageNo,int pageSize) throws IOException {
           if(pageNo<=1) pageNo = 1;
   
           // 条件搜索
           SearchRequest searchRequest = new SearchRequest("jd_goods");
           SearchSourceBuilder searchSourceBuilder = new SearchSourceBuilder();
   
           // 分页
           searchSourceBuilder.from(pageNo);
           searchSourceBuilder.size(pageSize);
   
           //精确匹配
           TermQueryBuilder termQueryBuilder = QueryBuilders.termQuery("title", keyword);
           searchSourceBuilder.query(termQueryBuilder);
           searchSourceBuilder.timeout(new TimeValue(60, TimeUnit.SECONDS));
   
           // 高亮
           HighlightBuilder highlightBuilder = new HighlightBuilder();
           highlightBuilder.field("title");
           highlightBuilder.preTags("<span style='color:red'>");
           highlightBuilder.postTags("</span>");
           highlightBuilder.requireFieldMatch(false);//关闭多个高亮，避免一句话中同样关键词多次高亮
           searchSourceBuilder.highlighter(highlightBuilder);
   
           //执行搜索
           searchRequest.source(searchSourceBuilder);
           SearchResponse searchResponse = restHighLevelClient.search(searchRequest, RequestOptions.DEFAULT);
           // 解析结果
           ArrayList<Map<String, Object>> list = new ArrayList<>();
           for (SearchHit hit : searchResponse.getHits().getHits()) {
               Map<String, HighlightField> highlightFields = hit.getHighlightFields();
               HighlightField title = highlightFields.get("title");
               Map<String, Object> sourceAsMap = hit.getSourceAsMap();//原来的结果
               //解析高亮的字段 , 将原来的字段更换为高亮的字段即可！
               if(title!=null){
                   Text[] fragments = title.fragments();//取出高亮字段
                   String new_title = "";
                   for (Text fragment : fragments) {
                       new_title+=fragment;
                   }
                   sourceAsMap.put("title",new_title);// 高亮字段替换原来的内容
               }
               list.add(sourceAsMap);
           }
           return list;
       }
   ```

2. 改变Controller中的搜索请求后进行尝试

   ```java
   @GetMapping("/search/{keyword}/{pageNo}/{pageSize}")
   public List<Map<String ,Object>> search(@PathVariable("keyword") String keyword,
                                           @PathVariable("pageNo")int pageNo,
                                           @PathVariable("pageSize")int pageSize) throws IOException {
       return contentService.HighlightSearch(keyword,pageNo,pageSize);
   }
   ```

3. 解决问题

   Vue给了很好的解决办法

   ![](https://img-blog.csdnimg.cn/img_convert/66d014b80db58e1871184015f2de6d56.png)

