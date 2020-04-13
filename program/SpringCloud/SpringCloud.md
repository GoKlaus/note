# SpringCloud

概念：

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
- 选型中立、丰富。例如，springcloud支持使用Eureka、Zookeeper或Consul实现服务发现
- 灵活。springcloud的组成部分是解耦的，开发人员可以按需求灵活挑选技术选型```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-netflix-eureka-server</artifactId>
</dependency>
<!--使用这两个依赖不同，第一个依赖可以直接自动注入配置，第二个不行-->

```

```



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