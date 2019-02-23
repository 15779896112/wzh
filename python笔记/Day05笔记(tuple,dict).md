### 一、break、continue和pass语句的使用

#### 1.break

> 作用:跳出循环【直接跳出整个循环，继续执行循环后面的代码】
>
> 代码演示：
>
> ```Python
> #break的使用
> #1.while
> n = 0
> while n < 5:
>     print("n = %d"%(n))
>     #print("n =" ,n)
>     #注意：if语句充当的是一个条件判断
>     if n == 3:
>         break
>     n += 1
> print("over")
>
> #2.for
> list1 = [1,2,3,4,5]
> for x in list1:
>     print("x = %d"%(x))
>     if x == 3:
>         break
> #结论：不管是while语句还是for语句，break的作用结束整个循环
>
> #3.特殊情况一
> #不管while中的条件是否满足，else分支都会被执行
> #思考问题：如果在while循环体中出现了break，else分支还会执行吗？-------不会
> m = 0
> while m < 3:
>     print(m)
>     if m == 1:
>         break
>     m += 1
> else:
>     print("else")
>
> #4.特殊情况二
> #当break使用在嵌套循环中的时候，结束的是当前循环【就近原则】
> x = 0
> y = 0
> while x < 20:
>     print("hello Python",x)
>     x += 1
>     while y < 5:
>         print("hello Python~~~~",y)
>         if y == 2:
>             break
>         y += 1
>     #break
>
> #注意：break是一个关键字，使用的过程中，单独就可以成为一条语句，后面不能跟任何的变量或者语句
> ```

#### 2.continue

> 作用：跳出当前正在执行的循环，继续执行下一次循环
>
> 代码演示：
>
> ```Python
> #continue的使用
>
> #1.for
> for i in range(10):
>     print(i)
>     if i == 3:
>         continue
>     print("*")
>
> for i in range(10):
>     print(i)
>     if i == 3:
>         break
>     print("*")
>
> #总结：continue只是结束当前正在执行的循环，而break表示直接结束整个循环
>
> # 2.while
> """
> num = 0
> while num < 10:
>     print("num = %d"%(num))
>     num += 1
>     if num == 3:
>         continue
> """
> num = 0
> while num < 10:
>     if num == 3:
>         num += 1
>         continue
>     print("num = %d" % (num))
>     num += 1
> ```

#### 3.pass

> Python中的pass是一条空语句
>
> 作用：为了保持代码结构的完整性，pass不做任何操作，只是充当了一个占位语句，保证代码可以正常的运行起来
>
> 应用场景：if，while，for中使用，可以在代码块的部分不添加任何语句，代码正常运行
>
> 代码演示：
>
> ```Python
> while True:
>     pass
>
> print("over")
> ```

#### 4.练习

> 代码演示：
>
> ```Python
> #需求;判断一个数是否是素数【质数】
> #方式一
> num1 = int(input("请输入一个数："))
> #思路：一个数能被其他数整除，将次数记录下来
> #条件：在2~num1 - 1的范围内，找到一个数能将num1整除，count1 + 1
> count1 = 0
> for i in range(2,num1):
>     #整除：求余【大数对小数求余】
>     if num1 % i == 0:
>         count1 += 1
>
> if count1 == 0 and num1 != 1:
>     print("是质数")
> else:
>     print("不是质数")
>
> #方式二：
> #思路：假设num2是质数，寻找不成立的条件【有数能被整除】将假设推翻掉
> num2 = int(input("请输入一个数："))
> #定义一个布尔类型的变量，用于记录这个数是不是一个质数
> is_prime  = True
> for j in range(2,num2):
>     if num2 % j == 0:
>         is_prime = False
>         break
>
> if is_prime == True and num2 != 1:
>     print("是质数")
> else:
>     print("不是质数")
> ```

### 三、布尔值和空值

#### 1.布尔值

> 一个布尔类型的变量一般有两个值，True,False
>
> 作用：用于分支和循环语句中作为条件判断
>
> 代码演示：
>
> ```Python
> #Boolean
> b1 = True
> b2 = False
>
> #条件表达式或者逻辑表达式结果都是布尔值
> print(4 > 5)
> print(1 and 0)
> ```

#### 2.空值

> Python中的一种特殊的数据类型，使用None表示
>
> 区别与0：0是数字类型，None本身就是一种数据类型
>
> 代码演示：
>
> ```Python
> #空值
> n = None
> print(n)   #None
> ```

### 四、数字类型Number

#### 1.分类

##### 1.1整数

