## Security > Network Firewall > Overview

Network Firewall is a network security service that NHN Cloud provides to securely protect infrastructure assets used in NHN Cloud.
You can apply access control specialized for NHN Cloud and easily use firewall features without using separate firewall products.


> The Network Firewall service is available only in the new network environment for the Korea (Pangyo) region.
> Projects created before March 7, 2022 in the Korea (Pangyo) region use the previous network environment, so you must create a new project to use the Network Firewall service.

## Major Features
* You can efficiently manage network communication policies.
    * Controls traffic with a single policy using the Stateful method.
* You can securely protect instances from external attacks using a Hub-Spoke architecture.
    * Controls internal traffic between VPCs and inbound/outbound traffic.
* Provides a secure Virtual Private Network (VPN) through encrypted tunnels between sites in the internet environment.    
* Provides real-time log search and backup features for network blocking and allowing.
    * Provides various backup methods tailored to customer environments (Syslog, Object Storage, Log & Crash Search).
* Provides high availability (redundancy) for stable operation.

## Network Firewall Service Architecture
You can configure the service in the following five configurations:

### Single Project
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/Architecture1.png" height="70%">

### Multiple Projects
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/Architecture2.png" height="70%" width="100%" />


### Cross-Region Projects
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/Architecture3.png" height="70%" width="100%" />


### Two Spoke VPCs in a Single Project
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/Architecture4.png" height="70%" width="100%" />


### Multiple Subnets in a Single VPC
<img src="https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/Architecture5.png" height="50%" width="100%" />


> [Note]
> 
> * The above architecture diagrams are general configurations, and the configuration of WEB, WAS, Load Balancer, and other components except Network Firewall may differ depending on the customer's environment.
> 
> * In cross-region project environments, only the same project can be configured. For more information, see the [User Guide](https://docs.nhncloud.com/ko/Network/Peering%20Gateway/ko/console-guide/).
> 
> * When configuring the service, you cannot connect to network environments configured before March 7, 2022.
> For example, if a project using a network environment configured before March 7, 2022 and a project using a network environment configured after that date exist, you can create Network Firewall in the new network environment, but you cannot use the network environment from before the improvement as a Spoke VPC.
