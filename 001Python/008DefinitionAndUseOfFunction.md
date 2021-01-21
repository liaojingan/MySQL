## 一、函数的定义
    1、将一件事情的步骤封装到一起并得到最终结果
    2、函数名代表了这个函数要做的事情
    3、函数体实现函数功能的流程
    4、方法或功能
    5、函数可以帮助我们重复使用，通过函数名我们可以知道函数的作用

## 二、函数的分类
    1、内置函数：print、id、int、range等
    2、自定义函数

## 三、def、return关键字
    1、通过关键字def定义函数
    2、函数可以有返回值，不是必须的
    3、return将函数结果返回的关键字
    4、return只能在函数体中使用
    5、return支持返回所有的数据类型
    6、有返回值的函数可以直接赋值给一个变量
    
```python
def capitalize(data):
    index = 0
    temp = ''
    for item in data:
        if index == 0:
            temp = item.upper()
        else:
            temp += item
        index += 1
    return temp

result = capitalize('Hello zhenzhen')
print(result)

# 打印结果
# Hello zhenzhen
```

## 四、return和print区别
    1、print只是单纯的将对象打印，不支持赋值语句
    2、return是对函数执行结果的返回，也支持赋值语句
    
```python
def test():
    for i in range(10):
        if i == 5:
            return i

result = test()
print('执行结果是：',result)

# 打印结果：return相当于break，return后面语句不再执行
# 执行结果是： 5
```

