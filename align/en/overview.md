## Network > NAT Gateway > Overview
An NAT gateway allows instances that is not connected to an internet gateway to access the internet. However, you cannot initiate connections to these instances from the internet.
This function is only available in the Korea (Pangyo) and Korea (Pyeongchon) regions.


### Main Features
* Instances that are not connected to an internet gateway can access the internet with the floating IP of an NAT gateway.
* When you configure a route specifying an NAT gateway as a gateway for a specific CIDR in the routing table, the source IP of packets destined for the configured CIDR from the instances connected to this routing table is converted to the floating IP of the NAT gateway.
* A single NAT gateway can be specified as a gateway in multiple routing tables in the same VPC.
* You can specify multiple NAT gateways as a gateway in a single routing table by identifying the destination CIDR.
* You cannot access instances with an NAT gateway address.
* If you are operating a firewall policy that allows internal access only to a specific source IP, you can configure the policy by specifying the floating IP of the NAT gateway. 
* Traffic that attempts a connection to an NAT gateway address from the outside is blocked.
* Network ACLs can be applied to the Korea (Pyeongchon) region.
