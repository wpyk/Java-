### 连接

 - -h 指定数据库位置
 - -u 指定username
 - -p 指定密码

```
mysql -h mysqldb.c1xr3pkrjhal.ap-northeast-1.rds.amazonaws.com -ukuangwen -p
```

```
mysql -uroot
```

###database操作

查看有那些数据库  
show databases;

创建database

```sql
mysql> create database wpyk;
Query OK, 1 row affected (0.57 sec)
```

指定使用那个database  
use database_name

```sql
mysql> use wpyk;
Database changed
```

删除数据库 危险

```sql
mysql> drop database wpyk;
Query OK, 0 rows affected (0.17 sec)


```
###table操作
查看所有的表

```sql
mysql> show tables;
+----------------+
| Tables_in_wpyk |
+----------------+
| t_config       |
+----------------+
1 row in set (0.09 sec)
```


创建表

```sql
create table `t_config`(
  `id` INT(11) NOT NULL AUTO_INCREMENT COMMENT 'config table id',   
  `name` VARCHAR(100) DEFAULT NULL COMMENT 'config key',
  `value` VARCHAR(100) DEFAULT NULL COMMENT 'config value',
   PRIMARY KEY (`id`)
)ENGINE=INNODB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8;
```


查看表里数据，使用*时是查看所有的列，即所有的数据。如果要单独查看某一列，则将*换成该列的列名。若要检索多列，则在列名间加上逗号（最后一个列名不加）

```sql
mysql> select * from t_config;
+----+--------+--------+
| id | name   | value  |
+----+--------+--------+
|  2 | resume | blog36 |
+----+--------+--------+
1 row in set (0.10 sec)
```


查询指定记录
```sql
select * from t_config where id = 2;
```

查询指定字段

```sql
select id,name from t_config;
```

模糊搜索

假如要进行模糊搜索的字段是在name这个属性里，则在name 後加like， 查询的字段放在''内，字段前后加%表示该字段前后内容并不清楚.也可以只用一个%表示单侧模糊匹配。

```
select * from t_book where name like '%sql%';
```




综合案例
```sql
select name from t_config where id in (2,3);

```

插入一条记录

```sql
mysql> insert into t_config(`name`,`value`) values('resume','blog36');
Query OK, 1 row affected (0.90 sec)
```

更新一条记录  
注意：如果更新语句不加where会很危险，因为它会更新表里所有记录

```sql
update t_book set name='sdfasql' where id=104;
```

删除指定记录  
注意：如果删除语句不加where会很危险，因为它会删除表里所有记录

```sql
mysql> delete from t_config where id = 2;
Query OK, 1 row affected (0.09 sec)

```


删除多条记录

```sql
mysql> delete from t_config where id in (5,11);
Query OK, 2 rows affected (0.49 sec)

```



清空整个table，删除表里所有记录,但是表结构还在，危险

```sql
mysql> delete from t_config;
Query OK, 4 rows affected (0.08 sec)
```

删除表，危险

```sql
mysql> drop table t_config;
Query OK, 0 rows affected (1.01 sec)

```

