---
title: HTTP-Cookie
date: 2016-10-11 21:20:46
tags: HTTP
---

## 1. 什么是Cookie
cookie就像服务器给用户贴的"嗨，我叫xxx"的贴纸一样，用户访问一个Web站点时，这个Web站点就可以读取那个服务器贴在用户身上的所有贴纸，是一种用来识别客户端的技术
-- 来自《HTTP权威指南》11.6.2

Cookie是`一小段文本信息`，伴随着用户请求和页面在`Web服务器`和`浏览器`之间传递
-- 来自 [细说Cookie](http://www.cnblogs.com/fish-li/archive/2011/07/03/2096903.html)


## 2. Cookie类型
+ 持久Cookie
+ 会话Cookie

它们之间唯一的区别就是它们的过期时间。

## 3. 使用方式
+ 服务端
    通过在`HTTP响应头`中增加 `Set-Cookie` 或 `Set-Cookie2` 头字段向客户端增加cookie
+ 客户端
    通过在`HTTP请求头`中增加 `cookie` 头字段将cookie值传递回去

## 4. Cookie中的属性
### 4.1 domain属性
此属性用来控制哪些站点可以看到这个cookie
如：
```
Set-Cookie: user="mary17"; domain="youcompany.com"
则所有以`youcompany.com`结尾的域名都能获取到此cookie
```

### 4.2 path属性
此属性用来控制哪些路径可以看到这个cookie
如：
```
Set-Cookie: tel="1313333322"; domain="youcompany.com"; path=/autos/
则只有以`youcompany.com`结尾的域名，并且请求路径以`/autos/`为前缀的请求可以获得此cookie
```

### 4.3 Expires属性
用来定义cookie的实际生存期，一旦到了过期时间，就不再存储或发送这个cookie
如：
```
Set-Cookie: user="mary17"; domain="youcompany.com"; expires=Webnesday, 09-Nov-00 23:12:40 GMT
```
唯一合法的时区为`GMT`

### 4.4 Secure属性
用来定义只有在HTTP使用`SSL安全连接时`才会发生此cookie
如：
```
Set-Cookie: user="mary17"; domain="youcompany.com"; secure
```

### 4.5 HttpOnly属性
用来定义只有基于`HTTP`或`HTTPS`的通信可以使用此cookie，也就意味着JS API `document.cookie`是无法访问到此cookie的
如：
```
Set-Cookie: user="user123"; domain="yourcompany.com"; httponly
IE6不支持
```

## 5.操作Cookie文件
在 Mac 平台下，Cookie存储在 `~/Library/Application Support/Google/Chrome/Default/Cookies` 文件里，这个文件实质上是一个 `sqlite3 数据库文件`，也就是说，我们是没法直接操作Cookie文件的

那么，要如何操作？
使用 `Chrome扩展程序—EditThisCookie` 来操作

## 6.HTTP-Session
在说Cookie与Session的区别之前，先要说明一下，Session是个什么东西。
Session是一种位于服务端，结合客户端的识别技术(如Cookie或胖URL)，以达到追踪客户端的技术，Session的生命周期其实并不是 `从打开浏览器到关闭浏览器` 这么简单，服务端为每个 Session 是采用过期时间来维护的，所以在某些应用里，我们经常会见到 `会话超时，请重新登陆` 的警示框

SessionId: 这其实是服务端在第一次接收到客户端请求时，为客户端生成的唯一标识，服务端用这个值来标识这个客户端，并且将这个值写入 HTTP响应首部 `Set-Cookie` 或 `Set-Cookie2` 中，客户端在随后的请求中，都会在 HTTP请求首部 `Cookie` 中写入SessionId的值，如此，服务端也就能识别出，这一次的请求和上一个请求是来自于同一个客户端～

总结一下区别:
+ 服务端技术
+ 依赖客户端识别技术，但不局限于Cookie，如果客户端禁止cookie的话，可以将SessionId写入胖URL
