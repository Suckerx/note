## JUC

## 线程和进程

### 概念

进程：一个程序，qq.exe，Music.exe  程序的集合；

一个进程往往可以包含多个线程，至少包含一个！

java默认2个线程，main和GC回收

Thread、Runnable、Callable

java无法真的开启线程，是调用本地方法，底层的C++，java无法直接操作硬件

### 并发、并行

并发编程：并发、并行

并发（多线程操作同一个资源）

- CPU 一核，模拟出多条线程，快速交替

并行（多个人一起）

- CPU 多核，多个线程可以同时执行；可用线程池提高效率

- ```java
  package com.Sucker.Demo01;
  
  public class Test1 {
      public static void main(String[] args) {
          //获取CPU的核数
          System.out.println(Runtime.getRuntime().availableProcessors());
      }
  }
  ```

并发编程的本质：充分利用CPU的资源

### 回顾多线程

**线程的状态**

```java
public enum State {
		//新生
        NEW,

        // 运行
        RUNNABLE,

        // 阻塞
        BLOCKED,

        // 等待，死死地等
        WAITING,

        //时等待
        TIMED_WAITING,

        // 终止
        TERMINATED;
    }
```

**wait / sleep**

1. 来自不同的类

   wait => Object

   sleep => Thread

2. 关于锁的释放

   wait会释放锁，sleep不会
   
3. 使用的范围不同

   wait：必须在同步代码块中使用

   sleep可以在任何地方使用

## Lock锁(重点)

### 传统 Synchronized

```java
package com.Sucker.Demo01;

//基本的卖票例子

/**
 * 真正的多线程开发，公司中的开发
 * 线程就是一个单独的资源类，没有任何的附属操作！
 * 包含：1.属性、方法
 */
public class SaleTicketDemo01 {
    public static void main(String[] args) {
        //并发
        Ticket ticket = new Ticket();

        // @FunctionalInterface  函数式接口 ，jdk1.8后，lambda表达式 (参数)->{}
        new Thread(()->{
            for (int i = 1; i < 60; i++) {
                ticket.sale();
            }
        },"A").start();

        new Thread(()->{
            for (int i = 1; i < 60; i++) {
                ticket.sale();
            }
        },"B").start();

        new Thread(()->{
            for (int i = 1; i < 60; i++) {
                ticket.sale();
            }
        },"C").start();


    }

}

// 资源类 OOP
class Ticket{
    //属性、方法
    private int number = 50;

    // 卖票的方式
    //synchronized 本质：队列，锁
    public synchronized void sale(){
        if(number>0){
            System.out.println(Thread.currentThread().getName()+"卖出了第"+(number--)+"张票,剩余："+number);
        }
    }

}
```

### Lock接口

所有已知实现类：

- ReentrantLock：可重入锁(常用)
- ReentrantReaderWriteLock.ReadLock：读锁
- ReentrantReaderWriteLock.WriteLock：写锁

```java
//源码:
public ReentrantLock() {
    sync = new NonfairSync(); // 非公平锁
}
public ReentrantLock(boolean fair) {
    sync = fair ? new FairSync() : new NonfairSync(); // 公平锁 FairSync，加参数
}
```

公平锁：十分公平，先来后到

非公平锁：十分不公平，可以插队 (默认)

使用方法：

```
lock三部曲
1.new Reentrantlock();
lock.lock(); // 加锁
finally -> lock.unlock(); // 解锁
```

```java
package com.Sucker.Demo01;

//基本的卖票例子

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/**
 * 真正的多线程开发，公司中的开发
 * 线程就是一个单独的资源类，没有任何的附属操作！
 * 包含：1.属性、方法
 */
public class SaleTicketDemo02 {
    public static void main(String[] args) {
        //并发
        Ticket2 ticket2 = new Ticket2();

        //lambda表达式
        new Thread(()->{ for (int i = 0; i < 40; i++) {ticket2.sale();} },"A").start();
        new Thread(()->{ for (int i = 0; i < 40; i++) {ticket2.sale();} },"B").start();
        new Thread(()->{ for (int i = 0; i < 40; i++) {ticket2.sale();} },"C").start();

    }

}

// 资源类 OOP
class Ticket2{
    //属性、方法
    private int number = 50;

    Lock lock = new ReentrantLock();

    // 卖票的方式
    public void sale(){

        lock.lock();//加锁

        try {
            //业务代码
            if(number>0){
                System.out.println(Thread.currentThread().getName()+"卖出了第"+(number--)+"张票,剩余："+number);
            }
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.unlock(); //解锁
        }

    }

}
```

### Synchronized 和 Lock 的区别

1. Synchronized 是内置的Java关键字 Lock是一个Java类
2. Synchronized 自动的，无法判断锁的状态 ，Lock 可以判断是否获取到了锁
3. Synchronized 会自动释放锁，Lock 必须要手动释放锁！如果不释放锁，会**死锁**
4. Synchronized 线程1(获得锁，阻塞)、线程2(等待，一直等)，Lock锁就不一定会等下去
5. Synchronized 可重入锁，不可以中断的，非公平；Lock 可重入锁，可以判断锁，非公平(可以自己设置)
6. Synchronized 适合锁少量的代码同步问题，Lock 适合锁大量的同步代码

## 生产者和消费者问题

### Synchronized版   wait  notify

```java
package com.Sucker.pc;

/**
 * 线程之间的通信问题：生产者和消费者问题！  等待唤醒，通知唤醒
 * 线程交替执行 A   B  操作同一个变量  num = 0
 * A num + 1
 * B num - 1
 */
public class A {
    public static void main(String[] args) {
        Data data = new Data();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    data.increment();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"A").start();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    data.decrement();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"B").start();

    }

}

// 判断等待，业务，通知
class Data{ //数字，资源类

    private int number = 0;

    //+1
    public synchronized void increment() throws InterruptedException {
        if(number!=0){ // 0
            // 等待
            this.wait();
        }
        number++;
        System.out.println(Thread.currentThread().getName()+"->"+number);
        // 通知其他线程，+1完毕
        this.notifyAll();
    }

    //-1
    public synchronized void decrement() throws InterruptedException {
        if (number==0){  // 1
            // 等待
            this.wait();
        }
        number--;
        System.out.println(Thread.currentThread().getName()+"->"+number);
        // 通知其他线程，-1完毕
        this.notifyAll();
    }

}
```

**出现得问题：虚假唤醒：线程可以唤醒，而不会被通知，中断或超时**

解决方法：将wait等待改在循环中，if改为while

### JUC版生产者消费者问题

通过Lock找到Condition，其中有await和signal

Lock替换Synchronized方法和语句得使用，Condition取代了对象监视器方法的使用

```java
package com.Sucker.pc;

import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/**
 * 线程之间的通信问题：生产者和消费者问题！  等待唤醒，通知唤醒
 * 线程交替执行 A   B  操作同一个变量  num = 0
 * A num + 1
 * B num - 1
 */
public class B {
    public static void main(String[] args) {
        Data2 data = new Data2();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    data.increment();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"A").start();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    data.decrement();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"B").start();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    data.increment();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"C").start();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    data.decrement();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"D").start();

    }

}

// 判断等待，业务，通知
class Data2{ //数字，资源类

    private int number = 0;

    Lock lock = new ReentrantLock();
    Condition condition = lock.newCondition();
//    condition.await();
//    condition.signalAll();


    //+1
    public void increment() throws InterruptedException {
        lock.lock();
        try {
            //业务代码
            while(number!=0){ // 0
                // 等待
                condition.await();
            }
            number++;
            System.out.println(Thread.currentThread().getName()+"->"+number);
            // 通知其他线程，+1完毕
            condition.signalAll();
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }

    }

    //-1
    public synchronized void decrement() throws InterruptedException {
        lock.lock();
        try {
            //业务代码
            while(number==0){ // 1
                // 等待
                condition.await();
            }
            number--;
            System.out.println(Thread.currentThread().getName()+"->"+number);
            // 通知其他线程，+1完毕
            condition.signalAll();
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }

}
```

**任何一个新的技术，绝对不仅仅是覆盖原来的技术，一定有优势和补充**

### Condition 精准通知和唤醒线程(线程有序执行)

```java
package com.Sucker.pc;

import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/**
 * @author 扶苏
 * A执行完 调用B B执行完调用C C执行完调用A
 */

public class C {
    public static void main(String[] args) {
        Data3 data = new Data3();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                data.printA();
            }
        },"A").start();
        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                data.printB();
            }
        },"B").start();
        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                data.printC();
            }
        },"C").start();

    }
}

class Data3{ //资源类
    private Lock lock = new ReentrantLock();
    private Condition condition1 = lock.newCondition();
    private Condition condition2 = lock.newCondition();
    private Condition condition3 = lock.newCondition();
    private int number = 1; // 1A  2B  3C

    public void printA(){
        lock.lock();
        try {
            // 业务 -》 判断 -》执行
            while(number!=1){
                // 等待
                condition1.await();
            }
            System.out.println(Thread.currentThread().getName()+"->AAAAA");
            // 唤醒  唤醒指定的B
            number = 2;
            condition2.signal();
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }
    public void printB(){
        lock.lock();
        try {
            // 业务 -》 判断 -》执行
            while (number!=2){
                //等待
                condition2.await();
            }
            System.out.println(Thread.currentThread().getName()+"->BBBBB");
            // 唤醒
            number = 3;
            condition3.signal();
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }
    public void printC(){
        lock.lock();
        try {
            // 业务 -》 判断 -》执行
            while (number!=3){
                //等待
                condition3.await();
            }
            System.out.println(Thread.currentThread().getName()+"->CCCCC");
            // 唤醒
            number = 1;
            condition1.signal();
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }

}
```

