## Security > Secure Key Manager > 콘솔 사용 가이드 > 시작하기

시작하기에서는 Secure Key Manager를 사용하는 데 필요한 기본적인 내용을 설명합니다.

![getting-started](http://static.toastoven.net/prod_kms/2024-02-27-ko/getting-started.png)

## 키 저장소 생성
Secure Key Manager는 키 저장소 단위로 인증 정보와 키를 관리합니다. 키 저장소가 없으면 다음과 같은 화면이 나타납니다.

![console-guide-01](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-01.png)

**키 저장소 추가**를 클릭하면 키 저장소를 생성할 수 있는 창이 나타납니다.

![console-guide-02](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-02.png)

이름과 설명을 입력하고 한 개 이상의 인증 방법을 선택한 후 **추가**를 클릭하면 키 저장소를 생성합니다. 생성한 키 저장소는 다음 그림과 같이 키 저장소 목록에 표시합니다.

![console-guide-03](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-03.png)

키 저장소 목록에서 키 저장소를 클릭하면 다음 그림과 같이 키 저장소를 관리할 수 있는 메뉴가 나타납니다.

![console-guide-04](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-04.png)

### 키 저장소 상세 정보

키 저장소 우측 상단의 더보기 버튼을 클릭하여, 상세 정보 메뉴를 통해 선택한 키 저장소의 상세 정보를 확인할 수 있습니다.
![console-guide-43](http://static.toastoven.net/prod_kms/2024-02-27-ko/console-guide-01.png)

## 키 생성
Secure Key Manager는 키를 3가지 유형으로 구분합니다. 기밀 데이터는 문자열 데이터를 저장하고 API를 사용한 조회 기능을 제공합니다. 대칭 키는 API를 사용한 데이터 암/복호화 기능을 제공합니다. 비대칭 키는 API를 사용한 데이터 서명/검증 기능을 제공합니다. 사용자는 사용 목적에 맞는 키 유형을 선택한 후 키를 생성할 수 있습니다.

**키 관리** 메뉴를 클릭하면 다음 그림과 같이 키를 관리할 수 있는 화면을 표시합니다.

![console-guide-05](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-05.png)

키 관리 화면에서 **키 추가**를 클릭하면 키를 생성할 수 있는 창이 나타납니다. 선택한 키 유형에 따라 원하는 데이터를 입력할 수 있습니다.

![console-guide-06](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-06.png)


![console-guide-07](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-07-gov.png)


![console-guide-08](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-08-gov.png)


기밀 데이터를 선택하면 이름, 설명, 데이터를 입력할 수 있고 대칭 키/비대칭 키를 선택하면 이름, 설명, 회전 주기를 입력할 수 있습니다. 필수 데이터를 입력한 후 **추가**를 클릭하면 키를 생성합니다. 생성한 키는 다음 그림과 같이 키 관리 화면에 표시합니다.

![console-guide-09](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-09.png)

### 키 가져오기
Secure Key Manager는 대칭 키(ARIA-256)를 가져오는 기능을 지원합니다.

![console-guide-10](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-10-gov.png)

**키 데이터** 영역에 키값을 입력하여 업로드할 수 있으며, 업로드 가능한 키의 형태는 다음과 같습니다.

```
0xXX, 0xXX, ..., 0xXX
```

위와 같은 32개의 Hex String을 쉼표(`,`) 또는 공백(` `)을 구분자로 구분하여 입력하여 키를 업로드합니다.

## 인증 정보 등록
Secure Key Manager에서 생성한 키는 인증에 성공한 클라이언트만 사용할 수 있습니다. 클라이언트 인증에 사용하는 인증 정보는 **IPv4 주소 관리**, **MAC 주소 관리**, **인증서 관리** 메뉴에서 등록합니다.

### IPv4 주소 등록
**IPv4 주소 관리**를 클릭하면 다음 그림과 같이 클라이언트 인증에 사용하는 IPv4 주소 관리 화면이 나타납니다.

![console-guide-11](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-11.png)

**IPv4 주소 추가**를 클릭하면 그림과 같이 IPv4 주소를 추가할 수 있는 창이 나타납니다.

![console-guide-12](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-12.png)

IPv4는 IP 형식뿐만 아니라, CIDR 표기법을 통한 IPv4의 대역을 등록할 수 있습니다.

![console-guide-38](http://static.toastoven.net/prod_kms/2023-09-26-ko/consoe-guide-38.png)

클라이언트 IPv4 주소와 설명을 입력한 후 **추가**를 클릭하면 IPv4 주소를 추가합니다. 이때 IPv4 주소에는 클라이언트가 Secure Key Manager에 접속할 때 사용하는 IPv4 주소를 입력해야 합니다. 추가한 IPv4 주소는 다음 그림과 같이 IPv4 주소 관리 화면에 표시합니다.

![console-guide-13](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-13.png)

### MAC 주소 등록
**MAC 주소 관리**를 클릭하면 클라이언트 인증에 사용하는 MAC 주소 관리 화면이 나타납니다.
![console-guide-14](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-14.png)

**MAC 주소 추가**를 클릭하면 MAC 주소를 추가할 수 있는 창이 나타납니다.

![console-guide-15](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-15.png)

클라이언트 MAC 주소와 설명을 입력한 후 **추가**를 클릭하면 MAC 주소를 추가합니다. 추가한 MAC 주소는 MAC 주소 관리 화면에 나타납니다.

![console-guide-16](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-16.png)

### 클라이언트 인증서 등록
**인증서 관리**를 클릭하면 클라이언트 인증에 사용하는 인증서 관리 화면이 나타납니다.

![console-guide-17](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-17.png)

**인증서 추가**를 클릭하면 인증서를 생성할 수 있는 창이 나타납니다.

![console-guide-18](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-18.png)

인증서 이름, 비밀번호, 설명을 입력하고 사용 기간을 선택한 후 **추가**를 클릭하면 인증서를 생성합니다. 생성한 인증서는 다음과 같이 인증서 관리 화면에 나타납니다. 인증서 관리 화면에서 **다운로드** 아이콘을 클릭하면 인증서 파일을 다운로드합니다.

![console-guide-19](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-19.png)

## 사용자 데이터 관리
Secure Key Manager는 사용자가 생성한 데이터(키, 인증 정보)의 상세 정보를 제공합니다. 사용자 데이터 목록에서 **상세 정보 아이콘**을 클릭하면 다음 그림과 같이 상세 정보를 표시합니다.

![console-guide-20](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-20.png)

### 사용자 데이터 삭제

사용자가 생성한 데이터의 초기 상태는 **사용 중**입니다. 불필요한 데이터를 삭제하려면 다음 그림과 같이 **상세 정보** 창에서 **삭제 요청**을 클릭합니다.

![console-guide-21](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-21.png)

삭제를 요청하면 다음 그림과 같이 데이터 상태를 **삭제 예정**으로 변경합니다. **삭제 예정**으로 변경한 데이터는 사용할 수 없으며 7일 후 완전히 삭제됩니다.

![console-guide-22](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-22.png)

**삭제 예정** 상태의 데이터는 **즉시 삭제**를 클릭해서 삭제 예정 시간까지 기다리지 않고 바로 삭제하거나 **삭제 취소**를 클릭해서 **사용 중** 상태로 되돌릴 수 있습니다.

![console-guide-23](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-23.png)

### 대칭 키/비대칭 키 회전

Secure Key Manager에서는 대칭 키/비대칭 키를 회전할 수 있습니다. 다음 그림과 같이 대칭 키/비대칭 키 상세 정보 창에서 자동 회전 주기를 설정할 수 있습니다. 회전 주기를 '0'으로 설정하면 자동 회전을 사용하지 않습니다.

![console-guide-24](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-24-gov.png)

회전 주기에 30 이상의 값을 설정하면 다음 회전 일을 표시하며 회전 주기마다 키를 자동으로 회전합니다.

![console-guide-25](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-25-gov.png)

대칭 키/비대칭 키 상세 정보 창에서 **즉시 회전**을 클릭하면 키를 바로 회전할 수 있습니다.

![console-guide-26](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-26-gov.png)

키를 회전하면 다음 그림과 같이 키 버전 목록에 새로운 버전이 추가됩니다.

![console-guide-27](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-27-gov.png)

예외로 키 가져오기를 통해 생성한 키는 Secure Key Manager를 통해 생성한 대칭 키와는 다르게 회전 기능을 제공하지 않습니다. 조회 시 다음과 같이 키 회전 영역이 존재하지 않습니다.

![console-guide-28](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-28-gov.png)

## API 인증 방법
Secure Key Manager는 API 호출 및 인증을 위해 User Access Key, Appkey, 프로젝트 통합 Appkey를 지원합니다.
사용 중인 버전의 API 가이드에서 지원하는 인증 방법을 확인하세요.

### User Access Key
User Access Key는 NHN Cloud 계정 또는 IAM 계정을 기반으로 발급되는 인증 키로, Secret Access Key와 함께 사용하여 API 요청에 대한 인증 수단으로 활용됩니다. API 요청 시 사용자 단위로 접근 권한을 인증할 수 있으며, 사용자별 세밀한 권한 제어가 가능합니다. 인증된 NHN Cloud 계정 또는 IAM 계정에 부여된 역할 및 권한에 따라 API 호출이 제한되지만, API 버전에 따라 인가 기능이 적용되지 않을 수도 있습니다.

> [주의]
> * User Access Key와 Secret Access Key는 유효 기간이 없는 고정 키 기반 인증 방식으로 키가 외부에 노출될 경우 해당 계정의 역할 및 권한 범위 내 모든 API가 무단 호출될 수 있습니다.
> * 키는 외부 저장소 또는 코드에 포함되지 않도록 안전하게 보관하고, 유출이 의심될 경우 즉시 폐기하고 재발급해야 합니다.

#### User Access Key 발급하기
User Access Key는 NHN Cloud 콘솔의 **API 보안 설정**에서 발급할 수 있습니다.

1) NHN Cloud 콘솔에서 우측 상단의 계정에 마우스 포인터를 올리면 표시되는 드롭다운 메뉴에서 **API 보안 설정**을 클릭합니다.

2) **+ User Access Key 생성**을 클릭합니다.<br>
![C_userAccessKey_1_ko](http://static.toastoven.net/prod_kms/2026-07-24-ko/C_userAccessKey_1_ko.png)

3) **User Access Key 생성** 모달 창에서 **토큰 유효 시간**을 설정한 뒤 **생성**을 클릭합니다.<br>
![C_userAccessKey_2_ko](http://static.toastoven.net/prod_kms/2026-07-24-ko/C_userAccessKey_2_ko.png)

4) **User Access Key 발급 완료** 모달 창에서 **Secret Access Key**를 복사한 뒤 **확인**을 클릭합니다.<br>
![C_userAccessKey_3_ko](http://static.toastoven.net/prod_kms/2026-07-24-ko/C_userAccessKey_3_ko.png)

> [주의]
> * 모달 창을 닫은 뒤에는 Secret Access Key를 다시 확인할 수 없습니다. Secret Access Key를 잊어버릴 경우 재생성해야 하므로 반드시 복사한 뒤 별도로 관리하세요.
> * User Access Key 또는 Secret Access Key 중 하나라도 유출되었거나 유출이 의심되는 경우 해당 키를 폐기하고 새로 발급 받아야 합니다.

> [참고]
> * User Access Key는 NHN Cloud 계정과 IAM 계정당 각각 5개까지 발급할 수 있습니다.
> * User Access Key ID는 90일마다 변경할 것을 권장합니다.

#### API 호출하기
User Access Key는 HTTP 요청 헤더에 포함하여 전달합니다. API 호출 시 아래 예시와 같이 헤더에 User Access Key를 설정해 호출하세요.

* HTTP 헤더 형식 예시
```
X-TC-AUTHENTICATION-ID: {User Access Key}
X-TC-AUTHENTICATION-SECRET: {Secret Access Key}
```

사용자가 HTTP 헤더에 키를 담아 서버에 요청을 보내면 서버는 해당 키의 유효성 및 권한을 확인한 뒤 요청을 승인하거나 거부합니다.

### Appkey
Appkey는 NHN Cloud의 각 서비스별로 발급되는 고유 인증 키로 API 요청 시 서비스 식별과 유효성 검증에 사용됩니다. 인증을 위한 별도의 사용자 등록, 토큰 요청 또는 갱신 절차 없이 API 요청 시 Appkey만 포함하면 되므로 인증 과정이 비교적 간단합니다.

#### Appkey 확인하기
Appkey는 서비스별로 발급되며, NHN Cloud 콘솔의 각 서비스 화면에서 확인할 수 있습니다.

1) NHN Cloud 콘솔 우측 상단에서 **URL & Appkey**를 클릭합니다.

2) **URL & Appkey - Secure Key Manager** 모달 창에서 Appkey를 확인하거나 복사한 뒤 **확인**을 클릭합니다.

