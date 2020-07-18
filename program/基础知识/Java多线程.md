[TOC]



# 线程安全的定义

当多个线程同时访问一个对象时，如果不用考虑这些线程在运行时环境下的调度和交替执行，也不需要进行额外的同步，或者在调用方进行任何其他的协调操作，调用这个对象的行为都可以获得正确的结果，那就称这个对象是线程安全的

----- `Brian Goetz 《Java并发编程实战（Java Concurrency In Practice）》`



# Java的多线程技能

不共享数据，每个线程内有自己的变量数据，其他线程不可见

共享数据，多个线程可以访问同一个变量



`synchoronized`关键字:可以用在任意对象和方法上，加锁的代码称作“互斥区”或“临界区”



线程规划器 



非线程安全问题：多个线程对同一个实例变量操作出现值被修改，值不同步的问题



两个方法的区别：

```java
public static boolean interrupted();
//静态方法，表示当前线程，在main方法调用，代表main的状态，另外线程代表另外线程
//第二次调用清除中断状态

public boolean isInterruppted();
//成员方法，那个对象调用，代表那个对象
```



异常法 中断线程



stop()方法  暴力停止，会抛出`TheadDeath`异常，不需要显示捕捉



stop()已经作废，   暴力强制停止有可能使一些清理性的工作得不到完成，另外对锁定的对象进行了“解锁”，导致数据得不到同步处理，出现数据 不一致的问题



isAlive()  检测线程是否处于活动状态（线程已经启动且尚未终止。线程正在运行或准备开始运行的状态）



==使用isAlive()使用时，作为构造参数传递给Thread对象进行start()启动时，注意Thread.currentThread()和this的差异==



## 线程的状态

线程的状态5种

**新建（new）、可运行（runable）、运行（running）、阻塞（blocked）、死亡（dead）**

