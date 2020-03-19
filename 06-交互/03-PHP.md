在看该笔记前，要先看动态网页站开发基础

## 注意

- php学习笔记有的中间不用看，看最后总结
- 手册查找：在索引里找
- php代码与html代码 
  - php不会受html执行的影响。
  - 什么时候执行：PHP在服务器运行环境执行。html在浏览器执行。
  - php执行时只关心字符串。
- 但真正开发时，配环境：不会一个个装，而是直接用集成环境去装（将apche、php、mysql等全部装好）。而初学：不这样做，是因为容易把这些软件的职责搞乱
- 学习重心：如何去跟HTML混编。
- php所有能力都是函数，内置1000多个函数
- 适用工具：sublime写php很方便，如if后tab键，会直接出现指令式的代码段。要不知道有哪些代码端，ctrl+shift+p命令面板里输入Snippet:，列出的都是代码端、对应方式
  - sublime高效、没有太多提示类的东西、纯粹点

## 配置 PHP 支持 

大致过程：解压php->loadmodule->addtype

> 实验：尝试在网站中添加一个扩展名为 php 的文件，然后到浏览器中访问它。
>
> 实验结果：并没有显示我们想要的 Hello PHP ，而是将代码原封不动的返回给浏览器了。
>
> ```
> <!‐‐ demo.php ‐‐> 
> <?php echo 'Hello PHP'; ?>
> ```
>
> 原因很简单：Apache 只能处理静态文件请求，对于后缀名为 .php 这种动态文件，它无法执行，所以就当成是一 个静态文件直接返回了。

解决方法——配置PHP支持：

1. 下载PHP，在服务器（电脑）上安装 PHP 

   1. 解压 php 到纯英文路径目录中 （PHP是辅助工具，放这就好，剩下是Apache的事）

   > 你可以理解为：Apache 是一家没有太多能力的公司，只能处理一些简单的业务（静态网站），但是心很大想 做更多的事（动态网站），所以就想到了外包，所有额外的业务都需要外包给其他程序，而 PHP 就是理解为 一个专门能够处理 php 业务的外包公司

2. 在 Apache 中添加支持 PHP 的配置  

   1. 在 Apache 的配置文件httpd.conf，找到添加位置，添加 PHP 处理模块（如果目录有空格，给目录加“”）

      ```
      # php support LoadModule php7_module C:/Develop/php/php7apache2_4.dll
      ```

   2. 在 <IfModule mime_module> 节点中添加 .php 扩展名解析支持（因为PHP不根据后缀判断是否工作，是根据MIME Type工作：如text/html。在conf/mime.types中没有将这类型与扩展名关联，所以要加载）

      ```
      # parse .php files 
      AddType application/x‐httpd‐php .php
      ```

   3. 默认文档配置节点 <IfModule dir_module> 中添加 index.php

      ```
      <IfModule dir_module>     
      	DirectoryIndex index.html index.php </IfModule>
      ```

## 什么是PHP

- 嵌入在HTML中的脚本语言，适合做动态网页开发（因为：动态网站核心：界面上的内容可以变化）
- 松散的弱类型语言（如js，现在流行）
- PHP的价值：通过执行某些PHP代码**获取**到指定的数据（API），**填充**到HTML的指定位置（混编）。
- PHP就好像一个大号的模板引擎，只是比模板引擎较复杂
- PHP的工作核心：字符串拼接：**php标记以外的**代码原封不动地输出，**php标记以内的**根据执行得到结果（根据代码逻辑来控制）。

## PHP写在哪

跟html混编在一块。（最终执行时：**php标记以外的**代码原封不动地输出，**php标记以内的**就根据代码逻辑来控制。）所以，注意！不要在.php写注释

## PHP使用

### PHP 标记 

- <?php 可以让代码进入“PHP 模式" （进入标记）
- ?> 可以让代码退出“PHP 模式”（结束标记）

- 只有处于 PHP 标记内部的代码才是 PHP 代码，PHP 标记以外都原封不动。
- 注意PHP内部代码有；

```
<?php echo date('Y‐m‐d'); ?>
```

### 省略结束标记

原因：若在php结束标记后面打换行，虽然界面中不显示，但浏览器源代码中会出现换行

建议删除结束标记情况：

- PHP 代码段处于整个文件的末尾
- 这个文件只用php代码，没有混编情况

