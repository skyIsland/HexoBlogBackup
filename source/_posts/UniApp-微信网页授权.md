title: UniApp+微信网页授权
author: ismatch
tags:
  - 'uniapp,小程序'
categories: []
date: 2022-04-24 11:48:00
---
#### 授权
##### v1

- app.vue进入页面
    - 获取缓存open_id，refreshtoken
	  - 成功则刷新refreshtoken
      refreshtoken异常则清除缓存getWxOauthUrl并location.href = res.data;
      - refreshtoken成功则重新设置token，open_id，refreshtoken
    - 异常则判断是否带有微信的code，
        - 有则getWxOpenId
            - 成功则设置token，open_id，refreshtoken
            - 反之清除缓存getWxOauthUrl并location.href = res.data;
        - 否则getWxOauthUrl()

- 还有其他请求授权过期时的处理？
<!--more--> 
##### v2
[Jwt](https://baijiahao.baidu.com/s?id=1711290402057923797&wfr=spider&for=pc)

- app.vue进入页面

    - 获取缓存open_id
        - 成功则请求一次CheckUserInfo或者checkWxLogin，401则会进入全局拦截
    - 失败则判断是否带有微信的code，
		- 有则getWxOpenId
			成功则设置token，open_id，refreshtoken
		- 反之清除缓存getWxOauthUrl并location.href = res.data;
    - 否则getWxOauthUrl()

还有其他请求授权过期时的处理？
> [uniapp.request全局拦截](https://uniapp.dcloud.io/api/interceptor.html)