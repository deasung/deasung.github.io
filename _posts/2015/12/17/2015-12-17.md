---

title: 고정 IP를 제공하는 Elastic IP
layout: post 
category: aws 
tags: 
  - aws
---

고정 IP를 제공하는 Elastic IP
---------------------------------------------

Elastic IP는 고정된 공인 IP를 제공함. EC2 인스턴스를 생성하면 기본적으로 공인 IP가 부여됨.

하지만 이 IP주소는 EC2 인스턴스가 실행되고 있는 동안에만 유효함 
-> EC2 인스턴스가 중단되면 IP주소는 반납됨 따라서 이 공인 IP는 바뀔수가 있슴 즉 유동IP

Elastic IP 주소는 한번 할당받으면 절대 바뀌지 않는 IP주소 
사용하지 않을경우 반납할수 있음.




Associate Address
* Instance : ec2 인스턴스ID
* Network Interface : Network Interface 입력 부분을 클릭하면 현재 생성되어 있는 Network Interface가 표시됨.
     EC2 인스턴스에 연결하기로 했으므로 이부분은 비워라
* Private IP Address : 내부 사설 IP주소. Instance에서 EC2 인스턴스를 선택하면 자동으로 설정됨.
* Reassociation : 해당 Elastic IP가 이미 다른 곳에 연결되어 있는데도 다시 새로운 곳에 연결하려고 하면 에러가 발생함

Reassociation에 체크하면 다른 곳에 연결되어 있더라도 강제로 가져와서 연결함.

이제 이 공인 IP를 DNS 서버에서 도메인과 연결하거나 HTTP,SSH,RDP등의 접속을 할수 있음.