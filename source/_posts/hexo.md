---
title: gitee及hexo搭建教程
from: hexo
url: 'https://fadeway32.gitee.io/'
author: fadeway32
about: blog/wiki
avatar: 'https://gitee.com/fadeway32/fadeway32/raw/master/img/F35AB4B62DEAE3B5DC2907087E35424E.png'
comments: true
tags: web
categories: Web
description: gitee及hexo搭建教程.
type: hexo
path: /article/hexo
abbrlink: 1305786659
date: 2023-09-01 00:00:00
top: 103


---




## 前言  

​        博客是一个自己积累和记录知识的平台，有很多人想要建立自己的博客，折腾来折腾去的，最后却只能在**博客园**或**简书**上发表文章。

​    有很多人选择把博客建在**Github**、**gitte**上，这是一个开源代码托管网站，我也把我的博客建在了GitHub上。当初我还为了用哪个博客框架而烦恼呢，因为有很多有名的开源博客框架，比如**Hexo、WordPress、VuePress、Halo \**等，wordpress是动态博客框架所以不能建在GitHub上，相比较剩下三种，我选择了\**Hexo**。

​    这里介绍了hexo和gitee的搭建方式：

## 一、环境准备



### 1.1、安装NodeJs

因为Hexo是基于NodeJs的，所以需要安装NodeJs。

去[NodeJs官网](https://nodejs.org/zh-cn/)下载长期支持版，然后打开安装程序，安装选项全部默认，一路点击`Next`。

安装好了之后，打开cmd输入`node -v`，如果显示的是下载的版本号那就是安装成功了。
![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/d6e40115252c48ecaa7ed8704b1781b7.png)

### 1.2、安装Git

​    打开[Git官网的下载地址](https://git-scm.com/downloads)，点击Download for Windows，就可以下载了。

然后打开安装程序，安装选项全部默认，一路点击**Next**。

安装完成后打开cmd，输入`git --version`检查安装，如果显示的是当前git的版本号，那就是安装成功了。
<div align="left">
<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/c08d0339b15e3f7d2b381453f226b638.png" alt="检查安装" style="zoom:100%;" align="left" />
</div> <br />




### 1.3 注册gitee账号及开启仓库

   登录gitee，需要开启page服务，需要上传身份信息,然后设置仓库地址为开源

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/17957899-9026a8fa7da82bf6.png)

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/QQ截图20230220092730.jpg)

### 1.4 图床搭建

 下载picGo https://kgithub.com/Molunerfinn/PicGo/releases/tag/v2.3.0

![image-20230220093012184](https://gitee.com/fadeway32/fadeway32/raw/master/img/202302200930957.png)

配置连接gitee参考

<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/202302200931846.png#p" alt="image-20230220093107098" align="left" style="zoom:100%" />

测试上传是否成功

### 1.5 typora md文档下载

typora 工具下载：https://ghpym.lanzoui.com/b00zng7gd

## 二 选择hexo主题



hexo官网地址:    https://hexo.io/zh-cn/

进行npm-install/或者yarn 

![image-20230220093725590](https://gitee.com/fadeway32/fadeway32/raw/master/img/202302200937199.png)

## 三  hexo语法学习、md文档语法学习

hexo语法学习：https://hexo.io/zh-cn/docs/commands.html

#### 3.1几个hexo常用的命令

Hexo常用命令详解
1、hexo init

```java
 hexo init 命令用于初始化一个本地文件夹为网站的根目录
```

2、hexo new

```
hexo new 将页面新建
```

3、hexo generate

```
$ hexo generate 可以简写成 hexo g
该命令用于生成静态文件
```

4、hexo server

```java
$ hexo server 命令用于启动本地服务器，一般可以简写成 hexo s
可以加一些参数
-p    选项，指定服务器端口，默认为 4000
-i    选项，指定服务器 IP 地址，默认为 0.0.0.0
-s    选项，静态模式 ，仅提供 public 文件夹中的文件并禁用文件监视
```

5、hexo deploy

```
$ hexo deploy 命令用于部署网站，一般可以简写成 hexo d
```


6、hexo clean

```
$ hexo clean 命令用于清理缓存文件，是一个比较常用的命令
```


7、hexo --safe

```
$ hexo --safe 表示安全模式，用于禁用加载插件和脚本
```


8、hexo --debug

```
$ hexo --debug 表示调试模式，用于将消息详细记录到终端和 debug.log 文件
```


9、hexo --silent

```
$ hexo --silent  表示静默模式，用于静默输出到终端
```

#### 3.2 md工具地址下载

typora 工具下载：https://ghpym.lanzoui.com/b00zng7gd

#### 3.3 md语法使用



```

**1.标题**

\# H1
\## H2
\### H3
\#### H4
\##### H5
\###### H6
（注意：#号和文字间至少得有一个空格）

同时H1和H2还有另一种写法

H1
=====
H2
\-------
```
（注意：这里“=”和“-”的个数也至少有一个，但要紧随文字下一行）

看效果图↓
<div align="left">
<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220225638.png"></img>
</div>
###  **2.列表**

 无序列表使用星号、加号或是减号（* +  -）作为列表标记：

直接看图↓
<div align="left">
<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224125.png"/>
</div>
有序列表则使用数字接着一个英文句点：
<div align="left">
<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224215.png"/>
</div>
 

 组合使用
<div align="left">
<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224244.png"/>
</div>
 

###  **3.文本强调**

Markdown 使用星号（`*`）和底线（`_`）作为标记强调字词的符号，被 `*` 或 `_` 包围的字词会被转成用 `<em>` 标签包围，用两个 `*` 或 `_`包起来的话，则会被转成 `<strong>`

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224323.png)

删除线~~，用两个波浪线包裹

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224356.png)

 

###  **4.代码及区块说明**

细心的小伙伴已经可以看到上面用的>，大于号，就是区块说明

代码块就是 ` 反引号包裹

<img src="https://img2018.cnblogs.com/blog/1643404/201905/1643404-20190527114656686-797027325.png" align="left">

大量代码块```三个反引号包裹

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224436.png)

 

###  **5.链接及图片引用**

Markdown 支持两种形式的链接语法： 行内式和参考式两种形式。不管是哪一种，链接文字都是用 [方括号] 来标记。

1.行内式：只要在方块括号后面紧接着圆括号并插入网址链接即可，如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224503.png)

 

2.参考式：在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记

 ![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224540.png)

3.图片，也是分为行内式和参考式

!![图片文字](url)  与链接一样只是在开头多了个！

 ![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224615.png)

 

###  **6.分割线**

 分割线可以由* - _（星号，减号，底线）这3个符号的至少3个符号表示，注意至少要3个，且不需要连续，有空格也可以

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224724.png)

### **7.表格**

 用:的不同位置来改变对齐方式，默认左对齐(:-)，右对齐(-:)，居中对齐(:-:)

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224752.png)

 还可以简写

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224849.png)

 

### **8.目录**

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230220224912.png)

点击  1.第一章  浏览器就会滚动的  第一章  上

 

**转义：**

 Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

```java
\   反斜线
`   反引号
*   星号
_   底线
{}  花括号
[]  方括号
()  括弧
#   井字号
+   加号
-   减号
.   英文句点
!   惊叹号
```

然后就可以记录自己的博客

