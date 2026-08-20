<!-- machine_translated: true -->

<!-- pre-align:aligned sig=0cdc970c9318 -->

<a id="network-transit-hub-api-v2-guide"></a>
## Network > Transit Hub > API v2 Guide { #network-transit-hub-api-v2-guide }

NHN Cloud Network services use IaaS tokens for authentication and authorization when making API calls. The IaaS token is an authentication token used for NHN Cloud's OpenStack-based infrastructure services (IaaS). For more information on issuing and using IaaS tokens, please refer to the [IaaS Token](/nhncloud/en/public-api/iaas-token).

For Transit Hub API, the `network` type endpoint is used. For more details, see `serviceCatalog` from the response of token issuance.

| Type | Region | Endpoint |
|---|---|---|
| network | Korea (Pangyo) Region<br>Korea (Pyeongchon) Region<br>Korea (Gwangju) Region | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

In each API response, you may find fields that are not specified within this guide. Those fields are for NHN Cloud internal usage, so refrain from using them because they may be changed without prior notice.

<a id="transit-hub"></a>
## Transit Hub { #transit-hub }

<a id="view-transit-hubs"></a>
### View Transit Hubs { #view-transit-hubs }

```
GET /v2.0/gateways/transithubs
X-Auth-Token: {tokenId}
```

<a id="view-transit-hubs-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Transit hub ID to query |
| String | Query | Token ID | - | Transit hub name to query |


<a id="view-transit-hubs-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithubs | String | nodegroups.uuid | List of transit hub information objects |
| transithubs.id | String | UUID | Transit Hub ID |
| transithubs.tenant_id | String | Token ID | Tenant ID |
| transithubs.name | String | Token ID | Transit Hub Name |
| transithubs.description | String | Token ID | Transit Hub description |
| transithubs.multicast_enable | String | Boolean | Whether to enable multicast feature |
| transithubs.default_association_enable | String | Boolean | Whether to enable the default routing table association feature |
| transithubs.default_propagation_enable | String | Boolean | Whether to enable the default routing table propagation feature |

<details><summary>Example</summary>

```json
{
  "transithubs": [
    {
      "status": "ACTIVE",
      "description": null,
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-12 22:19:05",
      "multicast_enable": true,
      "updated_at": "2024-02-12 22:19:05",
      "default_propagation_enable": true,
      "default_association_enable": true,
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "name": "thub"
    }
  ]
}
```
</details>

---
<a id="view-transit-hub"></a>
### View Transit Hub { #view-transit-hub }

```
GET /v2.0/gateways/transithubs/{transitHubId}
X-Auth-Token: {tokenId}
```

<a id="view-transit-hub-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transitHubId | O | UUID | Response | Transit Hub ID |

<a id="view-transit-hub-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub | String | Object | Transit hub information object |
| transithub.id | String | UUID | Transit Hub ID |
| transithub.tenant_id | String | Token ID | Tenant ID |
| transithub.name | String | Token ID | Transit Hub Name |
| transithub.description | String | Token ID | Transit Hub description |
| transithub.multicast_enable | String | Boolean | Whether to enable multicast feature |
| transithub.default_association_enable | String | Boolean | Whether to enable the default routing table association feature |
| transithub.default_propagation_enable | String | Boolean | Whether to enable the default routing table propagation feature |

<details><summary>Example</summary>

```json
{
  "transithub": {
    "status": "ACTIVE",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "multicast_enable": true,
    "updated_at": "2024-02-12 22:19:05",
    "default_propagation_enable": true,
    "default_association_enable": true,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub"
  }
}
```
</details>

---
<a id="create-transit-hub"></a>
### Create Transit Hub { #create-transit-hub }

```
POST /v2.0/gateways/transithubs
X-Auth-Token: {tokenId}
```

<a id="create-transit-hub-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub | String | Object | Response | Transit hub information object |
| transithub.name | String | Token ID | - | Transit Hub Name |
| transithub.description | String | Token ID | - | Transit Hub description |
| transithub.multicast_enable | String | Boolean | Response | Whether to enable multicast feature |
| transithub.default_association_enable | String | Boolean | Response | Whether to enable the default routing table association feature |
| transithub.default_propagation_enable | String | Boolean | Response | Whether to enable the default routing table propagation feature |




<details><summary>Example</summary>

```json
{
  "transithub": {
    "default_propagation_enable": true,
    "default_association_enable": true,
    "multicast_enable": true,
    "name": "thub",
    "description": "test"
  }
}
```
</details>

<a id="create-transit-hub-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub | String | Object | Transit hub information object |
| transithub.id | String | UUID | Transit Hub ID |
| transithub.tenant_id | String | Token ID | Tenant ID |
| transithub.name | String | Token ID | Transit Hub Name |
| transithub.description | String | Token ID | Transit Hub description |
| transithub.multicast_enable | String | Boolean | Whether to enable multicast feature |
| transithub.default_association_enable | String | Boolean | Whether to enable the default routing table association feature |
| transithub.default_propagation_enable | String | Boolean | Whether to enable the default routing table propagation feature |


<details><summary>Example</summary>

```json
{
  "transithub": {
    "status": "ACTIVE",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "multicast_enable": true,
    "updated_at": "2024-02-12 22:19:05",
    "default_propagation_enable": true,
    "default_association_enable": true,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub"
  }
}
```
</details>

---
<a id="modify-transit-hub"></a>
### Modify Transit Hub { #modify-transit-hub }

```
PUT /v2.0/gateways/transithubs/{transitHubId}
X-Auth-Token: {tokenId}
```

<a id="modify-transit-hub-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transitHubId | O | UUID | Response | Transit Hub ID |
| transithub | String | Object | Response | Transit hub information object |
| transithub.name | String | Token ID | - | Transit Hub Name |
| transithub.description | String | Token ID | - | Transit Hub description |

<details><summary>Example</summary>

```json
{
  "transithub": {
    "name": "thub1",
    "description": "test1"
  }
}
```
</details>

<a id="modify-transit-hub-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub | String | Object | Transit hub information object |
| transithub.id | String | UUID | Transit Hub ID |
| transithub.tenant_id | String | Token ID | Tenant ID |
| transithub.name | String | Token ID | Transit Hub Name |
| transithub.description | String | Token ID | Transit Hub description |
| transithub.multicast_enable | String | Boolean | Whether to enable multicast feature |
| transithub.default_association_enable | String | Boolean | Whether to enable the default routing table association feature |
| transithub.default_propagation_enable | String | Boolean | Whether to enable the default routing table propagation feature |


<details><summary>Example</summary>

```json
{
  "transithub": {
    "status": "ACTIVE",
    "description": "test1",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "multicast_enable": true,
    "updated_at": "2024-03-04 01:59:00.961621",
    "default_propagation_enable": true,
    "default_association_enable": true,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub1"
  }
}
```
</details>

---
<a id="delete-transit-hub"></a>
### Delete Transit Hub { #delete-transit-hub }

```
DELETE /v2.0/gateways/transithubs/{transitHubId}
X-Auth-Token: {tokenId}
```

<a id="delete-transit-hub-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transitHubId | O | UUID | Response | Transit Hub ID |


<a id="delete-transit-hub-response"></a>
#### Response
Stops the specified node group.










<a id="attachment"></a>
## Attachment { #attachment }

<a id="view-attachments"></a>
### View Attachments { #view-attachments }

```
GET /v2.0/gateways/transithub_attachments
X-Auth-Token: {tokenId}
```

