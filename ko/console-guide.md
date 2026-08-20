<!-- pre-align:aligned sig=4cffce67e4ac -->

<a id="network-service-gateway-console-user-guide"></a>
## Network > Service Gateway > 콘솔 사용 가이드 { #network-service-gateway-console-user-guide }

콘솔에서 **Service Gateway** 서비스를 사용하는 방법을 설명합니다.

<a id="service-gateway"></a>
## 서비스 게이트웨이 { #service-gateway }

<a id="create-a-service-gateway"></a>
### 서비스 게이트웨이 생성 { #create-a-service-gateway }

서비스 게이트웨이를 생성하는 방법은 다음과 같습니다.

1. **Network > Service Gateway**로 이동합니다.
2. **서비스 게이트웨이 생성** 버튼을 클릭하면 생성 화면이 나타납니다.
3. 서비스 게이트웨이에 사용할 **이름**을 입력합니다.
4. **연결 유형**을 선택합니다. 서비스 게이트웨이에 할당된 IP로 접근 시 선택한 대상과 연결됩니다.
    * **서비스 엔드포인트**: NHN Cloud가 제공하는 서비스에 연결합니다. 목록에서 연결할 **서비스**를 선택합니다.
    * **사용자 정의 엔드포인트**: 다른 사용자가 게시한 리소스(로드 밸런서)에 연결합니다. 엔드포인트 게시자에게 전달받은 **대상 서비스 이름**을 입력합니다. 서비스 이름은 `{region}.sep-{12자리 16진수}` 형식입니다(예: `kr1.sep-0a1b2c3d4e5f`).

    !!! tip "알아두기"
        입력한 서비스 이름은 생성 시 유효성이 검증되며, 게시자의 허용 프로젝트에 포함된 경우에만 연결할 수 있습니다.

5. **VPC**를 선택합니다. 선택된 VPC에 종속된 서비스 게이트웨이가 생성됩니다.
6. **서브넷**을 선택합니다. 선택된 서브넷에서 서비스 게이트웨이의 IP가 할당됩니다.
7. **사설 IP** 할당 방법을 선택합니다.
    * 자동 할당: 선택된 서브넷의 CIDR 범위 내에서 자동으로 할당합니다.
    * 지정: 사용할 IP 주소를 수동으로 입력합니다.

    !!! tip "알아두기"
        입력하는 IP 주소는 선택된 서브넷의 CIDR 범위 내에 있어야 합니다.

8. **NAT IP 고정** 여부를 선택합니다.
    * 일반적으로는 선택할 필요가 없으며, 선택한 **서비스**에서 접근제어 설정이 필요한 경우만 선택합니다.
    * 생성 시에만 선택이 가능하며 변경은 지원하지 않습니다.

    !!! tip "알아두기"
        선택이 가능한 서비스에서만 활성화됩니다.

<a id="view-a-service-gateway"></a>
### 서비스 게이트웨이 조회 { #view-a-service-gateway }

생성한 서비스 게이트웨이는 **Network > Service Gateway** 화면에서 확인할 수 있습니다. 서비스 게이트웨이를 선택하면 하단에 서비스 게이트웨이 정보가 나타납니다. 연결 유형이 **사용자 정의 엔드포인트**인 경우, 상세 정보의 **연결 대상**에서 엔드포인트의 표시 이름과 식별자를 확인할 수 있습니다.

<a id="modify-a-service-gateway"></a>
### 서비스 게이트웨이 변경 { #modify-a-service-gateway }

서비스 게이트웨이를 변경하는 방법은 다음과 같습니다. **이름**, **설명**만 변경할 수 있습니다.

1. **Network > Service Gateway**로 이동합니다.
2. **서비스 게이트웨이 변경** 버튼을 클릭한 후 변경 화면에서 원하는 항목을 변경합니다.

<a id="delete-a-service-gateway"></a>
### 서비스 게이트웨이 삭제 { #delete-a-service-gateway }

