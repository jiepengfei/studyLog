*C#的扩展方法:在不修改代码的情况下，为其增加新的功能*

但是还不会改变微软的数组类，为他增加新方法。

*三要素∶

*1.扩展方法所在的类必须是静态类

*2在第一个参数上，使用this关键字修饰被扩展的类型*3.在另一个命名空间下

*作用∶让调用者方便调用该方法

*(就好像是在调用自身的类型方法一样)*语法∶被扩展类型.方法名;

Tips

1.

如果有多个对话框的需求

如果这些对话框的行为相同,使用一个Window,对话框视为交互元素

行为不同做多个WIndow

2.

##### 使用方法

1.定义UIXXXWindow类，继承自UIWindow,负责处理该窗口逻辑

通过 GetUIEventListener方法获取需要交互的UI元素。

2.通过UIEventListener类提供的各种事件，完成交互行为。

3.通过UIManager 访问各个窗口。UIManager.Instance.GetWindow<窗口类型>().方法();



##### UI结构

根物体  (空物体,取名UI,管理下面所有UI) UIManager

​	窗口   			XXXUIWindow:UIWindow

​		交互元素 	UIEventListener

根物体（UI）挂载UIManager脚本
窗口挂载XXXWindow继承UIWindow
交互元素挂载UIEventListener

##### 核心类

###### UIWindow

所有UI窗口的基类，可以代表所有窗口（概念继承，以层次化方式管理类);定义所有窗口共有行为(显隐),获取监听器 // 概念上的复用排在前,代码上的复用排在后



tips:

通过设置Alpha通道值来控制显隐,而不是使用禁用启用组件

但是一个一个设置Alpha值显然不合适

Unity提供了Canvas Group组件,控制一组UI的显隐(挂载在窗口元素上)

```C#
using Common;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

/// <summary>
///
/// </summary>
namespace Card.UGUI.Framework
{
    /// <summary>
    /// UI窗口基类∶定义所有窗口共有成员(显隐)
    ///	</summary>
    public class UIWindow : MonoBehaviour
    {
        private CanvasGroup canvasGroup;
        private Dictionary<string, UIEventListener> uiEventDIC; // 缓存,以便于不用每次都去查找

        private void Awake()
        {
            canvasGroup = GetComponent<CanvasGroup>();
            uiEventDIC = new Dictionary<string, UIEventListener>();
        }

        /// <summary>
        /// 设置窗口可见性
        ///	</summary>
        /// <param name="state">显隐状态</param>
        /// <param name="delay">延迟时间</param>
        public void SetVisible(bool state, float delay = 0)
        {
            // 至少等待一帧,如有需求请写重载
            StartCoroutine(SetVisibleDelay(state, delay));
        }

        private IEnumerator SetVisibleDelay(bool state, float delay)
        {
            yield return new WaitForSeconds(delay);
            canvasGroup.alpha = state ? 1 : 0;
        }

        /// <summary>
        /// 根据子物体名称获取UI监听器
        ///	</summary>
        public UIEventListener GetUIEventListener(string name)
        {
            if (!uiEventDIC.ContainsKey(name))
            {
                print(name);
                // 这里可能会找不到,但是这个类调用到这里就是需要有个事件,所以在UIEventListener类中添加一个方法,保证必定有返回值,没有就新建再一个返回
                Transform tf = transform.FindChildByName(name);
                UIEventListener uiEvent = UIEventListener.GetListener(tf);
                uiEventDIC.Add(name, uiEvent);
            }
            return uiEventDIC[name];
        }
    }
}

```





###### UIManager

管理(记录、禁用、查找)窗口

```C#
using System.Collections.Generic;

namespace Card.UGUI.Framework
{
    /// <summary>
    /// UI管理器:管理(记录/隐藏)所有窗口,提供查找UI窗口方法
    ///	</summary>
    public class UIManager : MonoSingleton<UIManager>
    {
        // key窗口对象名称value窗口对象引用
        private Dictionary<string, UIWindow> uiWindowDIC;

        public override void Init()
        {
            base.Init();

            // 下列代码建议提取到单独方法中
            uiWindowDIC = new Dictionary<string, UIWindow>();
            UIWindow[] uiWindowArr = FindObjectsOfType<UIWindow>();
            for (int i = 0; i < uiWindowArr.Length; i++)
            {
                // 初始隐藏所有窗口
                uiWindowArr[i].SetVisible(false);
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
        public T GetWindow<T>() where T : class
        {
            string key = typeof(T).Name;
            if (!uiWindowDIC.ContainsKey(key)) return null;
            return uiWindowDIC[key] as T;
        }
    }
}
```



