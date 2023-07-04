

### 开发技巧

##### 1.一般以0点作为主场景位置起点，方便开发

##### 2.代码格式化快捷键ctrl + K +d



### Unity知识点

##### 1.hierarchy面板中的物体都存放在内存中

## Unity脚本

设置模板文件

F:\Unity 2021.2.11f1c1\Editor\Data\Resources\ScriptTemplates



### Tips

#### 开发技巧

```c#
private void OnGUI() // 开发自测按钮，点击按钮执行括号中的逻辑
{
    if (GUILayout.Button("按钮"))
    {
        ...
    }
}
```

```
Debug.DrawLine('起始位置', '终点位置');
画线
```

##### 控制台打印

Debug.log();

print();

##### 当脚本挂载到对象上时，自动添加依赖的组件或其他脚本到该对象上

[RequireComponent(typeof(AudioSource))]

##### 文件为杂项文件解决方案

右边解决方案资源管理器

C#资源

对应脚本

右键点击加入到项目中

（三维数学0314,10.00分钟）

##### 动画时间过短导致不播放

```c#
anim.CrossFade(animName);
改为
anim.PlayQueued(animName);
```

##### 物理射线

```C#
Physics.Raycast(起点坐标, 方向, 受击物体信息, 检测距离, 检测层)
// out: 相当于传递变量，在函数中赋值
// 检测层：用来区分环境与人物
Physics.Raycast(this.transform.position, this.transform.forward, out hit, 100, mask);
```

##### 通过代码读取资源

资源必须放到Resources目录下

```C#
GameObject prefabGO = Resources.Load<GameObject>('目录/资源名称')
```

获取单个精灵图：

Sprite sprite = Resources.Load<Sprite>('spriteName');

获取精灵图集：

Spritep[] spriteArray = Resources.LoadAll<Sprite>('spriteName');



##### 创建的新资源朝向问题

目标点位置朝法线方向移动少许距离（让新物体看起来清晰一些，不会和旧物体重叠）

新物体Z轴朝向法线方向

例：

Instantiate(prefabGO, targetPos + hit.normal * 0.01f, Quaternion.LookRotation(hit.normal));

##### 遍历到结束重新从第一位开始遍历

```c#
index = (index + 1) % array.length
```

##### int? 是C#的可空值类型

如int? a = null;

此时a不再是原来的值类型，如果需要获取值类型的数据，使用a.Value

##### 判断用户操作上下左右（手机滑动）

X轴移动绝对值高于Y轴则是左右

同时X＞0则为右

上下同理

##### 类型转化

xxx as 需要转化到的类型

##### 控制台

```
Clear 			清除所有信息
Collapse 		折叠相同信息
Clear On Play 	播放时清空信息
Error Pause 	如果异常暂停执行
```



#### 脚本文件与C#类的不同：

```
1.不要在脚本中写构造函数(因为不能在子线程中访问主线程成员);
2.
C#类一般组成(按顺序)：
	字段
	属性
	构造函数
	方法
脚本组成：
	字段
	方法
属性在编辑器(Unity)中不能显示、通常在脚本中不写。
```



### 生命周期

#### 初始阶段

##### Awake

```
当物体载入时立即调用1次;
常用于在游戏开始前进行初始化，可以判断当满足某种条件执行此脚本this.enable=true 。
```

##### OnEnable

```
每当脚本对象启用时调用。
```

##### Start

```
物体载入且脚本对象启用时被调用1次。
常用于数据或游戏逻辑初始化，执行时机晚于Awake。
如果多个物体的Awake与Start同时存在，会先执行完所有物体的Awake阶段再执行所有物体的Start阶段。
执行顺序与Unity编辑器中的物体顺序无关，如果两个物体的初始化有顺序要求，可以一个在Awake阶段执行，一个在Start阶段执行。
```

#### 物理阶段

##### FixedUpdate

```
执行时机：默认每隔0.02s执行一次
适用性：适合对物体做物理操作(移动、旋转等)，不会受到渲染影响
由于机器性能不同，每次渲染量不同，渲染时间不固定
```

##### OnCollisionXXX

```
当满足碰撞条件时调用。
```

##### OnTriggerXXX

```
当满足触发条件时调用。
```

#### 游戏逻辑

##### Update

```
执行时机：渲染帧执行，执行间隔不固定
适应性：处理游戏逻辑(如2048的移动后渲染)
```

##### LateUpdate

```
在Update函数被调用后执行，适用于跟随逻辑。(如主人物移动后的摄像机跟随移动逻辑)
```

#### 场景渲染

##### OnBecameVisible当可见:

```
当Mesh Renderer 在任何相机上可见时调用。
```

##### OnBecameInvisible当不可见:

```
当Mesh Renderer在任何相机上都不可见时调用。
```

#### 结束阶段

 OnDisable当不可用∶

```
对象变为不可用或附属游戏对象非激活状态时此函数被调用。
```

 OnDestroy当销毁∶

```
当脚本销毁或附属的游戏对象被销毁时被调用。
```

OnApplicationQuit当程序结束:

```
应用程序退出时被调用。
```

#### 输入事件

```
OnMouseEnter鼠标移入:
鼠标移入到当前Collider时调用。
OnMouseOver鼠标经过:
鼠标经过当前Collider时调用。
OnMouseExit鼠标离开:
鼠标离开当前Collider时调用。
OnMouseDown鼠标按下:
鼠标按下当前Collider时调用。
OnMouseUp鼠标抬起:
鼠标在当前Collider上抬起时调用。
```

### 调试

调试过程中，输入代码:

右键---快速监视

查看“即时窗口”

单帧调试︰启动调试运行场景暂停游戏加断点单帧执行结束调试



### Component类

提供查找（当前物体及后代、父类）组件的功能。

主要方法：

##### 获取后代物体的指定类型组件（从自身开始）：

```
this.GetComponentsInChildren<type>()
```

##### 获取父代物体的指定类型组件（从自身开始）：

```
this.GetComponentsInParent<type>()
```



### transform类

提供查找(父、根、子)变换组件、物体位置变化、旋转、改变大小功能

```
foreach (Transform child in this.transform)
{ // child为每个子物体的变换组件,不包括孙子物体及自身
	print(child.name);
}
```

##### 物体相对于世界坐标系原点的位置

```
this.transform.position
```

##### 物体相对于父物体轴心点的位置

这也是unity面板中的显示position，打开debug模式会显示为localPosition

```
this.transform.localPosition
```

##### 相对父物体缩放比例

```
this.transform.localScale
```

##### 物体与模型缩放比例(自身缩放比例*父物体缩放比例)

