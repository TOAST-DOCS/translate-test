<!-- pre-align:aligned sig=dbacc26b661d -->

# アプリ証明ガイド

<a id="overview"></a>
## 概要 { #overview }

NHN AppGuardの**アプリ証明(App Attestation)**は、アプリの改ざんの有無と実行環境の安全性をサーバーで検証し、検証に成功したアプリのみサービスへアクセスできるように制御する機能を提供します。

<a id="how-it-works"></a>
## 動作フロー { #how-it-works }

アプリでアプリ証明をリクエストすると、AppGuardサーバーで検証を実行し、結果をトークンとして発行します。発行されたトークンをサーバーへ送信して検証します。

```mermaid
sequenceDiagram
    participant App as アプリ
    participant AppGuard as AppGuardサーバー
    participant Server as サーバー
    Note over App, Server: トークン発行
    App->>AppGuard: 1. authenticate()
    Note over AppGuard: 整合性検証
    AppGuard-->>App: 2. JWTトークン
    Note over App, Server: トークン検証
    App->>Server: 3. token + appIdを送信
    Server->>AppGuard: 4. トークン検証API呼び出し
    AppGuard-->>Server: 5. 検証結果
    Server-->>App: 6. サービスの許可/拒否
```

<a id="how-to-apply"></a>
## 適用手順 { #how-to-apply }

<a id="step-1-protect-the-app-using-the-cli"></a>
### 1段階：CLIでアプリ保護 { #step-1-protect-the-app-using-the-cli }

`appguard-cli`でAPK/AABファイルを保護します。

→ [2.1 CLIを利用した保護作業]({{ cli_page }})

<a id="step-2-configure-app-attestation-settings-in-the-console"></a>
### 2段階：コンソールでアプリ証明設定 { #step-2-configure-app-attestation-settings-in-the-console }

Webコンソールでアプリの署名情報を登録し、アプリ証明オプションを設定します。

→ [5.2 コンソールアプリ証明設定](console.md)

<a id="step-3-use-app-attestation"></a>
### 3段階：アプリ証明の使用 { #step-3-use-app-attestation }

アプリのコードでSDKを利用してアプリ証明トークンを取得します。

→ [5.3 アプリ証明の使用方法](sdk.md)

<a id="step-4-verify-the-token-on-the-server"></a>
### 4段階：サーバーでトークン検証 { #step-4-verify-the-token-on-the-server }

発行されたトークンをサーバーへ送信し、サーバー側でAppGuardトークン検証APIを呼び出してアプリ証明の結果を確認します。

---

