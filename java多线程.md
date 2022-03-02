## 多线程

## 线程、进程、多线程

### 普通方法调用和多线程

1. 主线程调用run方法，只有主线程一条路径
2. 主线程调用start()，子线程执行run方法，多条执行路径，主线程和子线程并行交替执行

### 程序.进程.线程

一个进程可以有多个线程，如视频中同时听到声音、看图像、看弹幕等

### Process与Thread

- 说起进程，就不得不说程序。程序是指令和数据的有序集合，其本身没有任何运行的含义，是一个静态的概念
- 而进程则是执行程序的一次执行过程，它是一个动态的概念。是系统资源分配的单位
- 通常一个进程中可以包含若干个线程，当然一个进程中至少一个线程，不然没有存在的意义。线程是CPU调度和执行的单位
- 注意：很多多线程是模拟出来的，真正的多线程是指有多个CPU，即多核，如服务器。如果是模拟出来的多线程，即在一个cpu的情况下，在同一个时间点，cpu只能执行一个代码，因为切换的很快，所以就有同时执行的错觉

### 核心概念

- 线程就是独立的执行路径
- 在程序运行时，即使没有自己创建线程，后台也会有多个线程，如主线程，gc线程
- main()称之为主线程，为系统的入口，用于执行整个程序
- 在一个进程中，如果开辟了多个线程，线程的运行由调度器安排调度，调度器是与操作系统紧密相关的，先后顺序是不能人为干预的
- 对同一份资源操作时，会存在资源抢夺的问题，需要加入并发控制
- 线程会带来额外的开销，如cpu调度时间，并发控制开销
- 每个线程在自己的工作内存交互，内存控制不当会造成数据不一致

## 线程创建

### 三种创建方式

- Thread class ---> 继承Thread类（重点）
- Runnable接口 ---> 实现Runnable接口（重点）
- Callable接口 ---> 实现Callable接口（现阶段了解）

### Thread

创建一个新的执行线程有两种方法，一个是将一个类声明为Thread的子类。这个子类应该重写run类的方法，编写线程执行体。创建线程对象，调用start方法启动线程

交替执行，同时执行

```java
package com.Sucker.Demo01;

//创建线程方法一：继承Thread类，重写run()方法，调用start开启线程

//注意：线程开启不一定立即执行，由cpu调度
public class TestThread1 extends Thread {
    @Override
    public void run() {
        //run方法线程体
        for (int i = 0; i < 20; i++) {
            System.out.println("k---"+i);
        }
    }

    public static void main(String[] args) {
        //main线程，主线程

        //创建一个线程对象
        TestThread1 testThread1 = new TestThread1();

        //调用start方法开启线程
        testThread1.start();

        for (int i = 0; i < 200; i++) {
            System.out.println("duo---"+i);
        }
    }
}
```

线程不一定立即执行，CPU安排调度

案例：下载图片

首先下载commons-io-2.6 jar 包，在com层级下新建package--lib，将其复制进lib目录中，再右键lib目录选择add as library

```java
package com.Sucker.Demo01;

import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;
import java.net.URL;

//联系Thread，实现多线程同步下载图片
public class TestThread2 extends Thread {

    private String url;  //网络图片地址
    private String name; //保存的文件名

    public TestThread2(String url, String name){
        this.url=url;
        this.name=name;
    }

    //下载图片的执行体
    @Override
    public void run() {
        WebDownloader webDownloader = new WebDownloader();
        webDownloader.downloader(url,name);
        System.out.println("下载了文件名为："+name);
    }

    public static void main(String[] args) {
        TestThread2 t1 = new TestThread2("https://img-home.csdnimg.cn/images/20210721094624.jpg","20210721094624.jpg");
        TestThread2 t2 = new TestThread2("https://img-home.csdnimg.cn/images/20210721094624.jpg","25.jpg");
        TestThread2 t3 = new TestThread2("https://img-home.csdnimg.cn/images/20210721094624.jpg","26.jpg");

        t1.start();
        t2.start();
        t3.start();
    }


}


//下载器
class WebDownloader{
    //下载方法
    public void downloader(String url,String name){
        try {
            //调用jar包里面写好的类的方法，把url地址变成一个文件
            FileUtils.copyURLToFile(new URL(url),new File(name));
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("IO异常，downloader方法出现问题");
        }
    }
}
```

步骤：

- 首先使用下载器，通过工具类里的方法
- 实现一个线程类，继承Thread类
- 用构造器丢入url和name
- 重写run方法，里面执行
- 主线程main方法里面通过构造器创建多个线程并启动

------------------------------------------------------------------------------

第二种方法是实现Runnable

- 定义MyRunnable类实现Runnable接口
- 重写run方法，实现run()方法，编写线程执行体
- 创建线程对象，调用start()方法启动线程

```java
package com.Sucker.Demo01;

//创建线程方式二：实现Runnable接口，执行线程需要丢入runnable接口实现类，调用start方法
public class TestThread3 implements Runnable {
    @Override
    public void run() {
        //run方法线程体
        for (int i = 0; i < 20; i++) {
            System.out.println("k---"+i);
        }
    }

    public static void main(String[] args) {

        //创建一个Runnable接口的实现类对象
        TestThread3 testThread3 = new TestThread3();

        //创建线程对象，通过线程对象来开启线程，代理
//        Thread thread = new Thread(testThread1);
//        thread.start();

        new Thread(testThread3).start();//简写

        for (int i = 0; i < 1000; i++) {
            System.out.println("duo---"+i);
        }
    }
}
```

小结：

- 继承Thread
  - 子类继承Thread类具备多线程能力
  - 启动线程：子类对象.start()
  - 不建议使用：避免OOP单继承局限性
- 实现Runnable
  - 实现接口Runnable具有多线程能力
  - 启动线程：传入目标对象+Thread对象.start()
  - 推荐使用：避免单继承局限性，灵活方便，方便同一个对象被多个线程使用

