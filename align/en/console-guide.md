## Network > Transit Hub > Console User Guide

This guide describes how to use the Transit Hub service from the console.

## Manage

Manage **Transit Hub** settings.

### Create Transit Hub

To create a transit hub, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. Click **Create Transit Hub** to display the creation screen.
3. On the creation screen, enter the information about the Transit Hub.
    * Name: Enter a name for the transit hub.
    * Description: Describe the description of the transit hub.
    * Multicast support: Check if multicast communication is required.
    * Attach default routing table: When **attachment** is created, it automatically is attached to the default routing table.
    > [Note] Attachments created by shared transit hubs are not automatically attached to the default routing table.
    * Default routing table propagation: Automatically add the CIDR setting value of VPC related to **attachment** to the default routing table as a routing rule.
    > [Note] Attachments created by shared transit hubs are not automatically propagated to the default routing table.
> [Caution]
> * You cannot change multicast support, default routing table attachment/propagation settings.
> * Default routing table is created only when one or more of the default routing table attachments or default routing table propagation is selected.

### Modify Transit Hub

A transit hub can be modified as follows. You can only change the name and description.

1. Go to **Network > Transit Hub > Manage**.
2. Select a transit hub that you want to modify from the list on the screen.
3. Click **Modify Transit Hub** to display the modification screen.
4. On the modification screen, make changes to an item.

### Delete Transit Hub

To delete a transit hub, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. Select a transit hub that you want to delete from the list on the screen.
3. Click **Delete** Transit Hub to delete.

### Share Transit Hub

Share a transit hub with another project. In another project, you can create **Attachment** to the **shared transit hub**.<br>
To share Transit Hub, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. Select a transit hub that you want to share from the transit hub list.
3. Click **Share Transit Hub**, and enter the **tenant ID** of the other project with which you want to share the transit hub on the screen. <br>
> [Note] How to check out the **tenant ID** of another project
If you do not have access to another project, obtain a tenant ID from the administrator of the project.
> 1. Access the console screen of the project.
> 2. Go to **Network > VPC > Management**.
> 3. Select one of the VPCs that appears in the screen list.
> 4. Copy the ID value shown in **Basic Information > Tenant ID.

## Attach

Manage attachment that defines the relationship between transit hubs and other resources.

### Create Attachment

To create attachment, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to create an attachment
3. Go to the **Attachment** page.
4. Click **Create Attachment to display the creation screen.
5. On the creation screen, enter the information about attachment.
    * Name: Enter a name of the attachment.
    * Description: Describe the description of attachment.
    * Resource type: Select a resource type.
    > [Note] Currently, only VPC can be selected as the resource type.
    * Resource: Select a resource that is related to attachment.
    > [Note] Since only VPC can be selected as the resource type, only the VPC list is automatically output.
    * Subnet: Select a subnet where the **network interface** of the attachment is created.

### Modify Attachment

Attachment can be modified as follows. You can only change the name and description.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to modify the attachment.
3. Go to the **Attachment** page.
4. Select attachment you want to modify from the list.
5. Click **Modify Attachment** to display the modification screen.
6. On the modification screen, make changes to an item.

### Delete Attachment

To delete attachment, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to delete the attachment.
3. Go to the **Attachment** page.
4. Select attachment you want to delete from the list.
5. Click **Delete Attachment** to delete.

## Routing Table

Manage the Routing Table settings on the Transit Hub.

### Create Routing table

To create a routing table, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to create a routing table.
3. Go to the **Routing Tables** page.
4. Click **Create Routing Table** to display the creation screen.
5. On the creation screen, enter the information about the routing table.
    * Name: Enter a routing table name.
    * Description: Describe the description of a routing table.

### Modify Routing Table

Routing table can be modified as follows. You can only change the name and description.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to modify a routing table.
3. Go to the **Routing Tables** page.
4. Select a routing table you want to change from the list.
5. Click **Modify Routing Table** to display the modification screen.
6. On the modification screen, make changes to an item.

### Delete Routing Table

To delete routing table, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to delete a routing table.
3. Go to the **Routing Tables** page.
4. Select a routing table you want to delete from the list.
5. Click **Delete Routing Table** to delete.

### Manage Routing Table

Check the basic information for the selected **routing table and manage the packet handling rules and settings associated with routing.

#### Basic Information

You can check the basic information for the selected routing table.

#### Routing Association

Manage **routing association** that defines the relationship with the attachment for routing table to receive packets.

##### Create Routing Association

