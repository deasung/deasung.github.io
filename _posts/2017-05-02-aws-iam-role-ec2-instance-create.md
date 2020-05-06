---

title: Amazon IAM 역할을 사용하는 EC2 인스턴스 생성하기
published: true
---


EC2 인스턴스 전용 IAM 역할은 EC2 인스턴스를 생성할 때 설정해줘야함

> - 인스턴스 생성한다 
![](/assets/imgs/2017/05/02/iam-role-ec2-create-01-20170502.png)


> - Amazon AMI로 생성 
![](/assets/imgs/2017/05/02/iam-role-ec2-create-02-20170502.png)


> - IAM Role에 ExampleEC2Role 선택 
![](/assets/imgs/2017/05/02/iam-role-ec2-create-03-20170502.png)


> - 인스턴스 생성확인 
![](/assets/imgs/2017/05/02/iam-role-ec2-create-04-20170502.png)

> - SSH 접속확인
```
ec2-user -> Aws AMI로 인스턴스생성시에 접속유저명칭

ssh -i ~/.ssh/pem파일명 ec2-user@Public-ip
```
![](/assets/imgs/2017/05/02/iam-role-ec2-create-05-20170502.png)

> - aws s3 ls s3의 파일목록을 버는 명령어
```
aws s3 ls s3://버킷명
```
![](/assets/imgs/2017/05/02/iam-role-ec2-create-06-20170502.png)

> - 버킷명은 나오는데 버킷안에 파일목록이안나온다

```
버킷명 리전알아내는 명령어
aws s3api get-bucket-location --bucket 버킷명

* S3 리전확인
```

>- S3 파일목록 확인
```
aws s3 ls 버킷명 --region 리전명
```

## 정리 

이테스트의 목적은 해당인스턴스의 IAM의 역할에 따른 접근가능한거 수정

EC2 인스턴스를 생성할때 IAM역할을 사용하도록 설정했기 때문에 액세스 키와 시크릿 키를 따로 설정하지 않아도 aws s3 명령이 잘 동작함