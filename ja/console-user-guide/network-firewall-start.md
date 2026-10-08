<!-- pre-align:aligned sig=f37ed2d1fbde -->

<a id="getting-started-with-network-firewall"></a>
## Network Firewallを始める { #getting-started-with-network-firewall }

**Security > Network Firewall > コンソール使用ガイド > Network Firewallを始める**

<br>

<a id="prepare-before-creating-network-firewall"></a>
## Network Firewallを作成する前に準備する { #prepare-before-creating-network-firewall }

Network Firewallの作成に必要な最小限のネットワークサービスリソースは次のとおりです。

<a id="requirements-for-a-single-project-configuration"></a>
### 1つのプロジェクトを構成する場合の準備事項 { #requirements-for-a-single-project-configuration }

* 1つのプロジェクト
* 2つのVPC(Hub VPC、Spoke VPC)
* Hub VPC内の3つのサブネット
    * トラフィック(内部)サブネット、NAT(外部)サブネット、外部送信サブネット
* Spoke VPC内に少なくとも1つのサブネット
* Hub VPCのルーティングに接続されたインターネットゲートウェイ

<a id="requirements-for-configuring-2-spoke-vpcs-within-a-single-project"></a>
### 1つのプロジェクト内に2つのSpoke VPCを構成する場合の準備事項 { #requirements-for-configuring-2-spoke-vpcs-within-a-single-project }

* 1つのプロジェクト
* 3つのVPC(Hub VPC、Spoke1 VPC、Spoke2 VPC)
* Hub VPC内の3つのサブネット
    * トラフィック(内部)サブネット、NAT(外部)サブネット、外部送信サブネット
* Spoke1 VPC、Spoke2 VPC内にそれぞれ少なくとも1つのサブネット
* Hub VPCのルーティングに接続されたインターネットゲートウェイ

<a id="preparations-for-configuring-more-than-one-project"></a>
### 1つ以上のプロジェクトを構成する場合の準備事項 { #preparations-for-configuring-more-than-one-project }

* 2つのプロジェクト
* 2つのVPC(それぞれのプロジェクトにHub VPC、Spoke VPC)
* Hub VPC内の3つのサブネット
    * トラフィック(内部)サブネット、NAT(外部)サブネット、外部送信サブネット
* Spoke VPC内に少なくとも1つのサブネット
* Hub VPCのルーティングに接続されたインターネットゲートウェイ

<a id="preparations-for-configuring-cross-region-projects"></a>
### 異なるリージョン間のプロジェクトを構成する場合の準備事項 { #preparations-for-configuring-cross-region-projects }

* 1つのプロジェクト
* 2つのVPC(KR1リージョンにHub VPC、KR2リージョンにSpoke VPC)
* Hub VPC内の3つのサブネット
    * トラフィック(内部)サブネット、NAT(外部)サブネット、外部送信サブネット
* Spoke VPC内に少なくとも1つのサブネット
* Hub VPCのルーティングに接続されたインターネットゲートウェイ

<a id="preparations-for-configuring-multiple-subnets-within-a-single-vpc"></a>
### 単一VPC内に複数のサブネットを構成する場合の準備事項 { #preparations-for-configuring-multiple-subnets-within-a-single-vpc }

* 1つのプロジェクト
* 1つのVPC
* 3つのHubサブネット
    * トラフィック(内部)サブネット、NAT(外部)サブネット、外部送信サブネット
* Hubサブネットと重複しない少なくとも1つのSpokeサブネット
* Spokeサブネットに接続するルーティングテーブル
* VPCのルーティングに接続されたインターネットゲートウェイ

!!! tip "ポイント"
    * **Network Firewall > 概要**でサービス構成図をご参照ください。
    * 上記のサービスリソースは、[Network]カテゴリから作成可能です。 
    * Network Firewallの作成は、プロジェクトごとに1つのみ作成可能です。

<br>

