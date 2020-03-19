产生背景：没有对比就没有伤害，如过去的上传/下载/延迟速度。

用谷歌来模拟不同网速下的网站加载速率：

Network->右上的下标Add...->Add custom profile...->文件名、上传/下载/延迟速度->返回点右上下标中的该文件名，可以在该模式测试当前网页加载速度。

## 知识回顾

之前学到的 让浏览器**发出对服务端的请求**，获得服务端的数据的几种方式：

- 地址栏输入地址，回车，刷新 
- 特定元素的 href 或 src 属性 
- 表单提交

但都无法通过、很难通过**代码/编程**来进行对服务端发出请求**并且接受服务端返回的响应**。

过**代码/编程**来进行对服务端发出请求并且接受服务端返回的响应这叫网络编程（发送请求、接收响应）。

编程语言能做的事情取决于API（提供某种特定能力的事物，有输入有输出）。

没学ajax之前不能通过js发请求，必须要将页面刷新一下才能做这操作，所以要学Ajax。

通过Network点XHR可以看到AJAX请求。

XML：最早的服务端返回的响应（数据格式）、描述数据的手段。被json取代了，因为历史原因所以ajax有些内容不改。

学习核心：基本使用、使用封装API、跨域

## AJAX简介

全称：Asynchronous JavaScript and XML。

什么是AJAX：浏览器提供的**一套 API**

作用：可以通过 JavaScript 直接发送请求接收响应，从而**实现网络编程**（发送请求、接收响应）。

为什么要有AJAX：能让js发送请求，解决不刷新时想拿到数据的问题。因为之前没办法及时拿到服务端的数据（因为要刷新），不想刷新又想在表格中呈现数据——那只能把数据写死在js代码中，还不如直接写死在html中但也不方便。

学习重点：不是在于我要发个请求，而在于要如何通过代码来发请求（网络编程）

## AJAX快速上手

**不考虑兼容就4行代码**。不懂就跳过这块代码看下面的发送请求、接收响应。

```js
// 1. 创建一个 XMLHttpRequest 类型的对象 —— 相当于打开了一个浏览器 
var xhr = new XMLHttpRequest() 
// 2. 打开与一个网址之间的连接 —— 相当于在地址栏输入访问地址 
xhr.open('GET', './time.php') 
// 3. 通过连接发送一次请求 —— 相当于回车或者点击访问发送请求 
xhr.send(null) 
// 4. 指定 xhr 状态变化事件处理函数 —— 相当于处理网页呈现后的操作 
//onload是HTML5中提供的XMLHttpRequest2.0定义的，否则用onreadystatechange
xhr.onload = function () {   
	// 通过 xhr 的 readyState 判断此次请求的响应是否接收完成   
  if (this.readyState !== 4) return;     
	// 通过 xhr 的 responseText 获取到响应的响应体   
    //到这ajax操作就结束了。到这里，就是放我们之前所熟悉的代码js。进行发送请求动态获取数据呈现到页面上等
    console.log(this.responseText)  
 }
```

### AJAX发送请求

AJAX提供的核心类型：XMLHttpRequest。作用——模拟平时上网过程：这三行代码就是ajax的核心

```
// 涉及到 AJAX 操作的页面“不能”使用文件协议访问（文件的方式访问，某些情况可以；可以http方式访问）
// 1. 安装浏览器（用户代理）
    //  xhr js用户代理对象，就类似于浏览器的作用（发送请求接收响应）
    var xhr = new XMLHttpRequest()
    // 2. 打开浏览器 输入网址
    //参数：请求方式 网址/相对路径/绝对路径(用/或./表示根目录)
    xhr.open('GET', 'http://day-11.io/time.php')
    // 3. 敲回车键 开始请求
    xhr.send()
    // 4. 等待响应（较复杂，先不写）

    // 5. 看结果
```

> 在js中类型就是构造函数，可以通过new出来。

通过Network的XHR可以看到ajax请求，发送完了之后重点就是：接收响应——如何把服务端响应给我们的数据显示/打印出来（怎样把它从js里面拿到）。

### AJAX接收响应

> 首先注意：不能通过变量去接收xhr.send()，原因：因为响应需要时间，所以无法通过返回值的方式返回响应。
>
> AJAX是通过**onreadystatechange事件**获取响应（再通过xhr.readState获取响应的内容）。在HTML5中可用**onload事件**代替。
>
> 不建议用on的方式注册事件，而是用xhr.addEventListener('事件名', function () {...}) 防止事件注册多次，虽然该事件一般只注册一次但仍建议这样。


```
    //发送响应过程：1.创建浏览器（代理用户）
    var xhr = new XMLHttpRequest()

    // 如果需要补货第一个状态的变化，需要注意代码执行顺序的问题（不要出现来不及的情况）
    // xhr.onreadystatechange = function () {
    //   // 这个事件并不是只在响应时触发，状态改变就触发
    //   // console.log(1)
    //   console.log(this.readyState)
    // }
    
	//2.打开一个地址（以get的方式请求一个地址，请求响应可以用到相对/绝对地址，原因：在同一个网站下面）
    xhr.open('GET', './time.php')
	//3.发送请求
    xhr.send()

	//接收响应过程：4.接收响应
    // 因为客户端永远不知道服务端何时才能返回我们需要的响应，所以 AJAX API 采用事件的机制（通知的感觉）。
    xhr.onreadystatechange = function () {
      // 这个事件并不是只在响应时触发，而是XHR 状态改变就触发。注册事件时间的早晚决定接收的数据，所以如果需要补货第一个状态的变化，需要注意代码执行顺序的问题（不要出现来不及的情况）。
      // console.log(1)确认事件能否执行
 //我们只关心readState=4接收完响应的状态。写出非的形式代码就不会嵌套了
      if (this.readyState !== 4) return
      // 获取响应的内容responseText（即响应体），获取响应头的情况较少
      console.log(this.responseText)
    }
```

