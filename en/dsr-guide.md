## Network > Load Balancer(DSR) > Console Guide

<a id='manage-dsr-loadbalancers'></a>
## Load Balancer (DSR) Management

<a id='create-dsr-loadbalancers'></a>
### Create Load Balancer (DSR)
You can easily create a DSR-type load balancer in the NHN Cloud console by simply entering the load balancer (DSR) configuration values. Load Balancer (DSR) operates using the DSR (direct server return) method, providing high processing performance as server response traffic is sent directly to the client without passing through the load balancer.

The Load Balancer (DSR) creation screen consists of the following three areas.

#### 1. Load Balancer (DSR) Basic Information Settings

Configure the basic information for the Load Balancer (DSR). The required items are as follows:

* Name: Enter the name of the Load Balancer (DSR).
* Description: Describe the Load Balancer (DSR).
* VPC: Select the VPC to which the Load Balancer (DSR) will be connected.
* Subnet: Select the subnet where the Load Balancer (DSR) will be located. The Load Balancer (DSR) and member instances must be located in the same subnet.
* VIP (Virtual IP): This is the VIP address to be assigned to the Load Balancer (DSR). You can choose between **Auto Assignment** or **Direct Assignment** for the assignment method.
  * Auto Assignment: Automatically assigns one of the available IPs in the subnet to use as VIP.
  * Direct Assignment: Directly enter the desired IP within the subnet's CIDR range to use as VIP.

!!! danger "Caution"
    If the directly assigned VIP address does not belong to the subnet's CIDR range, creation will fail. Make sure to specify it within the IP range of the corresponding subnet.

!!! tip "Note"
    Load Balancer (DSR) operates at the TCP/UDP L4 level, and server response traffic does not go through the load balancer. Therefore, unlike general load balancers, L7 features (HTTP header-based routing, SSL Offloading, listener/member group concepts, etc.) are not provided.

#### 2. Health Check Settings

Configure health checks to periodically verify that member instances are operating normally.

* Health check protocol: Select the protocol to use for health checks. Choose one of **TCP / ICMP / HTTP**.
* Delay time: The cycle (in seconds) for sending health check requests.
* Maximum response wait time (timeout): The timeout period (in seconds) for each health check request. If there is no response within this time, it is considered a failure.
* Maximum retry count: The maximum number of retries until an instance is judged as abnormal. (1-10 times)

Set the following additional items for each protocol.

**TCP**

* Health check port: Specify the port number to attempt TCP connection.

**ICMP**

* No separate port configuration is required. Connectivity is verified through ICMP Echo Request/Reply.

**HTTP**

* Health check port: Specify the port number to send HTTP requests.
* HTTP path (URL): Enter the URL path to perform health checks. The default value is `/`.
* Expected HTTP response code: Enter the HTTP response code to be considered a normal response. The default value is `200`.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

!!! tip "Note"
    TCP/HTTP health checks request to the DSR VIP as the destination, so if the VIP is not configured on the lo interface of the member server, those packets cannot be received and processed, causing health checks to fail and the member to be judged as `INACTIVE`. ICMP health checks request to the member's actual IP, so they only verify connectivity regardless of VIP configuration.

#### 3. Member Settings

Specify the member instances to register when creating the Load Balancer (DSR). Member registration can also be done after creating the Load Balancer (DSR).

* Instance selection: Select instances (network interfaces) that belong to the same subnet as the Load Balancer (DSR). You can select one or more instances simultaneously to register as members.

!!! tip "Note"
    Load Balancer (DSR) forwards client requests to member instances while maintaining the destination port (VIP port) as is. Therefore, unlike general load balancers, service ports for each member are not specified during member registration, and only the network interface of the member instance is selected. The application on the member server must bind to `0.0.0.0` or the VIP to listen for the same port sent by the client.

