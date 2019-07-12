# Python3

作者：[张嘉玮][http://github.com/zhangjw-THU]

> [教程][http://github.com/TwoWater/python]
>
> <https://www.readwithu.com/>
>
> <https://github.com/zhangjw-THU>
>
> 

# 字典(Dictionary) #

经过之前的学习，我们可以知道 list 和 tuple 可以用来表示有序集合，之前我们那个例子是用 list 来存储了用户的昵称

```python
user=['liangdianshui','twowater','两点水']
```

如果我们需要把用户的账号也记录进去呢？

用 list 可以这样子解决：

```python
user=[['liangdianshui','111111'],['twowater','222222'],['两点水','333333']]
```

可是这样表示也不方便，而且很难根据昵称找到对应的昵称，且 list 越长，耗时越长；这时候就可以用 dict （字典）来表示了，Python 内置了 字典（dict），dict 全称dictionary，相当于 JAVA 中的 map，使用键-值（key-value）存储，具有极快的查找速度。

```python
user={'liangdianshui':'111111' ,'twowater':'222222' ,'两点水':'333333'}
```


## 1、dict （字典）的创建 ##

字典是另一种可变容器模型，且可存储任意类型对象。

字典的每个键值(key=>value)对用冒号(:)分割，每个对之间用逗号(,)分割，整个字典包括在花括号({})中 ,格式如下所示：

```python
dict = {key1 : value1, key2 : value2 }
```

注意：键必须是唯一的，但值则不必。值可以取任何数据类型，但键必须是不可变的。

创建 dict（字典）实例：

```python
dict1={'liangdianshui':'111111' ,'twowater':'222222' ,'两点水':'333333'}
dict2={'abc':1234,1234:'abc'}
```

## 2、访问 dict （字典） ##

```python
#-*-coding:utf-8-*-
dict1={'liangdianshui':'111111' ,'twowater':'222222' ,'两点水':'333333'}
print(dict1)

```

输出的结果：

```
{'liangdianshui': '111111', 'twowater': '222222', '两点水': '333333'}
```

这里需要注意的一点是：如果字典中没有这个键，是会报错的。

## 3、修改 dict （字典） ##

向字典添加新内容的方法是增加新的键/值对，修改或删除已有键/值对

```python
#-*-coding:utf-8-*-
dict1={'liangdianshui':'111111' ,'twowater':'222222' ,'两点水':'333333'}
print(dict1)
# 新增一个键值对
dict1['jack']='444444'
print(dict1)
# 修改键值对
dict1['liangdianshui']='555555'
print(dict1)
```

输出的结果：

```python
{'liangdianshui': '111111', 'twowater': '222222', '两点水': '333333'}
{'liangdianshui': '111111', 'twowater': '222222', '两点水': '333333', 'jack': '444444'}
{'liangdianshui': '555555', 'twowater': '222222', '两点水': '333333', 'jack': '444444'}
```

## 4、删除 dict （字典） ##

通过 `del` 可以删除 dict （字典）中的某个元素，也能删除 dict （字典）

通过调用 `clear()` 方法可以清除字典中的所有元素

```python
#-*-coding:utf-8-*-
dict1={'liangdianshui':'111111' ,'twowater':'222222' ,'两点水':'333333'}
print(dict1)
# 通过 key 值，删除对应的元素
del dict1['twowater']
print(dict1)
# 删除字典中的所有元素
dict1.clear()
print(dict1)
# 删除字典
del dict1
```

输出的结果：

```
{'liangdianshui': '111111', 'twowater': '222222', '两点水': '333333'}
{'liangdianshui': '111111', '两点水': '333333'}
{}
```

## 5、 dict （字典）使用时注意的事项 ##

(1) dict （字典）是不允许一个键创建两次的，但是在创建 dict （字典）的时候如果出现了一个键值赋予了两次，会以最后一次赋予的值为准

例如：

```python
#-*-coding:utf-8-*-
dict1={'liangdianshui':'111111' ,'twowater':'222222' ,'两点水':'333333','twowater':'444444'}
print(dict1)
print(dict1['twowater'])
```

输出的结果：

```
{'liangdianshui': '111111', 'twowater': '444444', '两点水': '333333'}
444444
```


(2) dict （字典）键必须不可变，可是键可以用数字，字符串或元组充当，但是就是不能使用列表

例如：

```python
#-*-coding:utf-8-*-
dict1={'liangdianshui':'111111' ,123:'222222' ,(123,'tom'):'333333','twowater':'444444'}
print(dict1)
```

输出结果：

```
{'liangdianshui': '111111', 123: '222222', (123, 'tom'): '333333', 'twowater': '444444'}
```

(3) dict 内部存放的顺序和 key 放入的顺序是没有任何关系

和 list 比较，dict 有以下几个特点：

* 查找和插入的速度极快，不会随着key的增加而变慢

* 需要占用大量的内存，内存浪费多

而list相反：

* 查找和插入的时间随着元素的增加而增加

* 占用空间小，浪费内存很少


## 6、dict （字典） 的函数和方法 ##

| 方法和函数        | 描述                                             |
| ----------------- | ------------------------------------------------ |
| cmp(dict1, dict2) | 比较两个字典元素                                 |
| len(dict)         | 计算字典元素个数                                 |
| str(dict)         | 输出字典可打印的字符串表示                       |
| type(variable)    | 返回输入的变量类型，如果变量是字典就返回字典类型 |
| dict.clear()      | 删除字典内所有元素                               |
| dict.copy()       | 返回一个字典的浅复制                             |
| dict.values()     | 以列表返回字典中的所有值                         |
| popitem()         | 随机返回并删除字典中的一对键和值                 |
| dict.items()      | 以列表返回可遍历的(键, 值) 元组数组              |