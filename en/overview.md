## Network > Service Gateway > Overview

The **Service Gateway** service allows you to use the **services** of NHN Cloud outside the **VPC** without using a **floating IP** and having the traffic going through the internet. The **service** selected when **creating the service gateway** and the automatically assigned IP maintain a one-to-one relationship. In the **VPC**, you can use the target **service** safely through the NHN Cloud's internal network using the **service gateway**'s IP address.

### Main Features

* You can connect to the services of NHN Cloud provided by the service gateway from your VPC without going through the internet.
* You can use only the services provided in the service list when creating a service gateway.
* The IP address of the service gateway is connected one-to-one with the service selected when creating the service gateway.
* When the VM Instance in the VPC communicates with the IP address of the service gateway, it communicates with the service associated with the service gateway.
* This service is currently only available in the Korea (Pangyo) and Korea (Pyeongchon) regions, and will be supported by other regions gradually.

### Provided Services

If you need to access NHN Cloud's services from a VM Instance in the VPC without going through the internet, create a service gateway by selecting a service provided by the service gateway.
For details on how to use each service, refer to the [Service Gateway > Console User Guide](/Network/Service%20Gateway/en/console-guide/). 

For the services offered, see the [**Service Endpoints**](/Network/Service%20Gateway/ko/service-endpoint/). The services offered will be expanded.
