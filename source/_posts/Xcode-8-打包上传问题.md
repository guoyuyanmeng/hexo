---
title: Xcode 8 打包上传问题
date: 2016-10-14 10:32:59

---

### Overview
最近好多人升级Xcode8.0以后打包上传的时候都遇到了报错信息，在这里记录下我自己遇到的错误信息和解决方案。
## bug info 
```
Vibrator has conflicting provisioning settings. Vibrator is automatically signed, but code signing identity iPhone Distribution:
has been manually specified. Set the code signing identity value to “iPhone Developer” in the build settings editor, or switch to manual. signing in the project editor.
Code signing is required for product type ‘Application’ in SDK ‘iOS 10.0’
```
![bugInfo.png](http://upload-images.jianshu.io/upload_images/1823587-937f66c9c00deeba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 解决方案
其实我的解决方案很简单。首先选中工程文件，
在General 中 Automatically manage signing关闭（去掉前面小方框中的对勾），
然后在重新打开Automatically manage signing（显示小方框中的duigou）
这时候Team 现象显示为None，重新选择自己的证书签名就OK了。
![Provisioning PorfileSetting.png](http://upload-images.jianshu.io/upload_images/1823587-11b11372af467246.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
