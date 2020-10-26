#### 1、javascript中特殊的值

undefined：未定义，所有js变量未赋初始值的时候，默认为undefined；

null：空值

NaN：Not a Number，非数字非数值,  1*a==NaN



#### 2、函数

typeof();



#### 3、关系运算符

== ：比数值

===：除了比较数值，还要比较类型



#### 4、逻辑运算

所有的变量都可以作为boolean类型的变量

0、null、undefined、“ ”  （空串）都是false

&&运算：

​         都为真，返回第二个表达式的值；

​         任意为假，返回第一个为假的值；

||运算：

​         全为假：返回最后一个的值；

​         只有一个微针，返回真的值



#### 5、数组

var 数组名=[];   长度可变、类型可变；自动扩容

var 数组名=[1,2]；



#### 6、函数

①

function 函数名（形参列表){

函数体

}

**函数调用才会执行；

**返回值直接return；

②

var 函数名=function(形参列表){函数体}

**重载会直接覆盖

arguments：表示参数



#### 7、自定义对象

①Object形式的自定义对象

var 变量名 =  new Object();

变量名.属性名= 值；

变量名.函数名=function();

②{}形式的自定义对象

var 变量名={

属性名：值，

属性名：值，

函数名：function(){}

}；



#### 8、js中的事件

![image-20200729160109104](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729160109104.png)



事件注册：动态、静态

![image-20200729160230819](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729160230819.png)



①onload事件：

​    静态：写完之后引用

<img src="C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729160630060.png" alt="image-20200729160630060" style="zoom:80%;" />

​    动态：window.onload=function(){}



②onclick事件

静态

<button onclick="onclickFun()"></button>

动态

window.onload=function(){

var btnObj=document.getElementById("id101");

btnObj.onclick=function(){

函数体；

}

}

<button id="id101"></button>



③onblur失去焦点事件

静态：function(){

console.log("静态，console为向控制台输出")

}

动态：

window.onload = function(){

var a = document.getElementId("id");

a.onblur(){

函数体；

}

}

④onchange内容发生改变事件

静态：

![image-20200729162034135](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729162034135.png)

动态：





⑤onsubmit表单提交事件

return false 可以阻止表单提交





#### 9、DOM模型

Document Object Model

![image-20200729162934079](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729162934079.png)



![image-20200729163055949](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729163055949.png)

例子：

![image-20200729164302277](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729164302277.png)



正则表达式：

var patt = new RegExp("e");

//var patt=/e/;

//var pstt=/[abc]/;

//var pstt=/[a-z]/;

//var pstt=/\w/;  是否包含字母、数字、下划线

var str = "abcd";

alert(patt.test(str));

![image-20200729165355486](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729165355486.png)

![image-20200729165448457](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729165448457.png)





10、常用方法

document.getElementById()；

document.getElementByName();

document.getElementByTagName();



11、节点的常用属性和方法





















