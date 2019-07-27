## jQuery DOM操作 ##

----------

***来源饥人谷课件，转载请注明来源***

----------

## 创建元素 ##

只需要把DOM字符串传入$方法即可返回一个jQuery对象

	var obj = $('<div class="test"><p><span>Done</span></p></div>');

## 添加元素 ##

###.append(content[,content]) / .append(function(index,html))###

Insert content, specified by the parameter, to the end of each element in the set of matched elements.

- 可以一次添加多个内容，内容可以是DOM对象、HTML string、 jQuery对象

- 如果参数是function，function可以返回DOM对象、HTML string、 jQuery对象，参数是集合中的元素位置与原来的html值

例子

	$( ".inner" ).append( "<p>Test</p>" );
	$( "body" ).append( $newdiv1, [ newdiv2, existingdiv1 ] );
	$( "p" ).append( "<strong>Hello</strong>" );
	$( "p" ).append( $( "strong" ) );
	$( "p" ).append( document.createTextNode( "Hello" ) );

### .appendTo(target) ###

把对象插入到目标元素尾部，目标元素可以是selector, DOM对象, HTML string, 元素集合, jQuery对象;

Insert every element in the set of matched elements to the end of the target.

	$( "h2" ).appendTo( $( ".container" ) );
	$( "<p>Test</p>" ).appendTo( ".inner" );

### .prepend(content[,content]) / .prepend(function(index,html)) ###

向对象头部追加内容，用法和append类似，内容添加到最开始

Insert content, specified by the parameter, to the beginning of each element in the set of matched elements.

	$( ".inner" ).prepend( "<p>Test</p>" );

### .prependTo(target) ###

把对象插入到目标元素头部，用法和prepend类似

Insert every element in the set of matched elements to the beginning of the target.

	$( "<p>Test</p>" ).prependTo( ".inner" );

### .before([content][,content])/ .before(function) ###

在对象前面(不是头部，而是外面，和对象并列同级)插入内容，参数和append类似

Insert content, specified by the parameter, before each element in the set of matched elements.

	$( ".inner" ).before( "<p>Test</p>" );
	$( ".container" ).before( $( "h2" ) );
	$( "p" ).first().before( newdiv1, [ newdiv2, existingdiv1 ] );
	$( "p" ).before( "<b>Hello</b>" );
	$( "p" ).before( document.createTextNode( "Hello" ) );

### .insertBefore(target) ###

把对象插入到target之前（同样不是头部，是同级）

Insert every element in the set of matched elements before the target.

	$( "h2" ).insertBefore( $( ".container" ) );

### .after([content][,content]) .after(function（index）) ###

和before相反，在对象后面(不是尾部，而是外面，和对象并列同级)插入内容，参数和append类似

Insert content, specified by the parameter, after each element in the set of matched elements.

	$( ".inner" ).after( "<p>Test</p>" );
	$( "p" ).after( document.createTextNode( "Hello" ) );

### .insertAfter(target) ###

和insertBefore相反，把对象插入到target之后（同样不是尾部，是同级）

Insert every element in the set of matched elements after the target.

	$( "<p>Test</p>" ).insertAfter( ".inner" );
	$( "p" ).insertAfter( "#foo" );

## 删除元素 ##

### .remove([selector]) ###

删除被选元素（及其子元素）

	$("#div1").remove();

我们也可以添加一个可选的选择器参数来过滤匹配的元素

	$('div').remove('.test');

### .empty() ###

清空被选择元素内所有子元素

Remove all child nodes of the set of matched elements from the DOM.

	$('body').empty();

### .detach() ###

.detach() 方法和.remove()一样, 除了 .detach()保存所有jQuery数据和被移走的元素相关联。当需要移走一个元素，不久又将该元素插入DOM时，这种方法很有用。

## 包裹元素 ##

### wrap(wrappingElement) / .wrap(function(index)) ###

为每个对象包裹一层HTML结构，可以是selector, element, HTML string, jQuery object

Wrap an HTML structure around each element in the set of matched elements.

	<div class="container">
	  <div class="inner">Hello</div>
	  <div class="inner">Goodbye</div>
	</div>

包裹元素

	$( ".inner" ).wrap( "<div class='new'></div>" );

看看结果
	
	<div class="container">
	  <div class="new">
	    <div class="inner">Hello</div>
	  </div>
	  <div class="new">
	    <div class="inner">Goodbye</div>
	  </div>
	</div>

### .wrapAll(wrappingElement) ###

把所有匹配对象包裹在同一个HTML结构中

Wrap an HTML structure around all elements in the set of matched elements.

	<div class="container">
	  <div class="inner">Hello</div>
	  <div class="inner">Goodbye</div>
	</div>

