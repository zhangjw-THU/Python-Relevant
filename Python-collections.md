# Python：collections

***

**张嘉玮**

**zhangjw16@mails.tsinghua.edu.cn**

`2019年7月17日11:21:07`

***

我们都知道，Python拥有一些内置的数据类型，比如str, int, list, tuple, dict等，collections模块在这些内置数据类型的基础上，提供了几个额外的数据类型：

|  数据类型   |                     功能                     |
| :---------: | :------------------------------------------: |
| namedtuple  |    生成可以使用名字来访问内容的tuple子类     |
|    deque    | 双端队列，可以快速的从另外一侧追加和推出对象 |
|   counter   |               计数器，用来计数               |
| orderedDict |                   有序字典                   |
| defaultdict |               带有默认值的字典               |

* ## Counter

  * Counter 作为**字典(dict)**的一个子类用来进行hashtable计数，将元素进行数量统计、计数后返回一个字典,`键值为元素：值为元素个数`

    ```python
    from collections import Counter
    s = 'abcbcaccbbad'  
    l = ['a','b','c','c','a','b','b']  
    d = {'2': 3, '3': 2, '17': 2}  
    # Counter 获取各元素的个数,返回字典  
    print(Counter(s))   # Counter({'b': 4, 'c': 4, 'a': 3, 'd': 1})  
    print(Counter(l))   # Counter({'b': 3, 'a': 2, 'c': 2})  
    print(Counter(d))   # Counter({'2': 3, '3': 2, '17': 2}) 
    """
    注意：字典类型的输入输出相同
    """
    ```

  * **most_common**

    ```python
    # most_common(int) 按照元素出现的次数进行从高到低的排序,返回前int个元素的字典  
    from collections import Counter
    s = 'abcbcaccbbad'
    m1 = Counter(s)  
    print(m1)                 # Counter({'c': 4, 'b': 4, 'a': 3, 'd': 1})  
    print(m1.most_common(3))  # [('c', 4), ('b', 4), ('a', 3)] 
    ```

  * **elements**

    ```python
    # elements 返回经过计数器Counter后的元素,返回的是一个迭代器  
    from collections import Counter
    d =['a','b','c','c','a','b','b']
    m1 = Counter(d)  # Counter({'a': 2, 'b': 3, 'c': 2})  
    print(''.join(sorted(m1.elements())))  #  aabbbcc
    print(sorted(m1.elements()))  # ['a', 'a', 'b', 'b', 'b', 'c', 'c'] 字典返回value个key 
    ```

  * **update**

    ```python
    from collections import Counter
    d =['a','b','c','c','a','b','b']
    m1 = Counter(d)	# Counter({'a': 2, 'b': 3, 'c': 2})
    m1.update('123a')	#	Counter({'1': 1, '2': 1, '3': 1, 'a': 3, 'b': 3, 'c': 2})
    ```

  * **substract**

    ```python
    # substract 和update类似，只是update是做加法，substract做减法,从另一个集合中减去本集合的元素，  
    sub1 = 'which'  
    sub2 = 'whatw'  
    subset = Counter(sub1)  
    print(subset)   # Counter({'h': 2, 'i': 1, 'c': 1, 'w': 1})  
    subset.subtract(Counter(sub2))  
    print(subset)   # Counter({'a': -1, 'c': 1, 'h': 1, 'i': 1, 't': -1, 'w': -1}) sub1中的h变为2，sub2中h为1,减完以后为1  
    ```

  * **items()**

    ```python
    subset.items()
    # dict_items([('w', -1), ('h', 1), ('i', 1), ('c', 1), ('a', -1), ('t', -1)])
    ```

  * **keys()**

    ```python
    subset.keys()
    #	dict_keys(['w', 'h', 'i', 'c', 'a', 't'])
    ```

    

  * **values()**

    ```python
    subset.values()
    #	dict_values([-1, 1, 1, 1, -1, -1])
    ```

    

