## 集合

1. 集合的概念：对对象的容器，实现了对对象常用的操作，类似数组功能
2. 与数组区别
   - 数组长度固定，集合长度不固定
   - 数组可以存储基本类型和引用类型，集合只能存储引用类型
3. 位置：java.util.*

## Collection体系集合

### Collection体系

1. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210602201808.png)

### Collection接口

1. 特点：代表一组任意类型的对象，无序，无下标，不能重复

2. 方法：

   - boolean add(Object obj) //添加一个对象

   - boolean addAll(Collection c)  //将一个集合中所有对象添加到此集合中

   - void clear()  //清空此集合中所有对象

   - boolean contains(Object o)  //检查此集合中是否包含o对象

   - boolean equals(Object o)  //比较此集合是否与指定对象相等

   - boolean isEmpty()  //判断此集合是否为空

   - boolean remove(Object o)  //在此集合中移除o对象

   - int size()  //返回此集合中的元素个数

   - Object[] toArray()  //将此集合转换成数组

   - ```java
     import java.util.ArrayList;
     import java.util.Collection;
     import java.util.Iterator;
     
     public class Demo01 {
         public static void main(String[] args) {
             //Collection接口的使用
             //创建集合
             Collection collection = new ArrayList();//父类引用指向子类对象，向上转型
             //添加元素
             collection.add("苹果");
             collection.add("西瓜");
             collection.add("榴莲");
             System.out.println(collection.size());
             System.out.println(collection);//相当于toString
             //删除元素
             collection.remove("榴莲");
             //collection.clear();//清空集合
             System.out.println(collection.size());
             //遍历元素1.增强for
             for (Object object : collection) {
                 System.out.println(object);
             }
             //遍历元素2.使用迭代器(迭代器是专门用来遍历集合的一种方式)
             //迭代器中三个方法
             //1.hasNext() 是否存在下一个元素
             //2.next() 获取下一个元素（并将指针后移）返回的是object类型 ，可以强制转换
             //3.remove() 删除当前元素
             Iterator iterator = collection.iterator();
             while(iterator.hasNext()){
                 String next = (String) iterator.next();//使用迭代器过程中不能使用集合删除操作，会报并发修改错误
                 System.out.println();
                 iterator.remove();
             }
             System.out.println(collection.size());//删除完后元素个数
     
             //判断
             System.out.println(collection.contains("西瓜"));//是否含有西瓜
             System.out.println(collection.isEmpty());//空为true
         }
     
     }
     ```

   - ```java
     import com.sun.xml.internal.ws.util.pipe.StandaloneTubeAssembler;
     
     import java.util.ArrayList;
     import java.util.Collection;
     import java.util.Iterator;
     
     /**
      * Collection的使用：保存学生信息
      */
     public class Demo02 {
         public static void main(String[] args) {
             //新建Collection对象
             Collection collection = new ArrayList();
             Student s1 = new Student("张三", 20);
             Student s2 = new Student("KKK", 18);
             Student s3 = new Student("www", 22);
             //1.添加数据,实际上添加地址
             collection.add(s1);
             collection.add(s2);
             collection.add(s3);//ArrayList可以添加相同元素
             System.out.println(collection.size());
             System.out.println(collection.toString());
             //删除 ，实际上删除地址，本身还是存在的
             collection.remove(s1);
             //清空
             //collection.clear();
             //遍历：增强for
             for (Object object : collection) {
                 Student s = (Student)object;
                 System.out.println(s.toString());
             }
             //迭代器遍历
             Iterator it = collection.iterator();
             while(it.hasNext()){
                 Student next = (Student)it.next();
                 System.out.println(next.toString());
             }
             //判断
             System.out.println(collection.contains(new Student("张三",20)));//返回false
             System.out.println(collection.isEmpty());
         }
     }
     ```

   - ```java
     //学生类
     public class Student {
         private String name;
         private int age;
     
         public Student() {
         }
     
         public Student(String name, int age) {
             this.name = name;
             this.age = age;
         }
     
         public String getName() {
             return name;
         }
     
         public void setName(String name) {
             this.name = name;
         }
     
         public int getAge() {
             return age;
         }
     
         public void setAge(int age) {
             this.age = age;
         }
     
         @Override
         public String toString() {
             return "Student{" +
                     "name='" + name + '\'' +
                     ", age=" + age +
                     '}';
         }
     }
     ```

## List接口

### List子接口

1. 有序的collection(也成为序列)。此接口的用户可以对列表中的每个元素的插入位置进行精确控制。用户可以根据元素的整数索引访问元素，并搜索列表中的元素

2. 特点：有序、有下标、元素可以重复

