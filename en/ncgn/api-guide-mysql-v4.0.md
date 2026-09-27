<!-- pre-align:aligned sig=d58a9ac7e400 -->

<a id="database-rds-for-enginepascalcase-api-guide"></a>
## Database > RDS for MySQL > API Guide { #database-rds-for-enginepascalcase-api-guide }

<a id="rds-for-enginepascalcase-api-common-information"></a>
## RDS for MySQL API Common Information { #rds-for-enginepascalcase-api-common-information }

<a id="api-endpoint"></a>
### API Endpoint { #api-endpoint }

| Region | Endpoint |
|------|----------|
| Korea (Pangyo) region | https://kr1-rds-mysql.api.gncloud.go.kr |


<a id="common-authorization"></a>
### Authentication and Authorization { #common-authorization }

RDS for MySQL uses User Access Key tokens for authentication and authorization when making API calls. The User Access Key token is a temporary, Bearer-type access token issued from a User Access Key. For more information on issuing and using User Access Key tokens, see [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).
The issued token must be included in the request header along with the Appkey.

| Name | Type | Format | Required | Description |
|-----|-----|-----|------|-----|
| X-TC-APP-KEY | Header | String | Y    | Appkey of RDS for MySQL or integrated Appkey for project |
| X-NHN-AUTHORIZATION | Header | String | Y    | Bearer type token issued with the Public API |

In addition, the APIs you can call are limited based on the project permissions. The `RDS for MySQL ADMIN` and `RDS for MySQL VIEWER` roles are granted the default permissions below, and you can grant only the permissions you need from the Role Group Management menu in the project.

* The `RDS for MySQL ADMIN` role is granted all permissions required to execute APIs.
* The `RDS for MySQL VIEWER` role is granted only the permissions to query information.
    * Cannot use any features aimed at DB instances or create, modify, or delete any DB instance.
    * But, notification group and user group-related features are available.

If an API request fails to authenticate or is not authorized, the following error occurs.

| resultCode | resultMessage | Description |
|------------|---------------|-----|
| 80401 | Unauthorized | Failed to authenticate. |
| 80403 | Forbidden | Unauthorized. |

<a id="common-response"></a>
### Common Response Information { #common-response }

The API responds with '200 OK' to all API requests. For more information on the response results, see the header in the response body.

<details>
  <summary><strong>Successful Response</strong></summary>

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
  <summary><strong>Failure Response</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| resultCode | Number | Result code<br/>- Success: `0`<br/>- Failure: `Non-zero` |
| resultMessage | String | Result message |
| isSuccessful | Boolean | Successful or not |

<a id="db-engine"></a>
## DB Engine Version { #db-engine }

<a id="supported-db-engine-versions"></a>
### Supported DB Engine Versions { #supported-db-engine-versions }

| DB engine version | Available for creation | Whether restoration from Object Storage is available | Authentication Plugin Support |
|------------|----------|------------------|------------|
| MYSQL_V5633 | N | N | NATIVE |
| MYSQL_V5715 | Y | Y | SHA256, NATIVE |
| MYSQL_V5719 | Y | Y | SHA256, NATIVE |
| MYSQL_V5726 | Y | Y | SHA256, NATIVE |
| MYSQL_V5731 | N | N | SHA256, NATIVE |
| MYSQL_V5733 | Y | N | SHA256, NATIVE |
| MYSQL_V5737 | Y | Y | SHA256, NATIVE |
| MYSQL_V8018 | N | N | CACHING_SHA2, NATIVE |
| MYSQL_V8023 | N | N | CACHING_SHA2, NATIVE |
| MYSQL_V8028 | N | N | CACHING_SHA2, NATIVE |
| MYSQL_V8032 | N | N | CACHING_SHA2, NATIVE |
| MYSQL_V8033 | N | N | CACHING_SHA2, NATIVE |
| MYSQL_V8034 | N | N | CACHING_SHA2, NATIVE |
| MYSQL_V8035 | Y | Y | CACHING_SHA2, NATIVE |
| MYSQL_V8036 | Y | Y | CACHING_SHA2, NATIVE |
| MYSQL_V8040 | Y | Y | CACHING_SHA2, NATIVE |
| MYSQL_V8041 | Y | Y | CACHING_SHA2, NATIVE |
| MYSQL_V8042 | Y | Y | CACHING_SHA2, NATIVE |
| MYSQL_V8043 | Y | Y | CACHING_SHA2, NATIVE |
| MYSQL_V8044 | Y | Y | CACHING_SHA2, NATIVE |
| MYSQL_V8045 | Y | Y | CACHING_SHA2, NATIVE |
| MYSQL_V8046 | Y | Y | CACHING_SHA2, NATIVE |
| MYSQL_V8405 | Y | Y | CACHING_SHA2 |
| MYSQL_V8406 | Y | Y | CACHING_SHA2 |
| MYSQL_V8407 | Y | Y | CACHING_SHA2 |
| MYSQL_V8408 | Y | Y | CACHING_SHA2 |
| MYSQL_V8409 | Y | Y | CACHING_SHA2 |
| MYSQL_V8411 | Y | Y | CACHING_SHA2 |

* The values above can be used for the dbVersion field of Enum type.
* Depending on the version, creation or restoration may not be available.

<a id="list-db-engines"></a>
### List DB Engines { #list-db-engines }

<a id="list-db-engines-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbVersion.List | List DB Engine Versions |

<a id="list-db-engines-request"></a>
#### Request

```http
GET /v4.0/db-versions
```

<a id="list-db-engines-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-engines-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbVersions": [
        {
            "dbVersion": "MYSQL_V8411",
            "dbVersionName": "MySQL 8.4.11",
            "restorableFromObs": true
        }
    ]
}
```

</details>

| Name | Format | Description |
|-----|-----|-----|
| dbVersions | Array | DB engine list |
| dbVersions.dbVersion | Enum | DB engine version |
| dbVersions.dbVersionName | String | DB engine version name |
| dbVersions.restorableFromObs | Boolean | Whether restoration from Object Storage is available |

---

<a id="project-information"></a>
## Project Information { #project-information }

<a id="list-project-members"></a>
### List Project Members { #list-project-members }

<a id="list-project-members-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Project.Get | List Project Members |

<a id="list-project-members-request"></a>
#### Request

```http
GET /v4.0/project/members
```

<a id="list-project-members-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-project-members-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| members | Array | Project member list |
| members.memberId | UUID | Project member identifier |
| members.memberName | String | Project member name |
| members.emailAddress | String | Project member email address |
| members.phoneNumber | String | Project member mobile |

---

<a id="list-regions"></a>
### List Regions { #list-regions }

<a id="list-regions-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Project.Get | List Regions |

<a id="list-regions-request"></a>
#### Request

```http
GET /v4.0/project/regions
```

<a id="list-regions-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-regions-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| regions | Array | Region list |
| regions.regionCode | Enum | Region code<br/>- `KR1`: Korea (Pangyo) |
| regions.isEnabled | Boolean | Whether to enable a region |

---

<a id="specifications-of-db-instance"></a>
## Specifications of DB Instance { #specifications-of-db-instance }

<a id="list-db-instance-specifications"></a>
### List DB Instance Specifications { #list-db-instance-specifications }

<a id="list-db-instance-specifications-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbFlavor.List | List DB Instance Specifications |

<a id="list-db-instance-specifications-request"></a>
#### Request

```http
GET /v4.0/db-flavors
```

<a id="list-db-instance-specifications-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-instance-specifications-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| dbFlavors | Array | List of DB instance specifications |
| dbFlavors.dbFlavorId | UUID | Identifier of DB instance specifications |
| dbFlavors.dbFlavorName | String | Name of DB instance specifications |
| dbFlavors.ram | Number | Memory size (MB) |
| dbFlavors.vcpus | Number | CPU cores |

---

<a id="network"></a>
## Network { #network }

<a id="list-subnets"></a>
### List Subnets { #list-subnets }

<a id="list-subnets-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Network.List | List subnets |

<a id="list-subnets-request"></a>
#### Request

```http
GET /v4.0/network/subnets
```

<a id="list-subnets-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-subnets-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| subnets | Array | Subnet list |
| subnets.subnetId | UUID | Subnet identifier |
| subnets.subnetName | String | Name to identify subnets |
| subnets.subnetCidr | String | CIDR of subnet |
| subnets.usingGateway | Boolean | Whether to use gateway |
| subnets.availableIpCount | Number | Number of available IPs |

---

<a id="storage"></a>
## Data Storage { #storage }

<a id="list-storage-type"></a>
### List Storage Type { #list-storage-type }

<a id="list-storage-type-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Storage.List | List Storage Types |

<a id="list-storage-type-request"></a>
#### Request

```http
GET /v4.0/storage-types
```

<a id="list-storage-type-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-storage-type-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| storageTypes | Array | Storage type list |

---

<a id="task-information"></a>
## Task Information { #task-information }

<a id="job-status"></a>
### Task Status { #job-status }

| Status Name                | Description                   |
|--------------------|----------------------|
| `PREPARING`        | Task in preparation         |
| `READY`            | Task in ready        |
| `RUNNING`          | Task in progress         |
| `COMPLETED`        | Task completed           |
| `REGISTERED`       | Task registered           |
| `WAIT_TO_REGISTER` | Task waiting to register       |
| `INTERRUPTED`      | Task being interrupted |
| `CANCELED`         | Task canceled           |
| `FAILED`           | Task failed           |
| `ERROR`            | Error occurred while task in progress   |
| `DELETED`          | Task deleted           |
| `FAIL_TO_READY`    | Failed to get ready for task        |

<a id="list-task-details"></a>
### List Task Details { #list-task-details }

<a id="list-task-details-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Job.Get | List Task Details |

<a id="list-task-details-request"></a>
#### Request

```http
GET /v4.0/jobs/{jobId}
```

<a id="list-task-details-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| jobId | URL | UUID | Y | Task identifier |

<a id="list-task-details-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-task-details-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Task identifier |
| jobStatus | Enum | Current task status<br/>- `DELETED`<br/>- `CANNOT_PROGRESS`<br/>- `FAILED`<br/>- `ERROR`<br/>- `CANCELED`<br/>- `INTERRUPTED`<br/>- `COMPLETED`<br/>- `COMPLETED_WITH_ERROR`<br/>- `RUNNING`<br/>- `PREPARING`<br/>- `READY`<br/>- `CREATED`<br/>- `FAIL_TO_READY`<br/>- `REGISTERED`<br/>- `FAIL_TO_REGISTER`<br/>- `WAIT_TO_REGISTER` |
| resourceRelations | Array | Relevant resource list |
| resourceRelations.resourceType | String | Relevant resource type |
| resourceRelations.resourceId | String | Relevant resource identifier |
| createdYmdt | DateTime | Created at |
| updatedYmdt | DateTime | Modified date and time |

---

<a id="db-instance-group"></a>
## DB Instance Group { #db-instance-group }

<a id="list-db-instance-groups"></a>
### List DB Instance Groups { #list-db-instance-groups }

<a id="list-db-instance-groups-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceGroup.List | List DB Instance Groups |

<a id="list-db-instance-groups-request"></a>
#### Request

```http
GET /v4.0/db-instance-groups
```

<a id="list-db-instance-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-instance-groups-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| dbInstanceGroups | Array | DB instance groups |
| dbInstanceGroups.dbInstanceGroupId | UUID | DB instance group identifier |
| dbInstanceGroups.replicationType | Enum | DB instance group replication type<br/>- `STANDALONE`: High availability is not used<br/>- `HIGH_AVAILABILITY`: High availability is used |
| dbInstanceGroups.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbInstanceGroups.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="list-db-instance-group-details"></a>
### List DB Instance Group Details { #list-db-instance-group-details }

<a id="list-db-instance-group-details-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceGroup.Get | List DB Instance Group Details |

<a id="list-db-instance-group-details-request"></a>
#### Request

```http
GET /v4.0/db-instance-groups/{dbInstanceGroupId}
```

<a id="list-db-instance-group-details-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceGroupId | URL | UUID | Y | DB instance group identifier |

<a id="list-db-instance-group-details-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-instance-group-details-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| dbInstanceGroupId | UUID | DB instance group identifier |
| replicationType | Enum | DB instance group replication type<br/>- `STANDALONE`: High availability is not used<br/>- `HIGH_AVAILABILITY`: High availability is used |
| dbInstances | Array | DB instances belong to DB instance group |
| dbInstances.dbInstanceId | UUID | DB instance identifier |
| dbInstances.dbInstanceType | Enum | Role type of DB instance<br/>- `MASTER`: Primary<br/>- `FAILED_MASTER`: Failed Over Primary<br/>- `CANDIDATE_MASTER`: Standby<br/>- `READ_ONLY_SLAVE`: Read replica |
| dbInstances.dbInstanceStatus | Enum | DB instance current status<br/>- `BEFORE_CREATE`: Before creation (gray)<br/>- `AVAILABLE`: Available (green)<br/>- `STORAGE_FULL`: Insufficient capacity (red)<br/>- `FAIL_TO_CREATE`: Failed to create (red)<br/>- `FAIL_TO_CONNECT`: Failed to connect (red)<br/>- `REPLICATION_STOP`: Replication stopped (red)<br/>- `REPLICATION_DELAY`: Replication delayed (yellow)<br/>- `FAILOVER`: Failover completed (red)<br/>- `SHUTDOWN`: Stopped (gray)<br/>- `DELETED`: Deleted (gray) |
| createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="db-instance"></a>
## DB Instance { #db-instance }

<a id="db-instance-status"></a>
### DB Instance Status { #db-instance-status }

| Status                  | Description                           |
|---------------------|------------------------------|
| `AVAILABLE`         | DB instance is available           |
| `BEFORE_CREATE`     | Before DB instance is created            |
| `STORAGE_FULL`      | Insufficient DB instance storage          |
| `FAIL_TO_CREATE`    | Failed to create DB instance           |
| `FAIL_TO_CONNECT`   | Failed to connect DB instance           |
| `REPLICATION_STOP`  | Replication of DB instance is stopped          |
| `FAILOVER`          | High availability DB instance failed over      |
| `SHUTDOWN`          | DB instance is stopped              |
| `DELETED`           | DB instance is deleted              |

<a id="db-instance-progress-status"></a>
### DB Instance Progress Status { #db-instance-progress-status }

| Status                         | Description           |
|----------------------------|--------------|
| `APPLYING_PARAMETER_GROUP` | Parameter group is being applied |
| `BACKING_UP`               | Backing up         |
| `CANCELING`                | Canceling         |
| `CREATING`                 | Creating         |
| `CREATING_SCHEMA`          | Creating DB schema  |
| `CREATING_USER`            | Creating user     |
| `DELETING`                 | Deleting         |
| `DELETING_SCHEMA`          | Deleting DB schema  |
| `DELETING_USER`            | Deleting user     |
| `EXPORTING_BACKUP`         | Exporting backup   |
| `FAILING_OVER`             | Under failover      |
| `MIGRATING`                | Under migration     |
| `MODIFYING`                | Under modification         |
| `PREPARING`                | In preparation         |
| `PROMOTING`                | Promoting         |
| `REBUILDING`               | Rebuilding        |
| `REPAIRING`                | Recovering         |
| `REPLICATING`              | Replicating         |
| `RESTARTING`               | Restarting        |
| `RESTARTING_FORCIBLY`      | Force restarting     |
| `RESTORING`                | Restoring         |
| `STARTING`                 | Starting         |
| `STOPPING`                 | Stopping         |
| `SYNCING_SCHEMA`           | Synchronizing DB schema |
| `SYNCING_USER`             | Synchronizing user    |
| `UPDATING_USER`            | Modifying user     |

<a id="list-db-instances"></a>
### List DB Instances { #list-db-instances }

<a id="list-db-instances-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.List | List DB instances |

<a id="list-db-instances-request"></a>
#### Request

```http
GET /v4.0/db-instances
```

<a id="list-db-instances-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-instances-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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
            "dbVersion": "MYSQL_V8411",
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

| Name | Format | Description |
|-----|-----|-----|
| dbInstances | Array | DB instances |
| dbInstances.dbInstanceId | UUID | DB instance identifier |
| dbInstances.dbInstanceGroupId | UUID | DB instance group identifier |
| dbInstances.dbInstanceName | String | Name to identify the primary DB instance |
| dbInstances.description | String | Additional information of DB instance |
| dbInstances.dbVersion | Enum | DB engine version |
| dbInstances.dbPort | Number | DB port |
| dbInstances.dbInstanceType | Enum | Role type of DB instance<br/>- `MASTER`: Primary<br/>- `FAILED_MASTER`: Failed Over Primary<br/>- `CANDIDATE_MASTER`: Standby<br/>- `READ_ONLY_SLAVE`: Read replica |
| dbInstances.dbInstanceStatus | Enum | DB instance current status<br/>- `BEFORE_CREATE`: Before creation (gray)<br/>- `AVAILABLE`: Available (green)<br/>- `STORAGE_FULL`: Insufficient capacity (red)<br/>- `FAIL_TO_CREATE`: Failed to create (red)<br/>- `FAIL_TO_CONNECT`: Failed to connect (red)<br/>- `REPLICATION_STOP`: Replication stopped (red)<br/>- `REPLICATION_DELAY`: Replication delayed (yellow)<br/>- `FAILOVER`: Failover completed (red)<br/>- `SHUTDOWN`: Stopped (gray)<br/>- `DELETED`: Deleted (gray) |
| dbInstances.progressStatus | Enum | DB instance current progress status |
| dbInstances.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbInstances.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-db-instance"></a>
### Create DB Instance { #create-db-instance }

<a id="create-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Create | Create DB Instance |

<a id="create-db-instance-request"></a>
#### Request

```http
POST /v4.0/db-instances
```

<a id="create-db-instance-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "description": "description-example",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "dbVersion": "MYSQL_V8411",
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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Name to identify the primary DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB instance<br/>- Maximum length: `100` |
| dbFlavorId | UUID | Y | Identifier of DB instance specifications |
| dbVersion | Enum | Y | DB engine version |
| dbPort | Number | Y | DB port<br/>- Minimum value: 3306, Maximum value: 43306 |
| dbUserName | String | Y | DB user account name<br/>- Minimum length: `1`<br/>- Maximum length: `32` |
| dbPassword | String | Y | DB user account password<br/>- Minimum length: `4`<br/>- Maximum length: `256` |
| parameterGroupId | UUID | Y | Parameter group identifier |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| userGroupIds | Array | N | User group identifiers |
| useHighAvailability | Boolean | N | Whether to use high availability<br/>- Default: `false` |
| pingInterval | Number | N | Ping interval (sec) when using high availability<br/>- Default: `3`<br/>- Minimum value: `1`<br/>- Maximum value: `600` |
| useDefaultNotification | Boolean | N | Whether to use default notification<br/>- Default: `false` |
| useDeletionProtection | Boolean | N | Whether to protect against deletion<br/>- Default: `false` |
| useSlowQueryAnalysis | Boolean | N | Whether to analyze slow queries<br/>- Default: `true` |
| authenticationPlugin | Enum | N | Authentication Plugin<br/>- `NATIVE`: mysql_native_password authentication<br/>- `CACHING_SHA2`: caching_sha2_password authentication (MySQL only)<br/>- `SHA256`: sha256_password authentication (MySQL only) |
| tlsOption | Enum | N | TLS option<br/>- Default: `NONE`<br/>- `NONE`: TLS is not used<br/>- `SSL`: SSL authentication<br/>- `X509`: X509 certificate authentication |
| network | Object | Y | Network information objects |
| network.subnetId | UUID | Y | Subnet identifier |
| network.usePublicAccess | Boolean | N | External access is available or not<br/>- Default: `false` |
| network.availabilityZone | Enum | Y | Availability zone where DB instance will be created |
| storage | Object | Y | Storage information object |
| storage.storageType | Enum | Y | Data storage type |
| storage.storageSize | Number | Y | Block Storage Size (GB)<br/>- Minimum value: `20` |
| storage.storageAutoscale | Object | N | Block Storage Auto Scaling Objects |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | Whether to enable storage auto scaling<br/>- Default: `false` |
| backup | Object | Y | Backup information objects |
| backup.backupPeriod | Number | Y | Backup retention period<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR1`: Korea (Pangyo) |
| backup.useBackupLock | Boolean | N | Whether to use table lock<br/>- Default: `true` |
| backup.backupSchedules | Array | Y | Backup schedule list |
| backup.backupSchedules.backupWndBgnTime | Time | Y | Backup start time |
| backup.backupSchedules.backupWndDuration | Enum | Y | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |

