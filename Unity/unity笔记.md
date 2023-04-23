## unity入门

#### 面板介绍

![](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220321202437188.png)

##### Project 项目资源面板

```
存放游戏的所有资源
与项目中资源文件夹Assets对应，例如场景、脚本、模型、音频、图片等文件。
```

##### Hierarchy 层次面板

```
显示当前场景中所有游戏对象的层级关系。
包含了当前场景的游戏对象 (GameObject)，其中一些是资源文件的实例，如3D模型和其他预制组件的实例。
```

##### Scene 场景面板

```
提供设计游戏界面的可视化面板

```

##### Game 游戏面板

```
预览游戏运行后的界面
```

##### Inspector 检视面板

```
·显示当前选定游戏对象附加的组件及其属性信息。
·为重要游戏物体选择图标:
```

#### 常用快捷键

```
1.按下鼠标滚轮拖动场景，滑动滚轮缩放场景。
2.鼠标右键旋转场景，点击”小手图标”后，通过左键移动场景。
3.点击右键同时按下W/S/A/D/Q/E键可实现场景漫游。
4.在Scene面板选中物体后按F键，或在Hierarchy面板双击物体，可将物体设置为场景视图的中心。
5.按住alt键同时通过鼠标左键围绕某物体旋转场景，鼠标右键缩放场景。
```

##### 变换工具

![](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220321203339504.png)

##### 顶点吸附

```
选择物体按住V键，确定顶点后再拖拽到目标物体的某个顶点上。
```

##### 变换切换



![](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220331220516972.png)

##### 播放控件



![](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220331220733494.png)

##### 视图



![](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220331220809126.png)

#### 材质

##### 纹理、着色器与材质的关系

![image-20220331220928094](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220331220928094.png)



##### 物理着色器

基于物理特性的Shader是Unity 5.x的重大革新之一，所谓物理着色器(Physically Based Shading,PBS)就是遵从物理学的能量守恒定律，可以创建出在不同光照环境下都接近真实的效果。



##### 属性

###### 渲染模式

```
Opaque 不透明，默认选项。
Transparent 透明，用于半透明和全透明物体，如玻璃。
Cutout 镂空，用于完全透明或完全不透明物体，如栅栏。
Fade 渐变，用于需要淡入淡出的物体。
```

```
Albedo基础贴图:决定物体表面纹理与颜色。

Metallic 金属∶使用金属特性模拟外观。

Specular 镜面反射:使用镜面特性模拟外观。

Smoothness光滑度∶设置物体表面光滑程度。

Normal Map法线贴图:描述物体表面凹凸程度。

Emission自发光∶控制物体表面自发光颜色和贴图。

    -- None 不影响环境

    -- Realtime 实时动态改变

    -- Backed烘焙生效

Tiling 平铺:沿着不同的轴，纹理平铺个数。

Offset偏移∶滑动纹理。
```



#### 摄像机组件

##### Transform

同普通物体一样，提供变化组件功能。

##### Camera属性

```
Clear Flags 清除标识：决定屏幕空白部分如何处理
选项：
	Skybox 天空盒：空白部分显示天空盒图案。
	Solid Color 纯色：空白部分显示背景颜色。
	Depth Only 仅深度:画中画效果时，小画面摄像机选择该项可清除屏幕空部分信息只保留物体颜色信息。
	Don't Clear不清除︰不清除任何颜色或深度缓存。

Background 背景：所有元素绘制后，没有天空盒的情况下，剩余屏幕的颜色。

Culling Mask 选择遮蔽层：选择要照射的层Layer。

Projection 投射方式:
    Perspective透视:透视图，物体具有近大远小效果。
    Orthographic正交:摄像机会均匀地渲染物体，没有透见感，通常小地图使用。

Size 大小(正交模式)︰摄影机视口的大小。

Field of view视野(透视模式)∶设置相机视野的远近距离。

Field of view 裁剪面︰相机到开始和结束渲染的距离：
	Near近:绘制的最近点。
	Far远:绘制的最远点。
	
Viewport Rect视口矩形:标明这台相机视图将会在屏幕上绘制的屏幕坐标。
	X:摄像机视图的开始水平位置。
	Y:摄像机视图的开始垂直位置。
	W宽度:摄像机输出在屏幕上的宽度。
	H高度:摄像机输出在屏幕上的高度。
	
Depth 深度︰相机在渲染顺序上的位置。具有较低深度的摄像机将在较高深度的摄像机之前渲染。
```



##### 天空盒 SkyBox

围绕整个场景的包装器，用于模拟天空的材质。（这是放在材质中的）

天空盒材质种类:6 Sided ，Procedural , Cubemap （很少用）。

###### 使用方式：

```
1. 摄像机添加组件SkyBox。
2. 光照窗口：
Window - rendering - Lighting - Environment -- Skybox可作为反射源将天空色彩反射到场景中物体。
（一般用第二种，因为更为真实）
```

###### 6 Sided 材质

属性：

​	Tint Color 色彩

​	Exposure 亮度

​	Rotation 旋转

其实就是用六张图去渲染立方体的六个面。

![image-20220414213010380](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220414213010380.png)



###### Procedural 材质

属性：

​	Sun 太阳模式

​		-- None 没有

​		-- Simple 简单

​		-- High Quality 高质量

​	Atmoshpere Thickness大气层厚度

​	Ground 地面颜色

​	如果为Environment Lighting的Sun属性设置一个平行光场景中会根据平行光角度自动创建太阳，并且位置随平行光旋转而改变。如果不设置，系统将默认选择场景中最亮的平行光。