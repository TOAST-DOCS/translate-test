<a id="network-traffic-mirroring-api-v2-guide"></a>
## Network > Traffic Mirroring > API v2 Guide { #network-traffic-mirroring-api-v2-guide }

NHN Cloud Network services use IaaS tokens for authentication and authorization when making API calls. The IaaS token is an authentication token used for NHN Cloud's OpenStack-based infrastructure services (IaaS). For more information on issuing and using IaaS tokens, please refer to the [IaaS Token](/nhncloud/en/public-api/iaas-token).

The Mirroring API uses a `network` type endpoint. For the exact endpoint, refer to `serviceCatalog` in the token issuance response.

| Type | Region | Endpoint |
| --- | --- | ----- |
| network | Korea (Pangyo) Region <br>Korea (Pyeongchon) Region <br>Korea (Gwangju) Region | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

API responses may contain fields not specified in the guide. The fields are used internally by NHN Cloud and are subject to change without notice, so they are not used.

<a id="mirroring-session-session"></a>
## Mirroring Session (Session) { #mirroring-session-session }

A session is a unit that mirrors traffic from a source port to a target port. If needed, you can link one or more filter groups to mirror only specific traffic.

<a id="view-session-lists"></a>
### View Session Lists { #view-session-lists }

```
GET /v2.0/mirroring/sessions
X-Auth-Token: {tokenId}
```

<a id="view-session-lists-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Session ID to query |
| tenant\_id | Query | String | - | Tenant ID |
| name | Query | String | - | Session name |
| direction | Query | Enum | - | One of `in`, `out`, `both` |
| sort\_dir | Query | Enum | - | Sorting direction. One of `asc`, `desc` |
| sort\_key | Query | String | - | Sort criteria field |
| fields | Query | String | - | Fields to include in the response. e.g. `fields=id&fields=name` |

<a id="view-session-lists-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| sessions | Body | Array | List of session objects |
| sessions.id | Body | UUID | Session ID |
| sessions.name | Body | String | Session name |
| sessions.description | Body | String | Description |
| sessions.target\_port\_id | Body | UUID | Target port ID |
| sessions.source\_port\_id | Body | UUID | Source port ID |
| sessions.filter\_groups | Body | Array[UUID] | List of connected filter group IDs |
| sessions.direction | Body | Enum | One of `in`, `out`, or `both` |
| sessions.tenant\_id | Body | String | Tenant ID |
| sessions.project\_id | Body | String | Project ID, same as tenant ID |
| sessions.target\_network\_id | Body | UUID | Network ID of target port |
| sessions.source\_network\_id | Body | UUID | Network ID of the source port |
| sessions.vni | Body | Number | Mirroring tunnel VNI |
| sessions.status | Body | Enum | Session status: `ACTIVE`, `BUILD`, `ERROR` |
| sessions.created\_at | Body | String | Creation time (UTC) |
| sessions.updated\_at | Body | String | Modification time (UTC) |

Example

```json
{
  "sessions": [
    {
      "id": "7b0b5e6f-9a75-4b5a-9d69-0fb6a6d8e111",
      "name": "mirror-sess-1",
      "description": "",
      "target_port_id": "c0a8012b-7f6d-4c16-951d-cca31af20c01",
      "source_port_id": "5d5b1ce7-9a68-4f3d-9c0d-2e6b5b9a1c02",
      "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
      "direction": "both",
      "tenant_id": "76841f7d054a40b88b2a99828280998c",
      "project_id": "76841f7d054a40b88b2a99828280998c",
      "target_network_id": "a2a9b0f0-1d75-4b3b-b3a1-5a1d2f3e4b55",
      "source_network_id": "b3b0f0a2-2e86-4c4c-a1b3-6c2d3e4f5a66",
      "vni": 5001001,
      "status": "ACTIVE",
      "created_at": "2025-08-29 05:25:30",
      "updated_at": "2025-08-29 05:25:30"
    }
  ]
}
```

***

<a id="view-sessions"></a>
### View Sessions { #view-sessions }

```
GET /v2.0/mirroring/sessions/{SessionId}
X-Auth-Token: {tokenId}
```

