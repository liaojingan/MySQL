## 一、类和对象
    类：相当于模板
    对象：又称为实例，相当于根据模板创建出来的一个个具体实例
    类属性：类中定义的所有变量
    类方法：和函数有所不同的是类方法至少包含一个self参数，类方法无法单独使用，只能和类的对象一起使用

## 二、什么是面向对象编程
    1、利用（面向）对象（属性与方法）去进行编码的过程
    2、自定义对象数据类型就是面向对象中的类（class）的概念
    3、类（class）包括：类属性和类方法

## 三、类的关键字class
    1、类名使用驼峰命名法，也就是每个单词首字母大写
    2、类的定义：class Name(object):
                .....
                def test(self):

    3、如果想要在函数中调用类属性就需要添加self. + 类属性名称
    4、self主要用来调用类属性和其它函数
    class Name(object):
        name = 'zhenzhen'
        def test(self):
            print(self.name)  # 使用self在函数中调用类属性
    name = Name()  # 类的实例化，创建对象
    name.test()  # 调用类的函数即方法

## 四、类的参数self(主要作用：调用属性、方法)
    1、self是类函数的必传参数，且必须放在第一个参数位置
    2、self是一个对象（所以可以进行调用），他代表实例化的变量本身
    3、self 可以通过点来定义一个类变量   比如self.name = 'zhenzhen'
    4、self 中的变量与含有self参数的函数可以在类中的任何一个函数内随意调用
    5、非函数中定义的变量在定义的时候不用self 
```python
class Dog(object):
    # 定义类变量
    name = None
    age = None

    def run(self):
        # self在函数中调用类变量
        print(f'{self.name}在奔跑')

    def eat(self):
        print(f'{self.age}岁大的小狗可以吃东西了')
# 实例化创建对象
dog = Dog()
# 给类变量赋值
dog.name = 'xiaolu'
dog.age = 3
# 通过对象调用方法
dog.run()
dog.eat()

# 打印结果
# xiaolu在奔跑
# 3岁大的小狗可以吃东西了
```
    6、如果变量定义在类下面而不是类的方法下面，那这个变量既是类的属性也是类实例的属性
    7、如果变量定义在类的方法下面，如果加了self，那这个变量就是类实例的属性，不是类的属性；如果没有加self，这个变量只是这个方法的局部变量，既不是类的属性也不是类实例的属性
    8、如果在类中定义函数时加了self，那这个函数是类实例的方法，而不是类的方法。

## 五、类的构造函数
    1、类中的一种默认函数，用来将类实例化的同时，将参数传入类中
    2、构造函数的创建:def __init__(self, a, b):
    self.a = a
    self.b = b
```python
class Dog(object):

    # 定义构造函数
    def __init__(self, name, age=None):
        self.name = name
        self.age = age

    def run(self):
        # self在函数中调用类变量
        print(f'{self.name}在奔跑')

    def eat(self):
        print(f'{self.age}岁大的小狗可以吃东西了')

# 实例化创建对象同时，将构造函数中参数传入
dog = Dog(name='xiaojin', age=4)
# 通过对象调用方法
dog.run()
dog.eat()

# 打印结果
# xiaojin在奔跑
# 4岁大的小狗可以吃东西了
```

## 六、对象的生命周期
    1、实例化__init__:对象生命的开始——>同时内存中分配一块内存块（将对象放入，可进行调用、赋值等操作，前提是已经实例化）
    2、删除对象__del__:——> 同时从内存中释放这个内存块（不使用这个对象的情况：一、变量名不被绑定了；二、执行完所有程序）
    3、类实例化后，自然就存在了__del__，不需要另外定义删除对象逻辑代码

## 七、私有函数、私有变量
    什么是私有函数、私有变量
    1、无法被实例化后的对象，进行调用类中的函数与变量
    2、类内部可以调用私有函数与私有变量
    3、只希望类内部业务调用使用，不希望被使用者调用
    
    私有函数、私有变量的定义方法
    1、在变量或函数前添加“__”（两个下横线），变量或函数名后边无需添加

