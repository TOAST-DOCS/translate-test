## Network > Load Balancer(DSR) > Console Guide

<a id='manage-dsr-loadbalancers'></a>
## Load Balancer(DSR) Management

<a id='create-dsr-loadbalancers'></a>
### Create Load Balancer(DSR)
You can easily create a DSR-type load balancer in the NHN Cloud console by simply entering the load balancer(DSR) configuration values. Load balancer(DSR) operates in DSR (direct server return) mode, where server response traffic is sent directly to clients without passing through the load balancer, providing high processing performance.

The load balancer(DSR) creation screen consists of the following three areas.

#### 1. Load Balancer(DSR) Basic Information Settings

Configure basic information for the load balancer(DSR). The required items are as follows:

* Name: Enter the name of the load balancer(DSR).
* Description: Describe the load balancer(DSR).
* VPC: Select the VPC to which the load balancer(DSR) will be connected.
* Subnet: Select the subnet to which the load balancer(DSR) will belong. The load balancer(DSR) and member instances must be located in the same subnet.
* VIP (Virtual IP): The VIP address to assign to the load balancer(DSR). You can choose between **Auto assignment** or **Manual specification** for the assignment method.
  * Auto assignment: Automatically assigns one of the available IPs in the subnet to use as the VIP.
  * Manual specification: Directly enter a desired IP within the subnet's CIDR range to use as the VIP.

!!! danger "[Caution]"
    If the manually specified VIP address does not belong to the subnet's CIDR range, creation will fail. Make sure to specify within the IP range of the relevant subnet.

!!! tip "[Note]"
    Load balancer(DSR) operates at the TCP/UDP L4 level, and server response traffic does not pass through the load balancer. Therefore, unlike regular load balancers, L7 features (HTTP header-based routing, SSL Offloading, listener/member group concepts, etc.) are not provided.

#### 2. Health Check Settings

Configure health checks that periodically verify whether member instances are operating normally.

* Health check protocol: Select the protocol to use for health checks. Choose one of **TCP / ICMP / HTTP**.
* Interval: The period (seconds) for sending health check requests.
* Timeout: The timeout period (seconds) for each health check request. If there is no response within this time, it is considered a failure.
* Max retries: The maximum number of retries before determining an instance as unhealthy. (1-10 times)

Set additional items by protocol as follows:

**TCP**

* Health check port: Specify the port number to attempt TCP connection.

**ICMP**

* No separate port configuration is required. Connectivity is verified with ICMP Echo Request/Reply.

**HTTP**

* Health check port: Specify the port number to send HTTP requests.
* HTTP path (URL): Enter the URL path to perform health checks. The default value is `/`.
* Expected HTTP response code: Enter the HTTP response code to consider as a normal response. The default value is `200`.

!!! danger "[Caution]"
    The interval must be greater than or equal to the timeout. If the timeout is greater than the interval, health checks may not operate normally.

!!! tip "[Note]"
    TCP/HTTP health checks send requests to the DSR VIP as the destination, so if the VIP is not configured on the member server's lo interface, those packets cannot be received and processed, causing health check failures and members to be determined as `INACTIVE`. ICMP health checks send requests to the member's actual IP, so they only verify connectivity regardless of VIP configuration.

#### 3. Member Settings

Specify the member instances to register when creating the load balancer(DSR). Member registration can also be done after creating the load balancer(DSR).

* Instance selection: Select instances (network interfaces) that belong to the same subnet as the load balancer(DSR). You can select multiple instances simultaneously to register as members.

!!! tip "[Note]"
    Load balancer(DSR) forwards client requests to member instances while maintaining the destination port (VIP port) as-is. Therefore, unlike regular load balancers, service ports per member are not specified when registering members, and only the network interface of the member instance is selected. The member server's application must be bound to `0.0.0.0` or the VIP to listen for the same port sent by the client.

