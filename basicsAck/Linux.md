##### 1、目录结构

<img src="C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20201007195830015.png" alt="image-20201007195830015" style="zoom:80%;" />

- /root：系统管理员的用户主目录

- /bin（Binary）：  /usr/bin     /usr/local/bin

  存放最经常使用的命令

- /boot：存放启动Linux时使用的核心文件，包括一些连接文件及镜像文件

- /etc：所有的系统管理所需要的配置文件和子目录

- /home：存放普通用户的主目录，在Linux中每个用户都有自己的目录，一般以用户的账号命名

- /var：存放着不断扩充着的东西，如日志文件

- /lib：系统开机所需要最基本的动态连接共享库，作用类似于Windows中的DLL文件

- /usr：存放用户的应用程序和文件，类似于Windows中的program files目录

- /media：Linux系统将自动识别的设备挂在到此目录下

- /sbin（Super User Binary)：/usr/bin     /usr/local/bin

  存放系统管理员使用的系统管理程序

- /mnt：为了让用户临时挂载别的文件系统，可以将外部的存储挂载在/mnt/上；如Windows和Linux的共享文件

- /usr/local：给主机额外安装软件的安装目录，一般是通过编译源码方式安装的程序

##### 2、vim的使用

```java
//vim hello.java
public class hello{
    public static void main(String[] args){
        System.out.println("Hello world !");
    }
}
//:wq    写入退出
//:q     无操作退出
//:q!    丢弃操作，强制退出
```

```
//常用快捷键
//拷贝当前行：yy   拷贝当前行向下5行：5yy     粘贴：p
//删除当前行：dd   删除当前行向下5行：5dd
//查找某个单词：/关键字      例：/hello    输入n，查找下一个
//设置文件的行号：:set nu         取消文件的行号： :set nonu
//到最末行：G   到最首行：gg
//撤销操作：u
//定位到指定行(20)：20+shift+g
```

##### 3、关机重启指令

>shutdown:
>
>- shutdown -h now  立即关机
>- shutdown -h 1    1分钟后关机
>- shutdown -r now  立即重启
>
>halt:          立即关机
>
>reboot:     重启
>
>sync:         把内存的数据同步到磁盘（关机重启前运行）
>
>logout:      注销

##### 4、用户指令

> **添加用户**
>
> useradd zjl          添加用户名
>
> useradd -d [指定目录] Xxx     添加到指定目录
>
> passwd  xxxxx    添加密码



> **删除用户**
>
> userdel Xxx   删除用户保留家目录
>
> userdel -r Xxx 删除用户及家目录



> **查询用户信息**
>
> id 用户名



> **切换用户**
>
> su -  Xxx   切换到Xxx用户
>
> exit 切换回
>
> whoami 查看当前用户

##### 5、用户组命令

> **增加组**
>
> groupadd 组名
>
> useradd -g 组名 用户名    将用户指定到组中



> **删除组**
>
> groupdel 组名



> **修改用户组**
>
> usermod -g 用户组 用户名

##### 6、用户和组的文件

> **用户配置文件：/etc/passwd**
>
> 其中每行的含义：用户名：口令：用户ID：组ID：家目录：shell



> **组配置文件：   /etc/group**
>
> 其中每行的含义：组名：口令：组标识号：组内用户列表



> **口令配置文件（密码）： /etc/shadow**
>
> 其中每行的含义：用户名：加密口令：最后一次修改的时间：最小时间间隔：最大时间间隔：警告时间：不活动时间：失效时间：标志

##### 7、实用指令

> 指令运行级别：（配置文件：/etc/inittab）
>
> 0. 关机
>
> 1. 单用户【找回丢失密码】
> 2. 多用户状态没有网络服务
> 3. 多用户状态有网络服务
> 4. 系统未使用保留给用户
> 5. 图形界面
> 6. 系统重启
>
> 指定运行级别的指令：init n



> 单用户级别修改密码：
>
> 1. 开机，在引导时输入回车键
> 2. 看到界面  输入e
> 3. 选中第二行（编辑内核）输入e
> 4. 在这一行输入1，再回车
> 5. 再输入b，进入单用户模式
> 6. 用passwd指令修改密码

##### 8、帮助指令

> man 指令       获取帮助信息
>
> help 指令

##### 9、文件目录类指令