To create **routing association, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a routing table.
3. Go to the **Routing Tables** page.
4. Select a routing table you want to manage from the list.
5. Go to the **Routing Association** page at the bottom.
6. Click **Create Routing Association** to display the creation screen.
7. On the creation screen, enter the information about Routing Association.
    * Attach: Select an attachment for a routing table to receive packets.
    > [Note] One attachment on a Transit Hub can only create one routing association on a routing table.

##### Delete Routing Association

To delete routing association, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a routing table.
3. Go to the **Routing Tables** page.
4. Select a routing table you want to manage from the list.
5. Go to the **Routing Association** page at the bottom.
6. Select routing association you want to delete from the list.
7. Click **Delete Routing Association** to delete.
   
#### Routing Propagation

You can automatically create a **routing rule** in the **routing table** that manages the outbound policy for packets. Manage **routing propagation**, which defines the relationship with **attachment** to automatically create **routing rules**.
> [Caution]
> * If a **routing rule** with the same band as the CIDR to be propagated already exists, the **routing rule by routing propagation is not automatically registered.
>     * **Routing propagation** that fails automatic **routing rule** registration changes its status to ERROR. Appropriate action is required, such as reviewing the CIDR and recreating **routing propagation** or using manual setting of **routing rules**.
> * Even if **routing propagation** is added for two or more **attachments** with the same network bandwidth (CIDR), routing rules are automatically registered only for the first routing propagation created in the same way as above.

##### Create Routing Propagation

To create routing propagation, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a routing table.
3. Go to the **Routing Tables** page.
4. Select a routing table you want to manage from the list.
5. Go to the **Routing Propagation** page.
6. Click **Create Routing Propagation** to display the creation screen.
7. On the creation screen, enter the information about Routing Propagation.
    * Attach: Select attachment that automatically creates a routing rule for routing table to receive packets.
    > [Note] One attachment in a transit hub can create up to one routing propagation per routing table.

##### Delete Routing Propagation

To delete routing propagation, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a routing table.
3. Go to the **Routing Tables** page.
4. Select a routing table you want to manage from the list.
5. Go to the **Routing Propagation** page.
6. Select Routing Propagation you want to delete from the list.
7. Click **Delete Routing Propagation** to delete.
> [Caution] When deleting routing propagation, the routing rule that was automatically added will be deleted together.

#### Routing Rule

Manage **routing rules** that handle the outbound rules of packets from the routing table.
> [Note] **Routing Rule** cannot be added if Routing Rule in the same band as the CIDR to be propagated already exists.

##### Create Routing Rule

To create a routing rule, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a routing table.
3. Go to the **Routing Tables** page.
4. Select a routing table you want to manage from the list.
5. Go to the **Routing Rule** page.
6. Click **Create Routing Rule** to display the creation screen.
7. On the creation screen, enter the information about routing rule.
    * CIDR: Enter the destination network band for the routing policy.
    > [Note] The priority of routing rules in the routing table is determined by the Longest Pre-fix Matching result of CIDR set in the routing rule.
    * Method: Select how to handle packets matched to the CIDR. Selecting **FORWARD** will send the packets to the specified attachment, and selecting **BLACKHOLE** will destroy the packets.
    * Attach: If **FORWARD** is selected from **Method**, select **attachment** to send packets from **Routing Table**.

##### Delete Routing Rule

To delete routing rule, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a routing table.
3. Go to the **Routing Tables** page.
4. Select a routing table you want to manage from the list.
5. Go to the **Routing Rule** page.
6. Select routing rule you want to delete from the list.
7. Click **Delete Routing Rule** to delete.

## Multicast

Manage the **Multicast settings on Transit Hub.
> [Caution] **Multicast Domain** cannot be created if **Multicast Support is not selected on Transit Hub and all multicast-related features are unavailable to use.

### Create Multicast Domain

To create **multicast domain, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to create a multicast domain.
3. Go to the **Multicast** page.
4. Click **Create Multicast Domain** to display the creation screen.
5. On the creation screen, enter the information about multicast domain.
    * Name: Enter the name of multicast domain.
    * Description: Describe the description of multicast domain.

### Modify Multicast Domain

Multicast domain can be modified as follows. You can only change the name and description.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to modify a multicast domain.
3. Go to the **Multicast** page.
4. Select multicast domain you want to modify from the list.
5. Click **Modify Multicast Domain** to display the modification screen.
6. On the modification screen, make changes to an item.

### Delete Multicast Domain

To delete Multicast domain, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of multicast domains, click **View Details** for the transit hub from which you want to delete the multicast domain.
3. Go to the **Multicast** page.
4. Select multicast domain you want to delete from the list.
5. Click **Delete Multicast Domain** to delete.

