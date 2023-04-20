
# [***React框架***](https://react.docschina.org/)

## React的起源和发展  

    起初facebook在建设instagram（图片分享）的时候，因为牵扯到一个东西叫数据流，那为了处理数据流并且还要考虑好性能方面的问题，Facebook开始对市场上的各种前端MVC框架去进行一个研究，然而并没有看上眼的，于是Facebook觉得，还是自己开发一个才是最棒的，那么他们决定抛开很多所谓的“最佳实践”，重新思考前端界面的构建方式，他们就自己开发了一套，果然大牛创造力还是很强大的。

React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设Instagram 的网站。做出来以后，发现这套东西很好用，就在2013年5月开源了。





## React的出发点

    基于HTML的前端界面开发正变得越来越复杂，其本质问题基本都可以归结于如何将来自于服务器端或者用户输入的动态数据高效的反映到复杂的用户界面上。而来自Facebook的React框架正是完全面向此问题的一个解决方案，按官网描述，其出发点为：用于开发数据不断变化的大型应用程序（Building large applications with data that changes over time）。相比传统型的前端开发，React开辟了一个相当另类的途径，实现了前端界面的高性能高效率开发。



## React与传统MVC的关系

轻量级的视图层库！A JavaScript library for building user interfaces  

    React不是一个完整的MVC框架，最多可以认为是MVC中的V（View），甚至React并不非常认可MVC开发模式；React 构建页面 UI 的库。可以简单地理解为，React 将将界面分成了各个独立的小块，每一个块就是组件，这些组件之间可以组合、嵌套，就成了我们的页面。





## React高性能的体现：虚拟DOM

### React高性能的原理：

在Web开发中我们总需要将变化的数据实时反应到UI上，这时就需要对DOM进行操作。而复杂或频繁的DOM操作通常是性能瓶颈产生的原因（如何进行高性能的复杂DOM操作通常是衡量一个前端开发人员技能的重要指标）。

React为此引入了虚拟DOM（Virtual DOM）的机制：在浏览器端用Javascript实现了一套DOM API。基于React进行开发时所有的DOM构造都是通过虚拟DOM进行，每当数据变化时，React都会重新构建整个DOM树，然后React将当前整个DOM树和上一次的DOM树进行对比，得到DOM结构的区别，然后仅仅将需要变化的部分进行实际的浏览器DOM更新。而且React能够批处理虚拟DOM的刷新，在一个事件循环（Event Loop）内的两次数据变化会被合并，例如你连续的先将节点内容从A-B,B-A，React会认为A变成B，然后又从B变成A  UI不发生任何变化，而如果通过手动控制，这种逻辑通常是极其复杂的。

尽管每一次都需要构造完整的虚拟DOM树，但是因为虚拟DOM是内存数据，性能是极高的，部而对实际DOM进行操作的仅仅是Diff分，因而能达到提高性能的目的。这样，在保证性能的同时，开发者将不再需要关注某个数据的变化如何更新到一个或多个具体的DOM元素，而只需要关心在任意一个数据状态下，整个界面是如何Render的。

#### React Fiber: 17.0.2

在react 16之后发布的一种react 核心算法，**React Fiber是对核心算法的一次重新实现**(官网说法)。之前用的是diff算法。

**在之前React中，更新过程是同步的，这可能会导致性能问题。**

当React决定要加载或者更新组件树时，会做很多事，比如调用各个组件的生命周期函数，计算和比对Virtual DOM，最后更新DOM树，这整个过程是同步进行的，也就是说只要一个加载或者更新过程开始，中途不会中断。因为JavaScript单线程的特点，如果组件树很大的时候，每个同步任务耗时太长，就会出现卡顿。

React Fiber的方法其实很简单——分片。把一个耗时长的任务分成很多小片，每一个小片的运行时间很短，虽然总时间依然很长，但是在每个小片执行完之后，都给其他任务一个执行的机会，这样唯一的线程就不会被独占，其他任务依然有运行的机会。






## React的特点和优势

   **1.虚拟DOM  ==> 高性能**

我们以前操作dom的方式是通过document.getElementById()的方式，这样的过程实际上是先去读取html的dom结构，将结构转换成变量，再进行操作

而reactjs定义了一套变量形式的dom模型，一切操作和换算直接在变量中，这样减少了操作真实dom，性能真实相当的高，和主流MVC框架有本质的区别，并不和dom打交道

   **2.组件系统  ===> 高效率**

*react最核心的思想是将页面中任何一个区域或者元素都可以看做一个组件 component*

那么什么是组件呢？  

**组件指的就是同时包含了html、css、js、image元素的聚合体**

使用react开发的核心就是将页面拆分成若干个组件，并且react一个组件中同时耦合了css、js、image，这种模式整个颠覆了过去的传统的方式

   **3.单向数据流**  

其实reactjs的核心内容就是数据绑定，所谓数据绑定指的是只要将一些服务端的数据和前端页面绑定好，开发者只关注实现业务就行了  

​    **4.JSX  语法**  

在vue中，我们使用render函数来构建组件的dom结构性能较高，因为省去了查找和编译模板的过程，但是在render中利用createElement创建结构的时候代码可读性较低，较为复杂，此时可以利用jsx语法来在render中创建dom，解决这个问题，但是前提是需要使用工具来编译jsx





## 构建React简易环境

react开发需要引入多个依赖文件：react.js、react-dom.js，分别又有开发版本和生产版本

react.js中有React对象，帮助我们创建组件等功能

react-dom.js中有ReactDOM对象，渲染组件的虚拟dom为真实dom的爆发功能

在编写react代码的时候会大量的使用到jsx代码，但是需要编译：

1. 浏览器端编译，通过引入browser、babel等对引入的script内的代码做编译 -- 浏览器  
2. 利用webpack等开发环境进行编译，将编译好的文件引入到应用中

```javascript
    <!--引入react的核心包-->
    <script src="./js/react.development.js"></script>
    <!--引入开发web的包-->
    <script src="./js/react-dom.development.js"></script>
    <!--引入解析jsx的包-->
    <script src="./js/babel.js"></script>
    
    <script type="text/babel">
    	ReactDOM.render(<h2>hello world</h2>,
           document.getElementById("box"))
    </script>
```





## 元素与组件

如果代码多了之后，不可能一直在render方法里写，所以就需要把里面的代码提出来，定义一个变量，像这样：

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
// 这里感觉又不习惯了？这是在用JSX定义一下react元素
const app = <h1>欢迎进入React的世界</h1>
ReactDOM.render(
  app,
  document.getElementById('root')
)
```





## 函数式组件

这里我们定义的方法实际上也是react定义组件的第一种方式-定义函数式组件，这也是无状态组件。

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
/*
const 组件名(首字母大写)=（props）=>{
	return jsx表达式             
}
*/
const App = (props) => {
    return (
    	<h1>欢迎进入{props.name}的世界</h1>
    )
}

ReactDOM.render(
  // React组件的调用方式
  <App name={"react"} />,
  document.getElementById('root')
)
```

这样一个完整的函数式组件就定义好了。但要**注意！注意！注意！**组件名必须**大写**，否则报错。





## class组件

ES6的加入让JavaScript直接支持使用class来定义一个类，react的第二种创建组件的方式就是使用的类的继承`ES6 class`是目前官方推荐的使用方式，它使用了ES6标准语法来构建，看以下代码：

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

/*
class 组件名  extends  React.Component {
	render(){ //render是必不可少的钩子函数
		return jsx表达式
	}
}
*/

class App extends React.Component {
  render () {
    return (
      // 注意这里得用this.props.name, 必须用this.props
      <h1>欢迎进入{this.props.name}的世界</h1>
  	)
  }
}
ReactDOM.render(
  <App name="react" />,
  document.getElementById('root')
)
```



> 更老的一种方法：

在15.x的版本只能这样创建组件, 但现在的项目基本上不用

```jsx
React.createClass({
  getInitialState(){ //定义组件初始化状态
      
  },
  getDefaultProps(){ //定义组件的默认属性
      
  },
  render () {
    return (
      <div>hello world</div>
  	)
  }
})
```





## 组件的组合、嵌套

将一个组件渲染到某一个节点里的时候，会将这个节点里原有内容覆盖

组件嵌套的方式就是将子组件写入到父组件的模板中去，且react没有Vue中的内容分发机制（slot），所以我们在一个组件的模板中只能看到父子关系

```jsx
// 从 react 的包当中引入了 React 和 React.js 的组件父类 Component
// 还引入了一个React.js里的一种特殊的组件 Fragment
import React, { Component, Fragment } from 'react'
import ReactDOM from 'react-dom'

class Title extends Component {
  render () {
    return (
      <h1>欢迎进入React的世界</h1>
  	)
  }
}
class Content extends Component {
  render () {
    return (
      <p>React.js是一个构建UI的库</p>
  	)
  }
}
/** 由于每个React组件只能有一个根节点，所以要渲染多个组件的时候，需要在最外层包一个容器，如果使用div, 会生成多余的一层dom
class App extends Component {
  render () {
    return (
    	<div>
    		<Title />
        	<Content />
      	</div>
  	)
  }
}
**/
// 如果不想生成多余的一层dom可以使用React提供的Fragment组件在最外层进行包裹
class App extends Component {
  render () {
    return (
      <Fragment>
      	<Title />
        <Content />
      </Fragment>
  	)
  }
}
ReactDOM.render(
  <App/>,
  document.getElementById('root')
)
```





## JSX语法糖

JSX是一种语法糖，全称：javascript xml

JSX语法不是必须使用的，但是因为使用了JSX语法之后会降低我们的开发难度，故而这样的语法又被成为语法糖。

看下面的DOM结构：

```html
<div class='app' id='appRoot'>
  <h1 class='title'>欢迎进入React的世界</h1>
  <p>
    React.js 是一个帮助你构建页面 UI 的库
  </p>
</div>
```

上面这个 HTML 所有的信息我们都可以用 JavaScript 对象来表示：

```js
{
  tag: 'div',
  attrs: { className: 'app', id: 'appRoot'},
  children: [
    {
      tag: 'h1',
      attrs: { className: 'title' },
      children: ['欢迎进入React的世界']
    },
    {
      tag: 'p',
      attrs: null,
      children: ['React.js 是一个构建页面 UI 的库']
    }
  ]
}
```

但是用 JavaScript 写起来太长了，结构看起来又不清晰，用 XML的方式写起来就方便很多了。

于是 React.js 就把 JavaScript 的语法扩展了一下，**让 JavaScript 语言能够支持这种直接在 JavaScript 代码里面编写类似 XML 标签结构的语法，这样写起来就方便很多了**。**编译的过程会把类似 XML 的 JSX 结构转换成 JavaScript 的对象结构**。

下面代码:

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

class App extends React.Component {
  render () {
    return (
      <div className='app' id='appRoot'>
        <h1 className='title'>欢迎进入React的世界</h1>
        <p>
          React.js 是一个构建页面 UI 的库
        </p>
      </div>
    )
  }
}

ReactDOM.render(
	<App />,
  document.getElementById('root')
)
```

编译之后将得到这样的代码:

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

class App extends React.Component {
  render () {
    return (
      React.createElement(
        "div",
        {
          className: 'app',
          id: 'appRoot'
        },
        React.createElement(
          "h1",
          { className: 'title' },
          "欢迎进入React的世界"
        ),
        React.createElement(
          "p",
          null,
          "React.js 是一个构建页面 UI 的库"
        )
      )
    )
  }
}

ReactDOM.render(
	React.createElement(App),
  document.getElementById('root')
)
```

**`React.createElement` 会构建一个 JavaScript 对象来描述你 XML 结构的信息，包括标签名、属性、还有子元素等, 语法为**

```jsx
React.createElement(
  type,
  [props],
  [...children]
)
```



在不使用JSX的时候，需要使用React.createElement来创建组件的dom结构，但是这样的写法虽然不需要编译，但是维护和开发的难度很高，且可读性很差



所谓的 JSX 其实就是 JavaScript 对象，所以使用 React 和 JSX 的时候一定要经过编译的过程:

> JSX代码 — > 使用react构造组件，bable进行编译—> JavaScript对象 — `ReactDOM.render()函数进行渲染`—>真实DOM元素 —>插入页面



另：

- JSX就是在js中使用的xml，但是，这里的xml不是真正的xml，只能借鉴了一些xml的语法，例如：


最外层必须有根节点、标签必须闭合

- jsx借鉴xml的语法而不是html的语法原因：xml要比html严谨，编译更方便
- react中jsx里的注释要写成{/*  */}的方式





## 组件dom添加样式

- 行内样式

想给虚拟dom添加行内样式，需要使用表达式传入样式对象的方式来实现：

```jsx
// 注意这里的两个括号，第一个表示我们在要JSX里插入JS了，第二个是对象的括号
 <p style={{color:'red', fontSize:'14px'}}>Hello world</p>
```

- 使用`class`

React推荐我们使用行内样式，因为React觉得每一个组件都是一个独立的整体

其实我们大多数情况下还是大量的在为元素添加类名，但是需要注意的是，`class`需要写成`className`（因为毕竟是在写类js代码，会收到js规则的现在，而`class`是关键字）

```jsx
<p className="hello" style = {this.style}>Hello world</p>
```





## React Event

在react中，我们想要给组件的dom添加事件的话，也是需要在行内添加的方式，事件名字需要写成小驼峰的方式，值利用表达式传入一个函数即可。（原生的事件全是小写`onclick`, React里的事件是驼峰`onClick`）

注意，在没有渲染的时候，页面中没有真实dom，所以是获取不到dom的

给虚拟dom结构中的节点添加样式。在行内添加,写成驼峰形式，值是一个函数名，需要用 { } 包裹

```js
class App extends React.Component {
	handleClick(){
		alert(1)
	}
    render () {
        return (
                <div className='app' id='appRoot'>
                    <h1 className='title'>欢迎进入React的世界</h1>
                    <p onClick={this.handleClick}>
                    	React.js 是一个构建页面 UI 的库
                    </p>
                </div>
            )
        }
}
ReactDOM.render(<App/>,document.getElementById("box"))
```





## jsx中数组的遍历操作

```js
//vue的模板中遍历数组 ==> <li v-for="item in arr">{{item}}</li>
//遍历数组  arr.map
//为什么加key?
//key 帮助 React 识别哪些元素改变了，比如被添加或删除。
//因此你应当给数组中的每一个元素赋予一个确定的标识。
var arr = ["aa","bb","cc"]
ReactDOM.render(
    <div>
        {
            arr.map((item,index)=>{
            	return <p key={index}>{item}</p>
            })
        }
	</div>,
document.querySelector("#box"))
```





## React的ref形式



字符串的ref形式是不推荐的！[官网已经说过时了](https://reactjs.bootcss.com/docs/refs-and-the-dom.html)



### callback形式

第一种方式通过callback方式进行绑定！

```javascript
    class App extends React.Component{

      componentDidMount(){
        this.textInput.focus()
      }

      render(){
        return (
          <div>
            <input ref={el=>this.textInput = el}/>  
          </div>
        )
      }
    }

    ReactDOM.render(<App/>,document.getElementById('root'))
```



### createRef形式

```javascript
   class App extends React.Component{
      constructor(){
        super()  //相当于调用了父类的空的构造函数
        this.myRef = React.createRef(); //第一步创建ref的引用
      }

      componentDidMount(){
        //第三步：一定要通过current属性才可以获取到ref标记的元素对象本身
        // console.log(this.myRef)
        this.myRef.current.focus()
      }

      render(){
        return (
          <div>
            {/* 第二步：组件或者dom元素通过ref={this.myRef}建立关联 */}
            <input ref={this.myRef} />
          </div>
        )
      }
    }

    ReactDOM.render(<App/>,document.getElementById('root'))
```



### useRef[形式](https://reactjs.bootcss.com/docs/hooks-reference.html#useref)

```javascript
    //16.8版本后引入react hooks 来去解决此类问题。(采用useRef这个Hook解决)
    //useEffect 这个hooks 代替类组件三个钩子函数   didmount didupdate willUnmount
    function App(){
      const inputEl = React.useRef(null);

      // const onButtonClick = ()=>{
      //   inputEl.current.focus();
      // }

      //只有初始化的时候才会执行此钩子函数
      React.useEffect(()=>{
        inputEl.current.focus();
      },[])


      return (
        <div>
          <input ref={inputEl}/>
          {/*<button onClick={onButtonClick}>Focus the input</button>*/}
        </div>
      )
    }

    ReactDOM.render(<App/>,document.getElementById('root'))
