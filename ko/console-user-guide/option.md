<!-- pre-align:aligned sig=05296d704911 -->

<a id="options"></a>
## 옵션 { #options }

**Security > Network Firewall > 콘솔 사용 가이드 > 옵션**

**옵션** 탭에서는 Network Firewall 운영에 필요한 옵션을 설정할 수 있습니다.

<br>

<a id="configure-logs"></a>
## 로그 설정하기 { #configure-logs }

<a id="default-block-policy-log-settings"></a>
### 기본 차단 정책 로그 설정 { #default-block-policy-log-settings }

* Network Firewall 생성 후 필수로 생성되는 기본 차단 정책 로그의 저장 여부를 선택합니다.
    * 사용 선택 시 기본 차단 정책으로 생성된 로그는 트래픽 로그에서 검색 가능합니다.

<a id="log-remote-transfer-setting"></a>
### 로그 원격 전송 설정 { #log-remote-transfer-setting }

* 원격지로 트래픽 로그를 저장할 수 있는 옵션을 선택합니다.
    * Syslog: 최대 2개의 원격지 주소로 로그를 전송
        * 2개의 원격지는 개별적으로 설정 가능(IP 주소, 프로토콜, 포트 번호)
    * Object Storage: NHN Cloud에서 제공하는 Object Storage 서비스로 로그를 전송
    <img src="../../../static/images/24.11.07/OBS_5.png" height="65%" />
        * 액세스 키 / 비밀 키: Object Storage 서비스에서 S3 API 자격 증명 등록 시 확인 가능한 액세스 키 정보를 입력
        * 버킷 이름: Object Storage 서비스에서 생성한 컨테이너의 이름을 입력
        * 엔드포인트: 리전별 엔드포인트를 확인한 뒤 위치에 맞게 엔드포인트를 입력
        * 리전: 리전별 이름을 확인한 뒤 리전 위치에 맞게 이름을 입력
    * Log & Crash Search: NHN Cloud에서 제공하는 Log & Crash Search 서비스로 로그를 전송
    <img src="../../../static/images/24.11.07/LNCS_2.png" height="65%" />
        * AppKey: Log & Crash Search 서비스를 활성화 후 생성된 AppKey를 입력

!!! tip "알아두기"

    * Object Storage 설정 시 [사용자 가이드](/Storage/Object%20Storage/ko/s3-api-guide/#aws-sdk)를 참고하여 입력하세요.
    * Log & Crash Search 서비스를 사용 시 로그 알람 설정 기능을 활용하여 이상 행위를 탐지할 수 있습니다.
    예를 들어, Network Firewall에 특정 목적지로 향하는 SSH 통신에 대한 ACL 차단 정책을 추가한 뒤 해당 정책에서 발생되는 로그에 대한 알람 조건을 설정합니다. (예: 1분 동안 SSH 접속 시도 로그가 20회 이상 발생)
    사용자가 설정한 조건을 만족 시 알람을 수신할 수 있습니다.  

<br>

<a id="configure-general-settings"></a>
## 일반 설정하기 { #configure-general-settings }

<a id="mirroring-settings"></a>
### 미러링 설정 { #mirroring-settings }

* Network Firewall에서 제공하는 기능 중 미러링의 사용 여부를 선택할 수 있습니다.
    * 사용 선택 시 필요한 서브넷은 Network Firewall 생성에 사용했던 서브넷을 사용합니다.

<a id="configure-network-firewall"></a>
### Network Firewall 구성 { #configure-network-firewall }

* 단일 또는 이중화로 Network Firewall의 구성 방식을 설정할 수 있습니다.

<a id="delete-network-firewall"></a>
### Network Firewall 삭제 { #delete-network-firewall }

* 운영 중인 Network Firewall을 삭제할 수 있습니다.
    * Network Firewall은 한국(판교) 리전과 한국(평촌) 리전에서 각각 삭제할 수 있습니다.

!!! tip "알아두기"

    * ACL 설정에 필요한 미러링 인터페이스의 IP 정보는 **Network > Network Interface**에서 확인 가능합니다.
        * 인터페이스 이름: NetworkFirewall_INF_MIRRORING_S_NAT_VIP
    * 구성 방식 변경 시 몇 분 정도의 시간이 소요되며, 구성 변경이 완료되기 전까지 서비스에 영향이 있을 수 있습니다.
    * 정책, NAT 등 Network Firewall 변경 작업은 구성 방식 변경이 완료된 뒤 진행할 것을 권장합니다.

!!! danger "주의"

    운영 중인 Network Firewall을 삭제할 경우 Network Firewall과 연결된 다른 서비스를 고려하여 진행하세요.  
    
<br>

<a id="disable-network-firewall-service"></a>
## Network Firewall 서비스 비활성화 { #disable-network-firewall-service }

**프로젝트 관리 > 이용 중인 서비스**에서 Network Firewall 서비스를 비활성화할 수 있습니다.

!!! tip "알아두기"

    * Network Firewall 서비스 비활성화는 한국(판교) 리전과 한국(평촌) 리전에 모두 적용됩니다.
    예를 들어 Network Firewall 서비스를 동일한 프로젝트의 한국(판교) 리전과 한국(평촌) 리전에 모두 활성화한 경우 두 리전 중 하나의 Network Firewall 서비스만 비활성화할 수 없습니다.
    * 비활성화하려면 한국(판교) 리전과 한국(평촌) 리전에서 각각 Network Firewall을 삭제한 뒤 진행하세요.