<a id="view-attachments-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Attachment ID to query |
| String | Query | Token ID | - | Attachment name to query |
| Resource ID | Query | UUID | - | Resource ID to query (VPC) |
| subnet_id | Query | UUID | - | Subnet ID to query |
| transithub_id | Query | UUID | - | Transit hub ID to query |



<a id="view-attachments-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_attachments | String | nodegroups.uuid | List of attachment information objects |
| transithub_attachments.id | String | UUID | Attachment ID |
| transithub_attachments.tenant_id | String | Token ID | Tenant ID |
| transithub_attachments.name | String | Token ID | Attachment name |
| transithub_attachments.description | String | Token ID | Attachment description |
| transithub_attachments.resource_id | String | UUID | Resource ID (VPC) |
| transithub_attachments.subnet_id | String | UUID | Subnet ID |
| transithub_attachments.transithub_id | String | UUID | Transit Hub ID |

<details><summary>Example</summary>

```json
{
  "transithub_attachments": [
    {
      "status": "ACTIVE",
      "remote": false,
      "name": "thub-attachment",
      "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
      "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-13 01:22:09",
      "updated_at": "2024-02-13 01:22:11",
      "resource_cidr": "172.16.0.0/12",
      "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
      "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": null
    }
  ]
}
```
</details>

---
<a id="view-attachment"></a>
### View Attachment { #view-attachment }

```
GET /v2.0/gateways/transithub_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

<a id="view-attachment-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| attachmentId | O | UUID | Response | Attachment ID |

<a id="view-attachment-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_attachment | String | Object | Attachment information object  |
| transithub_attachment.id | String | UUID | Attachment ID |
| transithub_attachment.tenant_id | String | Token ID | Tenant ID |
| transithub_attachment.name | String | Token ID | Attachment name |
| transithub_attachment.description | String | Token ID | Attachment description |
| transithub_attachment.resource_id | String | UUID | Resource ID (VPC) |
| transithub_attachment.subnet_id | String | UUID | Subnet ID |
| transithub_attachment.transithub_id | String | UUID | Transit Hub ID |

<details><summary>Example</summary>

```json
{
  "transithub_attachment": {
    "status": "ACTIVE",
    "remote": false,
    "name": "thub-attachment",
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:09",
    "updated_at": "2024-02-13 01:22:11",
    "resource_cidr": "172.16.0.0/12",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
    "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": null
  }
}
```
</details>

---
<a id="create-attachment"></a>
### Create Attachment { #create-attachment }

```
POST /v2.0/gateways/transithub_attachments
X-Auth-Token: {tokenId}
```

<a id="create-attachment-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_attachment | String | Object | Response | Load Balancer Information object |
| transithub_attachment.name | String | Token ID | - | Attachment name |
| transithub_attachment.description | String | Token ID | - | Attachment description |
| transithub_attachment.resource_id | String | UUID | Response | Resource ID (VPC) |
| transithub_attachment.subnet_id | String | UUID | Response | Subnet ID |
| transithub_attachment.transithub_id | String | UUID | Response | Transit hub ID where the attachment will be registered |

<details><summary>Example</summary>

```json
{
  "transithub_attachment": {
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub-attachment",
    "description": null
  }
}
```
</details>

<a id="create-attachment-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_attachment | String | Object | Attachment information object  |
| transithub_attachment.id | String | UUID | Attachment ID |
| transithub_attachment.tenant_id | String | Token ID | Tenant ID |
| transithub_attachment.name | String | Token ID | Attachment name |
| transithub_attachment.description | String | Token ID | Attachment description |
| transithub_attachment.resource_id | String | UUID | Resource ID (VPC) |
| transithub_attachment.subnet_id | String | UUID | Subnet ID |
| transithub_attachment.transithub_id | String | UUID | Transit Hub ID |


<details><summary>Example</summary>

```json
{
  "transithub_attachment": {
    "status": "ACTIVE",
    "remote": false,
    "name": "thub-attachment",
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:09",
    "updated_at": "2024-02-13 01:22:11",
    "resource_cidr": "172.16.0.0/12",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
    "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": null
  }
}
```
</details>

---
<a id="modify-attachment"></a>
### Modify Attachment { #modify-attachment }

```
PUT /v2.0/gateways/transithub_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

<a id="modify-attachment-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| attachmentId | O | UUID | Response | Attachment ID |
| transithub_attachment | String | Object | Response | Attachment information object |
| transithub_attachment.name | String | Token ID | - | Attachment name |
| transithub_attachment.description | String | Token ID | - | Attachment description |

<details><summary>Example</summary>

```json
{
  "transithub_attachment": {
    "name": "thub-attachment1",
    "description": "test1"
  }
}
```
</details>

<a id="modify-attachment-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_attachment | String | Object | Attachment information object  |
| transithub_attachment.id | String | UUID | Attachment ID |
| transithub_attachment.tenant_id | String | Token ID | Tenant ID |
| transithub_attachment.name | String | Token ID | Attachment name |
| transithub_attachment.description | String | Token ID | Attachment description |
| transithub_attachment.resource_id | String | UUID | Resource ID (VPC) |
| transithub_attachment.subnet_id | String | UUID | Subnet ID |
| transithub_attachment.transithub_id | String | UUID | Transit Hub ID |


<details><summary>Example</summary>

```json
{
  "transithub_attachment": {
    "status": "ACTIVE",
    "remote": false,
    "name": "thub-attachment1",
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:09",
    "updated_at": "2024-02-13 01:22:11",
    "resource_cidr": "172.16.0.0/12",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
    "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "test1"
  }
}
```
</details>

---
<a id="delete-attachment"></a>
### Delete Attachment { #delete-attachment }

