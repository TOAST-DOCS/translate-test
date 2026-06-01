## Network > Load Balancer(DSR) > Console Guide

<a id='manage-dsr-loadbalancers'></a>
## Load Balancer (DSR) Management

<a id='create-dsr-loadbalancers'></a>
### Create Load Balancer (DSR)
You can easily create a DSR-type load balancer by simply entering the load balancer (DSR) configuration values in the NHN Cloud console. Load Balancer (DSR) operates in DSR (direct server return) mode, where server response traffic is sent directly to the client without going through the load balancer, providing high processing performance.

The Load Balancer (DSR) creation screen consists of the following three areas:

#### 1. Load Balancer (DSR) Basic Information Settings

Configure basic information for the Load Balancer (DSR). Required items are as follows:

* Name: Enter the name of the Load Balancer (DSR).
* Description: Describe the Load Balancer (DSR).
* VPC: Select the VPC to which the Load Balancer (DSR) will be connected.
* Subnet: Select the subnet where the Load Balancer (DSR) will belong. The Load Balancer (DSR) and member instances must be located in the same subnet.
* VIP (Virtual IP): The VIP address to be assigned to the Load Balancer (DSR). You can choose between **Auto assign** or **Manual assign**.
  * Auto assign: Automatically assigns one of the available IPs from the subnet as the VIP.
  * Manual assign: Directly enter the desired IP within the subnet's CIDR range to use as the VIP.

!!! danger "Caution"
    If the manually specified VIP address does not belong to the subnet's CIDR range, creation will fail. Be sure to specify it within that subnet's IP range.

!!! tip "Tips"
    Load Balancer (DSR) operates at the TCP/UDP L4 level, and server response traffic does not go through the load balancer. Therefore, unlike general load balancers, L7 features (HTTP header-based routing, SSL Offloading, listener/member group concepts, etc.) are not provided.

#### 2. Health Check Settings

Configure health checks to periodically verify that member instances are operating normally.

* Health check protocol: Select the protocol to use for health checks. Choose one of **TCP / ICMP / HTTP**.
* Delay time: The interval (seconds) for sending health check requests.
* Maximum response wait time (timeout): The timeout period (seconds) for each health check request. If there is no response within this time, it is considered a failure.
* Maximum retry count: The maximum number of retries before determining an instance as abnormal. (1-10 times)

Configure additional items by protocol as follows:

**TCP**

* Health check port: Specify the port number to attempt TCP connection to.

**ICMP**

* No separate port configuration is required. Connectivity is verified with ICMP Echo Request/Reply.

**HTTP**

* Health check port: Specify the port number to send HTTP requests to.
* HTTP path (URL): Enter the URL path to perform health checks on. Default is `/`.
* Expected HTTP response code: Enter the HTTP response code to be considered as normal response. Default is `200`.

!!! danger "Caution"
    Delay time must be greater than or equal to timeout. If timeout is greater than delay time, health checks may not operate normally.

!!! tip "Tips"
    TCP/HTTP health checks request to the DSR VIP as destination, so if the VIP is not configured on the member server's lo interface, those packets cannot be received and processed, causing health checks to fail and members to be judged as `INACTIVE`. ICMP health checks request to the member's actual IP, so they only verify connectivity regardless of VIP configuration.

#### 3. Member Settings

Specify member instances to register when creating the Load Balancer (DSR). Member registration can also be done after Load Balancer (DSR) creation.

* Instance selection: Select instances (network interfaces) that belong to the same subnet as the Load Balancer (DSR). You can select one or more instances simultaneously to register as members.

!!! tip "Tips"
    Load Balancer (DSR) forwards client requests to member instances while maintaining the destination port (VIP port) as is. Therefore, unlike general load balancers, it does not specify service ports per member when registering members, and only selects the network interface of the member instance. The member server's application must bind to `0.0.0.0` or VIP and listen for the same port sent by the client.

