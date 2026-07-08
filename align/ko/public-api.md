<a id="network-traffic-mirroring-api-v2-guide"></a>
## Network > Traffic Mirroring > API v2 가이드 { #network-traffic-mirroring-api-v2-guide }

NHN Cloud Network 서비스는 API 호출 시 인증/인가를 위해 IaaS 토큰을 사용합니다. IaaS 토큰은 NHN Cloud의 OpenStack 기반 인프라 서비스(IaaS)에서 사용하는 인증 토큰입니다. IaaS 토큰 발급 및 사용에 대한 자세한 내용은 [IaaS 토큰](/nhncloud/ko/public-api/iaas-token)을 참고하세요.

미러링 API는 `network` 타입 엔드포인트를 이용합니다. 정확한 엔드포인트는 토큰 발급 응답의 `serviceCatalog`를 참조합니다.

| 타입 | 리전 | 엔드포인트 |
| --- | --- | ----- |
| network | 한국(판교) 리전<br>한국(평촌) 리전<br>한국(광주) 리전 | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://kr3-api-network-infrastructure.nhncloudservice.com |

API 응답에 가이드에 명시되지 않은 필드가 나타날 수 있습니다. 이런 필드는 NHN Cloud 내부 용도로 사용되며 사전 공지 없이 변경될 수 있으므로 사용하지 않습니다.

<a id="mirroring-session-session"></a>
## 미러링 세션(session) { #mirroring-session-session }

세션은 소스 포트의 트래픽을 타깃 포트로 미러링하는 단위를 의미합니다. 필요한 경우 하나 이상의 필터 그룹을 연결해 세부 트래픽만 미러링할 수 있습니다.

<a id="view-session-lists"></a>
### 세션 목록 보기 { #view-session-lists }

```
GET /v2.0/mirroring/sessions
X-Auth-Token: {tokenId}
```

<a id="view-session-lists-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 세션 ID |
| tenant\_id | Query | String | - | 테넌트 ID |
| name | Query | String | - | 세션 이름 |
| direction | Query | Enum | - | `in`, `out`, `both` 중 하나 |
| sort\_dir | Query | Enum | - | 정렬 방향. `asc`, `desc` 중 하나 |
| sort\_key | Query | String | - | 정렬 기준 필드 |
| fields | Query | String | - | 응답에 포함할 필드. 예: `fields=id&fields=name` |

<a id="view-session-lists-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| sessions | Body | Array | 세션 객체 목록 |
| sessions.id | Body | UUID | 세션 ID |
| sessions.name | Body | String | 세션 이름 |
| sessions.description | Body | String | 설명 |
| sessions.target\_port\_id | Body | UUID | 타깃 포트 ID |
| sessions.source\_port\_id | Body | UUID | 소스 포트 ID |
| sessions.filter\_groups | Body | Array[UUID] | 연결된 필터 그룹 ID 목록 |
| sessions.direction | Body | Enum | `in`, `out`, `both` 중 하나 |
| sessions.tenant\_id | Body | String | 테넌트 ID |
| sessions.project\_id | Body | String | 프로젝트 ID. 테넌트 ID와 동일 |
| sessions.target\_network\_id | Body | UUID | 타깃 포트의 네트워크 ID |
| sessions.source\_network\_id | Body | UUID | 소스 포트의 네트워크 ID |
| sessions.vni | Body | Number | 미러링 터널 VNI |
| sessions.status | Body | Enum | 세션 상태: `ACTIVE`, `BUILD`, `ERROR` |
| sessions.created\_at | Body | String | 생성 시간(UTC) |
| sessions.updated\_at | Body | String | 수정 시간(UTC) |

예시

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
### 세션 보기 { #view-sessions }

```
GET /v2.0/mirroring/sessions/{SessionId}
X-Auth-Token: {tokenId}
```

<a id="view-sessions-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| SessionId | URL | UUID | O | 세션 ID |
| tokenId | Header | String | O | 토큰 ID |
| fields | Query | String | - | 응답에 포함할 필드. 예: `fields=id&fields=name` |

