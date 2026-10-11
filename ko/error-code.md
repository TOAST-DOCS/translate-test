## Game > Launching > 오류 코드
## 오류 코드

오류 코드는 Response body(응답 본문)의 header에 있는 resultCode 및 resultMessage의 의미를 설명합니다.

| Result Code | Result Message | 설명 |
| --- | --- | --- |
| 0 | Success | 요청 성공 |
| 10001 | CONFIGURATION_GET_FAILED | Launching 정보 조회 실패 |
| 90020 | APPKEY_VERIFICATION_FAILED | 등록되지 않은 AppKey |
| 90404 | CONFIGURATION_PATH_NOT_FOUND | 주어진 서브 키에 대응되는 Launching 데이터를 찾을 수 없음 |
| -1 | FAIL | 미확인 오류 |

> [참고]
> 그 외 일반적인 오류 코드의 추가 정보는 "[Hypertext Transfer Protocol (HTTP) Status Code Registry](http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml)"에서 확인하시기 바랍니다.