这样不会有额外的空行产生。

### 输出内容方式

- echo
  
  ```php+HTML
  <?php
  // 用途：只能打印字符串（打印布尔值会true——1，false——没有）
  // 注意：echo后面紧跟着一个空格;字符串一般用单引号括起，因为双引号功能强大导致效率低些。
  // 可以同时输出多个内容，用“，”隔开。输出结果会拼接起来
  echo 'hello php';
  ```
  
- print

  - 用法跟echo一样，但只能打印一个数据。

- var_dump

  ```php+HTML
  <?php 
  // 用途：可打印各种值，一般调试用。用于输出数据类型及数据、布尔值
  //	var_dump 是一个函数，必须跟上 () 调用
  // 可以将数据以及数据的类型打印为特定格式 
  var_dump('hello php'); 
  ```

```
还有一些输出函数（可以通过查手册自学，用到再说），例如： exit() / print_r() 等等
```

### 与HTML混编

普通嵌入

```php+HTML
<p><?php echo 'hello'; ?></p>
```

语句混编

```php+HTML
<?php if ($age >= 18) { ?> 	//js+{ 不容易看
	<p>成年人</p> 
<?php } else { ?>  
	<p>小朋友</p>
<?php } ?>
```

更常见的用法

```php+HTML
<?php if ($age > 18): ?>	//js+指令式代码  易看
	<p>成年人</p> 
<?php else: ?>   
	<p>小朋友</p> 
<?php endif ?>
```

注意：换行——要在html页面换行，要

```
echo ’<br>‘； //而不是echo ’\n‘；
```

### 注释

#、//	单行注释

/**/	多行注释

注意：不要在与HTML混编时写注释。

```php+HTML
<?php 
// 这是一条单行注释 
# 井号也可以做注释（不要用，有点生僻）
/*
多行注释
*/
$foo = 'hello';
```

## 语法

### 编程语言常见的语法（学习新语言的方法）

所有编程语言都可以这样学习，按顺序跟上一门旧语言对比，那不同重点看哪儿

- 变量 —— 用于临时存放数据的容器 

- 顺序结构 —— 先干什么再干什么 
- 分支结构 —— 如果怎样就怎样否则怎样 
- 循环结构 —— 不断的做某件相同的事 
- 函数 —— 提前设计好一件事怎么干，然后想什么时候干就什么时候干 
- 运算符 —— 数学运算和字符串拼接 
- 字面量 —— 在代码中用某些字符组成，能够表达一个具体的值 这些字符之间表示数据的方式叫做字面量

如php：跟js不同的地方——这些重点来学，其它跟js一样报错了再说

1. 变量 
2. 双引号字符串和单引号字符串的差异 
3. 指令式的语法 
4. foreach 

5. 函数作用域问题
6. 字符串拼接

### 变量

- 申明变量：$变量名

- 变量名同样是区分大小写的。

- 变量无需声明类型。

  ```php+HTML
  <?php 
  $foo; // 申明一个变量，变量名为 `foo`，未对其进行赋值 $bar = 'baz'; // 申明一个变量，将一个值为 `baz` 的字符串赋值给它 
  echo $foo; // 输出一个变量名为 `foo` 的变量 fn($bar); // 将一个变量名为 `foo` 的变量作为 `fn` 的实参传递
  ```

#### 数据类型

常见的 PHP 数据类型与 JavaScript 基本一致：	

- string（字符串）

- integer（整型）—— 只能存整数 
- ﬂoat（浮点型）—— 可以存带小数位的数字 
- boolean（布尔型） 
- array（数组） 
- object（对象） 
- NULL（空） 
- Resource（资源类型） 
- Callback / Callable（回调或者叫可调用类型）

##### 字符串

单引号字符串 (只对字符串有用，对函数参数没用相当于\)

​	不支持特殊的转义符号，例如 \n 

​	如果要表示一个单引号字符内容，可以通过 \' 表达 

​	如果要表示一个反斜线字符内容，可以通过 \\ 表达

双引号字符串（一般不使用，因为功能强导致效率低）
	支持转义符号 (只对字符串有用，对函数参数没用不相当于\)

​	支持变量解析

> 字符串函数
> http://php.net/manual/zh/ref.strings.php
>
>  http://www.w3school.com.cn/php/php_string.asp

