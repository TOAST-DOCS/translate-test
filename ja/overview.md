## Security > Network Firewall > 概要

Network Firewall は、NHN Cloud で使用するインフラ資産を安全に保護するために提供するネットワークセキュリティサービスです。
NHN Cloud に特化されたアクセス制御を適用でき、別途のファイアウォール製品を使用しなくても簡単にファイアウォール機能を使用できます。


> Network Firewall サービスは、韓国（パンギョ）リージョンの場合、新しいネットワーク環境でのみ利用できます。
> 韓国（パンギョ）リージョンで 2022 年 3 月 7 日以前に作成したプロジェクトは改善前のネットワーク環境であるため、Network Firewall サービスを利用するには新しくプロジェクトを作成する必要があります。

## 主要機能
* 効率的にネットワーク通信ポリシーを管理できます。
    * Stateful 方式で 1 つのポリシーでトラフィックを制御します。
* Hub-Spoke 構造で外部攻撃からインスタンスを安全に保護できます。
    * VPC 間の内部トラフィックとインバウンド/アウトバウンドトラフィックを制御します。
* インターネット環境でサイト間の暗号化されたトンネルを通じて安全な仮想プライベートネットワーク (VPN) を提供します。    
* ネットワークのブロックと許可に関するリアルタイムログ検索とバックアップ機能を提供します。
    * お客様の環境に合わせてさまざまなバックアップ方式を提供します（Syslog、Object Storage、Log & Crash Search）。
* 安定的な運用のために高可用性（冗長化）を提供します。

## Network Firewall サービス構成図
サービスは次の 5 つの形態で構成できます。

### 1 つのプロジェクト
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/ja/Architecture1.png" height="70%">

### 1 つ以上のプロジェクト
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/ja/Architecture2.png" height="70%" width="100%" />


### 異なるリージョン間のプロジェクト
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/ja/Architecture3.png" height="70%" width="100%" />


### 1 つのプロジェクト内の 2 つの Spoke VPC
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/ja/Architecture4.png" height="70%" width="100%" />


### 1 つの VPC 内の複数のサブネット
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/ja/Architecture5.png" height="50%" width="100%" />


> [注記]
> 
> * 上記の構成図は一般的な構成であり、お客様の環境に応じて Network Firewall を除く WEB、WAS、Load Balancer などの構成が異なる場合があります。
> 
> * 異なるリージョンのプロジェクト環境では、同じプロジェクトのみ構成可能です。詳細については、「ユーザーガイド」を参照してください。
> 
> * サービス構成時、2022 年 3 月 7 日より前に構成したネットワーク環境とは接続できません。
> 例えば、2022 年 3 月 7 日より前に構成したネットワーク環境を使用するプロジェクトと、それ以降に構成したネットワーク環境を使用するプロジェクトが作成されている場合、新しいネットワーク環境に Network Firewall を作成することはできますが、改善前のネットワーク環境を Spoke VPC として使用することはできません。
