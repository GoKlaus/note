# maven

[TOC]

**参考：**[maven教程](http://wiki.jikexueyuan.com/project/maven/pom.html)



## 1.概述

​	maven是一个项目管理和整合工具，maven为开发者提供了一套完整的==构建生命周期==的框架

### maven可以完成以下工作：

* 构建
* 文档生成
* 报告
* 依赖
* SCMs
* 发布
* 分发
* 邮件列表



### maven的目标

maven的主要目的是为开发者提供：

* 一个可复用、可维护、更易理解的工程综合模型
* 与这个模型交互的插件或者工具

### 约定优于配置

约定：maven有默认的构建过程，不需要自己去创建过程，除非对构建过程做处理

> `所以开发者不用在关注所有的细节`

### 默认配置

| 配置项             | 默认值                        | 说明 |
| ------------------ | ----------------------------- | ---- |
| source code        | ${basedir}/src/main/java      |      |
| resources          | ${basedir}/src/main/resources |      |
| Tests              | ${basedir}/src/test           |      |
| Compiled byte Code | ${basedir}/target             |      |
| distributable JAR  | ${basedir}/target/classes     |      |
|                    |                               |      |



## 2.POM

pom代表工程对象模型。
==用这个文件抽象整个工程的构建过程，工程的依赖，并且对pom的修改会直接作用在整个工程上==

**pom中可以配置**

| 配置项               | 作用       |
| -------------------- | ---------- |
| project dependencies | 配置依赖   |
| plugins              | 插件的配置 |
| goals                |            |
| build profiles       |            |
| project version      |            |
| developers           |            |
| mailing list         |            |

> 所有的pom都是继承于同一个父pom(无论是否显式定义了这个父pom),这个pom也被称为super pom,可以通过命令行:==mvn help:effective-pom==来查看super pom的默认配置

### 构建生命周期

概念：==构建生命周期是一组阶段的序列(suquence of phase)，每个阶段定义了目标被执行的顺序，阶段是生命周期的一部分==

### maven生命周期的一些概念之间的关系

> 生命周期
>
> > 阶段:
> >
> > > 目标:  表示一个特定的、对构建和管理工程有帮助的任务

生命周期由==阶段组成==，

而阶段里包含==目标==

相同的目标可以==绑定在多个构建阶段==

目标绑定阶段的

```xml
<build>
	<plugins>
        <plugin>
            <!--引入插件，插件里有多个目标任务-->
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-antrun-plugin</artifactId>
   			<version>1.1</version>
   			<executions>
                <execution>
                    <id>id.pre-clean</id>
                    <!--定义绑定的阶段-->
                    <!--使用pre定义在某个阶段之前-->
                    <phase>pre-clean</phase>
                    <goals>
                        <!--配置的是该插件的run目标-->
                        <goal>run</goal>
                    </goals>
                	<configuration>
                    <tasks>
                        <echo>pre-clean phase</echo>
                    </tasks>
                	</configuration>
                </execution>
                <execution>
                     <id>id.clean</id>
                     <phase>clean</phase>
                     <goals>
                  		<goal>run</goal>
                	 </goals>
                 	<configuration>
                        <tasks>
                           <echo>clean phase</echo>
                        </tasks>
                 	</configuration>
                </execution>
    			<execution>
             		<id>id.post-clean</id>
                    <!--post定义在阶段之后-->
             		<phase>post-clean</phase>
           			<goals>
              			<goal>run</goal>
           			</goals>
              		<configuration>
                        <tasks>
                           <echo>post-clean phase</echo>
                        </tasks>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```



例如，一个典型的maven构建生命周期：

| 阶段              | 处理     | 描述                                |
| ----------------- | -------- | ----------------------------------- |
| prepare-resources | 资源拷贝 | 本阶段可以自定义需要拷贝的资源      |
| compile           | 编译     | 本阶段完成源代码编译                |
| package           | 打包     | 根据pom的定义，打包成jar，或者war等 |
| install           | 安装     | 在本地/远程仓库中安装工程包         |

`需要在某个特定的阶段之前或之后执行目标，可以使用pre和post来定义目标`

#### 三个周期

maven中含有三个标准的生命周期：

* clean
* default(or build)
* site

##### clean周期

* pre-clean
* clean
* post-clean



##### Default(or build)生命周期

| 生命周期阶段          | 描述                                                         |
| --------------------- | ------------------------------------------------------------ |
| validate              | 检查工程配置是否正确，完成构建过程的所有必要信息是否能够获取到。 |
| initialize            | 初始化构建状态，例如设置属性。                               |
| generate-sources      | 生成编译阶段需要包含的任何源码文件。                         |
| process-sources       | 处理源代码，例如，过滤任何值（filter any value）。           |
| generate-resources    | 生成工程包中需要包含的资源文件。                             |
| process-resources     | 拷贝和处理资源文件到目的目录中，为打包阶段做准备。           |
| compile               | 编译工程源码。                                               |
| process-classes       | 处理编译生成的文件，例如 Java Class 字节码的加强和优化。     |
| generate-test-sources | 生成编译阶段需要包含的任何测试源代码。                       |
| process-test-sources  | 处理测试源代码，例如，过滤任何值（filter any values)。       |
| test-compile          | 编译测试源代码到测试目的目录。                               |
| process-test-classes  | 处理测试代码文件编译后生成的文件。                           |
| test                  | 使用适当的单元测试框架（例如JUnit）运行测试。                |
| prepare-package       | 在真正打包之前，为准备打包执行任何必要的操作。               |
| package               | 获取编译后的代码，并按照可发布的格式进行打包，例如 JAR、WAR 或者 EAR 文件。 |
| pre-integration-test  | 在集成测试执行之前，执行所需的操作。例如，设置所需的环境变量。 |
| integration-test      | 处理和部署必须的工程包到集成测试能够运行的环境中。           |
| post-integration-test | 在集成测试被执行后执行必要的操作。例如，清理环境。           |
| verify                | 运行检查操作来验证工程包是有效的，并满足质量要求。           |
| install               | 安装工程包到本地仓库中，该仓库可以作为本地其他工程的依赖。   |
| deploy                | 拷贝最终的工程包到远程仓库中，以共享给其他开发人员和工程。   |

