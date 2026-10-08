<!-- pre-align:aligned sig=7d9aee4cb102 -->

# Cloud Access 開始ガイド

**セキュリティ > Cloud Access > コンソール使用ガイド > Cloud Access開始**

<br>

<a id="console-settings"></a>
## コンソール設定 { #console-settings }

エージェントの準備が完了したら、Cloud Accessサービスを使用するために接続設定とルート設定を行います。

<br>

<a id="save-configuration-information"></a>
### 設定情報の保存 { #save-configuration-information }

接続設定情報を入力して保存します。保存後、Cloud Accessを使用できます。

![setting_1.PNG](../../static/images/2025.06.24/2025.07/setting_1.png)

* VPCとサブネットを選択します。
    * VPCやサブネットがない場合は、NHN Cloudコンソールの**VPC**または**Subnet**メニューから作成してください。
* 顧客名を入力します。
    * 日本語、英語、数字、および一部の記号（-、_、.）が使用可能です。
* アルゴリズムを選択します。
    * AES-256とChaCha20をサポートしています。


!!! danger "注意"
    * 設定情報の保存前に、選択したVPCにインターネットゲートウェイが接続されているか確認してください。
        * インターネットゲートウェイが接続されていない場合、Cloud Accessを使用できません。
    * 設定情報の保存時、Cloud Accessに必要なインターフェース2つと冗長化のためのVIP 1つ、そしてフローティングIP 1つを作成します。作成以降、該当リソースが削除されないように注意してください。
    
<br>

<a id="route-settings"></a>
## ルート設定 { #route-settings }

外部エージェントを使用して接続したユーザーが内部インスタンスにアクセスできるよう、ルートを構成します。

<a id="one-vpc"></a>
### 1つのVPC { #one-vpc }

* ユーザーIP割り当て帯域: 10.0.0.0/24
* VPC: 172.16.0.0/12
* Cloud Access作成時選択したサブネット: 172.16.0.0/24
* アクセス可能帯域: 172.16.100.0/24

上記のように設定されている場合、**Network - Routing**で接続必要なインスタンスが属するルーティングテーブルを選択し、**ルート**タブに以下のようなルールを追加します。

* 宛先CIDR: 10.0.0.0/24
* ゲートウェイ: Virtual_IPタイプのNCAccess_INF_SUB_PORT_VIP

<a id="two-vpcs"></a>
### 2つのVPC { #two-vpcs }

* ユーザーIP割り当て帯域: 10.0.0.0/24
* VPC1: 172.16.0.0/12
* VPC2: 192.168.0.0/16
* Cloud Access作成時に選択したサブネット: 172.16.0.0/24
* アクセス可能帯域: 192.168.0.0/24

上記のように設定されている場合、VPC1(ローカル)とVPC2(ピア)間のピアリングを設定します。そして**Network - Routing**で、接続するインスタンスが属するルーティングテーブルを選択し、**ルート**タブに以下のようなルールを追加します。

* 対象CIDR: 10.0.0.0/24
* ゲートウェイ: VPC1とVPC2の間に作成されたPEERINGタイプのネットワークインターフェース

そして**Peering Gateway - ピアリング**で**ルート**タブを選択し、ローカルルートルールを追加します。

* 対象CIDR: 10.0.0.0/24
* ゲートウェイ: Virtual_IPタイプのNCAccess_INF_SUB_PORT_VIP

<a id="other-projects"></a>
### 他のプロジェクト { #other-projects }

* ユーザーIP割り当て帯域: 10.0.0.0/24
* プロジェクト1のVPC: 172.16.0.0/12
* プロジェクト2のVPC: 192.168.0.0/16
* Cloud Access作成時に選択したサブネット: 172.16.0.0/24
* アクセス可能帯域: 192.168.0.0/24

上記のように設定されている場合、1番プロジェクト(ローカル)と2番プロジェクト(ピア)間のピアリングを設定します。そして**Network - Routing**で、接続するインスタンスが属するルーティングテーブルを選択し、**ルート**タブに以下のようなルールを追加します。

* 対象CIDR: 10.0.0.0/24
* ゲートウェイ: プロジェクト1番のVPCとプロジェクト2番のVPCの間に作成されたPEERINGタイプのネットワークインターフェース

そして**Peering Gateway - プロジェクトピアリング**で**ルート**タブを選択し、ローカルルートルールを追加します。

* 対象CIDR: 10.0.0.0/24
* ゲートウェイ: Virtual_IPタイプのNCAccess_INF_SUB_PORT_VIP

!!! danger "注意"
    * インスタンスに適用されたSecurity Groupsで、ユーザーIP割当帯域を許可することで通信が可能になります。 
    * ユーザーIP割当帯域は、以下の項目と重複できません。 
        * 接続設定時に選択したサブネット
        * アクセス可能なネットワーク範囲
    * インスタンスに2つ以上のサブネットを接続する際、ユーザーIP割当帯域と重複するサブネットを構成する場合、通信が正常に行われません。
    
<br>

<a id="download-the-agent"></a>
## エージェントのダウンロード { #download-the-agent }

Cloud Accessサービスを利用するためのエージェントをダウンロードします。対応OSは以下の通りです。

* Windows 10 1903以上(32bit / 64bit)
* Windows 11(64bit)
* macOS 13.3以上

| OS | バージョン| ダウンロード | 更新日 |
|--------|------|------|------|
| Windows(64bit)|1.2.0|[CloudAccess_Setup_x64](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_04c78c238ba54583bb1036b393ec6ae5/windows/installer/CloudAccess_Setup_x64.exe)|2026. 01. 13.|
| Windows(32bit)|1.2.0|[CloudAccess_Setup_x86](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_04c78c238ba54583bb1036b393ec6ae5/windows/installer/CloudAccess_Setup_x86.exe)|2026. 01. 13.|
|macOS|1.1.1|[CloudAccess_macOS](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_04c78c238ba54583bb1036b393ec6ae5/macos/CloudAccess%20Installer.dmg)|2026. 01. 13.|

