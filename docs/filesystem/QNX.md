# QNX

QNX 是 Linux 支持的众多文件系统中的一种。

## QNX4

QNX4 文件系统的磁盘结构由以下部分组成：

- loader block
- root block
- bitmap
- root directory
- other directory, files, free blocks, etc.

### magic number

QNX4 文件系统的幻数(magic number)是开头的 `EB109000`。

### Loader block

Loader block 中为加载代码。

加载代码被 BIOS 加载后，再从分区中加载操作系统。

### Root block

Root block 包含以下目录：

```
|- /(文件系统的根目录)
|- /.inodes
|- /.boot
|- /.altboot
```

`./boot` 和 `./altboot` 包含使用 QNX 引导加载程序(QNX bootstrap loader)加载的操作系统镜像。

### Bitmap

分配空间时，QNX 使用存储在 `./bitmap` 文件夹中的位图 (bitmap)。

文件中的 bitmap 存储着所有块是否使用的信息。

文件中用一个 bit 表示一个块是否使用，当值为 `1` 时，这个块就在使用中。

### Root directory

Root directory 就是根目录，没啥好说的。

## QNX6

QNX6 是 QNX4 的下一代版本。

### magic number

QNX4 文件系统的幻数(magic number)是开头的 `EB109000`。