!!! danger "[Caution]"
    For member instances to properly receive and respond to traffic coming to the VIP, the following configuration is required inside the server:

    - Add VIP as an additional allowed address to the network interface (Console Network Interface menu)
    - Kernel parameter configuration (`arp_ignore=1`, `arp_announce=2`)
    - Add VIP to lo interface as `/32` subnet
    - Allow service port and health check traffic in Security Groups

    For detailed procedures, see the member server configuration guide in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/ko/overview/).

!!! tip "[Note]"
    The initial state of newly registered members is `INACTIVE`. When they pass health checks, they automatically transition to `ACTIVE` state and receive traffic.

After entering all items, click the **Create Load Balancer** button to create the load balancer(DSR).

<a id='view-dsr-loadbalancers'></a>
### View and Modify Load Balancer(DSR)

#### Load Balancer(DSR) List

After completing load balancer(DSR) creation, you can check the basic information of the created load balancers(DSR) on the list screen. The items displayed on the list screen are as follows:

* Name: The name specified when creating the load balancer(DSR).
* VIP address: The private IP assigned to the load balancer(DSR). You can access this IP from within the VPC.
* Floating IP: The floating IP connected for external access.
* Network: The name of the VPC to which the load balancer(DSR) belongs and the subnet CIDR.
* Member count: The number of member instances registered to the load balancer(DSR).
* Status: The creation/operation status of the load balancer(DSR).

!!! tip "[Note]"
    The status of the load balancer(DSR) is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Operating normally |
    | `BUILD` | Load balancer(DSR) being created |
    | `ERROR` | Error occurred. Please contact the administrator. |

You can create additional load balancers(DSR) with the **+ Create DSR** button at the top, and delete them by selecting load balancers(DSR) with checkboxes in the list and clicking the **Delete** button.

#### Load Balancer(DSR) Detailed Information

When you select a load balancer(DSR) from the list, detailed information is displayed at the bottom of the screen. The detailed screen is divided into three tabs: **Basic Information**, **Members**, and **Health Check**.

In the **Basic Information** tab, you can check the following information:

* Name, description
* Subnet and VIP address
* Floating IP connection information
* Status

#### Change Name
To change the name of the load balancer(DSR), click the **Edit Name** icon in the detailed information, enter the name to change, and click the **Confirm** button.

#### Change Floating IP
You can connect or disconnect a floating IP to allow access to the load balancer(DSR) from external networks.

1. Click the **Change Floating IP** button in the load balancer(DSR) detailed information.
2. Select the floating IP to connect. To disconnect the floating IP, select **Disable**.
3. Click the **Confirm** button to apply the settings.

!!! tip "[Note]"
    Even if you disconnect the floating IP, access through the VIP from within the VPC is not affected.

!!! tip "[Note]"
    The VPC, subnet, and VIP address to which the load balancer(DSR) is connected cannot be changed after creation. If changes are needed, you must delete and recreate the load balancer(DSR).

<a id='delete-dsr-loadbalancers'></a>
### Delete Load Balancer(DSR)
On the load balancer(DSR) list screen, select the load balancer(DSR) to delete, click the **Delete** button, and click the **Confirm** button in the confirmation window to delete the corresponding load balancer(DSR).

!!! danger "[Caution]"
    When you delete a load balancer(DSR), all members registered to that DSR are deleted together. If a floating IP is connected, it is automatically released.

<a id='manage-dsr-members'></a>
## Member Management

Select the desired load balancer(DSR) from the load balancer(DSR) list and click the **Members** tab to display the member instance management screen.

### Member List

In the **Members** tab, you can check the list and status of member instances registered to the load balancer(DSR). The items displayed in the list are as follows:

* IP address: The IP address of the member instance.
* Device model: The resource type that owns the network port registered as a member.
* Device information: The identification information (instance name, port ID, etc.) of the network port registered as a member is displayed in an integrated manner.
* Status: The current status of the member.

