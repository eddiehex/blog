---
title: vim中文乱码问题解决
categories: code
tags: vim
toc: true
---

1 新建～/.vimrc文件

```shell
vim ~/.vimrc
```

2 写入以下内容

```shell
set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1
set enc=utf8
set fencs=utf8,gbk,gb2312,gb18030
```

3 更新

```shell
source ~/.vimrc
```
