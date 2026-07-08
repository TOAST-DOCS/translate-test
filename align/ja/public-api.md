## Network > Traffic Mirroring > API v2ガイド

NHN Cloud Networkサービスは、API呼び出し時の認証/認可のためにIaaSトークンを使用します。IaaSトークンは、NHN CloudのOpenStackベースのインフラサービス(IaaS)で使用する認証トークンです。IaaSトークンの発行及び使用に関する詳細は、[IaaSトークン](/nhncloud/ja/public-api/iaas-token)を参照してください。

ミラーリングAPIは`network`タイプのエンドポイントを利用します。正確なエンドポイントは、トークン発行時のレスポンスにある`serviceCatalog`を参照してください。

| タイプ | リージョン | エンドポイント |
| --- | --- | ----- |
| network | 韓国(パンギョ)リージョン<br>韓国(ピョンチョン)リージョン<br>韓国(光州)リージョン | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

APIのレスポンスには、ガイドに明記されていないフィールドが含まれる場合があります。これらのフィールドはNHN Cloudの内部用として使用され、事前の通知なしに変更されることがあるため、使用しないでください。

## ミラーリングセッション(session)

セッションは、ソースポートのトラフィックをターゲットポートにミラーリングする単位を意味します。必要な場合、1つ以上のフィルタグループを関連付け、特定のトラフィックのみをミラーリングできます。

### セッション一覧の表示

```
GET /v2.0/mirroring/sessions
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエストボディを要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するセッションID |
| tenant\_id | Query | String | - | テナントID |
| name | Query | String | - | セッション名 |
| direction | Query | Enum | - | `in`、`out`、`both`のいずれか |
| sort\_dir | Query | Enum | - | ソート方向。`asc`、`desc`のいずれか |
| sort\_key | Query | String | - | ソート基準フィールド |
| fields | Query | String | - | レスポンスに含めるフィールド。例: `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| sessions | Body | Array | セッションオブジェクト一覧 |
| sessions.id | Body | UUID | セッションID |
| sessions.name | Body | String | セッション名 |
| sessions.description | Body | String | 説明 |
| sessions.target\_port\_id | Body | UUID | ターゲットポートID |
| sessions.source\_port\_id | Body | UUID | ソースポートID |
| sessions.filter\_groups | Body | Array[UUID] | 関連付けられたフィルタグループID一覧 |
| sessions.direction | Body | Enum | `in`、`out`、`both`のいずれか |
| sessions.tenant\_id | Body | String | テナントID |
| sessions.project\_id | Body | String | プロジェクトID。テナントIDと同じ |
| sessions.target\_network\_id | Body | UUID | ターゲットポートのネットワークID |
| sessions.source\_network\_id | Body | UUID | ソースポートのネットワークID |
| sessions.vni | Body | Number | ミラーリングトンネルVNI |
| sessions.status | Body | Enum | セッションステータス: `ACTIVE`、`BUILD`、`ERROR` |
| sessions.created\_at | Body | String | 作成時間(UTC) |
| sessions.updated\_at | Body | String | 修正時間(UTC) |

例

```json
{
  "sessions": [
    {
      "id": "7b0b5e6f-9a75-4b5a-9d69-0fb6a6d8e111",
      "name": "mirror-sess-1",
      "description": "",
      "target_port_id": "c0a8012b-7f6d-4c16-951d-cca31af20c01",
      "source_port_id": "5d5b1ce7-9a68-4f3d-9c0d-2e6b5b9a1c02",
      "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
      "direction": "both",
      "tenant_id": "76841f7d054a40b88b2a99828280998c",
      "project_id": "76841f7d054a40b88b2a99828280998c",
      "target_network_id": "a2a9b0f0-1d75-4b3b-b3a1-5a1d2f3e4b55",
      "source_network_id": "b3b0f0a2-2e86-4c4c-a1b3-6c2d3e4f5a66",
      "vni": 5001001,
      "status": "ACTIVE",
      "created_at": "2025-08-29 05:25:30",
      "updated_at": "2025-08-29 05:25:30"
    }
  ]
}
```

