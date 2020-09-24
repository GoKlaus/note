# java的引用

## 强引用

默认就是强引用

## 软引用

软引用是用来描述一些非必需但仍有用的对象。**在内存足够的时候，软引用对象不会被回收，只有在内存不足时，系统则会回收软引用对象，如果回收了软引用对象之后仍然没有足够的内存，才会抛出内存溢出异常**

## 弱引用

弱引用的引用强度比软引用更弱一些，**无论内存是否足够，只要 JVM 开始进行垃圾回收，那些被弱引用关联的对象都会被回收**

## 虚引用

虚引用是最弱的一种引用关系，如果一个对象仅持有虚引用，那么它就和没有任何引用一样，它随时可能会被回收，虚引用根本不会影响对象的声明周期



```
http://gw.api.taobao.com/router/rest?timestamp=2020-09-07%2018%3a40%3al7&method=taobao.tbk.privilege.get&session=620292147cl2cb2e7371f4442736dfha0639e45267c56f12452894142&adzone_id=109844900348&site_id=376150223&app_key=25635011&format=json&v=2.0&sign_method=hmac&item_id=586940778084&sign=8D8BB705087A803EA325C8925CFE776D
```

编程思想和java 核心的技术的笔记

# 1.对象导论

# 2.一切都是对象

在Java中，只有`基本类型`不是对象

### equals方法的准则

前提：是同一个类

建议不使用instanceof，无法解决otherObject是子类的情况，并且还有可能会招致一些麻烦

```java
if (!(otherObject   instanceof  Employee)) return false;
```

```
自反性：对于任何非空引用值x，x.equals(x)都应返回true
对称性：对于任何非空引用值x和y，当且仅当y.equals(x)返回true时，x.equals(y)才应返回true
传递性：对于任何非空引用值x、y和z，如果x.equals(y)返回true，并且y.equals(z)返回true，那么x.equals(z)应返回true
一致性：对于任何非空引用值x和y，多次调用x.equals(y)始终返回true或始终返回false，前提是对象上equals比较中所用的信息没有被修改
非空性：对于任何非空引用值x，x.equals(null)都应返回false
```


# 3.操作符
# 4.控制执行流程
# 5.初始化与清理
# 6.访问控制权限
# 7.复用类
# 8.多态
# 9.接口

## 函数式接口

函数式接口(Functional Interface)就是一个有且仅有一个抽象方法，但是可以有多个非抽象方法的接口。

函数式接口可以被隐式转换为 lambda 表达式。

Lambda 表达式和方法引用（实际上也可认为是Lambda表达式）上



## 关于值传递和引用传递

局部变量和方法参数在jvm中的储存方法是相同的，都是在栈上开辟空间来储存的，随着进入方法开辟，退出方法回收

java 只有值传递

# 10.内部类

1. 普通内部类
2. 静态内部类
3. 匿名内部类
4. 局部内部类

生成一个内部类的对象时，此对象与制造他的外围对象就有了一种联系，内部能访问外围对象的所有成员，而不需要任何特殊条件----内部类拥有外围类的所有元素的访问权

```java
此内部必定会秘密的一个指向外围类对象的引用，通过这个引用来访问外围类的成员
```



如果不需要内部类对象和外围类对象之间有联系，使用static  ----  称为嵌套类

嵌套类没有隐式的外围引用：

```java
--- 要创建嵌套类，就不需要其外围类的对象
--- 不能从嵌套类的对象中访问静态类的外围类对象
```

普通内部类字段、方法，只能放在类的外部层次上，所以普通的内部类不能有staic数据和字段



接口内部的类： 正常情况下，不能在接口内部放置任何代码，但嵌套类可以作为接口的一部分，接口内的类自动是public 和static的





# 11.持有对象

## 11.2 基本概念

Java容器类类库的用途是“保存对象”，并将其划分为两个不同的概念：

1. Collection，一个独立元素的队列，元素都服从一条或多条规则

   | 容器类型 | 服从规则                         |
   | -------- | -------------------------------- |
   | List     | 按照插入的顺序保存元素           |
   | Set      | 不能有重复元素                   |
   | Queue    | 按照排队规则来确定对象产生的顺序 |

   

2. Map。一组成对的“键值对”对象。    也被称为“关联数组”，或者“字典”

![img](assets/2529760-c09de6b64377d284.webp)

所有的Collection都可以用foreach语法遍历，因为都是Iterator接口



判断某个元素是否属于 结合内，或者集合是否包含这个对象，需要这个类有重写equals和hashCode



## 11.6 迭代器

迭代器（是一种设计模式）是一个对象，用来遍历并选择序列中的对象，客户端程序不必关注序列的底层结构

> 迭代器被称为轻量级对象

### ListIterrator

是Iterrator的子类型，可以双向移动

## 11.7 LinkedList

## 11.8  Stack

“栈”通常指“后进先出”（LIFO）的容器，也被称为“叠加栈”







# 12.通过异常处理错误
# 13.字符串
## 不可变String
>String对象是不可变的，String类的每一个看起来修改String值的方法，实际上都是创建了一个新的String对象------**不可变性**
### 重载"+"和StringBuilder
>可以给String对象添加任意多的别名，因为**String对象具有只读特性**，不会对他的应用有任何影响
>坏处：**会带来一定的效率问题**，
>重载：一个操作符在用于特定的类时，被赋予了特殊的意义。
```
Java中仅有的两个重载的操作符:
1、“+”
2、“+=”
```
```
public class Connection{
    public static void main(String[] args){
        String mango = "mango";
        String s = "abc"+mango+"def"+47;
        System.out.print(s);
    }
}
```
生成最终的String对象过程中产生了一堆需要垃圾回收的中间对象

>jvm自动的引入了`StringBuilder`类
### 无意识的递归
`如何使用toString()打印出对象的地址`
>使用this关键字
```
public class InfiniteRecursion{
    public static void main(String[] args){
        List<InfiniteRecuresion> v = 
            new ArrayList<InfiniteRecuresion>();
        for(int i = 0; i < 10; i++)
            v.add(new InfiniteRecursion();
        System.out.print(v);
    }
    public String toString(){
    //这样写有异常，+this会自动调用this.toString()方法，就发生了递归调用
    //    return "InfiniteRecursion address:"+this+"\n";
        return "InfiniteRecursion address:"+super.toString()+"\n";
    }
}
```
String类的方法返回值：
* 内容没有改变，返回原对象的引用
* 内容改变了，返回了一个新的引用
### 格式化输出
### printf()用法
### System.out.format()
### Formatter类
Java中管理所有的格式化功能，可以看做一个**翻译器**。
### 格式化说明符
### String.format()
应用场景：只需要使用此意format()方法时，String.format()用起来更方便
### 正则表达式
>正则表达式  包含的各种字符，字符类，逻辑操作符，量词等等需要再做一个研究，理解并学会使用正则
>**Pattern.compile()的另外一个版本**：接受一个标价参数

| 编译标记                     | 效果 |
| ---------------------------- | ---- |
| Pattern.CANON_EQ             |      |
| Pattern.CASE_INSENSITIVE(?i) |      |
| Pattern.CONMMENTS(?x)        |      |
| Pattern.DOTALL(?s)           |      |
| Pattern.MUTILINE(?m)         |      |
| Pattern.UNICODE_CSAE(?u)     |      |
| Pattern.UNIX_LINES(?d)       |      |
**匹配**
**分割**
**替换**
**第四种，后续添加**


### Pattern和Matcher
相比较于功能有限的String类，正则表达式对象功能更强大

## 扫描输入
> 使用StringReader将String转化为可读的流对象，使用这个对象来构造BufferReader对象，使用readLine()方法，一次读取一行文本
> Scanner类：
#### Scanner定界符
默认：根据空白字符对输入进行分词
支持：通过正则表达式指定定界符
~~~
    import java.util.*;
    
    public class ScannerDelimiter{
        public static void main(String[] args){
            Scanner scanner = new Scanner("12, 42, 78, 99, 42");
            scanner.useDelimiter("\\s*,\\s*");
            while(scanner.hasNextInt())
                System.out.println(scanner.nextInt());
        }
    }
~~~
`以上的代码制定了  ","为定界符，包括逗号前后任意的空白字符`
### 使用正则表达式扫描
>除了能够扫描基本类型之外，还可以用自定义的正则表达式进行扫描
## 14.类型信息
`运行时类型信息使得你可以在程序运行时发现和使用类型信息`
`RTTI：Run-Time Type Identification
通过运行时类型信息程序能够使用基类的指针或引用来检查这些指针或引用所指的对象的实际派生类型`
>Java是如何在运行时识别对象和类的信息的：
>1、"传统的"的RTTI，假定我们在编译时已经知道了所有的信息
>2、"反射"机制，允许我们在运行时发现和使用类的信息
### 为什么使用RTTI
>RTTI名字的含义：在运行时，识别一个对象的类型   

