# Java 多线程--学习笔记

知识体系图：
![知识体系图](http://graph.guoyw.com/Java_notes/JavaSE/多线程思维图.jpg)

## 多线程笔记
> 原文出处：[Java 多线程并发编程一览笔录](http://www.importnew.com/26678.html)

- 1. 线程是什么？

   线程是进程中独立运行的子任务。

- 2. 创建线程的方式

   方式一：将类声明为 Thread 的子类。该子类应重写 Thread 类的 run 方法
   方式二：声明实现 Runnable 接口的类。该类然后实现 run 方法
   **推荐方式二，因为接口方式比继承方式更灵活，也减少程序间的耦合。**

- 3. 获取当前线程信息？

   Thread.currentThread()

- 4. 线程的分类

   线程分为守护线程、用户线程。线程初始化默认为用户线程。
   setDaemon(true) 将该线程标记为守护线程或用户线程。
   **特性：设置守护线程，会作为进程的守护者，如果进程内没有其他非守护线程，那么守护线程也会被销毁，即使可能线程内没有运行结束。**

- 5. 线程间的关系？

   某线程a 中启动另外一个线程 t，那么我们称 线程 t是 线程a 的一个子线程，而 线程a 是 线程t 的 父线程。
   最典型的就是我们在main方法中 启动 一个 线程去执行。其中main方法隐含的main线程为父线程。

- 6. 线程API一览：如何启动、停止、暂停、恢复线程？

  - 6.1. start() 使线程处于就绪状态，Java虚拟机会调用该线程的run方法；
  - 6.2. stop() 停止线程，已过时，存在不安全性：
    - 6.2.1 是可能请理性的工作得不得完成；
    - 6.2.2 是可能对锁定的对象进行“解锁”，导致数据不同步不一致的情况。
    **推荐 使用 interrupt() +抛异常 中断线程。**
   3. suspend() 暂停线程，已过时。
   4. resume() 恢复线程，已过时。
   suspend 与resume 不建议使用，存在缺陷：
     * 是可能独占同步对象；
     * 是导致数据不一致。
   5. yield() 放弃当前线程的CPU资源。放弃时间不确认，也有可能刚刚放弃又获得CPU资源。
   6. t.join() 等待该线程t 销毁终止。

- 7. synchronized关键字用法

  - 7.1 原子性（互斥性）：实现多线程的同步机制，使得锁内代码的运行必需先获得对应的锁，运行完后自动释放对应的锁。
  - 7.2 内存可见性：在同一锁情况下，synchronized锁内代码保证变量的可见性。
  - 7.3 可重入性：当一个线程获取一个对象的锁，再次请求该对象的锁时是可以再次获取该对象的锁的。
  **如果在synchronized锁内发生异常，锁会被释放。**

  **总结：**

  - 7.1 synchronized方法 与 synchronized(this) 代码块 锁定的都是当前对象，不同的只是同步代码的范围
  - 7.2 synchronized (非this对象x) 将对象x本身作为“对象监视器”：
    - 7.2.1 多个线程同时执行 synchronized(x) 代码块，呈现同步效果。
    - 7.2.2 当其他线程同时执行对象x里面的 synchronized方法时，呈现同步效果。
    - 7.2.3 当其他线程同时执行对象x里面的 synchronized(this)方法时，呈现同步效果。
  - 7.3 静态synchronized方法 与 synchronized(calss)代码块 锁定的都是Class锁。Class 锁与 对象锁 不是同一个锁，两者同时使用情况可能呈异步效果。
  - 7.4 尽量不使用 synchronized(string)，是因为string的实际锁为string的常量池对象，多个值相同的string对象可能持有同一个锁。

- 8. volatile关键字用法

  - 8.1 内存可见性：保证变量的可见性，线程在每次使用变量的时候，都会读取变量修改后的最的值。
  - 8.2 不保证原子性。

- 9. 线程间的通信方式

  线程间通信的方式主要为共享内存、线程同步。

  线程同步除了synchronized互斥同步外，也可以使用wait/notify实现等待、通知的机制。

  - 1. wait/notify属于Object类的方法，但wait和notify方法调用，必须获取对象的对象级别锁，即synchronized同步方法或同步块中使用。
  - 2. wait()方法：在其他线程调用此对象的 notify() 方法或 notifyAll() 方法前，或者其他某个线程中断当前线程，导致当前线程一直阻塞等待。等同wait(0)方法。

    - 2.1 wait(long timeout) 在其他线程调用此对象的 notify() 方法或 notifyAll() 方法，或者其他某个线程中断当前线程，或者已超过某个实际时间量前，导致当前线程等待。 单位为毫秒。
    - 2.2 void wait(long timeout, int nanos) 与 wait(long timeout) 不同的是增加了额外的纳秒级别，更精细的等待时间控制。

  - 3. notfiy方法：唤醒在此对象监视器上等待的单个线程。选择是任意性的，并在对实现做出决定时发生。线程通过调用其中一个 wait 方法，在对象的监视器上等待。
  - 4. notifyAll方法：唤醒在此对象监视器上等待的所有线程。

  **需要：wait被执行后，会自动释放锁，而notify被执行后，锁没有立刻释放，由synchronized同步块结束时释放。**

  应用场景：简单的生产、消费问题。
  ```
  synchronized (lock) {//获取到对象锁lock
  	try {
  		lock.wait();//等待通信信号, 释放对象锁lock
  	} catch (InterruptedException e) {
  		e.printStackTrace();
  	}
  	//接到通信信号
  }
  ```
  ```
  synchronized (lock) {//获取到对象锁lock
  	lock.notify();//通知并唤醒某个正等待的线程
      //其他操作
  }
  //释放对象锁lock
  ```

- 10. ThreadLocal与InheritableThreadLocal

  让每个线程都有自己独立的共享变量，有两种方式：

  - 1. 该实例变量封存在线程类内部；如果该实例变量（非static）是引用类型，存在可能逸出的情况。
  - 2. 就是使用ThreadLocal在任意地方构建变量，即使是静态的（static)。具有很好的隔离性。
    - 2.1 重写initialValue()方法：  初始化ThreadLocal变量，解决get()返回null问题
    - 2.2 InheritableThreadLocal 子线程可以读取父线程的值，但反之不行