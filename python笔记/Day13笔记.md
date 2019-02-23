### 一、封装【private】

#### 1.概念

> 广义的封装：函数和类的定义本身，就是封装的体现
>
> 狭义的封装：一个类的某些属性，在使用的过程 中，不希望被外界直接访问，而是把这个属性给作为私有的【只有当前类持有】，然后暴露给外界一个访问的方法即可【间接访问属性】
>
> 封装的本质：就是属性私有化的过程
>
> 封装的好处：提高了数据的安全性，提高了数据的复用性
>
> 说明：举例：插排，不需要关心属性在类的内部做了什么样的操作，只需要关心将值传进去，或者将结果获取出来

#### 2.属性私有化

> 如果想让成员变量不被外界直接访问，则可以在属性名称的前面添加两个下划线__,成员变量则被称为私有成员变量
>
> 私有属性的特点：只能在类的内部直接被访问，在外界不能直接访问
>
> 代码演示：
>
> ```Python
> #1.属性不私有化的时候
> class Person():
>     def __init__(self,name,age):
>         self.name = name
>         self.age = age
>
>     def myPrint(self):
>         print(self.name,self.age)
>
> #通过构造函数给属性赋值
> per = Person("张三",10)
> per.myPrint()   #张三 10
> #通过对象直接访问属性，并且给属性赋值
> per.name = "李四"
> per.age = 22
> per.myPrint()   #李四 22
>
> #2.属性私有化
> #写法：在属性的前面添加两个下划线
> #用法：只能在类的内部被访问，外界不能直接访问
> class Person1():
>     def __init__(self,name,age):
>         self.name = name
>         self.__age = age
>
>     def myPrint(self):
>         print(self.name,self.__age)
>
> p1 = Person1("abc",10)
> p1.myPrint()   #abc 10
> p1.name = "hello"
> #其实动态绑定属性，age和__age其实是两个不同的变量
> p1.age = 222
> p1.myPrint()
> print(p1.age)
>
> #AttributeError: 'Person1' object has no attribute '__age',私有化了，在外界不能直接访问
> #print(p1.__age)
> ```

#### 3.get函数和set函数

> get函数和set函数并不是系统的函数，而是自定义的，为了和封装的概念相吻合，起名为getXxx和setXxx
>
> get函数：获取值
>
> set函数：赋值【传值】
>
> 代码演示：
>
> ```Python
> #3.get函数和set函数
> class Person2():
>     def __init__(self,name,age):
>         self.name = name
>         self.__age = age
>         #特殊情况一
>         self.__weight__ = 20.0
>         #特殊情况二
>         self._height = 155.0
>
>     def myPrint(self):
>         print(self.name,self.__age)
>
>     # 书写私有属性age的get函数和set函数【通过自定义的函数进行私有属性的赋值和获取值，暴露给外界】
>     """
>     get函数和set函数并不是系统的函数，而是自定义的，为了和封装的概念相吻合，起名为getXxx和setXxx
>     get函数：获取值
>     set函数：赋值【传值】
>     """
>     #set函数:给成员变量赋值
>     #命名方式：setXxx
>     #特点：需要设置参数，参数和私有成员变量有关
>     def setAge(self,age):
>         #数据的过滤
>         if age < 0:
>             age = 0
>         self.__age = age
>     #get函数：获取成员变量的值
>     #命名方式：getXxx
>     #特点：需要设置返回值，将成员变量的值返回
>     def getAge(self):
>         return self.__age
>
>     #注意：有几个私有属性，则书写几对get函数和set函数
>
> p2 = Person2("abc",10)
> p2.myPrint()   #abc 10
> #print(p2.__age)
> #间接的访问了私有的成员变量
> print(p2.getAge())
> p2.setAge(22)
> print(p2.getAge())
>
> p2.setAge(-20)
> print(p2.getAge())
>
> #总结：通过将属性私有化之后，然后提供get函数和set函数，外部代码就不能随意更改成员变量的值，这样在一定程度上保证了数据的安全性
>
> #4.工作原理【了解】
> #当编译器加载了程序之后，不能直接访问p2.__age,Python解释器把__age解释成_Person2__age
> #p2.__age = 100
> p2._Person2__age = 100
> print(p2.getAge())
>
> #5.特殊情况：尽量不要直接访问
> #a.在一个变量的前后各加两个下划线，在Python中被认为特殊成员变量，将不再属于私有变量
> #print(p2.__weight__)
> #b.特殊变量
> #print(p2._height)
>
> #面试题：下面变量的含义
> """
> xxx:普通的变量
> _xxx:受保护的变量，不建议使用这种形式
> __xxx:表示私有的，外界无法直接访问，只能通过暴露给外界的函数访问
> __xxxx__：一般是系统的内置变量，比如：__name__,__solts__,自定义标识符的时候尽量不要使用这种形式
> """
> ```

