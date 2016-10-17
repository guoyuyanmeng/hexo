---
title: pods项目之git版本管理
---
date: 2016-06-14 11:23:07

cocoapods是和方便的第三方库托管插件，使用cocoapods可以让我们节省很多枯燥的工作，但是在git中有时候会很烦人，xcode一遍一遍的提示UserInterfaceState.xcuserstate有未提交的change ，这时候就需要用git 中的.gitignore  来处理了。

---

## pods 安装库

（如果你的mac还没有安装cocoapods ---> [cocoapods安装](http://blog.csdn.net/guoyuyanmen/article/details/50638754)）
打开终端，cd 进入项目文件夹

```
//生成Podfile文件
touch  Podfile 

//打开Podfile文件，编辑支持版本和需要引入的三方库
vim Podfile
```
例如下图
![这里写图片描述](http://img.blog.csdn.net/20160603174144240)

编辑完Podfile文件，执行安装库命令

```
pod install
```
提示pods installed.表示安装成功

```
Analyzing dependencies
Downloading dependencies
...
Installing MBProgressHUD (0.9.2)
...
Generating Pods project
Integrating client project
Sending stats
Pod installation complete! There are 14 dependencies from the Podfile and 15
total pods installed.
```
这时候打开finder可以看到在工程下面多几个文件
yourProject.xcworkspace
Podfile
Podfile.lock
Pods文件夹

这些文件都是什么呢?Podfile不用说，就是上面我们手动生成的pods配置文件，下面我们说说其他几个文件

---
##  Podfile.lock

> This file is generated after the first run of pod install, and tracks
> the version of each Pod that was installed.

说白了就是首次执行 pod install的时候回自动生成Podfile.lock文件，并且能够追踪当前安装pods库的版本信息。如果你的工程导入到另外一台机器上，执行pod install 命令，即便当前某一个pods新的可用版本，pods库也不会跟新版本，还是会安装和原来的机器一样的版本号，这个就能够保证多人开发的时候保持依赖库一致，因此，Podfile.lock文件在git版本管理中不能被忽略。

> This file should always be kept under version control.

---
## pod文件夹
pod文件夹存放依赖库，并且记录pods依赖库当前安装的信息和一些配置。cocoapods官方推荐对pods文件夹做版本控制，但是也没有强烈推荐，还是看个人选择，各有优点吧。如果做版本控制，git clone 完代码也不用重新安装pods依赖库，直接可以编译运行，节省时间，同时计时依赖库在资源网站上下架也可以继续使用；如果不做版本控制，可以节省空间，节省代码同步的时间，可以减少合并分支的冲突。

> Whether or not you check in the Pods directory, the Podfile and
> Podfile.lock should always be kept under version control.

不论pods文件夹做不做版本控制，对于podfile和podfile.lock你都应该做版本控制

---
##  yourProject.xcworkspace

yourProject.xcworkspace文件是pods管理的xcode项目的程序入口，这个文件里面有一个文件UserInterfaceState.xcuserstate，总是提示有未提交的change ，很讨厌，所以我们把UserInterfaceState.xcuserstate放到.gitignore中，也就是不做版本控制。
首先添加UserInterfaceState.xcuserstate的路径到.gitignorewen中
然后先清除缓存，提交

```
$ git rm --cached yourProject.xcworkspace/xcuserdata/username.xcuserdatad/UserInterfaceState.xcuserstate

$ git add .

git commit -m "fixed untracked files"

```