```








## React中的数据承载-Props/State

任意的视图变化都应该由数据来控制

React也是基于数据驱动(声明式)的框架，组件中必然需要承载一些数据，在react中起到这个作用的是属性和状态（props & state）

1. 属性（props）  在组件外部传入，或者内部设置，组件内部通过this.props获得

2. 状态（state）   在组件内部设置或者更改，组件内部通过this.state获得

### 属性(props)

属性一般是外部传入的，组件内部也可以通过一些方式来初始化的设置，**属性不能被组件自己更改**

属性是描述性质、特点的，**组件自己不能随意更改**

使组件拥有属性的方式：

#### 1、属性传递

传入数据的时候，除了字符串类型，其他的都应该包上表达式，但是为了规整，所有的数据传递，最好都包上{}

```js
import React, { Component, Fragment } from 'react'
import ReactDOM from 'react-dom'

class Title extends Component {
  render () {
    return (
  		<h1>欢迎进入{this.props.name}的世界</h1>
  	)
  }
}

const Content = (props) => {
  return (
    <p>{props.name}是一个构建UI的库</p>
  )
}

class App extends Component {
  render () {
    return (
  	  <div>
      	<Title name="React" />
        <Content name="React.js" />
      </div>
  	)
  }
}

ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```



#### 2、设置组件的默认props

```js
import React, { Component, Fragment } from 'react'
import ReactDOM from 'react-dom'

class Title extends Component {
  // 使用类创建的组件，直接在这里写static方法，创建defaultProps
  static defaultProps = {
    name: 'React'
  }
  render () {
    return (
  		<h1>欢迎进入{this.props.name}的世界</h1>
  	)
  }
}

const Content = (props) => {
  return (
    <p>{props.name}是一个构建UI的库</p>
  )
}

// 使用箭头函数创建的组件，需要在这个组件上直接写defaultProps属性
Content.defaultProps = {
  name: 'React.js'
}

class App extends Component {
  render () {
    return (
  		<Fragment>
        {/* 由于设置了defaultProps， 不传props也能正常运行，如果传递了就会覆盖defaultProps的值 */}
      	<Title />
        <Content />
      </Fragment>
  	)
  }
}

ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```





#### 3、props.children

我们知道使用组件的时候，可以嵌套。要在自定义组件的使用嵌套结构，就需要使用 `props.children` 。在实际的工作当中，我们几乎每天都需要用这种方式来编写组件。

```js
import React, { Component, Fragment } from 'react'
import ReactDOM from 'react-dom'

class Title extends Component {
  render () {
    return (
  		<h1>欢迎进入{this.props.children}的世界</h1>
  	)
  }
}

const Content = (props) => {
  return (
    <p>{props.children}</p>
  )
}

class App extends Component {
  render () {
    return (
  		<Fragment>
      	<Title>React</Title>
        <Content><i>React.js</i>是一个构建UI的库</Content>
      </Fragment>
  	)
  }
}

ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```



#### 4、使用prop-types检查props

React其实是为了构建大型应用程序而生, 在一个大型应用中，根本不知道别人使用你写的组件的时候会传入什么样的参数，有可能会造成应用程序运行不了，但是不报错。为了解决这个问题，React提供了一种机制，让写组件的人可以给组件的```props```设定参数检查

```js
import One from "./components/one"
class App extends Component{
  render(){
    let userArr = [
      {id:1,sex:"男"},
      {id:2,sex:"女"}
    ]
    return (
      <div>
        <One num={true} userArr={userArr}/>
      </div>
    )
  }
}
```

```js
//定义组件的默认属性
//优先级比较低 如果外部传入同名属性，就会将其覆盖掉
static defaultProps = {
	num:100
}

static propTypes = {  
    //限定外部传入的num属性可以是number/string/boolean类型的
    num: PropTypes.oneOfType([PropTypes.number,PropTypes.string,PropTypes.bool]),
    //规定了外部必须传入一个userArr的数组，结构是一个对象，
    //对象里面包含两个字段分别是id:number.isRequired,sex:string.isRequired
    userArr:PropTypes.arrayOf(PropTypes.shape({
        id:PropTypes.number.isRequired,
        sex:PropTypes.string.isRequired   
    })).isRequired
}
```









### 状态(state)

状态就是组件描述某种显示情况的数据，由组件自己设置和更改，也就是说由组件自己维护，使用状态的目的就是为了在不同的状态下使组件的显示不同(自己管理)

在组件中可以通过constructor构造函数来给组件挂载初始状态,在组件内部通过this.state获取

**this.props和this.state是纯js对象,在vue中，$data属性是利用Object.defineProperty处理过的，更改$data的数据的时候会触发数据的getter和setter，但是react中没有做这样的处理，如果直接更改的话，react是无法得知的，所以，需要使用特殊的更改状态的方法：**

**setState(params)**

**在setState中传入一个对象，就会将组件的状态中键值对的部分更改，还可以传入一个函数，这个回调函数必须返回像上面方式一样的一个对象，函数可以接收prevState和props**

```js
//1.
let doing = this.state.doing=='学习'?'玩游戏':'学习'
this.setState({doing})

//2.
this.setState((prevState,props)=>{
    return {
        doing:prevState.doing=='学习'?'玩游戏':'学习'
    }
})
```

#### `setState`有两个参数

第一个参数可以是对象，也可以是方法return一个对象，我们把这个参数叫做`updater`

- 参数是对象

  ```jsx
  let dos = this.state.doing==="学英语"?"玩游戏":"学英语";
  this.setState({
      doing:dos
  });
  ```

- 参数是方法

  ```jsx
  this.setState((prevSate,props)=>{
      return {
          doing:prevSate.doing==="学英语"?"玩游戏":"学英语"
      }
  });
  ```

  注意的是这个方法接收两个参数，第一个是上一次的state, 第二个是props

**`setState`是异步的，所以想要获取到最新的state，没有办法获取，就有了第二个参数，这是一个可选的回调函数**

```jsx
this.setState((prevSate,props)=>{
    return {
        doing:prevSate.doing==="学英语"?"玩游戏":"学英语"
    }
}, () => {
  console.log('回调里的',this.state.doing)  //获取更新后的值
})
console.log('setState外部的',this.state.doing) //还是之前没有更新的值
```





#### 两种setState的比较：

另外setState(stateChange[, callback])这种形式的更改状态，会将传入的对象浅层合并到新的 state 中，例如，调整购物车商品数：

```js
this.setState({quantity: 2})
```

这种形式的 `setState()` 是异步的，并且在同一周期内会对多个 `setState` 进行批处理。例如，如果在同一周期内多次设置商品数量增加，则相当于：

```js
Object.assign(
  previousState,
  {quantity: state.quantity + 1},
  {quantity: state.quantity + 1},
  ...
)
```

后调用的 `setState()` 将覆盖同一周期内先调用 `setState` 的值，因此商品数仅增加一次。如果后续状态取决于当前状态，我们建议使用 updater 函数的形式代替：

```js
this.setState((prevState,props) => {
  return {quantity: prevState.quantity + 1}; //连续执行多次获放入队列中一次执行
}[, callback]);
```





### 实现下拉菜单的方式

1. 通过数据来控制元素的行内样式中display的值，或者去控制类名

```js
<ul style={{display:isMenuShow?'block':'none'}}><li>国内新闻</li></ul>
...
<ul className={isMenuShow?'show':'hide'}><li>国内新闻</li></ul>
```

2. 根据数据控制是否渲染改节点、组件
```js
{
    isMenuShow?<ul><li>国内新闻</li></ul>:''
}
```
```js
{
   isMenuShow && <ul><li>国内新闻</li></ul>
}
```



   3.通过ref对dom、组件进行标记，在组件内部通过this.refs获取到之后，进行操作

```js
<ul ref='content'><li>国内新闻</li></ul>
...
this.refs.content.style.display = this.state.isMenuShow?'block':'none'
```



### 属性和状态的对比

相似点：都是纯js对象，都会触发render更新，都具有确定性（状态/属性相同，结果相同）

不同点： 

1. 属性能从父组件获取，状态不能
2. 属性可以由父组件修改，状态不能
3. 属性能在内部设置默认值，状态也可以
4. 属性不在组件内部修改，状态要改
5. 属性能设置子组件初始值，状态不可以
6. 属性可以修改子组件的值，状态不可以

`state` 的主要作用是用于组件保存、控制、修改自己的可变状态。**`state` 在组件内部初始化，可以被组件自身修改，而外部不能访问也不能修改**。你可以认为 `state` 是一个局部的、只能被组件自身控制的数据源。**`state` 中状态可以通过 `this.setState`方法进行更新，`setState` 会导致组件的重新渲染。**

`props` 的主要作用是让使用该组件的父组件可以传入参数来配置该组件。**它是外部传进来的配置参数，组件内部无法控制也无法修改**。除非外部组件主动传入新的 `props`，否则组件的 `props` 永远保持不变。



没有 `state` 的组件叫无状态组件（stateless component），设置了 state 的叫做有状态组件（stateful component）。因为状态会带来管理的复杂性，我们尽量多写无状态组件，尽量少写有状态的组件。这样会降低代码维护的难度，也会在一定程度上增强组件的可复用性。







## [受控组件与非受控组件](https://react.docschina.org/docs/forms.html)

表单元素它的值来自于state 这个组件就是受控组件，否则就是非受控组件



### 1、受控组件

> 受控组件：在HTML中，表单元素(input textarea select等)通常自己维护 state，并根据用户输入进行更新。而在 React 中，可变状态通常保存在组件的 state中，并且只能通过使用 [`setState()`](https://react.docschina.org/docs/react-component.html#setstate)来更新。
>
> 我们可以把两者结合起来，使 React 的 state 成为“唯一数据源”。渲染表单的 React 组件还控制着用户输入过程中表单发生的操作。被 React 以这种方式控制取值的表单输入元素就叫做“受控组件”。

```js
class App extends React.Component{
    constructor(props){
        super(props);
        this.state={
        	n:1
        }
    }
    change=(e)=>{
        this.setState({
        	n: e.target.value
        })
    }
    render(){
        return (
            <div>
            	<input value={this.state.n} onChange={this.change} />									{this.state.n}
            </div>
           )
     }
 }
 ReactDOM.render(<App />,document.getElementById("box"));
```

由于在表单元素上设置了 `value` 属性，因此显示的值将始终为 `this.state.value`，这使得 React 的 state 成为唯一数据源。由于 `handlechange` 在每次按键时都会执行并更新 React 的 state，因此显示的值将随着用户输入而更新。

对于受控组件来说，输入的值始终由 React 的 state 驱动。你也可以将 value 传递给其他 UI 元素，或者通过其他事件处理函数重置，但这意味着你需要编写更多的代码。



### 2、textarea 标签

在 HTML 中, `<textarea>` 元素通过其子元素定义其文本:

```
<textarea>
  你好， 这是在 text area 里的文本
</textarea>
```

而在 React 中，`<textarea>` 使用 `value` 属性代替。这样，可以使得使用 `<textarea>` 的表单和使用单行 input 的表单非常类似：

```javascript
class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: '请撰写一篇关于你喜欢的 DOM 元素的文章.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('提交的文章: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          文章:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="提交" />
      </form>
    );
  }
}
```

请注意，`this.state.value` 初始化于构造函数中，因此文本区域默认有初值。



### 3、select 标签

在 HTML 中，`<select>` 创建下拉列表标签。例如，如下 HTML 创建了水果相关的下拉列表：

```
<select>
  <option value="grapefruit">葡萄柚</option>
  <option value="lime">酸橙</option>
  <option selected value="coconut">椰子</option>
  <option value="mango">芒果</option>
</select>
```

请注意，由于 `selected` 属性的缘故，椰子选项默认被选中。React 并不会使用 `selected` 属性，而是在根 `select` 标签上使用 `value` 属性。这在受控组件中更便捷，因为您只需要在根标签中更新它。例如：

```javascript
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('你喜欢的风味是: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          选择你喜欢的风味:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">葡萄柚</option>
            <option value="lime">酸橙</option>
            <option value="coconut">椰子</option>
            <option value="mango">芒果</option>
          </select>
        </label>
        <input type="submit" value="提交" />
      </form>
    );
  }
}
```

总的来说，这使得, `<input type="text">`, `<textarea>` 和 `<select>`之类的标签都非常相似—它们都接受一个 `value` 属性，你可以使用它来实现受控组件。



### 4、处理多个输入

当需要处理多个 `input` 元素时，我们可以给每个元素添加 `name` 属性，并让处理函数根据 `event.target.name` 的值选择要执行的操作。

```javascript
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          参与:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          来宾人数:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```



### 5、文件 input 标签

在 HTML 中，`<input type="file">` 可以让用户选择一个或多个文件上传到服务器，或者通过使用 [File API](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications) 进行操作。

在 React 中，`<input type="file">` 始终是一个非受控组件，因为它的值只能由用户设置，而不能通过代码控制。

您应该使用 File API 与文件进行交互。下面的例子显示了如何创建一个 [DOM 节点的 ref](https://zh-hans.reactjs.org/docs/refs-and-the-dom.html) 从而在提交表单时获取文件的信息。

```javascript
class FileInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.fileInput = React.createRef();
  }
  handleSubmit(event) {
    event.preventDefault();
    alert(
      `Selected file - ${this.fileInput.current.files[0].name}`
    );
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Upload file:
          <input type="file" ref={this.fileInput} />
        </label>
        <br />
        <button type="submit">Submit</button>
      </form>
    );
  }
}

ReactDOM.render(
  <FileInput />,
  document.getElementById('root')
);
```

因为它的 value 只读，所以它是 React 中的一个非受控组件。



### 6、受控输入空值

在受控组件上指定 value 的 prop 会阻止用户更改输入。如果你指定了 value，但输入仍可编辑，则可能是你意外地将value 设置为 undefined 或 null。

下面的代码演示了这一点。（输入最初被锁定，但在短时间延迟后变为可编辑。）

```javascript
ReactDOM.render(<input value="hi" />, mountNode);

setTimeout(function() {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);
```

```js
componentDidMount(){
    setTimeout(() => {
        this.setState({ //受控组件没有写onChange压根输入框不能输入数据，但是如果还能，说明...
        	value:undefined
        })
    }, 2000);
}
```



### 7、非受控组件

> 在大多数情况下，我们推荐使用 [受控组件](https://zh-hans.reactjs.org/docs/forms.html#controlled-components) 来处理表单数据。在一个受控组件中，表单数据是由 React 组件来管理的。另一种替代方案是使用非受控组件，这时表单数据将交由 DOM 节点来处理。
>
> 要编写一个非受控组件，而不是为每个状态更新都编写数据处理函数，你可以 [使用 ref](https://zh-hans.reactjs.org/docs/refs-and-the-dom.html) 来从 DOM 节点中获取表单数据。
>
> 例如，下面的代码使用非受控组件接受一个表单的值：

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

因为非受控组件将真实数据储存在 DOM 节点中，所以在使用非受控组件时，有时候反而更容易同时集成 React 和非 React 代码。如果你不介意代码美观性，并且希望快速编写代码，使用非受控组件往往可以减少你的代码量。否则，你应该使用受控组件。



### 8、dangerouslySetInnerHTML

对于富文本创建的内容，后台拿到的数据是这样的：

```
content = "<p>React.js是一个构建UI的库</p>"
```

处于安全的原因，React当中所有表达式的内容会被转义，如果直接输入，标签会被当成文本。这时候就需要使用`dangerouslySetHTML`属性，它允许我们动态设置`innerHTML`

```js
import React, { Component } from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  constructor() {
    super()
    this.state = {
      content : "<p>React.js是一个构建UI的库</p>"
    }
  }
  render () {
    return (
  		<div
            // 注意这里是两个下下划线 __html
            dangerouslySetInnerHTML={{__html: this.state.content}}
      	/>
  	)
  }
}
ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```





## 组件通信

### **父组件与子组件通信**

- 父组件将自己的状态传递给子组件，子组件当做属性来接收，当父组件更改自己状态的时候，子组件接收到的属性就会发生改变

- 父组件利用`ref`对子组件做标记，通过调用子组件的方法以更改子组件的状态,也可以调用子组件的方法..

### **子组件与父组件通信**

- 父组件将自己的某个方法传递给子组件，在方法里可以做任意操作，比如可以更改状态，子组件通过`this.props`接收到父组件的方法后调用。

### **跨组件通信**

在react没有类似vue中的事件总线来解决这个问题，我们只能借助它们共同的父级组件来实现，将非父子关系转换成多维度的父子关系。react提供了`context` api来实现跨组件通信, React 16.3之后的`context`api较之前的好用。

> Context 提供了一个无需为每层组件手动添加 props，就能在组件树间进行数据传递的方法。

props单向数据流动：

![图片描述](https://segmentfault.com/img/bVblBU2?w=1564&h=808)



如果觉得Props传递数据很繁琐，可以采用context,进行跨组件传递数据

![图片描述](https://segmentfault.com/img/bVblB1c?w=1560&h=792)



实例，使用`context` 实现购物车中的加减功能

```jsx
// counterContext.js
import React, { Component, createContext } from 'react'

