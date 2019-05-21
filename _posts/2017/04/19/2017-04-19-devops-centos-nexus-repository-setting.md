---

title: Nexus sonatype 개발환경 설정 원격배포
layout: post 
category: devops 
tags: 
  - devops
  - centos
  - maven
  - sonatype
---

Nexus sonatype 개발환경 설정 원격배포
---------------------------------------------

## Nexus,sonatype,remote 배포

개발 테스팅 환경 테스트 서버 VM : - OS: CentOS 5.11 - Nexus 설치 OSS 2

로컬 개발환경 - OS : MacOS Sierra - Develop Tools : IntellJ

참고 http://lahuman.jabsiri.co.kr/80 여기에보면 Repository추가 , 권한 , 유저생성 나와있음

![](/assets/imgs/2017/04/19/201704191254.png)

- 테스트 Repository로는 기본인 release,snapshots 으로 우선 테스트
참고로 나는 개발툴 인텔리J 

![](/assets/imgs/2017/04/19/201704191255.png)


- 프로젝트 우클릭 -> Maven -> Open 'settings.xml' 클릭
![](/assets/imgs/2017/04/19/201704191256.png)

- settings.xml에서 기본 nexus admin 계정으로 셋팅해준다.
![](/assets/imgs/2017/04/19/201704191257.png)


- pom.xml로 가서
![](/assets/imgs/2017/04/19/201704191258.png)

태그중 version에 "-SNAPSHOT"이라고 하면 snapshot repository로 배포 빼면 release repository로 배포가됨

snapshot은 같은 버전으로 여러번 배포가 가능 ( 개발시 자주 바뀌므로 사용함 ) release는 같은 버전으로 한번 밖에 배포할수 없음 (다시 배포하려면 서버에서 지우고 배포해야함)

배포용 maven build 
![](/assets/imgs/2017/04/19/201704191257_2.png)

스크립트 작성한걸로 실행시켜서 이상없으면 
![](/assets/imgs/2017/04/19/201704191258_2.png)

원격지 레파지토리에 배포 성공이면서 nexus Shapshots 레파지토리에 배포성공
![](/assets/imgs/2017/04/19/201704191259.png)