<a id="create-db-instance-section"></a>
#### When using high availability

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Name to identify the standby DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |

<a id="create-db-instance-section-2"></a>
#### When using storage auto scaling

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | Auto scale out conditions (%)<br/>- Minimum value: `50`<br/>- Maximum value: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | Auto scaling maximum size (GB)<br/>- Maximum value: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | Auto scaling cooldown time (minutes)<br/>- Minimum value: `10`<br/>- Maximum value: `1440` |

<a id="create-db-instance-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="restore-from-object-storage"></a>
### Restore from Object Storage { #restore-from-object-storage }

<a id="restore-from-object-storage-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.RestoreFromObs | Restore from Object Storage |

<a id="restore-from-object-storage-request"></a>
#### Request

```http
POST /v4.0/db-instances/restore-from-obs
```

<a id="restore-from-object-storage-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "description": "description-example",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "dbPort": 13306,
    "dbVersion": "MYSQL_V8411",
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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Name to identify the primary DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB instance<br/>- Maximum length: `100` |
| dbFlavorId | UUID | Y | Identifier of DB instance specifications |
| dbPort | Number | Y | DB port |
| dbVersion | Enum | Y | DB engine version |
| useHighAvailability | Boolean | N | Whether to use high availability<br/>- Default: `false` |
| pingInterval | Number | N | Ping interval (sec) when using high availability<br/>- Minimum value: `1`<br/>- Maximum value: `600` |
| storage | Object | Y | Storage information object |
| storage.storageType | Enum | Y | Storage type |
| storage.storageSize | Number | Y | Block Storage Size (GB)<br/>- Minimum value: `20` |
| storage.storageAutoscale | Object | N | Block Storage Auto Scaling Objects |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | Whether to enable storage auto scaling<br/>- Default: `false` |
| network | Object | Y | Network information objects |
| network.subnetId | UUID | Y | Subnet identifier |
| network.usePublicAccess | Boolean | N | External access is available or not<br/>- Default: `false` |
| network.availabilityZone | Enum | Y | Availability zone where DB instance will be created |
| backup | Object | Y | Backup information objects |
| backup.backupPeriod | Number | Y | Backup retention period<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR1`: Korea (Pangyo) |
| backup.useBackupLock | Boolean | N | Whether to use table lock<br/>- Default: `true` |
| backup.backupSchedules | Array | Y | Backup schedule list |
| backup.backupSchedules.backupWndBgnTime | Time | Y | Backup start time |
| backup.backupSchedules.backupWndDuration | Enum | Y | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |
| restore | Object | Y | Restoration information object |
| restore.tenantId | String | Y | Tenant ID of the Object Storage where the backup is saved |
| restore.username | String | Y | NHN Cloud member or IAM member ID |
| restore.password | String | Y | API password of the Object Storage where the backup is saved |
| restore.targetContainer | String | Y | Container of the Object Storage where the backup is saved |
| restore.objectPath | String | Y | Backup path stored in container |
| useDefaultNotification | Boolean | N | Whether to use default notification<br/>- Default: `false` |
| useSlowQueryAnalysis | Boolean | N | Whether to analyze slow queries<br/>- Default: `true` |
| parameterGroupId | UUID | Y | Parameter group identifier |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| userGroupIds | Array | N | User group identifiers |
| useDeletionProtection | Boolean | N | Whether to protect against deletion<br/>- Default: `false` |

<a id="restore-from-object-storage-section"></a>
#### When using high availability

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Name to identify the standby DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |

<a id="restore-from-object-storage-section-2"></a>
#### When using storage auto scaling

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | Auto scale out conditions (%)<br/>- Minimum value: `50`<br/>- Maximum value: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | Auto scaling maximum size (GB)<br/>- Maximum value: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | Auto scaling cooldown time (minutes)<br/>- Minimum value: `10`<br/>- Maximum value: `1440` |

<a id="restore-from-object-storage-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="delete-db-instance"></a>
### Delete DB Instance { #delete-db-instance }

<a id="delete-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Delete | Delete DB instance |

<a id="delete-db-instance-request"></a>
#### Request

```http
DELETE /v4.0/db-instances/{dbInstanceId}
```

<a id="delete-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="delete-db-instance-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "deleteAutoBackup": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| deleteAutoBackup | Boolean | N | Whether to delete automatic backups<br/>- Default: `false` |

<a id="delete-db-instance-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="list-db-instance-details"></a>
### List DB Instance Details { #list-db-instance-details }

<a id="list-db-instance-details-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Get | List DB Instance Details |

<a id="list-db-instance-details-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}
```

<a id="list-db-instance-details-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="list-db-instance-details-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-instance-details-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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
    "dbVersion": "MYSQL_V8411",
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

| Name | Format | Description |
|-----|-----|-----|
| dbInstanceId | UUID | DB instance identifier |
| dbInstanceGroupId | UUID | DB instance group identifier |
| dbInstanceName | String | Name to identify the primary DB instance |
| description | String | Additional information of DB instance |
| dbVersion | Enum | DB engine version |
| dbPort | Number | DB port |
| dbInstanceType | Enum | Role type of DB instance<br/>- `MASTER`: Primary<br/>- `FAILED_MASTER`: Failed Over Primary<br/>- `CANDIDATE_MASTER`: Standby<br/>- `READ_ONLY_SLAVE`: Read replica |
| dbInstanceStatus | Enum | DB instance current status<br/>- `BEFORE_CREATE`: Before creation (gray)<br/>- `AVAILABLE`: Available (green)<br/>- `STORAGE_FULL`: Insufficient capacity (red)<br/>- `FAIL_TO_CREATE`: Failed to create (red)<br/>- `FAIL_TO_CONNECT`: Failed to connect (red)<br/>- `REPLICATION_STOP`: Replication stopped (red)<br/>- `REPLICATION_DELAY`: Replication delayed (yellow)<br/>- `FAILOVER`: Failover completed (red)<br/>- `SHUTDOWN`: Stopped (gray)<br/>- `DELETED`: Deleted (gray) |
| progressStatus | Enum | DB instance current progress status |
| dbFlavorId | UUID | Identifier of DB instance specifications |
| parameterGroupId | UUID | Parameter group identifier applied to DB instance |
| dbSecurityGroupIds | Array | DB security group identifiers applied to DB instance |
| notificationGroupIds | Array | Notification group identifiers applied to DB instance |
| useDeletionProtection | Boolean | Whether to protect DB instance against deletion |
| useSlowQueryAnalysis | Boolean | Whether to analyze slow queries |
| supportAuthenticationPlugin | Boolean | Whether to support authentication plugin |
| needToApplyParameterGroup | Boolean | Need to apply the latest parameter group |
| needMigration | Boolean | Need to migrate |
| supportDbVersionUpgrade | Boolean | Whether to support DB version upgrade |
| createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-db-instance"></a>
### Modify DB Instance { #modify-db-instance }

<a id="modify-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Modify | Modify DB Instance |

<a id="modify-db-instance-request"></a>
#### Request

```http
PUT /v4.0/db-instances/{dbInstanceId}
```

