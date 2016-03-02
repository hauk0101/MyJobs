# 前端题目
###### 应答者 hauk0101
###### 日期 2016.02.26-2016.03.02  
## Javascript技术题目 
> 1.请列举一些数组元素去重方法。

作答：<br>
　　1）遍历数组法，新建数组，遍历传入数组，值不在新数组就加入该新数组中。

	//最简单的数组去重法
	function unique1(array)
	{
	    var r = new Array();
	    var isRepeat = false;
	    for(var i = 0;i < array.length;i++)
	    {
	        isRepeat = false;
	        for(var j =0;j < r.length;j++)
	        {
	            if (r[j] === array[i]) {
	               isRepeat = true;
	                break;
	            }
	        }
	        if(!isRepeat)
	        {
	            r.push(array[i]);
	        }
	    }
	    return r;
	}

　　2）对象键值对法，新建1个js对象和1个数组，遍历传入数组时，判断值是否为js对象的键，不是的话给对象新增该键并放入新数组。

	//速度最快，占空间最多
	function unique2(array)
	{
	    var res=[];
	    var json={};
	    var val,type;
	    for(var i = 0; i < array.length;i++)
	    {
	        val = array[i];
	        type =typeof val;
	        if(!json[array[i]])
	        {
	            res.push(array[i]);
	            json[array[i]] = 1;
	        }
	    }
	    return res;
	}


　　3）数组下表判断法，如果当前数组的第i项在当前数组中第一次出现的位置不是i，那么表示第i项是重复的，忽略掉。否则存入结果数组。

	function unique3(array)
	{
		var n = [array[0]];
		for(var i = 1; i < array.length; i++)
		{
			if(array.indexOf(array[i]) ==i)
			{
				n.push(array[i]);
			}	
		}
		return n;
	}

　　4）排序后相邻去除法，给传入数组排序，排序后相同值相邻，然后遍历时新数组只加入不与前一值重复的值。
	
	function unique4(array)
	{
		array.sort();
		var re=[array[0]];
		for(var i = 1; i < array.length; i++)
		{
			if(array[i] !== re[re.length -1])
			{
				re.push(array[i]);
			}			
		}
		return re;
	}

　　5）优化遍历数组法，获取没重复的最右一值放入新数组。

	function unique5(array)
	{
		var r = [];
		for(var i = 0, l = array.length; i < l; i++)
		{
			for(var j = i + 1; j < l; j++)
			{
				if(array[i] === array[j])
				{
					j = ++i;
				}
			}
			r.push(array[i]);
		}
		return r;
	}

　　6）借助第三方类库，使用jQuery类库中unique()方法。（只适用于节点对象集合，不适用于字符串数组及数字数组）
	
	$.unique(array) //节点对象集合

> 2.Javascript的作用域和作用域链是什么？

作答：<br>
　　作用域指的是变量的适用范围。Javascript中作用域主要分为全局作用域和局部作用域（函数作用域）两种。其中全局作用域中的对象可以在代码的任何地方访问，而局部作用域中所有的变量和函数只能在其内部使用。  
　　作用域链指的是函数拥有的一个内部属性[[Scope]]中包含的能够被创建的作用域中对象的集合。它决定了哪些数据能被函数访问。
	 

> 3.Javascript的变量声明提升是什么意思？

作答：<br>
　　变量声明提升即把变量提升到函数的top的地方。其中变量提升只是提升了变量的声明，并不会把赋值也提升上来。<br>
　　还有函数提升，即把整个函数都提到前面去。由于js中函数有2种写法，一种是函数表达式，一种是函数声明方式，只有函数声明形式才能被提升。

	//函数声明方式，可提升
	function myTest1()
	{
		foo();
		function foo()
		{
			alert("我来自 foo")；
		}
	}
	myTest1();

	//函数表达式方式,不可提升
	function myTest2()
	{
		goo();
		var goo = function goo()
		{
			alert("我来自 goo");
		}
	}
	myTest2();
	