<a id="view-sessions-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| SessionId | URL | UUID | O | Session ID |
| tokenId | Header | String | O | Token ID |
| fields | Query | String | - | Fields to include in the response. e.g. `fields=id&fields=name` |

<a id="view-sessions-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| session | Body | Object | Session object |
| session.id | Body | UUID | Session ID |
| session.name | Body | String | Session name |
| session.description | Body | String | Description |
| session.target\_port\_id | Body | UUID | Target port ID |
| session.source\_port\_id | Body | UUID | Source port ID |
| session.filter\_groups | Body | Array[UUID] | List of connected filter group IDs |
| session.direction | Body | Enum | One of `in`, `out`, or `both` |
| session.tenant\_id | Body | String | Tenant ID |
| session.project\_id | Body | String | Project ID |
| session.target\_network\_id | Body | UUID | Target port's network ID |
| session.source\_network\_id | Body | UUID | Source port's network ID |
| session.vni | Body | Number | Tunnel VNI |
| session.status | Body | Enum | `ACTIVE`, `BUILD`, `ERROR` |
| session.created\_at | Body | String | Creation time (UTC) |
| session.updated\_at | Body | String | Modification time (UTC) |

Example

```json
{
  "session": {
    "id": "7b0b5e6f-9a75-4b5a-9d69-0fb6a6d8e111",
    "name": "mirror-sess-1",
    "description": "",
    "target_port_id": "c0a8012b-7f6d-4c16-951d-cca31af20c01",
    "source_port_id": "5d5b1ce7-9a68-4f3d-9c0d-2e6b5b9a1c02",
    "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
    "direction": "both",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c",
    "target_network_id": "a2a9b0f0-1d75-4b3b-b3a1-5a1d2f3e4b55",
    "source_network_id": "b3b0f0a2-2e86-4c4c-a1b3-6c2d3e4f5a66",
    "vni": 5001001,
    "status": "ACTIVE",
    "created_at": "2025-08-29 05:25:30",
    "updated_at": "2025-08-29 05:25:30"
  }
}
```

***

<a id="create-sessions"></a>
### Create Sessions { #create-sessions }

```
POST /v2.0/mirroring/sessions
X-Auth-Token: {tokenId}
```

<a id="create-sessions-request"></a>
#### Request

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | Token ID |
| session | Body | Object | O | Session creation request object |
| session.name | Body | String | - | Session name (up to 32 characters, alphanumeric characters/`-`/`_`) |
| session.description | Body | String | - | Description (up to 255 characters) |
| session.target\_port\_id | Body | UUID | O | Target port ID |
| session.source\_port\_id | Body | UUID | O | Source port ID |
| session.filter\_groups | Body | Array[UUID] | - | List of filter group IDs to connect to. If none are present, all traffic will be mirrored. |
| session.direction | Body | Enum | O | One of `in`, `out`, or `both` |
| session.tenant\_id | Body | String | O | Tenant ID |
| session.project\_id | Body | String | O | Project ID |

Example

```json
{
  "session": {
    "name": "mirror-sess-1",
    "description": "",
    "target_port_id": "c0a8012b-7f6d-4c16-951d-cca31af20c01",
    "source_port_id": "5d5b1ce7-9a68-4f3d-9c0d-2e6b5b9a1c02",
    "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
    "direction": "both",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c"
  }
}
```

<a id="create-sessions-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| session | Body | Object | Session object |
| session.id | Body | UUID | Session ID |
| session.status | Body | Enum | Initially, mainly `BUILD` |
| Other | Body | - | Same as the session view |

Example

```json
{
  "session": {
    "id": "7b0b5e6f-9a75-4b5a-9d69-0fb6a6d8e111",
    "name": "mirror-sess-1",
    "description": "",
    "target_port_id": "c0a8012b-7f6d-4c16-951d-cca31af20c01",
    "source_port_id": "5d5b1ce7-9a68-4f3d-9c0d-2e6b5b9a1c02",
    "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
    "direction": "both",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c",
    "target_network_id": "a2a9b0f0-1d75-4b3b-b3a1-5a1d2f3e4b55",
    "source_network_id": "b3b0f0a2-2e86-4c4c-a1b3-6c2d3e4f5a66",
    "vni": 5001001,
    "status": "BUILD",
    "created_at": "2025-08-29 05:25:30",
    "updated_at": "2025-08-29 05:25:30"
  }
}
```

