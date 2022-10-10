ThreadLocal 是 Java 中所提供的的线程本地存储机制，可以利用该机制将数据`缓存在某个线程内部`，该线程可以在任意时刻、任意方法中获取缓存的数据。

ThreadLocal 底层是通过 ThreadLocalMap 实现的，每个 `Thread 对象` 中都存在一个 ThreadLocalMap ，Map 中的 key 为ThreadLocal 对象，value 为需要缓存的数据。

在线程池中使用 ThreadLocal 可能会造成内存泄露。因为当 ThreadLocal 对象用完之后，未把把设置的 key-value ，也就是 Entry 对象进行回收。线程对象是通过强引用指向 ThreadLocalMap ，ThreadLocalMap 也是通过强引用指向 Entry 对象，所以就导致线程不会回收，Entry 对象也不会回收，从而出现内存泄露。解决办法：在使用 ThreadLocal 对象之后，手动调用 ThreadLocal 的 remove 方法，手动清除 Entry 对象。

ThreadLocal 经典的应用场景就是连接管理，一个线程持有一个连接，该连接的数据对象可以在不同的方法之间进行传递，线程之间不共享同一个连接

![[Pasted image 20221002001730.png]]