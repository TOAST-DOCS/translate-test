<!-- pre-align:aligned sig=7d9aee4cb102 -->

# Cloud Access 시작하기

**Security > Cloud Access > 콘솔 사용 가이드 > Cloud Access 시작하기**

<br>

<a id="console-settings"></a>
## 콘솔 설정하기 { #console-settings }

에이전트 준비를 완료한 뒤 Cloud Access 서비스를 사용할 수 있도록 연결 설정 및 라우팅을 설정합니다.

<br>

<a id="save-configuration-information"></a>
### 설정 정보 저장 { #save-configuration-information }

연결 설정 정보를 입력합니다. 정보를 저장한 뒤 Cloud Access를 사용할 수 있습니다.

![setting_1.PNG](../../static/images/2025.06.24/2025.07/setting_1.png)

* VPC와 서브넷을 선택합니다.
    * 만약, VPC와 서브넷이 없을 경우 NHN Cloud 콘솔 내 **VPC** 및 **Subnet** 메뉴에서 먼저 생성하세요.
* 고객 이름을 입력합니다.
    * 한글, 영어, 숫자, 그리고 일부 기호(-, _, .)를 입력할 수 있습니다.
* 알고리즘을 선택합니다.
    * 알고리즘은 AES-256과 ChaCha20을 지원합니다.

!!! danger "주의"
    * 설정 정보 저장 전 선택한 VPC에 인터넷 게이트웨이가 연결되어 있는지 확인하세요.
        * 인터넷 게이트웨이가 연결되어 있지 않으면 Cloud Access를 사용할 수 없습니다.
    * 설정 정보 저장 시 Cloud Access에 필요한 인터페이스 2개와 이중화를 위한 VIP 1개, 그리고 Floating IP 1개를 생성합니다. 생성 이후 해당 자원이 삭제되지 않도록 주의하세요.

<br>

<a id="route-settings"></a>
## 라우트 설정하기 { #route-settings }

외부에서 에이전트를 사용해 연결된 사용자가 내부 인스턴스에 접근할 수 있도록 라우트를 설정합니다.

<a id="one-vpc"></a>
### 1개의 VPC { #one-vpc }

* 사용자 IP 할당 대역: 10.0.0.0/24
* VPC: 172.16.0.0/12
* Cloud Access 생성 시 선택한 서브넷: 172.16.0.0/24
* 접근 가능 대역: 172.16.100.0/24

위와 같이 설정되어 있을 때 **Network - Routing**에서 접속 필요한 인스턴스가 속한 라우팅 테이블을 선택하여 **라우트** 탭에 아래와 같은 규칙을 추가합니다.

* 대상 CIDR: 10.0.0.0/24
* 게이트웨이: Virtual_IP 타입의 NCAccess_INF_SUB_PORT_VIP

<a id="two-vpcs"></a>
### 2개의 VPC { #two-vpcs }

* 사용자 IP 할당 대역: 10.0.0.0/24
* VPC1: 172.16.0.0/12
* VPC2: 192.168.0.0/16
* Cloud Access 생성 시 선택한 서브넷: 172.16.0.0/24
* 접근 가능 대역: 192.168.0.0/24

위와 같이 설정되어 있을 때 VPC1(로컬)과 VPC2(피어) 간 피어링을 설정합니다. 그리고 **Network - Routing**에서 접속할 인스턴스가 속한 라우팅 테이블을 선택하여 **라우트** 탭에 아래와 같은 규칙을 추가합니다.

* 대상 CIDR: 10.0.0.0/24
* 게이트웨이: VPC1과 VPC2 사이에 생성된 PEERING 타입의 네트워크 인터페이스

그리고 **Peering Gateway - 피어링**에서 **라우트** 탭을 선택하여 로컬 라우트 규칙을 추가합니다.

* 대상 CIDR: 10.0.0.0/24
* 게이트웨이: Virtual_IP 타입의 NCAccess_INF_SUB_PORT_VIP

<a id="other-projects"></a>
### 다른 프로젝트 { #other-projects }

* 사용자 IP 할당 대역: 10.0.0.0/24
* 프로젝트 1번 VPC: 172.16.0.0/12
* 프로젝트 2번 VPC: 192.168.0.0/16
* Cloud Access 생성 시 선택한 서브넷: 172.16.0.0/24
* 접근 가능 대역: 192.168.0.0/24

위와 같이 설정되어 있을 때 1번 프로젝트(로컬)와 2번 프로젝트(피어) 간 피어링을 설정합니다. 그리고 **Network - Routing**에서 접속할 인스턴스가 속한 라우팅 테이블을 선택하여 **라우트** 탭에 아래와 같은 규칙을 추가합니다.

