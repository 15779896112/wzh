### 一、函数的特殊用法

#### 1.变量可以指向函数

> 代码演示：
>
> ```Python
> #abs------>absolute
>
> #abs（）是一个系统的内置函数【built-in function】
> print(abs(-10))   #10
>
> print(abs)   #<built-in function abs>
>
> #结论一：abs(-10)是函数的调用，而abs是函数本身
>
> x = abs(-20)
> print(x)   #20
>
> f = abs
> print(f)   #<built-in function abs>
>
> #结论二;函数本身也可以直接赋值给一个变量，也就是说：变量可以指向一个函数   num = 10
> #如果一个变量指向了一个函数，则可以通过这个变量去调用这个函数
> print(f(-30))
>
> #结论三：f = abs, 则表示f已经指向了abs所表示的函数，调用abs和调用f实现的效果是一样的
>
> def test():
>     return  "fjskghs"
>
> print(test())
> fun = test
> print(fun())
> ```

#### 2.函数名是一个变量

> 代码演示：
>
> ```Python
> #函数的特殊用法之函数名是一个变量
>
> #结论一：函数名其实就是指向函数的变量
>
> #abs（）：可以将abs看做一个变量，指向了一个可以计算绝对值的函数
>
> #abs更改指向【变量的重新赋值】
>
> num = 10
> num = "hello"
>
> #让abs指向一个整型
> print(abs)
> abs = 10
> print(abs)
>
> #print(abs(-100))
> ```

#### 3.函数作为参数

> 代码演示：
>
> ```Python
> #函数的特殊用法之函数作为参数
>
> #变量可以指向函数，函数名是一个变量，而函数的形参本身就是一个变量，可以接收实参，那么一个函数就可以接收另一个函数作为参数
> #高阶函数【一个函数就可以接收另一个函数作为参数】
>
> #一个简单的高阶函数【需求：求两个数的绝对值的和】
> #参数：x和y就是需要参与运算的数据，fun是一个函数
> """
> def add(x,y):
>     return abs(x) + abs(y)
>
> """
> def add(x,y,fun):
>     return fun(x) + fun(y)    #abs(x) + abs(y)
>
> #将函数名abs作为参数使用
> result = add(-5,6,abs)    #x = -5  y = 6   fun = abs  fun()
> print(result)
>
>
> #自定义函数
> def show():
>     print("abc")
>
> def func(f):
>     print("hello")
>     f()
>
> func(show)
> ```

### 二、偏函数【了解】

> 默认参数：可以降低函数调用的难度
>
> 偏函数：对函数参数做一些控制的函数
>
> 注意：偏函数不需要自定义，直接使用【系统函数】
>
> 代码演示：
>
> ```Python
> import  functools
>
> # 偏函数的使用
>
>
> #int(x)   可以将字符串或者浮点型转换为整型
> #默认：将其中的字符串按照十进制输出
> print(int("123"))
>
> #int（）还提供了一个额外的参数：base
> #print(int("abc123"))
> #base；指明前面数据的进制，int()执行完成之后，最终还是以十进制输出
> print(int("123",base = 10))   #123
> print(int("123",base = 8))    #83
>
>
> print(int("110",base = 2))
> print(int("11010",base = 2))
> print(int("110001",base = 2))
>
> #转换大量的二进制，每次传入base = 2麻烦，可以将这个功能提取出来
> def customInt(x,base=2):
>     return int(x,base)
> print(customInt("110"))  #6
> print(customInt("11010"))  #26
>
> #上面通过默认参数模仿了偏函数的使用，但是系统提供了功能：functools.partial可以创建一个偏函数【前提；需要导入import  functools】
> #参数：需要创建偏函数的原函数名  需要设定的参数
> int2 = functools.partial(int,base=2)
> print(int2("110"))   #6
> print(int2("11010"))  #26
>
> print(int2("110",base=10))   #110
>
> #总结：偏函数
> #主要针对的是系统函数，如果系统默认的操作满足不了需求，则可以在这个系统函数的基础上生成一个新的函数【偏函数】，两个函数可以实现不同的需求
> ```

### 三、闭包【掌握】

