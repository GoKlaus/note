[TOC]


# SpringCloud

bootstrap.yml作用

1. 可以加载外部配置
2. 优先级最高，不能被application.yml覆盖重写

```properties
# 通过设置SystemProperties 系统变量来禁用bootstrap配置文件
spring.cloud.bootstrap.enabled=false
```





















# SpringCloud 和 Dubbo 对比

概念：

提springcloud 就离不开微服务的概念

“微服务”一词来源于 Martin Fowler 的《Microservices》一文。微服务是一种架构风格，即将单体应用划分为小型的服务单元，微服务之间使用 HTTP 的 API 进行资源访问与操作。

使用nginx进行分发的缺点：

使用nginx的架构：在配置文件中耦合了服务调用的逻辑，削弱了微服务的完整性，也使得nginx在一定程度上变成了一个重量级的ESB（Enterprise Service Bus 企业服务总线）

Nginx 的转发信息流走向：

![Nginx转发的信息流](/home/klaus/documents/pic/note/5-1ZQ61JA91L.png)

服务的信息分散在各个系统，无法统一管理和维护。每一次的服务调用都是一次尝试，服务消费方并不知道有哪些实例在给他们提供服务。（不透明，不利于治理）这带来了一些问题：

- 无法直观地看到服务提供方和服务消费方当前的运行状况与通信频率；
- 消费方的失败重发、负载均衡等都没有统一策略，这加大了开发每个服务的难度，不利于快速演化。

为了解决上面的问题，我们需要一个现成的中心组件对服务进行整合，将每个服务的信息汇总，包括服务的组件名称、地址、数量等。

服务的调用方在请求某项服务时首先通过中心组件获取提供服务的实例信息（IP、端口等），再通过默认或自定义的策略选择该服务的某一提供方直接进行访问，所以考虑引入 Dubbo。

Dubbo 是阿里开源的一个 SOA 服务治理解决方案，文档丰富，在国内的使用度非常高。图 2 为 Dubbo 的基本架构图，使用 Dubbo 构建的微服务已经可以较好地解决上面提到的问题

![Dubbo的基本架构图](/home/klaus/documents/pic/note/5-1ZQ61J953103.png)

从上图可以看出：

- 调用中间层变成了可选组件，消费方可以直接访问服务提供方；
- 服务信息被集中到 Registry 中，形成了服务治理的中心组件；
- 通过 Monitor 监控系统，可以直观地展示服务调用的统计信息；
- 服务消费者可以进行负载均衡、服务降级的选择。

dubbo的缺陷：

