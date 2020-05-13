---

title: NGINX에 ELB 체크 하는 방법 
published: true
comments : true
---

vi /etc/nginx/nginx.conf 로가서 추가를 해줍니다.



```
location /elb-status {
        access_log off;
        return 200 'A-OK!';
        add_header Content-Type text/plain;
    }


```


```
sudo service nginx start

```

# AWS ELB 상태검사

AWS EC2 -> 로드 밸런서 -> 해당 로드밸런서 클릭후 하단탭에 상태검사 클릭 

![AWS ELB 상태검사](/assets/imgs/2018/07/02/aws-nginx-elb-health-check/1.png)

