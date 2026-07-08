## Network > Colocation Gateway > Console User Guide

This guide describes how to use the **Colocation Gateway** service from the console.

## Colocation Gateway

### Create a Colocation Gateway

To create a **colocation gateway**, use the following steps:

> [Note] Only VPCs pre-registered in NHN Cloud Zone can communicate with the on-premises network. For VPCs that are required to communicate with the on-premises network, make sure that you contact through [1:1 inquiry](https://www.nhncloud.com/kr/support/inquiry) of the NHN Cloud Customer Center before creating a colocation gateway.<br>
> [Caution] If you create a colocation gateway by selecting a VPC that is not pre-registered in the NHN Cloud Zone, communication with the on-premises network is not possible, and only communication with other VPCs connected to the same NHN Cloud Zone is available.

1. Go to **Network > Colocation Gateway**.
2. If you click **Create Colocation Gateway**, the screen for creation appears.
3. Enter the **Name** to use for the **colocation gateway**.
4. Choose a **VPC**.<br>
   The selected VPC is connected to the NHN Cloud Zone.<br>
   A VPC can be connected to only one NHN Cloud Zone.
5. Select **NHN Cloud Zone**.
6. Click **Confirm**.

### View a Colocation Gateway

You can view the created colocation gateway on the **Network > Colocation Gateway** page. If you select a colocation gateway, the colocation gateway information appears at the bottom.

### Modify a Colocation Gateway

A colocation gateway can be modified as follows. You can only change **Name** and **Description**.

1. Go to **Network > Colocation Gateway**.
2. Click **Change Colocation Gateway** and change items on the change screen.

### Delete a Colocation Gateway

To delete a colocation gateway, select the colocation gateway you want to delete in the **Network > Colocation Gateway** page and click the Delete Colocation Gateway button.

### Route

You can specify the port and virtual IP port of VM instances that process traffic coming from the colocation gateway. If you deploy Network Virtual Appliance VM that serves as the gate way for the route, you can control traffic inside the VM instance and forward traffic to other VPC by using the peering feature.<br>
* You can use the colocation gateway’s route feature to add the customer’s on-premises network to the hub VPC as a spoke in a situation where traffic is controlled by Network Virtual Appliance in the hub VPC after configuring VPC connection of hub and spoke model through peering. 

> [Note] This feature is only available in the Korea (Pangyo) and Korea (Pyeongchon) regions.

#### Create a Route

1. Select a colocation gateway in which you want to set a route.
2. Select Route in the bottom tab.
3. Select the **Change Route** button.
4. Click the **+** button.
5. Enter the target CIDR.
6. Select a gateway.
   > [Note] You can only select instance and virtual IP in a gateway.<br>
7. Click the **Confirm** button.

#### Delete a Route

1. Select a colocation gateway in which you want to delete a route setting.
2. Select a route in the botton tab.
3. Click the **Change Route** button.
4. Click the **+** button for the route to delete.
5. Click the **Confirm** button.

## Use a Colocation Gateway

To transmit packets to an on-premises network, add a routing path in **Network > Routing**.

### Configure a Route for a Colocation Gateway

1. Go to **Network > Routing**.
2. Choose the **Routing Table** for the **VPC** where you created the **colocation gateway**.
3. Select the **Route** tab from the **Routing Table** information displayed at the bottom.
4. Click **Create Route** to display the creation screen.
5. Enter the **Target CIDR**.<br>
   On-premises network CIDR or CIDR of another VPC connected to the same NHN Cloud Zone
6. Under **Gateway**, select **TRANSIT_GATEWAY** from the **Select Gateway** list.<br>
   > [Note] The TRANSIT_GATEWAY item can be created using Create Colocation Gateway.