数组 
PHP 中数组可以分为两类：
索引数组
	与 JavaScript 中的数组基本一致

```
<?php // 定义一个索引数组 $arr = array(1, 2, 3, 4, 5); 
var_dump($arr);   

// PHP 5.4 以后定义的方式可以用 `[]` $arr2 = [1, 2, 3, 4, 5]; 
var_dump($arr2);
```

关联数组
	有点类似于 JavaScript 中的对象

```
<?php // 注意：键只能是`integer`或者`string` $arr = array('key1' => 'value1', 'key2' => 'value2'); 
var_dump($arr);   

// PHP 5.4 以后定义的方式可以用 `[]` $arr2 = ['key1' => 'value1', 'key2' => 'value2']; var_dump($arr2);
```

#### 数据类型转换

> 参考：http://php.net/manual/zh/language.types.type-juggling.php

```
<?php 
$str = '132';
// 将一个内容为数字的字符串强制转换为一个整形的数字 $num = (int)$str; 
// 将一个数字强制转换为布尔值 
$flag = (bool)$num;
```

作业：

sublime ctrl+K、L转小写， ctrl+K、U转大写

## 关于API的定义

API（APP Application interface	应用程序编程接口）

接口都是提供某种特定能力的事物，特点：**有输入有输出**。而我们在开发时（写代码时）用到的接口称为API（应用程序）

2种接口：

​	1.我们用到的函数（方法）

​	2.web接口：如api.douban.com/v2/movie/top250

不用知道有多少API，要用时去查：知道函数作用是什么，它输入输出是什么就可以了。学任何语言把精力放在语法上去。

具体实例看笔记中的code

函数不用在前面写字符类型

​	php获取宽字符，除3或mb_系列函数，如mb_strlen，但它们不在内置函数中，在一个模块里面，所以前提要开启php扩展：模块成员必须通过配置文件载入模块过后再使用。

在php/ext中可以看到php_mbstring.dll这个扩展

但要开启：1.将php目录的php.ini-development复制一个修改为php.ini

​					2.修改php.ini中的extension_dir

​					3.在php.ini解开这个扩展的注释

​					4.默认apache加载的php.ini 是去Windows目录找的。可通过apache配置文件修改默认加载路径：

```
# 告诉APACHE php.ini所i在的路径
PHPIniDir d:/php
```

​					5.通知apache：重启apache

phpinfo函数可到浏览器查看接口是否配置、扩展是否进来（要有小标题）

## PHP中的REPL环境

php7才行

R E P L:读、执行、打印、循环

怎么样快速试验api？可直接执行php代码不用通过apache。（php里有php.exe，要用命令行去运行它：cd到该目录去运行、php -a进入REPL即可（末尾加；才能运行））

只有通过安装、删除、操作服务才用到管理员权限

isset和empty函数都会吞掉警告

false：0或字符串为空或字符串为0（会先转成数字对比）

js中有个include，判断字符串是否存在

Y——四位的年份，y——两位的年份

fopen、glob不常用

语法、超全局变量在具体应用中才能体现到它的意义

什么时候用常量：一般程序的配置信息（不会在运行过程中修改）都会在常量中定义

what why how where when

变量、函数命名规则

js:驼峰命名

php：小写下划线命名

php：常量大写下划线命名

## 载入文件（代码）：

​					CSS——import命令：@import url()

​					php——4种方式

require	载入之后就执行。若文件不存在，会提示错误,当前文件不再往下执行

require_once	载入之后只执行一次（载入配置文件时）。若文件不存在，会提示错误,当前文件不再往下执行

include	（载入html页面片段时）载入文件不存在不会报错（会有警告），当前文件会继续执行

include_once

> 警告的关闭：
>
> // 只有当 php.ini 中 display_errors = On 时候
> // 才会在界面上显示 notice 错误
> // 开发阶段一定设置为 On 生产阶段（上线）设置为 Off
>
> 如果想要写代码调用函数时忽略错误或者警告，可以在对应调用的API前加个@，但开发阶段需要有错误信息。

​		到Network可以看请求了多少文件

页面的公共地方：抽出来放到一个公共文件，再引用该文件



界面、功能（重要）。

## 表单处理：

一个网站除了使用数据，还有收集数据（就是用表单）

表单实例——基本的注册、登陆界面：

## 客户端表单提交注意事项：

（只关心了html）