　　参考博客[http://www.cnblogs.com/betarabbit/archive/2012/01/28/2330446.html](http://www.cnblogs.com/betarabbit/archive/2012/01/28/2330446.html)

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

作答：<br>
　　Ajax全称是“Asynchronous JavaScript and XML”(异步JavaScript和XML)，它是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。它的原理是在用户和服务器之间加了一个中间层，使用户操作与服务器响应异步化。它的核心是XMLHttpRequest对象，它是Ajax实现的关键——发送异步请求、接收响应及执行回调。<br>
　　jsonP全称是“JSON with Padding”，它是一个非官方的协议，它允许在服务器端集成Script tags 返回至客户端，通过javascript callback的形式实现跨域访问。其原理是动态添加&lt;script>标签来调用服务器提供的js脚本。

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

作答：<br>
　　1）不是交互性文字，或动态文字绘制等需求，可直接使用位图来代替。<br>
　　2）创建一个不可见的缓冲Canvas,文字首先绘制在此Canvas上，当需要显示时，通过drawImage(canvas...)绘制到显示的Canvas上，这样可有效避免直接调用fillText带来的性能降低问题，优化文字的渲染速度。


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

作答：<br>
　　为了获取canvas的WebGL上下文，请求来自canvas的名为“webgl”的上下文。如果失败，尝试请求“experimental-webgl”（试验性的webgl）。如果同样失败，则显示1个警告来告诉用户，当前浏览器不只是WebGL。

	function initWebGL(canvas)
	{
		//创建全局变量
		window.gl = null;
		
		try
		{
			//尝试创建标准上下文，如果失败，回退到试验性上下文
			gl = canvas.getContext("webgl") || canvas.getContext("experimental-webgl");
		}
		catch(e){}
		
		//如果没有GL上下文，则弹出警告提示
		if(!gl)
		{
			alert("WebGL初始化失败，可能是因为您的浏览器不支持。");
		}
	}

>2.列出10个常用的WebGL接口。

作答：<br>
　　1）WebGLRenderingContext<br>
　　2）WebGLProgram<br>
　　3）WebGLActiveInfo<br>
　　4）WebGLRenderbuffer<br>
　　5）WebGLTexture<br>
　　6）WebGLBuffer<br>
　　7）WebGLShader<br>
　　8）WebGLContextEvent<br>
　　9）WebGLShaderPrecisionFormat<br>
　　10）WebGLFramebuffer<br>

>3.WebGL如何绘制图片？

作答：<br>
　　WebGL中绘制图片是通过纹理实现的。在HTML中使用的一般类型的图片变换成纹理之后，就可以在WebGL中使用了。意思就是说要把网页中使用的图片数据变成WebGL中可以使用的形式。大体步骤如下：<br>
　　1）获取图片对象。<br>
　　2）生成纹理。<br>
　　3）将纹理与WebGL绑定。<br>
　　4）分配图片数据。<br>
　　5）将纹理放到需要显示的多边形中。<br>
　　2）设置需要的着色器。<br>


>4.WebGL如何绘制文本？

作答：<br>
　　1）绘制带有文本的纹理。可以使用photoshop或其它绘画程序，来绘制带有文本的一些图像。然后构造一些平面几何并显示它。<br>
　　2）由于WebGL是基于OpenGL和JavaScript的技术结合，可以考虑使用OpenGL实现文本的方法。

>5.WebGL的pipeline是怎么样的？

作答：<br>
　　在WebGL中编程，通常的目标都是想要渲染某种场景。这其中包括多重并发的绘制工作，称之为绘制调用（draw call），这些调用都是在GPU端通过一个叫做渲染管线（Rendering Pipeline）的处理流程来实现的。渲染管线的具体流程如下：

![](https://raw.githubusercontent.com/hauk0101/myjobs/master/wozlla/res/Rendering_Pipeline.jpg)

>6.着色器是什么？

作答：<br>
　　着色器是一组提供计算机图形资源在执行渲染任务时使用的指令。它是运行在GPU上的为图形渲染管线的一个特定部分而允运行的程序，它是一种把输入转化为输出的程序，也是一种相当独立的程序，它们不能互相通信，只能通过输入和输出的方式来进行沟通。它是一种用GLSL的类C语言实现的，包含了针对向量和矩阵操作的有用特性。

>7.绘制图片时Shader里必然会用到什么内置变量？

作答：<br>
　　绘制图片时需要用到两个着色器，分别是顶点着色器和片段着色器。<br>
　　顶点着色器需要设置特定的全局变量gl\_Position来表示投影矩阵的坐标。<br>
　　片段着色器则需要gl\_FragColor来设置一些颜色。<br>
　　此外，还需要有多变变量varying，其作用是从顶点着色器往片段着色器中传递相关数值。
　　

>8.drawArray和drawElements的区别？

作答：<br>
　　drawArray传输或指定的数据是最终的真实数据，在绘制时效能更好。<br>
　　drawElements指定的是真实数据的调用索引，在内存/显存占用上更节省。<br>

>9.有哪些优化WebGL性能的手段？

作答：<br>
　　1）绘制与混合，多线程渲染。在多线程渲染模式下，因为绘制和混合分别处于不同的线程，绘制使用 CPU，混合使用 GPU，这样可以通过 CPU/GPU 之间的并发运行有效地提升浏览器整体的渲染性能。<br>
　　2）分块渲染。网页的缓存通常都不是一大块，而是划分成一格一格的小块，通常为256×256或者512×512大小，这种渲染方式称为分块渲染。通过一个统一缓存池来管理的方式，适合多线程 CPU/GPU 并发的渲染模型，所以基本上支持硬件加速的浏览器都会使用分块渲染的方式。<br>
　　3）图层混合加速。<br>
　　虽然一般网页元素都是使用 CPU 来绘制，但是对于加速的2D Canvas 和 WebGL 来说，它们的绘制是直接使用 GPU 的，所以它们一般会拥有一个 GL FBO（FrameBufferObject）作为自己的缓存，Canvas/WebGL 的内容被绘制到这个 FBO 上面，而这个 FBO 所关联的纹理再在混合操作里面被拷贝到窗口缓存上。简单的来说，对于加速的2D Canvas 和 WebGL，它们的绘制和混合都是使用 GPU。<br>
　　此题主要参考博客[http://tech.uc.cn/?p=2763#more-2763](http://tech.uc.cn/?p=2763#more-2763)


##说明

　　由于本人对于Html5前端开发处于转型学习阶段，所以很多题目的答案多有参考相关书籍或互联网。例如：《HTML5程序设计》(第二版)、《锋利的jQuery》(第二版)、《JavaScript高级程序设计》(第二版)、《Head Firest HTML 与 CSS》(第二版)等书籍，以及Google搜索引擎、维基百科等互联网途径。