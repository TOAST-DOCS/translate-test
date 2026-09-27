<!-- pre-align:aligned sig=d58a9ac7e400 -->

<a id="database-rds-for-enginepascalcase-api-guide"></a>
## Database > RDS for MySQL > API Guide { #database-rds-for-enginepascalcase-api-guide }

<a id="rds-for-enginepascalcase-api-common-information"></a>
## RDS for MySQL API Common Information { #rds-for-enginepascalcase-api-common-information }

<a id="api-endpoint"></a>
### API Endpoint { #api-endpoint }

| Region | Endpoint |
|------|----------|
| Korea (Daegu) region | https://ngoic-kr4-rds-proxy.cloud.toastoven.net |


<a id="common-authorization"></a>
### Authentication and Authorization { #common-authorization }

User Access Key is required to use the RDS for MySQL API. A User Access Key is an authentication key issued based on an NHN Cloud or IAM account. It is used in conjunction with a Secret Access Key to authenticate API requests.

User Access Keys and Secret Access Keys can be issued in the console's **API Security Setting**. For more information on issuing and using User Access Key, see [User Access Key](/nhncloud/en/public-api/user-access-key).
The created Key must be included in the request header along with the Appkey.

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| X-TC-APP-KEY | Header | String | Y | Appkey of RDS for MySQL or integrated Appkey for project |
| X-TC-AUTHENTICATION-ID | Header | String | Y | User Access Key ID from the API Security Settings menu |
| X-TC-AUTHENTICATION-SECRET | Header | String | Y | Secret Access Key from the API Security Settings menu |

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

<a id="get-db-versions"></a>
### List DB Engine Versions { #get-db-versions }

<a id="get-db-versions-request"></a>
#### Request

```http
GET /v3.0/db-versions
```

<a id="get-db-versions-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-versions-response"></a>
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

<a id="get-project-members"></a>
### List Project Members { #get-project-members }

<a id="get-project-members-request"></a>
#### Request

```http
GET /v3.0/project/members
```

<a id="get-project-members-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-project-members-response"></a>
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

<a id="get-regions"></a>
### List Regions { #get-regions }

<a id="get-regions-request"></a>
#### Request

```http
GET /v3.0/project/regions
```

<a id="get-regions-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-regions-response"></a>
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
            "regionCode": "KR4",
            "isEnabled": false
        }
    ]
}
```

</details>

| Name | Format | Description |
|-----|-----|-----|
| regions | Array | Region list |
| regions.regionCode | Enum | Region code<br/>- `KR4`: Korea (Daegu) |
| regions.isEnabled | Boolean | Whether to enable a region |

---

<a id="specifications-of-db-instance"></a>
## Specifications of DB Instance { #specifications-of-db-instance }

<a id="get-db-flavors"></a>
### List DB Instance Specifications { #get-db-flavors }

<a id="get-db-flavors-request"></a>
#### Request

```http
GET /v3.0/db-flavors
```

<a id="get-db-flavors-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-flavors-response"></a>
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

<a id="get-subnets"></a>
### List Subnets { #get-subnets }

<a id="get-subnets-request"></a>
#### Request

```http
GET /v3.0/network/subnets
```

<a id="get-subnets-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-subnets-response"></a>
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

<a id="get-storage-types"></a>
### List Storage Types { #get-storage-types }

<a id="get-storage-types-request"></a>
#### Request

```http
GET /v3.0/storage-types
```

<a id="get-storage-types-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-storage-types-response"></a>
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

<a id="get-storages"></a>
### List Storage { #get-storages }

<a id="get-storages-request"></a>
#### Request

```http
GET /v3.0/storages
```

<a id="get-storages-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-storages-response"></a>
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
    "storages": [
        "General SSD",
        "General HDD"
    ]
}
```

</details>

| Name | Format | Description |
|-----|-----|-----|
| storages | Array | Storage list |

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

<a id="get-job"></a>
### List Task Details { #get-job }

<a id="get-job-request"></a>
#### Request

```http
GET /v3.0/jobs/{jobId}
```

<a id="get-job-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| jobId | URL | UUID | Y | Task identifier |

<a id="get-job-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-job-response"></a>
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

<a id="get-db-instance-groups"></a>
### List DB Instance Groups { #get-db-instance-groups }

<a id="get-db-instance-groups-request"></a>
#### Request

```http
GET /v3.0/db-instance-groups
```

<a id="get-db-instance-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-instance-groups-response"></a>
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

<a id="get-db-instance-group"></a>
### List DB Instance Group Details { #get-db-instance-group }

<a id="get-db-instance-group-request"></a>
#### Request

```http
GET /v3.0/db-instance-groups/{dbInstanceGroupId}
```

<a id="get-db-instance-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceGroupId | URL | UUID | Y | DB instance group identifier |

<a id="get-db-instance-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-instance-group-response"></a>
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

<a id="get-db-instances"></a>
### List DB Instances { #get-db-instances }

<a id="get-db-instances-request"></a>
#### Request

```http
GET /v3.0/db-instances
```

<a id="get-db-instances-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-instances-response"></a>
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

<a id="create-db-instance-request"></a>
#### Request

```http
POST /v3.0/db-instances
```

