<!-- pre-align:aligned sig=dbacc26b661d -->

# 앱 증명 가이드

<a id="overview"></a>
## 개요 { #overview }

NHN AppGuard의 **앱 증명(App Attestation)**은 앱의 위변조 여부와 실행 환경의 안전성을 서버에서 검증하고, 검증에 성공한 앱만 서비스에 접근할 수 있도록 제어할 수 있는 수단을 제공합니다.

<a id="how-it-works"></a>
## 동작 흐름 { #how-it-works }

앱에서 앱 증명을 요청하면 NHN AppGuard 서버에서 검증을 수행하고, 결과를 토큰으로 발급합니다. 발급 받은 토큰을 서버로 전달하여 검증합니다.

```mermaid
sequenceDiagram
    participant App as 앱
    participant AppGuard as AppGuard 서버
    participant Server as 서버
    Note over App, Server: 토큰 발급
    App->>AppGuard: 1. authenticate()
    Note over AppGuard: 무결성 검증
    AppGuard-->>App: 2. JWT 토큰
    Note over App, Server: 토큰 검증
    App->>Server: 3. token + appId 전달
    Server->>AppGuard: 4. 토큰 검증 API 호출
    AppGuard-->>Server: 5. 검증 결과
    Server-->>App: 6. 서비스 허용/거부
```

<a id="how-to-apply"></a>
## 적용 절차 { #how-to-apply }

<a id="step-1-protect-the-app-using-the-cli"></a>
### 1단계: CLI로 앱 보호 { #step-1-protect-the-app-using-the-cli }

`appguard-cli`로 APK/AAB 파일을 보호합니다.

→ [2.1 CLI를 이용한 보호작업]({{ cli_page }})

<a id="step-2-configure-app-attestation-settings-in-the-console"></a>
### 2단계: 콘솔에서 앱 증명 설정 { #step-2-configure-app-attestation-settings-in-the-console }

웹 콘솔에서 앱의 서명 정보를 등록하고 앱 증명 옵션을 설정합니다.

→ [6.2 콘솔 앱 증명 설정](console.md)

<a id="step-3-use-app-attestation"></a>
### 3단계: 앱 증명 사용 { #step-3-use-app-attestation }

앱 코드에서 SDK를 이용하여 앱 증명 토큰을 발급 받습니다.

→ [6.3 앱 증명 사용법](sdk.md)

<a id="step-4-verify-the-token-on-the-server"></a>
### 4단계: 서버에서 토큰 검증 { #step-4-verify-the-token-on-the-server }

발급 받은 토큰을 서버로 전달하고, 서버에서 NHN AppGuard 토큰 검증 API를 호출하여 앱 증명 결과를 확인합니다.

---

