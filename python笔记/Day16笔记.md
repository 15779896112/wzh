### 一、破解密码

#### 1. 排列

> 代码演示：
>
> ```Python
> import  itertools
>
> #1。排列
> #从n个不同的元素中取出m（m <= n）个元素,按照一定的顺序排成一列
> #m == n,全排列(permutations)
> # 参数：可迭代对象，个数
> """
> 1 ,2 ,3
> 123
> 321
> 231
> 312
> ...
> """
>
> result1 = itertools.permutations([1,2,3,4],1)
> print(result1)
> list = list(result1)
> print(list)
> print(len(list))
>
> """
> 总结：
> 4-1     4
> 4-2     12
> 4-3     24
> 4-4     24
>
> 排列的可能性：n! / (n-m)!
> """
> ```

#### 2.组合

> 代码演示：
>
> ```Python
> import itertools
>
> #组合：从n个不同的元素中取出m个元素
>
> result2 = itertools.combinations([1,2,3,4],3)
> print(result2)
> list = list(result2)
> print(list)
> print(len(list))
>
> """
> 4-4    1
> 4-3    4
> 4-2    6
> 4-1    4
>
> 组合的可能性：n! / (m! * (n -m)!)
> """
> ```

#### 3.排列组合

> 代码演示：
>
> ```Python
> import  itertools
>
> list = list(itertools.product("0123456789qwertyuioplkjhgfdsazxcvbnm",repeat=3))
> print(list)
> print(len(list))
> ```

### 二、正则表达式

#### 1.引入案例

> 代码演示：
>
> ```Python
> import  re     #regular  Expession   regex
> #需求：判断一个qq号是否是合法的
> """
> 分析：
> 1.全数字
> 2.第一位数字不能为0
> 3.位数：5~11
> """
> def checkQQ(str):
>     #不管str是否合法，假设合法
>     result = True
>
>     #寻找条件推翻假设
>     try:
>         #判断是否是全数字
>         num = int(str)
>
>         #判断位数
>         if len(str) >= 5 and len(str) <= 11:
>
>             #判断开头是否为0
>             if str[0] == "0":
>                 result = False
>
>         else:
>             result = False
>     except ValueError as e:
>         result = False
>
>     return  result
>
>
> print(checkQQ("6725675785678657"))
>
> #使用正则表达式实现上面的需求
> result = re.match(r"[1-9]\d{4,10}","6725675786574657")
> print(result)
> ```

#### 2.概述

> 正则表达式【Regular Expression】，简写为regex，RE，使用单个字符串来描述一系列具有特殊格式的字符串
>
> 功能：
>
> ​	a.搜索
>
> ​	b.替换
>
> ​	c.匹配
>
> 使用情景:
>
> ​	爬虫
>
> ​	验证手机号，验证邮箱，密码【用户名】

#### 3.使用规则

##### 3.1匹配单个数字或者字符

> 代码演示：
>
> ```Python
> import  re
> """
> ----------匹配单个字符与数字---------
> .                匹配除换行符以外的任意字符
> [0123456789]     []是字符集合，表示匹配方括号中所包含的任意一个字符
> [good]           匹配good中任意一个字符
> [a-z]            匹配任意小写字母
> [A-Z]            匹配任意大写字母
> [0-9]            匹配任意数字，类似[0123456789]
> [0-9a-zA-Z]      匹配任意的数字和字母
> [0-9a-zA-Z_]     匹配任意的数字、字母和下划线
> [^good]          匹配除了good这几个字母以外的所有字符，中括号里的^称为脱字符，表示不匹配集合中的字符
> [^0-9]           匹配所有的非数字字符
> \d               匹配数字，效果同[0-9]
> \D               匹配非数字字符，效果同[^0-9]
> \w               匹配数字，字母和下划线,效果同[0-9a-zA-Z_]
> \W               匹配非数字，字母和下划线，效果同[^0-9a-zA-Z_]
> \s               匹配任意的空白符(空格，回车，换行，制表，换页)，效果同[ \r\n\t\f]
> \S               匹配任意的非空白符，效果同[^ \f\n\r\t]
> """
> #[]  :只匹配其中的一位
> # - ：表示一个区间
> #1.
> #1.1编译正则表达式返回对象
> pattern = re.compile(r"[abcd]")   #正则表达式  [a-d]
> #1.2使用正则表达式匹配字符串，成功返回对象，并携带匹配之后额结果，如果匹配失败则返回None
> ret = pattern.match("dhello")    #需要被匹配的字符串
> print(ret)
> print(ret.group())
>
> #2.
> pattern = re.compile(r"[s-z]")
> ret = pattern.match("xhello")
> print(ret)
> print(ret.group())
>
> #3
> pattern = re.compile(r"[0-9]")
> ret = pattern.match("5hello")
> print(ret)
> print(ret.group())
>
> #4
> pattern = re.compile(r"[0-9a-zA-Z]")
> ret = pattern.match("8hello")
> print(ret)
> print(ret.group())
>
> #5  ^:脱字符【】否定的含义
> pattern = re.compile(r"[^0-9]")
> ret = pattern.match("chello")
> print(ret)
> print(ret.group())
>
> #6 \d:只匹配数字，等同于[0-9]
> pattern = re.compile(r"\d")
> ret = pattern.match("4")
> print(ret)
> print(ret.group())
>
> #7.   \w
> pattern = re.compile(r"\w")
> ret = pattern.match("7")
> print(ret)
> print(ret.group())
>
> #8   \s
> pattern = re.compile(r"\s")
> ret = pattern.match("\t")
> print(ret)
> print(ret.group())
>
> #9.   .：匹配不到换行符【\n】
> pattern = re.compile(r".")
> ret = pattern.match("\r")
> print(ret)
> print(ret.group())
> ```