<a id="modify-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="modify-db-instance-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "dbInstanceCandidateName": "dbInstanceCandidateName",
    "description": "description-example",
    "dbPort": 13306,
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbVersion": "MYSQL_V8411",
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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceName | String | N | Name to identify the primary DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| dbInstanceCandidateName | String | N | Name to identify the standby DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB instance<br/>- Maximum length: `100` |
| dbPort | Number | N | DB port<br/>- Minimum value: 3306, Maximum value: 43306 |
| dbFlavorId | UUID | N | Identifier of DB instance specifications |
| parameterGroupId | UUID | N | Parameter group identifier |
| dbVersion | Enum | N | DB engine version |
| useSlowQueryAnalysis | Boolean | N | Whether to analyze slow queries |
| useDummy | Boolean | N | Whether to use dummies when upgrading the DB version of a single DB instance<br/>- Default: `false` |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| executeBackup | Boolean | N | Whether to perform a backup at the current point in time<br/>- Default: `false` |
| useOnlineFailover | Boolean | N | Whether to restart using failover<br/>- Default: `false` |
| waitReplicationDelay | Boolean | N | Wait for replication delay to be resolved<br/>- Default: `false` |
| useReadOnly | Boolean | N | Block write load<br/>- Default: `false` |

<a id="modify-db-instance-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="view-backup-information"></a>
### View Backup Information { #view-backup-information }

<a id="view-backup-information-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Get | View Backup Information |

<a id="view-backup-information-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/backup-info
```

<a id="view-backup-information-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="view-backup-information-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-backup-information-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| backupPeriod | Number | Backup retention period |
| ftwrlWaitTimeout | Number | Query latency (sec) |
| backupRetryCount | Number | Number of backup retries |
| replicationRegion | Enum | Backup replication region<br/>- `KR1`: Korea (Pangyo) |
| useBackupLock | Boolean | Whether to use table lock |
| backupSchedules | Array | Backup schedule list |
| backupSchedules.backupWndBgnTime | Time | Backup start time |
| backupSchedules.backupWndDuration | Enum | Backup window<br/>- `HALF_AN_HOUR`<br/>- `ONE_HOUR`<br/>- `ONE_HOUR_AND_HALF`<br/>- `TWO_HOURS`<br/>- `TWO_HOURS_AND_HALF`<br/>- `THREE_HOURS` |

---

<a id="modify-backup-information"></a>
### Modify Backup Information { #modify-backup-information }

<a id="modify-backup-information-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Modify | Modify Backup Information |

<a id="modify-backup-information-request"></a>
#### Request

```http
PUT /v4.0/db-instances/{dbInstanceId}/backup-info
```

<a id="modify-backup-information-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="modify-backup-information-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| backupPeriod | Number | N | Backup retention period<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| replicationRegion | Enum | N | Backup replication region<br/>- `KR1`: Korea (Pangyo) |
| useBackupLock | Boolean | N | Whether to use table lock |
| backupSchedules | Array | N | Backup schedule list |
| backupSchedules.backupWndBgnTime | Time | Y | Backup start time |
| backupSchedules.backupWndDuration | Enum | Y | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |

<a id="modify-backup-information-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="view-binlog-lists"></a>
### View BinLog Lists { #view-binlog-lists }

<a id="view-binlog-lists-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceBinLog.List | View BinLog Lists |

<a id="view-binlog-lists-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/binlogs
```

<a id="view-binlog-lists-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| deletable | Query | Boolean | N | Whether to query only deletable BinLogs (true: excluding the last BinLog, false: all)<br/>- Default: `false` |

<a id="view-binlog-lists-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-binlog-lists-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| binLogs | Array | BinLog file list |
| binLogs.binLogFileName | String | BinLog file name |
| binLogs.binLogFileSize | Number | BinLog file size (Byte) |
| binLogs.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="delete-binlog"></a>
### Delete BinLog { #delete-binlog }

<a id="delete-binlog-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceBinLog.Purge | Delete BinLog |

<a id="delete-binlog-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/binlogs/purge
```

<a id="delete-binlog-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="delete-binlog-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "lastBinLogFileName": "mysql-bin.000010"
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| lastBinLogFileName | String | Y | Name of the last BinLog file to delete (files up to just before this file are deleted) |

<a id="delete-binlog-response"></a>
#### Response

This API does not return a response body.

---

<a id="view-certificate-file-lists"></a>
### View Certificate File Lists { #view-certificate-file-lists }

<a id="view-certificate-file-lists-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceCertificate.List | View certificate file lists |

<a id="view-certificate-file-lists-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/certificates
```

<a id="view-certificate-file-lists-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="view-certificate-file-lists-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-certificate-file-lists-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| certificates | Array | Certificate file list |
| certificates.fileName | String | Certificate file name |
| certificates.certificateType | Enum | Certificate type<br/>- `CA_FILE`<br/>- `CERT_FILE`<br/>- `KEY_FILE` |
| certificates.fileSize | Number | Certificate file size (Byte) |
| certificates.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="export-a-certificate-file"></a>
### Export a Certificate File { #export-a-certificate-file }

<a id="export-a-certificate-file-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceCertificate.Export | Export a certificate file |

<a id="export-a-certificate-file-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/certificates/upload
```

<a id="export-a-certificate-file-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="export-a-certificate-file-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| certificateTypes | Array | Y | List of certificate types to upload |
| tenantId | String | Y | Tenant ID of the Object Storage where the certificate file will be saved<br/>- Minimum length: `32`<br/>- Maximum length: `32` |
| username | String | Y | NHN Cloud member or IAM account ID |
| password | String | Y | API password of the Object Storage where the certificate file will be saved |
| targetContainer | String | Y | Container of the Object Storage where the certificate file will be saved |
| objectPath | String | Y | Path of the certificate file to be saved in the container |

<a id="export-a-certificate-file-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="list-db-schema"></a>
### List DB Schema { #list-db-schema }

<a id="list-db-schema-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceSchema.List | List DB Schema |

<a id="list-db-schema-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/db-schemas
```

<a id="list-db-schema-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="list-db-schema-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-schema-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| dbSchemas | Array | DB schema list |
| dbSchemas.dbSchemaId | UUID | DB schema identifier |
| dbSchemas.dbSchemaName | String | DB schema name |
| dbSchemas.dbSchemaStatus | Enum | DB schema current status<br/>- `STABLE`<br/>- `CREATING`<br/>- `SYNCING`<br/>- `DELETING`<br/>- `DELETED` |
| dbSchemas.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-db-schema"></a>
### Create DB Schema { #create-db-schema }

<a id="create-db-schema-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceSchema.Create | Create DB Schema |

<a id="create-db-schema-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/db-schemas
```

<a id="create-db-schema-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="create-db-schema-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "dbSchemaName": "dbSchemaName-example"
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbSchemaName | String | Y | DB schema name<br/>- Maximum length: `64`<br/>- Must start with a letter, allows letters/numbers/_, 1 to 64 characters, MySQL reserved words are not allowed |

<a id="create-db-schema-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="delete-db-schema"></a>
### Delete DB Schema { #delete-db-schema }

<a id="delete-db-schema-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceSchema.Delete | Delete DB Schema |

<a id="delete-db-schema-request"></a>
#### Request

```http
DELETE /v4.0/db-instances/{dbInstanceId}/db-schemas/{dbSchemaId}
```

<a id="delete-db-schema-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| dbSchemaId | URL | UUID | Y | DB schema identifier |

<a id="delete-db-schema-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-db-schema-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="list-db-users"></a>
### List DB Users { #list-db-users }

<a id="list-db-users-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceUser.List | List DB Users |

<a id="list-db-users-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/db-users
```

<a id="list-db-users-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="list-db-users-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-users-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| dbUsers | Array | DB users |
| dbUsers.dbUserId | UUID | DB user identifier |
| dbUsers.dbUserName | String | DB user account name |
| dbUsers.host | String | DB user account host name |
| dbUsers.authorityType | Enum | DB user permission type<br/>- `CUSTOM`: Custom permission<br/>- `READ`: Read permission<br/>- `CRUD`: CRUD permission<br/>- `DDL`: DDL permission<br/>- `ALL`: All permissions |
| dbUsers.dbUserStatus | Enum | DB user current status<br/>- `STABLE`<br/>- `CREATING`<br/>- `UPDATING`<br/>- `SYNCING`<br/>- `DELETING`<br/>- `DELETED` |
| dbUsers.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbUsers.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbUsers.authenticationPlugin | Enum | User authentication plugin<br/>- `NATIVE`: mysql_native_password authentication<br/>- `CACHING_SHA2`: caching_sha2_password authentication (MySQL only)<br/>- `SHA256`: sha256_password authentication (MySQL only) |
| dbUsers.tlsOption | Enum | Certificate option<br/>- `NONE`: TLS is not used<br/>- `SSL`: SSL authentication<br/>- `X509`: X509 certificate authentication |

---

<a id="create-db-user"></a>
### Create DB User { #create-db-user }

<a id="create-db-user-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceUser.Create | Create DB User |

<a id="create-db-user-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/db-users
```

<a id="create-db-user-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="create-db-user-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbUserName | String | Y | DB user account name<br/>- Minimum length: `1`<br/>- Maximum length: `32` |
| dbPassword | String | Y | DB user account password<br/>- Minimum length: `4`<br/>- Maximum length: `256` |
| host | String | Y | DB user account host name<br/>- Maximum length: `45` |
| authorityType | Enum | Y | DB user permission type<br/>- `CUSTOM`: Custom permission<br/>- `READ`: Read permission<br/>- `CRUD`: CRUD permission<br/>- `DDL`: DDL permission<br/>- `ALL`: All permissions |
| authenticationPlugin | Enum | N | User authentication plugin<br/>- `NATIVE`: mysql_native_password authentication<br/>- `CACHING_SHA2`: caching_sha2_password authentication (MySQL only)<br/>- `SHA256`: sha256_password authentication (MySQL only) |
| tlsOption | Enum | N | Certificate option<br/>- Default: `NONE`<br/>- `NONE`: TLS is not used<br/>- `SSL`: SSL authentication<br/>- `X509`: X509 certificate authentication |

<a id="create-db-user-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="delete-db-user"></a>
### Delete DB User { #delete-db-user }

<a id="delete-db-user-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceUser.Delete | Delete DB User |

<a id="delete-db-user-request"></a>
#### Request

```http
DELETE /v4.0/db-instances/{dbInstanceId}/db-users/{dbUserId}
```

<a id="delete-db-user-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| dbUserId | URL | UUID | Y | DB user identifier |

<a id="delete-db-user-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-db-user-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="modify-db-user"></a>
### Modify DB User { #modify-db-user }

<a id="modify-db-user-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceUser.Modify | Modify DB User |

<a id="modify-db-user-request"></a>
#### Request

```http
PUT /v4.0/db-instances/{dbInstanceId}/db-users/{dbUserId}
```

<a id="modify-db-user-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| dbUserId | URL | UUID | Y | DB user identifier |

<a id="modify-db-user-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "dbPassword": "dbPassword",
    "authorityType": "CUSTOM",
    "authenticationPlugin": "NATIVE",
    "tlsOption": "NONE"
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbPassword | String | N | DB user account password<br/>- Minimum length: `4`<br/>- Maximum length: `256` |
| authorityType | Enum | N | DB user permission type<br/>- `CUSTOM`: Custom permission<br/>- `READ`: Read permission<br/>- `CRUD`: CRUD permission<br/>- `DDL`: DDL permission<br/>- `ALL`: All permissions |
| authenticationPlugin | Enum | N | User authentication plugin<br/>- `NATIVE`: mysql_native_password authentication<br/>- `CACHING_SHA2`: caching_sha2_password authentication (MySQL only)<br/>- `SHA256`: sha256_password authentication (MySQL only) |
| tlsOption | Enum | N | Certificate option<br/>- `NONE`: TLS is not used<br/>- `SSL`: SSL authentication<br/>- `X509`: X509 certificate authentication |

<a id="modify-db-user-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="change-db-instance-deletion-protection-settings"></a>
### Change DB Instance Deletion Protection Settings { #change-db-instance-deletion-protection-settings }

<a id="change-db-instance-deletion-protection-settings-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Modify | Change DB Instance Deletion Protection Settings |

<a id="change-db-instance-deletion-protection-settings-request"></a>
#### Request

```http
PUT /v4.0/db-instances/{dbInstanceId}/deletion-protection
```

<a id="change-db-instance-deletion-protection-settings-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="change-db-instance-deletion-protection-settings-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "useDeletionProtection": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| useDeletionProtection | Boolean | Y | Whether to protect against deletion |

<a id="change-db-instance-deletion-protection-settings-response"></a>
#### Response

This API does not return a response body.

---

<a id="force-restart-db-instance"></a>
### Force Restart DB Instance { #force-restart-db-instance }

<a id="force-restart-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.ForceRestart | Force Restart DB instance |

<a id="force-restart-db-instance-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/force-restart
```

<a id="force-restart-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="force-restart-db-instance-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="force-restart-db-instance-response"></a>
#### Response

This API does not return a response body.

---

<a id="high-availability-status"></a>
### High Availability Status { #high-availability-status }

| Status                               | Description                              |
|----------------------------------|---------------------------------|
| `CREATED`                        | High availability has been created                    |
| `STABLE`                         | High availability is operating normally                    |
| `PAUSING`                        | High availability is being paused               |
| `PAUSED`                         | High availability has been paused                 |
| `PAUSED_DUE_TO_TASK`             | High availability has been paused due to a task         |
| `PAUSED_DUE_TO_STOP`             | When high availability is paused because the DB instance is stopped  |
| `DISABLE_MASTER_IN_REPLICATION`  | When high availability is suspended due to detection of abnormal replication on the primary     |
| `DISABLE_MHA_PROCESS`            | The high availability process has been stopped               |
| `DISABLE_REPLICATION_STOP`       | High availability has been disabled due to replication stoppage         |
| `DISABLE_REPLICATION_DELAY`      | High availability has been disabled due to replication delay         |
| `MASTER_FAILURE_DETECTION`       | When a primary failure is detected                  |
| `FAILOVER_STARTED`               | Failover has started                   |
| `FAILOVER_FAILED`                | Failover has failed                   |
| `FAILOVER_COMPLETED`             | Failover has been completed                   |
| `DELETED`                        | High availability has been deleted                    |

---

<a id="view-high-availability-information"></a>
### View High Availability Information { #view-high-availability-information }

<a id="view-high-availability-information-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Get | View High Availability Information |

