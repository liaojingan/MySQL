## 一、包
    1、包就是文件夹，包中还可以有包，也就是子文件夹
    2、一个个python文件就是模块

## 二、包的身份证
    1、__init__.py

## 三、创建一个包
    1、要有主题，明确功能，方便使用
    2、层次分明，调用清晰

## 四、包的导入
    1、将python中某个包或模块，导入到当前的py文件中
    2、用法：import package
       参数：package
       要求：只会拿到对应包下__init__中的功能或当前模块下的功能

## 五、模块的导入from.....import...... as ....（as 后面可以重新命名，防止相同函数名被调用）
    1、功能：通过从某个包找到对应的模块
    2、用法：from package import module
       参数：package：来源的包
       参数：module：包中的目标模块
    3、在__init__.py中导入其他模块，只需要在模块名称前加上一个点“.”表示当前路径
      eg：from .cat import action

## 六、第三方包
    1、其他程序员写好的功能封装成包（模块）发布到网上
    2、提高开发效率

## 七、利用pip与easy_install获取第三方包
    1、Python的第三方管理工具，pip的使用率最高
    2、Python3.4以上版本在安装python的时候已经自带了这两种包管理工具
    3、pip install 包名
    4、github.com 搜索python第三方包
    5、pip -V 查看pip版本
    6、第一个python第三方包：ipython
    ipython是一个python的交互式shell， 比默认的python shell好用的多，支持变量自动补全，自动缩进
    ipython只是作为调试环境使用
    7、通过国内地址下载第三方包（速度较快）
    pip install -i http://pypi.douban.com/simple/ ipython   豆瓣
    pip install -i http://pypi.sdutlinux.org/ ipython 山东理工大学
    pip install -i http://pypi.hustunique.com/ ipython 华中理工大学
    pip install -i http://pypi.mirrors.ustc.edu.cn/simple/ ipython 中国科技大学
    8、pip uninstall 包名
    9、pip install 包名==版本号，指定版本安装

## 八、datatime包
    1、日期与时间的结合体-data and time
    2、获取当前时间
    导入包与模块：from datetime import datetime 或 import datetime
    使用方法：datetime.now() 或 datetime.datetime.now()   (today)
    返回：年月日时分秒毫秒的datatime对象

    3、获取时间间隔
    导入包与模块：from datetime import datetime / from datetime import timedelta
    其中导入的timedelta是函数
    使用方法：timeobj = timedelta(days=0, seconds=0, microseconds=0, milliseconds=0, minutes=0, hours=0, week=0) 
```python
from datetime import datetime
from datetime import timedelta

# 当前日期
datetime_now = datetime.now()

# 设置一天的时间间隔
day_timedelta = timedelta(days=1)
before_one_days = datetime_now - day_timedelta
print(before_one_days)

# 打印结果
# 2020-12-10 10:01:00.697849
# 2020-12-09 10:01:00.697849
```

## 九、时间对象转字符串
    1、获取时间对象
    from datetime import datetime
    now = datetime.datetime.now()
    时间转字符串：
    date_str = now.strftime(format)
```python
from datetime import datetime
from datetime import timedelta

# 当前日期
datetime_now = datetime.now()
date_str = datetime_now.strftime('%Y/%m/%d %H/%M/%S')
print(date_str, type(date_str))


# 设置一天的时间间隔
day_timedelta = timedelta(days=1)
before_one_days = datetime_now - day_timedelta
before_date_str = before_one_days.strftime('%Y:%m:%d %H:%M:%S')
print(before_date_str, type(before_date_str))

# 打印结果
# 2020/12/10 12/00/00 <class 'str'>
# 2020:12:09 12:00:00 <class 'str'>
```

## 十、时间字符串转成时间类型
    1、获取时间模块：
    from datetime import datetime
    时间字符串转时间类型：
    datetime.strptime(tt, format)
    参数：tt：符合时间格式字符串
    参数：format：tt时间字符串匹配规则
```python
from datetime import datetime
from datetime import timedelta

# 当前日期
datetime_now = datetime.now()
date_str = datetime_now.strftime('%Y-%m-%d %H-%M-%S')
print(date_str, type(date_str))

# 时间字符串转成时间对象
date_obj = datetime.strptime(date_str, '%Y-%m-%d %H-%M-%S')
print(date_obj, type(date_obj))

# 打印结果
# 2020-12-10 13-44-13 <class 'str'>
# 2020-12-10 13:44:13 <class 'datetime.datetime'>
```

## 十一、时间格式字符
|字符|介绍|
|---|---|
|%Y|	完成的年份|
|%m|	月份|
|%d|	月中某一天|
|%H|	一天中第几个小时|
|%I|	一天中第几个小时|
|%M|	当前的第几分|
|%S|	当前分的第几秒，闰年多出2秒|
|%f|	当前秒的第几毫秒|
|%a|	简化版的星期，如星期三Wed|
|%A|	完整版的星期，如星期三Wednesday|
|%b|	简化版的月份，如二月Feb|
|%B|	完整版的月份，如二月February|
|%c|	本地日期时间，如Web Feb 5 10:12:23 2020|
|%p|	显示上午下午，AM表示上午，PM表示下午|
|%j|	一年中的第几天|
|%U|	一年中的星期数|


## 十二、time包
    1、时间戳：从1970年1月1日00时00分00秒至今的总毫秒（秒）数（python默认按秒）
        timestamp 表示时间戳，是float类型
    
    2、生成时间戳函数time
        导入包：import time
        使用方法：time.time()
        返回值：秒数级别的浮点类型
    
    3、获取本地时间函数localtime
        导入包：import time
        使用方法：time.localtime(timestamp)
        参数：timestamp：时间戳（非必填），不传返回当前最新的时间对象
        localtime对应字段介绍
        
