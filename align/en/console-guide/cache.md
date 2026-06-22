## Cache

**Database > EasyCache > Console User Guide > Cache**

Cache is a concept for managing nodes with virtual equipment and engines (Valkey and old Redis) installed, and is the largest resource unit within the EasyCache service.
A single cache consists of multiple nodes, and the nodes belonging to the cache share information such as the cache's engine version, port, password, parameter group, and security group.

* The available service port range is between 10,000 and 12,000.
* Currently we provide the Valkey engine. For Redis, we only support caches that have already been created.
* A cache automatically issues and provides a 32-byte ID.
* Users can enter or modify the cache name, and it has the limitation as below:
* Only letters, numbers, and some symbols (-, _) can be used within 20 characters.

The types of caches provided are as follows:

| Type | Description |
| --- | --- |
| Single node cache | A cache of one master node |
| High-availability cache | A cache of one master node and one or more read replica nodes |

### Node

A node is a basic resource unit that actually refers to the engine (Valkey and old Redis) and the virtual machine on which the engine is installed.
One node has one Valkey installed and by default follows the information shared by the cache.
A node automatically issues and provides a 32-byte ID.
The node name cannot be changed as it is automatically created by adding “-number/letter” to the name of the cache.

The types of nodes provided are as follows:

| Type | Description |
| --- | --- |
| Master node | A master node providing both read and write features |
| Read replica node (if in the same region as the master node) | A read-only replica node that serves read only. In the event of a failover, one of the read replica nodes changes to the master node. |
| Read replica node (if in a different region than the master node) | A read-only replica node that serves read only, but does not perform failover in the event of a failure. |
| High-availability Control Node | A separate node for controlling high availability, including the master node and read replica nodes, which are automatically created when you add one or more read replica nodes. |

### Create Cache

You can create a cache by using the settings below:

#### Availability Zone

NHN Cloud has divided its entire system into multiple availability zones to prepare for failures caused by physical hardware issues. Each availability zone has separate storage systems, network switches, racks, and power supplies. Failures within one availability zone do not affect other availability zones, increasing the availability of the entire service. EasyCache allows you to select the availability zone of the master node, and automatically assigns the availability zones of the read replica nodes based on the selected availability zone, thereby increasing availability. There is no network usage cost incurred during network communication between nodes created across multiple availability zones.

!!! danger "warning"
    The availability zone of master nodes already created can be changed.

#### Engine Version

The versions listed below are available:

| Version | Note |
| --- | --- |
| **Valkey 8** |  |
| 8.1.4 |  |
| 8.0.2 |  |
| **Redis 7** | New cache support ended |
| 7.2.6 |  |
| 7.2.4 |  |
| 7.0.7 |  |
| **Redis 6** | New cache support ended |
| 6.2.3 |  |
| **Redis 5** | New cache support ended |
| 5.0.8 |  |
| **Redis 3** | New cache support ended |
| 3.2.12 |  |

!!! tip "notice"
    Newly created caches no longer provide Redis, and we only serve caches that are already using Redis.

#### Instance Flavor

Instances have different numbers of CPU cores and memory capacities depending on their flavors.
When creating an instance, you must select the appropriate instance flavor based on your database workload.

| Type | Description |
| --- | --- |
| m2 | Flavor with balanced CPU and memory settings. |
| c2 | Flavor with high CPU performance. |
| r2 | Available when memory usage is high compared to other resources. |
| x1 | This flavor supports high-spec CPUs and memory. Used for services or applications that require high performance. |

!!! danger "warning"
    The instance flavor of caches and nodes already created can be changed. It is not currently available as an official feature, please contact the customer center if necessary.

#### Max Memory (MB)

You can specify Max Memory used by Valkey to avoid running out of memory when running a sync or backup.
When needed, cache modifications allow you to flexibly secure the capacity of memory.

#### Use Password

If you choose to use a password, automatically create a string and specify a password.
After the cache is completed, you can check it in the cache basic information or node basic information.

#### Network

You need to select the VPC subnet to connect to the node you belong to in the cache. The instance of the Compute service connected to the same subnet can communicate without a separate floating IP and no cost for network traffic. The node basically blocks all network access, so if you want to connect, you need to apply the DB security group.

!!! danger "warning"
    The subnets of caches and nodes already created can be changed.

#### Floating IP

