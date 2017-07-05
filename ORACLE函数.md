## Oracle函数

### 简单数值处理函数
```
1. round(x,y)和trunc(x,y),对x以y精度四舍五入/截断
  select round(12.5468,1) from dual;  --12.5
  select round(12.5468,2) from dual;  --12.55
  select trunc(12.5468,1) from dual;  --12.5
  select trunc(12.5468,2) from dual;  --12.54
  
2. NVL(x,y)：若x为空，则将x赋为y，否则保持原值。

3. ceil(x)和floor(x)对x向上/下取整数
  select ceil(2.33) from dual; --3
  select floor(2.98) from dual; --2
  
4. 其他
abs(x)--x的绝对值
sign(x)--x的符号
mod(x,y)--x对y取余
power(x,y)--x的y次方
sqrt(x)x的平方根

```

###date和timestamp日期和时间戳
```
1. select sysdate from dual;
  2017/7/5 14:37:27
2. select systimestamp from dual;
  05-7月 -17 02.37.27.347000 下午 +08:00
  
  timestamp 是oracle从date扩展出来的数据类型，包含所有date可表示的年月日时分秒信息，并且包括了秒的小数信息。
  timestamp数据类型更容易做日期的运算。
  
3. to_char(date,'YY-MM-DD HH24-MM-SS'),to_date('日期','格式')
select to_char(sysdate,'YY-MM-DD HH24:MM:SS') from dual;
select to_date('2017-12-15 12:56:32','YYYY-MM-DD HH24:Mi:SS') from dual;
  
```

### 时间运算函数
```
1. add_months(date,int)
select add_months(sysdate,3)from dual;

2. last_day()
  select last_day(sysdate) from dual;
  2017/7/31 15:05:19
  select last_day(sysdate)+1 from dual;
  2017/8/1 15:06:07
  
3. months_between(日期1，日期2)：会用日期1-日期2得到一个月份差，参数必须为date类型
select months_between(to_date('2017-01-02','yyyy-mm-dd'),to_date('2017-05-05','yyyy-mm-dd')) from dual;
  ---4.09677419354839
select months_between(to_date('2017-05-05','yyyy-mm-dd'),to_date('2017-01-02','yyyy-mm-dd')) from dual;
  ---4.09677419354839
select months_between(to_date('2017-01-02','yyyy-mm-dd'),to_date('2017-01-05','yyyy-mm-dd')) from dual;
  ----0.0967741935483871
  
4. next_day(date,char)char为星期一~星期日或1~7，指定date之后的第一个星期几，1代表周日，7代表周六。
select next_day(sysdate,7) from dual;
  --2017/7/8 15:38:09
select next_day(sysdate,'星期日') from dual;
  --2017/7/9 15:38:09

5. extract(year/month/day from date)从date中提取年月日
select extract(year from sysdate) from dual;
  --2017
select extract(month from sysdate)from dual;
  --7
select extract(day from sysdate) from dual;
  --5
```

### 字符串相关函数
```
1. chr(int)
select chr(65),chr(97) from dual;
  --A a
2. concat(str1,str2)字符串拼接
select concat('AA','bb') from dual;
  --AAbb
3. initcap(str)每个单词首字母大写
select initcap('smith is not a good guy')from dual;
  --Smith Is Not A Good Guy
4. length(str)字符串长度
select length('m哈') from dual;
  --2
5. lower(str),upper(str)
select lower('YOU ARE BED MAN') from dual;
  --you are bed man
select upper('you are bed man') from dual;
  --YOU ARE BED MAN
6. ltrim(str,substr)/rtrim(str,substr)
ltrim是从str左边开始，只要检测到substr中包含的字符，就截掉，一直到第一个不包含于substr中字符为止。
rtrim是从str右边开始，只要检测到substr中包含的字符，就截掉，一直到第一个不包含于substr中字符为止。
select ltrim('566556123456','56') from dual;
  --123456
select rtrim('1234561234655556','56') from dual;
  --1234561234
```
