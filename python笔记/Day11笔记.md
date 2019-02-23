### 一、目录遍历

> os  用于获取系统的功能，主要用于操作文件或者文件夹
>
> 代码演示：
>
> ```python
> import  os
>
> path = r"C:\Users\Administrator\Desktop\SZ-Python"
>
> #获取指定目录下所有的文件以及文件夹，返回值为一个列表
> filesList = os.listdir(path)
> print(filesList)
>
> #C:\Users\Administrator\Desktop\SZ-Python
> #通过初始路径拼接子文件或者子文件夹形成新的路径
> filePath = os.path.join(path,"作业")
> print(filePath)
>
> #判断指定的路径是否是文件夹【目录】
> result = os.path.isdir(filePath)
> print(result)
> ```

#### 1.使用递归遍历目录

> 代码演示：
>
> ```python
> #1.递归
> import os
>
> def getAll(path):
>     #1.获取当前目录下所有的文件以及文件夹
>     fileList = os.listdir(path)
>     print(fileList)
>
>     #2.遍历列表
>     for i in fileList:
>         #3.拼接路径
>         filePath = os.path.join(path,i)
>
>         #4.判断filePath是否是文件夹
>         if os.path.isdir(filePath):
>             #文件夹:递归
>             getAll(filePath)
>         else:
>             #文件
>             print("文件：",i)
>
> getAll(r"C:\Users\Administrator\Desktop\SZ-Python")
> ```

#### 2.栈模拟递归遍历目录

> 深度遍历
>
> 代码演示：
>
> ```python
> #栈
> #append   pop
> import  os
>
> def getAll(path):
>     #初始状态下，栈是空的
>     stack = []
>
>     #将初始路径添加到栈中
>     stack.append(path)
>
>     #处理栈，当栈为空的时候说明其中的内容为空，循环停止
>     while len(stack) != 0:
>         #从栈中取出数据
>         dirPath = stack.pop()
>
>         #获取指定路径下的所有的文件以及文件夹
>         filesList = os.listdir(dirPath)
>
>         #遍历列表‘
>         for fileName in filesList:
>             filePath  = os.path.join(dirPath,fileName)
>
>             if os.path.isdir(filePath):
>                 print("文件夹；",fileName)
>
>                 #如果是目录，将路径添加到栈中
>                 stack.append(filePath)
>
>                 print(stack)
>             else:
>                 print("文件：",fileName)
>
> getAll(r"C:\Users\Administrator\Desktop\SZ-Python")
> ```

#### 3.队列模拟递归遍历目录

> 广度遍历
>
> 代码演示：
>
> ```python
> #栈
> #append   popleft
> import  os
> import  collections
>
>
> def getAll(path):
>     #初始状态下，队列是空的
>     queue = collections.deque()
>
>     #将初始路径添加到队列中
>     queue.append(path)
>
>     #处理栈，当栈为空的时候说明其中的内容为空，循环停止
>     while len(queue) != 0:
>         #从栈中取出数据
>         dirPath = queue.popleft()
>
>         #获取指定路径下的所有的文件以及文件夹
>         filesList = os.listdir(dirPath)
>
>         #遍历列表‘
>         for fileName in filesList:
>             #拼接路径
>             filePath  = os.path.join(dirPath,fileName)
>
>             if os.path.isdir(filePath):
>                 print("文件夹；",fileName)
>
>                 #如果是目录，将路径添加到队列中
>                 queue.append(filePath)
>
>             else:
>                 print("文件：",fileName)
>
> getAll(r"C:\Users\Administrator\Desktop\SZ-Python")
> ```



### 二、包

> ```
> 包：初期理解为文件夹
>
> 作用：一种管理Python模块命名空间的形式，采用"点语法"   os.path
>
> 包和文件夹之间的区别:Python的包中有一个特殊的文件__init__.py文件,前期里面不写任何内容，但是，就是为了告诉编译器，当前这个目录不是普通目录，是一个包
>
> 创建方式：选中工程，创建Python package
> ```
>
> 代码演示：
>
> ```Python
>
> """
> 1.在Python中，一个py文件其实就是一个模块
> 2.如果要跨模块调用函数，需要在运行的模块中导入需要使用的模块，调用函数的时候需要指明函数的路径
> """
>
> #第一步：导入模块
> #导入格式：包名.模块名
> import aaa.textDemo01
> import ccc.module
>
> #os.path.isdir()
> aaa.textDemo01.test()
> ccc.module.test()
>
>
> #包存在的意义：在团队开发的过程中，为了解决文件命名冲突的问题，只要保证最上层的包命名不相同，就不会与别人的发生冲突
> ```

