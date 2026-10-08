<!-- pre-align:aligned sig=05296d704911 -->

<a id="options"></a>
## オプション { #options }

**Security > Network Firewall > コンソール使用ガイド > オプション**

**オプション**タブでは、Network Firewallの運用に必要なオプションを設定できます。

<br>

<a id="configure-logs"></a>
## ログの設定 { #configure-logs }

<a id="default-block-policy-log-settings"></a>
### デフォルト遮断ポリシーのログ設定 { #default-block-policy-log-settings }

* Network Firewallの作成後に必須で作成される、デフォルト遮断ポリシーログの保存の有無を選択します。
    * 使用を選択した場合、デフォルト遮断ポリシーによって生成されたログはトラフィックログで検索可能になります。

<a id="log-remote-transfer-setting"></a>
### ログの遠隔送信設定 { #log-remote-transfer-setting }

* 遠隔地にトラフィックログを保存できるオプションを選択します。
    * Syslog: 最大2つの遠隔地アドレスにログを送信
        * 2つの遠隔地は個別に設定可能(IPアドレス、プロトコル、ポート番号)
    * Object Storage: NHN Cloudで提供するObject Storageサービスへログを送信
    <img src="../../../static/images/24.11.07/OBS_5.png" height="65%" />
        * アクセスキー / シークレットキー: Object StorageサービスでS3 API認証情報の登録時に確認可能なアクセスキー情報を入力
        * バケット名: Object Storageサービスで作成したコンテナの名称を入力
        * エンドポイント: リージョンごとのエンドポイントを確認し、位置に合わせてエンドポイントを入力
        * リージョン: リージョンごとの名称を確認し、リージョンの位置に合わせて名称を入力
    * Log & Crash Search: NHN Cloudで提供するLog & Crash Searchサービスへログを送信
    <img src="../../../static/images/24.11.07/LNCS_2.png" height="65%" />
        * AppKey: Log & Crash Searchサービスを有効化した後に生成されたAppKeyを入力

!!! tip "ポイント"

    * Object Storage設定時、[ユーザーガイド](/Storage/Object%20Storage/ja/s3-api-guide/#aws-sdk)を参考にして入力してください。
    * Log & Crash Searchサービスを使用する場合、ログアラーム設定機能を活用して異常な振る舞いを検知できます。
    例えば、Network Firewallに特定の宛先に向かうSSH通信に対するACL遮断ポリシーを追加した後、該当するポリシーから発生するログに対するアラーム条件を設定します。(例: 1分間にSSH接続の試行ログが20回以上発生)
    ユーザーが設定した条件を満たした場合、アラームを受信できます。  

<br>

<a id="configure-general-settings"></a>
## 一般設定 { #configure-general-settings }

<a id="mirroring-settings"></a>
### ミラーリング設定 { #mirroring-settings }

* Network Firewallで提供する機能のうち、ミラーリングの使用の有無を選択できます。
    * 使用を選択した場合、必要なサブネットにはNetwork Firewallの作成時に使用したサブネットを使用します。

<a id="configure-network-firewall"></a>
### Network Firewall構成 { #configure-network-firewall }

* 単一または冗長化から、Network Firewallの構成方式を設定できます。

<a id="delete-network-firewall"></a>
### Network Firewallの削除 { #delete-network-firewall }

* 運用中のNetwork Firewallを削除できます。
    * Network Firewallは韓国(パンギョ)リージョンと韓国(ピョンチョン)リージョンでそれぞれ削除できます。

!!! tip "ポイント"

    * ACL設定に必要なミラーリングインターフェースのIP情報は、**Network > Network Interface**で確認可能です。
        * インターフェース名: NetworkFirewall_INF_MIRRORING_S_NAT_VIP
    * 構成方式の変更時は数分程度の時間がかかり、構成変更が完了するまでサービスに影響を及ぼす可能性があります。
    * ポリシーやNATなど、Network Firewallの変更作業は構成方式の変更が完了した後に進めることを推奨します。

!!! danger "注意"

    運用中のNetwork Firewallを削除する場合、Network Firewallと接続されている他のサービスを考慮して進めてください。  
    
<br>

<a id="disable-network-firewall-service"></a>
## Network Firewallサービスの無効化 { #disable-network-firewall-service }

**プロジェクト管理 > ご利用中のサービス**からNetwork Firewallサービスを無効化できます。

!!! tip "ポイント"

    * Network Firewallサービスの無効化は、韓国(パンギョ)リージョンと韓国(ピョンチョン)リージョンの両方に適用されます。
    例えば、同一プロジェクトの韓国(パンギョ)リージョンと韓国(ピョンチョン)リージョンの両方でNetwork Firewallサービスを有効化した場合、2つのリージョンのうち片方のNetwork Firewallサービスのみを無効化することはできません。
    * 無効化するには、韓国(パンギョ)リージョンと韓国(ピョンチョン)リージョンでそれぞれNetwork Firewallを削除してから進めてください。
