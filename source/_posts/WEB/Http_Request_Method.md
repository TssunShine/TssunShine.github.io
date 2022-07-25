---
title: Http Request Method
tags: [Http,CTFHub]
categories:
  - WEB
date: 2022-07-16 21:03:04
---

HTTP Method 是可以自定义的，并且区分大小写。

<!-- more -->

# GET

**Http GET 方法**请求指定的资源。使用 **GET** 的请求一般只用于获取数据。

## 语法

  ```php
  GET /index.html
  ```

## Request库实现

  ```python
  import requests
  r = requests.get(url)
  ```

## 规范

[Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.1)

---

# POST

**Http POST 方法**发送数据给服务器。请求主体的类型由 **Content-Type 首部指定。**

PUT 和 POST方法的区别是，PUT方法是幂等的：连续调用一次或者多次的效果相同（无副作用）。连续调用同一个POST可能会带来额外的影响，比如多次提交表单。

  - 一个 POST 请求通常是通过 HTML 表单发送，并返回服务器的修改结果。在这种情况下 content-type 是通过在 *form* 元素中设置正确的 `enctype` 属性，或是在 *input* 和 *button* 元素中设置 `formenctype` 属性来选择的

    - `application/x-www-form-urlencoded` ：数据被编码成以’&’分隔的键-值对，同时以’=’分隔键和值。非字母或数字的字符会被**percent-encoding：**该类型不支持二进制数据的原因（以`Multipart/form-data`代替）
    - `multipart/form-data`
    - `text/plain`

  - 当 POST 请求是通过除HTML表单之外的方式发送时，例如使用 XMLHttpRequest，那么请求主体可以是任何类型。按 HTTP 1.1 规范中描述， POST以统一的方法涵盖以下功能

    - 注释已有的资源
    - 在公告板，新闻组，邮件列表或类似的文章组中发布消息
    - 通过注册新增用户
    - 向数据处理程序提供一批数据，例如提交一个表单
    - 通过追加操作，扩展数据库数据

## 语法

  ```php
  POST /index.html
  ```

## Requests库实现

  ```python
  import requests
  r = requests.post(url,data = {'key':'value'})
  ```

## 规范

[RFC 7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.3)

---

# HEAD

**HTTP HEAD 方法**请求资源的头部信息，并且这些头部信息与 HTTP **GET** 方法请求时返回的一致。该请求方法的一个使用场景是在下载一个大文件前先获取其大小再决定是否要下载，以此可以节约带宽资源。

HEAD 方法的响应不应包含响应正文。即使包含了正文也必须忽略掉，虽然描述正文信息的 entity headers，例如 `Content-Length` 可能会包含在响应中，但它们并不是用来描述 HEAD 响应本身的，而是用来描述同样情况下 GET 请求应该返回的响应。

如果 HEAD 请求的结果显示在上一次 GET 请求后缓存的资源已经过期了，即使没有发出 GET 请求，缓存也会失效。

## 语法

  ```php
  HEAD /index.html
  ```

## Requests库实现

  ```python
  import requests
  r = requests.head(url)
  ```

## 规范

[RFC 7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.2)

---

# CONNECT

在HTTP协议中，**CONNECT 方法**可以开启一个客户端与所请求资源之间的双向沟通的通道。它可以用来创建隧道(tunnel)。

例如，CONNECT 可以用来访问采用了 SSL(HTTPS) 协议的站点。客户端要求代理服务器将TCP连接作为通往目的主机隧道。之后该服务器会代替客户端与目的主机建立连接。连接建立好之后，代理服务器会面向客户端发送或接受TCP消息流。

CONNECT 是一个应用范围为点到点的方法。

## 语法

  ```php
  CONNECT www.example.com:443 HTTP/1.1
  ```

## 规范

[RFC 7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.6)

---

# PUT

**HTTP PUT 请求方法**使用请求中的负载创建或者替换目标资源。

PUT 与 POST 的区别在于，PUT方法是幂等的：调用一次与连续调用多次是等价的（无副作用），而连续调用多次 POST 方法可能会有副作用，比如将一个订单重复提交多次。

## 语法

  ```php
  PUT /new.html HTTP/1.1
  ```

## Requests库实现

  ```python
  import requests
  r = requests.put(url,data = {'key'='value'})
  ```

## 规范

[RFC 7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.4)

---

# DELETE

**HTTP DELETE 请求方法** 用于删除指定的资源。

## 语法

  ```php
  DELETE /file.html HTTP/1.1
  ```

## Requests库实现

  ```python
  import requests
  r = requests.delete(url)
  ```

## 规范

[RFC 7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.5)

---

# OPTIONS

**HTTP OPTIONS 请求方法** 用于获取目的资源所支持的通信选项。客户端可以对特定的URL使用OPTIONS方法，也可以对整站(通过将URL设置为’*’)使用该方法。

## 语法

  ```php
  OPTIONS /index.html HTTP/1.1
  OPTIONS * HTTP/1.1
  ```

## Requests库实现

  ```python
  import requests
  r = requests.options(url)
  ```

## 规范

[RFC 7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.7)

---

# PATCH

**HTTP PATCH 请求方法** 用于对资源进行部分修改。

在 HTTP 协议中，PUT 方法被用来表示对资源进行整体覆盖，而 POST 方法则没有对标准的补丁格式提供支持。不同于 PUT 方法，而与 POST 方法类似，PATCH 方法是非幂等的，这就意味着连续多个相同的请求会产生不同的效果。

要判断一台服务器是否支持PATCH方法，需要查看它是否将其添加到了响应首部‘Allow’或者‘Access-Control-Allow-Methods’（在跨领域访问的场合，CORS）的方法列表中。

另外一个支持PATCH方法的隐含迹象是‘Accept-Patch’首部的出现，这个首部明确了服务器端可以接受的补丁文件的格式。

## 语法

```php
PATCH /file.txt HTTP/1.1
```

## 规范

[RFC 5789:PATCH Method for HTTP](https://datatracker.ietf.org/doc/html/rfc5789)

---

# TRACE

**HTTP TRACE 方法** 实现沿通向目标资源的路径的消息环回（loop-back）测试，提供了一种实用的debug机制。

请求的最终接受者应当原样反射（reflect）它接收到的消息，作为一个**Content-Type**为`message/http`的200（OK）响应的消息的主体（body）返回给客户端。

最终接受者是指初始（origin）服务器，或者第一个接收到`Max-Forwards`值为0的请求的服务器。

## 语法

```php
TRACE /index.html
```

## 规范

[Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.8)

---

> https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods

---

# 自定义请求方法

在使用curl命令时，可使用 `-X /<command/>`或 `--request /<command/>`来自定义与服务器通信使用的请求方法。

## CTFHUB示例

> CTFHUB-skillTree-WEB-Http协议-Http请求方法-writeup

![截屏2022-07-18 下午2.28.15](https://s2.loli.net/2022/07/18/7zKFhBcOrby8wG4.png)