> 可以处理Python中任意大小的整型
>
> 代码演示：
>
> ```Python
> num1 = 10
> num2 = num1
> print(num1,num2)
>
> #1.可以连续定义多个同种类型的变量,初始值相同
> num3 = num4 = num5 = 100
>
> #2.同时定义多个变量，初始值不同
> num6,num7 = 60,70
> print(num6,num7)
>
> #3.可以交换两个变量的值【掌握】
> #自己实现
> nn1 = 22
> nn2 = 33
> temp = nn1
> nn1 = nn2
> nn2 = temp
> print(nn1,nn2)
>
> n1 = 22
> n2 = 33
> print(n1,n2)   #22  33
> n1,n2 = n2,n1
> print(n1,n2)
>
> #4.获取变量在内存中的地址
> print(id(num1),id(num2))
> ```

##### 1.2浮点数

> 由整数部分和小数部分组成
>
> 注意：浮点数在计算机中运算的时候可能会出现四舍五入

##### 1.3复数

> 由实数部分和虚数部分组成
>
> 表示形式：a + bj或者complex(a,b)

#### 2.数字类型转换

> int(x):将x转换为整数
>
> float(x)：将x转换为一个浮点数
>
> 代码演示：
>
> ```Python
> print(int(1.9))   #1   取整
> print(float(1))   #1.0
> print(int("123"))   #123
> print(float("12.3")) #12.3
>
> #使用int或者float进行转换的时候，如果字符串中出现特殊符号，则转换失败
> #print(int("abc123"))   #ValueError: invalid literal for int() with base 10: 'abc123'
>
> print(int("+123"))   #123，当做数学上的正负号
> #print(int("12+3"))   #ValueError: invalid literal for int() with base 10: '12+3'
> print(int("-123"))  #-123
> #print(int("12-3"))  #ValueError: invalid literal for int() with base 10: '12-3'
> ```

#### 3.系统功能

##### 3.1数学功能

> abs(x):  absolute 求x的绝对值
>
> max():求最大值
>
> min()：求最小值
>
> pow(n,m):求一个数的多少次幂
>
> round(x，n):返回浮点数x的四舍五入值,如果给出n值，则表示舍入到小数点后几位
>
> 代码演示：
>
> ```Python
> print(abs(-10))
>
> print(max(23,34,6,56,57,6))
> print(min(23,34,6,56,57,6))
>
> print(pow(3,5))
>
> print(round(3.456))   #3
> print(round(3.656))   #4
> print(round(3.656,2))  #3.66
> print(round(3.646,1))   #3.6
> ```
>
> 导入math模块，math.功能名()
>
> 代码演示：
>
> ```Python
> #以下的功能必须导入math模块
> import  math
>
> #使用格式：math.功能名称
>
> #19向上取整
> print(math.ceil(18.1))
> print(math.ceil(18.9))
>
> #18向下取整
> print(math.floor(18.1))
> print(math.floor(18.9))
>
> #求平方
> print(pow(3,2))
> #开平方【掌握】
> print(math.sqrt(9))
>
> #获取整数部分和小数部分，得到的结果为元组
> print(math.modf(22.3))
> ```

##### 3.2随机数random【掌握】

> 代码演示：
>
> ```Python
> import random
>
> #1.random.choice(列表)  从指定列表中随机选择一个元素出来
> #指定列表
> num1 = random.choice([1,3,5,7,9])
> print(num1)
>
> #列表生成器
> num2 = random.choice(range(5))   #等价于[0,1,2,3,4]
> print(num2)
>
> #使用字符串，相当于使用了元素为字母的列表
> num3 = random.choice("hello")  #等价于["h","e","l","l","o"]
> print(num3)
>
> #需求;产生一个4~10之间的随机数
> print(random.choice([4,5,6,7,8,9,10]))
> print(random.choice(range(4,11)))
>
> #2.random.randrange(start,end,step)
> """
> start:指定范围的开始值，包含在范围内，默认为0
> end:指定范围的结束值，不包含在范围内
> step:步长，指定的递增基数，默认为1
> """
>
> #需求1：从1~100之间选取一个奇数随机数
> print(random.choice(range(1,100,2)))
> print(random.randrange(1,100,2))
> #需求2：生成一个0~99之间的随机数
> print(random.randrange(100))
>
> #3.random.random()   获取0~1之间的随机数，结果为浮点型
> n = random.random()
> #需求：保留小数点后两位
> print(round(n,2))
>
> #需求1：获取4~10之间的随机数
> n1 = random.random() * 6 + 4
> """
> [0,1] * 6 --------->[0,6]
> [0,6] + 4 -------->[4,10]
> """
>
> #4.将列表中的元素进行随机排序【了解】
> list1 = [23,5435,4,6]
> random.shuffle(list1)
> print(list1)
>
> #5.随机生成一个实数，它在[3,9]范围内，结果为浮点型
> print(random.uniform(3,9))
>
> #需求：求50~100之间的随机数，包括浮点数
> n2 = random.uniform(50,100)
> ```

