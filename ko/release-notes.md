<!-- pre-align:aligned sig=39caf24ddae0 -->

<a id="management-certificate-manager-release-notes"></a>
## Management > Certificate Manager > 릴리스 노트 { #management-certificate-manager-release-notes }

<a id="july-28-2026"></a>
### 2026. 07. 28. { #july-28-2026 }
<a id="july-28-2026-feature-updates"></a>
#### 기능 개선
* Certificate Manager API v1.3 인증서 목록 조회 API의 응답에 인증서 ID가 추가되었습니다.
* Certificate Manager API v1.3에 인증서 ID를 이용한 인증서 다운로드 API가 추가되었습니다.
    * 자세한 내용은 [API v1.3 가이드](/Management/Certificate%20Manager/ko/api-guide-v1.3)에서 확인할 수 있습니다.
* 알림 그룹 > 수신 그룹이 **알림 수신 그룹 관리**로 마이그레이션되었습니다.

<a id="april-14-2026"></a>
### 2026. 04. 14. { #april-14-2026 }
<a id="april-14-2026-api-v11-authentication-and-permission-updates"></a>
#### API v1.1 인증 및 권한 수정
* Certificate Manager API v1.1 가이드의 인증 및 권한 정보가 수정되었습니다.
    * API 사용을 위해 **Certificate Manager ADMIN 역할** 또는 **Certificate Manager VIEWER 역할**이 필요합니다.
    * 자세한 내용은 [API v1.1 가이드](/Management/Certificate%20Manager/ko/api-guide-v1.1)에서 확인할 수 있습니다.

<a id="march-10-2026"></a>
### 2026. 03. 10. { #march-10-2026 }
<a id="march-10-2026-added-a-api-version"></a>
#### API 버전 추가
* 토큰 인증 방식을 지원하는 Certificate Manager API v1.3이 추가되었습니다.
  <br> 자세한 내용은 API v1.3 가이드에서 확인할 수 있습니다.

<a id="november-25-2025"></a>
### 2025. 11. 25. { #november-25-2025 }
<a id="november-25-2025-feature-updates"></a>
#### 기능 개선
* 인증서 이름 제약이 변경되어, 구 인증서와 신규 인증서를 함께 관리할 수 있습니다.
    * 인증서 이름이 인증서 파일의 CN(CommonName) 값과 동일하지 않아도 되며, 프로젝트 내에서 유일한 이름이면 등록할 수 있습니다.
* 인증서의 Domains [CN(CommonName) + SAN(SubjectAlternativeNames)] 항목이 추가되었습니다.
    * Domains 정보는 인증서 파일 업로드 시 자동으로 수집됩니다.
* 인증서 타입(Single, Wildcard, SAN)이 제거되었습니다.
* 인증서 목록 및 상세 정보 UI가 변경되었습니다.
* 자세한 내용은 [콘솔 사용 가이드](/Management/Certificate%20Manager/ko/console-guide/)에서 확인할 수 있습니다.

<a id="march-26-2024"></a>
### 2024. 03. 26. { #march-26-2024 }
<a id="march-26-2024-add-a-new-api-version"></a>
#### API 버전 추가
* Certificate Manager의 API v1.1이 추가되었습니다. <br>자세한 내용은 API v1.1 가이드에서 확인할 수 있습니다.

<a id="february-27-2024"></a>
### 2024. 02. 27. { #february-27-2024 }
<a id="february-27-2024-added-the-feature-to-set-who-receives-notification-emails"></a>
#### 알림 메일 수신 대상 설정 기능 추가
* 조직/프로젝트 대시보드 > 알림 관리에서 수신 메일 주소명을 설정할 수 있도록 기능이 추가되었습니다.

<a id="march-28-2023"></a>
### 2023. 03. 28. { #march-28-2023 }
<a id="march-28-2023-feature-updates"></a>
#### 기능 개선
* 인증서 등록 시 선택한 파일이 인증서 파일(.pem)이 아닐 경우 `인증서 파일은 '.pem' 확장자 파일만 업로드할 수 있습니다.` 메시지가 표시되도록 개선하였습니다.
* 인증서 패스프레이즈 값을 최대 200자까지 입력할 수 있도록 제한하였습니다.
<a id="march-28-2023-bug-fixes"></a>
#### 버그 수정
* 사용자 데이터 수정 후 수정 버튼이 비활성화되는 문제를 수정하였습니다.

