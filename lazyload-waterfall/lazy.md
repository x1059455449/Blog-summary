# 懒加载 #

> 原理

先将img标签中的src链接设为同一张图片（空白图片），将其真正的图片地址存储再img标签的自定义属性中（比如data-src）。当js监听到该图片元素进入可视窗口时，即将自定义属性中的地址存储到src属性中，达到懒加载的效果。

> 翻译过来就是

当你访问一个页面的时候，先把img元素或是其他元素的背景图片路径替换成一张大小为1*1px图片的路径（这样就只需请求一次），只有当图片出现在浏览器的可视区域内时，才设置图片正真的路径，让图片显示出来。这就是图片懒加载。

## 为什么要用 ##

比如一个页面中有很多图片，如淘宝、京东首页等等，如果一上来就发送这么多请求，页面加载就会很漫长，如果js文件都放在了文档的底部，恰巧页面的头部又依赖这个js文件，那就不好办了。更为要命的是：一上来就发送百八十个请求，服务器可能就吃不消了（又不是只有一两个人在访问这个页面）。**而此时懒加载的效果就出来了，不仅可以减轻服务器的压力，而且可以让加载好的页面更快地呈现在用户面前（用户体验好）**

## 优点 ##

	页面加载速度快、可以减轻服务器的压力、节约了流量,用户体验好

### 实现步骤 ###

- 首先，不要将图片地址放到src属性中，而是放到其它属性(如data-original)中。

- 页面加载完成后，根据scrollTop属性判断图片是否在用户的视野内，如果在，则将data-original属性中的值取出存放到src属性中。

- 在滚动事件中重复判断图片是否进入视野，如果进入，则将data-original属性中的值取出存放到src属性中

[demo地址]()

## 预加载 ##

	提前加载图片，当用户需要查看时可直接从本地缓存中渲染

## 预加载的核心要点如下：##

- 图片等静态资源在使用之前的提前请求

- 资源后续使用时可以从缓存中加载，提升用户体验

- 页面展示的依赖关系维护（必需的资源加载完才可以展示页面，防止白屏等）

## 实现预加载主要有三个方法： ##

- html中img标签最初设置为display:none；

- js脚本中使用image对象动态创建好图片；

- 使用XMLHttpRequest对象可以更加精细的控制预加载过程，缺点是无法跨域：

    var xmlhttprequest = new XMLHttpRequest();
	xmlhttprequest.open("GET",src,true);

### 参考 ###

[https://www.jianshu.com/p/4876a4fe7731](https://www.jianshu.com/p/4876a4fe7731)

[https://blog.csdn.net/weixin_35955795/article/details/54411516](https://blog.csdn.net/weixin_35955795/article/details/54411516)

[https://www.cnblogs.com/flyromance/p/5042187.html](https://www.cnblogs.com/flyromance/p/5042187.html)

[https://www.cnblogs.com/Cathamerst/p/7445715.html](https://www.cnblogs.com/Cathamerst/p/7445715.html)

[原生js实现](https://www.deanhan.cn/js-lazyload.html)


