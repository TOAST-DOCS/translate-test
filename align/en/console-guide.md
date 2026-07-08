## Network > Security Groups > Console User Guide

## Security Management Group

### Creating security groups
A default security group is created when the service is launched for the first time, and additional security groups can be created afterwards.
When a security group is created, a rule for all outgoing traffic is added unconditionally. This rule can be changed or deleted in the Security Group Rule Settings.
Even if the security group has been created, the rule will not be applied unless you set the security group for the instance.


### Create Security Rules
Create rules to apply to the security group. You can create multiple security rules for a single security group. If a security group is set for an instance, all security rules created in the security group are applied.

| Item        | Description                                                         |
| ----------- | ------------------------------------------------------------ |
| Direction        | Ingress means the direction into the instance. Egress means the direction going out of the instance. |
| Ether Type  | It means the version of the EtherType IP. IPv4 or IPv6 can be specified. |
| IP protocol | You can specify a specific protocol or specify all. Another protocol 0 means 'random', and it allows all IP protocols.       |
| Port range   | For L4 protocol, the port range can be specified.         |
| Remote        | You can specify a security group or IP address range. If the rule direction is 'egress', the destination is remote; if it is 'ingress', the source is remote. <br>The source and destination of traffic are compared in consideration of the rule direction. If you specify a security group, it compares whether the address is the IP address of an instance that belongs to the specified security group. <br>If you select CIDR to specify an IP address or range, it compares if the address is the configured IP address or range. |
| Description        | You can add description for security group rules.          |

### Create security rules in bulk
You can create up to 300 security group rules at once by writing the security group rules in the provided template file and uploading them.

> [Note]
> If you do not enter a port range when adding TCP, ICMP, or UDP protocols, the entire port range (ALL) will be applied.
> If you delete the description area (lines 1-8) of the bulk creation template, the upload will not be processed properly.
### Download the list of security rules
You can download a list of security rules set for a security group to a file.

### Applying security groups
If you select a security group when you create an instance, the security group is applied. Multiple security groups can be set on the instance. The rules of all set security groups are applied to the instance.
For example, if the security group 'CONN' has rules 'Ingress TCP PORT 22' and 'Ingress TCP PORT 23', and the security group 'WEB' has rules 'Ingress TCP PORT 80' and 'Ingress TCP PORT 8080', setting two security groups 'CONN' and 'WEB' on a single instance will apply all four rules, allowing you to use all of the services.
The security groups that were applied to the instance can be changed in the Instance Management menu. The identical security group can be applied to a number of instances. 