### 三、模块

#### 1.概述

> 为了解决维护问题，一般情况下，在一个完整的项目中，会将特定的功能分组，分别放到不同的文件中，在使用的过程中，可以单独维护，各个不同的文件之间互不影响，每个.py文件就被称为一个模块，通过结合包的使用来组织文件
>
> 优点：
>
> a.提高了代码的可维护性
>
> b.提高了代码的复用性【当一个模块被完成之后，可以在多个文件中使用】
>
> c.引用其他的模块【第三方模块】  
>
> d.避免函数名和变量的命名冲突

#### 2.系统模块

> UTC：格林威治天文时间，UTC+8
>
> 时间戳：指定时间距离1970.1.1 00:00:00的秒数
>
> time：时间
>
> datetime:日期
>
> calendar：万年历
>
> os：系统，文件和文件夹

##### 2.1time时间模块

> 时间的表示形式：
>
> ​	a.时间戳
>
> ​	b.元组格式
>
> ​	c.字符串格式化
>
> 代码演示：
>
> ```Python
> #导入
> import time
>
> #1。获取当前时间对应的时间戳，使用浮点型表示【掌握】
> t1 = time.time()
> print(t1)
>
> #2。将时间戳转换为UTC
> g = time.gmtime(t1)
> print(g)  #time.struct_time(tm_year=2018, tm_mon=5, tm_mday=29, tm_hour=2, tm_min=29, tm_sec=1, tm_wday=1, tm_yday=149, tm_isdst=0)
>
> #3.根据时间戳生成当地时间【掌握】
> l = time.localtime(t1)
> print(l)
>
> #4.将具体时间转换为时间戳【掌握】
> m = time.mktime(l)
> print(m)
>
> #5.将时间转换为字符串形式【掌握】
> a = time.asctime(l)
> print(a)  #Tue May 29 10:36:57 2018
>
> #6.将时间戳转换为字符串形式
> c = time.ctime(t1)
> print(c)
>
> #7.将时间进行格式化【指定字符串的格式】【掌握】
> """
> %Y:年
> %m:月
> %d:日
> %H:时【24小时制】
> %h:时【12小时制】
> %M:分
> %S:秒
> """
> s1 = time.strftime("%Y.%m.%d %H:%M:%S",l)   #string format
> print(s1)
>
> #8.休眠,参数的单位为秒【掌握】
> print("4674747")
> time.sleep(2)
> print("hello")
>
> #9.用浮点数【一般用科学计数法】计算的秒数返回当前cpu的时间，用于衡量不同程序的耗时
> print(time.clock())
>
> #廖雪峰的网站   菜鸟教程
> ```
>
> 练习：
>
> ```Python
> #需求;已知一个时间的字符串，然后输出三天之后的时间
> """
> 思路：
> 1.将已知的字符串转换为对应的时间戳
> 2.利用时间戳计算三天后的时间【加法运算 + 3 * 24 * 3600】
> 3.将时间戳转换为时间的字符串，并且将时间格式化
> """
> import  time
>
> str = "2017-5-20"
>
> #1.将已知的字符串转换为对应的时间戳
> newStr = time.strptime(str,"%Y-%m-%d")
> print(newStr)
> time1 = time.mktime(newStr)
> print(time1)
> #2.利用时间戳计算三天后的时间【加法运算 + 3 * 24 * 3600】
> time2 = time1 + 3 * 24 * 3600
> #3.将时间戳转换为时间的字符串，并且将时间格式化
> time3 = time.strftime("%Y-%m-%d",time.localtime(time2))
> print(time3)   #2017-05-23
> ```

##### 2.2datetime日期模块

