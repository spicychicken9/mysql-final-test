# mysql-final-test

2019-2020 mysql final test

姓名：李志铜

学号：17061611

说明1：考试为开卷，可以上网，自觉不要相互电话和QQ；

说明2：考试时间为：2020 年 4 月 10 日 8:10分-9:40分。

说明3：试题比较多，抓紧时间，超时提交的github commit不被接受。未避免完全超时提交，可以在做题过程中多 commit 几次。

说明4：结束后发邮件给 42225@hdu.edu.cn 标题为“MySQL期末考试,姓名+学号”，内容为github链接。


1 打印当前时间（例如 2020-04-07 13:41:42），写出SQL语句和结果

sql语句：select now（）

结果：
```

mysql> select now();
+---------------------+
| now()               |
+---------------------+
| 2020-04-10 08:45:59 |
+---------------------+
1 row in set (0.00 sec)

```


2 组合打印自己的姓名和学号

(例如 张三+123456 或者 zhangsan+123456 显示需包含加号)，写出SQL语句和结果

```

mysql> SELECT '李志铜+17061611';
+-----------------+
| 李志铜+17061611 |
+-----------------+
| 李志铜+17061611 |
+-----------------+
1 row in set (0.00 sec)

```

3 建立如下表1和表2，写出建表语句和插入语句。



表1：其中deptno为主键
```

mysql> CREATE TABLE t_b1(
    -> deptno INT PRIMARY KEY,
    -> dname VARCHAR(20),
    -> loc VARCHAR(40)
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> INSERT INTO t_b1 VALUES (10, "ACCOUNTING", "NEW YORK"),
    -> (20, "RESEARCH", "DALLAS"),
    -> (30, "SALES", "CHICAGO"),
    -> (40, "OPERATIONS", "BOSTON");
Query OK, 4 rows affected (0.00 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM t_b1;
+--------+------------+----------+
| deptno | dname      | loc      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
+--------+------------+----------+
4 rows in set (0.00 sec)

```

```

mysql> create table t_b2(
    -> empno INT  PRIMARY KEY,
    -> ename VARCHAR(20),
    -> job  VARCHAR(20),
    -> MGR  INT,
    -> Hiredate Date,
    -> sal float,
    -> comm float,
    -> deptno INT
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> INSERT INTO t_b2 VALUES (7369, "SMITH", "CLERK", 7902, "1981-03-12", 800.00, NULL, 20),
    -> (7499, "ALLEN", "SALESMAN", 7698, "1982-03-12", 1600, 300, 30),
    -> (7521, "WARD", "SALESMAN", 7698, "1838-03-12", 1250, 500, 30),
    -> (7566, "JONES", "MANAGER", 7839, "1981-03-12", 2975, NULL, 20),
    -> (7654, "MARTIN", "SALESMAN", 7698, "1981-01-12", 1250, 1400, 30),
    -> (7698, "BLAKE", "MANAGER", 7839, "1985-03-12", 2450, NULL, 10),
    -> (7788, "SCOTT", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
    -> (7839, "KING", "PRESIDENT", NULL, "1981-03-12", 5000, NULL, 10),
    -> (7844, "TURNER", "SALESMAN", 7689, "1981-03-12", 1500, 0, 30),
    -> (7878, "ADAMS", "CLERK", 7788, "1981-03-12", 1100, NULL,20),
    -> (7900, "JAMES", "CLERK", 7698,"1981-03-12",  950, NULL, 30),
    -> (7902, "FORD", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
    -> (7934, "MILLER", "CLERK", 7782, "1981-03-12", 1300, NULL, 10);
Query OK, 13 rows affected (0.01 sec)
Records: 13  Duplicates: 0  Warnings: 0

```



3.1 表2 中再插入一条记录：

```
mysql> INSERT INTO t_b2 VALUES (17061611,"lizhitong","STUDENT",7782,"1999-01-26",NULL,NULL,10);
Query OK, 1 row affected (0.00 sec)

```

3.2 表中入职时间（Hiredate字段）最短的人。

SQL语句：SELECT ename，MAX（Hiredate） FROM t_b2

```

mysql> SELECT ename,max(Hiredate) FROM t_b2;
+-------+---------------+
| ename | max(Hiredate) |
+-------+---------------+
| SMITH | 1999-01-26    |
+-------+---------------+
1 row in set (0.00 sec)

```



3.3 有几种职位（job字段）？在关系代数中，本操作是什么运算？

六种。SQL语句：SELECT DISTINCT job FROM t_b2。关系代数中是，投影。

```

mysql> SELECT DISTINCT job FROM t_b2;
+-----------+
| job       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
| STUDENT   |
+-----------+
6 rows in set (0.00 sec)

```

3.4 将 MILLER 的 comm 增加 100； 然后，找到 comm 比 MILLER 低的人；

SQL语句：UPDATE t_b2 SET comm = comm+100 WHERE ename='MILLER';

