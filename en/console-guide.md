<!-- machine_translated: true -->

<!-- pre-align:aligned sig=df549469ae0a -->

<a id="storage-storage-gateway-console-user-guide"></a>
## Storage > Storage Gateway > Console User Guide { #storage-storage-gateway-console-user-guide }

This document describes how to manage and connect gateways and shares in Storage Gateway from the NHN Cloud console.

<a id="gateway"></a>
## Gateway { #gateway }
<a id="create-gateway"></a>
### Create Gateway { #create-gateway }
Create a new storage gateway. The gateway is configured by creating an instance in your project. 

<a id="create-gateway-gateway-information"></a>
#### Gateway Information
Set the name, description, and type of storage to connect.

!!! tip "Note"
    As of March 2025, you can connect Object Storage.

<a id="create-gateway-cache-storage"></a>
#### Cache Storage
Set the size of storage to use as disk cache for the storage gateway. This is available as an SSD type and can be set to a minimum of 50 GB and a maximum of 2,048 GB.

<a id="create-gateway-network"></a>
#### Network
Select a VPC and subnet to use for the storage gateway.
A network interface is created on the instance that configures the gateway, and the interface is associated with the subnet of the selected VPC. For more information about creating and managing network resources, see the [VPC User Guide](/Network/VPC/en/overview/).
Service gateways are used to connect storage outside of your VPC, such as Object Storage, without going over the Internet. For more information about Service Gateway, see the [Service Gateway User Guide](/Network/Service%20Gateway/en/overview/).

<a id="create-gateway-floating-ip"></a>
#### Floating IP
Set whether to use a floating IP. Enabling a floating IP for the gateway makes it accessible from the Internet. For more information, see the [Floating IP user guide](/Network/Floating%20IP/en/overview/).

<a id="create-gateway-security-groups"></a>
#### Security Groups
Specify a security group to which the instance of the storage gateway belongs. To mount to NHN Cloud storage through the gateway from outside the selected VPC network, the security group must specify rules for the following ports.

| Direction | IP protocol | Port range | Ether | Remote |
| --- | --- | --- | --- | --- |
| Inbound | TCP | 111 | IPv4 | Remote destination IP |
| Inbound | TCP | 2049 | IPv4 | Remote destination IP |
| Inbound | TCP | 57861-57869 | IPv4 | Remote destination IP |

The remote destination IP can be set as a band in CIDR format. 

!!! danger "Caution"
    Setting the remote destination IP as a wide band, such as `0.0.0.0/0`, can lead to security vulnerabilities. Set it to a minimal range.

For more information, see the [Security Groups User Guide](/Network/Security%20Groups/en/overview/).

<a id="create-gateway-redundancy"></a>
#### Redundancy
Select whether to enable storage gateway redundancy.
With redundancy enabled, you create two instances to form a cluster. If one instance in the cluster fails, you can use the gateway without interruption through the other instance. The instance that fails and is excluded from the service is automatically recovered by the auto-healing feature and put back into the cluster.

<a id="start-gateway"></a>
### Start Gateway { #start-gateway }
Start a stopped storage gateway.

<a id="stop-gateway"></a>
### Stop Gateway { #stop-gateway }
Stop the storage gateway. When you stop the gateway, the instances that make up the cluster stop and can't connect to storage.

!!! danger "Caution"
    Before stopping the storage gateway, you must unmount the gateway from the system you are using by connecting the NHN Cloud storage. Stopping the gateway while it is mounted may cause problems on your system.

<a id="delete-gateway"></a>
### Delete Gateway { #delete-gateway }
Delete the storage gateway. All instances and resources that make up the cluster are deleted. NHN Cloud storage that was connected to the gateway is not deleted. 

!!! tip "Note"
    To delete a gateway, you must first delete all shares you created on the gateway.

<a id="share"></a>
## Share { #share }
<a id="create-share"></a>
### Create Share { #create-share }
Create a share. A share is a setup to connect NHN Cloud storage to. When you create a share, you get the mount connection information, which you can use to mount and use NHN Cloud storage on your system.

<a id="create-share-share-information"></a>
#### Share Information
Set the share name and protocol to use for the path to the mount connection information.

!!! tip "Note"
    As of March 2025, the NFS protocol is available.

<a id="create-share-storage-information-for-connection"></a>
#### Storage Information for Connection
Set the storage connection information.
Object Storage requires the container name to connect to and the Access Key from your S3 API credentials. The container name must follow Amazon S3's bucket naming conventions. S3 API credentials can be issued using the Object Storage console or API. For more information, see the [Create Bucket](/Storage/Object%20Storage/en/s3-api-guide/#bucket) and [S3 API Credentials](/Storage/Object%20Storage/en/s3-api-guide/#s3-api-credential) sections of **the Object Storage Amazon S3-compatible API guide**.

