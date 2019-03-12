# java编程思想
[TOC]
## 1.对象导论

## 2.一切都是对象
## 3.操作符
## 4.控制执行流程
## 5.初始化与清理
## 6.访问控制权限
## 7.复用类
## 8.多态
## 9.接口
## 10.内部类
## 11.持有对象
## 12.通过异常处理错误
## 13.字符串
### 不可变String
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
#### printf()用法
#### System.out.format()
#### Formatter类
Java中管理所有的格式化功能，可以看做一个**翻译器**。
#### 格式化说明符
#### String.format()
应用场景：只需要使用此意format()方法时，String.format()用起来更方便
#### 正则表达式
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


#### Pattern和Matcher
相比较于功能有限的String类，正则表达式对象功能更强大

### 扫描输入
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
#### 使用正则表达式扫描
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
### Class对象
Java使用Class对象来执行其RTTI
>类是程序的一部分，每个类都有一个Class对象，当编写并且编译了一个新类，就会产生一个Class对象(更恰当的说，是保存在一个同名的.class文件中)，为了生成这个对象，运行这个程序的Java虚拟机(JVM)将使用被称为"类加载器"的子系统
***
>类加载器子系统实际上可以包含一条类加载链，但是只有一个`原生类加载器`，他是JVM实现的一部分。原生类加载器加载的是所谓的`可信类`，包括Java API类，通常是通过本地盘加载的。在这条链中，通常是不需要添加额外的类加载器，但是如果你有特殊的需求，那么你有一种方式可以加载额外的类加载器
***
>所有的类都是在对其第一次使用的时候动态的加载到JVM中的，当程序创建第一个对类的静态成员的引用时，就会加载这个类。`这个证明构造器也是类的静态方法，即使在构造器之前并没有使用static关键字。因此使用new操作符创建类的新对象也会当做对类的静态成员的引用。`

因此，Java程序在它开始运行之前并非完全被加载。如果尚未加载，默认的类加载器就会根据类名查找.class文件。这个字节码被加载时，它们会接受验证，确保没有被破坏，并且不包含不良Java代码（这是Java中用于安全防范目的的措施之一）。一  
***

## 15.泛型
## 16.数组
## 17.容器深入研究
## 18.Java I/O系统
## 19.枚举类型
## 20.注解
## 21.并发
## 22.图形化用户界面