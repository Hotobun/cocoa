---
title: 数据库基础操作
tags:
  - mysql
categories:
  - 基础
date: 2019-12-04 17:51:56
cover: /img/mysql.png
---

## 创建数据库
指定urf-8编码  
- `CREATE DATABASE databasename DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci; `

## 删除数据库 
- `drop databases <databasename>;`
- `>>> drop databases pwd;`
 
## 创建数据表
通用语法:
- `CREATE TABLE table_name (column_name column_type);`
```
CREATE TABLE IF NOT EXISTS `runoob_tbl`(
   `runoob_id` INT UNSIGNED AUTO_INCREMENT,   // int无符号自增
   `runoob_title` VARCHAR(100) NOT NULL,      
   `runoob_author` VARCHAR(40) NOT NULL,      
   `submission_date` DATE,
   PRIMARY KEY ( `runoob_id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

## 删除数据表
- `DROP TABLE tableanme ;`   

## 插入数据
```
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
```


## 查询数据
```
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][ OFFSET M]
```
1.查询语句中你可以使用一个或者多个表，表之间使用逗号(,)分割，并使用WHERE语句来设定查询条件。  
2.SELECT 命令可以读取一条或者多条记录。  
3.你可以使用星号（*）来代替其他字段，SELECT语句会返回表的所有字段数据  
4.你可以使用 WHERE 语句来包含任何条件。  
5.你可以使用 LIMIT 属性来设定返回的记录数。  
6.你可以通过OFFSET指定SELECT语句开始查询的数据偏移量。默认情况下偏移量为0。  

## where子句
用于筛选符合条件的数据   
```
select * from table 
    where id = 1 or data = 'hello' ;
```

## 简易备份与恢复
本机可忽略主机名与端口  
备份：  
`mysqldump -h主机名 -P端口 -u用户名 -p密码 --database 数据库名 > 文件名.sql`  
恢复：  
`mysql -u用户名 -p密码 数据库名 < 文件名.sql ;`  