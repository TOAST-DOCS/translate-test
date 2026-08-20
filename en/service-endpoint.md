<!-- machine_translated: true -->

<!-- pre-align:aligned sig=1d1c35e9431e -->

<a id="network-service-gateway-service-endpoint"></a>
## Network > Service Gateway > Service Endpoint { #network-service-gateway-service-endpoint }

A list of services that can communicate with the NHN Cloud internal network using Service Gateway and the endpoints for each service.

<a id="region-code"></a>
### Region Code { #region-code }

* Region services have different endpoint addresses for each region, so you must fill in the region code below `{region code}`.

| Region | Region Code |
| --- | ----- |
| Korea (Pangyo) | kr1 |
| Korea (Pyeongchon) | kr2 |
| Korea (Gwangju) | kr3 |
| Japan (Tokyo) | jp1 |

<a id="service-gateway-integration-services"></a>
### Service Gateway Integration Services { #service-gateway-integration-services }

* By creating a service gateway with the services below, you can access the internal network of NHN Cloud without going through the Internet.
    * To create a service gateway, see the [Service Gateway > Console User Guide](/Network/Service%20Gateway/en/console-guide/).
    * For services not listed below, contact [Customer Center](https://www.nhncloud.com/kr/support/inquiry).
* The service and endpoint addresses for which you can create a service gateway.
    * In the `/etc/hosts` file, you must add the IP address of the service gateway and the service endpoint address you want to access to the URL.
        * Example) 192.168.1.42 kr1-api-object-storage.nhncloudservice.com

