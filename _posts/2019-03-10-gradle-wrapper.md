---

title: 그레이들 래퍼
published: true
comments : true
---


## 그레이들 래퍼 설정방법

그레이들 설정 관련 기본 구조

![GRADLE-WRAPPER1](/assets/imgs/2019/03/10/2019-03-10-gradle-wrapper-01.jpeg)

## 설정 파일 용도 

- gradlew : 리눅스 및 맥 OS용 셀 스크립트

- gradlew.bat : 윈도우용 배치 스크립트 

- gradle/wrapper/gradle-wrapper.jar : Wrapper JAR

- gradle/wrapper/gradle-wrapper.properties : 그레이들 설정 정보 프로퍼티 파일(버전 정보)


## 그레이들 버전 올리는 방법 

```
$./gradle wrapper --gradle-version 4.8.1
```

![GRADLE-WRAPPER2](/assets/imgs/2019/03/10/2019-03-10-gradle-wrapper-02.jpeg)


