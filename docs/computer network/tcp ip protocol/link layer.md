# 链路层

## 以太网和 IEEE 802 封装

以太网一般是指数字设备公司、Inter公司和Xerox公司在1982年联合公布的一个标准，它采用 CSMA/CD 作为媒体接入办法。

几年后，IEEE 公布了一个稍有不同的标准集，其中 802.2 定义了 LLC，802.3 针对 CSMA/CD 网络。

在 TCP/IP 中，以太网 IP 数据报的封装是在 RFC 894 中定义的，IEEE 802 网络的 IP 数据报封装是在 RFC 1042 中定义的。**默认**使用 **RFC 894** 中的定义。

以太网取代了其他局域网技术，例如令牌环，FDDI 和 ARCNET。

> 以太网分为**经典以太网**和**交换式以太网**两类。交换式以太网正是广泛应用的以太网，而经典以太网是原始形式，速度为 3~10 Mbps。
> 
> 经典以太网的拓扑为**总线型拓扑** (单根数据线广播传输数据，对应计算机可接收) ，交换式以太网为了减少冲突和提高效率，使用交换机来交换数据，拓扑结构变成**星型拓扑**，但是逻辑上仍然是总线型拓扑。

### RFC 894 / 以太网

以太网的封装格式如下：

Destination Address | Source Address | Type | Data | CRC
-|-|-|-|-
6 bytes | 6 bytes | 2 bytes | 46~1500 bytes | 4 bytes

Type 字段取值如下表：

<table>
<tr>
<th>类型取值</th>
<th colspan="2" align="center">请求内容</th>
</tr>
<tr>
<td>0800</td>
<td colspan="2">IP 数据报 (46~1500 bytes)</td>
</tr>
<tr>
<td>0806</td>
<td>ARP 请求/应答 (28 bytes)</td>
<td>PAD (18 bytes)</td>
</tr>
<tr>
<td>8035</td>
<td>RARP 请求/应答 (28 bytes)</td>
<td>PAD (18 bytes)</td>
</tr>
</table>

### RFC 1042 / 802.2 + 802.3

RFC 1042 是 IEEE 802.2/802.3 中定义的帧格式。

其中头定义如下：

802.3 MAC | 802.2 LLC | 802.2 SNAP | Data | CRC
-|-|-|-|-
14 bytes | 3 bytes | 5 bytes | 38~1492 bytes | 4 bytes

#### MAC

802.3 MAC 层 (介质访问控制子层) 字段的数据格式如下表：

Destination Address | Source Address | Length
-|-|-
6 bytes | 6 bytes | 2 bytes

Length: 后续数据的字节长度，但不包括 CRC 校验。

#### LLC

LLC (逻辑链路控制子层, Logic Link Control) 是局域网中数据链路的上层部分。LLC 为上层提供了处理任何类型 MAC 的方法，例如以太网 IEEE 802.3 CSMA/CD。在 LLC 子层下面是 MAC 层。

LLC 包括两个数据访问点 SSAP 和 DSAP。在这种定义下，网络寻址先寻找 MAC 地址，再寻找 SAP 地址。

LLC 子层提供4种操作类型：

- LLC1，不确认的无连接服务。
- LLC2，面向连接服务。
- LLC3，带确认的无连接服务。
- LLC4，高速传送服务。

任何 802.2 LLC 都有如下数据格式：

<table>
<tr>
<th colspan="3" style="text-align:center;">802.2 LLC Header</th>
<th rowspan="2" style="text-align:center;"><br/>Information</th>
</tr>
<tr>
<th>DSAP address</th>
<th>SSAP address</th>
<th>Control</th>
</tr>
<tr>
<td>8 bits</td>
<td>8 bits</td>
<td>8 or 16 bits</td>
<td>multiple of 8 bits</td></tr>
</table>

#### SNAP

