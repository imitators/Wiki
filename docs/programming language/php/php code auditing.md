## 变量覆盖

**未初始化**的变量**能被用户控制**时，容易产生安全问题。

```
register_globals=ON;
```

`register_globals=ON` 时能和 HTML 表单一样注入变量，因此代码中**不需要初始化变量**。

`register_globals` 指令 (directive) 容易遭到滥用，因此在 PHP5.3 被淘汰，在 PHP5.4 被删除。

## 伪协议

伪协议本质是程序员留下的快捷入口，方便访问和调用。

### PHAR



## PDO