## 八锁现象彻底理解锁

1. 标准情况下，两个线程先打印 发短信还是打电话  结果：1.发短信 2.打电话

2. sendSms延迟4秒，两个线程先打印，发短信还是打电话   1.发短信  2. 打电话

   ```
   //synchronized  锁的对象是方法的调用者
   //两个方法用的是同一把锁，谁先拿到谁执行
   ```

```java
package com.Sucker.lock8;

import java.util.concurrent.TimeUnit;

/**
 * 8锁，关于锁的8个问题
 * 1.标准情况下，两个线程先打印 发短信还是打电话  结果：1.发短信 2.打电话
 */
public class Test1 {
    public static void main(String[] args) {
        Phone phone = new Phone();

        new Thread(()->{
            phone.sendSms();
        },"A").start();

        try {//休眠一秒
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        new Thread(()->{
            phone.call();
        },"B").start();

    }

}

class Phone{

    //synchronized  锁的对象是方法的调用者
    //两个方法用的是同一把锁，谁先拿到谁执行

    public synchronized void sendSms(){
        try {
            TimeUnit.SECONDS.sleep(4);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("sendSms");
    }

    public synchronized void call(){
        System.out.println("call");
    }

}
```

3. 增加了一个普通方法，先打印 发短信还是打电话  结果：普通方法先，因为没加锁且另一个方法有延迟4秒

4. 两个对象，两个同步方法，此时打电话，因为发短信有延迟4秒

```
* 2.增加了一个普通方法，先打印 发短信还是打电话  结果：普通方法先，因为没加锁且另一个方法有延迟4秒
* 3.两个对象，两个同步方法，此时打电话，因为发短信有延迟4秒
```

```java
package com.Sucker.lock8;

import java.util.concurrent.TimeUnit;

/**
 * 8锁，关于锁的8个问题
 * 2.增加了一个普通方法，先打印 发短信还是打电话  结果：普通方法先，因为没加锁且另一个方法有延迟4秒
 * 3.两个对象，两个同步方法，此时打电话，因为发短信有延迟4秒
 */
public class Test2 {
    public static void main(String[] args) {
        Phone2 phone1 = new Phone2();
        Phone2 phone2 = new Phone2();

        new Thread(()->{
            phone1.sendSms();
        },"A").start();

        try {//休眠一秒
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        new Thread(()->{
            phone2.call();
        },"B").start();

    }

}

class Phone2{

    //synchronized  锁的对象是方法的调用者
    public synchronized void sendSms(){
        try {
            TimeUnit.SECONDS.sleep(4);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("sendSms");
    }

    public synchronized void call(){
        System.out.println("call");
    }

    //这里没有锁，不是同步方法，不受锁的影响
    public void hello(){
        System.out.println("hello");
    }

}
```

5. 增加两个静态的同步方法 一个对象，先打印 发短信还是打电话？ 先执行的先输出
6. 两个对象  增加两个静态的同步方法 一个对象，先打印 发短信还是打电话？  加了static，锁的是Class

```
* 5.增加两个静态的同步方法 一个对象，先打印 发短信还是打电话？ 先执行的先输出
* 6.两个对象  增加两个静态的同步方法  先打印 发短信还是打电话？  加了static，锁的是Class
```

```java
package com.Sucker.lock8;

import java.util.concurrent.TimeUnit;

/**
 * 8锁，关于锁的8个问题
 * 5.增加两个静态的同步方法 一个对象，先打印 发短信还是打电话？ 先执行的先输出
 * 6.两个对象  增加两个静态的同步方法  先打印 发短信还是打电话？  加了static，锁的是Class
 */
public class Test3 {
    public static void main(String[] args) {
        //两个对象的Class类模板只有一个！ 加了static，锁的是Class
        Phone3 phone1 = new Phone3();
        Phone3 phone2 = new Phone3();

        new Thread(()->{
            phone1.sendSms();
        },"A").start();

        try {//休眠一秒
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        new Thread(()->{
            phone2.call();
        },"B").start();

    }

}

// Phone3唯一的一个Class 对象
class Phone3{

    //synchronized  锁的对象是方法的调用者
    //static 静态方法
    // 类一加载就有了！锁的是Class
    //两个方法用的是同一把锁，谁先拿到谁执行
    public static synchronized void sendSms(){
        try {
            TimeUnit.SECONDS.sleep(4);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("sendSms");
    }

    public static synchronized void call(){
        System.out.println("call");
    }

    //这里没有锁，不是同步方法，不受锁的影响
    public void hello(){
        System.out.println("hello");
    }

}
```

7. 1个静态的同步方法，1个普通的同步方法  1个对象，还是先打印打电话，因为是普通同步方

8. 1个静态的同步方法，1个普通的同步方法  2个对象，还是先打印打电话，因为两把锁，第二个普通同步方法走的是第二个锁

```java
package com.Sucker.lock8;

import java.util.concurrent.TimeUnit;

/**
 * 8锁，关于锁的8个问题
 * 7.1个静态的同步方法，1个普通的同步方法  1个对象，还是先打印打电话，因为是普通同步方法
 * 8.1个静态的同步方法，1个普通的同步方法  2个对象，还是先打印打电话，因为两把锁，第二个普通同步方法走的是第二个锁
 */
public class Test4 {
    public static void main(String[] args) {
        //两个对象的Class类模板只有一个！ 加了static，锁的是Class
        Phone4 phone1 = new Phone4();
        Phone4 phone2 = new Phone4();

        new Thread(()->{
            phone1.sendSms();
        },"A").start();

        try {//休眠一秒
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        new Thread(()->{
            phone2.call();
        },"B").start();

    }

}

// Phone3唯一的一个Class 对象
class Phone4{

    //静态的同步方法
    public static synchronized void sendSms(){
        try {
            TimeUnit.SECONDS.sleep(4);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("sendSms");
    }

    //普通的同步方法
    public synchronized void call(){
        System.out.println("call");
    }

}
```

**小结**

new  this  具体的一个对象

static  Class  唯一的一个模板

## 集合类不安全

### List不安全

```java
package com.Sucker.unsafe;

import java.sql.Array;
import java.util.*;
import java.util.concurrent.CopyOnWriteArrayList;

// java.util.ConcurrentModificationException  并发修改异常
public class ListTest {
    public static void main(String[] args) {
        //并发下  ArrayList  不安全
        /**
         * 解决方案：
         * 1.List<String> list = new Vector<>(); Vector默认安全
         * 2.List<String> list = Collections.synchronizedList(new ArrayList<>());
         */
        //CopyOnWrite  写入时复制  COW  计算机程序设计领域的一种优化策略
        // 多个线程调用时，List，读取的时候，固定的，写入(覆盖)
        // 在写入时避免覆盖，造成数据问题!
        // 读写分离
        // CopyOnWriteArrayList 比 Vector 优秀在效率更高 Vector用了Synchronized 而 CWAL用的是Lock锁

        List<String> list = new CopyOnWriteArrayList<>();

        for (int i = 1; i <= 10; i++) {
            new Thread(()->{
                list.add(UUID.randomUUID().toString().substring(0,5));
                System.out.println(list);
            },String.valueOf(i)).start();
        }
    }

}
```

### Set不安全

```java
package com.Sucker.unsafe;

import java.awt.peer.CanvasPeer;
import java.util.Collections;
import java.util.HashSet;
import java.util.Set;
import java.util.UUID;
import java.util.concurrent.CopyOnWriteArraySet;

/**
 * 同理可证：ConcurrentModificationException
 * 解决方案：
 * 1.工具类：Set<String> set = Collections.synchronizedSet(new HashSet<>());
 * 2.Set<String> set = new CopyOnWriteArraySet<>();
 */
public class SetTest {
    public static void main(String[] args) {
        //Set<String> set = new HashSet<>();
        //Set<String> set = Collections.synchronizedSet(new HashSet<>());
        Set<String> set = new CopyOnWriteArraySet<>();

        for (int i = 1; i <= 30; i++) {
            new Thread(()->{
                set.add(UUID.randomUUID().toString().substring(0,5));
                System.out.println(set);
            },String.valueOf(i)).start();
        }

    }
}
```

hashset的底层：

```java
public HashSet() {
    map = new HashMap<>();
}

// set.add 本质是 map 的key是无法重复的
public boolean add(E e) {
    return map.put(e, PRESENT)==null;
}
```

### Map不安全

```java
//默认值
static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16

static final int MAXIMUM_CAPACITY = 1 << 30;

static final float DEFAULT_LOAD_FACTOR = 0.75f;
```

```java
package com.Sucker.unsafe;

import java.util.*;
import java.util.concurrent.ConcurrentHashMap;

public class MapTest {
    public static void main(String[] args) {
        //默认值：Map<String, String> map = new HashMap<>(16,0.75);
        //解决方案：1.Map<String, String> map = Collections.synchronizedMap(new HashMap<>());
        //2.Map<String, String> map = new ConcurrentHashMap<>();
        //此处需要研究ConcurrentHashMap的原理
        Map<String, String> map = new ConcurrentHashMap<>();

        for (int i = 1; i <= 30; i++) {
            new Thread(()->{
                map.put(Thread.currentThread().getName(), UUID.randomUUID().toString().substring(0,5));
                System.out.println(map);
            },String.valueOf(i)).start();
        }

    }
}
```

