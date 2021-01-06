## 一、MySQL Connector
    MySQL Connector是Python的官方驱动模块，兼容性较好
    
    安装方法一：
        下载链接：https://dev.mysql.com/downloads/connector/python/
        找到对应的Python版本的驱动模块，下载到目录中双击安装即可
        
    安装方法二：
        cmd命令窗口执行：pip install mysql-connector -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com
        
  
## 创建连接

    方法一
```python
# coding=utf-8

import mysql.connector


con = mysql.connector.connect(
    user='root',
    port='3306',
    database='demo',
    host='localhost',
    password='Lja199514'
)

con.close()
``` 

    方法二
    
```python
# coding=utf-8

import mysql.connector


config = {
    'user': 'root',
    'port': 3306,
    'database': 'demo',
    'host': 'localhost',
    'password': 'Lja199514'
}

con = mysql.connector.connect(**config)
```

## 游标（Cursor）
    MySQL Connector中的游标用来执行SQL语句，而且查询的结果集也会保存在游标中
    cursor = con.cursor()
    cursor.execute(sql语句)
    
```python
# 执行sql简单案例
# coding=utf-8

import mysql.connector


con = mysql.connector.connect(
    user='root',
    port='3306',
    database='demo',
    host='localhost',
    password='Lja199514'
)

cursor = con.cursor()
sql = 'SELECT ename,empno,hiredate FROM t_emp;'
cursor.execute(sql)
for one in cursor:
    print(one[0], one[1], one[2])
    
con.close()
```

## SQL注入攻击案例
    获取到t_user表中满足条件的所有数据
```python
# coding=utf-8

import mysql.connector


config = {
    'host': 'localhost',
    'user': 'root',
    'port': 3306,
    'password': 'Lja199514',
    'database': 'vega'
}

con = mysql.connector.connect(**config)
cursor = con.cursor()
username = '1 OR 1=1'
password = '1 OR 1=1'
sql = "SELECT COUNT(*) FROM t_user WHERE username="+username+\ 
    " AND AES_DECRYPT(UNHEX(password),'HelloWorld')="+password
cursor.execute(sql)
print(cursor.fetchone()[0])
con.close()

# 结果是2
```

    SQL注入攻击的危害：由于SQL语句是解释型语言，所以在拼接SQL语句的时候，容易被注入恶意的SQL语句
   
```python
    # 这种SQL注入就会删除满足等于id的t_news表中所有数据
id = '1 OR 1=1'
sql = 'DELETE FROM t_news WHERE id=' + id
``` 

## SQL预编译机制
    预编译SQL就是数据库提前把SQL语句编译成二进制，这样反复执行同一条sql语句的效率就会提升
    比如需要向数据插入十万条数据就可以将下面的sql语句先进行预编译转换成二进制
    
```python
sql1 = 'INSERT INTO' \
       't_emp(empno,ename,job,mgr,hiredate,sal,comm,deptno)' \
       'VALUES(%s,%s,%s,%s,%s,%s,%s,%s)'
```
    再次执行的时候只需要传入%s占位符的数据即可，这种写法就不需要每次插入都进行词法分析所以速度大大提高
    
## SQL预编译机制抵制注入攻击
    SQL语句编译的过程中，关键字已经被解析过了，所以向编译后的SQL语句传入参数，
    都被当做普通字符串处理，数据库不会解析其中注入的SQL语句
    
```python
# coding=utf-8

import mysql.connector


config = {
    'host': 'localhost',
    'user': 'root',
    'port': 3306,
    'password': 'Lja199514',
    'database': 'vega'
}

con = mysql.connector.connect(**config)
cursor = con.cursor()
username = '1 OR 1=1'
password = '1 OR 1=1'
sql = "SELECT COUNT(*) FROM t_user WHERE username=%s"\
    " AND AES_DECRYPT(UNHEX(password),'HelloWorld')=%s"
# 不是将username,password传给%s，而是先将sql变量值传给cursor.execute编译成二进制
# 然后再将username,password传给已经编译好的sql语句
cursor.execute(sql, (username, password))
print(cursor.fetchone()[0])
con.close()

sql1 = 'INSERT INTO' \
       't_emp(empno,ename,job,mgr,hiredate,sal,comm,deptno)' \
       'VALUES(%s,%s,%s,%s,%s,%s,%s,%s)'

# 结果执行后为0
```

## 事务控制
    Connector提供了非常简单的事务控制函数，注意不是通过游标进行事务函数的
    语法格式：
        con.start_transaction([事务隔离级别])
        con.commit()
        con.rollback()
        
