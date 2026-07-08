
## Network > Colocation Gateway > API v2ガイド

NHN Cloud Networkサービスは、API呼び出し時の認証/認可のためにIaaSトークンを使用します。IaaSトークンは、NHN CloudのOpenStackベースのインフラサービス(IaaS)で使用する認証トークンです。IaaSトークンの発行及び使用に関する詳細は、[IaaSトークン](/nhncloud/ja/public-api/iaas-token)を参照してください。

コロケーションゲートウェイAPIは`network`タイプエンドポイントを利用します。正確なエンドポイントはトークン発行レスポンスの`serviceCatalog`を参照してください。

| タイプ | リージョン | エンドポイント |
|---|---|---|
| network | 韓国(パンギョ)リージョン<br>韓国(ピョンチョン)リージョン<br>韓国(光州)リージョン | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

APIレスポンスにガイドに記載されていないフィールドが表示される場合があります。このようなフィールドは、NHN Cloudの内部用途に使用され、事前告知なしに変更される可能性があるため、使用しないでください。

## コロケーションゲートウェイ

### コロケーションゲートウェイリスト表示

```
GET /v2.0/gateways/colocationgateways
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するコロケーションゲートウェイID |
| name | Query | String | - | 照会するコロケーションゲートウェイ名 |
| vpc_id | Query | String | - | 照会するコロケーションゲートウェイと接続されたVPC ID |


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| colocationgateways | Body | Array | コロケーションゲートウェイ情報オブジェクトリスト |
| colocationgateways.id | Body | UUID | コロケーションゲートウェイID |
| colocationgateways.name | Body | String | コロケーションゲートウェイ名 |
| colocationgateways.vpc_id | Body | UUID | 接続されたVPC ID |
| colocationgateways.tenant_id | Body | String | テナントID |
| colocationgateways.status | Body | UUID | リソース状態 |
| colocationgateways.description | Body | String | コロケーションゲートウェイの説明 |
| colocationgateways.vpc.name | Body | String | 接続されたVPC名 |
| colocationgateways.vpc.id | Body | String | 接続されたVPC ID |
| colocationgateways.vpc.cidrv4 | Body | String | 接続されたVPC CIDR |

<details><summary>例</summary>

```json
{
  "colocationgateways": [
    {
      "status": "AVAILABLE",
      "name": "test",
      "vpc": {
        "name": "Test Network",
        "id": "273c5003-436a-111-8318-b5f824ac55b2",
        "cidrv4": "192.168.1.0/24"
      },
      "vpc_id": "273c5003-436a-1111-8318-b5f824ac55b2",
      "tenant_id": "626931f748704725b3640afab6e70000",
      "project_id": "626931f748704725b3640afab6e70000",
      "id": "1b8b2ace-1111-421d-b2ae-5f508c98ccd9",
      "description": "test"
    }
  ]
}
```
</details>

---
### コロケーションゲートウェイ表示

```
GET /v2.0/gateways/colocationgateways/{colocationGatewayId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| colocationGatewayId | URL | UUID | O | コロケーションゲートウェイID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| colocationgateways | Body | Array | コロケーションゲートウェイ情報オブジェクトリスト |
| colocationgateways.id | Body | UUID | コロケーションゲートウェイID |
| colocationgateways.name | Body | String | コロケーションゲートウェイ名 |
| colocationgateways.vpc_id | Body | UUID | 接続されたVPC ID |
| colocationgateways.tenant_id | Body | String | テナントID |
| colocationgateways.status | Body | UUID | リソース状態 |
| colocationgateways.description | Body | String | コロケーションゲートウェイの説明 |
| colocationgateways.vpc.name | Body | String | 接続されたVPC名 |
| colocationgateways.vpc.id | Body | String | 接続されたVPC ID |
| colocationgateways.vpc.cidrv4 | Body | String | 接続されたVPC CIDR |

<details><summary>例</summary>

```json
{
  "colocationgateway": {
    "status": "AVAILABLE",
    "name": "test",
    "vpc": {
      "name": "Test Network",
      "id": "273c5003-436a-111-8318-b5f824ac55b2",
      "cidrv4": "192.168.1.0/24"
    },
    "vpc_id": "273c5003-436a-1111-8318-b5f824ac55b2",
    "tenant_id": "626931f748704725b3640afab6e70000",
    "project_id": "626931f748704725b3640afab6e70000",
    "id": "1b8b2ace-1111-421d-b2ae-5f508c98ccd9",
    "description": "test"
  }
}
```
</details>
