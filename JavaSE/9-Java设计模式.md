# Java 设计模式

## 六大原则

  - 开闭原则（Open Close Principle）
    >开闭原则就是说对扩展开放，对修改关闭。  
    在程序需要进行拓展的时候，不能去修改原有的代码，实现一个热插拔的效果。  
    所以一句话概括就是：为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，我们需要使用接口和抽象类，后面的具体设计中我们会提到这点。  

  - 里氏代换原则（Liskov Substitution Principle）
    >里氏代换原则(Liskov Substitution Principle LSP)面向对象设计的基本原则之一。  
    里氏代换原则中说，任何基类可以出现的地方，子类一定可以出现。  
    LSP是继承复用的基石，只有当衍生类可以替换掉基类，软件单位的功能不受到影响时，基类才能真正被复用，而衍生类也能够在基类的基础上增加新的行为。  
    里氏代换原则是对“开-闭”原则的补充。实现“开-闭”原则的关键步骤就是抽象化。而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范.

  - 依赖倒转原则（Dependence Inversion Principle）
    >这个是开闭原则的基础，具体内容：真对接口编程，依赖于抽象而不依赖于具体。

  - 接口隔离原则（Interface Segregation Principle）
    >这个原则的意思是：使用多个隔离的接口，比使用单个接口要好。还是一个降低类之间的耦合度的意思，从这儿我们看出，其实设计模式就是一个软件的设计思想，从大型软件架构出发，为了升级和维护方便。所以上文中多次出现：降低依赖，降低耦合。

  - 迪米特法则（最少知道原则）（Demeter Principle）
    >为什么叫最少知道原则，就是说：一个实体应当尽量少的与其他实体之间发生相互作用，使得系统功能模块相对独立

  - 合成复用原则（Composite Reuse Principle）
    >原则是尽量使用合成/聚合的方式，而不是使用继承。
      
## 设计模式

### 创建模式
  - 抽象工厂模式
   >* 工厂方法模式有一个问题就是，类的创建依赖工厂类，也就是说，如果想要拓展程序，必须对工厂类进行修改，这违背了闭包原则，所以，从设计角度考虑，有一定的问题，如何解决？
   >* 就用到抽象工厂模式，创建多个工厂类，这样一旦需要增加新的功能，直接增加新的工厂类就可以了，不需要修改之前的代码.
   >* 其实这个模式的好处就是，如果你现在想增加一个功能：发及时信息，则只需做一个实现类，实现Sender接口，同时做一个工厂类，实现Provider接口，就OK了，无需去改动现成的代码。
  - 工厂方法模式
    - 普通工厂模式
      >普通工厂模式，就是建立一个工厂类，对实现了同一接口的一些类进行实例的创建
    - 多个工厂方法模式
      >多个工厂方法模式，是对普通工厂方法模式的改进，在普通工厂方法模式中，如果传递的字符串出错，则不能正确创建对象，而多个工厂方法模式是提供多个工厂方法，分别创建对象
    - 静态工厂方法模式
      >静态工厂方法模式，将上面的多个工厂方法模式里的方法置为静态的，不需要创建实例，直接调用即可。

   **凡是出现了大量的产品需要创建，并且具有共同的接口时，可以通过工厂方法模式进行创建。在以上的三种模式中，第一种如果传入的字符串有误，不能正确创建对象，第三种相对于第二种，不需要实例化工厂类，所以，大多数情况下，我们会选用第三种——静态工厂方法模式**

  - 单例模式
    >单例对象（Singleton）是一种常用的设计模式。在Java应用中，单例对象能保证在一个JVM中，该对象只有一个实例存在。这样的模式有几个好处
    > 1. 某些类创建比较频繁，对于一些大型的对象，这是一笔很大的系统开销。
    > 2. 省去了new操作符，降低了系统内存的使用频率，减轻GC压力。
    > 3. 有些类如交易所的核心交易引擎，控制着交易流程，如果该类可以创建多个的话，系统完全乱了。（比如一个军队出现了多个司令员同时指挥，肯定会乱成一团），所以只有使用单例模式，才能保证核心交易服务器独立控制整个流程。

  - 建造者模式
    >工厂类模式提供的是创建单个类的模式，而建造者模式则是将各种产品集中起来进行管理，用来创建复合对象
  - 原型模式
    >将一个对象作为原型，对其进行复制、克隆，产生一个和原对象类似的新对象

### 结构型模式
  - 适配器模式
    > 适配器模式将某个类的接口转换成客户端期望的另一个接口表示，目的是消除由于接口不匹配所造成的类的兼容性问题
    - 类的适配器模式
    - 对象的适配器模式
    - 接口的适配器模式
  - 装饰器模式
    > 顾名思义，装饰模式就是给一个对象增加一些新的功能，而且是动态的，要求装饰对象和被装饰对象实现同一个接口，装饰对象持有被装饰对象的实例
    - 需要扩展一个类的功能。
    - 动态的为一个对象增加功能，而且还能动态撤销。（继承不能做到这一点，继承的功能是静态的，不能动态增删。）
    **缺点：产生过多相似的对象，不易排错！**
  - 代理模式
    > 代理模式就是多一个代理类出来，替原对象进行一些操作，比如我们在租房子的时候回去找中介，为什么呢？  
    > 因为你对该地区房屋的信息掌握的不够全面，希望找一个更熟悉的人去帮你做，此处的代理就是这个意思。  
    >再如我们有的时候打官司，我们需要请律师，因为律师在法律方面有专长，可以替我们进行操作，表达我们的想法。

    >如果已有的方法在使用的时候需要对原有的方法进行改进，此时有两种办法：
    >1. 修改原有的方法来适应。这样违反了“对扩展开放，对修改关闭”的原则。
    >2. 就是采用一个代理类调用原有的方法，且对产生的结果进行控制。这种方法就是代理模式。

    **使用代理模式，可以将功能划分的更加清晰，有助于后期维护！**
  - 外观模式
    > 外观模式是为了解决类与类之家的依赖关系的，像spring一样，可以将类和类之间的关系配置到配置文件中，而外观模式就是将他们的关系放在一个Facade类中，降低了类类之间的耦合度，该模式中没有涉及到接口。  
    > 如果我们没有Computer类，那么，CPU、Memory、Disk他们之间将会相互持有实例，产生关系，这样会造成严重的依赖，修改一个类，可能会带来其他类的修改，这不是我们想要看到的，有了Computer类，他们之间的关系被放在了Computer类里，这样就起到了解耦的作用，这，就是外观模式!  
  - 桥接模式
    > 桥接模式就是把事物和其具体实现分开，使他们可以各自独立的变化。  
    > 桥接的用意是：将抽象化与实现化解耦，使得二者可以独立变化，像我们常用的JDBC桥DriverManager一样，JDBC进行连接数据库的时候，在各个数据库之间进行切换，基本不需要动太多的代码，甚至丝毫不用动，原因就是JDBC提供统一接口，每个数据库提供各自的实现，用一个叫做数据库驱动的程序来桥接就行了。  
  - 组合模式
    > 组合模式有时又叫部分-整体模式在处理类似树形结构的问题时比较方便
  - 享元模式
    > 享元模式的主要目的是实现对象的共享，即共享池，当系统中对象多的时候可以减少内存的开销，通常与工厂模式一起使用

