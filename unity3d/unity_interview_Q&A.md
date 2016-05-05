#Unity3D面试题目 
######整理者：hauk0101
##Unity3D引擎相关部分
>1.让一个物体围绕某一点旋转，有几种方法？分别是什么？

作答：有三种方法。分别是：<br>
　　1)旋转函数transform.Rotate()来实现。<br>
　　2)transform的RotateAround(vector3 position,vector3 axis,float angle)函数。<br>
　　3)代码如下：

	private Transform obj1;
	private Transform obj2;
	private Quatrenion q;
	q.SetLookRotation(obj1.position,obj2.position);
	transform.rotation = q;

　　然后拖动obj1和obj2就可以看到物体永远保持z轴朝向obj1,并且以obj2的位置来保持y轴的倾斜度。

>2.Mesh,Sphere,Box,Capsule,四种碰撞器。请按照性能开销由小到大进行排序。

作答：性能开销有小到大顺序为：Sphere Collider(球状体碰撞器) < Capsule Collider(胶囊体碰撞器) < Box Collider(盒状体碰撞器) < Mesh Collider(网格体碰撞器)。

>3.向量的点积，叉积，在游戏中的应用（分别举一个例子说明）。

作答：<br>
　　1）判断目标在自己的前后方位可以使用点积，返回值为正时，目标在自己的前方，反之在自己的后方。
	
	Vector3.Dot(transform.forward,target.position);

　　2）判断目标在自己的左右方位可以使用叉积，返回值为正时，目标在自己的右方，反之在自己的左方。

	Vector3.Cross(transform.forward,target.position).y
	
　　3)a.normalized和b.normalized表示的是两个向量的单位向量，因为在公式里，有向量和模的除法，得出来的结果就是单位向量，所以我们这里和后面都直接用单位向量来计算，可以省去很多麻烦。<br>
　　4）Mathf.Rad2Deg表示的是单位弧度的度数。<br>
　　5）通过叉积计算度数是通过公式|c| = |a||b|sin<a,b>来逆向求值。|c|其实就是叉积的模，换句话说，也代表着Vector3.Distance(Vector3.zero,Vector3.Cross(a.normalized,b.normalized))的值。

>4.如何让粒子效果显示在UI前面？（NGUI或UGUI选其一回答）

