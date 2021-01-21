## 一、异常
    1、异常就是错误
    2、异常会导致程序崩溃并停止运行
    3、能监控并捕获异常，将异常部位的程序进行修理使得程序继续正常运行
    4、异常的语法
    try:
        <代码块1> 被try关键字检查并保护的业务代码
        except <异常的类型>：# 代码块一出现错误就执行的代码
```python
def upper(str_data):
    new_str = ''
    try:
        new_str = str_data.upper()
    except:
        print('程序出错了，无法将字符串字母转为大写')
    return new_str

result = upper('new')
print(result)
```

## 二、捕获通用异常
    1、无法确定是哪种异常情况下的通用捕获方法
     2、try:
        <代码块>
      except Exception as e:
        <异常代码块>

## 三、捕获具体异常
    1、确定是哪种异常的情况下使用的捕获方法
    2、except <具体的异常类型> as e
```python
def upper(str_data):
    new_str = ''
    try:
        new_str = str_data.upper()
    except Exception as e:
        print('程序出错了：{}'.format(e))
    return new_str

result = upper(1)
print(result)

def test():
    try:
        1 / 0
        # 异常报错后，后面代码不再执行
        print('hello')
    except ZeroDivisionError as e:
        print('程序出错了', e)
test()

# 打印结果
# 程序出错了：'int' object has no attribute 'upper'
# 程序出错了 division by zero
```

## 三、捕获多个异常
    1、捕获到其中其中一个异常后，后面的异常不会再捕获
```python
# 捕获多种异常方法一
def test():
    try:
        print('try star')
        res = 1/0
        print('try finish')
    except ZeroDivisionError as e:
        print(e)
    except Exception as e:
        print('this is public except, bug is: %s' % e)
        
# 捕获多种异常方法二
# 超过一个异常时，使用元组包裹
def test():
    try:
        print('try star')
        res = 1/0
        print('try finish')
    except (ZeroDivisionError, Exception) as e:
        print(e)
```

## 四、异常类型集合
|异常名称|说明|
|------|---|
|Exception|通用异常类型（基类）|
|ZeroDivisionError|不能整除0|
|AttributeError|对象没有这个属性|
|IOError|输入输出操作失败|
|IndexError|没有当前索引|
|KeyError|没有这个键值（key）|
|NameError|没有这个变量（未初始化对象|
|SyntaxError|Python语法错误|
|SystemError|解释器的系统错误|
|ValueError|传入的参数错误|

## 五、finally
    功能：
    1、无论是否发生异常，一定会执行finally后的语法块
    2、在函数中，即便try或except中进行了return也依然会执行finally语法块
    3、try语法至少要伴随except或finally中的一个
        用法：
        try:
            <代码块>
        except:
            <代码块>
        finally
            <代码块>
    4、python2.5之前的版本，finally需要独立使用，不可以和try配合，之后才演变成现在的模式
    在程序中，如果一个段代码必须要执行，即无论异常是否产生都要执行，那么此时就需要使用finally。 
    比如文件关闭，释放锁，把数据库连接返还给连接池等
 
```python
def test():
    try:
        a = 1
        b = a/0
    except ZeroDivisionError as e:
        print('程序出错了:', e)
    finally:
        return 'finally'

test()
print('--------')

def test1():
    try:
        1/0
    except Exception as e:
        # 即使先使用了return也会执行finally
        print('test')
        return e
    finally:
        print('finally')

test1()
```

## 六、自定义抛出异常函数raise
    1、将信息以报错的形式抛出
    2、用法：raise 异常类型(message)
     参数：message：错误信息
     返回值：无返回值
```python
def test(number):
    if number == 100:
        raise ValueError('number不可以等于100')
    return number
result = test(10)
print(result)

def test2(number):
    try:
        return test(number)
    except ValueError as e:
        return e
result = test2(100)
print(result)

# 打印结果
# 10
# number不可以等于100
```

## 七、自定义异常函数
    1、继承基类——Exception
    2、在构造函数中定义错误信息
