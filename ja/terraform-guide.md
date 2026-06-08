<a id="third-party-user-guide-terraform-user-guide"></a>
## サードパーティー使用ガイド > Terraform使用ガイド
この文書はTerraformでNHN Cloudを使用する方法を説明します。

<a id="terraform"></a>
## Terraform
Terraform は、インフラストラクチャを簡単に構築し、安全に変更し、効率的にインフラストラクチャの構成を管理できるオープンソースツールです。Terraform の主な特徴は次のとおりです。

* **Infrastructure as Code**
    * インフラストラクチャをコードとして定義することで、生産性と透明性を向上できます。
    * 定義したコードを簡単に共有でき、効率的にコラボレーションできます。
* **Execution Plan**
    * 変更計画と変更適用を分離することで、変更内容を適用する際に発生する可能性のあるミスを減らすことができます。
* **Change Automation**
    * 複数の場所に同じ構成のインフラストラクチャを構築し、変更を自動化できます。
    * インフラストラクチャを構築する時間を節約でき、ミスも減らすことができます。


#### Resources サポート

* Compute
    * nhncloud_compute_instance_v2
    * nhncloud_compute_volume_attach_v2
    * nhncloud_compute_keypair_v2
* Network
    * nhncloud_lb_loadbalancer_v2
    * nhncloud_lb_listener_v2
    * nhncloud_lb_pool_v2
    * nhncloud_lb_member_v2
    * nhncloud_lb_monitor_v2
    * nhncloud_networking_floatingip_v2
    * nhncloud_networking_floatingip_associate_v2
    * nhncloud_networking_port_v2
    * nhncloud_networking_vpc_v2
    * nhncloud_networking_vpcsubnet_v2
    * nhncloud_networking_routingtable_v2
    * nhncloud_networking_routingtable_attach_gateway_v2
    * nhncloud_networking_secgroup_v2
    * nhncloud_networking_secgroup_rule_v2
    * nhncloud_keymanager_secret_v1
    * nhncloud_keymanager_container_v1
* Block Storage
    * nhncloud_blockstorage_volume_v2
* Object Storage
    * nhncloud_objectstorage_container_v1
    * nhncloud_objectstorage_object_v1
* Container
    * nhncloud_kubernetes_cluster_v1
    * nhncloud_kubernetes_nodegroup_v1
    * nhncloud_kubernetes_cluster_resize_v1
    * nhncloud_kubernetes_nodegroup_upgrade_v1

#### Data sources サポート

* nhncloud_images_image_v2
* nhncloud_blockstorage_volume_v2
* nhncloud_compute_flavor_v2
* nhncloud_compute_keypair_v2
* nhncloud_blockstorage_snapshot_v2
* nhncloud_networking_vpc_v2
* nhncloud_networking_vpcsubnet_v2
* nhncloud_networking_routingtable_v2
* nhncloud_networking_secgroup_v2
* nhncloud_keymanager_secret_v1
* nhncloud_keymanager_container_v1
* nhncloud_kubernetes_cluster_v1
* nhncloud_kubernetes_nodegroup_v1


<a id="note"></a>
### 注意事項

* **以下の例では Terraform バージョン 1.0.0 を使用しています。**
* **バージョンを含むコンポーネントの名前と数値は変更される可能性があるため、確認してからご使用ください。**


<a id="terraform-installation"></a>

