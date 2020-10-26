# Redis

##### 1、什么是NoSQL

NoSQL == Not Only SQL

NoSQL：非关系型数据库：键值对

MySQL：关系型数据库：表格，行，列

##### 2、为什么要使用NoSQL

- 用户的个人信息，社交网络，地理位置，用户自己产生的数据，用户日志等等爆发式增长；传统的关系型数据库如MySQL已经不能适用所有场景，NoSQL可以很好地处理以上的问题，例如使用redis缓存中间件，尽可能避免了数据库被打崩的出现
- Redis为什么单线程还这么快：

  - redis将所有的数据全部放在内存中，所以使用单线程去操作就是最高的（多线程CPU需要上下文切换，耗时）
  - 对于内存系统来说，没有上下文的切换，效率比较高，多次读写都是在一个CPU上完成的，在内存情况下，是最佳方案

##### 3、NoSQL特点

- 方便扩展（数据之间没有关系）
- 大数据量高性能（Redis一秒写8万次，读11万次）
- 数据类型是多样的（不需要事先设计数据库）
- 传统的RDBMS和NoSQL
  - 传统的RDBMS
    - 结构化组织
    - 数据和关系都存在单独的表中
    - 严格的一致性
    - 基础的事务
  - NoSQL
    - 不仅仅是数据
    - 没有固定的查询语句
    - 键值对存储、列存储、文档存储、图形数据库（社交关系）
    - 最终一致性
    - 高性能、高可扩、高可用

##### 4、NoSQL的四大分类

- KV键值对：
  - 新浪：Redis
  - 美团：Redis+Tair
- 文档型数据库
  - MongoDB
    - 基于分布式文件存储的数据库，主要用来处理大量的文档
    - 介于关系型数据库和非关系型数据库中间的产品，MongoDB是非关系型数据库中功能最丰富，最像关系型数据库的
  - ConthDB
- 列存储数据库
  - HBase
  - 分布式的文件系统
- 图形数据库
  - 用来存储社交网络、推荐系统

![image-20200818092928524](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818092928524.png)



##### 5、Readis（**Re**mote **Di**ctionary **S**erver)

​      **远程字典服务**

1. 开源的、使用C语言编写、支持网络、基于内存可持久化的日志型、Key-Value数据库，并提供多种语言的API
2. 会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件，并在此基础上实现master-slave(主从)同步，也称为结构化数据库。
3. 应用
   - 内存存储、持久化，内存中是断电即失，持久化很重要（rdb/aof）
   - 效率高，可以用于高速缓存
   - 发布订阅系统
   - 地图信息分析
   - 计时器、计数器（浏览量）
4. 特性
   - 多样的数据类型
   - 持久化
   - 集群
   - 事务
5. ![image-20200818104318748](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818104318748.png)



##### 6、Redis在Linux上的使用

1. windows环境下载安装包：redis-6.0.6.tar.gz

2. 将tar.gz通过Xftp传送到linux服务器

3. 启动Xshell连接linux服务器

4. 解压tar.gz文件

   ```redis
   tar -zxvf redis-6.0.6.tar.gz
   ```

5. ![image-20200818131825890](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818131825890.png)

6. 进入解压后的文件，可以看到redis.config配置文件

7. ![image-20200818131946371](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818131946371.png)

8. ![image-20200818135740215](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818135740215.png)

9. make

10. 默认安装路径：/usr/local/bin

11. 将配置文件复制

12. redis不是默认后台启动，修改设置

13. ![image-20200818140351750](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818140351750.png) 改为yes

14. 启动 redis
    - **需要进入目录:   cd /usr/local/bin**
    - **redis-server kconfig/redis.conf**
    - **redis-cli -p 6379**
    - set name ZJL
    - get name
    - keys *   //查看key

15. ![image-20200818140601987](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818140601987.png)

16. shutdown    //关闭

17. exit              //退出



##### 7、redis性能测试

**redis-benchmark**

```redis
redis-server kconfig/redis.conf
redis-cli -p 6379
redis-benchmark -h localhost -p 6379 -c 100 -n 10000
```

![image-20200818143810688](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818143810688.png)





##### 8、基础知识

- 有16个数据库，默认使用第0个；可以使用select切换

  ```
  select 3  //选择第4个数据库
  ```

- 查看数据库大小

  ```
  DBSIZE
  ```

- 查看数据库所有的key

  ```
  keys *
  ```

- 清空数据库

  ```
  flushdb
  ```

- 清空所有数据库

  ```
  flushall
  ```

