### 一、面向对象思想

#### 1.面向对象思想设计

> 基于哲学观点：万物皆对象
>
> 举例说明：
>
> 案例一：我想吃大盘鸡
>
> 面向过程						面向对象
>
> 1.自己去买菜						1.委托一个人帮忙买菜
>
> 2.自己择菜						2.委托一个人帮忙择菜
>
> 3.自己做菜						3.委托一个人厨师做菜
>
> 4.自己吃							4.自己吃
>
> 案例二：小明是一个电脑小白，想要配置一台电脑
>
> 面向过程						面向对象
>
> 1.小明补充电脑知识				1.委托一个懂电脑的人买零件
>
> 2.小明去买零件					2.委托一个人组装
>
> 3.小明把零件运回来				3.小明打开玩游戏
>
> 4.小明组装
>
> 5.小明打开玩游戏
>
> 案例三：一辆红色的法拉利在京藏高速上奔驰
>
> 法拉利   京藏高速
>
> 面向过程：狗吃屎    		面向对象：吃狗屎
>
> 面向过程：蛋炒饭		面向对象：盖浇饭

#### 2.面向过程和面向对象的区别

##### 2.1面向过程

> process：处理
>
> 在生活案例中：
>
> ​	一种看待问题的思维方式，在解决问题的时候，侧重于问题是怎样一步一步解决的，然后亲力亲为的去解决
>
> 在程序中：
>
> ​	代码从上往下依次执行
>
> ​	各个模块之间的关系尽可能的独立的，当import的时候，加载的顺序也是从上往下依次加载
>
> ​	每个模块中的语句结构：顺序，分支，循环

##### 2.2面向对象

> 在生活案例中：
>
> ​	一种看待问题的思维方式，侧重于找到一个具有特殊功能的个体，然后委托这个个体帮忙完成某件事情，这个个体就被称为对象
>
> ​	好处：可以将复杂的问题简单化，将程序员从执行者变成了指挥者
>
> 在程序中：
>
> ​	根据不同的需求执行代码【代码执行顺序不一定】
>
> ​	程序的流程完全由需求决定【对象】
>
> ​	思想：如果对象存在，则直接使用；如果对象不存在，则创建对象
>
> 注意：面向对象只是一种思想，并不是一门编程语言
>
> Python是一门面向对象的编程语言，类和对象是 面向对象的核心

### 二、类和对象【掌握】

#### 1.类和对象的概念

> 类：多个具有特殊功能的个体的集合
>
> 对象：在一个类中，一个具有特殊功能的个体，能够帮忙解决某件特定的事情，也被称为实例【instance】
>
> 两者之间的关系：类用于描述某一类对象的共同特征，而对象是类的具体的存在【包含关系】
>
> 思考问题：先有类还是先有对象？
>
> 【不好说，但是，在程序中使用的时候，一般是先定义类，然后创建对象】
>
> 举例：
>
> ​			类					对象
>
> ​			人					王麻子，李四，尼古拉斯.赵四。。。。
>
> ​			快递				韵达，中通，圆通。。。。。
>
> ​			SupreHero			蝙蝠侠，蜘蛛侠，美国队长，猪猪侠。。。
>
> 帮忙理解:类其实也是一种数据类型，只不过一般情况下是自定义的，所以可以将类认为是自定义的数据类型，用法和整型，string，list等基本是相同的【定义变量，传参】

#### 2.类的定义

> 语法：
>
> class  类名():
>
> ​	类体
>
> 说明：
>
> ​	a.Python中使用class关键字定义类
>
> ​	b.类名只要是一个合法的标识符即可，但是要求：遵循大驼峰命名法则【首单词的首字母大写，不同单词之间首字母大写】
>
> ​	c.通过缩进区分类体
>
> ​	d.类体一般包含两部分内容：对类的特征的描述、对类的行为的描述
>
> 代码演示：
>
> ```Python
> #类的定义
> #类的声明
> class MyClass():
>     #类的实现
>     #类体
>     #print("hello")   #一般不会这么书写
>     pass
>
> #注意：在同一个py文件中可以同时定义多个类，但是，为了提高代码的可读性，结合模块的使用，最好是一个文件一个类
> class MyClass1():
>     pass
> ```

#### 3.类的设计【类体的实现】

> 三要素：
>
> ​	事物名称【类名】：举例：人
>
> ​	事物的特征【变量】：名词，举例：姓名，年龄。。。。
>
> ​	事物的行为【函数/方法】：动词，举例：吃，跑。。。。

### 三、类中的方法和变量【掌握】

#### 1.类中的方法和变量的定义

