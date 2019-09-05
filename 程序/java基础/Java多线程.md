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

### synchronized锁重入

关键字synchronized拥有锁重入的功能，当一个线程得到一个对象锁后，再次请求此对象锁时时可以再次得到该对象的锁的。证明synchronized方法/块的内部调用本类的其他synchronized方法/块时，是永远可以得到锁的

如果不可以重入的话，就会造成死锁

### 同步不具有继承性

## synchronized同步语句块

sychronized方法是对当前对象进行加锁，synchronized代码块是对某一个对象进行加锁



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



不是使用String作为对象监视器，因为jre常量池的原因




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