```java
Thread.currentThread().getName()这个方法得到当前执行线程的名字
```

例子：

```java
package com.Sucker.Demo01;

//多个线程同时操作同一个对象
//买火车票的例子

//发现问题：多个线程操作同一个资源情况下，线程不安全，数据紊乱
public class TestThread4 implements Runnable {

    //票数
    private int ticketNums = 10;


    @Override
    public void run() {
        while(true){
            if(ticketNums<=0) break;
            //模拟延时
            try {
                Thread.sleep(200);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            //Thread.currentThread().getName()这个方法得到当前执行线程的名字
            System.out.println(Thread.currentThread().getName()+"--->拿到了"+ticketNums--+"票");
        }
    }

    public static void main(String[] args) {
        TestThread4 ticket = new TestThread4();

        new Thread(ticket,"小明").start();//不同线程，可以起名字
        new Thread(ticket,"老师").start();
        new Thread(ticket,"黄牛党").start();

    }

}
```

发现问题：多个线程操作同一个资源情况下，线程不安全，数据紊乱

案例：龟兔赛跑

```java
package com.Sucker.Demo01;

//模拟龟兔赛跑
public class Race implements Runnable {
    
    //胜利者
    private static String winner; //静态常量static保证只有一个winner

    @Override
    public void run() {
        for (int i = 0; i <= 100; i++) {

            //模拟兔子睡觉
            if(Thread.currentThread().getName().equals("兔子") && i%10==0)
            {
                try {
                    Thread.sleep(1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }

            //判断比赛是否结束
            boolean flag = gammeOver(i);
            if(flag) break;

            System.out.println(Thread.currentThread().getName()+"-->跑了"+i+"步");
        }
    }

    //判断是否完成比赛
    private boolean gammeOver(int steps){
        //判断是否有胜利者
        if(winner!=null) return true;
        else if(steps>=100){
            winner = Thread.currentThread().getName();
            System.out.println("winner is "+winner);
            return true;
        }
        else return false;
    }

    public static void main(String[] args) {
        Race race = new Race();

        new Thread(race,"兔子").start();
        new Thread(race,"乌龟").start();
    }

}
```

### 实现Callable接口

1. 实现Callable接口，需要返回值类型
2. 重写call方法，需要抛出异常
3. 创建目标对象
4. 创建执行服务：ExecutorService ser = Executors.newFixedThreadPool(1)；
5. 提交执行：Future<Boolean> result1 = ser.submit(t1)
6. 获取结果：boolean r1 = result1.get()
7. 关闭服务：ser.shutdownNow()；

```java
package com.Sucker.Demo02;

import com.Sucker.Demo01.TestThread2;
import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;
import java.net.URL;
import java.util.concurrent.*;

//线程创建方式三：实现Callable接口
public class TestCallable implements Callable<Boolean> {
    private String url;  //网络图片地址
    private String name; //保存的文件名

    public TestCallable(String url, String name){
        this.url=url;
        this.name=name;
    }

    //下载图片的执行体
    @Override
    public Boolean call() {
       WebDownloader webDownloader = new WebDownloader();
        webDownloader.downloader(url,name);
        System.out.println("下载了文件名为："+name);
        return true;
    }

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        TestCallable t1 = new TestCallable("https://img-home.csdnimg.cn/images/20210721094624.jpg","20210721094624.jpg");
        TestCallable t2 = new TestCallable("https://cn.bing.com/images/search?view=detailV2&ccid=QnfHdp2q&id=BDCDE7C79D83FB599405AFD2188093140A3011E5&thid=OIP.QnfHdp2qT_0YJXjq1gmglgHaM1&mediaurl=https%3a%2f%2fuploadfile.bizhizu.cn%2fup%2f03%2fef%2f8f%2f03ef8fc438dbe2beb844b305ec87391e.jpg&exph=1774&expw=1024&q=jk%e7%be%8e%e5%a5%b3%e5%9b%be%e7%89%87&simid=608040684881330440&FORM=IRPRST&ck=851CB37FC70B002B589BA118850F85A4&selectedIndex=0","25.jpg");
        TestCallable t3 = new TestCallable("https://cn.bing.com/images/search?view=detailV2&ccid=ti3Zfhln&id=5D3EE2D7DE03E7400C8014499C2EE8B94A7F167D&thid=OIP.ti3ZfhlntGiUtwqXhdaLUAHaKL&mediaurl=https%3a%2f%2ftse1-mm.cn.bing.net%2fth%2fid%2fR-C.b62dd97e1967b46894b70a9785d68b50%3frik%3dfRZ%252fSrnoLpxJFA%26riu%3dhttp%253a%252f%252fimg.mm4000.com%252ffile%252f8%252f7b%252f260e19734b.jpg%26ehk%3dsZek3h%252fYAHyVd0KkDUGwyYRYOzMUYLFCkbZ4nbXssj4%253d%26risl%3d%26pid%3dImgRaw&exph=1513&expw=1100&q=jk%e7%be%8e%e5%a5%b3%e5%9b%be%e7%89%87&simid=608040800847024524&FORM=IRPRST&ck=3A1E7FE0E1914FF26937FF1227F44B89&selectedIndex=1","26.jpg");

        //创建线程服务：
        ExecutorService ser = Executors.newFixedThreadPool(3);//3个线程

        //提交执行
        Future<Boolean> r1 = ser.submit(t1);
        Future<Boolean> r2 = ser.submit(t2);
        Future<Boolean> r3 = ser.submit(t3);

        //获取结果
        boolean rs1 = r1.get();
        boolean rs2 = r2.get();
        boolean rs3 = r3.get();

        //关闭服务
        ser.shutdownNow();

    }

}

//下载器
class WebDownloader{
    //下载方法
    public void downloader(String url,String name){
        try {
            //调用jar包里面写好的类的方法，把url地址变成一个文件
            FileUtils.copyURLToFile(new URL(url),new File(name));
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("IO异常，downloader方法出现问题");
        }
    }
}
```

