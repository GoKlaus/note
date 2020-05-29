## lambda表达式



## Stream编程



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

