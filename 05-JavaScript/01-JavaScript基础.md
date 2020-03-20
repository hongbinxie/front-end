## js遇到问题：用MDN（js官方文档）

MDN——在线帮助文档

W3C——离线帮助文档

参考手册——离线

ctrl+鼠标左键	转到定义

百度、谷歌，多对比。

找错：用console.log("哈哈");在事件内运行，若不行，说明事件没执行，再将这代码放到上一层，上层不行，说明上层不行，再放上上层...直到行了,说明其下层代码没执行，检查下层代码。（若循环不行，输出该循环元素，若为空，说明上面有错，若上面输出哈哈还是不成功，放到循环内、事件内看看哪错了。）

## 调试js代码：断点调试

- 过去调试JavaScript的方式
  - alert()
  - console.log()
- 断点调试
- 端点：让程序中断在需要的**地方**。从而方便其分析。
- 调试：为了找代码的错误和问题所在

> 断点调试是指自己在程序的某一行设置一个断点，调试时，程序运行到这一行就会停住，然后你可以一步一步往下调试，调试过程中可以看各个变量当前的值，出错的话，调试到出错的代码行即显示错误，停下。

- 调试步骤

```javascript
写代码->打开浏览器->F12（开发人员工具）->Sources->双击文件->（加断点）在某一行代码前面点击一下。再刷新，让该行代码重新执行
```

- 调试中的相关操作

```javascript
Watch: 监视，通过watch可以监视变量的值的变化，非常的常用。可添加、删除值。
F10: 程序单步执行，让程序一行一行的执行，这个时候，观察watch中变量的值的变化。
F8：跳到下一个断点处，如果后面没有断点了，则程序执行结束。
F5：刷新页面
```

tips: ***监视变量，不要监视表达式，因为监视了表达式，那么这个表达式也会执行。***

# js基础

学习：

1.模仿。

2.能自己写。

3.能把大概意思说出来。

4.还能给别人说清楚。

## js分三个部分：

①ECMAScript标准：JS的基本语法

②DOM：Document Object Model文档对象模型。操作页面的元素

③BOM:Brower Object Model浏览器对象模型。操作的是浏览器

## js代码的注意问题：

1.一对script标签中，js代码有错误，则该代码后面的js代码不会执行

2.若前面的script标签有错误，不会影响后面的script标签

3.建议：script标签放在body标签中的最后位置。

4.若script标签起引入js文件作用，则里面不要写任何js代码

5.js大小写敏感，字符串要加单或双引号。

6.注意：作为参数时，值要加双引号，变量不需要。

7.什么时候用事件匿名函数或事件命名（自定义）函数？

如果是循环的方式添加事件，推荐用命名函数

如果不是循环方式添加事件，推荐使用匿名函数

## 注释：

```
//	单行注释
/* */、/** */	多行注释
/**+回车	函数注释
//end if、//end for	有多循环时注释
```

## 1.变量：存储单个数据的容器

变量声明（有var 有变量名，没有值）

**变量初始化**（有var 有变量名，**有赋值**），js一般直接初始化。

注意：变量名一般小写、驼峰法。

**应用：**

变量的交换（3种）

## 2.js数据类型（原始6种+额外）

1）原始属性类型：number、string、boolean、null、undefined、object

①可以再分成： 

- 基本类型（简单类型、值类型）：number、string、boolean。
- 复制类型（引用类型）：object。
- 空类型：undefined、null（无意义的）。

②值类型的值在哪一块空间中存储？栈中存储

引用类型的值在哪一块空间中存储？**对象在堆中存储，地址(引用)在栈中存储**（栈中：放该对象所在空间的地址（也叫引用）。堆中：放该对象）

③值类型之间传递，传递的是值

​	引用类型之间传递的是地址（引用）

​	值类型作为函数的参数，传递的是值

​	引用类型作为函数的参数，传递的是地址（引用）。但注意隐式全局变量！！！

例子：

var num=10; var num2=num;//传递的值：是把num在栈中的值复制一份，拷贝到num2的栈中

function f1(x) {

​	x=100;

}

var num=10;

f1(num);

console.log(num);//10。传递的值：num=10->x=10->f1中x=100，所以x=10被100覆盖。num与x无关，不变。

var obj = {

​	name:"小明"

}；

function f2(obj){

​	obj.name="小红"；

}

console.log（obj.name）;//小明

f2(obj);

console.log(obj.name);//小红。

分析：第倒三条语句：设obj栈中地址0x120,则堆中0x120处存name:"小明"->倒二：传递地址：把obj栈中地址传给obj2，从而指向name:"小明"，，但f2中obj2.name="小红"；所以小明被小红覆盖了->所以最后obj、obj2的地址指向的都是name:"小红"。

```
![1497497865969](C:\Users\74143\Desktop\1497497865969.png)var num1 = 55;
var num2 = 66;
function f1(num, num1) {
  num = 100;
  num1 = 100;
  num2 = 100;
  console.log(num);//100
  console.log(num1);//100
  console.log(num2);//100
}

f1(num1, num2);
console.log(num1);//55
console.log(num2);//100
console.log(num);//报错


function Person(name,age,salary) {
  this.name = name;
  this.age = age;
  this.salary = salary;
}
function f1(person) {
  person.name = "ls";
  person = new Person("aa",18,10);//开空间了，将person的地址换了，但p.name与person无关。
}

var p = new Person("zs",18,1000);
console.log(p.name);//zs
f1(p);
console.log(p.name);//ls
```

![2019-06-10_203425](C:\Users\74143\Desktop\2019-06-10_203425.png)

2）额外：function函数类型。

### 啥时候是undefined：

变量声明了但没赋值。

函数没有返回值或明确的返回值（即return不跟内容），但在调用时接收了。

### 获取数据类型

typeof 变量名

typeof（变量名）

### 类型转换

1.其他类型转数字：（3种）

parseInt()	转整数，要求字符串中第一位就是整数

parseFloat()	转小数，同上

Number()	转数字，要求字符串里只有数字

2.其他类型转字符串类型（2种）

.toString()	当变量有意义（不为undefined或null）时用

String()		当变量有、没意义时都可用

3.其他类型转布尔类型

Boolean()	当变量无意义或为“0”时显示为false

### number类型

范围：最大值Number.MAX_VALUE

​			最小值Number.MIN-VALUE

注意：不要用小数去验证小数

​			表示八进制：以0开头

​			表示十六进制：以0x开头

### string类型

js中的字符串里有转义符，用\。

用+拼接时，只要有一个字符串，其他不管什么类型都是拼接成字符串。