```python
class Cat(object):
    __cat_type = 'cat'

    def  __init__(self, name, sex):
        self.name = name
        self.__sex = sex

    def run(self):
        result = self.__run()
        print(result)

    def __run(self):
        return f'{self.__cat_type}, 小猫 {self.name} {self.__sex}开心的奔跑着'

    def jump(self):
        result = self.__jump()
        print(result)

    def __jump(self):
        return f'{self.__cat_type}, 小猫 {self.name} {self.__sex}开心的跳跃着'


class Test(object):
    pass

cat = Cat(name='米粒儿', sex='boy')
cat.run()
cat.jump()
print(dir(cat))
# 尽量不使用实例化调用私有方法和私有属性
print(cat._Cat__jump())
print(cat._Cat__cat_type)

# 打印结果
# cat, 小猫 米粒儿 boy开心的奔跑着
# cat, 小猫 米粒儿 boy开心的跳跃着
```

## 八、python中封装
    1、将不对外的私有属性或方法，通过可对外使用的函数而使用（类中定义私有的，只有类内部使用，外部无法访问）
    2、目的：保护隐私，明确区分内外
```python
class Parent(object):

    def __hello(self, data):
        print('hello %s' % data)

    def hello_world(self):
        self.__hello('world')

p = Parent()
p.hello_world()
# 打印结果
# hello world
```

## 九、装饰器
    1、作用：引入日志，屏蔽不合法程序，执行函数前预备处理，执行函数后的清理操作，权限校验、缓存等
    2、什么是装饰器：是一种函数；可以接受函数作为参数；可以返回函数；接收一个函数，内部对其处理；然后返回一个新函数，动态的增强函数功能
    将c函数在a函数中执行，在a函数中可以选择执行或不执行c函数，也可以对c函数的结果进行二次加工处理
    3、装饰的定义：def out(func_args): 外围函数（func_args要处理的函数）装饰器函数
    def inter(*args, **kwargs): 内嵌函数可变参数代表处理函数中参数
           return func_args(*args, **kwargs)
    return inter          外围函数返回内嵌函数
    4、装饰器用法
    第一种：将被调用的函数直接作为参数传入装饰器的外围函数括弧 
    第二种：将装饰器与被调用函数绑定在一起
    @符号+装饰器函数放在被调用函数的上一行，被调用函数正常定义，只需要直接调用被执行函数即可
```python
def check_str(func):
    print('func:',func)
    def inner(*args, **kwargs):
        print('args:', args, kwargs)
        result = func(*args, **kwargs)
        if result == 'ok':
            return 'result is %s' % result
        else:
            return 'result is failed: %s' % result
    return inner

@check_str
def test(data):
    return data

result= test('no')
print(result)

result = test(data='ok')
print(result)

# 打印结果
'''
func: <function test at 0x0000015E62A18E50>
args: ('no',) {}
result is failed: no
args: () {'data': 'ok'}
result is ok
'''
```

## 十、classmethod类装饰器
    1、classmethod的功能：将类函数可以不经过实例化而直接被调用
    2、用法：@classmethod
    def func(cls, ......):
        do
     参数：cls：替代普通类函数中的self ，变为cls，代表当前操作的是类
```python
class Test(object):

    def __init__(self, a):
        self.a = a

    def run(self):
        print('run')
        # 可以在self函数中执行cls函数
        self.jump()

    @classmethod
    def jump(cls):
        print('jump')
        # cls.run() 不可以在class装饰器函数中调用self函数

test = Test('A')
test.run()
# Test.run() 这样调用是错误的，因为没有进行实例化
# 这样调用是正确的，因为加上了类装饰器classmethod相当于实例化了
Test.jump()
```

## 十一、staticmethod类装饰器
    1、功能：将类函数可以不经过实例化而直接被调用，被该装饰器调用的函数不许传递self或cls参数，且无法在该函数内调用其他类函数或类变量
    2、用法：@staticmethod
    def func(.....):
        do
     参数：函数体内无cls或self参数
