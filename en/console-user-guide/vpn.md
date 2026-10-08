<!-- pre-align:aligned sig=b06e75492dcf -->

<a id="vpn"></a>
## VPN { #vpn }

**Security > Network Firewall > Console User Guide > VPN**

The **VPN** tab supports secure private communication through encrypted tunnels between sites.

<br>

<a id="create-gateway"></a>
## Create Gateway { #create-gateway }

* Click **Create Gateway** to create a gateway for connecting to a peer VPN device.

![gw_add.PNG](../../static/images/24.05.27/gw_add.png)

<a id="modify"></a>
### Modify { #modify }

* Click **Modify** button to modify a gateway.

<a id="delete"></a>
### Delete { #delete }

* Click the **Delete** button to delete a gateway.
    * If there is a tunnel connected to the gateway, it cannot be deleted.

<a id="associate-floating-ip"></a>
### Associate Floating IP { #associate-floating-ip }

* Configure the floating IP required for connection with the peer device.
    * Only unused floating IPs from the list created in **Network > Floating IP** are displayed.

![fip.PNG](../../static/images/24.05.27/fip.png)

!!! tip "Note"

    * VPC and subnet cannot be modified.
    * You can create up to 10 gateways.

<br>

<a id="create-tunnel"></a>
## Create Tunnel { #create-tunnel }

* Create a tunnel to connect to the peer device.

![tunnel_add.PNG](../../static/images/24.05.27/tunnel_add.png)

* Tunnel settings
    * Gateway: Gateways created in the Gateway tab are displayed. Select the gateway to connect to the tunnel.
        * If no gateway has been created, nothing is displayed.
    * Peer IP address: Enter the IP address of the peer VPN device to connect to.
    * IKE version: Set to the same version as the peer VPN device.
        * IKE version 1 supports Main Mode only.
    * Pre-Shared Key: Enter the same key value as the peer VPN device.
    * Dead Peer Detection (DPD): Attempts retransmission up to 5 times in 10-second intervals. When disabled, only responses to DPD requests from the peer VPN device are supported.
    * NAT-Traversal: A feature that prevents packet loss during tunnel creation. Generally, set to enabled when the peer VPN device has a public IP.
* Phase 1/2 settings
    * Enter the configuration information required to create an IPSec VPN tunnel.

!!! tip "Note"

    * Configure all settings to match the peer VPN device.
    * The local ID is optionally configured depending on the configuration method of the peer VPN device.
    * Up to 3 Phase 2 entries can be added.
    * Set the Phase 2 private IP to /24-bit or smaller. If a value larger than /24-bit needs to be configured, check the subnet range in advance and enter the starting IP of the subnet.
      * [Examples]
         * 192.168.100.0/20 (X) → 192.168.96.0/20 (O)
         * 172.16.30.0/21 (X) → 172.16.24.0/21 (O)
         * 10.0.50.0/22 (X) → 10.0.48.0/22 (O)
    * The local private IP and peer private IP must not overlap with each other. This range includes all private ranges connected to Network Firewall, including VPC peering.
    * The following CIDRs cannot be added to the local private IP or peer private IP. Adding them may cause communication issues for traffic passing through Network Firewall.
      * 10.0.0.0/8
      * 172.16.0.0/12
      * 192.168.0.0/16 

<a id="connect-tunnel"></a>
### Connect Tunnel { #connect-tunnel }

* The tunnel is created in a waiting for connection state. Click **Connect** to connect the created tunnel to the peer VPN device.

!!! tip "Note"

    * The status of each tunnel can be checked by color in the **Status** column.
      * Green: Connected normally to the peer VPN device
      * Red: Connection between peer VPN devices has failed due to issues such as configuration values or communication status
      * Gray: Waiting for connection (newly created tunnel)
      * Orange: Connection between peer VPN devices has been stopped by clicking the **Stop** button
    * After tunnel creation is complete, a connection may be established without clicking **Connect**, depending on the type and configuration of the peer device.

<a id="modify-tunnel"></a>
### Modify Tunnel { #modify-tunnel }

* Click **Modify** button to modify a tunnel.
    * All values except the gateway can be modified. If modified, the same values must also be updated on the peer VPN device.

<a id="stop-tunnel"></a>
### Stop Tunnel { #stop-tunnel }

* Click **Stop** button to stop a tunnel.
    * If the tunnel is stopped, private communication through the peer VPN device will be interrupted. 

<a id="delete-tunnel"></a>
### Delete Tunnel { #delete-tunnel }

* Click **Delete** button to delete a tunnel.

<a id="event"></a>
### Event { #event }

* You can search event logs generated when connecting a tunnel to the peer VPN device.

!!! tip "Note"

    * Only event logs for tunnels can be searched in Events.
    * For communication logs via VPN tunnel or audit logs such as tunnel creation and deletion, see the **Log** tab.