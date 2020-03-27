# 一、简介

官方中文网：http://www.bootcss.com/

## 什么是 Bootstrap？

一个包含css库、js库的响应式框架。（它自带了Normalize.css）

## 可以干什么？

可以做响应式网站

## 获取

下载：http://v3.bootcss.com/getting-started/#download

解压完后文件夹：

css：放css样式。只要bootstrap.min.js

js：放jq插件。必须依赖jQuery。（没用到，可不放）

fonts：放字体图标。（没用到，可不放）

## 使用

引用css、js、jQuery（压缩版）；

引入官网中全局CSS样式里的移动设备优先里的代码：可缩放选1，不可缩放选2；

在html中引入bootstrap的类。

> **照着对应版本手册**知道它提供了哪些预置的样式，每个样式对应着什么效果。要用它，把它的手册过一遍。（看不懂没关系，**看效果、对应代码、Bootstrap.css提供的特殊类名**）
>
> 浏览性的一致性：Normailze.css；

# 二、内容

只讲了常用的，要记！其他内容可以去官网文档看，复制粘贴

若嫌样式不好看自己弄个css文件去替换它：在网页中检查复制对应class来修改样式。不要去修改bootstrap.css

## 布局容器

.container：居中、占用80%宽度

.container-fluid：全宽

注意：不能互相嵌套

## 排版

### 1.标题

​	.h1、.h2、.h3 ...	用处不多

### 2.页面主体

```
//被bootstrap设置为
body{
	font-size: 14px;
	line-height: 1.428;
}
p{
	margin: 0 0 10px;
}
```

### 3.对齐

​	text-left（默认）

​	text-right

​	text-center

## 代码

### 代码块

​	<pre>	放置代码的h5标签

网站常写为：

```
<pre>
	//要将尖括号转义处理：&lt; &gt;，否则无法显示代码
	&lt;p&gt;
    	let str='你好';
    &lt;/p&gt;
</pre>
```

## 表格

.table	使表格有基本样式

.table-striped 	条纹状表格

.table-bordered	边框表格

.table-hover	鼠标悬停

.table-condensed	紧凑表格

响应式表格.table-responsive：

```
<div class="table-responsive">
  <table class="table">
    ...
  </table>
</div>
```

状态类	可以为行或单元格设置颜色：

| `.active`  | 鼠标悬停在行或单元格上时所设置的颜色 |
| :--------- | ------------------------------------ |
| `.success` | 标识成功或积极的动作                 |
| `.info`    | 标识普通的提示信息或动作             |
| `.warning` | 标识警告或需要用户注意               |
| `.danger`  | 标识危险或潜在的带来负面影响的动作   |

## 表单

> 用表单组来将同组的内容包裹。
> 要把输入框都放到表单组中。

竖向表单：添加表单组.form-group的div即可

横向表单: .form-inline。

水平表单: .form-horizontal

input美化：.form-control。也可美化下拉列表

把文本隐藏(seo优化)：.sr-only

给输入框加上$、.00等符号：.input-group-addon的div，并在外面套个.input-group的div连接

```
//连接:
<div class='input-group'>
	<div></div>
	<input type="text">
	<div></div>//可省
</div>
```

多选框和单选框

.disabled	阻止点击 。也可给text禁止修改

给label添加.checkbox-inline` 或 `.radio-inline	横向

控件尺寸

.input-lg	设置最大高度

.input-sm	设置最小高度

## 按钮

为 <a>、<button> 或 <input> 元素添加按钮类

 1.预定义样式：

```html
btn btn-default 默认样式
btn btn-primary 首选项
btn btn-success 成功
btn btn-info	一般信息
btn btn-warning	警告
btn btn-danger	危险
btn btn-link	链接
```

2.尺寸

使用 `.btn-lg`、`.btn-sm` 或 `.btn-xs` 就可以获得不同尺寸的按钮。

3.其他

btn-block	块级元素

active	激活状态

disabled	禁用

## 图片

在官网可以看到

1、响应式图片。可以设置居中。

- 响应式图片：img-responsive
- **图片居中：center-block**（常用）

2、图片形状

- img-rounded   圆角
- img-circle  圆
- img-thumbnail  有边框 

## 辅助类

针对文本内容

- **快速浮动**（重点）
  - pull-left	左浮  pull-right   右浮
- **清除浮动**
  - clearfix   
- **让内容块居中**
  - center-block

- **隐藏、显示内容**
  - hidden
  - show
- **图片替换里面的描述文字innerText**（SEO优化）
  - text-hide

- 情景文本颜色、背景色
- 关闭按钮（可自己写）
  - 记住class=“close”表示关闭
  - aria-hidden盲人阅读器，删掉
  - innerText里控制显示文本
- 三角符号（建议自己写）

## 🔺响应式工具

- visible	可见（显示）
  - xs	小于768px
  - sm   大于等于768px
  - md   大于等于992px
  - lg  大于等于1200px
- hidden  不可见（隐藏）
  - xs	小于768px
  - sm   大于等于768px
  - md   大于等于992px
  - lg  大于等于1200px
- 还可以转换
  - 如xs-block、xs-inline-block

# 三、栅格系统(响应式)

## 排版

### 基本使用(布局)

Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，**随着屏幕或视口（viewport）尺寸的增加，系统会自动分为    最多12列**。

简介：

栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，你的内容就可以放入这些创建好的布局中。

使用：
1》“行（row）”**必须包含在 .container （固定宽度）或 .container-fluid （100% 宽度）中**，以便为其赋予合适的排列（aligment）和内补（padding）。

2》**类似 .row （行）和 .col-xs-4 （列）这种预定义的类，可以用来快速创建栅格布局**。Bootstrap 源码中定义的 mixin 也可以用来创建语义化的布局。

3》col-lg-6

	col==>列
	lg==》尺寸
	6=＝》占用空间的6份

4》尺寸

	lg  ：大于等于1200px  ==》大桌面显示器
	md  : 大于等于992px   ==》桌面显示器 
	sm  : 大于等于768px   ==》平板
	xs  : 小于768px      ==》手机
