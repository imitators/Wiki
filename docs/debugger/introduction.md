# 调试

## 调试目标

### 硬件

1. visual studio 调试bochs，以理解cpu，总线，内存，硬盘，以及其他io设备。

2. visualgdb 调试qemu 以理解android手机平台的cpu，内存，固件，和其他硬件设备。

jtag纯硬件调试器不是谁都玩的起的。

### 操作系统

1. windows上，windbg调试wrk1.2，翻泄漏的win2k，nt4代码，源码调试reactos以理解窗口系统，ida/gdb调试vmware的gdbstub接口，以理解内核异常分发（适用于win，linux，mac），SysinternalsSuite监控系统，这方面工具很多。书籍也很多。

2. linux上，visualgdb远程调试内核还是命令程序都是受到良好支持的，是理解内核中的关键机制很给力的工具。linux从内核到命令任何开源c/c++，你基本都能编译调试版。命令行版如gdb，lldb其实并不适合调试源码，因为导航太差。另外linux上很多工具对了解系统非常有用，建议看《linux内核精髓》

3. android上，aosp代码是开源的，但是代码的native部分没有直接受官方支持的调试手段。visualgdb很接近这个目标，在深入配置之后，native代码是可调的。对于framework部分，android studio 是可做到的，只是配置比较麻烦。在深入配置之后，你基本上可以源码调试init，zygote，framework，以及其他感兴趣的组件。对于android内核可以用qemu的gdbstub接口来配置。调试真机内核是个大坑，还是别想了。

### 工具链

必须先了解编译原理，链接，建议书籍《程序员的自我修养-链接装载与库》

1. windows上，visual studio背后的编译驱动器，链接器，由于不开源，所以建议调试gcc，clang，他们支持交叉编译windows目标。

2. linux上，工具链你可以在visualgdb上配置，远程调试gcc，gdb，去搞清感兴趣的部分实现细节。

3. android上，工具链是交叉编译的clang，lldb，运行于linux之上，也可以用visualgdb。

### 工具方面

指的是SysinternalsSuite，apimonitor，windbg，od，ida，x64dbg，wireshark，unicorn，panda等专门的逆向工具，有源码的调源码，没源码的看文档教程。对于调试模型底层原理建议看《软件调试》

### 底层软件

bios，uefi，grub，uboot，bootloader，要么jtag，要么模拟器（qemu，bochs，vmware）加上visualgdb，或者ida

进程创建，可执行文件加载器（重定位，动态链接），异常处理过程：

建议找代码研读，最好是调试，**异常处理**是难以调试的，因为它**是建立调试的基础机制**，调试它会造成混乱，一个有效的策略是用系统级模拟器做调试，如qemu，bochs，或vmware。