#### readState

| readyState | 状态描述         | 说明                                                         |
| ---------- | ---------------- | ------------------------------------------------------------ |
| 0          | UNSENT           | **初始化**：（请求）代理对象                                 |
| 1          | OPENED           | open方法已经调用，**建立**一个与服务端特定端口的**连接**     |
| 2          | HEADERS_RECEIVED | send() 方法已经被调用，且已**接受到**了响应报文的**响应头**，但没拿到响应体（xhr.getAllResponseHeaders(’指定键可省略‘)可拿到，注意是否用到分割） |
| 3          | LOADING          | **响应体下载中**（在这里处理响应体不可靠）                   |
| 4          | DONE             | 响应体**下载完成**，可以直接使用 responseText 。             |

出现阶段：0（代码中写new后）、1（写open后、send后）、（2、3、4）（写接收响应时）

## 如何在ajax设置请求、响应

> 本质上 XMLHttpRequest 就是 JavaScript 在 Web 平台中发送 HTTP 请求的手段，所以我们发送出去的请求仍然是 HTTP 请求，同样符合 HTTP 约定的格式

请求：仍然是HTTP请求

```js
// 设置请求报文的请求行（协议版本是自动设置的）
xhr.open('GET', './time.php') 
// 设置请求头（设置多个请求头：多执行几次即可）
xhr.setRequestHeader('Accept', 'text/plain') 
// 一旦你的请求体是 urlencoded 格式的内容，一定要设置请求头中 Content-Type 'application/x-www-form-urlencoded'。   json的：'application/json'
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
// 设置请求体，不设置就为null或不写参数 xhr.send('请求体') 
xhr.send('key1=value1&key2=value2') // 以 urlencoded 格式设置请求体 '{"foo": "123"}'json格式
xhr.onreadystatechange = function () {   if (this.readyState === 4) {     
	// 获取响应状态码     
	console.log(this.status)    
    // 获取响应状态描述     
    console.log(this.statusText)     
    // 获取响应头信息     
  console.log(this.getResponseHeader('Content‐Type')) // 指定响应头     
  console.log(this.getAllResponseHeader())// 全部响应头     
    // 获取响应体     
   console.log(this.responseText) // 文本形式   
   console.log(this.responseXML) // XML 形式，了解即可不用了   
    } 
}
```

参考链接：
https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest 

https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest

## 具体用法：

### 数据接口的概念

> 接口（API）概念：只要能提供特定能力、有输入有输出都可以叫接口。2种：编程语言的一些函数、web API（**对于返回数据的地址我们称为接口或数据接口**，只不过形式上是Web形式，如api.douban.com/v2/movie/top250,可以给它？后传参数。可以用自己写的，也可以用别人提供的（前提：别人让你用），如github.com/zce/weapp-demo就是用这个豆瓣接口做的app）。
>
> 而ajax操作大部分就是以这种接口的地址作为我们需要去请求的（xhr.open的第二个参数），因为一般是拿数据。

### GET请求及实例

AJAX发送GET请求并传递参数：

> 通常在一次 GET 请求过程中，参数传递都是通过 URL 地址中的 ? 参数传递。

```js
var xhr = new XMLHttpRequest() 
// GET 请求传递参数通常使用的是问号传参 
// 这里可以在请求地址后面加上参数，从而传递数据到服务端 
xhr.open('GET', './delete.php?id=1') 
// 一般在 GET 请求时无需设置响应体，可以传 null 或者干脆不传 
xhr.send(null) xhr.onreadystatechange = function () {   if (this.readyState === 4) {     console.log(this.responseText)   
	} 
}   
// 一般情况下 URL 传递的都是参数性质的数据，而 POST 一般都是业务数据
```

实例：要求在界面上把所有用户的名字打印到列表中，然后点击用户名可以再发送个请求——alert拿到用户年龄。

步骤：1.拿到所有的数据2.拿到想要的结果

```
//07-ajax-get.html的
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AJAX发送GET请求并传递参数</title>
</head>
<body>
  //3.的
  <ul id="list"></ul>

  <script>
    //3.的
    var listElement = document.getElementById('list')

    // 发送请求获取列表数据呈现在页面
    // =======================================

    var xhr = new XMLHttpRequest()
	1.拿到所有的数据
    xhr.open('GET', 'users.php')

    xhr.send()

    xhr.onreadystatechange = function () {
      if (this.readyState !== 4) return
      //2.拿到想要的结果。注意：转换字符串成json格式。之后先console.log(data)打印测试下再操作
      var data = JSON.parse(this.responseText)
      // data => 数据
	  //3.有了结果后就可以对它进行遍历了。写了循环后一样console.log测试下。可以挨个打印每一个对象后，就在html中动态创建个li放到ul中：给ul加个id方便操作它，在js一开始的地方把id获取到。
      for (var i = 0; i < data.length; i++) {
        //console.log(data[i])
        //4.在这动态创建每个li的元素，然后li放东西
        var liElement = document.createElement('li')
        liElement.innerHTML = data[i].name
        liElement.id = data[i].id
		//5.把li元素放到ul中
        listElement.appendChild(liElement)
//6.2 客户端：给每个li元素注册点击事件
        liElement.addEventListener('click', function () {
          // 7.TODO: 通过AJAX操作获取服务端对应数据的信息
          // 如何获取当前被点击元素对应的数据的ID——通过创建liElement.id = data[i].id拿到
          // console.log(this.id)
          var xhr1 = new XMLHttpRequest()
          xhr1.open('GET', 'users.php?id=' + this.id)
          xhr1.send()
          xhr1.onreadystatechange = function () {
            if (this.readyState !== 4) return
            var obj = JSON.parse(this.responseText)
            alert(obj.age)
          }
        })
      }
    }
//6.客户端：给每个li元素注册点击事件（由于不是JQ，所以要找到所以li遍历注册点击事件）。又因为 li 是后来动态创建的，而必须要创建时注册事件，所以不能这样注册事件。所以要到6.2那。
    // for (var i = 0; i < listElement.children.length; i++) {
    //   listElement.children[i].addEventListener('click', function () {
    //     console.log(111)
    //   })
    // }


    // var xhr = new XMLHttpRequest()
    // // 这里任然是使用URL中的问号参数传递数据
    // xhr.open('GET', 'users.php?id=2')
    // xhr.send(null)

    // xhr.onreadystatechange = function () {
    //   if (this.readyState !== 4) return
    //   console.log(this.responseText)
    // }

  </script>
</body>
</html>
```