|属性名|介绍|取值范围|
|-----|---|------|
|tm_year|	四位数年|	2020|
|tm_mon|	月|	1-12|
|tm_mday|	日|	1-31|
|tm_hour|	小时|	1-23|
|tm_min|	分钟|	59|
|tm_sec|	秒|	0-61（闰月问题）|
|tm_wday|	一周的第几天|	0-6（0是周一|）
|tm_yday|	一年的第几日|	1-366（儒略历）|
|tm_isdst|	夏时令|	-1,0,1是否是夏时令|


```python
from datetime import datetime
import time

# 生成时间戳
now_time = time.time()
print(now_time, type(now_time))

# 生成本地时间
now_local = time.localtime()
print(now_local, type(now_local))

# 打印结果
'''
1607583925.8707647 <class 'float'>
time.struct_time(tm_year=2020, tm_mon=12, tm_mday=10, tm_hour=15, tm_min=5, tm_sec=25, tm_wday=3, tm_yday=345, tm_isdst=0) <class 'time.struct_time'>
'''
```

    4、暂停函数sleep
        导入包：import time
        使用方法：time.time(sleep)
        参数：sleep：希望程序被暂停的秒数
        
    5、time中strftime
        导入包：import time
        使用方法：time.strftime(format, t)
        参数：format：格式化规范 
        参数：t ：time.localtime对应的时间类型
        
    6、time中strptime
        导入包：import time
        使用方法：time.strptime(time_str, format)
        参数：time_str：符合时间格式的字符串
        参数：format：确保与time_str一致的格式化标准
```python
from datetime import datetime
import time


# 生成本地时间
now_local = time.localtime()
now_str = time.strftime('%Y-%m-%d %H:%M:%S', now_local)
print(now_str, type(now_str))

time_obj = time.strptime('2020-12-10', '%Y-%m-%d')
print(time_obj, type(time_obj))
```

    7、datetime中生成时间戳函数 
        导入包：datetime
        使用方法：now = datetime.datetime.now()
                datetime.datetime.timestamp(now)
        参数：now：datetime时间对象
    
    8、datetime时间戳转成时间对象
        导入包：datetime
        使用方法：now = datetime.datetime.now()
                datetime.datetime.fromtimestamp(now)
        参数：now：时间戳
        返回一个datetime时间对象
    
    总结：datetime包更多是对日期处理，time包更多是对时间的处理

```python
from datetime import datetime

# 生成时间戳
now = datetime.now()
now_stamp = datetime.timestamp(now)
print(now_stamp)

# 时间戳转换成时间对象
now_obj = datetime.fromtimestamp(now_stamp)
print(now_obj)

# 打印结果
# 1607587091.085822
# 2020-12-10 15:58:11.085822
```

## 十三、os文件与目录函数

|函数名|参数|介绍|举例|返回值|
|-----|---|---|---|-----|
|getcwd|	无|	返回当前路径|	os.getcwd()|	字符串|
|listdir|	path|	返回指定路径下所有的文件或文件夹|	os.listdir('c://windows')|	返回一个列表|
|makedirs|	path|	创建多级文件夹|	os.makedirs('d://test/py')|	无|
|removedirs|	path|	删除多级文件夹|	os.removedirs('d://test/py|	无|
|rename|	oldname  newname|	给文件或文件夹改名|	os.rename('d://test', d://test1)|	无|
|rmdir|	path|	只能删除空文件夹|	os.rmdir('d://test)|	无|


```python
import os


path = os.getcwd()
print(path)

list_path = os.listdir()
print(list_path)

# new_path = '%s/test/abc' % path
# os.makedirs(new_path)

# os.rename('test', 'test1')
os.removedirs('test1/abc')
```

## 十四、os.path模块常用方法

|函数名|参数|介绍|举例|返回值|
|-----|---|---|---|-----|
|exists|	path|	文件或路径是否存在|	os.path.exists('d://')|	bool类型|
|isdir|	path|	是否是路径|	os.path.isdir('d://')|	bool类型|
|isabs|	path|	是否是绝对路径|	os.path.isabs('test')|	bool类型|
|isfile|	path|	是否是文件|	os.path.isfile('d://1.py)|	bool类型|
|join|	path,  path*|	路径字符串合并|	os.path.join('d://','test')|	字符串|
|split|	path|	根据斜杠/，将最后一层路径切割|	os.path.split('d://test')|	列表|


## 十五、sys模块常用方法

|函数名|参数|介绍|举例|返回值|
|-----|---|---|---|-----|
|modules|	无|	Py启动时加载的模块|	sys.modules|	列表|
|path|	无|	返回当前Pyd 环境路径|	sys.path()|	列表|
|exit|	arg|	退出程序|	sys.exit()|	无
|getdefaultencoding|	无|	获取系统编码|	sys.getdefultencoding()|	字符串|
|platform|	无|	获取当前系统平台|	sys.platform()|	字符串|
|version(属性)|	无|	获取python版本|	sys.version|	字符串|
|argv|	*argv|	程序外部获取参数|	sys.argv|	列表|

```python
import sys

modules = sys.modules
print(modules)

path = sys.path
print(path)

code = sys.getdefaultencoding()
print(code)

print(sys.platform)
print(sys.version)

command = sys.argv[1]
if command == 'modules':
    modules = sys.modules
    print(modules)
elif command == 'path':
    path = sys.path
    print(path)
elif command == 'encoding':
    code = sys.getdefaultencoding()
    print(code)
elif command == 'platform':
    print(sys.platform)
elif command == 'version':
    print(sys.version)
else:
    print('not command')
```
