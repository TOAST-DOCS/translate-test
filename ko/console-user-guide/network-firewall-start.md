<!-- pre-align:aligned sig=f37ed2d1fbde -->

<a id="getting-started-with-network-firewall"></a>
## Network Firewall 시작하기 { #getting-started-with-network-firewall }

**Security > Network Firewall > 콘솔 사용 가이드 > Network Firewall 시작하기**

<br>

<a id="prepare-before-creating-network-firewall"></a>
## Network Firewall 생성 전 준비하기 { #prepare-before-creating-network-firewall }

Network Firewall 생성에 필요한 최소 네트워크 서비스 자원은 아래와 같습니다.

<a id="requirements-for-a-single-project-configuration"></a>
### 1개의 프로젝트 구성 시 준비 사항 { #requirements-for-a-single-project-configuration }

* 1개의 프로젝트
* 2개의 VPC(Hub VPC, Spoke VPC)
* Hub VPC 내 3개의 서브넷
    * 트래픽(내부) 서브넷, NAT(외부) 서브넷, 외부 전송 서브넷
* Spoke VPC 내 최소 1개의 서브넷
* Hub VPC의 Routing에 연결된 인터넷 게이트웨이

<a id="requirements-for-configuring-2-spoke-vpcs-within-a-single-project"></a>
### 1개의 프로젝트 내 2개의 Spoke VPC 구성 시 준비 사항 { #requirements-for-configuring-2-spoke-vpcs-within-a-single-project }

* 1개의 프로젝트
* 3개의 VPC(Hub VPC, Spoke1 VPC, Spoke2 VPC)
* Hub VPC 내 3개의 서브넷
    * 트래픽(내부) 서브넷, NAT(외부) 서브넷, 외부 전송 서브넷
* Spoke1 VPC, Spoke2 VPC 내 각각 최소 1개의 서브넷
* Hub VPC의 Routing에 연결된 인터넷 게이트웨이

<a id="preparations-for-configuring-more-than-one-project"></a>
### 1개 이상의 프로젝트 구성 시 준비 사항 { #preparations-for-configuring-more-than-one-project }

* 2개의 프로젝트
* 2개의 VPC(각각 프로젝트에 Hub VPC, Spoke VPC)
* Hub VPC 내 3개의 서브넷
    * 트래픽(내부) 서브넷, NAT(외부) 서브넷, 외부 전송 서브넷
* Spoke VPC 내 최소 1개의 서브넷
* Hub VPC의 Routing에 연결된 인터넷 게이트웨이

<a id="preparations-for-configuring-cross-region-projects"></a>
### 다른 리전 간 프로젝트 구성 시 준비 사항 { #preparations-for-configuring-cross-region-projects }

* 1개의 프로젝트
* 2개의 VPC(KR1 리전에 Hub VPC, KR2 리전에 Spoke VPC)
* Hub VPC 내 3개의 서브넷
    * 트래픽(내부) 서브넷, NAT(외부) 서브넷, 외부 전송 서브넷
* Spoke VPC 내 최소 1개의 서브넷
* Hub VPC의 Routing에 연결된 인터넷 게이트웨이

<a id="preparations-for-configuring-multiple-subnets-within-a-single-vpc"></a>
### 단일 VPC 내 여러 개의 서브넷 구성 시 준비 사항 { #preparations-for-configuring-multiple-subnets-within-a-single-vpc }

* 1개의 프로젝트
* 1개의 VPC
* 3개의 Hub 서브넷
    * 트래픽(내부) 서브넷, NAT(외부) 서브넷, 외부 전송 서브넷
* Hub 서브넷과 겹치지 않는 최소 1개의 Spoke 서브넷
* Spoke 서브넷에 연결할 라우팅 테이블
* VPC의 Routing에 연결된 인터넷 게이트웨이

!!! tip "알아두기"
    * **Network Firewall > 개요**에서 서비스 구성도를 참조하세요.
    * 위의 서비스 자원은 [Network] 카테고리에서 생성 가능합니다. 
    * Network Firewall 생성은 프로젝트당 1개씩만 생성 가능합니다.

<br>

<a id="create-network-firewall"></a>
## Network Firewall 생성하기 { #create-network-firewall }