```
//users.php的
<?php

header('Content-Type: application/json');

// `/users.php?id=1` => id 为 1 的用户信息

$data = array(
  array(
    'id' => 1,
    'name' => '张三',
    'age' => 18
  ),
  array(
    'id' => 2,
    'name' => '李四',
    'age' => 20
  ),
  array(
    'id' => 3,
    'name' => '二傻子',
    'age' => 18
  ),
  array(
    'id' => 4,
    'name' => '三愣子',
    'age' => 19
  )
);


if (empty($_GET['id'])) {
  // 没有 ID 获取全部
  // 因为 HTTP 中约定报文的内容就是字符串，而我们需要传递给客户端的信息是一个有结构的数据
  // 这种情况下我们一般采用 JSON 作为数据格式
  $json = json_encode($data); // => [{"id":1,"name":"张三"},{...}]
  echo $json;
} else {
  // 传递了 ID 只获取一条
  foreach ($data as $item) {
    if ($item['id'] != $_GET['id']) continue;
    $json = json_encode($item); // => [{"id":1,"name":"张三"},{...}]
    echo $json;
  }
}
```

### POST请求及实例

> POST 请求过程中，都是采用请求体承载需要提交的数据。

```js
var xhr = new XMLHttpRequest() 
// open 方法的第一个参数的作用就是设置请求的 method 
xhr.open('POST', './add.php') 
// 设置请求头中的 Content‐Type 为 application/x‐www‐form‐urlencoded 
// 标识此次请求的请求体格式为 urlencoded 以便于服务端接收数据 
xhr.setRequestHeader('Content‐Type', 'application/x‐www‐form‐urlencoded') // 需要提交到服务端的数据可以通过 send 方法的参数传递 // 格式：key1=value1&key2=value2 
xhr.send('key1=value1&key2=value2') xhr.onreadystatechange = function () {   if (this.readyState === 4) {     console.log(this.responseText)   
	} 
}
```

注意：实际开发中不能一会写js一会写php，一般先写好结果先测试下防止服务端出问题再写客户端功能。

> （但用浏览器直接去请求它，浏览器发的是get请求。怎么测试post请求？用个小工具Postman，它可以专门用来发各种类型请求、调试接口等。
>
> 测试post请求：输入.php所在网址，选post请求，多出来个body选项，点对应请求体格式，添加键值对如用户名、密码等，按send提交即可测试）
>
> 调试接口:输入接口地址，添加？后的参数按send

实例：要求页面不刷新把数据提交到服务端去（用form肯定会刷新，所以用table，技术用js+ajax）。

这里的loading代码块可以去掉：在网络请求慢时做加载效果

```
//08-ajax-post.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AJAX发送POST请求</title>
  <style>
    #loading {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: #555;
      opacity: .5;
      text-align: center;
      line-height: 300px;
    }

    #loading::after {
      content: '加载中...';
      color : #fff;
    }
  </style>
</head>
<body>
  <div id="loading"></div>
  <table border="1">
    <tr>
      <td>用户名</td>
      <td><input type="text" id="username"></td>
    </tr>
    <tr>
      <td>密码</td>
      <td><input type="password" id="password"></td>
    </tr>
    <tr>
      <td></td>
      <td><button id="btn">登录</button></td>
    </tr>
  </table>
  <script>

    // 写客户端js有一句话：找一个合适的时机，做一件合适的事情（做任何功能时首先要考虑这个东西在什么时候去工作：登录时，工作的内容是什么：把界面上的数据通过ajax提交到服务端）
    //0.时机：（怎么判断登陆时：通过点击按钮），所以给按钮注册点击事件
    var btn = document.getElementById('btn')
    // 1. 事情：1.1获取界面上的元素 value 
    var txtUsername = document.getElementById('username')
    var txtPassword = document.getElementById('password')
    var loading = document.getElementById('loading')

    btn.onclick = function () {
      //发请求就显示这个
      loading.style.display = 'block'
      //1.1获取界面上的元素 value
      var username = txtUsername.value
      var password = txtPassword.value
      // 1.2 通过 XHR 发送一个 POST 请求
      var xhr = new XMLHttpRequest()
      xhr.open('POST', 'login.php')
      // !!! 一定注意 如果请求体是 urlencoded 格式 必须设置这个请求头 ！！！
      xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
      // xhr.send('username=' + username + '&password=' + password)
//可以换成js中的模板字符串${变量名}，可以解析变量。    xhr.send(`username=${username}&password=${password}`)
      // 1.3 根据服务端的反馈 作出界面提示
      xhr.onreadystatechange = function () {
        if (this.readyState !== 4) return
        console.log(this.responseText)
        //一般响应处理完做这些操作：请求完就关掉加载效果
        loading.style.display = 'none'
      }
    }

  </script>
</body>
</html>
```

```
//login.php
<?php

// 接收用户提交的用户名密码：校验、响应
if (empty($_POST['username']) || empty($_POST['password'])) {
  // echo ;
  exit('请提交用户名和密码');
}
// 校验
$username = $_POST['username'];
$password = $_POST['password'];
if ($username === 'admin' && $password === '123') {
  exit('恭喜你登陆成功');
}

exit('用户名或者密码错误');
// 响应
```

