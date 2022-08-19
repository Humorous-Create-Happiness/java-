## IO流

### File类

File类的一个对象，代表一个文件或一个文件目录(俗称：文件夹)。

File类声明在 `java.io` 包下：文件和文件路径的抽象表示形式，与平台无关。

File类中涉及到关于文件或文件目录的创建、删除、重命名、修改时间、文件大小等方法，并未涉及到写入或读取文件内容的操作。如果需要读取或写入文件内容，必须使用IO流来完成。

想要在 Java 程序中表示一个真实存在的文件或目录，那么必须有一个 File 对象，但是 Java程序中的一个 File 对象，可能没有一个真实存在的文件或目录。

后续 File 类的对象常会作为参数传递到流的构造器中，指明读取或写入的"终点"。



常用构造器：

```java
public void test1() 
{
    //构造器1
    File file1 = new File("hello.txt");
    File file2 = new File("E:\\workspace_idea\\JavaSenic\\IO\\hello.txt");
    System.out.println(file1);
    System.out.println(file2);

    //构造器2
    File file3 = new File("E:\\workspace_idea\\JavaSenior", "hello.txt");
    System.out.println(file3);

    //构造器3
    File file4 = new File(file3, "hi.txt");
    System.out.println(file4);
}

```



路径的分类：

绝对路径：包含盘符在内的文件或文件目录的路径。

IDEA中：

- 如果使用JUnit中的单元测试方法测试，相对路径即为当前Module下。
- 如果使用main()测试，相对路径即为当前的Project下。

Eclipse中：

- 不管使用单元测试方法还是使用main()测试，相对路径都是当前的Project下。



路径分隔符：

```java
//windows和DOS系统
File file1 = new File("E:\\io\\test.txt");
//UNIX和URL
File file = new File("E:/io/test.txt");
//java提供的常量
File file = new File("E:"+File.separator+"io"+File.separator+"test.txt");


```



#### File类的获取方法：



```java
public String getAbsolutePath()//获取绝对路径


public String getPath()//获取路径


public String getName() //获取名称


public String getParent()//获取上层文件目录路径。若无，返回 null


public long length() //获取文件长度（即：字节数）。不能获取目录的长度。


public long lastModified() //获取最后一次的修改时间，毫秒值
```

方法的使用：

```java
public void test2()
{
    File file1 = new File("hello.txt");
    File file2 = new File("d:\\io\\hi.txt");

    System.out.println(file1.getAbsolutePath());
    System.out.println(file1.getPath());
    System.out.println(file1.getName());
    System.out.println(file1.getParent());
    System.out.println(file1.length());
    System.out.println(new Date(file1.lastModified()));

    System.out.println();

    System.out.println(file2.getAbsolutePath());
    System.out.println(file2.getPath());
    System.out.println(file2.getName());
    System.out.println(file2.getParent());
    System.out.println(file2.length());
    System.out.println(file2.lastModified());
}
@Test
public void test3()
{
    File file = new File("D:\\workspace_idea1\\JavaSenior");

    String[] list = file.list();
    for(String s : list)
    {
        System.out.println(s);
    }

    System.out.println();

    File[] files = file.listFiles();
    for(File f : files)
    {
        System.out.println(f);
    }

}

```



#### File类的重命名功能

public boolean renameTo(File dest)`:把文件重命名为指定的文件路径

注意：`file1.renameTo(file2)`为例：要想保证返回 `true` ,需要file1在硬盘中是存在的，且file2不能在硬盘中存在。

方法的使用：

```java
public void test4()
{
    File file1 = new File("hello.txt");
    File file2 = new File("D:\\io\\hi.txt");

    boolean renameTo = file2.renameTo(file1);
    System.out.println(renameTo);

}
```

####  File类的判断功能

方法：

```java
- public boolean isDirectory()//判断是否是文件目录
- public boolean isFile()//判断是否是文件
- public boolean exists()//判断是否存在
- public boolean canRead()//判断是否可读
- public boolean canWrite()//判断是否可写
- public boolean isHidden()//判断是否隐藏
```

使用：

```java
public void test5()
{
    File file1 = new File("hello.txt");
    file1 = new File("hello1.txt");

    System.out.println(file1.isDirectory());
    System.out.println(file1.isFile());
    System.out.println(file1.exists());
    System.out.println(file1.canRead());
    System.out.println(file1.canWrite());
    System.out.println(file1.isHidden());

    System.out.println();

    File file2 = new File("d:\\io");
    file2 = new File("d:\\io1");
    System.out.println(file2.isDirectory());
    System.out.println(file2.isFile());
    System.out.println(file2.exists());
    System.out.println(file2.canRead());
    System.out.println(file2.canWrite());
    System.out.println(file2.isHidden());

}
```



#### Flie类的创建功能



创建硬盘中对应的文件或文件目录

方法：

```java
public boolean createNewFile()//创建文件。若文件存在，则不创建，返回false

