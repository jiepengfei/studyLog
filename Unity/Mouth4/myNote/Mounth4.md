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