!!! tip "ポイント"
    Cloud Accessエージェントは、ユーザー端末とサービス間のセキュリティ接続を通じて、外部環境からでも安全な内部サービスへのアクセスをサポートする専用プログラムです。

<br>

<a id="add-a-connection"></a>
## 接続設定 { #add-a-connection }

<a id="add-connection"></a>
### 接続の追加 { #add-connection }

NHN Cloudリソースに接続するための項目を追加します。

![conncetion_add_1.PNG](../../static/images/2025.06.24/2025.07/add_1.png)

➊ドメイン、➋顧客キー、➌秘密キーをNHN Cloudコンソールの権限を持つ管理者から受け取り、入力します。

<br>

![conncetion_add_3.PNG](../../static/images/2025.06.24/2025.07/add_2.png)
 
➍ 「検証」ボタンをクリックし、検証完了後、➎顧客名が表示されます。その後、**追加**をクリックして接続を完了します。

<a id="delete-connection"></a>
### 接続の削除 { #delete-connection }

接続項目をクリックすると、**接続削除**ボタンが有効になり、追加した接続を削除できます。

<br>

!!! tip "ポイント"
    * 接続追加に必要な値は、NHN Cloudコンソールの権限を持つ管理者から取得してください。
        * 顧客名は検証後、管理者が設定した名前が自動で表示されます。
    * 複数の接続項目を追加可能ですが、有効なのは1つのみです。

<br>

<a id="tunnel-connection-via-authentication"></a>
## 認証によるトンネル接続 { #tunnel-connection-via-authentication }

接続が必要な項目を選択し、**接続**をクリックして認証を行います。

<a id="notice-settings"></a>
### 案内表示 { #notice-settings }

* 管理者が設定した案内メッセージを表示します。
    * **設定 > 案内設定**が**使用しない**の場合は表示されません。

<a id="first-authentication-account-password"></a>
### 第1段階認証（アカウントとパスワード） { #first-authentication-account-password }

![login_1.PNG](../../static/images/2025.06.24/2025.07/6.png)

* アカウント名：管理者から発行されたアカウントを入力します。
* パスワード：メールで届いた初期パスワードを入力します。
* アカウント名の保存: クリックしてログインした後、再ログインする際に直前にログインしたアカウント名を自動で入力して表示します。

<a id="agree-to-collection-and-usage-of-personal-information"></a>
### 個人情報収集・利用同意 { #agree-to-collection-and-usage-of-personal-information }
* Cloud Accessサービス運用のため個人情報を収集します。
    * 拒否した場合はサービス利用が制限されます。

<a id="additional-authentication"></a>
### 追加認証 { #additional-authentication }

* 第1段階完了後、設定された認証ポリシーに従って追加認証を実施します。 
    * サポートする認証方法：
        * メール
        * 携帯電話 
        * TOTP（ワンタイムパスワード） 
        * 生体情報（パスキー） 

<a id="change-initial-password"></a>
### 初期パスワードの変更 { #change-initial-password }

* 初期パスワードを変更します。
    * 管理者が設定したパスワードポリシーに従って変更してください。

<br>

!!! tip "ポイント"
    * NHN Cloudコンソールの権限を持つ管理者がユーザーアカウントを作成すると、登録されたユーザーのメールアドレスに仮パスワードとエージェントのダウンロードリンクが送信されます。
    * アカウント作成後、登録されたメールアドレスに初期パスワードが送信されます。
    * 初回認証時のみ個人情報同意画面が表示され、接続完了で同意されたと見なされます（認証を完了しないと再同意が必要）。
    * 以下のパスワード制約は常に適用されます：
        * 6～30文字以内
        * アカウントIDと同一のパスワードは不可
    * **アカウント名の保存**は、直前にログインしたアカウント名のみを表示し、ログインしていないアカウントは表示しません。
    
<br>

<a id="agent-features"></a>
## エージェントのトレイ機能 { #agent-features }

エージェントのトレイアイコンから利用できる機能です。

<br>

<a id="before-connecting-to-agent"></a>
### 接続前 { #before-connecting-to-agent }
 * 開く：接続画面を表示
 * 接続：接続項目を表示
 * アップデート確認：バージョン確認および更新
 * バージョン情報：ライセンスとプライバシーポリシーを表示
 * 設定：環境設定と言語設定
      * クラウド設定：パブリック or プライベート選択
      * 言語：韓国語、日本語、英語
 * 終了：エージェントを終了

<a id="after-connecting-to-agent"></a>
### 接続後 { #after-connecting-to-agent }
顧客名とアカウント名が表示
* 開く：接続項目表示
* 接続解除：接続解除
* パスワード変更:パスワードを変更します。
* お知らせ：通知内容表示（通知が設定されていない場合もあり）
* バージョン情報：バージョン・ライセンス表示
* 終了：エージェントを終了

<br>

<a id="delete-agent"></a>
## エージェントの削除 { #delete-agent }

エージェントはユーザーがいつでも直接削除できます。

* Windows: 設定 > アプリ > インストールされているアプリ(アプリと機能)でCloud Accessを選択した後、アンインストールをクリックして削除
* macOS: Finder > アプリケーションを選択した後、Cloud Accessをゴミ箱に移動して削除

!!! danger "注意"
    エージェント削除時、Cloud Accessサービスを利用できなくなるか、制限される場合があります。