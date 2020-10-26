JavaWeb

1、基于请求和响应

请求：Request

响应：Response

2、资源的分类

静态：html/css/js/txt

动态：Serverlet、JSP

3、常用服务器

Tomcat

4、

![image-20200730165015032](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730165015032.png)

5、Tomcat文件

![image-20200730165515384](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730165515384.png)

6、如何修改Tomcat的端口号

![image-20200730171127581](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730171127581.png)

平时http的默认端口号为：80

**7、怎样将web工程部署到Tomcat服务器上**

①第一种方式

![image-20200730171521963](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730171521963.png)

②第二种方式

首先找到Tomcat中的conf-->Catalina-->localhost文件

新建一个XML文件：abc.xml      (UTF-8)

示例：

<Context path="/abc" docBase="E:\Idea_project\book" />

Context表示工程上下文

path表示工程的访问路径

docBase表示工程目录位置

访问：http://ip:port/abc/index.html



8、手托一个html网页到浏览器和敲地址有什么不同

![image-20200730172915202](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730172915202.png)







9、新建一个服务器上的动态工程

![image-20200730174519782](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730174519782.png)

可以修改的：

URL、port、热部署