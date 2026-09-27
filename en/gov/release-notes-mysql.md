## Database > RDS for MySQL > Release Notes

## July 16, 2026

### Feature Updates

* Added MySQL 8.0.46, 8.4.9 version

### Bug Fixes

* Fixed an issue where the security patch was not performed when a single instance subject to security patch was changed to a high availability instance

## May 14, 2026

### Feature Updates

* Added security patch feature
    * Security patches for security vulnerabilities (CVEs) discovered in the OS can be performed as maintenance tasks.
    * For more information, refer to the [Security patch](/Database/RDS%20for%20MySQL/en/db-instance-gov/#security-patch) documentation.
* Added `SELECT` option in addition to the existing `INSERT` option for high availability Ping check method
* Added and updated API v4.0
    * Added the View High Availability Information API.

## March 12, 2026

### Feature Updates

* Added API v4.0
    * For more information, see [API v4.0 guide](/Database/RDS%20for%20MySQL/en/api-guide-v4.0-gov/) document.
* Added snapshot backup feature
    * Perform backups using Cinder storage snapshots with zero impact on DB performance
* Added MySQL 8.0.45, 8.4.8 version

## January 15, 2026

### Feature Updates

* Added maintenance feature
    * Applied various DB instance modifications during your scheduled maintenance duration
* Updated to grant ROLE_ADMIN privileges when the Direct Control for DB Schemas & Users setting is enabled
* Added MySQL 8.0.44, 8.4.7 version

### Bug Fixes

* Fixed an issue where the authentication plugin was not selected by default when adding a user on MySQL 8.4 DB instances.

## November 13, 2025

### Feature Updates

* Added version MySQL 8.4.6
* Improved to record the cause of backup failure due to Lock acquisition failure in the event log.
* Improved to display a warning message related to the password plugin when upgrading to version 8.4.

### Bug Fixes

* Fixed an issue where the failover status persisted when failover failed.
* Fixed an issue where DB instances stopped before the July deployment could not be started.
* Fixed an issue where unusable values could be used in server_audit_events.
* Fixed an issue where the latest parameter group would not be applied after selecting multiple DB instances when using a different parameter group for read replicas.
* Fixed an issue where unchangeable values would be changed when resetting a parameter group.

## September 11, 2025

### Feature Updates

* Added MySQL 8.4 LTS version
* Added MySQL 8.0.41, 8.0.42, 8.0.43 version

### Bug Fixes

* Fixed an issue where the standby master name was displayed with the current name entered when creating a high-availability instance after clicking on an already created high-availability instance.
* Fixed an issue where the name of a read replica added to high-availability could not be modified.
* Fixed an issue where the [Add VIP] drop-down menu was activated when adding a VIP to a DB instance was not possible.
* Fixed an issue where the internal IP would intermittently disappear when DHCP renewal failed.
* Fixed an issue where high-availability would stop functioning if a read replica creation failed on a high-availability instance.
* Fixed an issue where subscription notifications would not work when multiple events subscribed to by the same organization occurred.

## July 17, 2025

### Feature Updates

* Improved to disallow specifying the DB port type in egress rules of DB security groups
* Changed to require entering the name of the candidate master for high-availability DB instances
* Improved to allow DB instance resources to be checked in Resource Watcher
* Fixed billing so that the failover master is charged normally until it is deleted
* Improved to display accurate error messages when failover masters cannot be recovered due to missing binary logs

### Bug Fixes

* Fixed an issue where backup failed when special characters were included in the export path
* Fixed an issue where the user group was not deleted from event subscriptions when the user group was deleted
* Improved to display accurate error messages when deleting duplicate notification groups

## May 15, 2025

### Feature Updates

* Improved to support using VIP (Virtual IP)
    * VIP is now issued for newly created DB instances and is always configured to point to the master DB instance. For existing DB instances, VIPs can be issued manually by clicking the [Add VIP] button in the console
* Improved to allow explicitly disabling High Availability via the console when it is in an abnormal state
* Improved to allow entering decimal values in monitoring settings
* Improved to allow entering Korean characters in user group names
* Improved the change history modal window to check whether to restart when changing parameter groups on DB instances

### Bug Fixes

* Fixed an issue where you could enter invalid values in the event source when creating event subscriptions via the Open API
* Fixed an issue where the status of DB instances was intermittently not updated
* Fixed an issue where an unknown error modal window was sometimes exposed

## April 16, 2025

### Feature Updates

* Added and modified API v3.0
    * Added the API to list Log files
    * Added the Export Log file API


## July 11, 2024

### Feature Updates

* Added the MySQL 8.0.40 version

### Bug Fixes

* Fixed an issue where deleted notification group information appears on the view DB instance details screen

## September 12, 2024

### Feature Updates

* Added storage auto scaling feature
* Improved so that the DB instance is not restarted when the storage size is scaled up
* Separated the storage size scaling feature, which was included in the Modify DB Instance feature, into a dropdown menu
* Changed so that the paused state is maintained when the standby master is rebuilt while high availability is paused
* Removed the backup retry expiration time setting from the automatic backup settings and improved backups to be retried within the backup window time range

## July 11, 2024

### Others

* Ended support for the Korea (Pyeongchon) region

## September 12, 2024

### Feature Updates

* Added incremental backup feature
* Improved so that you can choose whether to delete automatic backups when deleting a DB instance

## July 11, 2024

### Feature Updates

* Added the foreign_key_checks setting procedure
* Added new parameters (MySQL 8.0.28 or later)
    * `innodb_ddl_threads`
    * `innodb_parallel_read_threads`

### Bug Fixes

* Fixed an issue where snapshot restoration with a backup of a deleted DB instance was not possible

## June 12, 2024

### Feature Updates

* Added the feature to upgrade DB instance OS

## May 16, 2024

### Feature Updates

* Added Slow Query analytics
    * Provided the Analytics tab with Slow Query analysis, Process List, and InnoDB Status monitoring features
    * Provided the feature to disable Slow Query Analytics on the Edit DB Instance screen
* Improved to see which parameter items actually change when applying parameter group changes
* Improved to expose warning text and raise an event when high availability status is abnormal
* Improved to select a storage type when creating read replicas
* Added MySQL 8.0.36 version
* Added and modified API v3.0
    * Added the `storage.storageType` field to DB instance replicate API request
    * Added the `notificationGroupIds` field to DB instance detail API response
    * Improved the ability to use project integration appkeys when calling API v3.0

## March 14, 2024

### Feature Updates

* Added the feature to promote candidate masters
* Added the feature to force promote candidate masters
* Added the feature to wait for replication delay on restart with failover
* Added the feature to turn off DB schema & user direct control settings

## February 15, 2024

### Feature Updates

* Added DB schema & user-directed control settings
* Improved to better identify connected notification groups
    * Exposed connected notification group information on the DB instance view details screen
* `Added MySQL 8.0.35 version`

## January 11, 2024

### Feature Updates

* Improved to control the timing of failover whe upgrading the DB engine version for high availability instances
* Improved to allow you to operate the hypervisor migration feature for each DB instance

## December 19, 2023

### Feature Updates

* Improved to make it easier to identify DB instances to which the changed parameter will be applied
    * Added the 'Apply' button in front of the target name to apply the changed parameter on the DB instance list screen.
    * Added the 'Apply' button to the parameter group item on the detail view screen of the DB instance to which the changed parameter will be applied.
    * Add filter option that requires application of changed parameters
* Changed to retrieve servers that have been deleted within the last month when checking the View deleted servers on the server dashboard screen

## November 16, 2023

### Feature Updates

* Added the feature to create read replicas on subnets in other regions with region peering connections
* Added forced promotion of DB instances
* Improved to allow you to select notification type when subscribing to events
* Added and modified API v3.0
    * Added the Export after backing up DB instance API

## September 27, 2022

### Feature Updates

* Improved to create instances by using read replica backups when configuring high availability and adding read replicas
* Added the feature to enable previously created high availability instances of MySQL 5.7.33 or later to use the authentication plugin and TLS option.
* Added the versions of MySQL 8.0.33 and MySQL 8.0.34
* Added and modified API v3.0
    * Added the API to list the last query to be restored
    * Added `dbVersion` and `useDummy` fields to the Modify DB Instance API request
    * Added `needToApplyParameterGroup`, `needMigration`, and `supportDbVersionUpgrade` fields to the List DB Instance API response.

## September 26, 2023

### Feature Updates

* Added a feature to upgrade DB engine version
    * Added support for pre-checks for compatibility when upgrading the DB Engine version from MySQL 5.7 to MySQL 8.0.
    * Added support for upgrading DB Engine version using a dummy DB instance
* Added the Pyeongchon region

## August 29, 2023

### Feature Updates

* Upgraded the version of the xtrabackup utility used for backups
* Improved so that the version of the xtrabackup utility used for backups can be checked in the console
* Added a feature to use the authentication plugin when creating or modifying users in MySQL 5.7.33 or later
* Added a feature to upgrade the DB engine version when modifying a DB instance
* Added a feature to use the authentication plugin and TLS option when creating or modifying users in MySQL 5.7.33 or later

## July 25, 2023

### Feature Updates

* Added DB instance deletion protection feature
* Added rebuild support when a candidate master fails
    * The DB instance on the candidate master does not change, so the fixed IP address does not change
    * All data in the database are deleted, and restored with the data of the master
* Made improvements so that, when adding a user to user groups, all users of organizatons and projects can be added

## May 30, 2023

### Feature Updates

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
    * Added rebuild support when a candidate master fails
    * The DB instance on the candidate master does not change, so the fixed IP address does not change
    * All data in the database are deleted, and restored with the data of the master
* Rebuilding read replica is available
    * The fixed IP address does not change because the DB instance of the read replica remain unchanged
    * All data in the database are deleted, and restored with the data of the master
* Recovery of master with a completed failover
    * High availability recovery of a new master and a master with a completed failover is available
    * Recovery can fail, and an unrecoverable master with a completed failover can be rebuilt
* Rebuilding master with a completed failover
    * The fixed IP does not change because DB instance of the master with a completed failover remain unchanged
    * All data in the database are deleted, and restored with the data of the master
* Added MySQL 8.0.32 version

## February 28, 2023

### Feature Updates

* Made modifications so that the Max Connection value is displayed on the Connection chart in MySQL metrics of the server dashboard

### Bug Fixes

* Fixed an issue where, when an error occurs in the IAM console, the page is not moved to an appropirate error page
* Fixed an issue where, when changing the DB instance type or expanding storage using failover, the Ping interval is set to default

## January 31, 2023

### Feature Updates

* Made modifications not to allow duplicate notification group names

### Bug Fixes

* Fixed an issue where, when continuously modifying the monitoring setting popup, the modifications are applied abnormally
* Fixed an issue where the refresh setting does not work in the server dashboard page
* Fixed an issue where an event of backup failure caused by DDL query execution is not logged properly

## December 27, 2022

### Feature Updates

* Made modifications so that, when backup fails due to DML overload, the cause is left in the event message

### Bug Fixes

* Fixed an issue where, when synchronizing DB schemas, schemas that cannot be deleted are intermittently registered
* Fixed an issue where another host with the same name as the deleted account cannot be added
* Fixed an issue where, when restarting an existing failed-over master, user access control cannot be modified

## November 29, 2022

### Added Features

* Added MySQL 5.7.37, MySQL 8.0.28 versions

### Bug Fixes

* Fixed an issue where an error message is left on the browser’s developer console
* Fixed an issue where backup fails when a single instance in a **Not Use** status for **Use table locking** is changed to a high availability instance
* Removed no longer used event codes
* Fixed an issue where a read replica cannot be deleted intermittently under certain conditions
* Fixed an issue where, when `sha256_password` is set under the `default_authentication_plugin` parameter, high availability configuration is turned off.

## October 4, 2022

### New Releases

* Relational Database Service (RDS) provides Relational Database in the cloud environment.
* No complicated configuration is required to enable relational database.
