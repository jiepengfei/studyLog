Month3

### Tips：

##### 1.一般脚本挂载在父物体身上，animator挂载在子物体身上；

获取：GetComponentInChildren<Animator>

##### 2.调用其他脚本：

GetComponent<挂载的脚本文件名字>()

##### 3.[System.Serializable]

在文件首声明，[System.Serializable]，使其可以序列化

例：

```C#
[System.Serializable] // 使其可以序列化,将当前对象“嵌入”到脚本后，可以在编译器中显示属性。
继承monoBehaviour的是脚本，没继承的是普通C#类，无法挂载在物体上，无法通过GetComponent<脚本名>找到。这时候可以将普通C#类挂载在脚本上
public class Xxx
{
	public string run = 'run';
}

public class PlayerStatus : MonoBehaviour
{
	pubilc Xxx param;
	private void OnMoveStart()
    {
        GetComponent<挂载的文件>().chParams.run;
    }
}

```

##### 4.在移动开始的时候开启动画，在移动结束的时候关闭动画

##### 5.多个参数封装为一个类

如果一个方法需要的参数过多（超过三个），建议把参数封装在一个类中，参数传递一个对象就可以。

##### 6.Tooltip

```C#
public class Xxx
{
    [Tooltip("中文提示")] // unity中编辑器对一个变量的中文提示
	public string run = 'run';
}
```

##### 7.namespace

 域名.项目名.类名，避免类重名

##### 8.RequireComponent

```C#
public class Xxx : MonoBehaviour
// 下面这句话的功能：如果添加了这个脚本，那么被Require的脚本会自动被添加到物体上
[RequireComponent(typeof(脚本名),typeof(脚本名))] // 脚本依赖
{
}
```

##### 9.模拟人物重力

```C#
public void Movement(Vector3 direction)
{
    LookAtTarget(direction);
    Vector3 forward = transform.forward;
    forward.y = -1; // 相当于重力
    // 向前移动
    controller.Move(forward * Time.deltaTime * moveSpeed);
}
```

##### 10.类图

右键---添加---新建项---类图                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               

##### 11.开闭原则

是多态的一种

对扩展开放，对修改关闭

例：普通

```C#
public void GoHome(string type)
{
	switch type:
    	case 'train':
    	...
        case 'bus':
    	...
}
如果需要新增交通方式就需要增加case，不符合开闭原则；
```

依赖倒置：依赖父级（运输方式），不要依赖子级（火车，汽车）

方法：使用抽象类，参数声明父，传参为子级。

```C#
public void GoHome(Transportation type)
{
    type.Transport(); // 调用子类方法
}
// 后续增加新的子类就行
public abstract class Transportation
{
    public abstract void Transport();
}
public class Train : Transportation
{
    public override void Transport()
    {
        ...
    }
}
```

##### 12.类内存分布

栈中存放对象地址，指向堆空间中，成员内存地址都在堆中。同时还有类型对象指针以及同步块索引。

##### 13.虚方法

c#中，加上virtual关键字声明的方法即为虚方法。

```C#
访问修饰符 virtual 返回类型 函数名(参数)
```

虚方法可以被子类重写，如果子类重写了此虚方法，那么被调用时会运行子类方法，否则就是调用父类方法，在子类中也可以调用父方法。这样的话我们就可以通过子类重写来实现不同的功能。

1.因为虚方法需要被子类调用，所以访问修饰符不能为private
2.父类虚方法使用的什么访问修饰符，子类重写就必须用什么访问修饰符

tips11中抽象方法也可以使用虚方法代替，同时类可以是普通类。

区别：

抽象类方法在类中不能实现，推迟给子类实现。

虚方法在类中可以实现，对于子类可选实现。

##### 14.对象初始化器

创建对象时，有选择的为属性赋值。

```C#
Xxx abc = new Xxx()
{
	aaa = new Aaa();
}
```

##### 15.所有的组件脚本（继承MonoBehavior）不能new对象

需要使用GameObject.AddComponent<>添加；

##### 16.方法重写原理

类中的方法，会在内存中注册一个方法表，存放方法名称与方法地址。

方法重写会先在子类方法表中添加新记录，然后修改父级方法表地址。

##### 17.方法隐藏

如果子类和父类同时拥有同名的方法，调用子类方法会只执行子类方法。

作用：解决脚本生命周期冲突

原理：在子类方法表中添加新纪录

解决方法：

```C#
private new void Start()
{
	base.Start();
	...
}
```

##### 18.接口命名以I开头

##### 19.接口的显式实现

作用：

1.解决多接口实现时的二义性（多接口的同名方法冲突）

