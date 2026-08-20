<!-- machine_translated: true -->

<!-- pre-align:aligned sig=1d1c35e9431e -->

<a id="network-service-gateway-service-endpoint"></a>
## Network > Service Gateway > 連動サービスエンドポイント { #network-service-gateway-service-endpoint }

サービスゲートウェイを利用してNHN Cloudの内部ネットワークと通信できるサービスリスト及び各サービスのエンドポイントです。

<a id="region-code"></a>
### リージョンコード { #region-code }

* リージョンサービスはリージョンごとにエンドポイントアドレスが異なるため、`{region code}`に下記のリージョンコードを記入する必要があります。

| リージョン | リージョンコード |
| --- | ----- |
| 韓国(パンギョ) | kr1 |
| 韓国(ピョンチョン) | kr2 |
| 韓国(光州) | kr3 |
| 日本(東京) | jp1 |

<a id="service-gateway-integration-services"></a>
### サービスゲートウェイ連動サービス { #service-gateway-integration-services }

* 下記のサービスでサービスゲートウェイを作成すると、インターネットを経由せず、NHN Cloud内部ネットワークにアクセスできます。
    * サービスゲートを作成する方法は[Service Gateway > コンソール使用ガイド](/Network/Service%20Gateway/jp/console-guide/)をご参照ください。
    * 下記に記載されていないサービスについては、[サポート](https://www.nhncloud.com/kr/support/inquiry)にお問い合わせください。
* サービスゲートウェイを作成できるサービスおよびエンドポイントアドレスです。
    * `/etc/hosts`ファイルにサービスゲートウェイのIPアドレスとアクセスしたいサービスエンドポイントアドレスを追加するとURLで接続できます。
        * 例) <span style="color:rgb(68, 68, 68);">192</span><span style="color:rgb(136, 0, 0);" class="hljs-selector-class">.168.1.42</span><span style="color:rgb(68, 68, 68);"> </span><span style="color:rgb(68, 68, 68);" class="hljs-selector-tag">kr1-api-object-storage</span><span style="color:rgb(136, 0, 0);" class="hljs-selector-class">.nhncloudservice.com</span>

