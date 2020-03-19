一定要有**看文档**的习惯。避免**版本升级**后不懂用的情况、可以看其它配置啥的

./同级、../上级。在Node中路径是路由形式/...，不写后缀。这不一样，一定别混淆

学习基本用法，看得懂就可以了。公司不需要自己去配，因为后面的脚手架基本基于webpack去开发，如vue，它的脚手架是直接配置好的，能看得懂能调试就好了

并且一定要知道打包的目录，因为若上传到服务器上，路径都要换，注意入口和**出口的路径**。

建议经常去github上逛逛，比如搜zepto，能看到它的引入方式：下载、在哪个目录、怎么去引。

## webpack介绍

先去官网看文档，看版本、概念（官方介绍）。

> 这里讲的是4.x版本

是什么？

一个模态模块(html、js、css、image)的打包器

能干什么？

模块化打包。

> 1.网站打包成什么样？
>
> css、html、js变成一行(把多余的空格和回车都给压缩了)
>
> 去除注释
>
> 去除引号
>
> （现在很多框架都是基于webpack做的。即开发时是整洁的，开发之后就要打包成这样。）
>

## 安装

> 前提：安装了node、npm。
>
> 3.x全局安装只用npm install webpack -g
>
> 而4.x多了个cli脚手架

（1）全局安装：用npm或cnpm安装

```
//2个分别安装：
npm install webpack -g
npm install webpack-cli -g
```

```
//或2个一起安装：
npm install webpack webpack-cli -g
```

2.初始化项目，生成package.json：

```
npm init
```

进入项目目录，局部安装：会生成node_modules

```
npm install webpack -S
npm install webpack-cli -S
```

## 简单的只打包js

> 3.x版本命令: webpack a.js b.js 把a打包成b
>
> 而4.x版本中，cli（脚手架）有个
>
> 默认entry：	src/index.js
>
> 默认output：	dist/main.js

1.在项目目录下，要创建默认入口src/index.js，在入口文件写代码

2.cmd中输入**打包命令：webpack**

会自动生成默认出口

> 注意：main.js会默认变成生产环境的代码：变成一行。

从生产环境代码->开发环境代码的打包命令（也叫**未压缩打包命令）：webpack --mode development**

## webpack四大核心

四个核心概念：入口（entry）、出口（output）、loader加载程序、插件（plugins）

loader:能让webpack去打包非js文件；插件：有效地打包或压缩css、js、html、图片等。一般loader和插件配合使用

## 进行能打包js、css、html、图片等的配置

> 若看不懂在官网文档中的概念里有详细配置过程。

1.	webpack本身是打包js的，但若想要打包其它的：必须要进行相关**配置**

2. 配置：

> 先了解四个核心概念：入口（entry）、出口（output）、loader加载程序、插件（plugins）
>
> loader:能让webpack去打包非js文件；插件：有效地打包或压缩css、js、html、图片等。一般loader和插件配合使用

（1）在项目目录里命名配置文件：webpack.config.js。在里面去配置

（2）配置便捷的非压缩打包命令：

在package.json里可以去配置。配置好就可npm start或npm run start或把start换成其它的。

```
"scirpt":{	//找到改位置
	...
	"start": "webpack --mode development"	//这儿start可以随便写
},
```

（3）配置默认入口、出口。之后打包命令依然是webpack

> src:开发阶段（写代码）。里面有如index.html、index.js、style.css、1.png等
>
> public:生产阶段（项目要上线）。里面有跟上面一样文件，只不过压缩了

```
const path = require('path');

module.exports = {

	entry: './src/index.js',	//路径，可以改
	output:{
		path: path.resolve(__dirname, 'public'),	//路径，可以改
    	filename: 'bundle.js'	//打包后生成什么js
	}	
    
};
```

（4）

### 配置本地服务器

1）安装：npm install webpack-dev-server -S

2）在webpack.config.js配置：

```
const path = require('path');

module.exports = {

	entry: './src/index.js',	//路径，可以改
	output:{
		path: path.resolve(__dirname, 'public'),	//路径，可以改
    	filename: 'bundle.js'	//打包后生成什么js。这儿也可以加hash：bundle-[hash].js,给个随机hash值。但每次改动入口的.js，会重新给hash值，后面会说到插件会自动去拿hash值
	},	
    devServer:{	//配置服务器
    	contentBase:"./public",	//选择本地服务器路径
    	inline:true	//代码实时刷新
    	//post:"",	//选择端口，默认的为8080。
    	//hot:
    }
};
```

3）在package.json配置便捷的运行命令:npm dev或npm run dev。原来命令：webpack-dev-server

```
"dev": "webpack-dev-server --open --inline"	//open表示自动打开，inline表示代码实时刷新
```

4）在本地服务器目录下新建个index.html，引入出口文件bundle.js。

注意：如果要改index.html中的内容，都是**到入口文件src/index.js里改**。改完等一等，有点慢

（之前用浏览器访问是显示本地服务器的目录浏览，现在则是显示index.html）

（5）

### 配置loader	

（loader有很多，需要用时去查）loader列表：https://blog.csdn.net/keliyxyz/article/details/51649429

这儿我们要引入css文件，在index.html中写import'../css/style.css';