Callable的好处：

- 可以定义返回值
- 可以抛出异常

##### Callable和Future

它们俩其实挺有意思，在运行的时候各司其职，`Callable`**产生结果**，`Future`**获取结果**。

使用步骤如下：

1. 创建 Callable 接口的实现类，并实现 call() 方法，该 call() 方法将作为线程执行体，并且有返回值；
2. 创建 Callable 实现类的实例，使用 FutureTask 类来包装 Callable 对象，该 FutureTask 对象封装了该 Callable 对象的 call() 方法的返回值；
3. 使用 FutureTask 对象作为 Thread 对象的 target 创建并启动新线程；
4. 调用 FutureTask 对象的 get() 方法来获得子线程执行结束后的返回值。

接下来通过一个示例来学习这两个对象的使用：

```java
public class Test {
    public static void main(String[] args) {
        CallableThreadTest cts = new CallableThreadTest();
        // 接收
        FutureTask<Integer> ft = new FutureTask<>(cts);
        new Thread(ft, "有返回值的线程").start();
        for (int i = 0; i < 30; i++) {
            System.out.println( "main" + " 的循环变量i的值：" + i);
        }
        try {
            System.out.println("子线程的返回值：" + ft.get());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
class CallableThreadTest implements Callable<Integer> {
    public Integer call() throws Exception {
        int i = 0;
        for (; i < 30; i++) {
            System.out.println(Thread.currentThread().getName() + " " + i);
        }
        return i;
    }
}
```

运行这段程序你应该可以获取到类似如下结果（每次运行的结果不一致）： `...` `...` `main 的循环变量i的值：28` `main 的循环变量i的值：29` `有返回值的线程 23` `有返回值的线程 24` `有返回值的线程 25` `有返回值的线程 26` `有返回值的线程 27` `有返回值的线程 28` `有返回值的线程 29` `子线程的返回值：30`

由于输出过长，省略了部分结果，可以发现在最后接收到了子线程的返回值。

在实现`Callable`接口中，此时不再是`run()`方法了，而是`call()`方法，此`call()`方法作为线程执行体，同时还具有返回值！

细心的你会发现这个结果是`call`函数的返回值，怎么拿到这个返回值的呢？是通过`FutureTask`拿到的，使用`ft.get()`方法即可获得线程的返回值，这就是一个简单的使用`Callable和Future`的过程了。

## Lamda表达式

- 避免匿名内部类定义过多
- 其实质属于函数式编程的概念
- 可以让代码变得简洁

理解Functional Interface（函数式接口）是学习Java8 lambda表达式的关键所在

函数式接口的定义：

- 任何接口，如果只包含唯一一个抽象方法，那么它就是一个函数式接口

  ```java
  public interface Runnable{
      public abstract void run();
  }
  ```

- 对于函数式接口，我们可以通过lambda表达式来创建该接口的对象

不断简化，直到用lambda简化

```java
package com.Sucker.lambda;

/*
推导lambda表达式
 */
public class TestLambda1 {

    //3.静态内部类
    static class Like2 implements ILike{
        @Override
        public void lambda() {
            System.out.println("i like lambda2");
        }
    }

    public static void main(String[] args) {
        ILike like = new Like();
        like.lambda();

        like = new Like2();
        like.lambda();

        //4.局部内部类
        class Like3 implements ILike{
            @Override
            public void lambda() {
                System.out.println("i like lambda3");
            }
        }

        like = new Like3();
        like.lambda();

        //5.匿名内部类,没有类的名称，必须借助接口或父类
        like = new ILike() {
            @Override
            public void lambda() {
                System.out.println("i like lambda4");
            }
        };
        like.lambda();

        //6.用lambda简化
        like = ()->{
            System.out.println("i like lambda5");
        };
        like.lambda();

    }

}

//1.定义一个函数式接口
interface ILike{
    void lambda();//接口里面隐式声明，自动是抽象方法
}

//2.实现类
class Like implements ILike{

    @Override
    public void lambda() {
        System.out.println("i like lambda");
    }
}
```

```java
package com.Sucker.lambda;

public class TestLambda2 {

    public static void main(String[] args) {
        ILove love = null;
        /*//1.lambda表达式简化
        ILove love = (int a)->{
            System.out.println("i love you-->"+a);
        };

        //简化1.参数类型
        love = (a)->{
            System.out.println("i love you-->"+a);
        };

        //简化2.简化括号
        love = a->{
            System.out.println("i love you-->"+a);
        };*/

        //简化3.去掉花括号
        love = a -> System.out.println("i love you-->"+a);

        love.love(222);
    }


}

interface ILove{
    void love(int a);
}
```

总结：

- lambda表达式只能在只有一行代码的情况下能够简化成一行，如果有多行，需要使用代码块包裹
- 前提是接口为函数式接口
- 多个参数也可以去掉参数类型，但是必须加上括号

## 静态代理

```java
package com.Sucker.Demo03;

//静态代理模式总结：
//真实对象和代理对象都要实现同一个接口
//代理对象要代理真实角色
//好处：代理对象可以做很多真实对象做不了的事情
//真实对象专注做自己的事情

public class StaticProxy {

    public static void main(String[] args) {
        WeddingCompany weddingCompany = new WeddingCompany(new You());
        weddingCompany.HappyMarry();
    }

}

interface Marry{
    void HappyMarry();
}

//真实角色
class You implements Marry{
    @Override
    public void HappyMarry() {
        System.out.println("结婚了");
    }
}

//代理角色,帮助你结婚
class WeddingCompany implements Marry{
    //代理谁--》真实目标角色
    private Marry target;//结婚的真实对象

    public WeddingCompany(Marry target) {
        this.target = target;
    }

    @Override
    public void HappyMarry() {
        before();
        this.target.HappyMarry();//这就是真实对象
        after();
    }

    private void after() {
        System.out.println("结婚后收尾款");
    }

    private void before() {
        System.out.println("结婚前步置");
    }

}
```

