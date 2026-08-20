<!-- machine_translated: true -->

<!-- pre-align:aligned sig=109ab9c97015 -->

<a id="storage-storage-gateway-overview"></a>
## Storage > Storage Gateway > 概要 { #storage-storage-gateway-overview }

Storage Gatewayは、1つ以上のクラウドインスタンスまたはオンプレミス機器からNHN Cloudストレージを接続し、データを効率的に保存・管理できるサービスです。

> [参考]
> Storage Gatewayは、2025年3月現在、韓国(パンギョ)リージョンで提供されており、NHN Cloudストレージサービスのうち、Object Storageと接続できます。

<a id="characteristics"></a>
## 特徴 { #characteristics }
<a id="sharable"></a>
### 共有性 { #sharable }
NHN Cloud ストレージを 1 つ以上のインスタンスまたはオンプレミス機器にマウントして使用できます。
サポートするプロトコルは NFS v3、v4 (Linux) です。

<a id="convenient"></a>
### 利便性 { #convenient }
様々なインターフェイスのNHN Cloudストレージをファイルレベルでマウントできるインターフェイスを提供するため、別途のファイルシステム構成やAPI呼び出しが必要ありません。

<a id="scalable"></a>
### 拡張性 { #scalable }
NHN Cloudストレージの優れた拡張性により、データ使用量に応じてストレージ容量を柔軟に増設できます。

<a id="stable"></a>
### 安定性 { #stable }
冗長化構成により、障害が発生してもサービスを中断することなく使用できます。

<a id="accessible"></a>
### アクセシビリティ { #accessible }
ゲートウェイのVPCネットワークにFloating IPを接続するか、ネットワークゲートウェイ設定を使用して、さまざまな環境からNHN Cloudストレージにアクセスできます。

<a id="secure"></a>
### セキュリティ性 { #secure }
NHN Cloud ストレージのサーバー側の暗号化機能を使用して、データを安全に保管できます。

<a id="disaster-recovery"></a>
### 災害復旧 { #disaster-recovery }
NHN Cloudストレージの災害復旧設定により、予期せぬ災害状況に備えることができます。


<a id="terms"></a>
## 用語 { #terms }
<a id="gateway"></a>
### ゲートウェイ { #gateway }
NHN Cloudストレージに接続するインターフェイスを提供するインスタンスクラスターです。
ユーザープロジェクトに作成され、冗長化構成が可能です。

<a id="share"></a>
### 共有 { #share }
NHN Cloudストレージを接続する設定です。
接続するストレージ情報、プロトコル、アクセス権限、ACLなどを設定できます。
