---
title: ssh 密钥登陆服务器
categories: code
tags: ssh
toc: true
---

### 登陆服务器后

```
[root@host ~]$ ssh-keygen  <== 建立密钥对
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): <== 按 Enter
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase): <== 输入密钥锁码，或直接按 Enter 留空
Enter same passphrase again: <== 再输入一遍密钥锁码
Your identification has been saved in /root/.ssh/id_rsa. <== 私钥
Your public key has been saved in /root/.ssh/id_rsa.pub. <== 公钥
The key fingerprint is:
0f:d3:e7:1a:1c:bd:5c:03:f1:19:f1:22:df:9b:cc:08 root@host
```

### 建立共钥

```
[root@host ~]$ cd .ssh
[root@host .ssh]$ cat id_rsa.pub >> authorized_keys
-- 更改权限
[root@host .ssh]$ chmod 600 authorized_keys
[root@host .ssh]$ chmod 700 ~/.ssh
```

### 关闭密码登陆权限

```
vi /etc/ssh/sshd_config
```

```
PasswordAuthentication no
```

### 下载私钥

```
cat root/.ssh/id_rsa
-- 直接复制，粘贴到文本编辑器中保存为无格式 shift + cmd +T
-- 本地更改私钥权限
chmod 600 id_rsa
```

### 登陆服务器

```
ssh root@ip -p aaa -i /Users/eddieho/documents/hk666
```