`RTTI和反射的区别？？？？？`
## Class对象
Java使用Class对象来执行其RTTI
>类是程序的一部分，每个类都有一个Class对象，当编写并且编译了一个新类，就会产生一个Class对象(更恰当的说，是保存在一个同名的.class文件中)，为了生成这个对象，运行这个程序的Java虚拟机(JVM)将使用被称为"类加载器"的子系统
***
>类加载器子系统实际上可以包含一条类加载链，但是只有一个`原生类加载器`，他是JVM实现的一部分。原生类加载器加载的是所谓的`可信类`，包括Java API类，通常是通过本地盘加载的。在这条链中，通常是不需要添加额外的类加载器，但是如果你有特殊的需求，那么你有一种方式可以加载额外的类加载器
***
>所有的类都是在对其第一次使用的时候动态的加载到JVM中的，当程序创建第一个对类的静态成员的引用时，就会加载这个类。`这个证明构造器也是类的静态方法，即使在构造器之前并没有使用static关键字。因此使用new操作符创建类的新对象也会当做对类的静态成员的引用。`

因此，Java程序在它开始运行之前并非完全被加载。如果尚未加载，默认的类加载器就会根据类名查找.class文件。这个字节码被加载时，它们会接受验证，确保没有被破坏，并且不包含不良Java代码（这是Java中用于安全防范目的的措施之一）。一  
***

# 15.泛型

​		一般类使用具体类型，要么基本类型，要么自定义类，越是具体的类，适用的范围相应就越小。

​		在面向对象编程语言中，多态算是一种**泛化机制**。基类作为参数，从基类导出的任何类也可以作为参数。但**final**类不能扩展，其他任何类都可以被扩展，仍然是有一定的限制。

​		与单继承体系相比，接口作为参数，而不是一个类，限制会变小。但有时接口也是对程序的约束还是太强了，任然需要实际实现这个接口的具体类。这里就需要一种“某种不具体的类型”，来编写更通用的代码，而不是一个具体的类或接口

​		泛型的概念：Java SE5 引入的改变。泛型实现了==参数化类型==的概念，使代码可以应用于多种类型。 ==解耦类或方法与所使用的的类型之间的约束==。-------就是将原来具体的类型参数化，实际使用传入具体的参数。

```
理解注释：
在使用的过程需要用到参数，参数是某种类型的对象，但是想适用范围更广，选择使用一个参数来代替具体的类型参数，到了具体使用的时候通过<具体类型>来告诉编译器，类里或者方法里的这些参数都变成这个。达到限制具体类型参与的目的
```



## 15.2 简单泛型

泛型对与容器类：

```java
class Automobile{}

public class Holder1{
    private Automobile a;
    public Holder1(Automobile a){
        this.a = a;
    }
    public getAutomobile(){
        return a;
    }
}
```

重用性不好，无法持有其他类型的任何对象，在内部已经声明的具体的类型参数。

Java SE5 之前可以通过这个持有Object类型的对象来扩大适用范围。

泛型的主要目的是用来指定==容器要持有什么样的对象，而且由编译器来保证类型的正确性==：

```java
public class Holder3<T>{
    private T a;
    public Holder3(T a){this.a = a;}
    public void set(T a){this.a = a;}
    public T get(){return a;}
    public static void main(String[] args){
        Holder3<Automobile> h3 = new Holder3<Automobile>(new Automobile());
        Automobile a = h3.get();
    }
}
```

使用时必要在<>尖括号中指明想要持有什么样子的类型：即告诉编译器，想要使用什么样的类型，让编译器帮处理一切细节。

### 15.2.1 一个元组类库

​	**元祖(tuple)**的概念：将一组对象直接打包存储于其中一个单一对象，这个容器对象允许读取其中的元素，但是不允许向其中存放新的元素。 (这个概念也称为**数据传送对象**，或**信使**) 

> 和DTO有些类似的感觉

```java
//不使用泛型
public class TwoTuple1{
    public final Item a;
    public final Price b;
    public TwoTuple1(Item a,Price b){
        this.a = a;
        this.b = b;
    }
}
//使用泛型
public class TwoTuple2<A,B>{
    public final A first;
    public final B second;
}
```

从适用性上的扩展是泛型带来显性的改变

不使用访问器和修改器(get和set)，使用final后，就无法将其他的值赋予first和second。

可以通过继承机制来实现长度更长的元组：

```java
public class ThreeTuple<A,B,C> extends TwoTuple2<A,B>{
    public final C third;
    public ThreeTuple(A a,B b,C c){
        super(a,b);
        this.third = c;
    }
}
public class FourTuple<A,B,C,D> extends ThreeTuple<A,B,C>{
    ////
}
```

### 15.2.1 一个堆栈类

​		一个内部链式存储机制：

```java
public class LinkedStack<T>{
    private static class Node<U>{
        U item;
        Node<U> next;
        Node(){
            item = null;
            next = null;
        }
        Node(U item,Node<U> next){
            this.item = item;
            this.next = next;
        }
        boolean end(){return item == null && next == null;}
    }
    private Node<T> top = new Node<T>();//End sentinel
    public void push(T item ){
        top = new Node<T>(item,top);
    }
    public T top(){
        T result = top.item;
        if(!top.end())
           top = top.next;
       	return result;
    }
    public void main(String[] args){
        LinkedStack<String> lss = new LinkedStack<String>();
        for(String s : "Phasers or stun!".split(" ")){
            lss.push(s);
        String s;
        while((s = lss.pop()) != null){
            System.out.println(S);
        }
    }
}
```

该例子使用了末端哨兵(end sentinel)来判断堆栈何时为空，每次调用一次push()方法，就会创建一个Node<T>对象，并将其链接到前一个Node<T>对象。

```
理解注释：
一种容器的实现思路，容器中的数据以节点的形式存在，每个节点包含下个节点的引用（地址），达到链式的存储方式
```



### 15.2.3 RandomList

假设需要一个持有特定类型对象的列表，每次调用其上的select()方法时，它可以随机选取一个元素。

```java
import java.util.*;

public class RandomList<T>{
    private Arraylist<T> storage = new ArrayList<T>();
    private Random rand = new Random(47);
    public void add(T item){ storage.add(item);}
    public T select(){
        return storage.get(rand.nextInt(storage.size());)
    }
    public static void main(String[] args){
        RandomList<String> rs = new RandomList<String>();
        for(String s : ("The quick brown fox jumped over " +
                        "the lazy brown dog").split(" "))
            rs.add(s);
        for(int i = 0; i < 11; i++)
            System.out.println(rs.select() + "");
    }
}

```

## 15.3 泛型接口

泛型在接口的应用，例如生成器(generator)，这是一种专门负责创建对象的类。实际上，这是工厂方法设计模式的一种应用。不过，生成器常见新的对象时，他不需要任何的参数，而工厂方法一般需要参数。

```java
pulic interface Generator<T> { T next();}
```

```java
public class CoffeeGenerator implements Generator<Coffee>, Iterable<Coffee>{
    private Class[] types = {Latte.class,Mocha.class,Cappuccino.class,Americano.class,Breva,class};
    private static Random rand = new Random(47);
    public CoffeeGenerator(){}
    
    private int size = 0;
    public CoffeeGenerator(int sz){ size = sz;}
    public Coffee Next(){
        try{
            return (Coffee)type[rand.nextInt(types.length)].newInstance();
        }catch(Exception e){
            throw new RnuTimeException(e);
        }
    }
    class CoffeeIterator implements Iterator<Coffee>{
        int count = size;
        public boolean hasNext(){
            count --;
            return CoffeeGenerator.this.next();
        }
        public void remove(){
            throw new UnsupportedOperationException();
        }
    }
    public Iterator<Coffee> iterator(){
        return new CoffeeIterator();
    }
    public static void main(String[] args){
        CoffeeGenerator gen = new CoffeeGenerator();
        for(int i = 0;i < 5; i++){
            System.out.println(gen.next());
        }
        for(Coffee c : new CoffeeGenerator(5)){
            System.out.println(c);
        }
    }
}
```

参数化的Generator接口确保next()的返回值是参数类型。CoffeeGenerator同事还实现了Iterable接口，说以在循环语句中使用。不过它还需要一个“末端哨兵”来判断何时停止，这是第二个构造器的功能。

```java
public class Fibonacci implements Generator<Integer>{
    private int count = 0;
    public Integer next(){return fib(count++);}
    private int fib(int n){
        if(n<2) return 1;
        return fib(n-2) + fib(n-1);
    }
    public static void main(String[] args){
        Fibonacci gen = new Fibonacci();
        for(int i = 0; i < 18; i++){
            System.out.println(gen.next() + " ");
        }
    }
}
```

在Fibnoacci类的里里外外使用的都是int类型，但是参数都是Integer——Java泛型的一个局限性：基本类型无法作为类型参数。  从Java SE5具备了自动打包和自动拆包的功能。

## 15.4 泛型方法

泛型用在方法上——是否拥有泛型方法，与其所在的类是否是泛型没有关系。

对于一个static方法而言，无法访问泛型类的类型参数，所以，如果static方法需要使用泛型能力，就必须使其成为泛型方法。

