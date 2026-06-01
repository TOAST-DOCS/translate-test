## Network > Load Balancer(DSR) > Console Guide

<a id='manage-dsr-loadbalancers'></a>
## Load Balancer (DSR) Management

<a id='create-dsr-loadbalancers'></a>
### Create Load Balancer (DSR)
You can easily create a DSR-type load balancer by simply entering the load balancer (DSR) configuration values in the NHN Cloud console. Load balancer (DSR) operates using the DSR (direct server return) method, where server response traffic is sent directly to the client without going through the load balancer, providing high processing performance.

The load balancer (DSR) creation screen consists of the following three sections.

#### 1. Load Balancer (DSR) Basic Information Settings

Configure basic information for the load balancer (DSR). The required items are as follows:

* Name: Enter the name of the load balancer (DSR).
* Description: Describe the load balancer (DSR).
* VPC: Select the VPC to which the load balancer (DSR) will be connected.
* Subnet: Select the subnet to which the load balancer (DSR) will belong. The load balancer (DSR) and member instances must be located in the same subnet.
* VIP (Virtual IP): The VIP address to be assigned to the load balancer (DSR). You can choose between **Auto assign** or **Manual assign** allocation methods.
  * Auto assign: Automatically allocates one of the available IPs in the subnet and uses it as the VIP.
  * Manual assign: Directly enter the desired IP within the subnet's CIDR range and use it as the VIP.

!!! danger "Caution"
    If the directly specified VIP address does not belong to the subnet's CIDR range, creation will fail. Make sure to specify it within the IP range of the subnet.

!!! tip "Note"
    Load balancer (DSR) operates at the TCP/UDP L4 level, and server response traffic does not go through the load balancer. Therefore, unlike general load balancers, L7 features (HTTP header-based routing, SSL Offloading, listener/member group concepts, etc.) are not provided.

#### 2. Health Check Settings

Configure health checks that periodically verify whether member instances are operating normally.

* Health check protocol: Select the protocol to use for health checks. Choose one of **TCP / ICMP / HTTP**.
* Delay: The interval (seconds) for sending health check requests.
* Max response timeout (timeout): The timeout period (seconds) for each health check request. If there is no response within this time, it is considered a failure.
* Max retry count: The maximum number of retries before determining an instance as unhealthy. (1~10 times)

Set additional items for each protocol as follows.

**TCP**

* Health check port: Specify the port number to attempt TCP connection.

**ICMP**

* No separate port configuration is required. Connectivity is verified through ICMP Echo Request/Reply.

**HTTP**

* Health check port: Specify the port number to send HTTP requests.
* HTTP path (URL): Enter the URL path to perform health checks. The default value is `/`.
* Expected HTTP response code: Enter the HTTP response code to consider as a normal response. The default value is `200`.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

!!! tip "Note"
    TCP/HTTP health checks request with the DSR VIP as the destination, so if the VIP is not configured on the member server's lo interface, the packets cannot be received and processed, causing health checks to fail and the member to be determined as `INACTIVE`. ICMP health checks request to the member's actual IP, so they only verify connectivity regardless of VIP configuration.

#### 3. Member Settings

Specify member instances to register when creating the load balancer (DSR). Member registration can also be done after creating the load balancer (DSR).

* Instance selection: Select instances (network interfaces) that belong to the same subnet as the load balancer (DSR). You can select multiple instances simultaneously and register them as members.

!!! tip "Note"
    Load balancer (DSR) forwards client requests to member instances while maintaining the destination port (VIP port) as-is. Therefore, unlike general load balancers, member-specific service ports are not specified when registering members, and only the network interface of member instances is selected. The member server's application must bind to `0.0.0.0` or VIP and listen on the same port sent by the client.

!!! danger "Caution"
    For member instances to properly receive and respond to traffic coming to the VIP, the following configuration is required inside the server:

    - Add VIP as an additional allowed address to the network interface (Console Network Interface menu)
    - Kernel parameter configuration (`arp_ignore=1`, `arp_announce=2`)
    - Add VIP to lo interface as `/32` subnet
    - Allow service port and health check traffic in Security Groups

    For detailed procedures, refer to the member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/ko/overview/).

!!! tip "Note"
    The initial status of newly registered members is `INACTIVE`. They automatically transition to `ACTIVE` status and receive traffic after passing health checks.

After entering all items, click the **Create Load Balancer** button to create the load balancer (DSR).

<a id='view-dsr-loadbalancers'></a>
### View and Modify Load Balancer (DSR)

#### Load Balancer (DSR) List

After completing load balancer (DSR) creation, you can check the basic information of created load balancers (DSR) on the list screen. The items displayed on the list screen are as follows:

* Name: The name specified when creating the load balancer (DSR).
* VIP address: The private IP assigned to the load balancer (DSR). This IP can be accessed from within the VPC.
* Floating IP: The floating IP connected for external access.
* Network: The name of the VPC to which the load balancer (DSR) belongs and the subnet CIDR.
* Member count: The number of member instances registered to the load balancer (DSR).
* Status: The creation/operation status of the load balancer (DSR).

!!! tip "Note"
    The status of load balancer (DSR) is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Operating normally |
    | `BUILD` | Load balancer (DSR) creation in progress |
    | `ERROR` | Error occurred. Please contact the administrator. |

You can create additional load balancers (DSR) with the **+ Create DSR** button at the top, and delete them by selecting load balancers (DSR) with checkboxes from the list and clicking the **Delete** button.

#### Load Balancer (DSR) Detailed Information

When you select a load balancer (DSR) from the list, detailed information is displayed at the bottom of the screen. The detailed screen is divided into three tabs: **Basic Information**, **Members**, and **Health Check**.