#### 4.@property装饰器

> 装饰器的作用：可以给函数动态添加功能，对于类的成员方法，装饰器一样起作用
>
> Python内置的@property装饰器的作用:将一个函数变成属性使用
>
> @property装饰器：简化get函数和set函数
>
> 使用：@property装饰器作用相当于get函数，同时，会生成一个新的装饰器@属性名.settter,相当于set函数的作用
>
> 作用：使用在类中的成员函数中，可以简化代码，同时可以保证对参数做校验
>
> 代码演示：
>
> ```Python
> class Person1():
>     def __init__(self,name,age):
>         self.__name = name
>         self.__age = age
>
>     def myPrint(self):
>         print(self.__name,self.__age)
>
>     """
>    def setAge(self,age):
>         #数据的过滤
>         if age < 0:
>             age = 0
>         self.__age = age
>
>     def getAge(self):
>         return self.__age
>     """
>
>     #注意：函数的命名方式：变量的名称
>     #作用：相当于get函数，设置返回值，将成员变量的值返回
>     @property
>     def age(self):
>         return  self.__age
>
>     #注意：函数的命名方式：需要和@property中函数的命名保持一致
>     #作用：相当于set函数,设置参数，给成员变量赋值
>     @age.setter
>     def age(self,age):
>         if age < 0:
>             age = 0
>         self.__age = age
>
>     @property
>     def name(self):
>         return  self.__name
>
>     @name.setter
>     def name(self,name):
>         self.__name = name
>
>
> p1 = Person1("abc",10)
> p1.myPrint()   #abc 10
> #p1.setAge(20)
> #print(p1.getAge())
>
> print(p1.age)  #10
> p1.age = 18   #相当于调用了set函数，将18传值，实质调用的是@age.setter修饰的函数
> print(p1.age) #相当于调用了get函数，将成员变量的值获取出来，实质调用的是@peoperty修饰的函数
>
> p1.name = "zhangsan"
> print(p1.name)
> ```

#### 5.私有方法

> 如果类中的一个函数名前面添加__,则认为这个成员函数时私有化的
>
> 特点：也不能在外界直接调用，只能在类的内类调用
>
> 代码演示：
>
> ```Python
> class Site():
>     def __init__(self,name):
>         self.name = name
>
>     def who(self):
>         print(self.name)
>         self.__foo()
>
>     #私有成员方法，只能在当前类的内部内调用
>     def __foo(self):    #私有函数
>         print("foo")
>
>     def foo(self):    #公开函数
>         print("foo~~~~")
>
>     #注意：以上两个函数是两个不同的函数，不存在覆盖的问题
>
> s = Site("千锋")
> s.who()
> #s.__foo()  #AttributeError: 'Site' object has no attribute 'foo'
> s.foo()
> ```

### 二、继承【extends】

#### 1.概念

> 如果两个或者两个以上的类具有相同的属性或者成员方法，我们可以抽取一个类出来，在抽取的类中声明公共的部分
>
> ​	被抽取出来的类：父类，基类，超类，根类
>
> ​	两个或者两个以上的类：子类，派生类
>
> ​	他们之间的关系：子类  继承自  父类
>
> 注意：
>
> ​	a.object是所有类的父类，如果一个类没有显式指明它的父类，则默认为object
>
> ​	b.简化代码，提高代码的复用性

#### 2.单继承

##### 2.1使用