```java
public class GenericMethods {
    public <T> void f(T x){
        System.out.println(x.getClass().getName());
    }
    public void main(String[] args){
        GenericMethods gm = new GenericMethods();
        gm.f(" ");
        gm.f(1);
        gm.f(1.0);
        gm.f(1.0F);
        gm.f('c');
        gm.f(gm);
    }
}
```

使用泛型类时，必须在创建对象的时候指定类型参数的值，

而使用泛型方法的时候，通常不必指明参数类型，因为编译器会为我们找出具体的类型。这称为**类型参数推断(type argument inference)**。

f()调用基本类型的时候，会自动打包

### 15.4.1 杠杆利用类型参数推断

```java
Map<Person, List<? extends Pet>> petPeople = 
    new HashMap<Person, List<? extends Pet>>();
```

类型推断只对赋值操作有效，其他时候不起作用

#### 显式的类型说明

泛型方法中可以显式的指明类型，不过这种语法很少见，要显式的指明类型，必须在点操作符与方法名之间插入尖括号，然后把类型置于尖括号内，如果是在定义该方法的内部必须在点操作符之前使用this关键字，如果是使用static的方法，必须在点操作符之前加上类名。

只有在进行非赋值语句时，才需要这样操作。

### 15.4.2 可变参数与泛型方法

泛型方法和可变参数列表能够很好的共存

```java
public class GenericVarargs{
    public static <T> List<T> makeList(T... args){
        List<T> result = new ArrayList<T>();
        for(T item : args)
            reustlt.add(item);
        return result;
    }
    public static void main (String[] args){
        List<String> ls = makeList("A");
        System.out.println(ls);
        ls = makeList("A","B","C");
        System.out.println(ls);
    }
}
```

### 15.4.3 用于Generator的泛型方法

### 15.4.4 一个通用的Generator

### 15.4.5 简化元组的使用

### 15.4.6 一个Set使用工具

## 15.5 匿名内部类

## 15.6 构建复杂模型

## 15.7 擦除的神秘之处

 **在泛型代码内部，无法获取任何有关泛型参数类型的信息。**

Java泛型是使用擦除来实现的，List<Stirng>和 List<Integer>在运行时事实上是相同的类型，两种形式都被擦除成原生的“List”类型。

### 15.7.1 C++的方式

C++没有擦除

```c++
#include<iostream>
using namespace std;
template<class T> class Manipulator {
    T obj;
    public:
    	Manipulator(T x) { obj = x; }
    	void manipulator { obj.f();}
};
class HasF {
    public:
    	void f() { cout << "HasF :: f()" << endl;}
};
int main() {
    HasF hf;
    Manipulator<HasF> manipulator(hf);
    manipulator.manipulator();
}
```

当实例化这个模板的时候，C++编译器将进行检查。在Manipulator<HasF>被实例化的这一刻，会检查到HasF拥有f()这个方法。如果情况并非如此，就会得到一个编译期错误。

```java
public class HasF {
    public void f() {
        System.out.println("HasF.f()");
    }
}

class Manipulato<T> {
    T obj;
    public Manipulator(T x) {
        obj = x;
    }
    public void manipulator() {
        obj.f();
    }
}
```

这是错误的表达，因为有了擦除，Java编译器无法将manipulator()必须能够在obj上调用f()这一需求映射到HasF拥有f()上。

为了完成上述功能，引入了**泛型类边界的概念**：告诉编译器只能遵守这个边界的类型，重用extends关键字

```java
class Manipulator<T extends HasF> {
    T obj;
    public Manipulator(T x) { obj = x; }
    public void manipulator() { obj.f(); }
}
```

**泛型类型参数**将擦除到他的第一个边界(可能会有多个边界),**类型参数**的擦除，代码解释：

```java
class Manipulator<T extends HasF> {
    T obj;
    public Manipulator(T x) { obj = x; }
    public void manipulator() { obj.f(); }
}
//编译器实际上会把类型参数替换为它的擦除，T擦除到了HasF，就好像在类的声明中用HasF替换掉了T一样
//在上述例子中，泛型没有贡献任何好处。只需很容易的自己去擦除。就可以创建出没有泛型的类：

class Manipulator3 {
    private HasF obj;
    public Manipulator3() { obj = x; }
    public void manipulator() {
        obj.f();
    }
}
```

以上的例子很好的体现了一点：当你希望使用的类型参数比某个更具体的类型(以及他的所有的子类型)更加泛化的时候

###  15.7.2 迁移兼容性

泛型类型只有在静态类型检查期间才出现，在此之后，程序中所有的泛型类型都将被擦除，例如

List<T> ------>  List

而普通的类型变量在未指定边界的情况下将被擦除为Object。

擦除的核心动机是泛化的客户端可以用非泛化的类库来使用，反之亦然。------>迁移兼容性

### 15.7.3  擦除的问题

擦除的代价是显著的，泛型不能用于显式的引用运行时的类型的操作中，例如转型、instanceof操作和new表达式，

### 15.7.4 边界处的动作

擦除带来的困惑，可以表示没有任何意义的事务。

```java
public class ArrayMaker<T> {
    private Class<T> kind;
    public ArrayMaker(Class<T> kind) { this.kind = kind; }
    @SuppressWarnings("unchenked")
    T[] create(int size) {
        return (T[])Array.newInstance(kind, size);
    }
    public static void main(Stirng[] args) {
        ArrayMaker<String> stringMaker = new ArrayMaker<String>(String.class);
        String[] stringArray = stringMaker.create();
        System.out.println(Arrays.toString(stringArray));
    }
}
```

## 15.9 边界

边界可以在泛型的参数类型上设置限制条件，可以强制规定泛型可以应用的类型，潜在的效果是按照边界类型来调用方法。

因为擦除移除了类型信息，所以无界泛型参数调用的方法只是那些可以用Object调用的方法。Java泛型重用了extends关键字来实现将参数限制为某个类型自己。

==extends关键字在泛型边界上下文环境中和在普通情况下所具有的的意义是完全不同的。==

```java
interface HasColor{
    java.awt.Color getColor();
}
class Colored<T extends HasColor>{
    T item;
    Colored(T item){ this.item = item; }
    java.awt.Color color(){
        return item.getColor();
    }
}
class Dimension{ public int x, y, z; }
class ColoredDimension<T extends HasColor & Dimension>{
    T item;
    ColoredDimension(T item){ this.item = item; }
    T getItem(){ return item; }
    java.awt.Color color(){ return item.getColor(); }
    int getX(){ return item.x; }
    int getY(){ return item.y; }
    int getZ(){ return item.z; }
}
```

可以使用继承来消除冗余

```java
class HoldItem<T>{
    T item;
    HoldItem(T item){ this.item = item; }
    T getItem(){ return item; }
}

class Colored2<T extends HasColor> extends HoldItem<T>{
    Colored2(T item){ super(item); }
    java.awt.Color color(){ return item.getColor(); }
}

class ColoredDimension2<T extends Dimension & HasColor> extends Colored2<T>{
    ColoredDimension2<T>{ super(item); }
    int getX(){ return item.x; }
    int getY(){ return item.y; }
    int getZ(){ return item.z; }
}
```

## 15.10 通配符

Apple的List在类型上不等价于Fruit的List，即使Apple是一种Fruit类型。

```java
class Fruit{}
class Apple extends Fruit {}
class Jonathan extends Apple {}
class Orange extends Fruit{}

public class NonCovariantGenerics{
    //Compile Error: incompatible types;
    List<Fruit> flist = new ArrayList<Apple>();
}
```



泛型没有内建的协变类型。数组在语言中是完全定义的，因此可以内建了编译期和运行时的检查，但是使用泛型时，编译器和运行时系统都不知道你想用类型做些什么，以及应该采用什么样的规则。

解释：

1. 两个泛型之间是没有关系的（所以自然没有继承关系）
2. List<Apple>在类型上不等价于List<Number>
3. 真正的问题是，讨论的是容器的类型，而不是容器持有的类型

### 延伸--Java泛型的协变、逆变和不变

协变：<? extends T> --->实现向上转型List<? extends Fruit> flist = new ArrayList<Apple>();    说明实际类型比变量显示的更小

逆变：<? super T>--->实现向下转型List<? super Apple> alist = new ArrayList<Fruit>();  说明实际类型比变量显示的更大

不变：T  --->没有关系，无法去比较

```
T   和   ？ 区别
声明一个泛型类或泛型方法
使用一个泛型类或泛型方法
```



 

**逆变与协变来描述类型转换（type transformation）后的继承关系**，其定义：如果A、B表示类型，f(·)表示类型转化

f(·)是**逆变（contravariant）**的，当A≤B时有f(B)≤f(A)成立；

f(·)是**协变（covariant）**的，当A≤B时有f(A)≤f(B)成立；

f(·)是**不变（invariant）**的，当A≤B时上述两个式子均不成立，即f(A)与f(B)相互之间没有继承关系

