# 流程控制

## 一、逻辑判断与逻辑语句
    1、对于一件事情正确与否（真假的判断）
    2、根据判断的结果做不同的事情，就是我们的逻辑业务
    3、一个逻辑语句是又条件语句和业务语句组合而成的

## 二、if语句功能
    1、用法：if bool_result          #语法块
                do                 #业务代码块，注意缩进
    2、参数：bool_result：判断结果的真假，布尔类型
       参数：do : 如果bool_result为True时执行任意的python代码
       返回值：if是关键字，无返回值
       
```python
info = 'my name is zhenzhen'
info_list = info.split(' ')

if info_list[3] == 'zhenzhen':
    info_list[3] = 'jingan'

print(info_list)
info = ' '.join(info_list)
print(info)

# 打印结果
# ['my', 'name', 'is', 'jingan']
# my name is jingan
```

## 三、else
    1、就是对于if条件不满足的时候执行另一个代码块的入口
    2、用法：if bool_result:        
                do            
            else:
            elsedo   #else语法块，需缩进
            #缩进等级与do语法块一致            
            参数：elsedo：else语句对应Python语句块
            返回值：else属于语法，没有返回值
            
```python
url = 'www.baidu.com'
if 'baidu' in url:
    print('你已经进入百度')
else:
    url = None
print('你进入的网页是：%s' % url)

# 打印结果
# 你已经进入百度
# 你进入的网页是：www.baidu.com
```

## 四、elif（或者如果）
    1、对于命题的非第一次的多种判断，每一种判断条件对应一组业务代码
    2、返回值：无返回值
    3、条件语句满足其中一个条件后，将退出当前的条件语句
    4、每个条件语句中仅有且必须有一个if语句，可以有0个或多个elif，可以有0个或1个else语句
    5、每个条件语句 if 必须是第一个条件语句
    
```python
user = [
    ('lisi', 18, 90),
    ('xiaomo', 20, 97),
    ('limu', 19, 92)
]

xiaomo = ['xiaomo', 20, 99]
if user[0][0] == xiaomo[0]:
    xiaomo[0] = '%s_new' % xiaomo[0]
    user.append(xiaomo)
elif user[1][0] == xiaomo[0]:
    xiaomo[0] = '%s_new' % xiaomo[0]
    user.append(xiaomo)
elif user[2][0] == xiaomo[0]:
    xiaomo[0] = '%s_new' % xiaomo[0]
    user.append(xiaomo)
else:
    user.append(xiaomo)


print(user)

# 打印结果
# [('lisi', 18, 90), ('xiaomo', 20, 97), ('limu', 19, 92), # ['xiaomo_new', 20, 99]]  

user = {
    'lisi': {'age': 20, 'count': 90},
    'limu': {'age': 23, 'count': 88},
    'xiaofang': {'age':22, 'count': 92}
}

limu = ['limu1', 22, 89]

if limu[0] in user:
    limu[0] = '%s_new' % limu[0]
else:
    user[limu[0]] = {'age': limu[1], 'count': limu[2]}
print(user)

# 打印结果
{'lisi': {'age': 20, 'count': 90}, 'limu': {'age': 23, 'count': 88}, 'xiaofang': {'age': 22, 'count': 92}, 'limu1': {'age': 22, 'count': 89}}

height = float(input('请输入身高：'))
weight = float(input('请输入体重：'))
xiaoming = '小明身高为{}，体重为{}'.format(height, weight)
print(xiaoming)

BMI = weight/(height**2)
print('小明的身体状况指数为%.2f' % BMI)
if BMI < 18.5:
    print('过轻')
elif 18.5 <= BMI <= 25:
    print('正常')
elif 25 < BMI <= 28:
    print('过重')
elif 28 < BMI <= 32:
    print('肥胖')
else:
    print('严重肥胖')
    
# 打印结果
# 请输入身高：1.65
# 请输入体重：55
# 小明身高为1.65，体重为55.0
# 小明的身体状况指数为20.20
# 正常
```

## 五、for循环（有限循环）

    1、周而复始的运动或变化称为循环也叫遍历
    2、for循环：通过for关键字将列表、元组、字典、字符串中每个元素按照序列顺序进行遍历（循环）
    3、for循环用法：
        for item in iterable:              # for循环语法块
        print(item)                        # 每次循环对应的代码块 ,代码块需要缩进
        参数：iterable：可迭代的循环数据类型，例如：字符串、列表、元组、字典
        参数：item：iterable中的每一个元素（成员）
        返回值：for循环是语句，没有返回值，但在特定情况下有返回值