> ls -a ----------显示隐藏目录
>
> cd ~ ----------返回家目录
>
> mkdir  []   ----------创建目录
>
> mkdir -p  []   ----------创建多级目录
>
> rmdir [] ----------删除空目录
>
> rm -rf [] ----------删除非空目录
>
> touch [] ----------创建空文件



> cp []  源文件 目标文件        ----------拷贝文件
>
> cp -r 源文件 目标文件         ----------拷贝整个文件夹
>
> \cp -r 源文件 目标文件        ----------强制覆盖 



> mv oldNameFile newNameFile    ----------重命名
>
> mv file  targetFile       ----------将file移动到targetFile中



> cat /etc/profile       ----------显示文件内容
>
> cat -n /etc/profile   ----------显示内容和行号
>
> cat -n /etc/profile | more ----------分页显示
>
> more 要查看的文件   ----------查看文件，一次性加载完
>
> less 要查看的文件 ---------查看文件，不断加载显示，非一次性加载



> ">"  重定向，覆盖--------ls > a.txt，将ls的信息传入a.txt中
>
> ">>"   追加
>
> echo  [1] >  [2]  --------重定向,将1覆盖2
>
> echo [1] >> [2]  --------追加



> echo []            -------输出内容到控制台
>
> echo $PATH  -------输出环境变量到控制台
>
> head []            -------默认输出文件前10行
>
> head -n 5 []    -------输出文件前5行
>
> tail []  -----------默认输出文件后10行
>
> tail -n 5 [] ------输出文件后5行
>
> tail -f []    -----------将文件更新的内容显示出来



> 软连接：类似于Windows中的快捷方式
>
> ln -s [原文件或目录] [软连接名] ------建立软连接
>
> rm -rf [软连接名] -----------删除软连接



> history -------查看已经执行过的历史命令
>
> history 10 -----最近执行的10条指令
>
> !5  --------最近执行过的第5条指令



##### 10、时间日期类

> date ------直接显示时间
>
> date “ + %Y - %m - %d" 显示年 月 日 
>
> date “ + %Y - %m - %d  %H:%M:%S" 



> 设置时间
>
> date -s "2020-10-9 20:05:20"



> 显示日历
>
> cal   -------显示当前月
>
> cal 2020--------显示指定年



##### 11、搜索查找指令

> find指令
>
> find [搜索范围] [选项] [参数]
>
> find /home -name *.txt---------按文件名查找
>
> find /home -user nobody ---------按文件拥有者查找
>
> find /  -size +20M   ---------按文件大小查找
>
> +n 表示大于n    -n表示小于n     n表示等于



> locate指令
>
> 可以快速定位文件路径，无需遍历整个文件系统，查询速度较快
>
> updatedb----------更新数据库
>
> locate [查询文件]-------基于数据库进行查询，第一次运行时，需要使用updatedb指令创建locate数据库



> grep指令
>
> grep [选项]  ---------查找内容源文件
>
> grep -n  []   ------显示行号
>
> grep -i  [] ----------不区分大小写
>
> cat hello.txt | grep yes      ---------在hello.txt文件中查找yes



##### 12、压缩和解压缩指令

> gzip   和  gunzip
>
> gzip  hellp.txt    --------压缩文件后，不会保留原来的文件
>
> gunzip  hellp.txt.gz ----------解压缩



>zip  和  unzip 
>
>zip [压缩文件名] [文件名]  ---------压缩文件
>
>zip -r [压缩文件名] [目录] -----------  -r表示递归压缩该目录
>
>unzip -d <目录> [解压文件] ----------解压到指定目录



> tar指令
>
> tar  -zcvf    a.tar.gz  a1.txt  a2.txt    -----将a1,a2一起压缩到a.tar.gz
>
> tar -zcvf    my.tar.gz  /home/       ------将目录打包
>
> tar -zxvf     a.tar.gz ----------解压到当前目录
>
> tar -zxvf     a.tar.gz   -C  /home/ -------解压到指定目录



##### 13、组管理

> ls -ahl          -----------查看文件的所有者、所在组
>
> chown   owner   [文件]------修改文件所有者为owner



> chgrp 组名 [文件]------修改文件所在组



##### 14、权限管理

