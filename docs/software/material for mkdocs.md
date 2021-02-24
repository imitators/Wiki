# Material for Mkdocs

## 笔记

> 可嵌套**代码块**、**内容标签**和**分组符号** `* ` 和 `1. `

```
!!! note "111"          // 添加命名
    111

    ``` python          // 添加代码
    def 111:
        print(111)
    ```

    111
```

笔记分类

!!! note

!!! abstract "abstract, summary"

!!! info

!!! tip "tip, hint"

!!! success "success, check"

!!! question "question, help"

!!! warning

!!! fail

!!! error "danger, error"

!!! bug

!!! example

!!! quote

## 内容标签

> 可嵌套**代码块**和**分组符号** `* ` 和 `1. `

```
=== "C"                         // 添加

    ``` c
    #include <stdio.h>

    int main(void) {
      printf("Hello world!\n");
      return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```
```

## 代码块

> 可嵌套分组符号

添加行号，高亮代码

```
 ```python linenum="1" hl_lines="2 3"        // 添加行号，2 到 3 行高亮现实
 def bubble_sort(items):
     for i in range(len(items)):
         for j in range(len(items) - 1 - i):
             if items[j] > items[j + 1]:
                 items[j], items[j + 1] = items[j + 1], items[j]
 ```
```

小代码块标记语言

```
The `#!python range()` function is used to generate a sequence of numbers.
```

The `#!python range()` function is used to generate a sequence of numbers.