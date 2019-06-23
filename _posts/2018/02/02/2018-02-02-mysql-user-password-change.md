---

title: Mysql 유저 패스워드 변경 
layout: post 
category: devops 
tags: 
  - mysql
---

# Mysql 유저 패스워드 변경 

```
update user set password=password('패스워드') where user='유저명';
```