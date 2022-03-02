## Spring

### 简介

- Spring 理念：使现有的技术更加容易使用，本身是一个大杂侩，整合了现有的技术框架！
- SSH：Struct2 + Spring + Hibernate!
- SSM：SpringMvc + Spring + Mybatis!

官网：[Spring Framework Documentation](https://docs.spring.io/spring-framework/docs/current/reference/html/)

GitHub：[Releases · spring-projects/spring-framework · GitHub](https://github.com/spring-projects/spring-framework/releases)

Spring Web MVC maven

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.3.9</version>
</dependency>
JDBC模块
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.3.9</version>
</dependency>

```

### 优点

- Spring是一个开源的免费的框架（容器）！
- Spring是一个轻量级的、非入侵式的框架！
- 控制反转（IOC），面向切面编程（AOP）
- 支持事务的处理，对框架整合的支持！

**总结：Spring就是一个轻量级的控制反转（IOC）和面向切面编程（AOP）的框架！**

### 组成

七大模块：

![](https://img-blog.csdnimg.cn/89f9546141644491bad22dc560c9e4b1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_17,color_FFFFFF,t_70,g_se,x_16)

### 拓展

Spring 的官网有介绍：现代化的Java开发！即基于Spring的开发

![](https://img-blog.csdnimg.cn/dfa8ca37c1ae47649240b71268108e6d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

- Spring Boot
  - 一个快速开发的脚手架
  - 基于SpringBoot可以快速开发单个微服务
  - 约定大于配置！
- Spring Cloud
  - SpringCloud 是基于SpringBoot实现的

学习SpringBoot的前提是需要掌握Spring及SpringMVC！承上启下！

弊端：发展太久后，违背原来理念！配置十分繁琐！

## IOC理论推导

原本开发步骤：

新建maven项目，删除src目录，导包

1. UserDao接口
2. UserDaoImpl实现类
3. UserService 业务接口
4. UserServiceImpl 业务实现类

在原来的业务中，用户得需求可能会影响我们原来得代码，我们需要根据用户得需求去修改源代码！如果程序代码量十分大，修改一次得成本十分昂贵

![](https://img-blog.csdnimg.cn/d5746e4c9f3d421cb78ed6e00d01af43.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_19,color_FFFFFF,t_70,g_se,x_16)

我们使用一个Set接口实现，已经发生了革命性得变化！

```java
package com.Sucker.Service;

import com.Sucker.dao.UserDao;
import com.Sucker.dao.UserDaoImpl;

public class UserServiceImpl implements UserService{

    private UserDao userDao;

    //利用set进行动态实现值得注入！
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void getUser() {
        userDao.getUser();
    }
}
```

```java
import com.Sucker.Service.UserService;
import com.Sucker.Service.UserServiceImpl;
import com.Sucker.dao.UserDaoImpl;
import com.Sucker.dao.UserDaoMysqlImpl;

public class MyTest {

    public static void main(String[] args) {

        //用户实际调用的是业务层，dao层他们不需要接触！
        UserService userService = new UserServiceImpl();
        
        //参数调整就可以调用不同
        ((UserServiceImpl) userService).setUserDao(new UserDaoMysqlImpl());
        userService.getUser();
    }

}
```

- 之前，程序是主动创建对象！控制权在程序员手中！
- 使用了set注入后，程序不再具有主动性，而是变成了被动得接收对象！

这种思想，从本质上解决了问题，程序员不再需要去管理对象得创建了。系统得耦合性大大降低了，可以更加专注于业务得实现上！这是 IOC 得原型！

![](https://img-blog.csdnimg.cn/cf7246bbbd5542368ef4eef9ceb4898b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### IOC本质
控制反转IoC（Inversion of Control），是一种设计思想，DI（依赖注入）是实现IoC的一种方法，也有人认为DI只是IoC的另一种说法。没有IoC的程序中，我们使用面向对象编程，对象的创建与对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制，控制反转后将对象的创建转移给第三方，个人认为所谓控制反转就是：获得依赖对象的方式反转了。

采用XML方式配置Bean的时候，Bean的定义信息是和实现分离的，而采用注解的方式可以把两者合为一体，Bean的定义信息直接以注解的形式定义在实现类中，从而达到了零配置的目的。
**控制反转是一种通过描述（XML或注解）并通过第三方去生产或获取特定对象的方式。在Spring中实现控制反转的是IoC容器，其实现方法是依赖注入（Dependency Injection，DI）。**

## HelloSpring

1. 新建一个maven项目，编写实体类

   ```java
   public class Hello {
       private String str;
   
       public String getStr() {
           return str;
       }
   
       public void setStr(String str) {
           this.str = str;
       }
   
       @Override
       public String toString() {
           return "Hello{" +
                   "str='" + str + '\'' +
                   '}';
       }
   }
   ```

2. 编写xml配置文件

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd">
   
   
       <!--使用Spring来创建对象，在Spring这些都称为Bean
       类型 变量名 = new 类型();
       Hello hello = new Hello();
   
       id = 变量名
       class = new的对象
       property 相当于给对象中的属性设置一个值！
           -->
       <bean id="hello" class="com.kuang.pojo.Hello">
           <property name="str" value="Spring"/>
       </bean>
   </beans>
   ```

3. 测试

   ```java
   import com.Sucker.pojo.Hello;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.support.ClassPathXmlApplicationContext;
   
   public class MyTest {
   
       public static void main(String[] args) {
           //获取Spring 的上下文对象
           ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
           //我们的对象现在都在Spring中管理，想要使用就直接在其中取即可
           Hello hello = (Hello) context.getBean("hello");
           System.out.println(hello.toString());
   
       }
   
   }
   ```

   其他小练习

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <bean id="mysqlImpl" class="com.Sucker.dao.UserDaoMysqlImpl"/>
       <bean id="orecalImpl" class="com.Sucker.dao.UserDaoOrecalImpl"/>
   
       <bean id="UserServiceImpl" class="com.Sucker.Service.UserServiceImpl">
           <property name="userDao" ref="mysqlImpl"/>
       </bean>
   
       <!--    ref:  引用Spring容器中创建好的对象
               value: 具体的值，基本数据类型！
       -->
   
   </beans>
   ```

   ```java
   import com.Sucker.Service.UserService;
   import com.Sucker.Service.UserServiceImpl;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.support.ClassPathXmlApplicationContext;
   
   public class MyTest {
   
       public static void main(String[] args) {
   
           //获取ApplicationContext； 拿到Spring的容器
           ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
   
           //需要什么直接 get
           UserServiceImpl userServiceImpl = (UserServiceImpl) context.getBean("UserServiceImpl");
   
           userServiceImpl.getUser();//更改xml配置文件即可实现不同的实现类调用
   
       }
   }
   ```



## IOC创建对象的方式

1. 使用无参构造创建对象，默认！

2. 假设想使用有参构造创建对象

   1. 下标赋值法

      ```xml
      <!--第一种：下标赋值法-->
      <bean id="user" class="com.Sucker.pojo.User">
          <!--        index = 0 给下标为0的第一个参数赋值-->
          <constructor-arg index="0" value="Sucker"/>
      </bean>
      ```

   2. 类型

      ```xml
      <!--    通过类型创建，不建议使用，只能一个参数-->
      <bean id="user" class="com.Sucker.pojo.User">
          <constructor-arg type="java.lang.String" value="Sucker"/>
      </bean>
      ```

   3. 直接通过参数名

      ```xml
      <bean id="user" class="com.Sucker.pojo.User">
          <constructor-arg name="name" value="Sucker"/>
      </bean>
      ```

      Assuming that the `ThingTwo` and `ThingThree` classes are not related by inheritance, no potential ambiguity exists. Thus, the following configuration works fine, and you do not need to specify the constructor argument indexes or types explicitly in the `<constructor-arg/>` element.

      ```xml
      <beans>
          <bean id="beanOne" class="x.y.ThingOne">
              <constructor-arg ref="beanTwo"/>
              <constructor-arg ref="beanThree"/>
          </bean>
      
          <bean id="beanTwo" class="x.y.ThingTwo"/>
      
          <bean id="beanThree" class="x.y.ThingThree"/>
      </beans>
      ```

      When another bean is referenced, the type is known, and matching can occur (as was the case with the preceding example). When a simple type is used, such as `<value>true</value>`, Spring cannot determine the type of the value, and so cannot match by type without help. Consider the following class:

总结：配置文件加载时，容器中管理的的对象就已经初始化了！

## Spring配置

### 别名

```xml
<!--别名，添加了别名，也可以使用别名获取到这个对象-->
<alias name="user" alias="ssssss"/>
```

### Bean的配置

```xml
<!--
    id: bean 的唯一标识符，也就是相当于我们学的对象名
    class : bean 对象所对应的全限定名 : 包名 + 类型
    name : 也是别名,而且name更高级，可以同时取多个别名
    -->
<bean id="user" class="com.Sucker.pojo.User" name="user2,u2 u3;u4">
    <property name="name" value="Sucker"/>
</bean>
```

### import

import，一般用于团队开发使用，他可以将多个配置文件导入合并成一个

假设现在有多个人进行开发，这三个人负责不同的类的开发，不同的类需要注册在不同的bean中，我们可以利用import将所有人的beans.xml合并为一个总的！

使用的时候直接使用总的配置就行（applicationContext.xml）

```xml
<import resource="beans.xml"/>
<import resource="beans1.xml"/>
<import resource="beans2.xml"/>
```

当导入的时候出现 id 相同的时候，相同 id 的相同内容会合并，不同的会根据后来居上覆盖

## DL依赖注入

### 构造器注入

参考IOC创建对象的方式

### Set方式注入【重点】

- 依赖注入：Set注入
  - 依赖：bean对象的创建依赖于容器
  - 注入：bean对象中的所有属性，由容器来注入！

【环境搭建】

1. 复杂类型

   ```java
   package com.Sucker.pojo;
   
   public class Address {
   
       private String address;
   
       public String getAddress() {
           return address;
       }
   
       public void setAddress(String address) {
           this.address = address;
       }
   }
   ```

2. 真实测试对象

   ```java
   public class Student {
   
       private String name;
       private Address address;
       private String[] books;
       private List<String> hobbies;
       private Map<String,String> card;
       private Set<String> games;
       private Properties info;
       private String wife;
   ```

3. beans.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <bean id="student" class="com.Sucker.pojo.Student">
           <!--第一种，普通值注入，value-->
           <property name="name" value="Sucker"/>
       </bean>
   
   </beans>
   ```

4. 测试类

   ```java
   public class MyTest {
   
       public static void main(String[] args) {
           ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
           Student student = (Student) context.getBean("student");
           System.out.println(student.getName());
       }
   }
   ```

5. 完善注入信息

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <bean id="address" class="com.Sucker.pojo.Address">
           <property name="address" value="湘潭"/>
       </bean>
   
       <bean id="student" class="com.Sucker.pojo.Student">
           <!--第一种，普通值注入，value-->
           <property name="name" value="Sucker"/>
   
           <!--第二种，Bean注入，ref-->
           <property name="address" ref="address"/>
   
           <!--数组-->
           <property name="books">
               <array>
                   <value>红楼梦</value>
                   <value>三国演义</value>
                   <value>水浒传</value>
               </array>
           </property>
   
           <!--list-->
           <property name="hobbies">
               <list>
                   <value>听歌</value>
                   <value>敲代码</value>
                   <value>看电影</value>
               </list>
           </property>
   
           <!--Map-->
           <property name="card">
               <map>
                   <entry key="身份证" value="1111111111111111"/>
                   <entry key="银行卡" value="1234141341414141"/>
               </map>
           </property>
   
           <!--Set-->
           <property name="games">
               <set>
                   <value>LOL</value>
                   <value>COC</value>
                   <value>BOB</value>
               </set>
           </property>
   
           <!--Null-->
   <!-- 第一种方式：<property name="wife" value=""/>-->
           <property name="wife">
               <null/>
           </property>
   
           <!--Properties-->
           <property name="info">
               <props>
                   <prop key="driver">20202019</prop>
                   <prop key="url">速速</prop>
                   <prop key="username">root</prop>
                   <prop key="password">123456</prop>
               </props>
           </property>
   
       </bean>
   
   </beans>
   ```

### 拓展方式注入

我们可以使用 p 命名空间和 c 命名空间进行注入

官方解释：

![](https://img-blog.csdnimg.cn/eb8622db929943dca645eed66b7a52e9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--p命名空间注入，可以直接注入属性得值：property-->
    <bean id="user" class="com.Sucker.pojo.User" p:name="suke" p:age="18"/>

    <!--c命名空间注入，通过构造器注入：construct-args-->
    <bean id="user2" class="com.Sucker.pojo.User" c:age="18" c:name="suss"/>

</beans>
```

```java
@Test
public void test2(){
    ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
    User user = context.getBean("user2", User.class);
    System.out.println(user);

}
```

注意点：p命名和c命名空间必须导入xml约束

```xml
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
```

### bean的作用域

| Scope                                                        | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [singleton](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-singleton) | (Default) Scopes a single bean definition to a single object instance for each Spring IoC container. |
| [prototype](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-prototype) | Scopes a single bean definition to any number of object instances. |
| [request](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-request) | Scopes a single bean definition to the lifecycle of a single HTTP request. That is, each HTTP request has its own instance of a bean created off the back of a single bean definition. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| [session](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-session) | Scopes a single bean definition to the lifecycle of an HTTP `Session`. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| [application](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-application) | Scopes a single bean definition to the lifecycle of a `ServletContext`. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| [websocket](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#websocket-stomp-websocket-scope) | Scopes a single bean definition to the lifecycle of a `WebSocket`. Only valid in the context of a web-aware Spring `ApplicationContext`. |

1. 单例模式（Spring的默认机制）

   ```xml
   <bean id="user2" class="com.Sucker.pojo.User" c:age="18" c:name="suss" scope="singleton"/>
   ```

   ![](https://img-blog.csdnimg.cn/8ef994f0e3cb42e7b3b744f75fbd7574.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

   ```java
   @Test
   public void test2(){
       ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
       User user = context.getBean("user2", User.class);
       User user2 = context.getBean("user2", User.class);
       System.out.println(user==user2);
   
   }
   //结果为true
   ```

2. 原型模式:每次从容器中get的时候，都会产生一个新对象

   ```xml
   <bean id="user2" class="com.Sucker.pojo.User" c:age="18" c:name="suss" scope="prototype"/>
   ```

   ![](https://img-blog.csdnimg.cn/1dad7e35fe8b4172ada738e7feeb3010.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

   ```java
   @Test
   public void test2(){
       ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
       User user = context.getBean("user2", User.class);
       User user2 = context.getBean("user2", User.class);
       System.out.println(user==user2);
   
   }
   //结果为false,两个对象不相等了
   ```

3. 其余的 request，session，application，这些只能在web开发中使用到！

## Bean的自动装配

- 自动装配是Spring满足bean依赖的一种方式！
- Spring会在上下文中自动寻找，并自动给bean装配属性！

在Spring中有三种装配的方式

1. 在xml中显式的配置
2. 在java中显式配置
3. 隐式的自动装配bean【重要】

### 测试

1. 环境搭建：一个人有两个宠物！

   ```xml
   <bean id="cat" class="com.Sucker.pojo.Cat"/>
   <bean id="dog" class="com.Sucker.pojo.Dog"/>
   
   <bean id="people" class="com.Sucker.pojo.People">
       <property name="name" value="sususu"/>
       <property name="dog" ref="dog"/>
       <property name="cat" ref="cat"/>
   </bean>
   ```

### ByName自动装配

```xml
<bean id="cat" class="com.Sucker.pojo.Cat"/>
<bean id="dog" class="com.Sucker.pojo.Dog"/>

<!--
    byName: 会自动在容器上下文中查找，和自己对象set方法后面的值对应的 beanid！
    注意是跟set方法后面的对应，会区分大小写，不是形参
    -->
<bean id="people" class="com.Sucker.pojo.People" autowire="byName">
    <property name="name" value="sususu"/>
</bean>
```

### ByType自动装配

```xml
<bean class="com.Sucker.pojo.Cat"/>
<bean id="dogfafa" class="com.Sucker.pojo.Dog"/>

<!--
    byName: 会自动在容器上下文中查找，和自己对象set方法后面的值对应的 beanid！
    注意是跟set方法后面的对应，会区分大小写，不是形参
    byName: 会自动在容器上下文中查找，和自己对象属性类型相同的 bean！
    id也可以不需要
    -->
<bean id="people" class="com.Sucker.pojo.People" autowire="byType">
    <property name="name" value="sususu"/>
</bean>
```

```java
@Test
public void test1(){
    ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
    People people = context.getBean("people", People.class);
    people.getCat().shout();
    people.getDog().shout();
}
```

小结：

- byName时，需要保证所有bean的 id 唯一，并且这个bean需要和自动注入的属性的set方法的值一致
- byType时，需要保证所有bean的 class 唯一，并且这个bean需要和自动注入的属性的类型一致

### 使用注解实现自动装配

The introduction of annotation-based configuration raised the question of whether this approach is “better” than XML

使用注解须知：

1. 导入约束：context 约束

2. **配置注解的支持：<context:annotation-config/>【重要】**

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           https://www.springframework.org/schema/context/spring-context.xsd">
   
       <context:annotation-config/>
   
   </beans>
   ```

**@Autowired**

直接在属性上使用即可！也可以在set方法上使用

使用Autowired 我们可以不用编写set方法，前提是这个自动装配的属性是在 IOC（Spring）容器中存在

遇到复杂情况时，先按照byType装配，若没找到则报错，多个再按byName装配，若对不上可以加@Qualifer(value=“xxx”)

科普：

```java
@Nullable  字段标记了这个注解，说明这个字段可以为null
```

```java
public @interface Autowired {
    boolean required() default true;
}
```

测试代码：

```java
package com.Sucker.pojo;

import org.springframework.beans.factory.annotation.Autowired;

public class People {
    //如果显式的定义了Autowired的required 属性为false，说明这个对象可以为null，否则不允许为空
    @Autowired(required = false)
    private Dog dog;
    @Autowired
    private Cat cat;
    private String name;

    public Dog getDog() {
        return dog;
    }

    public Cat getCat() {
        return cat;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "People{" +
                "dog=" + dog +
                ", cat=" + cat +
                ", name='" + name + '\'' +
                '}';
    }
}
```

如果@Autowired自动装配的环境比较复杂，自动装配无法通过一个注解【@Autowired】完成的时候，我们可以使用@Qualifier(value="xxx")去配置@Autowired的使用，指定一个唯一的bean对象

```java
public class People {
    @Autowired
    @Qualifier(value = "dog111")
    private Dog dog;
    @Autowired
    private Cat cat;
    private String name;
```

```xml
<bean id="cat" class="com.Sucker.pojo.Cat"/>
<bean id="dog" class="com.Sucker.pojo.Dog"/>
<bean id="dog111" class="com.Sucker.pojo.Dog"/>
<bean id="people" class="com.Sucker.pojo.People"/>
```

**@Resource注解**【JKD11已移除】

```java
public class People {
    @Resource(name = "dog2")
    private Dog dog;
    @Resource
    private Cat cat;
    private String name;
}
```

小结：

@Resource 和 @Autowired的区别：

- 都是用来自动装配的，都可以用在属性字段上
- @Autowired 默认通过byType的方式，当匹配到多个同类型时，使用byName进行装配，必须保证这个对象存在，可以使用@Qualifier(value="xxx")
- @Resource 也是先类型后名字

## 使用注解开发

Spring4之后，要使用注解开发，必须保证 aop 的包导入了

![](https://img-blog.csdnimg.cn/7f975718fbe743f2a62976554686906d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_18,color_FFFFFF,t_70,g_se,x_16)

使用注解需要导入context约束，增加注解的支持

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>
    
</beans>
```

@Component：组件，放在类上，说明这个类被Spring管理了，就是bean！

1. bean

   ```xml
   <!--指定要扫描的包，这个包下的注解就会生效-->
   <context:component-scan base-package="com.Sucker"/>
   <context:annotation-config/>这个是注解配置
   ```

   

2. 属性如何注入

   ```java
   //等价于 <bean id="user" class="com.Sucker.pojo.User"/>
   //@Component  组件
   @Component
   public class User {
   
       //相当于 <property name="name" value="kuangshen"/>
       @Value("Sucker")
       public String name;
       //也可以放到set方法上
   
   }
   
   ```

3. 衍生的注解

   @Component 有几个衍生注解，我们在web开发中，会按照MVC三层架构分层！

   - dao 【@Repository】
   - service【@Service】
   - controller【@Controller】

   这四个注解功能都是一样的，都是代表将某个类注册到Spring中，装配Bean

4. 自动装配机制

   ```xml
   - @Autowired：自动装配通过类型，名字。如果Autowired不能唯一自动装配上属性，则需要通过@Qualifier(value = "xxx")去配置。
   - @Nullable 字段标记了了这个注解，说明这个字段可以为null;
   - @Resource：自动装配通过名字，类型。
   ```

5. 作用域

   ```java
   @Component
   @Scope("prototype")
   public class User {
   
       //相当于 <property name="name" value="kuangshen"/>
       @Value("Sucker")
       public String name;
   
   }
   ```

6. 小结

   xml 与 注解：

   - xml 更加万能，适用于任何场合！维护更加简单方便
   - 注解 不是自己类不能使用，维护相对复杂

   xml 与 注解最佳实践：

   - xml 用来管理bean

   - 注解只负责完成属性的注入

   - 我们在使用的过程中，只需要注意：必须让注解生效，就需要开启注解支持

     ```xml
     <!--指定要扫描的包，这个包下的注解就会生效-->
     <context:component-scan base-package="com.Sucker"/>
     <context:annotation-config/>
     ```

## 使用Java的方式配置Spring

我们现在尝试完全不适用Spring的xml配置，全权交给Java来做！新特性

JavaConfig 是 Spring 的一个子项目，在Spring4之后，它成为了一个核心功能！

![](https://img-blog.csdnimg.cn/85c1f7925a0b4fed9355c83599a26501.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
package com.Sucker.config;
//这个也会被Spring容器托管，注册到容器中，因为它本来就是一个@Component
//@Configuration代表这是一个配置类，与我们之前看到的beans.xml相同
@Configuration
@Import(SuckerCoinfig2.class)
public class SuckerConfig {

    //注册一个bean，就相当于我们之前写的一个bean标签
    //这个方法的名字，就相当于bean标签中的id属性
    //这个方法的返回值，就相当于bean标签中的class属性
    @Bean
    public User getUser(){
        return new User();
    }

}
```

```java
import com.Sucker.config.SuckerConfig;
import com.Sucker.pojo.User;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class MyTest {

    public static void main(String[] args) {
        //注解配置类
        //如果完全使用了配置类方式去做，我们就只能通过 AnnotationConfig 上下文来获取容器，通过配置类的class对象加载！
        ApplicationContext context = new AnnotationConfigApplicationContext(SuckerConfig.class);
        User getUser = context.getBean("getUser", User.class);
        System.out.println(getUser.getName());
    }
}
```

这种纯Java的配置方式，在SpringBoot中随处可见！

## 代理模式

为什么要学习代理模式？因为这就是SpringAOP的底层！【SpringAOP 和 SpringMVC】

代理模式的分类：

- 静态代理
- 动态代理

![](https://img-blog.csdnimg.cn/20201112093129742.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpNjQzOTM3NTc5,size_16,color_FFFFFF,t_70#pic_center)

### 静态代理

角色分析：

- 抽象角色：一般会使用接口或者抽象类来解决
- 真实角色：被代理的角色
- 代理角色：代理真实角色，代理真实角色后，我们一般会做一些附属操作
- 客户：访问代理对象的人！

代码步骤：

1. 接口

   ```java
   //租房
   public interface Rent {
       public void rent();
   }
   ```

2. 真实角色

   ```java
   //房东
   public class Host implements Rent{
       @Override
       public void rent() {
           System.out.println("房东要出租房子");
       }
   }
   ```

3. 代理角色

   ```java
   //代理
   public class Proxy implements Rent{
   
       private Host host;
   
       public Proxy() {
       }
   
       public Proxy(Host host) {
           this.host = host;
       }
   
       @Override
       public void rent() {
           seeHouse();
           host.rent();
           hetong();
           fare();
       }
   
       //看房
       public void seeHouse(){
           System.out.println("中介带你看房");
       }
       //收中介费
       public void fare(){
           System.out.println("收中介费");
       }
   
       //签合同
       public void hetong(){
           System.out.println("签合同");
       }
   
   }
   ```

4. 客户端访问代理角色

   ```java
   public class Client {
       public static void main(String[] args) {
           //房东要出租房子
           Host host = new Host();
           //代理,中介帮房东出租房子，代理角色一般会有一些附属操作！
           Proxy proxy = new Proxy(host);
   
           //你直接找中介租房即可！
           proxy.rent();
       }
   }
   ```

代理模式的好处：

- 可以使真实角色的操作更加纯粹！不用去关注一些公共的业务
- 公共也就交给代理角色！实现了业务的分工！
- 公共业务发生扩展时，方便集中管理！

缺点：

- 一个真实角色就会产生一个代理角色！代码量翻倍--开发效率变低~

### 加深理解

例子：

接口：

```java
public interface UserService {
    public void add();
    public void delete();
    public void update();
    public void query();

}
```

真实对象：

```java
//真实对象
public class UserServiceImpl implements UserService{
    @Override
    public void add() {
        System.out.println("增加了一个用户");
    }

    @Override
    public void delete() {
        System.out.println("删除了一个用户");
    }

    @Override
    public void update() {
        System.out.println("修改了一个用户");
    }

    @Override
    public void query() {
        System.out.println("查询了一个用户");
    }
}
```

代理对象：

```java
public class UserServiceProxy implements UserService{

    private UserServiceImpl userService;

    public void setUserService(UserServiceImpl userService) {
        this.userService = userService;
    }

    @Override
    public void add() {
        log("add");
        userService.add();
    }

    @Override
    public void delete() {
        log("delete");
        userService.delete();
    }

    @Override
    public void update() {
        log("update");
        userService.update();
    }

    @Override
    public void query() {
        log("query");
        userService.query();
    }

    //日志方法
    public void log(String msg){
        System.out.println("使用了"+msg+"方法");
    }
}
```

客户端访问代理对象

```java
public class Client {
    public static void main(String[] args) {
        UserServiceImpl userService = new UserServiceImpl();

        UserServiceProxy proxy = new UserServiceProxy();
        proxy.setUserService(userService);
        proxy.add();

    }
}
```



AOP：

![](https://img-blog.csdnimg.cn/655ad17d478344dd953b3a50e2d54155.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)



### 动态代理

- 动态代理和静态代理角色一样
- 动态代理的代理类是动态生成的，不是我们直接写好的！
- 动态代理分为两大类：基于接口的动态代理，基于类的动态代理
  - 基于接口--JDK 动态代理 【我们在这里使用】
  - 基于类-- cglib
  - java字节码实现：javasist

需要了解两个类：Proxy：代理，InvocationHandler：调用处理程序

**InvocationHandler**

是个接口，reflect包下

**动态代理的好处：**

- 可以使真实角色的操作更加纯粹！不用去关注一些公共的业务
- 公共的业务就交给代理角色！实现了业务的分工
- 公共业务发生拓展时，方便集中管理！
- 一个动态代理类代理的是一个接口，一般就是对应的一类业务
- 一个动态代理类可以代理多个类，只要是实现了同一个接口即可！

代码步骤：

接口：

```java
//租房
public interface Rent {
    public void rent();
}
```

真实角色：

```java
//房东
public class Host implements Rent {
    @Override
    public void rent() {
        System.out.println("房东要出租房子");
    }
}
```

ProxyInvocationHandler类

```java
package com.Sucker.demo03;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

//使用这个类自动生成代理类!
public class ProxyInvocationHandler implements InvocationHandler {

    //被代理的接口
    private Rent rent;

    public void setRent(Rent rent) {
        this.rent = rent;
    }

    //生成得到代理类
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),rent.getClass().getInterfaces(),this );
    }

    //处理代理实例，并返回结果
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        seeHouse();
        //动态代理的本质，就是使用反射机制实现！
        Object result = method.invoke(rent, args);
        fare();
        return null;
    }

    public void seeHouse(){
        System.out.println("kanfangzi");
    }

    public void fare(){
        System.out.println("受中介费");
    }

}
```

测试类

```java
package com.Sucker.demo03;
public class Client {
    public static void main(String[] args) {
        //真实角色
        Host host = new Host();

        //代理角色：现在没有
        ProxyInvocationHandler pih = new ProxyInvocationHandler();
        //通过调用程序处理角色来处理我们要调用的接口对象！
        pih.setRent(host);
        Rent proxy = (Rent) pih.getProxy();//这里的proxy就是动态生成的，我们并没有去写
        proxy.rent();
    }
}
```

提取工具类

```java
//使用这个类自动生成代理类!
public class ProxyInvocationHandler implements InvocationHandler {

    //被代理的接口
    private Object target;

    public void setTarget(Object target) {
        this.target = target;
    }

    //生成得到代理类
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),target.getClass().getInterfaces(),this );
    }

    //处理代理实例，并返回结果
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        log(method.getName());
        Object result = method.invoke(target, args);
        return null;
    }

    public void log(String msg){
        System.out.println("执行了"+msg+"方法");
    }

}
```

测试类

```java
package com.Sucker.demo04;

