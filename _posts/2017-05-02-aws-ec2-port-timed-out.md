---
title: Amazon EC2 - PORT 타임아웃이 나면?
published: true
---


[인스턴스 연결 중 오류 발생:연결 시간 초과](http://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html)

![](/assets/imgs/2017/05/02/port-time-out-preview-201705021116.png)

[EC2-VPC] 네트워크 ACL(액세스 제어 목록)을 검사하여 서브넷 유무를 확인하십시오. 네트워크 ACL은 로컬 IP 주소에서 적절한 포트를 통해 수신되는 인바운드와 아웃바운드 트래픽을 모두 허용해야 합니다. 기본 네트워크 ACL은 인바운드와 아웃바운드 트래픽을 모두 허용합니다. `https://console.aws.amazon.com/vpc/`에서 Amazon VPC 콘솔을 엽니다. 탐색 창에서 Your VPCs를 선택합니다.[Summary] 탭에서 [Network ACL]을 찾아 ID(acl-xxxxxxxx)를 선택하고 ACL을 선택합니다.[Inbound Rules] 탭에서 규칙이 해당 컴퓨터로부터의 트래픽을 허용하는지 확인합니다. 허용하지 않을 경우 해당 컴퓨터로부터의 트래픽을 차단하는 규칙을 삭제하거나 수정합니다.[Outbound Rules] 탭에서 규칙이 해당 컴퓨터로의 트래픽을 허용하는지 확인합니다. 허용하지 않을 경우 해당 컴퓨터로의 트래픽을 차단하는 규칙을 삭제하거나 수정합니다.

![](/assets/imgs/2017/05/02/ec2-network&security-security-groups-preview-20170502.png)