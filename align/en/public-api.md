## Network > NAT Gateway > API v2 Guide

NHN Cloud Network services use IaaS tokens for authentication and authorization when making API calls. The IaaS token is an authentication token used for NHN Cloud's OpenStack-based infrastructure services (IaaS). For more information on issuing and using IaaS tokens, please refer to the [IaaS Token](/nhncloud/en/public-api/iaas-token).

The NAT Gateway API utilizes an endpoint of the `network` type. The exact endpoint is referenced in the `serviceCatalog`of the token issuance response.

| Type | Region                                                 | Endpoint                                                                                                                                                                               |
|---|--------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| network | Korea (Pangyo) Region<br>Korea (Pyeongchon) Region<br>Korea (Gwangju) Region | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

In each API response, you may find fields that are not specified within this guide. Those fields are for NHN Cloud internal usage, so refrain from using them because they may be changed without prior notice.


## NAT gateway
### View a list of NAT gateways
```
GET /v2.0/natgateways
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description                                                                             |
|---|---|---|---|--------------------------------------------------------------------------------|
| tokenId | Header | String | O | Token ID                                                                          |
| id | Query | UUID | - | NAT gateway ID to retrieve                                                               |
| tenant_id | Query | String | - | Tenant ID of the NAT gateway to retrieve                                                          |
| name | Query | String | - | Name of the NAT gateway to retrieve                                                              |
| sort_dir | Query | Enum | - | Sort direction of NAT gateways to retrieve<br>Sort by the field specified by `sort_key`<br>Either **asc**, or **desc** |
| sort_key | Query | String | - | Sort key of the NAT gateway to retrieve<br>Sort in the direction as specified by `sort_dir`                                |
| fields | Query | String | - | Field name of the NAT gateway to retrieve<br>Example: `fields=id&fields=name`                             |

#### Response

| Name                         | Type | Format | Description                                             |
|----------------------------|---|---|------------------------------------------------|
| natgateways                | Body | Array | NAT Gateway Information Object List                             |
| natgateways.id             | Body | UUID | ID of the NAT gateway                                  |
| natgateways.name           | Body | String | NAT gateway name                                   |
| natgateways.vpc_id         | Body | UUID | VPC ID of the NAT gateway                              |
| natgateways.subnet_id      | Body | UUID | Subnet ID of the NAT gateway                              |
| natgateways.port_id        | Body | UUID | Port ID of the NAT gateway                               |
| natgateways.floatingips_id | Body | UUID | Floating IP IDs for NAT gateways                           |
| natgateways.tenant_id      | Body | String | Tenant ID of the NAT gateway                              |
| natgateways.project_id     | Body | String | Project ID of the NAT gateway. Same as the tenant ID.                |
| natgateways.fixed_ip       | Body | String | Static IP address of the NAT gateway                            |
| natgateways.floating_ip    | Body | String | Floating IP addresses for NAT gateways                           |
| natgateways.create_time    | Body | String | NAT gateway creation time (in UTC)                       |
| natgateways.description    | Body | String | NAT gateway description                                   |
| natgateways.status         | Body | Enum | NAT gateway status<br>One of `ACTIVE`, `BUILD`, or `ERROR`. |


<details><summary>Example</summary>
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

### View NAT Gateways
```
GET /v2.0/natgateways/{NatGatewayId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type     | Format     | Required | Description                                                                   |
|---|--------|--------|---|----------------------------------------------------------------------|
| NatGatewayId | URL    | UUID   | O | NAT Gateway ID                                                         |
| tokenId | Header | String | O | Token ID                                                                |
| fields | Query  | String | - | Field name of the NAT gateway to retrieve<br>Return only specified fields in the response<br>Example: `fields=id&fields=name` |

#### Response

| Name                        | Type | Format | Description                                               |
|---------------------------|---|---|--------------------------------------------------|
| natgateway                | Body | Array | NAT Gateway Information Object                                  |
| natgateway.id             | Body | UUID | ID of the NAT gateway                                   |
| natgateway.name           | Body | String | NAT gateway name                                    |
| natgateway.vpc_id         | Body | UUID | VPC ID of the NAT gateway                               |
| natgateway.subnet_id      | Body | UUID | Subnet ID of the NAT gateway                               |
| natgateway.port_id        | Body | UUID | Port ID of the NAT gateway                                |
| natgateway.floatingips_id | Body | UUID | Floating IP IDs for NAT gateways                            |
| natgateway.tenant_id      | Body | String | Tenant ID of the NAT gateway                               |
| natgateway.project_id     | Body | String | Project ID of the NAT gateway. Same as the tenant ID.                 |
| natgateway.fixed_ip       | Body | String | Static IP address of the NAT gateway                             |
| natgateway.floating_ip    | Body | String | Floating IP addresses for NAT gateways                            |
| natgateway.create_time    | Body | String | NAT gateway creation time (in UTC)                            |
| natgateway.description    | Body | String | NAT gateway descriptions                                    |
| natgateway.status         | Body | Enum | NAT gateway status<br>One of `ACTIVE`, `BUILD`, or `ERROR`. |


<details><summary>Example</summary>
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
### Create a NAT gateway

Create a new NAT gateway.

```
POST /v2.0/natgateways
X-Auth-Token: {tokenId}
```

#### Request

| Name                        | Type | Format     | Required | Description                   |
|---------------------------|---|--------|----|----------------------|
| tokenId                   | Header | String | O  | Token ID                |
| natgateway                | Body | Object | O  | NAT Gateway Creation Request Object   |
| natgateway.name           | Body | String | O  | NAT gateway name         |
| natgateway.vpc_id         | Body | UUID   | O  | VPC ID of the NAT gateway    |
| natgateway.subnet_id      | Body | UUID   | O  | Subnet ID of the NAT gateway    |
| natgateway.floatingips_id | Body | UUID   | O  | Floating IP IDs for NAT gateways |
| natgateway.description    | Body | String | -  | NAT gateway descriptions         |



<details><summary>Example</summary>
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


#### Response
| Name                        | Type | Format | Description                                               |
|---------------------------|---|---|--------------------------------------------------|
| natgateway                | Body | Array | NAT Gateway Information Object                                  |
| natgateway.id             | Body | UUID | ID of the NAT gateway                                   |
| natgateway.name           | Body | String | NAT gateway name                                    |
| natgateway.vpc_id         | Body | UUID | VPC ID of the NAT gateway                               |
| natgateway.subnet_id      | Body | UUID | Subnet ID of the NAT gateway                               |
| natgateway.port_id        | Body | UUID | Port ID of the NAT gateway                                |
| natgateway.floatingips_id | Body | UUID | Floating IP IDs for NAT gateways                            |
| natgateway.tenant_id      | Body | String | Tenant ID of the NAT gateway                               |
| natgateway.project_id     | Body | String | Project ID of the NAT gateway. Same as the tenant ID.                 |
| natgateway.fixed_ip       | Body | String | Static IP address of the NAT gateway                             |
| natgateway.floating_ip    | Body | String | Floating IP addresses for NAT gateways                            |
| natgateway.create_time    | Body | String | NAT gateway creation time (in UTC)                               |
| natgateway.description    | Body | String | NAT gateway descriptions                                    |
| natgateway.status         | Body | Enum | NAT gateway status<br>One of `ACTIVE`, `BUILD`, or `ERROR`. |


<details><summary>Example</summary>
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
### Modifying the NAT gateway

Modify an existing NAT gateway.

```
PUT /v2.0/natgateways/{NatGatewayId}
X-Auth-Token: {tokenId}
```

#### Request

| Name                        | Type | Format     | Required | Description                 |
|---------------------------|---|--------|----|--------------------|
| NatGatewayId | URL    | UUID   | O  | NAT Gateway ID       |
| tokenId                   | Header | String | O  | Token ID              |
| natgateway                | Body | Object | O  | NAT Gateway Creation Request Object |
| natgateway.name           | Body | String | -  | NAT gateway name       |
| natgateway.description    | Body | String | -  | NAT gateway descriptions       |



<details><summary>Example</summary>
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


#### Response
| Name                        | Type | Format | Description                                              |
|---------------------------|---|---|-------------------------------------------------|
| natgateway                | Body | Array | NAT Gateway Information Object                                 |
| natgateway.id             | Body | UUID | ID of the NAT gateway                                   |
| natgateway.name           | Body | String | NAT gateway name                                    |
| natgateway.vpc_id         | Body | UUID | VPC ID of the NAT gateway                               |
| natgateway.subnet_id      | Body | UUID | Subnet ID of the NAT gateway                               |
| natgateway.port_id        | Body | UUID | Port ID of the NAT gateway                                |
| natgateway.floatingips_id | Body | UUID | Floating IP IDs for NAT gateways                            |
| natgateway.tenant_id      | Body | String | Tenant ID of the NAT gateway                               |
| natgateway.project_id     | Body | String | Project ID of the NAT gateway. Same as the tenant ID.                 |
| natgateway.fixed_ip       | Body | String | Static IP address of the NAT gateway                             |
| natgateway.floating_ip    | Body | String | Floating IP addresses for NAT gateways                            |
| natgateway.create_time    | Body | String | NAT gateway creation time (in UTC)                         |
| natgateway.description    | Body | String | NAT gateway descriptions                                    |
| natgateway.status         | Body | Enum | NAT gateway status<br>One of `ACTIVE`, `BUILD`, or `ERROR`. |


<details><summary>Example</summary>
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
### Delete a NAT gateway
Delete the specified NAT gateway.
```
DELETE /v2.0/natgateways/{NatGatewayId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| NatGatewayId | URL    | UUID   | O  | NAT Gateway ID       |
| tokenId | Header | String | O | Token ID |

#### Response
This API does not return a response body.

