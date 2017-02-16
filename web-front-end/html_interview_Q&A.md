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

>7.html5有哪些新特性、移除了哪些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分HTML和HTML5?

作答：

>8.简述一下你对HTML语义化的理解？

作答：

>9.HTML5的离线储存怎么使用，工作原理能不能解释一下？

作答：

>10.浏览器是怎么对HTML5离线储存资源进行管理和加载的呢？

作答：

>11.请描述一下cookies,sessionStorage和localStorage的区别？

作答：

>12.iframe有哪些缺点？

作答：

>13.Label的作用是什么？是怎么用的？（加for或包裹）

作答：

>14.HTML5的form如何关闭自动完成功能?

作答：

>15.如何实现浏览器内多个标签页之间的通信？

作答：

>16.webSocket如何兼容低浏览器?

作答：

>17.页面可见性（Page Visibility）API可以有哪些用途？

作答：

>18.如何在页面上实现一个圆形的可点击区域？

作答：

>19.实现不适用border画出1px高的线，在不同浏览器的Quirksmode和CSSCompat模式下都能保持同一效果。

作答：

>20.网页验证码是干嘛的，是为了解决什么安全问题？

作答：

>21.title与h1的区别、b和strong的区别、i和em的区别?

作答：