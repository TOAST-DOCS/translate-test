<!-- machine_translated: true -->

{% include-markdown '../_nas-for-big-data-vars.md' %}

<!-- pre-align:aligned sig=d48e0cc2304b -->

<a id="storage-nas-for-bigdata-console-user-guide"></a>
## Storage > NAS for BigData > コンソール使用ガイド { #storage-nas-for-bigdata-console-user-guide }

このドキュメントでは、NHN Cloud コンソールで NAS for BigData のボリュームとスナップショットを管理し、インスタンスに接続する方法について説明します。

<a id="volume"></a>
## ボリューム { #volume }
ボリュームはNASの論理的な保存領域であり、インスタンスにマウントしてデータを保存または読み込むことができます。

<a id="create_volume"></a>
### ボリューム作成 { #create_volume }

新しいボリュームを作成します。作成されたボリュームは、NFS (network file system) プロトコルを使用してインスタンスからアクセスできます。

| 項目 | 説明 |
| --- | --- |
| 名前 | 作成するボリュームの名前です。ボリューム名でNFSのアクセスパスを作成します。名前は100文字以内の英数字と一部の記号（'-'、'_'）のみ入力できます。|
| 説明 | ボリュームの説明です。 |
| VPC | ボリュームにアクセスするVPC(Virtual Private Cloud：仮想プライベートクラウド)です。 |
| サブネット | ボリュームにアクセスするサブネットです。選択したVPCのサブネットのみ選択できます。 |
| サイズ | 作成するボリュームのサイズです。最小 $[ min_size ]$ から最大 $[ max_size ]$ まで入力できます。 |
| アクセス制御リスト（ACL） | Network ACL サービスでアクセス制御リスト（ACL）を設定できます。詳細については、[Network ACL サービス ユーザーガイド]($[ network_acl_guide_url ]$)を参照してください。 |
| スナップショット自動作成 | 設定した周期に従ってスナップショットを自動的に作成します。設定した数を超過すると、最も古いスナップショットから順次削除されます。 |

<a id="delete_volume"></a>
### ボリューム削除 { #delete_volume }

ボリュームを削除します。

!!! danger "注意"
    接続されたインスタンスからマウント解除後、削除することを推奨します。マウント状態でボリュームを削除すると、ユーザーシステムに問題が発生する可能性があります。

ボリュームを削除すると、スナップショットを含むすべてのデータが削除されます。削除後はデータを復旧することはできません。

<a id="change_volume_size"></a>
### ボリュームサイズの変更 { #change_volume_size }

ボリュームのサイズを変更します。ボリュームの使用中にもサイズを変更できます。

<a id="change_acl"></a>
### アクセス制御設定の変更 { #change_acl }

Network ACL サービスでアクセス制御リスト（ACL）を設定できます。詳細については、[Network ACL サービスユーザーガイド]($[ network_acl_guide_url ]$)を参照してください。

<a id="snapshots"></a>
## スナップショット { #snapshots }
スナップショットは、ボリュームの特定時点の状態を保存した読み取り専用のコピーです。スナップショットを使用して、ボリュームをスナップショット作成時点の状態に復元できます。

| 項目 | 説明 |
| --- | --- |
| 名前 | スナップショットの名前です。システムが作成した場合は、指定されたルールに従って名前が決定されます。 |
| 作成日 | スナップショットを作成した日時です。 |

<a id="snapshots.create"></a>
### スナップショットの即時作成 { #snapshots.create }

スナップショットを即時に作成します。名前は32文字以内の英数字、及び一部の記号('-'、'\_'、'.')のみ入力できます。各スナップショットはボリューム内で固有の名前を持つ必要があります。

<a id="snapshots.restore"></a>
### スナップショットの復元 { #snapshots.restore }

ボリュームをスナップショットが作成された時点に復元します。スナップショットを復元するには、[カスタマーサポート]($[ support_url ]$)にお問い合わせください。

<a id="snapshots.delete"></a>
### スナップショットの削除 { #snapshots.delete }

指定したスナップショットを削除します。削除したスナップショットは復旧できません。

<a id="connect_volume"></a>
## ボリュームの接続 { #connect_volume }

作成したボリュームの接続情報を使用して、インスタンスにマウントできます。ただし、マウントするインスタンスはボリュームと同じサブネットに接続されている必要があります。

<a id="connect_volume.nfs"></a>
### NFSパッケージのインストール { #connect_volume.nfs }

<a id="connect_volume.nfs-debian-ubuntu"></a>
#### Debian, Ubuntu

```
sudo apt-get install nfs-common rpcbind
```

<br>

<a id="connect_volume.nfs-rocky"></a>
#### Rocky

```
sudo dnf install nfs-utils rpcbind
```

<br>

<a id="connect_volume.rpcbind"></a>
### rpcbindサービスの実行 { #connect_volume.rpcbind }

```
sudo service rpcbind start
```

<br>

<a id="connect_volume.mount"></a>
### ボリュームのマウント { #connect_volume.mount }

```
sudo mount -t nfs <nas-source> <mount-point>
```

| 項目 | 説明 |
| --- | --- |
| &lt;nas-source&gt; | ボリュームの接続パス（`NFS サーバーアドレス:エクスポートパス`）<br>例: 192.168.0.11:/GJ\_SHARE\_FS8/bacb62d4-f271-44ad-a5d2-505d21037b45 |
| &lt;mount-point&gt; | ボリュームをマウントするディレクトリ<br>例: /mnt |
