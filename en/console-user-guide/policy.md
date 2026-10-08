<!-- pre-align:aligned sig=9132502e0f26 -->

<a id="policy"></a>
## Policy { #policy }

**Security > Network Firewall > Console User Guide > Policy**

In the **Policy** tab, you can use the **ACL** feature to control traffic between VPCs connected to Network Firewall and inbound/outbound traffic, and the **Route** feature to specify the path for communication passing through Network Firewall.

<br>

<a id="configure-acl"></a>
## Configure ACL { #configure-acl }

<a id="add"></a>
### Add { #add }

* Add policies based on departure, destination, and destination port.
    * Select the departure, destination, and destination port through already created objects.
* Policies can be added by configuring options such as the policy status (enabled/disabled), action (allow/block), schedule, and whether to log per policy.
* The schedule feature operates after the policy status is enabled. (The schedule feature does not apply if the policy is disabled.)

![policy2.PNG](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/3.policy/policy2.png)

<a id="copy"></a>
### Copy { #copy }

* Click **Copy** to copy a policy.
    * Copy: Copies the same policy as the one you want to copy.
    * Reverse copy: Copies the policy with the source and destination of the policy being copied swapped.
![policy3.PNG](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/3.policy/policy3.png)
    
<a id="modify"></a>
### Modify { #modify }

* Click **modify** to modify a policy.

<a id="move"></a>
### Move { #move }

* Click **Move** to move a policy.
    * Could not move below the default-deny policy.
![policy4.PNG](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/3.policy/policy4.png)

<a id="delete"></a>
### Delete { #delete }

* Click **Delete** to delete a policy.

<a id="batch-download-of-policies"></a>
### Batch Download of Policies { #batch-download-of-policies }

* Download all policies created in the Policy tab at once.

<a id="batch-register-policies"></a>
### Batch Register Policies { #batch-register-policies }

* You can register policies at once using the downloaded template.

![policy5.PNG](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/3.policy/policy5.png)

!!! tip "Note"

    Copied policies are disabled. If needed, click **Modify** to enable the policy before use.


Deleted policies cannot be recovered, and the default-deny policy cannot be deleted.

<br>

<a id="configure-routing"></a>
## Configure Routing { #configure-routing }

<a id="configure-routing-add"></a>
### Add { #configure-routing-add }

* Click **Add** to select Ethernet, and enter the destination and gateway. 
    * Destination: Enter in subnet format
    * Ethernet: Select an Ethernet from the dropdown list.
    * Gateway: Enter in host format
  
<a id="configure-routing-modify"></a>
### Modify { #configure-routing-modify }

* Click **Modify** to modify a route.

<a id="configure-routing-delete"></a>
### Delete { #configure-routing-delete }

* Click **Delete** to delete a route.

!!! tip "Note"

    * If Ethernet is set to VPN, a gateway does not need to be specified.
    * For route settings for private IP ranges integrated with IPSec VPN, make sure to set Ethernet to VPN.
    * When entering a destination subnet, if the following validation message appears, check the subnet range in advance and enter the starting IP of the subnet.
        * [Examples]
            * 192.168.199.0/21 (X) → 192.168.192.0/21 (O)
            * 172.16.100.0/20 (X) → 172.16.96.0/20 (O)
            * 10.10.10.130/25 (X) → 10.10.10.128/25 (O)
            ![route_add.PNG](../../static/images/24.09.12/route_add.png)

!!! danger "Caution"

    * The default gateway of Network Firewall is the NAT Ethernet, and it cannot be modified or deleted.
    * If route settings are changed, communication issues may occur, so configure with caution. 