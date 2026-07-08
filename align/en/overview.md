## Network > Traffic Mirroring > Overview

Network packets in VPC can be captured and routed to detection tools for purposes such as content security, threat analysis, and troubleshooting.
Traffic Mirroring, with detection tools, allows you to quickly detect and respond to attacks and meet various security compliance requirements.

Traffic Mirroring is only available in new network environments in Korea (Pangyo) region and Korea (Pyeongchon) region.
For projects created before March 7, 2022 in Korea (Pangyo) region, they are in the old version network environment, so you must create new projects to use Traffic Mirroring.

## Main Features
* Mirror Session
    * Mirror source and target source can be linked with each mirror session unit.
* Mirror Source
    * It is a network interface to monitor network packets.
    * You can specify the instance's network interface.
    * The feature will be expanded to allow you to specify other resources as well.
* Mirror Target
    * It is a network interface to forward network packets copied from the mirror source.
    * You can specify the instance's network interface.
    * The feature will be expanded to allow you to specify other resources as well.
* Mirror Direction 
    * Direction of the packet to be mirrored can be set to inbound or outbound.
* Mirror Filter
    * Filters allow you to mirror only the specific network packets that you want.
    * You can specify protocols, ranges of source and target ports, and CIDR blocks of source and target.

## Service Targets
* When you want to capture network traffic and route it to the desired detection tool.
* When application traffic mirroring is required for testing and troubleshooting purposes.
