---

title: AWS S3 버킷 Permissions 정책 추가
published: true
comments : true
---


> - 정책 생성 aws policygen

해당 버킷의 모든 파일에 읽기 권한을 주는 것이라면 해당 버킷에 policy http://awspolicygen.s3.amazonaws.com/policygen.html 로 가셔서 Actions에 "GetObject"를 선택하고 ARN에 arn:aws:s3:::yourbucketname/* 을 입력하고 Add Statement 버튼을 누르시면 됩니다.

> - Generate Policy 버튼 누르면
정책 json 파일로 볼수 있는 창이 나타납니다


> - 복사해서 버킷 Permissions 탭에 붙여넣고 Save버튼을 누른다