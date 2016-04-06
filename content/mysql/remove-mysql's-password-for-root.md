---
title: "Remove MySql's Password for root"
date: 2016-04-05 22:41
---

今天安装了Percona Mysql Server 5.7。之前安装的版本初始情况下root用户没有密码，而这个版本则需要输入密码。
在开发环境重复敲密码挺繁琐的，所以决定将Mysql调教一下，免去密码输入的操作。

Step 1: 停止Mysql
```sh
[root@localhost ~]# /etc/init.d/mysql stop
Stopping mysqld:                                           [  OK  ]
```
Step 2: 重启mysql，忽略授权
```sh
[root@localhost ~]# mysqld_safe --skip-grant-tables &
```
Step 3: 登陆Mysql，并修改Mysql root用户密码
```sh
use mysql
FLUSH PRIVILEGES;
ALTER USER 'root'@'localhost' IDENTIFIED BY '';
```
Step 4: 重启mysql
```sh
/etc/init.d/mysql stop
/etc/init.d/mysql start
```
Step 5: 无密码登陆Mysql
```sh
mysql -u root
```
