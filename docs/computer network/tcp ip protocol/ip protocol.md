# IP 协议

## IP 协议特点

- 不可靠：无法保证抵达目的地
- 无连接：不维护后续状态，每个数据报独立选择路由

## Header format

IP 首部数据结构可表示为下表

| Version | Header Length | Type of service | Total length | Identification | Flags | Fragment Offset | TTL | Protocol | Header Checksum | Source IP Addr | Destination IP Addr | Options | Padding |
-|-|-|-|-|-|-|-|-|-|-|-|-|-
| 4 bits | 4 bits | 8 bits | 16 bits | 16 bits | 3 bits | 13 bits | 8 bits | 8 bits | 16 bits | 32 bits | 32 bits | viriable length | ... |

**Version**: IPv4/IPv6

**Type of service** (TOS, 服务类型): 用于识别 IP 包的优先级，现在已忽略。RFC 1340 描述了所有的标准应用如何设置这些服务特性。

其中包含了一个 3 bits 的优先权子字段(已被忽略)，4 bits 的 TOS 子字段，和一位未用位(设置为0)。

TOS 要求四个值：最小时延(Telnet & Rlogin)、最大吞吐量(FTP)、最高可靠性(SNMP & 路由选择协议)、最小费用(Usenet news, NNTP)。

新的路由协议如 OSPF 等都能根据这些字段的值进行路由决策。

**Total length**: MTU 最大值为 65535 bytes。

当 IP 数据报长度小于以太网最小帧长度(46 bytes)时，数据链路层会填充数据到 46 bytes，所以总长度必不可少。

**Identification** (标识): 存储 IP 数据报的标识。通常每发送一份报文，他的值加 1。IP 数据报超出长度限制 (MTU) 时，分片发送的所有片上标识相同。

如果由 TCP 和 UDP 生成的不同数据报，它们的标识可能相同，这时候通过重组算法来处理。但是伯克利的延伸系统，每发送一个数据报，IP 层都要把一个内核变量的值加 1，不会产生以上问题。内核变量的初始值根据系统引导时的时间来设置。

**Flags**: 此字段取值如下表

取值 | 1 | 0
-|-|-
最低位 MF | 后面还
有分片的数据报 | 没有分片数据包
次低位 DF | 不能分片 | 可以分片
最高位(目前无效) |  | 

**Fragment offset** (片偏移): 代表分片在原始数据中的相对位置。片偏移用于重组分段的 IP 数据报。

**Protocol**: 存储上层数据来自哪个协议。

### 网络字节序

网络字节序(network-byte-order)：TCP/IP 首部中所有的二进制整数在网络传输时都要求以大端字节序传输，因此又称作网络字节序。

小端字节序在传输时，需要转换为大端字节序传输。

小端字节序方便计算，大端字节序用于传输更多是 RFC 1700 的规定。

### 位序

bit-endianness 