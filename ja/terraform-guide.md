<a id="third-party-user-guide-terraform-user-guide"></a>
## サードパーティ使用ガイド > Terraform使用ガイド
このドキュメントは、TerraformでNHN Cloudを使用する方法を説明します。

<a id="terraform"></a>
## Terraform
Terraformは、インフラストラクチャを簡単に構築し、安全に変更し、効率的にインフラストラクチャの構成を管理できるオープンソースツールです。Terraformの主な特徴は、以下の通りです。

* **Infrastructure as Code**
    * インフラストラクチャをコードで定義することで、生産性と透明性を向上させることができます。
    * 定義したコードを簡単に共有でき、効率的に協働作業ができます。
* **Execution Plan**
    * 変更計画と変更適用を分離することで、変更内容を適用する際に発生する可能性のある実誤を減らすことができます。
* **Resource Graph**
    * 小さな変更がインフラストラクチャ全体にどのような影響を与えるかをあらかじめ確認できます。
    * 依存関係グラフを作成して、このグラフに基づいて計画を立て、この計画を適用した時に変更されるインフラストラクチャの状態を確認できます。
* **Change Automation**
    * 複数の場所に同じ構成のインフラストラクチャを構築し、変更することを自動化できます。
    * インフラストラクチャを構築するのにかかる時間を短縮でき、実誤も減らすことができます。


#### Resources対応

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

#### Data sources対応

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

* **以下の例で使用したTerraformバージョンは1.0.0です。**
* **バージョンを含むコンポーネントの名前と数値は変更される可能性があるため、確認してからご使用ください。**


<a id="terraform-installation"></a>
## Terraform インストール
[Terraform ダウンロードページ](https://www.terraform.io/downloads.html)から、ローカルPCのオペレーティングシステムに対応したファイルをダウンロードします。ファイルを解凍し、希望するパスに配置してから、環境設定にそのパスを追加すればインストールが完了します。

以下はLinux(Ubuntu/Debian)インストール例です。

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```


<a id="terraform-initialization"></a>
## Terraform 初期化
Terraformを使用する前に、以下のようにプロバイダー設定ファイルを作成します。

プロバイダーファイル名は任意に設定でき、この例では`provider.tf`を使用します。

provider バージョンは[NHN Cloud Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest)の`VERSION`情報を参照して作成します。

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
    * NHN Cloud コンソールの**Compute > Instance > 管理**メニューで**API エンドポイント設定**ボタンをクリックしてテナントIDを確認します。
* **password**
    * **APIエンドポイント設定**ダイアログで保存した**API パスワード**を使用します。
    * APIパスワード設定方法は**ユーザーガイド > Compute > Instance > API 使用準備**を参照してください。
* **auth_url**
    * NHN Cloud アイデンティティサービスアドレスを指定します。
    * NHN Cloud コンソールの**Compute > Instance > 管理**メニューで**API エンドポイント設定**ボタンをクリックしてアイデンティティサービス(identity) URLを確認します。
* **region**
    * NHN Cloud リソースを管理するリージョン情報を入力します。
    * **KR1**: 韓国(パンギョ)リージョン
    * **KR2**: 韓国(ピョンチョン)リージョン
    * **JP1**: 日本(東京)リージョン

プロバイダー設定ファイルが存在するパスで`init`コマンドを使用してTerraformを初期化します。

```
$ ls
provider.tf
$ terraform init
```