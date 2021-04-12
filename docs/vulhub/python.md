# python 常见漏洞分析

## 沙箱逃逸

目标：

- os包中的popen, system来getshell
- commends模块中的方法
- subprocess
- 写文件到指定位置

```python
import os
import subprocess
import commands

# python = 2
os.popen('ifconfig')
commands.getoutput('ifconfig')
commands.getstatusoutput('ifconfig')

# python >= 2
os.system('ifconfig')
os.spawn('ifconfig')
subprocess.getstatusoutput('pwd')
subprocess.call(['ifconfig'],shell=True)
subprocess.check_call("exit 1", shell=True)
subprocess.check_output("exit 1", shell=True)
```

### 绕过 import

- import
- \_\_import\_\_
- importlib

### 绕过指定包引入

=== "__import__"
    ```python
    f3ck = __import__("pbzznaqf".decode('rot_13'))
    print f3ck.getoutput('ifconfig')
    ```
=== "importlib"
    ```python
    import importlib
    f3ck = importlib.import_module("pbzznaqf".decode('rot_13')
    print f3ck.getoutput('ifconfig')
    ```

## pickle 反序列化

pickle模块用来对Python对象执行序列化和反序列化。Python的任何对象都可以通过它永久保存到硬盘文件。Pickle实际上是先把Python对象（list、dict、class等）转换为字符流，这个字符流包含反序列化（从字符流构建对象）所需的所有数据。

pickle有两个主要方法：`pickle.dump` 把对象导入到文件，`pickle.load` 从文件中加载对象。

??? note "pickle原理和控制字符"
    Pickle是一种堆栈语言，这意味着pickle指令将数据推入堆栈或从堆栈中弹出数据并以某种方式对其进行操作。要了解典型的泡菜工作原理，我们只需要了解以下六种泡菜说明即可：
    c：接下来的2行内容类似于，os.system、urllib.unquote是module.object的形式。
    (：就是左括号
    t：相当于右扩号
    S：代表本行后面的内容是String，即字符串。
    R：执行紧靠自己左边的一个括号对中的内容，即( 和他t直接的内容。
    .：点号结束pickle。

`pickle.dump` 将用户提供的内容序列化后，配合 `__reduce__` 魔术方法，可以在序列化的同时执行这之中的内容。

payload：

```python
import base64
import pickle

import os

class a(objct):
    class __reduce__(self):
        return (os.spawn())
```