底层数据结构不同：ArrayList 底层是基于数组实现；LinkedList 底层基于链表实现

使用场景也不同：ArrayList 更适合随机查找；LinkedList 更适合删除和添加。

另外 ArrayList 和 LinkedList 都实现了 List 接口，但是 LinkedList 还额外实现了 Deque 接口，所以 LinkedList 还可以当做队列使用。