import com.Sucker.demo02.UserService;
import com.Sucker.demo02.UserServiceImpl;

public class Client {
    public static void main(String[] args) {
        //真实角色
        UserServiceImpl userService = new UserServiceImpl();
        //代理角色，不存在
        ProxyInvocationHandler pih = new ProxyInvocationHandler();
        pih.setTarget(userService);//设置要代理的对象
        //动态生成代理类
        UserService proxy = (UserService) pih.getProxy();
        proxy.add();
    }
}
```

## AOP

### 什么是AOP

AOP（Aspect Oriented Programming）意为：面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

![](https://img-blog.csdnimg.cn/05c2a2f6aa7a4d54b4c2a1b62dfb07b3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

### AOP在Spring中的作用
提供声明式事务；允许用户自定义切面

- 横切关注点：跨越应用程序多个模块的方法或功能。即是，与我们业务逻辑无关的，但是我们需要关注的部分，就是横切关注点。如日志，安全，缓存，事务等等…
- 切面（ASPECT）：横切关注点被模块化的特殊对象。即，它是一个类。
- 通知（Advice）：切面必须要完成的工作。即，它是类中的一个方法。
- 目标（Target）：被通知对象。
- 代理（Proxy）：向目标对象应用通知之后创建的对象。
- 切入点（PointCut）：切面通知执行的“地点”的定义。
- 连接点（JointPoint）：与切入点匹配的执行点。

![](https://img-blog.csdnimg.cn/79c6a0bb2bd84c5e87965309773d489f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

SpringAOP中，通过Advice定义横切逻辑，Spring中支持5种类型的Advice：

![](https://img-blog.csdnimg.cn/8dcde749a16449c89e92902634455fe2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_12,color_FFFFFF,t_70,g_se,x_16)

![](https://img-blog.csdnimg.cn/5cb4867264c44beb9f3c1e4e4f193e51.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU3Vja2VyX-iLjw==,size_20,color_FFFFFF,t_70,g_se,x_16)

即AOP在不改变原有代码的情况下，去增加新的功能。

### 使用Spring实现AOP

【重点】使用AOP织入，需要导入一个依赖包！

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.7</version>
</dependency>
```