> ls -l 显示行
>
> -rw-------. 1 root root 1784 Oct  7 05:25 anaconda-ks.cfg
>
> 0-9位说明
>
> 第0位确定文件类型（-(文件) , d(目录) , l(连接) , c , b )
>
> 第1-3位确定所有者拥有的权限
>
> 第4-6位确定所属组拥有的权限
>
> 第7-9位确定其他用户拥有的权限 

![image-20201011133317669](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20201011133317669.png)

> **r = 4;  w = 2; x = 1;**
>
> rwx作用到文件
>
> [r] 表示read
>
> [w] 表示write，只能修改，不可删除文件
>
> [x] 表示execute，可执行



> rwx作用到目录
>
> [r] 表示read
>
> [w] 表示write ，创建+删除+重命名目录
>
> [x] 表示execute，可以进入该目录



> chmod----**修改文件或目录权限**   + 、-  、=
>
> 方法一：
>
> u:所有者  g:所有组  o:其他人    a:所有人
>
> chmod u = rwx, g = rx , o = x [文件目录名]
>
> chmod o+w  [文件目录名]   -----增加权限
>
> chmod  a - x [文件目录名] -------减少权限
>
> 方法二：
>
> r = 4; w = 2; x = 1;
>
> chmod u = rwx, g = rx, x = x  [文件名]
>
> chmod 751 [文件名]



> chown  [username]  [file] -----修改文件所有者
>
> chown  -R  [username] [directory] ------修改目录下所有文件所有者
>
> chgrp [groupname] [file] ---修改所在组
>
> chgrp -R [groupname] [directory] ---修改目录下所有文件所在组



##### 15、任务调度

> 设置任务调度文件： /etc/crontab
>
> 设置个人任务调度。执行：crontab   -e  
>
> 接着输入任务到调度文件，如：*/1**** ls -l  /etc/  >  /temp/to.txt
>
> //每分钟执行ls -l /etc/ > /temp/to.txt 命令
>
> 占位符说明：

> 第一个*表示一小时当中的第几分钟
>
> 第二个*表示一天当中的第几小时
>
> 第三个*表示一个月当中的第几天
>
> 第四个*表示一年当中的第几月
>
> 第五个*表示一周当中的星期几  

> crontab -r --------终止任务调度
>
> crontab -l  --------列出当前有哪些任务调度
>
> service crond restart ---------重启任务调度



##### 16、磁盘分区、挂载

> 查看分区情况：lsblk -f

> 1. 虚拟机增加硬盘、重启
>
> 2. 分区: fdisk    /dev/sdb
>
>    ​         输入：m  ----  n------   p-----enter------enter------w
>
> 3. 格式化: mkfs -t ext4  /dev/sdb1
>
> 4. 挂载: 创建目录如：mkdir /home/newdisk   
>
>    ​          挂载指令：mount  /dev/sdb1     /home/newdisk
>
> 5. 永久挂载:   vim  /etc/fstab
>
>    ​                   修改语句，实现永久挂载
>
>    ​                   mount -a
>
> 6. 卸载： umount  /dev/sdb1



> df -lh   ------------查看当前磁盘使用情况



> du -h  /目录   ----------查看指定目录的磁盘占用情况
>
> -s指定目录占用大小汇总  -h带计量单位  -a含文件
>
> --max-depth=1 子目录深度         -c列出明细的同时，增加汇总值
>
> du  -ach --max-depth=1 /opt



> 常用指令：
>
> 1. 统计/home文件夹下文件的个数
>
>    ls -l /home | grep "^-" | wc -l
>
> 2. 统计/home文件夹下目录的个数
>
>    ls -l /home | grep "^d" | wc -l
>
> 3. 统计/home文件夹下文件的个数，包括子文件夹中的个数
>
>    ls -lR /home | grep "^-" | wc -l
>
> 4. 统计/home文件夹下目录的个数，包括子文件夹中的个数
>
>    ls -lR /home | grep "^d" | wc -l
>
> 5. 以树状显示目录结构



##### 17、网络配置

> 修改为固定IP：
>
> vim /etc/sysconfig/network-scripts/ifcfg-eth0



##### 18、进程管理

![image-20201011181204011](C:\Users\11437\AppData\Roaming\Typora\typora-user-images\image-20201011181204011.png)

> ps -aux    --------查看进程
>
> pstree-----以树状形式显示  -p---显示PID-------  -u------显示用户
>
> -a: 显示所有进程 
>
> -u: 以用户的格式显示进程信息
>
> -x: 显示后台进程运行的参数
>
> ps -aux | grep Xxxx
>
> ps -ef | more -------查看父进程
>
> ps -ef |grep sshd --------查看sshd的父进程