> 类中的方法和变量是为了描述事物的行为和特征
>
> 类中定义的方法被称为成员方法
>
> 类中定义的变量被称为成员变量，也被称为属性      [os.name]
>
> 成员变量：类具有的特征
>
> 成员方法：类具有的行为
>
> 类存在的意义：拥有相同特征和行为的对象可以抽取出来一个类，类的存在是为了创建一个具体的对象
>
> 代码演示：
>
> ```Python
> #定义类
> #1.事物的名称：类名
> class Person():
>     #2.事物的特征：成员变量、属性
>     name = ""
>     age = 0
>     height = 0.0
>
>     #3.事物的行为：成员方法【函数】
>     #注意：类中的成员方法区别于普通方法：参数部分一定包含self，而且最好self出现在参数列表的第一个
>     #调用函数的时候，self不需要被传参
>     #初次之外，成员方法的用法和普通方法的使用完全相同，也可以设置默认参数或者关键字参数，不定长参数
>
>     #注意：self：自己，代表类的实例【对象】
>     #此处的self可以是任意的标识符，只不过为了结合其他编程的使用，习惯上使用self
>     def eat(self,food):
>         print("eating",food)
>     def run(self):
>         print("running")
> ```

#### 2.类中方法和属性的使用

2.1创建对象【实例化对象】

> 已知类，通过类创建对象
>
> 对象的创建过程被对象的实例化过程
>
> 语法：变量名 = 值
>
> ​	    对象名 = 类名()
>
> 代码演示：
>
> ```Python
> #定义类
> #1.事物的名称：类名
> class Person():
>     #2.事物的特征：成员变量、属性
>     name = ""
>     age = 0
>     height = 0.0
>
>     #3.事物的行为：成员方法【函数】
>     #注意：类中的成员方法区别于普通方法：参数部分一定包含self，而且最好self出现在参数列表的第一个
>     #调用函数的时候，self不需要被传参
>     #初次之外，成员方法的用法和普通方法的使用完全相同，也可以设置默认参数或者关键字参数，不定长参数
>
>     #注意：self：自己，代表类的实例【对象】
>     #此处的self可以是任意的标识符，只不过为了结合其他编程的使用，习惯上使用self
>     def eat(self,food):
>         print("eating",food)
>     def run(self):
>         print("running")
>         print("self的地址：", id(self))
>
>
> #对象的创建
> p1 = Person()
> print(p1)
>
> p2 = Person()
> print(p2)
>
> #p1和p2被称为对象，变量名，引用，指向了真正的对象
> #p1和p2在栈空间中开辟了空间，真正的对象的被存储在堆空间中
>
> #通过对象调用类中的成员方法和访问类中的成员变量
> #1.访问属性
> #语法：对象.属性名
> #赋值：对象.属性 = 值
> per = Person()
> print(per.name)
> per.name = "小姐姐"
> print(per.name)
> per.age = 18
> print(per.age)
> per.height = 1.70
> print(per.height)
>
> #2.调用方法
> #语法：对象.函数名(参数列表)
> #注意：self不需要被传参，传参的时候注意区分参数的类型【默认参数，不定长参数，关键字参数】
> per.run()
> print("per的地址：",id(per))
> """
> self的地址： 2687721120880
> per的地址： 2687721120880
> """
> per.eat("apple")
>
> person = Person()
> person.name = "张三"
> person.age = 20
> print(person.name,person.age)
> person.run()
> person.eat("")
>
> #结论：类中的成员变量和成员方法随着对象的出现而出现
> ```
>
> 总结：
>
> ​	访问变量采用：对象名.属性名
>
> ​	访问方法采用：对象名.方法名(参数列表)

#### 3.内存中的对象

> per = Person()
>
> 说明：
>
> a.程序中定义的Person类型的变量per实际上是一个变量名，它被存放在栈内存中，他指向实际的Person对象，而真正的Person对象则存放于堆内存中
>
> b.类中的成员变量随着对象的出现而出现，随着对象的消失而消失
>
> c.每个对象的成员变量会在堆空间中开辟一份自己的空间，相互之间互不影响

#### 4.动态绑定属性和限制绑定