##### 3.2匹配边界字符

> 代码演示：
>
> ```Python
> import  re
> """
> --------------锚字符(边界字符)-------------
>
> ^     行首匹配，和在[]里的^不是一个意思   startswith
> $     行尾匹配                          endswith
>
> \A    匹配字符串开始，它和^的区别是,\A只匹配整个字符串的开头，即使在re.M模式下也不会匹配它行的行首
> \Z    匹配字符串结束，它和$的区别是,\Z只匹配整个字符串的结束，即使在re.M模式下也不会匹配它行的行尾
>
> \b    匹配一个单词的边界，也就是值单词和空格间的位置   bounds
> \B    匹配非单词边界
>
> """
> #search()
> print(re.search(r"^to","today is a good day"))
> print(re.search(r"day$","today is a good day"))
>
> #findall()
> #re.M
> print(re.findall(r"\Ato","today is a good day\ntoday is a good day",re.M))
> print(re.findall(r"^to","today is a good day\ntoday is a good day",re.M))
> #总结：\A只匹配第一行的行首，^匹配每一行的行首
>
> #\b匹配边界【开始和结尾】，\B匹配的是非边界【中间】
> print(re.search(r"er\b","never"))   #er
> print(re.search(r"er\b","nerve"))   #None
> print(re.search(r"er\B","never"))    #None
> print(re.search(r"er\B","nerve"))   #er
> ```

##### 3.3匹配多个字符

> 代码演示：
>
> ```Python
> import  re
> """
> -------------------匹配多个字符------------------------
>
> 说明：下方的x、y、z均为假设的普通字符,n、m（非负整数），不是正则表达式的元字符
> (xyz)    匹配小括号内的xyz(作为一个整体去匹配)
> x?       匹配0个或者1个x
> x*       匹配0个或者任意多个x（.* 表示匹配0个或者任意多个字符(换行符除外)）
> x+       匹配至少一个x
> x{n}     匹配确定的n个x（n是一个非负整数）
> x{n,}    匹配至少n个x
> x{n,m}   匹配至少n个最多m个x。注意：n <= m
> x|y      |表示或，匹配的是x或y
> """
>
> #（）当做一个整体去匹配，返回的结果为一个列表
> print(re.findall(r"(ab)","aaacccaabbbbb"))
>
> print(re.findall(r"a?","aaacccaabbbbb"))
> print(re.findall(r"a*","aaacccaabbbbb"))
> print(re.findall(r"a+","aaacccaabbbbb"))
> """
> ['a', 'a', 'a', '', '', '', 'a', 'a', '', '', '', '', '', '']
> ['aaa', '', '', '', 'aa', '', '', '', '', '', '']
> ['aaa', 'aa']
> """
> #恰好出现n次
> print(re.findall(r"a{2}","aaacccaabbbbb"))
> #至少出现n次
> print(re.findall(r"a{2,}","aaacccaabbbbb"))
> #{m,n}：至少出现m次，至多出现n次
> print(re.findall(r"a{2,5}","aaacccaabbbbb"))
> #表示或
> print(re.findall(r"a|b","aaacccaabbbbb"))   #[ab]
> ```

##### 3.4匹配分组

> 代码演示：
>
> ```Python
> import  re
>
> #匹配分组
> #|   :或
> #()   :整体
> #search:会在字符串中从左向左进行查找，如果找到第一个符合条件的，则停止查找
> #正则1|正则2：只要正则1或者正则2中的一个满足，则直接按照这个条件查找
> pattern = re.compile("\d+|[a-z]+")
> ret = pattern.search("123-d223344aa$$aa")   #abc123-d223344aa$$aa
> print(ret.group())
>
> pattern = re.compile("([a-z]\d)+\w+")
> ret = pattern.search("abc123-d223344aa$$aa")   #abc123-d223344aa$$aa
> print(ret.group())
> ```

##### 3.5子模式

