## IO流

### 流的概念

1. 内存与存储设备之间传输数据的通道
2. 数据借助流传输

### 流的分类

1. 按方向分：
   - 输入流：将存储设备中的内容读入到内存中
   - 输出流：将内存中的内容写入到存储设备中
2. 按单位：
   - 字节流：以字节为单位，可以读写所有数据
   - 字符流：以字符为单位，只能读写文本数据
3. 按功能：
   - 节点流：具有实际传输数据的读写功能
   - 过滤流：在节点流的基础上增强功能

## 字节流抽象类

### 字节流的父类（抽象类）

1. InputStream：字节输入流
   - 此抽象类是表示字节输入流的所有类的超类
   - public int read () {}
   - public int read (byte[] b)
   - public int read (byte[] b ,int off ,int len)
2. OutputStream：字节输出流
   - 此抽象类是表示输出字节流的所有类的超类
   - public void write (int n)
   - public void write (byte [] b)
   - public void write (byte [] b ,int off ,int len)

### 文件字节流（字节流的子类）

1. FileInputStream：

   - public int read (byte[] b) :从流中读取多个字节，将读到的内容存入b数组，返回实际读到的字节数；如果达到文件的尾部，则返回-1

   - ```java
     /**
      * 演示FileInputStream的使用
      * 文件字节输入流
      */
     public class Demo01 {
         public static void main(String[] args) throws Exception{
             //1.创建FileInputStream,并指定文件路径
             FileInputStream fis = new FileInputStream("d:\\aaa.txt");
             //2.读取文件
             //2.1单个字节读取
             /*int data = 0;
             while((data=fis.read())!=-1){
                 System.out.print((char) data);
             }*/
     
             //2.2一次读取多个字节
             /*byte[] buf=new byte[3];
             int count = fis.read(buf);
             System.out.println(count);
             System.out.println(new String(buf));*/
             byte[] buf=new byte[1024];
             int count=0;
             while((count=fis.read(buf))!=-1){
                 System.out.println(new String(buf,0,count));
             }
             //3.关闭
             System.out.println();
             fis.close();
             System.out.println("执行完毕");
         }
     }
     ```

     

2. FileOutputStream：

   - public void write (byte[] b)：一次写入多个字节，将b数组中的所有字节，写入输出流

   - string.getBytes()方法可以获取这个字符串对应的字节数组

   - FileOutputStream fos=new FileOutputStream("d:\\bbb.txt"，true);后面的true表示不覆盖接着往后面写

   - ```java
     public class Demo02 {
         public static void main(String[] args) throws Exception{
             //1.创建文件字节输出流对象
             FileOutputStream fos=new FileOutputStream("d:\\bbb.txt",true);
             //2.写入文件
             /*fos.write(97);
             fos.write('b');
             fos.write('c');*/
             String string = "helloworld";
             fos.write(string.getBytes());
             //3.关闭
             fos.close();
             System.out.println("执行完毕");
         }
     }
     ```

     

### 字节流文件复制

```java
public class Demo03 {
    public static void main(String[] args) throws Exception{
        //1.1创建文件字节输入流
        FileInputStream fis=new FileInputStream("d:\\000.png");
        //1.2文件字节输出流
        FileOutputStream fos=new FileOutputStream("d:\\001.png");
        //2.实现复制，一边读，一边写
        byte[] buf=new byte[1024];
        int count=0;
        while((count=fis.read(buf))!=-1){
            fos.write(buf,0,count);
        }
        //3.关闭
        fis.close();
        fos.close();
        System.out.println("执行完毕");
    }
}

```

### BufferedInputStream/BufferedOutputStream的使用

1. 继承关系：java.lang.Object -> java.io.InputStream -> java.io.FilterInputStream -> java.io.BufferedInputStream

2. 字节缓冲流：

   - 缓冲流：BufferedInputStream/BufferedOutputStream
     - 提高IO效率，减少访问磁盘量
     - 数据存储在缓冲区内，flush是将缓冲区的内容写入文件中，也可以直接close
     - 内部有默认8K的缓冲区

3. ```java
   public class Demo04 {
       public static void main(String[] args) throws Exception{
           //1.创建BufferedInputStream
           FileInputStream fis=new FileInputStream("d:\\aaa.txt");
           BufferedInputStream bis=new BufferedInputStream(fis);
           //2.读取
           int data=0;
           while((data=bis.read())!=-1){
               System.out.print((char) data);
           }
           //3.关闭
           bis.close();//内部会将fis关掉
   
       }
   }
   //此为使用字节缓冲流读取文件
   ```

