## Game > Launching > 콘솔 사용 가이드

## Launching 데이터 관리

모바일 앱에서 사용할 Launching 데이터 설정 방법은 다음과 같습니다.

## 설정 정보

Console 화면의 **설정 정보** 탭에서 현재 Launching 정보를 조회할 수 있습니다.

![console_configuration_00](https://static.toastoven.net/prod_launching/ko/console_configuration_00.png)

> [참고]
> Launching 서비스를 사용하면 위 그림과 같이 기본으로 템플릿 데이터를 제공합니다.
> (실제 템플릿 데이터는 그림과는 다를 수 있습니다.)

### 폴더 및 키 선택과 변경

Launching 정보의 왼쪽 탐색 창에서 폴더나 키를 선택하면 오른쪽에 해당 폴더와 키 정보가 나타납니다. 선택된 폴더나 키의 이름과 설명을 변경한 후, **확인** 버튼을 클릭하면 해당 정보가 변경됩니다.
![console_configuration_01](https://static.toastoven.net/prod_launching/ko/console_configuration_01.png)

> [참고]
> **확인** 버튼은 Console 내부적으로 변경 사항을 반영한 것으로, 수정된 사항을 서버에 반영하려면 **배포** 탭에서 배포해야 합니다.

> [참고]
> 서로 다른 폴더에 있는 키 이름은 같을 수 있지만, 한 폴더 안에서는 키 이름이 같을 수 없습니다. 예를 들어 server 폴더 아래에 이름이 'ip'인 키는 하나만 있을 수 있지만, client라는 다른 폴더에는 이름이 같은 'ip' 키가 있을 수 있습니다.

### 키 형식 변경

키를 선택하면 나타나는 오른쪽의 키 정보에서 형식을 변경할 수 있습니다. 배열 형식으로 변경하면 해당 키에서 원하는 문자열 형식의 값을 추가하거나 삭제할 수 있습니다.

![console_configuration_02](https://static.toastoven.net/prod_launching/ko/console_configuration_02.png)

### 폴더 및 키 작업

#### 추가

Launching 정보의 왼쪽 탐색 창에서 폴더를 선택하고 마우스 오른쪽 버튼을 클릭하면 나타나는 메뉴에서 폴더 및 키를 추가하거나, 왼쪽 탐색 창 위의 **폴더 추가/키 추가** 버튼을 클릭해 폴더 및 키를 추가할 수 있습니다.

![console_configuration_03](https://static.toastoven.net/prod_launching/ko/console_configuration_03.png)

#### 복사, 붙여넣기 및 삭제

Launching 정보의 왼쪽 탐색 창에서 폴더 또는 키를 선택한 후 나타나는 메뉴에서 **복사/삭제/붙여넣기** 버튼을 클릭해 원하는 작업을 할 수 있습니다.

![console_configuration_04](https://static.toastoven.net/prod_launching/ko/console_configuration_04.png)

> [참고]
> 폴더를 삭제하면 해당 폴더에 속한 모든 하위 폴더 및 키가 삭제됩니다.

## 로직

**로직** 탭을 클릭하면, 등록된 Launching 정보를 변경하기 위한 서버 로직 정보를 확인할 수 있습니다. 로직은 고정된 Launching 정보를 동적으로 변경하기 위한 비즈니스 로직을 의미하며, 서버에서 구동되기 때문에 모바일 앱의 업데이트 없이 변경된 Launching 정보를 얻을 수 있습니다.

![console_logic_00](https://static.toastoven.net/prod_launching/ko/console_logic_00.png)

### 로직 추가

서버 로직을 추가하려면 로직이 동작하는 시작 시각 및 종료 시각, 로직이 적용되는 조건 및 결과를 입력해야 합니다.

조건에는 최종 결과가 Boolean 인 Javascript 의 조건문을 사용할 수 있습니다.
서버에 등록된 Launching 정보 및 Launching 조회 API의 GET 파라미터값을 일반 변수로 취급하여 사용할 수 있습니다. Launching 정보는 [launching.{folder}.{key}] 형식으로 사용할 수 있으며, 그 외에는 전부 일반 변수로 인식합니다.

결과는 로직의 조건이 맞을 경우, Launching 정보를 변경하는 설정으로, [launching.{folder}.{key}] 형식으로 사용할 수 있습니다.

**적용 기간**에서 로직이 적용될 시간을 설정할 수 있으며, 종료 시각을 설정하지 않고 로직에 계속 적용되게 할 수도 있습니다.

![console_logic_01](https://static.toastoven.net/prod_launching/ko/console_logic_01.png)

> [참고]
> Launching 정보에서 결과로 지정한 키가 없을 때는 새롭게 추가하고, 아니면 기존 정보를 덮어쓰게 됩니다.

> [주의]
> 로직의 조건은 최대 1KB를 넘길 수 없습니다. 또한, 로직 결과는 하나 이상 등록해야 하며, 로직 결과에서 설정하는 키와 결괏값은 최대 255바이트를 넘길 수 없습니다.

### 로직 수정

등록된 로직을 클릭하면 해당 로직을 수정할 수 있습니다.

![console_logic_02](https://static.toastoven.net/prod_launching/ko/console_logic_02.png)

#### 로직 실행 / 정지

로직 목록에서 정지 또는 실행할 로직의 체크박스를 선택한 후, 상단의 **실행 / 정지** 버튼을 클릭해 로직의 상태를 변경할 수 있습니다. 정지 상태의 로직은 Launching 정보를 수정하지 않습니다.

#### 로직 삭제

로직 목록에서 삭제할 로직의 체크박스를 선택한 후, 상단의 **삭제** 버튼을 클릭해 로직을 삭제할 수 있습니다.

> [주의]
> 로직 실행/정지를 포함한 모든 변경 사항을 서버에 반영하려면 **배포** 탭에서 배포해야 합니다.

### 로직 테스트

Launching 정보를 서버에 배포하기 전에 로직을 테스트할 수 있습니다. Launching 정보를 호출할 때 전달한 GET 파라미터와 로직의 적용 시각을 설정한 후 **로직 테스트** 버튼을 클릭하면 하단에 로직이 적용된 Launching 정보를 미리 확인할 수 있습니다.

여러 개의 파라미터 전달을 테스트할 때는, 파라미터 가장 오른쪽의 **+** 버튼을 클릭해 새로운 파라미터를 등록할 수 있습니다.

![console_logic_03](https://static.toastoven.net/prod_launching/ko/console_logic_03.png)

예를 들어 그림과 같이 로직을 등록한 후 테스트를 진행하면 로직 결과에서 테스트 결과를 확인할 수 있습니다.

로직의 조건으로 파라미터 'launching.server.cds'의 값이 'TEST'일 경우 [lauching.server.ip]의 값에 '127.0.0.1'을 넣도록 설정하였고, 로직 테스트 시 GET 파라미터로 'launching.server.cds'에 TEST를 설정해서 테스트 결과에서 [lauching.server.ip]에 '127.0.0.1' 값이 들어간 것을 확인할 수 있습니다.

> [참고]
> 로직 테스트 결과에서 노란색 음영이 처리된 부분은 실제 원본 Launching 정보에서 로직 및 GET 파라미터로 연산하여 추가 또는 변경된 키를 의미합니다.

### 서브 키

서브 키는 "launching."으로 시작하고 "."로 조합되는 키로, 서브 키를 사용하면 Launching 정보에서 일부 데이터만 가져올 수 있습니다.

다음 그림과 같이 서브 키를 [launching.server]로 지정하면 [launching.server]에 있는 데이터만 가져올 수 있습니다.

![console_logic_04](https://static.toastoven.net/prod_launching/ko/console_logic_04.png)

> [주의]
> 그림처럼 서브 키도 GET 파라미터로 지정합니다. "subKey"를 키로 설정한 GET 파라미터는 서브 키로 인식합니다.

### 키 패턴

키 패턴은 "$."로 시작하는 특수한 키로, 로직 조건 및 결과에서 사용할 수 있습니다.
전체 또는 서브 키를 사용해 전달된 최종 결과인 Launching 정보의 루트에서 상대적인 위치를 지정합니다.

다음 그림과 같이 로직이 등록되어 있다고 가정하겠습니다.

![console_logic_05](https://static.toastoven.net/prod_launching/ko/console_logic_05.png)

이런 경우 서브 키를 지정하지 않으면 로직이 적용되지 않습니다.

그러나 서브 키 [launching.server]를 지정해 일부 데이터만 가져올 경우, 로직 조건 "$.cds === 'TEST'"를 만족하게 되어, "$.ip = '127.0.0.1'"에 의해 값이 변경됩니다.

![console_logic_06](https://static.toastoven.net/prod_launching/ko/console_logic_06.png)

이처럼 서브 키 및 키 패턴을 사용해 Launching 정보를 유동적으로 변경할 수 있습니다.

## 가져오기

**가져오기** 탭에서 다른 프로젝트의 Launching 서비스에 등록된 Launching 정보 및 로직을 가져오거나, **내보내기** 탭의 **JSON 형식으로 복사하기**로 복사한 JSON 형식의 데이터로부터 가져올 수 있습니다.

다른 프로젝트를 선택한 후, **가져오기 실행** 버튼을 클릭해 Launching 정보 및 로직을 가져올 수 있습니다.

**JSON 형식으로부터 로드** 메뉴에서 JSON 형식의 데이터로부터 Launching 정보 및 로직을 가져올 수도 있습니다.

> [참고]
> **가져오기**를 실행한 후 **설정 정보/로직** 탭에서 Launching 정보 및 로직을 확인하고 테스트할 수 있습니다. 가져오기를 실행하면 **배포** 탭에서 배포를 진행해야 서버에 반영됩니다.

## 내보내기

**내보내기** 탭에서 다른 프로젝트의 Launching 서비스로 Launching 정보 및 로직을 내보내거나, JSON 형식의 데이터로 복사할 수 있습니다.

다른 프로젝트를 선택한 후, **내보내기 실행** 버튼을 클릭하면 Launching 정보 및 로직을 내보낼 수 있습니다.

**JSON 형식으로 복사하기** 메뉴에서 JSON 형식의 데이터를 복사할 수 있습니다.

## 배포

**설정 정보** 및 **로직** 탭에서 수정한 사항을 서버에 반영하려면 **배포** 탭에서 배포를 진행해야 합니다.
**배포** 탭에서는 배포하기 전 그림과 같이 Launching 정보 및 로직, 설명의 수정 사항을 확인할 수 있습니다.

![console_deploy_00](https://static.toastoven.net/prod_launching/ko/console_deploy_00.png)

**배포** 버튼을 클릭해 배포를 진행하면 서버에 반영되어 모바일 앱에서 변경된 Launching 정보를 가져가게 됩니다.
**초기화** 버튼을 클릭해 Console에서 수정한 내역을 다시 되돌릴 수 있습니다.

배포를 진행하면 Console에서 수정하기 직전의 Launching 정보와 로직을 백업합니다. **배포** 버튼을 클릭하면 백업할 이름을 지정해야 합니다.

### 백업 내역 확인

![console_deploy_01](https://static.toastoven.net/prod_launching/ko/console_deploy_01.png)

하단 백업 내역에서 현재까지 백업된 내역을 확인할 수 있습니다.

**설정 정보/로직 확인** 버튼을 클릭해 백업된 Launching 정보와 로직을 확인할 수 있고, 복원 또는 삭제할 수 있습니다.