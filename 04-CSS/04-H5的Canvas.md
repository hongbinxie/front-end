# canvas是什么

- 是一个html5新增的**标签**
- 是一个**画布**，可以**通过js的api**去画（添加图案）

# canva的使用场景

- 做游戏
- 画图案
  - 如做图表：业绩报表

# canvas的基本使用

> 注意：
>
> - canvas有默认大小：宽300、高150，可设置。
> - canvas的宽度和高度，一般都在js中定义
> - 如果在css中定义宽度和高度，内部元素也会受到影响
> - 建议打印看一下canvas对象的属性、方法

1.  `<canvas></canvas>`（建议给个id、类，好操作它）
2. 通过JS去操作，获取它
3. 创建一个2d、3d对象
   1. 2d对象：方法`getContext("2d")`
   2. 3d对象：需要插件的支持
4. 绘画

```html
<style>
	#myCanvas{
		border:1px solid red;
	}
</style>
<body>

<canvas id='myCanvas'></canvas>

<script>
var myCanvas = document.getElementById("myCanvas");
var cvs = myCanvas.getContext("2d");

cvs.fillStyle='blue';	//填充物颜色
cvs.fillRect(20,10,100,100);//填充物的位置、大小：从左上开始，x、y、宽、高
</script>
</body>    
```

# canvas-矩形（有填充、无填充）

- 有填充
  - 2d对象.fillStyle=''	        ===》填充颜色
  - 2d对象.fillRect(x,y,w,h)   ===》位置、大小
- 无填充（不能填充颜色）
  - 2d对象.StrokeStyle=''	         ===》线条颜色
  - 2d对象.StrokeRect(x,y,w,h)    ===》位置、大小

# canvas-线

	1>起始点：2d对象.moveTo(x,y);	//坐标
	2>结束点: 2d对象.lineTo(x,y);
			 ....			   //接下来就可无限lineTo了
	3>开始画：2d对象.stroke()	   //执行到这才会去画
	辅助：
	    线条加粗 :  2d对象.lineWidth = 5
	    线条颜色 :  2d对象.strokeStyle='red'
	    填充颜色 :（与矩形不同，要2步）
	        2d对象.fillStyle='red'
	        2d对象.fill() ==》加入此方法才可以填充
到这就可以完成很多东西了，如箭头等。不过学了下一节，有个注意点、画线更容易的方法。

## canvas-beginPath、closePath

> 画线会出现个问题：当你分别画了几条线，后画的线的颜色会影响前面的线。解决：用beginPath()可以解决

- 2d对象.beginPath()	**重置**当前的路径，或**开始**一条路径。
- 2d对象.closePath()    创建从**当前点**到**开始点**的路径。注意要放在stroke()之前才起效！

# cavas-arc()弧度

```
2d对象.arc()

2d对象.arc(x,y,r,sAngle,eAngle,counterclockwise);
开始画：2d对象.stroke()	//这儿才开始画

	x:横向位置
	y:垂直位置
	r:半径
	sAngle:起始点，注意：这里是与x轴的度数，0是x轴正方向
	eAngle:结束点。如1*Math.PI
	counterclockwise:方向	
        false ==>顺时针（默认为顺时针）
        true  ==>逆时针（注意：跟顺时针画出的弧度相反）
```



