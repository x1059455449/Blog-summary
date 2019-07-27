# jQuery #

----------

**来源饥人谷课件，转载请注明出处**

----------

## jQuery介绍 ##

[jQuery使用查询](http://devdocs.io/jquery/)

[jQuery官网](https://jquery.com/)

[jQuery 教程](http://www.w3school.com.cn/jquery/index.asp)

**为什么要用 jQuery**

> DOM API

	难用
	存在兼容性问题
	功能太少，不能与时俱进

> jQuery

	兼容性好
	API 友好
	功能强大，与时俱进

> jQuery使用场景

	DOM 操作较多（事件监听）
	简单的 AJAX
	需要兼容多款浏览器

> 什么时候不用 jQuery

	页面交互极为简单
	页面对流量有苛刻的要求
	上级强制、团队已经有了 jQuery 的代替品

> jQuery 做什么

	选择网页元素
	改变结果集
	元素的操作：取值和赋值
	元素的操作：移动
	元素的操作：复制、删除和创建
	工具方法
	事件操作
	特殊效果
	AJAX

> jQuery 的两种 API(只有这两种用法,全是方法操作)

	$.noConflict()
	$.each()
	$('ul').addClass()
	$('p').text('hi')
	简记：$.abc()  $('.xxx').abc()

**ready**

	$(callback)
	window.onload 事件
	document 的 DOMContentLoaded 事件
	$( document ).ready( handler )
	$().ready( handler ) (this is not recommended)
	$( handler )

## jQuery选择器 ##

> 引用jQuery

	BootCDN 
	
	使用unpkg.com发送至npm(主流)

> 使用jQuery获取元素

我们可以通过document.getElementById等方法获取DOM对象，但是方法名称长，使用不方便，而且功能有限，不能像CSS选择器那样灵活

jQuery定义了一套选择器规则，和CSS选择器目的一样，都是为了选择出符合特定规则的元素。讲jQuery不得不提到其选择器，这是jQuery能够快速流行的非常重要的原因，为了方便使用者jQuery刻意和CSS选择器使用相同的语法，几乎支持所有类型的CSS3选择器，当然也有一些其特定的选择器

## 选择器 ##

基本选择器
	 
	$('\*')	匹配页面所有元素
	$('#id')	id选择器
	$('.class')	类选择器
	$('element')	标签选择器

组合/层次选择器
	 
	$('E,F')	多元素选择器，用”,分隔，同时匹配元素E或元素F
	$('E F')	后代选择器，用空格分隔，匹配E元素所有的后代（不只是子元素、子元素向下递归）元素F
	$(E>F)	子元素选择器，用”>”分隔，匹配E元素的所有直接子元素
	$('E+F')	直接相邻选择器，匹配E元素之后的相邻的同级元素F
	$('E~F')	普通相邻选择器（弟弟选择器），匹配E元素之后的同级元素F（无论直接相邻与否）
	$('.class1.class2')	匹配类名中既包含class1又包含class2的元素

基本过滤选择器
	 
	$("E:first")	所有E中的第一个
	$("E:last")	所有E中的最后一个
	$("E:not(selector)")	按照selector过滤E
	$("E:even")            	所有E中index是偶数
	$("E:odd")             	所有E中index是奇数
	$("E:eq(n)")          	所有E中index为n的元素
	$("E:gt(n)")          	所有E中index大于n的元素
	$("E:lt(n)")           	所有E中index小于n的元素
	$(":header")	选择h1~h6 元素
	$("div:animated")	选择正在执行动画效果的元素

内容过滤器
	 
	$('E:contains(value)')	内容中包含value值的元素
	$('E:empty')	内容为空的元素
	$('E:has(F)')	子元素中有F的元素，$('div:has(a)'):包含a标签的div
	$('E: parent')	父元素是E的元素，$('td: parent'):父元素是td的元素

可视化选择器
	 
	$('E:hidden')	所有被隐藏的E
	$('E:visible')	所有可见的E

属性过滤选择器
	 
	$('E[attr]')	含有属性attr的E
	$('E[attr=value]')	属性attr=value的E
	$('E[attr !=value]')	属性attr！=value的E
	$('E[attr ^=value]')	属性attr以value开头的E
	$('E[attr $=value]')	属性attr以value结尾的E
	$('E[attr \*=value]')	属性attr包含value的E
	$('E[attr][attr \*=value]')	可以连用

子元素过滤器
	 
	$('E:nth-child(n)')	E的第n个子节点
	$('E:nth-child(3n+1)')	E的index符合3n+1表达式的子节点
	$('E:nth-child(even)')	E的index为偶数的子节点
	$('E:nth-child(odd)')	E的index为奇数的子节点
	$('E:first-child')	所有E的第一个子节点
	$('E:last-child')	所有E的最后一个子节点
	$('E:only-child')	只有唯一子节点的E的子节点

表单元素选择器
	 
	$('E:type')	特定类型的input
	$(':checked')	被选中的checkbox或radio
	$('option: selected')	被选中的option

## .eq(index), .get([index]) ##

对于一个特定结果集，我们想获取到指定index的jQuery对象，可以使用eq方法
   
	$('div').eq(3);//获取结果集中的第四个jQuery对象

我们可以通过类数组下标的获取方式或者get方法获取指定index的DOM对象，也就是我们说的jQuery对象转DOM对象

	$('div')[2];
	$('div').eq(2);

get()不写参数把所有对象转为DOM对象返回。addClassList,removeClassList同样适用

## 兄弟元素的获取 ##

## .next([selector]), .prev([selector]) ##

next取得匹配元素集合中的每一个元素紧邻的后面同辈元素的元素集合。如果提供一个选择器，那么只有紧跟着的兄弟元素满足选择器时，才会返回次元素。prev真好相反，获取元素之前的同辈元素

	$('.test').next();
	$('.test').prev('li');

## .nextAll([selector]), .prevAll([selector]) ##

nextAll获得每个匹配元素集合中每个元素所有后面的同辈元素，选择性筛选的选择器，而prevAll与之相反，获取元素前面的同辈元素

## .siblings([selectors]) ##

获得匹配元素集合中每个元素的兄弟元素，可以提供一个可选的选择器

	$('li.third-item').siblings()

## 父子元素获取 ##

## .parent([selector]) ##

取得匹配元素集合中，每个元素的父元素，可以提供一个可选的选择器

	$('li.item-a').parent()

## .parents([selector]) ##

获得集合中每个匹配元素的祖先元素，可以提供一个可选的选择器作为参数

	$('li.item-a').parents('div')

## .children([selector]) ##

获得匹配元素集合中每个元素的子元素，选择器选择性筛选

	$('ul.level-2').children()

## .find([selector]) ##

查找符合选择器的后代元素

	$('ul').find('li.current');

## 筛选当前结果集 ##

**.first()**

获取当前结果集中的第一个对象

**.last()**

获取当前结果集的最后一个对象

**.filter(selector), .filter(function(index))**

筛选当前结果集中符合条件的对象，参数可以是一个选择器或者一个函数

	$('li').filter(':even')
	
	$('li').filter(function(index) {
	  return index % 3 == 2;
	})

![](https://i.imgur.com/jQlZrkp.png)

**.not(selector), .not(function(index))**

从匹配的元素集合中移除指定的元素，和filter相反

**.is(selector), is(function(index)), is(dom/jqObj)**

判断当前匹配的元素集合中的元素，是否为一个选择器，DOM元素，或者jQuery对象，如果这些元素至少一个匹配给定的参数，那么返回true

    if ( $target.is("li") ) {
    $target.css("background-color", "red");
  	}

**.has(selector), .has(dom)**

筛选匹配元素集合中的那些有相匹配的选择器或DOM元素的后代元素

	$('li').has('span')

![](https://i.imgur.com/aZG90RE.png)

# 参考 #

[http://js.jirengu.com/lagucowori/1/](http://js.jirengu.com/lagucowori/1/)