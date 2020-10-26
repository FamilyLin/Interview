# Spring

Spring; Springmvc; Springboot; Springcloud

核心技术：IOC、AOP

依赖：ClassA中使用ClassB中的属性或方法，叫做A依赖于B

##### 一、IoC控制反转（Inversion of Control）

控制反转；将对象的创建、赋值、管理工作都交给代码之外的容器实现，对象的创建由其他外部资源完成。

控制：创建对象，对象的属性赋值，对象之间的关系管理

反转：把原来的开发人员管理、创建对象的权限转移给代码之外的容器实现，由容器代替开发人员管理对象。

容器：服务器软件、框架（Spring）

正转：由开发人员在代码中，使用new构造方法创建对象



###### 1、Ioc目的

减少对代码的改动，实现不同的功能；实现解耦合

###### 2、体现

servlet

①创建类继承HttpServlet

②web.xml中配置servlet



###### 3、技术实现：DI

（Dependency Injection: 依赖注入）

①只需要在程序中提供要使用的对象名称就可以，至于对象如何在容器中创建、赋值、查找都由容器内部实现

②Spring使用DI实现IoC功能，底层创建对象使用反射机制



###### 4、Spring使用步骤

①创建maven项目

②加入maven的依赖

​     Spring的依赖，5.2.5版本

​     Junit依赖

③创建类（接口|实现类）

④创建Spring的配置文件（<bean>）

⑤测试



###### 5、spring创建对象步骤（基于.XML 文件的DI实现）

```
//使用spring创建对象
//1.指定spring的配置文件
        String config = "beans.xml";
//2.创建spring容器的对象：ApplicationContext； 此时会创建配置文件中所有对象
//ApplicationContext表示spring容器，通过容器获取对象
//ClassPathXmlApplicationContext表示从类路径中加载spring配置文件
        ApplicationContext ac= new ClassPathXmlApplicationContext(config);
// 从容器中获取某个对象，调用对象的方法
//getBean("配置文件中的bean的id值)
        SomeService service = (SomeService)ac.getBean("someService");
// 使用spring对象
        service.doSome();
```



###### 6、基于XML的DI的语法分类

①set注入：spring调用类的set方法，在set方法可以实现属性的赋值

②构造注入：spring调用类的有参数构造方法，创建对象，在构造方法中完成赋值。



###### 7、set注入(.XML文件中进行设置)

调用类的无参构造方法

①简单类型的set注入(基本数据类型+String)

<bean id = "xx" calss="yy">

​        <property name="属性名" value="属性值"/>

​       <property name="name" value="zhangsan"/>

​       <property name="age" value="18"/>

​        <property .............../>

</bean>

②引用类型的set注入

<bean id="xxx" class="yyy">

​       <property name="name" value="lizi"/>

​       <property name="age" value="18"/>

​       <!---引用类型--->

​       <property name="school" ref="mySchool"/>      

</bean>

<!--声明school对象-->

<bean id="mySchool" class="包名.school">

​          <property name="name" value="TJU"/>

​          <property name="address" value="TJ"/>

</bean>



###### 8、构造注入

调用类的有参构造方法

需要使用<constructor-args>标签，一个标签表示构造方法中的一个参数；

<constructor-arg>标签属性：

​          name：表示构造方法的形参名

​          index：表示构造方法的参数位置，0/1/2/3.。。。

​          valule：构造方法的形参类型是简单类型

​          ref：形参类型是引用类型

<bean id="xxx" class="yyy">

 <constructor-arg name="myname" valule="s" />

</bean>



9、引用类型的自动注入

①byName(按名称注入)：java类中引用类型的属性名和spring容器中（配置文件）<bean>中的id名称一样，且数据类型是一致的，这样的容器中的bean，spring能够赋值给引用类型(aa一定要是xx中的引用类型名称)

<bean id="xx" class="yy" autowire="byName">

