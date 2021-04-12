# 侦察

web框架 中间件指纹 后端语言 前端语言 云服务

CDN UI框架 缓存

## 扫描

IP 资源/漏洞资源

网络扫描

```
nmap --script=vuln www.xxxx.com   // 漏洞扫描
nmap -sP 192.168.32.215     // Ping 扫描
nmap -sS 192.168.32.215     // TCPSYN 扫描
arp-scan -l                 // ARP 扫描
```

??? note "Nmap 扫描模式"
    **Tcp SYN Scan (sS)**。这是一个基本的扫描方式,它被称为半开放扫描，因为这种技术使得Nmap不需要通过完整的握手，就能获得远程主机的信息。Nmap发送SYN包到远程主机，但是它不会产生任何会话.因此不会在目标主机上产生任何日志记录,因为没有形成会话。这个就是SYN扫描的优势.如果Nmap命令中没有指出扫描类型,默认的就是Tcp SYN.但是它需要root/administrator权限.

    **Tcp connect() scan(sT)**如果不选择SYN扫描,TCP connect()扫描就是默认的扫描模式.不同于Tcp SYN扫描,Tcp connect()扫描需要完成三次握手,并且要求调用系统的connect().Tcp connect()扫描技术只适用于找出TCP和UDP端口.

    **Udp scan(sU)**。顾名思义,这种扫描技术用来寻找目标主机打开的UDP端口.它不需要发送任何的SYN包，因为这种技术是针对UDP端口的。UDP扫描发送UDP数据包到目标主机，并等待响应,如果返回ICMP不可达的错误消息，说明端口是关闭的，如果得到正确的适当的回应，说明端口是开放的.

    **FINscan(sF)**。有时候TcpSYN扫描不是最佳的扫描模式,因为有防火墙的存在.目标主机有时候可能有IDS和IPS系统的存在,防火墙会阻止掉SYN数据包。发送一个设置了FIN标志的数据包并不需要完成TCP的握手.

## 主机信息

硬件信息/软件信息/固件信息/客户端配置

端口和服务扫描

```
nmap -sV 192.168.32.215     // 端口和服务检测
http://coolaf.com/tool/port // 在线端口检测
msscan
zmap

whatweb -v -a 3 --proxy 192.168.32.1:41081 192.168.32.215   // web指纹检测
python3 dirsearch.py -e * -u "https://so.xxx.com"   // web目录爆破
```

??? note "Nmap 端口检测/指纹检测"
    **版本检测(sV)**。版本检测是用来扫描目标主机和端口上运行的软件的版本.它不同于其它的扫描技术，它不是用来扫描目标主机上开放的端口，不过它需要从开放的端口获取信息来判断软件的版本.使用版本检测扫描之前需要先用TCPSYN扫描开放了哪些端口.

    **Idlescan(sL)**。Idlescan是一种先进的扫描技术，它不是用你真实的主机Ip发送数据包，而是使用另外一个目标网络的主机发送数据包.

系统信息

```
nmap -O 192.168.32.215      // 操作系统信息
```

## 身份信息

证书/邮箱/员工姓名

[天眼查](https://tianyancha.com)搜索高管信息，生成对应的社工字典，可以爆破账号。

## 网络信息

域属性/DNS/网络信任依赖/网络拓扑/IP地址/安全设备

## 组织信息

商业关系/确定物理位置/确定业务节奏/确定角色

业务系统

用友OA/

架构

DMZ 区/办公区/生产区/核心DB

子公司
```
https://www.tianyancha.com/
```

企业状况

```

```

## 钓鱼信息

鱼叉式服务/鱼叉式附件/鱼叉式链接

## 闭源信息

授权的外部敏感数据（外包厂商/供应商/云厂商等）/购买技术数据

## 开源技术数据库

WHOIS/DNS/被动 DNS/数字证书/CDNs/扫描数据库

子域名

```
https://d.chinacycc.com/index.php?m=Login&a=index
https://phpinfo.me/domain/
https://www.t1h2ua.cn/tools/
子域名挖掘机
https://site.ip138.com/baidu.com/domain.htm
```

whois

```
http://tool.chinaz.com/
```

DNS 历史解析

最早的解析很可能是真实 ip

```
https://dnsdb.io/zh-cn/
https://x.threatbook.cn/
https://tools.ipip.net/cdn.php
```

CDN

多地ping确定是否有CDN

*很多时候，主站虽然是用了CDN，但子域名可能没有使用CDN，如果主站和子域名在一个ip段中，那么找到子域名的真实ip也是一种途径。

```
http://ping.chinaz.com/
http://ping.aizhan.com/
```

[绕过 CDN](https://www.cnblogs.com/qiudabai/p/9763739.html)

SSL 证书查询

```
https://www.chinassl.net/ssltools/ssl-checker.html
```

## 开放的网站和域

社交媒体/搜索引擎

## 目标

- 基础信息
  - 企业状况、架构、业务应用、子公司等
- 系统信息
- whois 信息
- 子域名收集
  - 域传送
  - 子域名爆破
  - SSL 证书查询
  - DNS 数据收集
  - whois 反查
  - 网站 JS 代码
  - 旁站查询
  - C 段查询
  - github
  - 搜索引擎
- 应用资产收集
  - 外包商
  - 目录扫描
  - web 指纹
  - 微信公众号、小程序、app
  - 中间件信息
  - 历史漏洞
  - fofa：`domain="baidu.com"`
  - shadon
  - zoomeye
  - Access key
- 社工库
- 端口开放信息
- WAF
- 网络架构

## 用户信息

- 工号
- 姓名
- 邮箱
- 职位
- 供应商
- 合作伙伴

## 边界突破

- OWASP top10
- 登录框
  - 用户枚举
  - 爆破
  - 密码找回
  - 逻辑绕过
  - sql注入
  - 未授权访问
  - 验证码爆破
- 中间件/框架
  - apache
    - 解析漏洞
    - 目录遍历
  - apache shiro 反序列化
    - 