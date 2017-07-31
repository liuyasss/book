## Python语法

#### for...else

> `for … else` 表示这样的意思，`for` 中的语句和普通的没有区别，`else `中的语句会在循环正常执行完后，再执行。默认情况下`range`函数起始默认为0，例如`range(5)`，表示`range(0,5)`

```python
for i in range(1, 3):
    if i % 2 == 0:
        print(i)
else:
    print(i)
    
# 输出结果
2
2
```

#### pass

> `pass `不做任何事情，一般用做占位语句。

```python
for i in 'python':
    if i == 'h':
        print(i)
        pass
    
# 输出结果
h
```

#### Number(数字)

> Number 数据类型用于存储数值
>
> 数据类型是不允许改变的,这就意味着如果改变 Number 数据类型的值，将重新分配内存空间

```python
var = 1
```

#### 字符串

> Python不支持单字符类型，**单字符**也在Python也是作为一个字符串使用。

```python
var = 'this is python'
print(var[0], var[1], var[2])

# 输出结果
t h i
```

#### 字符串更新

> `var[x:y]` 截取字符串`var`包括x，不包括y，左闭右开

```python
var = 'this is python'
print(var[:8] + 'java')

# 输出结果
this is java
```

#### 字符串格式化

> Python 支持格式化字符串的输出 。尽管这样可能会用到非常复杂的表达式，但最基本的用法是将一个值插入到一个有字符串格式符 %s 的字符串中。
>
> 在 Python 中，字符串格式化使用与 C 中 sprintf 函数一样的语法。

```python
print('this %s a %s' % ('is', 'python'))

# 输出结果
this is a python
```

### List(列表)

> 列表(序列)是Python中最基本的数据结构。序列中的每个元素都分配一个数字 - 它的位置(索引)，第一个索引是0，第二个索引是1，依此类推。
>
> Python有6个序列的内置类型，但最常见的是列表和元组。
>
> 序列都可以进行的操作包括索引，切片，加，乘，检查成员。
>
> 此外，Python已经内置确定序列的长度以及确定最大和最小的元素的方法。
>
> 列表是最常用的Python数据类型，它可以作为一个方括号内的逗号分隔值出现。
>
> 列表的数据项不需要具有相同的类型

| 函数                      | 描述                                |
| :---------------------- | :-------------------------------- |
| cmp(list1,list2)        | 比较两个列表的元素                         |
| len(list)               | 列表中的元素的个数                         |
| max(list)               | 返回列表元素最大值                         |
| min(list)               | 返回列表元素最小值                         |
| list(seq)               | 将元组转换为列表                          |
| list.append(obj)        | 在列表末尾添加新的对象                       |
| list.count(obj)         | 统计某个元素在列表中出现的次数                   |
| list.extend(seq)        | 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
| list.index(obj)         | 从列表中找出某个值第一个匹配项的索引位置              |
| list.insert(index, obj) | 将对象插入列表                           |
| list.pop(obj=list[-1])  | 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值    |
| list.remove(obj)        | 移除列表中某个值的第一个匹配项                   |
| list.reverse()          | 反向列表中元素                           |
| list.sort([func])       | 对原列表进行排序                          |

##### Python3中部分函数修改

> 修改后的比较运算符在 `operator`模块中

| 函数                | 描述                 |
| ----------------- | ------------------ |
| operator.lt(a, b) | lt(a, b) 相当于 a < b |
| operator.gt(a, b) | gt(a,b) 相当于 a > b  |
| operator.le(a, b) | le(a,b) 相当于 a <= b |
| operator.ge(a, b) | ge(a, b)相当于 a>= b  |
| operator.eq(a, b) | eq(a,b) 相当于 a == b |
| operator.ne(a, b) | ne(a,b) 相当于 a != b |

### Python 元组

> Python的元组与列表类似，不同之处在于元组的元素不能修改。
>
> 元组使用小括号，列表使用方括号。
>
> 元组创建很简单，只需要在括号中添加元素，并使用逗号隔开即可。

```python
tup1 = ('physics', 'chemistry', 1997, 2000);
tup2 = (1, 2, 3, 4, 5 );
tup3 = "a", "b", "c", "d";
```

#### 修改元组

> 元组中的元素值是不允许修改的，但我们可以对元组进行连接组合

```python
# -*- coding: UTF-8 -*-

tup1 = (12, 34.56);
tup2 = ('abc', 'xyz');

# 以下修改元组元素操作是非法的。
# tup1[0] = 100;

# 创建一个新的元组
tup3 = tup1 + tup2;
print tup3;
```

#### 删除元组

> 元组中的元素值是不允许删除的，但我们可以使用del语句来删除整个元组

```python
tup = ('physics', 'chemistry', 1997, 2000);

print tup;
del tup;
print "After deleting tup : "
print tup;
```

### 字典

> 字典是另一种可变容器模型，且可存储任意类型对象。
>
> 字典的每个键值(key=>value)对用冒号(**:**)分割，每个对之间用逗号(**,**)分割，整个字典包括在花括号(**{})**中

> 键必须是唯一的，但值则不必。
>
> 值可以取任何数据类型，但键必须是不可变的，如字符串，数字或元组。

```python
dict = {'Alice': '2341', 'Beth': '9102', 'Cecil': '3258'}

dict1 = { 'abc': 456 };
dict2 = { 'abc': 123, 98.6: 37 };
```

获取元组中的值

```python
dict1 = {'1':'apple','2':'hp','3':'dell'}
print(dict1.get('1'))
print(dict1['2'])
```

