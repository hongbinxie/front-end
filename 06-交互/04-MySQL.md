## 主要目的

学习数据库怎么安装、怎么使用、怎么通过代码的方式去操作它。

## 什么是数据库

数据库是一种数据存储的手段，只不过为了便于我们对数据的操作做了很多功能。

数据库就是数据的仓库，用来按照特定的结构去组织和管理我们的数据，有了数据库我们就可以更加方便、便捷的 操作（C / R / U / D）我们需要保存的数据。

**数据库查询**：指的是操作数据库的过程（增、删、改、查）

**数据库查询语言**：SQL（结构化查询语言）。基本查询语句、常用查询函数如果忘了去看pdf

分页查询数据的子语句：limit <skip>,<length>

​										（有个公式skip=（page-1）*size）

select * from users limit 2；//限制取几条

select * from users limit <skip>,<length>；//越过多少条取几条

## 安装与配置 MySQL

- 在开发领域，存储数据一般用**专门的数据库服务器专门提供的数据库服务**。
- 如果需要**让自己的机器也可以 提供数据库服务**，那么就需要安装特定的数据库服务器软件，这种类型的软件也有很多：Oracle、MySQL、SQL Server

解压版安装过程：

1. 解压到纯英文路径 

2. 解压目录添加 my.ini （可选，先不添加）

   参考：
   http://www.cnblogs.com/Ray-xujianguo/p/3322455.html

   https://gist.github.com/hanjong/1205199

   https://dev.mysql.com/doc/refman/5.5/en/mysqld-option-tables.html

```cmd
[mysqld] 
# MySQL 安装目录 
basedir=C:/Develop/mysql 
# 数据文件所在目录 datadir=C:/Develop/mysql/data
```

3. 以管理员身份运行 CMD 执行以下命令，**安装MySQL 服务**

```cmd
# 定位到安装目录下的 bin 文件夹 （因为安装服务的工具在里面）
$ cd <MySQL安装目录>/bin 
# 初始化 数据所需文件以及获取一个临时的访问密码，把它复制保存下来，不然要重新安装。要手打，复印会错
#若重新执行命令，会报错，因为mysal/data里的文件已经存在。不让初始化原因：考虑到可能有些重要的商业数据
$ mysqld ‐‐initialize ‐‐user=mysql ‐‐console 
# 将 MySQL 安装为服务 可以指定服务名称（可不写，会有个默认服务名） 。安装成功后，可到服务面板查看是否有MySQL服务，建议将启动方式设成手动启动。
$ mysqld ‐‐install MySQL
```

4. 登入 MySQL 服务器，重置密码

```cmd
# 先通过用户名密码进入 MySQL 操作环境 
$ mysql ‐u root ‐p 
Enter password: # 输入临时密码   
# 设置数据库访问密码，一定要加分号 mysql> set password for root@localhost = password('123');
# 输入exit;可退出，再登陆一遍测试数据库可登陆，再输入show databases;确保数据库成功。
```

启动服务，可以通过服务面板启动 或命令行（net不管当前目录在哪都可执行，可启动、停止系统上任何一个服务）中输入**net start MySQL**。每次启动完要记得登陆MySQL：$ mysql ‐u root ‐p。

mysql>show databases; 可以查看内置的数据库。

解压版卸载过程：服务卸载、文件删除即可。

​	先到服务面板停止服务，再到命令行（sc不管当前目录在哪都可执行，可删除系统上任何一个服务）卸载服务：**sc delete MySQL**。（服务名称，不是服务面板的显示名称，而要双击显示名称才能看到服务名称）。把解压文件删除掉就好。

# 数据库管理工具：

以后可视化工具会很少使用，所以要熟悉命令行去操作

## MySQL 的 REPL 环境对数据库的基本操作

R E P L：输入、执行、打印、循环

一般如果只是简单操作数据库，推荐使用 MySQL 内置的命令行工具完成：
通过命令行运行解压目录下 bin 目录中的 mysql.exe ：

```cmd
# 定位到 bin 目录
$ cd <解压目录>/bin 
# 运行 mysql，‐u 指定数据库用户名，‐p 指定密码 
$ mysql ‐u root ‐p wanglei 
# 一般不建议在命令中填写密码，因为这样会暴露你的密码，一般只加一个 ‐p 但是不给值 
$ mysql ‐u root ‐p 
Enter password: # 这时会要求你输入密码
```

