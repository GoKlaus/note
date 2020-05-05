[TOC]





# @Transactional

注解式声明事务



## Propagation

7种支持配置对应不同级别，影响数据存储



|                           | 作用                                                         | 其他 |
| ------------------------- | ------------------------------------------------------------ | ---- |
| Propagation.REQUIRED      | 支持当前事务，如果当前没有事务，就新建一个事务。这是最常见的选择 |      |
| Propagation.SUPPORTS      | 支持当前事务，如果当前没有事务，就以非事务方式执行           |      |
| Propagation.MANDATORY     | 支持当前事务，如果当前没有事务，就抛出异常。                 |      |
| Propagation.REQUEIRES_NEW | 新建事务，如果当前存在事务，把当前事务挂起。                 |      |
| Propagation.NOT_SUPPORTED | 以非事务方式执行操作，如果当前存在事务，就把当前事务挂起     |      |
| Propagation.NEVER         | 以非事务方式执行，如果当前存在事务，则抛出异常。             |      |
| Propagation.NESTED        | 支持当前事务，如果当前事务存在，则执行一个嵌套事务，如果当前没有事务，就新建一个事务。 |      |
|                           |                                                              |      |