## 15.10.1 

List<? extends Fruit> 的add()方法参数就变成了"? extends Fruit"，从这个描述中，编译器不能了解这里需要Fruit的那个具体子类型，因此他不会接受任何类型的Fruit。

将Apple向上转型为Fruit也没用，==编译器会直接拒绝调对参数列表中涉及通配符的方法的调用==

> 不知道具体这个？extends Fruit是什么类型，运行检查



```
List和List<?>
List表示   持有任何Object类型的原生List
List<?>表示  具有某种特定类型的非原生List，只是不知道那种类型是什么
```





### 15.10.2 逆变

超类型通配符，声明通配符继承某个类

### 15.10.4 捕获转换

通配符`?`和任意引用类型`T`的关系，对于ArrayList<?>类型是ArrayList<T>的超类型。



## 15.11 问题

 基本类型不能作为类型参数，

解决方案是

> Java SE5的自动包装机制，双向转换机制，ArrayList<Integer> 就像是一个ArrayList<int>一样



## 15.12 自限定的类型

```java
class SelfBounded<T extends SelfBounded<T>>
```



古怪的循环泛型（CRG）

CRG：**基类用导出类替代其参数。**意味着泛型基类编程了一种其所有导出类的公共功能的模板。

```java
//这个不是   
public interface BaseService<T>{
    void f();
}


public class BaseServiceImpl<T> implements BaseService<T> {
    
    private Mapper<T> mapper;
    
    void f(){
        
    }
}

public interface FruitMapper<Fruit> extends Mapper<Fruit>{
    
}

public interface FruitService extends FruitService<Fruit>{}

public class FruitServiceImpl implements FruitServiceImpl{}
```





### 自限定

自限定类型的价值在于可以产生**协变参数类型**

**协变返回类型**是在Java SE5中引入的



使用自限定类型，和普通的继承机制的区别，方法覆盖和方法重载。



### 动态类型安全



## 15.15 混型

最基本概念：混合多个类的能力以产生一个可以表示混型中所有类型的类，





潜在类型机制或者结构化类型机制

Python和C++支持潜在类型机制，Python是动态类型语言（所有的类型检查都发生在运行时），C++是静态类型语言（类型检查发生在编译期），潜在类型机制不要求静态或冬天类型检查

Ruby   Smalltalk  语言也支持潜在类型检查

Python支持正则（非成员）函数

Java不支持潜在类型机制，



## 15.17 对缺乏潜在类型机制的补偿



## 潜在类型机制

适配器设计模式

功能型编程风格



# 16.数组

数组与其他种类的容器之间的区别：

- 效率
- 类型
- 保存基本类型的能力

Java中，数组是一种效率最高的存储和随机访问对象引用序列的方式，

速度快的原因：简单的线性序列，  

付出代价：数组对象的大小被固定，并且在其生命周期中不可改变

如果编译期就能够指出错误，会显得更加优雅

数组可以持有基本类型，而泛型之前的容器则不能，有了泛型，可以指定并检查所持有对象的类型，并且有了自动包装机制，容器看起来还能够持有基本类型

## 16.2 数组是第一级对象

无论什么类型的数组，数组标识符是一个引用，指向在堆中创建的一个真实对象，这个数组对象来保存指向其他对象的引用。

只读成员length是数组对象的一部分（事实上，是唯一一个可以访问的字段或者方法）

length是数组的大小，而不是实际保存的元素个数

```
新生成的一个数组对象时，其中所有的引用被自动初始化为null
基本类型的数组：
1、数值型自动初始化为0
2、字符型（char）的，就自动初始化为（char）O
3、布尔型（boolean）----> false
```

指针和引用

```
指针是一个对象，利用地址，他的值直接指向存在电脑中另一个地方的值。在使用一个指针时，一个程序可以直接使用这个指针所存储的内存地址，又可以使用这个地址里存储的函数的值
```



## 16.5 数组与泛型

不支持实例化具有参数化类型的数组；

```java
Peel<Banana>[] pells = new Peel<Banana>[10];
```

擦除会移除参数信息，数组必须要知道持有的确切类型，以强制保证类型安全，以上不成立

参数化数组本身：

T[] 

不能创建泛型数组这一说法不十分准确：

可以创建对这种数组的引用

List<String>[] ls;        

```java
List<String>[] ls;//创建引用
List la = new List[10];//创建非泛型的数组
ls = (List<String>[]) la;//转型成泛型的数组
ls[0] = new ArrayList<String>();
```

## Arrays实用功能

### 数组拷贝

System.arraycopy()，复制数组比用for循环复制要快的多，针对所有类型做了重载

如果复制对象数组，只是复制了对象的引用，浅复制或者浅拷贝（shallow copy）

### 数组比较

Arrays.equals()，针对所有基本类型与Object都做了重载  

数组相等的条件是元素个数必须相等，并且对应位置的元素也相等，通过对每个元素使用equals方法比较（基本类型，使用基本类型的包装器类的equals方法）

### 数组元素的比较

程序设计的基本目标是“将保持不变的事物与会发生改变的事物相分离”

### 数组排序

排序的数组对象实现了Comparable接口或者具有相关联的Comparator

### 在已排序的数组中查找

排好序的数组可以使用Arrays.binarySearch()执行快速查找。

未排序的数组使用binarySearch()，将产生不可预料的结果

找到目标元素，产生的返回值等于或大于0，否则为负值，这个值表示位置的信息，如果数组中所有的元素都小于要查找的对象，插入点就等于a.size()，对于包含了重复元素，无法保证找到的是这些副本中的哪一个



# 17.容器深入研究

```java
Object.toString方法产生该对象的散列码的无符号十六进制表示（通过hashCode()生成的
```

所有的Collection子类型都刻意接收另一个Collection对象的构造器，用所接收的Collection对象中的元素来填充新的容器

### 17.2.3 Abstract类

享元模式

```

```

## 17.3 Collection的功能方法

### 未获支持操作

`UnsupportedOperationException`

## 17.5 List

### LinkedList

链表不支持快速的随机访问，如果需要查看链表中第n个元素，就必须从头开始，越过n-1个元素

## 17.6 Set和存储顺序

| Set(interface)  | 存入Set的每个元素都必须是唯一的，Set不保存重复元素，加入Set的元素必须定义equals()方法以确保对象的唯一性 |
| --------------- | ------------------------------------------------------------ |
| `HashSet`       | 为快速查找而设计的Set。存入`HashSet`的元素必须定义`hashCode()` |
| `TreeSet`       | 保持次序的Set，底层为树结构。使用它可以从Set中提取有序的序列。元素必须实现Comparable接口 |
| `LinkedHashSet` | 具有`HashSet`的查询速度，且内部使用链表维护元素的顺序(插入的次序)。迭代器遍历Set时，会按照元素插入的次序显示。元素必须定义`hashCode()`方法 |

`HashSet`对速度进行了优化

良好的编程风格而言，覆盖equals()时同事覆盖`hashCode()`方法

### `SortedSet`

`SortedSet`的`comparator()`，返回当天Set使用的`Comparator`；或者返回null，表示自然排序

`SortedSet`实现排序的原理：

```

```

## 17.7 队列

> 队列通常有两种实现方式：一种是使用循环数组，另一种是使用链表

### 优先级队列

### 双向队列

双向队列可以在任何一端添加或移除元素

## 17.8 Map

### 性能

在get()中使用线性搜索时，执行速度会相当的慢，HashMap使用特殊的值，称作散列码，来取代对健的缓慢搜索。

**散列码是“相对唯一”的、用以代表对象的int值，它是通过将该对象的某些信息进行转换而生成的。**

hashCode()是根类Object中的方法，因此所有Java对象都能产生散列码。

HashMap就是使用对象的hashCode进行快速查询的。此方法能够显著提高性能。





| 类别              | 特点 |
| ----------------- | ---- |
| HashMap           |      |
| LinkedHashMap     |      |
| TreeMap           |      |
| WeekHashMap       |      |
| ConcurrentHashMap |      |
| IdenityHashmap    |      |

### SortedMap

### LinkedHashMap

为了提高速度，LinkedHashMap散列化所有的元素，但遍历键值对时，却又以元素的插入顺序返回键值对 

## 17.9 散列与散列码



# 18.Java I/O系统



# 19.枚举类型

所有的enum都继承自java.lang.Enum类，java不支持多重继承，所有enum不能再继承其他的类

可以实现接口

枚举的枚举



# 20.注解
# 21.并发

## JMM

JMM(Java Memory Model,JMM)：Java虚拟机规范中定义了Java内存模型（Java Memory Model，JMM），用于==屏蔽掉各种硬件和操作系统的内存访问差异==，以实现让Java程序在各种平台下都能达到一致的并发效果，JMM规范了Java虚拟机与计算机内存是如何协同工作的：规定了一个线程如何和何时可以看到由其他线程修改过后的共享变量的值，以及在必须时如何同步的访问共享变量。

原始的Java内存模型存在一些不足，因此Java内存模型在Java1.5时被重新修订。这个版本的Java内存模型在Java8中仍然在使用。

