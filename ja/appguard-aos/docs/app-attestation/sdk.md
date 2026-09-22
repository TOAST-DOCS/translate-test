<!-- machine_translated: true -->

<!-- pre-align:aligned sig=fb5d29087d9e -->

# アプリ証明の使用方法

<a id="overview"></a>
## 概要 { #overview }

アプリ証明をアプリで使用するには、アプリ証明SDKを連携する必要があります。SDKはAppGuard AARファイルに含まれており、同期(Sync)及び非同期(Async)方式の証明APIを提供します。

- **最小AppGuard SDKバージョン**：0.5.0以上

<a id="add-dependency"></a>
## 依存関係の追加 { #add-dependency }

アプリ証明SDKは、NHN AppGuard AARファイルに含まれています。AARファイルのプロジェクト追加及び依存関係の設定は、[4.2 Java SDK連携](../sdk/java.md#ライブラリのインポート)をご参照ください。

<a id="synchronous-authentication-sync"></a>
## 同期証明 (Sync) { #synchronous-authentication-sync }

`authenticate()`メソッドを呼び出すと、証明が完了するまで呼び出し元のスレッドをブロックします。ネットワーク通信を含むため、**メイン(UI)スレッドでは呼び出さないでください。**

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
    // tokenとappIdをサーバーへ送信
} else {
    AppAttestationTokenResult.Error error = result.asError();
    int errorCode = error.getErrorCode();
    String errorMessage = error.getErrorMessage();
    // エラー処理
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
        // tokenとappIdをサーバーへ送信
    }
    is AppAttestationTokenResult.Error -> {
        val errorCode = result.errorCode
        val errorMessage = result.errorMessage
        // エラー処理
    }
}
```

証明に成功すると、`token`と`appId`をサーバーへ送信します。サーバーはこの値を使用してAppGuardトークン検証APIを呼び出し、アプリ証明の結果を確認します。

<a id="asynchronous-authentication-async"></a>
## 非同期証明 (Async) { #asynchronous-authentication-async }

コールバックを指定すると別スレッドで証明を実行し、完了時にコールバックを呼び出します。コールバックは**バックグラウンドスレッドで実行**されるため、UIの更新が必要な場合は`runOnUiThread()`に切り替える必要があります。

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
            // tokenとappIdをサーバーへ送信
        } else {
            AppAttestationTokenResult.Error error = result.asError();
            int errorCode = error.getErrorCode();
            String errorMessage = error.getErrorMessage();
            // エラー処理
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
            // tokenとappIdをサーバーへ送信
        }
        is AppAttestationTokenResult.Error -> {
            val errorCode = result.errorCode
            val errorMessage = result.errorMessage
            // エラー処理
        }
    }
}
```

<a id="api-reference"></a>
## APIリファレンス { #api-reference }

アプリ証明APIは、`com.nhnent.appguard.appattestation`パッケージに含まれています。

<a id="appattestation"></a>
### AppAttestation { #appattestation }

アプリ証明を実行するメインクラスです。別途初期化することなくインスタンスを作成してすぐに使用できます。

<a id="appattestation-authenticate-sync"></a>
#### authenticate (同期)

```java
public AppAttestationTokenResult authenticate(Context context)
```

同期的にアプリ証明を実行します。

- **パラメータ**：`context` — アプリケーションコンテキスト
- **戻り値**：`AppAttestationTokenResult` — 検証結果 (`Success`または`Error`)

!!! warning
    ブロッキング処理であるため、メイン(UI)スレッドでは呼び出さないでください。

<a id="appattestation-authenticate-async"></a>
#### authenticate (非同期)

```java
public void authenticate(Context context, AppAttestationTokenListener callback)
```

バックグラウンドスレッドで非同期的にアプリ証明を実行し、コールバックで結果を返します。

- **パラメータ**：
    - `context` — アプリケーションコンテキスト
    - `callback` — 検証結果を受け取るコールバック (`AppAttestationTokenListener`)

!!! warning
    コールバックはバックグラウンドスレッドで実行されます。UIの更新が必要な場合は`runOnUiThread()`に切り替える必要があります。

<a id="appattestationtokenresult"></a>
### AppAttestationTokenResult { #appattestationtokenresult }