### Share Multicast Domain

Share a multicast domain to another project. Other projects can create **multicast connections and** **multicast groups**from the list of multicast domains output **from the multicast** **under the shared transit hub**.<br>
To share a multicast domain, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to share a multicast domain.
3. Select multicast domain you want to share from the list.
4. Select **multicast domain you want to share from the list on the screen.
3. Click **Share Multicast Domain**, and then on the screen, enter the **tenant ID** of the other project with which you want to share the multicast domain. <br>
> [Note] How to check out the **tenant ID** of another project
If you do not have access to another project, obtain a tenant ID from the administrator of the project.
> 1. Access the console screen of the project.
> 2. Go to **Network > VPC > Management**.
> 3. Select one of the VPCs that appears in the screen list.
> 4. Copy the ID value shown in **Basic Information > Tenant ID**.

### Manage Multicast

Check basic information for the selected multicast domain and manage the packet handling policy and settings associated with the multicast.

#### Basic Information

You can check the basic information for the selected multicast domain.

#### Multicast Association

Manage multicast associations join subnets of VPC-type attachments to multicast networks in multicast domains.
> [Note]
> * Only **attachment** of VPC type is available on multicast association.
> * **Attachment** created in other project by transit hubs shared with other projects cannot be used in multicast association.
> * One subnet is only available to use on one **multicast association** throughout the entire **NHN Cloud**.This means that one **subnet** can only be attached to one **multicast domain**.

##### Create Multicast Association

To create multicast association, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a multicast domain.
3. Go to the **Multicast** page.
4. Select multicast domain you want to manage from the list.
5. Go to the **Multicast Association** page.
6. Click **Create Multicast Association** to display the creation screen.
7. On the creation screen, enter the information about multicast association.
    * Attach: Select attachment to join the multicast network in multicast domain.

##### Delete Multicast Association

To delete multicast association, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a multicast domain.
3. Go to the **Multicast** page.
4. Select multicast domain you want to manage from the transit hub list.
5. Go to the **Multicast Association** page.
6. Select multicast association you want to delete from the list on the screen.
7. Click **Delete Multicast Association** to delete.

#### Multicast Group

**Network interfaces** to participate in multicast communication provided by the **multicast domain** are managed as a **multicast group**. By configuring the **multicast group**, **network interfaces** with the same group IP address perform multicast communication with each other.<br>
> [Note] Only **Network Interface of VM Instance can be added as a multicast group.

##### Create Multicast Group

To create Multicast group, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a multicast domain.
3. Go to the **Multicast** page.
4. Select multicast domain you want to manage from the list.
5. Go to the **Multicast Group** page.
6. Click **Create Multicast Group** to display the creation screen.
7. On the creation screen, enter the information about multicast domain.
    * Multicast association: Select **Multicast Association**.
    * Network interface: Select **Network Interface* .
    * Group IP Address: Enter the multicast IP address.
    > [Note]
    > * The multicast IP address must be within the range 224.0.0.0/4.
    > * 221.0.0.1 cannot be entered. 
    * Type: Choose between member and source
        * Member<br>
          Receive multicast packets whose destination is the group IP address.<br>
          Network interface specified as a source in the same group cannot be specified as a member.
        * Source<br>
          Send multicast packets whose destination is the group IP address.Only one **network interface** can be specified as a source for each **group IP address**.<br>
          Network interface specified as a source in the same group cannot be specified as a member.

##### Delete Multicast Group

To delete multicast group, use the following steps.

1. Go to **Network > Transit Hub > Manage**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a multicast domain.
3. Go to the **Multicast** page.
4. Select multicast domain you want to manage from the transit hub list.
5. Go to the **Multicast Group** page.
6. Select multicast domain you want to delete from the list.
7. Click **Delete Multicast Group** to delete.

## Shared Transit Hub

If you've been shared transit hubs owned by other projects, you can view the list and join the communication on the **Shared Transit Hub** page.
> [Note] The following settings are available in the shared transit hub.
> * You can set up attachment and multicast by clicking View Details.
> * You can connect a VPC you own to a shared transit hub by creating an attachment.
> * If you have been given a shared multicast domain, the subnet of the VPC you own can participate in multicast communication managed by the multicast domain.

## Attachment (shared transit hub)

Manage attachments that define relationships between shared transit hubs and other resources.

### Create Attachment

To create attachment, use the following steps.

