---
title: Assertion failure in -[UICollectionViewData validateLayoutInRect:]
---
date: 2016-10-11 19:56:29
## Overview
最近发现一个好玩的问题，我在一个tableView的cell里面写了一个collectionView来加载图片。因为tableViewCell复用的缘故，每次复用cell的时候就会去获取cell对应数据，然后调用collectionView的reloadData方法。滑动tableVIew到固定一行的时候控制台就会输出以下bug 日志，然后程序就会crash.在stackoverflow上面也看到别人有相同的问题，有人提出是collectionView reload数据太频繁了，但是我发现就算是慢慢滑动，到固定某一个cell的时候也会报错，也就是说不是因为reload太频繁的缘故。但是在找不到其他原因的情况下我试着把reloadData方法卸载GCD异步线程里面发现问题真的不再复现了。很奇怪，哪位仁兄知道原因的帮忙解答一下。

### bug日志

```
Assertion failure in -[UICollectionViewData validateLayoutInRect:], /BuildRoot/Library/Caches/com.apple.xbs/Sources/UIKit/UIKit-3599.6/UICollectionViewData.m:433**

```



### 解决方案
```
// [_collectionView reloadData];

//在主线程中更新屏幕
dispatch_async(dispatch_get_main_queue(), ^{
    [_collectionView reloadData];
});
```