## 同步模式和异步模式

> 同步：一个人在同一个时刻只能做一件事情。在执行一些耗时的操作（不需要看管）不去做别的事，只是等 待
>
> 异步：在执行一些耗时的操作（不需要看管）去做别的事，而不是等待

open 方法的第三个参数是 async (异步)可以传入一个布尔值，默认为 true

```js
//同步、异步涉及到这段代码执行时间的长短不一样：如在这段代码前后都用console.log输出，则异步会同时执行这2个输出，同步会出现愣等（阻塞）情况导致时间慢。可以用开始秒表console.time('秒表名')、结束秒表console.timeEnd('秒表名')来计时（计算中间代码执行的时候）

var xhrAsync= new XMLHttpRequest()
xhrAsync.open('GET', 'time.php', true)
console.time('async')
xhrAsync.send()
console.log(xhrAsync.responseText)
console.timeEnd('async')

// 同步模式 ajax 操作会有楞等的情况
// 区别在于 send 方法会不会出现等待情况
// 同步模式下send方法会直接给我们结果。一定要注意事件注册时间问题：若有事件注册，会来不及，而异步则是发send信号时，就去注册事件。
//不建议用同步模式，会降低用户体验。只有在封装时才有可能会使用
var xhrSync= new XMLHttpRequest()
xhrSync.open('GET', 'time.php', true)
console.time('sync')
xhrSync.send()
console.log(xhrSync.responseText)
console.timeEnd('sync')
```

## 响应的数据格式XML、JSON

提问：如果希望服务端返回一个复杂数据，该如何处理？

> 只要涉及到响应类型不同时，服务端应就要设置上合理的Content-Type。（告诉客户端；用上JQ等时，JQ会帮忙转换，若遇到不设置的JQ应对方法如$.getJSON）
>
> 不管服务端采用XML还是JSON，本质上都是将数据返回给客户端

- XML

一种数据描述手段，老掉牙的东西。淘汰的原因：数据冗余太多

用途：ajax里、或一些程序的配置文件里有用到

> XML也可以设样式，最早的网页就是用XML做的，如网易rss

问题在于：如果你客户端发一个AJAX请求，服务端返回个XML，那客户端怎么去解析它？了解即可

```xml
//xml.php
//如果想返回XML，一定要设Content-Type。否则客户端会当HTML解析
<?php
header('Content-Type: application/xml');
?>
//XML的文档头
<?xml version="1.1" encoding="utf-8"?>
<student>
    <name>张三</name>
    <age>18</age>
    <girl_friend>
        <name>李四</name>
    </girl_friend>
</student>
```

```
//11-ajax-xml.html:AJAX请求XML格式的数据
	var xhr = new XMLHttpRequest()
    xhr.open('GET', 'xml.php')
    xhr.send()
    xhr.onreadystatechange = function () {
      if (this.readyState !== 4) return
      //console.log(this.responseText)到这，能成功打印，问题是：怎么把xml中的数据解析拿出来。应对：只打印this时this还包含了responsexml:document
      // this.responseXML 专门用于获取服务端返回的 XML 数据，操作方式就是通过 DOM 的方式操作
      // 但是需要服务端响应头中的 Content-Type 必须是 application/xml。否则Content-Type会被客户端认为是text/html，则responsexml:null
      console.log(this.responseXML.documentElement.children[0].innerHTML)//张三      console.log(this.responseXML.documentElement.getElementsByTagName('name')[0])//张三
    }
```

- JSON

一种数据描述手段，类似于 JavaScript 字面量方式

服务端采用 JSON 格式返回数据，客户端按照 JSON 格式解析数据。

```
{
 "name": "张三",
 "age": 18,
 "girl_friend": {
	"name": "李四"
 }
}
```

> 不管是 JSON 也好，还是 XML，只是在 AJAX 请求过程中用到，并不代表它们之间有必然的联系，它们只是 数据协议罢了

## 客户端如何处理服务端响应的数据（处理响应数据渲染）

学习目的：一个（有结构的）数据怎么从服务端拿回来：通过json方式。拿回来过后，在客户端这边处理很麻烦（过往：大量DOM或拼接），可以拿模板引擎去处理。

### 以往操作：代码方式

动态渲染数据到表格中案例：

```
//12-ajax-table.html
<body>
  <table>
    <tbody id="content"></tbody>
  </table>
  <script>
    var xhr = new XMLHttpRequest()
    xhr.open('GET', 'test.php')
    xhr.send()
    xhr.onreadystatechange = function () {
      if (this.readyState !== 4) return
      //console.log(this.responseText)就能拿到JSON，直接把它转换解析了拿到服务端返回的结果res
      var res = JSON.parse(this.responseText)
      // res => 服务端返回的结果
      //再拿到res对象里的data数据，我们真正要遍历的数据
      var data = res.data 
      for (var i = 0; i < data.length; i++) {
       // console.log(data[i]) 拿到数据的每一行需要显示的东西
        // 用创建的方式
        // 先创建行
        // 再创建列
        // 再将列添加到行
        // 再将行添加到tbody
        var tr = document.createElement('tr')
        var td = document.createElement('td')
        td.innerHTML = data[i].id
        var td = document.createElement('td')
        td.innerHTML = data[i].id
        ...
        tr.append...
        ...
        // 或用innerHTML拼接的方式
        var tr = document.createElement('tr')
        tr.innerHTML = '<td>' + data[i].id + '</td><td></td><td></td><td></td><td></td><td></td>'
      }
    }
  </script>
</body>
```

到了以后学到agule、vue就不会写这些东西了：大量DOM操作、拼接，连整个document都不用再写了

### 模板方式

一个（有结构的）数据怎么从服务端拿回来：通过json方式。拿回来过后，在客户端这边处理很麻烦，可以拿模板引擎去处理。

