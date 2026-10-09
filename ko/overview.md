<!-- pre-align:aligned sig=70f5c107edf8 -->

<a id="storage-nas-for-bigdata-overview"></a>
## Storage > NAS for BigData > 개요 { #storage-nas-for-bigdata-overview }

NAS for BigData는 클라우드 환경에서 대용량 파일 스토리지를 간편하게 활용할 수 있는 완전 관리형 NAS(network-attached storage) 서비스입니다. 표준 NFS(network file system) 프로토콜을 기반으로 클라우드 인스턴스에서 쉽게 마운트할 수 있으며, 로컬 디스크처럼 데이터를 읽고 쓸 수 있습니다.

확장할 수 있는 대용량 스토리지를 제공하며, 인스턴스 간 파일 공유, 대규모 데이터 분석, 백업 등 다양한 업무에 유연하게 대응할 수 있습니다.

<a id="features"></a>
## 특징 { #features }

<a id="features.capacity"></a>
### 대용량 스토리지 제공 { #features.capacity }

대규모 데이터를 다루는 프로젝트에서도 물리 장비 증설 없이 콘솔에서 실시간으로 용량을 조정할 수 있어 운영 부담을 줄여 줍니다. 볼륨 크기 변경은 데이터 손실 없이 반영되며, 이러한 확장성과 탄력성을 바탕으로 유연하게 데이터를 관리할 수 있습니다.

<a id="features.sharing"></a>
### NFS 기반의 효율적인 파일 공유 { #features.sharing }

NFS 프로토콜을 지원해 인스턴스 간 파일 공유를 쉽고 빠르게 구현할 수 있습니다. 하나의 볼륨을 여러 서버에서 동시에 마운트할 수 있어, 멀티 노드 환경의 병렬 처리나 분산 작업에 적합합니다.

<a id="features.access_control"></a>
### 손쉬운 생성 및 유연한 접근 제어 { #features.access_control }

웹 콘솔에서 복잡한 설정 없이도 빠르게 파일 수준의 스토리지를 구성할 수 있습니다. 또한 Network ACL 서비스에서 IP 기반의 접근 제어 정책을 설정할 수 있어, 다수의 인스턴스가 연결된 환경에서도 보안성과 유연성을 동시에 확보할 수 있습니다.

<a id="glossary"></a>
## 용어 { #glossary }

<a id="glossary.NAS"></a>
### NAS { #glossary.NAS }

NAS는 네트워크로 접근할 수 있는 파일 기반 저장 장치입니다. 사용자는 NAS를 로컬 디스크처럼 마운트하여 파일을 저장하거나 불러올 수 있으며, 여러 서버 간 데이터 공유에 적합합니다. 접근 제어 등 기본적인 보안 기능도 함께 제공됩니다.

<a id="glossary.volume"></a>
### 볼륨 { #glossary.volume }

볼륨은 NAS의 논리적인 저장 공간으로, 인스턴스에 마운트하여 데이터를 저장하거나 읽을 수 있습니다.

<a id="glossary.snapshots"></a>
### 스냅숏 { #glossary.snapshots }

스냅숏(snapshot)은 볼륨의 특정 시점을 기준으로 생성한 읽기 전용 복사본입니다. 예기치 않은 데이터 손상이나 삭제가 발생했을 때, 해당 시점으로 데이터를 신속하게 복원할 수 있습니다.
자동 스냅숏 생성 주기를 설정할 수 있으며, 생성된 스냅숏은 저장 공간을 일부 사용합니다.