<a id="view-high-availability-information-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/high-availability
```

<a id="view-high-availability-information-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="view-high-availability-information-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-high-availability-information-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| useHighAvailability | Boolean | Whether to use high availability<br/>- Default: `false` |
| haStatus | Enum | High availability status<br/>- `CREATED`: Created<br/>- `STABLE`: Normal<br/>- `PAUSING`: Pausing<br/>- `DISABLE`: Stopped<br/>- `DISABLE_MASTER_IN_REPLICATION`: High availability suspended due to detection of abnormal replication on the primary<br/>- `DISABLE_MHA_PROCESS`: High availability process suspended<br/>- `DISABLE_REPLICATION_STOP`: High availability suspended due to replication stop<br/>- `DISABLE_REPLICATION_DELAY`: High availability suspended due to replication delay<br/>- `FAILOVER_STARTED`: Failover started<br/>- `FAILOVER_FAILED`: Failover failed<br/>- `FAILOVER_COMPLETED`: Failover completed<br/>- `DELETED`: Deleted<br/>- `PAUSED`: Paused<br/>- `PAUSED_DUE_TO_TASK`: Paused due to a task<br/>- `PAUSED_DUE_TO_STOP`: Paused due to the DB instance being stopped<br/>- `MASTER_FAILURE_DETECTION`: Primary failure detected |
| pingInterval | Number | Ping interval (seconds) |
| pingType | Enum | Ping method<br/>- `CONNECTION`: CONNECTION method<br/>- `INSERT`: INSERT method<br/>- `SELECT`: SELECT method |

---

<a id="modify-high-availability"></a>
### Modify High Availability { #modify-high-availability }

<a id="modify-high-availability-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:HighAvailability.Modify | Modify high availability |

<a id="modify-high-availability-request"></a>
#### Request

```http
PUT /v4.0/db-instances/{dbInstanceId}/high-availability
```

<a id="modify-high-availability-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="modify-high-availability-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "useHighAvailability": false,
    "pingInterval": 1
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| useHighAvailability | Boolean | Y | Whether to use high availability |
| pingInterval | Number | N | Ping interval (sec) when using high availability<br/>- Minimum value: `1`<br/>- Maximum value: `600` |

<a id="modify-high-availability-section"></a>
#### When using high availability

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Name to identify the standby DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |

<a id="modify-high-availability-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="pause-high-availability"></a>
### Pause High Availability { #pause-high-availability }

<a id="pause-high-availability-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:HighAvailability.Pause | Pause high availability |

<a id="pause-high-availability-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/pause
```

<a id="pause-high-availability-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="pause-high-availability-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="pause-high-availability-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="recover-high-availability"></a>
### Recover High Availability { #recover-high-availability }

<a id="recover-high-availability-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:HighAvailability.Repair | Recover high availability |

<a id="recover-high-availability-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/repair
```

<a id="recover-high-availability-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="recover-high-availability-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="recover-high-availability-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="restart-high-availability"></a>
### Restart High Availability { #restart-high-availability }

<a id="restart-high-availability-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:HighAvailability.Resume | Restart high availability |

<a id="restart-high-availability-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/resume
```

<a id="restart-high-availability-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="restart-high-availability-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="restart-high-availability-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="separate-high-availability"></a>
### Separate High Availability { #separate-high-availability }

<a id="separate-high-availability-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:HighAvailability.Split | Separate high availability |

<a id="separate-high-availability-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/split
```

<a id="separate-high-availability-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="separate-high-availability-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="separate-high-availability-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="list-log-files"></a>
### List Log Files { #list-log-files }

<a id="list-log-files-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceLog.List | List Log Files |

<a id="list-log-files-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/log-files
```

<a id="list-log-files-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| logFileTypes | Query | Array | N | Log file type list |

<a id="list-log-files-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-log-files-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| logFiles | Array | Log File list |
| logFiles.logFileName | String | Log File name |
| logFiles.logFileType | Enum | Log file type<br/>- `ERROR`<br/>- `BINLOG`<br/>- `GENERAL`<br/>- `SLOW_QUERY`<br/>- `AUDIT`<br/>- `BACKUP` |
| logFiles.logFileSize | Number | Log File size(Byte) |
| logFiles.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="export-log-file"></a>
### Export Log File { #export-log-file }

<a id="export-log-file-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceLog.Export | Export Log File |

<a id="export-log-file-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/log-files/export
```

<a id="export-log-file-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="export-log-file-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| logFileNames | Array | Y | Log File name list |
| tenantId | String | Y | Tenant ID of the Object Storage where the log file will be saved<br/>- Minimum length: `32`<br/>- Maximum length: `32` |
| username | String | Y | NHN Cloud member or IAM account ID |
| password | String | Y | API password of the Object Storage where the log file will be saved |
| targetContainer | String | Y | Container of the Object Storage where the log file will be saved |
| objectPath | String | Y | Log file path to be stored in container |

<a id="export-log-file-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="view-log-file-contents"></a>
### View Log File Contents { #view-log-file-contents }

<a id="view-log-file-contents-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstanceLog.Get | View Log File Contents |

<a id="view-log-file-contents-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/log-files/{logFileName}
```

<a id="view-log-file-contents-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| logFileName | URL | UUID | Y | Log File name |
| logFileType | Query | Enum | Y | Log file type<br/>- `ERROR`<br/>- `BINLOG`<br/>- `GENERAL`<br/>- `SLOW_QUERY`<br/>- `AUDIT`<br/>- `BACKUP` |

<a id="view-log-file-contents-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-log-file-contents-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| content | String | Log file contents (up to 65533 bytes) |

---

<a id="get-maintenances"></a>
### List DB Instance Maintenances { #get-maintenances }

<a id="get-maintenances-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Maintenance.List | List DB Instance Maintenances |

<a id="get-maintenances-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/maintenances
```

<a id="get-maintenances-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| type | Query | String | N |  |
| statuses | Query | String | N |  |
| category | Query | String | N |  |

<a id="get-maintenances-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-maintenances-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| totalCounts | Number | Number of maintenance items |
| maintenances | Array | Maintenance list |
| maintenances.maintenanceId | UUID | Maintenance ID |
| maintenances.dbInstanceId | UUID | DB instance ID |
| maintenances.category | Enum | Maintenance category<br/>- `USER`: User maintenance category<br/>- `PROVIDER`: Provider maintenance category<br/>- `AUTO`: Automatic maintenance category |
| maintenances.description | String | Maintenance description |
| maintenances.type | Enum | Maintenance type<br/>- `UPDATE_DB_INSTANCE`: Modify DB instance (change specifications, change port, change parameter group)<br/>- `UPGRADE_ENGINE_VERSION`: Upgrade engine version<br/>- `APPLY_CHANGE_PARAMETER`: Change parameters of the parameter group<br/>- `UPGRADE_OS`: Upgrade OS version<br/>- `PATCH_SECURITY`: Security update<br/>- `MIGRATION`: Migration for hypervisor maintenance<br/>- `CLEANUP_STORAGE`: Storage cleanup |
| maintenances.payload | Object | Payload according to the maintenance type |
| maintenances.required | Boolean | Whether maintenance is mandatory |
| maintenances.deadlineYmdt | DateTime | Maintenance forced application date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| maintenances.status | Enum | Maintenance status<br/>- `PENDING`: Pending<br/>- `READY`: Ready<br/>- `RUNNING`: Running<br/>- `COMPLETED`: Completed<br/>- `FAILED`: Failed<br/>- `EXCLUDED`: Excluded<br/>- `DELETED`: Deleted<br/>- `SUSPENDED`: Suspended<br/>- `UNKNOWN` |
| maintenances.executionType | Enum | Maintenance execution type<br/>- `SCHEDULED`: Scheduled execution (automatic execution during the maintenance window)<br/>- `MANUAL`: Manual execution (immediate execution)<br/>- `FORCED`: Forced execution (automatic execution after the deadline is exceeded) |
| maintenances.addedYmdt | DateTime | Maintenance schedule registered date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| maintenances.executionStartedYmdt | DateTime | Maintenance start date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| maintenances.executionCompletedYmdt | DateTime | Maintenance end date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| maintenances.haPairSynced | Boolean | Whether the HA pair is synchronized |

---

<a id="execute-maintenance-now"></a>
### Execute DB Instance Maintenance Now { #execute-maintenance-now }

<a id="execute-maintenance-now-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Maintenance.Execute | Execute DB Instance Maintenance Now |

<a id="execute-maintenance-now-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/maintenances/execute-now
```

<a id="execute-maintenance-now-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="execute-maintenance-now-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| configId | String | Y | Setting ID |
| category | Enum | Y | Maintenance category<br/>- `USER`: User maintenance category<br/>- `PROVIDER`: Provider maintenance category<br/>- `AUTO`: Automatic maintenance category |
| description | String | N | Maintenance description |
| type | Enum | Y | Maintenance type<br/>- `UPDATE_DB_INSTANCE`: Modify DB instance (change specifications, change port, change parameter group)<br/>- `UPGRADE_ENGINE_VERSION`: Upgrade engine version<br/>- `APPLY_CHANGE_PARAMETER`: Change parameters of the parameter group<br/>- `UPGRADE_OS`: Upgrade OS version<br/>- `PATCH_SECURITY`: Security update<br/>- `MIGRATION`: Migration for hypervisor maintenance<br/>- `CLEANUP_STORAGE`: Storage cleanup |
| payload | String | Y | Payload according to the maintenance type |

<a id="execute-maintenance-now-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="schedule-maintenance"></a>
### Schedule DB Instance Maintenance { #schedule-maintenance }

<a id="schedule-maintenance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Maintenance.Update | Schedule DB Instance Maintenance |

<a id="schedule-maintenance-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/maintenances/schedule
```

<a id="schedule-maintenance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="schedule-maintenance-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| configId | String | Y | Setting ID |
| category | Enum | Y | Maintenance category<br/>- `USER`: User maintenance category<br/>- `PROVIDER`: Provider maintenance category<br/>- `AUTO`: Automatic maintenance category |
| description | String | N | Maintenance description |
| type | Enum | Y | Maintenance type<br/>- `UPDATE_DB_INSTANCE`: Modify DB instance (change specifications, change port, change parameter group)<br/>- `UPGRADE_ENGINE_VERSION`: Upgrade engine version<br/>- `APPLY_CHANGE_PARAMETER`: Change parameters of the parameter group<br/>- `UPGRADE_OS`: Upgrade OS version<br/>- `PATCH_SECURITY`: Security update<br/>- `MIGRATION`: Migration for hypervisor maintenance<br/>- `CLEANUP_STORAGE`: Storage cleanup |
| payload | String | Y | Payload according to the maintenance type |

<a id="schedule-maintenance-response"></a>
#### Response

This API does not return a response body.

---

<a id="delete-maintenance"></a>
### Delete DB Instance Maintenance { #delete-maintenance }

<a id="delete-maintenance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Maintenance.Delete | Delete DB Instance Maintenance |

<a id="delete-maintenance-request"></a>
#### Request

```http
DELETE /v4.0/db-instances/{dbInstanceId}/maintenances/{maintenanceId}
```

<a id="delete-maintenance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| maintenanceId | URL | UUID | Y | Maintenance ID |

<a id="delete-maintenance-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-maintenance-response"></a>
#### Response

This API does not return a response body.

---

<a id="list-network-information"></a>
### List Network Information { #list-network-information }

<a id="list-network-information-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Get | List Network Information |

<a id="list-network-information-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/network-info
```

<a id="list-network-information-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="list-network-information-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-network-information-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| availabilityZone | String | Availability zone where DB instance will be created |
| subnet | Object | Subnet object |
| subnet.subnetId | UUID | Subnet identifier |
| subnet.subnetName | String | Name to identify subnets |
| subnet.subnetCidr | String | CIDR of subnet |
| endPoints | Array | List of access information |
| endPoints.domain | String | Domain |
| endPoints.ipAddress | String | IP address |
| endPoints.endPointType | String | Connection information type |

---

<a id="modify-network-information"></a>
### Modify Network Information { #modify-network-information }

<a id="modify-network-information-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Modify | Modify Network Information |

<a id="modify-network-information-request"></a>
#### Request

```http
PUT /v4.0/db-instances/{dbInstanceId}/network-info
```

<a id="modify-network-information-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="modify-network-information-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "usePublicAccess": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| usePublicAccess | Boolean | Y | External access is available or not |

<a id="modify-network-information-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="promote-db-instance"></a>
### Promote DB Instance { #promote-db-instance }

<a id="promote-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Promote | Promote DB Instance |

<a id="promote-db-instance-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/promote
```

<a id="promote-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="promote-db-instance-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="promote-db-instance-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="rebuild-db-instance"></a>
### Rebuild DB Instance { #rebuild-db-instance }

<a id="rebuild-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Rebuild | Rebuild DB Instance |

<a id="rebuild-db-instance-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/rebuild
```

<a id="rebuild-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="rebuild-db-instance-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="rebuild-db-instance-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="replicate-db-instance"></a>
### Replicate DB Instance { #replicate-db-instance }

<a id="replicate-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Replicate | Replicate DB Instance |

<a id="replicate-db-instance-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/replicate
```

<a id="replicate-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="replicate-db-instance-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Name to identify the primary DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB instance<br/>- Maximum length: `100` |
| dbFlavorId | UUID | N | Identifier of DB instance specifications |
| dbPort | Number | N | DB port<br/>- Minimum value: 3306, Maximum value: 43306 |
| parameterGroupId | UUID | N | Parameter group identifier |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| userGroupIds | Array | N | User group identifiers |
| useDefaultNotification | Boolean | N | Whether to use default notification<br/>- Default: `false` |
| useDeletionProtection | Boolean | N | Whether to protect against deletion<br/>- Default: `false` |
| useSlowQueryAnalysis | Boolean | N | Whether to analyze slow queries<br/>- Default: `true` |
| network | Object | Y | Network information objects |
| network.usePublicAccess | Boolean | N | External access is available or not |
| network.availabilityZone | Enum | Y | Availability zone where DB instance will be created |
| storage | Object | N | Storage information object |
| storage.storageType | Enum | N | Data storage type |
| storage.storageSize | Number | N | Block Storage Size (GB)<br/>- Minimum value: `20` |
| storage.storageAutoscale | Object | N | Block Storage Auto Scaling Objects |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | Whether to enable storage auto scaling<br/>- Default: `false` |
| backup | Object | N | Backup information objects |
| backup.backupPeriod | Number | N | Backup retention period<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR1`: Korea (Pangyo) |
| backup.useBackupLock | Boolean | N | Whether to use table lock |
| backup.backupSchedules | Array | N | Backup schedule list |
| backup.backupSchedules.backupWndBgnTime | Time | N | Backup start time |
| backup.backupSchedules.backupWndDuration | Enum | N | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |

