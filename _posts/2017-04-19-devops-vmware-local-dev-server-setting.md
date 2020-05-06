---
title: VMWARE 이용해서 로컬 개발서버구축
published: true
---


## 우분투,JAVA,TOMCAT8,Mysql 설치 & 설정

우분투(14.04 LTS) 설치

- [http://www.ubuntu.com/](http://www.ubuntu.com/)
- [http://www.ubuntu.com/download/desktop](http://www.ubuntu.com/download/desktop)

위에 사이트에가서 이미지를 받으면 됩니다.

JAVA8(OpenJDK8) 설치 터미널명령어

```
터미널명령어
sudo add-apt-repository ppa:openjdk-r/ppa

sudo apt-get update

sudo apt-get install openjdk-8-jdk

sudo update-alternatives --config java

sudo update-alternatives --config javac

java -version
```

## TOMCAT8 설치

apt-get install방식으로 설치 tomcat8 설치하려면

/etc/apt/source.list

해당하는 패키지 추가해준다. 하단에 맨마지막에 추가함

deb http://us.archive.ubuntu.com/ubuntu vivid main universe

apt-get update

apt로 설치시에 tomcat webapps경로

/var/lib/tomcat8/webapps

## Mysql Install 설치

- Mysql 한글설정


![](/assets/imgs/2017/04/19/201704190112.png)

잘변경되었는지 확인status show variables like ‘c%’;