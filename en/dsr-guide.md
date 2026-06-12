## Network > Load Balancer(DSR) > Console User Guide

<a id='manage-dsr-loadbalancers'></a>
## Manage Load Balancer (DSR)

<a id='create-dsr-loadbalancers'></a>
### Create Load Balancer (DSR)
You can easily create a DSR-type load balancer by simply entering the settings in the NHN Cloud console. Load Balancer (DSR) operates in direct server return (DSR) mode, allowing server response traffic to be sent directly to the client without passing through the load balancer, providing high throughput.

The Load Balancer (DSR) creation screen consists of the following three sections.

#### 1. Configure Load Balancer (DSR) Basic Information

Configure the basic information for Load Balancer (DSR). The required items are as follows:

* Name: Enter the name of Load Balancer (DSR).
* Description: Describe Load Balancer (DSR).
* VPC: Select the VPC to which Load Balancer (DSR) will be connected.
* Subnet: Select the subnet where Load Balancer (DSR) will belong. Load Balancer (DSR) and member instances must be located in the same subnet.
* VIP (Virtual IP): The VIP address to assign to Load Balancer (DSR). You can select either **Auto Assign** or **Manual Assign** as the allocation method.
  * Auto Assign: Automatically assigns one of the available IPs in the subnet and uses it as VIP.
  * Manual Assign: Directly enter the desired IP within the subnet's CIDR range and use it as VIP.

!!! danger "Caution"
    Creation will fail if the directly specified VIP address is not within the subnet's CIDR range. Make sure to specify it within the IP range of the subnet.

!!! tip "Note"
Load Balancer (DSR) operates at the TCP/UDP L4 level, and server response traffic does not pass through the load balancer. Therefore, unlike a standard load balancer, L7 features such as HTTP header-based routing, SSL offloading, and the listener/member group concept are not provided.

#### 2. Configure Health Check

Configure health checks that periodically verify whether member instances are operating normally.

* Health Check Protocol: Select the protocol to use for health checks. Choose one of **TCP / ICMP / HTTP**.
* Delay: The interval (seconds) at which health check requests are sent.
* Max Response Wait Time (Timeout): The timeout (seconds) for each health check request. If there is no response within this time, it is considered a failure.
* Max Retry Count: The maximum number of retries before determining an instance as abnormal. (1-10 times)

Configure additional items per protocol as follows:

**TCP**

* Health Check Port: Specify the port number for TCP connection attempts.

**ICMP**

* No separate port configuration is required. Connectivity is verified through ICMP Echo Request/Reply.

**HTTP**

* Health Check Port: Specify the port number for HTTP requests.
* HTTP Path (URL): Enter the URL path for health checks. The default is `/`.
* Expected HTTP Response Code: Enter the HTTP response code to consider as a normal response. The default is `200`.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not function properly.

!!! tip "Note"
TCP/HTTP health checks send requests to the DSR VIP as the destination, if the VIP is not configured on the lo interface of the member server, the packets cannot be received or processed, causing the health check to fail and the member to be marked as `INACTIVE`. ICMP health checks send requests to the actual IP of the member, so they only verify connectivity regardless of the VIP configuration.

#### 3. Configure Members

Specify the member instances to register when creating Load Balancer (DSR). Member registration can also be done after creating Load Balancer (DSR).

* Select Instance: Select instances (network interfaces) that belong to the same subnet as Load Balancer (DSR). You can select one or more instances simultaneously and register them as members.

!!! tip "Note"
Load Balancer (DSR) forwards client requests to member instances while preserving the destination port of the client request (VIP port). Therefore, unlike a standard load balancer, the service port is not specified per member when registering members; only the network interface of the member instance is selected. The application on the member server must be bound to `0.0.0.0` or the VIP and listen on the same port that the client sends requests to.

