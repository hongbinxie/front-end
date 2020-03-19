> 这是Vue-CLI的笔记，但也会复习下之前的Vue基础
>
> 1、官网：如有不懂，搜索对应工具官网 来查询具体哪个的使用
>
> 2、建议：打开git bash或cmd来输入命令。
>
> ​			淘宝镜像cnpm比npm快
>
> 3、注意：若输入命令后不动、无反应，可能跟网速有关。
>
> 4、稍微了解webpack的话，就知道npm run serve命令在package.json中运行的是"serve": "vue-cli-service serve"。若改成"vue-cli-service serve --open"：表示自动打开浏览器。

# 单双引号、不加的问题

> 变量值赋值的时候要根据是什么类型来给对应的符号
>
> String 字符串 类型的加双引号    name="陈钰";
>
> char  字符   类型的加单引号    sex='男';
>
> boolean 布尔值 类型的不加引号   isShow=true;
>
> number 数字   类型的不加引号   num=18;
>
> 只要不是字符、字符串类型，都不需要加引号

> 在标签中用''。

在vue中也是如此。不过在**data里面的赋值符号**要改一下,**把等号改为冒号**，**把最后面的分号改为逗号**

String 字符串 类型的加双引号    name:"陈钰",

char  字符   类型的加单引号    sex:'男',

boolean 布尔值 类型的不加引号   isShow:true,

number 数字   类型的不加引号   num:18,

# vue的路径问题

./：相对路径

../：相对路径的上级目录

/：绝对路径

@/：一般代表src目录。在根目录/build/webpack.base.conf.js文件中@是配置的，可修改

# 安装vue-cli

> 若在git bash安装失败，则在cmd里运行安装命令

全局安装：

```cmd
npm install -g @vue/cli
```

测试：

```cmd
vue --version
```

# 创建vue项目

## 1.创建项目目录

> cmd、git bash下的创建命令不同。
>
> 若想在git bash使用cmd命令，可为命令添加别名：在`~/.bashrc` 文件中添加`alias vue='winpty vue.cmd`,重启git bash使文件生效

cmd输入：

```cmd
vue create 项目名
```

git bash输入：

```cmd
winpty vue.cmd create 项目名
```

## 2.选择安装方式

> git bash若直接用了cmd命令，则无法切换

1. 运行创建命令后会出现默认安装、可选安装，一般选默认安装
2. 之后按提示走。
3. 通过弹出的url来访问项目。项目正常显示，表示创建成功。

# vue目录结构

这是**基本**目录结构的说明。后期操作中还会操作一些文件，会有更详细的说明。

```
.git（隐藏文件） ===》git init
node_modules	 ===》项目所有依赖的包文件
public			 ===》本地服务的文件夹
	 |index.html ==>主页
src              ===》工作目录
	 |assets     ===》放入资源（图片,css）
	 |components ===》放入组件的
	 |App.vue    ===》根组件
	 |main.js    ===》项目的全局配置
.gitignore       ===》不需要上传到仓库中的文件的配置
babel.config.js  ===》有关babel的配置
package.json     ===》项目基本配置说明
README.md        ===》说明文件

项目网站的访问顺序：先打开index.html ===>main.js ===>app.vue。网站实际是打开app.vue。
```

> 具体看这：
>
> ​	0.访问的具体过程：先访问主页，主页里的id——app对应着main.js里的#app;#app渲染(render)到app.vue中了。
>
> 1. git init文件：方便通过本地传到github仓库或码云仓库上
>
> 2. src：以后操作或写代码最多的目录
>
> 3. .gitignore：如node_modules在这里默认被配置为不上传
>
> 4. bable的配置：让代码兼容性更好
>
> 5. index.html中有：
>
>    nostript标签		网站若禁止JS脚本，会提示标签里内容

# app.vue根组件

> 网站实际打开的是app.vue 根组件。下面简单介绍下组件，后面再详细说。

1. .app.vue是 根 组件（暂时不用理解）。网站默认打开的就是根组件。

