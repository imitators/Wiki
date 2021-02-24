# 工业控制系统

ICS (Industrial Control System, 工业控制系统) 的作用是控制关键生产设备的运行。

ICS 由几种不同类型的系统组成：

- **PLC** (Programmable Logic Controller, 可编程逻辑控制器)
- **SCADA** (Supervisory Control And Data Acquisition, 数据采集与监视控制系统)
- **DCS** (Distributed Control System, 分布式控制系统)
- **PCS** (Process Control System, 过程控制系统)
- **RTU** (Remote Terminal Unit, 远程终端单元)
- ...

## PLC 编程语言

### LD

ladder diagram (LD, ladder logic, 阶梯逻辑/阶梯图) 是图形化的 PLC 编程语言，和梯形图存在较多联系。

### FBD

function block diagram (功能块图) 是 PLC 编程的主要编程语言之一。

功能块分类如下：

- 标准功能块
    - 位逻辑功能块 (bit logic ...)
    - 双稳态功能块 (bistable ...)
    - 边缘检测 (edge detection)
    - 时间功能块 (timer ...)
    - 计数器功能块 (counter ...)
- 比较功能块
- 搜索功能块
- 自定义功能块