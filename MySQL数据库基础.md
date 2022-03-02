## MySQL数据库

### 什么是数据库

1. 数据库（DB，DataBase）
2. 概念：数据仓库，软件，安装在操作系统（windows，linux，mac...）之上！
3. 作用：存储数据，管理数据

### 数据库分类

1. 关系型数据库：（SQL）
   - MySQL，Oracle，Sql Server，DB2，SQLite
   - 通过表与表之间，行与列之间的关系进行数据存储
2. 非关系型数据库：（NoSQL）Not Only
   - Redis，MongDB
   - 非关系型数据库，对象存储，通过对象自身的属性来决定
3. DBMS（数据库管理系统）
   - 数据库管理软件，科学有效的管理我们的数据。维护和获取数据
   - MySQL，数据库管理系统

### MySQL简介

MySQL是一个关系型数据库管理系统

前世：瑞典MySQL AB 公司

今生：属于Oracle旗下产品

MySQL是最好的RDBMS（Relational Database Management System，关系数据库管理里系统）应用软件之一

开源的数据库软件

体积小、速度快、总体拥有成本低

## 安装MySQL

1. 参考教程：[(14条消息) 狂神说MySQL01：初识MySQL_狂神说-CSDN博客](https://blog.csdn.net/qq_33369905/article/details/105828923)

2. 下载5.7版本压缩包，使用官网exe卸载会很麻烦

3. 解压后，将其解压到想要的目录

4. 添加环境变量

   - 我的电脑 -> 属性 -> 高级 -> 环境变量

   - 选择PATH，在其后面添加：解压出来的mysql文件夹的bin文件夹目录，将其粘贴到PATH

   - 在与bin文件夹同层级下新建my.ini文件并编辑，注意替换路径！

   - ```java
     [mysqld]
     basedir=D:\Program Files\mysql-5.7\
     datadir=D:\Program Files\mysql-5.7\data\
     port=3306
     skip-grant-tables
     ```

   - 注意目录复制后要加上\

   - 再将basedir的路径覆盖datadir中data前的路径，注意data刚开始就是没有的！

5. 在管理员模式下运行CMD，并将路径切换至mysql下的bin目录，然后输入mysqld –install (安装mysql)

   - 输入cd /d D:\mysql-5.7.19\mysql-5.7.19-winx64\bin（注意替换路径为自己的bin目录）
   - 输入mysqld –install

6. 再输入  mysqld --initialize-insecure --user=mysql 初始化数据文件

7. 然后输入 net start mysql 启动mysql

8. 用命令 mysql –u root –p 进入mysql管理界面（密码可为空），注意-p后面没有空格

9. 进入界面后更改root密码

   - update mysql.user set authentication_string=password('123456') where user='root' and Host = 'localhost';

10. 刷新权限

    - flush privileges;

11. 修改 my.ini文件删除最后一句skip-grant-tables（加个#注释掉）

12. 输入exit或者ctrl+z退出

13. 重启mysql即可正常使用

    - 先net stop mysql
    - 再net start mysql

14. 输入mysql –u root –p进入管理界面，输入密码123456成功

## 可视化工具SQLyog

### 安装sqlyog

1. 下载sqlyog12.08
2. 安装好后打开
3. 注册码使用狂神提供[【狂神说Java】MySQL最新教程通俗易懂_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1NJ411J79W?p=4&spm_id_from=pageDriver)
4. 看到连接我的MySQL主机
   - 保存的连接随意写：这里写localhost
   - 我的SQL主机地址：这里写localhost
   - 用户名与密码为MySQL安装过程中设置的root与密码
   - 端口3306
   - 启动MySQL后点击连接
5. 使用SQLyog管理工具自己完成以下操作 :
   - 新建school数据库，在root@localhost处右键
   - 默认编码方式utf8
   - 数据库排序规则utf8_general_ci
6. 每一个sqlyog的执行操作，本质就是对应了一个sql，可以在软件的历史记录中查看
7. 在school数据库中表处右键创建表
   - 表名称自己填，此处student
   - 引擎为InnoDB，默认也是这个
   - 字符集utf8，核对utf8_general_ci
   - 列名分别为id，name，age
   - ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210713134440.png)
8. 找到student表，右键打开表，添加数据

## 命令行连接数据库

1. 命令行连接：

   ```sql
   mysql -u root -p -- 连接数据库
   update mysql.user set authentication_string=password('123456') where user='root' and Host = 'localhost'; -- 修改密码
   flush privileges; -- 刷新权限
   -- 所有的语句都使用分号；结尾
   
   show databases; -- 查看所有数据库
   
   use school; -- 切换数据库 use 数据库名
   show tables; -- 查看数据库中所有表
   describe student; --显示数据库中表中所有信息
   
   create database westos; -- 创建一个数据库
   
   exit; -- 退出连接
   
   -- 单行注释
   /*
   多行注释
   */
   ```

2. 数据库xxx语言  本质：CRUD增删改查

   - DDL 定义
   - DML 操作
   - DQL 查询
   - DCL 控制

## 操作数据库

操作数据库 -> 操作数据库中的表 -> 操作数据库中表的数据

mysql关键字不区分大小写

### 操作数据库

中括号代表可选，大括号代表必选

如果表名或者字段名是一个关键字，则需要带上``

1. 创建数据库

   ```sql
   CREATE DATABASE [IF NOT EXISTS] westos
   ```

2. 删除数据库

   - ```sql
     DROP DATABASE [IF EXISTS] westos
     ```

3. 使用数据库

   ```sql
   use school
   ```

4. 查看数据库

   ```sql
   SHOW DATABASES -- 查看所有数据库
   ```

5. 学习思路

   - 对照sqlyog可视化历史记录查看sql
   - 固定的语法或关键字必须要强行记住

### 数据库的列类型

```sql
-- 数值
```

- tinyint   十分小的数据   1个字节
- smallint   较小的数据   2个字节
- **int           标准的整数    4个字节**
- bigint       较大的数据    8个字节
- float         浮点数           4个字节
- double     浮点数           8个字节（精度问题）
- decimal    字符串形式的浮点数     金融计算时，一般使用   decimal语法格式“DECIMAL(M,D)”。其中，M是数字的最大数（精度），其范围为“1～65”，默认值是10；D是小数点右侧数字的数目（标度），其范围是“0～30”，但不得超过M。

```sql
-- 字符串
```

- char          字符串固定大小的      0-255
- **varchar      可变长字符串            0-65535       常用的变量**   类似javaString
- tinytext       微型文本                    2^8-1
- **text             文本串                       2^16-1**         保存大文本

```sql
-- 时间日期
```

java.util.Date

- date           YYYY-MM-DD       日期格式
- time           HH：mm：ss        时间格式
- **datetime    YYYY-MM-DD   HH：mm：ss   最常用的时间格式**
- **timestamp   时间戳                1970.1.1到现在的毫秒数！也较为常用**
- year            年份表示

```sql
null
```

- 没有值，未知
- == 注意，不要使用NULL进行运算，结果为NULL ==

### 数据库的字段属性（重点）

1. Unsigned：
   - 无符号的整数
   - 声明了该列不能声明为负数
2. zerofill：
   - 0填充的
   - 不足的位数，使用0来填充   int(3)   ,  5   ---  005
3. 自增
   - 通常理解为自增，自动在上一条记录的基础上+1（默认）
   - 通常用来设计唯一的主键~ index，必须是整数类型
   - 可以自定义设置主键自增的起始值和步长（sqlyog表中高级选项）
4. 非空 NULL not null
   - 假设设置为not null ，如果不赋值就会报错！
   - NULL，如果不填写值，默认就是null！
5. 默认
   - 设置默认值！
   - 如果不指定值，则会有默认值
6. 做项目需要的字段：表示一个记录存在的意义
   - id  主键
   - version 乐观锁
   - is_delete  伪删除
   - gmt_create  创建时间
   - gmt_update  修改时间

### 创建数据库表

1. 注意点：使用英文()，表的名称和字段尽量使用``括起来

2. AUTO_INCREMENT  自增

3. 字符串使用单引号或者双引号括起来

4. 所有语句后面加,（英文逗号），最后一句不用

5. default表示默认值

6. primary key表示主键

7. 最后写上engine=innodb default charset=utf-8

   ```sql
   CREATE TABLE IF NOT EXISTS `student` (
   
       `id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
       `name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
       `pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
       `sex` VARCHAR(2) NOT NULL DEFAULT '女' COMMENT '性别',
       `birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
       `address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
       `email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
       PRIMARY KEY(`id`)
   )ENGINE=INNODB DEFAULT CHARSET=utf8
   ```

8. 格式

   ```sql
   CREATE TABLE [IF NOT EXISTS] `表名`(
   	`字段名` 列类型 [属性] [索引] [注释],
   	`字段名` 列类型 [属性] [索引] [注释],
       `字段名` 列类型 [属性] [索引] [注释]
   )[表类型][字符集设置][注释]
   ```

9. 常用命令

   ```sql
   SHOW CREATE DATABASE school -- 查看创建数据库的语句
   SHOW CREATE TABLE student  -- 查看student数据表的定义语句
   DESC student  -- 显示表的结构
   ```

### 数据表的类型

1. 关于数据库引擎

   - INNODB  默认使用
   - MYISAM  早些年使用的

   |            | MyISAM | InnoDB        |
   | ---------- | ------ | ------------- |
   | 事务支持   | 不支持 | 支持          |
   | 数据行锁定 | 不支持 | 支持          |
   | 外键约束   | 不支持 | 支持          |
   | 全文索引   | 支持   | 不支持        |
   | 表空间大小 | 较小   | 较大，约为2倍 |

2. 常规使用操作

   - MyISAM  节约空间，速度较快
   - InnoDB  安全性高，事务的处理，多表多用户操作

