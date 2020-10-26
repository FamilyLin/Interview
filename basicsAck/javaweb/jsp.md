jsp (java service pages)

解决了Tomcat回传html代码复杂的问题

##### 1、在web目录下创建.jsp文件



##### 2、jsp如何访问：

例子：在web目录下：a.html   b.jsp

访问路径相同：http://ip:port/工程路径/a.html

​                           http://ip:port/工程路径/b.jsp



##### 3、jsp本质上是一个Servlet程序

当第一次访问jsp页面时，Tomcat服务器会帮我们把jsp页面翻译成一个java源文件，并且对其进行编译，变为.class程序

HttpJspBase 类直接继承了HttpServlet类，即jsp翻译出来的java类，间接继承了HttpServlet类，翻译出来的是一个Servlet程序

jsp就是Servlet程序



##### 4、jsp头部page指令

可以修改jsp页面中一些重要的属性或者行为

例子：

<%@ page contentType="text/html;charset=UTF-8" 

pageEncoding="UTF-8"

language="java" %>

errorpage属性：设置当jsp页面运行出错时，自动跳转去的错误页面路径

![image-20200731224501578](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200731224501578.png)

![image-20200731224609063](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200731224609063.png)

![image-20200731224905581](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200731224905581.png)



##### 5、jsp中的常用脚本

声明脚本：

<%!   声明java代码   %>

可以给jsp翻译出来的java类定义属性、static静态代码块、类方法、内部类



表达式脚本：

<%= 表达式 %>

在jsp页面上输出数据：整型、浮点型、字符串、对象

表达式脚本以out.print()的方式输出到页面上



代码脚本：

<%      java语句  %>

可以在jsp页面上，编写我们自己的方法



##### 6、jsp中的三种注释

①HTML注释

<!--    注释   -->

会被翻译到java源代码中，out.write()输出到客户端

②java注释

<%

​      //单行java注释

/*  多行java注释   */

%>

被翻译到java源代码中，

③jsp注释

<% --    jsp注释     --%>

jsp注释可以注释所有代码



##### 7、jsp九大内置对象

![image-20200731232059162](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200731232059162.png)



##### 8、四大域对象

![image-20200731232308372](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200731232308372.png)

使用优先顺序：

pageContext===>request===>session===>application



##### 9、jsp中的out输出和response.getWriter输出的区别

当jsp页面中所有代码执行完成后会做以下两个操作

①执行out.flush()操作，将out缓冲区的数据追加到response缓冲区末尾

②会执行response的刷新操作，把全部数据写给客户端



jsp翻译之后，

out.write()输出字符串没问题

out.print()输出任意数据都没问题（都转换我字符串后调用write输出）



##### 10、jsp的常用标签

①静态包含

在主页面jsp文件中写：

<%@ include file="/filename/footer.jsp"%>

然后在footer.jsp文件中写代码

a.静态包含不会翻译被包含的jsp页面

b.静态包含其实就是把被包含的jsp页面的代码拷贝到包含的位置执行输出



②动态包含

在主页面jsp文件中写

<jsp:include page="/include/footer.jsp">

​      <jsp:param name="username" value="bbj"/>

​      <传递函数/>

< /jsp:include >

需要在被包含jsp页面中写入：

<%request.getParameter("username")%>

a.动态包含会把被包含的jsp页面翻译为java代码

b.动态包含底层代码使用如下代码去调用jsp页面执行

c.动态包含还可以传递函数

JspRuntimeLibrary.include(request,response,"/include/footer.jsp",out,false);

![image-20200801083150882](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801083150882.png)





③请求转发

<jsp:forward page="/scope2.jsp">< /jsp:forward >



11、Listener监听器（接口）

javaweb的三大组件：servlet程序、Filter过滤器、Listener监听器

作用：监听变化，然后通过回调函数，反馈给程序做一些相应处理

ServletContextListener监听器：

可以监听ServletContext对象的创建和销毁

ServletContext对象在web工程启动的时候创建，在web工程停止的时候销毁

a、监听到创建和销毁后分别调用ServletContextListener监听器的方法反馈：

contextInitialized():监听到创建之后调用，做初始化

contextDestroyed:监听到销毁之后调用

b、使用步骤：

​      ①编写一个类实现ServletContextListener对象

​      ②实现两个回调方法

​      ③在web.xml中配置监听器

![image-20200801091803174](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801091803174.png)











