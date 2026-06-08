## Network > Load Balancer(DSR) > Console Guide

<a id='manage-dsr-loadbalancers'></a>
## Load Balancer (DSR) Management

<a id='create-dsr-loadbalancers'></a>
### Create Load Balancer (DSR)
You can easily create a DSR-type load balancer by entering load balancer (DSR) configuration values in the NHN Cloud console. Load Balancer (DSR) operates with the DSR (direct server return) method, where server response traffic is sent directly to clients without passing through the load balancer, providing high processing performance.

The Load Balancer (DSR) creation screen consists of the following three areas.

#### 1. Load Balancer (DSR) Basic Information Settings

Configure basic information for the load balancer (DSR). The required items are as follows:

* Name: Enter the name of the load balancer (DSR).
* Description: Describe the load balancer (DSR).
* VPC: Select the VPC to which the load balancer (DSR) will be connected.
* Subnet: Select the subnet to which the load balancer (DSR) will belong. The load balancer (DSR) and member instances must be located in the same subnet.
* VIP (Virtual IP): The VIP address to be assigned to the load balancer (DSR). You can choose between **Auto assign** or **Manual specification** for the assignment method.
  * Auto assign: Automatically assigns one of the available IPs in the subnet to use as VIP.
  * Manual specification: Directly enter the desired IP within the subnet's CIDR range to use as VIP.

> [Caution]
> If the manually specified VIP address does not belong to the subnet's CIDR range, creation will fail. Make sure to specify within the IP range of the subnet.

> [Note]
> Load Balancer (DSR) operates at the TCP/UDP L4 level, and server response traffic does not pass through the load balancer. Therefore, unlike general load balancers, L7 features (HTTP header-based routing, SSL Offloading, listener/member group concepts, etc.) are not provided.

#### 2. Health Check Settings

Configure health checks to periodically verify that member instances are operating normally.

* Health check protocol: Select the protocol to use for health checks. Choose one of **TCP / ICMP / HTTP**.
* Delay: The interval (seconds) for sending health check requests.
* Max response wait time (timeout): The timeout duration (seconds) for each health check request. If there is no response within this time, it is considered failed.
* Max retry count: The maximum number of retries before determining an instance as abnormal. (1-10 times)

Configure additional items for each protocol as follows.

**TCP**

* Health check port: Specify the port number to attempt TCP connection.

**ICMP**

* No separate port configuration is required. Connectivity is verified through ICMP Echo Request/Reply.

**HTTP**

* Health check port: Specify the port number to send HTTP requests.
* HTTP path (URL): Enter the URL path to perform health checks. The default value is `/`.
* Expected HTTP response code: Enter the HTTP response code to consider as a normal response. The default value is `200`.

> [Caution]
> The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

> [Note]
> TCP/HTTP health checks make requests to the DSR VIP as the destination, so if the VIP is not configured on the member server's lo interface, those packets cannot be received and processed, causing health checks to fail and members to be determined as `INACTIVE`. ICMP health checks make requests to the member's actual IP, so they only verify connectivity regardless of VIP configuration.

#### 3. Member Settings

Specify member instances to register when creating the load balancer (DSR). Member registration can also be done after load balancer (DSR) creation.

* Instance selection: Select instances (network interfaces) that belong to the same subnet as the load balancer (DSR). You can select one or more instances simultaneously to register as members.

> [Note]
> Load Balancer (DSR) forwards client requests to member instances while maintaining the destination port (VIP port) as-is. Therefore, unlike general load balancers, service ports per member are not specified when registering members, and only the network interface of member instances is selected. The application on the member server must bind to `0.0.0.0` or VIP to listen for the same port sent by the client.

> [Caution]
> For member instances to properly receive and respond to traffic coming to VIP, the following configuration is required inside the server:
> 
> - Add VIP as an additional allowed address to the network interface (Console Network Interface menu)
> - Kernel parameter configuration (`arp_ignore=1`, `arp_announce=2`)
> - Add VIP to lo interface as `/32` subnet
> - Allow service ports and health check traffic in Security Groups
> 
> For detailed procedures, refer to the member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

> [Note]
> The initial status of newly registered members is `INACTIVE`. They automatically transition to `ACTIVE` status and receive traffic after passing health checks.

After entering all items, click the **Create Load Balancer** button to create the load balancer (DSR).

<a id='view-dsr-loadbalancers'></a>
### View and Modify Load Balancer (DSR)

#### Load Balancer (DSR) List

After completing load balancer (DSR) creation, you can check the basic information of created load balancers (DSR) on the list screen. The items displayed on the list screen are as follows:

* Name: The name specified when creating the load balancer (DSR).
* VIP Address: The private IP assigned to the load balancer (DSR). This IP can be accessed from within the VPC.
* Floating IP: The floating IP connected for external access.
* Network: The name of the VPC and subnet CIDR to which the load balancer (DSR) belongs.
* Member Count: The number of member instances registered to the load balancer (DSR).
* Status: The creation/operation status of the load balancer (DSR).

> [Note]
> The status of load balancer (DSR) is determined as one of the following:
> 
> | Status | Meaning |
> |--|--|
> | `ACTIVE` | Operating normally |
> | `BUILD` | Load balancer (DSR) being created |
> | `ERROR` | Error occurred. Please contact administrator. |

You can create additional load balancers (DSR) with the **+ Create DSR** button at the top, and delete them by selecting load balancers (DSR) with checkboxes from the list and clicking the **Delete** button.

#### Load Balancer (DSR) Detailed Information

When you select a load balancer (DSR) from the list, detailed information is displayed at the bottom of the screen. The detailed screen is divided into three tabs: **Basic Information**, **Members**, and **Health Check**.

