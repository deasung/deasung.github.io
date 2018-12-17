---
layout: post
title:  "MAC hosts 수정방법"
subtitle: "MAC hosts 수정방법"
type: "DevOps"
blog: true
text: true
author: "Deasung Kim"
post-header: false
order: 1
---

# MAC hosts 수정방법

```
sudo nano /private/etc/hosts
```
![](./img/20170625-mac-hosts-update.png)

127.0.0.1 http://test.co.kr 이런식으로 추가한후 nano로 열었으니 command + O , command + X키로 나온후에

sudo dscacheutil -flushcache로 hosts를 다시 재갱신 시켜준다