#### 方式一：使用Spring的 API 接口【主要SpringAPI接口实现】

1. 在Service包下，定义UserService业务接口和UserServiceImpl实现类

   ```java
   package com.Sucker.Service;
   
   public interface UserService {
       public void add();
       public void delete();
       public void update();
       public void select();
   }
   ```

   ```java
   package com.Sucker.Service;
   public class UserServiceImpl implements UserService{
       public void add() {
           System.out.println("增加了一个用户");
       }
   
       public void delete() {
           System.out.println("删除了一个用户");
       }
   
       public void update() {
           System.out.println("修改了一个用户");
       }
   
       public void select() {
           System.out.println("查找了一个用户");
       }
   }
   ```

2. 在log包下，定义我们的增强类，一个Log前置增强和一个AfterLog后置增强类

   ```java
   package com.Sucker.log;
   import org.springframework.aop.MethodBeforeAdvice;
   import java.lang.reflect.Method;
   public class Log implements MethodBeforeAdvice {
   
       //method : 要执行的目标对象的方法
       //args : 参数
       //target : 目标对象
       public void before(Method method, Object[] args, Object target) throws Throwable {
           System.out.println(target.getClass().getName()+"的"+method.getName()+"被执行了");
       }
   }
   ```

   ```java
   package com.Sucker.log;
   import org.springframework.aop.AfterReturningAdvice;
   import java.lang.reflect.Method;
   public class AfterLog implements AfterReturningAdvice {
       //returnValue : 返回值
       public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
           System.out.println("执行了"+method.getName()+"返回结果为:"+returnValue);
       }
   }
   ```