public boolean mkdir()//创建文件目录。如果此文件目录存在，就不创建了。如果此文件目录的上层目录不存在，也不创建。

public boolean mkdirs()//创建文件目录。如果此文件目录存在，就不创建了。如果上层文件目录不存在，一并创建
```

使用：

```java
public void test6() throws IOException 
{
    File file1 = new File("hi.txt");
    if(!file1.exists())
    {
        //文件的创建
        file1.createNewFile();
        System.out.println("创建成功");
    }else{//文件存在
        file1.delete();
        System.out.println("删除成功");
    }


}
@Test
public void test7()
{
    //文件目录的创建
    File file1 = new File("d:\\io\\io1\\io3");

    boolean mkdir = file1.mkdir();
    if(mkdir)
    {
        System.out.println("创建成功1");
    }

    File file2 = new File("d:\\io\\io1\\io4");

    boolean mkdir1 = file2.mkdirs();
    if(mkdir1)
    {
        System.out.println("创建成功2");
    }
    //要想删除成功，io4文件目录下不能有子目录或文件
    File file3 = new File("D:\\io\\io1\\io4");
    file3 = new File("D:\\io\\io1");
    System.out.println(file3.delete());
}

```

#### File类的删除功能

删除磁盘中的文件或文件目录

```java
public boolean delete()//删除文件或者文件夹

