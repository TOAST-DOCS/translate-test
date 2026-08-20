<!-- machine_translated: true -->

<!-- pre-align:aligned sig=109ab9c97015 -->

<a id="storage-storage-gateway-overview"></a>
## Storage > Storage Gateway > Overview { #storage-storage-gateway-overview }

Storage Gateway allows you to connect NHN Cloud storage from one or more cloud instances or on-premises devices to efficiently store and manage data.

> [Note]
> Storage Gateway is available in the Korea (Pangyo) region as of March 2025 and can be connected to Object Storage among NHN Cloud storage services.

<a id="characteristics"></a>
## Characteristics { #characteristics }
<a id="sharable"></a>
### Shareability { #sharable }
You can use NHN Cloud storage by mounting it on one or more instances or on-premises devices.
The supported protocols are NFS v3, v4 (Linux).

<a id="convenient"></a>
### Convenient { #convenient }
It provides an interface to mount NHN Cloud storage of various interfaces at the file level, so no additional file system configuration or API calls are required.

<a id="scalable"></a>
### Scalable { #scalable }
NHN Cloud storage is highly scalable, giving you the flexibility to grow your storage capacity as your data usage grows.

<a id="stable"></a>
### Stable { #stable }
With a redundant configuration, you'll have uninterrupted service in the event of a failure.

<a id="accessible"></a>
### Accessible { #accessible }
You can access NHN Cloud Storage from different environments by connecting a floating IP to the VPC network on the gateway or by setting up a network gateway.

<a id="secure"></a>
### Secure { #secure }
NHN Cloud storage utilizes server-side encryption to keep your data secure.

<a id="disaster-recovery"></a>
### Disaster Recovery { #disaster-recovery }
Disaster recovery settings in NHN Cloud Storage help you prepare for unexpected disasters.


<a id="terms"></a>
## Terms { #terms }
<a id="gateway"></a>
### Gateway { #gateway }
A cluster of instances that provides an interface to connect to NHN Cloud storage.
The gateway is created in a user project and can be configured for redundancy.

<a id="share"></a>
### Share { #share }
A setting to connect NHN Cloud storage.
You can set storage information, protocols, access permissions, ACLs, and more to connect.