3. 最后去spring的文件中注册 , 并实现aop切入实现 , 注意导入约束，配置applicationContext.xml文件

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/aop
          http://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <!--注册bean，可以用注解，但这里用原生的-->
       <bean id="userService" class="com.Sucker.Service.UserServiceImpl"/>
       <bean id="log" class="com.Sucker.log.Log"/>
       <bean id="afterLog" class="com.Sucker.log.AfterLog"/>
   
       <!--方式一：使用原生Spring API接口-->
       <!--配置AOP:需要导入AOP的约束-->
       <aop:config>
           <!--切入点：poingcut  expression：表达式 execution(要执行的位置)-->
           <aop:pointcut id="pointcut" expression="execution(* com.Sucker.Service.UserServiceImpl.*(..))"/>
   
           <!-- 执行环绕增加-->
           <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
           <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
   
       </aop:config>
   
   </beans>
   ```

4. 测试

   ```java
   import com.Sucker.Service.UserService;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.support.ClassPathXmlApplicationContext;
   public class MyTest {
       public static void main(String[] args) {
           ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
           //动态代理的是接口
           UserService userService = context.getBean("userService", UserService.class);
           userService.add();
       }
   }
   ```

#### 方式二：自定义来实现AOP【主要是切面定义】

execution表达式参考：[(29条消息) AOP(execution表达式)_somilong的博客-CSDN博客_aop表达式](https://blog.csdn.net/somilong/article/details/74568223)

1. 在diy包下定义自己的DiyPointCut切入类

   ```java
   package com.Sucker.diy;
   public class DiyPointCut {
   
       public void before(){
           System.out.println("=========方法执行前========");
       }
       public void after(){
           System.out.println("=========方法执行后========");
       }
   }
   ```

2. 去spring中配置文件

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/aop
          http://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <!--注册bean，可以用注解，但这里用原生的-->
       <bean id="userService" class="com.Sucker.Service.UserServiceImpl"/>
       <bean id="log" class="com.Sucker.log.Log"/>
       <bean id="afterLog" class="com.Sucker.log.AfterLog"/>
   
       <!--方式二：自定义类-->
       <bean id="diy" class="com.Sucker.diy.DiyPointCut"/>
   
       <aop:config>
           <!--自定义切面，ref：要引用的类-->
           <aop:aspect ref="diy">
               <!--切入点-->
               <aop:pointcut id="pointcut" expression="execution(* com.Sucker.Service.UserServiceImpl.*(..))"/>
               <!--通知-->
               <aop:before method="before" pointcut-ref="pointcut"/>
               <aop:after method="after" pointcut-ref="pointcut"/>
           </aop:aspect>
       </aop:config>
   
   </beans>
   ```

