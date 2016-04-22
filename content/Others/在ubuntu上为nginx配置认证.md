---
title: "在Ubuntu上为Nginx配置认证"
date: 2016-04-06 22:51
---

### 安装htpasswd
我们会使用htpassword来创建和生成加密的用户信息用于基础认证（Basic Authentication）。通过下面命令安装`apache2-utils`。
```sh
apt-get update
apt-get install apache2-utils
```

### 创建用户名和密码
在用Nginx托管的网站目录下成一个`*.htpasswd`文件。例如：
```
htpasswd -c /etc/nginx/basicauth.htpasswd vincent
```
命令会有如下提示，输入密码：
```
New password:
Re-type new password:
Adding password for user vincent
```

### 更新Nginx配置
在网站的Nginx配置文件中增加如下两行：
```
auth_basic "Restricted"
auth_basic_user_file /path/to/vincent.htpasswd
```
第二行是你的htpasswd文件位置。

### Reload Nginx
```
/etc/init.d/nginx reload
```