!!! danger "Caution"
    For member instances to properly receive and respond to traffic coming to the VIP, the following configuration is required inside the server:

    - Add VIP as additional allowed address to network interface (Console Network Interface menu)
    - Kernel parameter configuration (`arp_ignore=1`, `arp_announce=2`)
    - Add VIP to lo interface as `/32` subnet
    - Allow service port and health check traffic in Security Groups

    For detailed procedures, refer to the member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/ko/overview/).

!!! tip "Tips"
    The initial status of newly registered members is `INACTIVE`. Once they pass health checks, they automatically transition to `ACTIVE` status and receive traffic.

After entering all items, click the **Create Load Balancer** button to create the Load Balancer (DSR).

<a id='view-dsr-loadbalancers'></a>
### View and Modify Load Balancer (DSR)

#### Load Balancer (DSR) List

Once Load Balancer (DSR) creation is completed, you can check the basic information of created Load Balancers (DSR) on the list screen. Items displayed on the list screen are as follows:

* Name: The name specified when creating the Load Balancer (DSR).
* VIP Address: The private IP assigned to the Load Balancer (DSR). It can be accessed with this IP from within the VPC.
* Floating IP: The floating IP connected for external access.
* Network: The name of the VPC and subnet CIDR where the Load Balancer (DSR) belongs.
* Member Count: The number of member instances registered to the Load Balancer (DSR).
* Status: The creation/operation status of the Load Balancer (DSR).

!!! tip "Tips"
    The status of Load Balancer (DSR) is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Operating normally |
    | `BUILD` | Load Balancer (DSR) being created |
    | `ERROR` | Error occurred. Please contact administrator. |

You can create additional Load Balancers (DSR) with the **+ Create DSR** button at the top, and delete them by selecting Load Balancers (DSR) with checkboxes in the list and clicking the **Delete** button.

#### Load Balancer (DSR) Details

When you select a Load Balancer (DSR) from the list, detailed information is displayed at the bottom of the screen. The details screen is divided into three tabs: **Basic Information**, **Members**, and **Health Check**.

In the **Basic Information** tab, you can check the following information:

* Name, Description
* Subnet and VIP address
* Floating IP connection information
* Status

#### Change Name
To change the name of the Load Balancer (DSR), click the **Modify Name** icon in the detailed information, enter the name to change, and click the **OK** button.

#### Change Floating IP
You can connect or disconnect floating IP to allow access to the Load Balancer (DSR) from external networks.

1. Click the **Change Floating IP** button in the Load Balancer (DSR) details.
2. Select the floating IP to connect. To disconnect floating IP, select **Not use**.
3. Click the **OK** button to apply the settings.

!!! tip "Tips"
    Even if you disconnect the floating IP, access through VIP from within the VPC is not affected.

!!! tip "Tips"
    The VPC, subnet, and VIP address connected to the Load Balancer (DSR) cannot be changed after creation. If changes are needed, you must delete the Load Balancer (DSR) and recreate it.

<a id='delete-dsr-loadbalancers'></a>
### Delete Load Balancer (DSR)
On the Load Balancer (DSR) list screen, select the Load Balancer (DSR) you want to delete, click the **Delete** button, and click the **OK** button in the confirmation window to delete the Load Balancer (DSR).

!!! danger "Caution"
    When you delete a Load Balancer (DSR), all members registered to that DSR are deleted together. If a floating IP is connected, it is automatically released.

<a id='manage-dsr-members'></a>
## Member Management

Select the desired Load Balancer (DSR) from the Load Balancer (DSR) list and click the **Members** tab to display the member instance management screen.

### Member List

In the **Members** tab, you can check the list and status of member instances registered to the Load Balancer (DSR). Items displayed in the list are as follows:

* IP Address: The IP address of the member instance.
* Device Model: The resource type that owns the network port registered as a member.
* Device Information: Integrated display of identification information (instance name, port ID, etc.) of the network port registered as a member.
* Status: Current status of the member.

