# 代码风格规范

必要规范：

if 用于过滤错误还是用于过滤正确

if都是true

if tr:
    if tr:
        if tr: 
            xxx
        else:
    else:
else:

优化方法：
- 不写 else，写 return

if都是错误

// 函数注释
func a:
    // 错误情况注释
    if er: xxx
    if er: xxx
    if er: xxx
    xxx

优化方法：
- 直接全局异常，再捕获处理