1. 必须有form标签
2. form必须指定action、method。
   1. 不设置action默认是当前页面（有兼容性问题，必须设置）。
   2. 不设置method默认是get
   3. 表单元素（表单域input）必须有name（如果希望被提交的情况）
   4. 表单中必须有一个提交按钮（没有js前提下）

提交功能：input的type为submit的按钮、input的type为image的按钮、button（它默认类型为submit。用得更多，可控程度更高）

js中提交功能：通过获取form元素的dom对象，用dom对象的方法submit来提交

## 服务端接受提交参数：

### 注册表单状态保持

（只关心了php）

```php+HTML
var_dump($_GET);
// $_GET 用于接收 URL 地址中问号参数中的提交数据（一般是 GET 参数）
//取一个具体值？如var_dump($_GET['usr']);
var_dump($_POST);
// $_POST 用于接收 请求体 中提交的数据（一般是 POST 提交的数据）

var_dump($_REQUEST);
// $_REQUEST = $_GET + $_POST
```

```
//  服务端注册处理的整体目标：（前提——判断提交方式是否对应）
//	接收用户提交的数据，保存到文件
//	表单处理经典三步骤
//	1.校验（完整性、正确性）、接收（校验完先检测再接收）
//	2.持久化（将数据持久地保存下来——硬盘/文件/数据库）
//	3.响应（服务端的反馈）

//这几步完成后，就解决各种发现的问题来实现功能，具体看笔记中code
1.用户体验，表单处理用户名状态保持（放后处理）——注册表单状态保持。应对：添加默认值value、三元表达式value="<?php echo isset($_POST['username']) ? $_POST['username'] : ''; ?>
2.接收数据：应是追加式不是覆盖式（去查手册）
3.校验步骤的优化，代码else逻辑嵌套过深（放后处理）。嵌套原因：有else。应对：找个办法替代else的功能（如果是if停止执行后面的代码）。
	return？结束方法的执行。但我们这段代码整体不在一个函数内部，不能写，写了会跟exit()一样。（所以不介意在非函数内部使用）具体用途？拿include、require载入返回值用，但不介意用。		exit()？整个程序不再执行，不可以。
	既然没有函数能，那我们自定义个函数：在函数里面用return（条件一定要取非，才能写return）。测试完有错：申明（标识）message提示消息为全局变量global $message 或 超全局变量：将message换成$GLOBALS['message'],这样html仍使用$message也可以。具体看demo的register1.php
4.关于错误消息的显示位置：如echo ‘会不会玩’；
```



过程中，服务端会做哪些后续处理，如注册：存下来、登陆：检测。

注意：

​			1.任何在客户端的东西都不能信：如js的表单校验（检查的设置选项-Disable JavaScritpt）。能相信的只有服务端能否接收到，js只能做些界面的提升而已。所以有些人没学js也可以写网站

​			2.先有个开头，然后会发现再有无数问题，等你去慢慢解决后功能就出来了，问题在于怎么开头。开头不会？让人帮忙

​			3.写代码都有个语义化：让代码更容易被人理解

​			4.关于错误消息的显示位置：在html页面中（浏览器默认会用get的方式请求）来请求post的数据会报错，且只有错误时需要添加一对tr。怎么判断：用php与thml混编、isset是否定义 来判断来请求

5.注册成功也给个提示消息（暂时保留）

作业：在列表页添加表单的数据。（不把js和php混合到一起上）

## 表单提交地址问题

一般为了便于维护，我们将表单提交给当前页面本身

​		那接受提交数据，写在哪？

​		1.一般将表单处理逻辑放在html之前，为了更灵活的控制html的输出。（原因：登陆失败要给提示，若放在后面，html页面都执行完了你再执行这个逻辑代码就晚了：万一我们要做个错误提示，逻辑在前面提示就会在下方html中显示。在后面就不显示了）

2.因为对于表单的处理逻辑不是每次都需要执行，所以一般我们会判断请求方式决定是否执行对数据的处理

```
<?php 
if ($_SERVER['REQUEST_METHOD'] === 'POST') {   // 表单提交请求（这的超全局成员：拿到服务端相关信息）
  // 请求的方式是post，当前是点击按钮产生的请求
  var_dump($_POST);
} ?>
```

建议使用 $_SERVER['PHP_SELF'] 动态获取当前页面访问路径，这样就不用因为文件重命名或者网站目录结 构调整而修改代码了：

