# 前端工具推荐

 浏览器：chrome、火狐

编辑器：sublime

切图工具：photoshop、firework

# 浏览器

浏览器是网页显示、运行的平台。

- 五大常用浏览器：

IE、火狐（Firefox）、谷歌（Chrome）、Safari、Opera。

- 常见的浏览器内核：

Trident、Gecko、Blink、Webkit。

> Trident（IE、很多国内浏览器内核）
>
> Gecko（Firefox内核）
>
> webkit（Safari苹果浏览器、以前的chrome内核）
>
> Chromium/Blink（chrome内核，是webkit的二次开发）
>
> 安卓、苹果手机：webkit内核
>
> WP7手机：Trident

# html转义符

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/html%E8%BD%AC%E4%B9%89%E7%AC%A61.png)

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/html%E8%BD%AC%E4%B9%89%E7%AC%A62.png)

# web标准

> 出现原因：各浏览器内核不同，工作原理、解析也就不同，导致显示上会有差异，所以代码要符合Web标准。

组成：结构、表现、行为。

- 结构：有哪些内容。主要用HTML
- 表现：内容的外观样式，主要用CSS
- 行为：内容的交互，主要用JavaScript

# html骨架

```
<html>
	<head>
		<title></title>
	</head>
	<body>
		...
	</body>
</html>
```

# 注释

```
HTML的单行、多行注释：<!-- -->	
CSS的单行、多行注释：/* */
JS单行注释：//
JS多行注释：/* */
```

# html标签

## 参考

（不懂时可查）

W3C : http://www.w3school.com.cn/

MDN: https://developer.mozilla.org/zh-CN/

## 注意事项

- 标签的属性值：用" "括起，不加单位！
- 尽量不使用 样式属性！
- 表格不是用来布局，常用于  处理、显示表格式数据

## 了解

### 标签语义化

即在合适的地方放上合适的标签。

遵循原则：先确定语义的HTML ，再选合适的CSS。

> 原因：
>
> 1. 方便代码的阅读和维护
> 2. 同时让浏览器或是网络爬虫可以很好地解析，从而更好分析其中的内容 
> 3. 使用语义化标签会具有更好地搜索引擎优化

### 标签的关系

有2种：

父子关系（嵌套）、兄弟关系（并列）

### 标签的分类

有3种分类方式。

- 有无 **语义**
  - 有语义标签（元素）：骨架结构标签；排版标签h,p,hr,br；文本格式化标签；图像标签img；链接标签a，base；特殊字符标签；列表标签；表格标签；表单标签共9种
  - 无语义标签（div、span）：块级标签。一般：需要一行只放一个元素用div，需要一行放好几个元素用span
- 是否 **成对**
  - 单标签有：hr、br、img、base、meta、input
  - 其余为双标签

- 按 **显示模式** 分：块、行、行内块

### 块标签

- 常见：h、p、div、ul、ol、li
- 作用：常用于搭建网页**布局、结构**。
- 特点：
  - 每个块标签单独占据一整行或多整行
  - 可设置宽、高、对齐、内外边距等属性。
  - 默认宽度：容器的100%
  - 容纳内联标签、其他块标签（p、h文字类块标签不能放块级元素）
  - 不可以看作文本

### 行内标签

> 也叫内敛标签。

- 常见：a、strong、b、em、i、del、s、ins、u、span

- 作用：常用于  控制页面中**文本样式**。

-  特点：
  - 不占有独立的区域：和相邻行内元素在一行上。
  - **靠本身内容**来支撑结构：高、宽、对齐等属性无效，只**水平方向的padding、margin**有效
  - 默认宽度：本身内容  的宽度
  - 容纳文本、其他行内元素（a特殊，但a里不能放a）
  - 可以看作文本

### 行内块元素

特殊的行内元素

- 常见：img、input 、td
- 特点：
  - **主要特点：可以对它们设置宽高、对齐、外内边距等**
  - 和相邻行内元素（行内块）在一行上,**但是之间有空白缝隙**
  - 默认宽度：本身内容  的宽度。
  - 可以看作文本

## 具体内容

### 骨架结构标签

主要

- html：文档根
- head：文档头部(描述文档信息，必须有title)
- title：文档标题
- body：文档主体(存放页面内容)

补充：

```
<!DOCTYPE  html>	文档类型
<meta  charset="utf-8">    字符集属性（通常使用UTF-8 字符集）
注释    ``
```

### 排版标签h,p,hr,br

h:	页面标题（块级标签。 h1:只给logo、页面中最重要标题信息用。h1-h6：尺寸从大到小，  权重从高到低）

p:	段落（块级元素。会根据浏览器窗口的大小 自动换行。不要用p标签来插入空行）

hr:	水平线。（单标签）

br:	换行。（不要用br标签创建列表）

### 文本格式化标签

b、strong	粗体（强调时才用后者）

i、em	斜体（强调时才用后者）

s、del	删除线（强调时才用后者）

u、ins	加下划线（强调时才用后者）

### 图像标签img

img的属性：

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/imgAtt.png)

### 链接标签a、base

| 标签名    | 作用                   | 属性                                                         | 注意                               |
| --------- | ---------------------- | ------------------------------------------------------------ | ---------------------------------- |
| a         | 链接                   | href：指定链接的地址（href="#"表示空链接）                                                                target：链接目标的弹出方式（常用值：*blank、*self；                                                  name：规定锚的名称。（可用 name 属性创建 HTML 页面中的**书签**。用#来跳转到name同名位置） | 锚点定位（做书签）的方法           |
| <base  /> | 设置整体链接的打开状态 | target：链接目标的弹出方式（常用值：*blank、*self；          | 在head部写。优先级比标签自身属性低 |

