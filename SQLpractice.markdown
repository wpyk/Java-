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





update feature 3



