[ConcurrentHashMap原理,以及在jdk7和jdk8版本的区别-KuangStudy-文章](https://www.kuangstudy.com/bbs/1384802904245817346)

## Callable

### 概述

Callable接口类似于Runnable，因为它们都是为其实例可能由另一个线程执行的类设计的。然而，Runnable不返回结果，也不能抛出被检查的异常

1. 可以有返回值
2. 可以抛出异常
3. 方法不同 run()/call()

Thread  与  Runnable  有关，现在想用Callable，那么需要将其与Runnable联系

Runnable接口中，其实现类有FutureTask，而FutureTask就与Callable有关，由此联系

```java
package com.Sucker.callable;


import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

public class CallableTest {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        // new Thread(new Runnable()).start();
        // new Thread(new FutureTask<V>()).start();
        // new Thread(new FutureTask<V>( Callable )).start();
        new Thread().start();//如何启动Callable

        MyThread thread = new MyThread();
        FutureTask futureTask = new FutureTask(thread);//适配类
        new Thread(futureTask,"A").start();

        Integer o = (Integer) futureTask.get(); //获取Callable的返回结果
        System.out.println(o);

    }

}

class MyThread implements Callable<Integer> {
    @Override
    public Integer call() {
        System.out.println("call()");
        return 1024;
    }
}
```

```java
Integer o = (Integer) futureTask.get();//这个get方法可能会产生阻塞，所以将他方到最后
//因为获取返回值这步可能是耗时操作
//或者使用异步通信
```

若两个线程执行两次，结果会被缓存，只输出一次

```java
package com.Sucker.callable;


import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

public class CallableTest {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        // new Thread(new Runnable()).start();
        // new Thread(new FutureTask<V>()).start();
        // new Thread(new FutureTask<V>( Callable )).start();
        new Thread().start();//如何启动Callable

        MyThread thread = new MyThread();
        FutureTask futureTask = new FutureTask(thread);//适配类
        new Thread(futureTask,"A").start();
        new Thread(futureTask,"B").start();//结果会被缓存，只输出一次

        Integer o = (Integer) futureTask.get(); //获取Callable的返回结果
        System.out.println(o);

    }

}

class MyThread implements Callable<Integer> {
    @Override
    public Integer call() {
        System.out.println("call()");
        return 1024;
    }
}
```

**细节：**

1. 有缓存
2. 结果可能需要等待，会阻塞！

## 常用的辅助类（必会）

### CountDownLatch

```java
package com.Sucker.add;

import java.util.concurrent.CountDownLatch;

//计数器
public class CountDownLatchDemo {
    public static void main(String[] args) throws InterruptedException {
        //参数表示总数  当有必须要执行的任务时使用
        CountDownLatch countDownLatch = new CountDownLatch(6);

        for (int i = 1; i <= 6; i++) {
            new Thread(()->{
                System.out.println(Thread.currentThread().getName()+"go out");
                countDownLatch.countDown();//数量-1
            },String.valueOf(i)).start();
        }

        countDownLatch.await(); // 等待计数器归零，然后再向下执行

        System.out.println("close door");

    }

}
```

原理：

- countDownLatch.countDown();//数量-1
- countDownLatch.await(); // 等待计数器归零，然后再向下执行

### CyclicBarrier

允许一组线程全部等待彼此达到共同屏障点的同步辅助。（加法计数器）

CyclicBarrier也叫同步屏障，在JDK1.5被引入，可以让一组线程达到一个屏障时被阻塞，直到最后一个线程达到屏障时，所以被阻塞的线程才能继续执行。
 CyclicBarrier好比一扇门，默认情况下关闭状态，堵住了线程执行的道路，直到所有线程都就位，门才打开，让所有线程一起通过。

```java
package com.Sucker.add;

import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierDemo {
    public static void main(String[] args) {
        /**
         * 集齐七颗龙珠召唤神龙
         */
        //CyclicBarrier这里参数为int 和 Runnable
        CyclicBarrier cyclicBarrier = new CyclicBarrier(7,()->{
            System.out.println("召唤神龙成功");//达到7个线程执行完才能执行这句话
        });

        for (int i = 1; i <= 7; i++) {
            final int temp = i;//通过final才能在线程里面拿到i
            new Thread(()->{
                System.out.println(Thread.currentThread().getName()+"收集"+temp+"个龙珠");
                try {
                    cyclicBarrier.await();//等待，计数
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } catch (BrokenBarrierException e) {
                    e.printStackTrace();
                }
            }).start();
        }

    }
}
```

### Semaphore

Semaphore：信号量

Semaphore也叫信号量，在JDK1.5被引入，可以用来控制同时访问特定资源的线程数量，通过协调各个线程，以保证合理的使用资源。

Semaphore内部维护了一组虚拟的许可，许可的数量可以通过构造函数的参数指定。

- 访问特定资源前，必须使用acquire方法获得许可，如果许可数量为0，该线程则一直阻塞，直到有可用许可。
- 访问资源后，使用release释放许可。

Semaphore和ReentrantLock类似，获取许可有公平策略和非公平许可策略，默认情况下使用非公平策略。

```java
package com.Sucker.add;

import java.util.concurrent.Semaphore;
import java.util.concurrent.TimeUnit;

public class SemaphoreDemo {
    public static void main(String[] args) {
        // 参数：线程数量：停车位 限流！
        Semaphore semaphore = new Semaphore(3);

        for (int i = 1; i <= 6; i++) {
            new Thread(()->{
                // acquire() 得到
                try {
                    semaphore.acquire();
                    System.out.println(Thread.currentThread().getName()+"抢到车位");
                    TimeUnit.SECONDS.sleep(2);//停两秒
                    System.out.println(Thread.currentThread().getName()+"离开车位");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }finally {
                    semaphore.release();// release() 释放
                }
            },String.valueOf(i)).start();
        }

    }
}
```

**原理：**

- semaphore.acquire(); 获得，假如已经满了，等待，等待被释放为止！
- semaphore.release(); 释放，会将当前的信号释放+1，然后唤醒等待的线程

作用：多个共享资源互斥的使用！并发限流，控制最大线程数

## ReadWriteLock（读写锁）

ReadWriteLock接口只有一个实现类：ReentrantReadWriteLock

ReadWriteLock维护一对关联的Locks，一个用于只读，一个用于写入。read lock 可以由多个阅读器线程同时进行，只要没有作者。write lock是独家的

```java
package com.Sucker.rw;

import sun.management.ThreadInfoCompositeData;

import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

/**
 * ReadWriteLock
 * 独占锁（写锁）
 * 共享锁（读锁）
 * 读-读  可以共存
 * 读-写  不可共存！
 * 写-写  不可共存！
 */
public class ReadWriteLockDemo {
    public static void main(String[] args) {
        MyCacheLock myCache = new MyCacheLock();

        //写入
        for (int i = 1; i <= 5; i++) {
            final int temp = i;//中间变量
            new Thread(()->{
                myCache.put(temp+"",temp+"");
            },String.valueOf(i)).start();
        }

        //读取
        for (int i = 1; i <= 5; i++) {
            final int temp = i;//中间变量
            new Thread(()->{
                myCache.get(temp+"");
            },String.valueOf(i)).start();
        }

    }
}

//加锁
class MyCacheLock{

    private volatile Map<String,Object> map = new HashMap<>();
    //读写锁: 更加细粒度的控制
    private ReadWriteLock readWriteLock = new ReentrantReadWriteLock();

    //存、写入的时候只希望同时只有一个线程写
    public void put(String key,Object value){
        readWriteLock.writeLock().lock();
        try {
            System.out.println(Thread.currentThread().getName()+"写入"+key);
            map.put(key, value);
            System.out.println(Thread.currentThread().getName()+"写入完成");
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            readWriteLock.writeLock().unlock();
        }
    }

    //取、读 所有人都可以读
    public void get(String key){
        readWriteLock.readLock().lock();
        try {
            System.out.println(Thread.currentThread().getName()+"读取"+key);
            Object o = map.get(key);
            System.out.println(Thread.currentThread().getName()+"读取完成");
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            readWriteLock.readLock().unlock();
        }

    }

}


/**
 * 自定义缓存
 */

class MyCache{

    private volatile Map<String,Object> map = new HashMap<>();

    //存、写
    public void put(String key,Object value){
        System.out.println(Thread.currentThread().getName()+"写入"+key);
        map.put(key, value);
        System.out.println(Thread.currentThread().getName()+"写入完成");
    }

    //取、读
    public void get(String key){
        System.out.println(Thread.currentThread().getName()+"读取"+key);
        Object o = map.get(key);
        System.out.println(Thread.currentThread().getName()+"读取完成");
    }

}
```

## 阻塞队列BlockingQueue

BlockQueue不是新东西

什么情况下我们会使用  阻塞队列：多线程并发处理，线程池！

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210731160327.png)

### 四组API

| 方式         | 抛出异常  | 不会抛出异常，有返回值 | 阻塞等待 | 超时等待      |
| ------------ | --------- | ---------------------- | -------- | ------------- |
| 添加         | add       | offer()空参            | put()    | offer(,,)有参 |
| 移除         | remove    | poll()空参             | take()   | poll(,)有参   |
| 检测队首元素 | element() | peek()                 | -        | -             |

抛出异常

```java
package com.Sucker.bq;

import java.util.concurrent.ArrayBlockingQueue;

public class Test {
    public static void main(String[] args) {
        //父类 Collection
        // List
        // Set
        test1();
    }

    /**
     * 抛出异常
     */
    public static void test1(){
        //参数是队列的大小
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(3);

        System.out.println(blockingQueue.add("a"));
        System.out.println(blockingQueue.add("b"));
        System.out.println(blockingQueue.add("c"));

        //  IllegalStateException:Queue full  抛出异常!
        //System.out.println(blockingQueue.add("d"));
        
        System.out.println(blockingQueue.element());//取队首元素

        System.out.println(blockingQueue.remove());
        System.out.println(blockingQueue.remove());
        System.out.println(blockingQueue.remove());

        //  NoSuchElementException 抛出异常
        //System.out.println(blockingQueue.remove());

    }

}
```

