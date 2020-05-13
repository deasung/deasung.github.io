---
title: MySQL(Maria DB) root 계정 외부접속 허용
tags: [mysql, maria, db]
published: true
comments : true
---


## MySQL(Maria DB) 로 접속 한다.

## use mysql 명령어를 입력한다.

## grant all privileges on *.* to 'root'@'%' identified by '비밀번호'; 입력한다.

- 모든 디비 및 테이블에 root 권한에 INSERT,UPDATE,DELETE 등 권한을 줌


## flush privileges; 입력한다. (참고로 이 명령어는 디비에 부하를 많이준다고 합니다.)
   
## my.cnf 파일 내용중에서 bind-address =127.0.0.1 을 주석(#)처리 하고 저장한다.
```
bind-address = 127.0.0.1 => #bind-address = 127.0.0.1

위치 -> ubuntu -> /etc/mysql/my.cnf
```
     
   
## MySQL을 재시작 한다

```
sudo service mysql restart
```   


2020.05.08 간만에 예전에 썼던 내용들을 보면서 좀더 추가 내용을 적기로 함

요즘에는 클라우드 기반으로 많이써서 직접 mysql 엔진을 건드리지 않지만,
직접 설치해서 운영시에는 저런 설정들이 필요할것이다.