서비스 게이트웨이를 삭제하려면 **Network > Service Gateway** 화면에서 삭제할 서비스 게이트웨이를 선택하고 **서비스 게이트웨이 삭제** 버튼을 클릭합니다.

<a id="custom-endpoints"></a>
## 사용자 정의 엔드포인트 { #custom-endpoints }

사용자 정의 엔드포인트는 사용자가 자신의 리소스(로드 밸런서)를 엔드포인트로 게시하여, 다른 프로젝트에서 서비스 게이트웨이로 연결할 수 있도록 공유하는 기능입니다. 게시자는 공유용 ***서비스 이름**(`service_name`)을 발급받아 연결을 허용할 대상에게 전달하고, 허용 프로젝트를 직접 관리합니다.

<a id="create-a-custom-endpoint"></a>
### 사용자 정의 엔드포인트 생성 { #create-a-custom-endpoint }

사용자 정의 엔드포인트를 생성하는 방법은 다음과 같습니다.

1. **Network > Service Gateway**로 이동한 후 **사용자 정의 엔드포인트** 탭을 선택합니다.
2. **사용자 정의 엔드포인트 생성** 버튼을 클릭하면 생성 화면이 나타납니다.
3. 엔드포인트에 사용할 **이름**을 입력합니다. (255자 이내, 영문/숫자/-/_만 입력 가능)
4. **표시 이름**을 입력합니다. 이 엔드포인트에 연결하는 서비스 게이트웨이에 표시되는 이름입니다. 생략하면 이름과 동일하게 적용됩니다.
5. **리소스 유형**과 **대상 리소스**를 선택합니다. 현재 리소스 유형은 **Load Balancer**만 지원하며, 대상 리소스에서 엔드포인트로 게시할 로드 밸런서를 선택합니다.
6. **최대 생성 개수**를 선택합니다. 이 엔드포인트로 생성할 수 있는 서비스 게이트웨이의 최대 개수입니다.
    * 제한 없음: 개수 제한 없이 생성할 수 있습니다. 1,000을 초과하는 개수가 필요한 경우에도 제한 없음을 선택합니다.
    * 직접 입력: 0부터 1,000까지 입력할 수 있습니다. 0을 입력하면 생성이 차단됩니다.
7. 필요 시 **설명**을 입력하고 **확인** 버튼을 클릭합니다.
8. 생성이 완료되면 공유용 **서비스 이름**(`{region}.sep-{12자리 16진수}`)이 자동으로 발급됩니다. 이 서비스 이름을 연결을 허용할 소비자에게 전달합니다.

!!! tip "알아두기"
    사용자 정의 엔드포인트는 프로젝트당 기본 5개까지 생성할 수 있습니다.

<a id="view-custom-endpoints"></a>
### 사용자 정의 엔드포인트 조회 { #view-custom-endpoints }

**사용자 정의 엔드포인트** 탭에서 생성한 엔드포인트 목록을 확인할 수 있습니다. 엔드포인트를 선택하면 하단에 상세 정보가 나타나며, **기본 정보**(서비스 이름, 리소스 유형, 대상 리소스, 최대 생성 개수 등), **허용 프로젝트**, **사용 현황**을 확인할 수 있습니다.

<a id="modify-a-custom-endpoint"></a>
### 사용자 정의 엔드포인트 변경 { #modify-a-custom-endpoint }

**이름**, **표시 이름**, **최대 생성 개수**, **설명**만 변경할 수 있습니다. 리소스 유형과 대상 리소스는 변경할 수 없습니다.

1. **사용자 정의 엔드포인트** 탭에서 변경할 엔드포인트를 선택합니다.
2. **변경** 버튼을 클릭한 후 변경 화면에서 원하는 항목을 변경합니다.

!!! tip "알아두기"
    최대 생성 개수를 줄여도 이미 생성된 서비스 게이트웨이는 유지됩니다. 다만 현재 개수가 최대 생성 개수를 초과하는 동안에는 새 서비스 게이트웨이를 추가로 생성할 수 없습니다.

