<!-- pre-align:aligned sig=9be9bdfa8e4e -->

<a id="network-firewall-troubleshooting-guide"></a>
## Network Firewall Troubleshooting Guide { #network-firewall-troubleshooting-guide }

**Security > Network Firewall > Troubleshooting Guide**

<br>

<a id="i-cannot-create-the-network-firewall-service"></a>
## I cannot create the Network Firewall service. { #i-cannot-create-the-network-firewall-service }

Check that the following network resources are prepared:

* Check that the Hub VPC and Spock VPC are ready.
* Check that the Hub VPC has 3 different subnets for traffic, NAT, and external transmission purposes.
* Check that the Spoke VPC or Spoke subnet is ready.
* Check that an internet gateway is connected to the routing table of the Hub VPC.

<br>

<a id="instances-in-the-spoke-vpc-cannot-communicate-with-the-internet"></a>
## Instances in the Spoke VPC cannot communicate with the internet. { #instances-in-the-spoke-vpc-cannot-communicate-with-the-internet }

Public communication from the Spoke VPC requires routing, peering, NAT, and ACL policies to all be configured. Check the following:

* Check that peering between the Hub VPC and Spoke VPC has been created.
* Check that a route for the Spoke CIDR destination has been added to the Hub VPC routing.
* Check that 0.0.0.0/0 or the required destination CIDR is set to the peering gateway in the Spoke VPC routing.
* Check that NetworkFirewall_INF_TRAFFIC_VIP is set as the gateway in the Peering Gateway route.
* Check that NAT settings have been added in **Network Firewall > NAT** tab.
* Check that the required allow policies have been added in **Network Firewall > Policy > ACL** tab.

<br>

<a id="instances-cannot-be-accessed-from-outside"></a>
## Instances cannot be accessed from outside. { #instances-cannot-be-accessed-from-outside }

Accessing instances from outside requires NAT, ACL, and Security Groups to all be configured. Check the following:

* Check that the Pre-NAT IP and Post-NAT IP are correctly connected in the **Network Firewall > NAT** tab.
    * Check that the IP object corresponding to the Post-NAT IP has been created first in the **Object** tab.
* Check that allow policies for the source, destination, and destination port exist in the **Network Firewall > Policy > ACL** tab
* Check that the source IP and port are also allowed in the instance's Security Groups.
* Check that a Floating IP has not been directly connected to the instance that requires access.
    * Directly connecting a Floating IP may cause communication issues.

<br>

<a id="blocked-logs-are-not-visible-in-the-log-tab"></a>
## Blocked logs are not visible in the Log tab. { #blocked-logs-are-not-visible-in-the-log-tab }

Logs blocked by the default-deny policy can only be checked after changing the default block policy log setting to enabled. Check the settings at the following path:

* Go to **Network Firewall > Options > Log Settings**, go to the default block policy log settings, and change to **Enabled**.
* Traffic logs are affected by the logging settings per policy and option configurations, so also check the logging settings of ACL policies.

<br>

!!! tip "If the issue is not resolved"

    If the issue persists after following the troubleshooting guide, contact the NHN Cloud Customer Center.
    * [Online 1:1 inquiry](https://www.nhncloud.com/kr/support/inquiry?sec_nfw_fn)
    * Main phone: 1588-7967 (Operating hours: Mon–Fri, 10 AM–7 PM)