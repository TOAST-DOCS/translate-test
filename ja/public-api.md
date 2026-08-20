<!-- machine_translated: true -->

<!-- pre-align:aligned sig=fbbff493af43 -->

<a id="network-service-gateway-api-v2-guide"></a>
## Network > Service Gateway > API v2ガイド { #network-service-gateway-api-v2-guide }

NHN Cloud Networkサービスは、API呼び出し時の認証/認可のためにIaaSトークンを使用します。IaaSトークンは、NHN CloudのOpenStackベースのインフラサービス(IaaS)で使用する認証トークンです。IaaSトークンの発行及び使用に関する詳細は、[IaaSトークン](/nhncloud/ja/public-api/iaas-token)を参照してください。

サービスゲートウェイAPIは`network`タイプエンドポイントを利用します。正確なエンドポイントはトークン発行レスポンスの`serviceCatalog`を参照します。

| タイプ | リージョン | エンドポイント |
|---|---|---|
| network | 韓国(パンギョ)リージョン<br>韓国(ピョンチョン)リージョン<br>韓国(光州)リージョン | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

APIレスポンスにガイドに記載されていないフィールドが表示される場合があります。このようなフィールドは、NHN Cloudの内部用途に使用され、事前告知なしに変更される可能性があるため、使用しないでください。

<a id="service-gateway"></a>
## サービスゲートウェイ { #service-gateway }

<a id="get-a-list-of-service-gateways"></a>
### サービスゲートウェイリスト表示 { #get-a-list-of-service-gateways }

```
GET /v2.0/gateways/servicegateways
X-Auth-Token: {tokenId}
```

<a id="get-a-list-of-service-gateways-request"></a>
#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するサービスゲートウェイID |
| name | Query | String | - | 照会するサービスゲートウェイ名 |
| service_endpoint_id | Query | UUID | - | 照会するサービスゲートウェイのサービスエンドポイント（またはユーザー定義エンドポイント）ID |
| network_id | Query | UUID | - | 照会するサービスゲートウェイVPC ID |
| subnet_id | Query | UUID | - | 照会するサービスゲートウェイサブネットID |
| port_id | Query | UUID | - | 照会するサービスゲートウェイポートID |
| fixed_ip| Query | String | - | 照会するサービスゲートウェイIPアドレス |
| include_gateway_identity| Query | Boolean | - | NAT IPアドレス固定の使用有無 |


<a id="get-a-list-of-service-gateways-response"></a>
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| servicegateways.id | Body | UUID | サービスゲートウェイID |
| servicegateways.name | Body | String | サービスゲートウェイ名 |
| servicegateways.port_id | Body | UUID | ポートID |
| servicegateways.tenant_id | Body | String | テナントID |
| servicegateways.network_id | Body | UUID | VPC ID |
| servicegateways.subnet_id | Body | UUID | サブネットID |
| servicegateways.fixed_ip | Body | String | サービスゲートウェイIPアドレス |
| servicegateways.include_gateway_identity| Body | Boolean | NAT IPアドレス固定の使用有無 |
| servicegateways.service_endpoint_id | Body | UUID | サービスエンドポイント（またはユーザー定義エンドポイント）ID |
| servicegateways.service_endpoint_id | Body | UUID | サービスエンドポイント（またはユーザー定義エンドポイント）ID |
| servicegateways.service_provider | Body | String | 接続タイプ（接続されたエンドポイントの値）。`csp`=サービスエンドポイント / `user`=ユーザー定義エンドポイント |
| servicegateways.description | Body | String | サービスゲートウェイの説明 |

<details><summary>例</summary>

```json
{
  "servicegateways": [
    {
      "status": "AVAILABLE",
      "include_gateway_identity": true,
      "description": "",
      "network_id": "55529e1d-c6ee-4be8-baa9-2b6546667e6d",
      "tenant_id": "302406c4a1d44b2cb2bc07a652c0b202",
      "fixed_ip": "192.168.0.82",
      "subnet_id": "72d9d6e0-3ee2-4287-bcf9-be45a8422ff1",
      "service_endpoint_id": "7ba5b6e7-d871-43d3-90d2-7e2beecaaae5",
      "service_provider": "csp",
      "create_time": "2023-08-31 02:11:09",
      "project_id": "302406c4a1d44b2cb2bc07a652c0b202",
      "port_id": "182a31be-9e29-400d-983b-f701cf9b4bbc",
      "id": "d383a4a3-dae7-4609-b2db-ecdf5859fac5",
      "name": "sgw_test"
    }
  ]
}
```

</details>

---
<a id="get-a-service-gateway"></a>
### サービスゲートウェイ表示 { #get-a-service-gateway }

```
GET /v2.0/gateways/servicegateways/{serviceGatewayId}
X-Auth-Token: {tokenId}
```

<a id="get-a-service-gateway-request"></a>
#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| serviceGatewayId | URL | UUID | O | サービスゲートウェイID |

