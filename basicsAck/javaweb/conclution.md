1、HTML（Hyper Text Markup Language）

超文本标记语言



2、超链接

《a href="path"》text《/a》

其他情况下链接用src="path"



3、DOM模型（Document Object Model）



4、jQuery ( javaScript + Query)

核心函数：$()

$(function（）{       //表示页面加载完成之后

​        var $id = $("#id");

$id.click(function(){

​             alert("jQuery的单击事件")；  

​      });

})；



5、XML可扩展的标记性语言

需要dom4j的jar包解析xml代码



6、JavaWeb的三大组件：

servlet程序 、Filter过滤器、Listener监听器



7、JSP（Java Server Pages）

解决动态生成HTML文档的技术

《%！   声明脚本   %》

《%=  表达式脚本 %》

《%   代码块脚本  %》

《%--       注释     --%》



8、JSP中的九大内置对象

request对象

response对象

pageContext对象    当前页面的上下文对象

session对象

exception 对象

application对象  ServletContext对象实例

config对象            ServletConfig对象实例

out 对象

page对象    表示当前Servlet对象实例（可以直接用this）



9、JSP的四大域对象

pageContext       保存数据在同一个jsp页面中使用

request                保存数据在同一个request对象中使用

session                 保存数据在一个会话中使用

application（ServletContext）      ServletContext对象



10、EL表达式（Expression Language）

主要代替jsp页面中的表达式脚本在jsp页面中进行数据的输出