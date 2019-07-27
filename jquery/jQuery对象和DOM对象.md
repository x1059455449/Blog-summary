## 概念 ##

**jQuery对象：**

它是一个全局对象，可以简写为美元符号$。在网页中加载jQuery函数库以后，就可以使用jQuery对象了。**jQuery对象本质上是一个构造函数，主要作用是返回jQuery对象的实例**

var $div = $('div');//此时的$div就是jQuery对象

**DOM对象**

用原生的javaScript方法（如getElementById等）获得的对象。

	var NewDiv = document.getElementsByTagName('div')
	//此时的NewDiv就是DOM对象

## 两者的区别 ##

- jQuery对象是一个类数组的对象，对象原型中封装了许多jQuery自定义的方法。
- 在jQuery对象中无法使用DOM对象的任何方法。

类数组：

顾名思义，是一个类似数组的东西，但是不含有数组的方法，但是可以使用下标[index]和length。

## 两者的内在联系和相互转换 ##

> DOM对象转换成jQuery对象

**方法：$(DOM对象)**

	//DOM对象
	var NewDiv = document.getElementsByTagName('div')
	//jQuery对象
	var $div = $(NewDiv)

**jQuery对象转换成DOM对象**

> jQuery对象是一个数据对象：使用[index]

	var $div = $('#header')//jQuery对象
	var NewDiv = $div[2]//DOM对象

> jQuery本身提供:使用.get(index)

var $div = $('#header')//jQuery对象
var NewDiv = $div.get(0)//DOM对象

## DOM对象方法 ##

![](https://i.imgur.com/kRTsmsd.png)

## jQuery实例对象的方法(具体请参考阮一峰jQuery教程) ##

**结果集的过滤方法**

	first方法，last方法
	next方法，prev方法
	parent方法，parents方法，children方法
	siblings方法，nextAll方法，prevAll方法**
	find方法，add方法，addBack方法，end方法

**DOM相关方法**

	html方法和text方法
	addClass方法，removeClass方法，toggleClass方法
	css方法
	prop方法，attr方法

**添加、复制和移动网页元素的方法**

	append方法，appendTo方法
	after方法，insertAfter方法
	before方法，insertBefore方法
	remove方法，detach方法，replaceWith方法

**动画效果方法**

	animate方法
	stop方法，delay方法


## 参考 ##

[阮一峰jQuery教程](https://javascript.ruanyifeng.com/jquery/basic.html#toc12)

[https://zhuanlan.zhihu.com/p/43292677](https://zhuanlan.zhihu.com/p/43292677)

jQuery有自己的一套对象和方法，原生DOM也有自己的一套对象和方法。

jQuery对象返回的是一个类似数组的对象，有length属性，也可以通过下标获取里面某一项的值，但是没有数组的方法。

如何判断所选的元素是jQuery对象还是DOM对象？
我们可以通过判断不存在的元素返回的是什么
如果是原生DOM，那么返回的是null
如果是jQuery对象，那么返回的是类数组对象，但是没有成员。

jQuery对象转换成DOM对象：
在所选的jQuery对象通过下标访问所得到的元素就是DOM对象。
在$()插入DOM对象就可以转换成jQuery对象