具体使用：lg时一行显示4个，sm时一行显示2个，xs时一行显示一个

```html
<div class='container'>
	
	<div class='row dv1 text-center'> <!--行-->
		
		<div class='col-lg-3 col-sm-6 col-xs-12'>A</div>
		<div class='col-lg-3 col-sm-6 col-xs-12'>B</div>
		<div class='col-lg-3 col-sm-6 col-xs-12'>C</div>
		<div class='col-lg-3 col-sm-6 col-xs-12'>D</div>

	</div>

</div>
```

### 列偏移

位置上的变化，可以用浮动，也可用列偏移

	offset
	
	col-xx-offset-xx
具体使用：偏移4份

```html
<div class='container-fluid'>
	
	<div class='row fz'> <!--行-->
		
		<div class='col-lg-4'>
			1
		</div>

		<div class='col-lg-4 col-lg-offset-4'>
			2
		</div>

	</div>

</div>
```

### 嵌套列

每个列可以走个嵌套的关系

例子：占9份的列里再来一行，行内分成12份，被占了3份、占了9份

	<div class='row'>
		<div class='col-md-9'>
			<div class='row'>
				<div class='col-md-3'></div>
				<div class='col-md-9'></div>
			</div>
		</div>
	</div>

### 列排序

常用于双飞翼（把主要内容提前加载）

改变列的顺序

```html
<div class='container-fluid'>

	<div class="row fz">
		
	  <div class="col-md-9 col-md-push-3">占有9份</div>
	  
	  <div class="col-md-3 col-md-pull-9">占有3份</div>
	</div>

</div>
```

## 响应式图片

具体例子：

1、md时一行排4个响应式图片，sm时排2个，xs时需要排1个（每组就一张图片时）

```html
<div class='container'>
	
	<div class='row bg'>		
		<div class='col-md-3 col-sm-6 col-xs-12'>			
			<img src="img/1.png" alt="" class='img-responsive center-block'>
		</div>

		<div class='col-md-3 col-sm-6 col-xs-12'>			
			<img src="img/2.png" alt="" class='img-responsive center-block'>
		</div>

		<div class='col-md-3 col-sm-6 col-xs-12'>			
			<img src="img/3.png" alt="" class='img-responsive center-block'>
		</div>

		<div class='col-md-3 col-sm-6 col-xs-12'>			
			<img src="img/4.png" alt="" class='img-responsive center-block'>
		</div>
	</div>
</div>	
```

2、每组几张图片就要用到visible、hidden

```html
<div class='container'>		
	<img src="img/1.jpeg" alt="" class='hidden-xs img-responsive'><!--大于768隐藏-->
	<img src="img/2.jpeg" alt="" class='visible-xs img-responsive'><!--小于768显示-->
</div>
```

## 实战

细节：

- 小横线处理：给个span，样式给

  ```
  width: 70px;
  height: 1px
  border-top: 1px solid #fff;
  display: inline-block
  ```

- 在一起的普通文字可以用`<br/>`来换行，没必要搞2个元素

- 只写这个初始化样式即可

  ```
  *{margin:0;padding:0;}
  ```

- 一般不给盒子宽高，用padding撑起来

- 检查时若响应式仍有不对，可以用媒体查询

- 常用的bootstrap样式类：

  按钮`btn btn-default`、响应式图片`img-responsive`、文字居中对齐`text-center`、栅格布局`col-md-x`（外面要套`container`）、让图片或内容块居中`center-block`

# 四、组件(必须引入JS、jQ)

必须引入jQuery.js、bootstrap.**js** ===》里面写的就是jquery的插件。jQ推荐使用1.10.x，1.11.x，否则会有用不了、兼容问题。

后期忘记了，可以复制粘贴

## 字体图标（重要）

