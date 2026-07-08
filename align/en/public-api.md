## Network > Security Groups > API v2 Guide

NHN Cloud Network services use IaaS tokens for authentication and authorization when making API calls. The IaaS token is an authentication token used for NHN Cloud's OpenStack-based infrastructure services (IaaS). For more information on issuing and using IaaS tokens, please refer to the [IaaS Token](/nhncloud/en/public-api/iaas-token).

Security Group API uses the `network` type endpoint. To see the accurate endpoint, refer to `serviceCatalog` of the token issuance response.

| Type | Region                                                                      | Endpoint                                                                                                                                                                                                                                                                                                           |
|---|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| network | Korea(Pangyo) Region<br>Korea(Pyeongchon) Region<br>Korea (Gwangju) Region<br>Japan(Tokyo) Region | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com<br>https://jp1-api-network-infrastructure.nhncloudservice.com|

API response may show the fields not specified by the guide. These fields are internally used by NHN Cloud, and not used because they are subject to change without prior notice.


## Security group
### See the list of security groups
```
GET /v2.0/security-groups
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Security group ID to view |
| tenant_id | Query | String | - | Tenant ID of the security group to view |
| name | Query | String | - | Security group name to view |
| sort_dir | Query | Enum | - | Sort direction of the security group to view<br>`Sorted by the field specified by sort_key`<br>**asc** or **desc** |
| sort_key | Query | String | - | Sort key of the security group to view<br>`Sorted by the direction specified by sort_dir` |
| fields | Query | String | - | Field name of the security group to view<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_groups | Body | Array | List of security groups object |
| security_groups.tenant_id | Body | String | Tenant ID |
| security_groups.description | Body | String | Security group description |
| security_groups.id | Body | UUID | Security group ID |
| security_groups.security_group_rules | Body | Array | List of security group rules |
| security_groups.name | Body | String | Security group name |

<details><summary>Example</summary>
<p>

```json
{
  "security_groups": [
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "description": "Default security group",
      "id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "security_group_rules": [
        {
          "direction": "ingress",
          "protocol": null,
          "description": "",
          "port_range_max": null,
          "id": "0c7279cd-657e-43cd-a635-6886ca3a8acd",
          "remote_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "remote_ip_prefix": null,
          "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
          "port_range_min": null,
          "ethertype": "IPv4"
        },
        {
          "direction": "egress",
          "protocol": null,
          "description": "",
          "port_range_max": null,
          "id": "4c5ae06e-44f0-4ea9-a999-29473873bca2",
          "remote_group_id": null,
          "remote_ip_prefix": null,
          "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
          "port_range_min": null,
          "ethertype": "IPv6"
        },
        {
          "direction": "egress",
          "protocol": null,
          "description": "",
          "port_range_max": null,
          "id": "4e21389a-bb3c-469c-8139-29da582bc3c5",
          "remote_group_id": null,
          "remote_ip_prefix": null,
          "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
          "port_range_min": null,
          "ethertype": "IPv4"
        },
        {
          "direction": "ingress",
          "protocol": null,
          "description": "",
          "port_range_max": null,
          "id": "72af180f-c425-4ec4-b7a3-90f86d4ce145",
          "remote_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "remote_ip_prefix": null,
          "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
          "port_range_min": null,
          "ethertype": "IPv6"
        }
      ],
      "name": "default"
    }
  ]
}
```

</p>
</details>

---

### See the security groups
```
GET /v2.0/security-groups/{securityGroupId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Example | Required | Description |
|---|---|---|---|---|
| securityGroupId | Query | UUID | O | Security group ID to view |
| tokenId | Header | String | O | Token ID |
| fields | Query | String | - | Field name of the security group to view<br>Only the specified fields are returned in the response<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Example | Description |
|---|---|---|---|
| security_group | Body | Object | Security group object |
| security_group.tenant_id | Body | String | Tenant ID |
| security_group.description | Body | String | Security group description |
| security_group.id | Body | UUID | Security group ID |
| security_group.security_group_rules | Body | Array | List of security group rules |
| security_group.name | Body | String | Security group name |

<details><summary>Example</summary>
<p>

```json
{
  "security_group": {
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "description": "Default security group",
    "id": "877b092c-2a31-4509-8d23-deeb02d95633",
    "security_group_rules": [
      {
        "direction": "ingress",
        "protocol": null,
        "description": "",
        "port_range_max": null,
        "id": "0c7279cd-657e-43cd-a635-6886ca3a8acd",
        "remote_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "remote_ip_prefix": null,
        "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv4"
      },
      {
        "direction": "egress",
        "protocol": null,
        "description": "",
        "port_range_max": null,
        "id": "4c5ae06e-44f0-4ea9-a999-29473873bca2",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv6"
      },
      {
        "direction": "egress",
        "protocol": null,
        "description": "",
        "port_range_max": null,
        "id": "4e21389a-bb3c-469c-8139-29da582bc3c5",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv4"
      }
      {
        "direction": "ingress",
        "protocol": null,
        "description": "",
        "port_range_max": null,
        "id": "72af180f-c425-4ec4-b7a3-90f86d4ce145",
        "remote_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "remote_ip_prefix": null,
        "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv6"
      }
    ],
    "name": "default"
  }
}
```

</p>
</details>

---

### Creating a security group

Create a new security group. Newly created security groups include the egress security group rules by default.

```
POST /v2.0/security-groups
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| security_group | Body | Object | O | Object requesting creation of security group |
| description | Body | String | - | Security group description |
| name | Body | String | - | Security group name |

<details><summary>Example</summary>
<p>

```json
{
    "security_group": {
        "name": "webservers",
        "description": "security group for webservers"
    }
}
```

</p>
</details>

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group | Body | Object | Security group object |
| security_group.tenant_id | Body | String | Tenant ID |
| security_group.description | Body | String | Security group description |
| security_group.id | Body | UUID | Security group ID |
| security_group.security_group_rules | Body | Array | List of security group rules |
| security_group.name | Body | String | Security group name |

<details><summary>Example</summary>
<p>

```json
{
  "security_group": {
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "description": "security group for webservers",
    "id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
    "security_group_rules": [
      {
        "direction": "egress",
        "protocol": null,
        "description": null,
        "port_range_max": null,
        "id": "057e031a-ec2a-4bee-859a-6bc1d88c57d0",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv4"
      },
      {
        "direction": "egress",
        "protocol": null,
        "description": null,
        "port_range_max": null,
        "id": "cd37d4a7-75ac-4246-95cf-e93b37b75a9f",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv6"
      }
    ],
    "name": "webservers"
  }
}
```

</p>
</details>

---

### Modifying a security group
Modify an existing security group
```
PUT /v2.0/security-groups/{securityGroupId}
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| securityGroupId | URL | UUID | O | Security group ID |
| security_group | Body | Object | O | Object requesting modification of security group |
| description | Body | String | - | Security group description |
| name | Body | String | - | Security group name |

<details><summary>예시</summary>
<p>

```json
{
    "security_group": {
        "name": "new-webservers",
        "description": "security group for new webservers"
    }
}
```

</p>
</details>

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group | Body | Object | Security group object |
| security_group.tenant_id | Body | String | Tenant ID |
| security_group.description | Body | String | Security group description |
| security_group.id | Body | UUID | Security group ID |
| security_group.security_group_rules | Body | Array | List of security group rules |
| security_group.name | Body | String | Security group name |

<details><summary>Example</summary>
<p>

```json
{
  "security_group": {
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "description": "security group for new webservers",
    "id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
    "security_group_rules": [
      {
        "direction": "egress",
        "protocol": null,
        "description": null,
        "port_range_max": null,
        "id": "057e031a-ec2a-4bee-859a-6bc1d88c57d0",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv4"
      },
      {
        "direction": "egress",
        "protocol": null,
        "description": null,
        "port_range_max": null,
        "id": "cd37d4a7-75ac-4246-95cf-e93b37b75a9f",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv6"
      }
    ],
    "name": "new-webservers"
  }
}
```

</p>
</details>

---

### Deleting a security group
Delete a specified security group
```
DELETE /v2.0/security-groups/{securityGroupId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| securityGroupId | URL | UUID | O | Security group ID |
| tokenId | Header | String | O | Token ID |

#### Response
This API does not return a response body.

---

## Security rules
### See the list of security rules
```
GET /v2.0/security-group-rules
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Security rule ID to view |
| remote_group_id | Query | UUID | - | Remote security group ID of the security rule to view |
| protocol | Query | String | - | Protocol of the security rule to view |
| direction | Query | Enum | - | Direction of packet to which the security rule to view is applied<br>**ingress** or **egress** |
| ethertype | Query | Enum | - | Network traffic of the security rule to view `Ethertype` value<br>**IPv4** or **IPv6** |
| port_range_max | Query | Integer | - | Maximum port range of the security rule to view |
| port_range_min | Query | Integer | - | Minimum port range of the security rule to view |
| security_group_id | Query | UUID | - | Security group ID containing the security rule to view |
| tenant_id | Query | String | - | Tenant ID of the security rule to view |
| remote_ip_prefix | Query | String | - | Destination IP prefix of the security rule to view |
| description | Query | String | - | Description of the security rule to view |
| sort_dir | Query | Enum | - | Sort direction of the security rule to view<br>`Sorted by the field specified by sort_key`<br>**asc** or **desc** |
| sort_key | Query | String | - | Sort key of the security rule to view<br>`Sorted in the direction specified by sort_dir` |
| fields | Query | String | - | Field name of the security rule to view<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group_rules | Body | Array | List of security rule objects |
| security_group_rules.direction | Body | Enum | Direction of packet to which the security rule is applied<br>**ingress** or **egress** |
| security_group_rules.ethertype | Body | Enum | Network traffic of the security rule `Ethertype` value<br>**IPv4** or **IPv6** |
| security_group_rules.protocol | Body | String | Protocol name of the security rule |
| security_group_rules.description | Body | String | Security rule description |
| security_group_rules.port_range_max | Body | Integer | Maximum port range of the security rule |
| security_group_rules.port_range_min | Body | Integer | Minimum port range of the security rule |
| security_group_rules.remote_group_id | Body | UUID | Remote security group ID of the security rule |
| security_group_rules.remote_ip_prefix | Body | Enum | Destination IP prefix of the security rule |
| security_group_rules.security_group_id | Body | UUID | Security group ID containing the security rule |
| security_group_rules.tenant_id | Body | String | Tenant ID |
| security_group_rules.id | Body | UUID | Security rule ID |

<details><summary>Example</summary>
<p>

```json
{
  "security_group_rules": [
    {
      "direction": "ingress",
      "protocol": "tcp",
      "description": "",
      "port_range_max": 65535,
      "id": "8eb7775f-1193-472a-98bd-e0599f94a64d",
      "remote_group_id": null,
      "remote_ip_prefix": "0.0.0.0/0",
      "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "port_range_min": 1,
      "ethertype": "IPv4"
    }
  ]
}
```

</p>
</details>

---

### See the security rules
```
GET /v2.0/security-group-rules/{securityGroupRuleId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| securityGroupRuleId | URL | UUID | O | Security rule ID |
| tokenId | Header | String | O | Token ID |
| fields | Query | String | - | Field name of the security rule to view<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group_rule | Body | Object | Security rule object |
| security_group_rule.direction | Body | Enum | Direction of packet to which the security rule is applied<br>**ingress** or **egress** |
| security_group_rule.ethertype | Body | Enum | Network traffic of the security rule `Ethertype` value<br>**IPv4** or **IPv6** |
| security_group_rule.protocol | Body | String | Protocol name of the security rule |
| security_group_rule.description | Body | String | Security rule description |
| security_group_rule.port_range_max | Body | Integer | Maximum port range of the security rule to view |
| security_group_rule.port_range_min | Body | Integer | Minimum port range of the security rule to view |
| security_group_rule.remote_group_id | Body | UUID | Remote security group ID of the security rule |
| security_group_rule.remote_ip_prefix | Body | Enum | Destination IP prefix of the security rule |
| security_group_rule.security_group_id | Body | UUID | Security group ID containing the security rule |
| security_group_rule.tenant_id | Body | String | Tenant ID |
| security_group_rule.id | Body | UUID | Security rule ID |

<details><summary>Example</summary>
<p>

```json
{
  "security_group_rule": {
    "direction": "ingress",
    "protocol": "tcp",
    "description": "",
    "port_range_max": 65535,
    "id": "8eb7775f-1193-472a-98bd-e0599f94a64d",
    "remote_group_id": null,
    "remote_ip_prefix": "0.0.0.0/0",
    "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "port_range_min": 1,
    "ethertype": "IPv4"
  }
}
```

</p>
</details>

---

### Creating a security rule

Create a new security group rule. You can create a security rule for IPv4 only.

```
POST /v2.0/security-group-rules
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| security_group_rule | Body | Object | O | Object requesting creation of security group |
| security_group_rule.remote_group_id | Body | UUID | - | Remote security group ID of the security rule |
| security_group_rule.direction | Body | Enum | O | Direction of packet to which the security rule is applied<br>**ingress**, **egress** |
| security_group_rule.ethertype | Body | Enum | - | Set to `IPv4`. Specified as `IPv4` if omitted |
| security_group_rule.protocol | Body | String | - | Protocol name of the security rule. Applied to all protocols if omitted. |
| security_group_rule.port_range_max | Body | Integer | - | Maximum port range of the security rule |
| security_group_rule.port_range_min | Body | Integer | - | Minimum port range of the security rule |
| security_group_rule.security_group_id | Body | UUID | O | Security group ID containing the security rule |
| security_group_rule.remote_ip_prefix | Body | Enum | - | Destination IP prefix of the security rule |
| security_group_rule.description | Body | String | - | Security rule description |

<details><summary>Example</summary>
<p>

```json
{
    "security_group_rule": {
        "direction": "ingress",
        "port_range_min": "80",
        "ethertype": "IPv4",
        "port_range_max": "80",
        "protocol": "tcp",
        "remote_group_id": "85cc3048-abc3-43cc-89b3-377341426ac5",
        "security_group_id": "a7734e61-b545-452d-a3cd-0189cbd9747a"
    }
}
```

</p>
</details>

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group_rule | Body | Object | Security rule object |
| security_group_rule.direction | Body | Enum | Direction of packet to which the security rule is applied<br>**ingress** or **egress** |
| security_group_rule.ethertype | Body | Enum | Network traffic of the security rule `Ethertype` value<br>**IPv4** or **IPv6** |
| security_group_rule.protocol | Body | String | Protocol name of the security rule |
| security_group_rule.description | Body | String | Security rule description |
| security_group_rule.port_range_max | Body | Integer | Maximum port range of the security rule to view |
| security_group_rule.port_range_min | Body | Integer | Minimum port range of the security rule to view |
| security_group_rule.remote_group_id | Body | UUID | Remote security group ID of the security rule |
| security_group_rule.remote_ip_prefix | Body | Enum | Destination IP prefix of the security rule |
| security_group_rule.security_group_id | Body | UUID | Security group ID containing the security rule |
| security_group_rule.tenant_id | Body | String | Tenant ID |
| security_group_rule.id | Body | UUID | Security rule ID |

<details><summary>Example</summary>
<p>

```json
{
  "security_group_rule": {
    "direction": "ingress",
    "protocol": "tcp",
    "description": "",
    "port_range_max": 65535,
    "id": "8eb7775f-1193-472a-98bd-e0599f94a64d",
    "remote_group_id": null,
    "remote_ip_prefix": "0.0.0.0/0",
    "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "port_range_min": 1,
    "ethertype": "IPv4"
  }
}
```

</p>
</details>

---

### Deleting a security rule
Delete a specified security rule
```
DELETE /v2.0/security-group-rules/{securityGroupRuleId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| securityGroupRuleId | URL | UUID | O | Security rule ID |
| tokenId | Header | String | O | Token ID |

#### Response
This API does not return a response body.

---

## Connection information
### View the list of the connection information
```
GET /v2.0/security-group-ports
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description                                                                         |
|---|---|---|----|----------------------------------------------------------------------------|
| tokenId | Header | String | O  | Token ID                                                                      |
| security_group_id | Query | UUID | O  | Security group ID to query                                                               |
| tenant_id | Query | String | -  | Tenant ID of security group to query                                                          |
| sort_dir | Query | Enum | -  | Sorting direction of security group to query<br>Sort by the field specified in `sort_key`<br>One of **asc** and **desc** |
| sort_key | Query | String | -  | Sorting key of security group to query<br>Sort by the direction specified in `sort_dir`                                |
| fields | Query | String | -  | Field name of security group to query<br>Example: `fields=id&fields=name`                             |

#### Response

| Name                                   | Type | Format | Description                                          |
|--------------------------------------|---|---|---------------------------------------------|
| security_group_ports                 | Body | Array | List of connection port information objects                             |
| security_group_ports.id              | Body | UUID | ID of connection port                                   |
| security_group_ports.name            | Body | String | Connection port name                                    |
| security_group_ports.status          | Body | Enum | Connection port status<br>Among `ACTIVE`, `BUILD`, and `DOWN`. |
| security_group_ports.admin_state_up  | Body | Boolean | Admin control status of port                            |
| security_group_ports.network_id      | Body | UUID |  Network ID of connection port                              |
| security_group_ports.tenant_id       | Body | String | Tenant ID of connection port                               |
| security_group_ports.project_id      | Body | String | Project ID of connection port. Same as tenant ID.                 |
| security_group_ports.device_owner    | Body | String | Resource type ussing connection port                          |
| security_group_ports.device_id       | Body | UUID | Resource ID using connection port                          |
| security_group_ports.mac_address     | Body | String | MAC address of connection port                               |
| security_group_ports.fixed_ips       | Body | Array | Static IP list of connection ports                             |
| security_group_ports.security_groups | Body | Array | Security group ID list configured on connection port                      |


<details><summary>Example</summary>
<p>

```json
{
  "security_group_ports": [
    {
      "status": "ACTIVE",
      "name": "",
      "admin_state_up": true,
      "network_id": "1031cd94-425a-4d23-9833-d7f19de30c1e",
      "tenant_id": "76841f7d054a40b88b2a99828280998c",
      "device_owner": "compute:kr-pub-a",
      "mac_address": "fa:16:3e:08:3f:e9",
      "project_id": "71843f7d054a20b88b2a97628270998c",
      "fixed_ips": [
        {
          "subnet_id": "f70ae850-3f8a-4fab-9b57-926871bd2c27",
          "ip_address": "192.168.10.91"
        }
      ],
      "id": "54ad4dfb-8fcb-413c-ad9c-dc381d1a93e2",
      "security_groups": [
        "22156aef-48c8-4ecd-9b29-83f28cad3bcb",
        "564e8224-7d50-4865-b044-4fbb89c5e911"
      ],
      "device_id": "418ce9ea-752e-4f4e-9c72-5a32479ee85a"
    }
  ]
}

```

</p>
</details>

