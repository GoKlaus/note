# RPC

RPC(Remote Procedure Call)---远程过程调用：

## Dubbo的总体架构图

![img](http://klaus_project.gitee.io/pic/note/1147548-20170928141450169-1251868962.png)

主要角色：

服务提供方（Provider）

服务消费方（Consumer）

注册中心（Registry Center）

![img](http://klaus_project.gitee.io/pic/note/1147548-20170928143017294-1702265087.png)

![img](http://klaus_project.gitee.io/pic/note/1147548-20170928143227981-1007327667.png)

## 协议支持

Dubbo支持多种协议，如下所示：

- Dubbo协议
- Hessian协议
- HTTP协议
- RMI协议
- WebService协议
- Thrift协议
- Memcached协议
- Redis协议
- Rest--基于标准的Java  REST  API—JAX-RS(Java API for RESTful Web Services的简写)实现的REST调用支持(dubbox支持)

[几种协议的使用场景][]

Dubbo源于阿里的淘宝网开源的分布式的服务架构，致力于提供高性能和透明化的RPC远程服务调用方案，是SOA服务化治理方案的核心框架。淘宝网将其开源之后，得到了很多的拓展和支持（比较出名的有：当当网的扩展版本dubbox，京东的扩展版本jd-hydra等）

       Dubbox（即Dubbo eXtensions）是当当网Fork基于dubbo2.x的升级版本，兼容原有的dubbox。其中升级了zookeeper和spring版本，并且支持restfull风格的远程调用

目前开发中主要通过的是dubbo协议

[协议参考](../tcp-ip/tcp-ip.md)



# 使用方式

## API配置

简单来说：API配置就是不使用注解和xml的，就是使用相应的jar包，去掉spring的依赖，在类中硬编码

## schema配置





## 配置的加载流程

dubbo支持的配置驱动方式有三种：XML配置、Annotation配置、API配置，这些在形式上会有差异，读取的时候总体遵循一下几个原则：

1. Dubbo支持了多层级的配置，并按照预定优先级自动实现配置间的覆盖，最终所有配置汇总到数据总线URL后驱动后续的服务暴露、引用等流程
2. ApplicationConfig、ServiceConfig、ReferenceConfig可以被理解成配置来源的一种，是直接面向用户编程的配置采集方式。
3. 配置格式以Properties为主，在配置内容上遵循约的path-based的命名规范。

```
多层级的配置：同样的配置，可以在provider、consumer中都可以配置，但是按照内置的优先级，优先采用高的
API的配置方式，在代码中自己手动完成，使用不多，目前没什么经验
配置的格式问题可以直接参考
```

## 配置的来源

默认四种：

1. JVM System Properties，-D参数
2. Externalized Configuration，外部化配置
3. ServiceConfig、ReferenceConfig等编程接口采集的配置
4. 本地配置文件dubbo.properties

## 覆盖关系

下图展示了配置覆盖关系的优先级，从上到下优先级依次降低：

![配置优先级](http://klaus_project.gitee.io/pic/note/configuration.jpg)





[官方文档][]

[dubbo源码][]



# SOA（服务治理）



# 监控

[][]

[dubbo ops][]



# dubbo的本地调试模式

开发中多人并行开发项目，存在公用一个注册中心，调试不一定是自己开发依赖的模块，用本地调试模式可以避免这种情况的发生：

三种方法可以选择：

1. 停止同一个服务版本的其他提供者，启动本地的服务提供者(多人开发的时候不适用)

2. 在消费者的.xml里对应服务的<dubbo:reference>里面加入属性url="dubbo://localhost:19604"，然后启动本地提供者，就可以实现dubbo直连，调试本地程序(有点麻烦)

3. 在当前登录用户下面加入dubbo-resolve.properties文件，内容指定要调试的服务，格式如下：com.emar.adx.yiqifa.adcenter.bl.service.CompleteProductService=dubbo\://localhost\:19604       之后启动相应的服务。

   >
   >
   >使用方式在JVM启动参数中加入-D参数映射服务地址，如：
   >
   >单个：
   >
   >(key为服务名，value为服务提供者url，此配置优先级最高，1.0.15及以上版本支持)
   >
   >> java -Dcom.alibaba.xxx.XxxService=dubbo://localhost:20890
   >
   >多个服务可以使用文件映射：
   >
   >(用-Ddubbo.resolve.file指定映射文件路径，此配置优先级高于<dubbo:reference>中的配置，1.0.15及以上版本支持)
   >(2.0以上版本自动加载${user.home}/dubbo-resolve.properties文件，不需要配置)
   >
   >> java -Ddubbo.resolve.file=xxx.properties
   >>
   >> 这种写法是默认加载${user.home}下的文件，对于win系统来说${user.home}指的是当前操作系统用户目录，如 Win7系统 Administrator的用户目录就是 C:\Users\Administrator
   >>



# dubbo-admin

## 搭建dubbo-admin的注意事项

### 1、dubbo-admin

使用github上的dubbo-admin项目来搭建

编译缓慢，而且需要nodejs来编译，且报错，后续没有继续采用这个方法

### 2、dubbo

直接将2.5.x版本的dubbo源码下载下来，然后编译了dubbo-admin部分，成功搭建了dubbo-admin





# 参数校验

项目中Controller进行了参数校验通过Spring的验证框架

而dubbo使用硬代码编写，对代码侵入较大，探索能否使用javax.validator配合注解来完成

dubbo里面自带了validator的实现

参考：

[聊聊dubbo的ValidationFilter](https://segmentfault.com/a/1190000019614955)







[官方文档]: https://dubbo.apache.org/zh-cn/	"官方文档"
[dubbo源码]: https://github.com/apache/dubbo	"dubbo源码"
[dubbo ops]: https://www.cnblogs.com/zjfjava/p/9694540.html



[几种协议的使用场景]: https://blog.csdn.net/lhx13636332274/article/details/73740960