​     <property name="name" value="lisi" />

</bean>

<bean id="aa" class="bb">

​     <property name="name" value="cc" />

</bean>

②byType(按类型注入)；java类中引用类型的数据类型和spring容器中的<bean>得class属性是同源关系的，这样的bean能够赋值给引用类型

同源关系：{

a、java类中的引用类型的数据类型和bean中class的值一样

b、java类中的引用类型的数据类型和bean中class的值父子类关系

c、java类中的引用类型的数据类型和bean中class的值为接口和实现类关系}

<bean id="xx" class="yy" autowire="byType">

​     <property name="name" value="lisi" />

</bean>

<bean id="aa" class="yyy">

​     <property name="name" value="school" />

</bean>



9、多配置文件

①主配置文件：(包含关系配置文件)

<import resource="其他配置文件的路径"/>

例：

<bean>

<import resource="classpath:bao1/s1.xml"/>

<import resource="classpath:bao1/s2.xml"/>

</bean>

使用通配符(*)

<import resource="classpath:bao1/asd-*.xml"/>



###### 9、基于注解的DI

通过注解完成java对象的创建、属性赋值

使用步骤：

①加入maven依赖：spring-context

②在类中加入spring的注解

③在spring的配置文件中加入一个组件扫描器的标签，说明注解在项目中的位置

<context:component-scan base-package="包名"/>



###### 10、常用注解

①@Component： 创建对象，等于<bean>的功能

​                                 属性：value对象的名称，bean中的id值

​                                  位置：类的上方

还可以省略value：@Component("xxxx")

或直接省略（“ ”）

例子：@Component(value="xxx")

​           需要在xml文件中配置组件扫描器

​           <context:component-scan base-package="包名"/>

指定多个包：使用多个扫描器

​                       使用分隔符（；或，）

​                       指定父包



②@Respotory（持久层）

放在Dao实现类上面，表示创建dao对象，访问数据库

③@Service（业务层）

放在service的实现类上面，表示创建service对象，做业务处理，有事务等功能

④@Controller（控制器上面）

放在控制器类的上面，创建控制器对象，接收用户提交的参数，显示请求的处理结果

以上三个注解的使用语法和@Component一样，可以给项目对象分层

⑤@Value（简单类型的属性赋值）

​                    value是String类型的，表示简单类型的属性值

​                    在属性定义的上面(常用)

​                    在set方法的上面（不常用）

例子：@value(value="zhangsan")

​              private String name;

⑥@Autowired（引用类型赋值）

支持byName, byType; 

​       默认使用byType

​           在属性定义的上面，无需set方法

​      显式声明使用byName

​           @Autowired

​            @Qualifier("idName")



⑦@Resource(来自JDK)

支持byName、byType; 默认byName

如果byName自动注入失败，使用byType



###### 11、总结：

经常修改使用基于.XML 配置文件的DI

不经常修改使用基于注解的DI，只需要配置文件指定包即可

IOC实现业务对象之间的解耦合，如service和dao对象之间的解耦合



##### 二、AOP面向切面编程（Aspect Orient Programming）

###### 1、动态代理

可以在程序的执行过程中，创建代理对象

通过代理对象执行方法，给目标类的方法增加额外的功能

**jdk动态代理实现步骤：**

​    ①创建目标类：SomeServiceImpl目标类，给他的doSome，doOther方法增加输出时间。事务；

​    ②创建**InvocationHandler**接口的实现类，在这个类实现给目标方法增加功能；

​    ③使用jdk中类**Proxy**，创建代理对象，实现创建对象的能力

jdk动态代理要求目标类必须实现接口



**cglib动态代理：**

第三方工具库，创建代理对象，原理是继承。通过继承目标类，创建子类，子类就是代理对象。要求目标类不能是final，方法也不能是final的



**动态代理的作用**

①在不改变源码的情况下，增加功能

②减少代码重复

③解耦合



