### 一、string字符串【掌握】

#### 1.常用功能

##### 1.1获取长度和次数

> 代码演示：
>
> ```Python
> #1.计算字符串长度  len
> #类似于list和tuple的中获取长度的用法
> str1 = "hfufhja"
> l = len(str1)
> print(l)
>
> #2,计算某个字符或者子字符串在原字符串中出现的次数   count
> str2 = "this is a good day good day"
> #count(str,[start,end])
> #在整个字符串中进行查找
> print(str2.count("day"))
> #在指定区间内进行查找
> print(str2.count("day",3,10))
> ```

##### 1.2大小写转换

> 代码演示：
>
> ```Python
> #注意：使用字符串中的功能，一般情况下，都是生成一个新的字符串，原字符串没有发生任何变化
> #3.大小写字母转换
> #lower()   将字符串中的大写字母转换为小写
> str31 = "Today Is a Good day"
> astr31 = str31.lower()
> print(astr31)
>
> #uppper()   将字符串中小写字母转换为大写
> str32 = "Today Is a Good day"
> astr32 = str2.upper()
> print(astr32)
>
> #swapcase()     将字符串中小写字母转换为大写，大写字母转换为小写
> str33 = "Today Is a Good day"
> astr33 = str33.swapcase()
> print(astr33)
>
> #capitalize()   将一句英文中首单词的首字母转化为大写，其他小写
> str34 = "today Is a Good day"
> astr34 = str34.capitalize()
> print(astr34)
>
> #title()       将一句英文中每个单词的首字母大写
> str35 = "today is a good day"
> astr35 = str35.title()
> print(astr35)
> ```

##### 1.3整数和字符串转换

> 代码演示：
>
> ```Python
> 4.字符串和数字之间的转换
> #int()     float()      str()
> #eval(str)   将str转换为有效的表达式，参与运算，并返回运算结果
> num1 = eval("123")
> print(num1)
> #print("123")
> print(type(num1))
> print(int("123"))
>
> #eval和int将+和-当做正负号处理
> print(eval("+123"))
> print(int("+123"))
> print(eval("-123"))
> print(int("-123"))
>
> #将12+3字符串转换为了有效的表达式，并运算了结果
> print(eval("12+3"))    #15
> #不成立
> #print(int("12+3"))   #ValueError: invalid literal for int() with base 10: '12+3'
>
> print(eval("12-3"))   #9
> #print(int("12-3"))    #ValueError: invalid literal for int() with base 10: '12-3'
>
> #print(eval("a123"))  #NameError: name 'a123' is not defined
> #print(int("a123"))  #ValueError: invalid literal for int() with base 10: 'a123'
>
> #总结：注意区分eval和int【eval：转换有效的表达式   int:将字符串转换为整型】
> ```

##### 1.4填充

> 代码演示：
>
> ```Python
> #5.填充【了解】
> #center（width[,fillchar]）  返回一个指定宽度的居中字符串，width是填充之后整个字符串的长度，fillchar为需要填充的字符串，默认使用空格填充
> str1 = "hello"
> print(str1.center(20))
> print(str1.center(10,"*"))
>
> #ljust（width[,fillchar]） 返回一个指定宽度的字符串，将原字符串居左对齐，width是填充之后整个字符串的长度
> print(str1.ljust(40,"%"))
>
> #rjust width[,fillchar]）  返回一个指定宽度的字符串，将原字符串居右对齐，width是填充之后整个字符串的长度
> print(str1.rjust(40,"%"))
>
> #zfill（width）   返回一个指定宽度的字符串,将原字符串居右对齐,剩余的部分使用的数字0填充
> print(str1.zfill(40))
> ```

##### 1.5查找

> 代码演示：
>
> ```Python
> #6.查找【掌握】
> str2 = "abcdefhello123hello"
> #find（str[,start,end]）  从左到右依次检测，str是否在原字符串中，，也可以指定查找的范围
> #特点;得到的子字符串第一次出现的开始字符的下标，如果查找不到则返回-1
> print(str2.find("hello"))    #6
> print(str2.find("e"))
> print(str2.find("yyy"))    #-1
> print(str2.find("e",3,10))
>
> #rfind(str[,start,end]）   类似于find，从右向左进行检测
> print(str2.rfind("hello"))  #14
>
> #index   和find的使用基本相同，唯一的区别在于如果子字符串查找不到，find返回-1，而index则直接报错
> print(str2.index("hello"))
> #print(str2.index("yyy"))   #ValueError: substring not found
>
> #rindex  和rfind的使用基本相同
>
> #max(str)   获取str中最大的字母【在字典中的顺序】
> #"abcdefhello123hello"
> print(max(str2))
>
> str3 = "46732647"
> print(max(str3))
>
> #min（str）  获取str中最小的字母【在字典中的顺序】
> ```

