<!-- pre-align:aligned sig=be0be57a5d82 -->

<a id="security-secure-key-manager-console-user-guide-approval-feature"></a>
## Security > Secure Key Manager > 콘솔 사용 가이드 > 승인 기능 { #security-secure-key-manager-console-user-guide-approval-feature }

국내·외 보안 인증 심사(ISMS-P, ISO 등)에서 요구하는 안전한 암호화 키 관리 요구 사항을 충족하기 위해 사용하는 Secure Key Manager의 승인 기능에 대해 설명합니다.

**승인 기능 활성화** 방법과 승인 기능 활성화 이후 승인 관련 역할 설정과 활성화 전과 후의 차이점 그리고 **승인 과정**에 대해 알아보겠습니다.

![approval-feature](http://static.toastoven.net/prod_kms/2024-02-27-ko/approval-feature.png)

<a id="enable-approval-feature"></a>
## 승인 기능 활성화 { #enable-approval-feature }

<a id="how-to-enable-approval-feature"></a>
### 승인 기능 활성화 방법 { #how-to-enable-approval-feature }
**조직 관리** 화면의 **거버넌스 설정**에서 **승인 프로세스 관리 설정**을 통해 Secure Key Manager의 승인 기능을 활성화합니다.

![console-guide-29](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-29.png)

<a id="set-up-roles-for-approval-feature"></a>
### 승인 기능 역할 설정 { #set-up-roles-for-approval-feature }
Secure Key Manager의 멤버 관리를 통해 승인자(APPROVAL ADMIN), 요청자(APPROVAL MEMBER) 역할을 획득하여 승인 절차를 진행합니다.

![console-guide-30](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-30.png)

<a id="differences-with-approval-feature-enabled"></a>
### 승인 기능 활성화에 따른 차이점 { #differences-with-approval-feature-enabled }
승인 기능을 활성화하고 승인자 또는 요청자 역할을 획득하면 Secure Key Manager에 **승인리스트**와 **키 저장소 관리** 탭이 추가됩니다. 두 탭은 승인자, 요청자만 접근할 수 있습니다.

![console-guide-31](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-31.png)

승인 기능을 활성화하면 더 이상 키 저장소에서 데이터를 추가, 수정, 삭제할 수 없으며, 변경 요청 시 **키 저장소 관리** 탭으로 이동합니다.

![console-guide-32](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-32.png)

<a id="approval-process"></a>
## 승인 과정 { #approval-process }

<a id="make-approval-requests"></a>
### 승인 요청 작성 { #make-approval-requests }
승인자와 요청자는 **키 저장소 관리** 탭에서 키 저장소별로 변경 내용을 승인 요청할 수 있습니다. 기존의 키 저장소와 유사한 동작을 통해 추가, 수정, 삭제를 진행합니다. 키, 인증 정보의 변경 상태에 대해서는 다음과 같이 상태에 표시됩니다.

![console-guide-33](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-33.png)

![console-guide-34](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-34.png)

키 저장소의 **승인 요청** 버튼으로 승인을 요청하고 해당 프로젝트의 승인 요청들은 **승인리스트** 탭에서 확인할 수 있습니다.

![console-guide-35](http://static.toastoven.net/prod_kms/2024-09-25-ko/console-guide-35.png)

<a id="apply-approval-requests"></a>
### 승인 요청 반영 { #apply-approval-requests }
승인자는 **승인리스트**에서 키 저장소의 변경 승인 요청을 확인하고 **승인** 또는 **거절**을 선택해 반영 여부를 결정합니다.

본인이 요청한 건에 대해서는 승인 권한이 없습니다.

![console-guide-36](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-36.png)

승인을 누르는 즉시 키 저장소에 반영됩니다. **키 저장소** 또는 **키 저장소 관리** 탭에서 변경 내용을 확인할 수 있습니다.

![console-guide-37](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-37.png)