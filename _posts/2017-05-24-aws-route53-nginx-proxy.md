---

title: AWS Route53 nginx proxy 연동
published: true
comments : true
---


저는 삽질로 AWS Security-Group에서 80포트를 Inbound 안해놔서 안되서

우선 설정으로는

nginx가 설치되었다는 가정하에

디렉토리로 가서cd /etc/nginx/sites-available/ vi 편집기로 default파일을 우선 복사한다음 열면


![](/assets/imgs/2017/05/24/route53-nginx-proxy1_20170524.png)

설정한후 nginx 재시작sudo /etc/init.d/nginx restart