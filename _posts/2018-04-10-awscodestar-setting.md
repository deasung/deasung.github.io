---

title: AWS CodeStar 구축
published: true
comments : true
---


1.CodeStar 프로젝트이름을 적는다

- s3버킷도 비슷한 이름으로 생성되니 중복되어있는게 없는지 생각하고 만든다


![CODESTAR 연동1](/assets/imgs/2018/04/10/awscodestar-setting/awscodestar-setting01.png)



2.프로젝트 세부정보 codestar는 이렇게 된다라는것을 보여주는듯


![CODESTAR 연동2](/assets/imgs/2018/04/10/awscodestar-setting/awscodestar-setting02.png)



3.EC2 키페어 셋팅을 해줘야함

![CODESTAR 연동3](/assets/imgs/2018/04/10/awscodestar-setting/awscodestar-setting03.png)




4.코드 편집용 툴 선택하는듯 난 건너뛰기를 함
![CODESTAR 연동4](/assets/imgs/2018/04/10/awscodestar-setting/awscodestar-setting04.png)




5.CodeCommit 연동용
- 하기전에 AWS IAM 사용자 git https권한을 줘야한다

![CODESTAR 연동5](/assets/imgs/2018/04/10/awscodestar-setting/awscodestar-setting05.png)


![CODESTAR 연동6](/assets/imgs/2018/04/10/awscodestar-setting/awscodestar-setting06.png)

6.AWSCLI 설치 (MAC기준)
- awscli를 설치를 해줘야한다.

```
$ pip install awscli --upgrade --user
$ was -- version 
(command not found나오면 구글링,mac이면 homebrew로 설치로 일단 해결함)

$ brew install awscli
```
- awscli 설정
우선 AWS IAM 로 가서 'NEW User'로 User를 하나 생성하고, Add permissions로 
'AWSCodeCommitFullAccess' 권한을 부여하고,AWS Access Key ID와 Secret Access Key를
잘 적어두었다가 아래에서 처럼 활용

![CODESTAR 연동7](/assets/imgs/2018/04/10/awscodestar-setting/awscodestar-setting07.png)

터미널창에서

```
$ git config --global credential.helper '!aws code commit credential-helper $@'

$ git config --global credential.UseHttpPath true
$ git clone 주소 

```

git clone를 하고 Intellj에서 gradle 방식으로 import를 한후 
pom.xml -> build.gradle로 변환 

```
# 프로젝트 폴더 (pom.xml이 있는곳) 으로 이동
gradle init --type pom
```

![CODESTAR 연동8](/assets/imgs/2018/04/10/awscodestar-setting/awscodestar-setting08.png)


내용이 많아서... 집에가서 마저 적어야지 ㅋㅋ;;
