## JVM体系结构

![](https://img-blog.csdnimg.cn/e89489c69d8b490197d55965b275ae13.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

## 类加载器

作用：加载 Class 文件

new 出的实例存在堆中，在栈中引用

![](https://img-blog.csdnimg.cn/c71d8db06b924775b01252d52a5b2d94.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

1. 虚拟机自带的加载器
2. 启动类 (根) 加载器
3. 拓展类加载器
4. 应用程序（系统类）加载器  （自底向上）

```java
public class Car {

    public int age;

    public static void main(String[] args) {
        // 类是模板，对象是具体的

        Car car1 = new Car();
        Car car2 = new Car();
        Car car3 = new Car();

        System.out.println(car1.hashCode());
        System.out.println(car2.hashCode());
        System.out.println(car3.hashCode());

        Class<? extends Car> aClass1 = car1.getClass();

        ClassLoader classLoader = aClass1.getClassLoader(); // AppClassLoader
        System.out.println(classLoader);
        System.out.println(classLoader.getParent()); // ExtClassLoader 扩展类加载器
        System.out.println(classLoader.getParent().getParent());// null 1.不存在  2.java程序获取不到


    }

}
```

## 双亲委派机制

原文链接：https://blog.csdn.net/codeyanbao/article/details/82875064

在介绍双亲委派机制的时候，不得不提ClassLoader（类加载器）。说ClassLoader之前，我们得先了解下Java的基本知识。

Java是运行在Java的虚拟机(JVM)中的，但是它是如何运行在JVM中了呢？我们在IDE中编写的Java源代码被编译器编译成.class的字节码文件。然后由我们得ClassLoader负责将这些class文件给加载到JVM中去执行。  

JVM中提供了三层的ClassLoader：

Bootstrap classLoader:主要负责加载核心的类库(java.lang.*等)，构造ExtClassLoader和APPClassLoader。

ExtClassLoader：主要负责加载jre/lib/ext目录下的一些扩展的jar。

AppClassLoader：主要负责加载应用程序的主函数类

我们就更容易理解了，当一个Hello.class这样的文件要被加载时。不考虑我们自定义类加载器，首先会在AppClassLoader中检查是否加载过，如果有那就无需再加载了。如果没有，那么会拿到父加载器，然后调用父加载器的loadClass方法。父类中同理也会先检查自己是否已经加载过，如果没有再往上。注意这个类似递归的过程，直到到达Bootstrap classLoader之前，都是在检查是否加载过，并不会选择自己去加载。直到BootstrapClassLoader，已经没有父加载器了，这时候开始考虑自己是否能加载了，如果自己无法加载，会下沉到子加载器去加载，一直到最底层，如果没有任何加载器能加载，就会抛出ClassNotFoundException。

```java
package java.lang;

public class String {
    // 双亲委派机制 ：安全
    // 1. APP -> EXC -> BOOT(最终执行) 一层一层往上找 在BOOT加载器中找到了所以不会执行这里的toString
    // 若最上层 没有再一层层往下 最终才会找到APP加载器中的这个

    @Override
    public String toString() {
        return "Hello";
    }

    public static void main(String[] args) {
        String s = new String;
        s.toString();
    }
    /**
     * 1. 类加载器收到类加载的请求  Application
     * 2. 将这个请求向上委托给父类加载器去完成，一直向上委托，直到启动类加载器
     * 3. 启动类加载器检查是否能够加载这个类，能加载就结束，使用当前加载器，否则抛出异常，通知子类加载器加载
     * 4. 重复步骤3
     */

}
```

**为什么要设计这种机制**
这种设计有个好处是，如果有人想替换系统级别的类：String.java。篡改它的实现，在这种机制下这些系统的类已经被Bootstrap classLoader加载过了（为什么？因为当一个类需要加载的时候，最先去尝试加载的就是BootstrapClassLoader），所以其他类加载器并没有机会再去加载，从一定程度上防止了危险代码的植入

## 沙箱安全机制

### 安全机制

参考：[(11条消息) Java之AccessController安全模型_we.think-CSDN博客](https://blog.csdn.net/ioteye/article/details/109921371)

java安全模型的核心就是java沙箱（sandbox），什么是沙箱？沙箱是一个限制程序运行的环境。沙箱机制就是将java代码限定在虚拟机（JVM）特定的运行范围中，并且严格限制代码对本地系统资源访问，通过这样的措施来保证对代码的有效隔离，防止对本地系统造成破坏。沙箱**主要限制系统资源访问**，那系统资源包括什么？CPU，内存、文件系统、网络。不同级别的沙箱对这些资源访问的限制也可以不一样。

所有的java程序运行都可以指定沙箱，可以定制安全策略

在java中将执行程序分为本地代码何远程代码两种，本地代码默认视为可信的，而远程代码则被看作是不受信的。对于受信的本地代码，可以访问一切本地资源。而对于非受信的远程代码在早期的java实现中，安全依赖于沙箱（sandbox）机制。如下图JDK1.0安全模型

![](https://img-blog.csdnimg.cn/20201122130153848.png)

但如此严格的安全机制也给程序的功能扩展带来障碍，比如当用户希望远程代码访问本地系统的文件时，就无法实现。因此在后续的java1.1版本中，针对安全机制做了改进，增加了**安全策略**，允许用户指定代码对本地资源的访问权限，如下图所示JDK1.1安全模型

![](https://img-blog.csdnimg.cn/20201122130059715.png)

在JDK 1.2 版本中，再次改进了安全机制，增加了代码签名。不论本地代码或是远程代码，都会按照用户的安全策略设定，由类加载器加载到虚拟机中权限不同的运行空间，来实现差异化的代码执行权限控制。

![](https://img-blog.csdnimg.cn/20201122125952373.png)

当前最新的安全机制实现，则引入了域 (Domain) 的概念。虚拟机会把所有代码加载到不同的系统域和应用域，系统域部分专门负责与关键资源进行交互，而各个应用域部分则通过系统域的部分代理来对各种需要的资源进行访问。虚拟机中，不同的受保护域 (Protected Domain)，对应不一样的权限 (Permission)。存在于不同域中的类文件，具有了当前域的全部权限。如下图JDK1.6最新安全模型
![](https://img-blog.csdnimg.cn/20201122125459801.png)

### 组成沙箱的基本组件

- 字节码校验器（bytecode verifier）：确保java类文件遵循java语言规范，这样可以帮助Java程序实现内存保护。但并不是所有的类文件都会经过字节码校验，比如核心类
- 类装载器（class loader）：其中类装载器在3个方面对Java沙箱起作用
  - 它防止恶意代码去干涉善意代码
  - 它守护了被信任的类库边界
  - 它将代码归入保护域，确定了代码可以进行哪些操作

虚拟机为不同的类加载器载入的类提供不同的命名空间，命名空间由一系列名称组成，每一个被装载的类将有一个名字，这个命名空间是由Java虚拟机为每一个类装载器维护的，他们互相之间甚至不可见

​	类装载器采用的机制是双亲委派机制。

1. 从最内层JVM自带类加载器开始加载，外层恶意同名类得不到加载从而无法使用
2. 由于严格通过包来区分访问域，外层恶意的类通过内置代码也无法获得权限访问到内部类，破坏代码自然无法生效
3. 存取控制器（access controller）：存取控制器可以控制核心API对操作系统的存取权限，而这个控制的策略设定，可以由用户指定
4. 安全管理器（security manager）：是核心API何操作系统之间的主要接口。实现权限控制，比存取控制器优先级高
5. 安全软件包（security package）：java.security下的类何扩展包下的类，允许用户为自己的应用增加新的安全特性，包括：
   - 安全提供者
   - 消息摘要
   - 数字签名  keytools
   - 加密
   - 鉴别

## Native

```java
package com.Sucker;

public class Demo {
    public static void main(String[] args) {
        new Thread(()->{

        },"my thread name").start();

    }
    //native:凡是带由native 关键字的，说明java的作用范围达不到了，会去调用底层C语言库
    // 会进入本地方法栈
    // 调用本地方法本地接口  JNI
    // JNI作用：扩展Java的使用，融合不同的编程语言为Java所用！ 最初：C、C++
    // 它在内存区域中专门开辟了一块 标记区域：Native Method Stack(本地方法栈)，登记 native 方法
    // 在最终执行的时候，加载本地方法库中的方法，通过 JNI
    private native void start0();
}
```

**JNI：Java Native Interface（Java本地方法接口）**

## PC寄存器

程序计数器：Program Counter Register

每个线程都有一个程序计数器，是线程私有的，就是一个指针，指向方法区中的方法字节码，在执行引擎时读取下一条指令，是一个非常小的内存空间，几乎可以忽略不计

## 方法区

Method Area 方法区

方法区是被所有线程共享，所有字段和方法字节码，以及一些特殊方法，如构造函数，接口代码也在此定义，简单说，所有定义的方法的信息都保存在该区域，**此区域属于共享区间**

**静态变量、常量、类信息（构造方法、接口定义）、运行时的常量池存在方法区中，但是实例变量存在堆内存中，和方法区无关**

static  final  Class  常量池

## 栈

栈：先进后出

队列：先进先出（FIFO：First input First Output）

栈：栈内存，主管程序的运行，生命周期和线程同步；线程结束，栈内存就释放

对于栈来说，不存在垃圾回收问题

栈里面会放：8大基本类型 + 对象引用 + 实例的方法

栈运行的原理：栈帧，存在父帧和子帧

栈满溢出：StackOverflowError

栈 + 堆 + 方法区：交互关系

![](https://img-blog.csdnimg.cn/3def4671dcc643c4b9575e36bc626293.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

**java对象在内存中实例化的过程图**

参考：[(12条消息) Java对象在内存中实例化的过程_youchitang的博客-CSDN博客_一个对象在内存中实例化的过程](https://blog.csdn.net/Tony__Jaa/article/details/107612059)

## 三种JVM

- Sun公司 HotSpot cmd下输入 java -version  -》Java HotSpot(TM) 64-Bit Server VM (build 25.291-b10, mixed mode)
- BEA `JRockit`
- IBM `J9 VM`

## 堆

### 概述

Heap，一个JVM只有一个堆内存，堆内存的大小是可以调节的

类加载器读取了类文件后，一般会把：类，方法，常量，变量，保存我们所有引用类型的真实对象

堆内存中分为三个区域：

- 新生区（伊甸园区）Young/New
- 养老区 Old
- 永久区  Perm

![](https://img-blog.csdnimg.cn/44d7324bed72439ca494eb24c7d5682e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

GC 垃圾回收，主要是在伊甸园区和养老区

假设内存满了，就会报错OOM ，堆内存不够  java.lang.OutOfMemoryError：java.heap.space

在JDK8以后，永久存储区改名为（元空间）

### 新生区

- 类：诞生和成长的地方，甚至死亡；
- 伊甸园区
- 幸存者区（0，1）

### 养老区

- 老年代的对象比较稳定，所以MajorGC不会频繁执行。

> 触发MinorGC的条件：
>  1 在进行MajorGC之前，一般都先进行了一次MinorGC，使得有新生代的对象进入老年代，当老年代空间不足时就会触发MajorGC。
>  2 当无法找到足够大的连续空间分配给新创建的较大对象时，也会触发MajorGC进行垃圾回收腾出空间。

MajorGC采用标记—清除算法(或者标记—整理算法)（不是Full GC）
MajorGC的耗时比较长，因为要先整体扫描再回收，MajorGC会产生内存碎片。为了减少内存损耗，一般需要合并或者标记出来方便下次直接分配。

**当老年代也满了装不下的时候，就会抛出OOM**

### 永久区

这个区域常驻内存的。用来存放JDK自身携带的Class对象，Interface元数据，即java运行时的一些环境或类信息，这个区域不存在垃圾回收！关闭JVM虚拟机时就会释放这个区域的内存

- jdk1.6之前：永久代，常量池是在方法区
- jdk1.7       ：永久代，但是慢慢退化，`去永久代`，常量池在堆中
- jdk1.8之后：无永久代，常量池在元空间

指内存的永久保存区域，主要存放Class和Meta（元数据）的信息。
Class在被加载的时候元数据信息会放入永久区域，但是GC不会在主程序运行的时候清除永久代的信息。***所以这也导致永久代的信息会随着类加载的增多而膨胀，最终导致OOM。\***

> 注意: 在Java8中，永久代已经被移除，被一个称为“元数据区”（元空间）的区域所取代。

元空间的本质和永久代类似，都是对JVM规范中方法区的实现。不过元空间与永久代之间最大的区别在于：**元空间并不在虚拟机中，而是使用本地内存。**因此默认情况下元空间的大小仅仅受本地内存的大小限制。类的元数据放入 native memory, 字符串池和类的静态变量放入java堆中。 这样可以加载多少类的元数据就不再由MaxPermSize控制, 而由系统的实际可用空间来控制。

```java
package com.Sucker;

public class Test {
    public static void main(String[] args) {
        //返回虚拟机试图使用的最大内存
        long max = Runtime.getRuntime().maxMemory();
        //返回JVM的总内存
        long total = Runtime.getRuntime().totalMemory();

        System.out.println("max="+max+"字节\t"+(max/(double)1024/1024)+"MB");
        System.out.println("total="+total+"字节\t"+(total/(double)1024/1024)+"MB");

        //默认情况下：分配的总内存 是电脑内存的1/4，初始化的内存：1/64

        //OOM：
          //1. 尝试扩大堆内存看结果
          //2. 分析内存，查看哪里出错（专业工具）

        //-Xms1024m -Xmx1024m -XX:+PrintGCDetails 调优

    }

}

```

### 分析OOM原因

在一个项目中，突然出现了OOM故障：

- 能够看到代码第几行出错：内存快照分析工具，MAT，Jprofiler
- Debug，一行行分析代码！

**MAT，Jprofiler 作用：**

- 分析Dump内存文件，快速定位内存泄漏
- 获得堆中的数据
- 获得大的对象
- ...

**使用Jprofiler工具**

在Plugins（插件）中先下载好Jprofiler 插件，再下载Jprofiler软件

![](https://img-blog.csdnimg.cn/18f0ba51a383407aac4cc0ab09447a8d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

**修改内存**

![](https://img-blog.csdnimg.cn/84b81f9f93f145cda61e335065c94397.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

**使用Jprofiler**

运行修改内存的代码后，获得Dump文件，在文件夹中显示Demo代码文件往上级目录找可以看到

![](https://img-blog.csdnimg.cn/71eec90cd2f44a86970ba6bb721cbe3a.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/c8fb480a41ce4047a4cb1197420fdb4d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

```java
package com.Sucker;

import java.sql.Array;
import java.util.ArrayList;

// -Xms 设置初始化内存分配大小，默认1/64
// -Xmx 设置最大分配内存，默认1/4
// -XX:+PrintGCDetails  打印GC垃圾清理信息
//-XX:+HeadDumpOnOutOfMemoryError  OOM Dump文件
// -Xms1m -Xmx8m -XX:+HeadDumpOnOutOfMemoryError
public class Demo03 {

    byte[] array = new byte[1*1024*1024]; // 1M

    public static void main(String[] args) {
        ArrayList<Demo03> list = new ArrayList<>();
        int count = 0;

        try {
            while (true){
                list.add(new Demo03());
                count++;
            }
        } catch (Exception e) {
            System.out.println("count:"+count);
            e.printStackTrace();
        }

    }

}
```

## GC：垃圾回收

### 概述

![](https://img-blog.csdnimg.cn/1687c1b816f540e89c913910f69898d7.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

JVM在进行GC时，并不是对这三个区域统一回收。大部分时候，回收都是新生代

- 新生代
- 幸存区（from，to）
- 老年区

GC两种类：轻GC，重GC

### GC的算法：标记清除法、标记压缩、复制算法、引用计数法

#### 引用计数法(基本不采用)：

![](https://img-blog.csdnimg.cn/a06482c34b2a4274865240e37293b823.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

算法思想：

- 每个对象在创建的时候，就给这个对象绑定一个计数器。每当有一个引用指向该对象时，计数器加一；每当有一个指向它的引用被删除时，计数器减一。这样，当没有引用指向该对象时，该对象死亡，计数器为0，这时就应该对这个对象进行垃圾回收操作。

核心思想：

- 为每个对象额外存储一个计数器 RC ，根据 RC 的值来判断对象是否死亡，从而判断是否执行 GC 操作。

#### 复制算法：

该算法将内存平均分成两部分，然后每次只使用其中的一部分，当这部分内存满的时候，将内存中所有存活的对象复制到另一个内存中，然后将之前的内存清空，只使用这部分内存，循环下去。姑且将两个区域称为form区和to区

注意：
这个算法与标记-整理算法的区别在于，该算法不是在同一个区域复制，而是将所有存活的对象复制到另一个区域内。

![](https://img-blog.csdnimg.cn/c81e590caab04cceb460850e7b6654f2.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/e87b6451382e459aa11c1993038e169d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

- 好处：没有内存碎片
- 坏处：浪费内存空间：多了一半空间永远是空to，假设对象100%存活（极端情况）-> OOM

复制算法最佳使用场景：对象存活度较低的时候：新生区

#### 标记清除算法

![](https://img-blog.csdnimg.cn/beb64887486a4d10ba1f3c3837c0386c.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

标记清除算法的执行过程分为两个阶段：标记阶段、清除阶段。

- 标记阶段会通过可达性分析将不可达的对象标记出来。
- 清除阶段会将标记阶段标记的垃圾对象清除。

优点：不需要额外的空间

缺点：两次扫描，严重浪费时间，会产生内存碎片

#### 标记压缩

![](https://img-blog.csdnimg.cn/14a91655f2ea47b191ae0cc53e35ebb9.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### 总结

内存效率：复制算法 > 标记清楚算法 > 标记压缩算法 （时间复杂度问题）

内存整齐度：复制算法 = 标记压缩算法 > 标记清除算法

内存利用率：标记压缩算法 = 标记清楚算法 > 复制算法

GC又称为：分代收集算法

年轻代：

- 存活率低
- 复制算法

老年代:

- 区域大，存活率高
- 标记清除（内存随便不是太多就继续清除）+ 标记压缩混合实现

可以看《深入理解JVM》

## JMM

JUC中查看