静态代理模式总结：
真实对象和代理对象都要实现同一个接口
代理对象要代理真实角色
好处：代理对象可以做很多真实对象做不了的事情
真实对象专注做自己的事情

类比线程：

```java
new Thread(()-> System.out.println("111")).start();//lambda简化Runnbale接口和run方法
new WeddingCompany(new You()).HappyMarry();
```

## 线程状态

### 线程五大状态

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210723135315.png)

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210723135354.png)

### 线程方法

| 方法                           | 说明                                       |
| ------------------------------ | ------------------------------------------ |
| setPriority(int newPrioirty)   | 更改线程的优先级                           |
| static void sleep(long millis) | 在指定的毫秒数内让当前正在执行的线程休眠   |
| void join()                    | 等待该线程终止                             |
| static void yield()            | 暂停当前正在执行的线程对象，并执行其他线程 |
| void interrupt()               | 中断线程，别用这个方式                     |
| boolean isAlive()              | 测试线程是否处于活动状态                   |

### 停止线程

- 不推荐使用JDK提供的stop()、destroy()方法【已废弃】
- 推荐线程自己停止
- 建议使用一个标志位进行终止变量，当flag=false，则终止线程运行

```java
package com.Sucker.state;

//测试停止线程
//1.建议自己停止--》利用次数，不建议死循环
//2.建议使用标志位--》设置一个标志位
//3.不要使用stop或者destroy等过时或JKD不建议使用的方法
public class TestStop implements Runnable {

    //1.设置一个标志位
    private boolean flag = true;

    @Override
    public void run() {
        int i=0;
        while(flag){
            System.out.println("run Thread"+i++);
        }
    }

    //设置一个公开的方法停止线程，转换标志位
    public void stop(){
        this.flag=false;
    }

    public static void main(String[] args) {
        TestStop testStop = new TestStop();
        new Thread(testStop).start();

        for (int i = 0; i < 1000; i++) {
            System.out.println("main"+i);
            if(i==900) {
                testStop.stop();//调用stop切换标志位，停止线程
                System.out.println("线程该停止了");
            }
        }

    }


}
```

### 线程休眠

- sleep(时间)指定当前线程阻塞的毫秒数
- sleep存在异常InterruptedException
- sleep时间达到后线程进入就绪状态
- sleep可以模拟网络延时，倒计时等
- 每一个对象都有一个锁，sleep不会释放锁

模拟倒计时

```java
package com.Sucker.state;

import static com.Sucker.state.TestSleep2.tenDown;

//模拟倒计时
public class TestSleep2 {

    public static void main(String[] args) {
        try {
            tenDown();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static void tenDown() throws InterruptedException {
        int num=10;

        while(true){
            Thread.sleep(1000);
            System.out.println(num--);
            if(num<=0) break;
        }
    }

}
```

```java
Date startTime = new Date(System.currentTimeMillis());//获取系统当前时间
```

获取系统当前时间

```java
package com.Sucker.state;

import sun.security.mscapi.CPublicKey;

import java.security.PublicKey;
import java.text.SimpleDateFormat;
import java.util.Date;

import static com.Sucker.state.TestSleep2.tenDown;

//模拟倒计时
public class TestSleep2 {

    public static void main(String[] args) {
        //打印当前系统时间
        Date startTime = new Date(System.currentTimeMillis());//获取系统当前时间

        while(true){
            try {
                Thread.sleep(1000);
                System.out.println(new SimpleDateFormat("HH:mm:ss").format(startTime));
                startTime = new Date(System.currentTimeMillis());//更新当前时间
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void tenDown() throws InterruptedException {
        int num=10;

        while(true){
            Thread.sleep(1000);
            System.out.println(num--);
            if(num<=0) break;
        }
    }

}
```

### 线程礼让（yield）

- 礼让线程，让当前正在执行的线程暂停，但不阻塞
- 将线程从运行状态转为就绪状态
- 让CPU重新调度，礼让不一定成功！

```java
package com.Sucker.state;

//测试礼让线程，不一定成功
public class TsetYield {

    public static void main(String[] args) {

        MyYield myYield = new MyYield();
        new Thread(myYield,"a").start();
        new Thread(myYield,"b").start();
    }

}

class MyYield implements Runnable{

    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"线程开始执行");
        Thread.yield();//线程礼让
        System.out.println(Thread.currentThread().getName()+"线程停止执行");
    }
}
```

### 线程强制执行（Join）

- Join合并线程，待此线程执行完成后，再执行其他线程，其他线程阻塞
- 可以想象成插队

```java
package com.Sucker.state;

//测试Join方法，想象成插队
//刚开始交替执行，当主线程i==200后调用join插队，必须等待vip执行完后 才能执行主线程
public class TestJoin implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 1000; i++) {
            System.out.println("线程vip来了"+i);
        }
    }

    public static void main(String[] args) throws InterruptedException {
        //启动线程
        TestJoin testJoin = new TestJoin();
        Thread thread = new Thread(testJoin);
        thread.start();

        //主线程
        for (int i = 0; i < 1000; i++) {
            if(i==200) thread.join();//插队
            System.out.println("main"+i);
        }

    }

}
```

### 线程状态观测

线程可以处于以下状态之一：

- NEW

  尚未启动的线程处于此装填

- RUNNABLE

  在Java虚拟机中执行的线程处于此状态

- BLOCKED

  被阻塞等待监视器锁定的线程处于此状态

- WAITING

  正在等待另一个线程执行动作达到指定等待时间的线程处于此状态

- TIMED_WAITING

  正在等待另一个线程执行动作达到指定等待时间的线程处于此状态

- TERMINATED

  已退出的线程处于此状态

