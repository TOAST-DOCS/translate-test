<!-- pre-align:aligned sig=a867bdc4fe63 -->

# 設定

**セキュリティ > Cloud Access > コンソール使用ガイド > 設定**

**設定**タブでは、Cloud Accessの運用に必要な各種設定を行うことができます。

<br>

<a id="log-settings"></a>
## ログ設定 { #log-settings }

<a id="default-deny-policy-log-settings"></a>
### デフォルト拒否ポリシーのログ設定 { #default-deny-policy-log-settings }

Cloud Accessサービスを有効にすると、**ポリシー > ACLポリシー**タブに default-deny ポリシーが表示されます。**使用**に設定すると、そのポリシーに一致するトラフィックのログが保存されます。

<a id="remote-log-transfer-settings"></a>
### リモートログ転送設定 { #remote-log-transfer-settings }

Cloud Accessの運用中に生成されたトラフィックログをSyslog、Object Storage、Log & Crash Searchを利用してリモートに自動転送し、長期保管が可能です。

* Syslog：最大2つのIPアドレスを設定し、トラフィックログを送信します。

![syslog.PNG](../../static/images/2025.06.24/syslog.png)

* Object Storage：NHN Cloudが提供するObject Storageサービスへログを送信します。

![OBS.PNG](../../static/images/2025.06.24/OBS.png)

* Log & Crash Search：NHN Cloudが提供するLog & Crash Searchサービスへログを送信します。

![LNCS.PNG](../../static/images/2025.06.24/LNCS.png)

<br>

!!! tip "ポイント"
    * Syslogは単一のIPアドレスのみ設定可能で、IP範囲やCIDRはサポートされていません。
    *  Object StorageおよびLog & Crash Searchにログを転送するには、事前にサービスを有効化しておく必要があります。
    * Object Storage設定に必要な入力情報は [Object Storage ユーザーガイド](/Storage/Object%20Storage/ja/s3-api-guide/#aws-sdk)を参照してください。

<br>

<a id="general-settings"></a>
## 一般設定 { #general-settings }

<a id="connection-settings"></a>
### 接続設定 { #connection-settings }

* Cloud Accessサービスの有効化時に入力した情報を確認できます。顧客名とアルゴリズムは変更可能です。
    * サポートされているアルゴリズム：AES-256、ChaCha20

<a id="login-security-settings"></a>
### ログインセキュリティ設定 { #login-security-settings }

* ログイン失敗回数、パスワード有効期間、パスワードポリシーを設定します。
    * ログイン失敗：ログイン失敗を許可する最大回数（1～5回）
    * パスワード有効期間：アカウント作成後、パスワードの有効期間（1～180日）
    * パスワードポリシー：エージェントを使用するユーザーのパスワードルールを設定します
        * 一部の必須ポリシーは設定に関係なく常に適用されます。

<a id="notice-settings"></a>
### ガイダンス設定 { #notice-settings }

* ユーザーがエージェントを通じて認証を行う際に表示する案内メッセージを設定できます。
    * 最大200文字まで入力可能です。

<a id="logo-settings"></a>
### ロゴ設定 { #logo-settings }

* 法人ロゴなど指定条件に合った画像をアップロードし、ログイン画面にロゴを表示できます。

<br>

!!! tip "ポイント"
    * 接続設定項目のうち、ドメイン、顧客キー、シークレットキーは、エージェントで接続追加時に使用する情報です。外部流出に注意してください。
    * ログイン失敗やパスワードの有効期限切れでアカウントがロックされた場合、Cloud Accessの権限を持つNHN Cloudコンソール管理者に問い合わせてください。
    * ガイダンスメッセージはログイン後もトレイアイコンから確認可能です。

!!! danger "注意"
    ログインセキュリティ設定は、Cloud Accessエージェントを使用する全ユーザーに共通で適用されます。設定時にはご注意ください。