## 异常处理
    语法格式：
    try:
        con = mysql.connector.connect(...)
        [con = start_tarnsaction()]
        ...
    except Exception as e:
        [con.rollback()]
        print(e)
    finally:
        if 'con' in dir():
            con.close()
    
```python
# coding=utf-8

import mysql.connector


try:
    con = mysql.connector.connect(
        port=3306,
        host='localhost',
        user='root',
        password='Lja199514',
        database='demo'
    )

    con.start_transaction()
    sql = 'INSERT INTO t_emp(empno,ename,job,mgr,hiredate,sal,comm,deptno)' \
          'VALUES(%s,%s,%s,%s,%s,%s,%s,%s)'
    cursor = con.cursor()
    cursor.execute(sql, (8000,'吴广','SALESMAN',None,'1982-01-11',2500,None,10))
    con.commit()

except Exception as e:
    # 防止端口号、host等错误导致无法连接报错，需要加上if判断
    if 'con' in dir():
        con.rollback()
    print(e)

finally:
    if 'con' in dir():
        con.close()
```

## 数据库连接的昂贵之处
    数据库连接是一种关键的、有限的、昂贵的资源，在并发执行的应用程序中体现的尤为突出（即创建并维持网络连接）
    
    TCP连接需要三次握手，四次挥手，然后数据库还需要验证用户信息
    
    数据库分配一个线程去接收客户端的网络连接，而且这个线程还是阻塞执行的，在创建TCP连接的过程中
    如果客户端还未发送过来握手请求，那么数据库的某一个线程就一直在等待，这是一种极大的浪费，而且
    连接创建出来还要验证登录用户信息，通过后客户端才能使用这个连接去操作数据库；
    
    另外系统中可运行的线程数是有限的，普通电脑最多就运行几千个线程，能分配给数据的线程数据并不是
    很多，所以数据库能支持的网络连接是跟线程数挂钩的，是有限的，所以像大网站一个数据库节点无法维
    持的，就要搞数据库集群
    
## 数据库连接池（Connection Pool）
    数据库连接池预先创建出一些数据库连接，然后缓存起来，避免了程序语言反复创建和销毁连接的昂贵代价
    连接池创建了不需要关闭
    
    数据库连接池语法格式：
    
```python
# coding=utf-8

import mysql.connector.pooling

config = {
    'port': 3306,
    'host': 'localhost',
    'user': 'root',
    'password': 'Lja199514',
    'database': 'demo'
}

pool = mysql.connector.pooling.MySQLConnectionPool(**config, pool_size=10)
con = pool.get_connection()
```

    实例：更新部门为20的员工底薪，加200
    
```python
# coding=utf-8

import mysql.connector.pooling
import mysql.connector.cursor

config = {
    'port': 3306,
    'host': 'localhost',
    'user': 'root',
    'password': 'Lja199514',
    'database': 'demo'
}

try:
    pool = mysql.connector.pooling.MySQLConnectionPool(**config, pool_size=10)
    con = pool.get_connection()
    con.start_transaction()
    cursor = con.cursor()
    sql = 'UPDATE t_emp SET sal=sal+%s WHERE deptno=%s'
    cursor.execute(sql, (200, 20))
    con.commit()
except Exception as e:
    if 'con' in dir():
        con.rollback()
    print(e)
```
    
    实例：删除20部门和员工信息
    
```python
# coding=utf-8

import mysql.connector.pooling


config = {
    'host': 'localhost',
    'port': 3306,
    'user': 'root',
    'password': 'Lja199514',
    'database': 'demo'
}

try:
    pool = mysql.connector.pooling.MySQLConnectionPool(**config, pool_size=10)
    con = pool.get_connection()
    con.start_transaction()
    sql = 'DELETE e,d FROM t_emp e JOIN t_dept d ON e.deptno=d.deptno WHERE d.deptno=20'
    cursor = con.cursor()
    cursor.execute(sql)
    con.commit()
except Exception as e:
    if 'con' in dir():
        con.rollback()
    print(e)
```

## 循环执行SQL语句
    游标对象中的executemany()函数可以反复执行一条SQL语句
    例如一次性插入多条数据或一次性更新多条数据
    
```python
# coding=utf-8

import mysql.connector.pooling


config = {
    'port': 3306,
    'user': 'root',
    'host': 'localhost',
    'database': 'demo',
    'password': 'Lja199514'
}

try:
    pool = mysql.connector.pooling.MySQLConnectionPool(**config, pool_size=10)
    con = pool.get_connection()
    cursor = con.cursor()
    con.start_transaction()
    sql = 'INSERT INTO t_dept(deptno,dname,loc) VALUES(%s,%s,%s)'
    data = [
        [100, 'A部门', '北京'], [101, 'B部门', '上海']
    ]
    cursor.executemany(sql, data)
    con.commit()
except Exception as e:
    if 'con' in dir():
        con.rollback()
    print(e)
```

    DML语句可以通过事务管理，DDL语句是无法通过事务管理的 
    