当使用 SNAP (子网接入协议, Sub-network Access Protocol) 时，802.2 LLC 的数据格式如下表所示：

<table><tbody>
<tr>
<th colspan="3" style="text-align:center;">802.2 LLC Header
</th>
<th colspan="2" style="text-align:center;">SNAP extension
</th>
<th rowspan="2" style="text-align:center;"></br>Upper layer data
</th></tr>
<tr>
<th>DSAP</br>AA
</th>
<th>SSAP</br>AA
</th>
<th>Control</br>03
</th>
<th>OUI</br>00
</th>
<th>Protocol ID
</th></tr>
<tr>
<td>8 bits
</td>
<td>8 bits
</td>
<td>8 or 16 bits
</td>
<td>24 bits
</td>
<td style="text-align:center;">16 bits
</td>
<td>multiple of 8 bits
</td></tr></table>

DSAP (目的服务访问点, Destination SAP): 目标服务访问点

SSAP (源服务访问点, Source SAP): 源服务访问点

Type 取值有三种：

<table>
<tr>
<th>类型取值</th>
<th colspan="2" align="center">请求内容</th>
</tr>
<tr>
<td>0800</td>
<td colspan="2">IP 数据报 (38~11492 bytes)</td>
</tr>
<tr>
<td>0806</td>
<td>ARP 请求/应答 (28 bytes)</td>
<td>PAD (10 bytes)</td>
</tr>
<tr>
<td>8035</td>
<td>RARP 请求/应答 (28 bytes)</td>
<td>PAD (10 bytes)</td>
</tr>
</table>

### CSMA/CD

CSMA/CD（Carrier Sense Multiple Access with Collision Detection，载波侦听多路访问/冲突检测协议）协议用于检测通信冲突并校正，其运行速率为 10Mb/s，地址为 48 bit。

CSMA/CD 标准在 IEEE 802.2 中定义。

实际上，冲突是以太网电缆传输距离限制的一个因素。

> 载波侦听（Carrier Sense），意思是网络上各个工作站在发送数据前，都要确认总线上有没有数据传输。若有数据传输（称总线为忙），则不发送数据；若无数据传输（称总线为空），立即发送准备好的数据。
> 
> 多路访问（Multiple Access），意思是网络上所有工作站收发数据，共同使用同一条总线，且发送数据是广播式。
> 
> “冲突检测”是指发送结点在发出信息帧的同时，还必须监听媒体，判断是否发生冲突（同一时刻，有无其他结点也在发送信息帧）。

#### 工作过程

一个节点监听信道并发送信息的过程总共分为 7 步：

1. （先听）载波监听，节点监听信道信息，确保某个信道未在使用中。
2. （无声再讲）如果信道一段时间内无声（称为帧间缝隙 IFG），则开始传输。
3. （有空就讲）如果信道一直忙碌，那么出现最小 IFG 时，节点开始发送信息。
4. （边听边说）如果空信道中，两个节点（几乎）同时开始发送，此时产生碰撞，双方信息包均会冲突损坏。以太网在传输过程中不停监听信道，以检测以上冲突。
5. （冲突停止）如果节点在传输期间检测到碰撞，立即停止传输并向信道发送"拥挤"信号，以确保其他节点也发现冲突。
6. 在等待一段时间后，想发送的节点进行新的发送。
> 此时采用离散数学中的**二进制指数退避策略** (Binary Exponential Back off Policy) 算法来决定不同的节点的随机延迟。
7. 返回到第一步。

## 尾部封装

RFC 893 描述了一种用于以太网的封装格式，称作尾部封装 (trailer encapsulation)，能让内核到内核的复制更加高效，但现在已经遭到反对。

## SLIP

SLIP (串行线路 IP, Serial Line IP) 是一种在串行线路上对 **IP 数据报**进行封装的简单形式，在 RFC 1055 中有对它的详细描述。常用于低速的串行链路。

SLIP 规则如下：