### 行为型模式

  - 父类与子类
    - 策略模式
      > 策略模式定义了一系列算法，并将每个算法封装起来，使他们可以相互替换，且算法的变化不会影响到使用算法的客户。  
      > 需要设计一个接口，为一系列实现类提供统一的方法，多个实现类实现该接口，设计一个抽象类（可有可无，属于辅助类），提供辅助函数。  
      > 策略模式的决定权在用户，系统本身提供不同算法的实现，新增或者删除算法，对各种算法做封装。因此，策略模式多用在算法决策系统中，外部用户只需要决定用哪个算法即可。  
    - 模版方法模式
      >一个抽象类中，有一个主方法，再定义1...n个方法，可以是抽象的，也可以是实际的方法，定义一个类，继承该抽象类，重写抽象方法，通过调用抽象类，实现对子类的调用
  - 两个类之间
    - 观察者模式
      > 当一个对象变化时，其它依赖该对象的对象都会收到通知，并且随着变化！对象之间是一种一对多的关系
    - 迭代子模式
      > 顾名思义，迭代器模式就是顺序访问聚集中的对象
    - 责任链模式
      > 接下来我们将要谈谈责任链模式，有多个对象，每个对象持有对下一个对象的引用，这样就会形成一条链，请求在这条链上传递，直到某一对象决定处理该请求。  
      > 但是发出者并不清楚到底最终那个对象会处理该请求，所以，责任链模式可以实现，在隐瞒客户端的情况下，对系统进行动态的调整。
    - 命令模式
      > 命令模式很好理解，举个例子，司令员下令让士兵去干件事情，从整个事情的角度来考虑，司令员的作用是，发出口令，口令经过传递，传到了士兵耳朵里，士兵去执行。  
      > 这个过程好在，三者相互解耦，任何一方都不用去依赖其他人，只需要做好自己的事儿就行，司令员要的是结果，不会去关注到底士兵是怎么实现的。  
      > 这个很好理解，命令模式的目的就是达到命令的发出者和执行者之间解耦，实现请求和执行分开，熟悉Struts的同学应该知道，Struts其实就是一种将请求和呈现分离的技术，其中必然涉及命令模式的思想。  
  - 类的状态
    - 备忘录模式
      > 主要目的是保存一个对象的某个状态，以便在适当的时候恢复对象，个人觉得叫备份模式更形象些，通俗的讲下：假设有原始类A，A中有各种属性，A可以决定需要备份的属性，备忘录类B是用来存储A的一些内部状态，类C呢，就是一个用来存储备忘录的，且只能存储，不能修改等操作。
    - 状态模式
      > 当对象的状态改变时，同时改变其行为，很好理解！就拿QQ来说，有几种状态，在线、隐身、忙碌等，每个状态对应不同的操作，而且你的好友也能看到你的状态，所以，状态模式就两点：
      >1. 可以通过改变状态来获得不同的行为。
      >2. 你的好友能同时看到你的变化
  - 通过中间类
    - 访问者模式
      > 访问者模式把数据结构和作用于结构上的操作解耦合，使得操作集合可相对自由地演化。  
      > 访问者模式适用于数据结构相对稳定算法又易变化的系统。因为访问者模式使得算法操作增加变得容易。  
      > 若系统数据结构对象易于变化，经常有新的数据对象增加进来，则不适合使用访问者模式。访问者模式的优点是增加操作很容易，因为增加操作意味着增加新的访问者。  
      > 访问者模式将有关行为集中到一个访问者对象中，其改变不影响系统数据结构。其缺点就是增加新的数据结构很困难。  

      > 简单来说，访问者模式就是一种分离对象数据结构与行为的方法，通过这种分离，可达到为一个被访问者动态添加新的操作而无需做其它的修改的效果。简单关系图：  
      > 该模式适用场景：如果我们想为一个现有的类增加新功能，不得不考虑几个事情：  
      >1. 新功能会不会与现有功能出现兼容性问题？
      >2. 以后会不会再需要添加？
      >3. 如果类不允许修改代码怎么办？
      >面对这些问题，最好的解决方法就是使用访问者模式，访问者模式适用于数据结构相对稳定的系统，把数据结构和算法解耦。
    - 中介者模式
      >中介者模式也是用来降低类类之间的耦合的，因为如果类类之间有依赖关系的话，不利于功能的拓展和维护，因为只要修改一个对象，其它关联的对象都得进行修改。如果使用中介者模式，只需关心和Mediator类的关系，具体类类之间的关系及调度交给Mediator就行，这有点像spring容器的作用
    - 解释器模式
      >一般主要应用在OOP开发中的编译器的开发中，基本就这样，解释器模式用来做各种各样的解释器，如正则表达式等的解释器等等！


## 实例

### 六种单例实现方式

#### 饿汉法
  饿汉法就是在第一次引用该类的时候就创建对象实例，而不管实际是否需要创建。代码如下：
  ```
  public class Singleton {
         private static Singleton = new Singleton();
         private Singleton() {}
         public static getSignleton(){
             return singleton();
         }
     }
  ```
  这样做的好处是编写简单，但是无法做到延迟创建对象。但是我们很多时候都希望对象可以尽可能地延迟加载，从而减小负载，所以就需要下面的懒汉法：

#### 单线程写法
  这种写法是最简单的，由私有构造器和一个公有静态工厂方法构成，在工厂方法中对singleton进行null判断，如果是null就new一个出来，最后返回singleton对象。这种方法可以实现延时加载，但是有一个致命弱点：线程不安全。如果有两条线程同时调用getSingleton()方法，就有很大可能导致重复创建对象。
  ```
  public class Singleton {
      private static Singleton singleton = null;
      private Singleton(){}
      public static Singleton getSingleton() {
          if(singleton == null) singleton = new Singleton();
          return singleton;
      }
  }
  ```
#### 考虑线程安全的写法
  这种写法考虑了线程安全，将对singleton的null判断以及new的部分使用synchronized进行加锁。同时，对singleton对象使用volatile关键字进行限制，保证其对所有线程的可见性，并且禁止对其进行指令重排序优化。如此即可从语义上保证这种单例模式写法是线程安全的。注意，这里说的是语义上，实际使用中还是存在小坑的，会在后文写到。
  ```
  public class Singleton {
      private static volatile Singleton singleton = null;
      private Singleton(){}
      public static Singleton getSingleton(){
          synchronized (Singleton.class){
              if(singleton == null){
                  singleton = new Singleton();
              }
          }
          return singleton;
      }
  }
  ```
