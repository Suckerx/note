## Mybatis

环境：

- JDK 1.8
- Mysql 5.7
- maven 3.6.1
- IDEA

回顾：

- JDBC
- Mysql
- Java基础
- Maven
- Junit

参考官方文档：[mybatis – MyBatis 3 | 简介](https://mybatis.org/mybatis-3/zh/index.html)

## 简介

### 什么是 MyBatis？

- MyBatis 是一款优秀的**持久层框架**
- 它支持自定义 SQL、存储过程以及高级映射。
- MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。
- MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

### 获得Mybatis

- Maven仓库

  ```xml
  <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
  <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.7</version>
  </dependency>
  ```

- Github：[Releases · mybatis/mybatis-3 · GitHub](https://github.com/mybatis/mybatis-3/releases)

- 中文文档：[mybatis – MyBatis 3 | 简介](https://mybatis.org/mybatis-3/zh/index.html)

### 持久化

数据持久化

- 持久化就是将程序的数据在持久状态和瞬时状态转化的过程

- 内存：**断电即失**
- 数据库(JDBC)、io文件持久化

### 持久层

Dao层，Service层，Controller层...

- 完成持久化工作的代码块
- 层界限十分明显

### 为什么需要Mybatis

- 帮助程序员将数据存入数据库中
- 方便
- 传统JDBC代码太复杂。简化，框架，自动化
- 不用Mybatis也可以。更容易上手。
- 优点：
  - 简单易学
  - 灵活
  - sql和代码分离，提高了可维护性
  - 提供映射标签，支持对象与数据库的orm字段关系映射
  - 提供对象关系映射标签，支持对象关系组建维护
  - 提供xml标签，支持编写动态sql

## 第一个Mybatis程序

思路：搭建环境-->导入Mybatis-->编写代码-->测试！

### 搭建环境

搭建数据库

```sql
CREATE DATABASE `mybatis`;

USE `mybatis`;

CREATE TABLE `user`(
   `id` INT(20) NOT NULL,
   `name` VARCHAR(30) DEFAULT NULL,
   `pwd` VARCHAR(30) DEFAULT NULL,
   PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `user`(`id`,`name`,`pwd`) VALUES
(1,'狂神','123456'),
(2,'张三','123456'),
(3,'李四','122326')
```

新建项目

1. 新建一个普通Maven项目，注意设置

   ![](https://img-blog.csdnimg.cn/a34e7c4f5e634d0390cd25a19dafdcbc.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

2. 删除src目录

3. 导入Maven依赖

   ```xml
   <!--    导入依赖-->
       <dependencies>
   <!--        mysql驱动-->
           <dependency>
               <groupId>mysql</groupId>
               <artifactId>mysql-connector-java</artifactId>
               <version>5.1.47</version>
           </dependency>
   <!--        mybatis-->
           <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
           <dependency>
               <groupId>org.mybatis</groupId>
               <artifactId>mybatis</artifactId>
               <version>3.5.7</version>
           </dependency>
   <!--        junit-->
           <dependency>
               <groupId>junit</groupId>
               <artifactId>junit</artifactId>
               <version>4.13</version>
           </dependency>
   
       </dependencies>
   ```

### 创建一个模块

- New Module-->普通Maven项目

- 若没有父模块需手动加入

```xml
<parent>
    <artifactId>Mybatis-Study</artifactId>
    <groupId>com.Sucker</groupId>
    <version>1.0-SNAPSHOT</version>
</parent>
```

- 编写Mybatis的核心配置文件

  - 在resource目录下新建 mybatis-config.xml 文件

    ```xml
    官方文档：
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE configuration
      PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
      "http://mybatis.org/dtd/mybatis-3-config.dtd">
    <configuration>
      <environments default="development">
        <environment id="development">
          <transactionManager type="JDBC"/>
          <dataSource type="POOLED">
            <property name="driver" value="${driver}"/>
            <property name="url" value="${url}"/>
            <property name="username" value="${username}"/>
            <property name="password" value="${password}"/>
          </dataSource>
        </environment>
      </environments>
      <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
      </mappers>
    </configuration>
    ```

    自主配置，注意连接数据库

    ```xml
    自主配置后：
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE configuration
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-config.dtd">
    <!--configuration核心配置文件-->
    <configuration>
        <environments default="development">
            <environment id="development">
                <transactionManager type="JDBC"/>
                <dataSource type="POOLED">
                    <property name="driver" value="com.mysql.jdbc.Driver"/>
                    <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                    <property name="username" value="root"/>
                    <property name="password" value="123456"/>
                </dataSource>
            </environment>
        </environments>
    
    </configuration>
    ```

- 编写Mybatis工具类（java-->com.Sucker.utils.MybatisUtils）

  ```java
  package com.Sucker.utils;
  //sqlSessionFactory --> sqlSession
  public class MybatisUtils {
  
      private static SqlSessionFactory sqlSessionFactory;
  
      static {
          try {
              //使用Mybatis第一步：获取sqlSessionFactory对象
              String resource = "mybatis-config.xml";
              InputStream inputStream = Resources.getResourceAsStream(resource);
              sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  
      //既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。
      // SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。
      // 你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句
  
      public static SqlSession getSqlSession(){
          return sqlSessionFactory.openSession();//得到能执行sql的对象
      }
  
  }
  ```

### 编写代码

- 实体类

  ```java
  package com.Suckerr.pojo;
  //实体类
  public class User {
  
      private int id;
      private String name;
      private String pwd;
  
      public User() {
      }
  
      public User(int id, String name, String pwd) {
          this.id = id;
          this.name = name;
          this.pwd = pwd;
      }
  
      public int getId() {
          return id;
      }
  
      public void setId(int id) {
          this.id = id;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public String getPwd() {
          return pwd;
      }
  
      public void setPwd(String pwd) {
          this.pwd = pwd;
      }
  
      @Override
      public String toString() {
          return "User{" +
                  "id=" + id +
                  ", name='" + name + '\'' +
                  ", pwd='" + pwd + '\'' +
                  '}';
      }
  }
  ```

- Dao接口

  ```java
  package com.Sucker.dao;
  ```

  ```java
  public interface UserDao {
      List<User> getUserList();
  }
  ```

- 接口实现类由原来的UserDaoImpl转变为一个Mapper配置文件

  ```java
  package com.Sucker.dao; //这个目录下新建UserMapper.xml
  ```

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!--namespace=绑定一个对应的Dao接口-->
  <mapper namespace="com.Sucker.dao.UserDao">
      <select id="getUserList" resultType="com.Sucker.pojo.User"> <!--id是方法名，resultType是返回类型-->
          select * from mybatis.user
      </select>
  </mapper>
  ```

### 测试

注意点：

org.apache.ibatis.binding.BindingException: Type interface com.Sucker.dao.UserDao is not known to the MapperRegistry.  表示没有注册Mapper

解决方法：在resources中的mybatis-config.xml中在注册

```xml
<!--    每一个Mapper.xml都需要在Mybatis核心配置文件中注册！-->
    <mappers>
        <mapper resource="com/Sucker/dao/UserMapper.xml"/>
    </mappers>
```

注意配置问题，由于maven的原因，需要设置导出过滤

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

- Junit测试

  在test目录下，新建com.Sucker.dao.UserDaoTest（测试代码放在test目录下）

  ```java
  public class UserDaoTest {
  
      @Test
      public void test(){
          //第一步：获得sqlSession对象
          SqlSession sqlSession = MybatisUtils.getSqlSession();
  
          //执行SQL
          //方式一：getMapper
          UserDao userDao = sqlSession.getMapper(UserDao.class);
          List<User> userList = userDao.getUserList();
  
          for (User user : userList) {
              System.out.println(user);
          }
  
          //关闭sqlSession
          sqlSession.close();
  
      }
  
  }
  ```

  方式二：Blog blog = (Blog) session.selectOne("org.mybatis.example.BlogMapper.selectBlog", 101);

  这种方式不推荐使用

**SqlSession**

每个线程都应该有它自己的 SqlSession 实例。SqlSession 的实例不是线程安全的，因此是不能被共享的，所以它的最佳的作用域是请求或方法作用域。换句话说，每次收到 HTTP 请求，就可以打开一个 SqlSession，返回一个响应后，就关闭它

## CRUD

### namespace

namespace中的包名要和 Dao / Mapper 接口中的包名一致

### select

选择，查询语句

- id：对应的namespace中的方法名；
- resultType：Sql语句执行的返回值类型
- parameterType：参数类型！

流程：

- 编写接口

  ```java
      //根据ID查询用户
      User getUserById(int id);
  ```

- 编写对应Mapper中的语句

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!--namespace=绑定一个对应的Dao接口-->
  <mapper namespace="com.Sucker.dao.UserMapper">
      
      <select id="getUserById" parameterType="int" resultType="com.Sucker.pojo.User">
          select * from mybatis.user where id = #{id}
      </select>
  
  </mapper>
  ```

- 测试

  ```java
  @Test
  public void getUserById(){
      SqlSession sqlSession = MybatisUtils.getSqlSession();
  
      UserMapper mapper = sqlSession.getMapper(UserMapper.class);
  
      User user = mapper.getUserById(1);
      System.out.println(user);
  
      sqlSession.close();
  }
  ```

### Insert

```xml
<!--    对象中的属性，可以直接取出来-->
    <insert id="addUser" parameterType="com.Sucker.pojo.User">
        insert into mybatis.user (id, name , pwd) values (#{id},#{name },#{pwd});
    </insert>
```

测试：

```java
    //增删改必须提交事务！
    @Test
    public void addUser(){

        SqlSession sqlSession = MybatisUtils.getSqlSession();

        UserMapper mapper = sqlSession.getMapper(UserMapper.class);

        mapper.addUser(new User(4,"哈哈","123333"));

        //提交事务
        sqlSession.commit();
        sqlSession.close();

    }
```

### Update

```xml
<update id="updateUser" parameterType="com.Sucker.pojo.User">
    update mybatis.user
    set name = #{name},pwd=#{pwd}
    where id=#{id};
</update>
```

### Delete

```xml
<delete id="deleteUser" parameterType="int">
    delete from mybatis.user where id=#{id}
</delete>
```

注意点：增删改需要提交事务

### 分析错误

- 标签名出错
- mybatis配置文件中resource 绑定mapper，需要使用路径 用 / 
- 配置文件必须符合规范

### Map

假设实体类，或者数据库中的表，字段或者参数过多，我们应当考虑使用Map！

可以只写需要用到的字段，而new User可能会有过多字段需要写

```java
int addUser2(Map<String,Object> map);
```

```xml
<insert id="addUser2" parameterType="map">
    insert into mybatis.user (id,pwd) values (#{userid},#{password});
</insert>
```

```java
@Test
public void addUser2(){

    SqlSession sqlSession = MybatisUtils.getSqlSession();

    UserMapper mapper = sqlSession.getMapper(UserMapper.class);

    Map<String, Object> map = new HashMap<String,Object>();

    map.put("userid",5);
    map.put("password","222333");

    mapper.addUser2(map);

    //提交事务
    sqlSession.commit();
    sqlSession.close();

}
```

Map传递参数，直接在sql中取出key即可！【parameterType="map"】

对象传递参数，直接在sql中取对象的属性即可！【parameterType="Object"】

只有一个基本类型参数的情况下，可以直接在sql中取到！

多个参数用Map，**或者注解！**

### 模糊查询

1. Java代码执行时注意 传递通配符 % %

   ```java
   List<User> userLike = mapper.getUserLike("%李%");
   ```

2. 在sql拼接中使用通配符

   ```xml
   <select id="getUserLike" resultType="com.Sucker.pojo.User">
       select * from mybatis.user where name like "%"#{value}"%";
   </select>
   ```

## 配置解析

### 核心配置文件

- mybatis-config.xml

- MyBatis 的配置文件包含了会深深影响 MyBatis 行为的设置和属性信息

  ```xml
  configuration（配置）
  properties（属性）
  settings（设置）
  typeAliases（类型别名）
  typeHandlers（类型处理器）
  objectFactory（对象工厂）
  plugins（插件）
  environments（环境配置）
  environment（环境变量）
  transactionManager（事务管理器）
  dataSource（数据源）
  databaseIdProvider（数据库厂商标识）
  mappers（映射器）
  ```

### 环境配置(environments)

MyBatis 可以配置成适应多种环境，这种机制有助于将 SQL 映射应用于多种数据库之中

**不过要记住：尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。**

环境environments default 可以更改，设置默认环境

environments 元素定义了如何配置环境。

```
<environments default="development">
  <environment id="development">
    <transactionManager type="JDBC">
      <property name="..." value="..."/>
    </transactionManager>
    <dataSource type="POOLED">
      <property name="driver" value="${driver}"/>
      <property name="url" value="${url}"/>
      <property name="username" value="${username}"/>
      <property name="password" value="${password}"/>
    </dataSource>
  </environment>
</environments>
```

注意一些关键点:

- 默认使用的环境 ID（比如：default="development"）。
- 每个 environment 元素定义的环境 ID（比如：id="development"）。
- 事务管理器的配置（比如：type="JDBC"）。
- 数据源的配置（比如：type="POOLED"）。

默认环境和环境 ID 顾名思义。 环境可以随意命名，但务必保证默认的环境 ID 要匹配其中一个环境 ID。

**事务管理器（transactionManager）**

在 MyBatis 中有两种类型的事务管理器（也就是 type="[JDBC|MANAGED]"）：

- JDBC – 这个配置直接使用了 JDBC 的提交和回滚设施，它依赖从数据源获得的连接来管理事务作用域。

- MANAGED – 这个配置几乎没做什么。它从不提交或回滚一个连接，而是让容器来管理事务的整个生命周期（比如 JEE 应用服务器的上下文）。 默认情况下它会关闭连接。然而一些容器并不希望连接被关闭，因此需要将 closeConnection 属性设置为 false 来阻止默认的关闭行为。例如:

  ```
  <transactionManager type="MANAGED">
    <property name="closeConnection" value="false"/>
  </transactionManager>
  ```

**提示** 如果你正在使用 Spring + MyBatis，则没有必要配置事务管理器，因为 Spring 模块会使用自带的管理器来覆盖前面的配置。

Mybatis默认的事务管理器是JDBC，连接池：POOLED

### 属性(properties)

我们可以通过properties属性来实现引用配置文件

这些属性可以在外部进行配置，并可以进行动态替换。你既可以在典型的 Java 属性文件中配置这些属性，也可以在 properties 元素的子元素中设置【db.properties】

编写一个配置文件

db.properties

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useSSL=true&useUnicode=true&characterEncoding=UTF-8
username=root
password=123456
```

![](https://img-blog.csdnimg.cn/b797174451aa4e7783b41fd6c10c0855.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

在核心配置文件中引入

```xml
<!--文件就在resource目录下，可以简写-->
<!--引入外部配置文件-->
<properties resource="db.properties">
    <property name="username" value="root"/>
    <property name="password" value="111111"/>
</properties>
```

设置好的属性可以在整个配置文件中用来替换需要动态配置的属性值。比如:

```xml
<dataSource type="POOLED">
  <property name="driver" value="${driver}"/>
  <property name="url" value="${url}"/>
  <property name="username" value="${username}"/>
  <property name="password" value="${password}"/>
</dataSource>
```

如果一个属性在不只一个地方进行了配置，那么，MyBatis 将按照下面的顺序来加载：

- 首先读取在 properties 元素体内指定的属性。
- 然后根据 properties 元素中的 resource 属性读取类路径下属性文件，或根据 url 属性指定的路径读取属性文件，并覆盖之前读取过的同名属性。
- 最后读取作为方法参数传递的属性，并覆盖之前读取过的同名属性。

因此，通过方法参数传递的属性具有最高优先级，resource/url 属性中指定的配置文件次之，最低优先级的则是 properties 元素中指定的属性。

- 可以直接引入外部文件
- 可以在其中增加一些属性配置
- 如果两个文件有同一个字段，优先使用外部配置文件

### 类型别名（typeAliases）

- 类型别名可为 Java 类型设置一个缩写名字

- 它仅用于 XML 配置，意在降低冗余的全限定类名书写

  ```xml
  <!--    可以给类起别名-->
  <typeAliases>
      <typeAlias type="com.Sucker.pojo.User" alias="User"/>
  </typeAliases>
  ```

  当这样配置时，`Blog` 可以用在任何使用 `domain.blog.Blog` 的地方。

- 也可以指定一个包名，MyBatis 会在包名下面搜索需要的 Java Bean，比如：

  ```xml
  <typeAliases>
      <package name="com.Sucker.pojo"/>
  </typeAliases>
  ```

  每一个在包 `domain.blog` 中的 Java Bean，在没有注解的情况下，会使用 Bean 的首字母小写的非限定类名来作为它的别名。 比如 `domain.blog.Author` 的别名为 `author`

在实体类比较少的时候，使用第一种方式。

如果实体类较多，建议使用第二种

第一种可以DIY别名，第二种则不能，如果需要改，需要在实体类上增加注解

```java
@Alias("uuuu")
public class User {
    ...
}
```

下面是一些为常见的 Java 类型内建的类型别名。它们都是不区分大小写的，注意，为了应对原始类型的命名重复，采取了特殊的命名风格。

| 别名       | 映射的类型 |
| :--------- | :--------- |
| _byte      | byte       |
| _long      | long       |
| _short     | short      |
| _int       | int        |
| _integer   | int        |
| _double    | double     |
| _float     | float      |
| _boolean   | boolean    |
| string     | String     |
| byte       | Byte       |
| long       | Long       |
| short      | Short      |
| int        | Integer    |
| integer    | Integer    |
| double     | Double     |
| float      | Float      |
| boolean    | Boolean    |
| date       | Date       |
| decimal    | BigDecimal |
| bigdecimal | BigDecimal |
| object     | Object     |
| map        | Map        |
| hashmap    | HashMap    |
| list       | List       |
| arraylist  | ArrayList  |
| collection | Collection |
| iterator   | Iterator   |

### 设置

这是 MyBatis 中极为重要的调整设置，它们会改变 MyBatis 的运行时行为

| 设置名             | 描述                                                         | 有效值        | 默认值 |
| :----------------- | :----------------------------------------------------------- | :------------ | :----- |
| cacheEnabled       | 全局性地开启或关闭所有映射器配置文件中已配置的任何缓存。     | true \| false | true   |
| lazyLoadingEnabled | 延迟加载的全局开关。当开启时，所有关联对象都会延迟加载。 特定关联关系中可通过设置 `fetchType` 属性来覆盖该项的开关状态。 | true \| false | false  |

| logImpl | 指定 MyBatis 所用日志的具体实现，未指定时将自动查找。 | SLF4J \| LOG4J \| LOG4J2 \| JDK_LOGGING \| COMMONS_LOGGING \| STDOUT_LOGGING \| NO_LOGGING | 未设置 |      |
| :------ | ----------------------------------------------------- | ------------------------------------------------------------ | ------ | ---- |

### 其他配置

- [typeHandlers（类型处理器）](https://mybatis.org/mybatis-3/zh/configuration.html#typeHandlers)
- [objectFactory（对象工厂）](https://mybatis.org/mybatis-3/zh/configuration.html#objectFactory)
- [plugins（插件）](https://mybatis.org/mybatis-3/zh/configuration.html#plugins)
  - mybatis-generator-core
  - mybatis-plus
  - 通用mapper

### 映射器

MapperRegistry：注册绑定我们的Mapper文件

方式一：【推荐使用】

```xml
<!--    每一个Mapper.xml都需要在Mybatis核心配置文件中注册！-->
<mappers>
    <mapper resource="com/Sucker/dao/UserMapper.xml"/>
</mappers>
```

方式二：使用class文件绑定注册

```xml
<!--    每一个Mapper.xml都需要在Mybatis核心配置文件中注册！-->
<mappers>
    <mapper class="com.Sucker.dao.UserMapper"/>
</mappers>
```

注意点：

- 接口和它的Mapper配置文件必须同名
- 接口和它的Mapper配置文件必须在同一个包下！

方式三：使用扫描包进行注入绑定

```xml
<mappers>
    <package name="com.Sucker.dao"/>
</mappers>
```

注意点：

- 接口和它的Mapper配置文件必须同名
- 接口和它的Mapper配置文件必须在同一个包下！

### 生命周期和作用域(Scope)

![](https://img-blog.csdnimg.cn/cf7200f2de884b68af9da96bafd2ee42.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

作用域和生命周期类别是至关重要的，因为错误的使用会导致非常严重的**并发问题**

**SqlSessionFactoryBuilder：**

- 一旦创建了SqlSessionFactory，就不再需要它了
- 局部变量

**SqlSessionFactory：**

- 可以想象为数据库连接池
- SqlSessionFactory 一旦被创建就应该在应用的运行期间一直存在，没有任何理由丢弃它或重新创建另一个实例
- 因此 SqlSessionFactory 的最佳作用域是应用作用域
- 最简单的就是使用**单例模式**或者静态单例模式

**SqlSession:**

- 连接到连接池的一个请求
- 每个线程都应该有它自己的 SqlSession 实例
- SqlSession 的实例不是线程安全的，因此是不能被共享的，所以它的最佳的作用域是请求或方法作用域
- 用完需要立即关闭，否则资源被占用

![](https://img-blog.csdnimg.cn/b3185bc3275741edaa99eba6a50c0b79.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

每一个Mapper代表一个具体业务

## ResultMap结果映射集

**解决属性名和字段名不一致的问题**

```java
public class User {

    private int id;
    private String name;
    private String password;
}
```

测试出现问题，查找不到对应password

```
User{id=1, name='狂神', password='null'}
```

解决方法：

- 起别名

  ```xml
  <select id="getUserById" parameterType="int" resultType="com.Sucker.pojo.User">
      select id,name,pwd as password from mybatis.user where id = #{id}
  </select>
  ```

### resultMap

结果集映射

```java
id  name  pwd
id  name  password
```

在dao层中的xml文件中配置结果集映射

```xml
<!--    结果集映射-->
    <resultMap id="UserMap" type="User">
    <!--column 数据库中的字段  property实体类中的属性-->
        <result column="id" property="id"/>
        <result column="name" property="name"/>
        <result column="pwd" property="password"/>
    </resultMap>

    <select id="getUserById" resultMap="UserMap">
        select * from mybatis.user where id = #{id}
    </select>
```



- resultMap元素是 Mybatis 中最强大的元素
- ResultMap 的设计思想是，对于简单的语句根本不需要配置显式的结果映射，而对于复杂的语句只需要描述他们的关系即可
- ResultMap 最优秀的地方在于，虽然你已经对他相当了解了，但是根本就不需要显示的用到他们（只需要将需要映射的字段显式的定义出来）

## 日志

### 日志工厂

如果一个数据库操作，出现了异常，我们需要排错。日志就是最好的助手！

以往：sout，debug

现在：日志工厂！

| 设置名 | 描述 | 有效值 | 默认值 |
| :----- | :--- | :----- | :----- |

| logImpl | 指定 MyBatis 所用日志的具体实现，未指定时将自动查找。 | SLF4J \| LOG4J \|                                                                                              LOG4J2 \|                                                                                              JDK_LOGGING \|                                                                       COMMONS_LOGGING                                                                                                \| STDOUT_LOGGING \| NO_LOGGING | 未设置 |
| ------- | ----------------------------------------------------- | ------------------------------------------------------------ | ------ |

- SLF4J 
- LOG4J  【掌握】
-  LOG4J2
-  JDK_LOGGING
-  COMMONS_LOGGING
-  STDOUT_LOGGING  【掌握】
- NO_LOGGING

在Mybatis中具体使用哪个日志实现，在设置中设定！

**STDOUT_LOGGING标准日志输出**

在Mybatis核心配置文件中配置

```xml
<settings>
    <setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
```

![](https://img-blog.csdnimg.cn/094bc98d53734e8cb75d3df0b2d0d3ec.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### LOG4J

- Log4j是[Apache](https://baike.baidu.com/item/Apache/8512995)的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是[控制台](https://baike.baidu.com/item/控制台/2438626)、文件、[GUI](https://baike.baidu.com/item/GUI)组件，甚至是套接口服务器、[NT](https://baike.baidu.com/item/NT/3443842)的事件记录器、[UNIX](https://baike.baidu.com/item/UNIX) [Syslog](https://baike.baidu.com/item/Syslog)[守护进程](https://baike.baidu.com/item/守护进程/966835)等
- 我们可以控制每一条日志的输出格式
- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程
- 可以通过一个[配置文件](https://baike.baidu.com/item/配置文件/286550)来灵活地进行配置

1. 导入相关包（pom.xml）

   ```xml
   <!-- https://mvnrepository.com/artifact/log4j/log4j -->
   <dependency>
       <groupId>log4j</groupId>
       <artifactId>log4j</artifactId>
       <version>1.2.17</version>
   </dependency>
   ```

2. resource下新建log4j.properties文件

   ```properties
   #将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
   log4j.rootLogger=DEBUG,console,file
   
   #控制台输出的相关设置
   log4j.appender.console = org.apache.log4j.ConsoleAppender
   log4j.appender.console.Target = System.out
   log4j.appender.console.Threshold=DEBUG
   log4j.appender.console.layout = org.apache.log4j.PatternLayout
   log4j.appender.console.layout.ConversionPattern=【%c】-%m%n
   
   #文件输出的相关设置
   log4j.appender.file = org.apache.log4j.RollingFileAppender
   log4j.appender.file.File=./log/kuang.log
   log4j.appender.file.MaxFileSize=10mb
   log4j.appender.file.Threshold=DEBUG
   log4j.appender.file.layout=org.apache.log4j.PatternLayout
   log4j.appender.file.layout.ConversionPattern=【%p】【%d{yy-MM-dd}】【%c】%m%n
   
   #日志输出级别
   log4j.logger.org.mybatis=DEBUG
   log4j.logger.java.sql=DEBUG
   log4j.logger.java.sql.Statement=DEBUG
   log4j.logger.java.sql.ResultSet=DEBUG
   log4j.logger.java.sql.PreparedStatement=DEBUG
   ```

3. 配置log4j为日志实现

   ```xml
   <settings>
       <setting name="logImpl" value="LOG4J"/>
   </settings>
   ```

4. log4j的使用，直接运行测试

   ![](https://img-blog.csdnimg.cn/3a4dd66c6d2d4d27b19b46d522d18682.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

**简单使用**

1. 在要使用Log4j的类中，导入包 import org.apache.log4j.Logger;

2. 日志对象，参数为当前类的class (反射)

   ```java
   static Logger logger = Logger.getLogger(UserDaoTest.class);
   ```

3. 日志级别

   ```java
           logger.info("info:进入了testLog4j");
           logger.debug("debug:进入了testLog4j");
           logger.error("error:进入了testLog4j");
   ```

4. 通过日志查找错误

   ```java
   public class UserDaoTest {
   
       static Logger logger = Logger.getLogger(UserDaoTest.class);
   
       @Test
       public void test(){
           //第一步：获得sqlSession对象
           SqlSession sqlSession = MybatisUtils.getSqlSession();
   
           logger.info("测试！");
   
           //执行SQL
           //方式一：getMapper
           UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
           User user = userMapper.getUserById(1);
   
           System.out.println(user);
   
           //关闭sqlSession
           sqlSession.close();
   
       }
   }
   ```

   ```xml
   [DEBUG][21-09-10][org.apache.ibatis.io.ResolverUtil]Checking to see if class com.Sucker.dao.UserDaoTest matches criteria [is assignable to Object]
   [DEBUG][21-09-10][org.apache.ibatis.io.ResolverUtil]Checking to see if class com.Sucker.dao.UserMapper matches criteria [is assignable to Object]
   
   
   [INFO][21-09-10][com.Sucker.dao.UserDaoTest]测试！
   
   
   [DEBUG][21-09-10][org.apache.ibatis.transaction.jdbc.JdbcTransaction]Opening JDBC Connection
   [DEBUG][21-09-10][org.apache.ibatis.datasource.pooled.PooledDataSource]Created connection 1652149987.
   [DEBUG][21-09-10][org.apache.ibatis.transaction.jdbc.JdbcTransaction]Setting autocommit to false on JDBC Connection [com.mysql.jdbc.JDBC4Connection@6279cee3]
   [DEBUG][21-09-10][com.Sucker.dao.UserMapper.getUserById]==>  Preparing: select * from mybatis.user where id = ?
   [DEBUG][21-09-10][com.Sucker.dao.UserMapper.getUserById]==> Parameters: 1(Integer)
   [DEBUG][21-09-10][com.Sucker.dao.UserMapper.getUserById]<==      Total: 1
   [DEBUG][21-09-10][org.apache.ibatis.transaction.jdbc.JdbcTransaction]Resetting autocommit to true on JDBC Connection [com.mysql.jdbc.JDBC4Connection@6279cee3]
   [DEBUG][21-09-10][org.apache.ibatis.transaction.jdbc.JdbcTransaction]Closing JDBC Connection [com.mysql.jdbc.JDBC4Connection@6279cee3]
   [DEBUG][21-09-10][org.apache.ibatis.datasource.pooled.PooledDataSource]Returned connection 1652149987 to pool.
   
   ```

## 分页

- 减少数据的处理量

### 使用Limit分页

```sql
语法：SELECT * from user limit startIndex,pagesize;
SELECT * from user limit 3; #[0,n]
```

使用Mybatis实现分页，核心SQL

1. 接口

   ```java
   //分页
   List<User> getUserByLimit(HashMap<String , Integer> map);
   ```

2. Mapper，xml

   ```xml
   <!--    分页-->
   <select id="getUserByLimit" parameterType="map" resultMap="UserMap"> 此处使用了结果集映射
       select * from mybatis.user limit #{startIndex},#{pageSize}
   </select>
   ```

3. 测试

   ```java
   @Test
   public void getUserByLimit(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
   
       HashMap<String, Integer> map = new HashMap<String, Integer>();
       map.put("startIndex",0);
       map.put("pageSize",2);
   
       List<User> userList = mapper.getUserByLimit(map);
       for (User user : userList) {
           System.out.println(user);
       }
   
       sqlSession.close();
   }
   ```

### RowBounds分页

了解即可

不再使用SQL实现

1. 接口

   ```java
       //分页2
       List<User> getUserByRowBounds();
   ```

2. mapper.xml

   ```xml
   <!--    分页2-->
   <select id="getUserByLimit" resultMap="UserMap">
       select * from mybatis.user
   </select>
   ```

3. 测试

   ```java
   @Test
   public void getUserByRowbounds(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       //RowBounds实现
       RowBounds rowBounds = new RowBounds(1,2);
   
       //通过Java层面实现分页
       List<User> userList = sqlSession.selectList("com.Sucker.dao.UserMapper.getUserByRowBounds",null,rowBounds);
   
       for (User user : userList) {
           System.out.println(user);
       }
   
       sqlSession.close();
   }
   ```

### 分页插件

![](https://img-blog.csdnimg.cn/058910acc6074a04bb56d0962d5b4782.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

了解即可

## 使用注解开发

### 面向接口编程

在真正的开发中，我们往往是面向接口编程

**根本原因：==解耦==,可拓展，提高复用，分层开发中，上层不用管具体的实现，大家都遵守共同的标准，使得开发变得容易，规范性更好**

在一个面向对象的系统中，系统的各种功能是由许许多多的不同对象协作完成的。在这种情况下，各个对象内部是如何实现自己的，对系统设计人员来讲就不那么重要了

而各个对象之间的协作关系则称为系统设计的关键。小到不同类之间的通信，大到各模块之间的交互，在系统设计之初都是要着重考虑的，这也是系统设计的主要工作内容。面向接口编程就是指按照这种思想来编程。

**关于接口的理解**

- 接口从更深层次的理解，应是定义（规范，约束）与实现（名实分离的原则）的分离
- 接口的本身反应了系统设计人员对系统的抽象理解
- 接口应有两类：
  - 第一类是对一个个体的抽象，它可以对应为一个抽象体(abstract class)；
  - 第二类是对一个个体某一方面的抽象，即形成一个抽象面(interface)；
- 一个体有可能有多个抽象面。抽象体与抽象面是有区别的

**三个面向区别**

- 面向对象是指，我们考虑问题时，以对象为单位，考虑它的属性和方法
- 面向过程是指，我们考虑问题时，以一个具体的流程(事务过程) 为单位，考虑它的实现
- 接口设计与非接口设计是针对复用技术而言的，与面向对象(过程) 不是一个问题，更多的体现就是对系统整体的架构

### 使用注解开发

1. 注解在接口上实现

   ```java
   @Select("select * from user")
   List<User> getUsers();
   ```

2. 需要在核心配置文件中绑定接口

   ```xml
   <!--    绑定接口-->
   <mappers>
       <mapper class="com.Sucker.dao.UserMapper"/>
   </mappers>
   ```

3. 测试

   ```java
   @Test
   public void test(){
   
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       //底层主要应用反射
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       List<User> users = mapper.getUsers();
       for (User user : users) {
           System.out.println(user);
       }
       sqlSession.close();
   
   }
   ```

本质：反射机制实现

底层：动态代理！

**Mybatis详细执行流程**

![](https://img-blog.csdnimg.cn/17173e0e953e4f139c5461b6b24ec93a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_14,color_FFFFFF,t_70,g_se,x_16#pic_center)

### CRUD

我们可以在工具类创建的时候实现自动提交事务！

```java
public static SqlSession getSqlSession(){
    return sqlSessionFactory.openSession(true);//得到能执行sql的Session对象
}//有参数为true时自动提交事务 无参数时默认false
```



编写接口，增加注解

方法存在多个参数的时候，所有的参数前面需要加上 @Param(“”)注解,参数对应SQL语句中的参数，不是对应方法的参数

```java
public interface UserMapper {
    @Select("select * from user")
    List<User> getUsers();

    // 方法存在多个参数的时候，所有的参数前面需要加上 @Param(“”)注解,参数对应SQL语句中的参数，不是对应方法的参数
    @Select("select * from user where id = #{id}")
    User getUserByID(@Param("id") int id);

    @Insert("insert into user(id,name,pwd) values(#{id},#{name},#{password})")
    int addUser(User user);

    @Update("update user set name=#{name},pwd=#{password} where id = #{id}")
    int updateUser(User user);

    @Delete("delete from user where id = #{uid}")
    int deleteUser(@Param("uid") int id);

}
```

测试类

【注意：必须将接口注册绑定在核心配置文件中！】

```java
    @Test
    public void test(){

        SqlSession sqlSession = MybatisUtils.getSqlSession();

        //底层主要应用反射
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);

        mapper.deleteUser(6);

        sqlSession.close();

    }

    /*
        List<User> users = mapper.getUsers();
        for (User user : users) {
            System.out.println(user);
        }

        User userByID = mapper.getUserByID(1);
        System.out.println(userByID);

        mapper.addUser(new User(6,"Hello","123123"));

        mapper.updateUser(new User(6,"to","111111"));


     */
```



使用注解来映射简单语句会使代码显得更加简洁，但对于稍微复杂一点的语句，Java 注解不仅力不从心，还会让你本就复杂的 SQL 语句更加混乱不堪。 因此，如果你需要做一些很复杂的操作，最好用 XML 来映射语句。

### 关于@Param()注解

- 基本类型的参数或String类型，需要加上
- 引用类型不需要加
- 如果只有一个基本类型，可以忽略，但是建议加上
- 在SQL中引用的就是这里 @Param("uid") 中设定的属性名！

## Lombok

```java
Project Lombok is a java library that automatically plugs into your editor and build tools, spicing up your java.
Never write another getter or equals method again, with one annotation your class has a fully featured builder, Automate your logging variables, and much more.
```

- java library
- plugs
- build tools
- with one annotation your class

使用步骤：

1. 在IDEA中安装Lombok插件！

2. 在项目中导入Lombok jar包

   ```xml
   <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
   <dependency>
       <groupId>org.projectlombok</groupId>
       <artifactId>lombok</artifactId>
       <version>1.18.20</version>
       <scope>provided</scope>
   </dependency>
   
   ```

3. 在实体类上加注解即可

   ```java
   @Data
   @AllArgsConstructor 
   @NoArgsConstructor
   ```

   

   ```java
   @Getter and @Setter
   @FieldNameConstants
   @ToString
   @EqualsAndHashCode
   @AllArgsConstructor, @RequiredArgsConstructor and @NoArgsConstructor
   @Log, @Log4j, @Log4j2, @Slf4j, @XSlf4j, @CommonsLog, @JBossLog, @Flogger, @CustomLog
   @Data
   @Builder
   @SuperBuilder
   @Singular
   @Delegate
   @Value
   @Accessors
   @Wither
   @With
   @SneakyThrows
   @val
   @var
   experimental @var
   @UtilityClass
   Lombok config system
   ```

```java
@Data：无参构造，get，set，toString，hashcode，equals
@AllArgsConstructor 
@NoArgsConstructor
@EqualsAndHashCode
@ToString
@Getter
```

## 多对一处理

多对一：多个学生对应一个老师

多个学生关联一个老师【多对一】

一个老师有很多学生【一对多】

![](https://img-blog.csdnimg.cn/d74139c740d64709969262f18f2e7921.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_18,color_FFFFFF,t_70,g_se,x_16)

### 测试环境搭建

1. 导入lombok

2. 新建实体类 Teacher Student

   ```java
   @Data
   public class Student {
   
       private int id;
       private String name;
   
       //学生需要关联一个老师
       private Teacher teacher;
   
   }
   ```

3. 建立Mapper接口

   ```java
   public interface TeacherMapper {
   
       @Select("select * from teacher where id = #{tid}")
       Teacher getTeacher(@Param("tid") int id);
   
   }
   ```

4. 建立Mapper.xml文件

5. 在核心配置文件中绑定注册Mapper接口或文件！【方式很多】

6. 测试查询是否成功

SQL：

```sql
CREATE TABLE `teacher` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO teacher(`id`, `name`) VALUES (1, '秦老师'); 

CREATE TABLE `student` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  `tid` INT(10) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fktid` (`tid`),
  CONSTRAINT `fktid` FOREIGN KEY (`tid`) REFERENCES `teacher` (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (1, '小明', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (2, '小红', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (3, '小张', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (4, '小李', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (5, '小王', 1);
```



一个表对应一个实体类，一个实体类对应一个Mapper接口，一个接口对应一个xml

xml可以写在resources目录下，但时要和Mapper接口目录相同，即resources下添加一个com.Sucker.dao文件夹（注意这里必须能展开）

建立xml，复制，mybatis核心配置文件来修改

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper                              <!--这里改为mapper-->
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">  <!--这里改为mapper-->
<!--mapper核心配置文件-->  <!--这里改为mapper-->
<mapper namespace="com.Sucker.dao.StudentMapper">   <!--这里绑定接口-->

</mapper>
```

在mybatis核心配置文件中注册mapper

com前面没有 / ，表示就在当前目录下

```xml
<mappers>
    <mapper class="com.Sucker.dao.TeacherMapper"/>
    <mapper class="com.Sucker.dao.StudentMapper"/>
</mappers>
```

### 按照查询嵌套处理

StudentMapper.xml

<!--复杂的属性，我们需要单独处理  对象： association  集合： collection-->

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--mapper核心配置文件-->
<mapper namespace="com.Sucker.dao.StudentMapper">

    <!--
    思路：
        1.查询所有的学生
        2.根据查询出来的学生的tid，寻找对应的老师！ 子查询

    -->
    
    <select id="getStudent" resultMap="StudentTeacher">
        select * from student;
    </select>
    <resultMap id="StudentTeacher" type="Student">
        <result property="id" column="id"/>
        <result property="name" column="name"/>
        <!--复杂的属性，我们需要单独处理  对象： association  集合： collection-->
        <association property="teacher" column="tid" javaType="Teacher" select="getTeacher"/>
    </resultMap>
    
    <select id="getTeacher" resultType="Teacher">
        select * from teacher where id = #{id}
    </select>

</mapper>
```

### 按照结果嵌套处理

```xml
    <!--按照结果嵌套处理-->
    <select id="getStudent2" resultMap="StudentTeacher2">
        select s.id sid,s.name sname,t.name tname
        from student s,teacher t
        where s.tid = t.id;
    </select>
    
    <resultMap id="StudentTeacher2" type="Student">
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
        <association property="teacher" javaType="Teacher">
            <result property="name" column="tname"/>
        </association>
    </resultMap>

```

回顾Mysql多对一查询方式：

- 子查询
- 联表查询

## 一对多处理

比如：一个老师拥有多个学生！

对于老师而言，就是一对多的关系

### 环境搭建

1. 实体类

   ```java
   @Data
   public class Teacher {
   
       private int id;
       private String name;
   
       private List<Student> students;
   
   }
   ```

   ```java
   @Data
   public class Student {
   
       private int id;
       private String name;
       private int tid;
   
   }
   ```


### 按结果嵌套查询

```xml
<!--    按结果嵌套查询-->
    <select id="getTeacher" resultMap="TeacherStudent">
        select s.id sid ,s.name sname,t.id tid ,t.name tname
        from student s,teacher t
        where s.tid=t.id and t.id = #{tid}
    </select>

    <resultMap id="TeacherStudent" type="Teacher">
        <result property="id" column="tid"/>
        <result property="name" column="tname"/>
        <!--复杂的属性，我们需要单独处理  对象： association  集合： collection
        javaType:指定的属性类型
        集合种的泛型信息，我们使用ofType获取
        -->
        <collection property="students" ofType="Student">
            <result property="id" column="sid"/>
            <result property="name" column="sname"/>
            <result property="tid" column="tid"/>
        </collection>
    </resultMap>
```

```java
@Test
public void Test(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    TeacherMapper mapper = sqlSession.getMapper(TeacherMapper.class);
    Teacher teacher = mapper.getTeacher(1);
    System.out.println(teacher);
    sqlSession.close();
}
```

### 按照查询嵌套处理

```xml
    
    <select id="getTeacher2" resultMap="TeacherStudent2">
        select * from mybatis.teacher where id = #{tid}
    </select>
    
    <resultMap id="TeacherStudent2" type="Teacher">
<!--        一样的可以省略-->
        <collection property="students" javaType="ArrayList" ofType="Student" select="getStudentByTeacherId" column="id"/>
    </resultMap>
    
    <select id="getStudentByTeacherId" resultType="Student">
        select * from mybatis.student where tid = #{tid}
    </select>
```

```java
@Test
public void Test2(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    TeacherMapper mapper = sqlSession.getMapper(TeacherMapper.class);
    Teacher teacher = mapper.getTeacher2(1);
    System.out.println(teacher);
    sqlSession.close();
}
```

### 小结

1. 关联 - association 【多对一】
2. 集合 - collection  【一对多】
3. javaType    &     ofType
   - javaTpye  用来指定实体类中的属性类型
   - ofType  用来指定映射到List 或者 集合中的 pojo 类型 ，泛型中的约束类型！

注意点：

- 保证SQL的可读性，尽量保证通俗易懂
- 注意一对多与多对一的关系，属性名和字段问题！
- 可以使用日志排查错误

## 动态SQL

动态SQL：动态SQL是指根据不同的条件生成不同的SQL语句

```
如果你之前用过 JSTL 或任何基于类 XML 语言的文本处理器，你对动态 SQL 元素可能会感觉似曾相识。在 MyBatis 之前的版本中，需要花时间了解大量的元素。借助功能强大的基于 OGNL 的表达式，MyBatis 3 替换了之前的大部分元素，大大精简了元素种类，现在要学习的元素种类比原来的一半还要少。

if
choose (when, otherwise)
trim (where, set)
foreach
```

### 搭建环境

```sql
CREATE TABLE `blog`(
`id` VARCHAR(50) NOT NULL COMMENT '博客id',
`title` VARCHAR(100) NOT NULL COMMENT '博客标题',
`author` VARCHAR(30) NOT NULL COMMENT '博客作者',
`create_time` DATETIME NOT NULL COMMENT '创建时间',
`views` INT(30) NOT NULL COMMENT '浏览量'
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

创建一个基础工程

- 导包

- 编写配置文件

- 编写实体类

  ```java
  @Data
  public class Blog {
      private int id;
      private String title;
      private String author;
      private Date createTime;
      private int views;
  }
  ```

- 编写实体类对应的Mapper接口 和 Mapper.xml文件

| mapUnderscoreToCamelCase | 是否开启驼峰命名自动映射，即从经典数据库列名 A_COLUMN 映射到经典 Java 属性名 aColumn。 | true \| false | False |
| ------------------------ | ------------------------------------------------------------ | ------------- | ----- |

我们一般在数据库中字段名使用 '`_`'连接，而在实体类中使用驼峰命名。但是这样查询之后使用的驼峰命名法的是映射不到实体类上的 。

要解决这个问题只需要在mybatis配置文件中添加以下配置

```xml
<settings>
    <setting name="logImpl" value="STDOUT_LOGGING"/>
    <!--        是否开启驼峰命名自动映射-->
    <setting name="mapUnderscoreToCamelCase" value="true"/>
</settings>
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--mapper核心配置文件-->
<mapper namespace="com.Sucker.dao.BlogMapper">

    <insert id="addBlog" parameterType="blog">
        insert into mybatis.blog(id,title,author,create_time,views)
        values (#{id},#{title},#{author},#{createTime},#{views});
    </insert>

</mapper>
```

测试类：

```java
public class MyTest {

    @Test
    public void addInitBlog(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

        Blog blog = new Blog();
        blog.setId(IDUtils.getId());
        blog.setTitle("Mybatis");
        blog.setAuthor("狂神说");
        blog.setCreateTime(new Date());
        blog.setViews(9999);

        mapper.addBlog(blog);

        blog.setId(IDUtils.getId());
        blog.setTitle("Java如此简单");
        mapper.addBlog(blog);

        blog.setId(IDUtils.getId());
        blog.setTitle("Spring");
        mapper.addBlog(blog);

        blog.setId(IDUtils.getId());
        blog.setTitle("微服务");
        mapper.addBlog(blog);

        sqlSession.close();
    }
}

```

### IF

```xml
<select id="queryBlogIF" parameterType="map" resultType="blog">
    select * from mybatis.blog where 1=1
    <if test="title != null">
        and title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</select>
```

```java
@Test
public void queryBlogIF(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

    HashMap map = new HashMap();
    map.put("title","java如此简单");
    List<Blog> blogs = mapper.queryBlogIF(map);
    for (Blog blog : blogs) {
        System.out.println(blog);
    }


    sqlSession.close();
}
```

### choose (when, otherwise)

有时候，我们不想使用所有的条件，而只是想从多个条件中选择一个使用。针对这种情况，MyBatis 提供了 choose 元素，它有点像 Java 中的 switch 语句。

```xml
<select id="queryBlogChoose" parameterType="map" resultType="blog">
    select * from mybatis.blog
    <where>
        <choose>
            <when test="title !=null">
                title = #{title}
            </when>
            <when test="author != null">
                and author = #{author}
            </when>
            <otherwise>
                and views = #{views}
            </otherwise>
        </choose>
    </where>
</select>
```

```java
    @Test
    public void queryBlogIF(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

        HashMap map = new HashMap();
//        map.put("title","java如此简单");
//        map.put("author","狂神说");
//        map.put("views","9999");

        List<Blog> blogs = mapper.queryBlogChoose(map);

        for (Blog blog : blogs) {
            System.out.println(blog);
        }


        sqlSession.close();
    }
```

### trim (where, set)

如果没有匹配的条件会怎么样？最终这条 SQL 会变成这样：

```sql
SELECT * FROM BLOG
WHERE
```

这会导致查询失败。如果匹配的只是第二个条件又会怎样？这条 SQL 会是这样:

```sql
SELECT * FROM BLOG
WHERE
AND title like ‘someTitle’
```

这个查询也会失败。这个问题不能简单地用条件元素来解决。这个问题是如此的难以解决，以至于解决过的人不会再想碰到这种问题。

MyBatis 有一个简单且适合大多数场景的解决办法。而在其他场景中，可以对其进行自定义以符合需求。而这，只需要一处简单的改动：使用where语句

*where* 元素只会在子元素返回任何内容的情况下才插入 “WHERE” 子句。而且，若子句的开头为 “AND” 或 “OR”，*where* 元素也会将它们去除。

```xml
select * from mybatis.blog
<where>
    <if test="title != null">
        and title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</where>
```

用于动态更新语句的类似解决方案叫做 *set*。*set* 元素可以用于动态包含需要更新的列，忽略其它不更新的列。比如：

```xml
<update id="updateBlog" parameterType="map">
    update mybatis.blog
    <set>
        <if test="title != null">
            title = #{title},
        </if>
        <if test="author != null">
            author = #{author}
        </if>
    </set>
    where id = #{id}
</update>
```

```java
    @Test
    public void queryBlogChoose(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

        HashMap map = new HashMap();
        map.put("title","java如此简单2");
        map.put("author","狂神说");
        map.put("id","7f1a8213ca3740c89a9a6c92df268b76");
//        map.put("views","9999");

        mapper.updateBlog(map);
        sqlSession.close();
    }
```

这个例子中，*set* 元素会动态地在行首插入 SET 关键字，并会删掉额外的逗号（这些逗号是在使用条件语句给列赋值时引入的）。



如果 *where* 元素与你期望的不太一样，你也可以通过自定义 trim 元素来定制 *where* 元素的功能。比如，和 *where* 元素等价的自定义 trim 元素为：

```sql
<trim prefix="WHERE" prefixOverrides="AND |OR ">
  ...
</trim>
```

*prefixOverrides* 属性会忽略通过管道符分隔的文本序列（注意此例中的空格是必要的）。上述例子会移除所有 *prefixOverrides* 属性中指定的内容，并且插入 *prefix* 属性中指定的内容。

用于动态更新语句的类似解决方案叫做 *set*。*set* 元素可以用于动态包含需要更新的列，忽略其它不更新的列。比如：

```sql
<update id="updateAuthorIfNecessary">
  update Author
    <set>
      <if test="username != null">username=#{username},</if>
      <if test="password != null">password=#{password},</if>
      <if test="email != null">email=#{email},</if>
      <if test="bio != null">bio=#{bio}</if>
    </set>
  where id=#{id}
</update>
```

这个例子中，*set* 元素会动态地在行首插入 SET 关键字，并会删掉额外的逗号（这些逗号是在使用条件语句给列赋值时引入的）。

来看看与 *set* 元素等价的自定义 *trim* 元素吧：

```sql
<trim prefix="SET" suffixOverrides=",">
  ...
</trim>
```

注意，我们覆盖了后缀值设置，并且自定义了前缀值。

### SQL片段

有的时候，我们可能会将一些功能的部分抽取出来，方便复用！

1. 使用 sql 标签抽取公共部分
2. 在需要的地方使用 include 标签引用

```xml
<sql id="if-title-author">
    <if test="title != null">
        and title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</sql>

<select id="queryBlogIF" parameterType="map" resultType="blog">
    select * from mybatis.blog
    <where>
        <include refid="if-title-author"></include>
    </where>
</select>
```

注意事项：

- 最好基于单表来定义SQL片段
- 不要存在where标签



### foreach

![](https://img-blog.csdnimg.cn/2d8075707a47446093f5067834ec7865.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```xml
select * from user where 1=1 and

  <foreach item="id" collection="ids"
      open="(" separator="or" close=")">
      	 #{id}
  </foreach>
(id=1 or id=2 or id=3)
```

测试：

```sql
1,java如此简单2,狂神说,2021-09-23 19:30:27,9999
2,Java如此简单,狂神说,2021-09-23 19:30:27,1000
3,Spring,狂神说,2021-09-23 19:30:27,9999
4,微服务,狂神说,2021-09-23 19:30:27,9999
```

```xml
<!--
    select * from mybatis.blog where 1=1 and (id=1 or id=2 or id=3)

    现在传递一个map，这个map中可以存在一个集合！
    -->
<select id="queryBlogForeach" parameterType="map" resultType="blog">
    select * from mybatis.blog
    <where>
        <foreach collection="ids" item="id" open="and (" close=")" separator="or">
            id = #{id}
        </foreach>
    </where>

</select>
```

```java
//查询1-2-3号记录的博客
List<Blog> queryBlogForeach(Map map);
```

```java
@Test
public void queryBlogForeach(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

    HashMap map = new HashMap();
    ArrayList<Integer> ids = new ArrayList<>();
    ids.add(1);
    ids.add(2);

    map.put("ids",ids);
    List<Blog> blogs = mapper.queryBlogForeach(map);

    for (Blog blog : blogs) {
        System.out.println(blog);
    }

    sqlSession.close();
}
```

`动态SQL就是在拼接SQL语句，我们只要保证SQL的正确性，按照SQL的格式，去排列组合即可`

建议：

- 先在MySQL中写出完整的SQL，再对应去修改成为动态SQL实现通用即可

## 缓存

### 简介

```
查询：  连接数据库，耗资源！
	一次查询的结果，给它暂存在一个可以直接取到的地方！---> 内存： 缓存
	
	我们再次查询相同数据的时候，直接走缓存，就不用走数据库了
```

1. 什么是缓存[ Cache ]？
   - 存在内存中的临时数据
   - 将用户经常查询的数据放在缓存（内存）中，用户去查询数据就不用从磁盘上（关系型数据库数据文件）查询，从缓存中查询，从而提高查询效率，解决了高并发系统的性能问题
2. 为什么使用缓存？
   - 减少和数据库的交互次数，减少系统开销，提高系统效率
3. 什么样的数据能够使用缓存？
   - 经常查询并且不经常改变的数据

### Mybatis缓存

- MyBatis包含一个非常强大的查询缓存特性，它可以非常方便的定制和配置缓存。缓存从可以极大的提升查询效率
- MyBatis系统中默认定义了两级缓存：**一级缓存**和**二级缓存**
  - 默认情况下，只有一级缓存开启。（SqlSession级别的缓存，也称为本地缓存）
  - 二级缓存需要手动开启和配置，它是基于namespace级别的缓存
  - 为了提高扩展性，Mybatis定义了缓存接口Cache。我们可以通过实现Cache接口来自定义二级缓存

### 一级缓存

- 一级缓存也叫本地缓存：SqlSession
  - 与数据库同一次会话期间查询到的数据会放在本地缓存中
  - 以后如果需要获取相同的数据，直接从缓存拿，没必要再去查询数据库

测试步骤：

1. 开启日志

2. 测试在一个Session中查询两次相同记录

3. 查看日志输出

   ![](https://img-blog.csdnimg.cn/d473989e00f94359b0759dafcb48cbdb.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

缓存失效的情况：

1. 查询不同的东西

2. 增删改可能会改变原来的数据，所以必定会刷新缓存！

   ![](https://img-blog.csdnimg.cn/174ae2be8f314b1fa824f76b12f487c3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

3. 查询不同的Mapper.xml

4. 手动清理缓存

   ```java
   sqlSession.clearCache();//手动清理缓存
   ```

测试：

```xml
@Test
public void test(){
SqlSession sqlSession = MybatisUtils.getSqlSession();
UserMapper mapper = sqlSession.getMapper(UserMapper.class);
User user1 = mapper.queryUserById(1);
System.out.println(user1);

//mapper.updateUser(new User(2,"aaaa","bbbbb"));
sqlSession.clearCache();//手动清理缓存

System.out.println("==================");
User user2 = mapper.queryUserById(1);
System.out.println(user2);


sqlSession.close();
}
```

小结：一级缓存默认是开启的，只在一次SqlSession中有效，也就是拿到连接到关闭连接这个区间段

### 二级缓存

- 二级缓存也叫全局缓存，一级缓存的作用域太低了，所以诞生了二级缓存
- 基于namespace级别的缓存，一个命名空间，对应一个二级缓存
- 工作机制
  - 一个会话查询一条数据，这个数据就会被放在当前会话的一级缓存中
  - 如果当前会话关闭了，这个会话对应的壹基金缓存就没了；但是我们想要的是，会话关闭了，一级缓存中的数据被保存在二级缓存中
  - 新的会话查询信息，就可以从二级缓存中获取内容
  - 不同的Mapper查出的数据会放在自己对应的缓存（map）中

步骤：

1. 开启全局缓存

   ```xml
   <!--显式的开启全局缓存-->
   <setting name="cacheEnabled" value="true"/>
   ```

2. 在要使用二级缓存的Mapper中开启

   

   默认情况下，只启用了本地的会话缓存，它仅仅对一个会话中的数据进行缓存。 要启用全局的二级缓存，只需要在你的 SQL 映射文件中添加一行：

   ```xml
   <cache/>
   ```

   基本上就是这样。这个简单语句的效果如下:

   - 映射语句文件中的所有 select 语句的结果将会被缓存。
   - 映射语句文件中的所有 insert、update 和 delete 语句会刷新缓存。
   - 缓存会使用最近最少使用算法（LRU, Least Recently Used）算法来清除不需要的缓存。
   - 缓存不会定时进行刷新（也就是说，没有刷新间隔）。
   - 缓存会保存列表或对象（无论查询方法返回哪种）的 1024 个引用。
   - 缓存会被视为读/写缓存，这意味着获取到的对象并不是共享的，可以安全地被调用者修改，而不干扰其他调用者或线程所做的潜在修改。

   **提示** 缓存只作用于 cache 标签所在的映射文件中的语句。如果你混合使用 Java API 和 XML 映射文件，在共用接口中的语句将不会被默认缓存。你需要使用 @CacheNamespaceRef 注解指定缓存作用域。

   

   ```xml
   <cache
          eviction="FIFO"
          flushInterval="60000"
          size="512"
          readOnly="true"/>
   
   <!--这里的useCache可以不用设置，默认为true，可以手动为false关闭-->
   
   <select id="queryUserById" parameterType="_int" resultType="user" useCache="true">
       select * from mybatis.user where id=#{id}
   </select>
   ```

   这个更高级的配置创建了一个 FIFO 缓存，每隔 60 秒刷新，最多可以存储结果对象或列表的 512 个引用，而且返回的对象被认为是只读的，因此对它们进行修改可能会在不同线程中的调用者产生冲突。

   可用的清除策略有：

   - `LRU` – 最近最少使用：移除最长时间不被使用的对象。
   - `FIFO` – 先进先出：按对象进入缓存的顺序来移除它们。
   - `SOFT` – 软引用：基于垃圾回收器状态和软引用规则移除对象。
   - `WEAK` – 弱引用：更积极地基于垃圾收集器状态和弱引用规则移除对象。

   默认的清除策略是 LRU。

   flushInterval（刷新间隔）属性可以被设置为任意的正整数，设置的值应该是一个以毫秒为单位的合理时间量。 默认情况是不设置，也就是没有刷新间隔，缓存仅仅会在调用语句时刷新。

   size（引用数目）属性可以被设置为任意正整数，要注意欲缓存对象的大小和运行环境中可用的内存资源。默认值是 1024。

   readOnly（只读）属性可以被设置为 true 或 false。只读的缓存会给所有调用者返回缓存对象的相同实例。 因此这些对象不能被修改。这就提供了可观的性能提升。而可读写的缓存会（通过序列化）返回缓存对象的拷贝。 速度上会慢一些，但是更安全，因此默认值是 false。

   **提示** 二级缓存是事务性的。这意味着，当 SqlSession 完成并提交时，或是完成并回滚，但没有执行 flushCache=true 的 insert/delete/update 语句时，缓存会获得更新。

   

3. 测试

   ```xml
   <cache
          eviction="FIFO"
          flushInterval="60000"
          size="512"
          readOnly="true"/>
   
   <select id="queryUserById" parameterType="_int" resultType="user" useCache="true">
       select * from mybatis.user where id=#{id}
   </select>
   ```

   ```java
   @Test
   public void test(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       SqlSession sqlSession2 = MybatisUtils.getSqlSession();
   
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
   
       User user1 = mapper.queryUserById(1);
       System.out.println(user1);
       sqlSession.close();
   
       UserMapper mapper2 = sqlSession2.getMapper(UserMapper.class);
       User user2 = mapper2.queryUserById(1);
       System.out.println(user2);
   
       System.out.println(user1==user2);
       sqlSession2.close();
   }
   ```

   结果是在二级缓存中

4. 问题：

   1. 只使用最基本的cache时，需要将实体类序列化！否则会报错（实现Serializable接口）

      ```java
       Cause: java.io.NotSerializableException: com.Sucker.pojo.User
      ```

      ```xml
      <cache/>
      ```

      ```java
      @Data
      @AllArgsConstructor
      @NoArgsConstructor
      public class User implements Serializable {
      
          private int id;
          private String name;
          private String pwd;
      
      }
      ```


小结：

- 只要开启了二级缓存，在同一个Mapper下就有效
- 所有的数据都会先放到一级缓存中
- 只有当会话提交，或者关闭的时候，才会提交到二级缓存中

### 缓存原理

![](https://img-blog.csdnimg.cn/f3ebfe7dd80b434db0fc9f2ca8e20c5f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)



### 自定义缓存-ehcache

```xml
Ehcache是一种广泛使用的开源Java分布式缓存。主要面向通用缓存
```

要在程序中使用Ehcache，先要导包！

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.1</version>
</dependency>
```

配置文件

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
        updateCheck="false">

    <diskStore path="./tmpdir/Tmp_EhCache"/>

    <defaultCache
            eternal="false"
            maxElementsInMemory="10000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="259200"
            memoryStoreEvictionPolicy="LRU"/>

    <cache
            name="cloud_user"
            eternal="false"
            maxElementsInMemory="5000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="1800"
            memoryStoreEvictionPolicy="LRU"/>
</ehcache>
```

一般不使用这个，用Redis数据库来做缓存！

### 29道动态SQL习题