In the **Basic Information** tab, you can check the following information:

* Name, Description
* Subnet and VIP address
* Floating IP connection information
* Status

#### Change Name
To change the name of the load balancer (DSR), click the **Edit Name** icon in the detailed information, enter the name to change, and click the **Confirm** button.

#### Change Floating IP
You can connect or disconnect a floating IP so that the load balancer (DSR) can be accessed from external networks.

1. Click the **Change Floating IP** button in the load balancer (DSR) detailed information.
2. Select the floating IP to connect. To disconnect the floating IP, select **Do not use**.
3. Click the **Confirm** button to apply the settings.

> [Note]
> Even if you disconnect the floating IP, access through VIP from within the VPC is not affected.

> [Note]
> The VPC, subnet, and VIP address connected to the load balancer (DSR) cannot be changed after creation. If changes are needed, you must delete the load balancer (DSR) and recreate it.

<a id='delete-dsr-loadbalancers'></a>
### Delete Load Balancer (DSR)
Select the load balancer (DSR) to delete from the load balancer (DSR) list screen, click the **Delete** button, and click the **Confirm** button in the confirmation window to delete the load balancer (DSR).

> [Caution]
> When you delete a load balancer (DSR), all members registered to that DSR are deleted together. If a floating IP is connected, it is automatically released.

<a id='manage-dsr-members'></a>
## Member Management

Select the desired load balancer (DSR) from the load balancer (DSR) list and click the **Members** tab to display the member instance management screen.

### Member List

In the **Members** tab, you can check the list and status of member instances registered to the load balancer (DSR). The items displayed in the list are as follows:

* IP Address: The IP address of the member instance.
* Device Model: The resource type that owns the network port registered as a member.
* Device Information: The identification information (instance name, port ID, etc.) of the network port registered as a member is displayed in an integrated manner.
* Status: The current status of the member.

> [Note]
> Since load balancer (DSR) forwards client requests to members while maintaining the destination port as-is, L4 service ports are not separately displayed in member items. The actual service port is the port requested by the client to VIP, and the member server's application must listen for that port.

> [Note]
> The status of members is determined as one of the following:
> 
> | Status | Meaning |
> |--|--|
> | `ACTIVE` | Health check successful, target for traffic distribution |
> | `INACTIVE` | Health check failed or immediately after new registration, excluded from traffic distribution targets |
> | `ONLINE` | Member manually deactivated |

<a id='add-dsr-members'></a>
### Add Members
Click the **+ Add Member** button in the **Members** tab to display the add member modal.

1. Select **instances** to register as members from the list. You can select one or more instances simultaneously.
2. Click the **Confirm** button to register the selected instances as members.

> [Note]
> Unlike general load balancers, load balancer (DSR) does not enter L4 service ports during the member addition step. Since load balancer (DSR) forwards client requests' destination ports to members without conversion, per-member port mapping is unnecessary.

> [Caution]
> Note the following constraints when registering members:
> 
> * Member instances must belong to the same subnet as the load balancer (DSR).
> * Only compute instances can be registered as members.
> * The same instance port cannot be registered multiple times in the same load balancer (DSR).
> * A maximum of 30 members can be registered to one load balancer (DSR) by default.

> [Note]
> To properly receive traffic after member registration, you need to add VIP as an additional allowed address to the network interface, and configure ARP kernel parameters, add VIP to lo interface, and set Security Groups rules inside the member server. For detailed procedures, refer to the member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='delete-dsr-members'></a>
### Delete Members
Select the member to delete from the list in the Members tab, click the **Delete** button, and when the confirmation window appears, click the **Confirm** button to remove the member from the load balancer (DSR).

> [Note]
> Deleting a member from the load balancer (DSR) does not delete the instance itself. Conversely, if you delete an instance registered as a member, that member is automatically removed from the load balancer (DSR).

<a id='manage-dsr-health-monitor'></a>
## Health Check Management

In the **Health Check** tab of the load balancer (DSR) detailed screen, you can check and change the currently configured health check information.

<a id='view-dsr-health-monitor'></a>
### View Health Check
In the **Health Check** tab, you can check the following information of the currently configured health check:

* Health check protocol: TCP / ICMP / HTTP
* Health check port: Target port for health checks when using TCP or HTTP protocol
* Delay: Health check request interval (seconds)
* Max response wait time: Health check timeout (seconds)
* Max retry count: Number of retries until abnormal determination
* HTTP path (URL) / Expected HTTP response code: Displayed only when using HTTP protocol

<a id='change-dsr-health-monitor'></a>
### Change Health Check Settings
Click the **Change Settings** button in the **Health Check** tab to change health check settings.

* Health check protocol: Choose from TCP / ICMP / HTTP
* Enter required items for each protocol.
  * TCP: Health check port
  * ICMP: No additional items
  * HTTP: Health check port, HTTP path, expected HTTP response code
* Configure delay time, max response wait time, and max retry count.

After completing the configuration, click the **Confirm** button to apply the changes.

> [Caution]
> The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

> [Note]
> Health check requests are sent from a dedicated health check IP automatically assigned in the same subnet as the load balancer (DSR). The Security Group of member instances must allow this traffic for health checks to operate normally. For details, refer to the Security Groups configuration section in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='dsr-quota'></a>
## Quotas and Limitations

The following quotas and limitations apply when using load balancer (DSR):

| Item | Default Limit | Description |
|--|--|--|
| Number of load balancers (DSR) per project | 10 | Number of load balancers (DSR) that can be created per project |
| Number of members per load balancer (DSR) | 30 | Number of members that can be registered to one load balancer (DSR) |

> [Note]
> If you need to use beyond the default quota, please contact customer support.