> ```
> __slots__变量的作用：限制一个类中的成员变量【程序在运行的过程中，就不能随意的动态绑定属性】
> 语法：__slots__ = (属性的名称)
> ```
>
> 代码演示：
>
> ```Python
> #1.类的定义
> class MyClass():
>     #2.成员变量
>     """
>     num1 = 0
>     num2 = 10
>     """
>     #限制属性
>     #注意：被限制的属性的名称通过字符串的方式出现在元组的元素中
>     __slots__ = ("num1","num2")
>
>     #3.成员方法
>     def fun1(self):
>         print("fun1")
>     def fun2(self,num):
>         print(num)
>
> #4.创建对象
> my = MyClass()
> #5.访问类中的成员变量
> my.num1 = 11
> my.num2 = 22
> print(my.num1,my.num2)
>
> #6.调用类中的成员方法
> my.fun1()
> my.fun2(30)
>
> #成员变量随着对象的出现而出现的
> #属性的动态绑定【Python是一门动态语言】
> my.n = 100
> print(my.n)
>
> my1 = MyClass()
> #print(my1.n)
> ```

#### 5.综合案例一

> 代码演示：
>
> practiceDemo01.py文件【测试模块】
>
> ```Python
> """
> 需求：使用面向对象的思想描述下面这个情景
> 开学了，王老师让小明，小花，小丽分别做自我介绍
> 需要介绍姓名，年龄，爱好，来一段才艺展示
> """
> """
> 分析：
> 老师类
>     特性：姓名
>     行为：让学生做自我介绍
>
> 学生类
>     特征：姓名，年龄，爱好
>     行为：一段才艺展示
> """
> #导入
> """
> import  practice01.teacher
> import  practice01.student
> """
> from practice01.teacher import  Teacher
> from practice01.student import Student
>
> #1.创建一个老师的对象
> wang = Teacher()
> wang.name = "王老师"
>
> #2.创建一个学生的对象
> xiaohua = Student()
> xiaohua.name = "小花"
> xiaohua.age = 18
> xiaohua.hobby = "唱歌"
>
> #3.让老师执行自己的行为
> wang.letStudentIntroduce(wang.name,xiaohua)   #stu = xiaohua
>
> xiaoli = Student()
> xiaoli.name = "小丽"
> xiaoli.age = 20
> xiaoli.hobby = "跳舞"
> wang.letStudentIntroduce(wang.name,xiaoli)
>
> xiaoming = Student()
> xiaoming.name = "小明"
> xiaoming.age = 25
> xiaoming.hobby = "吹牛逼"
> wang.letStudentIntroduce(wang.name,xiaoming)
> ```
>
> teacher.py文件【实体类】
>
> ```Python
> #老师类
> class Teacher():
>     #特征：成员变量
>     name = ""
>
>     #行为：成员方法
>     def letStudentIntroduce(self,name,stu):
>         #老师发出指令
>         print(name + "让" + stu.name + "做自我介绍")
>
>         #执行指令
>         stu.introduce(stu.name,stu.age,stu.hobby)
>
>         #不同的学生展示不同的才艺
>         if stu.name == "小花":
>             stu.singSong()
>         elif stu.name == "小丽":
>             stu.dance()
>         else:
>             stu.lie()
> ```
>
> student.py文件【实体类】
>
> ```Python
> #学生类
> class Student():
>     #特征：成员变量
>     name = ""
>     age = 0
>     hobby = ""
>
>     #行为：成员方法
>     def introduce(self,name,age,hobby):
>         print("大家好，我是%s，今年%d,爱好%s"%(name,age,hobby))
>
>     #唱歌
>     def singSong(self):
>         print("娘子~啊哈")
>
>     #跳舞
>     def dance(self):
>         print("广场舞")
>
>     #吹牛逼
>     def lie(self):
>         print("我家可穷了，就养了几百头牛")
> ```

### 四、构造函数和析构函数

#### 1.构造函数【掌握】