4. 使用字节流写入文件（BufferedOutputStream）

   - 该类实现缓冲的输出流。通过设置这种输出流，应用程序就可以将各个字节写入底层输出流中，而不必针对每次字节写入调用底层系统

   - close的内部会调用flush

   - ```java
     public class Demo05 {
         public static void main(String[] args) throws Exception{
             //1.创建字节输出缓冲流
             FileOutputStream fos=new FileOutputStream("d:\\buffer.txt");
             BufferedOutputStream bos=new BufferedOutputStream(fos);
             //2.写入文件
             for (int i = 0; i < 10; i++) {
                 bos.write("helloworld\r\n".getBytes());//此时先写入的是8K的缓冲区
                 bos.flush();//刷新到硬盘
             }
             //3.关闭(内部也会调用flush)
             bos.close();
         }
     }
     ```

## 对象流

### 概念

1. 对象流：ObjectOutputStream/ObjectInputStream
   - 继承OutputStream与InputStream
   - 增强了缓冲区功能
   - 增强了读写八种基本数据类型和字符串功能
   - 增强了读写对象的功能
     - readObject()：从流中读取一个对象
     - writeObject(Obbject obj)：向流中写入一个对象
   - 使用流传输对象的过程称为序列化（将对象通过流写入到文件）与反序列化（将对象从流中读取）

### 序列化

**相关知识**

之前我们学习了 InputStream（字节输入流）和 OutputStream (字节输出流)，下面我们来了解一下它们的子类---ObjectInputStream (对象输入流)和 ObjectOutputStream（对象输出流）。

**为什么要有对象流**

有的时候，我们可能需要将内存中的对象持久化到硬盘上（序列化），或者将硬盘中的对象信息读到内存中（反序列化），这个时候我们需要使用对象流。

**序列化和反序列化**

序列化： 是对象转换成一个字节序列的过程，是一个写操作。 反序列化：一个字节序列转换成对象的过程 ，是一个读操作。 序列化和反序列化中对象所对应的类，必须是实现 Serializable 接口。

**ObjectOutputStream****（对象输出流）**

ObjectOutputStream 是 OutputStream 的子类，也叫做序列化流。该流把对象转成字节数据输出到文件中保存，可实现对象的持久存储。

**ObjectOutputStream** **的构造方法**

| **构造方法**                         | **说明**                                   |
| ------------------------------------ | ------------------------------------------ |
| ObjectOutputStream(OutputStream out) | 使用底层输出流创建 ObjectOutputStream 对象 |

构造方法示例：

1. ` public static void main(String[] args) throws IOException {`
2. `        // 通过文件字节输出流创建对象输出流`
3. `        ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream("C:\\Users\\yy\\Desktop\\d.txt"));`
4. `    }`

**ObjectOutputStream** **的常用方法**

下表是它的常用方法：

| **方法**                                               | **说明**                                               |
| ------------------------------------------------------ | ------------------------------------------------------ |
| write(byte[] w，int off，int  len)                     | 把字节数组中偏移量从 off 开始的 len 个字节写入此输出流 |
| write(byte [] b)                                       | 将字节数组写入此输出流                                 |
| writeBooolean()、writeByte()、writeShort()、writeInt() | 将指定的基本数据类型以字节的方式写入到输出流           |
| flush()                                                | 刷新此输出流并强制写出所有缓冲的输出字节               |
| writeUTF(String s)                                     | 将字符串格式化顺序写入底层的输出流                     |
| writeObject(Object obj)                                | 特有的方法，将指定的对象写入 ObjectOutputStream 流     |

通过 writeObject 方法将 Hero 对象写入文件示例：

Hero 类：

1. `import java.io.Serializable;`
2. ` public class Hero implements Serializable {     // 实现Serializable接口`
3. ``
4. `    private static final long serialVersionUID = 1L;     //表示这个类当前的版本`
5. `    public String name;`
6. `    public float hp;`
7. ``
8. `}`

Test类：

