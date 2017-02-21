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

* 水平居中

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

* 

>10.用纯CSS创建一个三角形的原理是什么？

作答：

>11.一个满屏品字布局如何设计？

作答：

>12.常见兼容性问题？

作答：

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
