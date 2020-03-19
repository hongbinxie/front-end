官网http://nodejs.cn/

## Node是什么？

***Node*.*js* 是环境**。一个基于 Chrome V8 引擎的 **JS运行 环境**。

该环境里的JS操作**ECMA**(ECMAscript)。

> 该环境里的js不能操作BOM、DOM。BOM、DOM是浏览器的

## Node的优势

高并发：处理单一服务器时更好

io密集：文件操作、网络操作、数据库更好（指web端方面，不是指服务器端）

## 安装Node(环境搭建)

node就是环境，只安装它就行。

> node会自带npm安装，不用去单独安装npm。(npm是包管理)

1.官网下载好，一路下一步即可。

2.安装测试：node -v和npm -v

3.试用测试：随便写个js，**进入该目录中**用cmd或git bash执行它**node xx.js;**，无误即可。

# 基础

## CommonJS规范(模块化)

> CommonJS最大特点：模块化。

- 每一个文件都是一个模块，都有自己的作用域。(如a.js、b.js都是一个模块)
- 在模块内部，module代表自身。
- **引出：**模块中module.exports提供对外接口。(如b要用a里的变量，a的module.exports提供一个对外接口module.exports.变量。b如何去用接口也是关键)

require语法(引入)

- /代表绝对路径, ./代表相对路径
- 默认后缀: js json node。（即执行时可不写这些后缀，会自动依次去找。若都没有，报错。）
- require('...') ==>会引用node_modules目录里的文件

### 重要操作：模块间的抛出与引入

```
//模块间的引出与引入:b引用a的内容
//a.js
var t1 = 888;
var t2 = 999;
function fn1(){
	console.log("fn1");
}

module.exports.t1 = t1;
module.exports.fn1 = fn1;
//b.js
var mod = require('./a');

console.log(mod.t1);
mod.fn1();
```

## 全局对象global

> 浏览器的全局对象：window

node走ECMAscript语法，它的全局对象是global

```
//模块间的引出与引入:b引用a的内容+全局对象
//a.js
var t1 = 888;
global.t2 = 999;
function fn1(){
	console.log("fn1");
}

module.exports.t1 = t1;
module.exports.fn1 = fn1;
//b.js
var mod = require('./a');

console.log(mod.t1);
console.log(t2);
mod.fn1();
```

## NPM

### npm介绍

包管理器

作用：让js开发者下载别人写的包。也可上传自己写的包。

优势：集中管理包，方便查询下载。（如项目中用到轮播插件swiper，用搜索引擎或进它官网找不难。但项目中要用到秒杀插件、倒计时插件等，搜索引擎难找好的，就可去npm包看下。）

### npm常用命令

npm -v	查看版本

npm init	初始化项目

npm install xxx	下载包

npm list	查看所有包

命令大全https://www.3mooc.com/front/articleinfo/98

### npm下载 包

如npm install xxx下载完包后，项目目录会出现node_modules文件夹，里面除了包的文件夹，其它都是相关依赖。

测试包下载成功：拿文件去引用包输入下面代码，node运行。

```
var express = require('express');
console.log(express);
```

### package.json

> 当npm init初始化后，会在项目目录生成package.json文件。

是npm包信息。

是和node_modules相辅相成的：如github很多项目没有node_modules目录，项目跑不起来——但有package，在项目目录中运行npm install，就会把项目的所有依赖都下载到node_modules里。

信息有：包的名称、版本、依赖等。

### cnmp淘宝镜像

npm国外的，速度慢；

cnpm国内的

安装命令：

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

# 重要操作

## http创建Node服务器

> php要跑起来有apache的支持，而Node就有http的支持
>
> Node中的http模块：是内置的系统模块，无需下载。
>
> http.server是一个基于事件的http服务器，内部c++封装实现，接口JS实现

在项目目录建个server.js，输入

