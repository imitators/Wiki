# 介绍

这里累计了所有对编程语言的思考。

王垠在概括 Go 语言时，使用的框架如下：

- 语言设计
- 定位和优点
- 语法
- 工具链
- 特性1
- 没有特性2
- ...
- 库代码
- 总结

## 编程语言分类

语言代数：

- 第一代-机器语言
- 第二代-汇编语言
- 第三代-高级程序设计语言: C, C++ , Lisp, C#, Java
- 第四代-特定应用的设计语言: SQL, NOMAD, Postscript
- 第五代-基于逻辑和约束的语言: Prolog, OPS5

冯诺依曼语言：C

强制式和声明式：

- 强制式 (imperative): C, C++, C#, Java
- 声明式 (declarative): ML, Haskell, Prolog

脚本语言：Python, PHP, JavaScript, Ruby, Perl, Tcl, Awk

## Java

### 生成 JRE

打开目录 `C:\Program Files\Java\jdk-11.0.10`，管理员模式打开 cmd，执行如下代码  `bin\jlink.exe --module-path jmods --add-modules java.desktop --output jre`

### 环境变量

系统环境变量修改如下：

`CLASSPATH` 修改为 `.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar`，`Path` 后添加 `;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin`。

最后编写 `C:\Users\xxx\jae.bat`，内容如下：

```bat
echo 8 => Java 8
echo 9 => Java 9
echo 1 => Java 11
echo 5 => Java 15

set /p a=select the version about java:

if "%a%"=="8" (
    setx -m JAVA_HOME "C:\Program Files\Java\jdk-1.8.0_181"
)
if "%a%"=="9" (
    setx -m JAVA_HOME "C:\Program Files\Java\jdk-9.0.4"
)
if "%a%"=="1" (
    setx -m JAVA_HOME "C:\Program Files\Java\jdk-11.0.10"
)
if "%a%"=="5" (
    setx -m JAVA_HOME "C:\Program Files\Java\jdk-15.0.1"
)
```

此时使用管理员权限打开命令行，输入 `jae` 即可修改环境。

## Python

### 环境变量

系统环境变量修改如下：

新建 `pyenv` 值为 `C:\python3.8.6`，`Path` 后添加 `;%envpy%;%envpy%\Scripts`。

最后编写 `C:\Users\xxx\pye.bat`，内容如下：

```bat
echo 2 => python 2.7
echo 6 => python 3.6.6
echo 8 => python 3.8.6

set /p a=select the version about python:

if "%a%"=="2" (
    setx -m envpy "C:\python2.7"
)
if "%a%"=="6" (
    setx -m envpy "C:\python3.6.6"
)
if "%a%"=="8" (
    setx -m envpy "C:\python3.8.6"
)
```

此时使用管理员权限打开命令行，输入 `pye` 即可修改环境。