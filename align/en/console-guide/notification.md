# Notification

**Database > EasyCache > Console User Guide > Notification**

You can receive notifications about performance metrics through notification groups. Select the **Notification Type** and **Enabled** status, then specify the node to monitor and the user group to receive notifications. Set the thresholds and conditions for performance metrics to receive notifications through the **Monitoring Settings**. When the set metrics meet the conditions in the Monitoring Settings, the associated user group will be notified. Notifications are sent via SMS or email, depending on the notification type set for the notification group.

### Create a Notification Group

![notification1.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification1.PNG)

❶: Click **Create Notification Group** to open a pop-up where you can create a notification group.
❷: Select the method for receiving notifications.
❸: Notification groups with **Enabled** set to **No** do not send notifications.
❹: Select the node to monitor.
❺: Select the user group to receive notifications.

## Monitoring Settings

The monitoring settings consist of monitoring items, comparison method, threshold, and duration. It compares the performance metric value of a monitoring item against the threshold to determine whether the condition is met. If the condition is continuously met for at least the specified duration, a notification is sent. For example, if the CPU utilization threshold is over 90% and the duration is 5 minutes, users in the user group are notified when the node linked to the notification group's CPU utilization is over 90% for over 5 minutes. If CPU utilization is over 90% but falls below 90% within 5 minutes, no notification is sent.

### Monitoring Settings Items

The following performance metric topics can be monitored:

| Category | Item | Unit |
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

### Add Monitoring Setting

![notification2.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification2.PNG)

❶ Click **Monitoring Settings** to open a pop-up where you can modify monitoring settings.
❷ Click **Add Monitoring Settings** to add a new monitoring setting.
❸ Enter the item to monitor, comparison method, threshold, and duration, then click **Add**.

### Change and Delete Monitoring Settings

![notification3.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification3.PNG)

❶ Click the button to modify an added monitoring settings.
❷ Click the button to delete an added monitoring settings.

## User Group

Users who receive notifications can be managed in groups. The notification target must be registered as a project member. If the users in the user group are excluded from the project members, they will not be notified, even if they belong to the user group.

!!! danger "Caution"
    If there is no mobile phone information because a user did not complete real-name verification, the user will not receive SMS notifications.

### Create a User Group

![notification4.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification4.PNG)

❶ Click **Create User Group** to open a pop-up where you can create a user group.
❷ Select All Project Members under **Notification Type** to automatically include all members of the project.
❸ Select Custom under **Notification Type** to display the notification target list in the user group.
❹ Click **Add** to display the project members that can be added to the notification targets.
❺ Click **Confirm** to create the user group. 

### Modify and Delete a User Group

![notification5.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification5.PNG)

❶ Click the button to modify an added user group.
❷ Click the button to delete an added user group.