```
const http = require('http');	//引入http模块

const server = http.createServer((req,res)=>{	//创建服务器。参数1：封装了客户端请求，参数2：封装了服务器响应
	res.write("1111");	//响应输出
	res.end();			//响应结束，每次都要写
})						//}).listen(8080);

server.listen(8080);	//监听端口。或在server的）后.调用，来连写
```

注意：会写一个比较大的端口，因为默认80经常会有各种各样的问题

先不运行该文件，进入localhost:8080会报错。再运行即可。

## get请求url数据的操作

> 如果前台发出get请求，那后台如何拿到数据，解析格式呢？
>
> get是路径传值，可通过req.url去拿到

方法1：得到路径req.url 、引入url模块、url.parse(reqUrl,**true**).query拿到query

方法2：不用写true，引入querystring模块、querystring.parse(...)

> 具体看这：
>
> 一、拿到数据：
>
> 先创建前台页面index.html、server.js创建Node服务器
>
> **拿到url数据：req.url**
>
> 进入项目目录，命令行运行server.js启动服务器，再点击链接，命令行里拿到了数据。
>
> 数据是字符串不对，应该拿到json数据对象
>
> 二、拿到正确的数据
>
> 引入url模块。（它实质是个对象）
>
> 引入url模块的方法parse。（方法parse会拿到对象格式，对象中的query值接近正确数据）
>
> 添加第二个参数：true。（就显示了正确的对象数据）
>
> 追加.query.title。（拿到对象的值）

## get请求表单数据的操作

其它操作跟上节一样。这儿注意表单的输入框必须加name属性，否则url上不会添加。

客户端打印要加表头转换编码res.writeHead(200,{"Content-Type":"text/html;charset=utf8"})

> 创建前台
>
> 创建服务器
>
> 通过get请求url数据的操作，拿到了表单数据。
>
> 页面显示数据。res.end("用户名:"+formVal.userName+"----->"+"密码:"+formVal.userPwd);。（有乱码）
>
> 转换。res.writeHead(200,{"Content-Type":"text/html;charset=utf8"})

## post请求表单数据的操作

> 不能操作url请求，因为post数据不会显示在url上。
>
> 操作post：事件接收	2个事件：req.on('data')	每次发送的数据；req.on('end')	数据发送完成

req.on('data',(chunk)=>{})	参数代表每次的数据，去生成个变量去{}做+=即可。这是过程，在这打印没有用。

req.on('data',()=>{})	这是结果，一定是在结果里打出完整用户输入内容。{}里可做操作：打印、响应结束

转换格式：引入模块querystring，通过querystring.parse打印变量。

> 创建前台页面、创建Node服务器

## 通过Node连接mysql、查询内容

> 前提：
>
> 1.下载mysql：https://www.3mooc.com/front/articleinfo/99到官网或百度官网，点击下载社区版的第一个Download按钮
>
> 2.novicat数据库管理工具连接mysql，新建数据库实例：库->表->字段

写代码：

1.在目录中下载mysql包npm install mysql

2.引入mysql模块

3.配置mysql信息（默认端口3306，端口可不写。主机名：novicat连接时的ip：如localhost）

4.连接

5.进行什么查询操作（增删改查）

6.关闭

```
var mysql = require('mysql');
var connection = mysql.createConnection({
  host     : '主机名',
  user     : '用户名',
  password : '密码',
  database : '库名称',
  port     : '端口号'//可不写
});
connection.connect();	//连接
connection.query('select * from 表名称', function (error, results, fields) {//数据库操作函数。查询(增删改查)完后返回的结果：错误信息、结果、字段数据
  if (error) throw error;
  console.log(results)
});
connection.end();	//查询完关闭
```

## 登录

创建前台：登录页面

创建服务器：拿到post表单数据

连接数据库，**条件查询**信息。

```
select * from 表名称：查询所有
select * from 表名称 where userName=? and userPwd=?
```

```
connection.query('select * from 表名称 where userName=? and userPwd=?',[第一个?,第二个?],(err,results,fields)=>{		//3个参数：查询语句、数组、函数
	
})
```

