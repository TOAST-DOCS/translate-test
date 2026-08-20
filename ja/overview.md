<!-- machine_translated: true -->

<!-- pre-align:aligned sig=ad9be4a958b6 -->

<a id="storage-nas-for-bigdata-overview"></a>
## Storage > NAS for BigData > 概要 { #storage-nas-for-bigdata-overview }

NAS for BigData は、クラウド環境で大容量ファイルストレージを簡単に活用できる完全マネージド型 NAS（network-attached storage）サービスです。標準 NFS（network file system）プロトコルを基盤として、クラウドインスタンスから簡単にマウントでき、ローカルディスクのようにデータを読み書きできます。

拡張可能な大容量ストレージを提供しており、インスタンス間のファイル共有、大規模データ分析、バックアップなど、さまざまな業務に柔軟に対応できます。

<a id="features"></a>
## 特徴 { #features }

<a id="features.capacity"></a>
### 大容量ストレージの提供 { #features.capacity }

大規模なデータを扱うプロジェクトでも、物理機器の増設なしにコンソールからリアルタイムで容量を調整できるため、運用の負担を軽減します。ボリュームサイズの変更はデータ損失なしに反映され、このような拡張性と弾力性をベースに柔軟にデータを管理できます。

<a id="features.sharing"></a>
### NFSベースの効率的なファイル共有 { #features.sharing }

NFSプロトコルをサポートし、インスタンス間のファイル共有を簡単かつ迅速に実装できます。1つのボリュームを複数のサーバーから同時にマウントできるため、マルチノード環境の並列処理や分散作業に適しています。

<a id="features.access_control"></a>
### 簡単な作成と柔軟なアクセス制御 { #features.access_control }

Webコンソールから複雑な設定なしで迅速にファイルレベルのストレージを構成できます。また、Network ACLサービスでIPベースのアクセス制御ポリシーを設定できるため、多数のインスタンスが接続された環境でもセキュリティと柔軟性を同時に確保できます。

<a id="glossary"></a>
## 用語 { #glossary }

<a id="glossary.NAS"></a>
### NAS { #glossary.NAS }

NASは、ネットワークからアクセスできるファイルベースのストレージデバイスです。ユーザーはNASをローカルディスクのようにマウントしてファイルを保存または読み込むことができ、複数のサーバー間のデータ共有に適しています。アクセス制御などの基本的なセキュリティ機能もあわせて提供されます。

<a id="glossary.volume"></a>
### ボリューム { #glossary.volume }

ボリュームはNASの論理的な保存領域であり、インスタンスにマウントしてデータを保存または読み込むことができます。

<a id="glossary.snapshots"></a>
### スナップショット { #glossary.snapshots }

スナップショット(snapshot)は、ボリュームの特定の時点を基準に作成した読み取り専用のコピーです。予期しないデータの破損や削除が発生した際、該当する時点にデータを迅速に復元できます。
自動スナップショットの作成周期が設定可能で、作成されたスナップショットは保存領域を一部使用します。