<a id="view-sessions-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| session | Body | Object | 세션 객체 |
| session.id | Body | UUID | 세션 ID |
| session.name | Body | String | 세션 이름 |
| session.description | Body | String | 설명 |
| session.target\_port\_id | Body | UUID | 타깃 포트 ID |
| session.source\_port\_id | Body | UUID | 소스 포트 ID |
| session.filter\_groups | Body | Array[UUID] | 연결된 필터 그룹 ID 목록 |
| session.direction | Body | Enum | `in`, `out`, `both` 중 하나 |
| session.tenant\_id | Body | String | 테넌트 ID |
| session.project\_id | Body | String | 프로젝트 ID |
| session.target\_network\_id | Body | UUID | 타깃 포트의 네트워크 ID |
| session.source\_network\_id | Body | UUID | 소스 포트의 네트워크 ID |
| session.vni | Body | Number | 터널 VNI |
| session.status | Body | Enum | `ACTIVE`, `BUILD`, `ERROR` |
| session.created\_at | Body | String | 생성 시간(UTC) |
| session.updated\_at | Body | String | 수정 시간(UTC) |

예시

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
### 세션 생성하기 { #create-sessions }

```
POST /v2.0/mirroring/sessions
X-Auth-Token: {tokenId}
```

<a id="create-sessions-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | 토큰 ID |
| session | Body | Object | O | 세션 생성 요청 객체 |
| session.name | Body | String | - | 세션 이름(최대 32자, 영문/숫자/`-`/`_`) |
| session.description | Body | String | - | 설명(최대 255자) |
| session.target\_port\_id | Body | UUID | O | 타깃 포트 ID |
| session.source\_port\_id | Body | UUID | O | 소스 포트 ID |
| session.filter\_groups | Body | Array[UUID] | - | 연결할 필터 그룹 ID 목록. 없으면 전체 트래픽 미러링 |
| session.direction | Body | Enum | O | `in`, `out`, `both` 중 하나 |
| session.tenant\_id | Body | String | O | 테넌트 ID |
| session.project\_id | Body | String | O | 프로젝트 ID |

예시

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
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| session | Body | Object | 세션 객체 |
| session.id | Body | UUID | 세션 ID |
| session.status | Body | Enum | 초기에는 주로 `BUILD` |
| 그 외 | Body | - | 세션 보기와 동일 |

예시

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
### 세션 수정하기 { #modify-sessions }

```
PUT /v2.0/mirroring/sessions/{SessionId}
X-Auth-Token: {tokenId}
```

설명과 이름, 방향, 필터 그룹 목록만 수정할 수 있습니다. 포트 변경은 지원하지 않습니다.

<a id="modify-sessions-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| SessionId | URL | UUID | O | 세션 ID |
| tokenId | Header | String | O | 토큰 ID |
| session | Body | Object | O | 수정할 필드만 포함 |
| session.name | Body | String | - | 세션 이름 |
| session.description | Body | String | - | 설명 |
| session.filter\_groups | Body | Array[UUID] | - | 필터 그룹 ID 목록 |
| session.direction | Body | Enum | - | `in`, `out`, `both` |

예시

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
#### 응답

세션 보기 응답과 동일합니다.

***

<a id="delete-sessions"></a>
### 세션 삭제하기 { #delete-sessions }

```
DELETE /v2.0/mirroring/sessions/{SessionId}
X-Auth-Token: {tokenId}
```

<a id="delete-sessions-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| SessionId | URL | UUID | O | 세션 ID |
| tokenId | Header | String | O | 토큰 ID |

<a id="delete-sessions-response"></a>
#### 응답

이 API는 응답 본문을 반환하지 않습니다.

***

<a id="mirroring-filter-group-filtergroup"></a>
## 미러링 필터 그룹(filtergroup) { #mirroring-filter-group-filtergroup }

필터 그룹은 하나 이상의 필터를 묶는 컨테이너입니다. 세션에 연결하여 특정 트래픽만 미러링할 수 있습니다.

<a id="view-a-list-of-filter-groups"></a>
### 필터 그룹 목록 보기 { #view-a-list-of-filter-groups }

```
GET /v2.0/mirroring/filtergroups
X-Auth-Token: {tokenId}
```

<a id="view-a-list-of-filter-groups-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 필터 그룹 ID |
| tenant\_id | Query | String | - | 테넌트 ID |
| name | Query | String | - | 이름 |
| sort\_dir | Query | Enum | - | `asc`, `desc` |
| sort\_key | Query | String | - | 정렬 키 |
| fields | Query | String | - | 포함할 필드 |

