<!-- machine_translated: true -->

<!-- pre-align:aligned sig=fbe508816555 -->

# 制裁ガイド

<a id="a-sanctioned-by-detection-log"></a>
## A. 検知ログによる制裁 { #a-sanctioned-by-detection-log }

NHN AppGuardによる検知ログと、アプリ独自の様々なログを総合して制裁を行うことを推奨します。


<a id="b-register-the-callback-function-and-proceed-with-processing-from-the-server-side"></a>
## B. コールバック関数を登録してサーバー側で制裁などの処理を実行 { #b-register-the-callback-function-and-proceed-with-processing-from-the-server-side }

コールバック関数を登録すると、NHN AppGuardの検知結果を取得できます([連携APIの呼び出し](../sdk/java.md#コールバック関数の登録)を参照)。

<a id="recommended-sanction-method"></a>
### 推奨される制裁方式 { #recommended-sanction-method }

- **ブロック時**: 検知されたデータをサーバーに送信し、サーバー側で接続を終了する方式を推奨します。
- **非推奨**: クライアントで終了する場合、回避される可能性が高いため推奨しません。

NHN AppGuardのBlock機能を通じてブロックした場合でも、コールバック関数は呼び出されます([8.2 コールバックデータ](callback-data.md)を参照)。

<a id="c-enable-nhn-appguard-blocking"></a>
## C. NHN AppGuardのブロック機能の使用 { #c-enable-nhn-appguard-blocking }

Webコンソールでブロック設定ができます。

![](../assets/images/logs/sanctions-console-settings.png)

<a id="full-block"></a>
### 全体ブロック { #full-block }
**全体ブロックとして設定されたポリシー**で検知された場合:
- NHN AppGuardの案内ウィンドウが表示されます
- アプリが終了します

<a id="conditional-block"></a>
### 条件付きブロック { #conditional-block }
**条件付きブロックで設定した条件**で検知された場合:
- NHN AppGuardの案内ウィンドウが表示されます
- アプリが終了します

<a id="d-enable-nhn-appguard-blacklist-feature"></a>
## D. NHN AppGuardのブラックリスト機能の使用 { #d-enable-nhn-appguard-blacklist-feature }

Webコンソールでブラックリストを設定できます。

![](../assets/images/logs/blacklist-settings.png)

登録されたブラックリストIDでアプリを実行すると、設定されたブロック期間中、NHN AppGuardの案内ウィンドウが表示され、アプリが終了します。

以下は、ブロックされた場合に表示されるダイアログです。

![](../assets/images/logs/block-dialog.png)

!!! tip "「ポイント」"
    * Codeの値のうち、「_」の前の数字がコールバックのデータ値です。
    * 案内メッセージは、各国の言語に合わせて翻訳されて表示されます。

---

