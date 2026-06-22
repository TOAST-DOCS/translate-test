## 알림

**Database > EasyCache > 콘솔 사용 가이드 > 알림**

알림 그룹을 이용해 성능 지표에 대한 알림을 받을 수 있습니다. **알림 유형**과 **활성화 여부**를 선택한 뒤 감시 대상 노드와 알림을 받을 사용자 그룹을 지정합니다. **감시 설정**에서 알림을 받을 성능 지표의 임곗값과 조건을 설정합니다. 설정된 지표가 감시 설정의 조건을 충족하면 연결된 사용자 그룹에 알림을 발송합니다. 알림 그룹에 설정된 알림 유형에 따라 SMS 또는 메일로 알림을 발송합니다.

#### 알림 그룹 생성

![notification1.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification1.PNG)

❶: **알림 그룹 생성**을 클릭하면 알림 그룹을 생성할 수 있는 팝업 창이 나타납니다.
❷: 알림을 받을 방법을 선택합니다.
❸: **활성화 여부**를 **아니오**로 선택한 알림 그룹은 알림 발송을 하지 않습니다.
❹: 감시할 대상 노드를 선택합니다.
❺: 알림을 받을 사용자 그룹을 선택합니다.

### 감시 설정

감시 설정은 감시 항목, 비교 방법, 임곗값 및 지속 시간으로 구성됩니다. 감시 항목의 성능 지표값과 임곗값을 비교하여 조건을 충족하는지 판단합니다. 조건을 지속 시간 이상 연속해서 충족한다면 알림을 발송합니다. 예를 들어, CPU 사용률의 임곗값이 90% 이상이고 지속 시간이 5분이라면, 해당 알림 그룹과 연동된 노드의 CPU 사용률이 90% 이상인 상태가 5분 이상 지속되었을 때, 사용자 그룹에 정의된 사용자들에게 알림을 보냅니다. 만약 CPU 사용률이 90% 이상이 되어도, 5분 이내에 90% 미만으로 떨어지면 알림이 발생하지 않습니다.

#### 감시 설정 항목

감시 가능한 성능 지표 항목은 다음과 같습니다.

| 카테고리 | 항목 | 단위 |
| - | - | - |
| CPU | CPU_USAGE | % |
| CPU  | CPU_USAGE_IOWAIT | % |
| CPU  | CPU_USAGE_NICE | % |
| CPU  | CPU_USAGE_SYSTEM | % |
| CPU  | CPU_USAGE_USER | % |
| CPU  | LOAD_AVG_1M |  |
| CPU  | LOAD_AVG_5M |  |
| CPU  | LOAD_AVG_15M |  |
| MEMORY | MEMORY_USAGE | % |
| MEMORY | MEMORY_USED | Bytes |
| MEMORY | MEMORY_FREE | Bytes |
| MEMORY | MEMORY_BUFFERS | Bytes |
| MEMORY | MEMORY_CACHED | Bytes |
| MEMORY | SWAP_USED | Bytes |
| MEMORY | SWAP_TOTAL | Bytes |
| NETWORK | NETWORK_SENT | Bytes/sec |
| NETWORK | NETWORK_RECV | Bytes/sec |
| STORAGE | STORAGE_FREE_BYTE | Bytes |
| STORAGE  | STORAGE_IO_READ_TOTAL | Bytes/sec |
| STORAGE  | STORAGE_IO_WRITE_TOTAL | Bytes/sec |
| STORAGE  | STORAGE_IO_READ | % |
| STORAGE  | STORAGE_IO_WRITE | Bytes |
| STORAGE  | LINUX_DISK_FAULT |  |
| REDIS | REDIS_CONNECTED_CLIENTS |  |
| REDIS | REDIS_CONNECTED_SLAVES |  |
| REDIS | REDIS_USED_MEMORY_RATE | % |
| REDIS | REDIS_USED_MEMORY_RSS_RATE | % |
| REDIS | REDIS_MEM_FRAGMENTATION_RATIO | % |
| REDIS | REDIS_INSTANTANEOUS_OPS_PER_SEC | ops/sec |
| REDIS | REDIS_HIT_RATE | % |
| REDIS | REDIS_KEYS |  |
| REDIS | REDIS_DELTA_BLOCKED_CLIENTS |  |
| REDIS | REDIS_DELTA_NET_INPUT_BYTES | Bytes |
| REDIS | REDIS_DELTA_NET_OUTPUT_BYTES | Bytes |
| REDIS | REDIS_EXPIRED_KEYS |  |
| REDIS | REDIS_EVICTED_KEYS |  |
| REDIS | REDIS_KEYSPACE_HITS |  |
| REDIS | REDIS_KEYSPACE_MISSES |  |
| REDIS | REDIS_DELTA_CMDSTAT_GET_USEC_PER_CALL | ms |
| REDIS | REDIS_DELTA_CMDSTAT_SET_USEC_PER_CALL | ms |
| REDIS | REDIS_DELTA_CMDSTAT_GET_CALLS |  |
| REDIS | REDIS_DELTA_CMDSTAT_SET_CALLS |  |
| REDIS | REDIS_DELTA_CMDSTAT_HGET_CALLS |  |
| REDIS | REDIS_DELTA_CMDSTAT_HSET_CALLS |  |

#### 감시 설정 추가

![notification2.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification2.PNG)

❶ **감시 설정**을 누르면 감시 설정을 변경할 수 있는 팝업 창이 나타납니다.
❷ **감시 설정 추가**를 눌러 신규 감시 설정을 추가합니다.
❸ 감시할 항목과 비교 방법, 임곗값, 지속 시간을 입력한 뒤 **추가**를 클릭합니다.

#### 감시 설정 변경 및 삭제

![notification3.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification3.PNG)

❶ 버튼을 클릭하면 추가된 감시 설정을 변경할 수 있습니다.
❷ 버튼을 클릭하면 추가된 감시 설정을 삭제할 수 있습니다.

### 사용자 그룹

알림을 받을 사용자를 그룹으로 관리할 수 있습니다. 알림 대상은 반드시 프로젝트 멤버로 등록되어 있어야 합니다. 사용자 그룹에 속한 사용자가 프로젝트 멤버에서 제외되면 사용자 그룹에 속해 있더라도 알림을 받을 수 없습니다.

!!! danger "주의"
    실명 인증을 진행하지 않아 휴대폰 정보가 없을 경우 SMS 알림을 받을 수 없습니다.

#### 사용자 그룹 생성

![notification4.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification4.PNG)

❶ **사용자 그룹 생성**을 누르면 사용자 그룹을 생성할 수 있는 팝업 창이 나타납니다.
❷ **통보 방법** 항목의 프로젝트 전체 멤버 항목을 선택하면, 프로젝트에 속한 모두를 자동 반영합니다.
❸ **통보 방법** 항목의 사용자 지정 항목을 선택하면 사용자 그룹에 통보 대상 리스트가 나타납니다.
❹ **추가**를 누르면 통보 대상에 추가할 수 있는 프로젝트의 멤버가 나타납니다.
❺ **확인**을 눌러 사용자 그룹을 생성합니다.

#### 사용자 그룹 수정 및 삭제

![notification5.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification5.PNG)

❶ 버튼을 클릭하면 추가된 사용자 그룹을 수정할 수 있습니다.
❷ 버튼을 클릭하면 추가된 사용자 그룹을 삭제할 수 있습니다.