##### 1.6提取

> 代码演示：
>
> ```Python
> #7.提取字符串
> #strip(str)    使用str作为条件提取字符串，除了两头指定的字符串
> str1 = "********today is *********a good day*******"
> print(str1.strip("*"))   #today is *********a good day
>
> #lstrip(str)    提取字符串，除了左边的指定字符串
> str11 = "********today is *********a good day*******"
> print(str11.lstrip("*"))
>
> #rstrip()
> str12 = "********today is *********a good day*******"
> print(str12.rstrip("*"))
> ```

##### 1.7分割和合并

> 代码演示：
>
> ```Python
> #8.分割和合并【掌握：正则表达式】
> #split(str[,num)]   将str作为分隔符切割原字符串，结果为一个列表,如果制定了num，则仅使用num个字符串截取原字符串
> str3 = "today is a good day"
> print(str3.split(" "))   #['today', 'is', 'a', 'good', 'day']
> print(str3.split(" ",2))   #['today', 'is', 'a good day']
>
> #splitlines(flag)   按照换行符【\n，\r,\r\n】分隔，结果为列表
> #flag:False或者不写，则表示忽略换行符；如果True，则表示保留换行符
> str4 = """today
> is
> a
> good
> day
> """
> print(str4.splitlines(True))   #['today', 'is', 'a', 'good', 'day']    ['today\n', 'is\n', 'a\n', 'good\n', 'day\n']
>
> #join(list)    将原字符串作为连接符号，将列表中的元素分别连接起来，结果为字符串，作用和split是相反的
> str5 = "*"
> list1 = ["shangsan","lisi","jack"]
> print(str5.join(list1))
> ```

##### 1.8替换

> 代码演示：
>
> ```Python
> #9.替换
> #replace(old,new[,max])   用new的字符串将old的字符串替换掉.max表示可以替换的最大次数【从左到右】
> str1 = "this is a easy test test test test"
> print(str1.replace("test","exam"))
> print(str1.replace("test","exam",2))
>
> #使用场景：在一定情境下，可以实现字符串的简单加密，加密规则可以自定义
> #maketrans()   创建字符映射的转换表,结果为字典，通过key:value的方式
> #translate(table)
>
> t = str.maketrans("aco","123")
> print(t)   #{97: 54, 99: 56}
>
> str2 = "today is a good day"
> print(str2.translate(t))  #t4d6y is 6 g44d d6y
> ```

##### 1.9判断

> 代码演示：
>
> ```Python
> #10.判断
> #isalpha()   如果字符串中至少包含一个字符并且所有的字符都是字母，才返回True
> print("".isalpha())
> print("abc".isalpha())
> print("abc123".isalpha())   #False
>
> #isalnum   如果字符串中至少包含一个字符并且所有字符都是字母或者数字的时候才返回True
> print("".isalnum())   #False
> print("abc".isalnum())
> print("abc123".isalnum())
> print("123".isalnum())
> print("1abc".isalnum())
> print("1abc￥".isalnum())  #False
>
> #isupper  如果字符串中至少包含一个字符并且出现的字母必须是大写字母才返回True，数字的出现没有影响
> print("".isupper())
> print("aBC".isupper())
> print("123A".isupper())   #True
> print("abc".isupper())
>
> #islower
>
> #istitle   每个单词的首字母必须全部大写才返回True
> print("Good Day".istitle())
> print("good Day".istitle())
>
> #isdigit() 【掌握】   如果字符串中只包含数字，则返回True
> print("abc123".isdigit())
> print("2364".isdigit())
>
> #需求：将用户从控制台输入的字符串转化为整型【全数字】
> str = input()
> if str.isdigit():
>     int(str)
>     print("yes")
>
> ```

##### 1.10前缀和后缀

> 代码演示：
>
> ```Python
> #11.前缀和后缀【掌握】  子字符串是连续的
> #startswith
> str1 = "helloPython"
> print(str1.startswith("hello"))
>
> #endswith
> print(str1.endswith("on"))
> ```

##### 1.11编解码

> 代码演示：
>
> ```Python
> #12.字符串编码和解码
> #注意：主要针对的是中文
> #encode()   默认的编码格式为utf-8
> str2 = "this is 千锋教育"
> print(str2.encode())
> print(str2.encode("utf-8"))
> print(str2.encode("gbk"))
>
> #decode()   bytes对象
> #\xe5\x8d\x83\xe9\x94\x8b\xe6\x95\x99\xe8\x82\xb2
> #print(r"\xe5\x8d\x83\xe9\x94\x8b\xe6\x95\x99\xe8\x82\xb2".decode())    错误
> ```

