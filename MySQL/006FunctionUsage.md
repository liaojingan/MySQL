# MySQL函数
    分类：数字函数、字符函数、日期函数、条件函数
    
## 数字函数
|函数|功能|用例|
|---|---|---|
|ABS|绝对值|ABS(-100)|
|ROUND|四舍五入|ROUND(4.54)|
|FLOOR|强制舍位到最近的整数|FLOOR(9.9)|
|CEIL|强制进位到最近的整数|CEIL(3.2)|
|POWER|幂函数|POWER(2,3)|
|LOG|对数函数|LOG(7,3)|
|LN|对数函数|LN(10)|
|SQRT|开平方|SQRT(9)|
|PI|圆周率|PI()|
|SIN|三角函数|SIN(1)|
|COS|三角函数|COS(1)|
|TAN|三角函数|TAN(1)|
|COT|三角函数|COT(1)|
|RADIANS|角度转换弧度|RADIANS(30)|
|DEGREES|弧度转换角度|DEGREES(1)|

```sql
SELECT SIN(RADIANS(30));
SELECT COS(RADIANS(30));
```

## 日期函数
    1、获取系统日期和时间函数
        NOW()函数获取系统的日期和时间，格式yyyy-MM-dd hh:mm:ss
        数据库最小支持的时间单位是秒
    
    2、只获取当前系统日期函数
        CURDATE()函数能获取当前系统日期，格式yyyy-MM-dd
    
    3、只获取当前系统时间函数
        CURTIME()函数能获取当前系统时间，格式hh:mm:ss
        
```sql
SELECT NOW(),CURDATE(),CURTIME();
```

    4、日期格式化函数一
        DATE_FORMAT()函数用于格式化日期，返回用户想要的日期格式
        语法格式：DATE_FORMAT(日期,表达式)
        
```sql
SELECT ename,DATE_FORMAT(hiredate,'%Y') AS year FROM t_emp;
```

    日期格式化函数
    注意：%w中0表示星期天；%r表示小时分钟秒(12小时制)

|占位符|作用|
|----|----|
|%Y|年份|
|%m|月份|
|%d|日期|
|%w|星期(数字)|
|%W|星期(名称)|
|%j|本年第几天|
|%U|本年第几周|
|%H|小时(24)|
|%h|小时(12)|
|%i|分钟|
|%s|秒|
|%r|时间(r)|
|%T|时间(24)|

```sql
# 利用日期函数，查询明年你的生日是星期几
SELECT DATE_FORMAT('2021-01-04','%W');

# 利用日期函数，查询1981年上半年入职员工有多少人
SELECT COUNT(*)
FROM t_emp
WHERE DATE_FORMAT(hiredate,'%Y')='1981'
AND DATE_FORMAT(hiredate,'%m')<=6;
```

    5、日期计算的注意事项
        MySQL数据库里面，两个日期不能直接加减，日期也不能与数字加减，语法不会报错但计算是错误的
        
    6、日期偏移计算函数
        DATE_ADD()可实现日前向前或向后偏移的计算，时间单位灵活
        语法格式：DATE_ADD(日期, INTERVAL 偏移量 时间单位)——》注意INTERVAL后参数没有逗号分隔的
        

```sql
SELECT DATE_ADD(NOW(),INTERVAL 30 DAY);
# 计算6个月零3天前日期，使用嵌套
SELECT DATE_ADD(DATE_ADD(NOW(),INTERVAL -6 MONTH), INTERVAL -3 DAY);
```

    7、计算日期之间相隔的天数
        DATEDIFF()函数计算两个日期之间相差的天数
        DATEDIFF(日期,日期)

## 字符函数
    1. STIR(test,'A')是用来判断A字符串是否出现在test这个字段中
       INSERT('你好',1,0,'先生') 表示将'先生'插入到'你好'前面，1表示要插入字符串的位置，0表示不替换，要想替换则输入其它数值表示偏移量
       REPLACE('你好先生','先生','女士') 将'女士'替换为'先生'
       
