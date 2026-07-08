## Network > Security Groups > Overview

A security group is used to control the incoming and outgoing traffic of an instance to protect the instance. It uses a 'positive security model', where traffic specified by the rule is allowed and the rest of the traffic is blocked.

### Key Features
* When you start a service for the first time, a default security group is created and all incoming traffic is blocked.
    * Therefore, services such as 'ping' and 'ssh' cannot be used until necessary rules are set.
    * The same applies to both of external access using a floating IP and internal access using a private IP.
* The security group operates in a 'stateful' manner, so the session connected with the rule once will be allowed even if it does not have a rule for the opposite direction.
    * For example, if the first packet of the TCP 80 port destined for an instance was passed according to 'Ingress TCP PORT 80' rule, the packet sent with the TCP 80 port set as the source will not be blocked.
    * But if the session expires because the packet satisfying the rules does not come in for a certain period of time, the packet in the opposite direction is blocked as well.
* In the default security group, the rules for all outgoing traffic have been set. If you do not delete this rule, all sessions that start from the instance will be allowed.
* In the instance, multiple security groups can be set.
* It is more efficient to set the range rather than to add a rule one by one. If the number of rules increases, it may lead to performance degradation.
* Traffic with an inconsistent session state can be blocked.
* You can define and use rules that are not in the IP protocol list. 

