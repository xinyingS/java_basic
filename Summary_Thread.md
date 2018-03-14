Summary about Thread

reference from: https://www.nowcoder.com/ta/review-java/review?page=12

1. 创建线程的方式，哪种最好，为什么：
  有4种方式可以用来创建线程：
(1)继承Thread类
(2)实现Runnable接口
(3)应用程序可以使用Executor框架来创建线程池
(4)实现Callable接口
实现Runnable接口这种方式更受欢迎，因为这不需要继承Thread类。在应用设计中已经继承了别的对象的情况下，这需要多继承（而Java不支持多继承），只能实现接口。同时，线程池也是非常高效的，很容易实现和使用。

2. 概括线程可用状态：
view picture: https://www.nowcoder.com/ta/review-java/review?page=13
(1). 新建( new )：新创建了一个线程对象。
(2). 可运行( runnable )：线程对象创建后，其他线程(比如 main 线程）调用了该对象 的 start ()方法。该状态的线程位于可运行线程池中，等待被线程调度选中，获 取 cpu 的使用权 。
(3). 运行( running )：可运行状态( runnable )的线程获得了 cpu 时间片（ timeslice ） ，执行程序代码。
(4). 阻塞( block )：阻塞状态是指线程因为某种原因放弃了 cpu 使用权，也即让出了 cpu timeslice ，暂时停止运行。直到线程进入可运行( runnable )状态，才有 机会再次获得 cpu timeslice 转到运行( running )状态。阻塞的情况分三种：
    (一). 等待阻塞：运行( running )的线程执行 o . wait ()方法， JVM 会把该线程放 入等待队列( waitting queue )中。
    (二). 同步阻塞：运行( running )的线程在获取对象的同步锁时，若该同步锁 被别的线程占用，则 JVM 会把该线程放入锁池( lock pool )中。
    (三). 其他阻塞: 运行( running )的线程执行 Thread . sleep ( long ms )或 t . join ()方法，或者发出了 I / O 请求时， JVM 会把该线程置为阻塞状态。            当 sleep ()状态超时、 join ()等待线程终止或者超时、或者 I / O 处理完毕时，线程重新转入可运行( runnable )状态。
(5). 死亡( dead )：线程 run ()、 main () 方法执行结束，或者因异常退出了 run ()方法，则该线程结束生命周期。死亡的线程不可再次复生。

reference from：https://www.nowcoder.com/questionTerminal/f665a4c853b841339e7181a0fdbacfa8
可以用早起坐地铁来比喻这个过程：
(1) 还没起床：sleeping
(2) 起床收拾好了，随时可以坐地铁出发：Runnable
(3) 等地铁来：Waiting
(4) 地铁来了，但要排队上地铁：I/O阻塞
(5) 上了地铁，发现暂时没座位：synchronized阻塞
(6) 地铁上找到座位：Running
(7) 到达目的地：Dead

reference from：https://www.nowcoder.com/questionTerminal/f665a4c853b841339e7181a0fdbacfa8
比较重要的几点需要注意：
(1) sleep和yield的区别在于, sleep可以使优先级低的线程得到执行的机会,  而yield只能使同优先级的线程有执行的机会.
(2) interrupt方法不会中断一个正在运行的线程.就是指线程如果正在运行的过程中, 去调用此方法是没有任何反应的. 为什么呢, 因为这个方法只是提供给 被阻塞的线程, 即当线程调用了.Object.wait, Thread.join, Thread.sleep三种方法之一的时候, 再调用interrupt方法, 才可以中断刚才的阻塞而继续去执行线程.
(3) join()  当join(0)时等待一个线程执行直到它死亡返回主线程,  当join(1000)时主线程等待一个线程1000纳秒,后回到主线程继续执行.
(4) waite()和notify()必须在synchronized函数或synchronized　block中进行调用。如果在non-synchronized函数或non-synchronized　block中进行调用，虽然能编译通过，但在运行时会发生IllegalMonitorStateException的异常。
