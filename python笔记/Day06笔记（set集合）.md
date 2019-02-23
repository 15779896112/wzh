### 一、set集合【了解】

#### 1.概述

> 和数学上的集合基本是一样的，
>
> 特点:不允许有重复元素，可以进行交集，并集，差集的运算
>
> 本质：无序，无重复元素的集合

#### 2.创建

> set(列表或者元组或者字典)
>
> 代码演示：
>
> ```Python
> #注意：set的创建需要借助于list和tuple
>
> #1.通过list创建set
> list1 = [432,5,5,46,65]
> s1 = set(list1)
> print(list1)
> print(s1)
>
> #注意1：set中会自动将重复元素过滤掉
>
> #2.通过tuple创建set
> tuple1 = (235,45,5,656,5)
> s2 = set(tuple1)
> print(tuple1)
> print(s2)
>
> #3.通过dict创建set
> dict1 = {1:"hello",2:"good"}
> s3 = set(dict1)
> print(dict1)   #{1: 'hello', 2: 'good'}
> print(s3)   #{1, 2}
>
> #注意2：set跟dict类似，都使用{}表示，但是与dict之间的区别在于：set中相当于只存储了一组key，没有value
> ```

#### 3.操作

##### 3.1添加

> 代码演示：
>
> ```Python
> #1.添加
> #add()   在set的末尾进行追加
> s1 = set([1,2,3,4,5])
> print(s1)
> s1.add(6)
> print(s1)
>
> #注意：如果元素已经存在，则添加失败
> s1.add(3)
> print(s1)
> #print(s1.add(3))
>
> #s1.add([7,8,9])   #TypeError: unhashable type: 'list'  list是可变的，set中的元素不能是list类型
> s1.add((7,8,9))
> #s1.add({1:"a"})  #TypeError: unhashable type: 'dict'  ，dict中的键值对可以改变，set中的元素不能是dict类型
> print(s1)
>
> #update()   插入【末尾添加】，打碎插入【直接将元组，列表中的元素添加到set中，将字符串中的字母作为小的字符串添加到set中】
> s2 = set([1,2,3,4,5])
> print(s2)
> s2.update([6,7,8])
> s2.update((9,10))
> s2.update("good")
> #注意：不能添加整型，因为整型不能使用for循环遍历
> #s2.update(11)   #TypeError: 'int' object is not iterable
> print(s2)
> ```

##### 3.2删除

> 代码演示：
>
> ```Python
> #2.删除
> #remove()
> s3 = set([1,2,3,4,5])
> print(s3)
> s3.remove(3)
> print(s3)
> ```

##### 3.3遍历

> 代码演示：
>
> ```Python
> #3.set的遍历
> s4 = set([1,2,3,4,5])
> for i in s4:
>     print(i)
>
> #注意：set是没有索引的，所以不能通过s4[2]获取元素，原因：set是无序的
> #print(s4[2])  #TypeError: 'set' object does not support indexing
>
> #注意：获取的是编号和元素值
> for i,num in enumerate(s4):
>     print(i,num)
> ```

##### 3.4交集和并集

> 代码演示：
>
> ```Python
> #4.交集和并集
> s4 = set([1,2,3])
> s5 = set([4,5,3])
>
> #交集：&【按位与】    and
> r1 = s4 & s5
> print(r1)
> print(type(r1))
>
> #并集:|【按位或】   or
> r2 = s4 | s5
> print(r2)
> ```

### 三、简单算法【掌握】

> 代码演示：
>
> ```Python
> #需求：求列表中元素的最大值，不能借助于系统功能
> list1 = [5,54,6,774,43,44]
>
> #方式一
> #定义一个变量，用于记录最大值【参照物】
> #思路：如果要操作列表，初始值一般使用列表的第一个元素
> maxValue = list1[0]
> for num in list1:
>     if num > maxValue:
>         #给maxValue重新赋值
>         maxValue = num
> print(maxValue)
>
> #方式二
> maxValue1 = list1[0]
> for index in range(1,len(list1)):
>     if list1[index]  > maxValue1:
>         maxValue1 = list1[index]
>
> print(maxValue1)
>
> #需求升级：获取最大值以及最大值对应的下标
> maxValue2 = list1[0]
> maxIndex = 0
> for index in range(1, len(list1)):
>     if list1[index] > maxValue2:
>         maxValue2 = list1[index]
>         maxIndex = index
>
> print(maxValue2,maxIndex)
> ```

#### 1.排序

##### 1.1冒泡排序

> 排序思路：比较两个相邻下标对应的元素，如果以升序为例的话，则最大值出现在最右边
>
> 代码实现：
>
> ```Python
> list1 = [34,5,46,23,23,54,65,54]
>
> #升序排序：冒泡
> #外层循环：控制比较的轮数
> for out in range(0,len(list1) - 1):
>     #内层循环;控制每一轮比较的次数，兼顾参与比较的下标
>     for inner in range(0,len(list1) - out - 1):
>         if list1[inner] > list1[inner + 1]:
>             #方式一
>             temp = list1[inner]
>             list1[inner] = list1[inner + 1]
>             list1[inner + 1] = temp
>
>             #方式二：简写
>             #list1[inner],list1[inner + 1] = list1[inner + 1],list1[inner]
> print(list1)
>
> """"
> for inner in range(0,len(list1) - out):
> IndexError: list index out of range
>
> 原因分析：当out取值为0的时候，inner的取值范围为0~len(list1) - 1
>           当使用if list1[inner] > list1[inner + 1]:，当inner取值为len(list1) - 1，此时inner+1变成了len(list1)
> 解决办法：for inner in range(0,len(list1) - out - 1):
>         当out取值为0的时候，此时inner的取值范围：0~len(list1) - 2
>         假设元素个数为5，inner当取值为3的时候，inner+1取值为4，正好是索引的最大值的边界
> """
> ```