包裹元素

	$( ".inner" ).wrapAll( "<div class='new' />");

看看结果

    <div class="container">
      <div class="new">
        <div class="inner">Hello</div>
        <div class="inner">Goodbye</div>
      </div>
    </div>

### .wrapInner(wrappingElement) / .wrapInner(function(index)) ###

包裹匹配元素内容，这个不好描述，一看例子就懂

Wrap an HTML structure around the content of each element in the set of matched elements.

<div class="container">
  <div class="inner">Hello</div>
  <div class="inner">Goodbye</div>
</div>
包裹元素

	$( ".inner" ).wrapInner( "<div class='new'></div>");

执行结果

	<div class="container">
	  <div class="inner">
	    <div class="new">Hello</div>
	  </div>
	  <div class="inner">
	    <div class="new">Goodbye</div>
	  </div>
	</div>

### .unwrap() ###

把DOM元素的parent移除

Remove the parents of the set of matched elements from the DOM, leaving the matched elements in their place.

	pTags = $( "p" ).unwrap();

### html([string]) ###

这是一个读写两用的方法，用于获取/修改元素的innerHTML

当没有传递参数的时候，返回元素的innerHTML
当传递了一个string参数的时候，修改元素的innerHTML为参数值
看个例子

	$('div').html()
	
	$('div').html('123')

后续这种读写两用的方法很多，原理都类似

如果结果是多个进行赋值操作的时候会给每个结果都赋值
如果结果多个，获取值的时候，返回结果集中的第一个对象的相应值

### text() ###

和html方法类似，操作的是DOM的innerText值


## 属性&CSS操作 ##

**属性相关**

**.val([value])**

这是一个读写双用的方法，用来处理input的value，当方法没有参数的时候返回input的value值，当传递了一个参数的时候，方法修改input的value值为参数值

	$('input').val()
	
	$('input').val('newValue');
**.attr()/.attr(attributeName)**

获取元素特定属性的值

Get the value of an attribute for the first element in the set of matched elements.

	var title = $( "em" ).attr( "title" );

**.attr(attributeName,value) / .attr
(attributesJson) / .attr( attributeName, function(index, attr) )**

为元素属性赋值

Set one or more attributes for the set of matched elements.

	$( "#greatphoto" ).attr( "alt", "Beijing Brush Seller" );
	
	$( "#greatphoto" ).attr({
	  alt: "Beijing Brush Seller",
	  title: "photo by Kelly Clark"
	});
	
	$( "#greatphoto" ).attr( "title", function( i, val ) {
	  return val + " - photo by Kelly Clark";
	});//这里用id选择符举例是不是function永远最多迭代一次？用类选择符是不是更好些？

**.removeAttr()**

为匹配的元素集合中的每个元素中移除一个属性（attribute）

.removeAttr() 方法使用原生的 JavaScript removeAttribute() 函数,但是它的优点是可以直接在一个 jQuery 对象上调用该方法，并且它解决了跨浏览器的属性名不同的问题。

	$('div').removeAttr('id');

**.prop()/.removeProp()**

这两个方法是用来操作元素的property的，property和attibute是非常相似的概念，感兴趣的同学可以看看jQuery的attr与prop