| Service | Service Gateway endpoint name | Endpoint address |
| --- | ------------------ | -------- |
| [IaaS API Identity (nhncloudservice.com)](/Compute/Compute/en/identity-api/#token) | IaaS API Identity (nhncloudservice.com) | https://api-identity-infrastructure.nhncloudservice.com |
| [IaaS API Key-Manager](/Network/Load%20Balancer/en/public-api/) | IaaS API Key-Manager | https://{region code}-api-key-manager-infrastructure.nhncloudservice.com |
| [IaaS API Compute](/Compute/Instance/en/public-api/) | IaaS API Compute | https://{region code}-api-instance-infrastructure.nhncloudservice.com |
| [IaaS API Network](/Network/VPC/en/public-api/) | IaaS API Network | https://{region code}-api-network-infrastructure.nhncloudservice.com |
| [IaaS API Volume v2](/Storage/Block%20Storage/en/public-api/) | IaaS API Volume v2 | https://{region code}-api-block-storage-infrastructure.nhncloudservice.com |
| [IaaS API Container - Infra](/Container/NKS/en/public-api/) | IaaS API Container - Infra | https://{region code}-api-kubernetes-infrastructure.nhncloudservice.com |
| [NHN Container Registry(NCR)](/Container/NCR/en/public-api) | NHN Container Registry(NCR)<br>API Gateway | User registry URI<br>https://{region code}-ncr.api.nhncloudservice.com |
| [NHN Container Service(NCS)](/Container/NCS/en/public-api) | API Gateway | https://{region code}-ncs.api.nhncloudservice.com |
| [DNS Plus](/Network/DNS%20Plus/en/api-guide/) | API Gateway | https://dnsplus.api.nhncloudservice.com |
| [Object Storage](/Storage/Object%20Storage/en/api-guide/) | Object Storage | https://{region code}-api-object-storage.nhncloudservice.com |
| [RDS for MySQL](/Database/RDS%20for%20MySQL/en/api-guide-v3.0/) | API Gateway | https://{region code}-rds-mysql.api.nhncloudservice.com |
| [RDS for PostgreSQL](/Database/RDS%20for%20PostgreSQL/en/api-guide-v1.0/) | API Gateway | https://{region code}-rds-postgres.api.nhncloudservice.com |
| [RDS for MariaDB](/Database/RDS%20for%20MariaDB/en/api-guide-v3.0/) | API Gateway | https://{region code}-rds-mariadb.api.nhncloudservice.com |
| [Server Security Check](/Security/Server%20Security%20Check/en/Overview/) | Server Security Check | https://api-serversecuritycheck.nhncloudservice.com |
| [Security Monitoring](/Security/Security%20Monitoring/en/api-guide-v1.1/) | API Gateway | https://{region code}-secmon.api.nhncloudservice.com |
| [Gamebase](/Game/Gamebase/en/api-guide/) | API Gateway | https://api-gamebase.nhncloudservice.com|
| [Launching](/Game/Launching/en/api-guide/) | API Gateway | https://launching.api.nhncloudservice.com |
| [CDN](/Contents%20Delivery/CDN/en/api-guide-v2.0/) | API Gateway | https://cdn.api.nhncloudservice.com |
| [RCS Bizmessage](/Notification/RCS%20Bizmessage/en/api-guide/) | API Gateway | https://rcs-bizmessage.api.nhncloudservice.com |
| [Email](/Notification/Email/en/api-guide/) | API Gateway | https://email.api.nhncloudservice.com |
| [Face Recognition](/AI%20Service/Face%20Recognition/en/api-guide-v2.0/) | API Gateway | https://face-recognition.api.nhncloudservice.com |
| [OCR](/AI%20Service/OCR/en/general-ocr-api-guide/) | API Gateway | https://ocr.api.nhncloudservice.com |
| [Text to Speech](/AI%20Service/Text%20to%20Speech/en/api-guide/) | API Gateway | https://speech.api.nhncloudservice.com |
| [Speech to Text](/AI%20Service/Speech%20to%20Text/en/api-guide/) | API Gateway | https://speech.api.nhncloudservice.com |
| [Maps](/Application%20Service/Maps/en/api-guide-v3.0/) | API Gateway | https://{region code}-maps.api.nhncloudservice.com |
| [ROLE](/Application%20Service/ROLE/en/api-v3-guide/) | API Gateway | https://role.api.nhncloudservice.com |
| [API Gateway](/Application%20Service/API%20Gateway/en/api-guide-v1.0/) | API Gateway | https://{region code}-apigateway.api.nhncloudservice.com |
| [Cloud Search](/Search/Cloud%20Search/en/api-guide/api-v2.0-guide/) | API Gateway | https://{region code}-search.api.nhncloudservice.com |
| [Autocomplete](/Search/Autocomplete/en/api-guide/api-v2.0-guide/) | API Gateway | https://{region code}-autocomplete.api.nhncloudservice.com |
| [Log & Crash Search](/Data%20&%20Analytics/Log%20&%20Crash%20Search/en/api-guide/) | Log & Crash Search | http://api-logncrash.nhncloudservice.com |
| [Pipeline](/Dev%20Tools/Pipeline/en/api-guide/) | API Gateway | https://{region code}-pipeline.api.nhncloudservice.com |
| [Certificate Manager](/Management/Certificate%20Manager/en/api-guide-v1.1/) | API Gateway | https://certmanager.api.nhncloudservice.com |
| [Private CA](/Management/Private%20CA/en/api-guide-v2.0/) | API Gateway | https://{region code}-pca.api.nhncloudservice.com |
| [CloudTrail](/Governance%20&%20Audit/CloudTrail/en/api-guide/) | CloudTrail<br>API Gateway | https://cloud-trail.api.nhncloudservice.com |
| [Resource Watcher](/Governance%20&%20Audit/Resource%20Watcher/en/api-v2-guide/) | API Gateway | https://resource-watcher.api.nhncloudservice.com | 
| [API Authentication](/nhncloud/en/public-api/api-authentication/) |  API Gateway | https://oauth.api.nhncloudservice.com | 
| [Framework API](/nhncloud/en/public-api/framework-api/) |  API Gateway | https://core.api.nhncloudservice.com |
