[toc]

# 内容

1. 服务发现--eureka
2. 断路器--hytrix
3. 智能路由--zuul
4. 负载均衡--ribbon

eureka保证高可用：eureka server之间复制同步注册的服务

client的心跳机制，默认心跳时间30s

```
Being an instance also involves a periodic heartbeat to the registry (via the client’s serviceUrl) with default duration 30 seconds
```



服务状态页面和指示页面

```yml
eureka:
  instance:
    hostname: localhost
    instance-id: http://${eureka.instance.hostname}:${server.port}
#    默认/actuator/info
    status-page-url-path: ${management.contextPath}/info
#    默认/actuator/health
    health-check-url-path: ${management.contextPath}/health
```



在aws上使用eureka

定制[EurekaInstanceConfigBean](https://github.com/spring-cloud/spring-cloud-netflix/tree/master/spring-cloud-netflix-eureka-client/src/main/java/org/springframework/cloud/netflix/eureka/EurekaInstanceConfigBean.java)

```java
@Bean
@Profile("!default")
public EurekaInstanceConfigBean eurekaInstanceConfig() {
  EurekaInstanceConfigBean b = new EurekaInstanceConfigBean();
  AmazonInfo info = AmazonInfo.Builder.newBuilder().autoBuild("eureka");
  b.setDataCenterInfo(info);
  return b;
}
```