```php+HTML
<!‐‐ 通过 `$_SERVER['PHP_SELF']` 获取路径，可以轻松避免这个问题 ‐‐> 
<form action="<?php echo $_SERVER['PHP_SELF']; ?>">   <!‐‐ ... ‐‐> 
</form>
```

呈现错误信息：不用echo（只在php代码不会到html代码中）

> 鲁棒性：指的是我们的程序应对变化的能力

## 表单提交方式问题

1.请求的方式不同

2.传参方式不同，get：url传参，post：请求体传参

具体看表单处理.md  

## 常见表单元素处理

至于表单元素中的文本框文本域一类的元素，都是直接将元素的 name 属性值作为键，用户填写的信息作为值，发送到服务端。

注意：每一个input一定要给它配个label(label是为了解释说明input的作用，如对屏幕朗读软件。通过for属性来关联起来)。按钮一般不要给name，除非按钮有多个。只给需要输入操作的给label。

如果表单中有个文件域，表单的method必须为post（因为请求体可以传二进制的数据），表单的编码类型enctype必须为multipart/form-data。

但是表单元素中还有一些比较特殊的表单元素需要单独考虑：

### 单选按钮 radio

注意：每一个input一定要给它配个label(label是为了解释说明input的作用，如对屏幕朗读软件。通过for属性来关联起来)

```php+HTML
<!‐‐ 最终只会提交选中的那一项的 value ‐‐> <input type="radio" name="gender" value="male"> <input type="radio" name="gender" value="female">
<!‐‐ 以name为界，以value为值让服务端可以辨别。不然值默认都为on ‐‐>
```

### 复选按钮 checkbox

```php+HTML
<!‐‐必须要有name才会被提交 ‐‐>
<!‐‐没有设置value的 checkbox选中提交的 value 是 on ‐‐> 
<input type="checkbox" name="agree"> 
<!‐‐ 设置了 value 的 checkbox 选中提交的是 value 值 ‐‐> <input type="checkbox" name="agree" value="true">
```

如果需要同时提交多个选中项，可以在 name 属性后面 跟上 [] ：

```
<input type="checkbox" name="funs[]" id="" value="football"> <input type="checkbox" name="funs[]" id="" value="basketball"> <input type="checkbox" name="funs[]" id="" value="world peace">
```

最终提交到服务端，通过 $_POST 接收到的是一个索引数组。

###  选择框

```
<select name="subject">   
	<!‐‐ 设置 value 提交 value ‐‐>   
	<option value="1">语文</option>   
	<!‐‐ 没有设置 value 提交文本 innerText ‐‐>   
	<option>数学</option>
</select>
```

## 表单中的文件上传

先考虑功能层面上的东西，再去看案例（案列牵扯的比较多）

### 文件域的基本使用

如果表单中有文件域（文件上传），表单的method必须为post（因为请求体可以传二进制的数据），表单的编码类型enctype必须为multipart/form-data。（多部分的、多卷的）

查看请求体：谷歌浏览器中，Network右击请求的问题最下面view-type可看

#### 提交文件

想让文件域被提交，一定要加name

注意：input有个属性accept限制文件域可以选择哪种类型的文件，值是MIME Type或文件扩展名（能设多个，用，隔开），但只是提升了客户端友好性，php仍要设置校验

```
<input type="file" name="img">
```

#### 接收文件

```php
<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  // 接收文件 使用一个 叫做 $_FILES 超全局成员
  var_dump($_FILES);
}
?>
```



文件上传服务端处理逻辑（接收(处理)步骤），具体看code

