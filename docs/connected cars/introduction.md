# 车联网

传感器，算法，数据，协议，硬件，无线电

## 用户端系统

### T-BOX 系统

远程信息处理器 (Telematics BOX, 汽车T-BOX) 作为车内外信息交互的纽带，其主要功能是为汽车提供网络连接，大多用于实现各类远程功能。

T-BOX 集成了 OBD、MCU/CPU、FLASH、SENSOR、GPS、3G/4G、WiFi/蓝牙等模块。

T-BOX 对内与车载 CAN 总线相连，实现指令和信息的传递；对外通过云平台与手机/PC 端实现互联。

### CAN

CAN (Controller Area Network, 控制器局域网) 是一种能够实现分布式实时控制的串行通信网络。

CAN 和多个 ECU 相连。

CAN 具有如下优秀特点：
- 传输速度最高到 1Mbps
- 通信距离最远到 10km
- 无损位仲裁机制
- 多主结构

#### CANBus

国际上应用广泛的现场总线之一，由德国 BOSCH 开发，最终成为国际标准 ISO11898。

CANBus 是连接现场设备、面向广播的串行总线系统，最初用于汽车工业，后来也应用于工控领域。

### OTA

OTA (over the air) 是一项基于短消息机制的远程更新技术。

OTA 终端使用无线或蜂窝网络的接口来实现本地数据的更新。

OTA 分为两种：
- SOTA (software over the air)
- FOTA (firmware over the air)

SOTA 多用于应用程序，FOTA 多用于汽车硬件固件更新。

### IVI/ICE

IVI (In-Vehicle Infotainment, In-car Entertainment, 车载信息娱乐系统) 是车主可以直观接触到的部分，车内中控屏，音响，空调，甚至仪表盘都可以连接到IVI中。

IVI 专注于提供前端功能，而指令的上传下行更多交到 Tbox 处理。

### ECU

ECU (Electronic Control Unit, 电子控制单元) 负责控制汽车驾驶状态和实现各种功能。

ECU 负责采集传感器和总线的数据，并判断车辆状态和驾驶员企图，最终通过执行器控制汽车。

常见 ECU:
- EMS (发动机管理系统)
- TCU (变速箱控制单元)
- EPS (电动助力转向系统)
- ESC (车身稳定控制)
- MRC (主动悬挂控制)
- ...

## 云端系统

## 路端系统