|函数|功能|用例|
|---|---|---|
|LOWER|转换小写字符|LOWER(NAME)|
|UPPER|转换大写字符|UPPER(name)|
|LENGTH|字符数量|LENGTH(test)|
|CONCAT|连接字符串|CONCAT(sal,'$')|
|INSTR|字符出现的位置|STIR(test,'A')|
|INSERT|插入/替换字符|INSERT('你好',1,0,'先生')|
|REPLACE|替换字符|REPLACE('你好先生','先生','女士')|
|SUBSTR|截取字符串|SUBSTR(3,4)|
|SUBSTRING|截取字符串|SUBSTRING(3,4)|
|LPAD|左侧填充字符|LPAD('HELLO',10,'*')|
|RPAD|右侧填充字符|RPAD('HELLO',10,'*'|
|TRIM|去除首位空格|TRIM('你好先生')|

```sql
SELECT
	LOWER(ename),UPPER(ename),LENGTH(ename),
	CONCAT(sal,'$'),INSTR(ename,'A')
FROM t_emp;

# 结果*******3101
SELECT LPAD(SUBSTRING('18824123101',8,4),11,'*');

# 1个中文需要3个字符，所以除以3
SELECT RPAD(SUBSTRING('王珍珍',1,1),LENGTH('王珍珍')/3,'*');
```

## 条件函数
    1. SQL语句可以利用条件函数来实现编程语言中的条件判断
        IFNULL(表达式,值) 判断值是否是NULL
        IF(表达式,值1,值2) 类似于三元运算符，表达式为真则为值1，为假则为值2
        
```sql
# SALES部门发放礼品A，其余部门发放礼品B
# 只能在SELECT子句做筛选条件
SELECT
	e.empno,e.deptno,d.dname,
	IF(d.dname='SALES','礼品A','礼品B')
FROM t_emp e JOIN t_dept d ON e.deptno=d.deptno;
```

    2. 条件语句
        复杂的条件判断可以用条件语句实现，比IF语句功能更加强大
        语法格式一：满足哪个表达式就返回哪个值
        CASE
            WHERE 表达式 THEN 值1
            WHERE 表达式 THEN 值2
            ...
            ELSE 值2
        END 
        
```sql
# SALES部门去p1地点
# ACCOUNTING部门去p2地点
# RESEARCH部门去p3地点

SELECT e.ename,e.deptno,
	CASE
	WHEN d.dname='SALES' THEN 'p1'
	WHEN d.dname='ACCOUNTING' THEN 'p2'
	WHEN d.dname='RESEARCH' THEN 'p3'
	END AS place
FROM t_emp e JOIN t_dept d 
ON e.deptno=d.deptno;
```
    练习:公司决定为员工调整基本工资,具体调整方案如下:
    
|序号|条件|涨幅|
|---|---|---|
|1|SALES部门中工龄超过20年|10%|
|2|SALES部门中工龄不满20年|5%|
|3|ACCOUNTING部门|+300元|
|4|RESEARCH部门里低于部门平均底薪|+200元|
|5|没有部门的员工|+100元|

```sql
UPDATE t_emp e LEFT JOIN t_dept d ON e.deptno=d.deptno
LEFT JOIN (SELECT deptno,AVG(sal) avg FROM t_emp GROUP BY deptno) t
ON e.deptno=t.deptno
SET e.sal=(
	CASE 
		WHEN d.dname='SALES' AND DATEDIFF(NOW(),e.hiredate)/365>=20 THEN e.sal*1.1
		WHEN d.dname='SALES' AND DATEDIFF(NOW(),e.hiredate)/365<20 THEN e.sal*1.05
		WHEN d.dname='ACCOUNTING' THEN sal+300
		WHEN d.dname='RESEARCH' AND e.sal<t.avg THEN e.sal+200
		WHEN d.dname IS NUll THEN e.sal+100
		ELSE sal
	END 
);
```






 

