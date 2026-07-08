
## Network > Colocation Gateway > API v2 Guide

NHN Cloud Network services use IaaS tokens for authentication and authorization when making API calls. The IaaS token is an authentication token used for NHN Cloud's OpenStack-based infrastructure services (IaaS). For more information on issuing and using IaaS tokens, please refer to the [IaaS Token](/nhncloud/en/public-api/iaas-token).

The Colocation Gateway API utilizes an endpoint of the`network` type. See the `serviceCatalog`in the token issuance response for the exact endpoint.

| Type | Region | Endpoint |
|---|---|---|
| network | Korea (Pangyo) Region<br>Korea (Pyeongchon) Region<br>Korea (Gwangju) Region | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

In each API response, you may find fields that are not specified within this guide. Those fields are for NHN Cloud internal usage, so refrain from using them because they may be changed without prior notice.

## Colocation Gateway

### View a list of colocation gateways

```
GET /v2.0/gateways/colocationgateways
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Colocation Gateway ID to retrieve |
| name | Query | String | - | Colocation gateway name to retrieve |
| vpc_id | Query | String | - | VPC ID associated with the colocation gateway to retrieve |


#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| colocationgateways | Body | Array | List of Colocation Gateway Information Objects |
| colocationgateways.id | Body | UUID | Colocation Gateway ID |
| colocationgateways.name | Body | String | Colocation gateway name |
| colocationgateways.vpc_id | Body | UUID | Connected VPC ID |
| colocationgateways.tenant_id | Body | String | Tenant ID |
| colocationgateways.status | Body | UUID | Resource Status |
| colocationgateways.description | Body | String | Colocation Gateway description |
| colocationgateways.vpc.name | Body | String | Connected VPC name |
| colocationgateways.vpc.id | Body | String | Connected VPC ID |
| colocationgateways.vpc.cidrv4 | Body | String | Connected VPC CIDR |

<details><summary>Example</summary>

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
### View colocation gateways

```
GET /v2.0/gateways/colocationgateways/{colocationGatewayId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| colocationGatewayId | URL | UUID | O | Colocation Gateway ID |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| colocationgateways | Body | Array | List of Colocation Gateway Information Objects |
| colocationgateways.id | Body | UUID | Colocation Gateway ID |
| colocationgateways.name | Body | String | Colocation gateway name |
| colocationgateways.vpc_id | Body | UUID | Connected VPC ID |
| colocationgateways.tenant_id | Body | String | Tenant ID |
| colocationgateways.status | Body | UUID | Resource Status |
| colocationgateways.description | Body | String | Colocation Gateway description |
| colocationgateways.vpc.name | Body | String | Connected VPC name |
| colocationgateways.vpc.id | Body | String | Connected VPC ID |
| colocationgateways.vpc.cidrv4 | Body | String | Connected VPC CIDR |

<details><summary>Example</summary>

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
