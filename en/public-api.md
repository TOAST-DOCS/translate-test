<!-- pre-align:aligned sig=fbbff493af43 -->

<a id="network-service-gateway-api-v2-guide"></a>
## Network > Service Gateway > API v2 Guide { #network-service-gateway-api-v2-guide }

NHN Cloud Network services use IaaS tokens for authentication and authorization when making API calls. The IaaS token is an authentication token used for NHN Cloud's OpenStack-based infrastructure services (IaaS). For more information on issuing and using IaaS tokens, please refer to the [IaaS Token](/nhncloud/en/public-api/iaas-token).

For Service Gateway APIs, the `network` type endpoint is used. For more details, see `serviceCatalog` from the response of token issuance.

| Type | Region | Endpoint |
|---|---|---|
| network | Korea (Pangyo) Region<br>Korea (Pyeongchon) Region<br>Korea (Gwangju) Region | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

In each API response, you may find fields that are not specified within this guide. Those fields are for NHN Cloud internal usage, so refrain from using them because they may be changed without prior notice.

<a id="service-gateway"></a>
## Service Gateway { #service-gateway }

<a id="get-a-list-of-service-gateways"></a>
### Get a List of Service Gateways { #get-a-list-of-service-gateways }

```
GET /v2.0/gateways/servicegateways
X-Auth-Token: {tokenId}
```

<a id="get-a-list-of-service-gateways-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | The ID of the service gateway to retrieve |
| name | Query | String | - | The name of the service gateway to retrieve |
| service_endpoint_id | Query | UUID | - | The service endpoint (or custom endpoint) ID of the service gateway to retrieve |
| network_id | Query | UUID | - | The VPC ID of the service gateway to retrieve |
| subnet_id | Query | UUID | - | The subnet ID of the service gateway to retrieve |
| port_id | Query | UUID | - | The port ID of the service gateway to retrieve |
| fixed_ip| Query | String | - | The IP address of the service gateway to retrieve |
| include_gateway_identity| Query | Boolean | - | Whether to use a static NAT IP address |
<a id="get-a-list-of-service-gateways-response"></a>
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| servicegateways | Body | Array | A list of service gateway information objects |
| servicegateways.id | Body | UUID | The ID of the service gateway |
| servicegateways.name | Body | String | The name of the service gateway |
| servicegateways.port_id | Body | UUID | Port ID |
| servicegateways.tenant_id | Body | String | Tenant ID |
| servicegateways.network_id | Body | UUID | VPC ID |
| servicegateways.subnet_id | Body | UUID | Subnet ID |
| servicegateways.fixed_ip | Body | String | The IP address of the service gateway |
| servicegateways.include_gateway_identity| Body | Boolean | Whether to use fixed NAT IP address |
| servicegateways.service_endpoint_id | Body | UUID | Service endpoint (or Custom endpoint) ID |
| servicegateways.service_provider | Body | String | Connection type (the value of the connected endpoint). `csp`=Service Endpoint / `user`=Custom endpoint |
| servicegateways.description | Body | String | The description for the service gateway |

<details><summary>Example</summary>

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
### Get a Service Gateway { #get-a-service-gateway }

```
GET /v2.0/gateways/servicegateways/{serviceGatewayId}
X-Auth-Token: {tokenId}
```

<a id="get-a-service-gateway-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| serviceGatewayId | URL | UUID | O | The ID of the service gateway |

<a id="get-a-service-gateway-response"></a>
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| servicegateway | Body | Object | Service gateway information object|
| servicegateway.id | Body | UUID | The ID of the service gateway |
| servicegateway.name | Body | String | The name of the service gateway |
| servicegateway.port_id | Body | UUID | Port ID |
| servicegateway.tenant_id | Body | String | Tenant ID |
| servicegateway.network_id | Body | UUID | VPC ID |
| servicegateway.subnet_id | Body | UUID | Subnet ID |
| servicegateway.fixed_ip | Body | String | The IP address of the service gateway |
| servicegateway.include_gateway_identity| Body | Boolean | Whether to use fixed NAT IP address |
| servicegateway.service_endpoint_id | Body | UUID | Service endpoint (or custom endpoint) ID |
| servicegateway.service_provider | Body | String | Connection type (value of the connected endpoint). `csp`=Service Endpoint / `user`=Custom endpoint |
| servicegateway.api_endpoints | Body | Array | List of API endpoint information objects |
| servicegateway.api_endpoints.domain_name | Body | String | API endpoint domain |
| servicegateway.description | Body | String | The description for the service gateway |

