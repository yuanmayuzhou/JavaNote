# Java集合
## 1.List

### ArrayList和Vector的区别？

ArrayList是List的主要实现类，使用数组存储，查找更快，线程不安全。

Vector是List的古老实现类，使用数组存储，线程安全。

### ArrayList和LinkedList的区别？

ArrayList和LinkedList都是不同步的，也就是不保证线程安全。

ArrayList采用数组存储，插入元素时，在这个元素后面的元素都要后移一位，所以插入元素性能较差，但是访问更快，直接通过下标就可查出。

LinkedList采用双向链表，插入或增加元素时只需要维护元素的前驱元素和后驱元素的指向即可。因此新增修改元素更快，查找更慢。

## 2.Set

HashSet，是Set接口的主要实现类，HashSet底层基于HashMap，所以是线程不安全的。

LinkedHashSet，是HashSet的子类，基于LinkedHashMap，能够按照插入顺序遍历。

TreeSet，底层使用红黑树，元素是有序的。

## 3.Queue

### Queue和Deque的区别？

Queue是单端队列，遵循先进先出原则，Deque是双端队列，可以从队首或者队尾加入元素。

### ArrayDeque和LinkedList的区别？

ArrayDeque和LinkedList都实现了Deque接口，两者都有队列的功能，ArrayDeque基于可变长的数组加双指针来实现，而LinkedList基于链表实现，所以ArrayDeque插入新元素可能需要扩容，不过均摊后每个插入操作依然为O(1)，而LinkedList不需要扩容，但是每次插入数据都需要申请新的堆空间，所以从性能角度上，使用ArrayDeque实现队列比LinkedList更好。

## 4.Map

### HashMap和Hashtable的区别？

线程安全，HashMap不是线程安全的，Hashtable是线程安全的，如果需要保证线程安全，最好使用ConcurrentHashMap，因为它使用的是分段锁，而Hashtable使用同步锁，锁住了整个方法，所以在操作期间，其他线程读取数据时需要等待操作完成。

### ConcurrentHashMap线程安全的具体实现方式？

JDK1.8后的ConcurrentHashMap取消了Segment分段锁，采用CAS和Synchronized来保证线程安全，数据结构还是HashMap的数组 + 链表 + 红黑树，synchronized只锁住当前操作位置的链表或红黑树的首节点，这样只要其他元素操作只要哈希不冲突就不会产生并发，只有当前这个链表哈希冲突了，才进入同步锁处理并发。