> [주의]
> Appkey가 유출되었거나 유출이 의심되는 경우 NHN Cloud 고객 센터로 연락해 주시면 적합한 조치를 안내해 드리겠습니다.

#### API 호출하기
API 요청 시 Appkey는 path 파라미터로 포함하여 서비스 유효성을 검증합니다. API 요청 시 사용하는 path 형식은 해당 서비스의 API 가이드를 참고하세요.

* 예시
```
POST /v1.0/appkeys/{appKey}/
```

> [주의]
> Appkey는 유효 기간이 없는 고정 키 기반 인증 방식으로 인가 기능이 없어 키가 외부에 노출될 경우 무단으로 API가 호출될 수 있습니다. 키는 외부 저장소 또는 코드에 포함되지 않도록 안전하게 보관하고, 유출이 의심될 경우 즉시 재발급을 요청해야 합니다. Appkey가 유출되었거나 유출이 의심되는 경우 NHN Cloud 고객 센터로 연락해 주시면 적합한 조치를 안내해 드리겠습니다.

### 프로젝트 통합 Appkey
프로젝트 통합 Appkey는 NHN Cloud에서 하나의 프로젝트 내 여러 서비스에 대해 공통으로 사용할 수 있는 인증 키입니다. 각 서비스마다 Appkey를 개별로 관리할 필요 없이 프로젝트 통합 Appkey 하나로 해당 프로젝트에서 사용 중인 모든 서비스의 API를 효율적으로 호출할 수 있습니다. 따라서 관리 대상 키의 수를 줄이고, 사용자가 직접 Appkey를 생성하거나 삭제할 수 있어 키 관리가 유연하고 효율적입니다.