1. **Security > Network Firewall**로 이동합니다.
2. 각 필수 항목을 모두 선택하고 하단의 **Network Firewall 생성**을 클릭합니다.
    * RBAC: 인스턴스 객체 조회, Network Firewall 서비스 제공에 필요한 API 권한을 부여
    * 구성 방식: 단일 구성과 이중화 구성을 선택합니다.
    * VPC: Network Firewall에서 사용할 VPC
    * 서브넷: Network Firewall에서 내부 트래픽 제어를 위해 사용할 서브넷
    * NAT: Network Firewall에서 외부 트래픽 제어를 위해 사용할 서브넷
    * 외부 전송: Network Firewall에서 생성된 트래픽과 로그를 전송할 서브넷
    <img src="../../../static/images/24.09.12/create.png" height="60%" />

!!! tip "알아두기"
    * 생성된 Network Firewall은 사용자의 프로젝트에 노출되지 않습니다. 
    * 서브넷, NAT, 외부 전송에 사용하는 서브넷은 모두 다른 서브넷으로 선택해야 합니다.
        * 가급적 NHN Cloud 콘솔에서 생성할 수 있는 최소 단위(28비트)로 생성할 것을 권장합니다.
    * Network Firewall이 속할 VPC의 라우팅 테이블에 인터넷 게이트웨이가 연결되어 있어야 생성 가능합니다.
    * Network Firewall이 소유하고 있는 CIDR 대역과 연결이 필요한 CIDR 대역은 중복되지 않아야 합니다.
    * 단일 또는 이중화 구성을 선택하여 Network Firewall을 생성한 뒤 변경이 필요할 경우 **옵션** 탭에서 구성을 변경할 수 있습니다. 하지만 가용성 영역은 변경이 불가능하므로 이중화 구성의 경우 가급적 가용성 영역을 분리하여 구성하세요. 

!!! danger "주의"
    * Security Groups와는 별개의 서비스이므로 Network Firewall을 사용하면 두 서비스를 모두 허용해야 인스턴스에 접근할 수 있습니다.
    * **Network > Network Interface**에서 Virtual_IP 타입으로 생성되어 있는 IP는 Network Firewall에서 이중화 용도로 사용 중이므로 삭제할 경우 통신이 차단될 수 있습니다.

<br>

<a id="configure-connection"></a>
## 연결 설정하기 { #configure-connection }

> [예시]
> Network Firewall이 사용하는 VPC(Hub)는 10.0.0.0/24이고, Network Firewall과 연결이 필요한 VPC(Spoke)는 172.16.0.0/24일 때