3. 方法

   - void add(int index,Object o)  //在index位置插入对象o

   - boolean addAll(int index,Collection c)  //将一个集合中的元素添加到此集合中的index位置

   - Object get(int index)  //返回集合中指定位置的元素

   - List subList(int fromIndex, int toIndex)  //返回fromIndex和toIndex之间的集合元素

   - ```java
     //先创建集合对象
             List list = new ArrayList<>();
             //1.添加元素
             list.add("苹果");
             list.add("果");
             list.add(0,"guo果");
             System.out.println(list.size());
             System.out.println(list.toString());
             //2.删除元素
             list.remove(0);
             //3.遍历
             //3.1使用for遍历
             for (int i = 0; i < list.size(); i++) {
                 System.out.println(list.get(i));
             }
             //3.2增强for
             for (Object object : list) {
                 System.out.println(object);
             }
             //3.3使用迭代器
             Iterator it = list.iterator();
             while(it.hasNext()){
                 System.out.println(it.next());
             }
     ```

4. ListIterator为系列表迭代器，允许程序员按任一方向遍历列表、迭代期间修改列表，并获得迭代器在列表中的当前位置。

   ```java
   //3.4使用列表迭代器，和Iterator的区别，listIterator可以向前或者向后遍历，添加、删除、修改元素
           ListIterator lit = list.listIterator();
           while(lit.hasNext()){
               System.out.println(lit.nextIndex()+":"+lit.next());
           }//注意此时指针已经到最后了，所以可以从后往前遍历
           while(lit.hasPrevious()){
               System.out.println(lit.previousIndex()+":"+lit.previous());
           }
           //判断
           System.out.println(list.contains("pingguo"));
           System.out.println(list.isEmpty());
   
           //获取位置
           System.out.println(list.indexOf("果"));
   ```

   ```java
   import java.util.ArrayList;
   import java.util.List;
   
   public class Demo04 {
       public static void main(String[] args) {
           //创建集合
           List list = new ArrayList();
           //添加数字数据(自动装箱，基本类型转为包装类)
           list.add(20);
           list.add(30);
           list.add(40);
           list.add(50);
           System.out.println(list.size());
           System.out.println(list.toString());
           //删除操作
           list.remove(new Integer(20));//不能直接20，会数组越界
           //list.remove((Object) 20);或者转成Object类
   
           //补充方法subList：返回子集合
           List list1 = list.subList(1, 3);//左闭右开
           System.out.println(list1.toString());
       }
   }
   ```

5. List实现类

   - ArrayList【重点】：
     - 数组结构实现，查询快，增删慢
     - JDK1.2版本，运行效率快，线程不安全
   - Vector
     - 数组结构实现，查询快，增删慢
     - JDK1.0版本，运行效率慢，线程安全
   - LinkedList
     - 链表结构实现，增删快，查询慢

### ArrayList的使用

```java
import java.lang.reflect.Array;
import java.sql.Struct;
import java.util.ArrayList;
import java.util.Iterator;
import java.util.ListIterator;

public class Demo05 {
    public static void main(String[] args) {
        //创建集合
        ArrayList arrayList = new ArrayList();
        //1.添加元素
        Student s1 = new Student("刘德华",20);
        Student s2 = new Student("郭富城",22);
        Student s3 = new Student("梁朝伟",18);
        arrayList.add(s1);
        arrayList.add(s2);
        arrayList.add(s3);//可以添加重复的
        System.out.println(arrayList.size());
        System.out.println(arrayList.toString());
        //2.删除元素
        arrayList.remove(s1);//也可以通过下标
        arrayList.remove(new Student("刘德华",20));//这样是移除不掉的，因为里面是用的equals方法比较地址，可以通过重写这个方法解决
        System.out.println(arrayList.size());
        //3.遍历元素(重点)
        //3.1使用迭代器
        Iterator it = arrayList.iterator();
        while(it.hasNext()){
            Student s = (Student) it.next();
            System.out.println(s.toString());
        }
        //3.2使用列表迭代器
        System.out.println("-----------------");
        ListIterator lit = arrayList.listIterator();
        while(lit.hasNext()){
            Student ss = (Student) lit.next();
            System.out.println(ss.toString());
        }
        //3.2使用列表迭代器逆序
        System.out.println("-----------------");
        while (lit.hasPrevious()){
            Student ss = (Student) lit.previous();
            System.out.println(ss.toString());
        }
        //4.判断
        System.out.println(arrayList.contains(new Student("梁朝伟",18)));//此时可以比较成功返回true，因为重写了equals方法
        System.out.println(arrayList.isEmpty());

        //5.查找
        System.out.println(arrayList.indexOf(new Student("梁朝伟",18)));
    }
}
```

```java
//主要是重写equals方法，在Student类中
@Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && Objects.equals(name, student.name);
    }
```

### ArrayList源码分析

1. 默认容量  DEFAULT_CAPACITY = 10；注意：如果没有向集合中添加任何元素，那么容量为0，添加一个元素后变成10，达到10后变15，即每次扩容1.5倍

2. 存放元素的数组  elementData

3. 实际元素个数  size

