# Anaconda

Anaconda 不影响系统本身的 python 环境，并且结合了 pip 和 virtualenv 的功能。

## 使用

### 包

```
conda list                      列出当前环境的所有包
conda install requests          安装 requests 包
conda remove requests           卸载 requets 包
conda update requests           更新 requests 包
conda remove -n learn --all     删除 learn 环境及下属所有包
```

### 环境

```
conda env list                  列出 conda 管理的所有环境
activate                        切换到 base 环境
activate learn                  切换到 learn 环境
activate root                   切换到 root 环境

conda create [-n env_name] python=3             创建一个名为 learn 的环境
                                                // python 默认为 3 的最新版本
conda create [-n new_name] --clone [old_name]   重命名环境
conda remove -n env_name --all                  删除环境
```

### conda

```
conda update conda              升级 conda
conda update anaconda           升级 anaconda 前要先升级 conda
conda update --all              升级所有包
conda clean -p                  删除没有用的包
conda clean -t                  删除保存下来的压缩文件（.tar）
```

## 配置

### 仓库

```
conda env export > environment.yaml             导出当前环境的包信息
conda env create -f environment.yaml            用配置文件创建新的虚拟环境

conda config --set show_channel_urls yes    显示仓库
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/        添加仓库
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/    删除仓库
```

### 环境变量

Path

```
F:\Anaconda3
F:\Anaconda3\Scripts
F:\Anaconda3\Library\bin
```