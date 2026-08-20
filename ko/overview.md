<!-- pre-align:aligned sig=9381b37cc171 -->

<a id="network-service-gateway-overview"></a>
## Network > Service Gateway > 개요 { #network-service-gateway-overview }

Service Gateway 서비스를 이용하면 플로팅 IP를 쓰지 않고 트래픽이 인터넷을 경유하지 않고도 VPC 외부의 NHN Cloud의 서비스나 다른 사용자가 게시한 **사용자 정의 엔드포인트**를 이용할 수 있습니다. **서비스 게이트웨이 생성** 시 선택된 연결 대상과 자동으로 할당된 IP는 1:1 연결 관계를 유지하며, VPC에서는 서비스 게이트웨이의 IP를 이용하여 NHN Cloud의 내부 네트워크를 경유해 대상을 안전하게 이용할 수 있습니다.

<a id="main-features"></a>
### 주요 기능 { #main-features }

* VPC에서 인터넷을 경유하지 않고 서비스 게이트웨이에서 제공하는 NHN Cloud의 서비스에 연결할 수 있습니다.
* 서비스 게이트웨이 생성 시 연결 유형을 **서비스 엔드포인트**(NHN Cloud가 제공하는 서비스) 또는 **사용자 정의 엔드포인트**(다른 사용자가 게시한 리소스) 중에서 선택할 수 있습니다.
* 자신의 로드 밸런서를 사용자 정의 엔드포인트로 게시하고, 연결을 허용할 프로젝트를 지정하여 다른 프로젝트가 서비스 게이트웨이로 연결하도록 공유할 수 있습니다.
* 서비스 게이트웨이 생성 시 서비스 목록에 제공되는 서비스만 이용이 가능합니다.
* 서비스 게이트웨이의 IP 주소는 서비스 게이트웨이 생성 시 선택된 연결 대상과 1:1로 연결됩니다.
* VPC의 인스턴스에서에서 서비스 게이트웨이의 IP 주소로 통신 시 서비스 게이트웨이와 연결된 대상과 통신됩니다.
* 서비스 게이트웨이는 현재 한국(판교), 한국(평촌), 한국(광주) 리전에서 제공됩니다. 점차 다른 리전도 지원할 예정입니다.
* 단, 사용자 정의 엔드포인트는 한국(판교), 한국(평촌) 리전에서만 지원합니다.

<a id="provided-services"></a>
### 제공 서비스 { #provided-services }

VPC의 VM Instance에서 인터넷을 경유하지 않고 NHN Cloud의 서비스에 접근이 필요한 경우 서비스 게이트웨이에서 제공되는 서비스를 선택하여 서비스 게이트웨이를 생성합니다.
자세한 사용 방법은 [Service Gateway > 콘솔 사용 가이드](/Network/Service%20Gateway/ko/console-guide/)를 참고하세요.

제공 서비스는 [**서비스 엔드포인트**](/Network/Service%20Gateway/ko/service-endpoint/)를 참고하세요. 제공되는 서비스는 점차 확대될 예정입니다.

<a id="custom-endpoints"></a>
### 사용자 정의 엔드포인트 { #custom-endpoints }

NHN Cloud가 제공하는 서비스 외에, 다른 사용자가 게시한 리소스에도 서비스 게이트웨이로 연결할 수 있습니다. 리소스 소유자는 자신의 로드 밸런서를 사용자 정의 엔드포인트로 게시하고 공유용 서비스 이름을 발급받아 연결을 허용할 대상에게 전달하며, 소비자는 전달받은 서비스 이름으로 서비스 게이트웨이를 생성하여 연결합니다.
자세한 사용 방법은 [Service Gateway > 콘솔 사용 가이드](/Network/Service%20Gateway/ko/console-guide/)를 참고하세요.
