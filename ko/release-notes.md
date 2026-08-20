<!-- pre-align:aligned sig=263cd1eadb32 -->

<a id="security-secure-key-manager-release-notes"></a>
## Security > Secure Key Manager > 릴리스 노트 { #security-secure-key-manager-release-notes }

<a id="june-9-2026"></a>
### 2026. 06. 09. { #june-9-2026 }
<a id="june-9-2026-added-features"></a>
#### 신규 기능 추가
  * 키 저장소 생성/수정/삭제 API 추가(v1.3)
    * API를 이용하여 키 저장소를 생성, 수정, 삭제할 수 있는 기능 추가. 자세한 내용은 [API v1.3 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.3/)를 참고.

<a id="may-27-2026"></a>
### 2026. 05. 27. { #may-27-2026 }
<a id="may-27-2026-added-features"></a>
#### 신규 기능 추가
  * 비대칭 키 표준 스킴 서명/검증 API 추가(v1.3)
    * 표준 RSA 서명 스킴(RSASSA-PSS, RSASSA-PKCS1-v1_5)에 따라 비대칭 키로 데이터를 서명하고 검증할 수 있는 API 추가. 자세한 내용은 [API v1.3 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.3/)를 참고.
<a id="may-27-2026-feature-updates"></a>
#### 기능 개선/변경
  * 키 저장소 인증 방식 결합 옵션 추가
    * 키 저장소에 활성화된 여러 인증 방법(IPv4 주소, MAC 주소, 클라이언트 인증서)을 결합하는 방식을 선택할 수 있는 기능 추가. 모두 통과(AND, 기본값) 또는 하나만 통과(OR) 중 선택할 수 있으며, 기존 키 저장소는 모두 통과(AND)로 유지됩니다. 자세한 내용은 [콘솔 사용 가이드](/Security/Secure%20Key%20Manager/ko/console-guide/)를 참고.

<a id="april-14-2026"></a>
### 2026. 04. 14. { #april-14-2026 }
<a id="april-14-2026-feature-updates"></a>
#### 기능 개선/변경
  * `APPROVAL MEMBER` 역할 삭제
    * Secure Key Manager APPROVAL MEMBER 역할을 Secure Key Manager ADMIN 역할로 마이그레이션하여 역할 체계 단순화
  * 권한 세분화
    * `SecureKeyManager:API.ADMIN`, `SecureKeyManager:API.VIEWER` 권한을 추가하여 콘솔 및 API 권한을 세분화하여 관리하도록 변경

<a id="march-10-2026"></a>
### 2026. 03. 10. { #march-10-2026 }
<a id="march-10-2026-added-features"></a>
#### 신규 기능 추가
  * API v1.3 추가
    * `X-NHN-AUTHORIZATION` 헤더를 통한 토큰 인증 방식 추가. 자세한 내용은 [API v1.3 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.3/)를 참고.
  * 기밀 데이터 수정 API 추가(v1.2, v1.3)
    * API를 이용하여 Secure Key Manager에 저장한 기밀 데이터를 수정할 수 있는 기능 추가. 자세한 내용은 [API v1.2 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.2/) 또는 [API v1.3 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.3/)를 참고.

<a id="february-10-2026"></a>
### 2026. 02. 10. { #february-10-2026 }
<a id="february-10-2026-new-features"></a>
#### 신규 기능 추가
  * 키 저장소 목록 상세 조회 API 추가
    * API를 이용하여 키 저장소의 상세 정보 목록을 조회할 수 있는 기능 추가. 자세한 내용은 [API v1.0 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.0/) 또는 [API v1.2 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.2/)를 참고.
  * 키 목록 상세 조회 API 추가
    * API를 이용하여 키의 상세 정보 목록을 조회할 수 있는 기능 추가. 자세한 내용은 [API v1.0 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.0/) 또는 [API v1.2 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.2/)를 참고.

