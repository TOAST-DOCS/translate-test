## Network > Traffic Mirroring > Console User Guide

This guide describes how to use the Traffic Mirroring service from the console.

## Manage a Mirror Session

You can easily create a mirror session just by entering setting values from the console.

#### Mirror Session Information
Enter basic information on the mirror session. The following items are required. 

* Name: Enter a name for the mirror session. 
* Description: Describe the mirror session. 
* Direction: Set the monitoring direction for network packets. You can select one of Outbound and Inbound or both. 
* Mirror source port: Specify the network interface to monitor network packets. Only the instance's network interface can be specified. 
* Mirror target port: Specify the network interface to send network packets copied from the mirror source. Only the network interface of the instance can be specified. 
* Filter group: You can specify the filter group that is created. You can choose no or multiple items.

> [Caution] The network interface designated as the mirror target port becomes unable to communicate. If communication from the mirror target instance is required, you must add an MGMT network interface.
>
> [Caution] If no filter group is specified, traffic is not mirrored. 

> [Note] You cannot create a mirror session if the mirror source and mirror target are in the same mirror session.
>
> [Note] Network interfaces registered as mirror sources cannot be registered as mirror targets. Similarly, network interfaces registered as mirror targets cannot be registered as mirror sources.
>
> [Note] If a network interface registered as a mirror source and mirror target is deleted, the attached mirror session is also automatically deleted.

### About Mirror Session Information
After creating a mirror session, you return to the Mirror Session List screen. In Mirror Session List, you can find the basic information on the created mirror session. Items that appear on the list screen are as follows.

* Name: Name of the mirror session specified when creating the mirror session. 
* Description: Description of the mirror session specified when creating the mirror session.
* Tenant ID: ID of the project that created the mirror session. 
* Mirror Source Port: Displays information about the network interface that you specified as the mirror source when you created the mirror session. 
* Mirror Target Port: Displays information about the network interface that you specified as a mirror target when you created the mirror session.
* Mirror Filter Group: Displays information about the mirror filter group that is specified when creating the mirror session.

### Modify a Mirror Session
On Mirror Session List screen, select the desired mirror session and press the **Change Session** button to modify the settings of the mirror session.
> [Note] It is not allowed to change the mirror source port, mirror target port, and direction of the mirror session.

### Delete a Mirror Session
On the Mirror Session List screen, select the mirror session you want to delete and click the Delete button to delete the mirror session.

## Mirror Filter
You can create filter groups and rules to use in mirror sessions.

### Mirror Filter Group Information
Enter basic information for the mirror filter group. Required items are as follows. 

* Name: Enter a name for the mirror filter group.
* Description: Describe the mirror filter group.

### About Mirror Filter Groups
When you have finished creating a mirror filter group, you are returned to the Mirror Filter Group List screen.  Mirror Filter Group List screen allows you to view basic information about the created mirror filter group. Items that appear on the list screen are as follows.

#### Basic Information
* Name: Name of the mirror filter group specified when creating the mirror filter group. 
* Description:  Description of the mirror filter group specified when creating the mirror filter group.
* Tenant ID: The ID of the project that created the mirror filter group.

#### Filter Rules
Filter rules that belong to the filter group are listed. **Create Filter Rule**, **Change Filter Rule** and **Delete Filter Rule** that allow you to create, change and delete rules. 
The following items are required for filter rules.

* Protocol: Select protocols such as TCP, UDP, ICMP, etc.
* Departure Port: Enter the departure port or range. Enter if the protocol is TCP or UDP.
* Destination Port: Enter the destination port or range. Enter if the protocol is TCP or UDP. 
* Departure CIDR: Enter the departure IP or CIDR block.
* Destination IDR: Enter the destination IP or CIDR block.
* Order: Enter the order of application. This indicates the priority to which the filter rule applies, and the lower value is to be applied first.
* Application Method: Enter the action to be implemented if matched. You can select either Allow or Block.
* Description:  Describe the filter rules.

> [Note] Only description items can be changed for filter rules. If required to change other items, you must delete them and recreate them.


### Modify Mirror Filter Group
On the Mirror Filter Group List screen, select the desired mirror filter group and click the **Change Filter Group** button to modify the settings of the mirror filter group.

### Delete Mirror Filter Group
On the Mirror Filter Groups list screen, select the mirror filter group you want to delete and click the Delete button to delete the mirror filter group.
> [Note] If the mirror filter group is deleted, filter rules attached to mirror filter groups are automatically deleted.

> [Note] Filter groups attached to mirror sessions cannot be deleted.
