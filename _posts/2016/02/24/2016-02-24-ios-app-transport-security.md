---

title: App Transport Security
layout: post 
category: devops
tags: 
  - ios
  - app-transport-security
---

App Transport Security
---------------------------------------------

애플이 iOS9부터는 http를 https로 해야지만 네트워크 연결할 수 있도록 하였습니다.
하지만 예외는 항상 존재하는 법. 특정 도메인에 대해서 http를 허용하거나 아예 http를 허용하도록 해주었습니다.

Apple 문서
https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/index.html

1.특정 도메인 HTTP 허용
다음은 페이스북에서 다음과 같이 info.plist에 추가하라고 한 설정입니다.


```
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSExceptionDomains</key>
    <dict>
        <key></key>
        <dict>
            <key></key>
            <true/>                
            <key></key>
            <false/>
        </dict>
        <key></key>
        <dict>
            <key></key>
            <true/>
            <key></key>
            <false/>
        </dict>
        <key></key>
        <dict>
            <key></key>
            <true/>
            <key></key>
            <false/>
        </dict>
    </dict>
</dict>
```

HTTP 허용

다음은 http를 허용하는 설정입니다.

```
<key></key>
<dict>
  <key></key>
      <true/>
</dict>
```

2.localhost 허용

```
<key>NSAppTransportSecurity</key>
<dict>
   <key>NSExceptionDomains</key>
   <dict>
       <key>localhost</key>
       <dict>
        <key></key>
           <false/>          
           <key></key>
           <true/>
           <key></key>
           <true/>
           <key></key>
           <string>1.0</string>
           <key></key>
           <false/>
       </dict>
   </dict>
</dict>
```

3.Info.plist 에 추가해야함

![1](/assets/imgs/2016/02/24/2016-02-24-ios-app-transport-security.png)