!!! tip "Tips"
    Since Load Balancer (DSR) forwards to members while maintaining the client request's destination port as is, L4 service ports are not separately displayed in member items. The actual service port is the port requested by the client to the VIP, and the member server's application must listen on that port.

!!! tip "Tips"
    The status of members is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Health check successful, traffic distribution target |
    | `INACTIVE` | Health check failed or immediately after new registration, excluded from traffic distribution target |
    | `ONLINE` | Member manually disabled |

<a id='add-dsr-members'></a>
### Add Members
Click the **+ Add Members** button in the **Members** tab to open the member addition modal.

1. Select **instances** from the list to register as members. You can select one or more instances simultaneously.
2. Click the **OK** button to register the selected instances as members.

!!! tip "Tips"
    Unlike general load balancers, Load Balancer (DSR) does not enter L4 service ports during the member addition step. Since Load Balancer (DSR) forwards the client request's destination port to members without conversion, per-member port mapping is unnecessary.

!!! danger "Caution"
    Be aware of the following constraints when registering members:

    * Member instances must belong to the same subnet as the Load Balancer (DSR).
    * Only compute instances can be registered as members.
    * The same instance port cannot be registered multiple times to the same Load Balancer (DSR).
    * By default, up to 30 members can be registered to one Load Balancer (DSR).

!!! tip "Tips"
    To properly receive traffic after member registration, you need to add VIP as additional allowed address to network interface and configure ARP kernel parameters, add VIP to lo interface, and set Security Groups rules inside the member server. For detailed procedures, refer to the member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/ko/overview/).

<a id='delete-dsr-members'></a>
### Delete Members
Select the member to delete from the list in the Members tab, then click the **Delete** button. When the confirmation window appears, click the **OK** button to remove that member from the Load Balancer (DSR).

!!! tip "Tips"
    Deleting a member from the Load Balancer (DSR) does not delete the instance itself. Conversely, if you delete an instance registered as a member, that member is automatically removed from the Load Balancer (DSR).

<a id='manage-dsr-health-monitor'></a>
## Health Check Management

In the **Health Check** tab of the Load Balancer (DSR) details screen, you can check and change the currently configured health check information.

<a id='view-dsr-health-monitor'></a>
### View Health Check
In the **Health Check** tab, you can check the following information of the currently configured health check:

* Health check protocol: TCP / ICMP / HTTP
* Health check port: Health check target port when using TCP or HTTP protocol
* Delay time: Health check request interval (seconds)
* Maximum response wait time: Health check timeout (seconds)
* Maximum retry count: Number of retries until abnormal determination
* HTTP path (URL) / Expected HTTP response code: Displayed only when using HTTP protocol

<a id='change-dsr-health-monitor'></a>
### Change Health Check Settings
Click the **Change Settings** button in the **Health Check** tab to change health check settings.

* Health check protocol: Choose from TCP / ICMP / HTTP
* Enter required items by protocol:
  * TCP: Health check port
  * ICMP: No additional items
  * HTTP: Health check port, HTTP path, expected HTTP response code
* Configure delay time, maximum response wait time, and maximum retry count.

After completing configuration, click the **OK** button to apply changes.

!!! danger "Caution"
    Delay time must be greater than or equal to timeout. If timeout is greater than delay time, health checks may not operate normally.

!!! tip "Tips"
    Health check requests are sent from a dedicated health check IP automatically assigned to the same subnet as the Load Balancer (DSR). The member instance's Security Group must allow this traffic for health checks to operate normally. For details, refer to the Security Groups configuration section in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/ko/overview/).

<a id='dsr-quota'></a>
## Quotas and Restrictions

The following quotas and restrictions apply when using Load Balancer (DSR):

| Item | Default Limit | Description |
|--|--|--|
| Number of Load Balancers (DSR) per project | 10 | Number of Load Balancers (DSR) that can be created per project |
| Number of members per Load Balancer (DSR) | 30 | Number of members that can be registered to one Load Balancer (DSR) |

!!! tip "Tips"
    If you need to use beyond the default quota, please contact customer support.