> 简单来说，一个子类只能有一个父类，被称为单继承
>
> 语法：
>
> 父类：
>
> class 父类类名(object):
>
> ​	类体【所有子类公共的部分】
>
> 子类：
>
> class 子类类名（父类类名）:
>
> ​	类体【子类特有的属性和成员方法】
>
> 说明：一般情况下，如果一个类没有显式的指明父类，则统统书写为object
>
> 代码演示：
>
> person.py文件【父类】
>
> ```Python
> #1.定义父类
> class Person(object):
>     #构造函数【成员变量】
>     def __init__(self,name,age):
>         self.name = name
>         self.age = age
>
>
>     #成员方法
>     def show(self):
>         print("show")
>
>     def __fun(self):
>         print("fun")
> ```
>
> worker.py文件【子类1】
>
> ```Python
> from  extends01.person import Person
>
> #2.定义子类
> class Worker(Person):
>     #构造函数【成员变量】
>     def __init__(self,name,age,job):
>         """
>         self.name = name
>         self.age = age
>         """
>         self.job = job
>
>         #6.在子类的构造函数中调用父类的构造函数【从父类中继承父类中的成员变量】
>         #方式一：super(当前子类，self).__init__(属性列表)
>         #super(Worker, self).__init__(name,age)
>         #方式二：父类名.__init__(self,属性列表)
>         Person.__init__(self,name,age)
>         #方式三：super().__init__(属性列表)
>         #super().__init__(name,age)
>
>
>     #成员方法
>     def work(self):
>         print("work")
> ```
>
> student.py文件【子类2】
>
> ```Python
> from extends01.person import  Person
>
> class Student(Person):
>     # 构造函数【成员变量】
>     def __init__(self, name, age, score):
>
>         Person.__init__(self,name,age)
>         self.score = score
>
>     # 成员方法
>     def study(self):
>         print("study")
> ```
>
> extendsDemo01.py文件【测试模块】
>
> ```Python
> #测试模块
> from extends01.person import Person
> from extends01.worker import Worker
> from extends01.student import Student
>
> #3.创建父类的对象
> p = Person("zhangsan",10)
> p.show()
> #p.__fun()
>
> #4.创建子类的对象
> w = Worker("aaa",20,"工人")
> w.work()
>
> #5.子类对象访问父类中的内容
> #结论一：子类对象可以调用父类中的公开的成员方法【因为继承，私有方法除外】
> w.show()
> #w.__fun()
> #结论二：通过在子类的构造函数中调用父类的构造函数，子类对象可以直接访问父类中的成员变量【私有变量除外】
> print(w.name,w.age,w.job)
>
> s = Student("小明",9,90)
> s.study()
> s.show()
> ```

##### 2.2特殊用法

> 代码演示：
>
> ```Python
> #6.子类中出现一个和父类同名的成员函数,则优先调用子类中的成员函数
> #子类的成员函数覆盖了父类中的同名的成员函数
> s = Student("小明",9,90)
> s.study()
> s.show()
>
> #7.父类对象能不能访问子类中特有的成员函数和成员变量？----->不能
> per = Person("gs",10)
> #per.work()
> ```
>
> ```Python
> #8.slots属性能否应用在子类中
> #结论三：在父类中定义slots属性限制属性的定义，子类中是无法使用，除非在子类中添加自己的限制
> #父类
> class Student(object):
>     __slots__ = ("name","age")
>
> #子类
> class SeniorStudent(Student):
>     pass
>
>
> s  = Student()
> s.name = "zhangsan"
> s.age = 10
> #s.score = 90
>
> ss = SeniorStudent()
> ss.name = "lisi"
> ss.age = 20
> ss.score = 60
> ```

> 总结：
>
> 继承的特点：
>
> ​	a.子类对象可以直接访问父类中非私有化的属性
>
> ​	b.子类对象可以调用父类中非私有化的成员方法
>
> ​	c.父类对象不能访问或者调用子类 中任意的内容
>
> 继承的优缺点：
>
> 优点：
>
> ​	a.简化代码，减少代码的冗余
>
> ​	b.提高代码的复用性
>
> ​	c.提高了代码的可维护性
>
> ​	d.继承是多态的前提
>
> 缺点：
>
> ​	通常使用耦合性来描述类与类之间的关系，耦合性越低，则说明代码的质量越高
>
> ​	但是，在继承关系中，耦合性相对较高【如果修改父类，则子类也会随着发生改变】

#### 3.多继承

