<!-- pre-align:aligned sig=fbbff493af43 -->

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
| service_endpoint_id | Query | UUID | - | 조회할 서비스 게이트웨이의 서비스 엔드포인트(또는 사용자 정의 엔드포인트) ID |
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
| servicegateways.service_endpoint_id | Body | UUID | 서비스 엔드포인트(또는 사용자 정의 엔드포인트) ID |
| servicegateways.service_provider | Body | String | 연결 유형(연결된 엔드포인트의 값). `csp`=서비스 엔드포인트 / `user`=사용자 정의 엔드포인트 |
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
| servicegateway.service_endpoint_id | Body | UUID | 서비스 엔드포인트(또는 사용자 정의 엔드포인트) ID |
| servicegateway.service_provider | Body | String | 연결 유형(연결된 엔드포인트의 값). `csp`=서비스 엔드포인트 / `user`=사용자 정의 엔드포인트 |
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
| servicegateway.service_endpoint_id | Body | UUID | O | 서비스 엔드포인트(또는 사용자 정의 엔드포인트) ID |

> 사용자 정의 엔드포인트에 연결하려면 게시자에게 전달받은 `service_name`으로 [서비스 엔드포인트 목록 보기](#get-a-list-of-service-endpoints)를 조회해 얻은 `service_endpoint_id`를 사용합니다. 연결 유형(`service_provider`)은 연결된 엔드포인트에서 자동으로 결정되며 요청 값으로 지정하지 않습니다.


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
| servicegateway.service_endpoint_id | Body | UUID | 서비스 엔드포인트(또는 사용자 정의 엔드포인트) ID |
| servicegateway.service_provider | Body | String | 연결 유형(연결된 엔드포인트의 값). `csp`=서비스 엔드포인트 / `user`=사용자 정의 엔드포인트 |
| servicegateway.api_endpoints | Body | Array | API 엔드포인트 정보 객체 목록 |
| servicegateway.api_endpoints.domain_name | Body | String | API 엔드포인트 도메인 |
| servicegateway.description | Body | String | 서비스 게이트웨이 설명 |


<details><summary>예시</summary>

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

> 연결 유형(`service_provider`)은 연결된 엔드포인트의 값을 보여주는 읽기 전용 항목이며, 서비스 게이트웨이 수정으로 변경할 수 없습니다.

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
| servicegateway.service_endpoint_id | Body | UUID | 서비스 엔드포인트(또는 사용자 정의 엔드포인트) ID |
| servicegateway.service_provider | Body | String | 연결 유형(연결된 엔드포인트의 값). `csp`=서비스 엔드포인트 / `user`=사용자 정의 엔드포인트 |
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
| display_name | Query | String | - | 조회할 서비스 엔드포인트 이름 |
| service_name | Query | String | - | 조회할 서비스 이름(사용자 정의 엔드포인트 연결 시 사용, 형식 `{region}.sep-{12 hex}`) |

> 서비스 게이트웨이를 사용자 정의 엔드포인트에 연결할 때는 게시자에게 전달받은 `service_name`으로 조회하여 서비스 엔드포인트 ID를 획득합니다. 보안을 위해 `service_name` 값은 응답에 포함되지 않으며, 허용 프로젝트에 포함되지 않은 경우 빈 목록이 반환됩니다.


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
<a id="custom-endpoints"></a>
## 사용자 정의 엔드포인트 { #custom-endpoints }

사용자가 자신의 리소스(로드 밸런서)를 엔드포인트로 게시하여 다른 프로젝트와 공유하는 기능입니다. 게시자(소유자)가 생성/관리하며, 생성 시 공유용 서비스 이름(`service_name`)이 발급됩니다.

<a id="view-custom-endpoint-list"></a>
### 사용자 정의 엔드포인트 목록 보기 { #view-custom-endpoint-list }

```
GET /v2.0/gateways/myserviceendpoints
X-Auth-Token: {tokenId}
```

<a id="view-custom-endpoint-list-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 사용자 정의 엔드포인트 ID |
| endpoint_type | Query | String | - | 조회할 엔드포인트 유형(예: `lb.type1`) |
| port_id | Query | UUID | - | 조회할 대상 리소스(로드 밸런서) 포트 ID |

<a id="view-custom-endpoint-list-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| myserviceendpoints | Body | Array | 사용자 정의 엔드포인트 정보 객체 목록 |
| myserviceendpoints.id | Body | UUID | 사용자 정의 엔드포인트 ID |
| myserviceendpoints.name | Body | String | 이름 |
| myserviceendpoints.display_name | Body | String | 표시 이름(서비스 게이트웨이에 노출되는 이름) |
| myserviceendpoints.endpoint_type | Body | String | 엔드포인트 유형(리소스 유형, 예: `lb.type1`) |
| myserviceendpoints.port_id | Body | UUID | 대상 리소스(로드 밸런서) 포트 ID. `GET /v2.0/lbaas/loadbalancers?vip_port_id={port_id}`로 대상 로드 밸런서를 찾을 수 있습니다. |
| myserviceendpoints.service_name | Body | String | 공유용 서비스 이름(형식 `{region}.sep-{12 hex}`) |
| myserviceendpoints.max_count | Body | Integer | 최대 생성 개수(이 엔드포인트로 생성 가능한 서비스 게이트웨이 최대 개수). `0`=생성 차단, 미설정=무제한 |
| myserviceendpoints.current_count | Body | Integer | 사용 현황(이 엔드포인트로 현재 생성된 서비스 게이트웨이 수) |
| myserviceendpoints.service_provider | Body | String | 연결 유형(사용자 정의 엔드포인트는 `user`) |
| myserviceendpoints.description | Body | String | 설명 |
| myserviceendpoints.project_id | Body | String | 테넌트 ID |

<details><summary>예시</summary>

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
### 사용자 정의 엔드포인트 보기 { #get-a-custom-endpoint }

```
GET /v2.0/gateways/myserviceendpoints/{serviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="get-a-custom-endpoint-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| serviceEndpointId | URL | UUID | O | 사용자 정의 엔드포인트 ID |

<a id="get-a-custom-endpoint-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| myserviceendpoint | Body | Object | 사용자 정의 엔드포인트 정보 객체 |
| myserviceendpoint.id | Body | UUID | 사용자 정의 엔드포인트 ID |
| myserviceendpoint.name | Body | String | 이름 |
| myserviceendpoint.display_name | Body | String | 표시 이름 |
| myserviceendpoint.endpoint_type | Body | String | 엔드포인트 유형(리소스 유형) |
| myserviceendpoint.port_id | Body | UUID | 대상 리소스(로드 밸런서) 포트 ID. `GET /v2.0/lbaas/loadbalancers?vip_port_id={port_id}`로 대상 로드 밸런서를 찾을 수 있습니다. |
| myserviceendpoint.service_name | Body | String | 공유용 서비스 이름 |
| myserviceendpoint.max_count | Body | Integer | 최대 생성 개수 |
| myserviceendpoint.current_count | Body | Integer | 사용 현황(현재 생성된 서비스 게이트웨이 수) |
| myserviceendpoint.service_provider | Body | String | 연결 유형(`user`) |
| myserviceendpoint.description | Body | String | 설명 |
| myserviceendpoint.project_id | Body | String | 테넌트 ID |

<details><summary>예시</summary>

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
### 사용자 정의 엔드포인트 생성하기 { #create-a-custom-endpoint }

```
POST /v2.0/gateways/myserviceendpoints
X-Auth-Token: {tokenId}
```

<a id="create-a-custom-endpoint-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| myserviceendpoint | Body | Object | O | 사용자 정의 엔드포인트 정보 객체 |
| myserviceendpoint.name | Body | String | O | 이름(255자 이내, 영문/숫자/-/_) |
| myserviceendpoint.display_name | Body | String | - | 표시 이름(생략 시 `name`과 동일하게 적용) |
| myserviceendpoint.port_id | Body | UUID | O | 대상 리소스(로드 밸런서) 포트 ID. 로드 밸런서 보기(`GET /v2.0/lbaas/loadbalancers/{loadbalancerId}`) 응답의 `vip_port_id`를 사용합니다. |
| myserviceendpoint.max_count | Body | Integer | - | 최대 생성 개수(0~1,000). 0: 생성 차단, null 또는 미입력: 무제한 |
| myserviceendpoint.description | Body | String | - | 설명 |

> 대상 리소스로 로드 밸런서를 지정하면 `endpoint_type`이 `lb.type1`로, `service_provider`가 `user`로 자동 설정됩니다. 생성이 완료되면 공유용 `service_name`이 자동으로 발급됩니다. 프로젝트당 기본 5개까지 생성할 수 있습니다.

<details><summary>예시</summary>

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
#### 응답
응답 본문은 [사용자 정의 엔드포인트 보기](#get-a-custom-endpoint)와 동일하며, 자동 발급된 `service_name`이 포함됩니다.

---
<a id="modify-a-custom-endpoint"></a>
### 사용자 정의 엔드포인트 수정하기 { #modify-a-custom-endpoint }

```
PUT /v2.0/gateways/myserviceendpoints/{serviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="modify-a-custom-endpoint-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| serviceEndpointId | URL | UUID | O | 사용자 정의 엔드포인트 ID |
| myserviceendpoint | Body | Object | O | 사용자 정의 엔드포인트 정보 객체 |
| myserviceendpoint.name | Body | String | - | 이름 |
| myserviceendpoint.display_name | Body | String | - | 표시 이름 |
| myserviceendpoint.max_count | Body | Integer | - | 최대 생성 개수(0~1000). 0: 생성 차단, null: 무제한으로 변경, 필드 미포함 시 기존 값 유지 |
| myserviceendpoint.description | Body | String | - | 설명 |

> 리소스 유형(`endpoint_type`)과 대상 리소스(`port_id`)는 변경할 수 없습니다. 최대 생성 개수를 줄여도 기존 서비스 게이트웨이는 유지되며, 현재 개수가 최대 생성 개수를 초과하는 동안에는 추가 생성할 수 없습니다.

<details><summary>예시</summary>

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
#### 응답
응답 본문은 [사용자 정의 엔드포인트 보기](#get-a-custom-endpoint)와 동일합니다.

---
<a id="delete-custom-endpoint"></a>
### 사용자 정의 엔드포인트 삭제하기 { #delete-custom-endpoint }

```
DELETE /v2.0/gateways/myserviceendpoints/{serviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="delete-custom-endpoint-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| serviceEndpointId | URL | UUID | O | 사용자 정의 엔드포인트 ID |

> 이 엔드포인트를 사용 중인 서비스 게이트웨이가 있으면 삭제할 수 없습니다. 삭제 시 등록된 허용 프로젝트도 함께 삭제됩니다.

<a id="delete-custom-endpoint-response"></a>
#### 응답
이 API는 응답 본문을 반환하지 않습니다.

---
<a id="reissue-a-service-name"></a>
### 서비스 이름 재발급하기 { #reissue-a-service-name }

```
PUT /v2.0/gateways/serviceendpoints/{serviceEndpointId}/generate_service_name
X-Auth-Token: {tokenId}
```

<a id="reissue-a-service-name-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| serviceEndpointId | URL | UUID | O | 사용자 정의 엔드포인트 ID |

> 엔드포인트를 생성한 프로젝트의 구성원(소유자)만 수행할 수 있습니다. 재발급 시 기존 `service_name`은 즉시 폐기되어 더 이상 조회되지 않습니다. 기존 `service_name`으로 생성한 서비스 게이트웨이는 정상 동작하지만, 신규 생성 시에는 재발급된 `service_name`을 사용해야 합니다.

<a id="reissue-a-service-name-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| service_name | Body | String | 재발급된 공유용 서비스 이름 |

<details><summary>예시</summary>

```json
{
  "service_name": "kr1.sep-9f8e7d6c5b4a"
}
```

</details>

---
<a id="allowed-projects"></a>
## 허용 프로젝트 { #allowed-projects }

사용자 정의 엔드포인트에 연결(서비스 게이트웨이 생성)을 허용할 대상(테넌트)을 관리하는 목록(white list)입니다. 순수 허용 목록(권한)이며 생성 개수 제한은 다루지 않습니다(개수 제한은 엔드포인트의 `max_count`에서 관리).

<a id="view-allow-project-list"></a>
### 허용 프로젝트 목록 보기 { #view-allow-project-list }

```
GET /v2.0/gateways/serviceendpointallowprojects
X-Auth-Token: {tokenId}
```

<a id="view-allow-project-list-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| service_endpoint_id | Query | UUID | - | 조회할 사용자 정의 엔드포인트 ID |
| target_tenant_id | Query | String | - | 조회할 허용 대상 테넌트 ID |

<a id="view-allow-project-list-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| serviceendpointallowprojects | Body | Array | 허용 프로젝트 정보 객체 목록 |
| serviceendpointallowprojects.id | Body | UUID | 허용 프로젝트 ID |
| serviceendpointallowprojects.service_endpoint_id | Body | UUID | 사용자 정의 엔드포인트 ID |
| serviceendpointallowprojects.target_tenant_id | Body | String | 허용 대상. `*`=전체 프로젝트 / 테넌트 ID=특정 프로젝트 |
| serviceendpointallowprojects.name | Body | String | 이름(참고용) |
| serviceendpointallowprojects.description | Body | String | 설명 |

<details><summary>예시</summary>

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
### 허용 프로젝트 보기 { #view-allowed-projects }

```
GET /v2.0/gateways/serviceendpointallowprojects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="view-allowed-projects-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| allowProjectId | URL | UUID | O | 허용 프로젝트 ID |

<a id="view-allowed-projects-response"></a>
#### 응답
응답 본문은 [허용 프로젝트 목록 보기](#view-allow-project-list)의 단일 객체(`serviceendpointallowproject`)와 동일합니다.

---
<a id="create-an-allowed-project"></a>
### 허용 프로젝트 생성하기 { #create-an-allowed-project }

```
POST /v2.0/gateways/serviceendpointallowprojects
X-Auth-Token: {tokenId}
```

<a id="create-an-allowed-project-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| serviceendpointallowproject | Body | Object | O | 허용 프로젝트 정보 객체 |
| serviceendpointallowproject.service_endpoint_id | Body | UUID | O | 사용자 정의 엔드포인트 ID |
| serviceendpointallowproject.target_tenant_id | Body | String | O | 허용 대상. `*`=전체 프로젝트 / 테넌트 ID(32 hex)=특정 프로젝트 |
| serviceendpointallowproject.name | Body | String | - | 이름(참고용) |
| serviceendpointallowproject.description | Body | String | - | 설명 |

> 전체 허용(`*`)과 특정 프로젝트를 함께 등록한 경우 더 좁은 범위(특정 프로젝트)가 적용됩니다. 이를 이용해 무중단으로 허용 범위를 전환할 수 있습니다. 엔드포인트 소유자의 테넌트 ID는 등록할 수 없습니다(소유자는 항상 허용). 동일(엔드포인트, 테넌트) 조합이 이미 있으면 409.

<details><summary>예시</summary>

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
#### 응답
응답 본문은 [허용 프로젝트 목록 보기](#view-allow-project-list)의 단일 객체(`serviceendpointallowproject`)와 동일합니다.

---
<a id="modify-allowed-projects"></a>
### 허용 프로젝트 수정하기 { #modify-allowed-projects }

```
PUT /v2.0/gateways/serviceendpointallowprojects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="modify-allowed-projects-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| allowProjectId | URL | UUID | O | 허용 프로젝트 ID |
| serviceendpointallowproject | Body | Object | O | 허용 프로젝트 정보 객체 |
| serviceendpointallowproject.name | Body | String | - | 이름(참고용) |
| serviceendpointallowproject.description | Body | String | - | 설명 |

> 허용 대상(`target_tenant_id`)과 엔드포인트(`service_endpoint_id`)는 변경할 수 없으며, `name`·`description`만 수정할 수 있습니다.

<details><summary>예시</summary>

```json
{
  "serviceendpointallowproject": {
    "name": "allow-b-renamed",
    "description": "B 프로젝트 연동"
  }
}
```

</details>

<a id="modify-allowed-projects-response"></a>
#### 응답
응답 본문은 [허용 프로젝트 목록 보기](#view-allow-project-list)의 단일 객체(`serviceendpointallowproject`)와 동일합니다.

---
<a id="delete-an-allowed-project"></a>
### 허용 프로젝트 삭제하기 { #delete-an-allowed-project }

```
DELETE /v2.0/gateways/serviceendpointallowprojects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="delete-an-allowed-project-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| allowProjectId | URL | UUID | O | 허용 프로젝트 ID |

<a id="delete-an-allowed-project-response"></a>
#### 응답
이 API는 응답 본문을 반환하지 않습니다.

---
<a id="usage-status"></a>
## 사용 현황 { #usage-status }

사용자 정의 엔드포인트를 사용 중인(연결한) 소비자 측 서비스 게이트웨이 목록을 조회합니다.

<a id="view-usage-status-list"></a>
### 사용 현황 목록 보기 { #view-usage-status-list }

```
GET /v2.0/gateways/serviceendpointusages
X-Auth-Token: {tokenId}
```

<a id="view-usage-status-list-request"></a>
#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 사용자 정의 엔드포인트 ID(복수 지정 가능, 생략 시 소유한 모든 엔드포인트 대상) |
| network_id | Query | UUID | - | 조회할 서비스 게이트웨이 VPC ID(복수 지정 가능) |
| subnet_id | Query | UUID | - | 조회할 서비스 게이트웨이 서브넷 ID(복수 지정 가능) |
| limit | Query | Integer | - | 한 번에 조회할 최대 개수(생략 시 전체 반환) |
| marker | Query | UUID | - | 직전 페이지 마지막 항목의 서비스 게이트웨이 ID(다음 페이지 조회 시 사용) |
| page_reverse | Query | Boolean | - | `true`로 지정하면 이전 페이지 방향으로 조회 |
| sort_key | Query | String | - | 정렬 기준 필드(복수 지정 가능) |
| sort_dir | Query | String | - | 정렬 방향(`asc` 또는 `desc`). `sort_key`와 반드시 쌍으로, 같은 개수로 지정 |

> 결과는 기본적으로 서비스 게이트웨이 ID(`id`) 오름차순으로 정렬됩니다. 생성 시각순으로 조회하려면 `sort_key=create_time&sort_dir=desc`와 같이 명시해야 합니다. `sort_key`에는 응답 필드(`id`, `name`, `fixed_ip`, `status`, `tenant_id`, `network_id`, `subnet_id`, `service_endpoint_id`, `create_time`)를 사용할 수 있습니다.
> `limit`을 지정하면 응답에 다음/이전 페이지 링크(`serviceendpointusages_links`)가 포함됩니다. 다음 페이지는 링크의 URL을 그대로 호출하거나, 현재 페이지 마지막 항목의 `id`를 `marker`로 지정해 조회합니다. 페이지를 순회하는 동안에는 동일한 필터/정렬 조건을 유지해야 합니다.

<a id="view-usage-status-list-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| serviceendpointusages | Body | Array | 사용 현황 정보 객체 목록 |
| serviceendpointusages.id | Body | UUID | 서비스 게이트웨이 ID |
| serviceendpointusages.name | Body | String | 서비스 게이트웨이 이름 |
| serviceendpointusages.fixed_ip | Body | String | 서비스 게이트웨이 IP 주소 |
| serviceendpointusages.status | Body | String | 서비스 게이트웨이 상태 |
| serviceendpointusages.tenant_id | Body | String | 서비스 게이트웨이를 생성한 소비자 프로젝트의 테넌트 ID |
| serviceendpointusages.network_id | Body | UUID | 서비스 게이트웨이 VPC ID |
| serviceendpointusages.subnet_id | Body | UUID | 서비스 게이트웨이 서브넷 ID |
| serviceendpointusages.service_endpoint_id | Body | UUID | 연결된 사용자 정의 엔드포인트 ID |
| serviceendpointusages.create_time | Body | String | 서비스 게이트웨이 생성 시각 |
| serviceendpointusages_links | Body | Array | 페이지네이션 링크 목록(`limit` 지정 시에만 포함) |
| serviceendpointusages_links.rel | Body | String | 링크 유형. `next`=다음 페이지 / `previous`=이전 페이지 |
| serviceendpointusages_links.href | Body | String | 해당 페이지를 조회할 수 있는 URL |

<details><summary>예시</summary>

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
