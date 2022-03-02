## java学习

## 卸载JDK

1. 首先打开高级系统设置，找到环境变量中JAVA_HOME，其地址中删除java的包，再将环境变量也删除
2. 将path中的javahome相关删除
3. 打开Dos窗口（cmd）输入java -version检测

## 安装JDK

1. 搜索JDK8下载对应版本
2. 配置环境变量
   1. 我的电脑->右键->属性
   2. 环境变量->JAVA_HOME![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210427154103.png)
   3. Path中新建![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210427154617.png)
3. cmd中测试JDK安装成功，输入java -version

## HelloWorld

1. 新建文件夹存放代码
2. 新建java文件
   - 文件后缀名为.java
   - Hello.java
3. 编写代码

```java
public class Hello{
	public static void main(String[] args){
		System.out.print("Hello,World!");
	}
}
```

4. 文件名和类名一定要保持一致![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210427163621.png)

## 快捷用法

1. psvm快捷main函数，sout输出语句

## java基础语法

1. 单行注释与多行注释与C语言一样
2. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210428145748.png)

## 数据类型

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210428150440.png)

1. long类型需要在数字后面加L，float需要加F，布尔值是boolean
2. 二进制是前面加0b，八进制是加0，十六进制加0x
3. 浮点数有舍入误差，最好避免使用浮点数进行比较

## 类型转换

1. 强制类型转换需要加(),是由高到低时，而自动类型转换是由低到高，直接即可
2. 不能对布尔值进行转换
3. 不能把对象类型转换为不相干的类型
4. 转换时可能存在溢出问题和精度问题，转换前如果已经溢出，则转换无效
5. JKD7新特性，可以使用下划线分割数字，例如10_0000_0000更易阅读

## 变量

1. 每个变量都需要申明类型，可以是基本类型，也可以是引用类型
2. 实例变量：从属于对象，如果不初始化，默认为0，boolean值为false，除了基本类型，其余都是null![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210428160529.png)
3. 类变量 static 类似全局变量
4. 常量需加final，修饰符不存在先后顺序，例如final double PI=3.14，常量名一般使用大写字符，不能被继承
5. 变量命名规范，第一个单词小写，后面首字母大写，常量使用大写字母和下划线，类名使用首字母大写与驼峰原则，方法名也是首字母小写和驼峰原则

## 运算符

1. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210506172012.png)
2. 快捷键ctrl+D复制当前行到下一行
3. 混合类型运算时将会自动升为最高的数据类型再计算
4. 关系运算符例如>,<等运算时返回布尔值，true or false
5. ++，--为一元运算符，与C语言同样用法
6. 可以使用Math里面的函数，方法为Math.pow()等
7. 与或非与C语言一样，&&，||，！注意，若判断b&&a时b已经为false，那么就不会考虑a的结果
8. 位运算中&表示将每一位进行比较，都为1才为1，否则为0，而 | 则是有1出1，无1出0，异或 ^ 表示相同为0，不同为1，取反 ~ 则是取反。
9. 位运算效率高，左移 << 类似 *2 ，右移 >> 类似 /2 。2<<3为16![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210506181956.png)
10. 三元运算符，如果其他类型运算后+""则会执行运算，若""+运算，则会变为string类型，x ？ y ： z用法与C一样

## 包机制

1. 包机制![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210508153953.png)
2. 导包使用import，若将全部类导入可以使用import com.Sucker.base.*

## JavaDoc

1. JDK帮助文档中内容有用
2. 可以参考阿里巴巴开发人员手册
3. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210508155628.png)
4. 使用IDEA生成javadochttps://blog.csdn.net/weixin_42140580/article/details/89635775

## 用户交互Scanner

1. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210508162144.png)
2. 属于IO流的类要记得关闭
3. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210508172036.png)
4. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210508172120.png)
5. Scanner中判断整数和小数方法，接收键盘输入整数和小数![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210509124106.png)
6. hasNextDouble是判断是否为数字![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210509124901.png)

## 顺序结构

1. 顺序执行

## 选择结构

1. String s.equals()判断字符串是否相等

#### if选择结构

#### switch选择结构

1. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210509141350.png)
2. 注意可以支持String类型了
3. 反编译：java---class(字节码文件)---反编译(IDEA)

## 循环结构