[线程的五种状态详解](https://blog.csdn.net/xingjing1226/article/details/81977129)

![](http://dl.iteye.com/upload/picture/pic/116719/7e76cc17-0ad5-3ff3-954e-1f83463519d1.jpg)



![Java 线程的状态 ](/home/klaus/documents/pic/note/thread-1.png)

## 暂停线程

suspend() 

resume()

suspend()方法会独占锁，造成其他线程无法访问公共同步对象。

## 线程优先级

* 线程优先级的继承特性：在Java中，线程的优先级具有继承性，比如线程A启动线程B线程，则线程B的优先级与A是一样的。
* 优先级具有规则性：线程优先级与代码执行顺序无关，线程优先级具有一定的规则性，CPU尽量将执行资源让给优先级比较高的线程
* 优先级具有随机性：优先级较高的线程不一定每一次都先执行完



Java中有两种线程：

* 用户线程
* 守护线程（Deamon）：在进程中不存在非守护线程了，则守护线程自动销毁。

# 对象及变量的并发访问

”非线程安全“出现在”实例变量中“中，方法内部的私有变量，不存在 ”非线程安全“问题



关键字synchronized取得的都是对象锁，不是一段代码或方法（函数）当作锁：两个线程对同一个对象的操作，加了synchronized关键字，才存在同步锁的意义，如果代码或者方法（函数）当作锁，只要任何一个线程执行这个方法，就会同步，不论是不是操作同一个对象。

### 脏读

读取变量时，此值已经被其他线程更改过了

## synchronized

特性

1. 原子性
2. 可见性
3. 有序性
4. 可重入性

### 原子性

一个操作或者多个操作，要么全部执行并且执行过程不会被任何因素打断，要么就不执行

被synchronized修饰的类或对象的所有操作都是原子的。因为在执行操作之前必须获得对象锁，直到执行结束才释放，中间无法被打断（除了已经被废除的stop()方法），保证了原子性

tips：面试常问synchronized和volatile的区别，------最大区别就是volatile不具备原子性



### 可见性

可见性就是多个线程访问一个资源的时候，这个资源的状态，值信息等对于其他线程都是可见的。

获取到对象锁的状态对其他争夺锁的线程而言是可见的

线程释放锁之前，对数据的修改刷新到主内存中去保证资源变量的可见性

volatile保证可见性是当被修饰的变量数据被修改后，立即更新到主内存中



### 有序性

程序执行的顺序按照代码先后执行，（没有指令重排）



synchronized和volatile都具有有序性，Java允许编译器和处理器对指令进行重排，对单线程而言，没有影响，但是会影响多线程的并发执行顺序，



### synchronized锁可重入

关键字synchronized拥有锁重入的功能，当一个线程得到一个对象锁后，再次请求此对象锁时时可以再次得到该对象的锁的。证明synchronized方法/块的内部调用本类的其他synchronized方法/块时，是永远可以得到锁的

如果不可以重入的话，就会造成死锁

原因：本身已经持有这个对象锁，如果不满足可重入，再次请求这个对象锁的时候，没有可重入特性，会等待这个锁，但同时这个对象锁被自己持有，别的线程无法获得，就产生矛盾，死锁产生（个人理解）

> 若一个程序或子程序可以“在任意时刻被中断然后操作系统调度执行另外一段代码，这段代码又调用了该子程序不会出错”，则称其为可重入（reentrant或re-entrant）的。即当该子程序正在运行时，执行线程可以再次进入并执行它，仍然获得符合设计时预期的结果。与多线程并发执行的线程安全不同，可重入强调对单个线程执行时重新进入同一个子程序仍然是安全的。 --维基百科

可重入的条件：

- 不再函数内使用静态或全局数据
- 不返回静态或全局数据，所有数据都由函数调用者提供
- 使用本地数据（工作内存），或者通过制作全局数据的本地拷贝来保护全局数据
- 不调用不可重入的函数

可重入与线程安全

一般而言，可重入的函数一定是线程安全的，反之，则不一定成立，举个例子：

在不加锁的前提下，一个函数使用了全局或静态变量，那么它不是线程安全的，也不是可重入的，因为通常的枷锁方式是针对不同线程的访问（如Java的synchronized），当同一个线程多次访问就会出现问题。只有当函数满足可重入的四条条件时，才是可重入的



==synchronized是可重入锁==

从设计上讲，一个线程请求其他线程持有对象锁的时候，线程会阻塞。当线程请求自己持有的对象锁的时候，如果该线程是可重入锁，请求就会成功，否则阻塞。

synchronized可重入锁的实现

计数器

计数器为0时，没有线程持有这个对象锁

计数器为1时，说明有线程持有这个对象锁

变化过程： 线程请求到对象锁时，JVM记录持有锁的线程，并将计数器 0 -> 1



## 同步不具有继承性

## synchronized同步语句块

sychronized方法是对当前对象进行加锁

synchronized代码块是对某一个对象进行加锁

## synchronized底层原理

synchronized编译后会生成：

`monitorenter` 和 `monitorexit` 两条指令

`monitorenter`的作用

1. 





### 将任意对象作为对象监视器

* synchronized方法

  ```java
  --对其他synchronized同步方法或synchronized（this）同步代码块调用呈阻塞状态
  --同一时间只有一个线程可以执行synchronized同步方法中的代码
  ```

* synchronized（this）同步代码块

  ```java
  --对其他synchronized同步方法或synchronized（this）同步代码块调用呈阻塞状态
  --同一时间只有一个线程可以只想synchronized（this）同步代码块中的代码
  ```

* synchronized（非this对象x）

  ```java
  --在多个线程持有”对象监视器“为同一个对象的前提下，同一时间只有一个线程可以执行synchronized（非this对象x）同步代码块中的代码
  --当持有”对象监视器“为同一个对象的前提下，同一时间只有一个线程可以执行synchronized（非this对象x）同步代码块中的代码
  ```



不使用String作为对象监视器，因为`jre`常量池的原因




"synchronized（非this对象x）"格式的写法是将x对象本身作为“对象监视器”，可以得到以下3个结论：

```java
--当多个线程同步执行synchronized() {}同步代码块时呈同步效果
--当其他线程执行x对象中synchronized同步方法时呈同步效果
--当其他线程执行x对象里面的synchronized(this)代码块是也是呈现同步效果
```





### 静态同步synchronized方法与synchronized(class)代码块

```java
--synchronized 关键字加到static静态方法上是给class类上锁，非静态方法上是给对象加锁
--synchronized(this)和 synchronized static 一个是对象锁，一个是class锁，class锁对类的所有对象实例起作用  
```



### 多线程的死锁

不同线程等待根本不可能被释放的锁，从而导致所有的任务无法继续完成

JDK自带工具可以检测是否有死锁现象。 jdk/bin/jps  命令    jdk/bin/jstack

避免双方互相持有对方的锁的情况



### 内置类与静态内置类



### 锁对象的改变

多个线程同时持有锁对象，这些线程之间就是同步的，分别获得各自的锁对象，那么之间就是异步的



只要对象不变，即使对象的属性被修改，运行的结果还是同步的。



## volatile关键字

volatile关键字的主要作用是使变量在多个线程间可见



关键字volatile的作用是强制从公共堆栈中取得变量的值，而不是从线程私有数据栈中取得变量的值

volatile关键字和synchronized关键字：

```java
---关键字 volatile 是线程同步的轻量级实现，所以volatile性能肯定比synchronized要好，并且volatile只能修饰变量， synchronized 可以修饰方法、代码块。
---多线程访问 volatile 不会发生阻塞，而 synchronized 会出现阻塞
---volatile 保证数据的可见性，但不能保证原子性 ; 而 synchronized 可以保证原子性，也可以间接保证可见性，因为它会将似有内存和公共内存中的数据做同步
--- 关键字 volatile 解决的是变量在多个变量之间的可见性;而 synchronized 保证的是多个线程之间访问资源的同步性
```



### volatile非原子的特性

volatile  增加了实例变量在多个线程之间的可见性，不具备同步性

volatile关键字解决的是变量读取时的可见性问题，但无法保证原子性，对于多个线程访问同一个实例变量还是需要加锁同步



### 使用原子类操作

原子操作是不能分割的整体，没有其他线程能够中断或检查正在原子操作中的变量，在没有锁的情况下可以做到线程安全



### 原子类也并不完全安全

原子类提供原子的操作，但是方法和方法之间的调用却不是原子的

```java
//只有这个一个是原子的
aiRef.addAndGet(100);
System.out.println(Thread.currentThread.getName())
aiRef.addAndGet(1);
```



### synchronized代码块具有volatile同步的功能

关键字syhchronized可以使多个线程访问同一个资源具有同步性，而且具有将线程工作内存中的私有变量与公共内存中的变量同步的功能

```java
synchronized  两个特征：
---互斥性
---可见性
```

# 锁粗化和锁消除

锁粗化概念：







# 线程间的通信

线程间通信模型有两种：共享内存和消息传递，实现线程间通信都是基于两种模型来实现的

```java
---使用 wait/notify实现线程间的通信
---生产者/消费者模式的实现
---方法join的使用
---ThreadLocal的使用
```

## 等待通信机制

wait()使用前提：线程必须获取到该对象的对象级别锁，只能在同步方法或同步块中调用wait()方法。

执行完notify()方法后，当前线程不会立马释放该对象锁，呈wait状态的线程也并不能立马获取该对象的锁，要等到执行notify()方法的线程将程序执行完，也就是退出synchronized代码后，当前线程才会释放锁。一个获得了对象锁的wait线程执行完后，没有调用notify()语句，即使这个对象已经空闲，其他wait状态等待的线程由于没有受到该对象的通知，还会继续阻塞在wait状态，知道这个对象发出一个notify或notifyAll。

## 生产/消费者模式

### 一生产与一消费：操作值

### 多生产与多消费：操作值-假死



线程有几种实现方式？ 他们的区别是什么？线程池实现原理？JUC并发包？ThreadLocal Lock Synchronize的区别



悲观锁  乐观锁 读写锁 行锁 表锁 自旋锁 死锁 分布式锁 线程同步锁 公平锁 非公平锁 



线程池的优势：

降低资源消耗。复用已创建的线程降低线程创建和销毁的消耗

提高相应速度。任务到达时不需要等到线程创建就能立即执行

提高线程的可管理性。线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控

# 线程池的创建方式

Java通过`Executors（jdk1.5并发包）`提供四种线程池，分别为：
`newCachedThreadPool` 可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程。
`newFixedThreadPool` 创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待。
`newScheduledThreadPool `创建一个定长线程池，支持定时及周期性任务执行。
`newSingleThreadExecutor`创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行。



executor 的关闭方式

通过shutdown  和 shutdowNow 两个方法完成

也可以这样

```JAVA
executor.awaitTermination(5, TimeUnit.SECONDS)
```







# BlockingQueue

四个具体的实现类

1. ArrayBlockingQueue：数组阻塞队列，==**规定大小**==， 其构造函数必须带一个int参数来指明大小。顺序是FIFO先入先出来排序的
2. LinkedBlockingQueue：链阻塞队列，大小不固定，若其构造函数带一个规定大小的参数，生成的BlockingQueue有大小限制，若不带大小参数，所生成的BlockingQueue大小由Integer.MAX_VALUE来决定。FIFO
3. PriorityBlockingQueue：类似于LinkedBlockingQueue，但其所含对象的排序不是FIFO，而是依据对象的自然排序或者是构造函数所带的Comparator决定顺序
4. SynchronousQueue：特殊的BlockingQueue，他的内部同时只能够容纳单个元素，对其操作必须是放和取交替完成的。
5. DelayQueue：延迟队列，注入其中的元素必须实现java.util.concurrent.Delayed接口





# Callable

ExecutorService.submit 可以来执行这个接口

底层的还是使用Runable吗？



并行流底层还是Fork/Join框架，只是任务拆分优化得很好。

```java
Instant start = Instant.now();
        long result = LongStream.rangeClosed(0, 10000000L).parallel().reduce(0, Long::sum);
        Instant end = Instant.now();
        System.out.println("耗时：" + Duration.between(start, end).toMillis() + "ms");

        System.out.println("结果为：" + result);
```

耗时效率方面解释：Fork/Join 并行流等当计算的数字非常大的时候，优势才能体现出来。计算比较小，或者不是CPU密集型的任务，不建议使用并行处理

fork()：开启一个新线程（或是重用线程池内的空闲线程），将任务交给该线程处理。
join()：等待该任务的处理线程处理完毕，获得返回值

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617160144126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzM3NTQyODg5,size_16,color_FFFFFF,t_70)



Fork/join Fremework 底层使用到了work stealing 算法

那么什么是work stealing 算法



并发的学习，离不开三个概念，进程，线程，还有纤程



一个单核心的cpu，无论何时都是只有一个线程在运行，体现出多线程在运行的现象是因为时间切片的存在，cpu不会空闲

IPC（Inter Process Communication) resource 