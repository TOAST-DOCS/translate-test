<!-- pre-align:aligned sig=1d1c35e9431e -->

<a id="network-service-gateway-service-endpoint"></a>
## Network > Service Gateway > 서비스 엔드포인트 { #network-service-gateway-service-endpoint }

서비스 게이트웨이를 이용하여 NHN Cloud 내부 네트워크로 통신할 수 있는 서비스 목록 및 각 서비스별 엔드포인트입니다.

<a id="region-code"></a>
### 리전 코드 { #region-code }

* 리전 서비스는 각 리전별로 엔드포인트 주소가 다르므로 `{region code}`에 아래의 리전 코드를 기입해야 합니다.

| 리전 | 리전 코드 |
| --- | ----- |
| 한국(판교) | kr1 |
| 한국(평촌) | kr2 |
| 한국(광주) | kr3 |
| 일본(도쿄) | jp1 |

<a id="service-gateway-integration-services"></a>
### 서비스 게이트웨이 연동 서비스 { #service-gateway-integration-services }

* 아래 서비스로 서비스 게이트웨이를 생성하면 인터넷을 경유하지 않고, NHN Cloud 내부 네트워크로 접근할 수 있습니다.
    * 서비스 게이트웨이를 생성하는 방법은 [Service Gateway > 콘솔 사용 가이드](/Network/Service%20Gateway/ko/console-guide/)를 참고하세요.
    * 아래 기재되지 않은 서비스는 [고객 센터](https://www.nhncloud.com/kr/support/inquiry)로 문의하세요.
* 서비스 게이트웨이를 생성할 수 있는 서비스 및 엔드포인트 주소입니다.
    * `/etc/hosts` 파일에 서비스 게이트웨이의 IP 주소와 접근하고자 하는 서비스 엔드포인트 주소를 추가해야 URL로 접속할 수 있습니다.
        * 예시) 192.168.1.42 kr1-api-object-storage.nhncloudservice.com

