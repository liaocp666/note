* CopyOnWriteArrayList 内部也是通过数组实现的，在向 CoypOnWriteArrayList 添加元素时，会复制一个新的数组，写操作在新数组上进行，读操作在原数组上进行。
* 写操作和加锁，防止出现并发写入丢失数据的问题
* 写操作结束之后，会把原数组指向新数组
* CopyOnWriteArrayList 运行在写操作时读取数据，大大提高了读的性能，适合读多写少的场景。但 CopyOnWriteArrayList 会比较占用内存，同时可能读取到的数据不是实时最新的数据，所以不适合实时性要求很高的场景。