不抛出异常，有返回值

```java
package com.Sucker.bq;

import java.util.concurrent.ArrayBlockingQueue;

public class Test {
    public static void main(String[] args) {
        //父类 Collection
        // List
        // Set
        test2();
    }
    
    public void test2(){
        //参数是队列的大小
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(3);

        System.out.println(blockingQueue.offer("a"));
        System.out.println(blockingQueue.offer("b"));
        System.out.println(blockingQueue.offer("c"));
        
        System.out.println(blockingQueue.peek());//检测队首元素

        //System.out.println(blockingQueue.offer("d"));//返回一个boolean值，不抛出异常

        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll());//null 不抛出异常

    }

}
```

阻塞等待

```java
package com.Sucker.bq;

import java.util.concurrent.ArrayBlockingQueue;

public class Test {
    public static void main(String[] args) throws InterruptedException {
        //父类 Collection
        // List
        // Set
        test3();
    }

    /**
     * 等待，阻塞(一直阻塞)
     */
    public static void test3() throws InterruptedException {
        //参数是队列的大小
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(3);

        //一直阻塞
        blockingQueue.put("a");
        blockingQueue.put("b");
        blockingQueue.put("c");
        blockingQueue.put("c");// 队列满，一直阻塞

        System.out.println(blockingQueue.take());
        System.out.println(blockingQueue.take());
        System.out.println(blockingQueue.take());
        System.out.println(blockingQueue.take());//队列空，一直阻塞

    }


    /**
     * 等待，阻塞(等待超时)
     */

}
```

超时等待

```java
package com.Sucker.bq;

import com.sun.media.sound.SoftFilter;

import java.sql.Time;
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.TimeUnit;

public class Test {
    public static void main(String[] args) throws InterruptedException {
        //父类 Collection
        // List
        // Set
        test4();
    }

    /**
     * 等待，阻塞(等待超时)
     */
    public static void test4() throws InterruptedException {
        //参数是队列的大小
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(3);

        blockingQueue.offer("a");
        blockingQueue.offer("b");
        blockingQueue.offer("c");
        blockingQueue.offer("d",2, TimeUnit.SECONDS);//等待超过2秒就退出

        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll());
        blockingQueue.poll(2, TimeUnit.SECONDS);//超过2秒就退出

    }

}
```

### SynchronousQueue 同步队列

没有容量，进去一个元素必须等待取出后才能再放

put、take

```java
package com.Sucker.bq;

import java.util.concurrent.BlockingDeque;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.SynchronousQueue;
import java.util.concurrent.TimeUnit;

/**
 * 同步队列
 * 与其他BlockingQueue 不同 ，SynchronousQueue 不存储元素
 * put了一个元素，必须从里面先take出来，否则不能put
 */
public class SynchronousQueueDemo {
    public static void main(String[] args) {
        BlockingQueue<String> blockingQueue = new SynchronousQueue<>(); //同步队列

        new Thread(()->{
            try {
                System.out.println(Thread.currentThread().getName()+"put 1");
                blockingQueue.put("1");
                System.out.println(Thread.currentThread().getName()+"put 2");
                blockingQueue.put("2");
                System.out.println(Thread.currentThread().getName()+"put 3");
                blockingQueue.put("3");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"T1").start();

        new Thread(()->{
            try {
                TimeUnit.SECONDS.sleep(3);//让put线程先put进去
                System.out.println(Thread.currentThread().getName()+blockingQueue.take());
                TimeUnit.SECONDS.sleep(3);//让put线程先put进去
                System.out.println(Thread.currentThread().getName()+blockingQueue.take());
                TimeUnit.SECONDS.sleep(3);//让put线程先put进去
                System.out.println(Thread.currentThread().getName()+blockingQueue.take());
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"T2").start();

    }

}
```

## 线程池(重点)

**线程池：三大方法、7大参数、4种拒绝策略**

### 池化技术

程序的运行：占用系统的资源！ 优化资源的使用！-》 池化技术

线程池、连接池、内存池、对象池///...  创建和销毁十分浪费资源

池化技术：事先准备好一些资源，要用就来拿，用完再还

**线程池的好处：**

1. 降低资源的消耗
2. 提高相应的速度
3. 方便管理

**线程复用、可以控制最大并发数、管理线程**

### 线程池：三大方法

【强制】线程池不允许使用 Executors 去创建，而是通过 ThreadPoolExecutor 的方式，这样 的处理方式让写的同学更加明确线程池的运行规则，规避资源耗尽的风险。

说明：Executors 返回的线程池对象的弊端如下：

- 1）FixedThreadPool 和 SingleThreadPool:
  - 允许的请求队列长度为 Integer.MAX_VALUE，可能会堆积大量的请求，从而导致 OOM。
- CachedThreadPool 和 ScheduledThreadPool：
  - 允许的创建线程数量为 Integer.MAX_VALUE，可能会创建大量的线程，从而导致 OOM。

```java
package com.Sucker.pool;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

// Executors 工具类，3大方法
// 使用了线程池之后，使用线程池来创建线程
public class Demo01 {
    public static void main(String[] args) {
        //ExecutorService threadPool = Executors.newSingleThreadExecutor();//单个线程
        ExecutorService threadPool = Executors.newFixedThreadPool(5);//创建一个固定的线程池的大小
//        Executors.newCachedThreadPool();//可伸缩的

        try {
            for (int i = 0; i < 10; i++) {
                threadPool.execute(()->{
                    System.out.println(Thread.currentThread().getName()+"ok");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //线程池用完，程序结束，关闭线程池
            threadPool.shutdown();
        }

    }
}
```

### 7大参数

源码分析：

```java
public static ExecutorService newSingleThreadExecutor() {
    return new FinalizableDelegatedExecutorService
        (new ThreadPoolExecutor(1, 1,
                                0L, TimeUnit.MILLISECONDS,
                                new LinkedBlockingQueue<Runnable>()));
}

public static ExecutorService newFixedThreadPool(int nThreads) {
    return new ThreadPoolExecutor(nThreads, nThreads,
                                  0L, TimeUnit.MILLISECONDS,
                                  new LinkedBlockingQueue<Runnable>());
}

public static ExecutorService newCachedThreadPool() {
    return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                  60L, TimeUnit.SECONDS,
                                  new SynchronousQueue<Runnable>());
}

//本质：ThreadPoolExecutor
public ThreadPoolExecutor(int corePoolSize, //核心线程池大小
                          int maximumPoolSize, // 最大核心线程池大小
                          long keepAliveTime, // 超时了没人调用就会释放
                          TimeUnit unit, // 超时单位
                          BlockingQueue<Runnable> workQueue, // 阻塞队列
                          ThreadFactory threadFactory, // 线程工厂，创建线程的，一般不用动
                          RejectedExecutionHandler handler) { // 拒绝策略
    if (corePoolSize < 0 ||
        maximumPoolSize <= 0 ||
        maximumPoolSize < corePoolSize ||
        keepAliveTime < 0)
        throw new IllegalArgumentException();
    if (workQueue == null || threadFactory == null || handler == null)
        throw new NullPointerException();
    this.acc = System.getSecurityManager() == null ?
        null :
    AccessController.getContext();
    this.corePoolSize = corePoolSize;
    this.maximumPoolSize = maximumPoolSize;
    this.workQueue = workQueue;
    this.keepAliveTime = unit.toNanos(keepAliveTime);
    this.threadFactory = threadFactory;
    this.handler = handler;
}
```