和数据库里的内容对比。查到对应的返回成功，不对应则返回失败

```
if(results.length >0){
	res.writeHead(200,{'Content-Type':"text/html;charset=utf8"})
	res.write('登录成功')
	res.end();
}
```

## 注册

创建前台：注册页面

捋一下逻辑，如何去做内容：

​	1.首先要拿到用户输入的内容：通过http创建服务器、事件操作拿到post数据

​	2.然后放到数据库中：连接数据库、执行增语句、过程中有些问题到写时再看。而不是查删改语句了

要点——

​	1.增语句：insert into 表名称 value (100,123,456)	id、userName、userPwd

​	2.http会把网页图标也拿过来，导致每次拿数据，会多一行：要阻止它拿，如何操作呢？问题在于req.url，打印它查看为/favicon.icon。所以要先进行判定，req.url不为图标时才拿过来

```
if(req.url!='/favicon.icon'){
	......
    connection.query('insert into user value (?,?,?)',[0,userName,userPwd],(err,results,fields)=>{	//因为id是自增长的，所以用0表示默认自增长
                    if(err) throw err;
                    res.write("注册成功！！！");
                    res.end();
    })
    ......
}
```

注意：数据库特性。如数据库内容id为11的数据删了，那下一条它的id则会从12开始。

# express框架

一个基于node.js的web应用开发**框架**。

建议使用webstrom开发工具：操作项目时更方便、更快捷。

## express目录结构

```
bin
		www  ===》启动文件【入口文件】
app.js   ===》全局配置文件
node_modules	===》项目依赖的包文件
routers  ===》路由的配置
views    ===》页面
public   ===》静态资源  【css、img、js】
```

> 1.www中里面有端口号、连接到app.js全局配置文件等。（微信小程序的app.js也是全局配置文件）
>
> 2.关于访问页面：
>
> 过程——www给**端口**、引入app.js=>连接到app.js，引入routes=>routes，引入views，**路由配置**指定页面=>打开视图views里的页面.ejs文件，里面有模板语法。页面中可以放入public里的资源

## 创建express项目

1.webstorm-new-project-选择Node.js EXpress App-选择项目目录-**Template选择EJS模板**-创建(-yes-this windows)-等待安装完毕即可。

2.运行框架：菜单-run-Run bin/www弹出端口号-打开浏览器访问地址-进到express欢迎界面

> 了解
>
> 1.模板引擎：有模板语句
>
> 如php中有模板引擎smarty好用。express里也有模板引擎EJS好用
>
> 2.创建完会生成一个完整的工程目录，当然一些东西需要大家去填。但基本框架给你搭好了
>
> 3.如何知道端口：在项目目录/bin/www，这是启动文件

## express路由操作

1.先到app.js引入路由（require()）、给一级路径分配路由(app.use())

2.再到routes里新建或修改.js配置路由（进行输入res.send或渲染res.render）、用键值定义模板语法中的内容，如(res.render('index'),{tite:'标题',msg:'这是xxx信息'});。

3.再到views里新建或修改.ejs，用模板语法写页面去渲染。

二级路径直接在对应一级路径的.js下配置路由

## 引入静态资源和ejs模板语法

引入静态资源

1.放到对应目录中