Java内存模型（不仅仅是JVM内存分区）：调用栈和本地变量存放在线程栈上，对象存放在堆上。



- 一个本地变量可能是原始类型，在这种情况下，它总是“呆在”线程栈上。

- 一个本地变量也可能是指向一个对象的一个引用。在这种情况下，引用（这个本地变量）存放在线程栈上，但是对象本身存放在堆上。

- 一个对象可能包含方法，这些方法可能包含本地变量。这些本地变量仍然存放在线程栈上，即使这些方法所属的对象存放在堆上。

- 一个对象的成员变量可能随着这个对象自身存放在堆上。不管这个成员变量是原始类型还是引用类型。

- 静态成员变量跟随着类定义一起也存放在堆上。

- 存放在堆上的对象可以被所有持有对这个对象引用的线程访问。当一个线程可以访问一个对象时，它也可以访问这个对象的成员变量。如果两个线程同时调用同一个对象上的同一个方法，它们将会都访问这个对象的成员变量，但是每一个线程都拥有这个成员变量的私有拷贝。

#### 硬件内存架构

  现代硬件内存模型与Java内存模型有一些不同，理解内存模型架构以及Java内存模型如何与它协同工作也是非常重要的。

  现代计算机硬件架构的简单图示：

  ![img](/assets/v2-67833188e191c5e7a11d34e613ca352c_r.jpg)

  - **多CPU**：一个现代计算机通常由两个或者多个CPU。其中一些CPU还有多核。从这一点可以看出，在一个有两个或者多个CPU的现代计算机上同时运行多个线程是可能的。每个CPU在某一时刻运行一个线程是没有问题的。这意味着，如果你的Java程序是多线程的，在你的Java程序中每个CPU上一个线程可能同时（并发）执行。

  - **CPU寄存器**：每个CPU都包含一系列的寄存器，它们是CPU内内存的基础。CPU在寄存器上执行操作的速度远大于在主存上执行的速度。这是因为CPU访问寄存器的速度远大于主存。
  - **高速缓存cache**：由于计算机的存储设备与处理器的运算速度之间有着几个数量级的差距，所以现代计算机系统都不得不加入一层读写速度尽可能接近处理器运算速度的高速缓存（Cache）来作为内存与处理器之间的缓冲：将运算需要使用到的数据复制到缓存中，让运算能快速进行，当运算结束后再从缓存同步回内存之中，这样处理器就无须等待缓慢的内存读写了。CPU访问缓存层的速度快于访问主存的速度，但通常比访问内部寄存器的速度还要慢一点。每个CPU可能有一个CPU缓存层，一些CPU还有多层缓存。在某一时刻，一个或者多个缓存行（cache lines）可能被读到缓存，一个或者多个缓存行可能再被刷新回主存。
  - **内存**：一个计算机还包含一个主存。所有的CPU都可以访问主存。主存通常比CPU中的缓存大得多。
  - **运作原理**：通常情况下，当一个CPU需要读取主存时，它会将主存的部分读到CPU缓存中。它甚至可能将缓存中的部分内容读到它的内部寄存器中，然后在寄存器中执行操作。当CPU需要将结果写回到主存中去时，它会将内部寄存器的值刷新到缓存中，然后在某个时间点将值刷新回主存。

#### 一些问题：（多线程环境下尤其）

  - **缓存一致性问题**：在多处理器系统中，每个处理器都有自己的高速缓存，而它们又共享同一主内存（MainMemory）。基于高速缓存的存储交互很好地解决了处理器与内存的速度矛盾，但是也引入了新的问题：缓存一致性（CacheCoherence）。当多个处理器的运算任务都涉及同一块主内存区域时，将可能导致各自的缓存数据不一致的情况，如果真的发生这种情况，那同步回到主内存时以谁的缓存数据为准呢？为了解决一致性的问题，需要各个处理器访问缓存时都遵循一些协议，在读写时要根据协议来进行操作，这类协议有MSI、MESI（IllinoisProtocol）、MOSI、Synapse、Firefly及DragonProtocol，等等：
  - ![img](../../../%E6%95%B4%E7%90%86%E7%AC%94%E8%AE%B0/%E7%A8%8B%E5%BA%8F/java%E7%BC%96%E7%A8%8B%E6%80%9D%E6%83%B3/assets/v2-1a021d2833b7a537dcdfdf0025f52a6c_r.jpg)
  - **指令重排序问题**：为了使得处理器内部的运算单元能尽量被充分利用，处理器可能会对输入代码进行乱序执行（Out-Of-Order Execution）优化，处理器会在计算之后将乱序执行的结果重组，保证该结果与顺序执行的结果是一致的，但并不保证程序中各个语句计算的先后顺序与输入代码中的顺序一致。因此，如果存在一个计算任务依赖另一个计算任务的中间结果，那么其顺序性并不能靠代码的先后顺序来保证。与处理器的乱序执行优化类似，Java虚拟机的即时编译器中也有类似的指令重排序（Instruction Reorder）优化

#### Java内存模型和硬件内存架构之间的桥接

Java内存模型与硬件内存架构之间存在差异。硬件内存架构没有区分线程栈和堆。对于硬件，所有的线程栈和堆都分布在主内存中。部分线程栈和堆可能有时候会出现在CPU缓存中和CPU内部的寄存器中。如下图所示：

![img](assets/v2-1a7b7bb752799b6c067a0eaca0a1a9b2_r.jpg)



从抽象的角度来看，JMM定义了线程和主内存之间的抽象关系：

- 线程之间的共享变量存储在主内存（Main Memory）中
- 每个线程都有一个私有的本地内存（Local Memory），本地内存是JMM的一个抽象概念，并不真实存在，它涵盖了缓存、写缓冲区、寄存器以及其他的硬件和编译器优化。本地内存中存储了该线程以读/写共享变量的拷贝副本。
- 从更低的层次来说，主内存就是硬件的内存，而为了获取更好的运行速度，虚拟机及硬件系统可能会让工作内存优先存储于寄存器和高速缓存中。
- Java内存模型中的线程的工作内存（working memory）是cpu的寄存器和高速缓存的抽象描述。而JVM的静态内存储模型（JVM内存模型）只是一种对内存的物理划分而已，它只局限在内存，而且只局限在JVM的内存。

![img](assets/v2-af520d543f0f4f205f822ec3b151ad46_r.jpg)

![img](assets/v2-037270b0876b6af680d1832bcc9dca32_r.jpg)



#### JMM模型下的线程间通信

线程间通信必须要经过主内存。

如下，如果线程A与线程B之间要通信的话，必须要经历下面2个步骤：

1）线程A把本地内存A中更新过的共享变量刷新到主内存中去。

2）线程B到主内存中去读取线程A之前已更新过的共享变量。

![img](assets/v2-8750cb14ecaa93509e3f1981563513e1_r.jpg)

关于主内存与工作内存之间的具体交互协议，即一个变量如何从主内存拷贝到工作内存、如何从工作内存同步到主内存之间的实现细节，Java内存模型定义了以下八种操作来完成：

- **lock（锁定）**：作用于主内存的变量，把一个变量标识为一条线程独占状态。
- **unlock（解锁）**：作用于主内存变量，把一个处于锁定状态的变量释放出来，释放后的变量才可以被其他线程锁定。
- **read（读取）**：作用于主内存变量，把一个变量值从主内存传输到线程的工作内存中，以便随后的load动作使用
- **load（载入）**：作用于工作内存的变量，它把read操作从主内存中得到的变量值放入工作内存的变量副本中。
- **use（使用）**：作用于工作内存的变量，把工作内存中的一个变量值传递给执行引擎，每当虚拟机遇到一个需要使用变量的值的字节码指令时将会执行这个操作。
- **assign（赋值）**：作用于工作内存的变量，它把一个从执行引擎接收到的值赋值给工作内存的变量，每当虚拟机遇到一个给变量赋值的字节码指令时执行这个操作。
- **store（存储）**：作用于工作内存的变量，把工作内存中的一个变量的值传送到主内存中，以便随后的write的操作。
- **write（写入）**：作用于主内存的变量，它把store操作从工作内存中一个变量的值传送到主内存的变量中。

Java内存模型还规定了在执行上述八种基本操作时，必须满足如下规则：