4. add()方法

   ```java
   public boolean add(E e) {
           ensureCapacityInternal(size + 1);  // Increments modCount!!
           elementData[size++] = e;
           return true;
       }
   private void ensureCapacityInternal(int minCapacity) {
           ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));//从这里变成10
       }
   private void ensureExplicitCapacity(int minCapacity) {
           modCount++;
   
           // overflow-conscious code
           if (minCapacity - elementData.length > 0)
               grow(minCapacity);
       }
   
   private void grow(int minCapacity) {
           // overflow-conscious code
           int oldCapacity = elementData.length;
           int newCapacity = oldCapacity + (oldCapacity >> 1);
           if (newCapacity - minCapacity < 0)
               newCapacity = minCapacity;
           if (newCapacity - MAX_ARRAY_SIZE > 0)
               newCapacity = hugeCapacity(minCapacity);
           // minCapacity is usually close to size, so this is a win:
           elementData = Arrays.copyOf(elementData, newCapacity);
       }
   ```

### Vector类

1. Vector类可以实现可增长的对象数组、与数组一样，它包含可以使用整数索引进行访问的组件。但是Vector的大小可以根据需要增大或者缩小，以适应创建Vector后进行添加或移除项的操作

2. ```java
   import java.util.Enumeration;
   import java.util.Vector;
   
   public class Demo01 {
       public static void main(String[] args) {
           //创建集合
           Vector vector = new Vector<>();
           //1.添加元素
           vector.add("草莓");
           vector.add("芒果");
           vector.add("西瓜");
           System.out.println(vector.size());
           //2.删除元素与之前一样
   //        vector.remove(0);
   //        vector.remove("西瓜");
   //        vector.clear();
           //3.遍历
           //使用枚举器
           Enumeration en = vector.elements();
           while (en.hasMoreElements()){
               String o = (String) en.nextElement();
               System.out.println(o);
           }
           //4.判断
           System.out.println(vector.contains("西瓜"));
           System.out.println(vector.isEmpty());
           //5.其他方法
           //firstElement、lastElement、elementAt()；
       }
   }
   ```

### LinkedList使用

1. 双向链表

2. ```java
   import com.Sucker.Collection.Student;
   
   import java.util.Iterator;
   import java.util.LinkedList;
   import java.util.ListIterator;
   
   /**
    * LinkedList的使用
    * 存储结构：双向链表
    */
   public class Demo01 {
       public static void main(String[] args) {
           //创建集合
           LinkedList linkedList = new LinkedList<>();
           //1.添加元素
           Student s1 = new Student("刘德华",20);
           Student s2 = new Student("郭富城",22);
           Student s3 = new Student("梁朝伟",18);
           linkedList.add(s1);
           linkedList.add(s2);
           linkedList.add(s3);
           //linkedList.add("西瓜");
           System.out.println(linkedList.size());
           System.out.println(linkedList.toString());
   
           //2.删除
           linkedList.remove(new Student("刘德华",20));//已重写equals
           System.out.println(linkedList.size());
           //linkedList.clear();//清空
   
           //3.遍历
           //3.1for遍历
           System.out.println("-------------------------");
           for (int i = 0; i < linkedList.size(); i++) {
               System.out.println(linkedList.get(i));
           }
           System.out.println("-------------------------");
           for (Object object : linkedList) {
               Student s = (Student) object;
               System.out.println(s.toString());
           }
           //3.2使用迭代器
           System.out.println("-------------------------");
           Iterator it = linkedList.iterator();
           while(it.hasNext()){
               Student s = (Student)it.next();
               System.out.println(s.toString());
           }
           //3.3列表迭代器
           ListIterator lit = linkedList.listIterator();
           while(lit.hasNext()){
               Student s = (Student)lit.next();
               System.out.println(s.toString());
           }
   
           //4.判断
           System.out.println(linkedList.contains(s1));
           System.out.println(linkedList.isEmpty());
           //5.获取
           System.out.println(linkedList.indexOf(s1));//获取s1在链表中的位置
       }
   }
   
   ```

3. 源码分析

   ```java
   private void linkFirst(E e) {
           final Node<E> f = first;
           final Node<E> newNode = new Node<>(null, e, f);
           first = newNode;
           if (f == null)
               last = newNode;
           else
               f.prev = newNode;
           size++;
           modCount++;
       }
   ```

   ```java
   private static class Node<E> {
           E item;
           Node<E> next;
           Node<E> prev;
   
           Node(Node<E> prev, E element, Node<E> next) {
               this.item = element;
               this.next = next;
               this.prev = prev;
           }
       }
   ```

## 泛型

### 泛型概述

1. Java泛型是JDK1.5中引入的一个新特性，其本质是参数化类型，把类型作为参数传递。
2. 常见形式有泛型类，泛型接口、泛型方法
3. 语法
   - <T,...> T成为类型占位符，表示一种引用类型，只能是引用类型
4. 好处
   - 提高代码的重用性
   - 防止类型转换异常，提高代码安全性

### 泛型类

```java
/**
 * 泛型类
 * 语法：类名<T>
 * T是类型占位符，表示一种引用类型，如果编写多个可以使用逗号隔开
 */
public class MyGeneric<T> {
    //使用泛型T
    //1.创建变量
    T t;  //不能用new实例化，因为无法确定这个类型，其构造方法无法确定

    //2.作为方法的参数
    public void show(T t){
        System.out.println(t);
    }
    //3.泛型作为方法的返回值
    public T getT(){
        return t;
    }
}
```

