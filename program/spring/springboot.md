# 启动过程
启动过程，类加载器使用：
```java
ClassUtils.getDefaultClassLoader();
```







# springboot 打包成可执行jar需要

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

`spring-boot-starter-parent`里已经有了默认约定，绑定了repackage的goal了



在使用slf4j日志框架的时候，注意查看spring默认的实现框架，slf4j是一组定义接口，规范



spring boot 启动的真正入口类，类里也有默认的main方法，在不写入任何新的代码情况下，按照springboot的默认设置启动

```java
spring-boot-x.x.x-RELEASE.jar
org.springframework.boot.SpringApplication
```



# swagger 整合 spring boot  使用ui jar包有两个

springfox-swagger-ui

springfox-swagger-ui-rfc6570

两个是使用不太一样 rfc 的这个版本需要配合oauth2 使用



配置的时候容易出现

```shell
No mapping found for HTTP request with URI [/dm/swagger-ui.html] in DispatcherServlet
```

原因是swagger-ui.html在 jar包中，Spring Boot自动配置本身不会自动把/swagger-ui.html这个路径映射到对应的目录META-INF/resources/下面，在启动类上添加注解@EnableWebMvc

# @EnableWebMvc ....三个的区别





```java
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("swagger-ui.html")
                .addResourceLocations("classpath:/META-INF/resources/");
        registry.addResourceHandler("/webjars/**")
                .addResourceLocations("classpath:/META-INF/resources/webjars/");

    }
```





使用profile指定不同的配置文件

在classpath下

application-{profile}.yml

application-{profile}.properties

可以通过--spring.profiles.active=xxx来指定

java -jar --spring.profile.active=xxx    xxx.jar

java -jar -Dspring.profile.active=xxx xxx.jar

# Singleton和prototype区别

singleton：Spring Ioc容器中只会有一个bean实例

prototype：每次对该Bean请求（将其注入到另一个Bean中，或者以程序的方式调用容器的getBean()方法）时都会创建一个新的Bean实例。根据经验，对有状态的Bean应使用prototype作用域，而对无状态的Bean则应该使用singleton作用域。
对于具有prototype作用域的Bean，有一点很重要，即Spring不能对该Bean的整个生命周期负责。具有prototype作用域的Bean创建后交由调用者负责销毁对象回收资源。
简单的说：
singleton 只有一个实例，也即是单例模式。
prototype访问一次创建一个实例，相当于new。

# 启动过程

