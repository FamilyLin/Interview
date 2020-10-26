Servlet

##### 1、web.xml   配置文件

##### 2、servlet生命周期

①执行servlet构造器方法

②执行init初始化方法

第一、二步是在第一次访问的时候创建servlet程序会调用

③执行service方法

第三步、每次访问都会调用

④执行destroy销毁方法

第四步在工程停止时调用



##### 3、使用继承HttpServlet类的方式去实现Servlet程序

①编写一个类去继承HttpServlet类

②重写doget 或 doPost方法

③在web.xml中配置的servlet程序的访问地址



##### 4、Servlet的为继承体系

Interface Servlet:  只负责定义Servlet程度的访问规范

Class GenericServlet    inplements  Servlet：定义很多空实现

Class HttpServlet    extends   GenericServlet；实现了service方法，实现请求的分发处理：

String method  =  req.getMethod();   get || post

doGet||doPost:负责抛异常，说不支持请求

自定义类继承HttpServlet,重写doGet||doPost



##### 5、ServletConfig类

①可以获取程序的别名

servletConfig.getServletName();

②获取初始化参数

servletConfig.getInitParameter();

③获取ServletContext对象





##### 6、ServletContext接口

①表示servlet上下文对象 

②一个web工程只有一个ServletContext对象实例

在工程启动时创建，工程关闭时销毁

③ServletContext对象是一个域对象；像Map一样存取数据的对象；

![image-20200730195802098](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730195802098.png)



作用：

//获取ServletContext对象

ServletContext context = getServletContext();

①获取web.xml中配置的上下文参数 context-parameter

context.getInitParameter("name");

②获取当前的工程路径：格式： /工程路径

context.getcContextPath();

③获取工程部署后在服务器硬盘上的绝对路径

context.getRealPath("/")

/  斜杠被服务器解析为：http://ip:port/工程名/

④像map一样存取数据

//设置

context.setAttribute("key","name");

//获取key值

context.setAttribute("key");





##### **7、Http协议**

①请求：

   i:Get请求

>    a/请求行：
>
> ​         (1)请求的方式：    GET
>
> ​         (2)请求的资源路径[ +? +请求参数]
>
> ​         (3)请求的协议版本号       HTTP/1.1
>
>    b/请求头
>
> ​         key: value   组成       不同的键值对，表示不同的含义
>
> 

![image-20200730202722355](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730202722355.png)



   ii: POST请求

>   a/请求行
>
> ​         (1)请求的方式：    POST
>
> ​         (2)请求的资源路径[ +? +请求参数]
>
> ​         (3)请求的协议版本号       HTTP/1.1
>
>    b/请求头
>
> ​         key: value   组成       不同的键值对，表示不同的含义
>
> 空行
>
>    c/请求体：发送给服务器的数据
>
> ​         

![image-20200730203249015](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730203249015.png)



iii: 请求类型

![image-20200730203521777](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730203521777.png)





②响应 的HTTP格式

  i: 响应行

> 响应的协议和版本号
>
> 响应状态码
>
> 响应状态描述符

 ii: 响应头

> key : value 对   不同的响应头有不同的含义

空行

Iii: 响应体 --》回传给客户端的数据

![image-20200730204047349](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730204047349.png)

③常见的响应码：

200      表示请求成功

302       表示请求重定向

404       表示请求服务器已经收到，但是数据不存在（请求地址错误）

500       表示服务器已经收到请求，但是服务器内部错误（代码错误）

![image-20200730204442825](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730204442825.png)



8、HttpServletRequest类

只要有请求进入Tomcat服务器，服务器就会把请求过来的http协议封装到Request对象中，然后传递到service方法（doget、dopost）中给我们使用，我们可以通过HttpServletRequest对象，获取到所有**请求**的信息。

常用方法：

>![image-20200730205740064](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730205740064.png)



10、用POST请求时

需要设置:req.setCharacterEncoding("UTF-8");

否则中文乱码



11、请求的转发

特点：

>浏览器地址不变
>
>一次请求
>
>共享Request域中的数据
>
>可以转发到WEB-INF目录下
>
>不可以访问工程以外的资源



![image-20200730224047270](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730224047270.png)

请求转发必须要以斜杠打头

RequestDispatcher requestDispatcher = req.getRequestDispatcher("/servlet2");

向前走

requestDispatcher.forward(req,resp)



12、base标签设置页面相对路径工作时参照的地址

href属性就是参数的地址

![image-20200730230317316](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730230317316.png)



![image-20200730230450148](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730230450148.png)

![image-20200730230722337](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730230722337.png)



13、HttpServletRespond类

resp.getWriter();    

需要设置：

resp.setCharacterEncoding("UTF-8");

还需要设置浏览器：

resp.setHeader("Content-Type","text/html;charset=UTF-8");

或者同时设置：

resp.setContentType("text/html;charset=UTF-8");

此方法需要在获取流之前使用

resp.getOutputStream();



14、请求重定向

指客户端给服务器发请求，然后服务器给客户端一个新地址去访问。

![image-20200731130812278](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200731130812278.png)

特点：

①地址栏会发生改变

②两次请求

③不共享Request域中的数据

④不能访问WEB-INIF下的资源

⑤可以访问工程外的资源

方法一：

![image-20200731131359225](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200731131359225.png)



方法二：

![image-20200731131448791](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200731131448791.png)