```java
package com.Sucker.state;

//观察测试线程的状态
public class TestState {

    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(()->{
            for (int i = 0; i < 5; i++) {
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("//////");
        });

        //观察状态
        Thread.State state = thread.getState();
        System.out.println(state); //NEW

        //观察启动后
        thread.start();
        state = thread.getState();
        System.out.println(state); //RUN

        while(state!=Thread.State.TERMINATED){//只要线程不终止，就一直输出状态
            Thread.sleep(100);
            state = thread.getState();//更新线程状态
            System.out.println(state);
        }

    }

}
```

线程一旦死亡就不能再启动

## 线程优先级（priority）

- Java提供一个线程调度器来监控程序中启动后进入就绪状态的所有线程，线程调度器按照优先级决定应该调度哪个线程来执行
- 线程的优先级用数字来表示，范围从1~10
  - Thread.MIN_PRIORITY = 1
  - Thread.MAX_PRIORITY = 10
  - Thread.NORM_PROIRITY = 5
- 使用以下方式改变或获取优先级
  - getPriority().setPriority(int xxx)

优先级低只是意味着获得调度的概率低，并不是优先级低就不会被调用了，这都是看CPU的调度

优先级的设定建议在start调度之前

```java
package com.Sucker.state;

//测试线程优先级
public class TestPriority {

    public static void main(String[] args) {
        //主线程默认优先级
        System.out.println(Thread.currentThread().getName()+"-->"+Thread.currentThread().getPriority());

        MyPriority myPriority = new MyPriority();

        Thread t1 = new Thread(myPriority);
        Thread t2 = new Thread(myPriority);
        Thread t3 = new Thread(myPriority);
        Thread t4 = new Thread(myPriority);
        Thread t5 = new Thread(myPriority);
        Thread t6 = new Thread(myPriority);

        //先设置优先级，再启动
        t1.start();

        t2.setPriority(1);
        t2.start();

        t3.setPriority(4);
        t3.start();

        t4.setPriority(Thread.MAX_PRIORITY);
        t4.start();

    }

}

class MyPriority implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"-->"+Thread.currentThread().getPriority());
    }
}
```

结果不一定是按优先级排列 

## 守护（daemon）线程

- 线程分为用户线程和守护线程
- 虚拟机必须确保用户线程执行完毕
- 虚拟机不用等待守护线程执行完毕
- 如，后台记录操作日志，监控内存，垃圾回收等

```java
package com.Sucker.state;

//测试守护案例
//上帝守护你
public class TestDaemon {

    public static void main(String[] args) {
        God god = new God();
        You you = new You();

        Thread thread = new Thread(god);
        thread.setDaemon(true); //默认false 表示是用户线程，正常的线程都是用户线程

        thread.start(); //上帝守护线程启动

        new Thread(you).start();//你 用户线程启动

    }

}

//上帝
class God implements Runnable{
    @Override
    public void run() {
        while (true){
            System.out.println("上帝保佑你");
        }
    }
}

//你
class You implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 36500; i++) {
            System.out.println("你一生都开心的活着");
        }
        System.out.println("===goodbye world=====");
    }
}
```

## 线程同步

多个线程操作同一个资源

### 并发

同一个对象被多个线程同时操作

### 线程同步

处理多线程问题时，多个线程访问同一个对象，并且某些线程还想修改这个对象，这时候我们就需要线程同步，线程同步其实就是一种等待机制，多个需要同时访问此对象的线程进入**这个对象的等待池**形成队列，等待前面线程使用完毕，下一个线程再使用

形成条件：队列+锁（每个对象都有一个锁）  安全性

- 由于同一进程的多个线程共享同一块存储空间，在带来方便的同时，也带来了访问冲突问题，为了保证数据在方法中被访问时的正确性，在访问时加入**锁机制synchronized**，当一个线程获得对象的排它锁，独占资源，其他线程必须等待，使用后释放锁即可，存在以下问题：
  - 一个线程持有锁会导致其他所有需要此锁的线程挂起
  - 在多线程竞争下，加锁，释放锁会导致比较多的上下文切换和调度延时，引起性能问题
  - 如果一个优先级高的线程等待一个优先级低的线程释放锁会导致优先级倒置，引起性能问题

### 三大不安全案例

```java
package com.Sucker.syn;

//不安全的买票
//线程不安全，有负数
public class UnsafeBuyTicket {

    public static void main(String[] args) {
        BuyTicket station = new BuyTicket();

        new Thread(station,"苦逼的我").start();
        new Thread(station,"牛逼的你").start();
        new Thread(station,"可恶的黄牛").start();
    }

}

class BuyTicket implements Runnable{

    //票
    private int ticketNums = 10;
    boolean flag = true;
    @Override
    public void run() {
        //买票
        while(flag) {
            try {
                buy();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    private void buy() throws InterruptedException {
        //判断是否有票
        if(ticketNums<=0){
            flag = false;
            return;
        }

        //模拟延时
        Thread.sleep(100);

        //买票
        System.out.println(Thread.currentThread().getName()+"拿到了"+ticketNums--);
    }

}
```

```java
package com.Sucker.syn;

//不安全的取钱
//两个人去银行取钱
public class UnsafeBank {

    public static void main(String[] args) {
        //账户
        Account account = new Account(100,"结婚基金");
        Drawing you = new Drawing(account,50,"你");
        Drawing girlFriend = new Drawing(account,100,"girlFriend");

        you.start();
        girlFriend.start();

    }

}

class Account{
    int money;//余额
    String name;//卡名

    public Account(int money,String name) {
        this.money = money;
        this.name = name;
    }
}

//银行:模拟取款
class Drawing extends Thread{

    Account account;//账户
    //取了多少钱
    int drawingMoney;
    //现在手里有多少钱
    int nowMoney;

    public Drawing(Account account,int drawingMoney,String name){
        super(name);//调用父类有参构造
        this.account = account;
        this.drawingMoney = drawingMoney;
    }

    //取钱
    @Override
    public void run() {
        //判断有没有钱
        if(account.money - drawingMoney<0) {
            System.out.println("钱不够，取不了");
            return;
        }
        //sleep放大问题，看出线程不安全
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        //卡内余额 = 余额 - 你取的钱
        account.money = account.money - drawingMoney;

        //手里的钱
        nowMoney+=drawingMoney;

        System.out.println(account.name+"余额为"+account.money);
        //此时的Thread.currentThread().getName() = this.getName()
        //因为这个类继承了Thread类，可以调用其中getName方法
        System.out.println(this.getName()+"手里的钱"+nowMoney);


    }
}
```