3. 在物理空间存在的位置

   - 所有的数据库文件都存在 data 目录下，一个文件夹对应一个数据库
   - 本质还是文件的存储！

4. MySQL引擎在物理文件上的区别

   - InnoDB在数据库表中只有一个 *.frm文件，以及上级目录下的ibdata1文件
   - MyISAM对应文件
     - *.frm   表结构的定义文件
     - *.MYD   数据文件（data）
     - *.MYI    索引文件（index）

5. 设置数据库表的字符集编码

   ```sql
   CHARSET=UTF8
   ```

   不设置时会是MySQL默认的字符集编码（不支持中文！）

   MySQL的默认编码是Latin1，不支持中文

   可以在my.ini中配置默认编码

   ```sql
   character-set-server=utf8
   ```

### 修改删除表

1. 修改

   ```sql
   -- 修改表名 ALTER TABLE 旧表名 RENAME AS 新表名
   ALTER TABLE teacher RENAME AS teacher1
   -- 增加表的字段  ALTER TABLE 表名 ADD 字段名 列属性
   ALTER TABLE teacher1 ADD age INT(11)
   -- 修改表的字段  （重命名，修改约束！）
   -- ALTER TABLE 表名 MODIFY 字段名 列属性[]
   ALTER TABLE teacher1 MODIFY age1 VARCHAR(11)  -- 修改约束
   -- ALTER TABLE 表名 CHANGE 旧名字 新名字 列属性[]
   ALTER TABLE teacher1 CHANGE age1 age INT(11)  -- 字段重命名
   -- 注意：网上结论为change用来字段重命名，不能修改字段类型和约束
   --       modify不能用来字段重命名，只能修改字段类型和约束
   -- 但是实际发现，change也能修改字段类型和约束  所以此处有点问题，一般不这么改
   
   -- 删除表的字段
   ALTER TABLE teacher1 DROP age
   ```

2. 删除

   ```sql
   -- 删除表(如果表存在)
   DROP TABLE IF EXISTS teacher1
   ```

   所有的创建和删除操作尽量加上判断，以免报错

3. 注意点：

   - ``字段名使用反引号包裹
   - 注释使用 -- /**/
   - sql关键字大小写不敏感，建议小写
   - 所有符号全部使用英文

## MySQL数据管理

### 外键（了解即可）