In the **Basic Information** tab, you can check the following information:

* Name, description
* Subnet and VIP address
* Floating IP connection information
* Status

#### Change Name
To change the name of the load balancer (DSR), click the **Modify Name** icon in the detailed information, enter the name to change, and click the **OK** button.

#### Change Floating IP
You can connect or disconnect floating IP to allow access to the load balancer (DSR) from external networks.

1. Click the **Change Floating IP** button in the load balancer (DSR) detailed information.
2. Select the floating IP to connect. To disconnect the floating IP, select **Disabled**.
3. Click the **OK** button to apply the settings.

!!! tip "Note"
    Even if you disconnect the floating IP, access through VIP from within the VPC is not affected.

!!! tip "Note"
    The VPC, subnet, and VIP address to which the load balancer (DSR) is connected cannot be changed after creation. If changes are needed, you must delete the load balancer (DSR) and recreate it.

<a id='delete-dsr-loadbalancers'></a>
### Delete Load Balancer (DSR)
Select the load balancer (DSR) to delete from the load balancer (DSR) list screen, click the **Delete** button, and click the **OK** button in the confirmation window to delete the load balancer (DSR).

!!! danger "Caution"
    Deleting a load balancer (DSR) will also delete all members registered to that DSR. If a floating IP is connected, it will be automatically released.

<a id='manage-dsr-members'></a>
## Member Management

Select the desired load balancer (DSR) from the load balancer (DSR) list and click the **Members** tab to display the member instance management screen.

### Member List

In the **Members** tab, you can check the list and status of member instances registered to the load balancer (DSR). The items displayed in the list are as follows:

* IP address: The IP address of the member instance.
* Device model: The owner resource type of the network port registered as a member.
* Device information: The identification information (instance name, port ID, etc.) of the network port registered as a member is displayed in an integrated manner.
* Status: The current status of the member.

!!! tip "Note"
    Since load balancer (DSR) forwards to members while maintaining the destination port of client requests as-is, L4 service ports are not separately displayed in member items. The actual service port is the port requested by the client to the VIP, and the member server's application must listen on that port.

!!! tip "Note"
    The status of members is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Health check successful, traffic distribution target |
    | `INACTIVE` | Health check failed or immediately after new registration, excluded from traffic distribution target |
    | `ONLINE` | Member manually disabled |

<a id='add-dsr-members'></a>
### Add Members
Click the **+ Add Member** button in the **Members** tab to display the add member modal.

1. Select **instances** to register as members from the list. You can select multiple instances simultaneously.
2. Click the **OK** button to register the selected instances as members.

!!! tip "Note"
    Unlike general load balancers, load balancer (DSR) does not enter L4 service ports during the member addition step. Since load balancer (DSR) forwards the destination port of client requests to members without conversion, port mapping per member is unnecessary.

!!! danger "Caution"
    Pay attention to the following constraints when registering members:

    * Member instances must belong to the same subnet as the load balancer (DSR).
    * Only compute instances can be registered as members.
    * The same instance port cannot be registered multiple times in the same load balancer (DSR).
    * By default, up to 30 members can be registered to one load balancer (DSR).

!!! tip "Note"
    To properly receive traffic after member registration, you need to add VIP as an additional allowed address to the network interface, and configure ARP kernel parameters, add VIP to lo interface, and set Security Groups rules inside the member server. For detailed procedures, refer to the member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/ko/overview/).

<a id='delete-dsr-members'></a>
### Delete Members
Select the member to delete from the list in the members tab, then click the **Delete** button. When the confirmation window appears, click the **OK** button to remove the member from the load balancer (DSR).

!!! tip "Note"
    Deleting a member from the load balancer (DSR) does not delete the instance itself. Conversely, if you delete an instance registered as a member, that member is automatically removed from the load balancer (DSR).

<a id='manage-dsr-health-monitor'></a>
## Health Check Management

In the **Health Check** tab of the load balancer (DSR) detailed screen, you can check the currently configured health check information and make changes.

<a id='view-dsr-health-monitor'></a>
### View Health Check
In the **Health Check** tab, you can check the following information about the currently configured health check:

* Health check protocol: TCP / ICMP / HTTP
* Health check port: Health check target port when using TCP or HTTP protocol
* Delay: Health check request interval (seconds)
* Max response timeout: Health check timeout (seconds)
* Max retry count: Number of retries until unhealthy determination
* HTTP path (URL) / Expected HTTP response code: Displayed only when using HTTP protocol

<a id='change-dsr-health-monitor'></a>
### Change Health Check Settings
Click the **Change Settings** button in the **Health Check** tab to change health check settings.

* Health check protocol: Select from TCP / ICMP / HTTP
* Enter required items for each protocol.
  * TCP: Health check port
  * ICMP: No additional items
  * HTTP: Health check port, HTTP path, expected HTTP response code
* Configure delay time, max response timeout, and max retry count.

Click the **OK** button after completing settings to apply the changes.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

!!! tip "Note"
    Health check requests are sent from a dedicated health check IP automatically assigned to the same subnet as the load balancer (DSR). The member instance's Security Group must allow such traffic for health checks to operate normally. For more details, refer to the Security Groups configuration section in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/ko/overview/).

<a id='dsr-quota'></a>
## Quota and Limitations

The following quotas and limitations apply when using load balancer (DSR).

| Item | Default Limit | Description |
|--|--|--|
| Number of load balancers (DSR) per project | 10 | Number of load balancers (DSR) that can be created per project |
| Number of members per load balancer (DSR) | 30 | Number of members that can be registered to one load balancer (DSR) |

!!! tip "Note"
    If you need to use beyond the default quota, please contact customer support.