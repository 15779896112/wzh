### 一、迭代器【掌握】

#### 1.可迭代对象

> 可迭代对象【实体】：可以直接作用于for循环的实体【Iterable】
>
> 可以直接作用于for循环的数据类型：
>
> ​	a.list,tuple,dict,set,string	
>
> ​	b.generator【() 和yield】
>
> isinstance:判断一个实体是否是可迭代的对象	
>
> 代码演示：
>
> ```Python
> #一、可迭代对象
>
> #1.导入
> from  collections  import  Iterable
>
> #2.使用isinstance(数据，Iterable)
> print(isinstance([],Iterable))
> print(isinstance((),Iterable))
> print(isinstance({},Iterable))
> print(isinstance((x for x in range(10)),Iterable))
> print(isinstance("hello",Iterable))
>
> print(isinstance(10,Iterable))   #False
> print(isinstance(True,Iterable))  #False
>
> print("****88")
> ```

#### 2.迭代器

> 不但可以作用于for循环，还可以被next函数遍历【不断调用并返回一个元素，直到最后一个元素被遍历完成，则出现StopIteration】
>
> 目前为止，只有生成器才是迭代器【Iterator】
>
> 结论：迭代器肯定是可迭代对象，但是，可迭代对象不一定是迭代器
>
> isinstance:判断一个实体是否是迭代器
>
> 代码演示：
>
> ```Python
> #二、迭代器
> from  collections  import  Iterator
>
> print(isinstance([],Iterator))
> print(isinstance((),Iterator))
> print(isinstance({},Iterator))
> print(isinstance("hello",Iterator))
> print(isinstance((x for x in range(10)),Iterator))   #True
>
> print("****88")
> ```

#### 3.可迭代对象和迭代器之间的转换

> 可以将可迭代对象转换为迭代器：iter()
>
> 代码演示：
>
> ```Python
> #三、虽然list、tuple、dict、set、string都不是迭代器
> #iter():将list、tuple、dict、set、string的  Iterable转换为Iterator
> print(isinstance(iter([]),Iterator))
> print(isinstance(iter(()),Iterator))
> print(isinstance(iter({}),Iterator))
> print(isinstance(iter("hello"),Iterator))
> ```
>
> 总结：
>
> ​	a.凡是可以作用于for循环的对象都是Iterable类型
>
> ​	b.凡是可以作用于next函数的对象都是Iterator类型
>
> ​	c.list/tuple/dict/set/string都不是Iterator，可以通过iter()获得一个Iterator对象
>
> 【面试题】
>
> 区分可迭代对象和迭代器

### 三、装饰器【掌握】

#### 1.案例

> 代码演示：
>
> ```Python
> def test():
>     print("拼搏到无能为力，坚持到感动自己")
>
>
> f = test()  #变量可以指向指向函数，函数名也是一个变量，所以变量可以当做函数调用
> f()
>
>
> #思考问题：test增加功能，但是不能修改test函数内部----->装饰器
> ```
>
> 在代码运行期间，可以动态增加函数功能的方式，被称为装饰器【Decorator】
>
> 也就是说，在不修改原函数的基础上，给原函数增加功能
>
> 好处：在团队开发中，如果两个或者两个以上的程序员会用到相同的功能，但是功能又有细微的差别，采用装饰器：相互不影响，代码简化

#### 2.使用

##### 2.1简单装饰器

> 代码演示：
>
> ```Python
> #1.简单的装饰器
> def test():
>     print("拼搏到无能为力，坚持到感动自己")
>
> #a.书写闭包
> #b.给外部函数设置参数,fun表示的是原函数
> def outer(fun):
>     def inner():
>         # d.给原函数增加功能
>         print("hello")
>
>         #c.调用原函数
>         fun()
>
>     return inner
>
> #e.使用闭包
> f = outer(test)   #f = inner
> f()   #inner()
>
> #注意：增加的功能可以写在原函数调用的前面或者后面
> #注意：outer函数就被称为装饰器
>
>
> #练习：给下面的函数添加功能，打印九九乘法表
> def show():
>     for i in range(10):
>         print(i)
>
> def outer1(fun):
>     def inner1():
>         fun()
>         for i in range(1,10):
>             for j in range(1,i + 1):
>                 print("%dx%d=%d"%(j,i,i * j),end=" ")
>             print("")
>     return  inner1
>
> f1 = outer1(show)
> f1()
> ```