> 一个子类可以有多个父类
>
> 语法：
>
> class 子类类名(父类1，父类2，父类3.。。。)：
>
> ​	类体
>
> 代码演示：
>
> father.py文件【父类1】
>
> ```Python
> class Father(object):
>     def __init__(self,money):
>         self.money = money
>
>     def play(self):
>         print("playing")
>
>     def fun(self):
>         print("father中的fun")
> ```
>
> mother.py文件【父类2】
>
> ```Python
> class Mother(object):
>     def __init__(self,faceValue):
>         self.faceValue = faceValue
>
>     def eat(self):
>         print("eating")
>
>     def fun(self):
>         print("mother中的fun")
> ```
>
> child.py文件【子类】
>
> ```Python
> from extends02.father import Father
> from extends02.mother import Mother
>
> #定义子类，有多个父类
> class Child(Mother,Father):
>     def __init__(self,money,faceValue,hobby):
>         #调用父类中的构造函数
>         Father.__init__(self,money)
>         Mother.__init__(self,faceValue)
>         self.hobby = hobby
>
>     def study(self):
>         print("study")
> ```
>
> extendsDemo03.py文件【测试模块】
>
> ```Python
> from extends02.father import Father
> from extends02.mother import Mother
> from extends02.child import Child
>
>
> f = Father(100000)
> m = Mother(3.0)
>
> #创建子类对象
> c = Child(1000,3.0,"打游戏")
> #子类对象调用父类中的成员方法
> c.play()
> c.eat()
>
> #结论;如果多个父类中有相同的函数，通过子类的对象调用，调用的是哪个父类中的函数取决于在父类列表中出现的先后顺序
> c.fun()
> ```

#### 4.函数重写【override】

> 在子类中出现和父类同名的函数，则认为该函数是对父类中函数的重写

##### 4.1系统函数重写

> ```
> __str__   
> __repr__
> ```
>
> 代码演示：
>
> ```Python
> class Animal(object):
>     def __init__(self,name,age):
>         self.name = name
>         self.age = age
>
>     #重写__str__函数,重写之后一般return一个字符串，有关于成员变量
>     def __str__(self):
>         return "name=%s age=%d"%(self.name,self.age)
>
>     #重写__repr__,作用和str是相同的，优先使用str
>     def __repr__(self):
>         return "name=%s age=%d"%(self.name,self.age)
>
> a = Animal("大黄",10)
> print(a)   #<__main__.Animal object at 0x00000226A87AC240>
> print(a.__str__())
>
> #当一个类继承自object的时候，打印对象获取的是对象的地址，等同于通过子类对象调用父类中__str__
> #当打印对象的时候，默认调用了__str__函数
> #重写__str__的作用：为了调试程序
>
> """
> 总结：【面试题】
> a.__str__和__repr__都未被重写的时候，使用对象调用的是__str__,此时__str__返回的是对象的地址
> b.__str__和__repr__都被重写之后，使用对象调用的是__str__，此时__str__返回的是自定义的字符串
> c.重写了__str__，但是没有重写__repr__，则使用对象调用的是__str__，此时__str__返回的是自定义的字符串
> d.未重写__str__，但是重写了__repr__，则使用对象调用的是__repr__,此时，__repr__返回的是自定义的字符串
> """
>
> #使用时机：当一个对象的属性有很多的时候，并且都需要打印，则可以重写__str__，可以简化代码，调试程序
> ```

##### 4.2自定义函数重写

> 代码演示：
>
> ```Python
> #函数重写的时机：在继承关系中，如果父类中函数的功能满足不了子类的需求，则在子类中需要重写
> #父类
> class People(object):
>     def __init__(self,name):
>         self.name = name
>
>     def fun(self):
>         print("fun")
>
> #子类
> class Student(People):
>     def __init__(self,name,score):
>         self.score = score
>         super(Student,self).__init__(name)
>
>     #重写;将函数的声明和实现重新写一遍
>     def fun(self):
>         #在子类函数中调用父类中的函数【1.想使用父类中的功能，2.需要添加新的功能】
>         #根据具体的需求决定需不需要调用父类中的函数
>         super(Student,self).fun()
>         print("fajfhak")
>
>
> s = Student("fhafh",10)
> s.fun()
> ```