***

### セッションの表示

```
GET /v2.0/mirroring/sessions/{SessionId}
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエストボディを要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| SessionId | URL | UUID | O | セッションID |
| tokenId | Header | String | O | トークンID |
| fields | Query | String | - | レスポンスに含めるフィールド。例: `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| session | Body | Object | セッションオブジェクト |
| session.id | Body | UUID | セッションID |
| session.name | Body | String | セッション名 |
| session.description | Body | String | 説明 |
| session.target\_port\_id | Body | UUID | ターゲットポートID |
| session.source\_port\_id | Body | UUID | ソースポートID |
| session.filter\_groups | Body | Array[UUID] | 関連付けられたフィルタグループID一覧 |
| session.direction | Body | Enum | `in`、`out`、`both`のいずれか |
| session.tenant\_id | Body | String | テナントID |
| session.project\_id | Body | String | プロジェクトID |
| session.target\_network\_id | Body | UUID | ターゲットポートのネットワークID |
| session.source\_network\_id | Body | UUID | ソースポートのネットワークID |
| session.vni | Body | Number | トンネルVNI |
| session.status | Body | Enum | `ACTIVE`, `BUILD`, `ERROR` |
| session.created\_at | Body | String | 作成時間(UTC) |
| session.updated\_at | Body | String | 修正時間(UTC) |

例

```json
{
  "session": {
    "id": "7b0b5e6f-9a75-4b5a-9d69-0fb6a6d8e111",
    "name": "mirror-sess-1",
    "description": "",
    "target_port_id": "c0a8012b-7f6d-4c16-951d-cca31af20c01",
    "source_port_id": "5d5b1ce7-9a68-4f3d-9c0d-2e6b5b9a1c02",
    "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
    "direction": "both",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c",
    "target_network_id": "a2a9b0f0-1d75-4b3b-b3a1-5a1d2f3e4b55",
    "source_network_id": "b3b0f0a2-2e86-4c4c-a1b3-6c2d3e4f5a66",
    "vni": 5001001,
    "status": "ACTIVE",
    "created_at": "2025-08-29 05:25:30",
    "updated_at": "2025-08-29 05:25:30"
  }
}
```

***

### セッションの作成

