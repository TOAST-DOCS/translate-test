## Network > Transit Hub > API v2ガイド

NHN Cloud Networkサービスは、API呼び出し時の認証/認可のためにIaaSトークンを使用します。IaaSトークンは、NHN CloudのOpenStackベースのインフラサービス(IaaS)で使用する認証トークンです。IaaSトークンの発行及び使用に関する詳細は、[IaaSトークン](/nhncloud/ja/public-api/iaas-token)を参照してください。

トランジットハブAPIは`network`タイプエンドポイントを利用します。正確なエンドポイントはトークン発行レスポンスの`serviceCatalog`を参照します。

| タイプ | リージョン | エンドポイント |
|---|---|---|
| network | 韓国(パンギョ)リージョン<br>韓国(ピョンチョン)リージョン<br>韓国(光州)リージョン | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

APIレスポンスにガイドに記載されていないフィールドが表示される場合があります。このようなフィールドは、NHN Cloudの内部用途で使用され、事前告知なしに変更される可能性があるため、使用しないでください。

## トランジットハブ

### トランジットハブリスト表示

```
GET /v2.0/gateways/transithubs
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するトランジットハブID |
| name | Query | String | - | 照会するトランジットハブ名 |


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithubs | Body | Array | トランジットハブ情報オブジェクトリスト |
| transithubs.id | Body | UUID | トランジットハブID |
| transithubs.tenant_id | Body | String | テナントID |
| transithubs.name | Body | String | トランジットハブ名 |
| transithubs.description | Body | String | トランジットハブの説明 |
| transithubs.multicast_enable | Body | Boolean | マルチキャスト機能の使用有無 |
| transithubs.default_association_enable | Body | Boolean | 基本ルーティングテーブル接続機能の使用有無 |
| transithubs.default_propagation_enable | Body | Boolean | 基本ルーティングテーブル伝播機能の使用有無 |

<details><summary>例</summary>

```json
{
  "transithubs": [
    {
      "status": "ACTIVE",
      "description": null,
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-12 22:19:05",
      "multicast_enable": true,
      "updated_at": "2024-02-12 22:19:05",
      "default_propagation_enable": true,
      "default_association_enable": true,
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "name": "thub"
    }
  ]
}
```
</details>

---
### トランジットハブ表示

```
GET /v2.0/gateways/transithubs/{transitHubId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transitHubId | URL | UUID | O | トランジットハブID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub | Body | Object | トランジットハブ情報オブジェクト |
| transithub.id | Body | UUID | トランジットハブID |
| transithub.tenant_id | Body | String | テナントID |
| transithub.name | Body | String | トランジットハブ名 |
| transithub.description | Body | String | トランジットハブの説明 |
| transithub.multicast_enable | Body | Boolean | マルチキャスト機能の使用有無 |
| transithub.default_association_enable | Body | Boolean | 基本ルーティングテーブル接続の使用有無 |
| transithub.default_propagation_enable | Body | Boolean | 基本ルーティングテーブル伝播の使用有無 |

<details><summary>例</summary>

```json
{
  "transithub": {
    "status": "ACTIVE",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "multicast_enable": true,
    "updated_at": "2024-02-12 22:19:05",
    "default_propagation_enable": true,
    "default_association_enable": true,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub"
  }
}
```
</details>

---
### トランジットハブを作成する

```
POST /v2.0/gateways/transithubs
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub | Body | Object | O | トランジットハブ情報オブジェクト |
| transithub.name | Body | String | - | トランジットハブ名 |
| transithub.description | Body | String | - | トランジットハブの説明 |
| transithub.multicast_enable | Body | Boolean | O | マルチキャストの使用有無 |
| transithub.default_association_enable | Body | Boolean | O | 基本ルーティングテーブル接続の使用有無 |
| transithub.default_propagation_enable | Body | Boolean | O | 基本ルーティングテーブル伝播の使用有無 |




<details><summary>例</summary>

```json
{
  "transithub": {
    "default_propagation_enable": true,
    "default_association_enable": true,
    "multicast_enable": true,
    "name": "thub",
    "description": "test"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub | Body | Object | トランジットハブ情報オブジェクト |
| transithub.id | Body | UUID | トランジットハブID |
| transithub.tenant_id | Body | String | テナントID |
| transithub.name | Body | String | トランジットハブ名 |
| transithub.description | Body | String | トランジットハブの説明 |
| transithub.multicast_enable | Body | Boolean | マルチキャスト機能の使用有無 |
| transithub.default_association_enable | Body | Boolean | 基本ルーティングテーブル接続の使用有無 |
| transithub.default_propagation_enable | Body | Boolean | 基本ルーティングテーブル伝播の使用有無 |


<details><summary>例</summary>

```json
{
  "transithub": {
    "status": "ACTIVE",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "multicast_enable": true,
    "updated_at": "2024-02-12 22:19:05",
    "default_propagation_enable": true,
    "default_association_enable": true,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub"
  }
}
```
</details>

---
### トランジットハブを修正する

```
PUT /v2.0/gateways/transithubs/{transitHubId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transitHubId | URL | UUID | O | トランジットハブID |
| transithub | Body | Object | O | トランジットハブ情報オブジェクト |
| transithub.name | Body | String | - | トランジットハブ名 |
| transithub.description | Body | String | - | トランジットハブの説明 |

<details><summary>例</summary>

```json
{
  "transithub": {
    "name": "thub1",
    "description": "test1"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub | Body | Object | トランジットハブ情報オブジェクト |
| transithub.id | Body | UUID | トランジットハブID |
| transithub.tenant_id | Body | String | テナントID |
| transithub.name | Body | String | トランジットハブ名 |
| transithub.description | Body | String | トランジットハブの説明 |
| transithub.multicast_enable | Body | Boolean | マルチキャスト機能の使用有無 |
| transithub.default_association_enable | Body | Boolean | 基本ルーティングテーブル接続の使用有無 |
| transithub.default_propagation_enable | Body | Boolean | 基本ルーティングテーブル伝播の使用有無 |


<details><summary>例</summary>

```json
{
  "transithub": {
    "status": "ACTIVE",
    "description": "test1",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "multicast_enable": true,
    "updated_at": "2024-03-04 01:59:00.961621",
    "default_propagation_enable": true,
    "default_association_enable": true,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub1"
  }
}
```
</details>

---
### トランジットハブを削除する

```
DELETE /v2.0/gateways/transithubs/{transitHubId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transitHubId | URL | UUID | O | トランジットハブID |


#### レスポンス
このAPIはレスポンス本文を返しません。










## 接続

### 接続リスト表示

```
GET /v2.0/gateways/transithub_attachments
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会する接続ID |
| name | Query | String | - | 照会する接続名 |
| resource_id | Query | UUID | - | 照会するリソースID(VPC) |
| subnet_id | Query | UUID | - | 照会するサブネットID |
| transithub_id | Query | UUID | - | 照会するトランジットハブID |



#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_attachments | Body | Array | 接続情報オブジェクトリスト |
| transithub_attachments.id | Body | UUID | 接続ID |
| transithub_attachments.tenant_id | Body | String | テナントID |
| transithub_attachments.name | Body | String | 接続名 |
| transithub_attachments.description | Body | String | 接続の説明 |
| transithub_attachments.resource_id | Body | UUID | リソースID(VPC) |
| transithub_attachments.subnet_id | Body | UUID | サブネットID |
| transithub_attachments.transithub_id | Body | UUID | トランジットハブID |

<details><summary>例</summary>

```json
{
  "transithub_attachments": [
    {
      "status": "ACTIVE",
      "remote": false,
      "name": "thub-attachment",
      "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
      "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-13 01:22:09",
      "updated_at": "2024-02-13 01:22:11",
      "resource_cidr": "172.16.0.0/12",
      "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
      "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": null
    }
  ]
}
```
</details>

---
### 接続の表示

```
GET /v2.0/gateways/transithub_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| attachmentId | URL | UUID | O | 接続ID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_attachment | Body | Object | 接続情報オブジェクト |
| transithub_attachment.id | Body | UUID | 接続ID |
| transithub_attachment.tenant_id | Body | String | テナントID |
| transithub_attachment.name | Body | String | 接続名 |
| transithub_attachment.description | Body | String | 接続の説明 |
| transithub_attachment.resource_id | Body | UUID | リソースID(VPC) |
| transithub_attachment.subnet_id | Body | UUID | サブネットID |
| transithub_attachment.transithub_id | Body | UUID | トランジットハブID |

<details><summary>例</summary>

```json
{
  "transithub_attachment": {
    "status": "ACTIVE",
    "remote": false,
    "name": "thub-attachment",
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:09",
    "updated_at": "2024-02-13 01:22:11",
    "resource_cidr": "172.16.0.0/12",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
    "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": null
  }
}
```
</details>

---
### 接続を作成する

```
POST /v2.0/gateways/transithub_attachments
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_attachment | Body | Object | O | ロードバランサー情報オブジェクト |
| transithub_attachment.name | Body | String | - | 接続名 |
| transithub_attachment.description | Body | String | - | 接続の説明 |
| transithub_attachment.resource_id | Body | UUID | O | リソースID(VPC) |
| transithub_attachment.subnet_id | Body | UUID | O | サブネットID |
| transithub_attachment.transithub_id | Body | UUID | O | 接続が登録されるトランジットハブID |

<details><summary>例</summary>

```json
{
  "transithub_attachment": {
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub-attachment",
    "description": null
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_attachment | Body | Object | 接続情報オブジェクト |
| transithub_attachment.id | Body | UUID | 接続ID |
| transithub_attachment.tenant_id | Body | String | テナントID |
| transithub_attachment.name | Body | String | 接続名 |
| transithub_attachment.description | Body | String | 接続の説明 |
| transithub_attachment.resource_id | Body | UUID | リソースID(VPC) |
| transithub_attachment.subnet_id | Body | UUID | サブネットID |
| transithub_attachment.transithub_id | Body | UUID | トランジットハブID |


<details><summary>例</summary>

```json
{
  "transithub_attachment": {
    "status": "ACTIVE",
    "remote": false,
    "name": "thub-attachment",
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:09",
    "updated_at": "2024-02-13 01:22:11",
    "resource_cidr": "172.16.0.0/12",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
    "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": null
  }
}
```
</details>

---
### 接続を修正する

```
PUT /v2.0/gateways/transithub_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| attachmentId | URL | UUID | O | 接続ID |
| transithub_attachment | Body | Object | O | 接続情報オブジェクト |
| transithub_attachment.name | Body | String | - | 接続名 |
| transithub_attachment.description | Body | String | - | 接続の説明 |

<details><summary>例</summary>

```json
{
  "transithub_attachment": {
    "name": "thub-attachment1",
    "description": "test1"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_attachment | Body | Object | 接続情報オブジェクト |
| transithub_attachment.id | Body | UUID | 接続ID |
| transithub_attachment.tenant_id | Body | String | テナントID |
| transithub_attachment.name | Body | String | 接続名 |
| transithub_attachment.description | Body | String | 接続の説明 |
| transithub_attachment.resource_id | Body | UUID | リソースID(VPC) |
| transithub_attachment.subnet_id | Body | UUID | サブネットID |
| transithub_attachment.transithub_id | Body | UUID | トランジットハブID |


<details><summary>例</summary>

```json
{
  "transithub_attachment": {
    "status": "ACTIVE",
    "remote": false,
    "name": "thub-attachment1",
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:09",
    "updated_at": "2024-02-13 01:22:11",
    "resource_cidr": "172.16.0.0/12",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
    "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "test1"
  }
}
```
</details>

---
### 接続を削除する

```
DELETE /v2.0/gateways/transithub_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| attachmentId | URL | UUID | O | 接続ID |


#### レスポンス
このAPIはレスポンス本文を返しません。










## ルーティングテーブル

### ルーティングテーブルリストの表示

```
GET /v2.0/gateways/transithub_routing_tables
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するルーティングテーブルID |
| name | Query | String | - | 照会するルーティングテーブル名 |
| transithub_id | Query | UUID | - | 照会するトランジットハブID |



#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_tables | Body | Array | ルーティングテーブル情報オブジェクトリスト |
| transithub_routing_tables.id | Body | UUID | ルーティングテーブルID |
| transithub_routing_tables.tenant_id | Body | String | テナントID |
| transithub_routing_tables.name | Body | String | ルーティングテーブル名 |
| transithub_routing_tables.description | Body | String | ルーティングテーブルの説明 |
| transithub_routing_tables.transithub_id | Body | UUID | トランジットハブID |
| transithub_routing_tables.default_table | Body | Boolean | 基本ルーティングテーブルかどうか |

<details><summary>例</summary>

```json
{
  "transithub_routing_tables": [
    {
      "status": "ACTIVE",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-12 22:19:05",
      "updated_at": "2024-02-12 22:19:08",
      "default_table": true,
      "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "f5b96823-260a-415f-a162-d1914341137e",
      "name": "default-9d01afbb-0e"
    }
  ]
}
```
</details>

---
### ルーティングテーブルの表示

```
GET /v2.0/gateways/transithub_routing_tables/{routingTableId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| routingTableId | URL | UUID | O | ルーティングテーブルID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_table | Body | Object | ルーティングテーブル情報オブジェクト |
| transithub_routing_table.id | Body | UUID | ルーティングテーブルID |
| transithub_routing_table.tenant_id | Body | String | テナントID |
| transithub_routing_table.name | Body | String | ルーティングテーブル名 |
| transithub_routing_table.description | Body | String | ルーティングテーブルの説明 |
| transithub_routing_table.transithub_id | Body | UUID | トランジットハブID |
| transithub_routing_table.default_table | Body | Boolean | 基本ルーティングテーブルかどうか |

<details><summary>例</summary>

```json
{
  "transithub_routing_table": {
    "status": "ACTIVE",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "updated_at": "2024-02-12 22:19:08",
    "default_table": true,
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "f5b96823-260a-415f-a162-d1914341137e",
    "name": "default-9d01afbb-0e"
  }
}
```
</details>

---
### ルーティングテーブルを作成する

```
POST /v2.0/gateways/transithub_routing_tables
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_routing_table | Body | Object | O | ルーティングテーブル情報オブジェクト |
| transithub_routing_table.name | Body | String | - | ルーティングテーブル名 |
| transithub_routing_table.description | Body | String | - | ルーティングテーブルの説明 |
| transithub_routing_table.transithub_id | Body | UUID | O | ルーティングテーブルが登録されるトランジットハブID |

<details><summary>例</summary>

```json
{
  "transithub_routing_table": {
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub-routing-table",
    "description": null
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_table | Body | Object | ルーティングテーブル情報オブジェクト |
| transithub_routing_table.id | Body | UUID | ルーティングテーブルID |
| transithub_routing_table.tenant_id | Body | String | テナントID |
| transithub_routing_table.name | Body | String | ルーティングテーブル名 |
| transithub_routing_table.description | Body | String | ルーティングテーブルの説明 |
| transithub_routing_table.transithub_id | Body | UUID | トランジットハブID |
| transithub_routing_table.default_table | Body | Boolean | 基本ルーティングテーブルかどうか |

<details><summary>例</summary>

```json
{
  "transithub_routing_table": {
    "status": "BUILD",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-05 22:38:41",
    "updated_at": "2024-03-05 22:38:41",
    "default_table": false,
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "051eabf3-30f1-4e7a-a9bc-973c64f3c24a",
    "name": "thub-routing-table"
  }
}
```
</details>

---
### ルーティングテーブルを修正する

```
PUT /v2.0/gateways/transithub_routing_tables/{routingTableId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| routingTableId | URL | UUID | O | ルーティングテーブルID |
| transithub_routing_table | Body | Object | O | ルーティングテーブル情報オブジェクト |
| transithub_routing_table.name | Body | String | - | ルーティングテーブル名 |
| transithub_routing_table.description | Body | String | - | ルーティングテーブルの説明 |

<details><summary>例</summary>

```json
{
  "transithub_routing_table": {
    "name": "thub-routing-table1",
    "description": "test"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_table | Body | Object | ルーティングテーブル情報オブジェクト |
| transithub_routing_table.id | Body | UUID | ルーティングテーブルID |
| transithub_routing_table.tenant_id | Body | String | テナントID |
| transithub_routing_table.name | Body | String | ルーティングテーブル名 |
| transithub_routing_table.description | Body | String | ルーティングテーブルの説明 |
| transithub_routing_table.transithub_id | Body | UUID | トランジットハブID |
| transithub_routing_table.default_table | Body | Boolean | 基本ルーティングテーブルかどうか |


<details><summary>例</summary>

```json
{
  "transithub_routing_table": {
    "status": "ACTIVE",
    "description": "test",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-05 22:38:41",
    "updated_at": "2024-03-05 22:40:44.303417",
    "default_table": false,
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "051eabf3-30f1-4e7a-a9bc-973c64f3c24a",
    "name": "thub-routing-table1"
  }
}
```
</details>

---
### ルーティングテーブルを削除する

```
DELETE /v2.0/gateways/transithub_routing_tables/{routingTableId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| routingTableId | URL | UUID | O | ルーティングテーブルID |


#### レスポンス
このAPIはレスポンス本文を返しません。











## ルーティング接続

### ルーティング接続リストを表示

```
GET /v2.0/gateways/transithub_routing_associations
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するルーティング接続ID |
| attachment_id | Query | UUID | - | 照会する接続ID |
| routing_table_id | Query | UUID | - | 照会するルーティングテーブルID |



#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_associations | Body | Array | ルーティング接続情報オブジェクトリスト |
| transithub_routing_associations.id | Body | UUID | ルーティング接続ID |
| transithub_routing_associations.tenant_id | Body | String | テナントID |
| transithub_routing_associations.description | Body | String | ルーティング接続の説明 |
| transithub_routing_associations.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_routing_associations.routing_table_id | Body | UUID | ルーティングテーブルID |

<details><summary>例</summary>

```json
{
  "transithub_routing_associations": [
    {
      "status": "ACTIVE",
      "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
      "created_at": "2024-02-13 01:22:09",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "56f5c3d2-2a9f-4ada-a358-356c6387de76",
      "updated_at": "2024-02-13 01:22:09"
    }
  ]
}
```
</details>

---
### ルーティング接続を表示

```
GET /v2.0/gateways/transithub_routing_associations/{routingAssociationId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| routingAssociationId | URL | UUID | O | ルーティング接続ID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_association | Body | Object | ルーティング接続情報オブジェクト |
| transithub_routing_association.id | Body | UUID | ルーティング接続ID |
| transithub_routing_association.tenant_id | Body | String | テナントID |
| transithub_routing_association.description | Body | String | ルーティング接続の説明 |
| transithub_routing_association.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | ルーティングテーブルID |

<details><summary>例</summary>

```json
{
  "transithub_routing_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-02-13 01:22:09",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "56f5c3d2-2a9f-4ada-a358-356c6387de76",
    "updated_at": "2024-02-13 01:22:09"
  }
}
```
</details>

---
### ルーティング接続を作成する

```
POST /v2.0/gateways/transithub_routing_associations
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_routing_association | Body | Object | O | ルーティング接続情報オブジェクト |
| transithub_routing_association.description | Body | String | - | ルーティング接続の説明 |
| transithub_routing_association.attachment_id | Body | UUID | O | 接続(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | O | ルーティング接続が登録されるルーティングテーブルID |

<details><summary>例</summary>

```json
{
  "transithub_routing_association": {
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_association | Body | Object | ルーティング接続情報オブジェクト |
| transithub_routing_association.id | Body | UUID | ルーティング接続ID |
| transithub_routing_association.tenant_id | Body | String | テナントID |
| transithub_routing_association.description | Body | String | ルーティング接続の説明 |
| transithub_routing_association.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | ルーティングテーブルID |

<details><summary>例</summary>

```json
{
  "transithub_routing_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-03-05 22:51:48",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "a5532ee9-1d7b-44bd-a622-85198171ee98",
    "updated_at": "2024-03-05 22:51:48"
  }
}
```
</details>

---
### ルーティング接続を削除する

```
DELETE /v2.0/gateways/transithub_routing_associations/{routingAssociationId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| routingAssociationId | URL | UUID | O | ルーティング接続ID |


#### レスポンス
このAPIはレスポンス本文を返しません。











## ルーティング伝播

### ルーティング伝播リストを表示

```
GET /v2.0/gateways/transithub_routing_propagations
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するルーティング伝播ID |
| attachment_id | Query | UUID | - | 照会する接続ID |
| routing_table_id | Query | UUID | - | 照会するルーティングテーブルID |



#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_propagations | Body | Array | ルーティング伝播情報オブジェクトリスト |
| transithub_routing_propagations.id | Body | UUID | ルーティング伝播ID |
| transithub_routing_propagations.tenant_id | Body | String | テナントID |
| transithub_routing_propagations.description | Body | String | ルーティング伝播の説明 |
| transithub_routing_propagations.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_routing_propagations.routing_table_id | Body | UUID | ルーティングテーブルID |

<details><summary>例</summary>

```json
{
  "transithub_routing_propagations": [
    {
      "status": "ACTIVE",
      "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
      "created_at": "2024-02-13 01:22:09",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "6bf0efaa-6d32-4fef-a341-7662e9bf1eb1",
      "updated_at": "2024-02-13 01:22:09"
    }
  ]
}
```
</details>

---
### ルーティング伝播を表示

```
GET /v2.0/gateways/transithub_routing_propagations/{routingPropagationId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| routingPropagationId | URL | UUID | O | ルーティング伝播ID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_propagation | Body | Object | ルーティング伝播情報オブジェクト |
| transithub_routing_propagation.id | Body | UUID | ルーティング伝播ID |
| transithub_routing_propagation.tenant_id | Body | String | テナントID |
| transithub_routing_propagation.description | Body | String | ルーティング伝播の説明 |
| transithub_routing_propagation.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | ルーティングテーブルID |

<details><summary>例</summary>

```json
{
  "transithub_routing_propagation": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-02-13 01:22:09",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "6bf0efaa-6d32-4fef-a341-7662e9bf1eb1",
    "updated_at": "2024-02-13 01:22:09"
  }
}
```
</details>

---
### ルーティング伝播を作成する

```
POST /v2.0/gateways/transithub_routing_propagations
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_routing_propagation | Body | Object | O | ルーティング伝播情報オブジェクト |
| transithub_routing_propagation.description | Body | String | - | ルーティング伝播の説明 |
| transithub_routing_propagation.attachment_id | Body | UUID | O | 接続(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | O | ルーティング伝播が登録されるルーティングテーブルID |

<details><summary>例</summary>

```json
{
  "transithub_routing_propagation": {
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_propagation | Body | Object | ルーティング伝播情報オブジェクト |
| transithub_routing_propagation.id | Body | UUID | ルーティング伝播ID |
| transithub_routing_propagation.tenant_id | Body | String | テナントID |
| transithub_routing_propagation.description | Body | String | ルーティング伝播の説明 |
| transithub_routing_propagation.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | ルーティングテーブルID |

<details><summary>例</summary>

```json
{
  "transithub_routing_propagation": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-03-05 22:56:58",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "d1b54e63-0032-44dc-bb31-22d5723782ee",
    "updated_at": "2024-03-05 22:56:58.825231"
  }
}
```
</details>

---
### ルーティング伝播を削除する

```
DELETE /v2.0/gateways/transithub_routing_propagations/{routingPropagationId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| routingPropagationId | URL | UUID | O | ルーティング伝播ID |


#### レスポンス
このAPIはレスポンス本文を返しません。











## ルーティングルール

### ルーティングルールリストの表示

```
GET /v2.0/gateways/transithub_routing_rules
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するルーティングルールID |
| action | Query | Enum | - | 照会するルーティングルールアクション<br>`FORWARD`, `BLACKHOLE`のいずれか |
| rule_type | Query | Enum | - | 照会するルーティングルールタイプ<br>`STATIC`, `PROPAGATED`のいずれか |
| attachment_id | Query | UUID | - | 照会する接続(Attachment) ID |
| routing_table_id | Query | UUID | - | 照会するルーティングテーブルID |



#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_rules | Body | Array | ルーティングルール情報オブジェクトリスト |
| transithub_routing_rules.id | Body | UUID | ルーティングルールID |
| transithub_routing_rules.tenant_id | Body | String | テナントID |
| transithub_routing_rules.description | Body | String | ルーティングルールの説明 |
| transithub_routing_rules.cidr | Body | String | ルーティングルールIP帯域 |
| transithub_routing_rules.action | Body | Enum | ルーティングルールアクション<br>`FORWARD`, `BLACKHOLE`のいずれか |
| transithub_routing_rules.rule_type | Body | Enum | ルーティングルールタイプ<br>`STATIC`, `PROPAGATED`のいずれか |
| transithub_routing_rules.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_routing_rules.routing_table_id | Body | UUID | ルーティングテーブルID |
| transithub_routing_rules.propagation_id | Body | UUID | ルーティング伝播ID、伝播によりルーティングタイプが`PROPAGATED`の場合に使用 |

<details><summary>例</summary>

```json
{
  "transithub_routing_rules": [
    {
      "status": "ACTIVE",
      "rule_type": "PROPAGATED",
      "attachment_id": "ea9bb603-893c-4955-a7bb-64b6438a6f5b",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-12 22:35:48",
      "updated_at": "2024-02-12 22:35:48",
      "action": "FORWARD",
      "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
      "cidr": "172.16.0.0/12",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "propagation_id": "7a5d3159-a3a6-495b-bb0f-522c4d8a9933",
      "id": "3d10d565-8813-4c3c-9f1c-1af96eee9f14"
    }
  ]
}
```
</details>

---
### ルーティングルールの表示

```
GET /v2.0/gateways/transithub_routing_rules/{routingRuleId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| routingRuleId | URL | UUID | O | ルーティングルールID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_rule | Body | Object | ルーティングルール情報オブジェクト |
| transithub_routing_rule.id | Body | UUID | ルーティングルールID |
| transithub_routing_rule.tenant_id | Body | String | テナントID |
| transithub_routing_rule.description | Body | String | ルーティングルールの説明 |
| transithub_routing_rule.cidr | Body | String | ルーティングルールIP帯域 |
| transithub_routing_rule.action | Body | Enum | ルーティングルールアクション<br>`FORWARD`, `BLACKHOLE`のいずれか |
| transithub_routing_rule.rule_type | Body | Enum | ルーティングルールタイプ<br>`STATIC`, `PROPAGATED`のいずれか |
| transithub_routing_rule.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | ルーティングテーブルID |
| transithub_routing_rule.propagation_id | Body | UUID | ルーティング伝播ID、伝播によりルーティングタイプが`PROPAGATED`の場合に使用 |

<details><summary>例</summary>

```json
{
  "transithub_routing_rule": {
    "status": "ACTIVE",
    "rule_type": "PROPAGATED",
    "attachment_id": "ea9bb603-893c-4955-a7bb-64b6438a6f5b",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:35:48",
    "updated_at": "2024-02-12 22:35:48",
    "action": "FORWARD",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "cidr": "172.16.0.0/12",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "propagation_id": "7a5d3159-a3a6-495b-bb0f-522c4d8a9933",
    "id": "3d10d565-8813-4c3c-9f1c-1af96eee9f14"
  }
}
```
</details>

---
### ルーティングルールを作成する

```
POST /v2.0/gateways/transithub_routing_rules
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_routing_rule | Body | Object | O | ルーティングルール情報オブジェクト |
| transithub_routing_rule.name | Body | String | - | ルーティングルール名 |
| transithub_routing_rule.description | Body | String | - | ルーティングルールの説明 |
| transithub_routing_rule.cidr | Body | String | O | ルーティングルールIP帯域 |
| transithub_routing_rule.action | Body | Enum | - | ルーティングルールアクション<br>`FORWARD`, `BLACKHOLE`のいずれか<br>入力しない場合は`FORWARD` |
| transithub_routing_rule.attachment_id | Body | UUID | O | 接続(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | O | ルーティングルールが登録されるルーティングテーブルID |

<details><summary>例</summary>

```json
{
  "transithub_routing_rule": {
    "routing_table_id": "e5cb6442-4b5d-4298-84e2-adc9289c650e",
    "cidr": "1.1.1.0/24",
    "attachment_id": "6489cee8-0b5f-4053-b72d-1aa8b2921962"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_routing_rule | Body | Object | ルーティングルール情報オブジェクト |
| transithub_routing_rule.id | Body | UUID | ルーティングルールID |
| transithub_routing_rule.tenant_id | Body | String | テナントID |
| transithub_routing_rule.description | Body | String | ルーティングルールの説明 |
| transithub_routing_rule.cidr | Body | String | ルーティングルールIP帯域 |
| transithub_routing_rule.action | Body | Enum | ルーティングルールアクション<br>`FORWARD`, `BLACKHOLE`のいずれか |
| transithub_routing_rule.rule_type | Body | Enum | ルーティングルールタイプ<br>`STATIC`, `PROPAGATED`のいずれか |
| transithub_routing_rule.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | ルーティングテーブルID |
| transithub_routing_rule.propagation_id | Body | UUID | ルーティング伝播ID、伝播によりルーティングタイプが`PROPAGATED`の場合に使用 |

<details><summary>例</summary>

```json
{
  "transithub_routing_rule": {
    "status": "ACTIVE",
    "rule_type": "STATIC",
    "attachment_id": "6489cee8-0b5f-4053-b72d-1aa8b2921962",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-06 23:00:05",
    "updated_at": "2024-03-06 23:00:05",
    "action": "FORWARD",
    "routing_table_id": "e5cb6442-4b5d-4298-84e2-adc9289c650e",
    "cidr": "1.1.1.0/24",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "propagation_id": null,
    "id": "3f765a36-bd6a-450a-9e05-366ecb8446c3"
  }
}
```
</details>

---
### ルーティングルールを削除する

```
DELETE /v2.0/gateways/transithub_routing_rules/{routingRuleId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| routingRuleId | URL | UUID | O | ルーティングルールID |


#### レスポンス
このAPIはレスポンス本文を返しません。












## マルチキャストドメイン

### マルチキャストドメインリストの表示

```
GET /v2.0/gateways/transithub_multicast_domains
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するマルチキャストドメインID |
| name | Query | String | - | 照会するマルチキャストドメイン名 |
| transithub_id | Query | UUID | - | 照会するトランジットハブID |


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_domains | Body | Array | マルチキャストドメイン情報オブジェクトリスト |
| transithub_multicast_domains.id | Body | UUID | マルチキャストドメインID |
| transithub_multicast_domains.tenant_id | Body | String | テナントID |
| transithub_multicast_domains.name | Body | String | マルチキャストドメイン名 |
| transithub_multicast_domains.description | Body | String | マルチキャストドメインの説明 |
| transithub_multicast_domains.transithub_id | Body | UUID | トランジットハブID |

<details><summary>例</summary>
  
```json
{
  "transithub_multicast_domains": [
    {
      "status": "ACTIVE",
      "description": null,
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-13 01:20:31",
      "updated_at": "2024-02-13 01:20:32",
      "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
      "name": "thub-domain"
    }
  ]
}
```
</details>

---
### マルチキャストドメインの表示

```
GET /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| multicastDomainId | URL | UUID | O | マルチキャストドメインID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| tokenId | Header | String | トークンID |
| transithub_multicast_domain | Body | Object | マルチキャストドメイン情報オブジェクト |
| transithub_multicast_domain.name | Body | String | マルチキャストドメイン名 |
| transithub_multicast_domain.description | Body | String | マルチキャストドメインの説明 |
| transithub_multicast_domain.transithub_id | Body | UUID | マルチキャストドメインを登録するトランジットハブID |

<details><summary>例</summary>

```json
{
  "transithub_multicast_domain": {
    "status": "ACTIVE",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:20:31",
    "updated_at": "2024-02-13 01:20:32",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
    "name": "thub-domain"
  }
}
```
</details>



---
### マルチキャストドメインを作成する

```
POST /v2.0/gateways/transithub_multicast_domains
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_multicast_domain | Body | Object | O | マルチキャストドメイン情報オブジェクト |
| transithub_multicast_domain.name | Body | String | - | マルチキャストドメイン名 |
| transithub_multicast_domain.description | Body | String | - | マルチキャストドメインの説明 |
| transithub_multicast_domain.transithub_id | Body | UUID | O | マルチキャストドメインを登録するトランジットハブID |

<details><summary>例</summary>

```json
{
  "transithub_multicast_domain": {
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub-domain1"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_domain | Body | Object | マルチキャストドメイン情報オブジェクト |
| transithub_multicast_domain.id | Body | UUID | マルチキャストドメインID |
| transithub_multicast_domain.tenant_id | Body | String | テナントID |
| transithub_multicast_domain.name | Body | String | マルチキャストドメイン名 |
| transithub_multicast_domain.description | Body | String | マルチキャストドメインの説明 |
| transithub_multicast_domain.transithub_id | Body | UUID | トランジットハブID |

<details><summary>例</summary>

```json
{
  "transithub_multicast_domain": {
    "status": "BUILD",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-06 23:03:07",
    "updated_at": "2024-03-06 23:03:07",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "fba53b77-431b-466f-8a31-784942649e73",
    "name": "thub-domain1"
  }
}
```
</details>


---
### マルチキャストドメインを修正する

```
PUT /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| multicastDomainId | URL | UUID | O | マルチキャストドメインID |
| transithub_multicast_domain | Body | Object | O | マルチキャストドメイン情報オブジェクト |
| transithub_multicast_domain.name | Body | String | - | マルチキャストドメイン名 |
| transithub_multicast_domain.description | Body | String | - | マルチキャストドメインの説明 |

<details><summary>例</summary>

```json
{
  "transithub_multicast_domain": {
    "name": "thub-domain",
    "description": "test"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_domain | Body | Object | マルチキャストドメイン情報オブジェクト |
| transithub_multicast_domain.id | Body | UUID | マルチキャストドメインID |
| transithub_multicast_domain.tenant_id | Body | String | テナントID |
| transithub_multicast_domain.name | Body | String | マルチキャストドメイン名 |
| transithub_multicast_domain.description | Body | String | マルチキャストドメインの説明 |
| transithub_multicast_domain.transithub_id | Body | UUID | トランジットハブID |

<details><summary>例</summary>

```json
{
  "transithub_multicast_domain": {
    "status": "ACTIVE",
    "description": "test",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-06 23:03:07",
    "updated_at": "2024-03-06 23:06:18.031473",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "fba53b77-431b-466f-8a31-784942649e73",
    "name": "thub-domain"
  }
}
```
</details>


---
### マルチキャストドメインを削除する

```
DELETE /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| multicastDomainId | URL | UUID | O | マルチキャストドメインID |


#### レスポンス
このAPIはレスポンス本文を返しません。









## マルチキャスト接続

### マルチキャスト接続リストを表示

```
GET /v2.0/gateways/transithub_multicast_associations
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するマルチキャスト接続ID |
| name | Query | String | - | 照会するマルチキャスト接続名 |
| domain_id | Query | UUID | - | 照会するマルチキャストドメインID |


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_associations | Body | Array | マルチキャスト接続情報オブジェクトリスト |
| transithub_multicast_associations.id | Body | UUID | マルチキャスト接続ID |
| transithub_multicast_associations.tenant_id | Body | String | テナントID |
| transithub_multicast_associations.description | Body | String | マルチキャスト接続の説明 |
| transithub_multicast_associations.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_multicast_associations.subnet_id | Body | UUID | サブネットID |
| transithub_multicast_associations.domain_id | Body | UUID | マルチキャストドメインID |

<details><summary>例</summary>
  
```json
{
  "transithub_multicast_associations": [
    {
      "status": "ACTIVE",
      "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": "",
      "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-13 01:22:37",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "3da29ae0-f544-4b8e-88c4-eb2ef78d0214",
      "updated_at": "2024-02-13 01:22:37",
      "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
    }
  ]
}
```
</details>


---
### マルチキャスト接続の表示

```
GET /v2.0/gateways/transithub_multicast_associations/{multicastAssociationId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| multicastAssociationId | URL | UUID | O | ルーティングルールID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| tokenId | Header | String | トークンID |
| transithub_multicast_association | Body | Object | マルチキャスト接続情報オブジェクト |
| transithub_multicast_association.id | Body | UUID | マルチキャスト接続ID |
| transithub_multicast_association.tenant_id | Body | String | テナントID |
| transithub_multicast_association.description | Body | String | マルチキャスト接続の説明 |
| transithub_multicast_association.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_multicast_association.subnet_id | Body | UUID | サブネットID |
| transithub_multicast_association.domain_id | Body | UUID | マルチキャストドメインID |

<details><summary>例</summary>

```json
{
  "transithub_multicast_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:37",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "3da29ae0-f544-4b8e-88c4-eb2ef78d0214",
    "updated_at": "2024-02-13 01:22:37",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
  }
}
```
</details>


---
### マルチキャスト接続を作成する

```
POST /v2.0/gateways/transithub_multicast_associations
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_multicast_association | Body | Object | O | マルチキャスト接続情報オブジェクト |
| transithub_multicast_association.description | Body | String | - | マルチキャスト接続の説明 |
| transithub_multicast_association.attachment_id | Body | UUID | O | 接続(Attachment) ID |
| transithub_multicast_association.domain_id | Body | UUID | O | マルチキャストドメインID |

<details><summary>例</summary>

```json
{
  "transithub_multicast_association": {
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_association | Body | Object | マルチキャスト接続情報オブジェクト |
| transithub_multicast_association.id | Body | UUID | マルチキャスト接続ID |
| transithub_multicast_association.tenant_id | Body | String | テナントID |
| transithub_multicast_association.description | Body | String | マルチキャスト接続の説明 |
| transithub_multicast_association.attachment_id | Body | UUID | 接続(Attachment) ID |
| transithub_multicast_association.subnet_id | Body | UUID | サブネットID |
| transithub_multicast_association.domain_id | Body | UUID | マルチキャストドメインID |


<details><summary>例</summary>

```json
{
  "transithub_multicast_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-07 00:22:59",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "4da8461b-6c92-4225-8368-60e1e49e3d92",
    "updated_at": "2024-03-07 00:22:59",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
  }
}
```
</details>

---
### マルチキャスト接続を削除する

```
DELETE /v2.0/gateways/transithub_multicast_associations/{multicastAssociationId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| multicastAssociationId | URL | UUID | O | マルチキャスト接続ID |


#### レスポンス
このAPIはレスポンス本文を返しません。
















## マルチキャストグループ

### マルチキャストグループリストの表示

```
GET /v2.0/gateways/transithub_multicast_groups
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するマルチキャストグループID |
| name | Query | String | - | 照会するマルチキャストグループ名 |
| domain_id | Query | UUID | - | 照会するマルチキャストグループID |


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_groups | Body | Array | マルチキャストグループ情報オブジェクトリスト |
| transithub_multicast_groups.id | Body | UUID | マルチキャストグループID |
| transithub_multicast_groups.tenant_id | Body | String | テナントID |
| transithub_multicast_groups.description | Body | String | マルチキャストグループの説明 |
| transithub_multicast_groups.association_id | Body | UUID | マルチキャスト接続ID |
| transithub_multicast_groups.ipaddress | Body | String | マルチキャストグループIPアドレス |
| transithub_multicast_groups.member_type | Body | String | マルチキャストメンバータイプ |
| transithub_multicast_groups.source_type | Body | String | マルチキャストソースタイプ |
| transithub_multicast_groups.port_id | Body | UUID | マルチキャスト対象ポートID |

<details><summary>例</summary>
  
```json
{
  "transithub_multicast_groups": [
    {
      "description": "",
      "updated_at": "2024-03-07 00:28:20",
      "member_type": "STATIC",
      "source_type": null,
      "port_id": "b0ca1c15-13e1-4746-b8e1-9ec8e685d228",
      "ipaddress": "224.0.0.3",
      "id": "ce8c5fef-6859-4e68-8b46-4cd395c44b37",
      "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-03-07 00:28:20",
      "domain_id": "27d79c71-ccce-4928-af3c-5ffa5c3ed3fd",
      "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b"
    }
  ]
}
```
</details>

---
### マルチキャストグループの表示

```
GET /v2.0/gateways/transithub_multicast_groups/{multicastGroupId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| multicastGroupId | URL | UUID | O | マルチキャストグループID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_group | Body | Object | マルチキャストグループ情報オブジェクト |
| transithub_multicast_group.id | Body | UUID | マルチキャストグループID |
| transithub_multicast_group.tenant_id | Body | String | テナントID |
| transithub_multicast_group.description | Body | String | マルチキャストグループの説明 |
| transithub_multicast_group.association_id | Body | UUID | マルチキャスト接続ID |
| transithub_multicast_group.ipaddress | Body | String | マルチキャストグループIPアドレス |
| transithub_multicast_group.member_type | Body | String | マルチキャストメンバータイプ |
| transithub_multicast_group.source_type | Body | String | マルチキャストソースタイプ |
| transithub_multicast_group.port_id | Body | UUID | マルチキャスト対象ポートID |

<details><summary>例</summary>

```json
{
  "transithub_multicast_group": {
    "description": "",
    "updated_at": "2024-03-07 00:28:20",
    "member_type": "STATIC",
    "source_type": null,
    "port_id": "b0ca1c15-13e1-4746-b8e1-9ec8e685d228",
    "ipaddress": "224.0.0.3",
    "id": "ce8c5fef-6859-4e68-8b46-4cd395c44b37",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-07 00:28:20",
    "domain_id": "27d79c71-ccce-4928-af3c-5ffa5c3ed3fd",
    "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b"
  }
}
```
</details>

---
### マルチキャストグループを作成する

```
POST /v2.0/gateways/transithub_multicast_groups
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_multicast_group | Body | Object | O | マルチキャストグループ情報オブジェクト |
| transithub_multicast_group.description | Body | String | - | マルチキャストグループの説明 |
| transithub_multicast_group.association_id | Body | UUID | O | マルチキャスト接続ID |
| transithub_multicast_group.ipaddress | Body | String | O | マルチキャストグループIPアドレス |
| transithub_multicast_group.member_type | Body | String | - | マルチキャストメンバータイプ、メンバーとして使用する場合は`STATIC`を入力<br>メンバータイプとソースタイプのいずれかの入力必須 |
| transithub_multicast_group.source_type | Body | String | - | マルチキャストソースタイプ、ソースとして使用する場合は`STATIC`を入力<br>メンバータイプとソースタイプのいずれかの入力必須 |
| transithub_multicast_group.port_id | Body | UUID | O | マルチキャスト対象ポートID |


<details><summary>例</summary>

```json
{
  "transithub_multicast_group": {
    "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
    "port_id": "b0ca1c15-13e1-4746-b8e1-9ec8e685d228",
    "ipaddress": "224.0.0.10",
    "member_type": "STATIC"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_group | Body | Object | マルチキャストグループ情報オブジェクト |
| transithub_multicast_group.id | Body | UUID | マルチキャストグループID |
| transithub_multicast_group.tenant_id | Body | String | テナントID |
| transithub_multicast_group.description | Body | String | マルチキャストグループの説明 |
| transithub_multicast_group.association_id | Body | UUID | マルチキャスト接続ID |
| transithub_multicast_group.ipaddress | Body | String | マルチキャストグループIPアドレス |
| transithub_multicast_group.member_type | Body | String | マルチキャストメンバータイプ |
| transithub_multicast_group.source_type | Body | String | マルチキャストソースタイプ |
| transithub_multicast_group.port_id | Body | UUID | マルチキャスト対象ポートID |


<details><summary>例</summary>

```json
{
  "transithub_multicast_group": {
    "description": "",
    "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-07 00:40:19",
    "updated_at": "2024-03-07 00:40:19",
    "member_type": "STATIC",
    "domain_id": "27d79c71-ccce-4928-af3c-5ffa5c3ed3fd",
    "source_type": null,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "ipaddress": "224.0.0.10",
    "id": "91b281f8-41ab-4d27-8639-da27b23d21db"
  }
}
```
</details>


---
### マルチキャストグループを削除する

```
DELETE /v2.0/gateways/transithub_multicast_groups/{multicastGroupId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| multicastGroupId | URL | UUID | O | マルチキャストグループID |


#### レスポンス
このAPIはレスポンス本文を返しません。







## トランジットハブ共有

### 共有許可リストを表示

```
GET /v2.0/gateways/transithub_allow_projects
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会する共有許可情報ID |
| transithub_id | Query | UUID | - | 照会するトランジットハブID |


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_allow_projects | Body | Array | 共有許可情報リスト |
| transithub_allow_projects.id | Body | UUID | 共有許可情報ID |
| transithub_allow_projects.tenant_id | Body | String | テナントID |
| transithub_allow_projects.transithub_id | Body | UUID | 共有するトランジットハブID |
| transithub_allow_projects.transithub_name | Body | String | トランジットハブ名 |
| transithub_allow_projects.target_project_id | Body | UUID | 共有対象テナントID |

<details><summary>例</summary>
  
```json
{
  "transithub_allow_projects": [
    {
      "target_project_id": "cd29a534a15e46049b968dd0835b129b",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "transithub_name": "thub1",
      "transithub_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "186717d3-8e26-40ec-ad00-67a8463ccc4c"
    }
  ]
}
```
</details>

---
### 共有許可情報を作成する

```
POST /v2.0/gateways/transithub_allow_projects
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_allow_project | Body | Object | O | 共有許可情報オブジェクト |
| transithub_allow_project.transithub_id | Body | UUID | O | 共有するトランジットハブID |
| transithub_allow_project.target_project_id | Body | UUID | O | 共有対象テナントID |


<details><summary>例</summary>

```json
{
  "transithub_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "transithub_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_allow_project | Body | Object | 共有許可情報オブジェクト |
| transithub_allow_project.id | Body | UUID | 共有許可情報ID |
| transithub_allow_project.tenant_id | Body | String | テナントID |
| transithub_allow_project.transithub_id | Body | UUID | 共有するトランジットハブID |
| transithub_allow_project.transithub_name | Body | String | トランジットハブ名 |
| transithub_allow_project.target_project_id | Body | UUID | 共有対象テナントID |


<details><summary>例</summary>

```json
{
  "transithub_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "transithub_name": "dj-thub1",
    "transithub_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "3d962640-385f-4874-8766-aa1b4480e7e4"
  }
}
```
</details>


---
### 共有許可情報を削除する

```
DELETE /v2.0/gateways/transithub_allow_projects/{allowProjectId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| allowProjectId | URL | UUID | O | 共有許可情報ID |


#### レスポンス
このAPIはレスポンス本文を返しません。



### 共有されたリストを表示

```
GET /v2.0/gateways/transithub_shared_lists
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_id | Query | UUID | - | 照会するトランジットハブID |


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_shared_lists | Body | Array | 共有された情報リスト |
| transithub_shared_lists.id | Body | UUID | 共有された情報ID |
| transithub_shared_lists.tenant_id | Body | String | テナントID |
| transithub_shared_lists.transithub_id | Body | UUID | 共有されたトランジットハブID |
| transithub_shared_lists.transithub_name | Body | String | 共有されたトランジットハブ名 |
| transithub_shared_lists.transithub_project_id | Body | UUID | 共有されたトランジットハブのテナントID |

<details><summary>例</summary>
  
```json
{
  "transithub_shared_lists": [
    {
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "transithub_project_id": "1fb0cf13afb341b699f74bbbecab2117",
      "transithub_name": "thub",
      "transithub_id": "4050efd6-b6cc-4e2d-9402-dd5e1520872f",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "51c8fd9c-ae82-474f-9664-9fc31c77a563"
    }
  ]
}
```
</details>







## マルチキャストドメイン共有

### 共有許可リストを表示

```
GET /v2.0/gateways/transithub_multicast_domain_allow_projects
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会する共有許可情報ID |
| domain_id | Query | UUID | - | 照会するマルチキャストドメインID |


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_domain_allow_projects | Body | Array | 共有許可情報リスト |
| transithub_multicast_domain_allow_projects.id | Body | UUID | 共有許可情報ID |
| transithub_multicast_domain_allow_projects.tenant_id | Body | String | テナントID |
| transithub_multicast_domain_allow_projects.domain_id | Body | UUID | 共有するマルチキャストドメインID |
| transithub_multicast_domain_allow_projects.domain_name | Body | String | マルチキャストドメイン名 |
| transithub_multicast_domain_allow_projects.target_project_id | Body | UUID | 共有対象テナントID |

<details><summary>例</summary>

```json
{
  "transithub_multicast_domain_allow_projects": [
    {
      "target_project_id": "cd29a534a15e46049b968dd0835b129b",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "domain_name": "domain1",
      "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "186717d3-8e26-40ec-ad00-67a8463ccc4c"
    }
  ]
}
```
</details>

---
### 共有許可情報を作成する

```
POST /v2.0/gateways/transithub_multicast_domain_allow_projects
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| transithub_multicast_domain_allow_project | Body | Object | O | 共有許可情報オブジェクト |
| transithub_multicast_domain_allow_project.domain_id | Body | UUID | O | 共有するマルチキャストドメインID |
| transithub_multicast_domain_allow_project.target_project_id | Body | UUID | O | 共有対象テナントID |


<details><summary>例</summary>

```json
{
  "transithub_multicast_domain_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "domain_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_domain_allow_project | Body | Object | 共有許可情報オブジェクト |
| transithub_multicast_domain_allow_project.id | Body | UUID | 共有許可情報ID |
| transithub_multicast_domain_allow_project.tenant_id | Body | String | テナントID |
| transithub_multicast_domain_allow_project.domain_id | Body | UUID | 共有するマルチキャストドメインID |
| transithub_multicast_domain_allow_project.domain_name | Body | String | マルチキャストドメイン名 |
| transithub_multicast_domain_allow_project.target_project_id | Body | UUID | 共有対象テナントID |


<details><summary>例</summary>

```json
{
  "transithub_multicast_domain_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "domain_name": "domain1",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "3d962640-385f-4874-8766-aa1b4480e7e4"
  }
}
```
</details>


---
### 共有許可情報を削除する

```
DELETE /v2.0/gateways/transithub_multicast_domain_allow_projects/{allowProjectId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| allowProjectId | URL | UUID | O | 共有許可情報ID |


#### レスポンス
このAPIはレスポンス本文を返しません。



### 共有されたリストを表示

```
GET /v2.0/gateways/transithub_multicast_domain_shared_lists
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| domain_id | Query | UUID | - | 照会するマルチキャストドメインID |


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| transithub_multicast_domain_shared_lists | Body | Array | 共有された情報リスト |
| transithub_multicast_domain_shared_lists.id | Body | UUID | 共有された情報ID |
| transithub_multicast_domain_shared_lists.tenant_id | Body | String | テナントID |
| transithub_multicast_domain_shared_lists.domain_id | Body | UUID | 共有されたマルチキャストドメインID |
| transithub_multicast_domain_shared_lists.domain_name | Body | String | 共有されたマルチキャストドメイン名 |
| transithub_multicast_domain_shared_lists.domain_project_id | Body | UUID | 共有されたマルチキャストドメインのテナントID |

<details><summary>例</summary>

```json
{
  "transithub_multicast_domain_shared_lists": [
    {
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "domain_project_id": "1fb0cf13afb341b699f74bbbecab2117",
      "domain_name": "domain1",
      "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "51c8fd9c-ae82-474f-9664-9fc31c77a563"
    }
  ]
}
```
</details>