> 终止进程kill和killall
>
> kill [选项] 进程号 ----------常用选项为-9，表示强制杀死
>
> killall 进程名称（支持通配符）
>
> 1. 踢掉非法用户
>
>    ps -aux | grep sshd  -------查看登录用户
>
>    kill [进程号]---------杀死进程
>
> 2. 终止远程登录服务sshd，在适当时候再次重启sshd服务
>
>    kill [sshd服务的进程号]
>
> 3. 终止多个gedit编辑器
>
>    killall [进程名称]
>
>    killall gedit
>
> 4. 强制杀死一个终端
>
>    ps -aux | grep bash
>
>    kill -9 [终端进程号]



##### 19、服务管理

> systemctl 服务名 [start|stop|reload|status]
>
> 1. 查看防火墙状态
>
>    systemctl  status  firewalld
>
>    systemctl  stop firewalld
>
>    systemctl restart firewalld

> 用setup查看自启动服务

开机流程

开机-->BIOS-->/boot-->init进程1-->运行级别-->运行级对应的服务



> chkconfig可以给每个服务的个个运行级别设置自启动/关闭
>
> chkconfig --list | grep xxx-------------查看服务
>
> chkconfig 服务名 --list
>
> chkconfig --level 5 服务名 on/off-----设置在运行级别下是否自启动
>
> **重启后生效**



##### 20、进程监控

> top [选项] ----与ps命令相似，但是可以不断更新
>
> top -d 10-----每隔10s刷新
>
> -i------不显示任何闲置或僵死进行
>
> -p------指定进程ID进行监控



> netstat [选项] --------监控网络服务
>
> -an   按一定顺序排序
>
> -p  显示哪个进程在调用
>
> netstat -anp | more --------查看所有网络服务
>
> netstat -anp | grep sshd --------查看指定服务网络



##### 21、RPM和YUM

> rpm包的查询指令
>
> rpm -qa-----------查询所安装的所有rpm软件包
>
> rpm -qa | more
>
> rpm -qa | grep xxx------查询指定包
>
> rpm -qi [软件包名]-------查询软件包信息
>
> rpm -ql [软件包名]-------查询软件包文件安装信息
>
> rpm -qf [文件全路径名]--------查询文件所属软件包



> 卸载rpm包
>
> rpm -e [软件包名]
>
> rpm -e --nodeps [软件包名]

> 安装rpm包
>
> rpm -ivh [软件包名]
>
> -i：install   安装
>
> -v：verbose 提示
>
> -h：hash 进度条



> yum指令
>
> yum list | grep xxx-----------查询是否有xxx软件包
>
> yum install xxx---------安装





##### 22、JavaEE环境配置

> 1. 软件包放在/opt目录中
> 2. tar -zxvf [jdk文件名] 解压
> 3.  配置环境变量的配置文件 vim /etc/profile



##### 23、tomcat安装

> 1、解压------tar -zxvf [tomcat文件名]
>
> 2、进入文件夹-------cd apache-tomcat-8.5.58/bin/
>
> 3、启动：   ./startup.sh
>
> 4、配置防火墙，打开8080端口：
>
> firewall-cmd --zone=public --add-port=8080/tcp --permanent
>
> firewall-cmd --reload
>
> 5、重启tomcat





##### 24、常用快捷键

> ctrl + d : 键盘输入结束或退出终端
>
> ctrl + s : 暂停当前程序，按下任意键恢复
>
> ctrl +  z : 将当前程序放到后台运行；f + g 恢复到前台
>
> ctrl + a : 将光标移动到头部
>
> ctrl + e : 将光标移动到尾部
>
> ctrl + k : 删除从光标所在位置到行末
>
> alt + backspace ： 向前删除一个单词



> 通配符
>
> *： 匹配0或多个字符
>
> ？：匹配任意一个字符
>
> [list] : 匹配list中的任意单一字符
>
> [^list] : 匹配出list中的任意单一字符以外的字符
>
> [c1 - c2] ：匹配c1 - c2 中的任意单一字符
>
> {String1,string2.....} ： 匹配string1或string2其一字符串
>
> {c1..c2} : 匹配c1 - c2中全部字符