```
POST /v2.0/mirroring/sessions
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | トークンID |
| session | Body | Object | O | セッション作成リクエストオブジェクト |
| session.name | Body | String | - | セッション名(最大32文字、英字/数字/`-`/`_`) |
| session.description | Body | String | - | 説明(最大255文字) |
| session.target\_port\_id | Body | UUID | O | ターゲットポートID |
| session.source\_port\_id | Body | UUID | O | ソースポートID |
| session.filter\_groups | Body | Array[UUID] | - | 関連付けるフィルタグループID一覧。ない場合は全トラフィックをミラーリング |
| session.direction | Body | Enum | O | `in`、`out`、`both`のいずれか |
| session.tenant\_id | Body | String | O | テナントID |
| session.project\_id | Body | String | O | プロジェクトID |

例

```json
{
  "session": {
    "name": "mirror-sess-1",
    "description": "",
    "target_port_id": "c0a8012b-7f6d-4c16-951d-cca31af20c01",
    "source_port_id": "5d5b1ce7-9a68-4f3d-9c0d-2e6b5b9a1c02",
    "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
    "direction": "both",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c"
  }
}
```

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| session | Body | Object | セッションオブジェクト |
| session.id | Body | UUID | セッションID |
| session.status | Body | Enum | 初期は主に`BUILD` |
| その他 | Body | - | セッションの表示と同じ |

例

```json
{
  "session": {
    "id": "7b0b5e6f-9a75-4b5a-9d69-0fb6a6d8e111",
    "name": "mirror-sess-1",
    "description": "",
    "target_port_id": "c0a8012b-7f6d-4c16-951d-cca31af20c01",
    "source_port_id": "5d5b1ce7-9a68-4f3d-9c0d-2e6b5b9a1c02",
    "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
    "direction": "both",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c",
    "target_network_id": "a2a9b0f0-1d75-4b3b-b3a1-5a1d2f3e4b55",
    "source_network_id": "b3b0f0a2-2e86-4c4c-a1b3-6c2d3e4f5a66",
    "vni": 5001001,
    "status": "BUILD",
    "created_at": "2025-08-29 05:25:30",
    "updated_at": "2025-08-29 05:25:30"
  }
}
```

***

### セッションの修正

```
PUT /v2.0/mirroring/sessions/{SessionId}
X-Auth-Token: {tokenId}
```

説明と名前、方向、フィルタグループ一覧のみ修正できます。ポートの変更はサポートしていません。

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| SessionId | URL | UUID | O | セッションID |
| tokenId | Header | String | O | トークンID |
| session | Body | Object | O | 修正するフィールドのみ含む |
| session.name | Body | String | - | セッション名 |
| session.description | Body | String | - | 説明 |
| session.filter\_groups | Body | Array[UUID] | - | フィルタグループID一覧 |
| session.direction | Body | Enum | - | `in`, `out`, `both` |

例

```json
{
  "session": {
    "name": "mirror-sess-1b",
    "description": "update",
    "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
    "direction": "in"
  }
}
```

#### レスポンス

セッションの表示の応答と同じです。

***

### セッションの削除

```
DELETE /v2.0/mirroring/sessions/{SessionId}
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエストボディを要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| SessionId | URL | UUID | O | セッションID |
| tokenId | Header | String | O | トークンID |

#### レスポンス

このAPIはレスポンスボディを返しません。

***

## ミラーリングフィルタグループ(filtergroup)

フィルタグループは、1つ以上のフィルタをまとめるコンテナです。セッションに関連付け、特定のトラフィックのみをミラーリングできます。

### フィルタグループ一覧の表示

```
GET /v2.0/mirroring/filtergroups
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエストボディを要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | フィルタグループID |
| tenant\_id | Query | String | - | テナントID |
| name | Query | String | - | 名前 |
| sort\_dir | Query | Enum | - | `asc`, `desc` |
| sort\_key | Query | String | - | ソートキー |
| fields | Query | String | - | 含めるフィールド |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| filtergroups | Body | Array | フィルタグループ一覧 |
| filtergroups.id | Body | UUID | ID |
| filtergroups.name | Body | String | 名前 |
| filtergroups.description | Body | String | 説明 |
| filtergroups.tenant\_id | Body | String | テナントID |
| filtergroups.project\_id | Body | String | プロジェクトID |
| filtergroups.filters | Body | Array | グループ内のフィルタオブジェクト/ID一覧 |
| filtergroups.created\_at | Body | String | 作成時間(UTC) |
| filtergroups.updated\_at | Body | String | 修正時間(UTC) |

例

```json
{
  "filtergroups": [
    {
      "id": "2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10",
      "name": "fg-1",
      "description": "",
      "tenant_id": "76841f7d054a40b88b2a99828280998c",
      "project_id": "76841f7d054a40b88b2a99828280998c",
      "filters": [],
      "created_at": "2025-08-29 05:20:00",
      "updated_at": "2025-08-29 05:20:00"
    }
  ]
}
```

***

### フィルタグループの表示

```
GET /v2.0/mirroring/filtergroups/{FilterGroupId}
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエストボディを要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | トークンID |
| id | URL | UUID | O | フィルタグループID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| filtergroup | Body | Object | フィルタグループ一覧 |
| filtergroup.id | Body | UUID | ID |
| filtergroup.name | Body | String | 名前 |
| filtergroup.description | Body | String | 説明 |
| filtergroup.tenant\_id | Body | String | テナントID |
| filtergroup.project\_id | Body | String | プロジェクトID |
| filtergroup.filters | Body | Array | グループ内のフィルタオブジェクト/ID一覧 |
| filtergroup.created\_at | Body | String | 作成時間(UTC) |
| filtergroup.updated\_at | Body | String | 修正時間(UTC) |

