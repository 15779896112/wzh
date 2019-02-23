### 一、网络编程

#### 1.网络编程基础

##### 1.1概念

> 计算机网络：把分布在不同区域的计算机【设备】与专门的一些外部设备通过通信线路相关联，形成一个网络系统，从而使得计算机之间可以共享数据
>
> 网络编程：同一个网络中不同的机器之间的通信

##### 1.2计算机之间需要通信的必要条件

> ip地址，端口，网络协议
>
> 1.>ip地址
>
> ​	互联网协议地址【Internet Protocol Address】，是联网设备和互联网之间的唯一标识，在同一个网段中，ip地址是唯一的
>
> ​	ip地址是数字型，是一个32位的整数，
>
> ​		举例：10.36.131.32：32位的整数，分成4个8位的二进制，将二进制转换为0~255之间的十进制整数
>
> ​	分类：
>
> ​	a.形式分类
>
> ​		ipv4:分为4段
>
> ​		ipv6:分为6段
>
> ​	b.功能分类
>
> ​		A类：保留给政府机构，1.0.0.1~126.255.255.255
>
> ​		B类：分配中型企业，128.。。。。~191.。。
>
> ​		C类：分配个人,192...~223
>
> ​		D类：组播，224~239
>
> ​		E类：实验，240~255
>
> ​	127.0.0.1：回送地址，一般指的是本机的ip，localhost，一般用来进行测试
>
> ​	总结：ip地址可以唯一确定网络上的一个通信实体，但是一个通信实体上可能有很多的应用程序，可以同时提供网络服务，此时还需要借助于端口进行区分
>
> 2>端口
>
> ​	数据的发送和接收都需要通过端口，端口号用于唯一标识通信实体上进行网络通信的程序
>
> ​	注意：同一台机器上的不同的应用程序不能占用同一个端口，端口的范围：0~65535
>
> ​	作用：ip地址结合端口号，就可以唯一的确定一个网络中唯一一台计算机上的一个应用程序
>
> ​	分类：
>
> ​		a.公认端口：0~1023
>
> ​		b.注册端口：1025~49151
>
> ​		c.动态端口或者私有端口:1024~65535
>
> ​	常用端口：
>
> ​	mysql:3306
>
> ​	oracle:1521
>
> ​	tomcat:8080
>
> ​	qq；4000
>
> 3>网络协议
>
> ​	http:被动式协议
>
> ​	tcp
>
> ​	udp
>
> ​	tcp/ip：互联网协议

#### 2.TCP编程

> Transmission Control Protocol，传输控制协议，是一个传输层的通信协议
>
> 客户端/服务端：套接字【socket】，程序通常通过套接字向网络发出请求或者应答网络请求，使得两台设备之间进行通信
>
> 理解;打开了一个网络连接，必须知道ip地址，端口号，协议
>
> ​	特点：
>
> ​	a.安全的【确保接收方完全正确的接收数据】
>
> ​	b.面向连接【数据传输之前必须要建立连接】
>
> ​	c.传输的效率较低【面向连接需要耗时】
>
> ​	d.一旦连接建立，双方可以按照指定的格式发送数据【大小没有限制】
>
> 使用经典三次握手建立连接
>
> ​	a.客户端向服务端发起请求
>
> ​	b.服务端收到请求之后，会给客户端一个响应
>
> ​	c.客户端收到服务端的响应之后，给服务端回复一个确认信息
>
> 总结：使用tcp实现数据的发送和接收需要有发送方和接收方，但是两个通信实体之间没有明确的客户端或者服务端之分，在两个通信实体在建立连接之前，必须有一个通信实体先做出主动姿态，主动发起请求

##### 2.1socket通信流程

> 代码演示：
>
> server:
>
> ```Python
> #服务端流程描述
> import  socket
>
> #1.创建服务端的socket对象
> serverSocket = socket.socket()
>
> #2.为socket绑定端口和ip地址
> """
> bind(元组)，将端口号和ip地址创建元组，然后传参
> (host,port)
> """
> #查看ip地址：在终端输入ipconfig命令
> ip_port = ("10.36.131.32",6666)
> serverSocket.bind(ip_port)
>
> #3.服务端监听请求，随时准备接受客户端发来的连接
> """
> listen(backlog)
> backlog:在拒绝连接之前，可以挂起的最大连接数量
> 注意：不能无限大
> """
> serverSocket.listen(5)
>
> print("server waiting~~~~~")
>
> #4.服务端接收到客户端的请求，被动打开进行连接
> #accept()；在连接的时候，会处于阻塞状态
> #返回值：conn,address,conn表示连接到的套接字对象，address表示连接到的客户端的地址
> conn,addr = serverSocket.accept()
>
> #5.服务端接收消息
> """
> recv(size)
> 可以一次性接收到多大的数据
> """
> client_data = conn.recv(1024)
> print(str(client_data,"utf-8"))
>
> #6.服务端关闭
> serverSocket.close()
> ```
>
> client:
>
> ```Python
> import  socket
>
> #1.创建socket对象
> clientSocket = socket.socket()
>
> #2.发起连接请求
> #connect(元组)
> #（host,port）ip地址和端口号需要和服务端中绑定的ip地址以及端口号保持一致
> ip_port = ("10.36.131.32",6666)
> clientSocket.connect(ip_port)
>
> #3.发送数据
> #sendall(string) ,字节类型的字符串【编码的过程】
> clientSocket.sendall(bytes("hello你好啊",encoding="utf-8"))
>
> #4.关闭客户端
> clientSocket.close()
> ```

