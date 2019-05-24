---

title: SpringSecurity Authentication(인증) 용어만 간단히 정리
layout: post 
category: dev 
tags: 
  - aws
  - route53
---

SpringSecurity Authentication(인증) 용어만 간단히 정리
---------------------------------------------

[출처](http://flyburi.com/584)

- > 인증(Authentication):해당 사용자가 본인이 맞는지를 확인하는 절차

- > 인가(Authorization):인증된 사용자가 요청된 자원에 접근가능한지를 결정하는 절차


## 인증방식 
1) credential 기반 인증 : 사용자명과 비밀번호를 이용한 방식

## 이중 인증(twofactor 인증)
사용자가 입력한 개인 정보를 인증 후, 다른 인증 체계(예: 물리적인 카드)를 이용하여 두가지의 조합으로 인증하는 방식 3) 하드웨어 인증 : 자동차 키와 같은 방식

이중 Spring Security는 credential 기반의 인증을 취합니다. - principal : 아이디 - credential : 비밀번호