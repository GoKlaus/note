# redis基础

[toc]



[掘金--redis基础--敖丙]( https://juejin.im/post/5db69365518825645656c0de )



传统的关系型数据库如Mysql已经不能适用所有的场景了，比如秒杀的库存扣减，APP首页的访问流量高峰等等，都很容易把数据库打崩，所以引入了缓存中间件，目前市面上比较常用的缓存中间件有 **Redis** 和 **Memcached** 不过中和考虑了他们的优缺点，最后选择了Redis。



![img]( http://klaus_project.gitee.io/pic/note/16e43d17b5ad429a)

**Redis**采用的是基于内存的采用的是单进程单线程模型的 KV 数据库，由C语言编写，官方提供的数据是可以达到100000+的**QPS（每秒内查询次数）**。

- 完全基于内存，绝大部分请求是纯粹的内存操作，非常快速。它的，数据存在内存中，类似于**HashMap**，**HashMap**的优势就是查找和操作的时间复杂度都是O(1)；
- 数据结构简单，对数据操作也简单，**Redis**中的数据结构是专门进行设计的；
- 采用单线程，避免了不必要的上下文切换和竞争条件，也不存在多进程或者多线程导致的切换而消耗 **CPU**，不用去考虑各种锁的问题，不存在加锁释放锁操作，没有因为可能出现死锁而导致的性能消耗；
- 使用多路I/O复用模型，非阻塞IO；
- 使用底层模型不同，它们之间底层实现方式以及与客户端之间通信的应用协议不一样，**Redis**直接自己构建了VM 机制 ，因为一般的系统调用系统函数的话，会浪费一定的时间去移动和请求；

## 数据结构

### String

简单get set

```
set college szu
```



### Hash

类似对象的一种结构

一个对象（前提是**这个对象没嵌套其他的对象**）给缓存在 redis 里，然后每次读写缓存的时候，可以就操作 hash 里的**某个字段**。

```
hset person name bingo
hset person age 20
hset person id 1
hget person name

```

```
person = {
    "name": "bingo",
    "age": 20,
    "id": 1
}
```





### List 

有序列表

比如可以通过 list 存储一些列表型的数据结构，类似粉丝列表、文章的评论列表之类的东西。

比如可以通过 lrange 命令，读取某个闭区间内的元素，可以基于 list 实现分页查询，这个是很棒的一个功能，基于 redis 实现简单的高性能分页，可以做类似微博那种下拉不断分页的东西，性能高，就一页一页走。

```
lpush mylist 1
lpush mylist 2
lpush mylist 3 4 5

# 1
rpop mylist
```



### Set  

set 是无序集合，自动去重。

直接基于 set 将系统里需要去重的数据扔进去，自动就给去重了，如果你需要对一些数据进行快速的全局去重，你当然也可以基于 jvm 内存里的 HashSet 进行去重，但是如果你的某个系统部署在多台机器上呢？得基于 redis 进行全局的 set 去重。

可以基于 set 交集、并集、差集的操作，比如交集吧，可以把两个人的粉丝列表整一个交集，看看俩人的共同好友是谁？对吧。

把两个大 V 的粉丝都放在两个 set 中，对两个 set 做交集。



```

```



```
#-------操作一个set-------
# 添加元素
sadd mySet 1

# 查看全部元素
smembers mySet

# 判断是否包含某个值
sismember mySet 3

# 删除某个/些元素
srem mySet 1
srem mySet 2 4

# 查看元素个数
scard mySet

# 随机删除一个元素
spop mySet

#-------操作多个set-------
# 将一个set的元素移动到另外一个set
smove yourSet mySet 2

# 求两set的交集
sinter yourSet mySet

# 求两set的并集
sunion yourSet mySet

# 求在yourSet中而不在mySet中的元素
sdiff yourSet mySet
```

### Sorted Set

sorted set 是排序的 set，去重但可以排序，写进去的时候给一个分数，自动根据分数排序。

```
zadd board 85 zhangsan
zadd board 72 lisi
zadd board 96 wangwu
zadd board 63 zhaoliu

# 获取排名前三的用户（默认是升序，所以需要 rev 改为降序）
zrevrange board 0 3

# 获取某用户的排名
zrank board zhaoliu
```



疑问：每种数据结构的适合的应用场景？



看资料发现还有新的结构  ？

关键词 ：

HyperLogLog  

 Geo 

 Pub/Sub

BloomFilter

RedisSearch

Redis-ML









## 缓存穿透

缓存穿透是指缓存和数据库中都没有的数据，而用户不断发起请求，我们数据库的 id 都是1开始自增上去的，如发起为id值为 -1 的数据或 id 为特别大不存在的数据。这时的用户很可能是攻击者，攻击会导致数据库压力过大，严重会击垮数据库。

这种查询不存在数据的现象称作 **缓存穿透**



## 持久化

因为**Redis**数据在内存的特性，持久化必须得有

- RDB：**RDB** 持久化机制，是对 **Redis** 中的数据执行**周期性**的持久化。
- AOF：**AOF** 机制对每条写入命令作为日志，以 **append-only** 的模式写入一个日志文件中，因为这个模式是只追加的方式，所以没有任何磁盘寻址的开销，所以很快，有点像Mysql中的**binlog**。
- 可以同时使用RDB和AOF，AOF的保存的数据集通常比RDB保存的数据集更完整

**RDB**更适合做**冷备**，**AOF**更适合做**热备**



### 各自优缺点

#### RDB

==优点：==

1. 适合用来备份数据
2. 适合用来灾难恢复
3. 可以最大化Redis性能：父进程在保存 RDB 文件时唯一要做的就是 `fork` 出一个子进程，然后这个子进程就会处理接下来的所有保存工作，父进程无须执行任何磁盘 I/O 操作
4. RDB 在恢复大数据集时的速度比 AOF 的恢复速度要快

RDB恢复大数据集时数据快的原因是

==缺点：==

1. **RDB**都是快照文件，都是默认五分钟甚至更久的时间才会生成一次，服务宕机，数据丢失。**AOF**则最多丢一秒的数据，**数据完整性**更好
2. **RDB**在生成数据快照的时候，如果文件很大，客户端可能会暂停几毫秒甚至几秒，你公司在做秒杀的时候他刚好在这个时候**fork**了一个子进程去生成一个大快照，哦豁，出大问题。

#### AOF

==优点：==

1. 灵活设置fsync时间间隔，默认一秒，最多损失数据就是设置时间间隔内的数据
2. **AOF**在对日志文件进行操作的时候是以`append-only`的方式去写的，只是追加的方式写数据，自然就少了很多磁盘寻址的开销了，写入性能惊人，文件也不容易破损。
3. 记录完整写入操作，**AOF**的日志是通过一个叫**非常可读**的方式记录的，这样的特性就适合做**灾难性数据误删除**的紧急恢复了，比如公司的实习生通过**flushall**清空了所有的数据，只要这个时候后台重写还没发生，你马上拷贝一份**AOF**日志文件，把最后一条**flushall**命令删了就完事了。
4. Redis 可以在 AOF 文件体积变得过大时，自动地在后台对 AOF 进行重写

==缺点：==

1. 相同数据集，**AOF**文件通常比**RDB**文件体积大。
2. **AOF**开启后，**Redis**支持写的**QPS**会比**RDB**支持写的要低，他不是每秒都要去异步刷新一次日志**fsync**，当然即使这样性能还是很高，**ElasticSearch**也是这样的，异步刷新缓存区的数据去持久化，为啥这么做呢，不直接来一条怼一条呢，那我会告诉你这样性能可能低到没办法用的，大家可以思考下为啥哟。

## 效率

redis 单线程模型效率高：

1. 纯内存操作
2. 核心是基于非阻塞的IO多路复用机制
3. C语言实现，一般来说，C语言实现的程序“距离”操作系统更近
4. 单线程反而避免了多线程的频繁上下文切换问题，预防了多线程可能产生的竞争问题

## 与memcached比较

### 数据结构

- redis拥有更多的数据结构，能支持更丰富的数据操作如果需要缓存能够支持更复杂的结构和操作选用redis
- memcached只支持string

### 集群模式

在 redis3.x 版本中，便能支持 cluster 模式，而 memcached 没有原生的集群模式，需要依靠客户端来实现往集群中分片写入数据。

#### 性能对比

由于 redis 只使用**单核**，而 memcached 可以使用**多核**，所以平均每一个核上 redis 在存储小数据时比 memcached 性能更高。而在 100k 以上的数据中，memcached 性能要高于 redis。虽然 redis 最近也在存储大数据的性能上进行优化，但是比起 memcached，还是稍有逊色。



# redis模式

## 单机模式



## 主从模式

1. 默认配置，master节点可以进行读和写，slave只能进行读操作（readonly）
2. 不要修改配置让slave节点支持写操作，无意义，原因一，写入的数据不会被同步到其他节点;原因二，当master节点修改同一条数据后，slave节点的数据会被覆盖掉
3. slave状态不影响其他slave节点的读和master节点的读和写，重新启动后将从master节点同步过来
4. 这种模式下，master节点挂了，slave不会竞选成为master，不会影响slave的读，但是不会提供写服务，master节点启动之后才会重新提供写服务
5. master节点设置密码时
   客户端访问master需要密码
   slave启动需要密码，在配置中进行配置即可
   客户端访问slave不需要密码



客户端之续哟啊配置一个密码参数，redis配置文件配置两个参数

```conf
masterauth "masterauthword"

requirepass "password"
```

客户端配置文件

```
jedis-cluster.password=password
```

### 缺点

master挂掉对外无法提供写服务，生产环境不能停止服务，所以一般生产环境不会单单只有主从模式的，可以配合sentinel哨兵模式使用

## Sentinel（哨兵）模式

主从模式中，master节点挂了之后，slave不能主动选举一个master节点出来，安排一个或多个sentinel来做这件事，当sentinel发现master节点挂了以后，sentinel会**从slave中选举一个master**



1. sentinel模式建立在主从模式的基础上，如果只有一个redis节点，sentinel就没有任何意义
2. 当master节点挂了之后，sentinel会从slave中选举一个作为master，并且修改他们的配置文件，其他的slave配置文件也会被修改，比如slaveof属性就会指向新的master
3. 当master节点重新启动后，将不再是master，而是作为slave接收心的master节点的同步数据
4. sentinel因为也是一个进程有挂掉的可能，所以sentinel也会启动多个形成一个sentinel集群
5. 主从模式配置的密码，sentinel会同步将配置信息修改到配置文件中，不需要担心
6. 一个sentinel或sentinel集群可以管理多个主从redis
7. sentinel最好不要和redis部署在同意台机器，redis服务器宕机，sentinel也胡宕机
8. sentinel监控redis集群都会定义一个master名字，这个名字代表redis集群的master redis





使用sentinel模式的时候，客户端不要直接连接redis，而是直接连接sentinel的ip和port，由sentinel来提供具体可提供服务的redis实现，当master节点挂掉后，sentinel就会感知并将心的master节点提供给使用者



sentinel本身支持集群，单节点sentinel是不可靠的：

1. 单点sentinel，如果出现进程运行出错，或者网络阻塞，将无法实现redis集群的主备切换（单点问题）
2. 如果有多个sentinel，redis的客户端可以随意连接一个sentinel来获取关于redis集群中的信息
3. sentinel本身需要多数机制，也就是2个sentinel进程时，挂掉一个另一个就不可用了

### sentinel集群

sentinel集群不需要设置其他的sentinel地址，sentinel进程可以通过发布与订阅来自动发现正在监视相同主实例的其他sentinel。当一个sentinel发现一个新的sentinel时，会将新的sentinel添加到一个列表中，这个列表保存了sentinel已知的，监视同一个主服务器的所有其他sentinel



sentinel集群中的sentinel不会同一时刻并发去failover（故障切换or故障转移）同一个master，第一个进行failover的sentinel如果失败了（failover-timeout），另一个才会去重新failover



当Sentinel将一个slave选举为master并发送SLAVE OF NO ONE后，即使其它的slave还没针对新master重新配置自己，failover也被认为是成功了



上述过度过程中，若此时重启old master，则redis集群将处于无master状态，此时只能手动修改配置文件，然后重新启动集群.（生产情况下千万不要做如此愚蠢的操作，否则你会导致整个应用集群都启动失败。）

　　Master-Slave切换后，Sentinel会改写master，slave和sentinel的conf配置文件。

　　一旦一个Sentinel成功地对一个master进行了failover，它将会把关于master的最新配置通过广播形式通知其它sentinel，其它的Sentinel则更新对应master的配置。



## Cluster（集群）模式

本人所在项目组使用的cluster模式，项目在生产环境有8个Redis集群，每个集群的dbsize都在千万级。这种数据量显然不是哨兵模式可以满足的。

　　cluster的出现是为了解决单机Redis容量有限的问题，将Redis的数据根据一定的规则分配到多台机器。对cluster的一些理解：

　　一个 Redis 集群包含 16384 个哈希槽（hash slot），数据库中的每个键都属于这 16384 个哈希槽的其中一个，集群中的每个节点负责处理一部分哈希槽。

　　例如一个集群有三个主节点，其中：

　　节点 A 负责处理 0 号至 5500 号哈希槽。

　　节点 B 负责处理 5501 号至 11000 号哈希槽。

　　节点 C 负责处理 11001 号至 16384 号哈希槽。

　　这种将哈希槽分布到不同节点的做法使得用户可以很容易地向集群中添加或者删除节点。例如：如果用户将新节点 D 添加到集群中， 那么集群只需要将节点 A 、B 、 C 中的某些槽移动到节点 D 就可以了。

　　如果用户要从集群中移除节点 A ， 那么集群只需要将节点 A 中的所有哈希槽移动到节点 B 和节点 C ， 然后再移除空白（不包含任何哈希槽）的节点 A 就可以了。

　　这里需要注意的是，集群如果是5主5从，主节点也是16384个hash slot，而不会因为主节点的增多slot也增多。我们在分槽的时候，尽量把槽平均分给主节点。因为一个key落在哪个槽里面，是根据key的CRC16值模上16384得出的值来计算的。

　　2.Redis 集群对节点使用了主从复制功能： 集群中的每个节点都有 1 个至 N 个复制品（replica）， 其中一个复制品为主节点（master）， 而其余的 N-1 个复制品为从节点（slave）。

　　我们知道集群模式下，1主N从时，当主节点挂掉时，从节点通过心跳监听机制，会竞选成为主节点（这时设置的readonly会失效），所以在部署的时候，主从节点应该部署在不同的机器上，这个时候如果主节点的服务器宕机，从节点竞选成功后会继续承担读写的任务。

　　3.Redis 集群的节点间通过Gossip协议通信。

　　4.当前Redis集群不支持NAT环境或者IP，端口重新映射的环境。

　　cluster这种模式适合数据量巨大的缓存要求，当数据量不是很大使用sentinel即可。



# 事件驱动机制

涉及概念

- 事件定义

与消息驱动机制比较

1. 耦合高
2. 同模块好用

消息驱动机制

1. 耦合低
2. 跨模块好用



Redis中实现一个非常简洁的事件驱动库ae_event，只关注网络IO，以及定时器



该事件库处理两类事件

- 文件事件（file event）：用于处理Redis服务器和客户端之间的网络IO
- 时间事件（time event）：Redis服务器中的一些操作需要在给定的时间点执行，而时间事件就是吹了这类定时操作的



## 文件事件







# I/O多路复用技术

Redis是单线程的，如果操作都是顺序线性执行，一次I/O的执行会对后续造成影响，某次操作的I/O阻塞会导致整个进程无法对其他客户提供服务

I/O多路复用解决了

1. 解决线性操作，一次操作阻塞，导致后续客户端通行阻塞问题
2. 不需要进行线程切换，效率的提升，线程切换需要切换到内核，需要消耗时间和资源

其实多线程编辑和处理上比I/O多路复用简单，而I/O多路复用处理起来较为复杂。



处理逻辑，是怎么处理？

I/O 多路复用其实是在单个线程中通过记录跟踪每一个sock（I/O流） 的状态来管理多个I/O流。结合下图可以清晰地理解I/O多路复用



select, poll, epoll 都是I/O多路复用的具体的实现。epoll性能比其他几者要好。redis中的I/O多路复用的所有功能通过包装常见的select、epoll、evport和kqueue这些I/O多路复用函数库来实现的



# SETNX

set if not exists



主从



哨兵



集群