2. 组件一般分为3个部分：

   template  ---》放入html代码
   script        ---》放入js代码、导入等。可不用
   style          ---》放入css样式。可不用
3. template里的代码必须有一个父元素。如div
  

# 全局配置main.js

main.js的所有内容在任何组件里都是有效的

# (数据驱动)模板语法和计算属性

> jQuery中是操作DOM，vue中是**数据驱动**
>
> 数据放到哪，怎么放？如放到template的div中。就是通过**模板语法**来放。

1.数据（数据定义）：在script中定义。

```
<script>
export default {
	data(){	//定义，或者用data:function(){}
		return{
		
		}
	}
}
</script>
```

2.模板语法（数据展现）：{{ 数据 }}。放入template中。

3.计算属性（数据操作）：在数据中写入函数、模板简化。

```
computed:{
	函数名：function(){
		return ...
	}
}
```

（来避免在模板中写操作逻辑，使模板太臃肿，不好维护。）

具体如下：

```
<template>
	<div>
		{{ str }}
		<h1>{{ str }}</h1>
		<h2 v-text='str'></h2>
		<input type="text" :value='str'>
		//<h1>{{ str.split("").revserse().join("") }}<h1>//翻转操作。太臃肿
	</div>
		<h1>{{ changeStr }}</h1>//用计算属性后的模板简化：直接填入函数名
</template>

<script>
export default {
	data () {//函数,定义了数据。放入数据
		return {//对象
			str:"你好vue"
		},
		computer:{
			changeStr(){
				return this.str.split("").revserse().join("");//this.逻辑。this表示vue大对象
			}
		}
	}
}
</script>
```

# vue指令

> 什么是指令？在节点上带有v-xxx的内容
>
> 做什么？（单向）绑定数据（也叫插值）、加事件、双向绑定
>
> 面试题——虚拟DOM：
>
> 监听数据变化，若哪个节点变化，哪个节点就重新渲染：如在模板中输入了str跟一个加了改str值的事件。

指令集：指令=‘...’

1.**v-bind**或: （（单向）绑定数据，也叫插值）

v-bind:value	v-bind:text	v-bing:img等

简写	:value	:img等

数据放入位置：scirpt的data()里

2.v-on或@（加事件）

v-on:click	v-on:mouseover等

简写	@click等

函数放入位置：方法属性（跟计算属性放的位置一样）

```
method:{
	函数名(){
	
	}
}
```

3.v-text	文本

4.v-html	文本+html。数据里的html会起作用

5.v-model	数据的双向绑定

```
//如当在页面中的输入框输入数据，则h1的str也会发生变化
<input type="text" v-model='str'>
<h1>{{ str }}</h1>
双向绑定的原理：
发布者——》订阅者的一种模式：如上面，h1订阅了input，等后者发布了订阅者会跟着变。
```

6.v-once	也可以插入值，但不更新数据（即v-model改变不了它）

7.v-if、v-else	条件渲染

如在数据中输入了一个数组arr。在模板中进行条件选择：不空显示h1内容，空显示h2

```
<h1 v-if='arr.length>0'>{{arr}}</h1>
<h2 v-else>空的</h2>
```

8.v-for	列表渲染

> v-for若报错key，就在其后添加如:key="'arr'+item"、:key="'arr'+index"  或者关闭eslint检测

​	v-for='item in arr'	内容输入{{item}}，显示每项

​	v-for=‘(item,index) in arr’	内容输入{{item}}、{{index}}，显示每项及下标

🔺v-if、v-for结合使用 会出现的问题：v-if不能放li里，应放在ul里，否则会报错。

# 组件

> 组件名后缀在导入使用时可省略。

**1.什么是组件**

- 以.vue结尾的文件
- 扩展了html标签的：能把组件当标签用

**2.组件的使用**

- 使用场景：把一个完整的项目，拆分成不同的功能模块

- 放在哪：src下的components目录

- 注意：组件首字母要大写，才会与标签不冲突

