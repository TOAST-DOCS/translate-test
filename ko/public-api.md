<!-- pre-align:aligned sig=0fdf7e57a581 -->

<a id="network-service-gateway-api-v2-guide"></a>
## Network > Service Gateway > API v2 가이드 { #network-service-gateway-api-v2-guide }

NHN Cloud Network 서비스는 API 호출 시 인증/인가를 위해 IaaS 토큰을 사용합니다. IaaS 토큰은 NHN Cloud의 OpenStack 기반 인프라 서비스(IaaS)에서 사용하는 인증 토큰입니다. IaaS 토큰 발급 및 사용에 대한 자세한 내용은 [IaaS 토큰](/nhncloud/ko/public-api/iaas-token)을 참고하세요.

서비스 게이트웨이 API는 `network` 타입 엔드포인트를 이용합니다. 정확한 엔드포인트는 토큰 발급 응답의 `serviceCatalog`를 참조합니다.

| 타입 | 리전 | 엔드포인트 |
|---|---|---|
| network | 한국(판교) 리전<br>한국(평촌) 리전<br>한국(광주) 리전 | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

API 응답에 가이드에 명시되지 않은 필드가 나타날 수 있습니다. 이런 필드는 NHN Cloud 내부 용도로 사용되며 사전 공지 없이 변경될 수 있으므로 사용하지 않습니다.

<a id="service-gateway"></a>
## 서비스 게이트웨이 { #service-gateway }

<a id="get-a-list-of-service-gateways"></a>
### 서비스 게이트웨이 목록 보기 { #get-a-list-of-service-gateways }

```
GET /v2.0/gateways/servicegateways
X-Auth-Token: {tokenId}
```

<a id="get-a-list-of-service-gateways-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 서비스 게이트웨이 ID |
| name | Query | String | - | 조회할 서비스 게이트웨이 이름 |
| service_endpoint_id | Query | UUID | - | 조회할 서비스 게이트웨이의 서비스 엔드포인트 ID |
| network_id | Query | UUID | - | 조회할 서비스 게이트웨이 VPC ID |
| subnet_id | Query | UUID | - | 조회할 서비스 게이트웨이 서브넷 ID |
| port_id | Query | UUID | - | 조회할 서비스 게이트웨이 포트 ID |
| fixed_ip| Query | String | - | 조회할 서비스 게이트웨이 IP 주소 |
| include_gateway_identity| Query | Boolean | - | NAT IP 주소 고정 사용 여부 |


<a id="get-a-list-of-service-gateways-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| servicegateways | Body | Array | 서비스 게이트웨이 정보 객체 목록 |
| servicegateways.id | Body | UUID | 서비스 게이트웨이 ID |
| servicegateways.name | Body | String | 서비스 게이트웨이 이름 |
| servicegateways.port_id | Body | UUID | 포트 ID |
| servicegateways.tenant_id | Body | String | 테넌트 ID |
| servicegateways.network_id | Body | UUID | VPC ID |
| servicegateways.subnet_id | Body | UUID | 서브넷 ID |
| servicegateways.fixed_ip | Body | String | 서비스 게이트웨이 IP 주소 |
| servicegateways.include_gateway_identity| Body | Boolean | NAT IP 주소 고정 사용 여부 |
| servicegateways.service_endpoint_id | Body | UUID | 서비스 엔드포인트 ID |
| servicegateways.description | Body | String | 서비스 게이트웨이 설명 |

<details><summary>예시</summary>

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
### 서비스 게이트웨이 보기 { #get-a-service-gateway }

```
GET /v2.0/gateways/servicegateways/{serviceGatewayId}
X-Auth-Token: {tokenId}
```

<a id="get-a-service-gateway-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| serviceGatewayId | URL | UUID | O | 서비스 게이트웨이 ID |

<a id="get-a-service-gateway-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| servicegateway | Body | Object | 서비스 게이트웨이 정보 객체|
| servicegateway.id | Body | UUID | 서비스 게이트웨이 ID |
| servicegateway.name | Body | String | 서비스 게이트웨이 이름 |
| servicegateway.port_id | Body | UUID | 포트 ID |
| servicegateway.tenant_id | Body | String | 테넌트 ID |
| servicegateway.network_id | Body | UUID | VPC ID |
| servicegateway.subnet_id | Body | UUID | 서브넷 ID |
| servicegateway.fixed_ip | Body | String | 서비스 게이트웨이 IP 주소 |
| servicegateway.include_gateway_identity| Body | Boolean | NAT IP 주소 고정 사용 여부 |
| servicegateway.service_endpoint_id | Body | UUID | 서비스 엔드포인트 ID |
| servicegateway.api_endpoints | Body | Array | API 엔드포인트 정보 객체 목록 |
| servicegateway.api_endpoints.domain_name | Body | String | API 엔드포인트 도메인 |
| servicegateway.description | Body | String | 서비스 게이트웨이 설명 |

<details><summary>예시</summary>

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
### 서비스 게이트웨이 생성하기 { #create-a-service-gateway }

```
POST /v2.0/gateways/servicegateways
X-Auth-Token: {tokenId}
```

<a id="create-a-service-gateway-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| servicegateway | Body | Object | O | 서비스 게이트웨이 정보 객체 |
| servicegateway.name | Body | String | - | 서비스 게이트웨이 이름 |
| servicegateway.description | Body | String | - | 서비스 게이트웨이 설명 |
| servicegateway.network_id | Body | UUID | O | VPC ID |
| servicegateway.subnet_id | Body | UUID | O | 서브넷 ID |
| servicegateway.fixed_ip | Body | String | - | 서비스 게이트웨이 IP 주소 |
| servicegateway.include_gateway_identity| Body | Boolean | - | NAT IP 주소 고정 사용 여부 |
| servicegateway.service_endpoint_id | Body | UUID | O | 서비스 엔드포인트 ID |