- redis 是单线程的，基于内存操作，CPU不是Redis的瓶颈，Redis的瓶颈是机器的内存和网络带宽

- redis 是C语言写的，不比Memecache差

- 高性能的服务器不一定是多线程的

- 多线程（需要CPU的切换）不一定比单线程效率高

- Redis为什么单线程还这么快：

  - redis将所有的数据全部放在内存中，所以使用单线程去操作就是效率最高的（多线程CPU需要上下文切换，耗时）
  - 对于内存系统来说，没有上下文的切换，效率比较高，多次读写都是在一个CPU上完成的，在内存情况下，是最佳方案



##### 9、5大数据类型

> String : 作为常规的key-value对使用，例如粉丝数
>
> list：消息队列
>
> set：不重复的集合，统计不同用户访问量
>
> hash：key+map，可用于存储用户信息：
>
> ​            id +{name+ZJL};  id + {age + 26}
>
> Zset：排行榜，具有优先级的消息队列

```
Redis 是一个开源的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件MQ。支持多种类型的数据结构，如：字符串(String) , 散列（hashes）， 列表（lists)，集合（sets), 有序结合(sourted sets) 与范围查询 bitmaps，hyperloglogs 和地理空间（geospatial）索引半径查询。
Redis内置了复制（replication），LUA脚本（Lua scripting），LRU驱动事件（LRU eviction），事务（transactions) 和不同级别的磁盘持久化（persistence),并通过redis哨兵（sentinel）和自动分区（Cluster)提供高可用性（high availability)
```

- Redis-Key常用命令

  - ```
    exists name  //查看name这个key是否存在
    move name 1 //从当前数据库移除，1代表当前数据库
    EXPIRE name 10 //设置10秒后过期
    ttl name //查看还剩多长时间
    type name//查看key的类型
    ```

1. ###### String

   - ```
     append key1  “hello"  //在key1对应值后追加，不存在则新建
     strlen key1       //获取字符串长度
     
     set key1 0        //设置初始值为0
     incr key1         //每次访问加1
     decr  key1        //每次访问减1
     incrby key1 10    //每次访问加10
     decrby key1 10    //每次访问减10
     
     getrange key1 0 3 //查看0-3的字符
     getrange key1 0 -1//查看所有字符                           //==get key1
     setrange key1 2 xx //将第3个后面修改，替换
     
     setex key2 30 "hello" //设置30s后过期
     setnx key3 "hi"     //不存在新建，存在无                     //法覆盖
     
     mset k1 v1 k2 v2 k3 v3 //设置多个
     mget k1 k2 k3          //得到多个
     
     msetnx k1 v1 k4 v4  //设置失败，原子性
     
     ```

   - 对象

     ```
     set user:1{name:ZJL,age:26}
     //设置一个user:1对象，值为json字符来保存
     
     mset user:1:name ZJL user:1:age 2
     mget user:1:name user:1:age
     //等价
     ```

     

   - ```
     //先get再set
     getset key1 v1
     ```

   - String使用场景：value除了字符串还可以是数字

     - 计数器
     - 统计多单位的数量
     - 粉丝数
     - 对象缓存存储

2. ###### List

   - 所有list的命令都以"L"开头（大小写不敏感）

     ```
     lpush key1 v1   //插入到列表的头部
     Rpush key1 v2    //插入到列表的尾部
     lrange key1 0 1  
     
     Lpop key1 //移除列表的第一个元素
     Rpop key2 //移除列表的最后一个元素
     
     Lindex key1 1 //根据下标获取值
     
     Llen key1     //返回列表长度
     
     Lrem key1 2 v2 // 移除2个v2
     
     Ltrim key1 1 2 //截取其中的第2、3个元素
     
     rpoplpush key1 key2//将key1中最后一个元素                    //移到key2中
     lset key1 0 v2//在key1存在的情况下，将下标               //为0的元素更新为v2
     
     Linsert key1 before v2 v3 //在v2前插入v3
     Linsert key1 after v2 v3 //在v2后插入v3
     
     ```

   - list实际是一个链表

   - 如果key不存在，则新建

   - 两边插入或改动，效率较高；中间插入，效率较低

3. ###### Set

   - set中的值无序不重复

   - set中的命令以S开头

   - ```
     sadd myset v1        //添加元素
     Smembers myset       //查看所有元素
     Sismember myset v1   //判断是否存在v1
                      //存在返回1，不存在返回0
     
     scard myset   //获取set中的元素个数
     srem myset v1 //移除set中的指定元素
     
     Srandmember myset      //随机抽取一个
     Srandmember myset 2    //随机抽取两个
     
     spop myset     //随机移除元素
     
     smove myset myset2 v1  //将指定元素移到另                        //一个set中
     sdiff key1 key2          //差集
     sinter key1 key2         //交集
     sunion key1 key2         //并集
     ```

     