<a id="create-network-firewall"></a>
## Network Firewallを作成する { #create-network-firewall }

1. **Security > Network Firewall**に移動します。
2. 各必須項目を全て選択し、下部の**Network Firewall作成**をクリックします。
    * RBAC：インスタンスオブジェクト照会、Network Firewallサービスの提供に必要なAPI権限を付与
    * 構成方式：単一構成と冗長化構成から選択します。
    * VPC：Network Firewallで使用するVPC
    * サブネット：Network Firewallで内部トラフィック制御のために使用するサブネット
    * NAT：Network Firewallで外部トラフィック制御のために使用するサブネット
    * 外部送信：Network Firewallで生成されたトラフィックとログを送信するサブネット
    <img src="../../../static/images/24.09.12/create.png" height="60%" />

!!! tip "ポイント"
    * 作成されたNetwork Firewallは、ユーザーのプロジェクトには表示されません。 
    * サブネット、NAT、外部送信に使用するサブネットは、全て異なるサブネットを選択する必要があります。
        * なるべくNHN Cloudコンソールで作成できる最小単位(28ビット)で作成することを推奨します。
    * Network Firewallが属するVPCのルーティングテーブルにインターネットゲートウェイが接続されていて初めて作成可能です。
    * Network Firewallが所有しているCIDR帯域と、接続が必要なCIDR帯域は重複しないようにする必要があります。
    * 単一または冗長化構成を選択してNetwork Firewallを作成した後、変更が必要な場合は**オプション**タブから構成を変更できます。ただし、アベイラビリティゾーンは変更できないため、冗長化構成の場合はなるべくアベイラビリティゾーンを分離して構成してください。 

!!! danger "注意"
    * Security Groupsとは別個のサービスであるため、Network Firewallを使用する場合、両方のサービスを許可して初めてインスタンスにアクセスできます。
    * **Network > Network Interface**でVirtual_IPタイプとして作成されているIPは、Network Firewallで冗長化用途に使用されているため、削除した場合は通信が遮断される可能性があります。

<br>

<a id="configure-connection"></a>
## 接続を設定する { #configure-connection }

> [例]
> Network Firewallが使用するVPC(Hub)が10.0.0.0/24であり、Network Firewallと接続が必要なVPC(Spoke)が172.16.0.0/24である場合

