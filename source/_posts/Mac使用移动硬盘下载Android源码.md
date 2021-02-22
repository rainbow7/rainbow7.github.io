---
title: Mac使用移动硬盘下载Android源码
date: 2021-02-16 23:57:39
tags: Android
---

别管看不看，额，主要看有没有时间：），先把Android源码搞下来。废话不多说，开搞。

<!-- more -->

### 创建磁盘分区

无奈Mac的磁盘已经成天的提示不够用，只好使用移动硬盘来下载。我是专门弄了一块硬盘存放Android源码，这样的话比较省心。上来直接格式化为大小写敏感的分区，也就是**Mac OS扩展 区分大小写，日志式**，为什么要区分大小写， 是因如果要编译Android源码的话，是需要所在分区对大小写敏感。

### 安装[repo](https://source.android.com/source/developing)

* `mkdir ~/bin`  // 当前用户下创建bin目录
* `PAHT=~/bin:$PATH`  // 加入到临时变量
* `curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo`  // 下载repo到bin目录
* `chmod a+x ~/bin/repo`  // 修改repo的权限。意思是给所有用户添加执行权限
* `cd /Volumes/硬盘的名字`  // 进入到要下载源码的目录
* `mkdir aosp`  //创建工作空间，名字看自己喜好
* `cd aosp`  // 进入到工作空间

### 配置git

建议使用gmail邮箱。这个据说是为了以后更新源码方便，因为目前还没更新过，所以也不是很清楚到底有没有用。

* `git config --global user.name xxx`
* `git config --global user.email xxx@xxx.xx`
  
### 配置清华源（可选）

不方便科学上网，或者为了提高速度，可以配置清华源。
* 加一个环境变量，使用bash就在.bashrc，使用zsh就在.zshrc文件里加入`'export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo/'` 
  
### 初始化repo，同步代码

* `cd /Volumes/aosp` 进入到第2步建立好的目录
* [Android版本](https://android.googlesource.com/platform/manifest)，可以去这里看所有的分支。
* `repo init '$ repo init -u https://aosp.tuna.tsinghua.edu.cn/platform/manifest -b android-11.0.0_r9' `这里选择当前最新版本分支
* 初始化完成后，`repo sync` 等吧。
* 下载完成后，大概占用了50多G空间，解压完成后大概占用110多G的空间。只能说，真TM大啊。

> 其实大部分的教程也是基于[官方教程](https://source.android.com/source/downloading)进行的拓展，加了很多图文，我觉得对于一个开发者来说，其实有些太过于详细了。

> 特别鸣谢
> https://blog.csdn.net/u012528526/article/details/87994711
> https://juejin.cn/post/6844903832028184590