```python
class Test(object):

    def __init__(self, a):
        self.a = a

    def run(self):
        print('run')
        # 可以在self函数中执行cls函数
        self.jump()

    @classmethod
    def jump(cls):
        print('jump')
        # cls.run() 不可以在class装饰器函数中调用self函数

    @staticmethod
    def sleep():
        print('休息')

test = Test('A')
test.run()
# Test.run() 这样调用是错误的，因为没有进行实例化
# 这样调用是正确的，因为加上了类装饰器classmethod相当于实例化了
Test.jump()
Test.sleep()
# 实例化后也可调用staticmethod和classmethod装饰的函数
test.sleep()
```

## 十二、property功能
    1、作用：将类函数的执行免去括弧，类似于调用属性（变量）
    2、用法：@property
       def func(self):
            do
     参数介绍：无重要函数介绍
```python
class Test(object):

    def __init__(self, name):
        self.__name = name

    @property
    def name(self):
        return self.__name

    # 添加了property装饰器后，私有变量赋值的方法
    @name.setter
    def name(self, value):
        self.__name = value

t = Test(name='lisi')
print(t.name)
# 加了property不能直接实例化赋值
# print(t.name='zhangsan')
t.name = 'jingan'
print(t.name)

# 打印结果
# lisi
# jingan
```

## 十三、类的继承
    1、通过继承基类来获得基类的功能
    2、把被继承的类称作父类或基类，继承者被称为子类
    3、代码的重用
    
    父类与子类的关系
    1、子类拥有父类的所有属性和方法
    2、父类不具备子类自有属性和方法
    3、object就是一个通用父类
    4、定义子类时，将父类传入子类的参数内即可
    5、子类实例化后可以调用自己与父类的函数与变量
    6、父类无法调用子类的函数与变量
```python
class Parent(object):

    def __init__(self, name, sex):
         self.name = name
         self.sex = sex

    def talk(self):
        return f'{self.name} 在讨论'

    def is_sex(self):
        if self.sex == 'boy':
            return f'{self.name} 是boy'
        else:
            return f'{self.name} 是girl'

class ChildOne(Parent):

    def play_pingpong(self):
        return f'{self.name} is playing pingpong'

class ChildTwo(Parent):

    def play_football(self):
        return f'{self.name} is playing football'

# 继承父类后，因为父类初始化了两个参数，所以子类实例化后需要传入对应参数
c_one = ChildOne(name='lisi', sex='boy')
result = c_one.is_sex()
print(result)

c_two = ChildTwo(name='xiaofang', sex='girl')
result = c_two.is_sex()
print(result)

# 打印结果
# lisi 是boy
# xiaofang 是girl
```

## 十四、super函数
    1、作用：python子类继承父类的方法而使用的关键字，当子类继承父类后，就可以使用父类的方法
    2、用法：
```python
class Parent(object):

    def __init__(self, p):
        print('Hello, I am parent %s' % p)

class Child(Parent):

    def __init__(self, c, p):
        print('Hello, I am child %s' % c)
        # 子类调用父类的格式
        # super(当前类名, 类的实例).+ 需要调用的父类方法 + 加入父类要传入的参数，没有则不加
        super(Child, self).__init__(p)

if __name__ == '__main__':
    c = Child(c='child', p='parnet')
    
# 打印结果
# Hello, I am child child
# Hello, I am parent parnet
```
    3、super(Child, self)中两个参数在python3.0之后可以不传入

## 十五、类的多态
    1、同一功能的多状态化
    2、用法：子类中重写父类的方法
    3、使用多态以及继承父类的原因
    为了使用已经写好的类中的函数；为了保留子类中某个和父类名称一样的函数的功能，这时候，我们就用到了类的多态；可以帮助我们保留 子类中的函数功能