采用技术：模板引擎。目的：更容易将数据渲染到html中

核心：给我个数据，给我个模板，我根据一个规则帮你执行完得到一个结果

> 实际并不陌生，php就好像个大号的模板引擎（与HTML混编才不觉得恶心），在服务端做的。

客户端开发技术：也有个模板引擎——如artTemplate：https://aui.github.io/art-template/，国内的，最重要的一点：有中文文档（切换语言再点文档按钮）。自己去熟悉

​	用法：把一个js文件引到页面当中，先写一个模板，写完模板之后准备一个数据，把数据跟模板同时扔到一个js文件所提供的一个方式里，就可以出结果了。

​	中文文档-安装-在浏览器中实时编译-下载js-保存起来。然后到页面当中去引用这个文件，再用script的方式去定义模板。

学东西的套路：照着手册一步步学

常见的流行模板引擎：Jade/pug、Handlebars、ejs、Nunjucks。用法都一样，看的就是一个套路。（一般选用一个东西：根据它在github上的活跃程度、协议、加星程度、关注程度一系列数字去决定）

参考：github.com/tj/consolidate.js#supported-template-engines（做node开发一个比较出名的作者做的常见模板引擎列表）

#### 使用模板引擎动态渲染表格实例

> 1.选择一个模板引擎     https:github.com/tj/consolidate.js#supported-template-engines
> 2.下载模板引擎JS文件
> 3.引入到页面中
> 4.准备一个模板
> 5.准备一个数据
> 6.通过模板引擎的JS提供的一个函数将模板和数据整合得到渲染结果HTML
> 7.将渲染结果HTML 设置到 默认元素的 innerHTML 中
>
>     注意：
>     一、script 标签的特点是（模板引擎盯上了）
>     1. innerHTML 永远不会显示在界面上
>         2. 如果 type 不等于 text/javascript 的话，内部的内容不会作为 JavaScript 执行
> 二、为什么不在JS变量中写模板？
>         如果将模板写到JS中，维护不方便，不能换行，没有着色。如var tmpl = '{{if user}}<h2>{{user.name}}</h2>{{/if}}'
>  三、为什么使用script标记写模板？
>         script不会显示在界面

```
<body>
  <table id="demo"></table>
  <!--4的，建议type这样写,其它模板引擎就text/x-... -->
  <script id="tmpl" type="text/x-art-template">
    //该模板引擎的遍历方法
    {{each comments}}
    <!-- each 内部 $value 拿到的是当前被遍历的那个元素。 -->
    <tr>
      <td>{{$value.author}}</td>
      <td>{{$value.content}}</td>
      <td>{{$value.created}}</td>
    </tr>
    {{/each}}
  </script>  
  <!--3的-->
  <script src="template-web.js"></script>
  <script>
    var xhr = new XMLHttpRequest()
    xhr.open('GET', 'test.php')
    xhr.send()
    xhr.onreadystatechange = function () {
      if (this.readyState !== 4) return
//5的
      var res = JSON.parse(this.responseText)
      // 模板所需数据
      var context = { comments: res.data }
      // 6的：借助模板引擎的API 渲染数据，参数：模板标记的id，数据
      var html = template('tmpl', context)
      console.log(html)//->渲染过后的结果
      //7的
      document.getElementById('demo').innerHTML = html
    }
  </script>
</body>
```



## XMLHttpRequest的兼容方案（面试）

XMLHttpRequest 在老版本浏览器（**IE5/6**）中有兼容问题，可以通过另外一种方式代替（三元表达式判断一下支持、不支持）

```
var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP')
```

面试时考ajax时一定把这点写上，ajax考的就是这点

## AJAX的封装

封装的套路：

1. 写一个相对比较完善的用例

2. 写一个空函数，没有形参，将刚刚的用例直接作为函数的函数体
3. 根据使用过程中的**需求**抽象参数

接下来开始进行封装

1.写一个相对比较完善的用例

```
var xhr = new XMLHttpRequest()
xhr.open('GET','time.php')
xhr.send(null)
xhr.onreadstatechange = function () {
	if (this.readyState !==4) return
	console.log(this.responseText)
}
```

2.写一个空函数funcion ajax(){}，没有形参，将刚刚的用例直接作为函数的函数体。到这就能调用ajax()了，但到这只是最基本的封装，差得还很远

```
funcion ajax(){
	var xhr = new XMLHttpRequest()
    xhr.open('GET','time.php')
    xhr.send(null)
    xhr.onreadstatechange = function () {
        if (this.readyState !==4) return
        console.log(this.responseText)
    }
}
//调用
ajax()
```

3.**根据**使用过程中的**需求 **抽象参数

版本1：