<a id="view-a-list-of-filter-groups-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| filtergroups | Body | Array | 필터 그룹 목록 |
| filtergroups.id | Body | UUID | ID |
| filtergroups.name | Body | String | 이름 |
| filtergroups.description | Body | String | 설명 |
| filtergroups.tenant\_id | Body | String | 테넌트 ID |
| filtergroups.project\_id | Body | String | 프로젝트 ID |
| filtergroups.filters | Body | Array | 그룹 내 필터 객체/ID 목록 |
| filtergroups.created\_at | Body | String | 생성 시간(UTC) |
| filtergroups.updated\_at | Body | String | 수정 시간(UTC) |

예시

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
### 필터 그룹 보기 { #view-filter-groups }

```
GET /v2.0/mirroring/filtergroups/{FilterGroupId}
X-Auth-Token: {tokenId}
```

<a id="view-filter-groups-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | 토큰 ID |
| id | URL | UUID | O | 필터 그룹 ID |

<a id="view-filter-groups-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| filtergroup | Body | Object | 필터 그룹 목록 |
| filtergroup.id | Body | UUID | ID |
| filtergroup.name | Body | String | 이름 |
| filtergroup.description | Body | String | 설명 |
| filtergroup.tenant\_id | Body | String | 테넌트 ID |
| filtergroup.project\_id | Body | String | 프로젝트 ID |
| filtergroup.filters | Body | Array | 그룹 내 필터 객체/ID 목록 |
| filtergroup.created\_at | Body | String | 생성 시간(UTC) |
| filtergroup.updated\_at | Body | String | 수정 시간(UTC) |

***

<a id="create-filter-groups"></a>
### 필터 그룹 생성하기 { #create-filter-groups }

```
POST /v2.0/mirroring/filtergroups
X-Auth-Token: {tokenId}
```

<a id="create-filter-groups-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | 토큰 ID |
| filtergroup | Body | Object | O | 필터 그룹 생성 요청 객체 |
| filtergroup.name | Body | String | - | 이름(최대 32자, 영문/숫자/`-`/`_`) |
| filtergroup.description | Body | String | - | 설명(최대 255자) |
| filtergroup.tenant\_id | Body | String | O | 테넌트 ID |
| filtergroup.project\_id | Body | String | O | 프로젝트 ID |

예시

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
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| filtergroup | Body | Object | 필터 그룹 객체 |
| filtergroup.id | Body | UUID | ID |
| filtergroup.name | Body | String | 이름 |
| filtergroup.description | Body | String | 설명 |
| filtergroup.tenant\_id | Body | String | 테넌트 ID |
| filtergroup.project\_id | Body | String | 프로젝트 ID |
| filtergroup.filters | Body | Array | 그룹 내 필터 객체/ID 목록 |
| filtergroup.created\_at | Body | String | 생성 시간(UTC) |
| filtergroup.updated\_at | Body | String | 수정 시간(UTC) |

***

<a id="modify-filter-groups"></a>
### 필터 그룹 수정하기 { #modify-filter-groups }

```
PUT /v2.0/mirroring/filtergroups/{FilterGroupId}
X-Auth-Token: {tokenId}
```

이름과 설명만 수정할 수 있습니다.

<a id="modify-filter-groups-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| FilterGroupId | URL | UUID | O | 필터 그룹 ID |
| tokenId | Header | String | O | 토큰 ID |
| filtergroup | Body | Object | O | 수정할 필드만 포함 |
| filtergroup.name | Body | String | - | 이름 |
| filtergroup.description | Body | String | - | 설명 |

<a id="modify-filter-groups-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| filtergroup | Body | Object | 필터 그룹 객체 |
| filtergroup.id | Body | UUID | ID |
| filtergroup.name | Body | String | 이름 |
| filtergroup.description | Body | String | 설명 |
| filtergroup.tenant\_id | Body | String | 테넌트 ID |
| filtergroup.project\_id | Body | String | 프로젝트 ID |
| filtergroup.filters | Body | Array | 그룹 내 필터 객체/ID 목록 |
| filtergroup.created\_at | Body | String | 생성 시간(UTC) |
| filtergroup.updated\_at | Body | String | 수정 시간(UTC) |

***

<a id="delete-filter-groups"></a>
### 필터 그룹 삭제하기 { #delete-filter-groups }

```
DELETE /v2.0/mirroring/filtergroups/{FilterGroupId}
X-Auth-Token: {tokenId}
```

<a id="delete-filter-groups-requestresponse"></a>
#### 요청/응답

요청 본문 없음. 응답 본문 없음.

***

