# vgo简明教程(Go语言依赖包管理工具)

## 前言

vgo是Go语言推出的第三方库管理工具，即将在Go语言新版本中使用。  

相信大家都接触过其它语言的第三方库管理工具，比如Java的maven，PHP的composer，Python的pip，Node的npm等。vgo类似于这样的功能，方便Go语言项目管理第三方库。  

Go语言官方以前一直没有明确正式的包管理工具，因此导致包管理工具非常混乱，比如dep，glide，govendor，godep等。(虽然dep也是Go语言官方推出的，但是它最终会被放弃。)  
vgo的推出，是Go语言社区的需要，将解决包管理工具混乱的问题。Go语言官方将使用这个依赖工具为主，所以我们有必要提前了解一下它的使用。  

(vgo即英文versioned go的缩写)

## vendor目录

vendor目录是Go1.5版本后添加的依赖包管理目录。  
依赖包目录搜索顺序：vendor目录 -> GOROOT -> GOPATH

## 安装

> 说明：Go新版本中会直接使用vgo，但目前Go新版本还没有推出，为了提前了解和使用，需要另外安装。

### 源码安装

#### 无墙或可跳墙的方案(快速)

运行命令`go get -u golang.org/x/vgo`  
二进制文件会自动生成在GOPATH的bin目录下，如果你的GOPATH的bin目录没有在环境变量中配置，你需要将vgo二进制文件复制到你的环境变量路径里(方便任意目录下命令行可直接输入`vgo`来使用)。

#### 无法跳墙的方案

在GOPATH下的目录层次src/golang.org/x(没有哪个层次就创建哪个层次，因为vgo的包名是golang.org/x/vgo)，然后在x目录下使用git克隆vgo仓库`git clone github.com/golang/vgo`，进入vgo目录运行命令`go build main.go`，最后将生成的vgo二进制文件复制到你的环境变量路径里(注意vgo二进制文件的命名：Windows系统是vgo.exe，Mac或Linux是无后缀的vgo)。

> 此方法也是一些国内被墙掉的Go包常用的技巧方法，顺便提一下。

## 如何使用？

### 1、项目目录下的go.mod文件

go.mod文件像Java maven的pom.xml文件，PHP的composer.json文件，就是依赖的配置文件。  

`切记，go.mod文件至少要有 module 字段！！！`  
(提示：为了这个，有些人还在main包使用注释`package main // import "xxx"`语句来生成，其实你只要在go.mod文件指示这个项目的包路径就可以了，可以不要注释了。)  

go.mod文件常用字段：  
module 指示这个项目的包路径  
require 必须依赖  
exclude 排除依赖  
replace 替换依赖  

### 2、常用命令

`vgo version`查看vgo版本  
`vgo install`安装依赖  
`vgo build`编译项目  
`vgo run`运行项目  
`vgo get github.com/gin-gonic/gin`获取依赖包的最新版本  
`vgo get github.com/gin-gonic/gin@v1.2`获取依赖包的指定版本  
`vgo mod -vendor`将依赖包直接放在项目的vendor目录里  

更多命令请使用`vgo help`来查看。  

获取的依赖包数据会缓存到GOPATH路径下的src/mod目录里。  

## 举例说明

这里有一些vgo使用的例子：<https://github.com/wuyumin/vgo/tree/master/examples>  
比如最简单的hello目录，你在该目录下运行`vgo build`可以直接生成二进制文件。你可以查看一下go.mod文件的简单写法。


## 参考资料

- vgo进入Go语言仓库的commit：<https://github.com/golang/go/commit/5756895877492e3427c92e9ec8784eb1f4b01474>
- vgo仓库：<https://github.com/golang/vgo>
- vgo设计理念(英文，有墙)：<https://research.swtch.com/vgo>

## 修正建议

由于vgo目前是实验阶段，有些内容可能会有变化，我们会随时关注及更新本文，也欢迎大家使用GitHub来协作。  

GitHub上的原文链接：  
<https://github.com/wuyumin/vgo/tree/master/docs/zh-CN.md>  
欢迎在GitHub上star本项目进行协作或通过Issues提供修正建议。  