* ## deque

  deque 包含在文件_collections.py中,属于**高性能的数据结构**(High performance data structures)之一.可以从两端添加和删除元素,常用的结构是它的简化版

  * **append**

    队列右边添加元素

  * **appendleft**

    队列左边添加元素

  ```python
  from collections import deque
  s = 'abd121cd'
  dq = deque(s)
  dq
  #	deque(['a', 'b', 'd', '1', '2', '1', 'c', 'd'])
  
  dq.append('zjw')
  #	deque(['a', 'b', 'd', '1', '2', '1', 'c', 'd', 'zjw'])
  
  dq.appendleft('zxx')
  deque(['zxx', 'a', 'b', 'd', '1', '2', '1', 'c', 'd', 'zjw'])
  ```

  * **clear**
    clear 清空队列中的所有元素

  * **count**
    count(value)  返回队列中包含value的个数,结果类型为 integer

    ```python
    dq.count('a')
    #	1
    ```

  * **extend**
    extend 队列右边扩展,可以是列表、元组或字典，如果是字典则将字典的key加入到deque

    ```python
    dq.extend({'1':10,2:"20"})
    #	deque(['zxx', 'a', 'b', 'd', '1', '2', '1', 'c', 'd', 'zjw', '1', 2])
    ```

  * **extendleft**

    extendleft  同extend, 在左边扩展

    ```python
    dq.extendleft('yt')
    #	deque(['t', 'y', 'zxx', 'a', 'b', 'd', '1', '2', '1', 'c', 'd', 'zjw', '1', 2])
    ```

  * **pop**
    pop  移除并且返回队列右边的元素

  * **popleft**
    popleft 移除并且返回队列左边的元素

  * **remove**
    remove(value) 移除队列第一个出现的元素（从左往右开始的第一次出现的元素value)

  * **reverse**

    reverse  队列的所有元素进行反转

  * **rotate**

    rotate(n) 对队列的数进行移动,若n<0，则往左移动即将左边的第一个移动到最后,移动n次，n>0 往右移动.

    

* ### defaultdict

  默认字典,是字典的一个子类,继承有字典的方法和属性,默认字典在进行定义初始化的时候可以指定字典值得默认类型：

  ```python
  from collections import defaultdict
  dic = defaultdict(dict)  
  dic['k1'].update({'k2':'aaa'})  
  print(dic)  
  #	defaultdict(<class 'dict'>, {'k1': {'k2': 'aaa'}})
  ```

  我们看上面的例子,字典dic在定义的时候就定义好了值为字典类型,虽然现在字典中还没有键值 k1，但仍然可以执行字典的update方法. 这种操作方式在传统的字典类型中是无法实现的,必须赋值以后才能进行值得更新操作，否则会报错。

  ```python
  b = dict()  
  b['k1'].append('2')  
  # TypeError: 'type' object is not iterable  
  ```



