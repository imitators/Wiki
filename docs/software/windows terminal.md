# Windows Terminal

## 使用

### 快捷键

```
ctrl+shift+1            powershell
ctrl+shift+2            cmd
```

### cmd 设置环境变量

```
set                     查询所有
set key                 查询单个

set key=%key%;value     添加临时
setx key=%key%;value    添加用户
setx key=%key%;value -m 添加用户

set "key" "value"       修改临时
setx "key" "value"      修改用户
setx "key" "value" -m   修改系统

set key=                删除临时
setx key=               删除用户
setx "key" "" -m        删除系统
```

## powershell

### 设置

脚本路径：`C:\Users\[username]\Documents\WindowsPowerShell\a.psl`