- 怎么使用：（三步）

  1、`import 组件名 from '路径和组件名'   `

   2、export default{}中插入

  ```
  components:{
  	组件名
  }
  ```

  3、在template中使用：组件名--->即把组件当标签用（也可以单标签：`<组件名 />`）

**3.组件的通信(传值)**

## 父传子

（分发）

方法——

父组件：`<子组件  :变量='数据'></子组件>`(一般变量名和数据名保存一致，易区分)

子组件：export default{}中插入`props:['变量']`；模板语法

## 子传父

方法——

子组件：事件；`this.$emit('自定义事件名称',数据)`

```
this.$emit('changStr',this.str)
```

父组件：<子组件 @自定义事件名称=父自定义事件></子组件>去拿到子组件的值

```
<Header @changStr='headStr'></Header>
methods:{
  headStr(s){
     console.log(s)
  }
}
```

## 兄弟之间传

1、先（如在components）弄一个公共的.js文件：实例化vue的

```
import Vue from 'vue'	//引入vue

export default new Vue; //用ES6语法抛出去这个实例
```

2、

兄弟A：引入公共文件`import 公共文件名 from '路径和公共文件名'`、`公共文件名.$emit('自定义事件名',数据)`去分发

兄弟B：引入公共文件`import bus from './bus'`、**找个位置放B自定义方法去存A的数据**、用生命周期或 计算属性去响应。

```
//计算属性做。用生命周期的后期讲。
computed:{
	B自定义方法名(){
		公共文件名.$on('A自定义事件名',function(data){
			console.log(data)
		})
	}
}
```

## 组件传值的注意点

组件的传值，不能跳跃。

举例：切换城市页面

# 路由

> 路由官网：https://router.vuejs.org/api/#to

**1.什么是路由**

单页面应用(spa)：只在一个页面中切换内容，如APP

**2.路由安装**

创建-》选择自定义安装-》选router（按空格）-》一路回车，开始安装。

> 测试：按提示输入命令后，查看效果——
>
> 1.页面：多了个菜单选项，可以切换了，这就是由。
>
> 2.文件：src中多了route.js文件；src中多了views(视图层)文件夹，里面有2个组件

**3.**

## **路由完整流程**

1、在App.vue中页面布局template（先用工具构思个草图）

​	切换的内容？`<router-view></router-view>`

​	跳转到哪了？如`<router-link to='/home'>首页</router-link>`   （路径自定义）

2、创建跳转到的内容(.vue)

​	 各组件的内容写好。放在view目录下 或 不要view目录，全部放在components目录下。

3、配置router.js

```
import 组件名 form '路径+组件名1'
import 组件名 form '路径+组件名2'

router: [	//router里其它东西先清空，后面会用懒加载
	{
		path:"自定义路径",
		component:组件1
	},
	{
		path:"自定义路径",
		component:组件2
	}	
]
```

> 注意：
>
> ```
> import Vue from 'vue'	//引入vue.js：代表router依赖于vue.js
> import Router from 'vue-router' //引入了vue-router.js
> Vue.use(Router)	//使用：如果vue-router依赖于vue.js，必须要有use
> ```

## 通过to跳转 ：router-link配置

`<router-link></router-link>`		

属性：to、tag		样式属性：.router-link-active

```
to 的写法(基本写法+绑定写法2-5)	
		1》to='/home'
		2》:to='"/home"'	使用率不高
		3》:to='{path:"/home"}'		推荐、使用率高
		4》:to='{					可以传参数，能在url上看到
					path:"/home",
					query:	{userId:123}
				}'
		5》:to="{ 					可以床参数，通过JS去接收的
					name: 'user', 
					params: { userId: 123 }
				}"

tag：router-link默认为a标记，可以修改
	tag='li'
	tag='button'

router-link-active：默认触发的class类	
<style scoped>
.router-link-active{
	color:red;
}
</style>
```

## 通过JS跳转

> 有5种方法：router.push、router.replace（替换路由）、router.go（刷新）、router.back、router.forward
>
> 下面举例

