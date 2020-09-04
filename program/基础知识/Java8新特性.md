## lambda表达式



## Stream编程

Collector接口

```java
Supplier<A> supplier(); //提供一个Supplier 函数
BiConsumer<A, T> accumulator(); // 提供一个 BiConsumer 函数
BinaryOperator<A> combiner(); // 提供一个BinaryOperator 函数
Function<A, R> finisher(); // 提供一个 Function 函数
Set<Characteristics> characteristics();
```

Collectors类

提供一个Collector接口的实现类

```java
static class CollectorImpl<T, A, R> implements Collector<T, A, R> 
```

并且Collector接口提供静态方法

```java
public interface Collector {
  
  public static<T, R> Collector<T, R, R> of(Supplier<R> supplier,
                                              BiConsumer<R, T> accumulator,
                                              BinaryOperator<R> combiner,
                                              Characteristics... characteristics) {
        Objects.requireNonNull(supplier);
        Objects.requireNonNull(accumulator);
        Objects.requireNonNull(combiner);
        Objects.requireNonNull(characteristics);
        Set<Characteristics> cs = (characteristics.length == 0)
                                  ? Collectors.CH_ID
                                  : Collections.unmodifiableSet(EnumSet.of(Collector.Characteristics.IDENTITY_FINISH,
                                                                           characteristics));
        return new Collectors.CollectorImpl<>(supplier, accumulator, combiner, cs);
    }
}
```





## 接口的默认方法

```java
public interface DefaultFunctionInterface {
    default String defaultFunction() {
    	return "default function";
    }
}
```

定义静态方法

```java
public interface StaticFunctionInterface {
    static String staticFunction() {
    	return "static function";
    }
}

```



## 方法引用

### 构造器引用

Class::new， 或者Class<T>::new，要求构造器方法是没有参数的

### 静态方法引用

Class::static_method，要求接受Class类型的参数

### 特定类的任意对象方法引用

Class::method，要求方法是没有参数的

### 特定对象的方法引用

instance::method，要求方法接受一个参数，与上一个不同的地方在于，上一个是在列表元素上分别调用方法，而此是在某个对象上调用方法，将列表元素作为参数传入



## 重复注解



## 扩展注解的支持



## Optional



## Date/Time API



## JavaScript引擎Nashorn



## Base64