```java
public class Test {
public static void main(String[] args) throws IOException {
        //创建一个Hero对象
        Hero h = new Hero();
        // 设置属性
        h.name = "garen";
        h.hp = 616;
        // 准备一个文件用于保存该对象
        File f =new File("C:\\Users\\yy\\Desktop\\d.txt");
        try(
        // 将Hero对象写入文件
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream(f));){
            objectOutputStream.writeObject(h);
        }
    }
    }
```

执行结果：将对象写入了 d.txt 文件。

注意：Hero 类必须实现 Serializable 接口。

**ObjectInputStream****（对象输入流）**

ObjectInputStream 是 InputStream 的子类，也叫做反序列流。该流将之前使用 ObjectOutputStream 序列化的原始数据恢复为对象，以流的方式读取对象。 ######ObjectInputStream 的构造方法

下表中是它的构造方法：

| **构造方法**                      | **说明**                                  |
| --------------------------------- | ----------------------------------------- |
| ObjectInputStream(InputStream in) | 使用底层输入流创建 ObjectInputStream 对象 |

构造方法使用示例：

```java
public static void main(String[] args) throws IOException {
        // 通过文件字节输入流创建对象输入流对象
        ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream("C:\\Users\\yy\\Desktop\\d.txt"));
    }
```

**ObjectInputStream** **的常用方法**

下表是它的常用方法：

| **方法**                                           | **说明**                                                     |
| -------------------------------------------------- | ------------------------------------------------------------ |
| read(byte[] r, int off, int len)                   | 从流中读入字节数据到缓冲区数组中指定位置，off 为数组偏移量，len 为写入长度。 |
| read(byte [] b)                                    | 从流中读入字节数据到缓冲区数组中                             |
| readBooolean()、readByte()、readShort()、readInt() | 从输入流中读取基本数据类型                                   |
| readUTF()                                          | 按照格式化顺序读底层的输入流                                 |
| readObject()                                       | 特有的方法，把对象读入 ObjectInputStream 流                  |

readObject 方法使用示例：

```java
public static void main(String[] args) throws   IOException, ClassNotFoundException {
        try (
                // 通过文件字节输入流创建对象输入流对象
                ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream("C:\\Users\\yy\\Desktop\\d.txt"));) {
                // 获取对象
            System.out.print(objectInputStream.readObject());
        }
    }
```

执行结果：

1. `com.company.Hero@58372a00`

   以上为Educoder，以下为狂神

1. public class Student implements Serializable //实现这个接口表示可以序列化