![](https://img-blog.csdnimg.cn/20210414112748609.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FuZW5hbg==,size_16,color_FFFFFF,t_70)

7大参数与自定义线程池

```java
package com.Sucker.pool;

import java.util.concurrent.*;

// Executors 工具类，3大方法
// 使用了线程池之后，使用线程池来创建线程

/**
 * 四种拒绝策略
 * new ThreadPoolExecutor.AbortPolicy());// 这种策略下，银行满了，还有人进来，不处理并抛出异常
 * new ThreadPoolExecutor.CallerRunsPolicy()); // 哪儿来的回哪里去执行，这里会回到main线程执行
 * new ThreadPoolExecutor.DiscardPolicy()); // 队列满了，丢掉任务，但不会抛出异常
 * new ThreadPoolExecutor.DiscardOldestPolicy()); // 队列满了，尝试去和最早的竞争，失败了也丢掉，也不会抛出异常
 */
public class Demo01 {
    public static void main(String[] args) {
        //自定义线程池！ 工作中只会使用  ThreadPoolExecutor
        ExecutorService threadPool = new ThreadPoolExecutor(
                2,
                5,
                3,
                TimeUnit.SECONDS,
                new LinkedBlockingQueue<>(3),//候客区，最多3个
                Executors.defaultThreadFactory(),
                new ThreadPoolExecutor.DiscardOldestPolicy()); // 队列满了，尝试去和最早的竞争，失败了也丢掉，也不会抛出异常

        try {
            //最大承载：Queue + max
            for (int i = 1; i <= 9; i++) {
                threadPool.execute(()->{
                    System.out.println(Thread.currentThread().getName()+"ok");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //线程池用完，程序结束，关闭线程池
            threadPool.shutdown();
        }

    }
}
```

### 四种拒绝策略

```java
/**
 * 四种拒绝策略
 * new ThreadPoolExecutor.AbortPolicy());// 这种策略下，银行满了，还有人进来，不处理并抛出异常
 * new ThreadPoolExecutor.CallerRunsPolicy()); // 哪儿来的回哪里去执行，这里会回到main线程执行
 * new ThreadPoolExecutor.DiscardPolicy()); // 队列满了，丢掉任务，但不会抛出异常
 * new ThreadPoolExecutor.DiscardOldestPolicy()); // 队列满了，尝试去和最早的竞争，失败了也丢掉，也不会抛出异常
 */
```

### CPU密集型和IO密集型

池的最大大小如何设置

```java
//最大线程该如何定义？
//1. CPU 密集型 几核 ，就可以定义为几 可以保持CPU的效率最高
//System.out.println(Runtime.getRuntime().availableProcessors()); 获取CPU数量
//2. IO 密集型  判断程序中十分消耗IO资源的线程数量，设置大于其即可
```

## 四大函数式接口(必须掌握)

### 函数式接口：只有一个方法的接口

```java
public interface Runnable {
    public abstract void run();
}

//foreach(消费者类的函数式接口)
```

四大函数式接口：Consumer、Function、Predicate、Supplier

### Function函数式接口

有一个输入参数，有一个输出

源码：

```java
public interface Function<T, R> { // 传入参数T 返回类型R
    R apply(T t);
}
```

```java
package com.Sucker.function;

import java.util.function.Function;

/**
 * Function 函数型接口 有一个输入参数，有一个输出
 * 只要是 函数型接口 可以 用lambda表达式简化
 */
public class Demo01 {
    public static void main(String[] args) {
//        Function<String,String> function = new Function<String,String>() {
//            @Override
//            public String apply(String str) {
//                return str;
//            }
//        };

        Function function = (str)->{return str;};

        System.out.println(function.apply("asd"));

    }
}
```

### Predicate断定型接口

有一个输入参数，返回值只能是 布尔值！

```java
package com.Sucker.function;

import java.util.function.Predicate;

/**
 * 断定型接口，有一个输入参数，返回值只能是 布尔值！
 */
public class Demo02 {
    public static void main(String[] args) {
//        Predicate<String> predicate = new Predicate<String>() {
//            // 可以是 判断字符串是否为空
//            @Override
//            public boolean test(String str) {
//                return str.isEmpty();
//            }
//        };

        Predicate<String> predicate =(str)->{return str.isEmpty();};

        System.out.println(predicate.test("sa"));

    }
}
```

### Consumer 消费型接口

只有输入没有返回值

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```

```java
package com.Sucker.function;

import java.util.function.Consumer;

/**
 * Consumer 消费型接口，只有输入，没有返回值
 */
public class Demo03 {
    public static void main(String[] args) {
//        Consumer<String> consumer = new Consumer<String>() {
//            @Override
//            public void accept(String str) {
//                System.out.println(str);
//            }
//        };
        Consumer<String> consumer = (str)->{ System.out.println(str);};
        consumer.accept("aaaa");
    }
}
```

### Supplier 供给型接口

供给型接口 没有参数，只有返回值

```java
@FunctionalInterface
public interface Supplier<T> {
    T get();
}
```

```java
package com.Sucker.function;

import java.util.function.Supplier;

/**
 * Supplier 供给型接口 没有参数，只有返回值
 */
public class Demo04 {
    public static void main(String[] args) {
//        Supplier<Integer> spplier = new Supplier<Integer>() {
//            @Override
//            public Integer get() {
//                System.out.println("Get");
//                return 1024;
//            }
//        };

        Supplier<Integer> spplier = ()->{return 1024;};
        System.out.println(spplier.get());

    }
}
```

## Stream流式计算

```java
package com.Sucker.stream;

import java.nio.file.attribute.UserDefinedFileAttributeView;
import java.util.Arrays;
import java.util.List;

/**
 * 题目要求：一分钟完成，只能用一行代码实现
 * 现在存在5个用户！筛选
 * 1. ID 必须是偶数
 * 2. 年龄必须大于23岁
 * 3. 用户名转为大写
 * 4. 用户名字母倒序
 * 5. 只能输出一个用户！
 */
public class Test {
    public static void main(String[] args) {
        User u1 = new User(1,"a",21);
        User u2 = new User(2,"b",22);
        User u3 = new User(3,"c",23);
        User u4 = new User(4,"d",24);
        User u5 = new User(6,"e",25);

        //集合就是存储
        List<User> list = Arrays.asList(u1, u2, u3, u4, u5);

        //计算交给Stream流
        //lambda表达式、链式编程、函数式接口、Stream流式计算
        list.stream()
                .filter(u->{return u.getId()%2==0;})
                .filter(u->{return u.getAge()>23;})
                .map(u->{return u.getName().toUpperCase();})
                .sorted((uu1,uu2)->{return uu2.compareTo(uu1);})
                .limit(1)
                .forEach(System.out::println);

    }

}
```

## ForkJoin

分支合并，在JDK1.7时出现，并行执行任务，提高效率，大数据量

ForkJoin特点：工作窃取

这里面维护的都是双端队列 ，某个线程执行完毕了可以将另外没有执行完毕的线程的任务拿过来执行，提升效率

ForkJoinTask类其中有两个实现类

- RecursiveAction：递归事件，没有返回值
- RecursiveTask：递归任务，有返回值

测试代码：

计算类：

```java
package com.Sucker.forkjoin;

import java.util.concurrent.RecursiveTask;

/**
 * 求和计算的任务
 * ForkJoin   Stream并行流
 *  如何使用 forkjoin
 *  1. new ForkJoinPool 通过它来执行
 *  2. 计算任务 ForkJoin.execute(ForkJoinTask task)或submit
 *  3. 计算类要继承 ForkJoinTask，RecursiveTask是ForkJoinTask的子类
 */
public class ForkJoinDemo extends RecursiveTask<Long> {

    private Long start;
    private Long end;

    //临界值
    private Long temp = 10000L;

    public ForkJoinDemo(Long start, Long end) {
        this.start = start;
        this.end = end;
    }

    //计算方法
    @Override
    protected Long compute() {
        if((end-start)<temp){
            Long sum = 0L;
            for (Long i = start; i <= end; i++) {
                sum+=i;
            }
            return sum;
        }else {//forkjoin 递归
            long middle = (start+end)/2; //中间值
            ForkJoinDemo task1 = new ForkJoinDemo(start, middle);
            task1.fork(); // 拆分任务，把任务压入线程队列
            ForkJoinDemo task2 = new ForkJoinDemo(middle+1, end);
            task2.fork(); // 拆分任务，把任务压入线程队列
            return task1.join()+task2.join();

        }
    }

}
```

测试类：

```java
package com.Sucker.forkjoin;

import java.util.concurrent.ExecutionException;
import java.util.concurrent.ForkJoinPool;
import java.util.concurrent.ForkJoinTask;
import java.util.stream.LongStream;

public class Test {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        //test1(); // 6358
        //test2(); // 4243 可以更快，temp临界值可以动态调整
        test3(); // 177
    }

    //普通
    public static void test1(){
        long start = System.currentTimeMillis();
        Long sum = 0L;
        for (Long i = 1L; i <=10_0000_0000 ; i++) {
            sum+=i;
        }
        long end = System.currentTimeMillis();
        System.out.println("sum="+sum+"时间"+(end-start));
    }

    //使用ForkJoin
    public static void test2() throws ExecutionException, InterruptedException {
        long start = System.currentTimeMillis();

        ForkJoinPool forkJoinPool = new ForkJoinPool();
        ForkJoinTask<Long> task = new ForkJoinDemo(0L, 10_0000_0000L);
        //forkJoinPool.execute(task); // 没有返回值
        ForkJoinTask<Long> submit = forkJoinPool.submit(task);//提交任务
        Long sum = submit.get();

        long end = System.currentTimeMillis();
        System.out.println("sum="+sum+"时间"+(end-start));

    }

    public static void test3(){
        long start = System.currentTimeMillis();
        //Stream 并行流
        long sum = LongStream.rangeClosed(0L, 10_0000_0000).parallel().reduce(0, Long::sum);
        long end = System.currentTimeMillis();
        System.out.println("sum="+sum+"时间"+(end-start));

    }

}
```

## 异步回调

Future 设计的初衷：对将来的某个事件的结果进行建模

其中有实现类：CompletableFuture<T>

```java
package com.Sucker.future;

import java.awt.peer.CanvasPeer;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.TimeUnit;

/**
 * 异步调用： CompletableFuture
 * // 异步执行
 * // 成功回调
 * // 失败回调
 */
public class Demo01 {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        //发起请求
        // 没有返回值的 runAsync 异步回调
//        CompletableFuture<Void> completableFuture = CompletableFuture.runAsync(()->{
//            try {
//                TimeUnit.SECONDS.sleep(2);
//            } catch (InterruptedException e) {
//                e.printStackTrace();
//            }
//            System.out.println(Thread.currentThread().getName()+"runAsync=>void");
//        });
//
//        System.out.println("1111");
//
//        completableFuture.get(); // 获取阻塞执行结果

        // 有返回值的  supplyAsync 异步回调
        // 成功和失败回调，失败返回错误信息
        CompletableFuture<Integer> completableFuture = CompletableFuture.supplyAsync(()->{
            System.out.println(Thread.currentThread().getName()+"supplyAsync=>Integer");
            return 1024;
        });