| サービス | サービスゲートウェイエンドポイント名前</span> | エンドポイントアドレス |
| --- | ------------------ | -------- |
| [IaaS API Identity (nhncloudservice.com)](/Compute/Compute/jp/identity-api/#token) | IaaS API Identity (nhncloudservice.com) | https://api-identity-infrastructure.nhncloudservice.com |
| [IaaS API Key-Manager](/Network/Load%20Balancer/jp/public-api/) | IaaS API Key-Manager | https://{region code}-api-key-manager-infrastructure.nhncloudservice.com |
| [IaaS API Compute](/Compute/Instance/jp/public-api/) | IaaS API Compute | https://{region code}-api-instance-infrastructure.nhncloudservice.com |
| [IaaS API Network](/Network/VPC/jp/public-api/) | IaaS API Network | https://{region code}-api-network-infrastructure.nhncloudservice.com |
| [IaaS API Volume v2](/Storage/Block%20Storage/jp/public-api/) | IaaS API Volume v2 | https://{region code}-api-block-storage-infrastructure.nhncloudservice.com |
| [IaaS API Container - Infra](/Container/NKS/jp/public-api/) | IaaS API Container - Infra | https://{region code}-api-kubernetes-infrastructure.nhncloudservice.com |
| [NHN Container Registry(NCR)](/Container/NCR/jp/public-api) | NHN Container Registry(NCR)<br>API Gateway | ユーザーレジストリURI<br>https://{region code}-ncr.api.nhncloudservice.com |
| [NHN Container Service(NCS)](/Container/NCS/jp/public-api) | API Gateway | https://{region code}-ncs.api.nhncloudservice.com |
| [DNS Plus](/Network/DNS%20Plus/jp/api-guide/) | API Gateway | https://dnsplus.api.nhncloudservice.com |
| [Object Storage](/Storage/Object%20Storage/jp/api-guide/) | Object Storage | https://{region code}-api-object-storage.nhncloudservice.com |
| [RDS for MySQL](/Database/RDS%20for%20MySQL/jp/api-guide-v3.0/) | API Gateway | https://{region code}-rds-mysql.api.nhncloudservice.com |
| [RDS for PostgreSQL](/Database/RDS%20for%20PostgreSQL/jp/api-guide-v1.0/) | API Gateway | https://{region code}-rds-postgres.api.nhncloudservice.com |
| [RDS for MariaDB](/Database/RDS%20for%20MariaDB/jp/api-guide-v3.0/) | API Gateway | https://{region code}-rds-mariadb.api.nhncloudservice.com |
| [Server Security Check](/Security/Server%20Security%20Check/jp/Overview/) | Server Security Check | https://api-serversecuritycheck.nhncloudservice.com |
| [Security Monitoring](/Security/Security%20Monitoring/jp/api-guide-v1.1/) | API Gateway | https://{region code}-secmon.api.nhncloudservice.com |
| [Gamebase](/Game/Gamebase/jp/api-guide/) | API Gateway | https://api-gamebase.nhncloudservice.com|
| [Launching](/Game/Launching/jp/api-guide/) | API Gateway | https://launching.api.nhncloudservice.com |
| [CDN](/Contents%20Delivery/CDN/jp/api-guide-v2.0/) | API Gateway | https://cdn.api.nhncloudservice.com |
| [RCS Bizmessage](/Notification/RCS%20Bizmessage/jp/api-guide/) | API Gateway | https://rcs-bizmessage.api.nhncloudservice.com |
| [Email](/Notification/Email/jp/api-guide/) | API Gateway | https://email.api.nhncloudservice.com |
| [Face Recognition](/AI%20Service/Face%20Recognition/jp/api-guide-v2.0/) | API Gateway | https://face-recognition.api.nhncloudservice.com |
| [OCR](/AI%20Service/OCR/jp/general-ocr-api-guide/) | API Gateway | https://ocr.api.nhncloudservice.com |
| [Text to Speech](/AI%20Service/Text%20to%20Speech/jp/api-guide/) | API Gateway | https://speech.api.nhncloudservice.com |
| [Speech to Text](/AI%20Service/Speech%20to%20Text/jp/api-guide/) | API Gateway | https://speech.api.nhncloudservice.com |
| [Maps](/Application%20Service/Maps/jp/api-guide-v3.0/) | API Gateway | https://{region code}-maps.api.nhncloudservice.com |
| [ROLE](/Application%20Service/ROLE/jp/api-v3-guide/) | API Gateway | https://role.api.nhncloudservice.com |
| [API Gateway](/Application%20Service/API%20Gateway/jp/api-guide-v1.0/) | API Gateway | https://{region code}-apigateway.api.nhncloudservice.com |
| [Cloud Search](/Search/Cloud%20Search/jp/api-guide/api-v2.0-guide/) | API Gateway | https://{region code}-search.api.nhncloudservice.com |
| [Autocomplete](/Search/Autocomplete/jp/api-guide/api-v2.0-guide/) | API Gateway | https://{region code}-autocomplete.api.nhncloudservice.com |
| [Log & Crash Search](/Data%20&%20Analytics/Log%20&%20Crash%20Search/jp/api-guide/) | Log & Crash Search | http://api-logncrash.nhncloudservice.com |
| [Pipeline](/Dev%20Tools/Pipeline/jp/api-guide/) | API Gateway | https://{region code}-pipeline.api.nhncloudservice.com |
| [Certificate Manager](/Management/Certificate%20Manager/jp/api-guide-v1.1/) | API Gateway | https://certmanager.api.nhncloudservice.com |
| [Private CA](/Management/Private%20CA/jp/api-guide-v2.0/) | API Gateway | https://{region code}-pca.api.nhncloudservice.com |
| [CloudTrail](/Governance%20&%20Audit/CloudTrail/jp/api-guide/) | CloudTrail<br>API Gateway | https://cloud-trail.api.nhncloudservice.com |
| [Resource Watcher](/Governance%20&%20Audit/Resource%20Watcher/jp/api-v2-guide/) | API Gateway | https://resource-watcher.api.nhncloudservice.com | 
| [API Authentication](/nhncloud/ja/public-api/api-authentication/) |  API Gateway | https://oauth.api.nhncloudservice.com | 
| [Framework API](/nhncloud/ja/public-api/framework-api/) |  API Gateway | https://core.api.nhncloudservice.com |