2. ```java
   /**
    * 学生类
    */
   public class Student implements Serializable {//实现这个接口表示可以序列化
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

   ```java
   /**
    * 使用ObjectOutputStream实现对象的序列化
    */
   public class Demo06 {
       public static void main(String[] args) throws Exception{
           //1.创建对象流
           FileOutputStream fos=new FileOutputStream("d:\\stu.bin");//二进制文件
           ObjectOutputStream oos=new ObjectOutputStream(fos);
           //2.序列化(写入操作)
           Student zhangsan=new Student("张三",20);
           oos.writeObject(zhangsan);
           //3.关闭（close自带flush）
           oos.close();
           System.out.println("执行完毕");
       }
   }
   ```

### 反序列化

1. 读取重构成对象

2. ```java
   /**
    * 使用ObjectInputStream实现反序列化(读取重构成对象)
    */
   public class Demo07 {
       public static void main(String[] args) throws Exception{
           //1.创建一个对象流
           FileInputStream fis=new FileInputStream("d:\\stu.bin");
           ObjectInputStream ois=new ObjectInputStream(fis);
           //2.读取文件(反序列化
           Student s=(Student) ois.readObject();
           //3.关闭
           ois.close();
           System.out.println(s.toString());
       }
   }
   ```

   

### 序列化与反序列化的注意事项

1. 序列化类必须要实现Serializable接口

2. 序列化类中对象属性要求实现Serializable接口

3. 通过序列化ID，保证序列化和反序列化的类是同一个类  private static final long serialVersionUID = xxxL；

4. 使用transient修饰属性，这个属性不能序列化

5. 静态属性不能序列化

6. 序列化多个对象可以借助集合ArrayList实现

   - ```java
     public class Demo06 {
         public static void main(String[] args) throws Exception{
             //1.创建对象流
             FileOutputStream fos=new FileOutputStream("d:\\stu.bin");//二进制文件
             ObjectOutputStream oos=new ObjectOutputStream(fos);
             //2.序列化(写入操作)
             Student zhangsan=new Student("张三",20);
             Student lisi=new Student("李四",22);
             ArrayList<Student> list = new ArrayList<>();
             list.add(zhangsan);
             list.add(lisi);
             oos.writeObject(list);
             //oos.writeObject(zhangsan);
             //3.关闭（close自带flush）
             oos.close();
             System.out.println("执行完毕");
         }
     }
     ```

   - ```java
     public class Demo07 {
         public static void main(String[] args) throws Exception{
             //1.创建一个对象流
             FileInputStream fis=new FileInputStream("d:\\stu.bin");
             ObjectInputStream ois=new ObjectInputStream(fis);
             //2.读取文件(反序列化
             //Student s=(Student) ois.readObject();
             ArrayList<Student> list = (ArrayList<Student>) ois.readObject();
             //3.关闭
             ois.close();
             System.out.println(list.toString());
             //System.out.println(s.toString());
         }
     }
     ```

     

## 常见字符编码

1. ISO-8859-1 采用1个字节，最多表示256个字符。收录除ASCII外，还包括西欧、希腊语、泰语、阿拉伯语、希伯来语对应的文字负号
2. UTF-8 针对Unicode码的可变长度字符编码
3. GB2312 简体中文
4. GBK 简体中文、扩充
5. BIG5 繁体中文

## 字符流

### 字符流的父类(抽象类)

1. Reader：字符输入流
   - public int read()
   - public int read(char[] c)
   - public int read(char[] b ,int off, int len)
2. Writer：字符输出流
   - public void write(int n)
   - public void write(String str)
   - public void write(char[] c)
3. UTF-8对中文是3个字节1个字符

### 文件字符流（子类）

1. FileReader:

   - public int read(char[] c)  从流中读取多个字符，将读到的内容存入c数组，返回实际读到的字符数；如果达到文件的尾部，返回-1

   - 继承：java.lang.Object -> java.io.Reader -> java.io.InputStreamReader -> java.io.FileReader

   - 用来读取字符文件的便捷类。此类的构造方法假定默认字符编码和默认字节缓冲区大小都是适当的。

   - ```java
     /**
      * 使用FileReader读取文件
      */
     public class Demo02 {
         public static void main(String[] args) throws Exception{
             //1.创建FileReader 文件字符输入流
             FileReader fr=new FileReader("d:\\hello.txt");
             //2.读取
             //2.1单个字符读取
             /*int data=0;
             while((data=fr.read())!=-1){//读取一个字符
                 System.out.print((char) data);
             }*/
             char[] buf=new char[1024];
             int count=0;
             while((count=fr.read(buf))!=-1){
                 System.out.println(new String(buf,0,count));
             }
             //3.关闭
             fr.close();
         }
     }
     ```

2. FileWriter:

   - public void write(String str)  一次写多个字符，将b数组中所有字符，写入输出流

   - 继承：java.lang.Object -> java.io.Reader -> java.io.InputStreamReader -> java.io.FileReader

   - ``` java
     /**
      * 使用FileWriter 写入文件
      */
     public class Demo03 {
         public static void main(String[] args) throws Exception{
             //1.创建FileWriter对象
             FileWriter fw=new FileWriter("d:\\write.txt");
             //2.写入
             for (int i = 0; i < 10; i++) {
                 fw.write("java是世界上最好的语言\r\n");
                 //fw.flush();
             }
             //3.关闭
             fw.close();
             System.out.println("执行完毕");
         }
     }
     ```

### 字符流复制文件

1. 只能复制文本文件，不能复制图片和二进制文件

2. 字节流可以复制任意文件

3. ```java
   /**
    * 使用FileReader和FileWriter复制文本文件，不能复制图片或者二进制文件
    */
   public class Demo04 {
       public static void main(String[] args) throws Exception{
           //1.创建FileReader 和 FileWriter
           FileReader fr=new FileReader("d:\\write.txt");
           FileWriter fw=new FileWriter("d:\\write2.txt");
           //2.读写
           int data=0;
           while((data= fr.read())!=-1){
               fw.write(data);
           }
           //3.关闭
           fr.close();
           fw.close();
       }
   }
   ```

### 字符缓冲流

1. 缓冲流：BufferedReader/BufferedWriter
   - 高效读写
   - 支持输入换行符
   - 可一次写一行、读一行
   - 继承：java.io.Reader -> java.io.BufferedReader
   - 从字符输入流中读取文本，缓冲各个字符，从而实现字符、数组和行的高效读取
   - 其中有readlin方法读取一行，若返回为null则表示到尾部

### BufferedReader的使用

读取中文乱码问题：[(51条消息) FileReader读取中文字符乱码问题_wjw的博客-CSDN博客](https://blog.csdn.net/wjw521wjw521/article/details/72831704)

若改了后还是不行就将文件另存为设置编码为UTF-8

```java
/**
 * 使用字符缓冲流读取文件
 * BufferedReader
 */
