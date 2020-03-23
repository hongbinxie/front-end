sass中文官网https://www.sass.hk/

# 什么是css预处理器

- 扩展了 CSS 语言——包含了变量，运算，函数
- 使 CSS 更易维护和扩展。

应用场景：如换主题样式

# sass和scss的区别

1、sass语法：书写格式不好——没有花括号、分号，如

```
div		
	background: red
```

2、scss语法：书写格式良好——跟正常css一样

3、所以注意：以后**创建的是 .scss 文件**，不是 .sass文件

# sass的编译方式

## node编译

> sass中文官网https://www.sass.hk/

1、windows系统必须安装ruby，而mac自带：去百度随便下载即可，国外的下载慢。（测试：ruby -v）

2、命令（到所在位置编译）

安装sass：`gem install sass`
普通编译：`sass style.scss style.css`
压缩版编译：`sass --style compressed style.scss style.css`
监听:`sass --watch style.scss:style.css`（监听后编写.scss后，编译的.css里会自动编译）

## 工具编译

Koala工具的用法跟less一样（注意：目录不能有中文，会报错）

注意：编译的输出方式**设为expanded**，才为css标准格式

# 基本语法

> 跟less用法类似

- 变量：`$变量名称:值`

- 运算：+ - * /

- 嵌套。包括以下情况也支持

  ```
  正常：
  div {
  	border-top: 1px solid #ccc;
  	border-bottom: 1px solid red;
  }
  .scss中可写：(注意“:”别漏)
  div {
  	border: {
          top: 1px solid #ccc;
          bottom: 1px solid red;
  	}
  	
  }
  ```

- &写伪类：如`&:hover{}`

- 自定义函数:

```js
@function 函数名(){	//也可传值、可设默认值。需要返回结果
    //@return;			
    //@return 一个结果;
}
函数名()
```

支持的很多，如判断、循环，可以到sass中文官网https://www.sass.hk/去看

# sass和less的区别

1. 语法不同
2. 基于的语言不同
   	less ——》 JavaScript
   	sass ——》 ruby