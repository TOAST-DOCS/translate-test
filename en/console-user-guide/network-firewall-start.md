<!-- pre-align:aligned sig=f37ed2d1fbde -->

<a id="getting-started-with-network-firewall"></a>
## Getting started with Network Firewall { #getting-started-with-network-firewall }

**Security > Network Firewall > Console User Guide > Getting Started with Network Firewall**

<br>

<a id="prepare-before-creating-network-firewall"></a>
## Prepare Before Creating Network Firewall { #prepare-before-creating-network-firewall }

The minimum network service resources required to create Network Firewall are as follows:

<a id="requirements-for-a-single-project-configuration"></a>
### Requirements for a single project configuration { #requirements-for-a-single-project-configuration }

* 1 Project
* 2 VPCs (Hub VPC, Spoke VPC)
* 3 subnets within the Hub VPC
    * Traffic (internal) subnet, NAT (external) subnet, external transit subnet
* At least one subnet in the Spoke VPC
* Internet gateway connected to the Routing of the Hub VPC

<a id="requirements-for-configuring-2-spoke-vpcs-within-a-single-project"></a>
### Requirements for configuring 2 Spoke VPCs within a single project { #requirements-for-configuring-2-spoke-vpcs-within-a-single-project }

* 1 Project
* 3 VPCs (Hub VPC, Spoke1 VPC, Spoke2 VPC)
* 3 subnets within the Hub VPC
    * Traffic (internal) subnet, NAT (external) subnet, external transit subnet
* At least one subnet each in the Spoke1 VPC and Spoke2 VPC
* Internet gateway connected to the Routing of the Hub VPC

<a id="preparations-for-configuring-more-than-one-project"></a>
### Preparations for configuring more than one project { #preparations-for-configuring-more-than-one-project }

* 2 projects
* 2 VPCs (Hub VPC and Spoke VPC for each project)
* 3 subnets within the Hub VPC
    * Traffic (internal) subnet, NAT (external) subnet, external transit subnet
* At least one subnet in the Spoke VPC
* Internet gateway connected to the Routing of the Hub VPC

<a id="preparations-for-configuring-cross-region-projects"></a>
### Preparations for configuring cross-region projects { #preparations-for-configuring-cross-region-projects }

* 1 Project
* 2 VPCs (Hub VPC in KR1 region and Spoke VPC in KR2 region)
* 3 subnets within the Hub VPC
    * Traffic (internal) subnet, NAT (external) subnet, external transit subnet
* At least one subnet in the Spoke VPC
* Internet gateway connected to the Routing of the Hub VPC

<a id="preparations-for-configuring-multiple-subnets-within-a-single-vpc"></a>
### Preparations for configuring multiple subnets within a single VPC { #preparations-for-configuring-multiple-subnets-within-a-single-vpc }

* 1 Project
* 1 VPC
* 3 Hub subnets
    * Traffic (internal) subnet, NAT (external) subnet, external transit subnet
* At least 1 Spoke subnet that does not overlap with the Hub subnets
* Routing table to be connected to the Spoke subnet
* Internet gateway connected to Routing in the VPC

!!! tip "Notice"

    * See the service architecture in **Network Firewall > Overview**.
    * The service resources listed above can be created in the [Network] category.
    * Only 1 Network Firewall can be created per project.

<br>

<a id="create-network-firewall"></a>
## Create Network Firewall { #create-network-firewall }

1. Go to **Security > Network Firewall**.
2. Select all required items and click **Create Network Firewall** button at the bottom.
    * RBAC: Grant API permissions to query instance objects and provide the Network Firewall service
    * Configuration type: Select a single configuration and configure redundancy.
    * VPC: VPC that Network Firewall will use
    * Subnet: Subnet that Network Firewall uses to control internal traffic
    * NAT: Subnet that Network Firewall uses to control external traffic
    * External transmission: Subnet that sends traffic and logs created by Network Firewall
    <img src="../../../static/images/24.09.12/create.png" height="60%" />

!!! tip "Note"

    * The created Network Firewall is not exposed to the user's project.
    * The subnets used for the subnet, NAT, and external transmission must all be different subnets.
    * It is recommended to create using the minimum unit (28-bit) available in the NHN Cloud console whenever possible.
    * An internet gateway must be connected to the routing table of the VPC to which Network Firewall belongs in order to create it.
    * The CIDR range owned by Network Firewall and the CIDR range that requires connectivity must not overlap.
    * If changes are needed after creating Network Firewall with a single or redundant configuration, the configuration can be changed in the **Options** tab. However, since the availability zone cannot be changed, it is recommended to configure redundant configurations with separate availability zones whenever possible. 

!!! danger "Caution"

    * Network Firewall is a separate service from Security Groups. When using Network Firewall, both services must allow access in order to reach the instance.
    * IPs created with the Virtual_IP type in **Network > Network Interface** are being used for redundancy in Network Firewall. Deleting them may block communication.

<br>

<a id="configure-connection"></a>
## Configure Connection { #configure-connection }

