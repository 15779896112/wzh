### 一、错误和异常

#### 1.概念

> 两种容易辨认的错误
>
> ​	语法错误：一些关于语法的错误【缩进】
>
> ​	异常：代码完全正确，但是，程序运行之后，会报出 的错误
>
> exception/error
>
> 代码演示：
>
> ```Python
> list1 = [23,54,6,6]
> print(list1[2])
> print(list1[3])
> print(list1[4])  
>
> print("over")
>
> """
> 6
> 6
> Traceback (most recent call last):
>   File "C:/Users/Administrator/Desktop/SZ-Python/Day15Code/textDemo01.py", line 4, in <module>
>     print(list1[4])
> IndexError: list index out of range
> """
> ```
>
> 异常特点：当程序在执行的过程中遇到异常，程序将会终止在出现异常的代码处，代码不会继续向下执行
>
> 解决问题：越过异常，保证后面的代码继续执行【实质：将异常暂时屏蔽起来，目的是为了让后面的代码的执行不受影响】

#### 2.常见的异常

> NameError:变量未被定义
>
> TypeError:类型错误
>
> IndexError:索引异常
>
> keyError:
>
> ValueError:
>
> AttributeError:属性异常
>
> ImportError:导入模块的时候路径异常
>
> SyntaxError:代码不能编译
>
> UnboundLocalError:试图访问一个还未被设置的局部变量

#### 3.异常处理方式【掌握】

> 捕获异常
>
> 抛出异常

##### 3.1捕获异常

##### try-except-else

> 语法：
>
> ​	try:
>
> ​		可能存在异常的代码
>
> ​	except 错误表示码 as 变量：
>
> ​		语句1
>
> ​	except 错误表示码 as 变量：
>
> ​		语句2
>
> ​	。。。
>
> ​	else:
>
> ​		语句n
>
> 说明：
>
> ​	a.try-except-else的用法类似于if-elif-else
>
> ​	b.else可有可无，根据具体的需求决定
>
> ​	c.try后面的代码块被称为监测区域【检测其中的代码是否存在异常】
>
> ​	d.工作原理：首先执行try中的语句，如果try中的语句没有异常，则直接跳过所有的except语句，执行else；如果try中的语句有异常，则去except分支中进行匹配错误码，如果匹配到了，则执行except后面的语句；如果没有except匹配，则异常仍然没有被拦截【屏蔽】
>
> 代码演示：
>
> ```Python
> #一、try-except-else的使用
>
> #1.except带有异常类型
> try:
>     print(10 / 0)
> except ZeroDivisionError as e:
>     print("被除数不能为0",e)
>
> print("~~~~")
> """
> 总结：
> a.try-except屏蔽了异常，保证后面的代码可以正常执行
> b.except ZeroDivisionError as e相当于声明了一个ZeroDivisionError类型的变量【对象】，变量e中携带了错误的信息
> """
>
> #2.try后面的except语句可以有多个
> class Person(object):
>     __slots__ = ("name")
> try:
>     p = Person()
>     p.age = 19
>
>     print(10 / 0)
> except AttributeError as e:
>     print("属性异常",e)
> except ZeroDivisionError as e:
>     print("被除数不能为0",e)
>
> print("over")
>
> """
> 总结：
> a.一个try语句后面可以有多个except分支
> b.不管try中的代码有多少个异常，except语句都只会被执行其中的一个，哪个异常处于try语句的前面，则先先执行对应的except语句
> c.后面的异常不会报错【未被执行到】
> """
>
> #3.except语句的后面可以不跟异常类型
> try:
>     print(10 / 0)
> except:
>     print("被除数不能为0")
>
>
> #4.一个except语句的后面可以跟多种异常的类型
> #注意：不同的异常类型使用元组表示
> try:
>     print(10 / 0)
> except (ZeroDivisionError,AttributeError):
>     print("出现了异常")
>
>
> #5.else分支
> try:
>     print(10 / 4)
> except ZeroDivisionError as e:
>     print("出现了异常",e)
> else:
>     print("hello")
>
> """
> 总结：
> a.如果try中的代码出现了 异常，则直接去匹配except，else分支不会被执行
> b.如果try中的代码没有出现异常，则try中的代码正常执行，except不会被执行，else分支才会被执行
> """
>
> #6.try中不仅可以直接处理异常，还可以处理一个函数中的异常
> def show():
>     x = 1 / 0
>
> try:
>     show()
> except:
>     print("出现了异常")
>
> #7.直接使用BaseException代替所有的异常
> try:
>     y = 10 / 0
> except BaseException as e:
>     print(e)
>
> """
> 总结：在Python中，所有的异常其实都是类，他们都有一个共同的父类BaseException，可以使用BaseException将所有异常“一网打尽”
> """
> ```

