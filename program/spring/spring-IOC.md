[toc]





# IOC

Spring容器来实现对象的创建、协调工作

![启动流程](/home/klaus/documents/pic/note/20190310122523469.png)

![在这里插入图片描述](/home/klaus/documents/pic/note/20190310121611901.png)



简单分类如下：

- 工厂后置处理器（BeanFactoryPostProcessor）：这个包括了AspectJWeavingEnabler, ConfigurationClassPostProcessor, CustomAutowireConfigurer等等非常有用的工厂后处理器接口的方法。工厂后处理器也是容器级的。
- 容器级别生命周期处理器：包括了InstantiationAwareBeanPostProcessor 和 BeanPostProcessor 这两个接口实现，一般称它们的实现类为“后处理器”
- Bean级生命周期接口方法（仅作用于某个Bean）：这个包括了BeanNameAware、BeanFactoryAware、InitializingBean和DiposableBean这些接口的方法
- Bean自身的方法：这个包括了Bean本身调用的方法和通过配置文件中<bean>的init-method和destroy-method指定的方法





**在`spring ioc`的过程中，优先解析`@Component，@Service，@Controller`注解的类。其次解析配置类，也就是`@Configuration`标注的类。最后开始解析配置类中定义的`bean`。** 