<a id="mirroring-filter-filter"></a>
## 미러링 필터(filter) { #mirroring-filter-filter }

필터는 매칭 조건과 액션으로 구성되며, 특정 트래픽을 허용(`accept`) 또는 제외(`drop`)하는 용도로 사용됩니다. 필터는 반드시 특정 필터 그룹에 속해야 합니다.

<a id="view-filter-lists"></a>
### 필터 목록 보기 { #view-filter-lists }

```
GET /v2.0/mirroring/filters
X-Auth-Token: {tokenId}
```

<a id="view-filter-lists-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 필터 ID |
| filter\_group\_id | Query | UUID | - | 소속 필터 그룹 ID |
| tenant\_id | Query | String | - | 테넌트 ID |
| sort\_dir | Query | Enum | - | `asc`, `desc` |
| sort\_key | Query | String | - | 정렬 키 |
| fields | Query | String | - | 포함할 필드 |

<a id="view-filter-lists-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| filters | Body | Array | 필터 목록 |
| filters.id | Body | UUID | 필터 ID |
| filters.description | Body | String | 설명 |
| filters.filter\_group\_id | Body | UUID | 소속 필터 그룹 ID |
| filters.src\_cidr | Body | CIDR | 소스 CIDR. 미지정 가능 |
| filters.dst\_cidr | Body | CIDR | 대상 CIDR. 미지정 가능 |
| filters.src\_port\_range\_min | Body | Number | 소스 포트 범위 시작 |
| filters.src\_port\_range\_max | Body | Number | 소스 포트 범위 끝 |
| filters.dst\_port\_range\_min | Body | Number | 대상 포트 범위 시작 |
| filters.dst\_port\_range\_max | Body | Number | 대상 포트 범위 끝 |
| filters.protocol | Body | String | `tcp`, `udp`, `icmp` 또는 null |
| filters.action | Body | Enum | `accept`, `drop` |
| filters.priority | Body | Number | 우선순위(기본 101) |
| filters.tenant\_id | Body | String | 테넌트 ID |
| filters.project\_id | Body | String | 프로젝트 ID |
| filters.created\_at | Body | String | 생성 시간(UTC) |
| filters.updated\_at | Body | String | 수정 시간(UTC) |

예시

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
### 필터 보기 { #view-filters }

```
GET /v2.0/mirroring/filters/{FilterId}
X-Auth-Token: {tokenId}
```

<a id="view-filters-request"></a>
#### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | 토큰 ID |
| id | Query | URL | O | 필터 ID |

<a id="view-filters-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| filter | Body | Object | 필터 목록 |
| filter.id | Body | UUID | 필터 ID |
| filter.description | Body | String | 설명 |
| filter.filter\_group\_id | Body | UUID | 소속 필터 그룹 ID |
| filter.src\_cidr | Body | CIDR | 소스 CIDR. 미지정 가능 |
| filter.dst\_cidr | Body | CIDR | 대상 CIDR. 미지정 가능 |
| filter.src\_port\_range\_min | Body | Number | 소스 포트 범위 시작 |
| filter.src\_port\_range\_max | Body | Number | 소스 포트 범위 끝 |
| filter.dst\_port\_range\_min | Body | Number | 대상 포트 범위 시작 |
| filter.dst\_port\_range\_max | Body | Number | 대상 포트 범위 끝 |
| filter.protocol | Body | String | `tcp`, `udp`, `icmp` 또는 null |
| filter.action | Body | Enum | `accept`, `drop` |
| filter.priority | Body | Number | 우선순위(기본 101) |
| filter.tenant\_id | Body | String | 테넌트 ID |
| filter.project\_id | Body | String | 프로젝트 ID |
| filter.created\_at | Body | String | 생성 시간(UTC) |
| filter.updated\_at | Body | String | 수정 시간(UTC) |

***

<a id="create-filters"></a>
### 필터 생성하기 { #create-filters }

```
POST /v2.0/mirroring/filters
X-Auth-Token: {tokenId}
```

