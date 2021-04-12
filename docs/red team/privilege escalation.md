# 提权

## 滥用提升控制机制

设置 sid/设置 gid/绕过用户账户控制/sudo 和 sudo 缓存/快速提升执行

## 操纵访问令牌

令牌模拟/令牌盗窃/使用令牌创建流程/制作和模拟令牌/父级 PID 欺骗/SID 历史注入

## 引导或登录自启动执行

注册表运行键/启动文件夹/认证包/时间提供者/Winlogon Helper DLL/安全支持提供者/内核模块和扩展/重新打开应用程序/LSASS 驱动程序/快捷方式修改/端口监控/Plist 修改/打印处理器

## 引导或登录初始化脚本

登录脚本（Windows）/登录脚本（Mac）/网络登录脚本/rc.common/启动项

## 创建/修改系统进程

启动代理/系统服务/Windows 服务/启动守护进程

## 修改域策略

组策略修改/域信任修改

## 事件触发执行

更改默认文件关联/屏幕保护/Windows 管理规范事件订阅/.bash_profile 和 .bashrc/trap/LC_LOAD_DYLIB Addition/Netsh Helper DLL/辅助功能/AppCert DLLs/AppInit DLLs/应用 Shim/图像文件执行选项注入/PowerShell 配置文件/Emond/组件对象模型劫持

## 利用特权提升

## 劫持执行流程

服务文件权限不足/可执行安全文件权限不足/服务注册中心权限不足/通过未引用路径进行路径拦截/通过 PATH 环境变量进行路径拦截/通过搜索订单劫持进行路径拦截/DLL 搜索顺序劫持/DLL 侧面加载/LD_PRELOAD/Dylib 劫持/COR_PROFILER

## 进程注入

DLL 注入/便携式 exe 注入/线程执行劫持/异步过程调用/线程本地存储/Ptrace 系统调用/Proc 内存/EWM 注入/process doppelgänging/进程空心化/VDSO 劫持

## 计划任务

at（Windows）/计划任务/at（Linux）/Launchd/Cron/系统计时器

## 有效账号

默认账号/域账号/本地账号/云账号