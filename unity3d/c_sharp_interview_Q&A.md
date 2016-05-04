#Unity3D面试题目 
######整理者：hauk0101
##C#语言相关部分
>1.请复制下列代码，并在编辑器中测试：


	void Start()
	{
		float a = 600.0f;
		float b = 1.0f - 80.0f / 100.0f;
		float c = a * b;
		int d = (int)c;
		Debug.Log(a);
		Debug.Log(b);
		Debug.Log(c);
		Debug.Log(d);
	}
> 变量"d"的输出结果为多少？为什么？如何解决？

作答：d的输出是119。该方式对于浮点数会做无条件舍去，失去精确度。如果希望获取float的整数部分，可以 d = Math.Floor(c)。

	Math.Round()    //四舍六入五取偶
	Math.Ceiling()  //只要有小数都加1
	Math.Floor()	//总是舍去小数

>2.数列1，1，2，3，5，8，13...第n位数是多少？用C#递归算法实现。

作答：

	private int getResult(int n)
	{
		if(n <= 0)	return 0;						//此处可根据实际情况进行容错判断，否则会出现死循环
		if(n == 1 || n == 2)	return 1;
		return getResult(n-1) + getResult(n-2);		//需要注意，当n>46时，可能会出现内存溢出问题			
	}