1. IP 数据报以 END (0xc0) 字符作为结束。为了防止线路噪声被当成数据报内容，大多数实现在数据报的开头传输 END 以结束可能出错的报文。
2. `0xc0`(ESC) 用 `0xdb 0xdc` 表示
3. `0xdb`(SLIP 的 ESC 字符) 用 `0xdb 0xdd` 表示。

同时 SLIP 具有以下问题：

1. 每一端都要知道对方的 IP 地址
2. 数据帧汇总没有类型字段。如果一条串行线路用于 SLIP，则不能同时用于其他协议
3. SLIP 没有校验和，线路噪声产生的错误只能通过上层协议来发现或通过调制解调器来检测和纠错。
> 所以上层协议都提供 CRC，例如 IP 首部和 TCP 首部。

### 串行/并行

并行和串行指的是任务的执行方式。

**串行**是指多个任务时，各个任务按顺序执行，完成一个之后才能进行下一个。

**并行**指的是多个任务可以同时执行。

#### 通信时钟频率

时钟频率 (clock rate) 是指同步电路中时钟的基础频率，它以“若干次周期每秒”来度量，量度单位采用SI单位赫兹（Hz）。

## CSLIP

CSLIP 是压缩的 SLIP，是为了不在一个字节的短信息前添加40+字节的首部而提出的新协议，定义在 RFC 1144 中。

CSLIP 把 40 个字节压缩成 3 或 5 个字节，并且能在每一端维持 16 个 TCP 链接。

大多数 SLIP 产品都支持 CSLIP。

CSLIP 通过只发送首部字段中产生变化的部分来进行压缩，不变的部分由接收方填入。

## PPP

PPP (Point-to-Point Protocal, 点对点协议) 修改了 SLIP 中的所有缺陷，封装了更多的其他协议。

一条 PPP 会话主要经过**链路建立阶段**、**链路验证阶段**和**网络层协议阶段**和**网络层终止阶段**，LCP 数据报文是在链路建立阶段被交换的，它作为 PPP 的净载荷被封装在 PPP 数据帧的信息域中，NCP 协议数据报文是在网络协议阶段被交换的。

PPP 包括三部分：

1. 在串行链路上封装 IP 数据报的方法。PPP 支持 8 位和无奇偶检验的异步模式，还支持面向比特的同步链接。
2. 建立、配置和测试数据链路的网络控制协议 (LCP, Link Control Protocol)。它允许通信双方进行协商以确定不同选项。
3. 针对不同网络层协议的网络控制协议 (NCP, Network Control Protocol)。当前 RFC 定义的网络层有 IP、OSI网络层、DECnet 和 AppleTalk。

PPP 协议的数据帧格式如下：

<table>
<tr>
<th>标志</br>7E</th>
<th>地址</br>FF</th>
<th>控制</br>03</th>
<th>协议</th>
<th>信息</th>
<th>CRC</th>
<th>标志</br>7E</th>
</tr>
<tr>
<td>1 bytes</td>
<td>1 bytes</td>
<td>1 bytes</td>
<td>2 bytes</td>
<td>less than 1500 bytes</td>
<td>2 bytes</td>
<td>1 bytes</td>
</tr>
</table>

协议字段取值如下：

协议取值 | 信息内容
-|-
0021 | IP 数据报
C021 | 链路控制数据
8021 | 网络控制数据

协议后紧跟地址字节 `0xff` 和控制字节 `0x03`。

在同步链路中，标志字符 `0x7e` (`01111110`) 出现时，需要通过比特填充转义成 `011111010`。

在异步链路中，转义字符 `0x7d` 出现时，下一个字符的第六个 bit 取补码，例如 `0x7e` 转换成 `0x7d 0x5e`，`0x7d` 转换成 `0x7d 0x5d`，默认情况下字符值小于 `0x20` (ascii码小于0x20的都是特殊字符)，一般都要进行转义，以防它们原有的特殊含义被调制解调器等错误解释。

