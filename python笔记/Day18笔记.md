### 一、高阶函数【掌握】

#### 1.map()

> 代码演示：
>
> ```Python
> """
> map(function,iterable)
> function:函数
> iterable：可迭代对象
> 作用：将传入的函数依次作用于可迭代对象中的每一个元素，并把结果【Iterator】返回
> """
> #需求1：给一个已知列表中的元素求平方
> def square(x):
>     return x ** 2
> list1 = [1,2,3,4,5]
> result1 = map(square,list1)
> #注意:map是一个类，表示一种数据类型，集合或者序列，使用类似于list，tuple，set
> print(result1)   #<map object at 0x000001EE25431DA0>
> print(type(result1))   #<class 'map'>
> print(list(result1))  #[1, 4, 9, 16, 25]
>
> result2 = map(lambda x:x ** 2,list1)
> print(list(result2))
>
> #str = 10
>
> #需求2：将整型元素的列表转换为字符串元素的列表
> #举例：[1,2,3,4]------>["1","2","3","4"]
> #str(1) ---- >字符串1
> #注意：在使用系统函数之前，最好不要出现同名的变量
> result3 = map(str,[1,2,3,4])
> print(list(result3))
>
>
> #需求3：已知两个整型列表，将两个列表中相同位置的元素相加，得到一个新的列表
> def add(x,y):
>     return  x  + y
> l1 = [1,2,3,4,5]
> l2 = [6,7,8,9,10]
>
> result4 = map(add,l1,l2)
> print(list(result4))
> ```

#### 2.reduce()

> 代码演示：
>
> ```Python
> from  functools  import  reduce
>
> """
> reduce(function,Iterable)  :通过函数对参数列表中的元素进行累积
> function:函数
> Iterable：可迭代对象，一般使用列表
> 工作原理：用传给reduce的function先作用于list中第一个和第二个元素，用得到的结果和list中第三个元素计算。。。
> reduce(add,[a,b,c,d])
> add(add(add(a,b),c),d)---->递归
> """
>
> #需求1;求一个已知列表中元素的和
> list1 = [1,2,3,4,5]
> def add(x,y):
>     return x + y
> result1 = reduce(add,list1)
> print(result1)
>
> result2 = reduce(lambda x,y:x + y,list1)
> print(result2)
>
> #需求2：将列表[1,3,5,7,9]变换成整数13579
> """
> 分析：
> 13 = 1 * 10 + 3
> 135 = 13 * 10 + 5
> 1357 = 135 * 10 + 7
> 13579 = 1357 * 10 + 9
> """
> list2 = [1,3,5,7,9]
> def fn(x,y):
>     return x * 10 + y
>
> result3 = reduce(fn,list2)
> print(result3)
>
> #需求3：
> #结合map函数，实现一个将str转换为int的函数   int()
>
> #思路：传进来一个字符串，返回一个对应的整数
> def strToInt(s):
>     digits = {"0":0,"1":1,"2":2,"3":3,"4":4}
>     return digits[s]
>
> #"23401"------>23401
> r0 = map(strToInt,"23401")
> print(list(r0))   #[2, 3, 4, 0, 1]
>
> r1 = reduce(fn,map(strToInt,"23401"))
> print(r1)   #23401
> print(type(r1))   #<class 'int'>
> ```

#### 3.filter()

> 代码演示：
>
> ```Python
> """
> filter(function,序列)
> 作用：通过指定的条件过滤列表中的元素
> 工作原理：将传入的函数依次作用于列表中的每一个元素，根据返回的是True还是False决定元素是否需要保留
> """
>
> #需求1：将列表中的偶数筛选出来
> list1 = [1,2,3,4,5,6,7,8,9]
> #作用：定义筛选的规则
> def func(num):
>     if num % 2 == 0:
>         return  True
>     return  False
>
> result1  = filter(func,list1)
> print(result1)
> print(list(result1))  #[2, 4, 6, 8]
> ```

#### 4.sorted()

> 代码演示：
>
> ```Python
> #1.普通排序
> #默认为升序排序，得到了的一个新的列表
> list1 = [4,5,23,3,5,7]
> result1 = sorted(list1)
> print(list1)
> print(result1)  #r[3, 4, 5, 5, 7, 23]
>
> #2.按照绝对值进行排序
> #默认为升序排序，排序的依据是所有元素的绝对值的大小
> list2 = [4,5,-23,3,-5,7]
> result2 = sorted(list2,key=abs)
> print(result2)  #[3, 4, 5, -5, 7, -23]
>
> #3.降序升序
> list3 = [4,5,23,3,5,7]
> result3 = sorted(list3,reverse=True)
> print(result3)
>
> #4.字符也可以实现排序
> list4 = ["f","a","k","z"]
> result4 = sorted(list4)
> print(result4)
>
> #5.自定义排序规则
> #默认为升序排序
> def myFunc(str):
>     return len(str)
> list5 = ["gsg","a","34535","efgg","562875678257fhjawhgj"]
> result5 = sorted(list5,key=myFunc)
> print(result5)
> ```

## 二、虚拟环境【掌握】

#### 1, virtualenv的概述

```Python
virtualenv是用来创建Python的虚拟环境的库，虚拟环境能够独立于真实环境存在，
	并且可以同时有多个互相独立的Python虚拟环境，每个虚拟环境都可以营造一个干净
	的开发环境，对于项目的依赖、版本的控制有着非常重要的作用。

虚拟环境有什么意义？
	如果我们要同时开发多个应用程序，应用A需要Django1.11，而应用B需要Django1.8怎么办？
	这种情况下，每个应用可能需要各自拥有一套“独立”的Python运行环境。
	virtualenv就是用来为一个应用创建一套“隔离”的Python运行环境。
```

#### 2, virtualenv 的安装和使用

```Python
1.安装和创建virtualenv
	a,安装虚拟环境：安装virtualenv跟安装一般的Python库是一样的操作，直接使用pip命令就行了：
		pip install virtualenv
	b,创建虚拟环境：安装完成之后就可以使用virtualenv的命令来创建虚拟环境了，
		  首先需要进入需要创建虚拟环境的文件夹，比如F盘的envs文件夹，
		  然后使用以下命令创建一个虚拟环境，python版本的路径是可选的：
			virtualenv 虚拟环境名称 [-p python版本的路径]
			如：virtualenv env1 
2,启动虚拟环境:
		env1\Scripts\activate
	进入虚拟环境后：
		使用pip安装numpy模块
		创建test.py文件,并在文件中使用numpy模块
		在cmd命令窗口使用python test.py执行文件
			
3,退出虚拟环境(进入真实系统环境): 
		deactivate  
		(如果报错则使用:env1\Scripts\deactivate)
	退出虚拟环境后再执行test.py：
		在cmd命令窗口使用python test.py执行文件

```

#### 3, virtualenvwrapper 的安装和使用 

##### virtualenvwrapper是virtualenv的包装版，以后用这个，更加方便

```Python
Windows: pip install virtualenvwrapper-win
(Linux：pip install virtualenvwrapper)

创建:mkvirtualenv    虚拟环境名称  -p  python的路径 
删除:rmvirtualenv    虚拟环境名称
(注意：创建的虚拟环境放在用户目录下的Envs中)

进入:workon 虚拟环境名称
退出:deactivate 
```

#### 4, pip常用命令

```Python
pip install xxx:安装xxx依赖包
pip uninstall xxx ：卸载xxx包
pip list:查看所有依赖包
pip freeze:查看虚拟环境新安装的包

```




