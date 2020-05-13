---

title: 신경망 첫걸음 공부중
published: true
comments : true
---


## Jupyter
[jupyter]((https://aws.amazon.com/ko/route53/))




![](/assets/imgs/2017/11/26/20171126_01.png)

파이썬은 들여쓰기
코드가 다른 코드에 종속되는지 여부를 나타내는 매우 중요한 역할


![](/assets/imgs/2017/11/26/20171126_02.png)

![](/assets/imgs/2017/11/26/20171126_03.png)

![](/assets/imgs/2017/11/26/20171126_04.png)

def 바로 함수를 정의하는 키워드

import 명령어는 외부로부터 추가적인 기능을 가져올 때 사용하는 명령어

numpy라는 모듈 -> 배열 계산 등 유용한 기능을 포함

``` python
a = numpy.zeros( [3,2] )
print(a)

```

![](/assets/imgs/2017/11/26/20171126_05.png)

배열 또는 행렬은 신경망에서 입력의 전파와 오차의 역전파 과정
계산에 대한 명령을 간단히 하도록 도와주는 매우 유용한 개념



![](/assets/imgs/2017/11/26/20171126_06.png)
import matplotlib.pyplot 시각화 기능 담당 라이브러리

시각화 imshow(배열,속성)

interpolation="nearest"
같은 값을 가지는 원소는 같은 색상으로 표시


![](/assets/imgs/2017/11/26/20171126_07.png)

객체를 정의할 때에는 class라는 키워드 

클래스를 가지고 만든 객체 = 클래스의 인스턴스(instance)


![](/assets/imgs/2017/11/26/20171126_08.png)

매개변수로 self 적는이유 파이썬이 함수를 생성할 때
올바른 객체에 할당하기 위해

클래스는 정의이며 객체는 그정의를 현실에서 구현한 인스턴스


파이썬에서는 최초로 객체를 생성될때 
__init__()함수를 호출하도록 약속되어있음 


![](/assets/imgs/2017/11/26/20171126_09.png)


![](/assets/imgs/2017/11/26/20171126_10.png)


## 파이썬으로 인공 신경망 만들기

뼈대 코드 
- 초기화: 입력,은닉,출력 노드의 수 설정
- 학습: 학습 데이터들을 통해 학습하고 이에 따라 가중치를 업데이트 
- 질의: 입력을 받아 연산한 후 출력 노드에서 답을 전달

![](/assets/imgs/2017/11/26/20171126_11.png)

## 신경망의 핵심인 가중치
연결 노드의 가중치 
가중치 전파시 전달되는 신호와 역전파 시 오차를 계산하는 데 쓰임 
신경망을 개선하는 역할을 수행함

- (은닉노드 X 입력노드)의 크기를 가지는 입력계층과 은닉 계층사이의 가중치의 행렬 W(input_hidden)

- (출력노드 X 은닉노드)의 크기를 가지는 은닉 계층과 출력 계층 사이의 가중치의 행렬 W(hidden_output)

![](/assets/imgs/2017/11/26/20171126_12.png)
가중치는 양수가 아니라 음수 일수도 있음

![](/assets/imgs/2017/11/26/20171126_13.png)


![](/assets/imgs/2017/11/26/20171126_14.png)

## 더 정교한 가중치

numpy.random.normal() 

이 변수에 필요한 매개변수는 정규분포의 중심,표준편차,numpy 행렬 

``` python
self.wih = numpy.random.normal(0.0, pow(self.hnodes,-0.5), (self.hnodes,self.inodes))

self.who = numpy.random.normal(0.0, pow(self.onodes, -0.5),(self.onodes,self.hnodes))

## 표준편차는 파이썬의 문법으로 pow(self.hnodes, -0.5) 루트를 씌우고 역수

```