```php+HTML
<?php
//	也会有个判断过程，又会出现else嵌套过深问题，所以也自定义个函数
// avatar 头像
function upload () {
  if (!isset($_FILES['avatar'])) {
    $GLOBALS['message'] = '别玩我了';
    // （若没定义）即客户端提交的表单内容中根本没有文件域
    // 条件一定要取非，才能写return
    return;
  }

  $avatar = $_FILES['avatar'];
  //$avatar指的是一个关联数组
  // $avatar => array(5) {
  //   ["name"]=>
  //   string(11) "icon-02.png"
  //   ["type"]=>
  //   string(9) "image/png"
  //   ["tmp_name"]=>
  //   string(27) "C:\Windows\Temp\php1138.tmp"
  //   ["error"]=>
  //   int(0)
  //   ["size"]=>
  //   int(4398)
  // }
  //echo $avatar['error']; 检测文件错误码
  if ($avatar['error'] !== UPLOAD_ERR_OK) {
    // （上传失败）服务端没有接收到上传的文件
    //本来是写if ($avatar['error'] !== 0) ，但php为了语义化，用个常量去代表这个0，去php手册查看
    $GLOBALS['message'] = '上传失败';
    return;
  }

  // 接收到了文件
  // 将文件从临时目录移动到网站范围之内（网站根目录以内）
  $source = $avatar['tmp_name']; // 源文件在哪
  // => 'C:\Windows\Temp\php1138.tmp'
  $target = './uploads/' . $avatar['name']; // 目标放在哪，目标原名
  // => './uploads/icon-02.png'
  // 移动的目标路径中文件夹一定是一个已经存在的目录，不然报错。如果不存在，make一下这个dir
  $moved = move_uploaded_file($source, $target);

  if (!$moved) {
    $GLOBALS['message'] = '上传失败';
    return;
  }

  // 移动成功（上传整个过程OK）
  //echo ’123‘； 检测
}

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  // 接收文件 使用一个 叫做 $_FILES 超全局成员
  // var_dump($_FILES);
  upload();
}

?>
```

注意：

1.单个文件上传清空：

​	若有用户上传同名文件，一般将上传文件重命名：

```
  // 一般情况会将上传的文件重命名
  $target = './uploads/' . uniqid() . '-' . $source['name'];
  if (!move_uploaded_file($source['tmp_name'], $target)) {
    $GLOBALS['error_message'] = '上传音乐失败';
    return;
  }
```

如果不想要原名在内，自己百度（与php随机数有关）

2.多个文件上传

校验文件数量、文件种类

种类后处理，是因为写代码的原则：先处理简单的业务，再处理复杂的业务。

注意：input有个属性accept限制文件域可以选择哪种类型的文件，值是MIME Type，但只是提升了客户端友好性，php仍要设置校验

```
  // 判断用户是否选择了文件
  if ($source['error'] !== UPLOAD_ERR_OK) {
    $GLOBALS['error_message'] = '请选择音乐文件';
    return;
  }

  // 校验文件的大小
  //代码放在这个位置。
  // 校验文件的大小
  //字节跟M单位换算，这样写方便别人去看
  if ($source['size'] > 10 * 1024 * 1024) {
    $GLOBALS['error_message'] = '音乐文件过大';
    return;
  }

  if ($source['size'] < 1 * 1024 * 1024) {
    $GLOBALS['error_message'] = '音乐文件过小';
    return;
  }

  // 校验类型
  $allowed_types = array('audio/mp3', 'audio/wma');
  if (!in_array($source['type'], $allowed_types)) {
    $GLOBALS['error_message'] = '这是不支持的音乐格式';
    return;
  }
```



### 文件上传大小限制问题

错误码为1。

```
详细的错误码说明：http://php.net/manual/zh/features.file‐upload.errors.php 
http://php.net/manual/zh/features.ﬁle-upload.php
注意：
	修改 php.ini 中的 upload_max_filesize 配置，让服务端支持更大的单个上传文件。一般不设太大，防止别人恶意上传超大文件导致服务器内存不足崩溃，参考：设20M
	修改 php.ini 中的 post_max_size 配置，让服务端可以接受更大的请求体体积，参考：设80M
```

作业：音乐列表案例看表单处理pdf、登陆

# 音乐列表案例

学习目的：表单处理流程、动态网站开发核心：把数据拿出来渲染到页面上。

第一件事：考虑数据怎么存怎么取？

## 数据表述手段、存储数据格式的手段(JSON)

除了这些呢，就是我们专门用来存取数据的地方：数据库，比我们用这种普通文件存储的方式要更加简单，功能更加简单。

如json：想找某歌手的所有音乐，找数据：要遍历一下，然后挨个判断歌手名是否=该歌手

而数据库都有这种功能，让我们更容易做到这些事情。

其实数据库是一种数据存储的手段，只不过为了便于我们对数据的操作做了很多功能。

1.**字面量：代码中表述数据的手段**

```
var obj = {
	name: 123,
	age: 456
}

//数组字面量
[
	{ id: 1, name: '朱芳' },
	{ id: 1, name: '朱芳' },	
]
```



