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
```