2.解决接口中的成员对实现类不适用的问题（类所继承的接口中某方法不适用）

##### 20.类排序方式选择

内部∶调用IComparable 接口的CompareTo方法[常用/默认的排序依据]

Array.Sort(array);

内部:调用IComparer 接口的Compare 方法[其他不太常用的排序依据]

Array.Sort(array,new GrenadeComparer());

##### 21.委托

实际就是把函数作为参数传递

委托(delegate)是函数指针的升级版

变量（数据）是以某个地址为起点的一段内存中所存储的值

函数（算法）是以某个地址为起点的一段内存中所存储的一组机器语言指令

直接调用与间接调用

直接调用∶通过函数名来调用函数，CPU通过函数名直接获得函数所在地址并开始执行→返回

间接调用:通过函数指针来调用函数，CPU通过读取函数指针存储的值获得函数所在地址并开始执行→返回

委托的使用方式：

Action委托

Func委托

·正确使用1:

**模板方法**，“借用"指定的外部方法来产生结果

​	·相当于"填空题”

​	.常位于代码中部

​	·委托有返回值

·正确使用2∶

**回调( callback )方法**，调用指定的外部方法

​	·相当于"流水线”

​	.常位于代码末尾

​	·委托无返回值

###### 多播(multicast)委托

委托之间可以使用+号运算符相加。

```
action1 += action2;
action1 += action3;
action1.Invoke[]; // action1,2,3委托都会执行
```

##### 22.foreach原理

1.获取迭代器

IEnumerator iterator = hand.GetEnumerator();

2.移动到下一个元素

while (iterator.MoveNext())

{

​	// 3.获取元素

​	Console.WriteLine(iterator.Current);

}

##### 23.yield常用return

```C#
yield return null // 等待一个渲染帧

yield return new WaitForSeconds(1); // 等待一秒
```

yield以前的代码会被分配到MoveNext方法中

return后面的数据分配到Current属性中

##### 24.AnimationCurve

提供数据可视化的操作面板。如先快后慢曲线等

##### 25.Color.Lerp

将数值的变化转化为颜色的变化

Vector3.Lerp

Quaternion.Leap

同理

##### 26.两点之间的距离

Vector3.Distance(firstPosition, targetPosition) > 0.1f

##### 27.默认返回值

return default();

在程序未完成时想要调试，把返回值的报错补充。

##### 28.类型转换

Convert.ChangeType(变量, 要转化成的类型);

##### 29.画布字体大小问题

世界坐标模式下，一像素等于一米。

这时候修改画布缩放为0.01

##### 30.Hierarchy面板搜索

可以以挂载的脚本类型搜索（如Collider）

前面选择type

##### 31.2D 3DUI

这两个属于2D UI，固定在屏幕中

Screen Space - Overlay

Screen Space - Camera

这个属于3D UI，跟随世界坐标

World Space

##### 32.如果需要改变程序执行顺序，可以使用协程

##### 33.UGUI的本质

检测的是image以及text，而不是button等

2dUI不发射线，因为归属于同一个平面，只需要检测鼠标点击是否在矩形区域内

##### 34.alt+shift多行选中

##### 35.动画职责

策划：为动画片段添加事件，指向OnCancel，OnAttack

程序：在脚本中播放动画，动画中需要执行的逻辑，注册attackhandler事件

##### 36.[MenuItem("")]

菜单项，被它修饰的方法会在unity编辑器中产生菜单按钮

##### 37.AssetDatabase

包含了只适用于编译器中操作资源的相关功能

##### 38.StreamingAssets

unity特殊目录之一，该目录中的文件不会被压缩，移动端可读，pc端可读写

##### 39.Path类

提供文件路径相关api

##### 40.静态构造函数

作用：初始化类的静态数据成员

实际：类被加载时执行一次，早于脚本生命周期

##### 41.不同环境加载url地址不同

```C#
#if UNITY_EDITOR || UNITY_STANDALONE
url = "file://" + Application.dataPath + "/StreamingAssets/" + fileName;

#elif UNITY_IPHONE
url = "file://" + Application.dataPath + "/Raw/" + fileName;

#elif UNITY_ANDROID
url = "jar:file://" + Application.dataPath + "!/assets/" + fileName;
```

##### 42.using代码块其他使用方式

```C#
using (StringReader reader = new StringReader(fileContent))
{
    string line = reader.ReadLine();
    string[] keyValue = line.Split('=');
}// 当程序退出using代码块，将自动调用reader.Dispose()方法
```

##### 43.单例模式使用方法

单例类.Instance.方法

##### 44.计算夹角