<a id="create-db-instance-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "dbInstanceCandidateName": "dbInstanceCandidateName",
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
    "authenticationPlugin": "NATIVE",
    "tlsOption": "NONE",
    "network": {
        "subnetId": "550e8400-e29b-41d4-a716-446655440000",
        "usePublicAccess": false,
        "availabilityZone": "kr-pub-a"
    },
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20
    },
    "backup": {
        "backupPeriod": 0,
        "backupRetryCount": 0,
        "ftwrlWaitTimeout": 1800,
        "replicationRegion": "KR4",
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
| dbInstanceCandidateName | String | N | Name to identify the standby DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
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
| authenticationPlugin | Enum | N | Authentication Plugin<br/>- `NATIVE`: mysql_native_password authentication<br/>- `CACHING_SHA2`: caching_sha2_password authentication (MySQL only)<br/>- `SHA256`: sha256_password authentication (MySQL only) |
| tlsOption | Enum | N | TLS option<br/>- Default: `NONE`<br/>- `NONE`: TLS is not used<br/>- `SSL`: SSL authentication<br/>- `X509`: X509 certificate authentication |
| network | Object | Y | Network information objects |
| network.subnetId | UUID | Y | Subnet identifier |
| network.usePublicAccess | Boolean | N | External access is available or not<br/>- Default: `false` |
| network.availabilityZone | Enum | Y | Availability zone where DB instance will be created |
| storage | Object | Y | Storage information object |
| storage.storageType | Enum | Y | Storage type |
| storage.storageSize | Number | Y | Block Storage Size (GB)<br/>- Minimum value: `20` |
| backup | Object | Y | Backup information objects |
| backup.backupPeriod | Number | Y | Backup retention period<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR4`: Korea (Daegu) |
| backup.useBackupLock | Boolean | N | Whether to use table lock<br/>- Default: `true` |
| backup.backupSchedules | Array | Y | Backup schedule list |
| backup.backupSchedules.backupWndBgnTime | Time | Y | Backup start time |
| backup.backupSchedules.backupWndDuration | Enum | Y | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |

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
| jobId | UUID | Task identifier |

---

<a id="restore-db-instance-from-obs"></a>
### Restore from Object Storage { #restore-db-instance-from-obs }

<a id="restore-db-instance-from-obs-request"></a>
#### Request

```http
POST /v3.0/db-instances/restore-from-obs
```

<a id="restore-db-instance-from-obs-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "dbInstanceCandidateName": "dbInstanceCandidateName",
    "description": "description-example",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "dbPort": 13306,
    "dbVersion": "MYSQL_V8411",
    "useHighAvailability": false,
    "imageId": "550e8400-e29b-41d4-a716-446655440000",
    "pingInterval": 3,
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20
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
        "replicationRegion": "KR4",
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
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbSecurityGroupIds": [],
    "userGroupIds": [],
    "useDeletionProtection": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceName | String | N | Name to identify the primary DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| dbInstanceCandidateName | String | N | Name to identify the standby DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB instance<br/>- Maximum length: `100` |
| dbFlavorId | UUID | Y | Identifier of DB instance specifications |
| dbPort | Number | N | DB port |
| dbVersion | Enum | Y | DB engine version |
| useHighAvailability | Boolean | N | Whether to use high availability<br/>- Default: `false` |
| imageId | UUID | N | Image identifier |
| pingInterval | Number | N | Ping interval (sec) when using high availability<br/>- Minimum value: `1`<br/>- Maximum value: `600` |
| storage | Object | Y | Storage information object |
| storage.storageType | Enum | Y | Storage type |
| storage.storageSize | Number | Y | Block Storage Size (GB)<br/>- Minimum value: `20` |
| network | Object | Y | Network information objects |
| network.subnetId | UUID | Y | Subnet identifier |
| network.usePublicAccess | Boolean | N | External access is available or not<br/>- Default: `false` |
| network.availabilityZone | Enum | Y | Availability zone where DB instance will be created |
| backup | Object | Y | Backup information objects |
| backup.backupPeriod | Number | Y | Backup retention period<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR4`: Korea (Daegu) |
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
| parameterGroupId | UUID | Y | Parameter group identifier |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| userGroupIds | Array | N | User group identifiers |
| useDeletionProtection | Boolean | N | Whether to protect against deletion<br/>- Default: `false` |

<a id="restore-db-instance-from-obs-response"></a>
#### Response

This API does not return a response body.

---

<a id="delete-db-instance"></a>
### Delete DB Instance { #delete-db-instance }

<a id="delete-db-instance-request"></a>
#### Request

```http
DELETE /v3.0/db-instances/{dbInstanceId}
```

<a id="delete-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="delete-db-instance-request-body"></a>
#### Request Body

This API does not require a request body.

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
| jobId | UUID | Task identifier |

---

<a id="get-db-instance"></a>
### List DB Instance Details { #get-db-instance }

<a id="get-db-instance-request"></a>
#### Request

```http
GET /v3.0/db-instances/{dbInstanceId}
```

<a id="get-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="get-db-instance-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-instance-response"></a>
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
| supportAuthenticationPlugin | Boolean | Whether to support authentication plugin |
| needToApplyParameterGroup | Boolean | Need to apply the latest parameter group |
| needMigration | Boolean | Need to migrate |
| supportDbVersionUpgrade | Boolean | Whether to support DB version upgrade |
| createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="update-db-instance"></a>
### Modify DB Instance { #update-db-instance }

<a id="update-db-instance-request"></a>
#### Request

```http
PUT /v3.0/db-instances/{dbInstanceId}
```

<a id="update-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="update-db-instance-request-body"></a>
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
| useDummy | Boolean | N | Whether to use dummies when upgrading the DB version of a single DB instance<br/>- Default: `false` |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| executeBackup | Boolean | N | Whether to perform a backup at the current point in time<br/>- Default: `false` |
| useOnlineFailover | Boolean | N | Whether to restart using failover<br/>- Default: `false` |
| waitReplicationDelay | Boolean | N | Wait for replication delay to be resolved<br/>- Default: `false` |
| useReadOnly | Boolean | N | Block write load<br/>- Default: `false` |

<a id="update-db-instance-response"></a>
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

<a id="backup-db-instance"></a>
### Backup DB Instance { #backup-db-instance }

<a id="backup-db-instance-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/backup
```

<a id="backup-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="backup-db-instance-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "backupName": "backupName"
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| backupName | String | Y | Name to identify backups<br/>- Minimum length: `1`<br/>- Maximum length: `100` |

<a id="backup-db-instance-response"></a>
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

<a id="get-backup-info"></a>
### View Backup Information { #get-backup-info }

<a id="get-backup-info-request"></a>
#### Request

```http
GET /v3.0/db-instances/{dbInstanceId}/backup-info
```

<a id="get-backup-info-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="get-backup-info-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-backup-info-response"></a>
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
    "replicationRegion": "KR4",
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
| replicationRegion | Enum | Backup replication region<br/>- `KR4`: Korea (Daegu) |
| useBackupLock | Boolean | Whether to use table lock |
| backupSchedules | Array | Backup schedule list |
| backupSchedules.backupWndBgnTime | Time | Backup start time |
| backupSchedules.backupWndDuration | Enum | Backup window<br/>- `HALF_AN_HOUR`<br/>- `ONE_HOUR`<br/>- `ONE_HOUR_AND_HALF`<br/>- `TWO_HOURS`<br/>- `TWO_HOURS_AND_HALF`<br/>- `THREE_HOURS` |

---

<a id="update-backup-info"></a>
### Modify Backup Information { #update-backup-info }

<a id="update-backup-info-request"></a>
#### Request

```http
PUT /v3.0/db-instances/{dbInstanceId}/backup-info
```

<a id="update-backup-info-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="update-backup-info-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "backupPeriod": 0,
    "ftwrlWaitTimeout": 0,
    "backupRetryCount": 0,
    "replicationRegion": "KR4",
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
| replicationRegion | Enum | N | Backup replication region<br/>- `KR4`: Korea (Daegu) |
| useBackupLock | Boolean | N | Whether to use table lock |
| backupSchedules | Array | N | Backup schedule list |
| backupSchedules.backupWndBgnTime | Time | Y | Backup start time |
| backupSchedules.backupWndDuration | Enum | Y | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |

<a id="update-backup-info-response"></a>
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

<a id="backup-db-instance-to-object-storage"></a>
### Export after Backing up DB Instance { #backup-db-instance-to-object-storage }

<a id="backup-db-instance-to-object-storage-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/backup-to-object-storage
```

<a id="backup-db-instance-to-object-storage-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="backup-db-instance-to-object-storage-request-body"></a>
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

<a id="backup-db-instance-to-object-storage-response"></a>
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

<a id="change-image-meta"></a>
### Change DB Image Meta for Testing { #change-image-meta }

<a id="change-image-meta-request"></a>
#### Request

```http
PUT /v3.0/db-instances/{dbInstanceId}/change-image-meta
```

<a id="change-image-meta-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="change-image-meta-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="change-image-meta-response"></a>
#### Response

This API does not return a response body.

---

<a id="get-db-schemas"></a>
### List DB Schema { #get-db-schemas }

<a id="get-db-schemas-request"></a>
#### Request

```http
GET /v3.0/db-instances/{dbInstanceId}/db-schemas
```

<a id="get-db-schemas-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="get-db-schemas-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-schemas-response"></a>
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

<a id="create-db-schema-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/db-schemas
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
| jobId | UUID | Task identifier |

---

<a id="delete-db-schema"></a>
### Delete DB Schema { #delete-db-schema }

<a id="delete-db-schema-request"></a>
#### Request

```http
DELETE /v3.0/db-instances/{dbInstanceId}/db-schemas/{dbSchemaId}
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
| jobId | UUID | Task identifier |

---

<a id="get-db-users"></a>
### List DB Users { #get-db-users }

<a id="get-db-users-request"></a>
#### Request

```http
GET /v3.0/db-instances/{dbInstanceId}/db-users
```

<a id="get-db-users-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="get-db-users-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-users-response"></a>
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

<a id="create-db-user-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/db-users
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
| jobId | UUID | Task identifier |

---

<a id="delete-db-user"></a>
### Delete DB User { #delete-db-user }

<a id="delete-db-user-request"></a>
#### Request

```http
DELETE /v3.0/db-instances/{dbInstanceId}/db-users/{dbUserId}
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
| jobId | UUID | Task identifier |

---

<a id="update-db-user"></a>
### Modify DB User { #update-db-user }

<a id="update-db-user-request"></a>
#### Request

```http
PUT /v3.0/db-instances/{dbInstanceId}/db-users/{dbUserId}
```

<a id="update-db-user-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| dbUserId | URL | UUID | Y | DB user identifier |

<a id="update-db-user-request-body"></a>
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

<a id="update-db-user-response"></a>
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

<a id="change-deletion-protection"></a>
### Change DB Instance Deletion Protection Settings { #change-deletion-protection }

<a id="change-deletion-protection-request"></a>
#### Request

```http
PUT /v3.0/db-instances/{dbInstanceId}/deletion-protection
```

<a id="change-deletion-protection-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="change-deletion-protection-request-body"></a>
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

<a id="change-deletion-protection-response"></a>
#### Response

This API does not return a response body.

---

<a id="force-restart-db-instance"></a>
### Force Restart DB Instance { #force-restart-db-instance }

<a id="force-restart-db-instance-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/force-restart
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

<a id="update-high-availability"></a>
### Modify High Availability { #update-high-availability }

<a id="update-high-availability-request"></a>
#### Request

```http
PUT /v3.0/db-instances/{dbInstanceId}/high-availability
```

<a id="update-high-availability-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="update-high-availability-request-body"></a>
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

<a id="update-high-availability-response"></a>
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

<a id="pause-high-availability"></a>
### Pause High Availability { #pause-high-availability }

<a id="pause-high-availability-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/high-availability/pause
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
| jobId | UUID | Task identifier |

---

<a id="repair-high-availability"></a>
### Recover High Availability { #repair-high-availability }

<a id="repair-high-availability-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/high-availability/repair
```

<a id="repair-high-availability-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="repair-high-availability-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="repair-high-availability-response"></a>
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

<a id="resume-high-availability"></a>
### Restart High Availability { #resume-high-availability }

<a id="resume-high-availability-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/high-availability/resume
```

<a id="resume-high-availability-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="resume-high-availability-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="resume-high-availability-response"></a>
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

<a id="split-high-availability"></a>
### Separate High Availability { #split-high-availability }

<a id="split-high-availability-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/high-availability/split
```

<a id="split-high-availability-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="split-high-availability-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="split-high-availability-response"></a>
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

<a id="get-log-files"></a>
### List Log Files { #get-log-files }

<a id="get-log-files-request"></a>
#### Request

```http
GET /v3.0/db-instances/{dbInstanceId}/log-files
```

<a id="get-log-files-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| logFileTypes | Query | Array | N | Log file type list |

<a id="get-log-files-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-log-files-response"></a>
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

<a id="export-log-files"></a>
### Export Log File { #export-log-files }

<a id="export-log-files-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/log-files/export
```

<a id="export-log-files-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="export-log-files-request-body"></a>
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

<a id="export-log-files-response"></a>
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

<a id="get-network-info"></a>
### List Network Information { #get-network-info }

<a id="get-network-info-request"></a>
#### Request

```http
GET /v3.0/db-instances/{dbInstanceId}/network-info
```

<a id="get-network-info-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="get-network-info-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-network-info-response"></a>
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

<a id="update-network-info"></a>
### Modify Network Information { #update-network-info }

<a id="update-network-info-request"></a>
#### Request

```http
PUT /v3.0/db-instances/{dbInstanceId}/network-info
```

<a id="update-network-info-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="update-network-info-request-body"></a>
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

<a id="update-network-info-response"></a>
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

<a id="promote-db-instance"></a>
### Promote DB Instance { #promote-db-instance }

<a id="promote-db-instance-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/promote
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
| jobId | UUID | Task identifier |

---

<a id="replicate-db-instance"></a>
### Replicate DB Instance { #replicate-db-instance }

<a id="replicate-db-instance-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/replicate
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
    "network": {
        "usePublicAccess": false,
        "availabilityZone": "kr-pub-a"
    },
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20
    },
    "backup": {
        "backupPeriod": 0,
        "backupRetryCount": 0,
        "ftwrlWaitTimeout": 0,
        "replicationRegion": "KR4",
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
| dbPort | Number | Y | DB port<br/>- Minimum value: 3306, Maximum value: 43306 |
| parameterGroupId | UUID | N | Parameter group identifier |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| userGroupIds | Array | N | User group identifiers |
| useDefaultNotification | Boolean | N | Whether to use default notification<br/>- Default: `false` |
| useDeletionProtection | Boolean | N | Whether to protect against deletion<br/>- Default: `false` |
| network | Object | Y | Network information objects |
| network.usePublicAccess | Boolean | N | External access is available or not |
| network.availabilityZone | Enum | Y | Availability zone where DB instance will be created |
| storage | Object | N | Storage information object |
| storage.storageType | Enum | N | Data storage type |
| storage.storageSize | Number | N | Block Storage Size (GB)<br/>- Minimum value: `20` |
| backup | Object | N | Backup information objects |
| backup.backupPeriod | Number | N | Backup retention period<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR4`: Korea (Daegu) |
| backup.useBackupLock | Boolean | N | Whether to use table lock |
| backup.backupSchedules | Array | N | Backup schedule list |
| backup.backupSchedules.backupWndBgnTime | Time | N | Backup start time |
| backup.backupSchedules.backupWndDuration | Enum | N | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |

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
| jobId | UUID | Task identifier |

---

<a id="restart-db-instance"></a>
### Restart DB Instance { #restart-db-instance }

<a id="restart-db-instance-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/restart
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
    "useReadOnly": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| useOnlineFailover | Boolean | N | Whether to restart using failover<br/>- Default: `false` |
| executeBackup | Boolean | N | Whether to perform a backup at the current point in time<br/>- Default: `false` |
| waitReplicationDelay | Boolean | N | Wait for replication delay to be resolved<br/>- Default: `false` |
| useReadOnly | Boolean | N | Block write load<br/>- Default: `false` |

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
| jobId | UUID | Task identifier |

---

<a id="get-restoration-info"></a>
### View Restoration Information { #get-restoration-info }

<a id="get-restoration-info-request"></a>
#### Request

```http
GET /v3.0/db-instances/{dbInstanceId}/restoration-info
```

<a id="get-restoration-info-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="get-restoration-info-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-restoration-info-response"></a>
#### Response

This API does not return a response body.

---

<a id="get-last-query-to-restore"></a>
### View the Last Query to Be Restored { #get-last-query-to-restore }

<a id="get-last-query-to-restore-request"></a>
#### Request

```http
GET /v3.0/db-instances/{dbInstanceId}/restoration-info/last-query
```

<a id="get-last-query-to-restore-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |
| restoreType | Query | Enum | Y | Restoration type<br/>- `TIMESTAMP`: Point-in-time restoration using a time within the restorable period<br/>- `BINLOG`: Point-in-time restoration using a restorable binary log position |

<a id="get-last-query-to-restore-restoretype-timestamp"></a>
#### If restoreType is `TIMESTAMP`

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| restoreYmdt | Query | DateTime | Y | DB instance restore date (YYYY-MM-DDThh:mm:ss.SSSTZD) |

<a id="get-last-query-to-restore-restoretype-binlog"></a>
#### If restoreType is `BINLOG`

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| backupId | Query | UUID | Y | Identifier of the backup to use for restoration |
| binLogFileName | Query | String | Y | Binary log name to use for restoration |
| binLogPosition | Query | String | Y | Binary log location to use for restoration |

<a id="get-last-query-to-restore-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-last-query-to-restore-response"></a>
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

<a id="restore-db-instance"></a>
### Restoration { #restore-db-instance }

<a id="restore-db-instance-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/restore
```

<a id="restore-db-instance-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="restore-db-instance-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "dbInstanceName": "dbInstanceName",
    "dbInstanceCandidateName": "dbInstanceCandidateName",
    "description": "description-example",
    "dbFlavorId": "550e8400-e29b-41d4-a716-446655440000",
    "dbPort": 13306,
    "useHighAvailability": false,
    "imageId": "550e8400-e29b-41d4-a716-446655440000",
    "pingInterval": 3,
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20
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
        "replicationRegion": "KR4",
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
    "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
    "dbSecurityGroupIds": [],
    "userGroupIds": [],
    "useDeletionProtection": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| dbInstanceName | String | N | Name to identify the primary DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| dbInstanceCandidateName | String | N | Name to identify the standby DB instance<br/>- Minimum length: `1`<br/>- Maximum length: `100` |
| description | String | N | Additional information of DB instance<br/>- Maximum length: `100` |
| dbFlavorId | UUID | Y | Identifier of DB instance specifications |
| dbPort | Number | N | DB port |
| useHighAvailability | Boolean | N | Whether to use high availability<br/>- Default: `false` |
| imageId | UUID | N | Image identifier |
| pingInterval | Number | N | Ping interval (sec) when using high availability<br/>- Minimum value: `1`<br/>- Maximum value: `600` |
| storage | Object | Y | Storage information object |
| storage.storageType | Enum | Y | Storage type |
| storage.storageSize | Number | Y | Block Storage Size (GB)<br/>- Minimum value: `20` |
| network | Object | Y | Network information objects |
| network.subnetId | UUID | Y | Subnet identifier |
| network.usePublicAccess | Boolean | N | External access is available or not<br/>- Default: `false` |
| network.availabilityZone | Enum | Y | Availability zone where DB instance will be created |
| backup | Object | Y | Backup information objects |
| backup.backupPeriod | Number | Y | Backup retention period<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR4`: Korea (Daegu) |
| backup.useBackupLock | Boolean | N | Whether to use table lock<br/>- Default: `true` |
| backup.backupSchedules | Array | Y | Backup schedule list |
| backup.backupSchedules.backupWndBgnTime | Time | Y | Backup start time |
| backup.backupSchedules.backupWndDuration | Enum | Y | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |
| restore | Object | Y | Restoration information object |
| restore.restoreType | Enum | Y | Restoration type<br/>- `TIMESTAMP`: Point-in-time restoration using a time within the restorable period<br/>- `BINLOG`: Point-in-time restoration using a restorable binary log position<br/>- `BACKUP`: Snapshot restoration using a previously created backup |
| useDefaultNotification | Boolean | N | Whether to use default notification<br/>- Default: `false` |
| parameterGroupId | UUID | Y | Parameter group identifier |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| userGroupIds | Array | N | User group identifiers |
| useDeletionProtection | Boolean | N | Whether to protect against deletion<br/>- Default: `false` |

<a id="restore-db-instance-timestamp-restoretype-timestamp"></a>
#### Request when restoring a point in time restoration using Timestamp (if restoreType is `TIMESTAMP`)

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| restore.restoreYmdt | DateTime | N | DB instance restore date (YYYY-MM-DDThh:mm:ss.SSSTZD) |

You can only restore to a point in time earlier than the latest restorable time confirmed by querying the restoration information.

<a id="restore-db-instance-restoretype-binlog"></a>
#### Request for point-in-time restoration using binary logs (if restoreType is `BINLOG`)

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| restore.backupId | UUID | N | Identifier of the backup to use for restoration |
| restore.binLog | Object | N | Binary log information object to use for restoration |
| restore.binLog.binLogFileName | String | N | Binary log name to use for restoration |
| restore.binLog.binLogPosition | Number | N | Binary log location to use for restoration |

For point-in-time restoration using binary logs, you can restore the logs recorded after the binary log file and position of the reference backup.

<a id="restore-db-instance-restoretype-backup"></a>
#### Request when restoring from backup (if restoreType is `BACKUP`)

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| restore.backupId | UUID | N | Identifier of the backup to use for restoration |

<a id="restore-db-instance-response"></a>
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

<a id="start-db-instance"></a>
### Start DB Instance { #start-db-instance }

<a id="start-db-instance-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/start
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
| jobId | UUID | Task identifier |

---

<a id="stop-db-instance"></a>
### Stop DB Instance { #stop-db-instance }

<a id="stop-db-instance-request"></a>
#### Request

```http
POST /v3.0/db-instances/{dbInstanceId}/stop
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
| jobId | UUID | Task identifier |

---

<a id="get-storage-info"></a>
### View Storage Information { #get-storage-info }

<a id="get-storage-info-request"></a>
#### Request

```http
GET /v3.0/db-instances/{dbInstanceId}/storage-info
```

<a id="get-storage-info-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="get-storage-info-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-storage-info-response"></a>
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
    "storageStatus": "DELETED"
}
```

</details>

| Name | Format | Description |
|-----|-----|-----|
| storageType | Enum | Data storage type |
| storageSize | Number | Block Storage Size (GB) |
| storageStatus | Enum | Data Storage Current Status<br/>- `DELETED`: Deleted<br/>- `PENDING_DELETION`: Deletion pending<br/>- `DELETION_RESERVED`: Deletion reserved (waiting for snapshot cleanup)<br/>- `DETACHED`: Detached<br/>- `ATTACHED`: Attached |

---

<a id="update-storage-info"></a>
### Modify Storage Information { #update-storage-info }

<a id="update-storage-info-request"></a>
#### Request

```http
PUT /v3.0/db-instances/{dbInstanceId}/storage-info
```

<a id="update-storage-info-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | URL | UUID | Y | DB instance identifier |

<a id="update-storage-info-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "storageSize": 1
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| storageSize | Number | Y | Block Storage Size (GB)<br/>- Maximum value: `2048` |

<a id="update-storage-info-response"></a>
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

<a id="get-backups"></a>
### Retrieve Backup List { #get-backups }

<a id="get-backups-request"></a>
#### Request

```http
GET /v3.0/backups
```

<a id="get-backups-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| page | Query | Number | Y | Page to retrieve<br/>- Minimum value: `1` |
| size | Query | Number | Y | Page size to retrieve<br/>- Minimum value: `1`<br/>- Maximum value: `100` |
| backupType | Query | Enum | N | Backup type<br/>- `AUTO`<br/>- `MANUAL` |
| dbInstanceId | Query | UUID | N | Original DB instance identifier |
| dbVersion | Query | Enum | N | DB engine version |

<a id="get-backups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-backups-response"></a>
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

<a id="delete-backup"></a>
### Delete Backup { #delete-backup }

<a id="delete-backup-request"></a>
#### Request

```http
DELETE /v3.0/backups/{backupId}
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
| jobId | UUID | Task identifier |

