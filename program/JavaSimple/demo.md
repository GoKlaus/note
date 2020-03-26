[TOC]

# 5/12

## transient关键字

### 补充：

### 1、序列化和反序列化

​			==Java序列化是指把Java对象转换为字节序列的过程；而Java反序列化是指把字节序列恢复为Java对象的过程。从而达到网络传输、本地存储的效果。==

​		序列化（Serialization）是将对象的状态信息转化为可以存储或者传输的形式的过程，一般将一个对象存储到一个储存媒介，例如档案或记忆体缓冲等，在网络传输过程中，可以是字节或者XML等格式；而字节或者XML格式的可以还原成完全相等的对象，这个相反的过程又称为反序列化；

### 2、java对象的序列化和反序列化

​		java中创建好了的对象，只要没有被回收都可以反复使用此对象。但是，这些对象都是存储在jvm的堆中(stack)，只有jvm在运行的时候这些对象才是存在的，jvm停止这些对象也就随之消失。在真实场景中，需要将这些对象持久化下来，并且在需要的时候将对象重新读取出来，java的序列化可以帮助实现此功能。

​		java的序列化机制(java serialization)是java语言内建的一种对象持久化方式，通过序列化，可以将对象的状态信息保存在字节数组，并且在有需要的时候将这个字节数组通过反序列化的方式转化成对象 ，对象的序列化可以很容易的在jvm中的活动对象和字节数组(流)之间进行转换，java中对象的序列化和和反序列化被广泛的应用到RMI(远程方法调用)及网络传输中

## RPC

Remote Procedure Call --远程过程调用，被设计为在应用程序间通信的中立方式，它不理会操作系统以及语言之间的差异。即RPC支持多种语言，RMI只支持java写的应用程序

## RMI补充

```
RPC, Remote Procedure Call 即远程过程调用。见名知意：从远程主机调用一个过程/函数。

	RPC 的目标是：使得本程序调用其它远程主机上的函数，好像调用本程序内的函数一样简单，并且屏蔽编程语言的差异性。

	要实现上述目标首先需要设计一种通信协议，这被称为：RPC协议(RPC Protocol)

RPC协议 不是某一个具体的协议，而是一个类型名，代表一类用作RPC的协议。RPC协议是在网络应用层协议，广义上可以跨越平台、语言进行应用间通讯（说广义是因为可以开发一个协议但只支持单个语言）
是否RMI是RPC的一种


```



​		RMI(Remote Mothod Invocation)--调用远程对象方法，允许返回java对象以及基本数据类型。而RPC不支持对象的概念，传送到RPC服务的消息由外部数据表示(External Data Representation，XDR)语言表示，这种语言抽象了字节序类和数据结构之间的差异。只有有==XDR定义的数据类型才能被传递==，RPC不允许传递对象。可以说RMI是面向对象的RPC。

​		RPC和RMI之间的最主要区别在于方法是如何被调用的。在RMI中，远程接口使每个远程方法都具有方法签名。如果一个方法在服务器上执行，但是没有相匹配的签名被添加到这个远程接口上，那么这个新的方法就不能被RMI客户方所调用。

​		RPC中，当一个请求到达RPC服务器时，这个请求就包含了一个参数集和一个文本值，通常形成classname.methodname的形式。这就向RPC服务器表明，被请求的方法在为classname的类中，名叫methodname。然后RPC就去搜索与之相匹配的类和方法，并把它作为那种方法参数类型的输入。这里的参数类型是与RPC请求中的类型是相匹配的，一旦匹配成功，这个方法就被调用了，其结果被编码后返回客户方。

​		分布式计算系统要求运行在不同主机上的对象相互调用。各种分布式系统都有自己的调用协议，如CORBA的IIOP(Internet InterORB Protocol)，MTS的DCOM。EJB的组件--java中提供了完整的socket通讯接口，但socket要求客户端和服务端必须进行应用级协议的编码交换数据，所以采用socket相较而言比较麻烦。

​		RPC可以代替socket，抽象出通讯接口用于过程调用，使得编程者调用一个远程过程和一个本地过程同样方便。RPC系统采用XDR来编码远程调用的参数和返回值。

​		RPC不支持对象，而EJB构造的是完全面向对象的分布式系统，所以面向对象的远程调用RMI(Remote Method Invocation)。RMI是采用JRMP(Java Remote Method Protocol)通讯协议，是构建在TCP/IP协议上的一种远程调用方法。

==总结：==

|          | RPC(Remote Procedure Call) | RMI(Remote Mothod Invocation)             |
| -------- | -------------------------- | ----------------------------------------- |
|          | 远程过程调用               | 调用远程对象方法                          |
| 支持对象 | 不支持                     | 支持                                      |
| 采用协议 |                            | JRMP(Java Remote Method Protocol)通讯协议 |
| 支持语言 | 跨语言，平台               | java                                      |
|          |                            |                                           |
|          |                            |                                           |
|          |                            |                                           |
|          |                            |                                           |
|          |                            |                                           |



