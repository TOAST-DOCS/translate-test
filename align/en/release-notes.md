## EasyCache Release Notes
**Database > EasyCache > Release Notes**

### May 27, 2026

#### Feature Updates
- Added support for Valkey 9.0.3.

#### Bug Fixes
- Removed the exposure of the unnecessary parameter `dynamic-hz` for Valkey 8.1.4 and later.

### March 24, 2026

#### Feature Updates
- Added support for Valkey 8.1.6.
- Added a feature to check and synchronize differences in redis.conf settings between parameter groups and nodes in the console.

### January 27, 2026

#### Feature Updates
- Modified the console to display a button for updating the IP of the read-only domain after a failover is completed.
- Made it possible to search the cache list by ID.
- Updated some event lists included in the user guide to reflect the current status.
- Updated the names of some parameters for Valkey 8.x and later versions to the latest version.

#### Bug Fixes
- Fixed an issue where an error occurred when the RDB filename used for data import contained a specific string.
- Fixed the multilingual display of header items in the CSV file downloadable from the event screen.

### November 15, 2025

#### Feature Updates

- Added support for Valkey 8.1.4
- Improved texts in the guide for some parameters
- Made improvements so that the list from Event Subscription > Event Code is sorted by "Start", "Completed", and "Failed".

#### Bug Fixes

- Fixed a bug that caused engine version upgrades to fail under certain conditions.
- Fixed a bug where the Modify button was enabled while working on cache and parameter groups.
- Fixed a bug where the Reset High Availability button was exposed during node deletion.
- Fixed a bug where an error message was displayed in the Monitoring/User tabs of other region nodes.
- Fixed a bug where other region nodes were displayed in the Server Dashboard tab.

### September 23, 2025

#### Feature Updates
- Fixed an issue where a "Could not find the tenant resource" error message was displayed for a short time immediately after service activation
- Fixed an issue where emails were not sent when restarting EasyCache for hypervisor maintenance
- Fixed an issue where restarting EasyCache for hypervisor maintenance failed under certain conditions

### April 29, 2025

#### Added Features
- Added support for Valkey 8.0.2

#### Features Updates
- Terminated the feature to create new replication groups in Redis versions

#### Bug Fixes
- Fixed non-replication group nodes being exposed in the target replication group on the Notification tab
- Fixed intermittent abnormal error message exposure immediately after service activation
- Fixed an issue that caused replication group creation to fail in regions other than KR1 for a period of time after service activation

### February 25, 2025

#### Added Features
- Added the Redis ACL feature

#### Bug Fixes
- Fixed incorrect button names on some screens

### January 21, 2025

#### Added Features
- Added support for Redis 7.2.6

#### Bug Fixes
- Fixed an issue where an incorrect OS version upgrade success message are displayed
- Fixed an issue where the Modify button is not enabled when only changing the user group name

### November 26, 2024

#### Feature Updates
- Improved display string and sorting for user group creation and modification dates

#### Bug Fixes
- Fixed an issue where metric conditions are not modified

### October 15, 2024

#### Feature Updates
- Added a notification to remind users to select either email or SMS when creating notification groups

#### Bug Fixes
- Fixed a status phrase that appears when performing engine version upgrades
- Fixed an announcement phrase that appears immediately after requesting engine version upgrades
- Fixed an issue where some event phrases are not displayed in English and Japanese in the console

### August 27, 2024

#### Added Features

* Added the server dashboard page
* Added the OS version upgrade feature
* Added the feature to record event logs when notifications are sent

#### Feature Updates

* Changed the default OS to Ubuntu

### May 14, 2024

#### Bug Fixes

* Fixed an issue where, when selecting a certificate, the certificate list cannot be extended above a certain height
  
### April 9, 2024

#### Bug Fixes

* Fixed an issue where abnormal replication group loading status lasts infinitely

### March 12, 2024

#### Feature Updates

* Added support for Redis 7.2.4

### February 22, 2024

#### Feature Updates

* Replaced internal library

#### Bug Fixes

* Fixed an error where some metric conditions are not displayed correctly when viewing alarm details.
* Fixed an issue where duplicate event conditions are exposed on the alarm rule creation screen
- Fixed aexcessive alarm occurrence
- Fixed master down judgment time error that occurred under certain conditions

### December 19, 2023

#### Feature Updates

- Ended service in Japan (Tokyo) region

### November 14, 2023

#### Feature Udpates

- Added a note that the service is scheduled for End of Life in Japan (Tokyo) region when creating replication groups

### October 17, 2023

#### Bug Fixes

- Fixed an issue where the time for deleting auto backups could differ from the expected time by up to 3 hours.

### September 12, 2023

#### Feature Updates

- Improved internal performance

#### Bug Fixes

