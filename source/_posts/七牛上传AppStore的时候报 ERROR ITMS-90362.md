---
title: 七牛上传AppStore的时候报 ERROR ITMS-90362
---
date: 2016-05-27 21:25:07 

程序员日常加班写代码，加班调bug，加班发版本。
刚刚发版本的时候就遇到了七牛的迷之ITMS-90362 bug，强制要求使用ios 8.0，不然appstore 就会报错。

---

![上传报错图片](http://img.blog.csdn.net/20160527210854906)

bug背景，项目需要用到七牛框架上传视频，且只能用pods 安装。。。我们项目最低版本支持到7.0,所有工作完成以后上传app到AppStore的时候就会报错。
 为了快速发版，赶紧联系七牛的大牛来解决问题，最终提供一下方案：

### 1. 修改项目中用pods安装库的支持版本，与项目支持版本号保持一致。

![这里写图片描述](http://img.blog.csdn.net/20160527211653551)
修改完成之后重新编译，打包上传，发现然并卵。。。

### 2. 修改app支持版本号
![这里写图片描述](http://img.blog.csdn.net/20160527211931395)

修改完成后重新打包上传，虽然成功了，但是并不感到高兴。

### 3. 修改pods 配置文件Podfile
![这里写图片描述](http://img.blog.csdn.net/20160527212446850)
 如果Podfile文件里面使用了useframework命令的话，先删除useframework，然后 在 终端pod update重新配置pods的三方库，重新编译上传，不知道会不会成功。。。因为我一直用了本方法已经上传了，但还是记录下来吧。