- 如果要把一个变量从主内存中复制到工作内存，就需要按顺寻地执行read和load操作， 如果把变量从工作内存中同步回主内存中，就要按顺序地执行store和write操作。但Java内存模型只要求上述操作必须按顺序执行，而没有保证必须是连续执行。
- 不允许read和load、store和write操作之一单独出现
- 不允许一个线程丢弃它的最近assign的操作，即变量在工作内存中改变了之后必须同步到主内存中。
- 不允许一个线程无原因地（没有发生过任何assign操作）把数据从工作内存同步回主内存中。
- 一个新的变量只能在主内存中诞生，不允许在工作内存中直接使用一个未被初始化（load或assign）的变量。即就是对一个变量实施use和store操作之前，必须先执行过了assign和load操作。
- 一个变量在同一时刻只允许一条线程对其进行lock操作，但lock操作可以被同一条线程重复执行多次，多次执行lock后，只有执行相同次数的unlock操作，变量才会被解锁。lock和unlock必须成对出现
- 如果对一个变量执行lock操作，将会清空工作内存中此变量的值，在执行引擎使用这个变量前需要重新执行load或assign操作初始化变量的值
- 如果一个变量事先没有被lock操作锁定，则不允许对它执行unlock操作；也不允许去unlock一个被其他线程锁定的变量。
- 对一个变量执行unlock操作之前，必须先把此变量同步到主内存中（执行store和write操作）。

#### Java内存模型解决的问题

当对象和变量被存放在计算机中各种不同的内存区域中时，就可能会出现一些具体的问题。Java内存模型建立所围绕的问题：在多线程并发过程中，如何处理多线程读同步问题与可见性（多线程缓存与指令重排序）、多线程写同步问题与原子性（多线程竞争race condition）。

**1、多线程读同步与可见性**

**可见性（共享对象可见性）**：线程对共享变量修改的可见性。当一个线程修改了共享变量的值，其他线程能够立刻得知这个修改

**线程缓存导致的可见性问题：**

如果两个或者更多的线程在没有正确的使用volatile声明或者同步的情况下共享一个对象，一个线程更新这个共享对象可能对其它线程来说是不可见的：共享对象被初始化在主存中。跑在CPU上的一个线程将这个共享对象读到CPU缓存中，然后修改了这个对象。只要CPU缓存没有被刷新会主存，对象修改后的版本对跑在其它CPU上的线程都是不可见的。这种方式可能导致每个线程拥有这个共享对象的私有拷贝，每个拷贝停留在不同的CPU缓存中。

下图示意了这种情形。跑在左边CPU的线程拷贝这个共享对象到它的CPU缓存中，然后将count变量的值修改为2。这个修改对跑在右边CPU上的其它线程是不可见的，因为修改后的count的值还没有被刷新回主存中去。

![img](assets/v2-7abd7500588012315f4f0e068e20e341_r.jpg)

解决这个内存可见性问题你可以使用：

- Java中的volatile关键字：volatile关键字可以保证直接从主存中读取一个变量，如果这个变量被修改后，总是会被写回到主存中去。Java内存模型是通过在变量修改后将新值同步回主内存，在变量读取前从主内存刷新变量值这种依赖主内存作为传递媒介的方式来实现可见性的，无论是普通变量还是volatile变量都是如此，普通变量与volatile变量的区别是：volatile的特殊规则保证了新值能立即同步到主内存，以及每个线程在每次使用volatile变量前都立即从主内存刷新。因此我们可以说volatile保证了多线程操作时变量的可见性，而普通变量则不能保证这一点。
- Java中的synchronized关键字：同步快的可见性是由“如果对一个变量执行lock操作，将会清空工作内存中此变量的值，在执行引擎使用这个变量前需要重新执行load或assign操作初始化变量的值”、“对一个变量执行unlock操作之前，必须先把此变量同步回主内存中（执行store和write操作）”这两条规则获得的。
- Java中的final关键字：final关键字的可见性是指，被final修饰的字段在构造器中一旦被初始化完成，并且构造器没有把“this”的引用传递出去（this引用逃逸是一件很危险的事情，其他线程有可能通过这个引用访问到“初始化了一半”的对象），那么在其他线程就能看见final字段的值（无须同步）

**重排序导致的可见性问题：**

Java程序中天然的有序性可以总结为一句话：如果在本地线程内观察，所有操作都是有序的（“线程内表现为串行”(Within-Thread As-If-Serial Semantics)）；如果在一个线程中观察另一个线程，所有操作都是无序的（“指令重排序”现象和“线程工作内存与主内存同步延迟”现象）。

Java语言提供了volatile和synchronized两个关键字来保证线程之间操作的有序性：

- volatile关键字本身就包含了禁止指令重排序的语义
- synchronized则是由“一个变量在同一个时刻只允许一条线程对其进行lock操作”这条规则获得的，这个规则决定了持有同一个锁的两个同步块只能串行地进入

**指令序列的重排序：**

1）编译器优化的重排序。编译器在不改变单线程程序语义的前提下，可以重新安排语句的执行顺序。

2）指令级并行的重排序。现代处理器采用了指令级并行技术（Instruction-LevelParallelism，ILP）来将多条指令重叠执行。如果不存在数据依赖性，处理器可以改变语句对应机器指令的执行顺序。

3）内存系统的重排序。由于处理器使用缓存和读/写缓冲区，这使得加载和存储操作看上去可能是在乱序执行。

![img](assets/v2-a92ef160e8ba8d33541fb57b8a32de9c_r.jpg)

每个处理器上的写缓冲区，仅仅对它所在的处理器可见。这会导致处理器执行内存操作的顺序可能会与内存实际的操作执行顺序不一致。由于现代的处理器都会使用写缓冲区，因此现代的处理器都会允许对写-读操作进行重排序：

![img](assets/v2-f8a75081bcad888a7e73b4785a672e5b_r.jpg)

**数据依赖：**

编译器和处理器在重排序时，会遵守数据依赖性，编译器和处理器不会改变存在数据依赖关系的两个操作的执行顺序。（这里所说的数据依赖性仅针对单个处理器中执行的指令序列和单个线程中执行的操作，不同处理器之间和不同线程之间的数据依赖性不被编译器和处理器考虑）

![img](assets/v2-36500a7455955c58d02138913d5c0cd7_r.jpg)

**指令重排序对内存可见性的影响：**

![img](assets/v2-8ef063a1b514d9cfbdf059984f83ed2f_r.jpg)

当1和2之间没有数据依赖关系时，1和2之间就可能被重排序（3和4类似）。这样的结果就是：读线程B执行4时，不一定能看到写线程A在执行1时对共享变量的修改。

**指令重排序改变多线程程序的执行结果例子：**

![img](assets/v2-111bfd93bcd92fd2ee495a12cb34f9aa_hd.jpg)

flag变量是个标记，用来标识变量a是否已被写入。这里假设有两个线程A和B，A首先执行writer()方法，随后B线程接着执行reader()方法。线程B在执行操作4时，能否看到线程A在操作1对共享变量a的写入呢？

答案是：不一定能看到。

由于操作1和操作2没有数据依赖关系，编译器和处理器可以对这两个操作重排序；同样，操作3和操作4没有数据依赖关系，编译器和处理器也可以对这两个操作重排序。

**as-if-serial语义：**

不管怎么重排序（编译器和处理器为了提高并行度），（单线程）程序的执行结果不能被改变。（编译器、runtime和处理器都必须遵守as-if-serial语义）

**happens before：**

从JDK 5开始，Java使用新的JSR-133内存模型，JSR-133使用happens-before的概念来阐述操作之间的内存可见性：在JMM中，如果一个操作执行的结果需要对另一个操作可见（两个操作既可以是在一个线程之内，也可以是在不同线程之间），那么这两个操作之间必须要存在happens-before关系：

- 程序顺序规则：一个线程中的每个操作，happens-before于该线程中的任意后续操作。
- 监视器锁规则：对一个锁的解锁，happens-before于随后对这个锁的加锁。
- volatile变量规则：对一个volatile域的写，happens-before于任意后续对这个volatile域的读。
- 传递性：如果A happens-before B，且B happens-before C，那么A happens-before C。

一个happens-before规则对应于一个或多个编译器和处理器重排序规则

**内存屏障禁止特定类型的处理器重排序：**

重排序可能会导致多线程程序出现内存可见性问题。对于处理器重排序，JMM的处理器重排序规则会要求Java编译器在生成指令序列时，插入特定类型的内存屏障（Memory Barriers，Intel称之为Memory Fence）指令，通过内存屏障指令来禁止特定类型的处理器重排序。通过禁止特定类型的编译器重排序和处理器重排序，为程序员提供一致的内存可见性保证。

为了保证内存可见性，Java编译器在生成指令序列的适当位置会插入内存屏障指令来禁止特定类型的处理器重排序。

![img](assets/v2-6db326ce298332a673151117edcb1fcd_r.jpg)

StoreLoad Barriers是一个“全能型”的屏障，它同时具有其他3个屏障的效果。现代的多处理器大多支持该屏障（其他类型的屏障不一定被所有处理器支持）。执行该屏障开销会很昂贵，因为当前处理器通常要把写缓冲区中的数据全部刷新到内存中（Buffer Fully Flush）。

**2、多线程写同步与原子性**

**多线程竞争（Race Conditions）问题**：当读，写和检查共享变量时出现race conditions。

如果两个或者更多的线程共享一个对象，多个线程在这个共享对象上更新变量，就有可能发生race conditions。

