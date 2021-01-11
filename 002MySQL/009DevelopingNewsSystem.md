## Colorama模块
    作用：向控制台输出彩色字体
    Fore是针对字体颜色，Back是针对字体背景颜色，Style(重置输出文字颜色)是针对字体格式
    
    Fore: BLACK, RED, GREEN, YELLOW, BLUE, MAGENTA, CYAN, WHITE, RESET.
    Back: BLACK, RED, GREEN, YELLOW, BLUE, MAGENTA, CYAN, WHITE, RESET.
    Style: DIM, NORMAL, BRIGHT, RESET_ALL
    
```python
from colorama import Style
# 记得要及时关闭colorma的作用范围
# 如果不关闭的话，后面所有的输出都会是你指定的颜色
 
print(Style.RESET_ALL)
```
    
```python
# coding=utf-8

from colorama import Fore, Back, Style


print(Fore.LIGHTBLUE_EX, 'TestColor')
print(Back.LIGHTBLACK_EX, 'TestColor')
print(Style.RESET_ALL, 'TestColor')
```

## 项目结构
    vega包
        db包
            mysql_db.py
            user_dao.py  dao(数据库访问模式即对数据表的操作)
            ...
        service包(业务类)
            user_service.py
            ...
        app.py
        
    注意：如果程序是循环执行的（比如；可以循环登录退出），执行完程序后需要归还数据库连接(con.close())
    查询的sql语句不需要进行事务控制
    
    复杂的业务逻辑都写在service层中，比如用户在北京购物下单，北京地区有很多仓库都有该物品，这时候就需要在
    service层中进行复杂的计算拆分多个子订单，看使用哪个仓库进行发货比较合理，然后交给dao写到数据库中形成
    真正的订单，这时具体仓库才发货
    
## APP程序的作用

    APP程序用来处理控制台的输入与输出的，因为控制台的操作询问是轮殉执行的，所以需要在APP中使用死循环
    几层菜单就要做几层的死循环，当用户返回上一级菜单时，只需要break当前死循环即可
    
    getpass模块作用：输入密码时，密码字符内容隐藏
    