`authenticate()`の呼び出し結果を格納するクラスです。成功時は`Success`、失敗時は`Error`を返します。

<a id="appattestationtokenresult-issuccess-iserror"></a>
#### isSuccess / isError

```java
public boolean isSuccess()
public boolean isError()
```

証明の成否を返します。

<a id="appattestationtokenresult-assuccess-aserror"></a>
#### asSuccess / asError

```java
public AppAttestationTokenResult.Success asSuccess()
public AppAttestationTokenResult.Error asError()
```

それぞれ`Success`、`Error`オブジェクトにキャストします。

<a id="appattestationtokenresultsuccess"></a>
### AppAttestationTokenResult.Success { #appattestationtokenresultsuccess }

証明成功時の結果を格納するクラスです。

<a id="appattestationtokenresultsuccess-gettoken"></a>
#### getToken

```java
public String getToken()
```

アプリ証明のJWTトークンを返します。このトークンをサーバーへ送信して検証します。

<a id="appattestationtokenresultsuccess-getappid"></a>
#### getAppId

```java
public String getAppId()
```

アプリ識別子を返します。

<a id="appattestationtokenresulterror"></a>
### AppAttestationTokenResult.Error { #appattestationtokenresulterror }

証明失敗時のエラー情報を格納するクラスです。

<a id="appattestationtokenresulterror-geterrorcode"></a>
#### getErrorCode

```java
public int getErrorCode()
```

エラーコードを返します。エラーコードの一覧は[エラーコード](#error-codes)をご参照ください。

<a id="appattestationtokenresulterror-geterrormessage"></a>
#### getErrorMessage

```java
public String getErrorMessage()
```

エラーメッセージを返します。

<a id="appattestationtokenlistener"></a>
### AppAttestationTokenListener { #appattestationtokenlistener }

非同期証明の結果を受け取るためのコールバックインターフェースです。

<a id="appattestationtokenlistener-onappattestationtokenreceived"></a>
#### onAppAttestationTokenReceived

```java
void onAppAttestationTokenReceived(AppAttestationTokenResult result)
```

非同期証明が完了すると呼び出されます。

- **パラメータ**：`result` — 検証結果 (`AppAttestationTokenResult`)

<a id="error-codes"></a>
## エラーコード { #error-codes }

SDKの`getErrorCode()`で返されるエラーコードです。エラーコードは帯域別に分類されます。

| エラーコード帯域 | 分類 | 説明 |
|---------------|------|------|
| 100000~199999 | アプリ証明の失敗 | アプリ証明に失敗しました。 |
| 200000~299999 | ネットワークエラー | ネットワーク接続を確認して再試行してください。 |
| 300000~399999 | 内部エラー | エラーコードとメッセージを記録してお問い合わせください。 |
| 400000~499999 | 保護未適用 | CLI保護時に`--app-attestation`オプションが必要です。 |

アプリ証明に失敗すると、`getErrorCode()`は`100000(INTEGRITY_FAILED)`を返し、`getErrorMessage()`にサーバー結果コードが含まれます。(例："Integrity Failed : 4000076")

<a id="relationship-with-the-existing-appguard-sdk"></a>
## 既存AppGuard SDKとの関係 { #relationship-with-the-existing-appguard-sdk }

既存のAppGuard SDK([3. SDK連携ガイド](../sdk/overview-onprem.md))をすでに使用中の場合、既存のコードを変更する必要はなく、アプリ証明APIを追加で呼び出すだけで済みます。2つのSDKは同じAARに含まれていますが、独立して動作します。

<a id="important-notes"></a>
## 注意事項 { #important-notes }

1. **ネットワーク接続必須**：アプリ証明はサーバーと通信するため、ネットワーク接続が必要です。
2. **スレッドセーフ**：`AppAttestation`オブジェクトはスレッドセーフであり、複数のスレッドで同時に使用できます。
3. **`--app-attestation`オプション必須**：CLI保護時に`--app-attestation`オプションなしで保護されたアプリで証明を試みると、`NOT_PROTECTED(400000)`エラーが発生します。
4. **ProGuard設定不要**：AARに`consumer-rules.pro`が含まれているため、ProGuard/R8ルールが自動で適用されます。

---