到bootstrap的[官网](https://v3.bootcss.com/components/)挑选，复制类名添加即可。

注意：

- 必须引入**fonts目录**
- 不要和其他组件混合使用，应用`<span>`包裹起来。否则不对齐
- 只对内容为空的元素起作用，即`span`里不要写内容。否则不对齐
- 若有文字，文字前要加个空格，否则不好看

例子：

定位

```html
<button class='btn btn-lg'>
	<i class='glyphicon glyphicon-map-marker'></i> 定位
</button>
```

表单

```html
<form action="">
	
<div class="form-group has-success has-feedback">

  <div class="input-group"> <!--一组-->
    <span class="input-group-addon">@</span>	<!--字体图标-->
    <input type="text" class="form-control" id="inputGroupSuccess1" aria-describedby="inputGroupSuccess1Status">
  </div>

  <span class="glyphicon glyphicon-ok form-control-feedback"></span> <!--最后类：鼠标放上去显示-->
</div>
</form>
```

## 下拉菜单

使用：

1》将下拉菜单触发器和下拉菜单**都包裹在 .dropdown 里**，或者另一个声明了 position: relative; 的元素。然后加入组成菜单的 HTML 代码。否则下拉无效。（改成.dropup，就可以变成上拉菜单）

2》点击谁：需要给元素加入自定义属性

	data-toggle="属性名称"

可以给该元素里加个小三角`<span class='caret'></span>`

3》显示谁：加入类（class）

	class='dropdown-menu'

比如加在ul上。可以给里面加个小横线，如`<li class='divider'></li>`

禁用   类disabled

## 按钮 组（重要）

**1、弄成一个组**

在要组合起来的按钮外 加个类**btn-group**的元素即可

2、尺寸：-lg、-md、-sm、-xs

3、嵌套：如把下拉菜单也组合进来，在下拉菜单外再加个**btn-group**的元素

ps: dropdown-toggle可以把下拉菜单变圆角

4、垂直排列：btn-group-vertical

5、两端对齐的：btn-group-justified和a链接。若用button，则每个button外都要套btn-group

6、分裂式按钮：就不说了看官网

## 输入框组

` .input-group`	组合

注意：

1》在文本输入框 `<input> `前、后、两边加上文字元素或按钮，可实现对表单控件的扩展。

怎么使用？为` .input-group` 赋予 `.input-group-addon` 或 `.input-group-btn` 类。

-  `.input-group-addon`可以直接给文字元素加，而给单选、多选框等要套在外面才行。除了按钮
- `.input-group-btn`：是要在按钮外面套个加了`.input-group-btn`的div。（原因：由于不同浏览器的默认样式无法被统一的重新赋值）	

2》不要将表单组、栅格列（column）类直接和输入框组混合使用。而是**将输入框组嵌套到**表单组或栅格相关元素的内部。

## 导航

**都依赖.nav基类**，**.nav一定要加** 

标签类导航：.nav-tabs，选择状态 .active

胶囊类导航：.nav-pills，选择状态 .active

## 导航条（重要）

复制粘贴只要会改就可以了

```html
<nav class="navbar navbar-default">

  <div class="container-fluid">

    <div class="navbar-header">

      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-btn">
       
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>

      </button>

      <a class="navbar-brand" href="#">Brand</a>

    </div>

    <div class="collapse navbar-collapse" id="bs-btn">

      <ul class="nav navbar-nav">

        <li class="active">
          <a href="">11111</a>
        </li>

        <li>
          <a href="#">2222</a>
        </li>
      </ul>

      <form class="navbar-form navbar-left">
        <div class="form-group">
          <input type="text" class="form-control" placeholder="Search">
        </div>
        <button type="submit" class="btn btn-default">Submit</button>
      </form>

      <ul class="nav navbar-nav navbar-right">
        <li><a href="#">AAAAA</a></li>
        <li><a href="#">BBBBB</a></li> 
      </ul>

    </div>
  </div>
</nav>
```

基类：`.navbar`

不隐藏区域：`.navbar-header`

- 默认样式导航条	 `.navbar-default`	
- 反色的导航条        `.navbar-inverse`
- 组件的左右排列    如 `.navbar-left`	   
- 可以固定在顶部       `navbar-fixed-top ` ,但会有50px高度，所以要给`body`加上`paading-top：50px;`
- 品牌图标导航条	 `.navbar-brand`   它已经**被设置了内补（padding）和高度（height）**，你需要根据自己的情况添加一些 CSS 代码从而覆盖默认设置。
- 将表单加入到导航条	将表单放置于 `.navbar-form` 之内可以呈现很好的垂直对齐，并在较窄的视口（viewport）中呈现折叠状态。 若加到图标导航栏中，可调CSS来调整
- 将按钮加入到导航条   `.navbar-btn` ，让垂直对齐
- 将文本加入到导航条   `.navbar-rext` ，让垂直对齐
- 将文本加入到导航条   `.navbar-link` ，让垂直对齐

## 路径导航、分页

路径导航：

```
<ol class="breadcrumb">
  <li><a href="#">首页</a></li>
  <li><a href="#">新闻</a></li>
  <li class="active">娱乐新闻</li>
</ol>
```

分页：`.pagination`

`.disabled`	不可点

```html
<ul class="pagination">
  <li>
    <a href="#">
      <span>&laquo;</span>
    </a>
  </li>
  <li><a href="#">1</a></li>
  <li class='disabled'><a href="#">2</a></li>
  <li><a href="#">3</a></li>
  <li><a href="#">4</a></li>
  <li><a href="#">5</a></li>
  <li>
    <a href="#">
      <span>&raquo;</span>
    </a>
  </li>
</ul>

<ul class="pager"> <!--翻页-->
  <li><a href="#">上一页</a></li>
  <li><a href="#">下一页</a></li>
</ul>

<ul class="pager"><!--对齐的翻页-->
  <li class="previous">
    <a href="#">
      上一页
    </a></li>

  <li class="next">
    <a href="#">
      下一页 
    </a>
  </li>
</ul>
```

## 标签、徽章

标签label

要用时就复制拿过来即可、也可以自己写

```html
<span class="label label-default">New</span>
<span class='label label-success'>success</span>
<span class='label label-info'>info</span>
```

徽章badge

想调css，CSS覆盖即可

```html
<button class='btn btn-info'>    
    未读消息
    <i class='badge'>1</i>
</button>
```

## 巨幕(可以用)、页头

巨幕：(jumbotron)

这是一个轻量、灵活的组件，它能**延伸至整个浏览器视口**来展示网站上的关键内容。

```
<div class="jumbotron text-center">
  <h1>Hello, world!</h1>
  <p>我是p标记</p>
  <p>
    <a class="btn btn-primary btn-lg" href="#" role="button">a按钮</a>
  </p>
</div>
```


页头：(page-header)

场景： 文章｜列表

```
<div class="page-header">
  <h1>
    公告：
    <small>今天学习了bootstrap</small>
  </h1>
</div>
```

## 缩略图thumbnail

它不是响应式图片！就是图片加边框、加描述，起展示用

要配合栅格系统来使用，来让它响应式

```html
<div class='container-fluid'> 
 <div class="row">
    
      <div class="col-sm-6 col-md-4">	<!--这儿只写了一组-->
        <div class="thumbnail">
            <img src="img/1.png" alt="...">
            <div class='text-center'>
                <h3>学习</h3>
                <p>Bootstrap课程</p>
                <p>
                    <a href="#" class="btn btn-primary">点击学习</a>
                </p>
            </div>
        </div>
    </div>
  
 </div>
</div>      
```

## 警告框

.alert

可关闭的警告框：

	需要加入：alert-dismissible
	内容部分：
	1、右侧的关闭按钮或者字体图标。。需要加入：colse
	2、需要关闭功能加入自定义属性：data-dismiss="alert"
具体应用：

```html
  <style>
  .alert-log{
    display: none;
  }
  </style>
</head>
<body>
<button class='btn btn-info btn-log'>登陆</button>

<h1 class='alert alert-success alert-log alert-dismissible'>
  <button class='close' data-dismiss="alert">    
    <span>&times;</span>
  </button>
  恭喜您！登陆成功！
</h1>
<script>
  $(function(){
    $(".btn-log").click(function(){
        $(".alert-log").show(2000);
    })
  })
</script>  
```

## 进度条

.progress

```html
<div class='container'> 
带有提示标签的进度条    
  <div class="progress">
    <div class="progress-bar" style="width: 90%;">
      <span>60% Complete</span>
    </div>
  </div>
根据情境变化效果
  <div class="progress">
    <div class="progress-bar progress-bar-success" style="min-width: 20em;">
      0%
    </div>
  </div>
有条纹progress-bar-striped动画效果active
  <div class='progress'>
    <div class='progress-bar progress-bar-striped active' style='width:50%'>
      50%
    </div>
  </div>
</div>
点它时触发的模拟
<div class='container'>   
  <div class='progress'>
    <div class='progress-bar progress-bar-striped pro' style='width:50%'>
      50%
    </div>
  </div>
</div>

<button class='btn btn-info'>上传</button>
<script>  
  var num = 50;

  $(".btn").click(function(){
    fn();
    $('.pro').addClass("active");
  })

  function fn(){
    setInterval(function(){
        num++;
        if(num>100)num=100;
        $(".pro").text(num+"%");//加百分数
        $(".pro").css("width",num+"%");//加宽度
    },50)
  }
</script>
```

## 媒介对象

使用在文章、博客评论上
`.media`	

- media-left
- media-body
- media-right

其它：media-heading标题、media-left对齐、media-object评论人（套ul、li来嵌套）

## 列表组

ul、li也可换成div、a

列表组可加徽章、可默认选择active、可往里加标题

```html
<ul class="list-group">
  <li class="list-group-item">Cras justo odio</li>
  <li class="list-group-item">Dapibus ac facilisis in
    <span class="badge">14</span>
    </li>
  <li class="list-group-item">Morbi leo risus</li>
  <li class="list-group-item">Porta ac consectetur ac</li>
  <li class="list-group-item">Vestibulum at eros</li>
</ul>
```

## 面板

在列表、文章页的侧边会用到。

最常用的：是带表格的面板

```html
<div class='container' style='width:30%'>
    
    <div class="panel panel-default">
          
        <div class='panel-heading'>头部</div>
        <div class='panel-body'>
          内容区域
        </div>
        <ul class='list-group'>
          <li class='list-group-item'>1</li>
          <li class='list-group-item'>2</li>
          <li class='list-group-item'>3</li>
        </ul>

    </div>  
  
</div>
```

## 响应式嵌入内容

```
可以嵌入<iframe>、<embed>、<video> 和 <object>。不需要为 <iframe> 元素设置 frameborder="0" 属性
```

```html
<div class="embed-responsive embed-responsive-16by9">
  <iframe class="embed-responsive-item" src="https://v.qq.com/iframe/player.html?vid=o0540dckmvw&tiny=0&auto=0" width="640" height="498"></iframe>
</div>
```

# 五、JS插件(必须引入JS、jQ)

若对效果要求高，不建议用bootstrap里的js插件（而用其他的 或自己写），因为它其中很多功能存在问题，并不满足网站需求。

具体是：将data-*自定义属性去掉，换成JS去操作，每个都有些调用方法可以去官网看

## 模态框

会做成输入内容、发生ajax请求的弹出框

```html
<button type="button" class="btn btn-primary btn-lg" data-target="#myModal" id='modal'>
  按钮
</button>

<div class="modal fade" id='myModal'> <!--这里把data-toggle="modal"换成JS通过id来控制-->
  <div class="modal-dialog modal-md">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal"><span>&times;</span></button>
        <h4 class="modal-title">Modal title</h4>
      </div>
      <div class="modal-body">
        <p>One fine body&hellip;</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>

<script>

/*
$("#modal").click(function(){

    $("#myModal").modal('show');

})
*/
$("#modal").click(function(){

    $("#myModal").modal({
      show:true,
      keyboard: false
    });

})
/*
$('#myModal').on('hidden.bs.modal', function (e) {//关闭弹出1。在这儿可以进行ajax请求数据
      alert(1); 
})
*/
$('#myModal').on('show.bs.modal', function (e) {//点击弹出2

      alert('22222'); 

})
</script>
```

## 下拉菜单

也是（把data-toggle换成JS）通过id来控制

```html
<div class='dropdown' id='toggle_drop'>
	
	<button class='btn btn-info' id='dropdown' data-toggle='dropdown'>按钮</button>

	<ul class='dropdown-menu'>
		<li>1</li>
		<li>2</li>
		<li>3</li>
	</ul>

</div>

<script>
//$("#dropdown").dropdown();//显示下拉

$("#toggle_drop").on('show.bs.dropdown',function(){
	alert(1);
})
$("#toggle_drop").on('hide.bs.dropdown',function(){
	alert(2);
})
</script>
```

## 滚动监听（常用）

一般的锚点切换推荐，但若要用缓慢的自定义动画不推荐用。

滚动时可以知道到底滚动到哪一块

```html
	<style>
	.main{
		width:500px;
		height: 300px;
		border:1px solid #ccc;
		overflow: scroll;
	}
	</style>
</head>
<body>


<nav class="navbar navbar-default">
  <div class="container-fluid">
    
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">Brand</a>
    </div>

    
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav">

        <li class="active">
        	<a href="#home">首页 
        		<span class="sr-only">(current)</span>
        	</a>
        </li>
        <li>
        	<a href="#list">列表</a>
        </li>

        <li>
          <a href="#news">
          	新闻 
          	<span class="caret"></span>
          </a>
        </li>
      </ul>
    </div>
  </div>
</nav>

<div class='main' data-spy="scroll">
	
	<div id='home'>
		<h1>首页</h1>
		Ad leggings keytar, brunch id art party dolor labore. Pitchfork yr enim lo-fi before they sold out qui. Tumblr farm-to-table bicycle rights whatever. Anim keffiyeh carles cardigan. Velit seitan mcsweeney's photo booth 3 wolf moon irure. Cosby sweater lomo jean shorts, williamsburg hoodie minim qui you probably haven't heard of them et cardigan trust fund culpa biodiesel wes anderson aesthetic. Nihil tattooed accusamus, cred irony biodiesel keffiyeh artisan ullamco consequat.
		Ad leggings keytar, brunch id art party dolor labore. Pitchfork yr enim lo-fi before they sold out qui. Tumblr farm-to-table bicycle rights whatever. Anim keffiyeh carles cardigan. Velit seitan mcsweeney's photo booth 3 wolf moon irure. Cosby sweater lomo jean shorts, williamsburg hoodie minim qui you probably haven't heard of them et cardigan trust fund culpa biodiesel wes anderson aesthetic. Nihil tattooed accusamus, cred irony biodiesel keffiyeh artisan ullamco consequat.
	</div>
	<div id='list'>
		<h1>列表</h1>
		Ad leggings keytar, brunch id art party dolor labore. Pitchfork yr enim lo-fi before they sold out qui. Tumblr farm-to-table bicycle rights whatever. Anim keffiyeh carles cardigan. Velit seitan mcsweeney's photo booth 3 wolf moon irure. Cosby sweater lomo jean shorts, williamsburg hoodie minim qui you probably haven't heard of them et cardigan trust fund culpa biodiesel wes anderson aesthetic. Nihil tattooed accusamus, cred irony biodiesel keffiyeh artisan ullamco consequat.
		Ad leggings keytar, brunch id art party dolor labore. Pitchfork yr enim lo-fi before they sold out qui. Tumblr farm-to-table bicycle rights whatever. Anim keffiyeh carles cardigan. Velit seitan mcsweeney's photo booth 3 wolf moon irure. Cosby sweater lomo jean shorts, williamsburg hoodie minim qui you probably haven't heard of them et cardigan trust fund culpa biodiesel wes anderson aesthetic. Nihil tattooed accusamus, cred irony biodiesel keffiyeh artisan ullamco consequat.
		
	</div>
	<div id='news'>
		<h1>新闻</h1>
		Ad leggings keytar, brunch id art party dolor labore. Pitchfork yr enim lo-fi before they sold out qui. Tumblr farm-to-table bicycle rights whatever. Anim keffiyeh carles cardigan. Velit seitan mcsweeney's photo booth 3 wolf moon irure. Cosby sweater lomo jean shorts, williamsburg hoodie minim qui you probably haven't heard of them et cardigan trust fund culpa biodiesel wes anderson aesthetic. Nihil tattooed accusamus, cred irony biodiesel keffiyeh artisan ullamco consequat.
		Ad leggings keytar, brunch id art party dolor labore. Pitchfork yr enim lo-fi before they sold out qui. Tumblr farm-to-table bicycle rights whatever. Anim keffiyeh carles cardigan. Velit seitan mcsweeney's photo booth 3 wolf moon irure. Cosby sweater lomo jean shorts, williamsburg hoodie minim qui you probably haven't heard of them et cardigan trust fund culpa biodiesel wes anderson aesthetic. Nihil tattooed accusamus, cred irony biodiesel keffiyeh artisan ullamco consequat.
	</div>	

</div>
```

那不要data-spy又该怎么做？

```html
	<style>
	.item{
		width:100%;
		height:1200px;
		border:1px solid #ccc;
		margin-top:100px;
	}
	</style>
</head>
<body>


<nav class="navbar navbar-default navbar-fixed-top" id='nav'>
  <div class="container-fluid">
    
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">Brand</a>
    </div>

    
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav">

        <li class="active">
        	<a href="#home">首页 
        		<span class="sr-only">(current)</span>
        	</a>
        </li>
        <li>
        	<a href="#list">列表</a>
        </li>

        <li>
          <a href="#news">新闻</a>
        </li>

        <li>
        	<a href="#ad">广告</a>
        </li>
      </ul>
    </div>
  </div>
</nav>

<div class='container'>
	
	<div class='item' id='home'>
		<h1>首页</h1>
	</div>
	<div class='item' id='list'>
		<h1>列表</h1>
	</div>
	<div class='item' id='news'>
		<h1>新闻</h1>
	</div>
	<div class='item' id='ad'> 
		<h1>广告</h1>
	</div>

</div>


<script src='js/jquery-1.10.1.min.js'></script>
<script src='js/bootstrap.min.js'></script>
<script>
$(function(){
	$("body").scrollspy({
		target:"#nav",//假如有2个头部，让哪个拥有插件
		offset:100//偏移，快到下个区域时就变
	});

$('#nav').on('activate.bs.scrollspy',function(){

	alert(1);//到每块显示什么内容
  
})


})
</script>
```

## 标签页

原来的,没有锚点，很好。.fade in 淡入淡出

```html
<div class='container'>
		
	<ul class='nav nav-tabs'>
		<li class='active'><a href="#home" data-toggle='tab'>首页</a></li>
		<li><a href="#list" data-toggle='tab'>列表</a></li>
		<li><a href="#news" data-toggle='tab'>新闻</a></li>
	</ul>

	<div class='tab-content'>
		
		<ol class='tab-pane active' id='home'>
			<li>首页</li>
			<li>首页</li>
			<li>首页</li>
		</ol>
	
		<ol class='tab-pane' id='list'>
			<li>列表</li>
			<li>列表</li>
			<li>列表</li>
		</ol>

		<ol class='tab-pane' id='news'>
			<li>新闻</li>
			<li>新闻</li>
			<li>新闻</li>
		</ol>


		
	</div>

</div>
```

1、那去掉data-toggle后，用JS通过id去操作的：给nav加了个id

```js
$(function(){	$("#tabs").on("click","a",function(e){

		e.preventDefault();//取消默认行为，如锚点
		$(this).tab("show");//替代操作
	})
	$("#tabs").on("shown.bs.tab","a",function(){//在这可以ajax进行数据渲染
		alert(1);
	})             
})
```

## 工具提示

html中：通过title可以显示提示信息

jQ可以美化提示信息，bootstrap也是

加上title、`data-toggle="tooltip"`后，还必须加上方法名称`$("#btn").tooltip();`才行。默认朝上显示

```html
<button id='btn' class='btn btn-info' title='<h2>这是一个提示信息</h2>' data-toggle="tooltip">按钮</button>
<script>
$(function(){

	$("#btn").tooltip({
		placement:"auto",//自动显示好的位置
		delay: { "show": 1000, "hide": 2000 },//显示、消失时间
		html:true//会自动编译html标签
	});
	$('#btn').on('show.bs.tooltip', function () {//显示出来后要怎样
	  	alert(1);
	})    
})
</script>
```

## 弹出框、警告框、按钮  (没用）

正常开发不建议用，自己写还更简单

弹出框，跟提示信息很像

```
<button id="btn" type="button" class="btn btn-lg btn-danger" data-toggle="popover" title="标题" data-content="说明内容">点我弹出/隐藏弹出框</button>

$(function(){
	$("#btn").popover({
		placement:"bottom"
	});
})
```

警告框

```
<div id='alert' class="alert alert-warning alert-dismissible">
  <button type="button" class="close">
  		<span id='times'>&times;</span>
  </button>
  <strong>Warning!</strong>
</div>

$(function(){
/*
	$('#alert').on('closed.bs.alert', function () {	 		
	 	$(this).show(500);
	})
*/	
	$("#times").click(function(){
		$("#alert").fadeOut(2000);
	})
})
```

按钮，点后显示加载ing

```html
<button type="button" id="myButton" data-loading-text="Loading..." class="btn btn-primary" autocomplete="off">
  Loading state
</button>

$(function(){
/*
	$('#myButton').on('click', function () {
	    var $btn = $(this).button('loading');//显示文本
	  
	    $btn.button('toggle');//点后显示加载ing
	})
*/
	//下面是用jQ自己写的
	$("#myButton").click(function(){		$(this).attr("disabled","disabled").text("loading...!!!");//禁选、文本显示

	})
})
```

## 折叠

collapse

知道就可以了

1、点击按钮、p让文本隐藏

```html
<a href="#box" class='btn btn-info' data-toggle='collapse'>这是a链接</a>

<p data-target='#box' data-toggle='collapse'>这是p标记</p>

<div id='box' class='collapse'>
	展示出来的内容
</div>
```

2、折叠菜单

第一个显示，第二个隐藏。点击一个，另一个隐藏

```html
<div id='accordion'>

	<div class="panel panel-default">
	    <div class="panel-heading" id="headingOne">
	      <h4 class="panel-title">
	        <a data-toggle="collapse" data-parent="#accordion" href="#collapseOne">
	           点击1111111
	        </a>
	      </h4>
	    </div>
	    <div id="collapseOne" class="panel-collapse collapse in">
	      <div class="panel-body">
	        展示出来的内容111111
	      </div>
	    </div>
	</div>

	<div class="panel panel-default">
	    <div class="panel-heading" id="headingOne">
	      <h4 class="panel-title">
	        <a data-toggle="collapse" data-parent="#accordion" href="#collapseTwo">
	           点击22222
	        </a>
	      </h4>
	    </div>
	    <div id="collapseTwo" class="collapse">
	      <div class="panel-body">
	        展示出来的内容2222222
	      </div>
	    </div>
	</div>

</div>
```

3、通过JS操作的折叠菜单

点按钮展示出来

```html
<div class="panel panel-default">
    <div class="panel-heading" id="headingOne">
        <h4 class="panel-title">
            <a id='oA'>
                点击1111111
            </a>
        </h4>
    </div>
    <div id="one" class="collapse">
        <div class="panel-body">
            展示出来的内容111111
        </div>
    </div>
</div>
<script>
$(function(){
	$("#oA").click(function(){
		$("#one").collapse('show');
	})
})	
</script>
```

## Carousel(轮播器)、Affix（类似滚动监听）

不好用，到移动端就废了，不推荐

Carousel

```html
<!-- 有很多参数，可以直接加在父盒子上来控制-->
<div id="carousel-example-generic" class="carousel slide" data-wrap='false'>

  <ol class="carousel-indicators">
    <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
    <li data-target="#carousel-example-generic" data-slide-to="1"></li>
    <li data-target="#carousel-example-generic" data-slide-to="2"></li>
  </ol>

  
  <div class="carousel-inner" role="listbox">
    <div class="item active">
      <img src="img/banner.gif" alt="...">
      <div class="carousel-caption">
        <h1>这是第一张</h1>
      </div>
    </div>
    <div class="item">
      <img src="img/banner1.jpg" alt="...">
      <div class="carousel-caption">
       	<h1>这是第二张</h1>
      </div>
    </div>
    <div class="item">
      <img src="img/banner2.jpg" alt="...">
    </div>
  </div>
    
  <!-- Controls -->
  <a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
    <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
    <span class="sr-only">Previous</span>
  </a>
  <a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
    <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
    <span class="sr-only">Next</span>
  </a>
</div>
```

Affix  类似于滚动监听

```html
<style>
/* Custom Styles */
    ul.nav-tabs{
        width: 140px;
        margin-top: 20px;
        border-radius: 4px;
        border: 1px solid #ddd;
        box-shadow: 0 1px 4px rgba(0, 0, 0, 0.067);
    }
    ul.nav-tabs li{
        margin: 0;
        border-top: 1px solid #ddd;
    }
    ul.nav-tabs li:first-child{
        border-top: none;
    }
    ul.nav-tabs li a{
        margin: 0;
        padding: 8px 16px;
        border-radius: 0;
    }
    ul.nav-tabs li.active a, ul.nav-tabs li.active a:hover{
        color: #fff;
        background: #0088cc;
        border: 1px solid #0088cc;
    }
    ul.nav-tabs li:first-child a{
        border-radius: 4px 4px 0 0;
    }
    ul.nav-tabs li:last-child a{
        border-radius: 0 0 4px 4px;
    }
    ul.nav-tabs.affix{
        top: 30px; /* Set the top position of pinned element */
    }
</style>
</head>
<body data-spy="scroll" data-target="#myScrollspy">
<div class="container">
   <div class="jumbotron">
        <h1>Bootstrap Affix</h1>
    </div>
    <div class="row">
        <div class="col-xs-3" id="myScrollspy">
            <ul class="nav nav-tabs nav-stacked" data-spy="affix" data-offset-top="125">
                <li class="active"><a href="#section-1">第一部分</a></li>
                <li><a href="#section-2">第二部分</a></li>
                <li><a href="#section-3">第三部分</a></li>
                <li><a href="#section-4">第四部分</a></li>
                <li><a href="#section-5">第五部分</a></li>
            </ul>
        </div>
        <div class="col-xs-9">
            <h2 id="section-1">第一部分</h2>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam eu sem tempor, varius quam at, luctus dui. Mauris magna metus, dapibus nec turpis vel, semper malesuada ante. Vestibulum id metus ac nisl bibendum scelerisque non non purus. Suspendisse varius nibh non aliquet sagittis. In tincidunt orci sit amet elementum vestibulum. Vivamus fermentum in arcu in aliquam. Quisque aliquam porta odio in fringilla. Vivamus nisl leo, blandit at bibendum eu, tristique eget risus. Integer aliquet quam ut elit suscipit, id interdum neque porttitor. Integer faucibus ligula.</p>
            <p>Vestibulum quis quam ut magna consequat faucibus. Pellentesque eget nisi a mi suscipit tincidunt. Ut tempus dictum risus. Pellentesque viverra sagittis quam at mattis. Suspendisse potenti. Aliquam sit amet gravida nibh, facilisis gravida odio. Phasellus auctor velit at lacus blandit, commodo iaculis justo viverra. Etiam vitae est arcu. Mauris vel congue dolor. Aliquam eget mi mi. Fusce quam tortor, commodo ac dui quis, bibendum viverra erat. Maecenas mattis lectus enim, quis tincidunt dui molestie euismod. Curabitur et diam tristique, accumsan nunc eu, hendrerit tellus.</p>
            <hr>
            <h2 id="section-2">第二部分</h2>
            <p>Nullam hendrerit justo non leo aliquet imperdiet. Etiam in sagittis lectus. Suspendisse ultrices placerat accumsan. Mauris quis dapibus orci. In dapibus velit blandit pharetra tincidunt. Quisque non sapien nec lacus condimentum facilisis ut iaculis enim. Sed viverra interdum bibendum. Donec ac sollicitudin dolor. Sed fringilla vitae lacus at rutrum. Phasellus congue vestibulum ligula sed consequat.</p>
            <p>Vestibulum consectetur scelerisque lacus, ac fermentum lorem convallis sed. Nam odio tortor, dictum quis malesuada at, pellentesque vitae orci. Vivamus elementum, felis eu auctor lobortis, diam velit egestas lacus, quis fermentum metus ante quis urna. Sed at facilisis libero. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Vestibulum bibendum blandit dolor. Nunc orci dolor, molestie nec nibh in, hendrerit tincidunt ante. Vivamus sem augue, hendrerit non sapien in, mollis ornare augue.</p>
            <hr>
            <h2 id="section-3">第三部分</h2>
            <p>Integer pulvinar leo id risus pellentesque vestibulum. Sed diam libero, sodales eget sapien vel, porttitor bibendum enim. Donec sed nibh vitae lorem porttitor blandit in nec ante. Pellentesque vitae metus ipsum. Phasellus sed nunc ac sem malesuada condimentum. Etiam in aliquam lectus. Nam vel sapien diam. Donec pharetra id arcu eget blandit. Proin imperdiet mattis augue in porttitor. Quisque tempus enim id lobortis feugiat. Suspendisse tincidunt risus quis dolor fringilla blandit. Ut sed sapien at purus lacinia porttitor. Nullam iaculis, felis a pretium ornare, dolor nisl semper tortor, vel sagittis lacus est consequat eros. Sed id pretium nisl. Curabitur dolor nisl, laoreet vitae aliquam id, tincidunt sit amet mauris.</p>
            <p>Phasellus vitae suscipit justo. Mauris pharetra feugiat ante id lacinia. Etiam faucibus mauris id tempor egestas. Duis luctus turpis at accumsan tincidunt. Phasellus risus risus, volutpat vel tellus ac, tincidunt fringilla massa. Etiam hendrerit dolor eget ante rutrum adipiscing. Cras interdum ipsum mattis, tempus mauris vel, semper ipsum. Duis sed dolor ut enim lobortis pellentesque ultricies ac ligula. Pellentesque convallis elit nisi, id vulputate ipsum ullamcorper ut. Cras ac pulvinar purus, ac viverra est. Suspendisse potenti. Integer pellentesque neque et elementum tempus. Curabitur bibendum in ligula ut rhoncus.</p>
            <p>Quisque pharetra velit id velit iaculis pretium. Nullam a justo sed ligula porta semper eu quis enim. Pellentesque pellentesque, metus at facilisis hendrerit, lectus velit facilisis leo, quis volutpat turpis arcu quis enim. Nulla viverra lorem elementum interdum ultricies. Suspendisse accumsan quam nec ante mollis tempus. Morbi vel accumsan diam, eget convallis tellus. Suspendisse potenti.</p>
            <hr>
            <h2 id="section-4">第四部分</h2>
            <p>Suspendisse a orci facilisis, dignissim tortor vitae, ultrices mi. Vestibulum a iaculis lacus. Phasellus vitae convallis ligula, nec volutpat tellus. Vivamus scelerisque mollis nisl, nec vehicula elit egestas a. Sed luctus metus id mi gravida, faucibus convallis neque pretium. Maecenas quis sapien ut leo fringilla tempor vitae sit amet leo. Donec imperdiet tempus placerat. Pellentesque pulvinar ultrices nunc sed ultrices. Morbi vel mi pretium, fermentum lacus et, viverra tellus. Phasellus sodales libero nec dui convallis, sit amet fermentum sapien auctor. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Sed eu elementum nibh, quis varius libero.</p>
            <p>Vestibulum quis quam ut magna consequat faucibus. Pellentesque eget nisi a mi suscipit tincidunt. Ut tempus dictum risus. Pellentesque viverra sagittis quam at mattis. Suspendisse potenti. Aliquam sit amet gravida nibh, facilisis gravida odio. Phasellus auctor velit at lacus blandit, commodo iaculis justo viverra. Etiam vitae est arcu. Mauris vel congue dolor. Aliquam eget mi mi. Fusce quam tortor, commodo ac dui quis, bibendum viverra erat. Maecenas mattis lectus enim, quis tincidunt dui molestie euismod. Curabitur et diam tristique, accumsan nunc eu, hendrerit tellus.</p>
            <p>Phasellus fermentum, neque sit amet sodales tempor, enim ante interdum eros, eget luctus ipsum eros ut ligula. Nunc ornare erat quis faucibus molestie. Proin malesuada consequat commodo. Mauris iaculis, eros ut dapibus luctus, massa enim elementum purus, sit amet tristique purus purus nec felis. Morbi vestibulum sapien eget porta pulvinar. Nam at quam diam. Proin rhoncus, felis elementum accumsan dictum, felis nisi vestibulum tellus, et ultrices risus felis in orci. Quisque vestibulum sem nisl, vel congue leo dictum nec. Cras eget est at velit sagittis ullamcorper vel et lectus. In hac habitasse platea dictumst. Etiam interdum iaculis velit, vel sollicitudin lorem feugiat sit amet. Etiam luctus, quam sed sodales aliquam, lorem libero hendrerit urna, faucibus rhoncus massa nibh at felis. Curabitur ac tempus nulla, ut semper erat. Vivamus porta ullamcorper sem, ornare egestas mauris facilisis id.</p>
            <p>Ut ut risus nisl. Fusce porttitor eros at magna luctus, non congue nulla eleifend. Aenean porttitor feugiat dolor sit amet facilisis. Pellentesque venenatis magna et risus commodo, a commodo turpis gravida. Nam mollis massa dapibus urna aliquet, quis iaculis elit sodales. Sed eget ornare orci, eu malesuada justo. Nunc lacus augue, dictum quis dui id, lacinia congue quam. Nulla sem sem, aliquam nec dolor ac, tempus convallis nunc. Interdum et malesuada fames ac ante ipsum primis in faucibus. Nulla suscipit convallis iaculis. Quisque eget commodo ligula. Praesent leo dui, facilisis quis eleifend in, aliquet vitae nunc. Suspendisse fermentum odio ac massa ultricies pellentesque. Fusce eu suscipit massa.</p>
            <hr>
            <h2 id="section-5">第五部分</h2>
            <p>Nam eget purus nec est consectetur vehicula. Nullam ultrices nisl risus, in viverra libero egestas sit amet. Etiam porttitor dolor non eros pulvinar malesuada. Vestibulum sit amet est mollis nulla tempus aliquet. Praesent luctus hendrerit arcu non laoreet. Morbi consequat placerat magna, ac ornare odio sagittis sed. Donec vitae ullamcorper purus. Vivamus non metus ac justo porta volutpat.</p>
            <p>Vivamus mattis accumsan erat, vel convallis risus pretium nec. Integer nunc nulla, viverra ut sem non, scelerisque vehicula arcu. Fusce bibendum convallis augue sit amet lobortis. Cras porta urna turpis, sodales lobortis purus adipiscing id. Maecenas ullamcorper, turpis suscipit pellentesque fringilla, massa lacus pulvinar mi, nec dignissim velit arcu eget purus. Nam at dapibus tellus, eget euismod nisl. Ut eget venenatis sapien. Vivamus vulputate varius mauris, vel varius nisl facilisis ac. Nulla aliquet justo a nibh ornare, eu congue neque rutrum.</p>
            <p>Suspendisse a orci facilisis, dignissim tortor vitae, ultrices mi. Vestibulum a iaculis lacus. Phasellus vitae convallis ligula, nec volutpat tellus. Vivamus scelerisque mollis nisl, nec vehicula elit egestas a. Sed luctus metus id mi gravida, faucibus convallis neque pretium. Maecenas quis sapien ut leo fringilla tempor vitae sit amet leo. Donec imperdiet tempus placerat. Pellentesque pulvinar ultrices nunc sed ultrices. Morbi vel mi pretium, fermentum lacus et, viverra tellus. Phasellus sodales libero nec dui convallis, sit amet fermentum sapien auctor. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Sed eu elementum nibh, quis varius libero.</p>
            <p>Morbi sed fermentum ipsum. Morbi a orci vulputate tortor ornare blandit a quis orci. Donec aliquam sodales gravida. In ut ullamcorper nisi, ac pretium velit. Vestibulum vitae lectus volutpat, consequat lorem sit amet, pulvinar tellus. In tincidunt vel leo eget pulvinar. Curabitur a eros non lacus malesuada aliquam. Praesent et tempus odio. Integer a quam nunc. In hac habitasse platea dictumst. Aliquam porta nibh nulla, et mattis turpis placerat eget. Pellentesque dui diam, pellentesque vel gravida id, accumsan eu magna. Sed a semper arcu, ut dignissim leo.</p>
            <p>Sed vitae lobortis diam, id molestie magna. Aliquam consequat ipsum quis est dictum ultrices. Aenean nibh velit, fringilla in diam id, blandit hendrerit lacus. Donec vehicula rutrum tellus eget fermentum. Pellentesque ac erat et arcu ornare tincidunt. Aliquam erat volutpat. Vivamus lobortis urna quis gravida semper. In condimentum, est a faucibus luctus, mi dolor cursus mi, id vehicula arcu risus a nibh. Pellentesque blandit sapien lacus, vel vehicula nunc feugiat sit amet.</p>
        </div>
    </div>
</div>
```