const {
  Provider,
  Consumer: CountConsumer
} = createContext()

class CountProvider extends Component {
  constructor () {
    super()
    this.state = {
      count: 1
    }
  }
  increaseCount = () => {
    this.setState({
      count: this.state.count + 1
    })
  }
  decreaseCount = () => {
    this.setState({
      count: this.state.count - 1
    })
  }
  render() {
    return (
      <Provider value={{
        count: this.state.count,
        increaseCount: this.increaseCount,
        decreaseCount: this.decreaseCount
      }}
      >
        {this.props.children}
      </Provider>
    )
  }
}

export {
  CountProvider,
  CountConsumer
}
```

```jsx
// 定义CountButton组件
const CountButton = (props) => {
  return (
    <CountConsumer>
      // consumer的children必须是一个方法
      {
        ({ increaseCount, decreaseCount }) => {
          const { type } = props
          const handleClick = type === 'increase' ? increaseCount : decreaseCount
          const btnText = type === 'increase' ? '+' : '-'
          return <button onClick={handleClick}>{btnText}</button>
        }
      }
    </CountConsumer>
  )
}
```

```jsx
// 定义count组件，用于显示数量
const Count = (prop) => {
  return (
    <CountConsumer>
      {
        ({ count }) => {
          return <span>{count}</span>
        }
      }
    </CountConsumer>
  )
}
```

```jsx
// 组合
class App extends Component {
  render () {
    return (
  		<CountProvider>
        <CountButton type='decrease' />
        <Count />
        <CountButton type='increase' />
      </CountProvider>
  	)
  }
}
```

> 复杂的非父子组件通信在react中很难处理，多组件间的数据共享也不好处理，在实际的工作中我们会使用flux、redux、mobx来实现





## 请求数据

### 请求本地数据：

```js
 componentDidMount(){
    // data.json文件需要放在public静态资源目录中才可以请求到
    axios.get('/data.json').then(res=>{
      console.log(res)
    })
  }
```





### 请求卖座数据：

```js
axios.get('https://m.maizuo.com/gateway?cityId=440300&pageNum=1&pageSize=10&type=1&k=5095611',{
      headers:{
        'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"15984753841366499679797249"}',
        'X-Host': 'mall.film-ticket.film.list'
      }
    }).then(res=>{
      console.log(res)
    })
```





### 请求自己的数据:

```js
 axios.get('http://47.96.0.211:9000/db/in_theaters').then(res=>{
      console.log(res)
    })
```

因为浏览器同源策略，所以报跨域问题。如何解决，前端代理解决。

nodemodules/react-scripts/config/webpackDevServer.config.js文件：

```js
proxy:{
      "/api":{
        target:'http://47.96.0.211:9000',
        changeOrigin:true,
        pathRewrite:{
          '^/api':''
        }
      }
    },
```

虽然可以，但是一旦后续重新安装新的模块的时候，yarn.lock文件就会检测nodemodules目录是否改动过，如果改动的话，重置。



所以，可以借助yarn eject将react-scripts这个里面的一些配置项进行抽离到根目录里面即可。

报错！ 原因是本地代码没有被远程管理，需要创建远程仓库进行管理

```
git config 用户名 邮箱

git add .
git commit -m 'first-commit'
git remote add origin git@gitee.com:jiahuajiaoyu/react-2008-pro.git
git push origin master

git branch
git checkout -b 'fixbug'
git checkout master
git merge fixbug
git branch -d 'fixbug'
```









## React生命周期



React中组件也有生命周期，也就是说也有很多钩子函数供我们使用, 组件的生命周期，我们会分为四个阶段，挂载、更新、卸载、错误处理

### 挂载阶段

当组件实例被创建并插入 DOM 中时，其生命周期调用顺序如下：

1. constructor() 

2. static getDerivedStateFromProps()

3. render() 

4. componentDidMount()

   ```
   注意:
   下述生命周期方法即将过时，在新代码中应该避免使用它们：
   UNSAFE_componentWillMount()
   ```

   

### 更新阶段

当组件的 props 或 state 发生变化时会触发更新。组件更新的生命周期调用顺序如下： 

1. static getDerivedStateFromProps()
2. shouldComponentUpdate() 
3. render() 
4. getSnapshotBeforeUpdate() 
5. componentDidUpdate()

```
注意:
下述方法即将过时，在新代码中应该避免使用它们：
UNSAFE_componentWillUpdate()
UNSAFE_componentWillReceiveProps()
```



### 卸载阶段

当组件从 DOM 中移除时会调用如下方法：

​	componentWillUnmount()





### 错误处理

当渲染过程，生命周期，或子组件的构造函数中抛出错误时，会调用如下方法：

1. static getDerivedStateFromError()
2. componentDidCatch()





### 各生命周期详解

#### 1.constructor(props)

**如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数。**

在 React 组件挂载之前，会调用它的构造函数。在为 React.Component 子类实现构造函数时，应在其他语句之前前调用 `super(props)`。否则，`this.props` 在构造函数中可能会出现未定义的 bug。

通常，在 React 中，构造函数仅用于以下两种情况：

- 通过给 `this.state` 赋值对象来初始化[内部 state](https://react.docschina.org/docs/state-and-lifecycle.html)。
- 为[事件处理函数](https://react.docschina.org/docs/handling-events.html)绑定实例

在 `constructor()` 函数中**不要调用 `setState()` 方法**。如果你的组件需要使用内部 state，请直接在构造函数中为 **`this.state` 赋值初始 state**：

```js
constructor(props) {
  super(props);
  // 不要在这里调用 this.setState()
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}
```

只能在构造函数中直接为 `this.state` 赋值。如需在其他方法中赋值，你应使用 `this.setState()` 替代。





#### 2.static getDerivedStateFromProps(nextProps, prevState)

要注意的是，React 16.3 的版本中 getDerivedStateFromProps 的触发范围是和 16.4^ 是不同的，主要区别是在 `setState` 和 `forceUpdate` 时会不会触发，具体可以看这个[生命全周期图](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/) 。

`getDerivedStateFromProps` 会在调用 render 方法之前调用，并且在初始挂载及后续更新时都会被调用。它应返回一个对象来更新 state，如果返回 null 则不更新任何内容。

如果是由于父组件的`props`更改，所带来的重新渲染，也会触发此方法。

当状态发生变化的时候，this.setState()的时候，此钩子函数同样也会执行。

之前这里都是使用`constructor`+`componentWillRecieveProps`完成相同的功能的



可能的使用场景有两个：

- 无条件的根据 prop 来更新内部 state，也就是只要有传入 prop 值， 就更新 state
- 只有 prop 值和 state 值不同时才更新 state 值。



```javascript
   class App extends React.Component{
      state = {
        color:'red',
        x:1
      }
      render(){
        return (
          <div>
            <Child color={this.state.color}/>  
          </div>
        )
      }
      componentDidMount(){
        setTimeout(() => {
          this.setState({color:'green'})
        }, 2000);
      }
    }

    
    class Child extends React.Component{
      state = {
        color:''
      }
      static getDerivedStateFromProps(nextProps,prevState){
        if(nextProps.color === prevState.color){
          return null
        }else {
          return {
            color:nextProps.color
          }
        }
      }
      render(){
        return (
          <div>
            child--{this.state.color}
          </div>
        )
      }
    }
    ReactDOM.render(<App/>,document.querySelector('#root'))
```



现在Child组件内部也要调用setState方法更改state，我们发现其实没有任何变化。

```js
 class App extends React.Component{
      state = {
        color:'red',
        x:1
      }
      render(){
        return (
          <div>
            <Child color={this.state.color}/>  
          </div>
        )
      }
      componentDidMount(){
        setTimeout(() => {
          this.setState({color:'green'})
        }, 2000);
      }
    }

    
    class Child extends React.Component{
      state = {
        color:''
      }
      static getDerivedStateFromProps(nextProps,prevState){
        if(nextProps.color === prevState.color){
          return null
        }else {
          return {
            color:nextProps.color
          }
        }
      }

	  componentDidMount(){ //发现没有任何变化！
        setTimeout(() => {
          this.setState({color:'blue'})
        }, 3000);
      }

      render(){
        return (
          <div>
            child--{this.state.color}
          </div>
        )
      }
    }
    ReactDOM.render(<App/>,document.querySelector('#root'))
```

这是使用这个生命周期的一个常见 bug。为什么会发生这个 bug 呢？在开头有说到，在 React 16.4^ 的版本中 `setState` 和 `forceUpdate` 也会触发这个生命周期。所以组件的内部 state 变化后，又会走 getDerivedStateFromProps 方法，并把 state 值更新为传入的 prop值。

接下里我们来修复这个bug。

```js
 class App extends React.Component{
      state = {
        color:'red',
        x:1
      }
      render(){
        return (
          <div>
            <Child color={this.state.color}/>  
          </div>
        )
      }
      componentDidMount(){
        setTimeout(() => {
          this.setState({color:'green'})
        }, 2000);
      }
    }

    
    class Child extends React.Component{
      state = {
        color:'',
        prevColor:''
      }
      static getDerivedStateFromProps(nextProps,prevState){
        if(nextProps.color === prevState.prevColor){
          return null
        }else {
          return {
            color:nextProps.color,
            prevColor:nextProps.color
          }
        }
      }

	  componentDidMount(){ 
        setTimeout(() => {
          this.setState({color:'blue'})
        }, 3000);
      }

      render(){
        return (
          <div>
            child--{this.state.color}
          </div>
        )
      }
    }
    ReactDOM.render(<App/>,document.querySelector('#root'))
```

通过保存一个之前 prop 值，我们就可以在只有 prop 变化时才去修改 state。这样就解决上述的问题。

这里小结下 getDerivedStateFromProps 方法使用的注意点：

- 在使用此生命周期时，要注意把传入的 prop 值和之前传入的 prop 进行比较。
- 因为这个生命周期是静态方法，同时要保持它是纯函数，不要产生副作用。



#### 3.render()

render()方法是必需的。当他被调用时，他将计算`this.props`和`this.state`，并返回以下一种类型： 

1. React元素。通过jsx创建，既可以是dom元素，也可以是用户自定义的组件。 
2. 字符串或数字。他们将会以文本节点形式渲染到dom中。 
3. Portals。react 16版本中提出的新的解决方案，可以使组件脱离父组件层级直接挂载在DOM树的任何位置。
4. null，什么也不渲染 
5. 布尔值。也是什么都不渲染。

如需与浏览器进行交互，请在 `componentDidMount()` 或其他生命周期方法中执行你的操作。保持 `render()` 为纯函数，可以使组件更容易思考。

```
注意:
如果 shouldComponentUpdate() 返回 false，则不会调用 render()。
```



#### 4. componentDidMount

`componentDidMount`在组件被装配后立即调用。初始化使得DOM节点应该进行到这里。

**通常在这里进行ajax请求**

如果要初始化第三方的dom库，也在这里进行初始化。只有到这里才能获取到真实的dom.



#### 5.shouldComponentUpdate(nextProps, nextState)

调用`shouldComponentUpdate`使React知道，组件的输出是否受`state`和`props`的影响。默认每个状态的更改都会重新渲染，大多数情况下应该保持这个默认行为。

在渲染新的`props`或`state`前，`shouldComponentUpdate`会被调用。**默认为`true`**。这个方法不会在初始化时被调用，也不会在`forceUpdate()`时被调用。返回`false`不会阻止子组件在`state`更改时重新渲染。

如果`shouldComponentUpdate()`返回`false`，`componentWillUpdate`,`render`和`componentDidUpdate`不会被调用。

```
此方法仅作为性能优化的方式而存在。不要企图依靠此方法来“阻止”渲染，因为这可能会产生 bug。你应该考虑使用内置的 PureComponent 组件，而不是手动编写 shouldComponentUpdate()。PureComponent 会对 props 和 state 进行浅层比较，并减少了跳过必要更新的可能性。
如果你一定要手动编写此函数，可以将 this.props 与 nextProps 以及 this.state 与nextState 进行比较，并返回 false 以告知 React 可以跳过更新。
```



#### 6.getSnapshotBeforeUpdate(prevProps, prevState)

在react `render()`后的输出被渲染到DOM之前被调用。它使您的组件能够在它们被潜在更改之前捕获当前值（如滚动位置）。这个生命周期返回的任何值都将作为参数传递给componentDidUpdate（）。



#### 7.componentDidUpdate(prevProps, prevState, snapshot)

`componentDidUpdate()` 会在更新后会被立即调用。首次渲染不会执行此方法。

当组件更新时，将此作为一个机会来操作DOM。只要您将当前的props与以前的props进行比较（例如，如果props没有改变，则可能不需要网络请求），这也是做网络请求的好地方。

```
componentDidUpdate(prevProps) {
  // 典型用法（不要忘记比较 props）：
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}
```

如果组件实现`getSnapshotBeforeUpdate()`生命周期，则它返回的值将作为第三个“快照”参数传递给`componentDidUpdate()`。否则，这个参数是`undefined`。

```
注意:
如果 shouldComponentUpdate() 返回值为 false，则不会调用 componentDidUpdate()。
```



#### 8.componentWillUnmount()

`componentWillUnmount()` 会在组件卸载及销毁之前直接调用。在此方法中执行必要的清理操作，例如，清除 timer，取消网络请求或清除在 `componentDidMount()` 中创建的订阅等。

`componentWillUnmount()` 中**不应调用 `setState()`**，因为该组件将永远不会重新渲染。组件实例卸载后，将永远不会再挂载它。



## HOC(高阶组件)

https://blog.csdn.net/weixin_34227447/article/details/87953929

Higher-Order Components就是一个函数，传给它一个组件，它返回一个新的组件。

```jsx
const NewComponent = hoc(YourComponent)
```

比如，我们想要我们的组件通过自动注入一个版权信息。

```jsx
// withCopyright.js 定义一个高阶组件
import React, { Component, Fragment } from 'react'

const withCopyright = (WrappedComponent) => {
  return class NewComponent extends Component {
    render() {
      return (
        <Fragment>
          <WrappedComponent {...this.props}/>
          <div>&copy;版权所有 千锋教育 2019 </div>
        </Fragment>
      )
    }
  }
}
export default withCopyright
```

```jsx
// 使用方式
import withCopyright from './withCopyright'

class App extends Component {
  render () {
    return (
  		<div>
        <h1>Awesome React</h1>
        <p>React.js是一个构建用户界面的库</p>
      </div>
  	)
  }
}
const CopyrightApp = withCopyright(App)
```

这样只要我们有需要用到版权信息的组件，都可以直接使用withCopyright这个高阶组件包裹即可。

在这里要讲解在CRA 中配置装饰器模式的支持。







### 对于CRA的定制

​	因为我们发现，调用高阶组件的时候采用withCopy(About)代码，但是不够简洁优雅。

​	那么我们可以采用装饰器的写法实现调用高阶组件

```js
@WithCopy
class About extends Component {
    render() {
        return (
            <div>
                about -- {this.props.a}
            </div>
        )
    }
}
```

很不幸，目前的cra是不支持这种写法，我们需要单独进行定制，让其支持这种写法。



[Antd中提供了社区解决方案](https://ant.design/docs/react/use-with-create-react-app-cn)

> yarn add @craco/craco

对脚手架进行轻微的调整

```js
"scripts": {
    "start": "craco start",
    "build": "craco build",
    "test": "craco test"
 },
```



yarn start启动项目发现报错了，原因是因为根路径下面缺少 craco.config.js文件

```js
/* craco.config.js */
module.exports = {
  // ...
};
```

   

启动yarn start，发现报错了！ 

> 错误： Cannot find module 'react-scripts/package.json'

> yarn  add  react-scripts



自定义主题的配置：

> yarn add antd

index.js文件中：

```
import 'antd/dist/antd.less';
```

​	

然后安装 `craco-less` 并修改 `craco.config.js` 文件如下。

> yarn add craco-less

```js
const CracoLessPlugin = require('craco-less');