2.views里的对应.ejs引入资源。注意路径：**前面加/**，如

```
<img src="/image/1.png" alt="">
```

模板语法：

(1)内容

1.定义内容：到对应.js中输入。如

```
(res.render('index'),{ 
	tite:'标题',
	msg:'这是xxx信息'
});。
```

2.输出内容：到对应.ejs中输出。如<%= title %>，注意：**=代表输出内容，，没有=代表js语句**

(2)JS语句

1.定义内容：如

```
(res.render('index'),{ 
	tite:'标题',
	msg:'这是xxx信息',
	arr:['a','b','c']
});
```

2.输出js语句：<% %>，先把js语句写好再整理模板避免出错。如

```
<ul>
	<% arr.forEach((ietm)=>{ %>
		<li><%= item %></li>
	<% }) %>
</ul>
```

# 实战

## 开发项目的基本流程

> 这是基本流程，实际做时还要根据情况进行梳理。

1.设计数据库

表、结构、字段都要设计得比较完美，添加数据（之后才开始做，后面若需求变或哪儿需要添加字段，到时候再添加）

2.封装连接库、连接数据库

> 可在笔记中ctrl+f搜索封装连接库能找到怎么封装、怎么连接

因为项目中很多地方都需要连接mysql，供后期方便使用：封装后查看哪需要连接数据库，引入封装连接库，就可.query进行数据库操作了。其次才是正常的业务逻辑调整

3.各功能的业务逻辑

> 创建后台的静态页面可以在做功能时写，也可以先写好或找写好的。

## 项目1：express做简单的后台内容管理系统

这儿没做前台，只做了后台。

> 基本流程
>
> 0.设计数据库：因为是教程，所以设计数据库是写到哪一块再创建哪一块，如做到登陆，就创建用户表。
>
> 0.创建后台的静态页面可以在做功能时写，也可以先写好
>
> 1.做登录功能：需要输入用户名、密码登录，才能进入该后台页面
>
> 2..做管理功能：做去增删改查等查询操作

1.创建项目、运行项目测试是否正常

2.引入配置路由文件(.js)：到app.js中require

```
var indexRouter = require('./routes/index');
```

配置该文件的路径：到app.js中app.use。

```
app.use('/admin',indexRouter);
```

> 删除user的require、app.use，没用

4.修改完刷新，测试表单。查看是否配置路由成功。localhost:端口号/admin

5.编写后台页面。编写前先到对应.js文件删除模板定义内容参数，有用时再编写。

以下是各页面的编写。

### 后台的登录页面

要点：路径、登陆

> 登录表单index.ejs

1.写静态

2.写路径：先想下希望跳转的页面

```
localhost:3000/admin	登录表单
localhost:3000/admin/main	希望跳转的页面
```

所以action里写/admin/main。注意前面有/。

写完测试是否跳转。

3.实现登陆功能：输入什么才能登陆

> 创建数据库，创建用户表user，里字段id、userName、userPwd。
>
> 封装连接库：
>
> 1.在项目根目录新建一个js文件sql.js，把数据库配置都放到这，后期直接query就可以了
>
> ```
> var mysql = require('mysql'); //引入mysql模块
> var db =mysql.createConnection({
> 	host:"",
> 	user:"",
> 	password:"",
> 	database:""
> });	//配置相关信息
> 
> db.connect();	//连接数据库
> 
> module.exports = db;	//全局的抛出去,千万别写成局部的module.exports.db = db;
> 
> ```
>
> 2.在项目里下载mysql
>
> 3.封装后去看哪需要连接数据库，去连接
>
> 这儿index.js需要连接，引入封装连接库，然后通过.query即可操作
>
> ```
> var db = require("../sql.js");
> ```

（1）配置post

```
router.post("/main",function(req,res,next){	//post数据要到的地方：/main
	...
});
```

写完代码后，在连接里输入res.end("11");。进入登陆页面随便输入点登录，跳转到main：NotFound，而数据库已添加了11；刷新项目后再第二次登陆，页面显示11，证明配置成功。

（2）拿到用户输入的内容

> 没有express之前，post数据要用事件接受。
>
> 而express中封装了过程：直接用req.body即可。在webstorm里就可看到post数据了。

```
router.post("/main",function(req,res,next){	//post数据对应的地方：/main
	 var val = req.body;
	 var userName = val.userName;
	 var userPwd = val.userPwd;
	 
});
```

（3）作比较：查询数据库内容，把用户内容去作比较

先连接数据库：引入封装连接库文件：var db = require("../sql.js");

直接可以.query进行数据库操作

```
db.query('select * from user where userName=? and userPwd=?',[userName,userPwd],function(err,data){

	if(err){	//先进行判断
		throw err;
	}else if(data.length>0){
		res.end("111");	//登陆成功之后，肯定是跳转一个页面的：通过res.render("");可以渲染.但因为我们要找html模板所以先写到这
	}else{
		res.writeHead(200,{"Content":"text/html;charset=utf8"});
		res.end("登陆失败");
	}
	
})
```

### 后台主页渲染

> 做登录以后的页面的展示
>
> 上一节最后我们是让主页显示111：res.end("111");。应该写res.render(“”);去渲染一个页面。

1.想好渲染哪个静态页面？

这里渲染的主页是一个index.html

到view里新建个main.ejs，把静态页面的代码复制到这。填好了：res.render("main");。

刷新访问，发现有变化即成功。

2.改静态页面：改成路由路径	

> 改了多少页面路径，就要配置多少路由、路径、多少js、多少ejs

查看main.ejs

把页面路径都改好，改成路由形式，不用写后缀：/...	如src=“/top”

3.配置好路由和路径、创建js文件、创建ejs文件

配置路由、指定路径：到app.js中配置,如

```
var topRouter = require('./routes/top');
...
app.use('top',topRouter);
```

创建js文件：在routes里创建，代码跟user.js一样，复制过来。改成res.render("..."); user.js没有用了就把他删掉。

创建ejs文件：在view里创建，把对应页面的静态代码复制过来

4.引入静态资源、改路径（注意前面加/）

### 菜系管理页面渲染

> 其它管理功能类似，这儿就不做了
>
> 把页面调整对了，再到数据库进行增删改查啥的

1.改静态页面：改成路由路径	

2.创建.ejs

3.调整路由

```
var topRouter = require('./routes/top');
...
app.use('top',topRouter);
```

4.创建.js、res.render("");渲染哪个页面

5.引入静态资源

6.点击跳转这些后面改。

### 菜系管理-添加-查询

如点添加——

```
1.改静态页面：改成路由路径
2.调整路由
3.创建ejs
4.创建js、渲染
5.引入静态资源
```

页面调整好后，接下来做往数据库增的操作：

1.找到对应ejs里的表单在哪增：改action，注意前面加/

2.调整路由

3.创建js，注意是post请求方式、res.end("添加中......");

4.往数据库添加什么？需要拿到表单里的name

先测试能不能拿到

```
var val = req.body;
var cuisineName = val.cuisineName;
res.end("cuisineName");
```

接下来用数据库增语句放到数据库中

> 创建表cuisineList，字段id、cuisineName，添加一行数据

```
//1.先连接数据库
var db = require("../sql.js");
//2.到router.post里进行判断
if(cuisineName!=''){
	db.query('insert into cuisineList value (?,?)',[0,cuisineName],function(err,data){
		if(err){
			throw err;
		}else{
			res.end("添加成功");
		}
	})
}else{
	res.end("输入内容不能为空");
}
```

测试：看添加成功或失败的响应，数据库的数据变化。测试成功

到ejs的对应位置删除静态数据，注释一组等会参考，使它变成活的：

1.先测试下有没数据

```
db.query('select * from cuisineList',function(err,data){
		if(err){
			throw err;
		}else{
			console.log(data);		//测试完换回渲染
			//res.render("cuisineList");
		}
})
```

有数据后，需要把数据返回过去：返回到cuisineList.ejs中，让页面能拿到对应数据:

js中

```
res.render("cuisineList",{cuisineList:data});
```

ejs中对应位置，测试能否拿到数据

```
<%= cuisineList %>	
```

拿到后，ejs中改成

```
<% cuisineList.forEach(function(item){ %>	
<tr>
	<td><% item.id %></td>
	<td><% item.cuisineName %></td>
</tr>
<% }) %>
```

测试，成功后再添加条数据测试。