***

<a id="modify-sessions"></a>
### Modify Sessions { #modify-sessions }

```
PUT /v2.0/mirroring/sessions/{SessionId}
X-Auth-Token: {tokenId}
```

You can modify description, name, direction, and filter group list only. Changing ports is not supported.

<a id="modify-sessions-request"></a>
#### Request

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| SessionId | URL | UUID | O | Session ID |
| tokenId | Header | String | O | Token ID |
| session | Body | Object | O | Include only the fields to be modified |
| session.name | Body | String | - | Session name |
| session.description | Body | String | - | Description |
| session.filter\_groups | Body | Array[UUID] | - | List of filter group IDs |
| session.direction | Body | Enum | - | `in`, `out`, `both` |

Example

```json
{
  "session": {
    "name": "mirror-sess-1b",
    "description": "update",
    "filter_groups": ["2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10"],
    "direction": "in"
  }
}
```

<a id="modify-sessions-response"></a>
#### Response

Same as the session view response.

***

<a id="delete-sessions"></a>
### Delete Sessions { #delete-sessions }

```
DELETE /v2.0/mirroring/sessions/{SessionId}
X-Auth-Token: {tokenId}
```

<a id="delete-sessions-request"></a>
#### Request

This API does not request a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| SessionId | URL | UUID | O | Session ID |
| tokenId | Header | String | O | Token ID |

<a id="delete-sessions-response"></a>
#### Response

This API does not return a response body.

***

<a id="mirroring-filter-group-filtergroup"></a>
## Mirroring Filter Group (filtergroup) { #mirroring-filter-group-filtergroup }

A filter group is a container that groups one or more filters. You can connect them to a session to mirror only specific traffic.

<a id="view-a-list-of-filter-groups"></a>
### View a List of Filter Groups { #view-a-list-of-filter-groups }

```
GET /v2.0/mirroring/filtergroups
X-Auth-Token: {tokenId}
```

<a id="view-a-list-of-filter-groups-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Filter Group ID |
| tenant\_id | Query | String | - | Tenant ID |
| name | Query | String | - | Name |
| sort\_dir | Query | Enum | - | `asc`, `desc` |
| sort\_key | Query | String | - | Sort Key |
| fields | Query | String | - | Fields to Include |

<a id="view-a-list-of-filter-groups-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| filtergroups | Body | Array | List of filter groups |
| filtergroups.id | Body | UUID | ID |
| filtergroups.name | Body | String | Name |
| filtergroups.description | Body | String | Description |
| filtergroups.tenant\_id | Body | String | Tenant ID |
| filtergroups.project\_id | Body | String | Project ID |
| filtergroups.filters | Body | Array | List of filter objects/IDs within the group |
| filtergroups.created\_at | Body | String | Creation time (UTC) |
| filtergroups.updated\_at | Body | String | Modification time (UTC) |

Example

```json
{
  "filtergroups": [
    {
      "id": "2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10",
      "name": "fg-1",
      "description": "",
      "tenant_id": "76841f7d054a40b88b2a99828280998c",
      "project_id": "76841f7d054a40b88b2a99828280998c",
      "filters": [],
      "created_at": "2025-08-29 05:20:00",
      "updated_at": "2025-08-29 05:20:00"
    }
  ]
}
```

***

<a id="view-filter-groups"></a>
### View Filter Groups { #view-filter-groups }

```
GET /v2.0/mirroring/filtergroups/{FilterGroupId}
X-Auth-Token: {tokenId}
```

<a id="view-filter-groups-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | Yes | Token ID |
| id | URL | UUID | Yes | Filter Group ID |

