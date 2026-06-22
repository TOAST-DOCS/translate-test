## 이벤트

**Database > EasyCache > 콘솔 사용 가이드 > 이벤트**

이벤트는 Valkey 또는 사용자에 의해 발생한 중요한 사건을 의미합니다. 이벤트는 이벤트 유형, 발생 일시, 원본 소스와 메시지로 구성됩니다. 이벤트는 콘솔에서 조회 가능하며, 구독을 통해 이메일, SMS으로 이벤트 발생 알림을 받을 수 있습니다. 이벤트의 유형과 발생 가능한 이벤트는 아래와 같습니다.

* 현재 제공하는 이벤트 유형 및 이벤트 코드

| 이벤트 유형 | 이벤트 코드                                             | 구독 가능 여부 | 설명                                 |
| - |----------------------------------------------------| - |------------------------------------|
| CACHE | APPLY_LATEST_PARAMETER_GROUP_START                 | 예 | 최신 파라미터 그룹 적용 시작                   |
| CACHE | APPLY_LATEST_PARAMETER_GROUP_END                   | 예 | 최신 파라미터 그룹 적용 완료                   |
| CACHE | APPLY_LATEST_PARAMETER_GROUP_FAILED                | 예 | 최신 파라미터 그룹 적용 실패                   |
| CACHE | AUTO_BACKUP_ACTIVATION_START                       | 예 | 자동 백업 활성화 시작                       |
| CACHE | AUTO_BACKUP_ACTIVATION_END                         | 예 | 자동 백업 활성화 완료                       |
| CACHE | AUTO_BACKUP_ACTIVATION_FAILED                      | 예 | 자동 백업 활성화 실패                       |
| CACHE | AUTO_BACKUP_DEACTIVATION_START                     | 예 | 자동 백업 비활성화 시작                      |
| CACHE | AUTO_BACKUP_DEACTIVATION_END                       | 예 | 자동 백업 비활성화 완료                      |
| CACHE | AUTO_BACKUP_DEACTIVATION_FAILED                    | 예 | 자동 백업 비활성화 실패                      |
| CACHE | BACKUP_START                                       | 예 | 백업 시작                              |
| CACHE | BACKUP_END                                         | 예 | 백업 완료                              |
| CACHE | BACKUP_FAILED                                      | 예 | 백업 실패                              |
| CACHE | BACKUP_DELETION_START                              | 예 | 백업 삭제 시작                           |
| CACHE | BACKUP_DELETION_END                                | 예 | 백업 삭제 완료                           |
| CACHE | BACKUP_DELETION_FAILED                             | 예 | 백업 삭제 실패                           |
| CACHE | BACKUP_MIGRATE_START                               | 아니오 | 백업 마이그레이션 시작                       |
| CACHE | BACKUP_MIGRATE_END                                 | 아니오 | 백업 마이그레이션 완료                       |
| CACHE | BACKUP_MIGRATE_DOWNLOAD_FAILED                     | 아니오 | 백업 마이그레이션 다운로드 실패                  |
| CACHE | BACKUP_MIGRATE_RDB_CHECK_FAILED                    | 아니오 | 백업 마이그레이션 RDB 체크 실패                |
| CACHE | BACKUP_MIGRATE_RDB_CHECKSUM_FAILED                 | 아니오 | 백업 마이그레이션 RDB 체크섬 실패               |
| CACHE | BACKUP_MIGRATE_RDB_MEMORY_FAILED                   | 아니오 | 백업 마이그레이션 RDB 메모리 실패               |
| CACHE | BACKUP_MIGRATE_RDB_TYPE_FAILED                     | 아니오 | 백업 마이그레이션 RDB 타입 실패                |
| CACHE | BACKUP_MIGRATE_RDB_VERSION_FAILED                  | 아니오 | 백업 마이그레이션 RDB 버전 실패                |
| CACHE | BACKUP_MIGRATE_REPLICA_CHECK_FAILED                | 아니오 | 백업 마이그레이션 복제본 체크 실패                |
| CACHE | BACKUP_MIGRATE_RESTART_FAILED                      | 아니오 | 백업 마이그레이션 재시작 실패                   |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_START                | 예 | 기존 캐시로 백업 복원 시작                    |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_END                  | 예 | 기존 캐시로 백업 복원 완료                    |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_FAILED               | 예 | 기존 캐시로 백업 복원 실패                    |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_DOWNLOAD_FAILED      | 예 | 기존 캐시로 백업 복원 다운로드 실패               |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_CHECK_FAILED     | 예 | 기존 캐시로 백업 복원 RDB 체크 실패             |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_CHECKSUM_FAILED  | 예 | 기존 캐시로 백업 복원 RDB 체크섬 실패            |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_MEMORY_FAILED    | 예 | 기존 캐시로 백업 복원 RDB 메모리 실패            |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_TYPE_FAILED      | 예 | 기존 캐시로 백업 복원 RDB 타입 실패             |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_VERSION_FAILED   | 예 | 기존 캐시로 백업 복원 RDB 버전 실패             |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_REPLICA_CHECK_FAILED | 예 | 기존 캐시로 백업 복원 복제본 체크 실패             |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RESTART_FAILED       | 예 | 기존 캐시로 백업 복원 재시작 실패                |
| CACHE | BACKUP_RESTORE_NEW_CACHE_START                     | 예 | 새 캐시로 백업 복원 시작                     |
| CACHE | BACKUP_RESTORE_NEW_CACHE_END                       | 예 | 새 캐시로 백업 복원 완료                     |
| CACHE | BACKUP_RESTORE_NEW_CACHE_FAILED                    | 예 | 새 캐시로 백업 복원 실패                     |
| CACHE | CACHE_CERTIFICATE_UPDATE_START                     | 예 | 캐시 인증서 갱신 시작                       |
| CACHE | CACHE_CERTIFICATE_UPDATE_END                       | 예 | 캐시 인증서 갱신 완료                       |
| CACHE | CACHE_CERTIFICATE_UPDATE_FAILED                    | 예 | 캐시 인증서 갱신 실패                       |
| CACHE | CACHE_CREATION_START                               | 예 | 캐시 생성 시작                           |
| CACHE | CACHE_CREATION_END                                 | 예 | 캐시 생성 완료                           |
| CACHE | CACHE_CREATION_FAILED                              | 예 | 캐시 생성 실패                           |
| CACHE | CACHE_DATA_EXPORTING_START                         | 예 | 캐시 데이터 내보내기 시작                     |
| CACHE | CACHE_DATA_EXPORTING_END                           | 예 | 캐시 데이터 내보내기 완료                     |
| CACHE | CACHE_DATA_EXPORTING_FAILED                        | 예 | 캐시 데이터 내보내기 실패                     |
| CACHE | CACHE_DATA_EXPORTING_RDB_CREATE_FAILED             | 예 | 캐시 데이터 내보내기 RDB 생성 실패              |
| CACHE | CACHE_DATA_EXPORTING_SETTING_FAILED                | 예 | 캐시 데이터 내보내기 설정 실패                  |
| CACHE | CACHE_DATA_EXPORTING_UPLOAD_FAILED                 | 예 | 캐시 데이터 내보내기 업로드 실패                 |
| CACHE | CACHE_DATA_IMPORTING_START                         | 예 | 캐시 데이터 가져오기 시작                     |
| CACHE | CACHE_DATA_IMPORTING_END                           | 예 | 캐시 데이터 가져오기 완료                     |
| CACHE | CACHE_DATA_IMPORTING_FAILED                        | 예 | 캐시 데이터 가져오기 실패                     |
| CACHE | CACHE_DATA_IMPORTING_DOWNLOAD_FAILED               | 예 | 캐시 데이터 가져오기 다운로드 실패                |
| CACHE | CACHE_DATA_IMPORTING_RDB_CHECK_FAILED              | 예 | 캐시 데이터 가져오기 RDB 체크 실패              |
| CACHE | CACHE_DATA_IMPORTING_RDB_CHECKSUM_FAILED           | 예 | 캐시 데이터 가져오기 RDB 체크섬 실패             |
| CACHE | CACHE_DATA_IMPORTING_RDB_MEMORY_FAILED             | 예 | 캐시 데이터 가져오기 RDB 메모리 실패             |
| CACHE | CACHE_DATA_IMPORTING_RDB_TYPE_FAILED               | 예 | 캐시 데이터 가져오기 RDB 타입 실패              |
| CACHE | CACHE_DATA_IMPORTING_RDB_VERSION_FAILED            | 예 | 캐시 데이터 가져오기 RDB 버전 실패              |
| CACHE | CACHE_DATA_IMPORTING_REPLICA_CHECK_FAILED          | 예 | 캐시 데이터 가져오기 복제본 체크 실패              |
| CACHE | CACHE_DATA_IMPORTING_RESTART_FAILED                | 예 | 캐시 데이터 가져오기 재시작 실패                 |
| CACHE | CACHE_DATA_IMPORTING_SETTING_FAILED                | 예 | 캐시 데이터 가져오기 설정 실패                  |
| CACHE | CACHE_DELETION_START                               | 예 | 캐시 삭제 시작                           |
| CACHE | CACHE_DELETION_END                                 | 예 | 캐시 삭제 완료                           |
| CACHE | CACHE_DELETION_FAILED                              | 예 | 캐시 삭제 실패                           |
| CACHE | CACHE_DELETION_PROTECTION_DISABLING_START          | 예 | 캐시 삭제 보호 비활성화 시작                   |
| CACHE | CACHE_DELETION_PROTECTION_DISABLING_END            | 예 | 캐시 삭제 보호 비활성화 완료                   |
| CACHE | CACHE_DELETION_PROTECTION_DISABLING_FAILED         | 예 | 캐시 삭제 보호 비활성화 실패                   |
| CACHE | CACHE_DELETION_PROTECTION_ENABLING_START           | 예 | 캐시 삭제 보호 활성화 시작                    |
| CACHE | CACHE_DELETION_PROTECTION_ENABLING_END             | 예 | 캐시 삭제 보호 활성화 완료                    |
| CACHE | CACHE_DELETION_PROTECTION_ENABLING_FAILED          | 예 | 캐시 삭제 보호 활성화 실패                    |
| CACHE | CACHE_DETAIL_MODIFICATION_START                    | 예 | 캐시 상세 수정 시작                        |
| CACHE | CACHE_DETAIL_MODIFICATION_END                      | 예 | 캐시 상세 수정 완료                        |
| CACHE | CACHE_DETAIL_MODIFICATION_FAILED                   | 예 | 캐시 상세 수정 실패                        |
| CACHE | CACHE_FLAVOR_MODIFICATION_START                    | 예 | 캐시 사양 변경 시작                        |
| CACHE | CACHE_FLAVOR_MODIFICATION_END                      | 예 | 캐시 사양 변경 완료                        |
| CACHE | CACHE_FLAVOR_MODIFICATION_FAILED                   | 예 | 캐시 사양 변경 실패                        |
| CACHE | CACHE_HIGH_AVAILABILITY_REPAIR_START               | 예 | 캐시 고가용성 복구 시작                      |
| CACHE | CACHE_HIGH_AVAILABILITY_REPAIR_END                 | 예 | 캐시 고가용성 복구 완료                      |
| CACHE | CACHE_HIGH_AVAILABILITY_REPAIR_FAILED              | 예 | 캐시 고가용성 복구 실패                      |
| CACHE | CACHE_MASTER_ROLE_CHANGING_START                   | 예 | 캐시 마스터 역할 변경 시작                    |
| CACHE | CACHE_MASTER_ROLE_CHANGING_END                     | 예 | 캐시 마스터 역할 변경 완료                    |
| CACHE | CACHE_MASTER_ROLE_CHANGING_FAILED                  | 예 | 캐시 마스터 역할 변경 실패                    |
| CACHE | CACHE_MODIFICATION_START                           | 예 | 캐시 수정 시작                           |
| CACHE | CACHE_MODIFICATION_END                             | 예 | 캐시 수정 완료                           |
| CACHE | CACHE_MODIFICATION_FAILED                          | 예 | 캐시 수정 실패                           |
| CACHE | CACHE_RESTART_START                                | 예 | 캐시 재시작 시작                          |
| CACHE | CACHE_RESTART_END                                  | 예 | 캐시 재시작 완료                          |
| CACHE | CACHE_RESTART_FAILED                               | 예 | 캐시 재시작 실패                          |
| CACHE | CACHE_STARTING_START                               | 예 | 캐시 시작 시작                           |
| CACHE | CACHE_STARTING_END                                 | 예 | 캐시 시작 완료                           |
| CACHE | CACHE_STARTING_FAILED                              | 예 | 캐시 시작 실패                           |
| CACHE | CACHE_STOPPING_START                               | 예 | 캐시 중지 시작                           |
| CACHE | CACHE_STOPPING_END                                 | 예 | 캐시 중지 완료                           |
| CACHE | CACHE_STOPPING_FAILED                              | 예 | 캐시 중지 실패                           |
| CACHE | CACHE_UPGRADE_START                                | 예 | 캐시 업그레이드 시작                        |
| CACHE | CACHE_UPGRADE_END                                  | 예 | 캐시 업그레이드 완료                        |
| CACHE | CACHE_UPGRADE_FAILED                               | 예 | 캐시 업그레이드 실패                        |
| CACHE | CACHE_UPGRADE_HA_UPGRADE_FAILED                    | 예 | 캐시 업그레이드 HA 실패                     |
| CACHE | CACHE_UPGRADE_MASTER_UPGRADE_FAILED                | 예 | 캐시 업그레이드 마스터 실패                    |
| CACHE | CACHE_UPGRADE_REPLICA_PROMOTE_FAILED               | 예 | 캐시 업그레이드 복제본 승격 실패                 |
| CACHE | CACHE_UPGRADE_REPLICA_UPGRADE_FAILED               | 예 | 캐시 업그레이드 복제본 실패                    |
| CACHE | FAILOVER_DNS_FAILED                                | 아니오 | DNS 갱신 실패                          |
| CACHE | FAILOVER_DNSFAIL                                   | 예 | 장애 조치 DNS 실패                       |
| CACHE | FAILOVER_EXECUTED                                  | 예 | 장애 조치 발생                           |
| CACHE | FLOATING_IP_ATTACHING_START                        | 예 | 플로팅 IP 연결 시작                       |
| CACHE | FLOATING_IP_ATTACHING_END                          | 예 | 플로팅 IP 연결 완료                       |
| CACHE | FLOATING_IP_ATTACHING_FAILED                       | 예 | 플로팅 IP 연결 실패                       |
| CACHE | FLOATING_IP_DETACHING_START                        | 예 | 플로팅 IP 해제 시작                       |
| CACHE | FLOATING_IP_DETACHING_END                          | 예 | 플로팅 IP 해제 완료                       |
| CACHE | FLOATING_IP_DETACHING_FAILED                       | 예 | 플로팅 IP 해제 실패                       |
| CACHE | HA_NODE_CREATION_START                             | 예 | HA 노드 생성 시작                        |
| CACHE | HA_NODE_CREATION_END                               | 예 | HA 노드 생성 완료                        |
| CACHE | HA_NODE_CREATION_FAILED                            | 예 | HA 노드 생성 실패                        |
| CACHE | HA_NODE_DELETION_START                             | 예 | HA 노드 삭제 시작                        |
| CACHE | HA_NODE_DELETION_END                               | 예 | HA 노드 삭제 완료                        |
| CACHE | NODE_OS_UPGRADE_START                              | 예 | 노드 OS 업그레이드 시작                     |
| CACHE | NODE_OS_UPGRADE_END                                | 예 | 노드 OS 업그레이드 완료                     |
| CACHE | NODE_OS_UPGRADE_FAILED                             | 예 | 노드 OS 업그레이드 실패                     |
| CACHE | READONLY_DOMAIN_ATTACHING_START                    | 예 | 읽기 전용 도메인 연결 시작                    |
| CACHE | READONLY_DOMAIN_ATTACHING_END                      | 예 | 읽기 전용 도메인 연결 완료                    |
| CACHE | READONLY_DOMAIN_ATTACHING_FAILED                   | 예 | 읽기 전용 도메인 연결 실패                    |
| CACHE | READONLY_DOMAIN_DETACHING_START                    | 예 | 읽기 전용 도메인 해제 시작                    |
| CACHE | READONLY_DOMAIN_DETACHING_END                      | 예 | 읽기 전용 도메인 해제 완료                    |
| CACHE | READONLY_DOMAIN_DETACHING_FAILED                   | 예 | 읽기 전용 도메인 해제 실패                    |
| CACHE | READONLY_DOMAIN_UPDATE_START                       | 예 | 읽기 전용 도메인 업데이트 시작                  |
| CACHE | READONLY_DOMAIN_UPDATE_END                         | 예 | 읽기 전용 도메인 업데이트 완료                  |
| CACHE | READONLY_DOMAIN_UPDATE_FAILED                      | 예 | 읽기 전용 도메인 업데이트 실패                  |
| CACHE | SENTINEL_CREATION_START                            | 아니오 | 센티넬 노드 생성 시작                       |
| CACHE | SENTINEL_CREATION_END                              | 아니오 | 센티넬 노드 생성 완료                       |
| CACHE | SENTINEL_CREATION_FAILED                           | 아니오 | 센티넬 노드 생성 실패                       |
| CACHE | SENTINEL_DELETION_START                            | 아니오 | 센티넬 노드 삭제 시작                       |
| CACHE | SENTINEL_DELETION_END                              | 아니오 | 센티넬 노드 삭제 완료                       |
| CACHE | SENTINEL_DELETION_FAILED                           | 아니오 | 센티넬 노드 삭제 실패                       |
| CACHE | SENTINEL_FAILOVER                                  | 아니오 | 장애 조치 발생                           |
| CACHE | SENTINEL_FAILOVER_DNSFAIL                          | 아니오 | 장애 조치 DNS 실패                       |
| CACHE | SENTINEL_QUORUM_UPDATE_START                       | 예 | 센티넬 쿼럼 업데이트 시작                     |
| CACHE | SENTINEL_QUORUM_UPDATE_END                         | 예 | 센티넬 쿼럼 업데이트 완료                     |
| CACHE | SENTINEL_QUORUM_UPDATE_FAILED                      | 예 | 센티넬 쿼럼 업데이트 실패                     |
| CACHE | SLAVE_NODE_PROMOTION_START                         | 예 | 복제 노드 승격 시작                        |
| CACHE | SLAVE_NODE_PROMOTION_END                           | 예 | 복제 노드 승격 완료                        |
| CACHE | SLAVE_NODE_PROMOTION_FAILED                        | 예 | 복제 노드 승격 실패                        |
| NODE | NODE_DELETION_START                                | 예 | 노드 삭제 시작                           |
| NODE | NODE_DELETION_END                                  | 예 | 노드 삭제 완료                           |
| NODE | NODE_DELETION_FAILED                               | 예 | 노드 삭제 실패                           |
| NODE | NODE_DOWN_DETECTED                                 | 예 | 노드 중지됨                             |
| NODE | NODE_FLAVOR_MODIFICATION_START                     | 예 | 노드 사양 변경 시작                        |
| NODE | NODE_FLAVOR_MODIFICATION_END                       | 예 | 노드 사양 변경 완료                        |
| NODE | NODE_FLAVOR_MODIFICATION_FAILED                    | 예 | 노드 사양 변경 실패                        |
| NODE | NODE_PLANNED_MIGRATION_START                       | 예 | 노드 플랜드 마이그레이션 시작                   |
| NODE | NODE_PLANNED_MIGRATION_END                         | 예 | 노드 플랜드 마이그레이션 완료                   |
| NODE | NODE_PLANNED_MIGRATION_FAILED                      | 예 | 노드 플랜드 마이그레이션 실패                   |
| NODE | NODE_RECOVERED                                     | 예 | 노드 실행 중                            |
| NODE | NODE_UPGRADE_START                                 | 예 | 노드 엔진 업그레이드 시작                     |
| NODE | NODE_UPGRADE_END                                   | 예 | 노드 엔진 업그레이드 완료                     |
| NODE | NODE_UPGRADE_FAILED                                | 예 | 노드 엔진 업그레이드 실패                     |
| NODE | NODE_UPGRADE_DOWNLOAD_FAILED                       | 예 | 노드 엔진 업그레이드 다운로드 실패                |
| NODE | NODE_UPGRADE_PARAMETER_GROUP_UPDATE_FAILED         | 예 | 노드 엔진 업그레이드 파라미터 그룹 업데이트 실패        |
| NODE | NODE_UPGRADE_REDIS_N_SENTINEL_START_FAILED         | 예 | 노드 엔진 업그레이드 Redis 및 Sentinel 시작 실패 |
| NODE | NODE_UPGRADE_REDIS_N_SENTINEL_STOP_FAILED          | 예 | 노드 엔진 업그레이드 Redis 및 Sentinel 중지 실패 |
| NODE | NODE_UPGRADE_REDIS_UPGRADE_FAILED                  | 예 | 노드 엔진 업그레이드 Redis 업그레이드 실패         |
| NODE | NODE_UPGRADE_REPLICA_CHECK_FAILED                  | 예 | 노드 엔진 업그레이드 복제본 체크 실패              |
| NODE | NODE_UPGRADE_RPM_DELETE_FAILED                     | 예 | 노드 엔진 업그레이드 RPM 삭제 실패              |
| NODE | NODE_UPGRADE_SENTINEL_START_FAILED                 | 예 | 노드 엔진 업그레이드 센티넬 시작 실패              |
| NODE | NODE_UPGRADE_SENTINEL_STOP_FAILED                  | 예 | 노드 엔진 업그레이드 센티넬 중지 실패              |
| NODE | SLAVE_NODE_CREATION_START                          | 예 | 복제 노드 생성 시작                        |
| NODE | SLAVE_NODE_CREATION_END                            | 예 | 복제 노드 생성 완료                        |
| NODE | SLAVE_NODE_CREATION_FAILED                         | 예 | 복제 노드 생성 실패                        |
| NODE | STATUS_CHANGED_DISABLED                            | 아니오 | 비활성화                               |
| NODE | STATUS_CHANGED_ENABLED                             | 아니오 | 활성화                                |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_CREATION_START                   | 아니오 | DB 보안 그룹 생성 시작                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_CREATION_END                     | 아니오 | DB 보안 그룹 생성 완료                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_CREATION_FAILED                  | 아니오 | DB 보안 그룹 생성 실패                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_DELETION_START                   | 아니오 | DB 보안 그룹 삭제 시작                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_DELETION_END                     | 아니오 | DB 보안 그룹 삭제 완료                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_DELETION_FAILED                  | 아니오 | DB 보안 그룹 삭제 실패                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_MODIFICATION_START               | 아니오 | DB 보안 그룹 수정 시작                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_MODIFICATION_END                 | 아니오 | DB 보안 그룹 수정 완료                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_MODIFICATION_FAILED              | 아니오 | DB 보안 그룹 수정 실패                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_CREATION_START              | 아니오 | DB 보안 그룹 규칙 생성 시작                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_CREATION_END                | 아니오 | DB 보안 그룹 규칙 생성 완료                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_CREATION_FAILED             | 아니오 | DB 보안 그룹 규칙 생성 실패                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_DELETION_START              | 아니오 | DB 보안 그룹 규칙 삭제 시작                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_DELETION_END                | 아니오 | DB 보안 그룹 규칙 삭제 완료                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_DELETION_FAILED             | 아니오 | DB 보안 그룹 규칙 삭제 실패                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_MODIFICATION_START          | 아니오 | DB 보안 그룹 규칙 수정 시작                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_MODIFICATION_END            | 아니오 | DB 보안 그룹 규칙 수정 완료                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_MODIFICATION_FAILED         | 아니오 | DB 보안 그룹 규칙 수정 실패                  |
| PARAMETER_GROUP | PARAMETER_GROUP_CREATION_START                     | 아니오 | 파라미터 그룹 생성 시작                      |
| PARAMETER_GROUP | PARAMETER_GROUP_CREATION_END                       | 아니오 | 파라미터 그룹 생성 완료                      |
| PARAMETER_GROUP | PARAMETER_GROUP_CREATION_FAILED                    | 아니오 | 파라미터 그룹 생성 실패                      |
| PARAMETER_GROUP | PARAMETER_GROUP_DELETION_START                     | 아니오 | 파라미터 그룹 삭제 시작                      |
| PARAMETER_GROUP | PARAMETER_GROUP_DELETION_END                       | 아니오 | 파라미터 그룹 삭제 완료                      |
| PARAMETER_GROUP | PARAMETER_GROUP_DELETION_FAILED                    | 아니오 | 파라미터 그룹 삭제 실패                      |
| MONITORING | METRIC_ALARM_TRIGGERED                             | 예 | 모니터링 알람 발생                         |

