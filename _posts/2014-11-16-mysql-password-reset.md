---
title: 분실한 mysql root password 재설정하기 (Ubuntu 12.04 기준)
tags: [mysql]
published: true
comments : true
---


# Mysql을 처음 설치할 때 database root 계정으로 사용할 password를 설정한다. 하지만 시간이 오래 지나서 그때 설정한 password를 기억할 수 없다면 다음의 방법으로 재설정할 수 있다. (Ubuntu 12.04 기준)

## Step 1. 실행중인 mysql service를 중지 시킨다.

```
# service mysql stop
```

## Step 2. Password를 검사하지 않도록 mysql 환경설정 파일을 수정한다.
: /etc/mysql/my.conf file에 skip-grant-tables를 추가하면 password를 검사하지 않는다.

```
[mysqld]
#
# * Basic Settings
#
user         = mysql
pid-file     = /var/run/mysqld/mysqld.pid
socket       = /var/run/mysqld/mysqld.sock
port         = 3306
basedir      = /usr
datadir      = /var/lib/mysql
tmpdir       = /tmp
lc-messages-dir = /usr/share/mysql

skip-external-locking

skip-grant-tables
```

## Step 3. 새로운 설정 값으로 mysql service를 실행한다.

```
# sudo service mysql start
```

## Step 4. root 계정으로 mysql database를 연다.

```
$ mysql -uroot mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 37
Server version: 5.5.29-0ubuntu0.12.04.1 (Ubuntu)

Copyright (c) 2000, 2012, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

## Step 5. root password를 재설정한다.

```
mysql> UPDATE user SET password=PASSWORD('ROOT_비밀번호') WHERE user='root';
Query OK, 4 rows affected (0.00 sec)
Rows matched: 4  Changed: 4  Warnings: 0
```

## Step 6. my.conf를 복원하고 mysql service를 재실행 시킨다. 