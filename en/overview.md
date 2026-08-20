<!-- machine_translated: true -->

<!-- pre-align:aligned sig=9381b37cc171 -->

<a id="network-service-gateway-overview"></a>
## Network > Service Gateway > Overview { #network-service-gateway-overview }

The Service Gateway service allows you to use the NHN Cloud services outside the VPC or **custom endpoints** published by other users without using a floating IP and having the traffic go through the internet. The connection target selected when **creating the Service Gateway** and the automatically assigned IP maintain a one-to-one relationship. In the VPC, you can use the Service Gateway's IP address to access the target safely through NHN Cloud's internal network.

<a id="main-features"></a>
### Main Features { #main-features }

* You can connect to the services of NHN Cloud provided by the service gateway from your VPC without going through the internet.
* When creating a service gateway, you can choose the connection type: **service endpoint** (services provided by NHN Cloud) or **custom endpoint** (resources published by other users).
* You can publish your own load balancer as a custom endpoint, specify the projects that are allowed to connect, and share it so that other projects can connect via a service gateway.
* Only the services listed in the service list when creating a service gateway are available.
* The IP address of a service gateway is matched one-to-one to the connection target selected when the service gateway is created.
* When an instance in the VPC communicates with the IP address of the service gateway, it communicates with the target associated with the service gateway.
* The service gateway is currently available in the Korea (Pangyo), Korea (Pyeongchon), and Korea (Gwangju) regions. Other regions will be supported gradually.
* However, custom endpoints are supported only in the Korea (Pangyo) and Korea (Pyeongchon) regions.

<a id="provided-services"></a>
### Provided Services { #provided-services }

If you need to access NHN Cloud's services from a VM Instance in the VPC without going through the internet, create a service gateway by selecting a service provided by the service gateway.
For details on how to use each service, refer to [Service Gateway > Console User Guide](/Network/Service%20Gateway/en/console-guide/).

For the list of provided services, refer to [**Service Endpoint**](/Network/Service%20Gateway/en/service-endpoint/). The services provided will be expanded gradually.

<a id="custom-endpoints"></a>
### Custom Endpoints { #custom-endpoints }

In addition to the services provided by NHN Cloud, you can also connect via a service gateway to resources published by other users. The resource owner publishes their own load balancer as a custom endpoint, receives a service name for sharing, and delivers it to the intended consumers. The consumer then creates a service gateway using the received service name to establish a connection.
For details on how to use each service, refer to [Service Gateway > Console User Guide](/Network/Service%20Gateway/en/console-guide/).