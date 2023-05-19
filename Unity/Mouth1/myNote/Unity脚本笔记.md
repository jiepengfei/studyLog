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

