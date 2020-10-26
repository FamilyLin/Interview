一、File类

1、File类的一个对象代表一个文件或一个文件目录

2、路径分隔符：

Windows：\\

unix：/

3、构造器

① public File(String filePath)

​      File file1 = new File("pathname");

②File file2 = new File(String parentPath, String childPath)

③File file3 = new File(File parentPath, String childPath)

4、常用方法

getAbsolutePath();绝对路径

getPath();路径

getName();

getParent(); 文件夹目录

length();大小

lastModeified();最后一次修改的时间



适用于文件目录的两个方法：

public  String[] list():获取指定目录下的所有文件或者文件目录的名称数组

public File[] listFiles()；获取指定目录下的所有文件或者文件目录的File数组



public boolean renameTo(File dest);把文件重名为指定的文件路径

file1.renameTo(file2):要求file1存在，file2不存在



File  file1 = new File("hi.txt");

file1.createNewFile();

file1.delete();删除目录，要求目录下没有文件

File file2 = new File("d:\\io\\io1");

file2.mkdir();

file2.mkdirs(); 如果上层目录不存在，则一起创建



二、IO流

1、流的分类：

①数据单位不同：字节流（8 bit）、字符流(16 bit)

②流向不同：输入、输出

③角色不同：节点流、处理流 

​            |        字节流         |   字符流  

输入流|   InputStream    |   Reader

输出流|  OutputStream  |    Writer





2、流的体系结构：

①抽象基类：

InputStream 

OutputStream

Reader

Writer

②节点流

FileInputStream      (read(byte[]  buffer);

FileOutputStream   (write(byte[] buffer,0,len);

FileReader                (read(char[] cbuf);

FileWriter                  (write(char[] cbuf,0,len);

③缓冲流：

BufferedInputStream      (read(byte[]  buffer);

BufferedOutputStream   (write(byte[] buffer,0,len);

BufferedReader                (read(char[] cbuf / readLine())

BufferedWriter                  (write(char[] cbuf,0,len);



3、流的输入

①实例化File类的对象，指明要操作的文件

File file = new File("pathname");

②提供具体的流

FileReader fr = new FileReader(file);

③数据的读入

int data = fr.read();

返回读入的一个字符，如果达到文件末尾，返回-1

④流的关闭

fr.close();



4、流的输出

输出操作对应的File可以不存在，自动创建；

如存在，可以覆盖；

①提供File类的对象，指明写到的文件

File  file = new File("pathname");

②提供FileWriter的对象，用于数据的写出

FileWriter fw  = new FileWriter(file,boolean);

boolean:   true,不覆盖，在原有基础上继续添加；

​                   false,覆盖 

③写出

fw.write("what")；

④流的关闭

fw.close();



5、读写

①创建File，指明读入、写出

File  file1 = new File("pathname");

File  file2 = new File("pathname");

②创建输入流、输出流

FileWriter fr  = new FileReader(file1,boolean);

FileWriter fw  = new FileWriter(file2,boolean);

③读入写出操作

char[] cbuf = new char[5];

int len;

while((len = fr.read(cbuf) ) != -1){

​     fw.write(cbuf,0,len);

}

④关闭

fr.close();

fw.close();



6、对于非文本文件，需要用字节流FileInputStream和FileOutputStream

对于文本文件，可以用字符流Reader和Writer



7、缓冲流的读取和写入

 BufferedInputStream

BurrferedOutputStream

BufferedReader

BufferedWriter

①造文件

File file1 = new File();

File file2 = new File();

②造流

​      1>造节点流

​       FileInputStream fis = new BufferedInputStream(file1);

​       FileOutputStream fos = new BufferedOutputStream(file2);

​       2>造缓冲流

BufferedInputStream bis = new BufferedInputStream(fis);

BufferedOutputStream bos = new BufferedOutputStream(fos);

③读取和写入

byte[] buffer = new byte[10];

int len;

while((len = bis.read(buffer)) != -1){

​        bos.write(buffer,0,len);

​       //bos.flush();一般为自动调用

}

④关闭；要求：先关闭外层的流，后关闭内层的流

bos.close();

bis.close();

关闭外层流的同时，内层流自动关闭。



8、缓冲流的特点

①需要嵌套在已有流的外部使用；

②提高了读写的速度，内部提供了缓冲区

③ .flush()；刷新缓冲区



9、转换流(字符流)

解码：

InputStreamReader：将字节输入流转换为字符输入流

编码：

OutputStreamWriter：将字符输出流转换为字节输出流



10、字符集

ASCII

GB2312

GBK：最高位是1，表示两个字节；最高位是0，表示一个字节

Unicode

UTF-8



11、标准的输入、输出流：

System.in;

InputStreamRead isr = new InputStreamRead(System.in);

System.out;



12、对象流（处理流）

反序列化：ObjectInputStream：将磁盘文件中的对象还原为内存中的一个Java对象

序列化：ObjectOutputStream：将内存中的Java对象保存到磁盘中或通过网络传输出去



**Java对象为可序列化，需要满足的要求：**

①实现接口：Serializable

②当前类提供一个全局常量serialVersionUID

public static final long serialVersionUID = 123432L;

③除了当前类实现Serializable，其内部的属性都必须是可序列化的（基本数据类型是可序列化的）

static和transient修饰的成员变量不可序列化；



13、随机存取文件流：

RandomAccessFile：

既可以输入又可以输出；

直接继承java.lang.Object类；

实现了DataInput和DataOutput接口

作为输出流，如果目标文件不存在，则创建；如果存在，则覆盖；

.seek(n);将指针调到角标为n的位置