> 是对time模块的封装，比time模块更加全面
>
> 代码演示：
>
> ```Python
> import  datetime
>
> #1.获取当前时间
> d1 = datetime.datetime.now()
> print(d1)  #2018-05-29 11:20:51.432757
>
> #2.获取指定的时间，通过元组形式
> d2 = datetime.datetime(2015,10,1,10,23,23,1234)
> print(d2)
>
> #3.将时间格式化
> d3 = d1.strftime("%Y.%m.%d")
> print(d3)
>
> #4.将时间字符串转换为datetime实体
> d4 = datetime.datetime.strptime(d3,"%Y.%m.%d")
> print(d4)
>
> #5.直接进行加减运算
> date1 = datetime.datetime(2015,10,1,10,23,23,0)
> print(date1)
>
> date2 = datetime.datetime(2015,10,4,10,23,23,0)
> date3 = date2 - date1
> print(date3)  #3 days, 0:00:00
>
> print(date3.days)
> print(date3.seconds)
> ```

##### 2.3calendar日历模块

> 代码演示：
>
> ```Python
> import  calendar
>
> #返回指定年份中指定月份的万年历表示
> print(calendar.month(2018,5))
>
> #返回指定年份的万年历表示
> print(calendar.calendar(2018))
>
> #返回一个列表【二维列表】
> print(calendar.monthcalendar(2018,5))
>
> #当前周起始的日期
> print(calendar.firstweekday())
>
> #判断某年是否为闰年
> print(calendar.isleap(2010))
>
> #统计两个年份之间闰年的总数
> print(calendar.leapdays(2000,2020))
>
> #获取的是星期，0【星期一】~6【星期天】   1~12
> print(calendar.weekday(2018,5,29))
> ```

##### 2.4os模块

> 提供有关于操作系统的函数，处理文件或者文件夹
>
> 代码演示：
>
> ```Python
> import os
>
> #1.获取当前操作系统的名称
> #nt----->Windows   posix------>Linux,Mac os
> print(os.name)
>
> #2.获取当前系统的环境变量
> #以字典的形式返回
> print(os.environ)
> #通过key获取对应的value
> print(os.environ.get("APPDATA"))
>
> #3,获取指定目录下所有的文件或者文件夹的列表
> l = os.listdir(r"C:\Users\Administrator\Desktop\SZ-Python")
> print(l)
>
> #4.在指定的路径下创建文件夹
> #os.mkdir(r"C:\Users\Administrator\Desktop\aaa")
>
> #5.删除文件夹
> #os.rmdir(r"C:\Users\Administrator\Desktop\aaa")
> #删除文件
> #os.remove("")
>
> #6.获取文件属性
> #print(os.stat(r"C:\Users\Administrator\Desktop\aaa"))
>
> #7.给文件或者文件夹重命名
> #注意：当前的文件在关闭状态
> #rename(old,new)
> #os.rename(r"C:\Users\Administrator\Desktop\aaa",r"C:\Users\Administrator\Desktop\abc")
>
> #os.path模块下
> #1.路径的拼接
> path = os.path.join(r"C:\Users\Administrator\Desktop\SZ-Python","Day1Code")
> print(path)
>
> #2.绝对路径和相对路径【掌握】
> """
> 绝对路径：带有盘符的路径，缺点：只能在指定的计算机上使用
> 相对路径：不带盘符的路径，一般情况下是以当前的工程为参照物
>     例如：
>         aaa/textDemo01.py
>         ccc/module.py
> """
> #os.rename("bbb/check.py","bbb/show.py")
>
> #3.拆分路径
> #注意：返回的结果为元组，默认情况下只会拆分最后的文件或者文件夹
> tuple1 = os.path.split(r"C:\Users\Administrator\Desktop\SZ-Python\Day1Code")
> print(tuple)
>
> #4.拆分路径，获取指定路径对应的文件的扩展名
> print(os.path.splitext(r"C:\Users\Administrator\Desktop\SZ-Python\Day2Code\assignDemo.py"))
>
> #5.判断指定路径是否是文件夹
> print(os.path.isdir("aaa/textDemo01.py"))
>
> #6.判断指定路径是否是文件
> print(os.path.isfile("aaa/textDemo01.py"))
>
> #7.判断一个指定路径是否存在
> print(os.path.exists("aaa/textDemo01.py"))
>
> #8.获取文件的大小【字节】
> print(os.path.getsize("aaa/textDemo01.py"))
>
> #9.
> #获取指定文件夹的父路径
> print(os.path.dirname(r"C:\Users\Administrator\Desktop\SZ-Python\Day1Code"))
> #获取当前文件夹的名称
> print(os.path.basename(r"C:\Users\Administrator\Desktop\SZ-Python\Day1Code"))
> ```
>
> 练习：
>
> ```Python
> import  os
> #练习：获取指定目录下所有的py文件或者txt文件
> """
> 思路：
> 1.判断指定的目录是否存在
> 2.获取指定目录下所有的文件以及文件夹
> 3.拼接路径
> 4.判断拼接之后的路径是否是文件
> 5.判断文件名称的后缀
> """
> def getFile(path):
>     #1.
>     if os.path.exists(path):
>         #2
>         fileList = os.listdir(path)
>
>         #3.
>         for fileName in fileList:
>             filePath = os.path.join(path,fileName)
>
>             #4
>             if os.path.isfile(filePath):
>                 #5
>                 if fileName.endswith("py") or fileName.endswith("txt"):
>                     print(fileName)
>             else:
>                 print(fileName,"不是文件")
>
>     else:
>         print("指定的路径不存在")
>
> getFile(r"C:\Users\Administrator\Desktop\SZ-Python\Day5Code")
> ```

