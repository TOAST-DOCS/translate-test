<!-- pre-align:aligned sig=c775a568be8f -->

# 問題解決ガイド
**Security > Secure Key Manager > 問題解決ガイド**

Secure Key Managerを使用中に発生することがある主な問題に対する解決方法を説明します。

<a id="api-call-failure-returns-invalid-appkey-error-message"></a>
## APIの呼び出しが失敗し、Invalid Appkeyエラーメッセージが返されます。 { #api-call-failure-returns-invalid-appkey-error-message }
* APIの呼び出しに使用したアプリケーションキーが無効な時に発生します。
    * Secure Key Manager管理ページのURL & Appkeyウィンドウに表示される正しいアプリケーションキーを使用しているかを確認してください。

<a id="api-call-failure-returns-invalid-key-id-error-message"></a>
## APIの呼び出しが失敗し、Invalid Key Idエラーメッセージが返されます。 { #api-call-failure-returns-invalid-key-id-error-message }
* APIの呼び出しに使用したKey Idが無効な時に発生します。
    * 正しいKey Idを使用しているかを確認してください。
    * Keyが使用中の状態かを確認してください。
    
<a id="api-call-failure-returns-invalid-key-version-error-message"></a>
## APIの呼び出しが失敗し、Invalid Key Versionエラーメッセージが返されます。 { #api-call-failure-returns-invalid-key-version-error-message }
* APIの呼び出しに使用したKey Versionが無効な時に発生します。
    * 対称鍵復号APIで発生した場合、暗号化した時に使用していた鍵バージョンが存在するかを確認してください。
    * 非対称鍵検証APIで発生した場合、署名した時に使用していた鍵バージョンが存在するかを確認してください。

<a id="api-call-failure-returns-invalid-user-data-error-message"></a>
## APIの呼び出しが失敗し、Invalid User Dataエラーメッセージが返されます。 { #api-call-failure-returns-invalid-user-data-error-message }
* APIの呼び出しに使用したユーザーデータが無効な時に発生します。
    * 対称鍵復号APIで発生した場合、復号対象データが正しいかを確認してください。
    * 非対称鍵検証APIで発生した場合、署名値が正しいかを確認してください。

<a id="api-call-failure-returns-invalid-key-status-error-message"></a>
## APIの呼び出しが失敗し、Invalid Key Statusエラーメッセージが返されます。 { #api-call-failure-returns-invalid-key-status-error-message }
* APIの呼び出しに使用したKeyの状態が無効な時に発生します。
    * 対称鍵復号APIで発生した場合、暗号化した時に使用した鍵が'使用中'の状態かを確認してください。
    * 非対称鍵検証APIで発生した場合、署名した時に使用していた鍵が'使用中'の状態かを確認してください。

<a id="api-call-failure-returns-invalid-key-version-status-error-message"></a>
## APIの呼び出しが失敗し、Invalid Key Version Statusエラーメッセージが返されます。 { #api-call-failure-returns-invalid-key-version-status-error-message }
* APIの呼び出しに使用したKey Versionの状態が無効な時に発生します。
    * 対称鍵復号APIで発生した場合、暗号化した時に使用していた鍵バージョンが'使用中'の状態かを確認してください。
    * 非対称鍵検証APIで発生した場合、署名した時に使用していた鍵バージョンが'使用中'の状態かを確認してください。
    
<a id="api-call-failure-returns-ipv4-auth-failure-error-message"></a>
## APIの呼び出しが失敗し、IPv4 Auth Failureエラーメッセージが返されます。 { #api-call-failure-returns-ipv4-auth-failure-error-message }
* IPv4アドレス認証に失敗した時に発生します。
    * APIを呼び出すクライアントのIPv4アドレスをSecure Key Managerに登録したかを確認してください。
    * Secure Key Managerに登録したクライアントのIPv4アドレスが'使用中'の状態かを確認してください。

<a id="api-call-failure-returns-mac-auth-failure-error-message"></a>
## APIの呼び出しが失敗し、MAC Auth Failureエラーメッセージが返されます。 { #api-call-failure-returns-mac-auth-failure-error-message }
* MACアドレス認証に失敗した時に発生します。
    * APIを呼び出すクライアントのMACアドレスをSecure Key Managerに登録しているかを確認してください。
    * Secure Key Managerに登録したクライアントのMACアドレスが'使用中'の状態かを確認してください。
    * APIを呼び出す時、X-TOAST-CLIENT-MAC-ADDRリクエストヘッダにクライアントのMACアドレスを追加したかを確認してください。

<a id="api-call-failure-returns-certificate-auth-failure-error-message"></a>
## APIの呼び出しが失敗し、Certificate Auth Failureエラーメッセージが返されます。 { #api-call-failure-returns-certificate-auth-failure-error-message }
* クライアント証明書の認証に失敗した時に発生します。
    * Secure Key Managerで発行した証明書を使用しているかを確認してください。
    * Secure Key Managerに登録した証明書が'使用中'の状態かを確認してください。

<a id="api-call-failure-returns-certificate-related-error-messages"></a>
## APIの呼び出しが失敗し、証明書関連エラーメッセージが返されます。 { #api-call-failure-returns-certificate-related-error-messages }
* 証明書が不正な時に発生します。
    * Secure Key Managerで発行した証明書を使用しているかを確認してください。
    * 証明書の有効期限を確認してください。

<a id="api-call-failure-returns-url-not-found-error-message"></a>
## API呼び出しが失敗し、URL NOT FOUNDエラーメッセージを返します。 { #api-call-failure-returns-url-not-found-error-message }
* 正しくないURLでリクエストした場合に発生します。
    * 正しいURLを使用しているかご確認ください。
        
<a id="api-call-failure-returns-url-not-found-error-message-for-any-other-errors-that-occur-during-an-api-request-contact-us-at-customer-support-contact-us"></a>
#### その他のAPIリクエスト中に発生したエラーについては、顧客サポート > [お問い合わせ](https://www.nhncloud.com/KR/support/inquiry)へお問い合わせください
