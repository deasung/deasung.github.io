---

title: Mysql 유저 패스워드 변경 
published: true
comments : true
---


```
update user set password=password('패스워드') where user='유저명';
```