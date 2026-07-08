## Network > Transit Hub > Overview

If using **Transit Hub** service, a single gateway acting as a central hub allows multiple **VPC**s to form a centralized connection and an environment capable of communicating between **VPC**s. The service can eliminate complex peering relationships, centralize and simplify your network, and act as a router to manage communication paths between VPCs. </br>
**Transit Hub** is only available in new network environments for Korea (Pangyo) region. Projects created by Korea (Pangyo) region before March 7, 2022 are network environments before improvement, so you need to create new projects to use **Transit Hub**.

### Main Features

* Allows you to connect VPC resources to the internet.
* Provides routing settings between connected VPCs.
* Provides multicast communication between connected VPCs. Allows you to create multicast groups and set the recipients of traffic.
* Allows you to share Transit Hub with other projects within your organization.
* Allows you to implement a variety of architectures, including centralized connectivity and isolated routing.
* Streamline network configuration to increase operational efficiency.

### Service Targets

* When needs to simplify communication between VPCs by eliminating complex peering relationships.
* When routing between multiple VPCs needs to be centrally controlled
* When multicast communication between VPCs is required

### Terms

When multicast communication between VPCs is required

#### Transit Hub

It is a top-level resource that manages centralized connections and provides routing and multicast communication between connected resources.

#### Attachment

A resource that manages the association relationship between the Transit Hub and other resources. Currently, only **attachment** that is connected to the VPC is available.

#### Routing Table

Select **attachment** to forward packets based on the destination IP address of the packet and act as a router to forward packets. Depending on the settings that you enter when you create a Transit Hub, you can have one default routing table and if you need additional routing tables, you can create additional routing tables. 

#### Routing Association

These settings that specify **attachment** to which packets will flow into the **routing table**. Packets that flown into the **routing table** by **routing association** are forwarded to another **attachment** by **routing rule**. One **attachment** can only create one **routing association** from one **routing table**. 

#### Routing Propagation

Obtain the CIDR value of the resource associated with **attachment** and automatically create **routing rule**.

#### Routing Rule

This is a route policy included in the **routing table**. Set up static routing by specifying the destination CIDR and the **attachment** to which the packet is forwarded. Regardless of whether or not the **routing association** is created, you can designate the route of all **attachments** of the same **transit hub** and forward packets 
> [Note] All **attachments** under the same **transit hub** can be used as the next hop in the **routing rule**.

#### Multicast Domain

You can split a Transit Hub into multiple multicast domains and **multicast domains** will have multicast networks independent of one another.

#### Multicast Association

This is a setting to connect **attachment** and **multicast domain**. The **subnet** related to the VPC associated with the **attachment** will join the connected multicast network.
> [Note] One **subnet** can only be attached to one multicast domain.

#### Multicast Group

This means the set of VM instances that uses the same multicast IP address in the **multicast domain**. You can add **network interface** of VM instance that uses a subnet connected to a multicast domain as a multicast group.

* Group IP Address<br>
This is an IP address for multicast communication. VM instances that are set to source and member using the same group IP address in the multicast band can communicate multicast within the **multicast domain**.
* Source<br>
This is for sending multicast packets. You can specify one source per group IP address. The **network interface** specified as the source cannot be duplicated as a member of the same **group IP address**.
* Member<br>
This is for receiving multicast packets. Multicast packets sent by **source** are forwarded to the **network interface** specified by **member** with the same group IP address. 
