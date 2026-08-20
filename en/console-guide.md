<!-- machine_translated: true -->

{% include-markdown '../_nas-for-big-data-vars.md' %}

<!-- pre-align:aligned sig=d48e0cc2304b -->

<a id="storage-nas-for-bigdata-console-user-guide"></a>
## Storage > NAS for BigData > Console User Guide { #storage-nas-for-bigdata-console-user-guide }

This document describes how to manage NAS for BigData volumes and snapshots and connect them to instances in the NHN Cloud console.

<a id="volume"></a>
## Volume { #volume }
A volume is a logical storage space in NAS that can be mounted on an instance to store or read data.

<a id="create_volume"></a>
### Create a Volume { #create_volume }

Creates a new volume. The created volume can be accessed from instances by using the network file system (NFS) protocol.

| Item | Description |
| --- | --- |
| Name | Name of the volume to be created. The NFS access path is created using the volume name. The volume name is limited to up to 100 characters, including letters, numbers, and some symbols (-, _). |
| Description | Description of the volume. |
| VPC | The virtual private cloud (VPC) to access the volume. |
| Subnet | The subnet to access the volume. Only subnets in the selected VPC can be chosen. |
| Size | Size of the volume to be created. It can be entered from a minimum of $[ min_size ]$ to a maximum of $[ max_size ]$. |
| Access Control List (ACL) | Access control lists (ACLs) can be configured in the Network ACL service. For more information, see the [Network ACL service user guide]($[ network_acl_guide_url ]$). |
| Auto Create Snapshot | A snapshot is automatically created according to the configured cycle. When the configured limit is exceeded, the oldest snapshots are automatically deleted first. |

<a id="delete_volume"></a>
### Delete a Volume { #delete_volume }

Deletes a volume.

!!! danger "Caution"
    It is recommended to unmount the volume from connected instances before deleting it. Deleting a volume while it is still mounted may cause issues on the user system.

If you delete a volume, all data, including snapshots, is deleted. Data cannot be recovered after deletion.

<a id="change_volume_size"></a>
### Change a Volume Size { #change_volume_size }

Changes the size of a volume. The size can be changed even while the volume is in use.

<a id="change_acl"></a>
### Change Access Control Settings { #change_acl }

Access control lists (ACLs) can be configured in the Network ACL service. For more information, see the [Network ACL service user guide]($[ network_acl_guide_url ]$).

<a id="snapshots"></a>
## Snapshot { #snapshots }
A snapshot is a read-only copy that saves the state of a volume at a specific point in time. Snapshots can be used to restore a volume to the state it was in at the time the snapshot was created.

| Item | Description |
| --- | --- |
| Name | Name of the snapshot. If created by the system, the name is determined according to specified rules. |
| Created at | The date and time when the snapshot was created. |

<a id="snapshots.create"></a>
### Create a Snapshot Immediately { #snapshots.create }

Creates a snapshot immediately. The name is limited to up to 32 characters, including letters, numbers, and some symbols (-, \_, .). Each snapshot must have a unique name within the volume.

<a id="snapshots.restore"></a>
### Restore a Snapshot { #snapshots.restore }

Restores the volume to the point in time when the snapshot was created. Contact [customer support]($[ support_url ]$) to restore the snapshot.

<a id="snapshots.delete"></a>
### Delete a Snapshot { #snapshots.delete }

Deletes the specified snapshot. Deleted snapshots cannot be recovered.

<a id="connect_volume"></a>
## Connect to Volume { #connect_volume }

The created volume can be mounted on an instance using the connection information. However, the instance to be mounted must be connected to the same subnet as the volume.

<a id="connect_volume.nfs"></a>
### Install NFS Package { #connect_volume.nfs }

<a id="connect_volume.nfs-debian-ubuntu"></a>
#### Debian, Ubuntu

```
sudo apt-get install nfs-common rpcbind
```

<br>

<a id="connect_volume.nfs-rocky"></a>
#### Rocky

```
sudo dnf install nfs-utils rpcbind
```

<br>

<a id="connect_volume.rpcbind"></a>
### Run rpcbind Service { #connect_volume.rpcbind }

```
sudo service rpcbind start
```

<br>

<a id="connect_volume.mount"></a>
### Volume Mount { #connect_volume.mount }

```
sudo mount -t nfs <nas-source> <mount-point>
```

| Item | Description |
| --- | --- |
| &lt;nas-source&gt; | Connection path of the volume (`NFS server address:export path`)<br>Example: 192.168.0.11:/GJ\_SHARE\_FS8/bacb62d4-f271-44ad-a5d2-505d21037b45 |
| &lt;mount-point&gt; | Directory to mount the volume<br>Example: /mnt |
