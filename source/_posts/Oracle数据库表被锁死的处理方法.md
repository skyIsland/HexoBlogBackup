title: Oracle数据库表被锁死的处理方法
author: ismatch
tags:
  - Oracle
categories: []
date: 2020-06-04 11:26:00
---
(1)锁表查询的代码有以下的形式： select count(*) from v$locked_object; select * from v$locked_object;

(2)查看哪个表被锁 select b.owner,b.object_name,a.session_id,a.locked_mode from v$locked_object a,dba_objects b where b.object_id = a.object_id;

(3)查看是哪个session引起的 select b.username,b.sid,b.serial#,logon_time from v$locked_object a,v$session b where a.session_id = b.sid order by b.logon_time;

(4)杀掉对应进程 --方法1：alter system kill session 'sid,serial#' 执行命令：alter system kill session'24,111';（(其中24,111分别是上面查询出的sid,serial#）

--方法2（方法1不灵时采用）：在操作系统命令行 orakill SID spid
orakill ORCL 4436 alter system kill session '26,7013';