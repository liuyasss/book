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

进度

https://www.runoob.com/python/python-lists.html