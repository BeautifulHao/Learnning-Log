1、基本语法

包括static、final、transient等关键字的作用，foreach循环的原理等等。

越简单的问题越能看出一个人的水平，别人对你技术的考量绝大多数都是以深度优先、广度次之为标准的，切记。


2、集合

非常重要，也是必问的内容。基本上就是List、Map、Set，问的是各种实现类的底层实现原理，实现类的优缺点。

集合要掌握的是ArrayList、LinkedList、Hashtable、HashMap、ConcurrentHashMap、HashSet的实现原理，能流利作答，当然能掌握CopyOnWrite容器和Queue是再好不过的了。

- ArrayList 元素可重复、有序、非线程安全、可空。底层基于数组实现，便于遍历查询，不便于插入和新增（底层数据复制）。Vector线程安全版本。ArrayList擅长于随机访问
- LinkedList 元素可重复、有序、非线程安全、可空。底层基于双向列表实现，便于插入新增（无数据复制），不利于遍历查询（链表遍历）。
- HashMap 键可唯一空，值可重复，无序，非线程安全。底层采用数组和单向列表实现。
- TreeMap 键以某种排序规则排序，内部以red-black（红-黑）树数据结构实现
- TreeSet 基于TreeMap实现的有序不重复集合
- HashSet底层使用了HashMap实现,按键保存，值为固定值，键不重复。

3、设计模式

面试中关于设计模式的问答主要是三个方向：

你的项目中用到了哪些设计模式，如何使用

知道常用设计模式的优缺点

能画出常用设计模式的UML图


4、多线程

这也是必问的一块了。问得深入一些比如说Thread和Runnable的区别和联系、多次start一个线程会怎么样、线程有哪些状态。当然这只是最基本的，出乎意料地，几次面试几乎都被同时问到了一个问题，问法不尽相同，总结起来是这么一个意思：

假如有Thread1、Thread2、Thread3、Thread4四条线程分别统计C、D、E、F四个盘的大小，所有线程都统计完毕交给Thread5线程去做汇总，应当如何实现？

你对这个问题是否有答案呢？不难，java.util.concurrent下就有现成的类可以使用。

另外，线程池也是比较常问的一块，常用的线程池有几种？这几种线程池之间有什么区别和联系？线程池的实现原理是怎么样的？实际一些的，会给你一些具体的场景，让你回答这种场景该使用什么样的线程池比较合适。

最后，虽然这次面试问得不多，但是多线程同步、锁这块也是重点。synchronized和ReentrantLock的区别、synchronized锁普通方法和锁静态方法、死锁的原理及排查方法等等...

synchronized和ReentrantLock的对比
到现在，看到多线程中，锁定的方式有2种：synchronized和ReentrantLock。两种锁定方式各有优劣，下面简单对比一下：
- synchronized是关键字，就和if...else...一样，是语法层面的实现，因此synchronized获取锁以及释放锁都是Java虚拟机帮助用户完成的；ReentrantLock是类层面的实现，因此锁的获取以及锁的释放都需要用户自己去操作。特别再次提醒，ReentrantLock在lock()完了，一定要手动unlock()
- synchronized简单，简单意味着不灵活，而ReentrantLock的锁机制给用户的使用提供了极大的灵活性。这点在Hashtable和ConcurrentHashMap中体现得淋漓尽致。synchronized一锁就锁整个Hash表，而ConcurrentHashMap则利用ReentrantLock实现了锁分离，锁的只是segment而不是整个Hash表
- synchronized是不公平锁，而ReentrantLock可以指定锁是公平的还是非公平的
- synchronized实现等待/通知机制通知的线程是随机的，ReentrantLock实现等待/通知机制可以有选择性地通知
- 和synchronized相比，ReentrantLock提供给用户多种方法用于锁信息的获取，比如可以知道lock是否被当前线程获取、lock被同一个线程调用了几次、lock是否被任意线程获取等等
总结起来，我认为如果只需要锁定简单的方法、简单的代码块，那么考虑使用synchronized，复杂的多线程处理场景下可以考虑使用ReentrantLock。当然这只是建议性地，还是要具体场景具体分析的。
最后，查看了很多资料，JDK1.5版本只有由于对synchronized做了诸多优化，效率上synchronized和ReentrantLock应该是差不多。


