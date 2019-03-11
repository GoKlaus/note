# maven

[TOC]

## 1.概述

​	maven是一个项目管理和整合工具，maven为开发者提供了一套完整的构建生命周期的框架

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

> pom代表工程对象模型。
>==用这个文件抽象整个工程的构建过程，工程的依赖，并且对pom的修改会直接作用在整个工程上==

> pom中可以配置



| 配置项               | 作用 |
| -------------------- | ---- |
| project dependencies |      |
| plugins              |      |
| goals                |      |
| build profiles       |      |
| project version      |      |
| developers           |      |
| mailing list         |      |



