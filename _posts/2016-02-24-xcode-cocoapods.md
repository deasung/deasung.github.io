---
title: xcode cocoapods 사용법
published: true
---


Cocoapods 는 OS X 혹은 iOS 앱을 개발할때 사용되는 라이브러리 관리를 도와주는 Android 의 Maven 같은 도구

CocoaPods 를 사용하기 위해서는 Ruby gem 이 필요함. 맥에는 Ruby가 내장되어있지만 rbenv를 설치하여 ruby 버전과 gem을 관리함

- 1.설치
```
sudo gem install cocoapods
```

- 2.설치한 후 해당 프로젝트 가서 pod init

- 3.Podfile을 열어서(편집기가 가능할걸로)

![1](/assets/imgs/2016/02/24/2016-02-24-xcode-cocoapods-1.png)


사용할 오픈라이브러리를 추가해준다


![2](/assets/imgs/2016/02/24/2016-02-24-xcode-cocoapods-2.png)


- 4.pod install을 한다

- 5.xcworkspace를 클릭해서 연다.

![3](/assets/imgs/2016/02/24/2016-02-24-xcode-cocoapods-3.png)

- 6. 추가한 라이브러리를 연결해준다.

![4](/assets/imgs/2016/02/24/2016-02-24-xcode-cocoapods-4.png)