```
DELETE /v2.0/gateways/transithub_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

<a id="delete-attachment-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| attachmentId | O | UUID | Response | Attachment ID |


<a id="delete-attachment-response"></a>
#### Response
Stops the specified node group.










<a id="routing-table"></a>
## Routing Table { #routing-table }

<a id="view-routing-tables"></a>
### View Routing Tables { #view-routing-tables }

```
GET /v2.0/gateways/transithub_routing_tables
X-Auth-Token: {tokenId}
```

<a id="view-routing-tables-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Routing table ID to query |
| String | Query | Token ID | - | Routing table name to query |
| transithub_id | Query | UUID | - | Transit hub ID to query |



<a id="view-routing-tables-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_tables | String | nodegroups.uuid | List of routing table information objects |
| transithub_routing_tables.id | String | UUID | Routing table ID |
| transithub_routing_tables.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_tables.name | String | Token ID | Routing table name |
| transithub_routing_tables.description | String | Token ID | Routing table description |
| transithub_routing_tables.transithub_id | String | UUID | Transit Hub ID |
| transithub_routing_tables.default_table | String | Boolean | Whether routing table is default table |

<details><summary>Example</summary>

```json
{
  "transithub_routing_tables": [
    {
      "status": "ACTIVE",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-12 22:19:05",
      "updated_at": "2024-02-12 22:19:08",
      "default_table": true,
      "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "f5b96823-260a-415f-a162-d1914341137e",
      "name": "default-9d01afbb-0e"
    }
  ]
}
```
</details>

---
<a id="view-routing-table"></a>
### View Routing Table { #view-routing-table }

```
GET /v2.0/gateways/transithub_routing_tables/{routingTableId}
X-Auth-Token: {tokenId}
```

<a id="view-routing-table-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| routingTableId | O | UUID | Response | Routing table ID |

<a id="view-routing-table-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_table | String | Object | Routing table information object |
| transithub_routing_table.id | String | UUID | Routing table ID |
| transithub_routing_table.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_table.name | String | Token ID | Routing table name |
| transithub_routing_table.description | String | Token ID | Routing table description |
| transithub_routing_table.transithub_id | String | UUID | Transit Hub ID |
| transithub_routing_table.default_table | String | Boolean | Whether routing table is default table |

<details><summary>Example</summary>

```json
{
  "transithub_routing_table": {
    "status": "ACTIVE",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "updated_at": "2024-02-12 22:19:08",
    "default_table": true,
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "f5b96823-260a-415f-a162-d1914341137e",
    "name": "default-9d01afbb-0e"
  }
}
```
</details>

---
<a id="create-routing-table"></a>
### Create Routing Table { #create-routing-table }

```
POST /v2.0/gateways/transithub_routing_tables
X-Auth-Token: {tokenId}
```

<a id="create-routing-table-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_routing_table | String | Object | Response | Routing table information object |
| transithub_routing_table.name | String | Token ID | - | Routing table name |
| transithub_routing_table.description | String | Token ID | - | Routing table description |
| transithub_routing_table.transithub_id | String | UUID | Response | Transit hub ID where the routing table will be registered |

<details><summary>Example</summary>

```json
{
  "transithub_routing_table": {
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub-routing-table",
    "description": null
  }
}
```
</details>

<a id="create-routing-table-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_table | String | Object | Routing table information object |
| transithub_routing_table.id | String | UUID | Routing table ID |
| transithub_routing_table.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_table.name | String | Token ID | Routing table name |
| transithub_routing_table.description | String | Token ID | Routing table description |
| transithub_routing_table.transithub_id | String | UUID | Transit Hub ID |
| transithub_routing_table.default_table | String | Boolean | Whether routing table is default table |

<details><summary>Example</summary>

```json
{
  "transithub_routing_table": {
    "status": "BUILD",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-05 22:38:41",
    "updated_at": "2024-03-05 22:38:41",
    "default_table": false,
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "051eabf3-30f1-4e7a-a9bc-973c64f3c24a",
    "name": "thub-routing-table"
  }
}
```
</details>

---
<a id="modify-routing-table"></a>
### Modify Routing Table { #modify-routing-table }

```
PUT /v2.0/gateways/transithub_routing_tables/{routingTableId}
X-Auth-Token: {tokenId}
```

<a id="modify-routing-table-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| routingTableId | O | UUID | Response | Routing table ID |
| transithub_routing_table | String | Object | Response | Routing table information object |
| transithub_routing_table.name | String | Token ID | - | Routing table name |
| transithub_routing_table.description | String | Token ID | - | Routing table description |

<details><summary>Example</summary>

```json
{
  "transithub_routing_table": {
    "name": "thub-routing-table1",
    "description": "test"
  }
}
```
</details>

<a id="modify-routing-table-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_table | String | Object | Routing table information object |
| transithub_routing_table.id | String | UUID | Routing table ID |
| transithub_routing_table.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_table.name | String | Token ID | Routing table name |
| transithub_routing_table.description | String | Token ID | Routing table description |
| transithub_routing_table.transithub_id | String | UUID | Transit Hub ID |
| transithub_routing_table.default_table | String | Boolean | Whether routing table is default table |


<details><summary>Example</summary>

```json
{
  "transithub_routing_table": {
    "status": "ACTIVE",
    "description": "test",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-05 22:38:41",
    "updated_at": "2024-03-05 22:40:44.303417",
    "default_table": false,
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "051eabf3-30f1-4e7a-a9bc-973c64f3c24a",
    "name": "thub-routing-table1"
  }
}
```
</details>

---
<a id="delete-routing-table"></a>
### Delete Routing Table { #delete-routing-table }

```
DELETE /v2.0/gateways/transithub_routing_tables/{routingTableId}
X-Auth-Token: {tokenId}
```

<a id="delete-routing-table-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| routingTableId | O | UUID | Response | Routing table ID |


<a id="delete-routing-table-response"></a>
#### Response
Stops the specified node group.











<a id="routing-association"></a>
## Routing Association { #routing-association }

<a id="view-routing-associations"></a>
### View Routing Associations { #view-routing-associations }

```
GET /v2.0/gateways/transithub_routing_associations
X-Auth-Token: {tokenId}
```

<a id="view-routing-associations-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Routing association ID to query |
| attachment_id | Query | UUID | - | Attachment ID to query |
| routing_table_id | Query | UUID | - | Routing table ID to query |



<a id="view-routing-associations-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_associations | String | nodegroups.uuid | List of routing association information objects |
| transithub_routing_associations.id | String | UUID | Routing Association ID |
| transithub_routing_associations.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_associations.description | String | Token ID | Routing association description |
| transithub_routing_associations.attachment_id | String | UUID | Attachment ID |
| transithub_routing_associations.routing_table_id | String | UUID | Routing table ID |

<details><summary>Example</summary>

```json
{
  "transithub_routing_associations": [
    {
      "status": "ACTIVE",
      "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
      "created_at": "2024-02-13 01:22:09",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "56f5c3d2-2a9f-4ada-a358-356c6387de76",
      "updated_at": "2024-02-13 01:22:09"
    }
  ]
}
```
</details>

---
<a id="view-routing-association"></a>
### View Routing Association { #view-routing-association }

```
GET /v2.0/gateways/transithub_routing_associations/{routingAssociationId}
X-Auth-Token: {tokenId}
```

<a id="view-routing-association-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| routingAssociationId | O | UUID | Response | Routing Association ID |

<a id="view-routing-association-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_association | String | Object | Routing association information object |
| transithub_routing_association.id | String | UUID | Routing Association ID |
| transithub_routing_association.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_association.description | String | Token ID | Routing association description |
| transithub_routing_association.attachment_id | String | UUID | Attachment ID |
| transithub_routing_association.routing_table_id | String | UUID | Routing table ID |

<details><summary>Example</summary>

```json
{
  "transithub_routing_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-02-13 01:22:09",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "56f5c3d2-2a9f-4ada-a358-356c6387de76",
    "updated_at": "2024-02-13 01:22:09"
  }
}
```
</details>

---
<a id="create-routing-association"></a>
### Create Routing Association { #create-routing-association }

```
POST /v2.0/gateways/transithub_routing_associations
X-Auth-Token: {tokenId}
```

<a id="create-routing-association-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_routing_association | String | Object | Response | Routing association information object |
| transithub_routing_association.description | String | Token ID | - | Routing association description |
| transithub_routing_association.attachment_id | String | UUID | Response | Attachment ID |
| transithub_routing_association.routing_table_id | String | UUID | Response | Transit hub ID where the routing association will be registered |

<details><summary>Example</summary>

```json
{
  "transithub_routing_association": {
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49"
  }
}
```
</details>

<a id="create-routing-association-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_association | String | Object | Routing association information object |
| transithub_routing_association.id | String | UUID | Routing Association ID |
| transithub_routing_association.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_association.description | String | Token ID | Routing association description |
| transithub_routing_association.attachment_id | String | UUID | Attachment ID |
| transithub_routing_association.routing_table_id | String | UUID | Routing table ID |

<details><summary>Example</summary>

```json
{
  "transithub_routing_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-03-05 22:51:48",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "a5532ee9-1d7b-44bd-a622-85198171ee98",
    "updated_at": "2024-03-05 22:51:48"
  }
}
```
</details>

---
<a id="delete-routing-association"></a>
### Delete Routing Association { #delete-routing-association }

```
DELETE /v2.0/gateways/transithub_routing_associations/{routingAssociationId}
X-Auth-Token: {tokenId}
```

<a id="delete-routing-association-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| routingAssociationId | O | UUID | Response | Routing Association ID |


<a id="delete-routing-association-response"></a>
#### Response
Stops the specified node group.











<a id="routing-propagation"></a>
## Routing Propagation { #routing-propagation }

<!-- pre-align: ko에 대응 섹션 없음 — 검토 필요 (Heading text says 'View Routing Associations' but it is under 'Routing Propagation' (k63); k64 is '라우팅 전파 목록 보기' = 'View Routing Propagations'. The target wording copies the Routing Association heading and does not match the ko text, making it semantically incorrect — however it is matched to k64 as the positionally/structurally corresponding entry. No truly unmatched target heading exists here.) -->
<a id="routing-propagation-view-routing-associations"></a>
### View Routing Associations { #routing-propagation-view-routing-associations }

```
GET /v2.0/gateways/transithub_routing_propagations
X-Auth-Token: {tokenId}
```

<a id="routing-propagation-view-routing-associations-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Routing propagation ID to query |
| attachment_id | Query | UUID | - | Attachment ID to query |
| routing_table_id | Query | UUID | - | Routing table ID to query |



<a id="routing-propagation-view-routing-associations-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_propagations | String | nodegroups.uuid | List of routing propagation information objects |
| transithub_routing_propagations.id | String | UUID | Routing Propagation ID |
| transithub_routing_propagations.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_propagations.description | String | Token ID | Routing Propagation description |
| transithub_routing_propagations.attachment_id | String | UUID | Attachment ID |
| transithub_routing_propagations.routing_table_id | String | UUID | Routing table ID |

<details><summary>Example</summary>

```json
{
  "transithub_routing_propagations": [
    {
      "status": "ACTIVE",
      "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
      "created_at": "2024-02-13 01:22:09",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "6bf0efaa-6d32-4fef-a341-7662e9bf1eb1",
      "updated_at": "2024-02-13 01:22:09"
    }
  ]
}
```
</details>

---
<a id="view-routing-propagation"></a>
### View Routing propagation { #view-routing-propagation }

```
GET /v2.0/gateways/transithub_routing_propagations/{routingPropagationId}
X-Auth-Token: {tokenId}
```

<a id="view-routing-propagation-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| routingPropagationId | O | UUID | Response | Routing Propagation ID |

<a id="view-routing-propagation-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_propagation | String | Object | Routing propagation information object |
| transithub_routing_propagation.id | String | UUID | Routing Propagation ID |
| transithub_routing_propagation.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_propagation.description | String | Token ID | Routing Propagation description |
| transithub_routing_propagation.attachment_id | String | UUID | Attachment ID |
| transithub_routing_propagation.routing_table_id | String | UUID | Routing table ID |

<details><summary>Example</summary>

```json
{
  "transithub_routing_propagation": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-02-13 01:22:09",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "6bf0efaa-6d32-4fef-a341-7662e9bf1eb1",
    "updated_at": "2024-02-13 01:22:09"
  }
}
```
</details>

---
<a id="create-routing-propagation"></a>
### Create Routing Propagation { #create-routing-propagation }

```
POST /v2.0/gateways/transithub_routing_propagations
X-Auth-Token: {tokenId}
```

<a id="create-routing-propagation-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_routing_propagation | String | Object | Response | Routing propagation information object |
| transithub_routing_propagation.description | String | Token ID | - | Routing Propagation description |
| transithub_routing_propagation.attachment_id | String | UUID | Response | Attachment ID |
| transithub_routing_propagation.routing_table_id | String | UUID | Response | Transit hub ID where the routing propagation will be registered |

<details><summary>Example</summary>

```json
{
  "transithub_routing_propagation": {
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49"
  }
}
```
</details>

<a id="create-routing-propagation-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_propagation | String | Object | Routing propagation information object |
| transithub_routing_propagation.id | String | UUID | Routing Propagation ID |
| transithub_routing_propagation.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_propagation.description | String | Token ID | Routing Propagation description |
| transithub_routing_propagation.attachment_id | String | UUID | Attachment ID |
| transithub_routing_propagation.routing_table_id | String | UUID | Routing table ID |

<details><summary>Example</summary>

```json
{
  "transithub_routing_propagation": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-03-05 22:56:58",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "d1b54e63-0032-44dc-bb31-22d5723782ee",
    "updated_at": "2024-03-05 22:56:58.825231"
  }
}
```
</details>

---
<a id="delete-routing-propagation"></a>
### Delete Routing Propagation { #delete-routing-propagation }

```
DELETE /v2.0/gateways/transithub_routing_propagations/{routingPropagationId}
X-Auth-Token: {tokenId}
```

<a id="delete-routing-propagation-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| routingPropagationId | O | UUID | Response | Routing Propagation ID |


<a id="delete-routing-propagation-response"></a>
#### Response
Stops the specified node group.











<a id="routing-rule"></a>
## Routing Rule { #routing-rule }

<a id="view-routing-rules"></a>
### View Routing Rules { #view-routing-rules }

```
GET /v2.0/gateways/transithub_routing_rules
X-Auth-Token: {tokenId}
```

<a id="view-routing-rules-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Routing rule ID to query |
| Endpoint stage ID | Query | Enum | - | Routing rule action to query<br>One of `FORWARD`, `BLACKHOLE`  |
| rule_type | Query | Enum | - | Routing rule type to query<br>Either `STATIC` or `PROPAGATED`  |
| attachment_id | Query | UUID | - | Attachment ID to query |
| routing_table_id | Query | UUID | - | Routing table ID to query |



<a id="view-routing-rules-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_rules | String | nodegroups.uuid | List of routing rule information objects |
| transithub_routing_rules.id | String | UUID | Routing Rule ID |
| transithub_routing_rules.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_rules.description | String | Token ID | Routing rule description |
| transithub_routing_rules.cidr | String | Token ID | Routing rule IP band |
| transithub_routing_rules.action | String | Enum | Routing rule action<br>One of `FORWARD`, `BLACKHOLE`  |
| transithub_routing_rules.rule_type | String | Enum | Routing rule type<br>Either `STATIC` or `PROPAGATED`  |
| transithub_routing_rules.attachment_id | String | UUID | Attachment ID |
| transithub_routing_rules.routing_table_id | String | UUID | Routing table ID |
| transithub_routing_rules.propagation_id | String | UUID | Routing propagation ID, used when routing type `is PROPAGATED`by propagation |

<details><summary>Example</summary>

```json
{
  "transithub_routing_rules": [
    {
      "status": "ACTIVE",
      "rule_type": "PROPAGATED",
      "attachment_id": "ea9bb603-893c-4955-a7bb-64b6438a6f5b",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-12 22:35:48",
      "updated_at": "2024-02-12 22:35:48",
      "action": "FORWARD",
      "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
      "cidr": "172.16.0.0/12",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "propagation_id": "7a5d3159-a3a6-495b-bb0f-522c4d8a9933",
      "id": "3d10d565-8813-4c3c-9f1c-1af96eee9f14"
    }
  ]
}
```
</details>

---
<a id="view-routing-rule"></a>
### View routing rule { #view-routing-rule }

```
GET /v2.0/gateways/transithub_routing_rules/{routingRuleId}
X-Auth-Token: {tokenId}
```

<a id="view-routing-rule-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| routingRuleId | O | UUID | Response | Routing Rule ID |

<a id="view-routing-rule-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_rule | String | Object | Routing rule information object |
| transithub_routing_rule.id | String | UUID | Routing Rule ID |
| transithub_routing_rule.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_rule.description | String | Token ID | Routing rule description |
| transithub_routing_rule.cidr | String | Token ID | Routing rule IP band |
| transithub_routing_rule.action | String | Enum | Routing rule action<br>One of `FORWARD`, `BLACKHOLE`  |
| transithub_routing_rule.rule_type | String | Enum | Routing rule type<br>Either `STATIC` or `PROPAGATED`  |
| transithub_routing_rule.attachment_id | String | UUID | Attachment ID |
| transithub_routing_rule.routing_table_id | String | UUID | Routing table ID |
| transithub_routing_rule.propagation_id | String | UUID | Routing propagation ID, used when routing type `is PROPAGATED`by propagation |

<details><summary>Example</summary>

```json
{
  "transithub_routing_rule": {
    "status": "ACTIVE",
    "rule_type": "PROPAGATED",
    "attachment_id": "ea9bb603-893c-4955-a7bb-64b6438a6f5b",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:35:48",
    "updated_at": "2024-02-12 22:35:48",
    "action": "FORWARD",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "cidr": "172.16.0.0/12",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "propagation_id": "7a5d3159-a3a6-495b-bb0f-522c4d8a9933",
    "id": "3d10d565-8813-4c3c-9f1c-1af96eee9f14"
  }
}
```
</details>

---
<a id="create-routing-rule"></a>
### Create Routing Rule { #create-routing-rule }

```
POST /v2.0/gateways/transithub_routing_rules
X-Auth-Token: {tokenId}
```

<a id="create-routing-rule-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_routing_rule | String | Object | Response | Routing rule information object |
| transithub_routing_rule.name | String | Token ID | - | Routing rule name |
| transithub_routing_rule.description | String | Token ID | - | Routing rule description |
| transithub_routing_rule.cidr | String | Token ID | Response | Routing rule IP band |
| transithub_routing_rule.action | String | Enum | - | Routing rule action<br>One of `FORWARD`, `BLACKHOLE` <br>If not entered, `FORWARD` |
| transithub_routing_rule.attachment_id | String | UUID | Response | Attachment ID |
| transithub_routing_rule.routing_table_id | String | UUID | Response | The routing table ID where the routing rule will be registered. |

<details><summary>Example</summary>

```json
{
  "transithub_routing_rule": {
    "routing_table_id": "e5cb6442-4b5d-4298-84e2-adc9289c650e",
    "cidr": "1.1.1.0/24",
    "attachment_id": "6489cee8-0b5f-4053-b72d-1aa8b2921962"
  }
}
```
</details>

<a id="create-routing-rule-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_routing_rule | String | Object | Routing rule information object |
| transithub_routing_rule.id | String | UUID | Routing Rule ID |
| transithub_routing_rule.tenant_id | String | Token ID | Tenant ID |
| transithub_routing_rule.description | String | Token ID | Routing rule description |
| transithub_routing_rule.cidr | String | Token ID | Routing rule IP band |
| transithub_routing_rule.action | String | Enum | Routing rule action<br>One of `FORWARD`, `BLACKHOLE`  |
| transithub_routing_rule.rule_type | String | Enum | Routing rule type<br>Either `STATIC` or `PROPAGATED`  |
| transithub_routing_rule.attachment_id | String | UUID | Attachment ID |
| transithub_routing_rule.routing_table_id | String | UUID | Routing table ID |
| transithub_routing_rule.propagation_id | String | UUID | Routing propagation ID, used when routing type `is PROPAGATED`by propagation |

<details><summary>Example</summary>

```json
{
  "transithub_routing_rule": {
    "status": "ACTIVE",
    "rule_type": "STATIC",
    "attachment_id": "6489cee8-0b5f-4053-b72d-1aa8b2921962",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-06 23:00:05",
    "updated_at": "2024-03-06 23:00:05",
    "action": "FORWARD",
    "routing_table_id": "e5cb6442-4b5d-4298-84e2-adc9289c650e",
    "cidr": "1.1.1.0/24",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "propagation_id": null,
    "id": "3f765a36-bd6a-450a-9e05-366ecb8446c3"
  }
}
```
</details>

---
<a id="delete-routing-rule"></a>
### Delete Routing Rule { #delete-routing-rule }

```
DELETE /v2.0/gateways/transithub_routing_rules/{routingRuleId}
X-Auth-Token: {tokenId}
```

<a id="delete-routing-rule-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| routingRuleId | O | UUID | Response | Routing Rule ID |


<a id="delete-routing-rule-response"></a>
#### Response
Stops the specified node group.












<a id="multicast-domain"></a>
## Multicast Domain { #multicast-domain }

<a id="view-multicast-domains"></a>
### View multicast domains { #view-multicast-domains }

```
GET /v2.0/gateways/transithub_multicast_domains
X-Auth-Token: {tokenId}
```

<a id="view-multicast-domains-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Multicast domain ID to query |
| String | Query | Token ID | - | Multicast domain name to query |
| transithub_id | Query | UUID | - | Transit hub ID to query |


<a id="view-multicast-domains-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_domains | String | nodegroups.uuid | Multicast domain information objects |
| transithub_multicast_domains.id | String | UUID | Multicast Domain ID |
| transithub_multicast_domains.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_domains.name | String | Token ID | Multicast domain name |
| transithub_multicast_domains.description | String | Token ID | Multicast domain description |
| transithub_multicast_domains.transithub_id | String | UUID | Transit Hub ID |

<details><summary>Example</summary>
  
```json
{
  "transithub_multicast_domains": [
    {
      "status": "ACTIVE",
      "description": null,
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-13 01:20:31",
      "updated_at": "2024-02-13 01:20:32",
      "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
      "name": "thub-domain"
    }
  ]
}
```
</details>

---
<a id="view-multicast-domain"></a>
### View Multicast Domain { #view-multicast-domain }

```
GET /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