## 3.运算符的优先级

优先级从高到底
	1. ()  优先级最高
	2. 一元运算符  ++   --   !
	3. 算数运算符  先*  /  %   后 +   -
	4. 关系运算符  >   >=   <   <=
	5. 相等运算符   ==   !=    ===    !==
	6. 逻辑运算符 先&&   后||
	7. 赋值运算符

## 4.js流程控制：代码的执行过程（3种）,第一个{要在if同行

顺序结构：从上到下，从左到右执行的顺序。

分支结构：if语句、if-else语句或三元表达式语句、if-else if-esle if...语句、switch-case语句（5种）

注意：前4种是对范围的判断，swith-case是对具体值的判断。

```
1.
if (/* 条件表达式 */) {
  // 执行语句
}
2.
if (/* 条件表达式 */){
  // 成立执行语句
} else {
  // 否则执行语句
}
3.可写多个else if，具体看需求
if (/* 条件1 */){
  // 成立执行语句
} else if (/* 条件2 */){
  // 成立执行语句
} else if (/* 条件3 */){
  // 成立执行语句
} else {
  // 最后默认执行语句
}
```

循环结构：while循环、do-while循环、for循环（可遍历数组）、for-in循环（用来遍历对象）。计数器要写{}里。知道了循环的次数，推荐使用for循环.

```
var i =  ；计数器，可省略
while (条件) {
    要执行的代码块，循环体
    计数器，可省略，如i++;
}
```

continue:立即跳出当前循环，继续下一次循环（for跳到i++的地方、while跳到条件）

break:立即跳出整个循环（直接跳到循环的大括号）

以上两关键字在嵌套循环中，都只能跳出它们所在的那一层循环

若循环多，就添加注释end if、end for

## 5.数组：存储多个数据的容器、一组有序的数据

作用：可以一次性存储多个数据。

显示：直接输出数组名，就可显示数组的数据。

### 定义：（2种）

1.通过**构造函数** **创建**  数组

语法：	var 数组名 = new Array();//空数组。

​				var 数组名 = new Array(一个数字);//数组元素值为undefined的**长度**为该数的数组。

​				var 数组名 = new Array(多个值)；//数组元素**有这些值**的数组。值用，隔开

说明：Array()构造函数、new创建、参数：长度或值（值用，隔开）

2.通过**字面量**创建数组,更简单,不用new

var 数组名 = [];//空数组

var 数组名 = [多个值];//用,隔开

### 设置某位置值：数组名[下标]=值；

### 获取某位置值：var 变量名 = 数组名[下标];console.log(变量名);

### 遍历数组:将数组每个元素都显示出来.方法:用for循环、length设置循环次数

### 冒泡排序：把所有数据按一定顺序进行排列（从小到大，从大到小）

### 应用：

1.将数组元素**放到另一个数组中**：数组声明时为空数组，则当新数组放元素，要：newArr[**newArr.length**] = Arr[i];使动态变长。

2.反转数组：第一个循环：控制交换次数

​						再用交换变量方法

## 6.函数：

含义：把一坨**重复的**代码**封装**，在需要时调用。

作用：代码的重用。 

### 定义：

function 函数名() {

​	函数体，即一坨重复的代码

}

### 调用：函数名();

### js函数参数：函数在调用时用户传进来的值操作。js参数不写数据类型！

形参：函数在**定义**时小括号里的变量。

实参：函数在**调用**时小括号里传入的变量或值。

形参个数和实参个数可以不一致。

### 注意：

1.一个函数最好就一个功能。想要输出，一般是：在函数中用return来返回值。直接输出调用函数或函数调用时给调用一个变量名，再输出该变量。

2.重名函数会覆盖之前的函数。前面对函数的调用也会改变。

3.return会阻止所在函数体后面代码的执行。

4.若输出函数名，则输出的是该函数的定义。

5.想要返回多个值，用return去返回一个数组。

### arguments伪数组的使用

针对情况：定义一个函数，不确定用户传了几个参数时。

方法：使用arguments对象可以获取传入的每个参数的值。（同样用.length方法可以获得长度）

### 函数的其他定义方式:

#### 1.命名函数:

有函数名的函数，定义如上

#### 2.匿名函数:

**没函数名**的函数，匿名函数不能直接调用。

定义：用函数表达式，var **变量名**=匿名函数 **;**。如var f4 = function () {} **;**

​	注意：函数表达式要加；

​				匿名函数的变量名重名不影响之前的。

调用：变量名();	因为变量存储了一个函数，则该变量相当于一个函数，可以加小括号调用。

##### 自调用函数：一次性函数

声明的同时直接加括号调用。不用起名

针对情况：防止有命名，发生冲突

```
(function () {
  alert(123);
})();//将f1()的变量名f1直接用函数代码代替
```

### 函数可作为参数使用，叫回调函数

```
如 function f1(fn) {
	console.log("你好");fn();
   }
   function f2() {console.log("世界");}
   f1(f2);
```

### 函数可作为返回值使用，不用加括号

```
function fn(b) {
  var a = 10;
  return function () {
    alert(a+b);
  }
}
fn(15)();
```

### 函数和构造函数的区别：后者首字母也大写，作用是创建对象。

## 7.作用域

全局变量：使用var声明的变量、除了函数以外其他任何位置定义的变量都是全局变量。如果页面不关闭就不会释放，会占空间、消耗内存。

全局作用域：可在页面的任何位置使用

局部变量：在函数内部定义的变量。函数结束后就会被释放。

局部作用域：函数外部不能使用

隐式全局变量：不加var的变量，不推荐使用

js没有块级作用域一说，只有函数除外：一对大括号里使用的变量，其使用范围是该大括号内。

扩展：delete	删除变量。但全局变量（**使用var定义的变量**）不能被删。

### 作用域链

将所有的作用域按0-n级作用域列出来，可以有一个结构: 函数内指向函数外的链式结构（该链式结构是用来寻找变量的），就称作用域链。

会先找最近的作用域的变量。

## 8.预解析：提前解析代码

（js是解释语言，即遇到一行代码就解释一行代码，再执行一行代码。）

含义：**在解析代码之前**，会先把变量、函数的声明（定义）提前，提前到当前所在作用域**中**的 最上面！不会提升赋值、调用。

注意：预解析会分段（多对**script标签中**函数重名，预解析时不会冲突）。变量的声明会先找。

#### 特别注意：

```
（var f1;）
f1();//报错！
var f1=function(){//假象
	console.log(a);
	var a=10;
};
```

## 9.对象（一种无序属性的集合）

### 了解：