进入 MySQL 客户端的 REPL 环境过后，可以通过标准的 SQL 语句操作数据库。

常见的操作指令

```cmd
mysql> show databases;  ‐‐ 显示全部数据库 
mysql> create database <db‐name>;  ‐‐ 创建一个指定名称的数据库 mysql> use <db‐name>;  ‐‐ 使用一个数据库，相当于进入指定的数据库 mysql> show tables;  ‐‐ 显示当前数据库中有哪些表 mysql> create table <table‐name> (id int, name varchar(20), age int);  ‐‐ 创建一个指定名称的数据 表，并添加 3 个列 
mysql> desc <table‐name>;  ‐‐ 查看指定表结构 mysql> source ./path/to/sql‐file.sql  ‐‐ 执行本地 SQL 文件中的 SQL 语句 
mysql> drop table <table‐name>;  ‐‐ 删除（放弃）一个指定名称的数据表 mysql> drop database <db‐name>;  ‐‐ 删除（放弃）一个指定名称的数据库 mysql> exit|quit;  ‐‐ 退出数据库终端
```

drop少用，不可逆的操作。除了有些数据库管理软件提供的策略：每天晚上12点定期把数据库备份到另一个软件上面，如果你有需求了可以回滚到之前备份的状态

## 可视化工具

如果需要复杂的操作，推荐 Navicat Premium(付费)、SQLyog

注意默认字符集及排序规则：utf8、gbk支持中文、排序规则按常规的（general）。默认为拉丁文的。怎样统一设置？

​	在新建/编辑数据库、常规中设置字符集、排序规则。建议为没有汉字的表设不同的字符集

​	或改下MySQL服务的默认字符集：在mysql目录下新建配置文件my.ini（要么只用sublime或记事本编辑，切记不能切换着用，编码类型会变），也可到mysql官方文档看配置：

```
[mysqld] 
# 设置默认字符集,只会影响新建数据库的默认字符集
character-set-server=uft8
```

### 导入数据库

将导出的.sql中的代码复制黏贴到 数据库新建查询 上 执行，然后刷新出现即可。

# 数据库查询语言：SQL

1. SQL（结构化查询语言）。

2. 基本查询语句、常用查询函数如果忘了去看pdf

3. 分页查询数据的子语句：limit <skip>,<length>

​										（有个公式skip=（page-1）*size）

select * from users limit 2；//限制取几条

select * from users limit <skip>,<length>；//越过多少条取几条

# 通过代码执行SQL语句来操作数据库

1.大体流程：



2.如何在 PHP 代码中操作数据库是我们能否在自己的程序中使用数据库的核心。

```
数据库扩展：http://php.net/manual/zh/refs.database.php
```

如果需要使用 MySQLi 扩展，需要在 php.ini 文件中打开这个扩展（解除注释）

配置完扩展之后，可以用phpinfo();看下配置扩展有没成功（ctrl+F查找下有没存在mysqil的二级标题，有即成功）

3.代码：前提——开启MySQLi 扩展，才能使用该扩展提供的函数

版本1：只是看一下逻辑，不是最终版本

```
<?php

// 能通过PHP代码执行一个SQL语句得到查询的结果

// 1. 建立与数据库服务器之间的连接。连别人数据库也是知道对方的ip、用户名、密码、数据库名，让对方开启数据库访问权限即可
//为啥用该API？之前的mysql_connect已被淘汰，这里的i表示提高版
//建立连接就涉及到一个问题——指定哪个。参数：IP、用户名、密码、数据库名
//写完这句代码就可以到浏览器看下有没报错，没报错就没问题。
//用变量来接收，表示一个“桥”，装着web服务器与数据库服务器的连接
$connection = mysqli_connect('127.0.0.1', 'root', '123456', 'demo2');

//判断一下这个桥能否正常打通,不报错即可。
//var_dump($connection);
if (!$connection) {
  // 连接数据库失败提示
  exit('<h1>连接数据库失败</h1>');
}

//建立完连接后，进行查询（增删改查）——mysqli_query（基于哪个连接去查询，查询语句（但建议先在数据库查询窗口试好，再回到代码这执行））
$query = mysqli_query($connection, 'select * from users;');

// 基于刚刚创建的连接对象执行一次查询操作，这儿进行查询数据的呈现。但第一次测试，发现呈现的不是想要的数据。
//因为得到的$query是一个查询对象，这个查询对象可以用来再到数据一行一行拿数据
//var_dump($query);
//再以关联数组的方式 取一行 数据mysqli_fetch_assoc($query)
//$row = mysqli_fetch_assoc($query);
//var_dump($row);

//最终结果：循环去呈现查询结果的每行数据
while ($row = mysqli_fetch_assoc($query)) {
  var_dump($row);
}
```

