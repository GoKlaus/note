

[TOC]

# 1.简介





# 2.

## 2.1where标签的使用

> 作用：动态sql

```sql
<select id="selectByParams" parameterType="map" resultType="user">
　　　　select * from user
　　　　<where>
　　　　　　<if test="id != null ">id=#{id}</if>
　　　　　　<if test="name != null and name.length()>0" >and name=#{name}</if>
　　　　　　<if test="gender != null and gender.length()>0">and gender = #{gender}</if>
　　　　</where>
　　</select>　　　
```

## 2.2





在分布式环境下，务必将MyBatis的localCacheScope属性设置为STATEMENT，避免其他应用节点执行SQL更新语句后，本节点缓存得不到刷新而导致的数据一致性问题

```java
public enum LocalCacheScope {
  /**
   *
   */
  SESSION,

  /**
   * 每次都会清除缓存
   */
  STATEMENT
}
```

# 实际遇到问题

jar包中的mapper.xml文件加载

用 classpath 和 classpath*的区别来完成





## sql注入

概念

```
SQL注入攻击，简称SQL攻击或注入攻击，是发生于应用程序之数据库层的安全漏洞。简而言之，是在输入的字符串之中注入SQL指令，在设计不良的程序当中忽略了检查，那么这些注入进去的指令就会被数据库服务器误认为是正常的SQL指令而运行，因此遭到破坏或是入侵。
```



有哪些解决方案：

- `#{value}` 在预处理时，会把参数部分用一个占位符 ? 替代，其中 value 表示接受输入参数的名称。能有效解决 SQL 注入问题
- `${}` 表示使用拼接字符串，将接受到参数的内容不加任何修饰符拼接在 SQL 中，使用`${}`拼接 sql，将引起 SQL 注入问题。

举例：

```sql
SELECT * FROM XXX WHERE userName = admin and password = 111;
select * from xxx where username = admin or 1 = 1 # and password = 111;
# '#'在sql语句中是注释，将后面密码的验证去掉了，而前面的条件中1 = 1始终成立，所以不管密码正确与否，都能登录成功
```



在spring框架集成使用方式下，是通过MapperProxy来动态代理的




JDBC（Java Database Connectivity）是Java语言中提供的访问关系型数据的接口。在Java编写的应用中，使用JDBC API可以执行SQL语句、检索SQL执行结果以及将数据更改写回到底层数据源。JDBC API也可以用于分布式、异构的环境中与多个数据源交互。

JDBC API基于X/Open SQL CLI，是ODBC的基础。JDBC提供了一种自然的、易于使用的Java语言与数据库交互的接口。自1997年1月Java语言引入JDBC规范后，JDBC API被广泛接受，并且广大数据库厂商开始提供JDBC驱动的实现。JDBC API为Java程序提供了访问一个或多个数据源的方法。

在大多数情况下，数据源是关系型数据库，它的数据是通过SQL语句来访问的。当然，**使用JDBC访问其他数据源（例如文件系统或者面向对象系统等）也是有可能的**，只要该数据源提供JDBC规范驱动程序即可。

使用JDBC操作数据源大致需要以下几个步骤：

（1）与数据源建立连接。

（2）执行SQL语句。

（3）检索SQL执行结果。

（4）关闭连接。



DriverManager



DataSource

JDBC API中定义了两个DataSource接口比较重要的扩展，用于支撑企业级应用。这两个接口分别为：ConnectionPoolDataSource　支持缓存和复用Connection对象，这样能够在很大程度上提升应用性能和伸缩性。XADataSource　该实例返回的Connection对象能够支持分布式事务

更多关于分布式事务相关细节可参考JTA（Java Transaction API）规范文档

DatabaseMetadata

使用DatabaseMetadata的实例来确定目前使用的数据源是否支持某一特性，不同的JDBC厂商对这些特性的支持程度各不相同



==JDBC API由java.sql和javax.sql两个包构成==



## Statement 接口

Statement接口及它的子接口PreparedStatement和CallableStatement

Statement接口中定义了执行SQL语句的方法，这些方法不支持参数输入

PreparedStatement接口中增加了设置SQL参数的方法

CallableStatement接口继承自PreparedStatement，在此基础上增加了调用存储过程以及检索存储过程调用结果的方法





事务中的保存点

保存点通过在事务中标记一个中间的点来对事务进行更细粒度的控制，一旦设置保存点，事务就可以回滚到保存点，而不影响保存点之前的操作。DatabaseMetaData接口提供了supportsSavepoints()方法，用于判断JDBC驱动是否支持保存点。





SQL类用于在Java代码中动态构建SQL语句

SqlRunner和ScriptRunner在MyBatis源码测试用例中出现的频率较高，用于执行SQL脚本和SQL语句

MetaObject和MetaClass是MyBatis中的反射工具类，封装了对类和对象的操作

ObjectFactory和ProxyFactory是对象创建相关的工具类

ObjectFactory用于创建Mapper映射实体对象

ProxyFactory则用于创建Mapper映射实体对象的动态代理对象，通过动态代理来实现MyBatis中的懒加载机制





SqlSession是MyBatis中提供的与数据库交互的接口，SqlSession实例通过工厂模式创建