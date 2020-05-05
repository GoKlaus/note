[toc]



# 添加依赖

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
    <version>some-version</version>
</dependency>
```

使用这个jar包

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

使用这个报错，java.lang.ArrayStoreException: sun.reflect.annotation.TypeNotPresentExceptionProxy

是jar冲突问题

# 启动Eureka-Client后就关闭问题

缺少jar包

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
```

