.on( events [,selector ] [,data ], handler(eventObject) )
看起来参数及其复杂，我们看一下各个参数的意思

events：一个或多个空格分隔的事件类型和可选的命名空间，或仅仅是命名空间，比如"click", "keydown.myPlugin", 或者 ".myPlugin"

selector：一个选择器字符串，用于过滤出被选中的元素中能触发事件的后代元素。如果选择器是 null 或者忽略了该选择器，那么被选中的元素总是能触发事件

data：当一个事件被触发时，要传递给事件处理函数的event.data

handler(eventObject)：事件被触发时，执行的函数。若该函数只是要执行return false的话，那么该参数位置可以直接简写成 false

例子
	
	<div class="box">
	  <ul>
	    <li>我</li>
	    <li>爱</li>
	    <li>前</li>
	    <li>端</li>
	  </ul>
	</div>
	<input id="ipt" type="text"> <button id="btn">添加</button>
	<div id="wrap">
	</div>
	
	<script>
	$('.box li').on('click', function(){
	    console.log(1)
	  var str = $(this).text()
	  $('#wrap').text(str)
	})
	
	//等同于
	$('.box>ul>li').click(function(){
	    console.log(2)
	  var str = $(this).text()
	  $('#wrap').text(str)
	})
	
	//也可以这样写
	$('.box li').on('click.hello', function(){
	    console.log(3)
	  var str = $(this).text()
	  $('#wrap').text(str)
	})
	//命名空间没什么特别的作用，只不过在解绑事件时便于区分绑定的事件
	$('.box li').off('click.hello')
	
	//可是用如下方法新增的元素是没绑定事件的
	$('#btn').on('click', function(){
	  var value = $('#ipt').val()
	  $('.box>ul').append('<li>'+value+'</li>')
	})
	
	//我们可以用事件代理
	$('.box ul').on('click', 'li', function(){
	  var str = $(this).text()
	  $('#wrap').text(str)
	})
	
	setTimeout(function({
	$('.box li').eq(0).trigger('click')
	},3000)

	//上面代码相当于原生 js 的
	document.querySelector('.box ul').addEventListener('click', function(e){
	    if(e.target.tagName.toLowerCase() === 'li'){
	        //do something
	    }
	})
	
	//绑定事件的时候我们也可以给事件附带些数据，只不过这种用法很少见
	$('.box').on('click', {name: 'hunger'}, function(e){
	    console.log(e.data)
	})
	</script>
**.one( events [, selector ] [, data ], handler(eventObject) )**

同 on，绑定事件，但只执行一次，之后再怎么点击也是没有反应的(将上述on改成one，则全部只执行一次)

**.off( events [, selector ] [, handler ] )**

移除一个事件处理函数

	$('.box li').off('click')

**.trigger( eventType [, extraParameters ] )**

根据绑定到匹配元素的给定的事件类型执行所有的处理程序和行为,相当于用代码去触发事件,事件不一定是浏览器的默认事件，已有事件，自定义的事件也可以

	$('#foo').on('click', function() {
	  console.log($(this).text())
	});
	$('#foo').trigger('click')

### 其它 ###

![](https://i.imgur.com/VVSjlSr.png)

### 参考网站 ###

[jquery查询](https://oscarotero.com/jquery/)


