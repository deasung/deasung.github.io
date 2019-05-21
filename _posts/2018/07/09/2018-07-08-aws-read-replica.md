---

title: AWS read replica 생성
layout: post
category: aws
tags:
- aws
---

AWS read replica 생성
---------------------------------------------


# AWS read replica
이렇게 한 이유는 디비 이중화를 하기위해서 이렇게 했다
read replica 옵션은 AWS RDS Aurora만 되는 걸로 알고 있지만 자세한건 공식 문서로
https://aws.amazon.com/ko/rds/details/read-replicas/


### 1.디비 클릭한후 인스턴스 작업을 클릭후에 리전 간 읽기 전용 복제본 만들기 클릭

![AWS_read_replica_1](/assets/imgs/2018/07/09/aws-read-replica/aws-read-replica-01.png)

![AWS_read_replica_2](/assets/imgs/2018/07/09/aws-read-replica/aws-read-replica-02.png)

![AWS_read_replica_3](/assets/imgs/2018/07/09/aws-read-replica/aws-read-replica-03.png)


### 2.복제본 생성버튼 클릭

![AWS_read_replica_4](/assets/imgs/2018/07/09/aws-read-replica/aws-read-replica-04.png)

마무리를~

여기에서 더붙이면 Route53에 디비 퍼블릭엑세스 주소를 연결해놓으면 나름 2차도메인으로 써서
더욱 관리하기가 쉽다

추후에 개발했을때 문제는
쓰기 디비에서 insert,update,delete후에 바로 읽기디비에서는 잘갱신이 안되는듯한 바로 먼가
설정이 있는데 찾으면 다시 포스팅을 하겠다~
