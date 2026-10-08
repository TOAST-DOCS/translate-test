<!-- pre-align:aligned sig=9be9bdfa8e4e -->

<a id="network-firewall-troubleshooting-guide"></a>
## Network Firewall 문제 해결 가이드 { #network-firewall-troubleshooting-guide }

**Security > Network Firewall > 문제 해결 가이드**

<br>

<a id="i-cannot-create-the-network-firewall-service"></a>
## Network Firewall 서비스를 생성할 수 없습니다. { #i-cannot-create-the-network-firewall-service }

아래의 네트워크 자원이 준비되어 있는지 체크합니다.

* Hub VPC와 Spoke VPC가 준비되어 있는지 확인합니다.
* Hub VPC에 트래픽, NAT, 외부 전송 용도의 서로 다른 서브넷 3개가 있는지 확인합니다.
* Spoke VPC 또는 Spoke 서브넷이 준비되어 있는지 확인합니다.
* Hub VPC의 라우팅 테이블에 인터넷 게이트웨이가 연결되어 있는지 확인합니다.

<br>

<a id="instances-in-the-spoke-vpc-cannot-communicate-with-the-internet"></a>
## Spoke VPC에 속해있는 인스턴스가 인터넷 통신이 안됩니다. { #instances-in-the-spoke-vpc-cannot-communicate-with-the-internet }

Spoke VPC의 공인 통신은 라우팅, 피어링, NAT, ACL 정책이 모두 설정되어 있어야 동작합니다. 아래의 내용을 확인하세요.

* Hub VPC와 Spoke VPC 사이의 피어링이 생성되어 있는지 확인합니다.
* Hub VPC 라우팅에 Spoke CIDR 대상 경로가 추가되어 있는지 확인합니다.
* Spoke VPC 라우팅에 0.0.0.0/0 또는 필요한 대상 CIDR이 피어링 게이트웨이로 설정되어 있는지 확인합니다.
* Peering Gateway 라우트에서 NetworkFirewall_INF_TRAFFIC_VIP가 게이트웨이로 설정되어 있는지 확인합니다.
* **Network Firewall > NAT** 탭에서 NAT 설정이 추가되어 있는지 확인합니다.
* **Network Firewall > 정책 > ACL** 탭에서 필요한 허용 정책이 추가되어 있는지 확인합니다.

<br>

<a id="instances-cannot-be-accessed-from-outside"></a>
## 외부에서 인스턴스에 접속되지 않습니다. { #instances-cannot-be-accessed-from-outside }

외부에서 인스턴스에 접속하려면 NAT, ACL, Security Groups 설정이 모두 필요합니다. 아래 내용을 확인하세요.

* **Network Firewall > NAT** 탭에서 NAT 전 IP와 NAT 후 IP가 올바르게 연결되어 있는지 확인합니다.
    * NAT 후 IP에 해당하는 IP 객체가 **객체** 탭에 먼저 생성되어 있는지 확인합니다.
* **Network Firewall > 정책 > ACL** 탭에서 출발지, 목적지, 목적지 포트에 대한 허용 정책이 있는지 확인합니다.
* 인스턴스의 Security Groups에서도 출발지 IP와 포트를 허용했는지 확인합니다.
* 접속 필요한 인스턴스에 직접 Floating IP를 연결하지 않았는지 확인합니다.
    * 직접 Floating IP를 연결할 경우 통신에 문제가 있을 수 있습니다.

<br>

<a id="blocked-logs-are-not-visible-in-the-log-tab"></a>
## 차단된 로그가 로그 탭에서 보이지 않습니다. { #blocked-logs-are-not-visible-in-the-log-tab }

default-deny 정책에 의해 차단된 로그는 기본 차단 정책 로그 설정을 사용으로 변경해야 확인할 수 있습니다. 아래 경로에서 설정을 확인하세요.

* **Network Firewall > 옵션 > 로그 설정**에서 기본 차단 정책 로그 설정으로 이동하여 **사용**으로 변경합니다.
* 트래픽 로그는 정책별 로깅 여부와 옵션 설정에 영향을 받으므로 ACL 정책의 로깅 설정도 함께 확인하세요.

<br>

!!! tip "문제가 해결되지 않을 경우"
    문제 해결 가이드의 안내에 따라 진행하였으나 문제가 해결되지 않을 경우 NHN Cloud 고객 센터로 문의하세요.
    * [온라인 1:1 문의 바로가기](    
    https://www.nhncloud.com/kr/support/inquiry?alias=sec_nfw_fn)
    * 대표 전화: 1588-7967(운영시간: 월~금 10:00-19:00)