---

<a id="export-backup"></a>
### Export Backup { #export-backup }

<a id="export-backup-request"></a>
#### Request

```http
POST /v3.0/backups/{backupId}/export
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
| jobId | UUID | Task identifier |

---

<a id="restore-backup"></a>
### Restore Backup { #restore-backup }

<a id="restore-backup-request"></a>
#### Request

```http
POST /v3.0/backups/{backupId}/restore
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
    "network": {
        "subnetId": "550e8400-e29b-41d4-a716-446655440000",
        "usePublicAccess": false,
        "availabilityZone": "kr-pub-a"
    },
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20
    },
    "backup": {
        "backupPeriod": 0,
        "backupRetryCount": 0,
        "ftwrlWaitTimeout": 1800,
        "replicationRegion": "KR4",
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
| dbPort | Number | Y | DB port<br/>- Minimum value: 3306, Maximum value: 43306 |
| parameterGroupId | UUID | Y | Parameter group identifier |
| dbSecurityGroupIds | Array | N | DB security group identifiers |
| userGroupIds | Array | N | User group identifiers |
| useHighAvailability | Boolean | N | Whether to use high availability<br/>- Default: `false` |
| pingInterval | Number | N | Ping interval (sec) when using high availability<br/>- Default: `3`<br/>- Minimum value: `1`<br/>- Maximum value: `600` |
| useDefaultNotification | Boolean | N | Whether to use default notification<br/>- Default: `false` |
| useDeletionProtection | Boolean | N | Whether to protect against deletion<br/>- Default: `false` |
| network | Object | Y | Network information objects |
| network.subnetId | UUID | Y | Subnet identifier |
| network.usePublicAccess | Boolean | N | External access is available or not<br/>- Default: `false` |
| network.availabilityZone | Enum | Y | Availability zone where DB instance will be created |
| storage | Object | Y | Storage information object |
| storage.storageType | Enum | Y | Storage type |
| storage.storageSize | Number | Y | Block Storage Size (GB)<br/>- Minimum value: `20` |
| backup | Object | Y | Backup information objects |
| backup.backupPeriod | Number | Y | Backup retention period<br/>- Minimum value: `0`<br/>- Maximum value: `730` |
| backup.backupRetryCount | Number | N | Number of backup retries<br/>- Minimum value: `0`<br/>- Maximum value: `10` |
| backup.ftwrlWaitTimeout | Number | N | Query latency (sec)<br/>- Minimum value: `0`<br/>- Maximum value: `21600` |
| backup.replicationRegion | Enum | N | Backup replication region<br/>- `KR4`: Korea (Daegu) |
| backup.useBackupLock | Boolean | N | Whether to use table lock<br/>- Default: `true` |
| backup.backupSchedules | Array | Y | Backup schedule list |
| backup.backupSchedules.backupWndBgnTime | Time | Y | Backup start time |
| backup.backupSchedules.backupWndDuration | Enum | Y | Backup window<br/>- `HALF_AN_HOUR`: 30 minutes<br/>- `ONE_HOUR`: 1 hour<br/>- `ONE_HOUR_AND_HALF`: 1.5 hour<br/>- `TWO_HOURS`: 2 hour<br/>- `TWO_HOURS_AND_HALF`: 2.5 hour<br/>- `THREE_HOURS`: 3 hour |

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
| jobId | UUID | Task identifier |

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

<a id="get-db-security-groups"></a>
### List DB Security Groups { #get-db-security-groups }

<a id="get-db-security-groups-request"></a>
#### Request

```http
GET /v3.0/db-security-groups
```

<a id="get-db-security-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-security-groups-response"></a>
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

<a id="create-db-security-group-request"></a>
#### Request

```http
POST /v3.0/db-security-groups
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

<a id="delete-db-security-group-request"></a>
#### Request

```http
DELETE /v3.0/db-security-groups/{dbSecurityGroupId}
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

<a id="get-db-security-group"></a>
### List DB Security Group Details { #get-db-security-group }

<a id="get-db-security-group-request"></a>
#### Request

```http
GET /v3.0/db-security-groups/{dbSecurityGroupId}
```

<a id="get-db-security-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DB security group identifier |

<a id="get-db-security-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-db-security-group-response"></a>
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
    "dbSecurityGroup": {
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
}
```

</details>

| Name | Format | Description |
|-----|-----|-----|
| dbSecurityGroup | Object | DB security group |
| dbSecurityGroup.dbSecurityGroupId | UUID | DB security group identifier |
| dbSecurityGroup.dbSecurityGroupName | String | Name to identify DB security groups |
| dbSecurityGroup.description | String | Additional information of DB security group |
| dbSecurityGroup.progressStatus | Enum | Current status of DB security group<br/>- `NONE`: None<br/>- `CREATING_RULE`: Creating rule<br/>- `UPDATING_RULE`: Modifying rule<br/>- `DELETING_RULE`: Deleting rule<br/>- `APPLYING_DEFAULT_RULE`: Applying default rule |
| dbSecurityGroup.rules | Array | DB security group rules |
| dbSecurityGroup.rules.ruleId | UUID | DB security group rule identifier |
| dbSecurityGroup.rules.description | String | Additional information of DB security group rule |
| dbSecurityGroup.rules.direction | Enum | Communication direction<br/>- `INGRESS`: Inbound<br/>- `EGRESS`: Outbound |
| dbSecurityGroup.rules.etherType | Enum | Ether type<br/>- `IPV4`: IPv4 format<br/>- `IPV6`: IPv6 format |
| dbSecurityGroup.rules.port | Object | Port object |
| dbSecurityGroup.rules.port.portType | Enum | Port type<br/>- `ALL`: Entire port range (not used in the user console)<br/>- `PORT`: Specific port<br/>- `DB_PORT`: DB listening port<br/>- `PORT_RANGE`: Port range |
| dbSecurityGroup.rules.port.minPort | Number | Minimum value of port range |
| dbSecurityGroup.rules.port.maxPort | Number | Maximum value of port range |
| dbSecurityGroup.rules.cidr | String | CIDR |
| dbSecurityGroup.rules.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbSecurityGroup.rules.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbSecurityGroup.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbSecurityGroup.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="update-db-security-group"></a>
### Modify DB Security Group { #update-db-security-group }

<a id="update-db-security-group-request"></a>
#### Request

```http
PUT /v3.0/db-security-groups/{dbSecurityGroupId}
```

<a id="update-db-security-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DB security group identifier |

<a id="update-db-security-group-request-body"></a>
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

<a id="update-db-security-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="delete-db-security-group-rule"></a>
### Delete DB Security Group Rule { #delete-db-security-group-rule }

<a id="delete-db-security-group-rule-request"></a>
#### Request

```http
DELETE /v3.0/db-security-groups/{dbSecurityGroupId}/rules
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

<a id="create-db-security-group-rule-request"></a>
#### Request

```http
POST /v3.0/db-security-groups/{dbSecurityGroupId}/rules
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

<a id="update-db-security-group-rule"></a>
### Modify DB Security Group Rule { #update-db-security-group-rule }

<a id="update-db-security-group-rule-request"></a>
#### Request

```http
PUT /v3.0/db-security-groups/{dbSecurityGroupId}/rules/{ruleId}
```

<a id="update-db-security-group-rule-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbSecurityGroupId | URL | UUID | Y | DB security group identifier |
| ruleId | URL | UUID | Y | DB security group rule identifier |

<a id="update-db-security-group-rule-request-body"></a>
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

<a id="update-db-security-group-rule-response"></a>
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

<a id="get-parameter-groups"></a>
### List Parameter Groups { #get-parameter-groups }

<a id="get-parameter-groups-request"></a>
#### Request

```http
GET /v3.0/parameter-groups
```

<a id="get-parameter-groups-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbVersion | Query | Enum | N | DB engine version |

<a id="get-parameter-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-parameter-groups-response"></a>
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
    "parameterGroups": [
        {
            "parameterGroupId": "550e8400-e29b-41d4-a716-446655440000",
            "parameterGroupName": "parameterGroupName-example",
            "description": "description-example",
            "dbVersion": "MYSQL_V8411",
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
| parameterGroups | Array | Parameter groups |
| parameterGroups.parameterGroupId | UUID | Parameter group identifier |
| parameterGroups.parameterGroupName | String | Name to identify parameter groups |
| parameterGroups.description | String | Additional information of parameter group |
| parameterGroups.dbVersion | Enum | DB engine version |
| parameterGroups.parameterGroupStatus | Enum | Parameter group current status<br/>- `STABLE`: Applied<br/>- `NEED_TO_APPLY`: Need to apply<br/>- `DELETED`: Deleted |
| parameterGroups.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| parameterGroups.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-parameter-group"></a>
### Create Parameter Group { #create-parameter-group }

<a id="create-parameter-group-request"></a>
#### Request

```http
POST /v3.0/parameter-groups
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

<a id="delete-parameter-group-request"></a>
#### Request

```http
DELETE /v3.0/parameter-groups/{parameterGroupId}
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

<a id="get-parameter-group"></a>
### List Parameter Group Details { #get-parameter-group }

<a id="get-parameter-group-request"></a>
#### Request

```http
GET /v3.0/parameter-groups/{parameterGroupId}
```

<a id="get-parameter-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | Parameter group identifier |

<a id="get-parameter-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-parameter-group-response"></a>
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

<a id="modify-parameter-group-request"></a>
#### Request

```http
PUT /v3.0/parameter-groups/{parameterGroupId}
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

<a id="copy-parameter-group-request"></a>
#### Request

```http
POST /v3.0/parameter-groups/{parameterGroupId}/copy
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

<a id="modify-parameter-group-parameters"></a>
### Modify Parameter { #modify-parameter-group-parameters }

<a id="modify-parameter-group-parameters-request"></a>
#### Request

```http
PUT /v3.0/parameter-groups/{parameterGroupId}/parameters
```

<a id="modify-parameter-group-parameters-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| parameterGroupId | URL | UUID | Y | Parameter group identifier |

<a id="modify-parameter-group-parameters-request-body"></a>
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

<a id="modify-parameter-group-parameters-response"></a>
#### Response

This API does not return a response body.

---

<a id="reset-parameter-group"></a>
### Reset Parameter Group { #reset-parameter-group }

<a id="reset-parameter-group-request"></a>
#### Request

```http
PUT /v3.0/parameter-groups/{parameterGroupId}/reset
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

<a id="get-user-groups"></a>
### List User Groups { #get-user-groups }

<a id="get-user-groups-request"></a>
#### Request

```http
GET /v3.0/user-groups
```

<a id="get-user-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-user-groups-response"></a>
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
| userGroups | Array | User Groups |
| userGroups.userGroupId | UUID | User group identifier |
| userGroups.userGroupName | String | Name to identify user groups |
| userGroups.createdYmdt | DateTime | Created date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| userGroups.updatedYmdt | DateTime | Modified date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |

---

<a id="create-user-group"></a>
### Create User Group { #create-user-group }

<a id="create-user-group-request"></a>
#### Request

```http
POST /v3.0/user-groups
```

<a id="create-user-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "userGroupName": "userGroupName-example",
    "memberIds": [],
    "selectAllYN": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| userGroupName | String | Y | Name to identify user groups |
| memberIds | Array | Y | Project member identifiers |
| selectAllYN | Boolean | N | Whether to include all project members<br/>- Default: `false` |

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

<a id="delete-user-group-request"></a>
#### Request

```http
DELETE /v3.0/user-groups/{userGroupId}
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

<a id="get-user-group"></a>
### List User Group Details { #get-user-group }

<a id="get-user-group-request"></a>
#### Request

```http
GET /v3.0/user-groups/{userGroupId}
```

<a id="get-user-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| userGroupId | URL | UUID | Y | User group identifier |

<a id="get-user-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-user-group-response"></a>
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

<a id="update-user-group"></a>
### Modify User Group { #update-user-group }

<a id="update-user-group-request"></a>
#### Request

```http
PUT /v3.0/user-groups/{userGroupId}
```

<a id="update-user-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| userGroupId | URL | UUID | Y | User group identifier |

<a id="update-user-group-request-body"></a>
#### Request Body

<details>
  <summary><strong>Example Code</strong></summary>

```json
{
    "userGroupName": "userGroupName-example",
    "memberIds": [],
    "selectAllYN": false
}
```

</details>

| Name | Format | Required | Description |
|-----|-----|-----|-----|
| userGroupName | String | Y | Name to identify user groups |
| memberIds | Array | N | Project member identifiers |
| selectAllYN | Boolean | N | Whether to include all project members<br/>- Default: `false` |

<a id="update-user-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="notification-group"></a>
## Notification Group { #notification-group }

<a id="get-notification-groups"></a>
### List Notification Groups { #get-notification-groups }

<a id="get-notification-groups-request"></a>
#### Request

```http
GET /v3.0/notification-groups
```

<a id="get-notification-groups-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-notification-groups-response"></a>
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

<a id="create-notification-group-request"></a>
#### Request

```http
POST /v3.0/notification-groups
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

<a id="delete-notification-group-request"></a>
#### Request

```http
DELETE /v3.0/notification-groups/{notificationGroupId}
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

<a id="get-notification-group"></a>
### View Notification Group Details { #get-notification-group }

<a id="get-notification-group-request"></a>
#### Request

```http
GET /v3.0/notification-groups/{notificationGroupId}
```

<a id="get-notification-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| notificationGroupId | URL | UUID | Y | Notification group identifier |

<a id="get-notification-group-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-notification-group-response"></a>
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

<a id="update-notification-group"></a>
### Modify Notification Group { #update-notification-group }

<a id="update-notification-group-request"></a>
#### Request

```http
PUT /v3.0/notification-groups/{notificationGroupId}
```

<a id="update-notification-group-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| notificationGroupId | URL | UUID | Y | Notification group identifier |

<a id="update-notification-group-request-body"></a>
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

<a id="update-notification-group-response"></a>
#### Response

This API does not return a response body.

---

<a id="monitoring"></a>
## Monitoring { #monitoring }

<a id="get-metric-statistics"></a>
### View Stats { #get-metric-statistics }

<a id="get-metric-statistics-request"></a>
#### Request

```http
GET /v3.0/metric-statistics
```

<a id="get-metric-statistics-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| dbInstanceId | Query | UUID | Y | DB instance identifier |
| measureNames | Query | Array | Y | List of performance metrics to query |
| from | Query | DateTime | Y | Start date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| to | Query | DateTime | Y | End date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| interval | Query | Number | N | View interval<br/>- Unit: `minute`<br/>- Default: An appropriate value is automatically selected based on the start and end date and time |

<a id="get-metric-statistics-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-metric-statistics-response"></a>
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

<a id="get-metrics"></a>
### List Metrics { #get-metrics }

<a id="get-metrics-request"></a>
#### Request

```http
GET /v3.0/metrics
```

<a id="get-metrics-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-metrics-response"></a>
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

<a id="get-event-codes"></a>
### List Subscribable Event Codes { #get-event-codes }

<a id="get-event-codes-request"></a>
#### Request

```http
GET /v3.0/event-codes
```

<a id="get-event-codes-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-event-codes-response"></a>
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

<a id="get-events"></a>
### List Events { #get-events }

<a id="get-events-request"></a>
#### Request

```http
GET /v3.0/events
```

<a id="get-events-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| page | Query | Number | Y | Page to retrieve<br/>- Minimum value: `1` |
| size | Query | Number | Y | Page size to retrieve<br/>- Minimum value: `1`<br/>- Maximum value: `100` |
| from | Query | DateTime | Y | Start date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| to | Query | DateTime | Y | End date and time (YYYY-MM-DDThh:mm:ss.SSSTZD) |
| eventCategoryType | Query | Enum | Y | Event category types to query<br/>- `ALL`<br/>- `INSTANCE`<br/>- `DB_SECURITY_GROUP`<br/>- `MONITORING`<br/>- `JOB`<br/>- `BACKUP`<br/>- `TENANT` |
| sourceId | Query | UUID | N | Event target resource identifier |
| keyword | Query | String | N | String keyword in event message |
| ascendingOrder | Query | Enum | N | Event message sorting order<br/>- Default value: `DESC`<br/>- `ASC`<br/>- `DESC` |

<a id="get-events-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-events-response"></a>
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

<a id="get-event-subscriptions"></a>
### List Event Subscriptions { #get-event-subscriptions }

<a id="get-event-subscriptions-request"></a>
#### Request

```http
GET /v3.0/event-subscriptions
```

<a id="get-event-subscriptions-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| page | Query | Number | Y | Page to retrieve<br/>- Minimum value: `1` |
| size | Query | Number | Y | Page size to retrieve<br/>- Minimum value: `1`<br/>- Maximum value: `100` |
| eventSubscriptionId | Query | UUID | N | Event subscription identifier |
| eventSubscriptionName | Query | String | N | Name to identify event subscription |
| userGroupId | Query | UUID | N | User group identifier |

<a id="get-event-subscriptions-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="get-event-subscriptions-response"></a>
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

<a id="register-event-subscription"></a>
### Create an Event Subscription { #register-event-subscription }

<a id="register-event-subscription-request"></a>
#### Request

```http
POST /v3.0/event-subscriptions
```

<a id="register-event-subscription-request-body"></a>
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

<a id="register-event-subscription-response"></a>
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

<a id="delete-event-subscription"></a>
### Delete an Event Subscription { #delete-event-subscription }

<a id="delete-event-subscription-request"></a>
#### Request

```http
DELETE /v3.0/event-subscriptions/{eventSubscriptionId}
```

<a id="delete-event-subscription-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| eventSubscriptionId | URL | UUID | Y | Event subscription identifier |

<a id="delete-event-subscription-request-body"></a>
#### Request Body

This API does not require a request body.

<a id="delete-event-subscription-response"></a>
#### Response

This API does not return a response body.

---

<a id="modify-event-subscription"></a>
### Modify an Event Subscription { #modify-event-subscription }

<a id="modify-event-subscription-request"></a>
#### Request

```http
PUT /v3.0/event-subscriptions/{eventSubscriptionId}
```

<a id="modify-event-subscription-request-parameters"></a>
#### Request Parameters

| Name | Type | Format | Required | Description |
|-----|-----|-----|-----|-----|
| eventSubscriptionId | URL | UUID | Y | Event subscription identifier |

<a id="modify-event-subscription-request-body"></a>
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

<a id="modify-event-subscription-response"></a>
#### Response

This API does not return a response body.

---

