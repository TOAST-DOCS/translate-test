<!-- machine_translated: true -->

<!-- pre-align:aligned sig=ecfaf0722a63 -->

<a id="network-peering-gateway-console-user-guide"></a>
## Network > Peering Gateway > Console User Guide { #network-peering-gateway-console-user-guide }

This guide explains how to use the Peering Gateway service in the Console.

<a id="peering"></a>
## Peering { #peering }

**Peering** is a feature to connect two different **VPCs**. Normally, VPCs cannot communicate with each other because they are in different network zones. You can connect them using a **floating IP**, but it incurs extra charges depending on your network usage. However, the peering feature allows you to connect two **VPCs** at no additional cost.

* Peering connects two different VPCs. Connecting to another VPC across a VPC is not supported. For example, in the `A <-> B <-> C` connection, `A` and `C` cannot be connected.
* If you want to connect to another VPC through a peer VPC, you must use the **route** settings provided by the peering to have packets forwarded through the VM instance.

    !!! tip "Note"
        For information on how to use routes, refer to "Common Feature > Route" below.

* If the IP address ranges of the two VPCs overlap, peering cannot be used.<br>
  The IP address range of one VPC must not be a subset of the other. If this condition is not met, peering creation will fail.
* In regions other than Korea, communication is only possible from subnets connected to the **default routing table**.

    !!! tip "Note"
        When peering is created, a routing rule that forwards packets destined for the counterpart VPC's IP address range to the Peering Gateway is implicitly added to the default routing table to route peering communication. Therefore, you cannot configure another route with the counterpart VPC's IP address range as the CIDR in the default routing table. In addition, if you add a route that specifies a subset of the counterpart VPC's IP address range as the CIDR, it takes priority over the route for peering communication, which may cause peering communication to fail. Use caution in such cases.

* In the Korea region, after creating a peering, you must configure separate routes in the routing tables of both peered VPCs to enable communication.
    * Add the route by entering the IP address range of the counterpart VPC in the route's **Target CIDR**, and selecting the **PEERING** entry with the name of the peering from the gateway list.
    * Communication is only possible through subnets connected to the routing table where the route was added.
    * If you add a route to a routing table other than the default routing table, peer communication is possible from subnets connected to that routing table.
    * If you specify a VPC that has no subnets when creating a peering, the peering creation will fail.

<a id="create-a-peering"></a>
### Create Peering { #create-a-peering }

1. Go to **Network > Peering Gateway > Peering**.
2. Click the **Create Peering** button.
3. Enter a **Name** and **Description**, select the **Local VPC** and **Peer VPC**, and click **OK**.

<a id="change-a-peering"></a>
### Change Peering { #change-a-peering }

1. Go to **Network > Peering Gateway > Peering**.
2. Select the peering to change from the peering list.
3. Click the **Change Peering** button.
4. Change the **Name** or **Description** of the peering and click **OK**.

<a id="delete-a-peering"></a>
### Delete Peering { #delete-a-peering }

1. Go to **Network > Peering Gateway > Peering**.
2. Select the peering to delete from the peering list.
3. Click the **Delete Peering** button.

<a id="other-important-notes-on-retrieving-peering-ports-using-the-api"></a>
### (Other) Important Notes on Retrieving Peering Ports Using the API { #other-important-notes-on-retrieving-peering-ports-using-the-api }

When retrieving ports associated with peering using the API, the retrieval method differs depending on whether a **Peer ID** exists in the peering resource.

!!! tip "Note"
    For information on how to check the peer ID, refer to "References > How to check the peer ID" below.

* If there is no **Peer ID**: Retrieve using only the peering ID, as before.
    * GET /v2.0/ports?device_id={peering ID}
* If there is a **Peer ID**: You must pass both the peering ID and the peer ID to retrieve ports from both VPCs.
    * GET /v2.0/ports?device_id={peering ID}&device_id={peer ID}

<a id="region-peering"></a>
## Region Peering { #region-peering }

**Region Peering** is a feature that connects two **VPCs** created in different regions. Peering can be used to connect VPCs in the same region, but it cannot be used to connect VPCs in different regions. However, Region Peering allows you to connect two VPCs in different regions.

* Region peering connects two VPCs in different regions. Connecting to another VPC across a VPC is not supported. For example, in the `A <-> B <-> C` connection, `A` and `C` cannot be connected.
* If you want to connect to another VPC through the Peer VPC, you must configure the **route** settings provided by the peering so that packets are routed through a VM instance.

    !!! tip "Note"
        For information on how to use routes, refer to 'Common Feature > Route' below.

