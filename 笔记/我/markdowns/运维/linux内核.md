# Linux 内核

## 1.1、名词解释

1. RAM：随机存储器，内存

2. IP/EIP：instructor pointer，指令指针寄存器，记录将要执行的指针在代码段中的偏移地址

3. CS: 代码段寄存器，指向了cpu当前执行代码在内存中的位置 

   ip，cs都位于cpu中，两者搭配即是cpu将要执行的指令的内存地址

4. ROM：只读存储器，断电后数据不消失

## 1.2、启动过程

1. 芯片硬件上设置为启动就把cs:ip的位置指向0xFFFF0，即BIOS（rom芯片里）的地址

2. bios开始工作，检测显卡、内存、在内存中建立**中断向量表和中断服务程序**

3. boot操作系统

   中断向量表：存储中断服务程序的内存地址

   硬件厂商和操作系统厂商约定好第一次加载0盘面0磁道1扇区的bootselect程序，之后运行bootselect加载其余操作系统程序

   ![image-20220922133923937](/Users/liuyi/Library/Application Support/typora-user-images/image-20220922133923937.png)

4. 规划内存

   内核代码和数据

   主内存区：进程代码，内核管理进程数据结构

   缓冲区：主机与外设进行数据交换的中转站

   虚拟盘区：

## 1.3、linux介绍

### 1.3.1、组成

<img src="/Users/liuyi/Library/Application Support/typora-user-images/image-20220922182307736.png" alt="image-20220922182307736" style="zoom:50%;" />

1. 系统内存管理

2. 应用程序管理

3. 硬件设备管理

4. 文件系统管理

### 1.3.2、用户空间与内核空间

不同模式下cpu可以访问的寄存器、执行的指令不同

从用户到内核：系统调用或硬件中断

### 1.3.3、开机过程

- 1、主机加电自检，加载 BIOS 硬件信息。
- 2、读取 MBR 的引导文件(GRUB、LILO)。
- 3、引导 Linux 内核。
- 4、运行第一个进程 init (进程号永远为 1 )。
- 5、进入相应的运行级别。
- 6、运行终端，输入用户名和密码。

### 1.3.4、进程通信方式

- 1、管道(pipe)、流管道(s_pipe)、有名管道(FIFO)。
- 2、信号(signal) 。
- 3、消息队列。
- 4、共享内存。
- 5、信号量。
- 6、套接字(socket) 。

### 1.3.5、linux文件

<img src="https://pic1.zhimg.com/80/v2-56eba6191fac72a38203b9a17f4d4820_1440w.jpg" alt="img" style="zoom:50%;" />

### 1.3.6、硬连接，软连接

![preview](https://pic4.zhimg.com/v2-6e3f86a3b42b86bd4ed0079247efbd2b_r.jpg)

其余不写了，太多