4. ###### Hash

   - 存储map集合 <key-value>对

   - ```
     hset myhash field1 v1
     hget myhash field1
     hmset myhash f1 v1 f2 v2
     hmget myhash f1 f2
     hgetall myhash
     hdel myhash field1 //删除
     hlen myhash //获取键值对数量
     hexists myhash field1//判断指定对是否存在
     hkeys myhash//获取key
     hvals myhash//获取val
     
     hincrby myhash field 1  //增加
     hdecrby myhash field 1  //减小
     ```
     
     

5. ###### Zset（有序集合）

   - 指令以Z开头

   - ```
     zadd myset score key value //score 决定                         //value的优先级
     Zrange myset 0 -1 //所有的元素
     
     Zrangebyscore myset -inf +inf 
     //用score排序输出key
     
     Zrangebyscore myset -inf +inf withscores //由小到大排序并输出key-value
     zrevrange myset 0 -1 //由大到小排序
     
     zrem myset key //删除
     zcard myset //获取集合中的元素
     zcount myset 1 3 //获取指定区间的数量
     
     ```

   - 带权值排序   比如：排行榜



##### 10、3种特殊数据类型

1. **Geospatial 地理位置**

   - 朋友的定位、附近的人、打车距离

   - > 只有6个命令·：
     >
     > - GEOADD：添加 地理位置(经度 纬度)
     > - GEOPOS：获取地理位置
     > - GEODIST：返回两个给定位置间直线距离
     > - GEORADIUS：找附近的人，通过半径查找
     > - GEORADIUSBYMEMBER：找出指定元素周围的元素
     > - GEOHASH：返回一个或多个地点经纬度的一维字符串

   - geoadd China:city  116 34 beijing

   - geopos China:city beijing

   - geodist China:city beijing shanghai   km/可选

   - georadius China:city 116 34 500 km //查找以116 34为中心 半径为500km内的城市

   - georadiusbymember China:city beijing 1000km

   - GEO底层实现原理是Zset，可以通过Zset的命令来操作GEO

2. **Hyperloglog 基数统计**

   - 基数：集合中不重复的数

   - 传统的set保存用户Id，比较麻烦

   - Hyperloglog 可以不用保存id，直接计数

   - 有一定的错误率

   - ```
     PFadd mykey a b c  //添加
     PFCOUNT myket   //统计基数个数
     PFmerge mykey2 mykey1 mykey   //取mykey1 和 mykey并集 到 mykey2中
     
     ```

3. **Bitmap 位图场景**

   - 统计疫情感染人数：0 1 0 0 0 0 

   - 统计用户信息：是否活跃；是否登录

   - 操作二进制位进行记录

   - ```
     setbit sign 0 1 //假设周一打卡
     setbit sign 1 0 //假设周二未打卡
     ....
     getbit sign 1 //查看周二是否打卡
     
     bitcount sign //统计一共的打卡次数
     ```

     

##### 11、事务

1. Redis事务本质：一组命令的集合。一个事务中的所有命令都会被序列化，在事务执行过程中，会按照顺序执行。

2. 事务具有：一次性、顺序性、排他性

3. redis事务没有隔离级别的概念

4. 所有的命令在事务中，并没有直接被执行，只有发起执行命令的时候才会执行

5. redis单条命令保存原子性，但是事务不保证原子性

6. redis的事务：

   - 开启事务(multi)

   - 命令入队（....）

   - 执行事务(exec)

   - 放弃事务（DISCARD）

   - ```
     multi 
     set name zjl
     set age 26
     exec
     ```

7. 异常

   - 编译型异常：事务中所有的命令都不会被执行
   - 运行时异常：事务中的错误命令抛异常，其他命令正常执行

8. 监控：watch

   - 悲观锁：一直加锁
   - 乐观锁：不会上锁；更新数据时，会去判断是否有人修改过这个数据。
     - 获取version
     - 更新的时候比较version

   ```
   //正常执行
   set money 100
   set out 0
   watch money
   multi
   secrby money 20
   incrby out 20
   exec
   
   ```

   - 多线程执行时，使用watch可以当做**乐观锁**操作，一旦事务开始后，数据被另一线程修改，此事务执行失败。

   - ```
     //事务执行失败后，先解锁
     unwatch
     ```

   - 秒杀情况下，可以使用乐观锁