3. 测试

#### 方式三：使用注解实现！

1. 在diy包下定义注解实现的AnnotationPointCut增强类

   ```java
   package com.Sucker.diy;
   
   import org.aspectj.lang.ProceedingJoinPoint;
   import org.aspectj.lang.Signature;
   import org.aspectj.lang.annotation.*;
   
   //方式三：使用注解方式实现AOP
   @Aspect//标注这个类是一个切面
   public class AnnotationPointCut {
   
       @Before("execution(* com.Sucker.Service.UserServiceImpl.*(..))")
       public void before(){
           System.out.println("====方法执行前====");
       }
   
       @After("execution(* com.Sucker.Service.UserServiceImpl.*(..))")
       public void after(){
           System.out.println("====方法执行后====");
       }
   
       //在环绕增强中，我们可以给定一个参数，表示我们要获取切入的点
       @Around("execution(* com.Sucker.Service.UserServiceImpl.*(..))")
       public void around(ProceedingJoinPoint jp) throws Throwable {
           System.out.println("环绕前");
           Signature signature = jp.getSignature();//获得签名
           System.out.println("signature:"+signature);
           Object proceed = jp.proceed();//执行方法
           System.out.println("环绕后");
           System.out.println(proceed);
       }
   
   }
   ```

2. 在Spring配置文件中，注册bean，并增加支持注解的配置

   ```xml
   <!--方式三-->
       <bean id="annotationPointCut" class="com.Sucker.diy.AnnotationPointCut"/>
           <!--开启注解支持！-->
       <aop:aspectj-autoproxy/>
   ```

