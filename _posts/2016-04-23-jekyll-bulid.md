---
layout: post
title: HTTP协议那些事(持续更新)
description: http协议笔记
---

## web服务器

### 代理

转发的角色，每次通过代理服务器转发的请求或者响应，会追加写入Via首部信息，以标记经过的主机信息。

缓存代理

转发响应时，将资源缓存在代理服务器上，再次受到需求相同资源的请求时，直接将缓存的资源返回。

透明代理

转发请求或响应时，不对报文做任何加工的代理类型称为透明代理，反之称为非透明代理。

### 网关

利用网关可以由HTTP请求转化为其他通信协议，例如连接数据库，使用sql语句查询数据。

### 隧道

用于和远距离的服务器之间的通信，使用SSL等加密手段，确保安全。隧道本身是透明的，客户端不用在意它的存在。
  


## HTTP/1.1 常用首部字段

http首部字段重复时，处理结果可能不一致，有些浏览器优先处理第一次出现的首部，有些则不然。

**四种类型**

 * 通用首部字段
 * 请求首部字段
 * 响应首部字段
 * 实体首部字段
 
### Cookie

字段名 | 说明 | 类型
----- | --- | ----
Set-Cookie | 开始管理状态所使用的cookie信息  | 响应首部字段
Cookie | 服务器接受到的cookie信息  | 请求首部字段

**Set-Cookie**

    Set-Cookie : status=enable;expire=Tue, 05 Jul 2016....;path=/;domain= .app.com;
    

**Set-cookie字段的属性**    

    NAME = value     赋予Cookie的名称和值（必需）
    
    expire = DATE    Cookie的有效期，缺省值为关闭浏览器前为止
    
    path = PATH      将服务器上的文件目录作为Cookie的适用对象
    
    domian = 域名     作为Cookie的适用对象的域名
    
    Secure           仅在HTTPS安全通信时才会发送Cookie
    
    HttpOnly         使得Cookie不能被JS访问
    

**Cookie**

    Cookie : status = enable
          
 告知服务器，想获得http状态管理支持时，就会在请求中包含从服务器杰接受到的Cookie，接收到多个时，可以多个一起发送。