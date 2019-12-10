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