public class Demo05 {
    public static void main(String[] args) throws Exception{
        //1.创建缓冲流
        FileReader fr=new FileReader("d:\\write.txt");
        BufferedReader br=new BufferedReader(fr);
        //2.读取
        //2.1第一种方式
//        char[] buf=new char[1024];//自己创建缓冲区
//        int count=0;
//        while((count= br.read(buf))!=-1){
//            System.out.println(new String(buf,0,count));
//        }
        //2.2第二种方式,以行读
        String line = null;
        while((line=br.readLine())!=null){
            System.out.println(line);
        }
        //3.关闭
        br.close();
    }
}
```

### BufferedWriter的使用

```java
/**
 * 演示BufferedWriter的使用
 */
public class Demo06 {
    public static void main(String[] args) throws Exception{
        //1.创建BufferedWriter对象
        FileWriter fw = new FileWriter("d:\\buffer.txt");
        BufferedWriter bw = new BufferedWriter(fw);
        //2.写入
        for (int i = 0; i < 10; i++) {
            bw.write("好好学习，天天上上");
            bw.newLine();//写入一个换行符 windows \r\n  linux \n
        }
        //3.关闭
        bw.close();
    }
}
```

## PrintWriter类

1. 继承：java.lang.Object -> java.io.Writer -> java.io.PrintWriter

2. 向文本输出流打印对象的格式化表示形式。此类实现在PrintStream中的所有print方法，它不包含用于写入原始字节的方法。

3. 封装了print()/println()方法，支持写入后换行

4. 支持数据原样打印，将其原样打印到文件里面，与write类似

   ```java
   /**
    * 演示PrintWriter的使用
    */
   public class Demo07 {
       public static void main(String[] args) throws Exception{
           //1.创建打印流
           PrintWriter pw = new PrintWriter("d:\\print.txt");
           //2.打印
           pw.println(97);
           pw.println(true);
           pw.println(3.14);
           pw.println('c');
           //3.关闭
           pw.close();
       }
   }
   ```

## 转换流

### 概念

1. 桥转换流：：InputStreamReader/OutputStreamWriter
   - 可将字节流转换成字符流
   - 可设置字符的编码方式
   - 内存中的字符与硬盘中的字节的转换

### 转换流的使用

1. InputStreamReader的使用

2. ``` java
   /**
    * 使用InputStreamReader读取文件，可以指定使用的编码
    */
   public class Demo01 {
       public static void main(String[] args) throws Exception{
           //1.创建InputStreamReader对象
           FileInputStream fis = new FileInputStream("d:\\write.txt");
           InputStreamReader isr = new InputStreamReader(fis,"utf-8");//要保证与文件编码一致
           //2.读取文件
           int data=0;
           while ((data=isr.read())!=-1){
               System.out.print((char) data);
           }
           //3.关闭
           isr.close();
       }
   }
   ```

3. OutputStreamWriter的使用

4. ```java
   /**
    * 使用OutputStreamWriter写入文件，使用指定的编码
    */
   public class Demo02 {
       public static void main(String[] args) throws Exception{
           //1.创建OutputStreamWriter对象
           FileOutputStream fos = new FileOutputStream("d:\\info.txt");
           OutputStreamWriter osw = new OutputStreamWriter(fos,"gbk");
           //2.写入
           for (int i = 0; i < 10; i++) {
               osw.write("我爱四川，我爱家乡\r\n");
           }
           //3.关闭
           osw.close();
       }
   }
   ```

## File类

### 概念

1. 代表物理盘符中的一个文件或文件夹
2. 方法：
   - createNewFile()  //创建一个新文件
   - mkdir()  //创建一个新目录
   - delete()  //删除文件或空目录
   - exists()  //判断File对象所代表的对象是否存在
   - getAbsolutePath()  //获取文件的绝对路径
   - getName()  //取得名字
   - getParent()  //获取文件/目录所在目录
   - isDirectory()  //是否是目录
   - isFile()  //是否是文件
   - length()  //获得文件长度
   - listFiles()  //列出目录中所有内容
   - renameTo()  //修改文件名为
3. 路径分隔符;
4. 名称分隔符\

### 文件操作

```java
/**
 * File类的使用
 * (1) 分隔符
 * (2) 文件操作
 * (3) 文件夹操作
 */
