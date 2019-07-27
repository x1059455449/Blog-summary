## 协商缓存 ##

[深入理解浏览器的缓存机制](https://www.infoq.cn/article/8VU-VCrhoxducaFPrNOL)

[缓存（二）——浏览器缓存机制：强缓存、协商缓存](https://github.com/amandakelake/blog/issues/41)

[彻底理解浏览器的缓存机制](https://heyingye.github.io/2018/04/16/%E5%BD%BB%E5%BA%95%E7%90%86%E8%A7%A3%E6%B5%8F%E8%A7%88%E5%99%A8%E7%9A%84%E7%BC%93%E5%AD%98%E6%9C%BA%E5%88%B6/)

[HTTP强缓存和协商缓存](https://segmentfault.com/a/1190000008956069)

## 常见Http方法 ##

[P41]

## 持久连接 ##

每次的请求都会造成无谓的 TCP 连接建立和断开，增加通信量的开销。为解决上述 TCP 连接的问题，HTTP/1.1 和一部分的 HTTP/1.0 想出了持久连接（HTTP Persistent Connections，也称为 HTTP keep-alive 或HTTP connection reuse）的方法。持久连接的特点是，只要任意一端
没有明确提出断开连接，则保持 TCP 连接状态。

[P44]

## 管线化 ##

[P45]

## 常见Http方法 ##

GET 强调要

POST 强调给

PUT 提交

HEAD 拿到报文首部，不是报文主体

DELETE 删除

OPTIONS 询问支持的方法

CONNECT 要求用隧道协议连接代理

## RESTful API ##

表现层状态转换（英语：Representational State Transfer，缩写：REST），API设计规范，HTTP方法与对应数据库增删改查对应

	GET：读取（Read）
	POST：新建（Create）
	PUT：更新（Update）
	PATCH：更新（Update），通常是部分更新
	DELETE：删除（Delete）

范例

	GET /books , 列出所有的图书
	POST /books , 创建一本图书
	PUT /books, 批量更新图书信息
	DELETE /books, 删除所有图书
	GET /books/10， 获取10号图书详细信息
	PUT /books/10， 更新10号图书
	PATCH /books/10， 更新10号图书
	DELETE /books/10, 删除10号图书

## 拓展 ##

> GET 和 POST 的不同

> PUT和PATCH有什么差别

有以下字段：

	{
	    "username": "guangzai"
	    "email": "guanzgai@163.com" 
	}

PUT修改传参，需包含全部参数

	{
	    "username": "hunger"
	    "email": "guanzgai@163.com" 
	}

PATCH修改传参，只需要传递需要修改的参数
	
	{
	    "email": "guanzgai@163.com" 
	}

另外推荐在URL中强制加入版本号，如

	GET /v1/books

> Form表单支持哪些方法

form表单只支持 post 和get。但是可以通过变通的方法，让服务器知道你本意是想做什么。

	<form action="/books" method="POST">
	    <input type="hidden" name="_method" value="PUT">
	</form>

## 参考 ##

[Learn REST: A RESTful Tutorial](https://www.restapitutorial.com/)

