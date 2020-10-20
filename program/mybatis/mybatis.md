

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



# 实际遇到问题

jar包中的mapper.xml文件加载

用 classpath 和 classpath*的区别来完成



if test 判断list 是否空

```xml
<!-- -->
<if test="list!=null and list.size()!=0">
</if>
```



if test 判断str 

```xml
<if test="type!=null and type!=''">  
    AND type = #{type}  
</if> 
```



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