1. while循环，do-while循环(至少执行一次
2. for循环，可以通过100.for快捷键打出 i 从0-100
3. 注意sout中println输出完会换行，可以只用print，单独sout可以实现直接换行，使用\r\n表示换行![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210509145420.png)
4. 增强型for循环，主要用于数组或集合![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527152042.png)

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527152505.png)

5. break,continue,goto![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527152848.png)

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527161801.png)

## Java方法

1. 何谓方法：System.out.println()中System就是一个类，out为其下一个输出对象，println()就是一个方法。方法是语句的集合，它们在一起执行一个功能，方法类似函数![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527162942.png)
2. 方法的定义和调用![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527164005.png)

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527164204.png)

3. 方法的重载

   重载就是在一个类中，有相同的函数名称，但形参不同的函数

   通过返回值和实参确定调用哪个![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527164944.png)

   ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527165104.png)

4. 命令行传参

   传递命令行参数给main函数实现

   ```java
   package com.Sucker.method;
   
   public class Demo02 {
       public static void main(String[] args) {
           for (int i = 0; i < args.length; i++) {
               System.out.println("args["+ i +"]: "+args[i]);
           }
       }
   }
   ```

   ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210527165918.png)

5. 可变参数

   JKD1.5开始，Java支持传递同类型的可变参数给一个方法

   在方法声明中，在指定参数类型后加一个省略号（...）

   一个方法中只能指定一个可变参数，它必须是方法的最后一个参数，任何普通参数必须在它之前声明

   如果不用static，则可以通过new一个类，得到一个对象，通过对象.方法调用方法，这种形式是实例化这个类，这种方法是非静态方法，而加了static是静态方法。

   ```java
   package com.Sucker.method;
   
   public class Demo03 {
       public static void main(String[] args) {
           Demo03 demo03 = new Demo03();
           demo03.test(1,2,3,45,6);
       }
   
       public void test(int... i){
           System.out.println(i[0]);
           System.out.println(i[1]);
           System.out.println(i[2]);
           System.out.println(i[3]);
           System.out.println(i[4]);
       }
   }
   ```

6. 递归，用到数据结构栈

   ```java
   package com.Sucker.method;
   
   public class Demo04 {
       public static void main(String[] args) {
           System.out.println(f(3));
       }
   
       public static int f(int n){
           if(n==1) return 1;
           else return n*f(n-1);
       }
   }
   ```

7. 数组

   数组声明方式：int[] a，int a[]，两种方法都可以，但是首选第一种

   java使用new操作符来创建数组，int[] a = new a[size]；一般像这样将两步写在一起

   若没有赋值，则int型默认为0，string类型为null

   可以使用a.length获取长度

   ```java
   package com.Sucker.method;
   
   public class Demo05 {
       public static void main(String[] args) {
           int[] nums;//声明
           nums = new int[10];//创建
   ```

   声明数组是向堆栈中压入，创建数组则是在堆中开辟空间

   数组本身就是对象，Java中对象是在堆中的，因此数组无论保存原始类型还是其他对象类型，数组对象本身是在堆中的

   数组可以使用增强型遍历：for(int array : arrays) array相当于i，arrays是数组名

   方法可以返回一个数组！

   ```java
   package com.Sucker.array;
   
   public class Demo01 {
       public static void main(String[] args) {
           int[] arrays = {1,2,3,4,5};
           int[] result = reverse(arrays);
           System.out.println(result[0]);
       }
   
       public static int[] reverse(int[] arrays){
           int[] result = new int[arrays.length];
           for (int i = arrays.length-1,j=0; i >= 1; i--,j++) {
               result[j] = arrays[i];
           }
           return result;
       }
   }
   ```

   多维数组

   ```java
   package com.Sucker.array;
   
   public class Demo02 {
       public static void main(String[] args) {
           int[][] array = {{1,2},{2,3}};
           int a[][] = new int[2][2];
           System.out.println(array[0][1]);
       }
   }
   ```

   Arrays类：import java.util.Arrays;

   类中有许多不同方法

   ```java
   package com.Sucker.array;
   import java.util.Arrays;
   public class Demo03 {
       public static void main(String[] args) {
           int[] a = {1,2,3,4,5,6,7,8};
           //System.out.println(a);
           //toString打印数组元素
           System.out.println(Arrays.toString(a));
           //sort排序,默认升序
           Arrays.sort(a);
           //fill方法进行数组赋值
           Arrays.fill(a,0);//将a数组全部赋值为0
           Arrays.fill(a,2,4,1);//将a数组2-4号元素赋值为1，左闭右开
           System.out.println(Arrays.toString(a));
           //equals方法比较数组元素是否相等
           //binarySearch方法对数组进行二分查找法查找数组元素
       }
   }
   ```

   冒泡排序

   ```java
   for (int i = 0; i < arrays.length-1; i++) {
              for (int j = 0; j < arrays.length-1-i; j++) {
   ```

   稀疏数组：当一个数组中大部分元素为0或者为同一个值时，可以使用稀疏数组来保存

   ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210529144708.png)

   输出二维数组

   ```java
   package com.Sucker.array;
   
   public class Demo05 {
       public static void main(String[] args) {
           int[][] array1 = new int[11][11];
           for(int[] ints : array1){
               for(int anInt : ints){
                   System.out.println(anInt+"\t");
               }
           }
   
   ```

