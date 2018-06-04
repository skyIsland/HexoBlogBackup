title: Js比较时间大小
author: ismatch
tags:
  - js
categories: []
date: 2018-01-04 21:41:00
---
```
 function checkDate(param) {
            var now = new Date;
            var time = new Date(param);
            if (now <= time) {
                return true;
            }
            return false;
        }
```