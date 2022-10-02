## CountDownLatch

CountDownLatch 表示计数器，可以给 CountDownLatch 设置一个数字，一个线程调用 CountDownLatch 的 await() 将会阻塞，其他线程可以调用 CountDownLatch 的 countDown() 方法对CowntDownLatch 中的数字减一，当数字被减到 0 ，所有的 await() 线程将被唤醒。

CountDownLatch 底层原理是调用 await() 方法的线程会利用 AQS 排队，一旦数字被减为 0 ，则会将 AQS 排队的线程依次唤醒。

## Semaphore

Semaphore 表示信号量，可以设置许可的个数。表示同时允许最多多少个线程使用该信号量，通过 acquire() 来获取许可，如果没有许可可用，则线程阻塞，并通过 AQS 排队。可以通过 release() 方法来释放许可，当某个线程释放许可后，会从 AQS 正在排队的第一个线程依次唤醒，直到没有空闲许可