## 面向对象编程（oop）

### 面向对象

1. 面向对象思想

   - 分类的思想模式，思考问题首先思考解决问题需要哪些分类，再对这些分类进行单独思考，最后才对某个分类下的细节进行面向过程的思索

   - 面向对象编程的本质：以类的方式组织代码，以对象的组织（封装）数据

   - 三大特性：封装、继承、多态

   - 从认识论角度考虑是先有对象后有类。对象，是具体的事物，类是抽象的，是对对象的抽象。例如，很多个人为对象，而其中当教师的就是一个类，一类当教师的人

   - 从代码的运行角度考虑是先有类后有对象，类是对象的模板

2. 回顾方法的定义

   - 两个方法如果都是静态的（static）或非静态，则可以直接在一个方法中调用另一个，而一个是静态的一个不是，则不行，因为静态是已经存在的，而非静态需要new实例化后才存在

3. 值传递与引用传递

   - ```java
     package com.Sucker.oop;
     //引用传递：对象，本质还是值传递
     public class Demo01 {
         public static void main(String[] args) {
             Person person = new Person();
             System.out.println(person.name);
             change(person);
             System.out.println(person.name);
         }
     
         public static void change(Person person){
             //person是一个对象：指向的是 Person person = new Person();这是一个具体的人！
             person.name="Sucker";
         }
     }
     //定义了一个person类，有一个name属性
     class Person{
         String name;//null
     }
     ```

### 类与对象

1. 类与对象的关系：类是一种抽象的数据类型![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210529160129.png)

2. 创建与初始化对象

   - 一个类里面只能存在属性和方法，this代表当前这个类

   - 类是抽象的，需要实例化，实例化后会获得一个自己的对象

   - 使用new关键字创建时，除了分配内存空间外，，还会给创建好的对象进行默认的初始化以及对类中的构造器的调用

   - 以类的方式组织代码，以对象的组织(封装)数据

     ```java
     package com.Sucker.oop.Demo02;
     //学生类
     public class Student {
         //属性：字段
         String name;
         int age;
         //方法
         public void study(){
             System.out.println(this.name+"学习");
         }
     }
     ```

     ```java
     package com.Sucker.oop.Demo02;
     //一个项目应该只存在一个main方法
     public class Application {
         public static void main(String[] args) {
             //类是抽象的，需要实例化
             //类实例化后会返回一个自己的对象
             //student就是一个Student类的具体实例
             Student xiaoming = new Student();
             Student xiaohong = new Student();
     
             xiaoming.name="小明";
             xiaoming.age=3;
             System.out.println(xiaoming.name);
         }
     }
     ```

