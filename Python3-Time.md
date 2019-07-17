## Python：Time

***

**张嘉玮**

**zhangjw16@mails.tsinghua.edu.cn**

***

```python
import time
```

* **时间戳**：格林威治时间1970年01月01日00分00秒（北京时间1970年01月01日08时00分00秒）起至现在的总秒数。

* **元组struct_time**：日期、时间是包含许多变量的，所以在Python中定义了一个**元组struct_time**将所有这些变量组合在一起，包括：4位数年、月、日、小时、分钟、秒等。

  | 序号 |   属性   |                  值                  |
  | :--: | :------: | :----------------------------------: |
  |  0   | tm_year  |                 2019                 |
  |  1   |  tm_mon  |               1 到 12                |
  |  2   | tm_mday  |               1 到 31                |
  |  3   | tm_hour  |               0 到 23                |
  |  4   |  tm_min  |               0 到 59                |
  |  5   |  tm_sec  |       0 到 61 (60或61 是闰秒)        |
  |  6   | tm_wday  |            0到6 (0是周一)            |
  |  7   | tm_yday  |           1 到 366(儒略历)           |
  |  8   | tm_isdst | -1, 0, 1, -1是决定是否为夏令时的旗帜 |

  

### **时间获取函数**

```python
>>> time.time()
# 返回当地时间戳，float
1563326861.0936668

>>> time.ctime()
# 标准格式的时间
'Wed Jul 17 09:29:24 2019'

>>> time.gmtime()
# 以元祖方式返回格林威治时间:1*9的元组
time.struct_time(tm_year=2019, tm_mon=7, tm_mday=17, tm_hour=1, tm_min=30, tm_sec=51, tm_wday=2, tm_yday=198, tm_isdst=0)

>>>time.localtime()
# 以元组方式返回本地当前时间
time.struct_time(tm_year=2019, tm_mon=7, tm_mday=17, tm_hour=9, tm_min=33, tm_sec=54, tm_wday=2, tm_yday=198, tm_isdst=0)

```

### **时间格式化**

* strftime(tpl,ts)

  :bow_and_arrow:tpl：时间格式化模板字符串，用来定义输出效果。

  :bow_and_arrow:ts：计算机内部时间的类型变量。

  ```python
  >>> t = time.gmtime()
  # 以元祖方式返回格林威治时间:1*9的元组
  time.struct_time(tm_year=2019, tm_mon=7, tm_mday=17, tm_hour=1, tm_min=30, tm_sec=51, tm_wday=2, tm_yday=198, tm_isdst=0)
  
  >>> time.strftime("%Y-%m-%d %H:%M:%S %A %p",t)
  '2019-07-17 09:33:54 Wednesday AM'
  """
  %Y   年份
  %m  月份
  %B   月份名称 January
  %b   月份名称缩写  Jan
  %d   日期
  %A   星期 Monday
  %a   星期缩写 Mon
  %H   小时 24
  %h   小时 12
  %p   上下午
  %M  分钟
  %S   秒
  """
  ```

  :bow_and_arrow:如果strftime没有第二个参数，则默认获取当地时间。

  

* strptime：strptime（timestr, "%Y-%m-%d %H:%M:%S"）  根据时间字符串以及格式化输出，转换成结构体。

  ```python
  >>> timestr = time.strftime("%Y-%m-%d %H:%M:%S",time.localtime())
  >>> timestr
  '2019-07-17 09:49:13'
  
  >>> time.strptime(timestr,"%Y-%m-%d %H:%M:%S")
  time.struct_time(tm_year=2018, tm_mon=1, tm_mday=26, tm_hour=12, tm_min=55, tm_sec=33, tm_wday=4, tm_yday=26, tm_isdst=-1)
  
  ## 只要两个字符串结构体相同就OK
  ```

  

  ### **程序计时**

* **测量时间**：perf_counter()  返回一个CPU级别的精确时间计数值，单位为妙，由于这个计数值起点不确定，连续调用使用差值才有意义。

  ```python
  >>> start=time.perf_counter()
  >>> start
  3.9111116077602044e-06
  >>> end=time.perf_counter()
  >>> end
  10.212393474589648
  >>> end - start
  10.212389563478041
  ```

  

* **产生时间**：sleep(s) s妙的休眠时间，可以是浮点数，如time.sleep(3.5)

  ```python
  # 产生进度条
  import time
  scale = 50
  print("start".center(scale//2, "-"))
  start = time.perf_counter()
  for i in range(scale + 1):
          a = "*" * i
          b = "." * (scale - i)
          c = (i/scale)*100
          dur = time.perf_counter()-start
          print("\r{:^3.0f}%[{}->{}]{:.2f}s".format(c,a,b,dur), end="")
          time.sleep(0.1)
  print("\n"+"end".center(scale//2,"-"))
  ```

  

