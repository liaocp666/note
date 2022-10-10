## 1.7 JDK

1. 1.7 版本基于 Seqment 实现
2. 每个 Seqment 相当于小型的 Hashmap
3. 每个 Seqment 内部进行扩容，和 Hashmap 的扩容逻辑类似
4. 先生成新的数组，然后转移元素到新数组中
5. 扩容的判断也是每个 Seqment 内部单独判断的，判断是否超过阈值

## 1.8

1. 1.8 版本不基于 Seqment 实现
2. 当某个线程进行 Put 时，如果发现 ConcurrentHashMap 正在进行扩容，那么该线程一起扩容
3. 当某个线程进行 Put 时，ConcurrentHashMap 没有进行扩容，则将 key-value 添加到 ConcurrentHashMap 中，然后判断是否超过阈值，超出了则进行扩容
4. 扩容之前也先生成一个新数组
5. 在转移元素时，先将原数组分组，将每组给不同的线程进行元素转移，每个线程负责一组或多组的元素转移工作