module.exports = {
  plugins: [
    {
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: { '@primary-color': 'yellow' },
            javascriptEnabled: true,
          },
        },
      },
    },
  ],
};
```





[后续CRA支持装饰器需要这样配置](https://blog.csdn.net/lucky569/article/details/107253310/)：

> yarn add @babel/plugin-proposal-decorators

在craco.config.js文件中新增以下代码即可:

```js
babel: {
   plugins: [["@babel/plugin-proposal-decorators", { legacy: true }]]
},
```



其实就会发现 react面向社区化的。它把一些常用到的包都放在社区，用到的话单独去查找去进行相应的配置。

vue的话面向官方化，很多东西内部都帮助我们去实现了





## Portal

Portals 提供了一个最好的在父组件包含的DOM结构层级外的DOM节点渲染组件的方法。

```javascript
ReactDOM.createPortal(child,container);
```

第一个参数child是可渲染的react子项，比如元素，字符串或者片段等。第二个参数container是一个DOM元素。

### 1、用法

普通的组件，子组件的元素将挂载到父组件的DOM节点中。

```javascript
render() {
  // React 挂载一个div节点，并将子元素渲染在节点中
  return (
    <div>
      {this.props.children}
    </div>
  );
}
```

有时需要将元素渲染到DOM中的不同位置上去，这是就用到的portal的方法。

```javascript
render(){
    // 此时React不再创建div节点，而是将子元素渲染到Dom节点上。domNode，是一个有效的任意位置的dom节点。
    return ReactDOM.createPortal(
        this.props.children,
        domNode
    )
}
```

一个典型的用法就是当父组件的dom元素有 `overflow:hidden`或者`z-inde`样式，而你又需要显示的子元素超出父元素的盒子。举例来说，如对话框，悬浮框，和小提示。



### 2、在protal中的事件冒泡

虽然通过portal渲染的元素在父组件的盒子之外，但是渲染的dom节点仍在React的元素树上，在那个dom元素上的点击事件仍然能在dom树中监听到。

```react
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

const getDiv = () => {
    const div = document.createElement('div');
    document.body.appendChild(div);
    return div;
};

const withPortal = (WrappedComponent) => {
    class AddPortal extends Component {
        constructor(props) {
            super(props);
            this.el = getDiv();
        }

        componentWillUnmount() {
            document.body.removeChild(this.el);
        }

        render(props) {
            return ReactDOM.createPortal(<WrappedComponent {...props} />, this.el);
        }
    }
    return AddPortal;
};

class Modal extends Component {
    render() {
        return (
            <div>
                <div>amodal content</div>
                <button type="button">Click</button>
            </div>
        );
    }
}

const PortalModal = withPortal(Modal);

class Page extends Component {
    constructor(props) {
        super(props);
        this.state = { clicks: 0 };
        this.handleClick = this.handleClick.bind(this);
    }

    handleClick() {
        this.setState(state => ({
            clicks: state.clicks + 1
        }));
    }


    render() {
        return (
            <div onClick={this.handleClick}>
                <h3>ppppppppp</h3>
                <h3>num: {this.state.clicks}</h3>
                <PortalModal />
            </div>
        );
    }
}

export default Page;
```





## Redux 状态管理

### 1、传统MVC框架的缺陷

**什么是MVC？**

![](https://z3.ax1x.com/2021/04/08/cJKYTg.png)

`MVC`的全名是`Model View Controller`，是模型(model)－视图(view)－控制器(controller)的缩写，是一种软件设计典范。

`V`即View视图是指用户看到并与之交互的界面。

`M`即Model模型是管理数据 ，很多业务逻辑都在模型中完成。在MVC的三个部件中，模型拥有最多的处理任务。

`C`即Controller控制器是指控制器接受用户的输入并调用模型和视图去完成用户的需求，控制器本身不输出任何东西和做任何处理。它只是接收请求并决定调用哪个模型构件去处理请求，然后再确定用哪个视图来显示返回的数据。

**MVC只是看起来很美**

MVC框架的数据流很理想，请求先到Controller, 由Controller调用Model中的数据交给View进行渲染，但是在实际的项目中，又是允许Model和View直接通信的。然后就出现了这样的结果：

![](https://z3.ax1x.com/2021/04/08/cJKB60.md.png)

### 2、Flux

在2013年，Facebook让`React`亮相的同时推出了Flux框架，`React`的初衷实际上是用来替代`jQuery`的，`Flux`实际上就可以用来替代`Backbone.js`，`Ember.js`等一系列`MVC`架构的前端JS框架。

其实`Flux`在`React`里的应用就类似于`Vue`中的`Vuex`的作用，但是在`Vue`中，`Vue`是完整的`mvvm`框架，而`Vuex`只是一个全局的插件。

`React`只是一个MVC中的V(视图层)，只管页面中的渲染，一旦有数据管理的时候，`React`本身的能力就不足以支撑复杂组件结构的项目，在传统的`MVC`中，就需要用到Model和Controller。Facebook对于当时世面上的`MVC`框架并不满意，于是就有了`Flux`, 但`Flux`并不是一个`MVC`框架，他是一种新的思想。

![image-20190420012450223](https://z3.ax1x.com/2021/04/08/cJK67F.png)

- View： 视图层
- ActionCreator（动作创造者）：视图层发出的消息（比如mouseClick）
- Dispatcher（派发器）：用来接收Actions、执行回调函数
- Store（数据层）：用来存放应用的状态，一旦发生变动，就提醒Views要更新页面

Flux的流程：

1. 组件获取到store中保存的数据挂载在自己的状态上
2. 用户产生了操作，调用actions的方法
3. actions接收到了用户的操作，进行一系列的逻辑代码、异步操作
4. 然后actions会创建出对应的action，action带有标识性的属性
5. actions调用dispatcher的dispatch方法将action传递给dispatcher
6. dispatcher接收到action并根据标识信息判断之后，调用store的更改数据的方法
7. store的方法被调用后，更改状态，并触发自己的某一个事件
8. store更改状态后事件被触发，该事件的处理程序会通知view去获取最新的数据



### 3、Redux

React 只是 DOM 的一个抽象层，并不是 Web 应用的完整解决方案。有两个方面，它没涉及。

- 代码结构 
- 组件之间的通信

2013年 Facebook 提出了 Flux 架构的思想，引发了很多的实现。2015年，Redux 出现，将 Flux 与[函数式编程](<https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/>)结合一起，很短时间内就成为了最热门的前端架构。

如果你不知道是否需要 Redux，那就是不需要它

只有遇到 React 实在解决不了的问题，你才需要 Redux

简单说，如果你的UI层非常简单，没有很多互动，Redux 就是不必要的，用了反而增加复杂性。

- 用户的使用方式非常简单
- 用户之间没有协作
- 不需要与服务器大量交互，也没有使用 WebSocket
- 视图层（View）只从单一来源获取数据

**需要使用Redux的项目:**

- 用户的使用方式复杂
- 不同身份的用户有不同的使用方式（比如普通用户和管理员）
- 多个用户之间可以协作
- 与服务器大量交互，或者使用了WebSocket
- View要从多个来源获取数据

**从组件层面考虑，什么样子的需要Redux：**

- 某个组件的状态，需要共享
- 某个状态需要在任何地方都可以拿到
- 一个组件需要改变全局状态
- 一个组件需要改变另一个组件的状态

**Redux的设计思想：**

1. Web 应用是一个状态机，视图与状态是一一对应的。
2. 所有的状态，保存在一个对象里面（唯一数据源）。

> 注意：flux、redux都不是必须和react搭配使用的，因为flux和redux是完整的架构，在学习react的时候，只是将react的组件作为redux中的视图层去使用了。

**Redux的使用的三大原则：**

- Single Source of Truth(唯一的数据源)
- State is read-only(状态是只读的)
- Changes are made with pure function(数据的改变必须通过纯函数完成)



#### 自己实现Redux

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  
</head>
<body>
  
  <div id="root">
    <div class="counter">
      <span class="btn" onclick="store.dispatch({type: 'COUNT_DECREMENT', number: 10})">-</span>
      <span class="count" id="count"></span>
      <span class="btn" id="add" onclick="store.dispatch({type: 'COUNT_INCREMENT', number: 10})">+</span>
    </div>
  </div>
  <script type='text/javascript'>
    const createStore = (reducer) => {
      // 定义一个初始的state
      let state = null
      // getState用于获取状态
      const getState = () => state
      
      // 定义一个dispatch方法，让每次有action传入的时候返回reducer执行之后的结果
      const dispatch = (action) => {
        // 调用reducer来处理数据
        state = reducer(state, action)
      }
      //  初始化state
      dispatch({})

      return {
        getState,
        dispatch
      }
    }

    // 定义一个计数器的状态
    const countState = {
      count: 10
    }
    
    // 定一个方法叫changeState，用于处理state的数据，每次都返回一个新的状态
    const reducer = (state, action) => {
      // 如果state是null, 就返回countState
      if (!state) return countState
      switch(action.type) {
        // 处理减
        case 'COUNT_DECREMENT':
          return {
            ...state,
            count: state.count - action.number
          }
        // 处理加        
        case 'COUNT_INCREMENT':
          return {
            ...state,
            count: state.count + action.number
          }
        default:
          return state
      }
    }

    // 创建一个store
    const store = createStore(reducer)
    // 定义一个方法用于渲染计数器的dom
    const renderCount = () => {
      const countDom = document.querySelector('#count')
      countDom.innerHTML = store.getState().count
    }
    // 初次渲染数据
    renderCount()

  </script>
</body>
</html>
```



初始化数据渲染完成了，后续希望点击的时候界面可以渲染最新的count，需要用到发布订阅模式解决了。

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  
</head>
<body>
  
  <div id="root">
    <div class="counter">
      <span class="btn" onclick="store.dispatch({type: 'COUNT_DECREMENT', number: 10})">-</span>
      <span class="count" id="count"></span>
      <span class="btn" id="add" onclick="store.dispatch({type: 'COUNT_INCREMENT', number: 10})">+</span>
    </div>
  </div>
  <script type='text/javascript'>
    const createStore = (reducer) => {
      // 定义一个初始的state
      let state = null
      // getState用于获取状态
      const getState = () => state
      
      // 定义一个监听器，用于管理一些方法(方法的订阅)
      const listeners = []
      const subscribe = (listener) => listeners.push(listener)

      // 定义一个dispatch方法，让每次有action传入的时候返回reducer执行之后的结果
      const dispatch = (action) => {
        // 调用reducer来处理数据
        state = reducer(state, action)
        // 让监听器里的所有方法运行（方法的发布）
        listeners.forEach(listener => listener())
      }
      //  初始化state
      dispatch({})

      return {
        getState,
        dispatch,
        subscribe
      }
    }

    // 定义一个计数器的状态
    const countState = {
      count: 10
    }
    
    // 定一个方法叫changeState，用于处理state的数据，每次都返回一个新的状态
    const reducer = (state, action) => {
      // 如果state是null, 就返回countState
      if (!state) return countState
      switch(action.type) {
        // 处理减
        case 'COUNT_DECREMENT':
          return {
            ...state,
            count: state.count - action.number
          }
        // 处理加        
        case 'COUNT_INCREMENT':
          return {
            ...state,
            count: state.count + action.number
          }
        default:
          return state
      }
    }

    // 创建一个store
    const store = createStore(reducer)
    // 定义一个方法用于渲染计数器的dom
    const renderCount = () => {
      const countDom = document.querySelector('#count')
      countDom.innerHTML = store.getState().count
    }
    // 初次渲染数据
    renderCount()

    // 监听，只要有dispatch，renderCount就会自动运行
    store.subscribe(renderCount)

  </script>
</body>
</html>
```





#### 使用Redux框架

##### **Redux的流程：**

![image-20190420013410981](https://z3.ax1x.com/2021/04/08/cJMVcq.png)

![](https://s1.ax1x.com/2020/09/05/wEkeeK.jpg)

- store通过reducer创建了初始状态

- view通过store.getState()获取到了store中保存的state挂载在了自己的状态上

- 用户产生了操作，调用了actions 的方法

- actions的方法被调用，创建了带有标示性信息的action

- actions将action通过调用store.dispatch方法发送到了reducer中

- reducer接收到action并根据标识信息判断之后返回了新的state

- store的state被reducer更改为新state的时候，store.subscribe方法里的回调函数会执行，此时就可以通知view去重新获取state

  

##### **Reducer必须是一个纯函数：**

Reducer 函数最重要的特征是，它是一个纯函数。也就是说，只要是同样的输入，必定得到同样的输出。Reducer不是只有Redux里才有，之前学的数组方法`reduce`, 它的第一个参数就是一个reducer

**纯函数是函数式编程的概念，必须遵守以下一些约束。**

- 不得改写参数

- 不能调用系统 I/O 的API

- 不能调用Date.now()或者Math.random()等不纯的方法，因为每次会得到不一样的结果

由于 Reducer 是纯函数，就可以保证同样的State，必定得到同样的 View。但也正因为这一点，Reducer 函数里面不能改变 State，必须返回一个全新的对象，请参考下面的写法。

```js
// State 是一个对象
function reducer(state = defaultState, action) {
  return Object.assign({}, state, { thingToChange });
  // 或者
  return { ...state, ...newState };
}

// State 是一个数组
function reducer(state = defaultState, action) {
  return [...state, newItem];
}
```

最好把 State 对象设成只读。要得到新的 State，唯一办法就是生成一个新对象。这样的好处是，任何时候，与某个 View 对应的 State 总是一个不变(immutable)的对象。

我们可以通过在createStore中传入第二个参数来设置默认的state，但是这种形式只适合于只有一个reducer的时候。



##### **划分reducer**:

因为一个应用中只能有一个大的state，这样的话reducer中的代码将会特别特别的多，那么就可以使用combineReducers方法将已经分开的reducer合并到一起

> 注意：
>
> 1. 分离reducer的时候，每一个reducer维护的状态都应该不同
> 2. 通过store.getState获取到的数据也是会按照reducers去划分的
> 3. 划分多个reducer的时候，默认状态只能创建在reducer中，因为划分reducer的目的，就是为了让每一个reducer都去独立管理一部分状态



```js
// 需要分支reducer的合并操作
import {combineReducers} from 'redux'
import todolist from './todolist/reducer'
const reducer = combineReducers({
  todolist  //后续要用redux状态，需要从指明的模块中取值
})
export default reducer
```











#### [react-redux](https://react-redux.js.org/)

cnpm install react-redux -S

react-redux提供两个核心的api：

- Provider: 提供store

  - **Provider**

    根据单一store原则 ，一般只会出现在整个应用程序的最顶层。

- connect: 用于连接容器组件和展示组件

  **connect() 返回一个函数(其实就是高阶组件)，函数参数接收展示组件，返回容器组件**

  - **connect**

    语法格式为：

    `connect(mapStateToProps?, mapDispatchToProps?, mergeProps?, options?)(component)`

    一般来说只会用到前面两个，它的作用是：

    - 把`store.getState()`的状态转化为展示组件的`props`

    - 把`actionCreators`转化为展示组件`props`上的方法

      

>特别强调：
>
>官网上的第二个参数为mapDispatchToProps, 实际上就是actionCreators

只要上层中有`Provider`组件并且提供了`store`, 那么，子孙级别的任何组件，要想使用`store`里的状态，都可以通过`connect`方法进行连接。如果只是想连接`actionCreators`，可以第一个参数传递为`null`

​    

##### 容器组件（Smart/Container Components）和展示组件（Dumb/Presentational Components）

Redux 的 React 绑定库是基于 [容器组件和展示组件相分离](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0) 的开发思想。所以建议先读完这篇文章再回来继续学习。这个思想非常重要。

已经读完了？那让我们再总结一下不同点：

|                | 展示组件                   | 容器组件                           |
| -------------: | :------------------------- | :--------------------------------- |
|           作用 | 描述如何展现（骨架、样式） | 描述如何运行（数据获取、状态更新） |
| 直接使用 Redux | 否                         | 是                                 |
|       数据来源 | props                      | 监听 Redux state                   |
|       数据修改 | 从 props 调用回调函数      | 向 Redux 派发 actions              |
|       调用方式 | 手动                       | 通常由 React Redux 生成            |

大部分的组件都应该是展示型的，但一般需要少数的几个容器组件把它们和 Redux store 连接起来。这和下面的设计简介并不意味着容器组件必须位于组件树的最顶层。如果一个容器组件变得太复杂（例如，它有大量的嵌套组件以及传递数不尽的回调函数），那么在组件树中引入另一个容器，就像[FAQ](https://www.redux.org.cn/docs/faq/ReactRedux.html#react-multiple-components)中提到的那样

技术上讲你可以直接使用 `store.subscribe()` 来编写容器组件。但不建议这么做的原因是无法使用 React Redux 带来的性能优化。也因此，不要手写容器组件，而使用 React Redux 的 `connect()` 方法来生成，后面会详细介绍。





#### [redux中间件](https://www.jianshu.com/p/e1acf613adf6)

   

通常情况下，action只是一个对象，不能包含异步操作，这导致了很多创建action的逻辑只能写在组件中，代码量较多也不便于复用，同时对该部分代码测试的时候也比较困难，组件的业务逻辑也不清晰，使用中间件了之后，可以通过actionCreator异步编写action，这样代码就会拆分到actionCreator中，可维护性大大提高，可以方便于测试、复用，同时actionCreator还集成了异步操作中不同的action派发机制，减少编码过程中的代码量



> **做异步的操作在action里面去实现！需要安装redux中间件**
> redux-thunk   redux-saga   redux-promise



**redux-thunk原理：**

可以看出来redux-thunk最重要的思想，就是可以接受一个返回函数的action creator。如果这个action creator 返回的是一个函数，就执行它，如果不是，就按照原来的next(action)执行。
正因为这个action creator可以返回一个函数，那么就可以在这个函数中执行一些异步的操作。**换言之，redux的中间件都是对store.dispatch()的增强** 



**dispatch一个action之后，到达reducer之前，进行一些额外的操作，就需要用到middleware**。你可以利用 Redux middleware 来进行日志记录、创建崩溃报告、调用异步接口或者路由等等。





store.js

```js
import {createStore,applyMiddleware} from 'redux'
import thunk from 'redux-thunk'
// 需要引入合并好的render文件
import reducer from './store/reducer'
const store = createStore(reducer,applyMiddleware(thunk)) 
export default  store
```



actionCreators.js

```js
export const deleteTodo = (id)=>{
  return dispatch=>{
    // 做一些ajax相关的异步操作逻辑
    setTimeout(() => {
      dispatch({type:DELETE_TODO,id}) //手动调用dispatch去派发标志性action对象
    }, 2000);
  }
}
```





#### [redux-saga](https://redux-saga.js.org/docs/introduction/GettingStarted/)

https://www.jianshu.com/p/7cac18e8d870

yarn add redux-saga

```js
import {createStore,applyMiddleware} from 'redux'
import createSagaMiddleware from 'redux-saga'
import reducer from './store/reducer'
import mySaga from './sagas'

