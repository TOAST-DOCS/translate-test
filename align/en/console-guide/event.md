## Event

**Database > EasyCache > Console User Guide > Event**

Events represent significant occurrences triggered by Valkey or user actions. Each event consists of an event type, timestamp, source, and message. You can view these events directly in the console or set up subscriptions to receive real-time notifications via email or SMS. The following section outlines the types of events and a list of supported events:

* Supported Event Types and Codes

| Event type | Event code                                             | Subscribable | Description                                 |
| - |----------------------------------------------------| - |------------------------------------|
| CACHE | APPLY_LATEST_PARAMETER_GROUP_START | Yes | Application of the latest parameter group started |
| CACHE | APPLY_LATEST_PARAMETER_GROUP_END | Yes | Application of the latest parameter group completed |
| CACHE | APPLY_LATEST_PARAMETER_GROUP_FAILED | Yes | Application of the latest parameter group failed |
| CACHE | AUTO_BACKUP_ACTIVATION_START | Yes | Automatic backup activation started |
| CACHE | AUTO_BACKUP_ACTIVATION_END | Yes | Automatic backup activation completed |
| CACHE | AUTO_BACKUP_ACTIVATION_FAILED | Yes | Automatic backup activation failed |
| CACHE | AUTO_BACKUP_DEACTIVATION_START | Yes | Automatic backup deactivation started |
| CACHE | AUTO_BACKUP_DEACTIVATION_END | Yes | Automatic backup deactivation completed |
| CACHE | AUTO_BACKUP_DEACTIVATION_FAILED | Yes | Automatic backup deactivation failed |
| CACHE | BACKUP_START | Yes | Backup started |
| CACHE | BACKUP_END | Yes | Backup completed |
| CACHE | BACKUP_FAILED | Yes | Backup failed |
| CACHE | BACKUP_DELETION_START | Yes | Backup deletion started |
| CACHE | BACKUP_DELETION_END | Yes | Backup deletion completed |
| CACHE | BACKUP_DELETION_FAILED | Yes | Backup deletion failed |
| CACHE | BACKUP_MIGRATE_START | No | Backup migration started |
| CACHE | BACKUP_MIGRATE_END | No | Backup migration completed |
| CACHE | BACKUP_MIGRATE_DOWNLOAD_FAILED | No | Backup migration download failed |
| CACHE | BACKUP_MIGRATE_RDB_CHECK_FAILED | No | Backup migration RDB check failed |
| CACHE | BACKUP_MIGRATE_RDB_CHECKSUM_FAILED | No | Backup migration RDB checksum failed |
| CACHE | BACKUP_MIGRATE_RDB_MEMORY_FAILED | No | Backup migration RDB memory failed |
| CACHE | BACKUP_MIGRATE_RDB_TYPE_FAILED | No | Backup migration RDB type failed |
| CACHE | BACKUP_MIGRATE_RDB_VERSION_FAILED | No | Backup migration RDB version failed |
| CACHE | BACKUP_MIGRATE_REPLICA_CHECK_FAILED | No | Backup migration replica check failed |
| CACHE | BACKUP_MIGRATE_RESTART_FAILED | No | Backup migration restart failed |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_START | Yes | Backup restore started with existing cache |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_END | Yes | Backup restore completed with existing cache |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_FAILED | Yes | Backup restore failed with existing cache |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_DOWNLOAD_FAILED | Yes | Backup restore download failed with existing cache |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_CHECK_FAILED | Yes | Backup restore with existing cache RDB check failed |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_CHECKSUM_FAILED | Yes | Restoring backup to existing cache failed with RDB checksum |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_MEMORY_FAILED | Yes | Restoring backup to existing cache failed with RDB memory |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_TYPE_FAILED | Yes | Restoring backup to existing cache failed with RDB type |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RDB_VERSION_FAILED | Yes | Restoring backup to existing cache failed with RDB version |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_REPLICA_CHECK_FAILED | Yes | Restoring backup to existing cache failed with replica check |
| CACHE | BACKUP_RESTORE_EXISTING_CACHE_RESTART_FAILED | Yes | Restoring backup to existing cache failed with restart |
| CACHE | BACKUP_RESTORE_NEW_CACHE_START | Yes | Backup restore started with new cache |
| CACHE | BACKUP_RESTORE_NEW_CACHE_END | Yes | Backup restore completed with new cache |
| CACHE | BACKUP_RESTORE_NEW_CACHE_FAILED | Yes | Backup restore failed with new cache |
| CACHE | CACHE_CERTIFICATE_UPDATE_START | Yes | Cache certificate renewal started |
| CACHE | CACHE_CERTIFICATE_UPDATE_END | Yes | Cache certificate renewal completed |
| CACHE | CACHE_CERTIFICATE_UPDATE_FAILED | Yes | Cache certificate renewal failed |
| CACHE | CACHE_CREATION_START | Yes | Cache creation started |
| CACHE | CACHE_CREATION_END | Yes | Cache creation completed |
| CACHE | CACHE_CREATION_FAILED | Yes | Cache creation failed |
| CACHE | CACHE_DATA_EXPORTING_START | Yes | Cache data export started |
| CACHE | CACHE_DATA_EXPORTING_END | Yes | Cache data export completed |
| CACHE | CACHE_DATA_EXPORTING_FAILED | Yes | Cache data export failed |
| CACHE | CACHE_DATA_EXPORTING_RDB_CREATE_FAILED | Yes | Cache data export RDB creation failed |
| CACHE | CACHE_DATA_EXPORTING_SETTING_FAILED | Yes | Cache data export setting failed |
| CACHE | CACHE_DATA_EXPORTING_UPLOAD_FAILED | Yes | Cache data export upload failed |
| CACHE | CACHE_DATA_IMPORTING_START | Yes | Cache data import started |
| CACHE | CACHE_DATA_IMPORTING_END | Yes | Cache data import completed |
| CACHE | CACHE_DATA_IMPORTING_FAILED | Yes | Fetching cache data failed |
| CACHE | CACHE_DATA_IMPORTING_DOWNLOAD_FAILED | Yes | Cache data import download failed |
| CACHE | CACHE_DATA_IMPORTING_RDB_CHECK_FAILED | Yes | Cache data import RDB check failed |
| CACHE | CACHE_DATA_IMPORTING_RDB_CHECKSUM_FAILED | Yes | Cache data import RDB checksum failed |
| CACHE | CACHE_DATA_IMPORTING_RDB_MEMORY_FAILED | Yes | Cache data import RDB memory failed |
| CACHE | CACHE_DATA_IMPORTING_RDB_TYPE_FAILED | Yes | Cache data import RDB type failed |
| CACHE | CACHE_DATA_IMPORTING_RDB_VERSION_FAILED | Yes | Cache data import RDB version failed |
| CACHE | CACHE_DATA_IMPORTING_REPLICA_CHECK_FAILED | Yes | Checking cache data import replica failed |
| CACHE | CACHE_DATA_IMPORTING_RESTART_FAILED | Yes | Restarting cache data import failed |
| CACHE | CACHE_DATA_IMPORTING_SETTING_FAILED | Yes | Setting cache data import failed |
| CACHE | CACHE_DELETION_START | Yes | Deleting cache started |
| CACHE | CACHE_DELETION_END | Yes | Deleting cache completed |
| CACHE | CACHE_DELETION_FAILED | Yes | Deleting cache failed |
| CACHE | CACHE_DELETION_PROTECTION_DISABLING_START | Yes | Disabling cache deletion protection started |
| CACHE | CACHE_DELETION_PROTECTION_DISABLING_END | Yes | Disabling cache deletion protection completed |
| CACHE | CACHE_DELETION_PROTECTION_DISABLING_FAILED | Yes | Disabling cache deletion protection failed |
| CACHE | CACHE_DELETION_PROTECTION_ENABLING_START | Yes | Cache deletion protection activation started |
| CACHE | CACHE_DELETION_PROTECTION_ENABLING_END | Yes | Cache deletion protection activation completed |
| CACHE | CACHE_DELETION_PROTECTION_ENABLING_FAILED | Yes | Cache deletion protection activation failed |
| CACHE | CACHE_DETAIL_MODIFICATION_START | Yes | Cache detail modification started |
| CACHE | CACHE_DETAIL_MODIFICATION_END | Yes | Cache detail modification completed |
| CACHE | CACHE_DETAIL_MODIFICATION_FAILED | Yes | Cache detail modification failed |
| CACHE | CACHE_FLAVOR_MODIFICATION_START | Yes | Cache specification modification started |
| CACHE | CACHE_FLAVOR_MODIFICATION_END | Yes | Cache specification modification completed |
| CACHE | CACHE_FLAVOR_MODIFICATION_FAILED | Yes | Cache specification modification failed |
| CACHE | CACHE_HIGH_AVAILABILITY_REPAIR_START | Yes | Cache high availability repair started |
| CACHE | CACHE_HIGH_AVAILABILITY_REPAIR_END | Yes | Cache high availability repair completed |
| CACHE | CACHE_HIGH_AVAILABILITY_REPAIR_FAILED | Yes | Cache high availability repair failed |
| CACHE | CACHE_MASTER_ROLE_CHANGING_START | Yes | Cache master role change started |
| CACHE | CACHE_MASTER_ROLE_CHANGING_END | Yes | Cache master role change completed |
| CACHE | CACHE_MASTER_ROLE_CHANGING_FAILED | Yes | Cache master role change failed |
| CACHE | CACHE_MODIFICATION_START | Yes | Cache modification started |
| CACHE | CACHE_MODIFICATION_END | Yes | Cache modification completed |
| CACHE | CACHE_MODIFICATION_FAILED | Yes | Cache modification failed |
| CACHE | CACHE_RESTART_START | Yes | Cache restart started |
| CACHE | CACHE_RESTART_END | Yes | Cache restart completed |
| CACHE | CACHE_RESTART_FAILED | Yes | Cache restart failed |
| CACHE | CACHE_STARTING_START | Yes | Cache starting started |
| CACHE | CACHE_STARTING_END | Yes | Cache starting completed |
| CACHE | CACHE_STARTING_FAILED | Yes | Cache starting failed |
| CACHE | CACHE_STOPPING_START | Yes | Cache stopping started |
| CACHE | CACHE_STOPPING_END | Yes | Cache stopping Complete |
| CACHE | CACHE_STOPPING_FAILED | Yes | Cache stopping Failed |
| CACHE | CACHE_UPGRADE_START | Yes | Cache upgrade Start |
| CACHE | CACHE_UPGRADE_END | Yes | Cache upgrade Complete |
| CACHE | CACHE_UPGRADE_FAILED | Yes | Cache upgrade Failed |
| CACHE | CACHE_UPGRADE_HA_UPGRADE_FAILED | Yes | Cache upgrade HA failed |
| CACHE | CACHE_UPGRADE_MASTER_UPGRADE_FAILED | Yes | Cache upgrade master failed |
| CACHE | CACHE_UPGRADE_REPLICA_PROMOTE_FAILED | Yes | Cache upgrade replica promotion failed |
| CACHE | CACHE_UPGRADE_REPLICA_UPGRADE_FAILED | Yes | Cache upgrade replica failed |
| CACHE | FAILOVER_DNS_FAILED | No | DNS renewal failed |
| CACHE | FAILOVER_DNSFAIL | Yes | Failover DNS failed |
| CACHE | FAILOVER_EXECUTED | Yes | Failover occurred |
| CACHE | FLOATING_IP_ATTACHING_START | Yes | Floating IP connection started |
| CACHE | FLOATING_IP_ATTACHING_END | Yes | Floating IP attachment completed |
| CACHE | FLOATING_IP_ATTACHING_FAILED | Yes | Floating IP attachment failed |
| CACHE | FLOATING_IP_DETACHING_START | Yes | Floating IP detachment started |
| CACHE | FLOATING_IP_DETACHING_END | Yes | Floating IP detachment complete |
| CACHE | FLOATING_IP_DETACHING_FAILED | Yes | Floating IP detachment failed |
| CACHE | HA_NODE_CREATION_START | Yes | HA node creation started |
| CACHE | HA_NODE_CREATION_END | Yes | HA node creation completed |
| CACHE | HA_NODE_CREATION_FAILED | Yes | HA node creation failed |
| CACHE | HA_NODE_DELETION_START | Yes | HA node deletion start |
| CACHE | HA_NODE_DELETION_END | Yes | HA node deletion complete |
| CACHE | NODE_OS_UPGRADE_START | Yes | Node OS upgrade started |
| CACHE | NODE_OS_UPGRADE_END | Yes | Node OS upgrade complete |
| CACHE | NODE_OS_UPGRADE_FAILED | Yes | Node OS upgrade failed |
| CACHE | READONLY_DOMAIN_ATTACHING_START | Yes | Read-only domain attachment started |
| CACHE | READONLY_DOMAIN_ATTACHING_END | Yes | Read-only domain attachment completed |
| CACHE | READONLY_DOMAIN_ATTACHING_FAILED | Yes | Read-only domain attachment failed |
| CACHE | READONLY_DOMAIN_DETACHING_START | Yes | Read-only domain detachment started |
| CACHE | READONLY_DOMAIN_DETACHING_END | Yes | Read-only domain detachment completed |
| CACHE | READONLY_DOMAIN_DETACHING_FAILED | Yes | Read-only domain detachment failed |
| CACHE | READONLY_DOMAIN_UPDATE_START | Yes | Read-only domain update started |
| CACHE | READONLY_DOMAIN_UPDATE_END | Yes | Read-only domain update completed |
| CACHE | READONLY_DOMAIN_UPDATE_FAILED | Yes | Read-only domain update failed |
| CACHE | SENTINEL_CREATION_START | No | Sentinel node creation started |
| CACHE | SENTINEL_CREATION_END | No | Sentinel node creation completed |
| CACHE | SENTINEL_CREATION_FAILED | No | Sentinel node creation failed |
| CACHE | SENTINEL_DELETION_START | No | Sentinel node deletion started |
| CACHE | SENTINEL_DELETION_END | No | Sentinel node deletion completed |
| CACHE | SENTINEL_DELETION_FAILED | No | Sentinel node deletion failed |
| CACHE | SENTINEL_FAILOVER | No | Failover occurred |
| CACHE | SENTINEL_FAILOVER_DNSFAIL | No | Failover DNS failed |
| CACHE | SENTINEL_QUORUM_UPDATE_START | Yes | Sentinel quorum update started |
| CACHE | SENTINEL_QUORUM_UPDATE_END | Yes | Sentinel quorum update completed |
| CACHE | SENTINEL_QUORUM_UPDATE_FAILED | Yes | Sentinel quorum update failed |
| CACHE | SLAVE_NODE_PROMOTION_START | Yes | Replica node promotion started |
| CACHE | SLAVE_NODE_PROMOTION_END | Yes | Replica node promotion completed |
| CACHE | SLAVE_NODE_PROMOTION_FAILED | Yes | Replica node promotion failed |
| NODE | NODE_DELETION_START | Yes | Node deletion started |
| NODE | NODE_DELETION_END | Yes | Node deletion completed |
| NODE | NODE_DELETION_FAILED | Yes | Node deletion failed |
| NODE | NODE_DOWN_DETECTED | Yes | Node down |
| NODE | NODE_FLAVOR_MODIFICATION_START | Yes | Node specification modification started |
| NODE | NODE_FLAVOR_MODIFICATION_END | Yes | Node specification modification completed |
| NODE | NODE_FLAVOR_MODIFICATION_FAILED | Yes | Node specification modification failed |
| NODE | NODE_PLANNED_MIGRATION_START | Yes | Node plan migration started |
| NODE | NODE_PLANNED_MIGRATION_END | Yes | Node plan migration completed |
| NODE | NODE_PLANNED_MIGRATION_FAILED | Yes | Node plan migration failed |
| NODE | NODE_RECOVERED | Yes | Node running |
| NODE | NODE_UPGRADE_START | Yes | Node engine upgrade started |
| NODE | NODE_UPGRADE_END | Yes | Node engine upgrade completed |
| NODE | NODE_UPGRADE_FAILED | Yes | Node engine upgrade failed |
| NODE | NODE_UPGRADE_DOWNLOAD_FAILED | Yes | Node engine upgrade download failed |
| NODE | NODE_UPGRADE_PARAMETER_GROUP_UPDATE_FAILED | Yes | Node engine upgrade parameter group update failed |
| NODE | NODE_UPGRADE_REDIS_N_SENTINEL_START_FAILED | Yes | Node engine upgrade Redis and Sentinel start failed |
| NODE | NODE_UPGRADE_REDIS_N_SENTINEL_STOP_FAILED | Yes | Node engine upgrade Redis and Sentinel stop failed |
| NODE | NODE_UPGRADE_REDIS_UPGRADE_FAILED | Yes | Node engine upgrade Redis upgrade failed |
| NODE | NODE_UPGRADE_REPLICA_CHECK_FAILED | Yes | Node engine upgrade replica check failed |
| NODE | NODE_UPGRADE_RPM_DELETE_FAILED | Yes | Node Engine Upgrade RPM deletion failed |
| NODE | NODE_UPGRADE_SENTINEL_START_FAILED | Yes | Node Engine Upgrade Sentinel start failed |
| NODE | NODE_UPGRADE_SENTINEL_STOP_FAILED | Yes | Node Engine Upgrade Sentinel stop failed |
| NODE | SLAVE_NODE_CREATION_START | Yes | Replica node creation started |
| NODE | SLAVE_NODE_CREATION_END | Yes | Replica node creation completed |
| NODE | SLAVE_NODE_CREATION_FAILED | Yes | Replica node creation failed |
| NODE | STATUS_CHANGED_DISABLED | No | Disabled |
| NODE | STATUS_CHANGED_ENABLED | No | Enabled |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_CREATION_START | No | DB Security Group Creation started |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_CREATION_END | No | DB Security Group Creation completed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_CREATION_FAILED | No | DB Security Group Creation failed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_DELETION_START | No | DB Security Group Deletion started |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_DELETION_END | No | DB Security Group Deletion completed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_DELETION_FAILED | No | DB Security Group Deletion failed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_MODIFICATION_START | No | DB Security Group Modification started |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_MODIFICATION_END | No | DB Security Group Modification completed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_MODIFICATION_FAILED | No | DB Security Group Modification failed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_CREATION_START | No | DB Security Group Rule Creation started |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_CREATION_END | No | DB Security Group Rule Creation completed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_CREATION_FAILED | No | DB Security Group Rule Creation failed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_DELETION_START | No | DB Security Group Rule Deletion started |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_DELETION_END | No | DB Security Group Rule Deletion completed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_DELETION_FAILED | No | DB Security Group Rule Deletion failed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_MODIFICATION_START | No | DB Security Group Rule Modification started |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_MODIFICATION_END | No | DB Security Group Rule Modification completed |
| DB_SECURITY_GROUP | DB_SECURITY_GROUP_RULE_MODIFICATION_FAILED | No | DB security group rule modification failed |
| PARAMETER_GROUP | PARAMETER_GROUP_CREATION_START | No | Parameter group creation started |
| PARAMETER_GROUP | PARAMETER_GROUP_CREATION_END | No | Parameter group creation completed |
| PARAMETER_GROUP | PARAMETER_GROUP_CREATION_FAILED | No | Parameter group creation failed |
| PARAMETER_GROUP | PARAMETER_GROUP_DELETION_START | No | Parameter group deletion started |
| PARAMETER_GROUP | PARAMETER_GROUP_DELETION_END | No | Parameter group deletion completed |
| PARAMETER_GROUP | PARAMETER_GROUP_DELETION_FAILED | No | Parameter group deletion failed |
| MONITORING | METRIC_ALARM_TRIGGERED | Yes | Monitoring alarm triggered |