```python
# 父类
class LisiFather(object):
    def talk(self):
        print('lisi的父亲在讨论')

    def jump(self):
        print('lisi父亲在跳跃')

# 子类继承
class Lisi(LisiFather):
    # 重写父类方法
    def talk(self):
        print('Lisi在讨论')

lisi_f = LisiFather()
lisi_f.talk()

lisi = Lisi()
lisi.talk() #调用重写父类后的方法
lisi.jump()

# 打印结果
'''
lisi的父亲在讨论
Lisi在讨论
lisi父亲在跳跃
'''
```

## 十六、类的多重继承
    1、可以继承多个基（父）类
    2、多重继承的方法：
    将被继承的类放入子类的参数位中，用逗号隔开
    从做到右一次性继承
```python
class Car(object):
    def work(self):
        print('car will speed')

    def tool(self):
        print('tool contains desk etc')

class Food(object):
    def cake(self):
        print('cake is too sweat')

    def work(self):
        print('work is hard')

class Person(Car, Food):
    pass

if __name__ == '__main__':
    p = Person()
    p_tool = p.tool()
    p_cake = p.cake()
    # 不同类中有函数名相同方法被调用，根据继承顺序被调用
    p_work = p.work()
    # 查看子类继承调用顺序
    print(Person.__mro__)
    
# 打印结果
'''
tool contains desk etc
cake is too sweat
car will speed
(<class '__main__.Person'>, <class '__main__.Car'>, <class '__main__.Food'>, <class 'object'>)
'''
```

## 十七、类的高级函数
    1、__str__功能：如果定义了该函数，当print当前实例化对象的时候，会返回该函数的                        return信息（一般用来定义当前类的一些描述信息）
    2、用法：def __str__(self):
                return str_type
     参数：无
    返回值：一般返回对于该类的描述信息
    
    3、__getattr__功能：当调用的属性或方法不存在时，会返回该方法定义的信息，而不是直接报错
    4、用法：def __getattr__(self, key):
                print(something...)
     参数：key：调用任意不存在的属性名
     返回值：可以是任意类型也可以不进行返回

```python
class Test(object):

    def __str__(self):
        return 'this is a test class'

    def __getattr__(self, key):
        return '这个key：{}并不存在'.format(key)

t = Test()
print(t)
print(t.a)
print(t.b) 

# 打印结果
'''
this is a test class
这个key：a并不存在
这个key：b并不存在
'''
```

    5、__setattr__功能：拦截当前类中不存在的属性和值
    6、用法：def __setattr__(self, key, value):
                self.__dict__[key] = value
     参数：key：当前的属性名
     参数：value：当前的参数对应的值
     返回值：无
    7、__call__功能：本质是将一个类变成一个函数
    8、用法：def __call__(self, *args, **kwargs):
                print('call will start')
     参数：可任意传参
     返回值：与函数情况相同可有可无
```python
class Test(object):

    def __str__(self):
        return 'this is a test class'

    def __getattr__(self, key):
        return '这个key：{}并不存在'.format(key)

    def __setattr__(self, key, value):
        self.__dict__[key] = value
        # print(key, value)
        print(self.__dict__)

    def __call__(self, a):
        print('call is running')

t = Test()
print(t)
print(t.a)
print(t.b)
t.name = '张三'
t('珍珍')

# 打印结果
'''
this is a test class
这个key：a并不存在
这个key：b并不存在
{'name': '张三'}
call is running
'''
```

```python
class Test2(object):

    def __init__(self, attr=''):
        self.__attr = attr

    def __call__(self, name):
        # print('key is {} '.format(self.__attr))
        return name

    # 当调用的属性或方法不存在就会调用这个函数
    def __getattr__(self, key):
        if self.__attr:
            key = '{}{}'.format(self.__attr, key)
        else:
            key = key
        print(key)
        # 递归，再完成一次实例化
        return Test2(key)

t2 = Test2()
# 链式调用
name = t2.a.b.c('珍珍')
print(name)
result = t2.name.age.sex('ok')
print(result)

# 打印结果
'''
a
ab
abc
珍珍
name
nameage
nameagesex
ok
'''
```