| 서비스 | 서비스 게이트웨이 엔드포인트 이름 | 엔드포인트 주소 |
| --- | ------------------ | -------- |
| [IaaS API Identity (nhncloudservice.com)](/Compute/Compute/ko/identity-api/#token) | IaaS API Identity (nhncloudservice.com) | https://api-identity-infrastructure.nhncloudservice.com |
| [IaaS API Key-Manager](/Network/Load%20Balancer/ko/public-api/) | IaaS API Key-Manager | https://{region code}-api-key-manager-infrastructure.nhncloudservice.com |
| [IaaS API Compute](/Compute/Instance/ko/public-api/) | IaaS API Compute | https://{region code}-api-instance-infrastructure.nhncloudservice.com |
| [IaaS API Network](/Network/VPC/ko/public-api/) | IaaS API Network | https://{region code}-api-network-infrastructure.nhncloudservice.com |
| [IaaS API Volume v2](/Storage/Block%20Storage/ko/public-api/) | IaaS API Volume v2 | https://{region code}-api-block-storage-infrastructure.nhncloudservice.com |
| [IaaS API Container - Infra](/Container/NKS/ko/public-api/) | IaaS API Container - Infra | https://{region code}-api-kubernetes-infrastructure.nhncloudservice.com |
| [NHN Container Registry(NCR)](/Container/NCR/ko/public-api) | NHN Container Registry(NCR)<br>API Gateway | 사용자 레지스트리 URI<br>https://{region code}-ncr.api.nhncloudservice.com |
| [NHN Container Service(NCS)](/Container/NCS/ko/public-api) | API Gateway | https://{region code}-ncs.api.nhncloudservice.com |
| [DNS Plus](/Network/DNS%20Plus/ko/api-guide/) | API Gateway | https://dnsplus.api.nhncloudservice.com |
| [Object Storage](/Storage/Object%20Storage/ko/api-guide/) | Object Storage | https://{region code}-api-object-storage.nhncloudservice.com |
| [RDS for MySQL](/Database/RDS%20for%20MySQL/ko/api-guide-v3.0/) | API Gateway | https://{region code}-rds-mysql.api.nhncloudservice.com |
| [RDS for PostgreSQL](/Database/RDS%20for%20PostgreSQL/ko/api-guide-v1.0/) | API Gateway | https://{region code}-rds-postgres.api.nhncloudservice.com |
| [RDS for MariaDB](/Database/RDS%20for%20MariaDB/ko/api-guide-v3.0/) | API Gateway | https://{region code}-rds-mariadb.api.nhncloudservice.com |
| [Server Security Check](/Security/Server%20Security%20Check/ko/Overview/) | Server Security Check | https://api-serversecuritycheck.nhncloudservice.com |
| [Security Monitoring](/Security/Security%20Monitoring/ko/api-guide-v1.1/) | API Gateway | https://{region code}-secmon.api.nhncloudservice.com |
| [Gamebase](/Game/Gamebase/ko/api-guide/) | API Gateway | https://api-gamebase.nhncloudservice.com|
| [Launching](/Game/Launching/ko/api-guide/) | API Gateway | https://launching.api.nhncloudservice.com |
| [CDN](/Contents%20Delivery/CDN/ko/api-guide-v2.0/) | API Gateway | https://cdn.api.nhncloudservice.com |
| [RCS Bizmessage](/Notification/RCS%20Bizmessage/ko/api-guide/) | API Gateway | https://rcs-bizmessage.api.nhncloudservice.com |
| [Email](/Notification/Email/ko/api-guide/) | API Gateway | https://email.api.nhncloudservice.com |
| [Face Recognition](/AI%20Service/Face%20Recognition/ko/api-guide-v2.0/) | API Gateway | https://face-recognition.api.nhncloudservice.com |
| [OCR](/AI%20Service/OCR/ko/general-ocr-api-guide/) | API Gateway | https://ocr.api.nhncloudservice.com |
| [Text to Speech](/AI%20Service/Text%20to%20Speech/ko/api-guide/) | API Gateway | https://speech.api.nhncloudservice.com |
| [Speech to Text](/AI%20Service/Speech%20to%20Text/ko/api-guide/) | API Gateway | https://speech.api.nhncloudservice.com |
| [Maps](/Application%20Service/Maps/ko/api-guide-v3.0/) | API Gateway | https://{region code}-maps.api.nhncloudservice.com |
| [ROLE](/Application%20Service/ROLE/ko/api-v3-guide/) | API Gateway | https://role.api.nhncloudservice.com |
| [API Gateway](/Application%20Service/API%20Gateway/ko/api-guide-v1.0/) | API Gateway | https://{region code}-apigateway.api.nhncloudservice.com |
| [Cloud Search](/Search/Cloud%20Search/ko/api-guide/api-v2.0-guide/) | API Gateway | https://{region code}-search.api.nhncloudservice.com |
| [Autocomplete](/Search/Autocomplete/ko/api-guide/api-v2.0-guide/) | API Gateway | https://{region code}-autocomplete.api.nhncloudservice.com |
| [Log & Crash Search](/Data%20&%20Analytics/Log%20&%20Crash%20Search/ko/api-guide/) | Log & Crash Search | http://api-logncrash.nhncloudservice.com |
| [Pipeline](/Dev%20Tools/Pipeline/ko/api-guide/) | API Gateway | https://{region code}-pipeline.api.nhncloudservice.com |
| [Certificate Manager](/Management/Certificate%20Manager/ko/api-guide-v1.1/) | API Gateway | https://certmanager.api.nhncloudservice.com |
| [Private CA](/Management/Private%20CA/ko/api-guide-v2.0/) | API Gateway | https://{region code}-pca.api.nhncloudservice.com |
| [CloudTrail](/Governance%20&%20Audit/CloudTrail/ko/api-guide/) | CloudTrail<br>API Gateway | https://cloud-trail.api.nhncloudservice.com |
| [Resource Watcher](/Governance%20&%20Audit/Resource%20Watcher/ko/api-v2-guide/) | API Gateway | https://resource-watcher.api.nhncloudservice.com | 
| [API Authentication](/nhncloud/ko/public-api/api-authentication/) |  API Gateway | https://oauth.api.nhncloudservice.com | 
| [Framework API](/nhncloud/ko/public-api/framework-api/) |  API Gateway | https://core.api.nhncloudservice.com | 
