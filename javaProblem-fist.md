## 请简述session和cookie的区別.
```
1.cookie数据存放在客户的浏览器上，session数据放在服务器上。
2.cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗
  考虑到安全应当使用session。
3.session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的
  性能考虑到减轻服务器性能方面，应当使用COOKIE。
4.单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

![1](https://images2017.cnblogs.com/blog/1200652/201712/1200652-20171207223151581-969964750.png "1")
```
## HashMap和HashTable区别。
```
1.hashmap可以接受键值（key）和值（value）为null，而hashTable不可以。
2.hashmap是非synchronized，而hashTable是synchronize。
  也就是说hashTable是线程安全的，多个线程可以共享一个hashTable。
  Java 5提供了concurrentHashMap，他是hashTable的替代品。
3.由于hashTable是线程安全的，所以在单线程环境下它要比hashMap慢。
  如果不需要同步，只需要单线程，那么使用hashMap要比hashTable性能好的多。
4.HashMap的迭代器(Iterator)是fail-fast迭代器，
  而Hashtable的enumerator迭代器不是fail-fast的。
  所以当有其它线程改变了HashMap的结构（增加或者移除元素），
  将会抛出ConcurrentModificationException，
  但迭代器本身的remove()方法移除元素则不会抛出ConcurrentModificationException异常。
5.HashMap不能保证随着时间的推移Map中的元素次序是不变的。

```
## HashSet和TreeSet的区别。
```
1.TreeSet是二差树实现的,Treeset中的数据是自动排好序的，不允许放入null值。
2.HashSet是哈希表实现的,HashSet中的数据是无序的，可以放入null，但只能放入一个null，
  两者中的值都不能重复，就如数据库中唯一约束。
3.HashSet要求放入的对象必须实现HashCode()方法，放入的对象，是以hashcode码作为标识的，
  而具有相同内容的String对象，hashcode是一样，所以放入的内容不能重复。但是同一个类的对象可以放入不同的实例。
```

## ArrayList和LinkedList的区别。
```
1.ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构。 
2.对于随机访问get和set，ArrayList觉得优于LinkedList，因为LinkedList要移动指针。 
3.对于新增和删除操作add和remove，LinedList比较占优势，因为ArrayList要移动数据。
```

## ==与equals的区别。
```
1.对于==，如果作用于基本数据类型的变量，则直接比较其存储的 “值”是否相等；
  如果作用于引用类型的变量，则比较的是所指向的对象的地址
2.对于equals方法，注意：equals方法不能作用于基本数据类型的变量
  如果没有对equals方法进行重写，则比较的是引用类型的变量所指向的对象的地址；
  诸如String、Date等类对equals方法进行了重写的话，比较的是所指向的对象的内容。
```