```java
public class TestGeneric {
    public static void main(String[] args) {
        //使用泛型类创建对象
        MyGeneric<String> myGeneric = new MyGeneric<>();
        myGeneric.t = "hello";
        myGeneric.show("大家好");
        String string = myGeneric.getT();
        System.out.println(string);

        MyGeneric<Integer> myGeneric2 = new MyGeneric<>();
        myGeneric2.t = 100;
        myGeneric2.show(200);
        Integer integer = myGeneric2.getT();

        //MyGeneric<String> myGeneric3 = myGeneric2;不同泛型类型对象不能相互赋值
    }
}
```

### 泛型接口

1. 两种实现方式。1.实现类时确定好T  2.实现类也是一个泛型类，当创建实现类对象时再传T

2. ```java
   /**
    * 泛型接口
    * 语法：接口名<T>
    * 注意不能使用泛型静态常量
    */
   public interface GenericInterface<T> {
       String name="张三";
   
       T server(T t);
   }
   ```

3. ```java
   public class MyInterfaceImp implements GenericInterface<String> {
       @Override
       public String server(String s) {
           System.out.println(s);
           return s;
       }
   }
   ```

4. ```java
   package com.Sucker.Generic;
   //这里表示创建MyinterfaceImp2对象时传的类型就是T
   public class MyinterfaceImp2<T> implements GenericInterface<T> {
       @Override
       public T server(T t) {
           System.out.println(t);
           return null;
       }
   }
   ```

5. ```java
   		MyInterfaceImp imp = new MyInterfaceImp();
      		imp.server("xxxxx");
      		
      		MyinterfaceImp2<Integer> imp2 = new MyinterfaceImp2<>();
      		imp2.server(2000);
   ```

### 泛型方法

1. ```java
   /**
    * 泛型方法
    * 语法：<T> 返回值类型
    */
   public class MyGenericMethod {
       //泛型方法
       public <T> T show(T t){//这里void也可以改为T返回值
           System.out.println("泛型方法"+t);
           return t;
       }
   }
   ```

2. ```java
   		//泛型方法
           MyGenericMethod myGenericMethod = new MyGenericMethod();
           myGenericMethod.show("zhongguo");
           myGenericMethod.show(200);
           myGenericMethod.show(3.14);
   ```

### 泛型集合

1. 概念：参数化类型、类型安全的集合，强制集合元素的类型必须一致

2. 特点：

   - 编译时即可检查，而非运行时抛出异常
   - 访问时，不必类型转换(拆箱)
   - 不同泛型之间引用不能相互赋值，泛型不存在多态

3. ```java
   import com.Sucker.Collection.Student;
   import com.sun.org.apache.bcel.internal.generic.NEW;
   
   import java.util.ArrayList;
   import java.util.Iterator;
   
   public class Demo01 {
       public static void main(String[] args) {
           ArrayList<String> arrayList = new ArrayList<>();
           arrayList.add("xxx");
           arrayList.add("yyy");
   
           for (String string : arrayList) {
               System.out.println(string);
           }
   
           ArrayList<Student> arrayList2 = new ArrayList<>();
           Student s1 = new Student("张三", 20);
           Student s2 = new Student("KKK", 18);
           Student s3 = new Student("www", 22);
           arrayList2.add(s1);
           arrayList2.add(s2);
           arrayList2.add(s3);
           //arrayList2.add(200);限定了Student类型
   
           //迭代器
           Iterator<Student> it = arrayList2.iterator();
           while(it.hasNext()){
               Student s = it.next();
               System.out.println(s.toString());
           }
       }
   }
   ```

## Set集合

### Set集合概述

1. 特点：无序、无下标、元素不可重复
2. 方法：全部继承自Collection中的方法
3. Set实现类
   - HashSet【重点】：
     - 基于HashCode实现元素不重复
     - 当存入元素的哈希码相同时，会调用equals进行确认，如果结果为true，则拒绝后者存入
   - TreeSet
     - 基于排列顺序实现元素不重复

### Set接口使用

```java
import java.util.HashMap;
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

/**
 * 测试Set接口的使用
 * 特点：无序、不能重复
 */
public class Demo01 {
    public static void main(String[] args) {
        //创建集合
        Set<String> set = new HashSet<>();
        //1. 添加元素
        set.add("苹果");
        set.add("华为");
        set.add("小米");
        System.out.println(set.size());
        System.out.println(set.toString());
        //2.删除数据
        set.remove("小米");
        System.out.println(set.size());
        //3.遍历【重难点】
        //3.1增强for
        for (String string : set) {
            System.out.println(string);
        }
        //3.2迭代器
        Iterator<String> it = set.iterator();
        while(it.hasNext()){
            System.out.println(it.next());
        }
        //4.判断
        System.out.println(set.contains("华为"));
        System.out.println(set.isEmpty());
    }
}
```

### HashSet使用

