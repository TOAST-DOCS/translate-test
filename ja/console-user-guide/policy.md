<!-- pre-align:aligned sig=9132502e0f26 -->

<a id="policy"></a>
## ポリシー { #policy }

**Security > Network Firewall > コンソール使用ガイド > ポリシー**

**ポリシー**タブでは、Network Firewallと接続されたVPC間のトラフィックとインバウンド/アウトバウンドトラフィックを制御できる**ACL**と、Network Firewallを経由する通信の経路を指定できる**ルート**機能を使用できます。

<br>

<a id="configure-acl"></a>
## ACLの設定 { #configure-acl }

<a id="add"></a>
### 追加 { #add }

* 送信元、宛先、宛先ポートに基づいてポリシーを追加できます。
    * すでに作成されているオブジェクトを通じて、送信元、宛先、宛先ポートを選択します。
* ポリシーの状態(有効化/無効化)とアクション(許可/遮断)、スケジュールの設定、及びポリシー別ロギングの有無などのオプションを設定してポリシーを追加できます。
* スケジュール機能はポリシーの状態を有効化した後に動作します(ポリシーが無効になっている場合、スケジュール機能は適用されません)。

![policy2.PNG](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/3.policy/policy2.png)

<a id="copy"></a>
### コピー { #copy }

* **コピー**をクリックしてポリシーをコピーできます。
    * コピー: コピーしたいポリシーと同じポリシーをコピー
    * 逆方向コピー: コピーしたいポリシーの送信元と宛先を変更してコピー
    ![policy3.PNG](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/3.policy/policy3.png)
    
<a id="modify"></a>
### 修正 { #modify }

* **修正**をクリックしてポリシーを修正できます。

<a id="move"></a>
### 移動 { #move }

* **移動**をクリックしてポリシーを移動できます。
    * default-denyポリシーの下へは移動できません。
    ![policy4.PNG](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/3.policy/policy4.png)

<a id="delete"></a>
### 削除 { #delete }

* **削除**をクリックしてポリシーを削除できます。

<a id="batch-download-of-policies"></a>
### ポリシー一括ダウンロード { #batch-download-of-policies }

* ポリシータブに作成されているポリシー全体を一度にダウンロードできます。

<a id="batch-register-policies"></a>
### ポリシー一括登録 { #batch-register-policies }

* ダウンロードしたテンプレートを使用して、ポリシーを一度に登録できます。

![policy5.PNG](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/3.policy/policy5.png)

!!! tip "ポイント"

    コピーされたポリシーは無効化されます。使用が必要な場合は、**修正**をクリックしてポリシーを有効化してから使用してください。


!!! danger "注意"
    一度削除したポリシーは復元できず、default-denyポリシーは削除できません。

<br>

<a id="configure-routing"></a>
## ルートの設定 { #configure-routing }

<a id="configure-routing-add"></a>
### 追加 { #configure-routing-add }

* **追加**をクリックしてイーサネットを選択し、宛先とゲートウェイを入力します。 
    * 宛先: サブネット形式で入力
    * イーサネット: プルダウンリストに表示されるイーサネットを選択
    * ゲートウェイ: ホスト形式で入力
  
<a id="configure-routing-modify"></a>
### 修正 { #configure-routing-modify }

* **修正**をクリックしてルートを修正できます。

<a id="configure-routing-delete"></a>
### 削除 { #configure-routing-delete }

* **削除**をクリックしてルートを削除できます。

!!! tip "ポイント"

    * イーサネットをVPNとして選択する場合、ゲートウェイは指定しなくても構いません。
    * IPSec VPNと連携されたプライベートIP範囲に対するルート設定は、必ずイーサネットをVPNに設定してください。
    * 宛先サブネット入力時、以下のようなバリデーションメッセージが表示される場合、サブネットの範囲を事前に確認してサブネットの開始IPとして入力してください。
        * [例]
            * 192.168.199.0/21 (X) → 192.168.192.0/21 (O)
            * 172.16.100.0/20 (X) → 172.16.96.0/20 (O)
            * 10.10.10.130/25 (X) → 10.10.10.128/25 (O)
            ![route_add.PNG](../../static/images/24.09.12/route_add.png)

!!! danger "注意"

    * Network FirewallのデフォルトゲートウェイはNATイーサネットであり、修正または削除できません。
    * ルート設定が変更された場合、通信に問題が発生する可能性があるため、留意して設定してください。 
