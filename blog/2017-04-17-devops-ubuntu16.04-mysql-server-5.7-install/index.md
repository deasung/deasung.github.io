---
layout: post
title:  "Ubuntu 16.04 MySQL 설치"
subtitle: "Ubuntu 16.04 MySQL 설치"
type: "Seminar"
blog: true
text: true
author: "Deasung Kim"
post-header: false
order: 1
---


# Ubuntu 16.04 MySQL 설치

```
sudo apt install mysql-server-5.7

mysql -u root -p

1) Character Set 변경 (기본적으로 MySQL 캐릭터셋 latin1)

status 언어확인가능

sudo nano /etc/mysql/my.cnf

[mysqld]
collation-server = utf8_general_ci
character-set-server = utf8
skip-character-set-client-handshake

sudo service mysql restart

status  -> utf8로 바뀐지 확인
```

```
2) 원격 접속을 위한 유저 설정

mysql 접속 후



use mysql

INSERT INTO user(host, user, authentication_string, ssl_cipher, x509_issuer, x509_subject)

values ('%', '계정명', password('비밀번호'), '', '', '');


하면 계정이 생성될거고 그 유저에게 권한을 주는 일은


// 모든 권한

grant all privileges on *.* to 계정명@'%' identified by '비밀번호';

// 특정 DB 모든 권한

grant all privileges on DB명.* to 계정명@'%' identified by '비밀번호';


// 특정 권한

grant select, update, insert on *.* to 계정명@'%' identified by '비밀번호';

flush privileges; <- 해야적용됨

```