作答：<br>
　　1）如果是NGUI，则修改例子的renderQueue,修改尽量大就在所有UI上面，如果希望在两个UI之间，则需要查看NGUI源码。[http://m.blog.csdn.net/blog/yxriyin/44037673](http://m.blog.csdn.net/blog/yxriyin/44037673)<br>
　　2）如果是UGUI，一种可以使用相机专门处理粒子，一种是设置sortingOrder。[http://www.xuanyusong.com/archives/3435](http://www.xuanyusong.com/archives/3435)

>5.当一个细小的高速物体撞向另一个较大的物体时，会出现什么情况？如何避免？

作答：会发生穿透，即碰撞检测失败。解决方法如下：<br>
　　1）增大细小物体的碰撞体。<br>
　　2）使用射线检测。<br>
　　3）可以physics time减小，不建议这样做。<br>
　　4）确保rigidbody不超过一定的速度，不建议这样做。<br>

>6.Update(),Awake(),Start()的执行顺序是？游戏开始后，分别在何时执行？

作答：执行顺序为Awake()->Start()->Update()。<br>
　　　脚本自带函数执行顺序如下：
	
	Awake -> OnEnable -> Start -> FixedUpdate -> Update -> LateUpdate -> OnGUI -> Reset -> OnDisable -> OnDestroy

　　　Awake函数：用于在游戏开始之前初始化变量或游戏状态。在脚本整个生命周期内它仅被调用一次。Awake在所有对象被初始化之后调用，所以你可以安全的与其它对象对话或用诸如GameObject.FindWithTag()这样的函数搜索它们。每个游戏物体上的Awake以随机的顺序被调用。因此，应该用Awake来设置脚本间的引用，并用Start来传递信息。Awake总是在Start之前被调用。它不能用来执行协同程序。<br>
　　　Start函数：尽在Update函数第一次被调用前调用。Start在behaviour的声明周期中只被调用一次。它和Awake的不同是Start指在脚本实例被启用时调用。可以按需调整延迟初始化代码。Awake总是在Start之前执行。这允许你协调初始化顺序。在所有脚本实例中，Start函数总是在Awake函数之后调用。<br>
　　　Update函数：正常帧更新，用于更新逻辑。每一帧都执行，处理Rigidbody时，需要用FixedUpdate，每固定帧绘制时执行一次，和Update不同的是FixedUpdate是渲染帧执行，如果你的渲染效率低下的时候FixedUpdate调用次数就会跟着下降。FixedUpdate比较适用于物理引擎的计算，因为是跟每帧渲染有关。Update就比较适合做控制。

>7.Unity动态加载资源有几种方法，分别是什么？

作答：有三种，分别如下：<br>
　　1）通过Resources模块，调用它的load函数：可以直接load并返回某个类型的Object,前提是要把这个资源放在Resource命名的文件夹下，Unity不管有没有场景引用，都会将其全部打包到安装包中。<br>
　　2）通过bundle的形式：即将资源达成asset bundle放在服务器或者本地磁盘，然后使用WWW模块get下来，然后从这个bundle中load某个object。<br>
　　3）通过AssetDatabase.loadasset：这种方式只在editor范围内有效，游戏运行时没有这个函数，它通常实在开发中调试用的。

>8.Unity中游戏暂停和开始怎么实现？

作答：游戏暂停和开始一般是通过Time.ScaleTime的数值控制的，1.0表示正常，0.0表示停帧，也就是暂停。

>9.Animator Controller中参数类型bool和trigger的区别是什么？分别在何种情况下使用？

作答：两者的区别是动作复原，set trigger设置动作后，它会自动复原，而bool是需要将其设置成false,需要手动操作。当你需要自动控制动画状态时使用trigger,例如适合角色设计动画等单次触发的情况；当你需要手动控制动画状态时使用bool,例如角色射击状态（举枪）和静止状态（放下枪）的切换。

>10.两个对象发生碰撞的必要条件是什么？

作答：主动碰撞双方要有一个Rigidbody存在，并且碰撞双方必须都要有碰撞体组件。如果碰撞双方只有一个刚体，那么有刚体的物体一定要处于运动状态才会发生碰撞事件。也可以说必须相应两者的回调函数OnEnterTrigger。

>11.Lightmapping是什么？为什么要使用？

作答：光照贴图。主要是针对静态物体的烘焙，即将其阴影烘焙到地面的贴图上，达到比较真实的效果，以此来代替游戏场景中的实时灯光效果，以此来降低渲染的消耗。

>12.Unity中，控制3D人物模型位移的方式有几种？Animator组件的Apply Root Motion的作用是？

作答：<br>
　　1）常用的位移方式有4种组件。<br>

	transform.translate()	//向某方向移动物体多少距离
	transform.Position()	//在世界空间坐标transform的位置
	RigidBody.Velocity		//刚体的速度向量
	RigidBody.AddForce		//添加一个力到刚体，作为结果刚体将开始移动
	RigidBody.MovePosition	//移动刚体到position
	NavMeshAgent组件的SetDestination函数，设置自动Path目标点
	CharacterController组件的Move函数，每次都绝对运动
	Vector3.MoveToward()	//当前的地点移向目标

　　2）如果勾选了Animator组件的Apply Root Motion选项，角色的Transform将不能通过脚本来直接赋值，而是用过动画的运动来改变，如果不勾选，则可以通过脚本来改变角色的Transform。

>13.Unity中如何实现序列帧动画？

作答：大概有以下几种思路:<br>
　　1）在NGUI中，将每一帧资源打包成atlas,然后将该图集上添加脚本UISpriteAnimation。<br>
　　2）使用Shader中的MainTex的Offset，可实现把一整张有规律顺序的2D图片进行单张显示，通过改变offset偏移量，实现顺序显示。<br>
　　3）使用Animator进行K序列帧动画。<br>
　　4）使用程序逻辑控制播放，即在固定时间内进行图片切换显示。

>14.对象包含Box Collider 2D组件，且作为trigger使用时，检测是否有对象进入的函数是？

作答：OnTriggerEnter2D()函数。