#### 프로젝트 통합 Appkey 생성하기
NHN Cloud 콘솔의 각 프로젝트 화면에서 프로젝트 통합 Appkey를 생성하고 관리할 수 있습니다.

1) NHN Cloud 콘솔에서 프로젝트를 선택한 뒤 **프로젝트 관리** 탭을 클릭합니다.

2) **API 보안 설정**에서 **+ Appkey 생성**을 클릭합니다.<br>
![C_project_API_security_ko](http://static.toastoven.net/prod_kms/2026-07-24-ko/C_project_API_security_ko.png)

3) **Appkey 생성** 모달 창에서 **Appkey 이름** 입력 필드에 생성할 프로젝트 통합 Appkey의 이름을 입력한 뒤 **확인**을 클릭합니다.<br>
![C_project_API_security_2_ko](http://static.toastoven.net/prod_kms/2026-07-24-ko/C_project_API_security_2_ko.png)

> [주의]
> * 프로젝트 통합 Appkey가 외부에 노출될 경우 해당 프로젝트 내 모든 서비스 API가 무단 호출될 수 있으므로 보안 관리에 각별한 주의가 필요합니다. 프로젝트 통합 Appkey를 외부 저장소 또는 코드에 포함하지 않도록 안전하게 보관하고, 유출되었거나 유출이 의심되는 경우 기존 Appkey를 삭제한 뒤 새로운 Appkey를 생성해 교체하세요.

> [참고]
> * 프로젝트 통합 Appkey는 프로젝트당 최대 3개까지 생성할 수 있습니다.

#### API 호출하기
API 요청 시 프로젝트 통합 Appkey는 path 파라미터로 포함하여 서비스 유효성을 검증합니다. API 요청 시 사용하는 path 형식은 해당 서비스의 API 가이드를 참고하세요.

* 예시
```
POST /v1.0/appkeys/{프로젝트 통합 appKey}/
```


