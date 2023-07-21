# 1.Introduction

### 1.1 The Benefits of Using GPUs

在同样的价格和功率下，图形处理器（GPU）的指令吞吐量和内存带宽比CPU高得多。因此，很多应用在GPU上比在CPU上运行得更快。此外，FPGA等其他计算设备也很节能，但是其编程灵活性比GPU差得多。

GPU和CPU的差异源于不同的设计理念。我们不妨把执行一系列的工作称为一个线程（thread）。CPU是用来尽可能快地并行执行几十个线程，而GPU是用来并行执行几千个线程的。这意味着GPU需要降低单个线程的性能来提高吞吐量。

由于GPU专门用于并行计算，它的晶体管更多的用于数据处理，图1显示了CPU和GPU的资源对比。

![](..\picture\图1.png)

<div align = "center">图1 GPU将更多的晶体管用于数据处理</div>

对于高度并行地计算，将更多的集体管用于数据处理收益更大。因为GPU可以通过计算隐藏内存访问延迟，而不是依靠更大的cache和复杂的流程控制（flow control）来避免内存访问延迟，这两种方式都要需要很多晶体管。

通常一个应用既有并行部分也有串行部分，所以需要GPU和CPU的混合系统来最大化整体性能。具有高度并行性的应用程序可以利用GPU的这种大规模并行特性来实现比CPU上更高的性能。

### 1.2 CUDA: A General-Purpose Parallel Computing Platform and Programming Model

2006年11月，NVIDIA推出了CUDA，一种通用并行计算平台及编程模型，它能够利用NVIDIA GPU来解决复杂计算问题。

CUDA附带了一个软件环境，允许开发人员使用C++作为高级编程语言。如图2所示，CUDA也支持其他语言、API或基于指令的方法。

![](..\picture\图2.png)

<div align="center">图2 GPU计算应用，CUDA能够支持不同语言和API。</div>

### 1.3 A Scalable Programming Model

多核CPU和GPU的出现意味着并行体系成为主流。而这种硬件体系下的挑战在于如何使得应用程序能够**透明地**扩展并行性，从而充分利用不断增加的处理器核数。

CUDA 并行编程模型就是用来解决这一问题的。它的核心是**三个关键抽象**：线程组的层次结构、共享内存和屏障同步。

它们指导程序员先将问题划分为粗粒度的子问题，由线程块（thread block）独立解决。再将子问题划分为细粒度的问题，由块内的线程协同解决。每一个线程块都可以调度到任意的多处理器上（如图3所示），这种方式保证了CUDA编程的可扩展性。

![](..\picture\图3.png)

<div align="center">图2 GPU计算应用，CUDA能够支持不同语言和API。</div>

### 1.4 Document Structure

文档包括如下部分：