## Oracle第一课--创建表空间，权限管理和简单查询语句

整理一下上午的内容。之前学过Oracle，希望这次学习整理笔记的过程可以让我收获更多。


### 以默认用户（scott）登陆PLSQL

Oracle有个默认用户scott，密码为tiger，并默认锁定状态。要想以该用户登陆到scott，需要先对其解锁。解锁之前先在命令行中以system用户登录：

```
sqlplus(回车)
请输入用户名：system
输入口令：********
```
登陆system用户之后，为scott用户解锁并赋予其基本权限：
```
alter user scott account unlock
grant connect,resource to scott
若是允许scott将此系统权限传播给其他用户，可使用以下语句：
grant connect,resource to scott with admin option
注：若权限为对象权限，则应为with grant option
```
之后就可以使用scott用户登录PLSQL了，首次登陆之后，会提示口令失效，需要重置口令。

### 创建表空间
创建表空间必须要有dba权限
```
grant dba to scott
create tablespace temp0 datafile 'D:/Oracle/TEMP/tempdata.dba' size 50m next 50m maxsize 500m autoextend on;
此语句创建了一个名为temp0的表空间，对应物理的数据文件为D:/Oracle/TEMP/tempdata.dba，大小为50m,自动增长，一次增长50m，最大空间500m。
如果赋予权限之后想撤消可以用：revoke dba from scott;
（但是其实我没有赋予scott用户dba权限，不想给它这么大特权哈哈哈~）
```
###  创建/删除一个用户（CMD中）
```
create user temp identified by 123456;
grant connect,resource to temp;
conn temp/123456;(回车登陆到该用户)
create table temptable(id number);
若想删除用户需要连接到dba权限用户：
conn sys/******** as sysdba;
drop user temp cascade;
注：cascade关键字表示无论即使temp用户下还有数据库对象，也删除该用户。
如果想直接drop user temp; 需要先删除temp用户下的表temptable。
```

### 简单查询语句
scott有默认的四张表，bonus，dept,emp,salgrade.以下测试基于这四张表。
```
1. distinct
2. 别名
select distinct empno,ename as name from emp;
3. group by 
select sum(sal),min(sal) from emp group by job;
4. between...and.../in(...,...,...)/like'%%75'
5. is null/is not null
6. rownum 
select * from emp where rownum <= 5;
7. 拼接
select job||'M' from emp;
select job||'-'||sal from emp;
```
