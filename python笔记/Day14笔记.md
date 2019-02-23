### 一、多态

#### 1.概念

> 一种事物的多种体现形式，函数的重写其实就是多态的一种体现
>
> 在Python中，多态指的是父类的引用指向子类的对象
>
> 代码演示：
>
> ```Python
> #父类
> class Animal(object):
>     pass
>
> #子类
> class Dog(Animal):
>     pass
>
> class Cat(Animal):
>     pass
>
> #定义变量
> a = []   #a是list类型
> b = Animal()  #b是Animal类型
> c = Cat()  #c是Cat类型
>
> #isinstance():判断一个对象是否属于某种类型【系统还是自定义的类型】
> print(isinstance(a,list))
> print(isinstance(b,Animal))
> print(isinstance(c,Cat))
>
> print(isinstance(c,Animal))  #True
>
> print(isinstance(b,Dog))   #False
>
> #结论：子类对象可以是父类类型，但是，父类的对象不能是子类类型
> ```

#### 2.使用

> 案例：人可以喂猫，喂狗
>
> 思路：
>
> a.定义动物类【父类】
>
> b.定义子类，继承自动物类
>
> c.定义人类
>
> d.使用多态，优化
>
> 代码演示：
>
> duoTaiDemo.py文件
>
> ```Python
> from duotai.person import Person
> from duotai.cat import Cat
> from duotai.dog import Dog
>
> #1.创建一个Person的对象
> p = Person()
>
> #2.创建一个Cat的对象
> c = Cat("小白")
>
> #3.人执行自己的行为
> p.feedAnimal(c)
>
> d = Dog("旺财")
> p.feedAnimal(d)
> ```
>
> person.py文件
>
> ```Python
> class Person(object):
>     """
>     def feedCat(self,cat):
>         print("喂猫:",cat.name)
>         cat.eat()
>     def feedDog(self,dog):
>         print("喂猫:",dog.name)
>         dog.eat()
>     """
>     #多态
>     #ani被当做父类的引用 ，当传参的时候，实参是一个子类对象的时候，则体现出了 多态的应用
>     def feedAnimal(self,ani):   #ani = c   c = Cat("")
>         print("喂动物:", ani.name)
>         ani.eat()
> ```
>
> animal.py文件
>
> ```Python
> class Animal(object):
>     def __init__(self,name):
>         self.name = name
>
>     def eat(self):
>         print("eating")
> ```
>
> cat.py文件
>
> ```Python
> from duotai.animal import Animal
>
> class Cat(Animal):
>     def __init__(self,name):
>         super(Cat,self).__init__(name)
> ```
>
> dog.py文件
>
> ```Python
> from duotai.animal import Animal
>
> class Dog(Animal):
>     def __init__(self,name):
>         super(Dog,self).__init__(name)
> ```
>
> 总结：
>
> ​	简化代码，提高代码的可读性，可维护性

### 二、获取对象信息

> type()   isintance()     dir()
>
> 代码演示：
>
> ```Python
> #1.type() :判断一个对象所属的类型
> num = 10
> print(type(num))
> print(type("hello"))
>
> class Check(object):
>     pass
> c = Check()
> print(type(c))
>
> #使用==判断type返回的结果
> print(type(12) == type(57))  #True
> print(type(12) == type("57"))  #False
>
> #使用type返回的结果和数据类型直接判断
> print(type(12) == int)
>
> #2.isintance()  :判断一个对象是否属于某种指定的数据类型
> #自定义的类中
> class Dog(object):
>     pass
>
> d = Dog()
> print(isinstance(d,Dog))
> print(isinstance([1,2,4],list))
>
> #特殊用法：可以判断一个对象是否属于多种数据类型中的某一种
> print(isinstance([1,2,4],(tuple,list)))
>
> #3.dir()  :列出指定对象中所包含的所有的内容【成员变量，成员方法】
> dict = {}
> print(dir(dict))
>
> print(dir("abc"))
>
> print(dir(d))
> ```

### 三、类中特殊的属性和方法

#### 1.实例属性和类属性

##### 1.1实例属性和类属性的区别【面试题】

> a.定义的位置不同，类属性时直接定义在类中，实例属性定义在构造函数中
>
> b.访问的方式不同，类属性使用类名直接访问，实例属性使用对象访问
>
> c.在内存中出现的时机不同，类属性随着类的出现而出现，实例属性随着对象的出现而出现
>
> d.优先级不同，实例属性的优先级高于类属性
>
> 代码演示：
>
> ```Python
> class Person(object):
>     #1.定义位置
>     #类属性：直接定义在类中
>     name = "abc"
>     age = 0
>
>     def __init__(self,name):
>         #实例属性：定义在构造函数中
>         self.name = name
>
>
> #2.访问方式
> print(Person.name)  #类属性：类名.属性 或者 对象.属性
>
> p = Person("hello")
> print(p.name)   #实例属性：对象.属性
>
> #3.优先级不同：实例属性的优先级高于类属性
> print(p.name)   #hello
>
> #4.不同对象的类属性在内存中是不是同一块空间？----->不是
> p1 = Person("小白")
> p2 = Person("小红")
> print(p1.age)
> print(p2.age)
> p1.age = 33
> print(p1.age)
> print(p2.age)
> print(id(p1.age))
> print(id(p2.age))
> """
> 0
> 0
> 33
> 0
> 1420404832
> 1420403776
> """
>
> #注意：尽量避免类属性和实例属性的重名
>
> #删除属性【类属性，实例属性】
> del p1.age
> ```

