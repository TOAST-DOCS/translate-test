<!-- pre-align:aligned sig=9381b37cc171 -->

<a id="network-service-gateway-overview"></a>
## Network > Service Gateway > Overview { #network-service-gateway-overview }

The Service Gateway service allows you to use NHN Cloud services outside the VPC or **custom endpoints** published by other users without using a floating IP and having the traffic go through the internet. The connection target selected when **creating the Service Gateway** and the automatically assigned IP maintain a one-to-one relationship. In the VPC, you can use the Service Gateway's IP address to access the target safely through NHN Cloud's internal network.

<a id="main-features"></a>
### Main Features { #main-features }

* You can connect to the services of NHN Cloud provided by the service gateway from your VPC without going through the internet.
* When creating a service gateway, you can choose the connection type between **Service Endpoint** (services provided by NHN Cloud) or **Custom Endpoint** (resources published by other users).
* You can publish your own load balancer as a custom endpoint, specify the projects that are allowed to connect, and share it so that other projects can connect via a service gateway.
* You can use only the services provided in the service list when creating a service gateway.
* The IP address of the service gateway is connected one-to-one with the connection target selected when creating the service gateway.
* When an instance in the VPC communicates with the IP address of the service gateway, it communicates with the target associated with the service gateway.
* The service gateway is currently available in the Korea (Pangyo), Korea (Pyeongchon), and Korea (Gwangju) regions. Support will be expanded to other regions gradually.
* However, the custom endpoint is supported only in the Korea (Pangyo) and Korea (Pyeongchon) regions.

<a id="provided-services"></a>
### Provided Services { #provided-services }

If you need to access NHN Cloud's services from a VM Instance in the VPC without going through the internet, create a service gateway by selecting a service provided by the service gateway.
For more information, see [Service Gateway > Console User Guide](/Network/Service%20Gateway/en/console-guide/).

For the services offered, see the [**Service Endpoints**](/Network/Service%20Gateway/en/service-endpoint/). The services offered will be expanded.

<a id="custom-endpoints"></a>
### Custom Endpoints { #custom-endpoints }

In addition to services provided by NHN Cloud, you can use a service gateway to connect to resources published by other users. The resource owner publishes their load balancer as a custom endpoint, obtains a service name for sharing, and delivers it to the intended consumers. Consumers then create a service gateway using the provided service name to establish a connection.
For more information, see [Service Gateway > Console User Guide](/Network/Service%20Gateway/en/console-guide/).
