### 一、函数

#### 1.函数概述

##### 1.1认识函数

> 需求:求圆的面积
>
> s = π * r ** 2
>
> 代码演示：
>
> ```Python
> r1 = 6.8
> s1 = 3.14 * r1 ** 2
>
> r2 = 10
> s1 = 3.14 * r2 ** 2
>
> r3 = 2
> s1 = 3.14 * r3 ** 2
>
> r4 = 30
> s1 = 3.14 * r4 ** 2
>
> #define
> def test(r):
>   s = 3.14 * r * 2
>     
> test(6.8)
> test(10)
> test(30)
> ```
>
> 问题:代码重复
>
> ​         后期维护成本太高
>
> ​	代码可读性不高
>
> 解决问题：函数
>
> 在一个完整的项目中，某些功能会被反复使用，那么将这部分功能对应的代码提取出来，当需要使用功能的时候直接使用
>
> 本质：对一些特殊功能的封装
>
> 优点：
>
> ​	a.简化代码结构，提高应用的效率
>
> ​	b.提高代码复用性
>
> ​	c.提高代码的可读性和可维护性
>
> 建议：但凡涉及到功能，都尽量使用函数实现

##### 1.2定义函数

> 语法：
>
> def  函数名(参数1，参数2，参数3....):
>
> ​	函数体
>
> ​	返回值
>
> 说明：
>
> a.函数由两部分组成：声明部分和实现部分
>
> b.def,关键字，是define的缩写，表示定义的意思
>
> c.函数名：类似于变量名，遵循标识符的命名规则，尽量做到顾名思义
>
> d.（）：表示的参数列表的开始和结束
>
> e.参数1，参数2，参数3....   ：参数列表【形式参数，简称为形参】，其实本质上就是一个变量名，参数列表可以为空
>
> f.函数体：封装的功能的代码
>
> g.返回值：一般用于结束函数，可有可无，如果有返回值，则表示将相关的信息携带出去，携带给调用者，如果没有返回值，则相当于返回None    
>
> ​

#### 2.使用函数

##### 2.1简单函数

> 无参无返回值的函数
>
> 代码演示：
>
> ```Python
> #1.无参无返回值的函数
> #函数的声明部分
> def test():
>     #函数的实现部分
>     #函数体
>     print("hello")
> ```

##### 2.2函数的调用

> 定义好函数之后，让函数执行
>
> 格式：函数名(参数列表)
>
> 代码演示：
>
> ```Python
> #print(num)
> #test()
>
> #1.无参无返回值的函数
> #函数的声明部分
> def test():
>     #函数的实现部分
>     #函数体
>     #print("hello")
>     for i in range(10):
>         print(i)
>
> def test():
>     print("~~~~~~")
>
> #注意1：当定义好一个函数之后，这个函数不会自动执行函数体
>
> #2.函数的调用
> #格式：函数名(参数列表)
> #注意2：当调用函数的时候，参数列表需要和定义函数时候的参数列表保持一致
> #注意3：一个函数可以被多次调用
> test()
> test()
> test()
> test()
>
> #3.注意4：当在同一个py文件中定义多个同名的函数，最终调用函数，调用的最后出现的函数【覆盖：函数名类似于变量名，相当于变量的重新赋值】
> #4.注意5：自定义函数必须先定义，然后才调用，否则报NameError
> ```

> 函数的调用顺序：
>
> ```Python
> #函数调用
> #1.在一个自定义的函数内部也可以调用函数
> #2.函数调用的顺序
> def test1():
>     print("aaaa")
>     test2()
>     print("over")
>
> def test2():
>     print("bbbb")
>     test3()
>     test4()
>
> def test3():
>     print("cccc")
>
> def test4():
>     print("dddd")
>
> test1()
>
> #注意：函数在调用的过程中，相互之间的关系，以及代码执行的先后顺序
> ```

##### 2.3函数中的参数

> 参数列表：如果函数所实现的功能涉及到未知项参与运算，此时就可以将未知项设置为参数
>
> 格式：参数1,参数2.....
>
> 分类：
>
> ​	形式参数：在函数的声明部分，本质就是一个变量，用于接收实际参数的值  【形参】
>
> ​	实际参数：在函数调用部分，实际参与运算的值，用于给形式参数赋值     【实参】
>
> ​	传参：实际参数给形式参数赋值的过程，形式参数 = 实际参数
>
> 代码演示：
>
> ```Python
> #传参：实际参数给形式参数赋值的过程，形式参数 = 实际参数
>
> #需求：给函数一个姓名和一个年龄，在函数内部将内容打印出来
> def myPrint(name,age):
>     print("姓名：%s,年龄：%d"%(name,age))
>
> #调用函数
> str = "zhangsan"
> num = 19
> myPrint(str,num)
>
> """
> 传参：
> 实参给形参赋值
> name = "zhangsan"
> age = 19
> """
>
> #需求：求两个数的和
> def add(num1,num2):
>     sum = num1 + num2
>     print(sum)
>
> add(10,20)
> add(33,2)
>
> #TypeError: add() missing 2 required positional arguments: 'num1' and 'num2'   实参和形参不匹配
> ```
>
> 形参和实参之间的关系：
>
> ```Python
> #需求：交换两个变量的值
> def exchange(num1,num2):
>     temp = num1
>     num1 = num2
>     num2 = temp
>     print("exchange函数内部：num1=%d num2=%d"%(num1,num2))
>
> num1 = 11
> num2 = 22
> exchange(num1,num2)
> print("外面：num1=%d num2=%d" % (num1, num2))
>
> #1.实参和形参重名对函数实现没有影响
> #2.进行传参之后，实际参与运算的是形参，对实参没有影响【将形参可以理解为实参的替代品】
> #3.本质原因：形参和实参在内存中开辟的空间不同
> ```