##### 12、Jedis

1. 使用java操作redis需要用到Jedis

2. Redis官方推荐的java连接开发工具，使用java操作Redis的中间件

3. Jedis的使用

   1. 导入对应的依赖

      ![image-20200818205649277](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818205649277.png)

   2. 编码测试

      - 连接数据库
      - 操作命令
      - 断开连接

      ```
      import redis。clients.jedis.Jedis
      public class TestPing{
          psvm(String[] args){
          //新建一个对象，参数为ip/端口
              Jedis jedis = new Jedis("127.0.0.1",6379);
              sout(jedis.ping());
          }
      }
      ```

      

   3. 常用命令

      ![image-20200818210411416](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818210411416.png)

   4. String

      ![image-20200818210552272](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818210552272.png)

   5. list

      ![image-20200818210726351](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818210726351.png)

   6. set

      ![image-20200818210809986](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818210809986.png)

   7. hash

      ![image-20200818210906454](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818210906454.png)

   8. Zset

   

4. 事务

   ![image-20200818211239858](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818211239858.png)



##### 13、SpringBoot集成Redis

redisTemplate.opsForString().----

redisTemplate.opsForlist().----



##### 14、Redis.conf详解

1. 启动的时候，通过Redis.conf 启动

2. 大小写不敏感

3. 网络   

   ```
   bind 127.0.0.1 //绑定的IP
   protected-mode yes //保护模式
   port 6379 //端口号
   ```

4. 通用 General

   ```
   daemonize yes //以守护进程的方式运行，默认是no，需要自己开启为yes
   
   pidfile /var/run/redis_6379.pid //如果以后台的方式运行，需要制定一个pid文件
   ```

   ![image-20200818213532533](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818213532533.png)

5. 快照

   在规定的时间内，执行了多少次操作，则会持久化到文件 .rdb.aof

   ![image-20200818215059694](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818215059694.png)

6. 安全Security

   ![image-20200818215255874](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818215255874.png)

7. 限制 client

   ![image-20200818215430757](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818215430757.png)

8. APPEND ONLY 模式  aof配置

   ![image-20200818215700135](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818215700135.png)



##### 15、Redis持久化

- Redis是内存数据库，如果不将内存中的数据库状态保存到磁盘，那么一旦服务器进程退出，服务器中的数据库状态也会消失，所以Redis提供了持久化功能

1. RDB（Redis DataBase）持久化

   ![image-20200818220524949](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818220524949.png)

   - 在**指定时间间隔内**将内存中的数据集快照写进磁盘，它恢复时是将快照文件直接读到内存里

   - 触发机制：生成dump.rdb文件

     - redis.conf文件中的save设置规则满足，自动触发rdb规则
     - 执行flushall命令，触发rdb规则
     - 退出redis，触发rdb规则

   - 恢复rdb文件

     - 只需要将rdb文件放在 redis 的启动目录就可以，redis启动时，会自动检查dump.rdb并恢复其中的数据

   - 优点

     - 适合大规模数据的恢复
     - 对数据的完整性要求不高

   - 缺点

     - 需要一定的时间间隔进程操作，如果宕机了，最后一次修改的数据就没有了
     - fork进程，会占用一定的内存空间

     

2. AOF(Append Only File)持久化

   - ![image-20200818223052702](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818223052702.png)

   - 将所有命令都记录下来，恢复的时候将所有命令重新执行一遍
   - 以日志的形式来记录每个写操作，只许追加文件但不可以改写文件，redis启动的时候，会读取该文件重新构建数据
   - redis重启的话，就根据日志文件的内容将写指令从前到后执行一次，以完成数据的恢复工作
   - 保存为appendonly.aof文件
   - 默认不开启，默认开启RDB
   - 如果aof文件有错位，redis无法启动，可以用redis-check-aof --fix 修复
   - redis-check-aof --fix appendonly.aof
   - 优点
     - 每一次修改都同步，文件的完整性较好
     - 每秒同步一次，可能会丢失一秒的数据
     - 从不同步，效率较高
   - 缺点
     - 相对于数据文件，aof远远大于rdb，修复速度慢
     - 运行效率比rdb慢



##### 16、Redis的发布订阅

![image-20200818224653011](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818224653011.png)

1. 发布订阅是一种消息通信模式：发布者（pub)发送信息，订阅者（sub)接收消息，微信、微波的关注系统

2. redis客户端可以订阅任意数量的频道

