# JS数据类型 #

## 概述 ##

JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有六种。（ES6 又新增了第七种 Symbol 类型的值）

- 数值（number）：整数和小数（比如1和3.14）
- 字符串（string）：字符组成的文本（比如"Hello World"）
- 布尔值（boolean）：true（真）和false（假）两个特定值
- undefined：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
- null：表示无值，即此处的值就是“无”的状态。
- 对象（object）：各种值组成的集合
- Symbol 类型的值

通常，我们将数值、字符串、布尔值称为原始类型（primitive type）的值，即它们是最基本的数据类型，不能再细分了。而将对象称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。至于undefined和null，一般将它们看成两个特殊值。

对象又可以分成三个子类型。

	1.狭义的对象（object）
	2.数组（array）
	3.函数（function）

## typeof运算符 ##

JavaScript有三种方法，可以确定一个值到底是什么类型。

	typeof运算符
	
	instanceof运算符
	
	Object.prototype.toString方法
	
instanceof运算符和Object.prototype.toString方法，将在后文相关章节介绍。这里着重介绍typeof运算符。

typeof运算符可以返回一个值的数据类型，可能有以下结果：

**（1）原始类型**

数值、字符串、布尔值分别返回number、string、boolean。

	typeof 123 // "number"
	typeof '123' // "string"
	typeof false // "boolean"

**（2）函数**

函数返回function。

	function f() {}
	typeof f
	// "function"

**（3）undefined**

undefined返回undefined。

	typeof undefined
	// "undefined"
	利用这一点，typeof可以用来检查一个没有声明的变量，而不报错。
	
	v
	// ReferenceError: v is not defined
	
	typeof v
	// "undefined"

上面代码中，变量v没有用var命令声明，直接使用就会报错。但是，放在typeof后面，就不报错了，而是返回undefined。

实际编程中，这个特点通常用在判断语句。

	// 错误的写法
	if (v) {
	  // ...
	}
	// ReferenceError: v is not defined
	
	// 正确的写法
	if (typeof v === "undefined") {
	  // ...
	}

**（4）其他**

除此以外，其他情况都返回object。

	typeof window // "object"
	typeof {} // "object"
	typeof [] // "object"
	typeof null // "object"

从上面代码可以看到，空数组（[]）的类型也是object，这表示在JavaScript内部，数组本质上只是一种特殊的对象。

既然typeof对数组（array）和对象（object）的显示结果都是object，那么怎么区分它们呢？instanceof运算符可以做到。

	var o = {};
	var a = [];
	
	o instanceof Array // false
	a instanceof Array // true

instanceof 后续讲解。

## 布尔值 ##

布尔值代表“真”和“假”两个状态。“真”用关键字true表示，“假”用关键字false表示。布尔值只有这两个值。

下列运算符会返回布尔值：

	两元逻辑运算符： && (And)，|| (Or)
	前置逻辑运算符： ! (Not)
	相等运算符：===，!==，==，!=
	比较运算符：>，>=，<，<=

如果JavaScript预期某个位置应该是布尔值，会将该位置上现有的值自动转为布尔值。转换规则是除了下面六个值被转为false，其他值都视为true。

	undefined
	null
	false
	0
	NaN
	""或''（空字符串）

布尔值往往用于程序流程的控制，请看一个例子。

	if ('') {
	  console.log(true);
	}
	// 没有任何输出

上面代码的if命令后面的判断条件，预期应该是一个布尔值，所以JavaScript自动将空字符串，转为布尔值false，导致程序不会进入代码块，所以没有任何输出。

需要特别注意的是，空数组（[]）和空对象（{}）对应的布尔值，都是true。

	if ([]) {
	  console.log(true);
	}
	// true
	
	if ({}) {
	  console.log(true);
	}
	// true

更多关于数据类型转换的介绍，参见《数据类型转换》一节。（下面参考链接）

## 参考链接 ##

[阮一峰JS教程](http://javascript.ruanyifeng.com/grammar/types.html#toc6)

[JavaScript 数据类型和数据结构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures)

[Symbol函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

[JS语法和数据类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types)
