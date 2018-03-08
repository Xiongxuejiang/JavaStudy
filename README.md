# JavaStudy

## 前言
</p>
 自2014年从南昌到上海参加实习工作以来，到现在的杭州工作也有三年了。行业有话说，三年一个坎，我觉得我的坎就要到了。所以我想总结一下自己的技术，写写文档总结。禅宗有语云：“时时勤拂拭，勿使惹尘埃。”，因为我们不是圣贤，所以以勤为本，才是我们技术人员的出路。
 </p>
 ## Java 基础篇
 </p>
 1、HashMap 的源码，实现原理，JDK 8 对HashMap做了什么优化？
 </p>
```
 原理：HashMap 是基于哈希表的 Map 接口实现类。
 优化：JDK 8 对 HashMap 底层的实现进行了优化，例如引入了红黑树数据接口和扩容的优化。
```
<p>
2、HaspMap扩容是怎样扩容的，为什么都是2的N次幂的大小？
</P>
```
每次 HashMap 在调用put()方法的时候，都会去判断 length 是不是超过极限值，如果超过了极限值，
就会调用扩容方法。

如果 length 为2 的次幂， 那么length-1 转化为二进制必定是111... 的形式，这样的话操作效率会非常快而且不会浪费空间
```
<p>
3、HashMap、HashTable 和ConcurrentHashMap 有什么区别？
</p>
```
1、HashMap 是非线程安全的，而 HashMap 和 ConcurrentHashMap 是非线程安全的；
2、HashMap 是可以有键值为空（null）的存在，而HashTable 和 ConcurrentHashMap 有空会抛出空指针异常；
3、因为线程安全、哈希效率的问题，HashMap 效率比HashTable 的要高。
4、ConcurrentHashMap 对 整个桶书进行了分割分段（Segment），然后再没一点都使用了lock锁进行保护，相对于HashTable 的 syn 关键字锁的粒度更精细了一些
，并发性能更好，而HashMap 没有锁机制，不是线程安全的。
```
