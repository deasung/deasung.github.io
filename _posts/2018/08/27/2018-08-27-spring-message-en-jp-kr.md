---

title: SpringBoot 다국어 설정
layout: post 
category: spring 
tags: 
  - spring
  - java
---

SpringBoot 다국어 설정
---------------------------------------------

SpringBoot 다국어 설정

![1](/assets/imgs/2018/08/27/2018-08-27-01.png)

다국어면 국가별로 properties 파일에다가 
동일한코드값의 키로 셋팅해줘야 한다.

예시) messages.properties -> 기본 디폴트 프로퍼티 설정 파일

![2](/assets/imgs/2018/08/27/2018-08-27-02.png)

일본어 properties 설정파일

![3](/assets/imgs/2018/08/27/2018-08-27-03.png)

한글 properties 설정파일 

![4](/assets/imgs/2018/08/27/2018-08-27-04.png)

springboot yml 설정에서 다국어를 위한 설정을 추가해줘야 한다

![5](/assets/imgs/2018/08/27/2018-08-27-05.png)


[국제화 메시지를 하기위한 interface ](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/context/MessageSource.html)

![6](/assets/imgs/2018/08/27/2018-08-27-06.png)

1.MessageSource를 이용해서 한 방법 

![7](/assets/imgs/2018/08/27/2018-08-27-07.png)

2.직접 Util 서비스를 구현해서 이용하는법

![8](/assets/imgs/2018/08/27/2018-08-27-08.png)

3.메시지 클래스 작성

![9](/assets/imgs/2018/08/27/2018-08-27-09.png)

![10](/assets/imgs/2018/08/27/2018-08-27-10.png)

호출 했을시에

일본어 예시

![11](/assets/imgs/2018/08/27/2018-08-27-11.png)

영어 예시

![12](/assets/imgs/2018/08/27/2018-08-27-12.png)

한글 예시

![13](/assets/imgs/2018/08/27/2018-08-27-13.png)