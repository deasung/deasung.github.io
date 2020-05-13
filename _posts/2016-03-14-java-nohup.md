---
title: java 서버 프로그램 nohup 백그라운드 실행 및 종료
published: true
comments : true
---

1.cat > 파일명 

2.자바로 만든 서버 파일이 server.jar일때 이 jar를 실행하는 방법은 다음과 같다.
```
java -jar server.jar
```

그러나 이렇게 하면 백그라운드 실행이 안되므로 다음과 같이 start/stop.sh를 만들었다.
[start.sh]
```
nohup java -jar server.jar >/dev/null 2>&1 &
```

[stop.sh]
```
pid=`ps -ef | grep server.jar | grep -v 'grep' | awk '{print $2}'`
kill -9 $pid
```


[java-nohup](http://duongame.blogspot.kr/2015/04/java-nohup.html)

[shell-script](http://linuxforge.tistory.com/35)