1. **Network > Peering Gateway**로 이동하여 피어링을 생성합니다.
    * 피어링 게이트웨이 연결에 대한 자세한 사항은 [사용자 가이드](https://docs.nhncloud.com/ko/Network/Peering%20Gateway/ko/console-guide/)를 참조하세요.
    <img src="../../../static/images/23.12.19/ConnectionSettings3.png" height="65%" />
    <img src="../../../static/images/23.12.19/ConnectionSettings4.png" height="65%" />

!!! tip "알아두기"
    * Spoke VPC의 위치에 따라 알맞은 피어링을 생성합니다. 
        * Spoke VPC가 같은 프로젝트라면 피어링을 생성합니다.
        * Spoke VPC가 다른 프로젝트라면 프로젝트 피어링을 생성합니다.
        * Spoke VPC가 다른 리전이라면 리전 피어링을 생성합니다.

<br>

2. **Network > Routing**으로 이동하여 Hub VPC를 선택한 후 아래의 라우팅을 설정합니다.
    * 대상 CIDR: 172.16.0.0/24
    * 게이트웨이: 피어링 연결 후 추가된 피어링 타입의 게이트웨이
    <img src="../../../static/images/23.12.19/ConnectionSettings5.png" height="65%" />

<br>

3. **Network > Routing**으로 이동하여 Spoke VPC를 선택한 후 아래의 라우팅을 설정합니다.
    * 대상 CIDR: 0.0.0.0/0
    * 게이트웨이: 피어링 연결 후 추가된 피어링 타입의 게이트웨이
    <img src="../../../static/images/23.12.19/ConnectionSettings6.png" height="65%" />

!!! tip "알아두기"
    * 위와 같이 라우팅을 설정하면 Spoke VPC의 모든 통신이 Network Firewall을 통과하게 됩니다.
        * 통신을 분기 처리해야 할 경우 0.0.0.0/0이 아닌 대상을 명확하게 설정하세요.

<br>

4. **Network > Peering Gateway**로 이동하여 라우팅을 설정합니다.
    * 생성된 피어링을 선택하여 **라우트** 탭으로 이동합니다.
    * **피어** 또는 **로컬 라우트 변경** 버튼을 눌러 아래와 같이 라우팅을 설정합니다.
        * 대상 CIDR: 0.0.0.0/0
        * 게이트웨이: NetworkFirewall\_INF\_TRAFFIC\_VIP
        <img src="../../../static/images/23.12.19/ConnectionSettings7.png" height="65%" />
        <img src="../../../static/images/23.12.19/ConnectionSettings8.png" height="50%" />

위의 라우팅 설정이 완료되면 Spoke VPC에 있는 인스턴스가 Network Firewall을 경유하여 공인 통신을 할 수 있습니다. (**Network Firewall > NAT** 탭에서 목적지 NAT 추가 필요)

<br>

**만약 Spoke VPC의 서브넷이 2개 이상이고, Network Firewall을 통해 서브넷 간 트래픽 제어가 필요한 경우** 아래의 라우팅을 추가합니다.

> [예시]
> Spoke VPC(172.16.0.0/24)의 서브넷이 172.16.0.0/25와 172.16.0.128/25일 때

* **Network > Routing**으로 이동하여 Spoke VPC를 선택한 후 아래의 라우팅 2개를 추가합니다.
    * 대상 CIDR: 172.16.0.0/25과 172.16.0.128/25
    * 게이트웨이: 피어링 연결 후 추가된 피어링 타입의 게이트웨이
    <img src="../../../static/images/23.12.19/ConnectionSettings9.png" height="65%" />
    <img src="../../../static/images/23.12.19/ConnectionSettings10.png" height="65%" />

위의 라우팅 설정이 완료되면 Spoke VPC 안에 있는 서브넷 간 Network Firewall을 경유하여 사설 통신을 할 수 있습니다. (**Network Firewall > 정책** 탭에서 정책 추가 필요)

<br>

**만약 Spoke VPC가 2개 이상**이라면 아래의 라우팅을 추가합니다.

> [예시]
> Spoke VPC1(172.16.0.0/24)과 Spoke VPC2(192.168.0.0/24)일 때

* **Network > Routing**으로 이동하여 Hub VPC를 선택한 후 아래의 라우팅 2개를 추가합니다.
    * Spoke VPC 1
        * 대상 CIDR: 172.16.0.0/24
        * 게이트웨이: Hub VPC와 Spoke VPC1 사이에 추가된 피어링 타입의 게이트웨이
    * Spoke VPC 2
        * 대상 CIDR: 192.168.0.0/24
        * 게이트웨이: Hub VPC와 Spoke VPC2 사이에 추가된 피어링 타입의 게이트웨이
        <img src="../../../static/images/23.12.19/ConnectionSettings11.png" height="65%" />

!!! tip "알아두기"
    **연결 설정**의 **4**와 같이 Spoke VPC2-Hub 간 VPC 피어링에도 라우트 추가 설정이 필요합니다.

<br>

**만약 같은 VPC에서 Spoke 서브넷을 구성할 경우** 새로운 라우팅 테이블을 생성하여 서브넷을 연결하고 라우트를 추가합니다. 
* **Network > Routing**에서 라우팅 테이블을 생성하고 라우트를 추가합니다.
    <img src="../../../static/images/24.11.07/routetable_create.png" height="65%" />
    <img src="../../../static/images/24.11.07/route_create.png" height="65%" />

<br>

* **Network > Subnet**에서 Network Firewall과 겹치지 않는 Spoke 서브넷을 새로 생성하고 라우팅 테이블을 연결합니다.
    <img src="../../../static/images/24.11.07/subnet_create.png" height="65%" />
    <img src="../../../static/images/24.11.07/routetable_connect.png" height="65%" />

<br>

위의 라우팅 설정이 완료되면 서로 다른 Spoke VPC 간 Network Firewall을 경유하여 사설 통신을 할 수 있습니다. (**Network Firewall > 정책** 탭에서 정책 추가 필요)