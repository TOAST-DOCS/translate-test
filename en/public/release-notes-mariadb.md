<!-- machine_translated: true -->

<!-- pre-align:aligned sig=227955ea3124 -->

<a id="database-rds-for-mariadb-release-notes"></a>
## Database > RDS for MariaDB > Release Notes { #database-rds-for-mariadb-release-notes }

<a id="september-15-2026"></a>
## September 15, 2026 { #september-15-2026 }

<a id="september-15-2026-added-features"></a>
### Added Features { #september-15-2026-added-features }

* Added an option to restart the operating system when restarting a DB instance
* Added a feature to stop high availability instances

<a id="september-15-2026-feature-updates"></a>
### Feature Updates { #september-15-2026-feature-updates }

* Changed DB instance type terminology
    * Master → Primary
    * Candidate Master → Standby
    * Read Only Slave → Read Replica
    * Failed Master → Failed Over Primary
* Improved so that properties that must be applied to a DB instance group are now configured by modifying the DB instance group
* Improved to allow viewing past monitoring metrics after security patches and OS upgrades

<a id="september-15-2026-bug-fixes"></a>
### Bug Fixes { #september-15-2026-bug-fixes }

* Fixed a bug where the Object Storage tenant ID was exposed as-is in CloudTrail
* Fixed a bug where creating, modifying, or deleting security group rules intermittently failed when there were many security group rules
* Fixed a bug where a high availability DB could intermittently fail to boot due to network communication failures
* Fixed a bug where garbage security group rules intermittently remained when a DB port change failed

<a id="july-14-2026"></a>
## July 14, 2026 { #july-14-2026 }

<a id="feature-updates"></a>
### Feature Updates { #feature-updates }

* Added MariaDB 10.11.18, 11.4.12, 11.8.8 version

<a id="bug-fixes"></a>
### Bug Fixes { #bug-fixes }

* Fixed an issue where the security patch was not performed when a single instance subject to security patch was changed to a high availability instance

<a id="may-12-2026"></a>
## May 12, 2026 { #may-12-2026 }

<a id="may-12-2026-feature-updates"></a>
### Feature Updates { #may-12-2026-feature-updates }

