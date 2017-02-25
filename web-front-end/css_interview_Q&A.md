# Web前端面试题目
###### 整理者 hauk0101
## CSS相关部分

>1.介绍一下标准的CSS的盒子模型？与低版本IE的盒子模型有什么不同的？

作答：

* 有两种，IE盒子模型，W3C盒子模型
* 盒模型：内容（content）、填充（padding）、边界（margin）、边框（border）
* 区别：IE的content部分 把border和padding计算了进去 

>2.CSS选择符有哪些？哪些属性可以继承？

作答：

* id选择器（#myid）
* 类选择器（.myclassname）
* 标签选择器(div，h1,p)
* 相邻选择器（div+p）
* 子选择器（ul>li）
* 后代选择器（div a）
* 通配符选择器 （*）
* 属性选择器（a[rel="external"]）
* 伪类选择器（a:hover,li:nth-child）
* 可继承的样式：font-size | font-family | color | ul | li | dl | dd | dt
* 不可继承的样式：border | padding | margin | width | height

>3.CSS优先级算法如何计算？

作答：

* 优先级就近原则，同权重情况下样式定义最近者为准
* 载入样式以最后载入的定位为准
* 优先级排序：
	* 同权重：内联样式表（标签内部）> 嵌入样式表（当前文件中）> 外部样式表（外部文件中，即引用的样式文件）
	* !important > id > class > tag
	* important比内联优先级高

>4.CSS新增的伪类有哪些？

作答：

* p:first-of-type 选择属于其父元素的首个 p 元素的每个 p 元素
* p:last-of-type  选择属于其父元素的最后 p 元素的每个 p 元素
* p:only-of-type  选择属于其父元素唯一的 p 元素的每个 P 元素
* p:only-child    选择属于其父元素的唯一子元素的每个 p 元素
* p:nth-child(n)  选择属于其父元素的第n个子元素的每个 p 元素
* :after          在元素之后添加内容，也可以用来做清除浮动
* :before         在元素之前添加内容
* :enabled|disabled 控制表单控件的禁用状态
* :checked        单选框或复选框被选中

>5.如何居中div？如何居中一个浮动元素？如何让绝对定位的div居中？

作答：

* 使用css3将一个div水平和垂直居中显示
* 方案一：div绝对定位水平垂直居中（margin:auto实现绝对定位元素居中）

		/* 
		 *	代码两个关键点：
		 *	1.上下左右均设置0位置定位
		 *	2.margin:auto,其中width、height如何更改都是居中显示的，兼容性可以，IE7之
		 *	前版本不支持
		 */

		.div{
			width:100px;
			height:100px;
			position:absolute;
			text-align:center;
			left:0;
			right:0;
			bottom:0;
			margin:auto;
		}

	* 优点：
		* 支持跨浏览器，包括IE8-IE10
		* 无需其他特殊标记，CSS代码量少
		* 支持百分比%属性值和min-/max-属性
		* 只用这一个类可实现任何内容块居中
		* 不论是否设置padding都可居中（在不适用box-sizing属性的前提下）
		* 内容块可以被重绘
		* 完美支持图片居中
	* 缺点：
		* 必须声明高度（查看可变高度Variable Height）
		* 建议设置overflow:auto来防止内容越界溢出
		* 在Windows Phone设备上不起作用
* 方案二：div绝对定位水平垂直居中（margin负间距）

		/* 
		 * 代码关键点：
		 * 1.必须知道该div的宽度和高度
		 * 2.然后设置位置为绝对位置
		 * 3.距离页面窗口左边框和上边框的距离设置为50%，这个50%就是指页面窗口的宽度和高度的50%
		 * 4.最后将该div分别左移和上移，左移和上移的大小就是该DIV宽度和高度的一半
		 */
		
		.div{
			width:100px;
			height:100px;
			position:absolute;
			text-align:center;
			left:50%;
			top:50%;
			margin:-50px 0 0 -50px;
		}
	* 优点：
		* 良好的跨浏览器特性，兼容IE6-IE7
		* 代码量少
	* 缺点：
		* 不能自适应，不支持百分比尺寸和min-/max-属性设置
		* 内容可能溢出容器
		* 边距大小与padding,和是否定义box-sizing:border-box有关，计算需要根据不同情况 
*  方案三：div绝对定位水平垂直居中（Transforms变形）

		/*
		 * 这是最简单的方法，不仅能实现绝对居中同样的效果，也支持联合可变高度方式使用
		 * 内容块定义transform：transtate(-50%,-50%)
		 * 必须加上top:50%,left:50%
		 */
		
		.div{
			width:200px;
			height:200px;
			position:absolute;
			text-align:center;
			left：50%；
			right:50%;
			transform:translate(-50%,-50%);
			/*-webkit-transform: translate(-50%,-50%);*/
		    /*-ms-transform: translate(-50%,-50%);*/
		} 
	* 优点：
		* 内容可变高度
		* 代码量少
	* 缺点：
		* IE8不支持
		* 属性需要些浏览器厂商前缀
		* 可能干扰其他transform效果
		* 某些情形下会出现文本或元素边界渲染模糊的现象

* 若只是水平居中(可以使用margin:0 auto)
		
		.div{
			width:100px;
			height:100px;
			text-algin:center;
			margin:0 auto;
		}
		
>6.display有哪些值？说明他们的作用。

作答：

* block:块类型。默认宽度为父元素宽度，可设置宽高，换行显示。
* none：缺省值。像行内元素类型一样显示。
* inline：行内元素类型。默认宽度为内容宽度，不可设置宽高，同行显示。
* inline-block：默认宽度为内容宽度，可以设置宽高，同行显示。
* list-item:像块类型元素一样显示，并添加样式列表标记。
* table:此元素会作为块级表格来显示。
* inherit:规定应从父元素继承display属性的值。

