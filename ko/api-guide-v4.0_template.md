<!-- pre-align:aligned sig=7de1400fff9a -->

<a id="database-rds-for-enginepascalcase-api-guide"></a>
## Database > RDS for {{engine.pascalCase}} > API 가이드 { #database-rds-for-enginepascalcase-api-guide }

<a id="rds-for-enginepascalcase-api-common-information"></a>
## RDS for {{engine.pascalCase}} API 공통 정보 { #rds-for-enginepascalcase-api-common-information }

<a id="api-endpoint"></a>
### API 엔드포인트 { #api-endpoint }

| 리전        | 엔드포인트                                         |
|-----------|-----------------------------------------------|
{{#each regions}}
| {{this.text.ko}} | {{this.endpoint}} |
{{/each}}

<a id="authentication-and-authorization"></a>
### 인증 및 권한 { #authentication-and-authorization }

RDS for {{engine.pascalCase}}은(는) API 호출 시 인증/인가를 위해 User Access Key 토큰을 사용합니다. User Access Key 토큰은 User Access Key를 기반으로 발급되는 Bearer 타입의 일시적 액세스 토큰입니다. User Access Key 토큰 발급 및 사용에 대한 자세한 내용은 [User Access Key 토큰](/nhncloud/ko/public-api/user-access-key-token)을 참고하세요.
발급 받은 토큰은 Appkey와 함께 요청 Header에 포함해야 합니다.

| 이름                  | 종류     | 형식     | 필수 | 설명                                                          |
|---------------------|--------|--------|----|-------------------------------------------------------------|
| X-TC-APP-KEY        | Header | String | O  | RDS for {{engine.pascalCase}} 서비스의 Appkey 또는 프로젝트 통합 Appkey |
| X-NHN-AUTHORIZATION | Header | String | O  | Public API로 발급 받은 Bearer 유형 토큰                              |


또한 프로젝트 멤버 역할에 따라 호출할 수 있는 API가 제한됩니다. `RDS for {{engine.pascalCase}} ADMIN`, `RDS for {{engine.pascalCase}} VIEWER`로 구분하여 권한을 부여할 수 있습니다.

* `RDS for {{engine.pascalCase}} ADMIN` 권한은 모든 기능을 사용 가능합니다.
* `RDS for {{engine.pascalCase}} VIEWER` 권한은 정보를 조회하는 기능만 사용 가능합니다.
    * DB 인스턴스를 생성, 수정, 삭제하거나, DB 인스턴스를 대상으로 하는 어떠한 기능도 사용할 수 없습니다.
    * 단, 알림 그룹 및 사용자 그룹 관련 기능은 사용 가능합니다.

API 요청 시 인증에 실패하거나 권한이 없을 경우 다음과 같은 오류가 발생합니다.

| resultCode | resultMessage | 설명          |
|------------|---------------|-------------|
| 80401      | Unauthorized  | 인증에 실패했습니다. |
| 80403      | Forbidden     | 권한이 없습니다.   |

<a id="common-response-information"></a>
### 응답 공통 정보 { #common-response-information }

모든 API 요청에 '200 OK'로 응답합니다. 자세한 응답 결과는 응답 본문의 헤더를 참고합니다.

<a id="common-response-information-response-body"></a>
#### 응답 본문
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

<a id="common-response-information-field"></a>
#### 필드
| 이름            | 형식      | 설명                                      |
|---------------|---------|-----------------------------------------|
| resultCode    | Number  | 결과 코드<br/>- 성공: `0`<br/>- 실패: `0`이 아닌 값 |
| resultMessage | String  | 결과 메시지                                  |
| isSuccessful  | Boolean | 성공 여부                                   |


<a id="db-engine-type"></a>
### DB 엔진 유형 { #db-engine-type }

{{#if (eq engine.lowerCase "mysql")}}
| DB 엔진 유형     | 생성 가능 여부 | OBS로부터 복원 가능 여부 | 인증 플러그인 지원 |
|--------------|----------|-----------------|--------|
| MYSQL\_V5633 | X        | X               | NATIVE |
| MYSQL\_V5715 | O        | O               | NATIVE |
| MYSQL\_V5719 | O        | O               | NATIVE |
| MYSQL\_V5726 | O        | O               | NATIVE |
| MYSQL\_V5731 | X        | X               | NATIVE |
| MYSQL\_V5733 | O        | X               | NATIVE, SHA256 |
| MYSQL\_V5737 | O        | O               | NATIVE, SHA256 |
| MYSQL\_V8018 | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL\_V8023 | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL\_V8028 | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL\_V8032 | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL\_V8033 | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL\_V8034 | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL_V8035  | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL_V8036  | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL_V8040  | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL_V8041  | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL_V8042  | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL_V8043  | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL_V8044  | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL_V8045  | O        | O               | NATIVE, CACHING_SHA2 |
| MYSQL_V8405  | O        | O               | CACHING_SHA2 |
| MYSQL_V8406  | O        | O               | CACHING_SHA2 |
| MYSQL_V8407  | O        | O               | CACHING_SHA2 |
| MYSQL_V8408  | O        | O               | CACHING_SHA2 |
{{/if}}
{{#if (eq engine.lowerCase "mariadb")}}
| DB 엔진 유형        | 생성 가능 여부 | OBS로부터 복원 가능 여부 | 인증 플러그인 지원 |
|-----------------|----------|------------------|--|
| MARIADB_V10330  | O        | O                | NATIVE, ED25519 |
| MARIADB_V10611  | O        | O                | NATIVE, ED25519 |
| MARIADB_V10612  | O        | O                | NATIVE, ED25519 |
| MARIADB_V10616  | O        | O                | NATIVE, ED25519 |
| MARIADB_V10622  | O        | O                | NATIVE, ED25519 |
| MARIADB_V101107 | O        | O                | NATIVE, ED25519 |
| MARIADB_V101108 | O        | O                | NATIVE, ED25519 |
| MARIADB_V101113 | O        | O                | NATIVE, ED25519 |
| MARIADB_V11407  | O        | O                | NATIVE, ED25519 |
{{/if}}

* ENUM 타입의 dbVersion 필드에서 해당 값을 사용할 수 있습니다.
* 버전에 따라 생성 또는 복원이 불가능한 경우가 있을 수 있습니다.

<a id="project-information"></a>
## 프로젝트 정보 { #project-information }

<a id="list-regions"></a>
### 리전 목록 보기 { #list-regions }

```http
GET /v4.0/project/regions
```

<a id="list-regions-required-permissions"></a>
#### 필요 권한

| 권한명                                     | 설명         |
|-----------------------------------------|------------|
| RDSfor{{engine.pascalCase}}:Project.Get | 프로젝트 정보 조회 |

<a id="list-regions-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-regions-response"></a>
#### 응답

| 이름                 | 종류   | 형식      | 설명                                                                         |
|--------------------|------|---------|----------------------------------------------------------------------------|
| regions            | Body | Array   | 리전 목록                                                                      |
{{#if (eq engine.lowerCase "mysql")}}
| regions.regionCode | Body | Enum    | 리전 코드<br/>- `KR1`: 한국(판교) 리전<br/>- `KR2`: 한국(평촌) 리전<br/>- `JP1`: 일본(도쿄) 리전 |
{{/if}}
{{#if (eq engine.lowerCase "mariadb")}}
| regions.regionCode | Body | Enum    | 리전 코드<br/>- `KR1`: 한국(판교) 리전 |
{{/if}}
| regions.isEnabled  | Body | Boolean | 리전의 활성화 여부                                                                 |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "regions": [
{{#if (eq engine.lowerCase "mysql")}}    
        {
            "regionCode": "KR1",
            "isEnabled": true
        },
        {
            "regionCode": "KR2",
            "isEnabled": true
        },
        {
            "regionCode": "JP1",
            "isEnabled": true
        }
{{/if}}
{{#if (eq engine.lowerCase "mariadb")}}
        {
            "regionCode": "KR1",
            "isEnabled": true
        }
{{/if}}
    ]
}
```

</details>

---

<a id="list-project-members"></a>
### 프로젝트 멤버 목록 보기 { #list-project-members }

```http
GET /v4.0/project/members
```

<a id="list-project-members-required-permissions"></a>
#### 필요 권한

| 권한명                                     | 설명         |
|-----------------------------------------|------------|
| RDSfor{{engine.pascalCase}}:Project.Get | 프로젝트 정보 조회 |

<a id="list-project-members-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-project-members-response"></a>
#### 응답

| 이름                   | 종류   | 형식     | 설명              |
|----------------------|------|--------|-----------------|
| members              | Body | Array  | 프로젝트 멤버 목록      |
| members.memberId     | Body | UUID   | 프로젝트 멤버의 식별자    |
| members.memberName   | Body | String | 프로젝트 멤버의 이름     |
| members.emailAddress | Body | String | 프로젝트 멤버의 이메일 주소 |
| members.phoneNumber  | Body | String | 프로젝트 멤버의 전화번호   |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "members": [
        {
            "memberId": "1b1d3627-507a-49ea-8cb7-c86dfa9caa58",
            "memberName": "홍길동",
            "emailAddress": "gildong.hong@nhn.com",
            "phoneNumber": "+821012345678"
        }
    ]
}
```

</p>
</details>

---

<a id="specifications-of-db-instance"></a>
## DB 인스턴스 사양 { #specifications-of-db-instance }

<a id="list-db-instance-specifications"></a>
### DB 인스턴스 사양 목록 보기 { #list-db-instance-specifications }

```http
GET /v4.0/db-flavors
```

<a id="list-db-instance-specifications-required-permissions"></a>
#### 필요 권한

| 권한명                                       | 설명               |
|-------------------------------------------|------------------|
| RDSfor{{engine.pascalCase}}:DbFlavor.List | DB 인스턴스 사양 목록 보기 |

<a id="list-db-instance-specifications-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-db-instance-specifications-response"></a>
#### 응답

| 이름                     | 종류   | 형식     | 설명              |
|------------------------|------|--------|-----------------|
| dbFlavors              | Body | Array  | DB 인스턴스 사양 목록   |
| dbFlavors.dbFlavorId   | Body | UUID   | DB 인스턴스 사양의 식별자 |
| dbFlavors.dbFlavorName | Body | String | DB 인스턴스 사양 이름   |
| dbFlavors.ram          | Body | Number | 메모리 용량(MB)      |
| dbFlavors.vcpus        | Body | Number | CPU 코어 수        |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbFlavors": [
        {
            "dbFlavorId": "50be6d9c-02d6-4594-a2d4-12010eb65ec0",
            "dbFlavorName": "m2.c1m2",
            "ram": 2048,
            "vcpus": 1
        }
    ]
}
```

</p>
</details>

---

<a id="network"></a>
## 네트워크 { #network }

<a id="list-subnets"></a>
### 서브넷 목록 보기 { #list-subnets }

```http
GET /v4.0/network/subnets
```

<a id="list-subnets-required-permissions"></a>
#### 필요 권한

| 권한명                                      | 설명        |
|------------------------------------------|-----------|
| RDSfor{{engine.pascalCase}}:Network.List | 서브넷 목록 보기 |

<a id="list-subnets-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-subnets-response"></a>
#### 응답

| 이름                       | 종류   | 형식      | 설명               |
|--------------------------|------|---------|------------------|
| subnets                  | Body | Array   | 서브넷 목록           |
| subnets.subnetId         | Body | UUID    | 서브넷의 식별자         |
| subnets.subnetName       | Body | String  | 서브넷을 식별할 수 있는 이름 |
| subnets.subnetCidr       | Body | String  | 서브넷의 CIDR        |
| subnets.usingGateway     | Body | Boolean | 게이트웨이 사용 여부      |
| subnets.availableIpCount | Body | Number  | 사용 가능한 IP 수      |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "subnets": [
        {
            "subnetId": "1b2a9b23-0725-4b92-8c78-35db66b8ad9f",
            "subnetName": "Default Network",
            "subnetCidr": "192.168.0.0/24",
            "usingGateway": true,
            "availableIpCount": 240
        }
    ]
}
```

</p>
</details>

---

<a id="db-engine"></a>
## DB 엔진 { #db-engine }

<a id="list-db-engines"></a>
### DB 엔진 목록 보기 { #list-db-engines }

```http
GET /v4.0/db-versions
```

<a id="list-db-engines-required-permissions"></a>
#### 필요 권한

| 권한명                                        | 설명          |
|--------------------------------------------|-------------|
| RDSfor{{engine.pascalCase}}:DbVersion.List | DB 엔진 목록 보기 |

<a id="list-db-engines-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-db-engines-response"></a>
#### 응답

| 이름                           | 종류   | 형식      | 설명                    |
|------------------------------|------|---------|-----------------------|
| dbVersions                   | Body | Array   | DB 엔진 목록              |
| dbVersions.dbVersion         | Body | String  | DB 엔진 유형              |
| dbVersions.dbVersionName     | Body | String  | DB 엔진 이름              |
| dbVersions.restorableFromObs | Body | Boolean | 오브젝트 스토리지로부터 복원 가능 여부 |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbVersions": [
        {
            "dbVersion": "{{engine.sampleDbVersionCode}}",
            "dbVersionName": "{{engine.sampleDbVersionName}}",
            "restorableFromObs": true
        }
    ]
}
```

</p>
</details>

---

<a id="storage"></a>
## 데이터 스토리지 { #storage }

<a id="list-storage-type"></a>
### 데이터 스토리지 타입 목록 보기 { #list-storage-type }

```http
GET /v4.0/storage-types
```

<a id="list-storage-type-required-permissions"></a>
#### 필요 권한

| 권한명                                      | 설명                |
|------------------------------------------|-------------------|
| RDSfor{{engine.pascalCase}}:Storage.List | 데이터 스토리지 타입 목록 보기 |

<a id="list-storage-type-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-storage-type-response"></a>
#### 응답

| 이름           | 종류   | 형식    | 설명             |
|--------------|------|-------|----------------|
| storageTypes | Body | Array | 데이터 스토리지 타입 목록 |

<details><summary>예시</summary>
<p>

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

</p>
</details>

---

<a id="task-information"></a>
## 작업 정보 { #task-information }

<a id="task-status"></a>
### 작업 상태 { #task-status }

| 상태명                | 설명                   |
|--------------------|----------------------|
| `PREPARING`        | 작업이 준비 중인 경우         |
| `READY`            | 작업이 준비 완료된 경우        |
| `RUNNING`          | 작업이 진행 중인 경우         |
| `COMPLETED`        | 작업이 완료된 경우           |
| `REGISTERED`       | 작업이 등록된 경우           |
| `WAIT_TO_REGISTER` | 작업 등록 대기 중인 경우       |
| `INTERRUPTED`      | 작업 진행 중 인터럽트가 발생한 경우 |
| `CANCELED`         | 작업이 취소된 경우           |
| `FAILED`           | 작업이 실패한 경우           |
| `ERROR`            | 작업 진행 중 오류가 발생한 경우   |
| `DELETED`          | 작업이 삭제된 경우           |
| `FAIL_TO_READY`    | 작업 준비에 실패한 경우        |

<a id="list-task-details"></a>
### 작업 정보 상세 보기 { #list-task-details }

```http
GET /v4.0/jobs/{jobId}
```

<a id="list-task-details-required-permissions"></a>
#### 필요 권한

| 권한명                                 | 설명          |
|-------------------------------------|-------------|
| RDSfor{{engine.pascalCase}}:Job.Get | 작업 정보 상세 보기 |

<a id="list-task-details-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름    | 종류  | 형식   | 필수 | 설명      |
|-------|-----|------|----|---------|
| jobId | URL | UUID | O  | 작업의 식별자 |

<a id="list-task-details-response"></a>
#### 응답

| 이름                             | 종류   | 형식       | 설명                                |
|--------------------------------|------|----------|-----------------------------------|
| jobId                          | Body | UUID     | 작업의 식별자                           |
| jobStatus                      | Body | Enum     | 작업의 현재 상태                         |
| resourceRelations              | Body | Array    | 연관 리소스 목록                         |
| resourceRelations.resourceType | Body | Enum     | 연관 리소스 유형                         |
| resourceRelations.resourceId   | Body | UUID     | 연관 리소스의 식별자                       |
| createdYmdt                    | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt                    | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "jobId": "0ddb042c-5af6-43fb-a914-f4dd0540eb7c",
    "jobStatus": "RUNNING",
    "resourceRelations": [
        {
            "resourceType": "DB_INSTANCE",
            "resourceId": "56b39dcf-65eb-47ec-9d4f-09f160ba2266"
        }
    ],
    "createdYmdt": "2023-02-22T20:47:12+09:00",
    "updatedYmdt": "2023-02-22T20:49:46+09:00"
}
```

</p>
</details>

---

<a id="db-instance-group"></a>
## DB 인스턴스 그룹 { #db-instance-group }

<a id="list-db-instance-groups"></a>
### DB 인스턴스 그룹 목록 보기 { #list-db-instance-groups }

```http
GET /v4.0/db-instance-groups
```

<a id="list-db-instance-groups-required-permissions"></a>
#### 필요 권한

| 권한명                                              | 설명               |
|--------------------------------------------------|------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceGroup.List | DB 인스턴스 그룹 목록 보기 |

<a id="list-db-instance-groups-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-db-instance-groups-response"></a>
#### 응답

| 이름                                 | 종류   | 형식       | 설명                                                                       |
|------------------------------------|------|----------|--------------------------------------------------------------------------|
| dbInstanceGroups                   | Body | Array    | DB 인스턴스 그룹 목록                                                            |
| dbInstanceGroups.dbInstanceGroupId | Body | UUID     | DB 인스턴스 그룹의 식별자                                                          |
| dbInstanceGroups.replicationType   | Body | Enum     | DB 인스턴스 그룹의 복제 형태<br/>- `STANDALONE`: 단일<br/>- `HIGH_AVAILABILITY`: 고가용성 |
| dbInstanceGroups.createdYmdt       | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                        |
| dbInstanceGroups.updatedYmdt       | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                        |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbInstanceGroups": [
        {
            "dbInstanceGroupId": "05de0746-89fd-49c8-94f9-9c5b1df97009",
            "replicationType": "STANDALONE",
            "createdYmdt": "2023-02-13T17:35:20+09:00",
            "updatedYmdt": "2023-02-13T17:35:20+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="list-db-instance-group-details"></a>
### DB 인스턴스 그룹 상세 보기 { #list-db-instance-group-details }

```http
GET /v4.0/db-instance-groups/{dbInstanceGroupId}
```

<a id="list-db-instance-group-details-required-permissions"></a>
#### 필요 권한

| 권한명                                             | 설명               |
|-------------------------------------------------|------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceGroup.Get | DB 인스턴스 그룹 상세 보기 |

<a id="list-db-instance-group-details-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름                | 종류  | 형식   | 필수 | 설명              |
|-------------------|-----|------|----|-----------------|
| dbInstanceGroupId | URL | UUID | O  | DB 인스턴스 그룹의 식별자 |

<a id="list-db-instance-group-details-response"></a>
#### 응답

| 이름                           | 종류   | 형식       | 설명                                                                                                                                    |
|------------------------------|------|----------|---------------------------------------------------------------------------------------------------------------------------------------|
| dbInstanceGroupId            | Body | UUID     | DB 인스턴스 그룹의 식별자                                                                                                                       |
| replicationType              | Body | Enum     | DB 인스턴스 그룹의 복제 형태<br/>- `STANDALONE`: 단일<br/>- `HIGH_AVAILABILITY`: 고가용성                                                              |
| dbInstances                  | Body | Array    | DB 인스턴스 그룹에 속한 DB 인스턴스 목록                                                                                                             |
| dbInstances.dbInstanceId     | Body | UUID     | DB 인스턴스의 식별자                                                                                                                          |
| dbInstances.dbInstanceType   | Body | Enum     | DB 인스턴스의 역할 타입<br/>- `MASTER`: 마스터<br/>- `FAILED_MASTER`: 장애 조치된 마스터<br/>- `CANDIDATE_MASTER`: 예비 마스터<br/>- `READ_ONLY_SLAVE`: 읽기 복제본 |
| dbInstances.dbInstanceStatus | Body | Enum     | DB 인스턴스의 현재 상태                                                                                                                        |
| createdYmdt                  | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                                     |
| updatedYmdt                  | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                                     |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbInstanceGroupId": "36617a8e-0df8-4b16-b6ea-6306019e95da",
    "replicationType": "STANDALONE",
    "dbInstances": [
        {
            "dbInstanceId": "6d2db0ef-fe9b-4ed4-97b1-d97fcb4cf1b8",
            "dbInstanceType": "MASTER",
            "dbInstanceStatus": "AVAILABLE"
        }
    ],
    "createdYmdt": "2023-03-03T17:38:14+09:00",
    "updatedYmdt": "2023-03-03T17:38:14+09:00"
}
```

</p>
</details>

---

<a id="db-instance"></a>
## DB 인스턴스 { #db-instance }

<a id="db-instance-status"></a>
### DB 인스턴스 상태 { #db-instance-status }

| 상태                  | 설명                           |
|---------------------|------------------------------|
| `AVAILABLE`         | DB 인스턴스가 사용 가능한 경우           |
| `BEFORE_CREATE`     | DB 인스턴스가 생성 전인 경우            |
| `STORAGE_FULL`      | DB 인스턴스의 용량이 부족한 경우          |
| `FAIL_TO_CREATE`    | DB 인스턴스 생성에 실패한 경우           |
| `FAIL_TO_CONNECT`   | DB 인스턴스 연결에 실패한 경우           |
| `REPLICATION_STOP`  | DB 인스턴스의 복제가 중단된 경우          |
| `FAILOVER`          | DB 인스턴스가 고가용성 장애 조치된 경우      |
| `SHUTDOWN`          | DB 인스턴스가 중지된 경우              |
| `DELETED`           | DB 인스턴스가 삭제된 경우              |

<a id="db-instance-progress-status"></a>
### DB 인스턴스 진행 상태 { #db-instance-progress-status }

| 상태                         | 설명           |
|----------------------------|--------------|
| `APPLYING_PARAMETER_GROUP` | 파라미터 그룹 적용 중 |
| `BACKING_UP`               | 백업 중         |
| `CANCELING`                | 취소 중         |
| `CREATING`                 | 생성 중         |
| `CREATING_SCHEMA`          | DB 스키마 생성 중	 |
| `CREATING_USER`            | 사용자 생성 중	    |
| `DELETING`                 | 삭제 중         |
| `DELETING_SCHEMA`          | DB 스키마 삭제 중  |
| `DELETING_USER`            | 사용자 삭제 중     |
| `EXPORTING_BACKUP`         | 백업을 내보내는 중   |
| `FAILING_OVER`             | 장애 조치 중      |
| `MIGRATING`                | 마이그레이션 중     |
| `MODIFYING`                | 수정 중         |
| `PREPARING`                | 준비 중         |
| `PROMOTING`                | 승격 중         |
| `REBUILDING`               | 재구축 중        |
| `REPAIRING`                | 복구 중         |
| `REPLICATING`              | 복제 중         |
| `RESTARTING`               | 재시작 중        |
| `RESTARTING_FORCIBLY`      | 강제 재시작 중     |
| `RESTORING`                | 복원 중         |
| `STARTING`                 | 시작 중         |
| `STOPPING`                 | 정지 중         |
| `SYNCING_SCHEMA`           | DB 스키마 동기화 중 |
| `SYNCING_USER`             | 사용자 동기화 중	   |
| `UPDATING_USER`            | 사용자 수정 중	    |

<a id="list-db-instances"></a>
### DB 인스턴스 목록 보기 { #list-db-instances }

```http
GET /v4.0/db-instances
```

<a id="list-db-instances-required-permissions"></a>
#### 필요 권한

| 권한명                                         | 설명            |
|---------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstance.List | DB 인스턴스 목록 보기 |

<a id="list-db-instances-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-db-instances-response"></a>
#### 응답

| 이름                            | 종류   | 형식       | 설명                                                                                                                                    |
|-------------------------------|------|----------|---------------------------------------------------------------------------------------------------------------------------------------|
| dbInstances                   | Body | Array    | DB 인스턴스 목록                                                                                                                            |
| dbInstances.dbInstanceId      | Body | UUID     | DB 인스턴스의 식별자                                                                                                                          |
| dbInstances.dbInstanceGroupId | Body | UUID     | DB 인스턴스 그룹의 식별자                                                                                                                       |
| dbInstances.dbInstanceName    | Body | String   | DB 인스턴스를 식별할 수 있는 이름                                                                                                                  |
| dbInstances.description       | Body | String   | DB 인스턴스에 대한 추가 정보                                                                                                                     |
| dbInstances.dbVersion         | Body | Enum     | DB 엔진 유형                                                                                                                              |
| dbInstances.dbPort            | Body | Number   | DB 포트                                                                                                                                 |
| dbInstances.dbInstanceType    | Body | Enum     | DB 인스턴스의 역할 타입<br/>- `MASTER`: 마스터<br/>- `FAILED_MASTER`: 장애 조치된 마스터<br/>- `CANDIDATE_MASTER`: 예비 마스터<br/>- `READ_ONLY_SLAVE`: 읽기 복제본 |
| dbInstances.dbInstanceStatus  | Body | Enum     | DB 인스턴스의 현재 상태                                                                                                                        |
| dbInstances.progressStatus    | Body | Enum     | DB 인스턴스의 현재 진행 상태                                                                                                                     |
| dbInstances.createdYmdt       | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                                     |
| dbInstances.updatedYmdt       | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                                     |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbInstances": [
        {
            "dbInstanceId": "d067593b-1acc-4ccc-9e8a-cc72d6d79ec3",
            "dbInstanceGroupId": "51c7d080-ff36-4025-84b1-9d9d0b4fe9e0",
            "dbInstanceName": "db-instance",
            "description": null,
            "dbVersion": "{{engine.sampleDbVersionCode}}",
            "dbPort": 10000,
            "dbInstanceType": "MASTER",
            "dbInstanceStatus": "AVAILABLE",
            "progressStatus": "NONE",
            "createdYmdt": "2023-01-23T12:03:13+09:00",
            "updatedYmdt": "2023-02-02T17:20:17+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="list-db-instance-details"></a>
### DB 인스턴스 상세 보기 { #list-db-instance-details }

```http
GET /v4.0/db-instances/{dbInstanceId}
```

<a id="list-db-instance-details-required-permissions"></a>
#### 필요 권한

| 권한명                                        | 설명            |
|--------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Get | DB 인스턴스 상세 보기 |

<a id="list-db-instance-details-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="list-db-instance-details-response"></a>
#### 응답

| 이름                          | 종류   | 형식       | 설명                                                                                                                                    |
|-----------------------------|------|----------|---------------------------------------------------------------------------------------------------------------------------------------|
| dbInstanceId                | Body | UUID     | DB 인스턴스의 식별자                                                                                                                          |
| dbInstanceGroupId           | Body | UUID     | DB 인스턴스 그룹의 식별자                                                                                                                       |
| dbInstanceName              | Body | String   | DB 인스턴스를 식별할 수 있는 이름                                                                                                                  |
| description                 | Body | String   | DB 인스턴스에 대한 추가 정보                                                                                                                     |
| dbVersion                   | Body | Enum     | DB 엔진 유형                                                                                                                              |
| dbPort                      | Body | Number   | DB 포트                                                                                                                                 |
| dbInstanceType              | Body | Enum     | DB 인스턴스의 역할 타입<br/>- `MASTER`: 마스터<br/>- `FAILED_MASTER`: 장애 조치된 마스터<br/>- `CANDIDATE_MASTER`: 예비 마스터<br/>- `READ_ONLY_SLAVE`: 읽기 복제본 |
| dbInstanceStatus            | Body | Enum     | DB 인스턴스의 현재 상태                                                                                                                        |
| progressStatus              | Body | Enum     | DB 인스턴스의 현재 작업 진행 상태                                                                                                                  |
| dbFlavorId                  | Body | UUID     | DB 인스턴스 사양의 식별자                                                                                                                       |
| parameterGroupId            | Body | UUID     | DB 인스턴스에 적용된 파라미터 그룹의 식별자                                                                                                             |
| dbSecurityGroupIds          | Body | Array    | DB 인스턴스에 적용된 DB 보안 그룹의 식별자 목록                                                                                                         |
| notificationGroupIds        | Body | Array    | DB 인스턴스에 적용된 알림 그룹의 식별자 목록                                                                                                            |
| useDeletionProtection       | Body | Boolean  | DB 인스턴스 삭제 보호 여부                                                                                                                      |
| useSlowQueryAnalysis        | Body | Boolean  | Slow query 분석 여부                                                                                                                      |
| supportAuthenticationPlugin | Body | Boolean  | 인증 플러그인 지원 여부                                                                                                                         |
| needToApplyParameterGroup   | Body | Boolean  | 최신 파라미터 그룹 적용 필요 여부                                                                                                                   |
| needMigration               | Body | Boolean  | 마이그레이션 필요 여부                                                                                                                          |
| supportDbVersionUpgrade     | Body | Boolean  | DB 버전 업그레이드 지원 여부                                                                                                                     |
| createdYmdt                 | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                                     |
| updatedYmdt                 | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                                     |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbInstanceId": "d067593b-1acc-4ccc-9e8a-cc72d6d79ec3",
    "dbInstanceGroupId": "51c7d080-ff36-4025-84b1-9d9d0b4fe9e0",
    "dbInstanceName": "db-instance",
    "description": null,
    "dbVersion": "{{engine.sampleDbVersionCode}}",
    "dbPort": 10000,
    "dbInstanceType": "MASTER",
    "dbInstanceStatus": "AVAILABLE",
    "progressStatus": "NONE",
    "dbFlavorId": "e9ed4ef6-78d7-46fa-ace9-32481e97f3b7",
    "parameterGroupId": "b03e8b13-de27-4d04-a488-ff5689589372",
    "dbSecurityGroupIds": ["01908c35-d2c9-4852-baf0-17f06ec42c03"],
    "notificationGroupIds": ["83a62a33-ddbf-4a04-8653-e54463d5b1ac"],
    "useDeletionProtection": false,
    "useSlowQueryAnalysis": true,
    "supportAuthenticationPlugin": true,
    "needToApplyParameterGroup": false,
    "needMigration": false,
    "supportDbVersionUpgrade": true,
    "createdYmdt": "2022-11-23T12:03:13+09:00",
    "updatedYmdt": "2022-12-02T17:20:17+09:00"
}
```

</p>
</details>

---

<a id="create-db-instance"></a>
### DB 인스턴스 생성하기 { #create-db-instance }

```http
POST /v4.0/db-instances
```

<a id="create-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                           | 설명           |
|-----------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Create | DB 인스턴스 생성하기 |

<a id="create-db-instance-request"></a>
#### 요청

| 이름                      | 종류    | 형식      | 필수 | 설명                                                                  |
|-------------------------|-------|---------|----|---------------------------------------------------------------------|
| dbInstanceName          | Body  | String  | O  | DB 인스턴스를 식별할 수 있는 마스터 이름                                            |
| dbInstanceCandidateName | Body  | String  | O  | DB 인스턴스를 식별할 수 있는 예비 마스터 이름(고가용성 사용 시 필수 값)                         |
| description             | Body  | String  | X  | DB 인스턴스에 대한 추가 정보                                                   |
| dbFlavorId              | Body  | UUID    | O  | DB 인스턴스 사양의 식별자                                                     |
| dbVersion               | Body  | Enum    | O  | DB 엔진 유형                                                            |
| dbPort                  | Body  | Number  | O  | DB 포트<br/>- 최솟값: `3306`<br/>- 최댓값: `43306`                          |
| dbUserName              | Body  | String  | O  | DB 사용자 계정명                                                          |
| dbPassword              | Body  | String  | O  | DB 사용자 계정 암호<br/>- 최소 길이: `4`<br/>- 최대 길이: `256`                    |
| parameterGroupId        | Body  | UUID    | O  | 파라미터 그룹의 식별자                                                        |
| dbSecurityGroupIds      | Body  | Array   | X  | DB 보안 그룹의 식별자 목록                                                    |
| userGroupIds            | Body  | Array   | X  | 사용자 그룹의 식별자 목록                                                      |
| useHighAvailability     | Body  | Boolean | X  | 고가용성 사용 여부<br/>- 기본값: `false`                                       |
| pingInterval            | Body  | Number  | X  | 고가용성 사용 시 Ping 간격(초)<br/>- 기본값: `3`<br/>- 최솟값: `1`<br/>- 최댓값: `600` |
| pingType                | Body  | Enum    | X  | 고가용성 사용 시 Ping 타입<br/>- 기본값: `INSERT`<br/>- `INSERT`<br/>- `SELECT` |
| useDefaultNotification  | Body  | Boolean | X  | 기본 알림 사용 여부<br/>- 기본값: `false`                                      |
| useDeletionProtection   | Body  | Boolean | X  | 삭제 보호 여부<br/>- 기본값: `false`                                         |
| useSlowQueryAnalysis    | Body  | Boolean | X  | Slow query 분석 여부<br/>- 기본값: `true`                                  |
{{#if (eq engine.lowerCase "mysql")}}
| authenticationPlugin                         | Body | Enum    | X  | 인증 플러그인<br/>- 기본값: `NATIVE`(미지원 시 `CACHING_SHA2`)<br/>- NATIVE: `mysql_native_password`<br />- SHA256: `sha256_password`<br />- CACHING_SHA2: `caching_sha2_password`                                                                                                     |
| tlsOption                                    | Body | Enum    | X  | TLS Option<br/>- NONE<br />- SSL<br />- X509                                                                                                                                                                                |
{{/if}}
{{#if (eq engine.lowerCase "mariadb")}}
| authenticationPlugin                         | Body | Enum    | X  | 인증 플러그인<br/>- 기본값: `NATIVE`(미지원 시 `ED25519`)<br/>- NATIVE: `mysql_native_password`<br />- ED25519: `auth_ed25519` |
{{/if}}
| network                                      | Body | Object  | O  | 네트워크 정보 객체                                                                                                                                                                                                                  |
| network.subnetId                             | Body | UUID    | O  | 서브넷의 식별자                                                                                                                                                                                                                    |
| network.usePublicAccess                      | Body | Boolean | X  | 외부 접속 가능 여부<br/>- 기본값: `false`                                                                                                                                                                                             |
| network.availabilityZone                     | Body | Enum    | O  | DB 인스턴스를 생성할 가용성 영역<br/>- 예시: `kr-pub-a`                                                                                                                                                                                    |
| storage                                      | Body | Object  | O  | 데이터 스토리지 정보 객체                                                                                                                                                                                                                  |    
| storage.storageType                          | Body | Enum    | O  | 데이터 스토리지 타입<br/>- 예시: `General SSD`                                                                                                                                                                                         |
| storage.storageSize                          | Body | Number  | O  | 데이터 스토리지 크기(GB)<br/>- 최솟값: `20`<br/>- 최댓값: `2048`                                                                                                                                                                           |
| storage.storageAutoscale                     | Body | Object  | X  | 데이터 스토리지 자동 확장 객체                                                   |
| storage.storageAutoscale.useStorageAutoscale | Body | Boolean | X  | 스토리지 자동 확장 여부                                                       |
| storage.storageAutoscale.threshold           | Body | Number  | X  | 자동 확장 조건(%)<br/>- 최솟값: `50`<br/>- 최댓값: `95`                         |
| storage.storageAutoscale.maxStorageSize      | Body | Number  | X  | 자동 확장 최대 크기(GB)<br/>- 최댓값: `4096`                                   |
| storage.storageAutoscale.cooldownTime        | Body | Number  | X  | 자동 확장 쿨다운 시간(분)<br/>- 최솟값: `10`<br/>- 최댓값: `1440`                   |
| backup                                       | Body | Object  | O  | 백업 정보 객체                                                                                                                                                                                                                    |
| backup.backupPeriod                          | Body | Number  | O  | 백업 보관 기간(일)<br/>- 최솟값: `0`<br/>- 최댓값: `730`                                                                                                                                                                                 |
| backup.ftwrlWaitTimeout                      | Body | Number  | X  | 쿼리 지연 대기 시간(초)<br/>- 기본값: `1800`<br/>- 최솟값: `0`<br/>- 최댓값: `21600`                                                                                                                                                          |
| backup.backupRetryCount                      | Body | Number  | X  | 백업 재시도 횟수<br/>- 기본값: `0`<br/>- 최솟값: `0`<br/>- 최댓값: `10`                                                                                                                                                                     |
{{#if (eq engine.lowerCase "mysql")}}    
| backup.replicationRegion                     | Body | Enum    | X  | 백업 복제 리전<br />- `KR1`: 한국(판교) 리전<br/>- `KR2`: 한국(평촌) 리전<br/>- `JP1`: 일본(도쿄) 리전                                                                                                                                                      |
{{/if}}
| backup.useBackupLock                         | Body | Boolean | X  | 테이블 잠금 사용 여부<br/>- 기본값: `true`                                                                                                                                                                                              |
| backup.backupSchedules                       | Body | Array   | O  | 예정된 자동 백업 목록                                                                                                                                                                                                                   |
| backup.backupSchedules.backupWndBgnTime      | Body | String  | O  | 백업 시작 시각<br/>- 예시: `00:00:00`                                                                                                                                                                                               |
| backup.backupSchedules.backupWndDuration     | Body | Enum    | O  | 백업 Duration<br/>백업 시작 시각부터 Duration 안에 자동 백업이 실행됩니다.<br/>- `HALF_AN_HOUR`: 30분<br/>- `ONE_HOUR`: 1시간<br/>- `ONE_HOUR_AND_HALF`: 1시간 30분<br/>- `TWO_HOURS`: 2시간<br/>- `TWO_HOURS_AND_HALF`: 2시간 30분<br/>- `THREE_HOURS`: 3시간 |

<details><summary>예시</summary>
<p>

```json
{
    "dbInstanceName": "db-instance",
    "description": "description",
    "dbFlavorId": "71f69bf9-3c01-4c1a-b135-bb75e93f6268",
    "dbVersion": "{{engine.sampleDbVersionCode}}",
    "dbPort": 10000,
    "dbUserName": "db-user",
    "dbPassword": "password",
    "parameterGroupId": "488bf4f5-d8f7-459b-ace6-529b606c8570",
    "dbSecurityGroupIds": [
        "b0483a3d-e8e2-46f6-9e84-d5e31b0d44f4"
    ],
    "userGroupIds": [],
    "network": {
        "subnetId": "e721a9dd-dad0-4cf0-a53b-dd654ebfc683",
        "availabilityZone": "kr-pub-a"
    },
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20
    },
    "backup": {
        "backupPeriod": 1,
        "backupSchedules": [
            {
                "backupWndBgnTime": "00:00:00",
                "backupWndDuration": "ONE_HOUR"
            }
        ]
    }
}
```

</p>
</details>

<a id="create-db-instance-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="modify-db-instance"></a>
### DB 인스턴스 수정하기 { #modify-db-instance }

```http
PUT /v4.0/db-instances/{dbInstanceId}
```

<a id="modify-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                           | 설명           |
|-----------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Modify | DB 인스턴스 수정하기 |

<a id="modify-db-instance-request"></a>
#### 요청

| 이름                      | 종류   | 형식      | 필수 | 설명                                          |
|-------------------------|------|---------|----|---------------------------------------------|
| dbInstanceId            | URL  | UUID    | O  | DB 인스턴스의 식별자                                |
| dbInstanceName          | Body | String  | X  | DB 인스턴스를 식별할 수 있는 마스터 이름                    |
| dbInstanceCandidateName | Body | String  | X  | DB 인스턴스를 식별할 수 있는 예비 마스터 이름 |
| description             | Body | String  | X  | DB 인스턴스에 대한 추가 정보                           |
| dbPort                  | Body | Number  | X  | DB 포트<br/>- 최솟값: `3306`<br/>- 최댓값: `43306`  |
{{#if (eq engine.lowerCase "mysql")}}    
| dbVersion          | Body | Enum    | X  | DB 엔진 유형                                                                                                                              |
| useDummy      | Body | Boolean | X  | 단일 DB 인스턴스의 DB 버전 업그레이드 시 더미 사용 여부<br/>기본값: `false`                                         |
{{/if}}
| useSlowQueryAnalysis | Body | Boolean  | X | Slow query 분석 여부 |
| dbFlavorId         | Body | UUID    | X  | DB 인스턴스 사양의 식별자                                                           |
| parameterGroupId   | Body | UUID    | X  | 파라미터 그룹의 식별자                                                              |
| dbSecurityGroupIds | Body | Array   | X  | DB 보안 그룹의 식별자 목록                                                          |
| executeBackup      | Body | Boolean | X  | 현재 시점 백업 진행 여부<br/>- 기본값: `false`                                         |
| useOnlineFailover  | Body | Boolean | X  | 장애 조치를 이용한 재시작 여부<br/>고가용성을 사용 중인 DB 인스턴스에서만 사용 가능합니다.<br/>- 기본값: `false` |
| waitReplicationDelay  | Body | Boolean | X  | 복제 지연 해소 대기 여부<br/>고가용성을 사용 중인 DB 인스턴스에서만 사용 가능합니다.<br/>- 기본값: `false` |
| useReadOnly  | Body | Boolean | X  | 읽기 전용으로 변경 여부<br/>고가용성을 사용 중인 DB 인스턴스에서만 사용 가능합니다.<br/>- 기본값: `false` |

<details><summary>예시</summary>
<p>

```json
{
    "dbInstanceName": "db-instance2",
    "description": "description2",
    "dbPort": 10001,
    "dbSecurityGroupIds": [],
    "executeBackup": true
}
```

</p>
</details>

<a id="modify-db-instance-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="delete-db-instance"></a>
### DB 인스턴스 삭제하기 { #delete-db-instance }

```http
DELETE /v4.0/db-instances/{dbInstanceId}
```

<a id="delete-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                           | 설명           |
|-----------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Delete | DB 인스턴스 삭제하기 |

<a id="delete-db-instance-request"></a>
#### 요청

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |
| deleteAutoBackup          | Body | Boolean  | X  | 자동 백업 삭제 여부<br/>- 기본값: `false` |

<a id="delete-db-instance-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="restart-db-instance"></a>
### DB 인스턴스 재시작하기 { #restart-db-instance }

```http
POST /v4.0/db-instances/{dbInstanceId}/restart
```

<a id="restart-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                            | 설명            |
|------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Restart | DB 인스턴스 재시작하기 |

<a id="restart-db-instance-request"></a>
#### 요청

| 이름                | 종류   | 형식      | 필수 | 설명                                                                        |
|-------------------|------|---------|----|---------------------------------------------------------------------------|
| dbInstanceId      | URL  | UUID    | O  | DB 인스턴스의 식별자                                                              |
| useOnlineFailover | Body | Boolean | X  | 장애 조치를 이용한 재시작 여부<br/>고가용성을 사용 중인 DB 인스턴스에서만 사용 가능합니다.<br/>- 기본값: `false` |
| executeBackup     | Body | Boolean | X  | 현재 시점 백업 진행 여부<br/>- 기본값: `false`                                         |
| waitReplicationDelay     | Body | Boolean | X  | 복제 지연 해소 대기 여부<br/>고가용성을 사용 중인 DB 인스턴스에서만 사용 가능합니다.<br/>- 기본값: `false`                                         |
| useReadOnly     | Body | Boolean | X  | 읽기 전용으로 변경 여부<br/>고가용성을 사용 중인 DB 인스턴스에서만 사용 가능합니다.<br/>- 기본값: `false`                                         |

<a id="restart-db-instance-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---
<a id="force-restart-db-instance"></a>
### DB 인스턴스 강제 재시작하기 { #force-restart-db-instance }

```http
POST /v4.0/db-instances/{dbInstanceId}/force-restart
```

<a id="force-restart-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                                 | 설명               |
|-----------------------------------------------------|------------------|
| RDSfor{{engine.pascalCase}}:DbInstance.ForceRestart | DB 인스턴스 강제 재시작하기 |

<a id="force-restart-db-instance-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.


| 이름                | 종류   | 형식      | 필수 | 설명                                                                        |
|-------------------|------|---------|----|---------------------------------------------------------------------------|
| dbInstanceId      | URL  | UUID    | O  | DB 인스턴스의 식별자                                                              |


<a id="force-restart-db-instance-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>


---

<a id="start-db-instance"></a>
### DB 인스턴스 시작하기 { #start-db-instance }

```http
POST /v4.0/db-instances/{dbInstanceId}/start
```

<a id="start-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                          | 설명           |
|----------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Start | DB 인스턴스 시작하기 |

<a id="start-db-instance-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="start-db-instance-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="stop-db-instance"></a>
### DB 인스턴스 정지하기 { #stop-db-instance }

```http
POST /v4.0/db-instances/{dbInstanceId}/stop
```

<a id="stop-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                         | 설명           |
|---------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Stop | DB 인스턴스 정지하기 |

<a id="stop-db-instance-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="stop-db-instance-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="replicate-db-instance"></a>
### DB 인스턴스 복제하기 { #replicate-db-instance }

```http
POST /v4.0/db-instances/{dbInstanceId}/replicate
```

<a id="replicate-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                              | 설명           |
|--------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Replicate | DB 인스턴스 복제하기 |

<a id="replicate-db-instance-request"></a>
#### 요청

| 이름                                           | 종류   | 형식      | 필수 | 설명                                                                        |
|----------------------------------------------|------|---------|----|---------------------------------------------------------------------------|
| dbInstanceId                                 | URL  | UUID    | O  | DB 인스턴스의 식별자                                                              |
| dbInstanceName                               | Body | String  | O  | DB 인스턴스를 식별할 수 있는 이름                                                      |
| description                                  | Body | String  | X  | DB 인스턴스에 대한 추가 정보                                                         |
| dbFlavorId                                   | Body | UUID    | X  | DB 인스턴스 사양의 식별자<br/>- 기본값: 원본 DB 인스턴스 값                                   |
| dbPort                                       | Body | Number  | X  | DB 포트<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `3306`<br/>- 최댓값: `43306`        |
| parameterGroupId                             | Body | UUID    | X  | 파라미터 그룹의 식별자<br/>- 기본값: 원본 DB 인스턴스 값                                      |
| dbSecurityGroupIds                           | Body | Array   | X  | DB 보안 그룹의 식별자 목록<br/>- 기본값: 원본 DB 인스턴스 값                                  |
| userGroupIds                                 | Body | Array   | X  | 사용자 그룹의 식별자 목록                                                            |
| useDefaultNotification                       | Body | Boolean | X  | 기본 알림 사용 여부<br/>- 기본값: `false`                                            |
| useDeletionProtection                        | Body | Boolean | X  | 삭제 보호 여부<br/>- 기본값: `false`                                               |
| useSlowQueryAnalysis                         | Body | Boolean | X  | Slow query 분석 여부<br/>- 기본값: `true`                                        |
| network                                      | Body | Object  | O  | 네트워크 정보 객체                                                                |
| network.usePublicAccess                      | Body | Boolean | X  | 외부 접속 가능 여부<br/>- 기본값: 원본 DB 인스턴스 값                                       |
| network.availabilityZone                     | Body | Enum    | O  | DB 인스턴스를 생성할 가용성 영역<br/>- 예시: `kr-pub-a`                                  |
| storage                                      | Body | Object  | X  | 데이터 스토리지 정보 객체                                                            |    
| storage.storageType                          | Body | Enum    | X  | 데이터 스토리지 타입<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 예시: `General SSD`                        |
| storage.storageSize                          | Body | Number  | X  | 데이터 스토리지 크기(GB)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `20`<br/>- 최댓값: `2048` |
| storage.storageAutoscale                     | Body | Object  | X  | 데이터 스토리지 자동 확장 객체                                                         |
| storage.storageAutoscale.useStorageAutoscale | Body | Boolean | X  | 스토리지 자동 확장 여부                                                             |
| storage.storageAutoscale.threshold           | Body | Number  | X  | 자동 확장 조건(%)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `50`<br/>- 최댓값: `95`                               |
| storage.storageAutoscale.maxStorageSize      | Body | Number  | X  | 자동 확장 최대 크기(GB)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최댓값: `4096`                                         |
| storage.storageAutoscale.cooldownTime        | Body | Number  | X  | 자동 확장 쿨다운 시간(분)<br/>- 최솟값: `10`<br/>- 최댓값: `1440`                         |
| backup                                       | Body | Object  | X  | 백업 정보 객체                                                                  |
| backup.backupPeriod                          | Body | Number  | X  | 백업 보관 기간(일)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `0`<br/>- 최댓값: `730`       |
| backup.ftwrlWaitTimeout                      | Body | Number  | X  | 쿼리 지연 대기 시간(초)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `0`<br/>- 최댓값: `21600`  |
| backup.backupRetryCount                      | Body | Number  | X  | 백업 재시도 횟수<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `0`<br/>- 최댓값: `10`          |
{{#if (eq engine.lowerCase "mysql")}}    
| backup.replicationRegion                     | Body | Enum    | X  | 백업 복제 리전<br />- `KR1`: 한국(판교) 리전<br/>- `KR2`: 한국(평촌) 리전<br/>- `JP1`: 일본(도쿄) 리전<br/>- 기본값: 원본 DB 인스턴스 값                                                                                                                                                       |
{{/if}}
| backup.useBackupLock                         | Body | Boolean | X  | 테이블 잠금 사용 여부<br/>- 기본값: 원본 DB 인스턴스 값                                                                                                                                                                                                                |
| backup.backupSchedules                       | Body | Array   | X  | 예정된 자동 백업 목록                                                                                                                                                                                                                                           |
| backup.backupSchedules.backupWndBgnTime      | Body | String  | X  | 백업 시작 시각<br/>- 예시: `00:00:00`<br/>- 기본값: 원본 DB 인스턴스 값                                                                                                                                                                                               |
| backup.backupSchedules.backupWndDuration     | Body | Enum    | X  | 백업 Duration<br/>백업 시작 시각부터 Duration 안에 자동 백업이 실행됩니다.<br/>- `HALF_AN_HOUR`: 30분<br/>- `ONE_HOUR`: 1시간<br/>- `ONE_HOUR_AND_HALF`: 1시간 30분<br/>- `TWO_HOURS`: 2시간<br/>- `TWO_HOURS_AND_HALF`: 2시간 30분<br/>- `THREE_HOURS`: 3시간<br/>- 기본값: 원본 DB 인스턴스 값 |

<details><summary>예시</summary>
<p>

```json
{
    "dbInstanceName": "db-instance-replicate",
    "description": "description",
    "dbPort": 11000,
    "network": {
        "availabilityZone": "kr-pub-a"
    },
    "storage": {
        "stroageSize": 100
    }
}
```

</p>
</details>

<a id="replicate-db-instance-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="promote-db-instance"></a>
### DB 인스턴스 승격하기 { #promote-db-instance }

```http
POST /v4.0/db-instances/{dbInstanceId}/promote
```

<a id="promote-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                            | 설명           |
|------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Promote | DB 인스턴스 승격하기 |

<a id="promote-db-instance-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="promote-db-instance-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="rebuild-db-instance"></a>
### DB 인스턴스 재구축하기 { #rebuild-db-instance }

```http
POST /v4.0/db-instances/{dbInstanceId}/rebuild
```

<a id="rebuild-db-instance-required-permissions"></a>
#### 필요 권한

| 권한명                                            | 설명            |
|------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Rebuild | DB 인스턴스 재구축하기 |

<a id="rebuild-db-instance-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="rebuild-db-instance-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="view-restoration-information"></a>
### 복원 정보 조회 { #view-restoration-information }

```http
GET /v4.0/db-instances/{dbInstanceId}/restoration-info
```

<a id="view-restoration-information-required-permissions"></a>
#### 필요 권한

| 권한명                                        | 설명            |
|--------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Get | DB 인스턴스 상세 보기 |

<a id="view-restoration-information-request"></a>
#### 요청

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="view-restoration-information-response"></a>
#### 응답

| 이름                                      | 종류   | 형식       | 설명                                                                                                                                                                           |
|-----------------------------------------|------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| oldestRestorableYmdt                    | Body | DateTime | 가장 오래된 복원 가능한 시각                                                                                                                                                             |
| latestRestorableYmdt                    | Body | DateTime | 가장 최신의 복원 가능한 시각                                                                                                                                                             |
| restorableBackups                       | Body | Array    | 복원 가능한 백업 목록                                                                                                                                                                 |
| restorableBackups.backup                | Body | Object   | 백업 정보 객체                                                                                                                                                                     |
| restorableBackups.backup.backupId       | Body | UUID     | 백업의 식별자                                                                                                                                                                      |
| restorableBackups.backup.backupName     | Body | String   | 백업 이름                                                                                                                                                                        |
| restorableBackups.backup.useBackupLock  | Body | Boolean  | 테이블 잠금 사용 여부                                                                                                                                                                 |
| restorableBackups.backup.backupSize     | Body | Number   | 백업 크기                                                                                                                                                                        |
| restorableBackups.backup.backupType     | Body | Enum     | 백업 유형<br/>- `AUTO`: 자동<br/>- `MANUAL`: 수동                                                                                                                   |
| restorableBackups.backup.backupStatus   | Body | Enum     | 백업 상태<br/>- `BACKING_UP`: 백업 중인 경우<br/>- `COMPLETED`: 백업이 완료된 경우<br/>- `DELETING`: 백업이 삭제 중인 경우<br/>- `DELETED`: 백업이 삭제된 경우<br/>- `ERROR`: 오류가 발생한 경우 |
| restorableBackups.backup.dbInstanceId   | Body | UUID     | 원본 DB 인스턴스의 식별자                                                                                                                                                              |
| restorableBackups.backup.dbInstanceName | Body | String   | 원본 DB 인스턴스의 이름                                                                                                                                                               |
| restorableBackups.backup.dbVersion      | Body | String   | DB 엔진 유형                                                                                                                                                                     |
| restorableBackups.backup.failoverCount  | Body | Number   | 장애 조치 횟수                                                                                                                                                                     |
| restorableBackups.backup.binLogFileName | Body | String   | 바이너리 로그 파일명                                                                                                                                                                |
| restorableBackups.backup.binLogPosition | Body | Number   | 바이너리 로그 파일 위치                                                                                                                                                                |
| restorableBackups.backup.createdYmdt    | Body | DateTime | 백업 생성 일시                                                                                                                                                                     |
| restorableBackups.backup.updatedYmdt    | Body | DateTime | 백업 갱신 일시                                                                                                                                                                     |
| restorableBackups.restorableBinLogs     | Body | Array    | 해당 백업을 이용하여 복원 가능한 바이너리 로그 이름 목록                                                                                                                                             |



<details><summary>예시</summary>
<p>

```json
{
	"header": {
		"resultCode": 0,
		"resultMessage": "SUCCESS",
		"isSuccessful": true
	},
    "oldestRestorableYmdt": "2023-07-09T16:33:33+09:00",
	"latestRestorableYmdt": "2023-07-10T15:44:44+09:00",
	"restorableBackups": [
		{
			"backup": {
				"backupId": "145d889a-fe08-474f-8f58-bde576ff96a9",
				"backupName": "example-backup-name",
				"backupStatus": "COMPLETED",
				"dbInstanceId": "dba1be25-9429-4589-9716-7fb6daad7cb9",
				"dbInstanceName": "original-db-instance-name",
				"dbVersion": "{{engine.sampleDbVersionCode}}",
				"backupType": "MANUAL",
				"backupSize": 8299904,
				"useBackupLock": true,
				"failoverCount": 0,
				"binLogFileName": "mysql-bin.000001",
				"binLogPosition": 367916037,
				"createdYmdt": "2023-07-10T15:44:44+09:00",
				"updatedYmdt": "2023-07-10T15:46:07+09:00"
			},
			"restorableBinLogs": [
				"mysql-bin.000001"
			]
		}
	]
}
```

</p>
</details>

---

<a id="view-the-last-query-to-be-restored"></a>
### 복원될 마지막 쿼리 조회 { #view-the-last-query-to-be-restored }

```http
GET /v4.0/db-instances/{dbInstanceId}/restoration-info/last-query
```

<a id="view-the-last-query-to-be-restored-required-permissions"></a>
#### 필요 권한

| 권한명                                        | 설명            |
|--------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Get | DB 인스턴스 상세 보기 |

<a id="view-the-last-query-to-be-restored-common-request"></a>
#### 공통 요청

| 이름           | 종류    | 형식   | 필수 | 설명                                                                                                                          |
|--------------|-------|------|----|-----------------------------------------------------------------------------------------------------------------------------|
| dbInstanceId | URL   | UUID | O  | DB 인스턴스의 식별자                                                                                                                |
| restoreType  | Query | Enum | O  | 복원 타입 종류<br/>- `TIMESTAMP`: 복원 가능한 시간 이내의 시간을 이용한 시점 복원 타입<br/>- `BINLOG`: 복원 가능한 바이너리 로그 위치를 이용한 시점 복원 타입 |

<a id="view-the-last-query-to-be-restored-if-restoretype-is-timestamp"></a>
#### restoreType이 `TIMESTAMP`인 경우

| 이름          | 종류    | 형식       | 필수 | 설명                                        |
|-------------|-------|----------|----|-------------------------------------------|
| restoreYmdt | Query | DateTime | O  | DB 인스턴스 복원 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<a id="view-the-last-query-to-be-restored-if-restoretype-is-binlog"></a>
#### restoreType이 `BINLOG`인 경우

| 이름             | 종류    | 형식     | 필수 | 설명                 |
|----------------|-------|--------|----|--------------------|
| backupId       | Query | UUID   | O  | 복원에 사용할 백업의 식별자    |
| binLogFileName | Query | String | O  | 복원에 사용할 바이너리 로그 이름 |
| binLogPosition | Query | Number | O  | 복원에 사용할 바이너리 로그 위치 |

<a id="view-the-last-query-to-be-restored-response"></a>
#### 응답

| 이름           | 종류   | 형식       | 설명                                   |
|--------------|------|----------|--------------------------------------|
| executedYmdt | Body | DateTime | 쿼리 수행 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| lastQuery    | Body | String   | 마지막 수행 쿼리                            |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "executedYmdt": "2023-03-17T14:02:29+09:00",
    "lastQuery": "INSERT INTO `test`.`test`SET  @1='0123'"
}
```

</p>
</details>

---

<a id="restoration"></a>
### 복원 { #restoration }

```http
POST /v4.0/db-instances/{dbInstanceId}/restore
```

<a id="restoration-required-permissions"></a>
#### 필요 권한

| 권한명                                            | 설명           |
|------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Restore | DB 인스턴스 복원하기 |

<a id="restoration-common-request"></a>
#### 공통 요청

| 이름                                                  | 종류   | 형식      | 필수 | 설명                                                                                                                                                   |
|-----------------------------------------------------|------|---------|----|------------------------------------------------------------------------------------------------------------------------------------------------------|
| dbInstanceId                                        | URL  | UUID    | O  | DB 인스턴스의 식별자                                                                                                                                         |
| restore                                             | Body | Object  | O  | 복원 정보 객체                                                                                                                                             |
| restore.restoreType                                 | Body | Enum    | O  | 복원 타입 종류<br/>- `TIMESTAMP`: 복원 가능한 시간 이내의 시간을 이용한 시점 복원 타입<br/>- `BINLOG`: 복원 가능한 바이너리 로그 위치를 이용한 시점 복원 타입<br/>- `BACKUP`: 기존에 생성한 백업을 이용한 스냅숏 복원 타입 |
| dbInstanceName                                      | Body | String  | O  | DB 인스턴스를 식별할 수 있는 마스터 이름                                                                                                                             |
| dbInstanceCandidateName                             | Body | String  | O  | DB 인스턴스를 식별할 수 있는 예비 마스터 이름<br/>- 고가용성 사용 시 필수                                                                                                       |
| description                                         | Body | String  | X  | DB 인스턴스에 대한 추가 정보                                                                                                                                    |
| dbFlavorId                                          | Body | UUID    | X  | DB 인스턴스 사양의 식별자                                                                                                                                      |
| dbPort                                              | Body | Number  | X  | DB 포트<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `3306`<br/>- 최댓값: `43306`                                                                                   |
| parameterGroupId                                    | Body | UUID    | X  | 파라미터 그룹의 식별자<br/>- 기본값: 원본 DB 인스턴스 값                                                                                                                 |
| dbSecurityGroupIds                                  | Body | Array   | X  | DB 보안 그룹의 식별자 목록                                                                                                                                     |
| userGroupIds                                        | Body | Array   | X  | 사용자 그룹의 식별자 목록                                                                                                                                       |
| useHighAvailability                                 | Body | Boolean | X  | 고가용성 사용 여부<br/>- 기본값: `false`                                                                                                                        |
| pingInterval                                        | Body | Number  | X  | 고가용성 사용 시 Ping 간격(초)<br/>- 기본값: `3`<br/>- 최솟값: `1`<br/>- 최댓값: `600`                                                                                  |
| pingType                                            | Body | Enum    | X  | 고가용성 사용 시 Ping 타입<br/>- 기본값: `INSERT`<br/>- `INSERT`<br/>- `SELECT`                                                                                  |
| useDefaultNotification                              | Body | Boolean | X  | 기본 알림 사용 여부<br/>- 기본값: `false`                                                                                                                       |
| useDeletionProtection                               | Body | Boolean | X  | 삭제 보호 여부<br>기본값: `false`                                                                                                                             |
| useSlowQueryAnalysis                                | Body | Boolean | X  | Slow query 분석 여부<br/>- 기본값: `true`                                                                                                                   |
| network                                             | Body | Object  | X  | 네트워크 정보 객체                                                                                                                                           |
| network.subnetId                                    | Body | UUID    | X  | 서브넷의 식별자<br/>- 기본값: 원본 DB 인스턴스 값                                                                                                                     |
| network.usePublicAccess                             | Body | Boolean | X  | 외부 접속 가능 여부<br/>- 기본값: `false`                                                                                                                       |
| network.availabilityZone                            | Body | Enum    | X  | DB 인스턴스를 생성할 가용성 영역<br/>- 예시: `kr-pub-a`<br/>- 기본값: 랜덤 선택                                                                                            |
| storage                                             | Body | Object  | X  | 데이터 스토리지 정보 객체                                                                                                                                       |
| storage.storageType                                 | Body | Enum    | X  | 데이터 스토리지 타입<br/>- 예시: `General SSD`<br/>- 기본값: 원본 DB 인스턴스 값                                                                                          |
| storage.storageSize                                 | Body | Number  | X  | 데이터 스토리지 크기(GB)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `20`<br/>- 최댓값: `2048`                                                                            |
| storage.storageAutoscale                            | Body | Object  | X  | 데이터 스토리지 자동 확장 객체                                                                                                                                    |
| storage.storageAutoscale.useStorageAutoscale        | Body | Boolean | X  | 스토리지 자동 확장 여부                                                                                                                                        |
| storage.storageAutoscale.threshold                  | Body | Number  | X  | 자동 확장 조건(%)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `50`<br/>- 최댓값: `95`                                                                                  |
| storage.storageAutoscale.maxStorageSize             | Body | Number  | X  | 자동 확장 최대 크기(GB) <br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최댓값: `4096`                                                                                           |
| storage.storageAutoscale.cooldownTime               | Body | Number  | X  | 자동 확장 쿨다운 시간(분)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `10`<br/>- 최댓값: `1440`                                                                            |
| backup                                              | Body | Object  | X  | 백업 정보 객체                                                                                                                                             |
| backup.backupPeriod                                 | Body | Number  | X  | 백업 보관 기간(일)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `0`<br/>- 최댓값: `730`                                                                                  |
| backup.ftwrlWaitTimeout                             | Body | Number  | X  | 쿼리 지연 대기 시간(초)<br/>- 기본값: `1800`<br/>- 최솟값: `0`<br/>- 최댓값: `21600`                                                                                   |
| backup.backupRetryCount                             | Body | Number  | X  | 백업 재시도 횟수<br/>- 기본값: `0`<br/>- 최솟값: `0`<br/>- 최댓값: `10`                                                                                              |
{{#if (eq engine.lowerCase "mysql")}}
| backup.replicationRegion | Body | Enum | X | 백업 복제 리전<br/>- `KR1`: 한국(판교) 리전<br/>- `KR2`: 한국(평촌) 리전<br/>- `JP1`: 일본(도쿄) 리전                                                                                                                                                                                                                                                                                                                                                                              |
{{/if}}
| backup.useBackupLock | Body | Boolean | X | 테이블 잠금 사용 여부<br/>- 기본값: `true`                                                                                                                                                                                                                                                                                                                                                                                                                        |
| backup.backupSchedules | Body | Array | X | 예정된 자동 백업 목록<br/>- 기본값: 원본 DB 인스턴스 값                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| backup.backupSchedules.backupWndBgnTime | Body | String | X | 백업 시작 시각<br/>- 예시: `00:00:00`                                                                                                                                                                                                                                                                                                                                                                                                                         |
| backup.backupSchedules.backupWndDuration | Body | Enum | X | 백업 Duration<br>백업 시작 시각부터 Duration 안에 자동 백업이 실행됩니다.<br/>- `HALF_AN_HOUR`: 30분<br/>- `ONE_HOUR`: 1시간<br/>- `ONE_HOUR_AND_HALF`: 1시간 30분<br/>- `TWO_HOURS`: 2시간<br/>- `TWO_HOURS_AND_HALF`: 2시간 30분<br/>- `THREE_HOURS`: 3시간 |

<a id="restoration-request-when-restoring-a-point-in-time-restoration-using-timestamp-if-restoretype-is-timestamp"></a>
#### Timestamp를 이용한 시점 복원 시 요청(restoreType이 `TIMESTAMP`인 경우)

| 이름                  | 종류   | 형식       | 필수 | 설명                                                                                             |
|---------------------|------|----------|----|------------------------------------------------------------------------------------------------|
| restore.restoreYmdt | Body | DateTime | O  | DB 인스턴스 복원 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)<br>복원 정보 조회로 조회한 가장 최신의 복원 가능한 시간 이전에 대해서만 복원이 가능합니다. |


<details><summary>예시</summary>
<p>

```json
{
    "dbInstanceName": "db-instance",
    "description": "description",
    "dbFlavorId": "71f69bf9-3c01-4c1a-b135-bb75e93f6268",
    "dbPort": 10000,
    "dbUserName": "db-user",
    "dbPassword": "password",
    "parameterGroupId": "488bf4f5-d8f7-459b-ace6-529b606c8570",
    "dbSecurityGroupIds": [
        "b0483a3d-e8e2-46f6-9e84-d5e31b0d44f4"
    ],
    "userGroupIds": [],
    "network": {
		"subnetId": "3ae7914f-9b42-4729-b125-87417b72cf36",
		"availabilityZone": "kr-pub-a"
	},
	"storage": {
		"storageType": "General SSD",
		"storageSize": 20
	},
	"restore": {
		"restoreType": "TIMESTAMP",
		"restoreYmdt": "2023-07-10T15:44:44+09:00"
	},
	"backup": {
		"backupPeriod": 1,
		"backupSchedules": [
			{
				"backupWndBgnTime": "00:00:00",
				"backupWndDuration": "ONE_HOUR_AND_HALF"
			}
		]
	}
}
```

</p>
</details>

<a id="restoration-request-for-point-in-time-restoration-using-binary-logs-if-restoretype-is-binlog"></a>
#### 바이너리 로그를 이용한 시점 복원 시 요청(restoreType이 `BINLOG`인 경우)

| 이름                            | 종류   | 형식     | 필수 | 설명                 |
|-------------------------------|------|--------|----|--------------------|
| restore.backupId              | Body | UUID   | O  | 복원에 사용할 백업의 식별자    |
| restore.binLog                | Body | Object | O  | 바이너리 로그 정보 객체      |
| restore.binLog.binLogFileName | Body | String | O  | 복원에 사용할 바이너리 로그 이름 |
| restore.binLog.binLogPosition | Body | Number | O  | 복원에 사용할 바이너리 로그 위치 |

* 바이너리 로그를 이용한 시점 복원 시 기준 백업의 바이너리 로그 파일 및 위치를 기준으로 그 이후에 기록된 로그를 복원할 수 있습니다.


<details><summary>예시</summary>
<p>

```json
{
    "dbInstanceName": "db-instance",
    "description": "description",
    "dbFlavorId": "71f69bf9-3c01-4c1a-b135-bb75e93f6268",
    "dbPort": 10000,
    "dbUserName": "db-user",
    "dbPassword": "password",
    "parameterGroupId": "488bf4f5-d8f7-459b-ace6-529b606c8570",
    "dbSecurityGroupIds": [
        "b0483a3d-e8e2-46f6-9e84-d5e31b0d44f4"
    ],
    "userGroupIds": [],
    "network": {
		"subnetId": "3ae7914f-9b42-4729-b125-87417b72cf36",
		"availabilityZone": "kr-pub-a"
	},
	"storage": {
		"storageType": "General SSD",
		"storageSize": 20
	},
	"restore": {
		"restoreType": "BINLOG",
        "backupId":"3ae7914f-9b42-4729-b125-87417b72cf36",
		"binLogFileName": "mysql-bin.000001",
		"binLogPosition": 1234567
	},
	"backup": {
		"backupPeriod": 1,
		"backupSchedules": [
			{
				"backupWndBgnTime": "00:00:00",
				"backupWndDuration": "ONE_HOUR_AND_HALF"
			}
		]
	}
}
```

</p>
</details>

<a id="restoration-request-when-restoring-from-backup-if-restoretype-is-backup"></a>
#### 백업을 이용한 복원 시 요청(restoreType이 `BACKUP`인 경우)

| 이름               | 종류   | 형식   | 필수                           | 설명              |
|------------------|------|------|------------------------------|-----------------|
| restore.backupId | Body | UUID | O(restoreType이 `BACKUP`인 경우) | 복원에 사용할 백업의 식별자 |



<details><summary>예시</summary>
<p>

```json
{
    "dbInstanceName": "db-instance",
    "description": "description",
    "dbFlavorId": "71f69bf9-3c01-4c1a-b135-bb75e93f6268",
    "dbPort": 10000,
    "dbUserName": "db-user",
    "dbPassword": "password",
    "parameterGroupId": "488bf4f5-d8f7-459b-ace6-529b606c8570",
    "dbSecurityGroupIds": [
        "b0483a3d-e8e2-46f6-9e84-d5e31b0d44f4"
    ],
    "userGroupIds": [],
    "network": {
		"subnetId": "3ae7914f-9b42-4729-b125-87417b72cf36",
		"availabilityZone": "kr-pub-a"
	},
	"storage": {
		"storageType": "General SSD",
		"storageSize": 20
	},
	"restore": {
		"restoreType": "BACKUP",
        "backupId":"3ae7914f-9b42-4729-b125-87417b72cf36"
	},
	"backup": {
		"backupPeriod": 1,
		"backupSchedules": [
			{
				"backupWndBgnTime": "00:00:00",
				"backupWndDuration": "ONE_HOUR_AND_HALF"
			}
		]
	}
}
```

</p>
</details>

<a id="restoration-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |


---

<a id="restore-from-object-storage"></a>
### 오브젝트 스토리지로부터 복원 { #restore-from-object-storage }

```http
POST /v4.0/db-instances/restore-from-obs
```

<a id="restore-from-object-storage-required-permissions"></a>
#### 필요 권한

| 권한명                                                   | 설명                      |
|-------------------------------------------------------|-------------------------|
| RDSfor{{engine.pascalCase}}:DbInstance.RestoreFromObs | DB 인스턴스 오브젝트 스토리지로부터 복원 |

<a id="restore-from-object-storage-request"></a>
#### 요청

| 이름                                                  | 종류   | 형식      | 필수 | 설명                                                                                     |
|-----------------------------------------------------|------|---------|----|----------------------------------------------------------------------------------------|
| restore                                             | Body | Object  | O  | 복원 정보 객체                                                                               |
| restore.tenantId                                    | Body | String  | O  | 백업이 저장된 오브젝트 스토리지의 테넌트 ID                                                              |
| restore.username                                    | Body | String  | O  | NHN Cloud 계정 또는 IAM 계정 ID                                                              |
| restore.password                                    | Body | String  | O  | 백업이 저장된 오브젝트 스토리지의 API 비밀번호                                                            |
| restore.targetContainer                             | Body | String  | O  | 백업이 저장된 오브젝트 스토리지의 컨테이너                                                                |
| restore.objectPath                                  | Body | String  | O  | 컨테이너에 저장된 백업의 경로                                                                       |
| dbVersion                                           | Body | Enum    | O  | DB 엔진 유형                                                                               |
| dbInstanceName                                      | Body | String  | O  | DB 인스턴스를 식별할 수 있는 마스터 이름                                                               |
| dbInstanceCandidateName                             | Body | String  | O  | DB 인스턴스를 식별할 수 있는 예비 마스터 이름(고가용성 사용 시 필수 값)                                            |
| description                                         | Body | String  | X  | DB 인스턴스에 대한 추가 정보                                                                      |
| dbFlavorId                                          | Body | UUID    | O  | DB 인스턴스 사양의 식별자                                                                        |
| dbPort                                              | Body | Number  | O  | DB 포트<br/>- 최솟값: `3306`<br/>- 최댓값: `43306`                            |
| parameterGroupId | Body | UUID    | O  | 파라미터 그룹의 식별자                                                                           |
| dbSecurityGroupIds                                  | Body | Array   | X  | DB 보안 그룹의 식별자 목록                                                                       |
| userGroupIds                                        | Body | Array   | X  | 사용자 그룹의 식별자 목록                                                                         |
| useHighAvailability                                 | Body | Boolean | X  | 고가용성 사용 여부<br/>- 기본값: `false`                                           |
| pingInterval                                        | Body | Number  | X  | 고가용성 사용 시 Ping 간격(초)<br/>- 기본값: `3`<br/>- 최솟값: `1`<br/>- 최댓값: `600` |
| pingType                                            | Body | Enum    | X  | 고가용성 사용 시 Ping 타입<br/>- 기본값: `INSERT`<br/>- `INSERT`<br/>- `SELECT` |
| useDefaultNotification                              | Body | Boolean | X  | 기본 알림 사용 여부<br/>- 기본값: `false`                                          |
| useDeletionProtection                               | Body | Boolean | X  | 삭제 보호 여부<br>기본값: `false`                                                               |
| useSlowQueryAnalysis                                | Body | Boolean | X  | Slow query 분석 여부<br/>- 기본값: `true`                                                     |
| network                                             | Body | Object  | O  | 네트워크 정보 객체                                                                             |
| network.subnetId                                    | Body | UUID    | O  | 서브넷의 식별자                                                                               |
| network.usePublicAccess                             | Body | Boolean | X  | 외부 접속 가능 여부<br/>- 기본값: `false`                                          |
| network.availabilityZone                            | Body | Enum    | O  | DB 인스턴스를 생성할 가용성 영역<br/>- 예시: `kr-pub-a`                                |
| storage                                             | Body | Object  | O  | 데이터 스토리지 정보 객체                                                                         |
| storage.storageType                                 | Body | Enum    | O  | 데이터 스토리지 타입<br/>- 예시: `General SSD`                                     |
| storage.storageSize                                 | Body | Number  | O  | 데이터 스토리지 크기(GB)<br/>- 최솟값: `20`<br/>- 최댓값: `2048`                     |
| storage.storageAutoscale                            | Body | Object  | X  | 데이터 스토리지 자동 확장 객체                                                                      |
| storage.storageAutoscale.useStorageAutoscale        | Body | Boolean | X  | 스토리지 자동 확장 여부                                                                          |
| storage.storageAutoscale.threshold                  | Body | Number  | X  | 자동 확장 조건(%)<br/>- 최솟값: `50`<br/>- 최댓값: `95`                                            |
| storage.storageAutoscale.maxStorageSize             | Body | Number  | X  | 자동 확장 최대 크기(GB)<br/>- 최댓값: `4096`                                                      |
| storage.storageAutoscale.cooldownTime               | Body | Number  | X  | 자동 확장 쿨다운 시간(분)<br/>- 최솟값: `10`<br/>- 최댓값: `1440`                                      |
| backup                                              | Body | Object  | O  | 백업 정보 객체                                                                               |
| backup.backupPeriod                                 | Body | Number  | O  | 백업 보관 기간(일)<br/>- 최솟값: `0`<br/>- 최댓값: `730`                           |
| backup.ftwrlWaitTimeout                             | Body | Number  | X  | 쿼리 지연 대기 시간(초)<br/>- 기본값: `1800`<br/>- 최솟값: `0`<br/>- 최댓값: `21600`  |
| backup.backupRetryCount                             | Body | Number  | X  | 백업 재시도 횟수<br/>- 기본값: `0`<br/>- 최솟값: `0`<br/>- 최댓값: `10`             |
{{#if (eq engine.lowerCase "mysql")}}
| backup.replicationRegion | Body | Enum | X | 백업 복제 리전<br/>- `KR1`: 한국(판교) 리전<br/>- `KR2`: 한국(평촌) 리전<br/>- `JP1`: 일본(도쿄) 리전                                                                                                                                                                                                                                                                                                                                                                               |
{{/if}}
| backup.useBackupLock | Body | Boolean | X | 테이블 잠금 사용 여부<br/>- 기본값: `true`                                                                                                                                                                                                                                                                                                                                                                                                                         |
| backup.backupSchedules | Body | Array | O | 예정된 자동 백업 목록                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| backup.backupSchedules.backupWndBgnTime | Body | String | O | 백업 시작 시각<br/>- 예시: `00:00:00`                                                                                                                                                                                                                                                                                                                                                                                                                          |
| backup.backupSchedules.backupWndDuration | Body | Enum | O | 백업 Duration<br>백업 시작 시각부터 Duration 안에 자동 백업이 실행됩니다.<br/>- `HALF_AN_HOUR`: 30분<br/>- `ONE_HOUR`: 1시간<br/>- `ONE_HOUR_AND_HALF`: 1시간 30분<br/>- `TWO_HOURS`: 2시간<br/>- `TWO_HOURS_AND_HALF`: 2시간 30분<br/>- `THREE_HOURS`: 3시간 |



<details><summary>예시</summary>
<p>

```json
{
    "dbInstanceName": "db-instance",
    "description": "description",
    "dbFlavorId": "71f69bf9-3c01-4c1a-b135-bb75e93f6268",
    "dbPort": 10000,
    "dbVersion": "{{engine.sampleDbVersionCode}}",
    "dbUserName": "db-user",
    "dbPassword": "password",
    "parameterGroupId": "488bf4f5-d8f7-459b-ace6-529b606c8570",
    "dbSecurityGroupIds": [
        "b0483a3d-e8e2-46f6-9e84-d5e31b0d44f4"
    ],
    "userGroupIds": [],
    "network": {
		"subnetId": "3ae7914f-9b42-4729-b125-87417b72cf36",
		"availabilityZone": "kr-pub-a"
	},
	"storage": {
		"storageType": "General SSD",
		"storageSize": 20
	},
	"restore": {
		"tenantId":"tenant-id",
        "username":"username",
        "password":"password",
        "targetContainer":"targetContainer",
        "objectPath":"objectPath"
	},
	"backup": {
		"backupPeriod": 1,
		"backupSchedules": [
			{
				"backupWndBgnTime": "00:00:00",
				"backupWndDuration": "ONE_HOUR_AND_HALF"
			}
		]
	}
}
```

</p>
</details>

<a id="restore-from-object-storage-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |


---


<a id="change-db-instance-deletion-protection-settings"></a>
### DB 인스턴스 삭제 보호 설정 변경하기 { #change-db-instance-deletion-protection-settings }

```http
PUT /v4.0/db-instances/{dbInstanceId}/deletion-protection
```

<a id="change-db-instance-deletion-protection-settings-required-permissions"></a>
#### 필요 권한

| 권한명                                           | 설명           |
|-----------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Modify | DB 인스턴스 수정하기 |

<a id="change-db-instance-deletion-protection-settings-request"></a>
#### 요청

| 이름                    | 종류   | 형식      | 필수 | 설명           |
|-----------------------|------|---------|----|--------------|
| dbInstanceId          | URL  | UUID    | O  | DB 인스턴스의 식별자 |
| useDeletionProtection | Body | Boolean | O  | 삭제 보호 여부     |

<a id="change-db-instance-deletion-protection-settings-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="high-availability-status"></a>
### 고가용성 상태 { #high-availability-status }

| 상태                               | 설명                              |
|----------------------------------|---------------------------------|
| `CREATED`                        | 고가용성이 생성된 경우                    |
| `STABLE`                         | 고가용성이 정상인 경우                    |
| `PAUSING`                        | 고가용성이 일시 중지 중인 경우               |
| `PAUSED`                         | 고가용성이 일시 중지된 경우                 |
| `PAUSED_DUE_TO_TASK`             | 작업으로 인해 고가용성이 일시 중지된 경우         |
| `DISABLE_MASTER_IN_REPLICATION`  | 마스터 비정상 복제 감지로 고가용성이 중단된 경우     |
| `DISABLE_MHA_PROCESS`            | 고가용성 프로세스가 중단된 경우               |
| `DISABLE_REPLICATION_STOP`       | 복제 중단으로 인해 고가용성이 중단된 경우         |
| `DISABLE_REPLICATION_DELAY`      | 복제 지연으로 인해 고가용성이 중단된 경우         |
| `MASTER_FAILURE_DETECTION`       | 마스터 장애가 감지된 경우                  |
| `FAILOVER_STARTED`               | 장애 조치가 시작된 경우                   |
| `FAILOVER_FAILED`                | 장애 조치가 실패한 경우                   |
| `FAILOVER_COMPLETED`             | 장애 조치가 완료된 경우                   |
| `DELETED`                        | 고가용성이 삭제된 경우                    |

---

<a id="view-high-availability-information"></a>
### 고가용성 정보 보기 { #view-high-availability-information }

```http
GET /v4.0/db-instances/{dbInstanceId}/high-availability
```

<a id="view-high-availability-information-required-permissions"></a>
#### 필요 권한

| 권한명                                              | 설명         |
|----------------------------------------------------|------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Get | DB 인스턴스 상세 보기 |

<a id="view-high-availability-information-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="view-high-availability-information-response"></a>
#### 응답

| 이름                  | 종류   | 형식      | 설명                                                                                                                  |
|---------------------|------|---------|---------------------------------------------------------------------------------------------------------------------|
| useHighAvailability | Body | Boolean | 고가용성 사용 여부                                                                                                          |
| haStatus            | Body | Enum    | 고가용성 상태                                                                                                          |
| pingInterval        | Body | Number  | Ping 간격(초)                                                                                                          |
| pingType            | Body | Enum    | Ping 타입<br/>- `INSERT`<br/>- `SELECT`                                                                                |

<details><summary>예시</summary>

<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "useHighAvailability": true,
    "haStatus": "STABLE",
    "pingInterval": 3,
    "pingType": "INSERT"
}
```

</p>

</details>

---

<a id="modify-high-availability"></a>
### 고가용성 수정하기 { #modify-high-availability }

```http
PUT /v4.0/db-instances/{dbInstanceId}/high-availability
```

<a id="modify-high-availability-required-permissions"></a>
#### 필요 권한

| 권한명                                                 | 설명        |
|-----------------------------------------------------|-----------|
| RDSfor{{engine.pascalCase}}:HighAvailability.Modify | 고가용성 수정하기 |

<a id="modify-high-availability-request"></a>
#### 요청

| 이름                  | 종류   | 형식      | 필수 | 설명                                                   |
|---------------------|------|---------|----|------------------------------------------------------|
| dbInstanceId        | URL  | UUID    | O  | DB 인스턴스의 식별자                                         |
| useHighAvailability | Body | Boolean | O  | 고가용성 사용 여부                                           |
| pingInterval        | Body | Number  | X  | 고가용성 사용 시 Ping 간격(초)<br/>- 최솟값: `1`<br/>- 최댓값: `600` |
| pingType            | Body | Enum    | X  | 고가용성 사용 시 Ping 타입<br/>- `INSERT`<br/>- `SELECT` |
| dbInstanceCandidateName        | Body | String  | O  | DB 인스턴스를 식별할 수 있는 예비 마스터 이름<br/>- 고가용성 사용 시 필수값 |

<a id="modify-high-availability-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="restart-high-availability"></a>
### 고가용성 다시 시작하기 { #restart-high-availability }

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/resume
```

<a id="restart-high-availability-required-permissions"></a>
#### 필요 권한

| 권한명                                                 | 설명           |
|-----------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:HighAvailability.Resume | 고가용성 다시 시작하기 |

<a id="restart-high-availability-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="restart-high-availability-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="pause-high-availability"></a>
### 고가용성 일시 중지하기 { #pause-high-availability }

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/pause
```

<a id="pause-high-availability-required-permissions"></a>
#### 필요 권한

| 권한명                                                | 설명           |
|----------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:HighAvailability.Pause | 고가용성 일시 중지하기 |

<a id="pause-high-availability-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="pause-high-availability-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="recover-high-availability"></a>
### 고가용성 복구하기 { #recover-high-availability }

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/repair
```

<a id="recover-high-availability-required-permissions"></a>
#### 필요 권한

| 권한명                                                 | 설명        |
|-----------------------------------------------------|-----------|
| RDSfor{{engine.pascalCase}}:HighAvailability.Repair | 고가용성 복구하기 |

<a id="recover-high-availability-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="recover-high-availability-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="separate-high-availability"></a>
### 고가용성 분리하기 { #separate-high-availability }

```http
POST /v4.0/db-instances/{dbInstanceId}/high-availability/split
```

<a id="separate-high-availability-required-permissions"></a>
#### 필요 권한

| 권한명                                                | 설명        |
|----------------------------------------------------|-----------|
| RDSfor{{engine.pascalCase}}:HighAvailability.Split | 고가용성 분리하기 |

<a id="separate-high-availability-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="separate-high-availability-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="view-storage-information"></a>
### 데이터 스토리지 정보 보기 { #view-storage-information }

```http
GET /v4.0/db-instances/{dbInstanceId}/storage-info
```

<a id="view-storage-information-required-permissions"></a>
#### 필요 권한

| 권한명                                        | 설명            |
|--------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Get | DB 인스턴스 상세 보기 |

<a id="view-storage-information-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="view-storage-information-response"></a>
#### 응답

| 이름                                   | 종류   | 형식      | 설명                                                                                   |
|--------------------------------------|------|---------|--------------------------------------------------------------------------------------|
| storageType                          | Body | Enum    | 데이터 스토리지 타입                                                                          |
| storageSize                          | Body | Number  | 데이터 스토리지 크기(GB)                                                                      |
| storageStatus                        | Body | Enum    | 데이터 스토리지의 현재 상태<br/>- `DETACHED`: 부착되지 않음<br/>- `ATTACHED`: 부착됨<br/>- `DELETED`: 삭제됨 |
| storageAutoscale                     | Body | Object  | 데이터 스토리지 자동 확장 객체                                                                    |
| storageAutoscale.useStorageAutoscale | Body | Boolean | 스토리지 자동 확장 여부                                                                        |
| storageAutoscale.threshold           | Body | Number  | 자동 확장 조건(%)                                                                          |
| storageAutoscale.maxStorageSize      | Body | Number  | 자동 확장 최대 크기(GB)                                                                      |
| storageAutoscale.cooldownTime        | Body | Number  | 자동 확장 쿨다운 시간(분)                                                                      |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "storageType": "General SSD",
    "storageSize": 20,
    "storageStatus": "ATTACHED",
    "storageAutoscale": {
         "useStorageAutoscale": true,
         "threshold": 80,
         "maxStorageSize": 100,
         "cooldownTime": 10
    }
}
```

</p>
</details>


---

<a id="modify-storage-information"></a>
### 데이터 스토리지 정보 수정하기 { #modify-storage-information }

```http
PUT /v4.0/db-instances/{dbInstanceId}/storage-info
```

<a id="modify-storage-information-required-permissions"></a>
#### 필요 권한

| 권한명                                           | 설명           |
|-----------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Modify | DB 인스턴스 수정하기 |

<a id="modify-storage-information-request"></a>
#### 요청

| 이름                                   | 종류   | 형식      | 필수 | 설명                                                                        |
|--------------------------------------|------|---------|----|---------------------------------------------------------------------------|
| dbInstanceId                         | URL  | UUID    | O  | DB 인스턴스의 식별자                                                              |
| storageSize                          | Body | Number  | O  | 데이터 스토리지 크기(GB)<br/>- 최솟값: 현재값<br/>- 최댓값: `2048`                          |
| useOnlineFailover                    | Body | Boolean | X  | 장애 조치를 이용한 재시작 여부<br/>고가용성을 사용 중인 DB 인스턴스에서만 사용 가능합니다.<br/>- 기본값: `false` |
| storageAutoscale                     | Body | Object  | X  | 데이터 스토리지 자동 확장 객체                                                         |
| storageAutoscale.useStorageAutoscale | Body | Boolean | X  | 스토리지 자동 확장 여부                                                             |
| storageAutoscale.threshold           | Body | Number  | X  | 자동 확장 조건(%)<br/>- 최솟값: `50`<br/>- 최댓값: `95`                               |
| storageAutoscale.maxStorageSize      | Body | Number  | X  | 자동 확장 최대 크기(GB)<br/>- 최댓값: `4096`                                         |
| storageAutoscale.cooldownTime        | Body | Number  | X  | 자동 확장 쿨다운 시간(분)<br/>- 최솟값: `10`<br/>- 최댓값: `1440`                         |

<a id="modify-storage-information-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="view-backup-information"></a>
### 백업 정보 보기 { #view-backup-information }

```http
GET /v4.0/db-instances/{dbInstanceId}/backup-info
```

<a id="view-backup-information-required-permissions"></a>
#### 필요 권한

| 권한명                                        | 설명            |
|--------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Get | DB 인스턴스 상세 보기 |

<a id="view-backup-information-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="view-backup-information-response"></a>
#### 응답

| 이름                                | 종류   | 형식      | 설명             |
|-----------------------------------|------|---------|----------------|
| backupPeriod                      | Body | Number  | 백업 보관 기간(일)    |
| ftwrlWaitTimeout                  | Body | Number  | 쿼리 지연 대기 시간(초) |
| backupRetryCount                  | Body | Number  | 백업 재시도 횟수      |
| replicationRegion                 | Body | Enum    | 백업 복제 리전       |
| useBackupLock                     | Body | Boolean | 테이블 잠금 사용 여부   |
| backupSchedules                   | Body | Array   | 예정된 자동 백업 목록   |
| backupSchedules.backupWndBgnTime  | Body | String  | 백업 시작 시각       |
| backupSchedules.backupWndDuration | Body | Enum    | 백업 Duration    |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "backupPeriod": 1,
    "ftwrlWaitTimeout": 1800,
    "backupRetryCount": 0,
    "replicationRegion": null,
    "useBackupLock": false,
    "backupSchedules": [
        {
            "backupWndBgnTime": "00:00:00",
            "backupWndDuration": "ONE_HOUR_AND_HALF"
        }
    ]
}
```

</p>
</details>


---

<a id="modify-backup-information"></a>
### 백업 정보 수정하기 { #modify-backup-information }

```http
PUT /v4.0/db-instances/{dbInstanceId}/backup-info
```

<a id="modify-backup-information-required-permissions"></a>
#### 필요 권한

| 권한명                                           | 설명           |
|-----------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Modify | DB 인스턴스 수정하기 |

<a id="modify-backup-information-request"></a>
#### 요청

| 이름                                    | 종류   | 형식      | 필수 | 설명                                                                                                                                                                                                                          |
|---------------------------------------|------|---------|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dbInstanceId                          | URL  | UUID    | O  | DB 인스턴스의 식별자                                                                                                                                                                                                                |
| backupPeriod                          | Body | Number  | X  | 백업 보관 기간(일)<br/>- 최솟값: `0`<br/>- 최댓값: `730`                                                                                                                                                                                 |
| ftwrlWaitTimeout                      | Body | Number  | X  | 쿼리 지연 대기 시간(초)<br/>- 최솟값: `0`<br/>- 최댓값: `21600`                                                                                                                                                                            |
| backupRetryCount                      | Body | Number  | X  | 백업 재시도 횟수<br/>- 최솟값: `0`<br/>- 최댓값: `10`                                                                                                                                                                                    |
{{#if (eq engine.lowerCase "mysql")}}
| replicationRegion                     | Body | Enum    | X  | 백업 복제 리전<br />- `KR1`: 한국(판교) 리전<br/>- `KR2`: 한국(평촌) 리전<br/>- `JP1`: 일본(도쿄) 리전                                                                                                                                                       |
{{/if}}
| useBackupLock                         | Body | Boolean | X  | 테이블 잠금 사용 여부                                                                                                                                                                                                                |
| backupSchedules                       | Body | Array   | X  | 예정된 자동 백업 목록                                                                                                                                                                                                                   |
| backupSchedules.backupWndBgnTime      | Body | String  | O  | 백업 시작 시각<br/>- 예시: `00:00:00`                                                                                                                                                                                               |
| backupSchedules.backupWndDuration     | Body | Enum    | O  | 백업 Duration<br/>백업 시작 시각부터 Duration 안에 자동 백업이 실행됩니다.<br/>- `HALF_AN_HOUR`: 30분<br/>- `ONE_HOUR`: 1시간<br/>- `ONE_HOUR_AND_HALF`: 1시간 30분<br/>- `TWO_HOURS`: 2시간<br/>- `TWO_HOURS_AND_HALF`: 2시간 30분<br/>- `THREE_HOURS`: 3시간 |

<details><summary>예시</summary>
<p>

```json
{
    "backupPeriod": 5,
    "useBackupLock": true,
    "backupSchedules": [
        {
            "backupWndBgnTime": "01:00:00",
            "backupWndDuration": "TWO_HOURS"
        }
    ]
}
```

</p>
</details>

<a id="modify-backup-information-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="list-network-information"></a>
### 네트워크 정보 보기 { #list-network-information }

```http
GET /v4.0/db-instances/{dbInstanceId}/network-info
```

<a id="list-network-information-required-permissions"></a>
#### 필요 권한

| 권한명                                        | 설명            |
|--------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Get | DB 인스턴스 상세 보기 |

<a id="list-network-information-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="list-network-information-response"></a>
#### 응답

| 이름                     | 종류   | 형식     | 설명                                                                                                                                      |
|------------------------|------|--------|-----------------------------------------------------------------------------------------------------------------------------------------|
| availabilityZone       | Body | Enum   | DB 인스턴스를 생성할 가용성 영역                                                                                                                     |
| subnet                 | Body | Object | 서브넷 객체                                                                                                                                  |
| subnet.subnetId        | Body | UUID   | 서브넷의 식별자                                                                                                                                |
| subnet.subnetName      | Body | UUID   | 서브넷을 식별할 수 있는 이름                                                                                                                        |
| subnet.subnetCidr      | Body | UUID   | 서브넷의 CIDR                                                                                                                               |
| endPoints              | Body | Array  | 접속 정보 목록                                                                                                                                |
| endPoints.domain       | Body | String | 도메인                                                                                                                                     |
| endPoints.ipAddress    | Body | String | IP 주소                                                                                                                                   |
| endPoints.endPointType | Body | Enum   | 접속 정보 타입<br>-`EXTERNAL`: 외부 접속 도메인<br>-`INTERNAL`: 내부 접속 도메인<br>-`PUBLIC`: (Deprecated) 외부 접속 도메인<br>-`PRIVATE`: (Deprecated) 내부 접속 도메인 |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "availabilityZone": "kr-pub-a",
    "subnet": {
        "subnetId": "bd453789-34ae-416c-9f78-05b9e43a46be",
        "subnetName": "Default Network",
        "subnetCidr": "192.168.0.0/16"
    },
    "endPoints": [
        {
            "domain": "ea548a78-d85f-43b4-8ddf-c88d999b9905.internal.kr1.{{engine.lowerCase}}.rds.nhncloudservice.com",
            "ipAddress": "192.168.0.2",
            "endPointType": "INTERNAL"
        }
    ]
}
```

</p>
</details>

---

<a id="modify-network-information"></a>
### 네트워크 정보 수정하기 { #modify-network-information }

```http
PUT /v4.0/db-instances/{dbInstanceId}/network-info
```

<a id="modify-network-information-required-permissions"></a>
#### 필요 권한

| 권한명                                           | 설명           |
|-----------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:DbInstance.Modify | DB 인스턴스 수정하기 |

<a id="modify-network-information-request"></a>
#### 요청

| 이름              | 종류   | 형식      | 필수 | 설명           |
|-----------------|------|---------|----|--------------|
| dbInstanceId    | URL  | UUID    | O  | DB 인스턴스의 식별자 |
| usePublicAccess | Body | Boolean | O  | 외부 접속 가능 여부 |

<a id="modify-network-information-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="list-db-users"></a>
### DB 사용자 목록 보기 { #list-db-users }

```http
GET /v4.0/db-instances/{dbInstanceId}/db-users
```

<a id="list-db-users-required-permissions"></a>
#### 필요 권한

| 권한명                                             | 설명                  |
|-------------------------------------------------|---------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceUser.List | DB 인스턴스 내 사용자 목록 보기 |

<a id="list-db-users-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="list-db-users-response"></a>
#### 응답

| 이름                           | 종류   | 형식       | 설명                                                                                                                          |
|------------------------------|------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| dbUsers                      | Body | Array    | DB 사용자 목록                                                                                                                   |
| dbUsers.dbUserId             | Body | UUID     | DB 사용자의 식별자                                                                                                                 |
| dbUsers.dbUserName           | Body | String   | DB 사용자 계정 이름                                                                                                                |
| dbUsers.host                 | Body | String   | DB 사용자 계정의 호스트 이름                                                                                                           |
| dbUsers.authorityType        | Body | Enum     | DB 사용자 권한 타입<br/>- `READ`: SELECT 쿼리 수행 가능한 권한<br/>- `CRUD`: DML 쿼리 수행 가능한 권한<br/>- `DDL`: DDL 쿼리 수행 가능한 권한<br/>            |
| dbUsers.dbUserStatus         | Body | Enum     | DB 사용자의 현재 상태<br/>- `STABLE`: 생성됨<br/>- `CREATING`: 생성 중<br/>- `UPDATING`: 수정 중<br/>- `DELETING`: 삭제 중<br/>- `DELETED`: 삭제됨 |
{{#if (eq engine.lowerCase "mysql")}}
| dbUsers.authenticationPlugin | Body | Enum     | 인증 플러그인<br/>- NATIVE: `mysql_native_password`<br />- SHA256: `sha256_password`<br />- CACHING_SHA2: `caching_sha2_password`     |
| dbUsers.tlsOption            | Body | Enum     | TLS Option<br/>- NONE<br />- SSL<br />- X509                                                                                |
{{/if}}
{{#if (eq engine.lowerCase "mariadb")}}
| dbUsers.authenticationPlugin         | Body | Enum    | 인증 플러그인<br/>- NATIVE: `mysql_native_password`<br />- ED25519: `auth_ed25519` |
{{/if}}
| dbUsers.createdYmdt          | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                           |
| dbUsers.updatedYmdt          | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                           |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbUsers": [
        {
            "dbUserId": "4b3d530b-fd02-4d59-a620-83d019a67bbb",
            "dbUserName": "db-user",
            "host": "%",
            "authorityType": "DDL",
            "dbUserStatus": "STABLE",
{{#if (eq engine.lowerCase "mysql")}}
            "authenticationPlugin": "NATIVE",
            "tlsOption": "NONE",
{{/if}}
            "createdYmdt": "2023-03-17T14:02:29+09:00",
            "updatedYmdt": "2023-03-17T14:02:31+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="create-db-user"></a>
### DB 사용자 생성하기 { #create-db-user }

```http
POST /v4.0/db-instances/{dbInstanceId}/db-users
```


<a id="create-db-user-required-permissions"></a>
#### 필요 권한

| 권한명                                               | 설명                 |
|---------------------------------------------------|--------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceUser.Create | DB 인스턴스 내 사용자 생성하기 |

<a id="create-db-user-request"></a>
#### 요청

| 이름                   | 종류   | 형식     | 필수 | 설명                                                                                                               |
|----------------------|------|--------|----|------------------------------------------------------------------------------------------------------------------|
| dbInstanceId         | URL  | UUID   | O  | DB 인스턴스의 식별자                                                                                                     |
| dbUserName           | Body | String | O  | DB 사용자 계정 이름<br/>- 최소 길이: `1`<br/>- 최대 길이: `32`                                                                  |
| dbPassword           | Body | String | O  | DB 사용자 계정 암호<br/>- 최소 길이: `4`<br/>- 최대 길이: `256`                                                                 |
| host                 | Body | String | O  | DB 사용자 계정의 호스트명<br/>- 예시: `1.1.1.%`                                                                              |
| authorityType        | Body | Enum   | O  | DB 사용자 권한 타입<br/>- `READ`: SELECT 쿼리 수행 가능한 권한<br/>- `CRUD`: DML 쿼리 수행 가능한 권한<br/>- `DDL`: DDL 쿼리 수행 가능한 권한<br/> |
{{#if (eq engine.lowerCase "mysql")}}
| authenticationPlugin | Body | Enum   | X  | 인증 플러그인<br/>- 기본값: `NATIVE`(미지원 시 `CACHING_SHA2`)<br/>- NATIVE: `mysql_native_password`<br />- SHA256: `sha256_password`<br />- CACHING_SHA2: `caching_sha2_password` |
| tlsOption            | Body | Enum   | X  | TLS Option<br/>- NONE<br />- SSL<br />- X509                                                                            |

> [주의]
> DB 인스턴스의 `supportAuthenticationPlugin` 값이 true인 DB 인스턴스만 `authenticationPlugin`, `tlsOption`의 값을 설정할 수 있습니다.
{{/if}}
{{#if (eq engine.lowerCase "mariadb")}}
| authenticationPlugin | Body | Enum    | X  | 인증 플러그인<br/>- 기본값: `NATIVE`(미지원 시 `ED25519`)<br/>- NATIVE: `mysql_native_password`<br />- ED25519: `auth_ed25519` |
{{/if}}

<details><summary>예시</summary>
<p>

```json
{
    "dbUserName": "db-user",
    "dbPassword": "password",
    "host": "1.1.1.%",
{{#if (eq engine.lowerCase "mysql")}}
    "authorityType": "CRUD",
    "authenticationPlugin": "NATIVE",
    "tlsOption": "NONE"
{{/if}}
{{#if (eq engine.lowerCase "mariadb")}}
    "authorityType": "CRUD"
{{/if}}
}
```

</p>
</details>

<a id="create-db-user-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="modify-db-user"></a>
### DB 사용자 수정하기 { #modify-db-user }

```http
PUT /v4.0/db-instances/{dbInstanceId}/db-users/{dbUserId}
```

<a id="modify-db-user-required-permissions"></a>
#### 필요 권한

| 권한명                                               | 설명                 |
|---------------------------------------------------|--------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceUser.Modify | DB 인스턴스 내 사용자 수정하기 |

<a id="modify-db-user-request"></a>
#### 요청

| 이름                   | 종류   | 형식     | 필수 | 설명                                                                                                               |
|----------------------|------|--------|----|------------------------------------------------------------------------------------------------------------------|
| dbInstanceId         | URL  | UUID   | O  | DB 인스턴스의 식별자                                                                                                     |
| dbUserId             | URL  | UUID   | O  | DB 사용자의 식별자                                                                                                      |
| dbPassword           | Body | String | X  | DB 사용자 계정 암호<br/>- 최소 길이: `4`<br/>- 최대 길이: `256`                                                                 |
| authorityType        | Body | Enum   | X  | DB 사용자 권한 타입<br/>- `READ`: SELECT 쿼리 수행 가능한 권한<br/>- `CRUD`: DML 쿼리 수행 가능한 권한<br/>- `DDL`: DDL 쿼리 수행 가능한 권한<br/> |
{{#if (eq engine.lowerCase "mysql")}}
| authenticationPlugin | Body | Enum   | X  | 인증 플러그인<br/>- NATIVE: `mysql_native_password`<br />- SHA256: `sha256_password`<br />- CACHING_SHA2: `caching_sha2_password` |
| tlsOption            | Body | Enum   | X  | TLS Option<br/>- NONE<br />- SSL<br />- X509                                                                            |

> [주의]
> DB 인스턴스의 `supportAuthenticationPlugin` 값이 true인 DB 인스턴스만 `authenticationPlugin`, `tlsOption`의 값을 수정할 수 있습니다.
> `authenticationPlugin`의 값은 `dbPassword`와 동시에 수정을 해야 합니다.
{{/if}}
{{#if (eq engine.lowerCase "mariadb")}}
| authenticationPlugin | Body | Enum    | X  | 인증 플러그인<br/>- NATIVE: `mysql_native_password`<br />- ED25519: `auth_ed25519` |
{{/if}}

<details><summary>예시</summary>
<p>

```json
{
    "authorityType": "DDL"
}
```

</p>
</details>

<a id="modify-db-user-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="delete-db-user"></a>
### DB 사용자 삭제하기 { #delete-db-user }

```http
DELETE /v4.0/db-instances/{dbInstanceId}/db-users/{dbUserId}
```

<a id="delete-db-user-required-permissions"></a>
#### 필요 권한

| 권한명                                               | 설명                 |
|---------------------------------------------------|--------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceUser.Delete | DB 인스턴스 내 사용자 삭제하기 |

<a id="delete-db-user-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |
| dbUserId     | URL | UUID | O  | DB 사용자의 식별자  |

<a id="delete-db-user-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="list-db-schema"></a>
### DB 스키마 목록 보기 { #list-db-schema }

```http
GET /v4.0/db-instances/{dbInstanceId}/db-schemas
```

<a id="list-db-schema-required-permissions"></a>
#### 필요 권한

| 권한명                                               | 설명                  |
|---------------------------------------------------|---------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceSchema.List | DB 인스턴스 내 스키마 목록 보기 |

<a id="list-db-schema-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="list-db-schema-response"></a>
#### 응답

| 이름                       | 종류   | 형식       | 설명                                                                                                   |
|--------------------------|------|----------|------------------------------------------------------------------------------------------------------|
| dbSchemas                | Body | Array    | DB 스키마 목록                                                                                            |
| dbSchemas.dbSchemaId     | Body | UUID     | DB 스키마의 식별자                                                                                          |
| dbSchemas.dbSchemaName   | Body | String   | DB 스키마 이름                                                                                            |
| dbSchemas.dbSchemaStatus | Body | Enum     | DB 스키마의 현재 상태<br/>- `STABLE`: 생성됨<br/>- `CREATING`: 생성 중<br/>- `DELETING`: 삭제 중<br/>- `DELETED`: 삭제됨 |
| dbSchemas.createdYmdt    | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                    |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbSchemas": [
        {
            "dbSchemaId": "7c9a94b8-86c1-435d-8af2-82a5e9d53fd4",
            "dbSchemaName": "schema",
            "dbSchemaStatus": "STABLE",
            "createdYmdt": "2023-03-20T13:37:45+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="create-db-schema"></a>
### DB 스키마 생성하기 { #create-db-schema }

```http
POST /v4.0/db-instances/{dbInstanceId}/db-schemas
```

<a id="create-db-schema-required-permissions"></a>
#### 필요 권한

| 권한명                                                 | 설명                 |
|-----------------------------------------------------|--------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceSchema.Create | DB 인스턴스 내 스키마 생성하기 |

<a id="create-db-schema-request"></a>
#### 요청

| 이름           | 종류   | 형식     | 필수 | 설명           |
|--------------|------|--------|----|--------------|
| dbInstanceId | URL  | UUID   | O  | DB 인스턴스의 식별자 |
| dbSchemaName | Body | String | O  | DB 스키마 이름    |

<a id="create-db-schema-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="delete-db-schema"></a>
### DB 스키마 삭제하기 { #delete-db-schema }

```http
DELETE /v4.0/db-instances/{dbInstanceId}/db-schemas/{dbSchemaId}
```

<a id="delete-db-schema-required-permissions"></a>
#### 필요 권한

| 권한명                                                 | 설명                 |
|-----------------------------------------------------|--------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceSchema.Delete | DB 인스턴스 내 스키마 삭제하기 |

<a id="delete-db-schema-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|--------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |
| dbSchemaId   | URL | UUID | O  | DB 스키마의 식별자  |

<a id="delete-db-schema-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="list-log-files"></a>
### 로그 파일 목록 보기 { #list-log-files }

```http
GET /v4.0/db-instances/{dbInstanceId}/log-files
```

<a id="list-log-files-required-permissions"></a>
#### 필요 권한

| 권한명                                            | 설명                    |
|------------------------------------------------|-----------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceLog.List | DB 인스턴스 내 로그 파일 목록 보기 |

<a id="list-log-files-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류    | 형식    | 필수 | 설명                                                                                                                                                                                              |
|--------------|-------|-------|----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dbInstanceId | URL   | UUID  | O  | DB 인스턴스의 식별자                                                                                                                                                                                    |
| logFileTypes | Query | Array | X  | 로그 파일 타입 종류 목록<br/>- `ERROR`: error.log<br/>- `BINLOG`: mysql-bin<br/>- `GENERAL`: general.log<br/>- `SLOW_QUERY`: slow_query.log<br/>- `AUDIT`: server_audit.log<br/>- `BACKUP`: xtra_full.log |

<a id="list-log-files-response"></a>
#### 응답

| 이름                   | 종류   | 형식       | 설명                                                                                                                                                                                           |
|----------------------|------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| logFiles             | Body | Array    | 로그 파일 목록                                                                                                                                                                                     |
| logFiles.logFileName | Body | String   | 로그 파일명                                                                                                                                                                                     |
| logFiles.logFileType | Body | Enum     | 로그 파일 타입 종류<br/>- `ERROR`: error.log<br/>- `BINLOG`: mysql-bin<br/>- `GENERAL`: general.log<br/>- `SLOW_QUERY`: slow_query.log<br/>- `AUDIT`: server_audit.log<br/>- `BACKUP`: xtra_full.log |
| logFiles.logFileSize | Body | Number   | 로그 파일 크기(Byte)                                                                                                                                                                               |
| logFiles.createdYmdt | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                                                                                            |


<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "logFiles": [
        {
            "logFileName": "xtra_full.log-20230317",
            "logFileType": "BACKUP",
            "logFileSize": 4096,
            "createdYmdt": "2023-03-17T14:02:29+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="view-log-file-contents"></a>
### 로그 파일 내용 보기 { #view-log-file-contents }

```http
GET /v4.0/db-instances/{dbInstanceId}/log-files/{logFileName}
```

<a id="view-log-file-contents-required-permissions"></a>
#### 필요 권한

| 권한명                                           | 설명                    |
|-----------------------------------------------|-----------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceLog.Get | DB 인스턴스 내 로그 파일 내용 보기 |

<a id="view-log-file-contents-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류    | 형식     | 필수 | 설명                                                                                                                                                                                              |
|--------------|-------|--------|----|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dbInstanceId | URL   | UUID   | O  | DB 인스턴스의 식별자                                                                                                                                                                                    |
| logFileName  | URL   | String | O  | 로그 파일명                                                                                                                                                                                        |
| logFileType  | Query | Enum   | O  | 로그 파일 타입 종류<br/>- `ERROR`: error.log<br/>- `BINLOG`: mysql-bin<br/>- `GENERAL`: general.log<br/>- `SLOW_QUERY`: slow_query.log<br/>- `AUDIT`: server_audit.log<br/>- `BACKUP`: xtra_full.log |

<a id="view-log-file-contents-response"></a>
#### 응답

| 이름      | 종류   | 형식     | 설명                        |
|---------|------|--------|---------------------------|
| content | Body | String | 로그 파일 내용(최대 65533 Bytes) |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "content": "..."
}
```

</p>
</details>

---

<a id="export-log-file"></a>
### 로그 파일 내보내기 { #export-log-file }

```http
POST /v4.0/db-instances/{dbInstanceId}/log-files/export
```

<a id="export-log-file-required-permissions"></a>
#### 필요 권한

| 권한명                                              | 설명                   |
|--------------------------------------------------|----------------------|
| RDSfor{{engine.pascalCase}}:DbInstanceLog.Export | DB 인스턴스 내 로그 파일 내보내기 |

<a id="export-log-file-request"></a>
#### 요청

| 이름              | 종류   | 형식     | 필수 | 설명                             |
|-----------------|------|--------|----|--------------------------------|
| dbInstanceId    | URL  | UUID   | O  | DB 인스턴스의 식별자                   |
| logFileNames    | Body | Array  | O  | 로그 파일명 목록<br/>- 최소 크기: `1`   |
| tenantId        | Body | String | O  | 로그 파일이 저장될 오브젝트 스토리지의 테넌트 ID   |
| username        | Body | String | O  | NHN Cloud 계정 또는 IAM 계정 ID      |
| password        | Body | String | O  | 로그 파일이 저장될 오브젝트 스토리지의 API 비밀번호 |
| targetContainer | Body | String | O  | 로그 파일이 저장될 오브젝트 스토리지의 컨테이너     |
| objectPath      | Body | String | O  | 컨테이너에 저장될 로그 파일의 경로            |

<details><summary>예시</summary>
<p>

```json
{
    "logFileNames": ["xtra_full.log-20230317"],
    "tenantId": "399631c404744dbbb18ce4fa2dc71a5a",
    "username": "gildong.hong@nhn.com",
    "password": "password",
    "targetContainer": "container",
    "objectPath": "logs/backup"
}
```

</p>
</details>

<a id="export-log-file-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="view-binlog-lists"></a>
### BinLog 목록 보기 { #view-binlog-lists }

```http
GET /v4.0/db-instances/{dbInstanceId}/binlogs
```

<a id="view-binlog-lists-required-permission"></a>
#### 필요 권한

| 권한명                                               | 설명           |
|---------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstanceBinLog.List | BinLog 목록 보기 |

<a id="view-binlog-lists-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류    | 형식      | 필수 | 설명                                                                                   |
|--------------|-------|---------|----|---------------------------------------------------------------------------------------|
| dbInstanceId | URL   | UUID    | O  | DB 인스턴스의 식별자                                                                         |
| deletable    | Query | Boolean | X  | 삭제 가능한 BinLog만 조회할지 여부<br/>- `true`: 마지막 BinLog 제외<br/>- `false`: 전체<br/>- 기본값: `false` |

<a id="view-binlog-lists-response"></a>
#### 응답

| 이름                     | 종류   | 형식       | 설명                                |
|------------------------|------|----------|-----------------------------------|
| binLogs                | Body | Array    | BinLog 파일 목록                      |
| binLogs.binLogFileName | Body | String   | BinLog 파일명                      |
| binLogs.binLogFileSize | Body | Number   | BinLog 파일 크기(Byte)                |
| binLogs.createdYmdt    | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "binLogs": [
        {
            "binLogFileName": "mysql-bin.000001",
            "binLogFileSize": 1073741824,
            "createdYmdt": "2023-03-17T14:02:29+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="delete-binlog"></a>
### BinLog 삭제 { #delete-binlog }

```http
POST /v4.0/db-instances/{dbInstanceId}/binlogs/purge
```

<a id="delete-binlog-required-permission"></a>
#### 필요 권한

| 권한명                                                | 설명        |
|----------------------------------------------------|------------|
| RDSfor{{engine.pascalCase}}:DbInstanceBinLog.Purge | BinLog 삭제 |

<a id="delete-binlog-request"></a>
#### 요청

| 이름                 | 종류   | 형식     | 필수 | 설명                                     |
|--------------------|------|--------|----|----------------------------------------|
| dbInstanceId       | URL  | UUID   | O  | DB 인스턴스의 식별자                           |
| lastBinLogFileName | Body | String | O  | 삭제할 마지막 BinLog 파일명(해당 파일 직전까지 삭제됩니다) |

<details><summary>예시</summary>
<p>

```json
{
    "lastBinLogFileName": "mysql-bin.000010"
}
```

</p>
</details>

<a id="delete-binlog-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="view-certificate-file-lists"></a>
### 인증서 파일 목록 보기 { #view-certificate-file-lists }

```http
GET /v4.0/db-instances/{dbInstanceId}/certificates
```

<a id="view-certificate-file-lists-required-permission"></a>
#### 필요 권한

| 권한명                                                    | 설명           |
|--------------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbInstanceCertificate.List | 인증서 파일 목록 보기 |

<a id="view-certificate-file-lists-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름           | 종류  | 형식   | 필수 | 설명           |
|--------------|-----|------|----|---------------|
| dbInstanceId | URL | UUID | O  | DB 인스턴스의 식별자 |

<a id="view-certificate-file-lists-response"></a>
#### 응답

| 이름                           | 종류   | 형식       | 설명                                                                           |
|------------------------------|------|----------|------------------------------------------------------------------------------|
| certificates                 | Body | Array    | 인증서 파일 목록                                                                    |
| certificates.fileName        | Body | String   | 인증서 파일명                                                                    |
| certificates.certificateType | Body | Enum     | 인증서 타입<br/>- `CA_FILE`: CA 인증서<br/>- `CERT_FILE`: 인증서<br/>- `KEY_FILE`: 비밀 키 |
| certificates.fileSize        | Body | Number   | 인증서 파일 크기(Byte)                                                              |
| certificates.createdYmdt     | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                            |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "certificates": [
        {
            "fileName": "ca.pem",
            "certificateType": "CA_FILE",
            "fileSize": 2048,
            "createdYmdt": "2023-03-17T14:02:29+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="export-a-certificate-file"></a>
### 인증서 파일 내보내기 { #export-a-certificate-file }

```http
POST /v4.0/db-instances/{dbInstanceId}/certificates/upload
```

<a id="export-a-certificate-file-required-permission"></a>
#### 필요 권한

| 권한명                                                      | 설명          |
|----------------------------------------------------------|-------------|
| RDSfor{{engine.pascalCase}}:DbInstanceCertificate.Export | 인증서 파일 내보내기 |

<a id="export-a-certificate-file-request"></a>
#### 요청

| 이름               | 종류   | 형식     | 필수 | 설명                                                                           |
|------------------|------|--------|----|------------------------------------------------------------------------------|
| dbInstanceId     | URL  | UUID   | O  | DB 인스턴스의 식별자                                                                 |
| certificateTypes | Body | Array  | O  | 업로드할 인증서 타입<br/>- `CA_FILE`: CA 인증서<br/>- `CERT_FILE`: 인증서<br/>- `KEY_FILE`: 비밀 키 |
| tenantId         | Body | String | O  | 인증서 파일이 저장될 오브젝트 스토리지의 테넌트 ID                                                |
| username         | Body | String | O  | NHN Cloud 계정 또는 IAM 계정 ID                                                    |
| password         | Body | String | O  | 인증서 파일이 저장될 오브젝트 스토리지의 API 비밀번호                                              |
| targetContainer  | Body | String | O  | 인증서 파일이 저장될 오브젝트 스토리지의 컨테이너                                                  |
| objectPath       | Body | String | O  | 컨테이너에 저장될 인증서 파일의 경로                                                         |

<details><summary>예시</summary>
<p>

```json
{
    "certificateTypes": ["CA_FILE", "CERT_FILE", "KEY_FILE"],
    "tenantId": "399631c404744dbbb18ce4fa2dc71a5a",
    "username": "gildong.hong@nhn.com",
    "password": "password",
    "targetContainer": "container",
    "objectPath": "certificates/"
}
```

</p>
</details>

<a id="export-a-certificate-file-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="backups"></a>
## 백업 { #backups }

<a id="backup-status"></a>
### 백업 상태 { #backup-status }

| 상태           | 설명           |
|--------------|--------------|
| `BACKING_UP` | 백업 중인 경우     |
| `COMPLETED`  | 백업이 완료된 경우   |
| `DELETING`   | 백업이 삭제 중인 경우 |
| `DELETED`    | 백업이 삭제된 경우   |
| `ERROR`      | 오류가 발생한 경우   |

<a id="view-backup-details"></a>
### 백업 상세 보기 { #view-backup-details }

```http
GET /v4.0/backups/{backupId}
```

<a id="view-backup-details-required-permission"></a>
#### 필요 권한

| 권한명                                    | 설명       |
|----------------------------------------|----------|
| RDSfor{{engine.pascalCase}}:Backup.Get | 백업 상세 보기 |

<a id="view-backup-details-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름       | 종류  | 형식   | 필수 | 설명      |
|----------|-----|------|----|---------|
| backupId | URL | UUID | O  | 백업의 식별자 |

<a id="view-backup-details-response"></a>
#### 응답

| 이름                      | 종류   | 형식       | 설명              |
|-------------------------|------|----------|-----------------|
| backup                  | Body | Object   | 백업 상세 정보        |
| backup.backupId         | Body | UUID     | 백업의 식별자         |
| backup.regionCode       | Body | Enum     | 리전 코드           |
| backup.backupName       | Body | String   | 백업을 식별할 수 있는 이름 |
| backup.backupStatus     | Body | Enum     | 백업의 현재 상태       |
| backup.dbInstanceId     | Body | UUID     | 원본 DB 인스턴스의 식별자 |
| backup.dbInstanceName   | Body | String   | 원본 DB 인스턴스의 이름  |
| backup.dbVersion        | Body | Enum     | DB 엔진 버전        |
{{#if (eq engine.lowerCase "mysql")}}
| backup.utilVersion      | Body | String   | 백업에 사용된 xtrabackup 유틸리티 버전        |
{{/if}}
| backup.backupType       | Body | Enum     | 백업 유형                             |
| backup.backupMethodType | Body | Enum     | 백업 방식                             |
| backup.backupFileType   | Body | Enum     | 백업 파일 유형                          |
| backup.backupSize       | Body | Number   | 백업의 크기(Byte)                      |
| backup.isReplicable     | Body | Boolean  | 복제 가능 여부                          |
| backup.binLogFileName   | Body | String   | 바이너리 로그 파일명                       |
| backup.binLogPosition   | Body | Number   | 바이너리 로그 위치                        |
| backup.createdYmdt      | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| backup.updatedYmdt      | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "backup": {
        "backupId": "0017f136-3e01-4530-94aa-20661afe6632",
        "regionCode": "KR1",
        "backupName": "backup",
        "backupStatus": "COMPLETED",
        "dbInstanceId": "142e6ccc-3bfb-4e1e-84f7-38861284fafd",
        "dbInstanceName": "db-instance",
        "dbVersion": "{{engine.sampleDbVersionCode}}",
{{#if (eq engine.lowerCase "mysql")}}
        "utilVersion": "8.0.28",
{{/if}}
        "backupType": "AUTO",
        "backupMethodType": "FULL",
        "backupFileType": "XTRA_BACKUP",
        "backupSize": 4996786,
        "isReplicable": true,
        "binLogFileName": "mysql-bin.000001",
        "binLogPosition": 154,
        "createdYmdt": "2023-02-21T00:35:00+09:00",
        "updatedYmdt": "2023-02-22T00:35:32+09:00"
    }
}
```

</p>
</details>

---

<a id="retrieve-backup-list"></a>
### 백업 목록 조회 { #retrieve-backup-list }

```http
GET /v4.0/backups
```

<a id="retrieve-backup-list-required-permissions"></a>
#### 필요 권한

| 권한명                                     | 설명       |
|-----------------------------------------|----------|
| RDSfor{{engine.pascalCase}}:Backup.List | 백업 목록 조회 |

<a id="retrieve-backup-list-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름                | 종류    | 형식       | 필수 | 설명                                                                                                                                   |
|-------------------|-------|----------|----|--------------------------------------------------------------------------------------------------------------------------------------|
| page              | Query | Number   | X  | 조회할 목록의 페이지<br/>- 기본값: 1 <br/>- 최솟값: `1`                                                                                                           |
| size              | Query | Number   | X  | 조회할 목록의 페이지 크기<br/>- 기본값: 20                                        |
| backupType   | Query | Enum   | X  | 백업 유형<br/>- `AUTO`: 자동<br/>- `MANUAL`:  수동<br/>- 기본값: 전체 |
| dbInstanceId | Query | UUID   | X  | 원본 DB 인스턴스의 식별자                                          |
| dbVersion    | Query | Enum   | X  | DB 엔진 유형                                                 |

<a id="retrieve-backup-list-response"></a>
#### 응답

| 이름                   | 종류   | 형식       | 설명                                |
|----------------------|------|----------|-----------------------------------|
| totalCounts          | Body | Number   | 전체 백업 목록 수                        |
| backups              | Body | Array    | 백업 목록                             |
| backups.backupId     | Body | UUID     | 백업의 식별자                           |
| backups.backupName   | Body | String   | 백업을 식별할 수 있는 이름                   |
| backups.backupStatus | Body | Enum     | 백업의 현재 상태                         |
| backups.dbInstanceId | Body | UUID     | 원본 DB 인스턴스의 식별자                   |
| backups.dbVersion    | Body | Enum     | DB 엔진 유형                          |
{{#if (eq engine.lowerCase "mysql")}}    
| backups.utilVersion  | Body | String   | 백업에 사용된 xtrabackup 유틸리티 버전        |
{{/if}}
| backups.backupType   | Body | Enum     | 백업 유형                             |
| backups.backupSize   | Body | Number   | 백업의 크기(Byte)                      |
| createdYmdt          | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt          | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<details><summary>예시</summary>
<p>

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
            "backupId": "0017f136-3e01-4530-94aa-20661afe6632",
            "backupName": "backup",
            "backupStatus": "COMPLETED",
            "dbInstanceId": "142e6ccc-3bfb-4e1e-84f7-38861284fafd",
            "dbVersion": "{{engine.sampleDbVersionCode}}",
{{#if (eq engine.lowerCase "mysql")}}    
            "utilVersion": "8.0.28",
{{/if}}
            "backupType": "AUTO",
            "backupSize": 4996786,
            "createdYmdt": "2023-02-21T00:35:00+09:00",
            "updatedYmdt": "2023-02-22T00:35:32+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="create-backup"></a>
### 백업 생성하기 { #create-backup }

```http
POST /v4.0/backups
```

<a id="create-backup-required-permissions"></a>
#### 필요 권한

| 권한명                                       | 설명      |
|-------------------------------------------|---------|
| RDSfor{{engine.pascalCase}}:Backup.Create | 백업 생성하기 |

<a id="create-backup-common-request"></a>
#### 공통 요청

| 이름               | 종류   | 형식     | 필수 | 설명                                                                                   |
|------------------|------|--------|----|--------------------------------------------------------------------------------------|
| backupName       | Body | String | O  | 백업을 식별할 수 있는 이름                                                                      |
| backupMethodType | Body | Enum   | O  | 백업 방식 타입 종류<br/>- `FULL`: 전체 백업<br/>- `INCREMENTAL`: 증분 백업 <br/>- `SNAPSHOT`: 스냅숏 백업 |

<a id="create-backup-if-backupmethodtype-is-full"></a>
#### 전체 백업(backupMethodType이 `FULL`인 경우)

| 이름           | 종류   | 형식   | 필수 | 설명           |
|--------------|------|------|----|--------------|
| dbInstanceId | Body | UUID | O  | DB 인스턴스의 식별자 |


<details><summary>예시</summary>
<p>

```json
{
    "backupName": "example-backup-name",
    "backupMethodType": "FULL",
    "dbInstanceId": "142e6ccc-3bfb-4e1e-84f7-38861284fafd"
}
```

</p>
</details>

<a id="create-backup-if-backupmethodtype-is-incremental"></a>
#### 증분 백업(backupMethodType이 `INCREMENTAL`인 경우)

| 이름           | 종류   | 형식   | 필수 | 설명         |
|--------------|------|------|----|------------|
| baseBackupId | Body | UUID | O  | 기준 백업의 식별자 |


<details><summary>예시</summary>
<p>

```json
{
    "backupName": "example-backup-name",
    "backupMethodType": "INCREMENTAL",
    "baseBackupId": "3ae7914f-9b42-4729-b125-87417b72cf36"
}
```

</p>
</details>


<a id="create-backup-snapshot-backup-if-backupmethodtype-is-snapshot"></a>
#### 스냅숏 백업(backupMethodType이 `SNAPSHOT`인 경우)

| 이름           | 종류   | 형식   | 필수 | 설명           |
|--------------|------|------|----|--------------|
| dbInstanceId | Body | UUID | O  | DB 인스턴스의 식별자 |


<details><summary>예시</summary>
<p>

```json
{
    "backupName": "example-backup-name",
    "backupMethodType": "SNAPSHOT",
    "dbInstanceId": "142e6ccc-3bfb-4e1e-84f7-38861284fafd"
}
```

</p>
</details>


<a id="create-backup-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="export-backup"></a>
### 백업 내보내기 { #export-backup }

```http
POST /v4.0/backups/{backupId}/export
```

<a id="export-backup-required-permissions"></a>
#### 필요 권한

| 권한명                                       | 설명      |
|-------------------------------------------|---------|
| RDSfor{{engine.pascalCase}}:Backup.Export | 백업 내보내기 |

<a id="export-backup-request"></a>
#### 요청

| 이름              | 종류   | 형식     | 필수 | 설명                          |
|-----------------|------|--------|----|-----------------------------|
| backupId        | URL  | UUID   | O  | 백업의 식별자                     |
| tenantId        | Body | String | O  | 백업이 저장될 오브젝트 스토리지의 테넌트 ID   |
| username        | Body | String | O  | NHN Cloud 계정 또는 IAM 계정 ID   |
| password        | Body | String | O  | 백업이 저장될 오브젝트 스토리지의 API 비밀번호 |
| targetContainer | Body | String | O  | 백업이 저장될 오브젝트 스토리지의 컨테이너     |
| objectPath      | Body | String | O  | 컨테이너에 저장될 백업의 경로            |

<details><summary>예시</summary>
<p>

```json
{
    "tenantId": "399631c404744dbbb18ce4fa2dc71a5a",
    "username": "gildong.hong@nhn.com",
    "password": "password",
    "targetContainer": "container",
    "objectPath": "backups/backup_file"
}
```

</p>
</details>

<a id="export-backup-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

> [주의]
> 수동 백업의 경우 백업이 수행된 DB 인스턴스가 존재하지 않으면, 백업을 오브젝트 스토리지로 내보낼 수 없습니다.

---

<a id="restore-backup"></a>
### 백업 복원하기 { #restore-backup }

```http
POST /v4.0/backups/{backupId}/restore
```

<a id="restore-backup-required-permissions"></a>
#### 필요 권한

| 권한명                                        | 설명      |
|--------------------------------------------|---------|
| RDSfor{{engine.pascalCase}}:Backup.Restore | 백업 복원하기 |

<a id="restore-backup-request"></a>
#### 요청

| 이름                                           | 종류   | 형식      | 필수 | 설명                                                                  |
|----------------------------------------------|------|---------|----|---------------------------------------------------------------------|
| backupId                                     | URL  | UUID    | O  | 백업의 식별자                                                             |
| dbInstanceName                               | Body | String  | O  | DB 인스턴스를 식별할 수 있는 마스터 이름                                            |
| dbInstanceCandidateName                      | Body | String  | X  | DB 인스턴스를 식별할 수 있는 예비 마스터 이름(고가용성 사용 시 필수 값)                         |
| description                                  | Body | String  | X  | DB 인스턴스에 대한 추가 정보                                                   |
| dbFlavorId                                   | Body | UUID    | X  | DB 인스턴스 사양의 식별자          <br/> - 기본값: 원본 DB 인스턴스 값                                           |
| dbPort                                       | Body | Integer | X  | DB 포트 <br/> - 기본값: 원본 DB 인스턴스 값     <br/>- 최솟값: `3306`<br/>- 최댓값: `43306`                          |
| parameterGroupId                             | Body | UUID    | X  | 파라미터 그룹의 식별자    <br/> - 기본값: 원본 DB 인스턴스 값                                                          |
| dbSecurityGroupIds                           | Body | Array   | X  | DB 보안 그룹의 식별자 목록                                                    ||network|Body|Object|O|네트워크 정보 객체|
| userGroupIds                                 | Body | Array   | X  | 사용자 그룹의 식별자 목록                                                      |
| useHighAvailability                          | Body | Boolean | X  | 고가용성 사용 여부<br/>- 기본값: `false`                                       |
| pingInterval                                 | Body | Number  | X  | 고가용성 사용 시 Ping 간격(초)<br/>- 기본값: `3`<br/>- 최솟값: `1`<br/>- 최댓값: `600` |
| pingType                                     | Body | Enum    | X  | 고가용성 사용 시 Ping 타입<br/>- 기본값: `INSERT`<br/>- `INSERT`<br/>- `SELECT` |
| useDefaultNotification                       | Body | Boolean | X  | 기본 알림 사용 여부<br/>- 기본값: `false`                                      |
| useDeletionProtection                        | Body | Boolean | X  | 삭제 보호 여부<br/>- 기본값: `false`                                         | 
| useSlowQueryAnalysis                         | Body | Boolean | X  | Slow query 분석 여부<br/>- 기본값: `true`                                  |
| network                                      | Body | Object  | X  | 네트워크 정보 객체                                                          |
| network.subnetId                             | Body | UUID    | X  | 서브넷의 식별자<br/>- 기본값: 원본 DB 인스턴스 값                                                            |
| network.usePublicAccess                      | Body | Boolean | X  | 외부 접속 가능 여부<br/>- 기본값: `false`                                      |
| network.availabilityZone                     | Body | Enum    | X  | DB 인스턴스를 생성할 가용성 영역<br/>- 예시: `kr-pub-a`<br/>- 기본값: 랜덤 선택                            |
| storage                                      | Body | Object  | X  | 데이터 스토리지 정보 객체                                                      |
| storage.storageType                          | Body | Enum    | X  | 데이터 스토리지 타입<br/>- 예시: `General SSD`<br/>- 기본값: 원본 DB 인스턴스 값                                 |
| storage.storageSize                          | Body | Number  | X  | 데이터 스토리지 크기(GB)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `20`<br/>- 최댓값: `2048`                   |
| storage.storageAutoscale                     | Body | Object  | X  | 데이터 스토리지 자동 확장 객체                                                   |
| storage.storageAutoscale.useStorageAutoscale | Body | Boolean | X  | 스토리지 자동 확장 여부    <br/> - 기본값: 원본 DB 인스턴스 값                                                         |
| storage.storageAutoscale.threshold           | Body | Number  | X  | 자동 확장 조건(%) <br/> - 기본값: 원본 DB 인스턴스 값     <br/>- 최솟값: `50`<br/>- 최댓값: `95`                         |
| storage.storageAutoscale.maxStorageSize      | Body | Number  | X  | 자동 확장 최대 크기(GB) <br/> - 기본값: 원본 DB 인스턴스 값     <br/>- 최댓값: `4096`                                   |
| storage.storageAutoscale.cooldownTime        | Body | Number  | X  | 자동 확장 쿨다운 시간(분) <br/> - 기본값: 원본 DB 인스턴스 값     <br/>- 최솟값: `10`<br/>- 최댓값: `1440`                   |
| backup                                       | Body | Object  | X  | 백업 정보 객체                                                            |
| backup.backupPeriod                          | Body | Number  | X  | 백업 보관 기간(일)<br/>- 기본값: 원본 DB 인스턴스 값<br/>- 최솟값: `0`<br/>- 최댓값: `730`                         |
| backup.ftwrlWaitTimeout                      | Body | Number  | X  | 쿼리 지연 대기 시간(초)<br/>- 기본값: `1800`<br/>- 최솟값: `0`<br/>- 최댓값: `21600`  |
| backup.backupRetryCount                      | Body | Number  | X  | 백업 재시도 횟수<br/>- 기본값: `0`<br/>- 최솟값: `0`<br/>- 최댓값: `10`             |
{{#if (eq engine.lowerCase "mysql")}}
| backup.replicationRegion                     | Body | Enum    | X  | 백업 복제 리전<br />- `KR1`: 한국(판교) 리전<br/>- `KR2`: 한국(평촌) 리전<br/>- `JP1`: 일본(도쿄) 리전                                                                                                                                                       |
{{/if}}
| backup.useBackupLock                         | Body | Boolean | X  | 테이블 잠금 사용 여부<br/>- 기본값: `true`                                                                                                                                                                                              |
| backup.backupSchedules                       | Body | Array   | X  | 예정된 자동 백업 목록<br/>- 기본값: 원본 DB 인스턴스 값                                                                                                                                                                                                                   |
| backup.backupSchedules.backupWndBgnTime      | Body | String  | O  | 백업 시작 시각<br/>- 예시: `00:00:00`                                                                                                                                                                                               |
| backup.backupSchedules.backupWndDuration     | Body | Enum    | O  | 백업 Duration<br/>백업 시작 시각부터 Duration 안에 자동 백업이 실행됩니다.<br/>- `HALF_AN_HOUR`: 30분<br/>- `ONE_HOUR`: 1시간<br/>- `ONE_HOUR_AND_HALF`: 1시간 30분<br/>- `TWO_HOURS`: 2시간<br/>- `TWO_HOURS_AND_HALF`: 2시간 30분<br/>- `THREE_HOURS`: 3시간 |

<details><summary>예시</summary>
<p>

```json

{
    "dbInstanceName": "db-instance-restore",
    "dbFlavorId": "50be6d9c-02d6-4594-a2d4-12010eb65ec0",
    "dbPort": 10000,
    "parameterGroupId": "132d383c-38e3-468a-a826-5e9a8fff15d0",
    "network": {
        "subnetId": "e721a9dd-dad0-4cf0-a53b-dd654ebfc683",
        "availabilityZone": "kr-pub-a"
    },
    "storage": {
        "storageType": "General SSD",
        "storageSize": 20
    },
    "backup": {
        "backupPeriod": 1,
        "backupSchedules": [
            {
                "backupWndBgnTime": "00:00:00",
                "backupWndDuration": "HALF_AN_HOUR"
            }
        ]
    }
}
```

</p>
</details>

<a id="restore-backup-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="delete-backup"></a>
### 백업 삭제하기 { #delete-backup }

```http
DELETE /v4.0/backups/{backupId}
```

<a id="delete-backup-required-permissions"></a>
#### 필요 권한

| 권한명                                       | 설명      |
|-------------------------------------------|---------|
| RDSfor{{engine.pascalCase}}:Backup.Delete | 백업 삭제하기 |

<a id="delete-backup-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름       | 종류  | 형식   | 필수 | 설명      |
|----------|-----|------|----|---------|
| backupId | URL | UUID | O  | 백업의 식별자 |

<a id="delete-backup-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="db-security-group"></a>
## DB 보안 그룹 { #db-security-group }

<a id="db-security-group-progress"></a>
### DB 보안 그룹 진행 상태 { #db-security-group-progress }

| 상태              | 설명           |
|-----------------|--------------|
| `NONE`          | 진행 중인 작업이 없음 |
| `CREATING_RULE` | 규칙 정책 생성 중   |
| `UPDATING_RULE` | 규칙 정책 수정 중   |
| `DELETING_RULE` | 규칙 정책 삭제 중   |

<a id="list-db-security-groups"></a>
### DB 보안 그룹 목록 보기 { #list-db-security-groups }

```http
GET /v4.0/db-security-groups
```

<a id="list-db-security-groups-required-permissions"></a>
#### 필요 권한

| 권한명                                              | 설명             |
|--------------------------------------------------|----------------|
| RDSfor{{engine.pascalCase}}:DbSecurityGroup.List | DB 보안 그룹 목록 보기 |

<a id="list-db-security-groups-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름                | 종류    | 형식       | 필수 | 설명                                                                                                                                   |
|-------------------|-------|----------|----|--------------------------------------------------------------------------------------------------------------------------------------|
| page              | Query | Number   | X  | 조회할 목록의 페이지<br/>- 기본값: 1 <br/>- 최솟값: `1`                                                                                                           |
| size              | Query | Number   | X  | 조회할 목록의 페이지 크기<br/>- 기본값: 20                                        |

<a id="list-db-security-groups-response"></a>
#### 응답

| 이름                                   | 종류   | 형식       | 설명                                |
|--------------------------------------|------|----------|-----------------------------------|
| dbSecurityGroups                     | Body | Array    | DB 보안 그룹 목록                       |
| dbSecurityGroups.dbSecurityGroupId   | Body | UUID     | DB 보안 그룹의 식별자                     |
| dbSecurityGroups.dbSecurityGroupName | Body | String   | DB 보안 그룹을 식별할 수 있는 이름             |
| dbSecurityGroups.description         | Body | String   | DB 보안 그룹에 대한 추가 정보                |
| dbSecurityGroups.progressStatus      | Body | Enum     | DB 보안 그룹의 현재 진행 상태                |
| dbSecurityGroups.createdYmdt         | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| dbSecurityGroups.updatedYmdt         | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbSecurityGroups": [
        {
            "dbSecurityGroupId": "fe4f2aee-afbb-4c19-a5e9-eb2eab394708",
            "dbSecurityGroupName": "dbSecurityGroup",
            "description": "description",
            "progressStatus": "NONE",
            "createdYmdt": "2023-02-19T19:18:13+09:00",
            "updatedYmdt": "2022-02-19T19:18:13+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="list-db-security-group-details"></a>
### DB 보안 그룹 상세 보기 { #list-db-security-group-details }

```http
GET /v4.0/db-security-groups/{dbSecurityGroupId}
```

<a id="list-db-security-group-details-required-permissions"></a>
#### 필요 권한

| 권한명                                             | 설명             |
|-------------------------------------------------|----------------|
| RDSfor{{engine.pascalCase}}:DbSecurityGroup.Get | DB 보안 그룹 상세 보기 |

<a id="list-db-security-group-details-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름                | 종류  | 형식   | 필수 | 설명            |
|-------------------|-----|------|----|---------------|
| dbSecurityGroupId | URL | UUID | O  | DB 보안 그룹의 식별자 |

<a id="list-db-security-group-details-response"></a>
#### 응답

| 이름                  | 종류   | 형식       | 설명                                                                                                                 |
|---------------------|------|----------|--------------------------------------------------------------------------------------------------------------------|
| dbSecurityGroupId   | Body | UUID     | DB 보안 그룹의 식별자                                                                                                      |
| dbSecurityGroupName | Body | String   | DB 보안 그룹을 식별할 수 있는 이름                                                                                              |
| description         | Body | String   | DB 보안 그룹에 대한 추가 정보                                                                                                 |
| progressStatus      | Body | Enum     | DB 보안 그룹의 현재 진행 상태                                                                                                 |
| rules               | Body | Array    | DB 보안 그룹 규칙 목록                                                                                                     |
| rules.ruleId        | Body | UUID     | DB 보안 그룹 규칙의 식별자                                                                                                   |
| rules.description   | Body | String   | DB 보안 그룹 규칙에 대한 추가 정보                                                                                              |
| rules.direction     | Body | Enum     | 통신 방향<br/>- `INGRESS`: 수신<br/>- `EGRESS`: 송신                                                                       |
| rules.etherType     | Body | Enum     | Ether 타입<br/>- `IPV4`: IPv4<br/>- `IPV6`: IPv6                                                                     |
| rules.port          | Body | Object   | 포트 객체                                                                                                              |
| rules.port.portType | Body | Enum     | 포트 타입<br/>- `DB_PORT`: 각 DB 인스턴스 포트값으로 설정됩니다.<br/>- `PORT`: 지정된 포트값으로 설정됩니다.<br/>- `PORT_RANGE`: 지정된 포트 범위로 설정됩니다. |
| rules.port.minPort  | Body | Number   | 최소 포트 범위                                                                                                           |
| rules.port.maxPort  | Body | Number   | 최대 포트 범위                                                                                                           |
| rules.cidr          | Body | String   | 허용할 트래픽의 원격 소스                                                                                                     |
| rules.createdYmdt   | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                  |
| rules.updatedYmdt   | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                  |
| createdYmdt         | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                  |
| updatedYmdt         | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                  |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "dbSecurityGroup": {
        "dbSecurityGroupId": "fe4f2aee-afbb-4c19-a5e9-eb2eab394708",
        "dbSecurityGroupName": "dbSecurityGroup",
        "description": "description",
        "progressStatus": "NONE",
        "rules": [
            {
                "ruleId": "17c88ef6-95f1-4678-84f9-fee1b22e250d",
                "description": "description",
                "direction": "INGRESS",
                "etherType": "IPV4",
                "port": {
                    "portType": "PORT_RANGE",
                    "minPort": 10000,
                    "maxPort": 10005
                },
                "cidr": "0.0.0.0/0",
                "createdYmdt": "2023-02-19T19:18:13+09:00",
                "updatedYmdt": "2023-02-19T19:18:13+09:00"
            }
        ],
        "createdYmdt": "2023-02-19T19:18:13+09:00",
        "updatedYmdt": "2023-02-19T19:18:13+09:00"
    }
}
```

</p>
</details>

---

<a id="create-db-security-group"></a>
### DB 보안 그룹 생성하기 { #create-db-security-group }

```http
POST /v4.0/db-security-groups
```

<a id="create-db-security-group-required-permissions"></a>
#### 필요 권한

| 권한명                                                | 설명            |
|----------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbSecurityGroup.Create | DB 보안 그룹 생성하기 |

<a id="create-db-security-group-request"></a>
#### 요청

| 이름                  | 종류   | 형식     | 필수 | 설명                                                                                                                                                                                       |
|---------------------|------|--------|----|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dbSecurityGroupName | Body | String | O  | DB 보안 그룹을 식별할 수 있는 이름                                                                                                                                                                    |
| description         | Body | String | X  | DB 보안 그룹에 대한 추가 정보                                                                                                                                                                       |
| rules               | Body | Array  | O  | DB 보안 그룹 규칙 목록                                                                                                                                                                           |
| rules.description   | Body | String | X  | DB 보안 그룹 규칙에 대한 추가 정보                                                                                                                                                                    |
| rules.direction     | Body | Enum   | O  | 통신 방향<br/>- `INGRESS`: 수신<br/>- `EGRESS`: 송신                                                                                                                                             |
| rules.etherType     | Body | Enum   | O  | Ether 타입<br/>- `IPV4`: IPv4<br/>- `IPV6`: IPv6                                                                                                                                           |
| rules.cidr          | Body | String | O  | 허용할 트래픽의 원격 소스<br/>- 예시: `1.1.1.1/32`                                                                                                                                                    |
| rules.port          | Body | Object | O  | 포트 객체                                                                                                                                                                                    |
| rules.port.portType | Body | Enum   | O  | 포트 타입<br/>- `DB_PORT`: 각 DB 인스턴스 포트값으로 설정됩니다. `minPort`값과 `maxPort`값이 필요하지 않습니다.<br/>- `PORT`: 지정된 포트값으로 설정됩니다. `minPort`값과 `maxPort`값이 같아야 합니다.<br/>- `PORT_RANGE`: 지정된 포트 범위로 설정됩니다. |
| rules.port.minPort  | Body | Number | X  | 최소 포트 범위<br/>- 최솟값: 1                                                                                                                                                                    |
| rules.port.maxPort  | Body | Number | X  | 최대 포트 범위<br/>- 최댓값: 65535                                                                                                                                                                |

> [주의]
> DB 포트는 송신 방향으로 설정할 수 없습니다.

<details><summary>예시</summary>
<p>

```json
{
    "dbSecurityGroupName": "dbSecurityGroup",
    "description": "description",
    "rules": [
        {
            "direction": "INGRESS",
            "etherType": "IPV4",
            "port": {
                "portType": "PORT_RANGE",
                "minPort": 10000,
                "maxPort": 10005
            },
            "cidr": "0.0.0.0/0"
        }
    ]
}
```

</p>
</details>

<a id="create-db-security-group-response"></a>
#### 응답

| 이름                | 종류   | 형식   | 설명            |
|-------------------|------|------|---------------|
| dbSecurityGroupId | Body | UUID | DB 보안 그룹의 식별자 |

---

<a id="modify-db-security-group"></a>
### DB 보안 그룹 수정하기 { #modify-db-security-group }

```http
PUT /v4.0/db-security-groups/{dbSecurityGroupId}
```

<a id="modify-db-security-group-required-permissions"></a>
#### 필요 권한

| 권한명                                                | 설명            |
|----------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbSecurityGroup.Modify | DB 보안 그룹 수정하기 |

<a id="modify-db-security-group-request"></a>
#### 요청

| 이름                  | 종류   | 형식     | 필수 | 설명                    |
|---------------------|------|--------|----|-----------------------|
| dbSecurityGroupId   | URL  | UUID   | O  | DB 보안 그룹의 식별자         |
| dbSecurityGroupName | Body | String | X  | DB 보안 그룹을 식별할 수 있는 이름 |
| description         | Body | String | X  | DB 보안 그룹에 대한 추가 정보    |

<details><summary>예시</summary>
<p>

```json
{
    "dbSecurityGroupName": "dbSecurityGroup",
    "description": "description"
}
```

</p>
</details>

<a id="modify-db-security-group-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>


---

<a id="delete-db-security-group"></a>
### DB 보안 그룹 삭제하기 { #delete-db-security-group }

```http
DELETE /v4.0/db-security-groups/{dbSecurityGroupId}
```

<a id="delete-db-security-group-required-permissions"></a>
#### 필요 권한

| 권한명                                                | 설명            |
|----------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:DbSecurityGroup.Delete | DB 보안 그룹 삭제하기 |

<a id="delete-db-security-group-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름                | 종류  | 형식   | 필수 | 설명            |
|-------------------|-----|------|----|---------------|
| dbSecurityGroupId | URL | UUID | O  | DB 보안 그룹의 식별자 |

<a id="delete-db-security-group-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="create-db-security-group-rule"></a>
### DB 보안 그룹 규칙 생성하기 { #create-db-security-group-rule }

```http
POST /v4.0/db-security-groups/{dbSecurityGroupId}/rules
```

<a id="create-db-security-group-rule-required-permissions"></a>
#### 필요 권한

| 권한명                                                    | 설명               |
|--------------------------------------------------------|------------------|
| RDSfor{{engine.pascalCase}}:DbSecurityGroupRule.Create | DB 보안 그룹 규칙 생성하기 |

<a id="create-db-security-group-rule-request"></a>
#### 요청

| 이름                | 종류   | 형식     | 필수 | 설명                                                                                                                                                                                       |
|-------------------|------|--------|----|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dbSecurityGroupId | URL  | UUID   | O  | DB 보안 그룹의 식별자                                                                                                                                                                            |
| description       | Body | String | X  | DB 보안 그룹 규칙에 대한 추가 정보                                                                                                                                                                    |
| direction         | Body | Enum   | O  | 통신 방향<br/>- `INGRESS`: 수신<br/>- `EGRESS`: 송신                                                                                                                                             |
| etherType         | Body | Enum   | O  | Ether 타입<br/>- `IPV4`: IPv4<br/>- `IPV6`: IPv6                                                                                                                                           |
| port              | Body | Object | O  | 포트 객체                                                                                                                                                                                    |
| port.portType     | Body | Enum   | O  | 포트 타입<br/>- `DB_PORT`: 각 DB 인스턴스 포트값으로 설정됩니다. `minPort`값과 `maxPort`값이 필요하지 않습니다.<br/>- `PORT`: 지정된 포트값으로 설정됩니다. `minPort`값과 `maxPort`값이 같아야 합니다.<br/>- `PORT_RANGE`: 지정된 포트 범위로 설정됩니다. |
| port.minPort      | Body | Number | X  | 최소 포트 범위<br/>- 최솟값: 1                                                                                                                                                                    |
| port.maxPort      | Body | Number | X  | 최대 포트 범위<br/>- 최댓값: 65535                                                                                                                                                                |
| cidr              | Body | String | O  | 허용할 트래픽의 원격 소스<br/>- 예시: `1.1.1.1/32`                                                                                                                                                    |

> [주의]
> DB 포트는 송신 방향으로 설정할 수 없습니다.

<details><summary>예시</summary>
<p>

```json
{
    "direction": "INGRESS",
    "etherType": "IPV4",
    "port": {
        "portType": "PORT",
        "minPort": 10000,
        "maxPort": 10000
    },
    "cidr": "0.0.0.0/0"
}
```

</p>
</details>

<a id="create-db-security-group-rule-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="modify-db-security-group-rule"></a>
### DB 보안 그룹 규칙 수정하기 { #modify-db-security-group-rule }

```http
PUT /v4.0/db-security-groups/{dbSecurityGroupId}/rules/{ruleId}
```

<a id="modify-db-security-group-rule-required-permissions"></a>
#### 필요 권한

| 권한명                                                    | 설명               |
|--------------------------------------------------------|------------------|
| RDSfor{{engine.pascalCase}}:DbSecurityGroupRule.Modify | DB 보안 그룹 규칙 수정하기 |

<a id="modify-db-security-group-rule-request"></a>
#### 요청

| 이름                | 종류   | 형식     | 필수 | 설명                                                                                                                                                                                       |
|-------------------|------|--------|----|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dbSecurityGroupId | URL  | UUID   | O  | DB 보안 그룹의 식별자                                                                                                                                                                            |
| ruleId            | URL  | UUID   | O  | DB 보안 그룹 규칙의 식별자                                                                                                                                                                         |
| description       | Body | String | X  | DB 보안 그룹 규칙에 대한 추가 정보                                                                                                                                                                    |
| direction         | Body | Enum   | O  | 통신 방향<br/>- `INGRESS`: 수신<br/>- `EGRESS`: 송신                                                                                                                                             |
| etherType         | Body | Enum   | O  | Ether 타입<br/>- `IPV4`: IPv4<br/>- `IPV6`: IPv6                                                                                                                                           |
| port              | Body | Object | O  | 포트 객체                                                                                                                                                                                    |
| port.portType     | Body | Enum   | O  | 포트 타입<br/>- `DB_PORT`: 각 DB 인스턴스 포트값으로 설정됩니다. `minPort`값과 `maxPort`값이 필요하지 않습니다.<br/>- `PORT`: 지정된 포트값으로 설정됩니다. `minPort`값과 `maxPort`값이 같아야 합니다.<br/>- `PORT_RANGE`: 지정된 포트 범위로 설정됩니다. |
| port.minPort      | Body | Number | X  | 최소 포트 범위<br/>- 최솟값: 1                                                                                                                                                                    |
| port.maxPort      | Body | Number | X  | 최대 포트 범위<br/>- 최댓값: 65535                                                                                                                                                                |
| cidr              | Body | String | O  | 허용할 트래픽의 원격 소스<br/>- 예시: `1.1.1.1/32`                                                                                                                                                    |

> [주의]
> DB 포트는 송신 방향으로 설정할 수 없습니다.

<details><summary>예시</summary>
<p>

```json
{
    "direction": "INGRESS",
    "etherType": "IPV4",
    "port": {
        "portType": "DB_PORT"
    },
    "cidr": "0.0.0.0/0"
}
```

</p>
</details>

<a id="modify-db-security-group-rule-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="delete-db-security-group-rule"></a>
### DB 보안 그룹 규칙 삭제하기 { #delete-db-security-group-rule }

```http
DELETE /v4.0/db-security-groups/{dbSecurityGroupId}/rules
```

<a id="delete-db-security-group-rule-required-permissions"></a>
#### 필요 권한

| 권한명                                                    | 설명               |
|--------------------------------------------------------|------------------|
| RDSfor{{engine.pascalCase}}:DbSecurityGroupRule.Create | DB 보안 그룹 규칙 삭제하기 |

<a id="delete-db-security-group-rule-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름                | 종류    | 형식    | 필수 | 설명                  |
|-------------------|-------|-------|----|---------------------|
| dbSecurityGroupId | URL   | UUID  | O  | DB 보안 그룹의 식별자       |
| ruleIds           | Query | Array | O  | DB 보안 그룹 규칙의 식별자 목록 |

<a id="delete-db-security-group-rule-response"></a>
#### 응답

| 이름    | 종류   | 형식   | 설명          |
|-------|------|------|-------------|
| jobId | Body | UUID | 요청한 작업의 식별자 |

---

<a id="parameter-group"></a>
## 파라미터 그룹 { #parameter-group }

<a id="list-parameter-groups"></a>
### 파라미터 그룹 목록 보기 { #list-parameter-groups }

```http
GET /v4.0/parameter-groups
```

<a id="list-parameter-groups-required-permissions"></a>
#### 필요 권한

| 권한명                                             | 설명            |
|-------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:ParameterGroup.List | 파라미터 그룹 목록 보기 |

<a id="list-parameter-groups-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름        | 종류    | 형식   | 필수 | 설명       |
|-----------|-------|------|----|----------|
| dbVersion | Query | Enum | X  | DB 엔진 유형 |

<a id="list-parameter-groups-response"></a>
#### 응답

| 이름                                   | 종류   | 형식       | 설명                                                                |
|--------------------------------------|------|----------|-------------------------------------------------------------------|
| parameterGroups                      | Body | Array    | 파라미터 그룹 목록                                                        |
| parameterGroups.parameterGroupId     | Body | UUID     | 파라미터 그룹의 식별자                                                      |
| parameterGroups.parameterGroupName   | Body | String   | 파라미터 그룹을 식별할 수 있는 이름                                              |
| parameterGroups.description          | Body | String   | 파라미터 그룹에 대한 추가 정보                                                 |
| parameterGroups.dbVersion            | Body | Enum     | DB 엔진 유형                                                          |
| parameterGroups.parameterGroupStatus | Body | Enum     | 파라미터 그룹의 현재 상태<br/>- `STABLE`: 적용 완료<br/>- `NEED_TO_APPLY`: 적용 필요 |
| parameterGroups.createdYmdt          | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                 |
| parameterGroups.updatedYmdt          | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                 |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "parameterGroups": [
        {
            "parameterGroupId": "404e8a89-ca4d-4fca-96c2-1518754d50b7",
            "parameterGroupName": "parameter-group",
            "description": null,
            "dbVersion": "{{engine.sampleDbVersionCode}}",
            "parameterGroupStatus": "STABLE",
            "createdYmdt": "2023-02-31T15:28:17+09:00",
            "updatedYmdt": "2023-02-31T15:28:17+09:00"
        }
    ]
}
```

</p>
</details>


---

<a id="list-parameter-group-details"></a>
### 파라미터 그룹 상세 보기 { #list-parameter-group-details }

```http
GET /v4.0/parameter-groups/{parameterGroupId}
```

<a id="list-parameter-group-details-required-permissions"></a>
#### 필요 권한

| 권한명                                            | 설명            |
|------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:ParameterGroup.Get | 파라미터 그룹 상세 보기 |

<a id="list-parameter-group-details-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름               | 종류  | 형식   | 필수 | 설명           |
|------------------|-----|------|----|--------------|
| parameterGroupId | URL | UUID | O  | 파라미터 그룹의 식별자 |

<a id="list-parameter-group-details-response"></a>
#### 응답

| 이름                            | 종류   | 형식       | 설명                                                                                                     |
|-------------------------------|------|----------|--------------------------------------------------------------------------------------------------------|
| parameterGroupId              | Body | UUID     | 파라미터 그룹의 식별자                                                                                           |
| parameterGroupName            | Body | String   | 파라미터 그룹을 식별할 수 있는 이름                                                                                   |
| description                   | Body | String   | 파라미터 그룹에 대한 추가 정보                                                                                      |
| dbVersion                     | Body | Enum     | DB 엔진 유형                                                                                               |
| parameterGroupStatus          | Body | Enum     | 파라미터 그룹의 현재 상태<br/>- `STABLE`: 적용 완료<br/>- `NEED_TO_APPLY`: 적용 필요                                      |
| parameters                    | Body | Array    | 파라미터 목록                                                                                                |
| parameters.parameterId        | Body | UUID     | 파라미터 식별자                                                                                               |
| parameters.parameterFileGroup | Body | Enum     | 파라미터 파일 그룹 타입<br/>- `CLIENT`: client<br/>- `MYSQL`: mysql<br/>- `MYSQLD`: mysqld                       |
| parameters.parameterName      | Body | String   | 파라미터 이름                                                                                                |
| parameters.fileParameterName  | Body | String   | 파라미터 파일명                                                                                             |
| parameters.value              | Body | String   | 현재 설정된 값                                                                                               |
| parameters.defaultValue       | Body | String   | 기본값                                                                                                    |
| parameters.allowedValue       | Body | String   | 허용된 값                                                                                                  |
| parameters.updateType         | Body | Enum     | 수정 타입<br/>- `VARIABLE`: 언제든 수정 가능<br/>- `CONSTANT`: 수정 불가능<br/>- `INIT_VARIABLE`: DB 인스턴스 생성 시에만 수정 가능 |
| parameters.applyType          | Body | Enum     | 적용 타입<br/>- `SESSION`: 세션 적용<br/>- `FILE`: 설정 파일 적용(재시작 필요)<br/>- `BOTH`: 전체(재시작 필요)                   |
| createdYmdt                   | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                      |
| updatedYmdt                   | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                      |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "parameterGroupId": "404e8a89-ca4d-4fca-96c2-1518754d50b7",
    "parameterGroupName": "parameter-group",
    "description": null,
    "dbVersion": "{{engine.sampleDbVersionCode}}",
    "parameterGroupStatus": "STABLE",
    "parameters": [
        {
            "parameterId": "fa040b5e-f29f-46de-8f0d-bba4cb82887a",
            "parameterFileGroup": "client",
            "parameterName": "socket",
            "fileParameterName": "socket",
            "value": "/home/tcrds/db/mysql/tmp/mysql.sock",
            "defaultValue": "/home/tcrds/db/mysql/tmp/mysql.sock",
            "allowedValue": "",
            "updateType": "CONSTANT",
            "applyType": "BOTH"
        }
    ],
    "createdYmdt": "2023-03-13T11:02:28+09:00",
    "updatedYmdt": "2023-03-13T11:02:28+09:00"
}
```

</p>
</details>


---

<a id="create-parameter-group"></a>
### 파라미터 그룹 생성하기 { #create-parameter-group }

```http
POST /v4.0/parameter-groups
```

<a id="create-parameter-group-required-permissions"></a>
#### 필요 권한

| 권한명                                               | 설명           |
|---------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:ParameterGroup.Create | 파라미터 그룹 생성하기 |

<a id="create-parameter-group-request"></a>
#### 요청

| 이름                 | 종류   | 형식     | 필수 | 설명                   |
|--------------------|------|--------|----|----------------------|
| parameterGroupName | Body | String | O  | 파라미터 그룹을 식별할 수 있는 이름 |
| description        | Body | String | X  | 파라미터 그룹에 대한 추가 정보    |
| dbVersion          | Body | Enum   | O  | DB 엔진 유형             |

<details><summary>예시</summary>
<p>

```json
{
    "parameterGroupName": "parameter-group",
    "dbVersion": "{{engine.sampleDbVersionCode}}"
}
```

</p>
</details>

<a id="create-parameter-group-response"></a>
#### 응답

| 이름               | 종류   | 형식   | 설명           |
|------------------|------|------|--------------|
| parameterGroupId | Body | UUID | 파라미터 그룹의 식별자 |

---

<a id="copy-parameter-group"></a>
### 파라미터 그룹 복사하기 { #copy-parameter-group }

```http
POST /v4.0/parameter-groups/{parameterGroupId}/copy
```

<a id="copy-parameter-group-required-permissions"></a>
#### 필요 권한

| 권한명                                             | 설명           |
|-------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:ParameterGroup.Copy | 파라미터 그룹 복사하기 |

<a id="copy-parameter-group-request"></a>
#### 요청

| 이름                 | 종류   | 형식     | 필수 | 설명                   |
|--------------------|------|--------|----|----------------------|
| parameterGroupId   | URL  | UUID   | O  | 파라미터 그룹의 식별자         |
| parameterGroupName | Body | String | O  | 파라미터 그룹을 식별할 수 있는 이름 |
| description        | Body | String | X  | 파라미터 그룹에 대한 추가 정보    |

<details><summary>예시</summary>
<p>

```json
{
    "parameterGroupName": "parameter-group-copy",
    "description": "copy"
}
```

</p>
</details>

<a id="copy-parameter-group-response"></a>
#### 응답

| 이름               | 종류   | 형식   | 설명           |
|------------------|------|------|--------------|
| parameterGroupId | Body | UUID | 파라미터 그룹의 식별자 |

---

<a id="modify-parameter-group"></a>
### 파라미터 그룹 수정하기 { #modify-parameter-group }

```http
PUT /v4.0/parameter-groups/{parameterGroupId}
```

<a id="modify-parameter-group-required-permissions"></a>
#### 필요 권한

| 권한명                                               | 설명           |
|---------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:ParameterGroup.Modify | 파라미터 그룹 수정하기 |

<a id="modify-parameter-group-request"></a>
#### 요청

| 이름                 | 종류   | 형식     | 필수 | 설명                   |
|--------------------|------|--------|----|----------------------|
| parameterGroupId   | URL  | UUID   | O  | 파라미터 그룹의 식별자         |
| parameterGroupName | Body | String | X  | 파라미터 그룹을 식별할 수 있는 이름 |
| description        | Body | String | X  | 파라미터 그룹에 대한 추가 정보    |

<details><summary>예시</summary>
<p>

```json
{
    "parameterGroupName": "parameter-group"
}
```

</p>
</details>

<a id="modify-parameter-group-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="modify-parameter"></a>
### 파라미터 수정하기 { #modify-parameter }

```http
PUT /v4.0/parameter-groups/{parameterGroupId}/parameters
```

<a id="modify-parameter-required-permissions"></a>
#### 필요 권한

| 권한명                                               | 설명           |
|---------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:ParameterGroup.Modify | 파라미터 그룹 수정하기 |

<a id="modify-parameter-request"></a>
#### 요청

| 이름                             | 종류   | 형식     | 필수 | 설명           |
|--------------------------------|------|--------|----|--------------|
| parameterGroupId               | URL  | UUID   | O  | 파라미터 그룹의 식별자 |
| modifiedParameters             | Body | Array  | O  | 변경할 파라미터 목록  |
| modifiedParameters.parameterId | Body | UUID   | O  | 파라미터의 식별자    |
| modifiedParameters.value       | Body | String | O  | 변경할 파라미터 값   |

<details><summary>예시</summary>
<p>

```json
{
    "modifiedParameters": [
        {
            "parameterId": "3abac558-7274-44e1-9f4a-f100f53f67ba",
            "value": "0"
        }
    ]
}
```

</p>
</details>

<a id="modify-parameter-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="reset-parameter-group"></a>
### 파라미터 그룹 재설정하기 { #reset-parameter-group }

```http
PUT /v4.0/parameter-groups/{parameterGroupId}/reset
```

<a id="reset-parameter-group-required-permissions"></a>
#### 필요 권한

| 권한명                                              | 설명            |
|--------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:ParameterGroup.Reset | 파라미터 그룹 재설정하기 |

<a id="reset-parameter-group-request"></a>
#### 요청

| 이름               | 종류  | 형식   | 필수 | 설명           |
|------------------|-----|------|----|--------------|
| parameterGroupId | URL | UUID | O  | 파라미터 그룹의 식별자 |

<a id="reset-parameter-group-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="delete-parameter-group"></a>
### 파라미터 그룹 삭제하기 { #delete-parameter-group }

```http
DELETE /v4.0/parameter-groups/{parameterGroupId}
```

<a id="delete-parameter-group-required-permissions"></a>
#### 필요 권한

| 권한명                                               | 설명           |
|---------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:ParameterGroup.Delete | 파라미터 그룹 삭제하기 |

<a id="delete-parameter-group-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름               | 종류  | 형식   | 필수 | 설명           |
|------------------|-----|------|----|--------------|
| parameterGroupId | URL | UUID | O  | 파라미터 그룹의 식별자 |

<a id="delete-parameter-group-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="user-group"></a>
## 사용자 그룹 { #user-group }

<a id="list-user-groups"></a>
### 사용자 그룹 목록 보기 { #list-user-groups }

```http
GET /v4.0/user-groups
```

<a id="list-user-groups-required-permissions"></a>
#### 필요 권한

| 권한명                                        | 설명           |
|--------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:UserGroup.List | 사용자 그룹 목록 보기 |

<a id="list-user-groups-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-user-groups-response"></a>
#### 응답

| 이름                       | 종류   | 형식       | 설명                                |
|--------------------------|------|----------|-----------------------------------|
| userGroups               | Body | Array    | 사용자 그룹 목록                         |
| userGroups.userGroupId   | Body | UUID     | 사용자 그룹의 식별자                       |
| userGroups.userGroupName | Body | String   | 사용자 그룹을 식별할 수 있는 이름               |
| userGroups.createdYmdt   | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| userGroups.updatedYmdt   | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "userGroups": [
        {
            "userGroupId": "1aac0437-f32d-4923-ad3c-ac61c1cfdfe0",
            "userGroupName": "dev-team",
            "createdYmdt": "2023-02-23T10:07:54+09:00",
            "updatedYmdt": "2023-02-26T01:15:50+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="list-user-group-details"></a>
### 사용자 그룹 상세 보기 { #list-user-group-details }

```http
GET /v4.0/user-groups/{userGroupId}
```

<a id="list-user-group-details-required-permissions"></a>
#### 필요 권한

| 권한명                                       | 설명           |
|-------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:UserGroup.Get | 사용자 그룹 상세 보기 |

<a id="list-user-group-details-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름          | 종류  | 형식   | 필수 | 설명          |
|-------------|-----|------|----|-------------|
| userGroupId | URL | UUID | O  | 사용자 그룹의 식별자 |

<a id="list-user-group-details-response"></a>
#### 응답

| 이름                | 종류   | 형식       | 설명                                                                                                        |
|-------------------|------|----------|-----------------------------------------------------------------------------------------------------------|
| userGroupId       | Body | UUID     | 사용자 그룹의 식별자                                                                                               |
| userGroupName     | Body | String   | 사용자 그룹을 식별할 수 있는 이름                                                                                       |
| userGroupTypeCode | Body | Enum     | 사용자 그룹 종류    <br /> `ENTIRE`: 프로젝트 멤버 전체를 포함하는 사용자 그룹 <br /> `INDIVIDUAL_MEMBER`: 특정 프로젝트 멤버를 포함하는 사용자 그룹 |
| members           | Body | Array    | 프로젝트 멤버 목록                                                                                                |
| members.memberId  | Body | UUID     | 프로젝트 멤버의 식별자                                                                                              |
| createdYmdt       | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                         |
| updatedYmdt       | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                         |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "userGroupId": "1aac0437-f32d-4923-ad3c-ac61c1cfdfe0",
    "userGroupName": "dev-team",
	"userGroupTypeCode": "INDIVIDUAL_MEMBER",
    "members": [
        {
            "memberId": "1321e759-2ef3-4b85-9921-b13e918b24b5"
        }
    ],
    "createdYmdt": "2023-02-23T10:07:54+09:00",
    "updatedYmdt": "2023-02-26T01:15:50+09:00"
}
```

</p>
</details>

---

<a id="create-user-group"></a>
### 사용자 그룹 생성하기 { #create-user-group }

```http
POST /v4.0/user-groups
```

<a id="create-user-group-required-permissions"></a>
#### 필요 권한

| 권한명                                          | 설명          |
|----------------------------------------------|-------------|
| RDSfor{{engine.pascalCase}}:UserGroup.Create | 사용자 그룹 생성하기 |

<a id="create-user-group-request"></a>
#### 요청

| 이름            | 종류   | 형식      | 필수 | 설명                                                        |
|---------------|------|---------|----|-----------------------------------------------------------|
| userGroupName | Body | String  | O  | 사용자 그룹을 식별할 수 있는 이름                                       |
| memberIds     | Body | Array   | O  | 프로젝트 멤버의 식별자 목록 <br /> `selectAll`이 true인 경우 해당 필드 값은 무시됩니다 |
| selectAll     | Body | Boolean | X  | 프로젝트 멤버 전체 여부 <br /> true인 경우 해당 그룹은 전체 멤버를 대상으로 설정됩니다        |

<details><summary>예시</summary>
<p>

```json
{
    "userGroupName": "dev-team",
    "memberIds": [
        "1321e759-2ef3-4b85-9921-b13e918b24b5"
    ]
}
```

```json
{
    "userGroupName": "dev-team",
    "selectAll": true
}
```

</p>
</details>

<a id="create-user-group-response"></a>
#### 응답

| 이름          | 종류   | 형식   | 설명          |
|-------------|------|------|-------------|
| userGroupId | Body | UUID | 사용자 그룹의 식별자 |

---

<a id="modify-user-group"></a>
### 사용자 그룹 수정하기 { #modify-user-group }

```http
PUT /v4.0/user-groups/{userGroupId}
```

<a id="modify-user-group-required-permissions"></a>
#### 필요 권한

| 권한명                                          | 설명          |
|----------------------------------------------|-------------|
| RDSfor{{engine.pascalCase}}:UserGroup.Modify | 사용자 그룹 수정하기 |

<a id="modify-user-group-request"></a>
#### 요청

| 이름            | 종류   | 형식      | 필수 | 설명                                                 |
|---------------|------|---------|----|----------------------------------------------------|
| userGroupId   | URL  | UUID    | O  | 사용자 그룹의 식별자                                        |
| userGroupName | Body | String  | X  | 사용자 그룹을 식별할 수 있는 이름                                |
| memberIds     | Body | Array   | X  | 프로젝트 멤버의 식별자 목록                                    |
| selectAll     | Body | Boolean | X  | 프로젝트 멤버 전체 여부 <br /> true인 경우 해당 그룹은 전체 멤버를 대상으로 설정됩니다 |

<details><summary>예시</summary>
<p>

```json
{
    "userGroupName": "dev-team",
    "memberIds": [
        "1321e759-2ef3-4b85-9921-b13e918b24b5",
        "f9064b09-2b15-442e-a4b0-3a5a2754555e"
    ]
}
```

</p>
</details>

<a id="modify-user-group-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="delete-user-group"></a>
### 사용자 그룹 삭제하기 { #delete-user-group }

```http
DELETE /v4.0/user-groups/{userGroupId}
```

<a id="delete-user-group-required-permissions"></a>
#### 필요 권한

| 권한명                                          | 설명          |
|----------------------------------------------|-------------|
| RDSfor{{engine.pascalCase}}:UserGroup.Delete | 사용자 그룹 삭제하기 |

<a id="delete-user-group-request"></a>
#### 요청

| 이름          | 종류  | 형식   | 필수 | 설명          |
|-------------|-----|------|----|-------------|
| userGroupId | URL | UUID | O  | 사용자 그룹의 식별자 |

<a id="delete-user-group-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="notification-group"></a>
## 알림 그룹 { #notification-group }

<a id="list-notification-groups"></a>
### 알림 그룹 목록 보기 { #list-notification-groups }

```http
GET /v4.0/notification-groups
```

<a id="list-notification-groups-required-permissions"></a>
#### 필요 권한

| 권한명                                                | 설명          |
|----------------------------------------------------|-------------|
| RDSfor{{engine.pascalCase}}:NotificationGroup.List | 알림 그룹 목록 보기 |

<a id="list-notification-groups-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-notification-groups-response"></a>
#### 응답

| 이름                                       | 종류   | 형식       | 설명                                |
|------------------------------------------|------|----------|-----------------------------------|
| notificationGroups                       | Body | Array    | 알림 그룹 목록                          |
| notificationGroups.notificationGroupId   | Body | UUID     | 알림 그룹의 식별자                        |
| notificationGroups.notificationGroupName | Body | String   | 알림 그룹을 식별할 수 있는 이름                |
| notificationGroups.notifyEmail           | Body | Boolean  | 이메일 알림 여부                         |
| notificationGroups.notifySms             | Body | Boolean  | SMS 알림 여부                         |
| notificationGroups.isEnabled             | Body | Boolean  | 활성화 여부                            |
| notificationGroups.createdYmdt           | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| notificationGroups.updatedYmdt           | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "notificationGroups": [
        {
            "notificationGroupId": "b3901f17-9971-4d1e-8a81-8448cf533dc7",
            "notificationGroupName": "dev-team-noti",
            "notifyEmail": true,
            "notifySms": false,
            "isEnabled": true,
            "createdYmdt": "2023-02-20T13:34:13+09:00",
            "updatedYmdt": "2023-02-20T13:34:13+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="view-notification-group-details"></a>
### 알림 그룹 상세 보기 { #view-notification-group-details }

```http
GET /v4.0/notification-groups/{notificationGroupId}
```

<a id="view-notification-group-details-required-permissions"></a>
#### 필요 권한

| 권한명                                               | 설명          |
|---------------------------------------------------|-------------|
| RDSfor{{engine.pascalCase}}:NotificationGroup.Get | 알림 그룹 상세 보기 |

<a id="view-notification-group-details-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름                  | 종류  | 형식   | 필수 | 설명         |
|---------------------|-----|------|----|------------|
| notificationGroupId | URL | UUID | O  | 알림 그룹의 식별자 |

<a id="view-notification-group-details-response"></a>
#### 응답

| 이름                         | 종류   | 형식       | 설명                                |
|----------------------------|------|----------|-----------------------------------|
| notificationGroupId        | Body | UUID     | 알림 그룹의 식별자                        |
| notificationGroupName      | Body | String   | 알림 그룹을 식별할 수 있는 이름                |
| notifyEmail                | Body | Boolean  | 이메일 알림 여부                         |
| notifySms                  | Body | Boolean  | SMS 알림 여부                         |
| isEnabled                  | Body | Boolean  | 활성화 여부                            |
| dbInstances                | Body | Array    | 감시 대상 DB 인스턴스 목록                  |
| dbInstances.dbInstanceId   | Body | UUID     | DB 인스턴스의 식별자                      |
| dbInstances.dbInstanceName | Body | String   | DB 인스턴스를 식별할 수 있는 이름              |
| userGroups                 | Body | Array    | 사용자 그룹 목록                         |
| userGroups.userGroupId     | Body | UUID     | 사용자 그룹의 식별자                       |
| userGroups.userGroupName   | Body | String   | 사용자 그룹을 식별할 수 있는 이름               |
| createdYmdt                | Body | DateTime | 생성 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| updatedYmdt                | Body | DateTime | 수정 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "notificationGroupId": "b3901f17-9971-4d1e-8a81-8448cf533dc7",
    "notificationGroupName": "dev-team-noti",
    "notifyEmail": true,
    "notifySms": false,
    "isEnabled": true,
    "dbInstances": [
        {
            "dbInstanceId": "ed5cb985-526f-4c54-9ae0-40288593de65",
            "dbInstanceName": "database"
        }
    ],
    "userGroups": [
        {
            "userGroupId": "1aac0437-f32d-4923-ad3c-ac61c1cfdfe0",
            "userGroupName": "dev-team"
        }
    ],
    "createdYmdt": "2023-02-20T13:34:13+09:00",
    "updatedYmdt": "2023-02-20T13:34:13+09:00"
}
```

</p>
</details>

---

<a id="create-notification-group"></a>
### 알림 그룹 생성하기 { #create-notification-group }

```http
POST /v4.0/notification-groups
```

<a id="create-notification-group-required-permissions"></a>
#### 필요 권한

| 권한명                                                  | 설명         |
|------------------------------------------------------|------------|
| RDSfor{{engine.pascalCase}}:NotificationGroup.Create | 알림 그룹 생성하기 |

<a id="create-notification-group-request"></a>
#### 요청

| 이름                    | 종류   | 형식      | 필수 | 설명                          |
|-----------------------|------|---------|----|-----------------------------|
| notificationGroupName | Body | String  | O  | 알림 그룹을 식별할 수 있는 이름          |
| notifyEmail           | Body | Boolean | X  | 이메일 알림 여부<br/>- 기본값: `true` |
| notifySms             | Body | Boolean | X  | SMS 알림 여부<br/>- 기본값: `true` |
| isEnabled             | Body | Boolean | X  | 활성화 여부<br/>- 기본값: `true`    |
| dbInstanceIds         | Body | Array   | O  | 감시 대상 DB 인스턴스의 식별자 목록       |
| userGroupIds          | Body | Array   | O  | 사용자 그룹의 식별자 목록              |

<details><summary>예시</summary>
<p>

```json
{
    "notificationGroupName": "dev-team-noti",
    "notifyEmail": false,
    "isEnable": true,
    "dbInstanceIds": [
        "ed5cb985-526f-4c54-9ae0-40288593de65"
    ],
    "userGroupIds": [
        "1aac0437-f32d-4923-ad3c-ac61c1cfdfe0"
    ]
}
```

</p>
</details>

<a id="create-notification-group-response"></a>
#### 응답

| 이름                  | 종류   | 형식   | 설명         |
|---------------------|------|------|------------|
| notificationGroupId | Body | UUID | 알림 그룹의 식별자 |

---

<a id="modify-notification-group"></a>
### 알림 그룹 수정하기 { #modify-notification-group }

```http
PUT /v4.0/notification-groups/{notificationGroupId}
```

<a id="modify-notification-group-required-permissions"></a>
#### 필요 권한

| 권한명                                                  | 설명         |
|------------------------------------------------------|------------|
| RDSfor{{engine.pascalCase}}:NotificationGroup.Modify | 알림 그룹 수정하기 |

<a id="modify-notification-group-request"></a>
#### 요청

| 이름                    | 종류   | 형식      | 필수 | 설명                    |
|-----------------------|------|---------|----|-----------------------|
| notificationGroupId   | URL  | UUID    | O  | 알림 그룹의 식별자            |
| notificationGroupName | Body | String  | X  | 알림 그룹을 식별할 수 있는 이름    |
| notifyEmail           | Body | Boolean | X  | 이메일 알림 여부             |
| notifySms             | Body | Boolean | X  | SMS 알림 여부             |
| isEnabled             | Body | Boolean | X  | 활성화 여부                |
| dbInstanceIds         | Body | Array   | X  | 감시 대상 DB 인스턴스의 식별자 목록 |
| userGroupIds          | Body | Array   | X  | 사용자 그룹의 식별자 목록        |

<details><summary>예시</summary>
<p>

```json
{
    "notifyEmail": true,
    "dbInstanceIds": [
        "ed5cb985-526f-4c54-9ae0-40288593de65",
        "d51b7da0-682f-47ff-b588-b739f6adc740"
    ]
}
```

</p>
</details>

<a id="modify-notification-group-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="delete-notification-group"></a>
### 알림 그룹 삭제하기 { #delete-notification-group }

```http
DELETE /v4.0/notification-groups/{notificationGroupId}
```

<a id="delete-notification-group-required-permissions"></a>
#### 필요 권한

| 권한명                                                  | 설명         |
|------------------------------------------------------|------------|
| RDSfor{{engine.pascalCase}}:NotificationGroup.Delete | 알림 그룹 삭제하기 |

<a id="delete-notification-group-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름                  | 종류  | 형식   | 필수 | 설명         |
|---------------------|-----|------|----|------------|
| notificationGroupId | URL | UUID | O  | 알림 그룹의 식별자 |

<a id="delete-notification-group-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="monitoring"></a>
## 모니터링 { #monitoring }

<a id="list-metric-list"></a>
### Metric 목록 보기 { #list-metric-list }

```http
GET /v4.0/metrics
```

<a id="list-metric-list-required-permissions"></a>
#### 필요 권한

| 권한명                                     | 설명       |
|-----------------------------------------|----------|
| RDSfor{{engine.pascalCase}}:Metric.List | 통계 정보 조회 |

<a id="list-metric-list-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-metric-list-response"></a>
#### 응답

| 이름                  | 종류   | 형식     | 설명        |
|---------------------|------|--------|-----------|
| metrics             | Body | Array  | Metric 목록 |
| metrics.measureName | Body | Enum   | 조회 지표 유형  |
| metrics.unit        | Body | String | 측정값 단위    |

<details><summary>예시</summary>
<p>

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

</p>
</details>

---

<a id="view-stats"></a>
### 통계 정보 조회 { #view-stats }

```http
GET /v4.0/metric-statistics
```

<a id="view-stats-required-permissions"></a>
#### 필요 권한

| 권한명                                     | 설명       |
|-----------------------------------------|----------|
| RDSfor{{engine.pascalCase}}:Metric.List | 통계 정보 조회 |

<a id="view-stats-request"></a>
#### 요청

| 이름           | 종류    | 형식       | 필수 | 설명                                |
|--------------|-------|----------|----|-----------------------------------|
| dbInstanceId | Query | UUID     | O  | DB 인스턴스의 식별자                      |
| measureNames | Query | Array    | O  | 조회 지표 목록<br/>- 최소 크기: `1`         |
| from         | Query | Datetime | O  | 시작 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| to           | Query | Datetime | O  | 종료 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |
| interval     | Query | Number   | X  | 조회 간격                             |

<a id="view-stats-response"></a>
#### 응답

| 이름                                | 종류   | 형식        | 설명       |
|-----------------------------------|------|-----------|----------|
| metricStatistics                  | Body | Array     | 통계 정보 목록 |
| metricStatistics.measureName      | Body | Enum      | 측정 항목 유형 |
| metricStatistics.unit             | Body | String    | 측정값 단위   |
| metricStatistics.values           | Body | Array     | 측정값 목록   |
| metricStatistics.values.timestamp | Body | Timestamp | 측정 시간    |
| metricStatistics.values.value     | Body | Object    | 측정값      |

<details><summary>예시</summary>
<p>

```json
{
    "metricStatistics": [
        {
            "measureName": "MYSQL_STATUS",
            "unit": "",
            "values": [
                [
                    1679298540,
                    "1"
                ],
                [
                    1679298600,
                    "1"
                ],
                [
                    1679298660,
                    "1"
                ]
            ]
        }
    ]
}
```

</p>
</details>

---

<a id="event"></a>
## 이벤트 { #event }

<a id="event-category"></a>
### 이벤트 카테고리 { #event-category }

이벤트는 카테고리로 분류할 수 있으며 아래와 같습니다.

| 이벤트 카테고리    | 설명      |
|-------------|---------|
| ALL         | 전체      |
| BACKUP      | 백업      |
| DB_INSTANCE | DB 인스턴스 |
| JOB         | 작업      |
| TENANT      | 테넌트     |
| MONITORING  | 모니터링    |

<a id="list-events"></a>
### 이벤트 목록 조회 { #list-events }

```http
GET /v4.0/events
```

<a id="list-events-required-permissions"></a>
#### 필요 권한

| 권한명                                    | 설명        |
|----------------------------------------|-----------|
| RDSfor{{engine.pascalCase}}:Event.List | 이벤트 목록 보기 |

<a id="list-events-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름                | 종류    | 형식       | 필수 | 설명                                                                                                                                   |
|-------------------|-------|----------|----|--------------------------------------------------------------------------------------------------------------------------------------|
| page              | Query | Number   | X  | 조회할 목록의 페이지<br/>- 기본값: 1 <br/>- 최솟값: `1`                                                                                                           |
| size              | Query | Number   | X  | 조회할 목록의 페이지 크기<br/>- 기본값: 20                                        |
| from              | Query | Datetime | O  | 시작 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                                    |
| to                | Query | Datetime | O  | 종료 일시(YYYY-MM-DDThh:mm:ss.SSSTZD)                                                                                                    |
| eventCategoryType | Query | Enum     | O  | 조회할 이벤트 카테고리 유형<br/>- `ALL`: 전체<br/>- `INSTANCE`: DB 인스턴스<br/>- `BACKUP`: 백업<br/>- `DB_SECURITY_GROUP`: DB 보안 그룹<br/>- `TENANT`: 테넌트 |
| sourceId          | Query | String   | X  | 이벤트가 발생한 대상 리소스의 식별자                                                                                                                 |
| keyword           | Query | String   | X  | 이벤트 메시지에 포함된 문자열 검색어                                                                                                                 |
| ascendingOrder    | Query | Enum     | X  | 이벤트 메시지 정렬 순서<br/>- `ASC`: 오름차순<br/>- `DESC`: 내림차순<br/>- 기본값: `DESC`                                                                 |

<a id="list-events-response"></a>
#### 응답

| 이름                       | 종류   | 형식       | 설명                                    |
|--------------------------|------|----------|---------------------------------------|
| totalCounts              | Body | Number   | 전체 이벤트 목록 수                           |
| events                   | Body | Array    | 이벤트 목록                                |
| events.eventCategoryType | Body | Enum     | 이벤트 카테고리 유형                           |
| events.eventCode         | Body | Enum     | 발생한 이벤트의 유형                           |
| events.sourceId          | Body | String   | 이벤트 소스의 식별자                           |
| events.sourceName        | Body | String   | 이벤트 소스를 식별할 수 있는 이름                   |
| events.messages          | Body | Array    | 이벤트 메시지 목록                            |
| events.messages.langCode | Body | String   | 언어 코드                                 |
| events.messages.message  | Body | String   | 이벤트 메시지                               |
| events.eventYmdt         | Body | DateTime | 이벤트 발생 일시(YYYY-MM-DDThh:mm:ss.SSSTZD) |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "totalCounts": 28,
    "events": [
        {
            "eventCategoryType": "INSTANCE",
            "eventCode": "INSTC_02_01",
            "sourceId": "76f00947-356e-4a20-8922-428368cc45ed",
            "sourceName": "db-instance",
            "messages": [
                {
                    "langCode": "EN",
                    "message": "DB instance started"
                },
                {
                    "langCode": "JA",
                    "message": "DBインスタンスの起動"
                },
                {
                    "langCode": "KO",
                    "message": "DB 인스턴스 시작"
                },
                {
                    "langCode": "ZH",
                    "message": "DB instance started"
                }
            ],
            "eventYmdt": "2023-03-20T16:31:59+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="list-subscribable-event-codes"></a>
### 구독 가능한 이벤트 코드 목록 보기 { #list-subscribable-event-codes }

```http
GET /v4.0/event-codes
```

<a id="list-subscribable-event-codes-required-permissions"></a>
#### 필요 권한

| 권한명                                    | 설명        |
|----------------------------------------|-----------|
| RDSfor{{engine.pascalCase}}:Event.List | 이벤트 목록 보기 |

<a id="list-subscribable-event-codes-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

<a id="list-subscribable-event-codes-response"></a>
#### 응답

| 이름                           | 종류   | 형식    | 설명          |
|------------------------------|------|-------|-------------|
| eventCodes                   | Body | Array | 이벤트 코드 목록   |
| eventCodes.eventCode         | Body | Enum  | 이벤트 코드      |
| eventCodes.eventCategoryType | Body | Enum  | 이벤트 카테고리 유형 |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "eventCodes": [
        {
            "eventCode": "INSTC_05_01",
            "eventCategoryType": "INSTANCE"
        }
    ]
}
```

</p>
</details>

---

<a id="event-subscription"></a>
## 이벤트 구독 { #event-subscription }

<a id="list-event-subscriptions"></a>
### 이벤트 구독 목록 조회 { #list-event-subscriptions }

```http
GET /v4.0/event-subscriptions
```

<a id="list-event-subscriptions-required-permission"></a>
#### 필요 권한

| 권한명                                                    | 설명            |
|---------------------------------------------------------|---------------|
| RDSfor{{engine.pascalCase}}:EventSubscription.List | 이벤트 구독 목록 조회 |

<a id="list-event-subscriptions-request"></a>
#### 요청

| 이름                | 종류    | 형식       | 필수 | 설명                                       |
|-------------------|-------|----------|----|------------------------------------------|
| page              | Query | Number   | X  | 조회할 목록의 페이지<br/>- 기본값: 1 <br/>- 최솟값: `1` |
| size              | Query | Number   | X  | 조회할 목록의 페이지 크기<br/>- 기본값: 20             |
| eventSubscriptionId    | Query | UUID   | X  | 이벤트 구독의 식별자                              |
| eventSubscriptionName  | Query | String | X  | 이벤트 구독을 식별할 수 있는 이름                      |
| userGroupId            | Query | UUID   | X  | 사용자 그룹의 식별자                              |

<a id="list-event-subscriptions-response"></a>
#### 응답

| 이름                                            | 종류   | 형식       | 설명                       |
|-----------------------------------------------|------|----------|--------------------------|
| totalCounts                                   | Body | Number   | 전체 이벤트 구독 목록 수           |
| eventSubscriptions                            | Body | Array    | 이벤트 구독 목록                |
| eventSubscriptions.eventSubscriptionId        | Body | UUID     | 이벤트의 구독 식별자              |
| eventSubscriptions.eventCategoryType          | Body | Enum     | 이벤트 카테고리 유형              |
| eventSubscriptions.eventSubscriptionName      | Body | String   | 이벤트 구독을 식별할 수 있는 이름      |
| eventSubscriptions.enabled                    | Body | Boolean  | 활성화 여부                   |
| eventSubscriptions.notifyEmail                | Body | Boolean  | 이메일 발송 여부                |
| eventSubscriptions.notifySms                  | Body | Boolean  | SMS 발송 여부                |
| eventSubscriptions.eventCodes                 | Body | Array    | 구독할 이벤트 코드 목록            |
| eventSubscriptions.sources                    | Body | Array    | 구독할 이벤트 소스 목록            |
| eventSubscriptions.sources.sourceId           | Body | UUID     | 이벤트 소스의 식별자              |
| eventSubscriptions.sources.eventCategoryType  | Body | Enum     | 이벤트 카테고리 유형              |
| eventSubscriptions.userGroupIds               | Body | Array    | 이벤트 구독 중인 사용자 그룹의 식별자 목록 |
| eventSubscriptions.createdYmdt                | Body | DateTime | 생성 일시                    |

<details><summary>예시</summary>
<p>

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
            "eventSubscriptionId": "12345678-1234-1234-1234-123456789012",
            "eventCategoryType": "INSTANCE",
            "eventSubscriptionName": "example-event-subscription",
            "enabled": true,
            "notifyEmail": true,
            "notifySms": false,
            "eventCodes": [
                "INSTC_05_01"
            ],
            "sources": [
                {
                    "sourceId": "87654321-4321-4321-4321-210987654321",
                    "eventCategoryType": "INSTANCE"
                }
            ],
            "userGroupIds": [
                "11111111-2222-3333-4444-555555555555"
            ],
            "createdYmdt": "2024-01-01T12:00:00+09:00"
        }
    ]
}
```

</p>
</details>

---

<a id="create-an-event-subscription"></a>
### 이벤트 구독 생성하기 { #create-an-event-subscription }

```http
POST /v4.0/event-subscriptions
```

<a id="create-an-event-subscription-required-permission"></a>
#### 필요 권한

| 권한명                                                      | 설명           |
|----------------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:EventSubscription.Create | 이벤트 구독 생성하기 |

<a id="create-an-event-subscription-request"></a>
#### 요청

| 이름                           | 종류   | 형식      | 필수 | 설명                                    |
|------------------------------|------|---------|----|-----------------------------------------|
| eventCategoryType            | Body | Enum    | O  | 이벤트 카테고리 유형                          |
| eventSubscriptionName        | Body | String  | O  | 이벤트 구독을 식별할 수 있는 이름<br/>- 최대 길이: `100` |
| enabled                      | Body | Boolean | O  | 활성화 여부                                |
| notifyEmail                  | Body | Boolean | O  | 이메일 발송 여부                             |
| notifySms                    | Body | Boolean | O  | SMS 발송 여부                             |
| eventCodes                   | Body | Array   | O  | 구독할 이벤트 코드 목록                        |
| sources                      | Body | Array   | O  | 구독할 이벤트 소스 목록                        |
| sources.sourceId             | Body | UUID    | O  | 이벤트 소스의 식별자                          |
| sources.eventCategoryType    | Body | Enum    | O  | 이벤트 카테고리 유형                          |
| userGroupIds                 | Body | Array   | O  | 이벤트 구독할 사용자 그룹의 식별자 목록              |

<details><summary>예시</summary>
<p>

```json
{
    "eventCategoryType": "INSTANCE",
    "eventSubscriptionName": "example-event-subscription",
    "enabled": true,
    "notifyEmail": true,
    "notifySms": false,
    "eventCodes": [
        "INSTC_05_01"
    ],
    "sources": [
        {
            "sourceId": "87654321-4321-4321-4321-210987654321",
            "eventCategoryType": "INSTANCE"
        }
    ],
    "userGroupIds": [
        "11111111-2222-3333-4444-555555555555"
    ]
}
```

</p>
</details>

<a id="create-an-event-subscription-response"></a>
#### 응답

| 이름                    | 종류   | 형식   | 설명          |
|-----------------------|------|------|-------------|
| eventSubscriptionId   | Body | UUID | 이벤트 구독의 식별자 |

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "eventSubscriptionId": "12345678-1234-1234-1234-123456789012"
}
```

</p>
</details>

---

<a id="modify-an-event-subscription"></a>
### 이벤트 구독 수정하기 { #modify-an-event-subscription }

```http
PUT /v4.0/event-subscriptions/{eventSubscriptionId}
```

<a id="modify-an-event-subscription-required-permission"></a>
#### 필요 권한

| 권한명                                                      | 설명           |
|----------------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:EventSubscription.Modify | 이벤트 구독 수정하기 |

<a id="modify-an-event-subscription-request"></a>
#### 요청

| 이름                           | 종류   | 형식      | 필수 | 설명                              |
|------------------------------|------|---------|----|-----------------------------------|
| eventSubscriptionId          | URL  | UUID    | O  | 이벤트 구독의 식별자                    |
| eventCategoryType            | Body | Enum    | X  | 이벤트 카테고리 유형                    |
| eventSubscriptionName        | Body | String  | X  | 이벤트 구독을 식별할 수 있는 이름           |
| enabled                      | Body | Boolean | X  | 활성화 여부                          |
| notifyEmail                  | Body | Boolean | X  | 이메일 발송 여부                       |
| notifySms                    | Body | Boolean | X  | SMS 발송 여부                       |
| eventCodes                   | Body | Array   | X  | 구독할 이벤트 코드 목록                  |
| sources                      | Body | Array   | X  | 구독할 이벤트 소스 목록                  |
| sources.sourceId             | Body | UUID    | X  | 이벤트 소스의 식별자                    |
| sources.eventCategoryType    | Body | Enum    | X  | 이벤트 카테고리 유형                    |
| userGroupIds                 | Body | Array   | X  | 이벤트 구독할 사용자 그룹의 식별자 목록        |

<details><summary>예시</summary>
<p>

```json
{
    "eventSubscriptionName": "updated-event-subscription",
    "enabled": false,
    "notifyEmail": false,
    "notifySms": true,
    "eventCodes": [
        "INSTC_05_01",
        "INSTC_06_01"
    ],
    "sources": [
        {
            "sourceId": "87654321-4321-4321-4321-210987654321",
            "eventCategoryType": "INSTANCE"
        }
    ],
    "userGroupIds": [
        "11111111-2222-3333-4444-555555555555",
        "22222222-3333-4444-5555-666666666666"
    ]
}
```

</p>
</details>

<a id="modify-an-event-subscription-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---

<a id="delete-an-event-subscription"></a>
### 이벤트 구독 삭제하기 { #delete-an-event-subscription }

```http
DELETE /v4.0/event-subscriptions/{eventSubscriptionId}
```

<a id="delete-an-event-subscription-required-permission"></a>
#### 필요 권한

| 권한명                                                      | 설명           |
|----------------------------------------------------------|--------------|
| RDSfor{{engine.pascalCase}}:EventSubscription.Delete | 이벤트 구독 삭제하기 |

<a id="delete-an-event-subscription-request"></a>
#### 요청

| 이름                    | 종류  | 형식   | 필수 | 설명          |
|-----------------------|-----|------|----|-------------|
| eventSubscriptionId   | URL | UUID | O  | 이벤트 구독의 식별자 |

<a id="delete-an-event-subscription-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

<details><summary>예시</summary>
<p>

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    }
}
```

</p>
</details>

---
