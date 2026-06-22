<!-- pre-align:aligned sig=abf088ebdb6d -->

## Data & Analytics > DataQuery > リリースノート

<a id="may-27-2026"></a>

## 2026. 05. 27.

<a id="added-integration-services"></a>

### 連携サービスの追加

* データソースのタイプにData Lake Storageを追加しました。
<a id="april-28-2026"></a>

## 2026. 04. 28.

<a id="added-integration-services-2"></a>

### 連携サービスの追加
* Cloud Schedulerサービスに「予約されたクエリ」テンプレートを追加しました。
  * テンプレートを使用して、クエリを任意のスケジュールで実行できます。

<a id="march-24-2026"></a>

## 2026. 03. 24.

<a id="feature-updates"></a>

### 機能改善・変更
* コンソールクエリ結果の表示ポリシーを改善
  * コンソールで実行したクエリ結果を1MB、5,000行以内で表示していた制限を削除しました。
  * コンソールで実行したクエリ結果を最大30MBまで表示できるように改善しました。
  * コンソールクエリ結果を照会し、コピーするボタンを追加しました。
  
<a id="september-23-2025"></a>

## 2025. 09. 23.

<a id="trino-version-upgrade"></a>

### Trinoバージョンのアップグレード
* DataQueryのサービス基盤をTrino 476バージョンにアップグレードしました。
* これには、一部のクエリにおけるパフォーマンス向上とバグ修正が含まれています。

<a id="june-24-2025"></a>

## 2025. 06. 24.

<a id="added-features"></a>

### 機能追加
* クラスターの状態指標視覚化領域を追加しました。
  * 2025年6月24日以降に開始されたクラスターの状態を収集します。
  
<a id="may-27-2025"></a>

## 2025. 05. 27.

<a id="added-features-2"></a>

### 機能追加
* Object Storageデータソースと連動するためのメタストアのインスタンスタイプを設定する機能を追加しました。

<a id="january-21-2025"></a>

## 2025. 01. 21.

<a id="feature-updates-2"></a>

### 機能改善・変更
* DataQueryをTrino 462バージョンに基づいてサービスするようにアップグレードしました。
* iceberg connectorに関するadd_files_with_partition関数を追加しました。

<a id="october-29-2024"></a>

## 2024. 10. 29.

<a id="trino-version-upgrade-2"></a>

### Trinoバージョンのアップグレード
* DataQueryをTrino 455バージョンをベースにサービスするようにアップグレードしました。
* 一部のクエリの性能向上とバグ修正が含まれています。

<a id="added-features-3"></a>

### 機能追加

* データソースタイプにIcebergを追加しました。

<a id="july-23-2024"></a>

## 2024. 07. 23.

<a id="feature-updates-3"></a>

### 機能改善・変更
* クエリ履歴を保存するためのObject Storage認証情報の有効期限が切れると、連動無効化案内メールが送信されるようになりました。

<a id="june-25-2024"></a>

## 2024. 06. 25.

<a id="added-features-4"></a>

### 機能追加
* データソースタイプにMariaDBが追加されました。
* クエリ履歴保存機能が追加されました。

<a id="may-28-2024"></a>

## 2024. 05. 28.

<a id="feature-updates-4"></a>

### 機能改善・変更
* クエリ情報の保存期限を90日に変更しました。

<a id="may-1-2024"></a>

## 2024. 05. 01.

<a id="feature-updates-5"></a>

### 機能改善・変更
* Object Storageデータソースの最大登録制限を5個に変更しました。
* Object Storageデータソースの最小登録制限を削除しました。

<a id="february-27-2024"></a>

## 2024. 02. 27.

<a id="feature-updates-6"></a>

### 機能追加
* ユーザーがよく使うクエリを保存・管理できる機能が追加されました。

<a id="january-23-2024"></a>

## 2024. 01. 23.

<a id="trino-version-upgrade-3"></a>

### Trinoバージョンのアップグレード

* DataQueryで提供するTrinoバージョンが398から434にアップグレードされました。
* データソースのタイプにPostgreSQL、Oracle、EDBが追加されました。

<a id="october-31-23"></a>

## 2023. 10. 31.

<a id="feature-updates-7"></a>

### 機能改善・変更
* クラスタタイプ選択機能を追加しました。

<a id="december-27-2022"></a>

## 2022. 12. 27.

<a id="release-of-a-new-service"></a>

### 新規サービスのリリース

* 分散SQLクエリエンジンTrinoを使って大規模データに対してクエリを実行できるサービスです。
* データソースとしてNHN Cloud Object Storage、NHN Cloud RDS for MySQLをサポートします。