        System.out.println(completableFuture.whenComplete((t,u)->{
            System.out.println("t->"+t);// 正常的返回结果
            System.out.println("u->"+u);// 错误信息
        }).exceptionally((e)->{
            System.out.println(e.getMessage());
            return 233; // 可以获取到错误的返回结果
        }).get());

    }

}
```

## JMM

### Volatile

Volatile 是Java虚拟机提供的**轻量级的同步机制**

1. 保证可见性
2. **不保证原子性**
3. 禁止指令重排

### JMM概述

JMM：Java内存模型，不存在的东西，概念！约定

**关于JMM的一些同步的约定**

1. 线程解锁前，必须把共享变量**立刻**刷新回主存
2. 线程加锁前，必须读取主存中的最新值到工作内存中！
3. 加锁和解锁是同一把锁

8种操作：

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210803165258.png)

![](https://img-blog.csdnimg.cn/6953da2ee6aa43678858c6ae016e1f36.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

### 内存划分

参考：[java内存模型JMM理解整理 - 阿姆斯特朗回旋炮 - 博客园 (cnblogs.com)](https://www.cnblogs.com/null-qige/p/9481900.html)

JMM规定了内存主要划分为主内存和工作内存两种。此处的主内存和工作内存跟JVM内存划分（堆、栈、方法区）是在不同的层次上进行的，如果非要对应起来，主内存对应的是Java堆中的对象实例部分，工作内存对应的是栈中的部分区域，从更底层的来说，主内存对应的是硬件的物理内存，工作内存对应的是寄存器和高速缓存。

![](https://images2018.cnblogs.com/blog/1102674/201808/1102674-20180815143324915-2024156794.png)

JVM在设计时候考虑到，如果JAVA线程每次读取和写入变量都直接操作主内存，对性能影响比较大，所以每条线程拥有各自的工作内存，工作内存中的变量是主内存中的一份拷贝，线程对变量的读取和写入，直接在工作内存中操作，而不能直接去操作主内存中的变量。但是这样就会出现一个问题，当一个线程修改了自己工作内存中变量，对其他线程是不可见的，会导致线程不安全的问题。因为JMM制定了一套标准来保证开发者在编写多线程程序的时候，能够控制什么时候内存会被同步给其他线程。

### 内存交互操作

**内存交互操作有8种，虚拟机实现必须保证每一个操作都是原子的，不可在分的（对于double和long类型的变量来说，load、store、read和write操作在某些平台上允许例外）**

- lock   （锁定）：作用于主内存的变量，把一个变量标识为线程独占状态

- unlock （解锁）：作用于主内存的变量，它把一个处于锁定状态的变量释放出来，释放后的变量才可以被其他线程锁定
- read  （读取）：作用于主内存变量，它把一个变量的值从主内存传输到线程的工作内存中，以便随后的load动作使用
- load   （载入）：作用于工作内存的变量，它把read操作从主存中变量放入工作内存中
- use   （使用）：作用于工作内存中的变量，它把工作内存中的变量传输给执行引擎，每当虚拟机遇到一个需要使用到变量的值，就会使用到这个指令
- assign （赋值）：作用于工作内存中的变量，它把一个从执行引擎中接受到的值放入工作内存的变量副本中
- store  （存储）：作用于主内存中的变量，它把一个从工作内存中一个变量的值传送到主内存中，以便后续的write使用
- write 　（写入）：作用于主内存中的变量，它把store操作从工作内存中得到的变量的值放入主内存的变量中

**JMM对这八种指令的使用，制定了如下规则：**

- 不允许read和load、store和write操作之一单独出现。即使用了read必须load，使用了store必须write

- 不允许线程丢弃他最近的assign操作，即工作变量的数据改变了之后，必须告知主存
- 不允许一个线程将没有assign的数据从工作内存同步回主内存
- 一个新的变量必须在主内存中诞生，不允许工作内存直接使用一个未被初始化的变量。就是怼变量实施use、store操作之前，必须经过assign和load操作
- 一个变量同一时间只有一个线程能对其进行lock。多次lock后，必须执行相同次数的unlock才能解锁
- 如果对一个变量进行lock操作，会清空所有工作内存中此变量的值，在执行引擎使用这个变量前，必须重新load或assign操作初始化变量的值
- 如果一个变量没有被lock，就不能对其进行unlock操作。也不能unlock一个被其他线程锁住的变量
- 对一个变量进行unlock操作之前，必须把此变量同步回主内存

JMM对这八种操作规则和对[volatile的一些特殊规则](https://www.cnblogs.com/null-qige/p/8569131.html)就能确定哪里操作是线程安全，哪些操作是线程不安全的了。但是这些规则实在复杂，很难在实践中直接分析。所以一般我们也不会通过上述规则进行分析。更多的时候，使用java的happen-before规则来进行分析。

**当一个线程修改了主内存中的值时，另外的线程不能收到**

测试代码：

```java
package com.Sucker.testvolatile;

import java.util.concurrent.TimeUnit;

public class JMMDemo {

    private static int num = 0;
    public static void main(String[] args) { // main 线程

        new Thread(()->{
            while(num==0){}
        }).start();

        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        num = 1;
        System.out.println(num);

    }
}
```

此时输出1，但是程序一直不停止

## Volatile

### 保证可见性

```java
package com.Sucker.testvolatile;

import java.util.concurrent.TimeUnit;

public class JMMDemo {
    // 不加volatile 程序会死循环
    // 加 volatile 可以保证可见性
    private volatile static int num = 0;
    public static void main(String[] args) { // main 线程

        new Thread(()->{
            while(num==0){}
        }).start();

        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        num = 1;
        System.out.println(num);

    }
}
```

### 不保证原子性

原子性：不可分割

- 线程A在执行任务的时候，不能被打扰的，也不能被分割。要么同时成功，要么同时失败

```java
package com.Sucker.testvolatile;

// 不保证原子性
public class VDemo02 {

    // volatile 不保证原子性，结果仍然无法达到20000
    private volatile static int num = 0;

    public static void add(){
        num++;
    }

    public static void main(String[] args) {
        //理论上num结果应该为20000
        for (int i = 1; i <= 20; i++) {
            new Thread(()->{
                for (int j = 0; j < 1000; j++) {
                    add();
                }
            }).start();
        }
        //判断存活的线程数量>2就继续礼让，否则算是执行完毕 >2是因为main 和 gc
        while(Thread.activeCount()>2) Thread.yield(); // 表示只要还有其他线程，主线程就礼让给它

        System.out.println(num);
    }

}
```

**如果不加lock或synchronized，如何保证原子性**

使用原子类，解决原子性问题（atomic）

```java
package com.Sucker.testvolatile;

import java.util.concurrent.atomic.AtomicInteger;

// 不保证原子性
public class VDemo02 {

    // volatile 不保证原子性，结果仍然无法达到20000
    // 原子类的Integer
    private volatile static AtomicInteger num = new AtomicInteger();

    public static void add(){
        //num++; // 不是一个原子性操作
        num.getAndIncrement(); // AtomicInteger + 1 的方法  CAS
    }

    public static void main(String[] args) {
        //理论上num结果应该为20000
        for (int i = 1; i <= 20; i++) {
            new Thread(()->{
                for (int j = 0; j < 1000; j++) {
                    add();
                }
            }).start();
        }
        //判断存活的线程数量>2就继续礼让，否则算是执行完毕 >2是因为main 和 gc
        while(Thread.activeCount()>2) Thread.yield(); // 表示只要还有其他线程，主线程就礼让给它

        System.out.println(num);
    }

}
```

这些类的底层都和操作系统挂钩！在内存中修改值，Unsafe类是一个很特殊的存在！

### 禁止指令重排

指令重排：**写的程序，计算机并不是按照写的那样去执行**

源代码-->编译器优化的重排-->指令并行也可能会重排-->内存系统也会重排-->执行

**处理器在进行指令重排时，考虑：数据之间的依赖性**

```java
int x = 1; // 1
int y = 2; // 2
x = x + 5; // 3
y = x * x; // 4

我们所期望的：1234  但是可能执行的时候是：2134  1324
但不可能是 4123！
```

可能造成影响的结果   a b x y 四个值默认都是0

| 线程A | 线程B |
| ----- | ----- |
| x = a | y = b |
| b = 1 | a = 2 |

正常的结果：x = 0 ；y = 0；但是可能由于指令重排，

| 线程A | 线程B |
| ----- | ----- |
| b = 1 | a = 2 |
| x = a | y = b |

指令重排导致的异常结果：x = 2；y = 1；

**volatile可以避免指令重排**

内存屏障。CPU指令。作用：

1. 保证特定的操作的执行顺序！
2. 可以保证某些变量的内存可见性(利用这些特性volatile实现了可见性)

## 单例模式

### 概述

参考：[单例模式（单例设计模式）详解 (biancheng.net)](http://c.biancheng.net/view/1338.html)

在有些系统中，为了节省内存资源、保证数据内容的一致性，对某些类要求只能创建一个实例，这就是所谓的单例模式。

### 单例模式的定义与特点

单例（Singleton）模式的定义：指一个类只有一个实例，且该类能自行创建这个实例的一种模式。例如，Windows 中只能打开一个任务管理器，这样可以避免因打开多个任务管理器窗口而造成内存资源的浪费，或出现各个窗口显示内容的不一致等错误。

在计算机系统中，还有 Windows 的回收站、操作系统中的文件系统、多线程中的线程池、显卡的驱动程序对象、打印机的后台处理服务、应用程序的日志对象、数据库的连接池、网站的计数器、Web 应用的配置对象、应用程序中的对话框、系统中的缓存等常常被设计成单例。

单例模式在现实生活中的应用也非常广泛，例如公司 CEO、部门经理等都属于单例模型。J2EE 标准中的 [Servlet](http://c.biancheng.net/servlet/)Context 和 ServletContextConfig、[Spring](http://c.biancheng.net/spring/) 框架应用中的 ApplicationContext、数据库中的连接池等也都是单例模式。

单例模式有 3 个特点：

1. 单例类只有一个实例对象；
2. 该单例对象必须由单例类自行创建；
3. 单例类对外提供一个访问该单例的全局访问点。

### 单例模式的优点和缺点

单例模式的优点：

- 单例模式可以保证内存里只有一个实例，减少了内存的开销。
- 可以避免对资源的多重占用。
- 单例模式设置全局访问点，可以优化和共享资源的访问。


单例模式的缺点：

- 单例模式一般没有接口，扩展困难。如果要扩展，则除了修改原来的代码，没有第二种途径，违背开闭原则。
- 在并发测试中，单例模式不利于代码调试。在调试过程中，如果单例中的代码没有执行完，也不能模拟生成一个新的对象。
- 单例模式的功能代码通常写在一个类中，如果功能设计不合理，则很容易违背单一职责原则。

> 单例模式看起来非常简单，实现起来也非常简单。单例模式在面试中是一个高频面试题。希望大家能够认真学习，掌握单例模式，提升核心竞争力，给面试加分，顺利拿到 Offer。

### 单例模式的结构与实现

单例模式是[设计模式](http://c.biancheng.net/design_pattern/)中最简单的模式之一。通常，普通类的构造函数是公有的，外部类可以通过“new 构造函数()”来生成多个实例。但是，如果将类的构造函数设为私有的，外部类就无法调用该构造函数，也就无法生成多个实例。这时该类自身必须定义一个静态私有实例，并向外提供一个静态的公有函数用于创建或获取该静态私有实例。

### 饿汉式

```java
package com.Sucker.single;