##### try-except-finally

> 语法：
>
> ​	try:
>
> ​		可能存在异常的代码
>
> ​	except 错误表示码 as 变量：
>
> ​		语句1
>
> ​	except 错误表示码 as 变量：
>
> ​		语句2
>
> ​	。。。
>
> ​	finally:
>
> ​		语句n
>
> 说明:不管try中的语句是否存在异常，不管异常是否匹配到了except语句，finally语句都会被执行
>
> 作用：表示定义清理行为，表示无论什么情况下都需要进行的操作
>
> 代码演示：
>
> ```Python
> #二、try-except-finally的使用
>
> #1.
> try:
>     print(10 / 5)
> except ZeroDivisionError as e:
>     print(e)
>
> finally:
>     print("finally被执行")
>
>
> #2.特殊情况
> #注意：当在try或者except中出现return语句时，finally语句仍然会被执行
> def show():
>     try:
>         print(10 / 0)
>         return
>     except ZeroDivisionError as e:
>         print(e)
>
>     finally:
>         print("finally被执行~~~~")
>
> show()
> ```

##### 3.2抛出异常

> raise抛出一个指定的异常对象
>
> 语法：raise 异常对象     或者  raise
>
> 说明：异常对象通过错误表示码创建，一般来说错误表示码越准确越好
>
> 代码演示：
>
> ```Python
> #raise的使用主要体现在自定义异常中
>
> #1.raise表示直接抛出一个异常对象【异常是肯定存在的】
> #创建对象的时候，参数表示对异常信息的描述
> try:
>     raise NameError("hjafhfja")
> except NameError as e:
>     print(e)
>
> print("over")
>
> """
> 总结：
> 通过raise抛出的异常，最终还是需要通过try-except处理
> """
>
> #2.如果通过raise抛出的异常在try中不想被处理，则可以通过raise直接向上抛出
> try:
>     raise NameError("hjafhfja")
> except NameError as e:
>     print(e)
>     raise
> ```

#### 4.assert断言

> 对某个问题做一个预测，如果预测成功，则获取结果；如果预测失败，则打印预测的信息
>
> 代码演示：
>
> ```Python
> def func(num,divNum):
>
>     #语法：assert表达式，当出现异常时的信息描述
>     #assert关键字的作用：预测表达式是否成立，如果成立，则执行后面的代码；如果不成立，则将异常的描述信息打印出来
>     assert (divNum != 0),"被除数不能为0"
>
>     return  num / divNum
>
> print(func(10,20))
> print(func(10,0))
> ```

#### 5.异常的嵌套

> 代码演示：
>
> ```Python
> #需求：去拉萨，乘坐各种交通工具
> print("我要去拉萨")
>
> try:
>     print("我准备乘飞机过去")
>     raise Exception("由于大雾，飞机不能起飞")
>     print("到拉萨了，拉萨真漂亮")
> except Exception as e:
>     print(e)
>     try:
>         print("我准备乘火车过去")
>         raise  Exception("由于大暴雨，铁路断了")
>         print("到拉萨了，拉萨真漂亮")
>     except Exception as e:
>         print(e)
>         print("我准备跑过去")
>         print("到拉萨了，拉萨真漂亮")
> ```

#### 6.自定义异常

> 实现思路：
>
> a.定义一个类，继承自Exception类
>
> b.书写构造函数，属性保存异常信息【调用父类的构造函数】
>
> c.重写__str__函数，打印异常的信息
>
> d.定义一个成员函数，用来处理自己的异常
>
> 代码演示：
>
> ```Python
> class MyException(Exception):
>     def __init__(self,msg):
>         super(MyException,self).__init__()
>         self.msg = msg
>
>     def __str__(self):
>         return self.msg
>
>     def handle(self):
>         print("出现了异常")
>
> try:
>      raise MyException("自己异常的类型")
> except MyException as e:
>      print(e)
>      e.handle()
> ```