根据不同的需求：open的请求方式、地址会发生变化；当请求方式为POST，send的参数会变化；所以要把它们从写死的状态换成一个传入的参数。method(问题：当open请求方式是小写也能传入，我们的封装代码却不能正常执行，所以要转大写。), url, params(问题1：当传入第三个参数时，下面的调用1也要有对应的参数null。但调用1要也要写参数麻烦->最好有个默认值var params=params||null。问题2:params传入urlencoded型数据时需要告诉服务端Content-Type，要设置响应头->必须要有个设置操作xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')。问题2.1：不为POST请求时，不设置响应头->给个判断,但到这里发现send参数的设置就不大好了，所以优化掉，进入版本2)

```
funcion ajax(method, url, params){
	method = method.toUpperCase()
	var xhr = new XMLHttpRequest()
    xhr.open(method, url)
    if (method === 'POST') {
    	xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
    }
    
    var params = params || null
    
    xhr.send(params)
    xhr.onreadstatechange = function () {
        if (this.readyState !==4) return
        console.log(this.responseText)
    }
}
//调用
ajax('GET', 'time.php')
ajax('POST', 'add.php', 'key1=value1&key2=value2')
ajax('get', 'time.php')
ajax('post', 'add.php', 'key1=value1&key2=value2')
```

版本2：也是基本封装，只是相对完善

参数params的问题1.1：params设置优化——如果不是POST请求就永远是null，是POST就取params；如果是get请求，除了null也有可能传参数（如id这参数放url里），所以要对url进行处理。

```
funcion ajax(method, url, params){
	method = method.toUpperCase()
	var xhr = new XMLHttpRequest()
	
	if (method === 'GET') {
      url += '?' + params
    }
	
    xhr.open(method, url)
    
    var data = null
    if (method === 'POST') {
    	xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
    	data = params
    }
    
    xhr.send(data)
    xhr.onreadstatechange = function () {
        if (this.readyState !==4) return
        console.log(this.responseText)
    }
}
//调用
ajax('GET', 'time.php','id=1')
ajax('POST', 'add.php', 'key1=value1&key2=value2')
```

版本3：

问题1：上个版本中params传入参数是像key1=value1&key2=value2这样结构，看着太恶心写起来也麻烦，所以改进：希望params传入的是个对象而不是字符串。而调用时直接传入对象查看Network请求不行，所以要把params（的对象实参）转成key1=value1&key2=value2这样格式

```
funcion ajax(method, url, params){
	method = method.toUpperCase()
	var xhr = new XMLHttpRequest()
	
	if (typeof params === 'object') {
		var tempArr = []
		//遍历对象的每一个键
		for (var key in params) {
		   //拿到它每一个值
           var value = params[key]
           //把每对键值拼接起来：tempArr => [ 'key1=value1', 'key2=value2' ]
           tempArr.push(key + '=' + value)
           //要得到格式：params => 'key1=value1&key2=value2'。所以要join连接起来
           params = tempArr.join('&')
        }
	}
	
	if (method === 'GET') {
      url += '?' + params
    }
	
    xhr.open(method, url)
    
    var data = null
    if (method === 'POST') {
    	xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
    	data = params
    }
    
    xhr.send(data)
    xhr.onreadstatechange = function () {
        if (this.readyState !==4) return
        console.log(this.responseText)
    }
}
//调用
ajax('GET', 'time.php',{ id: 1 })
ajax('POST', 'add.php', { key1: 'value1',key2: 'value2' })
```

版本4：

核心问题：不应该在封装的函数中主观地处理响应结果（把我们之前写的console.log()去掉，alert()也不能写），所以要有返回值。

> 但无法在内部包含的函数中通过return  给外部函数的调用返回结果，所以要用作用链的方式拿到返回值：
>
> function foo () {
>     var res
>     function bar () {
>     res = 123
>     }
>     bar()
>     return res
> }

但又引起来了新的问题：代码执行顺序：

```
funcion ajax(method, url, params){
	var res = null

	method = method.toUpperCase()
	var xhr = new XMLHttpRequest()
	
	if (typeof params === 'object') {
		var tempArr = []
		for (var key in params) {
           var value = params[key]
           tempArr.push(key + '=' + value)
           params = tempArr.join('&')
        }
	}
	
	if (method === 'GET') {
      url += '?' + params
    }
	
    xhr.open(method, url)
    
    var data = null
    if (method === 'POST') {
    	xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
    	data = params
    }
    
    xhr.send(data)
    xhr.onreadstatechange = function () {
        if (this.readyState !==4) return
        //不应该在封装的函数中主观的处理响应结果
     	//console.log(this.responseText)
        //无法在内部包含的函数中通过 return 给外部函数的调用返回结果
        // return this.responseText
		// 由于异步模式下（这儿代码刚开始执行外部代码比这儿早且仍在执行） 这里的代码最后执行 所以不可能在外部通过返回值的方式返回数据
		//用同步：oepn参数加个false，且事件移到send前。但强烈拒绝使用，所以到这代码就写不下去了。就要用到js的一个操作：委托（回调）
		res = this.responseText
    }
	return res
}
//调用
ajax('GET', 'time.php',{ id: 1 })
ajax('POST', 'add.php', { key1: 'value1',key2: 'value2' })
```

版本5：最终版，未成形

由于版本4的方向错误，所以回到版本4前，回到开始的问题是：不应该在封装的函数中主观的处理响应结果（即封装者不能去主观地处理调用者的事情，如console.log就不行）->版本4用返回值的做法不行，无法返回->怎么样不主观：你告诉我该做什么事情。用委托（js中叫回调）：即调用者委托（让）封装者拿到数据后，**再告诉封装者拿着数据去做什么事情**->参数4：done

```
// 封装者
function ajax (method, url, params, done) {
   method = method.toUpperCase()
   var xhr = new XMLHttpRequest()

   if (typeof params === 'object') {
     var tempArr = []
     for (var key in params) {
        var value = params[key]
        tempArr.push(key + '=' + value)
      }
      params = tempArr.join('&')
     }

     if (method === 'GET') {
        url += '?' + params
     }

     xhr.open(method, url, false)

     var data = null
     if (method === 'POST') {
       xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
       data = params
     }

     xhr.onreadystatechange = function () {
       if (this.readyState !== 4) return
       // 不应该在封装的函数中主观的处理响应结果
       // console.log(this.responseText)
       // 你说我太主观，那么你告诉我应该做什么
       done(this.responseText)
     }
     xhr.send(data)
    }

   // 调用者,这儿分步骤好理解
   var onDone = function (res) {
     console.log('hahahahaha')
     console.log('hohohohoho')
     console.log(res)
     console.log('做完了')
   }

   ajax('get', 'time.php', {}, onDone)
   //实际调用写
   ajax('get', 'time.php', {}, function (res) {
     console.log('hahahahaha')
     console.log('hohohohoho')
     console.log(res)
     console.log('做完了')
   })
```

### 最终版

```js
 /**  * 发送一个 AJAX 请求  * @param  {String}   method 请求方法  * @param  {String}   url    请求地址  * @param  {Object}   params 请求参数  * @param  {Function} done   请求完成过后需要做的事情（委托/回调）  */ function ajax (method, url, params, done) {   // 统一转换为大写便于后续判断   method = method.toUpperCase()   
 
 // 对象形式的参数转换为 urlencoded 格式   var pairs = []   
 for (var key in params) {     pairs.push(key + '=' + params[key])   
 }   
 var querystring = pairs.join('&')     
 	var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new  ActiveXObject('Microsoft.XMLHTTP')  
 		 xhr.addEventListener('readystatechange', function () {     
 	if (this.readyState !== 4) return      
 	// 尝试通过 JSON 格式解析响应体     
 	try {       
 		done(JSON.parse(this.responseText))     } catch (e) {       
 		done(this.responseText)     
 		}   
 	})     
 
 // 如果是 GET 请求就设置 URL 地址 问号参数   if (method === 'GET') {     url += '?' + querystring   
  }  
  
  xhr.open(method, url)  
  
  // 如果是 POST 请求就设置请求体   
  var data = null  
  if (method === 'POST') {     xhr.setRequestHeader('Content‐Type', 'application/x‐www‐form‐urlencoded')     data = querystring   
  }   
  xhr.send(data) 
} 
```

调用

```js
ajax('get', './get.php', { id: 123 }, function (data) {   
	console.log(data) 
})  
ajax('post', './post.php', { foo: 'posted data' }, function (data) {   
	console.log(data)
})
```

但一般我们都是使用别人封装好的，功能比较完善。

jQuery 中有一套专门针对 AJAX 的封装，功能十分完善，经常使用，需要着重注意。1.几版兼容性最好，3.几最新。简单使用可看code，详细看下面官方手册。

这些（原生、封装）API记住使用过程就好。

参考：
http://www.jquery123.com/category/ajax/

http://www.w3school.com.cn/jquery/jquery_ref_ajax.asp

## 回调

简单实例

```
<script>

    function getTimestamp (done) {

      setTimeout(function () {

        // 执行调用者指定的事情
        done(Date.now())

      }, 1000)

    }

    // ========================================

    // 指定拿到数据过后怎么做
    var done = function (timestamp) {
      console.log(timestamp / 1000 / 60 / 60)
    }
    getTimestamp(done)

  </script>
```

js核心：回调

### 回调的嵌套情况

以后的js代码可能会出现这种情况：需要请求一个a地址，拿到响应的结果之后再去请求b地址->那么代码中会出现回调函数中可能会再出现ajax，如下面这种恶心的结构：

```
console.log(1)//第1次执行
ajax('time.php', function (res) {
  console.log(3)//第3次执行
  ajax('time.php', function (res) {
    ajax('time.php', function (res) {
      ajax('time.php', function (res) {
        ajax('time.php', function (res) {
          ajax('time.php', function (res) {

          })
        })
      })
    })
  })
  console.log(4)//第4次执行
})
console.log(2)//第2次执行
```

那么可能会有这样的方案：（then然后）

```
ajax('time.php')
  .then(function (res) {
    return ajax('time.php')
  })
  .then(function (res) {
    return ajax('time.php')
  })
  .then(function (res) {
    return ajax('time.php')
  })
  .then(function (res) {
    return ajax('time.php')
  })
//注意回调黑洞（死循环）问题，如：
function load () {
  ajax('time.php', load)
}
```

## JQ的ajax

$.ajax、$.get、$.post、$.getJSON、load方法、$.getScript

如

```
$.ajax('./time.php', {
  type: 'post', // method 请求方法
  success: function (res) {
    // res => 拿到的只是响应体
    console.log(res)
  }
})
```

## JQ的load方法(局部刷新)

实现页面的  局部刷新 效果，能节省请求，如不用再请求css、js等文件

在jQuery封装的ajax下。跟ajax关系不大，但是用ajax实现的

在某一个div或元素中面去载入另外一个页面的另外一个区域

实例：局部刷新（加载）、在页面上做一些加载提示

如何做得更好？切换时希望知道在加载过程中。看下栏

### 全局事件处理函数

全局事件处理函数作用：如将所有ajax请求的公共操作注册成ajax的全局事件，让它只要发ajax请求就去自动帮我们执行

参考：http://www.jquery123.com/category/ajax/global-ajax-event-handlers/

```
<script>
  $(function ($) {
     $(document)
       .ajaxStart(function () {
         // 只要有 ajax 请求发生 就会执行
        $('.loading').fadeIn()
         // 显示加载提示
         console.log('注意即将要开始请求了')
       })
       .ajaxStop(function () {
         // 只要有 ajax 请求结束 就会执行
         $('.loading').fadeOut()
         // 结束提示
         console.log('请求结束了')
       })

    $('.list-group-item').on('click', function () {
      var url = $(this).attr('href')
      $('#main').load(url + ' #main > *')
      return false 
    })
  })
</script>
```

### 最常见的加载进度方式

配合NProgress显示加载进度。

github、知乎等都有在用：只在网址栏下面走进度条——请求响应，响应结果完就一下过了。

要想用：有个NProgress库——使用其中的js、css文件。且最好都在页头引入。

## 跨域

跨域实际跟ajax无关。

过去不支持不同源地址之前的ajax请求，现在支持了（存在兼容、需要服务端进行一些配置），但我们仍要了解。

同源策略是浏览器的一种**安全策略**。所谓同源是指**域名，协议，端口完全相同**，只有同源的地址才可以相互通过 AJAX 的方式请求。

同源或者不同源说的是两个地址之间的关系，不同源地址之间请求我们称之为**跨域请求**

> 之前学的能自动发送请求的方式：img、link、script、iframe。表单、a连接要点或做些操作才能
>
> iframe:浏览器自带的功能，在页面中挖一个坑去载入另一个页面，跟load类似（而load是通过ajax、自己代码实现的）。

如何解决：通过JSONP技巧

### JSONP技巧

JSON with Padding，是一种借助于 script 标签发送跨域请求的技巧。

原理：客户端通过 script 标签请求服务端的 一个动态网页(如php文件)。该文件返回一段 能调用一个函数的JS。该JS作用：**调用**我们事先定义好的一个**函数**，从而将服务端想要给客户端发过去的**数据发送给客户端**

> 注意：1. JSONP 需要服务端配合，服务端按照客户端的要求返回一段 JavaScript 调用客户端的函数
> 2.只能发送 GET 请求
> 3.jQuery 中使用 JSONP 就是将 dataType 设置为 jsonp
> 4.其他常见的 AJAX 封装 库：Axios

实例：server.php、client.html（较多）

```
//server.php
<?php

$conn = mysqli_connect('localhost', 'root', '123456', 'demo');

$query = mysqli_query($conn, 'select * from users');
//这儿的$data就是我们想要的数据。数据库代码写完进网页看能否正常请求或用Postman
while ($row = mysqli_fetch_assoc($query)) {
  $data[] = $row;
}

// 如果客户端采用的是 script 标记对我发送的请求
// 一定要返回一段 JavaScript
// 输出的内容不能再是普通的json字符串了，而要在外面包裹一个函数的调用。注意：这里客户端指定函数名字aaabbb
header('Content-Type: application/javascript');
$result = json_encode($data);
//echo "aaabbb({$result})";

//如果没有传入callback参数不想以jsonp方式操作，就设json支持普通方式，不然继续往下走
if (empty($_GET['callback'])) {
  header('Content-Type: application/json');
  echo json_encode($data);
  exit();
}

//服务端接收随机函数名。注意：关联数组必须要写花括号。
//echo "{$_GET['callback']}({$result})";
//优化：若明确定义了函数，采取调用函数，就不会报错。
$callback_name = $_GET['callback'];
echo "typeof {$callback_name} === 'function' && {$callback_name}({$result})";
```

```
//client.html JSONP基本使用
//在客户端发起跨域请求
<script>
//var script = //document.createElement('script')
//script.src = 'http://localhost/jsonp/server.php'
//document.body.appendChild(script)

////准备一个函数，让服务端去调用
//function aaabbb (data) {
//   console.log('1111', data)
//}
//但以上代码重复执行2次就会出问题：第二次的console.log会覆盖第一次的。所以要给每一次请求设置唯一的（或不同的回调）函数

var script = document.createElement('script')
script.src = 'http://localhost/jsonp/server.php?callback=' + funcName
document.body.appendChild(script)

//2.随机生成一个函数名，可去测试下。随机数也可能会重复，所以加毫秒数就不大可能了。注意随机数格式。随机生成的函数，服务端不知道，所以要加到请求中
var funcName = 'jsonp_' + Date.now() + Math.random().toString().substr(2, 5)
//1.全局函数都在window底下。那['']用一个字符串去传递函数的名字，好处：[]里可以通过随机数或时间戳等来生成随机性函数名，这样就不重复了
window[funcName] = function  (data) {
   console.log('1111', data)
}
</script>
```

### JSONP封装

有了个用例之后，开始封装。1.封装的参数跟$.get一样	2.url替换 3.callback替换 4.get会传入如id等参数——params，解析下。

```
function jsonp (url, params, callback) {
  var funcName = 'jsonp_' + Date.now() + Math.random().toString().substr(2, 5)
  //解析url传入的参数
  if (typeof params === 'object') {
    var tempArr = []
    for (var key in params) {
      var value = params[key]
      tempArr.push(key + '=' + value)
    }
    params = tempArr.join('&')
  }


  var script = document.createElement('script')
  //2的
  script.src = url + '?' + params + '&callback=' + funcName
  document.body.appendChild(script)

  window[funcName] = function (data) {
    //3的
    callback(data)
    //每次用完了就删除随机函数，然后移除scirpt标记
    delete window[funcName]    	document.body.removeChild(script)
  }
}

//调用
jsonp('http://localhost/jsonp/server.php', { id: 123 }, function (res) {
  console.log(res)
})

jsonp('http://localhost/jsonp/server.php', { id: 123 }, function (res) {
  console.log(res)
})
```

JQ也有封装JSONP，使用跟$.get类似

基本使用如：

```
$.ajax({
      url: 'http://localhost/jsonp/server.php',
      dataType: 'jsonp',
      success: function (res) {
        console.log(res)
      }
})
```

总结：因为 XMLHttpRequest 这个对象不支持对不同源地址之间的跨域请求，所以我们找到了script标记

面试回答：它实际上是借用了script标记可以发送不同源地址请求的一个特性去完成的一个跨域请求

### AJAX跨域（CORS）

Cross Origin Resource Share，跨域资源共享

现在支持不同源地址之前的ajax请求，不过存在兼容问题、需要进行一些服务端的配置。

之前有个问题：涉及到AJAX操作的页面”不能“通过文件方式访问——就是跨域问题，现在也可以解决了。

1.服务端只需一行代码搞定：允许跨域请求header('Access-Control-Allow-Origin: *');

```
<?php

$conn = mysqli_connect('localhost', 'root', '123456', 'demo');

$query = mysqli_query($conn, 'select * from users');

while ($row = mysqli_fetch_assoc($query)) {
  $data[] = $row;
}

// 一行代码搞定
// 允许跨域请求：允许所有源对我这个源发起请求
//指定源：就把*换成网址
header('Access-Control-Allow-Origin: *');

header('Content-Type: application/json');
echo json_encode($data);
```

2.客户端不用做任何修改

```
<script src="jquery.js"></script>
  <script>

    $.get('http://localhost/cors.php', {}, function (res) {
      console.log(res)
    })

  </script>
```

