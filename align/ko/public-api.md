
## Network > Colocation Gateway > API v2 가이드

NHN Cloud Network 서비스는 API 호출 시 인증/인가를 위해 IaaS 토큰을 사용합니다. IaaS 토큰은 NHN Cloud의 OpenStack 기반 인프라 서비스(IaaS)에서 사용하는 인증 토큰입니다. IaaS 토큰 발급 및 사용에 대한 자세한 내용은 [IaaS 토큰](/nhncloud/ko/public-api/iaas-token)을 참고하세요.

코로케이션 게이트웨이 API는 `network` 타입 엔드포인트를 이용합니다. 정확한 엔드포인트는 토큰 발급 응답의 `serviceCatalog`를 참조합니다.

| 타입 | 리전 | 엔드포인트 |
|---|---|---|
| network | 한국(판교) 리전<br>한국(평촌) 리전<br>한국(광주) 리전 | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

API 응답에 가이드에 명시되지 않은 필드가 나타날 수 있습니다. 이런 필드는 NHN Cloud 내부 용도로 사용되며 사전 공지 없이 변경될 수 있으므로 사용하지 않습니다.

## 코로케이션 게이트웨이

### 코로케이션 게이트웨이 목록 보기

```
GET /v2.0/gateways/colocationgateways
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 코로케이션 게이트웨이 ID |
| name | Query | String | - | 조회할 코로케이션 게이트웨이 이름 |
| vpc_id | Query | String | - | 조회할 코로케이션 게이트웨이와 연결된 VPC ID |


#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| colocationgateways | Body | Array | 코로케이션 게이트웨이 정보 객체 목록 |
| colocationgateways.id | Body | UUID | 코로케이션 게이트웨이 ID |
| colocationgateways.name | Body | String | 코로케이션 게이트웨이 이름 |
| colocationgateways.vpc_id | Body | UUID | 연결된 VPC ID |
| colocationgateways.tenant_id | Body | String | 테넌트 ID |
| colocationgateways.status | Body | UUID | 리소스 상태 |
| colocationgateways.description | Body | String | 코로케이션 게이트웨이 설명 |
| colocationgateways.vpc.name | Body | String | 연결된 VPC 이름 |
| colocationgateways.vpc.id | Body | String | 연결된 VPC ID |
| colocationgateways.vpc.cidrv4 | Body | String | 연결된 VPC CIDR |

<details><summary>예시</summary>

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
### 코로케이션 게이트웨이 보기

```
GET /v2.0/gateways/colocationgateways/{colocationGatewayId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| colocationGatewayId | URL | UUID | O | 코로케이션 게이트웨이 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| colocationgateways | Body | Array | 코로케이션 게이트웨이 정보 객체 목록 |
| colocationgateways.id | Body | UUID | 코로케이션 게이트웨이 ID |
| colocationgateways.name | Body | String | 코로케이션 게이트웨이 이름 |
| colocationgateways.vpc_id | Body | UUID | 연결된 VPC ID |
| colocationgateways.tenant_id | Body | String | 테넌트 ID |
| colocationgateways.status | Body | UUID | 리소스 상태 |
| colocationgateways.description | Body | String | 코로케이션 게이트웨이 설명 |
| colocationgateways.vpc.name | Body | String | 연결된 VPC 이름 |
| colocationgateways.vpc.id | Body | String | 연결된 VPC ID |
| colocationgateways.vpc.cidrv4 | Body | String | 연결된 VPC CIDR |

<details><summary>예시</summary>

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