1. ```java
   /**
    * HashSet集合的使用
    * 存储结构：哈希表(数组+链表+红黑树)
    */
   public class Demo02 {
       public static void main(String[] args) {
           //新建集合
           HashSet<String> hashSet = new HashSet<>();
           //1.添加元素
           hashSet.add("刘德华");
           hashSet.add("梁朝伟");
           hashSet.add("林志玲");
           hashSet.add("周润发");//不会添加重复的、无序
           System.out.println(hashSet.size());
           System.out.println(hashSet.toString());
           //2.删除
           hashSet.remove("刘德华");
           //hashSet.clear();
           //3.遍历操作
           //3.1增强for
           for (String string : hashSet) {
               System.out.println(string);
           }
           //3.2使用迭代器
           Iterator<String> it = hashSet.iterator();
           while(it.hasNext()){
               System.out.println(it.next());
           }
           //4.判断
           System.out.println(hashSet.contains("gi"));
           System.out.println(hashSet.isEmpty());
       }
   }
   ```

2. ```java
   /**
    * HashSet的使用
    * 存储结构：哈希表(数组+链表+红黑树)
    */
   public class Demo03 {
       public static void main(String[] args) {
           //创建集合
           HashSet<Person> persons = new HashSet<>();
           //1.添加数据
           Person p1 = new Person("刘德华",20);
           Person p2 = new Person("林志玲",22);
           Person p3 = new Person("郭富城",22);
   
           persons.add(p1);
           persons.add(p2);
           persons.add(p3);
           //persons.add(p3);重复
           persons.add(new Person("郭富城",22));//这样可以，因为在堆中地址不一样，可以重写equals来判断
   
           System.out.println(persons.size());
           System.out.println(persons.toString());
   
       }
   }
   ```

### HashSet存储方式

1. 根据hashcode计算保存位置，如果此位置为空，则直接保存，如果不为空进行第二步

2. 再执行equals方法，如果equals方法为true，则认为是重复，否则，形成链表

3. ```java
   /**
    * HashSet的使用
    * 存储结构：哈希表(数组+链表+红黑树)
    */
   public class Demo03 {
       public static void main(String[] args) {
           //创建集合
           HashSet<Person> persons = new HashSet<>();
           //1.添加数据
           Person p1 = new Person("刘德华",20);
           Person p2 = new Person("林志玲",22);
           Person p3 = new Person("郭富城",22);
   
           persons.add(p1);
           persons.add(p2);
           persons.add(p3);
           //persons.add(p3);重复
           persons.add(new Person("郭富城",22));//这样可以，因为在堆中地址不一样，可以重写equals和hashcode来判断
   
           System.out.println(persons.size());
           System.out.println(persons.toString());
   
           //2.删除操作
           persons.remove(p1);
           persons.remove(new Person("郭富城",22));//此时重写了hashcode和equals可以删掉
           
           //3.遍历【重点】
           //3.1增强for
           for (Person person : persons) {
               System.out.println(person);
           }
           //3.2迭代器
           Iterator<Person> it = persons.iterator();
           while(it.hasNext()){
               System.out.println(it.next());
           }
           //4.判断
           System.out.println(persons.contains(p1));
           System.out.println(persons.contains(new Person("林志玲",22)));//重写了，true
           
       }
   }
   ```

   ```java
       @Override
       public int hashCode() {
           int n1 = this.name.hashCode();
           int n2 = this.age;
           return n1 + n2;
       }
   
       @Override
       public boolean equals(Object o) {
           if (this == o) return true;
           if (o == null || getClass() != o.getClass()) return false;
           Person person = (Person) o;
           return age == person.age && Objects.equals(name, person.name);
       }
   ```

### HashSet补充

1. ```java
   public static int hashCode(Object a[]) {
           if (a == null)
               return 0;
   
           int result = 1;
   
           for (Object element : a)
               result = 31 * result + (element == null ? 0 : element.hashCode());
   
           return result;
       }
   ```

2. 31是一个质数，能减少散列冲突，31能提高执行效率  31*i = (i << 5) - i  i左移5位相当于i的6次方

## TreeSet

### TreeSet概述

1. 基于排列顺序实现元素不重复
2. 实现了SortedSet接口，对集合元素自动排序
3. 元素对象的类型必须实现Comparable接口，指定排序规则
4. 通过CompareTo方法确定是否为重复元素

### TreeSet的使用

1. ```java
   /**
    * TreeSet的使用
    * 存储结构：红黑树
    */
   public class Demo04 {
       public static void main(String[] args) {
           //1.创建集合
           TreeSet<String> treeSet = new TreeSet<>();
           //2.添加元素
           treeSet.add("xyz");
           treeSet.add("abc");
           treeSet.add("hello");
           treeSet.add("hello");//重复
           System.out.println(treeSet.size());
           System.out.println(treeSet.toString());
   
           //2.删除
           treeSet.remove("xyz");
           System.out.println(treeSet.size());
           //treeSet.clear();清空
   
           //3.遍历
           //3.1增强for
           for (String string : treeSet) {
               System.out.println(string);
           }
           //3.2使用迭代器
           Iterator<String> it = treeSet.iterator();
           while(it.hasNext()){
               System.out.println(it.next());
           }
           //4.判断
           System.out.println(treeSet.contains("abc"));
           System.out.println(treeSet.isEmpty());
       }
   }
   ```