1.编程思想：把一些做事的经验融入到程序中。

面向过程：凡事都要亲力亲为，每件事的具体过程都要知道，注重的是过程。

面向对象：只要 根据需求找对象，所有事都用对象来做，注重的是结果。

面向对象特征：封装、继承、多态（抽象性）

2.js不是面向对象语言，js特性只有封装。但是可以**模拟**面向对象的思想。

js是一门**基于**对象的语言，js特征只有封装功能。但js能找对象、创建对象。

3.实例（动态）对象:通过构造函数创建出来，实例化的对象。（创建：用new）

​	实例方法必须通过实例对象调用。

静态对象：不需要创建，直接就是一个对象，方法（静态方法）直接通过这个对象名字调用。

​	静态方法必须通过大写的对象调用。

### 过程：

**找对象**（先了解什么是对象）->分析对象有什么特点：特征、行为->总结什么是对象->没有对象，就创建对象。

1.什么是对象：看得见，摸得到，具体特指的某**个**事物

2.找对象：基于上面概念，再通过**描述**找对象，再通过**文字描述**找对象

3.分析该对象有什么特点（特征、行为）

​	特征：属性。	行为：方法。

### 创建对象：（4种），也叫实例化对象

1.调用**系统的构造函数**创建（一个）对象。

​	**var 变量名 = new Object();**	//Object是构造函数

​	//对象有特点（属性）、行为（方法）

​	//如何添加属性？

​	变量名.属性名=值;	

​	//如何添加方法？

​	变量名.方法名=函数;

​	//如何获取属性？

​	console.log(变量名.属性名);

​	//如何调用方法 ？

​	变量名.方法名()；

​	//在当前对象的当前属性、方法中，可以使用this代表当前对象

```
var person = new Object();
  person.name = 'lisa';
  person.age = 35;
  person.job = 'actor';
  person.sayHi = function(){
  console.log('Hello,everyBody');
}
```

2.**工厂模式**创建（一个及以上）对象（结合第一种和需求通过）。

可一次性创建多个对象。

把创建对象的代码封装在一个函数中。

function createPerson(**name**, **age**, **job**) {
  var person = new Object();
  person.name = **name**;
  person.age = **age**;
  person.job = **job**;
  person.sayHi = function(){
    console.log('Hello,everyBody');
  }
  **return** person;
}
var p1 = createPerson('张三', 22, 'actor');	

3.**自定义构造函数**创建（一个及多个）对象。

function **Person**(name,age,job){

//注意！不用设return。
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayHi = function(){
  	console.log('Hello,everyBody');
  }
}
var p1 = new **Person**('张三', 22, 'actor');//此时系统做了4件事：（1）在内存中开辟（申请一个空闲的空间）空间，存储创建的新的对象（2）把this设置为当前对象（3）设置对象的属性和方法的值（4）把this这个对象返回。

4.**字面量**方式创建对象

缺点：一次性的对象。

普通写法：

var 变量名 = **{}**;//空对象。添加，调用属性、方法同第一种。

优化后写法：

var 变量名 = {

​	//添加属性

​	属性名：值，

​	//添加方法

​	方法名:函数

};

调用方法同第一种。修改内容，同第一种。

```
var o = {
  name: 'zs',
  age: 18,
  sex: true,
  sayHi: function () {
    console.log(this.name);
  }
};   
```

### new的执行过程：

（1）在内存中开辟（申请一个空闲的空间）空间，存储创建的新的对象（2）把this设置为当前对象（3）设置对象的属性和方法的值（4）把this这个对象返回。

### 总结对象

### json对象：其数据一般是键值对

json对象的数据都是成对的，一般json格式数据的值都用**双引号**括起来。键可不用。

目的：方便传值。把多个对象存到数组里，再遍历数组，里层再遍历对象来传值。

```
var json = {
	"name":"小明",
	"age":"10",
};
```

```
var objs=[phone1,phone2,phone3];
for(var i=0;i<objs.length;i++){
	var obj = objs[i];
	for(var key in obj){
		......
	}
}

phone1 = {"":"","":"","":""};
phone2 ={};
```



### 设置和访问（调用）属性、方法的两种方法

点语法：	变量名.属性名=值;设置属性

​					变量名.方法名=函数;//设置方法

​					console.log(变量名.属性名);//调用属性

​					变量名.方法名();//调用方法

双引号法：变量名[“属性名”]=值;//设置属性

​					变量名[“方法名”]=函数;//设置方法

​					console.log(变量名[“属性名”]);//调用属性

​					变量名[“方法名”]（）;//调用方法

也可以将属性名、方法名赋值给变量，通过对象调用			

```
var key = "name";
console.log(json[key]);//因为key是变量，不是字符串，不加双引号
```

### 遍历对象：通过for in循环

不能通过for循环遍历。因为无序。

可以通过for in循环

```
for(var key in json){//定义个变量，存的是该对象的所有属性名
	console.log(key);//输出json对象的属性名
	console.log(json[key]);//通过变量调用属性。
}
```

### 内置对象（不懂去查手册）

#### js中有四类对象：

1.内置对象——js系统自带的对象

2.自定义对象——自定义构造函数

3.浏览器对象——BOM

4.文档对象——DOM：通过DOM方式获取到的元素

#### Math对象

​	不是函数对象（js高级中讲），即是对象但不是函数。

​	不是构造器（构造函数），其属性、方法都是静态的：直接通过对象名. 出来的。

​	常用方法：

```javascript
Math.PI						// 圆周率
Math.random()				// 生成随机数，一般~*n+1,才能取大值
Math.floor()/Math.ceil()	 // 向下取整/向上取整
Math.round()				// 取整，四舍五入
Math.abs()					// 绝对值
Math.max()/Math.min()		 // 求最大和最小值

Math.sin()/Math.cos()		 // 正弦/余弦
Math.power()/Math.sqrt()	 // 求指数次幂/求平方根
```

#### Date对象

创建 `Date` 实例用来处理日期和时间。

常用：

```javascript
1.实例化对象：
var dt=new Date();	   //当前的服务器日期时间
var dt=new Date(字符串);	  //传入的时间（年月日用-或/隔开）
var dt=Date.now();	//当前服务器毫秒时间（从1970年1月1日到现在的毫秒数）
2.实例化方法：
var dt=new Date();
console.log(dt.getFullYear());	//获取年份	
console.log(dt.getMonth());	//获取月份，从0开始的，真实月份要+1
console.log(dt.getDate());	//获取日期
console.log(dt.getHours());	//获取小时
console.log(dt.getMinutes());	//获取分钟
console.log(dt.getSecond());	//获取秒
console.log(dt.getDay());	//获取星期，0是星期天，其他正常。
2.1 格式化方法：
toString()		// 转换成字符串
valueOf()		// 获取毫秒值
// 下面格式化日期的方法，在不同浏览器可能表现不一致，一般不用
toDateString()	//英文日期
toTimeString()	//数字格式日期
toLocaleDateString()	//小时分钟秒，英文的
toLocaleTimeString()	//小时分钟秒
// 不支持HTML5的浏览器，可以用下面这种方式
var now = + new Date();			// 调用 Date对象的valueOf() 
```