[SpringBoot启动结构图](https://www.processon.com/view/link/59812124e4b0de2518b32b6e)



SpringBoot启动通过配置文件`classpath:META-INF/spring.factories`  key value 为全限定路径的类名，反射实例化对象，监听器监听相关时间启动



```json
{"orgId":1,"roleId":1,"username":"demoData","password":"demoData","email":"demoData","mobile":"demoData"}
```











```
A web application can define any number of DispatcherServlets.</b>
* Each servlet will operate in its own namespace, loading its own application context
* with mappings, handlers, etc. Only the root application context as loaded by
* {@link org.springframework.web.context.ContextLoaderListener}, if any, will be shared.
*
* <p>As of Spring 3.1, {@code DispatcherServlet} may now be injected with a web
* application context, rather than creating its own internally. This is useful in Servlet
* 3.0+ environments, which support programmatic registration of servlet instances.
* See the {@link #DispatcherServlet(WebApplicationContext)} javadoc for details.
```

DispatcherServlet的注释





# 实际遇到问题

## zuul网关转发请求头

```java
package com.chinamobile.iot.client;

import com.chinamobile.iot.east.common.util.constants.ErrorEnum;
import com.chinamobile.iot.east.common.web.CommonUtil;
import com.chinamobile.iot.east.common.web.response.CommonResponse;
import feign.RequestInterceptor;
import feign.RequestTemplate;
import feign.hystrix.FallbackFactory;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.cloud.netflix.feign.FeignClient;
import org.springframework.stereotype.Component;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.context.request.RequestContextHolder;
import org.springframework.web.context.request.ServletRequestAttributes;

import javax.servlet.http.HttpServletRequest;
import java.util.Enumeration;

/**
 * description:
 *
 * @author klaus
 * @date 2020/4/26
 */
//smartCommunity-user 从eureka中找这个名字的项目
@FeignClient(value = "smartCommunity-user", configuration = AuthorizorClientFallBack.class)
public interface AuthorizorClient {

    @PostMapping("/sys/user/new/tokenAuth")
    CommonResponse authorizeByToken(@RequestParam("path") String path);

}

@Component
class AuthorizorClientFallBack implements FallbackFactory<AuthorizorClient>, RequestInterceptor {
//实现RequestInterceptor 来转发header
    private static final Logger LOGGER = LoggerFactory.getLogger(AuthorizorClientFallBack.class);

    @Override
    public AuthorizorClient create(Throwable throwable) {
        return new AuthorizorClient() {
            @Override
            public CommonResponse authorizeByToken(String path) {
                LOGGER.info("token auth failed, cause by {} ", throwable.getMessage());
                // TODO: 2020/4/26  增加对返回值类型来决定后续返回
                return (CommonResponse) CommonUtil.errorJson(ErrorEnum.E_50502);
            }
        };
    }

    //转发请求中带有的header
    @Override
    public void apply(RequestTemplate template) {
        ServletRequestAttributes attributes = (ServletRequestAttributes) RequestContextHolder
                .getRequestAttributes();
        HttpServletRequest request = attributes.getRequest();
        Enumeration<String> headerNames = request.getHeaderNames();
        if (headerNames != null) {
            while (headerNames.hasMoreElements()) {
                String name = headerNames.nextElement();
                String values = request.getHeader(name);
                template.header(name, values);
            }
            LOGGER.debug("feign interceptor header:{}", template.toString());
        }
    }
}
```



spi思想





@Conditional

生效原理



```java
@Order(Ordered.HIGHEST_PRECEDENCE + 40)
class OnPropertyCondition extends SpringBootCondition {
    
}
```



@ConditionalOnProperty



## Long值传递到web端精度丢失问题



JacksonConverter 不配置dateformat，仍然可以时间格式转换

```java
package com.chinamobile.iot.config;

import com.chinamobile.iot.security.EncryptionPropertyResolver;
import com.fasterxml.jackson.databind.DeserializationFeature;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import com.fasterxml.jackson.databind.module.SimpleModule;
import com.fasterxml.jackson.databind.ser.std.ToStringSerializer;
import com.ulisesbocchio.jasyptspringboot.EncryptablePropertyResolver;
import org.springframework.boot.autoconfigure.web.HttpMessageConverters;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.converter.HttpMessageConverter;
import org.springframework.http.converter.json.MappingJackson2HttpMessageConverter;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurerAdapter;

import java.text.SimpleDateFormat;
import java.util.List;

/**
 * description:
 *
 * @author klaus
 * @date 2020/4/21
 */
@Configuration
public class CommonConfiguration extends WebMvcConfigurerAdapter {
    @Bean(name = "encryptablePropertyResolver")
    public EncryptablePropertyResolver encryptablePropertyResolver() {
        return new EncryptionPropertyResolver();
    }

    /**
     * {@inheritDoc}
     * <p>This implementation is empty.
     *
     * @param converters
     */
    @Override
    public void configureMessageConverters(List<HttpMessageConverter<?>> converters) {
        super.configureMessageConverters(converters);
        converters.add(jackson2HttpMessageConverter());
    }

    @Bean
    public MappingJackson2HttpMessageConverter jackson2HttpMessageConverter() {
        MappingJackson2HttpMessageConverter converter = new MappingJackson2HttpMessageConverter();
        ObjectMapper mapper = new ObjectMapper();
//        mapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
        mapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS, true);
//        mapper.setDateFormat(new SimpleDateFormat("yyyy-MM-dd HH:mm:ss"));

        //Long类型转String类型
        SimpleModule simpleModule = new SimpleModule();
        simpleModule.addSerializer(Long.class, ToStringSerializer.instance);
        simpleModule.addSerializer(Long.TYPE, ToStringSerializer.instance);
        simpleModule.addSerializer(long.class, ToStringSerializer.instance);
        mapper.registerModule(simpleModule);
        converter.setObjectMapper(mapper);
        return converter;
    }
}

```

刚开始不生效，时间戳被格式化为yyyy-MM-dd,后来生效了，直接返回时间戳

