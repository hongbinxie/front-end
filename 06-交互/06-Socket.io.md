在看该文档前，建议先看下Node.js。

## 什么是Socket.IO

Socket.IO是一个库，可用于在浏览器和服务器之间进行**实时**，**双向**和基于**事件(异步，不用一直等)**的通信。它包括：

- 使Node.js服务器：[来源](https://github.com/socketio/socket.io) | [API](https://socket.io/docs/server-api/)
- 为浏览器（可从Node.js的也运行）一个JavaScript客户端库：[来源](https://github.com/socketio/socket.io-client) | [API](https://socket.io/docs/client-api/)

其主要特点是：

### 可靠性

即使存在以下情况，也会建立连接：

- 代理和负载平衡器。
- 个人防火墙和防病毒软件。

为此，它依赖于[Engine.IO](https://github.com/socketio/engine.io)，该[引擎](https://github.com/socketio/engine.io)首先建立长轮询连接，然后尝试升级到在侧面进行“测试”的更好传输，例如WebSocket。请参阅“ [目标”](https://github.com/socketio/engine.io#goals)部分以获取更多信息。

> socket.io既能支持老版本浏览器，又支持新版本浏览器。而WebSocket只支持新版本浏览器

### 自动重新连接支持

除非另有指示，否则断开连接的客户端将尝试永久重新连接，直到服务器再次可用为止。请在[此处](https://socket.io/docs/client-api/#new-Manager-url-options)查看可用的重新连接选项。

### 断线检测

心跳机制在Engine.IO级别上实现，使服务器和客户端都可以知道对方何时不再响应。

通过在服务器和客户端上设置计时器，并在连接握手期间共享超时值（pingInterval和pingTimeout参数），可以实现该功能。这些计时器要求将任何后续客户端调用都定向到同一服务器，因此使用多个节点时需要执行粘性会话。

### 二进制支持

可以发出任何可序列化的数据结构，包括：

- 浏览器中的[ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)和[Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)
- Node.js中的[ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)和[Buffer](https://nodejs.org/api/buffer.html)

### 多路传输支持

为了在应用程序内创建关注点分离（例如，每个模块或基于权限），Socket.IO允许您创建多个[Namespaces](https://socket.io/docs/rooms-and-namespaces/#Namespaces)，它们将充当单独的通信通道，但将共享相同的基础连接。

> 比如2个群，群里可以互相通信，但不能与群外去互相通信

### 客房支援

> 比如群里面还可以分组，后面组里通信不跟组外通信

在每个[Namespace中](https://socket.io/docs/rooms-and-namespaces/#Namespaces)，您可以定义套接字可以加入和离开的任意通道，称为[Rooms](https://socket.io/docs/rooms-and-namespaces/#Rooms)。然后，您可以广播到任何给定的房间，到达已加入该房间的每个插槽。

这是有用的功能，用于向一组用户或连接到多个设备的给定用户发送通知。

这些功能附带一个简单便捷的API，如下所示：

```
io.on（'connection'，function（socket） { 
  socket.emit（'request'，/ * * /）; //向套接字发出事件
   io.emit（'broadcast'，/ * * /）; / /向所有连接的套接字发出事件
   socket.on（'reply'，function（） { / * * / }）; //监听事件
 }）;
```

## 什么不是Socket.IO

Socket.IO **不是** WebSocket实现。尽管Socket.IO确实确实在可能的情况下使用WebSocket作为传输工具，但它会向每个数据包添加一些元数据：当需要消息确认时，数据包类型，名称空间和数据包ID。这就是为什么WebSocket客户端将无法成功连接到Socket.IO服务器，而Socket.IO客户端也将无法连接到WebSocket服务器的原因。请在[此处](https://github.com/socketio/socket.io-protocol)查看协议规范。

```
//警告：客户端将无法连接！
const client = io（'ws：//echo.websocket.org'）;
```

## 怎么安装

### 服务器

```
npm install --save socket.io
```

[资源](https://github.com/socketio/socket.io)

### Javascript客户端

> 也可以下载，点击顶部来源，然后下载或复制dist（打包好的）的socket.io.js(压缩)或... .io.dev.js(不压缩)

默认情况下，服务器会公开客户端的独立版本`/socket.io/socket.io.js`。

也可以从CDN提供服务，例如[cdnjs](https://cdnjs.com/libraries/socket.io)。

若要从Node.js的使用就像一个捆绑使用，或[的WebPack](https://webpack.js.org/)或[browserify](http://browserify.org/)，您还可以安装NPM包：

```
npm install-save socket.io-client
```

[资源](https://github.com/socketio/socket.io-client)

### 其他客户端实施

有几种其他语言的客户端实现，由社区维护：

- Java：[https](https://github.com/socketio/socket.io-client-java)：[//github.com/socketio/socket.io-client-java](https://github.com/socketio/socket.io-client-java)
- C ++：[https](https://github.com/socketio/socket.io-client-cpp)：[//github.com/socketio/socket.io-client-cpp](https://github.com/socketio/socket.io-client-cpp)
- 斯威夫特：[https](https://github.com/socketio/socket.io-client-swift) : [//github.com/socketio/socket.io-client-swift](https://github.com/socketio/socket.io-client-swift)
- 飞镖：[https](https://github.com/rikulo/socket.io-client-dart)：[//github.com/rikulo/socket.io-client-dart](https://github.com/rikulo/socket.io-client-dart)
- Python：[https](https://github.com/miguelgrinberg/python-socketio)：[//github.com/miguelgrinberg/python-socketio](https://github.com/miguelgrinberg/python-socketio)
- .Net：[https](https://github.com/Quobject/SocketIoClientDotNet)：[//github.com/Quobject/SocketIoClientDotNet](https://github.com/Quobject/SocketIoClientDotNet)

## 与Node http服务器一起使用

### 服务器（app.js）

```
var app = require('http').createServer(handler)
var io = require('socket.io')(app);
var fs = require('fs');

app.listen(80);

function handler (req, res) {
  fs.readFile(__dirname + '/index.html',
  function (err, data) {
    if (err) {
      res.writeHead(500);
      return res.end('Error loading index.html');
    }

    res.writeHead(200);
    res.end(data);
  });
}

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});  
```

### 客户端（index.html）

```
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io('http://localhost');
  socket.on('news', function (data) {
    console.log(data);
    socket.emit('my other event', { my: 'data' });
  });
</script>
```

## 与Express一起使用

### 服务器（app.js）

```
var app = require('express')();
var server = require('http').Server(app);
var io = require('socket.io')(server);

server.listen(80);
// WARNING: app.listen(80) will NOT work here!

app.get('/', function (req, res) {
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});
```

### 客户端（index.html）

```
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io.connect('http://localhost');
  socket.on('news', function (data) {
    console.log(data);
    socket.emit('my other event', { my: 'data' });
  });
</script>
```

## 发送和接收事件

Socket.IO允许您发射和接收自定义事件。此外`connect`，`message`和`disconnect`，你可以发出自定义事件：

### 服务器

```
// note, io(<port>) will create a http server for you
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  io.emit('this', { will: 'be received by everyone'});

  socket.on('private message', function (from, msg) {
    console.log('I received a private message by ', from, ' saying ', msg);
  });

  socket.on('disconnect', function () {
    io.emit('user disconnected');
  });
});
```

## 将自己限制为名称空间

如果您可以控制为特定应用程序发出的所有消息和事件，则可以使用默认值/命名空间。如果您想利用第三方代码或生成与他人共享的代码，socket.io提供了一种命名套接字的方式。

这具有`multiplexing`单个连接的优点。不是使用两个`WebSocket`连接，而是使用一个连接。

### 服务器（app.js）

```
var io = require('socket.io')(80);
var chat = io
  .of('/chat')
  .on('connection', function (socket) {
    socket.emit('a message', {
        that: 'only'
      , '/chat': 'will get'
    });
    chat.emit('a message', {
        everyone: 'in'
      , '/chat': 'will get'
    });
  });

var news = io
  .of('/news')
  .on('connection', function (socket) {
    socket.emit('item', { news: 'item' });
  });
```

### 客户端（index.html）

```
<script>
  var chat = io.connect('http://localhost/chat')
    , news = io.connect('http://localhost/news');
  
  chat.on('connect', function () {
    chat.emit('hi!');
  });
  
  news.on('news', function () {
    news.emit('woot');
  });
</script>
```

## 发送易失性消息

有时可能会丢弃某些消息。假设您有一个应用程序可显示关键字的实时推文`bieber`。

如果某个客户端尚未准备好接收消息（由于网络速度慢或其他问题，或者由于它们是通过长时间轮询连接的，并且处于请求-响应周期的中间），则它没有接收到所有推文与bieber相关，您的应用程序不会受到影响。

在这种情况下，您可能希望将这些消息作为易失性消息发送。

### 服务器

```
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  var tweets = setInterval(function () {
    getBieberTweet(function (tweet) {
      socket.volatile.emit('bieber tweet', tweet);
    });
  }, 100);

  socket.on('disconnect', function () {
    clearInterval(tweets);
  });
});
```

## 发送和获取数据（确认）

有时，当客户端确认消息接收后，您可能希望获得回调。

为此，只需将函数作为`.send`或的最后一个参数传递即可`.emit`。而且，当您使用时`.emit`，确认是由您完成的，这意味着您还可以传递数据：

### 服务器（app.js）

```
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  socket.on('ferret', function (name, word, fn) {
    fn(name + ' says ' + word);
  });
});
```

### 客户端（index.html）

```
<script>
  var socket = io(); // TIP: io() with no args does auto-discovery
  socket.on('connect', function () { // TIP: you can avoid listening on `connect` and listen on events directly too!
    socket.emit('ferret', 'tobi', 'woot', function (data) { // args are sent in order to acknowledgement function
      console.log(data); // data will be 'tobi says woot'
    });
  });
</script>
```

## 广播消息

要广播，只需`broadcast`在`emit`和`send`方法调用中添加一个标志。广播意味着将消息发送到其他人（除了启动该消息的套接字之外）。

### 服务器

```
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  socket.broadcast.emit('user connected');
});
```

## 像跨浏览器的WebSocket一样使用它

如果只需要WebSocket语义，也可以这样做。只需利用`send`并收听`message`事件：

### 服务器（app.js）

```
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  socket.on('message', function () { });
  socket.on('disconnect', function () { });
});
```

### 客户端（index.html）

```
<script>
  var socket = io('http://localhost/');
  socket.on('connect', function () {
    socket.send('hi');

    socket.on('message', function (msg) {
      // my msg
    });
  });
</script>
```

如果您不关心此类的重新连接逻辑，请查看[Engine.IO](https://github.com/socketio/engine.io)，这是Socket.IO使用的WebSocket语义传输层。

# 教程

> 要知道连接是以事件来进行操作：connection、emit、on

## 使用方法1：基本的

客户端

1、先下载，点击顶部来源，然后下载或复制dist（打包好的）的socket.io.js(压缩)或... .io.dev.js(不压缩)

2、创建新项目(这里为了方便可以使用Hbuilder创建基本html项目，无需自己创建目录结构)，引入（引入后就会创建个io对象给你使用。输出下io，有，说明引入成功）

服务器端

最基础操作：

1、创建新项目，复制与Node http服务器一起使用下的服务器(app.js)的代码，放入到.js文件中。

下面开始分析下（可跳过）

```js
var app = require('http').createServer(handler)//1、创建serve
var io = require('socket.io')(app);//3、创建服务里，需要用到实时通讯的话，只需要把socket.io引用进来，引进来后，就把app这个我们创建的应用服务传进去就可以了。2个括号：引用socket.io对象、然后用socket.io去实例化一个io对象 ：app。就可以通过这个id对象去实行数据的双向绑定、连接。可以写成var socketio = require('socket.io') var io = socketio(app);
var fs = require('fs');

app.listen(80);	//4、启动监听80的端口

//处理WEB服务器正常的请求
function handler (req, res) {//2、创建serve后，这里就会有个handler函数。这个内容其实写不写都无所谓，因为这个只是告诉你怎么去出来这个服务
  fs.readFile(__dirname + '/index.html', //读文件。就会读当前文件夹下有没index.html。如果有，就输入index.html。（它这没有去判断请求，只是把整个html输出出去，很简单的一个操作）
  function (err, data) {//读出来之后输出
    if (err) {
      res.writeHead(500);
      return res.end('Error loading index.html');
    }

    res.writeHead(200);
    res.end(data);
  });
}

//5、实时通讯的连接（on）
//io.on('connection',事件的回调函数)监听socketio的连接事件：一旦有哪个客户端向我连接了，就会触发这个事件的内容（即一旦连接进来，我就会执行这个函数）
io.on('connection', function (socket) {//执行这个函数之后我都做了什么事情呢？1.传入连接的套接字对象
    //socket.emit() 发送客户端数据：发送事件名、发送的内容
  socket.emit('news', { hello: 'world' });//2.这个连接对象触发了一个事件news：向客户端发送news事件，并将news的数据对象发送给客户端
    //监听客户端发送过来的内容
  socket.on('my other event', function (data) {//3.同时又监听了另一个事件my other event，如果别人有什么操作进来，就在这里进行一个相对应的执行
    console.log(data);
  });
});  
```

2、创建服务器的index.html,随便写个hello socketio

3、运行服务器看一下能不能收到socket.emit()发送的数据：打开终端，运行node index.js

> (错误处理：没有发现socktet.io的模块。应对：运行或再一次运行npm install --save socket-io。--save表示保存到package.json中，我们可以不写)

4、客户端进行连接（服务器不要关）：（之前我们已经引入了socket.io.js。）现在告诉服务器   连接的是谁（在客户端的index.html中写）

```js
let con = io.connect("http://localhost")	//告诉 连接的是谁
con.on('news',function(data){
    console.log(data)
})	//监听有没人给你发news，来得到数据;一旦有数据触发，就进行相应操作：这里先试着输出下数据看有没拿到。因为服务器跟客户端连接时，给客户端发了个带数据的news事件
con.emit('my other event',{
    uaername:"大哥",
    chatcontent:"吃饭了没？"
})	//收到数据后要反馈才能得到对方的又一次发送数据。所以emit()发送个数据对象给服务器：比如发吃饭了没
```

5、看下服务器有没收到客户端的数据（注意：一刷新，又会多一条客户端的数据）

> （为什么会收到？因为客户端在写代码时就会**实时**进行更新：客户端一更新，socketio就会立马执行客户端内容，然后立马发送消息）

6、客户端也有监听连接的事件（不只服务器有），写完下面代码，运行客户端查看效果

```js
let con = io.connect("http://localhost") //可以去控制台输入con，查看下连接事件长啥样（里面的id是唯一标识，服务器也可以通过id向你发送消息。服务端发送的二进制出数据、json数据这里也能看得到）	
con.on('connect',function(data){//监听连接，触发后执行相应操作
    console.log("连接事件")
    //console.log(data)	//data这时是没有的，因为服务器没有给它发送数据
})
con.on('news',function(data){
    console.log(data)
})
con.emit('my other event',{
    uaername:"大哥",
    chatcontent:"吃饭了没？"
})	
```

7、一般情况下，不会自己去写一个服务器，都会用express框架

## 使用方法2：与exprss框架一起使用

> 用express来实现服务器功能

> 用express框架该怎么实现服务器功能呢？express也会得到一个app，也是一样对它进行操作即可。下面会讲如何创建express对象，来进行连接操作

### 简化版(直接引入express)

1、创建新项目，复制与express一起使用下的服务器(app.js)的代码，放入到.js文件中。

下面进行分析（可跳过）

```js
var app = require('express')();	//1、引入express对象，实例化一个app。
var server = require('http').Server(app);//2、创建serve
var io = require('socket.io')(server);//3、与socketio进行一个连接。这样socketio就会自动地与require('http')关联起来

server.listen(80);
// WARNING: app.listen(80) will NOT work here!


//socketio就会自动地与require('http')关联起来，所以app.get、io.on就会同时启用，而且可以访问首页index.html
app.get('/', function (req, res) {
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});
```

2、运行服务器：node expressApp.js。（需要先安装express：npm install --save express）。访问的还是80端口

3、接下来的操作跟使用方法1的2-6一样

### 正常版(通过express生成器)

正常情况下，是通过express生成器自动生成一个项目

先安装express命令生成器npm install -g express-generator

1、创建express项目。终端运行

```
express --view=ejs chatapp
```

2、进入项目目录，安装下

```
npm install
```

> 为了能看到客户端和服务器的全局内容，这儿我们换用VS Code：把包含客户端和服务器的目录拖到VS Code

3、打开www，在www里 实例化socket.io

> 它换成了在www中引用http、创建server——app
>
> 原先：是在app.js中创建app，再与io关联起来，再在app.js中去使用它们（的方法）
>
> 现在：不在app.js和www中直接使用它们，要新建个js来把io导出来，再导到www中，让别人可以拿到并且去使用它

1、新建个socketio.js

```js
let socketio = {}

function getSocket(server){	//1、把server传进来
	socketio.io = require('socket.io')(server);	//拿到io
}

socketio.getSocket = getSocket;

module.exports = socketio	//把它导出来
```

2、在www的创建server——app后面写

```
var socketio = require('../socketio')  //导进来
socketio.getSocket(server)
```

3、若在哪个地方用，就是这样用的：比如要在app.js中用，写在module.export = app; 之前。

```
let socketio = require('../socketio');
let io = socketio.io;
io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});
```

4、先查看下package.json中没有有socket.io，没有就安装下。

```
npm install --save socket.io 
```

5、注意：该项目的地址是3000或8080，所以你的客户端的io.connect里面的链接里要加个`:8080`。（客户端的做法跟之前的一样，这儿就不写了）

6、运行：npm start（运行失败就重新安装下，再不行就npm install）

如果还不行就在第3个做个小延时

```js
setTimeout(() =>{	//做个100ms的小延时，把3的代码放进来
	let socketio = require('../socketio');
    let io = socketio.io;
    io.on('connection', function (socket) {
      socket.emit('news', { hello: 'world' });
      socket.on('my other event', function (data) {
        console.log(data);
      });
    });
},100);
```

### 推荐版

只用在socketio.js中使用就好了。（没有必要在app.js里做，还要进行额外操作，把之前在app.js写的剪切出来修改下）

直接socketio.js中写入：

```
let socketio = {}

function getSocket(server){	//1、把server传进来
	socketio.io = require('socket.io')(server);	//拿到io
	
	let io = socketio.io;
	io.on('connection', function (socket) {
		socket.emit('news', { hello: 'world' });
		socket.on('my other event', function (data) {
		console.log(data);
		});
	});
	
}

socketio.getSocket = getSocket;

module.exports = socketio	
```