<a id="view-multicast-domain-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| multicastDomainId | O | UUID | Response | Multicast Domain ID |

<a id="view-multicast-domain-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| String | O | Token ID | Token ID |
| transithub_multicast_domain | String | Object | Multicast domain information object |
| transithub_multicast_domain.name | String | Token ID | Multicast domain name |
| transithub_multicast_domain.description | String | Token ID | Multicast domain description |
| transithub_multicast_domain.transithub_id | String | UUID | Transit hub ID where multicast domain will be registered |

<details><summary>Example</summary>

```json
{
  "transithub_multicast_domain": {
    "status": "ACTIVE",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:20:31",
    "updated_at": "2024-02-13 01:20:32",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
    "name": "thub-domain"
  }
}
```
</details>



---
<a id="create-multicast-domain"></a>
### Create Multicast Domain { #create-multicast-domain }

```
POST /v2.0/gateways/transithub_multicast_domains
X-Auth-Token: {tokenId}
```

<a id="create-multicast-domain-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_multicast_domain | String | Object | Response | Multicast domain information object |
| transithub_multicast_domain.name | String | Token ID | - | Multicast domain name |
| transithub_multicast_domain.description | String | Token ID | - | Multicast domain description |
| transithub_multicast_domain.transithub_id | String | UUID | Response | Transit hub ID where multicast domain will be registered |

