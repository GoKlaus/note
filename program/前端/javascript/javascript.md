ECMA Script

定义javascript的标准不同厂商，对这个进行实现，也有各自的特点实现部分

DOM 也成为了HTML的标准



JavaScript数据类型

JavaScript拥有动态类型。这意味着相同的变量可用作不同的类型



**值类型(基本类型)**：字符串（String）、数字(Number)、布尔(Boolean)、对空（Null）、未定义（Undefined）、Symbol。

**引用数据类型**：对象(Object)、数组(Array)、函数(Function)。



变量生命周期

全局变量的作用域是全局性，函数内部声明的变量，只在函数内部起作用。这些变量是局部变量，作用域是局部性的；函数的参数也是局部性的，只在函数内部起作用



闭包是一种保护私有变量的机制，在函数执行时形成私有的作用域，保护里面的私有变量不受外界干扰。直观的说就是形成一个不销毁的栈环境



JavaScript 中的异步操作函数往往通过回调函数来实现异步任务





js dom html css 

web 页面的元素，各自有各自的体系，语法，及结构





Undefined Null Boolean Number String 五种基本类型

typeof  和  instanceof 区别



Vue 内置了完整的时间触发器，不需要再引入别的时间触发器了。



单向下行绑定， 防止子组件在无意中改变父级组件的状态

可以使用.sync修饰符来实现双向绑定



冒泡







作用域链



JavaScript具有自动垃圾收集机制，执行环境会负责管理代码执行中使用的内存

最常用的是标记清除（mark-and-sweep）

不太常用的收集策略引用计数（reference counting）



IE中一部分对象不是JavaScript原生对象。例如BOM和DOM中对象就是使用C++以COM（Components Object Model，组件对象模型）对象的形式实现的



解除引用的真正作用是让值脱离执行环境，以便垃圾收集器下次运行时将其回收





在ECMAScript中，引用类型是一种数据结构，用于将数据和功能组织在一起。它也常被称为类



12种节点类型

❏ Node.ELEMENT_NODE(1)；

❏ Node.ATTRIBUTE_NODE(2)；

❏ Node.TEXT_NODE(3)；

❏ Node.CDATA_SECTION_NODE(4)；

❏ Node.ENTITY_REFERENCE_NODE(5)；

❏ Node.ENTITY_NODE(6)；

❏ Node.PROCESSING_INSTRUCTION_NODE(7)；

❏ Node.COMMENT_NODE(8)；

❏ Node.DOCUMENT_NODE(9)；

❏ Node.DOCUMENT_TYPE_NODE(10)；

❏ Node.DOCUMENT_FRAGMENT_NODE(11)；❏ Node.NOTATION_NODE(12)



数组

数组每一项可以保存任何类型的数据

数组大小可以动态调整的