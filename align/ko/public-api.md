<a id="network-nat-gateway-api-v2-guide"></a>
## Network > NAT Gateway > API v2 가이드 { #network-nat-gateway-api-v2-guide }

NHN Cloud Network 서비스는 API 호출 시 인증/인가를 위해 IaaS 토큰을 사용합니다. IaaS 토큰은 NHN Cloud의 OpenStack 기반 인프라 서비스(IaaS)에서 사용하는 인증 토큰입니다. IaaS 토큰 발급 및 사용에 대한 자세한 내용은 [IaaS 토큰](/nhncloud/ko/public-api/iaas-token)을 참고하세요.

NAT 게이트웨이 API는 `network` 타입 엔드포인트를 이용합니다. 정확한 엔드포인트는 토큰 발급 응답의 `serviceCatalog`를 참조합니다.

| 타입 | 리전                                  | 엔드포인트                                                                                                                                                                                  |
|---|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| network | 한국(판교) 리전<br>한국(평촌) 리전<br>한국(광주) 리전 | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

API 응답에 가이드에 명시되지 않은 필드가 나타날 수 있습니다. 이런 필드는 NHN Cloud 내부 용도로 사용되며 사전 공지 없이 변경될 수 있으므로 사용하지 않습니다.


<a id="nat-gateway"></a>
## NAT 게이트웨이 { #nat-gateway }
<a id="view-a-list-of-nat-gateways"></a>
### NAT 게이트웨이 목록 보기 { #view-a-list-of-nat-gateways }
```
GET /v2.0/natgateways
X-Auth-Token: {tokenId}
```

<a id="view-a-list-of-nat-gateways-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명                                                                             |
|---|---|---|---|--------------------------------------------------------------------------------|
| tokenId | Header | String | O | 토큰 ID                                                                          |
| id | Query | UUID | - | 조회할 NAT 게이트웨이 ID                                                               |
| tenant_id | Query | String | - | 조회할 NAT 게이트웨이의 테넌트 ID                                                          |
| name | Query | String | - | 조회할 NAT 게이트웨이의 이름                                                              |
| sort_dir | Query | Enum | - | 조회할 NAT 게이트웨이의 정렬 방향<br>`sort_key`에서 지정한 필드를 기준으로 정렬<br>**asc**, **desc** 중 하나 |
| sort_key | Query | String | - | 조회할 NAT 게이트웨이의 정렬 키<br>`sort_dir`에서 지정한 방향대로 정렬                                |
| fields | Query | String | - | 조회할 NAT 게이트웨이의 필드 이름<br>예: `fields=id&fields=name`                             |

<a id="view-a-list-of-nat-gateways-response"></a>
#### 응답

| 이름                         | 종류 | 형식 | 설명                                             |
|----------------------------|---|---|------------------------------------------------|
| natgateways                | Body | Array | NAT 게이트웨이 정보 객체 목록                             |
| natgateways.id             | Body | UUID | NAT 게이트웨이의 ID                                  |
| natgateways.name           | Body | String | NAT 게이트웨이 이름                                   |
| natgateways.vpc_id         | Body | UUID | NAT 게이트웨이의 VPC ID                              |
| natgateways.subnet_id      | Body | UUID | NAT 게이트웨이의 서브넷 ID                              |
| natgateways.port_id        | Body | UUID | NAT 게이트웨이의 포트 ID                               |
| natgateways.floatingips_id | Body | UUID | NAT 게이트웨이의 플로팅 IP ID                           |
| natgateways.tenant_id      | Body | String | NAT 게이트웨이의 테넌트 ID                              |
| natgateways.project_id     | Body | String | NAT 게이트웨이의 프로젝트 ID. 테넌트 ID와 동일.                |
| natgateways.fixed_ip       | Body | String | NAT 게이트웨이의 고정 IP 주소                            |
| natgateways.floating_ip    | Body | String | NAT 게이트웨이의 플로팅 IP 주소                           |
| natgateways.create_time    | Body | String | NAT 게이트웨이 생성 시간(UTC 기준)                       |
| natgateways.description    | Body | String | NAT 게이트웨이 설명                                   |
| natgateways.status         | Body | Enum | NAT 게이트웨이 상태<br>`ACTIVE`, `BUILD`, `ERROR` 중 하나. |


<details><summary>예시</summary>
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