例子：格式化日期和时间

​			把毫秒值转换为对象： var dt=new Date(dt.valueOf());

#### String对象

​	也是字符串类型，但是引用类型。

​	是构造函数

​	字符串可以看成是字符组成的数组，可通过for循环进行遍历。

​	字符串具有不可变性。字符串的值是不能改变（字符串不可以通过索引来改变字符串中某个值。）而字符串的值之所以看起来是改变的,那是因为指向改变了,并不是真的值改变了。

字符串的常用属性:

​     .length------>字符串的长度

​    .charAt(索引),返回值是指定索引位置的字符串,超出索引,结果是空字符串

​    .fromCharCode(数字值,可以是多个参数),返回的是ASCII码对应的值

​     .concat(字符串1,字符串2,...);返回的是拼接之后的新的字符串

​      .indexOf(要找的字符串,从某个位置开始的索引);返回的是这个字符串的索引值,没找到则返回-1

​      .lastIndexOf(要找的字符串);从后向前找,但是索引仍然是从左向右的方式,找不到则返回-1

​     .replace("原来的字符串","新的字符串");用来替换字符串的

​     .slice(开始的索引,结束的索引); 从索引5的位置开始提取,到索引为10的前一个结束,没有10，并返回这个提取后的字符串

​      .split("要干掉的字符串",切割后留下的个数);切割字符串

​     .substr(开始的位置,个数);返回的是截取后的新的字符串

​      .substring(开始的索引,结束的索引),返回截取后的字符串,不包含结束的索引的字符串

​    .toLocaleLowerCase();转小写

​    .toLowerCase();转小写

​    .toLocaleUpperCase()转大写

​     .toUpperCase();转大写

​    .trim();干掉字符串两端的空格

#### Array对象

​	 Array.isArray(对象)---->判断这个对象是不是数组
​     instanceof关键字
​      .concat(数组,数组,数组,...) 组合一个新的数组
​      .every(函数)--返回值是布尔类型,函数作为参数使用,函数中有三个参数,第一个参数是元素的值，第二个参数是索引值,第三个参数是原来的数组(没用)
​      如果这个数组中的每个元素的值都符合条件,最后才返回的是true
​    
​     .filter(函数);返回的是数组中每一个元素都复合条件的元素,组成了一个新的数组
​    
​     .push(值);--->把值追加到数组中,加到最后了---返回值也是追加数据之后的数组长度
​      .pop();--->删除数组中最后一个元素,返回值就是删除的这个值
​      .shift();--->删除数组中第一个元素,返回值就是删除的这个值
​     .unshift();--->向数组的第一个元素前面插入一个新的元素,----返回值是插入后的程度
​      .forEach(函数)方法---遍历数组用---相当于for循环。ECMA5的，要想用，到MDN找兼容旧环境把固定代码放在一个js文件中或调用之前。
​     .indexOf(元素值);返回的是索引,没有则是-1
​     .join("字符串");----往字符串中间返回的是一个字符串
​      .map(函数);--->数组中的每个元素都要执行这个函数,把执行后的结果重新的全部的放在一个新的数组中
​      .reverse();----->反转数组
​     .sort();---排序的,可能不稳定,如果不稳定,请写MDN中的那个固定的代码
​      .arr.slice(开始的索引,结束的索引);把截取的数组的值放在一个新的数组中,但是不包含结束的索引对应的元素值
​      .splice(开始的位置,要删除的个数,替换的元素的值);一般是用于删除数组中的元素,或者是替换元素,或者是插入元素

#### Objct对象（js高级有意义）

## 基本包装类型

**普通变量**不能直接调用属性、方法

**对象**可以直接调用属性、方法

基本包装类型：本身是基本类型，但在执行代码过程中，若基本类型变量调用了属性、方法，那么该类型就不再是基本类型而是基本包装类型，这个变量也不是普通变量了，而是基本包装类型对象。string、number、boolean

### 注意：

1.如果是一个对象&&true，那么结果是true

如果是一个true&&对象，那么结果是对象

```
var flag=new Boolean(false);
var result=true&&flag;//Boolean
console.log(result);
```

2.

```
var num=10;
var num2=Number("10");	//转换，没有new
var num3=new Number("10")	//基本包装类型
```

# WEB API

API（应用程序编程接口）：就是系统提供给我们的方法（函数），（相当于程序给的后门，不用知道主程序是怎么开发的，你只要调用这个接口就能用了）。

WEB API： 浏览器提供的方法。

## DOM(文档对象模型)，操作页面元素的

先理解

（文档：把一个html文件看成是一个文档，由于万物皆对象，所以把这个文档看成是一个对象。

XML文件也可以看成是一个文档。）

（HTML：展示数据的。

XML:存储数据的。

目的：不用任何软件就可以打开。 

内容：没有系统标签，标签都自定义、但要遵循规范：

加个固定的xml版本标签:<?xml ...?>

加个自定义根标签，根标签里放其他标签）

### 概念

文档（document）：一个页面就是一个文档。

元素（element）：页面中所有的标签。标签可以看成元素，**元素可以看成是对象**。

节点（node）：页面中所有的内容。（内容有：标签、属性、文本（文本包括文字、换行、空格、回车等））

根元素：html标签

（又页面就是文档，文档中有根元素：html

html中有其它标签）

顶级对象：document

### DOM树

由文档及文档中的所有元素（标签）组成的一个树型结构图，叫DOM树。

### （重点记忆）DOM经常进行的操作

- 获取（页面）元素

- 动态创建元素

- 对元素进行操作(设置其属性或调用其方法)

- 事件(什么时机做相应的操作)：就是一件事，有触发和响应、事件源、事件名。

  如按钮被点击，弹出对话框：

  按钮——事件源

  点击——事件名，事件是个行为（函数、方法）

  被点了——触发了

  弹框了——响应

注意：js嵌入到html中，不方便维护

​			应把js代码和html分离。

## DOM操作（页面元素的）步骤：