#### 兼顾线程安全和效率的写法
  虽然上面这种写法是可以正确运行的，但是其效率低下，还是无法实际应用。因为每次调用getSingleton()方法，都必须在synchronized这里进行排队，而真正遇到需要new的情况是非常少的。所以，就诞生了第三种写法：
  ```
  public class Singleton {
      private static volatile Singleton singleton = null;

      private Singleton(){}

      public static Singleton getSingleton(){
          if(singleton == null){
              synchronized (Singleton.class){
                  if(singleton == null){
                      singleton = new Singleton();
                  }
              }
          }
          return singleton;
      }
  }
  ```
  这种写法被称为“双重检查锁”，顾名思义，就是在getSingleton()方法中，进行两次null检查。看似多此一举，但实际上却极大提升了并发度，进而提升了性能。为什么可以提高并发度呢？就像上文说的，在单例中new的情况非常少，绝大多数都是可以并行的读操作。因此在加锁前多进行一次null检查就可以减少绝大多数的加锁操作，执行效率提高的目的也就达到了。
  **坑**
   那么，这种写法是不是绝对安全呢？前面说了，从语义角度来看，并没有什么问题。但是其实还是有坑。说这个坑之前我们要先来看看volatile这个关键字。其实这个关键字有两层语义。  
   第一层语义相信大家都比较熟悉，就是可见性。可见性指的是在一个线程中对该变量的修改会马上由工作内存（Work Memory）写回主内存（Main Memory），所以会马上反应在其它线程的读取操作中。  
   顺便一提，工作内存和主内存可以近似理解为实际电脑中的高速缓存和主存，工作内存是线程独享的，主存是线程共享的。  
   volatile的第二层语义是禁止指令重排序优化。大家知道我们写的代码（尤其是多线程代码），由于编译器优化，在实际执行的时候可能与我们编写的顺序不同。
   编译器只保证程序执行结果与源代码相同，却不保证实际指令的顺序与源代码相同。  
   这在单线程看起来没什么问题，然而一旦引入多线程，这种乱序就可能导致严重问题。volatile关键字就可以从语义上解决这个问题。

  注意，前面反复提到“从语义上讲是没有问题的”，但是很不幸，禁止指令重排优化这条语义直到jdk1.5以后才能正确工作。此前的JDK中即使将变量声明为volatile也无法完全避免重排序所导致的问题。所以，在jdk1.5版本前，双重检查锁形式的单例模式是无法保证线程安全的。

#### 静态内部类法
   那么，有没有一种延时加载，并且能保证线程安全的简单写法呢？我们可以把Singleton实例放到一个静态内部类中，这样就避免了静态实例在Singleton类加载的时候就创建对象，并且由于静态内部类只会被加载一次，所以这种写法也是线程安全的：
   ```
   public class Singleton {
       private static class Holder {
           private static Singleton singleton = new Singleton();
       }

       private Singleton(){}

       public static Singleton getSingleton(){
           return Holder.singleton;
       }
   }
   ```
  但是，上面提到的所有实现方式都有两个共同的缺点：
  >- 都需要额外的工作(Serializable、transient、readResolve())来实现序列化，否则每次反序列化一个序列化的对象实例时都会创建一个新的实例。
  >- 可能会有人使用反射强行调用我们的私有构造器（如果要避免这种情况，可以修改构造器，让它在创建第二个实例的时候抛异常）。