<a id="replicate-db-instance-section"></a>
#### When using storage auto scaling

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | Auto scale out conditions (%)<br/>- Minimum value: `50`<br/>- Maximum value: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | Auto scaling maximum size (GB)<br/>- Maximum value: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | Auto scaling cooldown time (minutes)<br/>- Minimum value: `10`<br/>- Maximum value: `1440` |

<a id="replicate-db-instance-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="restart-db-instance"></a>
### Restart DB Instance { #restart-db-instance }

<a id="restart-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Restart | Restart DB Instance |

<a id="restart-db-instance-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/restart
```

<a id="restart-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="restart-db-instance-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| useOnlineFailover | Boolean | N | Whether to restart using failover<br/>- Default: `false` |
| executeBackup | Boolean | N | Whether to perform a backup at the current point in time<br/>- Default: `false` |
| waitReplicationDelay | Boolean | N | Wait for replication delay to be resolved<br/>- Default: `false` |
| useReadOnly | Boolean | N | Block write load<br/>- Default: `false` |
| osRestart | Boolean | N | Whether to restart the OS<br/>- Default: `false` |

<a id="restart-db-instance-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="view-restoration-information"></a>
### View Restoration Information { #view-restoration-information }

<a id="view-restoration-information-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Get | View Restoration Information |

<a id="view-restoration-information-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/restoration-info
```

<a id="view-restoration-information-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="view-restoration-information-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-restoration-information-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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
                "dbVersion": "MYSQL_V8411",
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

| Name | Format | Description |
|-----|-----|-----|
| oldestRestorableYmdt | DateTime | Earliest restorable time |
| latestRestorableYmdt | DateTime | Latest restorable time |
| restorableBackups | Array | List of restorable backups |
| restorableBackups.backup | Object | Backup information objects |
| restorableBackups.backup.backupId | UUID | Backup identifier |
| restorableBackups.backup.backupName | String | Backup name |
| restorableBackups.backup.backupStatus | Enum | Backup Status<br/>- `BACKING_UP`: Backup in progress<br/>- `COMPLETED`: Backup completed<br/>- `DELETING`: Backup being deleted<br/>- `DELETED`: Backup deleted<br/>- `ERROR`: Error occurred |
| restorableBackups.backup.dbInstanceId | UUID | Original DB instance identifier |
| restorableBackups.backup.dbInstanceName | String | Original DB instance name |
| restorableBackups.backup.dbVersion | Enum | DB engine version |
| restorableBackups.backup.backupType | Enum | Backup type<br/>- `AUTO`<br/>- `MANUAL` |
| restorableBackups.backup.backupSize | Number | Backup size |
| restorableBackups.backup.useBackupLock | Boolean | Whether to use table lock |
| restorableBackups.backup.failoverCount | Number | Number of failovers |
| restorableBackups.backup.binLogFileName | String | Binary log file name |
| restorableBackups.backup.binLogPosition | Number | Binary log file location |
| restorableBackups.backup.createdYmdt | DateTime | Backup created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| restorableBackups.backup.updatedYmdt | DateTime | Backup updated date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| restorableBackups.restorableBinLogs | Array | Binary log names that can be restored using the backup |

---

<a id="view-the-last-query-to-be-restored"></a>
### View the Last Query to Be Restored { #view-the-last-query-to-be-restored }

<a id="view-the-last-query-to-be-restored-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Get | View the Last Query to Be Restored |

<a id="view-the-last-query-to-be-restored-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/restoration-info/last-query
```

<a id="view-the-last-query-to-be-restored-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| restoreType | Query | Enum | Y | Restoration type<br/>- `TIMESTAMP`: Point-in-time restoration using a time within the restorable period<br/>- `BINLOG`: Point-in-time restoration using a restorable binary log position |

<a id="view-the-last-query-to-be-restored-restoretype-timestamp"></a>
#### If restoreType is `TIMESTAMP`

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| restoreYmdt | Query | DateTime | Y | DB instance restore date (YYYY-MM-DDThh:mm:ss.SSSTZD) |

<a id="view-the-last-query-to-be-restored-restoretype-binlog"></a>
#### If restoreType is `BINLOG`

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| backupId | Query | UUID | Y | Identifier of the backup to use for restoration |
| binLogFileName | Query | String | Y | Binary log name to use for restoration |
| binLogPosition | Query | String | Y | Binary log location to use for restoration |

<a id="view-the-last-query-to-be-restored-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-the-last-query-to-be-restored-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| executedYmdt | DateTime | Query executed date (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| lastQuery | String | Last executed query |

---

<a id="restoration"></a>
### Restoration { #restoration }

<a id="restoration-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Restore | Restoration |

<a id="restoration-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/restore
```

<a id="restoration-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="restoration-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Name to identify the primary DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB instance<br/>- Maximum length: `100` |
| dbFlavorId | UUID | N | Identifier of DB instance specifications. If not entered, the specifications of the original instance are applied. |
| dbPort | Number | N | DB port |
| useHighAvailability | Boolean | N | Whether to use high availability<br/>- Default: `false` |
| pingInterval | Number | N | Ping interval (sec) when using high availability<br/>- Minimum value: `1`<br/>- Maximum value: `600` |
| storage | Object | N | Storage information object. If not entered, the storage settings of the original instance are applied. |
| storage.storageType | Enum | N | Storage type. If not entered, the storage type of the original instance is applied. |
| storage.storageSize | Number | N | Data storage size (GB). If not entered, the storage size of the original instance is applied.<br/>- Minimum value: `20` |
| storage.storageAutoscale | Object | N | Block Storage Auto Scaling Objects |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | Whether to enable storage auto scaling<br/>- Default: `false` |
| network | Object | N | Network information object. If not entered, the network settings of the original instance are applied. |
| network.subnetId | UUID | N | Subnet identifier. If not entered, the value of the original instance is used. |
| network.usePublicAccess | Boolean | N | External access is available or not<br/>- Default: `false` |
| network.availabilityZone | Enum | N | Availability zone where DB instance will be created. If not entered, it is selected at random. |
| backup | Object | N | Backup information object. If not entered, the backup settings of the original instance are applied. |
| backup.backupPeriod | Number | N | Backup retention period (days). If not entered, the backup retention period of the original instance is applied.<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR1`: Korea (Pangyo) |
| backup.useBackupLock | Boolean | N | Whether to use table lock<br/>- Default: `true` |
| backup.backupSchedules | Array | N | Backup schedule list. If not entered, the backup schedule of the original instance is applied. |
| backup.backupSchedules.backupWndBgnTime | Time | N | Backup start time |
| backup.backupSchedules.backupWndDuration | Enum | N | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |
| restore | Object | Y | Restoration information object |
| restore.restoreType | Enum | Y | Restoration type<br/>- `TIMESTAMP`: Point-in-time restoration using a time within the restorable period<br/>- `BINLOG`: Point-in-time restoration using a restorable binary log position<br/>- `BACKUP`: Snapshot restoration using a previously created backup |
| useDefaultNotification | Boolean | N | Whether to use default notification<br/>- Default: `false` |
| useSlowQueryAnalysis | Boolean | N | Whether to analyze slow queries<br/>- Default: `true` |
| parameterGroupId | UUID | N | Parameter group identifier. If not entered, the parameter group of the original instance is applied. |
| dbSecurityGroupIds | Array | N | DB security group identifiers. If not entered, the security groups of the original instance are applied. |
| userGroupIds | Array | N | User group identifiers |
| useDeletionProtection | Boolean | N | Whether to protect against deletion<br/>- Default: `false` |

<a id="restoration-section"></a>
#### When using high availability

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Name to identify the standby DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |

<a id="restoration-section-2"></a>
#### When using storage auto scaling

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | Auto scale out conditions (%)<br/>- Minimum value: `50`<br/>- Maximum value: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | Auto scaling maximum size (GB)<br/>- Maximum value: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | Auto scaling cooldown time (minutes)<br/>- Minimum value: `10`<br/>- Maximum value: `1440` |

<a id="restoration-timestamp-restoretype-timestamp"></a>
#### Request when restoring a point in time restoration using Timestamp (if restoreType is `TIMESTAMP`)

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| restore.restoreYmdt | DateTime | N | DB instance restore date (YYYY-MM-DDThh:mm:ss.SSSTZD) |

You can only restore to a point in time earlier than the latest restorable time confirmed by querying the restoration information.

<a id="restoration-restoretype-binlog"></a>
#### Request for point-in-time restoration using binary logs (if restoreType is `BINLOG`)

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| restore.backupId | UUID | N | Identifier of the backup to use for restoration |
| restore.binLog | Object | N | Binary log information object to use for restoration |
| restore.binLog.binLogFileName | String | N | Binary log name to use for restoration |
| restore.binLog.binLogPosition | Number | N | Binary log location to use for restoration |

For point-in-time restoration using binary logs, you can restore the logs recorded after the binary log file and position of the reference backup.

<a id="restoration-restoretype-backup"></a>
#### Request when restoring from backup (if restoreType is `BACKUP`)

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| restore.backupId | UUID | N | Identifier of the backup to use for restoration |

<a id="restoration-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="start-db-instance"></a>
### Start DB Instance { #start-db-instance }

<a id="start-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Start | Start DB Instance |

<a id="start-db-instance-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/start
```

<a id="start-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="start-db-instance-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="start-db-instance-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="stop-db-instance"></a>
### Stop DB Instance { #stop-db-instance }

<a id="stop-db-instance-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Stop | Stop DB Instance |

<a id="stop-db-instance-request"></a>
#### Request

```http
POST /v4.0/db-instances/{dbInstanceId}/stop
```

<a id="stop-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="stop-db-instance-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="stop-db-instance-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="view-storage-information"></a>
### View Storage Information { #view-storage-information }

<a id="view-storage-information-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Get | View Storage Information |

<a id="view-storage-information-request"></a>
#### Request

```http
GET /v4.0/db-instances/{dbInstanceId}/storage-info
```

<a id="view-storage-information-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="view-storage-information-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-storage-information-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| storageType | String | Data storage type |
| storageSize | Number | Block Storage Size (GB) |
| storageStatus | Enum | Data Storage Current Status<br/>- `DELETED`: Deleted<br/>- `PENDING_DELETION`: Deletion pending<br/>- `DELETION_RESERVED`: Deletion reserved (waiting for snapshot cleanup)<br/>- `DETACHED`: Detached<br/>- `ATTACHED`: Attached |
| storageAutoscale | Object | Block Storage Auto Scaling Objects |
| storageAutoscale.useStorageAutoscale | Boolean | Whether to enable storage auto scaling |
| storageAutoscale.threshold | Number | Auto scale out conditions (%) |
| storageAutoscale.maxStorageSize | Number | Auto scaling maximum size (GB) |
| storageAutoscale.cooldownTime | Number | Auto scaling cooldown time (minutes) |

---

<a id="modify-storage-information"></a>
### Modify Storage Information { #modify-storage-information }

<a id="modify-storage-information-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbInstance.Modify | Modify Storage Information |

<a id="modify-storage-information-request"></a>
#### Request

```http
PUT /v4.0/db-instances/{dbInstanceId}/storage-info
```

<a id="modify-storage-information-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="modify-storage-information-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "storageSize": 1,
    "storageAutoscale": {
        "useStorageAutoscale": false
    }
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| storageSize | Number | Y | Block Storage Size (GB)<br/>- Maximum value: `2048` |
| storageAutoscale | Object | N | Block Storage Auto Scaling Objects |
| storageAutoscale.useStorageAutoscale | Boolean | N | Whether to enable storage auto scaling |

<a id="modify-storage-information-section"></a>
#### When using storage auto scaling

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| storageAutoscale.threshold | Number | Y | Auto scale out conditions (%)<br/>- Minimum value: `50`<br/>- Maximum value: `95` |
| storageAutoscale.maxStorageSize | Number | Y | Auto scaling maximum size (GB)<br/>- Maximum value: `4096` |
| storageAutoscale.cooldownTime | Number | Y | Auto scaling cooldown time (minutes)<br/>- Minimum value: `10`<br/>- Maximum value: `1440` |

<a id="modify-storage-information-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="backups"></a>
## Backups { #backups }

<a id="backup-status"></a>
### Backup Status { #backup-status }

| Status           | Description           |
|--------------|--------------|
| `BACKING_UP` | Backup in progress     |
| `COMPLETED`  | Backup is completed   |
| `DELETING`   | Backup is being deleted |
| `DELETED`    | Backup is deleted   |
| `ERROR`      | Error occurred   |

<a id="retrieve-backup-list"></a>
### Retrieve Backup List { #retrieve-backup-list }

<a id="retrieve-backup-list-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Backup.List | Retrieve Backup List |

<a id="retrieve-backup-list-request"></a>
#### Request

```http
GET /v4.0/backups
```

<a id="retrieve-backup-list-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| backupType | Query | Enum | N | Backup type<br/>- `AUTO`<br/>- `MANUAL` |
| dbInstanceId | Query | UUID | N | Original DB instance identifier |
| dbVersion | Query | Enum | N | DB engine version |
| page | Query | Number | N | Page of the list to query (default: 1)<br/>- Minimum value: `1` |
| size | Query | Number | N | Page size of the list to query (default: 20)<br/>- Minimum value: `1`<br/>- Maximum value: `100` |

<a id="retrieve-backup-list-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="retrieve-backup-list-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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
            "dbVersion": "MYSQL_V8411",
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

