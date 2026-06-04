## Network > Load Balancer(DSR) > Console Guide

<a id='manage-dsr-loadbalancers'></a>
## Load Balancer(DSR) Management

<a id='create-dsr-loadbalancers'></a>
### Create Load Balancer(DSR)
You can easily create a DSR-type load balancer in the NHN Cloud console by simply entering the load balancer(DSR) configuration values. The load balancer(DSR) operates using the DSR (direct server return) method, where server response traffic is sent directly to the client without passing through the load balancer, providing high processing performance.

The load balancer(DSR) creation screen consists of the following three areas:

#### 1. Load Balancer(DSR) Basic Information Settings

Configure basic information for the load balancer(DSR). The required items are as follows:

* Name: Enter the name of the load balancer(DSR).
* Description: Provide a description of the load balancer(DSR).
* VPC: Select the VPC to which the load balancer(DSR) will be connected.
* Subnet: Select the subnet where the load balancer(DSR) will be located. The load balancer(DSR) and member instances must be located in the same subnet.
* VIP (Virtual IP): The VIP address to be assigned to the load balancer(DSR). You can choose between **Auto-assign** or **Manual specification** for the assignment method.
  * Auto-assign: Automatically assigns one of the available IPs from the subnet to use as the VIP.
  * Manual specification: Directly enter the desired IP within the subnet's CIDR range to use as the VIP.

!!! danger "Caution"
    Creation will fail if the manually specified VIP address does not belong to the subnet's CIDR range. Be sure to specify within the IP range of the corresponding subnet.

!!! note "Note"
    The load balancer(DSR) operates at the TCP/UDP L4 level, and server response traffic does not pass through the load balancer. Therefore, unlike general load balancers, L7 features (HTTP header-based routing, SSL Offloading, listener/member group concepts, etc.) are not provided.

#### 2. Health Check Settings

Configure health checks to periodically verify that member instances are operating normally.

* Health check protocol: Select the protocol to use for health checks. Choose from **TCP / ICMP / HTTP**.
* Delay: The interval (in seconds) for sending health check requests.
* Max response wait time (timeout): The timeout duration (in seconds) for each health check request. If there is no response within this time, it is considered a failure.
* Max retry count: The maximum number of retries before determining an instance as abnormal. (1-10 times)

Configure the following additional items for each protocol:

**TCP**

* Health check port: Specify the port number to attempt TCP connections.

**ICMP**

* No separate port configuration is required. Connectivity is verified using ICMP Echo Request/Reply.

**HTTP**

* Health check port: Specify the port number to send HTTP requests.
* HTTP path (URL): Enter the URL path to perform health checks. The default value is `/`.
* Expected HTTP response code: Enter the HTTP response code to consider as a normal response. The default value is `200`.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

!!! note "Note"
    TCP/HTTP health checks make requests to the DSR VIP as the destination, so if the VIP is not configured on the member server's lo interface, those packets cannot be received and processed, causing health check failures and the member to be determined as `INACTIVE`. ICMP health checks make requests to the member's actual IP, so they only verify connectivity regardless of VIP configuration.

#### 3. Member Settings

Specify member instances to register when creating the load balancer(DSR). Member registration can also be done after creating the load balancer(DSR).

* Instance selection: Select instances (network interfaces) that belong to the same subnet as the load balancer(DSR). You can select one or more instances simultaneously to register as members.

!!! note "Note"
    The load balancer(DSR) forwards client requests to member instances while maintaining the destination port (VIP port) as is. Therefore, unlike general load balancers, when registering members, you do not specify service ports per member, and only select the network interface of member instances. The member server's application must bind to `0.0.0.0` or the VIP to listen for the same port that the client sent.

!!! danger "Caution"
    For member instances to properly receive and respond to traffic coming to the VIP, the following configuration is required inside the server:

    - Add VIP as an additional allowed address to the network interface (Console Network Interface menu)
    - Kernel parameter settings (`arp_ignore=1`, `arp_announce=2`)
    - Add VIP to the lo interface with `/32` subnet
    - Allow service port and health check traffic in Security Groups

    For detailed procedures, refer to the member server configuration guide in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

!!! note "Note"
    The initial state of newly registered members is `INACTIVE`. Once they pass health checks, they automatically transition to `ACTIVE` state and receive traffic.

After entering all items, click the **Create Load Balancer** button to create the load balancer(DSR).

<a id='view-dsr-loadbalancers'></a>
### View and Modify Load Balancer(DSR)

#### Load Balancer(DSR) List

After completing load balancer(DSR) creation, you can view basic information about the created load balancers(DSR) in the list screen. The items displayed in the list screen are as follows:

* Name: The name specified when creating the load balancer(DSR).
* VIP address: The private IP assigned to the load balancer(DSR). This IP can be accessed from within the VPC.
* Floating IP: The floating IP connected for external access.
* Network: The name of the VPC where the load balancer(DSR) belongs and the subnet CIDR.
* Member count: The number of member instances registered in the load balancer(DSR).
* Status: The creation/operation status of the load balancer(DSR).

!!! note "Note"
    The status of the load balancer(DSR) is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Operating normally |
    | `BUILD` | Creating load balancer(DSR) |
    | `ERROR` | Error occurred. Please contact the administrator. |

You can create additional load balancers(DSR) using the **+ Create DSR** button at the top, and delete load balancers(DSR) by selecting them with checkboxes in the list and clicking the **Delete** button.

