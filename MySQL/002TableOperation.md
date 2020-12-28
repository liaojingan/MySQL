# 数据库表的操作

## 一、什么是sql语言
    1、sql是用于访问和处理数据的标准的计算机语言


## 二、SQL语言分类
    1、DML：数据操作语言
        添加、删除、修改、查询

    2、DCL：数据控制语言
        用户、权限、事务

    3、DDL：数据定义语言
        逻辑库、数据表、视图、索引

## 三、注意事项
        sql语句不区分大小写，但是字符串区分大小写（一般关键字大写，非关键字小写）
        sql语句必须用分号结尾
        sql语句中的空白和换行没有限制，但是不能破坏语法

## 四、sql语句的注释
        方法一：#
        方法二：/*注释*/

## 五、创建逻辑库
        mysql> CREATE DATABASE 逻辑库名称;
        mysql> SHOW DATABASES;  # 查看逻辑空间
        mysql> DROP DATABASE 逻辑库名称;  # 删除逻辑空间

## 六、创建数据表DDL语句
        CREATE TABLE 数据表 (
        列名1 数据类型 [约束] [COMMENT 注释],
        列名2 数据类型 [约束] [COMMENT 注释],
        ......
        )  [COMMENT 注释];
        
```sql
        CREATE TABLE student (
        id INT UNSIGNED PRIMARY KEY,
        name VARCHAR(20) NOT NULL,
        sex CHAR(1) NOT NULL,
        birthday DATE NOT NULL,
        tel CHAR(11) NOT NULL,
        remark VARCHAR(200)
        );
```
        UNSIGNED表示无符号整数，即不可以是负数
        PRIMARY KEY 约束值不能重复
        NOT NULL 不允许为空
        CHAR(1) 固定长度的字符串
        VARCHAR(20) 不固定长度的字符串，不超过20个即可
    
        USE test; 语句运行后表示需要使用test这个逻辑库
    
## 七、数据表的其他操作
        SHOW tables;  打印逻辑空间所有名称
        DESC student;  查看具体某张表具体情况
        SHOW CREATE TABLE student; 查看创建表时的sql语句
        DROP TABLE student; 删除表
    
## 八、数据定义语言：
### 数字类型
    
| 类型 | 大小 | 说明 |
|-----|-----|-----|
|TYNYINT|1字节|小整数(8个二进制位-128 ~ 127)|
|SMALLINT|2字节|普通整数|
|MEDIUMINT|3字节|普通整数|
|INT|4字节|较大整数|
|BIGINT|8字节|大整数|
|FLOAT|4字节|单精度浮点数(对精度要求不高的，十进制转二进制丢数据)|
|DOBULE|8字节|双精度浮点数(对精度要求不高的)|
|DECIMAL|----|DECIMAL(10, 2)（对精度要求高的，例如钱的金额），以字符的形式保存，不存在转换进制丢精度的情况|
    
### 字符串类型

| 类型 | 大小 | 说明 |
|-----|-----|-----|
|CHAR|1-255字符|固定长度字符串|  
|VARCHAR|1-65535字符|不固定长度字符串|  
|TEXT|1-65535字符|不确定长度字符串，即不需要添加括号说明字符数|  
|MEDIUMTEXT|1-1千6百万字符|不确定长度字符串|  
|LONGTEXT|1-42亿字符|不确定长度字符串|  

### 日期类型

| 类型 | 大小 | 说明 |
|-----|-----|-----|
|DATE|3字节|日期（只有日期，没有时间，用横线分割“-”）|
|TIME|3字节|时间|
|YEAR|1字节|年份|
|DATETIME|8字节|日期时间|
|TIMESTAMP|4字节|时间戳|
    
## 九、修改表结构
    1、添加字段
        ALTER TABLE 表名称
        ADD 列1 数据类型 【约束】【COMMENT 注释】,
        ADD 列2 数据类型 【约束】【COMMENT 注释】,
        ......;
    
    2、修改字段类型和约束
        ALTER TABLE 表名称
        MODIFY 列1 数据类型 【约束】【COMMENT 注释】,
        MODIFY 列1 数据类型 【约束】【COMMENT 注释】,
        ......;
    解决报错：Data truncated for column 'home_tel' at row 1的方法
    http://www.bubuko.com/infodetail-3683689.html
    
    3、修改字段名称
        ALTER TABLE 表名称
        CHANGE 列1 新列名1 数据类型 【约束】【COMMENT 注释】,
        CHANGE 列1 新列名1 数据类型 【约束】【COMMENT 注释】,
        ......;
    
    4、删除字段
        ALTER TABLE 表名称
        DROP 列1，
        DROP 列2,
        ......; 
    
## 十、字段约束
    1、数据库范式
        构造数据库必须遵循一定的规则，这种规则就是范式
        目前关系型数据库有6种范式，一般情况下，只满足第三范式即可
        
    第一范式（原子性）：
        数据库基本要求，不满足这一点就不是关系型数据库
        数据表的每一列都是不可分割的基本数据项，同一列中不能有多个值，也不能存在重复 的属性，举例如下的班级“高三年级1班”还可以拆分为年级和班级所以不满足
        
        不符合第一范式：
        
|学号|姓名|班级|
|---|---|---|
|1000|刘娜|高三年级1班|

        符合第一范式：
        
|学号|姓名|年级|班级|
|---|---|---|---|
|1000|刘娜|高三|1班|
    
    第二范式（唯一性）：
        数据表中每条记录必须是唯一的，为了实现区分，通常要为表加上一个列来存储唯一标识，这个唯一属性列被称作主键列，举例如下
        
        无法区分重复数据：数据不具备唯一性
        
