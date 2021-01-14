# 不同数据类型转换

## 一、字符串与数字之间的转换
    1、什么是类型转换，为何做类型转换
    将自身的数据类型转换成新的数据类型，并拥有新的数据类型的所有功能的过程即为数据转换
    为了方便更好的帮助处理业务，将类型变更为更适合业务场景的类型
    
    2、字符串与数字之间转换的要求
    str ——> number：字符串转为数字，这个字符串必须全部由数字组成
    number ——> str：无要求
    
    3、字符串与数字之间的转换函数
     整型    转为字符串：使用str()函数          new_str = str(345)
    浮点型   转为字符串：使用str()函数          new_str = str(345)
    字符串   转为 整型：使用int()函数           new_int = int('345')
    字符串   转为 浮点型：使用float()函数       new_float = float('3.4')

```python
# 数字转字符串
int_data = 34
float_data = 3.14
str_int_data = str(int_data)
str_float_data = str(float_data)

print(str_int_data, str_float_data, type(str_int_data), type(str_float_data))

zero_number = 0
_number = -1
str_zero_number = str(zero_number)
str_number = str(_number)
print(str_zero_number, str_number, type(str_zero_number), type(str_number))

# 字符串转数字
str_float = '3.14'
str_int = '23454'
real_float = float(str_float)
real_int = float(str_int)
print(real_float, real_int, type(real_float), type(real_int))

print(int('34.5')) # 字符串浮点类型用int()是无法转换的

# 打印结果
"""
34 3.14 <class 'str'> <class 'str'>
0 -1 <class 'str'> <class 'str'>
3.14 23454.0 <class 'float'> <class 'float'>
"""
```

## 二、字符串与列表之间的转换
    1、字符串转列表的功能函数split()
        作用：将字符串以一定规则切割成列表
        用法：string.split(sep = None, maxsplit=-1)
        参数：sep：切割的规则符号，不填写，默认空格，如字符串无空格则分割成列表
        参数：maxsplit：根据切割符号切割的次数，默认-1无限制
        返回值：返回一个列表
        注意：split()中不能传空字符串，这样写是错误的：split('')

```python
a = 'abc'
print(a.split())

b = 'a,b,cd'
print(b.split(','))

c = 'a|b|c|d' #只切割一次
print(c.split('|', 1))

info = 'my name is zhenzhen'
new_info = info.split()
print(new_info)

# 打印结果
""""
['abc']
['a', 'b', 'cd']
['a', 'b|c|d']
['my', 'name', 'is', 'zhenzhen']
""""
```

## 三、列表转字符串的函数join()

    1、作用：将列表以一定规则转换成字符串
    2、用法：'sep'.join(iterable)
        参数：sep：生成字符串用来分割列表每个元素的符号
        参数：iterable：非数字类型的列表或元组或集合
        返回值：返回一个字符串
        注意：被分割的列表里面不可以包含数字、字典、元组、布尔、True类型的（数字包括整型、浮点数），也就是说只有字符串才可以使用join函数
    3、sort()函数只针对列表，sorted针对所有
    
```python
test = ['a', 'b', 'c', 'd']
new_test = '.'.join(test)
print(new_test, type(new_test))

# 排序
sort_str = 'a b k l i o e'
sort_list = sort_str.split()
sort_list.sort()
print(sort_list)
# 转回字符串
sort_str = ' '.join(sort_list)
print(sort_str)

# 打印结果
"""
a.b.c.d <class 'str'>
['a', 'b', 'e', 'i', 'k', 'l', 'o']
a b e i k l o
"""
```

## 四、字符串与bytes的转换

    1、什么是比特类型
        二进制的数据流——bytes 
        一种特殊的字符串
        所有功能用法与字符串一样，只需要在字符串前 +b 标记
    2、dir()函数可以打印查找对应的可以使用属性和函数
        返回有下横线的则是属性例如“__add__”，没有加下横线的则是函数例如'count'
        
```python
a = 'hello zhenzhen'
b = b'hello zhenzhen'
print(a, b, type(a), type(b))

# 传入的参数需要是比特类型
print(b.replace(b'zhenzhen', b'jingan'))

# 通过索引获取，会把字符转换成二级制数据流形式
print(b[2])

# 切片返回内容跟字符串一致
print(b[:3])

print(dir(b))

"""
hello zhenzhen b'hello zhenzhen' <class 'str'> <class 'bytes'>
b'hello jingan'
108
b'hel'
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'center', 'count', 'decode', 'endswith', 'expandtabs', 'find', 'fromhex', 'hex', 'index', 'isalnum', 'isalpha', 'isascii', 'isdigit', 'islower', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'removeprefix', 'removesuffix', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
"""
```

## 五、字符串转bytes的函数——encode功能（解决bytes类型不能输入中文的问题）

    1、作用：将字符串转成比特（bytes）类型
    2、用法：编码string.encode(encoding = 'utf-8', errors = 'strict')
        参数：encoding：转换成的编码格式，如ascii，gbk，默认是utf-8
        参数：errors：出错时的处理方法，默认strict，直接抛错误，也可以选择ignore错误
        返回值：返回一个比特类型
    
```python
a = 'hello 珍珍'
print(a.encode(encoding='utf-8'))

# b'hello \xe7\x8f\x8d\xe7\x8f\x8d' （将中文转换成中文可以识别的）
```


## 六、bytes转字符串的函数——decode功能
    1、作用：将比特类型转换成字符串，decode仅存在于比特类型也是与字符串类型区别
    2、用法：解码bytes.decode(encoding='utf-8', errors='strict')
        参数：encoding：转换成的编码格式，如ascii，gbk，默认是utf-8
        参数：errors：出错时的处理方法，默认strict，直接抛错误，也可以选择ignore错误
        返回值：返回一个字符串类型 
        
```python
a = b'hello zhenzhen'
print(a.decode(encoding='utf-8'))

# 打印结果
# hello zhenzhen
```


## 七、元组、列表、集合之间的转换
    总结：字符串实际上可以转换为任何类型，但字符串转换为列表、元组、集合后是一种不可逆的转换，意思就是：再次转换回来已经不可能
         