| Name | Format | Description |
|-----|-----|-----|
| totalCounts | Number | Number of all backup lists |
| backups | Array | Backup list |
| backups.backupId | UUID | Backup identifier |
| backups.backupName | String | Name to identify backups |
| backups.backupStatus | Enum | Backup current status<br/>- `BACKING_UP`: Backup in progress<br/>- `COMPLETED`: Backup completed<br/>- `DELETING`: Backup being deleted<br/>- `DELETED`: Backup deleted<br/>- `ERROR`: Error occurred |
| backups.dbInstanceId | UUID | Original DB instance identifier |
| backups.dbVersion | Enum | DB engine version |
| backups.utilVersion | String | Utility version |
| backups.backupType | Enum | Backup type<br/>- `AUTO`<br/>- `MANUAL` |
| backups.backupSize | Number | Backup size (bytes) |
| backups.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| backups.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-backup"></a>
### Create Backup { #create-backup }

<a id="create-backup-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Backup.Create | Create backup |

<a id="create-backup-request"></a>
#### Request

```http
POST /v4.0/backups
```

<a id="create-backup-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "backupName": "backupName",
    "backupMethodType": "FULL"
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| backupName | String | Y | Name to identify backups<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| backupMethodType | Enum | Y | Backup method type<br/>- `FULL`: Full backup<br/>- `INCREMENTAL`: Incremental backup<br/>- `SNAPSHOT`: Snapshot backup |

<a id="create-backup-backupmethodtype-incremental"></a>
#### If backupMethodType is `INCREMENTAL`

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| baseBackupId | UUID | Y | Identifier of the original backup |

<a id="create-backup-backupmethodtype-full"></a>
#### If backupMethodType is `FULL`

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceId | UUID | Y | DB instance identifier |

<a id="create-backup-backupmethodtype-snapshot"></a>
#### Snapshot Backup (if backupMethodType is `SNAPSHOT`)

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceId | UUID | Y | DB instance identifier |

<a id="create-backup-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="delete-backup"></a>
### Delete Backup { #delete-backup }

<a id="delete-backup-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Backup.Delete | Delete backup |

<a id="delete-backup-request"></a>
#### Request

```http
DELETE /v4.0/backups/{backupId}
```

<a id="delete-backup-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| backupId | URL | UUID | Y | Backup identifier |

<a id="delete-backup-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-backup-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="view-backup-details"></a>
### View Backup Details { #view-backup-details }

<a id="view-backup-details-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Backup.Get | View Backup Details |

<a id="view-backup-details-request"></a>
#### Request

```http
GET /v4.0/backups/{backupId}
```

<a id="view-backup-details-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| backupId | URL | UUID | Y | Backup identifier |

<a id="view-backup-details-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-backup-details-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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
        "dbVersion": "MYSQL_V8411",
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

| Name | Format | Description |
|-----|-----|-----|
| backup | Object | Backup details |
| backup.backupId | UUID | Backup identifier |
| backup.regionCode | Enum | Region code<br/>- `KR1`: Korea (Pangyo) |
| backup.backupName | String | Name to identify backups |
| backup.backupStatus | Enum | Backup current status<br/>- `BACKING_UP`: Backing up (spinner)<br/>- `VERIFYING`: Verifying (spinner)<br/>- `COMPLETED`: Available (green icon)<br/>- `DELETING`: Deleting (spinner)<br/>- `DELETED`: Deleted (gray icon)<br/>- `ERROR`: Error (red icon) |
| backup.dbInstanceId | UUID | Original DB instance identifier |
| backup.dbInstanceName | String | Original DB instance name |
| backup.dbVersion | Enum | DB engine version |
| backup.utilVersion | String | Utility version |
| backup.backupType | Enum | Backup type (AUTO, MANUAL)<br/>- `AUTO`<br/>- `MANUAL` |
| backup.backupMethodType | Enum | Backup method (FULL, SNAPSHOT, INCREMENTAL)<br/>- `FULL`<br/>- `INCREMENTAL`<br/>- `SNAPSHOT` |
| backup.backupFileType | Enum | Backup file type<br/>- `XBSTREAM`<br/>- `TAR_ZSTD`<br/>- `TAR_LZ4`<br/>- `TAR_GZIP`<br/>- `SNAPSHOT` |
| backup.backupSize | Number | Backup size (bytes) |
| backup.isReplicable | Boolean | Replicable |
| backup.binLogFileName | String | Binary log file name |
| backup.binLogPosition | Number | Binary log location |
| backup.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| backup.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="export-backup"></a>
### Export Backup { #export-backup }

<a id="export-backup-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Backup.Export | Export backup |

<a id="export-backup-request"></a>
#### Request

```http
POST /v4.0/backups/{backupId}/export
```

<a id="export-backup-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| backupId | URL | UUID | Y | Backup identifier |

<a id="export-backup-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| tenantId | String | Y | Tenant ID of the Object Storage where the backup will be saved<br/>- Minimum length: `32`<br/>- Maximum length: `32` |
| username | String | Y | NHN Cloud member or IAM member ID |
| password | String | Y | API password of the Object Storage where the backup will be saved |
| targetContainer | String | Y | Container of the Object Storage where the backup will be saved |
| objectPath | String | Y | Backup path to be stored in container |

<a id="export-backup-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="restore-backup"></a>
### Restore Backup { #restore-backup }

<a id="restore-backup-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Backup.Restore | Restore backup |

<a id="restore-backup-request"></a>
#### Request

```http
POST /v4.0/backups/{backupId}/restore
```

<a id="restore-backup-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| backupId | URL | UUID | Y | Backup identifier |

<a id="restore-backup-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceName | String | Y | Name to identify the primary DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB instance<br/>- Maximum length: `100` |
| dbFlavorId | UUID | N | Identifier of DB instance specifications. If not specified, the value of the original instance is used. |
| dbPort | Number | N | DB port. If not specified, the value of the original instance is used.<br/>- Minimum value: 3306, Maximum value: 43306 |
| parameterGroupId | UUID | N | Parameter group identifier. If not specified, the value of the original instance is used. |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| userGroupIds | Array | N | User group identifiers |
| useHighAvailability | Boolean | N | Whether to use high availability<br/>- Default: `false` |
| pingInterval | Number | N | Ping interval (sec) when using high availability<br/>- Default: `3`<br/>- Minimum value: `1`<br/>- Maximum value: `600` |
| useDefaultNotification | Boolean | N | Whether to use default notification<br/>- Default: `false` |
| useDeletionProtection | Boolean | N | Whether to protect against deletion<br/>- Default: `false` |
| useSlowQueryAnalysis | Boolean | N | Whether to analyze slow queries<br/>- Default: `true` |
| network | Object | N | Network information object. If not specified, the value of the original instance is used. |
| network.subnetId | UUID | N | Subnet identifier. If not specified, the value of the original instance is used. |
| network.usePublicAccess | Boolean | N | External access is available or not<br/>- Default: `false` |
| network.availabilityZone | Enum | N | Availability zone where DB instance will be created. If not specified, it is selected at random. |
| storage | Object | N | Storage information object. If not specified, the value of the original instance is used. |
| storage.storageType | Enum | N | Storage type. If not specified, the value of the original instance is used. |
| storage.storageSize | Number | N | Data storage size (GB). If not specified, the value of the original instance is used.<br/>- Minimum value: `20` |
| storage.storageAutoscale | Object | N | Data storage auto scaling object. If not specified, the value of the original instance is used. |
| storage.storageAutoscale.useStorageAutoscale | Boolean | N | Whether to enable storage auto scaling<br/>- Default: `false` |
| backup | Object | N | Backup information object. If not specified, the backup settings of the original instance are used. |
| backup.backupPeriod | Number | N | Backup retention period (days). If not specified, the value of the original instance is used.<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.backupRetryCount | Number | N | Number of backup retries. If not specified, the value of the original instance is used.<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec). If not specified, the value of the original instance is used.<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR1`: Korea (Pangyo) |
| backup.useBackupLock | Boolean | N | Whether to use table lock. If not specified, the value of the original instance is used. |
| backup.backupSchedules | Array | N | Backup schedule list. If not specified, the value of the original instance is used. |
| backup.backupSchedules.backupWndBgnTime | Time | Y | Backup start time |
| backup.backupSchedules.backupWndDuration | Enum | Y | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |

<a id="restore-backup-section"></a>
#### When using high availability

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceCandidateName | String | Y | Name to identify the standby DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |

<a id="restore-backup-section-2"></a>
#### When using storage auto scaling

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| storage.storageAutoscale.threshold | Number | Y | Auto scale out conditions (%)<br/>- Minimum value: `50`<br/>- Maximum value: `95` |
| storage.storageAutoscale.maxStorageSize | Number | Y | Auto scaling maximum size (GB)<br/>- Maximum value: `4096` |
| storage.storageAutoscale.cooldownTime | Number | Y | Auto scaling cooldown time (minutes)<br/>- Minimum value: `10`<br/>- Maximum value: `1440` |

<a id="restore-backup-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Identifier of requested task |

---

<a id="db-security-group"></a>
## DB Security Group { #db-security-group }

<a id="db-security-group-progress-status"></a>
### DB Security Group Progress { #db-security-group-progress-status }

| Status              | Description           |
|-----------------|--------------|
| `NONE`          | No task in progress |
| `CREATING_RULE` | Creating rules   |
| `UPDATING_RULE` | Modifying rules   |
| `DELETING_RULE` | Deleting rules   |

<a id="list-db-security-groups"></a>
### List DB Security Groups { #list-db-security-groups }

<a id="list-db-security-groups-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbSecurityGroup.List | List DB security groups |

<a id="list-db-security-groups-request"></a>
#### Request

```http
GET /v4.0/db-security-groups
```

<a id="list-db-security-groups-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| page | Query | Number | N | Page of the list to query (default: 1)<br/>- Minimum value: `1` |
| size | Query | Number | N | Page size of the list to query (default: 20)<br/>- Minimum value: `1`<br/>- Maximum value: `100` |

<a id="list-db-security-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-security-groups-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| totalCounts | Number | Total number of DB security groups |
| dbSecurityGroups | Array | DB security groups |
| dbSecurityGroups.dbSecurityGroupId | UUID | DB security group identifier |
| dbSecurityGroups.dbSecurityGroupName | String | Name to identify DB security groups |
| dbSecurityGroups.description | String | Additional information of DB security group |
| dbSecurityGroups.progressStatus | Enum | Current status of DB security group<br/>- `NONE`: None<br/>- `CREATING_RULE`: Creating rule<br/>- `UPDATING_RULE`: Modifying rule<br/>- `DELETING_RULE`: Deleting rule<br/>- `APPLYING_DEFAULT_RULE`: Applying default rule |
| dbSecurityGroups.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbSecurityGroups.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-db-security-group"></a>
### Create DB Security Group { #create-db-security-group }

<a id="create-db-security-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbSecurityGroup.Create | Create DB security group |

<a id="create-db-security-group-request"></a>
#### Request

```http
POST /v4.0/db-security-groups
```

<a id="create-db-security-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbSecurityGroupName | String | Y | Name to identify DB security groups<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB security group<br/>- Maximum length: `100` |
| rules | Array | Y | DB security group rules |
| rules.direction | Enum | Y | Communication direction<br/>- `INGRESS`: Inbound<br/>- `EGRESS`: Outbound |
| rules.etherType | Enum | Y | Ether type<br/>- `IPV4`: IPv4 format<br/>- `IPV6`: IPv6 format |
| rules.port | Object | Y | Port object |
| rules.port.portType | Enum | Y | Port type<br/>- `ALL`: Entire port range (not used in the user console)<br/>- `PORT`: Specific port<br/>- `DB_PORT`: DB listening port<br/>- `PORT_RANGE`: Port range |
| rules.port.minPort | Number | N | Minimum value of port range<br/>- Minimum value: `3306` |
| rules.port.maxPort | Number | N | Maximum value of port range<br/>- Maximum value: `65535` |
| rules.cidr | String | Y | CIDR |
| rules.description | String | N | Additional information of security group rule |

<a id="create-db-security-group-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| dbSecurityGroupId | UUID | DB security group identifier |

---

<a id="delete-db-security-group"></a>
### Delete DB Security Group { #delete-db-security-group }

<a id="delete-db-security-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbSecurityGroup.Delete | Delete DB security group |

<a id="delete-db-security-group-request"></a>
#### Request

```http
DELETE /v4.0/db-security-groups/{dbSecurityGroupId}
```

<a id="delete-db-security-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DB security group identifier |

<a id="delete-db-security-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-db-security-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="list-db-security-group-details"></a>
### List DB Security Group Details { #list-db-security-group-details }

<a id="list-db-security-group-details-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbSecurityGroup.Get | List DB Security Group Details |

<a id="list-db-security-group-details-request"></a>
#### Request

```http
GET /v4.0/db-security-groups/{dbSecurityGroupId}
```

<a id="list-db-security-group-details-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DB security group identifier |

<a id="list-db-security-group-details-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-db-security-group-details-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| dbSecurityGroupId | UUID | DB security group identifier |
| dbSecurityGroupName | String | Name to identify DB security groups |
| description | String | Additional information of DB security group |
| progressStatus | Enum | Current status of DB security group<br/>- `NONE`: None<br/>- `CREATING_RULE`: Creating rule<br/>- `UPDATING_RULE`: Modifying rule<br/>- `DELETING_RULE`: Deleting rule<br/>- `APPLYING_DEFAULT_RULE`: Applying default rule |
| rules | Array | DB security group rules |
| rules.ruleId | UUID | DB security group rule identifier |
| rules.description | String | Additional information of DB security group rule |
| rules.direction | Enum | Communication direction<br/>- `INGRESS`: Inbound<br/>- `EGRESS`: Outbound |
| rules.etherType | Enum | Ether type<br/>- `IPV4`: IPv4 format<br/>- `IPV6`: IPv6 format |
| rules.port | Object | Port object |
| rules.port.portType | Enum | Port type<br/>- `ALL`: Entire port range (not used in the user console)<br/>- `PORT`: Specific port<br/>- `DB_PORT`: DB listening port<br/>- `PORT_RANGE`: Port range |
| rules.port.minPort | Number | Minimum value of port range |
| rules.port.maxPort | Number | Maximum value of port range |
| rules.cidr | String | CIDR |
| rules.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| rules.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-db-security-group"></a>
### Modify DB Security Group { #modify-db-security-group }

<a id="modify-db-security-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbSecurityGroup.Modify | Modify DB security group |

<a id="modify-db-security-group-request"></a>
#### Request

```http
PUT /v4.0/db-security-groups/{dbSecurityGroupId}
```

<a id="modify-db-security-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DB security group identifier |

<a id="modify-db-security-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "dbSecurityGroupName": "dbSecurityGroupName",
    "description": "description-example"
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbSecurityGroupName | String | N | Name to identify DB security groups<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB security group<br/>- Maximum length: `100` |

<a id="modify-db-security-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="delete-db-security-group-rule"></a>
### Delete DB Security Group Rule { #delete-db-security-group-rule }

<a id="delete-db-security-group-rule-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbSecurityGroupRule.Delete | Delete DB security group rule |

<a id="delete-db-security-group-rule-request"></a>
#### Request

```http
DELETE /v4.0/db-security-groups/{dbSecurityGroupId}/rules
```

<a id="delete-db-security-group-rule-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DB security group identifier |
| ruleIds | Query | String | Y | DB security group rule identifiers |

<a id="delete-db-security-group-rule-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-db-security-group-rule-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Task identifier |

---

<a id="create-db-security-group-rule"></a>
### Create DB Security Group Rule { #create-db-security-group-rule }

<a id="create-db-security-group-rule-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbSecurityGroupRule.Create | Create DB security group rule |

<a id="create-db-security-group-rule-request"></a>
#### Request

```http
POST /v4.0/db-security-groups/{dbSecurityGroupId}/rules
```

<a id="create-db-security-group-rule-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DB security group identifier |

<a id="create-db-security-group-rule-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| direction | Enum | Y | Communication direction<br/>- `INGRESS`: Inbound<br/>- `EGRESS`: Outbound |
| etherType | Enum | Y | Ether type<br/>- `IPV4`: IPv4 format<br/>- `IPV6`: IPv6 format |
| port | Object | Y | Port object |
| port.portType | Enum | Y | Port type<br/>- `ALL`: Entire port range (not used in the user console)<br/>- `PORT`: Specific port<br/>- `DB_PORT`: DB listening port<br/>- `PORT_RANGE`: Port range |
| port.minPort | Number | N | Minimum value of port range<br/>- Minimum value: `3306` |
| port.maxPort | Number | N | Maximum value of port range<br/>- Maximum value: `65535` |
| cidr | String | Y | CIDR |
| description | String | N | Additional information of DB security group rule<br/>- Maximum length: `200` |

<a id="create-db-security-group-rule-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Task identifier |

---

<a id="modify-db-security-group-rule"></a>
### Modify DB Security Group Rule { #modify-db-security-group-rule }

<a id="modify-db-security-group-rule-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:DbSecurityGroupRule.Modify | Modify DB security group rule |

<a id="modify-db-security-group-rule-request"></a>
#### Request

```http
PUT /v4.0/db-security-groups/{dbSecurityGroupId}/rules/{ruleId}
```

<a id="modify-db-security-group-rule-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DB security group identifier |
| ruleId | URL | UUID | Y | DB security group rule identifier |

<a id="modify-db-security-group-rule-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| direction | Enum | Y | Communication direction<br/>- `INGRESS`: Inbound<br/>- `EGRESS`: Outbound |
| etherType | Enum | Y | Ether type<br/>- `IPV4`: IPv4 format<br/>- `IPV6`: IPv6 format |
| port | Object | Y | Port object |
| port.portType | Enum | Y | Port type<br/>- `ALL`: Entire port range (not used in the user console)<br/>- `PORT`: Specific port<br/>- `DB_PORT`: DB listening port<br/>- `PORT_RANGE`: Port range |
| port.minPort | Number | N | Minimum value of port range<br/>- Minimum value: `3306` |
| port.maxPort | Number | N | Maximum value of port range<br/>- Maximum value: `65535` |
| cidr | String | Y | CIDR |
| description | String | N | Additional information of DB security group rule<br/>- Maximum length: `200` |

<a id="modify-db-security-group-rule-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| jobId | UUID | Task identifier |

---

<a id="parameter-group"></a>
## Parameter Group { #parameter-group }

<a id="list-parameter-groups"></a>
### List Parameter Groups { #list-parameter-groups }

<a id="list-parameter-groups-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:ParameterGroup.List | List parameter groups |

<a id="list-parameter-groups-request"></a>
#### Request

```http
GET /v4.0/parameter-groups
```

<a id="list-parameter-groups-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| parameterGroupName | Query | String | N | Parameter group name (partial search) |
| dbVersion | Query | Enum | N | DB engine version |
| page | Query | Number | N | Page of the list to query (default: 1)<br/>- Minimum value: `1` |
| size | Query | Number | N | Page size of the list to query (default: 20)<br/>- Minimum value: `1`<br/>- Maximum value: `100` |

<a id="list-parameter-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-parameter-groups-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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
            "dbVersion": "MYSQL_V8411",
            "parameterGroupType": "USER",
            "parameterGroupStatus": "STABLE",
            "createdYmdt": "2023-12-31T15:00:00+09:00",
            "updatedYmdt": "2023-12-31T15:00:00+09:00"
        }
    ]
}
```