当一个阶段(phase)通过maven命令调用时,例如maven compile ,只有该阶段之前以及包括该阶段在内的所有阶段都会执行,==不同的maven目标将根据打包的类型(jar  war   ear),被绑定到不同的maven生命周期阶段==    ????这句话不太理解

##### site生命周期

site插件一般用来创建新的==报告文档，部署站点等==

* pre-site
* site
* post-site
* site-deploy



## 3.构建配置文件

概念：就是一组配置的集合，用来设置或者覆盖maven构建的默认配置

### profile类型

Profile 主要有三种类型：

| 类型        | 在哪里定义                                                   |
| ----------- | ------------------------------------------------------------ |
| Per Project | 定义在工程 POM 文件 pom.xml 中                               |
| Per User    | 定义在 Maven 设置 xml 文件中 （%USER_HOME%/.m2/settings.xml） |
| Global      | 定义在 Maven 全局配置 xml 文件中 （%M2_HOME%/conf/settings.xml） |

#### profile的激活方式：

##### 显示使用命令控制台输入

##### 通过maven设置

##### 基于环境变量(用户/变量 )

##### 操作系统配置

##### 现存/缺失 文件

## 4.仓库repository

### repository的分类

#### 本地(local)

在settings.xml中配置`<localRepository>`

#### 中央(central)

中央仓库的关键概念：

- 这个仓库由 Maven 社区管理。
- 不需要配置。
- 需要通过网络才能访问。

要浏览中央仓库的内容，maven 社区提供了一个 URL：**http://search.maven.org/#browse**。使用这个仓库，开发人员可以搜索所有可以获取的代码库。

#### 远程(remote)

### maven依赖的搜索顺序

当我们执行 Maven 构建命令时，Maven 开始按照以下顺序查找依赖的库：

- **步骤 1** － 在本地仓库中搜索，如果找不到，执行步骤 2，如果找到了则执行其他操作。
- **步骤 2** － 在中央仓库中搜索，如果找不到，并且有一个或多个远程仓库已经设置，则执行步骤 4，如果找到了则下载到本地仓库中已被将来引用。
- **步骤 3** － 如果远程仓库没有被设置，Maven 将简单的停滞处理并抛出错误（无法找到依赖的文件）。
- **步骤 4** － 在一个或多个远程仓库中搜索依赖的文件，如果找到则下载到本地仓库已被将来引用，否则 Maven 将停止处理并抛出错误（无法找到依赖的文件）。

## 5.插件

### 什么是插件

maven实际上是一个==依赖插件执行==的框架，每个任务实际上都是==由插件完成的==。maven插件通常用来：

* 创建jar文件
* 创建war文件
* 编译代码文件
* 代码单元测试
* 创建工程文档
* 创建工程报告

插件通常是提供了一个==目标的集合==，可以使用一下的命令语法执行：

```shell
mvn [plugin-name]:[goal-name]
```

### 插件的类型

| 类型              | 描述                                               |
| ----------------- | -------------------------------------------------- |
| Build plugins     | 在构建时执行，并在 pom.xml 的 元素中配置。         |
| Reporting plugins | 在网站生成过程中执行，并在 pom.xml 的 元素中配置。 |

### 常用插件

| 插件     | 描述                                                |
| -------- | --------------------------------------------------- |
| clean    | 构建之后清理目标文件。删除目标目录。                |
| compiler | 编译 Java 源文件。                                  |
| surefile | 运行 JUnit 单元测试。创建测试报告。                 |
| jar      | 从当前工程中构建 JAR 文件。                         |
| war      | 从当前工程中构建 WAR 文件。                         |
| javadoc  | 为工程生成 Javadoc。                                |
| antrun   | 从构建过程的任意一个阶段中运行一个 ant 任务的集合。 |

