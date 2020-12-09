# TCP/IP 协议族

TCP/IP 倾向于使用路由器而不是网桥进行连接。

## TCP/IP 模型分层

```
用户进程 用户进程 用户进程 用户进程     应用层
   |        |       |       |
   |        |       |       |
   |       TCP      |      UDP      运输层
   |        |       |       |
   |        --------|--------
   |                |
  ICMP  --------   IP ---- IGMP     网络层
                    |
                    |
  ARP  --------  硬件接口 -- RARP    链路层
                    |
                    |   
                   媒体

# TCP/IP 协议分层图
```

### 应用层

应用层负责处理特定的应用程序细节。

在 TCP/IP 中，应用层提供 Telnet，FTP，SMTP，SNMP 等通用应用程序。

### 运输层

运输层为应用程序提供端到端通信。

在 TCP/IP 协议中，有两个协议在运输层工作：

- TCP 负责切分应用层数据，确认接收的分组，设置超时时钟等。

- UDP 负责把称作数据报的分组从一台主机发送到另一台主机。

### 网络层

网络层也叫互联网层。

网络层处理分组在网络中的活动，例如分组的选路。

### 链路层

链路层也叫数据链路层或网络接口层。

链路层包括操作系统中的设备驱动和网络接口卡，它们一起与电缆的物理接口细节。

## 封装

```
                                    |用户数据|
                                    |       |              应用程序
                                    |       |                |
                            |Appl首部 用户数据|               |
                            |               |                |
                            |               |              TCP
                    |TCP首部      应用数据   |                |
                    |<------- TCP 段 ------>|                |
                    |                       |              IP
            |IP首部  TCP 首部      应用数据   |                |
            |<--------- IP 数据报 ---------->|                |
            |                               |              以太网驱动程序
|以太网首部   IP首部  TCP首部      应用数据     以太网尾部|      |
|    14        20      20                         4   |      |
|<-------------------- 以太网帧 ---------------------->|    -----
                                                           以太网

# 数据进入协议栈的封装过程
```

当 TCP 传输数据时，数据被送入协议栈中，逐个通过每一层后变为比特流。这个过程中每一层会添加一些首部(尾部)信息。

TCP 传给 IP 的数据单元称作 TCP 报文或者 TCP 段 (TCP segment)。UDP 传给 IP 的数据单元称作 UDP 数据报 (UDP datagram)。

IP 传给接口的数据称作分组 (packet)，分组既可以是 IP 数据报 (IP datagram)，也可以是 IP 数据报的一个片 (fragment)。

通过以太网传输的比特流称作帧 (Frame)。

## 首部数据格式

(header format)

### TCP

TCP 首部数据结构可表示为下表

Source port | Destination port | Sequence number | Acknowledge number (if ACK set) | Data offset | Reservd | Flags | Window site | Checksum | Urgent pointer |
-|-|-|-|-|-|-|-|-|-
16 bits | 16 bits | 32 bits | 32 bits | 4 bits | 3 bits | 9 bits | 16 bits | 16 bits | 16 bits |

Sequence number (序列号): 存储本报文段所发送的数据的第一个字节的序号。

Acknowledge number (确认号): 存储期望收到的下一段数据第一个字节的序号。

Reservd (保留位): 二进制值为`000000`。

Window site (窗口大小): 存储期望对方发送的数据量。

Checksum (校验和): 

计算方法如下

1. 对 TCP 中每 16bits 数值进行二进制求和。
2. 如果和的高 16bits 不为零，则将和的高位 16bit 与低位 16bits 反复相加，直到高位 16bits 为零。
3. 将剩下 16bits 取反，存入校验和字段。

接收方重复以上步骤，并判断校验和相减是否为零。

Urgent pointer (紧急指针): 如果 URG 标志存在时，存储紧急数据的偏移量。

### UDP

UDP 首部数据长度为 8 bytes，结构可以表示为下表

| Source port | Destination port | UDP length | Checksum |
-|-|-|-
16 bits | 16bits | 16 bits | 16 bits |

Checksum 的计算方式与 TCP 一致。Checksum 在 ipv4 中可选，在 ipv6 中必选。

## 分用

协议盒检查报文首部中的协议标识，以确定接收数据的上层协议的过程，称为分用 (Demultiplexing)。

## 端口号

任何 TCP/IP 实现所提供的服务都用 1~1023 之间的知名端口号。

FTP 服务器的 TCP 端口号: 21

Telnet 服务器的 TCP 端口号: 23

TFTP 服务器的 UDP 端口号: 69

类 Unix 系统中的通用查找办法

```
grep telnet /etc/services
grep domain /etc/services
```

## RFC

RFC (Request for Comment) 文档规定了所有的 Internet 标准。

RFC 文档分为以下几种：

- 赋值 RFC: 列出所有 Internet 协议中的常数和数字
- Internet 正式标准协议: 描述协议的标准化现状
- 主机需求 RFC
- 路由器需求 RFC

## 标准的简单服务

