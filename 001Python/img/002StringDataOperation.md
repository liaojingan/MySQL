## 一、什么是对象
    1、python中一切都是对象
    2、类就相当于一个模板，对象就是根据模板造出来，每个对象都有各自的方法和属性
    比如飞机图纸（类）就相当于模板，而根据图纸造出来的真实飞机就是（对象）；
    真实飞机上的零件机舱、飞行翼、轮子就是属性（相当于名词）；
    真实飞机可以进行飞行、加速、减速、降落就是方法（相当于动词）

## 二、字符串中capitalize函数
    1、capitalize的功能：将字符串首字母大写，其余字母小写
    2、用法：newstr = string.capitalize()，参数：函数括号弧内什么都不用填写
    3、对象+"."+函数 称为：调用函数
    
```python
name = 'zhenzhen'
new_name = name.capitalize()
print(new_name)   #  Zhenzhen
```
    4、capitalize注意事项：只对第一个字母有效，只对字母有效，已经是大写则无效
    
## 三、casefold和lower
    1、将字符串全体字母小写
 
```python
name = "ZHENZHEN"
new_name = name.casefold()
print(new_name)   # zhenzhen
```
    2、只对字符串中字母有效；已经是小写则无效
    3、casefold是python3.3版本后引入的，拥有将更多语种转换为小写，如德语 
    4、输出打印的都是新变量，原始字符串变量未改变
    
## 四、字符串的upper()函数
    1、将字符串全体大写
    2、用法：无需传入参数
    
```python
name = 'zhenzhen'
name_upper = name.upper()
print(name_upper)   # ZHENZHEN
```

    3、只对字符串字母有效，已经大写则无效

## 五、字符串中swapcase()函数
    1、将字符串中的大写转换为小写，小写转换为大写
    2、用法无需传入参数
    
```python
name = 'Zhenzhen'
name_swapcase = name.swapcase()
print(name_swapcase)  # zHENZHEN
```
    3、只对字符串中的字母有效
    
## 六、字符串中zfill()函数
    1、为字符串定义长度，如不满足，缺少的部分用0填补
    2、参数：width 需传入新字符串需要的长度参数
    
```python
name = 'Zhenzhen'
name_zfill = name.zfill(10)
print(name_zfill)  ## 00Zhenzhen
```

    3、与字符串的字符无关；定义长度小于当前长度，不发生变化

##七、字符串中count()函数
    1、返回当前字符串中某个成员（元素）的个数
    2、用法：inttype = string.count(item)   参数：item，想要查询个数的元素
    3、如果查询元素不存在，则返回0
  
```python
name = 'my name is zhenzhen'
name_count = name.count("z")
name_count1 = name.count("c")
print(name_count)     # 2
print(name_count1)    # 0
```

## 八、字符串中startswith()和endswith()函数
    1、startswith 判断开始位置是否是某成员（元素）
    2、endswith 判断结尾位置是否是某成员（元素）
    3、用法：需传入一个item参数，也就是想匹配的元素，返回布尔值
    
```python
name = 'my name is zhenzhen'
name_startswith = name.startswith('y')
name_endswith = name.endswith('n')
print(name_startswith)   # False
print(name_endswith)     # True
```

## 九、字符串中find()和index()函数
    1、find和Index都是返回你想寻找的成员位置
    2、用法：
    string.find(item)传入你想查询的元素参数；返回一个整型
    string.index(item)传入你想查询的元素参数；返回一个整型或者报错ValueError
    find找不到元素，会返回-1
    3、查找的元素有多个时，也只返回从左往右的第一个
    
```python
name = "zhenzhen"
name_find = name.find('z')
name_index = name.index('h')
print(name_find)  # 0
print(name_index) # 1
```

## 十、字符串中strip()，lstrip()，rstrip()函数
    1、strip去掉字符串左右两边的指定元素、默认是空格
    2、用法：需传入你想要去掉的元素、不填默认则是空格
    3、传入的元素如果不在开头或结尾则无效
    
```python
name = " my name is zhenzhen "
name_strip = name.strip()
print(name)
print(name_strip)
# 返回结果
# my name is zhenzhen 
# my name is zhenzhen

# 直接传入定义的字符串变量则全部被清空
name_strip01 = name.strip(name)
print(name_strip01)
```

## 十一、字符中replace()函数
    1、将字符串中旧的元素，替换成新的元素，且可指定数量
    2、用法：string.replace(old, new, max)
    old：被替换的元素
    new：替换old的元素
    max：可选，代表替换几个，默认替换全部匹配的old元素
    
```python
name = "hello jingan"
new_name = name.replace("jingan", "zhenzhen")
new_name1 = name.replace("l", "y", 1)
print(new_name)  # hello zhenzhen
print(new_name1) # heylo jingan
```

    注意：链式写法：为什么可以这样书写，原因在于第一个使用替换函数返回的是字符串，字符串可以再次调用替换函数
    
