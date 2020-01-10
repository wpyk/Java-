## 连接

 - -h 指定数据库位置
 - -u 指定username
 - -p 指定密码

```
mysql -h mysqldb.c1xr3pkrjhal.ap-northeast-1.rds.amazonaws.com -ukuangwen -p
```

```
mysql -uroot
```

## database操作

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
##table操作
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



### 创建表

```sql
create table `t_config`(
  `id` INT(11) NOT NULL AUTO_INCREMENT COMMENT 'config table id',   
  `name` VARCHAR(100) DEFAULT NULL COMMENT 'config key',
  `value` VARCHAR(100) DEFAULT NULL COMMENT 'config value',
   PRIMARY KEY (`id`)
)ENGINE=INNODB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8;
```



### 查询
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



### 查询指定记录
```sql
select * from t_config where id = 2;
```


### 查询指定字段

```sql
select id,name from t_config;
```


### 模糊搜索

假如要进行模糊搜索的字段是在name这个属性里，则在name 後加like， 查询的字段放在''内，字段前后加%表示该字段前后内容并不清楚.也可以只用一个%表示单侧模糊匹配。

```
select * from t_book where name like '%sql%';
```





### 综合案例
```sql
select name from t_config where id in (2,3);

```


### 插入一条记录

```sql
mysql> insert into t_config(`name`,`value`) values('resume','blog36');
Query OK, 1 row affected (0.90 sec)
```


### 更新一条记录  
注意：如果更新语句不加where会很危险，因为它会更新表里所有记录

```sql
update t_book set name='sdfasql' where id=104;
```


### 删除指定记录  
注意：如果删除语句不加where会很危险，因为它会删除表里所有记录

```sql
mysql> delete from t_config where id = 2;
Query OK, 1 row affected (0.09 sec)

```



### 删除多条记录

```sql
mysql> delete from t_config where id in (5,11);
Query OK, 2 rows affected (0.49 sec)

```




### 清空整个table，删除表里所有记录,但是表结构还在，危险

```sql
mysql> delete from t_config;
Query OK, 4 rows affected (0.08 sec)
```

### 删除表，危险

```sql
mysql> drop table t_config;
Query OK, 0 rows affected (1.01 sec)

```



### 实例练习
	CREATE TABLE student(  
	snum varchar(10) NOT NULL primary key,  
	sname varchar(20) NOT NULL ,  
	sage int(2) NOT NULL ,  
	sgender varchar(6) NOT NULL   
	);  

	CREATE TABLE teacher(  
	tnum varchar(10) NOT NULL primary key,   
	tname varchar(20) NOT NULL   
	);  

	CREATE TABLE course(    
	cnum varchar(10),-- course number   
	cname varchar(20),-- course name  
	tnum varchar(20),-- teacher number of this course  
	constraint pk_course primary key(cnum,tnum)  
	);  

	CREATE TABLE sc(  
	snum varchar(10),-- student number   
	cnum varchar(20),-- course number  
	score float(4,2),-- course score   
	constraint pk_sc primary key(snum,cnum)  
	);  

	insert into student values('s001','张一',21,'M');  
	insert into student values('s002','王二',22,'F');  
	insert into student values('s003','李三',21,'M');  
	insert into student values('s004','赵四',23,'F');  
	insert into student values('s005','孙五',21,'M');  
	insert into student values('s006','张花花',21,'M');  
	insert into student values('s007','王小玉',22,'F');  
	insert into student values('s008','李大嘴',22,'F');  
	insert into student values('s009','赵扁豆',23,'M');  
	insert into student values('s010','孙远',21,'M');  

	insert into teacher values('t001','刘老师');  
	insert into teacher values('t002','彭老师');  
	insert into teacher values('t003','王老师');  

	insert into course values('c001','计算机基础','t002');  
	insert into course values('c002','Servlet','t001');  
	insert into course values('c003','J2SE','t001');  
	insert into course values('c004','J2EE','t003');  
	insert into course values('c005','数据库','t003');  
	insert into course values('c006','PHP','t002');  
	insert into course values('c007','Python','t001');  
	insert into course values('c008','SQL','t001');  
	insert into course values('c009','Oracle','t003');  
	insert into course values('c010','毛泽东思想体系','t002');  


	insert into sc values('s001','c001',90);  
	insert into sc values('s002','c001',80.5);  
	insert into sc values('s003','c001',79.9);  
	insert into sc values('s004','c001',85.6);  
	insert into sc values('s001','c002',81.2);  
	insert into sc values('s002','c002',70);  
	insert into sc values('s003','c002',49);  
	insert into sc values('s001','c003',87.5);  
	insert into sc values('s001','c005',54.5);  

