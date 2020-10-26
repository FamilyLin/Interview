EL表达式和JSTL标签库

# 一、EL表达式

Expression Language

1、

作用：替代jsp页面中的表达式脚本在jsp页面中进行数据的输出

EL表达式比jsp输出脚本简洁

![image-20200801092423573](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801092423573.png)

格式：${表达式}

在输出null时，输出空



2、EL 表达式搜索域数据的顺序

当四个搜索域中都有相同的key数据时，搜索 顺序为从小到大：

pageContext==>rquest==>session==>application



3、运算符

![image-20200801103442830](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801103442830.png)

![image-20200801103507146](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801103507146.png)

![image-20200801103720784](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801103720784.png)



4、empty运算

值为null、空串、集合元素个数为0时，返回true；

例：<%

​                 request.setAttribute("emptyNull",nulll)

​         %>

![image-20200801104145147](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801104145147.png)

${empty emptyNull}<br/>  返回true



5、三元运算

exper?  a:b



6、特殊运算

![image-20200801105129127](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801105129127.png)

**中括号[]加单引号‘’或双引号“”**



7、EL表达式中的11个隐含对象

![image-20200801105759299](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801105759299.png)



pageContext,可以获取jsp的九大内置对象:用request举例

![image-20200801110525912](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801110525912.png)

![image-20200801110508070](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801110508070.png)

param/paraValues

![image-20200801111004944](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801111004944.png)

![image-20200801111217569](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801111217569.png)

![image-20200801111524715](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801111524715.png)

![image-20200801111550535](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801111550535.png)







# 二、JSTL标签库

JSP Standard Tag Library  JSP标准标签库

EL表达式主要是为了替换jsp中的表达式脚本；

JSTL标签库是为了替换代码脚本

1、组成

![image-20200801111819580](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801111819580.png)



2、使用

![image-20200801112034211](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801112034211.png)

①导入jstl的jar包

②使用taglib置零引入标签库



**a.使用set设置值**

![image-20200801112606731](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801112606731.png)

page 改为request运行

**b. if标签**

![image-20200801112835351](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801112835351.png)



c. < c:choose >   < c:when>   < c:otherwise>

![image-20200801113226789](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801113226789.png)

when的父标签只能为choose



d.< c: forEach >

![image-20200801113951476](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801113951476.png)



![image-20200801114307040](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200801114307040.png)