```python
# coding:utf-8

"""
    学生信息库
"""
class StudentInfo(object):
    def __init__(self, students):
        self.students = students

    def get_by_id(self, student_id):
        return self.students.get(student_id)

    def get_all_students(self):
        for id_, value in self.students.items():
            print('学号：{}，姓名：{}，年龄：{}，性别：{}，班级：{}'.format(id_, value['name'], value['age'], value['sex'],
                                                         value['class_number']))
        return self.students

    def add(self, **student):
        check = self.check_user_info(**student)
        if check is not True:
            print(check)
            return
        self.__add(**student)


    def adds(self, new_students):
        for student in new_students:
            check = self.check_user_info(**student)
            if check is not True:
                print(check, student.get('name'))
                continue
            self.__add(**student)

    # 因为add和adds函数都存在判断逻辑，重新查找较慢，所以可以再定义一个私有__add函数
    def __add(self, **student):
        new_id = max(self.students) + 1
        self.students[new_id] = student

    def delete(self, student_id):
        if student_id not in self.students:
            print('{}学号不存在'.format(student_id))
        else:
            user_info = students.pop(student_id)
            print('学号{}的{}同学信息已经被删除'.format(student_id, user_info))

    def deletes(self, ids):
        for id_ in ids:
            if id_ not in self.students:
                print(f'{id_} 不存在学生库中')
                continue
            student_info = self.students.pop(id_)
            print(f'学号{id_} 学生 {student_info["name"]} 已被移除')

    def update(self, student_id, **kwargs):
        if student_id not in self.students:
            print('不存在该学生信息')
            return
        check = self.check_user_info(**kwargs)
        if check is not True:
            print(check)

        students[student_id] = kwargs
        print('同学信息更新完毕')

    def updates(self, update_students):
        for student in update_students:
            id_ = list(student.keys())[0]
            if id_ not in self.students:
                print(f'学号{id_} 不存在')
                continue
            # user_info返回的是字典值，所以下面传入的参数加上**
            user_info = student[id_]
            check = self.check_user_info(**user_info)
            if check is not True:
                print(check)
                continue
            self.students[id_] = user_info
        print('所有用户信息更新完成')

    def search_users(self, **kwargs):
        values = list(self.students.values())
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
            # 模糊匹配所以用"in"，精确匹配用"=="
            # 模糊匹配为空则返回所有数据
            if value in user[key]:
                result.append(user)
        return result

    # 程序自上而下执行，要想下面函数调用此方法，则需将此函数放在之前，如果在类中则不用放在上面
    def check_user_info(self, **kwargs):
        if 'name' not in kwargs:
            return '学生姓名不存在'
        if 'age' not in kwargs:
            return '学生年龄不存在'
        if 'sex' not in kwargs:
            return '学生性别不存在'
        if 'class_number' not in kwargs:
            return '学生班级不存在'
        return True


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

if __name__ == '__main__':
    student_info = StudentInfo(students)
    user = student_info.get_by_id(1)
    print(user)
    student_info.add(name='珍珍', age=22, sex='girl', class_number='A')
    users = [
        {'name': '李四', 'age': 23, 'sex': 'boy', 'class_number': 'B'},
        {'name': '赵莹莹', 'age': 24, 'sex': 'girl', 'class_number': 'C'}
    ]
    student_info.adds(users)
    student_info.get_all_students()
    print('--------------')
    student_info.deletes([7, 8])
    student_info.get_all_students()
    print('--------------')
    student_info.updates([
        {1: {'name': 'likun', 'age': 26, 'sex': '男', 'class_number': 'A'}},
        {9: {'name': 'jinjin', 'age': 23, 'sex': '女', 'class_number': 'A'}}
    ])
    student_info.get_all_students()
    print('-----------------')
    result = student_info.search_users(name='珍')
    print(result)
```