***

### フィルタグループの作成

```
POST /v2.0/mirroring/filtergroups
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | トークンID |
| filtergroup | Body | Object | O | フィルタグループ作成リクエストオブジェクト |
| filtergroup.name | Body | String | - | 名前(最大32文字、英字/数字/`-`/`_`) |
| filtergroup.description | Body | String | - | 説明(最大255文字) |
| filtergroup.tenant\_id | Body | String | O | テナントID |
| filtergroup.project\_id | Body | String | O | プロジェクトID |

例

```json
{
  "filtergroup": {
    "name": "fg-1",
    "description": "",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c"
  }
}
```

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| filtergroup | Body | Object | フィルタグループオブジェクト |
| filtergroup.id | Body | UUID | ID |
| filtergroup.name | Body | String | 名前 |
| filtergroup.description | Body | String | 説明 |
| filtergroup.tenant\_id | Body | String | テナントID |
| filtergroup.project\_id | Body | String | プロジェクトID |
| filtergroup.filters | Body | Array | グループ内のフィルタオブジェクト/ID一覧 |
| filtergroup.created\_at | Body | String | 作成時間(UTC) |
| filtergroup.updated\_at | Body | String | 修正時間(UTC) |

***

### フィルタグループの修正

```
PUT /v2.0/mirroring/filtergroups/{FilterGroupId}
X-Auth-Token: {tokenId}
```

名前と説明のみ修正できます。

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| FilterGroupId | URL | UUID | O | フィルタグループID |
| tokenId | Header | String | O | トークンID |
| filtergroup | Body | Object | O | 修正するフィールドのみ含む |
| filtergroup.name | Body | String | - | 名前 |
| filtergroup.description | Body | String | - | 説明 |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| filtergroup | Body | Object | フィルタグループオブジェクト |
| filtergroup.id | Body | UUID | ID |
| filtergroup.name | Body | String | 名前 |
| filtergroup.description | Body | String | 説明 |
| filtergroup.tenant\_id | Body | String | テナントID |
| filtergroup.project\_id | Body | String | プロジェクトID |
| filtergroup.filters | Body | Array | グループ内のフィルタオブジェクト/ID一覧 |
| filtergroup.created\_at | Body | String | 作成時間(UTC) |
| filtergroup.updated\_at | Body | String | 修正時間(UTC) |

***

### フィルタグループの削除

```
DELETE /v2.0/mirroring/filtergroups/{FilterGroupId}
X-Auth-Token: {tokenId}
```

#### リクエスト/レスポンス

リクエストボディなし。レスポンスボディなし。

***

## ミラーリングフィルタ(filter)

フィルタは、マッチング条件とアクションで構成され、特定のトラフィックを許可(`accept`)または除外(`drop`)する目的で使用されます。フィルタは、必ず特定のフィルタグループに属している必要があります。

### フィルタ一覧の表示

```
GET /v2.0/mirroring/filters
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエストボディを要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | フィルタID |
| filter\_group\_id | Query | UUID | - | 所属フィルタグループID |
| tenant\_id | Query | String | - | テナントID |
| sort\_dir | Query | Enum | - | `asc`, `desc` |
| sort\_key | Query | String | - | ソートキー |
| fields | Query | String | - | 含めるフィールド |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| filters | Body | Array | フィルタ一覧 |
| filters.id | Body | UUID | フィルタID |
| filters.description | Body | String | 説明 |
| filters.filter\_group\_id | Body | UUID | 所属フィルタグループID |
| filters.src\_cidr | Body | CIDR | ソースCIDR。未指定可能 |
| filters.dst\_cidr | Body | CIDR | 宛先CIDR。未指定可能 |
| filters.src\_port\_range\_min | Body | Number | ソースポート範囲(開始) |
| filters.src\_port\_range\_max | Body | Number | ソースポート範囲(終了) |
| filters.dst\_port\_range\_min | Body | Number | 宛先ポート範囲(開始) |
| filters.dst\_port\_range\_max | Body | Number | 宛先ポート範囲(終了) |
| filters.protocol | Body | String | `tcp`、`udp`、`icmp`またはnull |
| filters.action | Body | Enum | `accept`, `drop` |
| filters.priority | Body | Number | 優先順位(デフォルト101) |
| filters.tenant\_id | Body | String | テナントID |
| filters.project\_id | Body | String | プロジェクトID |
| filters.created\_at | Body | String | 作成時間(UTC) |
| filters.updated\_at | Body | String | 修正時間(UTC) |