3. 构造器

   - 类中的构造器也叫构造方法，是在进行创建对象的时候必须调用的

   - 构造器两个特点：必须和类的名字相同、必须没有返回类型，也不能写void

   - alt+insert可以快速生成构造器

   - 有参构造：一旦定义了有参构造，无参构造就必须显示定义，但是如果父类中已经构建过无参方法，子类不需要重新构建，也就是说必须有一个继承类中有无参构造方法

   - ```java
     package com.Sucker.oop.Demo02;
     //java-->生成class文件
     public class Person {
         //一个类即使什么都不写，也会存在一个方法
         //显示的定义构造器
     
         String name;
         //实例化初始值
         //1.使用new关键字，本质是在调用构造器
         //2.用来初始化值
         public Person(){
             this.name="Sucker";
         }
     
         //有参构造：一旦定义了有参构造，无参构造就必须显示定义
         public Person(String name){
             this.name=name;
         }
     }
     ```

     ```java
     package com.Sucker.oop.Demo02;
     //一个项目应该只存在一个main方法
     public class Application {
         public static void main(String[] args) {
             Person person = new Person("Ssucker");
             System.out.println(person.name);
         }
     }
     ```

### 封装

- private：私有，私有的属性不能直接访问，可以通过方法调用

- 通过public的方法调用，alt+insert可以直接生成get和set方法

- 可以在方法中封装各种操作增加安全性

- 封装(数据的隐藏):通常禁止直接访问对象中数据的实际表示，而应该通过接口操作来访问，这称为信息隐藏

- 封装作用：

  - 提高安全性
  - 隐藏代码实现细节
  - 统一接口
  - 系统可维护性增加

- ```java
  package com.Sucker.oop.Demo03;
  
  public class Student {
  
      //属性私有
      private String name;
      private int id;
      private char sex;
  
      //提供一些可以操作这个属性的方法
      //提供一些public的get、set方法
  
      //get 获取这个数据
      public String getName(){
          return this.name;
      }
  
      //set 给这个数据赋值
      public void setName(String name){
          this.name=name;
      }
  }
  ```

  ```java
  package com.Sucker.oop;
  
  import com.Sucker.oop.Demo03.Student;
  
  public class Application {
      public static void main(String[] args) {
          Student s1 = new Student();
          s1.setName("Sucker");
          System.out.println(s1.getName());
      }
  }
  ```

### 继承

1. 继承

   - 继承的本质是对某一批类的抽象
   - extends的意思是“扩展”，子类是父类的扩展
   - Java中只有单继承，所有类都直接或间接继承Object
   - 子类继承父类的全部方法，修饰符需要用public，私有的无法被继承
   - ctrl+h查看继承的树结构

2. super

   - 调用父类

   - 调用子类的无参构造方法时会首先调用父类的无参构造方法，即执行隐藏代码super();

   - 当使用子类实例化时，如果没有显式的使用super去调用父类的构造函数，那么程序会自动调用**父类中的无参构造函数进行初始化工作**

   - 调用父类的构造方法时，必须在子类构造方法的第一个

   - super必须且只能出现在子类的方法或构造方法中

   - super和this不能同时调用构造方法，因为其都需要在第一行，但是可以使用super后再使用this.xx=xx

   - super与this对比![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210529180818.png)

   - ```java
     package com.Sucker.oop.Demo04;
     //Student is 人 ：派生类，子类
     public class Student extends Person{
         private String name = "suke";
         public void print(){
             System.out.println("Student");
         }
     
         public void test1(){
             print();
             this.print();
             super.print();
         }
         public void test(String name){
             System.out.println(name);
             System.out.println(this.name);
             System.out.println(super.name);
         }
     }
     ```

     ```java
     package com.Sucker.oop.Demo04;
     //Person 人 : 父类
     public class Person {
         protected String name = "Sucker";
         public void print(){
             System.out.println("Person");
         }
     }
     ```

     ```java
     package com.Sucker.oop;
     
     import com.Sucker.oop.Demo04.Student;
     
     public class Application {
         public static void main(String[] args) {
             Student student = new Student();
             student.test1();
         }
     }
     ```