版本2：由于1不够严谨

查部分：

```
<?php

// 查询数据的查询语句

// 1. 建立与数据库服务器之间的连接
$connection = mysqli_connect('127.0.0.1', 'root', '123456', 'demo2');

// 1. 必须在查询数据之前
// 2. 必须传入连接对象和编码
//mysqli_set_charset($connection, 'utf8');
// mysqli_query($connection, 'set names utf8;');

if (!$connection) {
  // 连接数据库失败
  exit('<h1>连接数据库失败</h1>');
}

// 基于刚刚创建的连接对象执行一次查询操作
$query = mysqli_query($connection, 'select * from users;');

if (!$query) {
  exit('<h1>查询失败</h1>');
}

// 遍历结果集
while ($row = mysqli_fetch_assoc($query)) {
  var_dump($row);
}

// 释放查询结果集
mysqli_free_result($query);

// 炸桥 关闭连接。原因：释放占用
mysqli_close($connection);

```

> PHP查询中文数据的编码问题：通过mysqli_set_charset(连接对象，编码类型)，必须要在查询数据之前设置，必须传入连接对象和编码。或mysqli_query($connection, 'set names utf8;')。第一种常用

增删改部分：

```
<?php

// 增删改数据的查询语句

// 1. 建立与数据库服务器之间的连接
$connection = mysqli_connect('127.0.0.1', 'root', '123456', 'demo2');

if (!$connection) {
  // 连接数据库失败
  exit('<h1>连接数据库失败</h1>');
}

// 基于刚刚创建的连接对象执行一次查询操作
$query = mysqli_query($connection, 'delete from users where id = 5;');

if (!$query) {
  exit('<h1>查询失败</h1>');
}

// 如何拿到受影响行——mysqli_affected_rows($connection)
// 注意：传入的一定是连接对象，而不是查询对象。因为该API返回的是这个连接对象上一次查询受影响的行数
$rows = mysqli_affected_rows($connection);

var_dump($rows);


// 炸桥 关闭连接
mysqli_close($connection);

```

作业：将音乐列表的json文件换成个数据库。

## 基于数据库增删改查实例

具体看code

这儿静态页面已经有了（列表页、添加/编辑页（2者区别：有没默认值））

1.页面拿过来先分析：数据库设计——看下数据库要存什么信息（设计表、设计表里的字段）？

通过界面能得到这些信息，不够回头再来数据库加。表结构添加完，加（改）数据：（通过语句去加或可视化界面加，语句加更方便。原因：insert语句多执行几次数据就多了，不用像后者一行行加）

### （列表）查功能

概括：先通过数据库连接查询出来我们要的数据，查询出来后在html代码中遍历出来即可。

2.现在有静态页面也有数据源了。看列表功能怎么去做。把静态页面写活（动态渲染把代码黏贴到.php，改下css路径。把html代码中需要动态生成的写死的地方给它动态生成：）

把html代码中需要动态生成的写死的地方给它动态生成：

（1）前提：获取已有数据——1.建立连接2.开始查询3.遍历结果集

以前是读文件的方式把数据拿出来，现在是通过读数据库的方式拿数据。现在看起来复杂：代码中要查询、数据库也要查询，之后我们会学怎么封装这些步骤成一个公共函数，调用起来就非常方便了。