- Fixed an issue where the profile field appears as empty after Redis version upgrade

### August 17, 2023

#### Feature Updates

- Modified the access port information for replication groups using TLS certificate in accordance with TLS access port format.


#### Bug Fixes

- Fixed an issue where HA reset fails under certain conditions

### June 13, 2023

#### Feature Updates

- Terminated the feature to create new replication groups in Redis 5.0.8
- Added a feature to communicate using TLS certificates

### April 11, 2023

#### Bug Fixes
- Fixed an issue where alarms in some value ranges do not occur under system memory metrics conditions

### March 14, 2023

#### Feature Updates
- Improved internal performance

### January 10, 2023

#### Feature Updates
- Added support for Redis 7.0.7
- Improved to display the protected-mode item in Profile

#### Bug Fixes
- Fixed an issue where version upgrade retry fails under certain conditions

### November 15, 2022

#### Bug Fixes
- Fixed an issue where an error message occurs when registering connection information in bulk
- Fixed an issue where HA restoration does not work properly when adding a node fails

### October 11, 2022

- Changed the domain for replication groups to connect from easycache.cloud.toast.com to easycache.nhncloudservice.com

### February 22, 2022

#### Feature Updates
- Changed the default value of maxmemory-policy from volatile-lru to allkeys-lru

### November 23, 2021

#### Added Features
- Added a feature to upgrade a replication group from Redis version 5 to Redis version 6

### October 26, 2021

#### Bug Fixes
- Fixed an issue where configuration profiles could be modified while performing import, export, or manual backup of data.

### September 28, 2021

#### Feature Updates
- Improved alarm rule creation screen.
- Improved service usage start processing.

#### Bug Fixes
- Fixed an issue where node creation fails when adding a node to a replication group with a large amount of data.
- Fixed an issue where, when restoring a backup file with version 5 to a new replication group, the version is displayed in the first replication group window, but the version is not displayed when the window is closed and reopened.
- Fixed an issue where the replication group status is not displayed as normal even when a replication was deleted in the replication unavailable status.
- Fixed an issue where selectable replication groups are not displayed when restoring a backup in which a replication group has been deleted in the replication group restore.

### August 24, 2021

#### Feature Updates

- Added support for Redis 6
- Added a feature to restore a backup to the existing replication group
- Added a feature to set the alarm trigger conditions using the alarm template when setting the alarm 
- Changed the UI so that default network of the **Access Control Information*- is not deletable

### July 27, 2021

#### Feature Updates

- Add a feature to(Export) EasyCache data to Object Storage.
- Modify **Promote Master*- to **Change Master*- and go to drop down menu. 

#### Bug Fixes

- Corrected the condition that CIDRs that failed to register are displayed as duplicates in the access control information

### June 29, 2021

#### Feature Updates

- Added a feature to choose between bytes, MB, or GB if the graph on the detailed screen of EasyCache monitoring is in a unit of bytes
- Added a feature to choose the node to be displayed on the detailed screen of EasyCache monitoring
- Added a feature to (import) data of Redis used externally to EasyCache
- Added the Multi Replica feature to distribute read function
- Added the current time to the screen to the right of the event search period calendar

#### Bug Fixes

- Fixed to expose the name in the replication group profile modification failure popup
- Fixed a bug where after deleting the replication group node and clicking the Delete button of another replication group node, the Delete button becomes inactive if no node is selected

### May 25, 2021

#### Feature Updates

- In monitoring, there was improvement by adjusting the size of each chart according to the size of the full screen.
- The monitoring data storage period was changed from 1 month to 40 days

#### Bug Fixes

- When setting the search period in the View Log, an error message that used to appear was fixed.

### April 27, 2021

#### Feature Updates

- Changed the system so that the nodes can only be deleted or restated when their status is 'unavailable'
- Modified the system so that event categories and search time will be automatically searched when the respective button is selected
- Modified the system so that the keyword will not remain when a notification event, replication group, or receiving group is searched for and its sub item list is selected in notification rules

### March 23, 2021

#### Feature Updates

- Added read-only domain event registration
- Fixed the system to show an error message when the replication group is using a subnet without internet gateway when setting up a public domain

#### Bug Fixes

- Fixed an issue where an error would occur when the user enters a blank space in the search field during log search

### February 23, 2021

#### Feature Updates

- Added read-only domain tooltip

#### Bug Fixes

- Fixed an issue where no replicated group is created if the maximum value is entered for a profile.

### January 26, 2021

#### Feature Updates

- Changed Maxmemory default from 70% to 50% of available memory
- Added **activedefrag**-related options in profile
- **View Log**  dialog box UI improved

#### Bug Fixes

- Fixed a bug where the date changes to January 2 when the time is changed in monitoring

### December 29, 2020

