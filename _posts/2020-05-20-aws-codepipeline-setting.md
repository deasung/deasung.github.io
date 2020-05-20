---
title: AWS -> CodePipeline 셋팅
tags: [aws, codepipeline, codebuild]
categories: [aws]
published: true
comments : true
---

# CodePipeline
> AWS CodePipeline은 소프트웨어 릴리스에 필요한 단계를 모델링, 시각화 및 자동화하는 데 사용할 수 있는 지속적 전달 서비스입니다. 소프트웨어 릴리스 프로세스를 구성하는 여러 단계를 신속하게 모델링하고 구성할 수 있습니다. CodePipeline은 소프트웨어 변경 내용을 지속적으로 릴리스하는 데 필요한 단계를 자동화합니다 (https://docs.aws.amazon.com/ko_kr/codepipeline/latest/userguide/welcome.html)


셋팅 하게된 이유 회사에서 젠킨스로 구성되어 있는 부분을 조금씩 아마존 인프라쪽에서 관리하기 위해 
 
차근차근 정리하면서 옮기는 중..

이건 셋팅하면서 정리한 내용일뿐입니다.

## 1.파이프라인 생성
![](/assets/imgs/2020/05/20/1.png)


## 2.파이프라인 설정
- 파이프라인 이름을 적어준다.
