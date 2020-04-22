

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