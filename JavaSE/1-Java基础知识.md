# Java基础知识

## Java语法基础

### 数据类型

  为什么Java会有数据类型呢，我之前开发用的是脚本语言对数据类型没有明确的区分，所以数据类型的意义？  
>  “子之武城，闻弦歌之声。夫子莞尔而笑，曰：‘割鸡焉用牛刀。’杀鸡的刀用来杀鸡，宰牛的刀用来宰牛，用宰牛的刀杀鸡，岂不大材小用？  
>  正是有了类型的区分，我们才可以根据不同的类型，确定其不同的功能，然后“各司其职”，不出差错。

#### 八种基本数据类型

* 数据类型  
在Java之中数据类型一共分为两大类：基本数据类型、引用数据类型。
在Java中规定了8种基本数据类型变量来存储整数、浮点数、字符和布尔值，如下:
![数据类型](http://graph.guoyw.com/Java_notes/JavaSE/%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B.png)

* 取值范围
![各数据类型范围](http://graph.guoyw.com/Java_notes/JavaSE/%E5%8F%96%E5%80%BC%E8%8C%83%E5%9B%B4.png)

#### 类型转换

* 自动类型转换
  假设参与某种运算有两个不同的操作数(操作数1和操作数2)，二者具有不同的数据类型，在运算操作之前，它们需要转换为同一数据类型，其相互转换的规则如下表所示。
  ![数据类型相互转换规则](http://graph.guoyw.com/Java_notes/JavaSE/%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E8%87%AA%E5%8A%A8%E8%BD%AC%E6%8D%A2.png)
  >现在，我们可以给出自动数据类型转型的规律：byte→short→int→long→float→double，按照范围由小到大实现自动转型操作。
  
* 强制类型转换
   强制类型转换，语法如下：
   > (欲转换的数据类型)变量名称;  
   
   若将一个超出该变量可表示范围的值赋给这个变量，这种转换称为缩小转换。由于在转换的过程中可能会丢失数据的精确度，因此Java并不会“自动”做这些类型的转换，此时就必须要做强制性的转换，例如 int x = (int)10.35(结果x=10)，将double类型的值(10.35)强制转换为int类型(10)，这样也丢失了很多的信息。
 
#### 自动拆箱、装箱
 自动拆箱、装箱是从JDK1.5开始才有的特性，其实它主要就是指基本类型与包装类的自动转换。
 
 * 如int 与Integer类型。
   int 是基本类型，而Integer是int的包装类，在JDK1.5之前，int类型的值是不能直接赋给Integer类型的值 的，也就是说 Integer integer = 5; 会报错，因为5是基本类型，而Integer是包装类，Integer的正确定义方式为： 
    Integer integer = new Integer(5);  
    但是，从基本类型转换成包装类是经常使用的操作，尤其是Integer与int的转换很是频繁。  
    所以在JDK1.5开始，它们之间的转换不在须要程序员再去进行转换了，JDK已经将它自动进行了转换，这种操作就叫自动拆箱、装箱。
    ```
    int i = 5;
    Integer ii = i;     //这种写法在JDK1.5及以后的版本是正确的，因为系统会自动将int向Integer进行转换，这种操作就叫自动装箱。

    int j = ii;         //这种写法是将Integer的值自动转换成了int基本类型，这种自动转换的方法就叫自动拆箱。
    ```
    
 * 不只是int与Integer可以自动转换，八大基本类型都可以, 以下是八大基本类型及对应的包装炻  
    基本类型 byte short int long float double char boolean   
    包装类型 Byte Short Integer Long Float Double Character Boolean  

* 其中，int与Integer的转换最多也最频繁，所以有一点要注意，也是面试时常问到的问题： 
  * int与Integer的区别： 
    int的默认值 为0，而Integer的默认值为null,在使用Integer前需要初始化。 
    int是基本类型，而Integer是包装类，可以自动 拆箱、拆箱，Integer封装了很多的方法
    
### 变量
  * 常量
    final 数据类型 常量名称 [=值];
    名称通常使用大写字母，例如PI、YEAR等
    必须要在常量声明时对其进行初始化，一旦初始化后，就无法再次对这个常量进行赋值。
  
  * 变量初始化
    > 变量是利用声明的方式，将内存中的某个内存块保留下来以供程序使用，其内的值是可变的。可声明的变量数据类型有整型(int)、字符型(char)、浮点型(float或double)，也可以是其他的数据类型(如用户自定义的数据类型——类)。  
    
    * 声明变量的作用
      (1)指定在内存中分配空间大小。  
      (2)规定这个变量所能接受的运算。  
    * 变量的命名规则
      变量也是一种标识符，所以它也遵循标识符的命名规则。  
    * 变量的作用范围
      * 成员变量
        在类体中定义的变量为成员变量。它的作用范围为整个类，也就是说在这个类中都可以访问到定义的这个成员变量。
        ```
          public class TestMemVar4_3 {
              static int var= 1; //定义一个成员变量
              public static void main(String[] args){
                 System.out.println("成员变量 var的值是："+var);
              }
              }
        ```
      * 局部变量
        在一个函数(或称方法)或函数内代码块(code block)中定义的变量称为局部变量，局部变量在函数或代码块被执行时创建，在函数或代码块结束时被销毁。局部变量在进行取值操作前必须被初始化或赋值操作，否则会出现编译错误！
        ```
        //main方法参数列表定义的局部变量args
        public static void main(String[] args)  {
           int sum= 0; //main方法体内定义的局部变量 sum
           for (int i= 1; i<= 5; i++) { // for循环体内定义的局部变量 i
               sum= sum+ i;
               System.out.println("i= "+ i+ ", sum= "+ sum);
           }
           }
        ```
**  注意事项： **
  >声明在方法中的变量在使用时必须要初始化;  
  
  ```
   对于全局变量如果不赋值，会有默认值如果在方法中有:
   public void test(){
   int i;
   System.out.print(i);
  }
  会报错。
  
  如果在类中有
  public class Test{
    int i;
    public void test(){
      System.out.print(i);
    }
  }
  则会给i初始值0。
  ```

### 枚举类型Enum
### 字符串String
   * 传送门
    [深入理解Java中的String](https://www.cnblogs.com/xiaoxi/p/6036701.html)
### 数组
    在Java中，数组也可以视为一种数据类型。它本身是一种引用类型;  
    Java的数组既可以存储基本类型的数据，也可以存储引用数据类型的数据。  

   * 传送门
    [Java 数组](http://www.runoob.com/java/java-array.html)
     
### 保留字&关键字
    就是用于给程序中的变量、类、方法命名的符号;
### 标识符
    标识符就是用于Java程序中变量，类，方法等命名的符号。
    > 使用标识符时，需要遵守几条规则：
        1. 标识符可以由字母，数字，下划线（——），美元（$）组成，但是不能包含@，%，空格等其他的特殊符号，不能以数字开头。例如 123name 就是不合法的  
        2.标识符不能是Java关键字和保留字（Java预留的关键字，或者以后升级版本中有可能作为关键字），但可以包含关键字和保留字~例如：不可以使用void 作为标识符，但是Myvoid 可以  
        3.标识符是严格却分大小写的，所以一定要分清alibaba和ALIbaba是两个不同的标识符哦  
        4.标识符的命名最好能反应出其作用，做到见名知意  
### 运算符
  * 一元运算符  
    ![一元运算符](http://graph.guoyw.com/Java_notes/JavaSE/%E4%B8%80%E5%85%83%E8%BF%90%E7%AE%97%E7%AC%A6.png)
    
  * 逻辑运算符
    逻辑运算符只对布尔型操作数进行运算并返回一个布尔型数据。也就是说，逻辑运算符的操作数和运行结果只能是真(true)或者假(false)。常见的逻辑运算符有3个，即与(&&)、或(||)、非(！)，如下  
    ![逻辑运算符](http://graph.guoyw.com/Java_notes/JavaSE/%E9%80%BB%E8%BE%91%E8%BF%90%E7%AE%97%E7%AC%A6.png)  
    我们需要逻辑“与”操作和“或”操作的两个操作数均需要运算，这时我们就需要使用避免短路的逻辑运算符——“&”和“|”，它们分别是可短路的逻辑运算符(&&和||)一半的字符。  
    ```
      if (1== 1 || 1 / 0== 0) { // true ||错误= true
        System.out.println("3:条件满足！ ") ;
      }
     //含有非法操作符(1/0)，但是短路操作符“||”的第一个操作数为(1==1)为true，所以第二个操作数直接被编译器“忽略”，最终if语句内逻辑判断值为true，所以1打印输出“条件满足”。
    ```
    
  * 位运算符
    位操作是指对操作数以二进制位(bit)为单位进行的运算。其运算的结果为整数。位操作的第一步是把操作数转换为二进制的形式，然后按位进行布尔运算，运算的结果也为二进制数。
    ![位运算符](http://graph.guoyw.com/Java_notes/JavaSE/%E4%BD%8D%E8%BF%90%E7%AE%97%E7%AC%A6.png)  
    
  * 三元运算符  
    三元(Ternary)运算符也称三目运算符，它的运算符是“?:”，有三个操作数。操作流程如下：首先判断条件，如果条件满足，就会赋予一个变量一个指定的内容(冒号：之前的)，不满足会赋予变量另外的一个内容(冒号之后的)，其操作语法如下。
    >数据类型变量=布尔表达式 ? 条件满足设置内容:条件不满足设置内容;
    
  * 关系运算符与if语句 
    * if语句通常用于某个条件进行真(true)、假(false)识别。if语句的格式如下。  
      >if (判断条件)
      >语句；
      
      如果括号中的判断条件成立，就会执行后面的语句；若是判断条件不成立，则后面的语句就不会被执行。  
    * 关系运算符  
      ![关系运算符](http://graph.guoyw.com/Java_notes/JavaSE/%E5%85%B3%E7%B3%BB%E8%BF%90%E7%AE%97%E7%AC%A6.png)
      
  * 括号运算符
    括号()也是Java的运算符；
    >() 提高括号中表达式的优先级
    
  * 运算符的优先级
    下表列出了各个运算符的优先级的排列，数字越小的表示优先级越高(优先级排名靠前)。
    ![运算符优先级](http://graph.guoyw.com/Java_notes/JavaSE/%E8%BF%90%E7%AE%97%E7%AC%A6%E4%BC%98%E5%85%88%E7%BA%A7.png)

## 流程控制
  流程控制 就是程序只有一个入口，也只有一个运行出口。程序中使用了上面这些结构到底有什么好处呢？这些单一的入口、出口可让程序可控、易读、好维护。
### 程序逻辑
  * 顺序结构。
    * 选择结构。
      * if语句
      * if..else语句
      * if..else if..else语句
      * 多重选择—switch语句
  * 循环结构。
    * while循环
    * do..while循环
    * for循环
    * foreach循环
    * 循环嵌套
    * 循环的跳转
      * break;   //其作用是使程序立即退出该循环结构。
      * continue; //执行continue语句将结束本次循环而立即测试循环的条件，以决定是否进行下一次循环。
      * return; // return语句可以使程序的流程离开return语句所在的方法。