* Deprecated Event Codes

| Event type | Event code | Subscribable | Description |
| - | - | - | - |
| CACHE | GROUP_CERTIFICATE_UPDATE_START | No | Group certificate renewal started |
| CACHE | GROUP_CERTIFICATE_UPDATE_END | No | Group certificate renewal completed |
| CACHE | GROUP_CERTIFICATE_UPDATE_FAILED | No | Group certificate renewal failed |
| CACHE | GROUP_CREATION_START | No | Group creation started |
| CACHE | GROUP_CREATION_END | No | Group creation completed |
| CACHE | GROUP_CREATION_FAILED | No | Group creation failed |
| CACHE | GROUP_DATA_EXPORTING_START | No | Group data export started |
| CACHE | GROUP_DATA_EXPORTING_END | No | Group data export completed |
| CACHE | GROUP_DATA_EXPORTING_FAILED | No | Group data export failed |
| CACHE | GROUP_DATA_EXPORTING_RDB_CREATE_FAILED | No | Group data export RDB creation failed |
| CACHE | GROUP_DATA_EXPORTING_SETTING_FAILED | No | Group data export setup failed |
| CACHE | GROUP_DATA_EXPORTING_UPLOAD_FAILED | No | Group data export upload failed |
| CACHE | GROUP_DATA_IMPORTING_START | No | Group data import start |
| CACHE | GROUP_DATA_IMPORTING_END | No | Group data import complete |
| CACHE | GROUP_DATA_IMPORTING_DOWNLOAD_FAILED | No | Group data import download failed |
| CACHE | GROUP_DATA_IMPORTING_RDB_CHECK_FAILED | No | Group data import RDB check failed |
| CACHE | GROUP_DATA_IMPORTING_RDB_CHECKSUM_FAILED | No | Group data import RDB checksum failed |
| CACHE | GROUP_DATA_IMPORTING_RDB_MEMORY_FAILED | No | Group data import RDB memory failed |
| CACHE | GROUP_DATA_IMPORTING_RDB_TYPE_FAILED | No | Group data import RDB type failed |
| CACHE | GROUP_DATA_IMPORTING_RDB_VERSION_FAILED | No | Group data import RDB version failed |
| CACHE | GROUP_DATA_IMPORTING_REPLICA_CHECK_FAILED | No | Group data import replica check failed |
| CACHE | GROUP_DATA_IMPORTING_RESTART_FAILED | No | Group data import restart failed |
| CACHE | GROUP_DATA_IMPORTING_SETTING_FAILED | No | Setting up group data import failed |
| CACHE | GROUP_DELETION_START | No | Group deletion started |
| CACHE | GROUP_DELETION_END | No | Group deletion completed |
| CACHE | GROUP_DELETION_FAILED | No | Group deletion failed |
| CACHE | GROUP_FLAVOR_MODIFICATION_START | No | Group specification modification started |
| CACHE | GROUP_FLAVOR_MODIFICATION_END | No | Group specification modification completed |
| CACHE | GROUP_FLAVOR_MODIFICATION_FAILED | No | Group specification modification failed |
| CACHE | GROUP_MODIFICATION_START | No | Group modification started |
| CACHE | GROUP_MODIFICATION_END | No | Group modification completed |
| CACHE | GROUP_MODIFICATION_FAILED | No | Group modification failed |
| CACHE | GROUP_RESTART_START | No | Group restart started |
| CACHE | GROUP_RESTART_END | No | Group restart completed |
| CACHE | GROUP_RESTART_FAILED | No | Group restart failed |
| CACHE | GROUP_UPGRADE_START | No | Group upgrade started |
| CACHE | GROUP_UPGRADE_END | No | Group upgrade completed |
| CACHE | GROUP_UPGRADE_FAILED | No | Group upgrade failed |
| CACHE | GROUP_UPGRADE_HA_UPGRADE_FAILED | No | Group upgrade HA failed |
| CACHE | GROUP_UPGRADE_MASTER_UPGRADE_FAILED | No | Group upgrade Master failed |
| CACHE | GROUP_UPGRADE_REPLICA_PROMOTE_FAILED | No | Group upgrade Replica Promotion failed |
| CACHE | GROUP_UPGRADE_REPLICA_UPGRADE_FAILED | No | Group upgrade Replica failed |
| PARAMETER_GROUP | PROFILE_UPDATE_START | No | Profile update started |
| PARAMETER_GROUP | PROFILE_UPDATE_END | No | Profile update completed |
| PARAMETER_GROUP | PROFILE_UPDATE_FAILED | No | Profile update failed |
| NODE | SENTINEL_INSTANCE_RUNNING | No | Instance running |
| NODE | SENTINEL_INSTANCE_STOPPED | No | Instance stopped |


### Event Subscription

You can subscribe to events filtered by event type, code, or source. Subscribing to an event type allows you to receive notifications for all event codes within that category. For more specific alerts, you can refine your subscription by selecting individual event codes and sources. Only project members can be selected as notification recipients. By default, notifications are sent via email; SMS alerts are sent only if a mobile number is registered with a real name.

![event1.PNG](https://static.toastoven.net/prod_easycache/25.09.27/event1.PNG)
![event2.PNG](https://static.toastoven.net/prod_easycache/25.09.27/event2.PNG)

❶: Click **Register Event Subscription** to open the registration popup window.
❷: Select an event type. The available event codes will update based on the selected type.
❸: Use an Event Template to populate multiple predefined event codes at once quickly.
❹: Select event codes manually. If you modify the event codes while using a template, the Event Template selection will be deselected.
❺: Select the event sources you wish to subscribe to.
❻: Select a user group to receive the event notifications.
❼: Select a notification method under the Notification Type section.
❽: Set the status to Enabled or Disabled. If set to **No**, notifications will not be sent even when events occur.