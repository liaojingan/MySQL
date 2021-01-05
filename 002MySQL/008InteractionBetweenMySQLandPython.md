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