```
<?php

// 1. 建立连接
$conn = mysqli_connect('localhost', 'root', '123456', 'test');

if (!$conn) {
  exit('<h1>连接数据库失败</h1>');
}

// 2. 开始查询
$query = mysqli_query($conn, 'select * from users;');

if (!$query) {
  exit('<h1>查询数据失败</h1>');
}

// 3. 遍历结果集。装满了我们之前所查到的数据，再到html代码中遍历一下，但这是闲得蛋疼：循环一下把它装在数组里面（这儿没必要），再到html代码中循环一下这个数组
// while ($item = mysqli_fetch_assoc($query)) {
	 //先测试
	 //var_dump($item);
	 //想办法把数据装起来
//   $data[] = $item;
// }

?>
```

有了数据之后，就把要改的写死的代码删掉，然后写php遍历代码：

```
<tbody>
        <?php while ($item = mysqli_fetch_assoc($query)): ?>
        <tr>
          <th scope="row"><?php echo $item['id'] ?></th>
          <td><img src="<?php echo $item['avatar']; ?>" class="rounded" alt="<?php echo $item['name']; ?>"></td>
          <td><?php echo $item['name']; ?></td>
          <td><?php echo $item['gender'] == 0 ? '♀' : '♂'; ?></td>
          //注意这儿拿当前时间做个减法
          <td><?php echo $item['birthday']; ?></td>
          <td class="text-center">
            <a class="btn btn-info btn-sm" href="edit.php">编辑</a>
            <button class="btn btn-danger btn-sm">删除</button>
          </td>
        </tr>
        <?php endwhile ?>
      </tbody>
```

### 删功能 及批量删除思路

概括：当我们点击删除按钮时，把对应的当前数据删掉（不可能只是在客户端界面上把当前数据删掉，而是发一个请求到服务端，告诉服务端我们要删掉id为几的这条数据）

具体做法:给删除 一个a链接，让a链接点击时发送一次请求，跟服务端产生一次交互。

注意：要获取一下通过？参数传过来的要删数据的id（因为？的方式可以告诉服务端我们这想删什么）

```
<a class="btn btn-danger btn-sm" href="delete.php?id=<?php echo $item['id'] ?>">删除</a>
```

delete.php中代码：

套路跟之前一样，只是语句不太一样：从查语句变成删语句。但html中要先获取一下通过？参数传过来的要删数据的id（因为？的方式可以告诉服务端我们这想删什么），再delete.php中通过代码接收参数

```
<?php

// 接收要删除的数据 ID
if (empty($_GET['id'])) {
  exit('<h1>必须传入指定参数</h1>');
}
//继续往下走，意味着传了id，我们把id接收下来
$id = $_GET['id']; // => 1,2,3

// 1. 建立连接
$conn = mysqli_connect('localhost', 'root', '123456', 'test');

if (!$conn) {
  exit('<h1>连接数据库失败</h1>');
}

// 2. 开始查询
//如SQL语句delete from users where id in (1,2,3)一样，把id = ' . $id . ';')改成id in (' . $id . ');')，再在网址上输入delete.php?id=1,2,3就批量删除了。原因：上面的$id接收到的就不再是单个数字，而是1,2,3这样格式的数据，就完成了批量删除的功能
$query = mysqli_query($conn, 'delete from users where id in (' . $id . ');');

if (!$query) {
  exit('<h1>查询数据失败</h1>');
}
//获取受影响行数，以后可不写，这只是为了锻炼调用API能力
$affected_rows = mysqli_affected_rows($conn);
//这儿用<=判断，而非>判断。因为我们之后要做个批量删除功能：批量删除那这就也不>0了
if ($affected_rows <= 0) {
  exit('<h1>删除失败</h1>');
}
//跳转回去
header('Location: index.php');
```

批量删除思路：checkbox选择/不选择时，删除按钮（有a链接，怎么看出来：底下地址栏有个链接地址显示、地址？后有参数）的显示/隐藏。涉及到一些js功能，PHP与js混在一起情况（js：处理界面上的东西php：处理服务端的逻辑）、js全选不全选功能。自己去做

### 增（/添加）功能

静态页面->动态页面.php（改添加链接、表单添加form属性、给每个input加name、label、给laber加for、option加value）。如

```
		  <option value="-1">请选择性别</option>
          <option value="1">男</option>
          <option value="0">女</option>
```

给表单测试下能否正常提交再去处理功能：看Network、点add.php看下Request Payload请求体的name及值是不是都有了