#### 枚举写法
  还有一种更加优雅的方法来实现单例模式，那就是枚举写法：
  ```
  enum SingletonDemo{
     INSTANCE;
     public void otherMethods(){
         System.out.println("Something");
     }
  }

  // 如果我们想调用它的方法时，仅需要以下操作：
  public class Hello {
    public static void main(String[] args){
        SingletonDemo.INSTANCE.otherMethods();
    }
  }

  ```
  使用枚举除了线程安全和防止反射强行调用构造器之外，还提供了自动序列化机制，防止反序列化的时候创建新的对象。因此，推荐尽可能地使用枚举来实现单例。

  原文来自：[](http://www.jcodecraeer.com/a/chengxusheji/java/2016/0326/4086.html)

### 三种代理模式实现方式
  代理(Proxy)是一种设计模式,提供了对目标对象另外的访问方式;即通过代理对象访问目标对象.这样做的好处是:可以在目标对象实现的基础上,增强额外的功能操作,即扩展目标对象的功能.  
  思想:不要随意去修改别人已经写好的代码或者方法,如果需改修改,可以通过代理的方式来扩展该方法。  
  代理模式的关键点是:代理对象与目标对象.代理对象是对目标对象的扩展,并会调用目标对象。  

#### 静态代理
  静态代理在使用时,需要定义接口或者父类,被代理对象与代理对象一起实现相同的接口或者是继承相同父类.

  下面举个案例来解释:  
  模拟保存动作,定义一个保存动作的接口:IUserDao.java,然后目标对象实现这个接口的方法UserDao.java,此时如果使用静态代理方式,就需要在代理对象(UserDaoProxy.java)中也实现IUserDao接口.调用的时候通过调用代理对象的方法来调用目标对象.  
  需要注意的是,代理对象与目标对象要实现相同的接口,然后通过调用相同的方法来调用目标对象的方法

  代码示例:
  接口:IUserDao.java
  ```
  /**
   * 接口
   */
  public interface IUserDao {

      void save();
  }
  ```
  目标对象:UserDao.java
  ```
  /**
   * 接口实现
   * 目标对象
   */
  public class UserDao implements IUserDao {
      public void save() {
          System.out.println("----已经保存数据!----");
      }
  }
  ```
  代理对象:UserDaoProxy.java
  ```
  /**
   * 代理对象,静态代理
   */
  public class UserDaoProxy implements IUserDao{
      //接收保存目标对象
      private IUserDao target;
      public UserDaoProxy(IUserDao target){
          this.target=target;
      }

      public void save() {
          System.out.println("开始事务...");
          target.save();//执行目标对象的方法
          System.out.println("提交事务...");
      }
  }
  ```
  测试类:App.java
  ```
  /**
   * 测试类
   */
  public class App {
      public static void main(String[] args) {
          //目标对象
          UserDao target = new UserDao();

          //代理对象,把目标对象传给代理对象,建立代理关系
          UserDaoProxy proxy = new UserDaoProxy(target);

          proxy.save();//执行的是代理的方法
      }
  }
  ```
  **静态代理总结:**
  1. 可以做到在不修改目标对象的功能前提下,对目标功能扩展.
  2. 缺点:

  因为代理对象需要与目标对象实现一样的接口,所以会有很多代理类,类太多.同时,一旦接口增加方法,目标对象与代理对象都要维护.
  如何解决静态代理中的缺点呢?答案是可以使用动态代理方式

#### 动态代理

  **动态代理有以下特点:**
  1. 代理对象,不需要实现接口
  2. 代理对象的生成,是利用JDK的API,动态的在内存中构建代理对象(需要我们指定创建代理对象/目标对象实现的接口的类型)
  3. 动态代理也叫做:JDK代理,接口代理

  **JDK中生成代理对象的API**
  代理类所在包:java.lang.reflect.Proxy  
  JDK实现代理只需要使用newProxyInstance方法,但是该方法需要接收三个参数,完整的写法是:  
  ```
  static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces,InvocationHandler h )
  ```
  注意该方法是在Proxy类中是静态方法,且接收的三个参数依次为:

  - ```ClassLoader loader,```:指定当前目标对象使用类加载器,获取加载器的方法是固定的
  - ```Class<?>[] interfaces,```:目标对象实现的接口的类型,使用泛型方式确认类型
  - ```InvocationHandler h```:事件处理,执行目标对象的方法时,会触发事件处理器的方法,会把当前执行目标对象的方法作为参数传入

  代码示例:  
  接口类IUserDao.java以及接口实现类,目标对象UserDao是一样的,没有做修改.在这个基础上,增加一个代理工厂类(ProxyFactory.java),将代理类写在这个地方,然后在测试类(需要使用到代理的代码)中先建立目标对象和代理对象的联系,然后代用代理对象的中同名方法

  代理工厂类:ProxyFactory.java
  ```
  /**
   * 创建动态代理对象
   * 动态代理不需要实现接口,但是需要指定接口类型
   */
  public class ProxyFactory{

      //维护一个目标对象
      private Object target;
      public ProxyFactory(Object target){
          this.target=target;
      }

     //给目标对象生成代理对象
      public Object getProxyInstance(){
          return Proxy.newProxyInstance(
                  target.getClass().getClassLoader(),
                  target.getClass().getInterfaces(),
                  new InvocationHandler() {
                      @Override
                      public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                          System.out.println("开始事务2");
                          //执行目标对象方法
                          Object returnValue = method.invoke(target, args);
                          System.out.println("提交事务2");
                          return returnValue;
                      }
                  }
          );
      }

  }
  ```
  测试类:App.java
  ```
  /**
   * 测试类
   */
  public class App {
      public static void main(String[] args) {
          // 目标对象
          IUserDao target = new UserDao();
          // 【原始的类型 class cn.itcast.b_dynamic.UserDao】
          System.out.println(target.getClass());

          // 给目标对象，创建代理对象
          IUserDao proxy = (IUserDao) new ProxyFactory(target).getProxyInstance();
          // class $Proxy0   内存中动态生成的代理对象
          System.out.println(proxy.getClass());

          // 执行方法   【代理对象】
          proxy.save();
      }
  }
  ```
  **总结:**
  代理对象不需要实现接口,但是目标对象一定要实现接口,否则不能用动态代理

#### Cglib代理

  面的静态代理和动态代理模式都是要求目标对象是实现一个接口的目标对象,但是有时候目标对象只是一个单独的对象,并没有实现任何的接口,这个时候就可以使用以目标对象子类的方式类实现代理,这种方法就叫做:Cglib代理

  Cglib代理,也叫作子类代理,它是在内存中构建一个子类对象从而实现对目标对象功能的扩展.

  - JDK的动态代理有一个限制,就是使用动态代理的对象必须实现一个或多个接口,如果想代理没有实现接口的类,就可以使用Cglib实现.
  - Cglib是一个强大的高性能的代码生成包,它可以在运行期扩展java类与实现java接口.它广泛的被许多AOP的框架使用,例如Spring AOP和synaop,为他们提供方法的interception(拦截)
  - Cglib包的底层是通过使用一个小而块的字节码处理框架ASM来转换字节码并生成新的类.不鼓励直接使用ASM,因为它要求你必须对JVM内部结构包括class文件的格式和指令集都很熟悉.

  Cglib子类代理实现方法:

  1. 需要引入cglib的jar文件,但是Spring的核心包中已经包括了Cglib功能,所以直接引入```pring-core-3.2.5.jar```即可.
  2. 引入功能包后,就可以在内存中动态构建子类
  3. 代理的类不能为final,否则报错
  4. 目标对象的方法如果为final/static,那么就不会被拦截,即不会执行目标对象额外的业务方法.

  代码示例:
  目标对象类:UserDao.java
  ```
  /**
   * 目标对象,没有实现任何接口
   */
  public class UserDao {

      public void save() {
          System.out.println("----已经保存数据!----");
      }
  }
  ```
  Cglib代理工厂:ProxyFactory.java
  ```
  /**
   * Cglib子类代理工厂
   * 对UserDao在内存中动态构建一个子类对象
   */
  public class ProxyFactory implements MethodInterceptor{
      //维护目标对象
      private Object target;

      public ProxyFactory(Object target) {
          this.target = target;
      }

      //给目标对象创建一个代理对象
      public Object getProxyInstance(){
          //1.工具类
          Enhancer en = new Enhancer();
          //2.设置父类
          en.setSuperclass(target.getClass());
          //3.设置回调函数
          en.setCallback(this);
          //4.创建子类(代理对象)
          return en.create();

      }

      @Override
      public Object intercept(Object obj, Method method, Object[] args, MethodProxy proxy) throws Throwable {
          System.out.println("开始事务...");

          //执行目标对象的方法
          Object returnValue = method.invoke(target, args);

          System.out.println("提交事务...");

          return returnValue;
      }
  }
  ```
  测试类:
  ```
  /**
   * 测试类
   */
  public class App {

      @Test
      public void test(){
          //目标对象
          UserDao target = new UserDao();

          //代理对象
          UserDao proxy = (UserDao)new ProxyFactory(target).getProxyInstance();

          //执行代理对象的方法
          proxy.save();
      }
  }
  ```
  在Spring的AOP编程中:
  如果加入容器的目标对象有实现接口,用JDK代理。
  如果目标对象没有实现接口,用Cglib代理。

>作者：岑宇
 出处：http://www.cnblogs.com/cenyu/
 本文版权归作者和博客园共有，欢迎转载，但未经作者同意必须保留此段声明，且在文章页面明显位置给出原文连接，否则保留追究法律责任的权利。
 如果文中有什么错误，欢迎指出。以免更多的人被误导。

### 三种工厂模式实现方式

#### 简单工厂模式

  ```
   // 抽象一个面条基类，(接口也可以)，这是产品的抽象类。
   public abstract class INoodles {
       /**
        * 描述每种面条啥样的
        */
       public abstract void desc();
   }

   // 先来一份兰州拉面（具体的产品类）：
   public class LzNoodles extends INoodles {
       @Override
       public void desc() {
           System.out.println("兰州拉面 上海的好贵 家里才5 6块钱一碗");
       }
   }
   // 程序员加班必备也要吃泡面（具体的产品类）：
   public class PaoNoodles extends INoodles {
       @Override
       public void desc() {
           System.out.println("泡面好吃 可不要贪杯");
       }
   }
   // 还有我最爱吃的家乡的干扣面（具体的产品类）：
   public class GankouNoodles extends INoodles {
     @Override
     public void desc() {
        System.out.println("还是家里的干扣面好吃 6块一碗");
     }
   }


   // 准备工作做完了，我们来到一家“简单面馆”（简单工厂类），菜单如下：
   public class SimpleNoodlesFactory {
       public static final int TYPE_LZ = 1;//兰州拉面
       public static final int TYPE_PM = 2;//泡面
       public static final int TYPE_GK = 3;//干扣面

       public static INoodles createNoodles(int type) {
           switch (type) {
               case TYPE_LZ:
                   return new LzNoodles();
               case TYPE_PM:
                   return new PaoNoodles();
               case TYPE_GK:
               default:
                   return new GankouNoodles();
           }
       }
   }
  ```
  简单面馆就提供三种面条（产品），你说你要啥，他就给你啥。这里我点了一份干扣面:
  ```
  /**
   * 简单工厂模式
   */
   INoodles noodles = SimpleNoodlesFactory.createNoodles(SimpleNoodlesFactory.TYPE_GK);
   noodles.desc();
  ```
  **特点**
  1. 它是一个具体的类，非接口 抽象类。有一个重要的create()方法，利用if或者 switch创建产品并返回。
  2. create()方法通常是静态的，所以也称之为静态工厂。

  **缺点**
  1. 扩展性差（我想增加一种面条，除了新增一个面条产品类，还需要修改工厂类方法）
  2. 不同的产品需要不同额外参数的时候 不支持。

#### 工厂方法模式
  - 模式描述
    > 提供一个用于创建对象的接口(工厂接口)，让其实现类(工厂实现类)决定实例化哪一个类(产品类)，并且由该实现类创建对应类的实例。
  - 模式作用
    >可以一定程度上解耦，消费者和产品实现类隔离开，只依赖产品接口(抽象产品)，产品实现类如何改动与消费者完全无关。
     可以一定程度增加扩展性，若增加一个产品实现，只需要实现产品接口，修改工厂创建产品的方法，消费者可以无感知（若消费者不关心具体产品是什么的情况）。
     可以一定程度增加代码的封装性、可读性。清楚的代码结构，对于消费者来说很少的代码量就可以完成很多工作。
     等等。//TODO
     另外，抽象工厂才是实际意义的工厂模式，工厂方法只是抽象工厂的一个比较常见的情况。
  - 适用场景
    > 消费者不关心它所要创建对象的类(产品类)的时候。
      消费者知道它所要创建对象的类(产品类)，但不关心如何创建的时候。
      等等。//TODO
      例如：hibernate里通过sessionFactory创建session、通过代理方式生成ws客户端时，通过工厂构建报文中格式化数据的对象。
  - 模式要素
    > 提供一个产品类的接口。产品类均要实现这个接口(也可以是abstract类，即抽象产品)。
      提供一个工厂类的接口。工厂类均要实现这个接口(即抽象工厂)。
      由工厂实现类创建产品类的实例。工厂实现类应有一个方法，用来实例化产品类。

  ```
  /**
   * 工厂方法模式_工厂接口
   *
   * @author popkidorc
   *
   */
  public interface IMyMessageFactory {

      public IMyMessage createMessage(String messageType);
  }
  ```
  ```
  /**
     * 工厂方法模式_工厂实现
     *
     * @author popkidorc
     *
     */
    public class MyMessageFactory implements IMyMessageFactory {

        @Override
        public IMyMessage createMessage(String messageType) {
            // 这里的方式是：消费者知道自己想要什么产品；若生产何种产品完全由工厂决定，则这里不应该传入控制生产的参数。
            IMyMessage myMessage;
            Map<String, Object> messageParam = new HashMap<String, Object>();
            // 根据某些条件去选择究竟创建哪一个具体的实现对象，条件可以传入的，也可以从其它途径获取。
            // sms
            if ("SMS".equals(messageType)) {
                myMessage = new MyMessageSms();
                messageParam.put("PHONENUM", "123456789");
            } else
            // OA待办
            if ("OA".equals(messageType)) {
                myMessage = new MyMessageOaTodo();
                messageParam.put("OAUSERNAME", "testUser");
            } else
            // email
            if ("EMAIL".equals(messageType)) {
                myMessage = new MyMessageEmail();
                messageParam.put("EMAIL", "test@test.com");
            } else
            // 默认生产email这个产品
            {
                myMessage = new MyMessageEmail();
                messageParam.put("EMAIL", "test@test.com");
            }
            myMessage.setMessageParam(messageParam);
            return myMessage;
        }
    }
  ```
  ```
  /**
   * 工厂方法模式_产品接口
   *
   * @author popkidorc
   *
   */
  public interface IMyMessage {

      public Map<String, Object> getMessageParam();

      public void setMessageParam(Map<String, Object> messageParam);

      public void sendMesage() throws Exception;// 发送通知/消息

  }
  ```
  ```
  /**
   * 工厂方法模式_虚拟产品类
   *
   * @author popkidorc
   *
   */
  public abstract class MyAbstractMessage implements IMyMessage {

      private Map<String, Object> messageParam;// 这里可以理解为生产产品所需要的原材料库。最好是个自定义的对象，这里为了不引起误解使用Map。

      @Override
      public Map<String, Object> getMessageParam() {
          return messageParam;
      }

      @Override
      public void setMessageParam(Map<String, Object> messageParam) {
          this.messageParam = messageParam;
      }
  }
  ```
  ```
  /**
   * 工厂方法模式_email产品
   *
   * @author popkidorc
   *
   */
  public class MyMessageEmail extends MyAbstractMessage {

      @Override
      public void sendMesage() throws Exception {
          // TODO Auto-generated method stub
          if (null == getMessageParam() || null == getMessageParam().get("EMAIL")
                  || "".equals(getMessageParam().get("EMAIL"))) {
              throw new Exception("发送短信,需要传入EMAIL参数");// 为了简单起见异常也不自定义了
          }// 另外邮件内容，以及其他各种协议参数等等都要处理

          System.out.println("我是邮件，发送通知给" + getMessageParam().get("EMAIL"));
      }

  }
  ```
  ```
  /**
   * 工厂方法模式_oa待办产品
   *
   * @author popkidorc
   *
   */
  public class MyMessageOaTodo extends MyAbstractMessage {

      @Override
      public void sendMesage() throws Exception {
          // TODO Auto-generated method stub
          if (null == getMessageParam()
                  || null == getMessageParam().get("OAUSERNAME")
                  || "".equals(getMessageParam().get("OAUSERNAME"))) {
              throw new Exception("发送OA待办,需要传入OAUSERNAME参数");// 为了简单起见异常也不自定义了
          }// 这里的参数需求就比较多了不一一处理了

          System.out
                  .println("我是OA待办，发送通知给" + getMessageParam().get("OAUSERNAME"));
      }

  }
  ```
  ```
  /**
   * 工厂方法模式_sms产品
   *
   * @author popkidorc
   *
   */
  public class MyMessageSms extends MyAbstractMessage {

      @Override
      public void sendMesage() throws Exception {
          // TODO Auto-generated method stub
          if (null == getMessageParam()
                  || null == getMessageParam().get("PHONENUM")
                  || "".equals(getMessageParam().get("PHONENUM"))) {
              throw new Exception("发送短信,需要传入PHONENUM参数");// 为了简单起见异常也不自定义了
          }// 另外短信信息，以及其他各种协议参数等等都要处理

          System.out.println("我是短信，发送通知给" + getMessageParam().get("PHONENUM"));
      }

  }
  ```
  ```
  /**
   * 工厂方法模式_消费者类
   *
   * @author popkidorc
   *
   */
  public class MyFactoryMethodMain {

      public static void main(String[] args) {
          IMyMessageFactory myMessageFactory = new MyMessageFactory();
          IMyMessage myMessage;
          // 对于这个消费者来说，不用知道如何生产message这个产品，耦合度降低
          try {
              // 先来一个短信通知
              myMessage = myMessageFactory.createMessage("SMS");
              myMessage.sendMesage();

              // 来一个oa待办
              myMessage = myMessageFactory.createMessage("OA");
              myMessage.sendMesage();

              // 来一个邮件通知
              myMessage = myMessageFactory.createMessage("EMAIL");
              myMessage.sendMesage();
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```

#### 抽象工厂模式

  为创建一组相关或相互依赖的对象提供一个接口，而且无需指定他们的具体类。
  ![类图](http://graph.guoyw.com/Java_notes/JavaSE/design_mode/%E6%8A%BD%E8%B1%A1%E5%B7%A5%E5%8E%82%E7%B1%BB%E5%9B%BE.png)

  **抽象工厂模式与工厂方法模式的区别**
  >抽象工厂模式是工厂方法模式的升级版本，他用来创建一组相关或者相互依赖的对象。他与工厂方法模式的区别就在于，工厂方法模式针对的是一个产品等级结构；
   而抽象工厂模式则是针对的多个产品等级结构。在编程中，通常一个产品结构，表现为一个接口或者抽象类，也就是说，工厂方法模式提供的所有产品都是衍生自同一个接口或抽象类，而抽象工厂模式所提供的产品则是衍生自不同的接口或抽象类。

  在抽象工厂模式中，有一个产品族的概念：所谓的产品族，是指位于不同产品等级结构中功能相关联的产品组成的家族。抽象工厂模式所提供的一系列产品就组成一个产品族；而工厂方法提供的一系列产品称为一个等级结构。我们依然拿生产汽车的例子来说明他们之间的区别。

  ![类图](http://graph.guoyw.com/Java_notes/JavaSE/design_mode/%E6%8A%BD%E8%B1%A1%E5%B7%A5%E5%8E%82%E5%AE%9E%E4%BE%8B1.png)

   在上面的类图中，两厢车和三厢车称为两个不同的等级结构；而2.0排量车和2.4排量车则称为两个不同的产品族。再具体一点，2.0排量两厢车和2.4排量两厢车属于同一个等级结构，2.0排量三厢车和2.4排量三厢车属于另一个等级结构；而2.0排量两厢车和2.0排量三厢车属于同一个产品族，2.4排量两厢车和2.4排量三厢车属于另一个产品族。

   明白了等级结构和产品族的概念，就理解工厂方法模式和抽象工厂模式的区别了，如果工厂的产品全部属于同一个等级结构，则属于工厂方法模式；如果工厂的产品来自多个等级结构，则属于抽象工厂模式。在本例中，如果一个工厂模式提供2.0排量两厢车和2.4排量两厢车，那么他属于工厂方法模式；如果一个工厂模式是提供2.4排量两厢车和2.4排量三厢车两个产品，那么这个工厂模式就是抽象工厂模式，因为他提供的产品是分属两个不同的等级结构。当然，如果一个工厂提供全部四种车型的产品，因为产品分属两个等级结构，他当然也属于抽象工厂模式了。

   ```
   interface IProduct1 {
       public void show();
   }
   interface IProduct2 {
       public void show();
   }

   class Product1 implements IProduct1 {
       public void show() {
           System.out.println("这是1型产品");
       }
   }
   class Product2 implements IProduct2 {
       public void show() {
           System.out.println("这是2型产品");
       }
   }

   interface IFactory {
       public IProduct1 createProduct1();
       public IProduct2 createProduct2();
   }
   class Factory implements IFactory{
       public IProduct1 createProduct1() {
           return new Product1();
       }
       public IProduct2 createProduct2() {
           return new Product2();
       }
   }

   public class Client {
       public static void main(String[] args){
           IFactory factory = new Factory();
           factory.createProduct1().show();
           factory.createProduct2().show();
       }
   }
   ```
   ```
   class Engine {
       public void getStyle(){
           System.out.println("这是汽车的发动机");
       }
   }
   class Underpan {
       public void getStyle(){
           System.out.println("这是汽车的底盘");
       }
   }
   class Wheel {
       public void getStyle(){
           System.out.println("这是汽车的轮胎");
       }
   }
   public class Client {
       public static void main(String[] args) {
           Engine engine = new Engine();
           Underpan underpan = new Underpan();
           Wheel wheel = new Wheel();
           ICar car = new Car(underpan, wheel, engine);
           car.show();
       }
   }
   ```

  **抽象工厂模式的优点**
   抽象工厂模式除了具有工厂方法模式的优点外，最主要的优点就是可以在类的内部对产品族进行约束。所谓的产品族，一般或多或少的都存在一定的关联，抽象工厂模式就可以在类内部对产品族的关联关系进行定义和描述，而不必专门引入一个新的类来进行管理。

  **抽象工厂模式的缺点**
   产品族的扩展将是一件十分费力的事情，假如产品族中需要增加一个新的产品，则几乎所有的工厂类都需要进行修改。所以使用抽象工厂模式时，对产品等级结构的划分是非常重要的。

  **适用场景**
  当需要创建的对象是一系列相互关联或相互依赖的产品族时，便可以使用抽象工厂模式。说的更明白一点，就是一个继承体系中，如果存在着多个等级结构（即存在着多个抽象类），并且分属各个等级结构中的实现类之间存在着一定的关联或者约束，就可以使用抽象工厂模式。假如各个等级结构中的实现类之间不存在关联或约束，则使用多个独立的工厂来对产品进行创建，则更合适一点。

  **总结**
  无论是简单工厂模式，工厂方法模式，还是抽象工厂模式，他们都属于工厂模式，在形式和特点上也是极为相似的，他们的最终目的都是为了解耦。在使用时，我们不必去在意这个模式到底工厂方法模式还是抽象工厂模式，因为他们之间的演变常常是令人琢磨不透的。经常你会发现，明明使用的工厂方法模式，当新需求来临，稍加修改，加入了一个新方法后，由于类中的产品构成了不同等级结构中的产品族，它就变成抽象工厂模式了；而对于抽象工厂模式，当减少一个方法使的提供的产品不再构成产品族之后，它就演变成了工厂方法模式。

  所以，在使用工厂模式时，只需要关心降低耦合度的目的是否达到了。

  > 原文来自：https://www.cnblogs.com/zailushang1996/p/8601808.html

### 委派模式

  委派模式有点像代理模式又有点像策略模式。例如：公司老板给项目经理下达任务，将任务全权交给项目经理，由项目经理根据一定的策略将任务分配给小组成员，项目经理从头跟到尾。项目经理就像一个受老板授权的中介，老板不需要和小组成员直接联系，甚至可以不知道他的存在。

  我们员工实现同一个干活的接口
  ```
  我们员工实现同一个干活的接口
  ```

  我们员工实现同一个干活的接口
  ```
  public class TargetA implements ITarget {
      @Override
      public void doSomething(String command) {
          System.out.println("我是员工A，现在开始干" + command + "");
      }
  }

  public class TargetB implements ITarget {
      @Override
      public void doSomething(String command) {
          System.out.println("我是员工B，现在开始干" + command + "");
      }
  }
  ```
  项目经理持有所有的小组成员，根据一定的策略选择干活的人
  ```
  public class Leader implements ITarget {

      private Map<String, ITarget> targets = new HashMap<>();

      /**
       * 项目经理持有小组成员可供选择，类似策略模式
       */
      public Leader() {
          targets.put("加密", new TargetA());
          targets.put("登录", new TargetB());
      }

      public void doSomething(String command) {
          targets.get(command).doSomething(command);
      }
  }
  ```
  领导下达命令
  ```
  public class Boss {

      public static void main(String[] args) {
          new Leader().doSomething("登录");
      }
  }
  ```
  从上面可以看出来委派模式就是静态代理和策略模式的一种特殊组合，代理模式注重的是过程，委派模式注重的是结果。策略模式注重的是可扩展（外部扩展），委派模式注重的是内部的灵活和复用。

> 原文来源：https://blog.csdn.net/caoyue_new/article/details/80500431

### 策略模式

  使用场景实例：

  - 假设某个网站销售各种书籍，对初级会员没有提供折扣，对中级会员提供每本10%的促销折扣，对高级会员提供每本20%的促销折扣。
  - 折扣是根据以下的3个算法中的1个进行的：
    - 算法1：对初级会员没有提供折扣。
    - 算法2：对中级会员提供10%的促销折扣。
    - 算法3：对高级会员提供20%的促销折扣。

    UML图：
    ![UML图](http://graph.guoyw.com/Java_notes/JavaSE/design_mode/策略模式实例1.png)

    ```
    // 折扣接口
    public interface MemberStrategy {
        /**
         * 计算图书的价格
         * @param booksPrice    图书的原价
         * @return    计算出打折后的价格
         */
        public double calcPrice(double booksPrice);
    }

    // 初级会员折扣实现类
    public class PrimaryMemberStrategy implements MemberStrategy {

        @Override
        public double calcPrice(double booksPrice) {

            System.out.println("对于初级会员的没有折扣");
            return booksPrice;
        }

    }

    // 中级会员折扣实现类
    public class IntermediateMemberStrategy implements MemberStrategy {

        @Override
        public double calcPrice(double booksPrice) {

            System.out.println("对于中级会员的折扣为10%");
            return booksPrice * 0.9;
        }

    }

    // 高级会员折扣实现类
    public class AdvancedMemberStrategy implements MemberStrategy {

        @Override
        public double calcPrice(double booksPrice) {

            System.out.println("对于高级会员的折扣为20%");
            return booksPrice * 0.8;
        }
    }

    //  价格类
    public class Price {
        // 持有一个具体的策略对象
        private MemberStrategy strategy;
        /**
         * 构造函数，传入一个具体的策略对象
         * @param strategy    具体的策略对象
         */
        public Price(MemberStrategy strategy){
            this.strategy = strategy;
        }

        /**
         * 计算图书的价格
         * @param booksPrice    图书的原价
         * @return    计算出打折后的价格
         */
        public double quote(double booksPrice){
            return this.strategy.calcPrice(booksPrice);
        }
    }

    //客户端
    public class Client {

        public static void main(String[] args) {
            // 选择并创建需要使用的策略对象
            MemberStrategy strategy = new AdvancedMemberStrategy();
            // 创建环境
            Price price = new Price(strategy);
            // 计算价格
            double quote = price.quote(300);
            System.out.println("图书的最终价格为：" + quote);
        }

    }


    ```
    　策略模式的重心不是如何实现算法，而是如何组织、调用这些算法，从而让程序结构更灵活，具有更好的维护性和扩展性。策略算法是相同行为的不同实现。在运行期间，策略模式在每一个时刻只能使用一个具体的策略实现对象。把所有的具体策略实现类的共同公有方法封装到抽象类里面，将代码向继承等级结构的上方集中。

    ![策略模式](http://graph.guoyw.com/Java_notes/JavaSE/design_mode/策略模式.png)

    **策略模式优点：**
    1. 通过策略类的等级结构来管理算法族。
    2. 避免使用将采用哪个算法的选择与算法本身的实现混合在一起的多重条件(if-else if-else)语句。

    **策略模式缺点：**
    1. 客户端必须知道所有的策略类，并自行决定使用哪一个策略类。
    2. 由于策略模式把每个算法的具体实现都单独封装成类，针对不同的情况生成的对象就会变得很多。

    >原文出自：https://www.cnblogs.com/WJQ2017/p/7629109.html

### 原型模式
  传送门：[原型模式](https://www.cnblogs.com/lfxiao/p/6812835.html)

### 模板方法模式

  模板方法模式UML图:
  ![模式UML图](http://graph.guoyw.com/Java_notes/JavaSE/design_mode/模板模式实例1.png)

  写的是一个汽车启动的过程，每一种汽车启动的过程都基本是一样的流程，无非是这一过程中存在一些细小差别。
  ```
  /**
   * 汽车模型
   * 模型模式
   * @author liaowp
   *
   */
  public abstract class CarModel {
       /**
        * 汽车启动
        */
       protected abstract void start();

       /**
        * 停车
        */
       protected abstract void stop();

       /**
        * 用户并不需要关注你的车怎么启动或者停下来的，可以开可以停就可以啦
        */
       final public void excet(){
           this.start();
           this.stop();
       }
  }


  /**
   * 大众车
   * @author liaowp
   *
   */
  public class Wcar extends CarModel{

      @Override
      protected void start() {
          System.out.println("大众车启动 。。。。。。。。突突突");
      }

      @Override
      protected void stop() {
          System.out.println("大众车停车。。。。。。。。。");
      }
  }

  /**
   * 奥迪
   * @author liaowp
   *
   */
  public class Ocar extends CarModel{

      @Override
      protected void start() {
          System.out.println("奥迪  无匙启动               突突突");
      }

      @Override
      protected void stop() {
          System.out.println("奥迪  停车              ");
      }

  }


  /**
   * 客户端
   * @author liaowp
   *
   */
  public class Client {
      public static void main(String[] args) {
          CarModel wcar=new Wcar();//家里的第一辆车，作为用户的我们并不需要关注车怎么启动的.子类变量变为父类。多态
          wcar.excet();

          //突然家里需要第二辆车了   奥迪     我们也不需要关注他怎么生产启动的
          CarModel ocar=new Ocar();
          ocar.excet();
      }
  }

  ```

  **模板方法模式适用场景**

  - 一次性实现一个算法的不变的部分，并将可变的行为留给子类来实现。
  - 各子类中公共的行为应被提取出来并集中到一个公共父类中以避免代码重复。这是Opdyke和Johnson所描述过的“重分解以一般化”的一个很好的例子。首先识别现有代码中的不同之处，并且将不同之处分离为新的操作。最后，用一个调用这些新的操作的模板方法来替换这些不同的代码。
  - 控制子类扩展。模板方法只在特定点调用“hook”操作，这样就只允许在这些点进行扩展。

  > 作者：鹏鹏
    出处：http://www.cnblogs.com/liaoweipeng/

### 观察者模式简单例子
  观测者模式定义了对象之间的一对多依赖，当一个对象状态发生改变时，其依赖者便会收到通知并做相应的更新。其原则是：为交互对象之间松耦合。以松耦合方式在一系列对象之间沟通状态，我们可以独立复用主题（Subject）/可观测者（Observable）和观测者（Observer），即只要遵守接口规则改变其中一方并不会影响到另一方。这也是其主要的设计原则。下面是一个简单的气象站发送天气信息给布告板，然后布告板把天气信息显示在板上的例子。
  首先先建立三个接口，主题（Subject）、观测者（Observer）和显示内容（DisplayElement），分别代表气象站、布告板信息接收和布告板信息显示。

  ```
  /**
   *  主题
   */
  public interface Subject {
      // 观察者注册
      public void registerObserver(Observer o);
      // 删除观察者
      public void removeObserver(Observer o);
      // 当主题有内容更新时调用，用于通知观察者
      public void notifyObserver();
  }
  /**
   *  观察者
   */
  public interface Observer {
      // 当气象站观测的天气发生变化时，主题会把参数值传给观察者
      public void update(float temp);
  }

  /**
   *  用于布告板显示
   */
  public interface DisplayElement {
      // 在显示布告板上显示的操作
      public void display();
  }

  ```
  接下来是实现气象站（）和布告板（）了。
  ```
  /**
   * 气象站实现主题，发布气象信息（气温）
   */
  public class WeatherStation implements Subject{
      private ArrayList observers;
      private float temp;

      public WeatherStation() {
          // 加个ArrayList存放所有注册的Observer对象;
          observers = new ArrayList<>();
      }

      @Override
      public void registerObserver(Observer o) {
          // 当新的观察者注册时添加进来
          observers.add(o);
      }

      @Override
      public void removeObserver(Observer o) {
          // 当观察者取消注册时去除该观察者
          int i = observers.indexOf(o);
          if (i>=0) {
              observers.remove(i);
          }
      }

      @Override
      public void notifyObserver() {
          // 更新状态，调用Observer的update告诉观察者有新的信息
          for (int i = 0; i < observers.size(); i++) {
              Observer observer = (Observer) observers.get(i);
              observer.update(temp);
          }
      }

      /*
       *  此方法用于气象站收到的数据,并且调用更新使数据实时通知给观察者
       */
      public void setMeasurements(float temp){
          this.temp = temp;
          System.out.println("气象站测量的温度为：" + temp + "℃");
          notifyObserver();
      }
  }

  /**
   * 布告板上的状态显示
   */
  public class ConditionDisplay implements Observer,DisplayElement{
      private float temp;
      private Subject weatherStation;

      public ConditionDisplay(Subject weatherStation) {
          // 构造时需要间主题/被观察者对象作为注册之用
          this.weatherStation = weatherStation;
          weatherStation.registerObserver(this);
      }

      @Override
      public void display() {
          // 将数据显示在布告板上
          System.out.println("布告板显示当前温度为：" + temp + "℃");
      }

      @Override
      public void update(float temp) {
          // 接受来自主题/被观察者（气象站）的数据
          this.temp = temp;
          display();
      }
  }

  ```
  测试结果
  ```
  /**
   * 天气观测站
   */
  public class WeatherObserver {

      public static void main(String[] args) {
          // 首先创建一个主题/被观察者
          WeatherStation weatherStation = new WeatherStation();
          // 创建观察者并将被观察者对象传入
          ConditionDisplay conditionDisplay = new ConditionDisplay(weatherStation);

          // 设置气象站模拟收到的气温数据
          weatherStation.setMeasurements(25);
          weatherStation.setMeasurements(24);
          weatherStation.setMeasurements(23);
      }
  }

  ```

#### JAVA内置观察者模式
  可以使用java内置的观察者模式，这样就无需自己写Subject和Observer类了，在java.util包下继承的Observable和实现Observer类即可。其修改后的代码如下：
  ```
  /**
   * 继承java内置的被观察者，因此不再需要注册和删除了
   */
  public class WeatherStationN extends Observable{
      private float temperature;
      public WeatherStationN() {
          // 由于继承了Observable，它已经创建了一个Vector来存放Observer对象的容器，所以此处不用再建立ArrayList
      }

      /*
       *  此方法用于气象站收到的数据,并且调用更新使数据实时通知给观察者
       */
      public void setMeasurements(float temp){
          this.temperature = temp;
          System.out.println("气象站测量的温度为：" + temp + "℃");
          // 更新强调用表示有状态更新
          setChanged();
          notifyObservers(temperature);
      }
  }

  /**
   * 实现java内置Observer接口
   */
  public class ConditionDisplayN implements java.util.Observer,DisplayElement{
      private Observable observable;
      private float temp;

      public ConditionDisplayN(Observable observable) {
          // 构造器需要Observable作为参数
          this.observable = observable;
          observable.addObserver(this);
      }

      @Override
      public void display() {
          // 将数据显示在布告板上
          System.out.println("布告板显示当前温度为：" + temp + "℃");
      }

      @Override
      public void update(Observable o, Object arg) {
          // 当被观察者有更新使触发
          if (o instanceof WeatherStationN) {
              this.temp = (float) arg;
              display();
          }
      }
  }
  ```
  测试运行结果

  ```
  /**
   * 天气观测站
   */
  public class WeatherObserver {

      public static void main(String[] args) {
          // 首先创建一个主题/被观察者
          WeatherStationN weatherStationN = new WeatherStationN();
          // 创建观察者并将被观察者对象传入
          ConditionDisplayN conditionDisplayN = new ConditionDisplayN(weatherStationN);

          // 设置气象站模拟收到的气温数据
          weatherStationN.setMeasurements(30);
          weatherStationN.setMeasurements(25);
          weatherStationN.setMeasurements(20);
      }
  }
  ```

  Observer是一个接口，而Observable是一个类，在使用时必须继承它，因此在继承Observable时就无法再继承其他超类了，因为Java毕竟不支持多重继承。且在Observable更新前，即notifyObservers()或notifyObservers(Object arg)前要先调用setChange()标记更新状态

  >原文出自：https://blog.csdn.net/qq_15128547/article/details/53205892
