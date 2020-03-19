# MVC模式和MVVM模式

1、MVC模式：

Model——》模型——》数据（js变量）

View——》视图——》用户所见界面（HTML，CSS）

Control——》控制器——》事件交互——》如何根据视图与用户交互后改变数据（通过DOM对象1绑定事件，将变量进行修改）

2、MVVM模式

视图（view）跟数据（model）通过vue（vm）进行双向绑定

```
<!-- view -->
<div id="app">
	{{message}}
</div>
			
<script>
			
	//vm
var app = new Vue({
	el:"#app",
	//model
    data:{
		message:"Hello World!"
	}
})
```

# 一、vue.js基础

# vue的基本使用

怎么使用？

1、在html引用vue.js。（就产生了Vue这个全局变量，可以`console.log(Vue)`打印下）

2、写绑定的模板：给div一个id或class，告知vue：要在什么地方使用vue（的模板变量{{变量}}）

3、实例化对象，在()里配置参数：

```js
let app = new Vue({
    el: "#app",	//告诉在哪使用vue
    data:{		
      title: "Hello Vue!"  		//告诉vue变量是什么
    }
})
```

(在这之后也可以`console.log(app)`打印下；可以输入`app.message=“呼呼”`，message就改变了，这就是双向绑定)

（这种模式存在问题：是替换的！Vue找到innerHTML，再去替换它——牺牲性能：用户有可能看到替换前的，影响体验。所以后面是用自动化打包工具vue-cli：先编译，绑定内容）

# 条件渲染v-if、v-show

1、v-if（、v-else、v-else-if）	不显示时，第一次就直接不渲染；若将显示内容改为不显示，将内容直接从DOM去除。建议**只是渲染一次**，用v-if。

- 值允许写表达式
- 注意：v-if和v-else、...中间不能有其它的元素，否则报错：`v-else used on element <p> without corresponding v-if`。
- 例子：

```html
<div class="app">
	<p>用户名：{{userName}}</p>
	<p v-if="vip > 998">用户等级：高级VIP</p>
	<p v-else-if="vip > 499">用户等级：普通VIP</p>
	<p v-else>用户等级：普通用户</p>
</div>

<script type="text/javascript">
	var app = new Vue({
		el: ".app",
		data: {
			userName: "小明",
			vip: 999
		}
	})
</script>
```

2、v-show 	不显示时，就会改成display:none,会渲染在DOM上。建议**反复需要切换**的内容，使用v-show。

- 值允许写表达式

```html
<div id="app">
	<div v-show="isShow">
		Hello Vue
	</div>
	<button @click="showBtn">切换显示按钮</button>	<!-- 绑定点击事件 -->
</div>
	

<script>
	var app = new Vue({
		el:"#app",
		data:{
			isShow:true
		},
		methods:{
			showBtn:function(){			    //要将事件函数写在method中
				this.isShow=!this.isShow;	//注意：函数内语句;建议写上。可以用app或this
			}
		}
	})
</script>
```

（添加事件之后，可以给事件传个参数e，在事件内添加`console.log(e)`打印下事件对象）

3、练习题：Tab切换

```html
<p v-show="tab==1">这是首页</p>	<!-- 注意这里只能使用== -->
<p v-show="tab==2">这是热门</p>
<p v-show="tab==3">这是我的</p>
<button @click = "changeTab" data-id="1">首页</button> <!-- data-id设置鼠标事件id -->
<button @click = "changeTab" data-id="2">热门</button>
<button @click = "changeTab" data-id="3">我的</button>

<script>
	var app = new Vue({
		el: "#app",
		data: {
			tab: 1
		},
		methods:{
			changeTab:function(e){	
				//console.log(e)   //查看e来获取id
				var tabId = e.target.dataset.id; //获取id	
				this.tab = tabId;	//将tab赋值为id
			}
		}
	})
</script>
```

# 列表渲染v-for

> 列表渲染常与条件渲染一起使用，系统会先循环后判断

v-for		循环反复做什么事

知识复习：一般数组[1,"1"] 	对象{a:小明,b:"12"}   对象数组[{a:小明,b:"12"},{a:小红,b:"18"}]

**1、关键点：3种情况**