```
this.transform.lossyScale // 只读属性

如:父物体localScale为3，当前物体localScale为2，lossyScale则为6
```

##### 向自身坐标系z轴移动1米

```
this.transform.Translate(0,0,1);
```

##### 向世界坐标系z轴移动1米

```
this.transform.Translate(0, 0, 1,Space.World);
```

##### 沿自身坐标系y轴旋转10度

```
this.transform.Rotate(0,0, 1);
```

##### 沿世界坐标系y轴旋转10度

```
this.transform.Rotate(0,10, 0, Space.World);
```

##### 获取根物体变换组件，即最开始的父组件

```
Transform rootTF = this.transform.root;
```

##### 获取父物体变换组件

```
Transform parentTF = this.transform.parent;
```

##### 根据索引获取子物体

```
int count = this.transform.childCount;
for (int i = 0; i< count; i++){
	Transform childTF = this.transform.GetChild(i);
}
```



### gameObject类

##### 在场景中物体激活状态(物体实际激活状态)，即是否在场景中渲染

```
this.gameObject.activelnHierarchy
```

##### 物体自身激活状态(物体在lnspector面板中的状态)

```
this.gameObject.activeSelf
```

##### 设置物体启用/禁用

```
this.gameObject.SetActive()
```

##### 获取所有使用该标签的物体

```
GameobjectallEnemy = GameObject.FindGameObjectsWithTag('tagName')
```

##### 获取使用该标签的物体（单个)

```
GameObject playerGo =Gameobject.FindWithTag('tagName')
```

#### 添加组件

```
// 创建物体，以light组件为例
GameObject lightGo = new Gameobject();
// 添加组件
Light light = lightGO.AddComponent<Light>(); // 组件类型
light.color = Color.red;
light.type = LightType.Point;
```

### Object类

##### 删除─个游戏对象、组件或资源

```
Destroy // Removes a gameobject, component or asset.
```

##### 加载新场景的时候使目标对象不被自动销毁

```
DontDestroyOnLoad // Makes the object target not be destroyed automatically when loading a new scene.
```

##### 返回Type类型第一个激活的加载的对象

```
FindObjectOfType // Returns the first active loaded object of Type type.
```

##### 返回Type类型的所有激活的加载的物体列表

```
FindObjectsOfType // Returns a list of all active loaded objects of Type type.
```

##### 克隆原始物体并返回克隆物体

```
Instantiate // Clones the object original and returns the clone.
```

### Time类

从Unity获取时间信息的接口

##### 常用属性

###### time :从游戏开始到现在所用时间。

```
存在绝对时间与相对时间，相对时间在游戏暂停时不继续计时，绝对时间不受影响。属性名忘了。
```

###### timeScale:时间缩放。

```c#
常用于暂停/继续游戏，子弹时间等。
例：
Time.timeScale = 0;
update渲染场景时执行，不受Time.timeScale影响。
fixedUpdate受Time.timeScale影响。
如果需要在暂停游戏时保持个别物体不受影响：
使用Time.unscaledDeltaTime
```

deltaTime :以秒为单位，表示每帧的经过时间。

```
在Update生命周期中，使用speed * Time.deltaTime维持恒定的更新速度，不受机器性能影响。
```

unscaledDeltaTime :不受缩放影响的每帧经过时间。

##### 定时操作

以间隔一秒操作为例：

有三种方案：

###### 1.使用Time.time，到达预定的时间后时间加一。

```c#
放在update生命周期中：
if (Time.time >= nextTime)
{
	...
	nextTime + 1;
}
```

###### 2.累加Time.deltaTime，到达一定值后执行逻辑，后清空累计值

```c#
放在update生命周期中：
{
    // 累加每帧间隔
	totalTime += Time.deltaTime;
	if (totalTime >= 1)
	{
		...
		totalTime = 0;
	}
}
```

###### 3.使用api InvokeRepeating（monoBehavior类）

```c#
放在start生命周期中：
{
	// 类似js的setInteval
	InvokeRepeating('要执行的方法名', 第一次执行时间（S）, 每次执行间隔（S）);
}
...
CancelInvoke('要取消的方法名');
同理有个api类似js的setTimeOut------Invoke
```



##### 预制件

一种资源类型，可以多次在场景进行实例。

###### 优点:对预制件的修改，可以同步到所有实例，从而提高开发效率。

如果单独修改实例的属性值，则该值不再随预制件变化。

Select键:通过预制件实例选择对应预制件

Revert键:放弃实例属性值，还原预制件属性值

Apply键:将某一实例的修改应用到所有实例



### Animation

##### Animaion View

通过动画视图可以直接创建和修改动画片段(Animation Clips)

显示动画视图：Window——Animation

##### 创建动画片段

为物体添加Animation组件

在动画视图中创建片段

##### 录制动画片段

录制步骤:

1.点击录制按钮，开始录制动画。

2.添加关键帧Add Property，选择组件类型。

3.选择关键帧，调整时间点。

4.在Scene 或 Inspector面板设置属性。

5.点击录制按钮，结束录制动画。

任何组件以及材质的属性都可进行动画处理，即使是自定义脚本组件的公共变量。

##### 常用Api

bool isPlay=animation.isPlaying;

bool isPlay=animation.IsPlaying("动画名");

animation.Play("动画名");

animation.PlayQueued("动画名");

animation.CrossFade ("动画名");

animation["动画名"].speed = 5;

animation["动画名"].wrapMode = WrapMode.PingPong;

animation["动画名"].length;

animation["动画名"].time;



### Input

##### 鼠标输入

获取鼠标输入

```c#
当指定的鼠标按钮被按下时返回true
bool result=Input.GetMouseButton(O);

在用户按下指定鼠标按键的第一帧返回true
bool result= Input.GetMouseButtonDown(O);

在用户释放指定鼠标按键的第一帧返回true
bool result= Input.GetMouseButtonUp(O);

按钮值设定:
0对应左键，1对应右键，2对应中键。
```

##### 键盘输入

获取键盘输入

```
当通过名称指定的按键被用户按住时返回true
bool result=Input.GetKey(KeyCode.A);

当用户按下指定名称按键时的那一帧返回true
bool result=Input.GetKeyDown(KeyCode.A);

在用户释放给定名称按键的那一帧返回true
bool result=Input.GetKeyUp(KeyCode.A);
```



#### InputManager 输入管理器

##### 制作玩家设置按键页面

输入管理器   Edit-Project Settings-Input

使用脚本通过虚拟轴名称获取自定义键的输入。

玩家可以在游戏启动时根据个人喜好对虚拟轴进行修改。



