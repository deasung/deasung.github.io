---

title: AWS IAM 역할 활용하기
published: true
comments : true
---


EC2 인스턴스,다른 AWS 계정,Facebook, Google, Amzon.com AWS 리소스에 대한 접근 권한을 설정할수 있음

EC2 인스턴스에서 API로 AWS 리소스에 접근하려면 항상 액세스 키와 시크릿 키를 설정해야만 했음 나중에 Auto Scaling 기능으로 EC2인스턴스를 늘려갈때 엑세스 키와 시크릿 키를 일일히 설정하려면 상당히 귀찮음

이런 부분을 자동화하지 않아도 IAM 역할을 사용하면 EC2 인스턴스 생성 즉시 API로 AWS리소스 접근 가능

- IAM Role 생성하기 
![](/assets/imgs/2017/05/02/iam-role-01-20170502.png)


- IAM Role 선택 
![](/assets/imgs/2017/05/02/iam-role-02-20170502.png)

EC2,S3선택하였음

- IAM Role 이름작성 
![](/assets/imgs/2017/05/02/iam-role-03-20170502.png)


- IAM Role 확인 
![](/assets/imgs/2017/05/02/iam-role-04-20170502.png)