<a id="create-filters-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| tokenId | Header | String | O | 토큰 ID |
| filter | Body | Object | O | 필터 생성 요청 객체 |
| filter.description | Body | String | - | 설명(최대 255자) |
| filter.filter\_group\_id | Body | UUID | O | 소속 필터 그룹 ID |
| filter.src\_cidr | Body | CIDR | - | 소스 CIDR |
| filter.dst\_cidr | Body | CIDR | - | 대상 CIDR |
| filter.src\_port\_range\_min | Body | Number | - | 소스 포트 시작 |
| filter.src\_port\_range\_max | Body | Number | - | 소스 포트 끝 |
| filter.dst\_port\_range\_min | Body | Number | - | 대상 포트 시작 |
| filter.dst\_port\_range\_max | Body | Number | - | 대상 포트 끝 |
| filter.protocol | Body | String | - | `tcp`, `udp`, `icmp` 또는 null |
| filter.action | Body | Enum | O | `accept`, `drop` |
| filter.priority | Body | Number | - | 우선순위. 기본 101 |
| filter.tenant\_id | Body | String | O | 테넌트 ID |
| filter.project\_id | Body | String | O | 프로젝트 ID |

예시

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
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| filter | Body | Object | 필터 목록 |
| filter.id | Body | UUID | 필터 ID |
| filter.description | Body | String | 설명 |
| filter.filter\_group\_id | Body | UUID | 소속 필터 그룹 ID |
| filter.src\_cidr | Body | CIDR | 소스 CIDR. 미지정 가능 |
| filter.dst\_cidr | Body | CIDR | 대상 CIDR. 미지정 가능 |
| filter.src\_port\_range\_min | Body | Number | 소스 포트 범위 시작 |
| filter.src\_port\_range\_max | Body | Number | 소스 포트 범위 끝 |
| filter.dst\_port\_range\_min | Body | Number | 대상 포트 범위 시작 |
| filter.dst\_port\_range\_max | Body | Number | 대상 포트 범위 끝 |
| filter.protocol | Body | String | `tcp`, `udp`, `icmp` 또는 null |
| filter.action | Body | Enum | `accept`, `drop` |
| filter.priority | Body | Number | 우선순위(기본 101) |
| filter.tenant\_id | Body | String | 테넌트 ID |
| filter.project\_id | Body | String | 프로젝트 ID |
| filter.created\_at | Body | String | 생성 시간(UTC) |
| filter.updated\_at | Body | String | 수정 시간(UTC) |

***

<a id="modify-filters"></a>
### 필터 수정하기 { #modify-filters }

```
PUT /v2.0/mirroring/filters/{FilterId}
X-Auth-Token: {tokenId}
```

설명만 수정할 수 있습니다. 매칭 조건, 액션, 우선순위, 소속 그룹은 수정할 수 없습니다.

<a id="modify-filters-request"></a>
#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| FilterId | URL | UUID | O | 필터 ID |
| tokenId | Header | String | O | 토큰 ID |
| filter | Body | Object | O | 수정할 필드만 포함 |
| filter.description | Body | String | - | 설명 |

<a id="modify-filters-response"></a>
#### 응답

| 이름 | 종류 | 형식 | 설명 |
| --- | --- | --- | --- |
| filter | Body | Object | 필터 목록 |
| filter.id | Body | UUID | 필터 ID |
| filter.description | Body | String | 설명 |
| filter.filter\_group\_id | Body | UUID | 소속 필터 그룹 ID |
| filter.src\_cidr | Body | CIDR | 소스 CIDR. 미지정 가능 |
| filter.dst\_cidr | Body | CIDR | 대상 CIDR. 미지정 가능 |
| filter.src\_port\_range\_min | Body | Number | 소스 포트 범위 시작 |
| filter.src\_port\_range\_max | Body | Number | 소스 포트 범위 끝 |
| filter.dst\_port\_range\_min | Body | Number | 대상 포트 범위 시작 |
| filter.dst\_port\_range\_max | Body | Number | 대상 포트 범위 끝 |
| filter.protocol | Body | String | `tcp`, `udp`, `icmp` 또는 null |
| filter.action | Body | Enum | `accept`, `drop` |
| filter.priority | Body | Number | 우선순위(기본 101) |
| filter.tenant\_id | Body | String | 테넌트 ID |
| filter.project\_id | Body | String | 프로젝트 ID |
| filter.created\_at | Body | String | 생성 시간(UTC) |
| filter.updated\_at | Body | String | 수정 시간(UTC) |

***

<a id="delete-filters"></a>
### 필터 삭제하기 { #delete-filters }

```
DELETE /v2.0/mirroring/filters/{FilterId}
X-Auth-Token: {tokenId}
```

<a id="delete-filters-requestresponse"></a>
#### 요청/응답

요청 본문 없음. 응답 본문 없음.