> [Note] Attachments created on shared transit hubs are not eligible for default routing table attachment, automatic routing table attachment by default routing table propagation, and routing rule auto-registration.

1. Go to **Network > Transit Hub > Shared Transit Hub**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to create an attachment
3. Go to the **Attachment** page.
4. Click **Create Attachment** to display the creation screen.
5. On the creation screen, enter the information about attachment.
    * Name: Enter a name of the attachment.
    * Description: Describe the description of attachment.
    * Resource type: Select a resource type.
    > [Note] Currently, only VPC can be selected as the resource type.
    * Resource: Select a resource that is related to attachment.
    > [Note] Only the VPC list is exposed because the resource type can only be a VPC.
    * Subnet: Select the subnet where the attachment's network interface is created.

### Modify Attachment

Attachment can be modified as follows. You can only change the name and description.

1. Go to **Network > Transit Hub > Shared Transit Hub**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to modify the attachment.
3. Go to the **Attachment** page.
4. In the list of transit hubs, select the attachment you want to change.
5. Click **Modify Attachment** to display the modification screen.
6. On the modification screen, make changes to an item.

### Delete Attachment

To delete attachment, use the following steps.

1. Go to **Network > Transit Hub > Shared Transit Hub**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to delete the attachment.
3. Go to the **Attachment** page.
4. Select attachment you want to delete from the list.
5. Click **Delete Attachment** to delete.

## Multicast (shared multicast domains)

Manage resources for participating in multicast communications in a shared received multicast domain.

### Manage Shared Multicast

Check basic information for the shared multicast domain and manage the packet handling policy and settings associated with the multicast.

#### Multicast Association

Manage **multicast association** so that VPC-type **attachment** can join the multicast network configured by a shared **multicast domain**.
> [Note]
> * Only attachment of VPC type is available on multicast association.
> * Attachment created in other project by transit hubs shared with other projects cannot be used in multicast association.
> * A single subnet can only create one multicast attachment, meaning that a single subnet can only be associated with one multicast domain.

##### Create Multicast Association

To create multicast association, use the following steps.

1. Go to **Network > Transit Hub > Shared Transit Hub**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a multicast domain.
3. Go to the **Multicast** page.
4. Select **multicast domain you want to manage from the list.
5. Select multicast domain you want to manage from the list.
6. Go to the **Multicast Association** page.
7. On the creation screen, enter the information about multicast association.
    * Attach: Select **attachment** to join the multicast network in multicast domain.

##### Delete Multicast Association

To delete multicast association, use the following steps.

1. Go to **Network > Transit Hub > Shared Transit Hub**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a multicast domain.
3. Go to the **Multicast** page.
4. Select multicast domain you want to manage from the list.
5. Go to the **Multicast Association** page.
6. Select multicast association you want to delete from the list.
7. Click **Delete Multicast Association** to delete.

#### Multicast Group

Manage network interfaces that will participate in multicast communications provided by a shared multicast domain as a multicast group. Multicast group settings enable network interfaces with the same group IP address to multicast communicate with each other.<br>
> [Note] Only the network interface of a VM instance can be added as a multicast group.

##### Create Multicast Group

To create Multicast group, use the following steps.

1. Go to **Network > Transit Hub > Shared Transit Hub**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a multicast domain.
3. Go to the **Multicast** page.
4. Select multicast domain you want to manage from the list.
5. Go to the **Multicast Group** page.
6. Click **Create Multicast Group** to display the creation screen.
7. On the creation screen, enter the information about multicast domain.
    * Multicast association: Select multicast association.
    * Network interface: Select network interface.
    * Group IP Address: Enter the multicast IP address.
    > [Note]
    > * Must be entered in the range of 224.0.0.0/4.
    > * 221.0.0.1 cannot be entered. 
    * Type: Choose between member and source
        * Member<br>
          Receive multicast packets whose destination is the group IP address.<br>
          Network interface specified as a source in the same group cannot be specified as a source.
        * Source<br>
          Send multicast packets whose destination is the group IP address.Only one network interface can be specified as a source for each group IP address.<br>
          Network interface specified as a source in the same group cannot be specified as a member.

##### Delete Multicast Group

To delete multicast group, use the following steps.

1. Go to **Network > Transit Hub > Shared Transit Hub**.
2. In the list of transit hubs, click **View Details** for the transaction hub from which you want to manage a multicast domain.
3. Go to the **Multicast** page.
4. Select multicast domain you want to manage from the list.
5. Go to the **Multicast Group** page.
6. Select multicast domain you want to delete from the list.
7. Click **Delete Multicast Group** to delete.

