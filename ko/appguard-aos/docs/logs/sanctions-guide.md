<!-- pre-align:aligned sig=fbe508816555 -->

# 제재 가이드

<a id="a-sanctioned-by-detection-log"></a>
## A. 탐지 로그를 통한 제재 { #a-sanctioned-by-detection-log }

NHN AppGuard를 통한 탐지 로그와 앱 자체 여러 로그들을 종합하여 제재를 진행하는 것을 권장합니다.


<a id="b-register-the-callback-function-and-proceed-with-processing-from-the-server-side"></a>
## B. 콜백 함수를 등록하여 서버 측에서 제재 등 처리 진행 { #b-register-the-callback-function-and-proceed-with-processing-from-the-server-side }

콜백 함수를 등록하면, NHN AppGuard의 탐지 결과를 얻을 수 있습니다([연동 API 호출](../sdk/java.md#콜백-함수-등록) 참고).

<a id="recommended-sanction-method"></a>
### 권장 제재 방식 { #recommended-sanction-method }

- **차단 시**: 탐지된 데이터를 서버로 전송하여 서버 측에서 연결을 종료하는 형태를 권장합니다.
- **비권장**: 클라이언트에서 종료하는 경우, 우회 가능성이 높아지기 때문에 권장하지 않습니다.

NHN AppGuard Block 기능으로 차단하는 경우에도 콜백 함수는 호출됩니다([8.2 콜백 데이터](callback-data.md) 참고).

<a id="c-enable-nhn-appguard-blocking"></a>
## C. NHN AppGuard 차단 기능 사용 { #c-enable-nhn-appguard-blocking }

웹 콘솔에서 차단 설정을 할 수 있습니다.

![](../assets/images/logs/sanctions-console-settings.png)

<a id="full-block"></a>
### 전체 차단 { #full-block }
**전체 차단으로 설정된 정책**으로 탐지될 경우:
- NHN AppGuard 안내 창이 나타남
- 앱이 종료됨

<a id="conditional-block"></a>
### 조건 차단 { #conditional-block }
**조건 차단 시 설정한 조건**으로 탐지될 경우:
- NHN AppGuard 안내 창이 나타남  
- 앱이 종료됨

<a id="d-enable-nhn-appguard-blacklist-feature"></a>
## D. NHN AppGuard 블랙리스트 기능 사용 { #d-enable-nhn-appguard-blacklist-feature }

웹 콘솔에서 블랙리스트를 설정할 수 있습니다.

![](../assets/images/logs/blacklist-settings.png)

등록된 블랙리스트 아이디로 앱을 실행하면 설정된 차단 기간 동안 NHN AppGuard 안내 창이 나타나고 앱이 종료됩니다.

아래는 차단될 경우 나타나는 대화 상자입니다.

![](../assets/images/logs/block-dialog.png)

!!! tip "알아두기"
    * Code 값 중 ‘_’ 앞 숫자가 콜백 데이터 값입니다.
    * 안내 메시지는 각 나라의 언어에 맞게 번역되어 표시됩니다.

---