## 案例一

    使用INSERT语句，把部门平均底薪超过公司平均底薪的这样部门里的
    员工信息导入到t_emp_new表里面，并且让这些员工隶属于sales部门

    注意： 创建t_emp_new表，并且拷贝t_emp表的结果集
    sql = 'CREATE TABLE t_emp_new AS (SELECT * FROM t_emp)'
    
```python
# coding=utf-8

import mysql.connector.pooling


config = {
    'port': 3306,
    'user': 'root',
    'password': 'Lja199514',
    'host': 'localhost',
    'database': 'demo'
}

try:
    pool = mysql.connector.pooling.MySQLConnectionPool(**config, pool_size=10)
    con = pool.get_connection()
    cursor = con.cursor()
    con.start_transaction()
    # 先删除t_emp_new表，防止该表之前已经被创建
    drop_sql = 'DROP TABLE t_emp_new'
    cursor.execute(drop_sql)
    # 创建t_emp_new表，并且拷贝t_emp表的结果集
    # sql = 'CREATE TABLE t_emp_new AS (SELECT * FROM t_emp)'
    # 只抓取t_emp表结果，不需要拷贝数据
    sql = 'CREATE TABLE t_emp_new LIKE t_emp'
    cursor.execute(sql)

    # 使用INSERT语句，把部门平均底薪超过公司平均底薪的这样部门里的
    # 员工信息导入到t_emp_new表里面，并且让这些员工隶属于sales部门
    avg_sql = 'SELECT AVG(sal) AS avg FROM t_emp'
    cursor.execute(avg_sql)
    # 上面sql只是返回一条结果集数据所以使用fetchone()取出游标中数据
    temp = cursor.fetchone()
    # avg公司平均底薪
    avg = temp[0]

    # 部门平均底薪超过公司平均底薪
    dept_avg_sql = 'SELECT deptno FROM t_emp GROUP BY deptno HAVING AVG(sal)>=%s'
    cursor.execute(dept_avg_sql, [avg])
    # fetchall()取出游标中所有数据
    temp1 = cursor.fetchall()

    # 拼接sql语句：INSERT INTO t_emp_new SELECT * FROM t_emp WHERE deptno IN (20,10)
    sql1 = 'INSERT INTO t_emp_new SELECT * FROM t_emp WHERE deptno IN ('
    for index in range(len(temp1)):
        one = temp1[index][0]
        if index < len(temp1)-1:
            sql1 += str(one)+','
        else:
            sql1 += str(one)
    sql1 += ')'
    cursor.execute(sql1)

    sql2 = 'DELETE FROM t_emp WHERE deptno IN('
    for index in range(len(temp1)):
        one = temp1[index][0]
        if index < len(temp1)-1:
            sql2 += str(one)+','
        else:
            sql2 += str(one)
    sql2 += ')'
    cursor.execute(sql2)

    sql3 = 'SELECT deptno FROM t_dept WHERE dname=%s'
    cursor.execute(sql3, ['SALES'])
    deptno = cursor.fetchone()[0]
    sql4 = 'UPDATE t_emp_new SET deptno=%s'
    cursor.execute(sql4, [deptno])

    con.commit()
except Exception as e:
    if 'con' in dir():
        con.rollback()
    print(e)
```
    MySQL和Python交互时，书写的SQL语句要化整为零，不需要写复杂的语句
    
    
## 案例二
    
    编写一个INSERT语句向部门插入两条记录，每条记录都在部门原有最大主键值的基础上+10
    
```python
# coding=utf-8

import mysql.connector.pooling


config = {
    'port': 3306,
    'user': 'root',
    'host': 'localhost',
    'database': 'demo',
    'password': 'Lja199514'
}

try:
    pool = mysql.connector.pooling.MySQLConnectionPool(**config, pool_size=10)
    con = pool.get_connection()
    cursor = con.cursor()
    con.start_transaction()
    # sql不可写成一边查询一边插入数据，下面MAX(deptno)+20不是+10，是因为没有提交事务前，主键最大的都是不变的
    sql = 'INSERT INTO t_dept (SELECT MAX(deptno)+10,%s,%s FROM t_dept UNION SELECT MAX(deptno)+20,%s,%s FROM t_dept)'
    cursor.execute(sql, ('A部门', '北京', 'B部门', '上海'))
    con.commit()
except Exception as e:
    if 'con' in dir():
        con.rollback()
    print(e)
``` 

 