<details><summary>Example</summary>

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
### Create a Service Gateway { #create-a-service-gateway }

```
POST /v2.0/gateways/servicegateways
X-Auth-Token: {tokenId}
```

<a id="create-a-service-gateway-request"></a>
#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| servicegateway | Body | Object | O | Service gateway information object |
| servicegateway.name | Body | String | - | The name of the service gateway |
| servicegateway.description | Body | String | - | The description for the service gateway |
| servicegateway.network_id | Body | UUID | O | VPC ID |
| servicegateway.subnet_id | Body | UUID | O | Subnet ID |
| servicegateway.fixed_ip | Body | String | - | Service gateway IP address |
| servicegateway.include_gateway_identity| Body | Boolean | - | Whether to use fixed NAT IP address |
| servicegateway.service_endpoint_id | Body | UUID | O | Service endpoint (or custom endpoint) ID |
> To connect to a custom endpoint, use the `service_endpoint_id` obtained by calling [Get a List of Service Endpoints](#get-a-list-of-service-endpoints) with the `service_name` provided by the publisher. The connection type (`service_provider`) is determined automatically from the connected endpoint and is not specified as a request value.

<details><summary>Example</summary>

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
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| servicegateway | Body | Object | A list of service gateway information objects |
| servicegateway.id | Body | UUID | The ID of the service gateway |
| servicegateway.name | Body | String | The name of the service gateway |
| servicegateway.port_id | Body | UUID | Port ID |
| servicegateway.tenant_id | Body | String | Tenant ID |
| servicegateway.network_id | Body | UUID | VPC ID |
| servicegateway.subnet_id | Body | UUID | Subnet ID |
| servicegateway.fixed_ip | Body | String | The IP address of the service gateway |
| servicegateway.include_gateway_identity| Body | Boolean | Whether to sue fixed NAT IP address |
| servicegateway.service_endpoint_id | Body | UUID | Service endpoint (or custom endpoint) ID |
| servicegateway.service_provider | Body | String | Connection type (value of the connected endpoint). `csp`=Service Endpoint / `user`=Custom endpoint |
| servicegateway.api_endpoints | Body | Array | List of API endpoint information objects |
| servicegateway.api_endpoints.domain_name | Body | String | API endpoint domain |
| servicegateway.description | Body | String | The description for the service gateway |


<details><summary>Example</summary>

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
### Modify a Service Gateway { #modify-a-service-gateway }

```
PUT /v2.0/gateways/servicegateways/{serviceGatewayId}
X-Auth-Token: {tokenId}
```

<a id="modify-a-service-gateway-request"></a>
#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| serviceGatewayId | URL | UUID | O | The ID of the service gateway |
| servicegateway | Body | Object | O | Service gateway information object |
| servicegateway.name | Body | String | - | The name of the service gateway |
| servicegateway.description | Body | String | - | The description for the service gateway |

> The connection type (`service_provider`) is a read-only field that shows the value of the connected endpoint and cannot be changed by modifying the service gateway.

<details><summary>Example</summary>

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
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| servicegateway | Body | Object | Service gateway information object |
| servicegateway.id | Body | UUID | The ID of the service gateway |
| servicegateway.name | Body | String | The name of the service gateway |
| servicegateway.port_id | Body | UUID | Port ID |
| servicegateway.tenant_id | Body | String | Tenant ID |
| servicegateway.network_id | Body | UUID | VPC ID |
| servicegateway.subnet_id | Body | UUID | Subnet ID |
| servicegateway.fixed_ip | Body | String | The IP address of the service gateway |
| servicegateway.include_gateway_identity| Body | Boolean | Whether to use fixed NAT IP address |
| servicegateway.service_endpoint_id | Body | UUID | Service endpoint (or custom endpoint) ID |
| servicegateway.service_provider | Body | String | Connection type (value of the connected endpoint). `csp`=Service Endpoint / `user`=Custom Endpoint |
| servicegateway.api_endpoints | Body | Array | List of API endpoint information objects |
| servicegateway.api_endpoints.domain_name | Body | String | API endpoint domain |
| servicegateway.description | Body | String | The description for the service gateway |


<details><summary>Example</summary>

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
### Delete a Service Gateway { #delete-a-service-gateway }

```
DELETE /v2.0/gateways/servicegateways/{serviceGatewayId}
X-Auth-Token: {tokenId}
```

<a id="delete-a-service-gateway-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| serviceGatewayId | URL | UUID | O | The ID of the service gateway |


<a id="delete-a-service-gateway-response"></a>
#### Response
Stops the specified node group.










<a id="service-endpoint"></a>
## Service Endpoint { #service-endpoint }

<a id="get-a-list-of-service-endpoints"></a>
### Get a List of Service Endpoints { #get-a-list-of-service-endpoints }

```
GET /v2.0/gateways/serviceendpoints/
X-Auth-Token: {tokenId}
```

<a id="get-a-list-of-service-endpoints-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | The ID of the service endpoint to retrieve |
| display_name | Query | String | - | The name of the service endpoint to retrieve |
| service_name | Query | String | - | The service name to retrieve (used when connecting to a custom endpoint; format: `{region}.sep-{12 hex}`) |
> When connecting a service gateway to a Custom endpoint, retrieve the service endpoint ID by querying with the `service_name` provided by the publisher. For security purposes, the `service_name` value is not included in the response, and an empty list is returned if the project is not included in the allowed projects.

<a id="get-a-list-of-service-endpoints-response"></a>
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| serviceendpoints | Body | Array | List of service endpoint information objects |
| serviceendpoints.id | Body | UUID | Service endpoint ID |
| serviceendpoints.display_name | Body | String | The name of the service endpoint to appear in the console |
| serviceendpoints.support_gateway_identity | Body | Boolean | Whether to use fixed NAT IP address |
| serviceendpoints.description | Body | String | The description for the service endpoint |

<details><summary>Example</summary>

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
### Get a Service Endpoint { #get-a-service-endpoint }

```
GET /v2.0/gateways/serviceendpoints/{seerviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="get-a-service-endpoint-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| serviceEndpointId | URL | UUID | O | Service endpoint ID |

<a id="get-a-service-endpoint-response"></a>
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| serviceendpoint | Body | Object | Service endpoint information object  |
| serviceendpoint.id | Body | UUID | Service endpoint ID |
| serviceendpoint.display_name | Body | String | The name of the service endpoint to appear in the console |
| serviceendpoint.support_gateway_identity | Body | Boolean | Whether to use fixed NAT IP address |
| serviceendpoint.description | Body | String | The description for the service endpoint |

<details><summary>Example</summary>

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
## Custom Endpoints { #custom-endpoints }

This feature allows you to publish your own resources (load balancers) as endpoints to share with other projects. The publisher (owner) creates and manages them. When created, a service name (`service_name`) for sharing is issued.

<a id="view-custom-endpoint-list"></a>
### View Custom Endpoint List { #view-custom-endpoint-list }

```
GET /v2.0/gateways/myserviceendpoints
X-Auth-Token: {tokenId}
```

<a id="view-custom-endpoint-list-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Custom endpoint ID to retrieve |
| endpoint_type | Query | String | - | Endpoint type to retrieve (e.g., `lb.type1`) |
| port_id | Query | UUID | - | Port ID of the target resource (load balancer) to retrieve |

<a id="view-custom-endpoint-list-response"></a>
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| myserviceendpoints | Body | Array | List of custom endpoint information objects |
| myserviceendpoints.id | Body | UUID | Custom endpoint ID |
| myserviceendpoints.name | Body | String | Name |
| myserviceendpoints.display_name | Body | String | Display name (the name exposed in the service gateway) |
| myserviceendpoints.endpoint_type | Body | String | Endpoint type (resource type, e.g., `lb.type1`) |
| myserviceendpoints.port_id | Body | UUID | Target resource (load balancer) port ID. You can find the target load balancer by using `GET /v2.0/lbaas/loadbalancers?vip_port_id={port_id}`. |
| myserviceendpoints.service_name | Body | String | Service name for sharing (format: `{region}.sep-{12 hex}`) |
| myserviceendpoints.max_count | Body | Integer | Maximum number of instances that can be created (the maximum number of service gateways that can be created using this endpoint). `0` = creation blocked, not set = unlimited |
| myserviceendpoints.current_count | Body | Integer | Current usage (the number of service gateways currently created using this endpoint) |
| myserviceendpoints.service_provider | Body | String | Connection type (custom endpoints use `user`) |
| myserviceendpoints.description | Body | String | Description |
| myserviceendpoints.project_id | Body | String | Tenant ID |

<details><summary>Example</summary>

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

<a id="get-a-custom-endpoint"></a>
### Get a Custom Endpoint { #get-a-custom-endpoint }

```
GET /v2.0/gateways/myserviceendpoints/{serviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="get-a-custom-endpoint-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| serviceEndpointId | URL | UUID | O | Custom endpoint ID |

<a id="get-a-custom-endpoint-response"></a>
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| myserviceendpoint | Body | Object | Custom endpoint information object |
| myserviceendpoint.id | Body | UUID | Custom endpoint ID |
| myserviceendpoint.name | Body | String | Name |
| myserviceendpoint.display_name | Body | String | Display name |
| myserviceendpoint.endpoint_type | Body | String | Endpoint type (resource type) |
| myserviceendpoint.port_id | Body | UUID | Target resource (load balancer) port ID. You can find the target load balancer using `GET /v2.0/lbaas/loadbalancers?vip_port_id={port_id}`. |
| myserviceendpoint.service_name | Body | String | Service name for sharing |
| myserviceendpoint.max_count | Body | Integer | Maximum number of instances that can be created |
| myserviceendpoint.current_count | Body | Integer | Current usage (number of service gateways currently created) |
| myserviceendpoint.service_provider | Body | String | Connection type (`user`) |
| myserviceendpoint.description | Body | String | Description |
| myserviceendpoint.project_id | Body | String | Tenant ID |

<details><summary>Example</summary>

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

<a id="create-a-custom-endpoint"></a>
### Create a Custom Endpoint { #create-a-custom-endpoint }

```
POST /v2.0/gateways/myserviceendpoints
X-Auth-Token: {tokenId}
```

<a id="create-a-custom-endpoint-request"></a>
#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| myserviceendpoint | Body | Object | O | Custom endpoint information object |
| myserviceendpoint.name | Body | String | O | Name (up to 255 characters; letters, numbers, `-`, `_`) |
| myserviceendpoint.display_name | Body | String | - | Display name (if omitted, same as `name`) |
| myserviceendpoint.port_id | Body | UUID | O | Target resource (load balancer) port ID. Use the `vip_port_id` from the response of Get a load balancer (`GET /v2.0/lbaas/loadbalancers/{loadbalancerId}`). |
| myserviceendpoint.max_count | Body | Integer | - | Maximum number of endpoints to create (0–1,000). 0: block creation, null or not entered: unlimited |
| myserviceendpoint.description | Body | String | - | Description |

> If you specify a load balancer as the target resource, `endpoint_type` is automatically set to `lb.type1` and `service_provider` is automatically set to `user`. Once creation is complete, a `service_name` for sharing is automatically issued. You can create up to 5 per project by default.

<details><summary>Example</summary>

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
#### Response
The response body is the same as [Get a Custom Endpoint](#get-a-custom-endpoint), and includes the automatically issued `service_name`.

<a id="modify-a-custom-endpoint"></a>
### Modify a Custom Endpoint { #modify-a-custom-endpoint }

```
PUT /v2.0/gateways/myserviceendpoints/{serviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="modify-a-custom-endpoint-request"></a>
#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| serviceEndpointId | URL | UUID | O | Custom endpoint ID |
| myserviceendpoint | Body | Object | O | Custom endpoint information object |
| myserviceendpoint.name | Body | String | - | Name |
| myserviceendpoint.display_name | Body | String | - | Display name |
| myserviceendpoint.max_count | Body | Integer | - | Maximum number of instances to create (0–1000). 0: block creation, null: change to unlimited, if the field is not included, the existing value is retained |
| myserviceendpoint.description | Body | String | - | Description |

> The resource type (`endpoint_type`) and the target resource (`port_id`) cannot be changed. Reducing the maximum number does not affect existing service gateways, and no additional service gateways can be created while the current count exceeds the maximum.

<details><summary>Example</summary>

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
#### Response
The response body is the same as [Get a Custom Endpoint](#get-a-custom-endpoint).

<a id="delete-custom-endpoint"></a>
### Delete Custom Endpoint { #delete-custom-endpoint }

```
DELETE /v2.0/gateways/myserviceendpoints/{serviceEndpointId}
X-Auth-Token: {tokenId}
```

<a id="delete-custom-endpoint-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| serviceEndpointId | URL | UUID | O | Custom endpoint ID |

> If there is a service gateway using this endpoint, it cannot be deleted. When deleted, the registered allowed projects are also deleted.

<a id="delete-custom-endpoint-response"></a>
#### Response
This API does not return a response body.

<a id="reissue-a-service-name"></a>
### Reissue a Service Name { #reissue-a-service-name }

```
PUT /v2.0/gateways/serviceendpoints/{serviceEndpointId}/generate_service_name
X-Auth-Token: {tokenId}
```

<a id="reissue-a-service-name-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| serviceEndpointId | URL | UUID | O | Custom endpoint ID |

> Only a member (owner) of the project that created the endpoint can perform this action. Upon reissuance, the existing `service_name` is immediately invalidated and can no longer be retrieved. Service gateways created with the existing `service_name` continue to function normally, but the reissued `service_name` must be used when creating new ones.

<a id="reissue-a-service-name-response"></a>
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| service_name | Body | String | Reissued service name for sharing |

<details><summary>Example</summary>

```json
{
  "service_name": "kr1.sep-9f8e7d6c5b4a"
}
```

</details>

<a id="allowed-projects"></a>
## Allowed Projects { #allowed-projects }

This is a list (whitelist) that manages the targets (tenants) that are allowed to connect to a custom endpoint (create a service gateway). It is a pure allowlist (permissions) and does not cover creation count limits (count limits are managed in the endpoint's `max_count`).

<a id="view-allow-project-list"></a>
### View Allow Project List { #view-allow-project-list }

```
GET /v2.0/gateways/serviceendpointallowprojects
X-Auth-Token: {tokenId}
```

<a id="view-allow-project-list-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| service_endpoint_id | Query | UUID | - | Custom endpoint ID to retrieve |
| target_tenant_id | Query | String | - | Allowed target tenant ID to retrieve |

<a id="view-allow-project-list-response"></a>
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| serviceendpointallowprojects | Body | Array | List of allowed project information objects |
| serviceendpointallowprojects.id | Body | UUID | Allowed project ID |
| serviceendpointallowprojects.service_endpoint_id | Body | UUID | Custom endpoint ID |
| serviceendpointallowprojects.target_tenant_id | Body | String | Allowed target. `*` = all projects / tenant ID = specific project |
| serviceendpointallowprojects.name | Body | String | Name (for reference) |
| serviceendpointallowprojects.description | Body | String | Description |

<details><summary>Example</summary>

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

<a id="view-allowed-projects"></a>
### View Allowed Projects { #view-allowed-projects }

```
GET /v2.0/gateways/serviceendpointallowprojects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="view-allowed-projects-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| allowProjectId | URL | UUID | O | Allowed project ID |

<a id="view-allowed-projects-response"></a>
#### Response
The response body is the same as the single object (`serviceendpointallowproject`) in [View Allowed Project List](#view-allow-project-list).

<a id="create-an-allowed-project"></a>
### Create an Allowed Project { #create-an-allowed-project }

```
POST /v2.0/gateways/serviceendpointallowprojects
X-Auth-Token: {tokenId}
```

<a id="create-an-allowed-project-request"></a>
#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| serviceendpointallowproject | Body | Object | O | Allow project information object |
| serviceendpointallowproject.service_endpoint_id | Body | UUID | O | Custom endpoint ID |
| serviceendpointallowproject.target_tenant_id | Body | String | O | Allow target. `*` = all projects / Tenant ID (32 hex) = specific project |
| serviceendpointallowproject.name | Body | String | - | Name (for reference) |
| serviceendpointallowproject.description | Body | String | - | Description |

> If you register both all-allow (`*`) and a specific project at the same time, the narrower scope (specific project) takes effect. You can use this to switch the allowed scope without downtime. The tenant ID of the endpoint owner cannot be registered (the owner is always allowed). If the same (endpoint, tenant) combination already exists, a 409 is returned.

<details><summary>Example</summary>

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
#### Response
The response body is identical to a single object (`serviceendpointallowproject`) from [View Allowing Project List](#view-allow-project-list).

<a id="modify-allowed-projects"></a>
### Modify Allowed Projects { #modify-allowed-projects }

```
PUT /v2.0/gateways/serviceendpointallowprojects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="modify-allowed-projects-request"></a>
#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| allowProjectId | URL | UUID | O | Allowed project ID |
| serviceendpointallowproject | Body | Object | O | Allowed project information object |
| serviceendpointallowproject.name | Body | String | - | Name (for reference) |
| serviceendpointallowproject.description | Body | String | - | Description |

> The allowed target (`target_tenant_id`) and endpoint (`service_endpoint_id`) cannot be changed. Only `name` and `description` can be modified.

<details><summary>Example</summary>

```json
{
  "serviceendpointallowproject": {
    "name": "allow-b-renamed",
    "description": "Project B integration"
  }
}
```

</details>

<a id="modify-allowed-projects-response"></a>
#### Response
The response body is the same as a single object (`serviceendpointallowproject`) in [View Allowed Project List](#view-allow-project-list).

<a id="delete-an-allowed-project"></a>
### Delete an Allowed Project { #delete-an-allowed-project }

```
DELETE /v2.0/gateways/serviceendpointallowprojects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="delete-an-allowed-project-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| allowProjectId | URL | UUID | O | Allowed project ID |

<a id="delete-an-allowed-project-response"></a>
#### Response
This API does not return a response body.

<a id="usage-status"></a>
## Usage Status { #usage-status }

Retrieves the list of consumer-side service gateways that are using (connected to) the custom endpoint.

<a id="view-usage-status-list"></a>
### View Usage Status List { #view-usage-status-list }

```
GET /v2.0/gateways/serviceendpointusages
X-Auth-Token: {tokenId}
```

<a id="view-usage-status-list-request"></a>
#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Custom endpoint ID to retrieve (multiple values allowed; if omitted, all owned endpoints are targeted) |
| network_id | Query | UUID | - | The VPC ID of the service gateway to retrieve (multiple values allowed) |
| subnet_id | Query | UUID | - | The subnet ID of the service gateway to retrieve (multiple values allowed) |
| limit | Query | Integer | - | Maximum number of items to retrieve at once (if omitted, all items are returned) |
| marker | Query | UUID | - | Service gateway ID of the last item on the previous page (used when requesting the next page) |
| page_reverse | Query | Boolean | - | If set to `true`, retrieves in the previous page direction |
| sort_key | Query | String | - | Field to sort by (multiple values allowed) |
| sort_dir | Query | String | - | Sort direction (`asc` or `desc`). Must be paired with `sort_key` and specified in the same quantity |

> By default, results are sorted in ascending order by service gateway ID (`id`). To retrieve results in order of creation time, you must specify it explicitly, such as `sort_key=create_time&sort_dir=desc`. The following response fields can be used for `sort_key`: `id`, `name`, `fixed_ip`, `status`, `tenant_id`, `network_id`, `subnet_id`, `service_endpoint_id`, `create_time`.
> If `limit` is specified, the response includes links to the next/previous pages (`serviceendpointusages_links`). To retrieve the next page, either call the URL in the link directly, or specify the `id` of the last item on the current page as the `marker`. The same filter and sort conditions must be maintained while paginating.

<a id="view-usage-status-list-response"></a>
#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| serviceendpointusages | Body | Array | List of usage information objects |
| serviceendpointusages.id | Body | UUID | Service gateway ID |
| serviceendpointusages.name | Body | String | Service gateway name |
| serviceendpointusages.fixed_ip | Body | String | The IP address of the service gateway |
| serviceendpointusages.status | Body | String | Service gateway status |
| serviceendpointusages.tenant_id | Body | String | Tenant ID of the consumer project that created the service gateway |
| serviceendpointusages.network_id | Body | UUID | Service gateway VPC ID |
| serviceendpointusages.subnet_id | Body | UUID | Service gateway subnet ID |
| serviceendpointusages.service_endpoint_id | Body | UUID | ID of the associated custom endpoint |
| serviceendpointusages.create_time | Body | String | Time at which the service gateway was created |
| serviceendpointusages_links | Body | Array | List of pagination links (included only when `limit` is specified) |
| serviceendpointusages_links.rel | Body | String | Link type. `next` = next page / `previous` = previous page |
| serviceendpointusages_links.href | Body | String | URL for retrieving the corresponding page |

<details><summary>Example</summary>

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