> [Example]
When the VPC (Hub) used by Network Firewall is 10.0.0.0/24, and the VPC (Spoke) that needs to connect to the Network Firewall is 172.16.0.0/24.

1. Go to **Network > Peering Gateway** to create a peering.
    * For more information on connecting a peering gateway, please see the [](https://docs.nhncloud.com/ko/Network/Peering%20Gateway/ko/console-guide/)user guide[](https://docs.nhncloud.com/ko/Network/Peering%20Gateway/ko/console-guide/).
    <img src="../../../static/images/23.12.19/ConnectionSettings3.png" height="65%" />
 <img src="../../../static/images/23.12.19/ConnectionSettings4.png" height="65%" />
   
!!! tip "Note"
    \* Create the appropriate peering based on the location of the Spoke VPC.
    \* If the Spoke VPC is in the same project, create a peering.
    \* If the Spoke VPC is in a different project, create a project peering.
    \* If the Spoke VPC is in a different region, create a region peering.

<br>

2. Go to **Network > Routing**, select a Hub VPC, and set up the routing as follows.
    * Destination CIDR: 172.16.0.0/24
    * Gateway: Gateway of peering type added after peering connection
    <img src="../../../static/images/23.12.19/ConnectionSettings5.png" height="65%" />

<br>

3. Go to **Network > Routing**, select a Spoke VPC, and set up the routing as follows:
    * Destination CIDR: 0.0.0.0/0
    * Gateway: Gateway of peering type added after peering connection
    <img src="../../../static/images/23.12.19/ConnectionSettings6.png" height="65%" />

!!! tip "Note"

    * Configuring routing as described above causes all communication from the Spoke VPC to pass through Network Firewall.
    * If communication needs to be branched, specify the destination explicitly instead of using 0.0.0.0/0.

<br>

4. Go to **Network > Peering Gateway > Project Peering**.
    * Select the created peering and go to the **Route** tab.
    * Click the **Peer** or **Change Local Route** to set up routing as follows:
        * Destination CIDR: 0.0.0.0/0
        * Gateway: NetworkFirewall_INF_TRAFFIC_VIP
        <img src="../../../static/images/23.12.19/ConnectionSettings7.png" height="65%" />
  <img src="../../../static/images/23.12.19/ConnectionSettings8.png" height="50%" />
      
Once the above routing settings are complete, instances in the Spoke VPC will be able to communicate publicly through the Network Firewall. (Requires adding destination NAT in **Network Firewall > NAT**)

<br>

**If the Spoke VPC has two or more subnets and traffic control between subnets is required via Network Firewall**, add the following routing:

> [Example]
When the subnet of the Spoke VPC (172.16.0.0/24) is 172.16.0.0/25 and 172.16.0.128/25

* Go to **Network > Routing**, and select Spoke VPC and add the two routings as follows.
    * Destination CIDR: 172.16.0.0/25 and 172.16.0.128/25
    * Gateway: Gateway of peering type added after peering connection
    <img src="../../../static/images/23.12.19/ConnectionSettings9.png" height="65%" />
  <img src="../../../static/images/23.12.19/ConnectionSettings10.png" height="65%" />
  
Once the above routing settings are complete, private communication between subnets within the Spoke VPC can be made through the Network Firewall. (Requires adding a policy in **Network Firewall > Policy** tab)

<br>

**If there are two or more spoke VPCs**, add the routing as follows.

> [Example]
When it is Spoke VPC1 (17.2.16.0.0/24) and Spoke VPC2 (192.168.0.0/24)

* Go to **Network > Routing** to select a Hub VPC, and add the two routings as follows:
    * Spoke VPC 1
        * Destination CIDR: 172.16.0.0/24
        * Gateway: Gateway of peering type added between Hub VPC and Spoke VPC1
    * Spoke VPC 2
        * Destination CIDR: 192.168.0.0/24
        * Gateway: Gateway of peering type added between Hub VPC and Spoke VPC2
        <img src="../../../static/images/23.12.19/ConnectionSettings11.png" height="65%" />

!!! tip "Note"

    VPC peering between Spoke VPC2-Hub also requires the Add Route setting, as shown in **4****in Connection Settings**.

<br>

**If you configure a Spoke subnet in the same VPC,** create a new routing table to associate subnets and add routes. 
* In **Network > Routing**, create a routing table and add a route.
<img src="../../../static/images/24.11.07/routetable_create.png" height="65%" />
<img src="../../../static/images/24.11.07/route_create.png" height="65%" />

<br>

* In **Network > Subnet**, create a new spoke subnet that does not overlap the Network Firewall and associate a routing table with it.
<img src="../../../static/images/24.11.07/subnet_create.png" height="65%" />
<img src="../../../static/images/24.11.07/routetable_connect.png" height="65%" />

<br>

Once the above routing settings are complete, private communication between different Spoke VPCs can be made through the Network Firewall. (Requires adding a policy in **Network Firewall > Policy** tab)