[jQuery的attr与prop](http://www.cnblogs.com/dolphinX/p/3348582.html)

## CSS相关 ##

**.css()**

这是个和attr非常相似的方法，用来处理元素的css

**.css(propertyName) / .css(propertyNames)**

获取元素style特定property的值

Get the value of style properties for the first element in the set of matched elements.

	var color = $( this ).css( "background-color" );
	
	var styleProps = $( this ).css([
	  "width",
	  "height",
	  "color",
	  "background-color"
	]);

**.css(propertyName,value) / .css( propertyName, function(index, value) ) / .css( propertiesJson )**

设置元素style特定property的值

Set one or more CSS properties for the set of matched elements.

	$( "div.example" ).css( "width", function( index ) {
	  return index * 50;
	});
	
	$( this ).css( "width", "+=200" );
	
	$( this ).css( "background-color", "yellow" );
	
	$( this ).css({
	  "background-color": "yellow",
	  "font-weight": "bolder"
	});

**.addClass(className) / .removeClass(className)
.addClass(className) / .addClass(function(index,currentClass))**

为元素添加class，不是覆盖原class，是追加，也不会检查重复

Adds the specified class(es) to each of the set of matched elements.

	$( "p" ).addClass( "myClass yourClass" );
	
	$( "ul li" ).addClass(function( index ) {
	  return "item-" + index;
	});

**removeClass([className]) / ,removeClass(function(index,class))**

移除元素单个/多个/所有class

Remove a single class, multiple classes, or all classes from each element in the set of matched elements.

	$( "p" ).removeClass( "myClass yourClass" );
	
	$( "li:last" ).removeClass(function() {
	  return $( this ).prev().attr( "class" );
	});

**.hasClass(className)**

检查元素是否包含某个class，返回true/false

Determine whether any of the matched elements are assigned the given class.

	$( "#mydiv" ).hasClass( "foo" )

**.toggleClass(className)**

toggle是切换的意思，方法用于切换，switch是个bool类型值，这个看例子就明白

	<div class="tumble">Some text.</div>

第一次执行

	$( "div.tumble" ).toggleClass( "bounce" )
	
	<div class="tumble bounce">Some text.</div>

第二次执行

	$( "div.tumble" ).toggleClass( "bounce" )
	
	<div class="tumble">Some text.</div>

## 常用函数 ##

## .each( function(index, Element) ) ##

遍历一个jQuery对象，为每个匹配元素执行一个函数

	$( "li" ).each(function( index ) {
	  console.log( index + ":" + $(this).text() );
	});

## jQuery.each( collection, callback(indexInArray, valueOfElement) ) ##

一个通用的迭代函数，它可以用来无缝迭代对象和数组。数组和类似数组的对象通过一个长度属性（如一个函数的参数对象）来迭代数字索引，从0到length - 1。其他对象通过其属性名进行迭代。

	var obj = {
	  "flammable": "inflammable",
	  "duh": "no duh"
	};
	$.each( obj, function( key, value ) {
	  alert( key + ": " + value );
	});

## .map( callback(index, domElement) ) ##

通过一个函数匹配当前集合中的每个元素,产生一个包含新的jQuery对象

	$('div').map(function(i, ele){
	    return this.id;
	});

## jQuery.extend([deep,] target [, object1 ] [, objectN ] ) ##

- 当我们提供两个或多个对象给$.extend()，对象的所有属性都添加到目标对象（target参数）。

- 如果只有一个参数提供给$.extend()，这意味着目标参数被省略。在这种情况下，jQuery对象本身被默认为目标对象。这样，我们可以在jQuery的命名空间下添加新的功能。这对于插件开发者希望向 jQuery 中添加新函数时是很有用的

目标对象（第一个参数）将被修改，并且将通过$.extend()返回。然而，如果我们想保留原对象，我们可以通过传递一个空对象作为目标对象：

	var object = $.extend({}, object1, object2);

在默认情况下，通过$.extend()合并操作不是递归的;

如果第一个对象的属性本身是一个对象或数组，那么它将完全用第二个对象相同的key重写一个属性。这些值不会被合并。如果将 true作为该函数的第一个参数，那么会在对象上进行递归的合并。

	var object1 = {
	  apple: 0,
	  banana: { weight: 52, price: 100 },
	  cherry: 97
	};
	var object2 = {
	  banana: { price: 200 },
	  durian: 100
	};
	
	// Merge object2 into object1
	$.extend( object1, object2 );

## .clone( [withDataAndEvents ] ) ##

.clone()方法深度复制所有匹配的元素集合，包括所有匹配元素、匹配元素的下级元素、文字节点

通常我们将页面上一个元素插入到DOM里另一个地方，它会被从老地方移走，类似剪切的效果

	$('.hello').appendTo('.goodbye');
	
	<div class="container">
	  <div class="goodbye">
	    Goodbye
	    <div class="hello">Hello</div>
	  </div>
	</div>

但是我们如果需要的是复制而不是剪切，我们可以像下面这样写代码：

	$('.hello').clone().appendTo('.goodbye');

## .index() / .index(selector)/ .index(element) ##

从给定集合中查找特定元素index

Search for a given element from among the matched elements.

- 没参数返回第一个元素index

- 如果参数是DOM对象或者jQuery对象，则返回参数在集合中的index

- 如果参数是选择器，返回第一个匹配元素index，没有找到返回-1

例子

	var listItem = $( "#bar" );
	alert( "Index: " + $( "li" ).index( listItem ) );

## .ready( handler ) ##

当DOM准备就绪时，指定一个函数来执行。

虽然JavaScript提供了load事件，当页面呈现时用来执行这个事件，直到所有的东西，如图像已被完全接收前，此事件不会被触发。

在大多数情况下，只要DOM结构已完全加载时，脚本就可以运行。传递处理函数给.ready()方法，能保证DOM准备好后就执行这个函数，因此，这里是进行所有其它事件绑定及运行其它 jQuery 代码的最佳地方。

如果执行的代码需要在元素被加载之后才能使用时，（例如，取得图片的大小需要在图片被加载完后才能知道），就需要将这样的代码放到 load 事件中。

下面两种语法全部是等价的：

	$(document).ready(handler)
	$(handler)

我们经常这么使用
	
	$(function(){
	    console.log('ready');
	});

### 参考 ###

