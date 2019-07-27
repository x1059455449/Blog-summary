# 浏览器加载机制

> 网页是什么

	网页 = html +css + javascript

	html:网页元素内容

	css:控制网页样式

	javascript:操作网页内容，实现功能或者效果

> javascript的发展历史

[官网](https://www.javascript.com/)

[MDN教程](https://developer.mozilla.org/en-US/docs/Web/javascript)

[W3C](http://www.w3school.com.cn/js/pro_js_history.asp)

**ES3、ES5、ES6分别指什么**
[https://zhuanlan.zhihu.com/p/22733283](https://zhuanlan.zhihu.com/p/22733283)

### 浏览器的渲染机制(名词解释)

* 解析HTML标签，构建DOM树
* 解析cSS标签，构建CSSOM树
* 把DOM和CSSOM组合成渲染树（render tree）
* 在渲染树的基础上进行布局，计算每个节点的几何结构
* 把每个节点绘制到屏幕上（painting）
![](https://i.imgur.com/va5Vh1Z.png)

### repaint 和 reflow 分别指什么
![](https://i.imgur.com/4kEIARE.png)

	这张图归纳为四个步骤：

	1、解析HTML以构建DOM树：渲染引擎开始解析HTML文档，转换树中的html标签或js生成的标签

	到DOM节点，它被称为 -- 内容树。
	
	2、构建渲染树：解析CSS（包括外部CSS文件和样式元素以及js生成的样式），根据CSS选择器

	计算出节点的样式，创建另一个树 —- 渲染树。
	
	3、布局渲染树: 从根节点递归调用，计算每一个元素的大小、位置等，给每个节点所应该出现

	在屏幕上的精确坐标。
	
	4、绘制渲染树: 遍历渲染树，每个节点将使用UI后端层来绘制好，我们可以看到Repain 和 

	Reflow 分别出现在了第三和第四步。因此我们给出下面的定义：
	
	对于DOM结构中的各个元素都有自己的盒子（模型），这些都需要浏览器根据各种样式（浏览器

	的、开发人员定义的等）来计算并根据计算结果将元素放到它该出现的位置，这个过程称之为

	reflow；当各种盒子的位置、大小以及其他属性，例如颜色、字体大小等都确定下来后，浏览器

	于是便把这些元素都按照各自的特性绘制了一遍，于是页面的内容出现了，这个过程称之为

	repaint。

	可见这两个东东对浏览器渲染页面是很重要的啊，都是会影响性能的，因此我们需要了解一些常

	见的会引起repaint和reflow的一些操作，并且应该尽量减少以提高渲染速度。

> 引起Repain和Reflow的一些操作

	1. 调整窗口大小

	2. 改变字体
	
	3. 增加或者移除样式表

	4. 内容变化，比如用户在input框中输入文字

	5. 激活 CSS 伪类，比如 :hover (IE 中为兄弟结点伪类的激活)

	6. 操作 class 属性

	7. 脚本操作 DOM(包括增加、删除、修改 DOM 结点)

	8. 计算 offsetWidth  和 offsetHeight 属性

	9. 设置 style 属性的值 

	注：display:none 会触发 reflow，而 visibility:hidden 只会

	触发 repaint，因为没有发现位置变化。

> 如何优化

* 尽可能在DOM树的最末端改变class
* 避免设置多层内联样式
* 动画效果应用到position属性为absolute或fixed的元素上
* 避免使用table布局，因为可能很小的一个小改动会造成整个 table 的重新布局

### CSS和JS放置顺序，异步机制(可模拟网速慢的情况)
* 使用link标签将样式放在顶部

* 将JS放在底部

	- 脚本会阻塞后面内容的呈现
	- 脚本会阻塞其后组建的下载

对于图片和CSS，在加载时会并发加载（如一个域名下同时加载两个文件），但在加载JavaScript时，会禁用并发，并且阻止其他内容的下载，所以把 JavaScript放入页面顶部也会导致  **白屏**  现象

### 白屏&FOUC(Flash of Unstyled Content)无样式内容闪烁

> 加载异步

![](https://i.imgur.com/wM7NYyK.png)

### 推荐阅读


> 文章推荐

[https://blog.csdn.net/oscar999/article/details/38379523](https://blog.csdn.net/oscar999/article/details/38379523)

[https://segmentfault.com/a/1190000002629708](https://segmentfault.com/a/1190000002629708)

[https://harttle.land/2016/05/18/async-javascript-loading.html](https://harttle.land/2016/05/18/async-javascript-loading.html)

[https://zhuanlan.zhihu.com/p/22733283](https://zhuanlan.zhihu.com/p/22733283)

[https://www.jianshu.com/p/6617efa874b0](https://www.jianshu.com/p/6617efa874b0)