##### 参数

```
Descriptive Name :

游戏加载界面中，正向按键的详细描述。

Descriptive Negative Name :

游戏加载界面中，反向按键的详细描述。

Negative Button :该按钮会给轴发送一个负值。

Positive Button:该按钮会给轴发送一个正值。

Alt Negative Button:给轴发送负值的另一个按钮。

Alt Positive Button :给轴发送正值的另一个按钮。

Gravity:输入复位的速度，仅用于类型为键/鼠标的按键。

*Dead:任何小于该值的输入值(不论正负值)都会被视为0，用于摇杆。

Sensitivity:灵敏度，对于键盘输入，该值越大则响应时间越快，该值越小则越平滑。对于鼠标输入，设置该值会对鼠标的实际移动距离按比例缩放。

Snap:如果启用该设置，当轴收到反向的输入信号时，轴的数值会立即置为0，否则会缓慢的应用反向信号值。仅用于键/鼠标输入。

Invert:启用该参数可以让正向按钮发送负值，反向按钮发送正值。

Type类型:

--键/鼠标(Key / Mouse),

--鼠标移动和滚轮(Mouse Movement),--摇杆(Joystick Axis)。

Axis:设备的输入轴（摇杆，鼠标，手柄等)

*Joy Num :设置使用哪个摇杆。默认是接收所有摇杆的输入。仅用于输入轴和非按键。
```



##### Api

```C#
bool result=Input.GetButton("虚拟轴名");

bool result=Input.GetButtonDown("虚拟轴名");

bool result=Input.GetButtonUp("虚拟轴名");

float value=Input.GetAxis("虚拟轴名");

float value=Input.GetAxisRaw("虚拟轴名");
```



### 3D Math

##### 沿xyz轴旋转

原理：

this.transform.rotation  *= Quaternion.Euler(1, 0, 0);

Api：

this.transform.rotate

欧拉角的数据类型为Vector3

上下旋转沿自身坐标系

左右旋转需沿世界坐标系Y轴

##### 常用Api

```
Quaternion.LookRotation
Quaternion.Euler
Quaternion.Lerp
Quaternion.FromToRotation
Quaternion.AngleAxis
```



##### 注视旋转

```C#
// 注视tf旋转
Vector3 dir = tf,position - this.transfrom.position;
this.transform.rotation = Quaternion.LookRotation(dir);
// Api(不能缓慢变化)
this.transform.LookAt(tf);

// 差值(逐渐变慢)旋转
Quaternion dir = Quaternion.LookRotation(tf,position - this.transfrom.position);
this.transform.rotation = Quaternion.Lerp(this.transform.rotation, dir, 0.1f)
// 匀速旋转
this.transform.rotation = Quaternion.RotateTowards(this.transform.rotation, dir)
// X轴注视旋转
this.transform.right = tf,position - this.transfrom.position;
// 返回两物体相距角度 单位度
Quaternion.Angle(a, b)
```

##### 被注视物体高于注视物体，人物倾斜问题修复

```C#
方案一：
targetPoint.y = this.transform.position.y;

方案二：
// 仅旋转Y轴
Vector3 euler = Quaternion.LookRotation(targetPoint - this.transform.position);
this.transform.eulerAngles = new Vector3(0, euler.y, 0);
```



### 坐标系

##### World Space

世界(全局)坐标系:整个场景的固定坐标。

作用∶在游戏场景中表示每个游戏对象的位置和方向。

##### Local Space

物体(局部)坐标系:每个物体独立的坐标系，原点为模型轴心点，随物体移动或旋转而改变。

作用:表示物体间相对位置与方向。

##### Screen Space

屏幕坐标系:以像素为单位，屏幕左下角为原(0，0)点，右上角为屏幕宽、高度(Screen.width ，Screen.height)，Z为到相机的距离。

作用:表示物体在屏幕中的位置。

##### Viewport Space

视口(摄像机)坐标系∶屏幕左下角为原(0，0)点，右上角为(1,1)，Z为到相机的距离。

作用:表示物体在摄像机中的位置。

#### 坐标系转换

##### Local Space --> World Space

```
transform.TransformPoint
转换点，受变换组件位置、旋转和缩放影响。

transform.TransformDirection
转换方向，受变换组件旋转影响。

transform.TransformVector
转换向量，受变换组件旋转和缩放影响。
```

##### World Space -->Local Space

```
transform.InverseTransformPoint
转换点，受变换组件位置、旋转和缩放影响。

transform.InverseTransformDirection
转换方向，受变换组件旋转影响。

transform.InverseTransformVector
转换向量，受变换组件旋转和缩放影响。
```

##### World Space <--> Screen Space

```
Camera.main.WorldToScreenPoint
将点从世界坐标系转换到屏幕坐标系中

Camera.main.ScreenToWorldPoint
将点从屏幕坐标系转换到世界坐标系中
```

##### World Space <--> Viewport Space

```
Camera.main.WorldToViewportPoint
将点从世界坐标系转换到视口坐标系中

Camera.main.ViewportToWorldPoint
将点从屏幕坐标系转换到世界坐标系中
```



### 刚体

带有刚体组件的游戏物体

Add Component-physics-Rigidbody

刚体组件可使游戏对象受物理引擎控制，在受到外力时产生真实世界中的运动。

物理引擎:模拟真实世界中物体物理特性的引擎。

##### 属性

```
质量 Mass :
物体的质量。

阻力Drag :
当受力移动时物体受到的空气阻力。0表示没有空气阻力，极大时可使物体停止运动，通常砖头0.001，羽毛设置为10。

角阻力Angular Drag:
当受扭力旋转时物体受到的空气阻力。0表示没有空气阻力，极大时使物体停止旋转。

使用重力Use Gravity:
若激活，则物体受重力影响。

是否是运动学Is Kinematic :
若激活，该物体不再受物理引擎控制，而只能通过变换组件来操作。

插值Interpolate:
用于缓解刚体运动时的抖动。
	无None --不应用插值。
	内插值Interpolate --基于上一帧的变换来平滑本帧变换。
	外插值Extrapolate --基于下一帧的预估变换来平滑本帧变换。

碰撞检测Collision Detection :
碰撞检测模式。快速移动的刚体在碰撞时有可能互相穿透，可以设置碰撞检测频率,但频率越高对物理引擎性能影响越大。
	不连续Discrete :不连续碰撞检测。适用于普通碰撞（默认模式）。
	连续Continuous :连续碰撞检测。
	动态连续Continuous Dynamic :连续动态碰撞检测,适用于高速物体。

约束Constraints :
对刚体运动的约束。
	冻结位置Freeze Position :刚体在世界中沿所选X，Y，Z轴的移动，将无效。
	冻结旋转 Freeze Rotation :刚体在世界中沿所选的X,Y,Z轴的旋转，将无效。
```