- 只支持rpc。服务提供方与调用方在代码上产生了强依赖，服务提供方需要不断将包含公共代码的 Jar 包打包出来供消费方使用。一旦打包出现问题，就会导致服务调用出错。（Dubbo框架的jar包依赖问题）Registry 严重依赖第三方组件（ZooKeeper 或者 [Redis](http://c.biancheng.net/redis/)），当这些组件出现问题时，服务调用很快就会中断。



Dubbo 和 [Spring Cloud](http://c.biancheng.net/spring_cloud/) 并不是完全的竞争关系，两者所解决的问题域并不一样。

Dubbo 的定位始终是一款 RPC 框架，而 [Spring](http://c.biancheng.net/spring/) Cloud 的目标是微服务架构下的一站式解决方案。如果非要比较的话，Dubbo 可以类比到 Netflix OSS 技术栈，而 Spring Cloud 集成了 Netflix OSS 作为分布式服务治理解决方案，但除此之外 Spring Cloud 还提供了配置、消息、安全、调用链跟踪等分布式问题解决方案。

| **功能名称** | **Dubbo** | **Spring Cloud**             |
| ------------ | --------- | ---------------------------- |
| 服务注册中心 | ZooKeeper | Spring Cloud Netflix Eureka  |
| 服务调用方式 | RPC       | REST API                     |
| 服务网关     | 无        | Spring Cloud Netflix Zuul    |
| 断路器       | 不完善    | Spring Cloud Netflix Hystrix |
| 分布式配置   | 无        | Spring Cloud Config          |
| 服务跟踪     | 无        | Spring Cloud Sleuth          |
| 消息总线     | 无        | Spring Cloud Bus             |
| 数据流       | 无        | Spring Cloud Stream          |
| 批量任务     | 无        | Spring Cloud Task            |
|              |           |                              |























Iaas：

Infrastructure as a Service  基础设施即服务

Paas：



Caas：



## springcloud特点

- 约定优于配置
- 适用各种环境。开发部署在PC Server或各种云环境（例如阿里云，AWS等）均可
- 隐藏了组件的复杂性，并提供声明式、无xml的配置方式
- 开箱即用，快速启动
- 轻量级的组件。springcloud的组件大都比较轻量，例如Eureka、Zuul等都是各自领域轻量级的实现
- 组件丰富，功能齐全。springcloud为微服务架构提供了非常完整的支持。例如，配置管理，服务发现，断路器，微服务网关等
- 选型中立、丰富。例如，springcloud支持使用Eureka、Zookeeper或Consul实现服务发现，nacos
- 灵活。springcloud的组成部分是解耦的，开发人员可以按需求灵活挑选技术选型--基于Java 的 spi 思想





<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-netflix-eureka-server</artifactId>
</dependency>
<!--使用这两个依赖不同，第一个依赖可以直接自动注入配置，第二个不行-->



spring cloud 和 dubbo 都是微服务整体解决方案

dubbo使用二进制传输，带宽占用较少

springcloud http协议传送， 如果加上JSON报文，消耗更大



dubbo开发难度大，存在jar包依赖问题



springcloud 接口协议约定比较自由松散，



dubbo注册中心 zk redis

springcloud eureka 或自研





Dubbo具有调度、发现、监控、治理等功能，**支持相当丰富的服务治理能力**。Dubbo架构下，注册中心对等集群，并会缓存服务列表已被数据库失效时继续提供发现功能，本身的服务发现结构有很强的**可用性与健壮性**，



Spring Cloud由众多子项目组成，如Spring Cloud Config、Spring Cloud Netflix、Spring Cloud Consul 等，提供了搭建分布式系统及微服务常用的工具，如**配置管理、服务发现、断路器、智能路由、微代理、控制总线、一次性token、全局锁、选主、分布式会话和集群状态等**，满足了构建微服务所需的所有解决方案。比如使用Spring Cloud Config 可以实现统一配置中心，对配置进行统一管理；使用Spring Cloud Netflix 可以实现Netflix 组件的功能 - 服务发现（Eureka）、智能路由（Zuul）、客户端负载均衡（Ribbon）。

但它并没有重复造轮子，而是选用目前各家公司开发的比较成熟的、经得住实践考验的服务框架（我们需要特别感谢Netflix ，这家很早就成功实践微服务的公司，几年前把自家几乎整个微服务框架栈贡献给了社区，Spring Cloud主要是对Netflix开源组件的进一步封装），通过Spring Boot 进行封装集成并简化其使用方式。基于Spring Boot，意味着其使用方式如Spring Boot 简单易用；能够与Spring Framework、Spring Boot、Spring Data 等其他Spring 项目完美融合，意味着能从Spring获得巨大的便利，意味着能减少已有项目的迁移成本。

其实，从社区活跃度和功能完整度，再对照业务需求和团队状况，基本可以确定如何选型。这里分享网易考拉海购实践以及团队选型的心声：

当前开源上可选用的微服务框架主要有Dubbo、Spring Cloud等，鉴于Dubbo完备的功能和文档且在国内被众多大型互联网公司选用，





# 实际遇到问题

```java
com.netflix.zuul.exception.ZuulException: Forwarding error
```

zuul的调用等待时间超时， 可以加入配置

```yml
##timeout config
hystrix:
  command:
    default:
      execution:
        timeout:
          enabled: true
        isolation:
          thread:
            timeoutInMilliseconds: 60000
ribbon:
  ReadTimeout: 60000
  ConnectTimeout: 60000
  MaxAutoRetries: 0
  MaxAutoRetriesNextServer: 1
  eureka:
    enabled: false

zuul:
  max:
    host:
      connections: 500
  host:
    socket-timeout-millis: 60000
```



## 鉴权逻辑

注册需要添加依赖

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    <version>1.4.4.RELEASE</version>
</dependency>
```

不添加，也不报错，但是就是没有注册信息





自定义过滤器：

模拟一个登录的校验。

基本逻辑：如果请求中有access-token参数，则认为请求有效，放行。

```java
@Component
public class LoginFilter extends ZuulFilter{
    @Override
    public String filterType() {
        // 登录校验，肯定是在前置拦截
        return FilterConstants.PRE_TYPE;
    }
 
    @Override
    public int filterOrder() {
        // 该常量值为5 ，减1后为4
        return FilterConstants.PRE_DECORATION_FILTER_ORDER - 1;
    }
 
    @Override
    public boolean shouldFilter() {
        // 返回true，代表过滤器生效。
        return true;
    }
 
    @Override
    public Object run() throws ZuulException {
        // 登录校验逻辑。
        // 1）获取Zuul提供的请求上下文对象
        RequestContext ctx = RequestContext.getCurrentContext();//RequestContext是一个Request域，此域的作用范围是从请求到达zuul一直到路由结束返回到客户端，整个完整流程都会存在
        // 2) 从上下文中获取request对象
        HttpServletRequest req = ctx.getRequest();
        // 3) 从请求中获取token
        String token = req.getParameter("access-token");
        // 4) 判断
        if(StringUtils.isBlank(token)){ //StringUtils,需引apache的commons-lang3包的依赖 使用此方式可以避免内存溢出
            // 没有token，登录校验失败，拦截
            ctx.setSendZuulResponse(false);//true则放行，false则拦截
            // 返回403状态码。也可以考虑重定向到登录页。
            ctx.setResponseStatusCode(HttpStatus.Forbidden.value());
        }
        // 校验通过，可以考虑把用户信息放入上下文，继续向后执行
        return null;//默认为空即为放行
    }
}
```

权限校验：

```java

```



# zuul 请求服务无法新携带数据问题

```java
 ctx.addZuulRequestHeader("userId", String.valueOf(map.get("userId")));
        ctx.addZuulRequestHeader("orgId", String.valueOf(map.get("orgId")));
```

参考



## zuul 请求对MultipartFile的重置问题

开发中一个请求中带有上传文件，ContentType 为 multipart/form-data

但是到了具体服务不会认为是这个类型





## @RequestBody和 MultipartFile 冲突的问题

为什么冲突

@RequestBody常用来处理Content-Type: 不是application/x-www-form-urlencoded编码的内容，例如application/json, application/xml等

MultipartFile 可以处理Content-Type为application/x-www-form-urlencoded application/form-data



# SpringCloud feign 文件上传问题

原因：

feign对象相当于发起新的http请求，不做设置是不会支持文件上传的两种Content-Type的

解决方案 

```java

```