```java
package com.Sucker.syn;

import java.util.ArrayList;
import java.util.List;

//线程不安全的集合
public class UnsafeList {

    public static void main(String[] args) {

        List<String> list = new ArrayList<String>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                list.add(Thread.currentThread().getName());//两个线程可能同时添加到同一个位置，就会覆盖
            }).start();
        }
        try {//加入sleep才能满足达到10000条线程进去
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(list.size());
    }

}
```

### 同步方法及同步块

- 由于我们可以通过private关键字来保证数据对象只能被方法访问，所以我们只需要针对方法提出一套机制，这套机制就是synchronized关键字，它包括两种用法：

  synchronized 方法 和synchronized 块

  同步方法：public synchronized void method(int args){}

- synchronized方法控制对”对象"的访问，每个对象对应一把锁，每个synchronized方法都必须获得调用该方法的对象的锁才能执行，否则线程会阻塞，方法一旦执行，就独占该锁，直到该方法返回才释放锁，后面被阻塞的线程才能获得这个锁，继续执行

  缺陷：若将一个大的方法申明为synchronized 将会影响效率

同步方法弊端：方法里面若有A和B代码，A为只读，B为修改，因此方法里面需要修改的内容才需要锁，锁的太多，浪费资源

**同步块：**

- 同步块：synchronized(Obj){}
- Obj称之为同步监视器
  - Obj可以是任何对象，但是推荐使用共享资源作为同步监视器
  - 同步方法中无需指定同步监视器，因为同步方法的同步监视器就是this，就是这个对象本身，或者是class[反射中讲解]
- 同步监视器的执行过程
  - 第一个线程访问，锁定同步监视器，执行其中代码
  - 第二个线程访问，发现同步监视器锁定，无法访问
  - 第一个线程访问完毕，解锁同步监视器
  - 第二个线程访问，发现同步监视器未锁，锁定它并访问

**同步块锁定的对象是需要增删改查的对象**

同步方法例子：

```java
package com.Sucker.syn;

//不安全的买票
//线程不安全，有负数
public class UnsafeBuyTicket {

    public static void main(String[] args) {
        BuyTicket station = new BuyTicket();

        new Thread(station,"苦逼的我").start();
        new Thread(station,"牛逼的你").start();
        new Thread(station,"可恶的黄牛").start();
    }

}

class BuyTicket implements Runnable{

    //票
    private int ticketNums = 10;
    boolean flag = true;
    @Override
    public void run() {
        //买票
        while(flag) {
            try {
                buy();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    //synchronized 同步方法，锁的是this
    private synchronized void buy() throws InterruptedException {
        //判断是否有票
        if(ticketNums<=0){
            flag = false;
            return;
        }

        //模拟延时
        Thread.sleep(100);

        //买票
        System.out.println(Thread.currentThread().getName()+"拿到了"+ticketNums--);
    }

}
```

同步块例子：

```java
package com.Sucker.syn;

//不安全的取钱
//两个人去银行取钱
public class UnsafeBank {

    public static void main(String[] args) {
        //账户
        Account account = new Account(100,"结婚基金");
        Drawing you = new Drawing(account,50,"你");
        Drawing girlFriend = new Drawing(account,100,"girlFriend");

        you.start();
        girlFriend.start();

    }

}

class Account{
    int money;//余额
    String name;//卡名

    public Account(int money,String name) {
        this.money = money;
        this.name = name;
    }
}

//银行:模拟取款
class Drawing extends Thread{

    Account account;//账户
    //取了多少钱
    int drawingMoney;
    //现在手里有多少钱
    int nowMoney;

    public Drawing(Account account,int drawingMoney,String name){
        super(name);//调用父类有参构造
        this.account = account;
        this.drawingMoney = drawingMoney;
    }

    //取钱
    @Override
    public void run() {

        //锁的对象就是变化的量，需要增删改的对象
        synchronized (account){

            //判断有没有钱
            if(account.money - drawingMoney<0) {
                System.out.println("钱不够，取不了");
                return;
            }
            //sleep放大问题，看出线程不安全
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            //卡内余额 = 余额 - 你取的钱
            account.money = account.money - drawingMoney;

            //手里的钱
            nowMoney+=drawingMoney;

            System.out.println(account.name+"余额为"+account.money);
            //此时的Thread.currentThread().getName() = this.getName()
            //因为这个类继承了Thread类，可以调用其中getName方法
            System.out.println(this.getName()+"手里的钱"+nowMoney);

        }

    }
}
```

扩充：JUC的安全类型集合

```java
package com.Sucker.syn;

import com.sun.org.apache.xpath.internal.objects.XString;

import java.util.concurrent.CopyOnWriteArrayList;

//测试JUC安全类型的集合
public class TestJUC {

    public static void main(String[] args) {
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<String>();
        for (int i = 0; i < 10000; i++) {
            list.add(Thread.currentThread().getName());
        }
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(list.size());

    }

}
```

## 死锁

- 多个线程各自占有一些共享资源，并且互相等待其他线程占有的资源才能运行，而导致两个或者多个线程都在等待对方释放资源，都停止执行的情形。某一个同步块同时拥有**两个以上对象的锁**时，就可能发生死锁问题

