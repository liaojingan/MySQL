# 字典

## 一、字典添加修改，[]处理法
    1、字典没有索引
    2、dict[ 'name' ] = 'zhenzhen'
    3、添加或修改，根据key是否存在所决定：key存在则修改，key不存在则添加

```python
user = {'username': 'zhenzhen', 'age': 23}
user['top'] = 165
print(user)

user['age'] = 22
print(user)

# 打印结果
# {'username': 'zhenzhen', 'age': 23, 'top': 165}
# {'username': 'zhenzhen', 'age': 22, 'top': 165}
```


## 二、update的功能与用法
    1、添加新的字典，如新字典中有和原字典相同的key，则该key的value会被新字典的value覆盖
    2、用法：dict.update(new_dict) ，new_dict参数：为新的字典，该函数无返回值

```python
user = {'username': 'zhenzhen', 'age': 23}
zhenzhen = {'username': '珍珍', 'age': 22, 'top': 165, 'sex': '女'}

user.update(zhenzhen)
print(user)

# 打印结果
# {'username': '珍珍', 'age': 22, 'top': 165, 'sex': '女'}
```    


## 三、setdefault的功能
    1、获取某个key的value，如key不存在于字典中，将会添加key并将value设为默认值
    2、用法：dict.setdefault(key, value)
    参数：key 需要获取的key，value 如果key不存在，对应这个key存入字典默认值
    
```python
user = {'username': 'zhenzhen', 'age': 23}
# 已存在key，则不修改
value = user.setdefault('username', 'zhenzhen')
print(user, value)

# 不存在key，则更新
value = user.setdefault('birthday', '6-25')
print(user, value)

# 打印结果
# {'username': 'zhenzhen', 'age': 23} zhenzhen
# {'username': 'zhenzhen', 'age': 23, 'birthday': '6-25'} 6-25
```


    注意：
    1、字典中key是唯一的
    2、字典中数据量没有限制
    3、字典中value可以是任何python的内置数据类型的对象和自定义对象

## 四、字典的key函数
    1、获取当前字典中所有的键（key）
    2、用法：dict.keys() 无需传参，返回一个key集合的伪列表
    伪列表：不具备列表的所有功能
    
```python
project = {'id': 1, 'name': 'house', 'process': 20}
# 生成伪列表，不具备列表所有功能
print(project.keys())

# 通过list函数将伪列表转换成列表
print(list(project.keys()))

# 打印结果
# dict_keys(['id', 'name', 'process'])
# ['id', 'name', 'process']
```


##五、字典的values函数
    1、获取当前字典中所有键值对中的值（value）
    2、用法：dict.values()；无需传参，返回一个value集合的伪列表
    
```python
project = {'id': 1, 'name': 'house', 'process': 20}
# 生成伪列表，不具备列表所有功能
print(project.values())

# 打印结果
# dict_values([1, 'house', 20])
```

## 六、字典key的获取
    1、字典+中括号内传key，不进行赋值操作即为获取，返回对应的value值

```python
project = {'id': 1, 'name': 'house', 'process': 20}
process = project['process']
print(process) # 20
```

    2、get功能：获取当前字典中指定key的value值
        用法：dict.get(key, default=None)
        参数：key 需要获取value的key；default：key不存在则返回此默认值，默认是None，我们也可以自定义
    3、[]和get的区别
        get 如果获取的key不存在，则返回默认值；[] 如果获取的Key不存在，直接报错
        get 获取方式更友善，但搜索更慢，因为需要先判断是否存在，不存在返回默认值

```python
user_info = {
    'age': 22,
    'top': 165,
    'sex': '女',
    'name': 'zhenzhen'
}

values =[]
values.append(user_info['age'])
values.append(user_info['top'])
values.append(user_info['sex'])
values.append(user_info['name'])
print(values)

# 传入的Key不存在，则显示默认值None
values.append(user_info.get('birthday'))
print(values)

# 传入的key不存在，但传入对应的值
values.append(user_info.get('habbit', 'shopping'))
print(values)

# 打印结果
# [22, 165, '女', 'zhenzhen']
# [22, 165, '女', 'zhenzhen', None]
# [22, 165, '女', 'zhenzhen', None, 'shopping']
```


## 七、clear()函数
    1、清空当前字典中所有的数据
    2、用法：dict.clear() 无参数，无返回值

## 八、pop()函数
    1、删除字典中指定的key，并将其结果返回，如果Key不存在则报错
    2、用法：dict.pop(key)；key参数：希望被删除的键，返回这个Key对应的值

## 九、字典的复制、copy函数
    1、将当前字典复制一个新的字典，和原始字典不是一个相同的内存地址
    2、用法：dict.copy() 该函数无参数，返回一个一模一样内存地址不同的字典
    
```python
fruits = {
    'apple': 30,
    'banana': 20,
    'pear': 100
}

real_fruits = fruits.copy()
print(real_fruits)

real_fruits['orange'] = 50
real_fruits.update({'cherry': 30})
print(real_fruits)

real_fruits['apple'] = real_fruits['apple'] - 5
print(real_fruits)

real_fruits.clear()
print(real_fruits)

# 打印结果
# {'apple': 30, 'banana': 20, 'pear': 100}
# {'apple': 30, 'banana': 20, 'pear': 100, 'orange': 50, 'cherry': 30}
# {'apple': 25, 'banana': 20, 'pear': 100, 'orange': 50, 'cherry': 30}
# {}
```


## 十、字典中的成员判断
    1、in 与 not in 可以运用在列表、元组、字符串、字典中，在字典中只能判断key是否存在
    2、get用于判断成员存在，value属于False类型则使用get不好判断，haskey被弃用了
    
```python
default_dic = {
    'a': None,
    'b': 1,
    'c': 0,
    'd': ''
}
print('a' in default_dic)
print(default_dic.get('a'))
print(default_dic.get('b'))

# 打印结果
# True
# None
# 1
```


## 十一、字典中的末尾删除函数：popitem
    1、删除当前字典末尾一组键值对并将其返回
    2、用法：dict.popitem() 不需要传参，返回被删除的键值对，用元组包裹0索引是key，1索引是value
    3、注意事项：如果字典为空，则直接报错

```python
students = {
    'zhenzhen': '到',
    'zhangsan': '在',
    'wangwu': '在呢',
    'lisi': '在的'
}
print('lisi 在吗')
lisi = students.popitem()
print('{} 喊 {}'.format(lisi[0],lisi[1]))

# 打印结果
# lisi 在吗
# lisi 喊 在的
```

## 十二、所有数据类型与布尔值的关系
    每一种数据类型，自身的值都有表示True与False
    not 可以对于一切结果取反 

    1、数据类型与布尔值的关系
|数据类型|为True|为False|
|------|------|------|
|int|非0|0|
|float|非0.0|0.0|
|str|len(str) != 0|len(str) == 0 即‘’|
|list|len(lsit) != 0|len(list) == 0 即[]|
|tuple|len(tuple) != 0|len(tuple) == 0 即()|
|dict|len(dict) != 0|len(dict) != 0 即{}|
|None|not None|None| 