```
<form action="<?php echo $_SERVER['PHP_SELF']; ?>" method="post" enctype="multipart/form-data" autocomplete="off">bootstrap的自动完成也关掉，实际项目时打开，测试时关掉影响操作
```

写一段php脚本（在当前页面被post请求时去处理些对应的逻辑：处理方式、自定义函数优化else嵌套过深、校验（验证非空（一些文本域：文本框及文件域、而一些特殊的，如性别、生日，它们提交的也是可以直接去判断的）、取（文本域）值、接收文件并验证、持久化（保存）、响应

```
<?php

function add_user() {
  // 验证非空
  if (empty($_POST['name'])) {
    $GLOBALS['error_message'] = '请输入姓名';
    return;
  }

  if (!(isset($_POST['gender']) && $_POST['gender'] !== '-1')) {
    $GLOBALS['error_message'] = '请选择性别';
    return;
  }

  if (empty($_POST['birthday'])) {
    $GLOBALS['error_message'] = '请输入日期';
    return;
  }

  // 取值
  $name = $_POST['name'];
  $gender = $_POST['gender'];
  $birthday = $_POST['birthday'];

  // 接收文件并验证
  if (empty($_FILES['avatar'])) {
    $GLOBALS['error_message'] = '请上传头像';
    return;
  }
  
  //获取扩展名，注意没有.
  $ext = pathinfo($_FILES['avatar']['name'], PATHINFO_EXTENSION);
  // => jpg
  //屏蔽掉中文路径的问题：让目标路径没有中文——文件名字有中文就不要这文件名字
  //两个点表示跳过2层上级文件夹 找到uploads。若想给文件名加个前缀avatar-，就'../uploads/avatar-'。再拼接上扩展名.和$ext
  $target = '../uploads/avatar-' . uniqid() . '.' . $ext;
  //移动到目标路径
  if (!move_uploaded_file($_FILES['avatar']['tmp_name'], $target)) {
    $GLOBALS['error_message'] = '上传头像失败';
    return;
  }
  //取值：头像的地址，这儿注意是用绝对路径/uploads... 用API字符串截取
  $avatar = substr($target, 2);

  //打印检测下有没问题	
  // var_dump($name);
  // var_dump($gender);
  // var_dump($birthday);
  // var_dump($avatar);
  // 保存
  //数据有了之后，接下来就是插入到数据库里面去

  // 1. 建立连接
  $conn = mysqli_connect('localhost', 'root', '123456', 'test');

  if (!$conn) {
    $GLOBALS['error_message'] = '连接数据库失败';
    return;
  } 
  
  // 写完打印测试下
  // var_dump("insert into users values (null, '{$name}', {$gender}, '{$birthday}', '{$avatar}');");
  // 2. 开始查询。修改成添加语句（在数据库执行成功后复制过来，将里面的假数据换成真数据，注意  里面有单引号外面就该用双引号  及解析变量外加花括号来声明变量避免问题提高可读性）
  $query = mysqli_query($conn, "insert into users values (null, '{$name}', {$gender}, '{$birthday}', '{$avatar}');");

  if (!$query) {
    $GLOBALS['error_message'] = '查询过程失败';
    return;
  }

  $affected_rows = mysqli_affected_rows($conn);

  if ($affected_rows !== 1) {
    $GLOBALS['error_message'] = '添加数据失败';
    return;
  }

  // 响应：header跳转
  header('Location: index.php');
}

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  add_user();
}

?>
```

```
html种添加错误信息：
<h1 class="heading">添加用户</h1>
<?php if (isset($error_message)): ?>
    <div class="alert alert-warning">
      <?php echo $error_message; ?>
    </div>
<?php endif ?>
```

客户端（界面）方面：

- 性别文本域最终提交的是什么？option加了value，提交value；若没，提交innertext。 注意这儿value给-1（请选择性别）、0（女）、1（男）
- 关于生日界面处理：html5的日期选择框（移动端用得多）或一些JQ的日期选择器插件（有些可以配合bootstrap样式）

### 改（/编辑）功能

点编辑跳转到编辑页（页面：跟添加页面差不多，复制粘贴改一下部分信息）