### 二、文件读写

#### 1.概念

> 在Python中，通过打开文件生成一个文件对象【文件描述符】操作磁盘上的文件，操作主要由文件读写

#### 2.普通文件的读写

> 普通文件包含：txt文件，图片，视频，音频等

##### 2.1读文件

> 操作步骤：
>
> ​	a.打开文件：open（）
>
> ​	b.读取文件内容：read()
>
> ​	c.关闭文件:close()
>
> 说明：最后一定不要忘了文件关闭，避免系统资源的浪费【因为一个文件对象会占用系统资源】
>
> 代码演示：
>
> ```Python
> #一、打开文件
> """
> open(path,flag[,encoding,errors])
> path:指定文件的路径【绝对路径和相对路径】
> flag:打开文件的方式
>     r:只读、
>     rb:read binary,以二进制的方式打开，只读【图片，视频，音频等】
>     r+:读写
>
>     w:只能写入
>     wb:以二进制的方式打开，只能写入【图片，视频，音频等】
>     w+:读写
>
>     a:append,如果一个文件不为空，当写入的时候不会覆盖掉原来的内容
> encoding：编码格式：gbk,utf-8
> errors:错误处理
> """
> path = r"C:\Users\Administrator\Desktop\SZ-Python\Day15\笔记\致橡树.txt"
> #调用open函数，得到了文件对象
> f = open(path,"r",encoding="gbk")
>
> """
> 注意：
> a.以r的方式打开文件时，encoding是不是必须出现
>     如果文件格式为gbk,可以不加encoding="gbk"
>     如果文件格式为utf-8,必须添加encoding="utf-8"
> b。如果打开的文件是图片，音频或者视频等，打开方式采用rb,但是，此时，不能添加encoding="xxx"
> """
>
> #二、读取文件内容
> #1.读取全部内容   ***********
> #str = f.read()
> #print(str)
>
> #2.读取指定的字符数
> #注意：如果每一行的结尾有个"\n",也被识别成字符
> """
> str1 = f.read(2)
> print(str1)
> str1 = f.read(2)
> print(str1)
> str1 = f.read(2)
> print(str1)
>
>
> #3.读取整行，不管该行有多少个字符    *********
> str2 = f.readline()
> print(str2)
> str2 = f.readline()
> print(str2)
> """
>
> #4.读取一行中的指定的字符
> #str3 = f.readline(3)
> #print(str3)
>
> #5.读取全部的内容，返回的结果为一个列表，每一行数据为一个元素
> #注意：如果指明参数，则表示读取指定个数的字符
> str4 = f.readlines()
> print(str4)
>
> #三、关闭文件
> f.close()
> ```
>
> 其他写法：
>
> ```Python
> #1.读取文件的简写形式
> #with open()  as 变量
>
> #好处：可以自动关闭文件，避免忘记关闭文件导致的资源浪费
> path = "致橡树.txt"
> with open(path,"r",encoding="gbk") as f:
>     result = f.read()
>     print(result)
>
> #2.
> try:
>     f1 = open(path,"r",encoding="gbk")
>     print(f1.read())
> except FileNotFoundError as e:
>     print("文件路径错误",e)
> except LookupError as e:
>     print("未知的编码格式",e)
> except UnicodeDecodeError as e:
>     print("读取文件解码错误",e)
> finally:
>     if f1:
>         f1.close()
> ```
>
> 读取图片等二进制文件：
>
> ```Python
> #1.
> f = open("dog.jpg","rb")
>
> result = f.read()
> print(result)
>
> f.close()
>
> #2
> with open("dog.jpg","rb") as f1:
>     f1.read()
>
> #注意：读取的是二进制文件，读取到的内容为\xff\xd8\xff\xe0\x00\x10JFIF\x00\x01\x01\x01\x00H\x00H\x00\x00\xff\xdb\x0
> ```

##### 2.2写文件

