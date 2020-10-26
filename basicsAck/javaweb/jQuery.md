jQuery

JavaScript & Query

1、导入jQuery库

src

2、$是一个函数，表示jQuery

3、怎样为按钮添加点击响应函数

①使用jQuery查询到标签函数

②使用标签对象.dick(function(){})

![image-20200729180124225](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729180124225.png)



4、核心函数$

①传入参数为函数时，表示页面加载完成之后，自动调用

②传入HTML字符串，会创建这个html标签对象

③传入选择器字符串

$("#id");    id选择器，根据ID查询标签对象

$("标签名：div.span");   标签名选择器，根据指定的标签名查询标签对象

$(".class")；  类型选择器，根据class属性查询对象

④传入参数为DOM对象，包装为jQuery对象



5、怎样区分DOM对象和jQuery对象

DOM对象：[object HTML标签名Element]

jQuery对象：[object Object]



6、jQuery对象本质

DOM对象数组 + jQuery提供的一系列功能函数

7、jQuery对象和DOM对象的区别

jQuery对象不能和DOM对象互相使用属性和方法；

8、DOM对象和jQuery对象互转

①DOM对象转化为jQuery对象

​         先有DOM对象；

​         $(DOM对象)；

②jQuery对象转化为DOM对象

​        先有jQuery对象；

​        jQuery对象[下标]取出相应的DOM对象；

​         





9、jQuery属性

![image-20200729201157105](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729201157105.png)

不传参数是获取；传入参数是设置。

![image-20200729202327258](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200729202327258.png)

attr();获取属性,不推荐操作checked/readOnly()/selected/disabled

attr(a,b);设置属性a 为 b

prop();推荐只操作checked/readOnly()/selected/disabled



10、DOM的增删改

a.appendTo(b);    添加到b后

a.prependTo(b);      添加到b前

a.insertAfter(b);

a.insertBefore(b);

a.replaceWith(b);   b替换a

a.replaeceAll(b);     a替换掉所有的b

a.remove()     删除a标签

a.empty();    清除a内的内容





11、jQuery增删

![image-20200730132441677](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730132441677.png)



**12、原生js和jQuery加载的区别**

jQuery的页面加载完之后是浏览器的内核解析完页面的标签、创建好DOM对象之后就会马上执行；

原生js的页面加载完成之后，除了要等浏览器内核解析完标签创建好DOM对象，还要等标签显示时需要的内容加载完成。

顺序：jQuery页面加载完成之后执行

​           原生js的页面加载完之后再执行

执行次数：

原生js的页面加载完成之后，只会执行最后一次的赋值函数

jQuery的页面记在完成之后，全部把注册的function函数，一次顺序全部执行。





![image-20200730144658558](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730144658558.png)

![image-20200730145138550](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730145138550.png)



![image-20200730145606696](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200730145606696.png)



















