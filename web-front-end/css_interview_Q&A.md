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

* 行框的排列会受到中间空白（回车\空格）等的影响，因为空格也属于字符，这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设置为0，就没有空格了。

>14.经常遇到的浏览器的兼容性有哪些？原因，解决方法是什么，常用hack的技巧？

作答： 答案同12

>15.为什么要初始化CSS样式。

作答：

* 因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化，往往会出现浏览器之间的页面显示差异。
* 当然，初始化样式会对SEO有一定影响，但鱼和熊掌不可得兼，但力求影响最小的情况下初始化。
* 最简单的初始化方法：*{padding:0；margin:0}(但是不建议使用这样的方法)

>16.absolute的containing block 计算方式跟正常流有什么不同？

作答：

无论属于哪种，都要先找到其祖先元素中最近的position值不为static的元素，然后再判断：

* 若此元素为inline元素，则containing block为能够包含这个元素生成的第一个和最后一个inline box的padding box(除margin,border外区域)的最小矩形；
* 否则，则由这个祖先元素的padding box构成。如果都找不到，则为initial containing block。

补充：

* static(默认的)/relative:简单说就是它的父元素的内容框（去掉padding的部分）
* absolute:向上找到最近的定位为absolute/relative的元素
* fixed:它的containing block一律为根元素（html/body），根元素也是initialcontaining block


>17.CSS里的visibility属性有个collapse属性值是干嘛用的？在不同浏览器下有什么区别？

作答：

* 对于普通元素visibility:collapse会将元素完全因此，不占据页面布局空间，与display:none变现相同。
* 如果目标元素为table,visibility:collapse将table隐藏，但是会占据页面布局空间，仅在Firefox下起作用，IE会显示元素，Chrome会将元素隐藏，但是占据空间。

>18.position跟display、margin collapse、overflow、float这些特性相互叠加后会怎么样？

作答：

* 如果元素的display为none,那么元素不被渲染，position,float不起作用
* 如果元素拥有position：absolute或者position:fixed属性，那么元素将为绝对定位，float不起作用
* 如果元素float属性不是none,元素会脱离文档流，根据float的属性值来显示
* 有浮动、绝对定位，inline-block属性的元素margin不会和垂直方向上的其他元素margin折叠

>19.对BFC规范（块级格式化上下文：block formatting context）的理解？

作答：

(W3C CSS2.1规范中的一个概念，它是一个独立容器，决定了元素如何对其内容进行定位，以及与其它元素的关系和相互作用)

* 一个页面是由很多个Box组成的，元素的类型和display属性，决定了这个Box的类型。
* 不同类型的Box,会参与不同的Formatting Context（决定如何渲染文档的容器），因此Box内的元素会以不同的方式渲染，也就是说BFC内部的元素和外部元素不会相互影响。

>20.CSS权重优先级是如何计算的？

作答：

* 权重的规则：标签的权重为1，class的权重为10，id的权重为100
* 以下例子是演示各种定义的权重值：
		/*权重为1*/
		div{
		}

		/*权重为10*/
		.class1{
		}
		
		/*权重为100*/
		#id1{
		}

		/*权重为100+1=101*/
		#id1 div{
		}

		/*权重为10+1=11*/
		.class1 div{
		}
		
		/*权重为10+10+1=21*/
		.class1 .class2 div{
		}
* 如果权重相同，则最后定义的样式会起作用，但是应该避免这种情况出现


>21.请解释一下为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式。

作答：

* 清除浮动是为了清除使用浮动元素产生的影响。浮动的元素，高度会塌陷，而高度塌陷使我们页面后面的布局不能正常显示。
* 清除浮动的方式：
	* 父级div定义height
	* 父级div也一起浮动
	* 常规的使用一个class
	
			.clearfix:before,.clearfix:after{
				content:" ";
				display:table;
			}
			.clearfix:after{
				clear:both;
			}
			.clearfix{
				*zoom:1;
			}
* SASS编译的时候，浮动元素的父级div定义伪类：after
	
		&:after,&:before{
			content:" ";
			visibility:hidden;
			display:block;
			height:0;
			clear:both;
		}
