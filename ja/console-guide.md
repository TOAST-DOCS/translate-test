<!-- machine_translated: true -->

<!-- pre-align:aligned sig=df549469ae0a -->

<a id="storage-storage-gateway-console-user-guide"></a>
## Storage > Storage Gateway > コンソール使用ガイド { #storage-storage-gateway-console-user-guide }

このドキュメントでは、NHN CloudコンソールでStorage Gatewayのゲートウェイと共有を管理および接続する方法について説明します。

<a id="gateway"></a>
## ゲートウェイ(Gateway) { #gateway }
<a id="create-gateway"></a>
### ゲートウェイ作成 { #create-gateway }
新しいストレージゲートウェイを作成します。ゲートウェイはユーザープロジェクトにインスタンスを作成して構成します。 

<a id="create-gateway-gateway-information"></a>
#### ゲートウェイ情報
ストレージゲートウェイの名前、説明、接続するストレージタイプを設定します。

!!! tip "ヒント"
    2025年3月現在、Object Storageを接続できます。

<a id="create-gateway-cache-storage"></a>
#### キャッシュストレージ
ストレージゲートウェイのディスクキャッシュとして使用するストレージのサイズを設定します。SSDタイプで提供され、最小50GB、最大2,048GBまで設定できます。

<a id="create-gateway-network"></a>
#### ネットワーク
ストレージゲートウェイに使用する VPC とサブネットを選択します。
ゲートウェイを構成するインスタンスには、選択した VPC のサブネットに関連付けられたネットワークインターフェイスが作成されます。ネットワークリソースの作成と管理の詳細については、[VPC ユーザーガイド](/Network/VPC/ja/overview/)を参照してください。
サービスゲートウェイは、Object Storage などのユーザー VPC 外部にあるストレージに、インターネットを経由せずに接続するために使用します。サービスゲートウェイの詳細については、[Service Gateway 使用ガイド](/Network/Service%20Gateway/ja/overview/)を参照してください。

<a id="create-gateway-floating-ip"></a>
#### Floating IP
フローティング IP の使用するかどうかを設定します。ゲートウェイにフローティング IP を使用すると、インターネットからゲートウェイにアクセスできます。詳細については、[Floating IP 使用ガイド](/Network/Floating%20IP/ja/overview/)を参照してください。

<a id="create-gateway-security-groups"></a>
#### セキュリティグループ
ストレージゲートウェイのインスタンスが属するセキュリティグループを指定します。選択した VPC ネットワーク外部からゲートウェイを経由して NHN Cloud ストレージにマウントするには、セキュリティグループに次のようなポートルールを明示する必要があります。

| 方向 | IPプロトコル | ポート範囲 | Ether | 遠隔 |
| --- | --- | --- | --- | --- |
| 受信 | TCP | 111 | IPv4 | 遠隔地IP |
| 受信 | TCP | 2049 | IPv4 | 遠隔地IP |
| 受信 | TCP | 57861-57869 | IPv4 | 遠隔地IP |

遠隔地IPは、CIDR形式の帯域で設定できます。

!!! danger "注意"
    遠隔地IPを`0.0.0.0/0`のような広い帯域に設定すると、セキュリティが脆弱になる可能性があります。最小限の範囲に設定してください。

詳細については、[Security Groups 使用ガイド](/Network/Security%20Groups/ja/overview/)を参照してください。

<a id="create-gateway-redundancy"></a>
#### 冗長化
ストレージゲートウェイを冗長化するかどうかを選択します。
冗長化を使用すると、2つのインスタンスを作成してクラスターを構成します。クラスターを構成する1つのインスタンスに障害が発生しても、他のインスタンスを介して中断することなくゲートウェイを使用できます。障害が発生してサービスから除外されたインスタンスは、オートヒーリング機能により自動的に復旧され、クラスターに投入されます。

<a id="start-gateway"></a>
### ゲートウェイ開始 { #start-gateway }
停止していたストレージゲートウェイを開始します。

