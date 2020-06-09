---
title: AWS -> Elastic Beanstalk Amazon Linux 2 platforms nginx 설정
tags: [aws]
categories: [aws]
published: true
comments : true
---

elastic beanstalk 로 셋팅해서 잘쓰다가 프록시 서버에서 413 에러가 떨어져서 nginx 설정점 바꿔야겠다 해서 

문서보고 따라했는데.. 하루종일 삽질쓰!!


# 하나하나 삽질한거를 적어본다.

```
files:
  "/var/proxy/staging/nginx/conf.d/01_proxy.conf":
    mode: "000644"
    owner: root
    group: root
    content: |
      client_max_body_size 20M;

container_commands:
  01_reload_nginx:
    command: sudo service nginx reload

```

하도 안되서 빈스톡으로 구성되어 있는 서버에 직접 터미널로 들어가서 

```
$ > cd /var/log 
```

![](/assets/imgs/2020/06/09/1.png)

빈스톡 서버 구성이 바뀌지 않는한 eb-engine.log는 계속 쌓여 있을거다 로그파일을 보니 

```
[WARN] skipping nginx folder under .ebextensions 
```

먼가 설정정보가 스킵되는 듯한 느낌 구글링 해보니 스택오브 플로우에 은혜로운 님께서 남긴 댓글을 봄 

일단 구글링한 링크는 공유

[https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/platforms-linux-extend.html](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/platforms-linux-extend.html) 

[https://stackoverflow.com/questions/61580965/beanstalk-deployment-ignores-my-nginx-configuration-files-in-ebextensions](https://stackoverflow.com/questions/61580965/beanstalk-deployment-ignores-my-nginx-configuration-files-in-ebextensions)


![](/assets/imgs/2020/06/09/2.png)

.platform 폴더 구성해서 nginx 설정 넣어주고 하면 되는것 같다.

이 구조는 Amazon Linux AMI platform versions (preceding Amazon Linux 2). 기준인거 같다.

![](/assets/imgs/2020/06/09/3.png)

.platform/nginx/nginx.conf

→ client_max_body_size 이거 추가하기위해 엄청난 삽집을 했다.

```
#Elastic Beanstalk Nginx Configuration File

user                    nginx;
error_log               /var/log/nginx/error.log warn;
pid                     /var/run/nginx.pid;
worker_processes        auto;
worker_rlimit_nofile    65252;

events {
  worker_connections  1024;
}

http {
  include       /etc/nginx/mime.types;
  default_type  application/octet-stream;

  log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
  '$status $body_bytes_sent "$http_referer" '
  '"$http_user_agent" "$http_x_forwarded_for"';

  include       conf.d/*.conf;

  # Set client upload size - 100Mbyte
  client_max_body_size 100M; 


  map $http_upgrade $connection_upgrade {
    default     "upgrade";
  }

  server {
    listen        80 default_server;
    access_log    /var/log/nginx/access.log main;

    client_header_timeout 60;
    client_body_timeout   60;
    keepalive_timeout     60;
    gzip                  off;
    gzip_comp_level       4;
    gzip_types text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript;

    # Include the Elastic Beanstalk generated locations
    include conf.d/elasticbeanstalk/*.conf;
  }
}
```


[중요] 여기서 보니 빌드파일 명령어 실행후 프록시 구성파일을 덮어쓰는것 같다 단 .platform/nginx/* 하위정보로 

만약에 내가 구성한 아티팩트에 저 구성이 없으면 기본구성으로 덮어쓰는 현상같음

![](/assets/imgs/2020/06/09/4.png)

그래도 도움을 주신 팀장님께 감사를 그리고 역시 문서를 잘봐야한다.. 요즘은 검색하면 기술블로그만 봐서 

앞으로 공식 문서를 더욱 잘보자 ㅠ