* 기록은 남아 있으나 더 이상 새로 생성하지 않는 이벤트 코드

| 이벤트 유형 | 이벤트 코드 | 구독 가능 여부 | 설명 |
| - | - | - | - |
| CACHE | GROUP_CERTIFICATE_UPDATE_START | 아니오 | 그룹 인증서 갱신 시작 |
| CACHE | GROUP_CERTIFICATE_UPDATE_END | 아니오 | 그룹 인증서 갱신 완료 |
| CACHE | GROUP_CERTIFICATE_UPDATE_FAILED | 아니오 | 그룹 인증서 갱신 실패 |
| CACHE | GROUP_CREATION_START | 아니오 | 그룹 생성 시작 |
| CACHE | GROUP_CREATION_END | 아니오 | 그룹 생성 완료 |
| CACHE | GROUP_CREATION_FAILED | 아니오 | 그룹 생성 실패 |
| CACHE | GROUP_DATA_EXPORTING_START | 아니오 | 그룹 데이터 내보내기 시작 |
| CACHE | GROUP_DATA_EXPORTING_END | 아니오 | 그룹 데이터 내보내기 완료 |
| CACHE | GROUP_DATA_EXPORTING_FAILED | 아니오 | 그룹 데이터 내보내기 실패 |
| CACHE | GROUP_DATA_EXPORTING_RDB_CREATE_FAILED | 아니오 | 그룹 데이터 내보내기 RDB 생성 실패 |
| CACHE | GROUP_DATA_EXPORTING_SETTING_FAILED | 아니오 | 그룹 데이터 내보내기 설정 실패 |
| CACHE | GROUP_DATA_EXPORTING_UPLOAD_FAILED | 아니오 | 그룹 데이터 내보내기 업로드 실패 |
| CACHE | GROUP_DATA_IMPORTING_START | 아니오 | 그룹 데이터 가져오기 시작 |
| CACHE | GROUP_DATA_IMPORTING_END | 아니오 | 그룹 데이터 가져오기 완료 |
| CACHE | GROUP_DATA_IMPORTING_DOWNLOAD_FAILED | 아니오 | 그룹 데이터 가져오기 다운로드 실패 |
| CACHE | GROUP_DATA_IMPORTING_RDB_CHECK_FAILED | 아니오 | 그룹 데이터 가져오기 RDB 체크 실패 |
| CACHE | GROUP_DATA_IMPORTING_RDB_CHECKSUM_FAILED | 아니오 | 그룹 데이터 가져오기 RDB 체크섬 실패 |
| CACHE | GROUP_DATA_IMPORTING_RDB_MEMORY_FAILED | 아니오 | 그룹 데이터 가져오기 RDB 메모리 실패 |
| CACHE | GROUP_DATA_IMPORTING_RDB_TYPE_FAILED | 아니오 | 그룹 데이터 가져오기 RDB 타입 실패 |
| CACHE | GROUP_DATA_IMPORTING_RDB_VERSION_FAILED | 아니오 | 그룹 데이터 가져오기 RDB 버전 실패 |
| CACHE | GROUP_DATA_IMPORTING_REPLICA_CHECK_FAILED | 아니오 | 그룹 데이터 가져오기 복제본 체크 실패 |
| CACHE | GROUP_DATA_IMPORTING_RESTART_FAILED | 아니오 | 그룹 데이터 가져오기 재시작 실패 |
| CACHE | GROUP_DATA_IMPORTING_SETTING_FAILED | 아니오 | 그룹 데이터 가져오기 설정 실패 |
| CACHE | GROUP_DELETION_START | 아니오 | 그룹 삭제 시작 |
| CACHE | GROUP_DELETION_END | 아니오 | 그룹 삭제 완료 |
| CACHE | GROUP_DELETION_FAILED | 아니오 | 그룹 삭제 실패 |
| CACHE | GROUP_FLAVOR_MODIFICATION_START | 아니오 | 그룹 사양 변경 시작 |
| CACHE | GROUP_FLAVOR_MODIFICATION_END | 아니오 | 그룹 사양 변경 완료 |
| CACHE | GROUP_FLAVOR_MODIFICATION_FAILED | 아니오 | 그룹 사양 변경 실패 |
| CACHE | GROUP_MODIFICATION_START | 아니오 | 그룹 수정 시작 |
| CACHE | GROUP_MODIFICATION_END | 아니오 | 그룹 수정 완료 |
| CACHE | GROUP_MODIFICATION_FAILED | 아니오 | 그룹 수정 실패 |
| CACHE | GROUP_RESTART_START | 아니오 | 그룹 재시작 시작 |
| CACHE | GROUP_RESTART_END | 아니오 | 그룹 재시작 완료 |
| CACHE | GROUP_RESTART_FAILED | 아니오 | 그룹 재시작 실패 |
| CACHE | GROUP_UPGRADE_START | 아니오 | 그룹 업그레이드 시작 |
| CACHE | GROUP_UPGRADE_END | 아니오 | 그룹 업그레이드 완료 |
| CACHE | GROUP_UPGRADE_FAILED | 아니오 | 그룹 업그레이드 실패 |
| CACHE | GROUP_UPGRADE_HA_UPGRADE_FAILED | 아니오 | 그룹 업그레이드 HA 실패 |
| CACHE | GROUP_UPGRADE_MASTER_UPGRADE_FAILED | 아니오 | 그룹 업그레이드 마스터 실패 |
| CACHE | GROUP_UPGRADE_REPLICA_PROMOTE_FAILED | 아니오 | 그룹 업그레이드 복제본 승격 실패 |
| CACHE | GROUP_UPGRADE_REPLICA_UPGRADE_FAILED | 아니오 | 그룹 업그레이드 복제본 실패 |
| PARAMETER_GROUP | PROFILE_UPDATE_START                               | 아니오 | 프로필 업데이트 시작                        |
| PARAMETER_GROUP | PROFILE_UPDATE_END                                 | 아니오 | 프로필 업데이트 완료                        |
| PARAMETER_GROUP | PROFILE_UPDATE_FAILED                              | 아니오 | 프로필 업데이트 실패                        |
| NODE | SENTINEL_INSTANCE_RUNNING                          | 아니오 | 인스턴스 실행                            |
| NODE | SENTINEL_INSTANCE_STOPPED                          | 아니오 | 인스턴스 중지됨                           |