> 如果在一个函数的内部定义另外一个函数，外部的函数叫做外函数，内部的函数叫做内函数
>
> 如果在一个外部函数中定义一个内部函数，并且外部函数的返回值是内部函数，就构成了一个闭包，则这个内部函数就被称为闭包【closure】
>
> 代码演示：
>
> ```Python
> """
> 如果在一个函数的内部定义另外一个函数，外部的函数叫做外函数，内部的函数叫做内函数
>
> 如果在一个外部函数中定义一个内部函数，并且外部函数的返回值是内部函数，就构成了一个闭包，
> 则这个内部函数就被称为闭包【closure】
>
> """
>
> #1.最简单的闭包
> #外函数
> def func(str):
>     #内函数【闭包】
>     def innerFunc():
>         print("hello")
>
>     return innerFunc
>
> #f中存储了外函数func的返回值，而func的返回值是innerFunc,j就相当于f = innerFunc
> f = func("abc")   #f = innerFunc
> #f（）就相当于innerFunc()
> f()
>
> #2.
> #a和b被称为外函数中的临时变量【自由变量】
> def outer(a):
>     b = 10
>     def inner():
>         #在内函数中可以直接使用外函数中临时变量
>         print(a + b)
>     return  inner
>
> f1 = outer(5)
> f1()
>
> #3.
> def outer1(num1):
>     def inner1(num2):
>         #在内函数中可以直接使用外函数中临时变量
>         print(num1,num2)
>     return  inner1
>
> f2 = outer1(10)
> f2(20)
>
> #应用场景：装饰器
> ```

### 四、变量的作用域

#### 1.出现的原因

> 变量的作用域：变量可以被使用【被访问】的范围
>
> 程序中的变量并不是在任意的语句中都可以被访问，访问权限取决于这个变量被定义在哪个位置

#### 2.作用范围划分

> 局部作用域：L【Local】
>
> 函数作用域：E【Enclosing】   将变量定义在闭包外的函数中
>
> 全局作用域：G【Global】
>
> 內建作用域：B【Built-in】
>
> 代码演示：
>
> ```Python
> #1.不同作用域变量的定义
>
> num4 = int(2.9)    #B;內建作用域
>
> num3 =  3    #G；全局作用域
>
> def outer():
>     num1 = 1    #E:函数作用域
>
>     def inner():
>         num2 = 2   #L:局部作用域
>
>         #注意：当所有的变量不同名的时候，在闭包中，可以任意访问四种不同作用域对应的变量
>         print(num4,num3,num2,num1)
>
>     return  inner
>
> f = outer()
> f()
> ```

#### 3.变量的查找规则

> 查找的顺序：L------>E------>G------>B【极端情况：当所有的变量同名的情况下】【面试题】
>
> - L：Local 函数内部作用域
> - E：enclosing 函数内部与内嵌函数之间
> - G：global 全局作用域
> - B：build-in 内置作用域
>
> 代码演示：
>
> ```Python
> #变量的查找规则
>
> #注意：全局作用域和内置作用域，当重名的时候，谁出现在后面，则先匹配到谁
> x = 0
>
> x1 = int(3.3)
>
> def outer1():
>     j = 1
>
>     def inner1():
>         i = 2
>         #【就近原则】
>         print(x)
>
>     return  inner1
>
> f1 = outer1()
> f1()
> ```

> ```Python
> #函数
> def show(a):
>     num1 = 10
>     print(num1,a)
> show(20)
> #print(num1,a)
> #结论一：在函数中定义的变量【形参，在函数体中定义的变量】，作用域仅限于函数内部
> # 【变量的生命周随着函数的出现而出现，函数执行完毕则变量随着被销毁】
>
> #if语句
> if True:
>     msg = "hello"
>     print(msg)
> print(msg)
>
>
>  #for循环
> for i in range(0,5):
>     print(i)
> print(i)
>
> #结论二;Python中只有模块【module】、类【class】和函数【def,lambda】才会引入新的作用域
> #其他的代码块：if语句，while语句，for语句，try-except语句都不会引入新的作用域
> ```

#### 4.全局变量和局部变量【掌握】

> 全局变量：将变量定义在函数的外面
>
> 局部变量：将变量定义在函数的内部
>
> 注意：局部变量只能在其被声明的当前函数中使用，而全局变量可以在整个程序中使用
>
> 代码演示：
>
> ```Python
> #全局变量
> total = 0
>
> def show():
>     print(total)
> show()
>
> if True:
>     total = 20
>     print(total)
>
> total = 10
> print(total)
>
> def add(arg1,arg2):
>     #arg1,arg2，total1都属于局部变量
>     total1 = arg1 + arg2
>     print(total1)
>
> add(10,20)
> #print(total1)
> ```

> 作业讲解：
>
> ```Python
> #1.计算1~某个数范围内奇数的和并返回
> def fun1(num):
>     sum = 0
>     for i in range(1,num + 1):
>         if i % 2 == 1:
>             sum += 1
>
>     return sum
>
> print(fun1(100))
>
> #2.判断某个数是否是质数，返回结果
> def fun2(num):
>     is_prime = True
>
>     for x in range(2,num):
>         if num % x == 0:
>             is_prime = False
>             break
>     if is_prime and num != 1:
>         return "质数"
>     else:
>         return "不是质数"
>
> fun2(10)
> ```

