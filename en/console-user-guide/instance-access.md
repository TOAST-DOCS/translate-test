<!-- pre-align:aligned sig=1e5a2402cc4a -->

<a id="instance-access"></a>
## Instance Access { #instance-access }

**Security > Network Firewall > Console User Guide > Instance Access**

After creating Network Firewall and completing all connection settings, you access your instance through the Network Firewall.

<br>

<a id="configure"></a>
## Configure { #configure }

For example, if you configure 3 subnets with 2 Spoke VPCs in 1 project and need web firewall access from outside, set up NAT and ACLs as shown below.

![](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/2.instance-access/instance-access1.png){ height="65%" }

* Go to **Network Firewall > NAT > Destination** tab
* Click **Add** and configure the destination NAT settings
  * Create a Destination IP object on the **Objects** tab before setup and need a spare floating IP
![](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/2.instance-access/instance-access2.png){ height="65%" }

* Allow the required ACLs on the **Network Firewall > Policy > ACLs** tab
  * Source/destination interfaces can be set to ALL    
    ![](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/2.instance-access/instance-access3.png){ height="65%" }  

!!! danger "Caution"
    
    You can access the instance only when the source IP is allowed in the security group.