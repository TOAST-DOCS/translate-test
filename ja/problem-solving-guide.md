<!-- pre-align:aligned sig=9be9bdfa8e4e -->

<a id="network-firewall-troubleshooting-guide"></a>
## Network Firewallトラブルシューティングガイド { #network-firewall-troubleshooting-guide }

**Security > Network Firewall > トラブルシューティングガイド**

<br>

<a id="i-cannot-create-the-network-firewall-service"></a>
## Network Firewallサービスを作成できません。 { #i-cannot-create-the-network-firewall-service }

以下のネットワークリソースが準備されているかチェックします。

* Hub VPCとSpoke VPCが準備されているか確認します。
* Hub VPCにトラフィック用、NAT用、外部送信用の互いに異なる3つのサブネットがあるか確認します。
* Spoke VPCまたはSpokeサブネットが準備されているか確認します。
* Hub VPCのルーティングテーブルにインターネットゲートウェイが接続されているか確認します。

<br>

<a id="instances-in-the-spoke-vpc-cannot-communicate-with-the-internet"></a>
## Spoke VPCに属するインスタンスでインターネット通信ができません。 { #instances-in-the-spoke-vpc-cannot-communicate-with-the-internet }

Spoke VPCのパブリック通信は、ルーティング、ピアリング、NAT、ACLポリシーが全て設定されて初めて動作します。以下の内容を確認してください。

* Hub VPCとSpoke VPCの間のピアリングが作成されているか確認します。
* Hub VPCのルーティングにSpoke CIDR対象の経路が追加されているか確認します。
* Spoke VPCのルーティングに0.0.0.0/0または必要な対象CIDRがピアリングゲートウェイとして設定されているか確認します。
* Peering Gatewayルートで、NetworkFirewall_INF_TRAFFIC_VIPがゲートウェイとして設定されているか確認します。
* **Network Firewall > NAT**タブで、NAT設定が追加されているか確認します。
* **Network Firewall > ポリシー > ACL**タブで、必要な許可ポリシーが追加されているか確認します。

<br>

<a id="instances-cannot-be-accessed-from-outside"></a>
## 外部からインスタンスに接続できません。 { #instances-cannot-be-accessed-from-outside }

外部からインスタンスに接続するには、NAT、ACL、Security Groupsの設定が全て必要です。以下の内容を確認してください。

* **Network Firewall > NAT**タブで、NAT前IPとNAT後IPが正しく接続されているか確認します。
    * NAT後IPに該当するIPオブジェクトが、あらかじめ**オブジェクト**タブに作成されているか確認します。
* **Network Firewall > ポリシー > ACL**タブで、送信元、宛先、宛先ポートに対する許可ポリシーがあるか確認します。
* インスタンスのSecurity Groupsでも送信元IPとポートを許可しているか確認します。
* 接続が必要なインスタンスに直接フローティングIPを接続していないか確認します。
    * 直接フローティングIPを接続する場合、通信に問題が発生する可能性があります。

<br>

<a id="blocked-logs-are-not-visible-in-the-log-tab"></a>
## 遮断されたログがログタブに表示されません。 { #blocked-logs-are-not-visible-in-the-log-tab }

default-denyポリシーによって遮断されたログは、デフォルト遮断ポリシーのログ設定を「使用」に変更することで確認できます。以下のパスで設定を確認してください。

* **Network Firewall > オプション > ログ設定**で、デフォルト遮断ポリシーのログ設定へ移動し、**使用**に変更します。
* トラフィックログは、ポリシー別のロギングの有無やオプション設定の影響を受けるため、ACLポリシーのロギング設定も併せて確認してください。

<br>

!!! tip "問題が解決しない場合"
    トラブルシューティングガイドの案内に従って進めても問題が解決しない場合は、NHN Cloudカスタマーサポートまでお問い合わせください。
    * [オンライン1:1お問い合わせはこちら](https://www.nhncloud.com/kr/support/inquiry?sec_nfw_fn)
    * 代表電話：1588-7967(運営時間：月~金 10:00-19:00)
