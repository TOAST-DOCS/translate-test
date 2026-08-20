<!-- machine_translated: true -->

{% include-markdown '../_nas-for-big-data-vars.md' %}

<!-- pre-align:aligned sig=70f5c107edf8 -->

<a id="storage-nas-for-bigdata-overview"></a>
## Storage > NAS for BigData > 概要 { #storage-nas-for-bigdata-overview }

NAS for BigData は、クラウド環境で大容量ファイルストレージを手軽に活用できるフルマネージド NAS (Network-Attached Storage) サービスです。標準の NFS (Network File System) プロトコルをベースに、クラウドインスタンスから簡単にマウントでき、ローカルディスクのようにデータの読み書きができます。

$[ overview_capacity_prefix ]$拡張可能な大容量ストレージを提供し、インスタンス間のファイル共有、大規模データ分析、バックアップなど、さまざまな業務に柔軟に対応できます。

<a id="features"></a>
## 特徴 { #features }

<a id="features.capacity"></a>
### 大容量ストレージの提供 { #features.capacity }

{% if overview_capacity_prefix %}最大 $[ max_size_text ]$ までストレージ容量を拡張できます。$[ scale_description ]$ {% endif %}大規模なデータを扱うプロジェクトでも、物理機器の増設なしにコンソールからリアルタイムで容量を調整でき、運用負担を軽減できます。ボリュームサイズの変更はデータを失うことなく反映され、このような拡張性と弾力性を基盤に柔軟にデータを管理できます。

<a id="features.sharing"></a>
### NFSベースの効率的なファイル共有 { #features.sharing }

NFSプロトコルをサポートし、インスタンス間のファイル共有を簡単かつ迅速に実装できます。1つのボリュームを複数のサーバーから同時にマウントできるため、マルチノード環境の並列処理や分散作業に適しています。

<a id="features.access_control"></a>
### 簡単な作成と柔軟なアクセス制御 { #features.access_control }

コンソールで複雑な設定なしに、素早くファイルレベルのストレージを構成できます。また、Network ACL サービスで IP ベースのアクセス制御ポリシーを設定でき、多数のインスタンスが接続された環境でもセキュリティと柔軟性を同時に確保できます。

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