例子：

```java
package com.Sucker.thread;

//死锁：多个线程互相抱着对方需要的资源，然后形成僵持
public class DeadLock {

    public static void main(String[] args) {

        Makeup g1 = new Makeup(0,"灰姑娘");
        Makeup g2 = new Makeup(1,"白雪公主");
        g1.start();
        g2.start();

    }

}

//口红
class Lipstick{

}

//镜子
class Mirror{

}

class Makeup extends Thread{

    //需要的资源只有一份，用static来保证只有一份
    static Lipstick lipstick = new Lipstick();
    static Mirror mirror = new Mirror();

    int choice;//选择
    String girlName;//使用化妆品的人

    Makeup(int choice,String girlName){
        this.choice = choice;
        this.girlName = girlName;
    }

    @Override
    public void run() {
        //化妆
        try {
            makeup();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    //化妆，互相持有对方的锁，就是需要拿到对方的资源
    private void makeup() throws InterruptedException {
        if(choice==0){
            synchronized (lipstick){//获得口红资源
                System.out.println(this.girlName+"获得口红的锁");
                Thread.sleep(1000);
                synchronized (mirror){//一秒钟后想获得镜子
                    System.out.println(this.girlName+"获得镜子的锁");
                }
            }
        }else{
            synchronized (mirror){//获得镜子资源
                System.out.println(this.girlName+"获得镜子的锁");
                Thread.sleep(2000);
                synchronized (lipstick){//一秒钟后想获得口红
                    System.out.println(this.girlName+"获得口红的锁");
                }
            }
        }
    }

}
```

此时互相持有对方所需要的资源，造成死锁，此时程序只输出灰姑娘获得口红锁与白雪公主获得镜子锁然后卡死

解决方法，将锁放出来让其释放

```java
//化妆，互相持有对方的锁，就是需要拿到对方的资源
    private void makeup() throws InterruptedException {
        if(choice==0){
            synchronized (lipstick){//获得口红资源
                System.out.println(this.girlName+"获得口红的锁");
                Thread.sleep(1000);
            }
            synchronized (mirror){//一秒钟后想获得镜子
                System.out.println(this.girlName+"获得镜子的锁");
            }
        }else{
            synchronized (mirror){//获得镜子资源
                System.out.println(this.girlName+"获得镜子的锁");
                Thread.sleep(2000);
            }
            synchronized (lipstick){//一秒钟后想获得口红
                System.out.println(this.girlName+"获得口红的锁");
            }
        }
    }
```

死锁的避免方法：

- 产生死锁的四个必要条件
  1. 互斥条件：一个资源每次只能被一个进程使用
  2. 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放
  3. 不剥夺条件：进程已获得的资源，在未使用完之前，不能强行剥夺
  4. 循环等待条件：若干进程之间形成一种头尾相接的循环等待资源关系
- 上面列出死锁的四个必要条件，只要破坏其中的任意一个或多个条件就可以避免死锁发生

## Lock(锁)

- 从JDK5.0开始，Java提供了更强大的线程同步机制——通过显式定义同步锁对象来实现同步。同步锁使用Lock对象充当
- java.util.concurrent.locks.Lock接口是控制多个线程对共享资源进行访问的工具。锁提供了对共享资源的独占访问，每次只能有一个线程对Lock对象加锁，线程开始访问共享资源之前应先获得Lock对象
- ReentrantLock （可重入锁）类实现了Lock，它拥有与synchronized相同的并发性和内存语义，在实现线程安全的控制中，比较常用的是ReentrantLock，可以显式加锁、释放锁

```java
package com.Sucker.gaoji;

import com.Sucker.Demo01.TestThread2;

import java.util.concurrent.locks.ReentrantLock;

//测试Lock锁
public class TestLock {

    public static void main(String[] args) {
        TestLock2 testLock2 = new TestLock2();

        new Thread(testLock2).start();
        new Thread(testLock2).start();
        new Thread(testLock2).start();
    }

}

class TestLock2 implements Runnable{

    int ticknetNums = 10;
    //定义lock锁
    private final ReentrantLock lock = new ReentrantLock();

    @Override
    public void run() {
        while (true){
            try {
                lock.lock();//加锁
                if(ticknetNums>0){
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(ticknetNums--);
                }else break;
            }finally {
                //解锁
                lock.unlock();
            }
        }
    }
}
```

注意加锁和解锁

synchronized 与 Lock 的对比

- Lock是显式锁(手动开启和关闭锁，别忘记关闭锁) synchronized是隐式锁，出了作用域自动释放
- Lock只有代码块锁，synchronized有代码块锁和方法锁
- 使用Lock锁，JVM将花费较少的时间来调度线程，性能更好。并且具有更好的扩展性(提供更多的子类)
- 优先使用顺序：
  - Lock > 同步代码块(已经进入了方法体，分配了相应资源) > 同步方法(在方法体之外)

## 线程协作

### 线程通信

- 应用场景：生产者和消费者问题
  - 假设仓库中只能存放一件产品，生产者将生产出来的产品放入仓库，消费者将仓库中产品取走消费
  - 如果仓库中没有产品，则生产者将产品放入仓库，否则停止生产并等待，直到仓库中的产品被消费者取走为止
  - 如果仓库中放有产品，则消费者可以将产品取走消费，否则停止消费并等待，直到仓库中再次放入产品为止

**这是一个线程同步问题，生产者和消费者共享同一个资源，并且生产者和消费者之间相互依赖，互为条件**

- 对于生产者，没有生产产品之前，要通知消费者等待，而生产了产品后，又需要马上通知消费者消费
- 对于消费者，在消费之后，要通知生产者已经结束消费，需要生产新的产品以供消费
- 在生产者消费者问题中，仅有synchronized是不够的
  - synchronized 可阻止并发更新同一个共享资源，实现了同步
  - synchronized 不能用来实现不同线程之间的消息传递(通信)

