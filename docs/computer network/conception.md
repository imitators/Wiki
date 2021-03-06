# 概念

## OSI 模型

OSI (Open System Interconnect) 也叫开放式系统互联。

OSI 模型中，对等层协议之间交换的信息单元统称为协议数据单元 (PDU,Protocol Data Unit)。

各层对应数据名称如下：

- 传输层——数据段（Segment）
- 网络层——分组（数据包）（Packet）
- 数据链路层——数据帧（Frame）
- 物理层——比特（Bit）

## 网络设备

### 同轴电缆

同轴电缆 (Coaxial Cable) 为同心圆结构，从内到外分别是 `中心导体，绝缘材料层，网状织物，护套`，目前导体采用铜材质。

同轴电缆主要用于模拟信号和数字信号的传输。

同轴电缆基本类型有**基带同轴电缆**和**宽带同轴电缆**两种。

同轴电缆与光纤，地面微波，卫星等，共同组成了物理层的传输介质。

### 网关

网关 (gateway) 是网络连接设备的重要组成部分，它不仅具有路由的功能，而且能在两个不同的协议集之间进行转换，从而使不同的网络之间进行互联。

### 交换机

交换机也叫交换式集线器，它通过对信息进行重新生成，并经过内部处理后转发至指定端口。

### 网桥

网桥在链路层对网络进行互联。

### 路由器

路由器 (Router) 在网络层上对网络进行互联。

路由器能根据分组类型过滤和选择路由，支持在LAN段之间有多个链路的网络，当某个链路损坏时，可选择其他路由以及根据网络通信的情况决定路由。

路由器

### 网卡

网卡又称为网络适配器 (Network Adapter) 或网络接口卡 (Network Interface Card, NIC)。

## DNS

域名系统 (Domain Name System)是一个分布式数据库，它负责提供主机名和 IP 地址的映射。

## 数字证书

数字证书称为数字标识 (Digital Certificate ，Digital ID)，它是证明通信双方身份的数字信息文件，类似于身份证。

数字证书由权威机构，又称为证书授权 (Certificate Authority, CA) 机构发行。

比较专业的数字证书定义是，数字证书是一个经证书授权中心数字签名的包含公开密钥拥有者信息以及公开密钥的文件。

最简单的证书包含一个公开密钥、名称以及证书授权中心的数字签名。一般情况下证书中还包括密钥的有效时间，发证机关（证书授权中心）的名称，该证书的序列号等信息，证书的格式遵循相关国际标准。

### 原理

### 安装

## 二进制概念

### bit

bit (位，比特)，简写为 1b

### byte

1 byte (字节)= 8 bits，简写为 1B

### word

1 word (字)= 2 bytes

## 字节序

字节序 (endianness) 是计算机中字或者字节的存储顺序，分为大端字节序 (big endian) 和小端字节序 (little endian) 两种