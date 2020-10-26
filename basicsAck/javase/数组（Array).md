##### 一、数组（Array)

1、理解：多个相同类型数据按一定顺序排列的集合

2、相关概念： 数组名、索引、元素、长度

 3、数组属于引用类型，数组的元素可以是基本类型或引用类型

4、连续

5、长度一旦确定，不可修改

6、数组的使用

![image-20200715223910658](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200715223910658.png)

①静态初始化（元素赋值）、动态初始化（不赋值）

②arr[index] = a;

③arr.length;

④for循环遍历

⑤整型（byte、short、int、long）: 0

​    浮点型（flout、double）：0.0

​    char型： ‘0‘（ASCII）

​    boolean型： false

​    引用数据类型：null

⑥ 栈（stack）：局部变量

​     堆（heap）：对象、数组

将heap的首地址值赋给stack中的局部变量



7、二维数组

![image-20200715232506757](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200715232506757.png)

①静态、

​    动态arr[3] [2];表示arr[3]中的元素，每一个有2个元素 

⑤![image-20200716190128489](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200716190128489.png)







##### 二、数组中的常见算法

###### 1、杨辉三角形

![image-20200716191030941](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200716191030941.png)

###### 2、回形数

（剑指offer中有类似）

###### 3、数组的复制

①arr2 = arr1; //直接把arr1地址给arr2，修改arr2，同时会修改arr1

②arr2 = new int[l]; 循环赋值；//实现真正的复制

###### 4、数组的反转

定义临时变量

String.reverse();

###### 5、数组中的查找

①线性查找，for循环遍历, equals();

②二分法查找，适用于有序数组

![image-20200716195333889](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200716195333889.png)

###### 6、排序算法

时间复杂度：分析关键字的比较次数和记录的移动次数

空间复杂度：分析排序算法需要用到的辅助内存

稳定性：若两个记录A和B的关键字值相等，但排序后A、B的先后次序保持不变，则称这种排序算法是稳定的。

内部排序：不需要借助于外部存储设备

外部排序：需要借助于外部存储设备

①冒泡排序：

依次对相邻两个进行排序，需要遍历（n-1）次

![image-20200716201332215](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200716201332215.png)

②快速排序

![image-20200716201409970](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200716201409970.png)

![image-20200716202211281](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200716202211281.png)



![image-20200716202327047](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200716202327047.png)

![image-20200716202350046](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200716202350046.png)

##### 三、操作数组的工具类

![image-20200716202720985](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200716202720985.png)

toString(): 利用StringBuilder() + append()

sort(): 快排

##### 四、常见异常

1、ArrayIndexOutOfBoundsException（角标越界）

2、NullPointerException（空指针异常）:找不到地址