**锚点定位**                                                                

通过创建锚点链接，用户能够快速定位到目标内容。   

步骤1：创建锚点（被点击的）

```
<a  href="#id名">锚点文本</a>
```

步骤2：（使用锚点的id名）设置定位目标

```
 <h3 id="two">第2集</h3>    
```

### 特殊字符标签

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/zifu.png)

### 列表标签

无序列表：ul、li

有序列表：ol、li

自定义列表：dl、dt名词、dd名词解释（列表项前没有任何项目符号）

自定义列表常用来：

<img src="https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/dl-Exa.png"/>

### 表格标签

> 注意：表格不是用来布局，常用于  处理、显示表格式数据

有以下标签：table表格、thead标题区域、tbody表主体区域、caption表格标题、tr表行、th表头、td单元格

用法：

```
<table>
	<thead>
		<caption>...</caption>
	</thead>
	<tbody>
		<tr>
			<th>...</th>
			<td>...</td>
			<td>..</td>
		</tr>
		<tr>
			<th>...</th>
			<td>...</td>
		</tr>
	</tbody>
</table>
```

表的属性：

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/tableAtt.png)

**合并单元格（重点）**

跨行合并：rowspan 

跨列合并：colspan

### 表单标签

> 注意：每个表单都应该有自己的表单域。

标签：

| 标签名     | 作用           | 具体、属性、注意                                             |
| ---------- | -------------- | ------------------------------------------------------------ |
| <from>     | 表单域         | 建一个表单，以实现用户信息的收集和传递，form中的所有内容都会被提交给服务器。                                                                                                                                  格式：<form  action="提交的地址" method="提交方式" name="表单名称">   各种表单控件  </form>                                                                                                                              提交方式：get公开、post安全性高。 |
| <input  /> | 输入框控件     | input：image图片按钮                                         |
| **label**  | 为控件定义标注 | 用于绑定一个表单元素, 当点击label标签的时候, 被绑定的表单元素就会获得输入焦点 |
| textarea   | 文本域控件     | 用来输入大量的信息。直接给宽、高，不要用属性：cols、rows。   |
| select     | 下拉菜单       | 注意：                                                                                                                                           1.<select></select>中至少应包含一对<option></option>。                                                             2.在option 中定义selected =" selected "时，当前项即为默认选中项。 |

input属性：

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/inputAtt.png)

# 🔺常用技巧

## 锚点定位（做书签）                                                                

通过创建锚点链接，用户能够快速定位到目标内容。   

步骤1：创建锚点（被点击的）

```
<a  href="#id名">锚点文本</a>
```

步骤2：（使用锚点的id名）设置定位目标

```
 <h3 id="two">第2集</h3>    
```

# icon图标

网页标题中的图标

- 使用icon图标

  1.先保存到根目录中

  2.在html中的head中输入

  ```
  <link rel="shortcut icon" href="favicon.ico" type="image/x-icon"/>
  ```

  type可以省略

- 如何拿到别人的icon图标

  打开域名/favicon.icon，另存为图片，名字不要改，保存到根目录

# 图标字体

> 电脑中字体一般放在C：//windows/fonts中
>
> UI人员怎么设计的图标字体？
>
> - 用矢量图形软件：illustrator、Sketch 
> - 在软件里创建 icon图标，保存为svg图给前端。
> - 前端把图（上传到某些网站或自己转换）转换成兼容性图标字体

网页设计中特殊的字体

- 特点：

  - 本质仍是文字，可以很随意的改变颜色、产生阴影、透明效果等
  - 可以做出跟图片一样可以做的事情,改变透明度、旋转度等

## 怎么使用

> 注意：icomoon文件夹不能丢

1. 拿图（从网上、UI设计师那。若是svg格式，转换成字体：上传到某些网站转换   或  自己转换）

2. 引入

   1. 把fonts文件夹放入网站目录中。

   2. 在样式里声明字体：粘贴固定的格式

   3. 先复制fonts目录下的demo.html中图标字体下的方框图片或

      代码如i::before{content:       "\e900";}，

      再给标签使用字体font-family。

3. 怎么追加新图标到原来的库里面？

把原icomoon文件夹里面的selection.json 重新上传，选yes。

然后，选中新图标，重新下载压缩包，替换原来文件即可。

## 推荐网站

1.推荐网站： http://icomoon.io

**icomoon**字库 **最提倡使用！**

IcoMoon成立于2011年，推出的第一个自定义图标字体生成器，它允许用户选择他们所需要的图标，使它们成一字型。 内容种类繁多，非常全面，唯一的遗憾是国外服务器，打开网速较慢。

使用：①点iconmoon app

②

![](https://raw.githubusercontent.com/hongbinxie/pic-bad/master/img/iconfont1.png)

2.推荐网站： http://www.iconfont.cn/

**icon font字库**

http://www.iconfont.cn/

这个是阿里妈妈M2UX的一个icon font字体图标字库，包含了淘宝图标库和阿里妈妈图标库。可以使用AI制作图标上传生成。 一个字，免费，免费！！

**fontello**

http://fontello.com/

在线定制你自己的icon font字体图标字库，也可以直接从GitHub下载整个图标集，该项目也是开源的。

**Font-Awesome**

http://fortawesome.github.io/Font-Awesome/

这是我最喜欢的字库之一了，更新比较快。目前已经有369个图标了。

**Glyphicon Halflings**

http://glyphicons.com/

这个字体图标可以在Bootstrap下免费使用。自带了200多个图标。

**Icons8**

https://icons8.com/

提供PNG免费下载，像素大能到500PX