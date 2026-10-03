<!-- pre-align:aligned sig=61dff5f1b687 -->

<a id="object"></a>
## オブジェクト { #object }

**Security > Network Firewall > コンソール使用ガイド > オブジェクト**

**オブジェクト**タブでは、ポリシーを作成する際に使用するIP、ポートを作成及び管理します。

<br>

<a id="configure-objects"></a>
## オブジェクトの設定 { #configure-objects }

<a id="add"></a>
### 追加 { #add }

* 必須項目を入力してオブジェクトを作成します。
    * オブジェクトは、IPとポートの2つの形式で追加できます。
    ![(object2)](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/4.object/object2.png)

<a id="modify"></a>
### 修正 { #modify }

* **修正**をクリックしてオブジェクトを修正できます。
    * タイプは修正できません。

<a id="delete"></a>
### 削除 { #delete }

* **削除**をクリックしてオブジェクトを削除できます。
    * Network Firewallで自動作成されたオブジェクトは、修正や削除ができません。

<a id="add-instance-object"></a>
### インスタンスオブジェクトの追加 { #add-instance-object }
* Network Firewallが作成されたプロジェクト内にあるインスタンスを活用してオブジェクトを追加できます。
![(object3)](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/4.object/object3.png)

<a id="batch-download-of-objects"></a>
### オブジェクト一括ダウンロード { #batch-download-of-objects }

* **オブジェクト**タブに作成されているIPとポートオブジェクト全体を、それぞれ一度にダウンロードできます。

!!! tip "ポイント"
    * グループオブジェクトの作成時、グループオブジェクトは追加できません(単一または範囲オブジェクトのみを選択して追加可能)。
    * インスタンスとは関係なく、単にインスタンスの名前とプライベートIPアドレスのみを参照してオブジェクトを作成します。作成したオブジェクトは**オブジェクト**タブで管理します。

!!! danger "注意"
    ポリシーで使用中のオブジェクトは、削除後ALLオブジェクトに変更されます。