5、 IO

IO分为File IO和Socket IO，File IO基本上是不会问的，问也问不出什么来，平时会用就好了，另外记得File IO都是阻塞IO。

Socket IO是比较重要的一块，要搞懂的是阻塞/非阻塞的区别、同步/异步的区别，借此理解阻塞IO、非阻塞IO、多路复用IO、异步IO这四种IO模型，Socket IO如何和这四种模型相关联。这是基本一些的，深入一些的话，就会问NIO的原理、NIO属于哪种IO模型、NIO的三大组成等等。

如果用过Netty，可能会问一些Netty的东西，毕竟这个框架基本属于当前最好的NIO框架了（Mina其实也不错，不过总体来说还是比不上Netty的），大多数互联网公司也都在用Netty。


6、JDK源码

要想拿高工资，JDK源码不可不读。上面的内容可能还和具体场景联系起来，JDK源码就是实打实地看你平时是不是爱钻研了。我面试过程中被问了不少JDK源码的问题，其中最刁钻的一个问题——String的hashCode()方法是怎么实现的，幸好我平时String源代码看得多，答了个大概。JDK源码其实没什么好总结的，纯粹看个人，总结一下比较重要的源码：

List、Map、Set实现类的源代码

ReentrantLock、AQS的源代码

AtomicInteger的实现原理，主要能说清楚CAS机制并且AtomicInteger是如何利用CAS机制实现的

线程池的实现原理

Object类中的方法以及每个方法的作用


7、 框架

一般来说会问你一下你们项目中使用的框架，然后给你一些场景问你用框架怎么做，比如我想要在spring初始化bean的时候做一些事情该怎么做、想要在bean销毁的时候做一些事情该怎么做、MyBatis中$和#的区别等等，这些都比较实际了，平时积累得好、有多学习框架的使用细节自然都不成问题。

8、数据库

数据库十有八九也都会问到。一些基本的像union和union all的区别、left join、几种索引及其区别就不谈了，比较重要的就是数据库性能的优化，如果对于数据库的性能优化一窍不通，那么有时间，还是建议你在面试前花一两天专门把SQL基础和SQL优化的内容准备一下。

阿里Java工程师分享：高薪程序员应该具备的技能


9、数据结构和算法分析

数据结构和算法分析，对于一名程序员来说，会比不会好而且在工作中绝对能派上用场。数组、链表是基础，栈和队列深入一些但也不难，树挺重要的，比较重要的树AVL树、红黑树，可以不了解它们的具体实现，但是要知道什么是二叉查找树、什么是平衡树，AVL树和红黑树的区别。


10、 Java虚拟机

谈谈Java虚拟机中比较重要的内容：

Java虚拟机的内存布局

GC算法及几种垃圾收集器

类加载机制，也就是双亲委派模型

Java内存模型

happens-before规则

volatile关键字使用规则

也许面试无用，但在走向大牛的路上，不可不会。


11、Web方面的一些问题

Java主要面向Web端，因此Web的一些问题也是必问的。我碰到过问得最多的两个问题是：

谈谈分布式Session的几种实现方式

讲一下Session和Cookie的区别和联系以及Session的实现原理

这两个问题之外，web.xml里面的内容是重点，Filter、Servlet、Listener，不说对它们的实现原理一清二楚吧，至少能对它们的使用知根知底。另外，一些细节的方面比如get/post的区别、forward/重定向的区别、HTTPS的实现原理也都可能会被考察到。

阿里Java工程师分享：高薪程序员应该具备的技能

最后，如果有兴趣有时间，建议学习、研究一下SOA和RPC，面向服务体系，大型分布式架构必备，救命良方、包治百病、屡试不爽。
