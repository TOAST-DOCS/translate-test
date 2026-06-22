## イベント

**Database > EasyCache > コンソール利用ガイド > イベント**

イベントとは、Valkeyまたはユーザーによって発生した重要な事象を意味します。イベントはイベントタイプ、発生日時、ソース、メッセージで構成されます。イベントはコンソールで照会可能であり、購読を通じてメールやSMSでイベント発生通知を受け取ることができます。イベントのタイプと発生可能なイベントは次のとおりです。

* 現在提供しているイベントタイプ及びイベントコード

| イベントタイプ | イベントコード                                            | 購読可否 | 説明                                |
| - |----------------------------------------------------| - |------------------------------------|
| CACHE | APPLY_LATEST_PARAMETER_GROUP_START                 | はい | 最新パラメータグループ適用開始                   |
| CACHE | APPLY_LATEST_PARAMETER_GROUP_END                   | はい | 最新パラメータグループ適用完了                  |
| CACHE | APPLY_LATEST_PARAMETER_GROUP_FAILED                | はい | 最新パラメータグループ適用失敗                  |
| CACHE | AUTO_BACKUP_ACTIVATION_START                       | はい | 自動バックアップ有効化開始                       |
| CACHE | AUTO_BACKUP_ACTIVATION_END                         | はい | 自動バックアップ有効化完了                      |
| CACHE | AUTO_BACKUP_ACTIVATION_FAILED                      | はい | 自動バックアップ有効化失敗                      |
| CACHE | AUTO_BACKUP_DEACTIVATION_START                     | はい | 自動バックアップ無効化開始                      |
| CACHE | AUTO_BACKUP_DEACTIVATION_END                       | はい | 自動バックアップ無効化完了                     |
| CACHE | AUTO_BACKUP_DEACTIVATION_FAILED                    | はい | 自動バックアップ無効化失敗                     |
| CACHE | BACKUP_START                                       | はい | バックアップ開始                              |
| CACHE | BACKUP_END                                         | はい | バックアップ完了                             |
| CACHE | BACKUP_FAILED                                      | はい | バックアップ失敗                             |
| CACHE | BACKUP_DELETION_START                              | はい | バックアップ削除開始                           |
| CACHE | BACKUP_DELETION_END                                | はい | バックアップ削除完了                          |
| CACHE | BACKUP_DELETION_FAILED                             | はい | バックアップ削除失敗                          |
| CACHE | BACKUP_MIGRATE_START                               | いいえ | バックアップマイグレーション開始                       |
| CACHE | BACKUP_MIGRATE_END                                 | いいえ | バックアップマイグレーション完了                       |
| CACHE | BACKUP_MIGRATE_DOWNLOAD_FAILED                     | いいえ | バックアップマイグレーションダウンロード失敗                 |
| CACHE | BACKUP_MIGRATE_RDB_CHECK_FAILED                    | いいえ | バックアップマイグレーションRDBチェック失敗               |
| CACHE | BACKUP_MIGRATE_RDB_CHECKSUM_FAILED                 | いいえ | バックアップマイグレーションRDBチェックサム 失敗              |
| CACHE | BACKUP_MIGRATE_RDB_MEMORY_FAILED                   | いいえ | バックアップマイグレーションRDBメモリ失敗              |
| CACHE | BACKUP_MIGRATE_RDB_TYPE_FAILED                     | いいえ | バックアップマイグレーションRDBタイプ失敗               |
| CACHE | BACKUP_MIGRATE_RDB_VERSION_FAILED                  | いいえ | バックアップマイグレーションRDBバージョン失敗               |
| CACHE | BACKUP_MIGRATE_REPLICA_CHECK_FAILED                | いいえ | バックアップマイグレーションレプリカチェック失敗               |
| CACHE | BACKUP_MIGRATE_RESTART_FAILED                      | いいえ | バックアップマイグレーション再起動失敗                  |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_START                | はい | 既存キャッシュへのバックアップ復元開始                    |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_END                  | はい | 既存キャッシュへのバックアップ復元完了                    |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_FAILED               | はい | 既存キャッシュへのバックアップ復元失敗                    |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_DOWNLOAD_FAILED      | はい | 既存キャッシュへのバックアップ復元ダウンロード失敗               |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_CHECK_FAILED     | はい | 既存キャッシュへのバックアップ復元RDBチェック失敗             |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_CHECKSUM_FAILED  | はい | 既存キャッシュへのバックアップ復元RDBチェックサム失敗            |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_MEMORY_FAILED    | はい | 既存キャッシュへのバックアップ復元RDBメモリ失敗            |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_TYPE_FAILED      | はい | 既存キャッシュへのバックアップ復元RDBタイプ失敗             |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_VERSION_FAILED   | はい | 既存キャッシュへのバックアップ復元RDBバージョン失敗             |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_REPLICA_CHECK_FAILED | はい | 既存キャッシュへのバックアップ復元レプリカチェック失敗             |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RESTART_FAILED       | はい | 既存キャッシュへのバックアップ復元再起動失敗                |
| CACHE | BACKUP_RESTORE_NEW_CACHE_START                     | はい | 新しいキャッシュへのバックアップ復元開始                     |
| CACHE | BACKUP_RESTORE_NEW_CACHE_END                       | はい | 新しいキャッシュへのバックアップ復元完了                     |
| CACHE | BACKUP_RESTORE_NEW_CACHE_FAILED                    | はい | 新しいキャッシュへのバックアップ復元失敗                     |
| CACHE | CACHE_CERTIFICATE_UPDATE_START                     | はい | キャッシュ証明書更新開始                       |
| CACHE | CACHE_CERTIFICATE_UPDATE_END                       | はい | キャッシュ証明書更新完了                      |
| CACHE | CACHE_CERTIFICATE_UPDATE_FAILED                    | はい | キャッシュ証明書更新失敗                      |
| CACHE | CACHE_CREATION_START                               | はい | キャッシュ作成開始                           |
| CACHE | CACHE_CREATION_END                                 | はい | キャッシュ作成完了                          |
| CACHE | CACHE_CREATION_FAILED                              | はい | キャッシュ作成失敗                          |
| CACHE | CACHE_DATA_EXPORTING_START                         | はい | キャッシュデータのエクスポート開始                     |
| CACHE | CACHE_DATA_EXPORTING_END                           | はい | キャッシュデータのエクスポート完了                     |
| CACHE | CACHE_DATA_EXPORTING_FAILED                        | はい | キャッシュデータのエクスポート失敗                     |
| CACHE | CACHE_DATA_EXPORTING_RDB_CREATE_FAILED             | はい | キャッシュデータのエクスポートRDB作成失敗              |
| CACHE | CACHE_DATA_EXPORTING_SETTING_FAILED                | はい | キャッシュデータのエクスポート設定失敗                  |
| CACHE | CACHE_DATA_EXPORTING_UPLOAD_FAILED                 | はい | キャッシュデータのエクスポートアップロード失敗                 |
| CACHE | CACHE_DATA_IMPORTING_START                         | はい | キャッシュデータのインポート開始                     |
| CACHE | CACHE_DATA_IMPORTING_END                           | はい | キャッシュデータのインポート完了                     |
| CACHE | CACHE_DATA_IMPORTING_FAILED                        | はい | キャッシュデータのインポート失敗                     |
| CACHE | CACHE_DATA_IMPORTING_DOWNLOAD_FAILED               | はい | キャッシュデータのインポートダウンロード失敗                |
| CACHE | CACHE_DATA_IMPORTING_RDB_CHECK_FAILED              | はい | キャッシュデータのインポートRDBチェック失敗              |
| CACHE | CACHE_DATA_IMPORTING_RDB_CHECKSUM_FAILED           | はい | キャッシュデータのインポートRDBチェックサム失敗             |
| CACHE | CACHE_DATA_IMPORTING_RDB_MEMORY_FAILED             | はい | キャッシュデータのインポートRDBメモリ失敗             |
| CACHE | CACHE_DATA_IMPORTING_RDB_TYPE_FAILED               | はい | キャッシュデータのインポートRDBタイプ失敗              |
| CACHE | CACHE_DATA_IMPORTING_RDB_VERSION_FAILED            | はい | キャッシュデータのインポートRDBバージョン失敗              |
| CACHE | CACHE_DATA_IMPORTING_REPLICA_CHECK_FAILED          | はい | キャッシュデータのインポートレプリカチェック失敗              |
| CACHE | CACHE_DATA_IMPORTING_RESTART_FAILED                | はい | キャッシュデータのインポート再起動失敗                 |
| CACHE | CACHE_DATA_IMPORTING_SETTING_FAILED                | はい | キャッシュデータのインポート設定失敗                  |
| CACHE | CACHE_DELETION_START                               | はい | キャッシュ削除開始                           |
| CACHE | CACHE_DELETION_END                                 | はい | キャッシュ削除完了                          |
| CACHE | CACHE_DELETION_FAILED                              | はい | キャッシュ削除失敗                          |
| CACHE | CACHE_DELETION_PROTECTION_DISABLING_START          | はい | キャッシュ削除保護無効化開始                   |
| CACHE | CACHE_DELETION_PROTECTION_DISABLING_END            | はい | キャッシュ削除保護無効化完了                  |
| CACHE | CACHE_DELETION_PROTECTION_DISABLING_FAILED         | はい | キャッシュ削除保護無効化失敗                  |
| CACHE | CACHE_DELETION_PROTECTION_ENABLING_START           | はい | キャッシュ削除保護有効化開始                    |
| CACHE | CACHE_DELETION_PROTECTION_ENABLING_END             | はい | キャッシュ削除保護有効化完了                   |
| CACHE | CACHE_DELETION_PROTECTION_ENABLING_FAILED          | はい | キャッシュ削除保護有効化失敗                   |
| CACHE | CACHE_DETAIL_MODIFICATION_START                    | はい | キャッシュ詳細修正開始                        |
| CACHE | CACHE_DETAIL_MODIFICATION_END                      | はい | キャッシュ詳細修正完了                       |
| CACHE | CACHE_DETAIL_MODIFICATION_FAILED                   | はい | キャッシュ詳細修正失敗                       |
| CACHE | CACHE_FLAVOR_MODIFICATION_START                    | はい | キャッシュスペック変更開始                        |
| CACHE | CACHE_FLAVOR_MODIFICATION_END                      | はい | キャッシュスペック変更完了                        |
| CACHE | CACHE_FLAVOR_MODIFICATION_FAILED                   | はい | キャッシュスペック変更失敗                        |
| CACHE | CACHE_HIGH_AVAILABILITY_REPAIR_START               | はい | キャッシュ高可用性修復開始                      |
| CACHE | CACHE_HIGH_AVAILABILITY_REPAIR_END                 | はい | キャッシュ高可用性修復完了                      |
| CACHE | CACHE_HIGH_AVAILABILITY_REPAIR_FAILED              | はい | キャッシュ高可用性修復失敗                      |
| CACHE | CACHE_MASTER_ROLE_CHANGING_START                   | はい | キャッシュマスターロール変更開始                    |
| CACHE | CACHE_MASTER_ROLE_CHANGING_END                     | はい | キャッシュマスターロール変更完了                    |
| CACHE | CACHE_MASTER_ROLE_CHANGING_FAILED                  | はい | キャッシュマスターロール変更失敗                    |
| CACHE | CACHE_MODIFICATION_START                           | はい | キャッシュ修正開始                           |
| CACHE | CACHE_MODIFICATION_END                             | はい | キャッシュ修正完了                          |
| CACHE | CACHE_MODIFICATION_FAILED                          | はい | キャッシュ修正失敗                          |
| CACHE | CACHE_RESTART_START                                | はい | キャッシュ再起動開始                          |
| CACHE | CACHE_RESTART_END                                  | はい | キャッシュ再起動完了                         |
| CACHE | CACHE_RESTART_FAILED                               | はい | キャッシュ再起動失敗                         |
| CACHE | CACHE_STARTING_START                               | はい | キャッシュ起動開始                           |
| CACHE | CACHE_STARTING_END                                 | はい | キャッシュ起動完了                           |
| CACHE | CACHE_STARTING_FAILED                              | はい | キャッシュ起動失敗                           |
| CACHE | CACHE_STOPPING_START                               | はい | キャッシュ停止開始                           |
| CACHE | CACHE_STOPPING_END                                 | はい | キャッシュ停止完了                           |
| CACHE | CACHE_STOPPING_FAILED                              | はい | キャッシュ停止失敗                           |
| CACHE | CACHE_UPGRADE_START                                | はい | キャッシュアップグレード開始                        |
| CACHE | CACHE_UPGRADE_END                                  | はい | キャッシュアップグレード完了                       |
| CACHE | CACHE_UPGRADE_FAILED                               | はい | キャッシュアップグレード失敗                       |
| CACHE | CACHE_UPGRADE_HA_UPGRADE_FAILED                    | はい | キャッシュアップグレードHA失敗                    |
| CACHE | CACHE_UPGRADE_MASTER_UPGRADE_FAILED                | はい | キャッシュアップグレードマスター失敗                   |
| CACHE | CACHE_UPGRADE_REPLICA_PROMOTE_FAILED               | はい | キャッシュアップグレードレプリカ昇格失敗                |
| CACHE | CACHE_UPGRADE_REPLICA_UPGRADE_FAILED               | はい | キャッシュアップグレードレプリカ失敗                   |
| CACHE | FAILOVER_DNS_FAILED                                | いいえ | DNS更新失敗                         |
| CACHE | FAILOVER_DNSFAIL                                   | はい | フェイルオーバーDNS失敗                      |
| CACHE | FAILOVER_EXECUTED                                  | はい | フェイルオーバー発生                          |
| CACHE | FLOATING_IP_ATTACHING_START                        | はい | フローティングIP接続開始                       |
| CACHE | FLOATING_IP_ATTACHING_END                          | はい | フローティングIP接続完了                      |
| CACHE | FLOATING_IP_ATTACHING_FAILED                       | はい | フローティングIP接続失敗                      |
| CACHE | FLOATING_IP_DETACHING_START                        | はい | フローティングIP解除開始                       |
| CACHE | FLOATING_IP_DETACHING_END                          | はい | フローティングIP解除完了                      |
| CACHE | FLOATING_IP_DETACHING_FAILED                       | はい | フローティングIP解除失敗                      |
| CACHE | HA_NODE_CREATION_START                             | はい | HAノード作成開始                        |
| CACHE | HA_NODE_CREATION_END                               | はい | HAノード作成完了                       |
| CACHE | HA_NODE_CREATION_FAILED                            | はい | HAノード作成失敗                       |
| CACHE | HA_NODE_DELETION_START                             | はい | HAノード削除開始                        |
| CACHE | HA_NODE_DELETION_END                               | はい | HAノード削除完了                       |
| CACHE | NODE_OS_UPGRADE_START                              | はい | ノードOSアップグレード開始                     |
| CACHE | NODE_OS_UPGRADE_END                                | はい | ノードOSアップグレード完了                    |
| CACHE | NODE_OS_UPGRADE_FAILED                             | はい | ノードOSアップグレード失敗                    |
| CACHE | READONLY_DOMAIN_ATTACHING_START                    | はい | 読み取り専用ドメイン接続開始                    |
| CACHE | READONLY_DOMAIN_ATTACHING_END                      | はい | 読み取り専用ドメイン接続完了                   |
| CACHE | READONLY_DOMAIN_ATTACHING_FAILED                   | はい | 読み取り専用ドメイン接続失敗                   |
| CACHE | READONLY_DOMAIN_DETACHING_START                    | はい | 読み取り専用ドメイン解除開始                    |
| CACHE | READONLY_DOMAIN_DETACHING_END                      | はい | 読み取り専用ドメイン解除完了                   |
| CACHE | READONLY_DOMAIN_DETACHING_FAILED                   | はい | 読み取り専用ドメイン解除失敗                   |
| CACHE | READONLY_DOMAIN_UPDATE_START                       | はい | 読み取り専用ドメインアップデート開始                  |
| CACHE | READONLY_DOMAIN_UPDATE_END                         | はい | 読み取り専用ドメインアップデート完了                 |
| CACHE | READONLY_DOMAIN_UPDATE_FAILED                      | はい | 読み取り専用ドメインアップデート失敗                 |
| CACHE | SENTINEL_CREATION_START                            | いいえ | Sentinelノード作成開始                       |
| CACHE | SENTINEL_CREATION_END                              | いいえ | Sentinelノード作成完了                       |
| CACHE | SENTINEL_CREATION_FAILED                           | いいえ | Sentinelノード作成失敗                       |
| CACHE | SENTINEL_DELETION_START                            | いいえ | Sentinelノード削除開始                       |
| CACHE | SENTINEL_DELETION_END                              | いいえ | Sentinelノード削除完了                       |
| CACHE | SENTINEL_DELETION_FAILED                           | いいえ | Sentinelノード削除失敗                       |
| CACHE | SENTINEL_FAILOVER                                  | いいえ | フェイルオーバー発生                          |
| CACHE | SENTINEL_FAILOVER_DNSFAIL                          | いいえ | フェイルオーバーDNS失敗                      |
| CACHE | SENTINEL_QUORUM_UPDATE_START                       | はい | Sentinelクォーラムアップデート開始                     |
| CACHE | SENTINEL_QUORUM_UPDATE_END                         | はい | Sentinelクォーラムアップデート完了                     |
| CACHE | SENTINEL_QUORUM_UPDATE_FAILED                      | はい | Sentinelクォーラムアップデート失敗                     |
| CACHE | SLAVE_NODE_PROMOTION_START                         | はい | レプリカノード昇格開始                        |
| CACHE | SLAVE_NODE_PROMOTION_END                           | はい | レプリカノード昇格完了                        |
| CACHE | SLAVE_NODE_PROMOTION_FAILED                        | はい | レプリカノード昇格失敗                        |
| NODE | NODE_DELETION_START                                | はい | ノード削除開始                           |
| NODE | NODE_DELETION_END                                  | はい | ノード削除完了                          |
| NODE | NODE_DELETION_FAILED                               | はい | ノード削除失敗                          |
| NODE | NODE_DOWN_DETECTED                                 | はい | ノード停止                             |
| NODE | NODE_FLAVOR_MODIFICATION_START                     | はい | ノードスペック変更開始                        |
| NODE | NODE_FLAVOR_MODIFICATION_END                       | はい | ノードスペック変更完了                        |
| NODE | NODE_FLAVOR_MODIFICATION_FAILED                    | はい | ノードスペック変更失敗                        |
| NODE | NODE_PLANNED_MIGRATION_START                       | はい | ノード計画的マイグレーション開始                   |
| NODE | NODE_PLANNED_MIGRATION_END                         | はい | ノード計画的マイグレーション完了                   |
| NODE | NODE_PLANNED_MIGRATION_FAILED                      | はい | ノード計画的マイグレーション失敗                   |
| NODE | NODE_RECOVERED                                     | はい | ノード実行中                           |
| NODE | NODE_UPGRADE_START                                 | はい | ノードエンジンアップグレード開始                     |
| NODE | NODE_UPGRADE_END                                   | はい | ノードエンジンアップグレード完了                    |
| NODE | NODE_UPGRADE_FAILED                                | はい | ノードエンジンアップグレード失敗                    |
| NODE | NODE_UPGRADE_DOWNLOAD_FAILED                       | はい | ノードエンジンアップグレードダウンロード失敗               |
| NODE | NODE_UPGRADE_PARAMETER_GROUP_UPDATE_FAILED         | はい | ノードエンジンアップグレードパラメータグループアップデート失敗       |
| NODE | NODE_UPGRADE_REDIS_N_SENTINEL_START_FAILED         | はい | ノードエンジンアップグレードRedis及びSentinel開始失敗 |
| NODE | NODE_UPGRADE_REDIS_N_SENTINEL_STOP_FAILED          | はい | ノードエンジンアップグレードRedis及びSentinel停止失敗 |
| NODE | NODE_UPGRADE_REDIS_UPGRADE_FAILED                  | はい | ノードエンジンアップグレードRedisアップグレード失敗        |
| NODE | NODE_UPGRADE_REPLICA_CHECK_FAILED                  | はい | ノードエンジンアップグレードレプリカチェック失敗             |
| NODE | NODE_UPGRADE_RPM_DELETE_FAILED                     | はい | ノードエンジンアップグレードRPM削除失敗             |
| NODE | NODE_UPGRADE_SENTINEL_START_FAILED                 | はい | ノードエンジンアップグレードSentinel開始失敗              |
| NODE | NODE_UPGRADE_SENTINEL_STOP_FAILED                  | はい | ノードエンジンアップグレードSentinel停止失敗              |
| NODE | SLAVE_NODE_CREATION_START                          | はい | レプリカノード作成開始                        |
| NODE | SLAVE_NODE_CREATION_END                            | はい | レプリカノード作成完了                        |
| NODE | SLAVE_NODE_CREATION_FAILED                         | はい | レプリカノード作成失敗                        |
| NODE | STATUS_CHANGED_DISABLED                            | いいえ | 無効化                              |
| NODE | STATUS_CHANGED_ENABLED                             | いいえ | 有効化                               |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_CREATION_START                   | いいえ | DBセキュリティグループ作成開始                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_CREATION_END                     | いいえ | DBセキュリティグループ作成完了                    |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_CREATION_FAILED                  | いいえ | DBセキュリティグループ作成失敗                    |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_DELETION_START                   | いいえ | DBセキュリティグループ削除開始                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_DELETION_END                     | いいえ | DBセキュリティグループ削除完了                    |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_DELETION_FAILED                  | いいえ | DBセキュリティグループ削除失敗                    |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_MODIFICATION_START               | いいえ | DBセキュリティグループ修正開始                     |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_MODIFICATION_END                 | いいえ | DBセキュリティグループ修正完了                    |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_MODIFICATION_FAILED              | いいえ | DBセキュリティグループ修正失敗                    |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_CREATION_START              | いいえ | DBセキュリティグループルール作成開始                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_CREATION_END                | いいえ | DBセキュリティグループルール作成完了                 |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_CREATION_FAILED             | いいえ | DBセキュリティグループルール作成失敗                 |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_DELETION_START              | いいえ | DBセキュリティグループルール削除開始                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_DELETION_END                | いいえ | DBセキュリティグループルール削除完了                 |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_DELETION_FAILED             | いいえ | DBセキュリティグループルール削除失敗                 |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_MODIFICATION_START          | いいえ | DBセキュリティグループルール修正開始                  |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_MODIFICATION_END            | いいえ | DBセキュリティグループルール修正完了                 |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_MODIFICATION_FAILED         | いいえ | DBセキュリティグループルール修正失敗                 |
| PARAMETER_GROUP | PARAMETER_GROUP_CREATION_START                     | いいえ | パラメータグループ作成開始                      |
| PARAMETER_GROUP | PARAMETER_GROUP_CREATION_END                       | いいえ | パラメータグループ作成完了                     |
| PARAMETER_GROUP | PARAMETER_GROUP_CREATION_FAILED                    | いいえ | パラメータグループ作成失敗                     |
| PARAMETER_GROUP | PARAMETER_GROUP_DELETION_START                     | いいえ | パラメータグループ削除開始                      |
| PARAMETER_GROUP | PARAMETER_GROUP_DELETION_END                       | いいえ | パラメータグループ削除完了                     |
| PARAMETER_GROUP | PARAMETER_GROUP_DELETION_FAILED                    | いいえ | パラメータグループ削除失敗                     |
| MONITORING | METRIC_ALARM_TRIGGERED                             | はい | モニタリングアラーム発生                        |