例

```json
{
  "filters": [
    {
      "id": "f1e2d3c4-b5a6-7890-1234-56789abcde01",
      "description": "allow tcp 80 to 10.0.0.0/24",
      "filter_group_id": "2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10",
      "src_cidr": null,
      "dst_cidr": "10.0.0.0/24",
      "src_port_range_min": null,
      "src_port_range_max": null,
      "dst_port_range_min": 80,
      "dst_port_range_max": 80,
      "protocol": "tcp",
      "action": "accept",
      "priority": 101,
      "tenant_id": "76841f7d054a40b88b2a99828280998c",
      "project_id": "76841f7d054a40b88b2a99828280998c",
      "created_at": "2025-08-29 05:22:00",
      "updated_at": "2025-08-29 05:22:00"
    }
  ]
}
```

***

### フィルタの表示

```
GET /v2.0/mirroring/filters/{FilterId}
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエストボディを要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | トークンID |
| id | Query | URL | O | フィルタID |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| filter | Body | Object | フィルタ一覧 |
| filter.id | Body | UUID | フィルタID |
| filter.description | Body | String | 説明 |
| filter.filter\_group\_id | Body | UUID | 所属フィルタグループID |
| filter.src\_cidr | Body | CIDR | ソースCIDR。未指定可能 |
| filter.dst\_cidr | Body | CIDR | 宛先CIDR。未指定可能 |
| filter.src\_port\_range\_min | Body | Number | ソースポート範囲(開始) |
| filter.src\_port\_range\_max | Body | Number | ソースポート範囲(終了) |
| filter.dst\_port\_range\_min | Body | Number | 宛先ポート範囲(開始) |
| filter.dst\_port\_range\_max | Body | Number | 宛先ポート範囲(終了) |
| filter.protocol | Body | String | `tcp`、`udp`、`icmp`またはnull |
| filter.action | Body | Enum | `accept`, `drop` |
| filter.priority | Body | Number | 優先順位(デフォルト101) |
| filter.tenant\_id | Body | String | テナントID |
| filter.project\_id | Body | String | プロジェクトID |
| filter.created\_at | Body | String | 作成時間(UTC) |
| filter.updated\_at | Body | String | 修正時間(UTC) |

***

### フィルタの作成

```
POST /v2.0/mirroring/filters
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | トークンID |
| filter | Body | Object | O | フィルタ作成リクエストオブジェクト |
| filter.description | Body | String | - | 説明(最大255文字) |
| filter.filter\_group\_id | Body | UUID | O | 所属フィルタグループID |
| filter.src\_cidr | Body | CIDR | - | ソースCIDR |
| filter.dst\_cidr | Body | CIDR | - | 宛先CIDR |
| filter.src\_port\_range\_min | Body | Number | - | ソースポート(開始) |
| filter.src\_port\_range\_max | Body | Number | - | ソースポート(終了) |
| filter.dst\_port\_range\_min | Body | Number | - | 宛先ポート(開始) |
| filter.dst\_port\_range\_max | Body | Number | - | 宛先ポート(終了) |
| filter.protocol | Body | String | - | `tcp`、`udp`、`icmp`またはnull |
| filter.action | Body | Enum | O | `accept`, `drop` |
| filter.priority | Body | Number | - | 優先順位。デフォルト101 |
| filter.tenant\_id | Body | String | O | テナントID |
| filter.project\_id | Body | String | O | プロジェクトID |