### 碰撞器

使刚体具有碰撞效果

可以单独作用于物体，但是要使移动的物体具有碰撞效果必须附加刚体组件。

##### 分类

```
静态碰撞器Static Collider:
只有碰撞器没有刚体的物体现象︰保持静止或者轻微移动，如:平面/树木

刚体碰撞器Rigidbody Collider:
具有刚体和碰撞器的物体;
现象:完全受物理引擎影响。

运动学刚体碰撞器:
带刚体,且勾选Is Kinematic，此碰撞器不能添加力，只能通过transform移动。
```

##### 属性

```
是否触发器Is Trigger : 
如激活，此碰撞器用于触发事件，并且被物理引擎忽略。

材质 Material :
引用何种物理材质决定了他和其他对象如何作用。

凸起的Convex:
不激活则网格碰撞器间没有碰撞效果;

Mesh 网格:
用于碰撞所引用的网格
```

##### 物理材质

```
用于调整碰撞对象的摩擦力和反弹效果。

属性

动态摩擦力Dynamic Friction:
移动时摩擦力

静态摩擦力Static Friction:
静止时摩擦力

弹力(Bounciness):
反弹程度
备注:摩擦力、弹力建议O---1之间

摩擦力合并模式Friction Combine Mode、
合并反弹Bounce Combine :
两个碰撞对象摩擦力/弹力的合并方式
平均值Average最小Min最大Max相乘Multiply
```

#### 碰撞条件

两者具有碰撞组件

运动的物体具有刚体组件

##### 碰撞三阶段

```
当进入碰撞时执行
void OnCollisionEnter(Collision collOther)

当碰撞体与刚体接触时每帧执行
void OnCollisionStay(Collision collOther)

当停止碰撞时执行
void OnCollisionExit(Collision collOther)
```



### 触发器

带有碰撞器组件，且Is Trigger属性被勾选的物体。

现象︰无碰撞效果。

#### 触发条件（碰撞与触发可以同时发生）

两者具有碰撞组件

其中之一带有刚体组件

其中之一勾选isTrigger

##### 触发三阶段

```
当Collider(碰撞体)进入触发器时执行
void OnTriggerEnter(Collider cldOther)

当碰撞体与触发器接触时每帧执行
void OnTriggerStay(Collider cldOther)

当停止触发时执行
void OnTriggerExit (Collider cldOther)
```



### UGUI

#### Canvas

画布，绘制UI元素的载体，所有UI元素必须在Canvas之下。UI元素的绘制顺序依赖于层次面板中的顺序。

##### 属性

###### Render Mode渲染方式

###### Screen Space-Overlay覆盖模式:

```
UI元素将绘制在其他元素之前，且绘制过程独立于场景元素和摄像机设置，画布尺寸由屏幕大小和分辨率决定。

Pixel Perfect完美像素∶若勾选，则会锐化屏幕显示效果。

Sort Order渲染顺序:在多个Canvas中，值越大越渲染到最上层。
```

###### Screen Space-Camera摄像机模式:

```
提供UICamera ,Cancas对象被绘制在一个与摄像机固定距离的平面上，且绘制效果受摄像机参数的影响。

Render Camera 
提供渲染的摄像机。

Plane Distance
平面与摄像机的距离。

Sorting Layer 排序层:
通过Edit--Project Settings-Tags and Layers调整Canvas渲染顺序。
```

###### World Space世界空间模式:

画布渲染于世界空间，与场景中其他3D物体性质相同。

##### 调试UGUI：

勾选左上角最后一个模式（新版本多出几个模式，可能不是最后一个了）

以及勾选上2D选项



##### 游戏物体需要显示在GUI上面

Render Mode为 Screen Space-Camera

新建一个Camera

camera组件的Clear Flags属性勾选Depth only

Culling Mask 勾选UI

将需要显示的游戏物体设为UI层



##### 小技巧

文字显示在物体上（如广告牌之类的）

Render Mode为 World Space

一般调整字体大小不会去调整像素（会导致字体变模糊）

而是调整父Canvas的Scale（一般为0.01, .0.01, 0.01）



##### canvas

当画布为overlay模式时

世界坐标（单位米）等同于屏幕坐标（单位像素）

this.transform.position

当前轴心点：

相对于父UI的轴心点位置

this.transform.localPosition



##### 设置UI宽度

rtf.SetSizeWithCurrentAnchors(RectTransform.Axis.Horizon, '需要设置的大小');

当锚点不分开时可以这么设置

size = rtf.sizeDelta





##### 页面适配

canvas属性选择：

Canvas Scaler/UI Scale Mode选择Scale With Screen

Reference Resolution XY与分辨率等同

Screen Match Mode/Match选择上面XY中较小的值



### 事件

#### 事件注册

##### 实现接口

```C#
using UnityEngine.EventSystems; // 引入unity事件系统
// 继承事件类型
public class DialogDrag : MonoBehaviour,IPointerDownHandler,IDragHandler
{
    // 接口实现
    public void OnPointerDown(PointerEventData eventData)
    {
        
    }
    public void OnDrag(PointerEventData eventData)
    {
        
    }
}
```



### C#知识点



##### 执行程序

点击生成，生成解决方案，文档/bin/debug中会有一个exe文件，点击可打开控制台。

程序在运行到最后一行后控制台就会自动关闭。

所以使用Console.WriteLine()作为中止程序的代码行（因为它在等待输入，所以不会执行完毕，按下回车后程序就走到下一行，结束后就关闭了。

程序其实都是运行在内存中的。

##### Console.WriteLine()

在控制台中输出

##### Console.WriteLine()

读取用户在控制台中的输入

按enter键结束

##### 快捷键

注释：ctrl + k + s

对齐：

取消注释：

变量重命名：ctrl + .

快速提取语句作为方法：

快速属性：prop+tab+tab

##### 基础文件解释：

```c#
using System;
// 引入命名空间，下面的Console.ReadLine就是引入的命名空间中的方法，如果不引入需要使用System.Console.ReadLine调用。
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

// 定义命名空间 后续引入这个命名空间就可以使用它里面的类的方法
namespace ConsoleApp1
{
    // 定义类
    internal class Program
    {
        // 定义方法
        static void Main(string[] args)
        {
            // 语句
            Console.WriteLine("请输入用户名");
            string input = Console.ReadLine();
            Console.WriteLine(input);
            Console.ReadLine();
        }
    }
}
```



