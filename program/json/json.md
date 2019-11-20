# JSON

`json:(JavaScript Object Notation)`JavaScript对象表示法

JSON是存储和交换文本信息的语法

JSON比xml更小、更快、更易解析

````json
json指的是JavaScript对象表示法(JavaScript Object Notation)
json是轻量级的文本数据交换格式
json独立于语言
json具有私我描述性，更易理解
json使用JavaScript语法来描述数据对象，但是json任然独立于语言和平台。JSON 解析器和 JSON 库支持许多不同的编程语言。
````

JSON-转换为JavaScript对象

JSON文本格式在语法上与创建JavaScript对象的代码相同。

由于这种相似性，无需解析器，JavaScript程序能够使用内建的`eval()`函数，用 JSON 数据来生成原生的 JavaScript 对象。

# XML相比

类似点

* JSON是纯文本
* JSON具有“自我描述性“
* JSON具有层级结构（值中存在值）
* JSON可通过JavaScript进行解析
* JSON数据可以通过AJAX传输

不同点

* 没有结束标签
* 更短
* 读写速度更快
* 能够使用内建的JavaScript eval()方法进行解析
* 使用数组
* 不使用保留字

## 为什么使用JSON

对于AJAX应用程序来说，JSON比XML更快更易使用：

### 使用XML

* 读取XML文档
* 使用XML DOM 来循环遍历文档
* 读取值并存储在变量中

### 使用JSON

* 读取JSON字符串
* 用eval()处理JSON字符串

# JSON语法规则

**JSON语法是JavaScript语法的子集**

* 数据在名称/值对中
* 数据由逗号分隔
* 花括号保存对象
* 方括号保存数组

JSON的值可以是：

* 数字(整数或浮点数)
* 字符串(在双引号中)
* 逻辑值(true  false)
* 数组(在方括号中)
* 对象(在或括号中)
* null

JSON 使用 JavaScript 语法

因为 JSON 使用 JavaScript 语法，所以无需额外的软件就能处理 JavaScript 中的 JSON。

通过 JavaScript，您可以创建一个对象数组，并像这样进行赋值：

例子

```javascript
var employees = [
{ "firstName":"Bill" , "lastName":"Gates" },
{ "firstName":"George" , "lastName":"Bush" },
{ "firstName":"Thomas" , "lastName": "Carter" }
];
```

可以像这样访问 JavaScript 对象数组中的第一项：

```javascript
employees[0].lastName;
```

返回的内容是：

```javascript
Gates
```

可以像这样修改数据：

```javascript
employees[0].lastName = "Jobs";
```