!!! tip "Note"
    When you create a share that connects Object Storage containers, the `{container name}+segments` container is automatically created in Object Storage. When you save a file that is larger than 25 MB through the gateway, it is uploaded as a multipart to the connected container, and the segment objects of the multipart object are stored in the `{containername}+segments` container.

<!-- 개행을 위한 주석 -->

!!! danger "Caution"
    To set IP ACLs on containers in Object Storage that you want to connect to, you must add **Allow Read/Write** for Service Gateway.

The user who issues Object Storage's S3 API credentials needs **read/write** permissions on the container to connect to.

If you delete the container or delete the S3 API credentials while connecting to and using a container in Object Storage through a storage gateway, it can cause problems on your system. You should be careful not to delete them.

If you delete objects in the `{container name}+segments` container while connecting to and using a container in Object Storage through a storage gateway, you will not be able to access the files you have stored. Be careful not to delete them.

<a id="create-share-nfs-permissions-settings"></a>
#### NFS Permissions Settings
Set permissions for clients to connect over the NFS protocol.

| Squash Option | Description |
| --- | --- |
| `no_root_squash` | Map the root of the client to the root of the NFS server. |
| `root_squash` | Map the root of the client to nobody or the UID/GID you specify. |
| `all_squash` | Maps all users on the client to nobody or the UID/GID you specify. |

If you do not enter a user ID and group ID, they are set to **root(0)** or **nobody(65534)**, depending on your Squash options. To map to other users and groups, enter the Linux user ID and group ID. The Linux user ID and group ID can be found with the `id` command in the Linux shell.

```
$ id
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu)
```

<a id="create-share-access-control-acl"></a>
#### Access Control (ACL)
Enter the IP or IP band of the client that can access NHN Cloud storage through the gateway in CIDR format.

<a id="create-share-cache-settings"></a>
#### Cache Settings
Set the memory cache validity time. The cache is retained for the set validity time.

<a id="delete-share"></a>
### Delete Share { #delete-share }
Delete a share. 

!!! danger "Caution"
    Before deleting a share, you must mount the NHN Cloud storage and unmount it from your system. Deleting a share while it is mounted may cause problems on your system.

<a id="immediately-empty-cache"></a>
### Immediately Empty Cache { #immediately-empty-cache }
Immediately deletes data stored in the disk cache area. 

<a id="change-access-key"></a>
### Change Access Key { #change-access-key }
Change the Access Key that you set when creating the share for the Object Storage type gateway.

!!! danger "Caution"
    Before you change the access key, you must mount your NHN Cloud storage and unmount it from your system. Changing the Access Key while mounted may cause problems on your system.

<a id="change-nfs-permissions"></a>
### Change NFS Permissions { #change-nfs-permissions }
Change the permissions of clients to connect over the NFS protocol.

<a id="change-access-control-acl"></a>
### Change Access Control (ACL) { #change-access-control-acl }
Change the IP or IP band of clients that can access NHN Cloud storage through the gateway.

<a id="connect-nfs"></a>
## Connect NFS { #connect-nfs }
To use NFS, you must install the NFS package and run the rpcbind service, as follows

<a id="install-nfs-package"></a>
### Install NFS Package { #install-nfs-package }
* **Debian, Ubuntu**
```
sudo apt-get install nfs-common rpcbind
```

* **CentOS**
```
sudo yum install nfs-utils rpcbind
```

<a id="run-rpcbind-service"></a>
### Run rpcbind Service { #run-rpcbind-service }
```
sudo service rpcbind start
```

<a id="mount-share"></a>
### Mount Share { #mount-share }
Using the mount connection information of the created share and the mount command, you can mount NHN Cloud storage to your system as follows.

```
sudo mount -t nfs {Mount share information} {Path to mount}
```

To use NFS v3, you must add the version option as follows

```
sudo mount -t nfs -o vers=3 {Mount share information} {Path to mount}
```

* Mount share information can be found in the details of the share.
Example: 192.168.0.11:/data

* Path to mount
Example: /mnt/data


<a id="posix-api"></a>
## POSIX API { #posix-api }
Gateways of type Object Storage support only a subset of the POSIX APIs.

<a id="supported-apis"></a>
### Supported APIs { #supported-apis }
```
read, write, readdir, truncate, fallocate, fsync
```

!!! danger "Caution"
    Do not use rename, hardlink, or symlink; they may not work or may create unintended objects in Object Storage.
    We do not recommend using tools that save to temporary files and then rename them, such as rsync and vi.