```html
<!-- 下面的item、key可以随便改 -->
<!-- 1、一般数组列表 -->
<ul>
	<!--循环数据的每一项 in 要循环的数据-->
	<li v-for="item in stars">   
		<!--拿到每一项-->
        {{item}}
	</li>
</ul>

<!-- 2、对象数组列表（拿属性）-->
<ul>
	<!--数据的每一项 in 要循环的数据-->
	<li v-for="item in stars"> 
        <!--拿到每一项（对象）的属性用.调用-->
		名字：{{item.name}}
        性别：{{item.sex}}
	</li>
</ul>

<!-- 对象数组列表（拿属性、索引值）。注意()，否则不规范-->
<ul>
	<!--数据的每一项 in 要循环的数据-->
	<li v-for="(item,key) in stars">
        <!--拿到索引、属性-->
		索引值：{{item.key}}、名字：{{item.name}}
	</li>
</ul>

<!-- 3、对象列表（拿数组里的对象1、对象1里的索引值）-->
<ul>
	<!--数据的每一项 in 要循环的数据（拿对象1）-->
	<li v-for="(item,key) in stars[0]">
        <!--拿对象1-->
		key:{{key}}--value:{{item}}
	</li>
</ul>
```

**2、**

## **列表条件渲染结合使用**

注意点——添加元素属性`key`：

- 若赋值是vue数据，则要用":"绑定：`:key`
- 若赋值是字符串，则不用绑定：`key`

做标识，**避免让vue重复使用内容**。因为若做了修改，系统会在原来界面上修改、去复用、**保留原先数据**而不重新渲染，可能**导致数据冲突**：如登录、注册页面的切换。若只是简单切换，可以不用加key。

# 模板语法(绑定)

## 插值(绑定数据)

**{{}}	可反复插值。可在数据里写简单的表达式**（若表达式内容要反复修改、写复杂表达式，则在计算属性中写。否则会降低性能）

v-once、{{}}		一次性插值：如`<p v-once>这个将不可改变:{{msg}}</p>`

v-html、{{}}		可使值里的html生效。不建议使用，会被XSS攻击！如会被上							传注入如js文件、ajax、跳转到钓鱼网站等。

## 绑定属性

v-bind:	可简写为":"。如`<p :id="tab">收藏</p>`

## 绑定事件

v-on:   可简写为“@”。

1、最基本使用：添加事件名

如`<button @click=“changeBg”></button>	`	

vue实例中添加：	

```js
//2种声明形式都行。
methods:{
	函数名:function(){	//声明形式1：匿名函数
		...
	}
    
	函数名:()=>{	//声明形式2：ES6箭头函数——（...参数）=>{函数声明}
		...
	}
}
```

2、添加表达式

```html
html的：
<div id="app">
	<h1>点击次数：{{count}}</h1>
	<!-- 可以使用表达式完成事件操作 -->
	<button type="button" @click="count+=1">点击</button>
</div>

js的：
data:{
	count:0
}
```

3、获取事件对象

```html
html的：
<div id="app">
    <h1>点击次数：{{count}}</h1>
	<!-- 获取事件对象 -->
	<button  @click="clickEvent">点击2</button>
</div>

js的:
methods:{
    clickEvent:function(event){
        console.log(event)
        console.log(this)
        this.count++;
    }
}
```

4、事件传参

例子：通过点击获取id

```html
<div id="app">
	<ul>
		<li v-for="item,index in stars" @click="clickEvent(index,item,$event)">索引值：{{index}}----内容：{{item}}</li> <!-- index、item传到事件里 -->
	</ul>
</div>

<script type="text/javascript">
	var app = new Vue({
		el:"#app",
		data:{
			stars:['蔡徐坤','范冰冰','李晨']
		},
		methods:{
			clickEvent:function(index,value,event){
				console.log(index)
				console.log(value)
				console.log(event)
				alter(123)
			}
		}
	})
</script>
```

### 事件修饰符

要用时，再来官网翻就好了，不需要记

- `.stop`		阻止事件冒泡（即几个嵌套事件，阻止事件继续向上层触发）

  ```html
  <div class="btnParent" @click="clickParent">
      <!-- stop修饰符，阻止冒泡事件向上传递 -->
  	<button @click.stop="clickEvent">按钮</button>
  </div>
  
  methods:{
      clickEvent:function(event){
      	console.log("clickEvent")
      },
      clickParent:function(){
      	console.log("clickParent")
  	}
  }
  ```

