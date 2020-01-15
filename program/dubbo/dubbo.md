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



协议的问题，可以了解具体协议族的相关知识点，这个比较多，通讯协议可以从TCP/IP类书籍去学习，这里说一下OSI七层模型和TCP/IP五层模型

![enter image description here](http://klaus_project.gitee.io/pic/note/2018032308054680.jpg)

**物理层（Physical Layer）**：主要定义物理设备标准，如网线的接口类型、光纤的接口类型、各种传输介质的传输速率等。它的主要作用是传输比特流（就是由1、0转化为电流强弱来进行传输,到达目的地后在转化为1、0，也就是我们常说的数模转换与模数转换），这一层的数据叫做比特，单位是bit比特。

**数据链路层（Datalink Layer）**：定义了如何让格式化数据以进行传输，以及如何让控制对物理介质的访问，这一层通常还提供错误检测和纠正，以确保数据的可靠传输。交换机(二层)、网桥设备在这一层。数据链路层协议的代表包括：PPP、STP、帧中继等。

**网络层（Network Layer）**：在位于不同地理位置的网络中的两个主机系统之间提供连接和路径选择，Internet的发展使得从世界各站点访问信息的用户数大大增加，而网络层正是管理这种连接的层。网络层负责在源机器和目标机器之间建立它们所使用的路由。路由器在该层。协议有：IP、ICMP（互联网控制报文协议）、ARP（地址转换协议）、RARP（反向地址转换协议）

**传输层（Transport Layer）**：O S I 模型中最重要的一层。定义了一些传输数据的协议和端口号（WWW端口80等），如：TCP（传输控制说协议，传输效率低，可靠性强，用于传输可靠性要求高，数据量大的数据），UDP（用户数据报协议，与TCP特性恰恰相反，用于传输可靠性要求不高，数据量小的数据，如QQ聊天数据就是通过这种方式传输的）， 主要是将从下层接收的数据进行分段和传输，到达目的地址后再进行重组，常常把这一层数据叫做段。

传输协议同时进行流量控制或是基于接收方可接收数据的快慢程度规定适当的发送速率。除此之外，传输层按照网络能处理的最大尺寸将较长的数据包进行强制分割。例如，以太网无法接收大于1 5 0 0 字节的数据包。发送方节点的传输层将数据分割成较小的数据片，同时对每一数据片安排一序列号，以便数据到达接收方节点的传输层时，能以正确的顺序重组。该过程即被称为排序。

**会话层（Session Layer）**：负责在网络中的两节点之间建立、维持和终止通信。 会话层的功能包括：建立通信链接，保持会话过程通信链接的畅通，同步两个节点之间的对话，决定通信是否被中断以及通信中断时决定从何处重新发送。

通过传输层（端口号：传输端口与接收端口）建立数据传输的通路，主要在你的系统之间发起会话或者接受会话请求（设备之间需要互相认识可以是IP也可以是MAC或者是主机名）。

**表示层（Presentation Layer）**：应用程序和网络之间的翻译官，在表示层，数据将按照网络能理解的方案进行格式化；这种格式化也因所使用网络的类型不同而不同。 　　表示层管理数据的解密与加密，如系统口令的处理。可确保一个系统的应用层所发送的信息可以被另一个系统的应用层读取。例如，PC程序与另一台计算机进行通信，其中一台计算机使用扩展二一十进制交换码（EBCDIC），而另一台则使用美国信息交换标准码（ASCII）来表示相同的字符。如有必要，表示层会通过使用一种通格式来实现多种数据格式之间的转换。

**应用层（Application Layer）**： 是最靠近用户的OSI层，这一层为用户的应用程序（例如电子邮件、文件传输和终端仿真）提供网络服务。



## 三次握手与四次挥手

所谓三次握手(Three-way Handshake)，是指建立一个 TCP 连接时，需要客户端和服务器总共发送3个包。

三次握手的目的是连接服务器指定端口，建立 TCP 连接，并同步连接双方的序列号和确认号，交换 TCP 窗口大小信息。在 socket 编程中，客户端执行 `connect()` 时。将触发三次握手。

- 第一次握手(SYN=1, seq=x):

  客户端发送一个 TCP 的 SYN 标志位置1的包，指明客户端打算连接的服务器的端口，以及初始序号 X,保存在包头的序列号(Sequence Number)字段里。

  发送完毕后，客户端进入 `SYN_SEND` 状态。

- 第二次握手(SYN=1, ACK=1, seq=y, ACKnum=x+1):

  服务器发回确认包(ACK)应答。即 SYN 标志位和 ACK 标志位均为1。服务器端选择自己 ISN 序列号，放到 Seq 域里，同时将确认序号(Acknowledgement Number)设置为客户的 ISN 加1，即X+1。 发送完毕后，服务器端进入 `SYN_RCVD` 状态。

- 第三次握手(ACK=1，ACKnum=y+1)

  客户端再次发送确认包(ACK)，SYN 标志位为0，ACK 标志位为1，并且把服务器发来 ACK 的序号字段+1，放在确定字段中发送给对方，并且在数据段放写ISN的+1

  发送完毕后，客户端进入 `ESTABLISHED` 状态，当服务器端接收到这个包时，也进入 `ESTABLISHED` 状态，TCP 握手结束。

三次握手的过程的示意图如下：

![三次握手](http://klaus_project.gitee.io/pic/note/tcp-connection-made-three-way-handshake.png)

TCP 的连接的拆除需要发送四个包，因此称为四次挥手(Four-way handshake)，也叫做改进的三次握手。客户端或服务器均可主动发起挥手动作，在 socket 编程中，任何一方执行 `close()` 操作即可产生挥手操作。

- 第一次挥手(FIN=1，seq=x)

  假设客户端想要关闭连接，客户端发送一个 FIN 标志位置为1的包，表示自己已经没有数据可以发送了，但是仍然可以接受数据。

  发送完毕后，客户端进入 `FIN_WAIT_1` 状态。

- 第二次挥手(ACK=1，ACKnum=x+1)

  服务器端确认客户端的 FIN 包，发送一个确认包，表明自己接受到了客户端关闭连接的请求，但还没有准备好关闭连接。

  发送完毕后，服务器端进入 `CLOSE_WAIT` 状态，客户端接收到这个确认包之后，进入 `FIN_WAIT_2` 状态，等待服务器端关闭连接。

- 第三次挥手(FIN=1，seq=y)

  服务器端准备好关闭连接时，向客户端发送结束连接请求，FIN 置为1。

  发送完毕后，服务器端进入 `LAST_ACK` 状态，等待来自客户端的最后一个ACK。

- 第四次挥手(ACK=1，ACKnum=y+1)

  客户端接收到来自服务器端的关闭请求，发送一个确认包，并进入 `TIME_WAIT`状态，等待可能出现的要求重传的 ACK 包。

  服务器端接收到这个确认包之后，关闭连接，进入 `CLOSED` 状态。

  客户端等待了某个固定时间（两个最大段生命周期，2MSL，2 Maximum Segment Lifetime）之后，没有收到服务器端的 ACK ，认为服务器端已经正常关闭连接，于是自己也关闭连接，进入 `CLOSED` 状态。

四次挥手的示意图如下：

![四次挥手](http://klaus_project.gitee.io/pic/note/tcp-connection-closed-four-way-handshake.png)





![四层模型](http://klaus_project.gitee.io/pic/note/20170328082811398.jfif)





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



[官方文档]: https://dubbo.apache.org/zh-cn/	"官方文档"
[dubbo源码]: https://github.com/apache/dubbo	"dubbo源码"
[dubbo ops]: https://www.cnblogs.com/zjfjava/p/9694540.html



[几种协议的使用场景]: https://blog.csdn.net/lhx13636332274/article/details/73740960