1.获取元素（标签、事件源）。（可以不给获取到的元素设变量名：当获取请求少时。设了变量名时，下面的处理函数里可以用this代替变量名，表示当前的元素对象）

2.为该元素注册（添加）事件：元素.事件名

3.为事件添加响应（事件处理函数，事件处理函数里写响应做的事）：

​		①元素.事件名**=函数名** **;**	不能加括号。（不能=函数调		用，因为事件需要的是**函数的代码**，要触发事件才能调		用，否则打开页面直接就调用了。）在嵌入中就是事件名=“函数调用”；

​		缺点：函数名有冲突问题

​		②优化版：

​		元素.事件名=匿名函数;	//匿名函数的函数名不会发生		冲突

4.在**事件处理函数中**设置**页面中各元素**的属性(可设置多个）。

（设置文本内容：

- innerHTML：它可以设置标签内容（包括文本内容、标签），有标签效果。推荐！！！
- innerText：设置文本，没有标签效果（会把标签也当文本输出）且**获取不了标签中的标签**，还有兼容问题。不推荐！！！
- 表单文本内容：推荐用value设置！！！因为上面2个不会在控制台有显示数据

样式属性名style。修改属性的属性可:元素.属性名.属性名

)

​	也是：元素.属性名=值;

​	（设置包括增删改查等操作。）

最终代码举例：

假设有btn、p原本内容为段落。

```
document.getElementByI("btn").onclick = function () {
	document.getElementById("p1").innerText = 	"这是一个p";
};
```

测试操作结果：2种s

1.看检查F12的element中有没有结果

2.看页面有没有效果

若不行，点开控制台查看错误。

### 获取元素

```javascript
1.获取哪些元素（标签）：
掌握
	.getElementById()	//根据id获取元素，返回一个元素对象
	.getElementsByTagName()	//根据 标签名 获取同类元素，返回的是一个伪数组，里面保存了多个DOM对象。注意s。
	.getElementsByTagName()[index]	//获取第index个同类标签
了解	都属于h5的
	.getElementsByName()	//根据 属性值 获取元素，返回一个伪数组。有的浏览器不支持
	.getElementsByClassName()//根据 类样式的名字 获取元素，返回一个伪数组。
	.querySelector()	//根据 选择器 获取一个元素。因为选择器有很多，只记三个：id、标签、类
	.querySelectorAll()	//根据选择器 获取 多个 元素，返回一个伪数组。
2.从哪获取：
	document	//从文档中获取
    document.getElementById(父元素名)	//从某元素（某块）中获取
3.注意
//给每个标签都设，用for循环遍历设置,把事件放里面。
//若用getElementsByTagName(),则不能直接元素.事件名=函数名、元素.属性=值，而要元素[index].事件名=函数名、元素[index].属性=值;因为返回的是伪数组。或用this.，但要注意this此时的值。
//若不想给同类标签同块中的一个标签设置，则用if筛选想给的或给不想的设id。
```

### 注意

1.凡是css中这个属性是多个单词的写法,在js代码中DOM操作时,把-干掉,后面的单词的首字母大写即可.、

2.在js代码中DOM操作时，设置元素的类样式，不用class关键字，应该使用className

3.用类样式设置div的样式：把要设的一堆样式写在css中，DOM中直接赋给元素类名就好。不用一个一个设样式。超过3个样式时推荐用。

4.一般搜索框用得到焦点onfocus、失去焦点onblur事件

​			图片等用鼠标进入onmouseover、鼠标离开onmouseout事件

### innerTxt和innerContent的兼容问题

innerTxt			//设置标签中间的内容，低版本火狐不支持

innerContent	//设置标签中间的内容，IE8不支持

```javascript
解决方法——写兼容代码：
//如果这个属性在浏览器不支持，那么这个属性的类型是undefined
//换句话说，若想知道浏览器支不支持一个属性，那么就判断这个属性的类型是不是undefined
代码：
function setInnerText(element,text){
    //判断浏览器是否支持这个属性：innerText。如果不支持就返回另个属性,如果支持就按原来的。
    if(typeof element.innerText=="undefined"){
        element.innerContent=text;
    }else{
        element.innerText=text;//如果支持就按原来的。
    }
}
function getInnerText(element){
    if(typeof element.innerText=="undefined"){
        return element.innerContent;
    }else{
        return element.innerText;
    }
}
```

#### 优化代码：把获取功能封装

```javascript
function my$(id){
	return document.getElementById(id);
}//封装完记得把该代码放到common.js中！
my$("btn").onclick=function() {
    this.src="images/1.jpg";
}
```

### 元素的样式操作

元素.style.属性=值；

元素.className=值；

### 排他功能

在事件处理函数中：

先把所有同类标签变为默认的值（事件处理函数中设个for循环，循环里面放这个），

再把当前点击的标签设为响应后的（放在事件处理函数中的for循环外的下面）。

![2019-06-11_182152](C:\Users\74143\Desktop\2019-06-11_182152.png)

注意！：这里的**this**.value不能用btnObjs[j]代替

原因：for循环是在页面加载的时候，执行完毕了

​			事件是在触发时，执行的

​			导致了此时的j=btnObjs.length=6，因为伪数组中没有下标6的元素，若用会报错。且这里不是为了让i改变，而是让元素改变，所以用this。

#### 例子：Tab切换案例（重点，排他功能）

原理：排他功能（让所有同类标签隐藏，让一个显示）。保存Tab栏的索引，把索引给下面的内容栏，让对应索引的内容栏显示。

## 案例（重点）

### 点击小图不跳转显示大图：2种

没超链接来切换图片

```javascript
document.getElementById("im").onclick=function() {
    this.src="images/1.jpg";
}
```

点击超链接切换图片

```javascript
<a id="ak" href="images/1.jpg"><img src="images/1-small.jpg" alt="" id="im"/></a>
<script>
    //点击图片，设置图片标签的src路径为超链接中大图的路径。
    document.getElementById("im").onclick=function() {
    this.src=document.getElementById("ak").href;
 return false;//重点，缺了这个不能实现！！！原因：看下面
}
</script>
```

### 点击按钮时改变表单默认选项

input中：
name、value都是要提交给后台的
name相同：设置为一组

value要不同：来区别。

**规律：**在表单标签中，如果属性和值**只有一个**，且值是这个**属性本身**，那么在写js代码的DOM操作时，这个属性值是布尔类型就可以了。如input的checked=“checked”可以写成checked=true，优化代码。

### 让一个按钮具备多个功能(如隐藏/显示)

用if语句

### 设置div样式优化案例:

