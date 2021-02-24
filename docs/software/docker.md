# Docker

## 使用

### 镜像

```
* docker images         查看本地已有镜像
docker search [name]    搜索镜像
                        // 详情见 hub.docker.com

* docker pull [name]    拉取镜像
docker build            创建 Dockerfile 镜像

docker rmi [name]       删除镜像
```

### 容器

```
* docker ps                     查看正在运行的容器
docker ps -a                    查看所有容器
docker inspect [容器ID] | grep IPAddress    查看容器ip地址

* docker run [container id]     运行容器
    * docker run -p [主机端口]:[容器端口] -it [容器名]:[标签] /bin/bash
    * docker run -d --name myredis -p 6666:6379 -v d:\DockerRedis\:/data redislabs/rebloom --appendonly yes
        // --name                       为容器命名
        // -i                           以交互模型运行容器
        // -it                          交互模式并指定一个伪终端
        // -d                           后台运行
        // -v                           挂载Win下共享的保存持久化数据的目录
        // --appendonly yes             开启持久化（数据会挂载到-v设定的目录）
        // –restart=always              随docker启动
        // --requirepass "your passwd"  连接密码
docker rm [container id]        删除容器

docker start [container id]     启动容器
docker stop [container id]      停止容器

exit/ctrl+d                     退出容器终端
1.Ctrl+P   2.Ctrl+Q             退出终端
```

### 服务

```
systemctl start docker/service docker start 启动服务
    // CentOS 系统不支持 service 指令
systemctl stop docker/service docker stop   关闭服务
```

### 配置文件

Linux 默认位置是 `/etc/docker/daemon.json`

Windows 默认位置是 `%programdata%\docker\config\daemon.json`