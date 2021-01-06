# 介绍

## 镜像后缀含义

Professional: 专业版

Enterprise: 企业版

Retail version: 零售版本

with Service Package 1 (with SP1): 含有安全更新包1的版本，更新包中包含大量安全补丁

VL Build: 大客户版本，支持 KMS 激活，与零售版没有区别

R2 (Release 2): 第二次发行版，在第一次基础上进行了改进

## 搭建域环境

[Win server 2008 R2 搭建域环境](https://mp.weixin.qq.com/s/zXaTlDg95TE2-VAF4G6myQ)

## DLL

动态链接库 (Dynamic-Link Library) 是 Win 系统中对于共享库概念的实现。

动态链接库有 3 种扩展名：

- .dll
- .ocx (for libraries containing ActiveX controls)
- .drv (for legacy system drivers)

### 调用顺序

动态链接库调用顺序 (Dynamic-Link Library Search Order)

!!!note
    以下部分来自于 [Anaconda 介绍](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#activating-an-environment)

由于动态链接库调用顺序的存在，Windows 对于正确激活非常敏感。

## WSL

Windows Subsystem for Linux