!!! danger "Caution"
    For member instances to properly receive and respond to traffic coming to the VIP, the following settings are required within the server:

    - Add the VIP as an additional allowed address on the network interface (console Network Interface menu)
    - Configure kernel parameters (`arp_ignore=1`, `arp_announce=2`)
    - Add the VIP to the `lo` interface with a `/32` subnet
    - Allow service port and health check traffic in Security Groups

    For detailed instructions, see the Member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

!!! tip "Note"
The initial status of a newly registered member is `INACTIVE`. Once the health check passes, the status automatically transitions to `ACTIVE` and the member begins receiving traffic.

After entering all items, click the **Create Load Balancer** button to create Load Balancer (DSR).

<a id='view-dsr-loadbalancers'></a>
### View and Modify Load Balancer (DSR)

#### Load Balancer (DSR) List

After completing the creation of Load Balancer (DSR), you can check the basic information of the created Load Balancers (DSR) on the list screen. The items exposed on the list screen are as follows:

* Name: The name specified when creating Load Balancer (DSR).
* VIP Address: The private IP assigned to Load Balancer (DSR). You can access with this IP from within the VPC.
* Floating IP: The floating IP connected for external access.
* Network: The name of the VPC and subnet CIDR where Load Balancer (DSR) belongs.
* Member Count: The number of member instances registered in Load Balancer (DSR).
* Status: The creation/operation status of Load Balancer (DSR).

!!! tip "Note"
    The status of Load Balancer (DSR) is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Operating normally |
    | `BUILD` | Creating Load Balancer (DSR) |
    | `ERROR` | Error occurred. Please contact administrator. |

You can create additional Load Balancers (DSR) with the **+ Create DSR** button at the top, and delete them by selecting Load Balancers (DSR) with checkboxes from the list and clicking the **Delete** button.

#### Load Balancer (DSR) Details

When you select Load Balancer (DSR) from the list, detailed information is displayed at the bottom of the screen. The detail screen is divided into three tabs: **Basic Information**, **Members**, and **Health Check**.

In the **Basic Information** tab, you can check the following information:

* Name, Description
* Subnet and VIP address
* Floating IP connection information
* Status

#### Change Name
To change the name of Load Balancer (DSR), click the **Edit Name** icon in the detailed information, enter the name to change, and click the **OK** button.

#### Change Floating IP
You can connect or disconnect floating IPs so that Load Balancer (DSR) can be accessed from external networks.

1. Click the **Change Floating IP** button in the Load Balancer (DSR) details.
2. Select the floating IP to connect. To disconnect the floating IP, select **Disable**.
3. Click the **OK** button to apply the settings.

!!! tip "Note"
    Even if you disconnect the floating IP, access through the VIP from within the VPC is not affected.

!!! tip "Note"
    The VPC, subnet, and VIP address connected to Load Balancer (DSR) cannot be changed after creation. If changes are needed, you must delete Load Balancer (DSR) and recreate it.

<a id='delete-dsr-loadbalancers'></a>
### Delete Load Balancer (DSR)
On the Load Balancer (DSR) list screen, select the Load Balancer (DSR) you want to delete, click the **Delete** button, and click the **OK** button in the confirmation window to delete the Load Balancer (DSR).

!!! danger "Caution"
    When you delete Load Balancer (DSR), all members registered to that DSR are also deleted. If a floating IP is connected, it is automatically released.

<a id='manage-dsr-members'></a>
## Manage Members

Select the desired Load Balancer (DSR) from the Load Balancer (DSR) list and click the **Members** tab to display the member instance management screen.

### Member List

In the **Members** tab, you can check the list and status of member instances registered in Load Balancer (DSR). The items displayed in the list are as follows:

* IP Address: The IP address of the member instance.
* Device Model: The owner resource type of the network port registered as a member.
* Device Information: The identification information (instance name, port ID, etc.) of the network port registered as a member is displayed in an integrated manner.
* Status: The current status of the member.