<details><summary>예시</summary>

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
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| servicegateway | Body | Object | 서비스 게이트웨이 정보 객체 목록 |
| servicegateway.id | Body | UUID | 서비스 게이트웨이 ID |
| servicegateway.name | Body | String | 서비스 게이트웨이 이름 |
| servicegateway.port_id | Body | UUID | 포트 ID |
| servicegateway.tenant_id | Body | String | 테넌트 ID |
| servicegateway.network_id | Body | UUID | VPC ID |
| servicegateway.subnet_id | Body | UUID | 서브넷 ID |
| servicegateway.fixed_ip | Body | String | 서비스 게이트웨이 IP 주소 |
| servicegateway.include_gateway_identity| Body | Boolean | NAT IP 주소 고정 사용 여부 |
| servicegateway.service_endpoint_id | Body | UUID | 서비스 엔드포인트 ID |
| servicegateway.api_endpoints | Body | Array | API 엔드포인트 정보 객체 목록 |
| servicegateway.api_endpoints.domain_name | Body | String | API 엔드포인트 도메인 |
| servicegateway.description | Body | String | 서비스 게이트웨이 설명 |


<details><summary>예시</summary>

```json
{
  "servicegateway": {
    "status": "AVAILABLE",
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
### 서비스 게이트웨이 수정하기 { #modify-a-service-gateway }

```
PUT /v2.0/gateways/servicegateways/{serviceGatewayId}
X-Auth-Token: {tokenId}
```

<a id="modify-a-service-gateway-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| serviceGatewayId | URL | UUID | O | 서비스 게이트웨이 ID |
| servicegateway | Body | Object | O | 서비스 게이트웨이 정보 객체 |
| servicegateway.name | Body | String | - | 서비스 게이트웨이 이름 |
| servicegateway.description | Body | String | - | 서비스 게이트웨이 설명 |

<details><summary>예시</summary>

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
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| servicegateway | Body | Object | 서비스 게이트웨이 정보 객체 |
| servicegateway.id | Body | UUID | 서비스 게이트웨이 ID |
| servicegateway.name | Body | String | 서비스 게이트웨이 이름 |
| servicegateway.port_id | Body | UUID | 포트 ID |
| servicegateway.tenant_id | Body | String | 테넌트 ID |
| servicegateway.network_id | Body | UUID | VPC ID |
| servicegateway.subnet_id | Body | UUID | 서브넷 ID |
| servicegateway.fixed_ip | Body | String | 서비스 게이트웨이 IP 주소 |
| servicegateway.include_gateway_identity| Body | Boolean | NAT IP 주소 고정 사용 여부 |
| servicegateway.service_endpoint_id | Body | UUID | 서비스 엔드포인트 ID |
| servicegateway.api_endpoints | Body | Array | API 엔드포인트 정보 객체 목록 |
| servicegateway.api_endpoints.domain_name | Body | String | API 엔드포인트 도메인 |
| servicegateway.description | Body | String | 서비스 게이트웨이 설명 |


<details><summary>예시</summary>

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
### 서비스 게이트웨이 삭제하기 { #delete-a-service-gateway }

```
DELETE /v2.0/gateways/servicegateways/{serviceGatewayId}
X-Auth-Token: {tokenId}
```

<a id="delete-a-service-gateway-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| serviceGatewayId | URL | UUID | O | 서비스 게이트웨이 ID |


<a id="delete-a-service-gateway-response"></a>
#### 응답
이 API는 응답 본문을 반환하지 않습니다.










<a id="service-endpoint"></a>
## 서비스 엔드포인트 { #service-endpoint }

<a id="get-a-list-of-service-endpoints"></a>
### 서비스 엔드포인트 목록 보기 { #get-a-list-of-service-endpoints }

```
GET /v2.0/gateways/serviceendpoints/
X-Auth-Token: {tokenId}
```

<a id="get-a-list-of-service-endpoints-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 서비스 엔드포인트 ID |
| display_name | Query | UUID | - | 조회할 서비스 엔드포인트 이름 |



<a id="get-a-list-of-service-endpoints-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| serviceendpoints | Body | Array | 서비스 엔드포인트 정보 객체 목록 |
| serviceendpoints.id | Body | UUID | 서비스 엔드포인트 ID |
| serviceendpoints.display_name | Body | String | 콘솔에 출력되는 서비스 엔드포인트 이름 |
| serviceendpoints.support_gateway_identity | Body | Boolean | NAT IP 주소 고정 사용 가능 여부 |
| serviceendpoints.description | Body | String | 서비스 엔드포인트 설명 |

<details><summary>예시</summary>

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
### 서비스 엔드포인트 보기 { #get-a-service-endpoint }

```
GET /v2.0/gateways/serviceendpoints/{seerviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="get-a-service-endpoint-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| serviceEndpointId | URL | UUID | O | 서비스 엔드포인트 ID |

<a id="get-a-service-endpoint-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| serviceendpoint | Body | Object | 서비스 엔드포인트 정보 객체  |
| serviceendpoint.id | Body | UUID | 서비스 엔드포인트 ID |
| serviceendpoint.display_name | Body | String | 콘솔에 출력되는 서비스 엔드포인트 이름 |
| serviceendpoint.support_gateway_identity | Body | Boolean | NAT IP 주소 고정 사용 가능 여부 |
| serviceendpoint.description | Body | String | 서비스 엔드포인트 설명 |

<details><summary>예시</summary>

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