##### 2.2客户端和服务端的数据交互

> 代码演示：
>
> server:
>
> ```Python
> import  socket
>
> server = socket.socket()
>
> server.bind(("10.36.131.32",6666))
>
> server.listen(5)
>
> conn,address = server.accept()
>
> print("连接成功")
>
> while True:
>     clientData = conn.recv(1024)
>     result = clientData.decode("utf-8")
>     print("客户端对服务端说：",result)
>
>     if result == "bye" or result == "再见":
>         break
>
>     sendData = input("请输入要给回复客户端的数据：")
>     conn.send(sendData.encode("utf-8"))
>
> server.close()
> ```
>
> client:
>
> ```Python
> import  socket
>
> client = socket.socket()
>
> client.connect(("10.36.131.32",6666))
>
> while True:
>     sendData = input("请输入要发送给服务端的数据：")
>     client.send(sendData.encode("utf-8"))
>
>     serverData = client.recv(1024)
>     result = serverData.decode("utf-8")
>     print("服务端回复：",result)
>
>     if result == "bye":
>         break
>
> client.close()
> ```

#### 3.UDP编程

> User Datagram Protocol,用户数据包协议
>
> 特点：
>
> ​	a.不安全的
>
> ​	b.无连接
>
> ​	c.效率高，速度快
>
> ​	d.对数据的大小是有限制的，每个被传输的数据包的大小不超过64k



### 四、发邮件和发短信【扩展】

#### 1.发短信

> 互亿无线
>
> ```
> #发送短信
> #APIID：C11345804
> #APIKEY：735d183ae02189f678c26800ac19b03a
> ```

> 代码演示：
>
> ```Python
> # 接口类型：互亿无线触发短信接口，支持发送验证码短信、订单通知短信等。
> # 账户注册：请通过该地址开通账户http://sms.ihuyi.com/register.html
> # 注意事项：
> # （1）调试期间，请使用用系统默认的短信内容：您的验证码是：【变量】。请不要把验证码泄露给其他人。；
> # （2）请使用APIID（查看APIID请登录用户中心->验证码短信->产品总览->APIID）及 APIkey来调用接口；
> # （3）该代码仅供接入互亿无线短信接口参考使用，客户可根据实际需要自行编写；
>
> # !/usr/local/bin/python
> # -*- coding:utf-8 -*-
> import http.client
> import urllib
>
> host = "106.ihuyi.com"
> sms_send_uri = "/webservice/sms.php?method=Submit"
>
> # 用户名是登录用户中心->验证码短信->产品总览->APIID
> account = "C11345804"
> # 密码 查看密码请登录用户中心->验证码短信->产品总览->APIKEY
> password = "735d183ae02189f678c26800ac19b03a"
>
> def send_sms(text, mobile):
>     params = urllib.parse.urlencode(
>         {'account': account, 'password': password, 'content': text, 'mobile': mobile, 'format': 'json'})
>     headers = {"Content-type": "application/x-www-form-urlencoded", "Accept": "text/plain"}
>     conn = http.client.HTTPConnection(host, port=80, timeout=30)
>     conn.request("POST", sms_send_uri, params, headers)
>     response = conn.getresponse()
>     response_str = response.read()
>     conn.close()
>     return response_str
>
>
> if __name__ == '__main__':
>     #需要接受短信的目标手机号
>     mobile = "18566666666"
>     text = "您的验证码是：121254。请不要把验证码泄露给其他人。"
>
>     print(send_sms(text, mobile))
> ```

#### 2.发邮件

> 代码演示：
>
> ```Python
> #发送纯文本
> #发邮件的模块
> import  smtplib
> #邮件标题
> from  email.header import Header
> #邮件文本
> from  email.mime.text import MIMEText
>
> """
> user:用户名
> pwd:授权码
> sender：发送方
> receiver：接收方
> content：邮件的正文
> title：邮件的标题
> """
> def sendMail(user,pwd,sender,receiver,content,title):
>     mail_host = "smtp.163.com"   #163的SMTP服务器
>
>     #第一部分：准备工作
>     #1.将邮件的信息打包成一个对象
>     message = MIMEText(content,"plain","utf-8")   #内容，格式，编码
>     #2.设置邮件的发送者
>     message["From"] = sender
>     #3.设置邮件的接收方
>     #message["To"] = receiver
>     #join():通过字符串调用，参数为一个列表
>     message["To"] = ",".join(receiver)
>     #4.设置邮件的标题
>     message["Subject"] = title
>
>     #第二部分：发送邮件
>     #1.启用服务器发送邮件
>     #参数：服务器，端口号
>     smtpObj = smtplib.SMTP_SSL(mail_host,465)
>     #2.登录邮箱进行验证
>     #参数：用户名，授权码
>     smtpObj.login(user,pwd)
>     #3.发送邮件
>     #参数：发送方，接收方，邮件信息
>     smtpObj.sendmail(sender,receiver,message.as_string())
>
>     print("mail send successful!")
>
> if __name__ == "__main__":
>     mail_user = "18501970795@163.com"
>     mail_pwd = "yang0122"
>
>     mail_sender = "18501970795@163.com"
>     mail_receiver = ["1490980468@qq.com"]
>
>     email_content = "人生苦短，我用Python"
>     email_title = "Python1805"
>
>     sendMail(mail_user,mail_pwd,mail_sender,mail_receiver,email_content,email_title)
>
> ```



