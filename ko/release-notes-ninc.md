## Security > Secure Key Manager > 릴리스 노트

### 2026. 07. 24.

#### 신규 기능 추가
  * 기밀 데이터 수정 API 추가(v1.2)
    * API를 이용하여 Secure Key Manager에 저장한 기밀 데이터를 수정할 수 있는 기능 추가. 자세한 내용은 [API v1.2 가이드](/Security/Secure%20Key%20Manager/ko/api-guide-v1.2-ninc/)를 참고.

#### 기능 개선/변경
  * `APPROVAL MEMBER` 역할 삭제
    * Secure Key Manager APPROVAL MEMBER 역할을 Secure Key Manager ADMIN 역할로 마이그레이션하여 역할 체계 단순화
  * 권한 세분화
    * `SecureKeyManager:API.ADMIN`, `SecureKeyManager:API.VIEWER` 권한을 추가하여 콘솔 및 API 권한을 세분화하여 관리하도록 변경
  * 키 저장소 인증 방식 결합 옵션 추가
    * 키 저장소에 활성화된 여러 인증 방법(IPv4 주소, MAC 주소, 클라이언트 인증서)을 결합하는 방식을 선택할 수 있는 기능 추가. 모두 통과(AND, 기본값) 또는 하나만 통과(OR) 중 선택할 수 있으며, 기존 키 저장소는 모두 통과(AND)로 유지됩니다. 자세한 내용은 [콘솔 사용 가이드](/Security/Secure%20Key%20Manager/ko/console-guide-gov/)를 참고.

### 2026. 03. 13.

#### 신규 서비스 출시

- 기밀 데이터, 대칭 키, 비대칭 키와 같이 애플리케이션 서버에 저장할 경우 보안 위험에 노출될 수 있는 데이터를 중앙 집중적으로 안전하게 관리하고, 인증을 통과한 클라이언트만 접근할 수 있게 제어하는 서비스입니다.