<a id="view-filter-groups-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| filtergroup | Body | Object | List of filter groups |
| filtergroup.id | Body | UUID | ID |
| filtergroup.name | Body | String | Name |
| filtergroup.description | Body | String | Description |
| filtergroup.tenant\_id | Body | String | Tenant ID |
| filtergroup.project\_id | Body | String | Project ID |
| filtergroup.filters | Body | Array | List of filter objects/IDs within the group |
| filtergroup.created\_at | Body | String | Creation Time (UTC) |
| filtergroup.updated\_at | Body | String | Modification Time (UTC) |

***

<a id="create-filter-groups"></a>
### Create Filter Groups { #create-filter-groups }

```
POST /v2.0/mirroring/filtergroups
X-Auth-Token: {tokenId}
```

<a id="create-filter-groups-request"></a>
#### Request

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | Token ID |
| filtergroup | Body | Object | O | Filter group creation request object |
| filtergroup.name | Body | String | - | Name (up to 32 characters, English letters/numbers/`-`/`_`) |
| filtergroup.description | Body | String | - | Description (up to 255 characters) |
| filtergroup.tenant\_id | Body | String | O | Tenant ID |
| filtergroup.project\_id | Body | String | O | Project ID |

Example

```json
{
  "filtergroup": {
    "name": "fg-1",
    "description": "",
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c"
  }
}
```

<a id="create-filter-groups-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| filtergroup | Body | Object | Filter group object |
| filtergroup.id | Body | UUID | ID |
| filtergroup.name | Body | String | Name |
| filtergroup.description | Body | String | Description |
| filtergroup.tenant\_id | Body | String | Tenant ID |
| filtergroup.project\_id | Body | String | Project ID |
| filtergroup.filters | Body | Array | List of filter objects/IDs in the group |
| filtergroup.created\_at | Body | String | Creation time (UTC) |
| filtergroup.updated\_at | Body | String | Modification time (UTC) |

***

<a id="modify-filter-groups"></a>
### Modify Filter Groups { #modify-filter-groups }

```
PUT /v2.0/mirroring/filtergroups/{FilterGroupId}
X-Auth-Token: {tokenId}
```

Name and description only can be modified.

<a id="modify-filter-groups-request"></a>
#### Request

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| FilterGroupId | URL | UUID | Yes | Filter Group ID |
| tokenId | Header | String | Yes | Token ID |
| filtergroup | Body | Object | Yes | Include only fields to modify |
| filtergroup.name | Body | String | - | Name |
| filtergroup.description | Body | String | - | Description |

<a id="modify-filter-groups-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| filtergroup | Body | Object | Filter Group Object |
| filtergroup.id | Body | UUID | ID |
| filtergroup.name | Body | String | Name |
| filtergroup.description | Body | String | Description |
| filtergroup.tenant\_id | Body | String | Tenant ID |
| filtergroup.project\_id | Body | String | Project ID |
| filtergroup.filters | Body | Array | List of filter objects/IDs within the group |
| filtergroup.created\_at | Body | String | Creation time (UTC) |
| filtergroup.updated\_at | Body | String | Modification time (UTC) |

***

<a id="delete-filter-groups"></a>
### Delete Filter Groups { #delete-filter-groups }

```
DELETE /v2.0/mirroring/filtergroups/{FilterGroupId}
X-Auth-Token: {tokenId}
```

<a id="delete-filter-groups-requestresponse"></a>
#### Request/Response

No request body. No response body.

***

<a id="mirroring-filter-filter"></a>
## Mirroring Filter (filter) { #mirroring-filter-filter }

A filter consists of matching conditions and actions, and is used to allow (`accept`) or exclude (`drop`) specific traffic. A filter must belong to a specific filter group.

<a id="view-filter-lists"></a>
### View Filter Lists { #view-filter-lists }

```
GET /v2.0/mirroring/filters
X-Auth-Token: {tokenId}
```

<a id="view-filter-lists-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Filter ID |
| filter\_group\_id | Query | UUID | - | Filter Group ID |
| tenant\_id | Query | String | - | Tenant ID |
| sort\_dir | Query | Enum | - | `asc`, `desc` |
| sort\_key | Query | String | - | Sort Key |
| fields | Query | String | - | Fields to Include |