* Added security patch feature
    * Security patches for security vulnerabilities (CVEs) discovered in the OS can be performed as maintenance tasks.
    * For more information, refer to the [Security patch](/Database/RDS%20for%20MariaDB/en/db-instance/#security-patch) documentation.
* Added `SELECT` option in addition to the existing `INSERT` option for high availability Ping check method
* Added MariaDB 10.6.25, 10.11.16, 11.4.10, 11.8.6 version
* Restricted new creation due to MariaDB 10.3 and 10.6 EOL (End of Life)
* Added and updated API v4.0
    * Added the View High Availability Information API.

<a id="march-10-2026"></a>
## March 10, 2026 { #march-10-2026 }

<a id="march-10-2026-feature-updates"></a>
### Feature Updates { #march-10-2026-feature-updates }

* Added API v4.0
    * For more information, see [API v4.0 guide](/Database/RDS%20for%20MariaDB/en/api-guide-v4.0/) document.
* Added snapshot backup feature
    * Perform backups using Cinder storage snapshots with zero impact on DB performance

<a id="january-13-2026"></a>
## January 13, 2026 { #january-13-2026 }

<a id="january-13-2026-feature-updates"></a>
### Feature Updates { #january-13-2026-feature-updates }

* Added maintenance feature
    * Applied various DB instance modifications during your scheduled maintenance duration
* Updated to grant ROLE_ADMIN privileges when the Direct Control for DB Schemas & Users setting is enabled

<a id="november-11-2025"></a>
## November 11, 2025 { #november-11-2025 }

<a id="november-11-2025-feature-updates"></a>
### Feature Updates { #november-11-2025-feature-updates }

* Improved to record the cause of backup failure due to Lock acquisition failure in the event log.

<a id="november-11-2025-bug-fixes"></a>
### Bug Fixes { #november-11-2025-bug-fixes }

* Fixed an issue where the failover status persisted when failover failed.
* Fixed an issue where DB instances stopped before the July deployment could not be started.
* Fixed an issue where the latest parameter group would not be applied after selecting multiple DB instances when using a different parameter group for read replicas.
* Fixed an issue where unchangeable values would be changed when resetting a parameter group.

<a id="september-09-2025"></a>
## September 09, 2025 { #september-09-2025 }

<a id="september-09-2025-feature-updates"></a>
### Feature Updates { #september-09-2025-feature-updates }

* Added MariaDB 10.6.22, 10.11.13, 11.4.7 version

<a id="september-09-2025-bug-fixes"></a>
### Bug Fixes { #september-09-2025-bug-fixes }

* Fixed an issue where the standby master name was displayed with the current name entered when creating a high-availability instance after clicking on an already created high-availability instance.
* Fixed an issue where the name of a read replica added to high-availability could not be modified.
* Fixed an issue where the [Add VIP] drop-down menu was activated when adding a VIP to a DB instance was not possible.
* Fixed an issue where the internal IP would intermittently disappear when DHCP renewal failed.
* Fixed an issue where high-availability would stop functioning if a read replica creation failed on a high-availability instance.
* Fixed an issue where subscription notifications would not work when multiple events subscribed to by the same organization occurred.

<a id="july-15-2025"></a>
## July 15, 2025 { #july-15-2025 }

<a id="july-15-2025-feature-updates"></a>
### Feature Updates { #july-15-2025-feature-updates }

* Improved to disallow specifying the DB port type in egress rules of DB security groups
* Changed to require entering the name of the candidate master for high-availability DB instances
* Improved to allow DB instance resources to be checked in Resource Watcher
* Fixed billing so that the failover master is charged normally until it is deleted
* Improved to display accurate error messages when failover masters cannot be recovered due to missing binary logs

<a id="july-15-2025-bug-fixes"></a>
### Bug Fixes { #july-15-2025-bug-fixes }

* Fixed an issue where backup failed when special characters were included in the export path
* Fixed an issue where the user group was not deleted from event subscriptions when the user group was deleted
* Improved to display accurate error messages when deleting duplicate notification groups

<a id="may-13-2025"></a>
## May 13, 2025 { #may-13-2025 }

<a id="may-13-2025-feature-updates"></a>
### Feature Updates { #may-13-2025-feature-updates }

* Improved to support using VIP (Virtual IP)
    * VIP is now issued for newly created DB instances and is always configured to point to the master DB instance. For existing DB instances, VIPs can be issued manually by clicking the [Add VIP] button in the console
* Improved to allow explicitly disabling High Availability via the console when it is in an abnormal state
* Improved to allow entering decimal values in monitoring settings
* Improved to allow entering Korean characters in user group names
* Improved the change history modal window to check whether to restart when changing parameter groups on DB instances

<a id="april-15-2025"></a>
## April 15, 2025 { #april-15-2025 }

<a id="april-15-2025-feature-updates"></a>
### Feature Updates { #april-15-2025-feature-updates }

* Added and modified API v3.0
    * Added the API to list Log files
    * Added the Export Log file API

<a id="february-11-2025"></a>
## February 11, 2025 { #february-11-2025 }

<a id="february-11-2025-bug-fixes"></a>
### Bug Fixes { #february-11-2025-bug-fixes }

* Fixed an issue where deleted notification group information appears on the view DB instance details screen

<a id="november-12-2024"></a>
## November 12, 2024 { #november-12-2024 }

<a id="november-12-2024-feature-updates"></a>
### Feature Updates { #november-12-2024-feature-updates }

* Added storage auto scaling feature
* Improved so that the DB instance is not restarted when the storage size is scaled up
* Separated the storage size scaling feature, which was included in the Modify DB Instance feature, into a dropdown menu
* Changed so that the paused state is maintained when the standby master is rebuilt while high availability is paused
* Removed the backup retry expiration time setting from the automatic backup settings and improved backups to be retried within the backup window time range
* Added the versions of MariaDB 10.11.7 and MariaDB 10.11.8

<a id="september-10-2024"></a>
## September 10, 2024 { #september-10-2024 }

<a id="september-10-2024-feature-updates"></a>
### Feature Updates { #september-10-2024-feature-updates }

* Added incremental backup feature
* Improved so that you can choose whether to delete automatic backups when deleting a DB instance

<a id="july-9-2024"></a>
## July 9, 2024 { #july-9-2024 }

<a id="july-9-2024-feature-updates"></a>
### Feature Updates { #july-9-2024-feature-updates }

* Added the foreign_key_checks setting procedure

<a id="july-9-2024-bug-fixes"></a>
### Bug Fixes { #july-9-2024-bug-fixes }

* Fixed an issue where snapshot restoration with a backup of a deleted DB instance was not possible

<a id="june-11-2024"></a>
## June 11, 2024 { #june-11-2024 }

<a id="june-11-2024-feature-updates"></a>
### Feature Updates { #june-11-2024-feature-updates }

* Added the feature to upgrade DB instance OS

<a id="may-14-2024"></a>
## May 14, 2024 { #may-14-2024 }

<a id="may-14-2024-feature-updates"></a>
### Feature Updates { #may-14-2024-feature-updates }

* Added Slow Query analytics
    * Provided the Analytics tab with Slow Query analysis, Process List, and InnoDB Status monitoring features
    * Provided the feature to disable Slow Query Analytics on the Edit DB Instance screen
* Improved to see which parameter items actually change when applying parameter group changes
* Improved to expose warning text and raise an event when high availability status is abnormal
* Improved to select a storage type when creating read replicas
* Added MariaDB 10.6.16 version
* Added and modified API v3.0
    * Added the `storage.storageType` field to DB instance replicate API request
    * Added the `notificationGroupIds` field to DB instance detail API response
    * Improved the ability to use project integration appkeys when calling API v3.0

<a id="march-12-2024"></a>
## March 12, 2024 { #march-12-2024 }

<a id="march-12-2024-feature-updates"></a>
### Feature Updates { #march-12-2024-feature-updates }

* Added the feature to promote candidate masters
* Added the feature to force promote candidate masters
* Added the feature to wait for replication delay on restart with failover
* Added the feature to turn off DB schema & user direct control settings

<a id="february-15-2024"></a>
## February 15, 2024 { #february-15-2024 }

<a id="february-15-2024-feature-updates"></a>
### Feature Updates { #february-15-2024-feature-updates }

* Added DB schema & user-directed control settings
* Improved to better identify connected notification groups
    * Exposed connected notification group information on the DB instance view details screen

<a id="january-9-2024"></a>
## January 9, 2024 { #january-9-2024 }

<a id="january-9-2024-feature-updates"></a>
### Feature Updates { #january-9-2024-feature-updates }

* Improved to control the timing of failover whe upgrading the DB engine version for high availability instances
* Improved to allow you to operate the hypervisor migration feature for each DB instance

<a id="december-19-2023"></a>
## December 19, 2023 { #december-19-2023 }

<a id="december-19-2023-feature-updates"></a>
### Feature Updates { #december-19-2023-feature-updates }

* Improved to make it easier to identify DB instances to which the changed parameter will be applied
    * Added the 'Apply' button in front of the target name to apply the changed parameter on the DB instance list screen.
    * Added the 'Apply' button to the parameter group item on the detail view screen of the DB instance to which the changed parameter will be applied.
    * Add filter option that requires application of changed parameters
* Changed to retrieve servers that have been deleted within the last month when checking the View deleted servers on the server dashboard screen

<a id="november-14-2023"></a>
## November 14, 2023 { #november-14-2023 }

<a id="november-14-2023-feature-updates"></a>
### Feature Updates { #november-14-2023-feature-updates }

* Added forced promotion of DB instances
* Improved to allow you to select notification type when subscribing to events
* Added and modified API v3.0
    * Added the Export after backing up DB instance API

<a id="october-17-2023"></a>
## October 17, 2023 { #october-17-2023 }

<a id="october-17-2023-feature-updates"></a>
### Feature Updates { #october-17-2023-feature-updates }

* Improved to create instances by using read replica backups when configuring high availability and adding read replicas
* Added the versions of MariaDB 10.6.11 and MariaDB 10.6.12
* Added and modified API v3.0
    * Added the API to list the last query to be restored
    * Added `needToApplyParameterGroup`, `needMigration`, and `supportDbVersionUpgrade` fields to the List DB Instance API response.

<a id="july-11-2023"></a>
## July 11, 2023 { #july-11-2023 }

<a id="july-11-2023-feature-updates"></a>
### Feature Updates { #july-11-2023-feature-updates }

* Added DB instance deletion protection feature

<a id="june-13-2023"></a>
## June 13, 2023 { #june-13-2023 }

<a id="june-13-2023-feature-updates"></a>
### Feature Updates { #june-13-2023-feature-updates }

* Added rebuild support when a candidate master fails
    * The DB instance on the candidate master does not change, so the fixed IP address does not change
    * All data in the database are deleted, and restored with the data of the master
* Improved so that all users in the organization and project can be added when adding users to a user group

<a id="may-16-2023"></a>
## May 16, 2023 { #may-16-2023 }

<a id="may-16-2023-feature-updates"></a>
### Feature Updates { #may-16-2023-feature-updates }

* Made improvements so that the user interface is consistent with NHN Cloud services
* Made modifications so that manual backup is not deleted even when DB instances are deleted
* Added parameter group feature
    * The database settings of DB instance can be freely changed
    * Applicable to multiple instances
    * Changes to settings in an existing DB instance are migrated to a parameter group with the same name as the DB instance
* Added DB security group feature
    * The access control of DB instance can be freely set
    * Applicable to multiple instances
    * Access control rules set on existing DB instances are migrated to the DB security group named as `{DB instance name}__{DB instance ID}` rule
* Provided a screen to view DB instances grouped by replication arrangements
* Displayed candidate master to console
    * Available to secure storage by deleting the binary log of candidate master
    * Various logs of candidate master can be checked and downloaded
* Rebuilding read replica is available
    * The fixed IP address does not change because the DB instance of the read replica remain unchanged
    * All data in the database are deleted, and restored with the data of the master
* Recovery of master with a completed failover
    * High availability recovery of a new master and a master with a completed failover is available
    * Recovery can fail, and an unrecoverable master with a completed failover can be rebuilt
* Rebuilding master with a completed failover
    * The fixed IP does not change because DB instance of the master with a completed failover remain unchanged
    * All data in the database are deleted, and restored with the data of the master

<a id="may-16-2023-bug-fixes"></a>
### Bug Fixes { #may-16-2023-bug-fixes }

* Fixed an issue where point-in-time recovery is not possible with a read replica backup

<a id="february-14-2023"></a>
## February 14, 2023 { #february-14-2023 }

<a id="february-14-2023-feature-updates"></a>
### Feature Updates { #february-14-2023-feature-updates }

* Made modifications so that the Max Connection value is displayed on the Connection chart in MariaDB metrics of the server dashboard

<a id="february-14-2023-bug-fixes"></a>
### Bug Fixes { #february-14-2023-bug-fixes }

* Fixed an issue where, when an error occurs in the IAM console, the page is not moved to an appropirate error page
* Fixed an issue where, when changing the DB instance type or expanding storage using failover, the Ping interval is set to default

<a id="january-10-2023"></a>
## January 10, 2023 { #january-10-2023 }

<a id="january-10-2023-feature-updates"></a>
### Feature Updates { #january-10-2023-feature-updates }

* Made modifications not to allow duplicate notification group names

<a id="january-10-2023-bug-fixes"></a>
### Bug Fixes { #january-10-2023-bug-fixes }

* Fixed an issue where, when continuously modifying the monitoring setting popup, the modifications are applied abnormally
* Fixed an issue where the refresh setting does not work in the server dashboard page
* Fixed an issue where an event of backup failure caused by DDL query execution is not logged properly

<a id="december-13-2022"></a>
## December 13, 2022 { #december-13-2022 }

<a id="december-13-2022-feature-updates"></a>
### Feature Updates { #december-13-2022-feature-updates }

* Made modifications so that, when backup fails due to DML overload, the cause is left in the event message

<a id="december-13-2022-bug-fixes"></a>
### Bug Fixes { #december-13-2022-bug-fixes }

* Fixed an issue where, when synchronizing DB schemas, schemas that cannot be deleted are intermittently registered
* Fixed an issue where another host with the same name as the deleted account cannot be added
* Fixed an issue where, when restarting an existing failed-over master, user access control cannot be modified

<a id="november-15-2022"></a>
## November 15, 2022 { #november-15-2022 }

<a id="november-15-2022-bug-fixes"></a>
### Bug Fixes { #november-15-2022-bug-fixes }

* Fixed an issue where, when `sha256_password` is set under the `default_authentication_plugin` parameter, high availability configuration is turned off.

<a id="october-11-2022"></a>
## October 11, 2022 { #october-11-2022 }

<a id="october-11-2022-feature-updates"></a>
### Feature Updates { #october-11-2022-feature-updates }

* Changed the domain change tooltip displayed on the instance details screen

<a id="october-11-2022-bug-fixes"></a>
### Bug Fixes { #october-11-2022-bug-fixes }

* Removed no longer used event codes
* Fixed an issue where a read replica cannot be deleted intermittently under certain conditions

<a id="september-14-2022"></a>
## September 14, 2022 { #september-14-2022 }

<a id="september-14-2022-bug-fixes"></a>
### Bug Fixes { #september-14-2022-bug-fixes }

* Fixed an issue where an error message is left on the browser’s developer console
* Fixed an issue where backup fails when a single instance in a **Not Use** status for **Use table locking** is changed to a high availability instance

<a id="august-9-2022"></a>
## August 9, 2022 { #august-9-2022 }

<a id="added-features"></a>
### Added Features { #added-features }

* Added a feature to export event lists to Excel

<a id="august-9-2022-feature-updates"></a>
### Feature Updates { #august-9-2022-feature-updates }

* Made modifications so that the DB Configuration of an instance where high availability is paused can be changed
* Changed the maximum backup retention period from 30 days to 2 years
* Made improvements so that, when backup fails due to DDL execution, the cause is left in the event message

<a id="august-9-2022-bug-fixes"></a>
### Bug Fixes { #august-9-2022-bug-fixes }

* Fixed an issue where backup fails intermittently due to communication issues with internal agents

<a id="july-12-2022"></a>
## July 12, 2022 { #july-12-2022 }

<a id="july-12-2022-added-features"></a>
### Added Features { #july-12-2022-added-features }

* Added a feature to view charts by grouping them per server on Server Dashboard

<a id="july-12-2022-feature-updates"></a>
### Feature Updates { #july-12-2022-feature-updates }

* Made modifications so that the DB Configuration of a read replica in a **replication stopped** status can be changed

<a id="july-12-2022-bug-fixes"></a>
### Bug Fixes { #july-12-2022-bug-fixes }

* Fixed an issue where DB instances in a **connection failed** status are displayed as **normal** intermittently
* Fixed an issue where, when creating a read replica, backup execution is left in event logs even if the execution is not performed
* Fixed an issue where volume scaling fails intermittently

<a id="june-14-2022"></a>
## June 14, 2022 { #june-14-2022 }

<a id="june-14-2022-feature-updates"></a>
### Feature Updates { #june-14-2022-feature-updates }

* Made improvements so that an event is logged when restart fails due to replication delay
* Changed the access information domain from cloud.toast.com to nhncloudservice.com

<a id="june-14-2022-bug-fixes"></a>
### Bug Fixes { #june-14-2022-bug-fixes }

* Fixed an issue where high availability configuration is not possible when the validate password plugin is used
* Fixed an issue where, even though the type change of the high availability instance has failed, the type of the candidate master is displayed as the type after the change

<a id="may-10-2022"></a>
## May 10, 2022 { #may-10-2022 }

<a id="may-10-2022-feature-updates"></a>
### Feature Updates { #may-10-2022-feature-updates }

* Changed the error log storage location to the data volume
* Made changes so that error logs are rotated up to 10 logs with a size of 100 MB
* Made modifications so that, when a forced restart is executed, the console cannot be operated until it can be used again
* Made modifications so that, after failover starts, the target instance cannot be manipulated in the console
* Improved usability so that you can view the innodb status in the processlist
* Made improvements so that you can move to other pages by numbers in the processlist
* Made improvements so that you can zoom in the chart in the processlist to view only the corresponding section
* Made improvements so that you can search by keywords in the processlist
* Made improvements so that you can download the results searched in the processlist in CSV format

<a id="may-10-2022-bug-fixes"></a>
### Bug Fixes { #may-10-2022-bug-fixes }

* Fixed an issue where, when performing point-in-time restoration with a backup of a read replica, a wrong restoration available time could be selected
* Fixed an issue where the monitoring graph is not visible in Safari
* Fixed an issue where, after changing the parameters of the master instance, changing the parameters of a read replica failed

<a id="april-12-2022"></a>
## April 12, 2022 { #april-12-2022 }

<a id="april-12-2022-feature-updates"></a>
### Feature Updates { #april-12-2022-feature-updates }

* Made improvements so that, when changing a read replica or normal instance to a high availability instance, replication is configured without additional backup if there is an existing backup available

<a id="april-12-2022-bug-fixes"></a>
### Bug Fixes { #april-12-2022-bug-fixes }

* Fixed an issue where, if instance stop and instance volume scaling are performed at the same time, the instance volume scaling operation does not end indefinitely
* Fixed an issue where an error occurs while restarting when the remaining space of the data volume is less than 1%
* Fixed an issue where an event of backup failure is logged intermittently even after successful backup

<a id="march-15-2022"></a>
## March 15, 2022 { #march-15-2022 }

<a id="march-15-2022-added-features"></a>
### Added Features { #march-15-2022-added-features }

* Added a feature to use variables in **DB configuration**

<a id="march-15-2022-bug-fixes"></a>
### Bug Fixes { #march-15-2022-bug-fixes }

* Fixed an issue where monitoring data is not collected under certain conditions
* Fixed an issue where an automatic backup of failed-over instance is not deleted
* Fixed an issue where an automatic backup that has failed to be created is not deleted when it reaches its expiration date
* Fixed an issue where restoration fails when there are too many users registered in MariaDB
* Fixed an issue where a backup settings modification event is logged even when the access rule is modified

<a id="january-11-2022"></a>
## January 11, 2022 { #january-11-2022 }

<a id="january-11-2022-added-features"></a>
### Added Features { #january-11-2022-added-features }

* Added a feature to check the running process list and InnoDB status in MariaDB

<a id="january-11-2022-feature-updates"></a>
### Feature Updates { #january-11-2022-feature-updates }

* Changed the minimum length of the name that can be entered when creating a DB schema in the console to 1 character, which is the same as that of MariaDB

<a id="december-14-2021"></a>
## December 14, 2021 { #december-14-2021 }

<a id="new-releases"></a>
### New Releases { #new-releases }

* Relational Database Service (RDS) provides Relational Database in the cloud environment.
* No complicated configuration is required to enable relational database.
* Supports MariaDB 10.3.30.
