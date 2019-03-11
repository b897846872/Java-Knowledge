## 请简述session和cookie的区別.

## HashMap和HashTable区别。
```
1.hashmap可以接受键值（key）和值（value）为null，而hashTable不可以。
2.hashmap是非synchronized，而hashTable是synchronize。也就是说hashTable是线程安全的，多个线程可以共享一个hashTable。Java 5提供了concurrentHashMap，他是hashTable的替代品。
3.由于hashTable是线程安全的，所以在单线程环境下它要比hashMap慢。如果不需要同步，只需要单线程，那么使用hashMap要比hashTable性能好的多。
4.HashMap的迭代器(Iterator)是fail-fast迭代器，而Hashtable的enumerator迭代器不是fail-fast的。所以当有其它线程改变了HashMap的结构（增加或者移除元素），将会抛出ConcurrentModificationException，但迭代器本身的remove()方法移除元素则不会抛出ConcurrentModificationException异常。
5.HashMap不能保证随着时间的推移Map中的元素次序是不变的。

```
## HashSet和TreeSet的区别。

## ArrayList和LinkedList的区别。

## ==与equals的区别。
