

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