###### 2、AOP

AOP是动态代理的规范化

面向切面编程：

​          ①找出切面

​          ②安排切面的执行时间

​          ③安排切面的执行位置

**术语：**

​    ①**aspect**：日志、事务、统计信息、参数检查、权限验证

​    ②JoinPoint：连接点，连接业务方法和切面的位置

​    ③**Pointcut**：切入点，连接点方法的集合

​    ④目标对象：被增加功能的类

​    ⑤**Advice**：通知，切面执行的时间

**切面三个关键要素**

   ①切面的功能

   ②切面的执行位置

   ③切面的执行时间



###### 3、AOP的实现框架

①spring：主要在事务处理时使用，但是很少用

②aspectJ：开源的AOP专门框架，被spring集成

​        实现方法 ：a.使用xml配置文件

​                            b.使用注解



###### 4、aspectJ框架的使用

①切面的执行时间：Advice

​    在aspectJ中使用注解表示

​                         a. @Before

​                         b. @AfterReturning

​                         c. @Around

​                         d. @AfterThrowing

​                         e. @After

②切面的执行位置：切入点表达式

execution(modifiers-pattern? ret-type-pattern
declaring-type-pattern?name-pattern(param-pattern)
throws-pattern?)  

execution(访问权限 **方法返回值** **方法声明(参数)** 异常类型)  

**③使用步骤：**

​     a. 创建maven项目

​     b.加入依赖：

​                           spring依赖

​                           aspectJ依赖

​                           junit单元测试

​    c.创建目标类：接口和实现类

​    d.**创建切面类**：普通类

​        在类的上面加入：@Aspect

​        在类中定义方法，方法就是切面要执行的功能代码

​        在方法的上面加入aspectJ中的通知注解，如：@Before

​        有需要指定**切入点表达式execution()**

​    e.**创建spring的配置文件**：声明对象，把对象交给容器统一管理，可以使用注解或.XML文件

​         声明目标对象

​         声明切面类对象

​         声明aspectJ框架中的自动代理生成器标签：用来完成代理对象的自动创建功能

​     f.创建测试类，从spring容器中获取目标对象（实际就是代理对象）通过代理执行方法，实现aop的功能增强



###### 5、AspectJ框架使用举例

例：

①创建目标类（接口及实现类）

 ![image-20200808191232904](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808191232904.png)

②实现目标类

![image-20200808191558879](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808191558879.png)

③创建切面类，在普通类前加@Aspect

​                            在方法前加通知注解

![image-20200808191117665](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808191117665.png)

④配置.xml文件

![image-20200808190846004](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808190846004.png)

⑤测试

![image-20200808191034645](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808191034645.png)



![image-20200808193824763](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808193824763.png)



###### 6、通知方法中的参数

在切面方法中，参数的类型是指定的

①JoinPoint   必须是形参列表中的第一个

②Object

③Exception

###### 7、aspectJ的注解：

**① @Before**

目标方法之前调用

![image-20200808191117665](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808191117665.png)

**②@AfterReturning**

目标方法返回值之后，对返回值进行功能处理；但是无法对返回值进行修改

![image-20200808205218165](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808205218165.png)

**③@Around**

可以目标方法前后都进行功能增强，可以改变目标方法最终调用结果；适用于事务处理

![image-20200808210623186](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808210623186.png)

**④@AfterThrowing**： 发生异常后执行

@AfterThrowing(value="" , throwing="ex")

**⑤@After**   最终通知，一定会被执行  （==finally）

一般做资源清除工作

**⑥@Pointcut**

如果有多个切入点表达式是重复的，可以复用，声明之后，可以被其他注解调用：

@Pointcut(value = "execution(* *..Impl.do(..))")

public void mypt(){无需代码}



@Before(value="mypt()")  // 调用上边Pointcut

public void xxx(){}





###### 8、CGlib动态代理