<a id="delete-a-custom-endpoint"></a>
### 사용자 정의 엔드포인트 삭제 { #delete-a-custom-endpoint }

**사용자 정의 엔드포인트** 탭에서 삭제할 엔드포인트를 선택하고 **삭제** 버튼을 클릭합니다.

!!! danger "주의"
    이 엔드포인트를 사용 중인 서비스 게이트웨이가 하나라도 있으면 삭제할 수 없습니다. 엔드포인트를 삭제하면 등록된 허용 프로젝트도 함께 삭제됩니다.

<a id="reissue-a-service-name"></a>
### 서비스 이름 재발급 { #reissue-a-service-name }

공유한 서비스 이름이 외부에 유출되는 등 변경이 필요한 경우 서비스 이름을 재발급할 수 있습니다.

1. **사용자 정의 엔드포인트** 탭에서 엔드포인트를 선택한 후 **기본 정보**에서 서비스 이름의 **재발급** 버튼을 클릭합니다.
2. 확인 창에서 **재발급** 버튼을 클릭합니다.

!!! danger "주의"
    재발급하면 기존 서비스 이름은 즉시 폐기되어 더 이상 조회되지 않습니다. 기존 서비스 이름으로 생성한 서비스 게이트웨이는 정상 동작하지만, 새로 서비스 게이트웨이를 생성하려면 재발급된 서비스 이름을 사용해야 합니다.

!!! tip "알아두기"
    서비스 이름 재발급은 엔드포인트를 생성한 프로젝트의 구성원(소유자)만 수행할 수 있습니다.

<a id="manage-allowed-projects"></a>
### 허용 프로젝트 관리 { #manage-allowed-projects }

허용 프로젝트는 이 엔드포인트로 연결(서비스 게이트웨이 생성)을 허용할 대상을 관리하는 목록입니다.

1. 엔드포인트를 선택한 후 상세 정보의 **허용 프로젝트** 탭으로 이동합니다.
2. **추가** 버튼을 클릭하고 **허용 범위**를 선택합니다.
    * **전체 프로젝트(*)**: 모든 프로젝트의 연결을 허용합니다.
    * **특정 프로젝트**: 허용할 프로젝트의 **테넌트 ID**(32자리 16진수)를 입력합니다.
3. 필요 시 **설명**을 입력하고 **확인** 버튼을 클릭합니다.

!!! tip "알아두기"
    전체 허용(*)과 특정 프로젝트를 함께 등록한 경우 더 좁은 범위(특정 프로젝트)가 적용됩니다. 이를 이용하면 무중단으로 허용 범위를 전환할 수 있습니다. 예를 들어 전체 허용(*) 상태에서 특정 프로젝트를 추가한 뒤 전체 허용(*)을 삭제하면, 연결 중단 없이 특정 프로젝트만 허용하도록 전환됩니다.

기존 허용 대상은 **설명**만 변경할 수 있으며, 허용 범위와 테넌트 ID는 변경할 수 없습니다. 허용 대상을 삭제하려면 목록에서 대상을 선택하고 **삭제** 버튼을 클릭합니다.

<a id="check-usage-status"></a>
### 사용 현황 확인 { #check-usage-status }

엔드포인트 상세 정보의 **사용 현황** 탭에서 이 엔드포인트에 연결 중인 서비스 게이트웨이 목록을 확인할 수 있습니다. (읽기 전용)

<a id="use-a-service-gateway"></a>
## 서비스 게이트웨이 사용 { #use-a-service-gateway }

<a id="check-the-service-gateway-ip"></a>
### 서비스 게이트웨이 IP확인 { #check-the-service-gateway-ip }

1. **Network > Service Gateway**로 이동합니다.
2. 서비스 게이트웨이 목록에서 **IP 주소**를 확인합니다.<br>
   이 VM Instance에서 이 IP 주소로 접속 시 서비스 게이트웨이가 연결하고 있는 서비스로 연결됩니다.

