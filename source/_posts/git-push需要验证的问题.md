title: git push需要验证的问题
author: ismatch
tags: []
categories: []
date: 2018-06-05 00:01:00
---
###### 之前在windows配置好ssh之后，push代码到github上，不会提示要登录的输入框，然而最近需要输入账号和密码
![image](../files/pusherror.png)
###### 最后...发现是Github 禁用了TLS v1.0 and v1.1，必须更新Windows的git凭证管理器
> [更新链接](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.14.0)