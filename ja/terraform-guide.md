<a id="third-party-user-guide-terraform-user-guide"></a>
## サードパーティ使用ガイド > Terraform使用ガイド
このドキュメントは、TerraformでNHN Cloudを使用する方法を説明します。

<a id="terraform"></a>
## Terraform
Terraformは、インフラストラクチャを簡単に構築し、安全に変更でき、効率的にインフラストラクチャの構成を管理できるオープンソースツールです。 Terraformの主な特性は次のとおりです。

* **Infrastructure as Code**
    * インフラストラクチャをコードで定義して、生産性と透明性を向上させることができます。
    * 定義したコードを簡単に共有できるため、効率的に協力できます。
* **Execution Plan**
    * 変更計画と変更適用を分離して、変更内容を適用するときに発生する可能性のあるミスを減らすことができます。
* **Resource Graph**
    * 小さな変更がインフラストラクチャ全体にどのような影響を与えるかを事前に確認できます。
    * 依存関係グラフを作成して、このグラフに基づいて計画を立て、この計画を適用したときに変更されるインフラストラクチャの状態を確認できます。
* **Change Automation**
    * 複数の場所に同じ構成のインフラストラクチャを構築および変更するように自動化できます。
    * インフラストラクチャを構築するのにかかる時間を節約でき、ミスも減らせます。


#### リソース対応

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

#### データソース対応

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

* **以下の例で使用されているTerraformバージョンは1.0.0です。**
* **バージョンを含むコンポーネントの名前と数字は変更される可能性があるため、確認して使用してください。**


<a id="terraform-installation"></a>
## Terraformインストール
[Terraformダウンロードページ](https://www.terraform.io/downloads.html)からローカルPCのOSに合わせたファイルをダウンロードします。 ファイルを解凍し、希望するパスに配置した後、環境設定にそのパスを追加すれば、インストール完了です。

以下はLinux(Ubuntu/Debian)インストール例です。

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```


<a id="terraform-initialization"></a>
## Terraform初期化
Terraformを使用する前に、次のようにプロバイダー構成ファイルを作成します。

プロバイダーファイル名は任意に設定でき、この例では`provider.tf`を使用します。

プロバイダーバージョンは、[NHN Cloud TerraformRegistry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest)の`VERSION`情報を参照して記述します。

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
    * NHN Cloudコンソールの**Compute > Instance > 管理**メニューで**APIエンドポイント設定**ボタンをクリックしてテナントIDを確認します。
* **password**
    * **APIエンドポイント設定**ダイアログボックスで保存した**API パスワード**を使用します。
    * APIパスワード設定方法は、**使用者ガイド > Compute > Instance > API使用準備**を参照してください。
* **auth_url**
    * NHN Cloudアイデンティティサービスアドレスを明示します。
    * NHN Cloudコンソールの**Compute > Instance > 管理**メニューで**APIエンドポイント設定**ボタンをクリックしてアイデンティティサービス(identity)URLを確認します。
* **region**
    * NHN Cloudリソースを管理するリージョン情報を入力します。
    * **KR1**: 韓国(パンギョ)リージョン
    * **KR2**: 韓国(ピョンチョン)リージョン
    * **JP1**: 日本(東京)リージョン

プロバイダー構成ファイルがあるパスで`init`コマンドを使用してTerraformを初期化します。

```
$ ls
provider.tf
$ terraform init
```

<a id="data-sources"></a>
## データソース

tfファイル作成に必要なインスタンスタイプID、イメージIDなどはコンソールで確認するか、Terraformが提供するデータソースを使用して取得できます。 データソースはtfファイル内に記述され、取得した情報は変更できず、参照のみ可能です。 NHN Cloudは定期的にイメージを更新するため、イメージ名が変更される場合があります。 使用しようとするイメージの正確な名前はコンソールを参照して明示します。

データソースは`{データソースリソースタイプ}.{データソース名}`として参照します。 以下の例では、`nhncloud_images_image_v2.ubuntu_2004_20201222`で取得したイメージ情報を参照します。

```
data "nhncloud_images_image_v2" "ubuntu_2004_20201222" {
  name = "Ubuntu Server 20.04.1 LTS (2020.12.22)"
  most_recent = true
}
```

データソース内で他のデータソースを参照できます。

```
data "nhncloud_blockstorage_volume_v2" "volume_00"{
  name = "ssd_volume1"
  status = "available"
}

data "nhncloud_blockstorage_snapshot_v2" "my_snapshot" {
  name = "my-snapshot"
  volume_id = data.nhncloud_blockstorage_volume_v2.volume_00.id
  status = "available"
  most_recent = true
}
```




<a id="terraform-usage"></a>
## Terraform基本使用法

Terraformを使用したインフラストラクチャ構築は、通常、以下のようなライフサイクルを持ちます。

1. tfファイル作成
2. 構築計画確認
3. リソース作成
4. リソース修正
5. リソース削除

まず、構築するインフラストラクチャ構成をtfファイルに記述します。 記述されたtfファイルに基づいた構築計画は、以下のように`plan`コマンドで確認します。

```
$ terraform plan
```

構築計画に問題がなければ、`apply`コマンドを使用してリソースを作成、修正、削除します。

```
$ terraform apply
```

次のセクションでは、これらのステップを例とともにさらに詳しく説明します。