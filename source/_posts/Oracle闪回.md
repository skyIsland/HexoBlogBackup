title: Oracle闪回
author: ismatch
tags: []
categories: []
date: 2022-04-02 11:52:00
---

#### 根据oracle自己的快照备份查询某一时刻的某张表数据

```
 select * from 表名 as of timestamp to_timestamp('2018-06-08 11:06:00', 'yyyy-MM-dd HH:mi:ss');
 ```

#### 可直接删除表数据，再插入历史快照数据：

```
delete from 表名;
<<<<<<< HEAD
commit;
=======

commit;

>>>>>>> a8fd0b0b16fb234960e5e99868aebc4812989c23
insert into 表名 select * from 表名 as of timestamp to_timestamp('2018-06-08 11:06:00', 'yyyy-MM-dd HH:mi:ss');
```


```
 SELECT * FROM ( select * from  table1 as of timestamp to_timestamp('2022-04-02 10:00:00','yyyy-mm-dd hh24:mi:ss')) where id not in(select id from  RF_W_DeviceFaultSituation)
 
 insert into table1 (SELECT * FROM ( select * from  table1 as of timestamp to_timestamp('2022-04-02 9:59:00','yyyy-mm-dd hh24:mi:ss')) where id not in(select id from  table1))
<<<<<<< HEAD
=======

>>>>>>> a8fd0b0b16fb234960e5e99868aebc4812989c23
```