想象一下，如果线程A读一个共享对象的变量count到它的CPU缓存中。再想象一下，线程B也做了同样的事情，但是往一个不同的CPU缓存中。现在线程A将count加1，线程B也做了同样的事情。现在count已经被增加了两次，每个CPU缓存中一次。如果这些增加操作被顺序的执行，变量count应该被增加两次，然后原值+2被写回到主存中去。然而，两次增加都是在没有适当的同步下并发执行的。无论是线程A还是线程B将count修改后的版本写回到主存中取，修改后的值仅会被原值大1，尽管增加了两次：

![img](assets/v2-02ae4be429d4b48a18442efe91131155_r.jpg)

解决这个问题可以使用Java同步块。一个同步块可以保证在同一时刻仅有一个线程可以进入代码的临界区。同步块还可以保证代码块中所有被访问的变量将会从主存中读入，当线程退出同步代码块时，所有被更新的变量都会被刷新回主存中去，不管这个变量是否被声明为volatile。

**使用原子性保证多线程写同步问题：**

**原子性：**指一个操作是按原子的方式执行的。要么该操作不被执行；要么以原子方式执行，即执行过程中不会被其它线程中断。

- Reads and writes are atomic for reference variables and for most primitive variables (all types except long and double).
- Reads and writes are atomic for all variables declared **volatile** (including long and double variables).