public class Demo01 {
    public static void main(String[] args) throws Exception {
        //separator();
        fileOpe();
    }
    //(1) 分隔符
    public static void separator(){
        System.out.println("路径分隔符"+ File.pathSeparator);
        System.out.println("名称分隔符"+File.separator);
    }
    //(2) 文件操作
    public static void fileOpe() throws Exception{
        //1.创建文件
        File file = new File("d:\\file.txt");//这里是创建文件对象
        if(!file.exists()) {//判断是否存在
            boolean b = file.createNewFile();
            System.out.println("创建结果：" + b);//true为创建成功,已经存在则返回false
        }
        //2.删除文件
        //2.1直接删除
        //System.out.println("删除结果:"+file.delete());//true表示删除成功

        //2.2使用jvm退出时删除
//        file.deleteOnExit();
//        Thread.sleep(5000);

        //3.获取文件信息
        System.out.println(file.getAbsoluteFile());//绝对路径
        System.out.println(file.getPath());//获取路径，写的什么就是什么
        System.out.println("获取文件名称："+file.getName());
        System.out.println("获取父目录："+file.getParent());
        System.out.println("获取文件长度"+file.length());
        System.out.println("文件创建时间:"+new Date(file.lastModified()).toString());
        //4.判断
        System.out.println("是否可写："+file.canWrite());//true为可写
        System.out.println("是否是文件："+file.isFile());
        System.out.println("是否隐藏："+file.isHidden());

    }
}
```

### 文件夹操作

```java
//注意删除部分的操作
/**
 * File类的使用
 * (1) 分隔符
 * (2) 文件操作
 * (3) 文件夹操作
 */