3. ```
   psubscribe name    //订阅消息
   public name hello  //发布消息
   subscribe name     //接收消息
   ```

   

4. ![image-20200818224934257](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818224934257.png)

5. 订阅后，会一直监听

6. 实时沟通消息系统；实时聊天；订阅、关注系统

##### 17、Redis的主从复制

![image-20200818225813388](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818225813388.png)

1. 将一台Redis服务器的数据，复制到其他的Redis服务器，前者称为主节点（master/leader)，后者称为从节点（slave/follower)；数据的复制是单向的，只能从主节点到从节点，master以写为主，slaver以读为主

2. 主从复制的主要作用

   ![image-20200818230012534](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818230012534.png)

3. 环境配置：只配置从库，不配置主库

   ```
   1.  info replication   //查看当前库的信息
   2.  vim redis.conf   //修改配置文件
       主要修改端口（port)   pid名字
       log文件名字          dump.rdb名称       
   3.  slaveof  127.0.0.1 6379
       //设置从机去跟随主机，slaveof 主机IP 端口
   ```

   命令配置是暂时的

   需要在conf文件中修改配置，变成永久的从机

4. 细节

   - 主机可以写，从机只能读
   - 主机断开后，从机依旧连接到主机
   - 主机恢复后，从机仍然连接到主机
   - 从机断开后，变为自己的主机

5. 复制原理

   - 全量复制：连接主机后，会将主机所有数据复制
   - 增量复制：主机继续将命令传送给从机，完成同步
   - 重新连接主机后，全量复制将自动执行
   - 主机断开连接后，从机使用slaveof no one 可以变成主机

6. **哨兵模式**

   ![image-20200818232411979](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818232411979.png)

   ![image-20200818232501027](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818232501027.png)

   1. 配置哨兵

      ```
      vim sentinel.conf   //新建文件
      sentinel monitor myredis 127.0.0.1 6379 1
      //sentinel monitor 被监控的名称  IP port 票数
      ```

   2. 启动哨兵

      ```
      redis-sentinel kconfig/sentinel.conf
      ```

      

   3. 如果主机宕机，会自动选择一个从机作为主机

   4. 优点

      - 哨兵集群，基于主从复制模式
      - 主从可以切换，故障可以转移，系统的可用性更好
      - 哨兵模式就是主从模式的升级，手动到自动，更加健壮

   5. 缺点

      - redis不好在线扩容，集群容量到达上限，扩容十分麻烦
      - 多哨兵集群，配置麻烦

##### 18、Redis缓存穿透和雪崩

1. 缓存穿透：用户想要查询一个数据，发现redis内存数据库没有，也就是**缓存没有命中**，于是向持久层数据库查询。发现也没有，于是本次查询失败。当用户很多的时候，缓存都没有命中（秒杀），于是都去请求持久层数据，会给持久层数据库造成很大的压力，这时候就相当于出现了缓存穿透

   1. 解决方案--布隆过滤器

      - 布隆过滤器是一种数据结构，对所有可能查询的参数以hash形式存储，在控制层先进行校验，不符合则丢弃，从而避免了对底层存储系统的查询压力
      - 存在误判
      - 删除困难

      

      ![image-20200818234358838](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818234358838.png)

   2. 解决方案--缓存空对象

      当存储层不命中后，即使返回的空对象也缓存起来，同时设置一个过期时间，之后再访问这个数据将会从缓存中获取，保护了后端数据源

      ![image-20200818234540983](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818234540983.png)

      

2. **缓存击穿**：**在某一个热点key缓存失效和恢复的间歇**，持续的大并发就穿破缓存，直接请求数据库，导致数据库瞬间压力过大

   1. 解决方案---设置热点数据永不过期
   2. 解决方案--加互斥锁：分布式锁，保证对于每个key同时只有一个线程去查询后端服务，其他线程没有获得分布式锁的权限；这种方式将高并发的压力转移到分布式锁，对分布式锁的考验很大

3. **缓存雪崩**：指在某一个时间段，**缓存集中过期失效**，redis宕机

   ![image-20200818235419294](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20200818235419294.png)

   1. 解决方案--高可用：redis可能挂掉，多增设几台（异地多活）
   2. 解决方案--限流降级：缓存失效后，通过加锁或者队列来控制读数据库写缓存的线程数量
   3. 解决方案--数据预热：在正式部署之前，先把可能的数据先预先访问一遍，这样部分可能大量访问的数据就会加载到缓存中。在即将发生大并发访问前手动触发加载缓存不同的key，设置不同的过期时间，让缓存失效的时间点尽量均匀





