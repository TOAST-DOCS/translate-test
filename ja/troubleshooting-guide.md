<!-- machine_translated: true -->

<!-- pre-align:aligned sig=c775a568be8f -->

# トラブルシューティングガイド
**Security > Secure Key Manager > トラブルシューティングガイド**

Secure Key Manager の使用中に発生する可能性がある主な問題とその解決方法について説明します。

<a id="api-call-failure-returns-invalid-appkey-error-message"></a>
## API 呼び出しが失敗し、Invalid Appkey エラーメッセージが返されます。 { #api-call-failure-returns-invalid-appkey-error-message }
* API 呼び出しに使用したアプリキーが無効な場合に発生します。
    * Secure Key Manager 管理ページの URL & Appkey ウィンドウに表示されている正しいアプリキーを使用しているか確認してください。

<a id="api-call-failure-returns-invalid-key-id-error-message"></a>
## API 呼び出しが失敗し、Invalid Key Id エラーメッセージが返されます。 { #api-call-failure-returns-invalid-key-id-error-message }
* API 呼び出しに使用した Key Id が無効な場合に発生します。
    * 正しい Key Id を使用しているか確認してください。
    * Key が使用中の状態であるか確認してください。

<a id="api-call-failure-returns-invalid-key-version-error-message"></a>
## API 呼び出しが失敗し、Invalid Key Version エラーメッセージが返されます。 { #api-call-failure-returns-invalid-key-version-error-message }
* API 呼び出しに使用した Key Version が無効な場合に発生します。
    * 対称鍵の復号 API で発生した場合、暗号化時に使用したキーバージョンが存在するか確認してください。
    * 非対称鍵の検証 API で発生した場合、署名時に使用したキーバージョンが存在するか確認してください。

<a id="api-call-failure-returns-invalid-user-data-error-message"></a>
## API 呼び出しが失敗し、Invalid User Data エラーメッセージが返されます。 { #api-call-failure-returns-invalid-user-data-error-message }
* API 呼び出しに使用したユーザーデータが無効な場合に発生します。
    * 対称鍵の復号 API で発生した場合、復号対象のデータが正しいか確認してください。
    * 非対称鍵の検証 API で発生した場合、署名値が正しいか確認してください。

<a id="api-call-failure-returns-invalid-key-status-error-message"></a>
## API 呼び出しが失敗し、Invalid Key Status エラーメッセージが返されます。 { #api-call-failure-returns-invalid-key-status-error-message }
* API 呼び出しに使用した Key のステータスが無効な場合に発生します。
    * 対称鍵の復号 API で発生した場合、暗号化時に使用したキーが「使用中」の状態であるか確認してください。
    * 非対称鍵の検証 API で発生した場合、署名時に使用したキーが「使用中」の状態であるか確認してください。

<a id="api-call-failure-returns-invalid-key-version-status-error-message"></a>
## API 呼び出しが失敗し、Invalid Key Version Status エラーメッセージが返されます。 { #api-call-failure-returns-invalid-key-version-status-error-message }
* API 呼び出しに使用した Key Version のステータスが無効な場合に発生します。
    * 対称鍵の復号 API で発生した場合、暗号化時に使用したキーバージョンが「使用中」の状態であるか確認してください。
    * 非対称鍵の検証 API で発生した場合、署名時に使用したキーバージョンが「使用中」の状態であるか確認してください。

<a id="api-call-failure-returns-ipv4-auth-failure-error-message"></a>
## API 呼び出しが失敗し、IPv4 Auth Failure エラーメッセージが返されます。 { #api-call-failure-returns-ipv4-auth-failure-error-message }
* IPv4アドレス認証に失敗した場合に発生します。
    * API を呼び出すクライアントの IPv4 アドレスを Secure Key Manager に登録しているか確認してください。
    * Secure Key Manager に登録したクライアントの IPv4 アドレスが「使用中」の状態であるか確認してください。

<a id="api-call-failure-returns-mac-auth-failure-error-message"></a>
## API 呼び出しが失敗し、MAC Auth Failure エラーメッセージが返されます。 { #api-call-failure-returns-mac-auth-failure-error-message }
* MACアドレス認証に失敗した場合に発生します。
    * API を呼び出すクライアントの MAC アドレスを Secure Key Manager に登録しているか確認してください。
    * Secure Key Manager に登録したクライアントの MAC アドレスが「使用中」の状態であるか確認してください。
    * API を呼び出す際に、X-TOAST-CLIENT-MAC-ADDR リクエストヘッダーにクライアントの MAC アドレスを追加しているか確認してください。

<a id="api-call-failure-returns-certificate-auth-failure-error-message"></a>
## API 呼び出しが失敗し、Certificate Auth Failure エラーメッセージが返されます。 { #api-call-failure-returns-certificate-auth-failure-error-message }
* クライアント証明書認証に失敗した場合に発生します。
    * Secure Key Manager で発行した証明書を使用しているか確認してください。
    * Secure Key Manager に登録した証明書が「使用中」の状態であるか確認してください。

<a id="api-call-failure-returns-certificate-related-error-messages"></a>
## API 呼び出しが失敗し、証明書関連のエラーメッセージが返されます。 { #api-call-failure-returns-certificate-related-error-messages }
* 証明書が正しくない場合に発生します。
    * Secure Key Manager で発行した証明書を使用しているか確認してください。
    * 証明書の有効期限を確認してください。

<a id="api-call-failure-returns-url-not-found-error-message"></a>
## API 呼び出しが失敗し、URL NOT FOUND エラーメッセージが返されます。 { #api-call-failure-returns-url-not-found-error-message }
* 正しくない URL でリクエストした場合に発生します。
    * 正しい URL を使用しているか確認してください。

<a id="api-call-failure-returns-url-not-found-error-message-for-any-other-errors-that-occur-during-an-api-request-contact-us-at-customer-support-contact-us"></a>
#### その他、API リクエスト中に発生したエラーについては、カスタマーサポート > [お問い合わせ](https://www.nhncloud.com/KR/support/inquiry)よりお問い合わせください。