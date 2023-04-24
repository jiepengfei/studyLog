#### Tips

左上角File==》Build Settings中是需要发布的场景列表，可以添加

协程在Update或OnGUI这类频繁执行的函数中使用会报错

##### 更改人物模型武器

修改武器的GameObject

更改武器网格形状Mesh

更改武器纹理图片Texture

##### 读取配置文件（StreamingAssets）路径

string configPath = Path.Combine(Application.streamingAssetsPath,"fileName.txt")

##### 寻路

新版本的自动寻路在Windows的Ai里而不是原来的Component

如果寻路物体形状奇怪，可以使用多个子物体拼凑一个大概的形状作为替代，原生的只有圆柱体或者正方体

Navigation中有三种选择

Nav Mesh Agent正常寻路

Off Mesh Link两个平面之间有间隔，可以使用这个连接，如连接河流两边的桥

Nav Mesh Obstacle动态寻路，如有带刚体的物体阻挡寻路物体，则会被阻拦，另寻路径

##### Characters/Import Package引入常用包，如常用的人物移动

##### 如果人物模型和动画不在同一个文件下，动画也需要设置为相同的animation type，动画才会正常运行

Inspector面板下Rig选项下的Animation Type有四种选项，None，Legacy对应animation组件，Generic对应animator组件且模型为非人型，Humanoid对应animator组件且模型为人型

Animator组件下，人物切换动画时rotate转动，可勾选Bake Into Pose解决

Animator组件下，人物切换动画时position变动，可勾选Bake Into Pose解决

##### unity中三种调用其他脚本函数的方法

第一种，被调用脚本函数为static类型，调用时直接用  脚本名.函数名()

第二种，GameObject.Find("脚本所在的物体的名字").SendMessage("函数名"); //能调用public和private类型函数

第三种，GameObject.Find("脚本所在的物体的名字").GetComponent<脚本名>().函数名(); //只能调用public类型函数

##### 根据gameObject获得里面的属性的值：

```
gameObject.GetComponent<脚本名字>().变量或者函数
```

根据gameObject修改里面的属性的值：

```
在这个gameObject提供一个方法然后用SendMessage调用

gameObject.SendMessage (方法，值);
```

#### 集合

一种数据容器，一种数据结构

容纳多个数据，大小可变，空间不一定连续

集合两大体系：非泛型集合，泛型集合

命名空间：

非泛型集合 System.Collections

泛型集合  System.Collections.Generic

非泛型缺点：

1. 性能不好，因为可能发生装箱。

2. 类型不安全，可能会发生类型转换的异常。

3. 使用不方便，用的时候需要手动做类型转换。

##### 列表

```
List<T>
```

##### 栈

```
Stack<T>
```

##### 队列

```
Queue<T>
```



#### 寻路





#### Mecanim动画系统

Animator























