# dubbo的本地调试模式

开发中多人并行开发项目，存在公用一个注册中心，调试不一定是自己开发依赖的模块，用本地调试模式可以避免这种情况的发生：

三种方法可以选择：

1. 停止同一个服务版本的其他提供者，启动本地的服务提供者(多人开发的时候不适用)

2. 在消费者的.xml里对应服务的<dubbo:reference>里面加入属性url="dubbo://localhost:19604"，然后启动本地提供者，就可以实现dubbo直连，调试本地程序(有点麻烦)

3. 在当前登录用户下面加入dubbo-resolve.properties文件，内容指定要调试的服务，格式如下：com.emar.adx.yiqifa.adcenter.bl.service.CompleteProductService=dubbo\://localhost\:19604       之后启动相应的服务。

   >
   >
   >使用方式在JVM启动参数中加入-D参数映射服务地址，如：
   >
   >单个：
   >
   >(key为服务名，value为服务提供者url，此配置优先级最高，1.0.15及以上版本支持)
   >
   >> java -Dcom.alibaba.xxx.XxxService=dubbo://localhost:20890
   >
   >多个服务可以使用文件映射：
   >
   >(用-Ddubbo.resolve.file指定映射文件路径，此配置优先级高于<dubbo:reference>中的配置，1.0.15及以上版本支持)
   >(2.0以上版本自动加载${user.home}/dubbo-resolve.properties文件，不需要配置)
   >
   >> java -Ddubbo.resolve.file=xxx.properties
   >>
   >> 这种写法是默认加载${user.home}下的文件，对于win系统来说${user.home}指的是当前操作系统用户目录，如 Win7系统 Administrator的用户目录就是 C:\Users\Administrator
   >>



# dubbo-admin

## 搭建dubbo-admin的注意事项

### 1、dubbo-admin

使用github上的dubbo-admin项目来搭建

编译缓慢，而且需要nodejs来编译，且报错，后续没有继续采用这个方法

### 2、dubbo

直接将2.5.x版本的dubbo源码下载下来，然后编译了dubbo-admin部分，成功搭建了dubbo-admin