Java提供了几个方法解决线程之间的通信问题

| 方法名             | 作用                                                         |
| ------------------ | ------------------------------------------------------------ |
| wait()             | 表示线程一直等待，直到其他线程通知，与sleep不同，会释放锁，只能在同步块 |
| wait(long timeout) | 指定等待的毫秒数                                             |
| notify()           | 唤醒一个处于等待状态的线程                                   |
| notifyAll()        | 唤醒同一个对象上所有调用wait()方法的线程，优先级别高的线程优先调度 |

**注意：均是Object类的方法，都只能在同步方法或者同步代码块中使用，否则会抛出异常IIIegalMonitorStateException**

**解决方式一：**

  并发协作模型“生产者/消费者模式” ---> 管程法

- 生产者：负责生产数据的模块(可能是方法，对象，线程，进程)；

- 消费者：负责处理数据的模块(可能是方法，对象，线程，进程)；

- 缓冲区：消费者不能直接使用生产者的数据，他们之间有个缓冲区

  **生产者将生产好的数据放入缓冲区，消费者从缓冲区拿出数据**

  Producer  --》数据缓冲区  --》 Consumer

**解决方式二：**

  并发协作模型”生产者/消费者模式“ --> 信号灯法

### 管程法

```java
package com.Sucker.gaoji;

//测试：生产者消费者模型 --> 利用缓冲区解决

//生产者 消费者 产品 缓冲区
public class TestPC {

    public static void main(String[] args) {
        SynContainer container = new SynContainer();

        new Productor(container).start();
        new Consumer(container).start();
    }
}

//生产者
class Productor extends Thread{
    SynContainer container;
    public Productor(SynContainer container){
        this.container = container;
    }

    //生产
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("生产了"+i+"只鸡");
            container.push(new Chicken(i));
        }
    }
}

//消费者
class Consumer extends Thread{
    SynContainer container;
    public Consumer(SynContainer container){
        this.container = container;
    }

    //消费
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("消费了"+container.pop().id+"只鸡");
        }
    }

}

//产品
class Chicken{
    int id;//产品编号
    public Chicken(int id) {
        this.id = id;
    }
}

//缓冲区
class SynContainer{

    //需要一个容器大小
    Chicken[] chickens = new Chicken[10];
    //容器计数器
    int count = 0;

    //生产者放入产品
    public synchronized void push(Chicken chicken){
        //如果容器满了，需要等待消费者消费
        if(count == chickens.length){
            //通知消费者消费，生产等待
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        //如果没有满，需要丢入产品
        chickens[count] = chicken;
        count++;

        //有产品了，可以通知消费者消费了
        this.notifyAll();
    }

    //消费者消费产品
    public synchronized Chicken pop(){
        //判断能否消费
        if(count==0){
            //等待生产者生产，消费者等待
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        //如果可以消费
        count--;
        Chicken chicken = chickens[count];

        //吃完了，通知生产者生产
        this.notifyAll();
        return chicken;

    }

}
```

### 信号灯法

```java
package com.Sucker.gaoji;

//测试生产者消费者问题2：信号灯法，标志位解决
public class TestPC2 {

    public static void main(String[] args) {
        TV tv = new TV();
        new Player(tv).start();
        new Watcher(tv).start();

    }

}

//生产者 --> 演员
class Player extends Thread{
    TV tv;
    public Player(TV tv){
        this.tv = tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            if(i%2==0) this.tv.play("快乐大本营");
            else this.tv.play("抖音");
        }
    }
    
}

//消费者 --> 观众
class Watcher extends Thread{
    TV tv;
    public Watcher(TV tv){
        this.tv = tv;
    }
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            tv.watch();
        }
    }

}

//产品 --> 节目
class TV{
    //演员表演，观众等待  T
    //观众观看，演员等待  F
    String voice;
    boolean flag = true;

    //表演
    public synchronized void play(String voice){
        if(!flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("演员表演了"+voice);
        //通知观众观看
        this.notifyAll();//通知唤醒
        this.voice = voice;
        this.flag = !this.flag;

    }

    //观看
    public synchronized void watch(){
        if(flag){//观众等待观看
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("观看了"+voice);
        //通知演员表演
        this.notifyAll();
        this.flag = !this.flag;
    }

}
```

## 线程池

- 背景：经常创建和销毁、使用量特别大的资源，比如并发情况下的线程，对性能的影响很大
- 思路：提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中。可以避免频繁创建销毁、实现重复利用。类似生活中的公共交通工具
- 好处：
  - 提高相应速度(减少了创建新线程的时间)
  - 降低资源消耗(重复利用线程池中线程，不需要每次都创建)
  - 便于线程管理(...)
    - corePoolSize：核心池的大小
    - maximumPoolSize：最大线程数
    - keepAliveTime：线程没有任务时最多保持多长时间后会终止
- JDK5.0起提供了线程池相关API：**ExecutorService 和 Executors**
- ExecutorService：真正的线程池接口。常见子类ThreadPoolExecutor
  - void execute(Runnable command) : 执行任务/命令，没有返回值，一般用来执行Runnable
  - <T>Future<T>submit(Callable<T>task)：执行任务，有返回值，一般用来执行Callable
  - void shutdown()：关闭线程池
- Executors：工具类、线程池的工厂类，用于创建并返回不同类型的线程池

```java
package com.Sucker.gaoji;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

//测试线程池
public class TestPool {

    public static void main(String[] args) {
        //1.创建服务，创建线程池
        //newFixedThreadPool 参数为：线程池的大小
        ExecutorService service = Executors.newFixedThreadPool(10);

        //执行
        service.execute(new MyThread());
        service.execute(new MyThread());
        service.execute(new MyThread());
        service.execute(new MyThread());

        //2.关闭连接
        service.shutdownNow();

    }

}

class MyThread implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName());
    }
}
```