* 解析原理：
	* display:block使生成的元素以块级元素显示，占满剩余空间
	* height:0避免生成内容破坏原有布局的高度
	* visibility:hidden使生成的内容不可见，并允许可能被生成内容盖住的内容可以进行点击和交互；
	* 通过content:"."生成内容作为最后一个元素，至于content里面是点还是其他都可以，例如oocss里面就有经典的content:".",有些版本可能content里面内容为空，firefox直到7.0 content:""仍然会产生额外的空隙；
	* zoom:1触发IE hasLayout
	* 通过分析发现，除了clear:both用来闭合浮动，其他的代码无非都是为了隐藏掉content生成的内容，这也就是其他版本的闭合浮动为什么font-size:0;line-height:0;
>22.移动端的布局用过媒体查询吗？

作答：

* 假设你现在正用一台显示设备来阅读这篇文章，同时你也想把它投影到屏幕上，或者打印出来，而显示设备、屏幕投影和打印等这些媒介都有自己的特点，CSS就是为文档提供在不同媒介上展示的适配方法。
* 当媒介查询为真时，相关的样式表或样式规则会按照正常的级联规被应用。当媒体查询返回假，标签上带有媒体查询的样式表仍将被下载（只不过不会被应用）。
* 包含了一个媒体类型和至少一个使用宽度、高度和颜色等媒体属性来限制样式表范围的表达式。CSS3加入的媒体查询使得无需修改内容便可以使样式应用于某些特定的设备范围。
		
		//例如：
		@media(min-width:700px)and(orientation:landscape){
			.sidebar{display:none;}
		}

>23.使用CSS预处理器吗？喜欢那个？

作答：有SASS、LESS、Stylus、Turbine、Swithch CSS、CSS Cacheer、DT CSS等等。

>24.CSS优化、提高性能的方法有哪些？

作答：

* 关键选择器（Key selector），选择器的最后面的部分为关键选择器（即用来匹配目标元素的部分）；
* 如果规则拥有ID选择器作为其关键选择器，则不要为规则增加标签，过滤掉无关的规则（这样样式系统就不会浪费时间去匹配它们了）；
* 提取项目的通用公有样式，增强可复用性，按模块编写组件；
* 增强项目的协同开发性、可维护性和可拓展性；
* 使用预处理工具或构建工具（glup对css进行语法检查、自动补前缀、打包压缩、自动优雅降级）。

>25.浏览器是怎样解析CSS选择器的？

作答：

* 样式系统从关键选择器开始匹配，然后左移查找规则选择器的祖先元素。
* 只要选择器的子树一直在工作，样式系统就会持续左移，知道和规则匹配，或者使因为不匹配而放弃该规则。

>26.在网页中应该使用奇数还是偶数的字体大小？为什么呢？

作答：

* 在没有特殊要求的情况下，建议使用偶数字体。
* 有如下几种原因：
	* 偶数字号相对更容易和web设置的其他部分构成比例关系。
	* 在早期的浏览器版本对奇数字体支持会有问题，如IE6会把定义的13px字号的字渲染成14px
	* 使用奇数字号可能会使文本段落无法对齐

>27.margin和padding分别适合什么场景使用？

作答：

* margin是用来隔开元素与元素的间隔，padding是用来隔开元素与内容的间隔。
* margin用于布局分开元素，使元素与元素互不相干；
* padding用于元素与内容之间的间隔，让内容（文字）与（包裹）元素之间有一段空隙。

>28.抽离样式模块怎么写，说出思路，有无实践经验？

作答：暂时没有实践经验。

>29.元素竖向百分比设定是相对于容器的高度吗？

作答：

* 竖向百分比之height:是相对于容器高度的。
* 竖向辈分比之间距（margin-top、margin-bottom、padding-top、padding-bottom）是相对于容器的宽度而不是高度。

>30.全屏滚动的原理是什么？用到了CSS的那些属性？

作答：

* 计算当前浏览器屏幕高度，每次翻页显示的内容高度即为屏幕高度
* 对鼠标滚轮事件进行监听，注意滚轮事件的浏览器兼容问题

>31.什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？

作答：

* 响应式设计是指网页能自动识别屏幕宽度、并作出相应调整的网页设计。
* 基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。
* 可以借助js等其他hack手法。

>32.视差滚动效果，如何给每页做不同的动画？（回到顶部，向下滑动要再次出现，和只出现一次分别怎么做？）