|学号|考试成绩|日期|
|---|------|---|
|230|58|2020-02-11|
|230|58|2020-02-11|
        
        可区分重复数据：数据具有唯一性
        
|流水号|学号|考试成绩|日期|
|----|---|------|---|
|202002110001|230|58|2020-02-11|
|202002110002|230|58|2020-02-11|
    
    第三范式（关联性）：满足了第三范式表示同时满足了第一第二范式.每列都与主键有直接关系，不存在传递依赖
        以下示例中女儿的玩具依赖于女儿，并不依赖于主键爸爸
        
|爸爸|儿子|女儿|女儿的玩具|女儿的衣服|
|---|---|---|--------|--------|
|陈华|陈浩|陈婷婷|海绵宝宝|校服|
        
        上面的表格拆分成两张表才符合第三范式

|爸爸|儿子|女儿|
|------|---|
|陈华|陈浩|陈婷婷|  
    
    依照第三范式，数据可以拆分保存到不同的数据表中，彼此保持联系
    
|女儿|女儿的玩具|女儿的衣服|
|---|--------|--------|
|陈婷婷|海绵宝宝|校服|
    
    2、mysql中的字段约束共有四种
    
|约束名称|关键字|描述|
|------|-----|---|
|唯一约束|UNIQUE|字段值唯一,且可以为NULL|
|非空约束|NOT NULL|字段值不能为NULL|
|主键约束|PRIMARY KEY|字段值唯一，且不能为NULL|
|外键约束|FOREIGN KEY|保持关联数据的逻辑性|

    主键约束 = 唯一约束 + 非空约束
    
    主键约束：建议主键一定要使用数字类型，因为数字的检索速度会非常快；如果主键是数字类型，可以设置自动增长
    CREATE TABLE t_teacher (
        id INT PRIMARY KEY AUTO_INCREMENT,
        ......
    );
    
    非空约束：NULL值是没有值，而不是空字符串
    注意：下面定义的DEFAULT FALSE表示为空时，默认为false; BOOLEAN默认映射成TYNINT类型FALSE为0；TRUE为1
    CREATE TABLE t_teacher (
        id INT PRIMARY KEY AUTO_INCREMENT,
        sex BOOLEAN NOT NULL DEFAULT FALSE,
        ......
    );
    
    唯一约束
    CREATE TABLE t_teacher (
        tel CHAR(11) NOT NULL UNIQUE,
        ......
    );
    
    注意创建表定义表名时，最好加上前缀，一般实际的表：前面加上表名第一个字母，虚拟表比如视图前面加上前缀v
    CREATE TABLE t_teacher(
        .......
    );
    
    外键约束的定义是写在子表上的
   
```sql
    # 下面是定义的员工子表，其中ENUM表示枚举，只能在规定的值中挑选的意思
    CREATE TABLE t_emp(
        empno INT UNSIGED PRIMARY KEY,
        ename VARCHAR(20) NOT NULL,
        sex ENUM('男', '女') NOT NULL,
        deptno UNSIGED,
        hiredate DATE NOT NULL,
        FOREIGN KEY (deptno) REFERENCES t_dept(deptno)
    );
    
    # 下面定义的是部门主表
    CREATE TABLE t_dept(
        deptno INT UNSIGNED PRIMARY KEY,
        danme VARCHAR(20) NOT NULL UNIQUE,
        tel CHAR(11) UNIQUE
    );
```
    
    不建议使用外键约束语法：
    外键约束闭环问题：如果形成外键闭环，我们将无法删除任何一张表的记录
    A表——》B表——》C表——》D表——》A表 
    要想删除A表数据，就得先删除B表，因为A表时主表；但B表又作为C表的主表，以此类推A表又作为D表主表所以就闭环了
    
## 十一、数据的索引机制
    1、数据排序的好处
        一旦数据排序后，查找的速度就会翻倍，数据表中的数据都是按照主键来排序的，因为主键有序所以查找速度就加快了，但是其它字段不一定有序，像姓名这种无序的就可以加上索引，以便提高查找速度
    
    2、创建索引
        方法一：创建表的时候直接定义需要添加索引的字段（二叉树二分查找）
        创建表时如果规定了索引名称则使用索引名称，如果没有规定则默认字段名作为索引名称
        
    CREATE TABLE 表名称(
        ......,
        INDEX [索引名称](字段),
        ......
    );
    
## 十二、如何添加与删除索引
    1、添加索引
        CREATE INDEX 索引名称 ON 表名(字段);
        ALTER TABLE 表名称 ADD INDEX [索引名](字段）;
    
        查看某张数据表设置了哪些索引
        SHOW INDEX FROM 表名；
    
    2、删除索引
        DROP INDEX 索引名称 ON 表名;

```sql  
    CREATE TABLE t_message(
        id INT UNSIGNED PRIMARY KEY,
        content VARCHAR(20) NOT NULL,
        type ENUM('公告', '通报', '个人通知') NOT NULL,
        create_time TIMESTAMP NOT NULL,
        INDEX idx_type (type)
    );
    
    DROP INDEX idx_type ON t_message;
    
    CREATE INDEX idx_type ON t_message(type);
    
    SHOW INDEX FROM t_message;
```  
    
## 十三、索引使用原则
    1、数据量很大，而且经常被查询的数据表可以设置索引，数据量少还设置索引，计算机还需要额外维护二叉树的开销
    2、数据量虽然很多，但是数据的写入次数远远超过查询那么也是不适合创建索引的，比如日志表，记录了很多用户操作但是业务上很少去查询日志表的数据，只是拿日志表作为行为备案
    3、索引只添加在经常被用作检索条件的字段上面，比如姓名，部门编号等
    4、不要在大字段上创建索引，比如长度超过50个字符串的，因为字符越多，排序时间越长
