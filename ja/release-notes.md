<!-- pre-align:aligned sig=263cd1eadb32 -->

<a id="security-secure-key-manager-release-notes"></a>
## Security > Secure Key Manager > リリースノート { #security-secure-key-manager-release-notes }

<a id="june-9-2026"></a>
### 2026. 06. 09. { #june-9-2026 }
<a id="june-9-2026-added-features"></a>
#### 新機能追加
  * キーストアの作成/変更/削除APIを追加(v1.3)
    * APIを利用してキーストアを作成、変更、削除できる機能を追加しました。詳細については[API v1.3 ガイド](/Security/Secure%20Key%20Manager/ko/api-guide-v1.3/)をご参照ください。
    
<a id="may-27-2026"></a>
### 2026. 05. 27. { #may-27-2026 }
<a id="may-27-2026-added-features"></a>
#### 新機能追加
  * 非対称鍵標準スキーム署名/検証API追加(v1.3)
    * 標準RSA署名スキーム(RSASSA-PSS、RSASSA-PKCS1-v1_5)に従って非対称鍵でデータを署名し、検証できるAPIを追加。詳細は[API v1.3ガイド](/Security/Secure%20Key%20Manager/ja/api-guide-v1.3/)を参照。
<a id="may-27-2026-feature-updates"></a>
#### 機能改善・変更
  * キーストア認証方式の組み合わせオプション追加
    * キーストアで有効になっている複数の認証方法(IPv4アドレス、MACアドレス、クライアント証明書)を組み合わせる方式を選択できる機能を追加。全て通過(AND、デフォルト値)または1つのみ通過(OR)から選択でき、既存のキーストアは全て通過(AND)として維持されます。詳細は[コンソール使用ガイド](/Security/Secure%20Key%20Manager/ja/console-guide/)を参照。
    
<a id="april-14-2026"></a>
### 2026. 04. 14. { #april-14-2026 }
<a id="april-14-2026-feature-updates"></a>
#### 機能改善・変更
  * `APPROVAL MEMBER` ロールの削除
    * Secure Key Manager APPROVAL MEMBERロールをSecure Key Manager ADMINロールに移行し、ロール体系を簡素化
  * 権限の細分化
    * `SecureKeyManager:API.ADMIN`、`SecureKeyManager:API.VIEWER`権限を追加し、コンソールおよびAPIの権限を細分化して管理できるよう変更

<a id="march-10-2026"></a>
### 2026. 03. 10. { #march-10-2026 }
<a id="march-10-2026-added-features"></a>
#### 新規機能の追加
  * API v1.3の追加
    * `X-NHN-AUTHORIZATION`ヘッダによるトークン認証方式の追加。詳細は[API v1.3 ガイド](/Security/Secure%20Key%20Manager/ko/api-guide-v1.3/)を参照。
  * 機密データ修正APIの追加(v1.2、v1.3)
    * APIを利用してSecure Key Managerに保存した機密データを修正できる機能の追加。詳細は[API v1.2 ガイド](/Security/Secure%20Key%20Manager/ko/api-guide-v1.2/)または[API v1.3 ガイド](/Security/Secure%20Key%20Manager/ko/api-guide-v1.3/)を参照。
    
<a id="february-10-2026"></a>
### 2026. 02. 10. { #february-10-2026 }
<a id="february-10-2026-new-features"></a>
#### 新機能の追加
  * キーストアリスト詳細照会APIの追加
    * APIを利用して、キーストアの詳細情報リストを照会できる機能を追加。詳細は[API v1.0ガイド](/Security/Secure%20Key%20Manager/ko/api-guide-v1.0/)または[API v1.2ガイド](/Security/Secure%20Key%20Manager/ko/api-guide-v1.2/)を参照。
  * キーリスト詳細照会APIの追加
    * APIを利用して、キーの詳細情報リストを照会できる機能を追加。詳細は[API v1.0ガイド](/Security/Secure%20Key%20Manager/ko/api-guide-v1.0/)または[API v1.2ガイド](/Security/Secure%20Key%20Manager/ko/api-guide-v1.2/)を参照。

