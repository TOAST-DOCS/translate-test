# Backup

**Database > EasyCache > Console User Guide > Backup**

You can prepare in advance to recover the cache in case of failure. You can perform backups through the web console whenever necessary, and you can configure it to perform backups periodically. During backup, the cache performance on which the backup runs may degrade. To avoid affecting service, it is better to perform backups when the service is under low load. If you do not want the backup to degrade performance, you can use a high-availability configuration.

!!! TIP "Note"
    Valkey creates an .rdb file when performing a backup. To restore using a created backup, it is recommended to use a cache with an engine version compatible with the backup.

## Backup Type

Backup offers manual and automatic backups.

### Manual Backup

You can perform a manual backup from the console to permanently save a cache data at a specific point in time. Unlike automatic backups, manual backups are not deleted when the cache is deleted unless you explicitly delete them.
When creating a manual backup, you must specify a name for the backup, with the following limitations
* Backup names are alphabetic, numeric, and - _ between 1 and 100 Only, and the first character has to be an alphabet.

![backup1.PNG](https://static.toastoven.net/prod_easycache/25.09.27/backup1.PNG)
#### Create a Manual Backup

❶ You can create a full backup manually by selecting the cache to back up from the Cache list and clicking **Backup**.
❷ You can create a backup manually by clicking **Create Backup** in the backup list and specifying the cache to back up.

### Automatic Backup
In addition to performing backups manually, automatic backups can occur when required for restore operations or based on the scheduled automatic backup settings.

#### Set Automatic Backup
When creating and modifying caches, you can specify settings that will be applied to backups.

![backup2.PNG](https://static.toastoven.net/prod_easycache/25.09.27/backup2.PNG)

##### Allow Automatic Backup
If automatic backup is not enabled, automatic backups are not performed and the automatic backup settings below cannot be configured.

##### Backup Retention Period (day)
Sets the time period for storing automatic backups on storage. It can be kept for up to 730 days, and if the automatic backup archive period changes, the expired automatic backup files will be deleted immediately.

##### Number of Automatic Backup Retries
You can set the automatic backup to retry if it fails due to cache load at the time of backup or for other various reasons. You can retry a maximum of 10 times. Depending on the automatic backup run time setting, you might not try again even if there are still more retries.

##### Scheduled Automatic Backup Time
You can set the time at which backups are performed automatically. The setting consists of a backup start time and a backup window. You can configure multiple backup times as long as they do not overlap. Backups are performed at a random point within the backup window based on the backup start time. The backup window is not related to the total time required to complete a backup. The time required for a backup is proportional to the memory usage of the cache and varies depending on the service load. If a backup fails and the backup window has not been exceeded, the backup is retried according to the number of backup retries configured.

!!! tip "Note"
    Backups may not be performed in some situations, such as when a previous backup fails to complete.

## Backup Storage and Pricing
All backup files are uploaded to the internal backup storage and stored. For manual backups, they are stored permanently until you delete them separately, and backup storage charges are incurred depending on the backup capacity. For automatic backups, it is stored for the set retention period and charges for the full size of the automatic backup file, which exceeds the storage size of the DB instance. If you do not have direct access to the internal backup storage where the backup file is stored, and when you need backup file, you can export the backup file to the object storage in NHN Cloud.

## Restore
You can restore data to any point in time using a backup. When restoring, you can choose to restore to an existing cache or create a new cache for restoration. You can restore to a cache that uses the same engine version as the source cache from which the backup was performed. To restore using an external RDB file, upload the RDB file to NHN Cloud Object Storage in the same region, and then use the data import feature of the desired cache.

!!! TIP "Note"
    Restoration may fail if the memory or Max Memory (MB) value of the cache to be restored is less than the backup memory capacity of the backup, or if a parameter group different from the source cache parameter group is used.