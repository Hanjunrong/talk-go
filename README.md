# talk-go
talk-go读书汇笔记汇总

## 运行环境 Ubuntu 20.04  4CPU 8G内存

### 平均负载案例分析
安装iostat mpstat pidstat 命令

`$ apt install sysstat`

`$ apt install stress`  stress  linux系统压力测试工具

`$ apt install stress-ng`  stress  linux系统压力测试工具升级版


### 平均负载

平均负载是指单位时间内，系统处于可运行状态和不可中断状态的平均进程数，也就是平均活跃进程数，它和 CPU 使用率并没有直接关系。

#### 可运行状态

所谓可运行状态的进程，是指正在使用 CPU 或者正在等待 CPU 的进程，也就是我们常用 ps 命令看到的，处于 R 状态（Running 或 Runnable）的进程。

#### 不可中断状态

不可中断状态的进程则是正处于内核态关键流程中的进程，并且这些流程是不可打断的，比如最常见的是等待硬件设备的 I/O 响应，也就是我们在 ps 命令中看到的 D 状态（Uninterruptible Sleep，也称为 Disk Sleep）的进程。不可中断状态实际上是系统对进程和硬件设备的一种保护机制

####  平均负载的合理值

当平均负载高于 CPU 数量 70% 的时候，你就应该分析排查负载高的问题了。一旦负载过高，就可能导致进程响应变慢，进而影响服务的正常功能。


当定位到某个程序负载过高时, 可以记住它的pid, 使用 `$ lsof -p pid` 来定位程序的路径

#### CPU上下文切换

多个进程在切换执行时会导致系统负载升高, CPU的上下文切换就是导致的原因之一

CPU上下文就是运行任务前, 必须依赖的环境,包含CPU寄存器和程序计数器

CPU上下文切换就是保存上个任务的上下文,加载下个任务的上下文,运行新任务

保存的上下文会存储在系统内核中

CPU上下文切换分为进程上下文切换, 线程上下文切换, 中断上下文切换

#### linux进程5种状态

linux上进程有5种状态: 
1. 运行(正在运行或在运行队列中等待) 
2. 中断(休眠中, 受阻, 在等待某个条件的形成或接受到信号) 
3. 不可中断(收到信号不唤醒和不可运行, 进程必须等待直到有中断发生) 
4. 僵死(进程已终止, 但进程描述符存在, 直到父进程调用wait4()系统调用后释放) 
5. 停止(进程收到SIGSTOP, SIGSTP, SIGTIN, SIGTOU信号后停止运行运行) 

ps工具标识进程的5种状态码: 

D 不可中断 uninterruptible sleep (usually IO) 

R 运行 runnable (on run queue) 

S 中断 sleeping 

T 停止 traced or stopped 

Z 僵死 a defunct (”zombie”) process 


# 第一阶段总结  第一周（5.25~5.31）
遇到的问题: 

环境准备的还是不够充分 家中电脑和公司电脑都要能够立即进入学习状态

收获: 

可以带着目标学习倪老师的教程, 看小伙伴们的石墨文档链接, 在群里看大家的讨论总结, 可以立马在机器上验证自己的想法

我为什么要学习这门课程:

不想自己遇到性能问题时一筹莫展, 不想出问题后没有排查思路, 不想与别人交流时听不懂一些名词指标

给自己设立一个学习目标,分阶段完成,试验自学效果,在业余时间也有学习的紧张感,压迫感, 否则会无休止的玩游戏,消耗完业余时间且没有收获

深入了解一点linux的知识, 充分了解自己写的代码的性能, 运行状态, 不能一抹黑, 对同事和公司造成隐患

说明:

第一阶段刚加入talk-go读书会, 还没有充分制定学习计划, 第二周第一天补上

对第一阶段笔记📒整理不够, 文档只看到了第三章, 第二周每晚补上

第一阶段总结暂不涉及知识点, 知识点的总结另开文档补充, 依据学有所获,学有所查,硬背是不可能的


