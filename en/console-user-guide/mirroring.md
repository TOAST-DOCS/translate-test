<!-- pre-align:aligned sig=7c6d3654a3c5 -->

<a id="mirroring"></a>
## Mirroring { #mirroring }

**Security > Network Firewall > Console User Guide > Mirroring**

The **Mirroring** tab copies network packets passing through Network Firewall to threat detection and analysis solutions such as IDS/IPS, SIEM, and NDR, enabling real-time detection and response to network threats.

!!! tip "Note"
    This feature can be used after enabling it by setting it to **Enabled** in **Options - Mirroring Settings**. (Activation takes approximately 30 seconds.)
    ![Mirorring_Config_Activation_800.png](../../static/images/Mirroring/25.03.06/Mirorring_Config_Activation_800.png)

<br>

<a id="configure-mirroring-rules"></a>
## Configure Mirroring Rules { #configure-mirroring-rules }

* Add mirroring rules to forward copied packets to the desired target device.
    * Name: Displays the name you set.
    * Direction: Displays the orientation you set.
    * Mirror specified interface: Displays the interface of the selected Network Firewall.
    * Mirroring Tx IP: Displays the IP of the mirroring interface.
    * Mirroring target IP: Displays the destination IP to send mirroring packets to.
    * Filter group: Displays the selected filter groups.
    * Status: Displays the status of this mirroring rule via a badge.
        * Active: Enabled 
        * Inactive: Disabled
    * Checks the detailed information of the configured mirroring rule.

<a id="add"></a>
### Add { #add }

* You can add a mirroring rule by clicking **Add**.
![Mirroring_Rule_Add_900.png](../../static/images/Mirroring/25.03.06/Mirroring_Rule_Add_900.png)
    * Status: Sets whether the mirroring rule is active or not.
    * Direction: Sets the incoming/outgoing packets to be mirrored on the mirroring interface. This setting allows you to mirror only packets in a specific direction.
        * Receive (Rx): Packets received on the mirror-designated interface
        * Transmit (Tx): Packets outgoing from the mirror-designated interface.
    * Mirror interface: Select from the following Network Firewall interfaces.
        * NetworkFirewall_INF_NAT: Upper interface for external control of Network Firewall
        * NetworkFirewall_INF_TRAFFIC: Lower interface for internal control of Network Firewall
    * Mirroring Tx IP: The mirroring interface on the external transmission subnet is set to default.
    * Mirror target IP: Enter the private IP of the target that will receive mirroring packets.
    * Virtual network identifier (VNI): Enter the VNI.

* Select a **filter group**.
    * If there are no previously added filter groups, you can click **Add Filter Group** to add one.
    * For more information, see [Filter Group Description](#%ED%95%84%ED%84%B0%20%EA%B7%B8%EB%A3%B9).
![Mirroring_Rule_Filter_Group_900.png](../../static/images/Mirroring/25.03.06/Mirroring_Rule_Filter_Group_900.png)

<a id="modify"></a>
### Modify { #modify }

* You can click **Modify** to modify a mirroring rule.

<a id="delete"></a>
### Delete { #delete }

* You can click **Delete** to delete the mirroring rule.

!!! tip "Note"
    * You must configure access permissions for the Mirroring Tx IP and UDP port 4789 in your policies (security groups, firewalls, etc.) so that the mirroring target device can receive VXLAN packets.
    * You can create up to 3 mirroring rules.
    * Applying mirroring rules may generate a large amount of communication data depending on your environment, so you must enter the mirroring target IP information accurately.
    * Network Firewall sends mirroring packets via a VXLAN tunnel, so VNI configuration is required. Enter a VNI value between 1 and 16,777,215, and ensure it is set the same as the mirroring target device.
    * Only one filter group can be applied per rule, and only the name, description, protocol, and transmission status can be modified.

<br>

<a id="configure-filter-group"></a>
## Configure Filter Group { #configure-filter-group }

* By configuring filters to be applied to mirroring rules through the **Filter Group**, you can select and transmit only the packets you want.
    * Name: Displays the name you set.
    * Associated mirroring rules: Displays mirroring rules that use this filter group.
    * Description: Displays a description.
    * View filter rules: Check the rules configured for the filter group.

<a id="configure-filter-group-add"></a>
### Add { #configure-filter-group-add }

* You can click **Add** to add a filter group.
    * Filter Rule Definitions
        * Priority: A lower number indicates a higher priority. Rules are applied from the highest priority to forward mirroring packets.
        * Protocol: Specifies the protocol.
            * ALL: Specifies all protocols. When selected, the source/destination settings are disabled.
            * TCP: Specifies TCP.
            * UDP: Specifies UDP.
            * ICMP: Specifies ICMP. When selected, the source/destination port settings are disabled.
        * Source/Destination CIDR: Configures the source and destination CIDR.
        * Source/Destination Port: Configure by selecting ALL, a port, or a port range.
            * ALL: Specifies all ports.
            * Port: Specifies a single port in the range of 1–65535.
            * Port range: Specifies a port range within 1–65535.
        * Forward: Configures whether to forward packets that match the rule.
            * Forward: Forwards packets that match the rule.
            * Do not forward: Does not forward packets that match the rule.

![Filter_Group_Add_900.png](../../static/images/Mirroring/25.03.06/Filter_Group_Add_900.png)

<a id="configure-filter-group-modify"></a>
### Modify { #configure-filter-group-modify }

* You can modify the filter group by clicking **Modify**.

<a id="configure-filter-group-delete"></a>
### Delete { #configure-filter-group-delete }

* You can delete the filter group by clicking **Delete**.

!!! tip "Note"

    * Click the [－] or [＋] button for each rule to delete or add rules, and click the up or down button to change the priority of a rule.
    ![Filter_Rule_900.png](../../static/images/Mirroring/25.03.06/Filter_Rule_900.png)
    * Up to 10 filter groups can be configured, including the default filter group.
    * Up to 30 filter rules can be configured.
    * Filter rules are applied in order from the highest to the lowest priority. Therefore, packets that have already been processed by a do-not-forward rule will not be subject to the next priority rule.
    * The default filter group cannot be deleted.