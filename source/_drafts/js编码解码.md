title: js编码解码
author: ismatch
tags:
  - js
categories: []
date: 2018-01-04 21:52:00
---
### JS编码,解码. asp.net(C#)对应解码,编码

### escape不编码字符有69个：
```
*，+，-，.，/，@，_，0-9，a-z，A-Z
```


### encodeURI不编码字符有82个：
```
!，#，$，&，'，(，)，*，+，,，-，.，/，:，;，=，?，@，_，~，0-9，a-z，A-Z
```


### encodeURIComponent不编码字符有71个：!， '，(，)，*，-，.，_，~，0-9，a-z，A-Z

#### 1.
##### JS: escape :

##### js使用数据时可以使用escape
##### 例如：搜藏中history纪录。
##### 0-255以外的unicode值进行编码时输出%u****格式，其它情况下escape，encodeURI，encodeURIComponent编码结果相同。
#### 解码使用：unescape

##### C#:


```
HttpUtility.UrlEncode 
HttpUtility.UrlDecode
```

 

#### 2.
##### JS: encodeURI ：

##### 进行url跳转时可以整体使用encodeURI
##### 例如：
```
Location.href=encodeURI("http://cang.baidu.com/do/s?word=百度&ct=21");
```

##### 解码使用decodeURI();

##### C#: decodeURIComponent

 

### 3.
#### JS: encodeURIComponent ：

##### 传递参数时需要使用encodeURIComponent，这样组合的url才不会被#等特殊字符截断。                           
> 例如：
```
<script language="javascript">document.write('<a href="http://passport.baidu.com/?logout&aid=7& u='+encodeURIComponent("http://cang.baidu.com/bruce42")+'">退出</a& gt;');</script>
```

##### 解码使用decodeURIComponent()

##### C#:


```
[HttpContext.Current.]Server.UrlDecode

[HttpContext.Current.]Server.UrlEncode
```