1. **Network > Peering Gateway**に移動してピアリングを作成します。
    * ピアリングゲートウェイ接続の詳細については、[ユーザーガイド](https://docs.nhncloud.com/ko/Network/Peering%20Gateway/ko/console-guide/)をご参照ください。
    <img src="../../../static/images/23.12.19/ConnectionSettings3.png" height="65%" />
    <img src="../../../static/images/23.12.19/ConnectionSettings4.png" height="65%" />

!!! tip "ポイント"
    * Spoke VPCの位置に合わせて、適切なピアリングを作成します。 
        * Spoke VPCが同じプロジェクト内である場合は、ピアリングを作成します。
        * Spoke VPCが異なるプロジェクトである場合は、プロジェクトピアリングを作成します。
        * Spoke VPCが異なるリージョンである場合は、リージョンピアリングを作成します。

<br>

2. **Network > Routing**に移動してHub VPCを選択した後、以下のルーティングを設定します。
    * 対象CIDR：172.16.0.0/24
    * ゲートウェイ：ピアリング接続後に追加されたピアリングタイプのゲートウェイ
    <img src="../../../static/images/23.12.19/ConnectionSettings5.png" height="65%" />

<br>

3. **Network > Routing**に移動してSpoke VPCを選択した後、以下のルーティングを設定します。
    * 対象CIDR：0.0.0.0/0
    * ゲートウェイ：ピアリング接続後に追加されたピアリングタイプのゲートウェイ
    <img src="../../../static/images/23.12.19/ConnectionSettings6.png" height="65%" />

!!! tip "ポイント"
    * 上記のようにルーティングを設定すると、Spoke VPCの全ての通信がNetwork Firewallを通過するようになります。
        * 通信を振り分け処理する必要がある場合は、0.0.0.0/0ではなく対象を明確に設定してください。

<br>

4. **Network > Peering Gateway**に移動してルーティングを設定します。
    * 作成されたピアリングを選択して**ルート**タブに移動します。
    * **ピア**または**ローカルルート変更**ボタンを押して、以下のようにルーティングを設定します。
        * 対象CIDR：0.0.0.0/0
        * ゲートウェイ：NetworkFirewall_INF_TRAFFIC_VIP
        <img src="../../../static/images/23.12.19/ConnectionSettings7.png" height="65%" />
        <img src="../../../static/images/23.12.19/ConnectionSettings8.png" height="50%" />

上記のルーティング設定が完了すると、Spoke VPCにあるインスタンスがNetwork Firewallを経由してパブリック通信を行えるようになります。(**Network Firewall > NAT**タブから宛先NATの追加が必要)

<br>

**もしSpoke VPCのサブネットが2つ以上であり、Network Firewallを通じてサブネット間のトラフィック制御が必要な場合**は、以下のルーティングを追加します。

> [例]
> Spoke VPC(172.16.0.0/24)のサブネットが172.16.0.0/25と172.16.0.128/25である場合

* **Network > Routing**に移動してSpoke VPCを選択した後、以下のルーティング2つを追加します。
    * 対象CIDR：172.16.0.0/25と172.16.0.128/25
    * ゲートウェイ：ピアリング接続後に追加されたピアリングタイプのゲートウェイ
    <img src="../../../static/images/23.12.19/ConnectionSettings9.png" height="65%" />
    <img src="../../../static/images/23.12.19/ConnectionSettings10.png" height="65%" />

上記のルーティング設定が完了すると、Spoke VPC内にあるサブネット間でNetwork Firewallを経由してプライベート通信を行えるようになります。(**Network Firewall > ポリシー**タブからポリシーの追加が必要)

<br>

**もしSpoke VPCが2つ以上である場合**は、以下のルーティングを追加します。

> [例]
> Spoke VPC1(172.16.0.0/24)とSpoke VPC2(192.168.0.0/24)である場合

* **Network > Routing**に移動してHub VPCを選択した後、以下のルーティング2つを追加します。
    * Spoke VPC 1
        * 対象CIDR：172.16.0.0/24
        * ゲートウェイ: Hub VPCとSpoke VPC1の間に追加されたピアリングタイプのゲートウェイ
    * Spoke VPC 2
        * 対象CIDR: 192.168.0.0/24
        * ゲートウェイ: Hub VPCとSpoke VPC2の間に追加されたピアリングタイプのゲートウェイ
        <img src="../../../static/images/23.12.19/ConnectionSettings11.png" height="65%" />

!!! tip "ポイント"
    **接続設定**の**4**と同様に、Spoke VPC2-Hub間のVPCピアリングにもルート追加設定が必要です。

<br>

**もし同じVPCでSpokeサブネットを構成する場合**は、新しいルーティングテーブルを作成してサブネットを接続し、ルートを追加します。 
* **Network > Routing**でルーティングテーブルを作成し、ルートを追加します。
    <img src="../../../static/images/24.11.07/routetable_create.png" height="65%" />
    <img src="../../../static/images/24.11.07/route_create.png" height="65%" />

<br>

* **Network > Subnet**でNetwork Firewallと重複しないSpokeサブネットを新しく作成し、ルーティングテーブルを接続します。
    <img src="../../../static/images/24.11.07/subnet_create.png" height="65%" />
    <img src="../../../static/images/24.11.07/routetable_connect.png" height="65%" />

<br>

上記のルーティング設定が完了すると、異なるSpoke VPC間でNetwork Firewallを経由してプライベート通信を行えるようになります。(**Network Firewall > ポリシー**タブからポリシーの追加が必要)