dubbo共支持如下几种通信协议：

- [dubbo://](http://dubbo.io/User+Guide-zh.htm#UserGuide-zh-dubbo%3A%2F%2F)
- [rmi://](http://dubbo.io/User+Guide-zh.htm#UserGuide-zh-rmi%3A%2F%2F)
- [hessian://](http://dubbo.io/User+Guide-zh.htm#UserGuide-zh-hessian%3A%2F%2F)
- [http://](http://dubbo.io/User+Guide-zh.htm#UserGuide-zh-http%3A%2F%2F)
- [webservice://](http://dubbo.io/User+Guide-zh.htm#UserGuide-zh-webservice%3A%2F%2F)
- [thrift://](http://dubbo.io/User+Guide-zh.htm#UserGuide-zh-thrift%3A%2F%2F)
- [memcached://](http://dubbo.io/User+Guide-zh.htm#UserGuide-zh-memcached%3A%2F%2F)
- [redis://](http://dubbo.io/User+Guide-zh.htm#UserGuide-zh-redis%3A%2F%2F)









### 3、序列化及反序列化相关接口及类

```java
java.io.Serializable;
java.io.Externalizable;
```

#### Serializable和Externalizable

不采用第三方工具包来完成序列化的情形下讨论：

==要实现java对象的序列化和反序列化，通过实现Serializable和Externalizable接口即可==。



### JDK8 关于Serializable接口

serializable接口是一个标记接口，没有任何方法和字段，仅用于标识可串行化的语义，不实现此接口的类将不会使任何状态序列化或反序列化。可序列化的子类型都是可序列化的。



为了允许序列化不可序列化的子类型，子类型可能承担保存和回复超类型的公共，受保护和(如果可访问)包字段的状态的责任，只有当他扩展的类具有可访问的无参构造函数来初始化类的状态。如果不是这样，声明一个类Serializable是一个错误。错误将在运行时检测到。

```
对这里的这段话不太理解：序列化不可序列化的子类型，子类型可能承担保存和回复超类型的公共，受保护和(如果可访问)包字段的状态的责任
```

在反序列化期间，非可序列化类的字段将使用该类的public和protected no-arg构造函数进行初始化。对于可序列化的子类，必须可以访问no-arg函数。可序列化子类的字段将从流中回复。











在序列化和反序列化过程中需要特殊处理的类必须采用具有这些精确签名的特殊方法：

```java
private void writeObject(java.io.ObjectOutputStream out) throw IOException;
private void readObject(java.io.ObjectInputStream in) throw IOException,ClassNotFoundException;
private void readObjectNoData() throw ObjectStreamExcepiton;
```

writeObject方法负责为特定的类编写类的状态，以便相应的readObject方法可以恢复它。可以通过调用out.defaultWriteObject来调用保存对象字段的默认机制。该方法不需要关注其超类或者子类的状态。通过writeObject或者通过使用DataOutput支持的原始数据类型将各个字段写入ObjectOutputStream来保存状态。





## 1、transient的作用和用法

​		java对象只要实现了Serializable接口，这个对象就可以被序列化，java的这种序列化模式为开发者提供了很多便利，我们可以不必关心具体序列化的过程，只要这个类实现了Serializable接口，这个类的所有属性和方法都会自动序列化。

​		实际中，会有部分属性需要序列化，其他属性不需要序列化，例如用户的敏感信息(身份证，银行卡号)，为了安全起见，不希望在网络操作(主要涉及到序列化操作，本地序列化缓存 也适用)中被传输，就可以使用transient关键字。即，这个字段的生命周期仅存于调用者的内存中而不会写到磁盘里被持久化。

​		 总之，java 的transient关键字为我们提供了便利，你只需要实现Serilizable接口，将不需要序列化的属性前添加关键字transient，序列化对象的时候，这个属性就不会序列化到指定的目的地中。

```
总结：
声明属性不会被序列化
```

## 2、 transient使用小结

1）一旦变量被transient修饰，变量将不再是对象持久化的一部分，该变量内容在序列化后无法获得访问。

2）transient关键字==只能修饰变量，而不能修饰方法和类==。注意，本地变量是不能被transient关键字修饰的。变量如果是用户自定义类变量，则该类需要实现Serializable接口。

3）被transient关键字修饰的变量不再能被序列化，==一个静态变量不管是否被transient修饰，均不能被序列化==

```
总结：
1、static修饰(静态变量)变量，本身就不能被序列化--可以看做static默认带有transient修饰
2、
```

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

/**
 * @description 使用transient关键字不序列化某个变量
 *        注意读取的时候，读取数据的顺序一定要和存放数据的顺序保持一致
 *        
 * @author Alexia
 * @date  2013-10-15
 */
public class TransientTest {
    
    public static void main(String[] args) {
        
        User user = new User();
        user.setUsername("Alexia");
        user.setPasswd("123456");
        
        System.out.println("read before Serializable: ");
        System.out.println("username: " + user.getUsername());
        System.err.println("password: " + user.getPasswd());
        
        try {
            ObjectOutputStream os = new ObjectOutputStream(
                    new FileOutputStream("C:/user.txt"));
            os.writeObject(user); // 将User对象写进文件
            os.flush();
            os.close();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        try {
            // 在反序列化之前改变username的值
            User.username = "jmwang";
            
            ObjectInputStream is = new ObjectInputStream(new FileInputStream(
                    "C:/user.txt"));
            user = (User) is.readObject(); // 从流中读取User的数据
            is.close();
            
            System.out.println("\nread after Serializable: ");
            System.out.println("username: " + user.getUsername());
            System.err.println("password: " + user.getPasswd());
            
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

class User implements Serializable {
    private static final long serialVersionUID = 8294180014912103005L;  
    
    public static String username;
    private transient String passwd;
    
    public String getUsername() {
        return username;
    }
    
    public void setUsername(String username) {
        this.username = username;
    }
    
    public String getPasswd() {
        return passwd;
    }
    
    public void setPasswd(String passwd) {
        this.passwd = passwd;
    }

}
```





# 5/23

## 如何减少开发中的bug

bug是不可避免的，开发中应该遵循一套原则来尽量避免明显的， 不该出现的

### 2/8原则

80%的代码用来处理异常情况，如果代码的异常逻辑很少，说明代码不完善。
80%的时间思考

### 2个技巧 

防御性编程
不相信任何人的代码，检查所有输入和返回值，处理所有异常
代码写三遍
第一遍将逻辑写通
第二遍完善代码：检查是否遗漏的异常没有处理，是否有的地方日志没有加，是否不符合编程规范
第三遍优化代码：逻辑是否可以优化，某些处理是否可以用更好的方式

### 三个条件

熟悉编程语言
单元测试
熟悉业务



# 5/27

Java程序中可以用来新建对象的方式：

* new语句
* 反射机制
* Object.clone方法
* 反序列化
* Unsafe.allocateInstance方法

其中，Object.clone方法和反序列化通过复制现有的数据，来初始化对象

Unsafe.allocateInstance方法则没有初始化实例字段，而new语句和反射机制是调用构造器来初始化实例手段



# 压缩指针技术

在Java虚拟机中，每一个对象都有一个对象头，它由标记字段和类型指针所构成。标记字段用以存储Java虚拟机有关该对象的运行数据，如哈希码、GC信息及锁信息，而类型指针则指向该类型的类。在64位的JVM中，对象头的标记字段占64位，而类型指针又占了64位。也就是说每一个java对象在内存中的额外开销就是16个字节。

为了减少对象的内存使用量，64位JVM引入了压缩指针的概念，将堆中原本64位的Java对象指针压缩成32位的，对象头中的类型指针也会被压缩成32位，使得对象头的大小从16字节下降到12字节。

压缩指针不仅可以作用于对象头的类型指针，也可以作用于引用类型的字段，以及引用类型的数组。

**压缩指针技术原理：内存对齐**

默认情况下，JVM中对象的起始位置需要对齐至8的倍数，如果一个对象用不到8N字节，那么空白的那部分空间就浪费掉了，这些浪费掉的空间我们称之为对象间的填充。

指针里面存放的是地址，由于堆中对象的起始地址是对齐8的倍数，所以指针存放一个引用(或者对象的类)的内存地址时，根本就不用存放最后的三位二进制数。

因为所有的对象或类的内存地址都对齐了8，所以他们的内存地址的最低三位总是000，32位的指针就可以寻址到2的35次方个字节，也就是32GB的地址空间(超过32GB则会关闭压缩指针)。

可以通过配置虚拟机的内存对齐选项来进一步提升寻址范围，但是，同时也可能增加对象间填充，导致压缩指针没有达到原本节省空间的效果。

就算关闭了压缩指针，Java虚拟机还是会进行内存对齐。此外，内存对齐不仅存在于对象与对象之间，也存在于对象中的字段之间。比如Java虚拟机要求long字段，double字段，以及非压缩指针状态下的引用字段地址为8的倍数。原因是：CPU的缓存机制，如果字段不是对齐的，那么久有可能出现跨缓存行的字段，该字段的读取可能需要替换两个缓存行，而该字段的存储也会同时污染两个缓存行。

## 字段重排列技术

对象的字段之间存在的内存对齐：指的是重新分配字段的先后顺序，以达到内存对齐的目的。

有以下连个规则：

* 如果一个字段占据C个字节，那么字段的偏移量需要对齐至NC。这里的偏移量，指的是字段地址与对象的起始地址差值
* 子类所继承的字段的偏移量，需要与父类对应字段偏移量保持一致



## 虚共享

假设两个线程分别访问同一对象中不同的 volatile 字段，逻辑上它们并没有共享内容，因此不需要同步。

如果这两个字段恰好在同一个缓存行中，那么对这些字段的写操作会导致缓存行的写回，也就造成了实质上的共享。

Java8还引入了一个新的注释@Contended，用来解决对象字段之间的虚共享。

Java 虚拟机会让不同的@Contended字段处于独立的缓存行中，因此你会看到大量的空间被浪费掉，避免无谓的缓存行同步操作。

具体的算法属于实现细节了，大家有兴趣可以去用：

-XX:-RestrictContended

这个虚拟机选项，查看Contended字段的内存布局。

参考——

[99.9%的Java程序员都说不清的问题：JVM中的对象内存布局？](<https://juejin.im/post/5ceac2bc5188253382697580?utm_source=gold_browser_extension>)

# 6/9

并发编程中考虑两个关键问题

* 通信
* 同步

通信的意思是指线程之间使用何种机制来交换信息。在命令式编程中，线程之间的通信机制有两种  

* 共享内存
* 消息传递

共享内存的并发模型中，线程之间共享程序的公共状态，线程之间通过写-读内存中的公共状态来隐式的进行通信，典型的共享内存通信方式就是通过**共享对象**进行通信

消息传递的并发模型中，线程之间没有公共状态，线程之间必须通过明确的发送消息来显示进行通信，在java中典型的消息传递方式就是wait()和notify()。

## 线程之间的同步

同步是指程序用于控制不同线程之间操作发生的相对顺序的机制

共享内存并发模型里，同步是显示进行的。程序员必须显示指定某个方法或者某段代码需要在线程之外互斥执行

消息传递的并发模型里，由于消息的发送必须在消息的接收之前，因此同步是隐式进行的

## java并发采用的是共享内存模型

java线程之间的通信总是隐式进行，整个通信过程对程序员完全透明。



# 7/2 JMX

java management extensions 是管理Java的一种扩展。这种机制可以直接管理正在运行中的Java 程序。

## JMX的构成

三个部分：

1. 程序端的Instrumentation，指的是MBean，类似JavaBean

2. 程序端的JMX agent，指的是MBean Server，启动与JVM内的基于各种协议的适配器，接收客户端的调遣，调用相应的MBean

3. 客户端的Remote Management，面向用户的程序，是MBeans在用户前的投影，用户操作投影，会反映到程序端的MBean中。内部的原理是client通过某种协议调用agent操控MBeans

   JMX agent与Remote Management之间是通过协议链接的，包括：

   - HTTP

   - SNMP

   - RMI

   - IIOP

     JMX agent中有针对上面协议的各种适配器

     Remote Management client可以用现成的工具，如JConsole，也可以手动设计







# 深拷贝

参考：

[Java如何对一个对象进行深拷贝？]( https://juejin.im/entry/5bc3db04f265da0aaa053baa )

```java
public class DeepClone{
    public T deepClone(T obj) {
        ObjectOutputStream oos = null;
        ObjectInputStream ois = null;
        try{
            ByteArrayOutputStream bos = new ByteArrayOutputStream();
        oos = new ObjectOutputStream(bos);
        oos.writeObjec(obj);
        oos.flush();
        
        ByteArrayInputStream bis = new ByteArrayInputStream(bos.toByteArray());
        ois = new ObjectInpuStream(bis);
        T newObj = (T)ois.readObjec();
        } catch(Exception e) {
            System.out.println(e.getMessage());
        } finally {
            if(oos != null) {
                oos.close();
            }
            if(ois != null){
                ois.close();
            }
        }
        
    }
}
```



```java
//预定义
@Data
public class User implemets Serializable{
    private String name;
    private Address adr;
    
}

public class Address implements Serializable{
    private String city;
    private String country;
    
}
```







其他实现方式：

## 方法一 构造函数

```java
public void constructorCopy() {

    Address address = new Address("杭州", "中国");
    User user = new User("大山", address);

    // 调用构造函数时进行深拷贝
    User copyUser = new User(user.getName(), new Address(address.getCity(), address.getCountry()));

    // 修改源对象的值
    user.getAddress().setCity("深圳");

    // 检查两个对象的值不同
    assertNotSame(user.getAddress().getCity(), copyUser.getAddress().getCity());

}
```

## 方法二 重载clone()方法

## 方法三 Apache Commons Lang序列化

```java
public void serializableCopy() {

    Address address = new Address("杭州", "中国");
    User user = new User("大山", address);

    // 使用Apache Commons Lang序列化进行深拷贝
    User copyUser = (User) SerializationUtils.clone(user);

    // 修改源对象的值
    user.getAddress().setCity("深圳");

    // 检查两个对象的值不同
    assertNotSame(user.getAddress().getCity(), copyUser.getAddress().getCity());

}
```

## 方法四 Gson序列化

```java
public void gsonCopy() {

    Address address = new Address("杭州", "中国");
    User user = new User("大山", address);

    // 使用Gson序列化进行深拷贝
    Gson gson = new Gson();
    User copyUser = gson.fromJson(gson.toJson(user), User.class);

    // 修改源对象的值
    user.getAddress().setCity("深圳");

    // 检查两个对象的值不同
    assertNotSame(user.getAddress().getCity(), copyUser.getAddress().getCity());

}
```

## 方法五 Jackson序列化

 修改一下User类，Address类，实现默认的无参构造函数，使其支持Jackson。 

```java
public class User {

    private String name;
    private Address address;

    // constructors, getters and setters

    public User() {
    }

}

public class Address {

    private String city;
    private String country;

    // constructors, getters and setters

    public Address() {
    }

}


public void jacksonCopy() throws IOException {

    Address address = new Address("杭州", "中国");
    User user = new User("大山", address);

    // 使用Jackson序列化进行深拷贝
    ObjectMapper objectMapper = new ObjectMapper();
    User copyUser = objectMapper.readValue(objectMapper.writeValueAsString(user), User.class);

    // 修改源对象的值
    user.getAddress().setCity("深圳");

    // 检查两个对象的值不同
    assertNotSame(user.getAddress().getCity(), copyUser.getAddress().getCity());

}
```

## 总结

| 深拷贝方法                | 优点                                                         | 缺点                                                         |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 构造函数                  | 1. 底层实现简单 2. 不需要引入第三方包 3. 系统开销小 4. 对拷贝类没有要求，不需要实现额外接口和方法 | 1. 可用性差，每次新增成员变量都需要新增新的拷贝构造函数      |
| 重载clone()方法           | 1. 底层实现较简单 2. 不需要引入第三方包 3. 系统开销小        | 1. 可用性较差，每次新增成员变量可能需要修改clone()方法 2. 拷贝类（包括其成员变量）需要实现Cloneable接口 |
| Apache Commons Lang序列化 | 1. 可用性强，新增成员变量不需要修改拷贝方法                  | 1. 底层实现较复杂 2. 需要引入Apache Commons Lang第三方JAR包 3. 拷贝类（包括其成员变量）需要实现Serializable接口 4. 序列化与反序列化存在一定的系统开销 |
| Gson序列化                | 1. 可用性强，新增成员变量不需要修改拷贝方法 2. 对拷贝类没有要求，不需要实现额外接口和方法 | 1. 底层实现复杂 2. 需要引入Gson第三方JAR包 3. 序列化与反序列化存在一定的系统开销 |
| Jackson序列化             | 1. 可用性强，新增成员变量不需要修改拷贝方法                  | 1. 底层实现复杂 2. 需要引入Jackson第三方JAR包 3. 拷贝类（包括其成员变量）需要实现默认的无参构造函数 4. 序列化与反序列化存在一定的系统开销 |



# 为什么阿里巴巴禁用Executors创建线程池

### 线程池的定义

管理一组工作线程。通过线程池复用线程有如下几点有点

- 减少资源创建 => 减少内存开销，创建线程占用内存
- 降低系统开销 => 创建线程需要时间，会延迟处理的请求
- 提高系统稳定性 => 避免无限创建线程引起的OutOfMemoryError【简称OOM】



简介TheadPoolExecutor，构造函数有4个，最终调用都是：

```java
public ThreadPoolExecutor(int corePoolSize,
                          int maximumPoolSize,
                          long keepAliveTime,
                          TimeUnit unit,
                          BlockingQueue<Runnable> workQueue,
                          ThreadFactory threadFactory,
                          RejectedExecutionHandler handler)
```

参数说明

- corePoolSize => 线程池核心线程数量
- maximumPoolSize => 线程池最大数量
- keepAliveTime => 空闲线程存活时间
- unit => 时间单位
- workQueue => 线程池所使用的缓冲队列
- threadFactory => 线程池创建线程使用的工厂
- handler => 线程池对拒绝任务的处理策略



==核心线程（corePool）==：线程池最终执行任务的角色肯定还是线程，同时我们也会限制线程的数量，所以我们可以这样理解核心线程，有新任务提交时，首先检查核心线程数，如果核心线程都在工作，而且数量也已经达到最大核心线程数，则不会继续新建核心线程，而会将任务放入等待队列。

==等待队列 (workQueue)==：等待队列用于存储当核心线程都在忙时，继续新增的任务，核心线程在执行完当前任务后，也会去等待队列拉取任务继续执行，这个队列一般是一个线程安全的阻塞队列，它的容量也可以由开发者根据业务来定制。

==非核心线程==：当等待队列满了，如果当前线程数没有超过最大线程数，则会新建线程执行任务，那么核心线程和非核心线程到底有什么区别呢？说出来你可能不信，本质上它们没有什么区别，创建出来的线程也根本没有标识去区分它们是核心还是非核心的，线程池只会去判断已有的线程数（包括核心和非核心）去跟核心线程数和最大线程数比较，来决定下一步的策略。

==线程活动保持时间 (keepAliveTime)==：线程空闲下来之后，保持存活的持续时间，超过这个时间还没有任务执行，该工作线程结束。

==饱和策略 (RejectedExecutionHandler)==：当等待队列已满，线程数也达到最大线程数时，线程池会根据饱和策略来执行后续操作，默认的策略是抛弃要加入的任务。



作者：三好码农
链接：https://juejin.im/post/5c8896be5188257ec828072f





![](demo.assets/微信图片_20191118210932.jpg)



### Executors创建线程池的方式

- Executors.newCachedThreadPool()
- Executors.newFixedThreadPool()
- Executors.newSingleThreadExecutor()



### Executors#newCachedThreadPool方法

```java
public static ExecutorService newCachedThreadPool() {
    return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                  60L, TimeUnit.SECONDS,
                                  new SynchronousQueue<Runnable>());
}
```

CachedThreadPool是一个根据需要创建新线程的线程池



- corePoolSize => 0，核心线程池的数量为0
- maximumPoolSize => Integer.MAX_VALUE，可以认为最大线程数是无限的
- keepAliveTime => 60L
- unit => 秒
- workQueue => SynchronousQueue



当一个任务提交时，corePoolSize为0不创建核心线程，SynchronousQueue是一个不存储元素的队列，可以理解为队里永远是满的，因此最终会创建非核心线程来执行任务。对于非核心线程空闲60s时将被回收。**因为Integer.MAX_VALUE非常大，可以认为是可以无限创建线程的，在资源有限的情况下容易引起OOM异常**

###  Executors#newSingleThreadExecutor方法 

```java
public static ExecutorService newSingleThreadExecutor() {
        return new FinalizableDelegatedExecutorService
            (new ThreadPoolExecutor(1, 1,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>()));
    }
```

SingleThreadExecutor是单线程线程池，只有一个核心线程



- corePoolSize => 1，核心线程池的数量为1
- maximumPoolSize => 1，只可以创建一个核心线程
- keepAliveTime => 0L
- unit => 毫秒
- workQueue => LinkedBlockingQueue



当一个任务提交时，首先会创建一个核心线程来执行任务，如果超过核心线程的数量，将会放入队列中，**因为LinkedBlockingQueue是长度为Integer.MAX_VALUE的队列，可以认为是无界队列，因此往队列中可以插入无限多的任务，在资源有限的时候容易引起OOM异常**，同时因为无界队列，maximumPoolSize和keepAliveTime参数将无效，压根就不会创建非核心线程

###  Executors#newFixedThreadPool方法 

```java
public static ExecutorService newFixedThreadPool(int nThreads) {
    return new ThreadPoolExecutor(nThreads, nThreads,
                                  0L, TimeUnit.MILLISECONDS,
                                  new LinkedBlockingQueue<Runnable>());
}
```

FixedThreadPool是固定核心线程的线程池，固定核心线程数由用户传入



- corePoolSize => n，核心线程池的数量为n
- maximumPoolSize => n，线程池最大数量为n
- keepAliveTime => 0L
- unit => 毫秒
- workQueue => LinkedBlockingQueue
- 它和SingleThreadExecutor类似，唯一的区别就是核心线程数不同，并且由于使用的是LinkedBlockingQueue，在资源有限的时候容易引起OOM异常

### 总结：



FixedThreadPool和SingleThreadExecutor => 允许的请求队列长度为Integer.MAX_VALUE，可能会堆积大量的请求，从而引起OOM异常

CachedThreadPool => 允许创建的线程数为Integer.MAX_VALUE，可能会创建大量的线程，从而引起OOM异常



这就是为什么禁止使用Executors去创建线程池，而是推荐自己去创建ThreadPoolExecutor的原因



# java模拟listener

监听器就是一个**实现特定接口的普通java程序**，这个程序专门用于**监听另一个java对象的方法调用或属性改变**，当被监听对象发生上述事件后，监听器的处理逻辑就会启动

## 监听器组件

监听器涉及三个组件：**事件源，事件对象，事件监听器**

**当事件源发生某个动作的时候，它会调用事件监听器的方法，并在调用事件监听器方法的时候把事件对象传递进去。**

**我们在监听器中就可以通过事件对象获取得到事件源，从而对事件源进行操作！**

![](https://segmentfault.com/img/remote/1460000013240473?w=889&h=253)



## 监听器

```java
  /**
     * 事件监听器
     *
     * 监听Person事件源的eat和sleep方法
     */
    interface PersonListener{
    
        void doEat(Event event);
        void doSleep(Event event);
    }
```



## 事件源

**事件源需要注册监听器(即在事件源上关联监听器对象)**

如果**触发了eat或sleep()方法的时候，会调用监听器的方法，并将事件对象传递进去**

```java


    /**
     *
     * 事件源Person
     *
     * 事件源要提供方法注册监听器(即在事件源上关联监听器对象)
     */
    
    class Person {
    
        //在成员变量定义一个监听器对象
        private PersonListener personListener ;
        
        //在事件源中定义两个方法
        public void Eat() {
            
            //当事件源调用了Eat方法时，应该触发监听器的方法，调用监听器的方法并把事件对象传递进去
            personListener.doEat(new Event(this));
        }
    
        public void sleep() {
    
            //当事件源调用了Eat方法时，应该触发监听器的方法，调用监听器的方法并把事件对象传递进去
            personListener.doSleep(new Event(this));
        }
    
        //注册监听器，该类没有监听器对象啊，那么就传递进来吧。
        public void registerLister(PersonListener personListener) {
            this.personListener = personListener;
        }
    
    }
```







## 事件对象

**事件对象封装了事件源。**

**监听器可以从事件对象上获取得到事件源的对象(信息)**		

```java

    /**
     * 事件对象Even
     *
     * 事件对象封装了事件源
     *
     * 在监听器上能够通过事件对象获取得到事件源
     *
     *
     */
    class Event{
        private Person person;
    
        public Event() {
        }
    
        public Event(Person person) {
            this.person = person;
        }
    
        public Person getResource() {
            return person;
        }
    
    }
```



## 测试

```java
public static void main(String[] args) {

        Person person = new Person();

        //注册监听器()
        person.registerLister(new PersonListener() {
            @Override
            public void doEat(Event event) {
                Person person1 = event.getResource();
                System.out.println(person1 + "正在吃饭呢！");
            }

            @Override
            public void doSleep(Event event) {
                Person person1 = event.getResource();
                System.out.println(person1 + "正在睡觉呢！");
            }
        });


        //当调用eat方法时，触发事件，将事件对象传递给监听器，最后监听器获得事件源，对事件源进行操作
        person.Eat();
    }

```





# AOP

oop的补充



## aspectj框架

### 概念：

@Aspect

@Pointcut

@Before

@After

@Aroud





# Reflect

java.lang.reflect

Class 类在java lang 包

获取Method对象的区别

```java
xxx.getClass().getMethod();
xxx.class.getMethod();

xxx.getClass().getDeclaringMethod();
xxx.class.getDeclaringMethod();
//可以获取private method
```

获取实现接口

## [类型体系](https://www.jianshu.com/p/e8eeff12c306)

### ParameterizedType 表示参数化类型，也就是泛型，例如List<T>

1.  getActualTypeArguments() ---获取泛型中的实际类型，可能会存在多个泛型，例如Map<K,V>,所以会返回Type[]数组
2. getRawType()---获取声明泛型的类或者接口，也就是泛型中<>前面的那个值
3. getOwnerType()---可以获取到内部类的“拥有者”；例如： Map 就是 Map.Entry<String,String>的拥有者

```java
xxx.getGenericInterfaces();

//获取带泛型的接口
Type[] types = xxx.getGenericInterfaces();
for (Type type : type ) {
    if (type instanceof ParameterizedType) {
        //判断是不是带泛型的接口
    }
}

//获取父类 
xxx.getGenericSuperclass();

p.get
```

### GenericArrayType

泛型数组类型，例如List<String>[] 、T[]等

```java
private T[] t;
private List<String>[] listArray;

public static void main(String[] args) throws NoSuchFieldException {
    Field fieldListArray = GenericArrayListTest.class.getDeclareField("listArray");
    Type typeListArray = fieldListArray.getGenericType();
    System.out.println(typeListArray.getClass().getName());
    Field fieldT = GenericArrayTypeTest.class.getDeclareField("listArray");
    Type typeT = fieldT.getGenericType();
    System.out.println(typeT.getClass().getName());
}
```

在GenericArrayType接口中，仅有1个方法，就是getGenericComponentType()；

返回泛型数组中元素的Type类型，即List<String>[] 中的 List<String>（ParameterizedTypeImpl）、T[] 中的T（TypeVariableImpl）

==值得注意的是，无论是几维数组，getGenericComponentType()方法都只会脱去最右边的[]，返回剩下的值==；

### TypeVariable

泛型的类型变量，指的是List<T>、Map<K,V>中的T，K，V等值，实际的Java类型是TypeVariableImpl（TypeVariable的子类）；此外，还可以对类型变量加上extend限定，这样会有类型变量对应的上限

```java

    private List<K> listArray;

    public static void main(String[] args) throws NoSuchFieldException {
        Field fieldList = HashMapCopy.class.getDeclaredField("listArray");
        Type type = fieldList.getGenericType();

        if (type instanceof ParameterizedType) {
            Type[] arguments =
                    ((ParameterizedType) type).getActualTypeArguments();
            System.out.println(arguments[0].getClass().getName());
            
            
        }
    }
```

getBounds()---获得该类型变量的上限，也就是泛型中extend右边的值；例如 List<T extends Number> ，Number就是类型变量T的上限；如果我们只是简单的声明了List<T>（无显式定义extends），那么默认为Object；

getGenericDeclaration()---获取声明该类型变量实体，也就是TypeVariableTest<T>中的TypeVariableTest

getName()---获取类型变量在源码中定义的名称；



## 位运算

`|` 或

`>>` 右移

`<<`左移

`~` 非

`^` 异或

`>>>` 和`>>`的区别



# 类加载器ClassLoader

## 1、类加载器

Java 文件被运行，第一步，需要通过 javac 编译器编译为 class 文件；第二步，JVM 运行 class 文件，实现跨平台。而 JVM 虚拟机第一步肯定是 加载 class 文件，所以，类加载器实现的就是（来自《深入理解Java虚拟机》）：

```
通过一个类的全限定名来获取描述此类的二进制字节流
```

类加载器有几个重要的特性：

1. 每个类加载器都有自己的预定义的搜索范围，用来加载 class 文件；
2. 每个类和加载它的类加载器共同确定了这个类的唯一性，也就是说如果一个 class 文件被不同的类加载器加载到了 JVM 中，那么这两个类就是不同的类，虽然他们都来自同一份 class 文件；
3. 双亲委派模型。
   

## 2、双亲委派模型

### 2.1 

1. 所有的类加载器都是有层级结构的，每个类加载器都有一个父类类加载器（通过组合实现，而不是继承），除了**启动类加载器（Bootstrap ClassLoader）**；
2. 当一个类加载器接收到一个类加载请求时，首先将这个请求委派给它的父加载器去加载，所以每个类加载请求最终都会传递到顶层的**启动类加载器**，如果父加载器无法加载时，子类加载器才会去尝试自己去加载；

通过双亲委派模型就实现了类加载器的三个特性：

1. 委派（delegation）：子类加载器委派给父类加载器加载；
2. 可见性（visibility）：子类加载器可访问父类加载器加载的类，父类不能访问子类加载器加载的类；
3. 一性（uniqueness）：可保证每个类只被加载一次，比如 Object 类是被 Bootstrap ClassLoader 加载的，因为有了双亲委派模型，所有的 Object 类加载请求都委派到了 Bootstrap ClassLoader，所以保证了只被加载一次。

### 2.2 Java 中的类加载器

从 JVM 虚拟机的角度来看，只存在两种不同的类加载器：

1. 启动类加载器（Bootstrap ClassLoader），是虚拟机自身的一部分；
2. 所有其他的类加载器，独立于虚拟机外部，都继承自抽象类 java.lang.ClassLoader。

而绝大多数 Java 应用都会用到如下 3 中系统提供的类加载器：

1. **启动类加载器**（Bootstrap/Primordial/NULL ClassLoader）：顶层的类加载器，没有父类加载器。负责加载 /lib 目录下的，或则被 -Xbootclasspath 参数所指定路径中的，并被 JVM 识别的（仅按文件名识别，如 rt.jar，名字不符合的类库即使放在 lib 目录也不会被加载）类库加载到虚拟机内存中。所有被 Bootstrap classloader 加载的类，它的 Class.getClassLoader 方法返回的都是 null，所以也称作 NULL ClassLoader。
2. **扩展类加载器**（Extension CLassLoader）：由 sun.misc.Launcher$ExtClassLoader 实现，负责加载 <JAVA_HOME>/lib/ext 目录下，或被 java.ext.dirs 系统变量所指定的目录下的所有类库；
3. **应用程序类加载器**（Application/System ClassLoader）：由 sun.misc.Launcher$AppClassLoader 实现。它是 ClassLoader.getSystemClassLoader() 方法的默认返回值，所以也称为系统类加载器（System ClassLoader）。它负责加载 classpath 下所指定的类库，如果应用程序没有自定义过自己的类加载器，一般情况下这个就是程序中默认的类加载器。


##  Java 程序中的类加载器层级结构图：

![img](https://img-blog.csdn.net/20180914180854640?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW5nc2hrXw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)



它的整个生命周期将会经历加载（Loading）、验证（Verification）、准备（Preparation）、解析（Resolution）、初始化（Initialization）、使用（Using）和卸载（Unloading）七个阶段，其中验证、准备、解析三个部分统称为连接（Linking)