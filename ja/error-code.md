## Game > Launching > エラーコード
## エラーコード

Response body(レスポンス本文)のheaderにあるresultCodeおよびresultMessageの意味を説明します。

| Result Code | Result Message | 説明 |
| --- | --- | --- |
| 0 | Success | リクエスト成功 |
| 10001 | CONFIGURATION_GET_FAILED | Launching情報の照会失敗 |
| 90020 | APPKEY_VERIFICATION_FAILED | 登録されていないAppKey |
| 90404 | CONFIGURATION_PATH_NOT_FOUND | 与えられたサブキーに対応するLaunchingデータが見つからない |
| -1 | FAIL | 未確認エラー |

> [参考]
> それ以外の一般的なエラーコードの追加情報は、"[Hypertext Transfer Protocol (HTTP) Status Code Registry](http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml)"で確認してください。
