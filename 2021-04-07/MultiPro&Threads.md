## 多线程和多进程的区别是什么？
### 一.  多进程
1. 多进程优点
- 每个进程互相独立，不影响主程序的稳定性，子进程崩溃没关系；
- 通过增加CPU，就可以容易扩充性能；
- 可以尽量减少线程加锁/解锁的影响，极大提高性能，就算是线程运行的模块算法效率低也没关系；
- 每个子进程都有2GB地址空间和相关资源，总体能够达到的性能上限非常大
2. 多进程缺点
- 逻辑控制复杂，需要和主程序交互；
- 需要跨进程边界，如果有大数据量传送，就不太好，适合小数据量传送、密集运算
- 多进程调度开销比较大；
### 二.  多线程
1. 多线程的优点
- 无需跨进程边界；
- 程序逻辑和控制方式简单；
- 所有线程可以直接共享内存和变量等；
- 线程方式消耗的总资源比进程方式好；
2. 多线程缺点
- 每个线程与主程序共用地址空间，受限于2GB地址空间；
- 线程之间的同步和加锁控制比较麻烦；
- 一个线程的崩溃可能影响到整个程序的稳定性；
- 到达一定的线程数程度后，即使再增加CPU也无法提高性能，例如Windows Server 2003，大约是1500个左右的线程数就快到极限了（线程堆栈设定为1M），如果设定线程堆栈为2M，还达不到1500个线程总数；
- 线程能够提高的总性能有限，而且线程多了之后，线程本身的调度也需要消耗较多的CPU