!!! tip "Note"
Since Load Balancer (DSR) forwards client requests to members while preserving the destination port, the L4 service port is not displayed separately in the member list. The actual service port is the port that the client uses to send requests to the VIP, and the application on the member server must listen on the port.

!!! tip "Note"
    The status of members is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Health check successful, target for traffic distribution |
    | `INACTIVE` | Health check failed or immediately after new registration, excluded from traffic distribution |
    | `ONLINE` | Member manually disabled |

<a id='add-dsr-members'></a>
### Add Members
Click the **+ Add Member** button in the **Members** tab to display the add member modal.

1. Select **instances** to register as members from the list. You can select one or more instances simultaneously.
2. Click the **OK** button to register the selected instances as members.

!!! tip "Note"
    Unlike a standard load balancer, Load Balancer (DSR) does not input L4 service ports during the member addition step. Since Load Balancer (DSR) forwards client requests' destination ports to members without conversion, per-member port mapping is unnecessary.

!!! danger "Caution"
    Pay attention to the following restrictions when registering members:

    * Member instances must belong to the same subnet as Load Balancer (DSR).
    * Only compute instances can be registered as members.
    * The same instance port cannot be registered more than once in the same Load Balancer (DSR).
    * A single Load Balancer (DSR) can register up to 30 members by default.

!!! tip "Note"
To properly receive traffic after registering a member, add the VIP as an additional allowed address on the network interface, and configure the ARP kernel parameters, add the VIP to the lo interface, and set up Security Groups rules within the member server. For detailed instructions, see the Member server configuration guide in Load Balancer (DSR) Overview.

<a id='delete-dsr-members'></a>
### Delete Members
Select the member to delete from the list in the Members tab, then click the **Delete** button. When the confirmation window appears, click the **OK** button to remove that member from Load Balancer (DSR).

!!! tip "Note"
    Deleting a member from Load Balancer (DSR) does not delete the instance itself. Conversely, if you delete an instance registered as a member, that member is automatically removed from Load Balancer (DSR).

<a id='manage-dsr-health-monitor'></a>
## Manage Health Check

In the **Health Check** tab of the Load Balancer (DSR) details screen, you can check and change the currently configured health check information.

<a id='view-dsr-health-monitor'></a>
### View Health Check
In the **Health Check** tab, you can check the following information about the currently configured health check:

* Health Check Protocol: TCP / ICMP / HTTP
* Health Check Port: Target port for health checks when using TCP or HTTP protocol
* Delay: Health check request interval (seconds)
* Max Response Wait Time: Health check timeout (seconds)
* Max Retry Count: Number of retries until abnormal determination
* HTTP Path (URL) / Expected HTTP Response Code: Displayed only when using HTTP protocol

<a id='change-dsr-health-monitor'></a>
### Change Health Check Settings
Click the **Change Settings** button in the **Health Check** tab to change the health check settings.

* Health Check Protocol: Select from TCP / ICMP / HTTP
* Enter required items per protocol.
  * TCP: Health check port
  * ICMP: No additional items
  * HTTP: Health check port, HTTP path, expected HTTP response code
* Configure delay time, max response wait time, and max retry count.

After completing the configuration, click the **OK** button to apply the changes.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not function properly.

!!! tip "Note"
Health check requests are sent from a dedicated health check IP automatically assigned to the same subnet as Load Balancer (DSR). The Security Group of member instances must allow this traffic for health checks to function correctly. For more information, see the Security Groups configuration section in the Load Balancer (DSR) Overview.

<a id='dsr-quota'></a>
## Quota and Restrictions

The following quotas and restrictions apply when using Load Balancer (DSR).

| Item | Default Limit | Description |
|--|--|--|
| Number of Load Balancers (DSR) per project | 10 | Number of Load Balancers (DSR) that can be created per project |
| Number of members per Load Balancer (DSR) | 30 | Number of members that can be registered in one Load Balancer (DSR) |

!!! tip "Note"
    If you need to exceed the default quotas, please contact customer support.