- `.prevent`     阻止默认事件。就可以不用跳转页面，而可以进行ajax请求。如表单提交

  ```html
  <form action="" method="post">
  		<input type="text" name="username" id="" value="" />
  		<!-- 阻止默认事件 -->
  		<input @click.prevent="searchWeather" type="submit" value="提交"/>
  </form>
  ```

  ```js
  searchWeather:function(){
      console.log("查询天气")
  }
  ```

- `.capture`    

- `.self`     自身触发的内容

- `.once`      只触发一次，如抽奖活动

  ```
  <h1>只触发一次修饰符</h1>
  
  <button type="button" @click.once='onceEvent'>只触发一次按钮</button>
  
  onceEvent:function(){
  	console.log('只触发一次')
  }
  ```

- `.passive`

- .keydown     按键。其它的看官网，还可以自定义。

  - 如按回车才能触发 `@keydown.enter="searchWeather"`
  - 按F1：Vue.config.keyCodes.f1 = 112    F1的键值就是112
  - 若既想要回车、又想F1：`@keydown.enter.f1="searchWeather"`

### 案例：查询天气，跟回车键才能触发

```html
<div id="app">
	<form action="" method="post">
		<!-- 绑定输入框回车事件 -->
		<input type="text" @keydown.enter.f1="searchWeather" name="username" v-model="city" id="" value="" />
        
		<!-- 阻止默认事件 -->
		<input @click.prevent="searchWeather" type="submit" value="提交"/>
	</form>
	<div id="weather">	//显示天气内容
		<h1>{{tmp}}</h1>
		<h3>{{brief}}</h3>
	</div>
	
	<button type="button" @click.ctrl.exact="ctrlEvent">按住ctrl事件</button>
</div>

<script type="text/javascript">
    
	// 配置按键的自定义修饰符
	Vue.config.keyCodes.f1 = 112
    
	var app = new Vue({
		el:"#app",
		data:{
			city:"广州",
			tmp:"",
			brief:""
		},
		methods:{
			searchWeather:async function(){
				console.log("查询天气")
				console.log(this.city)	//拿到值就可进行ajax了：可以引用JQ的或原生的，比如找和风天气的api
				let httpUrl = `https://free-api.heweather.net/s6/weather/now?location=${this.city}&key=3c497450d8e44c5280421ceaba1db581`//你要请求的地址
				let res = await fetch(httpUrl)	//开始做ajax请求：用异步或ES6箭头函数都可以
				let result = await res.json()//异步，所以要等待。到这就拿到了，可以打印查看。提交查看对应地址的数据
				console.log(result)
				let now = result.HeWeather6[0].now; //细化数据
				this.tmp = now.tmp;//细化数据：温度
				this.brief = now.cond_txt;//细化数据：多云
			},
			ctrlEvent:function(){
				console.log('ctrlEvent')
			}
		}
	})
</script>
```

## 计算属性

应用场景：

**若表达式内容要反复修改、写复杂的表达式**(如循环条件渲染，要反复地先循环后判断，比较消耗性能)

- 在一次修改情况下，它和{{}}性能相同
- 若要反复修改、写复杂的表达式，则计算属性 性能更好：因为它**会将计算结果进行缓存**，只要表达式里数据不改变，就不会重新计算。

{{函数名}}、vue实例中添加：

```
computed:{
	函数名:function(){	//声明形式1
		...
		return	...	  //计算属性必须要有返回值
	}
    
	函数名:()=>{	//声明形式2
		...
		return	...	  //计算属性必须要有返回值
	}
}
```

### 循环条件渲染改进

```html
<!-- 之前已经在vue中添加了student对象数组 -->
<li v-for="item,index in oddStudents">
	<h3>{{item.studentName}}</h3>
	<h4>{{item.age}}</h4>