删除注意事项：Java中的删除不走回收站。
```

小练习：

利用 File 构造器，`new` 一个文件目录file

1）在其中创建多个文件和目录

2）编写方法，实现删除fle中指定文件的操作

如下：

```java
public void test1() throws IOException 
{
    File file = new File("E:\\io\\io1\\hello.txt");
    //创建一个与file同目录下的另外一个文件，文件名为：haha.txt
    File destFile = new File(file.getParent(),"haha.txt");
    boolean newFile = destFile.createNewFile();
    if(newFile)
    {
        System.out.println("创建成功！");
    }
}
```





### IO流概述

IO 是 Input/Output 的缩写，I/O 技术是非常实用的技术，用于处理设备之间的数据传输。如读/写文件，网络通讯等。

Java程序中，对于数据的输入输出操作以 “流(stream)” 的方式进行。

`Java.IO` 包下提供了各种“流”类和接口，用以获取不同种类的数据，并通过标准的方法输入或输出数据。

#### 分类

**操作数据单位：字节流、字符流**

对于文本文件(`.txt,.java,.c,.cpp`)，使用字符流处理

对于非文本文件(`.jpg,.mp3,.mp4,.avi,.doc,.ppt,...`)，使用字节流处理

**数据的流向：输入流、输出流**

输入 input:读取外部数据（磁盘、光盘等存储设备的数据）到程序（内存）中。

输出 output:将程序（内存）数据输出到磁盘、光盘等存储设备中。

**流的角色：节点流、处理流**

节点流：直接从数据源或目的地读写数据。

处理流：不直接连接到数据源或目的地，而是“连接”在已存在的流（节点流或处理流）之上，通过对数据的处理为程序提供更为强大的读写功能。

#### 常用的几个IO流结构

| 抽象基类    | 节点流（或文件流）                             | 缓冲流（处理流的一种）                                       |
| ----------- | ---------------------------------------------- | ------------------------------------------------------------ |
| InputStream | `FileInputStream (read(byte[] buffer))`        | `BufferedInputStream (read(byte[] buffer))`                  |
| OutputSteam | `FileOutputStream (write(byte[] buffer,0,len)` | `BufferedOutputStream (write(byte[] buffer,0,len)` / `flush()` |
| Reader      | `FileReader (read(char[] cbuf))`               | `BufferedReader (read(char[] cbuf)` / `readLine()`           |
| Writer      | `FileWriter (write(char[] cbuf,0,len)`         | `BufferedWriter (write(char[] cbuf,0,len)` / `flush()`       |





#### 对抽象基类的说明：

| 抽象基类 | 字节流      | 字符流 |
| -------- | ----------- | ------ |
| 输入流   | InputSteam  | Reader |
| 输出流   | OutputSteam | Writer |

方法：

InputStream和Reader是所有输入流的基类。

```java

//InputStream（典型实现：FileInputStream）

int read()
//从输入流中读取数据的下一个字节。返回0到255范围内的int字节值。如果因为已经到达流末尾而没有可用的字节，则返回值-1。


int read(byte[] b)
//从此输入流中将最多b.length个字节的数据读入一个byte数组中。如果因为已经到达流末尾而没有可用的字节，则返回值-1.否则以整数形式返回实际读取的字节数。


int read(byte[] b,int off,int len)
//将输入流中最多len个数据字节读入byte数组。尝试读取len个字节，但读取的字节也可能小于该值。以整数形式返回实际读取的字节数。如果因为流位于文件末尾而没有可用的字节，则返回值-1。


public void close throws IOException
//关闭此输入流并释放与该流关联的所有系统资源


//程序中打开的文件IO资源不属于内存里的资源，垃圾回收机制无法回收该资源，所以应该显式关闭文件IO资源。


//FileInputStream 从文件系统中的某个文件中获得输入字节。FileInputStream 用于读取非文本数据之类的原始字节流。要读取字符流，需要使用 FileReader。

```

```java
//Reader（典型实现：FileReader）

int read()
//读取单个字符。作为整数读取的字符，范围在0到65535之间（0x00-0xffff）(2个字节的 Unicode码)，如果已到达流的末尾，则返回-1。


int read（char[] cbuf)
//将字符读入数组。如果已到达流的末尾，则返回-1。否则返回本次读取的字符数。


int read（char[] cbuf,int off,int len)
//将字符读入数组的某一部分。存到数组cbuf中，从off处开始存储，最多读len个字符。如果已到达流的末尾，则返回-1。否则返回本次读取的字符数。


public void close throws IOException
//关闭此输入流并释放与该流关联的所有系统资源
//程序中打开的文件IO资源不属于内存里的资源，垃圾回收机制无法回收该资源，所以应该显式关闭文件IO资源。


//FileInputStream 从文件系统中的某个文件中获得输入字节。FileInputStream 用于读取非文本数据之类的原始字节流。要读取字符流，需要使用 FileReader。

```



```java
//OutputStream:


void write(int b)
//将指定的字节写入此输出流。 write的常规协定是：向输出流写入一个字节。要写入的字节是参数b的八个低位。b的24个高位将被忽略。即写入0~255范围的


void write（byte[] b)
//将 b.length 个字节从指定的byte数组写入此输出流。write(b)的常规协定是：应该与调用wite(b,0,b.length)的效果完全相同。


void write(byte[] b,int off,int len)
//将指定byte数组中从偏移量off开始的len个字节写入此输出流。


public void flush()throws IOException
//刷新此输出流并强制写出所有缓冲的输出字节，调用此方法指示应将这些字节立即写入它们预期的目标。


public void close throws IOException
//关闭此输岀流并释放与该流关联的所有系统资源。

```



```java
//Writer:


void write(int c)
//写入单个字符。要写入的字符包含在给定整数值的16个低位中，16高位被忽略。即写入0到65535之间的 Unicode码。


void write(char[] cbuf)
//写入字符数组


void write(char[] cbuf,int off,int len)
//写入字符数组的某一部分。从off开始，写入len个字符


void write(String str)
//写入字符串。


void write(String str,int off,int len)
//写入字符串的某一部分。


void flush()
//刷新该流的缓冲，则立即将它们写入预期目标。


public void close throws IOException
//关闭此输出流并释放与该流关联的所有系统资源
```

#### 输入、输出标准化过程

**输入过程：**

① 创建 File 类的对象，指明读取的数据的来源。（要求此文件一定要存在）

② 创建相应的输入流，将 File 类的对象作为参数，传入流的构造器中

③ 具体的读入过程：创建相应的 `byte[]` 或 `char[]`。

④ 关闭流资源

说明：程序中出现的异常需要使用 `try-catch-finally` 处理。

**输出过程：**

① 创建 File 类的对象，指明写出的数据的位置。（不要求此文件一定要存在）

② 创建相应的输出流，将 File 类的对象作为参数，传入流的构造器中

③ 具体的写出过程：`write(char[]/byte[] buffer,0,len)`

④ 关闭流资源

说明：程序中出现的异常需要使用 `try-catch-finally` 处理。

### 节点流（文件流）

#### 文件字符流 FileReader 和 FileWriter 的使用

**文件的输入**

从文件中读取到内存（程序）中

步骤：

```java
 FileReader fr = new FileReader(new File("Test. txt"));//建立一个流对象，将已存在的一个文件加载进流
char[] ch = new char[1024];//创建一个临时存放数据的数组 
 fr.read(ch);//调用流对象的读取方法将流中的数据读入到数组中。
fr.close();//关闭资源。 

```

使用：

```java
public void testFileReader1()  
{
    FileReader fr = null;
    try {
        //1.File类的实例化
        File file = new File("hello.txt");

        //2.FileReader流的实例化
        fr = new FileReader(file);

        //3.读入的操作
        //read(char[] cbuf):返回每次读入cbuf数组中的字符的个数。如果达到文件末尾，返回-1
        char[] cbuf = new char[5];
        int len;
        while((len = fr.read(cbuf)) != -1)
        {
            String str = new String(cbuf,0,len);
            System.out.print(str);
        }
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally 
    {
        if(fr != null)
        {
            //4.资源的关闭
            try 
            {
                fr.close();
            } 
            catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
    }

}
```

**注意点：**

1. `read()` 的理解：返回读入的一个字符。如果达到文件末尾，返回-1
2. 异常的处理：为了保证流资源一定可以执行关闭操作。需要使用 `try-catch-finally` 处理
3. 读入的文件一定要存在，否则就会报 `FileNotFoundException`。

**文件的输出**

从内存（程序）到硬盘文件中

方法：

```java
File Writer fw = new File Writer(new File("Test.txt"))//创建流对象，建立数据存放文件 


 fw.write("HelloWord")//调用流对象的写入方法，将数据写入流


fw.close();//关闭流资源，并将流中的数据清空到文件中。 

```

使用：

```java
public void testFileWriter() 
{
    FileWriter fw = null;
    try 
    {
        //1.提供File类的对象，指明写出到的文件
        File file = new File("hello1.txt");

        //2.提供FileWriter的对象，用于数据的写出
        fw = new FileWriter(file,false);

        //3.写出的操作
        fw.write("I have a dream!\n");
        fw.write("you need to have a dream!");
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally 
    {
        //4.流资源的关闭
        if(fw != null)
        {

            try 
            {
                fw.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }
        }
    }
}

```

#### 文件字节流 FileInputSteam 和 FileOutputSteam 的使用

文件字节流操作与字符流操作类似，只是实例化对象操作和数据类型不同。

使用：

```java
//使用字节流FileInputStream处理文本文件，可能出现乱码。
@Test
public void testFileInputStream() 
{
    FileInputStream fis = null;
    try 
    {
        //1. 造文件
        File file = new File("hello.txt");

        //2.造流
        fis = new FileInputStream(file);

        //3.读数据
        byte[] buffer = new byte[5];
        int len;//记录每次读取的字节的个数
        while((len = fis.read(buffer)) != -1)
        {

            String str = new String(buffer,0,len);
            System.out.print(str);

        }
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally {
        if(fis != null){
            //4.关闭资源
            try 
            {
                fis.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
    }

}
```

#### 注意点

定义路径时，可以用 `/` 或 `\\`。

输出操作，对应的 File 可以不存在的。并不会报异常。

File 对应的硬盘中的文件如果不存在，在输出的过程中，会自动创建此文件。

File 对应的硬盘中的文件如果存在：

- 如果流使用的构造器是：`FileWriter(file,false)` / FileWriter(file)`:对原有文件的覆盖。
- 如果流使用的构造器是：`FileWriter(file,true)`:不会对原有文件覆盖，而是在原有文件基础上追加内容。

读取文件时，必须保证文件存在，否则会报异常。

对于文本文件(`.txt,.java,.c,.cpp`)，使用字符流处理

对于非文本文件(`.jpg,.mp3,.mp4,.avi,.doc,.ppt,...`)，使用字节流处理

### 缓冲流

#### 缓冲流涉及到的类：

- `BufferedInputStream`
- `BufferedOutputStream`
- `BufferedReader`
- `BufferedWriter`

#### 引入目的：

- 作用：提供流的读取、写入的速度
- 提高读写速度的原因：内部提供了一个缓冲区。默认情况下是8kb

#### 如何使用

- 当读取数据时，数据按块读入缓冲区，其后的读操作则直接访问缓冲区。
- 当使用 `BufferedInputStream` 读取字节文件时，`BufferedInputStream` 会一次性从文件中读取8192个(8Kb)，存在缓冲区中，直到缓冲区装满了，才重新从文件中读取下一个8192个字节数组。
- 向流中写入字节时，不会直接写到文件，先写到缓冲区中直到缓冲区写满，`BufferedOutputStream` 才会把缓冲区中的数据一次性写到文件里。使用方法 `flush()` 可以强制将缓冲区的内容全部写入输出流。
- 关闭流的顺序和打开流的顺序相反。只要关闭最外层流即可，关闭最外层流也会相应关闭内层节点流。
- `flush()` 方法的使用：手动将 buffer 中内容写入文件。
- 如果是带缓冲区的流对象的 `close()` 方法，不但会关闭流，还会在关闭流之前刷新缓冲区，关闭后不能再写出。

**使用 BufferInputStream 和 BufferOutputStream 实现非文本文件的复制：**

```java
public void testBufferedStream()
{
    BufferedInputStream bis = null;
    BufferedOutputStream bos = null;
    try 
    {
        //1.造文件
        File srcFile = new File("test.jpg");
        File destFile = new File("test4.jpg");
        //2.造流
        //2.1造节点流
        FileInputStream fis = new FileInputStream(srcFile);
        FileOutputStream fos = new FileOutputStream(destFile);
        //2.2造缓冲流，可以合并书写
        bis = new BufferedInputStream(fis);
        bos = new BufferedOutputStream(fos);

        //3.文件读取、写出操作
        byte[] buffer = new byte[1024];
        int len;
        while ((len = bis.read(buffer)) != -1)
        {
            bos.write(buffer,0,len);
        }
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally 
    {
        //4.关闭流
        if (bos != null)
        {
            try 
            {
                bos.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }
        }
        if (bis != null)
        {

            try 
            {
                bis.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }
        }
    }
}

```

**使用 BufferedReader 和 BufferedWriter 实现文本文件的复制**

```java
public void testBufferedReaderBufferedWriter()
{
    BufferedReader br = null;
    BufferedWriter bw = null;
    try 
    {
        //创建文件和相应的流
        br = new BufferedReader(new FileReader(new File("dbcp.txt")));
        bw = new BufferedWriter(new FileWriter(new File("dbcp1.txt")));

        //读写操作
        //方式一：使用char[]数组
        //            char[] cbuf = new char[1024];
        //            int len;
        //            while((len = br.read(cbuf)) != -1){
        //                bw.write(cbuf,0,len);
        //    //            bw.flush();
        //            }

        //方式二：使用String
        String data;
        while((data = br.readLine()) != null)
        {
            //方法一：
            //                bw.write(data + "\n");//data中不包含换行符
            //方法二：
            bw.write(data);//data中不包含换行符
            bw.newLine();//提供换行的操作

        }


    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally 
    {
        //关闭资源
        if(bw != null)
        {

            try 
            {
                bw.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }
        }
        if(br != null)
        {
            try 
            {
                br.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
    }

}


```

#### 实现图片加密操作

```java
public void test1() 
{

    FileInputStream fis = null;
    FileOutputStream fos = null;
    try 
    {
        fis = new FileInputStream("test.jpg");
        fos = new FileOutputStream("testSecret.jpg");

        byte[] buffer = new byte[20];
        int len;
        while ((len = fis.read(buffer)) != -1) 
        {

            for (int i = 0; i < len; i++) {
                buffer[i] = (byte) (buffer[i] ^ 5);
            }

            fos.write(buffer, 0, len);
        }
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally {
        if (fos != null) 
        {
            try 
            {
                fos.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
        if (fis != null) 
        {
            try 
            {
                fis.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
    }
}
```

**解密操作**

- 将加密后图片文件通过字节流读取到程序中
- 将图片的字节流逐一进行 `^` 操作（原理：`A^B^B = A`）
- 将处理后的图片字节流输出

```java
//图片的解密
@Test
public void test2() 
{

    FileInputStream fis = null;
    FileOutputStream fos = null;
    try 
    {
        fis = new FileInputStream("testSecret.jpg");
        fos = new FileOutputStream("test4.jpg");

        byte[] buffer = new byte[20];
        int len;
        while ((len = fis.read(buffer)) != -1) 
        {
          
            for (int i = 0; i < len; i++) 
            {
                buffer[i] = (byte) (buffer[i] ^ 5);
            }

            fos.write(buffer, 0, len);
        }
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally {
        if (fos != null) 
        {
            try {
                fos.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
        if (fis != null) 
        {
            try 
            {
                fis.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
    }
}

```

#### 统计文本字符出现次数

实现思路：

1. 遍历文本每一个字符
2. 字符出现的次数存在Map中
3. 把map中的数据写入文件

```java
public void testWordCount() 
{
    FileReader fr = null;
    BufferedWriter bw = null;
    try 
    {
        //1.创建Map集合
        Map<Character, Integer> map = new HashMap<Character, Integer>();

        //2.遍历每一个字符,每一个字符出现的次数放到map中
        fr = new FileReader("dbcp.txt");
        int c = 0;
        while ((c = fr.read()) != -1) 
        {
            //int 还原 char
            char ch = (char) c;
            // 判断char是否在map中第一次出现
            if (map.get(ch) == null) 
            {
                map.put(ch, 1);
            } else {
                map.put(ch, map.get(ch) + 1);
            }
        }

        //3.把map中数据存在文件count.txt
        //3.1 创建Writer
        bw = new BufferedWriter(new FileWriter("wordcount.txt"));

        //3.2 遍历map,再写入数据
        Set<Map.Entry<Character, Integer>> entrySet = map.entrySet();
        for (Map.Entry<Character, Integer> entry : entrySet) 
        {
            switch (entry.getKey()) 
            {
                case ' ':
                    bw.write("空格=" + entry.getValue());
                    break;
                case '\t'://\t表示tab 键字符
                    bw.write("tab键=" + entry.getValue());
                    break;
                case '\r'://
                    bw.write("回车=" + entry.getValue());
                    break;
                case '\n'://
                    bw.write("换行=" + entry.getValue());
                    break;
                default:
                    bw.write(entry.getKey() + "=" + entry.getValue());
                    break;
            }
            bw.newLine();
        }
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally 
    {
        //4.关流
        if (fr != null) 
        {
            try 
            {
                fr.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
        if (bw != null) 
        {
            try 
            {
                bw.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
    }
}
```

### 转换流

转换流提供了在字节流和字符流之间的转换

Java API提供了两个转换流：

- `InputstreamReader`：将 `Inputstream` 转换为 `Reader`
- `OutputStreamWriter`：将 `Writer` 转换为 `OutputStream`

字节流中的数据都是字符时，转成字符流操作更高效。

很多时候我们使用转换流来处理文件乱码问题。实现编码和解码的功能

#### InputStreamReader

InputStreamReader 将一个字节的输入流转换为字符的输入流

解码：字节、字节数组 --->字符数组、字符串

构造器：

```java
public InputStreamReader(InputStream in)

public InputStreamReader(Inputstream in,String charsetName)//可以指定编码集
```

####  OutputStreamWriter

OutputStreamWriter 将一个字符的输出流转换为字节的输出流

编码：字符数组、字符串 ---> 字节、字节数组

构造器：

```java
public OutputStreamWriter(OutputStream out)
public OutputStreamWriter(Outputstream out,String charsetName)//可以指定编码集
```

使用：

```java
public void test1() 
{
    InputStreamReader isr = null;
    OutputStreamWriter osw = null;
    try 
    {
        //1.造文件、造流
        File file1 = new File("dbcp.txt");
        File file2 = new File("dbcp_gbk.txt");

        FileInputStream fis = new FileInputStream(file1);
        FileOutputStream fos = new FileOutputStream(file2);

        isr = new InputStreamReader(fis, "utf-8");
        osw = new OutputStreamWriter(fos, "gbk");

        //2.读写过程
        char[] cbuf = new char[20];
        int len;
        while ((len = isr.read(cbuf)) != -1)
        {
            osw.write(cbuf,0,len);
        }
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally {
        //3.关流
        if (isr != null)
        
        {

            try 
            {
                isr.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }
        }
        if (osw != null)
        {
            try 
            {
                osw.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
    }
}

```

#### 编码集

**常见的编码表**

ASCII：美国标准信息交换码。用一个字节的7位可以表示。

ISO8859-1：拉丁码表。欧洲码表用一个字节的8位表示。

GB2312：中国的中文编码表。最多两个字节编码所有字符

GBK：中国的中文编码表升级，融合了更多的中文文字符号。最多两个字节编码

Unicode：国际标准码，融合了目前人类使用的所字符。为每个字符分配唯一的字符码。所有的文字都用两个字节来表示。

UTF-8：变长的编码方式，可用1-4个字节来表示一个字符。

**应用**

编码：字符串-->字节数组

解码：字节数组-->字符串

转换流的编码应用

- 可以将字符按指定编码格式存储
- 可以对文本数据按指定编码格式来解读
- 指定编码表的动作由构造器完成

### 标准输入、输出流

方法：

```java
System.in://标准的输入流，默认从键盘输入

System.out://标准的输出流，默认从控制台输出

//System 类的 setIn(InputStream is) 方式重新指定输入的流

//System 类的 setOut(PrintStream ps) 方式重新指定输出的流。

/


```



从键盘输入字符串，要求将读取到的整行字符串转成大写输出。然后继续进行输入操作，直至当输入 e 或者 exit 时，退出程序。

实现：

```java
public static void main(String[] args) 
{
    BufferedReader br = null;
    try 
    {
        InputStreamReader isr = new InputStreamReader(System.in);
        br = new BufferedReader(isr);

        while (true) 
        {
            System.out.println("请输入字符串：");
            String data = br.readLine();
            if ("e".equalsIgnoreCase(data) || "exit".equalsIgnoreCase(data)) 
            {
                System.out.println("程序结束");
                break;
            }

            String upperCase = data.toUpperCase();
            System.out.println(upperCase);

        }
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally 
    {
        if (br != null) 
        {
            try 
            {
                br.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
    }
}
```

### 打印流

`PrintStream` 和 `PrintWriter` **说明：**

- 提供了一系列重载的 `print()` 和 `println()` 方法，用于多种数据类型的输出
- `System.out` 返回的是 `PrintStream` 的实例

如下：

```java
public void test2() 
{
    PrintStream ps = null;
    try 
    {
        FileOutputStream fos = new FileOutputStream(new File("D:\\IO\\text.txt"));
        // 创建打印输出流,设置为自动刷新模式(写入换行符或字节 '\n' 时都会刷新输出缓冲区)
        ps = new PrintStream(fos, true);
        if (ps != null) 
        {// 把标准输出流(控制台输出)改成文件
            System.setOut(ps);
        }


        for (int i = 0; i <= 255; i++) 
        { // 输出ASCII字符
            System.out.print((char) i);
            if (i % 50 == 0) 
            { // 每50个数据一行
                System.out.println(); // 换行
            }
        }


    } catch (FileNotFoundException e) 
    {
        e.printStackTrace();
    } finally 
    {
        if (ps != null) 
        {
            ps.close();
        }
    }

}
```

### 数据流

`DataInputStream` 和 `DataOutputStream` **作用：** 用于读取或写出基本数据类型的变量或字符串

**示例代码：**

将内存中的字符串、基本数据类型的变量写出到文件中。

```java
public void test3()
{
    //1.造对象、造流
    DataOutputStream dos = null;
    try 
    {
        dos = new DataOutputStream(new FileOutputStream("data.txt"));
        //数据输出
        dos.writeUTF("Bruce");
        dos.flush();//刷新操作，将内存的数据写入到文件
        dos.writeInt(23);
        dos.flush();
        dos.writeBoolean(true);
        dos.flush();
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally 
    {
        //3.关闭流
        if (dos != null)
        {
            try 
            {
                dos.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }
        }
    }
}
```

将文件中存储的基本数据类型变量和字符串读取到内存中，保存在变量中。

```java
/*
注意点：读取不同类型的数据的顺序要与当初写入文件时，保存的数据的顺序一致！
 */
@Test
public void test4()
{
    DataInputStream dis = null;
    try 
    {
        //1.造对象、造流
        dis = new DataInputStream(new FileInputStream("data.txt"));
        //2.从文件读入数据
        String name = dis.readUTF();
        int age = dis.readInt();
        boolean isMale = dis.readBoolean();

        System.out.println("name:"+name);
        System.out.println("age:"+age);
        System.out.println("isMale:"+isMale);
    } catch (IOException e) 
    {
        e.printStackTrace();
    } finally 
    {
        //3.关闭流
        if (dis != null)
        {

            try 
            {
                dis.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }
        }
    }
}
```

### 对象流

```java
ObjectOutputStream://内存中的对象--->存储中的文件、通过网络传输出去：序列化过程
ObjectInputStream://存储中的文件、通过网络接收过来 --->内存中的对象：反序列化过程
```

前提：

1. 需要实现接口：`Serializable`（标识接口）
2. 当前类提供一个全局常量：`serialVersionUID`（序列版本号）
3. 除了当前 `Person` 类需要实现 `Serializable` 接口之外，还必须保证其内部所属性也必须是可序列化的。（默认情况下，基本数据类型可序列化）

补充：`ObjectOutputStream` 和 `ObjectInputStream` 不能序列化 `static` 和 `transient` 修饰的成员变量

#### 序列化代码实现

将对象写入磁盘或进行网络传输

要求被序列化对象必须实现序列化

```java
public void testObjectOutputStream(){
    ObjectOutputStream oos = null;

    try {
        //1.创建对象，创建流
        oos = new ObjectOutputStream(new FileOutputStream("object.dat"));
        //2.操作流
        oos.writeObject(new String("我爱北京天安门"));
        oos.flush();//刷新操作

        oos.writeObject(new Person("王铭",23));
        oos.flush();

        oos.writeObject(new Person("张学良",23,1001,new Account(5000)));
        oos.flush();

    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        if(oos != null){
            //3.关闭流
            try {
                oos.close();
            } catch (IOException e) {
                e.printStackTrace();
            }

        }
    }

}
```



反序列化：将磁盘的对象数据源读出

```java
public void testObjectInputStream()
{
    ObjectInputStream ois = null;
    try 
    {
        ois = new ObjectInputStream(new FileInputStream("object.dat"));

        Object obj = ois.readObject();
        String str = (String) obj;

        Person p = (Person) ois.readObject();
        Person p1 = (Person) ois.readObject();

        System.out.println(str);
        System.out.println(p);
        System.out.println(p1);

    } catch (IOException e) {
        e.printStackTrace();
    } catch (ClassNotFoundException e) {
        e.printStackTrace();
    } finally 
    {
        if(ois != null)
        {
            try 
            {
                ois.close();
            } catch (IOException e) 
            {
                e.printStackTrace();
            }

        }
    }
}

```

### 任意存取文件流

`RandomAccessFile` 直接继承于 `java.lang.Object` 类，实现了 `DataInput` `和DataOutput` 接口

`RandomAccessFile` 既可以作为一个输入流，又可以作为一个输出流

`RandomAccessFile` 类支持“随机访问”的方式，程序可以直接跳到文件的任意地方来读、写文件

- 支持只访问文件的部分内容
- 可以向已存在的文件后追加内容

`RandomAccessFile` 对象包含一个记录指针，用以标示当前读写处的位置

`RandomaccessFile` 类对象可以自由移动记录指针：

- `long getFilePointer()`：获取文件记录指针的当前位置
- ` void seek(long pos)`：将文件记录指针定位到 `pos` 位置

构造器：

```java
public RandomAccessFile(File file,String mode) public RandomAccessFile(String name,String mode)
```

如何使用：

如果 `RandomAccessFile` 作为输出流时，写出到的文件如果不存在，则在执行过程中自动创建。

如果写出到的文件存在，则会对原文件内容进行覆盖。（默认情况下，从头覆盖）

可以通过相关的操作，实现 `RandomAccessFile` **“插入”**数据的效果。借助 `seek(int pos)` 方法

创建 `RandomAccessFile` 类实例需要指定一个 `mode` 参数，`该参数指定RandomAccessFile` 的访问模式:

- r：以只读方式打开
- rw：打开以便读取和写入
- rwd：打开以便读取和写入；同步文件内容的更新
- rws：打开以便读取和写入；同步文件内容和元数据的更新

如果模式为只读 r ,则不会创建文件，而是会去读取一个已经存在的文件,读取的文件不存在则会出现异常。如果模式为 rw 读写,文件不存在则会去创建文件，存在则不会创建。



使用：

```java
public void test1() {

    RandomAccessFile raf1 = null;
    RandomAccessFile raf2 = null;
    try {
        //1.创建对象，创建流
        raf1 = new RandomAccessFile(new File("test.jpg"),"r");
        raf2 = new RandomAccessFile(new File("test1.jpg"),"rw");
        //2.操作流
        byte[] buffer = new byte[1024];
        int len;
        while((len = raf1.read(buffer)) != -1){
            raf2.write(buffer,0,len);
        }
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        //3.关闭流
        if(raf1 != null){
            try {
                raf1.close();
            } catch (IOException e) {
                e.printStackTrace();
            }

        }
        if(raf2 != null){
            try {
                raf2.close();
            } catch (IOException e) {
                e.printStackTrace();
            }

        }
    }
}
```

- 创建文件对象，创建相应的流
- 处理流数据
- 关闭流
- 用try-catch-finally处理异常