<a id="view-nat-gateways"></a>
### NAT 게이트웨이 보기 { #view-nat-gateways }
```
GET /v2.0/natgateways/{NatGatewayId}
X-Auth-Token: {tokenId}
```

<a id="view-nat-gateways-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류     | 형식     | 필수 | 설명                                                                   |
|---|--------|--------|---|----------------------------------------------------------------------|
| NatGatewayId | URL    | UUID   | O | NAT 게이트웨이 ID                                                         |
| tokenId | Header | String | O | 토큰 ID                                                                |
| fields | Query  | String | - | 조회할 NAT 게이트웨이의 필드 이름<br>지정한 필드만 응답에 반환<br>예: `fields=id&fields=name` |

<a id="view-nat-gateways-response"></a>
#### 응답

| 이름                        | 종류 | 형식 | 설명                                               |
|---------------------------|---|---|--------------------------------------------------|
| natgateway                | Body | Array | NAT 게이트웨이 정보 객체                                  |
| natgateway.id             | Body | UUID | NAT 게이트웨이의 ID                                   |
| natgateway.name           | Body | String | NAT 게이트웨이 이름                                    |
| natgateway.vpc_id         | Body | UUID | NAT 게이트웨이의 VPC ID                               |
| natgateway.subnet_id      | Body | UUID | NAT 게이트웨이의 서브넷 ID                               |
| natgateway.port_id        | Body | UUID | NAT 게이트웨이의 포트 ID                                |
| natgateway.floatingips_id | Body | UUID | NAT 게이트웨이의 플로팅 IP ID                            |
| natgateway.tenant_id      | Body | String | NAT 게이트웨이의 테넌트 ID                               |
| natgateway.project_id     | Body | String | NAT 게이트웨이의 프로젝트 ID. 테넌트 ID와 동일.                 |
| natgateway.fixed_ip       | Body | String | NAT 게이트웨이의 고정 IP 주소                             |
| natgateway.floating_ip    | Body | String | NAT 게이트웨이의 플로팅 IP 주소                            |
| natgateway.create_time    | Body | String | NAT 게이트웨이 생성 시간(UTC 기준)                            |
| natgateway.description    | Body | String | NAT 게이트웨이 설명                                    |
| natgateway.status         | Body | Enum | NAT 게이트웨이 상태<br>`ACTIVE`, `BUILD`, `ERROR` 중 하나. |


<details><summary>예시</summary>
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
<a id="create-a-nat-gateway"></a>
### NAT 게이트웨이 생성하기 { #create-a-nat-gateway }

새로운 NAT 게이트웨이를 생성합니다.

```
POST /v2.0/natgateways
X-Auth-Token: {tokenId}
```

<a id="create-a-nat-gateway-request"></a>
#### 요청

| 이름                        | 종류 | 형식     | 필수 | 설명                   |
|---------------------------|---|--------|----|----------------------|
| tokenId                   | Header | String | O  | 토큰 ID                |
| natgateway                | Body | Object | O  | NAT 게이트웨이 생성 요청 객체   |
| natgateway.name           | Body | String | O  | NAT 게이트웨이 이름         |
| natgateway.vpc_id         | Body | UUID   | O  | NAT 게이트웨이의 VPC ID    |
| natgateway.subnet_id      | Body | UUID   | O  | NAT 게이트웨이의 서브넷 ID    |
| natgateway.floatingips_id | Body | UUID   | O  | NAT 게이트웨이의 플로팅 IP ID |
| natgateway.description    | Body | String | -  | NAT 게이트웨이 설명         |



<details><summary>예시</summary>
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


