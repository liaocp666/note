1. Sychronized 是一个关键字，ReentrantLock 是一个类
2. Sychronized 是会自动加锁和释放锁，ReentrantLock 需要手动加锁和释放锁
3. Sychronized 的底层是 JVM 层面的锁，ReentrantLock 是 API 层面的锁
4. Sychronized 是非公平锁，ReentrantLock 是可选择公平锁或非公平锁
5. Sychronized 锁的是对象，锁信息保存在对象头中，ReentrantLock 通过代码中的 int 类型的 state 标志来表示锁的状态
6. Sychronized 底层有一个锁升级的过程