## Terraform のインストール
[Terraform ダウンロードページ](https://www.terraform.io/downloads.html)から、ローカル PC のオペレーティングシステムに対応するファイルをダウンロードします。ファイルを解凍して任意のパスに配置し、そのパスを環境設定に追加すると、インストールが完了します。

次は Linux (Ubuntu/Debian) のインストール例です。

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```

<a id="terraform-provider-provided"></a>

## Terraform provider の提供

NHN Cloud は HashiCorp 社の公式パートナーとして [Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest) を通じて Terraform provider を提供します。

Terraform は terraform バイナリファイルを始点として、ローカル環境や配布サーバーのようなリモート環境で、対象を呼び出す方式で実行されます。この際、「対象」は呼び出し方式がそれぞれ異なりますが、対象のサプライヤー、つまりプロバイダーが提供する API を呼び出してやり取りを行います。ここで Terraform が対象とのやり取りを可能にするのが「プロバイダー」です。

<a id="terraform-initialization"></a>

## Terraform初期化
Terraformを使用する前に、次のようにプロバイダー設定ファイルを作成します。

プロバイダーファイル名は任意に設定可能で、この例では `provider.tf` を使用します。

providerバージョンは [NHN Cloud Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest) の `VERSION` 情報を参考にして作成します。

```
# Define required providers
terraform {
  required_providers {
    nhncloud = {
      source = "nhn-cloud/nhncloud"
      version = "{VERSION}"
    }
  }
}

# Configure the nhncloud Provider
provider "nhncloud" {
  user_name   = "terraform-guide@nhncloud.com"
  tenant_id   = "aaa4c0a12fd84edeb68965d320d17129"
  password    = "difficultpassword"
  auth_url    = "https://api-identity-infrastructure.nhncloudservice.com/v2.0"
  region      = "KR1"
}
```

* **user_name**
    * NHN Cloud IDを使用します。
* **tenant_id**
    * NHN Cloud コンソールの **[Compute > Instance > 管理]** メニューで **[API エンドポイント設定]** ボタンをクリックしてテナントIDを確認します。
* **password**
    * **[API Endpoint 設定]** ダイアログボックスで保存した **[API パスワード]** を使用します。
    * API パスワード設定方法は **[ユーザーガイド > Compute > Instance > API 使用準備]** を参照してください。
* **auth_url**
    * NHN Cloud アイデンティティサービスアドレスを指定します。
    * NHN Cloud コンソールの **[Compute > Instance > 管理]** メニューで **[API エンドポイント設定]** ボタンをクリックしてアイデンティティサービス(identity) URLを確認します。
* **region**
    * NHN Cloud リソースを管理するリージョン情報を入力します。
    * **KR1**: 韓国(板橋) リージョン
    * **KR2**: 韓国(平村) リージョン
    * **JP1**: 日本(東京) リージョン

プロバイダー設定ファイルがあるパスで `init` コマンドを使用してTerraformを初期化します。

```
$ ls
provider.tf
$ terraform init
```



<a id="terraform-usage"></a>

## Terraform 基本使用方法

Terraform を利用したインフラ構築は通常、次のようなライフサイクルを持ちます。

1. tf ファイル作成
2. 構築計画確認
3. リソース作成
4. リソース修正
5. リソース削除

まず構築するインフラ構成を tf ファイルに作成します。作成された tf ファイルに従った構築計画は次のように `plan` コマンドで確認します。

```
$ terraform plan
```

構築計画に問題がなければ `apply` コマンドを利用してリソースを作成、修正、削除します。

```
$ terraform apply
```

次のセクションでは、これらのステップを例とともにより詳しく説明します。


<a id="create-tf-files"></a>
### tf ファイル作成

プロバイダ設定ファイルがあるパスに tf ファイルを作成します。複数のリソース設定を一つの tf ファイルにまとめることも、リソース別に別々の tf ファイルとして作成することも可能です。Terraform は作成された全ての tf ファイルを一度に読み込んで構築計画を策定します。

次は `instance.tf` ファイルにインスタンスを作成するリソースを定義した tf ファイルの例です。

```
$ ls
instance.tf provider.tf
$ cat instance.tf
resource "nhncloud_compute_instance_v2" "terraform-instance-01" {
  name      = "terraform-instance-01"
  region    = "KR1"
  flavor_id = "da74152c-0167-4ce9-b391-8a88a8ff2754"
  key_pair  = "terraform-keypair"
  network {
    uuid = "00d5b852-cb77-4307-b6be-d81dad24eec1"
  }
  security_groups = ["default"]
  block_device {
    uuid = "6d0993b4-cd6d-4242-b59b-94258f265331"
    source_type = "image"
    destination_type = "volume"
    boot_index = 0
    volume_size = 20
    delete_on_termination = true
  }
}
```