> 操作步骤：
>
> ​	a.打开文件：open()
>
> ​	b.写入数据：write()
>
> ​	c.刷新管道【内部缓冲区】：flush()
>
> ​	d.关闭文件：close()
>
> 代码演示：
>
> ```Python
> path = "file1.txt"
>
> #1.打开文件
> #注意：写入文件的时候，文件可以不存在，当open的时候会自动创建文件
> #读取文件的时候，文件必须先存在，才能open
> f = open(path,"w",encoding="utf-8")
>
> #2.写入数据
> #注意：将数据写入文件的时候，默认是没有换行的，如果向换行，则可以手动添加\n
> f.write("Python1805高薪就业，走上人生巅峰")
>
> #3.刷新数据缓冲区
> #作用：加速数据的流动，保证缓冲区的流畅
> f.flush()
>
> #4.关闭文件
> f.close()
>
> #简写形式
> with open(path,"w",encoding="utf-8") as f1:
>     f1.write("hello")
>     f.flush()
> ```

#### 3.编码和解码

> 编码：encode，字符串类型转换为字节类型
>
> 解码：decode，字节类型转换为字符串类型
>
> 注意：编码和解码的格式必须保持一致
>
> 代码演示：
>
> ```Python
> path = "file2.txt"
>
> #编码:字符串----》字节
> with open(path,"wb") as f1:
>     str = "today is a good day 今天是个好天气"
>     f1.write(str.encode("utf-8"))
>
> #解码：字节----->字符串
> with open(path,"rb") as f2:
>     data = f2.read()
>     print(data)
>     print(type(data))
>
>     newData = data.decode("utf-8")
>     print(newData)
>     print(type(newData))
> ```

#### 4.csv文件的读写

> csv:逗号分隔值【Comma Separated  Values】
>
> 一种文件格式，.csv,本质是一个纯文本文件，可以作为不同程序之间数据交互的格式
>
> 打开方式:记事本，excel

##### 4.1读文件

> 代码演示：
>
> ```Python
> #C:\Users\Administrator\Desktop\SZ-Python\Day15\笔记\text.csv
> import  csv
>
>
> #方式一：三部曲
> def readCsv1(path):
>     #1.打开文件
>     csvFile = open(path,"r")
>
>     #2.将文件对象封装成可迭代对象
>     reader= csv.reader(csvFile)
>
>     #3.读取文件内容
>     #遍历出来的结果为列表
>     for item in reader:
>         print(item)
>
>     #4.关闭文件
>     csvFile.close()
>
> readCsv1(r"C:\Users\Administrator\Desktop\SZ-Python\Day15\笔记\text.csv")
>
> #方式二：简写
> def readCsv2(path):
>     with open(path,"r") as f:
>         reader = csv.reader(f)
>         for item in reader:
>             print(item)
>
> readCsv2(r"C:\Users\Administrator\Desktop\SZ-Python\Day15\笔记\text.csv")
> ```

##### 4.2写文件

> 代码演示：
>
> ```Python
> import  csv
>
> #1.从列表写入数据
> def writeCsv1(path):
>     infoList = [['username', 'password', 'age', 'address'],['zhangsan', 'abc123', '17', 'china'],['lisi', 'aaabbb', '10', 'england']]
>
>     #1.打开文件
>     #注意：如果不设置newline，每一行会自动有一个空行
>     csvFile = open(path,"w",newline="")
>
>     #2.将文件对象封装成一个可迭代对象
>     writer = csv.writer(csvFile)
>
>     #3.写入数据
>     for i in range(len(infoList)):
>         writer.writerow(infoList[i])
>
>     #4.关闭文件
>     csvFile.close()
>
> writeCsv1("file3.csv")
>
> #2.从字典写入文件
> def writeCsv2(path):
>     dic = {"张三":123,"李四":456,"王麻子":789}
>     csvFile = open(path, "w", newline="")
>     writer = csv.writer(csvFile)
>
>     for key in dic:
>         writer.writerow([key,dic[key]])
>
>     csvFile.close()
>
> #3.简写形式
> def writeCsv3(path):
>     infoList = [['username', 'password', 'age', 'address'], ['zhangsan', 'abc123', '17', 'china'],
>                 ['lisi', 'aaabbb', '10', 'england']]
>     with open(path, "w", newline="") as f:
>         writer = csv.writer(f)
>
>         for rowData in infoList:
>             writer.writerow(rowData)
> ```

#### 