#### 数据类型

##### 整型

```
1个字节:有符号sbyte(-128~127)，无符号byte(O~255)
2个字节:有符号short(-32768~32767)，与无符号ushort(O~65535)
4字节:有符号int，无符号uint
8字节:有符号long，无符号ulong
```

###### Tips: 其实一般存年龄也用int，不在乎三个字节，且约定俗成。

##### 浮点型

```
4字节:单精度浮点类型float，精度7位。
8字节:双精度浮点类型double，精度15-16位。
16字节:128位数据类型decimal，精度28-29位，适用于财务和货币计算。
注意事项:
	1.非整形变量赋值要加上后缀，如果不加默认为double。2.浮点型运算会出现舍入误差:
	bool number= 1.0f - 0.9f == 0.1f;
	二进制无法精确表示1/10，就像十进制无法精确表示1/3，所以二进制表示十进制会有一些舍入误差，对于精度要求较高的场合会导致代码的缺陷，可以使用decimal代替。
	一般unity存地址，都是用的float。
```

##### 字符类型

```
char字符，2字节，存储单个字符，使用单引号。
string字符串，存储文本，使用双引号。
```

##### bool类型

```
1字节，可以直接赋值true真false假，或者赋表达式做判断。
```

##### 变量声明

```
声明变量：在内存中开辟一块空间，存储变量名与变量值。
赋值：找到变量名所存在的空间，更改该空间的值。
```

#### 基本类型转换

##### 转换语法

```c#
int num = 100;
byte num1 = (byte)num;
在要转换的变量前加(要变成的类型);
```



##### 隐式转换

由小类型到大类型的自动转换。

```
多种类型变量参与的运算，会产生类型提升，结果自动转换为较大字节类型。
byte类型在运算时会自动转化为int类型，因为byte类型运算很容易发生溢出。
但是运算符缩写不会自动转化（+=，-=等等）。
```



##### 显式转换

```c#
手动强制转换。
大类型到小类型的数据可能造成数据丢失，前面的数字字节丢失。
如 
int num = 265;  --------100001001
byte bt = (byte)num;---- 00001001
```



##### ToString转换

```c#
任意类型转换为字符串类型。int num = 100;
string strNumber = num.ToString();
```



##### Parse转换

```c#
字符串类型转换为其他类型string strNumber = "100";
int num = int.Parse(strNumber);
若字符串未被识别为该类型的有效值，则程序抛异常。int number01 = int.Parse("1.0");
float number02= float.Parse("1.Of");
```

##### TryParse

```c#
通过bool表达式配合TryParse使用，防止类型转换失败。语法:
int number;
bool result = int.TryParse( "500”, out number);
```



#### Tips

##### if语句如果只有一行语句，大括号可以省略。

##### int类型相除，如果为非整数的话会向下取整。

##### C#占位符：

```c#
string str = string.Format("第 { 0 } 个点位符", "1" );
```

###### 占位符数据格式化：

```
{0:d2} // 以两位数显示数字（时间格式）
```

##### vs中紫色立方体代表方法，扳手图标代表属性。

##### 代码规范：

```c#
实例成员的初始化放在构造函数中做，而不是在声明成员时做。
例：
private int[] arr = new int[5]; ×
private int[] arr;
public Student()
{
	arr = new int[5]; √
}
```



#### 函数返回值类型

函数返回值必须与定义的返回值类型兼容。

void代表无返回值类型，函数体中可以没有return关键字。

定义函数：

private static 返回值类型 函数名(){

}

#### 方法(函数)

##### 定义：

```c#
[访问修饰符] [可选修饰符] 返回类型 方法名称(参数列表){

	//方法体

	return结果;

}

void代表无返回值类型，方法体中return关键字可有可无。
    
例：
private static void Add(){
    
}

private static int Add(int numberOne,int numberTwo){
    return int a;
}
static int GetWeekByDay(int year,int month,int day){}
调用：
int result = Add(numberOne,numberTwo);
```



##### 方法重载

```
两个方法名称相同，但参数列表不同（如（int hour,int date)与(int hour)。一个为一个参数，一个为两个参数。
用于在不同条件下解决同一类型的问题。
仅仅out与ref的区别不可以构成重载。
官方方法按F12可以查看其重载的方法。按键盘上下键或鼠标左键可以查看下一个。
例：
```

![image-20220517215343284](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220517215343284.png)



#### 参数类型

##### 值参数

```c#
意思是如果是值类型，在方法内部参数值改变不会影响到原变量。
例：
int a = 1;
fun(a);
Console.WriteLine(a); // 1
fun(int num)
{
	num = 2;
}
引用类型因为本身存的就是内存地址，所以修改引用类型的内部数值时会改变原数据。但是如果更改的是被引用的地址就不会影响到原数据。
arr[0] = 1; // 修改引用地址的数据
arr = new Array[]; // 修改被引用地址
默认为值参数。
调用方法时复制实参变量所存储的内容。
作用:传递数据。
语法:
(数据类型参数名[数据类型参数名])
```

##### 引用参数

```c#
即使是传值类型作为参数，也会将值类型的内存地址传进去。修改参数值会影响到方法外部的变量值。
例：
int a = 1;
fun(ref a);
Console.WriteLine(a); // 2
fun(ref int num)
{
	num = 2;
}
使用ref关键字修饰。
调用方法时复制实参变量在栈中的引用。作用:改变数据。
语法∶
...( ref数据类型参数名[,ref数据类型参数名])
```

##### 输出参数

```
当一个方法需要两个或以上返回值时，使用输出参数作为传参参数(至于一个为return,一个为out还是都为out就看个人喜好，都可以)
使用out关键字修饰。
调用方法时复制实参变量在栈中的引用。
作用:返回结果。
语法:
...( out 数据类型参数名[,out 数据类型参数名])
与引用参数区别
ref要求实参必须在传递前进行赋值，
out要求形参离开方法前必须赋值。
```



#### 递归

核心思想：将一个需求层层拆解，限制更小的范围，然后专注解决最后拆解出来的小需求。



#### for循环

i++放在非循环语句中，比如放在if中，可以实现类递归的效果。

```c#
for (int i = 0; i < arr.length;){
    if (arr[i] == 2) {
        .... // 发现为二，不自增，下次进来i还是上一次的i;
    } else {
        i++;
	}
}
```



#### 数组



##### 声明

```c#
数据类型[] 数组名;
初始化的元素类型与声明时的类型必须相同。
例:
int[] array01 = new int[5];
string[] array02 = new string[3];
```



