## window.onload ##

	**该load事件触发在文件加载过程结束。此时，文档中的所有对象都在DOM中，并且所有图像和子帧都已完成加载**

但也有Event reference，如DOMContentLoaded和DOMFrameContentLoaded（可使用处理EventTarget.addEventListener()），这些页面的DOM已建成后被解析，但不要等待其他资源来完成加载。

## 详情请参考： ##

[window.onload](https://developer.mozilla.org/en-US/docs/Web/API/window.onload?redirect=no)

[Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)


----------

----------

## document.onDOMContentLoaded ##

**在DOMContentLoaded当最初的HTML文档已被完全加载和分析事件被触发，而无需等待样式表，图片和子框架完成加载。**load 应该仅使用一个非常不同的事件来检测完全加载的页面。使用load哪里DOMContentLoaded更合适是一个非常常见的错误，所以要小心。

## 详情请参考： ##

[DOMCont ent Loaded](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded)


----------

----------

## $(document).ready ##

$(document).ready指定DOM完全加载时要执行的函数.

.ready()只要页面的文档对象模型（DOM）可以安全地操作，该方法就提供了一种运行JavaScript代码的方法。这通常是在用户查看或与页面交互之前执行所需任务的好时机，例如添加事件处理程序和初始化插件。当通过对此方法的连续调用添加多个函数时，它们在DOM按照添加顺序准备就绪时运行。从jQuery 3.0开始，jQuery确保在一个处理程序中发生的异常不会阻止随后添加的处理程序执行。

大多数浏览器以事件的形式提供类似的功能DOMContentLoaded。但是，**jQuery的.ready()方法以一种重要且有用的方式不同：如果DOM准备就绪并且DOMContentLoaded在代码调用之前浏览器触发.ready( handler )，则该函数handler仍将被执行。相反，DOMContentLoaded事件触发后添加的事件侦听器永远不会执行。**

**浏览器还在对象load上提供事件window。当此事件触发时，表示页面上的所有资源都已加载，包括图像。**可以在jQuery中使用查看此事件$( window ).on( "load", handler )。如果代码依赖于加载的资源（例如，如果需要图像的尺寸），则应将代码放在load事件的处理程序中。

请注意，虽然DOM在页面完全加载之前总是准备就绪，但在处理程序执行的代码中附加事件侦听器通常是不安全的。例如，脚本可以在使用诸如的方法加载页面后很长时间内动态加载。虽然添加处理程序将始终处于动态加载脚本来执行，该的已经发生的事件以及那些听众将永远不会运行。load.ready()$.getScript().ready()windowload

## 详情请参考： ##

[.ready()](http://api.jquery.com/ready/)

## 总结 ##

window.onload：**事件触发在文件加载过程结束**。此时，文档中的所有对象都在DOM中，并且所有图像和子帧都已完成加载

document.onDOMContentLoaded：**在DOMContentLoaded当最初的HTML文档已被完全加载和分析事件被触发**，而无需等待样式表，图片和子框架完成加载。

$(document).ready：如果DOM准备就绪并且DOMContentLoaded在代码调用之前浏览器触发.ready( handler )，则该函数handler仍将被执行。相反，DOMContentLoaded事件触发后添加的事件侦听器永远不会执行。

一般onload只能执行一次 ready方法可以执行多次