<a id="create-a-nat-gateway-response"></a>
#### 응답
| 이름                        | 종류 | 형식 | 설명                                               |
|---------------------------|---|---|--------------------------------------------------|
| natgateway                | Body | Array | NAT 게이트웨이 정보 객체                                  |
| natgateway.id             | Body | UUID | NAT 게이트웨이의 ID                                   |
| natgateway.name           | Body | String | NAT 게이트웨이 이름                                    |
| natgateway.vpc_id         | Body | UUID | NAT 게이트웨이의 VPC ID                               |
| natgateway.subnet_id      | Body | UUID | NAT 게이트웨이의 서브넷 ID                               |
| natgateway.port_id        | Body | UUID | NAT 게이트웨이의 포트 ID                                |
| natgateway.floatingips_id | Body | UUID | NAT 게이트웨이의 플로팅 IP ID                            |
| natgateway.tenant_id      | Body | String | NAT 게이트웨이의 테넌트 ID                               |
| natgateway.project_id     | Body | String | NAT 게이트웨이의 프로젝트 ID. 테넌트 ID와 동일.                 |
| natgateway.fixed_ip       | Body | String | NAT 게이트웨이의 고정 IP 주소                             |
| natgateway.floating_ip    | Body | String | NAT 게이트웨이의 플로팅 IP 주소                            |
| natgateway.create_time    | Body | String | NAT 게이트웨이 생성 시간(UTC 기준)                               |
| natgateway.description    | Body | String | NAT 게이트웨이 설명                                    |
| natgateway.status         | Body | Enum | NAT 게이트웨이 상태<br>`ACTIVE`, `BUILD`, `ERROR` 중 하나. |


<details><summary>예시</summary>
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
<a id="modifying-the-nat-gateway"></a>
### NAT 게이트웨이 수정하기 { #modifying-the-nat-gateway }

기존 NAT 게이트웨이를 수정합니다.

```
PUT /v2.0/natgateways/{NatGatewayId}
X-Auth-Token: {tokenId}
```

<a id="modifying-the-nat-gateway-request"></a>
#### 요청

| 이름                        | 종류 | 형식     | 필수 | 설명                 |
|---------------------------|---|--------|----|--------------------|
| NatGatewayId | URL    | UUID   | O  | NAT 게이트웨이 ID       |
| tokenId                   | Header | String | O  | 토큰 ID              |
| natgateway                | Body | Object | O  | NAT 게이트웨이 생성 요청 객체 |
| natgateway.name           | Body | String | -  | NAT 게이트웨이 이름       |
| natgateway.description    | Body | String | -  | NAT 게이트웨이 설명       |



<details><summary>예시</summary>
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


<a id="modifying-the-nat-gateway-response"></a>
#### 응답
| 이름                        | 종류 | 형식 | 설명                                              |
|---------------------------|---|---|-------------------------------------------------|
| natgateway                | Body | Array | NAT 게이트웨이 정보 객체                                 |
| natgateway.id             | Body | UUID | NAT 게이트웨이의 ID                                   |
| natgateway.name           | Body | String | NAT 게이트웨이 이름                                    |
| natgateway.vpc_id         | Body | UUID | NAT 게이트웨이의 VPC ID                               |
| natgateway.subnet_id      | Body | UUID | NAT 게이트웨이의 서브넷 ID                               |
| natgateway.port_id        | Body | UUID | NAT 게이트웨이의 포트 ID                                |
| natgateway.floatingips_id | Body | UUID | NAT 게이트웨이의 플로팅 IP ID                            |
| natgateway.tenant_id      | Body | String | NAT 게이트웨이의 테넌트 ID                               |
| natgateway.project_id     | Body | String | NAT 게이트웨이의 프로젝트 ID. 테넌트 ID와 동일.                 |
| natgateway.fixed_ip       | Body | String | NAT 게이트웨이의 고정 IP 주소                             |
| natgateway.floating_ip    | Body | String | NAT 게이트웨이의 플로팅 IP 주소                            |
| natgateway.create_time    | Body | String | NAT 게이트웨이 생성 시간(UTC 기준)                         |
| natgateway.description    | Body | String | NAT 게이트웨이 설명                                    |
| natgateway.status         | Body | Enum | NAT 게이트웨이 상태<br>`ACTIVE`, `BUILD`, `ERROR` 중 하나. |


<details><summary>예시</summary>
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
<a id="delete-a-nat-gateway"></a>
### NAT 게이트웨이 삭제하기 { #delete-a-nat-gateway }
지정한 NAT 게이트웨이를 삭제합니다.
```
DELETE /v2.0/natgateways/{NatGatewayId}
X-Auth-Token: {tokenId}
```

<a id="delete-a-nat-gateway-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| NatGatewayId | URL    | UUID   | O  | NAT 게이트웨이 ID       |
| tokenId | Header | String | O | 토큰 ID |

<a id="delete-a-nat-gateway-response"></a>
#### 응답
이 API는 응답 본문을 반환하지 않습니다.

