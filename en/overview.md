## Network > Service Gateway > Overview

The **Service Gateway** service allows you to use NHN Cloud **services** outside the **VPC** or **custom endpoints** published by other users without using a **floating IP** or routing traffic through the internet. The connection target selected when **creating a Service Gateway** and the automatically assigned IP maintain a one-to-one relationship. In the **VPC**, you can use the **Service Gateway**'s IP address to access the target securely through NHN Cloud's internal network.

### Main features

* You can connect to NHN Cloud services provided by the service gateway from a VPC without going through the internet.
* When creating a service gateway, you can select the connection type from **Service Endpoint** (services provided by NHN Cloud) or **Custom Endpoint** (resources published by other users).
* You can publish your own load balancer as a **custom endpoint** and share it with other projects by specifying the projects allowed to connect, enabling other projects to connect via a service gateway.
* Only the services listed in the service list when creating a service gateway are available.
* The IP address of the service gateway is linked one-to-one with the connection target selected when the service gateway was created.
* When a VM Instance in the VPC communicates with the IP address of the service gateway, it communicates with the target connected to the service gateway.
* Service Gateway is currently available in the Korea (Pangyo), Korea (Pyeongchon), and Korea (Gwangju) regions. Other regions will be supported gradually.
* However, custom endpoints are only supported in the Korea (Pangyo) and Korea (Pyeongchon) regions.

### Provided Services

If you need to access NHN Cloud services from a VM Instance in the VPC without going through the internet, create a service gateway by selecting a service provided by the service gateway.
For more information, see [Service Gateway > Console User Guide](/Network/Service%20Gateway/en/console-guide/).

For the list of available services, see [**Service Endpoints**](/Network/Service%20Gateway/en/service-endpoint/). The services provided will be expanded gradually.

### Custom Endpoint

In addition to the services provided by NHN Cloud, you can also connect to resources published by other users via a service gateway. Resource owners can publish their own load balancer as a custom endpoint, obtain a service name for sharing, and provide it to those allowed to connect. Consumers can then create and connect a service gateway using the provided service name.
For more information, see [Service Gateway > Console User Guide](/Network/Service%20Gateway/en/console-guide/).