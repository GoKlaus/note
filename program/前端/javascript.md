Undefined Null Boolean Number String 五中基本类型

typeof  和  instanceof 区别







作用域链



JavaScript具有自动垃圾收集机制，执行环境会负责管理代码执行中使用的内存

最常用的是标记清楚（mark-and-sweep）

不太常用的收集策略引用计数（reference counting）



IE中一部分对象不是JavaScript原生对象。例如BOM和DOM中对象就是使用C++以COM（Components Object Model，组件对象模型）对象的形式实现的



解除引用的真正作用是让值脱离执行环境，以便垃圾收集器下次运行时将其回收





在ECMAScript中，引用类型是一种数据结构，用于将数据和功能组织在一起。它也常被称为类





数组

数组每一项可以保存任何类型的数据

数组大小可以动态调整的