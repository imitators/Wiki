# C 核心概念

## 编译系统

GCC 编译器驱动程序读取源程序文件(.c)后，编译系统 (compilation system) 编译过程如下：

> GCC 是 GNU 项目开发出的众多工具之一
>
> GNU 目标为开发出一个类 UNIX 系统，并且源码能不受限制的修改和传播，目前已经开发了除内核外的众多部件

```
源程序 (.c) -- 预处理器 (cpp) -> 修改后的源程序 (.i) -- 编译器 (ccl) -> 汇编程序 (.s) -- 汇编器 (as) -> 可重定位目标程序 (.o) -- 链接器 (ld) -> 可执行目标程序
```

预处理：根据 hello.c 开头的 `# ...` 修改原始程序（例如 `# include <stdio.h>` 读取系统头文件 stdio.h），输出 hello.i 文件。

编译阶段：将 hello.i 翻译成包含一个**汇编语言程序**的 hello.s 文件。

汇编阶段：将 hello.s 翻译成机器语言指令，并把指令打包成**可重定位目标程序**的格式。

链接阶段：将标准 C 库中被调用的函数（例如 `printf()` 链接 printf.o），输出可执行文件 hello。

## 使用

### 保留关键字

=== "unsigned"

    无符号数

=== "typeof"

    给数据类型命名

    ```
    e.g.

    typedef int *int_pointer;
    int_pointer a;  // a 是一个指向 int 类型数据的指针
    ```

### 常用函数

printf (format string, parameter)

### 指针

声明时的指针类型就是指针指向的数据类型。

数组表示法能引用指针，指针表示法也能引用数组元素。、

& 取地址

### GC

垃圾回收机制 (garbage collector)