// 饿汉式单例
public class Hungry {

    // 可能会浪费空间
    private byte[] data1 = new byte[1024*1024];
    private byte[] data2 = new byte[1024*1024];
    private byte[] data3 = new byte[1024*1024];
    private byte[] data4 = new byte[1024*1024];

    private Hungry(){ //构造器私有，别人无法new对象

    }

    private final static Hungry HUNGRY = new Hungry();

    public static Hungry getInstance(){
        return HUNGRY;
    }

}
```

### DCL懒汉式

```java
package com.Sucker.single;

// 懒汉式单例
public class LazyMan {

    private LazyMan(){
        System.out.println(Thread.currentThread().getName()+"ok");
    }

    private volatile static LazyMan lazyMan;

    // 双重检测锁模式的  懒汉式单例  简称DCL懒汉式
    public static LazyMan getInstance(){
        if(lazyMan==null){
            synchronized (LazyMan.class){
                if(lazyMan==null){
                    lazyMan = new LazyMan(); // 极端情况下还是会出问题，因为不是原子性操作(指的是上面的if会被影响)
                }
            }
        }
        return lazyMan;
    }

    /**
     * 1，分配内存空间
     * 2. 执行构造方法，初始化对象
     * 3. 把这个对象指向这个空间
     *
     * 期望执行 123
     * 实际可能 132
     * 两个线程 A先成功 B来的时候先指向了空间，判断就会lazyMan！=null，然后直接return
     * 此时还没有完成构造
     * 所以为了避免这种情况，需要加上volatile
     */

    // 多线程并发
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            new Thread(()->{
                LazyMan.getInstance();
            }).start();
        }
    }

}
```

### DCL懒汉式反射破坏

```java
package com.Sucker.single;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;

// 懒汉式单例
public class LazyMan2 {

    private static boolean sucker = false;

    private LazyMan2(){
        synchronized (LazyMan2.class){
            if(sucker==false) sucker = true;
            else throw new RuntimeException("不要试图使用反射破坏异常");
        }
    }

    private volatile static LazyMan2 lazyMan;

    // 双重检测锁模式的  懒汉式单例  简称DCL懒汉式
    public static LazyMan2 getInstance(){
        if(lazyMan==null){
            synchronized (LazyMan2.class){
                if(lazyMan==null){
                    lazyMan = new LazyMan2(); // 极端情况下还是会出问题，因为不是原子性操作(指的是上面的if会被影响)
                }
            }
        }
        return lazyMan;
    }

    // 反射破坏安全!
    public static void main(String[] args) throws Exception {
//        LazyMan instance = LazyMan.getInstance();

        Field sucker = LazyMan2.class.getDeclaredField("sucker");
        sucker.setAccessible(true);// 破坏私有权限

        Constructor<LazyMan2> declaredConstructor = LazyMan2.class.getDeclaredConstructor(null);//空参构造器
        declaredConstructor.setAccessible(true); // 无视私有构造器
        LazyMan2 instance = declaredConstructor.newInstance();//反射创建对象

        sucker.set(instance,false);

        LazyMan2 instance2 = declaredConstructor.newInstance();//反射创建对象

        System.out.println(instance);
        System.out.println(instance2);

    }

}
```

### 静态内部类

```java
package com.Sucker.single;

//静态内部类
public class Holder {

    private Holder(){

    }

    public static Holder getInstance(){
        return InnerClass.HOLDER;
    }

    public static class InnerClass{
        private static final Holder HOLDER = new Holder();
    }

}
```

**单例不安全，因为有反射**

### 枚举

```java
package com.Sucker.single;

import java.lang.reflect.Constructor;

// enum 枚举 本身也是一个 Class类
public enum EnumSingle {

    INSTANCE;

    public EnumSingle getInstance(){
        return INSTANCE;
    }

}

class Test{

    public static void main(String[] args) throws Exception {
        EnumSingle instance1 = EnumSingle.INSTANCE;
        //这里源码有问题，实际上是有参构造
        Constructor<EnumSingle> declaredConstructor = EnumSingle.class.getDeclaredConstructor(String.class,int.class);
        declaredConstructor.setAccessible(true);
        EnumSingle instance2 = declaredConstructor.newInstance();

        // NoSuchMethodException  没有这个无参构造方法
        //Cannot reflectively create enum objects 不能通过反射
        System.out.println(instance1);
        System.out.println(instance2);

    }

}
```

**枚举类型的最终反编译是有参构造，枚举可以防止反射破坏单例**

## 深入理解CAS

### Unsafe类

Java无法操作内存，但是Java可以调用C++(native)，C++可以操作内存，Unsafe类相当于Java的后门，可以通过它操作内存

```java
package com.Sucker.cas;

import java.util.concurrent.atomic.AtomicInteger;

public class CASDemo {

    // CAS  compareAndSet  比较并交换
    public static void main(String[] args) {
        AtomicInteger atomicInteger = new AtomicInteger(2020);

        // 参数为 期望 、更新
        //public final boolean compareAndSet(int expect, int update)
        // 如果我期望的值达到了 ，那么就更新，否则就不更新  CAS 是CPU的并发原语！
        System.out.println(atomicInteger.compareAndSet(2020, 2021));//true
        System.out.println(atomicInteger.get());

        System.out.println(atomicInteger.compareAndSet(2020, 2021));//false
        System.out.println(atomicInteger.get());

    }

}
```



```java
public final int getAndIncrement() {
    return unsafe.getAndAddInt(this, valueOffset, 1);
}

public final int getAndAddInt(Object var1, long var2, int var4) {
    int var5;
    do {
        var5 = this.getIntVolatile(var1, var2); //获取内存地址的值
    } while(!this.compareAndSwapInt(var1, var2, var5, var5 + var4));//若满足期望var5，就+1
	//这是一个自旋锁
    return var5;
}
```

CAS：比较当前工作内存中的值和主内存中的值，如果这个值是期望的，那么执行操作！如果不是就一直循环

**缺点：**

1. 循环会耗时
2. 一次性只能保证一个共享变量的原子性
3. 会导致ABA问题

### CAS：ABA问题

第二个线程将1换成3再换回1，而第一个线程仍然以为是原来的1

![](https://img-blog.csdnimg.cn/c3bb8585c14f43b5ae4bf01bfc2b61ce.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

```java
package com.Sucker.cas;

import java.util.concurrent.atomic.AtomicInteger;

public class CASDemo {

    // CAS  compareAndSet  比较并交换
    public static void main(String[] args) {
        AtomicInteger atomicInteger = new AtomicInteger(2020);

        // 参数为 期望 、更新
        //public final boolean compareAndSet(int expect, int update)
        // 如果我期望的值达到了 ，那么就更新，否则就不更新  CAS 是CPU的并发原语！
        //==========捣乱的线程=============
        System.out.println(atomicInteger.compareAndSet(2020, 2021));
        System.out.println(atomicInteger.get());

        System.out.println(atomicInteger.compareAndSet(2021, 2020));
        System.out.println(atomicInteger.get());

        //============== 期望的线程 ================
        System.out.println(atomicInteger.compareAndSet(2020, 6666));
        System.out.println(atomicInteger.get());

    }

}
```

## 原子引用

### 乐观锁与悲观锁

悲观锁(Pessimistic Lock), 顾名思义，就是很悲观，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会block直到它拿到锁。

乐观锁(Optimistic Lock), 顾名思义，就是很乐观，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号等机制。乐观锁适用于多读的应用类型，这样可以提高吞吐量，像数据库如果提供类似于write_condition机制的其实都是提供的乐观锁。

 两种锁各有优缺点，不可认为一种好于另一种，像乐观锁适用于写比较少的情况下，即冲突真的很少发生的时候，这样可以省去了锁的开销，加大了系统的整个吞吐量。但如果经常产生冲突，上层应用会不断的进行retry，这样反倒是降低了性能，所以这种情况下用悲观锁就比较合适

### 原子引用解决ABA问题：乐观锁

带版本号的原子操作，可以知道其他线程操作了资源

```java
package com.Sucker.cas;

import java.util.concurrent.TimeUnit;
import java.util.concurrent.atomic.AtomicInteger;
import java.util.concurrent.atomic.AtomicStampedReference;

public class CASDemo {

