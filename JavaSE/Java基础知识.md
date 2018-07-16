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
   * 1.int的默认值 为0，而Integer的默认值为null,在使用Integer前需要初始化。 
   * 2.int是基本类型，而Integer是包装类，可以自动 拆箱、拆箱，Integer封装了很多的方法，
    
 
 
