## Database > EasyCache > Overview

NHN Cloud EasyCache is a service that provides Valkey or Redis (REmote DIctionary Server) in a cloud environment.
You can use a highly available in-memory cache server with simple settings.

## Characteristics and Features

* To use EasyCache, you must activate the Compute & Network service.

### Replication Group

* A group of in-memory cache servers that can be created instantly when you want.
* You can use management features.
* You can use replication group securely using certificates.

### Monitoring

* You can view the measurements to monitor the cache performance of the server in graphs.

### Backup

* You can perform automatic backup of memory data at specified time, once per day.
* You can perform manual backup of memory data instantly at the time you want.
* The data is stored in safe external storage.
* Using the stored backup data, a new replication group can be created at any time.

### Profile Configuration

* You can manage the configuration of Valkey and Redis servers with profiles.
* You can configure a default profile or a user profile.

### Alarm

* You can get notification on the event and monitoring status of replication groups.
* You can manage the events and threshold settings for monitoring.

### Event

* You can search for and check the status of replication groups and nodes.

## Glossary 

### Replication Group

* A replication group is provided as Standalone and Replication types.
* Server specification supports 2-64 GB memory.
* You can create a replication group with virtual devices of all specifications provided by the Compute & Network service of NHN Cloud.
* You cannot access the operating system of a replication group directly. You can access a Valkey server using the assigned domain and the port that you entered when creating a replication group.
* You can create a replication group only when you select VPC subnet in the Compute & Network service, and you can communicate with the instance of the Compute & Network service through VPC subnet.
* A replication group is disconnected from external networks, except for the user's subnet. If connection from an external network is required, floating IP must be attached.
* If you are using the Compute & Network service, you can configure a subnet for connection when you create a replication group.
* Network connection is enabled between the replication group and the instance in the connected subnet.
* A master is a general instance that allows read and write operations. 
* A replica is an instance that replicates a master in real time.

### Availability Zone

* A logical area where a replication group is created.

### Floating IP

* A dynamic IP used for communication with external networks.
* To use a floating IP, an internet gateway must be associated with the user's VPC subnet attached to the instance to be configured.
* The Valkey of instance associated with a floating IP is accessible from external network through a public domain.
* You will be charged for a floating IP as soon as it is created, apart from Valkey instances.

### High Availability (Automatic HA)

* If you use the HA feature, the service monitors the master of replication group, detects failure, and performs failover automatically. This feature can reduce the service downtime as much as possible.