To access the node from the outside, the floating IP must be connected to the master node. You can create a floating IP only if you connect the subnet connected with the Internet Gateway. Floating IP is charged at the same time as it is used, and separately, if traffic in the Internet direction through floating IP is generated, it will be charged separately.
If you are using the floating IP, the floating IP domain for the floating IP is created together and can be found in the cache default information and the basic information of the master node.

#### Parameter Group

The parameter group is a set of parameters on the VALKEY of the nodes in the cache. When creating a cache, you must choose one parameter group. Parameter groups can be changed freely after creation. For more information about the parameter group, please refer to the **@parameter group ** item.

#### DB Security Group

DB security groups are used to restrict access in case of external intrusion. You can allow access to a specific port range or specified port for transmission and receiving traffic.
You can apply multiple DB security groups at once, and please refer to the **@DB security group ** section for a detailed description of the DB security group.

#### TLS Authentication

NHN Cloud's **@Certificate Manager ** You can select one of the certificates stored in the service and communicate with the TLS certificate.

** TLS service port **: a port for connection using TLS certificate. It is necessary to set the number to more than 10,000 and more than 12,000, unlike the service port.
** ** TLS service port only **: TLS service can be used to connect. If you activate this feature, you cannot access it using a common service port.
*** Select certificate **: you can choose one of the TLS certificates stored in the Certificate Manager service. You need to enter the Appkey of the Certificate Manager service.
* VALKEY requires both public, secret key, and CA public keys. Therefore, the certificate to be used should include all the keys, and for how to generate the key, refer to the [Certificate Manager> Troubleshooting Guide] (https://docs.nhncloud.com/en/manage/certificate%20Manager/en/troubleshooting-guide/).

!!! danger "warning"
    If you decide whether to use the TLS certificate at the time of the creation of a replica group, you will not be able to change it later.

#### Backup

You can set the value of the cache periodically, or you can create a backup at the time you want through the console. The backup is carried out in the master, and the performance may occur during the performance. It is recommended to back up at a time when the service load is low in order not to affect the service. The backup file is stored in the internal backup storage and is charged according to the backup capacity. In order to prepare for unexpected failure, it is recommended to set up a backup periodically. For more information about the backup, please refer to the **@backup ** item.

#### Default Notifications

You can set up a default notification when creating a cache. If you set the default notification, a new notification group is created under the name {Cash Name} -DEFAULT, and the following notification items are automatically set. Notification groups created with Default Notifications can be freely modified or deleted. For more information about the notification group, please refer to the **@notification group ** item.

The monitoring settings for the default notification group are as follows:

| Item | Comparison method | Threshold | Duration |
| --- | ----- | --- | ----- |
| CPU usage | > | 80% | 10 min |
| Memory usage | > | 80% | 10 min |
| No. of connected clients | > | 9,000 | 1 min |
| No. of blocked clients | > | 1 | 10 min |
| No. of deleted keys | > | 1 | 10 min |

#### Deletion Protection

If you activate deletion protection, you can protect the cache from accidental deletion.

### Cache and node list

You can check the cache created from the console. You can view a list of nodes belonging to a cache by cache unit.
![cache1.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache1.PNG)

➊: You can collapse or expand the list of nodes belonging to the cache by clicking the button.
➋: It shows the most recently collected monitoring metrics. When the node list is collapsed, the monitoring metrics of the master node are displayed in the cache.
➌: You can view the current status.
➍: A spinner appears when there is a task in progress.
➎: You can change the search condition.

The state of the cache and nodes consists of the following values, which change depending on the user's actions and current state.

| Status | Description |
| --- | --- |
| REGISTERD | Before create |
| STABLE | Available |
| FAILED\_TO\_CREATE | Failed to create |
| FAILED\_TO\_CONNECT | Failed to connect |
| REPLICATION\_STOP | Replication stopped |
| WARNING | Abnormal |
| DISABLE | Unavailable |
| PLANNED\_MIGRATION\_FAILED | Failed to migrate |
| SHUTDOWN | Stopped |

### Cache and node details

You can view the details by selecting the cache and node.

![cache2.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache2.PNG)

➊: When you click on a domain in the connection information, a pop-up window will appear where you can view detailed information about the domain, including IP information.
➋: When you click on a DB Security Group, a pop-up window will appear where you can check the DB Security Rules.
➌: Clicking on a parameter group will take you to a screen where you can check the parameters.
➍: You can adjust the height of the details panel by dragging and dropping with the mouse.
➎: You can adjust the details panel to a predefined height.

#### Access Information

When creating a cache, an access domain is issued. The access domain points to an IP address belonging to the user's VPC subnet. For a high-availability cache, if a failover occurs and one of the read replicas changes to the new master, the access domain does not change. Therefore, unless there is a special reason, the application's access information must use the connection domain.

If you use a floating IP, an additional floating IP domain will be issued. The floating IP domain indicates the address of the floating IP. Even if a failover occurs and the master is replaced with a new one, you can still access the new master using the same floating IP and domain. Because floating IP domains are accessible from outside, you must protect the cache by setting up appropriate rules in the DB security group.

If you have read replica nodes, you can set up a read-only domain by modifying the cache. When using a read-only domain, point the read-only domain to an IP address belonging to the VPC subnet of the read replica nodes that belong to the same cache and the same region. If a failover occurs and one of the read replicas becomes the new master, the IP information pointed to by the read-only domain is also updated.

![cache3.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache3.PNG)

#### Event (cache)

Events triggered by the selected cache are displayed in chronological order, and you can view them by specifying the period you want.

![cache4.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache4.PNG)

#### Backup

A list of backups created by the selected cache will be displayed, and you can create a backup by clicking **Create Backup**.

![cache5.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache5.PNG)

#### Domain

The cache shows all domain information, but the node basic information shows different domain information depending on the node type, so please refer to the explanation below.

| Node type | Domain information shown |
| ----- | ----------- |
| Master node | access domain, floating IP domain |
| Read replica node | Read-only domain |
| High-availability Control Node | None |

#### OS Version

The selected node shows the OS version in working.

![cache6.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache6.PNG)

#### Monitoring

Shows various monitoring indicators of the selected node.

![cache7.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache7.PNG)

#### Event (node)

Events triggered by the selected node are displayed in chronological order, and you can view them by specifying the period you want.

![cache8.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache8.PNG)

#### Log

The **Logs** tab of a node allows you to view Valkey's logs for a specified period of time. Click the **View in New Tab** to view the log in a new tab with a wider screen.

![cache9.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache9.PNG)

#### User

The Users tab of a node allows you to create, view, edit, and delete users in Valkey.

➊: clicking **Create** will bring up a pop-up window where you can enter the user's information you want.
➋: you can choose whether to activate or not for the user.
➌: you can grant permissions to users via ACL expressions supported by Valkey.
➍: when you click **Save** in the settings file, the user information currently stored in Valkey memory will be recorded to the settings file, so that the user settings will be maintained even after restarting.

!!! danger "warning"
    * User settings are information set per node and are not propagated to other nodes belonging to the same cache. Therefore, if you have different user settings for each node, failover may not proceed properly, so be careful.
    * Please note that user information created on the node may be lost due to reasons such as cache restart before being saved to the configuration file.

### Modify Cache

![cache10.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache10.PNG)
You can easily change various items of the selected cache by checking the checkbox of the cache you want in the console screen and clicking **Edit**. Apply the requested changes sequentially to the cache. If a restart is required during the application process, restart the cache after applying all changes. The following items cannot be changed and require a restart:

| Item | Changeable | Restart required | Description |
| --- | -------- | --------- | --- |
| Availability zone | No |  |  |
| Engine version | Yes | Yes |  |
| Max Memory | Yes | No |  |
| Instance flavor | No |  |  |
| Cache name | Yes | No |  |
| Cache type | Yes | No | Provided separately as a node add/delete function, not a cache modification function |
| Description | Yes | No |  |
| Use password | No |  |  |
| Service port | No |  |  |
| Master down after | Yes | No |  |
| Network (VPC subnet) | No |  |  |
| Floating IP setting | Yes | No |  |
| Read-only domain | Yes | No |  |
| Parameter group | Yes | Depends on the case | Determines whether to restart based on changed parameters |
| DB security group | Yes | No |  |
| Use TLS certificate | No |  |  |
| TLS service port | No |  |  |
| Use TLS service port only | No |  |  |
| Select TLS certificate | Yes | No |  |
| Backup setting | Yes | No |  |
| Basic notification | Yes | No |  |
| Deletion protection | Yes | No |  |

#### Modify Engine Version

You can upgrade the cache by upgrading to a higher engine version than the current one.
Engine version upgrades require careful consideration, as they can cause service interruptions or outages.
The engine version upgrade will begin with the read replica nodes and high-availability control nodes in the cache. Once all nodes have been upgraded, the master will be replaced. The engine version of the old master node, now a read replica node, will be upgraded, ultimately replacing the master.
If the cache only contains one master node, the engine version upgrade will occur immediately, resulting in service interruption.

!!! danger "Warning"
    * Please note that if there are read replica nodes in the same region as the master node, the master will eventually change.

!!! tip "Note"
    * Redis versions prior to 7.0.7 can be upgraded to 7.0.7 before being upgraded to the next version.
    * Redis versions 7.0.7 or later provide upgrades to the latest version.

### Modify Node

![cache11.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache11.PNG)
You can change some items of the selected node by selecting the checkbox of the desired node in the console screen and clicking **Modify**.

| Item | Changeable | Restart required | Description |
| --- | -------- | --------- | --- |
| Node name | No | | |
| Node type | No | | | |
| Availability zone | No | | | |
| Engine version | No | | Changes can be made on the cache modification screen, not the node modification screen, and are sequentially reflected on nodes belonging to the cache. |
| Instance flavor | No | | Currently not supported. (to be supported) |
| Operating system version | Yes | Yes | Only the latest version can be updated. |

#### Modify OS Version

Node OS version upgrades are supported. OS upgrades can address security vulnerabilities or address OS end-of-life (EOL) events.
Operating an OS version requires caution, as it may result in service interruption in some cases.
For the master node, if there are read replicas, the OS version upgrade cannot be performed. The OS version upgrade must be performed first on the read replica nodes and the high-availability control node, then the existing master node must be converted to a read replica using the Change Master feature before proceeding with the OS version upgrade.
If there are no other nodes besides the master node, the OS version upgrade can be performed on the master node, but service interruption will inevitably occur.

### Import Data

![cache12.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache12.PNG)

You can retrieve data from **@Object Storage** in the same region and apply it to the cache.
Enter your tenant ID, API password, and the data file path in the format {containerName}/{path or fileName}, then click **Import Data** to start the task.

!!! danger "Warning"
    * Nodes will be unavailable during data import, and existing data will be deleted, so we recommend creating a manual backup before importing.
    * Only RDB files compatible with the engine version can be imported.

### Export Data

![cache13.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache13.PNG)
You can export data from the cache you want to **@Object Storage** in the same region. Enter your tenant ID and API password, then enter the container name and data name Prefix\* and click **Export Data** to begin the process.

!!! tip "Note"
    An RDB file is created in Object Storage at the path entered by the user, with the data name prefix value entered and a random string concatenated.

### Add Node

![cache14.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache14.PNG)
You can add a read replica node by selecting the checkbox for the desired cache in the console screen and clicking **Add Read Replica Node**.
For single-node caches, adding a read replica node in the same region as the master node will also create a high-availability control node.
You can create up to two read replica nodes in the same region as the master node, or one in a different region.
Once the node is added, the cache type changes to a high-availability cache. If the master node fails, a failover will occur and the master node will be replaced if a read replica node exists in the same region.

!!! danger "Warning"
    Read replicas created in other regions will not fail over if the master node fails.

### Remove Replication Connection and Forced Replication Connection

![cache15.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache15.PNG)
In the console, you can select the checkbox for a read replica node located in a different region than the master node and use the **Remove Replication Connection** or **Forced Replication Connection** functions.
Using the Remove Replication Connection function removes the replication connection from the master in the source region and promotes it to become the new master.

!!! tip "Note"
    * Performing a forced replication connection removal may result in inconsistencies with the source region's cache and master node configuration information, as this involves forcing a replication connection operation. Therefore, it is recommended only for special cases, such as a failure in the source region.
* Read replicas in the same region as the master do not support the replication connection removal feature. (to be supported)

### Delete Node

![cache16.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache16.PNG)
You can delete a read replica node by selecting the checkbox for the node belonging to the high-availability cache you want on the console screen and clicking **Delete Node**.
The master node and high-availability control node cannot be deleted by design.
After the selected read replica node is deleted, if there are no more read replica nodes remaining in the same region as the master node, the high-availability control node will also be deleted.

### Change Master

![cache17.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache17.PNG)
You can change the master by selecting the checkbox for the high-availability cache you want on the console screen and using the Change Master function.
When the existing master node is converted to a read replica, one of the read replica nodes located in the same region as the master node becomes the new master.

### Stop Cache

![cache18.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache18.PNG)
You can stop any running cache you want. If it's a high-availability cache, all nodes in the cache will be stopped.

### Start Cache

![cache19.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache19.PNG)
You can restart any stopped cache you want. If it's a high-availability cache, restart all nodes belonging to the cache.

### Restart Cache

![cache20.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache20.PNG)
You can restart any cache you want from the console screen. If it's a high-availability cache, all nodes in the cache will restart.

### Apply Parameter Group Changes

![cache21.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache21.PNG)
If you modify a parameter group that is already in use by a cache in the **Parameter Groups** tab, the parameter group will not be immediately applied to the caches that are using it and the nodes that belong to the cache. Instead, a **Parameter** button will appear in the cache list on the console screen, and if you select the checkbox, the **Parameter Group Changes** item will be enabled.

!!! danger "Warning"
    When applying parameter group changes, be careful as a restart may occur depending on the changed parameter items in that parameter group.

### Reset High Availability

![cache22.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache22.PNG)
If the cache's high availability status is abnormal, the cache status will be displayed as **Abnormal**, and a **Reset High Availability** button will be displayed in the cache list for your use. Restting high availability reset will rewrite high availability-related settings or recreate high availability nodes.

### Migration

If a virtual machine needs to be migrated from one of the nodes in the cache, a Migrate button will appear on that node.
The migration function requires caution, as it may cause service interruption in some cases.

!!! tip "Note"
    For master nodes, if there are read replicas, the button will be visible but disabled and cannot be migrated. Migration must be performed first on the read replica nodes and the high-availability control node, then the existing master node must be converted to a read replica using the Change Master feature before migration can proceed.

### Delete Cache

You can delete caches that are no longer in use at any time. Deleting a cache will also delete all nodes belonging to the cache. Deleted caches and nodes cannot be recovered, so we recommend enabling deletion protection for important caches.

### Backup

You can prepare in advance to recover cache data in case of a failure. You can perform backups from the console whenever needed, or schedule backups to be performed periodically. For more information, see the **@Backup** section.

### Restoration

You can restore data using a backup. When restoring, you can choose to restore to an existing cache or a new cache. For details, see **@Restore** in **@Backup**.

### High-availability Cache

EasyCache's cache automatically creates a high-availability control node when you add a read replica node in the same region as the master node, and automatically performs failover in the event of a failure.

!!! danger "Warning"
    Because the nodes that make up a high-availability cache do not share user settings, changes to user settings on one node will not propagate to other nodes in the cache. Therefore, if user settings differ across nodes, failover may not proceed properly, so caution is advised.

#### Failure Detection

![cache24.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache24.PNG)
All nodes in the same region as the master node detect the master node and, based on the master down after entered when adding a read replica node, determine whether communication has failed and initiate failover. Therefore, it is important to set a master down after appropriate for cache usage.

#### Auto Failover

If a failure is detected through failure detection, one of the read replica nodes in the same region as the master is elected as the new master through agreement between nodes, and the existing master is changed to a read replica.
The IP information of connection domain and read-only domain for connection are updated based on the new failed-over node, and the floating IP domain does not change, but the floating IP pointed to by the floating IP domain is automatically changed to point to the new master.

!!! tip "Note"
    * Failover is only supported for nodes within the same region as the master node. Automatic failover is not supported if read replicas are only added in different regions.
    * We recommend clicking the Update Read-Only Domain button only after the failure is fully resolved to ensure the IP information is updated based on the final status of the read-only nodes.
    * Unlike an actual failover, the read-only domain IP information is automatically updated when IP changes occur through manual master changes or other administrative functions.

#### Remove Forced Replication Connection

![cache25.PNG](https://static.toastoven.net/prod_easycache/25.09.27/cache25.PNG)
Read replica nodes added to other regions are not eligible for automatic failover in the event of a master failure. However, if you need to use a read replica node in another region immediately in the event of a failure, you can use the **Remove Forced Replication Connection** feature to promote a read replica node in another region to become the master node.
**Remove Forced Replication Connection** will create a new, separate cache in another region, separate from the existing nodes, promote the existing read replica node to the master node, and expose a new connection domain.

!!! tip "Note"
    * Performing a forced replication connection removal can cause inconsistencies with the cache and master node configuration in the source region, as it forces a forced replication connection operation. Therefore, it should only be used in special cases, such as a failure in the source region. If your goal is simply to separate a read replica in another region to a new cache, we recommend using the regular replication connection removal feature.
    * Read replicas in the same region as the master do not support the replication connection removal feature (to be supported).