<a id="stop-gateway"></a>
### ゲートウェイ停止 { #stop-gateway }
ストレージゲートウェイを停止します。ゲートウェイを停止すると、クラスターを構成するインスタンスが停止し、ストレージと接続できません。

!!! danger "注意"
    ストレージゲートウェイを停止する前に、NHN Cloud ストレージを接続して使用中のシステムからアンマウントする必要があります。マウント状態でゲートウェイを停止すると、ユーザーシステムに問題が発生する可能性があります。

<a id="delete-gateway"></a>
### ゲートウェイ削除 { #delete-gateway }
ストレージゲートウェイを削除します。クラスターを構成する全てのインスタンスとリソースが削除されます。ゲートウェイに接続されていたNHN Cloudストレージは削除されません。

!!! tip "ヒント"
    ゲートウェイを削除するには、まず、ゲートウェイに作成した全ての共有を削除する必要があります。

<a id="share"></a>
## 共有(Share) { #share }
<a id="create-share"></a>
### 共有作成 { #create-share }
共有を作成します。共有とは、NHN Cloud ストレージを接続するための設定です。共有を作成すると、マウント接続情報を取得できます。この接続情報を使用して、ユーザーのシステムに NHN Cloud ストレージをマウントして利用できます。

<a id="create-share-share-information"></a>
#### 共有情報
マウント接続情報のパスに使用する共有名とプロトコルを設定します。

!!! tip "ヒント"
    2025年3月現在、NFSプロトコルを使用できます。