##### 2.4值传递和引用传递【面试题】

> 值传递：传参的过程中传递的是值，一般指的是不可变的数据类型，number,tuple,string
>
> 引用传递：传参的过程中传递的是引用，一般指的是可变的数据类型，list，dict,set
>
> 代码演示：
>
> ```Python
> #值传递
> def func1(a):
>     a = 10
>
> temp = 20
> #传参：temp,但实际上传的是20
> func1(temp)
> print(temp)   #20
>
>
> #引用传递
> def func2(list1):
>     list1[0] = 100
>
> l = [10,20,30,40]
> func2(l)    #list1 = l
> print(l[0])
>
>
> """
> l = [10,20,30,40]
> list1 = l
> list1[0] = 100
>
> """
> ```
>
> 总结：
>
> 引用传递本质上传递的是内存地址

##### 2.5参数的类型【掌握】

> a.必需参数
>
> ​	调用函数的时候必须以正确的顺序传参，传参的时候参数的数量和形参必须保持一致
>
> 代码演示：
>
> ```Python
> #1.必需参数
> def show1(str1,num1):
>     print(str)
>
> show1("hello",10)
> #show1()
> #如果形参没有任何限制，则默认为必需参数，调用函数的时候则必需传参，顺序一致，数量一致
> ```
>
> b.关键字参数
>
> ​	使用关键字参数允许函数调用的时候实参的顺序和形参的顺序可以不一致，可以使用关键字进行自动的匹配
>
> 代码演示：
>
> ```Python
> #2.关键字参数
> def show2(name,age):
>     age += 1
>     print(name,age)
>
> #正常调用
> show2("abc",10)
> #show2(10,"abc")
>
> #关键字参数调用函数
> #注意1：关键字参数中的关键字其实就是形参的变量名，通过变量名进行传参
> show2(age = 20,name = "lisi")
> show2(name = "lisi",age = 20)
>
> #注意2：关键字参数只有一个的情况下，只能出现在参数列表的最后
> show2("lisi",age = 30)
>
> #错误演示
> #show2(40,name = "lisi")   TypeError: show2() got multiple values for argument 'name'
> #show2(name = "lisi",40)
>
> #系统的关键字参数
> print("",end=" ")
> ```
>
> c.默认参数
>
> ​	调用函数的时候，如果没有传递参数，则会使用默认参数
>
> 代码演示：
>
> ```Python
> #3.默认参数
> #注意1：在形参设置默认参数，如果传参，则使用传进来的数据，如果不传参，则使用默认数据
> def fun1(name,age=18):
>     print(name,age)
>
> fun1("zhangsan",20)
> fun1("lisi")
> fun1(name = "abc",age = 33)
> fun1(name = "hello")
>
> #注意2：在参数列表中，如果所有的形参都是默认参数，正常使用；但是，如果默认参数值只有一个，则只能出现在参数列表的最后面
> def fun2(num1 = 10,num2 = 20):
>     print(num1.num2)
> ```
>
> d.不定长参数
>
> ​	可以处理比当初声明时候更多的参数  *        **
>
> 代码演示：
>
> ```Python
> #4.不定长参数【可变参数】
> #4.1   *   ：被当做tuple处理，变量名其实就是一个元组名
> #注意1：传参的时候，实参可以根据需求任意传参,数量不确定
> #注意2:定义不定长参数时，最好将不定长参数放到参数列表的最后面【如果不定长参数出现在参数列表的前面，则在实参列表中使用关键字参数】
> def func1(name,*hobby):
>     print(name)
>     print(hobby)
>     print(type(hobby))   #<class 'tuple'>
>
>     #遍历
>     for element in hobby:
>         print(element)
>
> func1("aaa","anc","aaa","5435","tesrg","gtsrhesh",10,True)
>
> # 4.2  **   :被当做字典处理，变量名就相当于字典名
> def func2(**args):
>     print(args)
>     print(type(args))   #<class 'dict'>
>
>     for k,v in args.items():
>         print(k,v)
>
> #注意1：使用**的时候，实参就必须按照key=value的方式进行传参
> func2(x = 10,y = 20)
> ```

