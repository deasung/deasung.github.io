---
title: AWS -> Codebuild 셋팅
tags: [aws, codebuild]
categories: [aws]
published: true
comments : true
---

AWS CodeBuild는 소스 코드를 컴파일하는 단계부터 테스트 실행 후 소프트웨어 패키지를 개발하여 배포하는 단계까지 마칠 수 있는 
완전관리형의 지속적 통합 서비스라고 공홈에서 아주 자세히 잘 나옵니다~

[https://aws.amazon.com/ko/codebuild/](https://aws.amazon.com/ko/codebuild/)

## 1.빌드 프로젝트 구성

딱히 추가구성을 할 필요가 없어서 체크를 안했음;

![](/assets/imgs/2020/05/24/1.png)

## 2.소스

소스는 bitbucket cloud로 연동을 했음.
소스 버전은 develop으로 개발용으로 셋팅중이니 


![](/assets/imgs/2020/05/24/2.png)

## 3.환경

이미지 버전을 standard 2.0 으로 셋팅을 Springboot2 버전 이상을 쓸수 있게 gradle
버전이 제일 맞는게 이거라서 일단은 이걸로 셋팅을~

![](/assets/imgs/2020/05/24/3.png)

서비스 역활은 기존에 셋팅되어 있는게 있으면 기존 역활로 써도 된다.

![](/assets/imgs/2020/05/24/4.png)

![](/assets/imgs/2020/05/24/5.png)

vpc랑 시큐리티 보안그룹도 셋팅 할수 있으니 참고를~

## 4.Buildspec

![](/assets/imgs/2020/05/24/6.png)

buildspec.yml 이름을 그대로 쓸수 있고 
또한 명칭을 바꿀수도 있다.

## 5.아티팩트

![](/assets/imgs/2020/05/24/7.png)

빌드한 결과물을 어디다가 저장할지 셋팅할수도 있음?
일단 s3에다가 저장하게 수정

![](/assets/imgs/2020/05/24/8.png)


## 6.로그

![](/assets/imgs/2020/05/24/9.png)

클라우드 워치랑 연동할수도 있

```
[Container] 2020/05/06 01:52:05 Waiting for agent ping
[Container] 2020/05/06 01:52:08 Waiting for DOWNLOAD_SOURCE
[Container] 2020/05/06 01:52:13 Phase is DOWNLOAD_SOURCE
[Container] 2020/05/06 01:52:13 CODEBUILD_SRC_DIR=/codebuild/output/src034368496/src/bitbucket.org/glowpickeng/admin-java-api
[Container] 2020/05/06 01:52:13 Phase complete: DOWNLOAD_SOURCE State: FAILED
[Container] 2020/05/06 01:52:13 Phase context status code: YAML_FILE_ERROR Message: YAML file does not exist
```

## 7.CodeBuild buildspec.yml 셋팅
https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html


## 8.S3 올리기 IAM → 권한 셋팅
[참고하기에 좋은 블로그 글 IAM관련](https://devhaks.github.io/2019/02/16/code-build/)


## 9.buildspec.yml 셋팅

```
version: 0.2

phases:

  install:
    runtime-versions:
      java: openjdk8

  build:
    commands:
      - echo Build Starting on `date`
      - chmod +x ./gradlew
      - ./gradlew build

#  post_build:
#    commands:
#      - echo $(basename ./build/libs/*.jar)
#      - pwd
  post_build:
    commands:
      - ls -al
      - aws s3 cp --recursive ./build/libs/ s3://#{s3_bucket}

#cache:
#  paths:
#    - '/root/.gradle/caches/**/*'

```


일단은 이렇게 개발쪽은 셋팅했다. 동료들이 편하게 로직에만 
신경쓰면 되는 환경이 되었다~ 더 고도화를 해보자!

