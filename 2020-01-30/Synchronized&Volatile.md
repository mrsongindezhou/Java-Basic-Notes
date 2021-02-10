
## 简述 Synchronized，Volatile，可重入锁的不同使用场景及优缺点
#### synchronized：
- 场景：最常用的用于保证线程安全的方式，其使用相对也比较简单，适用于同步代码执行时间较长；
- 优点：线程不会进行自旋，不占用CPU资源；
- 缺点：线程阻塞，响应时间长
#### volatile：
- 场景：主要用于一个线程写，多个线程读的场合；
- 优点：线程能直接读取内存中最新的数据，如果volatile变量修饰符使用恰当的话，它比synchronized的使用和执行成本更低，因为它不会引起线程上下文的切换和调度；
- 缺点：不保证原子性，不能保证线程安全
#### 可重入锁：
- 场景：ReentrantLock和synchronized都是可重入锁，用在定时任务，如果定时任务执行时间超过下次计划执行时间，确保只有一个线程正在执行；
- 优点：有公平和非公平两种模式，还可以避免死锁；
- 缺点：需要在finally块中释放锁