①如果目标类无接口，默认使用CGLib动态代理

②有接口时，也可以使用CGLib动态代理：

​      需要在.xml文件中修改：

​        <aop: aspectj-autoproxy proxy-target-class="true"/>



##### 三、MyBatis框架与spring框架集成

###### 1、MyBatista使用步骤

①定义dao接口，   studentDao

②定义mapper文件      studentDao.xml

③定义mybatis的主配置文件  mybatis.xml

④创建dao的代理对象

studentDao dao = SqlSession.getMapper(studentDao.class);

List<Student> students = dao.selectStudents();

###### 2、MyBatis和Spring集成

①新建maven对象

②加入maven依赖

- spring依赖
- mybatis依赖
- mysql驱动
- spring的事务依赖
- mybatis和spring集成的依赖：mybatis官方体用的，用来在spring项目中创建mybatis的SqlSessionFactory    dao对象

③创建实体类

④创建dao接口和mapper文件

⑤创建mybatis主配置文件

⑥创建Service接口和实现类，属性是dao

⑦创建spring的配置文件：声明mybatis的对象交给spring创建

applicationContext.xml配置：

- 数据源------druid

![image-20200808224509286](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808224509286.png)

- SqlSessionFactory

![image-20200808224439700](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808224439700.png)

- Dao对象

![image-20200808225110351](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808225110351.png)

- 声明自定义的service
- ![image-20200808225727512](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200808225727512.png)

⑧创建测试类，获取Service对象，通过service调用dao

完成数据库的访问



##### 四、spring的事务处理

###### 1、事务

一组sql语句或操作，成功：全部成功；失败：任意一条失败

###### 2、事务位置

service类的业务方法上，因为业务方法需要调用多个dao方法，执行多个sql语句

###### 3、spring处理事务

提供一种处理事务的模型，使用统一步骤，完成多种不同的数据库访问技术的事务处理

①**事务管理器是一个接口和多个实现类**

接口：PlatformTransactionManager

访问mybatis需要使用spring创建好的实现类：

​                                     DataSourceTransactionManager

<bean id="xxx" class="..DataSourceTransactionManager">



②事务的传播行为：共7种，掌握三种

   PROPAGATION_REQUIRED:必须有事务，没有就创建

   PROPAGATION_REQIRES_NEW：可有可无

   PROPAGATION_SUPPORTED：总新建

③事务处理的时间：

​    a.执行成功：commit

​    b.运行时异常：rollback

​    c.受查异常（非运行时异常）：默认commit



###### 4、使用注解进行事务处理的过程（小项目）

@Transactional注解增加事务，需放在public方法上面

①需要声明事务管理器对象

<bean id="xx" class="DataSourceTransactionManager">

![image-20200809111254457](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200809111254457.png)

![image-20200809111434337](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200809111434337.png)

②在方法上面加入@Transactional

可以单写一个@Transactional，也可以更改默认设置，

下图是默认设置

![image-20200809111607460](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200809111607460.png)

③开启事务注解驱动（不用自己写）

​       @Around("增加的事务功能的业务方法名称")

​       Object myAround(){

​         自动开启事务

​          try{

​          运行正常；

​          commit();  

​          }

​          catch{

​           roolback();  

​          }

​          }



###### 5、使用AspectJ进行事务处理的过程（大项目）

实现步骤：都是在XML配置文件中实现

①使用aspectJ框架，需要加入依赖

②声明事务管理器对象

<bean id="xx" class="DataSourceTransactionManager">

![image-20200809135839890](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200809135839890.png)

③声明方法需要的事务类型（配置方法的事务属性（隔离级别、传播行为、超时））

![image-20200809140125692](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200809140125692.png)

![image-20200809140405895](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200809140405895.png)

④配置aop：指定哪些类要创建代理

![image-20200809140853225](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200809140853225.png)



注册监听器

![image-20200809143633415](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200809143633415.png)



