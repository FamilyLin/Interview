##### 1、连接数据库：

方式一：

![image-20200805232810513](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200805232810513.png)



方式二：

![image-20200805233157825](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200805233157825.png)



方式三：

![image-20200805233431824](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200805233431824.png)



方式四：

![image-20200805233748333](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200805233748333.png)



**方式五**：

![image-20200805234212161](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200805234212161.png)

优点：

①实现了数据（jdbc.properties）和代码的分离

②修改配置文件，避免了程序程序打包



//实现和数据库的连接

public void testInsert（） throws Exception{

//1.读取文件内容信息

​    InputStream is = ClassLoader.getSystemClassLoader.getResourceAsStream(jdbc.properties);

Properties pros = new Properties();

String user = pros.getProperty("user");

String password = pros.getProperty("password");

String url = pros.getProperty("url");

String driverClass = pros.getProperty("driverClass");

//2.加载驱动

Class.forName(driverClass);

//3.获取连接

Connection **conn** = DriverManager.getConnection(url,user,password);

return conn;

}

![image-20200806133114534](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200806133114534.png)

总结：JDBC的使用

![image-20200806134227492](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200806134227492.png)



sql语句的执行：execute();

执行并返回结果集：executeQuery();



##### 2、PrepareStatement和Statement的区别

①PreparementStatement解决了sql注入问题

②PreparementStatement可以操作Blob类型的数据

③PreparementStatement可以预编译，实现批量操作

a.利用Batch攒sql-----------b.不允许自动提交--jdbc33

需要在url后加语句：？rewriteBatchedStatements=true

![image-20200806211920897](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200806211920897.png)





##### 3、事务

①取消自动提交：conn.setAutoCommit(false);

②设置事务：try{取消自动提交-----提交数据}

​                     catch{------回滚}

③ACID属性：Atomicity

​                        Consistency

​                        Isolation         

​                        Durability

④获取隔离级别：conn.getTransactionIsolation()

​    设置隔离级别：conn.setTransactionIsolation()

​     隔离级别：

​             读未提交；    read-uncomitted

​             不可重复读；read-committed

​             可重复读；    repeatable-read

​             串行化           serializable



###### 4、DAO

①BaseDao：抽象类

②XXXXDao：接口



###### 5、数据库连接池

提高程序的响应速度，降低资源的消耗

①C3P0  用.xml文件存储配置信息

②DBCP  用.properties文件存储配置信息

③Druid   用.properties文件存储配置信息

配置文件：

`url=hdbc:mysql://localhost:3306/test`

`username=root`

`password=`

`driverClassName=com.mysql.hdbc.Driver`

使用代码：

`private static DataSource source;`

`static{`

​     `Properties pros = new Properties();`

​     `FileInputStream is = new FileInputStream(new File("src/druid.properties"));`

​     `pros.load(is);`

​      `source = BasicDataSourceFactory.createDataSource(pros);`

`}`

`public static Connection getConnection() throws Exception{`

​          `Connection conn = source.getConnection();`

​          `return conn;`

`}`



6、反射

获取运行时类的对象、属性、方法