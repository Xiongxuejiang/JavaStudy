# JavaStudy

# 前言

</p>
 自2014年从南昌到上海参加实习工作以来，到现在的杭州工作也有三年了。行业有话说，三年一个坎，我觉得我的坎就要到了。所以我想总结一下自己的技术，写写文档总结。禅宗有语云：“时时勤拂拭，勿使惹尘埃。”，因为我们不是圣贤，所以以勤为本，才是我们技术人员的出路。
 </p>

# Java 基础篇


 1、HashMap 的源码，实现原理，JDK 8 对HashMap做了什么优化？


```
 原理：HashMap 是基于哈希表的 Map 接口实现类。
 优化：JDK 8 对 HashMap 底层的实现进行了优化，例如引入了红黑树数据接口和扩容的优化。
```


2、HaspMap扩容是怎样扩容的，为什么都是2的N次幂的大小？


```
每次 HashMap 在调用put()方法的时候，都会去判断 length 是不是超过极限值，如果超过了极限值，
就会调用扩容方法。
如果 length 为2 的次幂，那么length-1 转化为二进制必定是111... 的形式，这样的话操作效率会非常快而且不会浪费空间
```


3、HashMap、HashTable 和ConcurrentHashMap 有什么区别？


```
1、HashMap 是非线程安全的，而 HashMap 和 ConcurrentHashMap 是非线程安全的；
2、HashMap 是可以有键值为空（null）的存在，而HashTable 和 ConcurrentHashMap 有空会抛出空指针异常；
3、因为线程安全、哈希效率的问题，HashMap 效率比HashTable 的要高。
4、ConcurrentHashMap 对 整个桶书进行了分割分段（Segment），然后再没一点都使用了lock锁进行保护，相对于HashTable 的 syn 关键字锁的粒度更精细了一些
，并发性能更好，而HashMap 没有锁机制，不是线程安全的。
```
4、极高并发下的HashMap 和 concurrentHashMap 那个性能好，为什么，如何实现？

```
HashTable使用一把锁处理并发问题，当有多个线程访问时，需要多个线程竞争一把锁，导致阻塞
ConcurrentHashMap则使用分段，相当于把一个HashMap分成多个，然后每个部分分配一把锁，这样就可以支持多线程访问
```
5、HashMap在高并发下如果没有处理线程安全会有怎样的安全隐患，具体表现是什么。

