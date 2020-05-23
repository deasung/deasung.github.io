---
title: AWS pipeline -> bitbucket cloud 베타용 연동 
published: true
comments : true
---

자세한건 공식문서를 읽는게 제일 좋습니다.
AWS pipeline -> bitbucket cloud 베타용 연동용 [공식문서](https://aws.amazon.com/ko/about-aws/whats-new/2019/12/aws-codepipeline-now-supports-atlassian-bitbucket-cloud/)
링크입니다.

최근에 회사 기존 젠킨스 CI랑 Bitbucket Clound Pipeline으로 되어 있는 부분을 

조금씩 AWS CI로 옮기는중에 적는 내용입니다~!

# 간단한 정리 

## 1.정책을 만들어 줍니다.

![1](/assets/imgs/2020/05/18/1.png)

## 2.정책을 json편집기로 입력해준다.

![2](/assets/imgs/2020/05/18/2.png)

json 파일 내용입니다.

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


## 3.파이프라인 항목으로 이동
Bitbucket 연결 버튼을 클릭해 줍니다.

![3](/assets/imgs/2020/05/18/3.png)


## 4.Bitbucket Cloud랑 연동
창이 나오는데 연동을 해주면 됩니다 

![4](/assets/imgs/2020/05/18/4.png)