##### 2.6函数的返回值

> 作用：表示一个函数执行完毕之后得到的结果
>
> 使用:return,表示结束函数，将函数得到的结果返回给调用者
>
> 代码演示：
>
> ```Python
> #1.结束函数，返回数据
> #需求：求两个整数的和，并返回
> def add(num1,num2):
>     sum1 = num1 + num2
>     #print(sum1)
>
>     #将结果返回给调用者
>     return sum1
>
>     #注意：在同一个代码块中，如果在return后面出现语句，则永远不会被执行
>     #print("hello")
>
>
> #注意：如果一个函数由返回值，要么采用变量将返回值接出来，要么将整个函数的调用直接参与运算
> r = add(10,20)
> print(r)
> print(add(10,20))   #30
> #print("~~~~",sum1)
>
> total = add(1,2) + 5
> print(total)    #8
>
>
> def func(num1,num2):
>     sum2 = num1 + num2
>
>
> #注意：如果一个函数没有返回值，则整体计算的结果为None
> #print(func(10,20))
>
> #如果一个函数没有返回值，则这个函数的调用不能直接参与运算
> total1 = func(1,2) + 5  #TypeError: unsupported operand type(s) for +: 'NoneType' and 'int'
> print(total1)
> ```
>
> 在分支语句中使用return
>
> ```Python
> #2.如果一个函数体中有分支，设置了返回值，最好每一个分支都有一个返回值
> #需求：输入两个数，比较两个数的大小，返回较大的一个
> def compare(num1,num2):
>     if num1 > num2:
>         return num1
>     elif num1 < num2:
>         return num2
>     else:
>         return True,num1
>
> result = compare(12,12)
> print(result)
>
> #注意1：在Python中，不同分支返回的数据类型可以是不相同的
> #注意2;在Python中，一个return可以同时返回多个数据，被当做元组处理
> ```

> 总结：
>
> 自定义一个函数
> 是否需要设置参数：是否有未知项参与运算
>
> 是否需要设置返回值：是否需要在函数外面使用函数运算之后的结果

> 函数使用练习：
>
> ```Python
> #需求1：封装函数功能，统计1~某个数范围内能被3整除的数的个数
> """
> 参数：某个数
> 返回值：可设置可不设置
> """
> def getCount(num):
>     count = 0
>     for i in range(num + 1):
>         if i % 3 == 0:
>             count += 1
>
>     #print(count)
>     return count
>
> r1 = getCount(1000)
> print(r1)
> r2 = getCount(100)
> print(r2)
>
>
> #需求2：封装函数功能，判断某年是否是闰年
> """
> 参数：某年
> 返回值：可设置可不设置
> """
> def isLeapYear(year):
>     if (year % 4 == 0 and year % 100 != 0) or year % 400 == 0:
>         #print("闰年")
>         #return "闰年"
>         return  True
>     else:
>         #print("平年")
>         #return "平年"
>         return False
>
> result = isLeapYear(2020)
> print(result)
> ```

#### 3.匿名函数【掌握】

> 不再使用def这种的形式定义函数，使用lambda来创建匿名函数
>
> 特点：
>
> ​	a.lambda只是一个表达式，比普通函数简单
>
> ​	b.lambda一般情况下只会书写一行，包含参数，实现体，返回值
>
> 语法:lambda 参数列表 ： 实现部分
>
> 代码演示：
>
> ```Python
> #语法:lambda 参数列表 ： 实现部分
>
> #1.
> #需求：求两个数的和
> #普通函数
> def add(num1,num2):
>     sum = num1 + num2
>
> add(num1 = 10,num2 = 20)
>
> #匿名函数本身是没有函数名，将整个lambda表达式赋值给一个变量，然后将这个变量当做函数使用
> sum1 = lambda n1,n2:n1 + n2
> print(sum1(10,20))
>
> #2.在匿名函数中也可以使用关键字参数
> g = lambda  x,y:x ** 2 + y ** 2
> print(g(3,4))
> print(g(x = 3,y = 4))
>
> #3.在匿名函数中也可以使用默认参数
> h = lambda  x=0,y=0 : x ** 2 + y ** 2
> print(h())
> print(h(10))
> print(h(10,20))
> ```

#### 4.空函数和主函数

##### 4.1空函数

> 一个什么都没有实现的函数
>
> 借助于pass语句
>
> 代码演示：
>
> ```Python
> def func():
>     pass
> ```

##### 4.2主函数

> 每一个程序都有一个入口：主函数【main函数】
>
> 在Python中，主函数是隐式的
>
> 代码演示：
>
> ```Python
> def show():
>     print("hello")
>
>
> #通过__name__   == "__main__"表示其中的代码是在主函数中运行的
> if  __name__  == "__main__":
>     show()
> ```