![image-20230516223712557](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20230516223712557.png)

###### UIEventListener

```C#
using UnityEngine;
using UnityEngine.EventSystems;

namespace Card.UGUI.Framework
{
    // 定义委托数据类型
    public delegate void PointerEventHandler(PointerEventData eventData);
    /// <summary>
    /// UI事件监听器∶管理所有UGU事件，提供事件参数类。附加到需要交互的UI元素上,用于监听用户操作
    ///	</summary>
    public class UIEventListener : MonoBehaviour, IPointerClickHandler, IPointerDownHandler, IPointerUpHandler
    // 这个类实现思想与EventTrigger类似,如果有需要添加的事件类型,可以参考该类继承的接口添加
    {
        // 声明事件
        public event PointerEventHandler PointerClick;
        public event PointerEventHandler PointerDown;
        public event PointerEventHandler PointerUp;

        /// <summary>
        /// 通过变换组件获取事件监听器
        ///	</summary>
        /// <param name=""tf"></param>
        /// <returns></returns>
        public static UIEventListener GetListener(Transform tf)
        {
            UIEventListener uiEventListener = tf.GetComponent<UIEventListener>();
            if (uiEventListener == null) uiEventListener = tf.gameObject.AddComponent<UIEventListener>();
            return uiEventListener;
        }

        // 继承接口
        public void OnPointerClick(PointerEventData eventData)
        {
            if (PointerClick != null) PointerClick(eventData);
        }
        public void OnPointerDown(PointerEventData eventData)
        {
            if (PointerDown != null) PointerDown(eventData);
        }
        public void OnPointerUp(PointerEventData eventData)
        {
            if (PointerUp != null) PointerUp(eventData);
        }
    }

}
```



##### 辅助类

###### UIMainWindow

附加到主窗口中，负责处理主窗口逻辑

```C#
using Card.UGUI.Framework;
using UnityEngine.EventSystems;

/// <summary>
///
/// </summary>
namespace Card.UGUI
{
    public class UIMainWindow : UIWindow
    {
        private void Start()
        {
            // 在开始时注册需要交互的元素事件
            // TransformHelper.FindChildByName(transform, "ButtonGameStart").GetComponent<Button>().onClick.AddListener(OnGameStartButtonClick);
            // 添加C#拓展方法后调用方式
            // transform.FindChildByName( "ButtonGameStart").GetComponent<Button>().Point.AddListener(OnGameStartButtonClick);
            // 定义事件监听类,提供所有UGUI事件(带事件参数类)
            // 因为该类事件会发生很多次,所以提取到UIWindow去实现
            // transform.FindChildByName( "ButtonGameStart").GetComponent<UIEventListener>().PointerClick += OnPointerClick;
            GetUIEventListener("ButtonGameStart").PointerClick += OnPointerClick;
        }

        private void OnPointerClick(PointerEventData eventData)
        {
            // 调用游戏开始方法
            GameController.Instance.GameStart();
        }
    }
}
```



###### GameController

负责处理游戏流程，如游戏开始时的UI显示

新建一个空物体名为GameController,脚本挂载给该物体

```C#
using Card.UGUI.Framework;
using Card.UGUI;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

/// <summary>
/// 负责处理游戏流程，如游戏开始时的UI显示
///	</summary>

public class GameController : MonoSingleton<GameController>
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

    public void GameStart()
    {
        print("youxikaishi1");
        UIManager.Instance.GetWindow<UIMainWindow>().SetVisible(false);
    }
}

```





一个面板下有多个功能按钮,如果这些按钮点击的效果需要交互,那么他们之间的数据通讯会很麻烦,所以在面板上处理逻辑,例:游戏主窗口类





##### 助手类

```c#
namespace Common
{
    /// <summary>
    /// 变换组件助手类
    /// </summary>
    public static class TransformHelper
    {
        /// <summary>
        /// 未知层级，查找后代指定名称的变换组件。
        /// </summary>
        /// <param name="currentTF">当前变换组件</param>
        /// <param name="childName">后代物体名称</param>
        public static Transform FindChildByName(this Transform currentTF, string childName)
        {
            // 递归∶方法内部又调用自身的过程。
            // 1.在子物体中查找
            Transform childTF = currentTF.Find(childName);
            if (childTF != null) return childTF;
            for (int i = 0; i < currentTF.childCount; i++)
            {
                // 2.将任务交给子物体
                childTF = FindChildByName(currentTF.GetChild(i) ,childName);
                if (childTF != null) return childTF;
            }
            return null;
        }
    }
}
```



类图

![image-20230520232451569](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20230520232451569.png)
