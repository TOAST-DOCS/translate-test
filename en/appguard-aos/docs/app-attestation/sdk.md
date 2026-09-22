<!-- machine_translated: true -->

<!-- pre-align:aligned sig=d9789ac3a88a -->

# How to Use App Attestation

<a id="overview"></a>
## Overview { #overview }

To use app attestation in an app, the Integrity SDK must be integrated. The SDK is included in the AppGuard AAR file and provides both synchronous (Sync) and asynchronous (Async) authentication APIs.

- **Minimum AppGuard SDK version**: 0.5.0 or later

<a id="add-dependency"></a>
## Add Dependency { #add-dependency }

The app attestation SDK is included in the NHN AppGuard AAR file. For instructions on adding the AAR file to your project and configuring dependencies, see [4.2 Java SDK Integration](../sdk/java.md#라이브러리-가져오기).

<a id="synchronous-authentication-sync"></a>
## Synchronous Authentication (Sync) { #synchronous-authentication-sync }

Calling the `authenticate()` method blocks the calling thread until authentication is complete. Since it involves network communication, it **must not be called on the main (UI) thread.**

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
    // Transmit token and appId to the server
} else {
    AppAttestationTokenResult.Error error = result.asError();
    int errorCode = error.getErrorCode();
    String errorMessage = error.getErrorMessage();
    // Handle error
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
        // Transmit token and appId to the server
    }
    is AppAttestationTokenResult.Error -> {
        val errorCode = result.errorCode
        val errorMessage = result.errorMessage
        // Handle error
    }
}
```

Upon successful authentication, transmit the `token` and `appId` to the server. The server uses these values to call the AppGuard token verification API and check the integrity result.

<a id="asynchronous-authentication-async"></a>
## Asynchronous Authentication (Async) { #asynchronous-authentication-async }

Pass a callback to perform authentication on a separate thread. The callback is called upon completion. Since the callback **runs on a background thread**, use `runOnUiThread()` to switch to the main thread if UI updates are required.

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
            // Transmit token and appId to the server
        } else {
            AppAttestationTokenResult.Error error = result.asError();
            int errorCode = error.getErrorCode();
            String errorMessage = error.getErrorMessage();
            // Handle error
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
            // Transmit token and appId to the server
        }
        is AppAttestationTokenResult.Error -> {
            val errorCode = result.errorCode
            val errorMessage = result.errorMessage
            // Handle error
        }
    }
}
```

<a id="api-reference"></a>
## API Reference { #api-reference }

The app attestation API is included in the `com.nhnent.appguard.appattestation` package.

<a id="appattestation"></a>
### AppAttestation { #appattestation }

The main class that performs app attestation. An instance can be created and used immediately without separate initialization.

<a id="appattestation-authenticate-sync"></a>
#### authenticate (Sync)

```java
public AppAttestationTokenResult authenticate(Context context)
```

Performs app attestation synchronously.

- **Parameter**: `context` — Application context
- **Return value**: `AppAttestationTokenResult` — Verification result (`Success` or `Error`)

!!! warning
    This is a blocking operation and must not be called on the main (UI) thread.

<a id="appattestation-authenticate-async"></a>
#### authenticate (Async)

```java
public void authenticate(Context context, AppAttestationTokenListener callback)
```

Performs app attestation asynchronously on a background thread and delivers the result via callback.

- **Parameters**:
    - `context` — Application context
    - `callback` — Callback to receive the verification result (`AppAttestationTokenListener`)

!!! warning
    The callback runs on a background thread. Use `runOnUiThread()` to switch to the main thread if UI updates are required.

<a id="appattestationtokenresult"></a>
### AppAttestationTokenResult { #appattestationtokenresult }

The class that holds the result of an `authenticate()` call. Returns `Success` on success and `Error` on failure.

<a id="appattestationtokenresult-issuccess-iserror"></a>
#### isSuccess / isError

```java
public boolean isSuccess()
public boolean isError()
```

Returns whether authentication succeeded or failed.

<a id="appattestationtokenresult-assuccess-aserror"></a>
#### asSuccess / asError

```java
public AppAttestationTokenResult.Success asSuccess()
public AppAttestationTokenResult.Error asError()
```

Casts to the `Success` or `Error` object, respectively.

<a id="appattestationtokenresultsuccess"></a>
### AppAttestationTokenResult.Success { #appattestationtokenresultsuccess }

The class that holds the result of a successful authentication.

<a id="appattestationtokenresultsuccess-gettoken"></a>
#### getToken

```java
public String getToken()
```

Returns the app attestation JWT token. Transmit this token to the server for verification.

<a id="appattestationtokenresultsuccess-getappid"></a>
#### getAppId

```java
public String getAppId()
```

Returns the app identifier.

<a id="appattestationtokenresulterror"></a>
### AppAttestationTokenResult.Error { #appattestationtokenresulterror }

The class that holds error information for a failed authentication.

<a id="appattestationtokenresulterror-geterrorcode"></a>
#### getErrorCode

```java
public int getErrorCode()
```

Returns the error code. For a list of error codes, see [Error Codes](#error-codes).

<a id="appattestationtokenresulterror-geterrormessage"></a>
#### getErrorMessage

```java
public String getErrorMessage()
```

Returns the error message.

<a id="appattestationtokenlistener"></a>
### AppAttestationTokenListener { #appattestationtokenlistener }

A callback interface for receiving asynchronous authentication results.

<a id="appattestationtokenlistener-onappattestationtokenreceived"></a>
#### onAppAttestationTokenReceived

```java
void onAppAttestationTokenReceived(AppAttestationTokenResult result)
```

Called when asynchronous authentication is complete.

- **Parameter**: `result` — Verification result (`AppAttestationTokenResult`)

<a id="error-codes"></a>
## Error Codes { #error-codes }

Error codes returned by `getErrorCode()` in the SDK. Error codes are classified by range.

| Error Code Range | Category | Description |
|---------------|------|------|
| 100000–199999 | App attestation failure | App attestation of the app failed. |
| 200000–299999 | Network error | Check the network connection and try again. |
| 300000–399999 | Internal error | Record the error code and message, and contact us. |
| 400000–499999 | Protection not applied | The `--integrity` option is required when protecting with the CLI. |

If app attestation fails, `getErrorCode()` returns `100000 (INTEGRITY_FAILED)`, and `getErrorMessage()` contains the server result code. (e.g., "Integrity Failed : 4000076")

<a id="relationship-with-the-existing-appguard-sdk"></a>
## Relationship with the Existing AppGuard SDK { #relationship-with-the-existing-appguard-sdk }

If you are already using the existing AppGuard SDK ([3. SDK Integration Guide](../sdk/overview-onprem.md)), you can call the app attestation API in addition to the existing code without any changes. Both SDKs are included in the same AAR but operate independently.

<a id="important-notes"></a>
## Important Notes { #important-notes }

1. **Network connection required**: App attestation requires a network connection as it communicates with the server.
2. **Thread safety**: The `AppAttestation` object is thread-safe and can be used simultaneously from multiple threads.
3. **`--integrity` option required**: If authentication is attempted on an app protected without the `--integrity` option during CLI protection, a `NOT_PROTECTED (400000)` error will occur.
4. **No ProGuard configuration required**: Since `consumer-rules.pro` is included in the AAR, ProGuard/R8 rules are applied automatically.

---

