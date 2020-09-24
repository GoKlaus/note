[TOC]





### CURD

创建（Create）、更新（Update）、读取（Retrieve）和删除（Delete）

### Like

四种匹配方式

`%`-0个或者多个字符，有些情况若是中文，使用两个%%来表示

`_`-表示任意单个字符

`[]`-表示任意在括号的内的字符

`[^]`-表示不再任意括号所列字段之内的单个字符

## 索引

### 概念

```
索引是一种特殊的文件(InnoDB数据表上的索引是表空间的一个组成部分)，它们包含着对数据表里所有记录的引用指针。更通俗的说，数据库索引好比是一本书前面的目录，能加快数据库的查询速度。
```

### 类型

### 单列索引

#### 普通索引 INDEX

MySQL中基本索引类型，没有什么限制，允许在定义索引的列中插入重复值和空值，纯粹为了查询数据更快一点

如何建立

```sql
--建表语句
CREATE TABLE `sys_area`
(    `id`             bigint(20)  NOT NULL,
    `name`           varchar(50) NOT NULL COMMENT '区域名',
    `parent_id`      bigint(20)  NULL COMMENT '上级区域id',
    `org_id`         bigint(20)  NOT NULL COMMENT '组织id',
    `create_user_id` bigint(20)  NOT NULL COMMENT '创建者id',
    `gmt_create`     timestamp   NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `gmt_modified`   timestamp   NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
    `remark`         varchar(40) NOT NULL DEFAULT '' COMMENT '备注',
    `status`         tinyint(2)  NOT NULL DEFAULT 1 COMMENT '状态  0：禁用   1：正常',
    PRIMARY KEY (`id`),
    INDEX `idx_org` (`org_id`),
    INDEX `name` (`name`),
    INDEX `idx_org_name_parent` (`parent_id`)
)ENGINE = InnoDB
 DEFAULT CHARACTER SET = utf8 COMMENT = '区域表';
```



#### 唯一索引 UNIQUE

索引列中的值必须是唯一的，但是允许为空值

如何建立

```sql

```



#### **主键索引， PRIMARY KEY**

是一种特殊的唯一索引，不允许有空值　　

如何建立

```sql

```



### 多列索引



### 全文索引 FULLTEXT

只有在MyISAM引擎上才能使用 (MySQL 5.6版本的InnoDB 开始支持全文索引)，只能在CHAR,VARCHAR,TEXT类型字段上使用全文索引，全文索引，就是在一堆文字中，通过其中的某个关键字等，就能找到该字段所属的记录行.



### 空间索引 SPATIAL

只有在MyISAM引擎上才能使用（MySQL 5.7版本的InnoDB 开始支持)**，**空间索引是对空间数据类型（坐标，地理位置等）的字段建立的索引，MySQL中的空间数据类型有四种，GEOMETRY、POINT、LINESTRING、POLYGON。**创建空间索引的列，必须将其声明为NOT NULL**





### 组合索引

在表中的多个字段组合上创建的索引，只有在查询条件中使用了这些字段的左边字段时，索引才会被使用，使用组合索引时遵循最左前缀集合





另外索引也可以分为聚集索引和非聚集索引：

聚集（clustered）索引

数据行的物理顺序与列值（一般是主键 的那一列）的逻辑顺序相同，一个表中只能拥有一个聚集索引。（即主键索引）

非聚集索引(辅助索引)

该索引中索引的逻辑顺序与磁盘上行的物理存储顺序不同，一个表中可以拥有多个非聚集索引。（包括普通索引，唯一索引，全文索引等）





### Btree索引中的最左匹配原则

Btree是按照从左到右的顺序来建立搜索树的。比如索引是(name,age,sex)，会先检查name字段，如果name字段相同再去检查后两个字段。

所以当传进来的是后两个字段的数据（age，sex），因为建立搜索树的时候是按照第一个字段建立的，所以必须根据name字段才能知道下一个字段去哪里查询。

所以传进来的是（name，sex）时，首先会根据name指定搜索方向，但是第二个字段缺失，所以将name字段正确的都找到后，然后才会去匹配sex的数据。

建立索引的规则： 

1、利用最左前缀：Mysql会一直向右查找直到遇到范围操作（>，<，like、between）就停止匹配。比如a=1 and b=2 and c>3 and d=6；此时如果建立了（a,b,c,d）索引，那么后面的d索引是完全没有用到，当换成了（a,b,d,c）就可以用到  c是范围查询。

2、不能过度索引：在修改表内容的时候，索引必须更新或者重构，所以索引过多时，会消耗更多的时间。

3、尽量扩展索引而不要新建索引

4、最适合的索引的列是出现在where子句中的列或连接子句中指定的列。