```python
user = ['lisi', 'zhangsan', 'limu', 'xiaojin']
for name in user:
    if name == 'limu':
        print('你好，李牧')
    else:
        print('你好{}，欢迎来到课堂'.format(name))
    print('-------------')
print('finish')

# 打印结果
"""
你好lisi，欢迎来到课堂
-------------
你好zhangsan，欢迎来到课堂
-------------
你好，李牧
-------------
你好xiaojin，欢迎来到课堂
-------------
finish
"""

w = []
l = [1, 2, 3]
s = [4, 5, 6]
for i in l:
    for j in s:
        k = i + j
        w.append(k)
        print(w)
```

## 六、字典利用items内置函数进行for循环
    1、作用：将字典转为伪列表，每个Key，value转成元组
    2、用法：for key, value in dict.items():
    print(key, value)
    参数：items无参数
    参数：key：for循环体中获取的字典当前元素的key
    参数：value：for循环体中对应当前key的value的值
    返回值：for循环不是语句，没有返回值，items返回一个伪列表 
    
```python
user = {
    'age': 23,
    'name': 'lisi',
    'score': 88
}

for key, value in user.items():
    print(key, value)

info_list = [{
    'age': 22,
    'sex': '女',
    'height': 165
}]

for info in info_list:
    print(info.get('age'))
    print(info.get('sex'))
    
# 打印结果
# age 23
# name lisi
# score 88
# 22
# 女
```

## 七、内置函数range()
    1、作用：返回的是一个一定范围的可迭代对象，元素为整型，他不是列表，无法打印信息，但可循环
    2、用法：for item in range(start, stop, step=1)
    print(item)
     参数：start：开始的数字，类似索引左边
     参数：stop：结束的数字，类似索引右边
     参数： step：步长，类似索引中第三个数
    返回值：返回一个可迭代（可循环的）以整型为主的对象

```python
for i in range(5):
    print(i)
 
# 打印结果
"""
0
1
2
3
4
"""
```

## 八、else在for循环中的使用
    1、else只有在for循环正常退出后执行，即在循环过程没有报错，没有中途停止
    
```python
for i in range(3):
    print(i)
else:
    print('循环结束')
    
# 打印结果
"""
0
1
2
循环结束
"""

numberlist = [1, 2, 3, 4, 5, 6, 7, 8, 10]
for number in numberlist:
        if number % 2 == 0:
            print('第{}个偶数是{}'.format(int(number/2), number))
            
# 打印结果
"""
第1个偶数是2
第2个偶数是4
第3个偶数是6
第4个偶数是8
第5个偶数是10
"""
```


## 九、嵌套for循环
    1、for循环中的for循环

```python
a = [1, 2, 3]
b = [4, 5, 6]
for i in a:
    for j in b:
        print(i+j)
    
# 打印结果
"""
5
6
7
6
7
8
7
8
9
"""
```


## 十、while循环（无限循环）
    1、以一定条件为基础，条件满足则无限循环，条件不满足退出循环
    2、不依赖可迭代的数据类型，而for循环依赖
    3、用法：while bool_result:
                do
     参数：bool_result：布尔类型，此处与if语法一致
     参数：do：while循环体的代码  # 需要缩进
     返回值：while循环是语句没有返回值
     
```python
index = 0
name_list = ['lisi', 'zhangsan', 'wangwu']
length = len(name_list)

while index <= length-1:
    print(name_list[index])
    index += 1
    
# 打印结果
# lisi
#zhangsan
# wangwu
```

## 十一、循环的继续与退出continue、break（只能在循环体内使用）
    1、continue功能：循环遇到continue停止本次循环，进入下一次循环
    2、用法：while bool:
            continue
            for item in itrerable:
                continue
                print(item)
     参数：continue属于语法，不需要加括号（），即可执行，无参数
     返回值，continue是语法，无返回值
    
    3、break功能：使循环正常停止遍历，这时如果循环配合了else语句，else语句将不执行
    4、用法：while bool:
                break
            for item in itrerable:
                break
                print(item)
     参数：break属于语法，不需要加括号（），即可执行，无参数
     返回值，break是语法，无返回值
    
    5、continue和break通常伴随着循环语句中的条件语句，满足某些条件可以继续执行，不满足某些条件提前结束循环
    6、在while循环中，break语句优于while逻辑体的判断
    
```python
users = [
    {'name': 'lisi', 'age': 22, 'sex': '男'},
    {'name': 'limu', 'age': 23, 'sex': '男'},
    {'name': 'xiaomeng', 'age': 21, 'sex': '女'}
]

for user in users:
    if user.get('sex') == '女':
        continue
    else:
        print('{}加入到帮忙的队列中'.format(user.get('name')))
       
# 打印结果
# lisi加入到帮忙的队列中
# limu加入到帮忙的队列中

for i in range(1, 10):
    for j in range(1, i+1):
        print('{}*{} = {}'.format(j, i, i*j), end=' ')
    print('')
    
# ---------

k = 1
while k <= 9:
    n = 1
    while n <= k:
        print('{}*{} = {}'.format(n, k, n*k), end=' ')
        n += 1
    k += 1
    print(' ')
```