## 五、必传参数
    1、必传参数：函数中定义的参数没有默认值，在调用函数时如果不传入则报错
    2、在定义函数的时候，参数后面没有等号与默认值 比如（def add(a = 1, b =2）错误
    3、总结：在定义函数的时候，没有默认值且必须在函数执行的时候传递进去的参数，且参数顺序相同，就是必传参数

## 六、默认参数
    1、定义函数时，定义参数含有默认值，通过赋值语句给他一个默认的值
    2、如果默认参数在调用函数时赋予了新的值，函数将优先使用后传入的值工作
    
```python
def add(a, b=1):
    return a + b

result = add(1)
print(result) # 2
```

## 七、不确定参数——也称为可变参数
    1、没有固定的参数名和数量（不知道要传入的参数名称具体是什么）
    2、*args：将无参数的值合并成元组
    3、**kwargs：代表将有参数与默认值的赋值语句合并成字典
    
```python
def test(*args, **kwargs):
    print(args, type(args))
    print(kwargs, type(kwargs))

test(1, 3, 5, 6, name='zhenzhen', age=23)

def test1(*args, **kwargs):
    print(args)
    print(kwargs)

a = (1, 2, 3, 5)
b = {'name': 'zhenzhen', 'age': 22}
test1(*a, **b)

# 打印结果
# (1, 3, 5, 6) <class 'tuple'>
# {'name': 'zhenzhen', 'age': 23} <class 'dict'>
# (1, 2, 3, 5)
# {'name': 'zhenzhen', 'age': 22}
```

## 八、参数规则
    1、参数的定义从左到右依次是：必传参数、默认参数、可变元组参数，可变字典参数
    2、函数的参数传递非常灵活
    3、必传参数，与默认参数的传递多样化
    优先推荐传参方式最好加上对应参数名，注意传入可变参数得加上星号*
    
```python
def add(a, b=1):
    return a + b

result = add(1, 2)
print(result)

result1 = add(a=1, b=3)
print(result1)

# 因为传入的参数有定义变量名和对应赋值，所以传参顺序可改变
result2 = add(b=4, a=2)
print(result2)

def test2(a, b=1, *args):
    print(a, b, args)

s = (1, 2)
test2(1, 2, *s)

# 一般不推荐这种顺序定义参数，就是*args参数在前
def test3(*args, a, b=1):
    print(a, b, args)

test3(a=1, b=3, *s)


def test4(a, b=3, **kwargs):
    print(a, b, kwargs)

test4(2, 4, name='zhenzhen')
test4(a=1, b=3, name='jingan')
test4(name='lisi', age=23, a=1, b=3)

d = {'name': 'xiaojin'}
test4(a=1, b=3, **d)

# 打印结果
# 3
# 4
# 6
# 1 2 (1, 2)
# 1 3 (1, 2)
# 2 4 {'name': 'zhenzhen'}
# 1 3 {'name': 'jingan'}
# 1 3 {'name': 'lisi', 'age': 23}
# 1 3 {'name': 'xiaojin'}
```

## 九、函数的参数类型定义
    1、参数类型定义方法：参数名+ 冒号 + 类型函数
    2、函数3.7之后版本可用
    3、函数不会对参数类型进行验证，即使传入不同类型也不会报错，只是提示作用
    
```python
def person(name:str, age:int = 22):
    print(name, age)

person('zhenzhen')

def test(a:int, b:int = 3, *args:int, **kwargs:str):
    print(a, b, args, kwargs)

test(1, 2, 3, name='zhenzhen')

# 打印结果
# zhenzhen 22
# 1 2 (3,) {'name': 'zhenzhen'}
```

## 十、全局变量
    1、全局变量：在Python脚本最上层代码块变量
    2、全局变量可以在函数内被读取使用，无法修改
    * 如果一个变量，既能在一个函数中使用，也能在其他的函数中使用，这样的变量就是全局变量

```python
a =300 #全局变量
def test():
    a = 100
    a += 10
    print("a的值是:%s"%a)#有局部变量，就优先使用

def test01():
    a = 200 #如果局部变量和全局变量的变量名一样，优先使用局部变量
    print("test01的值是:%s"%a)

def test02():
    print("test02的值是:%s"%a)#没有局部变量所以就调用了全局变量

test()
test02()
test01()
print(a)
"""
a的值是:110
test02的值是:300
test01的值是:200
300
"""
```


    * 如果要使用其他函数中的值，可以先用return返回，然后再作为参数传入

```python
a =300
def test():
    a = 100
    a += 10
    print("a的值是:%s"%a)
    return a

def test01():
    a = 200
    print("test01的值是:%s"%a)

def test02(a):
    print("test02的值是:%s"%a)

b = test()
test02(b)
print(a)
```


## 十一、 局部变量
    局部变量，就是在函数内部定义的变量
    不同的函数，可以定义相同的名字的局部变量，但不会产生影响
    局部变量的作用，为了临时保存数据需要在函数中定义变量来进行存储，这就是它的作用

```python
def test():
    a = 100
    a += 10
    print("a的值是:%s"%a)
    
test()
print(a)
"""
因为定义的变量a为局部变量作用范围在该函数中，print(a)不在该函数中，所以并不执行。
"""
```

## 十二、global
    1、global只支持数字、字符串、空类型，布尔类型，其余类型是不生效的
    2、函数体中修改全局变量使用global
    
```python
a = 666

def test1():
    global a
    print("全局变量修改前a的值是%s"%a)
    a = 100
    print("全局变量修改后a的值是%s"%a)

def test2():
    print("最后全局变量a的值是%s"%a)

test1()
test2()
'''
全局变量修改前a的值是666
全局变量修改后a的值是100
最后全局变量a的值是100
'''
```

## 十三、递归函数
    1、一个函数不停的反复调用执行
    2、用法： def test(a):
    print(a)
    return test(a)  # 返回的是自身
    3、需要满足两个条件：
    一、函数内部调用自身
    二、具有退出循环，即递归边界条件
    
    计算阶乘 n! = 1 * 2 * 3 * ... * n
    
```python
def cal_num(num):
    #定义的这个函数本身就是为了计算阶乘的,比如要计算n~(n-1)的阶乘
    # 只需要n * cal_num(n-1)后面只需要调用函数本身计算阶乘即可
    if num > 1:
        result = num * cal_num(num - 1)
        return result
    else:
        result = 1 #num=1即为边界
        return result

print(cal_num(39))
```

    斐波那契数列指的是这样一个数列 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233，377，610，........
    特点： 前面两个数的和等于第三个数

```python
def get_num(num):
    if num > 2:
        return get_num(num-1)+ get_num(num-2)
    else:
        result = 1
        return result

nums = []
for i in range(1 , 21):
    nums.append(get_num(i))

print(nums)
``` 

## 十四、匿名函数
    1、lambda功能：定义一个轻量化函数
    2、即用即删除，很适合完成一个功能，但此功能只在此处使用
    3、匿名函数的两种定义方法
    无参数：f = lambda : value
    f()
      有参数：lambda x,y : x*y
    f(3,5)

```python
test = lambda : 1
result = test()
print(result)

test1 = lambda x, y: x + y
print(test1(2, 4))

# 必传参数一定要在前
test2 = lambda x, y=3: x + y
print(test2(2))
```

    应用场景

```python
user = [
    {'name': 'zhenzhen'},
    {'name': 'jingan'},
    {'name': 'lisi'}
]

# x 代表user中的每个成员，通过name排序
user.sort(key=lambda x : x['name'])
print(user)

# 打印结果
[{'name': 'jingan'}, {'name': 'lisi'}, {'name': 'zhenzhen'}]
```

    案例练习
```python
# coding:utf-8

"""
    学生信息库
"""

students = {
    1: {
        'name': 'zhenzhen',
        'age': 23,
        'class_number': 'A',
        'sex': 'girl'
    },
    2: {
        'name': 'jingan',
        'age': 23,
        'class_number': 'A',
        'sex': 'boy'
    },
    3: {
        'name': 'lisi',
        'age': 24,
        'class_number': 'B',
        'sex': 'girl'
    },
    4: {
        'name': 'xiaofang',
        'age': 20,
        'class_number': 'C',
        'sex': 'girl'
    },
    5: {
        'name': 'zhaoyun',
        'age': 21,
        'class_number': 'B',
        'sex': 'boy'
    }
}

# 程序自上而下执行，要想下面函数调用此方法，则需将此函数放在之前
def check_user_info(**kwargs):
    if 'name' not in kwargs:
        return '学生姓名不存在'
    if 'age' not in kwargs:
        return '学生年龄不存在'
    if 'sex' not in kwargs:
        return '学生性别不存在'
    if 'class_number' not in kwargs:
        return '学生班级不存在'
    return True

def get_all_students():
    for id_, value in students.items():
        print('学号：{}，姓名：{}，年龄：{}，性别：{}，班级：{}'.format(id_, value['name'], value['age'], value['sex'], value['class_number']))
    return students

# result = get_all_students()
# print('----', result)

def add_student(**kwargs):
    check = check_user_info(**kwargs)
    if check != True:
        print(check)

    id_ = max(students) + 1

    students[id_] = {
        'name': kwargs['name'],
        'age': kwargs['age'],
        'sex': kwargs['sex'],
        'class_number': kwargs['class_number']
    }

# add_student(name='小明', age=22, sex='男', class_number='A')
# get_all_students()

def delete_student(student_id):
    if student_id not in students:
        print('{}学号不存在'.format(student_id))
    else:
        user_info = students.pop(student_id)
        print('学号{}的{}同学信息已经被删除'.format(student_id, user_info))
# delete_student(1)
# get_all_students()

def update_student(student_id, **kwargs):
    if student_id not in students:
        print('不存在该学生信息')
        return
    check = check_user_info(**kwargs)
    if check != True:
        print(check)

    students[student_id] = kwargs

def get_user_by_id(student_id):
    return students.get(student_id)


def search_user(**kwargs):
    values = list(students.values())
    print(values)
    key = None
    value = None
    result = []

    if 'name' in kwargs:
        key = 'name'
        value = kwargs[key]
    elif 'age' in kwargs:
        key = 'age'
        value = kwargs[key]
    elif 'sex' in kwargs:
        key = 'sex'
        value = kwargs[key]
    elif 'class_number' in kwargs:
        key = 'class_number'
        value = kwargs[key]
    else:
        print('没有搜索的关键字')

    for user in values:
        if user[key] == value:
            result.append(user)
    return result

users = search_user(age=23)
print(users)
```