!!! danger "Caution"
    For member instances to normally receive and respond to traffic coming to the VIP, the following configuration is required inside the server:

    - Add VIP as an additional allowed address to the network interface (Console Network Interface menu)
    - Kernel parameter settings (`arp_ignore=1`, `arp_announce=2`)
    - Add VIP to the lo interface with `/32` subnet
    - Allow service port and health check traffic in Security Groups

    For detailed procedures, refer to the member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

!!! tip "Note"
    The initial status of newly registered members is `INACTIVE`. Once they pass health checks, they automatically transition to `ACTIVE` status and start receiving traffic.

After entering all items, click the **Create Load Balancer** button to create the Load Balancer (DSR).

<a id='view-dsr-loadbalancers'></a>
### View and Modify Load Balancer (DSR)

#### Load Balancer (DSR) List

Once Load Balancer (DSR) creation is complete, you can check the basic information of the created Load Balancers (DSR) on the list screen. The items displayed on the list screen are as follows:

* Name: The name specified when creating the Load Balancer (DSR).
* VIP address: The private IP assigned to the Load Balancer (DSR). You can access it through this IP within the VPC.
* Floating IP: The floating IP connected for external access.
* Network: The name of the VPC and subnet CIDR where the Load Balancer (DSR) belongs.
* Member count: The number of member instances registered to the Load Balancer (DSR).
* Status: The creation/operation status of the Load Balancer (DSR).

!!! tip "Note"
    The status of the Load Balancer (DSR) is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Operating normally |
    | `BUILD` | Load Balancer (DSR) is being created |
    | `ERROR` | Error occurred. Contact administrator. |

You can create additional Load Balancers (DSR) using the **+ Create DSR** button at the top, and delete them by selecting Load Balancers (DSR) with checkboxes from the list and clicking the **Delete** button.

#### Load Balancer (DSR) Detailed Information

When you select a Load Balancer (DSR) from the list, detailed information is displayed at the bottom of the screen. The detail screen is divided into three tabs: **Basic Information**, **Members**, and **Health Check**.

In the **Basic Information** tab, you can check the following information:

* Name, Description
* Subnet and VIP address
* Floating IP connection information
* Status

#### Change Name
To change the name of the Load Balancer (DSR), click the **Edit Name** icon in the detailed information, enter the name to change, and click the **OK** button.

#### Change Floating IP
You can connect or disconnect a floating IP to allow access to the Load Balancer (DSR) from external networks.

1. Click the **Change Floating IP** button in the Load Balancer (DSR) detailed information.
2. Select the floating IP to connect. To disconnect the floating IP, select **Disable**.
3. Click the **OK** button to apply the settings.

!!! tip "Note"
    Even if you disconnect the floating IP, access through VIP from within the VPC is not affected.

!!! tip "Note"
    The VPC, subnet, and VIP address connected to the Load Balancer (DSR) cannot be changed after creation. If changes are needed, you must delete the Load Balancer (DSR) and recreate it.

<a id='delete-dsr-loadbalancers'></a>
### Delete Load Balancer (DSR)
Select the Load Balancer (DSR) to delete from the Load Balancer (DSR) list screen, click the **Delete** button, and click the **OK** button in the confirmation window to delete the corresponding Load Balancer (DSR).

!!! danger "Caution"
    When you delete a Load Balancer (DSR), all members registered to that DSR are deleted together. If a floating IP is connected, it is automatically released.

<a id='manage-dsr-members'></a>
## Member Management

Select the desired Load Balancer (DSR) from the Load Balancer (DSR) list and click the **Members** tab to display the member instance management screen.

### Member List

In the **Members** tab, you can check the list and status of member instances registered to the Load Balancer (DSR). The items displayed in the list are as follows:

* IP address: The IP address of the member instance.
* Device model: The type of resource that owns the network port registered as a member.
* Device information: The identification information of the network port registered as a member (instance name, port ID, etc.) is displayed in an integrated manner.
* Status: The current status of the member.