##### 3.3三角函数功能【了解】

### 五、tuple元组

#### 1.概述

> 和列表相似，本质上是一种有序的集合
>
> 元组和列表的不同之处：
>
> ​	a.列表:[]     元组：()
>
> ​	b.列表中的元素可以进行增加和删除操作，但是，元组中的元素不能修改【元素：一旦被初始化，将不能发生改变】

#### 2.创建元组

> 创建列表:
>
> ​	创建空列表：list1 = []
>
> ​	创建有元素的列表：list1 = [元素1，元素2，。。。。。]
>
> 创建元组
>
> ​	创建空元组：tuple1 = ()
>
> ​	创建有元素的元组：tuple1 = (元素1，元素2，。。。。)
>
> 代码演示：
>
> ```Python
> #创建空元组：
> tuple1 = ()
>
> #创建有元素的元组：
> tuple2 = (10,20,30)
>
> #在元组中可以存储不同类型的数据
> tuple3 = ("hello",True,100)
>
> #注意：创建只有一个元素的元组
> #按照下面的方式书写，表示定义了一个整型的变量，初始值为1
> tuple4 = (1)
> tuple4 = 1
> #为了消除歧义，修改如下：
> tuple4 = (1,)
>
> num1 = 10
> num2 = (10)
> print(num1,num2)
> ```

#### 3.元组元素的访问

> 代码演示：
>
> ```Python
> #元组元素的访问
> #格式：元组名[索引],和列表完全相同
> tuple1 = (10,20,30,40,50)
> #1.获取元素值
> print(tuple1[2])
> #获取元组中的最后一个元素
> print(tuple1[4])
> #print(tuple1[5])  #IndexError: tuple index out of range  索引越界
>
> #正数表示从前往后获取，负数表示从后往前获取
> print(tuple1[-1])
> print(tuple1[-2])
> print(tuple1[-5])
> # print(tuple1[-6])   #IndexError: tuple index out of range  索引越界
>
> #2.修改元素值----->不能修改，本质原因不能修改元素的地址
> #和列表不同的地方：元组的元素值不能随意的更改
> #tuple1[1] = 100
> tuple2 = (1,35,54,[4,5,6])
> #获取元组中列表中的元素
> print(tuple2)   #(1, 35, 54, [4, 5, 6])
> tuple2[3][1] = 50
> print(tuple2)  #(1, 35, 54, [4, 50, 6])
>
> #3.删除元组
> tuple3 = (53,6,7,76)
> del tuple3
> ```

#### 4.元组操作

> 代码演示：
>
> ```Python
> #1.元组组合
> #+
> tuple1 = (3,43,5,4)
> tuple2 = (3,5,45,4)
> print(tuple1 + tuple2)
>
> #2.元组重复
> #*
> print(tuple1 * 3)
>
> #注意：元组组合和元组重复得到的是一个新的元组，原来的元组并没有发生任何改变
>
> #3.判断元素是否在元组中
> #成员运算符
> #in    not in
> print(100 in tuple1)
> print(100 not in  tuple1)
>
> #4.元组截取【切片】
> tuple3 = (1,23,43,54,54,656,57,6)
> print(tuple3[2:4])
> print(tuple3[2:])
> print(tuple3[:4])
> ```

#### 5.元组功能

> 代码演示：
>
> ```Python
> #1.获取元组的元素个数
> tuple1 = (54,3,5,46,56)
> print(len(tuple1))
>
> #2.获取元组中元素的最大值和最小值
> print(max(tuple1))
> print(min(tuple1))
>
>
> #3.元组和列表之间的相互转换:取长补短
> #3.1   元组-----》列表
> #list()
> list1 = list(tuple1)    #int()   float()
> print(list1)
>
> #3.2  列表------》元组
> #tuple()
> list2 = [34,5,46,4]
> tuple2 = tuple(list2)
> print(tuple2)
>
> #4.遍历元组
> #4.1直接遍历元素
> for element in tuple1:
>     print(element)
>
> #4.2遍历索引
> for index in range(len(tuple1)):
>     print(tuple1[index])
>
> #4.3同时遍历索引和元素
> for i,num in enumerate(tuple1):
>     print(i,num)
> ```

#### 6.二维元组