</li>
```

```js
oddStudents:function(){
	var results = this.students.filter((item,i)=>{	//filter:过滤方法
		return item.age%2==0
	})
	return results
}
```

### 计算属性的setter(了解)

即 计算属性 计算完后，也把计算完后的值给 原来值

内容：

- getter:**计算**后的值
- setter：去**改**原来的值

举例：反转vue数据msg，计算之后也能把msg改成计算值

原来的

```html
{{reverseMsg}}
```

```js
computed:{
    reverseMsg:function(){
        return this.msg.split("").reverse().join("")//分解、反转、连接
    }
}
```

之后的

```
computed:{
    reverseMsg:{
    	get:function(){		//计算
        	return this.msg.split("").reverse().join("")
        },
        set:function(val){		//修改。修改一定要传值
        	this.msg = value.split("").reverse().join("")
        }
    }
}
```

## 侦听器

用来监听数据的变化。建议少用，会消耗性能

如：

```
watch:{
	msg:function(val){		//参数为：要监听变化的值
		console.log("监听事件————msg")
		console.log(val)
	}
}
```

## 绑定类名(5种方式)

用v-bind:绑定类名，使设置样式的方法更灵活

这样就可以不用在想要获取样式时，给它添加class.

注意：可以在已有class的标签上添加，来追加类。

1、放置字符串

```html
<div :class="styleStr"></div>
```

```js
data:{
    styleStr:"abc cba"
}
```

2、通过**对象**的方式决定是否存在某个、多个类。

```html
<style>
	.action{
		width: 200px;
		height: 200px;
		background: skyblue;
	}
</style>
<div :class="{active:isTrue}"></div>
```

```js
data:{
    isTrue:true
}
```

3、直接放置**对象**

```html
<div :class="styleObj"></div>
```

```js
data:{
    styleObj:{active:true,"col-lg-6":true}	//注意：如使用有-的类，如bootstrap类，在对象中是非法的，要用“”括起
}
```

之后就可直接用对象的方式操作

4、放置数组

> 老放true、false太累了，我们可以直接放置数组

```html
<div :class="styleArr"></div>
```

```js
data:{
    styleArr:['col-xs-12','red-bg']
}
```

之后就可直接用数组的方式操作：

添加		如app.styleArr.push('blue-bg')

删除		如app.styleArr.pop()

5、数组和对象混合使用

```html
<div :class="styleArrObj"></div>
```

```js
data:{
    styleArrObj:['col-xs-12',{active:true}]
}
```

## 绑定内联样式

用v-bind:绑定

1、对象方式的变量拼接（太麻烦）

```html
<!-- CSS内联样式变量拼接 -->
<div style="width: 100px;height: 100px;background: skyblue;" 
:style="{ border: borderWidth+'px solid red',padding:paddingWidth+'px' }"></div>
```

```html
data:{
	borderWidth:50,
	paddingWidth:30,
}
```

2、直接放置对象

```html
<div :style="styleObj"></div>
```

```js
data:{
    styleObj:{
        width:"200px",
        height:"300px",
        padding:"50px",
        'background-color':'skyblue'	//或驼峰命名不加引号
	}
}
```

3、直接放置数组

```html
<div :style="styleArr"></div>
```

```js
data:{
    styleArr:[
        {
            width:"200px",
            height:"300px",
            padding:"50px",
            'background-color':'skyblue'
        },
        {
            border:"30px solid yellow"
            }
	]
}
```

小案例：点击按钮，右边弹出侧边栏

用绑定类名实现：

```html
<div id="app">
	<div class="page">
		首页
		<button @click="toggleMenu" type="button">切换侧边栏</button>
	</div>
	<div class="rMenu" :class="{active:isShow}">
		侧边栏
	</div>
</div>
```

```js
methods:{
    toggleMenu:function(){
        this.isShow = !this.isShow;
    }
}
```

用绑定内联样式实现

	<div id="app">
		<div class="page">
			首页
			<button @click="toggleMenu" type="button">切换侧边栏</button>
		</div>
		<div class="rMenu" :style="{transform: 'translateX('+menuWidth+'vw)'}">
			侧边栏
		</div>
	</div>
	<script src="js/vue.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		let app = new Vue({
			el:"#app",
			data:{
				menuWidth:100
			},
			methods:{
				toggleMenu:function(){
					if(this.menuWidth==100){
						this.menuWidth = 70
					}else{
						this.menuWidth = 100
					}
				}
			}
		})
	</script>
## 绑定表单输入v-model

靠`v-model`来完成操作,而不靠{{}}。

input、textarea、

checkbox（注意v-model和v-for不能混合使用，要`:value="item"`）

```html
<h1>复选框:选择喜欢的水果</h1>
<span v-for="item in fruits">
    {{item}}		//显示复选框文本
    <input  type="checkbox" name="fruit" v-model="checkFruits" :value="item" />	//显示复选框选项