##### 初始化

```
数组初始化后，内存中存储该数据类型的默认值。
-- 整形为О
-- 非整形为0.0
-- char为\0
-- string为 null
-- bool为false
```

##### 初始化＋赋值

```c#
可以在数组初始化的同时对元素进行赋值。语法:
数据类型]数组名=new数据类型{元素1,元素2};
例如∶
int[] array01 = new int[]{ 1,2,3,4,5 };
string[] array02 = new string[]{"a", "b","c"};
初始化时[]内也可以填入数组长度，但必须与所赋值的元素总数一致。
例如∶
double[] array03 = new double[2]{ 1.0,2.0 };
```

##### 声明＋赋值

```c#
可以在数组声明的同时对元素进行赋值。
语法:
数据类型[] 数组名={元素1,元素2};
例如:
int[] array01 = {1,2,3,4,5};
元素个数即为数组长度。
程序员可以省略初始化，但编译器内部仍然会"new数据类型”。
不支持以下写法:
double[] array03;
array03 ={ 1.0,2.0 };
```



##### foreach

```c#
foreach是一种更简单更明了的读取数组元素的语句。
局限性:
    --只能读取全部元素(语句本身)
    --不能修改元素
    --只能遍历实现lenumerable接口的集合对象
语法：
foreach(元素类型 变量名 in 数组名)
{
	变量名表示数组中的每个元素
}
```



##### 数组常用方法

```c#
数组长度:数组名.Length
清除元素值:Array.Clear
复制元素:Array.copy
数组名.CopyTo
克隆:数组名.Clone
查找元素: Array.IndexOf Array.LastIndexOf
排序: Array.Sort
反转:Array.Reverse
若是二维数组，则有
array.GetLength(0);//获取第一维的长度，即行数
array.GetLength(1);//获取第二维的长度，即列数
```

##### 多维数组

```c#
具有两个或多个索引的数组。
语法:
--声明 ＋ 初始化
数据类型[]数组名= new数据类型[行数,列数];
string[,] array01 = new string[3,2];
--初始化 ＋ 赋值
数组名=new数据类型 {元素1,元素2},{元素3,元素4}};
int[,] array02 = new int[,]{{1,2},3,4}};
--读写元素
数组名[行索引,列索引]
```

##### 交错数组

```c#
元素为数组的数组，每个元素都是一个新的一位数组。(可以理解为列长短不一的数组，定义与一般数组不同，赋值与读写都相同。)
语法:
--定义
数据类型[][] 数组名= new 数据类型[元素总数];
string[][] array = new string[3][];
--赋值
数组名[索引= new数据类型[子元素数];
array[0] = new string[2];
--读写元素
数组名[元素索引][子元素索引]
```

##### 参数数组

```c#
方便使用者传参。就是语法糖在形参处默认帮使用者定义了new Array;
在方法形参中通过关键字params定义。
方法调用者可以传递数组，也可以传递一组数据类型相同的变量，甚至可以不传递参数。
注意:
参数数组必须在形参列表中的最后一位。只能在一维数组上使用params关键字。
WriteLine中使用占位符，就是通过参数数组实现的。
例：
private static int Add( params int[] array )
{
    int sum = O;
    foreach (int item in array)
        sum += item;
    return sum;
}

调用:
Add(int[] arr = {1, 2});
Add(1, 2, 3);
Add(); // 结果为0
上述三种调用方式都可。
```



#### 集合类

用类封装的数组，可以理解为js的数组。

#### 数据类型

##### 值类型与引用类型

```
局部变量的值类型:声明在栈中，数据在栈中。
局部变量的引用类型∶声明在栈中，数据在堆中，栈中存储数据的引用。
```

比较引用地址的方法：

```c#
object.ReferenceEquals(s1,s2); // return bool;
```



##### 类型归属

![image-20220619205919779](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220619205919779.png)

###### 注：C#中string类型是引用类型(因为不知道字符串长度);



##### 内存分配

```
程序运行时，CLR将申请的内存空间从逻辑上进行划分。
栈区:
--空间小(1MB)，读取速度快。
--用于存储正在执行的方法，分配的空间叫做栈帧。栈帧中存储方法的参数以及变量等数据。方法执行完毕后，对应的栈帧将被清除。
堆区:
--空间大，读取速度慢。
--用于存储引用类型的数据。
```

##### 局部变量(与js不同)

```
定义在方法内部的变量。
特点:
--没有默认值，必须自行设定初始值，否则不能使用。--方法被调用时，存在栈中，方法调用结束时从栈中清除。
```

##### 成员变量

```
定义在类中方法外的变量
特点:
--具有默认值。
--所在类被实例化后，存在堆中，对象被回收时，成员变量从堆中清除。
--可以与局部变量重名。
```



#### 拆装箱

##### 装箱(box)

```
值类型隐式转换为object类型或由此值类型实现的任何接口类型的过程。
例：形参object类型，实参传递值类型，则装箱。
可以通过重载、泛型避免。
内部机制:
1.在堆中开辟内存空间(需要一块数据空间，一块同步块索引空间，一块类型对象指针空间。
所以相对比较消耗性能，但是相对其他优化可以忽略不计。)
⒉将值类型的数据复制到堆中
3.返回堆中新分配对象的地址
```

##### 拆箱(unbox)

```
从object类型到值类型或从接口类型到实现该接口的值类型的显式转换。
内部机制:
1.判断给定类型是否是装箱时的类型
2.返回已装箱实例中属于原值类型字段的地址
```

##### 注意

```
拆箱后的类型必须与装箱时的类型相同。
伴随拆箱的字段复制步骤不属于拆箱过程。
装箱和拆箱不是互逆的过程，装箱的性能开销远大于拆箱。
```



#### string

##### 特性

```
字符串常量具备字符串池特性
	字符串常量在创建前，首先在字符串池中查找是否存在相同文本。如果存在，则直接返回该对象引用;如果不存在，则开辟空间存储。
	目的:提高内存利用率。

字符串具有不可变性
	字符串常量一旦进入内存，就不得再次改变。因为如果在原位置改变会使其他对象内存被破坏，导致内存泄漏。当遇到字符串变量引用新值时，会在内存中新建一个字符串，将该字符串地址交由该变量引用。
```



#### 枚举

##### 简单枚举

```
列举某种数据的所有取值。(单选框)
作用:增强代码的可读性，限定取值。
语法: enum 名字{值1，值2，值3，值4}。
枚举元素默认为int，准许使用的枚举类型有byte、sbyte、short、ushort、int、uint、long或ulong。
每个枚举元素都是有枚举值。默认情况下，第一个枚举的值为0，后面每个枚举的值一次递增1，可以修改值，后面枚举数的值依次递增。
```

