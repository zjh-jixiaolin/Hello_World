# 测试笔记

[TOC]



## ① 接口可靠性

### 1. RS232

串口重定向只测一个  

![image-20231020103641346](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310201432618.png)

![image-20231020103724529](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310201432184.png)

**Burnintest 接口吞吐量峰值：**

![image-20231020103940723](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310201432193.png)

**100cycles 数据总量查看：**

![image-20231020104021816](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310201432739.png)

#### **串口发送文件：**

**准备：**

- 测试串口10m发送10MB文件，需一台串口测试主机（4H 熊工后边）和串口线。被测板（如S821）需将 **串口发送接收软件** 放到C盘根目录下，并根据板上接口数量修改 **ComReceive.bat** 和 **ComSend.bat** 脚本内容。

  >修改脚本时，需对应主板上的com口（例如：被测主板的com2进行接收时间，则需要保留脚本中的 com2receive.ttl，其余进行注销）。

**测试：**

- **发送：** 被测板子运行 **ComSend.bat**，串口测试主机运行 **ComReceive.bat** 即可开始发送文件。
- **接收：** 被测板子运行 **ComReceive.bat**，串口测试主机运行 **ComSend.bat** 即可开始接收文件。

>注意发送或者接收文件时需要将过程进行截图保存，等待进度条到99%后进行拍照上传。

![image-20231020105438891](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310201432269.png)

<img src="https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310201431374.png" alt="image-20231020113509791" style="zoom:67%;" />

### 2. USB

USB3.0 和 USB2.0 **连接模式**识别步骤：

- 使用软件 **HWinfo** 进行检测识别，流程：Bus ——> PCI Bus #0 ——> Intel，Device ID # ——> USB大容量设备。![image-20231020143141642](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310201431421.png)









### 3. 声卡

前面板指 **板上插针**，后面板指  **板子USB接口、串口、网口** 这些。

**声卡强制输出：** 

- 强制将**音频信号**从计算机发送到**特定的输出设备**，不考虑系统或应用程序的默认设置（**不识别设备，直接强制输出**）。

  ![image-20231020141821583](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310201432879.png)



### 4. 网口

#### 强制速率：

![image-20231026160121466](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261750367.png)

#### 网口灯定义：

如下为 **S821** 网口灯定义截图，百兆通信和千兆通信时如果**只连接不通信时左灯为灭，连接且通信时左灯为绿灯闪烁**。

>实测时为通信状态，所以会跟规格书上有所不同。

![image-20231026160625908](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261750443.png)



## ② BIOS功能可靠性

### 1. 网络唤醒

在 U盘中找到网络唤醒软件，`LanWakeUp` 安装并启动，启动设置需要唤醒主机的MAC地址，唤醒主机进入S3或者S4，使用另外一台主机发包实现唤醒。

![image-20230731105459313](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/image-20230731105459313.png)



### 2. 网络引导 PXE

通常网络引导用来引导系统和重启，一般是用来批量控制或装机。用一台网络引导设备通过网线连接到需要操控的主机。**S821** 使用的是 **UEFI** 模式，通过 **PXE** 来引导安装系统或引导自动重启镜像，现在 **新平台** 只支持 **UEFI**，大概率不支持 **Legacy**。

被测主板需在 **BIOS下开启PXE网络配置并设置为首选项**，具体操作如下：

![image-20231026170610704](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261750026.png)

![image-20231026171059543](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261750975.png)

**设置启动项**

![image-20231026172012218](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261750902.png)

**f4保存退出后进入此界面等待PXE主机唤醒**

![image-20231026172257722](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261750818.png)

>完成此操作后，将被测主板和PXE主机的网口相连接.

**PXE主机操作如下：**

![image-20231026174219197](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261751067.png)

![image-20231026174525576](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261751083.png)

![image-20231026174900505](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261751834.png)

![image-20231026174941633](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261751558.png)

![image-20231026175010914](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261751102.png)



### 3.串口重定向

![image-20231026170217575](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261752232.png)

![image-20231026170400758](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310261752735.png)







## ④ 电源接口可靠性.

### 1. 电源输入

测试 **过压和欠压** 时需要查看板子是否 **上件过欠压保护**。



### 2. 电源输出







## ⑤ 一致性测试

### 1. RTC电池

**测量RTC空载电压值：**取下主板 RTC 电池，使用万用表怼电池正负极进行测量。