<a id="get-a-service-gateway-response"></a>
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| servicegateway | Body | Object | サービスゲートウェイ情報オブジェクト |
| servicegateway.id | Body | UUID | サービスゲートウェイID |
| servicegateway.name | Body | String | サービスゲートウェイ名 |
| servicegateway.port_id | Body | UUID | ポート ID |
| servicegateway.tenant_id | Body | String | テナント ID |
| servicegateway.network_id | Body | UUID | VPC ID |
| servicegateway.subnet_id | Body | UUID | サブネット ID |
| servicegateway.fixed_ip | Body | String | サービスゲートウェイの IP アドレス |
| servicegateway.include_gateway_identity| Body | Boolean | NAT IPアドレスの固定使用有無 |
| servicegateway.service_endpoint_id | Body | UUID | サービスエンドポイント(またはユーザー定義エンドポイント) ID |
| servicegateway.service_provider | Body | String | 接続タイプ（接続されたエンドポイントの値）。`csp`=サービスエンドポイント / `user`=ユーザー定義エンドポイント |
| servicegateway.api_endpoints | Body | Array | APIエンドポイント情報オブジェクトリスト |
| servicegateway.api_endpoints.domain_name | Body | String | APIエンドポイントドメイン |
| servicegateway.description | Body | String | サービスゲートウェイの説明 |
<details><summary>例</summary>

```json
{
  "servicegateway": {
    "status": "AVAILABLE",
    "include_gateway_identity": true,
    "description": "",
    "network_id": "55529e1d-c6ee-4be8-baa9-2b6546667e6d",
    "tenant_id": "302406c4a1d44b2cb2bc07a652c0b202",
    "fixed_ip": "192.168.0.82",
    "subnet_id": "72d9d6e0-3ee2-4287-bcf9-be45a8422ff1",
    "api_endpoints": [
      {
        "domain_name": "test.test.com"
      }
    ],
    "service_endpoint_id": "7ba5b6e7-d871-43d3-90d2-7e2beecaaae5",
    "service_provider": "csp",
    "create_time": "2023-08-31 02:11:09",
    "project_id": "302406c4a1d44b2cb2bc07a652c0b202",
    "port_id": "182a31be-9e29-400d-983b-f701cf9b4bbc",
    "id": "d383a4a3-dae7-4609-b2db-ecdf5859fac5",
    "name": "sgw_test"
  }
}
```

</details>

---
<a id="create-a-service-gateway"></a>
### サービスゲートウェイを作成する { #create-a-service-gateway }

```
POST /v2.0/gateways/servicegateways
X-Auth-Token: {tokenId}
```