> 代码演示：
>
> ```Python
> #当做一维元组进行处理，实质：一维元组中的元素为一个一维元组
> tuple1 = ((2,43,5),(54,65,6),(5,54,54,54))
> print(tuple1[1][1])
>
> #遍历二维列表或者二维元组的思路：嵌套循环
> #遍历外层元组
> for element in tuple1:
>   	#遍历内层元组
>     for num in elment:
>       print(num)
> ```

### 六、dict字典

#### 1.概述

> 思考问题：保存多个学生的成绩
>
> list1 = [65,7,8,99,100]
>
> tuple1 = (65,7,8,99,100)
>
> 存在的问题：无法学生和成绩的匹配
>
> 解决问题：字典，将学生姓名作为key，成绩作为value，进行存储，方便查找
>
> 本质：也只一种存储数据的方式，数据是以键值对的形式存储的，但是字典是无序的
>
> 优点：具有快速查找的优势

#### 2.key的特性

> a.字典中的key必须是唯一的
>
> b.字典中的key必须是不可变的
>
> ​	list是可变的，不能充当key		
>
> ​	tuple是不可变的，可以充当key，整数，字符串都可以充当key

#### 3.字典的创建

> 语法：字典名称 = {key1:value1,key2:value2,.......}
>
> 代码演示：
>
> ```Python
> #创建空字典
> dict1 = {}
>
> #创建带有键值对的字典
> dict2 = {"zhangsan":96,"lisi":60,"jack":80}
> print(dict2)
> ```

#### 4.元素访问【掌握】

##### 4.1 获取

> 语法：字典名[key]
>
> 代码演示：
>
> ```Python
> #字典中元素的访问
> dict1 = {"zhangsan":96,"lisi":60,"jack":80}
> #1.获取
> #通过key获取对应的value
> score = dict1["lisi"]
> print(score)
>
> #如果key不存在的时候，无法访问
> #print(dict1["tom"])  #KeyError: 'tom'
>
> #虽然key不存在，但是不会报错，返回的是None
> result = dict1.get("tom")
> print(result)
> if result == None:
>     print("key不存在")
> else:
>     print("key是存在的")
> ```

##### 4.2 添加

> 代码演示：
>
> ```Python
> #2.修改和添加
> print(dict1)
> #当key不存在的时候，表示添加一对键值对
> dict1["tom"] = 70
> print(dict1)
> #当key存在的时候，表示修改对应的value
> dict1["lisi"] = 88
> print(dict1)
> ```

##### 4.3 删除

> 代码演示：
>
> ```Python
> #3.删除
> #注意：删除指定的key，则对应的value也会随着被删除
> dict1.pop("lisi")
> print(dict1)
> ```

#### 5.字典的遍历【掌握】

> 代码演示：
>
> ```Python
> dict1 = {'zhangsan': 96, 'lisi': 88, 'jack': 80, 'tom': 70}
>
> #1.只获取key【掌握】
> for key in dict1:
>     #通过key获取value
>     value = dict1[key]
>     print(key,"=",value)
>
> #2.只获取value
> #将所有的value重新生成了一个列表
> list1 = dict1.values()
> print(list1)
> for value in list1:
>     print(value)
>
> #3.同时获取键值对的索引以及key
> for i,key in enumerate(dict1):
>     print(i,key)
>     print(dict1[key])
>
> #4.同时获取key和value【掌握】
> for key,value in dict1.items():
>     print(key,value)
> ```

#### 6.练习

> 代码演示：
>
> ```python
> #1.逐一显示指定字典中的所有键，并在显示结束之后输出总键数
> dict1= {"x":1,"y":2,"z":3}
> #count1 = 0
> for key in dict1:
>     print(key)
>     #count1 += 1
> else:
>     print(len(dict1))
>
> #2.list1 = [0,1,2,3,4,5,6],list2 = ["Sun","Mon","Tue","Wed","Thu","Fri","Sat"].以list1中的元素作为key，
> # 以list2中的元组作为value生成一个新的字典dict2
> list1 = [0,1,2,3,4,5,6]
> list2 = ["Sun","Mon","Tue","Wed","Thu","Fri","Sat"]
> dict2 = {}
> #{0:"Sun",1:"Mon".....}
>
> #定义一个变量，作为list1和list2的索引
> index = 0
>
> #前提：两个列表的长度相等
> if len(list1) == len(list2):
>
>     while index < len(list1):
>         #当字典中不存在某个key-value时，赋值于相当于添加一对键值对
>         dict2[list1[index]] = list2[index]    #dict2[0] = "Sun"
>         #为了循环可以在适当的时机停止下来，可以将list1和list2中的元素全部获取出来，赋值给字典
>         index += 1
>
> print(dict2)
> ```