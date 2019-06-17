
---

title: MySQL(Maria DB) root 계정 외부접속 허용
layout: post 
category: devops
tags: 
  - mysql
---

MySQL(Maria DB) root 계정 외부접속 허용
---------------------------------------------

1. MySQL(Maria DB) 로 접속 한다.

2. use mysql 명령어를 입력한다.

3. grant all privileges on *.* to 'root'@'%' identified by '비밀번호'; 입력한다.

4. flush privileges; 입력한다.


5. my.cnf 파일 내용중에서 bind-address =127.0.0.1 을 주석(#)처리 하고 저장한다.
     bind-address = 127.0.0.1 => #bind-address = 127.0.0.1
   위치 -> ubuntu -> /etc/mysql/my.cnf
   
   
6. MySQL을 재시작 한다

```
sudo service mysql restart
```   