##### 1.12ASCII码转换

> 代码演示：
>
> ```Python
> #13。ASCII吗的转换
> #ord()
> print(ord("A"))
> print(ord("0"))
>
> #chr()
> print(chr(65))
> print(chr(110))
> ```

#### 2.练习

> 需求一：
>
> ```Python
> #需求1：统计下面字符串中每个单词的出现次数，并生成一个字典，单词为key，次数为value
> """
> 实现思路：
> 1.以空格为切割符切割字符串
> 2.遍历第一步中得到的list
> 3.将单词提取出来，去一个字典中判断
> 4.如果单词不存在，就以该单词作为key，1作为value存储到字典中
> 5.如果单词存在，将对应key的value递增1【修改指定key的value】
> """
> str1 = "tomorrow is sunny day tomorrow is sunny day tomorrow is wind day"
> dict1 = {}    #创建一个空字典，备用
> list1 = str1.split(" ")    #切割字符串
> #方式一：get（）
> """
> for word in list1:      #遍历列表
>     value = dict1.get(word)    #None
>     if value == None:
>         dict1[word] = 1      #往字典中添加键值对
>     else:
>         dict1[word] += 1     #给字典中指定key的value修改值
>
> print(dict1)
> """
> #方式二：成员运算符
> for word in list1:      #遍历列表
>     if word not in dict1:
>         dict1[word] = 1
>     else:
>         dict1[word] += 1
> print(dict1)
> ```

> 需求二：
>
> ```Python
>
> #需求2：从控制台输入一个字符串，表示时间，编写程序，获取这个时间的下一秒
> #例如输入：12:23:33    输出12:23:34
> """
> 思路分析：
> 1.将字符串切割，得到时分秒的数据
> 2.得到时间的下一秒：给秒加1
> 3.12:23:59----》12:24:00    当秒数增加完之后为60的时候，分钟需要增加1，秒数应该置为0
> 4.12:59:59----》13:00：00   当分钟增加完之后为60的时候，时钟需要增加1，分钟置为0
> 5.当时钟增加完之后为24的时候，时钟置为0
> """
> timeStr = input("请输入正确格式的时间：")
>
> timeList = timeStr.split(":")
> h = int(timeList[0])
> m = int(timeList[1])
> s = int(timeList[2])
>
> s += 1
>
> if s == 60:
>     m += 1
>     s = 0
>     if m == 60:
>         h += 1
>         m = 0
>         if h == 24:
>             h = 0
>
> print("%.2d:%.2d:%.2d"%(h,m,s))
>
> #%.2f
> ```

> 需求三：
>
> ```Python
> #需求3：实现简单的购物车功能
> """
> 思路分析
> 1.引导用户选择商品【提供】
> 2.引导用户输入金额
> 3.加入购物车
> 4.查看购物车，计算余额
> """
> product_list  = [
>     ("Mac",10000),
>     ("kindle",500),
>     ("iphone x",8000),
>     ("bike",3000)
> ]
>
> saving = input("请输入金额：")
>
> #定义一个列表，充当购物车
> shopping_car  = []
>
> #判断金额是否是数字
> if saving.isdigit():
>     #将saving转换为整数
>     saving = int(saving)
>
>     while True:
>         #打印商品信息，提供给用户选择
>         for index,p in enumerate(product_list):
>             print(index,":",p)
>
>         #引导用户选择商品
>         choice = input("请输入商品的编号[输入q退出]:")
>
>         #判断编号是否合法
>         if choice.isdigit():
>             choice = int(choice)
>
>             if choice >= 0 and choice < len(product_list):
>                 #将用户选择的商品从product_list取出来
>                 item = product_list[choice]   #元组
>
>                 #item[0] :商品名称   item[1]：商品的价格
>                 if item[1] <= saving:
>
>                     #saving减少
>                     saving -= item[1]
>
>                     #需要将商品添加到购物车对应的list中
>                     shopping_car.append(item)
>
>                 else:
>                     print("余额不足")
>
>             else:
>                 print("不存在的编号")
>         elif choice == "q":
>             print("-------你已经购买如下商品：-------")
>             for i in shopping_car:
>                 print(i)
>
>             print("你还剩余%d元钱"%(saving))
>
>             break
>         else:
>             print("不合法的编号")
> else:
>     print("invalid input")
> ```

