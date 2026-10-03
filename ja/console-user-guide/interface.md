<!-- pre-align:aligned sig=b90768e8e6c9 -->

<a id="interface"></a>
## インターフェース { #interface }

**Security > Network Firewall > コンソール使用ガイド > インターフェース**

**インターフェース**タブでは、Network Firewallに使用するインターフェースを作成・管理します。

<br>

<a id="configure-interface"></a>
## インターフェースを設定する { #configure-interface }

<a id="add"></a>
### 追加 { #add }
* **追加**をクリックしてインターフェースを追加します。
    * 名前を入力し、VPC、サブネットを選択します。
    ![(interface6)](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/5.interface/interface6.png)

<a id="modify"></a>
### 修正 { #modify }
* **修正**をクリックしてインターフェースを修正できます。
    * VPCとサブネットは修正できません。

<a id="delete"></a>
### 削除 { #delete }
* **削除**をクリックしてインターフェースを削除できます。

<a id="enabledisable"></a>
### 使用設定 { #enabledisable }
* オーバーフローメニューからインターフェースを使用、または未使用に設定できます。
![(interface7)](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/5.interface/interface7.png)

!!! tip "ポイント"

    修正は名前と説明のみ修正可能です。

!!! danger "注意"
    
    * 使用中のインターフェースは削除できません。
        * ACL及びルート設定に該当するインターフェースがなく、インターフェースタブで未使用状態の場合のみ削除可能です。
    * 現在使用中のインターフェースを「未使用」に設定すると、通信に影響を及ぼす可能性があります。
    * 作成されたインターフェース情報は、[Network > Network Interface]で確認できます。
        * Network Firewallで作成したVirtual_IPタイプのインターフェースを変更する場合、未使用状態のインターフェースは使用できなくなり、すでに使用中のインターフェースは通信に影響を及ぼす可能性があります。