<details><summary>Example</summary>

```json
{
  "transithub_multicast_domain": {
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub-domain1"
  }
}
```
</details>

<a id="create-multicast-domain-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_domain | String | Object | Multicast domain information object |
| transithub_multicast_domain.id | String | UUID | Multicast Domain ID |
| transithub_multicast_domain.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_domain.name | String | Token ID | Multicast domain name |
| transithub_multicast_domain.description | String | Token ID | Multicast domain description |
| transithub_multicast_domain.transithub_id | String | UUID | Transit Hub ID |

<details><summary>Example</summary>

```json
{
  "transithub_multicast_domain": {
    "status": "BUILD",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-06 23:03:07",
    "updated_at": "2024-03-06 23:03:07",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "fba53b77-431b-466f-8a31-784942649e73",
    "name": "thub-domain1"
  }
}
```
</details>


---
<a id="modify-multicast-domain"></a>
### Modify Multicast Domain { #modify-multicast-domain }

```
PUT /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

<a id="modify-multicast-domain-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| multicastDomainId | O | UUID | Response | Multicast Domain ID |
| transithub_multicast_domain | String | Object | Response | Multicast domain information object |
| transithub_multicast_domain.name | String | Token ID | - | Multicast domain name |
| transithub_multicast_domain.description | String | Token ID | - | Multicast domain description |

<details><summary>Example</summary>

```json
{
  "transithub_multicast_domain": {
    "name": "thub-domain",
    "description": "test"
  }
}
```
</details>

<a id="modify-multicast-domain-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_domain | String | Object | Multicast domain information object |
| transithub_multicast_domain.id | String | UUID | Multicast Domain ID |
| transithub_multicast_domain.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_domain.name | String | Token ID | Multicast domain name |
| transithub_multicast_domain.description | String | Token ID | Multicast domain description |
| transithub_multicast_domain.transithub_id | String | UUID | Transit Hub ID |

<details><summary>Example</summary>

```json
{
  "transithub_multicast_domain": {
    "status": "ACTIVE",
    "description": "test",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-06 23:03:07",
    "updated_at": "2024-03-06 23:06:18.031473",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "fba53b77-431b-466f-8a31-784942649e73",
    "name": "thub-domain"
  }
}
```
</details>


---
<a id="delete-multicast-domain"></a>
### Delete Multicast Domain { #delete-multicast-domain }

```
DELETE /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

