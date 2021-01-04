# 数据库基本查询一

## 导入sql操作
    执行sql文件：新建一个逻辑空间——右键选择“运行sql文件”——导入即可
    https://blog.csdn.net/weixin_44861443/article/details/108095951

## 一、记录查找
    1、最基本的查询语句是由select和from关键字组成的
    2、select语句屏蔽了物理层的操作，用户不必关心数据的真实存储，交由数据库高效查询
    
```sql
USE demo;
SELECT ename, job FROM t_emp;
```

## 二、使用列别名
    1、通常情况下，select子句中使用了表达式，那么这列的名字就默认为表达式，因此需要一种对列名重命名的机制

```sql
# 如果sal*12不起别名，则返回默认为sal*12
SELECT
	empno,
	sal*12 AS 'income'
FROM t_emp;
```

## 三、查询语句的子句执行顺序
    1、执行时会先进行语法分析和优化，读取sql语句
    2、FROM子句优先级高（选择数据来源）
    3、最后执行SELECT子句（选择输出内容）

## 四、数据分页
    1、比如加载朋友圈，只会先加载部分信息，不用一次性加载全部信息，那样会浪费cpu时间、内存和网络宽带
    2、如果结果集的记录很多，可以使用LIMIT关键字限定结果集数量
    SELECT ......  FROM ...... LIMIT 起始位置，偏移量; （偏移量表示：返回的数据数量）
    3、数据分页简写，可默认起始位置为0

```sql
    # 前五条数据
    SELECT empno, ename FROM t_emp LIMIT 0, 5;
    # 第五条到第十条数据
    SELECT empno, ename FROM t_emp LIMIT 5, 5;
    # 默认起始位置是0
    SELECT empno, ename FROM t_emp LIMIT 10;
```

    4、执行顺序：FROM —— SELECT ——LIMIT

## 五、结果集排序
    1、如果没有设置，查询语句不会对结果集进行排序，也就是说如果需要排序，就必须使用ORDER BY子句
    2、ORDER BY 格式（默认升序）
       SELECT ...... FROM ...... ORDER BY 列名 【ASC/DESC】升序或降序;

```sql
SELECT empno, ename, sal 
FROM t_emp 
ORDER BY sal DESC;
```

    3、如果排序是数字类型，就按照数字大小排序，如果是日期就根据日期大小排序；如果是字符串就按照字符集序号排序（就是比较每个字母）

```sql
SELECT empno, ename, hiredate, deptno 
FROM t_emp 
ORDER BY hiredate;
```

    4、默认情况下，如果两条数据字段内容相同，比如两个人的工资是一样的，默认情况下是按照主键大小来排列的，也可以通过多个条件进行排序，第一个字段不满足就采用第二个字段，所有字段都不满足，自动按照主键排序

```sql
SELECT empno, ename, sal, hiredate 
FROM t_emp 
ORDER BY sal DESC,hiredate ASC;

# 工资排在前五位信息
SELECT	
	empno, ename, sal
FROM t_emp ORDER BY sal DESC LIMIT 0, 5;
```

    5、执行顺序
        ORDER BY 子句写在 LIMIT子句前面
        FROM —— SELECT —— ORDER BY —— LIMIT 

## 六、结果集中去除重复数据（不是数据表中删除重复记录）
    1、未查询主键字段，则容易出现重复数据如下查询员工表有多少种职业 

```sql
SELECT job FROM t_emp;
```

    2、去除重复记录只需要在需要去重的字段加上关键字DISTINCT
       SELECT DISTINCT 字段 FROM ......;

```sql
SELECT DISTINCT job FROM t_emp;
```

    3、注意事项
        使用DISTINCT的SELECT子句只能查询一列数据，如果查询多列，去重则失效
        DISTINCT关键字只能在SELECT子句中只能使用一次

## 七、条件查询
    1、WHERE子句实现筛选数据（普通筛选）
       格式：SELECT ... FROM ... WHERE 条件 [AND/OR] 条件...;
    
```sql
SELECT empno,ename,sal
FROM t_emp
WHERE deptno=10 AND sal>=2000;

# 10或20部门且工资大于等于2000的员工
SELECT empno,ename,sal
FROM t_emp
WHERE (deptno=10 OR deptno=20) AND sal>=2000;
```

    2、WHERE语句中的条件运算会用到四类运算符
        * 数字运算符
        * 比较运算符
        * 逻辑运算符
        * 按位运算符

