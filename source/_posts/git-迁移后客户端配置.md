---
title: git 迁移后客户端配置
---
date: 2016-06-08 16:04:50


在项目开发中有时候git版本管理服务器地址会发生变化，此时我们本地也要相应更改一些设置，以适配新的服务器。

---



# 1. 修改git远程仓库地址

在终端设置远程仓库地址：

```
//查看远程仓库地址
$ git remote -v

//删除远程仓库地址
$ git remote rm [remoteName]

//添加远程仓库地址
$ git remote add [remoteNmae] [remoteUrl]

//例如 git remote add origin http://git.practice.com:8090/username/practice.git
```

# 2. 设置SSHkey

## 2.1 生成秘钥对 

### 查看本地是否已经配置SSH Key
```bash
$ ls -al ~/.ssh
```

### 使用ssh-keygen生成密钥对SSH key
```bash
$ ssh-keygen -t rsa -C "your email"
```


提示秘钥对生成，键入秘钥对保存文件名
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/username/.ssh/id_rsa): 
使用默认文件名，直接回车

提示输入密码，可以直接回车，也可以设置密码
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 

最后提示
Your identification has been saved in /Users/username/.ssh/id_rsa.
Your public key has been saved in /Users/username/.ssh/id_rsa.pub.
...
表示秘钥对生成成功，用命令查看，可以看到新添加的文件

```bash
$ ls -al ~/.ssh
```


## 2.2 复制ssh key信息
 

### 在终端显示秘钥对信息
```bash
$ cat ~/.ssh/id_rsa.pub
```

### 复制秘钥对信息
```bash
$ pbcopy < id_rsa.pub
```

## 2.3添加ssh key到gitlab

在浏览器打开之前设置的remote url 
1.点击用户名，找到`Profile Setting` 选项
2.点击Profile Setting ，找到`SSH Keys`选项
3.添加复制好的SSH Key



