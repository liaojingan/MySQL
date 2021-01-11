# 列表和元组

## 一、列表（元组）之间的累加与累乘
```python
name = ['zhangsan', 'lisi']
new_name = name + name
new_name1 = name * 2
print(new_name) # ['zhangsan', 'lisi', 'zhangsan', 'lisi']
```


## 二、列表的添加:append()函数
    1、将一个元素添加到当前列表中
    2、用法：list.append(new_item)；new_item为添加进列表的新的元素
    3、被添加的元素只会添加到末尾
    4、可修改性：是在原有列表的基础上添加，不需要额外添加新的变量
    5、可以添加任意数据类型

```python
name = ['zhangsan']
name.append('zhenzhen')
print(name) # ['zhangsan', 'zhenzhen']
```

## 四、列表和元素的count()函数
    1、返回当前列表中某个成员的个数
    2、用法：inttype = list.count(item)；item：你想查询个数的元素
    3、如果查询的成员不存在，则返回0
    4、列表只会检查完整元素是否存在需要计算的内容
   
```python
fruit_list = ['苹果', '西瓜', '香蕉', '苹果']
print(fruit_list.count('苹果')) # 2
print(fruit_list.count('苹')) # 0
```


## 五、列表中remove()函数
    1、删除列表中某个元素
    2、用法：list.remove(list)；item参数：准备删除的列表元素

```python
animal = ['cat', 'dog', 'mouse', 'chicken']
animal.remove('dog')
print('还剩余的动物有：%s' % animal)
# 打印结果：还剩余的动物有：['cat', 'mouse', 'chicken']
```  

    3、删除的元素不存在，则报错
    4、删除的元素有多个，只会删除第一个
    5、remove函数不会返回新的列表，而是在原先的列表对元素进行删除

## 六、python 的内置函数del()

    1、把变量完全删除，即删除内存
```python
animal = ['cat', 'dog', 'mouse', 'chicken']
del animal
print(animal) # NameError: name 'animal' is not defined
```


## 七、列表中reverse()函数
    1、对当前列表顺序进行反转
    2、用法：list.reverse()，无需传入参数

```python
animal = ['cat', 'dog', 'mouse', 'chicken']
animal.reverse()
print(animal) # ['chicken', 'mouse', 'dog', 'cat']
```

## 八、列表中sort()函数
    1、对当前列表按照一定规律排序
    2、用法：list.sort(key=None, reverse=False)
    key：参数比较
    reverse：排序规则；reverse=True降序；reverse=False升序，默认
    3、列表中的元素类型必须相同，否则无法排序报错，例如都是字符串、数字等
    
```python
animal = ['cat', 'dog', 'mouse', 'chicken']
animal.sort()
print(animal) # ['cat', 'chicken', 'dog', 'mouse']
```

##九、列表中clear()函数
    1、将当前列表中的数据清空
    2、list.clear() 无参数，无返回值
    
```python
animal = ['cat', 'dog', 'mouse', 'chicken']
animal.clear()
print(animal) # []
```
    3、使用clear()函数比重新赋值一个空列表更加节省性能，原因在于：clear()函数是在已经定义好内存中，直接操作内存中的变量，不涉及建立内存块过程

##十、列表的copy()函数

    1、将当前的列表复制一份相同的列表，新列表与旧列表相同，但内存空间不同
    2、用法：list.copy()，不需要传参，返回一个一模一样的列表

```python
animal = ['cat', 'dog', 'mouse', 'chicken']
new_animal = animal.copy()
print(new_animal) # ['cat', 'dog', 'mouse', 'chicken']
```

    3、copy()函数和二次赋值的区别
    二次赋值的变量与原始变量享有相同的内存空间，但是使用del删除其中一个列表，另一个列表仍然存在，因为是多个变量指向一个地址，只是删除一个则还剩下一个

```python
a = [1, 3, 5]
b = a # 二次赋值
# 这里给b或a添加或删除元素，都是同时改变的，因为享有相同内存空间
```

    copy()函数创建的新列表与原始列表不是同一内存空间，不同享数据变更
    
```python
a = [1, 4, 5]
b = a.copy()
b.append(10)
print(a) # [1, 4, 5]
print(b) # [1, 4, 5, 10]  # 不同内存空间，所以不同享数据变更
```

    copy属于浅拷贝
    通俗的说，我们有一个列表a，列表里的元素还是列表，当我们拷贝出新列表b后，无论是a还是b的内部的列表中数据发生变化之后，相互之间都会受到影响，就称为浅拷贝
    
```python
a = [[1, 3, 5], [2, 4, 6]]
b = a.copy()
print(b) # [[1, 3, 5], [2, 4, 6]]
b[0].append(10)
print(a) # [[1, 3, 5, 10], [2, 4, 6]]
print(b) # [[1, 3, 5, 10], [2, 4, 6]]
```

    deepcopy属于深拷贝
    不仅是对第一层数据进行了copy，对深层的数据也进行了copy，原始变量和新变量不是同一内存空间，不共享数据
    
```python
import copy
a = [[1, 3, 5], [2, 4, 6]]
b = copy.deepcopy(a)
print(b)
b[0].append(9)
print(a)
print(b)

# 打印结果
# [[1, 3, 5], [2, 4, 6]]
# [[1, 3, 5], [2, 4, 6]]
# [[1, 3, 5, 9], [2, 4, 6]]
```