Vector3.Angle(当前变换组件.forward, 目标变换组件位置)

##### 45.开启协程

协程需要继承monobehavior才能开启，或者使用继承了脚本的游戏对象.StartCoroutine开启协程。

##### 46.人物信息

获取挂载在游戏对象上的脚本实例

skillManager = GetComponent<CharacterSkillManager>();

##### 47.开启/停止Update调用

this.enable = bool

设置当前脚本激活状态（只会影响当前脚本部分声明周期如update等，不影响脚本方法被调用

##### 48.选中一个目标后选取另一个目标将前一个目标取消选中

核心思想：存储上次选中的物体

取消上次选中的物体

存储的物体改为当前选中的物体

选中当前物体

##### 49.使用缓存减少反射的性能消耗

```C#
private static T CreateObject<T>(string className) where T : class
{
    if (!cache.ContainsKey(className))
    {
        Type type = Type.GetType(className);
        object instance = Activator.Createlnstance(type);
        cache.Add(className, instance);
    }
    return cache[classname] as T;
}
```

##### 50.[SerializeField]

将私有字段在编译器中显示，方便调试，之后可以删除

##### 51.声音组件

Audio Source

几个重要属性

Play On Awake(一般取消勾选，不然会在游戏开始时出声)

声音衰减曲线，一般设置线性衰减，选择最小开始衰减距离以及最远声音距离

##### 52.[HideInInspector]

在面板中隐藏该public字段，使用代码进行调用

##### 53.调试技巧

1.如果有Update中的代码需要调试。直接打断点会直接卡死，此时需要点击unity的中间暂停按钮。然后点击右侧的下一步，逐帧调试

2.增加一个调试用的public成员变量，这样程序运行过程中就能知道改变量的值有没有改变

```C#
public FSMStateID test_urrentState;
public void Update()
{
	test_CurrentStateID = currentState.StateID;
}
```

##### 54.运动轨迹拖尾组件

Trail Renderer

##### 55.利用命名写活代码

```C#
例：
//自定义特效命名规则:
//Effects ÷物体标签
if (args.Hit.collider == null) return;
string prefabName ="Effects" + args.Hit.collider.tag;
Gameobject prefab = ResourceManager.Load<Gameobject>(prefabName);
if (prefab ==null) return;
GameobjectPool.Instance.CréateObject(prefabName, prefab, args.Hit);
```

##### 56.时间参数类

命名后缀：EventArgs

##### 57.辅线程访问Unity组件属性

创建委托对象，交给委托完成，在主线程Update中循环清空Action队列。

#### UI结构

UI

----MainWindowCanvas

--------Text

```
根物体（UI）挂载UIManager脚本
窗口挂载XXXWindow继承UIWindow
交互元素挂载UIEventListener
```



#### UI框架

##### 核心类

###### UIWindow

```
所有UI窗口的基类
可以代表所有窗口（概念继承，以层次化方式管理类）
定义所有窗口共有行为（显隐等）

控制显隐
添加Canvas Group组件，设置它的Alpha通道值
```

###### UIManager

```
管理（记录、禁用、查找）窗口
设计为单例模式
```

###### UIEventListener

```
因为button只提供click事件检测，这个类继承IPointDownHandler等接口实现
通过委托调用后续传入的方法
管理所有UGUI事件，提供事件参数类。
附加到需要交互的U元素上，用于监听用户的操作。
类似于EventTrigger
```



##### 辅助类

###### UIMainWindow

```
附加到主窗口中，负责处理主窗口逻辑
```

###### GameController

```
负责处理游戏流程，如游戏开始时的UI显示
```





#### 对象池

核心思想：通过空间换取时间（比如说技能，前后冷却技能释放之后创建出来的游戏对象都是同一个）

适用性：频繁创建/销毁游戏对象时

数据结构：Dictionary<string,List<GameObject>>

```C#
CreateObject(string key,GameObject prefab,Vector3 pos,Quaternion rotate)
{
	在池中查找是否存在禁用的物体
	{
		如果没有禁用物体,创建对象;
		加入池中
	}
	使用对象
	{
		设置位置/旋转
		启用物体
	}
}
CollectObject(GameObject go)
{
	禁用物体
	// 删除字典记录，这里主要是需要删除字典list中的gameobject（一些贴图，材质之类的资源，这个占内存空间大，归属UnityEngine.Object，key之类的归属System.Object
}
```

##### Tips

需要通过对象池创建的物体，如需每次创建时执行，则让物体脚本实现IResetable接口，接口中有一个reset方法。因为放在脚本awake中只会在第一次创建的时候执行一次
