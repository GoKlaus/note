# Effective-java #
[toc]

## chapter 01 ##

### 1. 考虑使用静态工厂方法替代构造方法 ###

优点：
第一个优点是，与构造方法不同，它们是有名字的。


``` java
public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
}
```

``` java
Calendar.getInstance();

```

第二个优点是，与构造方法不同，它们不需要每次调用时都创建一个新对象
静态工厂方法重复调用返回相同实例这个特点可以让类在任何时候都能对实例保持严格的控制。这样做的类被称为实例控制类（ instance-controlled）。


第三个优点是，与构造方法不同，它们可以返回其返回类型的任何子类型的对象。

第四个优点是返回对象的类可以根据输入参数的不同而不同。
第五个优点是，在编写包含该方法的类时，返回的对象的类不需要存在。

缺点：
没有公共或受保护构造方法的类不能被子类化。
藏在api文档里不容易发现


- from —— 类型转换方法，它接受单个参数并返回此类型的相应实例，例如：Date d = Date.from(instant);
- of —— 聚合方法，接受多个参数并返回该类型的实例，并把他们合并在一起，例如：Set faceCards = EnumSet.of(JACK, QUEEN, KING);
- valueOf —— from 和 to 更为详细的替代 方式，例如：BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);
- instance 或 getinstance —— 返回一个由其参数 (如果有的话) 描述的实例，但不能说它具有相同的值，例如：StackWalker luke = StackWalker.getInstance(options);
- create 或 newInstance —— 与 instance 或 getInstance 类似，除此之外该方法保证每次调用返回一个新的实例，例如：Object newArray = Array.newInstance(classObject, arrayLen);
- getType —— 与 getInstance 类似，但是在工厂方法处于不同的类中的时候使用。getType 中的 Type 是工厂方法返回的对象类型，例如：FileStore fs = Files.getFileStore(path);
- newType —— 与 newInstance 类似，但是在工厂方法处于不同的类中的时候使用。newType中的 Type 是工厂方法返回的对象类型，例如：BufferedReader br = Files.newBufferedReader(path);
- type —— getType 和 newType 简洁的替代方式，例如：List litany = Collections.list(legacyLitany);



服务提供者框架（service provider fremework）

JDBC（Java Database Connectivity） API就是服务提供这框架，指一个这样的系统：多个服务提供者实现一个服务，系统为服务提供者的客户端提供多个实现，并把他们从多个实现中解耦出来

服务提供者框架中有三个重要的组件，第四个组件可选

1. 服务提供者接口（service provider interface） 提供者实现的
2. 提供者注册API（provider registration API）系统用来注册实现让客户端访问他们的
3. 服务访问API（service access api）是客户端用来获取服务的实例的
4. 服务提供者接口（servie provider interface）这些公共者负责创建其服务实现的实例



重叠构造器模式， 参数多了，代码量就多了

Builder模式比重叠构造器还要冗长



终结方法守卫者（finalizer guardian）

### 2. 当构造方法参数过多时使用 builder 模式 ###

``` java
// Builder Pattern
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        // Required parameters
        private final int servingSize;
        private final int servings;

        // Optional parameters - initialized to default values
        private int calories      = 0;
        private int fat           = 0;
        private int sodium        = 0;
        private int carbohydrate  = 0;

        public Builder(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings    = servings;
        }

        public Builder calories(int val) { 
            calories = val;      
            return this;
        }

        public Builder fat(int val) { 
           fat = val;           
           return this;
        }

        public Builder sodium(int val) { 
           sodium = val;        
           return this; 
        }

        public Builder carbohydrate(int val) { 
           carbohydrate = val;  
           return this; 
        }

        public NutritionFacts build() {
            return new NutritionFacts(this);
        }
    }

    private NutritionFacts(Builder builder) {
        servingSize  = builder.servingSize;
        servings     = builder.servings;
        calories     = builder.calories;
        fat          = builder.fat;
        sodium       = builder.sodium;
        carbohydrate = builder.carbohydrate;
    }
}

```

