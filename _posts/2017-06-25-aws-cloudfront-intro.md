---

title: Amazon CloudFront 콘텐츠 전송 네트워크(CDN)
published: true
---


출처:[https://aws.amazon.com/ko/cloudfront/](https://aws.amazon.com/ko/cloudfront/)

Amazon CloudFront는 CDN 캐싱을 통해 웹 사이트, API, 동영상 콘텐츠 또는 기타 웹 자산의 전송을 가속화하는 글로벌 콘텐츠 전송 네트워크(CDN) 서비스입니다. 다른 Amazon Web Services 제품과 통합하여 사용하면 개발자와 기업이 최소 사용 약정 없이도 콘텐츠를 최종 사용자에게 전송하는 속도를 손쉽게 가속화할 수 있습니다.

### 장점

S3에 존재하는 원본 정적 컨텐츠를 전 세계에 존재하는 50여개의 CloudFront 엣지 로케이션 서버에 캐싱 하므로서 전 세계의 사용자가 동일한 주소로 이미지를 요청하더라도 그 사용자에게 물리적으로 가장 가까운 엣지 로케이션 서버에서 파일을 제공하므로서 컨텐츠 빠르고 안정적으로 서빙 할 수 있도록 해줍니다.

![cloudFront](/assets/imgs/2017/06/25/aws-cloudfront-1-20170525.png)

AWS 콘솔에 가서 Services 클릭하면 하단에 저메뉴가 있습니다. aws-cloudfront-1-20170525

일단 우리는 돈에 민감한 개발자..라서 요금표를 보겠습니다.

주로 저처럼 HTTP요청을 주로할것같아서 일단 온디맨드방식의 요금표 입니다

### 요금표

![cloudFront-요금표](/assets/imgs/2017/06/25/aws-cloudfront-2-20170525.png)

대한민국 기준 HTTP 요청 0.0090 USD 10000개당 요청금액

오늘 2017-05-25일 기준의 환율로 10000건당 10원이라는 소리입니다

![cloudFront-요금표](/assets/imgs/2017/06/25/aws-cloudfront-3-20170525.png)

이정도면.. 누가 악의적으로 HTTP요청하지 않은 이상 마이크로 서비스는 괜찮을것같습니다.

HTTP,HTTPS 요청은 가격이 틀립니다.(HTTPS 요청이 비싼)

기타

만약 파일이 자주 바뀐다면 CloudFront에 어울리지 않습니다.
