<!-- pre-align:aligned sig=d29522461c5f -->

<a id="container-nhn-container-servicencs-release-notes"></a>
## Container > NHN Container Service(NCS) > 릴리스 노트 { #container-nhn-container-servicencs-release-notes }
<a id="october-28-2025"></a>
### 2025. 10. 28. { #october-28-2025 }
<a id="october-28-2025-added-features"></a>
#### 기능 추가
* 워크로드에서 사용하는 컨테이너 이미지에 대해 악성 코드 검사 수행 기능이 추가되었습니다.

<a id="march-4-2025"></a>
### 2025. 03. 04. { #march-4-2025 }
<a id="march-4-2025-added-features"></a>
#### 기능 추가
* 워크로드 생성 시 내부 요청 응답 대기 시간 항목이 추가되었습니다. 내부 요청 응답 대기 시간 설정을 통해 다른 워크로드의 내부 로드 밸런서 VIP로 통신 요청 시 타임 아웃을 적용할 수 있습니다.

<a id="november-26-2024"></a>
### 2024. 11. 26. { #november-26-2024 }
<a id="november-26-2024-added-features"></a>
#### 기능 추가
* 컨테이너에 접근할 수 있는 웹 터미널 기능이 추가되었습니다.
* 워크로드 오토스케일링 기능이 추가되었습니다.
* 워크로드 작업별 재시작 기능이 추가되었습니다.
* NCS를 위한 Public API가 공개되었습니다.
    * Public API에 대한 내용은 [API 가이드](/Container/NCS/ko/public-api/)를 참고하세요.

<a id="august-27-2024"></a>
### 2024. 08. 27. { #august-27-2024 }
<a id="august-27-2024-added-features"></a>
#### 기능 추가
* NCS에서 발생한 이벤트를 Resource Watcher에서 확인할 수 있습니다.

<a id="may-28-2024"></a>
### 2024. 05. 28. { #may-28-2024 }
<a id="may-28-2024-added-features"></a>
#### 기능 추가
* 워크로드 작업 종료 시간을 예약 설정할 수 있습니다.
* 템플릿 버전 관리 기능이 추가되었습니다.
* 초기화 컨테이너 기능이 추가되었습니다.
* 이벤트 조회 기간이 30일로 상향되었습니다.
* HostAliases를 설정할 수 있습니다.

<a id="february-27-2024"></a>
### 2024. 02. 27. { #february-27-2024 }
<a id="february-27-2024-added-features"></a>
#### 기능 추가
* 컨테이너 인자(Args) 설정 기능이 추가되었습니다.
* 워크로드 배포 컨트롤러 선택 기능이 추가되었습니다.
* 내부 로드 밸런서 기능이 추가되었습니다.
* 워크로드의 Private DNS 연동 기능이 추가되었습니다.

<a id="february-27-2024-feature-updates"></a>
#### 기능 개선
* 컨테이너 간 임시 공유 스토리지가 제공됩니다.

<a id="november-28-2023"></a>
### 2023. 11. 28. { #november-28-2023 }
<a id="november-28-2023-added-features"></a>
#### 기능 추가
* 컨테이너 설정 기능들이 추가되었습니다.
    * DNS 서버 주소 설정
    * 상태 점검(LivenessProbe, StartupProbe) 설정
    * 수명 주기 훅(Lifecycle Hook) 설정
    * 컨피그맵 설정
    * 시크릿 설정
    * NAS 컨테이너 연결 경로 설정
* GPU와 임시 스토리지 모니터링 기능이 추가되었습니다.
* 워크로드 생성 시 보안 그룹을 선택할 수 있습니다.
* NCS에서 발생한 이벤트를 NHN CloudTrail에서 확인할 수 있습니다.

<a id="november-28-2023-feature-updates"></a>
#### 기능 개선
* Load Balancer가 제공됩니다.
    * Load Balancer Instance는 더 이상 지원하지 않습니다.
* 컨테이너 포트에 HTTPS, TERMINATED_HTTPS 프로토콜이 추가되었습니다.
* 로그 탭이 개선되었습니다.
* 컨테이너의 현재와 마지막 상태에 대한 상세 이유를 이벤트 탭에서 확인할 수 있도록 개선되었습니다.

<a id="august-29-2023"></a>
### 2023. 08. 29. { #august-29-2023 }
<a id="august-29-2023-added-features"></a>
#### 기능 추가
* 워크로드 예약 기능을 추가하였습니다.
* 워크로드 중지/재시작 기능을 추가하였습니다.

<a id="august-29-2023-feature-updates"></a>
#### 기능 개선
* NAS 스토리지 연결 실패 원인을 이벤트 탭에서 확인할 수 있도록 개선되었습니다.

<a id="july-25-2023"></a>
### 2023. 07. 25. { #july-25-2023 }
<a id="july-25-2023-feature-updates"></a>
#### 기능 개선
* 컨테이너의 최대 리소스 사이즈가 상향되었습니다.

<a id="may-30-2023"></a>
### 2023. 05. 30. { #may-30-2023 }
<a id="may-30-2023-feature-updates"></a>
#### 기능 개선
* GPU 타입을 선택할 수 있는 기능이 추가되었습니다.
* 컨테이너 포트에 HTTP 프로토콜이 추가되었습니다.
* Quota 기능이 추가되었습니다.

<a id="march-28-2023"></a>
### 2023. 03. 28. { #march-28-2023 }

<a id="march-28-2023-feature-updates"></a>
#### 기능 개선
* 내부 구조를 개선해 서비스의 안정성을 향상했습니다.

<a id="added-features"></a>
### 2023. 02. 28. { #added-features }

<a id="added-features-2"></a>
#### 기능 추가
* 권한 세분화 기능을 추가하였습니다.
* 워크로드 변경 기능을 추가하였습니다.

<a id="january-31-2023"></a>
### 2023. 01. 31. { #january-31-2023 }

<a id="january-31-2023-added-features"></a>
#### 기능 추가
* 모니터링 기능을 추가하였습니다.

<a id="december-27-2022"></a>
### 2022. 12. 27. { #december-27-2022 }

<a id="december-27-2022-release-of-a-new-service"></a>
#### 신규 서비스 출시
* 콘솔에서 컨테이너를 생성하고 관리할 수 있습니다.