##### 2.2有参数的装饰器

> 代码演示：
>
> ```Python
> #2.原函数有参数的装饰器
> def getAge(age):
>     print(age)
>
> getAge(10)
> getAge(-5)
>
> print("************")
>
> #需求：在不修改原函数的基础上，进行数据的过滤：当用户输入age为负数的时候，则置为0
> def wrapper(fun):
>     #注意：当原函数有参数，装饰器的作用是为了操作原函数中的参数，给inner设置参数
>     def inner(num):
>         #增加新功能：过滤负数
>         if num < 0:
>             num = 0
>
>         #调用原函数
>         fun(num)  #age = num
>     return  inner
>
> f = wrapper(getAge)
> f(10)   #num = 10
> f(-5)
> ```

##### 2.3系统的简写

> 代码演示：
>
> ```Python
> #3.简化demo2中的操作：@装饰器的名称  应用到原函数中
>
> #需求：在不修改原函数的基础上，进行数据的过滤：当用户输入age为负数的时候，则置为0
> def wrapper(fun):
>     #注意：当原函数有参数，装饰器的作用是为了操作原函数中的参数，给inner设置参数
>     def inner(num):
>         #增加新功能：过滤负数
>         if num < 0:
>             num = 0
>
>         #调用原函数
>         fun(num)  #age = num
>     return  inner
>
> #将wrapper装饰器应用在了getAge函数上，
> @wrapper
> def getAge(age):
>     print(age)
>
> getAge(10)
> getAge(-5)
>
> """
> @wrapper
>
> 等价于
>
> f = wrapper(getAge)
> f(10)   #num = 10
>
> #注意;当使用@的时候，在同一个文件中，装饰器必须出现的原函数的前面
>
> """
> ```

##### 2.4不定长参数的装饰器

> 代码演示：
>
> ```Python
> #4.不定长参数的装饰器
>
> #应用场景：当同一个装饰器作用于不同函数的时候，这些函数的参数的个数是不相同的
> def wrapper(fun):
>     def inner(*args):
>         print("hello")
>
>         fun(*args)   #a = args[0]   b = args[1]
>
>     return  inner
>
> @wrapper
> def fun1(a,b):
>     print(a + b)
>
> @wrapper
> def fun2(a,b,c,d):
>     print(a,b,c,d)
>
> fun1(10,20)   #args = (10,20)
> fun2(1,2,3,4)
> ```

##### 2.5多个装饰器作用于同一个函数 

> 代码演示：
>
> ```Python
> #5.将多个装饰器应用到同一个函数上
> def wrapper1(fun):
>     def inner1():
>         print("1~~~~")
>         fun()
>
>     return inner1
>
> def wrapper2(fun):
>     def inner2():
>         print("2~~~~")
>         fun()
>
>     return inner2
>
> @wrapper1
> @wrapper2
> def show():
>     print("hello")
>
> show()
>
> """
> 1~~~~
> 2~~~~
> hello
> """
>
> #结论：多个装饰器作用于同一个函数的时候，从第一个装饰器开始，从上往下依次执行，但是，原函数只会被执行一次
> ```

### 四、函数递归【掌握】

#### 1.概念

> 递归函数：一个会调用自身的函数【在一个函数的内部，自己调用自己】
>
> 递归调用
>
> 递归中包含了一种隐式的循环，他会重复指定某段代码【函数体】，但这种循环不需要条件控制
>
> 使用递归解决问题思路：
>
> ​	a.找到一个临界条件【临界值】
>
> ​	b.找到相邻两次循环之间的关系
>
> ​	c.一般情况下，会找到一个规律【公式】