<a id="june-24-2025"></a>
### 2025. 06. 24. { #june-24-2025 }
<a id="june-24-2025-feature-updates"></a>
#### 機能改善/変更
  * 新規エラーメッセージ追加
    * 有効ではないURIでAPIリクエストを行った際のエラーメッセージを追加。詳細は[トラブルシューティング](/Security/Secure%20Key%20Manager/ja/troubleshooting-guide/#api-call-failure-returns-url-not-found-error-message)を参照。

<a id="april-28-2025"></a>
### 2025. 04. 28. { #april-28-2025 }
<a id="april-28-2025-feature-updates"></a>
#### 機能改善/変更
  * データ保管期限を3年から1年に変更
    * [関連告知](https://www.nhncloud.com/kr/support/notice/detail/6493)

<a id="march-25-2025"></a>
### 2025. 03. 25. { #march-25-2025 }
<a id="march-25-2025-added-new-features"></a>
#### 新機能追加
  * キーストアリスト/詳細照会API追加
    * APIを利用してキーストアのIDリスト及びキーストアIDを通じてキーストアの詳細情報を照会する機能を追加
  * キーリスト/詳細照会APIを追加
    * APIを利用してキーIDリスト及びキーIDを通じてキーの詳細情報を照会する機能を追加
  * 認証情報リスト/詳細照会APIを追加
    * APIを利用して認証情報の値リスト及び認証情報の値を通じて認証情報を詳細に照会する機能を追加

<a id="september-25-2024"></a>
### 2024. 09. 25. { #september-25-2024 }
<a id="september-25-2024-feature-updates"></a>
#### 機能改善/変更
  * 承認リストの表からNumber列を削除

<a id="august-27-2024"></a>
### 2024. 08. 27. { #august-27-2024 }
<a id="august-27-2024-added-new-features"></a>
#### 新機能追加
  * Secure Key Managerのイベント通知をResource Watcherサービスで受信できる機能を追加
<a id="august-27-2024-feature-updates"></a>
#### 機能改善/変更
  * 承認プロセスの自己承認機能を削除
    * 本人がリクエストした件を承認できないように変更

<a id="april-23-2024"></a>
### 2024. 04. 23. { #april-23-2024 }
<a id="april-23-2024-bug-fixes"></a>
#### バグ修正
  * API を利用してデータ(キー、認証情報)を削除し、削除されたデータを照会する場合、エラーモーダルウィンドウが表示された後、更新前までは削除していないデータも照会できないエラーを修正しました。

<a id="march-26-2024"></a>
### 2024. 03. 26. { #march-26-2024 }
<a id="march-26-2024-added-new-features"></a>
#### 新規機能追加
  * 認証情報登録/削除API追加
    * PIを利用してキーを使用するための認証情報を登録または削除する機能を追加しました。
    * APIを利用して認証情報を追加または削除するには、**User Access Key ID** と **Secret Access Key** が必要です。詳細は[User Access Key](/nhncloud/ja/public-api/user-access-key)を参照してください。

<a id="february-27-2024"></a>
### 2024. 02. 27. { #february-27-2024 }
<a id="february-27-2024-added-new-features"></a>
#### 新規機能追加
  * 通知メール受信対象設定機能を追加
    * 組織/プロジェクトダッシュボード > 通知管理で、受信メールのアドレス名を設定できる機能が追加されました。
<a id="february-27-2024-feature-updates"></a>
#### 機能改善/変更
  * キーストアID表示
    * キーストア詳細情報でキーストアIDを確認できる領域を表示
    * キーストアID右側のさらに表示ボタンを通じてキーストアIDをコピーできる機能を追加

<a id="november-28-2023"></a>
### 2023. 11. 28. { #november-28-2023 }
<a id="november-28-2023-added-new-features"></a>
#### 新規機能追加
  * キー追加/削除API追加
    * APIを利用してキーを追加または削除する機能を追加
    * APIを利用してキーを追加または削除するには **User Access Key ID** と **Secret Access Key** が必要。詳細は[User Access Key](/nhncloud/ja/public-api/user-access-key)を参照。

<a id="september-26-2023"></a>
### 2023. 09. 26. { #september-26-2023 }
<a id="september-26-2023-feature-updates"></a>
#### 機能改善/変更
  * IPv4帯域幅認証機能を追加
    * IPv4で認証時、CIDR表記による帯域幅認証機能を追加

<a id="july-25-2023"></a>
### 2023. 07. 25. { #july-25-2023 }
<a id="july-25-2023-bug-fixes"></a>
#### バグ修正
  * 承認プロセス証明書キャンセル機能のエラーを修正
    * 承認プロセスで**使用中**状態の証明書に対して削除を要求した後、要求をキャンセルする際に、元の**使用中**状態ではなく**削除キャンセル予定**状態と表示されるエラーを修正しました。

<a id="may-30-2023"></a>
### 2023. 05. 30. { #may-30-2023 }
<a id="may-30-2023-bug-fixes"></a>
#### バグ修正
  * 承認プロセス通知(メール)機能のエラーを修正
    * 承認権限を持つ一部の管理者が通知(メール)を受信できないエラーを修正
  * 承認プロセスIP/MAC大容量登録機能のエラーを修正
    * 承認プロセスIP/MAC大容量登録時、画面にすぐに反映されないエラーを修正

<a id="april-25-2023"></a>
### 2023. 04. 25. { #april-25-2023 }
<a id="april-25-2023-added-new-features"></a>
#### 新規機能追加
  * 承認プロセス通知(メール)機能の追加
    * 承認リクエスト登録時、承認権限を持っている権限者にメールを転送する機能を追加

<a id="february-28-2023"></a>
### 2023. 02. 28. { #february-28-2023 }
<a id="february-28-2023-bug-fixes"></a>
#### バグ修正
  * テンプレートファイルのダウンロードエラーを修正
    * 大量登録テンプレートファイルが誤った形式のテンプレートとしてダウンロードされるエラーを修正

<a id="january-31-2023"></a>
### 2023. 01. 31. { #january-31-2023 }
<a id="january-31-2023-bug-fixes"></a>
#### バグ修正
  * 承認機能改善およびエラー修正
    * 承認機能使用中に機密データ修正画面に移動した時、データ領域が空で表示されるように修正
    * 承認機能使用中に機密データを修正した後、修正されたデータが表示されるように修正
  * キーストア管理タブでMACアドレスのツールチップ文言にMACアドレスではなくIPv4が表示される問題を修正

<a id="december-27-2022"></a>
### 2022. 12. 27. { #december-27-2022 }
<a id="december-27-2022-feature-updates"></a>
#### 機能改善/変更
  * APIドメイン変更
    * SecureKeyManager APIドメインを`api-keymanager.cloud.toast.com`から`api-keymanager.nhncloudservice.com`に変更

<a id="november-29-2022"></a>
### 2022. 11. 29. { #november-29-2022 }
<a id="november-29-2022-bug-fixes"></a>
#### バグ修正
  * 承認機能の改善とエラー修正
    * 承認機能の使用中に発生するエラーメッセージの文言を理解しやすくしました
    * 承認機能の使用中にキー保存場所を最初に追加した時、承認手順なしで追加されるエラーを修正
  * 証明書認証エラーの修正
    * 証明書で認証する時、断続的に失敗する問題を修正

<a id="october-25-2022"></a>
### 2022. 10. 25. { #october-25-2022 }
<a id="october-25-2022-bug-fixes"></a>
#### バグ修正
  * 統合アプリケーションキーエラーを修正
    * プロジェクト統合アプリケーションキーを利用したAPI呼び出しが正常に動作しない問題を修正
  * 承認機能エラーを修正
    * 承認機能を使用した時、キーバージョン別削除機能が正常に動作しない問題を修正

<a id="september-27-2022"></a>
### 2022. 09. 27. { #september-27-2022 }
<a id="september-27-2022-added-new-features"></a>
#### 新規機能追加
  * 非対称鍵照会機能を追加
    * 鍵バージョン別の非対称鍵照会機能を追加

<a id="july-26-2022"></a>
### 2022. 07. 26. { #july-26-2022 }
<a id="july-26-2022-added-new-features"></a>
#### 新規機能追加
  * 承認機能追加
    * キー作成、修正、削除およびキー保存場所のアクセス制御変更など、主要変更事項に対する承認手続きを導入可能
  * 新しい対称鍵照会バージョンを追加
    * キーバージョン別対称鍵照会機能を追加

<a id="november-23-2021"></a>
### 2021. 11. 23. { #november-23-2021 }
<a id="november-23-2021-added-new-features"></a>
#### 新規機能追加
  * 対称鍵照会機能を追加

<a id="october-26-2021"></a>
### 2021. 10. 26. { #october-26-2021 }
<a id="october-26-2021-added-new-features"></a>
#### 新規機能追加
  * キーインポート機能の追加
    * 対称鍵インポート機能の追加
<a id="october-26-2021-feature-updates"></a>
#### 機能改善/変更
  * 機密データ照会機能の修正
    * Webコンソールで機密データの照会時、フィールドをマスキングして提供
<a id="october-26-2021-bug-fixes"></a>
#### バグ修正
  * 未払いユーザーなのに正常にサービスを利用できていた問題を修正

<a id="september-28-2021"></a>
### 2021. 09. 28. { #september-28-2021 }
<a id="september-28-2021-bug-fixes"></a>
#### バグ修正
  * 権限グループを利用して付与した権限の場合、認識が正常にできなかった問題を修正
  * 使用履歴初期化ボタンが正常に動作しなかった問題を修正

<a id="march-24-2020"></a>
### 2020. 03. 24. { #march-24-2020 }
<a id="march-24-2020-added-new-features"></a>
#### 新規機能追加
  * ユーザーがSecure Key Managerコンソールで作業した内容をCloud Trailに記録
  * CSVファイルを使用した認証データ(IPv4アドレス/MACアドレス)の大量登録機能を追加
  * CSVファイルを使用した認証データ(IPv4アドレス/MACアドレス)のダウンロード機能を追加

<a id="december-24-2019"></a>
### 2019. 12. 24. { #december-24-2019 }
<a id="december-24-2019-added-new-features"></a>
#### 新規機能追加
  * 統計画面を追加
    * プロジェクト単位でAPI使用統計を照会できる画面を追加
<a id="december-24-2019-feature-updates"></a>
#### 機能改善/変更
  * キー保存場所の画面を改善
    * キー保存場所リストの表示方式を変更
    * キー保存場所の下位メニューを変更
    * キー保存場所にクイックメニューを追加
  * 使用履歴画面を改善
    * プロジェクト単位でAPIの使用履歴を照会できるように変更

<a id="july-23-2019"></a>
### 2019. 07. 23. { #july-23-2019 }
<a id="july-23-2019-feature-updates"></a>
#### 機能改善/変更
  * UI改善
    * テキストとボタンが重なって表示される現象を修正
    * 日本語で画面を表示する時、テキストが改行される現象を修正

<a id="may-28-2019"></a>
### 2019. 05. 28. { #may-28-2019 }
<a id="may-28-2019-release-of-new-service"></a>
#### サービスリリース
  * 機密データ、対称鍵、非対称鍵などをアプリケーションサーバーに保存する場合、危険にさらされることがあるデータを中央集中的に安全に管理し、認証をパスしたクライアントのみアクセスできるように制御するサービスです。