##### 标志枚举

```c#
可以同时赋多个枚举值。(可复选)
条件:
--任意两个枚举值做按位或运算的结果不能与其他枚举值相同。
--使用[Flags]特性标记枚举类型。
语法:
[Flags]
enum枚举类型名称{
	枚举值1= 1,
	枚举值2= 2,
	枚举值3= 4,
	枚举值4= 8,
	枚举值4= 16,
}
```



#### 类与对象

##### 语法：

```c#
访问级别 class 类名 {
    字段
    属性
    构造函数
    方法
}
例：
class User
{
    // 字段 存储数据的变量
    private string name;
    private string loginld;
    private string Password;
    
    // 属性 get set属性的方法，与字段同名并大写。
    public string Name
    {
        get
        {...}
        set
        {...}
    }
    // 自动属性
    // public string Name {get;set;}
    
    // 构造函数 若不手动添加，编译器会自动加一个构造函数，若手动添加则没有
    public User(){
    }
    
    // 构造函数的重载
    public User(string loginld, string pwd){
        this.loginld = loginld;
        this.Password = pwd;
    }
    
    // 方法
    public void PrintUser(){
        Console.WriteLine("账号:{0}，密码:{1}",Loginid, Password);
    }
}
通常每个类都在一个独立的c#源文件中。
创建新的类意味着在当前项目中产生了一种新的数据类型。
```

###### 访问修饰符

```
用于修饰类及类成员的访问可见范围。
public:所属类的成员以及非所属类的成员都可以访问。
private:只有所属类的成员才能访问。[类成员的默认级别]。
```

###### 属性

```
对字段起保护作用，可实现只读、只写功能。
本质就是对字段的读取与写入方法。
语法∶
[访问修饰符]数据类型属性名
{
	get { return 字段; }
	set { 字段 = value; }
}
通常一个公有属性和一个私有字段对应。
属性只是外壳，实际上操作的私有字段。
当属性访问器中不需要任何其他逻辑时，使用自动属性可以更加简洁。例：见上文。
```

###### 构造函数

通过:this调用构造函数重载。

```
提供了创建对象的方式，初始化类数据成员的特殊方法。
与类同名。
没有返回值，也不能写void。
不能被直接调用，必须通过new运算符在创建对象时才会自动调用。
每个类都必须至少有一个构造函数，若不提供，编译器自动生成一个无参构造函数。
如果程序员定义了构造函数，则编译器不会再提供。
```

##### this关键字

```
表示当前对象的引用。
访问当前类成员时，使用this关键字，可以提高代码的可读性;在没有歧义的情况下，也可以省略。
```



#### 字典集合



#### 继承

```c#
父类型的引用指向子类的对象
只能使用父类成员
Person person02 = new Student();
如果需要访问该子类成员，需要强制类型转换
Student stuo2 = (Student)person02;
```



#### Static

##### 静态成员变量

```
使用static关键字修饰的成员变量。
静态成员变量属于类，类被加载时初始化，且只有一份。
实例成员变量属于对象，在每个对象被创建时初始化，每个对象一份。
特点:存在优先于对象，被所有对象所共享，常驻内存。
```

##### 静态构造函数

```
初始化类的静态数据成员。
仅在类被加载时执行一次。
不允许使用访问修饰符。
```

##### 静态方法

```
通过引用调用实例方法时，会隐式的传递对象引用，以便在方法内部可以正确访问该对象成员变量。
通过类名调用静态方法时，因为没有具体对象，所以在static方法中不能访问实例成员。
```

##### 静态类

```
使用static关键字修饰的类。
不能实例化，只能包含静态成员。
静态类不能被继承，但是静态方法、属性都可以被继承。
```

##### 适用性

```
利:单独空间存储，所有对象共享，可直接被类名调用。
弊:静态方法中只能访问静态成员，共享数据被多个对象访问会出现并发。
适用场合:
1.所有对象需要共享的数据。
2.在没有对象前就要访问成员。
3.工具类适合做静态类(常用，不需要过多数据)。
```



#### 结构 struct

##### 结构属于值类型，类属于引用类型。

```
定义:用于封装小型相关变量的值类型。
与类语法相似，都可以包含数据成员和方法成员。
但结构属于值类型，类属于引用类型。
适用性:
表示点、颜色等轻量级对象。
如创建存储1000个点的数组，如果使用类，将为每个对象分配更多内存，使用结构可以节约资源。
```

##### 语法

```
使用struct关键字定义。
除非字段被声明为const或 static，否则无法初始化。
结构不能继承，但可以实现接口。
结构总会包含无参数构造函数。
构造函数中必须初始化所有字段。
```



### Month3

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

##### C#线程同步

百度





### Month4

##### 发展方向

```
c#  unity -> NGUI(看  分析）（写）编写编辑器
c++ -> 图形学(openglES DX) -> 开源引擎（OGRE) -> 自研

c#unity -> NGUI(看  分析)(写）编写编辑器
c++ -〉 图形学（openglES DX）-> 着色器（cg | 综合 物理）1%

c# unity ->NGUI (看 分析）(写）编写编辑器
插件（着色器（可视化）镜头特效 原理) —> 技术美术

c#unity -> VR 2B 客户 产品经理 利润 ?
```



##### Draw Calls优化

###### 1.动态批处理：

Dynamic Batching

1.单个网格顶点在300以内

2.相同材质且材质必须是单pass

3.必须是Mesh Renderer渲染出的组件才能参与动态批处理

4.所有静态物体都不能参与动态批处理

5.模型缩放过大不会被优化



###### 2.静态批处理

Static Batching

1.只有静态物体会参与静态批处理

2.跟顶点数无关

3.和pass无关

4.缩放有关

5.必须是Mesh Renderer渲染出的组件才能参与静态批处理

###### 2.图片格式选择

选择无损压缩，文件更小的png格式

RGBA DXT5 图片更大，有透明（树木等需要透明的选择

RGBA DXT1 图片更小，无透明（不需要透明的选择



勾选碰撞器isTrigger会关闭物理引擎，节省开销，如UI这类的触发器



##### 打包

二进制文件（如XML文件等）在unity打包的时候不会随工程打包出去，放在特殊文件夹下（StreamingAssets等）才会随工程打包出去

##### StreamingAssets

打包资源

不压缩不加密

在pc端可读可写

在移动端只读

##### Plugins

该文件夹下的文件会优先编译打包，所以适合放插件，调用的时候不会空引用