##### 1.2选择排序

> 排序思路：固定一个下标，然后拿这个下标对应的元素和其他的元素依次进行比较，最小值出现在最左边
>
> 代码演示：
>
> ```Python
> list1 = [34,5,46,23,23,54,65,54]
>
> #排序方式：选择排序
>
> #外层循环：控制比较的轮数
> for out in range(0,len(list1) - 1):
>     #内层循环：控制每一轮比较的次数，兼顾参与比较的下标
>     for inner in range(out + 1,len(list1)):
>         """
>             0-1  0-2  0-3  0-4
>             1-2  1-3  1-4
>             2-3  2-4
>             3-4
>         """
>         #out表示小的下标，inner的最小值out+1
>         if list1[out] > list1[inner]:
>             temp = list1[out]
>             list1[out] = list1[inner]
>             list1[inner] = temp
> print(list1)
>
> #注意：注意区分冒泡和选择的边界问题
> ```

### 三、String字符串

#### 1.概述

> 由多个字母，数字，特殊字符组成的有限序列
>
> 在Python中，使用单引号或者双引号都可以表示字符串
>
> 注意:没有单符号的数据类型
>
> 'a'   "a"

#### 2.创建字符串

> 代码演示：
>
> ```Python
> str1 = "hello"
>
> str2 = "abc1234"
>
> str3 = "***fhhg%%%"
>
> str4 = "中文"
> ```

#### 3.字符串运算

> 代码演示：
>
> ```Python
> #1.+   字符串连接
> s1 = "welcome"
> s2 = " to China"
> print(s1 + s2)
>
> #注意：在Python中，使用+。只能是字符串和字符串之间。和其他数据类型使用的话不支持
> #print("abc" + 10)
> #print("123" + 1)
> #print(1 + "12" + 12)
> #print("hello" + True)
>
> #2. *   字符串重复
> s3 = "good"
> print(s3 * 3)
>
> #3.获取字符串中的某个字符
> """
> 类似于列表和元组的使用，通过索引来获取指定位置的字符
> 注意索引的取值范围【0~长度 - 1】，同样会出现索引越界
> 访问方式：字符串名称[索引]
> """
> s4 = "abcdef"
> print(s4[1])
> #print(s4[10])  #IndexError: string index out of range
>
> #获取字符串的长度：len()
> #遍历字符串,和list，tuple的用法完全相同
> for element in s4:
>     print(element)
> for index in range(0,len(s4)):
>     print(s4[index])
> for index,str in enumerate(s4):
>     print(index,str)
>
> #4.截取字符串【切片】
> str1 = "hello world"
> #指定区间
> print(str1[3:7])
> #从指定位置到结尾，包含指定位置
> print(str1[3:])
> #从开头到指定位置，但是不包含指定位置
> print(str1[:7])
>
> str2 = "abc123456"
> print(str2[2:5]) #c12
> print(str2[2:])  #c123456
> print(str2[2::2])  #c246
> print(str2[::2])   #ac246
> print(str2[::-1])  #654321cba   倒序
> print(str2[-3:-1])  #45   -1表示最后一个字符
>
> #5.判断一个子字符串是否在原字符串中
> #in  not in
> str3 = "today is a good day"
> print("good"  in str3)
> print("good1"  not in str3)
> ```

#### 4.格式化输出

> 通过%来改变后面字母或者数字的含义，%被称为占位符
>
> ​	%d          整数
>
> ​	%f		浮点型，特点：可以指定小数点后的位数
>
> ​	%s		字符串
>
> 代码演示：
>
> ```Python
> #6.格式化输出
> num = 10
> string1 = "hello"
> print("string1=",string1,"num=",num)
> #注意：变量的书写顺序尽量和前面字符串中出现的顺序保持一致
> print("string1=%s,num=%d"%(string1,num))
>
> f = 12.247
> print("string1=%s,num=%d,f=%f"%(string1,num,f))
> #需求：浮点数保留小数点后两位
> print("string1=%s,num=%d,f=%.2f"%(string1,num,f))    #round(12.247,2)
> ```

#### 5.常用转义字符

> 通过\来改变后面字母或者特殊字符的含义
>
> ​	\t  		相当于tab键
>
> ​	\n		相当于enter键
>
> ​	\b		相当于backspace
>
> 代码演示：
>
> ```Python
> #7.转义字符
> string2 = "hello\tworld"
> string21 = "hello   world"
> print(string2)
> print(string21)
>
> #换行：\n    多行注释
> string3 = "hello\nPython"
> string31 = """hello
> python2354623
> """
> print(string3)
> print(string31)
>
> #需求："hello"
> print("\"hello\"")
>
> #C:\Users\Administrator\Desktop\SZ-Python1805\Day6\视频
> print("C:\\Users\\Administrator\\Desktop")
> #注意;如果一个字符串中有多个字符需要转义，则可以在字符串的前面添加r,可以避免对字符串中的每个特殊字符进行转义
> print(r"C:\Users\Administrator\Desktop")
> ```

​	