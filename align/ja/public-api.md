## Network > NAT Gateway > API v2ガイド

NHN Cloud Networkサービスは、API呼び出し時の認証/認可のためにIaaSトークンを使用します。IaaSトークンは、NHN CloudのOpenStackベースのインフラサービス(IaaS)で使用する認証トークンです。IaaSトークンの発行及び使用に関する詳細は、[IaaSトークン](/nhncloud/ja/public-api/iaas-token)を参照してください。

NATゲートウェイAPIは`network`タイプエンドポイントを利用します。正確なエンドポイントはトークン発行レスポンスの`serviceCatalog`を参照します。

| タイプ | リージョン                                | エンドポイント                                                                                                                      |
|---|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| network | 韓国(パンギョ)リージョン<br>韓国(ピョンチョン)リージョン<br>韓国(光州)リージョン | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

APIレスポンスにガイドに記載されていないフィールドが表示される場合があります。このようなフィールドは、NHN Cloudの内部用途に使用され、事前告知なしに変更される可能性があるため、使用しないでください。


## NATゲートウェイ
### NATゲートウェイ一覧を表示
```
GET /v2.0/natgateways
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明                                                                           |
|---|---|---|---|--------------------------------------------------------------------------------|
| tokenId | Header | String | O | トークンID                                                                          |
| id | Query | UUID | - | 照会するNATゲートウェイID                                                               |
| tenant_id | Query | String | - | 照会するNATゲートウェイのテナントID                                                          |
| name | Query | String | - | 照会するNATゲートウェイの名前                                                            |
| sort_dir | Query | Enum | - | 照会するNATゲートウェイのソート方向<br>`sort_key`で指定したフィールドを基準にソート<br>**asc**、**desc**のいずれか |
| sort_key | Query | String | - | 照会するNATゲートウェイのソートキー<br>`sort_dir`で指定した方向でソート                              |
| fields | Query | String | - | 照会するNATゲートウェイのフィールド名<br>例：`fields=id&fields=name`                             |

#### レスポンス

| 名前                       | 種類 | 形式 | 説明                                           |
|----------------------------|---|---|------------------------------------------------|
| natgateways                | Body | Array | NATゲートウェイ情報オブジェクトリスト                           |
| natgateways.id             | Body | UUID | NATゲートウェイのID                                  |
| natgateways.name           | Body | String | NATゲートウェイ名                                 |
| natgateways.vpc_id         | Body | UUID | NATゲートウェイのVPC ID                              |
| natgateways.subnet_id      | Body | UUID | NATゲートウェイのサブネットID                              |
| natgateways.port_id        | Body | UUID | NATゲートウェイのポートID                               |
| natgateways.floatingips_id | Body | UUID | NATゲートウェイのフローティングIP ID                           |
| natgateways.tenant_id      | Body | String | NATゲートウェイのテナントID                              |
| natgateways.project_id     | Body | String | NATゲートウェイのプロジェクトID。テナントIDと同じ。                |
| natgateways.fixed_ip       | Body | String | NATゲートウェイの固定IPアドレス                          |
| natgateways.floating_ip    | Body | String | NATゲートウェイのフローティングIPアドレス                         |
| natgateways.create_time    | Body | String | NATゲートウェイ作成時間(UTC基準)                       |
| natgateways.description    | Body | String | NATゲートウェイの説明                                 |
| natgateways.status         | Body | Enum | NATゲートウェイの状態<br>`ACTIVE`, `BUILD`, `ERROR`のいずれか。 |


<details><summary>例</summary>
<p>

```json
{
  "natgateways": [
    {
      "status": "ACTIVE",
      "description": "",
      "floatingips_id": "16e1411c-315f-4eb6-bbf7-29654aaba0b6",
      "floating_ip": "133.186.243.20",
      "create_time": "2025-02-24 06:20:36",
      "port_id": "fac6acaf-af3f-4f22-889d-7e768e6808f8",
      "id": "aaabd5cb-ca65-416e-8f6e-2f9e4d62d8d6",
      "name": "natgw-1",
      "tenant_id": "76841f7d054a40b88b2a99828280998c",
      "fixed_ip": "172.16.10.90",
      "vpc_id": "2c590fdf-993d-4377-a49b-a54f66759909",
      "subnet_id": "119fcc8c-c4da-48a4-9b12-690388ac5686",
      "project_id": "76841f7d054a40b88b2a99828280998c"
    }
  ]
}
```

</p>
</details>

---

### NATゲートウェイ表示
```
GET /v2.0/natgateways/{NatGatewayId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類   | 形式   | 必須 | 説明                                                                 |
|---|--------|--------|---|----------------------------------------------------------------------|
| NatGatewayId | URL    | UUID   | O | NATゲートウェイID                                                         |
| tokenId | Header | String | O | トークンID                                                                |
| fields | Query  | String | - | 照会するNATゲートウェイのフィールド名<br>指定したフィールドのみレスポンスに返す<br>例：`fields=id&fields=name` |

#### レスポンス

| 名前                      | 種類 | 形式 | 説明                                             |
|---------------------------|---|---|--------------------------------------------------|
| natgateway                | Body | Array | NATゲートウェイ情報オブジェクト                                |
| natgateway.id             | Body | UUID | NATゲートウェイのID                                   |
| natgateway.name           | Body | String | NATゲートウェイ名                                  |
| natgateway.vpc_id         | Body | UUID | NATゲートウェイのVPC ID                               |
| natgateway.subnet_id      | Body | UUID | NATゲートウェイのサブネットID                               |
| natgateway.port_id        | Body | UUID | NATゲートウェイのポートID                                |
| natgateway.floatingips_id | Body | UUID | NATゲートウェイのフローティングIP ID                            |
| natgateway.tenant_id      | Body | String | NATゲートウェイのテナントID                               |
| natgateway.project_id     | Body | String | NATゲートウェイのプロジェクトID. テナントIDと同じ。                 |
| natgateway.fixed_ip       | Body | String | NATゲートウェイの固定IPアドレス                           |
| natgateway.floating_ip    | Body | String | NATゲートウェイのフローティングIPアドレス                          |
| natgateway.create_time    | Body | String | NATゲートウェイ作成時間(UTC基準)                            |
| natgateway.description    | Body | String | NATゲートウェイの説明                                  |
| natgateway.status         | Body | Enum | NATゲートウェイの状態<br>`ACTIVE`, `BUILD`, `ERROR`のいずれか。 |


<details><summary>例</summary>
<p>

```json
{
  "natgateway": {
    "status": "ACTIVE",
    "description": "",
    "floatingips_id": "16e1411c-315f-4eb6-bbf7-29654aaba0b6",
    "floating_ip": "133.186.243.20",
    "create_time": "2025-02-24 06:20:36",
    "id": "aaabd5cb-ca65-416e-8f6e-2f9e4d62d8d6",
    "name": "natgw-1",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "vpc_id": "2c590fdf-993d-4377-a49b-a54f66759909",
    "subnet_id": "119fcc8c-c4da-48a4-9b12-690388ac5686",
    "port_id": "fac6acaf-af3f-4f22-889d-7e768e6808f8",
    "fixed_ip": "172.16.10.90",
    "project_id": "76841f7d054a40b88b2a99828280998c"
  }
}
```

</p>
</details>

---
### NATゲートウェイの作成

新しいNATゲートウェイを作成します。

```
POST /v2.0/natgateways
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前                      | 種類 | 形式   | 必須 | 説明                 |
|---------------------------|---|--------|----|----------------------|
| tokenId                   | Header | String | O  | トークンID                |
| natgateway                | Body | Object | O  | NATゲートウェイ作成リクエストオブジェクト |
| natgateway.name           | Body | String | O  | NATゲートウェイ名       |
| natgateway.vpc_id         | Body | UUID   | O  | NATゲートウェイのVPC ID    |
| natgateway.subnet_id      | Body | UUID   | O  | NATゲートウェイのサブネットID    |
| natgateway.floatingips_id | Body | UUID   | O  | NATゲートウェイのフローティングIP ID |
| natgateway.description    | Body | String | -  | NATゲートウェイの説明       |



<details><summary>例</summary>
<p>

```json
{
  "natgateway": {
    "name": "natgw-1",
    "description": "",
    "vpc_id": "1031ad94-425a-4d23-9833-d6f19de30c1e",
    "subnet_id": "f70ae850-3f8a-4fab-9b57-926871bd2c27",
    "floatingips_id": "fdef9dc2-d8d7-480d-9bf3-754e9e73da39"
  }
}
```

</p>
</details>


#### レスポンス
| 名前                      | 種類 | 形式 | 説明                                             |
|---------------------------|---|---|--------------------------------------------------|
| natgateway                | Body | Array | NATゲートウェイ情報オブジェクト                                |
| natgateway.id             | Body | UUID | NATゲートウェイのID                                   |
| natgateway.name           | Body | String | NATゲートウェイ名                                  |
| natgateway.vpc_id         | Body | UUID | NATゲートウェイのVPC ID                               |
| natgateway.subnet_id      | Body | UUID | NATゲートウェイのサブネットID                               |
| natgateway.port_id        | Body | UUID | NATゲートウェイのポートID                                |
| natgateway.floatingips_id | Body | UUID | NATゲートウェイのフローティングIP ID                            |
| natgateway.tenant_id      | Body | String | NATゲートウェイのテナントID                               |
| natgateway.project_id     | Body | String | NATゲートウェイのプロジェクトID. テナントIDと同じ。                 |
| natgateway.fixed_ip       | Body | String | NATゲートウェイの固定IPアドレス                           |
| natgateway.floating_ip    | Body | String | NATゲートウェイのフローティングIPアドレス                          |
| natgateway.create_time    | Body | String | NATゲートウェイ作成時間(UTC基準)                               |
| natgateway.description    | Body | String | NATゲートウェイの説明                                  |
| natgateway.status         | Body | Enum | NATゲートウェイの状態<br>`ACTIVE`, `BUILD`, `ERROR`のいずれか。 |


<details><summary>例</summary>
<p>

```json
{
  "natgateway": {
    "status": "BUILD",
    "description": "",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "floatingips_id": "fdef9dc2-d8d7-480d-9bf3-754e9e73da39",
    "floating_ip": "133.186.243.6",
    "id": "c3df608d-5f38-4baf-b24e-27da20a4c579",
    "name": "natgw-1",
    "create_time": "2025-04-08 22:30:15",
    "vpc_id": "1031ad94-425a-4d23-9833-d6f19de30c1e",
    "subnet_id": "f70ae850-3f8a-4fab-9b57-926871bd2c27",
    "port_id": "0c61cf46-d2bc-4583-ad96-91892a190b0e",
    "fixed_ip": "192.168.10.111",
    "project_id": "76841f7d054a40b88b2a99828280998c"
  }
}
```

</p>
</details>

---
### NATゲートウェイの修正

既存NATゲートウェイを修正します。

```
PUT /v2.0/natgateways/{NatGatewayId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前                      | 種類 | 形式   | 必須 | 説明               |
|---------------------------|---|--------|----|--------------------|
| NatGatewayId | URL    | UUID   | O  | NATゲートウェイID       |
| tokenId                   | Header | String | O  | トークンID              |
| natgateway                | Body | Object | O  | NATゲートウェイ作成リクエストオブジェクト |
| natgateway.name           | Body | String | -  | NATゲートウェイ名     |
| natgateway.description    | Body | String | -  | NATゲートウェイの説明     |



<details><summary>例</summary>
<p>

```json
{
  "natgateway": {
    "name": "natgw-2",
    "description": "TEST NAT Gateway"
  }
}
```

</p>
</details>


#### レスポンス
| 名前                      | 種類 | 形式 | 説明                                            |
|---------------------------|---|---|-------------------------------------------------|
| natgateway                | Body | Array | NATゲートウェイ情報オブジェクト                               |
| natgateway.id             | Body | UUID | NATゲートウェイのID                                   |
| natgateway.name           | Body | String | NATゲートウェイ名                                  |
| natgateway.vpc_id         | Body | UUID | NATゲートウェイのVPC ID                               |
| natgateway.subnet_id      | Body | UUID | NATゲートウェイのサブネットID                               |
| natgateway.port_id        | Body | UUID | NATゲートウェイのポートID                                |
| natgateway.floatingips_id | Body | UUID | NATゲートウェイのフローティングIP ID                            |
| natgateway.tenant_id      | Body | String | NATゲートウェイのテナントID                               |
| natgateway.project_id     | Body | String | NATゲートウェイのプロジェクトID. テナントIDと同じ。                 |
| natgateway.fixed_ip       | Body | String | NATゲートウェイの固定IPアドレス                           |
| natgateway.floating_ip    | Body | String | NATゲートウェイのフローティングIPアドレス                          |
| natgateway.create_time    | Body | String | NATゲートウェイ作成時間(UTC基準)                         |
| natgateway.description    | Body | String | NATゲートウェイの説明                                  |
| natgateway.status         | Body | Enum | NATゲートウェイの状態<br>`ACTIVE`, `BUILD`, `ERROR`のいずれか。 |


<details><summary>例</summary>
<p>

```json
{
  "natgateway": {
    "status": "ACTIVE",
    "description": "TEST NAT Gateway",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "floatingips_id": "fdef9dc2-d8d7-480d-9bf3-754e9e73da39",
    "floating_ip": "133.186.243.6",
    "id": "c3df608d-5f38-4baf-b24e-27da20a4c579",
    "name": "natgw-2",
    "create_time": "2025-04-08 22:30:15",
    "vpc_id": "1031ad94-425a-4d23-9833-d6f19de30c1e",
    "subnet_id": "f70ae850-3f8a-4fab-9b57-926871bd2c27",
    "port_id": "0c61cf46-d2bc-4583-ad96-91892a190b0e",
    "fixed_ip": "192.168.10.111",
    "project_id": "76841f7d054a40b88b2a99828280998c"
  }
}
```

</p>
</details>

---
### NATゲートウェイの削除
指定したNATゲートウェイを削除します。
```
DELETE /v2.0/natgateways/{NatGatewayId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| NatGatewayId | URL    | UUID   | O  | NATゲートウェイID       |
| tokenId | Header | String | O | トークンID |

#### レスポンス
このAPIはレスポンス本文を返しません。
