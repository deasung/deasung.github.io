---

title: AWS CloudFront 와 S3연동
published: true
comments : true
---




aws service 탭에 가셔서 cloundfront 메뉴를 클릭하면

하기전에 우선 S3 버킷을 만들어야 합니다~


- Service 탭에서 S3를 클릭합니다 
![](/assets/imgs/2017/06/25/cloudfront-s3-3-20170526.png)


- Create bucket을 클릭한다 
![](/assets/imgs/2017/06/25/cloudfront-s3-4-20170526.png)


- 버킷이름과 리전과 기존에 만든 버킷정책이 있으면 연동해준다. 저는 기존에 쓰는 버킷에서 정책을 연동하였습니다.

![](/assets/imgs/2017/06/25/cloudfront-s3-5-20170526.png)

서울리젼이 아닌곳에서 버킷을 생성시에는 돈이 더드는것으로 알고있습니다~?!
![](/assets/imgs/2017/06/25/cloudfront-s3-6-20170526.png)

### Versioning
> - S3는 특정 버킷의 객체들에 대하여 버전 관리 기능을 하는 버저닝 기능을 제공함
> - 버저닝 기능을 사용하면 파일을 삭제 후 복원할 수 있고 이전으로 되돌릴 수도 있음
> - 버저닝 되는 객체도 그만큼 S3의 용량을 차지
> - 이게 다 돈입니다~

### Logging 서버[엑세스 로깅](http://docs.aws.amazon.com/ko_kr/AmazonS3/latest/dev/ServerLogs.html)
> - 버킷 액세스 요청을 추적하기 위해 액세스 로깅을 활성화

> - 각 액세스 로그 레코드는 한 액세스 요청에 대한 세부 정보(요청자, 버킷 이름, 요청 시간, 요청 작업, 응답 상태, 오류 코드 등)를 제공

> - 액세스 로그 정보는 보안 및 액세스 감사에 유용할 수 있음

### Logging 참고 

Amazon S3 버킷에 대해 서버 액세스 로깅을 활성화하는 데는 추가 비용이 들지 않지만, 시스템에서 제공하는 로그 파일에 대해서는 일반적인 스토리지 요금이 발생합니다. (로그 파일은 언제든지 삭제할 수 있습니다.) 로그 파일 전송 시 데이터 전송 요금은 발생하지 않지만 다른 데이터 전송과 마찬가지로 전송된 로그 파일에 액세스하는 데는 비용이 부과됩니다.

### [Tags Amazon EC2 리소스에 태그 지정](http://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/Using_Tags.html)

원한다면 고유의 메타데이터를 태그의 형태로 각 리소스에 배정하여 인스턴스, 이미지 및 기타 Amazon EC2 리소스를 쉽게 관리

버킷에 권한을 설정하는 화면입니다. 
![](/assets/imgs/2017/06/25/cloudfront-s3-7-20170526.png)

앞에서 설정한 버킷설정을 확인하는 리뷰창입니다. 
![](/assets/imgs/2017/06/25/cloudfront-s3-8-20170526.png)


버킷이 생성된 화면 
![](/assets/imgs/2017/06/25/cloudfront-s3-9-20170526.png)


## CloudFront S3연동
- 서비스탭에서 CloudFront를 클릭합니다. 
![](/assets/imgs/2017/06/25/cloudfront-s3-1-20170526.png)

- Create Distribution 버튼을 클릭합니다. 
![](/assets/imgs/2017/06/25/cloudfront-s3-2-20170526.png)

- 컨텐츠타입을 선택합니다. 
![](/assets/imgs/2017/06/25/cloudfront-s3-10-20170526.png)

웹 배포 사용하여 HTTP 또는 HTTPS를 통해 다음 콘텐츠를 제공할 수 있습니다.

RTMP Adobe Media Server 및 Adobe Real-Time Messaging Protocol(RTMP)을 사용하여 미디어 파일을 스트리밍합니다. RTMP 배포에서는 Amazon S3 버킷을 오리진을 사용해야합니다(S3 실서버)

실습은 웹 정적리소스파일로 테스트를 합니다. 

![](/assets/imgs/2017/06/25/cloudfront-s3-11-20170526.png)


