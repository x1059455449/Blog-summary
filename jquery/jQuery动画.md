# jQuery 动画 #

## 基础动画 ##

**.hide([duration ] [,easing ] [,complete ])**

用于隐藏元素，没有参数的时候等同于直接设置display属性

> 例子

	$('.target').hide();
	//等同于
	$('.target').css('display', 'none')

	//分割线
	$('#book').hide(300, function() {
	alert('Animation complete.');
	})

	$('#book').hide(300, 'linear', function() {
	   alert('Animation complete.');
	})

**.show( [duration ] [, easing ] [, complete ] )**

用于显示元素，用法和hide类似

**.toggle( [duration ] [, easing ] [, complete ] )**

用来切换元素的隐藏、显示，类似于toggleClass，用法和show、hide类似

	注意：事件处理套件也有一个名为.toggle()方法。哪一个被调用取决于传递的参数的设置

## 渐变 ##

**.fadeIn( [duration ] [, easing ] [, complete ] )**

通过淡入的方式显示匹配元素，参数含义和上面相同

	$('#book').fadeIn('slow', function() {
	// Animation complete
	});

**.fadeOut( [duration ] [, easing ] [, complete ] )**

通过淡出的方式隐藏匹配元素

	$('#book').fadeOut('slow', function() {
	// Animation complete.
	});

**.fadeTo( duration, opacity [, easing ] [, complete ] )**

调整匹配元素的透明度，方法通过匹配元素的不透明度做动画效果

	$('#book').fadeTo('slow', 0.5, function() {
	  // Animation complete.
	});

**.fadeToggle( [duration ] [, easing ] [, complete ] )**

通过匹配的元素的不透明度动画，来显示或隐藏它们，方法执行匹配元素的不透明度动画。当被可见元素调用时，元素不透明度一旦达到0，display样式属性设置为none ，所以元素不再影响页面的布局。

	$("button:first").click(function() {
	  $("p:first").fadeToggle("slow", "linear");
	});

## 滑动 ##

**.slideDown( [duration ] [, easing ] [, complete ] )**

用滑动动画显示一个匹配元素，方法将给匹配元素的高度的动画，这会导致页面的下面部分滑下去，弥补了显示的方式

	$('#book').slideDown('slow', function() {
	    // Animation complete.
	});

**.slideUp( [duration ] [, easing ] [, complete ] )**

用滑动动画隐藏一个匹配元素，方法将给匹配元素的高度的动画，这会导致页面的下面部分滑上去，当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局。 display 样式属性将被设置为none，以确保该元素不再影响页面布局。

	$('#book').slideUp('slow', function() {
	    // Animation complete.
	});

**.slideToggle( [duration ] [, easing ] [, complete ] )**
用滑动动画显示或隐藏一个匹配元素，方法将给匹配元素的高度的动画，这会导致页面中，在这个元素下面的内容往下或往上滑。display属性值保存在jQuery的数据缓存中，所以display可以方便以后可以恢复到其初始值。

如果一个元素的display属性值为inline，然后是隐藏和显示，这个元素将再次显示inline。当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局。

	$('#clickme').click(function() {
	 $('#book').slideToggle('slow', function() {
	 // Animation complete.
	 });
	});

## 动画队列 ##

	$box.hide(1000, function(){
	   $box.show(1000, function(){
	     $box.fadeOut('slow',function(){
	       $box.fadeIn('slow',function(){
	         $box.slideUp(function(){
	           $box.slideDown(function(){
	             console.log('动画执行完毕')
	           })
	         })
	       })
	     })
	   })
	})
	//等价于
	$box.hide(1000)
	    .show(1000)
	    .fadeOut()
	    .fadeIn()
	    .slideUp()
	    .slideDown(function(){
	      console.log('真的完毕了')
	    })

## 自定义动画 ##

上面几个简单的动画不能满足需求的时候，jquery提供了自定义动画行为的方法

	.animate( properties [, duration ] [, easing ] [, complete ] )


properties是一个CSS属性和值的对象,动画将根据这组对象移动。

	$('#clickme').click(function() {
	  $('#book').animate({
	    opacity: 0.25,
	    left: '+=50',
	    height: 'toggle'
	  }, 5000, function() {
	    // Animation complete.
	  });
	});

**.clearQueue**

清除动画队列中未执行的动画

**.finish**

停止当前动画，并清除动画队列中所有未完成的动画,最终展示动画队列最后一帧的最终状态

**.stop( [clearQueue ] [, jumpToEnd ] )**

停止当前正在运行的动画

	clearQueue(default: false)
	jumpToEnd(default: false)


## 参考 ##

[.animate()](https://api.jquery.com/animate/)
