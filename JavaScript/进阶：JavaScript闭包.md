# 闭包 #

> 定义

[MDN定义](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

[javascriptkit](http://www.javascriptkit.com/javatutors/closures.shtml)

## 词法作用域 ##

> 作用域链

- 函数在执行的过程中，先从自己内部找变量
- 如果找不到，再从创建当前函数所在的作用域(词法作用域)去找, 以  此往上
- 注意找的是变量的当前的状态

[作用域链的博客](https://www.jianshu.com/p/6205431ab3cd)

**函数连同它作用域链上的要找的这个变量，共同构成闭包**

一般情况下使用闭包主要是为了

- **封装数据**

- **暂存数据**

> 一个典型的闭包案例

	function car(){
	  var speed = 0
	  function fn(){
	    speed++
	    console.log(speed)
	  }
	  return fn
	}
	
	var speedUp = car()
	speedUp()   //1
	speedUp()   //2

在说闭包时先了解什么是**立即执行语句和立即执行函数以及他们之间的区别**，请移步文末参考博客

当函数内部没有执行以下的代码时

	function fn(){
		speed++
		console.log(speed)
		}
	return fn

在代码执行完成后，函数内部的局部变量speed就会被销毁，由于全局标量speedUp一直存在（除非关闭当前页面，否则全局变量一直存在），那么函数内部的作用域就没有办法被销毁，里面有东西一直被使用，这点与浏览器的垃圾回收机制相仿，当我们执行speedUp()，他会在函数的词法作用域下去寻找，函数里面又返回了一个fn，因而形成闭包，简单的理解为

	var speed = 0
	function fn(){
		 speed++
		 console.log(speed)
	}

这一段代码形成一个闭包，如果不return fn,那函数内部的局部变量就会被销毁。

我们可以看看上述代码利用立即执行语句和立即执行函数可以怎么演变：

	function car(){
	  var speed = 0
	  function fn(){
	    speed++
	    console.log(speed)
	  }
	  return fn
	}
	
	var speedUp = car()

	//1
	function car(){
	  var speed = 0
	  return function (){
	    speed++
	    console.log(speed)
	  }
	}
	
	var speedUp = car()
	
	//2
	function car(speed){
	  return function (){
	    speed++
	    console.log(speed)
	  }
	}
	
	var speedUp = car(3)
	
	//3
	function car(){
	  var speed = arguments[0]
	  return function (){
	    speed++
	    console.log(speed)
	  }
	}
	
	var speedUp = car()
	
	//4
	function car(){
	  var speed = 0
	  return function (){
	    speed++
	    console.log(speed)
	  }
	}
	
	//5 car可以不写，则为匿名函数 
	var speedUp = (function car(speed){
		return function (){
	    speed++
	    console.log(speed)
	  }
	}
	)(3)




> 闭包的相关案例

如下代码输出多少？如果想输出3，那如何改造代码？

	var fnArr = [];
	for (var i = 0; i < 10; i ++) {
	  fnArr[i] =  function(){
	    return i
	  };
	}
	console.log( fnArr[3]() ) // 10

同等演变

假设只有两层循环：

	var fnArr = []
	for (var i = 0; i < 2; i ++) {
		fnArr[i] =  (function(j){
		   return function(){
		     return j
		    } 
		  })(i)
	}
	fnArr[3]()

	//1
	var fnArr = [] 
	fnArr[0] = (function(j){
		   return function(){
		     return j
		    } 
		  })(0)
	}
	fnArr[1] = (function(j){
		   return function(){
		     return j
		    } 
		  })(1)
	}
	fnArr[3]()
	
	//2
	var a = (function(j){
		   return function(){
		     return j
		    } 
		  })(0)
	}
	var b = (function(j){
		   return function(){
		     return j
		    } 
		  })(1)
	}
	b()
	
	//3
	var a = (function(j){
		   return function(){
		     return j
		    } 
		  })(0)
	}
	function fn2(j){
		   return function(){
		     return j
		    }
	}
	var b = fn2(1)
	
	//4
	var a = (function(j){
		   return function(){
		     return j
		    } 
		  })(0)
	}
	function fn2(j){
		   return function(){
		     return j
		    }
		return f
	}
	var b = fn2(1)
	
	//5
	var a = (function(j){
		   return function(){
		     return j
		    } 
		  })(0)
	}
	function fn2(j){
		var j = arguments[0]
		function f(){
		     return j
		    }
		return f
	}
	var b = fn2(1)