1、给如按钮 的跳转目标 加`@click='事件名'`

2、在script写：

```
method:[
	事件名(){
		this.$router.push({
			path:"/config"
		})
	}
]
```

## router-view的keep-alive

**1.keep-alive是什么？**

vue内置的组件，能在组件切换过程中将状态保存在内存中，**防止dom重复渲染**

**2.使用场景**

把页面保存在内存中，记住输入的内容（如密码）等操作

**3.使用与需求**

	<keep-alive>
		<router-view></router-view>
	</keep-alive>
需求：有的页面需要保存，有的不需要

	include属性 : 包含哪个。用,隔开（要给那个页面加数据name）
	exclude属性 ：不包含哪个。用,隔开(要给那个页面加数据name)
## router.js详解(懒加载、重定向、嵌套)

> mode: 'history'	是否加锚点的，默认即可
>
> base: process.env.BASE_URL	默认即可

一、说明

	{
	  path: '/',      //自定义url路径
	  name: 'home',   //名称:基本上做标识或者判断。可省略
	  component: Home //对应访问的组件
	}

二、懒加载

> 提高加载速度：把不同路由对应的组件分割成不同的代码块

	{
	  path: '/about',
	  name: 'about',
	  component: () => import('./views/About.vue')
	}

三、路由重定向

链接不存在，跳转到 提示页或首页。若没有，则内容为空

	{ 
	  path: '*', 
	  redirect: Home或"/home"	前者可能不行
	}

四、路由嵌套

通过children往里去套路由（即主栏目下有二级栏目，如列表页有文章）

	{
	  path: '/about',
	  name: 'about',
	  component: () => import('./views/About.vue'),
	  children:[
	      {
	        path:"/xxx:id",		还能加id
	        component:Home
	      },
	      {
	        path:"/xxx",
	        component:Home
	      }
	  ]
	}
## 路由的传值

如传：在router.js中某个路由**通过路径**加个id，在到url里输/aa  或  app.vue中加个router-link的query，要拿到id

拿：通过在该路由里加**模块语法、计算属性**来**拿到this.$route**，再通过“.”进行判断、拿值

```
1》
{
    path: '/about/:id',
    name: 'about'
}
2》
<router-link :to="{path:'/about',query:{
aaa:123
}}">About</router-link>
```

# 交互(axios的基本用法)

> 使用vue中，怎么与后台进行接口交互。
>
> 知识前提：先了解Promise，用起axios会轻松很多
>
> 后期数据的渲染、逻辑的判断放到项目中再说

1、**axios**的优势：它不依赖于vue，所以不需要use

2、大致使用：

```js
1》在目录中下载：npm install axios --save
2》引入axios
//注意：1、希望所有页面都能用：就在main.js中去引入
//     2、希望只有某一组件能用:就在某一组件中去引入
	import axios from 'axios'
	Vue.prototype.axios = axios		//JS原型
3》再使用(this.axios)
	this.axios.get("路径").then()
```
3、具体过程：get和post举例——

一、假如在App.vue中去使用get方式

（1）假设我们有数据：先在bublic里创建个data.json，随便输：{”a“:1}，然后去请求它，注意路径该这么写：'http://localhost:8080/data.json'

（2）在App.vue中输入

```js
<script>
export default {
  computed:{
    http:function(){
      //1、可以先console.log(this.axios) 测试能否使用
      //2、.then可以放到下一行，这时Promise的语法
      //3、该如何请求接口？axios跟ajax一样可以post、get，这儿我们先使用下get
      return this.axios.get('http://localhost:8080/data.json')
      .then((res)=>{	//4、请求的数据在哪？在.then()上
        console.log(res.data)//首先传入参数res拿到数据，发现在res的data上，所以res.data就可以拿到这个对象了，再.a就可以拿到1了。
      })
    }
  }
}
</script>
```

（2）数据怎么传给后台？

- 可以用get方法：直接在''”里接着写?id=1：(当然现在看不出来)

  `this.axios.get('http://localhost:8080/data.json?id=1').then()`