（[https://docs.oracle.com/javase/tutorial/essential/concurrency/atomic.html](https://link.zhihu.com/?target=https%3A//docs.oracle.com/javase/tutorial/essential/concurrency/atomic.html)）

**实现原子性：**

- 由Java内存模型来直接保证的原子性变量操作包括read、load、assign、use、store、write，我们大致可以认为基本数据类型变量、引用类型变量、声明为volatile的任何类型变量的访问读写是具备原子性的（long和double的非原子性协定：对于64位的数据，如long和double，Java内存模型规范允许虚拟机将没有被volatile修饰的64位数据的读写操作划分为两次32位的操作来进行，即允许虚拟机实现选择可以不保证64位数据类型的load、store、read和write这四个操作的原子性，即如果有多个线程共享一个并未声明为volatile的long或double类型的变量，并且同时对它们进行读取和修改操作，那么某些线程可能会读取到一个既非原值，也不是其他线程修改值的代表了“半个变量”的数值。但由于目前各种平台下的商用虚拟机几乎都选择把64位数据的读写操作作为原子操作来对待，因此在编写代码时一般也不需要将用到的long和double变量专门声明为volatile）。这些类型变量的读、写天然具有原子性，但类似于 “基本变量++” / “volatile++” 这种复合操作并没有原子性。
- 如果应用场景需要一个更大范围的原子性保证，需要使用同步块技术。Java内存模型提供了lock和unlock操作来满足这种需求。虚拟机提供了字节码指令monitorenter和monitorexist来隐式地使用这两个操作，这两个字节码指令反映到Java代码中就是同步快——synchronized关键字。

#### JMM对特殊Java语义的特殊规则支持

[volatile总结](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI3NzM2OTQ5Mg%3D%3D%26mid%3D2247484289%26idx%3D1%26sn%3Dbdf6721e01c613bfb1458a8584e80800%26chksm%3Deb66047adc118d6c395c14e5b953686bfdfac93fd6fa8c0731bb89aadd7437bba800d034659d%26scene%3D21%23wechat_redirect) （保证内存可见性：Lock前缀的指令、内存屏障禁止重排序）

[synchronized总结](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzI3NzM2OTQ5Mg%3D%3D%26mid%3D2247484280%26idx%3D1%26sn%3D8de305338c5ab348c3e2a784084e4306%26chksm%3Deb660483dc118d95e9bcde15a01103f818ed2fd399989f36dc2d57740a305e91cf986d4f5a64%26scene%3D21%23wechat_redirect) （保证内存可见性和操作原子性：互斥锁；锁优化）









### java多线程的三大核心

```java
> 原子性
> 可见性
> 顺序性
```

### 原子性

`Java` 的原子性就和数据库事务的原子性差不多，一个操作中要么全部执行成功或者失败。

`JMM` 只是保证了基本的原子性，但类似于 `i++` 之类的操作，看似是原子操作，其实里面涉及到:

- 获取 i 的值。
- 自增。
- 再赋值给 i。

这三步操作，所以想要实现 `i++` 这样的原子操作就需要用到 `synchronized` 或者是 `lock` 进行加锁处理。

如果是基础类的自增操作可以使用 `AtomicInteger` 这样的原子类来实现(其本质是利用了 `CPU` 级别的 的 `CAS` 指令来完成的)。

其中用的最多的方法就是: `incrementAndGet()` 以原子的方式自增。 源码如下:

```java
public final long incrementAndGet() {
        for (;;) {
            long current = get();
            long next = current + 1;
            if (compareAndSet(current, next))
                return next;
        }
    }
```

首先是获得当前的值，然后自增 +1。接着则是最核心的 `compareAndSet() `来进行原子更新。

```java
public final boolean compareAndSet(long expect, long update) {
        return unsafe.compareAndSwapLong(this, valueOffset, expect, update);
    }
```

其逻辑就是判断当前的值是否被更新过，是否等于 `current`，如果等于就说明没有更新过然后将当前的值更新为 `next`，如果不等于则返回`false` 进入循环，直到更新成功为止。

还有其中的 `get()` 方法也很关键，返回的是当前的值，当前值用了 `volatile` 关键词修饰，保证了内存可见性。

```java
 private volatile int value;
```



### 可见性

现代计算机中，由于 `CPU` 直接从主内存中读取数据的效率不高，所以都会对应的 `CPU` 高速缓存，先将主内存中的数据读取到缓存中，线程修改数据之后首先更新到缓存，之后才会更新到主内存。如果此时还没有将数据更新到主内存其他的线程此时来读取就是修改之前的数据。

![img](assets/68747470733a2f2f7773322e73696e61696d672e636e2f6c617267652f303036744b6654636c7931666d6f75753366706f6b6a33316165306f736a74312e6a7067.jpg)

如上图所示。

`volatile` 关键字就是用于保证内存可见性，当线程A更新了 volatile 修饰的变量时，它会立即刷新到主线程，并且将其余缓存中该变量的值清空，导致其余线程只能去主内存读取最新值。

使用 `volatile` 关键词修饰的变量每次读取都会得到最新的数据，不管哪个线程对这个变量的修改都会立即刷新到主内存。

`synchronized`和加锁也能能保证可见性，实现原理就是在释放锁之前其余线程是访问不到这个共享变量的。但是和 `volatile` 相比开销较大。



### 顺序性

以下这段代码:

```java
int a = 100 ; //1
int b = 200 ; //2
int c = a + b ; //3
```

正常情况下的执行顺序应该是 `1>>2>>3`。但是有时 `JVM` 为了提高整体的效率会进行==指令重排==导致执行的顺序可能是 `2>>1>>3`。但是 `JVM` 也不能是什么都进行重排，是在保证最终结果和代码顺序执行结果一致的情况下才可能进行重排。

重排在单线程中不会出现问题，但在多线程中会出现数据不一致的问题。

Java 中可以使用 `volatile` 来保证顺序性，`synchronized 和 lock` 也可以来保证有序性，和保证原子性的方式一样，通过同一段时间只能一个线程访问来实现的。

除了通过 `volatile` 关键字显式的保证顺序之外， `JVM` 还通过 `happen-before` 原则来隐式的保证顺序性。

其中有一条就是适用于 `volatile` 关键字的，针对于 `volatile` 关键字的写操作肯定是在读操作之前，也就是说读取的值肯定是最新的。

### volatile 的应用

#### 双重检查锁的单例模式

可以用 `volatile` 实现一个双重检查锁的单例模式：

```java
  public class Singleton {
        private static volatile Singleton singleton;

        private Singleton() {
        }

        public static Singleton getInstance() {
            if (singleton == null) {
                synchronized (Singleton.class) {
                    if (singleton == null) {
                        singleton = new Singleton();
                    }
                }
            }
            return singleton;
        }

    }
```

这里的 `volatile` 关键字主要是为了防止指令重排。 如果不用 `volatile` ，`singleton = new Singleton();`，这段代码其实是分为三步：

- 分配内存空间。(1)
- 初始化对象。(2)
- 将 `singleton` 对象指向分配的内存地址。(3)

加上 `volatile` 是为了让以上的三步操作顺序执行，反之有可能第三步在第二步之前被执行就有可能导致某个线程拿到的单例对象还没有初始化，以致于使用报错。

#### 控制停止线程的标记

```java
  private volatile boolean flag ;
    private void run(){
        new Thread(new Runnable() {
            @Override
            public void run() {
                while (flag) {
                    doSomeThing();
                }
            }
        });
    }

    private void stop(){
        flag = false ;
    }
```



这里如果没有用 volatile 来修饰 flag ，就有可能其中一个线程调用了 `stop()`方法修改了 flag 的值并不会立即刷新到主内存中，导致这个循环并不会立即停止。

这里主要利用的是 `volatile` 的内存可见性。

总结一下:

- `volatile` 关键字只能保证可见性，顺序性，**不能保证原子性**。

### 异步同步，阻塞和非阻塞

#### 1.同步与异步

同步和异步关注的是**消息通信机制** (synchronous communication/ asynchronous communication)

#### 2.阻塞与非阻塞

阻塞和非阻塞关注的是**程序在等待调用结果（消息，返回值）时的状态.**



`unix`网络编程中将IO模型分为5类：阻塞IO，非阻塞IO，IO复用，信号驱动，异步IO。

1. 阻塞IO就是那种recv, read，一直等，等到有了数据才返回；
2. 非阻塞IO就是立即返回，设置描述符为非阻塞，但是要进程自己一直检查是否可读；
3. IO复用其实也是阻塞的，不过可以用来等很多描述符，比起阻塞有了进步，可以算有点异步了，但需要阻塞着检查是否可读。**对同一个描述符的IO操作也是有序的。**
4. 信号驱动采用信号机制等待，有了更多的进步，不用监视描述符了，而且不用阻塞着等待数据到来，被动等待信号通知，由信号处理程序处理。**但对同一个描述符的IO操作还是有序的。**
5. 异步IO，发送IO请求后，不用等了，也不再需要发送IO请求获取结果了。等到通知后，其实是系统帮你把数据读取好了的，**你等到的通知也不再是要求你去读写IO了，而是告诉你IO请求过程已经结束了**。你要做的就是可以处理数据了。且同一个描述符上可能同时存在很多请求。(对应上面那个买书例子中，就是送书到我家，我直接看书就行了，不需要再去跑一趟了)。

其中IO服用和信号驱动，在处理业务逻辑上可以说有异步，但在IO操作层面上来说还是同步的

posix.1严格定义的异步IO是要求没有任何一点阻塞，而上述的前面四个（阻塞IO，非阻塞IO，IO复用，信号驱动）都不同程度阻塞了，而且都有一个共同的阻塞： 内核拷贝数据到进程空间的这段时间需要等待。

# 22.图形化用户界面  

 







# JMX

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





[TOC]

# 5/12

## transient关键字



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



# 7/2 





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





![](/home/klaus/work_dir/note/program/基础知识/demo.assets/微信图片_20191118210932.jpg)



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
2.  getRawType()---获取声明泛型的类或者接口，也就是泛型中<>前面的那个值
3.  getOwnerType()---可以获取到内部类的“拥有者”；例如： Map 就是 Map.Entry<String,String>的拥有者

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



hashCode的默认实现是返回内存地址，这句话不对，具体方法返回看运行时库和JVM的具体实现

其实OPENJDK，hashCode就有五种



# J2EE的13种规范

Java 提供了很多服务提供者接口(Service Provider Interface，SPI)，允许第三方为这些接口提供实现。常见的 SPI 有 JDBC、JNDI、JAXP 等，这些SPI的接口由核心类库提供，却由第三方实现，这样就存在一个问题：SPI 的接口是 Java 核心库的一部分，是由BootstrapClassLoader加载的；SPI实现的Java类一般是由AppClassLoader来加载的。BootstrapClassLoader是无法找到 SPI 的实现类的，因为它只加载Java的核心库。它也不能代理给AppClassLoader，



1.JDBC(JavaDatabase Connectivity)

JDBC是以统一方式访问数据库的API.

它提供了独立于平台的数据库访问,也就是说,有了JDBC API,我们就不必为访问Oracle数据库专门写一个程序,为访问Sybase数据库又专门写一个程序等等,只需要用JDBC API写一个程序就够了,它可以向相应数据库发送SQL调用.JDBC是Java应用程序与各种不同数据库之间进行对话的方法的机制.简单地说,它做了三件事:与数据库建立连接--发送操作数据库的语句--处理结果.

 

2.JNDI(JavaName and Directory Interface)

JNDI是一组在Java应用中访问命名和目录服务的API.

(命名服务将名称和对象联系起来,我们即可用名称访问对象.JNDI允许把名称同Java对象或资源关联起来,建立逻辑关联,而不必知道对象或资源的物理ID.)JNDI为开发人员提供了查找和访问各种命名和目录服务的通用,统一的接口,可访问的目录及服务如下表:

利用JNDI的命名与服务功能可满足企业级API对命名与服务的访问,诸如EJB,JMS,JDBC 2.0以及IIOP上的RMI通过JNDI来使用CORBA的命名服务.

JNDI和JDBC类似,都是构建在抽象层上.因为:

它提供了标准的独立于命名系统的API,这些API构建在命名系统之上.这一层有助于将应用与实际数据源分离,因此不管是访问的LDAP,RMI还是DNS.也就是说,JNDI独立于目录服务的具体实现,只要有目录的服务提供接口或驱动,就可以使用目录.

 

3.EJB(EnterpriseJavaBean)

J2EE将业务逻辑从客户端软件中抽取出来，封装在一个组件中。这个组件运行在一个独立的服务器上，客户端软件通过网络调用组件提供的服务以实现业务逻辑，而客户端软件的功能只是负责发送调用请求和显示处理结果。

在J2EE中，这个运行在一个独立的服务器上，并封装了业务逻辑的组件就是EJB组件。其实就是把原来放到客户端实现的代码放到服务器端，并依靠RMI进行通信。

 

4.RMI(Remote MethodInvoke)

是一组用户开发分布式应用程序的API.

这一协议调用远程对象上的方法使用了序列化的方式在客户端和服务器之间传递数据,使得原先的程序在同一操作系统的方法调用,变成了不同操作系统之间程序的方法调用,即RMI机制实现了程序组件在不同操作系统之间的通信.它是一种被EJB使用的更底层的协议.

RMI/JNI: RMI可利用标准Java本机方法接口与现有的和原有的系统相连接

RMI/JDBC: RMI利用标准JDBC包与现有的关系数据库连接

这就实现了与非Java语言的现有服务器进行通信.

 

5.JavaIDL/CORBA(Common Object Request BrokerArchitecture)

Java接口定义语言/公用对象请求代理程序体系结构

在JavaIDL的支持下，开发人员可以将Java和CORBA集成在一起。他们可以创建Java对象并使之可在CORBA ORB中展开,或者他们还可以创建Java类并作为和其它ORB一起展开的CORBA对象的客户。后一种方法提供了另外一种途径，通过它Java可以被用于将新的应用和旧的系统相集成。

CORBA是面向对象标准的第一步，有了这个标准，软件的实现与工作环境对用户和开发者不再重要，可以把精力更多地放在本地系统的实现与优化上。

 

6.JSP(Java Server Pages)

JSP页面=HTML+Java,其根本是一个简化的Servlet设计.

服务器在页面被客户端请求后,对这些Java代码进行处理,然后将执行结果连同原HTML代码生成的新HTML页面返回给客户端浏览器.

 

7.Java Servlet

Servlet是一种小型的Java程序,扩展了Web服务器的功能,作为一种服务器的应用,当被请求时开始执行.Servlet提供的功能大多和JSP类似,不过,JSP通常是大多数的HTML代码中嵌入少量的Java代码,而Servlet全部由Java写成并生成HTML.

 

8.XML

XML是一个用来定义其它标记语言的语言,可用作数据共享。XML的发展和Java是相互独立的。不过，它和Java具有的相同目标就是跨平台。通过将Java与XML结合，我们可以得到一个完全与平台无关的解决方案。

 

9.JMS(JavaMessage Service)

它是一种与厂商无关的API,用来访问消息收发系统消息.它类似于JDBC.JDBC是可以用来访问不同关系数据库的API,而JMS则提供同样与厂商无关的访问消息收发服务的方法,这样就可以通过消息收发服务实现从一个JMS客户机向另一个JMS客户机发送消息,所需要的是厂商支持JMS.换句话说,JMS是Java平台上有关面向消息中间件的技术规范.

 

10.JTA(JavaTransaction API)

定义了一种标准API,应用程序由此可以访问各种事务监控.它允许应用程序执行分布式事务处理--在两个或多个网络计算机资源上访问并且更新数据.JTA和JTS为J2EE 平台提供了分布式事务服务.

JTA事务比JDBC事务更强大,一个JTA事务可以有多个参与者,而一个JDBC事务则被限定在一个单一的数据库连接.

 

11.JTS(JavaTransaction Service)

JTS是CORBA OTS事务监控器的一个基本实现。JTS指定了一个事务管理器的实现（Transaction Manager），这个管理器在一个高级别上支持JTA规范，并且在一个低级别上实现了OMGOTS规范的Java映射。一个JTS事务管理器为应用服务器、资源管理器、standalone应用和通信资源管理器提供事务服务。

 

12.JavaMail

用于访问邮件服务器的API,提供了一套邮件服务器的抽象类.

 

13.JAF(JavaBeansActivation Framework)

JAF是一个专用的数据处理框架,它用于封装数据,并为应用程序提供访问和操作数据的接口.也就是说,JAF让Java程序知道怎么对一个数据源进行查看,编辑,打印等.

JavaMail利用JAF来处理MIME编码的邮件附件.