**测量主板RTC电池漏电流： ** 首先 **主板进行断电**，接上测量漏电流的 uA（微安） 电流表，电流表**负极接 CMOS 电池**，并将CMOS 电池接到开发板上，**正极接地**观察电流表，以此来测量漏电流（需断电测量）。

![image-20230925141106017](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202309251411477.png)



### 2. 漏电压

测量漏电压是为了确保开发板的安全性和可靠性。

**G3 to S5状态测量：** 异常断电后，板子通电不开机

**S0 to S5状态测量：** 系统下关机（通电不开机）

**SB：** 用于开发板在待机或关闭（关机）状态下提供较低的电压（存在的电压）

**VCC:** 用于提供设备的主要电源，确保主要组件和电路正常工作，一般为内存附件电感（R56 2314）

>5VSB：关机状态下存在5V的电压点，VCC5：开机状态下存在5V的电压点。



### 3.RTC时钟精度

AC Off 模式校时：使用 **ClockWise** 校时软件进行测试，校时服务器：**ntp1.aliyun.com**。校时后会显示 **你的系统时间校时正确** ，上拉记录时间，然后**关闭**电脑等待15小时（最低标准）后 **接上网线** 再进行校时，即可得出误差。

Power On模式校时：校时后，上拉记录时间，然后点击 **Close**，拔掉网线，主板在开机状态下静放 **15小时** 后再**接上网线**进行校时，即可得出误差

>进行校时需 **连接网线**。

![image-20231016150730816](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310161507071.png)



## ③ 显示接口可靠性

### 1. 单显

测试单显时，如副显接口不能单独显示（**不支持单显**）的话，则不需要测试，全部N/A。

**EDP** 显示接口不支持音频，只有 **HDMI** 和 **DP** 接口支持音频。















## ⑦ 环境可靠性

### 1. 高低温负载测试

进行高低温负载需准备 **4台设备** 跑不同负载软件，其中**Intel(R)ThermalAnalysisTool** 负载较重，DUT1 ~ 4的负载软件配置如下：

- DUT1：**Intel(R)ThermalAnalysisTool（CPU+Gfx）**，IP：192.168.1.1。
- DUT2：**Intel(R)ThermalAnalysisTool（监控）+ FurMark（GPU） + BurnlnTest（CPU，Disk，RAM）+ Chariot（网络负载）**，IP：192.168.1.2。
- DUT3：**Intel(R)ThermalAnalysisTool（监控）+  FurMark（GPU） + Prime95（CPU）+ Chariot（网络负载）**，IP：192.168.1.1。
- DUT4：**Intel(R)ThermalAnalysisTool（监控）+ FurMark + BurnlnTest（CPU，Disk，RAM）**，IP：192.168.1.2。

>Intel(R)ThermalAnalysisTool（CPU+Gfx）由于负载较重，不适合搭配 Chariot（网络负载）一起跑。



##### **前置准备：** 

---

①打开系统电源选项，将屏幕与睡眠改为从不。再点击 **其他电源设置**  进行设置，设置如下：

<img src="https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/image-20230719103937498.png" alt="image-20230719103937498"  />

② 左下角搜索组策略（编辑组策略）——> 计算机配置 ——> 管理模板 ——> 系统 ——> 电源管理 ——> 睡眠设置 ——> 将 **唤醒计算机时需要密码（接通电源）** 和 **当唤醒计算机需要密码（使用电池）**都改为 **已禁用** 然后应用确定。

![image-20231012095506010](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310121000825.png) 

③ 关掉Windows安全中心和防火墙。

![image-20231012094314526](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310120947988.png)

>**安装软件：**
>
>CPU负载软件：BrunlnTest、Prime95、Intel(R)ThermalAnalysisTool
>
>GPU负载测试软件：FurMask、Intel(R)ThermalAnalysisTool
>
>网络负载软件：IxCHariot（需要进行破解）

**完成以上初始化操作即可进行高低温负载测试、网络负载测试：**



##### BrunlnTest 测试

---

==BrunlnTest==：测试各类负载，进行 **高温负载** 测试时可作为 **CPU负载软件**，进行负载时选项如下：

<img src="https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/image-20230719105322794.png" alt="image-20230719105322794"  />

##### Prime95 测试

---

==Prime95==：**CPU负载软件**，具体配置 ——> **管理员权限**运行  prime95.exe ，弹出窗口选择 **Just Stress Testing** 后CPU负载开始。

![image-20230719110515317](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/image-20230719110515317.png)

![image-20231012095948528](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310121000373.png)

##### FurMask 测试

---

