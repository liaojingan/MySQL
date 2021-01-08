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