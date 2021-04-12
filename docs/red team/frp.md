# frp

??? note "简介"
    frp 是一个可用于内网穿透的高性能的反向代理应用，支持 tcp, udp 协议，为 http 和 https 应用协议提供了额外的能力，且尝试性支持了点对点穿透
    跨平台支持linux，win，mac
    类似于ngrok，运维、开发人员经常使用它管理内网机器和调试程序，例如将内网的22，3389转发到公网，开发人员将本地web服务转发到公网调试，msf/rat远控的内网上线，可以代替前几年流行的”内网通”服务
    优点：不需要免杀，支持加密传输

## **frps**

启动 frps

```
./frps -c frps.ini	#启用服务端frp
```

frps.ini 设置

```shell
bind_port 	#客户端连接的端口
token 		#密码（尽量复杂点）
```

## **frpc**

启动 frpc
```
systemctl daemon-reload
systemctl start frps
```

设置为开机启动

```
systemctl enable frps
```

设置

```
server_addr = 102.224.185.237 #VPS服务器的IP
server_port = 7000 #服务端服务器设置frps.ini中的端口
token = 123123 #服务端服务器设置frps.ini中的密码

[web] #服务器名（可以填写ssh、ftp等）
type = tcp #连接协议类型
local_ip = 127.0.0.1 #访问的ip可以是内网任何一个ip！
local_port = 80 #本地端口（根据协议修改）
remote_port = 6001 #远程服务器的ip端口
```