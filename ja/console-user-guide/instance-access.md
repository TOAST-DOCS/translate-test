<!-- pre-align:aligned sig=1e5a2402cc4a -->

<a id="instance-access"></a>
## インスタンス接続 { #instance-access }

**Security > Network Firewall > コンソール使用ガイド > インスタンス接続**

Network Firewallを作成し、接続設定を全て完了した後、Network Firewallを経由してインスタンスに接続します。

<br>

<a id="configure"></a>
## 設定する { #configure }

例えば、1つのプロジェクト内の2つのSpoke VPCで3つのサブネットを構成し、外部からWebファイアウォールへの接続が必要な場合、以下のようにNAT、ACLを設定します。

![](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/2.instance-access/instance-access1.png){ height="65%" }

* **Network Firewall > NAT > 宛先**タブに移動
* **追加**ボタンをクリックした後、宛先NATを設定
  * 設定前に**オブジェクト**タブで宛先IPオブジェクトの作成と、余剰のフローティングIPが必要 
    ![](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/2.instance-access/instance-access2.png){ height="65%" }

* **Network Firewall > ポリシー > ACL**タブで、必要なACLを許可
  * 送信元/宛先インターフェースはALLに設定可能    
    ![](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/2.instance-access/instance-access3.png){ height="65%" }  

!!! danger "注意"
    
    送信元IPをセキュリティグループで許可して初めて、インスタンスに接続可能になります。