3. 测试

   ```java
   import com.Sucker.Service.UserService;
   import com.Sucker.Service.UserServiceImpl;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.support.ClassPathXmlApplicationContext;
   
   public class MyTest {
       public static void main(String[] args) {
           ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
           //动态代理的是接口
           UserService userService = context.getBean("userService", UserService.class);
           userService.add();
       }
   }
   /*
   环绕前
   signature:void com.Sucker.Service.UserService.add()
   ====方法执行前====
   增加了一个用户
   ====方法执行后====
   环绕后
   null
   */
   ```



## 整合Mybatis

步骤：

1. 导入相关jar包

   - junit

   - mybatis

   - mysql数据库

   - spring相关

   - aop织入

   - mybatis-spring【new】

     注意这里mybatis的包不能用高版本，否则没有resource包，3.4.4即可

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
       <parent>
           <artifactId>spring-study</artifactId>
           <groupId>com.Sucker</groupId>
           <version>1.0-SNAPSHOT</version>
       </parent>
       <modelVersion>4.0.0</modelVersion>
   
       <artifactId>spring-10-mybatis</artifactId>
   
       <dependencies>
   
           <dependency>
               <groupId>junit</groupId>
               <artifactId>junit</artifactId>
               <version>4.13</version>
           </dependency>
   
           <dependency>
               <groupId>mysql</groupId>
               <artifactId>mysql-connector-java</artifactId>
               <version>5.1.47</version>
           </dependency>
   
           <dependency>
               <groupId>org.mybatis</groupId>
               <artifactId>mybatis</artifactId>
               <version>3.4.4</version>
           </dependency>
   
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-webmvc</artifactId>
               <version>5.3.9</version>
           </dependency>
   
           <!--Spring操作数据库，还需要一个Spring-jdbc的包-->
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-jdbc</artifactId>
               <version>5.3.9</version>
           </dependency>
   
           <dependency>
               <groupId>org.aspectj</groupId>
               <artifactId>aspectjweaver</artifactId>
               <version>1.9.7</version>
           </dependency>
   
           <dependency>
               <groupId>org.mybatis</groupId>
               <artifactId>mybatis-spring</artifactId>
               <version>2.0.6</version>
           </dependency>
           
           <dependency>
               <groupId>org.projectlombok</groupId>
               <artifactId>lombok</artifactId>
               <version>1.18.20</version>
           </dependency>
   
       </dependencies>
       
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
   
   </project>
   ```

2. 编写配置文件

3. 测试

### 回忆mybatis

1. 编写实体类
2. 编写核心配置文件
3. 编写接口
4. 编写Mapper.xml
5. 测试

1. 编写pojo实体类

   ```java
   package com.Sucker.pojo;
   import lombok.Data;
   @Data
   public class User {
   
       private int id;
       private String name;
       private String pwd;
   }
   ```

2. 编写实现mybatis的配置文件

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE configuration
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">
   <configuration>
   
       <!--起别名-->
       <typeAliases>
           <package name="com.Sucker.pojo"/>
       </typeAliases>
   
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
   
       <mappers>
           <!--class方式可以偷懒,如果要注解等都生效需要UserMapper接口和xml在同一个包下且同名-->
           <mapper class="com.Sucker.mapper.UserMapper"/>
       </mappers>
   
   </configuration>
   ```