* 대상 CIDR: 10.0.0.0/24
* 게이트웨이: 프로젝트 1번 VPC와 프로젝트 2번 VPC 사이에 생성된 PEERING 타입의 네트워크 인터페이스

그리고 **Peering Gateway - 프로젝트 피어링**에서 **라우트** 탭을 선택하여 로컬 라우트 규칙을 추가합니다.

* 대상 CIDR: 10.0.0.0/24
* 게이트웨이: Virtual_IP 타입의 NCAccess_INF_SUB_PORT_VIP

!!! danger "주의"
    * 인스턴스에 적용된 Security Groups에서 사용자 IP 할당 대역을 허용해야 통신 가능합니다. 
    * 사용자 IP 할당 대역은 아래의 항목과 겹칠 수 없습니다. 
        * 연결 설정 시 선택한 서브넷
        * 접근 가능 대역
    * 인스턴스에 2개 이상의 서브넷을 연결할 때 사용자 IP 할당 대역과 겹치는 서브넷을 구성할 경우 통신이 정상적으로 이루어지지 않습니다.

<br>

<a id="download-the-agent"></a>
## 에이전트 다운로드하기 { #download-the-agent }

Cloud Access 서비스 사용을 위한 에이전트를 다운로드합니다. 서비스에서 지원하는 운영체제는 아래와 같습니다.

* Windows 10 1903 이상(32bit/64bit)
* Windows 11(64bit)
* macOS 13.3 이상

| 운영체제 | 버전| 다운로드 | 업데이트 날짜 |
|--------|------|------|------|
| Windows(64bit)|1.2.0|[CloudAccess_Setup_x64](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_04c78c238ba54583bb1036b393ec6ae5/windows/installer/CloudAccess_Setup_x64.exe)|2026. 01. 13.|
| Windows(32bit)|1.2.0|[CloudAccess_Setup_x86](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_04c78c238ba54583bb1036b393ec6ae5/windows/installer/CloudAccess_Setup_x86.exe)|2026. 01. 13.|
|macOS|1.1.1|[CloudAccess_macOS](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_04c78c238ba54583bb1036b393ec6ae5/macos/CloudAccess%20Installer.dmg)|2026. 01. 13.|

!!! tip "알아두기"
    Cloud Access 에이전트는 사용자 단말과 서비스 간의 보안 연결을 통해 외부 환경에서도 안전한 내부 서비스 접근을 지원하는 전용 프로그램입니다.
    
<br>

<a id="add-a-connection"></a>
## 연결 설정하기 { #add-a-connection }

<a id="add-connection"></a>
### 연결 추가 { #add-connection }

에이전트를 사용하여 NHN Cloud 리소스에 접속하기 위해 연결 항목을 추가합니다.

![conncetion_add_1.PNG](../../static/images/2025.06.24/2025.07/add_1.png)

➊ 도메인 주소, ➋ 고객 키, ➌ 비밀 키를 NHN Cloud 콘솔 권한을 가진 관리자에게서 전달 받아 입력합니다. 

<br>

![conncetion_add_3.PNG](../../static/images/2025.06.24/2025.07/add_2.png)

➍ 검증 버튼을 클릭하여 검증이 완료되면 ➎ 고객 이름을 확인할 수 있습니다. 이후 **추가**를 클릭해 연결을 추가합니다.

<a id="delete-connection"></a>
### 연결 삭제 { #delete-connection }

연결 항목을 클릭하면 **연결 삭제** 버튼이 활성화되어 추가한 연결을 삭제할 수 있습니다.

<br>

!!! tip "알아두기"
    * 연결 추가에 필요한 값은 NHN Cloud 콘솔 권한을 가진 관리자를 통해 확인할 수 있습니다.
        * 고객 이름은 검증이 완료되면 관리자가 입력한 이름으로 자동으로 노출됩니다.
    * 다수의 연결 항목을 추가할 수 있으나 연결은 1개만 가능합니다.

<br>

<a id="tunnel-connection-via-authentication"></a>
## 인증을 통한 터널 연결하기 { #tunnel-connection-via-authentication }

접속이 필요한 연결을 선택한 뒤 **연결**을 클릭해 인증을 진행합니다.

<a id="notice-settings"></a>
### 안내 설정 { #notice-settings }

* Cloud Access 서비스 권한을 가진 관리자가 설정한 안내 문구를 노출합니다.   
    * **설정-안내 설정**을 **사용 안 함** 설정 시 노출되지 않습니다.

<a id="first-authentication-account-password"></a>
### 1차 인증(계정 및 비밀번호) { #first-authentication-account-password }

![login_1.PNG](../../static/images/2025.06.24/2025.07/6.png)

