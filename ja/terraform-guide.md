<a id="third-party-user-guide-terraform-user-guide"></a>
## サードパーティー使用ガイド > Terraform使用ガイド
この文書はTerraformでNHN Cloudを使用する方法を説明します。

<a id="terraform"></a>
## Terraform
Terraformは、インフラを簡単に構築し、安全に変更し、効率的にインフラの構成を管理できるオープンソースツールです。Terraformの主な特徴は以下の通りです。

* **Infrastructure as Code**
    * インフラをコードで定義することで、生産性と透明性を向上させることができます。
    * 定義したコードを簡単に共有できるため、効率的に協業することができます。
* **Execution Plan**
    * 変更計画と変更適用を分離することで、変更内容を適用する際に発生する可能性のあるミスを減らすことができます。
* **Change Automation**
    * 複数の場所に同じ構成のインフラを構築・変更できるよう自動化することができます。
    * インフラを構築する時間を節約でき、ミスも減らすことができます。


#### Resourcesサポート

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

#### Data sourcesサポート

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
* **バージョンを含む構成要素の名前と数字は変更される可能性がありますので、確認してからご使用ください。**


<a id="terraform-installation"></a>

## Terraformインストール
[Terraformダウンロードページ](https://www.terraform.io/downloads.html)でローカルPCのOSに対応したファイルをダウンロードします。ファイルを解凍して任意のパスに配置し、環境設定に該当パスを追加するとインストールが完了します。

以下はLinux（Ubuntu/Debian）のインストール例です。

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```

<a id="terraform-provider-provided"></a>

## Terraform provider の提供

NHN CloudはHashiCorp社の公式パートナーとして[Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest)を通じてTerraform providerを提供しています。

Terraformはterraformバイナリファイルを起点として、ローカル環境またはデプロイサーバーのようなリモート環境で目的のターゲットを呼び出す方式で実行されます。この際、「目的のターゲット」は呼び出し方式がそれぞれ異なりますが、ターゲットの供給者、すなわちプロバイダーが提供するAPIを呼び出して相互作用を行います。ここでTerraformがターゲットとの相互作用を可能にするものが「プロバイダー」です。



<a id="terraform-initialization"></a>

## Terraform初期化
Terraformを使用する前に、次のようにプロバイダー設定ファイルを作成します。

プロバイダーファイル名は任意に設定可能で、この例では`provider.tf`を使用します。

providerバージョンは[NHN Cloud Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest)の`VERSION`情報を参考にして作成します。

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
    * **APIエンドポイント設定**ダイアログボックスで保存した**APIパスワード**を使用します。
    * APIパスワード設定方法は**ユーザーガイド > Compute > Instance > API使用準備**を参考にします。
* **auth_url**
    * NHN Cloud認証サービスアドレスを明示します。
    * NHN Cloudコンソールの**Compute > Instance > 管理**メニューで**APIエンドポイント設定**ボタンをクリックして認証サービス(identity) URLを確認します。
* **region**
    * NHN Cloudリソースを管理するリージョン情報を入力します。
    * **KR1**: 韓国(板橋)リージョン
    * **KR2**: 韓国(坪村)リージョン
    * **JP1**: 日本(東京)リージョン

プロバイダー設定ファイルがあるパスで`init`コマンドを利用してTerraformを初期化します。

```
$ ls
provider.tf
$ terraform init
```



<a id="terraform-usage"></a>

## Terraform 基本使用法

Terraformを利用したインフラ構築は通常、以下のようなライフサイクルを持ちます。

1. tf ファイル作成
2. 構築計画確認
3. リソース作成
4. リソース修正
5. リソース削除

まず構築するインフラ形状を tf ファイルに記述します。作成された tf ファイルに基づく構築計画は以下のように `plan` コマンドで確認します。

```
$ terraform plan
```

構築計画に問題がなければ `apply` コマンドを利用してリソースを生成、修正、削除します。

```
$ terraform apply
```

次のセクションでは、これらの段階を例とともにより詳しく説明します。


<a id="create-tf-files"></a>
### tf ファイル作成

プロバイダ設定ファイルがあるパスに tf ファイルを作成します。複数のリソース設定を一つの tf ファイルにまとめたり、リソース別に別々の tf ファイルとして作成することも可能です。Terraformは作成されたすべての tf ファイルを一度に読み込んで構築計画を策定します。

以下は `instance.tf` ファイルにインスタンスを生成するリソースを定義した tf ファイルの例です。

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

