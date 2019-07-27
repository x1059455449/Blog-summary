## XSS攻击 ##

> 什么是XSS攻击

XSS又称CSS，全称Cross SiteScript，跨站脚本攻击，是Web程序中常见的漏洞，XSS属于被动式且用于客户端的攻击方式，所以容易被忽略其危害性。其原理是攻击者向有XSS漏洞的网站中输入(传入)恶意的HTML代码，当其它用户浏览该网站时，这段HTML代码会自动执行，从而达到攻击的目的。如，盗取用户Cookie、破坏页面结构、重定向到其它网站等。

XSS攻击类似于SQL注入攻击，攻击之前，我们先找到一个存在XSS漏洞的网站，XSS漏洞分为两种，一种是DOM Based XSS漏洞，另一种是Stored XSS漏洞。理论上，所有可输入的地方没有对输入数据进行处理的话，都会存在XSS漏洞，漏洞的危害取决于攻击代码的威力，攻击代码也不局限于script。

[百度对XSS的解释](https://baike.baidu.com/item/xss/917356)

[XSS攻击](https://blog.csdn.net/ghsau/article/details/17027893)

[XSS攻击方式](http://www.cnblogs.com/bangerlee/archive/2013/04/06/3002142.html)

> 为什么不推荐使用eval(关于安全性方面)

eval只是一个普通的函数，只不过他有一个快速通道通向编译器，可以将string变成可执行的代码。有类似功能的还有Function , setInterval 和 setTimeout。

关于安全性，我们经常听到eval是魔鬼，他会引起XSS攻击，实际上，如果我们对信息源有足够的把握时，eval并不会引起很大的安全问题。而且不光是eval，其他方式也可能引起安全问题。比如：莫名其妙给你注入一个标<script src=""\>签，或者一段来历不明的JSON-P请求，再或者就是Ajax请求中的eval代码… 因此，只要你的信息源不安全，你的代码就不安全。不单单是因为eval引起的。你用eval的时候会在意XSS的问题，你越在意就越出问题，出的多了，eval就成噩梦了。

[推荐阅读：JavaScript 为什么不推荐使用 eval？](https://www.zhihu.com/question/20591877)

> 如何防范

1. 过滤用户输入
2. 对不可信输出编码
3. 安全Cookie
4. 提高防范意识、多测试

[https://segmentfault.com/a/1190000009514661](https://segmentfault.com/a/1190000009514661)

主要是前面三个措施，后者还需用户提高意识

## CSRF ##

> 什么是CSRF攻击

Cross Site Request Forgery，中文名：跨站请求伪造。其原理是攻击者构造网站后台某个功能接口的请求地址，诱导用户去点击或者用特殊方法让该请求地址自动加载。用户在登录状态下这个请求被服务端接收后会被误以为是用户合法的操作。对于 GET 形式的接口地址可轻易被攻击，对于 POST 形式的接口地址也不是百分百安全，攻击者可诱导用户进入带 Form 表单可用POST方式提交参数的页面

## 详情参考 ##

[浅谈CSRF攻击方式](http://www.cnblogs.com/hyddd/archive/2009/04/09/1432744.html)

[常见网络攻击--XSS && CSRF](https://segmentfault.com/a/1190000009514661)


> 如何防范

1.规范请求类型。

任何资源操作的请求，必须是POST、PUT、DELETE，总之不能是GET

2.检查Referer

即检查请求头中的来源网站，从而保证此次请求来源于信任的网站。

3.设置请求Token

当我访问页面时，服务端会在页面写入一个随机token值,并设置token生命周期。之后我的请求就必须带上此次token值，请求过的token就会失效，无法再用。更加安全性的页面，如登录页面，应该加验证码。

4.防住第一道防线-XSS

再次强调，如果cookie被别人拿走，任何防御都将在理论上失效。上述的防御手段仅仅是提高攻击门槛。有了你的cookie，我可以直接请求你的页面，获取你的token，获取你的验证码图片并解析出来，然后再发起请求。而服务器还以为这是你本人。

## Https ##

> 什么是https

HTTPS（全称：Hyper Text Transfer Protocol over Secure Socket Layer 或 Hypertext Transfer Protocol Secure，超文本传输安全协议），是以安全为目标的HTTP通道，简单讲是HTTP的安全版。即HTTP下加入SSL层，HTTPS的安全基础是SSL，因此加密的详细内容就需要SSL。 它是一个URI scheme（抽象标识符体系），句法类同http:体系。用于安全的HTTP数据传输。https:URL表明它使用了HTTP，但HTTPS存在不同于HTTP的默认端口及一个加密/身份验证层（在HTTP与TCP之间）。这个系统的最初研发由网景公司(Netscape)进行，并内置于其浏览器Netscape Navigator中，提供了身份验证与加密通讯方法。现在它被广泛用于万维网上安全敏感的通讯，例如交易支付方面.

[详情参考httpswiki](https://en.wikipedia.org/wiki/HTTPS)

> 保证措施

服务器给你发送非对称加密的公钥，你用这个公钥来加密对称密钥，服务器用非对称的私钥解密成对称密钥，再利用双方都知道的公用密钥来传递信息
利用ca证书老保证服务器传给你的公钥是安全的

> 如何防范（加密）

1 对称加密 ： 加密和解密数据使用同一个密钥。这种加密方式的优点是速度很快，常见对称加密的算法有 AES；

2 非对称加密： 加密和解密使用不同的密钥，叫公钥和私钥。数据用公钥加密后必须用私钥解密，数据用私钥加密后必须用公钥解密。一般来说私钥自己保留好，把公钥公开给别人，让别人拿自己的公钥加密数据后发给自己，这样只有自己才能解密。 这种加密方式的特点是速度慢，CUP 开销大，常见非对称加密算法有 RSA；

3 Hash： hash 是把任意长度数据经过处理变成一个长度固定唯一的字符串，但任何人拿到这个字符串无法反向解密成原始数据（解开你就是密码学专家了），Hash 常用来验证数据的完整性。常见 Hash 算法有 MD5（已经不安全了）、SHA1、SHA256

## 参考文章 ##

[跨站请求伪造wiki](https://zh.wikipedia.org/wiki/%E8%B7%A8%E7%AB%99%E8%AF%B7%E6%B1%82%E4%BC%AA%E9%80%A0)

[跨站脚本wiki](https://zh.wikipedia.org/wiki/%E8%B7%A8%E7%B6%B2%E7%AB%99%E6%8C%87%E4%BB%A4%E7%A2%BC)

[https-wiki](https://en.wikipedia.org/wiki/HTTPS)

