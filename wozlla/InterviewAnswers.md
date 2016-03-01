# 前端题目
## Javascript技术题目 
> 1.请列举一些数组元素去重方法。

作答：

> 2.Javascript的作用域和作用域链是什么？

作答：<br>
　　作用域指的是变量的适用范围。Javascript中作用域主要分为全局作用域和局部作用域（函数作用域）两种。其中全局作用域中的对象可以在代码的任何地方访问，而局部作用域中所有的变量和函数只能在其内部使用。  
　　作用域链指的是函数拥有的一个内部属性[[Scope]]中包含的能够被创建的作用域中对象的集合。它决定了哪些数据能被函数访问。
	 

> 3.Javascript的变量声明提升是什么意思？

作答：

> 4.如何解决回调层次过深的问题？

作答：<br>
　　解决JS程序中回调层次过深（“回调地狱”）的方案有以下几种：<br>
　1）使用具名函数，并保持代码层级不要太深<br>

	function fun3(err,c)
	{
		// do something with a in function 3
	}
	function fun2(err,b)
	{
		// do something with b in function 2
		asyncFun3(fun3);	
	}
	function fun1(err,a)
	{
		// do something with a in function 1
		asyncFun2(fun2);
	}
	asyncFun1(fun1);

　2）使用Promise或者链式Promise<br>
　3）使用Async等辅助库，待解是需要引入额外的库，而且代码上也不够直观<br>
　4）使用Generator<br>
　5）使用CO<br>
	
　　说明：本题主要参考博客[http://www.alloyteam.com/2015/04/solve-callback-hell-with-generator/](http://www.alloyteam.com/2015/04/solve-callback-hell-with-generator/)

> 5.Ajax是指什么？jsonP是指什么？两者的原理分别是？

作答：

## Canvas技术题目

>1.请列举十个以上常用的canvas2d的接口。

作答：<br>
　　1）createLinerGradient()：创建线性渐变（用在画布内容上）。<br>
　　2）createPattern()：在指定的方向上重复指定的元素。<br>
　　3）createRadialGradient()：创建放射状/环形的渐变（用在画布内容上）<br>
　　4）addColorStop()：规定渐变对象中的颜色和停止位置。<br>
　　5）scale()：缩放当前绘图至更大或更小。<br>
　　6）rotate()：旋转当前绘图。<br>
　　7）translate()：重新映射画布上的（0，0）位置。<br>
　　8）transform()：替换绘图的当前转换矩阵。<br>
　　9）setTransform()：将当前转换重置为单位矩阵。然后运行transform()。<br>
　　10）fillText()：在画布上绘制“被填充的”文本。<br>
　　11）strokeText()：在画布上绘制文本（无填充）。<br>
　　12）measureText()：返回包含指定文本宽度的对象。<br>
　　13）drawImage()：向画布上绘制图像、画布或视频。<br>
　　14）createImageData()：创建新的、空白的 ImageData 对象。<br>
　　15）getImageData()：	返回 ImageData 对象，该对象为画布上指定的矩形复制像素数据。<br>
　　16）putImageData()：把图像数据（从指定的 ImageData 对象）放回画布上。<br>
　　17）save()：保存当前环境的状态。<br>
　　18）restore()：返回之前保存过的路径状态和属性。<br>
　　19）createEvent()：创建自定义事件。<br>
　　20）getContext()：返回一个对象,指出访问绘图功能必要的API。<br>
　　17）toDataURL()：返回canvas图像的URL。<br>


>2.在canvas下如何优化文字的渲染速度？

作答：

>3.写下几种composite operation。

作答：<br>
　　canvas中的图形组合模式的属性globalCompositeOperation有12种类型：<br>
　　1）source-over(default)：默认设置，新图形会覆盖在原有内容之上。<br>
　　2）destination-over：会在原有内容之下绘制新图形。<br>
　　3）source-in：新图形会仅仅出现在与原有内容重叠的部分。其它区域都变成透明的。<br>
　　4）destination-in：原有内容中与新图形重叠的部分会被保留，其它区域都变成透明的。<br>
　　5）source-out：结果是只有新图形中与原有内容不重叠的部分会被绘制出来。<br>
　　6）destination-out：原有内容中与新图形不重叠的部分会被保留。<br>
　　7）source-atop：新图形中与原有内容重叠的部分会被绘制，并覆盖于原有内容之上。<br>
　　8）destination-atop：原有内容中与新内容重叠的部分会被保留，并会在原有内容之下绘制新图形<br>
　　9）lighter：两图形中重叠部分作加色处理。<br>
　　10）darker：两图形中重叠的部分作减色处理。<br>
　　11）xor：重叠的部分会变成透明。<br>
　　12）copy：只有新图形会被保留，其它都被清除掉。<br>	

>4.transform和setTransform接口的区别。

作答：<br>
　　画布上的每个对象都拥有一个当前的变换矩阵。其中transform()方法替换当前的变换矩阵，即允许缩放、旋转、移动并倾斜当前的环境。而setTransform()方法会先重置当前变换矩阵为单位矩阵，之后再替换为当前的需要设置的变化矩阵。

>5.请列举几个比较出名的js游戏框架。

作答：<br>
　　cocos2d-js，createjs,lufylegend,Babylon.js,Three.js, Turbulenz,Famo.us,PlayCanvas.js。<br>
　　Unity3D引擎可用js语言开发，Egret白鹭引擎是国内比较出名的Html5游戏引擎，用TypeScript语言开发。

## WebGL技术题
>1.如何兼容性地获取WebGL context?

作答：

>2.列出10个常用的WebGL接口。

作答：

>3.WebGL如何绘制图片？

作答：

>4.WebGL如何绘制文本？

作答：

>5.WebGL的pipeline是怎么样的？

作答：

>6.着色器是什么？

作答：

>7.绘制图片时Shader里必然会用到什么内置变量？

作答：

>8.drawArray和drawElements的区别？

作答：

>9.有哪些优化WebGL性能的手段？

作答：