``` java
NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8)
    .calories(100).sodium(35).carbohydrate(27).build();

```

## chapter03

### [9.使用 try-with-resources 语句替代 try-finally 语句](http://sjsdfg.gitee.io/effective-java-3rd-chinese/#/notes/09. 使用try-with-resources语句替代try-finally语句?id=_9-使用-try-with-resources-语句替代-try-finally-语句)

1、多个try-finally一起使用显的太冗长

2、存在异常风险

```java
// try-finally is ugly when used with more than one resource!
static void copy(String src, String dst) throws IOException {
    InputStream in = new FileInputStream(src);
    try {
        OutputStream out = new FileOutputStream(dst);
        try {
            byte[] buf = new byte[BUFFER_SIZE];
            int n;
            while ((n = in.read(buf)) >= 0)
                out.write(buf, 0, n);
        } finally {
            out.close();
        }
    } finally {
        in.close();
    }
}
```





使用try-with-resource需要资源必须实现AutoCloseable接口

```java
// try-with-resources - the the best way to close resources!
static String firstLineOfFile(String path) throws IOException {
    try (BufferedReader br = new BufferedReader(
           new FileReader(path))) {
       return br.readLine();
    }
}

// try-with-resources on multiple resources - short and sweet
static void copy(String src, String dst) throws IOException {
    try (InputStream   in = new FileInputStream(src);
         OutputStream out = new FileOutputStream(dst)) {
        byte[] buf = new byte[BUFFER_SIZE];
        int n;
        while ((n = in.read(buf)) >= 0)
            out.write(buf, 0, n);
    }
}
```

### [10. 重写 equals 方法时遵守通用约定](http://sjsdfg.gitee.io/effective-java-3rd-chinese/#/notes/10. 重写equals方法时遵守通用约定?id=_10-重写-equals-方法时遵守通用约定)

如果满足以下任一下条件，则说明是正确的做法：

- 每个类的实例都是固有唯一的。 对于像 Thread 这样代表活动实体而不是值的类来说，这是正确的。 Object 提供的 equals 实现对这些类完全是正确的行为。
- 类不需要提供一个「逻辑相等（logical equality）」的测试功能。例如 `java.util.regex.Pattern` 可以重写 equals 方法检查两个是否代表完全相同的正则表达式 Pattern 实例，但是设计者并不认为客户需要或希望使用此功能。在这种情况下，从 Object 继承的 equals 实现是最合适的。
- 父类已经重写了 equals 方法，则父类行为完全适合于该子类。例如，大多数 Set 从 AbstractSet 继承了 equals 实现、List 从 AbstractList 继承了 equals 实现，Map 从 AbstractMap 的 Map 继承了 equals 实现。
- 类是私有的或包级私有的，可以确定它的 equals 方法永远不会被调用。如果你非常厌恶风险，可以重写 equals 方法，以确保不会被意外调用：

```java
@Override 
public boolean equals(Object o) {
    throw new AssertionError(); // Method is never called
}
```



重写equals ，需要判断逻辑相等的情况（logical equality），有别于对象标识（object identity）

当你重写 equals 方法时，必须遵守它的通用约定。Object 的规范如下： equals 方法实现了一个等价关系（equivalence relation）。它有以下这些属性:

- **自反性：** 对于任何非空引用 x，`x.equals(x)` 必须返回 true。
- **对称性：** 对于任何非空引用 x 和 y，如果且仅当 `y.equals(x)` 返回 true 时 `x.equals(y)` 必须返回 true。
- **传递性：** 对于任何非空引用 x、y、z，如果 `x.equals(y)` 返回 true，`y.equals(z)` 返回 true，则 `x.equals(z)` 必须返回 true。
- **一致性：** 对于任何非空引用 x 和 y，如果在 equals 比较中使用的信息没有修改，则 `x.equals(y)` 的多次调用必须始终返回 true 或始终返回 false。
- 对于任何非空引用 x，`x.equals(null)` 必须返回 false。