## Storage > Storage Gateway > Overview

Storage Gateway allows you to connect NHN Cloud storage from one or more cloud instances or on-premises devices to efficiently store and manage data.

> [Note]
> Storage Gateway is available in the Korea (Pangyo) region as of March 2025 and can be connected to Object Storage among NHN Cloud storage services.

## Characteristics
### Sharable
You can use NHN Cloud storage by mounting it on one or more instances or on-premises devices.
The supported protocols are NFS v3, v4 (Linux).

### Convenient
It provides an interface to mount NHN Cloud storage of various interfaces at the file level, so no additional file system configuration or API calls are required.

### Scalable
NHN Cloud storage is highly scalable, giving you the flexibility to grow your storage capacity as your data usage grows.

### Stable
With a redundant configuration, you'll have uninterrupted service in the event of a failure.

### Accessible
You can access NHN Cloud Storage from different environments by connecting a floating IP to the VPC network on the gateway or by setting up a network gateway.

### Secure
NHN Cloud storage utilizes server-side encryption to keep your data secure.

### Disaster Recovery
Disaster recovery settings in NHN Cloud Storage help you prepare for unexpected disasters.


## Terms
### Gateway
A cluster of instances that provides an interface to connect to NHN Cloud storage.
The gateway is created in a user project and can be configured for redundancy.

### Share
A setting to connect NHN Cloud storage.
You can set storage information, protocols, access permissions, ACLs, and more to connect.