* You can connect VPCs in the same project or in different projects.
* When a region peering is created, it is automatically created in the connected region.
* When a region peering is deleted, it is automatically deleted in the connected region.
* If the IP address ranges of the two VPCs overlap, region peering cannot be used.
* Duplicate VPC connections cannot be created.
* A separate **route** must be configured in the **routing table** of both peered VPCs to enable communication.
    * Add the route by entering the IP address range of the counterpart VPC in the route's **Target CIDR**, and selecting the **INTER_REGION_PEERING** entry with the name of the region peering from the gateway list.
    * Communication is only possible through subnets connected to the routing table where the route was added.
    * If a route is added to a routing table other than the default routing table, peering communication is possible from subnets connected to that routing table.
    * If a VPC without a subnet is specified when creating region peering, the region peering creation fails.

<a id="create-a-region-peering"></a>
### Create Region Peering { #create-a-region-peering }

!!! tip "Note"
    To create a region peering between different projects, your project's tenant ID and VPC ID must be allowed in Manage Peering Allowed Targets of the peer project. This is not required when creating a region peering within the same project.
    Before you can create a region peering between different projects, you must send your tenant ID and VPC ID to the administrator of the peer project and request to register the information in Manage Peering Allowed Targets.
    After registration of information in the peer project is completed, you can create a region peering by following these steps.
    For information on how to use Manage Peering Allowed Targets, refer to 'Common Feature > Manage Peering Allowed Targets' below.

1. Go to **Network > Peering Gateway > Region Peering**.
2. Click the **Create Region Peering** button.
3. Select the **Name**, **Local VPC**, and **Peer Region**.
4. Select the **Peer Tenant**.
    * If you select **Same Tenant**, no additional information is required.
    * If you select **Other Tenant**, you must enter the **Peer Tenant ID**.

    !!! tip "Note"
        For the Peer Tenant ID, refer to the 'References' section below.

5. Enter the **Peer VPC ID**.

    !!! tip "Note"
        For the Peer VPC ID, refer to the 'References' section below.

<a id="delete-a-region-peering"></a>
### Delete Region Peering { #delete-a-region-peering }

1. Go to **Network > Peering Gateway > Region Peering**.
2. In the peering list, select the region peering to delete.
3. Click the **Delete Region Peering** button.

<a id="project-peering"></a>
## Project Peering { #project-peering }

**Project Peering** is a feature to connect two **VPCs** created in different projects. Peering can be used to connect VPCs in the same project, but it cannot be used to connect VPCs in different projects. However, the project peering feature allows you to connect two VPCs in different projects.

* Project peering connects two VPCs in different projects. Connecting to another VPC across a VPC is not supported. For example, in the `A <-> B <-> C` connection, `A` and `C` cannot be connected.
* If you want to connect to another VPC through the Peer VPC, you must configure the **route** settings provided by the peering so that packets are routed through a VM instance.

    !!! tip "Note"
        For information on how to use routes, refer to 'Common Feature > Route' below.

* Only two VPCs in different projects within the same region can be connected.
* When a project peering is created, it is automatically created in the connected project.
* When a project peering is deleted, it is automatically deleted in the connected project.
* If the IP address ranges of the two VPCs overlap, project peering cannot be used.
* Duplicate VPC connections cannot be created.
* A separate **route** must be configured in the **routing table** of both peered VPCs to enable communication.
    * Add the route by entering the IP address range of the counterpart VPC in the route's **Target CIDR**, and selecting the **INTER_PROJECT_PEERING** entry with the name of the project peering from the gateway list.
    * Communication is only possible through subnets connected to the routing table where the route was added.
    * If a route is added to a routing table other than the default routing table, peering communication is possible from subnets connected to that routing table.
    * If a VPC without a subnet is specified when creating project peering, the project peering creation fails.

<a id="create-a-project-peering"></a>
### Create Project Peering { #create-a-project-peering }

!!! tip "Note"
    To create a project peering, your project's tenant ID and VPC ID must be allowed in Manage Peering Allowed Targets of the peer project.
    Before creating a project peering, you need to pass the tenant ID and VPC ID to the administrator of the peer project and ask them to register the information in Manage Peering Allowed Targets.
    After registration of information in the peer project is completed, you can create a project peering by following these steps.
    For information on how to use Manage Peering Allowed Targets, refer to 'Common Feature > Manage Peering Allowed Targets' below.

1. Go to **Network > Peering Gateway > Project Peering**.
2. Click the **Create Project Peering** button.
3. Enter the **Name**, **Local VPC**, **Peer Tenant ID**, and **Peer VPC ID**.

    !!! tip "Note"
        For information on how to check the Peer Tenant ID and Peer VPC ID, refer to the 'References' section below.

<a id="delete-a-project-peering"></a>
### Delete Project Peering { #delete-a-project-peering }

