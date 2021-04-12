# nc

```
connect to somewhere:	nc [-options] hostname port[s] [ports] ... 
listen for inbound:	    nc -l -p port [-options] [hostname] [port]

options:
	-c shell commands	as `-e'; use /bin/sh to exec [dangerous!!]
	-e filename		program to exec after connect [dangerous!!]
    -t			answer TELNET negotiation

```