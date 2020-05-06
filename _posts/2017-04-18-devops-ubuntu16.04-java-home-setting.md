---
title: Ubuntu 16.04 $JAVA_HOME 설정
published: true
---


자바가 설치되었다는 과정하에

```
sudo vi /etc/profile

export JAVA_HOME="/usr/lib/jvm/java-8-oracle"

source /etc/profile

$JAVA_HOME
```
-> bash: /usr/lib/jvm/java-8-oracle 디렉토리입니다 나오면 성공