<a id="create-share-storage-information-for-connection"></a>
#### 接続ストレージ情報
接続するストレージの情報を設定します。
Object Storage では、接続するコンテナ名と S3 API認証情報の Access Key が必要です。接続するコンテナの名前は、Amazon S3 のバケット命名規則に従う必要があります。S3 API認証情報は、Object Storage コンソールまたは API を使用して発行できます。詳細については、**Object Storage Amazon S3互換 API ガイド**の[バケット作成](/Storage/Object%20Storage/ja/s3-api-guide/#bucket)セクションと[S3 API認証情報](/Storage/Object%20Storage/ja/s3-api-guide/#s3-api-credential)セクションを参照してください。

!!! tip "ヒント"
    Object Storageコンテナを接続する共有を作成すると、Object Storageに`{コンテナ名}+segments`コンテナが自動的に作成されます。ゲートウェイを介して25MBを超えるファイルを保存すると、接続されたコンテナにマルチパートでアップロードされ、マルチパートオブジェクトのセグメントオブジェクトが`{コンテナ名}+segments`コンテナに保存されます。

<!-- 改行のためのコメント -->

!!! danger "注意"
    接続する Object Storage のコンテナに IP ACL を設定する場合は、必ずサービスゲートウェイへの **read/write 許可** を追加する必要があります。

Object StorageのS3 API認証情報を発行するユーザーは、接続するコンテナに対する**read/write**権限が必要です。

ストレージゲートウェイを通じて Object Storage のコンテナを接続して使用している間に、コンテナを削除したり S3 API認証情報を削除したりすると、ユーザーシステムに問題が発生する可能性があります。削除しないように注意してください。

スtoレージゲートウェイを通じて Object Storage のコンテナを接続して使用中に、`{コンテナ名}+segments` コンテナのオブジェクトを削除すると、保存したファイルにアクセスできなくなります。削除しないように注意してください。

<a id="create-share-nfs-permissions-settings"></a>
#### NFS権限設定
NFSプロトコルで接続するクライアントの権限を設定します。

| Squashオプション | 説明 |
| --- | --- |
| `no_root_squash` | クライアントのrootをNFSサーバーのrootにマッピングします。 |
| `root_squash` | クライアントのrootをnobodyまたは指定したUID/GIDにマッピングします。 |
| `all_squash` | クライアントのすべてのユーザーを nobody または指定した UID/GID にマッピングします。 |

ユーザーIDとグループIDを入力しない場合、Squashオプションに従って **root(0)** または **nobody(65534)** に設定されます。それ以外のユーザーとグループにマッピングするには、Linux ユーザーIDとグループIDを入力します。Linux ユーザーIDとグループIDは、Linux シェルで `id` コマンドで確認できます。

```
$ id
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu)
```

<a id="create-share-access-control-acl"></a>
#### アクセス制御(ACL)
ゲートウェイを介してNHN CloudストレージにアクセスできるクライアントのIPまたはIP帯域をCIDR形式で入力します。

<a id="create-share-cache-settings"></a>
#### キャッシュ設定
メモリキャッシュの有効時間を設定します。設定された有効時間の間、キャッシュが維持されます。

<a id="delete-share"></a>
### 共有削除 { #delete-share }
共有を削除します。 

!!! danger "注意"
    共有を削除する前に、NHN Cloudストレージをマウントして使用しているシステムからアンマウントする必要があります。マウントした状態で共有を削除すると、ユーザーシステムに問題が発生する可能性があります。

<a id="immediately-empty-cache"></a>
### キャッシュをすぐに空にする { #immediately-empty-cache }
ディスクキャッシュ領域に保存されているデータを直ちに削除します。

<a id="change-access-key"></a>
### Access Key変更 { #change-access-key }
Object Storageタイプゲートウェイの共有作成時に設定したAccess Keyを変更します。

!!! danger "注意"
    Access Keyを変更する前に、NHN Cloudストレージをマウントして使用中のシステムからアンマウントする必要があります。マウントした状態でAccess Keyを変更すると、ユーザーシステムに問題が発生する可能性があります。

<a id="change-nfs-permissions"></a>
### NFS権限変更 { #change-nfs-permissions }
NFSプロトコルで接続するクライアントの権限を変更します。

<a id="change-access-control-acl"></a>
### アクセス制御(ACL)変更 { #change-access-control-acl }
ゲートウェイを介してNHN CloudストレージにアクセスできるクライアントのIPまたはIP帯域を変更します。

<a id="connect-nfs"></a>
## NFS接続 { #connect-nfs }
NFSを使用するには、次のようにNFSパッケージをインストールし、rpcbindサービスを実行する必要があります。

<a id="install-nfs-package"></a>
### NFSパッケージインストール { #install-nfs-package }
* **Debian, Ubuntu**
```
sudo apt-get install nfs-common rpcbind
```

* **CentOS**
```
sudo yum install nfs-utils rpcbind
```

<a id="run-rpcbind-service"></a>
### rpcbindサービス実行 { #run-rpcbind-service }
```
sudo service rpcbind start
```

<a id="mount-share"></a>
### 共有マウント { #mount-share }
作成した共有のマウント接続情報と mount コマンドを使用して、次のように NHN Cloud ストレージをユーザーシステムにマウントできます。

```
sudo mount -t nfs {マウント接続情報} {マウントするパス}
```

NFS v3を使用するには次のようにバージョンオプションを追加する必要があります。

```
sudo mount -t nfs -o vers=3 {マウント接続情報} {マウントするパス}
```

* マウント接続情報は共有の詳細情報で確認できます。 
 例：192.168.0.11:/data

* マウントするパス
 例：/mnt/data


<a id="posix-api"></a>
## POSIX API { #posix-api }
Object StorageタイプのゲートウェイはPOSIX APIの一部のみサポートします。

<a id="supported-apis"></a>
### サポートするAPI { #supported-apis }
```
read, write, readdir, truncate, fallocate, fsync
```

!!! danger "注意"
    rename、hardlink、symlinkは使用できません。動作しないか、Object Storageに意図しないオブジェクトが作成される可能性があります。
    rsync, viのような一時ファイルに保存した後、名前を変更するツールは使用しないことを推奨します。
