## Network > Load Balancer(DSR) > Console Guide

<a id='manage-dsr-loadbalancers'></a>
## Load Balancer(DSR) Management

<a id='create-dsr-loadbalancers'></a>
### Create Load Balancer(DSR)
You can easily create a DSR-type load balancer by simply entering the Load Balancer(DSR) configuration values in the NHN Cloud console. Load Balancer(DSR) operates with the DSR (direct server return) method, where server response traffic is sent directly to the client without going through the load balancer, providing high processing performance.

The Load Balancer(DSR) creation screen consists of the following three areas:

#### 1. Load Balancer(DSR) Basic Information Settings

Configure basic information for the Load Balancer(DSR). The required items are as follows:

* Name: Enter the name of the Load Balancer(DSR).
* Description: Describe the Load Balancer(DSR).
* VPC: Select the VPC to which the Load Balancer(DSR) will be connected.
* Subnet: Select the subnet where the Load Balancer(DSR) will belong. The Load Balancer(DSR) and member instances must be located in the same subnet.
* VIP (Virtual IP): VIP address to be assigned to the Load Balancer(DSR). You can choose between **Auto assign** or **Direct specification** for the assignment method.
  * Auto assign: Automatically assigns one of the available IPs in the subnet to use as VIP.
  * Direct specification: Directly enter the desired IP within the subnet's CIDR range to use as VIP.

!!! danger "Caution"
    Creation will fail if the directly specified VIP address does not belong to the subnet's CIDR range. Make sure to specify within the IP range of the relevant subnet.

!!! tip "Note"
    Load Balancer(DSR) operates at the TCP/UDP L4 level, and server response traffic does not pass through the load balancer. Therefore, unlike regular load balancers, L7 features (HTTP header-based routing, SSL Offloading, listener/member group concepts, etc.) are not provided.

#### 2. Health Check Settings

Configure health checks that periodically verify whether member instances are operating normally.

* Health check protocol: Select the protocol to use for health checks. Choose one of **TCP / ICMP / HTTP**.
* Delay time: The interval (in seconds) for sending health check requests.
* Maximum response timeout: The timeout period (in seconds) for each health check request. If there is no response within this time, it is considered a failure.
* Maximum retry count: The maximum number of retries before determining an instance as abnormal. (1~10 times)

Configure additional items by protocol as follows:

**TCP**

* Health check port: Specify the port number to attempt TCP connection.

**ICMP**

* No separate port configuration required. Checks connectivity with ICMP Echo Request/Reply.

**HTTP**

* Health check port: Specify the port number to send HTTP requests.
* HTTP path (URL): Enter the URL path to perform health checks. The default value is `/`.
* Expected HTTP response code: Enter the HTTP response code to consider as a normal response. The default value is `200`.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

!!! tip "Note"
    TCP/HTTP health checks request with DSR VIP as the destination, so if the VIP is not configured on the member server's lo interface, those packets cannot be received and processed, causing health check failures and members to be determined as `INACTIVE`. ICMP health checks request to the member's actual IP, so they only check connectivity regardless of VIP configuration.

#### 3. Member Settings

Specify member instances to register when creating the Load Balancer(DSR). Member registration can also be done after Load Balancer(DSR) creation.

* Instance selection: Select instances (network interfaces) that belong to the same subnet as the Load Balancer(DSR). You can select one or more instances simultaneously to register as members.

!!! tip "Note"
    Load Balancer(DSR) forwards client requests to member instances while maintaining the original destination port (VIP port). Therefore, unlike regular load balancers, it does not specify member-specific service ports when registering members, only selecting the member instance's network interface. The member server's application must bind to `0.0.0.0` or VIP and listen on the same port that the client sent.

!!! danger "Caution"
    For member instances to properly receive and respond to traffic coming to the VIP, the following configuration is required inside the server:

    - Add VIP as an additional allowed address to the network interface (Console Network Interface menu)
    - Kernel parameter configuration (`arp_ignore=1`, `arp_announce=2`)
    - Add VIP to lo interface as `/32` subnet
    - Allow service port and health check traffic in Security Groups

    For detailed procedures, refer to the member server configuration guide in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

!!! tip "Note"
    The initial status of newly registered members is `INACTIVE`. Once they pass the health check, they automatically transition to `ACTIVE` status and receive traffic.

After entering all items, click the **Create Load Balancer** button to create the Load Balancer(DSR).

<a id='view-dsr-loadbalancers'></a>
### View and Modify Load Balancer(DSR)

#### Load Balancer(DSR) List

Once Load Balancer(DSR) creation is complete, you can check the basic information of the created Load Balancer(DSR)s in the list screen. The items displayed in the list screen are as follows:

* Name: The name specified when creating the Load Balancer(DSR).
* VIP address: The private IP assigned to the Load Balancer(DSR). It can be accessed with this IP from within the VPC.
* Floating IP: The floating IP connected for external access.
* Network: The name of the VPC and subnet CIDR where the Load Balancer(DSR) belongs.
* Member count: The number of member instances registered to the Load Balancer(DSR).
* Status: The creation/operation status of the Load Balancer(DSR).

!!! tip "Note"
    The status of Load Balancer(DSR) is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Operating normally |
    | `BUILD` | Creating Load Balancer(DSR) |
    | `ERROR` | Error occurred. Please contact administrator. |