2.**JSON：是一种类似于js的字面量的手段，也是表述数据的手段，现如今用得最多的数据格式。**原因：解析容易，直接能把json字符串转换成对象或者说数组

```
[
	{   
		"name": "zce",   
		"age": 18,   
		"gender": true,   			           "girl_friend": null 
	},
	{   
		"name": "zce",   
		"age": 18,   
		"gender": true,   			           "girl_friend": null 
	}
]
```

3.json中	**属性名称**必须用**双引号**包裹

​				**字符串**必须用**双引号**包裹 

​				不允许使用注释

4.如何解析服务器上传的json字符串中的数据(为了描述方便，这里把该数据给str)？

js中ES5提供了一个json对象：JSON.parse(str)得到一个数组，把json字符串转化为数据；用arr接受这些数据；把数据转成一个json字符串：JSON.stringIfy(arr)转换成 字符串 风格的，来得到转换成json格式的字符串。



1.数据怎么存怎么取？用json来存取（storage.json，里面有1个数组，数组里有4个对象，每个对象分别有5个属性）
2.把已有数据快速用页面呈现出来。静态页面（list.html、add.html）
3.动态php文件（list.php）。把数据呈现到已有页面上。

- 已有页面：把list.html粘过来，注意依赖文件，如.css，再测试下页面能否正常显示。

- 数据：把表格里的数据换成我们从文件中读出来的数据：在页头加入php脚本去读取文件（不放下面原因：先获取数据再渲染数据，若先渲染就没意义了）。

  ​	具体步骤：1.获取文件中记录的数据，并展示到表格中（展示层面：是浏览器通过执行html去完成的。所以这儿php代码目的——为了动态生成表格的HTML标签）

  ​			1.1把已有数据做程序：当用户请求过来，我们读一下json文件，把json文件的数据解析出去，呈现到界面上。（问题：php中怎么样解析json？）。

  php中怎么样解析json:

```
<?php
//php中怎么样解析json
//1.读文件
$contents = file_get_contents('storage.json');
// $contents => JSON 格式的字符串
// 2.把 JSON 格式的字符串转换为对象(数组)        的过程叫做反序列化
$data = json_decode($contents, true);//打印检测发现返回的是对象。原因：json_decode默认反序列化是将json中的对象转换为PHP中stdClass类型的对象。应对：加true这个参数让使用关联数组的方式返回数据
//var_dump($arr); //先打印测试下，是否正确
// $data => []。既然是个数组，那我们就对它进行遍历，在哪遍历？每遍历数组当中一个元素，就生成表格里的一个tr标签，所以在tr标签外面遍历。
?>

html中：
<tbody class="text-center">
		//2.2应该遍历的是什么？$data,索引数组，不需关心键，关心值就行了as $item
        <?php foreach ($data as $item): ?>
        <tr>
          //2.3 每一个item就是我们正在遍历的那一项。获取项里的值。会报错：报错时不要先切回代码去，先去过遍错误信息。错误：$item不是关联数组。原因：json_decode把json中的对象转换成stdClass的对象。应对：给该API添加第二个参数：true 或用对象语法$item->title（不建议，用传统语法关联数组语法就好）
          <td><?php echo $item['title'] ?></td>
          <td><?php echo $item['artist'] ?></td>
          <td><img src="<?php echo $item['images'][0] ?>" alt=""></td>
          <td><audio src="<?php echo $item['source'] ?>" controls></audio></td>
          <td><button class="btn btn-danger btn-sm">删除</button></td>
        </tr>
        <?php endforeach ?>
</tbody>
```

1.2添加（add.php）。

​	客户端：首先有个添加的页面：把静态页面代码粘贴过来。

​    处理表单属性（再测试下，打开页面检查的Network，点页面的提交，查看请求：移到最下面看请求体）

​    服务端:在页头写php添加代码。想一下：新增的流程：

​	重心：提交、接收处理,具体看code

```
<?php

/**
 * 只是在表单提交时执行
 */
function add_music () {
  // 目标
  //  将用户提交过来的数据保存到 storage.json 中
  // 步骤
  //  1. 接收并 校验（最麻烦的就是校验。有多少name判断多少次，但文件上传单独考虑）
  //  2. 持久化（一句代码就可完成）
  //  3. 响应
  
  //	校验文本框
  ......
  //	校验上传文件（注意：若有用户上传同名文件，一般将上传文件重命名）
  ......
  //	
}

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  add_music();
}
```

