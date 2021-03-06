# Java面向对象基础

  面向对象的三个重要特征(封装性、继承性、多态性)，以及声明创建类和对象(数组)的方法。  
  软件设计：采用自顶向下、逐步求精及模块化的程序设计方法，使用三种基本控制结构构造程序，任何程序都可由顺序、选择、循环这三种基本控制结构来构造。
  结构化程序设计方法可以用一句话概括：程序=算法+数据结构。
  按照面向对象思想可以理解为：程序=对象+消息传递。（实现：重用性、灵活性和扩展性）

  * 面向过程编程 与 面相对象编程 比较
    ![面向过程编程与面相对象编程比较](http://graph.guoyw.com/Java_notes/JavaSE/%E9%9D%A2%E7%9B%B8%E8%BF%87%E7%A8%8B%E4%B8%8E%E5%AF%B9%E8%B1%A1.png)
  * 两种编程范式之间的联系
     面向对象是在面向过程的基础上发展而来的，只是添加了它独有的一些特性。面向对象程序中的对象就是由数据和方法构成，所以完整的面向对象概念应该是:
     对象=数据+方法
     更进一步的可以描述为，
     程序=对象+消息传递=(数据+方法)+消息传递

## 类与对象
### 类和对象的关系
  * 类
    * 具有相同属性及相同行为的一组对象称为类(class)。
    * 在面向对象程序设计中，类是一个独立的单位，它有一个类名，其内部包括成员变量，用于描述对象的属性；还包括类的成员方法，用于描述对象的行为。
    * 在Java程序设计中，类被认为是一种抽象的数据类型，这种数据类型不但包括数据，还包括方法，这大大地扩充了数据类型的概念。
    * 类是一个抽象的概念，要利用类的方式来解决问题，必须用类创建一个实例化的对象，然后通过对象去访问类的成员变量，去调用类的成员方法来实现程序的功能。
    * 一个类可创建多个类对象，它们具有相同的属性模式，但可以具有不同的属性值。Java程序为每一个对象都开辟了内存空间，以便保存各自的属性值。
  * 对象
    * 对象(object)是类的实例化后的产物。
    * 对象的特征分为静态特征和动态特征两种。
      * 静态特征指对象的外观、性质、属性等。
      * 动态特征指对象具有的功能、行为等。
    * 一个对象由一组属性和一系列对属性进行操作的方法构成。
  * 类和对象的关系
    * 类是对某一类事物的描述，是抽象的、概念上的定义；
    * 对象是实际存在的该类事物的个体，因而也称作实例(instance)。
### 类的声明于定义
  类在使用之前，必须先声明它，然后才可以声明变量，并创建对象。语法如下：
  >[标识符]class类的名称{
  >  //类的成员变量
  >  //类的方法
  >}

  * 类的标识符--访问控制符
    * default (默认模式) 方法、类不需要添加标识符。表示只允许同一个包内(package)是可以访问的；
    * private (私有的) 表示此成员或方法只能被自己类中的方法使用，而不能被外部类或对象直接使用。
    * protected(保护)：具有子类访问权限。则此类中属性或方法可以被同一包下的类使用，也可以被不同包下的子类使用，但不能被不同包下的其他类使用。
    * public(公共)：具有公共访问权限。如果类中的属性或方法被public修饰，则此类中的属性或方法可以被任何类调用。
  ![访问控制符](http://graph.guoyw.com/Java_notes/JavaSE/%E6%8E%A7%E5%88%B6%E7%AC%A6.png)

#### 对象声明
  * 声明语法：
    > [修饰符] 类名 对象名 = new 类名();
  * 创建原理：
  ![创建原理](http://graph.guoyw.com/Java_notes/JavaSE/%E5%AF%B9%E8%B1%A1%E5%88%9B%E5%BB%BA%E5%8E%9F%E7%90%86.png)
  * 对象的比较
    * “==” 运算符用于比较两个对象的内存地址值(引用值)是否相等。
    * equals() 方法用于比较两个对象的内容是否一致。

### 静态
> static方法就是没有this的方法。在static方法内部不能调用非静态方法，反过来是可以的。而且可以在没有创建任何对象的前提下，仅仅通过类本身来调用static方法。这实际上正是static方法的主要用途。
> 一句话来描述就是：方便在没有创建对象的情况下来进行调用（方法/变量）。

  * static方法
    > static方法一般称作静态方法，由于静态方法不依赖于任何对象就可以进行访问，因此对于静态方法来说，是没有this的，因为它不依附于任何对象，既然都没有对象，就谈不上this了。
     并且由于这个特性，在静态方法中不能访问类的非静态成员变量和非静态成员方法，因为非静态成员方法/变量都是必须依赖具体的对象才能够被调用。
     但是要注意的是，虽然在静态方法中不能访问非静态成员方法和非静态成员变量，但是在非静态成员方法中是可以访问静态成员方法/变量的.
  * static变量
    > static变量也称作静态变量，静态变量和非静态变量的区别是：静态变量被所有的对象所共享，在内存中只有一个副本，它当且仅当在类初次加载时会被初始化。
     而非静态变量是对象所拥有的，在创建对象的时候被初始化，存在多个副本，各个对象拥有的副本互不影响。
     static成员变量的初始化顺序按照定义的顺序进行初始化。
  * static代码块
    > static关键字还有一个比较关键的作用就是 用来形成静态代码块以优化程序性能。
     static块可以置于类中的任何地方，类中可以有多个static块。在类初次被加载的时候，会按照static块的顺序来执行每个static块，并且只会执行一次。
     为什么说static块可以用来优化程序性能，是因为它的特性:只会在类加载的时候执行一次。

举个例子：
```
  public class Test {
      Person person = new Person("Test");
      static{
          System.out.println("test static");
      }

      public Test() {
          System.out.println("test constructor");
      }

      public static void main(String[] args) {
          new MyClass();
      }
  }

  class Person{
      static{
          System.out.println("person static");
      }
      public Person(String str) {
          System.out.println("person "+str);
      }
  }


  class MyClass extends Test {
      Person person = new Person("MyClass");
      static{
          System.out.println("myclass static");
      }

      public MyClass() {
          System.out.println("myclass constructor");
      }
  }

  结果：
      test static
      myclass static
      person static
      person Test
      test constructor
      person MyClass
      myclass constructor
```
> 首先加载Test类，因此会执行Test类中的static块。接着执行new MyClass()，而MyClass类还没有被加载，因此需要加载MyClass类。
 在加载MyClass类的时候，发现MyClass类继承自Test类，但是由于Test类已经被加载了，所以只需要加载MyClass类，那么就会执行MyClass类的中的static块。
 在加载完之后，就通过构造器来生成对象。
 而在生成对象的时候，必须先初始化父类的成员变量，因此会执行Test中的Person person = new Person()，而Person类还没有被加载过，因此会先加载Person类并执行Person类中的static块，接着执行父类的构造器，完成了父类的初始化，然后就来初始化自身了，因此会接着执行MyClass中的Person person = new Person()，最后执行MyClass的构造器。


传送门：[Java中的static关键字解析](https://www.cnblogs.com/dolphin0520/p/3799052.html)

### 构造函数
  在每一个类中定义，与类名相同的方法，使用关键字new实例化的时候被调用。
  * 构造函数的特点
    * 一个对象建立，构造函数只运行一次。
    * 函数名与类名相同
    * 不用定义返回值类型。（不同于void类型返回值，void是没有具体返回值类型；构造函数是连类型都没有）
    * 不可以写return语句。（返回值类型都没有，也就不需要return语句了）
    * 构造函数也是函数的一种，同样具备函数的重载（Overloding）特性。

### 包
  java包的作用是为了区别类名的命名空间。
  * 把功能相似或相关的类或接口组织在同一个包中，方便类的查找和使用
  * 如同文件夹一样，包也采用了树形目录的存储方式
  * 包也限定了访问权限，拥有包访问权限的类才能访问某个包中的类。
  * 使用 "import" 语句，导入Java 程序包
  * 通常，一个公司使用它互联网域名的颠倒形式来作为它的包名.例如：互联网域名是 runoob.com，所有的包名都以 com.runoob 开头。

### 内部类
  Java中，可以将一个类定义在另一个类里面或者一个方法里面，这样的类称为内部类。内部类一般来说包括这四种:
  * 成员内部类
  * 局部内部类
  * 匿名内部类
  * 静态内部类

  内部类的使用场景和好处：
  * 每个内部类都能独立的继承一个接口的实现，所以无论外部类是否已经继承了某个(接口的)实现，对于内部类都没有影响。内部类使得多继承的解决方案变得完整，
  * 方便将存在一定逻辑关系的类组织在一起，又可以对外界隐藏。

传送门：[Java内部类详解](https://www.cnblogs.com/dolphin0520/p/3811445.html)

### 方法
  * 方法中的形参与实参
  ![方法中的形参与实参](http://graph.guoyw.com/Java_notes/JavaSE/%E5%BD%A2%E5%8F%82%E4%B8%8E%E5%AE%9E%E5%8F%82.png)
  形参变量隶属于方法体，是方法的局部变量，只有在被调用的时候才会被创建，临时性分配内存，结束后释放内存。
  方法在调用是，实参的数量类型和形参严格保持一次。
  * 方法重载
    * 方法名相同
    * 方法的参数列表不同（参数个数、参数类型、参数顺序、至少有一项不同）
    * 方法的返回值类型和修饰符不做要求，可以相同，也可以不同。

## 面向对象三大特性

### 封装
#### 概念
  封装性(encapsulation)：封装是一种信息隐蔽技术，它体现于类的说明，是对象的重要特性。  
  封装使数据和加工该数据的方法(函数)封装为一个整体，以实现独立性很强的模块，使得用户只能见到对象的外特性(对象能接受哪些消息，具有哪些处理能力)，而对象的内特性(保存内部状态的私有数据和实现加工能力的算法)对用户是隐蔽的。  
  封装的目的在于把对象的设计者和对象的使用者分开，使用者不必知晓其行为实现的细节，只须用设计者提供的消息来访问该对象。
  
  
### 继承
#### 概念
  继承性：继承性是子类共享其父类数据和方法的机制。它由类的派生功能体现。
  一个类直接继承其他类的全部描述，同时可修改和扩充。继承具有传递性。继承分为单继承(一个子类有一父类)和多重继承(一个类有多个父类)。 
  类的对象是各自封闭的，如果没继承性机制，则类的对象中的数据、方法就会出现大量重复。继承不仅支持系统的可重用性，而且还促进系统的可扩充性。

传送门：[Java：类与继承](https://www.cnblogs.com/dolphin0520/p/3803432.html)

 * 属性静态绑定、可继承的方法动态绑定
   * 父类子类有相同属性时，是在父类基础上添加而非覆盖。
   * 方法和属性调用时，是从当前类开始一直向上查找。找到就停止。
   * 调用的是谁的方法，查找的起点就是谁。所以，准确判断是哪个类的方法很重要。

   ```
     public class Test {
         public static void main(String[] args)  {
             Shape shape = new Circle();
             System.out.println(shape.name);
             shape.printType();
             shape.printName();
             System.out.println(shape.getName());
             System.out.println(shape.getCName());

         }
     }

     class Shape {
         public String name = "shape";

         public Shape(){
             System.out.println("shape constructor");
         }

         public void printType() {
             System.out.println("this is shape");
         }

         public static void printName() {
             System.out.println("shape");
         }

         public String getName(){
             return name;
         }
     }

     class Circle extends Shape {
         public String name = "circle";

         public Circle() {
             System.out.println("circle constructor");
         }

         public void printType() {
             System.out.println("this is circle");
         }

         public static void printName() {
             System.out.println("circle");
         }
         public String getCName(){
             return name;
         }
     }

     // 输出 结果为：
     shape constructor
     circle constructor
     shape
     this is circle
     shape
     shape
     circle
   ```
  
### 多态
#### 概念
  多态性：对象根据所接收的消息而做出动作。
  同一消息被不同的对象接受时可产生完全不同的行动，这种现象称为多态性。
  利用多态性用户可发送一个通用的信息，而将所有的实现细节都留给接受消息的对象自行决定，如是，同一消息即可调用不同的方法。

  > 如：同样是run方法，飞鸟调用时是飞，野兽调用时是奔跑。
  多态性的实现受到继承性的支持，利用类继承的层次关系，把具有通用功能的协议存放在类层次中尽可能高的地方，而将实现这一功能的不同方法置于较低层次，
  这样，在这些低层次上生成的对象就能给通用消息以不同的响应。在OOPL中可通过在派生类中重定义基类函数(定义为重载函数或虚函数)来实现多态性。

 * 多态存在的三个必要条件
   * 要有继承；
   * 要有重写；
   * 父类引用指向子类对象 (继承中的例子)
 * 多态的好处
   * 可替换性（substitutability）:多态对已存在代码具有可替换性。例如，多态对圆Circle类工作，对其他任何圆形几何体，如圆环，也同样工作。
   * 可扩充性（extensibility）:多态对代码具有可扩充性。增加新的子类不影响已存在类的多态性、继承性，以及其他特性的运行和操作。实际上新加子类更容易获得多态功能。例如，在实现了圆锥、半圆锥以及半球体的多态基础上，很容易增添球体类的多态性。
   * 接口性（interface-ability）:多 态是超类通过方法签名，向子类提供了一个共同接口，由子类来完善或者覆盖它而实现的。
   * 灵活性（flexibility）:它在应用中体现了灵活多样的操作，提高了使用效率。
   * 简化性（simplicity）:多态简化对应用软件的代码编写和修改过程，尤其在处理大量对象的运算和操作时，这个特点尤为突出和重要。

传送门：[理解Java的多态](https://www.cnblogs.com/chenssy/p/3372798.html)


## 接口
  * 接口的特性
    传送门：[接口的特性](http://www.cnblogs.com/xdp-gacl/p/3651121.html)
  * 接口与抽象类
    传送门：[接口与抽象类](http://www.cnblogs.com/dolphin0520/p/3811437.html)
  * 对象克隆
  * 接口与回调
    传送门：[Java接口回调一般用法](https://blog.csdn.net/jonsnoww/article/details/68932292)


## 重载与重写的区别
  * 重写方法的规则：
     * 参数列表必须完全与被重写的方法相同，否则不能称其为重写而是重载。
     * 返回的类型必须一直与被重写的方法的返回类型相同，否则不能称其为重写而是重载。
     * 访问修饰符的限制一定要大于被重写方法的访问修饰符（public>protected>default>private）
     * 重写方法一定不能抛出新的检查异常或者比被重写方法申明更加宽泛的检查型异常。例如：父类的一个方法申明了一个检查异常IOException，在重写这个方法是就不能抛出Exception,只能抛出IOException的子类异常，可以抛出非检查异常。

  * 而重载的规则：
     * 必须具有不同的参数列表；
     * 可以有不同的返回类型，只要参数列表不同就可以了；
     * 可以有不同的访问修饰符；
     * 可以抛出不同的异常；

在继承预计口实现中：
   * 重写是动态绑定
   * 重载是静态绑定

 方法查找规则：  
     (1)在常量池中找到方法调用的符号引用  
     (2)查看Person的方法表，得到speak方法在该方法表的偏移量（假设为15），这样就得到该方法的直接引用。  
     (3)根据this指针确定方法接收者(girl)的实际类型  
     (4)根据对象的实际类型得到该实际类型对应的方法表，根据偏移量15查看有无重写（override）该方法，如果重写，则可以直接调用；如果没有重写，则需要拿到按照继承关系从下往上的基类（这里是Person类）的方法表，同样按照这个偏移  
传送门：[例子-> 看2.1 接口举例](http://www.cnblogs.com/xdp-gacl/p/3651121.html)