Q：查询学生表的前十条数据  
	select * from student where snum<=10;  
	select * from student where snum!>10; --->这一句是错的  
	select * from student where snum between s001 and s010;  --->这句也是错的  

Q：查询成绩表中的最高分，最低分，平均分，总分 (本题考查聚集函数)  
最高分：select max(score) as MAX from sc;  
最低分：select min(score) as MAX from sc;  
平均分：select avg(score) as AVERAGE from sc;  
总分：  select sum(score) as SUM from sc;   

Q：查询刘老师所教授的课程的数量  
找刘老师的课：select * from course where tnum='t001';  
计数： select count(*) from course where tnum='t001';  

Q:查询所有老师所带的课程数量  
select count(*) as number from course;  
select count(*) as nuber from course where tnum in ('t001','t002','t003');  

Q:查询姓张的学生名单  
select * from student where sname like '%张%';  

Q:查询课程名称为"数据库",且分数低于60 的学生姓名和分数  
select snum,score from sc where cnum=(select cnum from course where cname='数据库') having score <60;  
select sname,score from student st,sc, course c where sc.score <60 and sc.snum =st.snum and sc.cnum=c.cnum and c.cname='数据库';  


## 左连接，右连接，内连接，全连接

连接条件可在FROM或WHERE子句中指定，建议在FROM子句中指定连接条件。WHERE和HAVING子句也可以包含搜索条件，以进一步筛选连接条件所选的行。   
   
      连接可分为以下几类：     
    
      内连接。（典型的连接运算，使用像   =   或   <>   之类的比较运算符）。包括相等连接和自然连接。    
      内连接使用比较运算符根据每个表共有的列的值匹配两个表中的行。例如，检索   students   和   courses   表中学生标识号相同的所有行。   
    
      外连接。外连接可以是左向外连接、右向外连接或完整外部连接。    
      在FROM子句中指定外连接时，可以由下列几组关键字中的一组指定：   
      LEFT   JOIN   或   LEFT   OUTER   JOIN。     
      左向外连接的结果集包括LEFT  OUTER子句中指定的左表的所有行，而不仅仅是连接列所匹配的行。如果左表的某行在右表中没有匹配行，则在相关联的结果集行中右表的所有选择列表列均为空值。    
      RIGHT  JOIN  或  RIGHT   OUTER   JOIN。    
      右向外连接是左向外连接的反向连接。将返回右表的所有行。如果右表的某行在左表中没有匹配行，则将为左表返回空值。   
   
      FULL   JOIN   或   FULL   OUTER   JOIN。     
      完整外部连接返回左表和右表中的所有行。当某行在另一个表中没有匹配行时，则另一个表的选择列表列包含空值。如果表之间有匹配行，则整个结果集行包含基表的数据值。   
   
      交叉连接。交叉连接返回左表中的所有行，左表中的每一行与右表中的所有行组合。交叉连接也称作笛卡尔积。   
   
例如，下面的内连接检索与某个出版商居住在相同州和城市的作者：  
   
  USE   pubs  
  SELECT   a.au_fname,   a.au_lname,   p.pub_name  
  FROM   authors   AS   a   INNER   JOIN   publishers   AS   p  
        ON   a.city   =   p.city  
        AND   a.state   =   p.state  
  ORDER   BY   a.au_lname   ASC,   a.au_fname   ASC   
   
      FROM   子句中的表或视图可通过内连接或完整外部连接按任意顺序指定；但是，用左或右向外连接指定表或视图时，表或视图的顺序很重要。有关使用左或右向外连接排列表的更多信息，请参见使用外连接。     
    
例子：  
  a表       id   name     b表     id     job   parent_id  
              1   张3                   1     23     1  
              2   李四                  2     34     2  
              3   王武                  3     34     4  
   
  a.id同parent_id   存在关系   
    
  内连接   
  select   a.*,b.*   from   a   inner   join   b     on   a.id=b.parent_id  
   
  结果是    
  1   张3                   1     23     1  
  2   李四                  2     34     2   
    
  左连接   
  select   a.*,b.*   from   a   left   join   b     on   a.id=b.parent_id  
   
  结果是    
  1   张3                    1     23     1  
  2   李四                  2     34     2  
  3   王武                  null   

  右连接   
  select   a.*,b.*   from   a   right   join   b     on   a.id=b.parent_id  
   
  结果是    
  1   张3                   1     23     1  
  2   李四                 2     34     2  
  null                       3     34     4   
    
  完全连接   
  select   a.*,b.*   from   a   full   join   b     on   a.id=b.parent_id   

  结果是    
  1   张3                   1     23     1  
  2   李四                 2     34     2  
  null                 3     34     4  
  3   王武                 null