##十二、列表中的extend()函数
    1、将其他列表或元组中的元素倒入到当前列表中
    2、用法：list.extend(iterable)，iterable参数代表列表或元组，该函数无返回值
    
```python
students = ['zhangsan', 'lisi']
new_students = ['wangwu', 'zhenzhen']
students.extend(new_students)
print(students) # ['zhangsan', 'lisi', 'wangwu', 'zhenzhen']
```

    3、如果extend传入的参数是字符串会拆分字符，如果传入字典则只显示key值

## 十三、列表的insert()添加函数
    1、将一个元素添加到当前列表的指定位置中
    2、用法：list.insert(index, new_item)；item参数：新的元素放在哪个位置（数字）；new_item参数：添加的新元素（成员）
    
```python
fruits = ['苹果', '香蕉', '荔枝']
fruits.insert(1, '芒果')
print(fruits) # ['苹果', '芒果', '香蕉', '荔枝']
```

    3、insert和append的区别
        append只能添加到列表结尾，Insert可添加到任意位置
        如果insert传入的位置不存在，则将新元素添加到列表结尾
        字符串、元组、列表元素位置是从0开始计算的
    4、当插入的位置已经存在数据，不会覆盖，会顺延展示

## 十四、索引与切片之列表

    1、什么是索引：字符串，列表和元组都有索引，从最左边记录的位置就是索引，索引用数字表示，用0开始；最大索引是他们的长度-1

```python
fruits = ['苹果', '香蕉', '荔枝']
new = fruits[0]
print(new) #  苹果
```

    2、什么是切片：
    索引用来对单个元素进行访问，切片则对一定范围内的元素进行访问
    切片通过冒号在中括号内把相隔的两个索引查找出来[0:10]
    切片规则：包左不包右
    切片后获取的列表与原始列表不是同一个列表
    
```python
num = [1, 3, 5, 7, 10, 2, 4, 6, 8]
new_num = num[0:2]
print(new_num)
print('列表的最大索引数：', len(num)-1)
print('获取完整的列表：', num[:])
print('另一种获取完整列表方法', num[0:])
print('获取除最后一个元素方法：', num[:-1])
print('列表的反序：', num[::-1])
print('列表的反向获取：', num[-3: -1])
print('通过步长获取切片：', num[0: 8:2])
print('通过切片生成空列表：', num[0: 0])

# 打印结果：包左不包右
# [1, 3]
# 列表的最大索引数： 8
# 获取完整的列表： [1, 3, 5, 7, 10, 2, 4, 6, 8]
# 另一种获取完整列表方法 [1, 3, 5, 7, 10, 2, 4, 6, 8]
# 获取除最后一个元素方法： [1, 3, 5, 7, 10, 2, 4, 6]
# 列表的反序： [8, 6, 4, 2, 10, 7, 5, 3, 1]
# 列表的反向获取： [4, 6]
# 通过步长获取切片： [1, 5, 10, 4]
# 通过切片生成空列表： []
```

    3、列表的索引、获取与修改
    list[index] = new_item  对指定索引位置修改
    数据的修改只能在存在的索引范围内；
    列表无法通过添加新的索引的方式赋值；
    
    list.index(item)   通过传入元素，查找对应索引值
    
```python
# 通过索引修改值
test = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
test[2] = 'x'
print(test)

# 通过切片修改值
test[2: 5] = 'o', 'p', 'q'
print(test)

# 通过值查找索引
name = ['lisi', 'xiaowang', 'zhangsan']
name_index = name.index('zhangsan')
print(name_index)

# 打印结果
# ['a', 'b', 'x', 'd', 'e', 'f', 'g']
#['a', 'b', 'o', 'p', 'q', 'f', 'g']
# 2
```


## 十五、列表内置pop()函数
    1、通过索引删除并获取列表的元素
    2、用法：list.pop(index)； index参数：删除列表的第几个索引
    函数会删除该索引的元素并返回
    如果传入的Index不存在则报错
    
```python
name = ['lisi', 'xiaowang', 'zhangsan']
pop_name = name.pop(1)
print(pop_name)
print(name)

# 打印结果
# xiaowang
# ['lisi', 'zhangsan']
```


## 十六、列表内置函数del()
    1、通过del删除索引
    2、用法：del list[index] ；直接删除无返回值；如果Index不存在则报错
    
```python
name = ['lisi', 'xiaowang', 'zhangsan']
del name[1]
print(name)

# 打印结果
# ['lisi', 'zhangsan']
```


## 十七、索引切片在元组中的特殊性
    1、可以和列表中一样获取索引与切片索引
    2、元组函数index和列表用法完全一致
    3、元组无法通过索引修改与删除元素，因为元组不可修改
    4、可以通过del删除整个元组，不能只删除单个元素

## 十八、字符串的索引与获取
    1、索引规则与列表相同
    2、切片和索引的获取与列表相同
    3、字符串无法通过索引修改与删除，因为字符串不可修改

## 十九、字符串中find与Index函数
    1、获取元素的索引位置
    2、用法：string.find(item)；item参数：查询个数的元素，返回索引位置(第一个字母位置)
          string.index(item)；item参数：查询个数的元素，返回索引位置
    3、find如果获取不到，返回-1
    4、index如果获取不到，直接报错
    
```python
name = 'my name is zhangsan'
new_name = name.index('is')
print(new_name)  # 8


# 字符串反序
name = 'my name is zhangsan'
new_name = name[::-1]
print(new_name)
```