- Origin Domain Name 
![](/assets/imgs/2017/06/25/cloudfront-s3-12-20170526.png)

S3버킷과 ELB에 목록이 나타납니다. 여기서 커스텀 오리진을 사용하려면 이곳에 오리진 서버의 도메인을 적으면됩니다.

- Origin Path 
버킷 경로를 설정하는거 ex) aws-study-ds/서브버킷폴더 지정안하면 절대경로로 셋팅하는듯

- Origin ID
자동으로 셋팅됩니다 오리진서버를 구별하기 위해

- Restrict Bucket Access 
S3 버킷에 CloudFront만 접근할 수 있도록 설정하는 옵션.

- Origin Custom Headers 
헤더 이름과 값을 지정

Default Cache Behavior Settings 설정 
![](/assets/imgs/2017/06/25/cloudfront-s3-13-20170526.png)

- Viewer Protocal Policy 
CloudFront로 보여질 프로토콜 정책

- Allowed HTTP Methods 
허용하는 HTTP 메소드 종류

- Object Caching 
파일의 캐시 유지 시간을 설정. 유지 시간이 지나면 CloudFront에서 파일 삭제

- Forward Cookies 
오리진의 쿠키를 CloudFront를 거쳐 사용자에게 전달할지 설정. 설정 않으면 캐시 성능 향상

- Forward Query Strings
CloudFront에서 오리진으로 쿼리 문자열을 전달. 오리진에서 쿼리 문자열에 따라 파일을 구분해서 보여주고 싶을 때 설정. 설정 않으면 캐시 성능 향상

- Smooth Streaming
실시간 스트리밍 프로토콜인 Microsoft Smooth Streaming을 사용하고 싶을 때 설정

- Restrict Viewer Access 
signed URL로 CloudFront 사용을 제한하고 싶을 때 설정

- Compress Objects Automatically 
오브젝트 압축 자동화(gzip)

Distribution Settings 설정
![](/assets/imgs/2017/06/25/cloudfront-s3-14-20170526.png)
- Price Class 
요금 수준 실제 서비스에서 필요 없는 부분을 제외할 때 설정

- Alternate Domain Names 
Route 53에서 도메인을 연결하라면 이 부분을 설정

- SSL Certificate
HTTPS 프로토콜을 사용하기 위한 인증서 설정

- Default Root Object 
CloudFront 배포 도메인의 최상위로 접속했을 때 기본적으로 보여줄 파일 이름.

- __Logging __ 
CloudFront 접속 로그 설정

- __ Comment__ 
메모

- Distribution State
배포를 생성한 뒤 배포 상태 설정

생성버튼을 누릅니다.
![](/assets/imgs/2017/06/25/cloudfront-s3-16-20170526.png)

## 생성 요청하였지만 아직 완료되지 않음 ( 소요시간 : 15분 ~ 20분 ) 걸립니다~
![](/assets/imgs/2017/06/25/cloudfront-s3-15-20170526.png)

## S3에 파일을 업로드합니다~
![](/assets/imgs/2017/06/25/cloudfront-s3-17-20170526.png)

## Link URL 주소를 클릭하면 실제 파일 프리뷰가 보입니다.
![](/assets/imgs/2017/06/25/cloudfront-s3-18-20170526.png)

## 실제 파일 이미지 가 보입니다.

http,https로 요청해도됩니다. 
![](/assets/imgs/2017/06/25/cloudfront-s3-19-20170526.png)


## 구글개발자도구로 네트워크에서 보면 현재 cloundfront로 요청이안된상태입니다.

![](/assets/imgs/2017/06/25/cloudfront-s3-20-20170526.png)

## CloudFront 도메인명을 복사한후
![](/assets/imgs/2017/06/25/cloudfront-s3-22-20170526.png)

## 복사한 도메인으로 s3파일링크 앞에 도메인주소를 바꿔주면
![](/assets/imgs/2017/06/25/cloudfront-s3-23-20170526.png)
Response 응답쪽에 X-Cache에 Hit from cloudfront로 나오면 실제 오리진서버에서 캐싱된 클라우드프런트로 땡겨온것입니다. 이렇게 나오면 정상입니다~