> 代码演示：
>
> ```Python
> import  re
>
> #子模式
> #()
> #如果在正则表达式中出现\1  \2等标识符的时候，那么\1代表从左向右的第一个（）中的内容。。。被称为子模式【简化正则表达式】
> pattern = re.compile(r"<([a-z]+)><(\w+)>\w+</\2></\1>")
> ret = pattern.search("<div><span>hello</span></div>")
> print(ret.group())
> #子模式访问
> print(ret.group(1))
> print(ret.group(2))
> ```

##### 3.6贪婪和非贪婪

> 代码演示：
>
> ```Python
> import re
>
> #贪婪和非贪婪【匹配一位还是匹配多位的区别】
> #+   *  ：多次匹配【贪婪匹配】
> #在+或者*后面添加？则改为非贪婪匹配
> result1 = re.findall(r"a(\d+)","a23333333b")
> print(result1)   #['23333333']
>
> result1 = re.findall(r"a(\d+?)","a23333333b")
> print(result1)   #['2']
>
> #特殊情况;如果一个正则表达式的前后都有限定条件的时候，那么则不存在贪婪模式，？将不起作用
> result1 = re.findall(r"a(\d+)b","a23333333b")
> print(result1)
> result1 = re.findall(r"a(\d+?)b","a23333333b")
> print(result1)
> ```

##### 3.7模式修正

> 代码演示：
>
> ```Python
> import re
>
> #模式修正
> """
> re.I:忽略大小写模式【ignorecase】
> re.M：视为多行模式【more】
> re.S：视为单行模式【single】
> """
> pattern = re.compile(r"^love",re.M)
> string = """
> alove you
> love her
> love he
> """
> result1 = pattern.search(string)
> print(result1.group())
>
> pattern = re.compile(r"[a-z]+",re.I)
> result1 = pattern.search("LLLLLLlove")
> print(result1.group())
> ```

#### 4.re模块中常用功能函数

> 代码演示：
>
> ```Python
> import re
>
> #re模块中常用的函数
>
> #1.compile()
> str1 = "today is a good day"
> str2 = r"\w*"
> pattern1 = re.compile(str2)
> print(pattern1.findall(str1))
>
> #2.match()
> result = re.match(r"[1-9]\d{4,10}","6725675786574657")
> print(result)
>
> #3.search()
> #注意：只要匹配到一个符合条件的子字符串，则直接返回，后面的内容不参与搜索
> print(re.search(r"\dcom","www.4comnghughs").group())
>
> #4.findall()
> #注意;返回的结果为列表
> #finditer(): 返回的结果为可迭代器
> iter = re.finditer(r"\d+","12 fjhaehgj 66 fhaj  ")
> print(iter)
>
> for i in iter:
>     print(i)
>
>     #获取值
>     print(i.group())
>     #获取下标
>     print(i.span())
>
>
> #5.split() :返回一个列表
> s1 = "1one2two3445545three454four56977878five"
> print(re.split(r"\d+",s1))
> print(re.split(r"[0-9]{1,}",s1))
> print(re.split(r"[^a-z]+",s1))
>
> s2 = "zhangsan lilei      lisi    Han   Jack"
> print(re.split(r" +",s2))
>
> s3 = "zhangsan@@@@lilei##########lisi%%%Han&&&&&&&&&&&&&Jack"
> print(re.split(r"[^a-zA-Z]+",s3))
>
> #6.sub() 替换，返回的是替换之后的字符串
> string1 = "today is a good day today is a good da"
> #用-将空格替换
> #参数：旧的字符换【正则表达式】  新的字符串   原字符串
> print(re.sub(r"\s","-",string1))
>
> #subn()  替换，返回一个元组（新的字符串，替换的次数）
> print(re.subn(r"\s","-",string1))
> ```

#### 5.注意事项

> 代码演示：
>
> ```python
> import  re
>
> #注意问题
> #1.match，findall，search之间的区别
> a = re.search(r"[\d]","abc3ab5").group()
> print(a)   #3
>
> b = re.findall(r"[\d]","abc3ab5")
> print(b)  #['3']
>
> c = re.match(r"[\d]","abc3")
> print(c)  #None
>
> #2.flags的用法【模式修正】
> print(re.split("a","1A2a3A4a",re.I))   #['1A2', '3A4', '']
> """
> split(pattern,string,maxsplit,flags),当传入三个参数的时候，表示只匹配前三个参数，flags不起作用
> """
> #解决方案：关键字参数
> print(re.split("a","1A2a3A4a",flags=re.I))
>
> #3.使用split函数之后去除""
> poem = "床前明月光,疑是地上霜.举头望明月，低头思故乡。"
> list1 = re.split(r"[,.，。]",poem)
> print(list1)  #
>
> for item in list1:
>     if item == "":
>         list1.remove("")
>
> print(list1)  #['床前明月光', '疑是地上霜', '举头望明月', '低头思故乡']
> ```