#### Added Features

- Added read-only domain feature

#### Feature Updates

- Improved the feature related to login control information
- Improved to show guidance when mouse is hovered over the Change instance type button
- Changed the dialog button name to OK.

#### Bug Fixes

- Fixed an issue where the task of profile modification fails and made unavailable when changing the profile of a replication group if the profile before the change is modified
- Fixed an issue of Korean filter option names were displayed when the website language is set to 'Japanese'

### Nov 24, 2020

#### Feature Updates

- View All Logs added

### October 27, 2020

#### Bug Fixes
- Modified node name to reflect changes in group name when changing name of replication group
- Modified error message in cases where a quarter of CPU and RAM is exceeded

### September 22, 2020

#### Feature Updates

- Korea (Pyeongchon) region opened
- Added log check feature
- Sort and display VPC subnet list by name
- Service use permissions response

#### Bug Fixes

- Modified unit of monitoring graph
    - Input byte: byte -> bytes/1min
    - Output byte: byte -> bytes/1min
    - Processed commands per second: counts/seconds -> count/1sec
- During profile modification, the bug where the status of a replication group using the profile currently being modified is displayed as normal rather than displaying modification in progress

### August 25, 2020

#### Feature Updates

- Changed the password setting for Redis access as optional

#### Bug Fixes

- Fixed an issue where node promotion completion time and condition display does not accord when promoting replica nodes

### July 28, 2020

#### Added Features

- Instance type change feature added

#### Feature Updates

- Deleted Compute Optimized type from supported instance type

#### Bug Fixes

- Fixed an issue where clients connected from monitoring graph is displayed as an accumulation
- Fixed a bug where, when restoring from Redis 3.2.12 replication group which used custom profile, the profile would be restored to Redis 3.2 default profile

### June 23, 2020

#### Feature Updates

- Registered events on CloudTrail service

#### Bug Fixes

- Fixed an issue in which the operation duration (uptime_in_seconds) of INFO’s Redis server is displayed in values with additional 9 hours
- Fixed an issue where, when users click the View button to check their passwords, nodes fail to acquire passwords during node failures
- Fixed an issue where HA reset fails even after HA reset button is displayed and reset is executed
- Fixed an issue where dates could not be selected freely from search period on the monitoring screen

### May 26, 2020

#### Feature Updates

- Redis 5.0 supported
- Profile copying feature provided
- Monitoring updated
    - Moved query tab from replication group details screen to a separate tab on top of the initial screen
    - Added Current Time button
    - Added Auto Renew checkbox
    - Added replication group selection drop-down menu
    * Updated single graph to be displayed additionally as a pop-up to allow users to select statistical entries and aggregation duration
* Changed features to allow user to modify values through detailed settings when creating or modifying profiles

#### Bug Fixes

* Fixed an issue where the modification button is disabled when trying to modify replication groups with no nodes added after modifying replication groups with added nodes
* Fixed a bug where 「Number of Connected Clients」 and 「Number of Blocked Clients」 on the monitoring option is displayed as an accumulation value
* Fixed an issue where the profile list is not fully displayed after modification
* Fixed an issue where the screen does not reload after modifying profiles currently being used by replication groups

### April 28, 2020

#### Feature Updates

- Provided feature to allow users to enable health check response time on watch setting
- Provided master manual promotion feature
- Changed a monitoring field to display successful/failed query numbers as per time instead of an accumulation value
- Changed alarm rules to allow changing memory usage in %

#### Bug Fixes

- Fixed an issue where monitoring graphs are partially displayed every 10 minutes
- Fixed an issue where replication group and node status is not properly reflected after failed nodes are restored within a few seconds after a failover
- Made changes to allow password modification of warning replication groups
- Modified a portion of menus and labels

### March 24, 2020

#### Feature Updates

- Changed default config value of EasyCache(tcp-keepalive [0→300])

### February 25, 2020

#### Feature Updates

- Modified feature to allow users to simultaneously add multiple connection information
- Updated SMS content
- Modified messages when entering duplicated CIDR

#### Bug Fixes
- Fixed an issue where infinite loops of data synchronization occurs when replica node is added in presence of bulk data
- Fixed an issue where node is displayed as creating on node alarm even after node creation failure within a replication group

### February 11, 2020

#### Feature Updates

- Upgraded version of NHN Cloud user authentication module

#### Bug Fixes
- Fixed an issue where selection fails in cases of selecting VPC subnets of users that did not set up internet gateways when creating replication groups

### January 21, 2020

#### Feature Updates

- Japanese supported for console screen and event messages
- Event registration added when domain change fails after failover

### December 24, 2019

#### New service release

- NHN Cloud EasyCache is a service that provides Redis (REmote DIctionary Server) in a cloud environment.