public class Demo01 {
    public static void main(String[] args) throws Exception {
        directoryOpe();
    }
    //(3) 文件夹操作
    public static void directoryOpe() throws Exception{
        //1.创建文件夹
        File dir = new File("d:\\aaa\\bbb\\ccc");
        if(!dir.exists()){
            //dir.mkdir();//只能创建单级目录
            System.out.println("创建结果："+dir.mkdirs());//创建多级目录
        }
        //2.删除文件夹
        //2.1直接删除
        //System.out.println("删除结果："+dir.delete());//只能删除最底层，且必须为空目录
        //2.2使用jvm删除
//        dir.deleteOnExit();//同上要求
//        Thread.sleep(5000);

        //3.获取文件夹信息
        System.out.println("获取绝对路径："+dir.getAbsoluteFile());
        System.out.println("获取路径："+dir.getPath());
        System.out.println("获取文件夹名称："+dir.getName());//最底层文件夹名称
        System.out.println("获取父目录:"+dir.getParent());
        System.out.println("获取创建时间："+new Date(dir.lastModified()).toLocaleString());

        //4.判断
        System.out.println("是否是文件夹："+dir.isDirectory());
        System.out.println("是否是隐藏："+dir.isHidden());

        //5.遍历文件夹
        File dir2 = new File("d:\\图片");
        String[] files = dir2.list();
        for (String string : files) {
            System.out.println(string);
        }

    }
}
```

## FileFilter接口(文件过滤器)

1. public interface FileFilter

   - boolean accept(File pathname)
   - 当调用File类中的listFiles()方法时，支持传入FileFilter接口接口实现类，对获取文件进行过滤，只有满足条件的文件才可以出现在listFiles()的返回值中

2. 使用

3. ```java
   /**
    * File类的使用
    * (1) 分隔符
    * (2) 文件操作
    * (3) 文件夹操作
    */
   public class Demo01 {
       public static void main(String[] args) throws Exception {
           //separator();
           //fileOpe();
           directoryOpe();
       }
       //(1) 分隔符
       public static void separator(){
           System.out.println("路径分隔符"+ File.pathSeparator);
           System.out.println("名称分隔符"+File.separator);
       }
       //(2) 文件操作
       public static void fileOpe() throws Exception{
           //1.创建文件
           File file = new File("d:\\file.txt");//这里是创建文件对象
           if(!file.exists()) {//判断是否存在
               boolean b = file.createNewFile();
               System.out.println("创建结果：" + b);//true为创建成功,已经存在则返回false
           }
           //2.删除文件
           //2.1直接删除
           //System.out.println("删除结果:"+file.delete());//true表示删除成功
   
           //2.2使用jvm退出时删除
   //        file.deleteOnExit();
   //        Thread.sleep(5000);
   
           //3.获取文件信息
           System.out.println(file.getAbsoluteFile());//绝对路径
           System.out.println(file.getPath());//获取路径，写的什么就是什么
           System.out.println("获取文件名称："+file.getName());
           System.out.println("获取父目录："+file.getParent());
           System.out.println("获取文件长度"+file.length());
           System.out.println("文件创建时间:"+new Date(file.lastModified()).toString());
           //4.判断
           System.out.println("是否可写："+file.canWrite());//true为可写
           System.out.println("是否是文件："+file.isFile());
           System.out.println("是否隐藏："+file.isHidden());
   
       }
   
       //(3) 文件夹操作
       public static void directoryOpe() throws Exception{
           //1.创建文件夹
           File dir = new File("d:\\aaa\\bbb\\ccc");
           if(!dir.exists()){
               //dir.mkdir();//只能创建单级目录
               System.out.println("创建结果："+dir.mkdirs());//创建多级目录
           }
           //2.删除文件夹
           //2.1直接删除
           //System.out.println("删除结果："+dir.delete());//只能删除最底层，且必须为空目录
           //2.2使用jvm删除
   //        dir.deleteOnExit();//同上要求
   //        Thread.sleep(5000);
   
           //3.获取文件夹信息
           System.out.println("获取绝对路径："+dir.getAbsoluteFile());
           System.out.println("获取路径："+dir.getPath());
           System.out.println("获取文件夹名称："+dir.getName());//最底层文件夹名称
           System.out.println("获取父目录:"+dir.getParent());
           System.out.println("获取创建时间："+new Date(dir.lastModified()).toLocaleString());
   
           //4.判断
           System.out.println("是否是文件夹："+dir.isDirectory());
           System.out.println("是否是隐藏："+dir.isHidden());
   
           //5.遍历文件夹
           File dir2 = new File("d:\\图片");
           String[] files = dir2.list();
           for (String string : files) {
               System.out.println(string);
           }
           System.out.println("------FileFilter接口使用-------");
           File[] files2 = dir2.listFiles(new FileFilter() {//匿名内部类方式
               @Override
               public boolean accept(File pathname) {
                   if(pathname.getName().endsWith(".jpg")) {//endWith判断后缀
                       return true;//表示可以被遍历到
                   }
                   return false;
               }
           });
           for (File file : files2) {
               System.out.println(file.getName());
           }
       }
   }
   ```

## 递归遍历与递归删除

```java
/**
 * 递归遍历文件夹
 * 递归删除文件夹
 */
public class ListDemo {
    public static void main(String[] args) {
        listDir(new File("d:\\myfiles"));
    }
    public static void listDir(File dir) {
        File[] files=dir.listFiles();
        System.out.println(dir.getAbsolutePath());
        if(files.length>0&&files!=null){
            for (File file : files) {
                if(file.isDirectory()){
                    listDir(file);
                }
                else {
                    System.out.println(file.getAbsolutePath());
                }
            }
        }
    }