3. 方法的重写

   - 重写都是方法的重写，与属性无关

   - 当静态时，与左边数据类型有关，会调用父类方法

   - ```java
     package com.Sucker.oop.Demo04;
     
     public class B {
         public static void test(){
             System.out.println("B->test");
         }
     }
     ```

     ```java
     package com.Sucker.oop.Demo04;
     
     public class A extends B{
         public static void test(){
             System.out.println("A->test");
         }
     }
     ```

     ```java
     package com.Sucker.oop;
     
     import com.Sucker.oop.Demo04.A;
     import com.Sucker.oop.Demo04.B;
     
     public class Application {
         public static void main(String[] args) {
             //静态方法的调用只和左边定义的数据类型有关
             //非静态：重写
             A a = new A();
             a.test();
             //父类的引用指向了子类
             B b = new A();
             b.test();
         }
     }
     ```

     此时是static静态，输出为A->test和B->test

   - 非静态时会重写父类方法，即此时b是Anew出来的对象，调用A的方法

   - ```java
     package com.Sucker.oop.Demo04;
     
     public class B {
         public void test(){
             System.out.println("B->test");
         }
     }
     ```

     ```java
     package com.Sucker.oop.Demo04;
     
     public class A extends B{
         public void test(){
             System.out.println("A->test");
         }
     }
     ```

     ```java
     package com.Sucker.oop;
     
     import com.Sucker.oop.Demo04.A;
     import com.Sucker.oop.Demo04.B;
     
     public class Application {
         public static void main(String[] args) {
             //静态方法的调用只和左边定义的数据类型有关
             //非静态：重写
             A a = new A();
             a.test();
             //父类的引用指向了子类
             B b = new A();//子类重写了父类的方法
             b.test();
         }
     }
     ```

     此时输出都是A->test

   - 重写需要有继承关系，子类重写父类的方法

   - ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210529183158.png)

   - 为什么需要重写：父类的功能子类不一定需要或者不一定满足

   - Alt+Insert : override快捷键

   - 无法重写：

     - static 方法，属于类，不属于实例
     - final常量
     - private方法

### 多态

1. 多态：即同一方法可以根据发送对象的不同而采取多种不同的行为方式![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210529223350.png)
2. 父类可以指向子类，但是不能调用子类独有的方法
3. 多态是方法的多态，不是属性的多态
4. 父类和子类需要有联系否则可能会有类型转换异常 ClassCastException！
5. 存在条件：继承关系，方法需要重写，父类引用指向子类对象! Father f1 = new Son();

### instanceof

1. instanceof用法：判断X是否与Y有继承关系

   ```java
   public class Application {
       public static void main(String[] args) {
           //Object > String
           //Object > Person > Teacher
           //Object > Person > Student
           //看前面这个是否是后面的子类或者就是后面这个类型,object对象是Student
   
           Object object = new Student();
   
           System.out.println(object instanceof Student);//true
           System.out.println(object instanceof Person);//true
           System.out.println(object instanceof Object);//true
           System.out.println(object instanceof Teacher);//false
           System.out.println(object instanceof String);//false
   
           Person person = new Student();
           System.out.println(person instanceof Student);//true
           System.out.println(person instanceof Person);//true
           System.out.println(person instanceof Object);//true
           System.out.println(person instanceof Teacher);//false
           //System.out.println(object instanceof String);//编译报错，同级
       }
   }
   ```

2. instanceof 是 Java 的保留关键字。它的作用是测试它左边的对象是否是它右边的类的实例，返回 boolean 的数据类型

3. instanceof是Java中的二元运算符，左边是对象，右边是类；当对象是右边类或子类所创建对象时，返回true；否则，返回false

4. ```java
   public static void main(String[] args) {
           A a = null;
           B b = null;
           boolean result;
           result = a instanceof A;
           System.out.println(result); // 结果：false null用instanceof跟任何类型比较时都是false
           result = b instanceof B;
           System.out.println(result); // 结果：false null用instanceof跟任何类型比较时都是false
   
   
           a = new B();
           b = new B();
           result = a instanceof A;
           System.out.println(result); // 结果：true a是接口A的实例对象引用指向子类类B，类B实现了接口A，所以属于同一个继承树分支
           result = a instanceof B;
           System.out.println(result); // 结果：true a是接口A的实例对象引用指向子类类B，类B实现了接口A，所以属于同一个继承树分支
           result = b instanceof A;
           System.out.println(result);// 结果：true b是类B的实例对象，类B实现了接口A，所以属于同一个继承树分支
           result = b instanceof B;
           System.out.println(result);// 结果：true b是类B的实例对象，类B实现了接口A，所以属于同一个继承树分支
   
   
           B b2 = new C();
           result = b2 instanceof A;
           System.out.println(result); // 结果：true b2是父类B引用指向子类C，类B实现了接口A，所以属于同一个继承树分支
           result = b2 instanceof B;
           System.out.println(result); // 结果：true b2是父类B引用指向子类C，所以属于同一个继承树分支
           result = b2 instanceof C;
           System.out.println(result); // 结果：true b2是父类B引用指向子类C，所以属于同一个继承树分支
   ```