<a id="create-a-service-gateway-request"></a>
#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| servicegateway | Body | Object | O | サービスゲートウェイ情報オブジェクト |
| servicegateway.name | Body | String | - | サービスゲートウェイ名 |
| servicegateway.description | Body | String | - | サービスゲートウェイの説明 |
| servicegateway.network_id | Body | UUID | O | VPC ID |
| servicegateway.subnet_id | Body | UUID | O | サブネット ID |
| servicegateway.fixed_ip | Body | String | - | サービスゲートウェイの IP アドレス |
| servicegateway.include_gateway_identity| Body | Boolean | - | NAT IPアドレス固定使用の有無 |
| servicegateway.service_endpoint_id | Body | UUID | O | サービスエンドポイント（またはユーザー定義エンドポイント）ID |
> ユーザー定義エンドポイントに接続するには、パブリッシャーから受け取った `service_name` を使用して[サービスエンドポイントリスト表示](#get-a-list-of-service-endpoints)を照会して取得した `service_endpoint_id` を使用します。接続タイプ（`service_provider`）は接続先エンドポイントから自動的に決定されるため、リクエスト値として指定しません。

<details><summary>例</summary>

```json
{
  "servicegateway": {
    "network_id": "55529e1d-c6ee-4be8-baa9-2b6546667e6d",
    "subnet_id": "72d9d6e0-3ee2-4287-bcf9-be45a8422ff1",
    "fixed_ip": "192.168.0.82",
    "service_endpoint_id": "7ba5b6e7-d871-43d3-90d2-7e2beecaaae5",
    "name": "sgw_test",
    "description": "test"
  }
}
```

</details>

<a id="create-a-service-gateway-response"></a>
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| servicegateway | Body | Object | サービスゲートウェイ情報オブジェクトリスト |
| servicegateway.id | Body | UUID | サービスゲートウェイID |
| servicegateway.name | Body | String | サービスゲートウェイ名 |
| servicegateway.port_id | Body | UUID | ポートID |
| servicegateway.tenant_id | Body | String | テナントID |
| servicegateway.network_id | Body | UUID | VPC ID |
| servicegateway.subnet_id | Body | UUID | サブネット ID |
| servicegateway.fixed_ip | Body | String | サービスゲートウェイの IP アドレス |
| servicegateway.include_gateway_identity| Body | Boolean | NAT IPアドレス固定の使用有無 |
| servicegateway.service_endpoint_id | Body | UUID | サービスエンドポイント（またはユーザー定義エンドポイント）ID |
| servicegateway.service_provider | Body | String | 接続タイプ（接続されたエンドポイントの値）。`csp`=サービスエンドポイント / `user`=ユーザー定義エンドポイント |
| servicegateway.api_endpoints | Body | Array | APIエンドポイント情報オブジェクトのリスト |
| servicegateway.api_endpoints.domain_name | Body | String | APIエンドポイントドメイン |
| servicegateway.description | Body | String | サービスゲートウェイの説明 |
<details><summary>例</summary>

```json
{
  "servicegateway": {
    "status": "BUILD",
    "include_gateway_identity": false,
    "description": "",
    "network_id": "55529e1d-c6ee-4be8-baa9-2b6546667e6d",
    "tenant_id": "302406c4a1d44b2cb2bc07a652c0b202",
    "fixed_ip": "192.168.0.82",
    "subnet_id": "72d9d6e0-3ee2-4287-bcf9-be45a8422ff1",
    "api_endpoints": [
      {
        "domain_name": "test.test.com"
      }
    ],
    "service_endpoint_id": "7ba5b6e7-d871-43d3-90d2-7e2beecaaae5",
    "service_provider": "csp",
    "create_time": "2023-08-31 02:11:09",
    "project_id": "302406c4a1d44b2cb2bc07a652c0b202",
    "port_id": "182a31be-9e29-400d-983b-f701cf9b4bbc",
    "id": "d383a4a3-dae7-4609-b2db-ecdf5859fac5",
    "name": "sgw_test"
  }
}
```

</details>

---
<a id="modify-a-service-gateway"></a>
### サービスゲートウェイを修正する { #modify-a-service-gateway }

```
PUT /v2.0/gateways/servicegateways/{serviceGatewayId}
X-Auth-Token: {tokenId}
```

<a id="modify-a-service-gateway-request"></a>
#### リクエスト

| tokenId | Header | String | O | トークンID |
| serviceGatewayId | URL | UUID | O | サービスゲートウェイID |
| serviceGatewayId | URL | UUID | O | サービスゲートウェイID |
| servicegateway | Body | Object | O | サービスゲートウェイ情報オブジェクト |
| servicegateway.name | Body | String | - | サービスゲートウェイ名 |
| servicegateway.description | Body | String | - | サービスゲートウェイの説明 |

> 接続タイプ (`service_provider`) は、接続されたエンドポイントの値を示す読み取り専用の項目であり、サービスゲートウェイの変更では修正できません。

<details><summary>例</summary>

```json
{
  "servicegateway": {
    "name": "sgw_test1",
    "description": "test1"
  }
}
```

</details>

<a id="modify-a-service-gateway-response"></a>
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| servicegateway | Body | Object | サービスゲートウェイ情報オブジェクト |
| servicegateway.id | Body | UUID | サービスゲートウェイ ID |
| servicegateway.name | Body | String | サービスゲートウェイ名 |
| servicegateway.port_id | Body | UUID | ポートID |
| servicegateway.tenant_id | Body | String | テナントID |
| servicegateway.network_id | Body | UUID | VPC ID |
| servicegateway.subnet_id | Body | UUID | サブネット ID |
| servicegateway.fixed_ip | Body | String | サービスゲートウェイの IP アドレス |
| servicegateway.include_gateway_identity| Body | Boolean | NAT IPアドレスの固定使用有無 |
| servicegateway.service_endpoint_id | Body | UUID | サービスエンドポイント（またはユーザー定義エンドポイント）ID |
| servicegateway.service_provider | Body | String | 接続タイプ（接続されたエンドポイントの値）。`csp`=サービスエンドポイント / `user`=ユーザー定義エンドポイント |
| servicegateway.api_endpoints | Body | Array | APIエンドポイント情報オブジェクトリスト |
| servicegateway.api_endpoints.domain_name | Body | String | APIエンドポイントドメイン |
| servicegateway.description | Body | String | サービスゲートウェイの説明 |
<details><summary>例</summary>

```json
{
  "servicegateway": {
    "status": "AVAILABLE",
    "include_gateway_identity": false,
    "description": "test1",
    "network_id": "55529e1d-c6ee-4be8-baa9-2b6546667e6d",
    "tenant_id": "302406c4a1d44b2cb2bc07a652c0b202",
    "fixed_ip": "192.168.0.82",
    "subnet_id": "72d9d6e0-3ee2-4287-bcf9-be45a8422ff1",
    "api_endpoints": [
      {
        "domain_name": "test.test.com"
      }
    ],
    "service_endpoint_id": "7ba5b6e7-d871-43d3-90d2-7e2beecaaae5",
    "service_provider": "csp",
    "create_time": "2023-08-31 02:11:09",
    "project_id": "302406c4a1d44b2cb2bc07a652c0b202",
    "port_id": "182a31be-9e29-400d-983b-f701cf9b4bbc",
    "id": "d383a4a3-dae7-4609-b2db-ecdf5859fac5",
    "name": "sgw_test1"
  }
}
```

</details>

---
<a id="delete-a-service-gateway"></a>
### サービスゲートウェイを削除する { #delete-a-service-gateway }

```
DELETE /v2.0/gateways/servicegateways/{serviceGatewayId}
X-Auth-Token: {tokenId}
```

<a id="delete-a-service-gateway-request"></a>
#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| serviceGatewayId | URL | UUID | O | サービスゲートウェイID |


<a id="delete-a-service-gateway-response"></a>
#### レスポンス
このAPIはレスポンス本文を返しません。










<a id="service-endpoint"></a>
## サービスエンドポイント { #service-endpoint }

<a id="get-a-list-of-service-endpoints"></a>
### サービスエンドポイントリスト表示 { #get-a-list-of-service-endpoints }

```
GET /v2.0/gateways/serviceendpoints/
X-Auth-Token: {tokenId}
```

<a id="get-a-list-of-service-endpoints-request"></a>
#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するサービスエンドポイント ID |
| display_name | Query | String | - | 照会するサービスエンドポイント名 |
| service_name | Query | String | - | 照会するサービス名（ユーザー定義エンドポイント接続時に使用、形式 `{region}.sep-{12 hex}`） |
> サービスゲートウェイをカスタムエンドポイントに接続する際は、パブリッシャーから受け取った `service_name` で照会してサービスエンドポイント ID を取得します。セキュリティのため、`service_name` の値はレスポンスに含まれず、許可プロジェクトに含まれていない場合は空のリストが返されます。

<a id="get-a-list-of-service-endpoints-response"></a>
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| serviceendpoints | Body | Array | サービスエンドポイント情報オブジェクトリスト |
| serviceendpoints.id | Body | UUID | サービスエンドポイントID |
| serviceendpoints.display_name | Body | String | コンソールに出力されるサービスエンドポイントの名前 |
| serviceendpoints.support_gateway_identity | Body | Boolean | NAT IPアドレス固定の使用有無 |
| serviceendpoints.description | Body | String | サービスエンドポイントの説明 |

<details><summary>例</summary>

```json
{
  "serviceendpoints": [
    {
      "display_name": "Object Storage",
      "support_gateway_identity": true,
      "description": "",
      "name": "OBS",
      "id": "7ba5b6e7-d871-43d3-90d2-7e2beecaaae5"
    }
  ]
}
```
</details>

---
<a id="get-a-service-endpoint"></a>
### サービスエンドポイント表示 { #get-a-service-endpoint }

```
GET /v2.0/gateways/serviceendpoints/{seerviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="get-a-service-endpoint-request"></a>
#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| serviceEndpointId | URL | UUID | O | サービスエンドポイントID |

<a id="get-a-service-endpoint-response"></a>
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| serviceendpoint | Body | Object | サービスエンドポイント情報オブジェクト |
| serviceendpoint.id | Body | UUID | サービスエンドポイントID |
| serviceendpoint.display_name | Body | String | コンソールに出力されるサービスエンドポイントの名前 |
| serviceendpoint.support_gateway_identity | Body | Boolean | NAT IPアドレス固定の使用有無 |
| serviceendpoint.description | Body | String | サービスエンドポイントの説明 |

<details><summary>例</summary>

```json
{
  "serviceendpoint": {
      "display_name": "Object Storage",
      "support_gateway_identity": true,
      "description": "",
      "name": "OBS",
      "id": "7ba5b6e7-d871-43d3-90d2-7e2beecaaae5"
  }
}
```
</details>

---

<a id="custom-endpoints"></a>
## カスタムエンドポイント { #custom-endpoints }

ユーザーが自分のリソース（ロードバランサー）をエンドポイントとして公開し、他のプロジェクトと共有する機能です。公開者（オーナー）が作成・管理し、作成時に共有用のサービス名（`service_name`）が発行されます。

<a id="view-custom-endpoint-list"></a>
### カスタムエンドポイントリスト表示 { #view-custom-endpoint-list }

```
GET /v2.0/gateways/myserviceendpoints
X-Auth-Token: {tokenId}
```

<a id="view-custom-endpoint-list-request"></a>
#### リクエスト
この API はリクエスト本文を必要としません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン ID |
| id | Query | UUID | - | 照会するユーザー定義エンドポイント ID |
| endpoint_type | Query | String | - | 照会するエンドポイントのタイプ(例: `lb.type1`) |
| port_id | Query | UUID | - | 照会対象リソース（ロードバランサー）のポート ID |

<a id="view-custom-endpoint-list-response"></a>
#### 応答

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| myserviceendpoints | Body | Array | ユーザー定義エンドポイント情報オブジェクトのリスト |
| myserviceendpoints.id | Body | UUID | ユーザー定義エンドポイント ID |
| myserviceendpoints.name | Body | String | 名前 |
| myserviceendpoints.display_name | Body | String | 表示名（サービスゲートウェイに公開される名前） |
| myserviceendpoints.endpoint_type | Body | String | エンドポイントタイプ（リソースタイプ、例: `lb.type1`） |
| myserviceendpoints.port_id | Body | UUID | 対象リソース（ロードバランサー）ポート ID。`GET /v2.0/lbaas/loadbalancers?vip_port_id={port_id}` で対象ロードバランサーを検索できます。 |
| myserviceendpoints.service_name | Body | String | 共有用サービス名（形式 `{region}.sep-{12 hex}`） |
| myserviceendpoints.max_count | Body | Integer | 最大作成数（このエンドポイントで作成可能なサービスゲートウェイの最大数）。`0`=作成ブロック、未設定=無制限 |
| myserviceendpoints.current_count | Body | Integer | 使用状況(このエンドポイントで現在作成されているサービスゲートウェイの数) |
| myserviceendpoints.service_provider | Body | String | 接続タイプ（ユーザー定義エンドポイントは `user`） |
| myserviceendpoints.description | Body | String | 説明 |
| myserviceendpoints.project_id | Body | String | テナント ID |
<details><summary>例</summary>

```json
{
  "myserviceendpoints": [
    {
      "id": "ef2b41aa-81f4-40de-9dc9-677ca58428f1",
      "name": "my-lb-service",
      "display_name": "My LB Service",
      "endpoint_type": "lb.type1",
      "port_id": "a6e6ff53-8c70-48db-95ec-8b4895f002c2",
      "service_name": "kr1.sep-0a1b2c3d4e5f",
      "max_count": 10,
      "current_count": 3,
      "service_provider": "user",
      "description": "",
      "project_id": "302406c4a1d44b2cb2bc07a652c0b202"
    }
  ]
}
```

</details>

---
<a id="get-a-custom-endpoint"></a>
### カスタムエンドポイント表示 { #get-a-custom-endpoint }

```
GET /v2.0/gateways/myserviceendpoints/{serviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="get-a-custom-endpoint-request"></a>
#### リクエスト
この API はリクエスト本文を必要としません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン ID |
| serviceEndpointId | URL | UUID | O | ユーザー定義エンドポイント ID |

<a id="get-a-custom-endpoint-response"></a>
#### 応答

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| myserviceendpoint | Body | Object | カスタムエンドポイント情報オブジェクト |
| myserviceendpoint.id | Body | UUID | ユーザー定義エンドポイント ID |
| myserviceendpoint.name | Body | String | 名前 |
| myserviceendpoint.display_name | Body | String | 表示名 |
| myserviceendpoint.endpoint_type | Body | String | エンドポイントタイプ（リソースタイプ） |
| myserviceendpoint.port_id | Body | UUID | 対象リソース（ロードバランサー）のポート ID。`GET /v2.0/lbaas/loadbalancers?vip_port_id={port_id}` で対象のロードバランサーを検索できます。 |
| myserviceendpoint.service_name | Body | String | 共有用サービス名 |
| myserviceendpoint.max_count | Body | Integer | 最大作成数 |
| myserviceendpoint.current_count | Body | Integer | 使用状況（現在作成されているサービスゲートウェイ数） |
| myserviceendpoint.service_provider | Body | String | 接続タイプ（`user`） |
| myserviceendpoint.description | Body | String | 説明 |
| myserviceendpoint.project_id | Body | String | テナント ID |
<details><summary>例</summary>

```json
{
  "myserviceendpoint": {
    "id": "ef2b41aa-81f4-40de-9dc9-677ca58428f1",
    "name": "my-lb-service",
    "display_name": "My LB Service",
    "endpoint_type": "lb.type1",
    "port_id": "a6e6ff53-8c70-48db-95ec-8b4895f002c2",
    "service_name": "kr1.sep-0a1b2c3d4e5f",
    "max_count": 10,
    "current_count": 3,
    "service_provider": "user",
    "description": "",
    "project_id": "302406c4a1d44b2cb2bc07a652c0b202"
  }
}
```

</details>

---
<a id="create-a-custom-endpoint"></a>
### カスタムエンドポイントの作成 { #create-a-custom-endpoint }

```
POST /v2.0/gateways/myserviceendpoints
X-Auth-Token: {tokenId}
```

<a id="create-a-custom-endpoint-request"></a>
#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン ID |
| myserviceendpoint | Body | Object | O | ユーザー定義エンドポイント情報オブジェクト |
| myserviceendpoint.name | Body | String | O | 名前（255文字以内、英数字/-/_） |
| myserviceendpoint.display_name | Body | String | - | 表示名(省略時は `name` と同じ値が適用されます) |
| myserviceendpoint.port_id | Body | UUID | O | 対象リソース（ロードバランサー）のポート ID。ロードバランサー表示（`GET /v2.0/lbaas/loadbalancers/{loadbalancerId}`）レスポンスの `vip_port_id` を使用します。 |
| myserviceendpoint.max_count | Body | Integer | - | 最大作成数（0〜1,000）。0: 作成ブロック、null または未入力: 無制限 |
| myserviceendpoint.description | Body | String | - | 説明 |

> 対象リソースとしてロードバランサーを指定すると、`endpoint_type` が `lb.type1` に、`service_provider` が `user` に自動設定されます。作成が完了すると、共有用の `service_name` が自動的に発行されます。プロジェクトあたりデフォルトで最大 5 つまで作成できます。

<details><summary>例</summary>

```json
{
  "myserviceendpoint": {
    "name": "my-lb-service",
    "display_name": "My LB Service",
    "port_id": "a6e6ff53-8c70-48db-95ec-8b4895f002c2",
    "max_count": 10,
    "description": ""
  }
}
```

</details>

<a id="create-a-custom-endpoint-response"></a>
#### レスポンス
レスポンス本文は「[カスタムエンドポイント表示](#get-a-custom-endpoint)」と同じですが、自動発行された `service_name` が含まれます。

---
<a id="modify-a-custom-endpoint"></a>
### カスタムエンドポイントの変更 { #modify-a-custom-endpoint }

```
PUT /v2.0/gateways/myserviceendpoints/{serviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="modify-a-custom-endpoint-request"></a>
#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン ID |
| serviceEndpointId | URL | UUID | O | ユーザー定義エンドポイント ID |
| myserviceendpoint | Body | Object | O | ユーザー定義エンドポイント情報オブジェクト |
| myserviceendpoint.name | Body | String | - | 名前 |
| myserviceendpoint.display_name | Body | String | - | 表示名 |
| myserviceendpoint.max_count | Body | Integer | - | 最大作成数（0〜1000）。0: 作成をブロック、null: 無制限に変更、フィールド未指定の場合は既存の値を維持 |
| myserviceendpoint.description | Body | String | - | 説明 |

> リソースタイプ（`endpoint_type`）とターゲットリソース（`port_id`）は変更することはできません。最大作成数を減らしても既存のサービスゲートウェイは維持され、現在の数が最大作成数を超えている間は追加作成できません。

<details><summary>例</summary>

```json
{
  "myserviceendpoint": {
    "name": "my-lb-renamed",
    "display_name": "My LB (renamed)",
    "max_count": 20,
    "description": "renamed"
  }
}
```

</details>

<a id="modify-a-custom-endpoint-response"></a>
#### レスポンス
レスポンスボディは[ユーザー定義エンドポイント表示](#get-a-custom-endpoint)と同じです。

---
<a id="delete-custom-endpoint"></a>
### カスタムエンドポイントの削除 { #delete-custom-endpoint }

```
DELETE /v2.0/gateways/myserviceendpoints/{serviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="delete-custom-endpoint-request"></a>
#### リクエスト
この API はリクエスト本文を必要としません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン ID |
| serviceEndpointId | URL | UUID | O | ユーザー定義エンドポイント ID |

> このエンドポイントを使用中のサービスゲートウェイが存在する場合は削除できません。削除すると、登録された許可プロジェクトも合わせて削除されます。

<a id="delete-custom-endpoint-response"></a>
#### レスポンス
この API はレスポンス本文を返しません。

---
<a id="reissue-a-service-name"></a>
### サービス名の再発行 { #reissue-a-service-name }

```
PUT /v2.0/gateways/serviceendpoints/{serviceEndpointId}/generate_service_name
X-Auth-Token: {tokenId}
```

<a id="reissue-a-service-name-request"></a>
#### リクエスト
この API はリクエスト本文を必要としません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン ID |
| serviceEndpointId | URL | UUID | O | ユーザー定義エンドポイント ID |

> エンドポイントを作成したプロジェクトのメンバー（オーナー）のみが実行できます。再発行すると、既存の `service_name` は即時廃棄され、以降は照会されなくなります。既存の `service_name` で作成したサービスゲートウェイは正常に動作しますが、新規作成時は再発行された `service_name` を使用する必要があります。

<a id="reissue-a-service-name-response"></a>
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| service_name | Body | String | 再発行された共有用サービス名 |

<details><summary>例</summary>

```json
{
  "service_name": "kr1.sep-9f8e7d6c5b4a"
}
```

</details>

---
<a id="allowed-projects"></a>
## 許可プロジェクト { #allowed-projects }

カスタムエンドポイントへの接続（サービスゲートウェイの作成）を許可する対象（テナント）を管理するリスト（ホワイトリスト）です。純粋な許可リスト（権限）であり、作成数の制限は扱いません（数の制限はエンドポイントの `max_count` で管理）。

<a id="view-allow-project-list"></a>
### 許可プロジェクトリスト表示 { #view-allow-project-list }

```
GET /v2.0/gateways/serviceendpointallowprojects
X-Auth-Token: {tokenId}
```

<a id="view-allow-project-list-request"></a>
#### リクエスト
この API はリクエスト本文を必要としません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン ID |
| service_endpoint_id | Query | UUID | - | 照会するユーザー定義エンドポイント ID |
| target_tenant_id | Query | String | - | 照会する許可対象テナント ID |

<a id="view-allow-project-list-response"></a>
#### 応答

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| serviceendpointallowprojects | Body | Array | 許可プロジェクト情報オブジェクトリスト |
| serviceendpointallowprojects.id | Body | UUID | 許可されたプロジェクト ID |
| serviceendpointallowprojects.service_endpoint_id | Body | UUID | ユーザー定義エンドポイント ID |
| serviceendpointallowprojects.target_tenant_id | Body | String | 許可対象。`*`=全プロジェクト / テナント ID=特定プロジェクト |
| serviceendpointallowprojects.name | Body | String | 名前（参考用） |
| serviceendpointallowprojects.description | Body | String | 説明 |

<details><summary>例</summary>

```json
{
  "serviceendpointallowprojects": [
    {
      "id": "d9e0f111-2222-3333-4444-555566667777",
      "service_endpoint_id": "ef2b41aa-81f4-40de-9dc9-677ca58428f1",
      "target_tenant_id": "302406c4a1d44b2cb2bc07a652c0b202",
      "name": "allow-b",
      "description": "allow b-tenant"
    }
  ]
}
```

</details>

---
<a id="view-allowed-projects"></a>
### 許可プロジェクト表示 { #view-allowed-projects }

```
GET /v2.0/gateways/serviceendpointallowprojects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="view-allowed-projects-request"></a>
#### リクエスト
この API はリクエスト本文を必要としません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークン ID |
| allowProjectId | URL | UUID | O | 許可プロジェクト ID |

<a id="view-allowed-projects-response"></a>
#### レスポンス
レスポンス本文は[許可プロジェクトリスト表示](#view-allow-project-list)の単一オブジェクト（`serviceendpointallowproject`）と同じです。

---
<a id="create-an-allowed-project"></a>
### 許可プロジェクトの作成 { #create-an-allowed-project }

```
POST /v2.0/gateways/serviceendpointallowprojects
X-Auth-Token: {tokenId}
```

<a id="create-an-allowed-project-request"></a>
#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン ID |
| serviceendpointallowproject | Body | Object | O | 許可プロジェクト情報オブジェクト |
| serviceendpointallowproject.service_endpoint_id | Body | UUID | O | ユーザー定義エンドポイント ID |
| serviceendpointallowproject.target_tenant_id | Body | String | O | 許可対象。`*`=全プロジェクト / テナント ID（32桁の16進数）=特定プロジェクト |
| serviceendpointallowproject.name | Body | String | - | 名前(参考用) |
| serviceendpointallowproject.description | Body | String | - | 説明 |

> 全許可（`*`）と特定プロジェクトを同時に登録した場合、より狭い範囲（特定プロジェクト）が適用されます。これを利用して、無停止で許可範囲を切り替えることができます。エンドポイントの所有者のテナント ID は登録できません（所有者は常に許可）。同一の（エンドポイント、テナント）の組み合わせがすでに存在する場合は 409 が返されます。

<details><summary>例</summary>

```json
{
  "serviceendpointallowproject": {
    "service_endpoint_id": "ef2b41aa-81f4-40de-9dc9-677ca58428f1",
    "target_tenant_id": "302406c4a1d44b2cb2bc07a652c0b202",
    "name": "allow-b",
    "description": "allow b-tenant"
  }
}
```

</details>

<a id="create-an-allowed-project-response"></a>
#### レスポンス
レスポンス本文は、[許可プロジェクトリスト表示](#view-allow-project-list)の単一オブジェクト（`serviceendpointallowproject`）と同じです。

---
<a id="modify-allowed-projects"></a>
### 許可プロジェクトの変更 { #modify-allowed-projects }

```
PUT /v2.0/gateways/serviceendpointallowprojects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="modify-allowed-projects-request"></a>
#### リクエスト

| tokenId | Header | String | O | 認証トークン ID |
| allowProjectId | URL | UUID | O | 許可プロジェクト ID |
| allowProjectId | URL | UUID | O | 許可プロジェクト ID |
| serviceendpointallowproject | Body | Object | O | 許可プロジェクト情報オブジェクト |
| serviceendpointallowproject.name | Body | String | - | 名前(参考用) |
| serviceendpointallowproject.description | Body | String | - | 説明 |

> 許可対象 (`target_tenant_id`) とエンドポイント (`service_endpoint_id`) は変更できません。`name`・`description` のみ変更できます。

<details><summary>例</summary>

```json
{
  "serviceendpointallowproject": {
    "name": "allow-b-renamed",
    "description": "Bプロジェクト連携"
  }
}
```

</details>

<a id="modify-allowed-projects-response"></a>
#### レスポンス
レスポンス本文は、[許可プロジェクトリスト表示](#view-allow-project-list)の単一オブジェクト（`serviceendpointallowproject`）と同じです。

---
<a id="delete-an-allowed-project"></a>
### 許可プロジェクトの削除 { #delete-an-allowed-project }

```
DELETE /v2.0/gateways/serviceendpointallowprojects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="delete-an-allowed-project-request"></a>
#### リクエスト
この API はリクエスト本文を必要としません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン |
| allowProjectId | URL | UUID | O | 許可プロジェクト ID |

<a id="delete-an-allowed-project-response"></a>
#### レスポンス
この API はレスポンス本文を返しません。

---
<a id="usage-status"></a>
## 使用状況 { #usage-status }

ユーザー定義エンドポイントを使用中（接続済み）のコンシューマー側サービスゲートウェイのリストを照会します。

<a id="view-usage-status-list"></a>
### 使用状況リスト表示 { #view-usage-status-list }

```
GET /v2.0/gateways/serviceendpointusages
X-Auth-Token: {tokenId}
```

<a id="view-usage-status-list-request"></a>
#### リクエスト
このAPIはリクエスト本文を必要としません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | 認証トークン |
| id | Query | UUID | - | 照会するユーザー定義エンドポイント ID（複数指定可能、省略時は所有するすべてのエンドポイントが対象） |
| network_id | Query | UUID | - | 照会するサービスゲートウェイの VPC ID（複数指定可能） |
| subnet_id | Query | UUID | - | 照会するサービスゲートウェイのサブネット ID（複数指定可能） |
| limit | Query | Integer | - | 一度に照会する最大件数（省略時は全件返します） |
| marker | Query | UUID | - | 直前ページの最後の項目のサービスゲートウェイ ID（次のページ照会時に使用） |
| page_reverse | Query | Boolean | - | `true`に指定すると、前のページ方向で照会します |
| sort_key | Query | String | - | ソートの基準フィールド（複数指定可能） |
| sort_dir | Query | String | - | ソート方向（`asc` または `desc`）。`sort_key` と必ずペアで、同じ数だけ指定 |

> 結果はデフォルトでサービスゲートウェイ ID (`id`) の昇順で並べ替えられます。作成日時順で取得するには、`sort_key=create_time&sort_dir=desc` のように指定する必要があります。`sort_key` には、レスポンスフィールド (`id`、`name`、`fixed_ip`、`status`、`tenant_id`、`network_id`、`subnet_id`、`service_endpoint_id`、`create_time`) を使用できます。
> `limit` を指定すると、レスポンスに次/前のページリンク (`serviceendpointusages_links`) が含まれます。次のページを取得するには、リンクの URL をそのまま呼び出すか、現在のページの最後の項目の `id` を `marker` として指定します。ページを順次取得する間は、同じフィルター/並べ替え条件を維持する必要があります。

<a id="view-usage-status-list-response"></a>
#### 応答

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| serviceendpointusages | Body | Array | 使用状況情報オブジェクトのリスト |
| serviceendpointusages.id | Body | UUID | サービスゲートウェイ ID |
| serviceendpointusages.name | Body | String | サービスゲートウェイ名 |
| serviceendpointusages.fixed_ip | Body | String | サービスゲートウェイの IP アドレス |
| serviceendpointusages.status | Body | String | サービスゲートウェイのステータス |
| serviceendpointusages.tenant_id | Body | String | サービスゲートウェイを作成したコンシューマープロジェクトのテナント ID |
| serviceendpointusages.network_id | Body | UUID | サービスゲートウェイ VPC ID |
| serviceendpointusages.subnet_id | Body | UUID | サービスゲートウェイのサブネット ID |
| serviceendpointusages.service_endpoint_id | Body | UUID | 接続されたユーザー定義エンドポイント ID |
| serviceendpointusages.create_time | Body | String | サービスゲートウェイ作成日時 |
| serviceendpointusages_links | Body | Array | ページネーションリンクリスト(`limit` 指定時のみ含まれる) |
| serviceendpointusages_links.rel | Body | String | リンクの種類。`next`=次のページ / `previous`=前のページ |
| serviceendpointusages_links.href | Body | String | 該当ページを照会できる URL |
<details><summary>例</summary>

```json
{
  "serviceendpointusages": [
    {
      "id": "d383a4a3-dae7-4609-b2db-ecdf5859fac5",
      "name": "sgw_partner",
      "fixed_ip": "192.168.0.51",
      "status": "AVAILABLE",
      "tenant_id": "302406c4a1d44b2cb2bc07a652c0b202",
      "network_id": "55529e1d-c6ee-4be8-baa9-2b6546667e6d",
      "subnet_id": "72d9d6e0-3ee2-4287-bcf9-be45a8422ff1",
      "service_endpoint_id": "ef2b41aa-81f4-40de-9dc9-677ca58428f1",
      "create_time": "2023-08-31 02:11:09"
    }
  ],
  "serviceendpointusages_links": [
    {
      "rel": "next",
      "href": "https://kr1-api-network-infrastructure.nhncloudservice.com/v2.0/gateways/serviceendpointusages?limit=20&marker=d383a4a3-dae7-4609-b2db-ecdf5859fac5"
    },
    {
      "rel": "previous",
      "href": "https://kr1-api-network-infrastructure.nhncloudservice.com/v2.0/gateways/serviceendpointusages?limit=20&marker=d383a4a3-dae7-4609-b2db-ecdf5859fac5&page_reverse=True"
    }
  ]
}
```

</details>
