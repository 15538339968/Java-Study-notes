# Java 多线程

知识体系图：
![知识体系图](http://graph.guoyw.com/Java_notes/JavaSE/多线程思维图.jpg)

## 认识线程

  传送门：[Java 多线程](https://www.cnblogs.com/wxd0108/p/5479442.html)

- 线程定义
  线程是程序的最小执行单元；
  进程是操作系统进行调度和分配资源的基本单位；
  关联：一个程序至少有一个进程，
- 线程分类
  - 用户线程
  - 守护线程
- 线程优先级
  传送门：[Java 线程优先级](http://www.cnblogs.com/xdp-gacl/p/3634382.html)
- 线程内存模型
  传送门：[线程内存模型](https://www.cnblogs.com/chihirotan/p/6486436.html)

  - Java内存间交互操作
     JLS定义了线程对主存的操作指令：lock，unlock，read，load，use，assign，store，write。这些行为是不可分解的原子操作，在使用上相互依赖，read-load从主内存复制变量到当前工作内存，use-assign执行代码改变共享变量值，store-write用工作内存数据刷新主存相关内容。

    - read（读取）：作用于主内存变量，把一个变量值从主内存传输到线程的工作内存中，以便随后的load动作使用
    - load（载入）：作用于工作内存的变量，它把read操作从主内存中得到的变量值放入工作内存的变量副本中。
    - use（使用）：作用于工作内存的变量，把工作内存中的一个变量值传递给执行引擎，每当虚拟机遇到一个需要使用变量的值的字节码指令时将会执行这个操作。
    - assign（赋值）：作用于工作内存的变量，它把一个从执行引擎接收到的值赋值给工作内存的变量，每当虚拟机遇到一个给变量赋值的字节码指令时执行这个操作。
    - store（存储）：作用于工作内存的变量，把工作内存中的一个变量的值传送到主内存中，以便随后的write的操作。
    - write（写入）：作用于主内存的变量，它把store操作从工作内存中一个变量的值传送到主内存的变量中。

- 多线程的三个特性
  - 1. 原子性（Atomicity）
    原子性是指一个原子操作在cpu中不可以暂停然后再调度，既不被中断操作，要不执行完成，要不就不执行。原子操作保证了原子性问题。

    x++（包含三个原子操作）a.将变量x 值取出放在寄存器中 b.将将寄存器中的值+1 c.将寄存器中的值赋值给x

    >由Java内存模型来直接保证的原子性变量操作包括read、load、use、assign、store和write六个，大致可以认为基础数据类型的访问和读写是具备原子性的。
     如果应用场景需要一个更大范围的原子性保证，Java内存模型还提供了lock和unlock操作来满足这种需求，尽管虚拟机未把lock与unlock操作直接开放给用户使用，但是却提供了更高层次的字节码指令monitorenter和monitorexit来隐匿地使用这两个操作，这两个字节码指令反映到Java代码中就是同步块---synchronized关键字，因此在synchronized块之间的操作也具备原子性。

  - 2. 可见性(Visibility)

    java 内存模型的主内存和工作内存，解决了可见性问题。
    volatile赋予了变量可见——禁止编译器对成员变量进行优化，它修饰的成员变量在每次被线程访问时，都强迫从内存中重读该成员变量的值；而且，当成员变量发生变化时，强迫线程将变化值回写到共享内存，这样在任何时刻两个不同线程总是看到某一成员变量的同一个值，这就是保证了可见性。

    >可见性就是指当一个线程修改了线程共享变量的值，其它线程能够立即得知这个修改。无论是普通变量还是volatile变量都是如此，普通变量与volatile变量的区别是volatile的特殊规则保证了新值能立即同步到主内存，以及每使用前立即从内存刷新。因为我们可以说volatile保证了线程操作时变量的可见性，而普通变量则不能保证这一点。

  - 3. 有序性(Ordering)
    Java内存模型中的程序天然有序性可以总结为一句话：如果在本线程内观察，所有操作都是有序的；如果在一个线程中观察另一个线程，所有操作都是无序的。前半句是指“线程内表现为串行语义”，后半句是指“指令重排序”现象和“工作内存主主内存同步延迟”现象。

- 线程状态
  1. 新建状态（New）：新创建了一个线程对象。
  2. 就绪状态（Runnable）：线程对象创建后，其他线程调用了该对象的start()方法。该状态的线程位于可运行线程池中，变得可运行，等待获取CPU的使用权。
  3. 运行状态（Running）：就绪状态的线程获取了CPU，执行程序代码。
  4. 阻塞状态（Blocked）：阻塞状态是线程因为某种原因放弃CPU使用权，暂时停止运行。直到线程进入就绪状态，才有机会转到运行状态。阻塞的情况分三种：
  （一）、等待阻塞：运行的线程执行wait()方法，JVM会把该线程放入等待池中。
  （二）、同步阻塞：运行的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则JVM会把该线程放入锁池中。
  （三）、其他阻塞：运行的线程执行sleep()或join()方法，或者发出了I/O请求时，JVM会把该线程置为阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入就绪状态。
  5. 死亡状态（Dead）：线程执行完了或者因异常退出了run()方法，该线程结束生命周期。
  ![线程状态](http://graph.guoyw.com/Java_notes/JavaSE/%E5%A4%9A%E7%BA%BF%E7%A8%8B%E7%8A%B6%E6%80%81.png)

- 多线程安全
  - synchronized
    Synchronized关键字保证了数据读写一致和可见性等问题，但是他是一种阻塞的线程控制方法，在关键字使用期间，所有其他线程不能使用此变量，这就引出了一种叫做非阻塞同步的控制线程安全的需求；(同步机制采用了“以时间换空间”的方式)

  - volatile
    Java语言规范中指出：为了获得最佳速度，允许线程保存共享成员变量的私有拷贝，而且只当线程进入或者离开同步代码块时才与共享成员变量的原始值对比。这样当多个线程同时与某个对象交互时，就必须要注意到要让线程及时的得到共享成员变量的变化。而volatile关键字就是提示VM：对于这个成员变量不能保存它的私有拷贝，而应直接与共享成员变量交互。使用建议：在两个或者更多的线程访问的成员变量上使用volatile。当要访问的变量已在synchronized代码块中，或者为常量时，不必使用。由于使用volatile屏蔽掉了VM中必要的代码优化，所以在效率上比较低，因此一定在必要时才使用此关键字。 就跟C中的一样 禁止编译器进行优化~~~~

  - ThreadLocal
    ThreadLocal不是为了解决多线程访问共享变量，而是为每个线程创建一个单独的变量副本，提供了保持对象的方法和避免参数传递的复杂性。

    顾名思义它是local variable（线程局部变量）。它的功用非常简单，就是为每一个使用该变量的线程都提供一个变量值的副本，是每一个线程都可以独立地改变自己的副本，而不会和其它线程的副本冲突。从线程的角度看，就好像每一个线程都完全拥有该变量。(ThreadLocal采用了“以空间换时间”的方式)

## 创建线程

- 继承Thread类，重写run方法
  传送门：[创建线程的两种方式](https://blog.csdn.net/mark_lq/article/details/50292969)
- 实现Runnable接口，重写run方法
- 实现Callable接口，重写call方法
  - 异步计算结果Future/FutureTask
  传送门：[Java并发之Runnable、Callable、Future、FutureTask](https://www.jianshu.com/p/cf12d4244171)
- 线程组
  传送门：[线程组](https://www.cnblogs.com/xrq730/p/4856072.html)
- 匿名内部类实现
  传送门：[匿名内部类实现](https://blog.csdn.net/qq_29720657/article/details/78705865)

## 终止线程

 1. 使用退出标志，使线程正常退出，也就是当run方法完成后线程终止。
 2. 使用stop方法强行终止线程（这个方法不推荐使用，因为stop和suspend、resume一样，也可能发生不可预料的结果）。
 3. 使用interrupt方法中断线程。

### 停止状态
  * 处于运行状态的线程停止
  * 即将或正在处于非运行态的线程停止
    * 处于可中断等待线程的停止
    * 处于IO阻塞状态线程的停止
  * 处于大数据IO读写中的线程停止
  * 在线程运行前停止线程

传送门：[终止线程](https://blog.csdn.net/anhuidelinger/article/details/11746365)

## 线程状态
  上面意见简单说过了。
  [线程状态](http://www.jiacheo.org/blog/338)

## Thread 类

### 对象方法
  - 启动start()
  - 终端interrupt()
  - 等待线程终止join()
  - 将该线程标记为守护线程或用户线程setDaemon(boolean on)
  - 更改线程的优先级setPriority(int newPriority)
  - 得到线程ID getId()
  - 得到或者设置线程名称 getName()和setName()

  传送门：[yield与join方法的区别](http://www.importnew.com/14958.html)

### 静态方法
  - 返回对当前正在执行的线程对象的引用currentThread()
  - 线程休眠sleep(long millis)
  - 暂停当前正在执行的线程对象，并执行其他线程yield()

## 线程同步

### synchronized
  - 可见性
  - 原子性(互斥性)
  - 可重入性

  [Synchronized的实现原理](http://www.hollischuang.com/archives/1883)

  [synchronized关键字详解](http://www.cnblogs.com/mengdd/archive/2013/02/16/2913806.html)

### volatile
  - 不保证原子性
  - 可见性
  - 有序性

   [volatile关键字](http://www.techug.com/post/java-volatile-keyword.html)

   [volatile关键字解析](http://www.cnblogs.com/dolphin0520/p/3920373.html)

### 显示锁 Lock

   [内置锁与显式锁](https://segmentfault.com/a/1190000009255406)

#### ReentrantLock
  - 公平锁与非公平锁
  - 获取锁lock()
  - 解锁unlock()
  - 尝试获取锁tryLock()
  - tryLock(long timeout, TimeUnit unit)
    在timeout时间内阻塞的获取锁，成功返回true，超时返回false。同时立即处理interrupt信息，并抛出异常。

  [ReentrantLock之公平锁与非公平锁浅析](https://blog.csdn.net/zmx729618/article/details/51593666)

#### ReentrantReadWriteLock
  - 公平锁与非公平锁
  - 返回用于读取操作的锁（共享锁）readLock()
  - 返回用于写入操作的锁（独占锁）writeLock()
  - 读读共享、读写互斥、写读互斥、写写互斥

  [Java并发编程--ReentrantReadWriteLock](https://www.cnblogs.com/zaizhoumo/p/7782941.html)

----
  下面的先列一下，之后抽时间看过之后再来补充
----

### 并发编程工具类

#### 闭锁CountDownLatch
  - 计数器减1 countDown()
  - 阻塞等待至计数器为0 await()
  - await(long timeout,TimeUnit unit)
#### 关卡CyclicBarrier
  - 阻塞互相待await()
  - await(long timeout,TimeUnit unit)

#### 信号量Semaphore
  - 公平策略与非公平策略
  - 从此信号量阻塞地获取一个许可 acquire()
  - 释放一个许可，将其返回给信号量 release()
#### AQS

### 乐观锁和悲观锁

## 线程通信

### 基于共享内存通信
  - 管道
  - ThreadLocal
    重写initialValue解决空指针问题
### wait() 与 notify/notifyAll()
### 显示锁Lock的Condition通信
### join

## 线程异常捕获
  - UncaughtExceptionHandler
  - 线程组重载UncaughtException

## 线程池

### 线程池定义

### 线程池组成
  - 线程池管理器
  - 工作线程
  - 任务接口
  - 任务队列

### concurrent包

### Executors框架

### Executor

## 原子类

### 基本类
### 引用类
### 数组类
### 属性原子更新类