```python
# 链式写法：敏感字符替换
info = ('该剧讲述了渝州城永安当的小伙计景天和唐门大小姐雪见受到两人随'
        '身玉佩的彼此吸引，他们二人“热闹而又尴尬”地相识了，成了一对欢'
        '喜冤家。')
a = "玉佩"
b = "冤家"
c = "*"
d = "&"
new_info = info.replace(a, c).replace(b, d)
print(new_info)
```

## 十二、字符串中返回bool类型的函数集合
    1、isspace() 判断字符串是否是一个由空格组成的字符串(由空格组成的字符串，不是空字符串)
    2、用法：booltype = sting.isspace() 不需要传入参数，返回布尔类型
    
```python
name = "  "
print(name.isspace())# True
```

    1、istitle() 判断字符串是否是一个标题类型（比如每个单词首字母大写这种格式），该函数只用于英文
    2、用法：booltype = string.istitle() 不需要传入参数，返回布尔类型
    
```python
name = "Hello Zhenzhen"
print(name.istitle())# True
```

    1、isupper()和islower() 判断字符串中字母是否都是大写或者小写
    2、booltype = string.isupper() 不需要传入参数，返回布尔类型，islower同理
    3、只检测字符串中的字母，对其他字符不做判断
    
```python
name = "Hello Zhenzhen"
new_name = name.isupper()
print(new_name)  # False
```

## 十三、join和split

## 十四、字符的编码格式
    1、什么是编码格式？
    有一定规则的格式，使用了这种规则，我们就知道传输的是什么意思
    2、常见编码格式
    gbk 中文编码
    ascii 英文编码
    3、国际通用的编码格式
    utf-8 通用编码

## 十五、字符串格式化
    1、定义：一个固定的字符串中有部分元素，根据变量的值而改变的字符串
    2、格式化使用场景和目的
    发送邮件的时候
    发送短信的时候
    App上发推送的时候
    对于重复性很多的信息，通过格式化的形式，可以减少代码的书写量
    3、根据类型定义的格式化
    字符串格式化使用操作符%来实现
    
```python
name = 'zhenzhen'
age = 23
info = 'my name is %s, age is %s' #代码格式：%两边各有一个空格
print(info % (name, age)) ## my name is zhenzhen, age is 23 

books = ['python', 'html', 'java']
print('I have some books %s' % books)
# 打印结果，字典同理
# I have some books ['python', 'html', 'java']
```

    4、字符串格式化函数format()
    string.format()函数用来格式化字符串
    使用format的字符串主体使用 {} 大括号来替代格式符
    
```python
test = 'today is {0}, my name is {1}'
print(test.format('星期三', 'zhenzhen')) 
# 打印结果：today is 星期三, my name is zhenzhen
```

    5、python3.6之后加入的格式化方法f-strings
    定义一个变量
    字符串前加 f 符号
    需要格式化的位置使用 {变量名}
    
```python
name = 'zhenzhen'
print(f'my name is {name}') # my name is zhenzhen
```

## 十六、字符串格式化符号
    1、用于对应各种数据类型的格式化符号
    %s          格式化字符串，通用类型
    %d          格式化整型
    %f          格式化浮点型
    %u          格式化无符号整型（正整型）
    %c          格式化字符
    
```python
print('%c' % 1020)  # ϼ   #最大可格式化数值999999
print('%c' % 'b')   # b   #只支持int和char类型，char就是只有一个字符的字符串

print('%u' % -1)  # -1
print('%f' % 3.14) # 3.140000  #默认是保留六位小数

print('%d' % 1.6) # 1  
```
    2、format只支持格式化整型、格式化浮点型两种类型
 
```python
print('{:d}'.format(2))
print('{:f}.'.format(3))
```

    3、不常用格式符
    %o        格式化无符号八进制
    %x        格式化无符号十六进制
    %e        科学计数法格式化浮点数
    
```python
number = int('123ab', 16) # 表示生成一个16进制整型
print(number)
```

## 十七、字符串转义字符
    1、字符要转成其他含义的功能，称为转移字符
    2、\ + 字符
    3、python中转移字符
        \n    换行，一般用于末尾，strip对其也有效
        \t     横向制表符，可以认为是一个间隔符
        \v     纵向制表符，会有一个男性符号
        \a    响铃
        \b    退格符，将光标前移，覆盖，也就是删除前一个
        \r     回车
        \f     翻页，会出现一个女性符号，几乎用不到
        \'     转移字符串中的单引号
        \''     转移支付查中的双引号
        \\     转移斜杠
        
```python
info = 'my name\n is \tzhenzhen'# \t前面需要有空格才生效
print(info)
```
    4、在字符串前面加r来将当前字符串的转义字符无效化