</span>
<h2>{{checkFruits}}</h2>	//此处v-model

js的：
data:{
    fruits:['苹果','雪梨',"香蕉","葡萄"],
    checkFruits:[]
}
```

radiobox，与上面类似

```html
<h1>单选框:选择最喜欢的水果</h1>
<span v-for="item in fruits">
    {{item}}
    <input  type="radio" name="zfruit" v-model="radioFruits" :value="item" />
</span>
<h2>{{radioFruits}}</h2>

js的：
data:{
    fruits:['苹果','雪梨',"香蕉","葡萄"],
    radioFruits:""		
}
```

select	注意：不是给option绑定。因为iOS的bug，所以要提供一个值为空的禁用选项

```html
<!-- 单选 -->
<h1>选项框：选择你居住的城市</h1>
<select v-model="chooseCity">
    <option disabled value="">请选择</option>	<!-- 禁用选项 -->
    <option v-for="item in citys" :value="item">{{item}}</option>
</select>
<h3>{{chooseCity}}</h3>

<!-- 多选。要按住ctrl -->
<h1>选项框：选择你喜欢的城市</h1>
<select v-model="moreCity" multiple="multiple">
    <option v-for="item in citys" :value="item">{{item}}</option>
</select>
<h3>{{moreCity}}</h3>

js的
chooseCity:"",
moreCity:[]
```

### 修饰符

.trim 忽略空格 

将字符转变为数字获取：`.number`

```html
<h1>将字符串变为数字获取</h1>
<input type="text" name="age" v-model.number="age" value="" />

JS的：
age:16
```

小案例：todoList

# 过渡动画

提供了transition的封装组件。会自动识别v-if、v-show的true、false

过程：将要过渡的地方**包裹**起来（会给包裹的内容**自动追加**class）；告知transition过渡方式，如`name="fade"`、`name="slideRight"`（属性name会与框架追加的类名一致）；**需要自己写**会追加的类的样式

```css
/* 前缀与自定义的属性相同，后面的不能改。里面内容可 改 */
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
```

过渡的类名

若想用库，则需要自定义过渡的类名，具体到官网看。

# 生命周期

> 直接看官网图就够了。

**1、什么是生命周期？**生命周期到底有哪些阶段？

8个生命周期函数，只需要知道生命周期函数即可。

创建前：此时数据data和事件方法methods还未绑定到app对象上

创建后：数据data和方法methods绑定到应用对象app上

加载前：渲染之前,根据数据生成的DOM对象是获取不到的

加载后：渲染之后,可以获取数据生成的DOM对象

更新：内容已更新完毕

销毁。

# 组件

> 组件相当于一个小应用

**1、创建组件**

```js
Vue.component(“组件名”,{	//创建完后，是全局的	
	template:'<h1>{{laochen}}</h1>',//要设置个模板——写视图内容
	data:function(){	//注意：这儿不再是{}了而是函数，因为组件要反复使用，需要返回一个新的对象。这儿看情况加，看数据是哪给的
    	return {
            laochen:"hello laochen"
        }
	}	
})
```

**2、注册组件**

```js
var app = new Vue({
    el:"#app",
    data:{},
    components:{	//注册组件
        '组件名'
    }
})
```

**3、使用组件**

把组件当标签用，放到其它组件中。

## 父子传值

父组件传值给子组件：1、给子组件设**props的值**，2、往子组件标签的属性里去传值。

```html
<div id="app">
    <ul>
        <!-- 从父组件传值到子组件 -->
        <!-- 显示组件。注意：这儿属性只能用-而不能用驼峰 -->
        <!-- 静态属性：props属性前不加:，就不是动态，不会变 -->
        <school school-name="清华北大"></school>
        <!-- 动态属性。注意这儿的引号：不然动态属性会认为里面是个变量。加了引号就是字符串 -->
        <school :school-name="'上海浙大'"></school>
        <!-- 动态属性 -->
        <school :school-name="schoolList[0]"></school>
        <!-- 循环传值组件：循环，绑定属性、值给好。可以再拿个索引值：定义属性、把index传进去。建议尽量带key，'abc'+可有可不有：key只是给vue用了计算的，与我们无关-->
        <school v-for="item,index in schoolList" :key="'abc'+index" :index='index' :school-name="item"></school>
    </ul>