<a id="june-24-2025"></a>
### 2025. 06. 24. { #june-24-2025 }
<a id="june-24-2025-feature-updates"></a>
#### 기능 개선/변경
  * 신규 오류 메시지 추가
    * 유효하지 않은 URI로 API 요청 시 오류 메시지 추가. 자세한 내용은 [문제 해결 가이드](/Security/Secure%20Key%20Manager/ko/troubleshooting-guide/#api-call-failure-returns-url-not-found-error-message)를 참고.

<a id="april-28-2025"></a>
### 2025. 04. 28. { #april-28-2025 }
<a id="april-28-2025-feature-updates"></a>
#### 기능 개선/변경
  * 데이터 보관 기한이 3년에서 1년으로 변경
    * [관련 공지](https://www.nhncloud.com/kr/support/notice/detail/6493)

<a id="march-25-2025"></a>
### 2025. 03. 25. { #march-25-2025 }
<a id="march-25-2025-added-new-features"></a>
#### 신규 기능 추가
  * 키 저장소 목록/상세 조회 API 추가
    * API를 이용하여 키 저장소의 ID 목록 및 키 저장소 ID를 통해 키 저장소를 상세 조회할 수 있는 기능 추가
  * 키 목록/상세 조회 API 추가
    * API를 이용하여 키 ID 목록 및 키 ID를 통해 키를 상세 조회할 수 있는 기능 추가
  * 인증 정보 목록/상세 조회 API 추가
    * API를 이용하여 인증 정보의 값 목록 및 인증 정보의 값을 통해 인증 정보를 상세 조회할 수 있는 기능 추가

<a id="september-25-2024"></a>
### 2024. 09. 25. { #september-25-2024 }
<a id="september-25-2024-feature-updates"></a>
#### 기능 개선/변경
  * 승인리스트의 표에서 Number 열 삭제

<a id="august-27-2024"></a>
### 2024. 08. 27. { #august-27-2024 }
<a id="august-27-2024-added-new-features"></a>
#### 신규 기능 추가
  * Secure Key Manager의 이벤트 알림을 Resource Watcher 서비스에서 받을 수 있는 기능 추가
<a id="august-27-2024-feature-updates"></a>
#### 기능 개선/변경
  * 승인 프로세스 자가 승인 기능 제거
    * 본인이 요청한 건에 대해 승인을 하지 못하도록 변경

<a id="april-23-2024"></a>
### 2024. 04. 23. { #april-23-2024 }
<a id="april-23-2024-bug-fixes"></a>
#### 버그 수정
  * API를 이용해 데이터(키, 인증 정보)를 삭제하고 삭제된 데이터를 조회하는 경우, 오류 모달창 노출 후 새로고침 이전까지는 삭제하지 않은 데이터도 조회할 수 없는 오류 수정

<a id="march-26-2024"></a>
### 2024. 03. 26. { #march-26-2024 }
<a id="march-26-2024-added-new-features"></a>
#### 신규 기능 추가
  * 인증 정보 등록/삭제 API 추가
    * API를 이용해 키를 사용하기 위한 인증 정보를 등록하거나 삭제할 수 있는 기능 추가
    * API를 이용해 인증 정보를 추가하거나 삭제하려면 **User Access Key ID**와 **Secret Access Key** 필요. 자세한 내용은 [User Access Key](/nhncloud/ko/public-api/user-access-key)를 참고.

<a id="february-27-2024"></a>
### 2024. 02. 27. { #february-27-2024 }
<a id="february-27-2024-added-new-features"></a>
#### 신규 기능 추가
  * 알림 메일 수신 대상 설정 기능 추가
    * 조직/프로젝트 대시보드 > 알림 관리에서 수신 메일 주소명을 설정할 수 있도록 기능이 추가되었습니다.
<a id="february-27-2024-feature-updates"></a>
#### 기능 개선/변경
  * 키 저장소 ID 노출
    * 키 저장소 상세 정보에서 키 저장소 ID를 확인할 수 있는 영역 노출
    * 키 저장소 ID 우측 더보기 버튼을 통해 키 저장소 ID를 복사할 수 있는 기능 추가

<a id="november-28-2023"></a>
### 2023. 11. 28. { #november-28-2023 }
<a id="november-28-2023-added-new-features"></a>
#### 신규 기능 추가
  * 키 추가/삭제 API 추가
    * API를 이용해 키를 추가하거나 삭제할 수 있는 기능 추가
    * API를 이용해 키를 추가하거나 삭제하려면 **User Access Key ID**와 **Secret Access Key** 필요. 자세한 내용은 [User Access Key](/nhncloud/ko/public-api/user-access-key)를 참고.

<a id="september-26-2023"></a>
### 2023. 09. 26. { #september-26-2023 }
<a id="september-26-2023-feature-updates"></a>
#### 기능 개선/변경
  * IPv4 대역폭 인증 기능 추가
    * IPv4로 인증 시 CIDR 표기법을 통한 대역폭 인증 기능 추가

<a id="july-25-2023"></a>
### 2023. 07. 25. { #july-25-2023 }
<a id="july-25-2023-bug-fixes"></a>
#### 버그 수정
  * 승인 프로세스 인증서 취소 기능 오류 수정
    * 승인 프로세스에서 **사용 중** 상태의 인증서에 대해 삭제를 요청한 뒤 요청을 취소할 때 원래의 **사용 중** 상태가 아닌 **삭제 취소 예정** 상태로 표시되는 오류 수정

<a id="may-30-2023"></a>
### 2023. 05. 30. { #may-30-2023 }
<a id="may-30-2023-bug-fixes"></a>
#### 버그 수정
  * 승인 프로세스 알림(메일) 기능 오류 수정
    * 승인 권한을 가진 일부 관리자가 알림(메일)을 받지 못하는 오류 수정
  * 승인 프로세스 IP/MAC 대용량 등록 기능 오류 수정
    * 승인 프로세스 IP/MAC 대용량 등록 시 화면에 즉시 반영되지 않는 오류 수정

<a id="april-25-2023"></a>
### 2023. 04. 25. { #april-25-2023 }
<a id="april-25-2023-added-new-features"></a>
#### 신규 기능 추가
  * 승인 프로세스 알림(메일) 기능 추가
    * 승인 요청 등록 시 승인 권한을 가진 관리자에게 메일을 전송하는 기능 추가

<a id="february-28-2023"></a>
### 2023. 02. 28. { #february-28-2023 }
<a id="february-28-2023-bug-fixes"></a>
#### 버그 수정
  * 템플릿 파일 다운로드 오류 수정
    * 대량 등록 템플릿 파일이 잘못된 형태의 템플릿으로 다운로드되는 오류 수정

<a id="january-31-2023"></a>
### 2023. 01. 31. { #january-31-2023 }
<a id="january-31-2023-bug-fixes"></a>
#### 버그 수정
  * 승인 기능 개선 및 오류 수정
    * 승인 기능 사용 중 기밀 데이터 수정 화면에 진입 시 데이터 영역이 빈 칸으로 표시되도록 수정
    * 승인 기능 사용 중 기밀 데이터를 수정한 뒤 수정된 데이터가 표시되도록 수정
  * 키 저장소 관리 탭에서 MAC 주소의 툴팁 문구에 MAC 주소가 아닌 IPv4로 표시되는 문제 수정

<a id="december-27-2022"></a>
### 2022. 12. 27. { #december-27-2022 }
<a id="december-27-2022-feature-updates"></a>
#### 기능 개선/변경
  * API 도메인 변경
    * SecureKeyManager API 도메인을 `api-keymanager.cloud.toast.com`에서 `api-keymanager.nhncloudservice.com`으로 수정

<a id="november-29-2022"></a>
### 2022. 11. 29. { #november-29-2022 }
<a id="november-29-2022-bug-fixes"></a>
#### 버그 수정
  * 승인 기능 개선 및 오류 수정
    * 승인 기능 사용 중 발생하는 오류 메시지의 문구를 이해하기 쉽도록 개선
    * 승인 기능 사용 중 키 저장소를 최초로 추가할 때 승인 절차 없이 추가가 진행되는 오류 수정
  * 인증서 인증 오류 수정
    * 인증서로 인증할 때 간헐적으로 실패하는 문제 수정

<a id="october-25-2022"></a>
### 2022. 10. 25. { #october-25-2022 }
<a id="october-25-2022-bug-fixes"></a>
#### 버그 수정
  * 통합 앱키 오류 수정
    * 프로젝트 통합 앱키를 이용한 API 호출이 제대로 동작하지 않는 문제 수정
  * 승인 기능 오류 수정
    * 승인 기능 사용 시 키 버전별 삭제 기능이 제대로 동작하지 않는 문제 수정

<a id="september-27-2022"></a>
### 2022. 09. 27. { #september-27-2022 }
<a id="september-27-2022-added-new-features"></a>
#### 신규 기능 추가
  * 비대칭키 조회 기능 추가
    * 키 버전별 비대칭키 조회 기능 추가

<a id="july-26-2022"></a>
### 2022. 07. 26. { #july-26-2022 }
<a id="july-26-2022-added-new-features"></a>
#### 신규 기능 추가
  * 승인 기능 추가
    * 키 생성, 수정, 삭제 및 키 저장소에 대한 접근 제어 변경 등 주요 변경 사항에 대한 승인 절차 도입 가능
  * 새로운 대칭키 조회 버전 추가
    * 키 버전별 대칭키 조회 기능 추가

<a id="november-23-2021"></a>
### 2021. 11. 23. { #november-23-2021 }
<a id="november-23-2021-added-new-features"></a>
#### 신규 기능 추가
  * 대칭키 조회 기능 추가

<a id="october-26-2021"></a>
### 2021. 10. 26. { #october-26-2021 }
<a id="october-26-2021-added-new-features"></a>
#### 신규 기능 추가
  * 키 가져오기 기능 추가
    * 대칭키 가져오기 기능 추가
<a id="october-26-2021-feature-updates"></a>
#### 기능 개선/변경
  * 기밀 데이터 조회 기능 수정
    * 웹 콘솔에서 기밀 데이터 조회 시 필드를 마스킹하여 제공
<a id="october-26-2021-bug-fixes"></a>
#### 버그 수정
  * 미납 사용자인데도 정상적으로 서비스를 이용할 수 있었던 문제 수정

<a id="september-28-2021"></a>
### 2021. 09. 28. { #september-28-2021 }
<a id="september-28-2021-bug-fixes"></a>
#### 버그 수정
  * 권한 그룹을 이용해 부여한 권한일 경우, 인식이 제대로 되지 않던 문제 해결
  * 사용 내역 초기화 버튼이 제대로 동작하지 않던 문제 수정

<a id="march-24-2020"></a>
### 2020. 03. 24. { #march-24-2020 }
<a id="march-24-2020-added-new-features"></a>
#### 신규 기능 추가
  * 사용자가 Secure Key Manager 콘솔에서 작업한 내용을 Cloud Trail에 기록
  * CSV 파일을 사용한 인증 데이터(IPv4 주소/MAC 주소) 대량 등록 기능 추가
  * CSV 파일을 사용한 인증 데이터(IPv4 주소/MAC 주소) 다운로드 기능 추가

<a id="december-24-2019"></a>
### 2019. 12. 24. { #december-24-2019 }
<a id="december-24-2019-added-new-features"></a>
#### 신규 기능 추가
  * 통계 화면 추가
    * 프로젝트 단위로 API 사용 통계를 조회할 수 있는 화면 추가
<a id="december-24-2019-feature-updates"></a>
#### 기능 개선/변경
  * 키 저장소 화면 개선
    * 키 저장소 목록의 표시 방식 변경
    * 키 저장소의 하위 메뉴 변경
    * 키 저장소에 퀵 메뉴 추가
  * 사용 내역 화면 개선
    * 프로젝트 단위로 API 사용 내역을 조회할 수 있게 변경

<a id="july-23-2019"></a>
### 2019. 07. 23. { #july-23-2019 }
<a id="july-23-2019-feature-updates"></a>
#### 기능 개선/변경
  * UI 개선
    * 텍스트와 버튼을 겹쳐서 표시하는 현상 수정
    * 일본어로 화면을 표시할 때 텍스트 줄 바뀜 현상 수정

<a id="may-28-2019"></a>
### 2019. 05. 28. { #may-28-2019 }
<a id="may-28-2019-release-of-new-service"></a>
#### 신규 서비스 출시
  * 기밀 데이터, 대칭 키, 비대칭 키와 같이 애플리케이션 서버에 저장할 경우 보안 위험에 노출될 수 있는 데이터를 중앙 집중적으로 안전하게 관리하고, 인증을 통과한 클라이언트만 접근할 수 있게 제어하는 서비스입니다.