5、不同值较少的列不必要建立索引（性别）。



# 索引注意事项

1、如果条件中有or，即使其中有条件带索引也不会使用(这也是为什么尽量少用or的原因)

 注意：要想使用or，又想让索引生效，只能将or条件中的每个列都加上索引

2.对于多列索引，不是使用的第一部分，则不会使用索引（最左匹配原则）

3.like查询是以%开头，会全表扫描

4.如果列类型是字符串，那一定要在条件中将数据使用引号引用起来,否则不使用索引

5.如果mysql估计使用全表扫描要比使用索引快,则不使用索引

此外，查看索引的使用情况
show status like ‘Handler_read%';
大家可以注意：
handler_read_key:这个值越高越好，越高表示使用索引查询到的次数
handler_read_rnd_next:这个值越高，说明查询低效

1) 没有查询条件，或者查询条件没有建立索引 

2) 在查询条件上没有使用引导列 

3) 查询的数量是大表的大部分，应该是30％以上。 

4) 索引本身失效

5) 查询条件使用函数在索引列上，或者对索引列进行运算，运算包括(+，-，*，/，! 等) 错误的例子：select * from test where id-1=9; 正确的例子：select * from test where id=10; 

6) 对小表查询 

7) 提示不使用索引

8) 统计数据不真实 

9) CBO计算走索引花费过大的情况。其实也包含了上面的情况，这里指的是表占有的block要比索引小。 

10)隐式转换导致索引失效.这一点应当引起重视.也是开发中经常会犯的错误. 由于表的字段tu_mdn定义为varchar2(20),但在查询时把该字段作为number类型以where条件传给Oracle,这样会导致索引失效. 错误的例子：select * from test where tu_mdn=13333333333; 正确的例子：select * from test where tu_mdn='13333333333'; 

12) 1,<> 2,单独的>,<,(有时会用到，有时不会) 

13,like "%_" 百分号在前. 

14,表没分析. 

15,单独引用复合索引里非第一位置的索引列. 

16,字符型字段为数字时在where条件里不添加引号. 

17,对索引列进行运算.需要建立函数索引. 

18,not in ,not exist. 

19,当变量采用的是times变量，而表的字段采用的是date变量时或相反情况。 

20,B-tree索引 is null不会走,is not null会走，位图索引 is null,is not null 都会走 

21,联合索引 is not null 只要在建立的索引列（不分先后）都会走, in null时 必须要和建立索引第一列一起使用,当建立索引第一位置条件是is null 时,其他建立索引的列可以是is null（但必须在所有列 都满足is null的时候）,或者=一个值； 当建立索引的第一位置是=一个值时,其他索引列可以是任何情况（包括is null =一个值）,以上两种情况索引都会走。其他情况不会走。

在字段not null的情况下，is null和is not null都不会走索引

## 如何强制使用索引？

代码中使用

```sql
select * from oa_attend oa
FORCE index(i_oa_create_time)
where oa.create_time >= '2018-10-01 00:00:00' and oa.create_time<='2018-11-14 00:00:00';
 
select * from oa_attend oa 
FORCE index(i_oa_create_time)
where oa.create_time BETWEEN '2018-10-01 00:00:00' and '2018-11-14 00:00:00';
```

## KEY与INDEX 含义讲解