### 数字运算符
|序号|表达式|意义|
|---|-----|---|
|1|+|加|
|2|-|减|
|3|*|乘|
|4|/|除|
|5|%|求模|

    注意：普通数值与null值做加减乘除，还是等于Null（10 + null = null），要想参与运算可将null值转换成0，使用函数IFNULL(null, 0)

    DATEDIFF(expr1, expr2)函数使用：可以计算两个日期之间差了多少天

```sql
# 部门为10，年收入大于15000,工龄大于20年(comm表示奖金)
SELECT empno, ename, sal, hiredate
FROM t_emp
WHERE deptno=10 AND (sal+IFNULL(comm,0))*12>=15000
AND DATEDIFF(NOW(),hiredate)/365>=20;
```

    3、比较运算符

### 比较运算符
|序号|表达式|意义|
|---|-----|---|
|1|>|大于|
|2|>=|大于等于|
|3|<|小于|
|4|<=|小于等于|
|5|=|等于|
|6|!=|不等于|
|7|IN|包含|
    
 
```sql
# 部门为10,20,30，职位不是SALESMAN，入职日期小于1985-01-01
SELECT empno, ename, job, deptno, hiredate
FROM t_emp
WHERE deptno IN(10,20,30) AND job!='SALESMAN'
AND hiredate<'1985-01-01';
```

### 比较运算符
|序号|表达式|意义|例子|
|---|-----|---|---|
|8|IS NULL|为空|comm IS NULL|
|9|IS NOT NULL|不为空|comm IS NOT NULL|
|10|BETWEEN AND|范围|sal BETWEEN 2000 AND 3000|
|11|LIKE|模糊查询|ename LIKE "A%"（%表示0到多，下划线"_"表示只匹配一个字符）|
|12|REGEXP|正则表达式|ename REGEXP "[A-Za-z]{4}"（匹配中文就写中文集）|

    比较运算符
    LIKE 和 REGEXP 是用来判断字符串的，匹配规则^表示字符串开头，$表示字符串结尾

```sql
# 佣金不为空的数据
SELECT 
	ename,comm
FROM t_emp
WHERE comm IS NOT NULL;

# 佣金为空，工资在2000到3000之间的数据
SELECT 
	ename,comm,sal
FROM t_emp
WHERE comm IS NULL
AND sal BETWEEN 2000 AND 3000; 

# 佣金为空，工资在2000到3000之间，名称包含A的数据
SELECT 
	ename,comm,sal
FROM t_emp
WHERE comm IS NULL
AND sal BETWEEN 2000 AND 3000
AND ename LIKE '%A%';

# 佣金不为空，工资在1000到3000之间，以中文开头结尾2到4个字符的数据
SELECT 
	ename,comm,sal
FROM t_emp
WHERE comm IS NOT NULL
AND sal BETWEEN 1000 AND 3000
AND ename REGEXP '^[\\u4e00-\\u9fa5]{2,4}$';
```

    4、逻辑运算符
### 逻辑运算符

|序号|表达式|意义|
|---|-----|---|
|1|AND|与关系|
|2|OR|或关系|
|3|NOT|非关系|
|4|XOR|异或关系(同为FALSE，异为TRUE)|

```sql
# 不在部门10,20的员工
SELECT
	ename,deptno
FROM t_emp
WHERE NOT deptno IN(10,20);
```

    5、二进制按位运算
    二进制位运算的实质是将参与运算的两个操作数，按对应的二进制数逐位进行逻辑运算
    SELECT 3&7;   把3和7按照二进制做逻辑运算
     0011
         &0111
    ----------------
            0011    都是1的情况下&的结果才是1    十进制3
          
|序号|表达式|意义|
|---|-----|---|
|1|&|位与关系|
|2|\|位或关系|
|3|~|取反|
|4|^|位异或|
|5|<<|左移|
|6|>>|右移|
    
    WHERE子句注意事项:
        WHERE子句中，条件执行的顺序是从左向右的，所以我们应该把索引条件，或者筛选掉记录最多的条件写在最左侧
    
    执行顺序：FROM —— WHERE —— SELECT —— ORDER BY —— LIMIT
    只有筛选出符合WHERE条件数据才能使用SELECT筛选合适的字段