<a id="delete-multicast-domain-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| multicastDomainId | O | UUID | Response | Multicast Domain ID |


<a id="delete-multicast-domain-response"></a>
#### Response
Stops the specified node group.









<a id="multicast-association"></a>
## Multicast Association { #multicast-association }

<!-- pre-align: ko에 대응 섹션 없음 — 검토 필요 (Heading text says 'View multicast domains' but it is under 'Multicast Association' (t105); k106 is '멀티캐스트 연결 목록 보기' = 'View Multicast Associations'. The target wording copies the Multicast Domain heading and does not match the ko text — however it is matched to k106 as the positionally/structurally corresponding entry. No truly unmatched target heading exists here.) -->
<a id="multicast-association-view-multicast-domains"></a>
### View multicast domains { #multicast-association-view-multicast-domains }

```
GET /v2.0/gateways/transithub_multicast_associations
X-Auth-Token: {tokenId}
```

<a id="multicast-association-view-multicast-domains-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Multicast association ID to query |
| String | Query | Token ID | - | Multicast association name to query |
| domain_id | Query | UUID | - | Multicast domain ID to query |


<a id="multicast-association-view-multicast-domains-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_associations | String | nodegroups.uuid | Multicast association information objects |
| transithub_multicast_associations.id | String | UUID | Multicast association ID |
| transithub_multicast_associations.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_associations.description | String | Token ID | Multicast association description |
| transithub_multicast_associations.attachment_id | String | UUID | Attachment ID |
| transithub_multicast_associations.subnet_id | String | UUID | Subnet ID |
| transithub_multicast_associations.domain_id | String | UUID | Multicast Domain ID |

<details><summary>Example</summary>
  
```json
{
  "transithub_multicast_associations": [
    {
      "status": "ACTIVE",
      "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": "",
      "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-13 01:22:37",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "3da29ae0-f544-4b8e-88c4-eb2ef78d0214",
      "updated_at": "2024-02-13 01:22:37",
      "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
    }
  ]
}
```
</details>


---
<a id="view-multicast-association"></a>
### View Multicast Association { #view-multicast-association }

```
GET /v2.0/gateways/transithub_multicast_associations/{multicastAssociationId}
X-Auth-Token: {tokenId}
```

<a id="view-multicast-association-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| multicastAssociationId | O | UUID | Response | Routing Rule ID |

<a id="view-multicast-association-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| String | O | Token ID | Token ID |
| transithub_multicast_association | String | Object | Multicast association information object |
| transithub_multicast_association.id | String | UUID | Multicast association ID |
| transithub_multicast_association.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_association.description | String | Token ID | Multicast association description |
| transithub_multicast_association.attachment_id | String | UUID | Attachment ID |
| transithub_multicast_association.subnet_id | String | UUID | Subnet ID |
| transithub_multicast_association.domain_id | String | UUID | Multicast Domain ID |

<details><summary>Example</summary>

```json
{
  "transithub_multicast_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:37",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "3da29ae0-f544-4b8e-88c4-eb2ef78d0214",
    "updated_at": "2024-02-13 01:22:37",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
  }
}
```
</details>


---
<a id="create-multicast-association"></a>
### Create Multicast Association { #create-multicast-association }

```
POST /v2.0/gateways/transithub_multicast_associations
X-Auth-Token: {tokenId}
```

<a id="create-multicast-association-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_multicast_association | String | Object | Response | Multicast association information object |
| transithub_multicast_association.description | String | Token ID | - | Multicast association description |
| transithub_multicast_association.attachment_id | String | UUID | Response | Attachment ID |
| transithub_multicast_association.domain_id | String | UUID | Response | Multicast Domain ID |

<details><summary>Example</summary>

```json
{
  "transithub_multicast_association": {
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
  }
}
```
</details>

<a id="create-multicast-association-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_association | String | Object | Multicast association information object |
| transithub_multicast_association.id | String | UUID | Multicast association ID |
| transithub_multicast_association.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_association.description | String | Token ID | Multicast association description |
| transithub_multicast_association.attachment_id | String | UUID | Attachment ID |
| transithub_multicast_association.subnet_id | String | UUID | Subnet ID |
| transithub_multicast_association.domain_id | String | UUID | Multicast Domain ID |


<details><summary>Example</summary>

```json
{
  "transithub_multicast_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-07 00:22:59",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "4da8461b-6c92-4225-8368-60e1e49e3d92",
    "updated_at": "2024-03-07 00:22:59",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
  }
}
```
</details>

---
<a id="delete-multicast-association"></a>
### Delete Multicast Association { #delete-multicast-association }

```
DELETE /v2.0/gateways/transithub_multicast_associations/{multicastAssociationId}
X-Auth-Token: {tokenId}
```

<a id="delete-multicast-association-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| multicastAssociationId | O | UUID | Response | Multicast association ID |


<a id="delete-multicast-association-response"></a>
#### Response
Stops the specified node group.
















<a id="multicast-group"></a>
## Multicast Group { #multicast-group }

<a id="view-multicast-group"></a>
### View multicast group { #view-multicast-group }

```
GET /v2.0/gateways/transithub_multicast_groups
X-Auth-Token: {tokenId}
```

<a id="view-multicast-group-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Multicast group ID to query |
| String | Query | Token ID | - | Multicast group name to query |
| domain_id | Query | UUID | - | Multicast group ID to query |