</div>
```

```js
<script type="text/javascript">
	//产品组件
	Vue.component("school",{
		props:['schoolName','index'],
		template:`<li>
					<h3>{{index}}-学校名称：{{schoolName}}</h3>				
				</li>`	//1、把父组件传来的变量放到props，2、props再传到模板这，3、最后放到父组件视图中的子组件标签中当属性，给子组件标签使用
	})
		
	//根组件
	let app = new Vue({
		el:"#app",
		data:{
			schoolList:['sxt','czbk','xmg']//父组件数据
		}
	})	
</script>
```

## 子父传值

将子组件的值 传给 父组件：通过**自定义触发事件`$emit`**、监听函数@、进行数据的修改

```html
<div id="app">
    <ul>
        <!-- 循环传值组件 -->
        <school v-for="item,index in schoolList" @cschool='changeEvent' :key="'abc'+index" :index='index' :school-name="item"></school>
    </ul>
    <h2>选中的学校是：{{chooseSchool}}<h2>
</div>
```

```js
<script type="text/javascript">
	//产品组件
	Vue.component("school",{
		props:['schoolName','index'],
		template:`<li>
					<h3>{{index}}-学校名称：{{schoolName}}</h3>				
					<button @click="chooseEvent">选择学校</button>
				</li>`	//将子组件中点击按钮选择的学校 传给 父组件：子传父
    	methods:{
    		chooseEvent:function(schoolName){ //子组件先拿到数据
    			this.$emit('cschool',schoolName)//给触发事件自定义名。事件可以定义数据、传值数据，现在就把值传进来
			}
		}
	})
		
	//根组件
	let app = new Vue({
		el:"#app",
		data:{
			schoolList:['清华','北大','浙大','中大']//父组件数据
            chooseSchool:""
		},
        methods:{
            changeEvent:function(data){	//监听触发。事件传值完，这里肯定就能拿到数据了！
                this.chooseSchool = data //父组件拿到数据了，那此时就可以修改数据了。
            }
        }
	})	
</script>
```

### 技巧

除了props以外的方法不大建议，组件之间尽量低耦合，不要交互在一起。否则一有改动，可能有些问题不好发现

1、将父元素方法 传给 子元素

不触发事件，改为子组件标签里传父组件的方法：`:action='方法名'`、再把这个方法传到子组件中`this.action(schoolName)`

```html
<div id="app">
    <ul>
        <!-- 循环传值组件 -->
        <!-- 因为父元素的方法可以直接修改父元素的数据
			 所以将父元素的方法传递给子元素，
			 然后由子元素进行调用，从而修改父元素的数据
		-->
        <school v-for="item,index in schoolList" :action='changeEvent' :key="'abc'+index" :index='index' :school-name="item"></school>	<!--绑定方法：2、子组件通过这个方法来修改父组件的数据-->
    </ul>
    <h2>选中的学校是：{{chooseSchool}}<h2>
</div>
```

```js
<script type="text/javascript">
	//产品组件
	Vue.component("school",{
		props:['schoolName','index','action'],//方法传进来
		template:`<li>
					<h3>{{index}}-学校名称：{{schoolName}}</h3>				
					<button @click="chooseEvent">选择学校</button>
				</li>`	
    	methods:{
    		chooseEvent:function(schoolName){ 
    			this.action(schoolName) 
			}
		}
	})
		
	//根组件
	let app = new Vue({
		el:"#app",
		data:{
			schoolList:['清华','北大','浙大','中大']
            chooseSchool:""
		},
        methods:{
            changeEvent:function(data){	//1、把这里父元素的方法传给子组件
                this.chooseSchool = data //3、修改父组件的数据
            }
        }
	})	
