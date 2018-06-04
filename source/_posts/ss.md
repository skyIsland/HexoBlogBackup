title: '利用js的slice,只需一行代码完成星星评分'
author: ismatch
date: 2018-01-04 21:57:15
tags:
---
#### slice可是好东西哦


> *slice() 方法可从已有的数组中返回选定的元素。*

```
//五星好评
var rate = 5;
&quot;★★★★★☆☆☆☆☆&quot;.slice(5 - rate, 10 - rate);
```
![](/img/star.png)