作答：暂时没有相关的实践经验。

>33.::before和:after中双冒号和单冒号有什么区别？解释一下这2个伪元素的作用。

作答：

* 单冒号（：）用于CSS3伪类，双冒号（::）用于CSS3伪元素。（伪元素由双冒号和伪元素名称组成）
* 双冒号是在当前规范中引入的，用于区分伪类和伪元素。不过浏览器需要同时支持旧的已经存在的伪元素写法，而新的在CSS3中引入的伪元素则不允许再支持旧的单冒号写法
* 想让插入的内容出现在其它内容前，使用::before，否则使用::after；在代码顺序上，::after生成的内容也比::before生成的内容靠后。如果按堆栈视角，::after生成的内容会在::before生成的内容之上

>34.如何修改chrome记住密码后自动填充表单的黄色背景？

作答：

	input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill {
		background-color: rgb(250, 255, 189); /* #FAFFBD; */
		background-image: none;
		color: rgb(0, 0, 0);
	}

>35.你对line-height是如何理解的？

作答：

[点击此处打开链接](http://www.zhangxinxu.com/wordpress/?p=384)

>36.设置元素浮动后，该元素的display的值是多少？

作答：

自动变成display:block

>37.怎么让Chrome支持小于12px的文字？

作答：

* 用图片：如果是内容固定不变情况下，使用将小于12px文字内容切除做图片，这样不影响兼容，也不影响美观
* 使用12px以及12px以上字体大小：为了兼容各大主流浏览器，建议设计美工图时候设置大于或等于12px的字体大小，为了兼容、为了代码更简单 从新考虑权重下兼容性。
* 继续使用小于12px字体大小样式设置，如果不考虑chrome可以不考虑兼容，同时在设置小于12px对象设置-webkit-text-size-adjust:none，做到最大兼容考虑


>38.让页面里的字体变清晰，变细用CSS怎么做？

作答： 

-webkit-font-smoothing:antialiased;

>39.font-style属性可以让它赋值为“oblique”,oblique是什么意思？

作答：

倾斜的字体样式。

>40.position:fixed；在android下无效怎么处理？

作答：

* fixed的元素是相对整个页面固定位置的，你在屏幕上滑动只是在移动这个所谓的viewport，原来的网页还好好地在那，fixed的内容也没有变过位置，所以并不是IOS不支持fixed,只是fixed的元素不是相对手机屏幕固定的。

>41.如果需要手动写动画，你认为最小时间间隔是多久，为什么？

作答：

* 多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小时间间隔为1/60 * 1000 ms = 16.7ms

>42.display:inline-block什么时候会显示间隙？

作答：

* 移除空格、使用margin负值、使用font-size:0、letter-spacing、word-spacing

>43.overflow:scroll时不能平滑滚动的问题怎么处理？

作答：

* 可以添加-webkit-overflow-scrolling：touch

>44.有一个高度自适应的div,里面有两个div,一个高度100px,希望另一个填满剩下的高度。

作答：

[点击此处打开链接](https://segmentfault.com/q/1010000000762512/a-1020000000762933)

>45.png、jpg、gif这些图片格式解释一下，分别什么时候用。有没有了解过webp？

作答：

* png支持透明背景图像，无损压缩，体积比较大
* jpg不支持透明背景图像，体积比较小
* gif支持动画
* webp是谷歌开发的一种图片格式，可以减小图片体积，但在不同浏览器存在兼容问题。

>46.什么是Cookie隔离？（或者说：请求资源的时候不要让它带cookie怎么做）

作答：

* 如果静态文件都放在主域名下，那静态文件请求的时候都是带有cookie的数据提交给server的，非常浪费流量，所以可以隔离开
* 因为cookie有域的限制，因此不能跨域提交请求，故使用非主要域名的时候，请求头中就不会带有cookie数据，这样可以降低请求头的大小，降低请求时间，从而达到讲题整体请求延时的目的。
* 同时这种方式不会将cookie传入Web Server，也减少了Web Server对cookie的处理分析环节，提高了webserver的http请求解析速度。

>47.style标签写在body后和body前有什么区别？

作答：

加载的顺序不同，写在body之前，在页面加载body的元素时已经加载了CSS样式，可以避免布局混乱显示。