2. ```java
   //先按姓名再按你年龄
       @Override
       public int compareTo(Person o) {
           int n1 = this.getName().compareTo(o.getName());
           int n2 = this.age-o.getAge();
           return n1==0 ? n2 : n1;
       }
   ```

3. ```java
   /**
    * 使用TreeSet保存数据
    * 存储结构：红黑树
    * 要求：元素必须要实现Comparable接口，重写compareTo方法判断重复，compareTo方法的返回值为0则表示重复
    */
   public class Demo05 {
       public static void main(String[] args) {
           //创建集合
           TreeSet<Person> persons = new TreeSet<>();
           //1.添加元素
           Person p1 = new Person("xyz",20);
           Person p2 = new Person("hello",22);
           Person p3 = new Person("zhangsan",22);
           Person p4 = new Person("zhangsan",20);
   
           persons.add(p1);
           persons.add(p2);
           persons.add(p3);//元素实现了Comparable接口，compareTo方法也重写了
           persons.add(p4);//名字一样比年龄来排序
           System.out.println(persons.size());
           System.out.println(persons.toString());
   
           //2.删除
           persons.remove(p1);
           persons.remove(new Person("zhangsan",20));//compareTo方法已经重写
           System.out.println(persons.toString());
   
           //3.遍历
           //3.1增强for
           for (Person person : persons) {
               System.out.println(person);
           }
           //3.2使用迭代器
           Iterator<Person> it = persons.iterator();
           while(it.hasNext()){
               System.out.println(it.next());
           }
           //4.判断
           System.out.println(persons.contains(p1));
           System.out.println(persons.contains(new Person("zhangsan",22)));
       }
   }
   ```

### Comparator接口

[(51条消息) Java Map集合利用比较器Comparator根据Key和Value的排序_X-rapido的专栏-CSDN博客](https://blog.csdn.net/xiaokui_wingfly/article/details/42964695)

1. 使用Comparator接口时可以在new对象时指定比较规则，则实现类就可以不用实现Comparable接口

2. 匿名内部类方式创建接口实现类

3. ```java
   /**
    * TreeSet集合的使用
    * Comparator：实现定制比较(比较器)
    * Comparable：可比较的
    */
   public class Demo06 {
       public static void main(String[] args) {
           //创建集合,并指定比较规则
           TreeSet<Person> persons = new TreeSet<>(new Comparator<Person>() {//匿名内部类方式创建接口实现类
               @Override
               public int compare(Person o1, Person o2) {
                   int n1 = o1.getAge()-o2.getAge();
                   int n2 = o1.getName().compareTo(o2.getName());
                   return n1==0 ? n2 : n1;
               }
           });
   
           Person p1 = new Person("xyz",20);
           Person p2 = new Person("hello",22);
           Person p3 = new Person("zhangsan",22);
   
           persons.add(p1);
           persons.add(p2);
           persons.add(p3);
           System.out.println(persons.toString());
       }
   }
   ```
   
   ```java
   //自定义排序规则，降序排序
   import java.util.*;
   // 自定义类实现Comparator
   class DescSort implements Comparator<Integer> {
       // 重写compare方法
       public int compare(Integer s1, Integer s2) {
           // 如果第一个数大于第二个数，返回负数，默认为正数
           if (s1.compareTo(s2) > 0)
               return -1;
           // 如果第一个数小于第二个数，返回正数，默认为负数
           else if (s1.compareTo(s2) < 0)
               return 1;
           // 如果第一个数等于第二个数，返回0
           else
               return 0;
       }
   }
   public class tt {
       public static void main(String[] args) {
           // 创建存储整数的TreeSet集合
           Set<Integer> set = new TreeSet<>();
           // 创建Comparator对象
           Comparator<Integer> comp = new DescSort();
           // 把Comparator对象与TreeSet对象关联
           set = new TreeSet<Integer>(comp);
           // 添加元素
           for (int i = 9; i < 14; i++)
               set.add(i);
           // 打印集合
           System.out.print(set);
       }
   }
   ```

### TreeSet案例实现

```java
/**
 * 要求：使用TreeSet集合实现字符串按照长度进行排序
 * Comparator接口实现定制比较
 */
public class Demo07 {
    public static void main(String[] args) {
        //创建集合并指定比较规则
        TreeSet<String> treeSet = new TreeSet<>(new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                int n1 = o1.length()-o2.length();
                int n2 = o1.compareTo(o2);
                return n1==0 ? n2 : n1;
            }
        });
        //添加数据
        treeSet.add("helloworld");
        treeSet.add("pingguo");
        treeSet.add("lisi");
        treeSet.add("zhangsan");
        treeSet.add("cat");
        treeSet.add("nanjing");
        treeSet.add("xian");
        System.out.println(treeSet.toString());
    }
}
```

## Map集合

### Map集合概述

1. ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210607101049.png)
2. Map父接口
   - 特点：存储一对数据(Key--Value)，无序、无下标，键不可重复，值可以重复
   - 方法：
     - V put(K key，V value)  //将对象存入到集合中，关联键值，key重复则覆盖原值
     - Object get(Object key)  //根据键获取对应的值
     - Set(K)  //返回所有key
     - Collection<V> values()  //返回包含所有值的Collection集合
     - Set<Map.Entry<K，V>>  //键值匹配的Set集合

