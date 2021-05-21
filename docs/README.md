# 高性能计算学习路线

## 高性能计算 = 高性能的算法 + 高性能的软件系统 + 高性能的硬件

HPC是一个比较综合的方向，涉及算法、体系结构、编程语言、操作系统、计算机网络等，还涉及专业的学科知识譬如生物信息学等，这也正是它的趣味性所在。High level 地想一想，要以最高效的方式来对一个给定问题求解，我们必然需要有高效的算法设计（上层）、高效的编程模型和代码生成（中层）、以及高效的计算机体系结构来执行机器码（下层）。要实现极致的效率，三者必须协作。

推荐入门书籍：

- OpenMP 和 MPI ：《并行程序设计导论》
- CUDA : 《CUDA 并行程序设计》 《GPU 编程指南》 第5、6、9章
- 运维 ： 《Linux命令行与shell脚本编程大全》 (“Linux Command Line and Shell Scripting Bible”)
- 编译、链接 ： 《程序员的自我修养:装载、链接与库》 《深入理解计算机系统》第7章

利用**提问**的方式来梳理下一些知识，大部分都是开放式问题， 启发你自己去查找资料、思考。

## 基础篇

- 什么是超算？
- 什么是并行计算？什么是并行分布式计算？为什么需要并行分布式计算？
- 什么是线程？什么是进程？

### 程序性能分析

- Intel vtune profiler 如何使用？
- 如何测试程序性能？什么是热点分析？
- 程序性能分析报告怎么看？
- 什么是火焰图？
- 什么是 ebpf？
- 有哪些常用的 profiler？
- 我应该优化程序哪一部分？
- 性能优化有哪些策略：
  1. 并行度优化
  2. 数据传输优化
  3. 存储器访问优化
  4. 向量化优化
  5. 负载均衡优化
  6. 多线程扩展性优化

### 学习OpenMP

- 什么是OpenMP？有什么作用？
- 如何使用OpenMP来加速我的代码？在Linux环境下如何配置？
- 我该在哪并行？如何选择并行区域？
- 什么是数据依赖？什么是数据冲突？如何解决？
- 什么是原子操作？为什么需要原子操作？
- 我该选择多少线程来运行呢？线程数量越多越好吗？
- 我的代码运行正确吗？如何检验优化后代码运行的正确性？
- 我的代码优化成功了吗？加速比如何计算？
- OpenMP实战：多线程矩阵乘法，矩阵分块乘法。

### 学习MPI

- 什么是MPI？
- MPI 有哪些实现（openmpi 、intel-mpi、 mpich2 、platform-mpi）
- 什么是主进程master，什么是从进程slave？
- 什么是进程间通信？为什么进程间需要通信？如何进行进程间通信？
- 如何发送数据和接收数据？都有哪些方法？每种方法之间又何不同？
- 什么是同步？为什么需要同步？
- 什么是死锁？如何避免死锁？我该如何编译和运行MPI程序？
- 为什么我在一个节点上运行这么多进程和我在多个节点上运行这么多进程时间不一样？
- MPI实战：矩阵乘法，矩阵分块乘法。

### 学习使用高性能集群

- 如何远程登录（SSH）？节点之间如何做到无密码访问？
- 集群是怎样运作的？什么是管理节点？什么是计算节点？
- 为什么所有节点都能看到同样的目录？什么是共享存储？
- 了解你的集群。集群拓扑结构是怎样的？配置是什么？使用的是什么网络？
- Linux基本命令 ？如何上传和下载文件？
- 如何从源码编译？什么是软件依赖？什么是动态链接库？什么是动态链接？什么是静态链接？
- 什么是脚本？掌握Shell脚本的使用。

## 提高篇

### 计算机体系结构

推荐 [现代微处理器架构 90 分钟指南](https://www.starduster.me/2020/11/05/modern-microprocessors-a-90-minute-guide/)

- CPU的频率、寄存器、缓存、内存的读写时延大概是一个什么比例？
- 内存，PCIE，显存的带宽大概有多大？
- 缓存的结构是什么？缓存里面有哪些设计指标？如何影响缓存的效果？
- 多核的CPU并行执行，缓存是如何保持一致的？
- CPU的流水线是什么？
- 分支预测是怎么做的？
- ILP(Instruction-level parallelism)是怎么做到的？
- 什么是 NUMA 节点？什么是 SMT？
- CPU的向量指令集（SIMD）是干嘛的？如何写程序用上SIMD？
- GPU和CPU的设计区别在哪？GPU适用于什么场合？
- GPU的编程范式是什么？GPU程序怎么写？
- GPU的摩尔定律终结没有？

### 操作系统、编译器、运行时系统、算法

推荐 [高速缓存与内存一致性专栏](https://zhuanlan.zhihu.com/p/136300660)

- 虚拟内存、TLB都是啥？为什么使用虚拟内存？
- 进程的内存分布是啥样的？
- OS眼中的线程、进程是如何被映射到多个CPU核心上执行的？线程之间是如何调度的？
- 最主要的一些编译优化都是啥？尤其是循环优化。
- 如何做性能分析？都有些啥工具？
- 如何用各种hardware performance counter？
- pthread怎么用？它是怎么实现的？
- OpenMP怎么用？它是怎么实现的？和pthread的区别与联系？
- OpenMP里面的各种细节，譬如如何同步、如何共享数据等
- MPI怎么用？它是怎么实现的？和OpenMP分别代表了什么模型？
- OpenMP里的各种细节，各种collect，如何同步之类的
- SIMD、SPMD、SIMT之间的区别是什么？
- 线程之间如何同步？
- 并行编程和串行编程有啥区别？
- 并行编程都有哪些模型？
- 如何把一个算法并行化？这个过程中都有哪些讲究？
- 如何把一个算法在GPU上高性能地实现？
- 如何实现lock-free数据结构和算法？
- 如何设计cache-oblivious algorithms？

## 参考资料与拓展阅读

- [Extreme HTTP Performance Tuning: 1.2M API req/s on a 4 vCPU EC2 Instance](https://talawah.io/blog/extreme-http-performance-tuning-one-point-two-million/) 展示了性能调优和热点分析的各种工具的使用。
- [Intel Developer Zone](https://software.intel.com/content/www/us/en/develop/home.html) 中有 vtune, advisor 等性能分析工具的使用指南，还有 intel 的各种高性能计算库的文档。
- [CUDA docs](https://docs.nvidia.com/cuda/index.html) 中有 CUDA 的文档和入门教程。
- [Linux perf](http://www.brendangregg.com/linuxperf.html) 介绍了对 Linux 进行性能分析与调优的各种工具

内容收集主要来自 [高性能计算学习路线](https://www.zhihu.com/question/33576416) 和 [华农队长的备赛指南](https://baijiahao.baidu.com/s?id=1623535574079054530&wfr=spider&for=pc)

部分内容如有侵权，请在 [我们的 GitHub repo](https://github.com/heptagonhust/HPC-roadmap) 中开一个 issue, 我们会尽快移除。

如果你有更好的想法，欢迎来开一个 Pull Request 来帮助改进这个入门文档。
