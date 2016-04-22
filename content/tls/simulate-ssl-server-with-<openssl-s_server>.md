---
title: "Simulate SSL server with [openssl s_server]"
date: 2016-04-06 16:00
---

> 我需要使用openssl s_server的原因很简单，sitemonitor遇到很多SSL异常问题，但是我们在实验室环境不能重现用户的场景，测试时只能依赖用户的网站。通过openssl s_server可以模拟一些
用户的网站SSL配置，从而方便TroubleShooting以及降低测试成本和可控性。

### 准备
首先需要生成`s_server`需要的秘钥和证书，通过如下命令生成：
```sh
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
```
上面的命令会要求输入一些基本信息，按要求输入即可。

### 启动SSL Server
启动`s_server`时可以指定监听的端口，支持的TLS版本，支持的cipher等，例如：
```sh
openssl s_server -tls1 -cipher RC4-SHA  -key key.pem -cert cert.pem -accept 9443 -www
```
下面简单较少上我这里用到的参数。

* -tls1: 仅支持tls v1,类似的参数还有好几个，可以用来指定TLS版本信息；
* -cipher: 用来指定支持的CIPHER信息，这里`RC4-SHA`只接收RC4相关的CIPHER；
* -key: key
* -cert: 证书
* -accept: 监听的端口
* -www: 当client连接上来的时候，发回一个网页，内容就是SSL握手的一些内容。



### References:
1. http://blog.csdn.net/as3luyuan123/article/details/16850727
2. https://www.openssl.org/docs/manmaster/apps/s_server.html