</script>
```

2、不传值了。子元素通过**调用$parent属性的方法**找到父元素的vue对象

去掉绑定方法`:action="事件名"`，把子组件里的`this.action(schoolName)`改为

```
this.$parent.changeEvent(schoolName)
```

3、直接在子组件的点击事件上写方法（在子元素视图直接**调用父元素方法**）

去掉子元素的methods，在template里改

```
<button @click="$parent.changeEvent(schoolName)">选择学校</button>
```

4、通过**父元素数据**直接修改(要执行的内容少才能用，“”里不能加分号)

直接

```
<button @click="$parent.chooseSchool = schoolName">选择学校</button>
```

5、$root	最外层的app根组件

```
<button @click="$root.changeEvent(schoolName)">选择学校</button>
```

6、父组件的$children，使用方式类似（通过mouted()可打印查看）

## 在组件上使用v-model

```html
<div id="app">
    <input-com :username='username' @input='username=$event'></input-com>
    <input-com v-model="username"></input-com>		<!--2、再使用v-model-->
    <h3>{{username}}</h3>
</div>
<script type="text/javascript">
    Vue.component('input-com',{
        props:['username'],
        template:`<input type="text" @input="$emit('input',$event.target.value)" :value="username" />`,		//	//1、先写这儿

    })

    let app = new Vue({
        el:"#app",
        data:{
            username:""
        },
        methods:{
            changeEvent:function(data){
                this.username = data
            }
        }
    })
</script>
```

## 插槽

> 当网页结构不变时，想插入不同的数据，就可以使用组件的插槽了
>
> 怎么让组件标签中的文本有效果，就要用到插槽
>
> 按上一节的传值方式也可以，但不够灵活

1、slot

```html
<div id="app">

    <alert-com :html='content'></alert-com>
    <!-- slot里面的内容变量只跟父元素有关 -->
    <alert-com1>
        <p>小心陈老师,{{content}}</p>
    </alert-com1>

</div>
<script type="text/javascript">
    Vue.component('alert-com',{
        props:['html'],
        template:`
<div class="alert">
<h1>温馨提示</h1>
<div class="content">
{{html}}
    </div>
    </div>
`
    })
    Vue.component('alert-com1',{
        template:`
<div class="alert">
<h1>温馨提示</h1>
<div class="content">
<slot></slot>
    </div>
    </div>
`,
        data:function(){

            return {
                abc:"abc123"
            }
        }
    })

    let app = new Vue({
        el:"#app",
        data:{
            content:"小心熊出没"
        }
    })
</script>
```

2、动态组件`:is`	切换不同的组件（但在js里写太麻烦，所以vue出了单文件组件——正常开发，用脚手架vue-cli）

```html
<div id="app">

    <div id="content">
        <component :is="com"></component>
    </div>

    <button @click="chooseContent(1)">首页</button>
    <button @click="chooseContent(2)">列表</button>
    <button @click="chooseContent(3)">新闻</button>
    <button @click="chooseContent(4)">个人</button>
</div>
<script type="text/x-template" id="laochen">
			<div>
				<h1>首页内容</h1>
				<p>Hello hello hello vue</p>
    </div>

</script>
<script type="text/javascript">
    let com1 = Vue.component("index-com",{
        name:'index',
        template:'#laochen'
    })
    let com2 =Vue.component("list-com",{
        template:'<div><h1>列表内容</h1><p></p></div>'
    })
    let com3 =Vue.component("news-com",{
        template:'<h1>新闻内容</h1>'
    })
    let com4 =Vue.component("me-com",{
        template:'<h1>个人中心内容</h1>'
    })

    let app = new Vue({
        el:"#app",
        data:{
            com:com1
        },
        methods:{
            chooseContent:function(id){
                console.log(id)
                console.log(this)
                //通过获取id,选择注册好的组件
                this.com = this.$options.components['com'+id]
            }
        },
        components:{
            com1,com2,com3,com4
        }
    })
</script>
```

# 面试题

- 虚拟DOM
- v-if和v-show区别
  - v-if：不显示时，第一次就直接不渲染；若将显示内容改为不显示，将内容直接从DOM去除。建议**只是渲染一次**，用v-if。
  - v-show：不显示时，就会改成display:none,会渲染在DOM上。建议**反复需要切换**的内容，使用v-show。