* 계정명: Cloud Access 서비스 권한을 가진 관리자로부터 생성 받은 계정을 입력합니다.
* 비밀번호: 계정 생성 시 입력한 메일 주소로 수신한 임시 비밀번호를 입력합니다.
* 계정명 저장: 클릭 후 로그인을 한 뒤 재로그인 시 직전에 로그인 한 계정명을 자동으로 입력하여 노출합니다. 

<a id="agree-to-collection-and-usage-of-personal-information"></a>
### 개인정보 수집·이용 동의 { #agree-to-collection-and-usage-of-personal-information }
* Cloud Access 서비스를 운영하기 위한 개인정보를 수집합니다.
    * 거절 시 서비스 이용이 제한될 수 있습니다.

<a id="additional-authentication"></a>
### 추가 인증 { #additional-authentication }

* 1차 인증을 완료하게 되면 관리자가 설정한 인증 정책에 따라 추가 인증을 진행합니다. 
    * 총 4개의 인증 방식을 지원합니다.
        * 이메일
        * 휴대폰 
        * TOTP(time-based one-time password) 
        * 생체 정보(패스 키) 

<a id="change-initial-password"></a>
### 초기 비밀번호 변경 { #change-initial-password }

* 초기 비밀번호를 변경합니다.
    * Cloud Access 서비스 권한을 가진 관리자가 설정한 비밀번호 정책에 따라 비밀번호를 변경할 수 있습니다.

<br>

!!! tip "알아두기"
    * NHN Cloud 콘솔 권한을 가진 관리자가 사용자 계정을 생성하면 등록된 사용자의 이메일 주소로 임시 비밀번호와 에이전트 다운로드 링크가 발송됩니다.
    * 계정을 생성한 뒤 첫 인증 시에만 개인정보 수집·이용 동의 절차를 진행하며, 계정 연결이 완료되어야만 동의를 득한 것으로 간주합니다(동의 수락을 클릭 후 인증을 완료하지 않고 취소하면 다시 동의를 해야 합니다.).
    * 비밀번호 설정 시 관리자가 설정한 비밀번호 정책과 관계없이 아래의 정책은 필수로 적용됩니다.
        * 6자리 이상 30자리 이하의 길이
        * 사용자 계정(ID)과 동일한 비밀번호 설정 금지
    * **계정명 저장**은 직전에 로그인한 계정명만 노출하며, 로그인하지 않은 계정은 노출하지 않습니다.

<br>

<a id="agent-features"></a>
## 에이전트 기능 살펴보기 { #agent-features }

에이전트의 트레이 아이콘 기능에 대해서 살펴봅니다.

<br>

<a id="before-connecting-to-agent"></a>
### 에이전트 연결 전 { #before-connecting-to-agent }
 * 열기: 연결 항목을 보여주는 화면을 엽니다.
 * 연결: 연결 항목을 보여줍니다.
 * 업데이트 확인: 에이전트의 현재 상태를 확인합니다. 업데이트 필요 시 업데이트를 진행합니다.
 * 버전 정보: 에이전트의 현재 버전 정보와 오픈소스 라이선스 및 개인정보 처리 방침을 확인할 수 있습니다.
 * 설정: 에이전트의 환경 설정 및 언어 설정을 할 수 있습니다.
      * 클라우드 환경 설정: 퍼블릭 또는 공공클라우드를 선택합니다.
      * 언어 설정: 한국어, 영어, 일본어를 지원합니다.
 * 종료: 에이전트를 종료합니다.

<a id="after-connecting-to-agent"></a>
### 에이전트 연결 후 { #after-connecting-to-agent }
고객 이름과 계정명이 노출됩니다.
* 열기: 연결 항목을 보여주는 화면을 엽니다.
* 연결 해제: 에이전트 연결을 해제합니다.
* 비밀번호 변경: 비밀번호를 변경합니다.
* 공지: 설정된 공지를 확인합니다(공지가 설정되어 있지 않을 수 있습니다.).
* 버전 정보: 에이전트의 현재 버전 정보와 오픈소스 라이선스 및 개인정보 처리 방침을 확인할 수 있습니다.
* 종료: 에이전트를 종료합니다.

<br>

<a id="delete-agent"></a>
## 에이전트 삭제하기 { #delete-agent }

에이전트는 사용자가 언제든지 직접 삭제할 수 있습니다.

* Windows: 설정 > 앱 > 설치된 앱(앱 및 기능)에서 Cloud Access 선택 후 제거를 클릭하여 삭제
* macOS: Finder > 응용 프로그램 선택 후 Cloud Access를 휴지통으로 이동하여 삭제

!!! danger "주의"
    에이전트 삭제 시 Cloud Access 서비스 이용이 불가능하거나 제한될 수 있습니다.