<!-- pre-align:aligned sig=d58a9ac7e400 -->

<a id="database-rds-for-enginepascalcase-api-guide"></a>
## Database > RDS for MariaDB > APIガイド { #database-rds-for-enginepascalcase-api-guide }

<a id="rds-for-enginepascalcase-api-common-information"></a>
## RDS for MariaDB API共通情報 { #rds-for-enginepascalcase-api-common-information }

<a id="api-endpoint"></a>
### APIエンドポイント { #api-endpoint }

| リージョン | エンドポイント |
|------|----------|
| 韓国(パンギョ)リージョン | https://kr1-rds-mariadb.api.gov-nhncloudservice.com |


<a id="common-authorization"></a>
### 認証および権限 { #common-authorization }

RDS for MariaDBは、API呼び出し時の認証/認可にUser Access Keyトークンを使用します。User Access Keyトークンは、User Access Keyに基づいて発行されるBearerタイプの一時的なアクセストークンです。User Access Keyトークンの発行及び使用方法は[User Access Keyトークン](/nhncloud/ja/public-api/user-access-key-token)を参照してください。
発行されたトークンはAppkeyと一緒にリクエストヘッダに含める必要があります。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|------|-----|
| X-TC-APP-KEY | Header | String | Y    | RDS for MariaDBサービスのAppkeyまたはプロジェクト統合Appkey |
| X-NHN-AUTHORIZATION | Header | String | Y    | Public APIで発行されたBearerタイプトークン |

また、プロジェクトの権限によって呼び出すことができるAPIが制限されます。`RDS for MariaDB ADMIN`、`RDS for MariaDB VIEWER`ロールには次のように基本権限が付与されており、プロジェクト内のロールグループ管理メニューで必要な権限のみを付与できます。

* `RDS for MariaDB ADMIN`ロールには、API実行に必要なすべての権限が付与されます。
* `RDS for MariaDB VIEWER`ロールには、情報を照会する権限のみ付与されます。
    * DBインスタンスを作成、修正、削除したり、DBインスタンスを対象とするいかなる機能も使用できません。
    * ただし、通知グループとユーザーグループに関連する機能は使用可能です。

APIリクエスト時、認証に失敗したり権限がない場合、次のようなエラーが発生します。

| resultCode | resultMessage | 説明 |
|------------|---------------|-----|
| 80401 | Unauthorized | 認証に失敗しました。 |
| 80403 | Forbidden | 権限がありません。 |

<a id="common-response"></a>
### レスポンス共通情報 { #common-response }

すべてのAPIリクエストに「200 OK」でレスポンスします。詳細なレスポンス結果はレスポンス本文のヘッダを参照してください。

<details>
  <summary><strong>成功レスポンス</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</details>

<details>
  <summary><strong>失敗レスポンス</strong></summary>

```json
{
    "header": {
        "resultCode": -1,
        "resultMessage": "FAIL",
        "isSuccessful": false
    }
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| resultCode | Number | 結果コード<br/>- 成功: `0`<br/>- 失敗: `0`ではない値 |
| resultMessage | String | 結果メッセージ |
| isSuccessful | Boolean | 成否 |

<a id="db-engine"></a>
## DBエンジンバージョン { #db-engine }

<a id="supported-db-engine-versions"></a>
### サポートするDBエンジンバージョン { #supported-db-engine-versions }

| DBエンジンバージョン | 作成可否 | オブジェクトストレージから復元できるかどうか | 認証プラグインサポート |
|------------|----------|------------------|------------|
| MARIADB_V10330 | N | N | ED25519, NATIVE |
| MARIADB_V10611 | N | N | ED25519, NATIVE |
| MARIADB_V10612 | N | N | ED25519, NATIVE |
| MARIADB_V10616 | N | N | ED25519, NATIVE |
| MARIADB_V10622 | N | N | ED25519, NATIVE |
| MARIADB_V10625 | N | N | ED25519, NATIVE |
| MARIADB_V101107 | Y | Y | ED25519, NATIVE |
| MARIADB_V101108 | Y | Y | ED25519, NATIVE |
| MARIADB_V101113 | Y | Y | ED25519, NATIVE |
| MARIADB_V101116 | Y | Y | ED25519, NATIVE |
| MARIADB_V101118 | Y | Y | ED25519, NATIVE |
| MARIADB_V11407 | Y | Y | ED25519, NATIVE |
| MARIADB_V11410 | Y | Y | ED25519, NATIVE |
| MARIADB_V11412 | Y | Y | ED25519, NATIVE |
| MARIADB_V11806 | Y | Y | ED25519, NATIVE |
| MARIADB_V11808 | Y | Y | ED25519, NATIVE |

* EnumタイプのdbVersionフィールドに上記の値を使用できます。
* バージョンによっては作成または復元ができない場合があります。

<a id="list-db-engines"></a>
### DBエンジンリストを表示 { #list-db-engines }

<a id="list-db-engines-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbVersion.List | DBエンジンバージョンリストを表示 |

<a id="list-db-engines-request"></a>
#### リクエスト

```http
GET /v4.0/db-versions
```

<a id="list-db-engines-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-engines-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbVersions": [
        {
            "dbVersion": "MARIADB_V11808",
            "dbVersionName": "Maria DB 11.8.8",
            "restorableFromObs": true
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbVersions | Array | DBエンジンリスト |
| dbVersions.dbVersion | Enum | DBエンジンバージョン |
| dbVersions.dbVersionName | String | DBエンジンバージョン名 |
| dbVersions.restorableFromObs | Boolean | オブジェクトストレージから復元できるかどうか |

---

<a id="project-information"></a>
## プロジェクト情報 { #project-information }

<a id="list-project-members"></a>
### プロジェクトメンバーリストを表示 { #list-project-members }

<a id="list-project-members-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Project.Get | プロジェクトメンバーリストを表示 |

<a id="list-project-members-request"></a>
#### リクエスト

```http
GET /v4.0/project/members
```

<a id="list-project-members-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-project-members-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "members": [
        {
            "memberId": "550e8400-e29b-41d4-a716-446655440000",
            "memberName": "memberName-example",
            "emailAddress": "user@example.com",
            "phoneNumber": "010-1234-5678"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| members | Array | プロジェクトメンバーリスト |
| members.memberId | UUID | プロジェクトメンバーの識別子 |
| members.memberName | String | プロジェクトメンバーの名前 |
| members.emailAddress | String | プロジェクトメンバーのメールアドレス |
| members.phoneNumber | String | プロジェクトメンバーの電話番号 |

---

<a id="list-regions"></a>
### リージョンリストを表示 { #list-regions }

<a id="list-regions-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Project.Get | リージョンリストを表示 |

<a id="list-regions-request"></a>
#### リクエスト

```http
GET /v4.0/project/regions
```

<a id="list-regions-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-regions-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "regions": [
        {
            "regionCode": "KR1",
            "isEnabled": false
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| regions | Array | リージョンリスト |
| regions.regionCode | Enum | リージョンコード<br/>- `KR1`: 韓国(パンギョ) |
| regions.isEnabled | Boolean | リージョンが有効かどうか |

---

<a id="specifications-of-db-instance"></a>
## DBインスタンスの仕様 { #specifications-of-db-instance }

<a id="list-db-instance-specifications"></a>
### DBインスタンス仕様リストを表示 { #list-db-instance-specifications }

<a id="list-db-instance-specifications-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbFlavor.List | DBインスタンス仕様リスト表示 |

<a id="list-db-instance-specifications-request"></a>
#### リクエスト

```http
GET /v4.0/db-flavors
```

<a id="list-db-instance-specifications-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-instance-specifications-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbFlavors": [
        {
            "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
            "dbFlavorName": "dbFlavorName-example",
            "ram": 1,
            "vcpus": 1
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbFlavors | Array | DBインスタンス仕様リスト |
| dbFlavors.dbFlavorId | UUID | DBインスタンス仕様の識別子 |
| dbFlavors.dbFlavorName | String | DBインスタンス仕様名 |
| dbFlavors.ram | Number | メモリ容量(MB) |
| dbFlavors.vcpus | Number | CPUコア数 |

---

<a id="network"></a>
## ネットワーク { #network }

<a id="list-subnets"></a>
### サブネットリストを表示 { #list-subnets }

<a id="list-subnets-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Network.List | サブネットリスト表示 |

<a id="list-subnets-request"></a>
#### リクエスト

```http
GET /v4.0/network/subnets
```

<a id="list-subnets-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-subnets-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "subnets": [
        {
            "subnetId": "550e8400-e29b-41d4-a716-446655440000",
            "subnetName": "subnetName-example",
            "subnetCidr": "192.168.0.0/24",
            "usingGateway": false,
            "availableIpCount": 1
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| subnets | Array | サブネットリスト |
| subnets.subnetId | UUID | サブネットの識別子 |
| subnets.subnetName | String | サブネットを識別できる名前 |
| subnets.subnetCidr | String | サブネットのCIDR |
| subnets.usingGateway | Boolean | ゲートウェイを使用するかどうか |
| subnets.availableIpCount | Number | 使用可能なIP数 |

---

<a id="storage"></a>
## データストレージ { #storage }

<a id="list-storage-type"></a>
### ストレージタイプリストを表示 { #list-storage-type }

<a id="list-storage-type-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Storage.List | ストレージタイプリストを表示 |

<a id="list-storage-type-request"></a>
#### リクエスト

```http
GET /v4.0/storage-types
```

<a id="list-storage-type-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-storage-type-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "storageTypes": [
        "General SSD",
        "General HDD"
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| storageTypes | Array | ストレージタイプリスト |

---

<a id="task-information"></a>
## 作業情報 { #task-information }

<a id="job-status"></a>
### 作業状態 { #job-status }

| 状態名                | 説明                   |
|--------------------|----------------------|
| `PREPARING`        | 作業が準備中の場合         |
| `READY`            | 作業が準備完了している場合        |
| `RUNNING`          | 作業が進行中の場合         |
| `COMPLETED`        | 作業が完了している場合           |
| `REGISTERED`       | 作業が登録されている場合           |
| `WAIT_TO_REGISTER` | 作業登録待機中の場合       |
| `INTERRUPTED`      | 作業進行中に割り込みが発生した場合 |
| `CANCELED`         | 作業がキャンセルされた場合           |
| `FAILED`           | 作業が失敗した場合           |
| `ERROR`            | 作業進行中にエラーが発生した場合   |
| `DELETED`          | 作業が削除された場合           |
| `FAIL_TO_READY`    | 作業の準備に失敗した場合        |

<a id="list-task-details"></a>
### 作業情報の詳細表示 { #list-task-details }

<a id="list-task-details-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Job.Get | 作業情報詳細表示 |

<a id="list-task-details-request"></a>
#### リクエスト

```http
GET /v4.0/jobs/{jobId}
```

<a id="list-task-details-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| jobId | URL | UUID | Y | 作業の識別子 |

<a id="list-task-details-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-task-details-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "jobStatus": "DELETED",
    "resourceRelations": [
        {
            "resourceType": "resourceType-example",
            "resourceId": "resourceId-example"
        }
    ],
    "createdYmdt": "2023-12-31T15:00:00+09:00",
    "updatedYmdt": "2023-12-31T15:00:00+09:00"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | 作業の識別子 |
| jobStatus | Enum | 作業の現在状態<br/>- `DELETED`<br/>- `CANNOT_PROGRESS`<br/>- `FAILED`<br/>- `ERROR`<br/>- `CANCELED`<br/>- `INTERRUPTED`<br/>- `COMPLETED`<br/>- `COMPLETED_WITH_ERROR`<br/>- `RUNNING`<br/>- `PREPARING`<br/>- `READY`<br/>- `CREATED`<br/>- `FAIL_TO_READY`<br/>- `REGISTERED`<br/>- `FAIL_TO_REGISTER`<br/>- `WAIT_TO_REGISTER` |
| resourceRelations | Array | 関連リソースリスト |
| resourceRelations.resourceType | String | 関連リソースタイプ |
| resourceRelations.resourceId | String | 関連リソースの識別子 |
| createdYmdt | DateTime | 作成日時 |
| updatedYmdt | DateTime | 修正日時 |

---

<a id="db-instance-group"></a>
## DBインスタンスグループ { #db-instance-group }

<a id="list-db-instance-groups"></a>
### DBインスタンスグループリストを表示 { #list-db-instance-groups }

<a id="list-db-instance-groups-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceGroup.List | DBインスタンスグループリスト表示 |

<a id="list-db-instance-groups-request"></a>
#### リクエスト

```http
GET /v4.0/db-instance-groups
```

<a id="list-db-instance-groups-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-instance-groups-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbInstanceGroups": [
        {
            "dbInstanceGroupId": "550e8400-e29b-41d4-a716-446655440000",
            "replicationType": "STANDALONE",
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbInstanceGroups | Array | DBインスタンスグループリスト |
| dbInstanceGroups.dbInstanceGroupId | UUID | DBインスタンスグループの識別子 |
| dbInstanceGroups.replicationType | Enum | DBインスタンスグループの複製形態<br/>- `STANDALONE`: 高可用性を使用しない<br/>- `HIGH_AVAILABILITY`: 高可用性を使用 |
| dbInstanceGroups.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbInstanceGroups.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="list-db-instance-group-details"></a>
### DBインスタンスグループの詳細を表示 { #list-db-instance-group-details }

<a id="list-db-instance-group-details-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceGroup.Get | DBインスタンスグループ詳細表示 |

<a id="list-db-instance-group-details-request"></a>
#### リクエスト

```http
GET /v4.0/db-instance-groups/{dbInstanceGroupId}
```

<a id="list-db-instance-group-details-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceGroupId | URL | UUID | Y | DBインスタンスグループの識別子 |

<a id="list-db-instance-group-details-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-instance-group-details-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbInstanceGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "replicationType": "STANDALONE",
    "dbInstances": [
        {
            "dbInstanceId": "550e8400-e29b-41d4-a716-446655440000",
            "dbInstanceType": "MASTER",
            "dbInstanceStatus": "AVAILABLE"
        }
    ],
    "createdYmdt": "2023-12-31T15:00:00+09:00",
    "updatedYmdt": "2023-12-31T15:00:00+09:00"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbInstanceGroupId | UUID | DBインスタンスグループの識別子 |
| replicationType | Enum | DBインスタンスグループの複製形態<br/>- `STANDALONE`: 高可用性を使用しない<br/>- `HIGH_AVAILABILITY`: 高可用性を使用 |
| dbInstances | Array | DBインスタンスグループに属するDBインスタンスリスト |
| dbInstances.dbInstanceId | UUID | DBインスタンスの識別子 |
| dbInstances.dbInstanceType | Enum | DBインスタンスのロールタイプ<br/>- `MASTER`: Primary<br/>- `FAILED_MASTER`: Failed Over Primary<br/>- `CANDIDATE_MASTER`: Standby<br/>- `READ_ONLY_SLAVE`:リードレプリカ |
| dbInstances.dbInstanceStatus | Enum | DBインスタンスの現在状態<br/>- `BEFORE_CREATE`: 作成前(グレー)<br/>- `AVAILABLE`: 使用可能(緑色)<br/>- `STORAGE_FULL`: 容量不足(赤色)<br/>- `FAIL_TO_CREATE`: 作成失敗(赤色)<br/>- `FAIL_TO_CONNECT`: 接続失敗(赤色)<br/>- `REPLICATION_STOP`: 複製中断(赤色)<br/>- `REPLICATION_DELAY`: 複製遅延(黄色)<br/>- `FAILOVER`: フェイルオーバー完了(赤色)<br/>- `SHUTDOWN`: 停止済み(グレー)<br/>- `DELETED`: 削除済み(グレー) |
| createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="db-instance"></a>
## DBインスタンス { #db-instance }

<a id="db-instance-status"></a>
### DBインスタンス状態 { #db-instance-status }

| 状態                  | 説明                           |
|---------------------|------------------------------|
| `AVAILABLE`         | DBインスタンスが使用可能な場合           |
| `BEFORE_CREATE`     | DBインスタンスが作成前の場合            |
| `STORAGE_FULL`      | DBインスタンスの容量が不足している場合          |
| `FAIL_TO_CREATE`    | DBインスタンス作成に失敗した場合           |
| `FAIL_TO_CONNECT`   | DBインスタンス接続に失敗した場合           |
| `REPLICATION_STOP`  | DBインスタンスの複製が中断した場合          |
| `FAILOVER`          | DBインスタンスが高可用性フェイルオーバーした場合      |
| `SHUTDOWN`          | DBインスタンスが停止した場合              |
| `DELETED`           | DBインスタンスが削除された場合              |

<a id="db-instance-progress-status"></a>
### DBインスタンス進行状態 { #db-instance-progress-status }

| 状態                         | 説明           |
|----------------------------|--------------|
| `APPLYING_PARAMETER_GROUP` | パラメータグループ適用中 |
| `BACKING_UP`               | バックアップ中         |
| `CANCELING`                | キャンセル中         |
| `CREATING`                 | 作成中         |
| `CREATING_SCHEMA`          | DBスキーマ作成中  |
| `CREATING_USER`            | ユーザー作成中     |
| `DELETING`                 | 削除中         |
| `DELETING_SCHEMA`          | DBスキーマ削除中  |
| `DELETING_USER`            | ユーザー削除中     |
| `EXPORTING_BACKUP`         | バックアップをエクスポート中   |
| `FAILING_OVER`             | フェイルオーバー中      |
| `MIGRATING`                | マイグレーション中     |
| `MODIFYING`                | 修正中         |
| `PREPARING`                | 準備中         |
| `PROMOTING`                | 昇格中         |
| `REBUILDING`               | 再構築中        |
| `REPAIRING`                | 復旧中         |
| `REPLICATING`              | 複製中         |
| `RESTARTING`               | 再起動中        |
| `RESTARTING_FORCIBLY`      | 強制再起動中     |
| `RESTORING`                | 復元中         |
| `STARTING`                 | 起動中         |
| `STOPPING`                 | 停止中         |
| `SYNCING_SCHEMA`           | DBスキーマ同期中 |
| `SYNCING_USER`             | ユーザー同期中    |
| `UPDATING_USER`            | ユーザー修正中     |

<a id="list-db-instances"></a>
### DBインスタンスリストを表示 { #list-db-instances }

<a id="list-db-instances-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.List | DBインスタンスリスト表示 |

<a id="list-db-instances-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances
```

