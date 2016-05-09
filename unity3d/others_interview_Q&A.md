#Unity3D面试题目 
######整理者：hauk0101
##其它游戏相关问题
>1.当游戏中需要频繁创建一个物体对象时，我们需要怎么做来节省内存？

作答：<br>
　　可以使用pool对象池。（可以用PoolManager插件）<br>
　　使用AssetBundle也可以降低一定内存。

>2.如何实现磁铁效果？比如跑酷游戏中，获得磁铁道具后，自动吸附附近金币的效果。

作答：两种方法，逻辑判断和物理碰撞检测。<br>
　　　逻辑判断：当角色触发磁铁状态后，在角色的一定范围内，判断是否有金币，如果有则将范围内的金币朝向角色运动。<br>
　　　物理碰撞检测：在角色身上添加一定大小的碰撞器，只有当角色处于磁铁状态后，该碰撞器发生作用，同时检测只有当碰撞器与金币发生碰撞器才触发吸附金币效果。

>3.FPS游戏中,哪些东西适合使用对象池技术？

作答：子弹可以使用对象池，特效也可以使用对象池。敌人NPC和玩家NPC都可以使用对象池技术。

>4.在塔防游戏中，如何让塔指向进入攻击范围的敌人并射击？请简述程序流程。

作答：首先根据与敌人的距离进行判定，到达一定距离的时候，让塔旋转到敌人的方向，并进行射击。

>5.什么是单例？举一个游戏中使用单例的例子。

作答：单例模式确保某一个类只有一个实例，并且自行实例化并向整个系统提供这个实例，这个类成为单例类。<br>
　　　在Unity中，单例分为单例脚本和单例类。单例类的实现代码如下：
	 
	public class Singleton
	{
		private static Singleton instance;
		public static Singleton Instance
		{
			get
			{
				if(instance == null)
					instance = new Singleton();
				return instance;
			}
		}
	}

　　单例脚本的实现代码如下：
	
	public class Singleton:MonoBehaviour
	{
		private static Singleton instance;
		public static Singleton Instance
		{
			get
			{
				return instance;
			}
		}
		
		void Awake()
		{
			instance = this;
		}
	}

　　两者的区别在于单例自身实例化的时机。

>6.塔防游戏中（如《保卫萝卜》），地图的路径信息如何储存？让怪物沿着路径行走的方法是？

作答：博客园的[这篇文章](http://www.cnblogs.com/hll2008/p/4235714.html)
写的还是非常详细的，项目虽然是cocos2d - x3.x,但是思路都是一样。路径点信息如何储存，一张图一个ID,然后把路径点信息保存到xml文件里，根据ID去xml取路径点信息即可。让怪物沿着路径行走，坐标点与坐标点之间作差，再给其一个速度，同时用距离判断是否开始计算移动到下个点。至于向量计算，我给个[网址](http://blog.gamerisker.com/archives/347.html)分享给大家，这里描述的相当详细。

>7.《英雄联盟》中，带位移的技能能否穿越墙壁如何来判定？如闪现穿墙、撞墙？（以程序角度）

作答：通过地图信息和英雄位置信息，这两点可以计算出英雄离墙的距离。
进而通过距离（Unity的c#封装的代码Vecter3.Distance（英雄位置，墙体位置），服务端的选择的语言以及封装的代码那就有各式各样了）、当前鼠标位置（屏幕坐标到世界坐标的转换）、墙体薄厚（tag标识）,这三条来判断是可以穿墙还是撞墙。

>8.继承和接口的用法和区别？

作答：类的继承：B继承了A之后，可以直接调用A里的公共属性或者方法，还可以重写A(父类)里的虚函数等。<br>
　　　接口定义了一份规范，实现了接口的类或结构就意味着遵守接口定义的规范，接口只允许包含方法、属性、索引器和时间的签名，只允许包含签名；不允许包含实现几口，不包含常量、字段、运算符、实例构造函数、西构造函数、以及任何静态成员。<br>
　　　需要注意的是在C#中只能继承一个类，但可以继承多个接口。

>9.如何控制子弹发射频率，技能冷却时间等（需示例代码）。

作答：子弹发射频率和技能冷却本质上一样，这里给出技能冷却代码：
使用UGUI的技能冷却:

	public class SkillItem : MonoBehaviour
	{
	    public float coldTime = 2;        //设定冷却时间
	    public Image filledImage;              //效果演示图片，需要设置Image Type为Filled ;
	    private float timer = 0;                //间隔时间计算
	     
	    private bool isStartTimer = false;//标志.是否开始计时
	        // Use this for initialization
	        void Start ()
	        {
	            filledImage = transform.Find("FilledImage").GetComponent<Image>();//找到对应图片组件
	        }
	         
	        // Update is called once per frame
	        void Update () {
	            //进行冷却时间计时
	            if (isStartTimer)
	            {
	                timer += Time.deltaTime;//计时
	                filledImage.fillAmount = (coldTime - timer)/coldTime;//遮罩图片冷却动画
	                if (timer >= coldTime)//计时完毕,可以进行下一次释放
	                {
	                    filledImage.fillAmount = 0;
	                    timer = 0;
	                    isStartTimer = false;
	                }
	            }
	        }
	    //回调函数，点击技能按钮时触发
	    public void OnClick()
	    {
	        isStartTimer = true;//更改标志位，进行冷却时间计时
	    }
	}

>10.根据你的经验，说说unity项目使用SVN进行版本控制时的一些注意事项？

作答：需要版本管理的目录<br>
新建一个Unity Project之后，发现产生了很多目录和文件，其中只有两个是需要版本管理的：Assets、ProjectSettings。其他的都是自动生成的：<br>
　　　*.csproj，*.sln这些IDE的工程文件是自动生成的；<br>
　　　Library，主要存的是一个本地的Cache文件，不要加到版本管理中；<br>
　　　Tem，这个是Build过程中产生的文件；<br>
　　　提交的时候仅提交Assets 和 ProjectSettings 两个目录下所有东西，忽略掉其他所有目录和文件提交的时候.metafile也要提交


　　　Unity Project Settings<br>
　　　为了配合SVN，需要对Unity工程做一些设置：<br>
　　　菜单：Edit->Project Settings->Editor：Version Control 选择为[Visible Meta Files]；<br>
　　　菜单：Editor-> Project Settings->Editor：Asset Serialization Mode选择为：[Force Text]<br>
　　　菜单：Edit->Preferences -> Packages：Repository选择为[External]；

>11.分享下你学习Unity的经验/学习路线。有没有什么推荐的教程和书籍？

作答：看书、看博客、Google、做项目。

>12.说说你了解的优化内存的方法。

作答：<br>
　　1）对象池。<br>
　　2）内存释放。[参考文章](http://blog.csdn.net/wuming0108/article/details/26471635)<br>
　　3)Unity3D内部内存、Mono托管内存优化。[参考文章](http://www.cnblogs.com/murongxiaopifu/p/4284988.html)<br>
　　

>13.