</details>

| Name | Format | Description |
|-----|-----|-----|
| totalCounts | Number | Total number of parameter groups |
| parameterGroups | Array | Parameter groups |
| parameterGroups.parameterGroupId | UUID | Parameter group identifier |
| parameterGroups.parameterGroupName | String | Name to identify parameter groups |
| parameterGroups.description | String | Additional information of parameter group |
| parameterGroups.dbVersion | Enum | DB engine version |
| parameterGroups.parameterGroupType | Enum | Parameter group type<br/>- `USER`<br/>- `ADMIN`<br/>- `DEFAULT` |
| parameterGroups.parameterGroupStatus | Enum | Parameter group current status<br/>- `STABLE`: Applied<br/>- `NEED_TO_APPLY`: Need to apply<br/>- `DELETED`: Deleted |
| parameterGroups.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| parameterGroups.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-parameter-group"></a>
### Create Parameter Group { #create-parameter-group }

<a id="create-parameter-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:ParameterGroup.Create | Create parameter group |

<a id="create-parameter-group-request"></a>
#### Request

```http
POST /v4.0/parameter-groups
```

<a id="create-parameter-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "parameterGroupName": "parameterGroupName",
    "description": "description-example",
    "dbVersion": "MYSQL_V8411"
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| parameterGroupName | String | Y | Name to identify parameter groups<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of parameter group<br/>- Maximum length: `100` |
| dbVersion | Enum | Y | DB engine version |

<a id="create-parameter-group-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| parameterGroupId | UUID | Parameter group identifier |

---

<a id="delete-parameter-group"></a>
### Delete Parameter Group { #delete-parameter-group }

<a id="delete-parameter-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:ParameterGroup.Delete | Delete parameter group |

<a id="delete-parameter-group-request"></a>
#### Request

```http
DELETE /v4.0/parameter-groups/{parameterGroupId}
```

<a id="delete-parameter-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | Parameter group identifier |

<a id="delete-parameter-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-parameter-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="list-parameter-group-details"></a>
### List Parameter Group Details { #list-parameter-group-details }

<a id="list-parameter-group-details-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:ParameterGroup.Get | List parameter group details |

<a id="list-parameter-group-details-request"></a>
#### Request

```http
GET /v4.0/parameter-groups/{parameterGroupId}
```

<a id="list-parameter-group-details-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | Parameter group identifier |

<a id="list-parameter-group-details-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-parameter-group-details-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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
    "dbVersion": "MYSQL_V8411",
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

| Name | Format | Description |
|-----|-----|-----|
| parameterGroupId | UUID | Parameter group identifier |
| parameterGroupName | String | Name to identify parameter groups |
| description | String | Additional information of parameter group |
| dbVersion | Enum | DB engine version |
| parameterGroupStatus | Enum | Parameter group current status<br/>- `STABLE`: Applied<br/>- `NEED_TO_APPLY`: Need to apply<br/>- `DELETED`: Deleted |
| parameters | Array | Parameter list |
| parameters.parameterId | UUID | Parameter identifier |
| parameters.parameterFileGroup | Enum | Parameter file group type<br/>- `CLIENT`<br/>- `MYSQL`<br/>- `MYSQLD` |
| parameters.parameterName | String | Parameter name |
| parameters.fileParameterName | String | Parameter file name |
| parameters.value | String | Current value |
| parameters.defaultValue | String | Default value |
| parameters.allowedValue | String | Permitted values |
| parameters.updateType | Enum | Modification type<br/>- `VARIABLE`<br/>- `CONSTANT`<br/>- `INIT_VARIABLE` |
| parameters.applyType | Enum | Application type<br/>- `BOTH`<br/>- `SESSION`<br/>- `FILE` |
| createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-parameter-group"></a>
### Modify Parameter Group { #modify-parameter-group }

<a id="modify-parameter-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:ParameterGroup.Modify | Modify parameter group |

<a id="modify-parameter-group-request"></a>
#### Request

```http
PUT /v4.0/parameter-groups/{parameterGroupId}
```

<a id="modify-parameter-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | Parameter group identifier |

<a id="modify-parameter-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "parameterGroupName": "parameterGroupName",
    "description": "description-example"
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| parameterGroupName | String | N | Name to identify parameter groups<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of parameter group<br/>- Maximum length: `100` |

<a id="modify-parameter-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="copy-parameter-group"></a>
### Copy Parameter Group { #copy-parameter-group }

<a id="copy-parameter-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:ParameterGroup.Copy | Copy parameter group |

<a id="copy-parameter-group-request"></a>
#### Request

```http
POST /v4.0/parameter-groups/{parameterGroupId}/copy
```

<a id="copy-parameter-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | Parameter group identifier |

<a id="copy-parameter-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "parameterGroupName": "parameterGroupName",
    "description": "description-example"
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| parameterGroupName | String | Y | Name to identify parameter groups<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of parameter group<br/>- Maximum length: `100` |

<a id="copy-parameter-group-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| parameterGroupId | UUID | Parameter group identifier |

---

<a id="modify-parameter"></a>
### Modify Parameter { #modify-parameter }

<a id="modify-parameter-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:ParameterGroup.Modify | Modify Parameter |

<a id="modify-parameter-request"></a>
#### Request

```http
PUT /v4.0/parameter-groups/{parameterGroupId}/parameters
```

<a id="modify-parameter-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | Parameter group identifier |

<a id="modify-parameter-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| modifiedParameters | Array | Y | Parameters to change |
| modifiedParameters.parameterId | UUID | Y | Parameter identifier |
| modifiedParameters.value | String | Y | Parameter value to change |

<a id="modify-parameter-response"></a>
#### Response

This API does not return a response body.

---

<a id="reset-parameter-group"></a>
### Reset Parameter Group { #reset-parameter-group }

<a id="reset-parameter-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:ParameterGroup.Reset | Reset parameter group |

<a id="reset-parameter-group-request"></a>
#### Request

```http
PUT /v4.0/parameter-groups/{parameterGroupId}/reset
```

<a id="reset-parameter-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | Parameter group identifier |

<a id="reset-parameter-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="reset-parameter-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="user-group"></a>
## User Group { #user-group }

<a id="list-user-groups"></a>
### List User Groups { #list-user-groups }

<a id="list-user-groups-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:UserGroup.List | List user groups |

<a id="list-user-groups-request"></a>
#### Request

```http
GET /v4.0/user-groups
```

<a id="list-user-groups-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| page | Query | Number | N | Page of the list to query (default: 1)<br/>- Minimum value: `1` |
| size | Query | Number | N | Page size of the list to query (default: 20)<br/>- Minimum value: `1`<br/>- Maximum value: `100` |

<a id="list-user-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-user-groups-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| totalCounts | Number | Total number of user groups |
| userGroups | Array | User Groups |
| userGroups.userGroupId | UUID | User group identifier |
| userGroups.userGroupName | String | Name to identify user groups |
| userGroups.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| userGroups.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-user-group"></a>
### Create User Group { #create-user-group }

<a id="create-user-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:UserGroup.Create | Create user group |

<a id="create-user-group-request"></a>
#### Request

```http
POST /v4.0/user-groups
```

<a id="create-user-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "userGroupName": "userGroupName-example",
    "memberIds": [],
    "selectAll": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| userGroupName | String | Y | Name to identify user groups |
| memberIds | Array | Y | Project member identifiers |
| selectAll | Boolean | N | Whether to include all project members<br/>- Default: `false` |

<a id="create-user-group-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| userGroupId | UUID | User group identifier |

---

<a id="delete-user-group"></a>
### Delete User Group { #delete-user-group }

<a id="delete-user-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:UserGroup.Delete | Delete user group |

<a id="delete-user-group-request"></a>
#### Request

```http
DELETE /v4.0/user-groups/{userGroupId}
```

<a id="delete-user-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| userGroupId | URL | UUID | Y | User group identifier |

<a id="delete-user-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-user-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="list-user-group-details"></a>
### List User Group Details { #list-user-group-details }

<a id="list-user-group-details-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:UserGroup.Get | List user group details |

<a id="list-user-group-details-request"></a>
#### Request

```http
GET /v4.0/user-groups/{userGroupId}
```

<a id="list-user-group-details-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| userGroupId | URL | UUID | Y | User group identifier |

<a id="list-user-group-details-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-user-group-details-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| userGroupId | UUID | User group identifier |
| userGroupName | String | Name to identify user groups |
| userGroupTypeCode | Enum | User group type<br/>- `ENTIRE`<br/>- `INDIVIDUAL_MEMBER` |
| members | Array | Project member list |
| members.memberId | UUID | Project member identifier |
| createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-user-group"></a>
### Modify User Group { #modify-user-group }

<a id="modify-user-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:UserGroup.Modify | Modify user group |

<a id="modify-user-group-request"></a>
#### Request