#### 3.自定义模块【掌握】

##### 3.1自定义import模块

> 代码演示：
>
> ```Python
> #1.格式：import  包1.包2.模块的名称
> #注意1：通过点语法区分包的层级关系
> #引入模块
>
> #注意2：如果要同时导入多个模块，有两种方式
> #方式一
> """
> import os
> import datetime
> import math
> """
> #方式二
> import os,math,datetime
>
> #注意3：当导入自定义模块的时候，需要注意包的存在
> #注意5：当通过import将模块导入的时候，将模块对应的文件整个加载了一遍
> import ccc.module
> import moduleTextDemo01
>
> print("***************")
>
> #注意4：当模块有包的层级关系时，需要调用其中函数的时候，需要指明函数的路径
> ccc.module.test()     #os.path.isdir()
>
> moduleTextDemo01.fun1()
> moduleTextDemo01.fun2()
> moduleTextDemo01.fun3()
>
> print(moduleTextDemo01.num)
> ```

##### 3.2自定义form-import模块

> 代码演示：
>
> ```Python
>
> #form 模块名  import 函数名1/类名，函数名2.。。。
> #import  moduleTextDemo01
> from moduleTextDemo01 import  fun1,fun2,fun3
>
> #注意：采用了form。。。import的方式导入指定的函数之后，可以直接调用函数
> fun1()
> fun2()
> fun3()
>
> #好处：进行局部的导入，避免内存空间的浪费
>
>
> #注意：当前文件中如果存在和模块中同名的函数的时候，当前文件中的函数仍然会将模块中的函数给覆盖掉
> def fun1():
>     print("hello")
>
> fun1()
> ```

##### 3.3自定义form-import*模块

> 代码演示：
>
> ```Python
> #from 。。。。 import  *      *代表全部
> """
> 下面三种导入方式完全等价：将moduleTextDemo01模块中的所有的内容全部导入
> from moduleTextDemo01 import  *
> import moduleTextDemo01
> from  moduleTextDemo01 import  fun1,fun2,fun3
> """
> from moduleTextDemo01 import  *
>
> fun1()
> ```

> 总结：在python中，每个py文件其实都是一个模块，如果跨模块调用函数，则采用导入的方式
>
> 将不同的功能进行划分，调用函数的时候相对比较方便的

#### 4.__name__属性和dir函数

##### 4.1name属性

> ```Python
> #__name__的作用：如果不想让模块中的某些代码执行，可以通过属性仅仅调用程序中的一部分功能
> #【写在if判断中的代码只有当前模块被执行的时候才会被执行，检测到是其他的文件在使用当前的模块，则if语句中的代码不会被执行】
>
> def fun1():
>     print("aaa")
>
> def fun2():
>     print("bbb")
>
> def fun3():
>     print("ccc")
>
>
> #作用：写在下面判断中的代码，只有当前模块运行的时候才会被执行【起到屏蔽的作用】
> if __name__ == "__main__":
>     fun1()
>     fun2()
>     fun3()
> ```

##### 4.2dir函数

> 代码演示：
>
> ```Python
> #dir:
> import math,moduleTextDemo01
>
> #获取指定模块里面的所有的内容
> #dir(模块名称)  返回的是一个列表
> print(dir(math))
> print(dir(moduleTextDemo01))
> ```

