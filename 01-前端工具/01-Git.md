# 了解

- 版本控制：解决多人开发的过程，容易引起文件冲突。如svn、git

- git的优势：具有svn的功能、具有互联网的特性、git有分支概念

- git和github：
  - git客户端	github服务器端
- git可将文件提交、下载到github上。git也可独立使用

# 面试题

git 和 svn区别：

​	svn	集中式版本控制：只能从服务器拿文件

​	git	分布式版本控制：不仅可以从服务器拿文件，还可以从其他开发人员那拿文件

# 基本常用命令

> 注意：
>
> 1.一般是下班时才git commit把一天内容上传上去，上班时再下载下来。
>
> 2.想要使用，就一定要初始化该目录
>
> 3.其它常用命令可以看目录下的网页

git init	初始化

git status	查看状态

git add	添加到等待

git commit -m "注释信息支持中文"	提交

git log 查看日志

git checkout 文件名称 检出（下载）

git show 版本号

rm 文件名  ---- 删除本地文件

git rm 文件名  删除等待区域的文件

# 本地git的使用和安装

## git的安装

官网下载https://git-scm.com/downloads

## 查看版本号

测试：git --version	

## 1.创建全局的账户 和 邮箱

注意这跟github的账户无关，这是本地的。

```
git config --global user.name "用户名"
git config --global user.email "邮箱"
```

## √2.git初始化目录

想在哪个目录使用git，就在该目录cmd输入

```
git init
```

会生成 .git 隐藏目录。（.git是个局部使用的目录，只能在该初始化目录下起作用。）

## 3.配置.git创建局部账户

配置**局部账户**：

打开.git下的config，输入

```
[user]
	name=用户名
	email=邮箱
```

## √4.几个文件状态

本地文件：在**使用目录下的**文件。可以提交到内网的本地仓库。**若修改了，要重新添加提交。**

等待提交的列表：文件添加到**临时空间中**等待提交。

本地仓库：提交成功之后，会存储到git创建的**另一个目录**。（可以是自己的机器，也可以是同个路由器下的其他机器来供多人使用。）

远程仓库：github（官方提供的远程服务器）。前提：提交到本地仓库的东西才能推送到github

## 5.查看文件状态

> 一般不在cmd中写，而是在git bash中写

右击使用目录，在git bash中输入。

```
git status
```

**反馈结果说明：**

反馈	状态

红色	未添加提交、修改了

绿色	在等待提交列表中

不显示	提交到本地仓库了	

# 上传(6-8)

工作目录下的所有文件只要有改动都需重新上传

## 6.添加到等待提交列表

```
git add 文件名
```

## 7.提交到本地仓库

注意：一般情况下，下班的时候再把一天内容提交上去

```
git commit -m "注释信息支持中文"
```

## √8.查看工作日志

查看谁什么时间干了什么事：上传账户、上传时间、注释。

# 下载

## 9.下载最新版本(误删还原)

一般也叫检出

```
git checkout 文件名
```

##  10.查看某一版本

先到git log	复制对应的版本号(commit 后的**前几位**即可，不重复就行：如6)。再输入(粘贴版本号时不会显示，直接回车)

```
git show 版本号
```

就会显示出该版本的**详细信息**。

## 11.删除本地文件

```
rm 文件名
```

## 12.删除等待区域文件

```
git rm 文件名
```

# 分支(团队用)

master表示主分支

注意：

没做任何操作前，默认主次分支的git log是一样的。

做了操作则主次分支的git log不一样。

## 查看分支

```
git branch
```

## 创建分支

```
git branch 分支名
```

## 切换分支

```
git checkout 分支名
```

## 合并(子)分支

切换到主分支下，才能合并。是指文件合并到一起，子分支就没用了。

```
git merga 子分支名
```

## 删除分支

```
git branch -d 子分支名
```

# git远程操作github服务器

先需要到github注册账户

## 创建远程仓库

登陆github，点击右上角＋，创建新项目。

输入项目名、项目描述、选择公开或私有即可。

**注意：**会生成一个链接(有https或ssh两种形式)，用来本地访问github的**这个仓库**。

## 本地仓库关联远程仓库

创建个仓库目录，推送前先记得初始化该目录：git init。否则会显示错误：fatal: Not a git repository (or any of the parent directories): .git

给本地仓库添加远程仓库的源地址，来关联远程仓库：git remote add origin 某远程仓库地址。

## 推送到远程仓库

```
git push -u origin master 
```

执行之后会让输入github账户密码，稍等即可。

## 加载到本地

点开仓库，仓库的克隆或下载选项下有地址，建议使用**http地址**。输入

```
git clone 远程仓库地址
```

# git错误提示

fatal: Not a git repository (or any of the parent directories): .git

原因：没有初始化git本地版本管理仓库，所以无法执行git命令

解决方法：git init，然后执行一下git status查看状态信息，good，问题解决。

# 其他操作

## 更改用户名

起名建议：名姓

右上角下拉中选setting，选择account，change your username。
