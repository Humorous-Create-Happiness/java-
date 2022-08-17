# java 基础语法 #

## 注释(不会执行) ##

1.单行注释

   ```java
   //输出HELLOWORLD
   //    <--  双斜杠开头就是注释
   ```

2.多行注释

```java
/* 多行注释
   多行注释
           */
```

3.文件注释

```java
/**    @description          */
```

## 标识符 ##

![图片](C:\Users\Lenovo\Documents\360截图\360截图20220724152814542.jpg)

```java
```

除了上述的关键字外，标识符只能以大写开头，美元开头，_ （下划线后面可以加数字）开头

```java
String Mom = "niubi";
String _123Mom = "niubi";
String $Mom = "niubi";
```

## 数据类型 ##

（java是强类型语言，必须先定义在使用，定义后不在改变）

```java
String a; //输出后报错
String a = 10 //输出后报错
String a = "666"  //行了
```



###    基本类型 ###

​           整数类型   byte   short  int (21亿)    long 

```java 
  byte num1 = 127；
  short num2 =  199999；
  int num3 = 210000000000；
  long num4 = 978237473427L；
```

​           小数类型 float double

```java
  float num5 = 3.1F；
  double num6 = 3.14159265； 
```

​            字符类型 char

```java
  char name = "国"；
  String name2 = "一堆字"；
```

​           布尔类型 boolean

​           

###    引用类型 ###

​            类

​            接口

​            数组

​          小知识：一字节(byte)等于八位（bit）



​          整数拓展      二进制（0b开头）八进制（0开头）十六进制(0x开头)

```java
     int i = 10;
     int i1 = 010//(八进制)
     int i2 = 0b10 //(要我说吗)
```

​         请不要用浮点数进行比较!

​         请不要用浮点数进行比较!

​         请不要用浮点数进行比较!



​           字符拓展     int(字符) == ASCII码

​           布尔值扩展     if (flag==true){}

​                                    if(flag){}

## 类型转换

​        转换优先级（不能对布尔值进行转换）

​       byte > short > int > long > float > double > char

```java
    int i = 128;
    byte b = (byte)i;  //手动转化（低到高），内存可能溢出
    double c = i;     //自动转化（高到低）
    
    char c = "a";
    int d = c+1; 
    //输出98
    char e = (char)d;
```

​      *数字可以用下划线分割*

​      注意数据溢出





## 变量与常量   ##

变量的声明

      ```java
      public class Hey{
          public static void main(String[] args){
              int a=1,b=2,c=3;
              String x = "HEY";
              char d = 'a';
              double e = 2.34;
          }
          
      }
      ```

变量的作用域

```java
public class Demo08{
    static double = 250;   //类变量
    //
    String name;
    int age;       //实例变量,从属于对象，不定义有默认值                            0,0.0，flase,null
    //main方法
    public static void main(String[] args){
        i= 1;    //局部变量
        Sout(i);
        
        Demo08 demo08 = new demo08();
        Sout(age);
        Sout(name);   //实例变量在main函数中的引用
        
        Sout(double)  //类变量在main函数的引用
    }
    
        
        
        
    //其他声明方式
    public void add(){
        
    }
}
```



常量的使用

```java
public class Demo09{
    static final double PI = 3.14;   //final改变常量
    final static  int P = 0;         //顺序不影响
    
}
```



命名规范

​     1.命名需要见名知意；

​     2.变量要满足驼峰原则；appStone

​     3.常量的命名需要大写：MAIN



## 运算符

算术运算符 + ，- ，* ，/ , % , ++ , -- 

赋值运算符 =

关系运算符 < , > , >= , <= ，==  , != , instancef

逻辑运算符&&， || ，！

  Math. pow(2,3)                          使用工具操作

```java
Sout("a && b:"+(a&&b));
Sout("a || b:"+(a||b));
Sout("!a && b:"+(!a&&b));

int c=5;
boolean d =(c<4)&&(c++<6);
Sout (d)
Sout (c)   c=5 //c的值没有变化，d的后续不执行
```



位运算符 >> , << ,  >>> ,|

```java
 a = 0011 1100;
 b = 0100 0110;     //不经定义就是位运算
 a&b = 0000 0100    //&: 都为1是取1
 a|b = 0111 1110    //|:都为0时取0
 a^b = 0111 1010    //^:相同取0，相反取1
 ~b =1011 1001      //~:取反
 <<    *2      //左移       
 >>    /2      //右移
```



字符串连接符

```java
int a=20,b=30;
Sout(""+a+b);---------50
Sout(a+b+"");---------2030
```



条件运算符

```java
(条件)?(条件满足的值):(条件不满足的值)
```



扩展赋值运算符



## 包机制

包的本质就是文件夹

```java
package  pkg1[.pkg2[.pkg3]];
improt  pkg1[.pkg2].(classname|*);     //*号导入包下所有类

```



### JavaDoc

生成API文档

```java
/**
@author    作者
@version   版本号
@since
@param
@return
*/

public class Doc{
    
    String name;
    
    public String test(String name) throws exception{
        return name;
    }
}

//javaDoc 
```























