<a id="february-28-2023"></a>
### 2023. 02. 28. { #february-28-2023 }
<a id="february-28-2023-added-features"></a>
#### 기능 추가
* SAN 인증서 기능이 추가되었습니다.
  * SAN(subject alternative name)은 1개의 인증서로 여러 개의 도메인에 SSL을 적용할 수 있는 인증서입니다.
  * SAN 인증서를 등록하여 서브 인증서들의 만료일과 알림 설정을 용이하게 관리할 수 있습니다.
  * SAN 인증서를 추가하거나 수정할 때 인증서 파일(.pem)의 정보를 읽어 인증서 이름과 서브 인증서 이름을 자동으로 입력합니다.

<a id="february-28-2023-feature-updates"></a>
#### 기능 개선
* 사용자 데이터 이름을 공백으로만 입력할 수 없도록 개선하였습니다.

<a id="january-31-2023"></a>
### 2023. 01. 31. { #january-31-2023 }
<a id="january-31-2023-feature-updates"></a>
#### 기능 개선
* 사용자 데이터의 최대 길이를 3,000자에서 700자로 제한하였습니다.
* 도메인의 이름 규칙이 변경되었습니다.
    * 도메인의 처음과 끝, dot(.)과 dot(.) 사이를 63자로 제한하였습니다.
    * 도메인의 최대 길이를 260자로 제한하였습니다.
<a id="january-31-2023-bug-fixes"></a>
#### 버그 수정
* 이메일 알림 시 알림 그룹과 사용자 데이터 이름이 HTML 포맷이면 HTML 포맷이 적용되는 문제를 수정하였습니다.

<a id="december-27-2022"></a>
### 2022. 12. 27. { #december-27-2022 }
<a id="december-27-2022-feature-updates"></a>
#### 기능 개선
* 검색 바의 **초기화** 버튼을 클릭하면 모든 옵션이 선택되도록 개선하였습니다.
* 드롭다운 목록에서 검색 옵션을 선택한 뒤 **적용** 버튼을 클릭하지 않고 드롭다운 목록을 닫을 경우에도 선택한 옵션이 적용되도록 개선하였습니다.
* 도메인에서 자동 수집 기능이 동작하지 않는 경우 등록자 및 등록 기관 항목에 `-` 기호가 표시되도록 개선하였습니다.
* SMS 알림에서 조직 이름이 추가되고, 안내 문구가 축약되었습니다.
<a id="december-27-2022-bug-fixes"></a>
#### 버그 수정
* 도메인 추가 페이지에 재진입할 경우 만료일 날짜가 이전에 설정한 값으로 설정되는 문제를 수정하였습니다.

<a id="october-25-2022"></a>
### 2022. 10. 25. { #october-25-2022 }
<a id="october-25-2022-feature-updates"></a>
#### 기능 개선
* 프로젝트 통합 앱키를 이용한 API 호출이 제대로 동작하지 않는 문제를 수정하였습니다.
* 도메인/인증서 수집 실패 시 당일 확인 건에 대해서만 메일이 발송되도록 로직을 수정하였습니다.

<a id="october-4-2022"></a>
### 2022. 10. 04. { #october-4-2022 }
<a id="october-4-2022-feature-updates"></a>
#### 기능 개선
* 역할 그룹 관리를 통해 권한을 부여할 경우 권한이 정상적으로 적용되지 않는 문제를 수정하였습니다.

<a id="august-23-2022"></a>
### 2022. 08. 23. { #august-23-2022 }
<a id="august-23-2022-feature-updates"></a>
#### 기능 개선
* API 엔드포인트의 도메인이 api-certificate-manager.cloud.toast.com에서 certmanager.api.nhncloudservice.com으로 변경되었습니다.

<a id="march-24-2020"></a>
### 2020. 03. 24. { #march-24-2020 }
<a id="march-24-2020-added-features"></a>
#### 기능 추가
Certificate Manager에 등록한 인증서 목록을 조회할 수 있는 API를 추가했습니다.
* [API] 인증서 목록 조회 API 추가

<a id="january-21-2020"></a>
### 2020. 01. 21. { #january-21-2020 }
<a id="january-21-2020-new-releases"></a>
#### 신규 서비스 출시
Certificate Manager는 만료일 연장을 놓치지 않도록, 만료일이 가까워지면 알림(SMS, 이메일)을 발송하는 서비스입니다.
만료일이 존재하는 TLS 인증서, 도메인, 사용자 데이터(예: 라이선스)를 관리하고, 만료일에 따른 알림 발송 규칙과 알림을 받을 사용자를 정할 수 있습니다.
