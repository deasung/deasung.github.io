---

title: 4월 GDG 정기모임
layout: post 
category: seminar 
tags: 
  - gdg
  - seminar
---

4월 GDG 정기모임
---------------------------------------------

## 2017.04.15 토요일 4월 정기모임

장소는 부천 만화박물관2층 

![](/assets/imgs/2017/04/16/KakaoTalk_20170416_221022429.jpg)

![](/assets/imgs/2017/04/16/KakaoTalk_20170416_221018933.jpg)

이사진은 Go로 RESTFUL API설계하신분 강연내용 

![](/assets/imgs/2017/04/16/KakaoTalk_20170416_221018268.jpg)

이사진은 ES6로 현재 잘쓰고 있는지 물어보시면서 차이점을 친절하게 알려주신분 

![](/assets/imgs/2017/04/16/KakaoTalk_20170416_221017489.jpg)

## 1.세션 웹개발자가 데스크톱 애플리케이션 만들기
[세션발표자 github주소](https://github.com/cionman)

[Electron](https://electron.atom.io/)
![](/assets/imgs/2017/04/16/electron_img_2017_04_16.png)
Electron으로 만든 프로그램이 슬랙도 있고 , Atom 에디터도 있다고함

비쥬얼스튜디오코드 로 디버깅할려면 electron 개발자 디버깅옵션을 주석처리하고 해야된다고함

JQuery include하고 하면 에러가뜬다고함 $ 객체 찾을수 없다고 에러가남

실제로 디버깅할때 방식이 공식홈페이지에서는

Require 방식 (이것을 추천하심) Node-integration 사용 안함 -> 화면단에서 노드모듈을 사용하는데 제약이 있다고함

## 2.GO로 RESTFUL API만들기

내가 Go를 안써봐서 이건 잘모르겠지만 상당히 간단하다? 소규모 서비스를 만들때 좋을것같다. 스프링부트도 간단하긴한데 더빨리만들것같다 공부를 해봐야겠다

app.go -> 앱실행 메서드 포함,핸들러 설정포함,패키지선언

automigrate -> foreignkey 를 안만들어지는 버그가 있다고함

DB 마이그레이션할때 여타 다른 프레임워크 스프링에서는 properties옵션에서 테이블을 지우고 계속 생성하면서 개발을할수있는지여부?

## 3.ES6 잘쓰고 계시죠?

[BABEL](https://babeljs.io/) ES6에 기능을 기존 브라우저에서 쓸수 있도록 트랜스 컴파일을 해주는 거라고 함. 예전에도 한번써봤음

for of 내용 루프에서 값을 뽑아낼때 주로 쓴다~for (variable of iterable) { statement }

예제``` //Iterating over an Array

let iterable = [10, 20, 30];

for (let value of iterable) { value += 1; console.log(value); } // 11 // 21 // 31

let iterable = [10, 20, 30];

for (const value of iterable) { console.log(value); } // 10 // 20 // 30

//Iterating over a String let iterable = 'boo';

for (let value of iterable) { console.log(value); } // "b" // "o" // "o"

//Iterating over a TypedArray let iterable = new Uint8Array([0x00, 0xff]);

for (let value of iterable) { console.log(value); } // 0 // 255

//Iterating over a Map let iterable = new Map([['a', 1], ['b', 2], ['c', 3]]);

for (let entry of iterable) { console.log(entry); } // ['a', 1] // ['b', 2] // ['c', 3]

for (let [key, value] of iterable) { console.log(value); } // 1 // 2 // 3

//Iterating over a Set let iterable = new Set([1, 1, 2, 2, 3, 3]);

for (let value of iterable) { console.log(value); } // 1 // 2 // 3


**JavaScript function default parameters 설정방법**
function log ( str = ‘(empty)’) -> 함수인자에 디폴트값을 셋팅할수 있음
```
/* ECMAScript 6에 포함된 Default Function Parameters */
function multiply(a, b = 1) {
  return a * b;
}

multiply(5); // 5
```

**Rest Operator** 나머지 매개변수(rest parameter) 구문은 정해지지 않은 수 인수를 배열로 나타낼수 있다.

```
function(a, b, ...theArgs) {
  // ...
}
```

```
//예제

function fun1(...theArgs) {
  console.log(theArgs.length);
}

fun1();  // 0
fun1(5); // 1
fun1(5, 6, 7); // 3

```
클래스 
- > 1.기존 prototype 비슷함 
- > 2.클래스 set,get , 메소드도 생김 
- > 3.Static Function 유틸성 클래스 쓸만할 듯   

- > 4.스태틱함수는 new로 인스턴스하면서 없어진다고함 

- > 5.변수,클래스 상관없이 export 
- > 6.Import는 별칭을 쓸수 있음 
- > 7.Promise - 비동기 작업을 동기처럼 실행 쓰는 목적은 가독성 향상 콜백지옥 해결X - Promise.resolve new Promise() Promise.resolve(), Promise.reject()와 다름

- Async & Await Await : 현재 구문을 멈추고 다른 Promise를 실행, 그 Promise 완료되면 다시 진행


[MDN](https://developer.mozilla.org/ko/)
[TypeScript](https://www.typescriptlang.org/)
타입스크립트 = 제너릭지원

## 라이트닝 토크
1.[아이로보](https://irobo.co.kr/) 금융관련 회사인거같은데 머신런닝 개인자산관리 회사인재를 구할려고 오신거같다.

2.Remote Company 원하는 곳에서 일해도 괜찮아 인상깊었다

주로 쓰는 협업툴 github 칸반보드 ToDo,Pending,In-Progress,Done 칸반보드를 이렇게 설정하였음

회사는 [Team Mondrian](https://teammondrian.com/)

3.디자인패턴 스터디후기 공부해야할사람 소스 분석을 많이 해야 하는사람 시스템 설계를 하는 사람 설계/아키텍쳐를 지향하는 사람 개발을 여러 사람이 나눠서 개발을 할 때 시스템 리팩토링을 해야하는 사람

4.M & 스타트업 #dvmoomoodv classprep 스타트업을 선택한 이유 기대감 근데 역시 일이많다라는거

해결방법 슬럼프 해결방법 각종 커뮤니티 활동을 통해 슬럼프를 해결하신거같다