# Web前端面试题目
###### 整理者 hauk0101
## HTML相关部分

>1.Doctype作用？严格模式与混杂模式如何区分？它们有何意义？

作答：

* <!DOCTYPE>声明位于HTML文档中的第一行，处于<html>标签之前。告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。
* 标准模式的排版和JS运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示，模拟老式浏览器的行为以防止站点无法工作。

>2.HTML5为什么只需要写<!DOCTYPE HTML>？

作答：

* HTML5不基于SGML，因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为（让浏览器按照它们应该的方式来运行）；而HTML4.01基于SGML，所以需要对DTD进行引用，才能告知浏览器文档所使用的的文档类型。

>3.行内元素有哪些？块级元素有哪些？空（void）元素有哪些？

作答：

　　CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值，如div的display默认值为“block”,则为“块级”元素；span默认display属性值为“inline”，则为“行内”元素。

* 行内元素：&lt; a &gt;、&lt; b &gt;、&lt; span &gt;、&lt; img &gt;、&lt; input &gt;、&lt; select &gt;、&lt; strong &gt;
* 块级元素：&lt; p &gt;、&lt; div &gt;、&lt; ul &gt;、&lt; ol &gt;、&lt; li &gt;、&lt; dl &gt;、&lt; dt &gt;、&lt; dd &gt;、&lt; h1 &gt;、&lt; h2 &gt;、&lt; h3 &gt;、&lt; h4 &gt;
* 空(void)：&lt; br &gt;、&lt; hr &gt;、&lt; img &gt;、&lt; input &gt;、&lt; link &gt;、&lt; meta &gt;

>4.页面导入样式时，使用link和@import有什么区别?

作答： 

* link属于XHTML标签，除了加载CSS外，还能用于定义RSS，定义rel连接属性等作用，而@import是CSS提供的，只能用于加载CSS
* 页面被加载时，link会同时被加载，而@import引用的CSS会等到页面被加载完成后再加载
* @import是CSS2.1提出的，只在IE5以上才能被识别，而link是XHTML标签，无兼容问题

>5.介绍一下你对浏览器内核的理解？

作答：
　　主要分为两部分：渲染引擎（layoutengineer或RenderingEngine）和JS引擎

* 渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。
* JS引擎:解析和执行JavaScript来实现网页的动态效果。最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。



>6.常见的浏览器内核有哪些?

作答：

* Trident内核：IE、MaxThon、TT、The World、360、搜狗浏览器等。（又称MSHTML）
* Gecko内核：Netscape6及以上版本，FF，MozillaSuite/SeaMonkey等。
* Presto内核：Opera7以上。（Opera内核原为：Presto,现为：Blink）
* Webkit内核：Safari、Chrome等。（Chrome的：Blink(Webkit的分支)）

>7.html5有哪些新特性、移除了哪些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分HTML和HTML5?

作答：

* 新特性：HTML5已经不是SGML的子集，主要是关于图像、位置、存储、多任务等功能的增加。
	* 绘画canvas
	* 用于媒介回放的video和audio元素
	* 本地离线存储localStorage长期存储数据，浏览器关闭后数据不丢失
	* sessionStorage的数据在浏览器关闭后自动删除
	* 语义化更好的内容元素，比如 article、footer、header、nav、section
	* 表单控件，calendar、date、time、email、url、search
	* 新技术，webworker、websocket、Geolocation
* 移除的元素：
	* 纯表现的元素：basefont、big、center、font、s、strike、tt、u
	* 对可用性产生负面影响的元素:frame、frameset、noframes
* 支持HTML新标签：
	* IE8/IE7/IE6支持通过documnet.createElement方法产生的标签
	* 可以利用这一特性让这些浏览器支持HTML5新标签
	* 浏览器支持新标签后，还需要添加标签默认的样式
	* 也可以直接使用成熟的框架，如html5shim

			<!--[ifIt IE9]>
				<script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
			<![endir]-->
* 如何区分HTML5：DOCTYPE声明、新增的结构元素、功能元素

>8.简述一下你对HTML语义化的理解？

作答：

* 用正确的标签做正确的事情。
* html语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引起解析。
* 即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的。
* 搜索引擎的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重，利于SEO。
* 是阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

>9.HTML5的离线储存怎么使用，工作原理能不能解释一下？

作答：

