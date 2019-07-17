# Python：datetime

***

**张嘉玮**

**zhangjw16@mails.tsinghua.edu.cn**

`2019年7月17日11:15:41`

***

* **datetime库概述**

  datetime库定义了2个常量和5个类。

  **2个常量**：`MINYEAR=1`和`MAXYEAR=9999`

  **5个类：**

  |     类      |            内容            |
  | :---------: | :------------------------: |
  |   date类    |        表示日期的类        |
  |   time类    |        表示时间的类        |
  | datetime类  |      表示时间日期的类      |
  | timedelta类 | 表示两个datetime对象的差值 |
  |  tzinfo类   |     表示失去的相关信息     |

  ```python
  
  >>> from datetime import datetime
  >>> now=datetime.now()
  >>> print（now）
  datetime.datetime(2019, 7, 17, 10, 50, 37, 43428)
  >>> print(type(now))
  datetime.datetime
  ```

  <!--

  注意到`datetime`是模块，`datetime`模块还包含一个`datetime`类，通过`from datetime import datetime`导入的才是`datetime`这个类。如果仅导入`import datetime`，则必须引用全名`datetime.datetime`。`datetime.now()`返回当前日期和时间，其类型是`datetime`

  -->

  

  

### 五个类：

* #### **date类：**

  date类包含三个参数，分别为year，month，day，返回格式为year-month-day

  * **构造函数：**

    `__new__(year,month,day)`：默认的构造函数，创建date类的对象时直接传入year，month，day三个参数即可返回对应的日期。

     `fromtimestamp(t)`：使用时间戳构造对象，使用方法为：datetime.date.fromtimestamp(t)，传入参数t为一个时间戳，返回时间戳t对应的日期。

     `today()`：使用今天的日期构造对象，使用方法为：datetime.date.today()，无参数，返回今天的日期。

     `fromordinal(n)`：使用日期序数构造对象，使用方法为：datetime.date.fromordinal(n)，传入参数为一个整数序数，代表从公元1年1月1日开始的序数，序数每增加1代表增加1天，返回最终计算出的日期。

  * **方法：**

    `timetuple()`：返回日期对应的time.struct_time对象，格式为`time.struct_time(tm_year=1, tm_mon=1, tm_mday=2, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=1, tm_yday=2, tm_isdst=-1)`    

     `toordinal()`：相当于`fromordinal(n)`的逆过程，返回值即为`fromordinal(n)`中的日期序数n。

     `weekday()`：返回该日期对应星期几，用[0,6]代表星期一到星期日。

     `isoweekday()`：作用同`weekday()`，用[1,7]代表星期一到星期日。

     `isocalendar()`：返回一个三元组，格式为(year,week_number,weekday)，分别代表年，第几周，星期几。

     `isoformat()`：返回标准日期格式：YYYY-MM-DD。

     `ctime()`：返回格式为：Sat Sep  8 00:00:00 2018

     `strftime(format)`：把日期按照format指定的格式进行格式化，具体的格式化符号如下。

     `replace(year,month,day)`：传入参数为year，month，day，返回对应的新日期。

    ```python
    """
    %y 两位数的年份表示（00-99）
    %Y 四位数的年份表示（000-9999）
    %m 月份（01-12）
    %d 月内中的一天（0-31）
    %H 24小时制小时数（0-23）
    %I 12小时制小时数（01-12）
    %M 分钟数（00=59）
    %S 秒（00-59）
    %a 本地简化星期名称
    %A 本地完整星期名称
    %b 本地简化的月份名称
    %B 本地完整的月份名称
    %c 本地相应的日期表示和时间表示
    %j 年内的一天（001-366）
    %p 本地A.M.或P.M.的等价符
    %U 一年中的星期数（00-53）星期天为星期的开始
    %w 星期（0-6），星期天为星期的开始
    %W 一年中的星期数（00-53）星期一为星期的开始
    %x 本地相应的日期表示
    %X 本地相应的时间表示
    %Z 当前时区的名称
    %% %号本身
    """
    ```

  

* ### **time类：**

  **time类**包含六个参数，分别为hour，minute，second，microsecond，tzinfo，fold，返回格式为hour:minute:second(.microsecond)

  * **构造函数：**

    `__new__(hour=0, minute=0, second=0, microsecond=0, tzinfo=None, fold=0)`：默认的构造函数，创建time类的对象时直接传入相应参数即可返回对应的时间。

  * **方法：**

    `isoformat()`：返回标准时间格式：HH:MM:SS.mmmmmm+zz:zz。

     `strftime(format)`：把时间按照format指定的格式进行格式化，具体的格式化符号与date类中介绍的相同。

     `utcoffset()`：返回timezone的偏移量。

     `tzname()`：返回timezone的名称。

     `replace()`：传入对应的参数，返回新的时间。

    

