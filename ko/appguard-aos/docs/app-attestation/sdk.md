<!-- pre-align:aligned sig=fb5d29087d9e -->

# 앱 증명 사용법

<a id="overview"></a>
## 개요 { #overview }

앱 증명을 앱에서 사용하려면 앱 증명 SDK를 연동해야 합니다. SDK는 NHN AppGuard AAR 파일에 포함되어 있으며, 동기(Sync) 및 비동기(Async) 방식의 증명 API를 제공합니다.

- **최소 AppGuard SDK 버전**: 0.5.0 이상

<a id="add-dependency"></a>
## 의존성 추가 { #add-dependency }

앱 증명 SDK는 NHN AppGuard AAR 파일에 포함되어 있습니다. AAR 파일의 프로젝트 추가 및 의존성 설정은 [4.2 Java SDK 연동](../sdk/java.md#라이브러리-가져오기)을 참고하세요.

<a id="synchronous-authentication-sync"></a>
## 동기 증명(Sync) { #synchronous-authentication-sync }

`authenticate()` 메서드를 호출하면 증명이 완료될 때까지 호출 스레드를 블로킹합니다. 네트워크 통신을 포함하므로 메인(UI) 스레드에서 호출하면 안 됩니다.

<a id="synchronous-authentication-sync-java"></a>
#### Java

```java
import com.nhnent.appguard.appattestation.AppAttestation;
import com.nhnent.appguard.appattestation.AppAttestationTokenResult;

AppAttestation appAttestation = new AppAttestation();
AppAttestationTokenResult result = appAttestation.authenticate(context);

if (result.isSuccess()) {
    AppAttestationTokenResult.Success success = result.asSuccess();
    String token = success.getToken();
    String appId = success.getAppId();
    // token과 appId를 서버로 전달
} else {
    AppAttestationTokenResult.Error error = result.asError();
    int errorCode = error.getErrorCode();
    String errorMessage = error.getErrorMessage();
    // 에러 처리
}
```

<a id="synchronous-authentication-sync-kotlin"></a>
#### Kotlin

```kotlin
import com.nhnent.appguard.appattestation.AppAttestation
import com.nhnent.appguard.appattestation.AppAttestationTokenResult

val appAttestation = AppAttestation()
val result = appAttestation.authenticate(context)

when (result) {
    is AppAttestationTokenResult.Success -> {
        val token = result.token
        val appId = result.appId
        // token과 appId를 서버로 전달
    }
    is AppAttestationTokenResult.Error -> {
        val errorCode = result.errorCode
        val errorMessage = result.errorMessage
        // 에러 처리
    }
}
```

증명에 성공하면 `token`과 `appId`를 서버로 전달합니다. 서버는 이 값으로 NHN AppGuard 토큰 검증 API를 호출하여 앱 증명 결과를 확인합니다.

<a id="asynchronous-authentication-async"></a>
## 비동기 증명(Async) { #asynchronous-authentication-async }

콜백을 전달하면 별도 스레드에서 증명을 수행하고, 완료 시 콜백을 호출합니다. 콜백은 백그라운드 스레드에서 실행되므로, UI 업데이트가 필요하면 `runOnUiThread()`로 전환해야 합니다.

<a id="asynchronous-authentication-async-java"></a>
#### Java

```java
AppAttestation appAttestation = new AppAttestation();
appAttestation.authenticate(context, new AppAttestationTokenListener() {
    @Override
    public void onAppAttestationTokenReceived(AppAttestationTokenResult result) {
        if (result.isSuccess()) {
            AppAttestationTokenResult.Success success = result.asSuccess();
            String token = success.getToken();
            String appId = success.getAppId();
            // token과 appId를 서버로 전달
        } else {
            AppAttestationTokenResult.Error error = result.asError();
            int errorCode = error.getErrorCode();
            String errorMessage = error.getErrorMessage();
            // 에러 처리
        }
    }
});
```

<a id="asynchronous-authentication-async-kotlin"></a>
#### Kotlin

```kotlin
val appAttestation = AppAttestation()
appAttestation.authenticate(context) { result ->
    when (result) {
        is AppAttestationTokenResult.Success -> {
            val token = result.token
            val appId = result.appId
            // token과 appId를 서버로 전달
        }
        is AppAttestationTokenResult.Error -> {
            val errorCode = result.errorCode
            val errorMessage = result.errorMessage
            // 에러 처리
        }
    }
}
```

<a id="api-reference"></a>
## API 레퍼런스 { #api-reference }

앱 증명 API는 `com.nhnent.appguard.appattestation` 패키지에 포함되어 있습니다.

<a id="appattestation"></a>
### AppAttestation { #appattestation }

앱 증명을 수행하는 메인 클래스입니다. 별도의 초기화 없이 인스턴스를 생성하여 바로 사용할 수 있습니다.

<a id="appattestation-authenticate-sync"></a>
#### authenticate(동기)

```java
public AppAttestationTokenResult authenticate(Context context)
```

동기적으로 앱 증명을 수행합니다.

- **매개변수**: `context` — 애플리케이션 컨텍스트
- **반환값**: `AppAttestationTokenResult` — 검증 결과 (`Success` 또는 `Error`)

!!! warning
    블로킹 작업이므로 메인(UI) 스레드에서 호출하면 안 됩니다.

<a id="appattestation-authenticate-async"></a>
#### authenticate(비동기)

```java
public void authenticate(Context context, AppAttestationTokenListener callback)
```

백그라운드 스레드에서 비동기적으로 앱 증명을 수행하고, 콜백으로 결과를 전달합니다.

- **매개변수**:
    - `context` — 애플리케이션 컨텍스트
    - `callback` — 검증 결과를 받을 콜백 (`AppAttestationTokenListener`)

!!! warning
    콜백은 백그라운드 스레드에서 실행됩니다. UI 업데이트가 필요하면 `runOnUiThread()`로 전환해야 합니다.

<a id="appattestationtokenresult"></a>
### AppAttestationTokenResult { #appattestationtokenresult }

`authenticate()` 호출 결과를 담는 클래스입니다. 성공 시 `Success`, 실패 시 `Error`를 반환합니다.

<a id="appattestationtokenresult-issuccess-iserror"></a>
#### isSuccess / isError

```java
public boolean isSuccess()
public boolean isError()
```

증명 성공/실패 여부를 반환합니다.

<a id="appattestationtokenresult-assuccess-aserror"></a>
#### asSuccess / asError

```java
public AppAttestationTokenResult.Success asSuccess()
public AppAttestationTokenResult.Error asError()
```

각각 `Success`, `Error` 객체로 캐스팅합니다.

<a id="appattestationtokenresultsuccess"></a>
### AppAttestationTokenResult.Success { #appattestationtokenresultsuccess }

증명 성공 시의 결과를 담는 클래스입니다.

<a id="appattestationtokenresultsuccess-gettoken"></a>
#### getToken

```java
public String getToken()
```

앱 증명 JWT 토큰을 반환합니다. 이 토큰을 서버로 전달하여 검증합니다.

<a id="appattestationtokenresultsuccess-getappid"></a>
#### getAppId

```java
public String getAppId()
```

앱 식별자를 반환합니다.

<a id="appattestationtokenresulterror"></a>
### AppAttestationTokenResult.Error { #appattestationtokenresulterror }

증명 실패 시의 에러 정보를 담는 클래스입니다.

<a id="appattestationtokenresulterror-geterrorcode"></a>
#### getErrorCode

```java
public int getErrorCode()
```

에러 코드를 반환합니다. 에러 코드 목록은 [에러 코드](#error-codes)를 참고하시기 바랍니다.

<a id="appattestationtokenresulterror-geterrormessage"></a>
#### getErrorMessage

```java
public String getErrorMessage()
```

에러 메시지를 반환합니다.

<a id="appattestationtokenlistener"></a>
### AppAttestationTokenListener { #appattestationtokenlistener }

비동기 증명 결과를 받기 위한 콜백 인터페이스입니다.

<a id="appattestationtokenlistener-onappattestationtokenreceived"></a>
#### onAppAttestationTokenReceived

```java
void onAppAttestationTokenReceived(AppAttestationTokenResult result)
```

비동기 증명이 완료되면 호출됩니다.

- **매개변수**: `result` — 검증 결과 (`AppAttestationTokenResult`)

<a id="error-codes"></a>
## 에러 코드 { #error-codes }

SDK의 `getErrorCode()`로 반환되는 에러 코드입니다. 에러 코드는 대역별로 분류됩니다.

| 에러 코드 대역 | 분류 | 설명 |
|---------------|------|------|
| 100000~199999 | 앱 증명 실패 | 앱 증명에 실패했습니다. |
| 200000~299999 | 네트워크 에러 | 네트워크 연결을 확인하고 재시도하시기 바랍니다. |
| 300000~399999 | 내부 에러 | 에러 코드와 메시지를 기록하여 문의하시기 바랍니다. |
| 400000~499999 | 보호 미적용 | CLI 보호 시 `--app-attestation` 옵션이 필요합니다. |

앱 증명에 실패하면 `getErrorCode()`는 `100000(INTEGRITY_FAILED)`을 반환하며, `getErrorMessage()`에 서버 결과 코드가 포함됩니다. (예: `Integrity Failed : 4000076`)

<a id="relationship-with-the-existing-appguard-sdk"></a>
## 기존 NHN AppGuard SDK와의 관계 { #relationship-with-the-existing-appguard-sdk }

기존 NHN AppGuard SDK([3. SDK 연동 가이드](../sdk/overview-onprem.md))를 이미 사용 중이라면, 기존 코드를 변경할 필요 없이 앱 증명 API를 추가로 호출하면 됩니다. 두 SDK는 동일한 AAR에 포함되어 있지만 독립적으로 동작합니다.

<a id="important-notes"></a>
## 주의사항 { #important-notes }

1. **네트워크 연결 필수**: 앱 증명은 서버와 통신하므로 네트워크 연결이 필요합니다.
2. **스레드 안전성**: `AppAttestation` 객체는 스레드 안전(Thread-safe)하게 설계되어 있으며, 여러 스레드에서 동시에 사용할 수 있습니다.
3. **`--app-attestation` 옵션 필수**: CLI 보호 시 `--app-attestation` 옵션 없이 보호된 앱에서 증명을 시도하면 `NOT_PROTECTED(400000)` 에러가 발생합니다.
4. **ProGuard 설정 불필요**: AAR에 `consumer-rules.pro`가 포함되어 있어, ProGuard/R8 규칙이 자동 적용됩니다.

---

