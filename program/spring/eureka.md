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





eureka上删除服务：
1、http://172.16.3.16:11000/eureka/apps/
获取到所有服务信息

如：

```xml
<instance>
            <instanceId>172.16.3.231=28005</instanceId>
            <hostName>172.16.3.231</hostName>
            <app>SMARTCOMMUNITY-STAFF</app>
            <ipAddr>172.16.3.231</ipAddr>
            <status>UP</status>
            <overriddenstatus>UNKNOWN</overriddenstatus>
            <port enabled="true">28005</port>
            <securePort enabled="false">443</securePort>
            <countryId>1</countryId>
            <dataCenterInfo class="com.netflix.appinfo.InstanceInfo$DefaultDataCenterInfo">
                <name>MyOwn</name>
            </dataCenterInfo>
```



 2、取出对应的instanceId和app字段值（172.16.3.231=28005，SMARTCOMMUNITY-STAFF）
 http://172.16.3.16:11000/eureka/apps/SMARTCOMMUNITY-USER/172.20.237.180=28004  DELETE  删除对应的无效服务