### 이벤트 구독

이벤트 유형, 코드 및 소스로 구분하여 이벤트를 구독할 수 있습니다. 이벤트 유형으로 구독하면 이벤트 유형에 포함된 모든 이벤트 코드의 알림을 받습니다. 알림이 너무 광범위할 경우 이벤트 코드와 소스로 세분화해 구독할 수 있습니다. 프로젝트 멤버만 알림을 받을 사용자로 선택할 수 있습니다. 기본적으로 이메일로 이벤트 알림이 발송되며, 실명을 인증한 휴대전화 번호가 등록된 경우에만 SMS로 추가 이벤트 알림이 발송됩니다.

![event1.PNG](https://static.toastoven.net/prod_easycache/25.09.27/event1.PNG)
![event2.PNG](https://static.toastoven.net/prod_easycache/25.09.27/event2.PNG)

❶: **이벤트 구독 등록**을 누르면 이벤트 구독을 등록할 수 있는 팝업 창이 나타납니다.
❷: 구독할 이벤트 유형을 선택합니다. 이벤트 유형에 따라 선택할 수 있는 이벤트 코드가 변경됩니다.
❸: 이벤트 템플릿을 이용하면 템플릿에 미리 정해진 이벤트 코드들을 한 번에 입력할 수 있습니다.
❹: 구독할 이벤트 코드를 직접 선택합니다. 이벤트 템플릿을 사용한 상태에서 이벤트 코드를 변경할 경우 이벤트 템플릿 항목이 해제됩니다.
❺: 구독할 이벤트 소스를 직접 선택합니다.
❻: 이벤트 알림을 받을 사용자 그룹을 선택합니다.
❼: 알림 유형을 통해 알림을 받을 방식을 선택합니다.
❽: 활성화 여부를 선택합니다. 활성화 여부를 **아니오**로 선택할 경우 이벤트 발생 알림을 발송하지 않습니다.