### 类型转换

1. 强制类型转换

   ```java
   public class Application {
       public static void main(String[] args) {
           //类型之间的转化 : 父  子
           //高   低
           Person obj = new Student();
           //将obj这个对象强制转换为Student类型，我们就可以使用Student类型的方法
           Student student = (Student) obj;
           student.go();//或者直接写  ((Student) obj).go();
       }
   }
   ```

2. 子类转换父类

   ```java
   public class Application {
       public static void main(String[] args) {
           Student student = new Student();
           student.go();
           //子类转换为父类可能会丢失自己本来的一些方法！
           Person person = student;
           person.run();
       }
   }
   ```

3. 注意事项

   - 子转父，向上转型，直接转，丢失子类中原本可直接调用的特有方法
   - 父转子，向下转型，强制转换
   - ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210529234603.png)

### static

1. 静态变量调用可直接使用类名，静态变量对于类，所有对象(实例）所共享

   ```java
   public static void main(String[] args) {
           Student s1 = new Student();
           s1.score;
           System.out.println(Student.age);//静态变量推荐直接使用类名访问
           //System.out.println(Student.score);//报错
           System.out.println(s1.age);
           System.out.println(s1.score);
       }
   ```

2. 非静态方法可以调用静态方法，静态方法不能调用非静态方法

   ```java
   public class Student {
       private static int age;//静态的变量
       private double score;//非静态变量
   
       public void run(){
           go();
       }
       public static void go(){
   
       }
   
       public static void main(String[] args) {
           go();
           Student student = new Student();
           student.run();
       }
   }
   ```

3. ```java
   public class Person {
       //第二个执行，可以用来赋初值
       {
           //代码块（匿名代码块）
           System.out.println("匿名代码块");
       }
       //最早执行，与类一同加载，只执行一次
       static{
           //静态代码块
           System.out.println("静态代码块");
       }
       //第三个执行
       public Person() {
           System.out.println("构造方法");
       }
   
       public static void main(String[] args) {
           Person person = new Person();
       }
   }
   ```

   若不newPerson则只加载了static的静态代码块，静态代码块只执行一次，其他的每次都执行

4. 静态导入包

   ```java
   package com.Sucker.oop.Demo06;
   //静态导入包
   import static java.lang.Math.random;
   public class Test {
       public static void main(String[] args) {
           System.out.println(random());
       }
   }
   ```

   本来是需要写Math.random()

### 抽象类

1. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210530002621.png)

2. extends是单继承，java没有多继承，但是接口可以多继承

3. abstract抽象类，不能new抽象类，只能通过其子类去继承它：约束！

4. 抽象类中可以写普通方法，但是抽象方法必须在抽象类中

5. 抽象类就是抽象的抽象：约束

6. 抽象类有构造方法

7. ```java
   package com.Sucker.oop.Demo07;
   //抽象类的所有方法，继承了它的子类，都必须要实现它的方法，除非子类本身也是抽象类
   public class A extends Action{
       @Override
       public void doSomething() {
           
       }
   }
   ```

   ```java
   package com.Sucker.oop.Demo07;
   //abstract 关键字 抽象类
   public abstract class Action {
       //abstract,抽象方法，只有方法名字，没有方法的实现！
       public abstract void doSomething();
   }
   ```

### 接口

1. 接口

   ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210530005302.png)

2. 接口只有方法的定义

3. interface定义接口的关键字，implements实现接口

4. ```java
   package com.Sucker.oop.Demo08;
   //interface 定义接口的关键字，接口都需要有实现类
   public interface UserService {
   
       //常量 public static final
       int AGE = 99;
       //接口中的所有定义都是抽象的 public abstract 写了就是灰色的，可以不写
       void add(String name);
       void delete(String name);
       void update(String name);
       void query(String name);
   }
   ```

   ```java
   package com.Sucker.oop.Demo08;
   
   public interface TimeService {
       void timer();
   }
   ```

   ```java
   package com.Sucker.oop.Demo08;
   //类，实现接口，使用implements关键字
   //实现了接口的类，需要重写接口中的所有方法
   //利用接口实现多继承
   public class UserServiceImpl implements UserService,TimeService{
   
       @Override
       public void add(String name) {
   
       }
   
       @Override
       public void delete(String name) {
   
       }
   
       @Override
       public void update(String name) {
   
       }
   
       @Override
       public void query(String name) {
   
       }
   
       @Override
       public void timer() {
   
       }
   }
   ```