注意：

1.单个文件上传清空：

​	若有用户上传同名文件，一般将上传文件重命名：

```
  // 一般情况会将上传的文件重命名
  $target = './uploads/' . uniqid() . '-' . $source['name'];
  if (!move_uploaded_file($source['tmp_name'], $target)) {
    $GLOBALS['error_message'] = '上传音乐失败';
    return;
  }
```

如果不想要原名在内，自己百度（与php随机数有关）

2.多个文件上传

校验文件数量、文件种类

种类后处理，是因为写代码的原则：先处理简单的业务，再处理复杂的业务。

注意：input有个属性accept限制文件域可以选择哪种类型的文件，值是MIME Type或文件扩展名（能设多个，用，隔开），但只是提升了客户端友好性，php仍要设置校验

```
  // 判断用户是否选择了文件
  if ($source['error'] !== UPLOAD_ERR_OK) {
    $GLOBALS['error_message'] = '请选择音乐文件';
    return;
  }

  // 校验文件的大小
  //代码放在这个位置。
  // 校验文件的大小
  //字节跟M单位换算，这样写方便别人去看
  if ($source['size'] > 10 * 1024 * 1024) {
    $GLOBALS['error_message'] = '音乐文件过大';
    return;
  }

  if ($source['size'] < 1 * 1024 * 1024) {
    $GLOBALS['error_message'] = '音乐文件过小';
    return;
  }

  // 校验类型
  $allowed_types = array('audio/mp3', 'audio/wma');
  if (!in_array($source['type'], $allowed_types)) {
    $GLOBALS['error_message'] = '这是不支持的音乐格式';
    return;
  }
```

还有多选文件问题、删除问题。

3.多选文件问题：具体看songs的add.php

如何接收单个文件域的多文件上传

客户端上，提升界面友好性：input还有个属性：mutiple。可以让一个文件域多选

服务端：在input的name值里多加个[]，再添加校验PHP代码。具体看songs

```
// 2. 接收图片文件
  // 如何接收单个文件域的多文件上传？？？
  if (empty($_FILES['images'])) {
    $GLOBALS['error_message'] = '请正常使用表单';
    return;
  }
$images = $_FILES['images']; 
  // 准备一个容器装所有的海报路径
  $data['images'] = array();
  
  //之前每个成员类型都是字符串，现在都是索引数组。就看用for、foreach哪个合适，这里用for好。原因：取每个成员的某个值都要用到下标
  // 遍历这个文件域中的每一个文件（判断是否成功、判断类型、判断大小、移动到网站目录中）
  for ($i = 0; $i < count($images['name']); $i++) {
    // $images['error'] => [0, 0, 0]
    if ($images['error'][$i] !== UPLOAD_ERR_OK) {
      $GLOBALS['error_message'] = '上传海报文件失败1';
      return;
    }
// 类型的校验
    // $images['type'] => ['image/png', 'image/jpg', 'image/gif']
    if (strpos($images['type'][$i], 'image/') !== 0) {
      $GLOBALS['error_message'] = '上传海报文件格式错误';
      return;
    }

    // TODO: 文件大小的判断
    if ($images['size'][$i] > 1 * 1024 * 1024) {
      $GLOBALS['error_message'] = '上传海报文件过大';
      return;
    }

    // 移动文件到网站范围之内
    $dest = '../uploads/' . uniqid() . $images['name'][$i];
    if (!move_uploaded_file($images['tmp_name'][$i], $dest)) {
      $GLOBALS['error_message'] = '上传海报文件失败2';
      return;
    }

    $data['images'][] = substr($dest, 2);
  }
```

## 保存数据逻辑

追加不了。就读出来添加再覆盖。

json不在意换行。汉字传进去unicode字符，不用关心

关于上传文件路径有坑：相对还是绝对。

添加完跳转回列表页：  header('Location: list.php');



如遇到问题：

php代码段tab不出来？

开发工具的代码段工作不工作取决于当前的语言模式是什么（如黏贴过html就会变成html。）应对：CTRL+SHIFT+P 可通过set Syntax:PHP(或输入set ph切换语言模式)

session(HTTP会话、Cookie)