<a id="connect-to-the-service-gateway"></a>
### 서비스 게이트웨이 접속 { #connect-to-the-service-gateway }

생성된 서비스 게이트웨이의 IP 주소가 `192.168.1.42`라 할 경우 다음과 같은 방법으로 서비스에 접근이 가능합니다.

* VM Instance에서 서비스 게이트웨이 IP로 접속하면 서비스 게이트웨이 생성 시 선택된 서비스로 연결되어 서비스 사용이 가능합니다.
    * IP 주소를 사용하여 https 프로토콜을 이용할 경우 인증서 관련 오류가 발생할 수도 있습니다.
    * https 사용이 필요한 경우 VM Instance의 `/etc/hosts`에 IP 주소와 URL을 추가하시기 바랍니다.
    * 예시) IP 주소를 이용하여 오브젝트 스토리지에서 파일 다운로드

            ~# wget http://192.168.1.42/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

* 서비스 게이트웨이를 이용하여 서비스 접근 시 URL을 지원하지 않습니다. URL 접근이 필요한 경우 아래 예시와 같이 `/etc/hosts` 파일에 URL을 추가해야 합니다.
    * 예시) URL을 이용하여 **오브젝트 스토리지**에서 파일 다운로드<br>
      `/etc/hosts` 파일에 아래와 같이 서비스 게이트웨이의 IP 주소와 Object Storage의 URL을 추가합니다.

            192.168.1.42    kr1-api-object-storage.nhncloudservice.com

        IP 주소 대신 `/etc/hosts`에 추가한 URL로 접속

            ~# wget https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

<a id="example-of-using-object-storage-from-a-service-gateway"></a>
## 서비스 게이트웨이에서 오브젝트 스토리지 사용 예제 { #example-of-using-object-storage-from-a-service-gateway }

**오브젝트 스토리지**에 관련된 내용은 예제 설명을 위한 수준에서만 기술합니다. 오브젝트 스토리지의 자세한 사용 방법은 **사용자 가이드 > Storage > Oject Storage**를 참고하시기 바랍니다.

<a id="example-of-using-object-storage-from-a-service-gateway-create-a-service-gateway"></a>
### 서비스 게이트웨이 생성 { #example-of-using-object-storage-from-a-service-gateway-create-a-service-gateway }

**오브젝트 스토리지 API**를 사용하려면 **인증 토큰**을 발급받아야 합니다. 인터넷 사용이 불가능한 격리된 환경의 VPC에서 Object Storage를 사용하려면 인증 토큰도 서비스 게이트웨이를 이용하여 발급받아야 하며, 다음 절차에 따라서 서비스 게이트웨이를 생성해야 합니다.

1. **Object Storage** 서비스를 선택하여 서비스 게이트웨이를 생성합니다.<br>
   오브젝트 스토리지 API 접속을 위한 서비스 게이트웨이입니다.
2. **IaaS API Identity** 서비스를 선택하여 서비스 게이트웨이를 생성합니다.<br>
   인증 토큰(token) 발급을 위한 서비스 게이트웨이입니다.
3. 생성된 두 개의 서비스 게이트웨이에서 IP 주소를 확인합니다.

<a id="edit-the-etchosts-file"></a>
### /etc/hosts 파일 편집 { #edit-the-etchosts-file }

**Object Storage**를 선택하여 생성한 서비스 게이트웨이의 IP 주소가 192.168.1.42이고 **IaaS API Identity**를 선택하여 생성한 서비스 게이트웨이의 IP 주소로 192.168.1.57을 할당받은 경우, VM Instance의 `/etc/hosts` 파일에 아래와 같이 IP 주소와 URL을 추가합니다.

!!! tip "알아두기"
    오브젝트 스토리지의 API URL 주소는 콘솔 화면의 **Storage > Object Storage**에서 **API 엔드포인트 설정** 버튼을 클릭하여 확인할 수 있습니다.

