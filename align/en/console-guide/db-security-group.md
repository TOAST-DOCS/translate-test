# DB Security Group

**Database > EasyCache > Console User Guide > DB Security Group**

DB Security Group is used to protect caches and nodes by collectively controlling inbound and outbound traffic of nodes belonging to a cache. A positive security model is used, which allows traffic specified by rules and blocks all other traffic. If a DB Security Group is not attached to a cache, all inbound and outbound traffic is blocked. Even if a DB Security Group is created, its rules are not applied unless it is attached to a cache. Multiple DB Security Groups can be applied to a cache. The main features of DB Security Group are as follows:

* Because DB Security Group operates in a stateful manner, sessions established by a DB security rule are allowed even if there is no rule in the opposite direction.
* For example, if the first packet of TCP 3306 destined for a node passes through according to the "Inbound TCP PORT 3306" rule, packets sent from the node using TCP port 3306 as the source are not blocked.
* However, if no packets matching the rule arrive for a certain period of time and the session expires, packets in the opposite direction are also blocked.
* Specifying a range for DB security rules is more efficient than adding them one by one. Increasing the number of DB security rules may cause performance degradation.
Traffic with mismatched session states may be blocked.

DB Security Group consists of a name, a description, and multiple DB security rules. The name of DB Security Group has the following constraints:

* DB Security Group names can only contain between 1 and 100 uppercase and lowercase English letters, numbers, and certain symbols (-, \_, .). The first character must be an English letter.

### Apply DB Security Group
You can select a DB Security Group to apply when creating a cache. All nodes in the cache are affected by the selected DB Security Group. Multiple DB Security Groups can be applied to a cache. The rules of all applied DB Security Groups are applied to the cache. You can freely modify the selection on the Modify Cache screen.

## DB Security Rule
You can create multiple DB security rules in a single DB Security Group. When a DB Security Group is configured for a cache, all DB security rules created in that DB Security Group are applied to all nodes belonging to the cache.

| Item | Description |
| - | - |
| Direction | Inbound refers to traffic flowing into nodes belonging to a cache. Outbound refers to traffic flowing out of nodes belonging to a cache. |
| Port | Set the port to which the rule applies. You can select Port, Port Range, Service Port, or TLS Service Port. If Service Port or TLS Service Port is selected, the port value is set according to the cache information associated with the DB Security Group. |
| Ether | The version of the EtherType IP. You can specify IPv4 or IPv6. |
| Remote | You can specify an IP address range. If the rule direction is Outbound, the destination is the remote. If the direction is Inbound, the source is the remote. Depending on the rule direction, the source and destination of the traffic are compared against the configured IP address or range. |
| Description | You can add a description of the DB Security Group rule. |

### Change DB Security Rule
When changes are made, such as creating, modifying, or deleting DB security rules, the changes are applied sequentially to the caches associated with the DB Security Group and to the nodes that belong to the caches. You cannot add new DB security rules to a DB Security Group, or modify or delete other DB security rules, until the changes have been applied to all caches and nodes associated with the DB Security Group.