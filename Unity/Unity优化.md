

unity优化



1.不使用或少使用动态光照，使用light mapping和light probes（光照探头)

2.不使用法线贴图（或者只在主角身上使用)。

3.不使用稠密的粒子

4.不使用fog

5．使用尽量少的material，使用尽量少的pass和render次数，如反射、阴影这些操作.

6.只使用mobile组里面的那些预置shader.

7.使用occlusion culling.

8.使用LOD.

9.远处的物体绘制在skybox 上。





##### CPU

Draw Call优化

DrawCall优化合并，即 DrawCall Batching. 

分为 Dynamic Batching和 Static Batching

之前讲过



##### 物理

1.真实的物理很消耗性能(因为会加载英伟达的物理引擎)，不要轻易使用，尽量使用自己的代码模仿假的物理(有条件可以一个简模一个精模)

2.不要使用mesh collider



物理效果.

1．设置一个合适的Fixed Timestep

2.使用层次而不是标签。我们可以轻松为对象分配层次和标签，并查询特定对象，但是涉及

碰撞逻辑时，层次至少在运行表现上会更有明显优势。更快的物理计算和更少的无用分配内

存是使用层次的基本原因。.





##### 顶点

优化几何体

使用LOD (Level of detail）技术

使用遮挡剔除（0cclusion culling）技术



注意是否有多余的动画脚本，模型自动导入到U3D会有动画脚本



每个角色尽量使用一个Skinned Mesh Renderer,这是因为当角色仅有一个Skinned MeshRenderer 时，Unity会使用可见性裁剪和包围体更新的方法来优化角色的运动,

而这种优化只有在角色仅含有一个Skinned Mesh Renderer 时才会启动。角色的面数一般不要超过1500，骨骼数量少于30就好，角色Material数量一般1~2个为最佳。。





##### 代码:

GC(Garbage Collection垃圾回收)

因为GC是CPU调度的。大量的调用GC确实可以回收内存，但如果内存占用量不是很大的情况下，调用GC的性价比就很低，因为GC对CPU的开销所造成的代价更大。所以优化GC，就是减少对GC 的调用。.

首先我们要明确所谓的GC是Mono运行时的机制，而非Unity3D游戏引擎的机制，.所以GC也主要是针对Mono的对象来说的，而它管理的也是Mono的托管堆。.

最好不用LINQ的命令，因为它们会分配临时的空间，同样也是GC收集的目标。





1.foreach。.

Mono下的foreach使用需谨慎。频繁调用容易触及堆上限，导致GC过早触发，出现卡顿现象。

特别注意的是在Update中如果非必要，不要使用foreach。尽可能用for来代替foreach使用

2.使用ObjectPool对象池来管理对象，避免频繁的Instance,Destroy。



##### GPU显存带宽



使用纹理图集（一张大贴图里包含了很多子贴图）来代替一系列单独的小贴图

使用光照纹理(lightmap)而非实时灯光。.

使用LOD，好处就是对那些离得远，看不清的物体的细节可以忽略。

遮挡剔除（Occlusion culling)



"Generate Mip Maps”会为同一张纹理创建出很多不同大小的小纹理，构成一个纹理金字塔。而在游戏中可以根据距离物体的远近，来动态选择使用哪一个纹理。这是因为，在距离物体很远的时候，就算我们使用了非常精细的纹理，但肉眼也是分辨不出来的，这种时候完全可以使用更小、更模糊的纹理来代替，而这大量可以节省访问的像素的数目。但它的缺点是，由于需要为每一个纹理建立一个图像金字塔，因此它会需要占用更多的内存。(点击随意一张图片,inspector中勾选Generate Mip Maps)

Max Size:决定了纹理的长宽值，如果我们使用的纹理本身超过了这个最大值，Unity会对其进行缩小来满足这个条件。这里再重复一点，**所有纹理的长宽比最好是正方形，而且长度值最好是2的整数幂**。这是因为有很多优化策略只有在这种时候才可以发挥最大效用。,

Format:负责纹理使用的压缩模式。

贴图压缩格式: ios 上尽量使用PVRTC，Android 上使用ETC.





##### 内存

1.场景切换时避开峰值。当前一个场景还未释放的时候，切换到新的场景。这时候由于两个内存叠加很容易达到内存峰值。解决方案是，在屏幕中间遮盖一个Loading场景。在旧的释放完，并且新的初始化结束后，施放Loading场景，使之有效的避开内存大量叠加超过峰值。



##### Unity3D代码优化

1、在使用数组时应当注意.

length = myArray. Length:

for(int i=0:i<length:i++)

{
}

避免每次访问数组长度

for(int i=0 ; i<myArray.Length: i++)

{

}

2、如果没有必要每帧都处理，则可以每隔几帧处理一次,以下案例每隔6帧执行一次方法调用

void Update ( )

{

​	if (Time.frameCount %6 == 0) 

​	{

​		DoSomethingo() ; 

​	} 

}



3、定时重复调用可以使用InvokeRepeating函数实现，比如，启动0.5秒后每隔1秒执行一次DoSomeThing函数: .

void Start() 

{

​	InvokeRepeating("DoSomeThing"，0.5f，1.0f); .

}

4、少使用临时变量，特别是在 Update OnGUI_等实时调用的函数

void Update()

{

​	Vector3 pos;

​	pos=transform. position; 

}

可以改为: 

private Vector3 pos;

void Update()

{

​	pos=transform. position;

}



5、优化数学运算，尽量避免使用float，而使用int，特别是在手机游戏中，尽量少用复杂的数学函数，比如 sin,cos等函数。改除法/为乘法,例如:使用x*0.5f而不是x/2.0f 。



6、删除空的Update方法。当通过Assets目录创建新的脚本时，脚本里会包括一个Update方法，当你不使用时删除它。



7、引用一个游戏对象的最合乎逻辑的组件。有人可能会这样写someGameObject.transform,

gameObject.rigidbody.transform.gameObject.rigidbody.transform，但是这样做了一些不必要的工作，你可以在最开始的地方引用它，像这样:。

Private Transform myTrans;

void Start ().

{

​	myTrans=transform; 

}

8、协程是一个好方法。可以使用协同程序来代替不必每帧都执行的方法。(还有InvokeRepeating_方法也是一个好的取代 Update的方法)。-

9、尽可能不要再Update或FixedUpdate中使用搜索方法（例如GameObject.Find)可以像前面那样在Start方法里获得它。。

10、不要使用SendMessage之类的方法，他比直接调用方法慢了100倍，你可以直接调用或通过C#的委托来实现。.