5. 接口作用

   - 约束
   - 定义一些方法，让不同的人实现
   - 接口不能被实例化（new），因为接口中没有构造方法
   
6. java采用接口方式创建类的对象与用类创建类的对象方式类似，但是区别在于用接口创建的对象不能调用实现类里的方法，只能调用接口里定义的方法

   []: https://blog.csdn.net/weixin_51355516/article/details/110238113

### 内部类

1. 内部类就是在一个类的内部再定义一个类,通过外部类来实例化内部类

2. 内部类可以获得外部类的私有属性，编译后可生成独立的字节码文件

3. 注意通过外部类实例化内部类是outer.new Inner()

4. 当外部类和内部类存在重名属性时，会优先访问内部类，如果此时需要访问外部类，则需要加上Outer.this前缀，即外部类名.this.属性

5. 成员内部类不能包含静态成员，但是可以包含静态常量。即可以static final

   ```java
   package com.Sucker.oop.Demo09;
   
   public class Outer {
   
       private int id=10;
       public void out(){
           System.out.println("这是外部类的方法");
       }
   
       public class Inner{
           public void in(){
               System.out.println("这是内部类的方法");
           }
           public void getID(){
               System.out.println(id);
           }
       }
   }
   ```

   ```java
   import com.Sucker.oop.Demo09.Outer;
   
   public class Application {
       public static void main(String[] args) {
           Outer outer = new Outer();
           //通过外部类来实例化内部类
           Outer.Inner inner = outer.new Inner();
           inner.getID();
           //也可以一步到位
           Inner inner = new Outer.new Inner();
       }
   }
   ```

   加了static就是静态内部类

   静态内部类可以直接创建对象或通过类名访问，可以声明静态成员

   此时静态内部类和外部类级别相同，想要调用外部类的属性需要创建外部类对象(new)

   调用静态内部类属性可以直接访问，调用静态内部类的静态成员用类名访问

   注意：只有内部类才可以使用static修饰，普通类不能

   ```java
   public static void main(String[] args){
       //直接调用内部类对象
       Outer.Inner inner = new Outer.Inner();//这里的.只是表示包含关系
       inner.show();
   }
   ```

   

6. 一个java类可以有多个class类，但只能由一个puclic class类

7. 局部内部类

   - 局部内部类和局部变量都不能加修饰符,可以在局部内部类里面直接访问外部类属性
   - 局部内部类里面也不能有静态成员，除非加上final常量

   ```java
   public class Outer {
   	private String name0="ll";
       //局部内部类
       public void method(){
           //局部变量,默认加了final常量，不能改变
           String add="www";
           
           //局部内部类
           class Inner{
               private String name = "null";
               private final static int count=88;//不加final就报错
                   
               public void in(){
                   //访问外部类属性
                   System.out.println(name0);//实际上就是省略了Outer.this.
                   //访问内部类属性
                   System.out.println(name);//实际上就是省略了this.
              //访问局部变量，jdk1.7要求变量一定是final常量，而1.8已默认加上
                   System.out.println(add);
               }
           }
           Inner inner = new Inner();
           inner.in();//此时可以通过new外部类调用method方法，即可调用到in方法
       }
   }
   ```

8. 匿名内部类,没有类名的局部内部类，没有名字初始化类,不用将实例保存在变量中

   - 必须继承一个父类或者实现一个接口
   - 匿名内部类就是定义类、实现类、创建对象的语法合并，只能创建一个该类的对象
   - 减少代码量

   ```java
   package com.Sucker.oop.Demo09;
   
   public class Test {
       public static void main(String[] args) {
           //没有名字初始化类,不用将实例保存在变量中
           new Apple().eat();
   		//使用匿名内部类优化，相当于创建了一个局部内部类
           UserService userService = new UserService(){
               @Override
               public void Hello() {
   				sout...
               }
           };
   	    usb.Hello();
           //若不这么写，则可以使用局部内部类
           class fan implements UserService{
               @Override
               public void Hello(){
                   sout....
               }
           }
           UserService userService = new fan();
           userService.Hello();
       }
   }
   
   class Apple{
       public void eat(){
           System.out.println("1");
       }
   }
   
   interface UserService{
       void Hel                                              lo();
   }
   ```