!!! danger "주의"
    리전마다 사용하는 오브젝트 스토리지 API의 URL 주소는 다르기 때문에 **API 엔드포인트 설정**의 URL을 반드시 확인해 주시기 바랍니다.

```
192.168.1.42	api-identity-infrastructure.nhncloudservice.com
192.168.1.57	kr1-api-object-storage.nhncloudservice.com
```

<a id="obtain-the-authentication-token"></a>
### 인증 토큰 발급 { #obtain-the-authentication-token }

오브젝트 스토리지의 **API 비밀번호 설정**을 하고 인증 토큰을 발급받습니다.

* API 비밀번호 설정
    1. **Storage > Object Storage**에서 **API 엔드포인트 설정** 버튼을 클릭합니다.
    2. **API 엔드포인트 설정** 화면의 **API 비밀번호 설정**에 사용할 비밀번호를 입력하고 **변경** 버튼을 클릭합니다.

    !!! tip "알아두기"
        상세한 사용 방법은 [사용자 가이드 > Storage > Object Storage > API 가이드](https://docs.nhncloud.com/ko/Storage/Object%20Storage/ko/api-guide/)를 참고하시기 바랍니다.

* 인증 토큰 발급 요청<br>
  **NHN Cloud 로그인 ID**와 앞서 설정한 **API 비밀번호 설정**의 비밀번호를 이용하여 아래와 같이 **IaaS API Identify** 서비스용으로 생성한 서비스 게이트웨이 URL에 토큰 발급을 요청합니다.
    * `auth.passwordCredentials.username`에는 NHN Cloud 로그인 ID 사용
    * `auth.passwordCredentials.password`에는 API 비밀번호 설정에 입력한 비밀번호 사용
  

            ~# curl -X POST -H 'Content-Type:application/json' https://api-identity-infrastructure.nhncloudservice.com/v2.0/tokens -d '{"auth": {"tenantId": "2fda9d4b88244a0a92ff23841198e2e6", "passwordCredentials": {"username": "example@nhn.com", "password": "example123"}}}'

* 인증 토큰 발급 응답<br>
  아래 응답에서 `access.token.id` 항목의 값이 인증 토큰입니다. `access.token.expires`에 기록된 시간까지 인증 토큰이 유효합니다.

            {"access":{"token":{"id":"gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY","expires":"2022-04-13T19:19:30Z","tenant":{"id":"2fda9d4b8821111192ff23841198e2e6","name":"tTMgSSSF","groupId":"XXj2zkH7777modGU","description":"","enabled":true,"project_domain":"NORMAL","swift":true},"issued_at":"2022-04-13T07:32:14.000441"},"serviceCatalog":[{"endpoints":[{"region":"KR1","publicURL":"https://api-identity.infrastructure.cloud.toast.com/v2.0"}],"type":"identity","name":"keystone"},{"endpoints":[{"region":"KR2","publicURL":"https://kr2-api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"},{"region":"KR1","publicURL":"https://api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"}],"type":"object-store","name":"swift"}],"user":{"id":"80884888887b45dbaf9b815117130671","username":"5111111c-b111-4b11-b11b-01111f81111f","name":"5211122c-bfc4-4115-b11b-05b52f84

<a id="use-the-object-storage-api"></a>
### 오브젝트 스토리지 API 사용 { #use-the-object-storage-api }

인증 토큰 발급을 마쳤으면 오브젝트 스토리지 API를 사용할 수 있습니다. 오브젝트 스토리지에 example이라는 컨테이너를 생성하고 test_file.txt를 넣어 놨다고 가정할 경우, 아래와 같은 API 사용법으로 컨테이너에 있는 파일을 조회할 수 있습니다.

* 요청<br>
  `X-Auth-Token`에 인증 토큰을 추가하여 요청

        ~# curl -X GET -H 'X-Auth-Token:gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY' https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6/example

* 응답<br>
  오브젝트 스토리지 컨테이너에 있는 파일 목록 확인

        test_file.txt