异步链路中的采用了不完整的比特填充技术，以强制执行错误检测。

```
7E
0111 1110

7D        5E
0111 1101 0101 1110     //二进制表示

1011 1110 0111 1010     //传输字符串，根据 RS-232 规定，最低位优先发送
                ^
                |-- 这一位变化了
```

> RS-232是美国电子工业联盟（EIA）制定的串行数据通信的接口标准，被广泛用于计算机串行接口外设连接。

PPP 相比于 SLIP 增加了三个字节：协议字段 1 个字节，CRC 字段 2 个字节。同时 PPP 也使用 IP 网络控制协议，能减小 IP 和 TCP 首部的长度（对应 CSLIP）。

虽然优点很多，但是每帧多三个字节，同时需要发送 LCP 数据包进行更复杂的协商。

### 同步/异步通信

**同步** (synchronous) 指没有停顿的连续数据流，中间没有间隔。

同步有以下特点：

- 强大的错误检测 (例如 CRC)
- 数据传输同步的计时组件
- 用于高速高容量传输
- 与异步相比减少管理费用

**异步** (asynchronous) 有如下特点：

- 没有计时组件
- 使用处理位围绕每个字节
- 用校验位控制错误
- 每个字节需要三个指令 (开始，停止，校验)

### 比特填充

比特填充 (bit stuffing) : 当 `01111110` (`0x7e`) 作为帧结束标志时，如果这个字节同时也出现在信息中，那么在五个 `1` 之后需要插入一个 `0` 来转义。

当检测到 `11111` 时，如果第六位是 `0`，则删去 `0`，后续字符拼接得到原字符，如果后两位是 `10` 代表标志字段 (在这里就是帧结束标志)，如果是 `11` 代表异常终止状态。

### LCP

LCP (Link Control Protocal, 链路控制协议) 是 PPP 的子集，PPP 通信中通过收发 LCP 包来确定数据传输中的必要信息。

链路控制协议能指定需要转义的字符和协商省略标识符和地址字段，并把协议字段由两个字节减少成一个字节。

LCP 协议作用如下：

- 检查链接设备的身份并确定是否接收链接
- 确定通信中能接受的数据包尺寸
- 搜索配置错误
- 如果要求超过参数，可以终止链接

## 环回接口

环回接口 (Loopback Interface) 允许同一台主机上的客户程序和服务器程序通过 TCP/IP 进行通信，A 类网络号 `127` 就是为环回接口预留的，大多数系统把 IP 地址 `127.0.0.1` 分配给这个接口，并命名为 `localhost`。传给环回接口的数据报不能再任何网络上出现。

环回接口检查目的 IP 地址和广播地址、多播地址、接口 IP 地址是否相同。相同时通过环回驱动程序放入 IP 输入队列中。

## MTU

MTU (最大传输单元 ,Maximum transmission unit) 指链路层协议的数据最大传输量。超过需要进行分片 (fragmentation)。

其中点到点的链路层 (例如 SLIP 和 PPP) 的 MTU 不是网络媒体的物理特性，而是逻辑限制，目的是为交互使用提供足够快的响应时间。

## 路径 MTU

如果两台主机之间的通信通过多个网络，那么通信路径中最小的 MTU 称为**路径 MTU**，RFC 1191 描述了确定路径 MTU 的方法。

路径 MTU 不是常数，而取决于但是所选择的路由，而选路不一定是对称的 (A到B和B到A的路由可能不同)，因此两个方向的路径 MTU 不一定相同。

## 串行线路吞吐量计算

简单理解成 payload 在传输数据中的占比。

### 分组交换

分组交换 (packet switching) 是在通信过程中，通信双方以分组为单位、使用存储-转发机制实现数据交互的通信方式。

> 分组：分组交换将数据划分成多个等长的数据段，每个加上首部的数据段就是分组。