注意：头像部分问题留着。文件域不能设置默认值（选不到客户端上用户自己的文件）

逻辑：1.接收处理：接收要修改ID、查询（对应ID）数据、加入SQL更改语句、传入参数（在html中：注意null在==情况跟0相等，所以要===‘0’） 2.提交更改了的表单：

```
// 1. 建立连接
$conn = mysqli_connect('localhost', 'root', '123456', 'test');

if (!$conn) {
  exit('<h1>连接数据库失败</h1>');
}

// 2. 开始查询。只有一条数据但也一定要加limit 1.上面的删除语句也要加：使数据找到这条就不会往下找了，提高效率。
$query = mysqli_query($conn, "select * from users where id = {$id} limit 1;");

if (!$query) {
  exit('<h1>查询数据失败</h1>');
}
```

```
$user = mysqli_fetch_assoc($query);
//因为找不到，就不用呈现下面的html了。所以跳转
if (!$user) {
  exit('<h1>找不到你要编辑的数据</h1>');
}
```

 2.提交更改了的表单：

分析业务：点击编辑按钮（a链接，点击链接肯定会有请求响应的过程发生）,跳转到另一个地址。

在html传上id：

```
<a class="btn btn-info btn-sm" href="edit.php?id=<?php echo $item['id'] ?>">编辑</a>
```

跳转到编辑页面edit.php后，表单提交时也要提交给index.php id，必须在action地址后面加上id

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/%E7%BC%96%E8%BE%91%E5%8A%9F%E8%83%BD%E6%B5%81%E7%A8%8B.png)

```
<form action="<?php echo $_SERVER['PHP_SELF']; ?>?id=<?php echo $user['id']; ?>"
```

3.提交添加后，请求方式从get拿变成了post发：执行最后一张图的红色三步

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/%E7%BC%96%E8%BE%91%E5%8A%9F%E8%83%BD%E6%B5%81%E7%A8%8B.png)

```
function edit () {
  global $user;

  // 验证非空
  if (empty($_POST['name'])) {
    $GLOBALS['error_message'] = '请输入姓名';
    return;
  }

  if (!(isset($_POST['gender']) && $_POST['gender'] !== '-1')) {
    $GLOBALS['error_message'] = '请选择性别';
    return;
  }

  if (empty($_POST['birthday'])) {
    $GLOBALS['error_message'] = '请输入日期';
    return;
  }

  // 取值，到这儿复制上面的
  $user['name'] = $_POST['name'];
  $user['gender'] = $_POST['gender'];
  $user['birthday'] = $_POST['birthday'];

  // 有上传就修改。这儿接收文件部分需要重新去处理，因为有文件接收文件，没有文件就不修改这头像（新增不用）
  if (isset($_FILES['avatar']) && $_FILES['avatar']['error'] === UPLOAD_ERR_OK) {
    // 用户上传了新头像 -> 用户希望修改头像
    $ext = pathinfo($_FILES['avatar']['name'], PATHINFO_EXTENSION);
    $target = '../uploads/avatar-' . uniqid() . '.' . $ext;
    if (!move_uploaded_file($_FILES['avatar']['tmp_name'], $target)) {
      $GLOBALS['error_message'] = '上传头像失败';
      return;
    }
    $user['avatar'] = substr($target, 2);
  }

  // $user => 修改过后的信息
  // TODO: 将数据更新回数据库
}

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  edit();
}
```

文件域要呈现原有头像：

```
<img src="<?php echo $user['avatar']; ?>" alt="">//这条代码。
      <div class="form-group">
        <label for="avatar">头像</label>
```

# 注意

字段类型：char 只适合存固定长度的数据。

​							varchar 可变长度，如名字，一个汉字3个字符的话长度一般设20；性别，tinyint最小字符；数据库不存年龄这种会变的，而是存生日；头像，一般varchar、200长度来存路径

一般表名起名都是复数形式。

表结构添加完，加、改数据：（通过语句去加或可视化界面加，语句加更方便。原因：insert语句多执行几次数据就多了，不用像后者一行行加）

一般每张表都有id，给id设自动增值

性别用数字存，日期SQL语句存给有特殊格式的字符串如2010-12-12

每次代码中要执行查询语句，都先到数据库里试一下