> ```
> 采用上面的方式创建对象【直接给成员变量赋值】，很多的类一般倾向于创建成有初始状态的
> __init__:构造函数【作用：创建对象，给对象的成员变量赋初始值】
> 构造函数：构造器
> 调用的时机：当一个对象被创建的时候，第一个被自动调用的函数
> per = Person()
>
> 语法：
> 	def __init__(self,args1,args2....)
> 		函数体
> 说明：
> 	a.之前的写法中并没有显式的定义__init__函数，说明系统默认提供了一个无参的构造函数
> 	b.args1,args2...一般设置的形参列表和成员变量有关
> ```
>
> 代码演示：
>
> ```Python
> #1.构造函数被调用的时机
> class Check():
>     num1 = 0
>     str1 = ""
>
>     #构造函数
>     def __init__(self):
>         print("jfahj")
>
>     def show(self):
>         print("show")
> #注意：当创建对象的时候，默认调用了系统提供的无参的构造函数
> c = Check()
> c.show()
>
> #2.给构造函数添加参数
> class Check1():
>     name = ""
>     age = 0
>     """
>     def __init__(self,n,a):
>         print("fajkgak")
>     """
>     #注意2：当使用构造函数的时候，可以使用无参的，也可以使用有参的，在Python中的解决办法：设置不定长参数
>     #注意3：Python中，一个类中只能有一个构造函数
>     def __init__(self, *n):
>         print("fajkgak")
>
>
> #注意1：当手动头添加了有参的构造函数之后，系统将不再提供无参的构造函数
> c1 = Check1()
> c11 = Check1("fsiugh")
>
> #3.有参构造函数的使用
> class Check2():
>     name = ""
>     age = 0
>
>     #构造函数的形参列表：和成员变量有关
>     def __init__(self,n,a):
>        print(n,a)
>        name = n
>        age = a
>
> #注意1：当手动头添加了有参的构造函数之后，系统将不再提供无参的构造函数
> c2 = Check2("zhangsan",10)
> print(c2.name,c2.age)   #0
>
>
> #4.self的使用
> class Check3():
>     name = ""
>     age = 0
>
>     #构造函数的形参列表：和成员变量有关
>     def __init__(self,n,a):
>        print(n,a)
>        #self的使用：通过self来区分成员变量和局部变量,所以self.name代表name是一个全局变量【成员变量】
>        self.name = n
>        self.age = a
>
> c3 = Check3("zhangsan",10)
> print(c3.name,c3.age)  #10
>
> #5.使用self之后，可以省略成员变量的定义【掌握】
> #self只是一个标识符，可以替换成任意的标识符
> class Check4():
>
>     #构造函数的形参列表：和成员变量有关
>     def __init__(self,name,age):
>        print(name,age)
>        #self的使用：通过self来区分成员变量和局部变量,所以self.name代表name是一个全局变量【成员变量】
>        self.name = name
>        self.age = age
>
>     def show(self):
>         print("showing")
>
> c4 = Check4("lisi",20)
> print(c4.name,c4.age)
> c4.show()
> ```

#### 2.析构函数

> ```
> 与构造函数正好相反，当对象被销毁的时候自动调用的函数，被称为析构函数
> __del__:
>
> 删除变量：   del  变量名，此时可以触发析构函数的调用
>
> 使用情景：清理工作，比如关闭数据库，关闭文件等
> ```
>
> 代码演示：
>
> ```Python
> import  time
>
> class Pig():
>     def __init__(self,name,age):
>         self.name  = name
>         self.age = age
>         print("构造函数被执行")
>
>
>     def show(self):
>         print("show")
>
>     #析构函数
>     def __del__(self):
>         print("~析构函数被调用")
>
>
> #析构函数被调用的时机：1：当程序运行完成的时候    2：使用del删除变量
> p = Pig("abc",10)
>
> del p
>
> #注意：对象释放以后就不能再访问了【相当于根本未创建过这个对象】
> #print(p.age)
>
> time.sleep(5)
>
> #在函数里定义的对象，会在函数结束时自动释放，这样可以用来减少内存空间的浪费
> #其实就是作用域的问题
> def func():
>     per2 = Person("aa", 1, 1, 1)
>
> func()
> ```

#### 3.综合案例二

> practiceDemo02.py文件【测试模块】
>
> ```Python
> """
> 需求：富二代王思聪开着豪车，很自豪的向他的新女友炫耀
>
> 富二代类
> 特征：姓名
> 行为：开车，炫耀
>
> 汽车类
> 特征：品牌，颜色
> 行为：奔驰
> """
> #测试模块
> from  practice02.car import Car
> from practice02.richMan import RichMan
>
> #1.创建一个富二代的对象
> wang = RichMan("王思聪")
>
> #2.创建一个汽车的对象
> c = Car("玛莎拉蒂","闷骚红")
> c.run()
>
> #3.让富二代执行自己的行为
> wang.driveCar(c)
> wang.showCar(c)
> ```
>
> richMan.py文件【实体类】
>
> ```Python
> class RichMan():
>     #构造函数
>     def __init__(self,name):
>         self.name = name
>
>     #成员函数
>     def driveCar(self,car):
>         print("富二代%s开着他的豪车%s"%(self.name,car.brand))
>     def showCar(self,car):
>         print(car.brand,car.color)
> ```
>
> car.py文件【实体类】
>
> ```Python
> class Car():
>     #构造函数
>     def __init__(self,brand,color):
>         self.brand = brand
>         self.color = color
>
>     #成员函数
>     def run(self):
>         print("%s在马路上奔驰"%(self.brand))
> ```