* ### **datetime类:**

  **datetime类**是date类和time类的合体，包含前两个类的全部参数。

  * **构造函数：**

    `__new__(year, month, day, hour=0, minute=0, second=0,microsecond=0, tzinfo=None, fold=0)`：默认的构造函数，创建datetime类的对象时直接传入相应参数即可返回对应的时间日期。

     `fromtimestamp(t)`：使用时间戳构造对象，传入参数t为一个时间戳，返回时间戳t对应的日期和时间。

     `utcfromtimestamp(t)`：使用时间戳构造对象，传入参数t为一个时间戳，返回时间戳t对应的UTC（时间标准时间）日期和时间。

     `now()`：使用当前日期和时间构造对象，无参数，返回当前的日期和时间。

     `utcnow()`：使用当前日期和时间构造对象，无参数，返回当前的UTC（时间标准时间）日期和时间。

     `combine(date,time)`：使用date和time构造对象，传入参数为1个date对象和1个time对象，返回计算出的日期。

  * **方法：**

    `timetuple()`：返回日期时间对应的time.struct_time对象，格式为`time.struct_time(tm_year=1973, tm_mon=11, tm_mday=29, tm_hour=21, tm_min=33, tm_sec=9, tm_wday=3, tm_yday=333, tm_isdst=-1)`    。

     `utctimetuple()`：与`timetuple()`相似，返回日期时间对应的UTC（时间标准时间）time.struct_time对象。

     `astimezone()`：返回的格式中加入时区信息，格式为：1973-11-29 21:33:09+08:00。

     `date()`：返回date部分

     `time()`：返回time部分，tzinfo设置为None。（另有timetz()方法返回有相同tzinfo的time()）

     `isoformat(sep)`：返回标准日期时间格式，传入参数sep可设置日期和时间的分隔符，默认为'T'：1973-11-29T21:33:09。

     `ctime()`：返回格式为：Sat Sep  8 00:00:00 2018

     `strftime(format)`：把日期按照format指定的格式进行格式化，具体的格式化符号与date类中介绍的相同。

     `strptime(date_string,format)`：将字符串格式转换为日期格式，具体的格式化符号与date类中介绍的相同。

     `replace()`：传入对应的参数，返回新的日期时间。

  * **举例：**

    * **获取指定日期和时间**

      要指定某个日期和时间，我们直接用参数构造一个`datetime`：

      ```python
      >>> from datetime import datetime
      >>> dt = datetime(2020,1,21)
      >>> dt
      datetime.datetime(2020, 1, 21, 0, 0)
      ```

    * **str转换为datetime**

      很多时候，用户输入的日期和时间是字符串，要处理日期和时间，首先必须把str转换为datetime。转换方法是通过`datetime.strptime()`实现，需要一个日期和时间的格式化字符串。

      ```python
      >>> cday=datetime.strptime('2019-1-1 18:20:20','%Y-%m-%d %H:%M:%S')
      >>> print(cday)
      datetime.datetime(2019, 1, 1, 18, 20, 20)
      ```

      字符串`'%Y-%m-%d %H:%M:%S'`规定了日期和时间部分的格式。
      注意转换后的datetime是没有时区信息的。

    * datetime转换为str

      如果已经有了datetime对象，要把它格式化为字符串显示给用户，就需要转换为str，转换方法是通过`strftime()`实现的，同样需要一个日期和时间的格式化字符串：

      ```python
      >>> from datetime import *
      >>> now=datetime.now()
      >>> now.strftime('%Y-%m-%d %p')
      '2019-07-17 AM'
      ```

* ### **timedelta类:**

  timedelta类代表两个datetime对象之间的时间差。

  * **构造函数：**

    `__new__(days=0, seconds=0, microseconds=0,milliseconds=0, minutes=0, hours=0, weeks=0)`：默认的构造函数，创建timedelta类的对象时直接传入相应参数即可返回对应单位的时间差。

  * **方法：**

    1. 支持两个timedelta对象之间的加、减操作。

    2. 支持对一个timedelta进行取正、取负、取绝对值等操作。

    3. 支持两个timedelta对象之间的比较。

    4. 支持一个timedelta对象乘以、除以一个整数的操作。

       

  * **举例：**

    ```python
    >>> from datetime import datetime,timedelta
    >>> now=datetime.now()
    
    >>> now
    datetime.datetime(2019, 7, 17, 11, 9, 38, 612847)
    
    >>> now+timedelta(hours=10)
    datetime.datetime(2019, 7, 17, 21, 9, 38, 612847)
    
    >>> now+timedelta(days=2,hours=12)
    datetime.datetime(2019, 7, 19, 23, 9, 38, 612847)
    ```

    

* ### **tzinfo类：**

  **tzinfo类**是一个虚拟基类，代表时区（time zone），创建子类时必须重写name()，utcoffset()，dst()这三个方法。

  