const sagaMiddleware = createSagaMiddleware()
const store = createStore(reducer,applyMiddleware(sagaMiddleware)) 


// then run the saga
sagaMiddleware.run(mySaga)
export default  store
```

```js
import axios from 'axios'
import { call, put, takeEvery } from 'redux-saga/effects'
import {DELETE_TODO} from './store/todolist/actionType'


export const delay = ms => new Promise(resolve => setTimeout(resolve, ms))
export const delay2 = () => new Promise(async resolve => {
  let res = await axios.get('https://m.maizuo.com/gateway?cityId=110100&pageNum=1&pageSize=10&type=1&k=7712711',{
    headers:{
      'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"15984753841366499679797249","bc":"110100"}',
      'X-Host': 'mall.film-ticket.film.list'
    }
  })
  resolve(res)
})

function* fetchUser({id}) {
  let res = yield call(delay2)   //call的作用就是做异步操作的   
  console.log('res===>',res.data.data.films)  
  yield put({type: DELETE_TODO, id});  //put作用就是派发action对象给reducer处理  （put=dispatch）
}

function* mySaga() {
  yield takeEvery("deleteById", fetchUser);
}

export default mySaga;
```

```js
export default connect(state=>({todos:state.todolist.todos}),dispatch=>{
  return {
    change(id){
      let action = changeNewTodo(id)
      dispatch(action)
    },
    delete(id){
      //使用redux-saga
      dispatch({type:'deleteById',id})
    }
  }
})(TodoContent)
```









## [React-router-dom](https://reactrouter.com/docs/en/v6/getting-started/installation#create-react-app)

注意：目前最新的版本为6的版本了。

https://www.imooc.com/article/302147

https://juejin.cn/post/6862305213148381198

https://reactrouter.com/

React Router库包含三个不同的npm包，以下每个包都有不同的用途。

- react-router
- react-router-dom
- react-router-native

程序包 `react-router` 是核心库，用作上面列出的他两个程序包的对等依赖项。`react-router-dom` 是React应用中用于路由的软件包。列表中的最后一个包，`react-router-native` 有用于开发React Native应用的绑定。



`React Router v6`给我们带来方便的同时，还把包减少了一半以上的体积。（从20kb减少到8kb）

![img](https://img1.sycdn.imooc.com/5e7244d00001a7bd22130549.jpg)





### 路由的简单使用

​	安装路由： **yarn  add react-router-dom**

​    需要在最外层的节点上面：

```js
import {HashRouter as Router} from "react-router-dom"
ReactDOM.render(
  <Router>
    <App />
  </Router>,
  document.getElementById('root')
);
```

​    

​	使用Route实现路由

```js
import React,{Component} from 'react';
import {Route,Routes} from "react-router-dom"
import Home from "./views/Home"
import About from "./views/About"



//Route指代路由对象，path匹配路径；element当遇到当前的URL时，会告诉 Route 组件要渲染哪个React组件
//注意：Route 组件的 element 属性现在允许你传递一个React组件，而不仅仅是该React组件的名称
class App extends Component{
  render(){
    return (
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    )
  }
}
export default App;
```









### 	声明式导航 

在HTML中的不同网页之间导航的概念是使用锚点标记：

```html
<a href="">Some Link Name</a>
复制代码
```

在React应用程序中使用这种方法将导致在每次渲染新视图或页面本身时刷新web页面。为了避免刷新网页，`react-router-dom` 库提供了 `Link` 组件。

接下来，在 `App` 函数组件内部，创建一个导航栏，如代码片段所示：

```react
  <nav style={{ margin: 10 }}>
    <Link className={({ isActive }) => isActive ? "red" : ""} to="/" style={{ padding: 5 }}>
      Home
    </Link>
    <Link className={({ isActive }) => isActive ? "red" : ""} to="/about" style={{ padding: 5 }}>
    About
    </Link>
  </nav>
```

到浏览器窗口，以查看正在运行的导航栏：

![img](http://myimgcloud.oss-cn-hangzhou.aliyuncs.com/202008/react-router-v6/3.gif)





### 处理嵌套路由

嵌套路由是一个很重要的概念，需要理解。当路由被嵌套时，一般认为网页的某一部分保持不变，只有网页的子部分发生变化。

它从React Router库中挑选了一个名为 `Outlet` 的最佳元素，为特定路由呈现任何匹配的子元素。首先，从 `react-router-dom` 库中导入 `Outlet`：

```
import { Outlet } from 'react-router-dom';
```

为了模仿基本博客，我们在 `App.js` 文件中添加一些模拟数据。该代码段包含一个称为 `BlogPosts` 的对象，该对象进一步包含不同的对象作为属性。每个对象都由三部分组成：

- 一个唯一的ID
- 文章的标题
- 文章的描述

```javascript
const BlogPosts = {
  '1': {
    title: 'First Blog Post',
    description: 'Lorem ipsum dolor sit amet, consectetur adip.'
  },
  '2': {
    title: 'Second Blog Post',
    description: 'Hello React Router v6'
  }
};
```

这个独特的片段将被用于web浏览器的URL中，以查看每个帖子的内容。接下来，创建一个名为 `Posts` 的函数组件，其中显示所有博客帖子的列表：

```javascript
function Posts() {
  return (
    <div style={{ padding: 20 }}>
      <h2>Blog</h2>
      {/* 渲染任何匹配的子级 */}
      <Outlet />
    </div>
  );
}
```

定义另一个名为 `PostLists` 的组件，只要浏览器窗口中的URL点击[http://localhost:3000/posts，就会显示所有文章的列表。让我们使用JavaScript](https://link.juejin.cn?target=http%3A%2F%2Flocalhost%3A3000%2Fposts%EF%BC%8C%E5%B0%B1%E4%BC%9A%E6%98%BE%E7%A4%BA%E6%89%80%E6%9C%89%E6%96%87%E7%AB%A0%E7%9A%84%E5%88%97%E8%A1%A8%E3%80%82%E8%AE%A9%E6%88%91%E4%BB%AC%E4%BD%BF%E7%94%A8JavaScript) `Object.entry()` 方法从对象 `BlogPosts` 中返回一个数组，这个数组将被映射为显示所有博客文章的标题列表：

```javascript
function PostLists() {
  return (
    <ul>
      {Object.entries(BlogPosts).map(([slug, { title }]) => (
        <li key={slug}>
          <h3>{title}</h3>
        </li>
      ))}
    </ul>
  );
}
```

修改 `App` 函数组件中的路由，如下所示：

```html
<Routes>
  <Route path="/posts" element={<Posts />}>
    <Route path="" element={<PostLists />} />
    <Route path="a" element={<PostListsA />} />
  </Route>
</Routes>
```

这表明每当触发URL [http://localhost:3000/posts时，将渲染博客文章列表，因此，组件](https://link.juejin.cn?target=http%3A%2F%2Flocalhost%3A3000%2Fposts%E6%97%B6%EF%BC%8C%E5%B0%86%E6%B8%B2%E6%9F%93%E5%8D%9A%E5%AE%A2%E6%96%87%E7%AB%A0%E5%88%97%E8%A1%A8%EF%BC%8C%E5%9B%A0%E6%AD%A4%EF%BC%8C%E7%BB%84%E4%BB%B6) `PostsLists`：

![img](http://myimgcloud.oss-cn-hangzhou.aliyuncs.com/202008/react-router-v6/4.png)





### 访问路由的URL参数和动态参数

要想从渲染的博客文章列表中点击文章标题来访问各个文章，你要做的就是，将每个文章的标题包裹在 `PostsLists` 组件中的 `Link` 组件内。然后，使用每个文章的 `slug` 定义每个文章的路径，前缀为 `/posts/` 的文章在浏览器中的路径是一致的。

```html
<ul>
  {Object.entries(BlogPosts).map(([slug, { title }]) => (
    <li key={slug}>
      <Link to={`/posts/${slug}`}>
        <h3>{title}</h3>
      </Link>
    </li>
  ))}
</ul>

```

接下来，从 `react-router-dom` 库中导入一个名为 `useParams` 的钩子。通过这个钩子，你可以访问特定路由（或Slug）可能具有的任何动态参数。每个 `slug` 的动态参数都会是每篇博文的 `title` 和 `description`。访问它们的需要是，当在浏览器窗口中以URL形式触发博客文章的特定段时，显示每个博客文章的内容：

```javascript
import { useParams } from 'react-router-dom';
```

创建一个名为 `Post` 的新函数组件，该组件将从 `useParams` 钩子中获取当前的文章。使用JavaScript中的方括号符号语法，将创建一个新的 `post` 变量，该变量包含属性的值或博客文章的当前内容。

```javascript
function Post() {
  const BlogPosts = {
    "1": {
      title: "第一篇博客文章",
      description: "第一篇博客文章，是关于Vue3.0的"
    },
    "2": {
      title: "第二篇博客文章",
      description: "Hello React Router v6"
    }
  };
  
  const { slug } = useParams();
  const post = BlogPosts[slug];
  const { title, description } = post;
  return (
    <div style={{ padding: 20 }}>
      <h3>{title}</h3>
      <p>{description}</p>
    </div>
  );
}
```

最后，在 `App` 函数组件中添加一个称为 `:slug` 的动态路由，以渲染每个文章的内容：

```html
// 其余代码保持不变
<Route path="/posts" element={<Posts />}>
  <Route path="" element={<PostLists />} />
  <Route path="a" element={<PostListsA />} />
  <Route path=":slug" element={<Post />} />
</Route>
复制代码
```

这是此步骤之后的完整输出：

![img](http://myimgcloud.oss-cn-hangzhou.aliyuncs.com/202008/react-router-v6/5.gif)

### navigate实现编程式导航

```react
import { useNavigate } from 'react-router-dom';

function MyButton() {
  let navigate = useNavigate();
  function handleClick() {
    navigate('/home');
  };
  return <button onClick={handleClick}>Submit</button>;
};
```

默认是push跳转，也可以改成replace跳转

```
navigate('/home', {replace: true});
```



### [withRouter](https://reactrouter.com/docs/en/v6/faq)

在普通的组件中，默认props获取不到路由相关的api,如果想要获取，需要封装withRouter这个hoc高阶组件实现。

```react
import {
  useLocation,
  useNavigate,
  useParams
} from "react-router-dom";

function withRouter(Component) {
  function ComponentWithRouterProp(props) {
    let location = useLocation();
    let navigate = useNavigate();
    let params = useParams();
    return (
      <Component
        {...props}
        router={{ location, navigate, params }}
      />
    );
  }

  return ComponentWithRouterProp;
}
```











### React Router基本原理

React Router甚至大部分的前端路由都是依赖于[`history.js`](<https://github.com/browserstate/history.js>)的，它是一个独立的第三方js库。可以用来兼容在不同浏览器、不同环境下对历史记录的管理，拥有统一的API。

- 老浏览器的history: 通过`hash`来存储在不同状态下的`history`信息，对应`createHashHistory`，通过检测`location.hash`的值的变化，使用`location.replace`方法来实现url跳转。通过注册监听`window`对象上的`hashChange`事件来监听路由的变化，实现历史记录的回退。
- 高版本浏览器: 利用HTML5里面的history，对应`createBrowserHistory`, 使用包括`pushState`， `replaceState`方法来进行跳转。通过注册监听`window`对象上的`popstate`事件来监听路由的变化，实现历史记录的回退。
- node环境下: 在内存中进行历史记录的存储，对应`createMemoryHistory`。直接在内存里`push`和`pop`状态。



> 







# React项目

## 一. CRA的脚手架制定

​	因为我们发现，调用高阶组件的时候采用withCopy(About)代码，但是不够简洁优雅。

​	那么我们可以采用装饰器的写法实现调用高阶组件

```js
@WithCopy
class About extends Component {
    render() {
        return (
            <div>
                about -- {this.props.a}
            </div>
        )
    }
}
```

很不幸，目前的cra是不支持这种写法，我们需要单独进行定制，让其支持这种写法。



[Antd中提供了社区解决方案](https://ant.design/docs/react/use-with-create-react-app-cn)

> yarn add @craco/craco

对脚手架进行轻微的调整

```js
"scripts": {
    "start": "craco start",
    "build": "craco build",
    "test": "craco test"
 },
```



yarn start启动项目发现报错了，原因是因为根路径下面缺少 craco.config.js文件

```js
/* craco.config.js */
module.exports = {
  // ...
};
```

   

启动yarn start，发现报错了！ 

> 错误： Cannot find module 'react-scripts/package.json'

> yarn  add  react-scripts



自定义主题的配置：

> yarn add antd

index.js文件中：

```
import 'antd/dist/antd.less';
```

​	

然后安装 `craco-less` 并修改 `craco.config.js` 文件如下。

> yarn add craco-less

```js
const CracoLessPlugin = require('craco-less');

module.exports = {
  plugins: [
    {
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: { '@primary-color': 'yellow' },
            javascriptEnabled: true,
          },
        },
      },
    },
  ],
};
```





[后续CRA支持装饰器需要这样配置](https://blog.csdn.net/lucky569/article/details/107253310/)：

> yarn add @babel/plugin-proposal-decorators

在craco.config.js文件中新增以下代码即可:

```js
babel: {
   plugins: [["@babel/plugin-proposal-decorators", { legacy: true }]]
},
```



其实就会发现 react面向社区化的。它把一些常用到的包都放在社区，用到的话单独去查找去进行相应的配置。

vue的话面向官方化，很多东西内部都帮助我们去实现了





自定义主题的配置：

theme.js

```
module.exports = {
  '@primary-color':' #1890ff', // 全局主色
  '@link-color':' #1890ff', // 链接色
  '@success-color':' #52c41a', // 成功色
  '@warning-color':' #faad14', // 警告色
  '@error-color':' #f5222d', // 错误色
  '@font-size-base':' 14px', // 主字号
  '@heading-color':' rgba(0, 0, 0, 0.85)', // 标题色
  '@text-color':' rgba(0, 0, 0, 0.65)', // 主文本色
  '@text-color-secondary':' rgba(0, 0, 0, 0.45)', // 次文本色
  '@disabled-color':' rgba(0, 0, 0, 0.25)', // 失效色
  '@border-radius-base':' 2px', // 组件/浮层圆角
  '@border-color-base':' #d9d9d9', // 边框色
  '@box-shadow-base':' 0 3px 6px -4px rgba(0, 0, 0, 0.12), 0 6px 16px 0 rgba(0, 0, 0, 0.08),0 9px 28px 8px rgba(0, 0, 0, 0.05)', // 浮层阴影
}
```



croco.config.js

```
const theme = require('./theme')

 lessOptions: {
     modifyVars: theme,
     javascriptEnabled: true,
 },
