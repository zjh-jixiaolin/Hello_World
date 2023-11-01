# 资料


[TOC]

## 2.1 单片机的内部资源

### 2.1.1 单片机的三大资源

---

- `Flash` — 程序存储空间，早期单片机为 `OTPROM`。

- `RAM` — 数据存储空间。

- `SFR` — 特殊功能寄存器。

  ![image-20230718221451008](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202307182217222.png)

#### Flash（程序存储空间）

​	在早期的单片机，主要使用 `OTPROM`（即一次可编程只读存储器）存储单片机程序，程序只能写入一次，如果需要重写程序则只能换一片（成本较高）。随技术的发展出现了 `Flash` ，其特点是**可反复擦写**、**容量大**、**成本低**。对于单片机 `Flash` 最大意义是 **断电后数据不丢失** （概念类似于电脑硬盘）。

#### RAM（数据存储空间）

​	`RAM` 是单片机数据存储空间，用来存储 **程序运算过程中产生的和需要的数据**（概念类似于电脑内存），优点是 **读写速度快**、**理论无限次写入（寿命无限）**，缺点就是 **断电后数据丢失**。举个例子，用计算器算个加减法，一些中间的数据都会保存在 RAM 里边，关电后数据丢失，所以我们每次打开计算器，都是从归零开始计算。

#### SFR（特殊功能寄存器）

​	`SFR` 是单片机**内部外设**和 `CPU` 交互的寄存器。`CPU` 通过读写 `SFR` 来**配置外设**,从而**控制**单片机的**输入输出**和**其他功能**。单片机有很多的功能，每个功能对于一个或多个 `SFR`，而我们通过 `SFR` 的**读写**即可实现单片机的各种多样性功能。

>单片机有很多功能，每个功能对应一个或多个 SFR，我们就是通过对 SFR 的 **读写** 来实现单片机的多种多样的功能的。

### 2.1.2 51 单片机

---

​	兼容 `Intel MCS-51` 体系结构的一系列单片机。课程使用的单片机为 `STC89C52`，由宏晶科技出品的一款 `51` 内核的单片机，具有标准的 `51` 体系结构，全部的 `51` 标准功能。

资源情况如下：

- `Flash` 程序空间是 `8KB` (`1K`=`1024`字节，`1` 字节= `8` 位)。
- `RAM` 数据空间是 `512` 字节。
- `SFR` 后边会逐一提到并且应用。

>比特（bit）是计算机内部数据的最小单位。计算机采用二进制形式存储数据，0和1分别表示比特。
>
>字节（Byte）是计算机操作数据的基本单位。由 8个连续的比特（bit）组成。字节作为一个整体，可以表示一个字符或数字。一个字节最大为8个1（11111111）即2的8次方，总共是256种状态。                
>
>**MB、KB、字节、bit位换算关系：1MB=1024KB、1KB=1024字节（Byte）、1字节=8bit。**                                                               
>
>参考：[详解计算机的字、字节（Byte）、比特（bit）](https://zhuanlan.zhihu.com/p/422907374)