## 异常机制

### Error与Exception

1. 简单分类：检查性异常、运行时异常、错误ERROR![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210530014827.png)
2. 异常体系结构
   - Java把异常当作对象来处理，并定义一个基类java.lang.Throwable作为所有异常的超类
   - 在Java API中已经定义了许多异常类，这些异常类分为两大类，错误Error和Exception
   - ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210530015106.png)
3. Error：Error类对象由Java虚拟机生成并抛出![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210530015320.png)
4. Exception![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210530015451.png)

### 捕获与抛出异常

1. try-catch，可以不用finally，catch()中的参数是想要捕获的异常类型，可以和if-else一样多个catch，注意若范围更大的异常类型在上面则可能直接被捕获不执行下面catch

   ```java
   public class Test {
       public static void main(String[] args) {
   
           int a=1;
           int b=0;
   
           try{  //try监控区域
               System.out.println(a/b);
           }catch (ArithmeticException e){ //捕获异常
               System.out.println("程序出现异常，b不能为0");
           }catch (Exception e) {
               System.out.println("Exception");
           }catch (Throwable t){
               System.out.println("Throwable");
           } finally { //处理善后工作
               System.out.println("finally");
           }
       }
   }
   ```

2. 快捷键Ctrl+Alt+T选择用那种代码将其包裹

   ```java
   public class Test2 {
       public static void main(String[] args) {
           try {
               System.out.println(a/b);
           } catch (Exception e) {
               e.printStackTrace();//打印错误的栈信息
           } finally {
           }
       }
   ```

3. throw主动抛出从异常

   ```java
   public class Test2 {
       public static void main(String[] args) {
           int a=1;
           int b=0;
           new Test2().add(1,0);
       }
   
       public void add(int a,int b){
           if(b==0){
               throw new ArithmeticException();//主动抛出异常,一般在方法中使用
           }
           
       }
   }
   ```

4. throws用法

   - 定义一个方法的时候可以使用throws关键字声明。使用throws关键字声明的方法表示此方法不处理异常，而交给方法调用处进行处理。

     throws关键字格式：

     public 返回值类型 方法名称（参数列表，，，）throws 异常类{}；

      假设定义一个除法，对于除法操作可能出现异常，可能不会。所以对于这种方法最好将它使用throws关键字声明，一旦出现异常，则应该交给调用处处理。

   - ```java
     class Math{
       public int div(int i,int j) throws Exception{   // 定义除法操作，如果有异常，则交给被调用处处理
         int temp = i / j ;   // 计算，但是此处有可能出现异常
         return temp ;
       }
     };
     public class ThrowsDemo01{
       public static void main(String args[]){
         Math m = new Math() ;     // 实例化Math类对象
         try{
           System.out.println("除法操作：" + m.div(10,2)) ;
         }catch(Exception e){    // 处理异常
           e.printStackTrace() ;   // 就打印了异常内容
         }
       }
     };
     ```

### 自定义异常

1. 用户自定义异常类，只需要继承Exception类即可

   ```java
   package com.Sucker.exception.Demo02;
   
   public class Tset {
       //可能会存在异常的方法
   
       static void test(int a) throws MyException {
           System.out.println("传递的参数为"+a);
   
           if(a>10) throw new MyException(a);//抛出
           System.out.println("OK");
       }
   
       public static void main(String[] args) {
           try {
               test(11);
           } catch (MyException e) {
               System.out.println("MyException->"+e);
           }
       }
   }
   ```

   ```java
   package com.Sucker.exception.Demo02;
   //自定义异常类
   public class MyException extends Exception{
       //传递数字>10抛出异常
       private int detail;
   
       public MyException(int a) { //构造器，new的本质就是调用构造器
           this.detail = a;
       }
   
       //toString:异常的打印信息
       @Override
       public String toString() {
           return "MyException{" + "detail=" + detail + '}';
       }
   }
   ```

   注意这里toString是默认调用的，重写了也是默认调用