<a id="view-multicast-group-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_groups | String | nodegroups.uuid | Multicast group information objects |
| transithub_multicast_groups.id | String | UUID | Multicast Group ID |
| transithub_multicast_groups.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_groups.description | String | Token ID | Multicast group description |
| transithub_multicast_groups.association_id | String | UUID | Multicast association ID |
| transithub_multicast_groups.ipaddress | String | Token ID | Multicast group IP address |
| transithub_multicast_groups.member_type | String | Token ID | Multicast member type |
| transithub_multicast_groups.source_type | String | Token ID | Multicast source type |
| transithub_multicast_groups.port_id | String | UUID | Multicast destination port ID |

<details><summary>Example</summary>
  
```json
{
  "transithub_multicast_groups": [
    {
      "description": "",
      "updated_at": "2024-03-07 00:28:20",
      "member_type": "STATIC",
      "source_type": null,
      "port_id": "b0ca1c15-13e1-4746-b8e1-9ec8e685d228",
      "ipaddress": "224.0.0.3",
      "id": "ce8c5fef-6859-4e68-8b46-4cd395c44b37",
      "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-03-07 00:28:20",
      "domain_id": "27d79c71-ccce-4928-af3c-5ffa5c3ed3fd",
      "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b"
    }
  ]
}
```
</details>

---
<a id="multicast-group-view-multicast-group"></a>
### View Multicast Group { #multicast-group-view-multicast-group }

```
GET /v2.0/gateways/transithub_multicast_groups/{multicastGroupId}
X-Auth-Token: {tokenId}
```

<a id="multicast-group-view-multicast-group-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| multicastGroupId | O | UUID | Response | Multicast Group ID |

<a id="multicast-group-view-multicast-group-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_group | String | Object | Multicast group information object |
| transithub_multicast_group.id | String | UUID | Multicast Group ID |
| transithub_multicast_group.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_group.description | String | Token ID | Multicast group description |
| transithub_multicast_group.association_id | String | UUID | Multicast association ID |
| transithub_multicast_group.ipaddress | String | Token ID | Multicast group IP address |
| transithub_multicast_group.member_type | String | Token ID | Multicast member type |
| transithub_multicast_group.source_type | String | Token ID | Multicast source type |
| transithub_multicast_group.port_id | String | UUID | Multicast destination port ID |

<details><summary>Example</summary>

```json
{
  "transithub_multicast_group": {
    "description": "",
    "updated_at": "2024-03-07 00:28:20",
    "member_type": "STATIC",
    "source_type": null,
    "port_id": "b0ca1c15-13e1-4746-b8e1-9ec8e685d228",
    "ipaddress": "224.0.0.3",
    "id": "ce8c5fef-6859-4e68-8b46-4cd395c44b37",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-07 00:28:20",
    "domain_id": "27d79c71-ccce-4928-af3c-5ffa5c3ed3fd",
    "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b"
  }
}
```
</details>

---
<a id="create-multicast-group"></a>
### Create Multicast Group { #create-multicast-group }

```
POST /v2.0/gateways/transithub_multicast_groups
X-Auth-Token: {tokenId}
```

<a id="create-multicast-group-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_multicast_group | String | Object | Response | Multicast group information object |
| transithub_multicast_group.description | String | Token ID | - | Multicast group description |
| transithub_multicast_group.association_id | String | UUID | Response | Multicast association ID |
| transithub_multicast_group.ipaddress | String | Token ID | Response | Multicast group IP address |
| transithub_multicast_group.member_type | String | Token ID | - | Multicast member type, enter `STATIC` if used as a member<br>Must enter one of the member type and source type |
| transithub_multicast_group.source_type | String | Token ID | - | Multicast source type, enter `STATIC` if used as a source<br>Must enter one of the member type and source type |
| transithub_multicast_group.port_id | String | UUID | Response | Multicast destination port ID |


<details><summary>Example</summary>

```json
{
  "transithub_multicast_group": {
    "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
    "port_id": "b0ca1c15-13e1-4746-b8e1-9ec8e685d228",
    "ipaddress": "224.0.0.10",
    "member_type": "STATIC"
  }
}
```
</details>

<a id="create-multicast-group-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_group | String | Object | Multicast group information object |
| transithub_multicast_group.id | String | UUID | Multicast Group ID |
| transithub_multicast_group.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_group.description | String | Token ID | Multicast group description |
| transithub_multicast_group.association_id | String | UUID | Multicast association ID |
| transithub_multicast_group.ipaddress | String | Token ID | Multicast group IP address |
| transithub_multicast_group.member_type | String | Token ID | Multicast member type |
| transithub_multicast_group.source_type | String | Token ID | Multicast source type |
| transithub_multicast_group.port_id | String | UUID | Multicast destination port ID |


<details><summary>Example</summary>

```json
{
  "transithub_multicast_group": {
    "description": "",
    "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-07 00:40:19",
    "updated_at": "2024-03-07 00:40:19",
    "member_type": "STATIC",
    "domain_id": "27d79c71-ccce-4928-af3c-5ffa5c3ed3fd",
    "source_type": null,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "ipaddress": "224.0.0.10",
    "id": "91b281f8-41ab-4d27-8639-da27b23d21db"
  }
}
```
</details>


---
<a id="delete-multicast-group"></a>
### Delete Multicast Group { #delete-multicast-group }

```
DELETE /v2.0/gateways/transithub_multicast_groups/{multicastGroupId}
X-Auth-Token: {tokenId}
```

<a id="delete-multicast-group-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| multicastGroupId | O | UUID | Response | Multicast Group ID |


<a id="delete-multicast-group-response"></a>
#### Response
Stops the specified node group.







<a id="share-transit-hub"></a>
## Share Transit Hub { #share-transit-hub }

<a id="view-sharing-allowed-list"></a>
### View Sharing Allowed List { #view-sharing-allowed-list }

```
GET /v2.0/gateways/transithub_allow_projects
X-Auth-Token: {tokenId}
```

<a id="view-sharing-allowed-list-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Sharing allowed information ID to query |
| transithub_id | Query | UUID | - | Transit hub ID to query |


<a id="view-sharing-allowed-list-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_allow_projects | String | nodegroups.uuid | Sharing allowed information list |
| transithub_allow_projects.id | String | UUID | Sharing allowed information ID |
| transithub_allow_projects.tenant_id | String | Token ID | Tenant ID |
| transithub_allow_projects.transithub_id | String | UUID | Transit hub ID to share |
| transithub_allow_projects.transithub_name | String | Token ID | Transit Hub Name |
| transithub_allow_projects.target_project_id | String | UUID | Tenant ID to share with |

<details><summary>Example</summary>
  
```json
{
  "transithub_allow_projects": [
    {
      "target_project_id": "cd29a534a15e46049b968dd0835b129b",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "transithub_name": "thub1",
      "transithub_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "186717d3-8e26-40ec-ad00-67a8463ccc4c"
    }
  ]
}
```
</details>

---
<a id="create-sharing-allowed-information"></a>
### Create sharing allowed information { #create-sharing-allowed-information }

```
POST /v2.0/gateways/transithub_allow_projects
X-Auth-Token: {tokenId}
```

<a id="create-sharing-allowed-information-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_allow_project | String | Object | Response | Share sharing allowed information object |
| transithub_allow_project.transithub_id | String | UUID | Response | Transit hub ID to share |
| transithub_allow_project.target_project_id | String | UUID | Response | Tenant ID to share with |


<details><summary>Example</summary>

```json
{
  "transithub_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "transithub_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c"
  }
}
```
</details>