    // CAS  compareAndSet  比较并交换
    public static void main(String[] args) {
//        AtomicInteger atomicInteger = new AtomicInteger(2020);
        // 参数有两个，一个是期望值  一个是时间戳(版本号)

        // AtomicStampedReference 注意：如果泛型是一个包装类，注意对象的引用问题
        // 正常的业务，里面比较的是一个个的对象
        AtomicStampedReference<Integer> atomicStampedReference = new AtomicStampedReference<Integer>(1,1);

        new Thread(()->{
            int stamp = atomicStampedReference.getStamp();//获得当前版本号
            System.out.println("a1->"+stamp);

            try {
                TimeUnit.SECONDS.sleep(2);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            System.out.println(atomicStampedReference.compareAndSet(1, 2,
                    atomicStampedReference.getStamp(), atomicStampedReference.getStamp() + 1));

            System.out.println("a2->"+atomicStampedReference.getStamp());

            System.out.println(atomicStampedReference.compareAndSet(2, 1,
                    atomicStampedReference.getStamp(), atomicStampedReference.getStamp() + 1));

            System.out.println("a3->"+atomicStampedReference.getStamp());

        },"a").start();

        // 乐观锁的原理相同
        new Thread(()->{
            int stamp = atomicStampedReference.getStamp();//获得当前版本号
            System.out.println("b1->"+stamp);

            try {
                TimeUnit.SECONDS.sleep(2); // 保证两个线程刚开始拿到的是同一个版本号
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            System.out.println(atomicStampedReference.compareAndSet(1, 6,
                    stamp, stamp + 1));

            System.out.println("b2->"+atomicStampedReference.getStamp());

        },"b").start();

    }

}
```

**Integer的一个大坑**

所有的相同类型的包装类对象之间值的比较，全部使用 equals 方法比较。 说明：对于 Integer var = ? 在-128 至 127 范围内的赋值，Integer 对象是在 IntegerCache.cache 产生，会复用已有对象，这个区间内的 Integer 值可以直接使用==进行 判断，但是这个区间之外的所有数据，都会在堆上产生，并不会复用已有对象，这是一个大坑， 推荐使用 equals 方法进行判断。

而 compareAndSet 方法中就是使用==进行判断

## 各种锁的理解

### 公平锁、非公平锁

公平锁：非常公平，不能插队，必须先来后到

非公平锁：非常不公平，可以插队 (默认都是非公平) 

上方Lock锁有解释

### 可重入锁

可重入锁（递归锁）

![](https://img-blog.csdnimg.cn/b91394ff737c47e6a4b0482b45a5d48b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

可重入锁是一种特殊的互斥锁，它可以被同一个线程多次获取，而不会产生死锁。

1. 首先它是互斥锁：任意时刻，只有一个线程锁。即假设A线程已经获取了锁，在A线程释放这个锁之前，B线程是无法获取到这个锁的，B要获取这个锁就会进入阻塞状态。

2. 其次，它可以被同一个线程多次持有。即，假设A线程已经获取了这个锁，如果A线程在释放锁之前又一次请求获取这个锁，那么是能够获取成功的。

举例说明：

``` java

public class LockTest {
public synchronized void lockA() {
lockB(); //lockA方法中调用lockB方法

}

public synchronized void lockB() {
System.out.println("lock B");

}

}

```

如上面的的代码所示，假如我们要调用lockA方法，而lockA方法又要调用lockB方法，并且这两个方法上都有synchronized关键字，即两个方法都会以类对象作为锁，所以两个方法是同一把锁，如果没有可重入锁的机制，那么这个方法就无法被正确执行。另外可以想象一下，假如我们有一个递归方法，而这个方法是需要加锁的，如果没有可重入锁的机制，加锁的递归方法也是不能实现的。这就是为什么要有可重入锁。

> Synchronized版

```java
package com.Sucker.lock;

// Synchronized
public class Demo1 {
    public static void main(String[] args) {
        Phone phone = new Phone();

        new Thread(()->{
            phone.sms();
        },"A").start();

        new Thread(()->{
            phone.sms();
        },"B").start();

    }
}

class  Phone{
    public synchronized void sms(){
        System.out.println(Thread.currentThread().getName()+"sms");
        call();
    }

    public synchronized void call(){
        System.out.println(Thread.currentThread().getName()+"call");
    }

}
```

> Lock版

```java
package com.Sucker.lock;

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class Demo02 {
    public static void main(String[] args) {
        Phone2 phone = new Phone2();

        new Thread(()->{
            phone.sms();
        },"A").start();

        new Thread(()->{
            phone.sms();
        },"B").start();

    }
}

class  Phone2{
    Lock lock = new ReentrantLock();

    public void sms(){

        lock.lock();
        try {
            System.out.println(Thread.currentThread().getName()+"sms");
            call();
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }

    public synchronized void call(){

        lock.lock();// 细节问题：这里相当于两把锁，锁必须要配对，否则会死锁
        try {
            System.out.println(Thread.currentThread().getName()+"call");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

}
```



### 自旋锁

spinlock

```java
public final int getAndAddInt(Object var1, long var2, int var4) {
    int var5;
    do {
        var5 = this.getIntVolatile(var1, var2); //获取内存地址的值
    } while(!this.compareAndSwapInt(var1, var2, var5, var5 + var4));//若满足期望var5，就+1
	//这是一个自旋锁
    return var5;
}
```

自定义测试锁:

```java
package com.Sucker.lock;

import java.util.concurrent.atomic.AtomicReference;

public class SpinLockDemo {

    //通过原子引用来

    // 若是int 默认为0
    // Thread 默认为null
    AtomicReference<Thread> atomicReference = new AtomicReference<>();

    // 加锁
    public void myLock(){
        Thread thread = Thread.currentThread();
        System.out.println(Thread.currentThread().getName()+"-> mylock");

        // 自旋锁
        while (!atomicReference.compareAndSet(null,thread)){

        }

    }


    // 解锁
    public void myUnLock(){
        Thread thread = Thread.currentThread();
        System.out.println(Thread.currentThread().getName()+"-> myUnlock");
        atomicReference.compareAndSet(thread,null);

    }

}
```

测试代码：

```java
package com.Sucker.lock;

import java.sql.Time;
import java.util.concurrent.TimeUnit;

public class TestSpinLock {
    public static void main(String[] args) throws InterruptedException {

        // 底层使用自旋锁CAS
        SpinLockDemo lock = new SpinLockDemo();

        new Thread(()->{
            lock.myLock();
            try {
                TimeUnit.SECONDS.sleep(5);
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                lock.myUnLock();
            }
        },"T1").start();

        TimeUnit.SECONDS.sleep(1); // 保证T1先拿到锁

        new Thread(()->{
            lock.myLock(); // 虽然会执行输出那句话，但是还是会阻塞等待T1解锁
            try {
                TimeUnit.SECONDS.sleep(1);
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                lock.myUnLock();
            }
        },"T2").start();

    }

}
```

结果：

T1-> mylock
T2-> mylock
T1-> myUnlock
T2-> myUnlock

```java
// Thread 默认为null ，传入的默认值null
AtomicReference<Thread> atomicReference = new AtomicReference<>();
```

lock（)方法利用的CAS，当第一个线程A获取锁的时候，能够成功获取到，不会进入while循环，如果此时线程A没有释放锁，另一个线程B又来获取锁，此时由于不满足CAS，所以就会进入while循环，不断判断是否满足CAS，直到A线程调用unlock方法释放了该锁。

### 死锁

回顾多线程篇

> 死锁测试：

```java
package com.Sucker.lock;

import java.util.concurrent.TimeUnit;

public class DeadLockDemo {
    public static void main(String[] args) {

        String lockA = "lockA";
        String lockB = "lockB";

        new Thread(new MyThread(lockA,lockB),"T1").start();
        new Thread(new MyThread(lockB,lockA),"T2").start();

    }

}

class MyThread implements Runnable{

    private String lockA;
    private String lockB;

    public MyThread(String lockA, String lockB) {
        this.lockA = lockA;
        this.lockB = lockB;
    }

    @Override
    public void run() {
        synchronized (lockA){
            System.out.println(Thread.currentThread().getName()+"lock:"+lockA+"->get"+lockB);

            try {
                TimeUnit.SECONDS.sleep(2);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            synchronized (lockB){
                System.out.println(Thread.currentThread().getName()+"lock:"+lockB+"->get"+lockA);
            }
        }
    }
}
```

结果：

T1lock:lockA->getlockB
T2lock:lockB->getlockA  且程序不停止

> 解决问题：

1. 使用`jps -l`命令定位进程号

   ```java
   D:\JavaCode\JavaSE\JUC>jps -l
   15024 sun.tools.jps.Jps
   11832
   15064 com.Sucker.lock.DeadLockDemo
   22588 org.jetbrains.jps.cmdline.Launcher
   ```

2. 使用`jstack 进程号`找到死锁问题

   ```java
   Java stack information for the threads listed above:
   ===================================================
   "T2":
           at com.Sucker.lock.MyThread.run(DeadLockDemo.java:40)
           - waiting to lock <0x000000076b2c5ad0> (a java.lang.String)//等待获得
           - locked <0x000000076b2c5b08> (a java.lang.String)//c
           at java.lang.Thread.run(Thread.java:748)
   "T1":
           at com.Sucker.lock.MyThread.run(DeadLockDemo.java:40)
           - waiting to lock <0x000000076b2c5b08> (a java.lang.String)//等待去获得
           - locked <0x000000076b2c5ad0> (a java.lang.String)//持有
           at java.lang.Thread.run(Thread.java:748)
   
   Found 1 deadlock.
   ```

   