!!! tip "[Note]"
    Since load balancer(DSR) forwards to members while maintaining the destination port of client requests as-is, L4 service ports are not separately displayed in member items. The actual service port is the port requested by the client to the VIP, and the member server's application must listen on that port.

!!! tip "[Note]"
    The status of members is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Health check successful, target for traffic distribution |
    | `INACTIVE` | Health check failed or immediately after new registration, excluded from traffic distribution targets |
    | `ONLINE` | Member manually disabled |

<a id='add-dsr-members'></a>
### Add Members
Click the **+ Add Member** button in the **Members** tab to display the add member modal.

1. Select the **instances** to register as members from the list. You can select multiple instances simultaneously.
2. Click the **Confirm** button to register the selected instances as members.

!!! tip "[Note]"
    Unlike regular load balancers, load balancer(DSR) does not enter L4 service ports in the member addition step. Since load balancer(DSR) forwards client requests to members without converting the destination port, per-member port mapping is unnecessary.

!!! danger "[Caution]"
    Note the following constraints when registering members:

    * Member instances must belong to the same subnet as the load balancer(DSR).
    * Only compute instances can be registered as members.
    * The same instance port cannot be registered multiple times to the same load balancer(DSR).
    * By default, up to 30 members can be registered to one load balancer(DSR).

!!! tip "[Note]"
    To properly receive traffic after member registration, you need to add the VIP as an additional allowed address to the network interface, and configure ARP kernel parameters, add VIP to lo interface, and set Security Groups rules inside the member server. For detailed procedures, see the member server configuration guide in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/ko/overview/).

<a id='delete-dsr-members'></a>
### Delete Members
Select the member to delete from the list in the members tab, click the **Delete** button. When the confirmation window appears, click the **Confirm** button to remove the corresponding member from the load balancer(DSR).

!!! tip "[Note]"
    Deleting a member from the load balancer(DSR) does not delete the instance itself. Conversely, if you delete an instance registered as a member, that member is automatically removed from the load balancer(DSR).

<a id='manage-dsr-health-monitor'></a>
## Health Check Management

In the **Health Check** tab of the load balancer(DSR) detailed screen, you can check and change the currently configured health check information.

<a id='view-dsr-health-monitor'></a>
### View Health Check
In the **Health Check** tab, you can check the following information of the currently configured health check:

* Health check protocol: TCP / ICMP / HTTP
* Health check port: Target port for health checks when using TCP or HTTP protocol
* Interval: Health check request period (seconds)
* Timeout: Health check timeout (seconds)
* Max retries: Number of retries until unhealthy determination
* HTTP path (URL) / Expected HTTP response code: Displayed only when using HTTP protocol

<a id='change-dsr-health-monitor'></a>
### Change Health Check Settings
Click the **Change Settings** button in the **Health Check** tab to change health check settings.

* Health check protocol: Choose from TCP / ICMP / HTTP
* Enter the required items for each protocol:
  * TCP: Health check port
  * ICMP: No additional items
  * HTTP: Health check port, HTTP path, expected HTTP response code
* Set interval, timeout, and max retries.

After completing the settings, click the **Confirm** button to apply the changes.

!!! danger "[Caution]"
    The interval must be greater than or equal to the timeout. If the timeout is greater than the interval, health checks may not operate normally.

!!! tip "[Note]"
    Health check requests are sent from a health check dedicated IP automatically assigned to the same subnet as the load balancer(DSR). The member instance's Security Group must allow this traffic for health checks to operate normally. For details, see the Security Groups configuration section in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/ko/overview/).

<a id='dsr-quota'></a>
## Quotas and Limitations

The following quotas and limitations apply when using load balancer(DSR):

| Item | Default Limit | Description |
|--|--|--|
| Number of load balancers(DSR) per project | 10 | Number of load balancers(DSR) that can be created per project |
| Number of members per load balancer(DSR) | 30 | Number of members that can be registered to one load balancer(DSR) |

!!! tip "[Note]"
    If you need to use beyond the default quotas, please contact customer support.