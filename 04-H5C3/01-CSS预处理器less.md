less的官方中文网：http://lesscss.cn/

# 什么是css预处理器

- 扩展了 CSS 语言——包含了变量，运算，函数
- 使 CSS 更易维护和扩展。

应用场景：如换主题样式

# less简介

1、less的官方中文网：http://lesscss.cn/

2、less语法：

​		变量:   `@变量名:值;`

3、注意：

​		虽然浏览器支持 .less 文件,但是**less文件中写入变量...就不支持了**,必须要把.less文件编译成.css文件

# less编译方式

> 编译方式有很多，推荐前2者：node、工具、.js文件

## node方式

1. 全局安装less：

   ```
   npm install -g less
   ```

2. 创建、编写 .less 文件

3. 每次编写后，到所在位置，编译成 .css 文件。（注意之后的html中**要引入的是 .css**）

   非压缩版本:

   ```
   lessc styles.less styles.css
   ```

   压缩版本：

   ```
   lessc -x style.less style.css
   ```

## 工具方法

1. 下载工具：如[Koala（考拉）](http://koala-app.com/index-zh.html)（可无脑下一步，设中文、要重启）
2. 创建、编写 .less 文件
3. 拖放**目录**到 Koala，然后点击 Refresh(编译)，就会生成在目录里生成.css。（然后编写.less时，.css会监听、自动编译，不需要再重新编译了）（注意：目录不能有中文，会报错）
   - 默认为非压缩版
   - 压缩版：左击 .less 文件，选输出方式为compress，执行编译
4. 在html中引入 .css文件

# less基本语法

> 1、基本语法：变量、运算、自定义函数、嵌套、用&写伪类
>
> 2、它的引入跟css的一样：
>
> ```
> @import "a";	//library.less
> @import "b.css";
> ```

- 变量——`@变量名:值;`

- 运算：有＋- * /，如

  ```
  div {
  	width:300px-100;	
  }
  ```

- 自定义函数

```
.函数名(形参){//定义,传参。可以有默认值，如.fn(@fz:20px){}

}
.函数名(实参)	//调用
```

如：

```
.fn(@fz){
	font-size:@fz;
}
div {
	.fn(200px);
}
```

- 嵌套，如

```
场景：
<ul>
	<li><span><span></li>
</ul>
正常情况要：
ul {}
ul li {}
ul li span {}
叠加就可以在.less中写：
ul {
	list-style: none;
	li {
		color: orange;
		span {
			display: block;
		}
	}
}
```

- 用&写伪类，如在.less中写

  ```
  a {
  	&:hover {
  		font-size: 50px;
  	}
  }
  编译成.css后：
  a:hover {
  	font-size: 50px;
  }
  ```

  