You can create additional Load Balancer(DSR)s with the **+ Create DSR** button at the top, and delete them by selecting Load Balancer(DSR)s with checkboxes in the list and clicking the **Delete** button.

#### Load Balancer(DSR) Detailed Information

When you select a Load Balancer(DSR) from the list, detailed information is displayed at the bottom of the screen. The detail screen is divided into three tabs: **Basic Information**, **Members**, and **Health Check**.

In the **Basic Information** tab, you can check the following information:

* Name, description
* Subnet and VIP address
* Floating IP connection information
* Status

#### Change Name
To change the name of the Load Balancer(DSR), click the **Edit Name** icon in the detailed information, enter the new name, and click the **Confirm** button.

#### Change Floating IP
You can connect or disconnect a floating IP to allow access to the Load Balancer(DSR) from external networks.

1. Click the **Change Floating IP** button in the Load Balancer(DSR) detailed information.
2. Select the floating IP to connect. To disconnect the floating IP, select **Not used**.
3. Click the **Confirm** button to apply the settings.

!!! tip "Note"
    Even if you disconnect the floating IP, access through VIP from within the VPC is not affected.

!!! tip "Note"
    The VPC, subnet, and VIP address that the Load Balancer(DSR) is connected to cannot be changed after creation. If changes are needed, you must delete the Load Balancer(DSR) and recreate it.

<a id='delete-dsr-loadbalancers'></a>
### Delete Load Balancer(DSR)
Select the Load Balancer(DSR) you want to delete from the Load Balancer(DSR) list screen, click the **Delete** button, and click the **Confirm** button in the confirmation window to delete the relevant Load Balancer(DSR).

!!! danger "Caution"
    When you delete a Load Balancer(DSR), all members registered to that DSR are deleted together. If a floating IP is connected, it is automatically released.

<a id='manage-dsr-members'></a>
## Member Management

Select the desired Load Balancer(DSR) from the Load Balancer(DSR) list and click the **Members** tab to display the member instance management screen.

### Member List

In the **Members** tab, you can check the list and status of member instances registered to the Load Balancer(DSR). The items displayed in the list are as follows:

* IP address: The IP address of the member instance.
* Device model: The resource type that owns the network port registered as a member.
* Device information: The identification information (instance name, port ID, etc.) of the network port registered as a member is displayed in an integrated manner.
* Status: The current status of the member.

!!! tip "Note"
    Since Load Balancer(DSR) forwards to members while maintaining the destination port of client requests, the L4 service port is not displayed separately in member items. The actual service port is the port that the client requested to the VIP, and the member server's application must listen on that port.

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

1. Select **instances** from the list to register as members. You can select one or more instances simultaneously.
2. Click the **Confirm** button to register the selected instances as members.

!!! tip "Note"
    Unlike regular load balancers, Load Balancer(DSR) does not enter L4 service ports in the member addition step. Since Load Balancer(DSR) forwards the destination port of client requests to members without conversion, member-specific port mapping is unnecessary.

!!! danger "Caution"
    Note the following constraints when registering members:

    * Member instances must belong to the same subnet as the Load Balancer(DSR).
    * Only compute instances can be registered as members.
    * The same instance port cannot be registered multiple times to the same Load Balancer(DSR).
    * By default, up to 30 members can be registered to one Load Balancer(DSR).

!!! tip "Note"
    To normally receive traffic after member registration, you need to add VIP as an additional allowed address to the network interface and configure ARP kernel parameters, add VIP to lo interface, and set Security Groups rules inside the member server. For detailed procedures, refer to the member server configuration guide in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='delete-dsr-members'></a>
### Delete Members
Select the members to delete from the list in the Members tab, then click the **Delete** button. When the confirmation window appears, click the **Confirm** button to remove the relevant members from the Load Balancer(DSR).

!!! tip "Note"
    Deleting members from Load Balancer(DSR) does not delete the instances themselves. Conversely, if you delete an instance that is registered as a member, that member is automatically removed from the Load Balancer(DSR).

<a id='manage-dsr-health-monitor'></a>
## Health Check Management

In the **Health Check** tab of the Load Balancer(DSR) detail screen, you can check and change the currently configured health check information.

<a id='view-dsr-health-monitor'></a>
### View Health Check
In the **Health Check** tab, you can check the following information about the currently configured health check:

* Health check protocol: TCP / ICMP / HTTP
* Health check port: Target port for health check when using TCP or HTTP protocol
* Delay time: Health check request interval (seconds)
* Maximum response timeout: Health check timeout (seconds)
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
* Configure delay time, maximum response timeout, and maximum retry count.

After completing the configuration, click the **Confirm** button to apply the changes.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

!!! tip "Note"
    Health check requests are sent from a health check-dedicated IP automatically assigned in the same subnet as the Load Balancer(DSR). The member instance's Security Group must allow this traffic for health checks to operate normally. For details, refer to the Security Groups configuration section in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='dsr-quota'></a>
## Quotas and Limitations

The following quotas and limitations apply when using Load Balancer(DSR):

| Item | Default Limit | Description |
|--|--|--|
| Number of Load Balancer(DSR)s per project | 10 | Number of Load Balancer(DSR)s that can be created per project |
| Number of members per Load Balancer(DSR) | 30 | Number of members that can be registered to one Load Balancer(DSR) |

!!! tip "Note"
    If you need to use beyond the default quotas, please contact customer support.