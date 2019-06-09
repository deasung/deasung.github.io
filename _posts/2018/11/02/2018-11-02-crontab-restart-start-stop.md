---

title: Crontab 크론탭 시작/중지/재시작
layout: post 
category: devops 
tags: 
  - crontab
---

크론탭 시작
```
service crond start
```


크론탭 중지
```
service crond stop
```



크론탭 재시작
```
service crond restart
```

크론탭 설치여부 확인(피드백이 있다면 설치되어있는거임.)
```
ps -ef | grep cron
```