#### 修改字典

```python
dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'};
 
dict['Age'] = 8; # update existing entry
dict['School'] = "DPS School"; # Add new entry
```

#### 删除字典

```python
dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'};
 
del dict['Name']; # 删除键是'Name'的条目
dict.clear();     # 清空词典所有条目
del dict ;        # 删除词典
```

#### 遍历字典

```python
# 遍历key，value
for key,value in dict1.items():
    print(key,value)
# 遍历key
for key in dict1.keys():
    print (key)
# 遍历value
for value in dict1.values():
    print(value)
```

### 日期和时间

> Python 程序能用很多方式处理日期和时间，转换日期格式是一个常见的功能。
>
> Python 提供了一个 `time 和 calendar` 模块可以用于格式化日期和时间。
>
> 时间间隔是以秒为单位的浮点小数。
>
> 每个时间戳都以自从1970年1月1日午夜（历元）经过了多长时间来表示。
>
> Python 的 time 模块下有很多函数可以转换常见日期格式。如函数time.time()用于获取当前时间戳

```python
import time;  # 引入time模块

ticks = time.time()
print "当前时间戳为:", ticks
# 格式化时间

# 格式化成2016-03-20 11:45:39形式
print time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()) 

# 格式化成Sat Mar 28 22:24:24 2016形式
print time.strftime("%a %b %d %H:%M:%S %Y", time.localtime()) 
  
# 将格式字符串转换为时间戳
a = "Sat Mar 28 22:24:24 2016"
print time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y"))
```

- %y 两位数的年份表示（00-99）
- %Y 四位数的年份表示（000-9999）
- %m 月份（01-12）
- %d 月内中的一天（0-31）
- %H 24小时制小时数（0-23）
- %I 12小时制小时数（01-12）
- %M 分钟数（00=59）
- %S 秒（00-59）
- %a 本地简化星期名称
- %A 本地完整星期名称
- %b 本地简化的月份名称
- %B 本地完整的月份名称
- %c 本地相应的日期表示和时间表示
- %j 年内的一天（001-366）
- %p 本地A.M.或P.M.的等价符
- %U 一年中的星期数（00-53）星期天为星期的开始
- %w 星期（0-6），星期天为星期的开始
- %W 一年中的星期数（00-53）星期一为星期的开始
- %x 本地相应的日期表示
- %X 本地相应的时间表示
- %Z 当前时区的名称
- %% %号本身

#### 日历

```python
import calendar
cal =calendar.month(2017,7)
print (cal)
```

### Python 函数

> 函数是组织好的，可重复使用的，用来实现单一，或相关联功能的代码段。
>
> 函数能提高应用的模块性，和代码的重复利用率。你已经知道Python提供了许多内建函数，比如print()。但你也可以自己创建函数，这被叫做用户自定义函数。

#### 定义函数

> 定义一个由自己想要功能的函数，以下是简单的规则：
>
> - 函数代码块以 **def** 关键词开头，后接函数标识符名称和圆括号**()**。
> - 任何传入参数和自变量必须放在圆括号中间。圆括号之间可以用于定义参数。
> - 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
> - 函数内容以冒号起始，并且缩进。
> - **return [表达式]** 结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回 None。

#### 匿名函数

> python 使用 lambda 来创建匿名函数。
>
> - lambda只是一个表达式，函数体比def简单很多。
> - lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
> - lambda函数拥有自己的命名空间，且不能访问自有参数列表之外或全局命名空间里的参数。
> - 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

```python
sum = lambda x,y:x + y
print (sum(1, 2))
```

#### 不定长参数函数

```python
def f(x, *y):
    print('单一参数x:',x)
    for i in y:
        print('长参数y:', i)
    return
f('a','b','c')
# 输出
# 单一参数x: a
# 长参数y: b
# 长参数y: c
```

#### 缺省参数

> 调用函数时，缺省参数的值如果没有传入，则被认为是默认值

```python
#可写函数说明
def printinfo( name, age = 35 ):
   "打印任何传入的字符串"
   print "Name: ", name;
   print "Age ", age;
   return;
 
#调用printinfo函数
printinfo( age=50, name="miki" );
printinfo( name="miki" );
```

### Python 模块

> Python 模块(Module)，是一个 Python 文件，以 .py 结尾，包含了 Python 对象定义和Python语句。
>
> 模块让你能够有逻辑地组织你的 Python 代码段。
>
> 把相关的代码分配到一个模块里能让你的代码更好用，更易懂。
>
> 模块能定义函数，类和变量，模块里也能包含可执行的代码。

```python
# my_print.py
def print_info(s):
    print(s)
    return
```

```python
import my_print
my_print.print_info('this is other moudle')
```

### Python中的包

> 包是一个分层次的文件目录结构，它定义了一个由模块及子包，和子包下的子包等组成的 Python 的应用环境。
>
> 简单来说，包就是文件夹，但该文件夹下必须存在\_init\_.py文件, 该文件的内容可以为空。\__init\_.py用于标识当前文件夹是一个包。
>
> 考虑一个在 **package_runoob** 目录下的 **test1.py、test2.py、__init__.py ** 文件，test.py 为测试调用包的代码，目录结构如下：

> markdown 语法下划线 “\_”，需要用到转义字符

```
test.py
package_runoob
|-- __init__.py
|-- runoob1.py
|-- runoob2.py
```

```python
import package_runoob.test1
import package_runoob.test2

package_runoob.test1.print_info()
package_runoob.test2.print_info()
```

进度 https://www.runoob.com/python/python-files-io.html