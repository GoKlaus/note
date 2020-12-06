[toc]

# 1、基本概念

## Producer

生产者，也就是发送消息的一方。生产者负责创建消息，然后将其投递到Kafka中

## Broker

服务代理节点

## Consumer

消费者，也就是接收消息的一方。消费者连接到Kafka上并接收消息，进而进行相应的业务逻辑处理

Consumer 

ConsumerGroup

消费组是一个逻辑上的概念，将旗下的消费者归于一类

规则：

```
default -> 每一个分区只能被一个消费组中的一个消费者所消费， 消费者可以消费多个分区，但一个分区只能有同一个分组里的一个消费者，不能多个
消费者多于分区，就会有消费者没有分到分区

customization -> 可以配置客户端策略 
```







## Zookeeper





## Topic

主题是逻辑上的概念，主题分为多个分区，一个分区只属于单个主题，也称为主题分区（`Topic-Partitiion`）

主题可以跨分区

分区规则，决定消息被发送到哪个分区

分区可以分布在不同Broker上



## Partition

Topic-Partitiion





## 多副本机制

目的：故障转移，容灾能力，高可用

|          | 角色 | 能力 |
| -------- | ---- | ---- |
| leader   | 主   |      |
| follower | 从   |      |
|          |      |      |



## AR（Assigned Replicas）

分区中所有的副本 = AR

AR=ISR+OSR

二者的区别在于：保持一定程度的同步，保持的是ISR，落后的是OSR

这个一定程度可以通过参数设置

ISR OSR里的副本是流转的

ISR ------> OSR 没保持住一定程度

OSR-------> ISR 赶上了一定程度



leader选举区别

默认情况：leader故障，新leader从ISR中重新选出

可通过配置允许OSR中副本竞选



### ISR（In-Sync Replicas）

ISR包括leader和其他保持了一定程度的同步的副本

### OSR（Out-of-Sync Replicas）



## HW

High Watermark 俗称高水位，是一个offset



## LEO

Log End Offset 标识当前日志文件中下一条待写入消息的offset



HW 和 LEO都是offset

HW 决定可读的offset范围

LEO决定下次写入leader的offset



## 消息投递的方式

### P2P

点对点模式是基于队列的

表现形式：消息生产发送到队列，消息消费者从队列中接收消息



### PUB/SUB

发布/订阅 定义了如何向一个内容节点发布和订阅消息，内容节点被称为主题（Topic）





kafka同时支持两种消息投递模式，如何实现的：

1. 同一消费组的，消息均衡投递给所有的消费者，一个消息被一个消费者消费
2. 不通消费组的，同一消息会被所有消费者处理