改造后（立即执行语句,演变过程）

	var fnArr = []
	for (var i = 0; i < 10; i ++) {
	  fnArr[i] =  (function(j){
	    return function(){
	      return j
	    } 
	  })(i)
	}
	console.log( fnArr[3]() ) // 3

	var fnArr = []
	for (var i = 0; i < 10; i ++) {
	  (function(i){
	    fnArr[i] =  function(){
	      return i
	    } 
	  })(i)
	}
	console.log( fnArr[3]() ) // 3

	var fnArr = []
	for (let i = 0; i < 10; i ++) {
	  fnArr[i] =  function(){
	    return i
	  } 
	}
	console.log( fnArr[3]() ) // 3

封装一个 Car 对象

	var Car = (function(){
	   var speed = 0;
	   function set(s){
	       speed = s
	   }
	   function get(){
	      return speed
	   }
	   function speedUp(){
	      speed++
	   }
	   function speedDown(){
	      speed--
	   }
	   return {
	      setSpeed: setSpeed,
	      get: get,
	      speedUp: speedUp,
	      speedDown: speedDown
	   }
	})()
	Car.set(30)
	Car.get() //30
	Car.speedUp()
	Car.get() //31
	Car.speedDown()
	Car.get()  //30

如下代码输出多少？如何连续输出 0,1,2,3,4

	for(var i=0; i<5; i++){
	  setTimeout(function(){
	    console.log('delayer:' + i )
	  }, 0)
	}

输出结果为：delayer:5（连续输出5个），执行setTimeout时，代码会挂到任务队列中区，待i遍历完成之后执行，而此时i = 5，所以输出delayer:5（连续输出5个）

修改后

	for(var i=0; i<5; i++){
	  (function(j){
	    setTimeout(function(){
	      console.log('delayer:' + j )
	    }, 0)//1000-1000*j    
	  })(i)
	}

或者

	for(var i=0; i<5; i++){
	  setTimeout((function(j){
	    return function(){
	      console.log('delayer:' + j )
	    }
	  }(i)), 0)    
	}

如下代码输出多少？

	function makeCounter() {
	  var count = 0
	
	  return function() {
	    return count++
	  };
	}
	
	var counter = makeCounter()
	var counter2 = makeCounter();
	
	console.log( counter() ) // 0
	console.log( counter() ) // 1
	
	console.log( counter2() ) // 0
	console.log( counter2() ) // 1

补全代码，实现数组按姓名、年纪、任意字段排序

	var users = [
	  { name: "John", age: 20, company: "Baidu" },
	  { name: "Pete", age: 18, company: "Alibaba" },
	  { name: "Ann", age: 19, company: "Tecent" }
	]
	
	users.sort(byName) 
	users.sort(byAge)
	users.sort(byField('company'))

解答

	function byName(user1, user2){
	  return user1.name > user2.name
	}
	
	function byAge (user1, user2){
	  return user1.age > user2.age
	}
	
	function byFeild(field){
	  return function(user1, user2){
	    return user1[field] > user2[field]
	  }
	}
	users.sort(byField('company'))

写一个 sum 函数，实现如下调用方式

	console.log( sum(1)(2) ) // 3
	console.log( sum(5)(-1) ) // 4

解答

	function sum(a) {
	  return function(b) {
	    return a + b
	  }
	}

**函数柯里化-只传递给函数一部分参数来调用它，让它返回一个函数去处理剩下的参数**

# 参考 #

[Javascript-立即调用函数表达式](https://blog.csdn.net/weixin_35987513/article/details/52403756)

[立即执行函数: (function(){...})() 与 (function(){...}()) 有什么区别?](https://segmentfault.com/q/1010000000442042)

[Scoping & Hoisting](https://segmentfault.com/a/1190000000348228)

[什么是立即执行函数？有什么作用？](https://zhuanlan.zhihu.com/p/22465092)

[Javascript闭包（Closure）](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)












