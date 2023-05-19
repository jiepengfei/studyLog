Tips

1.

如果有多个对话框的需求

如果这些对话框的行为相同,使用一个Window,对话框视为交互元素

行为不同做多个WIndow

2.

##### 使用方法

UIManager.Instance.GetWindow<窗口类型>().方法();



##### UI结构

根物体  (空物体,取名UI,管理下面所有UI) UIManager

​	窗口   XXXUIWindow:UIWindow

​		交互元素

根物体（UI）挂载UIManager脚本
窗口挂载XXXWindow继承UIWindow
交互元素挂载UIEventListener

##### 核心类

###### UIWindow

所有UI窗口的基类，可以代表所有窗口（概念继承，以层次化方式管理类);定义所有窗口共有行为(显隐) // 概念上的复用排在前,代码上的复用排在后



tips:

通过设置Alpha通道值来控制显隐,而不是使用禁用启用组件

但是一个一个设置Alpha值显然不合适

Unity提供了Canvas Group组件,控制一组UI的显隐(挂载在窗口元素上)

```C#
namespace VR(类型).UGUI(基于UGUI).Framework(框架)
{
    /// <summary>
    /// UI窗口基类∶定义所有窗口共有成员(显隐)
    ///	</summary>
    public class UIWindow : MonoBehaviour
    {
        private CanvasGroup canvasGroup;

        private void Awake()
        {
            canvasGroup = GetComponent<CanvasGroup>();
        }

        /// <summary>
        /// 设置窗口可见性
        ///	</summary>
        /// <param name="state">显隐状态</param>
        /// <param name="delay">延迟时间</param>
        public void SetVisible(bool state, float delay=0){
            // 至少等待一帧,如有需求请写重载
            StartCoroutine(SetVisibleDelay(state, delay));
        }

        private IEnumerator SetVisibleDelay(bool state, float delay)
        {
            yield return new WaitForSeconds(delay);
            canvasGroup.alpha = state ? 1 : 0;
        }
    }
}
```





###### UIManager

管理(记录、禁用、查找)窗口

```C#
namespace VR(类型).UGUI(基于UGUI).Framework(框架)
{
    /// <summary>
    /// UI管理器:管理(记录/隐藏)所有窗口,提供查找UI窗口方法
    ///	</summary>
    public class UlManager : MonoSingleton<UIManager>
    {
        // key窗口对象名称value窗口对象引用
        private Dictionary<string, uIWindow> uiWindowDIC;
        
        public override void Init(){
            base.Init();
            
            // 下列代码建议提取到单独方法中
        	uiWindowDIC = new Dictionary<string, UIWindow>;
            UIWindow[] uiWindowArr = FindObjectsOfType<UIWindow>();
            for (int i = o; i < uiWindowArr.Length; i++)
            {
                // 初始隐藏所有窗口
                uiWindowArr[i].SetVisiable(false);
                // 记录窗口
                AddWindow(uiWindowArr[i]);
            }
        }
        /// <summary>
        /// 后续需要动态添加新窗口时使用
        ///	</summary>
        /// <param name=""Window">窗口对象</param>
        public void AddWindow(UIWindow window)
        {
        	uiWindowDIC.Add(window.GetType().Name, window);
        }
        /// <summary>
        /// 根据类型查找窗口的功能
        ///	</summary>
        /// <typeparam name=""T">需要查找的窗口类型</typeparam>
        /// <returns>指定类型的窗口对象</returns>
        public T GetWindow<T>() where T :class
        {
			string key = typeof(T).Name;
            if (LuiWindowDIC.ContainsKey(key)) return null;
            return uiWindowDIC[key] as T;
        }
    }
}
```



![image-20230516223712557](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20230516223712557.png)

##### 辅助类

###### UIMainWindow

附加到主窗口中，负责处理主窗口逻辑

```C#
namespace VR.UGUI
{
    public class UIMainWindow : UIWindow
    {
    }
}
```



###### GameController

负责处理游戏流程，如游戏开始时的UI显示

新建一个空物体名为GameController,脚本挂载给该物体

```C#
/// <summary>
/// 负责处理游戏流程，如游戏开始时的UI显示
///	</summary>

public class GameController : MonoBehaviour
{
    // 游戏开始前
    private void Start()
    {
        // 单例的使用方式范例
        // UIManager.Instance寻找单例对象
        // .Func()调用该单例类提供的方法
        // 显示主窗口
        UIManager.Instance.GetWindow<UIMainWindow>().SetVisible(true);
    }
}
```