<a id="view-filter-lists-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| filters | Body | Array | Filter List |
| filters.id | Body | UUID | Filter ID |
| filters.description | Body | String | Description |
| filters.filter\_group\_id | Body | UUID | Filter group ID |
| filters.src\_cidr | Body | CIDR | Source CIDR. Optional |
| filters.dst\_cidr | Body | CIDR | Destination CIDR. Optional |
| filters.src\_port\_range\_min | Body | Number | Start of source port range |
| filters.src\_port\_range\_max | Body | Number | End of source port range |
| filters.dst\_port\_range\_min | Body | Number | Start of destination port range |
| filters.dst\_port\_range\_max | Body | Number | End of destination port range |
| filters.protocol | Body | String | `tcp`, `udp`, `icmp`, or null |
| filters.action | Body | Enum | `accept`, `drop` |
| filters.priority | Body | Number | Priority (default 101) |
| filters.tenant\_id | Body | String | Tenant ID |
| filters.project\_id | Body | String | Project ID |
| filters.created\_at | Body | String | Creation Time (UTC) |
| filters.updated\_at | Body | String | Modification Time (UTC) |

Example

```json
{
  "filters": [
    {
      "id": "f1e2d3c4-b5a6-7890-1234-56789abcde01",
      "description": "allow tcp 80 to 10.0.0.0/24",
      "filter_group_id": "2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10",
      "src_cidr": null,
      "dst_cidr": "10.0.0.0/24",
      "src_port_range_min": null,
      "src_port_range_max": null,
      "dst_port_range_min": 80,
      "dst_port_range_max": 80,
      "protocol": "tcp",
      "action": "accept",
      "priority": 101,
      "tenant_id": "76841f7d054a40b88b2a99828280998c",
      "project_id": "76841f7d054a40b88b2a99828280998c",
      "created_at": "2025-08-29 05:22:00",
      "updated_at": "2025-08-29 05:22:00"
    }
  ]
}
```

***

<a id="view-filters"></a>
### View Filters { #view-filters }

```
GET /v2.0/mirroring/filters/{FilterId}
X-Auth-Token: {tokenId}
```

<a id="view-filters-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | Yes | Token ID |
| id | Query | URL | Yes | Filter ID |

<a id="view-filters-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| filter | Body | Object | Filter List |
| filter.id | Body | UUID | Filter ID |
| filter.description | Body | String | Description |
| filter.filter\_group\_id | Body | UUID | Filter Group ID |
| filter.src\_cidr | Body | CIDR | Source CIDR. Optional |
| filter.dst\_cidr | Body | CIDR | Destination CIDR. Optional |
| filter.src\_port\_range\_min | Body | Number | Source port range start |
| filter.src\_port\_range\_max | Body | Number | Source port range end |
| filter.dst\_port\_range\_min | Body | Number | Destination port range start |
| filter.dst\_port\_range\_max | Body | Number | Destination port range end |
| filter.protocol | Body | String | `tcp`, `udp`, `icmp`, or null |
| filter.action | Body | Enum | `accept`, `drop` |
| filter.priority | Body | Number | Priority (default 101) |
| filter.tenant\_id | Body | String | Tenant ID |
| filter.project\_id | Body | String | Project ID |
| filter.created\_at | Body | String | Creation time (UTC) |
| filter.updated\_at | Body | String | Modified Time (UTC) |

***

<a id="create-filters"></a>
### Create Filters { #create-filters }

```
POST /v2.0/mirroring/filters
X-Auth-Token: {tokenId}
```

<a id="create-filters-request"></a>
#### Request

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | Token ID |
| filter | Body | Object | O | Filter Create Request Object |
| filter.description | Body | String | - | Description (max 255 characters) |
| filter.filter\_group\_id | Body | UUID | O | Affiliated Filter Group ID |
| filter.src\_cidr | Body | CIDR | - | Source CIDR |
| filter.dst\_cidr | Body | CIDR | - | Destination CIDR |
| filter.src\_port\_range\_min | Body | Number | - | Source Port Start |
| filter.src\_port\_range\_max | Body | Number | - | Source Port End |
| filter.dst\_port\_range\_min | Body | Number | - | Destination port start |
| filter.dst\_port\_range\_max | Body | Number | - | Destination port end |
| filter.protocol | Body | String | - | `tcp`, `udp`, `icmp`, or null |
| filter.action | Body | Enum | O | `accept`, `drop` |
| filter.priority | Body | Number | - | Priority. Default 101 |
| filter.tenant\_id | Body | String | O | Tenant ID |
| filter.project\_id | Body | String | O | Project ID |