例

```json
{
  "filter": {
    "description": "allow tcp 80 to 10.0.0.0/24",
    "filter_group_id": "2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10",
    "dst_cidr": "10.0.0.0/24",
    "dst_port_range_min": 80,
    "dst_port_range_max": 80,
    "protocol": "tcp",
    "action": "accept",
    "priority": 101,
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c"
  }
}
```

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| filter | Body | Object | フィルタ一覧 |
| filter.id | Body | UUID | フィルタID |
| filter.description | Body | String | 説明 |
| filter.filter\_group\_id | Body | UUID | 所属フィルタグループID |
| filter.src\_cidr | Body | CIDR | ソースCIDR。未指定可能 |
| filter.dst\_cidr | Body | CIDR | 宛先CIDR。未指定可能 |
| filter.src\_port\_range\_min | Body | Number | ソースポート範囲(開始) |
| filter.src\_port\_range\_max | Body | Number | ソースポート範囲(終了) |
| filter.dst\_port\_range\_min | Body | Number | 宛先ポート範囲(開始) |
| filter.dst\_port\_range\_max | Body | Number | 宛先ポート範囲(終了) |
| filter.protocol | Body | String | `tcp`、`udp`、`icmp`またはnull |
| filter.action | Body | Enum | `accept`, `drop` |
| filter.priority | Body | Number | 優先順位(デフォルト101) |
| filter.tenant\_id | Body | String | テナントID |
| filter.project\_id | Body | String | プロジェクトID |
| filter.created\_at | Body | String | 作成時間(UTC) |
| filter.updated\_at | Body | String | 修正時間(UTC) |

***

### フィルタの修正

```
PUT /v2.0/mirroring/filters/{FilterId}
X-Auth-Token: {tokenId}
```

説明のみ修正できます。マッチング条件、アクション、優先順位、所属グループは修正できません。

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| FilterId | URL | UUID | O | フィルタID |
| tokenId | Header | String | O | トークンID |
| filter | Body | Object | O | 修正するフィールドのみ含む |
| filter.description | Body | String | - | 説明 |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| filter | Body | Object | フィルタ一覧 |
| filter.id | Body | UUID | フィルタID |
| filter.description | Body | String | 説明 |
| filter.filter\_group\_id | Body | UUID | 所属フィルタグループID |
| filter.src\_cidr | Body | CIDR | ソースCIDR。未指定可能 |
| filter.dst\_cidr | Body | CIDR | 宛先CIDR。未指定可能 |
| filter.src\_port\_range\_min | Body | Number | ソースポート範囲(開始) |
| filter.src\_port\_range\_max | Body | Number | ソースポート範囲(終了) |
| filter.dst\_port\_range\_min | Body | Number | 宛先ポート範囲(開始) |
| filter.dst\_port\_range\_max | Body | Number | 宛先ポート範囲(終了) |
| filter.protocol | Body | String | `tcp`、`udp`、`icmp`またはnull |
| filter.action | Body | Enum | `accept`, `drop` |
| filter.priority | Body | Number | 優先順位(デフォルト101) |
| filter.tenant\_id | Body | String | テナントID |
| filter.project\_id | Body | String | プロジェクトID |
| filter.created\_at | Body | String | 作成時間(UTC) |
| filter.updated\_at | Body | String | 修正時間(UTC) |

***

### フィルタの削除

```
DELETE /v2.0/mirroring/filters/{FilterId}
X-Auth-Token: {tokenId}
```

#### リクエスト/レスポンス

リクエストボディなし。レスポンスボディなし。
