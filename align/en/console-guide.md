## Network > NAT Gateway > Console User Guide
This guide describes how to use the NAT Gateway service from the console.

## NAT Gateway 
This function is only available in the Korea (Pangyo) and Korea (Pyeongchon) regions.

### Create an NAT Gateway
Create an NAT gateway by setting the items below.

| Item      | Description                                                         |
| --------|------------------------------------------------------------ |
| Name      | You can specify the name of the NAT gateway. |
| VPC      | Specify the VPC in which to create the NAT gateway. |
| Subnet     | Specify a subnet among the subnets of the selected VPC, which is associated with the routing table with which the internet gateway is associated. You cannot create an NAT gateway with a subnet that does not satisfy the condition.  |
| Floating IP  | Specify the floating IP to assign to the NAT gateway. When accessing the internet, this IP is translated to a source IP. |
| Description      | You can add a description for the NAT gateway.  |

* You cannot change the VPC, subnet, and floating IP of an NAT gateway.
* A floating IP set on an NAT gateway cannot be disassociated. When the NAT gateway is deleted, the floating IP is automatically disassociated.
* You cannot access instances with an NAT gateway address.
* Traffic that attempts a connection to an NAT gateway address from the outside is blocked.
* Network ACLs are applied to the Korea (Pyeongchon) region.
* The quota for NAT gateway is 3.

### Configure a Route
* If you configure a route in the routing table that specifies the NAT gateway as a gateway for a specific CIDR, the NAT gateway is used.
* In instances connected to the routing table that has set the NAT gateway as a route, if the CIDR configured in the route is the destination, the source IP of the packet is converted to the floating IP of the NAT gateway.
* A single NAT gateway can be specified as a gateway in multiple routing tables of the same VPC.
* An NAT gateway can also be specified as a gateway in a routing table associated with a subnet that is different from the subnet specified when setting the NAT gateway.
* You can specify multiple NAT gateways as a gateway in a single routing table by identifying the destination CIDR.
* If you set the NAT gateway as a gateway for a route destination CIDR other than IP Prefix 0 (/0) in the route configuration, the communication will be performed through the NAT gateway even if the instance has a floating IP configured.


### Configure a Network ACL
If you configure a network ACL for the VPC of the NAT gateway in the Korea (Pyeongchon) region, it will also be applied to the NAT gateway. [How to configure a network ACL](https://docs.toast.com/en/Network/Network%20ACL/en/overview/)