##### 1.2动态添加属性和方法

> 代码演示：
>
> ```Python
> from  types import MethodType
>
>
> class Person(object):
>     #__slots__ = ("name","age")
>     pass
>
>
> #1.动态添加属性
> per = Person()
> str = "fjsgh"
> per.name = str
>
> #2.动态添加方法
> def say(self):
>     print("fhsj")
> """
> per.test = say
> per.test(per)
> """
>
> #弊端：违背了普通函数定义
> #解决方案：MethodType类，存在于types模块下
>
> #类似于偏函数
> #参数：函数名，对象
> #作用：在现有函数的基础上生成了一个对象【新的函数】，赋值给成员变量，则认为给对象添加了一个成员方法
> per.test = MethodType(say,per)
> per.test()
> ```

#### 2.类方法和静态方法

> 类方法：使用@classmethod装饰器修饰的方法，被称为类方法，可以通过类名调用，也可以通过对象调用，但是一般情况下使用类名调用
>
> 静态方法：使用@staticmethod装饰器修饰的方法，被称为静态方法，可以通过类名调用，也可以通过对象调用，但是一般情况下使用类名调用
>
> 代码演示：
>
> ```Python
> class Test(object):
>     #1.类属性
>     age = 100
>
>     def __init__(self,name):
>         #2.实例属性
>         self.name = name
>
>     #3.成员方法,通过对象调用
>     #必须有一个参数，这个参数一般情况下为self，self代表是当前对象
>     def func(self):
>         print("func")
>
>     #4.类方法
>     """
>     a.必须有一个参数，这个参数一般情况下为cls，cls代表的是当前类
>     b.类方法是属于整个类的，并不是属于某个具体的对象，在类方法中禁止出现self
>     c.在类方法的内部，可以直接通过cls调用当前类中的属性和方法
>     d.在类方法的内部，可以通过cls创建对象
>     """
>     @classmethod
>     def test(cls):
>         print("类方法")
>         print(cls)   #<class 'methodDemo01.Test'>
>         print(cls.age)
>
>         #6
>         #注意：cls完全当做当前类使用
>         c = cls("hello")
>         c.func()
>
>     #7.静态方法
>     @staticmethod
>     def show():
>         print("静态方法")
>
> t = Test("hjfsh")
> t.func()
>
> #5,.调用类方法
> Test.test()   #类名.类方法的名称()
> t.test()       #对象.类方法的名称()
>
> #7。调用静态方法
> Test.show()
> t.show()
> ```
>
> 总结：实例方法【成员方法】、类方法以及静态方法之间的区别
>
> a.语法上
>
> ​	实例方法：第一个参数一般为self，在调用的时候不需要传参，代表的是当前对象【实例】
>
> ​	静态方法：没有特殊要求
>
> ​	类方法：第一个参数必须为cls，代表的是当前类
>
> b.在调用上
>
> ​	实例方法：只能对象
>
> ​	静态方法：对象  或者 类
>
> ​	类方法：对象 或者 类
>
> c.在继承上【相同点】
>
> ​	实例方法、静态方法、类方法：当子类中出现和父类中重名的函数的时候，子类对象调用的是子类中的方法【重写】
>
> 代码演示：
>
> ```Python
> class SuperClass(object):
>     @staticmethod
>     def show():
>         print("父类中的静态方法")
>
>     @classmethod
>     def check(cls):
>         print("父类中的类方法")
>
> class SubClass(SuperClass):
>     pass
>
> s = SubClass()
> s.show()
> s.check()
> ```
>
> 注意：注意区分三种函数的书写形式，在使用，没有绝对的区分	

#### 3.类常用属性

> ```
> __name__
> 	通过类名访问，获取类名字符串
> 	不能通过对象访问，否则报错
> 	
> __dict__
> 	通过类名访问，获取指定类的信息【类方法，静态方法，成员方法】，返回的是一个字典
> 	通过对象访问，获取的该对象的信息【所有的属性和值】，，返回的是一个字典
> 	
> __bases__
> 	通过类名访问，查看指定类的所有的父类【基类】
> ```