!!! tip "Note"
    Since Load Balancer (DSR) forwards client requests to members while maintaining the destination port as is, L4 service ports are not separately displayed in member items. The actual service port is the port requested by the client to the VIP, and the application on the member server must listen to that port.

!!! tip "Note"
    The status of members is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Health check successful, target for traffic distribution |
    | `INACTIVE` | Health check failed or immediately after new registration, excluded from traffic distribution |
    | `ONLINE` | Member manually disabled |

<a id='add-dsr-members'></a>
### Add Members
Click the **+ Add Member** button in the **Members** tab to open the member addition modal.

1. Select **instances** to register as members from the list. You can select one or more instances simultaneously.
2. Click the **OK** button to register the selected instances as members.

!!! tip "Note"
    Unlike general load balancers, Load Balancer (DSR) does not enter L4 service ports during the member addition step. Since Load Balancer (DSR) forwards client requests to members without converting the destination port, member-specific port mapping is unnecessary.

!!! danger "Caution"
    Please note the following constraints when registering members:

    * Member instances must belong to the same subnet as the Load Balancer (DSR).
    * Only compute instances can be registered as members.
    * The same instance port cannot be registered multiple times to the same Load Balancer (DSR).
    * A maximum of 30 members can be registered to one Load Balancer (DSR) by default.

!!! tip "Note"
    To normally receive traffic after member registration, you need to add VIP as an additional allowed address to the network interface, and configure ARP kernel parameters, add VIP to the lo interface, and set Security Groups rules inside the member server. For detailed procedures, refer to the member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='delete-dsr-members'></a>
### Delete Members
Select the member to delete from the list in the Members tab, click the **Delete** button. When the confirmation window appears, click the **OK** button to remove the corresponding member from the Load Balancer (DSR).

!!! tip "Note"
    Deleting a member from the Load Balancer (DSR) does not delete the instance itself. Conversely, if you delete an instance registered as a member, that member is automatically removed from the Load Balancer (DSR).

<a id='manage-dsr-health-monitor'></a>
## Health Check Management

You can check and change the currently configured health check information in the **Health Check** tab of the Load Balancer (DSR) detail screen.

<a id='view-dsr-health-monitor'></a>
### View Health Check
In the **Health Check** tab, you can check the following information about the currently configured health check:

* Health check protocol: TCP / ICMP / HTTP
* Health check port: Health check target port when using TCP or HTTP protocol
* Delay time: Health check request cycle (seconds)
* Maximum response wait time: Health check timeout (seconds)
* Maximum retry count: Number of retries until abnormal determination
* HTTP path (URL) / Expected HTTP response code: Displayed only when using HTTP protocol

<a id='change-dsr-health-monitor'></a>
### Change Health Check Settings
Click the **Change Settings** button in the **Health Check** tab to change health check settings.

* Health check protocol: Choose from TCP / ICMP / HTTP
* Enter required items for each protocol.
  * TCP: Health check port
  * ICMP: No additional items
  * HTTP: Health check port, HTTP path, expected HTTP response code
* Set delay time, maximum response wait time, and maximum retry count.

After completing the settings, click the **OK** button to apply the changes.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not operate normally.

!!! tip "Note"
    Health check requests are sent from a dedicated health check IP automatically assigned in the same subnet as the Load Balancer (DSR). The Security Group of member instances must allow such traffic for health checks to operate normally. For details, refer to the Security Groups configuration section in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='dsr-quota'></a>
## Quotas and Limitations

The following quotas and limitations apply when using Load Balancer (DSR).

| Item | Default Limit | Description |
|--|--|--|
| Number of Load Balancers (DSR) per project | 10 | Number of Load Balancers (DSR) that can be created per project |
| Number of members per Load Balancer (DSR) | 30 | Number of members that can be registered to one Load Balancer (DSR) |

!!! tip "Note"
    If you need to use more than the default quota, contact customer support.