- 也可以下面的方式

```js
computed:{
    http()=>{			
      this.axios.get('http://localhost:8080/data.json',{
        params:{	//这样也是可以的
          id:1
        }
      })
        .then((res)=>{
          console.log(res.data)
        })
}
```

二、假如在App.vue中去使用post方式

跟上面类似

```js
computed:{
    http()=>{			
      this.axios.post('http://localhost:8080/data.json',{
        params:{	//post可以直接省略params,直接写id:1
          id:1
        }
      })
        .then((res)=>{
          console.log(res.data)
        })
}
```

# 生命周期（又叫钩子函数）

> 就是从有到无的过程。
>
> 使用率100%

一、生命周期（又叫钩子函数）

> 实例化-》**初始化（有两个生命周期beforecreate、created）**-》el（#app）：NO的话就停止（直到加载调用时继续往下走）；YES继续往下走-》template（组件），YES 就-》组件渲染，相当于JS的onload（有两个生命周期beforeMounte、Mounted）-》**数据的修改（有两个生命周期beforeUpdate、Updated）**-》**销毁（有两个生命周期beforeDestroy、destroy）**

一共有4个阶段：（每个阶段上都有2个生命周期）

​	1》创建
​	2》组件渲染
​	3》修改数据
​	4》销毁

二、该怎么写？

写在script中

```
beforeCreate(){
    console.log(1)
},
created(){
	console.log(2)
}
```

三、生命周期在什么地方使用？

> 数据是通过axios请求接口来的，再把数据渲染到页面中，那在什么地方写这些逻辑？而一旦刷新或进入页面时，就要请求接口，所以我们只能写到mounted(){...}中

使用场景：比如在一刷新（或进入）页面要请求接口。

​				   比如使用keep-alive后，会去增加2个生命周期，后期再说

举例：

1、比如我们定义一个接口data.json,写入{"arr":["a","b","c"]}，然后就可以直接在mouted里去axios：

```
mounted(){
	this.axios.get('http://localhost:8080/data.json')
      .then((res)=>{	
        console.log(res.data)
      })
}
```

2、然后可以进行逻辑判断了，比如渲染数据

```
<ul>
	<li v-for='item in str' :key="'str'+item">
		{{item}}
	</li>
</ul>
...

mounted(){
	this.axios.get('http://localhost:8080/data.json')
      .then((res)=>{	
        this.str = res.data.arr
      })
}
```

# 插件样式

## vue中使用插件

> vue-xxx和xxx的区别：前者是写vue时用的，后者是写DOM结构时用的。vue-xxx的底层的api是xxx。所以看api也可以到xxx官网去看，没有问题
>
> 插件在使用过程中还有很多问题，下一节有讲到

比如想使用一个轮播插件、分享插件等，该如何去找、如何去用？

**怎么用？**

操作步骤永远都是：安装npm i xxx --save、引入、使用

注意：

- 引入要看vue-cli的版本，可能人家说明文档上的方法不行，要百度或经验：比如3中css不能这样引入，需要用其它方法：去xxx官网下载css放到src里的assets文件夹下，在main.js里引用：`import '路径'`
- 插件里的结构，你可以去拷贝来用。ref可以去掉，后面会讲；@..callback可以删了，没有用。:option的值是一个对象，可以在下面定义 或 按人家的写也没有问题：把data(){...}直接拿过来



**怎么找？**

github.com上找插件，直接搜索。

比如：

- 搜vue分享插件，里面会告诉你怎么去用
- 搜vue-xxx(比如我们要用swiper，是要搜vue-swiper，不能直接搜)

> 可能会遇到Vue.component() 表示能在全局使用该组件

## 样式模块化(局部化)

任何组件的style默认是全局使用的。

要只有这个组件自己才能使用，给style加个scoped属性

## 样式穿透(改样式)

