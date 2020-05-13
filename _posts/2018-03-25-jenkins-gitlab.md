---

title: Jenkins 설치 & Gitlab 연동
published: true
comments : true
---



# Jenins 설치

### 자바 설치
```
sudo apt-add-repository ppa:webupd8team/java

sudo apt-get update

sudo apt-get install oracle-java8-installer
```

### gradle 설치
```
$ sudo apt-get install gradle
$ gradle -version
```


### Jenkins 설치

패키지 주소를 apt-key에 더한후 젠킨스 다운

```
$ wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
OK

$ echo deb http://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list


$ sudo apt-get update
$ sudo apt-get install jenkins

```

### Jenkins 시작하기

* sudo systemctl start jenkins 젠킨스 시작
* sudo systemctl status jenkins 젠킨스가 제대로 시작되고 있는지 로그 볼수 있는?

``` 
$ sudo systemctl start jenkins
$ sudo systemctl status jenkins
● jenkins.service - LSB: Start Jenkins at boot time
  Loaded: loaded (/etc/init.d/jenkins; bad; vendor preset: enabled)
  Active:active (exited) since Thu 2017-04-20 16:51:13 UTC; 2min 7s ago
    Docs: man:systemd-sysv-generator(8)
    …

```    

Jenkins를 설치할 때 /var/lib/jenkins/secrets/initialAdminPassword 파일의 내용을 빈칸에 입력해야한다.


![Jenkins 설치1](/assets/imgs/2018/03/25/jenkins-gitlab/01.png)

![Jenkins 설치2](/assets/imgs/2018/03/25/jenkins-gitlab/06.png)

![Jenkins 설치3](/assets/imgs/2018/03/25/jenkins-gitlab/02.png)

![Jenkins 설치4](/assets/imgs/2018/03/25/jenkins-gitlab/03.png)

![Jenkins 설치5](/assets/imgs/2018/03/25/jenkins-gitlab/04.png)

![Jenkins 설치6](/assets/imgs/2018/03/25/jenkins-gitlab/05.png)

# GITLAB연동

gitlab에 접속해서 로그인을 한후 셋팅을 클릭하면

![GITLAB 연동1](/assets/imgs/2018/03/25/jenkins-gitlab/15.png)



![GITLAB 연동2](/assets/imgs/2018/03/25/jenkins-gitlab/07.png)
ACCESS TOKEN을 발급을 받아야한다.


![GITLAB 연동3](/assets/imgs/2018/03/25/jenkins-gitlab/08.png)
젠킨스화면에서 Credentials 만들어야 한다


![GITLAB 연동4](/assets/imgs/2018/03/25/jenkins-gitlab/09.png)
현재는 등록되어 있는게 없으므로 만들어야 한다

![GITLAB 연동5](/assets/imgs/2018/03/25/jenkins-gitlab/10.png)
Gitlab 관련 정보를 등록한다 ID/설명은 괜찮지만 토큰값은 실제로 
Gitlab에서 발급받은 토큰값을 입력한다

![GITLAB 연동6](/assets/imgs/2018/03/25/jenkins-gitlab/11.png)
등록되면 이렇게 보임~!

![GITLAB 연동7](/assets/imgs/2018/03/25/jenkins-gitlab/12.png)
젠킨스 새작업을 만들고

![GITLAB 연동8](/assets/imgs/2018/03/25/jenkins-gitlab/13.png)
젠킨스 프로젝트를 Github project의 프로젝트 URL과 설명을 달고

![GITLAB 연동9](/assets/imgs/2018/03/25/jenkins-gitlab/14.png)

하단에 전역으로 설정되어 있는거를 연동하면 이렇게 일단은 연동될것이다

부족하지만 일단은 나도 여러 블로그의 내용을 보고 따라한거를 정리한거라

역시 구글링은 필수다..
