---
title: git 知识
categories: code
tags: git
---

```
ssh -T git@github.com
--首先配置config
git config --global user.name "your name"
git config --global user.email "your_email@youremail.com"
```

```
-- 推文件
git init
git add . / 任意文件/文件夹（但必须非空）
git commit -m "    "
git remote add origin git@github.com:yourName/yourRepo.git
git push origin master
```

```
-- 删文件
rm file --先将文件删除
git status --查看状态
git commit -m ""
git push origin master
```

```shell
# 目前git 推代码需要使用个人口令
```

```sh
git config --global credential.helper store

git pull /git push (这里需要输入用户名和密码，以后就不用啦)
```