```



模块化规范：

​	amd cmd (用在浏览器端  amd遵循依赖前置，cmd遵循依赖就近)

   commonjs(node.js  require|module.exports)

   es6module(import   export default)



## 二 搭建项目的基本页面与路由

### 2-1 配置基本页面

src/views/页面文件夹/页面

​	           dashboard/index.jsx

​              article/index.jsx  | edit.jsx

​              settings/index.jsx

​              login/index.jsx

​             notfound/index.jsx



src/views/index.js

```
import ArticleList from './article'
import ArticleEdit from './article/edit'
import Dashboard from './dashboard'
import Settings from './settings'
import Notfound from './notfound'
import Login from './login'


export {
  ArticleList,
  ArticleEdit,
  Dashboard,
  Settings,
  Notfound,
  Login
}
```





### 2-2 配置路由

index.js

```
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router,Routes,Route } from "react-router-dom";
import 'antd/dist/antd.less'
import {Dashboard,ArticleList,ArticleEdit,Settings, Login,Notfound} from './views'
import Admin from './admin'

/*
  /login 登录页面
  /404  404页面


  /admin/dashboard          仪表盘页面（首页）
  /admin/article            文章列表页面
  /admin/article/edit/:id   文章编辑页面
  /admin/settings           设置页面
*/
ReactDOM.render(
  <Router>
    <Routes>
      <Route path='/' element={<Admin/>}>
        <Route index element={<Dashboard/>}></Route>
        <Route path='/admin/dashboard' element={<Dashboard/>}></Route>
        <Route path='/admin/article' element={<ArticleList/>}></Route>
        <Route path='/admin/article/edit/:id' element={<ArticleEdit/>}></Route>
        <Route path='/admin/settings' element={<Settings/>}></Route>
      </Route>
      <Route path='/login' element={<Login/>}></Route>
      <Route path='*' element={<Notfound/>}></Route>
    </Routes>
  </Router>,
  document.getElementById('root')
);
```

Admin.jsx

```
import React, { Component } from 'react'
import {Outlet} from 'react-router-dom'
export default class admin extends Component {
  render() {
    return (
      <div>
        <Outlet/>
      </div>
    )
  }
}
```







src/routes/index.js

```
import {Dashboard,ArticleList,ArticleEdit,Settings, Login,Notfound} from '../views'
import Admin from '../admin'
import {useRoutes} from 'react-router-dom'

let routes = [
  {
    path: "/",
    element: <Admin />,
    children: [
      { path: "", element: <Dashboard /> },
      { path: "/admin/dashboard", element: <Dashboard /> },
      { path: "/admin/article", element: <ArticleList /> },
      { path: "/admin/article/edit/:id", element: <ArticleEdit /> },
      { path: "/admin/settings", element: <Settings /> },
    ]
  },
  { path: "/login", element: <Login /> },
  { path: "*", element: <Notfound /> }
]

function App(){
  let element = useRoutes(routes);
  return element;
}

export {
  routes,
  App
}
```

```
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router} from "react-router-dom";
import 'antd/dist/antd.less'
import {App} from './routes'

ReactDOM.render(
  <Router>
    <App/>
    
    {/* <Routes>
          <Route path='/' element={<Admin/>}>
            <Route index element={<Dashboard/>}></Route>
            <Route path='/admin/dashboard' element={<Dashboard/>}></Route>
            <Route path='/admin/article' element={<ArticleList/>}></Route>
            <Route path='/admin/article/edit/:id' element={<ArticleEdit/>}></Route>
            <Route path='/admin/settings' element={<Settings/>}></Route>
          </Route>
        <Route path='/login' element={<Login/>}></Route>
        <Route path='*' element={<Notfound/>}></Route>
    </Routes> */}
    
  </Router>,
  document.getElementById('root')
);
```





### 2-3 路由懒加载的实现

yarn add [react-loadable](https://www.npmjs.com/package/react-loadable)

默认内部会将所有的组件进行打包加载引入到首页里面去，然后首页去加载的时候肯定比较慢，用时过长，用户体验差。

后续采用路由懒加载，内部就会随用随载，就不会将所有的组件一次性打包到首页中，提高首页的打开速度，不容易发生卡顿、白屏现象。



src/views/index.js

```
// import ArticleList from './article'
// import ArticleEdit from './article/edit'
// import Dashboard from './dashboard'
// import Settings from './settings'
// import Notfound from './notfound'
// import Login from './login'


//采用路由懒加载的方式暴露视图组件
import Loadable from 'react-loadable';
import Loading from '../components/loading';
const ArticleList = Loadable({
  loader: () => import('./article'),
  loading: Loading,
})
const ArticleEdit = Loadable({
  loader: () => import('./article/edit'),
  loading: Loading,
})
const Dashboard = Loadable({
  loader: () => import('./dashboard'),
  loading: Loading,
})
const Settings = Loadable({
  loader: () => import('./settings'),
  loading: Loading,
})
const Notfound = Loadable({
  loader: () => import('./notfound'),
  loading: Loading,
})
const Login = Loadable({
  loader: () => import('./login'),
  loading: Loading,
})
export {
  ArticleList,
  ArticleEdit,
  Dashboard,
  Settings,
  Notfound,
  Login
}
```





## 三. Layouts布局

### 3-1 借助layout组件进行界面布局

src/components/layouts/index.jsx

```
import React, { Component } from 'react'
import { Layout, Menu } from 'antd';
import { UserOutlined, LaptopOutlined, NotificationOutlined } from '@ant-design/icons';

const { SubMenu } = Menu;
const { Header, Content, Footer, Sider } = Layout;
export default class index extends Component {
  render() {
    return (
      <Layout>
        <Header className="header">
          <div className="logo" />
        </Header>
        <Content style={{ padding: '0 50px' }}>
          <Layout className="site-layout-background" style={{ padding: '24px 0' }}>
            <Sider className="site-layout-background" width={200}>
              <Menu
                mode="inline"
                defaultSelectedKeys={['1']}
                defaultOpenKeys={['sub1']}
                style={{ height: '100%' }}
              >
                <Menu.Item key="1">option1</Menu.Item>
                <Menu.Item key="2">option2</Menu.Item>
                <Menu.Item key="3">option3</Menu.Item>
                <Menu.Item key="4">option4</Menu.Item>
              </Menu>
            </Sider>
            <Content style={{ padding: '0 24px', minHeight: 280 }}>{this.props.children}</Content>
          </Layout>
        </Content>
        <Footer style={{ textAlign: 'center' }}>Ant Design ©2018 Created by Ant UED</Footer>
    </Layout>
    )
  }
}
```



admin.jsx

```
import Layouts from './components/layouts'

<Layouts>
	<Outlet/>
</Layouts>
```



layouts/index.less

```
#root,.ant-layout{
  height:100%;
}
```





### 3-2 左侧导航的显示

```
import { BugTwoTone,DatabaseOutlined,SettingOutlined} from '@ant-design/icons';


<Menu
mode="inline"
defaultSelectedKeys={['1']}
defaultOpenKeys={['sub1']}
style={{ height: '100%' }}
>
    <Menu.Item key="1" icon={<BugTwoTone twoToneColor="#52c41a"/>}>仪表盘</Menu.Item>
    <Menu.Item key="2" icon={<DatabaseOutlined />}>文章列表</Menu.Item>
    <Menu.Item key="3" icon={<SettingOutlined />}>设置</Menu.Item>
</Menu>
```





如果后续图标没有满足你的要求，可以使用iconfont实现：

```
import { createFromIconfontCN } from '@ant-design/icons';
const IconFont = createFromIconfontCN({
  scriptUrl: '//at.alicdn.com/t/font_2339840_ugs20m0pwas.js',
});

<Menu.Item key="3" icon={<IconFont type="icon-xuexiao_xuexiaoxinxi" />}>设置</Menu.Item>
```





### 3-3 点击menu进行跳转

```
<Menu
mode="inline"
defaultSelectedKeys={['1']}
defaultOpenKeys={['sub1']}
style={{ height: '100%' }}
onClick={this.handleClick}
>
<Menu.Item key="/admin/dashboard" icon={<BugTwoTone twoToneColor="#52c41a"/>}>仪表盘</Menu.Item>
<Menu.Item key="/admin/article" icon={<DatabaseOutlined />}>文章列表</Menu.Item>
<Menu.Item key="/admin/settings" icon={<IconFont type="icon-xuexiao_xuexiaoxinxi" />}>设置</Menu.Item>
</Menu>
```

```
handleClick = ({key})=>{
    let {navigate} = this.props.router
    navigate(key)
  }
```



类组件需要借助高阶组件withRouter进行包裹，props上面才可以拥有路由相关的api.

```
import withRouter from '../withRouter';


@withRouter
class index extends Component {

}
```





### 3-4 将仪表盘设置为二级菜单

```
 <Menu
     mode="inline"
     defaultOpenKeys={['sub1']}  // 让那个二级菜单初始化的时候展开
     defaultSelectedKeys={['/admin/dashboard']}
     selectedKeys={[path]}  // 刷新页面的时候，发现之前的始终是仪表盘导航选中。
     style={{ height: '100%' }}
     onClick={this.handleClick}
 > 
 	 <SubMenu key="sub1" icon={<BugTwoTone twoToneColor="#52c41a"/>} title="二级菜单">
         <Menu.Item key="/admin/dashboard" icon={<BugTwoTone twoToneColor="#52c41a"/>}>仪表盘</Menu.Item>
         <Menu.Item key="/admin/aaa" icon={<BugTwoTone twoToneColor="#52c41a"/>}>Aaa</Menu.Item>
     </SubMenu>
     <Menu.Item key="/admin/article" icon={<DatabaseOutlined />}>文章列表</Menu.Item>
     <Menu.Item key="/admin/settings" icon={<IconFont type="icon-xuexiao_xuexiaoxinxi" />}>设置</Menu.Item>
 </Menu>
```

```
children: [
      { path: "", element: <Dashboard /> },
      { path: "/admin/dashboard", element: <Dashboard /> },
      { path: "/admin/aaa", element: <Aaa /> },
      { path: "/admin/article", element: <ArticleList /> },
      { path: "/admin/article/edit/:id", element: <ArticleEdit /> },
      { path: "/admin/settings", element: <Settings /> },
    ]
```

```
let {location} = this.props.router
let path = location.pathname
if(path === '/'){
	path = '/admin/dashboard'
}
```







## 四. 文章列表的实现

### 4-1  mock来去模拟数据

后端没有来得及创建接口数据，需要前端人员进行mock数据。

http://rap2.taobao.org/





### 4-2 axios拦截器的封装

src/request/index.js

```

import axios from 'axios'
// 创建axios的实例
const service = axios.create({
  baseURL:'http://rap2api.taobao.org/app/mock/294683'
})


// axios拦截器的创建
// 请求发送给后端之前进行拦截操作   可以在请求头上面携带一些公共的字段发给后端
service.interceptors.request.use(config=>{
  config.headers = {...config.headers,authToken:'xxxxxxx'}
  return config
})



// 响应之后的拦截器
// 可以根据后端返回的不同的状态码进行不同业务逻辑的操作
service.interceptors.response.use(res=>{
  if(res.data.code === 200){
    return res.data.data
  }
})


// 暴露请求文章列表的数据方法
export const getArticle = ()=>{
  return service.post('/api/v1/articlelist')
}
```



article:

```
import {getArticle} from '../../request'

componentDidMount(){
    getArticle().then(res=>{
      console.log('article----->',res)
    })
  }
```



### 4-3 渲染文章列表数据

```
const dataSource = [
  {
    key: '1',
    name: '胡彦斌',
    age: 32,
    address: '西湖区湖底公园1号',
  },
  {
    key: '2',
    name: '胡彦祖',
    age: 42,
    address: '西湖区湖底公园1号',
  },
];
const columns = [
  {
    title: '姓名',  // 列的名字
    dataIndex: 'name', // dataSource里面每个对象的name值取出来放在此列
  },
  {
    title: '年龄',
    dataIndex: 'age',
  },
  {
    title: '住址',
    dataIndex: 'address',
  },
];

<Card title="文章列表">
	<Table dataSource={dataSource} columns={columns} />
</Card>
```





```
componentDidMount(){
    this.getData()
  }

  getData = ()=>{
    getArticle().then(res=>{
      const columnsKeys = Object.keys(res.list[0]) 
      const columns = columnsKeys.map(item=>{
        return {
          title:item,
          dataIndex:item
        }
      })
      this.setState({
        dataSource:res.list,
        columns
      })
    })
  }

```

```
<Card title="文章列表">
	<Table dataSource={this.state.dataSource} columns={this.state.columns}  rowKey={record=>record.id}/>
</Card>
```





### 4-4 中文映射

```
const titleDisplayMap = {
  id:'id',
  author:'作者',
  title:'标题',
  amount:'阅读量',
  currentAt:'发布时间'
}
```

```
const columns = columnsKeys.map(item=>{
        return {
          title:titleDisplayMap[item],
          dataIndex:item
        }
      })
```







### 4-5 阅读量的优化

希望300以上的变成绿色，300以下的变成红色

```
getData = ()=>{
    getArticle().then(res=>{
      const columnsKeys = Object.keys(res.list[0]) 
      const columns = columnsKeys.map(item=>{
        if(item === 'amount') { // 如果是阅读量这一列
          return {
            title:titleDisplayMap[item],
            render(text){
              return <Tooltip placement={text.amount>300?'top':'bottom'} title={text.amount>300?'高于300':'低于300'}><Tag color={text.amount>300?'green':'red'}>{text.amount}</Tag></Tooltip>
            }
          }
        }else{
          return {
            title:titleDisplayMap[item],
            dataIndex:item
          }
        }
      })
      this.setState({
        dataSource:res.list,
        columns
      })
    })
  }

```



对于多种类型的判断？

```
changeAmount = amount => {
    if(amount < 300){
      return {
        color:'red',
        placement:'bottom',
        title:'小于300'
      }
    }else if(amount>=300 && amount <400){
      return {
        color:'orange',
        placement:'bottom',
        title:'介于300到400之间'
      }
    }else{
      return {
        color:'green',
        placement:'top',
        title:'高于400'
      }
    }
  }
```

```
const columns = columnsKeys.map(item=>{
        if(item === 'amount') { // 如果是阅读量这一列
          return {
            title:titleDisplayMap[item],
            render:(text)=>{
              return <Tooltip placement={this.changeAmount(text.amount).placement} title={this.changeAmount(text.amount).title}>
                  <Tag color={this.changeAmount(text.amount).color}>{text.amount}</Tag>
                </Tooltip>
            }
          }
        }else{
          return {
            title:titleDisplayMap[item],
            dataIndex:item
          }
        }
      })
```



### 4-6 拖拽表格实现

yarn add  react-sortable-hoc  array-move

```
import React, { Component } from 'react'
import { Table,Tag,Tooltip } from 'antd';
import { sortableContainer, sortableElement, sortableHandle } from 'react-sortable-hoc';
import { MenuOutlined } from '@ant-design/icons';
import { arrayMoveImmutable } from 'array-move';
import {getArticle} from '../../request'
import './index.less'
const titleDisplayMap = {
  id:'id',
  author:'作者',
  title:'标题',
  amount:'阅读量',
  currentAt:'发布时间'
}
// 拖拽的手柄
const DragHandle = sortableHandle(() => <MenuOutlined style={{ cursor: 'grab', color: '#999' }} />);
const SortableItem = sortableElement(props => <tr {...props} />);
const SortableContainer = sortableContainer(props => <tbody {...props} />);
export default class index extends Component {
  state = {
    dataSource: [], //数据源，每条数据对象需要有个index属性
    columns:[]     //列 {title,dataIndex,render(text){}}
  };

  componentDidMount(){
    this.getData()
  }
  
  getData = ()=>{
    getArticle().then(res=>{
      const columnsKeys = Object.keys(res.list[0]) 
      const columns = columnsKeys.map(item=>{
        if(item === 'amount') { // 如果是阅读量这一列
          return {
            title:titleDisplayMap[item],
            render:(text)=>{
              return <Tooltip placement={this.changeAmount(text.amount).placement} title={this.changeAmount(text.amount).title}>
                  <Tag color={this.changeAmount(text.amount).color}>{text.amount}</Tag>
                </Tooltip>
            }
          }
        }

        if(item === 'id'){
          return {
            title:titleDisplayMap[item],
            render: (text) => <>
                      <DragHandle/> &nbsp;
                      <span>{text.id}</span>
                    </>,
          }
        }


        return {
          title:titleDisplayMap[item],
          dataIndex:item
        }
        
      })

      // 需要给dataSource数组里面的每个对象添加一个index属性即可
      res.list = res.list.map(item=>{  // [{之前数据的基础上,index:xxxx},{}]
        return {...item,index:item.id}
      })

      this.setState({
        dataSource:res.list,
        columns
      })
    })
  }


