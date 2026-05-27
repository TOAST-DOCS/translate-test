## Network > Load Balancer(DSR) > Console Guide

<a id='manage-dsr-loadbalancers'></a>



## Member Management

Select the desired load balancer (DSR) from the load balancer (DSR) list and click the **Members** tab to display the member instance management screen.

### Member List

In the **Members** tab, you can view the list and status of member instances registered to the load balancer (DSR). The items displayed in the list are as follows:

* IP Address: The IP address of the member instance.
* Device Model: The resource type that owns the network port registered as a member.
* Device Information: The identification information (instance name, port ID, etc.) of the network port registered as a member is displayed in an integrated manner.
* Status: The current status of the member.

!!! tip "Note"
    Since the load balancer (DSR) forwards client requests to members while maintaining the original destination port, the L4 service port is not separately displayed in the member items. The actual service port is the port requested by the client to the VIP, and the member server's application must listen on that port.

!!! tip "Note"
    The member status is determined as one of the following:

    | Status | Meaning |
    |--|--|
    | `ACTIVE` | Health check successful, target for traffic distribution |
    | `INACTIVE` | Health check failed or immediately after new registration, excluded from traffic distribution targets |
    | `ONLINE` | Member is manually deactivated |

<a id='add-dsr-members'></a>
### Add Members
Click the **+ Add Member** button in the **Members** tab to display the add member modal.

1. Select the **instance** to register as a member from the list. You can select multiple instances simultaneously.
2. Click the **Confirm** button to register the selected instances as members.

!!! tip "Note"
    Unlike regular load balancers, load balancer (DSR) does not require entering the L4 service port during the member addition step. Since the load balancer (DSR) forwards client requests to members without converting the destination port, port mapping per member is unnecessary.

!!! danger "Caution"
    Be aware of the following constraints when registering members:

    * Member instances must belong to the same subnet as the load balancer (DSR).
    * Only compute instances can be registered as members.
    * The same instance port cannot be registered multiple times in the same load balancer (DSR).
    * A single load balancer (DSR) can register up to 30 members by default.

!!! tip "Note"
    To properly receive traffic after member registration, you need to add the VIP as an additional allowed address to the network interface, configure ARP kernel parameters within the member server, add the VIP to the lo interface, and configure Security Groups rules. For detailed procedures, refer to the member server configuration guide in [Load Balancer (DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='delete-dsr-members'></a>
### Delete Members
Select the member to delete from the list in the Members tab and click the **Delete** button. When the confirmation window appears, click the **Confirm** button to remove the member from the load balancer (DSR).

!!! tip "Note"
    Deleting a member from the load balancer (DSR) does not delete the instance itself. Conversely, if you delete an instance that is registered as a member, that member is automatically removed from the load balancer (DSR).

<a id='manage-dsr-health-monitor'></a>

## Health Check Management

You can view and modify the currently configured health check information in the **Health Check** tab of the Load Balancer(DSR) details screen.

<a id='view-dsr-health-monitor'></a>
### View Health Check
In the **Health Check** tab, you can view the following information about the currently configured health check:

* Health check protocol: TCP / ICMP / HTTP
* Health check port: Target port for health checks when using TCP or HTTP protocol
* Delay time: Health check request interval (seconds)
* Maximum response wait time: Health check timeout (seconds)
* Maximum retry count: Number of retries until unhealthy determination
* HTTP path (URL) / Expected HTTP response code: Displayed only when using HTTP protocol

<a id='change-dsr-health-monitor'></a>
### Change Health Check Settings
You can modify health check settings by clicking the **Change Settings** button in the **Health Check** tab.

* Health check protocol: Select from TCP / ICMP / HTTP
* Enter required items for each protocol:
  * TCP: Health check port
  * ICMP: No additional items
  * HTTP: Health check port, HTTP path, expected HTTP response code
* Configure delay time, maximum response wait time, and maximum retry count.

After completing the configuration, click the **OK** button to apply the changes.

!!! danger "Caution"
    The delay time must be greater than or equal to the timeout. If the timeout is greater than the delay time, health checks may not function properly.

!!! tip "Note"
    Health check requests are sent from a dedicated health check IP automatically assigned to the same subnet as the Load Balancer(DSR). You must allow this traffic in the Security Group of member instances for health checks to function properly. For more details, refer to the Security Groups configuration section in [Load Balancer(DSR) Overview](/Network/Load%20Balancer(DSR)/en/overview/).

<a id='dsr-quota'></a>

## Quotas and Limitations

The following quotas and limitations apply when using Load Balancer (DSR).

| Item | Default Limit | Description |
|--|--|--|
| Number of Load Balancers (DSR) per project | 10 | Number of Load Balancers (DSR) that can be created per project |
| Number of members per Load Balancer (DSR) | 30 | Number of members that can be registered to one Load Balancer (DSR) |

!!! tip "Note"
    If you need to use beyond the default quotas, please contact customer support.