#### 2.使用

> 代码演示：
>
> ```Python
> #案例一
> """
>                1 2 3 4 5 6 7  8  9 10  11.。。。
> 斐波那契数列：1,1,2,3,5,8,13,21,34,55,89.....
>
> 解决问题：报一个数，输出数列中对应的数
>
> 规律：
> a.第一个位置和第二个位置上数是固定的，都是1
> b.第n个位置上的数：第 n - 1 的数  +   第 n - 2 的数
>
> r1 = func1(1)  ------>1
> r2 = func1(2)  ------>1
> r3 = fun1(3) ------>func1(1) + func1(2)----->1 + 1 = 2
> r4 = fun1(4)------->fun1(3) + fun1(2) ----->func1(1) + func1(2) +  fun1(2) ---->1  + 1 + 1 = 3
> r5 = fun1(5) ----->fun1(4) + fun1(3) ----->fun1(3) + fun1(2) + func1(1) + func1(2)--->func1(1) + func1(2) ++ fun1(2) + func1(1) + func1(2)--->5
> .....
> rn = fun1(n) ----->fun1(n- 1) + fun1(n - 2)
> """
>
> def func1(num):
>     #临界值
>     if num == 1 or num == 2:
>         return 1
>     else:
>         #print("~~~~",num)
>         result = func1(num- 1) + func1(num - 2)    #result = func1(1) + func1(2)  --->1 + 1 =2
>         return result
>
> print(func1(10))
>
> #练习;使用递归计算1~某个数之间的和
> """
> add(1) = 1   :临界值
> add(2) = add(1) + 2
> add(3) = add(2) + 3 ---->add(1) + 2 + 3 = 1 + 2 + 3
> add(4) = add(3) + 4---->add(2) + 3 + 4 ---->add(1) + 2 + 3 + 4---->1 + 2 + 3 + 4
> ....
> add(n) = add(n - 1) + n
> """
> def add(num):
>
>     """
>     n = 1
>     sum = 0
>     while n <= 100:
>         sum += n
>         n += 1
>
>     return sum
>
>     sum1 = 0
>     for i in range(1,num + 1):
>         sum1 += i
>     return  sum1
>     """
>     #使用递归实现
>     if num == 1:
>         return 1
>     else:
>         return add(num - 1) + num
>
> print(add(100))
> ```
>
> 注意：以后在实际项目中尽量少用递归，如果隐式循环的次数太多，会导致内存泄漏【栈溢出】
>
> 优点：简化代码，逻辑清晰

### 五、栈和队列【了解】

> 用于存储数据的线性表
>
> 栈：在表的一端进行插入和删除
>
> 队列：在表的一端进行插入，在表的另一端进行数据的删除

#### 1.栈

> Stack
>
> 开口向上的容器：先进后出，后进先出
>
> 代码演示：
>
> ```Python
> #list的底层维护了一个栈的线性表
>
> myStack = []
>
> #插入数据
> #数据入栈【压栈】
> myStack.append(1)
> print(myStack)
> myStack.append(2)
> print(myStack)
> myStack.append(3)
> print(myStack)
> myStack.append(4)
> print(myStack)   #[1,2,3,4]
>
> #出栈
> myStack.pop()
> print(myStack)
> myStack.pop()
> print(myStack)
> myStack.pop()
> print(myStack)
> myStack.pop()
> print(myStack)
> ```

#### 2.队列

> queue
>
> 水平放置的水管：先进先出，后进后出
>
> 代码演示：
>
> ```Python
> import  collections   #数据结构的集合
>
> queue  = collections.deque([1,2,3,4])
> print(queue)
>
> #入队【存储数据】
> queue.append(5)
> print(queue)
> queue.append(6)
> print(queue)
>
> #出队【获取数据】
> queue.popleft()
> print(queue)
> queue.popleft()
> print(queue)
> queue.popleft()
> print(queue)
> ```