3. 编写UserMapper接口

   ```java
   public interface UserMapper {
       public List<User> selectUser();
   }
   ```

4. 编写UserMapper.xml文件

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.Sucker.mapper.UserMapper">
       
       <select id="selectUser" resultType="user">
           select * from mybatis.user
       </select>
   
   </mapper>
   ```

5. 测试

   ```java
   import com.Sucker.mapper.UserMapper;
   import com.Sucker.pojo.User;
   import org.apache.ibatis.session.SqlSession;
   import org.apache.ibatis.session.SqlSessionFactory;
   import org.apache.ibatis.session.SqlSessionFactoryBuilder;
   import org.junit.Test;
   import org.apache.ibatis.io.Resources;
   
   import java.io.IOException;
   import java.io.InputStream;
   import java.util.List;
   
   public class MyTest {
   
       @Test
       public void test() throws IOException {
           //没有工具类，手动实现
           String resources = "mybatis-config.xml";
           InputStream in = Resources.getResourceAsStream(resources);
           SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(in);
           SqlSession sqlSession = sessionFactory.openSession(true);//true表示自动提交事务
   
           UserMapper mapper = sqlSession.getMapper(UserMapper.class);
           List<User> userList = mapper.selectUser();
   
           for (User user : userList) {
               System.out.println(user);
           }
       }
   }
   ```

### Mybatis-Spring

**什么是MyBatis-Spring？**

MyBatis-Spring 会帮助你将 MyBatis 代码无缝地整合到 Spring 中。

文档链接：http://mybatis.org/spring/zh/index.html

如果使用 Maven 作为构建工具，仅需要在 pom.xml 中加入以下代码即可：

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>2.0.2</version>
</dependency>
```

**整合实现一：**

1. 引入Spring配置文件spring-dao.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
   </beans>
   ```

2. 配置数据源替换mybaits的数据源

   ```xml
       <!--DataSource:使用Spring的数据源替换Mybatis的配置  c3p0 dbcp druid
       这里使用Spring提供的JDBC : org.springframework.jdbc.datasource.DriverManagerDataSource
       -->
       <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
           <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
           <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
           <property name="username" value="root"/>
           <property name="password" value="123456"/>
       </bean>
   ```

3. 配置SqlSessionFactory，关联MyBatis

   ```xml
       <!--sqlSessionFactory-->
       <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
           <property name="dataSource" ref="dataSource"/>
           <!--绑定Mybatis配置文件-->
           <property name="configLocation" value="classpath:mybatis-config.xml"/>
           <property name="mapperLocations" value="classpath:com/Sucker/mapper/*.xml"/>
       </bean>
   ```

4. 注册sqlSessionTemplate，关联sqlSessionFactory

   ```xml
       <!--org.mybatis.spring.SqlSessionTemplate : 就是我们使用的sqlSession-->
       <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
           <!--只能使用构造器注入sqlSessionFactory 因为它没有set方法-->
           <constructor-arg index="0" ref="sqlSessionFactory"/>
       </bean>
   ```

5. 需要UserMapper接口的UserMapperImpl 实现类，私有化sqlSessionTemplate

   ```java
   package com.Sucker.mapper;
   
   import com.Sucker.pojo.User;
   import org.mybatis.spring.SqlSessionTemplate;
   
   import java.util.List;
   
   public class UserMapperImpl implements UserMapper{
   
       //我们所有的操作，原来都使用sqlSession来执行，现在我们都使用sqlSessionTemplate;
       private SqlSessionTemplate sqlSession;
   
       public void setSqlSession(SqlSessionTemplate sqlSession) {
           this.sqlSession = sqlSession;
       }
   
       public List<User> selectUser() {
           UserMapper mapper = sqlSession.getMapper(UserMapper.class);
           return mapper.selectUser();
       }
   }
   ```

6. 将自己写的实现类，注入到Spring配置文件中。

   ```xml
   	<bean id="userMapper" class="com.Sucker.mapper.UserMapperImpl">
           <property name="sqlSession" ref="sqlSession"/>
       </bean>
   ```

7. 测试使用即可！

   ```java
   public class MyTest {
       @Test
       public void test() throws IOException {
   
           ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
   
           UserMapper userMapper = context.getBean("userMapper", UserMapper.class);
           for (User user : userMapper.selectUser()) {
               System.out.println(user);
           }
   
       }
   }
   ```

结果成功输出！现在我们的Mybatis配置文件的状态！发现都可以被Spring整合！

现在mybatis-config.xml只剩起别名

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <!--起别名-->
    <typeAliases>
        <package name="com.Sucker.pojo"/>
    </typeAliases>

</configuration>
```

再将注册bean的功能放入applicationContext.xml中，在其中import  spring-dao.xml，将spring-dao.xml 配置成类似模板

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <import resource="spring-dao.xml"/>

    <bean id="userMapper" class="com.Sucker.mapper.UserMapperImpl">
        <property name="sqlSession" ref="sqlSession"/>
    </bean>

