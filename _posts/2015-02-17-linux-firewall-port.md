---
title: 리눅스(Linux) 포트(port)  열기, 방화벽(firewall)  설정/해제 등 안내 리눅스(Linux)
published: true
comments : true
---


리눅스 port를 열기 위해서는  iptables를 통해서, 포트를 열고 막고를  할 수 있습니다.

아래의 예제 부분만 따라 하시면 해당 port에 대해 모두 열 수 있습니다.
Inbound (외부에서 서버로 들어오는) , Outbound( 서버에서 외부로 나가는 )  모두 port를 열기 위해서는 아래의 iptables로 INPUT, OUPUT 을 해주면 모두 열립니다.
권한은 root에서 해주시기 바랍니다.

```
iptables -I INPUT 1 -p tcp --dport 5900 -j ACCEPT 
iptables -I OUTPUT 1 -p tcp --dport 5900 -j ACCEPT
```

 
예를 들면 ) FTP port 21번을 열고 싶다.
```
iptables -I INPUT 1 -p tcp --dport 21 -j ACCEPT 
iptables -I OUTPUT 1 -p tcp --dport 21 -j ACCEPT 

service iptables save
/etc/init.d/iptables restart
```

확인 

```
/etc/sysconfig/iptables (직접 추가해도 가능.)
```


iptables 방화벽 켜고 /끄기

```
/etc/init.d/iptables save
/etc/init.d/iptables start
/etc/init.d/iptables stop
```