<a id="list-db-instances-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-instances-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbInstances": [
        {
            "dbInstanceId": "550e8400-e29b-41d4-a716-446655440000",
            "dbInstanceGroupId": "550e8400-e29b-41d4-a716-446655440000",
            "dbInstanceName": "dbInstanceName-example",
            "description": "description-example",
            "dbVersion": "MARIADB_V11808",
            "dbPort": 13306,
            "dbInstanceType": "MASTER",
            "dbInstanceStatus": "AVAILABLE",
            "progressStatus": "NONE",
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbInstances | Array | DBインスタンスリスト |
| dbInstances.dbInstanceId | UUID | DBインスタンスの識別子 |
| dbInstances.dbInstanceGroupId | UUID | DBインスタンスグループの識別子 |
| dbInstances.dbInstanceName | String | Primary DBインスタンスを識別できる名前 |
| dbInstances.description | String | DBインスタンスの追加情報 |
| dbInstances.dbVersion | Enum | DBエンジンバージョン |
| dbInstances.dbPort | Number | DBポート |
| dbInstances.dbInstanceType | Enum | DBインスタンスのロールタイプ<br/>- `MASTER`: Primary<br/>- `FAILED_MASTER`: Failed Over Primary<br/>- `CANDIDATE_MASTER`: Standby<br/>- `READ_ONLY_SLAVE`:リードレプリカ |
| dbInstances.dbInstanceStatus | Enum | DBインスタンスの現在状態<br/>- `BEFORE_CREATE`: 作成前(グレー)<br/>- `AVAILABLE`: 使用可能(緑色)<br/>- `STORAGE_FULL`: 容量不足(赤色)<br/>- `FAIL_TO_CREATE`: 作成失敗(赤色)<br/>- `FAIL_TO_CONNECT`: 接続失敗(赤色)<br/>- `REPLICATION_STOP`: 複製中断(赤色)<br/>- `REPLICATION_DELAY`: 複製遅延(黄色)<br/>- `FAILOVER`: フェイルオーバー完了(赤色)<br/>- `SHUTDOWN`: 停止済み(グレー)<br/>- `DELETED`: 削除済み(グレー) |
| dbInstances.progressStatus | Enum | DBインスタンスの現在進行状態 |
| dbInstances.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbInstances.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-db-instance"></a>
### DBインスタンスを作成する { #create-db-instance }

<a id="create-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Create | DBインスタンスの作成 |

<a id="create-db-instance-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances
```

<a id="create-db-instance-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "description": "description-example",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "dbVersion": "MARIADB_V11808",
    "dbPort": 13306,
    "dbUserName": "dbUserName",
    "dbPassword": "dbPassword",
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbSecurityGroupIds": [],
    "userGroupIds": [],
    "useHighAvailability": false,
    "pingInterval": 3,
    "useDefaultNotification": false,
    "useDeletionProtection": false,
    "useSlowQueryAnalysis": true,
    "authenticationPlugin": "NATIVE",
    "tlsOption": "NONE",
    "network": {
        "subnetId": "550e8400-e29b-41d4-a716-446655440000",
        "usePublicAccess": false,
        "availabilityZone": "kr-pub-a"
    },
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20,
        "storageAutoscale": {
            "useStorageAutoscale": false
        }
    },
    "backup": {
        "backupPeriod": 0,
        "backupRetryCount": 0,
        "ftwrlWaitTimeout": 1800,
        "replicationRegion": "KR1",
        "useBackupLock": true,
        "backupSchedules": [
            {
                "backupWndBgnTime": "00:00:00",
                "backupWndDuration": "HALF_AN_HOUR"
            }
        ]
    }
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Primary DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | DBインスタンスの追加情報<br/>- 最大長さ: `100` |
| dbFlavorId | UUID | Y | DBインスタンス仕様の識別子 |
| dbVersion | Enum | Y | DBエンジンバージョン |
| dbPort | Number | Y | DBポート<br/>- 最小値: 3306、最大値: 43306 |
| dbUserName | String | Y | DBユーザーアカウント名<br/>- 最小長さ: `1`<br/>- 最大長さ: `32` |
| dbPassword | String | Y | DBユーザーアカウントのパスワード<br/>- 最小長さ: `4`<br/>- 最大長さ: `256` |
| parameterGroupId | UUID | Y | パラメータグループの識別子 |
| dbSecurityGroupIds | Array | N | DBセキュリティグループの識別子リスト |
| userGroupIds | Array | N | ユーザーグループの識別子リスト |
| useHighAvailability | Boolean | N | 高可用性を使用するかどうか<br/>- デフォルト値: `false` |
| pingInterval | Number | N | 高可用性使用時のPing間隔(秒)<br/>- デフォルト値: `3`<br/>- 最小値: `1`<br/>- 最大値: `600` |
| useDefaultNotification | Boolean | N | 基本通知の使用有無<br/>- デフォルト値: `false` |
| useDeletionProtection | Boolean | N | 削除保護の有無<br/>- デフォルト値: `false` |
| useSlowQueryAnalysis | Boolean | N | Slow query分析を行うかどうか<br/>- デフォルト値: `true` |
| authenticationPlugin | Enum | N | 認証プラグイン<br/>- `NATIVE`: mysql_native_password認証<br/>- `ED25519`: ed25519認証(MariaDB専用) |
| tlsOption | Enum | N | TLSオプション<br/>- デフォルト値: `NONE`<br/>- `NONE`: TLS未使用<br/>- `SSL`: SSL認証<br/>- `X509`: X509証明書認証 |
| network | Object | Y | ネットワーク情報オブジェクト |
| network.subnetId | UUID | Y | サブネットの識別子 |
| network.usePublicAccess | Boolean | N | 外部接続可否<br/>- デフォルト値: `false` |
| network.availabilityZone | Enum | Y | DBインスタンスを作成するアベイラビリティゾーン |
| storage | Object | Y | ストレージ情報オブジェクト |
| storage.storageType | Enum | Y | データストレージタイプ |
| storage.storageSize | Number | Y | データストレージサイズ(GB)<br/>- 最小値: `20` |
| storage.storageAutoscale | Object | N | データストレージ自動拡張オブジェクト |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | ストレージ自動拡張を行うかどうか<br/>- デフォルト値: `false` |
| backup | Object | Y | バックアップ情報オブジェクト |
| backup.backupPeriod | Number | Y | バックアップ保管期間(日)<br/>- 最小値: `0`<br/>- 最大値: `730` |
| backup.backupRetryCount | Number | N | バックアップ再試行回数<br/>- 最小値: `0`<br/>- 最大値: `10` |
| backup.ftwrlWaitTimeout | Number | N | クエリ遅延待機時間(秒)<br/>- 最小値: `0`<br/>- 最大値: `21600` |
| backup.replicationRegion | Enum | N | バックアップ複製リージョン<br/>- `KR1`: 韓国(パンギョ) |
| backup.useBackupLock | Boolean | N | テーブルロックを使用するかどうか<br/>- デフォルト値: `true` |
| backup.backupSchedules | Array | Y | バックアップスケジュールリスト |
| backup.backupSchedules.backupWndBgnTime | Time | Y | バックアップ開始時間 |
| backup.backupSchedules.backupWndDuration | Enum | Y | バックアップウィンドウ<br/>- `HALF_AN_HOUR`: 30分<br/>- `ONE_HOUR`: 1時間<br/>- `ONE_HOUR_AND_HALF`: 1時間30分<br/>- `TWO_HOURS`: 2時間<br/>- `TWO_HOURS_AND_HALF`: 2時間30分<br/>- `THREE_HOURS`: 3時間 |

<a id="create-db-instance-section"></a>
#### 高可用性を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Standby DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |

<a id="create-db-instance-section-2"></a>
#### ストレージ自動拡張を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | 自動拡張条件(%)<br/>- 最小値: `50`<br/>- 最大値: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | 自動拡張最大サイズ(GB)<br/>- 最大値: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | 自動拡張クールダウン時間(分)<br/>- 最小値: `10`<br/>- 最大値: `1440` |

<a id="create-db-instance-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="restore-from-object-storage"></a>
### オブジェクトストレージから復元 { #restore-from-object-storage }

<a id="restore-from-object-storage-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.RestoreFromObs | オブジェクトストレージから復元 |

<a id="restore-from-object-storage-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/restore-from-obs
```

<a id="restore-from-object-storage-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "description": "description-example",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "dbPort": 13306,
    "dbVersion": "MARIADB_V11808",
    "useHighAvailability": false,
    "pingInterval": 3,
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20,
        "storageAutoscale": {
            "useStorageAutoscale": false
        }
    },
    "network": {
        "subnetId": "550e8400-e29b-41d4-a716-446655440000",
        "usePublicAccess": false,
        "availabilityZone": "kr-pub-a"
    },
    "backup": {
        "backupPeriod": 0,
        "ftwrlWaitTimeout": 1800,
        "backupRetryCount": 0,
        "replicationRegion": "KR1",
        "useBackupLock": true,
        "backupSchedules": [
            {
                "backupWndBgnTime": "00:00:00",
                "backupWndDuration": "HALF_AN_HOUR"
            }
        ]
    },
    "restore": {
        "tenantId": "0123456789abcdef0123456789abcdef",
        "username": "username-example",
        "password": "password-example",
        "targetContainer": "targetContainer-example",
        "objectPath": "objectPath-example"
    },
    "useDefaultNotification": false,
    "useSlowQueryAnalysis": true,
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbSecurityGroupIds": [],
    "userGroupIds": [],
    "useDeletionProtection": false
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Primary DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | DBインスタンスの追加情報<br/>- 最大長さ: `100` |
| dbFlavorId | UUID | Y | DBインスタンス仕様の識別子 |
| dbPort | Number | Y | DBポート |
| dbVersion | Enum | Y | DBエンジンバージョン |
| useHighAvailability | Boolean | N | 高可用性を使用するかどうか<br/>- デフォルト値: `false` |
| pingInterval | Number | N | 高可用性使用時のPing間隔(秒)<br/>- 最小値: `1`<br/>- 最大値: `600` |
| storage | Object | Y | ストレージ情報オブジェクト |
| storage.storageType | Enum | Y | ストレージタイプ |
| storage.storageSize | Number | Y | データストレージサイズ(GB)<br/>- 最小値: `20` |
| storage.storageAutoscale | Object | N | データストレージ自動拡張オブジェクト |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | ストレージ自動拡張を行うかどうか<br/>- デフォルト値: `false` |
| network | Object | Y | ネットワーク情報オブジェクト |
| network.subnetId | UUID | Y | サブネットの識別子 |
| network.usePublicAccess | Boolean | N | 外部接続可否<br/>- デフォルト値: `false` |
| network.availabilityZone | Enum | Y | DBインスタンスを作成するアベイラビリティゾーン |
| backup | Object | Y | バックアップ情報オブジェクト |
| backup.backupPeriod | Number | Y | バックアップ保管期間(日)<br/>- 最小値: `0`<br/>- 最大値: `730` |
| backup.ftwrlWaitTimeout | Number | N | クエリ遅延待機時間(秒)<br/>- 最小値: `0`<br/>- 最大値: `21600` |
| backup.backupRetryCount | Number | N | バックアップ再試行回数<br/>- 最小値: `0`<br/>- 最大値: `10` |
| backup.replicationRegion | Enum | N | バックアップ複製リージョン<br/>- `KR1`: 韓国(パンギョ) |
| backup.useBackupLock | Boolean | N | テーブルロックを使用するかどうか<br/>- デフォルト値: `true` |
| backup.backupSchedules | Array | Y | バックアップスケジュールリスト |
| backup.backupSchedules.backupWndBgnTime | Time | Y | バックアップ開始時間 |
| backup.backupSchedules.backupWndDuration | Enum | Y | バックアップウィンドウ<br/>- `HALF_AN_HOUR`: 30分<br/>- `ONE_HOUR`: 1時間<br/>- `ONE_HOUR_AND_HALF`: 1時間30分<br/>- `TWO_HOURS`: 2時間<br/>- `TWO_HOURS_AND_HALF`: 2時間30分<br/>- `THREE_HOURS`: 3時間 |
| restore | Object | Y | 復元情報オブジェクト |
| restore.tenantId | String | Y | バックアップが保存されたオブジェクトストレージのテナントID |
| restore.username | String | Y | NHN Cloud会員またはIAMメンバーID |
| restore.password | String | Y | バックアップが保存されたオブジェクトストレージのAPIパスワード |
| restore.targetContainer | String | Y | バックアップが保存されたオブジェクトストレージのコンテナ |
| restore.objectPath | String | Y | コンテナに保存されたバックアップのパス |
| useDefaultNotification | Boolean | N | 基本通知の使用有無<br/>- デフォルト値: `false` |
| useSlowQueryAnalysis | Boolean | N | Slow query分析を行うかどうか<br/>- デフォルト値: `true` |
| parameterGroupId | UUID | Y | パラメータグループの識別子 |
| dbSecurityGroupIds | Array | N | DBセキュリティグループの識別子リスト |
| userGroupIds | Array | N | ユーザーグループの識別子リスト |
| useDeletionProtection | Boolean | N | 削除保護の有無<br/>- デフォルト値: `false` |

<a id="restore-from-object-storage-section"></a>
#### 高可用性を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Standby DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |

<a id="restore-from-object-storage-section-2"></a>
#### ストレージ自動拡張を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | 自動拡張条件(%)<br/>- 最小値: `50`<br/>- 最大値: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | 自動拡張最大サイズ(GB)<br/>- 最大値: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | 自動拡張クールダウン時間(分)<br/>- 最小値: `10`<br/>- 最大値: `1440` |

<a id="restore-from-object-storage-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="delete-db-instance"></a>
### DBインスタンスを削除する { #delete-db-instance }

<a id="delete-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Delete | DBインスタンスの削除 |

<a id="delete-db-instance-request"></a>
#### リクエスト

```http
DELETE /v4.0/db-instances/{dbInstanceId}
```

<a id="delete-db-instance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="delete-db-instance-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "deleteAutoBackup": false
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| deleteAutoBackup | Boolean | N | 自動バックアップの削除有無<br/>- デフォルト値: `false` |

<a id="delete-db-instance-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="list-db-instance-details"></a>
### DBインスタンスの詳細を表示 { #list-db-instance-details }

<a id="list-db-instance-details-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Get | DBインスタンス詳細表示 |

<a id="list-db-instance-details-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}
```

<a id="list-db-instance-details-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="list-db-instance-details-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-instance-details-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbInstanceId": "550e8400-e29b-41d4-a716-446655440000",
    "dbInstanceGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbInstanceName": "dbInstanceName-example",
    "description": "description-example",
    "dbVersion": "MARIADB_V11808",
    "dbPort": 13306,
    "dbInstanceType": "MASTER",
    "dbInstanceStatus": "AVAILABLE",
    "progressStatus": "NONE",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbSecurityGroupIds": [
        "550e8400-e29b-41d4-a716-446655440000"
    ],
    "notificationGroupIds": [
        "550e8400-e29b-41d4-a716-446655440000"
    ],
    "useDeletionProtection": false,
    "useSlowQueryAnalysis": false,
    "supportAuthenticationPlugin": false,
    "needToApplyParameterGroup": false,
    "needMigration": false,
    "supportDbVersionUpgrade": false,
    "createdYmdt": "2023-12-31T15:00:00+09:00",
    "updatedYmdt": "2023-12-31T15:00:00+09:00"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbInstanceId | UUID | DBインスタンスの識別子 |
| dbInstanceGroupId | UUID | DBインスタンスグループの識別子 |
| dbInstanceName | String | Primary DBインスタンスを識別できる名前 |
| description | String | DBインスタンスの追加情報 |
| dbVersion | Enum | DBエンジンバージョン |
| dbPort | Number | DBポート |
| dbInstanceType | Enum | DBインスタンスのロールタイプ<br/>- `MASTER`: Primary<br/>- `FAILED_MASTER`: Failed Over Primary<br/>- `CANDIDATE_MASTER`: Standby<br/>- `READ_ONLY_SLAVE`:リードレプリカ |
| dbInstanceStatus | Enum | DBインスタンスの現在状態<br/>- `BEFORE_CREATE`: 作成前(グレー)<br/>- `AVAILABLE`: 使用可能(緑色)<br/>- `STORAGE_FULL`: 容量不足(赤色)<br/>- `FAIL_TO_CREATE`: 作成失敗(赤色)<br/>- `FAIL_TO_CONNECT`: 接続失敗(赤色)<br/>- `REPLICATION_STOP`: 複製中断(赤色)<br/>- `REPLICATION_DELAY`: 複製遅延(黄色)<br/>- `FAILOVER`: フェイルオーバー完了(赤色)<br/>- `SHUTDOWN`: 停止済み(グレー)<br/>- `DELETED`: 削除済み(グレー) |
| progressStatus | Enum | DBインスタンスの現在進行状態 |
| dbFlavorId | UUID | DBインスタンス仕様の識別子 |
| parameterGroupId | UUID | DBインスタンスに適用されたパラメータグループの識別子 |
| dbSecurityGroupIds | Array | DBインスタンスに適用されたDBセキュリティグループの識別子リスト |
| notificationGroupIds | Array | DBインスタンスに適用された通知グループの識別子リスト |
| useDeletionProtection | Boolean | DBインスタンス削除保護の有無 |
| useSlowQueryAnalysis | Boolean | Slow query分析を行うかどうか |
| supportAuthenticationPlugin | Boolean | 認証プラグインサポートの有無 |
| needToApplyParameterGroup | Boolean | 最新パラメータグループの適用が必要かどうか |
| needMigration | Boolean | マイグレーションが必要かどうか |
| supportDbVersionUpgrade | Boolean | DBのバージョンアップグレードをサポートするかどうか |
| createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-db-instance"></a>
### DBインスタンスを修正する { #modify-db-instance }

<a id="modify-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Modify | DBインスタンスの修正 |

<a id="modify-db-instance-request"></a>
#### リクエスト

```http
PUT /v4.0/db-instances/{dbInstanceId}
```

<a id="modify-db-instance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="modify-db-instance-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "dbInstanceCandidateName": "dbInstanceCandidateName",
    "description": "description-example",
    "dbPort": 13306,
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbVersion": "MARIADB_V11808",
    "useSlowQueryAnalysis": false,
    "useDummy": false,
    "dbSecurityGroupIds": [],
    "executeBackup": false,
    "useOnlineFailover": false,
    "waitReplicationDelay": false,
    "useReadOnly": false
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceName | String | N | Primary DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| dbInstanceCandidateName | String | N | Standby DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | DBインスタンスの追加情報<br/>- 最大長さ: `100` |
| dbPort | Number | N | DBポート<br/>- 最小値: 3306、最大値: 43306 |
| dbFlavorId | UUID | N | DBインスタンス仕様の識別子 |
| parameterGroupId | UUID | N | パラメータグループの識別子 |
| dbVersion | Enum | N | DBエンジンバージョン |
| useSlowQueryAnalysis | Boolean | N | Slow query分析を行うかどうか |
| useDummy | Boolean | N | 単一DBインスタンスのDBバージョンアップグレード時にダミーを使用するかどうか<br/>- デフォルト値: `false` |
| dbSecurityGroupIds | Array | N | DBセキュリティグループの識別子リスト |
| executeBackup | Boolean | N | 現時点のバックアップを実行するかどうか<br/>- デフォルト値: `false` |
| useOnlineFailover | Boolean | N | フェイルオーバーを利用した再起動を行うかどうか<br/>- デフォルト値: `false` |
| waitReplicationDelay | Boolean | N | 複製遅延の解消を待機<br/>- デフォルト値: `false` |
| useReadOnly | Boolean | N | 書き込み負荷の遮断<br/>- デフォルト値: `false` |

<a id="modify-db-instance-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="view-backup-information"></a>
### バックアップ情報を表示 { #view-backup-information }

<a id="view-backup-information-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Get | バックアップ情報を表示 |

<a id="view-backup-information-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/backup-info
```

<a id="view-backup-information-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="view-backup-information-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-backup-information-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "backupPeriod": 1,
    "ftwrlWaitTimeout": 1,
    "backupRetryCount": 1,
    "replicationRegion": "KR1",
    "useBackupLock": false,
    "backupSchedules": [
        {
            "backupWndBgnTime": "00:00:00",
            "backupWndDuration": "HALF_AN_HOUR"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| backupPeriod | Number | バックアップ保管期間(日) |
| ftwrlWaitTimeout | Number | クエリ遅延待機時間(秒) |
| backupRetryCount | Number | バックアップ再試行回数 |
| replicationRegion | Enum | バックアップ複製リージョン<br/>- `KR1`: 韓国(パンギョ) |
| useBackupLock | Boolean | テーブルロックを使用するかどうか |
| backupSchedules | Array | バックアップスケジュールリスト |
| backupSchedules.backupWndBgnTime | Time | バックアップ開始時間 |
| backupSchedules.backupWndDuration | Enum | バックアップウィンドウ<br/>- `HALF_AN_HOUR`<br/>- `ONE_HOUR`<br/>- `ONE_HOUR_AND_HALF`<br/>- `TWO_HOURS`<br/>- `TWO_HOURS_AND_HALF`<br/>- `THREE_HOURS` |

---

<a id="modify-backup-information"></a>
### バックアップ情報を修正する { #modify-backup-information }

<a id="modify-backup-information-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Modify | バックアップ情報を修正する |

<a id="modify-backup-information-request"></a>
#### リクエスト

```http
PUT /v4.0/db-instances/{dbInstanceId}/backup-info
```

<a id="modify-backup-information-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="modify-backup-information-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "backupPeriod": 0,
    "ftwrlWaitTimeout": 0,
    "backupRetryCount": 0,
    "replicationRegion": "KR1",
    "useBackupLock": false,
    "backupSchedules": [
        {
            "backupWndBgnTime": "00:00:00",
            "backupWndDuration": "HALF_AN_HOUR"
        }
    ]
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| backupPeriod | Number | N | バックアップ保管期間(日)<br/>- 最小値: `0`<br/>- 最大値: `730` |
| ftwrlWaitTimeout | Number | N | クエリ遅延待機時間(秒)<br/>- 最小値: `0`<br/>- 最大値: `21600` |
| backupRetryCount | Number | N | バックアップ再試行回数<br/>- 最小値: `0`<br/>- 最大値: `10` |
| replicationRegion | Enum | N | バックアップ複製リージョン<br/>- `KR1`: 韓国(パンギョ) |
| useBackupLock | Boolean | N | テーブルロックを使用するかどうか |
| backupSchedules | Array | N | バックアップスケジュールリスト |
| backupSchedules.backupWndBgnTime | Time | Y | バックアップ開始時間 |
| backupSchedules.backupWndDuration | Enum | Y | バックアップウィンドウ<br/>- `HALF_AN_HOUR`: 30分<br/>- `ONE_HOUR`: 1時間<br/>- `ONE_HOUR_AND_HALF`: 1時間30分<br/>- `TWO_HOURS`: 2時間<br/>- `TWO_HOURS_AND_HALF`: 2時間30分<br/>- `THREE_HOURS`: 3時間 |

<a id="modify-backup-information-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="view-binlog-lists"></a>
### BinLog一覧照会 { #view-binlog-lists }

<a id="view-binlog-lists-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceBinLog.List | BinLog一覧照会 |

<a id="view-binlog-lists-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/binlogs
```

<a id="view-binlog-lists-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |
| deletable | Query | Boolean | N | 削除可能なBinLogのみ照会するかどうか(true: 最後のBinLogを除外、false: 全体)<br/>- デフォルト値: `false` |

<a id="view-binlog-lists-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-binlog-lists-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "binLogs": [
        {
            "binLogFileName": "binLogFileName-example",
            "binLogFileSize": 1,
            "createdYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| binLogs | Array | BinLogファイル一覧 |
| binLogs.binLogFileName | String | BinLogファイル名 |
| binLogs.binLogFileSize | Number | BinLogファイルサイズ(Byte) |
| binLogs.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="delete-binlog"></a>
### BinLog削除 { #delete-binlog }

<a id="delete-binlog-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceBinLog.Purge | BinLog削除 |

<a id="delete-binlog-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/binlogs/purge
```

<a id="delete-binlog-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="delete-binlog-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "lastBinLogFileName": "mysql-bin.000010"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| lastBinLogFileName | String | Y | 削除する最後のBinLogファイル名(該当ファイルの直前まで削除されます) |

<a id="delete-binlog-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="view-certificate-file-lists"></a>
### 証明書ファイル一覧照会 { #view-certificate-file-lists }

<a id="view-certificate-file-lists-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceCertificate.List | 証明書ファイル一覧照会 |

<a id="view-certificate-file-lists-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/certificates
```

<a id="view-certificate-file-lists-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="view-certificate-file-lists-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-certificate-file-lists-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "certificates": [
        {
            "fileName": "fileName-example",
            "certificateType": "CA_FILE",
            "fileSize": 1,
            "createdYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| certificates | Array | 証明書ファイル一覧 |
| certificates.fileName | String | 証明書ファイル名 |
| certificates.certificateType | Enum | 証明書タイプ<br/>- `CA_FILE`<br/>- `CERT_FILE`<br/>- `KEY_FILE` |
| certificates.fileSize | Number | 証明書ファイルサイズ(Byte) |
| certificates.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="export-a-certificate-file"></a>
### 証明書ファイルエクスポート { #export-a-certificate-file }

<a id="export-a-certificate-file-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceCertificate.Export | 証明書ファイルエクスポート |

<a id="export-a-certificate-file-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/certificates/upload
```

<a id="export-a-certificate-file-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="export-a-certificate-file-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "certificateTypes": [],
    "tenantId": "0123456789abcdef0123456789abcdef",
    "username": "username-example",
    "password": "password-example",
    "targetContainer": "targetContainer-example",
    "objectPath": "objectPath-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| certificateTypes | Array | Y | アップロードする証明書タイプリスト |
| tenantId | String | Y | 証明書ファイルが保存されるオブジェクトストレージのテナントID<br/>- 最小長さ: `32`<br/>- 最大長さ: `32` |
| username | String | Y | NHN CloudメンバーまたはIAMアカウントID |
| password | String | Y | 証明書ファイルが保存されるオブジェクトストレージのAPIパスワード |
| targetContainer | String | Y | 証明書ファイルが保存されるオブジェクトストレージのコンテナ |
| objectPath | String | Y | コンテナに保存される証明書ファイルのパス |

<a id="export-a-certificate-file-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="list-db-schema"></a>
### DBスキーマリストを表示 { #list-db-schema }

<a id="list-db-schema-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceSchema.List | DBスキーマリストを表示 |

<a id="list-db-schema-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/db-schemas
```

<a id="list-db-schema-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="list-db-schema-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-schema-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbSchemas": [
        {
            "dbSchemaId": "550e8400-e29b-41d4-a716-446655440000",
            "dbSchemaName": "dbSchemaName-example",
            "dbSchemaStatus": "STABLE",
            "createdYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbSchemas | Array | DBスキーマリスト |
| dbSchemas.dbSchemaId | UUID | DBスキーマの識別子 |
| dbSchemas.dbSchemaName | String | DBスキーマ名 |
| dbSchemas.dbSchemaStatus | Enum | DBスキーマの現在状態<br/>- `STABLE`<br/>- `CREATING`<br/>- `SYNCING`<br/>- `DELETING`<br/>- `DELETED` |
| dbSchemas.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-db-schema"></a>
### DBスキーマを作成する { #create-db-schema }

<a id="create-db-schema-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceSchema.Create | DBスキーマを作成する |

<a id="create-db-schema-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/db-schemas
```

<a id="create-db-schema-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="create-db-schema-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbSchemaName": "dbSchemaName-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbSchemaName | String | Y | DBスキーマ名<br/>- 最大長さ: `64`<br/>- 英字で始まり、英字/数字/_が使用可能、1文字から64文字、MySQL予約語は使用不可 |

<a id="create-db-schema-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="delete-db-schema"></a>
### DBスキーマを削除する { #delete-db-schema }

<a id="delete-db-schema-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceSchema.Delete | DBスキーマを削除する |

<a id="delete-db-schema-request"></a>
#### リクエスト

```http
DELETE /v4.0/db-instances/{dbInstanceId}/db-schemas/{dbSchemaId}
```

<a id="delete-db-schema-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |
| dbSchemaId | URL | UUID | Y | DBスキーマの識別子 |

<a id="delete-db-schema-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-db-schema-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="list-db-users"></a>
### DBユーザーリストを表示 { #list-db-users }

<a id="list-db-users-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceUser.List | DBユーザーリストを表示 |

<a id="list-db-users-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/db-users
```

<a id="list-db-users-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="list-db-users-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-users-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbUsers": [
        {
            "dbUserId": "550e8400-e29b-41d4-a716-446655440000",
            "dbUserName": "dbUserName-example",
            "host": "192.168.0.1",
            "authorityType": "CUSTOM",
            "dbUserStatus": "STABLE",
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00",
            "authenticationPlugin": "NATIVE",
            "tlsOption": "NONE"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbUsers | Array | DBユーザーリスト |
| dbUsers.dbUserId | UUID | DBユーザーの識別子 |
| dbUsers.dbUserName | String | DBユーザーアカウント名 |
| dbUsers.host | String | DBユーザーアカウントのホスト名 |
| dbUsers.authorityType | Enum | DBユーザー権限タイプ<br/>- `CUSTOM`: ユーザー定義権限<br/>- `READ`: 読み取り権限<br/>- `CRUD`: CRUD権限<br/>- `DDL`: DDL権限<br/>- `ALL`: 全体権限 |
| dbUsers.dbUserStatus | Enum | DBユーザーの現在状態<br/>- `STABLE`<br/>- `CREATING`<br/>- `UPDATING`<br/>- `SYNCING`<br/>- `DELETING`<br/>- `DELETED` |
| dbUsers.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbUsers.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbUsers.authenticationPlugin | Enum | ユーザー認証プラグイン<br/>- `NATIVE`: mysql_native_password認証<br/>- `ED25519`: ed25519認証(MariaDB専用) |
| dbUsers.tlsOption | Enum | 証明書オプション<br/>- `NONE`: TLS未使用<br/>- `SSL`: SSL認証<br/>- `X509`: X509証明書認証 |

---

<a id="create-db-user"></a>
### DBユーザーを作成する { #create-db-user }

<a id="create-db-user-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceUser.Create | DBユーザーを作成する |

<a id="create-db-user-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/db-users
```

<a id="create-db-user-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="create-db-user-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbUserName": "dbUserName",
    "dbPassword": "dbPassword",
    "host": "192.168.0.1",
    "authorityType": "CUSTOM",
    "authenticationPlugin": "NATIVE",
    "tlsOption": "NONE"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbUserName | String | Y | DBユーザーアカウント名<br/>- 最小長さ: `1`<br/>- 最大長さ: `32` |
| dbPassword | String | Y | DBユーザーアカウントのパスワード<br/>- 最小長さ: `4`<br/>- 最大長さ: `256` |
| host | String | Y | DBユーザーアカウントのホスト名<br/>- 最大長さ: `45` |
| authorityType | Enum | Y | DBユーザー権限タイプ<br/>- `CUSTOM`: ユーザー定義権限<br/>- `READ`: 読み取り権限<br/>- `CRUD`: CRUD権限<br/>- `DDL`: DDL権限<br/>- `ALL`: 全体権限 |
| authenticationPlugin | Enum | N | ユーザー認証プラグイン<br/>- `NATIVE`: mysql_native_password認証<br/>- `ED25519`: ed25519認証(MariaDB専用) |
| tlsOption | Enum | N | 証明書オプション<br/>- デフォルト値: `NONE`<br/>- `NONE`: TLS未使用<br/>- `SSL`: SSL認証<br/>- `X509`: X509証明書認証 |

<a id="create-db-user-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="delete-db-user"></a>
### DBユーザーを削除する { #delete-db-user }

<a id="delete-db-user-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceUser.Delete | DBユーザーを削除する |

<a id="delete-db-user-request"></a>
#### リクエスト

```http
DELETE /v4.0/db-instances/{dbInstanceId}/db-users/{dbUserId}
```

<a id="delete-db-user-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |
| dbUserId | URL | UUID | Y | DBユーザーの識別子 |

<a id="delete-db-user-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-db-user-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="modify-db-user"></a>
### DBユーザーを修正する { #modify-db-user }

<a id="modify-db-user-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceUser.Modify | DBユーザーを修正する |

<a id="modify-db-user-request"></a>
#### リクエスト

```http
PUT /v4.0/db-instances/{dbInstanceId}/db-users/{dbUserId}
```

<a id="modify-db-user-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |
| dbUserId | URL | UUID | Y | DBユーザーの識別子 |

<a id="modify-db-user-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbPassword": "dbPassword",
    "authorityType": "CUSTOM",
    "authenticationPlugin": "NATIVE",
    "tlsOption": "NONE"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbPassword | String | N | DBユーザーアカウントのパスワード<br/>- 最小長さ: `4`<br/>- 最大長さ: `256` |
| authorityType | Enum | N | DBユーザー権限タイプ<br/>- `CUSTOM`: ユーザー定義権限<br/>- `READ`: 読み取り権限<br/>- `CRUD`: CRUD権限<br/>- `DDL`: DDL権限<br/>- `ALL`: 全体権限 |
| authenticationPlugin | Enum | N | ユーザー認証プラグイン<br/>- `NATIVE`: mysql_native_password認証<br/>- `ED25519`: ed25519認証(MariaDB専用) |
| tlsOption | Enum | N | 証明書オプション<br/>- `NONE`: TLS未使用<br/>- `SSL`: SSL認証<br/>- `X509`: X509証明書認証 |

<a id="modify-db-user-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="change-db-instance-deletion-protection-settings"></a>
### DBインスタンス削除保護設定を変更する { #change-db-instance-deletion-protection-settings }

<a id="change-db-instance-deletion-protection-settings-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Modify | DBインスタンス削除保護設定を変更する |

<a id="change-db-instance-deletion-protection-settings-request"></a>
#### リクエスト

```http
PUT /v4.0/db-instances/{dbInstanceId}/deletion-protection
```

<a id="change-db-instance-deletion-protection-settings-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="change-db-instance-deletion-protection-settings-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "useDeletionProtection": false
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| useDeletionProtection | Boolean | Y | 削除保護の有無 |

<a id="change-db-instance-deletion-protection-settings-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="force-restart-db-instance"></a>
### DBインスタンスを強制再起動する { #force-restart-db-instance }

<a id="force-restart-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.ForceRestart | DBインスタンスの強制再起動 |

<a id="force-restart-db-instance-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/force-restart
```

<a id="force-restart-db-instance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="force-restart-db-instance-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="force-restart-db-instance-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="high-availability-status"></a>
### 高可用性の状態 { #high-availability-status }

| 状態                               | 説明                              |
|----------------------------------|---------------------------------|
| `CREATED`                        | 高可用性が作成された場合                    |
| `STABLE`                         | 高可用性が正常な場合                    |
| `PAUSING`                        | 高可用性が一時停止中の場合               |
| `PAUSED`                         | 高可用性が一時停止された場合                 |
| `PAUSED_DUE_TO_TASK`             | タスクにより高可用性が一時停止された場合         |
| `PAUSED_DUE_TO_STOP`             | DBインスタンスの停止により高可用性が一時停止した場合  |
| `DISABLE_MASTER_IN_REPLICATION`  | Primaryの異常複製検知により高可用性が中断した場合     |
| `DISABLE_MHA_PROCESS`            | 高可用性プロセスが中断された場合               |
| `DISABLE_REPLICATION_STOP`       | レプリケーションの中断により高可用性が中断された場合         |
| `DISABLE_REPLICATION_DELAY`      | レプリケーションの遅延により高可用性が中断された場合         |
| `MASTER_FAILURE_DETECTION`       | Primaryの障害が検知された場合                  |
| `FAILOVER_STARTED`               | フェイルオーバーが開始された場合                   |
| `FAILOVER_FAILED`                | フェイルオーバーが失敗した場合                   |
| `FAILOVER_COMPLETED`             | フェイルオーバーが完了した場合                   |
| `DELETED`                        | 高可用性が削除された場合                    |

---

<a id="view-high-availability-information"></a>
### 高可用性情報の照会 { #view-high-availability-information }

<a id="view-high-availability-information-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Get | 高可用性情報の照会 |

<a id="view-high-availability-information-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/high-availability
```

<a id="view-high-availability-information-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="view-high-availability-information-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-high-availability-information-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "useHighAvailability": false,
    "haStatus": "CREATED",
    "pingInterval": 1,
    "pingType": "CONNECTION"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| useHighAvailability | Boolean | 高可用性を使用するかどうか<br/>- デフォルト値: `false` |
| haStatus | Enum | 高可用性の状態<br/>- `CREATED`: 作成済み<br/>- `STABLE`: 正常<br/>- `PAUSING`: 一時停止中<br/>- `DISABLE`: 停止<br/>- `DISABLE_MASTER_IN_REPLICATION`: Primaryの異常複製検知による高可用性の中断<br/>- `DISABLE_MHA_PROCESS`: 高可用性プロセスの中断<br/>- `DISABLE_REPLICATION_STOP`: 複製中断による高可用性の中断<br/>- `DISABLE_REPLICATION_DELAY`: 複製遅延による高可用性の中断<br/>- `FAILOVER_STARTED`: フェイルオーバー開始<br/>- `FAILOVER_FAILED`: フェイルオーバー失敗<br/>- `FAILOVER_COMPLETED`: フェイルオーバー完了<br/>- `DELETED`:削除済み<br/>- `PAUSED`: 一時停止<br/>- `PAUSED_DUE_TO_TASK`: 作業による一時停止<br/>- `PAUSED_DUE_TO_STOP`: DBインスタンス停止による一時停止<br/>- `MASTER_FAILURE_DETECTION`: Primary障害検知 |
| pingInterval | Number | Ping間隔(秒) |
| pingType | Enum | Ping方式<br/>- `CONNECTION`: CONNECTION方式<br/>- `INSERT`: INSERT方式<br/>- `SELECT`: SELECT方式 |

---

<a id="modify-high-availability"></a>
### 高可用性を修正する { #modify-high-availability }

<a id="modify-high-availability-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:HighAvailability.Modify | 高可用性の修正 |

<a id="modify-high-availability-request"></a>
#### リクエスト

```http
PUT /v4.0/db-instances/{dbInstanceId}/high-availability
```

<a id="modify-high-availability-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="modify-high-availability-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "useHighAvailability": false,
    "pingInterval": 1
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| useHighAvailability | Boolean | Y | 高可用性を使用するかどうか |
| pingInterval | Number | N | 高可用性使用時のPing間隔(秒)<br/>- 最小値: `1`<br/>- 最大値: `600` |

<a id="modify-high-availability-section"></a>
#### 高可用性を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Standby DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |

<a id="modify-high-availability-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="pause-high-availability"></a>
### 高可用性を一時停止する { #pause-high-availability }

<a id="pause-high-availability-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:HighAvailability.Pause | 高可用性の一時停止 |

<a id="pause-high-availability-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/pause
```

<a id="pause-high-availability-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="pause-high-availability-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="pause-high-availability-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="recover-high-availability"></a>
### 高可用性を復旧する { #recover-high-availability }

<a id="recover-high-availability-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:HighAvailability.Repair | 高可用性の復旧 |

<a id="recover-high-availability-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/repair
```

<a id="recover-high-availability-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="recover-high-availability-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="recover-high-availability-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="restart-high-availability"></a>
### 高可用性を再開する { #restart-high-availability }

<a id="restart-high-availability-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:HighAvailability.Resume | 高可用性の再開 |

<a id="restart-high-availability-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/resume
```

<a id="restart-high-availability-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="restart-high-availability-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="restart-high-availability-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="separate-high-availability"></a>
### 高可用性を分離する { #separate-high-availability }

<a id="separate-high-availability-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:HighAvailability.Split | 高可用性の分離 |

<a id="separate-high-availability-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/split
```

<a id="separate-high-availability-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="separate-high-availability-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="separate-high-availability-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="list-log-files"></a>
### ログファイルリスト表示 { #list-log-files }

<a id="list-log-files-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceLog.List | ログファイルリスト表示 |

<a id="list-log-files-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/log-files
```

<a id="list-log-files-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |
| logFileTypes | Query | Array | N | ログファイルタイプリスト |

<a id="list-log-files-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-log-files-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "logFiles": [
        {
            "logFileName": "logFileName-example",
            "logFileType": "ERROR",
            "logFileSize": 1,
            "createdYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| logFiles | Array | ログファイルリスト |
| logFiles.logFileName | String | ログファイル名 |
| logFiles.logFileType | Enum | ログファイルタイプ<br/>- `ERROR`<br/>- `BINLOG`<br/>- `GENERAL`<br/>- `SLOW_QUERY`<br/>- `AUDIT`<br/>- `BACKUP` |
| logFiles.logFileSize | Number | ログファイルサイズ(Byte) |
| logFiles.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="export-log-file"></a>
### ログファイルのエクスポート { #export-log-file }

<a id="export-log-file-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceLog.Export | ログファイルのエクスポート |

<a id="export-log-file-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/log-files/export
```

<a id="export-log-file-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="export-log-file-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "logFileNames": [],
    "tenantId": "0123456789abcdef0123456789abcdef",
    "username": "username-example",
    "password": "password-example",
    "targetContainer": "targetContainer-example",
    "objectPath": "objectPath-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| logFileNames | Array | Y | ログファイル名リスト |
| tenantId | String | Y | ログファイルが保存されるオブジェクトストレージのテナントID<br/>- 最小長さ: `32`<br/>- 最大長さ: `32` |
| username | String | Y | NHN CloudメンバーまたはIAMアカウントID |
| password | String | Y | ログファイルが保存されるオブジェクトストレージのAPIパスワード |
| targetContainer | String | Y | ログファイルが保存されるオブジェクトストレージのコンテナ |
| objectPath | String | Y | コンテナに保存されるログファイルのパス |

<a id="export-log-file-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="view-log-file-contents"></a>
### ログファイルの内容照会 { #view-log-file-contents }

<a id="view-log-file-contents-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstanceLog.Get | ログファイルの内容照会 |

<a id="view-log-file-contents-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/log-files/{logFileName}
```

<a id="view-log-file-contents-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |
| logFileName | URL | UUID | Y | ログファイル名 |
| logFileType | Query | Enum | Y | ログファイルタイプ<br/>- `ERROR`<br/>- `BINLOG`<br/>- `GENERAL`<br/>- `SLOW_QUERY`<br/>- `AUDIT`<br/>- `BACKUP` |

<a id="view-log-file-contents-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-log-file-contents-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "content": "content-example"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| content | String | ログファイルの内容(最大65533 bytes) |

---

<a id="get-maintenances"></a>
### DBインスタンスのメンテナンス一覧照会 { #get-maintenances }

<a id="get-maintenances-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Maintenance.List | DBインスタンスのメンテナンス一覧照会 |

<a id="get-maintenances-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/maintenances
```

<a id="get-maintenances-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |
| type | Query | String | N |  |
| statuses | Query | String | N |  |
| category | Query | String | N |  |

<a id="get-maintenances-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="get-maintenances-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "totalCounts": 1,
    "maintenances": [
        {
            "maintenanceId": "550e8400-e29b-41d4-a716-446655440000",
            "dbInstanceId": "550e8400-e29b-41d4-a716-446655440000",
            "category": "USER",
            "description": "description-example",
            "type": "UPDATE_DB_INSTANCE",
            "payload": {
            },
            "required": false,
            "deadlineYmdt": "2023-12-31T15:00:00+09:00",
            "status": "PENDING",
            "executionType": "SCHEDULED",
            "addedYmdt": "2023-12-31T15:00:00+09:00",
            "executionStartedYmdt": "2023-12-31T15:00:00+09:00",
            "executionCompletedYmdt": "2023-12-31T15:00:00+09:00",
            "haPairSynced": false
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| totalCounts | Number | メンテナンスリストの件数 |
| maintenances | Array | メンテナンスリスト |
| maintenances.maintenanceId | UUID | メンテナンスID |
| maintenances.dbInstanceId | UUID | DBインスタンスID |
| maintenances.category | Enum | メンテナンスカテゴリー<br/>- `USER`: ユーザーメンテナンスカテゴリー<br/>- `PROVIDER`: Providerメンテナンスカテゴリー<br/>- `AUTO`: 自動メンテナンスカテゴリー |
| maintenances.description | String | メンテナンスの説明 |
| maintenances.type | Enum | メンテナンスタイプ<br/>- `UPDATE_DB_INSTANCE`: DBインスタンスの修正(仕様変更、ポート変更、パラメータグループ変更)<br/>- `UPGRADE_ENGINE_VERSION`: エンジンバージョンのアップグレード<br/>- `APPLY_CHANGE_PARAMETER`: パラメータグループのパラメータ変更<br/>- `UPGRADE_OS`: OSバージョンのアップグレード<br/>- `PATCH_SECURITY`: セキュリティアップデート<br/>- `MIGRATION`: ハイパーバイザー点検のためのマイグレーション<br/>- `CLEANUP_STORAGE`: ストレージの整理 |
| maintenances.payload | Object | メンテナンスタイプによるPayload |
| maintenances.required | Boolean | メンテナンスが必須かどうか |
| maintenances.deadlineYmdt | DateTime | メンテナンス強制適用日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| maintenances.status | Enum | メンテナンス状態<br/>- `PENDING`: 待機<br/>- `READY`: 準備<br/>- `RUNNING`: 実行中<br/>- `COMPLETED`: 完了<br/>- `FAILED`: 失敗<br/>- `EXCLUDED`: 除外<br/>- `DELETED`: 削除<br/>- `SUSPENDED`: 保留<br/>- `UNKNOWN` |
| maintenances.executionType | Enum | メンテナンス実行タイプ<br/>- `SCHEDULED`: 予約実行(メンテナンス期間に自動実行)<br/>- `MANUAL`: 手動実行(即時実行)<br/>- `FORCED`: 強制実行(デッドライン超過による自動実行) |
| maintenances.addedYmdt | DateTime | メンテナンススケジュール登録日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| maintenances.executionStartedYmdt | DateTime | メンテナンス開始日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| maintenances.executionCompletedYmdt | DateTime | メンテナンス終了日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| maintenances.haPairSynced | Boolean | HAペアを同期するかどうか |

---

<a id="execute-maintenance-now"></a>
### DBインスタンスのメンテナンスを即時実行する { #execute-maintenance-now }

<a id="execute-maintenance-now-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Maintenance.Execute | DBインスタンスのメンテナンスを即時実行する |

<a id="execute-maintenance-now-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/maintenances/execute-now
```

<a id="execute-maintenance-now-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="execute-maintenance-now-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "configId": "configId-example",
    "category": "USER",
    "description": "description-example",
    "type": "UPDATE_DB_INSTANCE",
    "payload": "payload-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| configId | String | Y | 設定ID |
| category | Enum | Y | メンテナンスカテゴリー<br/>- `USER`: ユーザーメンテナンスカテゴリー<br/>- `PROVIDER`: Providerメンテナンスカテゴリー<br/>- `AUTO`: 自動メンテナンスカテゴリー |
| description | String | N | メンテナンスの説明 |
| type | Enum | Y | メンテナンスタイプ<br/>- `UPDATE_DB_INSTANCE`: DBインスタンスの修正(仕様変更、ポート変更、パラメータグループ変更)<br/>- `UPGRADE_ENGINE_VERSION`: エンジンバージョンのアップグレード<br/>- `APPLY_CHANGE_PARAMETER`: パラメータグループのパラメータ変更<br/>- `UPGRADE_OS`: OSバージョンのアップグレード<br/>- `PATCH_SECURITY`: セキュリティアップデート<br/>- `MIGRATION`: ハイパーバイザー点検のためのマイグレーション<br/>- `CLEANUP_STORAGE`: ストレージの整理 |
| payload | String | Y | メンテナンスタイプによるPayload |

<a id="execute-maintenance-now-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="schedule-maintenance"></a>
### DBインスタンスのメンテナンスを予約する { #schedule-maintenance }

<a id="schedule-maintenance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Maintenance.Update | DBインスタンスのメンテナンスを予約する |

<a id="schedule-maintenance-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/maintenances/schedule
```

<a id="schedule-maintenance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="schedule-maintenance-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "configId": "configId-example",
    "category": "USER",
    "description": "description-example",
    "type": "UPDATE_DB_INSTANCE",
    "payload": "payload-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| configId | String | Y | 設定ID |
| category | Enum | Y | メンテナンスカテゴリー<br/>- `USER`: ユーザーメンテナンスカテゴリー<br/>- `PROVIDER`: Providerメンテナンスカテゴリー<br/>- `AUTO`: 自動メンテナンスカテゴリー |
| description | String | N | メンテナンスの説明 |
| type | Enum | Y | メンテナンスタイプ<br/>- `UPDATE_DB_INSTANCE`: DBインスタンスの修正(仕様変更、ポート変更、パラメータグループ変更)<br/>- `UPGRADE_ENGINE_VERSION`: エンジンバージョンのアップグレード<br/>- `APPLY_CHANGE_PARAMETER`: パラメータグループのパラメータ変更<br/>- `UPGRADE_OS`: OSバージョンのアップグレード<br/>- `PATCH_SECURITY`: セキュリティアップデート<br/>- `MIGRATION`: ハイパーバイザー点検のためのマイグレーション<br/>- `CLEANUP_STORAGE`: ストレージの整理 |
| payload | String | Y | メンテナンスタイプによるPayload |

<a id="schedule-maintenance-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="delete-maintenance"></a>
### DBインスタンスのメンテナンスを削除する { #delete-maintenance }

<a id="delete-maintenance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Maintenance.Delete | DBインスタンスのメンテナンスを削除する |

<a id="delete-maintenance-request"></a>
#### リクエスト

```http
DELETE /v4.0/db-instances/{dbInstanceId}/maintenances/{maintenanceId}
```

<a id="delete-maintenance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |
| maintenanceId | URL | UUID | Y | メンテナンスID |

<a id="delete-maintenance-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-maintenance-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="list-network-information"></a>
### ネットワーク情報表示 { #list-network-information }

<a id="list-network-information-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Get | ネットワーク情報表示 |

<a id="list-network-information-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/network-info
```

<a id="list-network-information-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="list-network-information-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-network-information-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "availabilityZone": "kr-pub-a",
    "subnet": {
        "subnetId": "550e8400-e29b-41d4-a716-446655440000",
        "subnetName": "subnetName-example",
        "subnetCidr": "192.168.0.0/24"
    },
    "endPoints": [
        {
            "domain": "domain-example",
            "ipAddress": "192.168.0.1",
            "endPointType": "https://example.com"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| availabilityZone | String | DBインスタンスを作成するアベイラビリティゾーン |
| subnet | Object | サブネットオブジェクト |
| subnet.subnetId | UUID | サブネットの識別子 |
| subnet.subnetName | String | サブネットを識別できる名前 |
| subnet.subnetCidr | String | サブネットのCIDR |
| endPoints | Array | 接続情報リスト |
| endPoints.domain | String | ドメイン |
| endPoints.ipAddress | String | IPアドレス |
| endPoints.endPointType | String | 接続情報タイプ |

---

<a id="modify-network-information"></a>
### ネットワーク情報を修正する { #modify-network-information }

<a id="modify-network-information-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Modify | ネットワーク情報を修正する |

<a id="modify-network-information-request"></a>
#### リクエスト

```http
PUT /v4.0/db-instances/{dbInstanceId}/network-info
```

<a id="modify-network-information-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="modify-network-information-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "usePublicAccess": false
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| usePublicAccess | Boolean | Y | 外部接続可否 |

<a id="modify-network-information-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="promote-db-instance"></a>
### DBインスタンスを昇格する { #promote-db-instance }

<a id="promote-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Promote | DBインスタンスの昇格 |

<a id="promote-db-instance-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/promote
```

<a id="promote-db-instance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="promote-db-instance-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="promote-db-instance-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="rebuild-db-instance"></a>
### DBインスタンスの再構築 { #rebuild-db-instance }

<a id="rebuild-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Rebuild | DBインスタンスの再構築 |

<a id="rebuild-db-instance-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/rebuild
```

<a id="rebuild-db-instance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="rebuild-db-instance-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="rebuild-db-instance-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="replicate-db-instance"></a>
### DBインスタンスを複製する { #replicate-db-instance }

<a id="replicate-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Replicate | DBインスタンスの複製 |

<a id="replicate-db-instance-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/replicate
```

<a id="replicate-db-instance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="replicate-db-instance-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "description": "description-example",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "dbPort": 13306,
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbSecurityGroupIds": [],
    "userGroupIds": [],
    "useDefaultNotification": false,
    "useDeletionProtection": false,
    "useSlowQueryAnalysis": true,
    "network": {
        "usePublicAccess": false,
        "availabilityZone": "kr-pub-a"
    },
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20,
        "storageAutoscale": {
            "useStorageAutoscale": false
        }
    },
    "backup": {
        "backupPeriod": 0,
        "backupRetryCount": 0,
        "ftwrlWaitTimeout": 0,
        "replicationRegion": "KR1",
        "useBackupLock": false,
        "backupSchedules": [
            {
                "backupWndBgnTime": "00:00:00",
                "backupWndDuration": "HALF_AN_HOUR"
            }
        ]
    }
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Primary DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | DBインスタンスの追加情報<br/>- 最大長さ: `100` |
| dbFlavorId | UUID | N | DBインスタンス仕様の識別子 |
| dbPort | Number | N | DBポート<br/>- 最小値: 3306、最大値: 43306 |
| parameterGroupId | UUID | N | パラメータグループの識別子 |
| dbSecurityGroupIds | Array | N | DBセキュリティグループの識別子リスト |
| userGroupIds | Array | N | ユーザーグループの識別子リスト |
| useDefaultNotification | Boolean | N | 基本通知の使用有無<br/>- デフォルト値: `false` |
| useDeletionProtection | Boolean | N | 削除保護の有無<br/>- デフォルト値: `false` |
| useSlowQueryAnalysis | Boolean | N | Slow query分析を行うかどうか<br/>- デフォルト値: `true` |
| network | Object | Y | ネットワーク情報オブジェクト |
| network.usePublicAccess | Boolean | N | 外部接続可否 |
| network.availabilityZone | Enum | Y | DBインスタンスを作成するアベイラビリティゾーン |
| storage | Object | N | ストレージ情報オブジェクト |
| storage.storageType | Enum | N | データストレージタイプ |
| storage.storageSize | Number | N | データストレージサイズ(GB)<br/>- 最小値: `20` |
| storage.storageAutoscale | Object | N | データストレージ自動拡張オブジェクト |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | ストレージ自動拡張を行うかどうか<br/>- デフォルト値: `false` |
| backup | Object | N | バックアップ情報オブジェクト |
| backup.backupPeriod | Number | N | バックアップ保管期間(日)<br/>- 最小値: `0`<br/>- 最大値: `730` |
| backup.backupRetryCount | Number | N | バックアップ再試行回数<br/>- 最小値: `0`<br/>- 最大値: `10` |
| backup.ftwrlWaitTimeout | Number | N | クエリ遅延待機時間(秒)<br/>- 最小値: `0`<br/>- 最大値: `21600` |
| backup.replicationRegion | Enum | N | バックアップ複製リージョン<br/>- `KR1`: 韓国(パンギョ) |
| backup.useBackupLock | Boolean | N | テーブルロックを使用するかどうか |
| backup.backupSchedules | Array | N | バックアップスケジュールリスト |
| backup.backupSchedules.backupWndBgnTime | Time | N | バックアップ開始時間 |
| backup.backupSchedules.backupWndDuration | Enum | N | バックアップウィンドウ<br/>- `HALF_AN_HOUR`: 30分<br/>- `ONE_HOUR`: 1時間<br/>- `ONE_HOUR_AND_HALF`: 1時間30分<br/>- `TWO_HOURS`: 2時間<br/>- `TWO_HOURS_AND_HALF`: 2時間30分<br/>- `THREE_HOURS`: 3時間 |

<a id="replicate-db-instance-section"></a>
#### ストレージ自動拡張を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | 自動拡張条件(%)<br/>- 最小値: `50`<br/>- 最大値: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | 自動拡張最大サイズ(GB)<br/>- 最大値: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | 自動拡張クールダウン時間(分)<br/>- 最小値: `10`<br/>- 最大値: `1440` |

<a id="replicate-db-instance-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="restart-db-instance"></a>
### DBインスタンスを再起動する { #restart-db-instance }

<a id="restart-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Restart | DBインスタンスの再起動 |

<a id="restart-db-instance-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/restart
```

<a id="restart-db-instance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="restart-db-instance-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "useOnlineFailover": false,
    "executeBackup": false,
    "waitReplicationDelay": false,
    "useReadOnly": false,
    "osRestart": false
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| useOnlineFailover | Boolean | N | フェイルオーバーを利用した再起動を行うかどうか<br/>- デフォルト値: `false` |
| executeBackup | Boolean | N | 現時点のバックアップを実行するかどうか<br/>- デフォルト値: `false` |
| waitReplicationDelay | Boolean | N | 複製遅延の解消を待機<br/>- デフォルト値: `false` |
| useReadOnly | Boolean | N | 書き込み負荷の遮断<br/>- デフォルト値: `false` |
| osRestart | Boolean | N | OSを再起動するかどうか<br/>- デフォルト値: `false` |

<a id="restart-db-instance-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="view-restoration-information"></a>
### 復元情報照会 { #view-restoration-information }

<a id="view-restoration-information-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Get | 復元情報照会 |

<a id="view-restoration-information-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/restoration-info
```

<a id="view-restoration-information-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="view-restoration-information-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-restoration-information-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "oldestRestorableYmdt": "2023-12-31T15:00:00+09:00",
    "latestRestorableYmdt": "2023-12-31T15:00:00+09:00",
    "restorableBackups": [
        {
            "backup": {
                "backupId": "550e8400-e29b-41d4-a716-446655440000",
                "backupName": "backupName-example",
                "backupStatus": "BACKING_UP",
                "dbInstanceId": "550e8400-e29b-41d4-a716-446655440000",
                "dbInstanceName": "dbInstanceName-example",
                "dbVersion": "MARIADB_V11808",
                "backupType": "AUTO",
                "backupSize": 1,
                "useBackupLock": false,
                "failoverCount": 1,
                "binLogFileName": "binLogFileName-example",
                "binLogPosition": 1,
                "createdYmdt": "2023-12-31T15:00:00+09:00",
                "updatedYmdt": "2023-12-31T15:00:00+09:00"
            },
            "restorableBinLogs": []
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| oldestRestorableYmdt | DateTime | 復元可能な最も早い時間 |
| latestRestorableYmdt | DateTime | 復元可能な最も遅い時間 |
| restorableBackups | Array | 復元可能なバックアップリスト |
| restorableBackups.backup | Object | バックアップ情報オブジェクト |
| restorableBackups.backup.backupId | UUID | バックアップの識別子 |
| restorableBackups.backup.backupName | String | バックアップ名 |
| restorableBackups.backup.backupStatus | Enum | バックアップ状態<br/>- `BACKING_UP`:バックアップ中の場合<br/>- `COMPLETED`:バックアップが完了している場合<br/>- `DELETING`:バックアップが削除中の場合<br/>- `DELETED`:バックアップが削除されている場合<br/>- `ERROR`:エラーが発生した場合 |
| restorableBackups.backup.dbInstanceId | UUID | 原本DBインスタンスの識別子 |
| restorableBackups.backup.dbInstanceName | String | 原本DBインスタンスの名前 |
| restorableBackups.backup.dbVersion | Enum | DBエンジンバージョン |
| restorableBackups.backup.backupType | Enum | バックアップタイプ<br/>- `AUTO`<br/>- `MANUAL` |
| restorableBackups.backup.backupSize | Number | バックアップサイズ |
| restorableBackups.backup.useBackupLock | Boolean | テーブルロックを使用するかどうか |
| restorableBackups.backup.failoverCount | Number | フェイルオーバー回数 |
| restorableBackups.backup.binLogFileName | String | バイナリログファイル名 |
| restorableBackups.backup.binLogPosition | Number | バイナリログファイル位置 |
| restorableBackups.backup.createdYmdt | DateTime | バックアップ作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| restorableBackups.backup.updatedYmdt | DateTime | バックアップ更新日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| restorableBackups.restorableBinLogs | Array | 該当バックアップを利用して復元可能なバイナリログ名リスト |

---

<a id="view-the-last-query-to-be-restored"></a>
### 復元される最後のクエリ照会 { #view-the-last-query-to-be-restored }

<a id="view-the-last-query-to-be-restored-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Get | 復元される最後のクエリ照会 |

<a id="view-the-last-query-to-be-restored-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/restoration-info/last-query
```

<a id="view-the-last-query-to-be-restored-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |
| restoreType | Query | Enum | Y | 復元タイプ<br/>- `TIMESTAMP`: 復元可能な時間内の時間を利用した時点復元<br/>- `BINLOG`: 復元可能なバイナリログの位置を利用した時点復元 |

<a id="view-the-last-query-to-be-restored-restoretype-timestamp"></a>
#### restoreTypeが`TIMESTAMP`の場合

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| restoreYmdt | Query | DateTime | Y | DBインスタンス復元日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<a id="view-the-last-query-to-be-restored-restoretype-binlog"></a>
#### restoreTypeが`BINLOG`の場合

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| backupId | Query | UUID | Y | 復元に使用するバックアップの識別子 |
| binLogFileName | Query | String | Y | 復元に使用するバイナリログの名前 |
| binLogPosition | Query | String | Y | 復元に使用するバイナリログの位置 |

<a id="view-the-last-query-to-be-restored-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-the-last-query-to-be-restored-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "executedYmdt": "2023-12-31T15:00:00+09:00",
    "lastQuery": "lastQuery-example"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| executedYmdt | DateTime | クエリ実行日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| lastQuery | String | 最後に実行したクエリ |

---

<a id="restoration"></a>
### 復元 { #restoration }

<a id="restoration-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Restore | 復元 |

<a id="restoration-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/restore
```

<a id="restoration-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="restoration-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "description": "description-example",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "dbPort": 13306,
    "useHighAvailability": false,
    "pingInterval": 3,
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20,
        "storageAutoscale": {
            "useStorageAutoscale": false
        }
    },
    "network": {
        "subnetId": "550e8400-e29b-41d4-a716-446655440000",
        "usePublicAccess": false,
        "availabilityZone": "kr-pub-a"
    },
    "backup": {
        "backupPeriod": 0,
        "ftwrlWaitTimeout": 1800,
        "backupRetryCount": 0,
        "replicationRegion": "KR1",
        "useBackupLock": true,
        "backupSchedules": [
            {
                "backupWndBgnTime": "00:00:00",
                "backupWndDuration": "HALF_AN_HOUR"
            }
        ]
    },
    "restore": {
        "restoreType": "TIMESTAMP"
    },
    "useDefaultNotification": false,
    "useSlowQueryAnalysis": true,
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbSecurityGroupIds": [],
    "userGroupIds": [],
    "useDeletionProtection": false
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Primary DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | DBインスタンスの追加情報<br/>- 最大長さ: `100` |
| dbFlavorId | UUID | N | DBインスタンス仕様の識別子。未入力の場合、原本インスタンスの仕様が適用されます。 |
| dbPort | Number | N | DBポート |
| useHighAvailability | Boolean | N | 高可用性を使用するかどうか<br/>- デフォルト値: `false` |
| pingInterval | Number | N | 高可用性使用時のPing間隔(秒)<br/>- 最小値: `1`<br/>- 最大値: `600` |
| storage | Object | N | ストレージ情報オブジェクト。未入力の場合、原本インスタンスのストレージ設定が適用されます。 |
| storage.storageType | Enum | N | ストレージタイプ。未入力の場合、原本インスタンスのストレージタイプが適用されます。 |
| storage.storageSize | Number | N | データストレージサイズ(GB)。未入力の場合、原本インスタンスのストレージサイズが適用されます。<br/>- 最小値: `20` |
| storage.storageAutoscale | Object | N | データストレージ自動拡張オブジェクト |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | ストレージ自動拡張を行うかどうか<br/>- デフォルト値: `false` |
| network | Object | N | ネットワーク情報オブジェクト。未入力の場合、原本インスタンスのネットワーク設定が適用されます。 |
| network.subnetId | UUID | N | サブネットの識別子。未入力の場合、原本インスタンスの値を使用 |
| network.usePublicAccess | Boolean | N | 外部接続可否<br/>- デフォルト値: `false` |
| network.availabilityZone | Enum | N | DBインスタンスを作成するアベイラビリティゾーン。未入力の場合、ランダムに選択 |
| backup | Object | N | バックアップ情報オブジェクト。未入力の場合、原本インスタンスのバックアップ設定が適用されます。 |
| backup.backupPeriod | Number | N | バックアップ保管期間(日)。未入力の場合、原本インスタンスのバックアップ保管期間が適用されます。<br/>- 最小値: `0`<br/>- 最大値: `730` |
| backup.ftwrlWaitTimeout | Number | N | クエリ遅延待機時間(秒)<br/>- 最小値: `0`<br/>- 最大値: `21600` |
| backup.backupRetryCount | Number | N | バックアップ再試行回数<br/>- 最小値: `0`<br/>- 最大値: `10` |
| backup.replicationRegion | Enum | N | バックアップ複製リージョン<br/>- `KR1`: 韓国(パンギョ) |
| backup.useBackupLock | Boolean | N | テーブルロックを使用するかどうか<br/>- デフォルト値: `true` |
| backup.backupSchedules | Array | N | バックアップスケジュールリスト。未入力の場合、原本インスタンスのバックアップスケジュールが適用されます。 |
| backup.backupSchedules.backupWndBgnTime | Time | N | バックアップ開始時間 |
| backup.backupSchedules.backupWndDuration | Enum | N | バックアップウィンドウ<br/>- `HALF_AN_HOUR`: 30分<br/>- `ONE_HOUR`: 1時間<br/>- `ONE_HOUR_AND_HALF`: 1時間30分<br/>- `TWO_HOURS`: 2時間<br/>- `TWO_HOURS_AND_HALF`: 2時間30分<br/>- `THREE_HOURS`: 3時間 |
| restore | Object | Y | 復元情報オブジェクト |
| restore.restoreType | Enum | Y | 復元タイプ<br/>- `TIMESTAMP`: 復元可能な時間内の時間を利用した時点復元<br/>- `BINLOG`: 復元可能なバイナリログの位置を利用した時点復元<br/>- `BACKUP`: 既に作成したバックアップを利用したスナップショット復元 |
| useDefaultNotification | Boolean | N | 基本通知の使用有無<br/>- デフォルト値: `false` |
| useSlowQueryAnalysis | Boolean | N | Slow query分析を行うかどうか<br/>- デフォルト値: `true` |
| parameterGroupId | UUID | N | パラメータグループの識別子。未入力の場合、原本インスタンスのパラメータグループが適用されます。 |
| dbSecurityGroupIds | Array | N | DBセキュリティグループの識別子リスト。未入力の場合、原本インスタンスのセキュリティグループが適用されます。 |
| userGroupIds | Array | N | ユーザーグループの識別子リスト |
| useDeletionProtection | Boolean | N | 削除保護の有無<br/>- デフォルト値: `false` |

<a id="restoration-section"></a>
#### 高可用性を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Standby DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |

<a id="restoration-section-2"></a>
#### ストレージ自動拡張を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | 自動拡張条件(%)<br/>- 最小値: `50`<br/>- 最大値: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | 自動拡張最大サイズ(GB)<br/>- 最大値: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | 自動拡張クールダウン時間(分)<br/>- 最小値: `10`<br/>- 最大値: `1440` |

<a id="restoration-timestamp-restoretype-timestamp"></a>
#### Timestampを利用した時点復元時、リクエスト(restoreTypeが`TIMESTAMP`の場合)

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| restore.restoreYmdt | DateTime | N | DBインスタンス復元日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

復元情報の照会で確認した復元可能な最も遅い時間より前の時点のみ復元できます。

<a id="restoration-restoretype-binlog"></a>
#### バイナリログを利用した時点復元時、リクエスト(restoreTypeが`BINLOG`の場合)

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| restore.backupId | UUID | N | 復元に使用するバックアップの識別子 |
| restore.binLog | Object | N | 復元に使用するバイナリログ情報オブジェクト |
| restore.binLog.binLogFileName | String | N | 復元に使用するバイナリログの名前 |
| restore.binLog.binLogPosition | Number | N | 復元に使用するバイナリログの位置 |

バイナリログを利用した時点復元時、基準バックアップのバイナリログファイルおよび位置を基準に、それ以降に記録されたログを復元できます。

<a id="restoration-restoretype-backup"></a>
#### バックアップを利用した復元時、リクエスト(restoreTypeが`BACKUP`の場合)

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| restore.backupId | UUID | N | 復元に使用するバックアップの識別子 |

<a id="restoration-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="start-db-instance"></a>
### DBインスタンスを起動する { #start-db-instance }

<a id="start-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Start | DBインスタンスの起動 |

<a id="start-db-instance-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/start
```

<a id="start-db-instance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="start-db-instance-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="start-db-instance-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="stop-db-instance"></a>
### DBインスタンスを停止する { #stop-db-instance }

<a id="stop-db-instance-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Stop | DBインスタンスの停止 |

<a id="stop-db-instance-request"></a>
#### リクエスト

```http
POST /v4.0/db-instances/{dbInstanceId}/stop
```

<a id="stop-db-instance-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="stop-db-instance-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="stop-db-instance-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="view-storage-information"></a>
### ストレージ情報を表示 { #view-storage-information }

<a id="view-storage-information-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Get | ストレージ情報を表示 |

<a id="view-storage-information-request"></a>
#### リクエスト

```http
GET /v4.0/db-instances/{dbInstanceId}/storage-info
```

<a id="view-storage-information-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="view-storage-information-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-storage-information-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "storageType": "General SSD",
    "storageSize": 1,
    "storageStatus": "DELETED",
    "storageAutoscale": {
        "useStorageAutoscale": false,
        "threshold": 1,
        "maxStorageSize": 1,
        "cooldownTime": 1
    }
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| storageType | String | データストレージタイプ |
| storageSize | Number | データストレージサイズ(GB) |
| storageStatus | Enum | データストレージの現在状態<br/>- `DELETED`:削除済み<br/>- `PENDING_DELETION`: 削除猶予済み<br/>- `DELETION_RESERVED`: 削除予約済み(スナップショット整理待機)<br/>- `DETACHED`: 解除済み<br/>- `ATTACHED`: 割り当て済み |
| storageAutoscale | Object | データストレージ自動拡張オブジェクト |
| storageAutoscale.useStorageAutoscale | Boolean | ストレージ自動拡張を行うかどうか |
| storageAutoscale.threshold | Number | 自動拡張条件(%) |
| storageAutoscale.maxStorageSize | Number | 自動拡張最大サイズ(GB) |
| storageAutoscale.cooldownTime | Number | 自動拡張クールダウン時間(分) |

---

<a id="modify-storage-information"></a>
### ストレージ情報を修正する { #modify-storage-information }

<a id="modify-storage-information-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbInstance.Modify | ストレージ情報を修正する |

<a id="modify-storage-information-request"></a>
#### リクエスト

```http
PUT /v4.0/db-instances/{dbInstanceId}/storage-info
```

<a id="modify-storage-information-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DBインスタンスの識別子 |

<a id="modify-storage-information-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "storageSize": 1,
    "storageAutoscale": {
        "useStorageAutoscale": false
    }
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| storageSize | Number | Y | データストレージサイズ(GB)<br/>- 最大値: `2048` |
| storageAutoscale | Object | N | データストレージ自動拡張オブジェクト |
| storageAutoscale.useStorageAutoscale | Boolean | N | ストレージ自動拡張を行うかどうか |

<a id="modify-storage-information-section"></a>
#### ストレージ自動拡張を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| storageAutoscale.threshold | Number | Y | 自動拡張条件(%)<br/>- 最小値: `50`<br/>- 最大値: `95` |
| storageAutoscale.maxStorageSize | Number | Y | 自動拡張最大サイズ(GB)<br/>- 最大値: `4096` |
| storageAutoscale.cooldownTime | Number | Y | 自動拡張クールダウン時間(分)<br/>- 最小値: `10`<br/>- 最大値: `1440` |

<a id="modify-storage-information-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="backups"></a>
## バックアップ { #backups }

<a id="backup-status"></a>
### バックアップ状態 { #backup-status }

| 状態           | 説明           |
|--------------|--------------|
| `BACKING_UP` | バックアップ中の場合     |
| `COMPLETED`  | バックアップが完了している場合   |
| `DELETING`   | バックアップが削除中の場合 |
| `DELETED`    | バックアップが削除されている場合   |
| `ERROR`      | エラーが発生した場合   |

<a id="retrieve-backup-list"></a>
### バックアップリスト照会 { #retrieve-backup-list }

<a id="retrieve-backup-list-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Backup.List | バックアップリスト照会 |

<a id="retrieve-backup-list-request"></a>
#### リクエスト

```http
GET /v4.0/backups
```

<a id="retrieve-backup-list-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| backupType | Query | Enum | N | バックアップタイプ<br/>- `AUTO`<br/>- `MANUAL` |
| dbInstanceId | Query | UUID | N | 原本DBインスタンスの識別子 |
| dbVersion | Query | Enum | N | DBエンジンバージョン |
| page | Query | Number | N | 照会するリストのページ(デフォルト値: 1)<br/>- 最小値: `1` |
| size | Query | Number | N | 照会するリストのページサイズ(デフォルト値: 20)<br/>- 最小値: `1`<br/>- 最大値: `100` |

<a id="retrieve-backup-list-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="retrieve-backup-list-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "totalCounts": 1,
    "backups": [
        {
            "backupId": "550e8400-e29b-41d4-a716-446655440000",
            "backupName": "backupName-example",
            "backupStatus": "BACKING_UP",
            "dbInstanceId": "550e8400-e29b-41d4-a716-446655440000",
            "dbVersion": "MARIADB_V11808",
            "utilVersion": "utilVersion-example",
            "backupType": "AUTO",
            "backupSize": 1,
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| totalCounts | Number | 全バックアップリスト数 |
| backups | Array | バックアップリスト |
| backups.backupId | UUID | バックアップの識別子 |
| backups.backupName | String | バックアップを識別できる名前 |
| backups.backupStatus | Enum | バックアップの現在状態<br/>- `BACKING_UP`:バックアップ中の場合<br/>- `COMPLETED`:バックアップが完了している場合<br/>- `DELETING`:バックアップが削除中の場合<br/>- `DELETED`:バックアップが削除されている場合<br/>- `ERROR`:エラーが発生した場合 |
| backups.dbInstanceId | UUID | 原本DBインスタンスの識別子 |
| backups.dbVersion | Enum | DBエンジンバージョン |
| backups.utilVersion | String | ユーティリティバージョン |
| backups.backupType | Enum | バックアップタイプ<br/>- `AUTO`<br/>- `MANUAL` |
| backups.backupSize | Number | バックアップサイズ(Byte) |
| backups.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| backups.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-backup"></a>
### バックアップの作成 { #create-backup }

<a id="create-backup-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Backup.Create | バックアップの作成 |

<a id="create-backup-request"></a>
#### リクエスト

```http
POST /v4.0/backups
```

<a id="create-backup-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "backupName": "backupName",
    "backupMethodType": "FULL"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| backupName | String | Y | バックアップを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| backupMethodType | Enum | Y | バックアップ方式タイプ<br/>- `FULL`：全体バックアップ<br/>- `INCREMENTAL`：増分バックアップ<br/>- `SNAPSHOT`：スナップショットバックアップ |

<a id="create-backup-backupmethodtype-incremental"></a>
#### 増分バックアップ(backupMethodTypeが`INCREMENTAL`の場合)

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| baseBackupId | UUID | Y | 原本バックアップの識別子 |

<a id="create-backup-backupmethodtype-full"></a>
#### 全体バックアップ(backupMethodTypeが`FULL`の場合)

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceId | UUID | Y | DBインスタンスの識別子 |

<a id="create-backup-backupmethodtype-snapshot"></a>
#### スナップショットバックアップ(backupMethodTypeが`SNAPSHOT`の場合)

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceId | UUID | Y | DBインスタンスの識別子 |

<a id="create-backup-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="delete-backup"></a>
### バックアップを削除する { #delete-backup }

<a id="delete-backup-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Backup.Delete | バックアップの削除 |

<a id="delete-backup-request"></a>
#### リクエスト

```http
DELETE /v4.0/backups/{backupId}
```

<a id="delete-backup-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| backupId | URL | UUID | Y | バックアップの識別子 |

<a id="delete-backup-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-backup-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="view-backup-details"></a>
### バックアップ詳細照会 { #view-backup-details }

<a id="view-backup-details-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Backup.Get | バックアップ詳細照会 |

<a id="view-backup-details-request"></a>
#### リクエスト

```http
GET /v4.0/backups/{backupId}
```

<a id="view-backup-details-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| backupId | URL | UUID | Y | バックアップの識別子 |

<a id="view-backup-details-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-backup-details-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "backup": {
        "backupId": "550e8400-e29b-41d4-a716-446655440000",
        "regionCode": "KR1",
        "backupName": "backupName-example",
        "backupStatus": "BACKING_UP",
        "dbInstanceId": "550e8400-e29b-41d4-a716-446655440000",
        "dbInstanceName": "dbInstanceName-example",
        "dbVersion": "MARIADB_V11808",
        "utilVersion": "utilVersion-example",
        "backupType": "AUTO",
        "backupMethodType": "FULL",
        "backupFileType": "XBSTREAM",
        "backupSize": 1,
        "isReplicable": false,
        "binLogFileName": "binLogFileName-example",
        "binLogPosition": 1,
        "createdYmdt": "2023-12-31T15:00:00+09:00",
        "updatedYmdt": "2023-12-31T15:00:00+09:00"
    }
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| backup | Object | バックアップ詳細情報 |
| backup.backupId | UUID | バックアップの識別子 |
| backup.regionCode | Enum | リージョンコード<br/>- `KR1`: 韓国(パンギョ) |
| backup.backupName | String | バックアップを識別できる名前 |
| backup.backupStatus | Enum | バックアップの現在状態<br/>- `BACKING_UP`: バックアップ中(スピナー)<br/>- `VERIFYING`: 検証中(スピナー)<br/>- `COMPLETED`: 使用可能(緑色アイコン)<br/>- `DELETING`: 削除中(スピナー)<br/>- `DELETED`: 削除済み(グレーアイコン)<br/>- `ERROR`: エラー(赤色アイコン) |
| backup.dbInstanceId | UUID | 原本DBインスタンスの識別子 |
| backup.dbInstanceName | String | 原本DBインスタンスの名前 |
| backup.dbVersion | Enum | DBエンジンバージョン |
| backup.utilVersion | String | ユーティリティバージョン |
| backup.backupType | Enum | バックアップタイプ(AUTO, MANUAL)<br/>- `AUTO`<br/>- `MANUAL` |
| backup.backupMethodType | Enum | バックアップ方式(FULL, SNAPSHOT, INCREMENTAL)<br/>- `FULL`<br/>- `INCREMENTAL`<br/>- `SNAPSHOT` |
| backup.backupFileType | Enum | バックアップファイルタイプ<br/>- `XBSTREAM`<br/>- `TAR_ZSTD`<br/>- `TAR_LZ4`<br/>- `TAR_GZIP`<br/>- `SNAPSHOT` |
| backup.backupSize | Number | バックアップサイズ(Byte) |
| backup.isReplicable | Boolean | レプリケーション可否 |
| backup.binLogFileName | String | バイナリログファイル名 |
| backup.binLogPosition | Number | バイナリログ位置 |
| backup.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| backup.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="export-backup"></a>
### バックアップのエクスポート { #export-backup }

<a id="export-backup-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Backup.Export | バックアップエクスポート |

<a id="export-backup-request"></a>
#### リクエスト

```http
POST /v4.0/backups/{backupId}/export
```

<a id="export-backup-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| backupId | URL | UUID | Y | バックアップの識別子 |

<a id="export-backup-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "tenantId": "0123456789abcdef0123456789abcdef",
    "username": "example@nhncloud.com or example",
    "password": "password-example",
    "targetContainer": "targetContainer-example",
    "objectPath": "objectPath-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| tenantId | String | Y | バックアップが保存されるオブジェクトストレージのテナントID<br/>- 最小長さ: `32`<br/>- 最大長さ: `32` |
| username | String | Y | NHN Cloud会員またはIAMメンバーID |
| password | String | Y | バックアップが保存されるオブジェクトストレージのAPIパスワード |
| targetContainer | String | Y | バックアップが保存されるオブジェクトストレージのコンテナ |
| objectPath | String | Y | コンテナに保存されるバックアップのパス |

<a id="export-backup-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="restore-backup"></a>
### バックアップを復元する { #restore-backup }

<a id="restore-backup-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Backup.Restore | バックアップの復元 |

<a id="restore-backup-request"></a>
#### リクエスト

```http
POST /v4.0/backups/{backupId}/restore
```

<a id="restore-backup-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| backupId | URL | UUID | Y | バックアップの識別子 |

<a id="restore-backup-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "description": "description-example",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "dbPort": 13306,
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbSecurityGroupIds": [],
    "userGroupIds": [],
    "useHighAvailability": false,
    "pingInterval": 3,
    "useDefaultNotification": false,
    "useDeletionProtection": false,
    "useSlowQueryAnalysis": true,
    "network": {
        "subnetId": "550e8400-e29b-41d4-a716-446655440000",
        "usePublicAccess": false,
        "availabilityZone": "kr-pub-a"
    },
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20,
        "storageAutoscale": {
            "useStorageAutoscale": false
        }
    },
    "backup": {
        "backupPeriod": 0,
        "backupRetryCount": 0,
        "ftwrlWaitTimeout": 0,
        "replicationRegion": "KR1",
        "useBackupLock": false,
        "backupSchedules": [
            {
                "backupWndBgnTime": "00:00:00",
                "backupWndDuration": "HALF_AN_HOUR"
            }
        ]
    }
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Primary DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | DBインスタンスの追加情報<br/>- 最大長さ: `100` |
| dbFlavorId | UUID | N | DBインスタンス仕様の識別子。未指定の場合、原本インスタンスの値を使用 |
| dbPort | Number | N | DBポート。未指定の場合、原本インスタンスの値を使用<br/>- 最小値: 3306、最大値: 43306 |
| parameterGroupId | UUID | N | パラメータグループの識別子。未指定の場合、原本インスタンスの値を使用 |
| dbSecurityGroupIds | Array | N | DBセキュリティグループの識別子リスト |
| userGroupIds | Array | N | ユーザーグループの識別子リスト |
| useHighAvailability | Boolean | N | 高可用性を使用するかどうか<br/>- デフォルト値: `false` |
| pingInterval | Number | N | 高可用性使用時のPing間隔(秒)<br/>- デフォルト値: `3`<br/>- 最小値: `1`<br/>- 最大値: `600` |
| useDefaultNotification | Boolean | N | 基本通知の使用有無<br/>- デフォルト値: `false` |
| useDeletionProtection | Boolean | N | 削除保護の有無<br/>- デフォルト値: `false` |
| useSlowQueryAnalysis | Boolean | N | Slow query分析を行うかどうか<br/>- デフォルト値: `true` |
| network | Object | N | ネットワーク情報オブジェクト。未指定の場合、原本インスタンスの値を使用 |
| network.subnetId | UUID | N | サブネットの識別子。未指定の場合、原本インスタンスの値を使用 |
| network.usePublicAccess | Boolean | N | 外部接続可否<br/>- デフォルト値: `false` |
| network.availabilityZone | Enum | N | DBインスタンスを作成するアベイラビリティゾーン。未指定の場合、ランダムに選択 |
| storage | Object | N | ストレージ情報オブジェクト。未指定の場合、原本インスタンスの値を使用 |
| storage.storageType | Enum | N | ストレージタイプ。未指定の場合、原本インスタンスの値を使用 |
| storage.storageSize | Number | N | データストレージサイズ(GB)。未指定の場合、原本インスタンスの値を使用<br/>- 最小値: `20` |
| storage.storageAutoscale | Object | N | データストレージ自動拡張オブジェクト。未指定の場合、原本インスタンスの値を使用 |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | ストレージ自動拡張を行うかどうか<br/>- デフォルト値: `false` |
| backup | Object | N | バックアップ情報オブジェクト。未指定の場合、原本インスタンスのバックアップ設定を使用 |
| backup.backupPeriod | Number | N | バックアップ保管期間(日)。未指定の場合、原本インスタンスの値を使用<br/>- 最小値: `0`<br/>- 最大値: `730` |
| backup.backupRetryCount | Number | N | バックアップ再試行回数。未指定の場合、原本インスタンスの値を使用<br/>- 最小値: `0`<br/>- 最大値: `10` |
| backup.ftwrlWaitTimeout | Number | N | クエリ遅延待機時間(秒)。未指定の場合、原本インスタンスの値を使用<br/>- 最小値: `0`<br/>- 最大値: `21600` |
| backup.replicationRegion | Enum | N | バックアップ複製リージョン<br/>- `KR1`: 韓国(パンギョ) |
| backup.useBackupLock | Boolean | N | テーブルロックを使用するかどうか。未指定の場合、原本インスタンスの値を使用 |
| backup.backupSchedules | Array | N | バックアップスケジュールリスト。未指定の場合、原本インスタンスの値を使用 |
| backup.backupSchedules.backupWndBgnTime | Time | Y | バックアップ開始時間 |
| backup.backupSchedules.backupWndDuration | Enum | Y | バックアップウィンドウ<br/>- `HALF_AN_HOUR`: 30分<br/>- `ONE_HOUR`: 1時間<br/>- `ONE_HOUR_AND_HALF`: 1時間30分<br/>- `TWO_HOURS`: 2時間<br/>- `TWO_HOURS_AND_HALF`: 2時間30分<br/>- `THREE_HOURS`: 3時間 |

<a id="restore-backup-section"></a>
#### 高可用性を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Standby DBインスタンスを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |

<a id="restore-backup-section-2"></a>
#### ストレージ自動拡張を使用する場合

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | 自動拡張条件(%)<br/>- 最小値: `50`<br/>- 最大値: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | 自動拡張最大サイズ(GB)<br/>- 最大値: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | 自動拡張クールダウン時間(分)<br/>- 最小値: `10`<br/>- 最大値: `1440` |

<a id="restore-backup-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | リクエストした作業の識別子 |

---

<a id="db-security-group"></a>
## DBセキュリティグループ { #db-security-group }

<a id="db-security-group-progress-status"></a>
### DBセキュリティグループ進行状態 { #db-security-group-progress-status }

| 状態              | 説明           |
|-----------------|--------------|
| `NONE`          | 進行中の作業がない |
| `CREATING_RULE` | ルールポリシーの作成中   |
| `UPDATING_RULE` | ルールポリシーの修正中   |
| `DELETING_RULE` | ルールポリシーの削除中   |

<a id="list-db-security-groups"></a>
### DBセキュリティグループリストを表示 { #list-db-security-groups }

<a id="list-db-security-groups-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbSecurityGroup.List | DBセキュリティグループリスト表示 |

<a id="list-db-security-groups-request"></a>
#### リクエスト

```http
GET /v4.0/db-security-groups
```

<a id="list-db-security-groups-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| page | Query | Number | N | 照会するリストのページ(デフォルト値: 1)<br/>- 最小値: `1` |
| size | Query | Number | N | 照会するリストのページサイズ(デフォルト値: 20)<br/>- 最小値: `1`<br/>- 最大値: `100` |

<a id="list-db-security-groups-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-security-groups-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "totalCounts": 1,
    "dbSecurityGroups": [
        {
            "dbSecurityGroupId": "550e8400-e29b-41d4-a716-446655440000",
            "dbSecurityGroupName": "dbSecurityGroupName-example",
            "description": "description-example",
            "progressStatus": "NONE",
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| totalCounts | Number | DBセキュリティグループリストの総数 |
| dbSecurityGroups | Array | DBセキュリティグループリスト |
| dbSecurityGroups.dbSecurityGroupId | UUID | DBセキュリティグループの識別子 |
| dbSecurityGroups.dbSecurityGroupName | String | DBセキュリティグループを識別できる名前 |
| dbSecurityGroups.description | String | DBセキュリティグループの追加情報 |
| dbSecurityGroups.progressStatus | Enum | DBセキュリティグループの現在進行状態<br/>- `NONE`: なし<br/>- `CREATING_RULE`: ルール作成中<br/>- `UPDATING_RULE`: ルール修正中<br/>- `DELETING_RULE`: ルール削除中<br/>- `APPLYING_DEFAULT_RULE`: 基本ルール適用中 |
| dbSecurityGroups.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbSecurityGroups.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-db-security-group"></a>
### DBセキュリティグループを作成する { #create-db-security-group }

<a id="create-db-security-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbSecurityGroup.Create | DBセキュリティグループの作成 |

<a id="create-db-security-group-request"></a>
#### リクエスト

```http
POST /v4.0/db-security-groups
```

<a id="create-db-security-group-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbSecurityGroupName": "dbSecurityGroupName",
    "description": "description-example",
    "rules": [
        {
            "direction": "INGRESS",
            "etherType": "IPV4",
            "port": {
                "portType": "ALL",
                "minPort": 3306,
                "maxPort": 1
            },
            "cidr": "192.168.0.0/24",
            "description": "description-example"
        }
    ]
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbSecurityGroupName | String | Y | DBセキュリティグループを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | DBセキュリティグループの追加情報<br/>- 最大長さ: `100` |
| rules | Array | Y | DBセキュリティグループルールリスト |
| rules.direction | Enum | Y | 通信方向<br/>- `INGRESS`:受信<br/>- `EGRESS`:送信 |
| rules.etherType | Enum | Y | Etherタイプ<br/>- `IPV4`: IPv4形式<br/>- `IPV6`: IPv6形式 |
| rules.port | Object | Y | ポートオブジェクト |
| rules.port.portType | Enum | Y | ポートタイプ<br/>- `ALL`: ポート範囲全体(ユーザーコンソールでは使用しません)<br/>- `PORT`: 特定ポート<br/>- `DB_PORT`: DB受信ポート<br/>- `PORT_RANGE`: ポート範囲 |
| rules.port.minPort | Number | N | ポート範囲の最小値<br/>- 最小値: `3306` |
| rules.port.maxPort | Number | N | ポート範囲の最大値<br/>- 最大値: `65535` |
| rules.cidr | String | Y | CIDR |
| rules.description | String | N | セキュリティグループルールの追加情報 |

<a id="create-db-security-group-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbSecurityGroupId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbSecurityGroupId | UUID | DBセキュリティグループの識別子 |

---

<a id="delete-db-security-group"></a>
### DBセキュリティグループを削除する { #delete-db-security-group }

<a id="delete-db-security-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbSecurityGroup.Delete | DBセキュリティグループの削除 |

<a id="delete-db-security-group-request"></a>
#### リクエスト

```http
DELETE /v4.0/db-security-groups/{dbSecurityGroupId}
```

<a id="delete-db-security-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DBセキュリティグループの識別子 |

<a id="delete-db-security-group-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-db-security-group-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="list-db-security-group-details"></a>
### DBセキュリティグループの詳細を表示 { #list-db-security-group-details }

<a id="list-db-security-group-details-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbSecurityGroup.Get | DBセキュリティグループの詳細を表示 |

<a id="list-db-security-group-details-request"></a>
#### リクエスト

```http
GET /v4.0/db-security-groups/{dbSecurityGroupId}
```

<a id="list-db-security-group-details-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DBセキュリティグループの識別子 |

<a id="list-db-security-group-details-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-db-security-group-details-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbSecurityGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbSecurityGroupName": "dbSecurityGroupName-example",
    "description": "description-example",
    "progressStatus": "NONE",
    "rules": [
        {
            "ruleId": "550e8400-e29b-41d4-a716-446655440000",
            "description": "description-example",
            "direction": "INGRESS",
            "etherType": "IPV4",
            "port": {
                "portType": "ALL",
                "minPort": 1,
                "maxPort": 1
            },
            "cidr": "192.168.0.0/24",
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00"
        }
    ],
    "createdYmdt": "2023-12-31T15:00:00+09:00",
    "updatedYmdt": "2023-12-31T15:00:00+09:00"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| dbSecurityGroupId | UUID | DBセキュリティグループの識別子 |
| dbSecurityGroupName | String | DBセキュリティグループを識別できる名前 |
| description | String | DBセキュリティグループの追加情報 |
| progressStatus | Enum | DBセキュリティグループの現在進行状態<br/>- `NONE`: なし<br/>- `CREATING_RULE`: ルール作成中<br/>- `UPDATING_RULE`: ルール修正中<br/>- `DELETING_RULE`: ルール削除中<br/>- `APPLYING_DEFAULT_RULE`: 基本ルール適用中 |
| rules | Array | DBセキュリティグループルールリスト |
| rules.ruleId | UUID | DBセキュリティグループルールの識別子 |
| rules.description | String | DBセキュリティグループルールの追加情報 |
| rules.direction | Enum | 通信方向<br/>- `INGRESS`:受信<br/>- `EGRESS`:送信 |
| rules.etherType | Enum | Etherタイプ<br/>- `IPV4`: IPv4形式<br/>- `IPV6`: IPv6形式 |
| rules.port | Object | ポートオブジェクト |
| rules.port.portType | Enum | ポートタイプ<br/>- `ALL`: ポート範囲全体(ユーザーコンソールでは使用しません)<br/>- `PORT`: 特定ポート<br/>- `DB_PORT`: DB受信ポート<br/>- `PORT_RANGE`: ポート範囲 |
| rules.port.minPort | Number | ポート範囲の最小値 |
| rules.port.maxPort | Number | ポート範囲の最大値 |
| rules.cidr | String | CIDR |
| rules.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| rules.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-db-security-group"></a>
### DBセキュリティグループを修正する { #modify-db-security-group }

<a id="modify-db-security-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbSecurityGroup.Modify | DBセキュリティグループの修正 |

<a id="modify-db-security-group-request"></a>
#### リクエスト

```http
PUT /v4.0/db-security-groups/{dbSecurityGroupId}
```

<a id="modify-db-security-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DBセキュリティグループの識別子 |

<a id="modify-db-security-group-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "dbSecurityGroupName": "dbSecurityGroupName",
    "description": "description-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| dbSecurityGroupName | String | N | DBセキュリティグループを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | DBセキュリティグループの追加情報<br/>- 最大長さ: `100` |

<a id="modify-db-security-group-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="delete-db-security-group-rule"></a>
### DBセキュリティグループルールを削除する { #delete-db-security-group-rule }

<a id="delete-db-security-group-rule-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbSecurityGroupRule.Delete | DBセキュリティグループルールの削除 |

<a id="delete-db-security-group-rule-request"></a>
#### リクエスト

```http
DELETE /v4.0/db-security-groups/{dbSecurityGroupId}/rules
```

<a id="delete-db-security-group-rule-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DBセキュリティグループの識別子 |
| ruleIds | Query | String | Y | DBセキュリティグループルールの識別子リスト |

<a id="delete-db-security-group-rule-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-db-security-group-rule-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | 作業の識別子 |

---

<a id="create-db-security-group-rule"></a>
### DBセキュリティグループルールを作成する { #create-db-security-group-rule }

<a id="create-db-security-group-rule-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbSecurityGroupRule.Create | DBセキュリティグループルールの作成 |

<a id="create-db-security-group-rule-request"></a>
#### リクエスト

```http
POST /v4.0/db-security-groups/{dbSecurityGroupId}/rules
```

<a id="create-db-security-group-rule-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DBセキュリティグループの識別子 |

<a id="create-db-security-group-rule-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "direction": "INGRESS",
    "etherType": "IPV4",
    "port": {
        "portType": "ALL",
        "minPort": 3306,
        "maxPort": 1
    },
    "cidr": "192.168.0.0/24",
    "description": "description-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| direction | Enum | Y | 通信方向<br/>- `INGRESS`:受信<br/>- `EGRESS`:送信 |
| etherType | Enum | Y | Etherタイプ<br/>- `IPV4`: IPv4形式<br/>- `IPV6`: IPv6形式 |
| port | Object | Y | ポートオブジェクト |
| port.portType | Enum | Y | ポートタイプ<br/>- `ALL`: ポート範囲全体(ユーザーコンソールでは使用しません)<br/>- `PORT`: 特定ポート<br/>- `DB_PORT`: DB受信ポート<br/>- `PORT_RANGE`: ポート範囲 |
| port.minPort | Number | N | ポート範囲の最小値<br/>- 最小値: `3306` |
| port.maxPort | Number | N | ポート範囲の最大値<br/>- 最大値: `65535` |
| cidr | String | Y | CIDR |
| description | String | N | DBセキュリティグループルールの追加情報<br/>- 最大長さ: `200` |

<a id="create-db-security-group-rule-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | 作業の識別子 |

---

<a id="modify-db-security-group-rule"></a>
### DBセキュリティグループルールを修正する { #modify-db-security-group-rule }

<a id="modify-db-security-group-rule-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:DbSecurityGroupRule.Modify | DBセキュリティグループルールの修正 |

<a id="modify-db-security-group-rule-request"></a>
#### リクエスト

```http
PUT /v4.0/db-security-groups/{dbSecurityGroupId}/rules/{ruleId}
```

<a id="modify-db-security-group-rule-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DBセキュリティグループの識別子 |
| ruleId | URL | UUID | Y | DBセキュリティグループルールの識別子 |

<a id="modify-db-security-group-rule-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "direction": "INGRESS",
    "etherType": "IPV4",
    "port": {
        "portType": "ALL",
        "minPort": 3306,
        "maxPort": 1
    },
    "cidr": "192.168.0.0/24",
    "description": "description-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| direction | Enum | Y | 通信方向<br/>- `INGRESS`:受信<br/>- `EGRESS`:送信 |
| etherType | Enum | Y | Etherタイプ<br/>- `IPV4`: IPv4形式<br/>- `IPV6`: IPv6形式 |
| port | Object | Y | ポートオブジェクト |
| port.portType | Enum | Y | ポートタイプ<br/>- `ALL`: ポート範囲全体(ユーザーコンソールでは使用しません)<br/>- `PORT`: 特定ポート<br/>- `DB_PORT`: DB受信ポート<br/>- `PORT_RANGE`: ポート範囲 |
| port.minPort | Number | N | ポート範囲の最小値<br/>- 最小値: `3306` |
| port.maxPort | Number | N | ポート範囲の最大値<br/>- 最大値: `65535` |
| cidr | String | Y | CIDR |
| description | String | N | DBセキュリティグループルールの追加情報<br/>- 最大長さ: `200` |

<a id="modify-db-security-group-rule-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| jobId | UUID | 作業の識別子 |

---

<a id="parameter-group"></a>
## パラメータグループ { #parameter-group }

<a id="list-parameter-groups"></a>
### パラメータグループリストを表示 { #list-parameter-groups }

<a id="list-parameter-groups-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:ParameterGroup.List | パラメータグループリスト表示 |

<a id="list-parameter-groups-request"></a>
#### リクエスト

```http
GET /v4.0/parameter-groups
```

<a id="list-parameter-groups-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| parameterGroupName | Query | String | N | パラメータグループ名(部分検索) |
| dbVersion | Query | Enum | N | DBエンジンバージョン |
| page | Query | Number | N | 照会するリストのページ(デフォルト値: 1)<br/>- 最小値: `1` |
| size | Query | Number | N | 照会するリストのページサイズ(デフォルト値: 20)<br/>- 最小値: `1`<br/>- 最大値: `100` |

<a id="list-parameter-groups-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-parameter-groups-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "totalCounts": 1,
    "parameterGroups": [
        {
            "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
            "parameterGroupName": "parameterGroupName-example",
            "description": "description-example",
            "dbVersion": "MARIADB_V11808",
            "parameterGroupType": "USER",
            "parameterGroupStatus": "STABLE",
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| totalCounts | Number | パラメータグループの総数 |
| parameterGroups | Array | パラメータグループリスト |
| parameterGroups.parameterGroupId | UUID | パラメータグループの識別子 |
| parameterGroups.parameterGroupName | String | パラメータグループを識別できる名前 |
| parameterGroups.description | String | パラメータグループの追加情報 |
| parameterGroups.dbVersion | Enum | DBエンジンバージョン |
| parameterGroups.parameterGroupType | Enum | パラメータグループタイプ<br/>- `USER`<br/>- `ADMIN`<br/>- `DEFAULT` |
| parameterGroups.parameterGroupStatus | Enum | パラメータグループの現在状態<br/>- `STABLE`:適用完了<br/>- `NEED_TO_APPLY`:適用必要<br/>- `DELETED`:削除済み |
| parameterGroups.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| parameterGroups.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-parameter-group"></a>
### パラメータグループを作成する { #create-parameter-group }

<a id="create-parameter-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:ParameterGroup.Create | パラメータグループの作成 |

<a id="create-parameter-group-request"></a>
#### リクエスト

```http
POST /v4.0/parameter-groups
```

<a id="create-parameter-group-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "parameterGroupName": "parameterGroupName",
    "description": "description-example",
    "dbVersion": "MARIADB_V11808"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| parameterGroupName | String | Y | パラメータグループを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | パラメータグループの追加情報<br/>- 最大長さ: `100` |
| dbVersion | Enum | Y | DBエンジンバージョン |

<a id="create-parameter-group-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| parameterGroupId | UUID | パラメータグループの識別子 |

---

<a id="delete-parameter-group"></a>
### パラメータグループを削除する { #delete-parameter-group }

<a id="delete-parameter-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:ParameterGroup.Delete | パラメータグループの削除 |

<a id="delete-parameter-group-request"></a>
#### リクエスト

```http
DELETE /v4.0/parameter-groups/{parameterGroupId}
```

<a id="delete-parameter-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | パラメータグループの識別子 |

<a id="delete-parameter-group-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-parameter-group-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="list-parameter-group-details"></a>
### パラメータグループの詳細を表示 { #list-parameter-group-details }

<a id="list-parameter-group-details-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:ParameterGroup.Get | パラメータグループ詳細表示 |

<a id="list-parameter-group-details-request"></a>
#### リクエスト

```http
GET /v4.0/parameter-groups/{parameterGroupId}
```

<a id="list-parameter-group-details-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | パラメータグループの識別子 |

<a id="list-parameter-group-details-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-parameter-group-details-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "parameterGroupName": "parameterGroupName-example",
    "description": "description-example",
    "dbVersion": "MARIADB_V11808",
    "parameterGroupStatus": "STABLE",
    "parameters": [
        {
            "parameterId": "550e8400-e29b-41d4-a716-446655440000",
            "parameterFileGroup": "CLIENT",
            "parameterName": "parameterName-example",
            "fileParameterName": "fileParameterName-example",
            "value": "value-example",
            "defaultValue": "defaultValue-example",
            "allowedValue": "allowedValue-example",
            "updateType": "VARIABLE",
            "applyType": "BOTH"
        }
    ],
    "createdYmdt": "2023-12-31T15:00:00+09:00",
    "updatedYmdt": "2023-12-31T15:00:00+09:00"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| parameterGroupId | UUID | パラメータグループの識別子 |
| parameterGroupName | String | パラメータグループを識別できる名前 |
| description | String | パラメータグループの追加情報 |
| dbVersion | Enum | DBエンジンバージョン |
| parameterGroupStatus | Enum | パラメータグループの現在状態<br/>- `STABLE`:適用完了<br/>- `NEED_TO_APPLY`:適用必要<br/>- `DELETED`:削除済み |
| parameters | Array | パラメータリスト |
| parameters.parameterId | UUID | パラメータの識別子 |
| parameters.parameterFileGroup | Enum | パラメータファイルグループタイプ<br/>- `CLIENT`<br/>- `MYSQL`<br/>- `MYSQLD` |
| parameters.parameterName | String | パラメータ名 |
| parameters.fileParameterName | String | パラメータファイル名 |
| parameters.value | String | 現在設定されている値 |
| parameters.defaultValue | String | デフォルト値 |
| parameters.allowedValue | String | 許可された値 |
| parameters.updateType | Enum | 修正タイプ<br/>- `VARIABLE`<br/>- `CONSTANT`<br/>- `INIT_VARIABLE` |
| parameters.applyType | Enum | 適用タイプ<br/>- `BOTH`<br/>- `SESSION`<br/>- `FILE` |
| createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-parameter-group"></a>
### パラメータグループを修正する { #modify-parameter-group }

<a id="modify-parameter-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:ParameterGroup.Modify | パラメータグループの修正 |

<a id="modify-parameter-group-request"></a>
#### リクエスト

```http
PUT /v4.0/parameter-groups/{parameterGroupId}
```

<a id="modify-parameter-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | パラメータグループの識別子 |

<a id="modify-parameter-group-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "parameterGroupName": "parameterGroupName",
    "description": "description-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| parameterGroupName | String | N | パラメータグループを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | パラメータグループの追加情報<br/>- 最大長さ: `100` |

<a id="modify-parameter-group-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="copy-parameter-group"></a>
### パラメータグループをコピーする { #copy-parameter-group }

<a id="copy-parameter-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:ParameterGroup.Copy | パラメータグループのコピー |

<a id="copy-parameter-group-request"></a>
#### リクエスト

```http
POST /v4.0/parameter-groups/{parameterGroupId}/copy
```

<a id="copy-parameter-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | パラメータグループの識別子 |

<a id="copy-parameter-group-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "parameterGroupName": "parameterGroupName",
    "description": "description-example"
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| parameterGroupName | String | Y | パラメータグループを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| description | String | N | パラメータグループの追加情報<br/>- 最大長さ: `100` |

<a id="copy-parameter-group-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| parameterGroupId | UUID | パラメータグループの識別子 |

---

<a id="modify-parameter"></a>
### パラメータを修正する { #modify-parameter }

<a id="modify-parameter-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:ParameterGroup.Modify | パラメータを修正する |

<a id="modify-parameter-request"></a>
#### リクエスト

```http
PUT /v4.0/parameter-groups/{parameterGroupId}/parameters
```

<a id="modify-parameter-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | パラメータグループの識別子 |

<a id="modify-parameter-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "modifiedParameters": [
        {
            "parameterId": "550e8400-e29b-41d4-a716-446655440000",
            "value": "value-example"
        }
    ]
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| modifiedParameters | Array | Y | 変更するパラメータリスト |
| modifiedParameters.parameterId | UUID | Y | パラメータの識別子 |
| modifiedParameters.value | String | Y | 変更するパラメータ値 |

<a id="modify-parameter-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="reset-parameter-group"></a>
### パラメータグループをリセットする { #reset-parameter-group }

<a id="reset-parameter-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:ParameterGroup.Reset | パラメータグループのリセット |

<a id="reset-parameter-group-request"></a>
#### リクエスト

```http
PUT /v4.0/parameter-groups/{parameterGroupId}/reset
```

<a id="reset-parameter-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | パラメータグループの識別子 |

<a id="reset-parameter-group-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="reset-parameter-group-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="user-group"></a>
## ユーザーグループ { #user-group }

<a id="list-user-groups"></a>
### ユーザーグループリストを表示 { #list-user-groups }

<a id="list-user-groups-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:UserGroup.List | ユーザーグループリスト表示 |

<a id="list-user-groups-request"></a>
#### リクエスト

```http
GET /v4.0/user-groups
```

<a id="list-user-groups-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| page | Query | Number | N | 照会するリストのページ(デフォルト値: 1)<br/>- 最小値: `1` |
| size | Query | Number | N | 照会するリストのページサイズ(デフォルト値: 20)<br/>- 最小値: `1`<br/>- 最大値: `100` |

<a id="list-user-groups-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-user-groups-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "totalCounts": 1,
    "userGroups": [
        {
            "userGroupId": "550e8400-e29b-41d4-a716-446655440000",
            "userGroupName": "userGroupName-example",
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| totalCounts | Number | ユーザーグループリストの総数 |
| userGroups | Array | ユーザーグループリスト |
| userGroups.userGroupId | UUID | ユーザーグループの識別子 |
| userGroups.userGroupName | String | ユーザーグループを識別できる名前 |
| userGroups.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| userGroups.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-user-group"></a>
### ユーザーグループを作成する { #create-user-group }

<a id="create-user-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:UserGroup.Create | ユーザーグループの作成 |

<a id="create-user-group-request"></a>
#### リクエスト

```http
POST /v4.0/user-groups
```

<a id="create-user-group-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "userGroupName": "userGroupName-example",
    "memberIds": [],
    "selectAll": false
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| userGroupName | String | Y | ユーザーグループを識別できる名前 |
| memberIds | Array | Y | プロジェクトメンバーの識別子リスト |
| selectAll | Boolean | N | プロジェクトメンバー全体を含めるかどうか<br/>- デフォルト値: `false` |

<a id="create-user-group-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "userGroupId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| userGroupId | UUID | ユーザーグループの識別子 |

---

<a id="delete-user-group"></a>
### ユーザーグループを削除する { #delete-user-group }

<a id="delete-user-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:UserGroup.Delete | ユーザーグループの削除 |

<a id="delete-user-group-request"></a>
#### リクエスト

```http
DELETE /v4.0/user-groups/{userGroupId}
```

<a id="delete-user-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| userGroupId | URL | UUID | Y | ユーザーグループの識別子 |

<a id="delete-user-group-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-user-group-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="list-user-group-details"></a>
### ユーザーグループの詳細を表示 { #list-user-group-details }

<a id="list-user-group-details-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:UserGroup.Get | ユーザーグループ詳細表示 |

<a id="list-user-group-details-request"></a>
#### リクエスト

```http
GET /v4.0/user-groups/{userGroupId}
```

<a id="list-user-group-details-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| userGroupId | URL | UUID | Y | ユーザーグループの識別子 |

<a id="list-user-group-details-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-user-group-details-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "userGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "userGroupName": "userGroupName-example",
    "userGroupTypeCode": "ENTIRE",
    "members": [
        {
            "memberId": "550e8400-e29b-41d4-a716-446655440000"
        }
    ],
    "createdYmdt": "2023-12-31T15:00:00+09:00",
    "updatedYmdt": "2023-12-31T15:00:00+09:00"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| userGroupId | UUID | ユーザーグループの識別子 |
| userGroupName | String | ユーザーグループを識別できる名前 |
| userGroupTypeCode | Enum | ユーザーグループタイプ<br/>- `ENTIRE`<br/>- `INDIVIDUAL_MEMBER` |
| members | Array | プロジェクトメンバーリスト |
| members.memberId | UUID | プロジェクトメンバーの識別子 |
| createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-user-group"></a>
### ユーザーグループを修正する { #modify-user-group }

<a id="modify-user-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:UserGroup.Modify | ユーザーグループの修正 |

<a id="modify-user-group-request"></a>
#### リクエスト

```http
PUT /v4.0/user-groups/{userGroupId}
```

<a id="modify-user-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| userGroupId | URL | UUID | Y | ユーザーグループの識別子 |

<a id="modify-user-group-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "userGroupName": "userGroupName-example",
    "memberIds": [],
    "selectAll": false
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| userGroupName | String | Y | ユーザーグループを識別できる名前 |
| memberIds | Array | N | プロジェクトメンバーの識別子リスト |
| selectAll | Boolean | N | プロジェクトメンバー全体を含めるかどうか<br/>- デフォルト値: `false` |

<a id="modify-user-group-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="notification-group"></a>
## 通知グループ { #notification-group }

<a id="list-notification-groups"></a>
### 通知グループリストを表示 { #list-notification-groups }

<a id="list-notification-groups-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:NotificationGroup.List | 通知グループリスト表示 |

<a id="list-notification-groups-request"></a>
#### リクエスト

```http
GET /v4.0/notification-groups
```

<a id="list-notification-groups-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-notification-groups-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "notificationGroups": [
        {
            "notificationGroupId": "550e8400-e29b-41d4-a716-446655440000",
            "notificationGroupName": "notificationGroupName-example",
            "notifyEmail": false,
            "notifySms": false,
            "isEnabled": false,
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| notificationGroups | Array | 通知グループリスト |
| notificationGroups.notificationGroupId | UUID | 通知グループの識別子 |
| notificationGroups.notificationGroupName | String | 通知グループを識別できる名前 |
| notificationGroups.notifyEmail | Boolean | メール通知 |
| notificationGroups.notifySms | Boolean | SMS通知 |
| notificationGroups.isEnabled | Boolean | 有効かどうか |
| notificationGroups.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| notificationGroups.updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-notification-group"></a>
### 通知グループを作成する { #create-notification-group }

<a id="create-notification-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:NotificationGroup.Create | 通知グループの作成 |

<a id="create-notification-group-request"></a>
#### リクエスト

```http
POST /v4.0/notification-groups
```

<a id="create-notification-group-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "notificationGroupName": "notificationGroupName",
    "notifyEmail": true,
    "notifySms": true,
    "isEnabled": true,
    "dbInstanceIds": [],
    "userGroupIds": []
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| notificationGroupName | String | Y | 通知グループを識別できる名前<br/>- 最小長さ: `1`<br/>- 最大長さ: `100` |
| notifyEmail | Boolean | N | メール通知<br/>- デフォルト値: `true` |
| notifySms | Boolean | N | SMS通知<br/>- デフォルト値: `true` |
| isEnabled | Boolean | N | 有効かどうか<br/>- デフォルト値: `true` |
| dbInstanceIds | Array | Y | 監視対象DBインスタンスの識別子リスト |
| userGroupIds | Array | Y | ユーザーグループの識別子リスト |

<a id="create-notification-group-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "notificationGroupId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| notificationGroupId | UUID | 通知グループの識別子 |

---

<a id="delete-notification-group"></a>
### 通知グループを削除する { #delete-notification-group }

<a id="delete-notification-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:NotificationGroup.Delete | 通知グループの削除 |

<a id="delete-notification-group-request"></a>
#### リクエスト

```http
DELETE /v4.0/notification-groups/{notificationGroupId}
```

<a id="delete-notification-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| notificationGroupId | URL | UUID | Y | 通知グループの識別子 |

<a id="delete-notification-group-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-notification-group-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="view-notification-group-details"></a>
### 通知グループの詳細を表示 { #view-notification-group-details }

<a id="view-notification-group-details-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:NotificationGroup.Get | 通知グループ詳細表示 |

<a id="view-notification-group-details-request"></a>
#### リクエスト

```http
GET /v4.0/notification-groups/{notificationGroupId}
```

<a id="view-notification-group-details-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| notificationGroupId | URL | UUID | Y | 通知グループの識別子 |

<a id="view-notification-group-details-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-notification-group-details-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "notificationGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "notificationGroupName": "notificationGroupName-example",
    "notifyEmail": false,
    "notifySms": false,
    "isEnabled": false,
    "dbInstances": [
        {
            "dbInstanceId": "550e8400-e29b-41d4-a716-446655440000",
            "dbInstanceName": "dbInstanceName-example"
        }
    ],
    "userGroups": [
        {
            "userGroupId": "550e8400-e29b-41d4-a716-446655440000",
            "userGroupName": "userGroupName-example"
        }
    ],
    "createdYmdt": "2023-12-31T15:00:00+09:00",
    "updatedYmdt": "2023-12-31T15:00:00+09:00"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| notificationGroupId | UUID | 通知グループの識別子 |
| notificationGroupName | String | 通知グループを識別できる名前 |
| notifyEmail | Boolean | メール通知 |
| notifySms | Boolean | SMS通知 |
| isEnabled | Boolean | 有効かどうか |
| dbInstances | Array | 監視対象DBインスタンスリスト |
| dbInstances.dbInstanceId | UUID | DBインスタンスの識別子 |
| dbInstances.dbInstanceName | String | Primary DBインスタンスを識別できる名前 |
| userGroups | Array | ユーザーグループリスト |
| userGroups.userGroupId | UUID | ユーザーグループの識別子 |
| userGroups.userGroupName | String | ユーザーグループを識別できる名前 |
| createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | 修正日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-notification-group"></a>
### 通知グループを修正する { #modify-notification-group }

<a id="modify-notification-group-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:NotificationGroup.Modify | 通知グループの修正 |

<a id="modify-notification-group-request"></a>
#### リクエスト

```http
PUT /v4.0/notification-groups/{notificationGroupId}
```

<a id="modify-notification-group-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| notificationGroupId | URL | UUID | Y | 通知グループの識別子 |

<a id="modify-notification-group-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "notificationGroupName": "notificationGroupName-example",
    "notifyEmail": false,
    "notifySms": false,
    "isEnabled": false,
    "dbInstanceIds": [],
    "userGroupIds": []
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| notificationGroupName | String | N | 通知グループを識別できる名前 |
| notifyEmail | Boolean | N | メール通知<br/>- デフォルト値: `false` |
| notifySms | Boolean | N | SMS通知<br/>- デフォルト値: `false` |
| isEnabled | Boolean | N | 有効かどうか<br/>- デフォルト値: `false` |
| dbInstanceIds | Array | N | 監視対象DBインスタンスの識別子リスト |
| userGroupIds | Array | N | ユーザーグループの識別子リスト |

<a id="modify-notification-group-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="monitoring"></a>
## モニタリング { #monitoring }

<a id="view-stats"></a>
### 統計情報照会 { #view-stats }

<a id="view-stats-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Metric.List | 統計情報照会 |

<a id="view-stats-request"></a>
#### リクエスト

```http
GET /v4.0/metric-statistics
```

<a id="view-stats-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| dbInstanceId | Query | UUID | Y | DBインスタンスの識別子 |
| measureNames | Query | Array | Y | 照会するパフォーマンス指標リスト |
| from | Query | DateTime | Y | 開始日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| to | Query | DateTime | Y | 終了日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| interval | Query | Number | N | 照会間隔<br/>- 単位: `分`<br/>- デフォルト値: 開始/終了日時に応じて適切な値が自動的に選択されます |

<a id="view-stats-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="view-stats-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "metricStatistics": [
        {
            "measureName": "CPU_USAGE",
            "unit": "%",
            "values": [
                [
                    1679298540,
                    "7.5%"
                ]
            ]
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| metricStatistics | Array | 統計情報リスト |
| metricStatistics.measureName | Enum | 測定項目タイプ |
| metricStatistics.unit | String | 測定値の単位 |
| metricStatistics.values | Array | 測定値リスト |
| metricStatistics.values.timestamp | Timestamp | 測定時間 |
| metricStatistics.values.value | String | 測定値 |

---

<a id="list-metric-list"></a>
### Metricリスト表示 { #list-metric-list }

<a id="list-metric-list-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Metric.List | Metricリスト表示 |

<a id="list-metric-list-request"></a>
#### リクエスト

```http
GET /v4.0/metrics
```

<a id="list-metric-list-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-metric-list-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "metrics": [
        {
            "measureName": "CPU_USAGE",
            "unit": "%"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| metrics | Array | Metricリスト |
| metrics.measureName | Enum | 照会指標タイプ |
| metrics.unit | String | 測定値の単位 |

---

<a id="event"></a>
## イベント { #event }

<a id="event-category"></a>
### イベントカテゴリー { #event-category }

イベントはカテゴリに分類することができ、下記の通りです。

| イベントカテゴリー    | 説明      |
|-------------|---------|
| ALL         | 全体      |
| BACKUP      | バックアップ      |
| DB_INSTANCE | DBインスタンス |
| JOB         | 作業      |
| TENANT      | テナント     |
| MONITORING  | モニタリング    |

<a id="list-subscribable-event-codes"></a>
### 購読可能なイベントコード一覧表示 { #list-subscribable-event-codes }

<a id="list-subscribable-event-codes-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Event.List | 購読可能なイベントコード一覧表示 |

<a id="list-subscribable-event-codes-request"></a>
#### リクエスト

```http
GET /v4.0/event-codes
```

<a id="list-subscribable-event-codes-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-subscribable-event-codes-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "eventCodes": [
        {
            "eventCode": "INSTC_02_01",
            "eventCategoryType": "ALL"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| eventCodes | Array | イベントコードリスト |
| eventCodes.eventCode | Enum | イベントコード |
| eventCodes.eventCategoryType | Enum | イベントカテゴリータイプ<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |

---

<a id="list-events"></a>
### イベントリスト照会 { #list-events }

<a id="list-events-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:Event.List | イベントリスト照会 |

<a id="list-events-request"></a>
#### リクエスト

```http
GET /v4.0/events
```

<a id="list-events-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| from | Query | DateTime | Y | 開始日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| to | Query | DateTime | Y | 終了日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| eventCategoryType | Query | Enum | Y | 照会するイベントカテゴリータイプ<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| sourceId | Query | UUID | N | イベントが発生した対象リソースの識別子 |
| keyword | Query | String | N | イベントメッセージに含まれる文字列検索ワード |
| ascendingOrder | Query | Enum | N | イベントメッセージソート順序<br/>- デフォルト値: `DESC`<br/>- `ASC`<br/>- `DESC` |
| page | Query | Number | N | 照会するリストのページ(デフォルト値: 1)<br/>- 最小値: `1` |
| size | Query | Number | N | 照会するリストのページサイズ(デフォルト値: 20)<br/>- 最小値: `1`<br/>- 最大値: `100` |

<a id="list-events-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-events-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "totalCounts": 1,
    "events": [
        {
            "eventCategoryType": "ALL",
            "eventCode": "INSTC_02_01",
            "sourceId": "550e8400-e29b-41d4-a716-446655440000",
            "sourceName": "sourceName-example",
            "messages": [
                {
                    "langCode": "KO",
                    "message": "message-example"
                }
            ],
            "eventYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| totalCounts | Number | 全イベントリストの数 |
| events | Array | イベントリスト |
| events.eventCategoryType | Enum | イベントカテゴリータイプ<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| events.eventCode | Enum | 発生したイベントのタイプ |
| events.sourceId | UUID | イベントソースの識別子 |
| events.sourceName | String | イベントソースを識別できる名前 |
| events.messages | Array | イベントメッセージリスト |
| events.messages.langCode | Enum | 言語コード<br/>- `KO`<br/>- `EN`<br/>- `JA`<br/>- `ZH` |
| events.messages.message | String | イベントメッセージ |
| events.eventYmdt | DateTime | イベント発生日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="event-subscription"></a>
## イベント購読 { #event-subscription }

<a id="list-event-subscriptions"></a>
### イベント購読一覧照会 { #list-event-subscriptions }

<a id="list-event-subscriptions-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:EventSubscription.List | イベント購読一覧照会 |

<a id="list-event-subscriptions-request"></a>
#### リクエスト

```http
GET /v4.0/event-subscriptions
```

<a id="list-event-subscriptions-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| eventSubscriptionId | Query | UUID | N | イベント購読の識別子 |
| eventSubscriptionName | Query | String | N | イベント購読を識別できる名前 |
| userGroupId | Query | UUID | N | ユーザーグループの識別子 |
| page | Query | Number | N | 照会するリストのページ(デフォルト値: 1)<br/>- 最小値: `1` |
| size | Query | Number | N | 照会するリストのページサイズ(デフォルト値: 20)<br/>- 最小値: `1`<br/>- 最大値: `100` |

<a id="list-event-subscriptions-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="list-event-subscriptions-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "totalCounts": 1,
    "eventSubscriptions": [
        {
            "eventSubscriptionId": "550e8400-e29b-41d4-a716-446655440000",
            "eventCategoryType": "ALL",
            "eventSubscriptionName": "eventSubscriptionName-example",
            "enabled": false,
            "notifyEmail": false,
            "notifySms": false,
            "eventCodes": [],
            "sources": [
                {
                    "sourceId": "550e8400-e29b-41d4-a716-446655440000",
                    "eventCategoryType": "ALL"
                }
            ],
            "userGroupIds": [
                "550e8400-e29b-41d4-a716-446655440000"
            ],
            "createdYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| totalCounts | Number | 全イベント購読一覧数 |
| eventSubscriptions | Array | イベント購読一覧 |
| eventSubscriptions.eventSubscriptionId | UUID | イベント購読の識別子 |
| eventSubscriptions.eventCategoryType | Enum | イベントカテゴリータイプ<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| eventSubscriptions.eventSubscriptionName | String | イベント購読を識別できる名前 |
| eventSubscriptions.enabled | Boolean | 有効かどうか |
| eventSubscriptions.notifyEmail | Boolean | メール送信の有無 |
| eventSubscriptions.notifySms | Boolean | SMS送信の有無 |
| eventSubscriptions.eventCodes | Array | 購読するイベントコード一覧 |
| eventSubscriptions.sources | Array | 購読するイベントソース一覧 |
| eventSubscriptions.sources.sourceId | UUID | イベントソースの識別子 |
| eventSubscriptions.sources.eventCategoryType | Enum | イベントカテゴリータイプ<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| eventSubscriptions.userGroupIds | Array | イベント購読中のユーザーグループの識別子一覧 |
| eventSubscriptions.createdYmdt | DateTime | 作成日時(YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-an-event-subscription"></a>
### イベント購読作成 { #create-an-event-subscription }

<a id="create-an-event-subscription-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:EventSubscription.Create | イベント購読作成 |

<a id="create-an-event-subscription-request"></a>
#### リクエスト

```http
POST /v4.0/event-subscriptions
```

<a id="create-an-event-subscription-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "eventCategoryType": "ALL",
    "eventSubscriptionName": "eventSubscriptionName-example",
    "enabled": false,
    "notifyEmail": false,
    "notifySms": false,
    "eventCodes": [],
    "sources": [
        {
            "sourceId": "550e8400-e29b-41d4-a716-446655440000",
            "eventCategoryType": "ALL"
        }
    ],
    "userGroupIds": []
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| eventCategoryType | Enum | Y | イベントカテゴリータイプ<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| eventSubscriptionName | String | Y | イベント購読を識別できる名前 |
| enabled | Boolean | Y | 有効かどうか |
| notifyEmail | Boolean | Y | メール送信の有無 |
| notifySms | Boolean | Y | SMS送信の有無 |
| eventCodes | Array | Y | 購読するイベントコード一覧 |
| sources | Array | Y | 購読するイベントソース一覧 |
| sources.sourceId | UUID | Y | イベントソースの識別子 |
| sources.eventCategoryType | Enum | Y | イベントカテゴリータイプ<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| userGroupIds | Array | Y | イベント購読するユーザーグループの識別子一覧 |

<a id="create-an-event-subscription-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "eventSubscriptionId": "550e8400-e29b-41d4-a716-446655440000"
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| eventSubscriptionId | UUID | イベント購読の識別子 |

---

<a id="delete-an-event-subscription"></a>
### イベント購読削除 { #delete-an-event-subscription }

<a id="delete-an-event-subscription-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:EventSubscription.Delete | イベント購読削除 |

<a id="delete-an-event-subscription-request"></a>
#### リクエスト

```http
DELETE /v4.0/event-subscriptions/{eventSubscriptionId}
```

<a id="delete-an-event-subscription-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| eventSubscriptionId | URL | UUID | Y | イベント購読の識別子 |

<a id="delete-an-event-subscription-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="delete-an-event-subscription-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="modify-an-event-subscription"></a>
### イベント購読修正 { #modify-an-event-subscription }

<a id="modify-an-event-subscription-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:EventSubscription.Modify | イベント購読修正 |

<a id="modify-an-event-subscription-request"></a>
#### リクエスト

```http
PUT /v4.0/event-subscriptions/{eventSubscriptionId}
```

<a id="modify-an-event-subscription-request-parameters"></a>
#### リクエストパラメータ

| 名前 | 種類 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|-----|
| eventSubscriptionId | URL | UUID | Y | イベント購読の識別子 |

<a id="modify-an-event-subscription-request-body"></a>
#### リクエスト本文

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "eventCategoryType": "ALL",
    "eventSubscriptionName": "eventSubscriptionName-example",
    "enabled": false,
    "notifyEmail": false,
    "notifySms": false,
    "eventCodes": [],
    "sources": [
        {
            "sourceId": "550e8400-e29b-41d4-a716-446655440000",
            "eventCategoryType": "ALL"
        }
    ],
    "userGroupIds": []
}
```

</details>

| 名前 | 形式 | 必須 | 説明 |
|-----|-----|-----|-----|
| eventCategoryType | Enum | N | イベントカテゴリータイプ<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| eventSubscriptionName | String | N | イベント購読を識別できる名前 |
| enabled | Boolean | N | 有効かどうか |
| notifyEmail | Boolean | N | メール送信の有無 |
| notifySms | Boolean | N | SMS送信の有無 |
| eventCodes | Array | N | 購読するイベントコード一覧 |
| sources | Array | N | 購読するイベントソース一覧 |
| sources.sourceId | UUID | Y | イベントソースの識別子 |
| sources.eventCategoryType | Enum | Y | イベントカテゴリータイプ<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| userGroupIds | Array | N | イベント購読するユーザーグループの識別子一覧 |

<a id="modify-an-event-subscription-response"></a>
#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="availability-zones"></a>
## アベイラビリティゾーン { #availability-zones }

<a id="get-availability-zones"></a>
### アベイラビリティゾーンリストを表示 { #get-availability-zones }

<a id="get-availability-zones-required-permissions"></a>
#### 必要権限

| 権限名 | 説明 |
|-----|-----|
| RDSforMariaDB:AvailabilityZone.List | アベイラビリティゾーンリストを表示 |

<a id="get-availability-zones-request"></a>
#### リクエスト

```http
GET /v4.0/availability-zones
```

<a id="get-availability-zones-request-body"></a>
#### リクエスト本文

このAPIはリクエスト本文を要求しません。

<a id="get-availability-zones-response"></a>
#### レスポンス

<details>
  <summary><strong>サンプルコード</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "availabilityZones": [
        {
            "availabilityZoneName": "availabilityZoneName-example",
            "zoneState": {
                "available": false
            }
        }
    ]
}
```

</details>

| 名前 | 形式 | 説明 |
|-----|-----|-----|
| availabilityZones | Array | アベイラビリティゾーンリスト |
| availabilityZones.availabilityZoneName | String | アベイラビリティゾーン名 |
| availabilityZones.zoneState | Object | アベイラビリティゾーンの状態 |
| availabilityZones.zoneState.available | Boolean | アベイラビリティゾーンが使用可能かどうか |

---