    public static void deleteDir(File dir) {
        File[] files = dir.listFiles();
        if(files.length>0&&files!=null){
            for (File file : files) {
                if(file.isDirectory()){
                    deleteDir(file);
                }
                else {
                    System.out.println(file.getAbsolutePath()+"删除："+file.delete());
                }
            }
        }
        System.out.println(dir.getAbsolutePath()+"删除："+dir.delete());
    }
}
```

## Properties

1. Properties:属性集合，继承Hashtable

2. 特点：
   - 存储属性名和属性值
   - 属性名和属性值都是字符串类型
   - 没有泛型
   - 和流有关
   
3. 使用

4. ```java
   /**
    * 演示Properties集合的使用
    */
   public class Demo02 {
       public static void main(String[] args) throws Exception{
           //1.创建集合
           Properties properties = new Properties();
           //2.添加数据
           properties.setProperty("username","zhangsan");
           properties.setProperty("age","20");
           System.out.println(properties.toString());
           //3.遍历
           //3.1使用keySet
           //3.2使用entrySet
           //3.3使用StringPropertyNames()
           Set<String> pronames = properties.stringPropertyNames();
           for (String pro : pronames) {
               System.out.println(pro+"==="+properties.getProperty(pro));
           }
   
           //4.与流有关的方法
           //--------list方法----------
   //        PrintWriter pw=new PrintWriter("d:\\print.txt");
   //        properties.list(pw);
   //        pw.close();
   
           //-------store 保存--------
   //        FileOutputStream fos = new FileOutputStream("d:\\print.properties");
   //        properties.store(fos,"注释");
   //        fos.close();
   
           //-------load 加载--------
           Properties properties2 = new Properties();
           FileInputStream fis = new FileInputStream("d:\\print.properties");
           properties2.load(fis);
           fis.close();
           System.out.println(properties2.toString());
   
       }
   }
   ```

5. java.util.Properties集合继承于Hashtable，来表示一个持久的属性集，他使用键值结构存储数据，每个键及其对应的值都是一个字符串，该类被许多java类使用，比如获取系统属性时，System.getProperties，方法就是返回一个Properties对象

6. properties集合是唯一一个与IO流相结合的集合
   可以使用Properties集合中的方法store把集合中的数据持久化
   可以使用Properties集合中的load方法，把硬盘中保存的文件（键值对）存储到集合中使用，这在项目中 用于读取配置文件经常使用到

7. 属性表中每个键及其对应值都是一个字符串
   Properties集合是一个双列集合（双列集合是每个元素由键和值两部分组成，由键可以找到值，键必须是唯一的，值可以重复）

8. 构造方法：

   - public properties（） 创建一个空的属性列表

     基本的存储方法：
     public Object setProperty（String key，String value） ：保存一对属性
     public String setProperties（String key） :使用此属性列表中指定的键搜索属性值
     public Set stringPropertNames（） 获取所有名称的集合

   - ```java
     public class Main {
         public static void main(String[] args) {
             Properties properties = new Properties();
             //存入键值对
             properties.setProperty("one","1");
             properties.setProperty("two","2");
             //拿出所有键
             Set<String> strings = properties.stringPropertyNames();
             //遍历键
             for (String string : strings) {
                 //通过键获取值
                 String property = properties.getProperty(string);
                 //输出
                 System.out.println(string+":"+property);
             }
         }
     }
     ```

   - 结果：

     - one：1
     - two：2

9. 与流有关的用法：

   - store ( OutputStream out, String comments) ： 以适合使用 load 方法加载到 Properties 表中的格式，将此 Properties 表中的属性列表（键和元素对）写入输出流。与 load 方法相反，该方法将键 - 值对写入到指定的文件中去。

     参数中使用了字节输入流，通过流对象，可以关联到某文件上，这样就可以能够加载文本中的数据了，文本数据

   - ```java
     public class Main {
         public static void main(String[] args) throws IOException {
             Properties properties = new Properties();
             //存入键值对
             properties.setProperty("one","1");
             properties.setProperty("two","2");
             //加载文本中信息到属性集
             properties.store(new FileWriter("c.text"),"savedate");
             //拿出所有键
             Set<String> strings = properties.stringPropertyNames();
         }
     }
     ```

   - 结果

     - 在c.txt中
     - #savedate
     - #Sun Jul 19 10：38：05 CST 2020
     - one = 1
     - two = 2

   - public void load(InputStream inStream) ： 从字节输入流中读取键值对。

     注意：
     1.存储键值对的文件中，键与值默认的链接符号可以使用=，空格等其他符号
     2.存储键值对的文件中，可以使用“#”进行注释，被注释的键值对默认不会被读取
     3.存储键值对的文件中，键与值都是字符串，不要加引号

   - ```java
     public class Main {
         public static void main(String[] args) throws IOException {
             Properties properties = new Properties();
             properties.load(new FileReader("c.text"));
             //拿出所有键
             Set<String> strings = properties.stringPropertyNames();
             for (String string : strings) {
                 System.out.println(string+":"+properties.getProperty(string));
             }
         }
     }
     ```

   - 结果

     - one：1
     - two：2

10. 此处参考博客：

    []: https://www.cnblogs.com/pjhaymy/p/13338986.html#:~:text=java.uti,erties%E5%AF%B9%E8%B1%A	"Properties集合基础"