</beans>
```

**整合实现二：**

mybatis-spring1.2.3版以上的才有这个，官方文档截图：

dao继承Support类 , 直接利用 getSqlSession() 获得 , 然后直接注入SqlSessionFactory . 比起整合方式一 , 不需要管理SqlSessionTemplate , 而且对事务的支持更加友好 . 可跟踪源码查看。

![](https://img-blog.csdnimg.cn/20201122213331963.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpNjQzOTM3NTc5,size_16,color_FFFFFF,t_70#pic_center)

测试：

1. UserMapperImpl2

   ```java
   import java.util.List;
   public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper{
       public List<User> selectUser() {
           return getSqlSession().getMapper(UserMapper.class).selectUser();
       }
   }
   ```

2. 注入到Spring配置文件中

   ```xml
       <bean id="userMapper2" class="com.Sucker.mapper.UserMapperImpl2">
           <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
       </bean>
   ```

3. 测试

## 声明式事务

### 回顾事务

- 把一组业务当成一个业务来做；要么都成功，要么都失败！
- 事务在项目开发中，十分的重要！涉及到数据的一致性问题！
- 确保完整性和一致性；

**事务ACID原则：**

- 原子性
- 一致性
- 隔离性
  - 多个业务可能操作同一个资源，防止数据损坏
- 持久性
  - 事务一旦提交，无论系统发生什么问题，结果都不会再被影响，被持久化的写到存储器中！

**测试：**

将上面的代码拷贝到一个新项目中
在之前的案例中，我们给userMapper接口新增两个方法，删除和增加用户；

```java
    //添加一个用户
    public int addUser(User user);

    //删除一个用户
    public int deleteUser(int id);
```

UserMapper文件，我们故意把 deletes 写错，测试！

```xml
<insert id="addUser" parameterType="user">
    insert into mybatis.user (id, name, pwd) values(#{id},#{name},#{pwd});
</insert>

<delete id="deleteUser" parameterType="_int">
    deletes from mybatis.user where id=#{id}
</delete>
```

编写接口的UserMapperImpl实现类，在实现类中，我们去操作一波

```java
package com.Sucker.mapper;

import com.Sucker.pojo.User;
import org.mybatis.spring.support.SqlSessionDaoSupport;

import java.util.List;

public class UserMapperImpl extends SqlSessionDaoSupport implements UserMapper{

    public List<User> selectUser() {

        User user = new User(6,"小王","232322");

        UserMapper mapper = getSqlSession().getMapper(UserMapper.class);

        mapper.addUser(user);
        mapper.deleteUser(5);

        return mapper.selectUser();
    }

    public int addUser(User user) {
        return getSqlSession().getMapper(UserMapper.class).addUser(user);
    }

    public int deleteUser(int id) {
        return getSqlSession().getMapper(UserMapper.class).deleteUser(id);
    }
}
```

测试

```java
import com.Sucker.mapper.UserMapper;
import com.Sucker.pojo.User;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import java.util.List;

public class MyTest {

    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserMapper userMapper = context.getBean("userMapper", UserMapper.class);
        List<User> userList = userMapper.selectUser();
        for (User user : userList) {
            System.out.println(user);
        }
    }
}
```

报错：sql异常，delete写错了

结果 ：数据库结果显示插入成功！

没有进行事务的管理；我们想让他们都成功才成功，有一个失败，就都失败，我们就应该需要事务！

以前我们都需要自己手动管理事务，十分麻烦！

但是Spring给我们提供了事务管理，我们只需要配置即可；

### Spring中的事务管理

- 声明式事务：AOP
  - 一般情况下比编程式事务好用。
  - 将事务管理代码从业务方法中分离出来，以声明的方式来实现事务管理。
  - 将事务管理作为横切关注点，通过aop方法模块化。Spring中通过Spring AOP框架支持声明式事务管理。
- 编程式事务：需要在代码中，进行事务的管理
  - 将事务管理代码嵌到业务方法中来控制事务的提交和回滚
  - 缺点：必须在每个事务操作业务逻辑中包含额外的事务管理代码

Spring在不同的事务管理API之上定义了一个抽象层，使得开发人员不必了解底层的事务管理API就可以使用Spring的事务管理机制。Spring支持编程式事务管理和声明式的事务管理。

**1. 使用Spring管理事务，注意头文件的约束导入 : tx**

```xml
xmlns:tx="http://www.springframework.org/schema/tx"

http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd">
```

**2. JDBC事务**

```xml
    <!--配置声明式事务-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>
```

**3. 配置好事务管理器后我们需要去配置事务的通知**

```xml
    <!--结合AOP实现事务的织入-->
    <!--配置事务通知-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <!--给哪些方法配置事务-->
        <!--配置事务的传播特性：propagation="REQUIRED" 默认是这个-->
        <tx:attributes>
            <tx:method name="add" propagation="REQUIRED"/>
            <tx:method name="delete" propagation="REQUIRED"/>
            <tx:method name="update" propagation="REQUIRED"/>
            <tx:method name="query" read-only="true"/>
            <tx:method name="*" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>
```

spring事务传播特性：
事务传播行为就是多个事务方法相互调用时，事务如何在这些方法间传播。spring支持7种事务传播行为：

propagation_requierd：如果当前没有事务，就新建一个事务，如果已存在一个事务中，加入到这个事务中，这是最常见的选择。
propagation_supports：支持当前事务，如果没有当前事务，就以非事务方法执行。
propagation_mandatory：使用当前事务，如果没有当前事务，就抛出异常。
propagation_required_new：新建事务，如果当前存在事务，把当前事务挂起。
propagation_not_supported：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。
propagation_never：以非事务方式执行操作，如果当前事务存在则抛出异常。
propagation_nested：如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行与propagation_required类似的操作。
Spring 默认的事务传播行为是 PROPAGATION_REQUIRED，它适合于绝大多数的情况。

就好比，我们刚才的几个方法存在调用，所以会被放在一组事务当中！

**4. 配置AOP，导入aop的头文件**

```xml
    <!--配置事务的切入点-->
    <aop:config>
        <aop:pointcut id="txPointCut" expression="execution(* com.Sucker.mapper.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
    </aop:config>
```

**5. 删掉刚才插入的数据，再次测试！**

```java
    @Test
    public void test(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");

        UserMapper userMapper = context.getBean("userMapper", UserMapper.class);

        for (User user : userMapper.selectUser()) {
            System.out.println(user);
        }
    }
```

其他方式参考官方文档