<a id="create-sharing-allowed-information-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_allow_project | String | Object | Share sharing allowed information object |
| transithub_allow_project.id | String | UUID | Sharing allowed information ID |
| transithub_allow_project.tenant_id | String | Token ID | Tenant ID |
| transithub_allow_project.transithub_id | String | UUID | Transit hub ID to share |
| transithub_allow_project.transithub_name | String | Token ID | Transit Hub Name |
| transithub_allow_project.target_project_id | String | UUID | Tenant ID to share with |


<details><summary>Example</summary>

```json
{
  "transithub_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "transithub_name": "dj-thub1",
    "transithub_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "3d962640-385f-4874-8766-aa1b4480e7e4"
  }
}
```
</details>


---
<a id="delete-sharing-allowed-information"></a>
### Delete Sharing Allowed Information { #delete-sharing-allowed-information }

```
DELETE /v2.0/gateways/transithub_allow_projects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="delete-sharing-allowed-information-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| allowProjectId | O | UUID | Response | Sharing allowed information ID |


<a id="delete-sharing-allowed-information-response"></a>
#### Response
Stops the specified node group.



<a id="view-shared-list"></a>
### View Shared List { #view-shared-list }

```
GET /v2.0/gateways/transithub_shared_lists
X-Auth-Token: {tokenId}
```

<a id="view-shared-list-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_id | Query | UUID | - | Transit hub ID to query |


<a id="view-shared-list-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_shared_lists | String | nodegroups.uuid | Shared information list |
| transithub_shared_lists.id | String | UUID | Shared Information ID |
| transithub_shared_lists.tenant_id | String | Token ID | Tenant ID |
| transithub_shared_lists.transithub_id | String | UUID | Shared Transit Hub ID |
| transithub_shared_lists.transithub_name | String | Token ID | Shared transit hub name |
| transithub_shared_lists.transithub_project_id | String | UUID | Tenant ID of the shared transit hub |

<details><summary>Example</summary>
  
```json
{
  "transithub_shared_lists": [
    {
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "transithub_project_id": "1fb0cf13afb341b699f74bbbecab2117",
      "transithub_name": "thub",
      "transithub_id": "4050efd6-b6cc-4e2d-9402-dd5e1520872f",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "51c8fd9c-ae82-474f-9664-9fc31c77a563"
    }
  ]
}
```
</details>







<a id="share-multicast-domain"></a>
## Share Multicast Domain { #share-multicast-domain }

<a id="share-multicast-domain-view-sharing-allowed-list"></a>
### View Sharing Allowed List { #share-multicast-domain-view-sharing-allowed-list }

```
GET /v2.0/gateways/transithub_multicast_domain_allow_projects
X-Auth-Token: {tokenId}
```

<a id="share-multicast-domain-view-sharing-allowed-list-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| id | Query | UUID | - | Sharing allowed information ID to query |
| domain_id | Query | UUID | - | Multicast domain ID to query |


<a id="share-multicast-domain-view-sharing-allowed-list-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_domain_allow_projects | String | nodegroups.uuid | Sharing allowed information list |
| transithub_multicast_domain_allow_projects.id | String | UUID | Sharing allowed information ID |
| transithub_multicast_domain_allow_projects.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_domain_allow_projects.domain_id | String | UUID | Multicast domain ID to share |
| transithub_multicast_domain_allow_projects.domain_name | String | Token ID | Multicast domain name |
| transithub_multicast_domain_allow_projects.target_project_id | String | UUID | Tenant ID to share with |

<details><summary>Example</summary>
  
```json
{
  "transithub_multicast_domain_allow_projects": [
    {
      "target_project_id": "cd29a534a15e46049b968dd0835b129b",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "domain_name": "domain1",
      "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "186717d3-8e26-40ec-ad00-67a8463ccc4c"
    }
  ]
}
```
</details>

---
<a id="share-multicast-domain-create-sharing-allowed-information"></a>
### Create Sharing Allowed Information { #share-multicast-domain-create-sharing-allowed-information }

```
POST /v2.0/gateways/transithub_multicast_domain_allow_projects
X-Auth-Token: {tokenId}
```

<a id="share-multicast-domain-create-sharing-allowed-information-request"></a>
#### Request

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| transithub_multicast_domain_allow_project | String | Object | Response | Share sharing allowed information object |
| transithub_multicast_domain_allow_project.domain_id | String | UUID | Response | Multicast domain ID to share |
| transithub_multicast_domain_allow_project.target_project_id | String | UUID | Response | Tenant ID to share with |


<details><summary>Example</summary>

```json
{
  "transithub_multicast_domain_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "domain_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c"
  }
}
```
</details>

<a id="share-multicast-domain-create-sharing-allowed-information-response"></a>
#### Response

| Format | Description | Description | Header |
|---|---|---|---|
| transithub_multicast_domain_allow_project | String | Object | Share sharing allowed information object |
| transithub_multicast_domain_allow_project.id | String | UUID | Sharing allowed information ID |
| transithub_multicast_domain_allow_project.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_domain_allow_project.domain_id | String | UUID | Multicast domain ID to share |
| transithub_multicast_domain_allow_project.domain_name | String | Token ID | Multicast domain name |
| transithub_multicast_domain_allow_project.target_project_id | String | UUID | Tenant ID to share with |


<details><summary>Example</summary>

```json
{
  "transithub_multicast_domain_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "domain_name": "domain1",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "3d962640-385f-4874-8766-aa1b4480e7e4"
  }
}
```
</details>


---
<a id="share-multicast-domain-delete-sharing-allowed-information"></a>
### Delete Sharing Allowed Information { #share-multicast-domain-delete-sharing-allowed-information }

```
DELETE /v2.0/gateways/transithub_multicast_domain_allow_projects/{allowProjectId}
X-Auth-Token: {tokenId}
```

<a id="share-multicast-domain-delete-sharing-allowed-information-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| allowProjectId | O | UUID | Response | Sharing allowed information ID |


<a id="share-multicast-domain-delete-sharing-allowed-information-response"></a>
#### Response
Stops the specified node group.



<a id="share-multicast-domain-view-shared-list"></a>
### View Shared List { #share-multicast-domain-view-shared-list }

```
GET /v2.0/gateways/transithub_multicast_domain_shared_lists
X-Auth-Token: {tokenId}
```

<a id="share-multicast-domain-view-shared-list-request"></a>
#### Request
This API does not require a request body.

| Format | Description | Description | tokenId | Header |
|---|---|---|---|---|
| String | O | Token ID | Response | Token ID |
| domain_id | Query | UUID | - | Multicast domain ID to query |


<a id="share-multicast-domain-view-shared-list-response"></a>
#### Response

| Format | Type | Description | Header |
|---|---|---|---|
| transithub_multicast_domain_shared_lists | String | nodegroups.uuid | Shared information list |
| transithub_multicast_domain_shared_lists.id | String | UUID | Shared Information ID |
| transithub_multicast_domain_shared_lists.tenant_id | String | Token ID | Tenant ID |
| transithub_multicast_domain_shared_lists.domain_id | String | UUID | Shared multicast domain ID  |
| transithub_multicast_domain_shared_lists.domain_name | String | Token ID | Shared multicast domain name |
| transithub_multicast_domain_shared_lists.domain_project_id | String | UUID | Tenant ID of the shared multicast domain |

<details><summary>Example</summary>
  
```json
{
  "transithub_multicast_domain_shared_lists": [
    {
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "domain_project_id": "1fb0cf13afb341b699f74bbbecab2117",
      "domain_name": "domain1",
      "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "51c8fd9c-ae82-474f-9664-9fc31c77a563"
    }
  ]
}
```
</details>