Example

```json
{
  "filter": {
    "description": "allow tcp 80 to 10.0.0.0/24",
    "filter_group_id": "2a3a9c36-0a9a-4a1e-8bb2-03e8d7fa1f10",
    "dst_cidr": "10.0.0.0/24",
    "dst_port_range_min": 80,
    "dst_port_range_max": 80,
    "protocol": "tcp",
    "action": "accept",
    "priority": 101,
    "tenant_id": "76841f7d054a40b88b2a99828280998c",
    "project_id": "76841f7d054a40b88b2a99828280998c"
  }
}
```

<a id="create-filters-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| filter | Body | Object | Filter List |
| filter.id | Body | UUID | Filter ID |
| filter.description | Body | String | Description |
| filter.filter\_group\_id | Body | UUID | Filter Group ID |
| filter.src\_cidr | Body | CIDR | Source CIDR. Optional |
| filter.dst\_cidr | Body | CIDR | Destination CIDR. Optional |
| filter.src\_port\_range\_min | Body | Number | Source port range start |
| filter.src\_port\_range\_max | Body | Number | Source port range end |
| filter.dst\_port\_range\_min | Body | Number | Destination port range start |
| filter.dst\_port\_range\_max | Body | Number | End of destination port range |
| filter.protocol | Body | String | `tcp`, `udp`, `icmp`, or null |
| filter.action | Body | Enum | `accept`, `drop` |
| filter.priority | Body | Number | Priority (default 101) |
| filter.tenant\_id | Body | String | Tenant ID |
| filter.project\_id | Body | String | Project ID |
| filter.created\_at | Body | String | Creation time (UTC) |
| filter.updated\_at | Body | String | Modification time (UTC) |

***

<a id="modify-filters"></a>
### Modify Filters { #modify-filters }

```
PUT /v2.0/mirroring/filters/{FilterId}
X-Auth-Token: {tokenId}
```

Only the description can be modified. Matching conditions, actions, priorities, and group affiliation cannot be modified.

<a id="modify-filters-request"></a>
#### Request

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| FilterId | URL | UUID | Yes | Filter ID |
| tokenId | Header | String | Yes | Token ID |
| filter | Body | Object | Yes | Include only fields to be modified |
| filter.description | Body | String | - | Description |

<a id="modify-filters-response"></a>
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| filter | Body | Object | Filter List |
| filter.id | Body | UUID | Filter ID |
| filter.description | Body | String | Description |
| filter.filter\_group\_id | Body | UUID | Filter Group ID |
| filter.src\_cidr | Body | CIDR | Source CIDR. Optional |
| filter.dst\_cidr | Body | CIDR | Destination CIDR. Can be unspecified |
| filter.src\_port\_range\_min | Body | Number | Source port range start |
| filter.src\_port\_range\_max | Body | Number | Source port range end |
| filter.dst\_port\_range\_min | Body | Number | Destination port range start |
| filter.dst\_port\_range\_max | Body | Number | Destination port range end |
| filter.protocol | Body | String | `tcp`, `udp`, `icmp`, or null |
| filter.action | Body | Enum | `accept`, `drop` |
| filter.priority | Body | Number | Priority (default 101) |
| filter.tenant\_id | Body | String | Tenant ID |
| filter.project\_id | Body | String | Project ID |
| filter.created\_at | Body | String | Creation Time (UTC) |
| filter.updated\_at | Body | String | Modification Time (UTC) |

***

<a id="delete-filters"></a>
### Delete Filters { #delete-filters }

```
DELETE /v2.0/mirroring/filters/{FilterId}
X-Auth-Token: {tokenId}
```

<a id="delete-filters-requestresponse"></a>
#### Request/Response

No request body. No response body.