#### 5.global和nonlocal关键字的使用【掌握】

> 使用场景：当内部作用域【局部作用域，函数作用域】想要修改全局变量的作用域的时候

1.global

> 代码演示：
>
> ```Python
> #global
>
> #全局变量
> num = 1
> def fun1():
>
>     #此时要使用全局变量中的num，需要给编译器做一个声明，声明此处使用num就是使用的全局变量中的num
>     global num      #global:全球的
>     print(num)
>     print(id(num))   #1355785312
>
>     #局部变量
>     num = 123
>     print(num)
>     print(id(num))   #1355789216
>
> fun1()
>
>
> #练习
> a = 10
> def test():
>     global  a
>     a = a + 1
>     print(a)
>
> test()
> ```

2.nonlocal

> 代码演示：
>
> ```Python
> #前提：nonlocal关键字是定义在闭包中  #nonlocal：非局部的
> x = 0    
>
> def outer():
>     x = 1
>
>     def inner():
>         #使用nonlocal关键字进行声明，相当于将局部作用域范围扩大了
>         nonlocal x
>         x = 2
>         print("inner:",x)
>     #return  inner
>
>     inner()
>
>     print("outer:",x)   #2
>
> outer()
> print("global:",x)
> """
> 原本：
> inner: 2
> outer: 1
> global: 0
> """
>
> """
> 修改：
> inner: 2
> outer: 2
> global: 0
> """
> ```

### 五、列表生成式和生成器【掌握】

#### 1.列表生成式

> list comprehension
>
> 系统内置的用于创建list的方式
>
> range(start,end,step)缺点:生成的列表一般情况下都是等差数列
>
> 代码演示：
>
> ```Python
> #列表生成式
>
> list1 = list(range(1,11))
> print(list1)   #[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>
>
> #需求：[1, 4, 9, 16, 25]
> list2 = []
> for x in range(1,11):
>     list2.append(x ** 2)
> print(list2)  #[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
>
> #1
> #使用列表生成式完成上面的需求
> #列表生成式的格式：[生成的元素 for-in循环]
> list3 = [x ** 2 for x in range(1,11)]
> print(list3)   #[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
>
> #2.
> #[4,16,36,64,100]
> list4 = [x ** 2 for x in range(1,11) if x % 2 == 0]
> print(list4)
>
>
> #3.嵌套for循环，第一个循环就相当于外层循环，第二个循环就相当于内层循环
> list5 = [m + n for m in "ABC" for n in "XYZ"]
> print(list5)
>
> #["AX","AY","AZ"....]
>
> """
> for m in "ABC"：
>     for n in "XYZ"：
>         print(m + n)
>
> """
>
> #4
> #for k,v in dict.items)():
> d = {"x":"1","y":"2","z":"3"}
> for k,v in d.items():
>     print(k,v)
>
> list6 = [k + "=" + v for k,v in d.items()]
> print(list6)   #['x=1', 'y=2', 'z=3']
>
>
> #练习：使用列表生成式生成一个新的列表，将一个已知列表中的所有的字符变为小写
> l1 = ["Hello","GOOD","ABC","kkH"]
> #l2 = ["hello","good","abc","kkh"]
>
> newList1 = []
> for element in l1:
>     str = element.lower()
>     newList1.append(str)
> print(newList1)
>
>
> newList2 = [s.lower() for s in l1]
> print(newList2)
> ```

#### 2.生成器

> generator
>
> next()
>
> 代码演示：
>
> ```Python
> #生成器
>
> #方式一：（），将列表生成式中的[]改成()
> #列表生成式的类型是list，生成器的类型是generator【当做一种新的数据类型】
> r1 = (x ** 2 for x in range(1,6))
> print(r1)   #(1,4,9,16,25)
> print(type(r1))
>
> """
> for i in r1:
>     print(i)
> """
>
> #生成器区别于列表生成式：可以使用next遍历，每调用一次则获取一个元素
> #next()
> print(next(r1))
> print(next(r1))
> print(next(r1))
> print(next(r1))
> print(next(r1))
> #注意：当生成器中的元素全部获取完成之后，接着调用next函数的，则会出现StopIteration
> #print(next(r1))   #StopIteration异常
>
>
> #方式二：yield---->让步
> #(x for x in range(1,6))----->1,2,3,4,5
> def test(n):
>     for i in range(1, n + 1):
>         #执行到yield的时候，则函数会停止，将yiled后面的变量返回
>         yield i ** 2
>         #yield后面的代码的执行时机：当调用next函数的时候
>         print(i)
>
> t = test(5)
> print(t)  #<generator object test at 0x0000019CC432A1A8>
> print(next(t))
> print(next(t))
> print(next(t))
> print(next(t))
> print(next(t))
> ```