1. Go to **Network > Peering Gateway > Project Peering**.
2. In the peering list, select the project peering to delete.
3. Click the **Delete Project Peering** button.

<a id="common-feature"></a>
## Common Feature { #common-feature }

Describes the common features provided by peering (Peering, Region Peering, and Project Peering).

<a id="manage-peering-allowed-targets"></a>
### Manage Peering Allowed Targets { #manage-peering-allowed-targets }

The Region Peering, Project Peering page submenu allows you to set up a peering connection request between different projects on the receiving end. Enter the peer tenant ID of the VPC sending the request and the peer VPC ID to add it to the peering allowed VPCs and allow the peer to accept the request.

<a id="manage-peering-allowed-targets-add-an-peering-allowed-target"></a>
#### Add Peering Allowed Target

1. Go to **Network > Peering Gateway > Region Peering** or **Network > Peering Gateway > Project Peering**.
2. Click the **Manage Peering Allowed Targets** button.
3. Click the **Add Peering Allowed VPC** button.
4. Enter the **Name**, **Peer Tenant ID**, and **Peer VPC ID**, then click **OK**.

    !!! tip "Note"
        For information on how to check the peer tenant ID and peer VPC ID, refer to the 'References' section below.

<a id="manage-peering-allowed-targets-delete-a-peering-allowed-target"></a>
#### Delete Peering Allowed Target

1. Go to **Network > Peering Gateway > Region Peering** or **Network > Peering Gateway > Project Peering**.
2. Click the **Manage Peering Allowed Targets** button.
3. In the peering allowed VPC list, click the delete button for the target to delete.

<a id="route"></a>
### Route { #route }

You can use the **route** settings provided by peering to configure traffic forwarding to other VPCs via VM instances in the peer VPC. The peering route can be configured by specifying the port and virtual IP port of the VM instance that processes all traffic coming from the peering. If you deploy a Network Virtual Appliance (NVA) VM that serves as the gateway for the route, you can control traffic inside the VM instance and forward traffic to other peerings.
* A configuration that sets up a hub and spoke (Hub & Spoke) VPC connection through peering and controls all traffic with the Network Virtual Appliance located in the hub VPC can be achieved by using the routing feature of peering.

<a id="route-create-route"></a>
#### Create Route

1. Select the peering for which you want to configure a route.
2. Select the route tab at the bottom.
3. Click the **Change Route** button.

    !!! tip "Note"
        For peering, there are two buttons. Change Peer Route is to add a route to the peer VPC selected when the peering was created, while Change Local Route refers to the local VPC location.

4. Click the **+** button.
5. Enter the target CIDR.
6. Select a gateway.

    !!! tip "Note"
        Only instances and virtual IPs can be selected as the gateway.

7. Click **OK**.

<a id="route-delete-route"></a>
#### Delete Route

1. Select the peering from which you want to delete a route.
2. Select the route tab at the bottom.
3. Click the **Change Route** button.

    !!! tip "Note"
        For peering, there are two buttons. Change Peer Route is to add a route to the peer VPC selected when the peering was created, while Change Local Route refers to the local VPC location.

4. Click the **-** button for the target to delete.
5. Click **OK**.

<a id="other-considerations"></a>
## References { #other-considerations }

<a id="how-to-check-peer-vpc-id"></a>
### How to Check Peer VPC ID { #how-to-check-peer-vpc-id }

You can check the **VPC ID** of the peer with the following steps.

!!! tip "Note"
    If you do not have access to the project that the peer VPC belongs to, ask the administrator of the peer project to provide you with the VPC ID.

1. Access the Console of the peer project.
2. Go to **Network > VPC > Management**.
3. Select the target VPC for peering.
4. Copy the UUID value displayed in **Basic Information > VPC Name**.

<a id="how-to-check-the-peer-tenant-id"></a>
### How to Check the Peer Tenant ID { #how-to-check-the-peer-tenant-id }

You can check the **tenant ID** of the peer with the following steps.

!!! tip "Note"
    If you do not have access to the peer project, obtain a tenant ID from the administrator of the peer project.

1. Access the Console of the peer project.
2. Go to **Network > VPC > Management**.
3. Select any one VPC from the peering target or the VPCs displayed on the screen.
4. Copy the ID value displayed in **Basic Information > Tenant ID**.

<a id="how-to-check-the-peer-id"></a>
### How to Check the Peer ID { #how-to-check-the-peer-id }

You can check the peer ID of the peering with the following steps.

!!! tip "Note"
    For peerings where the peer ID is not displayed, you can look up the port using the existing method.

1. Go to **Network > Peering Gateway > Peering**.
2. Select the target peering.
3. Copy the value displayed in **Basic Information > Peer ID**.