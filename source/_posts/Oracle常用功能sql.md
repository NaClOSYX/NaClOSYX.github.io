---
title: Oracle常用功能sql
date: 2023-02-14 00:00:00 +0800
updated: 2023-02-14 00:00:00 +0800
categories: [博客, 数据库]
tags: [常用, 学习, 数据库] 
author: NaClO
---

- 闪回

  ```sql
  select * from 表名 as of timestamp to_timestamp('2021-6-19 1:10:00','yyyy-mm-dd hh24:mi:ss');
  ```

- 查询sql记录

  ```sql
  select * from v$sql WHERE SQL_TEXT LIKE '%表名%' ORDER BY last_load_time DESC;
  ```

- 自带视图

  ```sql
  SELECT * FROM v$tempfile;
  SELECT * FROM dba_temp_files;
  
  SELECT * FROM v$sysstat;
  SELECT * FROM v$sort_usage;
  SELECT * FROM v$sort_segment;
  
  ```

- 查约束

  ```sql
  select *from user_constraints where CONSTRAINT_Name LIKE '%键名%'
  select *from user_cons_columns where CONSTRAINT_Name LIKE '%键名%'
  ```

- 时间

  ```sql
  SELECT SYSDATE  FROM dual;
  SELECT SYSTIMESTAMP FROM dual;
  ```

- 锁表

  ```sql
  -- 查看有没有表被锁住
  select * from v$locked_object;
  
  -- 查询锁表的详细信息
  select sess.sid,sess.serial#,lo.oracle_username,
  lo.os_user_name,ao.object_name,lo.locked_mode
  from v$locked_object lo, dba_objects ao, v$session sess, v$process p
  where ao.object_id = lo.object_id and lo.session_id = sess.sid;
  
  -- 结束掉锁住的表
  alter system kill session 'sid,serial#';
  ```

- s