### Map接口使用

1. 创建Mpa接口不能直接实例化

2. keySet方法遍历与entrySet方法遍历，后者为键值对，效率更高

3. ```java
   /**
    * Map接口的使用
    * 特点：1.存储键值对  2.键不能重复，值可以重复 3.无序
    */
   public class Demo01 {
       public static void main(String[] args) {
           //创建Map集合
           Map<String,String> map = new HashMap<>();//接口不能直接实例化
           //1.添加元素
           map.put("cn","中国");
           map.put("uk","英国");
           map.put("us","美国");
           map.put("cn","zhongguo");//此时不会加新的，而是将原来值中国覆盖
           System.out.println(map.size());
           System.out.println(map.toString());
   
           //2.删除
           map.remove("us");//利用key删除
           System.out.println(map.size());
           //map.clear();
   
           //3.遍历
           //3.1使用keySst();返回Set集合
           //Set<String> keyset = map.keySet();
           for (String key : map.keySet()) {//这里是简写为一行
               System.out.println(key);
               System.out.println(map.get(key));
           }
           //3.2使用entrySet()方法,得到是键值对,效率比keySet更高
           //Set<Map.Entry<String, String>> entries = map.entrySet();
           for (Map.Entry<String,String> entry : map.entrySet()) {
               System.out.println(entry.getKey()+"--"+entry.getValue());
           }
           //4.判断
           System.out.println(map.containsKey("us"));
           System.out.println(map.containsValue("泰国"));
       }
   }
   ```

### Map集合的实现类

1. HashMap【重点】
   - JDK1.2版本，线程不安全，运行效率快，允许用null作为key或是value
   - 基于哈希表的Map接口的实现。此实现提供所有可选的映射操作。此类不保证映射的顺序，特别是不保证该顺序恒久不变
   - 无参构造方法具有默认初始容量16，默认加载因子为0.75，即超过容量75%则扩容

### HashMap的使用

1. 使用key的hashcode和equals作为重复

2. ```java
   /**
    * HashMap集合的使用
    * 存储结构：哈希表(数组+链表+红黑树)
    * 使用key的hashcode和equals作为重复
    */
   public class Demo02 {
       public static void main(String[] args) {
           HashMap<Student,String> students = new HashMap<Student, String>();
           //添加元素
           Student s1 = new Student("孙悟空",100);
           Student s2 = new Student("猪八戒",101);
           Student s3 = new Student("沙师弟",102);
           students.put(s1,"北京");
           students.put(s2,"上海");//值是可以重复的
           students.put(s3,"杭州");
           students.put(new Student("沙师弟",102),"杭州");//地址不同可以加入，重写hashcode和equals后不行
           System.out.println(students.size());
           System.out.println(students.toString());
   
           //2.删除
           students.remove(s1);
           System.out.println(students.size());
           //3.遍历
           //3.1使用keySet
           for (Student key : students.keySet()) {
               System.out.println(key.toString()+"---"+students.get(key));
           }
           //3.2使用entrySet();
           for (Map.Entry<Student,String> entry : students.entrySet()) {
               System.out.println(entry.getKey()+"---"+entry.getValue());
           }
   
           //4.判断
           System.out.println(students.containsKey(new Student("沙师弟",102)));//重写后是true
           System.out.println(students.containsValue("杭州"));
       }
   }
   ```

   ```java
   	@Override
       public boolean equals(Object o) {
           if (this == o) return true;
           if (o == null || getClass() != o.getClass()) return false;
           Student student = (Student) o;
           return stuNo == student.stuNo && Objects.equals(name, student.name);
       }
   
       @Override
       public int hashCode() {
           return Objects.hash(name, stuNo);
       }
   ```

### HashMap源码分析

1. static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16  hashMap初始容量大小16
2. static final int MAXIMUM_CAPACITY = 1 << 30;  //hashMap数组最大容量2^30
3. static final float DEFAULT_LOAD_FACTOR = 0.75f;  ///默认加载因子
4. static final int TREEIFY_THRESHOLD = 8;  //JDK1.8，当链表长度大于8且数组长度大于等于64时，调整为红黑树
5. static final int UNTREEIFY_THRESHOLD = 6;  //JDK1.8，当链表程度小于6时，调整为链表
6. static final int MIN_TREEIFY_CAPACITY = 64;  //当链表长度大于8且数组长度大于等于64时，调整为红黑树
7. transient Node<K,V>[] table;  //哈希表中的数组
8. size；//元素个数
9. 刚创建hashMap后没有添加元素时table=null，size=0；达到0.75的阈值后扩容为原来两倍
10. JDK1.8以前，链表时头插入，以后便是尾插入

### Hashtable