>7.position的值relative和absolute定位的原点是？

作答：

* absolute：生成绝对定位的元素，相对于值不为static的第一个父元素进行定位。
* fixed：生成绝对定位的元素，相对于浏览器窗口进行定位。
* relative:生成相对定位的元素，相对于其正常位置进行定位。
* static:默认值。没有定位，元素出现在正常的流中。（忽略top、bottom、left、right、z-index声明）
* inherit:规定从父元素继承position属性的值。

>8.CSS3有哪些新特性？

作答：

* 圆角：border-radius
* 多列布局：multi-column layout
* 阴影和反射：shadow/reflect
* 文字特效：text-shadow
* 文字渲染：text-decoration
* 线性渐变：gradient
* 旋转：transform
* 缩放、定位、倾斜、动画、多背景：transform、scale、translate、sken、animation

>9.请解释一下CSS3的Flexbox（弹性盒布局模型），以及适用场景？

作答：

* 一个用于页面布局的全新CSS3功能，Flexbox可以把列表放在同一个方向（从上到下排列，从左到右），并让列表能延伸到占用可用的空间。较为复杂的布局还可以通过一个伸缩容器（flexcontainer）来实现。采用Flex布局的元素，称为Flex容器（flexcontainer），简称“容器”。它的所有子元素自动成为容器成员，称为Flex项目（flex item），简称“项目”。
* 常规布局时基于块和内联流方向，而Flex布局是基于flex-flow流可以很方便的用来做居中，能对不同平布大小自适应，在布局上有了比以前更加灵活的空间。

>10.用纯CSS创建一个三角形的原理是什么？

作答：

* 把上、左、右三条边隐藏掉（颜色设为transparent）

		#demo{
			width:0;
			height:0;
			border-width:20px;
			border-style:solid;
			border-color:transparent transparent red transparent;
		}

>11.一个满屏品字布局如何设计？

作答：

* 简单的方式：
	* 上面的div宽为100%；
	* 下面的两个div分别宽50%；
	* 然后用float或者inline使其不换行即可。

>12.常见兼容性问题？

作答：

* png24位的图片在IE6浏览器出现背景，解决方案是做成png8
* 浏览器默认的margin和padding不同，解决方案是加一个全局的*{margin:0;padding:0}来统一
* Chrome中文界面下默认会将小于12px的文本强制按照12px显示，可以通过加入CSS属性-webkit-text-size-adjust:none；解决
* 超链接访问过火hover样式就不出现了，被点击访问过的超链接样式不再具有hover和active，解决方法是改变CSS属性的排列顺序："L-V-H-A"-> a:link{} a:visited{} a:hover{} a:active{}

>13.li与li之间有看不见的空白间隔是什么原因引起的？有什么解决方法？

作答：

>14.经常遇到的浏览器的兼容性有哪些？原因，解决方法是什么，常用hack的技巧？

作答：

>15.为什么要初始化CSS样式。

作答：

>16.absolute的containing block 计算方式跟正常流有什么不同？

作答：

>17.CSS里的visibility属性有个collapse属性值是干嘛用的？在不同浏览器下有什么区别？

作答：

>18.position跟display、margin collapse、overflow、float这些特性相互叠加后会怎么样？

作答：

>19.对BFC规范（块级格式化上下文：block formatting context）的理解？

作答：

>20.CSS权重优先级是如何计算的？

作答：

>21.请解释一下为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式。

作答：

>22.移动端的布局用过媒体查询吗？

作答：

>23.使用CSS预处理器吗？喜欢那个？

作答：

>24.CSS优化、提高性能的方法有哪些？

作答：

>25.浏览器是怎样解析CSS选择器的？

作答：

>26.在网页中应该使用奇数还是偶数的字体大小？为什么呢？

作答：

>27.margin和padding分别适合什么场景使用？

作答：

>28.抽离样式模块怎么写，说出思路，有无实践经验？

作答：

>29.元素竖向百分比设定是相对于容器的高度吗？

作答：

>30.全屏滚动的原理是什么？用到了CSS的那些属性？

作答：

>31.什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？

作答：

>32.视差滚动效果，如何给每页做不同的动画？（回到顶部，向下滑动要再次出现，和只出现一次分别怎么做？）

作答：

>33.::before和:after中双冒号和单冒号有什么区别？解释一下这2个伪元素的作用。

作答：

>34.如何修改chrome记住密码后自动填充表单的黄色背景？

作答：

>35.你对line-height是如何理解的？

作答：

>36.设置元素浮动后，该元素的display的值是多少？（自动变成display:block）

作答：

>37.怎么让Chrome支持小于12px的文字？

作答：

>38.让页面里的字体变清晰，变细用CSS怎么做？（-webkit-font-smoothing:antialiased;）

作答： 

>39.font-style属性可以让它赋值为“oblique”,oblique是什么意思？

作答：

>40.position:fixed；在android下无效怎么处理？

作答：

>41.如果需要手动写动画，你认为最小时间间隔是多久，为什么？

作答：

>42.display:inline-block什么时候回显示间隙？

作答：

>43.overflow:scroll时不能平滑滚动的问题怎么处理？

作答：

>44.有一个高度自适应的div,里面有两个div,一个高度100px,希望另一个填满剩下的高度。

作答：

>45.png、jpg、gif这些图片格式解释一下，分别什么时候用。有没有了解过webp？

作答：

>46.什么事Cookie隔离？（或者说：请求资源的时候不要让它带cookie怎么做）

作答：

>47.style标签卸载body后和body前有什么区别？

作答：
