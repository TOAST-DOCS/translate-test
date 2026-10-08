<!-- pre-align:aligned sig=39caf24ddae0 -->

<a id="management-certificate-manager-release-notes"></a>
## Management > Certificate Manager > リリースノート { #management-certificate-manager-release-notes }

<a id="july-28-2026"></a>
### 2026. 07. 28. { #july-28-2026 }
<a id="july-28-2026-feature-updates"></a>
#### 機能改善
* Certificate Manager API v1.3の証明書一覧照会APIのレスポンスに証明書IDが追加されました。
* Certificate Manager API v1.3に証明書IDを利用した証明書ダウンロードAPIが追加されました。
    * 詳細は[API v1.3ガイド](./api-guide-v1.3/)で確認できます。
* 通知グループ > 受信グループが**通知受信グループ管理**に移行されました。

<a id="april-14-2026"></a>
### 2026. 04. 14. { #april-14-2026 }
<a id="april-14-2026-api-v11-authentication-and-permission-updates"></a>
#### API v1.1 認証及び権限の修正
* Certificate Manager API v1.1 ガイドの認証及び権限情報が修正されました。
* APIを使用するためには、**Certificate Manager ADMINロール**または**Certificate Manager VIEWERロール**が必要です。
* 詳細は[API v1.1 ガイド](./api-guide-v1.1/)で確認できます。

<a id="march-10-2026"></a>
### 2026. 03. 10. { #march-10-2026 }
<a id="march-10-2026-added-a-api-version"></a>
#### APIバージョンの追加
* トークン認証方式をサポートするCertificate Manager API v1.3が追加されました。
  <br> 詳細はAPI v1.3ガイドで確認できます。

<a id="november-25-2025"></a>
### 2025. 11. 25. { #november-25-2025 }
<a id="november-25-2025-feature-updates"></a>
#### 機能改善
* 証明書名の制約が変更され、旧証明書と新規証明書を一緒に管理できるようになりました。
    * 証明書名が証明書ファイルのCN(CommonName)値と同一でなくても、プロジェクト内で一意の名前であれば登録できます。
* 証明書のDomains [CN(CommonName) + SAN(SubjectAlternativeNames)]項目が追加されました。
    * Domains情報は、証明書ファイルのアップロード時に自動で収集されます。
* 証明書タイプ(Single, Wildcard, SAN)が削除されました。
* 証明書一覧及び詳細情報のUIが変更されました。
* 詳細については、[コンソール利用ガイド](./console-guide/)で確認できます。

<a id="march-26-2024"></a>
### 2024. 03. 26. { #march-26-2024 }
<a id="march-26-2024-add-a-new-api-version"></a>
#### APIバージョン追加
* Certificate ManagerのAPI v1.1が追加されました。 <br>詳細はAPI v1.1ガイドでご確認ください。

<a id="february-27-2024"></a>
### 2024. 02. 27. { #february-27-2024 }
<a id="february-27-2024-added-the-feature-to-set-who-receives-notification-emails"></a>
#### 通知メール受信先設定機能を追加
* 組織/プロジェクトダッシュボード > 通知管理で受信メールアドレス名を設定できるように機能が追加されました。

<a id="march-28-2023"></a>
### 2023. 03. 28. { #march-28-2023 }
<a id="march-28-2023-feature-updates"></a>
#### 機能改善
* 証明書登録時に選択したファイルが証明書ファイル(.pem)ではない場合、`証明書ファイルは「.pem」拡張子ファイルのみアップロードできます。`メッセージが表示されるように改善しました。
* 証明書のパスフレーズの値を最大200文字まで入力できるように制限しました。
<a id="march-28-2023-bug-fixes"></a>
#### バグ修正
* ユーザーデータ修正後、修正ボタンが無効になる問題を修正しました。

<a id="february-28-2023"></a>
### 2023. 02. 28. { #february-28-2023 }
<a id="february-28-2023-added-features"></a>
#### 機能追加
* SAN証明書機能が追加されました。
  * SAN(subject alternative name)は1つの証明書で複数のドメインにSSLを適用できる証明書です。
  * SAN証明書を登録してサブ証明書の有効期限と通知設定を簡単に管理できます。
  * SAN証明書を追加または修正する時、証明書ファイル(.pem)の情報を読み取り証明書名とサブ証明書名を自動的に入力します。

<a id="february-28-2023-feature-updates"></a>
#### 機能改善
* ユーザーデータ名を空白にできないように改善しました。

<a id="january-31-2023"></a>
### 2023. 01. 31. { #january-31-2023 }
<a id="january-31-2023-feature-updates"></a>
#### 機能改善
* ユーザーデータの最大長さを3,000文字から700文字に制限しました。
* ドメインの名前ルールが変更されました。
    * ドメインの最初と最後、dot(.)とdot(.)の間を63文字に制限しました。
    * ドメインの最大長さを260文字に制限しました。
<a id="january-31-2023-bug-fixes"></a>
#### バグ修正
* メール通知時、通知グループとユーザーデータ名がhtmlフォーマットの場合、htmlフォーマットが適用される問題を修正しました。

<a id="december-27-2022"></a>
### 2022. 12. 27. { #december-27-2022 }
<a id="december-27-2022-feature-updates"></a>
#### 機能改善
* 検索バーの**初期化**ボタンをクリックすると、すべてのオプションが選択されるように改善しました。
* ドロップダウンリストで検索オプションを選択した後、適用ボタンをクリックせずにドロップダウンリストを閉じた場合にも選択したオプションが適用されるように改善しました。
* ドメインで自動収集機能が動作しない場合、登録者および登録機関項目に`-`記号が表示されるように改善しました。
* SMS通知で組織名が追加され、案内文言が短縮されました。
<a id="december-27-2022-bug-fixes"></a>
#### バグ修正
ドメイン追加ページに再び移動すると、有効期限が以前に設定した値に設定される問題を修正しました。

<a id="october-25-2022"></a>
### 2022. 10. 25. { #october-25-2022 }
<a id="october-25-2022-feature-updates"></a>
#### 機能改善
* プロジェクト統合アプリケーションキーを利用したAPI呼び出しが正常に動作しない問題を修正しました。
* ドメイン/証明書収集に失敗した時、当日確認件についてのみメールが送信されるようにロジックを修正しました。

<a id="october-4-2022"></a>
### 2022. 10. 04. { #october-4-2022 }
<a id="october-4-2022-feature-updates"></a>
#### 機能改善
* 役割グループ管理から権限を付与する場合に、権限が正常に適されない問題を修正しました。

<a id="august-23-2022"></a>
### 2022. 08. 23. { #august-23-2022 }
<a id="august-23-2022-feature-updates"></a>
#### 機能改善
* APIエンドポイントのドメインがapi-certificate-manager.cloud.toast.comからcertmanager.api.nhncloudservice.comに変更されました。

<a id="march-24-2020"></a>
### 2020. 03. 24. { #march-24-2020 }
<a id="march-24-2020-added-features"></a>
#### 機能追加
Certificate Managerに追加した証明書のリストを照会できるAPIを追加しました。
* [API]証明書リスト照会APIを追加

<a id="january-21-2020"></a>
### 2020. 01. 21. { #january-21-2020 }
<a id="january-21-2020-new-releases"></a>
#### サービスリリース
Certificate Managerは、有効期限の延長を逃さないように、有効期限が近づいたらアラーム(SMS、EMAIL)を送信するサービスです。
有効期限が存在するTLS証明書/ドメイン/ユーザーデータ(例：ライセンス)を管理し、有効期限に応じたアラーム送信ルールとアラーム受信ユーザーを指定できます。