```python
# 类中继承了Exception基类，并在构造函数定义错误信息
class NameLimitError(Exception):

    def __init__(self, message):
        self.message = message

class NumberLimitError(Exception):

    def __init__(self, message):
        self.message = message

def test1(name):
    if name == '珍珍':
        raise NameLimitError('名称不可以是珍珍')
    return name

def test2(number):
    if number > 100:
        raise NumberLimitError('number不可以大于100')

try:
    test1('珍珍')
except NameLimitError as e:
    print(e)

try:
    test2(101)
except NumberLimitError as e:
    print(e)
    
# 打印结果
# 名称不可以是珍珍
# number不可以大于100
```

```python
class ShortInputException(Exception):

    def __init__(self, length, atleast):
        self.length = length
        self.atleast = atleast

def main():
    try:
        text = 'abc'
        if len(text) < 5:
            raise ShortInputException(len(text), 5)
    except ShortInputException as result:
        print('输入的长度为{},长度至少应该是{}'.format(result.length, result.atleast))
    else:
        print('没有异常发生')
    finally:
        print('输入的字符串是{}'.format(text))

main()

# 打印结果
# 输入的长度为3,长度至少应该是5
# 输入的字符串是abc
```
    如何理解什么时候需要加入异常判断
    https://www.zhihu.com/question/25530011?sort=created

## 八、断言
    1、断言的功能：assert——》用于判断一个表达式，在表达式为false的时候触发异常
    2、用法：assert expression, message
     参数：expression：表达式，一般是判断相等，或者判断是某种数据类型的bool判d断的语句
     参数：message：具体的错误信息
    3、isinstance(对比的数据，目标类型) ：用来判断数据是否符合对应的类型
    eg：isinstance(100, int)，判断100是否是int类型，符合则返回True  
```python
# coding:utf-8

"""
    学生信息库
"""
class NotArgError(Exception):
    def __init__(self, message):
        self.message = message

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
        try:
            self.check_user_info(**student)
        except Exception as e:
            raise e   # 只有一个学生，允许使用raise直接抛出
        self.__add(**student)


    def adds(self, new_students):
        for student in new_students:
            try:
                self.check_user_info(**student)
            except Exception as e:
                print(e, student.get('name'))
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
        try:
            self.check_user_info(**kwargs)
        except Exception as e:
            raise e

        students[student_id] = kwargs
        print('同学信息更新完毕')

    def updates(self, update_students):
        for student in update_students:
            try:
                id_ = list(student.keys())[0]
            except IndexError as e:
                print(e)
                continue # 如果出现异常，保证跳过这次循环可以执行下一次循环
            if id_ not in self.students:
                print(f'学号{id_} 不存在')
                continue
            # user_info返回的是字典值，所以下面传入的参数加上**
            user_info = student[id_]
            try:
                self.check_user_info(**user_info)
            except Exception as e:
                print(e)
                continue
            self.students[id_] = user_info
        print('所有用户信息更新完成')

    def search_users(self, **kwargs):
        assert len(kwargs) == 1, '参数长度必须是1'

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
            raise NotArgError('没有搜索的关键字')

        for user in values:
            # 模糊匹配所以用"in"，精确匹配用"=="
            # 模糊匹配为空则返回所有数据
            if value in user[key]:
                result.append(user)
        return result

    # 程序自上而下执行，要想下面函数调用此方法，则需将此函数放在之前，如果在类中则不用放在上面
    def check_user_info(self, **kwargs):
        assert len(kwargs) == 4, '参数必须是4个'

        if 'name' not in kwargs:
            raise NotArgError('没有发现学生姓名参数')
        if 'age' not in kwargs:
            raise NotArgError('没有发现学生年龄参数')
        if 'sex' not in kwargs:
            raise NotArgError('没有发现学生性别参数')
        if 'class_number' not in kwargs:
            raise NotArgError('没有发现学生班级参数')

        name_value = kwargs['name']
        age_value = kwargs['age']
        sex_value = kwargs['sex']
        class_number_value = kwargs['class_number']
        # isinstance(对比的数据， 目标类型) eg：isinstance(1, int)，返回布尔类型
        if not isinstance(name_value, str):
            raise TypeError('name应该是字符串')
        if not isinstance(age_value, int):
            raise TypeError('age应该是整型')
        if not isinstance(sex_value, str):
            raise TypeError('sex应该是字符串')
        if not isinstance(class_number_value, str):
            raise TypeError('class_number应该是字符串')


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


## 九、如何查找程序中bug
    1、程序中出现的错误，但又没有通过异常去获取，以至于直接抛出，导致程序的崩溃
    2、debug