==FurMask==：测试 **图像负载（GPU）**软件，打开软件，选择**支持最大分辨率**后 ——> `GPU stress test` 即可开始测试，屏幕默认分辨率为 `1080P`，如果屏幕上有写分辨率参数，则需要软件选择对应分辨率。

<img src="https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/image-20230719105810789.png" alt="image-20230719105810789"  />

##### TAT 测试

---

==Intel(R)ThermalAnalysisTool==：Intel官方热分析工具，可测 **GPU图像负载和CPU负载**，还能监控 **CPU功耗和温度**。

监控设置操作如下：选择 **Monitor ALL** 然后再取消（取消那些自选的）—— 选择  **CPU Component** 拉开，将 **CPU0 ~ CPU3** 中的 **Frequency（功耗）**和 **DTS（温度）** 选上 —— 将**Power**中的 **IA Core Power（CPU 核心功耗）** 、**Integrated Graphics Power(集成显卡功耗)** 、**Rest of Package Power（剩余功耗）**、 **Package Power(总功耗)** 都选上即可。

<img src="https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310121725678.png" alt="image-20231012100850623"  />

##### Chariot 测试

---

==Chariot==：网络负载测试软件，测试前需将**软件安装好并激活**两台机器的 **IP** 进行设置，如 **192.168.1.1** 和 **192.168.1.2**，接上网线运行**测试配置文件（需放到桌面）**中的**1lan.tst（单网口的情况下）**，即可进行两台机器**双向收发**。

![image-20231012102020487](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310121020006.png)



<br />



### 2. 高低温 — CPU频率/功率检测

测试CPU占用率负载，分为 **Turbo（高性能模式）** 和 **非Turbo（普通模式）**，一般在 **BIOS**下进行模式的选择，使用测试软件为**Intel(R)ThermalAnalysisTool**，具体操作如下如下：

##### **单核 Turbo** 

---

一般板子默认为 **Turbo（高性能模式）** 模式，频率的 **参考值** 即为板子的 **CPU最大单核频率**，如图为2600MHz（参考 [ark.intel.com](https://ark.intel.com/content/www/cn/zh/ark/products/214758/intel-celeron-processor-j6412-1-5m-cache-up-to-2-60-ghz.html)）：

![image-20231013161257385](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140925583.png)

**单核Turbo CPU频率测试如图：**

![image-20231013160142219](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140925134.png)

**监控画面：**

![image-20231013160244847](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140925415.png)



##### 多核Turbo 和 多核非Turbo

---

多核Turbo：Turbo代表 CPU为**睿频（超频）**状态，多核需将CPU的所有核心都跑到 100%。

多核非Turbo：非Turbo代表 CPU为 **基频** 状态，多核需将CPU的所有核心都跑到 100%。

>**如何将CPU设置Turbo和非Turbo？**
>
>​	进入BIOS下设置为Turbo 或 非Turbo模式
>
>![image-20231013172511682](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140925969.png)
>
>![image-20231013172545106](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140925739.png)

![image-20231013175751541](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140925571.png)

![image-20231013180344682](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140926992.png)

![image-20231013180604419](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140926394.png)



##### CPU Power负载（PL1、PL2）

---

需要测试**多核Turbo CPU功率** 和 **多核非Turbo CPU功耗**，其中 **PL1和PL2参考值**如下图查看：

![image-20231013181012024](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140926279.png)

**测试演示：**

![image-20231016143559946](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310161436107.png)

![image-20231013181300926](https://raw.githubusercontent.com/zjh-jixiaolin/map_strong/main/202310140926134.png)

>Turbo 和 非Turbo模式在BIOS中开启或关闭



## ⑧ IO性能

### 1. RAM 性能

测试 RAM 性能时，先计算 **内存带宽理论值，作为测试的参考值（板载内存尚未有标准）**。然后查看板子内存为通道数，是否可拔插，如单通道内存指需要一根内存，双通道指至少需要两根内存。测试软件使用 **AIDA64进行内存测试**



### 2. SATA性能

如为板载开发板，则补测一个 **EMMC**的读写



### 3. USB性能

测试 **USB性能** 时需要使用 **USB 转 SATA盘** 接SATA进行测试（U盘通常跑不满速，使用 SATA能确保跑满和稳定性），**板卡3.0接口需要同时测试3.0和2.0的接口**。



### 4. 网口/光口性能

准备工作：被测板











## 专用词

S0：正常工作状态（开机到桌面）		S3：睡眠		S4：休眠		S5：关机

RX：接受		TX：发送





























