```
HashMap事实上并非线程安全的，在高并发的情况下，是非常可能发生死循环的，由此造成CPU 100%，这是非常可怕的。
所以在多线程的情况下，用HashMap是非常不妥当的行为，应採用线程安全类ConcurrentHashMap进行取代。
```
6、java中四种修饰符的限制范围。
```
public： Java语言中访问限制最宽的修饰符，一般称之为“公共的”。被其修饰的类、属性以及方法不仅可以跨类访问，而且允许跨包（package）访问。
private: Java语言中对访问权限限制的最窄的修饰符，一般称之为“私有的”。被其修饰的类、属性以及方法只能被该类的对象访问，其子类不能访问，更不能允许跨包访问。
protect: 介于public 和 private 之间的一种访问修饰符，一般称之为“保护形”。被其修饰的类、属性以及方法只能被类本身的方法及子类访问，即使子类在不同的包中也可以访问。
default：即不加任何访问修饰符，通常称为“默认访问模式“。该模式下，只允许在同一个包中进行访问。
```
7、Object类中的方法
```
1，构造函数
2，hashCode和equale函数用来判断对象是否相同,
3，wait(),wait(long),wait(long,int),notify(),notifyAll()
4，toString()和getClass,
5，clone()函数的用途是用来另存一个当前存在的对象。
6，finalize()用于在垃圾回收
```
8、接口和抽象类的区别，注意JDK8的接口可以有实现。
```
相同点：
1. 接口和抽象类都能定义方法和属性。
2. 接口和抽象类都是看作是一种特殊的类。大部分的时候，定义的方法要子类来实现
3. 抽象类和接口都可以不含有抽象方法。接口没有方法就可以作为一个标志。比如可序列化的接口Serializable，没有方法的接口称为空接口。没有抽象方法的抽象类，小编不知道有什么作用，总之是可以通过编译的。
4. 抽象类和接口都不能创建对象。
5. 抽象类和接口都能利用多态性原理来使用抽象类引用指向子类对象。
6. 继承和实现接口或抽象类的子类必须实现接口或抽象类的所有的方法，抽象类若有没有实现的方法就继续作为抽象类，要加abstract修饰。若接口的子类没有实现的方法，也要变为抽象类。
不同点：
1. 接口能够多实现，而抽象类只能单独被继承，其本质就是，一个类能继承多个接口，而只能继承一个抽象类。
2. 方法上，抽象类的方法可以用abstract 和public或者protect修饰。而接口默认为public abttact 修饰。
3. 抽象类的方法可以有需要子类实现的抽象方法，也可以有具体的方法。而接口在老版本的jdk中，只能有抽象方法，但是Java8版本的接口中，接口可以带有默认方法。
4. 属性上，抽象类可以用各种各样的修饰符修饰。而接口的属性是默认的public static final
5. 抽象类中可以含有静态代码块和静态方法，而接口不能含有静态方法和静态代码块。
6. 抽象类可以含有构造方法，接口不能含有构造方法。
7. 设计层面上，抽象类表示的是子类“是不是”属于某一类的子类，接口则表示“有没有”特性“能不能”做这种事。如飞机和鸟都能飞，但是他们在设计上实现一个Fly接口，实现fly()方法。远比两个类继承飞行物抽象类好得多。因为，飞机和鸟有太多的属性不一样。
8. 设计层面上，另外一点，抽象类可以是一个模板，因为可以自己带集体方法，所以要加一个实现类都能有的方法，直接在抽象类中写出并实现就好，接口在以前的版本则不行。新版本Java8才有默认方法。
9. 既然说到Java 8 那么就来说明，Java8中的接口中的默认方法是可以被多重继承的。而抽象类不行。
10. 另外，接口只能继承接口。而抽象类可以继承普通的类，也能继承接口和抽象类。
```
9、动态代理两种方式以及区别
```
常见的实现代理的两种方式：（1）JDK动态代理（2）使用cglib产生代理
这两种方法各有好坏。jdk动态代理是由java内部的反射机制生成字节码并生成对象来实现的，而cglib代理底层是借助
asm来实现的，这个asm就是一个java字节码操纵框架，它能用来动态生成类或者增强类的功能，ASM从类文件中读入
信息后，改变类的行为，分析类的信息，这就跟aop实现方式中的静态织入的是一样的，就是相当于把切面织入类的
字节码文件中，以此达到拦截的作用。一般jdk动态代理用于目标类都是基于统一的接口，cglib多用于对类的代理，
这些类不需要实现统一的接口。
```
10、Java序列化的方式。
```
一、是相应的对象实现了序列化接口Serializable，这个使用的比较多，对于序列化接口Serializable
接口是一个空的接口，它的主要作用就是标识这个对象时可序列化的，jre对象在传输对象的时候会进行相关的封装；
二、实现序列化的第二种方式为实现接口Externalizable，Externalizable继承了Serializable 接口；
```
11、传值和传引用的区别，Java是怎么样的，有没有传值引用。
```
值传递：方法调用时，实际参数把它的值的副本传递给对应的形式参数。特点：此时内存中存在两个相等的基本类型，
即实际参数和形式参数，后面方法中的操作都是对形参这个值的修改，不影响实际参数的值。
引用传递：方法调用时，实际参数的引用(地址，而不是参数的值)被传递给方法中相对应的形式参数，
函数接收的是原始值的内存地址；特点：在方法执行中，形参和实参内容相同，指向同一块内存地址，
方法执行中对引用的操作将会影响到实际对象。
```
12、一个ArrayList在循环过程中删除，会不会出问题，为什么。
```
会出现问题
```