* 記録は残っていますが、これ以上新規生成されないイベントコード

| イベントタイプ | イベントコード | 購読可否 | 説明 |
| - | - | - | - |
| CACHE | GROUP_CERTIFICATE_UPDATE_START | いいえ | グループ証明書更新開始 |
| CACHE | GROUP_CERTIFICATE_UPDATE_END | いいえ | グループ証明書更新完了 |
| CACHE | GROUP_CERTIFICATE_UPDATE_FAILED | いいえ | グループ証明書更新失敗 |
| CACHE | GROUP_CREATION_START | いいえ | グループ作成開始 |
| CACHE | GROUP_CREATION_END | いいえ | グループ作成完了 |
| CACHE | GROUP_CREATION_FAILED | いいえ | グループ作成失敗 |
| CACHE | GROUP_DATA_EXPORTING_START | いいえ | グループデータのエクスポート開始 |
| CACHE | GROUP_DATA_EXPORTING_END | いいえ | グループデータのエクスポート完了 |
| CACHE | GROUP_DATA_EXPORTING_FAILED | いいえ | グループデータのエクスポート失敗 |
| CACHE | GROUP_DATA_EXPORTING_RDB_CREATE_FAILED | いいえ | グループデータのエクスポートRDB作成失敗 |
| CACHE | GROUP_DATA_EXPORTING_SETTING_FAILED | いいえ | グループデータのエクスポート設定失敗 |
| CACHE | GROUP_DATA_EXPORTING_UPLOAD_FAILED | いいえ | グループデータのエクスポートアップロード失敗 |
| CACHE | GROUP_DATA_IMPORTING_START | いいえ | グループデータのインポート開始 |
| CACHE | GROUP_DATA_IMPORTING_END | いいえ | グループデータのインポート完了 |
| CACHE | GROUP_DATA_IMPORTING_DOWNLOAD_FAILED | いいえ | グループデータのインポートダウンロード失敗 |
| CACHE | GROUP_DATA_IMPORTING_RDB_CHECK_FAILED | いいえ | グループデータのインポートRDBチェック失敗 |
| CACHE | GROUP_DATA_IMPORTING_RDB_CHECKSUM_FAILED | いいえ | グループデータのインポートRDBチェックサム失敗 |
| CACHE | GROUP_DATA_IMPORTING_RDB_MEMORY_FAILED | いいえ | グループデータのインポートRDBメモリ失敗 |
| CACHE | GROUP_DATA_IMPORTING_RDB_TYPE_FAILED | いいえ | グループデータのインポートRDBタイプ失敗 |
| CACHE | GROUP_DATA_IMPORTING_RDB_VERSION_FAILED | いいえ | グループデータのインポートRDBバージョン失敗 |
| CACHE | GROUP_DATA_IMPORTING_REPLICA_CHECK_FAILED | いいえ | グループデータのインポートレプリカチェック失敗 |
| CACHE | GROUP_DATA_IMPORTING_RESTART_FAILED | いいえ | グループデータのインポート再起動失敗 |
| CACHE | GROUP_DATA_IMPORTING_SETTING_FAILED | いいえ | グループデータのインポート設定失敗 |
| CACHE | GROUP_DELETION_START | いいえ | グループ削除開始 |
| CACHE | GROUP_DELETION_END | いいえ | グループ削除完了 |
| CACHE | GROUP_DELETION_FAILED | いいえ | グループ削除失敗 |
| CACHE | GROUP_FLAVOR_MODIFICATION_START | いいえ | グループスペック変更開始 |
| CACHE | GROUP_FLAVOR_MODIFICATION_END | いいえ | グループスペック変更完了 |
| CACHE | GROUP_FLAVOR_MODIFICATION_FAILED | いいえ | グループスペック変更失敗 |
| CACHE | GROUP_MODIFICATION_START | いいえ | グループ修正開始 |
| CACHE | GROUP_MODIFICATION_END | いいえ | グループ修正完了 |
| CACHE | GROUP_MODIFICATION_FAILED | いいえ | グループ修正失敗 |
| CACHE | GROUP_RESTART_START | いいえ | グループ再起動開始 |
| CACHE | GROUP_RESTART_END | いいえ | グループ再起動完了 |
| CACHE | GROUP_RESTART_FAILED | いいえ | グループ再起動失敗 |
| CACHE | GROUP_UPGRADE_START | いいえ | グループアップグレード開始 |
| CACHE | GROUP_UPGRADE_END | いいえ | グループアップグレード完了 |
| CACHE | GROUP_UPGRADE_FAILED | いいえ | グループアップグレード失敗 |
| CACHE | GROUP_UPGRADE_HA_UPGRADE_FAILED | いいえ | グループアップグレードHA失敗 |
| CACHE | GROUP_UPGRADE_MASTER_UPGRADE_FAILED | いいえ | グループアップグレードマスター失敗 |
| CACHE | GROUP_UPGRADE_REPLICA_PROMOTE_FAILED | いいえ | グループアップグレードレプリカ昇格失敗 |
| CACHE | GROUP_UPGRADE_REPLICA_UPGRADE_FAILED | いいえ | グループアップグレードレプリカ失敗 |
| PARAMETER_GROUP | PROFILE_UPDATE_START                               | いいえ | プロファイルの更新開始                        |
| PARAMETER_GROUP | PROFILE_UPDATE_END                                 | いいえ | プロファイルの更新完了                       |
| PARAMETER_GROUP | PROFILE_UPDATE_FAILED                              | いいえ | プロファイルの更新失敗                       |
| NODE | SENTINEL_INSTANCE_RUNNING                          | いいえ | インスタンス実行                           |
| NODE | SENTINEL_INSTANCE_STOPPED                          | いいえ | インスタンス停止                           |