把要设的一堆样式写在css中，DOM中直接赋给元素类名就好。不用一个一个设样式。超过3个样式时推荐用。

```
<style>
	.cls{
		width:300px;
		height:200px;
		dispaly：none；
	}
</style>
...
<script>
	my$("btn").onclick=function() {
		my$("dv").className="cls"
	}
</script>
```

### 网页开关灯（宣传节约电能用）

点按钮时设document.body的背景颜色为黑色，按钮值可以为开/关灯 

### 阻止超链接默认跳转（return false;）

因为函数都有返回值，当不返回就没有操作。

没有返回值的布尔类型为false，所以我们用return false；

```
写法1：<a href="www.baidu.com" onclick="alert(1);return false">百度</a>
优化写法：
<script>
function f1() {
	alert(1);
	return false;
}
</script>
<a href="www.baidu.com" onclick="return f1()">百度</a>
第三种写法（最优）：DOM操作，自己写。
```

其例子：美女相册。

弹出二维码

高亮显示

模拟搜索框、失去焦点

验证文本框密码长度



## js DOM操作常用方法

隐藏/显示:	元素.style.display="none/block";

## 自定义属性（重点）

含义：本身html没有这个属性，程序员为了存储一些数据自定义的。

操作：

- **手动**添加、获取自定义属性：在html标签中添加一个自定义属性，若想获取这个属性的值，需要使用getAttribute("属性名")。不推荐！！！

- **动态**添加、获取自定义属性：推荐！！！

  ​	设置自定义属性：setAttribute(“属性名”，“属性值”)

  ​	获取自定义属性：getAttribute("属性名")

- 移除（自定义、自带）属性：removeAttribute("属性名")

## 移除属性的值和移除属性

- 让属性="";	//移除属性的值，不是移除属性
- 移除属性：removeAttribute("属性名")

## 节点

### 概念

含义：

用途：为了更方便操作元素。任意一个标签中的元素获取都非常方便

### 节点的属性（3个）

特性：

- 可以使用标签（元素）.出来
- 可以使用属性节点.出来
- 可以使用文本节点.出来

nodeType:节点的类型1——标签、2——属性、3——文本。

nodeName：节点的名字：标签节点——大写的标签名、属性节点——小写的属性名、文本节点——#text

nodeValue：节点的值：标签节点——null、属性节点——属性值、文本节点——文本内容 

### 获取相关的节点（12行代码）

```javascript
一、注意：
1.父节点=父元素(标签)。
页面里有标签、属性、文本，但只有标签能做父节点。
2.子节点！=子元素。子节点范围更大（标签、属性、文本）。
3.从子节点和兄弟节点开始，只要是节点在IE8中是元素，只要是元素IE8中就不支持、得到的是undefined。谷歌、火狐都正常。
二、12行代码
//父节点
.parentNode
//父元素
.parentElement
//子节点
.childNodes
//子元素
.children

//第一个子节点。下面的只要是节点在IE8中是元素。谷歌、火狐正常
.firstChild
//第一个子元素。下面的只要是元素在IE8中不支持。谷歌、火狐正常
.firstElementChild
//最后一个子节点
.lastChild
//最后一个子元素
.lastElementChild
//某个元素的前一个兄弟节点
.previousSibling
//某个元素的前一个兄弟元素
.previousElementSibling
//某个元素的后一个兄弟节点
.nextSibling
//某个元素的后一个兄弟元素
.nextElementSibling
```

### 封装节点的兼容代码（5段）

### 通过节点的方式来操作（增删改查）元素

实例：

1. 通过节点操作元素的背景颜色
2. 通过节点操作隔行变色

## 元素的创建（3种）

### 为什么要有元素的创建？

为了提高用户体验。尽可能让网站元素少只显示必要的东西，当鼠标放到某位置时才显示

### 创建元素的3种方式：

1.document.write("标签的代码及内容"); 

​	页面加载时不影响原有内容。

​	百度“百度新闻代码”，用此方式可以嵌入外部的代码内容。

​	缺点：如果是在页面加载完毕后，此时通过这种方式创建元素，那么页面上存在的所有内容都被干掉了

2.对象.innerHTML="标签及代码";

​	通过字符串方式创建，再为该对象**赋值**。

​	注意：不能直接放在body中，否则跟第一种同效果。一般放到一个盒子中。

3.document.createElement(“标签的名字”);

​	通过对象方式创建。

优点：方便。	第三种方式创建元素，要再把元素追加到父级元素中：my$("dv").appendChild(pObj);

​	缺点：会重复创建。只创建一个按钮优化方案：有则删除，无则创建

```javascript
my$("btn").onclick=function () {
        //判断,div中有没有这个按钮,有就删除
        //判断这个按钮的子元素是否存在
        if(!my$("btn2")){//如果为true就有
            var obj=document.createElement("input");
            obj.type="button";
            obj.value="按钮";
            obj.id="btn2";
            my$("dv").appendChild(obj);
        }

};
```

### 元素操作（添加元素、移除元素）

```javascript
var body = document.body;
var div = document.createElement('div');
body.appendChild(div);

var firstEle = body.children[0];
body.insertBefore(div,firstEle);

var text = document.createElement('p');
body.replaceChild(text, div);

body.removeChild(firstEle);
```

## 事件

### 绑定事件方式（BOM中：3种）

BOM中有3种，JQuery中有更多——

1.只能绑定一个事件的，不能绑定多个，否则会干掉前面的：对象.on+事件类型=事件处理函数。

> #### 下面的2种是为同一元素绑定多个相同事件的：（2种+兼容代码）

2.对象.addEventListener("事件类型"，事件处理函数，false)；——谷歌、火狐支持，IE8不支持

> 参数1:事件的类型---事件的名字,没有on。
> 参数2:事件处理函数---函数(命名函数,匿名函数)。
> 参数3:布尔类型,目前就写false。

```javascript
 my$("btn").addEventListener("click",function () {
    console.log("小苏猥琐啊");
  },false);
  my$("btn").addEventListener("click",function () {
    console.log("小苏龌龊啊");
  },false);
  my$("btn").addEventListener("click",function () {
    console.log("小苏邪恶啊");
  },false);
  my$("btn").addEventListener("click",function () {
    console.log("小苏下流啊");
  },false);
```

3.对象.attachEvent(“有on的事件类型”，事件处理函数)；——IE8支持，火狐谷歌不支持

> 参数1:事件类型---事件名字，有on
> 参数2:事件处理函数---函数(命名函数,匿名函数)