```http
PUT /v4.0/user-groups/{userGroupId}
```

<a id="modify-user-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| userGroupId | URL | UUID | Y | User group identifier |

<a id="modify-user-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "userGroupName": "userGroupName-example",
    "memberIds": [],
    "selectAll": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| userGroupName | String | Y | Name to identify user groups |
| memberIds | Array | N | Project member identifiers |
| selectAll | Boolean | N | Whether to include all project members<br/>- Default: `false` |

<a id="modify-user-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="notification-group"></a>
## Notification Group { #notification-group }

<a id="list-notification-groups"></a>
### List Notification Groups { #list-notification-groups }

<a id="list-notification-groups-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:NotificationGroup.List | List notification groups |

<a id="list-notification-groups-request"></a>
#### Request

```http
GET /v4.0/notification-groups
```

<a id="list-notification-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-notification-groups-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| notificationGroups | Array | Notification Groups |
| notificationGroups.notificationGroupId | UUID | Notification group identifier |
| notificationGroups.notificationGroupName | String | Name to identify notification groups |
| notificationGroups.notifyEmail | Boolean | Whether to be notified by email |
| notificationGroups.notifySms | Boolean | Whether to be notified by SMS |
| notificationGroups.isEnabled | Boolean | Indicates whether the flavor is enabled |
| notificationGroups.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| notificationGroups.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-notification-group"></a>
### Create Notification Group { #create-notification-group }

<a id="create-notification-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:NotificationGroup.Create | Create notification group |

<a id="create-notification-group-request"></a>
#### Request

```http
POST /v4.0/notification-groups
```

<a id="create-notification-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| notificationGroupName | String | Y | Name to identify notification groups<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| notifyEmail | Boolean | N | Whether to be notified by email<br/>- Default: `true` |
| notifySms | Boolean | N | Whether to be notified by SMS<br/>- Default: `true` |
| isEnabled | Boolean | N | Indicates whether the flavor is enabled<br/>- Default: `true` |
| dbInstanceIds | Array | Y | DB instance identifiers to monitor |
| userGroupIds | Array | Y | User group identifiers |

<a id="create-notification-group-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| notificationGroupId | UUID | Notification group identifier |

---

<a id="delete-notification-group"></a>
### Delete Notification Group { #delete-notification-group }

<a id="delete-notification-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:NotificationGroup.Delete | Delete notification group |

<a id="delete-notification-group-request"></a>
#### Request

```http
DELETE /v4.0/notification-groups/{notificationGroupId}
```

<a id="delete-notification-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| notificationGroupId | URL | UUID | Y | Notification group identifier |

<a id="delete-notification-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-notification-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="view-notification-group-details"></a>
### View Notification Group Details { #view-notification-group-details }

<a id="view-notification-group-details-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:NotificationGroup.Get | View notification group details |

<a id="view-notification-group-details-request"></a>
#### Request

```http
GET /v4.0/notification-groups/{notificationGroupId}
```

<a id="view-notification-group-details-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| notificationGroupId | URL | UUID | Y | Notification group identifier |

<a id="view-notification-group-details-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-notification-group-details-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| notificationGroupId | UUID | Notification group identifier |
| notificationGroupName | String | Name to identify notification groups |
| notifyEmail | Boolean | Whether to be notified by email |
| notifySms | Boolean | Whether to be notified by SMS |
| isEnabled | Boolean | Indicates whether the flavor is enabled |
| dbInstances | Array | DB Instances to monitor |
| dbInstances.dbInstanceId | UUID | DB instance identifier |
| dbInstances.dbInstanceName | String | Name to identify the primary DB instance |
| userGroups | Array | User Groups |
| userGroups.userGroupId | UUID | User group identifier |
| userGroups.userGroupName | String | Name to identify user groups |
| createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="modify-notification-group"></a>
### Modify Notification Group { #modify-notification-group }

<a id="modify-notification-group-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:NotificationGroup.Modify | Modify notification group |

<a id="modify-notification-group-request"></a>
#### Request

```http
PUT /v4.0/notification-groups/{notificationGroupId}
```

<a id="modify-notification-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| notificationGroupId | URL | UUID | Y | Notification group identifier |

<a id="modify-notification-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| notificationGroupName | String | N | Name to identify notification groups |
| notifyEmail | Boolean | N | Whether to be notified by email<br/>- Default: `false` |
| notifySms | Boolean | N | Whether to be notified by SMS<br/>- Default: `false` |
| isEnabled | Boolean | N | Indicates whether the flavor is enabled<br/>- Default: `false` |
| dbInstanceIds | Array | N | DB instance identifiers to monitor |
| userGroupIds | Array | N | User group identifiers |

<a id="modify-notification-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="monitoring"></a>
## Monitoring { #monitoring }

<a id="view-stats"></a>
### View Stats { #view-stats }

<a id="view-stats-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Metric.List | List metric information |

<a id="view-stats-request"></a>
#### Request

```http
GET /v4.0/metric-statistics
```

<a id="view-stats-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | Query | UUID | Y | DB instance identifier |
| measureNames | Query | Array | Y | List of performance metrics to query |
| from | Query | DateTime | Y | Start date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| to | Query | DateTime | Y | End date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| interval | Query | Number | N | View interval<br/>- Unit: `minute`<br/>- Default: An appropriate value is automatically selected based on the start and end date and time |

<a id="view-stats-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="view-stats-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| metricStatistics | Array | Statistics information list |
| metricStatistics.measureName | Enum | Measure type |
| metricStatistics.unit | String | Unit of measured value |
| metricStatistics.values | Array | Measured value list |
| metricStatistics.values.timestamp | Timestamp | Measure time |
| metricStatistics.values.value | String | Measured value |

---

<a id="list-metric-list"></a>
### List Metrics { #list-metric-list }

<a id="list-metric-list-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Metric.List | List Metrics |

<a id="list-metric-list-request"></a>
#### Request

```http
GET /v4.0/metrics
```

<a id="list-metric-list-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-metric-list-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| metrics | Array | Metric List |
| metrics.measureName | Enum | Metric type to query |
| metrics.unit | String | Unit of measured value |

---

<a id="event"></a>
## Event { #event }

<a id="event-category"></a>
### Event Category { #event-category }

Events can be categorized into categories, which are shown below.

| Event category    | Description      |
|-------------|---------|
| ALL         | All      |
| BACKUP      | Backups      |
| DB_INSTANCE | DB Instance |
| JOB         | Jobs      |
| TENANT      | Tenant     |
| MONITORING  | Monitoring    |

<a id="list-subscribable-event-codes"></a>
### List Subscribable Event Codes { #list-subscribable-event-codes }

<a id="list-subscribable-event-codes-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Event.List | List Subscribable Event Codes |

<a id="list-subscribable-event-codes-request"></a>
#### Request

```http
GET /v4.0/event-codes
```

<a id="list-subscribable-event-codes-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-subscribable-event-codes-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| eventCodes | Array | Event Codes |
| eventCodes.eventCode | Enum | Event Code |
| eventCodes.eventCategoryType | Enum | Event category type<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |

---

<a id="list-events"></a>
### List Events { #list-events }

<a id="list-events-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:Event.List | List Events |

<a id="list-events-request"></a>
#### Request

```http
GET /v4.0/events
```

<a id="list-events-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| from | Query | DateTime | Y | Start date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| to | Query | DateTime | Y | End date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| eventCategoryType | Query | Enum | Y | Event category types to query<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| sourceId | Query | UUID | N | Event target resource identifier |
| keyword | Query | String | N | String keyword in event message |
| ascendingOrder | Query | Enum | N | Event message sorting order<br/>- Default value: `DESC`<br/>- `ASC`<br/>- `DESC` |
| page | Query | Number | N | Page of the list to query (default: 1)<br/>- Minimum value: `1` |
| size | Query | Number | N | Page size of the list to query (default: 20)<br/>- Minimum value: `1`<br/>- Maximum value: `100` |

<a id="list-events-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-events-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| totalCounts | Number | Total number of events |
| events | Array | Events |
| events.eventCategoryType | Enum | Event category type<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| events.eventCode | Enum | Occurred event type |
| events.sourceId | UUID | Event source identifier |
| events.sourceName | String | Name to identify event sources |
| events.messages | Array | Event messages |
| events.messages.langCode | Enum | Language code<br/>- `KO`<br/>- `EN`<br/>- `JA`<br/>- `ZH` |
| events.messages.message | String | Event Message |
| events.eventYmdt | DateTime | Event occurred date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="event-subscription"></a>
## Event Subscription { #event-subscription }

<a id="list-event-subscriptions"></a>
### List Event Subscriptions { #list-event-subscriptions }

<a id="list-event-subscriptions-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:EventSubscription.List | List event subscriptions |

<a id="list-event-subscriptions-request"></a>
#### Request

```http
GET /v4.0/event-subscriptions
```

<a id="list-event-subscriptions-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| eventSubscriptionId | Query | UUID | N | Event subscription identifier |
| eventSubscriptionName | Query | String | N | Name to identify event subscription |
| userGroupId | Query | UUID | N | User group identifier |
| page | Query | Number | N | Page of the list to query (default: 1)<br/>- Minimum value: `1` |
| size | Query | Number | N | Page size of the list to query (default: 20)<br/>- Minimum value: `1`<br/>- Maximum value: `100` |

<a id="list-event-subscriptions-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="list-event-subscriptions-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| totalCounts | Number | Total number of event subscriptions |
| eventSubscriptions | Array | List of event subscriptions |
| eventSubscriptions.eventSubscriptionId | UUID | Event subscription identifier |
| eventSubscriptions.eventCategoryType | Enum | Event category type<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| eventSubscriptions.eventSubscriptionName | String | Name to identify event subscription |
| eventSubscriptions.enabled | Boolean | Indicates whether the flavor is enabled |
| eventSubscriptions.notifyEmail | Boolean | Whether to send emails |
| eventSubscriptions.notifySms | Boolean | Whether to send SMS messages |
| eventSubscriptions.eventCodes | Array | List of event codes to subscribe to |
| eventSubscriptions.sources | Array | List of event sources to subscribe to |
| eventSubscriptions.sources.sourceId | UUID | Event source identifier |
| eventSubscriptions.sources.eventCategoryType | Enum | Event category type<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| eventSubscriptions.userGroupIds | Array | List of identifiers of user groups subscribing to the event |
| eventSubscriptions.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-an-event-subscription"></a>
### Create an Event Subscription { #create-an-event-subscription }

<a id="create-an-event-subscription-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:EventSubscription.Create | Create an event subscription |

<a id="create-an-event-subscription-request"></a>
#### Request

```http
POST /v4.0/event-subscriptions
```

<a id="create-an-event-subscription-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| eventCategoryType | Enum | Y | Event category type<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| eventSubscriptionName | String | Y | Name to identify event subscription |
| enabled | Boolean | Y | Indicates whether the flavor is enabled |
| notifyEmail | Boolean | Y | Whether to send emails |
| notifySms | Boolean | Y | Whether to send SMS messages |
| eventCodes | Array | Y | List of event codes to subscribe to |
| sources | Array | Y | List of event sources to subscribe to |
| sources.sourceId | UUID | Y | Event source identifier |
| sources.eventCategoryType | Enum | Y | Event category type<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| userGroupIds | Array | Y | List of identifiers of user groups to subscribe to |

<a id="create-an-event-subscription-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| eventSubscriptionId | UUID | Event subscription identifier |

---

<a id="delete-an-event-subscription"></a>
### Delete an Event Subscription { #delete-an-event-subscription }

<a id="delete-an-event-subscription-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:EventSubscription.Delete | Delete an event subscription |

<a id="delete-an-event-subscription-request"></a>
#### Request

```http
DELETE /v4.0/event-subscriptions/{eventSubscriptionId}
```

<a id="delete-an-event-subscription-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| eventSubscriptionId | URL | UUID | Y | Event subscription identifier |

<a id="delete-an-event-subscription-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-an-event-subscription-response"></a>
#### Response

This API does not return a response body.

---

<a id="modify-an-event-subscription"></a>
### Modify an Event Subscription { #modify-an-event-subscription }

<a id="modify-an-event-subscription-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:EventSubscription.Modify | Modify an event subscription |

<a id="modify-an-event-subscription-request"></a>
#### Request

```http
PUT /v4.0/event-subscriptions/{eventSubscriptionId}
```

<a id="modify-an-event-subscription-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| eventSubscriptionId | URL | UUID | Y | Event subscription identifier |

<a id="modify-an-event-subscription-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| eventCategoryType | Enum | N | Event category type<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| eventSubscriptionName | String | N | Name to identify event subscription |
| enabled | Boolean | N | Indicates whether the flavor is enabled |
| notifyEmail | Boolean | N | Whether to send emails |
| notifySms | Boolean | N | Whether to send SMS messages |
| eventCodes | Array | N | List of event codes to subscribe to |
| sources | Array | N | List of event sources to subscribe to |
| sources.sourceId | UUID | Y | Event source identifier |
| sources.eventCategoryType | Enum | Y | Event category type<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| userGroupIds | Array | N | List of identifiers of user groups to subscribe to |

<a id="modify-an-event-subscription-response"></a>
#### Response

This API does not return a response body.

---

<a id="availability-zones"></a>
## Availability Zones { #availability-zones }

<a id="get-availability-zones"></a>
### List Availability Zones { #get-availability-zones }

<a id="get-availability-zones-required-permissions"></a>
#### Required permissions

| Permission Name | Description |
|-----|-----|
| RDSforMySQL:AvailabilityZone.List | List Availability Zones |

<a id="get-availability-zones-request"></a>
#### Request

```http
GET /v4.0/availability-zones
```

<a id="get-availability-zones-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-availability-zones-response"></a>
#### Response

<details>
  <summary><strong>Example Code</strong></summary>

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

| Name | Format | Description |
|-----|-----|-----|
| availabilityZones | Array | Availability zone list |
| availabilityZones.availabilityZoneName | String | Availability zone name |
| availabilityZones.zoneState | Object | Availability zone status |
| availabilityZones.zoneState.available | Boolean | Whether the availability zone is available |

---

