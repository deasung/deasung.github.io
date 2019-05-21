---

title: Centos 5.11 Jenkis 설치
layout: post 
category: devops 
tags: 
  - devops
  - centos
  - jenkis
---

Centos 5.11 Jenkis 설치
---------------------------------------------

설치명령어

```
$ wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
$ sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
$ sudo apt-get update && sudo apt-get install jenkins
```

설치하고 나면 비밀번호 재설정해야함cd /var/lib/jenkins/secrets/ vi initialAdminPassword


![](/assets/imgs/2017/04/18/201704180117.png)
