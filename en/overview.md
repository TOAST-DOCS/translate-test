<!-- pre-align:aligned sig=c8373fddc2f9 -->

<a id="network-firewall-overview"></a>
## Network Firewall Overview { #network-firewall-overview }

**Security > Network Firewall > Overview**

Network Firewall is a network security service to safely protect infrastructure assets used by NHN Cloud. 
You can easily use access control specialized for NHN Cloud and the firewall feature without using a separate firewall product.

!!! tip "Note"

    The Network Firewall service is only available in the new network environment for the Korea (Pangyo) region.
    Projects created before March 7, 2022 in the Korea (Pangyo) region are in the old network environment before the improvements, so you need to create a new project to use the Network Firewall service.

<br>

<a id="main-features"></a>
## Main Features { #main-features }

* Allows you to manage network communication policies efficiently.
    * Controls traffic with a single policy in the stateful manner.
* Allows for safe protection of instances against external attacks with the Hub-Spoke structure.
    * Controls internal traffic and inbound/outbound traffic between VPCs.
* Controls traffic by connecting multiple interfaces and configuring routes.
* Provides a secure virtual private network (VPN) over an encrypted tunnel between sites in an Internet environment.   
* Provides real-time log search and backup for blocking and allowing networks.
    * Provides several backup methods to suit the customer's environment (Syslog, Object Storage, Log & Crash Search).
* Provides high availability (redundancy) for reliable operation.

<br>

<a id="service-architecture"></a>
## Service Architecture { #service-architecture }
You can configure the service in the following five forms:

<a id="1-project"></a>
### 1 Project { #1-project }
![](https://static.toastoven.net/prod_nfw/26.07.28/1.overview/architecture1.png){ height="70%" }

<a id="1-or-more-projects"></a>
### 1 or More Projects { #1-or-more-projects }
![](https://static.toastoven.net/prod_nfw/26.07.28/1.overview/architecture2.png){ width="100%" height="70%" }


<a id="projects-between-different-regions"></a>
### Projects Between Different Regions { #projects-between-different-regions }
![](https://static.toastoven.net/prod_nfw/26.07.28/1.overview/architecture3.png){ width="100%" height="70%" }


<a id="2-spoke-vpcs-in-1-project"></a>
### 2 Spoke VPCs in 1 Project { #2-spoke-vpcs-in-1-project }
![](https://static.toastoven.net/prod_nfw/26.07.28/1.overview/architecture4.png){ width="100%" height="70%" }


<a id="multiple-subnets-in-a-single-vpc"></a>
### Multiple Subnets in a Single VPC { #multiple-subnets-in-a-single-vpc }
![](https://static.toastoven.net/prod_nfw/26.07.28/1.overview/architecturer5.png){ width="100%" height="50%" }


!!! tip "Note"
    * The above configuration diagram is a typical configuration, and the configuration of WEB, WAS, Load Balancer, etc. except Network Firewall may differ depending on the customer's environment.
    * In a project environment in a different region, it can only be configured in the same project. For more information, see the [user guide](/Network/Peering%20Gateway/en/console-guide/).

!!! danger "Caution"

    When you configure a service, you cannot associate it with the network environment configured before March 7, 2022.

    For example, if an organization has projects created that uses a network environment configured before 7 March 2022 and another that uses a network environment configureed afterwards, you can create a Network Firewall in the new network environment, but you cannot use the pre-improvement network environment as a Spoke VPC.