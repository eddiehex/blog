---
title: vim中文乱码问题解决
categories: code
tags: vim
toc: true
---

#### 新建～/.vimrc文件

```shell
vim ~/.vimrc
```

#### 写入以下内容

```shell
set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1
set enc=utf8
set fencs=utf8,gbk,gb2312,gb18030
```

#### 更新

```shell
source ~/.vimrc
```

#### 其他

linux 无法正常显示中文

```shell
echo "export LANG=en_US.UTF-8" >> ~/.bashrc 
source ~/.bashrc
```