> 代码演示：
>
> ```Python
> class Animal(object):
>     def __init__(self,arg):
>         super(Animal, self).__init__()
>         self.arg = arg
>
>
> class Tiger(Animal):
>     age = 100
>     height = 200
>
>     def __init__(self,name):
>         #super(Tiger, self).__init__(name)
>         self.name = name
>
>     def haha(self):
>         print("haha")
>
>     @classmethod
>     def test(cls):
>         print("cls")
>
>     @staticmethod
>     def show():
>         print("show")
>
>
> if __name__ == "__main__":
>
>     #1.__name__
>     print(Tiger.__name__)  #Tiger
>
>     t = Tiger("")
>     #print(t.__name__)  #AttributeError: 'Tiger' object has no attribute '__name__'
>
>     #2.__dict__
>     print(Tiger.__dict__)  #类属性，所有的方法
>     print(t.__dict__)   #实例属性
>
>     #3.__bases__，获取指定类的所有的父类，返回的是一个元组
>     print(Tiger.__bases__)
> ```

### 四、运算符重载【了解】

> 运算符重载其实就是函数重写
>
> 代码演示：
>
> ```Python
> print(1 + 1)
> print("1" + "1")
> #print("1" + 1)
> #不同的数据类型进行加法运算得到的是不同的解释
>
> #思考问题：两个对象相加？
> class Person(object):
>     def __init__(self,num):
>         self.num = num
>
>     def __str__(self):
>         return "num=" + str(self.num)
>
>     def __add__(self, other):
>         #两个对象相加得到的结果仍然为一个对象
>         return Person(self.num + other.num)   #Peson(30)
>
>
> p1 = Person(10)
> p2 = Person(20)
>
> print(p1)  #10
> print(p2)  #20
>
> print(p1 + p2)  #30
>
> #p1 + p2----->p1.__add__(p2),
> ```

### 五、单例设计模式【扩展】

#### 1.概念

> 什么是设计模式
>
> ​	经过已经总结好的解决问题的方案
>
> ​	23种设计模式，比较常用的是单例设计模式，工厂设计模式，代理模式，装饰模式
>
> 什么是单例设计模式
>
> ​	单个实例【对象】
>
> ​	在程序运行的过程中，确保某一个类只能有一个实例【对象】，不管在哪个模块中获取对象，获取到的都是同一个对象
>
> ​	单例设计模式的核心：一个类有且仅有一个实例，并且这个实例需要应用在整个工程中

#### 2.应用场景

> 实际应用：数据库连接池操作-----》应用程序中多处需要连接到数据库------》只需要创建一个连接池即可，避免资源的浪费

#### 3.实现

##### 3.1模块

> Python的模块就是天然的单例设计模式
>
> 模块的工作原理：
>
> ​	import xxx,模块被第一次导入的时候，会生成一个.pyc文件，当第二次导入的时候，会直接加载.pyc文件，将不会再去执行模块源代码

##### 3.2使用new【掌握】

> ```
> __new__（）:实例从无到有的过程【对象的创建过程】
> ```
>
> 代码演示：
>
> ```Python
> class Singleton(object):
>     #类属性
>     instance = None
>
>     #类方法
>     @classmethod
>     def __new__(cls, *args, **kwargs):
>         #如果instance的值不为None，说明已经被实例化了，则直接返回；如果为NOne，则需要被实例化
>         if not cls.instance:
>             cls.instance = super(Singleton,cls).__new__(*args, **kwargs)
>
>         return cls.instance
>
> class MyClass(Singleton):
>     pass
>
> #当创建对象的时候自动被调用
> one = MyClass()
> two = MyClass()
>
> print(id(one))
> print(id(two))
>
> print(one is two)
> ```

##### 3.3装饰器【掌握】

> 代码演示：
>
> ```Python
> #单例类：将装饰器作用于一个类上
> def singleton(cls):
>     #类属性
>     instance = {}
>
>     #成员方法
>     def getSingleton(*args, **kwargs):
>         #思路：如果cls在字典中，则直接返回；如果不存在，则cls作为key，对象作为value，添加到字典中
>         if cls not in instance:
>             instance[cls] = cls(*args, **kwargs)
>         return  instance[cls]
>
>     return getSingleton
>
> @singleton
> class Test(object):
>     pass
>
> t1 = Test()
> t2 = Test()
>
> print(id(t1) == id(t2))
> print(t1 is t2)
> ```

##### 3.4使用在类中【掌握】

> 代码演示：
>
> ```Python
> #单例类
> class Foo(object):
>     #1.声明一个变量【类属性】
>     instance = None
>
>     #2.向外界提供一个公开的方法，用于返回当前类唯一的对象
>     #方法命名格式：defaultInstance,currentInstance ,getInstance
>     @classmethod
>     def getInstance(cls):
>         if cls.instance:
>             return cls.instance
>         else:
>             #实例化
>             cls.instance = cls()
>             return  cls.instance
>
> obj1 = Foo.getInstance()
> obj2 = Foo.getInstance()
>
> print(id(obj1) == id(obj2))
> print(obj1 is obj2)
> ```