* ###  OrderedDict

  OrderDict 叫做有序字典,也是字典类型(dict)的一个子类,是对字典的一个补充。 前面我们说过,字典类型是一个无序的集合,如果要想将一个传统的字典类型进行排序一般会怎么做了，我们可能会将字典的键值取出来做排序后在根据键值来进行有序的输出,我们看下面的一个例子：

  ```python
  from collections import OrderedDict
  # 定义传统字典  
  dic1=dict()
  # 按顺序添加字典内容  
  dic1['a']='123'
  dic1['d']='jjj'
  dic1['c']='394'
  dic1['b']='999'
  print(dic1)
  # 结果： {'a': '123', 'c': '394', 'b': 'jjj', 'd': '999'}  
  # 排序  
  dic1_key_list=[]
  for k in dic1.keys():
      dic1_key_list.append(k)
  print(dic1_key_list)
  dic1_key_list.sort()
  print(dic1_key_list)
  for key in dic1_key_list:
      print('dic1字典排序结果 %s:%s'%(key,dic1[key]))
      
  '''
  {'a': '123', 'd': 'jjj', 'c': '394', 'b': '999'}
  ['a', 'd', 'c', 'b']
  ['a', 'b', 'c', 'd']
  dic1字典排序结果 a:123
  dic1字典排序结果 b:999
  dic1字典排序结果 c:394
  dic1字典排序结果 d:jjj
  '''
  ```

  以上为定义传统字典类型时的一个简单排序过程。 如果我们定义一个有序字典时,将不用再如此麻烦, 字典顺序将按照录入顺序进行排序且不会改变。

  ```python
  from collections import OrderedDict
  # 定义传统字典  
  dic1=OrderedDict()
  # 按顺序添加字典内容  
  dic1['a']='123'
  dic1['d']='jjj'
  dic1['c']='394'
  dic1['b']='999'
  print(dic1)
  
  for k,v in dic1.items():
      print('有序字典：%s:%s'%(k,v))
      
  '''
  OrderedDict([('a', '123'), ('d', 'jjj'), ('c', '394'), ('b', '999')])
  有序字典：a:123
  有序字典：d:jjj
  有序字典：c:394
  有序字典：b:999
  '''
  ```

  

* ### nametuple

  * 标准的tuple类型使用数字索引来访问元素

  ```python
  bob=('Bob',30,'male')
  print('Representation:',bob)
  jane=('Jane',29,'female')
  print('\nField by index:',jane[0])
  print('\nFields by index:')
  for p in [bob,jane]:
      print('%s is a %d year old %s'%p)
      
  '''
  Representation: ('Bob', 30, 'male')
  
  Field by index: Jane
  
  Fields by index:
  Bob is a 30 year old male
  Jane is a 29 year old female
  '''
  ```

  * 这种对于标准的元组访问,我们需要知道元素对应下标索引值,但当元组的元素很多时,我们可能无法知道每个元素的具体索引值,这个时候就是**可命名元组**登场的时候了。

  * **nametuple** 的创建是由自己的类工厂nametuple()进行创建,而不是由标准的元组来进行实例化，通过nametuple()创建类的参数包括类名称和一个包含元素名称的字符串。

  ```python
  from collections import namedtuple
  # 创建一个nametuplede 类,类名称为Person，并赋给变量P  
  P = namedtuple('Person', 'name,age,gender') 
  print('Type of Person:', type(P))  
  # Type of Person: <class 'type'>
  
  # 通过Person类实例化一个对象bob 
  bob = P(name='Bob', age=30, gender='male') 
  print('\nRepresentation:', bob)  
  # Representation: Person(name='Bob', age=30, gender='male') 
  
  # 通过Person类实例化一个对象jane
  jane = P(name='Jane', age=29, gender='female')
  print('\nField by name:', jane.name)
  # Field by name: Jane 
  
  print('\nFields by index:')
  for p in [bob, jane]:  
      print('%s is a %d year old %s' % p)
      
  '''
  Type of Person: <class 'type'>
  
  Representation: Person(name='Bob', age=30, gender='male')
  
  Field by name: Jane
  
  Fields by index:
  Bob is a 30 year old male
  Jane is a 29 year old female
  '''
  ```

  * 通过上面的实例可以看出,我们通过nametuple()创建了一个Person的类,并复制给P变量,Person的类成员包括name,age,gender,并且顺序已经定了,在实例化zhangsan这个对象的时候,对张三的属性进行了定义。这样我们在访问zhangsan这个元组的时候就可以通过张三的属性来复制(zhangsan.name、zhangsan.age等)。这样就算这个元组有1000个元素我们都能通过元素的名称来访问而不用考虑元素的下标索引值。

  * 非法的参数值

    使用nametuple()来创建类的时候,传递的成员属性参数名称不能非法（不能为系统参数名称），且参数名称不能重复,否则会报值错误