```

mysql> UPDATE t_b2 SET comm = comm+100 WHERE ename='MILLER';
Query OK, 0 rows affected (0.00 sec)
Rows matched: 1  Changed: 0  Warnings: 0

```



3.5 计算每个人的收入(ename, sal + comm)；计算总共有多少人；计算所有人的平均收入。 提示：计算时 NULL 要当做 0 处理；





3.6 显示每个人的下属, 没有下属的显示 NULL。本操作使用关系代数中哪几种运算？



3.7 建立一个视图：每个人的empno, ename, job 和 loc。简述为什么要建立本视图。
```

mysql>  CREATE VIEW view_1
    -> (s_empno,s_ename,s_job)
    -> AS SELECT empno,ename,job
    -> FROM t_b2;
Query OK, 0 rows affected (0.01 sec)

mysql> SELECT * FROM view_1;
+----------+-----------+-----------+
| s_empno  | s_ename   | s_job     |
+----------+-----------+-----------+
|     7369 | SMITH     | CLERK     |
|     7499 | ALLEN     | SALESMAN  |
|     7521 | WARD      | SALESMAN  |
|     7566 | JONES     | MANAGER   |
|     7654 | MARTIN    | SALESMAN  |
|     7698 | BLAKE     | MANAGER   |
|     7788 | SCOTT     | ANALYST   |
|     7839 | KING      | PRESIDENT |
|     7844 | TURNER    | SALESMAN  |
|     7878 | ADAMS     | CLERK     |
|     7900 | JAMES     | CLERK     |
|     7902 | FORD      | ANALYST   |
|     7934 | MILLER    | CLERK     |
| 17061611 | lizhitong | STUDENT   |
+----------+-----------+-----------+
14 rows in set (0.00 sec)

```


3.8 为表2增加一个约束：deptno字段需要在表1中存在；这称做什么完整性？





3.9 为表2增加一个索引：ename 字段。简述为什么要在 ename 字段建立索引
```

mysql> CREATE INDEX suoyin
    -> ON t_b2 (ename);
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

```




3.10 将表2的 sal 字段改名为 salary
```

mysql> ALTER TABLE t_b2
    -> CHANGE sal salary float;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

```
3.11 撰写一个函数 get_deptno_from_empno，输入 empno，输出对应的 deptno。 简述函数和存储过程有什么不同。



4 建立一个新用户，账号为自己的姓名拼音，密码为自己的学号；

```

mysql> CREATE USER 'lizhitong'@'localhost'
    -> IDENTIFIED BY '17061611';
Query OK, 0 rows affected (0.02 sec)

```



4.1 将表1的SELECT, INSERT, UPDATE(ename)权限赋给该账号。

```

mysql>  GRANT SELECT,INSERT,UPDATE ON *.*
    -> TO 'lizhitong'@'localhost';
Query OK, 0 rows affected (0.00 sec)

```

4.2 显示该账号权限

```

mysql> SHOW GRANTS FOR 'lizhitong'@'localhost';
+----------------------------------------------------------------+
| Grants for lizhitong@localhost                                 |
+----------------------------------------------------------------+
| GRANT SELECT, INSERT, UPDATE ON *.* TO 'lizhitong'@'localhost' |
+----------------------------------------------------------------+
1 row in set (0.00 sec)

```



4.3 `with grant option` 是什么意思。

WITH GRANT OPTION 这个选项表示该用户可以将自己拥有的权限授权给别人。

5 表 1 和表 2 这样设计是否符合第一范式，是否符合第二范式，为什么？



6 画出表 1 和表 2 所对应的 E-R 图



7 什么是外模式，什么是内模式。为什么要分成这几层？

外模式又称子模式，对应于用户级。它是某个或某几个用户所看到的数据库的数据视图，是与某一应用有关的数据的逻辑表示。外模式是从模式导出的一个子集，包含模式中允许特定用户使用的那部分数据；内模式又称存储模式，对应于物理级，它是数据库中全体数据的内部表示或底层描述，是数据库最低一级的逻辑描述，它描述了数据在存储介质上的存储方式物理结构，对应着实际存储在外存储介质上的数据库。内模式由内模式描述语言来描述、定义，它是数据库的存储观。

8 什么是ACID？

指事务的ACID特性，包括原子性、一致性、隔离性、持续性。

8.1 编写一个事务，“将 MILLER 的 comm 增加 100，如果增加后的 comm 大于 1000 则回滚”；



8.2 如何查看 MySQL 当前的隔离级别？

（1）查看当前会话隔离级别：select @@tx_isolation;

（2）查看系统当前隔离级别：select @@global.tx_isolation;

8.3 如果隔离级别为 READ-UNCOMMITED, 完成 “MILLER 的 comm 增加 100” 事务操作完成后，可能读到的结果有哪些，原因是什么？



9 有哪些场景不适合用关系型数据库？为什么？

数据量大(PB级别)而增删改查又很简单的应用。不知适合数据仓储道,那需要进行反规范化(denormalize),即把拆得很细的,符合各种范式的表重新归并专成大表.