[MySql常见约束](https://www.cnblogs.com/fanqisoft/p/10697866.html)



约束：一种限制，用于限制表中数据，为了保证表中数据的准确性和可靠性

种类：

1. NOT NULL ：非空，用于保证字段非空
2. DEFAULT：默认值，用于保证字段的默认值
3. PRIMARY KEY：主键，用于保证该字段具有唯一性并且非空
4. UNIQUE：唯一，用于保证该字段的值具有唯一性
5. CHECK：检查约束（MYSQL不支持），检查字段的值是否为指定的值
6. FOREIGN KEY：外键，用于限制两个表的关系，用于保证该字段的值必须来自于主表的关联列的值，在从表添加外键约束，用于引用主表中某些值

如何添加约束：

1、列级约束（六大约束都支持，但是外键约束没有效果）

```sql
create table if not exists t_stuinfo(
    id int primary key,    #主键
    stuName varchar(20) not null,    #非空
    gender char(1) check(gender='男' or gender='女'),    #检查约束，MySql没有效果但不报错
    seat int unique,    #唯一约束
    age int default 18,    #默认（值）约束
    majorId int references major(id) #外键约束，MySql没有效果，但不报错
    );
```

2、表级约束（除了非空、默认，其他都支持）

语法 在创建字段语句下面

```sql
constraint 约束名 约束类型(字段名)
```



```sql
create table if not exists t_stuinfo(
    id int,
    stuName varchar(20),
    gender char(1),
    seat int,
    age int,
    majorId int,
    constraint pk primary key(id),    #约束名随意，主键不生效，但不报错。
    constraint uq unique(seat),    #唯一约束
    constraint ck check(gender='男' or gender='女'),    #检查约束，MySql不支持此约束，不报错但不生效
    constraint fk_stuinfo_major foreign key(majorId) references major(id)    #外键约束
    );
```

 主键和唯一的区别

| 约束名称 | 保证唯一性 | 是否允许为空 | 一个表中可以有多少个 | 是否允许组合 |
| -------- | ---------- | ------------ | -------------------- | ------------ |
| 主键     | √          | ×            | 最多有1个，可以没有  | √（不推荐）  |
| 唯一     | √          | √            | 可以有多个           | √（不推荐）  |

外键：

　　1.要求在从表中设置外键关系

　　2.从表的外键列的类型和主表的关联列的类型要求一致或兼容，名称无要求。

　　3.主表的关联列必须时一个Key（一般为主键或唯一，外键也可以但无意义）

　　4.插入数据时，先插入主表，再插入从表

　　  删除数据时，先删除从表，再删除主表

### 标识列

又为自增长列，可以不用手动的插入值，系统提供默认的序列值

特点：

1. 标识列必须和一个Key搭配（Key指主键、唯一、外键....）
2. 一个表最多有一个标识列
3. 标识列的类型只能是数值型
4. 标识列可以通过SET auto_increment_increment = 3;设置步长（全局），可以通过插入行时手动插入标识列值设置起始值。

1.创建表时设置标识列

```sql
1 create table user(
2     id int primary key auto_increment,
3     name varchar(20)
4     );
```

2.修改表时设置标识列

```sql
1     alter table 表名称 modify column id int primary key auto_increment;
```

3.修改表时删除标识列

```sql
1 alter table 表名称 modify column id int primary key;
```

### KEY 和 INDEX比较

单独KEY 和其他关键字结合的KEY(primary key)是不同的

如果只是key的话，就是普通索引

```sql
DROP TABLE IF EXISTS `community_staff_trace`;
CREATE TABLE `community_staff_trace`
(
    `id`             bigint(20) NOT NULL AUTO_INCREMENT,
    `staff_id`       varchar(50)         DEFAULT NULL COMMENT '智慧小镇人员id',
    `standard_image` varchar(255)        DEFAULT NULL COMMENT '底库照片',
    `snap_image`     varchar(255)        DEFAULT NULL COMMENT '抓拍照片',
    `org_id`         varchar(10)         DEFAULT NULL COMMENT '公司id',
    `area_id`        varchar(20)         DEFAULT NULL COMMENT '抓拍区域id',
    `device_id`      varchar(20)         DEFAULT NULL COMMENT '设备id',
    `is_alarm`       varchar(1)          DEFAULT NULL COMMENT '告警状态1:正常 0:异常',
    `similarity`     varchar(20)         DEFAULT NULL COMMENT '相似度',
    `plat_record_id` varchar(50)         DEFAULT NULL COMMENT '老火瞳平台刷脸记录id',
    `snap_time`      timestamp  NULL     DEFAULT NULL COMMENT '抓拍时间',
    `create_time`    timestamp  NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '创建时间',
    PRIMARY KEY (`id`) USING BTREE,
    KEY `staff_id` (`staff_id`) USING BTREE COMMENT '人员id',
    KEY `area_id` (`area_id`) USING BTREE COMMENT '区域id'
) ENGINE = InnoDB
  AUTO_INCREMENT = 2
  DEFAULT CHARSET = utf8
  ROW_FORMAT = COMPACT COMMENT ='人员轨迹表';
```



==key 是数据库的物理结构==，包含两层含义：

1. 约束（偏重于约束和规范数据库的结构完整性）
2. 索引（辅助查询）



**primary key**

> 1. 约束作用（constraint），用来规范一个存储主键和唯一性
> 2. 也在此key上建立了一个主键索引

**unique key**

>1. 约束作用（constraint），规范数据的唯一性
>2. key上建立了一个唯一索引

**foreign key**

>1. 约束作用（constraint），规范数据的引用完整性
>2. key上建立了一个index



mysql的key是同时具有constraint和index的意义，这点和其他数据库表现的可能有区别。

（至少在oracle上建立外键，不会自动建立index），因此创建key也有如下几种方式：
（1）在字段级以key方式建立， 如 create table t (id int not null primary key);
（2）在表级以constraint方式建立，如create table t(id int, CONSTRAINT pk_t_id PRIMARY key (id));
（3）在表级以key方式建立，如create table t(id int, primary key (id));



index 也是数据库的物理结构，用于辅助查询，意义没有key 丰富(primary key ，unique key etc..)创建时会在另外的表空间（mysql中的innodb表空间）以一个类似目录的结构存储

区别在于：

***\*不会去约束索引的字段的行为\****（那是key要做的事情）





# 事务



`InnoDB`提供事务支持，默认的是可重复读（REPEATABLE READ），

`MySQL/InnoDB` 提供SQL标准所描述的所有四个事务隔离级别。你可以在命令行用`--transaction-isolation`选项，或在选项文件里，为所有连接设置默认隔离级别。

`my.inf`文件的`[mysqld]`节里类似如下设置该选项：

```inf
transaction-isolation = {READ-UNCOMMITTED | READ-COMMITTED | REPEATABLE-READ | SERIALIZABLE}
```

## ACID

- 原子性  一个事务必须被视为一个不可分割的最小工作单元，整个事务中的所有操作要么全部提交成功，要么全部失败回滚，对于一个事务来说，不可能只执行其中的一部分操作，这就是事务的原子性
- 一致性   数据库总是从一个一致性的状态转换到另一个一致性的状态(数据处于一种语义上的有意义且正确的状态。一致性是对数据可见性的约束，保证在一个事务中的多次操作的数据中间状态对其他事务不可见的。因为这些中间状态，是一个过渡状态，与事务的开始状态和事务的结束状态是不一致的)。
- 隔离性  通常来说，一个事务所做的修改在最终提交以前，对其他事务是不可见的。
- 持久性  一旦事务提交，则其所做的修改会永久保存到数据库。

隔离性涉及到隔离级别的概念，在不同的隔离级别下，会有不同的表现形式

## 隔离级别

先熟悉这几个概念：

==脏读==

 脏读就是指当一个事务正在访问数据，并且对数据进行了修改，而这种修改还没有提交到数据库中，这时，另外一个事务也访问这个被**修改后未提交**的数据，然后使用了这个数据。

简单说就是读到了未提交的数据

==不可重复读==

是指在一个事务内，多次读同一数据。在这个事务还没有结束时，另外一个事务也访问该同一数据。那么，在第一个事务中的两次读数据之间，由于第二个事务的修改，那么第一个事务两次读到的的数据可能是不一样的。这样就发生了在一个事务内两次读到的数据是不一样的，因此称为是不可重复读。 

简单说就是：一次事务中两次读取相同列数据不一样

==可重复读==

一次事务中两次读取相同列数据一样

==幻读==

第一个事务对一个表中的数据进行了修改，这种修改涉及到表中的全部数据行。同时，第二个事务也修改这个表中的数据，这种修改是向表中插入一行新数据。那么，以后就会发生操作第一个事务的用户发现表中还有没有修改的数据行，就好象发生了幻觉一样。

简单一次事务中同样的查询条件，查询的结果第二次比第一次多，针对insert操作

不可重复读与幻读好像好类似，但其实它们是有很大的不同，不可重复读主要体现在update与delete，而幻读主要体现在insert，从实现层面上讲，要解决不可重复读，我们只需要对查询的数据进行加锁就可以实现，此时update与delete这些行都会阻塞等待，但是insert依旧可以，避免不了幻读，而要解决幻读，必须对其行与行之前也加锁，在mysql中，是通过next key lock（行锁+gap lock）来实现的。



不可重复读发生在update 和 delete  

幻读发生在insert 情形下



隔离级别种类：

| 隔离级别                     | 脏读（Dirty Read） | 不可重复读（NonRepeatable Read） | 幻读（Phantom Read） |
| ---------------------------- | ------------------ | -------------------------------- | -------------------- |
| 未提交读（Read uncommitted） | 可能               | 可能                             | 可能                 |
| 已提交读（Read committed）   | 不可能             | 可能                             | 可能                 |
| 可重复读（Repeatable read）  | 不可能             | 不可能                           | 可能                 |
| 可串行化（Serializable ）    | 不可能             | 不可能                           | 不可能               |

- 未提交读(Read Uncommitted)：允许脏读，也就是可能读取到其他会话中未提交事务修改的数据
- 提交读(Read Committed)：只能读取到已经提交的数据。Oracle等多数数据库默认都是该级别 (不重复读)
- 可重复读(Repeated Read)：可重复读。在同一个事务内的查询都是事务开始时刻一致的，InnoDB默认级别。在SQL标准中，该隔离级别消除了不可重复读，但是还存在幻象读
- 串行读(Serializable)：完全串行化的读，每次读都需要获得表级共享锁，读写相互都会阻塞



mysql默认隔离级别是可重复读

```sql
> SELECT @@tx_isolation;  --mysql 查询隔离级别
> REPEATABLE-READ 
```





```sql
--事务的使用
-- 开启事务
begin;
--start transaction;

--回滚事务
rollback;
rollback work;

--设置事务保存点
savepoint identifier;
--删除事务保存点
release savepoint identifier;
--回滚到事务保存点
rollback to identifier;

--设置事务级别
set transaction





```





# 锁 #

锁包括：全局锁、表锁、行锁、死锁、乐观锁、悲观锁等，不同的数据库引擎支持的锁支持粒度也是不同的

# 日志





# Mysql操作命令和内置函数

## 内置函数

### find_in_set

和 in 功能相似，in 适合常量，find_in_set适合函数

like是广泛的模糊查询，而 find_in_set() 是精确匹配，并且字段值之间用‘,'分开



### concat

将多个字符串连接成一个字符串



### concat_ws

和concat()一样，将多个字符串连接成一个字符串，但是可以一次性指定分隔符～（concat_ws就是concat with separator）

==把分隔符指定为null，结果全部变成了null==



### group_concat



# 性能优化和分布式







# 存储引擎如何选择

存储引擎种类

## InnoDB

数据库概念的混淆

数据库：物理操作系统文件或其他形式文件的集合。在MySQL数据库中，数据库文件可以是frm，MYD，MYI，ibd结尾的文件。当使用NDB引擎时，数据库的文件可能不是操作系统上的文件，而是存放在内存之中的文件。

> 数据是文件的集合，物理介质用来存储信息的
>
> 对数据库数据的任何操作，数据库定义，数据查询，数据维护都是在数据库实例下进行的。通过数据库实例与数据库沟通

实例：MySQL数据库由后台线程以及一个共享内存区组成。共享内存可以被运行的后台程序所共享。
MySQL是 一个但进程多线程架构的数据库，与SQL Server比较类似。Oracle多进程架构

```bash
mysql --help |grep my.cnf
# 可以查看MySQL会在哪些位置找配置文件

show engines \G;
# 登陆mysql，查看mysql存储引擎的特性
```

mysql体系结构图：

![img](https://img2018.cnblogs.com/blog/403167/201901/403167-20190116145915277-683033214.jpg)

连接池组件

管理服务和工具组件

SQL接口组件

查询分析器组件

优化器组件

缓冲组件

插件式存储引擎

物理文件

> 模块组件化，灵活可自定义修改，开源的魅力
>
> 根据不同存储引擎的特点应用，建立不同的表



存储引擎是基于表的，而不是数据库

[MySQL技术内幕]()

InnoDB存储引擎最早是第三方的，后来被Oracle收购

OLTP（Online Transaction Processing 在线事务处理）

InnoDB从MySQL5.5.8版本开始作为默认的存储引擎的

MySQL将InnoDB存储引擎的表单独存放到一个独立的ibd文件中

InnoDB存储引擎支持用裸设备（row disk）用来建立其表空间

InnoDB通过使用多版本并发控制（MVCC）来获得高并发性，并且实现了SQL标准的4中隔离级别，默认为REPEATABLE级别。

使用一种被称为next-key locking（间隙锁）来避免幻读（phantom）现象的产生。InnoDB存储引擎还提供插入缓冲（insert buffer）、二次写（double write）、自适应哈希索引（adaptive hash index）、预读（read ahead）等高性能和高可用的功能

InnoDB 使用聚集（clustered）方式，每张表存储都是按主键的顺序进行存放。如果没有显示在DDL中指定主键，InnoDB存储引擎会每一行生成一个6字节的ROWID，作为主键

InnoDB的数据存储在表空间中，表空间是由InnoDB管理的黑盒文件系统，由一系列系统文件组成。InnoDB可以将每个表的数据和索引存放在单独的文件中。InnoDB也可以使用裸设备作为表空间存储介质。

InnoDB是基于聚簇索引建立，与其他存储引擎有很大的区别，聚簇索引对主键查询有很高的性能，不过它的二级索引（secondary index，非主键索引）必须包含主键列。所以如果主键列很大的话，索引会很大。

MVCC（Multi-Version Concurrency Control）（与MVCC相对的是，基于锁的并发控制，Lock-Based Concurrency Control）是一种基于多版本的并发控制协议，每行数据都增加了两个隐藏字段，一个记录创建的版本号，一个记录删除的版本号。在多版本并发控制中，为了保证数据操作在多线程过程中，保证事务隔离的机制，降低锁竞争的压力，保证较高的并发量，在每开启一个事务时，被操作的数据会生成一条新的数据行（临时），但是在提交前对其他事务是不可见的，对于数据的更新（包括增删改）操作成功，会将这个版本号更新到数据的行中，事务提交成功，将新的版本号更新到此数据行中，这样保证了每个事务操作的数据，都是互不影响的，也不存在锁的问题。

MVCC只工作在 REPEATABLE READ和READ COMMITED隔离级别下。READ UNCOMMITED不是MVCC兼容的，因为查询不能找到适合他们事务版本的行版本；它们每次都只能读到最新的版本。SERIABLABLE也不与MVCC兼容，因为读操作会锁定他们返回的每一行数据。

## MyISAM

在5.5.8之前，MyISAM是默认的引擎，

MyISAM 面向一些OLAP（Online Analysis Processing）数据库应用，包括全文索引、压缩、空间函数。但是MyISAM不支持事务和行级锁，而且在崩溃后无法安全恢复。即使后续版本中MyISAM支持了事务，但是很多人的概念中依然是不支持事务的引擎。



ETL（Extract-Transform-Load）

MyISAM存储引擎由MYD和MYI组成，MYD存放数据文件，MYI存放索引文件，可以通过myisampack工具来进一步压缩数据文件（赫夫曼编码静态算法来压缩，压缩后表是只读的）

支持表大小，5.0之前4GB，如果需要支持大于4GB，指定MAX_ROWS 和AVG_ROW_LENGTH，现在256TB



MyISAM并不是无所事处。对于一些只读数据，或者表空间较小，可以忍受恢复操作，可以使用MyISAM。MyISAM会将表存储在两个文件中：数据文件、索引文件。分别是.MYD、.MYI扩展名。MyISAM表可以包含动态或者静态行。MySQL会根据表定义选择那种行格式。MyISAM表的行记录数，取决于磁盘空间和操作系统中的单个文件最大尺寸。

在MySQL中，默认配置只能存储256TB的数据。因为指向数据记录的指针长度是6字节。需要修改可以修改表的MAX_ROWS和AVG_ROW_LENGTH选项。两个相乘是最大的大小。会导致重建索引。

MyISAM是对整个表加锁，而不是行锁，读取的时候对表加共享锁，写入的时候加排他锁。但是在表有读取查询的同时，也可以往表内写入记录。

对于MyISAM，即使是Blob，Text等等长字段，也可以基于前500字符创建索引，MyISAM支持全文索引，这是一个基于分词创建的索引，也可以支持复杂的查询。

MyISAM可以选择延迟更新索引键，在创建表的时候指定delay_key_write选项，在每次修改执行完成时，不会立刻将修改的索引数据写入磁盘，而是写到缓存区，只有在清理缓存区或者关闭表的时候才会将索引写入磁盘。这可以极大的提升写入性能，但是在主机崩溃时会造成索引损坏，需要执行修复操作。

MyISAM另一个特性是支持压缩表。如果数据在写入后不会修改，那么这个表适合MyISAM压缩表。可以使用myisampack对MyISAM表进行打包，压缩表是不可以修改数据的。压缩表可以极大的减少磁盘占用，因此可以减少磁盘IO，提升性能，压缩表也支持索引，但是索引也是只读的。

整体来说MyISAM并没有那么不堪，但是由于没有行锁机制，所以在海量写入的时候，会导致所有查询处于Locked状态。

**其他存储引擎**

MySQL还有一些其他特殊用途的引擎，有些可能不再支持，具体支持情况参考数据库支持引擎。

## Archive

Archive引擎支持是Insert，Select操作，现在支持索引，Archive引擎会缓存所有的写，并利用zlib对写入行进行压缩，所以比MyISAM表的磁盘IO更少。但是在每次Select查询都需要执行全表扫描。所以在Archive适合日志和数据采集应用。这类应用在分析时往往需要全表扫描忙活着更快的Insert操作场景中也可以使用。

Archive引擎支持行级锁和专用的缓存区，所以可以实现高并发写入，在查询开始到返回表存在的所有行数之前，Archive会阻止其他Select执行，用来实现一致性读。另外也实现了批量写入结束前批量写入数据对读操作不可见，这种机制模仿了事务和MVCC的特性，但是Archive不是一个事务型引擎，而是针对高写入压缩做了优化的简单引擎。

## Blackhole

Blackhole没有实现任何存储机制，它会舍弃所有写入数据，不做任何保存，但是服务器会记录Blackhole表的日志，用于复制数据到备库，或者只是简单的记录到日志，这种特殊的存储引擎可以在一些特俗的复制架构和日志审核时发挥作用。但是不推荐。

## CSV

CSV引擎可以将普通的CSV文件作为MySQL表来处理，但是这种表不支持索引，CSV可以在数据库运行时拷贝或者拷出文件，可以将Excel等电子表格中的数据存储未CSV文件，然后复制到MySQL中，就能在MySQL中打开使用。同样，如果将数据写入到一个CSV引擎表，其他外部程序也可以从表的数据文件中读取CSV的数据。因此CSV可以作为数据交换机制。非常好用。

## Federated

Federated引擎是访问其他MySQL服务器的一个代理，它会创建一个到远程MySQL服务器的客户端连接，并将查询传输到远程服务器执行，然后提取或者发送需要的数据。最初设计该存储引擎是为了和企业级数据库如MicrosoftSQLServer和Oracle的类似特性竞争的，可以说更多的是一种市场行为。尽管该引擎看起来提供了一种很好的跨服务器的灵活性，但也经常带来问题，因此默认是禁用的。

## Memroy

heap

如果需要快速地访问数据，并且这些数据不会被修改，重启以后丢失也没有关系，那么使用Memory表（以前也叫做HEAP表）是非常有用的。Memory表至少比MyISAM表要快一个数量级，因为所有的数据都保存在内存中，不需要进行磁盘I/O。Memory表的结构在重启以后还会保留，但数据会丢失。

Memroy表在很多场景可以发挥好的作用：

1. 用于查找（lookup）或者映射（mapping）表，例如将邮编和州名映射的表。
2. 用于缓存周期性聚合数据（periodicallyaggregateddata）的结果。
3. 用于保存数据分析中产生的中间数据。

Memory表支持Hash索引，因此查找操作非常快。虽然Memory表的速度非常快，但还是无法取代传统的基于磁盘的表。Memroy表是表级锁，因此并发写入的性能较低。它不支持BLOB或TEXT类型的列，并且每行的长度是固定的，所以即使指定了VARCHAR列，实际存储时也会转换成CHAR，这可能导致部分内存的浪费。如果MySQL在执行查询的过程中需要使用临时表来保存中间结果，内部使用的临时表就是Memory表。如果中间结果太大超出了Memory表的限制，或者含有BLOB或TEXT字段，则临时表会转换成MyISAM表。

## Merge

Merge引擎是MyISAM引擎的一个变种。Merge表是由多个MyISAM表合并而来的虚拟表。如果将MySQL用于日志或者数据仓库类应用，该引擎可以发挥作用。但是引入分区功能后，该引擎已经被放弃

## NDB 集群 引擎

NDB集群存储引擎，作为SQL和NDB原生协议之间的接口。MySQL服务器、NDB集群存储引擎，以及分布式的、share-nothing的、容灾的、高可用的NDB数据库的组合，被称为MySQL集群（MySQLCluster）。



**特殊**

## PERFORMANCE_SCHEMA

MySQL 5.5新增一个存储引擎：命名**PERFORMANCE_SCHEMA** ,主要用于收集数据库服务器性能参数。MySQL用户是不能创建存储引擎为PERFORMANCE_SCHEMA的表。

performance_schema提供以下功能：

1. 提供进程等待的详细信息，包括锁、互斥变量、文件信息；
2. 保存历史的事件汇总信息，为提供MySQL服务器性能做出详细的判断；
3. 对于新增和删除监控事件点都非常容易，并可以随意改变mysql服务器的监控周期，例如（CYCLE、MICROSECOND）

**performance_schema功能开启和部分表功能**

Performance的开启很简单，在my.cnf中[mysqld]加入performanc_schema，检查性能数据库是否启动的命令:

SHOW VARIABLES LIKE 'performance_schema';



## 常见问题：

场景适用选择？



## 常见索引引擎

**索引是在存储引擎中实现的，也就是说不同的存储引擎，会使用不同的索引**



BTREE 和 HASH的区别

BTREE :







sql优化



数据库同步问题











## 主键生成策略

uuid



# 自定义函数



## 树结构的查询

这是sql server 写法，mysql 里没有with as 用法

查询一个节点的所有后代（查子树）

```sql
with temp(obj_id, parent_id, other_data, t_level)
as
(
	select obj_id, parent_id, other_data, 0 as t_level from t_obj
    where parent_id = ''
    union all --递归语句
    select c.obj_id, c.parent_id, c.other_data, ce.t_level + 1 from t_obj as c 
    inner join temp as ce 
    on c.parent_id = ce.obj_id
)
select * from temp;
```



查询祖先节点

```sql
with temp(obj_id, parent_id, other_data, t_level)
as 
(
	select obj_id, parent_id, other_data, 0 as t_level from t_obj
	where parent_id = ''
	union all --递归语句
	select c.obj_id, c.parent_id, c.other_data, ce.t_level - 1 from t_obj as c
	inner join temp as ce
    on ce.parent_id = c.obj_id
    where ce.obj_id <> c.parent_id
)
select * from temp order by obj_id asc;
```



mysql

## 向下递归

**利用find_in_set()函数和group_concat()函数实现递归查询：**

```sql
DROP FUNCTION IF EXISTS queryChildrenAreaInfo;
DELIMITER ;;
CREATE FUNCTION queryChildrenAreaInfo(areaId bigint)
RETURNS VARCHAR(4000)
BEGIN
DECLARE sTemp VARCHAR(4000);
DECLARE sTempChd VARCHAR(4000);

SET sTemp='$';
SET sTempChd = CAST(areaId AS CHAR);

WHILE sTempChd IS NOT NULL DO
SET sTemp= CONCAT(sTemp,',',sTempChd);
SELECT GROUP_CONCAT(id) INTO sTempChd FROM t_areainfo WHERE FIND_IN_SET(parentId,sTempChd)>0;
END WHILE;
RETURN sTemp;
END
;;
DELIMITER ;

-- 调用方式
select * from t_area where find_in_set(area_id, queryChildrenAreaInfo(1));
```



## 向上递归

```sql
DROP FUNCTION IF EXISTS queryChildrenAreaInfo1;
DELIMITER;;
CREATE FUNCTION queryChildrenAreaInfo1(areaId INT)
RETURNS VARCHAR(4000)
BEGIN
DECLARE sTemp VARCHAR(4000);
DECLARE sTempChd VARCHAR(4000);

SET sTemp='$';
SET sTempChd = CAST(areaId AS CHAR);
SET sTemp = CONCAT(sTemp,',',sTempChd);

SELECT parentId INTO sTempChd FROM t_areainfo WHERE id = sTempChd;
WHILE sTempChd <> 0 DO
SET sTemp = CONCAT(sTemp,',',sTempChd);
SELECT parentId INTO sTempChd FROM t_areainfo WHERE id = sTempChd;
END WHILE;
RETURN sTemp;
END
;;
DELIMITER ;
```



# value 和 values

**插入单行** 的时候使用VALUES，在 **插入多行** 的时候使用VALUE 这样比较快一点

这个value表现和数量的表现是相反的，单数复数

# 临时表

特点：

- 生命周期：会话， 临时表只在当前连接可见，当关闭连接时，Mysql会自动删除表并释放所有空间
- 在会话中可以使用drop table 来销毁
- 3.23版本之后才有

example

```sql
mysql> CREATE TEMPORARY TABLE SalesSummary (
    -> product_name VARCHAR(50) NOT NULL
    -> , total_sales DECIMAL(12,2) NOT NULL DEFAULT 0.00
    -> , avg_unit_price DECIMAL(7,2) NOT NULL DEFAULT 0.00
    -> , total_units_sold INT UNSIGNED NOT NULL DEFAULT 0
);



Query OK, 0 rows affected (0.00 sec)

mysql> INSERT INTO SalesSummary
    -> (product_name, total_sales, avg_unit_price, total_units_sold)
    -> VALUES
    -> ('cucumber', 100.25, 90, 2);

mysql> SELECT * FROM SalesSummary;
+--------------+-------------+----------------+------------------+
| product_name | total_sales | avg_unit_price | total_units_sold |
+--------------+-------------+----------------+------------------+
| cucumber     |      100.25 |          90.00 |                2 |
+--------------+-------------+----------------+------------------+
1 row in set (0.00 sec)
mysql> DROP TABLE SalesSummary;
mysql>  SELECT * FROM SalesSummary;
ERROR 1146: Table 'RUNOOB.SalesSummary' doesn't exist
```

用查询直接创建临时表的方式

```sql
CREATE TEMPORARY TABLE 临时表名 AS
(
    SELECT *  FROM 旧的表名
    LIMIT 0,10000
);
```



## 一张表查出数据插入另一张表

```sql
insert into A(a,b,c)(select a,b,c from B);
```

实例

```sql
set @a := 0;
insert into sys_role_access(`id`, role_id, access_id, create_user_id, modify_user_id)(select @a := @a + 1 as `id`, 1 as role_id, id as access_id, 1 as `create_user_id`, 1 as `modify_user_id` from sys_access);
```





# sql优化措施

1. 对查询进行优化，应尽量避免全表扫描，首先应考虑在 where 及 order by 涉及的列上建立索引。注意：要想使用or，又想让索引生效，只能将or条件中的每个列都加上索引
2. 应尽量避免在 where 子句中使用!=或<>（不等于）操作符，否则将引擎放弃使用索引而进行全表扫描。
3. 应尽量避免在 where 子句中对字段进行 null 值判断，否则将导致引擎放弃使用索引而进行全表扫描。可以设置默认值，避免使用null
4. 左模糊查询"%--"是无法使用索引的，右模糊会走索引