1. 方式一：在创建表的时候，增加约束（较为复杂）

   ```sql
   CREATE TABLE `grade`(
       `gradeid` int(10) not null auto_increment comment '年级id',
       `gradename` varchar(50) not null comment '年级名称',
       primary key(`gradeid`)
   )engine=INNODB default charset=utf8
   
   -- 学生表的 gradeid 字段要去引用年级表的 gradeid
   -- 定义外键key
   -- 给这个外键添加约束（执行引用） reference引用
   
   show create table student
   
   CREATE TABLE `student` (
     `id` int(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
     `name` varchar(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
     `pwd` varchar(20) NOT NULL DEFAULT '123456' COMMENT '密码',
     `sex` varchar(2) NOT NULL DEFAULT '女' COMMENT '性别',
     `birthday` datetime DEFAULT NULL COMMENT '出生日期',
     `gradeid` int(10) NOT NULL COMMENT '学生的年级',
     `address` varchar(100) DEFAULT NULL COMMENT '家庭住址',
     `email` varchar(50) DEFAULT NULL COMMENT '邮箱',
     PRIMARY KEY (`id`),
     KEY `FK_gradeid` (`gradeid`),
     CONSTRAINT `FK_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `grade` (`gradeid`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8
   ```

   删除有外键关系的表的时候，必须要先删除引用别人的表（从表），再删除被引用的表（主表）

2. 创建表成功后，添加外键约束

   ```sql
   -- 创建表的时候没有外键
   ALTER TABLE `student`
   ADD CONSTRAINT `FK_gradeid` FOREIGN KEY(`gradeid`) references `grade`(`gradeid`);
   
   -- ALTER TABLE 表名 ADD CONSTRAINT 约束名 FOREIGN KEY(作为外键的列) REFERENCES 哪个表（哪个字段）
   ```

   以上的操作都是物理外键，数据库级别的外键，不建议使用！（避免数据库过多造成困扰肉）

   最佳实践

   - 数据库只是单纯的表，只用来存数据，只有行（数据）和列（字段）
   - 我们想使用多张表的数据，想使用外键（程序去实现）

### DML语言（全部记住）

1. 数据库意义：数据存储，数据管理
2. DML语言：数据操作语言
   - Insert
   - update
   - delete

### 添加

**Insert语句**

```sql
-- 插入语句（添加）
INSERT INTO 表名([字段1,字段2,字段3,]) VALUES('值1'),('值2'),('值3'),('值4')...
INSERT INTO `grade`(`gradename`) VALUES('大四')

-- 由于主键自增我们可以省略（如果不写表的字段，它就会一一匹配）
-- INSERT INTO `grade` VALUES('大四') -- 此时对应的是自增的主键，而gradename则是null，所以报错

-- 一般写插入语句，我们一定要数据和字段一一对应！

-- 插入多个字段
INSERT INTO `grade`(`gradename`)
VALUES('大二'),('大一')  -- 注意这里逗号隔开两行，若同一行则在一个括号内

INSERT INTO `student`(`name`) VALUES('张三')

INSERT INTO `student`(`name`,`pwd`,`sex`) VALUES('张三','aaaaaa','男')

INSERT INTO `student`(`name`,`pwd`,`sex`)
VALUES('李四','aaaaaa','男'),('王五','aaaa','男')
```

语法: INSERT INTO 表名([字段1,字段2,字段3,]) VALUES('值1'),('值2'),('值3'),('值4')...	

注意事项：

1. 字段和字段之间用 英文逗号 隔开
2. 字段可以省略，但是后面值必须要与表一一对应
3. 可以同时插入多条数据，VALUES 后面的值需要用 , 隔开 VALUES() , ()

### 修改

**update 语句**

```sql
-- 修改学员名字  带简介
UPDATE `student` SET `name`='sucker' where id=1;

-- 不指定条件的情况下，会改动所有表！
UPDATE `student` SET `name`='sucker'

-- 修改多个属性，逗号隔开
UPDATE `student` SET `name`='SUCKER',`email`='12312' WHERE id=1;

-- 语法：
-- UPDATE 表名 set colum_name = value,[colum_name = value,...] where [条件]
```

条件：where 子句 运算符  id等于某个值，大于某个值，在某个区间内修改...

操作符会返回布尔值

| 操作符           | 含义   | 范围        | 结果  |
| ---------------- | ------ | ----------- | ----- |
| =                | 等于   | 5=6         | false |
| <>或！=          | 不等于 | 5！=6       | false |
| >                |        |             |       |
| <                |        |             |       |
| <=               |        |             |       |
| >=               |        |             |       |
| BETWEEN...AND... | 闭区间 |             |       |
| AND              | &&     | 5>1 and 1>2 | false |
| OR               | \|\|   | 5>1 or 1>2  | true  |

```sql
-- 通过多个条件定位数据
UPDATE `student` SET `name`='长江七号' WHERE `name`='suker11' AND `sex`='女'
```

注意事项：

- column_name  是数据库的列，尽量带上``

- 条件，可以理解为筛选的条件，如果没有指定会修改所有的列

- value 是一个具体的值，也可以是一个变量

  ```sql
  UPDATE `student` SET `birthday`=CURRENT_TIME WHERE `name`='sucker1' AND `sex`='男'
  ```

### 删除

**delete命令**

语法：delete  from  表名  [where  条件]

```sql
-- 删除数据
DELETE from `student` where id = 1
```

**TRUNCATE命令**

作用：完全清空一个数据库，表的结构和索引约束不会变

```sql
-- 清空 student 表
TRUNCATE `student`
```

**delete与TRUNCATE的区别**

- 相同点：都能删除数据，都不会删除表结构

- 不同点：

  - TRUNCATE 重新设置 自增列 计数器会归零
  - TRUNCATE 不会影响事务

  ```sql
  -- 测试DELETE与TRUNCATE区别
  create table `test`(
    `id` int(4) not null auto_increment,
    `coll` varchar(20) not null,
    primary key(`id`)
  )engine=innodb default charset=utf8
  
  insert into `test`(`coll`) values('1'),('2'),('3')
  DELETE From `test` -- 不会影响自增
  
  insert into `test`(`coll`) values('1'),('2'),('3')
  Truncate table `test`  -- 自增归零
  ```

  了解即可：DELETE删除的问题   重启数据库后发生的现象：

  - InnoDB  自增量会从1开始  （因为存在内存中，断电即失）
  - MyISAM  继续从上一个自增量开始  （因为存在文件中，不会丢失）

## DQL查询数据（最重点）

### （Data Query LANGUAGE : 数据查询语言）

- 所有的查询操作都用它   Select
- 简单的查询，复杂的查询它都能做
- 数据库中最核心的语言
- 使用频率最高

```sql
-- SELECT 语法
SELECT[ALL|DISTINCT|DISTINCTROW|TOP]
{*|talbe.*|[table.]field1[AS alias1][,[table.]field2[AS alias2][,…]]}
FROM tableexpression[,…][IN externaldatabase]
[WHERE…]
[GROUP BY…] -- 指定结果按照哪几个字段来分组
[HAVING…]  -- 过滤分组的记录必须满足的次要条件
[ORDER BY…]  -- 指定查询记录按一个或多个条件排序
[limit]  -- 指定查询的记录从哪条到哪条
```

### 指定查询字段

```sql
-- 查询全部的学生  SELECT 字段 FROM 表
SELECT * FROM student

SELECT * FROM result

-- 查询指定字段
SELECT `StudentNo`,`StudentName` FROM student

-- 起别名，给结果起一个名字  AS    表头更名
-- 也可以给表起别名
SELECT `StudentNo` AS 学号,`StudentName` AS 学生姓名 FROM student AS s

-- 函数 CONCAT(A,B)  拼接字符串
SELECT CONCAT('姓名: ',StudentName) AS 新名字 FROM student
```

语法：SELECT 字段,... FROM 表

有时候，列名不容易见名知意，可以起别名   AS    字段名  AS  别名     表名  AS  别名

### 去重

**作用，去除SELECT语句查询出的重复结果**

```sql
SELECT * FROM result -- 查询全部成绩
SELECT `StudentNo` FROM result -- 查询哪些学生参加了考试

SELECT DISTINCT `StudentNo` FROM result  -- 发现重复数据，去重
```

### 数据库的列（表达式）

```sql
SELECT VERSION()  -- 查询系统版本  （函数）
SELECT 100*3-1 AS 计算结果  -- 用于计算  （表达式）
SELECT @@auto_increment_increment  -- 查询自增步长  （变量）

-- 学员考试成绩 +1分 查看
SELECT `StudentNo`,`StudentResult`+1 AS 加分后 FROM result

```

**数据库中表达式：文本值，列，null，函数，计算表达式，系统变量...**

select 表达式  from  表

### where条件子句

**作用：检索数据中符合条件的值**

**搜索的条件由一个或多个表达式组成！结果 布尔值**

1. 逻辑运算符

   | 运算符   | 语法           | 描述                       |
   | -------- | -------------- | -------------------------- |
   | and  &&  | a and b  a&&b  | 逻辑与，两个都为真结果为真 |
   | or  \|\| | a or b  a\|\|b | 逻辑或，其中1个为真即为真  |
   | Not  ！  | Not a  ！a     | 逻辑非                     |

   **尽量使用英文字母**

   ```sql
   -- where
   select `studentNo`,`StudentResult` from result  -- 列名也不区分大小写
   
   -- 查询考试成绩在95-100范围内
   SELECT `studentNo`,`StudentResult` FROM result
   where studentresult >= 95 and studentresult <= 100
   
   -- 模糊查询（区间）
   select `StudentNo`,`StudentResult` from result
   where `StudentResult` between 95 and 100
   
   -- 除了1000号以外的学生的成绩
   SELECT `StudentNo`,`StudentResult` FROM result
   where `StudentNo` != 1000;
   
   -- !=  Not
   SELECT `StudentNo`,`StudentResult` FROM result
   WHERE not `StudentNo`=1000;
   ```

2. 模糊查询：比较运算符

   | 运算符      | 语法               | 描述                                    |
   | ----------- | ------------------ | --------------------------------------- |
   | IS NULL     | a is null          | 如果操作符为NULL，结果为真              |
   | IS NOT NULL | a is not null      | 如果操作符不为NULL，结果为真            |
   | BETWEEN AND | a between b and c  | 若a在b和c之间，结果为真                 |
   | **Like**    | a like b           | SQL匹配，如果a匹配到b，结果为真         |
   | **In**      | a in (a1,a2,a3...) | 假设a在a1,a2...其中的某个值中，结果为真 |

```sql
-- ===============模糊查询=================

-- 查询姓刘的同学
-- like结合 %(代表0-任意个字符)  _（代表一个字符）
select `StudentNo`,`StudentName` from `student`
where `StudentName` like '刘%'

-- 查询姓刘的同学名字后面只有一个字的
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE `StudentName` LIKE '刘_'

-- 查询姓刘的同学名字后面只有两个字的
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE `StudentName` LIKE '刘__'

-- 查询名字中有嘉字的
select `StudentNo`,`StudentName` from `student`
where `StudentName` like '%嘉%'

-- ===== in（具体的一个或多个值） =====
-- 查询1001，1002，1003号学员信息
SELECT `StudentNo`,`StudentName` FROM `student`
where `StudentNo` in (1001,1002,1003);

-- 查询在北京的学生
SELECT `StudentNo`,`StudentName` FROM `student`
where `Address` in ('北京','河南洛阳')

-- ===== null not null =====
-- 查询地址为空的学生 null 或者空串''
SELECT `StudentNo`,`StudentName` FROM `student`
where `Address`='' or `Address` is null 

-- 查询有出生日期的同学
SELECT `StudentNo`,`StudentName` FROM `student`
where `BornDate` is not null

-- 查询没有出生日期的同学
SELECT `StudentNo`,`StudentName` FROM `student`
where `BornDate` is null
```

### 联表查询

1. JOIN 对比

   **Join(连接的表)  on(判断条件)  连接查询**

   **where  等值查询**

   七种JOIN理论

   ![](https://img-blog.csdnimg.cn/20181103160140252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5nX18y,size_16,color_FFFFFF,t_70)

   ```sql
   -- 查询参加了考试的同学（学号，姓名，科目编号，分数）
   SELECT * FROM student
   SELECT * FROM result
   
   /*思路
   1. 分析需求，分析查询的字段来自哪些表 （连接查询）
   2. 确定使用哪种连接查询？ 7种
   确定交叉点（这两个表中哪个数据是相同的）
   判断的条件：学生表中 StudentNo = 成绩表中 StudentNo
   */
   
   -- inner join
   SELECT s.`StudentNo`,`StudentName`,`SubjectNo`,`StudentResult`
   FROM `student` AS s
   INNER JOIN result AS r
   WHERE s.StudentNo = r.StudentNo
   
   -- Right Join
   SELECT s.`StudentNo`,`StudentName`,`SubjectNo`,`StudentResult`
   FROM `student` s -- 别名可以不写 AS
   RIGHT JOIN result r
   ON s.StudentNo = r.StudentNo  -- 这里on与where作用大致相同
   
   -- Left Join
   SELECT s.`StudentNo`,`StudentName`,`SubjectNo`,`StudentResult`
   FROM `student` s -- 别名可以不写 AS
   LEFT JOIN result r
   ON s.StudentNo = r.StudentNo  -- 这里on与where作用大致相同
   ```

   | 操作       | 描述                                                         |
   | ---------- | ------------------------------------------------------------ |
   | Inner Join | 用from表为主表中的每一行去匹配另一个表，匹配条件为On语句或where语句 |
   | Left Join  | 会从左表中返回所有的值，即使右表没有匹配                     |
   | Right Join | 会从右表中返回所有的值，即使左表没有匹配                     |

   ```sql
   -- 查询缺考的同学
   SELECT s.`StudentNo`,`StudentName`,`SubjectNo`,`StudentResult`
   FROM `student` s -- 别名可以不写 AS
   LEFT JOIN result r
   ON s.StudentNo = r.StudentNo
   WHERE `StudentResult` IS NULL
   
   -- 思考题（查询参加考试的同学信息：学号、学生姓名、科目名、分数）
   -- 分析：student result subject 三张表
   
   SELECT s.`StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
   FROM student s
   RIGHT JOIN result r
   ON r.StudentNo = s.StudentNo
   INNER JOIN `subject` sub
   ON r.SubjectNo=sub.SubjectNo
   
   -- 多表查询要一步步写，先查询两张再增加
   ```

2. 自连接

   **自己的表和自己连接，核心：一张表拆为两张一样的表即可**

   **父类**

   | categoryid | categoryname |
   | ---------- | ------------ |
   | 2          | 信息技术     |
   | 3          | 软件开发     |
   | 5          | 美术设计     |
   |            |              |

   **子类**

   | pid  | categoryid | categoryname |
   | ---- | ---------- | ------------ |
   | 3    | 4          | 数据库       |
   | 2    | 8          | 办公信息     |
   | 3    | 6          | web开发      |
   | 5    | 7          | ps技术       |

   操作：查询父类对应的子类关系

   | 父类     | 子类     |
   | -------- | -------- |
   | 信息技术 | 办公信息 |
   | 软件开发 | 数据库   |
   | 软件开发 | web开发  |
   | 美术设计 | ps技术   |

   ```sql
   -- 查询父子信息
   SELECT a.`categoryname` AS '父栏目',b.`categoryname` AS '子栏目'
   FROM `category` AS a,`category` AS b
   WHERE a.`categoryid`=b.`pid`
   ```

   ```sql
   -- ========== 自连接 ===========
   CREATE TABLE `school`.`category`( 
     `categoryid` INT(3) NOT NULL COMMENT '主题id', 
     `pid` INT(3) NOT NULL COMMENT '父id',
     `categoryname` VARCHAR(10) NOT NULL COMMENT '主题名字',
   PRIMARY KEY (`categoryid`)
   ) ENGINE=INNODB AUTO_INCREMENT=9 DEFAULT CHARSET=utf8 
   
   INSERT INTO `category` (`categoryid`, `pid`, `categoryname`)
   VALUES (2,1,'信息技术'),
   (3,1,'软件开发'),
   (4,3,'数据库'),
   (5,1,'美术设计'),
   (6,3,'web开发'),
   (7,5,'ps技术'),
   (8,2,'办公信息');
   
   -- 查询父子信息
   SELECT a.`categoryname` AS '父栏目',b.`categoryname` AS '子栏目'
   FROM `category` AS a,`category` AS b
   WHERE a.`categoryid`=b.`pid`
   
   -- 查询学员所属年级（学号、学生姓名、年级名称）
   SELECT `StudentNo`,`StudentName`,`GradeName`
   FROM student s
   INNER JOIN `grade` g
   ON s.`GradeId` = g.`GradeId`
   
   -- 查询科目所属的年级 (科目名称、年级名称)
   SELECT `SubjectName`,`GradeName`
   FROM `subject` sub
   INNER JOIN `grade` g
   ON sub.`GradeId` = g.`GradeId`
   
   -- 查询参加 数据库结构-1 考试的同学信息：学号、学生姓名、科目名、分数
   SELECT s.`StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
   FROM `student` s
   INNER JOIN `result` r
   ON s.StudentNo = r.StudentNo
   INNER JOIN `subject` sub
   ON r.`SubjectNo` = sub.`SubjectNo`
   WHERE `SubjectName` = '数据库结构-1'
   ```

### 分页和排序

1. 排序

```sql
-- ========== 分页 limit 和 排序 order by =============
-- 排序：升序 ASC  ，降序  DESC
-- ORDER BY 通过哪个字段排序，怎么排

-- 查询的结果根据 成绩降序排序
SELECT s.`StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
FROM `student` s
INNER JOIN `result` r
ON s.StudentNo = r.StudentNo
INNER JOIN `subject` sub
ON r.`SubjectNo` = sub.`SubjectNo`
WHERE `SubjectName` = '数据库结构-1'
ORDER BY `StudentResult` ASC
```

2. 分页

   ```sql
   -- 为什么要分页？
    -- 缓解数据库压力，给人的体验更好
    
    -- 分页，每页只显示五条数据
    -- 语法：limit 起始行，一页显示几行
    -- 网页应用：当前，总的页数，页面的大小
    -- LIMIT 0,5  1~5
    -- LIMIT 1,5  2~6
     
   SELECT s.`StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
   FROM `student` s
   INNER JOIN `result` r
   ON s.StudentNo = r.StudentNo
   INNER JOIN `subject` sub
   ON r.`SubjectNo` = sub.`SubjectNo`
   WHERE `SubjectName` = '数据库结构-1'
   ORDER BY `StudentResult` ASC
   LIMIT 1,5
   
   -- 【pageSize：页面大小】
   -- 【(n-1)*pageSize:起始值】
   -- 【n：当前页】
   -- 【数据总数/页面大小 = 总页数】
   ```

   语法：limit(查询起始下标，pageSize)

   ```sql
   -- 查询 JAVA第一学期 课程成绩排名前十的学生，并且分数要大于80 的学生信息（学号、姓名、课程名称、分数）
   select s.`StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
   from `student` s
   inner join result r
   on s.`StudentNo` = r.`StudentNo`
   inner join `subject` sub
   on sub.`SubjectNo` = r.`SubjectNo`
   WHERE `SubjectName` = 'Java程序设计-1' AND StudentResult>=80
   order by `StudentResult` DESC
   limit 0,10
   ```

### 子查询

where (这个值是计算出来的)

本质：在where语句中嵌套一个子查询语句

```sql
-- ========= where =========

-- 1.查询数据库结构-1的所有考试结果 （学号、科目编号、成绩），降序排列
-- 方式一：使用连接查询
SELECT `StudentNo`,r.`SubjectNo`,`StudentResult`
FROM `result` r
INNER JOIN `subject` sub
ON r.SubjectNo = sub.SubjectNo
WHERE `SubjectName` = '数据库结构-1'
ORDER BY StudentResult DESC

-- 方式二：使用子查询（由里及外）
SELECT `StudentNo`,`SubjectNo`,`StudentResult`
FROM `result`
WHERE StudentNo = (
      SELECT `SubjectNo` FROM `subject`
      WHERE `SubjectName`='数据库结构-1'
)
ORDER BY StudentResult DESC


-- 2.查询课程为 高等数学-2 且 分数不小于80分的学生的学号和姓名
SELECT s.`StudentNo`,`StudentName`
FROM `student` s
INNER JOIN result r
ON r.StudentNo = s.StudentNo
INNER JOIN `subject` sub
ON sub.SubjectNo = r.SubjectNo
WHERE SubjectName = '高等数学-2' AND StudentResult >= 80


-- 分数不小于80分的学生的学号和姓名
SELECT DISTINCT s.`StudentNo`,`StudentName`
FROM `student` s
INNER JOIN result r
ON r.StudentNo = s.StudentNo
WHERE StudentResult >= 80

-- 在这个基础上增加科目  高等数学-2
-- 查询高等数学-2的编号
SELECT DISTINCT s.`StudentNo`,`StudentName`
FROM `student` s
INNER JOIN result r
ON r.StudentNo = s.StudentNo
WHERE StudentResult >= 80 AND `SubjectNo` = (
      SELECT `SubjectNo` FROM `subject`
      WHERE `SubjectName`='高等数学-2'
)

-- 再改造 (由里及外)
SELECT `StudentNo`,`StudentName` FROM student WHERE `StudentNo` IN (
    SELECT `StudentNo` FROM `result` WHERE `StudentResult`>=80 AND `SubjectNo` = (
        SELECT `SubjectNo` FROM `subject` WHERE `SubjectName`='高等数学-2'  
  )
) 
-- 子查询效率更高
```

```sql
-- 练习：查询 C语言-1 前五名学员的成绩信息（学号、姓名、分数）(不确保正确！欢迎指正)
SELECT s.`StudentNo`,`StudentName`,`StudentResult`
FROM student s
INNER JOIN result r
ON r.StudentNo = s.StudentNo
WHERE s.`StudentNo` IN (
    SELECT `StudentNo` FROM `result` WHERE `SubjectNo` = (
        SELECT `SubjectNo` FROM `subject` WHERE `SubjectName` = 'C语言-1'
    ) 
)
ORDER BY StudentResult DESC
LIMIT 0,5
```

### 过滤和分组

```sql
-- 查询不同课程的平均分、最高分、最低分
-- 核心：根据不同课程分组
SELECT `SubjectName`,AVG(StudentResult) AS 平均分,MAX(StudentResult),MIN(StudentResult)
FROM result r
INNER JOIN `subject` sub
ON r.`SubjectNo` = sub.`SubjectNo`
GROUP BY r.SubjectNo  -- 通过某个字段分组
HAVING 平均分 > 80  -- 过滤分组的记录必须满足的次要条件

```

## MySQL函数

**官网：https://dev.myql.com/doc/refman/5.7/en/func-op-summary-ref.heml**

### 常用函数

```sql
-- =========== 常用函数 =============

-- 数学运算
SELECT ABS(-8)  -- 绝对值
SELECT CEILING(9.4)  -- 向上取整
SELECT FLOOR(9.4)  -- 向下取整
SELECT RAND()  -- 返回一个0~1之间的随机数
SELECT SIGN(0)  -- 判断一个数的符号，正为1，负为-1

-- 字符串函数
SELECT CHAR_LENGTH('wafaw')  -- 字符串长度
SELECT CONCAT('w','a','n')  -- 拼接字符串
SELECT INSERT('www',1,2,'ss') -- 替换，从第一个开始，长度为2，结果是ssw
SELECT LOWER('KAF')  -- 转小写
SELECT UPPER('ajgfko') -- 转大写
SELECT INSTR('sucker','ke') -- 返回第一次出现的子串的索引，结果为4
SELECT REPLACE('坚持就能成功','就能','不一定能')  -- 替换出现的指定字符串
SELECT SUBSTR('坚持就能成功',4,3)  -- 返回指定的子字符串，从4号开始截取3个
SELECT REVERSE('坚持就能成功')  -- 反转

-- 查询姓周的同学  名字 邹
SELECT REPLACE(studentName,'周','邹') FROM student
WHERE StudentName LIKE '周%'

-- 时间和日期函数  （记住）
SELECT CURRENT_DATE()  -- 获取当前日期
SELECT CURDATE()  -- 获取当前日期
SELECT NOW()  -- 获取当前时间
SELECT LOCALTIME()  -- 获取本地时间
SELECT SYSDATE()  -- 系统时间

SELECT YEAR(NOW())
SELECT MONTH(NOW())
SELECT DAY(NOW())
SELECT HOUR(NOW())
SELECT MINUTE(NOW())
SELECT SECOND(NOW())

-- 系统
SELECT SYSTEM_USER()
SELECT USER()
SELECT VERSION() -- 版本号
```

### 聚合函数（常用）

| 函数名      | 描述   |
| ----------- | ------ |
| **COUNT()** | 计数   |
| SUM()       | 求和   |
| AVG         | 平均值 |
| MAX()       | 最大值 |
| MIN()       | 最小值 |
| ...         |        |

```sql
-- ========== 聚合函数 ===========
-- 都能够统计 表中数据
SELECT COUNT(studentname) FROM student  -- Count(字段)，会忽略所有null，字段为主键时效率最高
SELECT COUNT(*) FROM student -- Count(*) 不会忽略null 本质计算行数
SELECT COUNT(1) FROM result -- Count(1)  不会忽略null 本质计算行数

SELECT SUM(studentresult) AS 总和 FROM result
SELECT AVG(studentresult) AS 平均分 FROM result
SELECT MAX(studentresult) AS 最高分 FROM result
SELECT SIN(studentresult) AS 最低分 FROM result
```

### 数据库级别的MD5加密（拓展）

1. MD5主要增强算法复杂度和不可逆性
2. MD5不可逆，具体的值的MD5是一样的
3. MD5破解网站的原理：背后有一个字典

```sql
-- ======= 测试MD5 ========

CREATE TABLE `testmd5`(
    `id` INT(4) NOT NULL,
    `name` VARCHAR(20) NOT NULL,
    `pwd` VARCHAR(50) NOT NULL,
    PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 明文密码
INSERT INTO testmd5 VALUES(1,'zhangsan','123456'),
(2,'lisi','123456'),
(3,'wangwu','123456');

-- 加密
UPDATE testmd5 SET pwd=MD5(pwd) WHERE id=4

UPDATE testmd5 SET pwd=MD5(pwd) -- 加密全部密码

-- 插入时加密
INSERT INTO testmd5 VALUES(4,'zhangsan',MD5(123456))

-- 如何校验：将用户传递进来的密码，进行md5加密，然后比对加密后的值
SELECT * FROM `testmd5` WHERE `name`='zhangsan' AND pwd=MD5(123456)
-- 第一次加密后比对可以成功，再次加密后比对不能成功

```

## 事务

### 什么是事务

1. 要么都成功，要么都失败
2. 将一组SQL放在一个批次中去执行
3. 参考链接：[(14条消息) 事务ACID理解_dengjili的专栏-CSDN博客_acid](https://blog.csdn.net/dengjili/article/details/82468576)
4. **事务原则：ACID 原则  原子性，一致性，隔离性，持久性  （脏读、幻读...）**
   - **原子性（Atomicity）**：要么都成功，要么都失败
   - **一致性（Consistency）**：事务前后的数据完整性要保证一致：例如转账，前后总量不变
   - **隔离性（Isolation）**：事务的隔离性是多个用户并发访问数据库时，数据库为每一个用户开启的事务，不能被其他事务的操作数据所干扰，多个并发事务之间要相互隔离。
   - **持久性（Durability）**：事务一旦提交后就不可逆，被持久化到数据库中！
5. 隔离所导致的一些问题
   - **脏读**：指一个事务读取了另外一个事务未提交的数据。
   - **不可重复读**：在一个事务内读取表中的某一行数据，多次读取结果不同。（这个不一定是错误，只是某些场合不对）
   - **虚读（幻读）**：是指在一个事务内读取到了别的事务插入的数据，导致前后读取数量总量不一致。一般是行影响

### 测试事务

```sql
-- ======== 事务 =========

-- mysql是默认开启事务自动提交的
SET autocommit = 0 /* 关闭 */
SET autocommit = 1 /* 开启 */

-- 手动处理事务
SET autocommit = 0 -- 关闭自动提交

-- 事务开启
START TRANSACTION  -- 标记一个事务的开启，从这个之后的sql都在同一个事务内

INSERT xx
INSERT xx

-- 提交：持久化（成功！）
COMMIT
-- 回滚：回到原来的样子（失败！）
ROLLBACK

-- 事务结束
SET autocommit = 1 -- 开启自动提交

-- 了解
SAVEPOINT 保存点名 -- 设置一个事务的保存点
ROLLBACK TO SAVEPOINT 保存点名  -- 回滚到保存点
RELEASE SAVEPOINT 保存点名 -- 撤销保存点
```

### 模拟事务场景

```sql
-- 转账
CREATE DATABASE shop CHARACTER SET utf8 COLLATE utf8_general_ci;
USE shop

CREATE TABLE `acount`(
    `id` INT(3) NOT NULL AUTO_INCREMENT,
    `name` VARCHAR(30) NOT NULL,
    `money` DECIMAL(9,2) NOT NULL,
    PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO `acount`(`name`,`money`)
VALUES('A',2000.00),('B',10000.00)

-- 模拟转账 ：事务
SET autocommit = 0; -- 关闭自动提交
START TRANSACTION -- 开启一个事务（一组事务）

UPDATE acount SET money=money-500 WHERE `name`='A'  -- A-500
UPDATE acount SET money=money+500 WHERE `name`='B'  -- B+500

COMMIT; -- 提交事务,提交后数据持久化，回滚无效
ROLLBACK; -- 回滚

SET autocommit = 1; -- 开启自动提交
```

## 索引

### 索引的本质

MySQL官方对索引的定义为：**索引（Index）是帮助MySQL高效获取数据的数据结构。**

提取句子主干，就可以得到索引的本质：索引是数据结构。

### 索引的分类

- 主键索引 （PRIMARY KEY）
  - 唯一的标识，主键不可重复，只能有一个列作为主键
- 唯一索引 （UNIQUE KEY）
  - 避免一列中出现重复的行数据，唯一索引可以重复，多个列都可以标识为唯一索引
- 常规索引 （KEY / INDEX）
  - 默认的。index或key关键字设置
- 全文索引 （FullText）
  - 在特定的数据库引擎下才有，MyISM
  - 快速定位数据

### 索引的使用

```sql
-- 索引的使用
-- 1. 在创建表的时候给字段增加索引
-- 2. 创建完毕后，增加索引

-- 显示所有的索引信息
SHOW INDEX FROM student

-- 增加一个全文索引  索引名  （列名）
ALTER TABLE `student` ADD FULLTEXT INDEX `StudentName`(`StudentName`) 

-- id _ 表名 _ 字段名
-- CREATE INDEX 索引名 on 表（字段）
CREATE INDEX id_app_user_name ON app_user(`name`)

-- EXPLAIN 分析sql执行的状况

EXPLAIN SELECT * FROM student; -- 非全文索引

EXPLAIN SELECT * FROM student WHERE MATCH(StudentName) AGAINST('刘')
```

### 测试索引

```sql
CREATE TABLE `app_user` (
  `id` BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(50) DEFAULT '' COMMENT '用户昵称',
  `email` VARCHAR(50) NOT NULL COMMENT '用户邮箱',
  `phone` VARCHAR(20) DEFAULT '' COMMENT '手机号',
  `gender` TINYINT(4) UNSIGNED DEFAULT '0' COMMENT '性别（0：男;1:女）',
  `password` VARCHAR(100) NOT NULL COMMENT '密码',
  `age` TINYINT(4) DEFAULT '0' COMMENT '年龄',
  `create_time` DATETIME DEFAULT CURRENT_TIMESTAMP,
  `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8mb4 COMMENT = 'app用户表'

-- 插入100万数据  33.496 sec
delimiter $$  -- 写函数之前必写，标志
create function mock_data()
returns int
begin
   declare num int default 1000000;
   declare i int default 0;
   while i<num do
	-- 插入语句
      insert into `app_user`(`name`,`email`,`phone`,`gender`,`password`,`age`)
      values(concat('用户',i),'123456@qq.com',
      concat('18',floor(rand()*((999999999-100000000)+100000000))),
      floor(rand()*2),uuid(),floor(rand()*100));
      set i=i+1;
   end while;
   return i;
end;
select mock_data();

select * from `app_user` where `name` = '用户9999'; -- 0.492 sec
SELECT * FROM `app_user` WHERE `name` = '用户9999'; -- 0.398 sec
c -- 0.447 sec

explain SELECT * FROM `app_user` WHERE `name` = '用户9999';

-- id _ 表名 _ 字段名
-- CREATE INDEX 索引名 on 表（字段）
create index id_app_user_name on app_user(`name`)

SELECT * FROM `app_user` WHERE `name` = '用户9999'; -- 0.002 sec

EXPLAIN SELECT * FROM `app_user` WHERE `name` = '用户9999';  -- rows = 1
```

索引在小数据量时区别不大，在大数据量的时候，区别明显

### 索引原则

1. 索引不是越多越好
2. 不要对经常变动的数据加索引
3. 小数据量的表不需要加索引
4. 索引一般加在经常用于查询的字段上！

**索引的数据结构：**[CodingLabs - MySQL索引背后的数据结构及算法原理](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)

## 权限管理与备份

### 用户管理

1. SQLyog 可视化管理

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy91SkRBVUtyR0M3SmY3ZGVvbHdRYTQ0clh2aWNJaFhaME5HTDRzWktnOG5pY0JHcllsRUJKaDFWM3ltSjRXekJ4OXpYc0laeVBZRkFESkJ6bjBpYkNtZ2lhdUEvNjQw?x-oss-process=image/format,png)

注意：主机选择的是什么连接的时候就是什么

2. SQL命令操作

   用户表：mysql.user

   本质：对这张表进行增删改查

   ```sql
   -- 创建用户  create user 用户名 identified by '密码'
   CREATE USER Sucker IDENTIFIED BY '123456' -- 创建一个用户并定义密码
   
   -- 修改密码（修改当前用户密码）
   SET PASSWORD = PASSWORD('123456')
   
   -- 修改密码（修改指定用户密码）
   SET PASSWORD FOR Sucker = PASSWORD('111111')
   
   -- 重命名  rename user 原名 to 新名
   RENAME USER Sucker TO Sucker2
   
   -- 用户授权  all privileges  全部的权限 on  库.表
   -- ALL PRIVILEGES 除了给别人授权，其他都能干，可以在管理员界面将grant勾选上
   GRANT ALL PRIVILEGES ON *.* TO Sucker
   
   -- 查询权限
   SHOW GRANTS FOR Sucker  -- 查看指定用户的权限
   SHOW GRANTS FOR root@localhost
   
   -- 撤销权限 REVOKE 哪些权限 在哪个库撤销 给谁撤销
   REVOKE ALL PRIVILEGES ON *.* FROM Sucker
   
   -- 删除用户
   DROP USER Sucker
   ```

### MySQL备份

1. 备份原因：

   - 保证重要的数据不丢失
   - 数据转移

2. MySQL数据库备份的方式

   - 直接拷贝物理文件

   - 在SQLyog这种可视化工具中手动导出

     - 在想要导出的表或库中右键备份或导出，选择SQL转储

   - 使用命令行  mysqldump

     ```sql
     -- mysqldump -h主机 -u用户名 -p密码  数据库 表名 > 物理磁盘位置/文件名
     mysqldump -hlocalhost -uroot -p123456 school student >D:/a.sql
     
     -- mysqldump -h主机 -u用户名 -p密码  数据库 表1 表2 表3 > 物理磁盘位置/文件名
     mysqldump -hlocalhost -uroot -p123456 school student result >D:/a.sql
     
     -- mysqldump -h主机 -u用户名 -p密码  数据库 > 物理磁盘位置/文件名
     mysqldump -hlocalhost -uroot -p123456 school >D:/a.sql
     
     -- 导入
     -- 登录的情况下，切换到指定的数据库
     -- source 备份文件
     source D:/a.sql
     
     -- 未登录
     mysql -u用户名 -p密码 数据库名 <文件路径
     ```

## 规范数据库设计

### 设计原因

当数据库比较复杂时，需要设计

**糟糕的数据库设计：**

- 数据冗余，浪费空间
- 数据库插入和删除都会麻烦、异常【物理外键】
- 程序性能差

**良好的数据库设计：**

- 节省内存空间
- 保证数据库完整性
- 方便开发系统

**软件开发中，关于数据库的设计**

- 分析需求：分析业务和需要处理的数据库需求
- 概要设计：设计关系图 E-R图

**设计数据库的步骤：（个人博客）**

- 收集信息，分析需求
  - 用户表（用户登录注销，用户的个人信息，写博客，创建分类）
  - 分类表（文章分类，谁创建的）
  - 文章表（文章的信息）
  - 评论表
  - 友链表（友链信息）
  - 自定义表（系统信息，某个关键的字，或者一些主字段）
- 标识实体（把需求落地到每个字段）
- 标识实体之间的关系
  - 写博客：user -> blog
  - 创建分类：user -> category
  - 关注：user -> user
  - 友链：links
  - 评论：user -> user -> blog

### 三大范式

**数据规范化的原因**

- 信息重复
- 更新异常
- 插入异常
  - 无法正常显示信息
- 删除异常
  - 丢失有效的信息

**三大范式**

参考博客：

1. 第一范式（1NF）

   - **原子性：保证每一列不可再分**
     - 例如学校信息列内不能分为硕士，研二或本科，大二

2. 第二范式（2NF）

   - 前提：满足第一范式
   - **第二范式需要确保数据库的每一列都与主键相关，而不能只与其部分相关（主要针对联合主键）**
     - 例如联合主键：同一个订单可能包含不同产品，所以订单号和产品号为联合主键，而产品数量、产品折扣、产品价格都和`订单号`与`产品号`有关，但是订单金额和订单时间只与订单号有关，违反第二范式

3. 第三范式（3NF）

   - 前提：满足第一范式和第二范式

   - **第三范式需要确保数据表中的每一列数据都和主键直接相关，而不能间接相关。**

     ![](https://images2018.cnblogs.com/blog/1218459/201809/1218459-20180909211311408-1364899740.png)

     上表中，所有属性都完全依赖于学号，所以满足第二范式，但是“班主任性别”和“班主任年龄”直接依赖的是“班主任姓名”，

     而不是主键“学号”，所以需做如下调整：

     ![](https://images2018.cnblogs.com/blog/1218459/201809/1218459-20180909211539242-1391100354.png)

     ps:如果把上表中的班主任姓名改成班主任教工号可能更确切，更符合实际情况，不过只要能理解就行。

4. 规范性和性能的问题

   - 考虑商业化的需求和目标 （成本，用户体验）  数据库的性能更加重要
   - 在规范性能的问题时，要适当考虑 规范性！
   - 故意给某些表增加一些冗余字段  （从多表查询变为单表查询）
   - 故意增加一些计算列（从大数据量降低为小数据量的查询：索引）

## JDBC（重点）

### 数据库驱动

驱动：声卡、显卡、数据库

程序通过数据库驱动操作数据库

### JDBC

SUN 公司为了简化开发人员的（对数据库的统一）操作，提供了一个（Java操作数据库的）规范  俗称JDBC

这些操作的实现由具体厂商去做

对于开发人员来说，我们只需要掌握 JDBC 接口的操作即可！

java.sql

javax.sql

**还需要导入一个数据库驱动包   mysql-connector-java-5.1.47.jar **

### 第一个JDBC程序

`创建测试数据库`

```sql
CREATE DATABASE `jdbcStudy` CHARACTER SET utf8 COLLATE utf8_general_ci;

USE `jdbcStudy`;

CREATE TABLE `users`(
 `id` INT PRIMARY KEY,
 `NAME` VARCHAR(40),
 `PASSWORD` VARCHAR(40),
 `email` VARCHAR(60),
 birthday DATE
);

INSERT INTO `users`(`id`,`NAME`,`PASSWORD`,`email`,`birthday`)
VALUES(1,'zhangsan','123456','zs@sina.com','1980-12-04'),
(2,'lisi','123456','lisi@sina.com','1981-12-04'),
(3,'wangwu','123456','wangwu@sina.com','1979-12-04')
```

1. 创建一个普通项目（IDEA中）

2. 导入数据库驱动

   - new Directory名为lib

   - 将jar包复制进lib目录  mysql-connector-java-5.1.47

   - 右键add as library  点击ok

     ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210717150236.png)

3. 编写测试代码

   ```java
   package com.Sucker.lesson01;
   
   import javax.lang.model.element.NestingKind;
   import java.sql.*;
   
   //  第一个JDBC程序
   public class JdbcFirstDemo {
       public static void main(String[] args) throws ClassNotFoundException, SQLException {
           //1. 加载驱动
           Class.forName("com.mysql.jdbc.Driver");  //固定写法,加载驱动，注意抛出异常
   
           //2. 用户信息和url
           // useUnicode=true&characterEncoding=utf8&useSSL=true  设定支持中文编码，中文字符为utf8，使用安全的连接
           // 第一个参数使用？连接
           String url = "jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true";
           String username = "root";
           String password = "123456";
           //3. 连接成功，数据库对象   Connection 代表数据库
           Connection connection = DriverManager.getConnection(url, username, password);
   
           //4. 执行SQL对象  Statement 执行sql的对象
           Statement statement = connection.createStatement();
   
           //5. 执行SQL的对象  执行SQL  可能存在结果，查看返回结果
           String sql = "select * from `users`";
   
           ResultSet resultSet = statement.executeQuery(sql); // 返回的结果集,其中封装了查询出来的全部结果
   
           while(resultSet.next()){
               System.out.println("id="+resultSet.getObject("id"));
               System.out.println("name="+resultSet.getObject("NAME"));
               System.out.println("pwd="+resultSet.getObject("PASSWORD"));
               System.out.println("email="+resultSet.getObject("email"));
               System.out.println("birthday="+resultSet.getObject("birthday"));
           }
           //6. 释放连接
           resultSet.close();
           statement.close();
           connection.close();
       }
   }
   ```

4. 步骤总结

   - 加载驱动
   - 连接数据库 DriverManager
   - 获得执行sql的对象 Statement
   - 获得返回的结果集
   - 释放连接

> URL

```java
String url = "jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true";

//mysql -- 3306
//协议://主机地址：端口号/数据库名？参数1&参数2...
//oralce -- 1521
//jdbc:oralce:thin:@localhost:1521:sid 
```

> DriverManager

```java
Connection connection = DriverManager.getConnection(url, username, password);

//connection 代表数据库
//设置数据库自动提交
//事务提交
//事务回滚
connection.rollback();
connection.commit();
connection.setAutoCommit();
```

> Statement 执行SQL对象   PrepareStatement  执行SQL对象

```java
String sql = "select * from `users`"; // 编写sql

statement.executeQuery(); //查询操作返回 ResultSet
statement.execute();  //执行任何SQL
statement.executeUpdate();  //更新、插入、删除 都是用这个  返回一个受影响的行数
```

> ResultSte 查询的结果集：封装了所有的查询结果

```java
resultSet.getObject();  //在不知道类型的情况下使用
//知道列的类型使用指定类型
resultSet.getString();
resultSet.getInt();
resultSet.getFloat();
resultSet.getDate();
resultSet.getObject();
...
```

> 遍历，指针

```java
resultSet.beforeFirst(); //指针移动到最前面
resultSet.afterLast(); //移动到最后面
resultSet.next();  //移动到下一个
resultSet.previous(); //移动到前一行
resultSet.absolute(row); //移动到指定行
```

> 释放资源

```java
resultSet.close();
statement.close();
connection.close();//耗资源，用完关掉
```

### statement对象

**jdbc中的statement对象用于向数据库发送SQL语句，想完成对数据库的增删改查，只需要通过这个对象向数据库发送增删改查语句即可**

Statement对象的executeUpdate方法，用于向数据库发送增、删、改的sql语句，executeUpdate执行完后，将会返回一个整数（即增删改语句导致了数据库几行数据发生了变化）

Statement.executeQuery方法用于向数据库发送查询语句,executeQuery方法返回代表查询结果的ResultSet对象

> CRUD操作-create

使用executeUpdate(String sql)方法完成数据添加操作

```java
Statement st = conn.createStatement();
String sql = "insert into user(...) values(...)";
int num = se.executeUpdate(sql);
if(num>0){
    System.out.println("插入成功");
}
```

> CRUD操作-delete

使用executeUpdate(String sql)方法完成数据删除操作

```java
Statement st = conn.createStatement();
String sql = "delete from user where id=1";
int num = se.executeUpdate(sql);
if(num>0){
    System.out.println("成功");
}
```

> CRUD操作-update

```java
Statement st = conn.createStatement();
String sql = "update user set name = '' where name = '' ";
int num = se.executeUpdate(sql);
if(num>0){
    System.out.println("成功");
}
```

> CRUD操作-Retrieve

```java
Statement st = conn.createStatement();
String sql = "select * from user where id=1";
int num = se.executeQuery(sql);
if(num>0){
    System.out.println("成功");
}
```

代码实现

1. 提取工具类

   ```java
   //src目录下新建db.properties文件（File）
   
   driver=com.mysql.jdbc.Driver
   url=jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true
   username=root
   password=123456
   ```

   ```java
   //新建utils包，包内建立工具类
   
   package com.Sucker.lesson02.utils;
   
   import com.mysql.jdbc.Driver;
   
   import java.io.IOException;
   import java.io.InputStream;
   import java.sql.*;
   import java.util.Properties;
   
   public class jdbcUtils {
       private static String driver = null;
       private static String url = null;
       private static String username = null;
       private static String password = null;
   
       static{
   
           try{
               InputStream in = jdbcUtils.class.getClassLoader().getResourceAsStream("db.properties");
               Properties properties = new Properties();
               properties.load(in);
   
               driver = properties.getProperty("driver");
               url = properties.getProperty("url");
               username = properties.getProperty("username");
               password = properties.getProperty("password");
   
               //1.驱动加载，只用加载一次
               Class.forName(driver);
   
           } catch (Exception e) {
               e.printStackTrace();
           }
       }
   
       //获取连接
       public static Connection getConnection() throws SQLException {
           return DriverManager.getConnection(url,username,password);
       }
       //释放资源
       public static void release(Connection conn, Statement st, ResultSet rs){
           if(rs!=null){
               try {
                   rs.close();
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
           if(st!=null){
               try {
                   st.close();
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
           if(conn!=null){
               try {
                   conn.close();
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
   
       }
   }
   ```

2. 增删改代码实现

   ```java
   package com.Sucker.lesson02;
   
   import com.Sucker.lesson02.utils.jdbcUtils;
   
   import java.sql.Connection;
   import java.sql.ResultSet;
   import java.sql.SQLException;
   import java.sql.Statement;
   
   public class TestUpdate {
       public static void main(String[] args) {
   
           Connection conn = null;
           Statement st = null;
           ResultSet rs = null;
   
           try {
               conn = jdbcUtils.getConnection();  //获取数据库连接
               st = conn.createStatement();  //获得SQL的执行对象
               String sql = "UPDATE users SET `NAME` = 'sucker',`email` = 'safa@qq.com' WHERE id = 1";
               int i = st.executeUpdate(sql);
               if(i>0){
                   System.out.println("successful");
               }
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           }finally {
               jdbcUtils.release(conn,st,rs);
           }
       }
   }
   ```

   增删替换sql即可，可先在sqlyog中编写完成

3. 查询代码实现（executeQuery）

   ```java
   package com.Sucker.lesson02;
   
   import com.Sucker.lesson02.utils.jdbcUtils;
   
   import java.sql.Connection;
   import java.sql.ResultSet;
   import java.sql.SQLException;
   import java.sql.Statement;
   
   public class TestSelect {
       public static void main(String[] args) {
   
           Connection conn = null;
           Statement st = null;
           ResultSet rs = null;
   
           try {
               conn = jdbcUtils.getConnection();
               st = conn.createStatement();
   
               //SQL
               String sql = "select * from users where id = 1";
   
               rs = st.executeQuery(sql); //推荐使用Query查询
   
               while(rs.next()){
                   System.out.println(rs.getString("NAME"));
               }
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           }finally {
               jdbcUtils.release(conn,st,rs);
           }
       }
   }
   ```

   > SQL注入的问题

   sql存在漏洞，会被攻击导致数据泄露  ==SQL会被凭借 or==

   ```sql
   package com.Sucker.lesson02;
   
   import com.Sucker.lesson02.utils.jdbcUtils;
   
   import java.sql.Connection;
   import java.sql.ResultSet;
   import java.sql.SQLException;
   import java.sql.Statement;
   
   public class SQL注入 {
       public static void main(String[] args) {
           // 正常登录：login("sucker","123456");
           login(" 'or '1=1","'or'1=1");
       }
   
       //登录业务
       public static void login(String username,String password){
   
           Connection conn = null;
           Statement st = null;
           ResultSet rs = null;
   
           try {
               conn = jdbcUtils.getConnection();
               st = conn.createStatement();
   
               // SELECT * FROM users WHERE `NAME` = 'sucker' AND `password` = '123456';
               // SELECT * FROM users WHERE `NAME` = '' or '1=1' AND `password` = ''or'1=1';
               String sql = "select * from users where `NAME` = '"+username+"' and `password` = '"+password+"'";
   
               rs = st.executeQuery(sql); //推荐使用Query查询
   
               while(rs.next()){
                   System.out.println(rs.getString("NAME"));
                   System.out.println(rs.getString("password"));
               }
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           }finally {
               jdbcUtils.release(conn,st,rs);
           }
       }
   }
   ```

### PreparedStatement对象

本质区别：可以防止SQL注入。效率更高

1. 新增

   ```java
   package com.Sucker.lesson03;
   
   import com.Sucker.lesson02.utils.jdbcUtils;
   
   import javax.lang.model.element.NestingKind;
   import java.sql.Connection;
   import java.util.Date;
   import java.sql.PreparedStatement;
   import java.sql.SQLException;
   
   public class TestInsert {
       public static void main(String[] args) {
           Connection conn = null;
           PreparedStatement pst = null;
   
           try {
               conn = jdbcUtils.getConnection();
   
               //区别
               //?是占位符代替参数
               String sql = "INSERT INTO `users`(`id`,`NAME`,`PASSWORD`,`email`,`birthday`) values(?,?,?,?,?)";
   
               pst = conn.prepareStatement(sql);//需要参数 预编译SQL，先写sql，不执行
   
               //手动给参数赋值
               pst.setInt(1,4);  //对id，从第1个参数开始赋值
               pst.setString(2,"Scuker");
               pst.setString(3,"123123");
               pst.setString(4,"23243@qq.com");
               // 注意点：  sql.Date  数据库
               //          util.Date   Java       new Date().getTime()  获得时间戳
               pst.setDate(5,new java.sql.Date(new Date().getTime()));
   
               //执行
               int i = pst.executeUpdate();
               if(i>0){
                   System.out.println("successful");
               }
   
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           } finally {
               jdbcUtils.release(conn,pst,null);
           }
       }
   }
   ```

2. 删除

   ```java
   package com.Sucker.lesson03;
   
   import com.Sucker.lesson02.utils.jdbcUtils;
   
   import java.sql.Connection;
   import java.sql.PreparedStatement;
   import java.sql.SQLException;
   import java.util.Date;
   
   public class TeseDelete {
       public static void main(String[] args) {
           Connection conn = null;
           PreparedStatement pst = null;
   
           try {
               conn = jdbcUtils.getConnection();
   
               //区别
               //?是占位符代替参数
               String sql = "delete from users where id = ?";
   
               pst = conn.prepareStatement(sql);//需要参数 预编译SQL，先写sql，不执行
   
               //手动给参数赋值
               pst.setInt(1,4);
   
               //执行
               int i = pst.executeUpdate();
               if(i>0){
                   System.out.println("successful");
               }
   
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           } finally {
               jdbcUtils.release(conn,pst,null);
           }
       }
   }
   
   ```

3. 更新

   ```java
   package com.Sucker.lesson03;
   
   import com.Sucker.lesson02.utils.jdbcUtils;
   
   import java.sql.Connection;
   import java.sql.PreparedStatement;
   import java.sql.SQLException;
   
   public class TestUpdate {
       public static void main(String[] args) {
           Connection conn = null;
           PreparedStatement pst = null;
   
           try {
               conn = jdbcUtils.getConnection();
   
               //区别
               //?是占位符代替参数
               String sql = "update users set `NAME`=? where id = ?;";
   
               pst = conn.prepareStatement(sql);//需要参数 预编译SQL，先写sql，不执行
   
               //手动给参数赋值
               pst.setString(1,"苏科");
               pst.setInt(2,1);
   
               //执行
               int i = pst.executeUpdate();
               if(i>0){
                   System.out.println("successful");
               }
   
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           } finally {
               jdbcUtils.release(conn,pst,null);
           }
       }
   }
   ```

4. 查询

   ```java
   package com.Sucker.lesson03;
   
   import com.Sucker.lesson02.utils.jdbcUtils;
   
   import java.sql.Connection;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.SQLException;
   
   public class TestSelect {
       public static void main(String[] args) {
           Connection conn=null;
           PreparedStatement pst = null;
           ResultSet rs = null;
   
           try {
               conn = jdbcUtils.getConnection();
   
               String sql = "select * from users where id = ?";
   
               pst = conn.prepareStatement(sql);
   
               pst.setInt(1,1); //传递参数
   
               //执行
               rs = pst.executeQuery();
   
               if(rs.next()){
                   System.out.println(rs.getString("NAME"));
               }
   
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           } finally {
               jdbcUtils.release(conn,pst,rs);
           }
       }
   }
   ```

### 使用IDEA连接数据库

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210717205607.png)

连接时注意Drivers目录要选择lib目录下的jar包，注意MySQL的版本

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210717211437.png)

更新数据需要Submit

编写SQL

![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210717212005.png)

### JDBC操作事务

要么都成功，要么都失败

> ACID原则

原子性：要么全部完成，要么都不完成

一致性：总数不变

隔离性：多个进程互不干扰

持久性：一旦提交不可逆，持久化到数据库

隔离所导致的一些问题

- **脏读**：指一个事务读取了另外一个事务未提交的数据。
- **不可重复读**：在一个事务内读取表中的某一行数据，多次读取结果不同。（这个不一定是错误，只是某些场合不对）
- **虚读（幻读）**：是指在一个事务内读取到了别的事务插入的数据，导致前后读取数量总量不一致。一般是行影响

> 代码实现

 1. 开启事务 conn.setAutoCommit(false);//开启事务

 2. 一组业务执行完毕，提交事务

 3. 可以在catch语句中显式的定义 回滚语句 ，但默认失败就会回滚

    ```java
    package com.Sucker.lesson04;
    
    import com.Sucker.lesson02.utils.jdbcUtils;
    
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    
    public class TestTransaction {
        public static void main(String[] args) {
            Connection conn = null;
            PreparedStatement pst = null;
            ResultSet rs = null;
    
            try {
                conn = jdbcUtils.getConnection();
                //关闭数据库的自动提交功能,自动会开启事务
                conn.setAutoCommit(false);//开启事务
    
                String sql1 = "update account set money = money-100 where name = 'A'";
                pst = conn.prepareStatement(sql1);
                pst.executeUpdate();
    
                String sql2 = "update account set money = money+100 where name = 'B'";
                pst = conn.prepareStatement(sql2);
                pst.executeUpdate();
    
                //业务完毕，提交事务
                conn.commit();
                System.out.println("successful");
    
            } catch (SQLException throwables) {
                //如果失败，会默认回滚，就算不写下面语句也行
                try {
                    conn.rollback();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
                throwables.printStackTrace();
            } finally {
                jdbcUtils.release(conn,pst,rs);
            }
        }
    }
    ```

### 数据库连接池

数据库连接 --- 执行完毕 --- 释放

连接 --- 释放  十分浪费系统资源

**池化技术：预先准备一些资源，直接连接预先准备好的资源**

编写连接池，实现一个接口  DataSource

> 开源数据源实现

​	DBCP

​	C3P0

​	Druid：阿里巴巴

使用了这些数据库连接池后，我们在项目开发中就不需要编写连接数据库的代码

> DBCP

需要用到的 jar 包

commons-dbcp-1.4   commons-pool-1.6 导入进lib内

代码实现

1. 首先建立dbcpconfig.properties文件，同上statement对象中，建立在src目录下

```java
#连接设置
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true
username=root
password=123456

#!-- 初始化连接 --
initialSize=10

#最大连接数量
maxActive=50

#!-- 最大空闲连接 --
maxIdle=20

#!-- 最小空闲连接 --
minIdle=5

#!-- 超时等待时间以毫秒为单位 6000毫秒/1000等于60秒 --
maxWait=60000

#JDBC驱动建立连接时附带的连接属性属性的格式必须为这样：【属性名=property;】
#注意：user 与 password 两个属性会被明确地传递，因此这里不需要包含他们。
connectionProperties=useUnicode=true;characterEncoding=utf8

#指定由连接池所创建的连接的自动提交（auto-commit）状态。
defaultAutoCommit=true

#driver default 指定由连接池所创建的连接的只读（read-only）状态。
#如果没有设置该值，则“setReadOnly”方法将不被调用。（某些驱动并不支持只读模式，如：Informix）
defaultReadOnly=

#driver default 指定由连接池所创建的连接的事务级别（TransactionIsolation）。
#可用值为下列之一：（详情可见javadoc。）NONE,READ_UNCOMMITTED, READ_COMMITTED, REPEATABLE_READ, SERIALIZABLE
defaultTransactionIsolation=READ_COMMITTED
```

2. 建立utils包，建立工具类

   ```java
   package com.Sucker.lesson05.utils;
   
   import com.Sucker.lesson02.utils.jdbcUtils;
   import org.apache.commons.dbcp.BasicDataSource;
   import org.apache.commons.dbcp.BasicDataSourceFactory;
   
   import javax.sql.DataSource;
   import java.io.InputStream;
   import java.sql.*;
   import java.util.Properties;
   
   public class JdbcUtils_DBCP {
   
       private static DataSource dataSource = null;
   
       static{
           try{
               InputStream in = JdbcUtils_DBCP.class.getClassLoader().getResourceAsStream("dbcpconfig.properties");
               Properties properties = new Properties();
               properties.load(in);
   
               //创建数据源  工厂模式 ---> 创建
               dataSource = BasicDataSourceFactory.createDataSource(properties);
   
           } catch (Exception e) {
               e.printStackTrace();
           }
       }
   
       //获取连接
       public static Connection getConnection() throws SQLException {
           return dataSource.getConnection(); // 从数据源中获取连接
       }
       //释放资源
       public static void release(Connection conn, Statement st, ResultSet rs){
           if(rs!=null){
               try {
                   rs.close();
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
           if(st!=null){
               try {
                   st.close();
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
           if(conn!=null){
               try {
                   conn.close();
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
   
       }
   }
   ```

   ![](https://gitee.com/sucker-s/cloudimages/raw/master/img/20210717231640.png)

   3. 测试代码

   ```java
   package com.Sucker.lesson05;
   
   import com.Sucker.lesson02.utils.jdbcUtils;
   import com.Sucker.lesson05.utils.JdbcUtils_DBCP;
   
   import java.sql.Connection;
   import java.sql.PreparedStatement;
   import java.sql.SQLException;
   import java.util.Date;
   
   public class TestDBCP {
       public static void main(String[] args) {
           Connection conn = null;
           PreparedStatement pst = null;
   
           try {
               conn = JdbcUtils_DBCP.getConnection();
   
               //区别
               //?是占位符代替参数
               String sql = "INSERT INTO `users`(`id`,`NAME`,`PASSWORD`,`email`,`birthday`) values(?,?,?,?,?)";
   
               pst = conn.prepareStatement(sql);//需要参数 预编译SQL，先写sql，不执行
   
               //手动给参数赋值
               pst.setInt(1,4);  //对id，从第1个参数开始赋值
               pst.setString(2,"Scuker");
               pst.setString(3,"123123");
               pst.setString(4,"23243@qq.com");
               // 注意点：  sql.Date  数据库
               //          util.Date   Java       new Date().getTime()  获得时间戳
               pst.setDate(5,new java.sql.Date(new Date().getTime()));
   
               //执行
               int i = pst.executeUpdate();
               if(i>0){
                   System.out.println("successful");
               }
   
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           } finally {
               JdbcUtils_DBCP.release(conn,pst,null);
           }
       }
   }
   ```

   连接池可以省略一些步骤

> C3P0

需要用到的jar包

c3p0-0.9.5.5   mchange-commons-java-0.2.19   导入进lib内

代码实现

1. 首先建立 c3p0-config.xml 文件，同上statement对象中，建立在src目录下

   ```java
   <?xml version="1.0" encoding="UTF-8"?>
   <c3p0-config>
       <!--
       c3p0的缺省（默认）配置,
       如果在代码中"ComboPooledDataSource ds = new ComboPooledDataSource();这样写就表示使用的是c3p0的缺省（默认）-->
       <default-config>
           <property name="driverClass">com.mysql.jdbc.Driver</property>
           <property name="jdbcUrl">jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&amp;characterEncoding=utf8&amp;uesSSL=true&amp;</property>
           <property name="user">root</property>
           <property name="password">123456</property>
   
           <property name="acquireIncrement">5</property>
           <property name="initialPoolSize">10</property>
           <property name="minPoolSize">5</property>
           <property name="maxPoolSize">20</property>
       </default-config>
   
       <!--
       c3p0的命名配置
       如果在代码中ComboPooledDataSource ds=new ComboPooledDataSource("MySQL");这样写就表示使用的是MySQL的缺省（默认）-->
       <name-config name="MySQL">
           <property name="driverClass">com.mysql.jdbc.Driver</property>
           <property name="jdbcUrl">jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&amp;characterEncoding=utf8&amp;uesSSL=true&amp;</property>
           <property name="user">root</property>
           <property name="password">123456</property>
   
           <property name="acquireIncrement">5</property>
           <property name="initialPoolSize">10</property>
           <property name="minPoolSize">5</property>
           <property name="maxPoolSize">20</property>
       </name-config>
   
   </c3p0-config>
   ```

2. 建立utils包，建立工具类

   ```java
   package com.Sucker.lesson05.utils;
   
   import com.mchange.v2.c3p0.ComboPooledDataSource;
   import org.apache.commons.dbcp.BasicDataSourceFactory;
   
   import javax.sql.DataSource;
   import java.io.InputStream;
   import java.sql.Connection;
   import java.sql.ResultSet;
   import java.sql.SQLException;
   import java.sql.Statement;
   import java.util.Properties;
   
   public class JdbcUtils_C3P0 {
   
       private static ComboPooledDataSource dataSource = null;
   
       static{
           try{
               //代码版配置
   //            dataSource = new ComboPooledDataSource();
   //            dataSource.setDriverClass();
   //            dataSource.setUser();
   //            dataSource.setPassword();
   //            dataSource.setJdbcUrl();
   //
   //            dataSource.setMaxPoolSize();
   //            dataSource.setMinPoolSize();
   
               //创建数据源  工厂模式 ---> 创建
               dataSource = new ComboPooledDataSource("MySQL");//配置文件写法，不写参数为默认c3p0配置
   
           } catch (Exception e) {
               e.printStackTrace();
           }
       }
   
       //获取连接
       public static Connection getConnection() throws SQLException {
           return dataSource.getConnection(); // 从数据源中获取连接
       }
       //释放资源
       public static void release(Connection conn, Statement st, ResultSet rs){
           if(rs!=null){
               try {
                   rs.close();
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
           if(st!=null){
               try {
                   st.close();
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
           if(conn!=null){
               try {
                   conn.close();
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
   
       }
   }
   ```

3. 测试代码

   ```java
   package com.Sucker.lesson05;
   
   import com.Sucker.lesson05.utils.JdbcUtils_C3P0;
   import com.Sucker.lesson05.utils.JdbcUtils_DBCP;
   
   import java.sql.Connection;
   import java.sql.PreparedStatement;
   import java.sql.SQLException;
   import java.util.Date;
   
   public class TestC3P0 {
       public static void main(String[] args) {
           Connection conn = null;
           PreparedStatement pst = null;
   
           try {
               conn = JdbcUtils_C3P0.getConnection();//原本自己实现，现在用别人的
   
               //区别
               //?是占位符代替参数
               String sql = "INSERT INTO `users`(`id`,`NAME`,`PASSWORD`,`email`,`birthday`) values(?,?,?,?,?)";
   
               pst = conn.prepareStatement(sql);//需要参数 预编译SQL，先写sql，不执行
   
               //手动给参数赋值
               pst.setInt(1,5);  //对id，从第1个参数开始赋值
               pst.setString(2,"Scuker");
               pst.setString(3,"123123");
               pst.setString(4,"23243@qq.com");
               // 注意点：  sql.Date  数据库
               //          util.Date   Java       new Date().getTime()  获得时间戳
               pst.setDate(5,new java.sql.Date(new Date().getTime()));
   
               //执行
               int i = pst.executeUpdate();
               if(i>0){
                   System.out.println("successful");
               }
   
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           } finally {
               JdbcUtils_C3P0.release(conn,pst,null);
           }
       }
   }
   ```

> 总结

​	无论使用什么数据源，本质还是一样的，DataSource接口不会变，方法就不会变

**tips：一对多的表，建表时一般在多的那个表来个字段作为外键，多对多建表是针对两个表建立第三张表来表示两者关系**