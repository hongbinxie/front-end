## 回顾：请求响应过程（web工作流程）

了解整个WEB是怎样运转的？从浏览器输入一个地址发起对网站的请求整个过程发生了什么？

> 注意：服务端不是返回文件，而是返回执行后的结果

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/%E8%AF%B7%E6%B1%82%E5%93%8D%E5%BA%94%E7%9A%84%E8%BF%87%E7%A8%8B.png)

1. 用户打开**浏览器**

2. 地址栏输入我们需要访问的网站**网址**（URL） 

3. 浏览器通过 DNS 服务器获取即将访问的网站 IP **地址** 

4. 浏览器发起一个对这个 IP 的**请求**

5. 服务端接收到这个请求，进行相应的**处理** 

6. 服务端将处理完的**结果**返回给客户端浏览器（间接）

7. 浏览器将服务端返回的结果**呈现到界面上**

  > 注意：这是静态文件的过程，看下面

   ![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/IP%E5%9C%B0%E5%9D%801.png)

比一般请求响应过程多的阶段——判断机制：是否为静（动）态文件。（注意：找其它程序按一定规律执行代码，如PHP）

> 实现服务端动态网页的技术有很多种：JSP、ASP.NET、PHP、Node 等等。

## HTTP简介

HTTP协议：HyperText Transfer Protocol，用于从万维网（WWW:World Wide Web ）服务器传输超文本到本地浏览器的超文本（网络）传输协议

基于TCP/IP通信协议来传递数据（HTML 文件, 图片文件, 查询结果等）。

## HTTP 工作原理

工作于客户端-服务端架构上。HTTP客户端（浏览器）通过URL（统一资源标识符）向HTTP服务端（WEB服务器）发送所有请求。

Web服务器有：Apache服务器，IIS服务器（Internet Information Services）等。

Web服务器根据接收到的请求后，向客户端发送响应信息。

HTTP默认端口号为80，但是你也可以改为8080或者其他端口。

**HTTP三点注意事项：**

- 无连接：限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。来节省传输时间。
- 媒体独立：这意味着，只要客户端和服务器知道如何处理的数据内容，任何类型的数据都可以通过HTTP发送。客户端以及服务器指定使用适合的MIME-type内容类型。
- 无状态协议：无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。

CGI(Common Gateway Interface) 是 HTTP 服务器与你的或其它机器上的程序进行“交谈”的一种工具，其程序须运行在网络服务器上。使网页具有交互功能。

## 客户端请求消息

客户端发送一个HTTP请求到服务器的请求消息包括以下格式：请求行（request line）、请求头部（header）、空行和请求数据四个部分组成，下图给出了请求报文的一般格式。

## 服务器响应消息

HTTP响应也由四个部分组成，分别是：状态行、消息报头、空行和响应正文。

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/%E8%AF%B7%E6%B1%82%E6%8A%A5%E6%96%87%E7%9A%84%E4%B8%80%E8%88%AC%E6%A0%BC%E5%BC%8F.png)

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%93%8D%E5%BA%94%E6%B6%88%E6%81%AF.jpg)

### 用GET来传递数据的实例

<https://www.runoob.com/http/http-messages.html>

# HTTP 请求方法

3+6种请求方法： GET, POST 和 HEAD、OPTIONS、PUT、PATCH、DELETE、TRACE 和 CONNECT 方法。

<https://www.runoob.com/http/http-methods.html>

# HTTP 响应头信息

<https://www.runoob.com/http/http-header-fields.html>

# HTTP状态码

当浏览者访问一个网页时，浏览者的浏览器会向网页所在服务器发出请求。当浏览器接收并显示网页前，此网页所在的服务器会返回一个包含HTTP状态码的信息头（server header）用以响应浏览器的请求。

HTTP状态码的英文为HTTP Status Code。

下面是常见的HTTP状态码：

- 200 - 请求成功
- 301 - 资源（网页等）被永久转移到其它URL
- 404 - 请求的资源（网页等）不存在
- 500 - 内部服务器错误

## HTTP状态码分类

HTTP状态码由三个十进制数字组成，第一个十进制数字定义了状态码的类型，后两个数字没有分类的作用。HTTP状态码共分为5种类型：

<https://www.runoob.com/http/http-status-codes.html>

# HTTP content-type

定义网络文件的类型和网页的编码，决定浏览器将以什么形式、什么编码读取这个文件，这就是经常看到一些 PHP 网页点击的结果却是下载一个文件或一张图片的原因。

Content-Type 标头告诉客户端实际返回的内容的内容类型。

语法格式：

```
Content-Type: text/html; charset=utf-8
Content-Type: multipart/form-data; boundary=something
```

实例：<https://www.runoob.com/http/http-content-type.html>