引入css需要style-loader和css-loader，而如果**css想引用图片**还需file-loader

1)下载：npm install style-loader css-loader -S、npm install file-loader -S

2)配置：

```
const path = require('path');

module.exports = {

	...
	module:{
		
		rules:[
			{//还可以options、结合插件去用，后面说。
				test:/\.css$/,	//打包文件的后缀。正则，\.代表转义.
				use: ['style-loader','css-loader']	//要配置全,否则无效
			},
			{
				test:/\.(jpg|png|jpeg)$/,	//打包文件的后缀,里面还可写
				use: 'file-loader'	//要配置全,否则无效
			}
		]
		
	}
};
```

配置完打包测试下。

（6）

### 配置插件

> src:开发阶段（写代码）。里面有如index.html、index.js、style.css、1.png等
>
> public:生产阶段（项目要上线）。里面有跟上面一样文件，只不过压缩了

要进行更多插件的配置，就去搜索该插件。

要打包html，就需要html-webpack-plugin。要查看更多配置https://www.npmjs.com/package/html-webpack-tags-plugin

1)下载：npm install html-webpack-plugin -S

2)配置（webpack.config.js）

```
const path = require('path');
const HtmlWebpackPlugin = require("html-webpack-plugin");	//1.引入插件

module.exports = {
	...
	plugins:[	2.写配置
		
		new HtmlWebpackPlugin({
			template:"./src/index.html"	//若无参则不会打包对应内容。模板参数
			//filename:"a.html"	//可以给过来的index.html改名称
			minify:{	//重要，缩小
				removeAttributeQuotes:true,//去除引号
				removeComments:true,//去除注释
	          	removeEmptyAttributes:true,//去除空属性
	          	collapseWhitespace:true//去除空格
			}
		})
		
	]
};
```

## 其它loader——HTML的img标记

html-withimg-loader	让html支持图片

1.下载（安装）：npm install html-withimg-loader -S

2.配置（webpack.config.js）

```
{
	test:/\.html$/,	//打包文件的后缀
	use: 'html-withimg-loader'	//要配置全,否则无效
}
```

## 字体图标和把打包文件放入文件夹

这儿我们去bootstrap拿字体图标：引入bootstrap，添加<i class="字体图标的类"></i>，然后测试下，报错，从这可以拿到字体图标常用的后缀

```
{
	test:/\.(woff|ttf|svg|eot|xttf|woff2)$/,	//打包文件的后缀
	use: 'file-loader?limit=1024&name=./fonts/[names].[ext]'	//要配置全,否则无效。加参数:先?后参数：限制大小、定义路径和名称(names代表原名,ext代表原后缀)
}
```

## 提取分离CSS

之前已经给出口文件建好了各自目录：img、js、fonts。这儿要建css。有几个坑

1.css提取

插件：extract-text-webpack-plugin

下载：npm install extract-text-webpack-plugin**@next** -S

配置：

```
...
const 	EXtractTextPlugin = require("extract-text-webpack-plugin");//1.引入

module.exports = {
	rules:[
		{//还可以options、结合插件去用，后面说。
			test:/\.css$/,	//打包文件的后缀。正则，\.代表转义.
			use:EXtractTextPlugin.extract({		//把之前的use: ['style-loader','css-loader']改了
				
				fallback:"style-loader",
				use:[{
                    loader:'css-loader',
                    options:{
                      minimize:true	//css压缩
                    }
           	 	}],
                publicPath:"../"	//测试后会发现img目录跑到css目录了，要配这个
			})	
		},
		...
	],
	plugins:[
		new EXtractTextPlugin('./CSS/[name].css'),	//2.配置1
		...
	]
};	
```

## 配置babel

核心：babel-core

功能：babel-loader

​			babel-preset-env

​			babel-preset-react	支持jsx语法

1.安装（下载）		

​	npm install babel-core babel-loader babel-preset-env babel-preset-react -S

2.配置（2种方法）

方法1：在webpack.config.js里配置（不建议。babel-loader依赖少时才这样）

```
{
    test:/(\.jsx|\.js)$/,
    use:{
      	loader:"babel-loader",
     	options:{
     		presets:["env",'react']		//添加功能
     	}
     },
     exclude:/node_modules/		//别包含：node_modules。其它的都要ES6转成ES5
}
```

方法2：（建议。因为你不知道有多少依赖要添加）

先在webpack.config.js里简单配置


```
{
    test:/(\.jsx|\.js)$/,
    use:{
      	loader:"babel-loader"
     },
    exclude:/node_modules/
}
```

还要在项目目录下新建与node_modules等同级的文件——.babelrc文件，里面配置：

```
{
	
	"presets":["env",'react']	//添加功能

}
```

## 引入第三方库文件

如jQuery、Bootstrap

1.安装：npm install jquery -S	默认下最新版，若想下其它版本，后面加个@版本号

2.引入：在入口index.js里需要引入，如写import $ from 'jquery'

## 常用loader

style-loader和css-loader	打包css

file-loader							  让css支持图片；打包字体图标

html-withimg-loader			让html支持图片

babel-loader						  把ES6转换成ES5语法

## 常用插件

html-webpack-plugin	打包html

extract-text-webpack-plugin	提取分离css