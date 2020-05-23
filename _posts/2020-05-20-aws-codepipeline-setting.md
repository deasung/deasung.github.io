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

![](/assets/imgs/2020/05/20/2.png)

- 고급설정 (딱히 건드린건 없음) 다음버튼을 눌러준다.

![](/assets/imgs/2020/05/20/3.png)


## 3.소스 스테이지 추가 
회사에서는 Bitbucket Cloud로 소스 형상 관리를 하므로 이걸로 소스 스테이지 추가 

Bitbucket Cloud는 아직 베타라 aws iam에서 정책을 추가 해야한다.

정책 예시)

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "codestar-connections:CreateConnection",
                "codestar-connections:DeleteConnection",
                "codestar-connections:GetConnection",
                "codestar-connections:ListConnections",
                "codestar-connections:GetInstallationUrl",
                "codestar-connections:GetIndividualAccessToken",
                "codestar-connections:ListInstallationTargets",
                "codestar-connections:StartOAuthHandshake",
                "codestar-connections:UpdateConnectionInstallation",
                "codestar-connections:UseConnection",
                "codestar-connections:PassConnection"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

![](/assets/imgs/2020/05/20/4.png)

## 4.빌드 스테이지 추가 

앞전에 미리 추가해놓은 빌드 공급자 (CodeBuild) 추가 해준다.

딱히 환경변수는 아직은 셋팅은 안하니 일단 다음 버튼을 클릭

![](/assets/imgs/2020/05/20/5.png)

## 5. 배포 스테이지 추가 

배포는 AWS에서 다양한 공급자를 제공해준다.

회사에서는 Elastic Beanstalk으로 셋팅할꺼라 일단은 이걸로 선택


![](/assets/imgs/2020/05/20/6.png)

배포 스테이지도 앞전에 추가 해놓은 Elastic Beanstalk 환경으로 구성한걸로 추가후에 다음 버튼 클릭


![](/assets/imgs/2020/05/20/7.png)

## 6. 검토 단계

앞전에 설정한 것들을 한번더 확인해주는 단계 놓친거 있나 다시 한번 확인을~

![](/assets/imgs/2020/05/20/8.png)

![](/assets/imgs/2020/05/20/9.png)

확인을 다한후에 파이프라인 생성 버튼을 클릭해준다.

## 7.생성하자마자 한번 돌아가는중

![](/assets/imgs/2020/05/20/10.png)

파이프라인이 제대로 돌았는지 확인~ 

![](/assets/imgs/2020/05/20/11.png)

이로써 개발서버용 한셋 구성이 마무리 운영은 좀더 복잡할수도 있지만 운영도 나중에 정리를 해야겠다.

열심히 로직에만 신경쓰면 된다. 나머진 알아서 ~ 코드 반영 및 배포가 되므로~