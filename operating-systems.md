# 问题收集


1. 多线程 多进场 临界资源的访问
a. 进程是资源分配（内存、计算）的基本单位，线程是程序执行的最小单位。
b. 进程有独立的地址空间，会记录自己的代码段、堆栈地址、数据地址。但是同一个进程的不同线程，会共享大部分数据，使用相同的地址空间。
c. 切换线程比进程快很多，开销小很多，因为共享地址空间。他也可以有自己的局部变量和堆栈。相互通信，线程之间也会方便很多，比如全局变量，静态变量。
d. 临界资源是一次只允许一个进程/线程访问的资源。访问的时候，需要告诉协调机构，进入临界资源、退出临界资源。
决定不同进程访问有两种方式，同步与异步。同步就是一个进程访问时，另一进程的访问会被互斥锁阻塞。

2.
【异步非阻塞】为什么用？因为我的评论监督的算法复杂度是关于评论的长度线性增长的。对于每条评论处理的时间不同。而且算法运行时，CPU会因为等待网络IO被闲置。所以我们需要一个非阻塞的后端去发挥CPU的性能。
【异步】调用完之后，被调用者结束后回调调用方。【同步】调用方等待被调用方执行完毕。
【非阻塞】调用方在调用的时候，屏蔽其他调用。