```javascript
my$("btn").attachEvent("onclick",function () {
    console.log("小杨好帅哦1");
 });

my$("btn").attachEvent("onclick",function () {
    console.log("小杨好帅哦2");
 });

 my$("btn").attachEvent("onclick",function () {
   console.log("小杨好帅哦3");
 });
```

所以有了：兼容代码——

```javascript
//为任意元素绑定任意的事件。参数1： 任意的元素,事件的类型,事件处理函数
function addEventListener(element,type,fn) {
  //判断浏览器是否支持这个方法
  if(element.addEventListener){
    element.addEventListener(type,fn,false);
  }else if(element.attachEvent){
    element.attachEvent("on"+type,fn);
  }else{
    element["on"+type]=fn;//或element."on"+type=fn;
  }
}

addEventListener(my$("btn"),"click",function () {
  console.log("哦1");
});
addEventListener(my$("btn"),"click",function () {
  console.log("哦2");
});
addEventListener(my$("btn"),"click",function () {
  console.log("哦3");
});
```

#### 绑定事件的区别

相同点：都可以为元素绑定事件

不同点：方法名不一样；参数个数不一样；浏览器支持情况不一样；

​				this不同：addEventListener是当前绑定事件的对象，attachEvent中的this是

​				window；事件类型不一样：前者+on，后者不加。

### 解绑事件的方式（3种）

> 注意：用什么方式绑定事件，就应该用对应的方式解绑事件
>
> ​			第二、三种解绑方式，需要在绑定事件的时候，使用命名函数

1.对象.on事件名=事件处理函数；——>解绑：对象.on事件名=null;

2.对象.addEventListener("没有on的事件类型"，命名函数，false)；

——>解绑：对象.removeEventListener("事件类型"，命名函数的名字，false)；——支持程度同绑定事件

3.对象.attachEvent("on事件类型",命名函数);

——>解绑：对象.detachEvent("on事件类型",函数名字);

```
2.的代码：
function f1() {
    console.log("第一个");
  }
  function f2() {
   console.log("第二个");
 }
  my$("btn").addEventListener("click",f1,false);
 my$("btn").addEventListener("click",f2,false);

  //点击第二个按钮把第一个按钮的第一个点击事件解绑
 my$("btn2").onclick=function () {
   //解绑事件的时候,需要在绑定事件的时候,使用命名函数
    my$("btn").removeEventListener("click",f1,false);
  };
```

### 绑定、解绑事件的兼容代码

```
//绑定事件的兼容
function addEventListener(element,type,fn) {
  if(element.addEventListener){
    element.addEventListener(type,fn,false);
  }else if(element.attachEvent){
    element.attachEvent("on"+type,fn);
  }else{
    element["on"+type]=fn;
  }
}
//解绑事件的兼容
//为任意的一个元素,解绑对应的事件
function removeEventListener(element,type,fnName) {
  if(element.removeEventListener){
    element.removeEventListener(type,fnName,false);
  }else if(element.detachEvent){
    element.detachEvent("on"+type,fnName);
  }else{
    element["on"+type]=null;
  }
}
function f1() {
  console.log("第一个");
}
function f2() {
  console.log("第二个");
}
addEventListener(my$("btn1"),"click",f1);
addEventListener(my$("btn1"),"click",f2);
my$("btn2").onclick=function () {
  removeEventListener(my$("btn1"),"click",f1);
};
```

### 事件冒泡（每次都要先考虑到，阻止发生）

事件冒泡：多个元素嵌套，有层次关系，这些元素都注册了相同的事件，如果里面的元素的事件触发了，那么外面的元素的该事件会自动触发。方向：从里向外（从上到下）

为同一个元素绑定多个不同的事件，指向的是同一个事件处理函数

标签嵌套：实际上是覆盖的关系。

#### 阻止事件冒泡（BOM）

1.window.event.cancelBubble=true——IE、谷歌支持，火狐不支持。

2.e.stopPropagation(); 谷歌和火狐支持，IE8不支持e。e要为事件处理函数的参数

（window.event对象（IE中的标准）=e对象（火狐的标准））

### 事件的三个阶段

可通过e.eventPhase这个属性可以知道当前的事件是什么阶段的，对应值如下：

1.事件捕获阶段：从外向内，布尔类型：true

2.事件目标阶段：最开始选择的目标，但不一定最先出现

3.事件冒泡阶段：从里向外，布尔类型：false

> addEventListener("没有on的事件类型"，事件处理函数，控制事件阶段的)
>
> 一般默认都是冒泡阶段，很少用捕获阶段。

### 为同一个元素绑定多个不同的事件，指向相同的事件处理函数

```javascript
my$("btn").onclick = f1;
my$("btn").onmouseover = f1;
my$("btn").onmouseout = f1;
function f1(e) {
  switch (e.type) {
    case "click":
      alert("好帅哦");
      break;
    case "mouseover":
      this.style.backgroundColor = "red";
      break;
    case "mouseout":
      this.style.backgroundColor = "green";
      break;
  }
}
```

封装动画函数——匀速的动画函数，过渡到缓动的动画函数

**轮播图**

​		简单

​		左右焦点

​		无缝连接

## **三大系列之一：offset系列**

在任意位置获取到元素的样式：宽（有边框）、高（有边框）、离左离右距离、父级元素（标签）

具体值：

```
没有脱离文档流:
offsetLeft:父级元素margin+父级元素padding+父级元素的border+自己的margin
脱离文档流：
主要是自己的left和自己的margin
```

> 用style.属性来获取的话：如果样式是在CSS中设置，那么外面是获取不到的
> 在style属性中，可以获取到。 

## 三大系列之二：scroll系列

”卷曲——滚出去“的意思

一、属性:

1.元素中内容的**实际宽、高**（无边框）。如果内容少或没，就是元素的宽高。

2.向上、左卷曲出去的距离

二、滚动事件onscroll

三、封装系列的属性：浏览器向上、左卷曲出去的距离的值：

```javascript
//最终版本：这里将上、左卷曲封装在一起，要返回2个值：用return只能1个、用一般对象.属性代码较多、用json对象.属性成形。
//0是防止浏览器都不兼容时不会报错
function getScroll() {
  return {
    left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft||0,
    top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0
  };
}
```

四、固定导航栏案例

2个bug：①下的标准流部分会顶替脱离文档流部分：将标准流的margin-top用offsetHeight限制②滚动回来时将修改的东西重置。

## 三大系列之三：client系列

可视区域的宽（无边框，边框内部的宽）、高、左边框的宽度、上边框的高度、可视区域的横坐标、可视区域的纵坐标

### 实例：图片跟着鼠标移动

第一个版本：不修复bug的