  changeAmount = amount => {
    if(amount < 300){
      return {
        color:'red',
        placement:'bottom',
        title:'小于300'
      }
    }else if(amount>=300 && amount <400){
      return {
        color:'orange',
        placement:'bottom',
        title:'介于300到400之间'
      }
    }else{
      return {
        color:'green',
        placement:'top',
        title:'高于400'
      }
    }
  }
  onSortEnd = ({ oldIndex, newIndex }) => {
    const { dataSource } = this.state;
    if (oldIndex !== newIndex) {
      const newData = arrayMoveImmutable([].concat(dataSource), oldIndex, newIndex).filter(el => !!el);
      this.setState({ dataSource: newData });
    }
  };

  DraggableContainer = props => (
    <SortableContainer
      useDragHandle
      disableAutoscroll
      helperClass="row-dragging"
      onSortEnd={this.onSortEnd}
      {...props}
    />
  );

  DraggableBodyRow = ({ className, style, ...restProps }) => {
    const { dataSource } = this.state;
    const index = dataSource.findIndex(x => x.index === restProps['data-row-key']);
    return <SortableItem index={index} {...restProps} />;
  };

  render() {
    const { dataSource,columns } = this.state;
    return (
      <Table
        pagination={false}
        dataSource={dataSource}
        columns={columns}
        rowKey="index"
        components={{
          body: {
            wrapper: this.DraggableContainer,
            row: this.DraggableBodyRow,
          },
        }}
      />
    );
  }
}

```

```
.row-dragging {
  background: #fafafa;
  border: 1px solid #ccc;
}

.row-dragging td {
  padding: 16px;
}

.row-dragging .drag-visible {
  visibility: visible;
}
```





### 4-7 发布时间格式化处理

yarn add moment

```
if(item === 'currentAt'){
          return {
            title:titleDisplayMap[item],
            render:(text)=>{
              return <span>{moment(text.currentAt).format('YYYY-MM-DD HH:mm')}</span>
            }
          }
        }
```





### 4-8 阅读量的筛选与排序

```
if(item === 'amount') { // 如果是阅读量这一列
          return {
            title:titleDisplayMap[item],
            render:(text)=>{
              return <Tooltip placement={this.changeAmount(text.amount).placement} title={this.changeAmount(text.amount).title}>
                  <Tag color={this.changeAmount(text.amount).color}>{text.amount}</Tag>
                </Tooltip>
            },
            filters:[
              {
                text: '高于250',
                value: '>250',
              },
              {
                text: '低于250',
                value: '<=250',
              },
            ],
            onFilter: (value, record) => {
              if(value === '>250'){
                return record.amount > 250
              }else{
                return record.amount <= 250
              }
            },
            sortDirections: ['descend'], // 只能降序排列
            sorter: (a, b) => a.amount - b.amount,
          }
        }
```





当数据量比较大的时候，我们可以给Table配置一个scroll属性，限制在某个区域里面进行滚动。

```
scroll={{ 
    y: 500,
    x: 1200,
    scrollToFirstRowOnChange:false //排序或者筛选后不能滚动到顶部的
}}  
```





### 4-9 前端分页实现

```
state = {
    dataSource:[],
    columns:[],
    total:0  //文章列表的总数
  }
```

```
this.setState({
        dataSource:res.list,
        columns,
        total:res.total
      })
```

```
pagination={{
        position:['topRight'],
        total:this.state.total
       }}
```



```
 state = {
    dataSource:[],
    columns:[],
    total:0,//文章列表的总数
    limited:10, //每一页的条数
    offset:0   //代表每一页第一条数据的下标  第一页(0-9)  第二页(10-19)  第三页(20-29)
  }
