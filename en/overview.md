<!-- pre-align:aligned sig=b92c97be33b3 -->

# Cloud Access Overview

**Security > Cloud Access > Overview**

Cloud Access is a service that enables secure access to NHN Cloud resources based on a Zero Trust security model.

Using a dedicated agent, users can access resources easily without complex configurations. At the same time, administrators can efficiently manage the service through the NHN Cloud console, with features such as user and continuous authentication, real-time logging, and monitoring.

<br>

<a id="main-features"></a>
## Main Features { #main-features }

* Customized Account Management
    * Administrators can assign customized access permissions and policies to each user. Beyond simple allow/block rules, they can define which resources a user can access, during which time frames, and from which devices.
    * Users can be grouped based on the customer’s environment, enabling consistent policy enforcement even in complex user configurations.
* Continuous Device Verification
    * When accessing resources, users’ devices are continuously verified based on defined policies — including checks for IP and MAC addresses, OS, running processes, registry settings, antivirus status, and more.
* Real-time Monitoring and Logging
    * The system collects and stores real-time activity logs such as connection attempts, authentication history, and policy violations.
        * Administrators can quickly identify who is connected to which resources and detect any anomalies.
    * Collected logs are automatically stored in NHN Cloud’s Object Storage (OBS) or integrated with the Log & Crash Search service, based on the customer’s security requirements. This supports long-term log retention, regulatory compliance, and helps customers build a more structured and secure operating environment.

    
<br>

<a id="configuration-how-it-works"></a>
## Configuration & how it works { #configuration-how-it-works }

The administrator set up the user policy on the policy decision point (PDP) with the NHN Cloud console. If a user attempts to access the internal resource with sign-in afterwards, it will be allowed or denied by performing the real-time policy verification with Cloud Access service, which is a policy enforcement point (PEP).

![conncetion_Architecture_1.PNG](../static/images/2025.06.24/2025.07/architecture_3.png)

!!! tip "Important"
    Cloud Access can be configured in various ways. For details about how to configure, refer to [Console Guide - Get Started](./console-user-guide/cloud-access-start/).

<br>

<a id="price"></a>
## Price { #price }
The Cloud Access service fee is charged as follows:

* Fees will be charged from the moment you save and complete the required service settings in **Settings - Connection Settings**.
    * No fees will be charged upon service activation.

For more information on service fees, please refer to [Service Fee] (https://www.nhncloud.com/kr/service/security/cloud-access).

<br>

<a id="disable"></a>
## Disable { #disable }

!!! danger "Caution"
    If Cloud Access service is enabled in both the Korea (Pangyo) and Korea (Pyeongchon) regions and you disable it, the service will be disabled in all regions. Please be careful when disabling the service. (feature updates planned)