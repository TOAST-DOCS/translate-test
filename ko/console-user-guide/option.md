<!-- pre-align:aligned sig=a867bdc4fe63 -->

# 설정

**Security > Cloud Access > 콘솔 사용 가이드 > 설정**

**설정** 탭에서는 Cloud Access 운영에 필요한 여러 가지 설정을 할 수 있습니다.

<br>

<a id="log-settings"></a>
## 로그 설정하기 { #log-settings }

<a id="default-deny-policy-log-settings"></a>
### 기본 차단 정책 로그 설정 { #default-deny-policy-log-settings }

Cloud Access 서비스를 활성화하면 **정책 - ACL 정책** 탭에 default-deny 정책이 노출되며, **사용**으로 설정할 경우 해당 정책에 매칭되는 차단 로그가 저장됩니다.

<a id="remote-log-transfer-settings"></a>
### 로그 원격전송 설정 { #remote-log-transfer-settings }

Cloud Access 운영 중 발생된 트래픽 로그를 원격지로 자동 전송하여 장기간 보관할 수 있도록 Syslog, Object Storage, Log & Crash Search를 통한 원격 전송 기능을 제공합니다.

* Syslog: 최대 2개의 IP 주소를 입력하여 트래픽 로그를 전송합니다.

![syslog.PNG](../../static/images/2025.06.24/syslog.png)

* Object Storage: NHN Cloud에서 제공하는 Object Storage 서비스로 로그를 전송합니다.

![OBS.PNG](../../static/images/2025.06.24/OBS.png)

* Log & Crash Search: NHN Cloud에서 제공하는 Log & Crash Search 서비스로 로그를 전송합니다.

![LNCS.PNG](../../static/images/2025.06.24/LNCS.png)

<br>

!!! tip "알아두기"

    * Syslog는 단일 IP 주소만 설정할 수 있으며, IP 범위 또는 대역은 지원하지 않습니다.
    * Object Storage 및 Log & Crash Search로 로그를 전송하려면, 해당 서비스가 사전에 활성화되어 있어야 합니다. 
    * Object Storage 설정에 필요한 입력 정보는 [Object Storage 사용자 가이드](/Storage/Object%20Storage/ko/s3-api-guide/#aws-sdk)를 참고하세요.

<br>

<a id="general-settings"></a>
## 일반 설정하기 { #general-settings }

<a id="connection-settings"></a>
### 연결 설정 { #connection-settings }

* 연결 설정에서는 Cloud Access 서비스 활성화 시 입력한 정보를 확인할 수 있으며, 이 중 고객 이름과 알고리즘은 변경 가능합니다.
    * 알고리즘은 AES-256과 ChaCha20을 지원합니다.

<a id="login-security-settings"></a>
### 로그인 보안 설정 { #login-security-settings }

* 로그인 보안 설정에서는 로그인 실패 횟수, 비밀번호 만료 기간, 비밀번호 정책을 설정할 수 있습니다.
    * 로그인 실패: 사용자가 인증을 시도할 때 허용되는 최대 실패 횟수를 설정합니다. 
        * 최소 1회부터 최대 5회까지 설정할 수 있습니다.
    * 비밀번호 만료: 계정 생성 후 비밀번호의 유효 기간을 설정합니다.
        * 최소 1일에서 최대 180일까지 설정 가능합니다.
    * 비밀번호 정책: 에이전트를 통해 접속하는 사용자의 비밀번호 생성 기준을 설정합니다.
        * 일부 필수 정책은 설정 여부와 관계없이 자동으로 적용됩니다. 

<a id="notice-settings"></a>
### 안내 설정 { #notice-settings }

* 안내 설정에서는 사용자가 에이전트를 통해 인증 시 표시할 안내 문구를 설정할 수 있습니다.
    * 안내 문구는 최대 200자까지 입력 가능합니다.

<a id="logo-settings"></a>
### 로고 설정 { #logo-settings }

* 로고 설정에서는 사용자의 법인 로고 등 정해진 조건에 맞는 이미지를 업로드하여 로그인 인증 화면에 로고를 표시하도록 설정할 수 있습니다.

<br>

!!! tip "알아두기"

    * 연결 설정 항목 중 도메인과 고객 키, 그리고 비밀 키는 사용자가 에이전트 연결 추가 시 사용하는 정보입니다. 외부에 유출되지 않도록 유의하세요.
    * 로그인 실패 또는 비밀번호 만료로 인해 계정이 잠긴 경우 Cloud Access 서비스 권한이 있는 NHN Cloud 콘솔 관리자에게 문의하세요.
    * 안내 문구는 로그인 후에도 트레이 아이콘 기능을 통해 확인할 수 있습니다.

!!! danger "주의"
    로그인 보안 설정은 Cloud Access 에이전트를 사용하는 모든 사용자에게 공통 적용되므로 사용 설정 시 주의하세요.