```

接下来，需要将limited与offset两个字段传递给后端。

```
getData = ()=>{
    getArticle(this.state.limited,this.state.offset).then(res=>{
```

```

// 暴露请求文章列表的数据方法
export const getArticle = (limited,offset)=>{
  return service.post('/api/v1/articlelist',{limited,offset})
}
```



接下来，当我们点击分页器的时候，需要将最新的offset传递给后端：

```
  // page代表当前点击的页码，pageSize代表每一页的条数
  handleChange(page, pageSize){
    // console.log(page, pageSize)   page=1|offset:0   page=2|offset:10   page=3|offset:20
    this.setState({
      limited:pageSize,
      offset:(page-1)*pageSize
    },()=>{
      this.getData()  //进行异步请求，将最新的limited与offset重新发送给后端
    })
  }
```



假设用户一进来，希望进入到第五页：

```
state = {
    dataSource:[],
    columns:[],
    total:0,//文章列表的总数
    limited:10, //每一页的条数
    offset:40   //代表每一页第一条数据的下标  第一页(0-9)  第二页(10-19)  第三页(20-29)
  }
```

```
pagination={{
        position:['topRight'],
        total:this.state.total,
        onChange:this.handleChange,
        current: this.state.offset / this.state.limited + 1       
       }}
```





### 4-10 增加操作栏

```

      // 追加新的一列
      columns.push({
        title:'操作',
        render:()=>{
          return <ButtonGroup>
            <Button type="primary">编辑</Button>
            <Button type="primary" danger>删除</Button>
          </ButtonGroup>
        }
      })
```

删除接口创建：

/api/v1/articledelete/:id   delete请求

入参： header上面携带authToken字段

出参： code:200   data:{msg:'删除成功‘}

```
// 暴露删除文章的接口方法
export const articleDeleteById = id => {
  return service.delete('/api/v1/articledelete/'+id)
}
```



```
<Button type="primary" danger onClick={this.handleDelete.bind(this,text)}>删除</Button>
```

```
 // 删除操作
  handleDelete = ({id,title})=>{
    Modal.confirm({
      title:'确定要删除吗？',
      content:<>你要删除<span style={{color:'red'}}>{title}</span>文章吗？</>,
      okText:'确定',
      cancelText:'取消',
      onOk:(close)=>{ //点击确定的触发事件
        return new Promise((resolve,reject)=>{ //需要等待删除成功后，再去调用close()关闭弹窗
          articleDeleteById(id).then(res=>{
            message.success({  //删除成功后，全局提示删除成功
              content:res.msg,
              duration:1,
              style:{
                position:'fixed',
                left:'46%',
                top:'46%'
              }
            })
            close() // 必须要等到文章删除完毕了，后端返回结果了，弹窗才能消失  
            this.getData() //重新请求页面
          })
        })
      }
    })
  }
```



### 4-11 点击编辑跳转到编辑页面

```
<Button type="primary" onClick={this.handleEdit.bind(this,text)}>编辑</Button>
```

```
// 跳转到编辑页面
  handleEdit = ({id})=>{
    let {navigate} = this.props.router
    navigate('/admin/article/edit/'+id)
  }
```



## 五. 编辑页面实现

### 5-1 编辑页面的布局

```
import React, { Component } from 'react'
import {Card,Form, Input, Button, Checkbox} from 'antd'
export default class edit extends Component {

  onFinish = (values) => {
    console.log('Success:', values);
  };

  onFinishFailed = (errorInfo) => {
    console.log('Failed:', errorInfo);
  };

  render() {
    return (
      <Card title='文章编辑'>
        <Form
          name="basic"
          labelCol={{
            span: 4,
          }}
          wrapperCol={{
            span: 14,
          }}
          initialValues={{
            username:'初始化的值',
            remember: false,
          }}
          onFinish={this.onFinish}
          onFinishFailed={this.onFinishFailed}
          autoComplete="off"
        >
          <Form.Item
            label="用户名"
            name="username"
            rules={[
              {
                required: true,
                message: 'Please input your username!',
              }
            ]}
          >
            <Input />
          </Form.Item>

          <Form.Item
            label="Password"
            name="password"
            rules={[
              {
                required: true,
                message: 'Please input your password!',
              },
            ]}
          >
            <Input.Password />
          </Form.Item>

          <Form.Item
            name="remember"
            valuePropName="checked"
            wrapperCol={{
              offset: 4,
              span: 16,
            }}
          >
            <Checkbox>Remember me</Checkbox>
          </Form.Item>

          <Form.Item
            wrapperCol={{
              offset: 4,
              span: 16,
            }}
          >
            <Button type="primary" htmlType="submit">
              Submit
            </Button>
          </Form.Item>
        </Form>
      </Card>
    )
  }
}
```



### 5-2 修改编辑页面

```
import React, { Component } from 'react'
import {Card,Form, Input, Button, InputNumber,DatePicker} from 'antd'
import E from "wangeditor"
import './index.less'
export default class edit extends Component {

  onFinish = (values) => {
    console.log('Success:', values);
  };

  onFinishFailed = (errorInfo) => {
    console.log('Failed:', errorInfo);
  };

  componentDidMount(){
    this.initEditor()
  }

  initEditor = ()=>{
    const editor = new E("#editor")
    editor.create()
  }

  render() {
    return (
      <Card title='文章编辑'>
        <Form
          name="basic"
          labelCol={{
            span: 4,
          }}
          wrapperCol={{
            span: 14,
          }}
          onFinish={this.onFinish}
          onFinishFailed={this.onFinishFailed}
          autoComplete="off"
        >
          <Form.Item
            label="标题"
            name="title"
            rules={[
              {
                required: true,
                message: 'Please input title!',
              }
            ]}
          >
            <Input />
          </Form.Item>

          <Form.Item
            label="作者"
            name="author"
            rules={[
              {
                required: true,
                message: 'Please input author!',
              }
            ]}
          >
            <Input />
          </Form.Item>

          <Form.Item
            label="阅读量"
            name="amount"
            rules={[
              {
                required: true,
                message: 'Please input amount!',
              }
            ]}
          >
            <InputNumber min={1}/>
          </Form.Item>

          <Form.Item
            label="发布时间"
            name="currentAt"
            rules={[
              {
                required: true,
                message: 'Please input currentAt!',
              }
            ]}
          >
             <DatePicker showTime />
          </Form.Item>

          <Form.Item
            label="文章内容"
            name="content"
            rules={[
              {
                required: true,
                message: 'Please input content!',
              }
            ]}
          >
            <div id='editor'/>
          </Form.Item>

          <Form.Item
            wrapperCol={{
              offset: 4,
              span: 16,
            }}
          >
            <Button type="primary" htmlType="submit">
              Submit
            </Button>
          </Form.Item>
        </Form>
      </Card>
    )
  }
}
```

```
#editor{
  z-index: 0;
  position: relative;
}
```

对于文章内容的修改，采用了wangeditor这个轻量级的富文本编辑器。

https://www.wangeditor.com/doc/

yarn add wangeditor



注意：

​	当点击表单提交的时候，发现content内容没有设置上！

​    因为content这个字段不会进行自动设置，其它组件都是antd的组件，内部会进行设置的。

​	

```
<Form
  ref={el=>this.formRef = el}
```

```
initEditor = ()=>{
    const editor = new E("#editor")
    editor.create()

    
    // 当修改了编辑器里面内容的时候
    editor.config.onchange = newHtml=> {
      this.formRef.setFieldsValue({ // 需要给contnent字段赋值
        content:newHtml
      })
    };
  }
```



### 5-3 编辑页面文章数据回填

/api/v1/article/:id

get请求

headers:{authToken:xxxx}

res:  code:200  data:{title,author,amount,currentAt,content}

```
// 根据id查询文章信息进行编辑表单回填
export const getArticleDetailById = id => {
  return service.get(`/api/v1/article/${id}`)
}
```

```
componentDidMount(){
    this.initEditor()

    // 需要进行数据请求，表单回填
    getArticleDetailById(this.props.router.params.id).then(res=>{
      // 需要调用setFieldValues设置表单字段
      this.formRef.setFieldsValue({
        title:res.title,
        author:res.author,
        amount:res.amount,
        currentAt:moment(res.currentAt), //注意：后端返回的是时间戳，需要转成moment对象设置DatePicker组件才可以
        content:res.content
      })
      // 设置富文本编辑器content内容
      this.editor.txt.html(res.content)
    })
  }
```



### 5-4 表单提交

创建保存文章的接口：

/api/v1/articlesave/:id

post请求

headers:{authToken:xxxxx}

body:{title,amount,author,currentAt,content}

res:code:200  data:{msg:'保存文章成功'}

```
// 保存文章的接口
// id代表保存文章的id
// data是一个对象，代表传递给后端的文章信息  data={title,author,xxxx}
export const saveArticleById = (id,data) => {
  return service.post(`/api/v1/articlesave/${id}`,data)
}
```



```
onFinish = (values) => {
    // 将currentAt这个字段转成时间戳后，传递给后端
    values.currentAt = values.currentAt.valueOf();
    saveArticleById(this.props.router.params.id,values).then(res=>{
      message.success(res.msg)
    })
  };
```

联调接口？

 传参的个数是否一致。

 传参的字段的数据类型是否一致。

 传参的位置是否一致。（headers | body | query 参数位置确定好）





### 5-5  loading效果

```
state = {
    spinning:false
  }
```

```
<Card title='文章编辑'>
        <Spin spinning={this.state.spinning}>
           <Form/>
        </Spin>
</Card>
```



```
onFinish = (values) => {
    // 将spinning状态变成true
    this.setState({spinning:true})

    // 将currentAt这个字段转成时间戳后，传递给后端
    values.currentAt = values.currentAt.valueOf();
    saveArticleById(this.props.router.params.id,values).then(res=>{
      message.success(res.msg)
    }).finally(()=>{
      this.setState({spinning:false})
       // 保存文章成功后，跳转到文章列表页面
      this.props.router.navigate(-1)
    })
  };
```

```
 componentDidMount(){
    this.initEditor()

    // 需要进行数据请求，表单回填
    this.setState({spinning:true})
    getArticleDetailById(this.props.router.params.id).then(res=>{
      res.currentAt = moment(res.currentAt)

      // 需要调用setFieldValues设置表单字段
      this.formRef.setFieldsValue(res)
      // 设置富文本编辑器content内容
      this.editor.txt.html(res.content)
    }).finally(()=>{
      this.setState({spinning:false})
    })
  }
```







## 六. 通知中心功能

### 6-1 DropDown实现下拉菜单布局

```

  menu = ()=>{
    return (
      <Menu onClick={this.handleClick}>
        <Menu.Item key={'/admin/notifications'}>
          <Badge dot>
            通知中心
          </Badge>
        </Menu.Item>
        <Menu.Item key={'/admin/article'}>
          文章列表
        </Menu.Item>
        <Menu.Item key={'/admin/settings'}>
          设置
        </Menu.Item>
      </Menu>
    )
  }
```

```
<Header className="header qf-header">
    <Dropdown overlay={this.menu()}>
        <Badge count={9} offset={[5,-10]}>
        欢迎您：张三丰 <DownOutlined />
        </Badge>
    </Dropdown>
</Header>
```

```
.qf-header{
  display: flex;
  justify-content: flex-end;
  background: #fff;
  align-items: center;
}
```





最后，创建notifications页面：

```
const Notifications = Loadable({
  loader:()=>import('./notifications'),
  loading:Loading
})
export {
  ArticleList,
  ArticleEdit,
  Dashboard,
  Settings,
  Notfound,
  Login,
  Aaa,
  Notifications
}
```

routes

```
 { path: "/admin/notifications", element: <Notifications /> },
```



### 6-2 通知中心页面实现

```
import React, { Component } from 'react'
import { List, Avatar,Card } from 'antd';
const data = [
  {
    title: 'Ant Design Title 1',
  },
  {
    title: 'Ant Design Title 2',
  },
  {
    title: 'Ant Design Title 3',
  },
  {
    title: 'Ant Design Title 4',
  },
];
export default class index extends Component {
  render() {
    return (
      <Card title={'通知中心'}>
        <List
          itemLayout="horizontal"
          dataSource={data}
          renderItem={item => (
            <List.Item>
              <List.Item.Meta
                avatar={<Avatar src="https://joeschmoe.io/api/v1/random" />}
                title={<a href="https://ant.design">{item.title}</a>}
                description="Ant Design, a design language for background applications, is refined by Ant UED Team"
              />
            </List.Item>
          )}
        />
      </Card>
    )
  }
}
```



### 6-3 借助redux实现状态管理

yarn add redux react-redux redux-thunk

redux遵循单一数据源，store是惟一的，需要创建store文件

src/store.js

```
import {createStore,applyMiddleware} from 'redux'
import reducer from './reducer'
import thunk from 'redux-thunk'
const store = createStore(reducer,applyMiddleware(thunk))
export default store
```



reducer/index.js

```
import {combineReducers} from 'redux'
import notifications from './notifications'
const reducer = combineReducers({
  notifications
})
export default reducer
```



reducer/notifications.js

```

// 分支的reducer文件应该是一个纯函数
// 固定的输入必须要有固定的输出，不能对之前的状态进行任何的更改，返回一个新的状态
// 纯函数中不能做一些异步操作、math.random方法等。

const initState = {
  list:[
    {id:1,title:'1111111111',desc:'1111111111111111111'},
    {id:2,title:'2222222222',desc:'2222222222222222222'}
  ]
}

const reducer = (state=initState,action)=>{
  switch(action.type){
    default:
      return state
  }
}
export default reducer
```



接下来，需要使用redux架构了，需要在最外层的节点上面嵌套Provider，将store向下传递（封装了context上下文）

```
import {Provider} from 'react-redux'
import store from './store'
ReactDOM.render(
  <Provider store={store}>
  <Router>
    <App/> 
  </Router>
  </Provider>,
  document.getElementById('root')
);
```

在Notifications页面中，需要使用到redux的共享状态？需要借助connect方法才可以。

```
import {connect} from 'react-redux'

@connect()
class index extends Component {
```

打印this.props，发现有dispatch，说明组件与redux仓库已经成功建立关联了。



```
const mapState = state => {
  return {
    list:state.notifications.list
  }
}

@connect(mapState)
class index extends Component {
  render() {
    return (
      <Card title={'通知中心'}>
        <List
          itemLayout="horizontal"
          dataSource={this.props.list}
          renderItem={item => (
            <List.Item>
              <List.Item.Meta
                avatar={<Avatar src="https://joeschmoe.io/api/v1/random" />}
                title={<a href="https://ant.design">{item.title}</a>}
                description={item.desc}
              />
            </List.Item>
          )}
        />
      </Card>
    )
  }
}
```



### 6-4 按钮的处理

```

@connect(mapState)
class index extends Component {
  render() {
    return (
      <Card title={'通知中心'} extra={<Button>全部标记为已读</Button>}>
        <List
          itemLayout="horizontal"
          dataSource={this.props.list}
          renderItem={item => (
            <List.Item>
              <List.Item.Meta
                avatar={<Avatar src="https://joeschmoe.io/api/v1/random" />}
                title={<Badge dot><a href="https://ant.design">{item.title}</a></Badge>}
                description={item.desc}
              />
              <Button>标记为已读</Button>
            </List.Item>
          )}
        />
      </Card>
    )
  }
}
```

需要在redux里面，对于每条数据添加hasRead.

```
const initState = {
  list:[
    {id:1,title:'1111111111',desc:'1111111111111111111',hasRead:true},
    {id:2,title:'2222222222',desc:'2222222222222222222',hasRead:false}
  ]
}
```

```

@connect(mapState)
class index extends Component {
  render() {
    return (
      <Card title={'通知中心'} extra={<Button disabled={this.props.list.every(item=>item.hasRead===true)}>全部标记为已读</Button>}>
        <List
          itemLayout="horizontal"
          dataSource={this.props.list}
          renderItem={item => (
            <List.Item>
              <List.Item.Meta
                avatar={<Avatar src="https://joeschmoe.io/api/v1/random" />}
                title={<Badge dot={!item.hasRead}><a href="https://ant.design">{item.title}</a></Badge>}
                description={item.desc}
              />
              { !item.hasRead && <Button>标记为已读</Button>}
            </List.Item>
          )}
        />
      </Card>
    )
  }
}
```



接下来，在Layouts组件里面也是用到了redux状态管理：

```
import {connect} from 'react-redux'

const mapState = state => {
  return {
    notificationsCount:state.notifications.list.filter(item=>item.hasRead===false).length
  }
}

@connect(mapState)
@withRouter
class index extends Component {
```

```
<Header className="header qf-header">
          <Dropdown overlay={this.menu()}>
            <Badge count={this.props.notificationsCount} offset={[5,-10]}>
              欢迎您：张三丰 <DownOutlined />
            </Badge>
          </Dropdown>
        </Header>
```

```
<Menu.Item key={'/admin/notifications'}>
          <Badge dot={this.props.notificationsCount>0}>
            通知中心
          </Badge>
        </Menu.Item>
```



### 6-5 点击按钮触发actions

actions/notifications.js

```
import {MARK_NOTIFICATIONS_BY_ID} from './actionType'
export const markNotificationsById = id => {
  return dispatch => {
    // 因为安装了redux的中间件redux-thunk 后续就可以在此处写异步操作了。
    setTimeout(() => {
      dispatch({  //1s以后，通过手动调用dispatch，将具有type信息的action对象交给reducer处理，返回一个新状态，更新界面。
        type:  MARK_NOTIFICATIONS_BY_ID,
        payload:{id}
      })
    }, 1000);
  }
}
```



reducer/notifications.js

```
const reducer = (state=initState,action)=>{  // 根据传递来的action的type匹配，最终返回一个全新的状态
  switch(action.type){
    case MARK_NOTIFICATIONS_BY_ID:
      return {
        ...state,
        list:state.list.map(item=>{
          if(item.id === action.payload.id){
            item.hasRead = !item.hasRead
          }
          return item
        })
      }
    default:
      return state
  }
}
```



需要在Notificaiton.jsx页面中调用actionCreators方法？

```
import {markNotificationsById} from '../../actions/notifications'

@connect(mapState,{markNotificationsById})
class index extends Component {

	{ !item.hasRead && <Button onClick={this.props.markNotificationsById.bind(this,item.id)}>标记为已读</Button>}
}
```

当reducer返回新状态的时候，容器组件就会知道状态发生变化了，然后通过props的方式将最新的状态传递给展示组件，展示组件外部接收到了属性发生改变了，从而render渲染。（初始化、props/state/forceUpdate）



实现全部标记为已读：

```
export const markNotificationsAll = ()=>{
  return dispatch => {
    setTimeout(() => {
      dispatch({
        type:MARK_NOTIFICATIONS_ALL,
      })
    }, 1000);
  }
}
```

```
case MARK_NOTIFICATIONS_ALL:
    return {
        ...state,
        list:state.list.map(item=>{
        	item.hasRead = true  //将所有的都变成已读
        	return item
    	})
	}
```

```
import {markNotificationsById,markNotificationsAll} from '../../actions/notifications'

@connect(mapState,{markNotificationsById,markNotificationsAll})
class index extends Component {
	<Card title={'通知中心'} extra={<Button onClick={this.props.markNotificationsAll} disabled={this.props.list.every(item=>item.hasRead===true)}>全部标记为已读</Button>}>
}
```



### 6-6 模拟通知中心的数据

url:/api/v1/notifications

method:get

headers:{authToken:'xxx'}

res:code:200  data:{list:[{id,title,desc,hasRead}]}



```
// 获取通知中心的数据
export const getNotifications = ()=>{
  return service.get('/api/v1/notifications')
}
```



异步获取通知中心的数据，获取完毕后需要派发给reducer，更改redux的状态list.

```
export const getNotificationsData = ()=>{
  return dispatch => {
    getNotifications().then(res=>{
      dispatch({
        type:NOTIFICATIONS_DATA,
        payload:{
          list:res.list
        }
      })
    })
  }
}
```

```
case NOTIFICATIONS_DATA:
      return {
        ...state,
        list:action.payload.list
      }
```



Layouts.jsx

```
import {getNotificationsData} from '../../actions/notifications'

@connect(mapState,{getNotificationsData})
@withRouter
class index extends Component {
	componentDidMount(){
        // 一进来，需要请求通知中心的数据
        this.props.getNotificationsData()
      }
}
```



index.less

```
.ant-layout-content{
  overflow-y: auto;
}
```



### 6-7 loading的加载

```
const initState = {
  list:[],
  loading:true  //正在加载
}
```



Notifications.jsx

```
const mapState = state => {
  return {
    list:state.notifications.list,
    loading:state.notifications.loading
  }
}

<Spin spinning={this.props.loading}>
```



actions/notifications.js

```
const startNotifications = ()=>{
  return {
    type: START_NOTIFICATIONS
  }
}
const endNotifications = ()=>{
  return {
    type: END_NOTIFICATIONS
  }
}
```

```

export const getNotificationsData = ()=>{
  return dispatch => {

    // 需要派发开始的action对象给reducer处理
    dispatch(startNotifications())
	// 异步获取数据派发给reducer更改list状态
    getNotifications().then(res=>{
      dispatch({
        type:NOTIFICATIONS_DATA,
        payload:{
          list:res.list
        }
      })
    }).finally(()=>{
      // 需要派发结束的action对象给reducer处理
      dispatch(endNotifications())
    })
  }
}
```

```
case START_NOTIFICATIONS:
      return {
        ...state,
        loading:true  // 正在加载中
      }
    case END_NOTIFICATIONS:
      return {
        ...state,
        loading:false   // 结束了
      }
```



## 七. 登录实现

### 7-1 login页面

```
import React from 'react'
import { Form, Input, Button, Checkbox } from 'antd';
import './index.less'
export default function index() {
  const onFinish = (values) => {
    console.log('Success:', values);
  };

  const onFinishFailed = (errorInfo) => {
    console.log('Failed:', errorInfo);
  };
  return (
    <Form
      name="basic"
      initialValues={{
        remember: true,
      }}
      onFinish={onFinish}
      onFinishFailed={onFinishFailed}
      autoComplete="off"
      className='myform'
    >
      <h3>千锋教育后台登录系统-Admin</h3>
      <Form.Item
        label="Username"
        name="username"
        rules={[
          {
            required: true,
            message: 'Please input your username!',
          },
        ]}
      >
        <Input />
      </Form.Item>

      <Form.Item
        label="Password"
        name="password"
        rules={[
          {
            required: true,
            message: 'Please input your password!',
          },
        ]}
      >
        <Input.Password />
      </Form.Item>

      <Form.Item
        name="remember"
        valuePropName="checked"
      >
        <Checkbox>Remember me</Checkbox>
      </Form.Item>

      <Form.Item
      >
        <Button type="primary" htmlType="submit">
          Submit
        </Button>
      </Form.Item>
    </Form>
  )
}

```

index.less

```
.myform{
  position: fixed;
  top:50%;
  left:50%;
  width:500px;
  transform: translate(-50%,-50%);
  button{
    width:100%;
  }
  h3{
    text-align: center;
  }
}
```



接下来需要写登录模块的接口：

url   /api/v1/login

method: post

body: {username,password}

res: code:200   data:{id,avatar,displayName,authToken}



request

```
// 用户登录接口
export const loginRequest = (data)=>{
  return service2.post('/api/v1/login',data)
}
```



将用户相关状态需要通过redux进行管理，所以reducer/index.js

```
import {combineReducers} from 'redux'
import notifications from './notifications'
import user from './user'
const reducer = combineReducers({
  notifications,
  user
})
export default reducer
```



reducer/user.js

```
// 需要定义用户的初始化状态
const initState = {
  id:'',
  avatar:'',
  displayName:'',
  isLogin:false  //默认用户未登录
}

const reducer = (state=initState,action)=>{
  switch(action.type){
    default:
      return state
  }
}
export default reducer
```



actions/user.js

```
const loginSuccess = userData => {
  return {
    type:LOGIN_SUCCESS,
    payload:{userData}
  }
}

const loginFailed = userData => {
  return {
    type:LOGIN_FAILED
  }
}

export const login = (userInfo)=>{
  return dispatch=>{
    loginRequest(userInfo).then(res=>{
      if(res.data.code === 200){
        dispatch(loginSuccess(res.data.data))
      }else{ //如果失败，需要派发失败的action对象给reducer处理
        dispatch(loginFailed())
      }
    })
  }
}
```



reducer

```
switch(action.type){
    case LOGIN_SUCCESS:
      return {
        ...state,
        ...action.payload.userData,
        isLogin:true  //用户登录成功
      }
    case LOGIN_FAILED:
      return {
        ...state,
        isLogin:false //用户登录失败
      }
    default:
      return state
  }
```



index.js

```
function App(){
  const isLogin = useSelector((state) => state.user.isLogin)
  let element = useRoutes(routes);
  if(isLogin){
    return element
  }else{
    return <Login/>
  }
}
```



### 7-2 token存储

```

export const login = (userInfo)=>{
  return dispatch=>{
    loginRequest(userInfo).then(res=>{
      if(res.data.code === 200){
        console.log('res===>',userInfo,res.data.data)
        if(userInfo.remember){
          localStorage.setItem('authToken',res.data.data.authToken)
        }else{
          sessionStorage.setItem('authToken',res.data.data.authToken)
        }
        dispatch(loginSuccess(res.data.data))
      }else{ //如果失败，需要派发失败的action对象给reducer处理
        dispatch(loginFailed())
      }
    })
  }
}
```

```
const isLogin = Boolean(localStorage.getItem('authToken')) || Boolean(sessionStorage.getItem('authToken'))
```



### 7-3 用户名显示

```
const mapState = state => {
  console.log('state==>',state)
  return {
    notificationsCount:state.notifications.list.filter(item=>item.hasRead===false).length,
    displayName:state.user.displayName,
    avatar:state.user.avatar
  }
}
```

```
<Header className="header qf-header">
          <Dropdown overlay={this.menu()}>
            <Badge count={this.props.notificationsCount} offset={[5,-10]}>
              欢迎您：<Avatar src={this.props.avatar}></Avatar>{this.props.displayName} <DownOutlined />
            </Badge>
          </Dropdown>
        </Header>
```



但是浏览器已刷新的时候，发现头像与用户名没有了。因为已刷新重置了。

将用户信息存储在本地存储中才可以。

actions/user

```
const loginFailed = userData => {
  localStorage.removeItem('authToken')
  localStorage.removeItem('userData')
  sessionStorage.removeItem('authToken')
  sessionStorage.removeItem('userData')
  return {
    type:LOGIN_FAILED
  }
}

export const login = (userInfo)=>{
  return dispatch=>{
    loginRequest(userInfo).then(res=>{
      if(res.data.code === 200){
        const {
          authToken,
          ...userData
        } = res.data.data
        if(userInfo.remember){
          localStorage.setItem('authToken',authToken)
          localStorage.setItem('userData',JSON.stringify(userData))
        }else{
          sessionStorage.setItem('authToken',authToken)
          sessionStorage.setItem('userData',JSON.stringify(userData))
        }
        dispatch(loginSuccess(res.data.data))
      }else{ //如果失败，需要派发失败的action对象给reducer处理
        dispatch(loginFailed())
      }
    })
  }
}
```

reducer/user.js

```
const userData = JSON.parse(localStorage.getItem('userData')) || JSON.parse(sessionStorage.getItem('userData'))
// 需要定义用户的初始化状态
const initState = {
  ...userData,
  isLogin  //默认用户未登录
}
```





### 7-4 退出功能

```
const loginFailed = () => {
  localStorage.removeItem('authToken')
  localStorage.removeItem('userData')
  sessionStorage.removeItem('authToken')
  sessionStorage.removeItem('userData')
  return {
    type:LOGIN_FAILED
  }
}

export const logout = ()=>{
  return dispatch=>{
    dispatch(loginFailed())
  }
}
```



reducer/user.js

```
 case LOGIN_FAILED:
      return {
        id:'',
        avatar:'',
        displayName:'',
        isLogin:false //用户登录失败
      }
```



Layouts.jsx

```
import {logout} from '../../actions/user'

@connect(mapState,{getNotificationsData,logout})
```

```
menu = ()=>{
    return (
      <Menu onClick={this.handleClick}>
        <Menu.Item key={'/admin/notifications'}>
          <Badge dot={this.props.notificationsCount>0}>
            通知中心
          </Badge>
        </Menu.Item>
        <Menu.Item key={'/admin/article'}>
          文章列表
        </Menu.Item>
        <Menu.Item key={'/admin/settings'}>
          设置
        </Menu.Item>
        <Menu.Item key={'/'}>
          退出
        </Menu.Item>
      </Menu>
    )
  }
```

```
handleClick = ({key})=>{
    if(key === '/'){
      // 需要调用actions里面的logout方法
      this.props.logout()
    }
    let {navigate} = this.props.router
    navigate(key)
  }
```

actionCreators的logout方法触发，派发登录失败的action对象给reducer处理，reducer返回新状态，更改isLogin变成false,跳转到登录界面。



