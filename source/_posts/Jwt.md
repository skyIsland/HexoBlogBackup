title: Jwt
author: ismatch
tags:
  - jwt
categories: []
date: 2020-04-29 01:13:00
---
#### 记录一下jwt的使用
1.JWT是由三段信息构成的，将这三段信息文本用.链接一起就构成了Jwt字符串。
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJVc2VySWQiOiJBZG1pbiIsIkV4cGlyZSI6IjIwMjAtMDQtMjkgMjM6MjU6MTgifQ.-YB1zO4CxyoDhPVGvqSQnjlIy0puehv6z8WlA7p9d6Y
```
- 第一部分为头部（header)：
	- 声明类型，这里是jwt；
   - 声明加密算法,通常直接使用 HMACSHA256
   
   ```
   {"alg":"HS256","type":\"JWT\"}
   ```
- 第二部分为载荷/负载（payload)：   
	- 想存啥存啥...有一些通用的字段，比如：Expire-过期时间
   ```
   {"UserId":"1","Expire":"2020-04-29 00:31:00"}
   ```
- 第三部分为签证（signature)：
	- 1.var str = "第一部分【header】进行base64编码+第二部分【payload】进行base64编码";
   - 2.再对这个str进行HMACSHA256加密
- 此时你拥有的如下
 - 第一部分【header】进行base64编码 eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
 - 第二部分【payload】进行base64编码 eyJVc2VySWQiOiJBZG1pbiIsIkV4cGlyZSI6IjIwMjAtMDQtMjkgMjM6MjU6MTgifQ
 - 第三部分【signature】-YB1zO4CxyoDhPVGvqSQnjlIy0puehv6z8WlA7p9d6Y
 - 最后把你拥有的字符串用点号【.】进行拼接起来，就得到了eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJVc2VySWQiOiJBZG1pbiIsIkV4cGlyZSI6IjIwMjAtMDQtMjkgMjM6MjU6MTgifQ.-YB1zO4CxyoDhPVGvqSQnjlIy0puehv6z8WlA7p9d6Y
 
2.得到了Token值之后，每次请求接口就可以在参数里或者header里带上Token来进行表明身份啦