存放所有库文件

Windows下的.dll动态链接库

Linux、MAC、Android、IOS下.so共享函数库

##### 安卓的沙箱运行环境

导致数据持久化策略差异

##### XML打包时候需要先切换打包类型，否则会失败





##### SQLite

数据库可视化软件：Navicat for SQLite

增删改查等操作，需要先连接数据库，增删改查完成后需要断开连接

```C#
private void InsertData(){
	CreateDataBase();
	db.InsertInto();
	db.closesqlconnection();
}
```

增删改的数据额如果是字符类型，需要额外一个单引号(sqi语法)

```C#
db.UpdateInto("Role" ,new string[] { "name", "1v" , "exp"},new string[]{"'数据库'","1", "1.1"});
```



##### 预处理指令

以#关键字作为开头的语句

如unity提供的判断运行环境的

#if UNITY_EDITER

#elseif 

#endif

以及自定义预处理语句

#if QQ

#else if STEAM

用于对接不同平台发布的SDK

在Assets对应的Inspector面板下的Scripts Define Symbols进行配置





##### Android端使用数据库

使用预处理指令，把数据库发在持久化文件下，在移动端判断是否存在数据库，不存在则使用UnityWebRequire类拷贝数据库到移动端。



##### 数据存储选择

txt	存放一些不重要的数据，如

xml	一些小项目选择存放数据的方式，如跑酷类

db	数据量比较多，可加密（查看官方文档）





##### 对接Android SDK

P715

Eclipse

在设置中指定SDK路径：Windows/Preferences/Android/SDK Location

新建一个其他类型工程：File/New/Other

选择工程类型：Android/Android Application Project

编辑新项目信息：

Application Name：一般采用签名的最后部分（项目名

Project Name：同上

Package Name ：必须和Unity中的签名保持一致（Bundle Identifier

Required SDK：最小支持安卓版本（超出版本可能会有问题

Target SDK：最大支持安卓版本

Compile With：安卓编译平台

Theme：无（因为没有安卓显示需求

下一步：选择默认值

下一步修改图标：选择默认值

Create Activity：选中，选择Blank Activity或者Empty Activity（根据不同版本的eclipse选择）

下一步：点击finish

判断是否可用：展开src文件夹，如果其中什么内容都没有，则不可用。删除原安装包。切换最后一步的Blank Activity或Empty Activity

如果src文件下有代码，即可用：包名/MainActivity.java



XX\Unity\Editor\Data\PlaybackEngines\AndroidPlayer\Variations\mono\Release\Classes

文件夹下会有个.jar包,拖拽并选择Copy files到安卓工程的libs文件夹下

右键选择改.jar包Build Path/Add to Build Path

如果安卓工程的根目录下出现了classes.jar这个包,则说明成功了



MainActivity.java文件中,删除两个view相关的import

import com.unity3d.player.UnityPlayerActivity

大家注意，新版Unity的这个类要去根目录下搜类名

原来extends Activity,改为继承UnityPlayerActivity

注释掉第二行的带view的方法



在unity Project面板,

1.取消自动build的勾选:Build Automatically

2.properties中选择Android,勾选is Library

3.点击Clean,默认选项点击OK

4.点击Build Project



进入安卓工程      工作区/工程名/bin/

复制  工程名.jar与AndroidManifest.xml

复制 根目录下的res文件夹



打开unity,在Assets下建一个新目录:Plugins/Android,拷贝上面两个文件以及res文件夹



调用安卓SDK:

前两行代码固定:

```C#
AndroidJavaClass jc = new AndroidJavaclass("com.unity3d.player.UnityPlayer" );
AndroidJavaobject jo = jc.Getstatic<Androidjavaobject>("currentActivity");
num = jo.call<int>("GetInt"); // 调用安卓中的方法
```



问题排查:安卓的发布设置中在build中点击出inspect面板

参数得和安卓ADK对上,

Android TV Compatibility;Android Game都需要勾选上



##### 异步加载场景不会,但是异步累加的场景会让unity的默认寻路失效



##### 切换画质的选项

Edit/Project Settings/Editor

##### 限制游戏帧率

Application.targetFrameRate



##### GameMain物体

控制游戏流程等,全程不销毁

```C#
private IEnumerator Start(){
	//限制游戏帧率
	Application.targetFrameRate = 45;
	//读取配置文件
	Configuration.LoadConfig(config);
	while (!configuration.IsDone)
		yield return null;
	DontDestroyonLoad(gameobject);
	//加载场景
}
```

##### 查看帧率

游戏面板中的不准确,使用FPSCalc这个脚本

切换unity版本时候,只需要导入Assets文件夹,其他文件夹(Library,ProjectSetting等)都和unity配置有关,所以切换版本的时候会出现各种错误.



##### 更新方式

1.全部更新

2.热更新

unity热更新只支持更新资源文件类(如配置文件等),所以推荐一些可能的改动点包装成配置文件,方便热更新,而不是整个打包更新



##### 游戏存档

进度,角色数据分开不同的数据库表存取



##### Animation Type

一般选择Generic,Humanoid可能会无法满足差异化需求



##### 脚本执行顺序优先级

打开任意一个脚本,在inspector面板中,点击Execution Order,数值越小优先级越高



##### 选择在过渡场景中进行一些资源的处理,如全局的单例对象加载等



##### 导出包的时候只导出资源类资源,像一些配置类的取消导出



##### Animator系统特殊参数

Entry 初始状态

Any State 任意状态,可以切换死亡等

default 默认状态

Exit

Has Exit Time可以使用来做攻击后摇等



##### 特效生成

在任务模型中添加一个空物体,根据需要生成特效的位置改动空物体的位置



##### 长时间在内存中驻留的数据是不安全的,如单例类的数据,玩家可以通过内存修改的方式修改内存中的数据,可以在使用游戏数值的时候去数据库中重新获取数据.



##### HUD组件

制作血条



##### [MenuItem("URL/功能名")]

static function

在编辑器中点击这个菜单项就会执行下面的static函数



##### meta文件(多人协作项目才用得上)

Edit/ProjectSetting/Editor

在Inspector面板中Version Control确保选择的是Visible Meta Files(或者在文件夹中显示隐藏文件)

在拷贝给其他人Assets下的文件时,把对应的meta文件也拷贝过去

meta文件记录的都是资源,文件夹/脚本/插件/图片等都算资源,每在Assets中生成一份资源,就会同时生成一个meta文件

大部分meta文件大小都在1kb左右,内部内容很少,其中有一个guid相关的,记录索引相关



##### 协程

P691