
---
title: Xcode编译Erroe ----Undefined symbols for architecture
---
date: 2016-06-03 16:53:00

---
##  Xcode build的时候报错

```
 Undefined symbols for architecture arm64:
 ...
 "_OBJC_CLASS_$_AFHTTPRequestOperationManager", referenced from:
_OBJC_CLASS_$_AppDelegate in AppDelegate.o
"_OBJC_CLASS_$_AFHTTPResponseSerializer", referenced from:
objc-class-ref in AppDelegate.o
...
```
---
在cocoapods管理第三方的时候经常遇见，很烦人，解决办法有一下几种：


### 1、检查库文件是否导入
检查Compile Sources中是否有缺少.m文件；
检查link binary with libraries中是否缺少依赖库，
但是在Xcode7上面好像很少出现这种问题，但是出问题也了不能不查。

### 2、确定系统依赖库是否导入
我们用到的大部分第三方库都需要导入响应的系统依赖库，例如libz.dylib(或者libz.tbd)，当缺少依赖库时也会报错，具体需要哪些系统依赖库要看第三方文档。

### 3、检查导入库路径是否正确
检查所导入库文件路径的下文件是否存在，并检查targets-->building setting下search paths下相应路径是否正确。
![这里写图片描述](http://img.blog.csdn.net/20160603164025715)

### 4、设置Other Linker Flags
很多第三方库直接导入xcode，编译的时候都不能正确识别，需要在build settings 中设置 Other Linker Flags：
######   a、添加值$(inherited)
######   b、添加值-ObjC
######   c、添加值-force_load  path/to/yourSdk

### 5、设置Link With Standerd Libraries
有时候工程中需要用到混编，如果Link With Standerd Libraries的值不小心设置成NO的话很可能许多函数找不到，报Undefined symbols for architecture arm64错误，将其值设置成YES就可以了。

### 6、DerivedData
设置完以上步骤，clean 一下工程 重新编译，如果还出错，关闭xcode，打开finder ，使用快捷键command +shift +g 搜索目录~/Library/Developer/Xcode/DerivedData/   找到你的app对应的文件夹，删除这个文件夹，重新打开xcode运行，应该就OK了。