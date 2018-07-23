# Java 集合框架

  集合框架结思维导图：
  ![集合框架结思维导图](http://graph.guoyw.com/Java_notes/JavaSE/%E9%9B%86%E5%90%88%E6%A1%86%E6%9E%B6%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE.png)

### LinkedList
### ArrayList
### HashMap
  传送门： [HashMap详细介绍(源码解析)](https://www.cnblogs.com/skywang12345/p/3310835.html)
#### HashMap的主要对外接口

  - clear() 的作用是清空HashMap。它是通过将所有的元素设为null来实现的。
  - containsKey() 的作用是判断HashMap是否包含key。
  - getEntry() 的作用就是返回“键为key”的键值对，它的实现源码中已经进行了说明。
    这里需要强调的是：HashMap将“key为null”的元素都放在table的位置0处，即table[0]中；“key不为null”的放在table的其余位置！
  - containsValue() 的作用是判断HashMap是否包含“值为value”的元素。
  - entrySet()、values()、keySet()
    它们3个的原理类似，这里以entrySet()为例来说明。
    entrySet()的作用是返回“HashMap中所有Entry的集合”，它是一个集合
  - get() 的作用是获取key对应的value
  - put() 的作用是对外提供接口，让HashMap对象可以通过put()将“key-value”添加到HashMap中。
  - putAll() 的作用是将"m"的全部元素都添加到HashMap中
  - remove() 的作用是删除“键为key”元素

#### HashMap遍历方式