#### Load Balancer(DSR) Detailed Information

When you select a load balancer(DSR) from the list, detailed information is displayed at the bottom of the screen. The detailed screen is divided into three tabs: **Basic Information**, **Members**, and **Health Check**.

In the **Basic Information** tab, you can view the following information:

* Name, description
* Subnet and VIP address
* Floating IP connection information
* Status

#### Change Name
To change the name of the load balancer(DSR), click the **Edit Name** icon in the detailed information, enter the name to change, and click the **Confirm** button.

#### Change Floating IP
You can connect or disconnect a floating IP to allow access to the load balancer(DSR) from external networks.

1. Click the **Change Floating IP** button in the load balancer(DSR) detailed information.
2. Select the floating IP to connect. To disconnect the floating IP, select **Not used**.
3. Click the **Confirm** button to apply the settings.

!!! note "Note"
    Even if you disconnect the floating IP, access through VIP from within the VPC is not affected.

!!! note "Note"
    The VPC, subnet, and VIP address connected to the load balancer(DSR) cannot be changed after creation. If changes are needed, you must delete the load balancer(DSR) and recreate it.

<a id='delete-dsr-loadbalancers'></a>
### Delete Load Balancer(DSR)
In the load balancer(DSR) list screen, select the load balancer(DSR) to delete, click the **Delete** button, and click the **Confirm** button in the confirmation window to delete the corresponding load balancer(DSR).

!!! danger "Caution"
    When you delete a load balancer(DSR), all members registered in that DSR are deleted together. If a floating IP is connected, it is automatically released.

<a id='manage-dsr-members'></a>
## Member Management

Select the desired load balancer(DSR) from the load balancer(DSR) list and click the **Members** tab to display the member instance management screen.

### Member List

In the **Members** tab, you can view the list and status of member instances registered in the load balancer(DSR). The items displayed in the list are as follows:

* IP address: The IP address of the member instance.
* Device model: The resource type that owns the network port registered as a member.
* Device information: The identification information of the network port registered as a member (instance name, port ID, etc.) is displayed in an integrated manner.
* Status: The current status of the member.

!!! note "Note"
    Since the load balancer(DSR) forwards client requests to members while maintaining the destination port as is, the L4 service port is not separately displayed in the member items. The actual service port is the port requested by the client to the VIP, and the member server's application must listen to that port.

!!! note "Note"
    The status of members is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Health check successful, target for traffic distribution |
    | `INACTIVE` | Health check failed or immediately after new registration, excluded from traffic distribution targets |
    | `ONLINE` | Member manually disabled |

<a id='add-dsr-members'></a>
### Add Members
Click the **+ Add Member** button in the **Members** tab to display the add member modal.

1. Select the **instance** to register as a member from the list. You can select one or more instances simultaneously.
2. Click the **Confirm** button to register the selected instances as members.

!!! note "Note"
    Unlike general load balancers, the load balancer(DSR) does not require entering L4 service ports in the member addition step. Since the load balancer(DSR) forwards client request destination ports to members without conversion, per-member port mapping is unnecessary.

!!! danger "Caution"
    Be aware of the following constraints when registering members:

    * Member instances must belong to the same subnet as the load balancer(DSR).
    * Only compute instances can be registered as members.
    * The same instance port cannot be registered multiple times in the same load balancer(DSR).
    * By default, up to 30 members can be registered in one load balancer(DSR).

!!! note "Note"
    To properly receive traffic after member registration, you need to add the VIP as an additional allowed address to the network interface and configure ARP kernel parameters, add VIP to the lo interface, and set Security Group rules inside the member server. For detailed procedures, refer to the member server configuration guide in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='delete-dsr-members'></a>
### Delete Members
Select the member to delete from the list in the Members tab, click the **Delete** button, and when a confirmation window appears, click the **Confirm** button to remove the corresponding member from the load balancer(DSR).

!!! note "Note"
    Deleting a member from the load balancer(DSR) does not delete the instance itself. Conversely, if you delete an instance registered as a member, that member is automatically removed from the load balancer(DSR).

<a id='manage-dsr-health-monitor'></a>
## Health Check Management

In the **Health Check** tab of the load balancer(DSR) detailed screen, you can view and change the currently configured health check information.

<a id='view-dsr-health-monitor'></a>
### View Health Check
In the **Health Check** tab, you can view the following information about the currently configured health check:

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
* Enter the required items for each protocol:
  * TCP: Health check port
  * ICMP: No additional items
  * HTTP: Health check port, HTTP path, expected HTTP response code
* Configure delay, max response wait time, and max retry count.

After completing the configuration, click the **Confirm** button to apply the changes.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

!!! note "Note"
    Health check requests are sent from a dedicated health check IP automatically assigned in the same subnet as the load balancer(DSR). The Security Group of member instances must allow such traffic for health checks to operate normally. For more information, refer to the Security Groups configuration section in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='dsr-quota'></a>
## Quota and Limitations

The following quotas and limitations apply when using load balancer(DSR):

| Item | Default Limit | Description |
|--|--|--|
| Number of load balancers(DSR) per project | 10 | Number of load balancers(DSR) that can be created per project |
| Number of members per load balancer(DSR) | 30 | Number of members that can be registered in one load balancer(DSR) |

!!! note "Note"
    If you need to use beyond the default quota, please contact customer support.