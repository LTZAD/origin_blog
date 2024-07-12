---
title: SQLite 笔记
date: 2024-07-07 23:00:00
categories:
- SQLite
cover: /pictures/cover_sql.jpg
copyright_author: 找不到服务器
description: 一些关于SQLite的笔记
swiper_index: 3
tags:
- 教学
- SQLite
---

# SQLite 笔记
SQLite C++依赖库:
<https://github.com/SRombauts/SQLiteCpp>  

## 参考
[SQLite 教程 -菜鸟教程](https://www.runoob.com/sqlite/sqlite-tutorial.html)  
[SQLite Download Page](https://www.sqlite.org/download.html)  
[SQLite中文网](https://sqlite.readdevdocs.com/)  
[DB Browser for SQLite](https://sqlitebrowser.org/)  
[感受一下C++操作SQLite有多麻烦 -简书](https://www.jianshu.com/p/562576ec138c)  
[玩转SQLite-11：C语言高效API之sqlite3_prepare系列函数 -CSDN博客](https://blog.csdn.net/hbsyaaa/article/details/127858034)  
[SQLite主键](https://www.yiibai.com/sqlite/primary-key.html)  
[Sqlite数据库-使用的查询语句大全 -CSDN博客](https://blog.csdn.net/gymaisyl/article/details/108404902)  
[SQLite 教程 -极客教程](https://geek-docs.com/sqlite)  

## 语法笔记
| 功能 | 命令 |
|---|---|
| 打开文件（cmd） | sqlite3 filename.db |
| 打开文件（sql） | .open filename.db |
| 退出 | .exit |
| 列出所有表格 | .tables |
| 列出表格的键 | .schema tablename |
| 显示模式 | .header on  \  .mode column |
| 创建表格 | CREATE TABLE tablename; |
| 删除表格 | DROP TABLE tablename; |
| 清空表格 | DELETE FROM sqlite_sequence WHERE name = 'tablename'; |
| 修改表格名称 | ALTER TABLE table_name RENAME TO new_table_name; |
| 添加列 | ALTER TABLE tablename ADD COLUMN columnname INTEGER DEFAULT 0; |
| 增 | INSERT INTO tablename VALUES (7, 'James', 24, 'Houston', 10000.00 ); |
| 删 | DELETE FROM tablename WHERE rowid=valuename; |
| 改 | UPDATE tablename SET columnname=valuename WHERE conditionname; |
| 查 | SELECT * FROM tablename; |