1. JDK1.0版本，线程安全，运行效率慢，不允许null作为key或是value

### Properties

1. Hashtable的子类，要求key和value都是String。通常用于配置文件的读取

### TreeMap

1. 实现了SortedMap接口(是Map的子接口)，可以对key自动排序

2. 要求实现comparable接口

3. 重复元素会替换原来的值

4. 可以在创建集合的时候指定比较规则，实现定制比较

5. ```java
   TreeMap<Student, String> treeMap = new TreeMap<>(new Comparator<Student>(Student) {
               @Override
               public int compare(Student o1, Student o2) {
                   return 0;
               }
           });
   ```

6. ```java
   public class Student implements Comparable<Student>{
       private String name;
       private int stuNo;
   
       public Student() {
       }
   
       public Student(String name, int stuNo) {
           this.name = name;
           this.stuNo = stuNo;
       }
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       public int getStuNo() {
           return stuNo;
       }
   
       public void setStuNo(int stuNo) {
           this.stuNo = stuNo;
       }
   
       @Override
       public String toString() {
           return "Student{" +
                   "name='" + name + '\'' +
                   ", stuNo=" + stuNo +
                   '}';
       }
   
       @Override
       public boolean equals(Object o) {
           if (this == o) return true;
           if (o == null || getClass() != o.getClass()) return false;
           Student student = (Student) o;
           return stuNo == student.stuNo && Objects.equals(name, student.name);
       }
   
       @Override
       public int hashCode() {
           return Objects.hash(name, stuNo);
       }
   
       @Override
       public int compareTo(Student o) {
           int n2 = this.stuNo-o.getStuNo();
           return n2;
       }
   }
   ```

7. ```java
   public class Demo03 {
       public static void main(String[] args) {
           //创建集合
           TreeMap<Student, String> treeMap = new TreeMap<>();
           //1.添加元素
           Student s1 = new Student("孙悟空",100);
           Student s2 = new Student("猪八戒",101);
           Student s3 = new Student("沙师弟",102);
           treeMap.put(s1,"北京");
           treeMap.put(s2,"上海");//值是可以重复的
           treeMap.put(s3,"杭州");
           treeMap.put(new Student("沙师弟",102),"深圳");//不能添加进去，因为重写compareTo方法，但新的值会替换原来的
           System.out.println(treeMap.size());
           System.out.println(treeMap.toString());
   
           //2.删除
           treeMap.remove(s3);
           System.out.println(treeMap.size());
           //3.遍历
           //3.1使用keySet
           for (Student key : treeMap.keySet()) {
               System.out.println(key+"---"+treeMap.get(key));
           }
           //3.2使用entrySet
           for (Map.Entry<Student,String> entry : treeMap.entrySet()) {
               System.out.println(entry.getKey()+"---"+entry.getValue());
           }
   
           //4.判断
           System.out.println(treeMap.containsKey(new Student("沙师弟",102)));
       }
   }
   ```

## Collections工具类

1. 概念：集合工具类，定义了除了存取以外的集合常用方法

2. 方法：

   - public static void reverse(List<?> list)  //翻转集合中元素的顺序
   - public static void shuffle(List<?> list)  //随机重置集合元素的顺序
   - public static void sort(List<T> list)  //升序排序 （元素类型必须实现Comparable接口）
   - Collections.copy(dest,list);这个方法必须要求两个集合大小一样
   - 数组转成集合,此时的集合时一个受限集合，不能添加和删除元素
   - 基本数据类型不能直接转集合，要用Integer等包装类型

3. ```java
   public class Demo04 {
       public static void main(String[] args) {
           ArrayList<Integer> list = new ArrayList<>();
           list.add(20);
           list.add(5);
           list.add(12);
           list.add(30);
           list.add(6);
           //sort排序
           Collections.sort(list);
           System.out.println(list.toString());
   
           //binarySearch二分查找
           int i = Collections.binarySearch(list, 12);
           System.out.println(i);//找到下标
   
           //copy复制
           ArrayList<Integer> dest = new ArrayList<>();
           for (int j = 0; j < list.size(); j++) {
               dest.add(list.get(j));
           }
           //Collections.copy(dest,list);这个方法必须要求两个集合大小一样
           System.out.println(dest.toString());
   
           //reverse翻转
           Collections.reverse(list);
           System.out.println(list.toString());
   
           //shuffle打乱顺序
           Collections.shuffle(list);
           System.out.println(list.toString());
   
           //补充：list转成数组
           Integer[] arr = list.toArray(new Integer[0]);//后面这个0表示数组长度，如果小于list长度则直接为list的长度
           System.out.println(arr.length);
           System.out.println(Arrays.toString(arr));
   
           //数组转成集合
           String[] names={"张三","李四","王无"};
           List<String> list2 = Arrays.asList(names);
           //此时的集合时一个受限集合，不能添加和删除元素
           System.out.println(list2.toString());
   
           Integer[] nums = {100,200,300,400,500};
           List<Integer> list3 = Arrays.asList(nums);
           System.out.println(list3);
       }
   }
   ```