* 在用户没有与Internet连接时，可以正常访问站点或应用，在用户与Internet连接时，更新用户机器上的缓存文件。
* 原理：HTML5的离线存储是基于一个新建的.appcahe文件的缓存机制（不是存储技术），通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。
* 如何使用：
	* 页面头部像下面一样加入一个manifest的属性；
	* 在cache.manifest文件的编写离线存储的资源；

			CACHEMANIFEST
			#v0.11
			CACHE:
			js/app.js
			css/style.css
			NETWORK;
			resourse/logo.png
			FALLBACK;
			//offline.html
	* 在离线状态时，操作window.applicationCache进行需求实现。

>10.浏览器是怎么对HTML5离线储存资源进行管理和加载的呢？

作答：

* 在线情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app,那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。
* 离线的情况下，浏览器就直接使用离线存储的资源。

>11.请描述一下cookies,sessionStorage和localStorage的区别？

作答：

* cookies是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）
* cookies数据始终在同源的http请求中携带（即使不需要），即会在浏览器和服务器间来回传递。
* sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。
* 存储大小：
	* cookie数据大小不能超过4K。
	* sessionStorage和localStorage虽然也有存储大小的限制，但比cookie大的多，可以达到5M或更大。
* 有效时间:
	* localStorage，存储持久数据，浏览器关闭后数据不丢失，除非主动删除数据。
	* sessionStorage，数据在当前浏览器窗口关闭后自动删除。
	* cookie,设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。

>12.iframe有哪些缺点？

作答：

* iframe会阻塞主页面的Onload事件
* 搜索引擎的检索程序无法解读这种页面，不利于SEO
* iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载
* 使用iframe之前需要考虑这两个缺点，如果需要使用iframe，最好是通过JavaScript动态给iframe添加src属性值，这样可以绕开以上两个问题。

>13.Label的作用是什么？是怎么用的？（加for或包裹）

作答：

* label标签来定义表单控制间的关系，当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。

>14.HTML5的form如何关闭自动完成功能?

作答：

* 给不想要提示的form或某个input设置为autocomplete=off。

>15.如何实现浏览器内多个标签页之间的通信？

作答：

* WebSocket、SharedWorker
* 也可以调用localstorge、cookies等本地存储方式
* localstorge另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件，我们通过监听事件，控制它的值来进行页面信息通信
* 注意：Safari在无痕模式下设置localstorge值时会跑出QuotaExceededError的异常

>16.webSocket如何兼容低浏览器?

作答：

* Adobe Flash Scoket
* ActiveX HTMLFile(IE)
* 基于multipart编码发送XHR
* 基于长轮询的XHR

>17.页面可见性（Page Visibility）API可以有哪些用途？

作答：

* 通过visibilityState的值检测页面当前是否可见，以及打开网页的时间等
* 在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放
* 节省服务器资源，Ajax轮询这类服务器资源占用常常会被忽略，关闭这种请求可以节省资源
* 节省内存消耗
* 节省带宽消耗

>18.如何在页面上实现一个圆形的可点击区域？

作答：

* map+area或者svg
* border-radius
* 纯js实现需要求一个点在不在圆上简单算法、获取鼠标坐标等等

>19.实现不使用border画出1px高的线，在不同浏览器的Quirksmode和CSSCompat模式下都能保持同一效果。

作答：

	<div style="height:1px; overflow:hidden;background:red"></div>

>20.网页验证码是干嘛的，是为了解决什么安全问题？

作答：

* 区分用户是计算机还是人的公共自动程序
* 可以防止恶意破解密码、刷票、论坛灌水
* 有效防止黑客对某一个特定注册用户用特定程序暴力破解方式进行不断的登录尝试

>21.title与h1的区别、b和strong的区别、i和em的区别?

作答：

* title属性没有明确意义指标是个标题
* h1则表示层次明确的标题，对页面信息的抓取也有很大的影响
* strong是标注重点内容，有语气加强的含义，使用阅读设备阅读网络时，strong会重读，而b是展示强调内容
* i内容展示位斜体，em表示强调的文本
* 自然样式标签(Physical Style Elements):b,i,u,s,pre
* 语义样式标签(Semantic Style Elements):strong,em,ins,del,code
* 应该准确使用语义样式标签，但不能滥用，如果不能确定时首选使用自然样式标签