> 这儿讲下swiper的使用：不要的功能可以在结构里删除，如果想要swiper轮播图的小圆点，就去swiper官网里找组件-》分页器，可以把代码拿过来 或看tab里有很多其它样式。

- 语法：父元素 >>> 子元素

比如 想修改小圆点的样式，就要找到该元素类的父元素的类，然后`.父元素类 >>> 子元素类 {...}`

## 预处理器stylus

> - CSS预处理器：都是为了让开发效率变高
> - 如何用less、sass、stylus写？步骤一样
> - stylus语法类似于sass，写样式时可以不写{}

**1、安装**

创建项目时要选择CSS Pre-processors-》Stylus-》一路回车等待安装完成

**2、使用**

- `<style lang='stylus'></style>`

- 写样式时可以不写{}

- 比如换主题（如植树节换绿色、国庆换红色）-》**不用一个个去修改，可以像JS一样修改一个变量即可**-》**1.stylus可以用变量**

- **2.stylus的文件是.styl**：比如写个var.styl文件，写$bg=red（**3.stylus语法**），然后有个元素想用红色-》在想改样式的组件中`<style lang='stylus'></style>`中写入`@import '~@/assets/var.styl'`（**style中的样式引入**），然后改样式

  ```css
  p 
   background:$bg
  ```

到这，基础差不多就讲完了，一些细节问题会在后面做项目中讲到

# vuex状态管理

> 知道修改的过程就可以了

**1、vuex是什么？**

状态管理——管理所有组件的事件、行为等，方便更好传值，**解决传值比较麻烦的情况**

图：vue组件作为一个等待者...

**2、vuex的安装**

安装时选Vuex，一路回车就行。

变化：

- src目录会多个store.js文件
- main.js中会引入store、实例化中把store挂载到了#app上

**3、vuex的使用**

1、vuex-state-mapState

（1）**state** ——》放入的是数据

> 到真正做项目时，数据都是放到store里面，否则传值太累

（2）组件如何使用数据？(3种)

- {{ this.$store.state.cityName }}

- ```js
  //推荐
  import {mapState} from 'vuex'
  ...
  	computed:mapState(['cityName'])	//跟原本的computed不冲突
  
  {{cityName}}
  ```

- ```js
  import {mapState} from 'vuex'
  ...
      computed:{
          datas(){
              return 123
          },
          ...mapState(['cityName'])	//这样去写:使用扩展运算符
      }
  
  {{datas}}  {{cityName}}
  ```

2、修改state数据-mapMutations

> actions和mapMutations都可以改，前者是异步的,比较麻烦需要用commit提交

（1）比如在state里写了str:123，点击按钮想改变str的值：

```js
{{ str }}
<button @click='btn'>按钮</button>

	methods:{
        btn(){
            //console.log(this.str)
            //this.str = 456  //会报错：不能直接改，看下面
        }
    }
```

（2）怎么修改？4步

```js
1》store.js

mutations: {
    changeStr(state){
        state.str=456;		//1.
    }
}

2》组件
import {mapState,mapMutations } from 'vuex'	//2.
<button @click='btn'></button>

methods:{
    btn(){
        this.changeStr()			//4.
    },
    ...mapMutations(['changeStr'])	//3.
}
```

假如`<button @click='btn("北京")'></button>`想传个北京怎么办呢？

```
mutations: {
    changeStr(state,cName){
    	state.str=cName;	
    }
}

methods:{
    btn(cName){
        this.changeStr(cName)		
    },
    ...mapMutations(['changeStr'])	
}
```



# 必问面试题

1.虚拟DOM：

监听数据变化，若哪个节点变化，哪个节点就重新渲染：如在模板中输入了str跟一个加了改str值的事件。

2.双向绑定的原理：

发布者——》订阅者的一种模式。

```
//如h1订阅了input，等后者发布了订阅者会跟着变。（具体操作：当在页面中的输入框输入数据，则h1的str也会发生变化）
<input type="text" v-model='str'>
<h1>{{ str }}</h1>
```

3、[生命周期](#生命周期（又叫钩子函数）)