```
<body>
<img src="images/tianshi.gif" alt="" id="im">
<script src="common.js"></script>
<script>
  //鼠标在页面中移动,图片跟着鼠标移动
  //通过arguments.length，可以得出:事件处理函数中实际上是有一个参数的,这个参数和事件有关系,是一个对象----->事件参数对象，我们给它自定义名字e
  //谷歌和火狐中都有这个事件参数对象,但IE8中没有
  //事件参数对象:e----在IE8中用window.event来代替，但火狐不支持
  //页面的鼠标移动事件
  document.onmousemove=function (e) {
    //鼠标的移动的横纵坐标
    //可视区域的横坐标
    //可视区域的纵坐标
    e=window.event||e;//简化！：兼容代码
 	my$("im").style.left=e.clientX+"px";
 	my$("im").style.top=e.clientY+"px";
  };
</script>
</body>
```

实际有很多bug，这儿要封装到好几个函数，再封装到对象（文件）里面：

bug1：页面是大于可视区域的，如因为clientY不变，当页面向上滚动，clientY就会往上缩（卷曲），导致虽然鼠标不动，但图片也往上缩，脱离鼠标

debug1：当滚动条滚动时，图片被限制在原来的可视区域的范围内：

​	①pageX、pageY相当于页面顶部的距离，但！IE8不能用

​	②所以只能用client系列：clientY(可视区域的距离)+向上卷曲出去的距离（但需要兼容代码）、clientX(可视区域的距离)+向左卷曲出去的距离（但需要兼容代码）。下面修复：

第二个版本：添加兼容代码，可以在任何浏览器中实现

```javascript
<body>
<img src="images/tianshi.gif" alt="" id="im">

<script src="common.js"></script>
<script>
  document.onmousemove=function (e) {
    //鼠标的移动的横纵坐标
    //可视区域的横坐标
    //可视区域的纵坐标
    e=window.event||e;//简化！：兼容代码
    
    function getScroll(){
        return{
  top:window.pageYOffset||document.body.scrollTop||document.documentElement.scrollTop||0,
  left:window.pageXOffset||document.body.scrollLeft||document.documentElement.scrollLeft||0
     	}
    }	
    //可视区域横坐标+向左卷曲出去的横坐标 	
  my$("im").style.left=e.clientX+getScroll().left+"px";
 	//可视区域纵坐标+向上卷曲出去的横坐标
  my$("im").style.top=e.clientY+getScroll().top+"px";
  };
</script>

</body>
```

最终版本：

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>title</title>
  <style>
    *{
      margin: 0;
      padding: 0;
    }
    body{
      height: 2000px;
    }
    img{
      position: absolute;
    }
  </style>
</head>
<body>
<img src="images/bird.png" alt="" id="im" />
<script src="common.js"></script>
<script>
  //图片跟着鼠标飞,可以在任何的浏览器中实现
  //window.event和事件参数对象e的兼容
  //clientX和clientY单独的使用的兼容代码
  //scrollLeft和scrollTop的兼容代码
  //pageX,pageY和clientX+scrollLeft 和clientY+scrollTop

  //把代码封装在一个函数

  //把代码放在一个对象中
  var evt={
    //window.event和事件参数对象e的兼容
    getEvent:function (evt) {
      return window.event||evt;
    },
    //可视区域的横坐标的兼容代码
    getClientX:function (evt) {
      return this.getEvent(evt).clientX;
    },
    //可视区域的纵坐标的兼容代码
    getClientY:function (evt) {
      return this.getEvent(evt).clientY;
    },
    //页面向左卷曲出去的横坐标
    getScrollLeft:function () {
      return window.pageXOffset||document.body.scrollLeft||document.documentElement.scrollLeft||0;
    },
    //页面向上卷曲出去的纵坐标
    getScrollTop:function () {
      return window.pageYOffset||document.body.scrollTop||document.documentElement.scrollTop||0;
    },
    //相对于页面的横坐标(pageX或者是clientX+scrollLeft)
    getPageX:function (evt) {
      return this.getEvent(evt).pageX? this.getEvent(evt).pageX:this.getClientX(evt)+this.getScrollLeft();
    },
    //相对于页面的纵坐标(pageY或者是clientY+scrollTop)
    getPageY:function (evt) {
      return this.getEvent(evt).pageY?this.getEvent(evt).pageY:this.getClientY(evt)+this.getScrollTop();
    }
  };
  
  //最终的代码
  document.onmousemove=function (e) {
    my$("im").style.left=evt.getPageX(e)+"px";
    my$("im").style.top=evt.getPageY(e)+"px";
  };



//  var obj={
//    sayHi:function () {
//      console.log("考尼奇瓦");
//      this.eat();//this就是obj这个对象
//    },
//    eat:function () {
//      console.log("饭以ok,下来密西吧");
//    }
//
//  };
//  //调用sayHi方法的同时,调用eat方法,是否可以在一个方法中调用另一个方法?
//  //在对象的方法中调用另一个方法如何调用?
//
//  obj.sayHi();

</script>
</body>
</html>
```

### 拖拽案例

知识点复习：

阻止浏览器的默认事件：①return false;或 ②e.preventDefault();//IE8不支持

阻止事件冒泡：window.event.cancelBubble=true;或e.stopPropagation();

```
//获取超链接,注册点击事件,显示登录框和遮挡层
  my$("link").onclick = function () {
    my$("login").style.display = "block";
    my$("bg").style.display = "block";
  };

  //获取关闭,注册点击事件,隐藏登录框和遮挡层
  my$("closeBtn").onclick = function () {
    my$("login").style.display = "none";
    my$("bg").style.display = "none";
  };
```

### 滚动条案例

### 放大镜案例

## 直接通过document获取元素：

```javascript
//获取body
console.log(document.body);//获取的是元素--标签
//获取title
console.log(document.title);//标签中的值
document.title="嘎嘎去";
//获取html
console.log(document.documentElement);
```





## 获取元素计算后的样式属性值：为缓动动画函数服务

```javascript
//谷歌,火狐支持
//console.log(window.getComputedStyle(my$("dv"),null).left);   console.log(window.getComputedStyle(my$("dv"),null)["left"]);
//IE8支持    //console.log(my$("dv").currentStyle.left);

//获取任意一个元素的任意一个样式属性的值  
function getStyle(element,attr) {
    //判断浏览器是否支持这个方法
   return window.getComputedStyle? window.getComputedStyle(element,null)[attr]:element.currentStyle[attr];
  }


my$("btn").onclick=function () {
  console.log(getStyle(my$("dv"),"top"));
};
```