### イベント購読

イベントタイプ、コード、及びソースで区分してイベントを購読できます。イベントタイプで購読すると、そのイベントタイプに含まれる全てのイベントコードの通知を受け取ります。通知が広範囲にわたる場合は、イベントコードとソースで細分化して購読できます。プロジェクトメンバーのみ通知を受け取るユーザーとして選択できます。基本的にメールでイベント通知が送信され、実名認証された携帯電話番号が登録されている場合のみ、SMSで追加のイベント通知が送信されます。

![event1.PNG](https://static.toastoven.net/prod_easycache/25.09.27/event1.PNG)
![event2.PNG](https://static.toastoven.net/prod_easycache/25.09.27/event2.PNG)

❶: **イベント購読登録**をクリックすると、イベント購読を登録できるポップアップウィンドウが表示されます。
❷: 購読するイベントタイプを選択します。イベントタイプによって選択できるイベントコードが変更されます。
❸: イベントテンプレートを利用すると、テンプレートにあらかじめ定められたイベントコードを一度に入力できます。
❹: 購読するイベントコードを直接選択します。イベントテンプレートを使用した状態でイベントコードを変更した場合、イベントテンプレート項目は解除されます。
❺: 購読するイベントソースを直接選択します。 
❻: イベント通知を受け取るユーザーグループを選択します。 
❼: 通知タイプを通じて通知を受け取る方法を選択します。
❽: 有効にするかどうかを選択します。有効化を**いいえ**に選択した場合、イベント発生通知は送信されません。
