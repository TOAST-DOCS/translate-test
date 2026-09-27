<!-- machine_translated: true -->

<!-- pre-align:aligned sig=5410a458e2ca -->

<a id="database-rds-for-mysql-release-notes"></a>
## Database > RDS for MySQL > リリースノート { #database-rds-for-mysql-release-notes }

<a id="september-15-2026"></a>
## 2026. 09. 15. { #september-15-2026 }

<a id="september-15-2026-added-features"></a>
### 機能追加 { #september-15-2026-added-features }

* MySQL 8.4.11バージョンを追加
* DBインスタンス再起動時に、OSを再起動するオプションを追加
* 高可用性インスタンスの停止機能を追加

<a id="september-15-2026-feature-updates"></a>
### 機能改善 { #september-15-2026-feature-updates }

* DBインスタンスタイプの用語変更
    * マスター → Primary
    * 予備マスター → Standby
    * リードレプリカ → Read Replica
    * フェイルオーバーしたマスター → Failed Over Primary
* DBインスタンスグループ単位で適用される属性は、DBインスタンスグループを修正するように改善
* セキュリティパッチ、OSアップグレード後に過去のモニタリング指標を確認できるように改善
* DBインスタンスタイプごとに通知を設定できるように改善

<a id="september-15-2026-bug-fixes"></a>
### 不具合の修正 { #september-15-2026-bug-fixes }

* CloudTrailにObject StorageのテナントIDがそのまま表示されるバグを修正
* バージョン8.4で`CREATE TABLE ... SELECT`構文の実行後の時点への時点復元ができないバグを修正
* セキュリティグループルールが多い場合に、セキュリティグループルールの作成・変更・削除が断続的に失敗するバグを修正
* 断続的にネットワーク通信の失敗により、高可用性DBが起動しない場合があるバグを修正
* DBポートの変更に失敗した際、断続的にガベージセキュリティグループルールが残存するバグを修正

<a id="july-14-2026"></a>
## 2026. 07. 14. { #july-14-2026 }

<a id="feature-updates"></a>
### 機能追加及び改善 { #feature-updates }

* MySQL 8.0.46、8.4.9バージョンを追加

<a id="bug-fixes"></a>
### 不具合の修正 { #bug-fixes }

* セキュリティパッチ対象の単一インスタンスを高可用性インスタンスに変更する際、セキュリティパッチが実行されない問題を修正

<a id="may-12-2026"></a>
## 2026. 05. 12. { #may-12-2026 }

<a id="may-12-2026-feature-updates"></a>
### 機能追加及び改善 { #may-12-2026-feature-updates }

* セキュリティパッチ機能を追加
    * OSで発見されたセキュリティの脆弱性(CVE)に対するセキュリティパッチを、メンテナンス作業として実行できます。
    * 詳細については、[セキュリティパッチ](/Database/RDS%20for%20MySQL/ja/db-instance/#security-patch)のドキュメントを参照してください。
* 高可用性Pingチェック方式に、従来の`INSERT`に加えて`SELECT`オプションを追加
* API v4.0の追加及び変更
    * 高可用性情報の照会APIが追加されます。

<a id="march-10-2026"></a>
## 2026. 03. 10. { #march-10-2026 }

<a id="march-10-2026-feature-updates"></a>
### 機能追加及び改善 { #march-10-2026-feature-updates }

* API v4.0の追加
    * 詳細については、[API v4.0 ガイド](/Database/RDS%20for%20MySQL/ja/api-guide-v4.0/)ドキュメントを参照してください。
* スナップショットバックアップ機能の追加
    * Cinderストレージスナップショットを利用して、DBのパフォーマンスに影響を与えずにバックアップを実行
* MySQL 8.0.45, 8.4.8バージョン追加

<a id="january-13-2026"></a>
## 2026. 01. 13. { #january-13-2026 }

<a id="january-13-2026-feature-updates"></a>
### 機能追加及び改善 { #january-13-2026-feature-updates }

* メンテナンス機能追加
    * DBインスタンスの様々な変更作業を設定したメンテナンス期間に適用
* DBスキーマ&ユーザー直接制御設定時,ROLE_ADMIN権限も付与するように修正
* MySQL 8.0.44, 8.4.7バージョン追加

<a id="january-13-2026-bug-fixes"></a>
### 不具合の修正 { #january-13-2026-bug-fixes }

* MySQL 8.4 DBインスタンスでユーザー追加時、認証プラグインがデフォルトで選択されない問題を修正

<a id="november-11-2025"></a>
## 2025. 11. 11. { #november-11-2025 }

<a id="november-11-2025-feature-updates"></a>
### 機能追加及び改善 { #november-11-2025-feature-updates }

* MySQL 8.4.6バージョン追加
* Lockの取得失敗によるバックアップ失敗時に、原因をイベントに残すよう改善
* 8.4バージョンへのアップグレード時に、パスワードプラグイン関連の警告文を表示するよう改善
* リージョンピアリングを設定していないサブネットでも、リージョン間のリードレプリカを作成できるよう修正

<a id="november-11-2025-bug-fixes"></a>
### 不具合の修正 { #november-11-2025-bug-fixes }

* フェイルオーバー失敗時に「フェイルオーバー中」の状態が続く問題を修正
* 7月のデプロイ以前に停止されたDBインスタンスを開始できない問題を修正
* `server_audit_events`に使用不可能な値を使用できる問題を修正
* リードレプリカのみ別のパラメータグループを使用する場合、複数のDBインスタンスを選択した後に最新のパラメータグループを適用できない問題を修正
* 他のリージョンのリードレプリカがあるグループでマスターの選択を解除すると、エラー通知モーダルが表示される現象を修正
* パラメータグループのリセット時に変更不可能な値が変更される現象を修正

<a id="september-09-2025"></a>
## 2025. 09. 09. { #september-09-2025 }

<a id="september-09-2025-feature-updates"></a>
### 機能追加及び改善 { #september-09-2025-feature-updates }

* MySQL 8.4 LTSバージョン追加
* MySQL 8.0.41, 8.0.42, 8.0.43バージョン追加

<a id="september-09-2025-bug-fixes"></a>
### 不具合の修正 { #september-09-2025-bug-fixes }

* 既存の高可用性インスタンスをクリックした後、新規に高可用性インスタンスを作成する際に、予備マスターの名前が入力された状態で表示される現象を修正
* 高可用性構成に追加されたリードレプリカの名前を修正できない現象を修正
* DBインスタンスにVIPを追加できない状況で、ドロップダウンメニューの[VIP追加]メニューが有効化される現象を修正
* DHCPの更新に失敗した際に、内部IPが断続的に消失する現象を修正
* 高可用性インスタンスでリードレプリカの作成中に障害が発生した場合に、高可用性構成が中断される現象を修正
* 同一組織内でサブスクライブしたイベントが複数発生した場合に、サブスクリプションの通知が動作しない現象を修正

<a id="july-15-2025"></a>
## 2025. 07. 15. { #july-15-2025 }

<a id="july-15-2025-feature-updates"></a>
### 機能追加及び改善 { #july-15-2025-feature-updates }

* DBセキュリティグループの送信(アウトバウンド)ルールで、DBポートタイプを指定できないように改善
* 高可用性DBインスタンスのスタンバイマスター名も入力するよう修正
* Resource WatcherでDBインスタンスのリソースが確認できるよう改善
* フェイルオーバーしたマスターも、削除されるまで正常に課金されるよう修正
* バイナリログがなくフェイルオーバーしたマスターを復旧できない場合に、正確なエラーメッセージが表示されるよう改善

<a id="july-15-2025-bug-fixes"></a>
### 不具合の修正 { #july-15-2025-bug-fixes }

* バックアップのエクスポート時に、パスに特殊文字が含まれているとバックアップが失敗する問題を修正
* ユーザーグループの削除時に、イベントサブスクリプションから当該ユーザーグループが削除されない問題を修正
* 重複した通知グループを削除する際に、正確なエラーメッセージが表示されるよう改善

<a id="may-13-2025"></a>
## 2025. 05. 13. { #may-13-2025 }

<a id="may-13-2025-feature-updates"></a>
### 機能追加及び改善 { #may-13-2025-feature-updates }

* VIP(Virtual IP)を使用できるように改善
    * 新規に作成するDBインスタンスからVIPを発行し、VIPは常にマスターDBインスタンスを指すように設定されます。既存のDBインスタンスには、コンソールの［VIP追加］ボタンをクリックして直接発行できます。
* 高可用性が異常な状態でも、コンソールから明示的に停止できるように改善
* 監視設定で小数値を入力できるように改善
* ユーザーグループ名にハングルを入力できるように改善
* DBインスタンスのパラメーターグループを変更する際に、変更内容モーダルウィンドウで再起動の有無を確認できるように改善

<a id="may-13-2025-bug-fixes"></a>
### 不具合の修正 { #may-13-2025-bug-fixes }

* Open APIを通じてイベント購読を作成する際に、イベントソースに異常な値を入力できる問題を修正
* 断続的にDBインスタンスの状態が更新されない問題を修正
* 断続的に原因不明のエラーモーダルウィンドウが表示される問題を修正

<a id="april-15-2025"></a>
## 2025. 04. 15. { #april-15-2025 }

<a id="april-15-2025-feature-updates"></a>
### 機能追加及び改善 { #april-15-2025-feature-updates }

* API v3.0追加及び変更
    * ログファイルリスト表示API追加
    * ログファイルエクスポートAPI追加

<a id="february-11-2025"></a>
## 2025. 02. 11. { #february-11-2025 }

<a id="february-11-2025-feature-updates"></a>
### 機能追加及び改善 { #february-11-2025-feature-updates }

* MySQL 8.0.40バージョン追加

<a id="february-11-2025-bug-fixes"></a>
### 不具合の修正 { #february-11-2025-bug-fixes }

* DBインスタンス詳細表示画面で、削除された通知グループ情報が表示される問題を修正

<a id="november-12-2024"></a>
## 2024. 11. 12. { #november-12-2024 }

<a id="november-12-2024-feature-updates"></a>
### 機能追加及び改善 { #november-12-2024-feature-updates }

* ストレージ自動拡張機能追加
* ストレージサイズ拡張時、DBインスタンスを再起動しないように改善
* DBインスタンス修正機能に含まれていたストレージサイズ拡張機能をドロップダウンメニューに分離
* 高可用性一時停止状態で予備マスターを再構築する際、一時停止状態が維持されるように変更
* 自動バックアップ設定中のバックアップ再試行有効期限設定項目を削除し、バックアップウィンドウの時間範囲内でバックアップを再試行するように改善

<a id="september-10-2024"></a>
## 2024. 09. 10. { #september-10-2024 }

<a id="september-10-2024-feature-updates"></a>
### 機能追加及び改善 { #september-10-2024-feature-updates }

* 増分バックアップ機能追加
* DBインスタンス削除時、自動バックアップ削除の有無を選択できるように改善

<a id="july-9-2024"></a>
## 2024. 07. 09. { #july-9-2024 }

<a id="july-9-2024-feature-updates"></a>
### 機能追加及び改善 { #july-9-2024-feature-updates }

* foreign_key_checks設定プロシージャ追加
* 新規パラメータの追加(MySQL 8.0.28バージョン以上)
    * `innodb_ddl_threads`
    * `innodb_parallel_read_threads`

<a id="july-9-2024-bug-fixes"></a>
### 不具合の修正 { #july-9-2024-bug-fixes }

* 削除されたDBインスタンスのバックアップでスナップショット復元ができない問題を修正

<a id="june-11-2024"></a>
## 2024. 06. 11. { #june-11-2024 }

<a id="june-11-2024-feature-updates"></a>
### 機能追加及び改善 { #june-11-2024-feature-updates }

* DBインスタンスOSアップグレード機能の追加

<a id="may-14-2024"></a>
## 2024. 05. 14. { #may-14-2024 }

<a id="may-14-2024-feature-updates"></a>
### 機能追加及び改善 { #may-14-2024-feature-updates }

* Slow Queryの分析機能を追加
    * Slow Query分析、Process List、InnoDB Statusモニタリング機能を含む分析タブを提供
    * DBインスタンスの修正画面でSlow Query分析機能を使用しないように設定できる機能を提供
* パラメータグループの変更内容を適用する際に、実際に変更されるパラメータ項目を確認できるように改善
* 高可用性状態が異常な場合、警告文を表示してイベントを発生させるように改善
* リードレプリカを作成する際にストレージの種類を選択できるように改善
* MySQL 8.0.36バージョンを追加
* API v3.0追加及び変更
    * DBインスタンスを複製するAPIリクエストに`storage.storageType`フィールドを追加
    * DBインスタンスの詳細表示APIレスポンスに`notificationGroupIds`フィールドを追加
    * API v3.0を呼び出す際にプロジェクト統合アプリケーションキーを使用できるように改善

<a id="march-12-2024"></a>
## 2024. 03. 12. { #march-12-2024 }

<a id="march-12-2024-feature-updates"></a>
### 機能追加及び改善 { #march-12-2024-feature-updates }

* 予備マスターの昇格機能を追加
* 予備マスターの強制昇格機能を追加
* フェイルオーバーを利用した再起動の際、複製ディレイを待機できるように機能を追加
* DBスキーマ&ユーザー直接制御設定解除機能を追加

<a id="february-15-2024"></a>
## 2024. 02. 15. { #february-15-2024 }

<a id="february-15-2024-feature-updates"></a>
### 機能追加及び改善 { #february-15-2024-feature-updates }

* DBスキーマ&ユーザー直接制御設定機能を追加
* 接続された通知グループの識別が容易になるように改善
    * DBインスタンスの詳細表示画面で接続された通知グループ情報を表示
* MySQL 8.0.35バージョン追加

<a id="january-9-2024"></a>
## 2024. 01. 09. { #january-9-2024 }

<a id="january-9-2024-feature-updates"></a>
### 機能追加及び改善 { #january-9-2024-feature-updates }

* 高可用性インスタンスのDBエンジンのバージョンアップグレード時にフェイルオーバー のタイミングを手動で制御できるように改善
* DBインスタンスごとにハイパーバイザーマイグレーション機能を動作できるように改善

<a id="december-19-2023"></a>
## 2023. 12. 19. { #december-19-2023 }

<a id="december-19-2023-feature-updates"></a>
### 機能追加及び改善 { #december-19-2023-feature-updates }

* 変更されたパラメータを適用するDBインスタンスを識別しやすいように改善
    * DB インスタンス一覧画面で、変更されたパラメータを適用する対象名の前に「適用」ボタンを追加
    * 変更されたパラメータを適用するDBインスタンスの詳細表示画面でパラメータグループ項目に「適用」ボタンを追加
    * 変更されたパラメータ適用必要フィルタオプション追加
* サーバーダッシュボード画面で削除されたサーバーも表示するオプションにチェックした時、削除されてから1ヶ月以内のサーバーのみ照会するように変更

<a id="november-14-2023"></a>
## 2023. 11. 14. { #november-14-2023 }

<a id="november-14-2023-feature-updates"></a>
### 機能追加及び改善 { #november-14-2023-feature-updates }

* リージョンピアリングが接続された他のリージョンのサブネットにリードレプリカを作成できるように機能追加
* DBインスタンスの強制昇格機能を追加
* イベント購読時に通知タイプを選択できるように改善
* API v3.0追加及び変更
    * DBインスタンスのバックアップ後、エクスポートAPI追加

<a id="october-17-2023"></a>
## 2023. 10. 17. { #october-17-2023 }

<a id="october-17-2023-feature-updates"></a>
### 機能追加及び改善 { #october-17-2023-feature-updates }

* 高可用性構成およびリードレプリカ追加時、リードレプリカのバックアップも使用して作成できるように改善
* 既に作成されたMySQL 5.7.33バージョン以上の高可用性インスタンスでも認証プラグインとTLSオプションを使用できるように有効化機能を追加
* MySQL 8.0.33, MySQL 8.0.34バージョン追加
* API v3.0追加及び変更
    * 復元される最後のクエリ照会APIが追加されます。
    * DBインスタンスを修正するAPIのリクエストに`dbVersion`、`useDummy`フィールドが追加されます。
    * DBインスタンスの詳細を表示APIのレスポンスに`needToApplyParameterGroup`、`needMigration`、`supportDbVersionUpgrade`フィールドが追加されます。

<a id="september-12-2023"></a>
## 2023. 09. 12. { #september-12-2023 }

<a id="september-12-2023-feature-updates"></a>
### 機能追加及び改善 { #september-12-2023-feature-updates }

* DBエンジンのバージョンアップグレード機能を追加
    * MySQL 5.7からMySQL 8.0にDBエンジンのバージョンをアップグレードした際に互換性を確認するための事前点検機能をサポート
    * ダミーDBインスタンスを使用したDBエンジンのバージョンアップグレードをサポート

<a id="august-17-2023"></a>
## 2023. 08. 17. { #august-17-2023 }

<a id="august-17-2023-feature-updates"></a>
### 機能追加及び改善 { #august-17-2023-feature-updates }

* バックアップに使用されるxtrabackupユーティリティのバージョンをアップグレード
* コンソールでバックアップに使用されたxtrabackupユーティリティのバージョンを確認できるように改善
* DBインスタンス修正時にDBエンジンバージョンをアップグレードできる機能を追加
* MySQL 5.7.33バージョン以上でユーザーを作成または修正する際、認証プラグインとTLSオプションを使用できるように機能を追加

<a id="july-11-2023"></a>
## 2023. 07. 11. { #july-11-2023 }

<a id="july-11-2023-feature-updates"></a>
### 機能追加及び改善 { #july-11-2023-feature-updates }

* DBインスタンス削除保護機能の追加

<a id="june-13-2023"></a>
## 2023. 06. 13. { #june-13-2023 }

<a id="june-13-2023-feature-updates"></a>
### 機能追加及び改善 { #june-13-2023-feature-updates }

* 予備マスターに問題が発生した場合の再構築をサポート
    * 予備マスターのDBインスタンスは変更されないため、固定IPアドレスは変更されません。
    * データベースのデータは全て削除され、マスターのデータで復旧されます。
* ユーザーグループにユーザーを追加する際、組織やプロジェクトのすべてのユーザーを追加できるように改善

<a id="may-16-2023"></a>
## 2023. 05. 16. { #may-16-2023 }

<a id="may-16-2023-feature-updates"></a>
### 機能追加及び改善 { #may-16-2023-feature-updates }

* サービスのユーザーインターフェース(UI)をNHN Cloud全体のサービスと一貫性があるように改善
* DBインスタンスが削除されても、手動バックアップは削除されないように修正。
* パラメータグループ機能を追加
    * DBインスタンスのデータベース設定を自由に変更できるようにサポート
    * 複数のDBインスタンスに適用可能
    * 既存のDBインスタンスの設定変更は、DBインスタンスと同じ名前のパラメータグループにマイグレーション
* DBセキュリティグループ機能を追加
    * DBインスタンスのアクセス制御を自由に設定できるようにサポート
    * 複数のDBインスタンスに適用可能
    * 既存のDBインスタンスに設定されたアクセス制御ルールは`{DBインスタンス名}__{DBインスタンスID}`ルールで命名されたDBセキュリティグループにマイグレーション
* 複製関係によってDBインスタンスをまとめて見ることができる画面を提供
* コンソールに予備マスターを表示
    * 予備マスターのバイナリログ(binary log)を削除して容量を確保可能
    * 予備マスターの各種ログの確認及びダウンロードをサポート
* リードレプリカの再構築をサポート
    * リードレプリカのDBインスタンスは変更されないため、固定IPアドレスは変更されません
    * データベースのデータは全て削除され、マスターのデータで復旧されます。
* フェイルオーバーが発生したマスターの復旧サポート
    * フェイルオーバーが発生したマスターと新規マスターを高可用性構成で復旧可能
    * 復旧は失敗する可能性があり、復旧できないフェイルオーバーが発生したマスターは再構築可能
* フェイルオーバーが発生したマスター再構築サポート
    * フェイルオーバーが発生したマスターのDBインスタンスは変更されないため、固定IPアドレスは変更されません
    * データベースのデータは全て削除され、マスターのデータで復旧されます。
* MySQL 8.0.32バージョン追加

<a id="may-16-2023-bug-fixes"></a>
### 不具合の修正 { #may-16-2023-bug-fixes }

* リードレプリカのバックアップで時点復元ができない問題を修正しました。

<a id="february-14-2023"></a>
## 2023. 02. 14. { #february-14-2023 }

<a id="february-14-2023-feature-updates"></a>
### 機能改善 { #february-14-2023-feature-updates }

* サーバーダッシュボードのMySQL指標のうち、ConnectionチャートにMax Connection値を追加で表記するように改善

<a id="february-14-2023-bug-fixes"></a>
### 不具合の修正 { #february-14-2023-bug-fixes }

* IAMコンソールでエラーが発生した時に適切なエラーページに移動しない問題を修正
* フェイルオーバーを利用してDBインスタンスタイプの変更またはストレージの拡張を行う場合にPing間隔がデフォルト値に設定される問題を修正

<a id="january-10-2023"></a>
## 2023. 01. 10. { #january-10-2023 }

<a id="january-10-2023-feature-updates"></a>
### 機能改善 { #january-10-2023-feature-updates }

* 通知グループ名の重複を許可しないように修正

<a id="january-10-2023-bug-fixes"></a>
### 不具合の修正 { #january-10-2023-bug-fixes }

* 監視設定をポップアップウィンドウを閉じずに続けて修正する場合に、設定が正常に適用されない問題を修正
* サーバーダッシュボードページの更新設定が動作しない問題を修正
* DDLクエリ実行によるバックアップ失敗イベントが正常に残らない問題を修正

<a id="december-13-2022"></a>
## 2022. 12. 13. { #december-13-2022 }

<a id="december-13-2022-feature-updates"></a>
### 機能改善 { #december-13-2022-feature-updates }

* DML負荷によるバックアップ失敗時、その内容をイベントメッセージに残すように改善

<a id="december-13-2022-bug-fixes"></a>
### 不具合の修正 { #december-13-2022-bug-fixes }

* DBスキーマを同期する時、断続的に削除できないスキーマが登録される現象を修正
* 削除したアカウントと同じ名前の別のホストを追加できない問題を修正
* フェイルオーバーした既存マスターを再起動するとユーザーアクセス制御を修正できない問題を修正

<a id="november-15-2022"></a>
## 2022. 11. 15. { #november-15-2022 }

<a id="november-15-2022-bug-fixes"></a>
### 不具合の修正 { #november-15-2022-bug-fixes }

* `default_authentication_plugin`パラメータを`sha256_password`に設定すると、高可用性構成が解除される問題を修正

<a id="october-11-2022"></a>
## 2022. 10. 11. { #october-11-2022 }

<a id="october-11-2022-feature-updates"></a>
### 機能改善 { #october-11-2022-feature-updates }

* DBインスタンス作成時にデフォルトで表示されるバージョンを8.0.28バージョンに変更
* インスタンス詳細画面で表示されるドメイン変更ツールチップの文言修正

<a id="october-11-2022-bug-fixes"></a>
### 不具合の修正 { #october-11-2022-bug-fixes }

* 廃止予定のイベントコードを削除
* 特定条件で断続的にリードレプリカを削除できない問題を修正

<a id="others"></a>
### その他 { #others }

* 5.6.33バージョンのインスタンスを作成できないように修正

<a id="september-14-2022"></a>
## 2022. 09. 14. { #september-14-2022 }

<a id="added-features"></a>
### 機能追加 { #added-features }

* MySQL 5.7.37, MySQL 8.0.28バージョン追加

<a id="september-14-2022-bug-fixes"></a>
### 不具合の修正 { #september-14-2022-bug-fixes }

* Webブラウザの開発者コンソールにエラーメッセージが残る現象を修正
* **テーブルロック使用しない**状態の単一インスタンスを高可用性インスタンスに変更するとバックアップが失敗する現象を修正

<a id="august-9-2022"></a>
## 2022. 08. 09. { #august-9-2022 }

<a id="august-9-2022-added-features"></a>
### 機能追加 { #august-9-2022-added-features }

* イベントリストをExcelにエクスポートする機能を追加

<a id="august-9-2022-feature-updates"></a>
### 機能改善 { #august-9-2022-feature-updates }

* 高可用性停止したインスタンスもDB Configurationを変更できるように修正
* バックアップ保管周期を最大30日から最大2年に修正
* DDL実行によるバックアップ失敗時、イベントメッセージに原因を残すように改善

<a id="august-9-2022-bug-fixes"></a>
### 不具合の修正 { #august-9-2022-bug-fixes }

* 断続的に内部エージェントとの通信問題によりバックアップに失敗する問題を修正

<a id="july-12-2022"></a>
## 2022. 07. 12. { #july-12-2022 }

<a id="july-12-2022-added-features"></a>
### 機能追加 { #july-12-2022-added-features }

* サーバーダッシュボードでチャートをサーバーごとにグループ化して見ることができる機能を追加

<a id="july-12-2022-feature-updates"></a>
### 機能改善 { #july-12-2022-feature-updates }

* **レプリケーション中断**状態のリードレプリカのDB Configuration変更ができるように修正

<a id="july-12-2022-bug-fixes"></a>
### 不具合の修正 { #july-12-2022-bug-fixes }

* 断続的に**接続失敗**状態のDBインスタンスの状態が **正常**と表示される問題を修正
* リードレプリカ作成時、バックアップを実行していなくてもイベントログにバックアップ実行が残る問題を修正
* 断続的にボリューム拡張が失敗する問題を修正

<a id="june-14-2022"></a>
## 2022. 06. 14. { #june-14-2022 }

<a id="june-14-2022-feature-updates"></a>
### 機能改善 { #june-14-2022-feature-updates }

* 複製ディレイにより再起動が失敗する場合はイベントを残すように改善
* 接続情報ドメインがcloud.toast.comからnhncloudservice.comに変更

<a id="june-14-2022-bug-fixes"></a>
### 不具合の修正 { #june-14-2022-bug-fixes }

* validate passwordプラグイン使用時、高可用性構成ができない問題を修正
* 高可用性インスタンスのタイプ変更が失敗したにもかかわらず、candidate masterのタイプが変更後のタイプに見える問題を修正

<a id="may-10-2022"></a>
## 2022. 05. 10. { #may-10-2022 }

<a id="may-10-2022-added-features"></a>
### 機能追加 { #may-10-2022-added-features }

* 自動バックアップの場合、他のリージョンにバックアップファイルを複製してリージョンの障害に備えることができる機能を提供

<a id="may-10-2022-feature-updates"></a>
### 機能改善 { #may-10-2022-feature-updates }

* エラーログの保存位置をデータボリュームに変更
* エラーログが100MBサイズで最大10個まで循環するように変更
* 強制再起動の実行時に、再び使用できるようになるまでコンソールを操作できないように修正
* フェイルオーバーの開始時点からコンソールで対象インスタンスを操作できないように修正
* processlistで、innodb statusを一緒に見られるようにユーザビリティを改善
* processlistで、数字でページを移動できるように改善
* processlistで、チャートを拡大してその区間だけを確認できるように改善
* processlistで、キーワードで検索できるように改善
* processlistで、照会した内容をCSV形式でダウンロードできるように改善

<a id="may-10-2022-bug-fixes"></a>
### 不具合の修正 { #may-10-2022-bug-fixes }

* 読み取りレプリカのバックアップで復元した時、誤った復元時間を選択できていた問題を修正
* Safariでモニタリンググラフが表示されない問題を修正
* マスターインスタンスのパラメータ変更後、読み取りレプリカのパラメータ変更に失敗する問題を修正
* 5.6.33バージョンで読み取りレプリカを繰り返し作成または削除すると、断続的に読み取りレプリカの作成に失敗する問題を修正

<a id="april-12-2022"></a>
## 2022. 04. 12. { #april-12-2022 }

<a id="april-12-2022-feature-updates"></a>
### 機能改善 { #april-12-2022-feature-updates }

* 読み取りレプリカまたは一般インスタンスを高可用性インスタンスに変更するとき、使用可能な既存のバックアップがある場合、追加のバックアップなしでレプリケーションを構成するように改善

<a id="april-12-2022-bug-fixes"></a>
### 不具合の修正 { #april-12-2022-bug-fixes }

* インスタンスの停止とインスタンスボリュームの拡張を同時に行う場合、インスタンスボリュームの拡張作業が無限に終わらない現象を修正
* 5.6.33バージョンで間欠的にリードレプリカの昇格が失敗する現象を修正
* データボリュームの残り容量が1%未満の場合、再起動する時にエラーが発生する現象を修正
* 間欠的にバックアップが成功したにもかかわらず、バックアップ失敗としてイベントが記録される現象を修正

<a id="march-15-2022"></a>
## 2022. 03. 15. { #march-15-2022 }

<a id="march-15-2022-added-features"></a>
### 機能追加 { #march-15-2022-added-features }

* **DB Configuration**に変数使用機能を導入

<a id="march-15-2022-bug-fixes"></a>
### 不具合の修正 { #march-15-2022-bug-fixes }

* 特定の条件でモニタリングデータが収集されない現象を修正
* フェイルオーバーが発生したインスタンスの自動バックアップが削除されない現象を修正
* 作成に失敗した自動バックアップが期間満了した時に削除されない現象を修正
* MySQLに登録されたユーザーが多すぎる場合、復元に失敗する現象を修正
* access ruleを修正してもバックアップ設定変更イベントが記録される現象を修正

<a id="january-11-2022"></a>
## 2022. 01. 11. { #january-11-2022 }

<a id="january-11-2022-added-features"></a>
### 機能追加 { #january-11-2022-added-features }

* MySQLで実行中のプロセスリストおよびInnoDB状態を確認することができる機能の追加

<a id="january-11-2022-feature-updates"></a>
### 機能改善 { #january-11-2022-feature-updates }

* コンソールでDBスキーマを作成する時、入力可能な名前の最小文字数をMySQLと同じに修正

<a id="december-14-2021"></a>
## 2021. 12. 14. { #december-14-2021 }

<a id="december-14-2021-feature-updates"></a>
### 機能改善 { #december-14-2021-feature-updates }

* モニタリング照会API v1の提供中断
* データ暗号化機能の提供中断

<a id="december-14-2021-bug-fixes"></a>
### 不具合の修正 { #december-14-2021-bug-fixes }

* インスタンス複製完了直後に、複製中断イベントが残る現象の修正
* 通知グループ上にマウスカーソルを合わせた時、監視設定の項目が隠れるバグを修正
* イベント購読時、イベントコードが「全て選択」の場合、購読ができない内部イベントコードの通知を受け取る問題の修正
* インスタンス作成直後に作成したインスタンスを選択すると不明なエラーが発生するバグを修正
* DBインスタンスの停止時にイベントを残すように修正

<a id="november-9-2021"></a>
## 2021. 11. 09. { #november-9-2021 }

<a id="november-9-2021-added-features"></a>
### 機能追加 { #november-9-2021-added-features }

* 自動バックアップを1日に複数回実行できるように機能追加
* 時点復元時、特定のbinlog positionに復元することができる機能の追加
* 一般インスタンスを90日間停止することができる機能の追加

<a id="november-9-2021-feature-updates"></a>
### 機能改善 { #november-9-2021-feature-updates }

* 容量不足状態でもインスタンスを修正できるように機能改善
* 強制再起動時にMySQLが正常に動かない現象を緩和
* Out Of MemoryでMySQLが終了した場合、再起動するように修正

<a id="november-9-2021-bug-fixes"></a>
### 不具合の修正 { #november-9-2021-bug-fixes }

* インスタンスの作成に必要なファイルをダウンロードできず、インスタンスの作成が失敗する問題を改善
* 長期間実行されるバックアップの場合、ユーザークエリ遅延によるバックアップ失敗であっても一般バックアップ失敗としてイベントが残るバグを修正

<a id="october-12-2021"></a>
## 2021. 10. 12. { #october-12-2021 }

<a id="october-12-2021-feature-updates"></a>
### 機能改善 { #october-12-2021-feature-updates }

* 時点復元ができない期間を表示しないように修正

<a id="october-12-2021-bug-fixes"></a>
### 不具合の修正 { #october-12-2021-bug-fixes }

* サービス有効化直後に、データ暗号化を使用する高可用性インスタンスを作る時、復元ができない問題を修正
* ストレージ拡張後、ページの更新ができない現象を修正

<a id="september-14-2021"></a>
## 2021. 09. 14. { #september-14-2021 }

<a id="september-14-2021-feature-updates"></a>
### 機能改善 { #september-14-2021-feature-updates }

* バックアップイベント開始、成功、失敗ケース改善
* MySQL 5.7.33バージョンを追加サポート
* フェイルオーバーを利用しないで高可用性インスタンスのボリュームを拡張することができる機能を追加

<a id="september-14-2021-bug-fixes"></a>
### 不具合の修正 { #september-14-2021-bug-fixes }

* オブジェクトストレージにあるバックアップを利用して復元する時、正常に復元できないバグを修正
* オブジェクトストレージにバックアップをエクスポートする時、ファイルおよびディレクトリの有無を確認していたロジックバグを修正
* インスタンスを選択した時、不明なエラーウィンドウが表示されるバグを修正

<a id="august-25-2021"></a>
## 2021. 08. 25. { #august-25-2021 }

<a id="august-25-2021-feature-updates"></a>
### 機能改善 { #august-25-2021-feature-updates }

* バックアップのためのボリュームディスク使用方法変更と性能改善
* サービスを有効にする時、リージョン別情報同期を改善

<a id="august-25-2021-bug-fixes"></a>
### 不具合の修正 { #august-25-2021-bug-fixes }

* 動作と関連がない無効なタイプのイベントを記録するバグを修正
* 高可用性インスタンスの障害措置を進行中にインスタンスの状態と一致しないイベントを記録するバグを修正
* Database Activityチャートにinsert項目がないバグを修正

<a id="july-13-2021"></a>
## 2021. 07. 13. { #july-13-2021 }

<a id="july-13-2021-feature-updates"></a>
### 機能改善 { #july-13-2021-feature-updates }

* MySQL 8.0.23バージョンを追加サポート
* イベント購読リストで有効になっているかどうかを確認できるように改善
* 作成したインスタンスがない時、ダッシュボードに作成したインスタンスがないという文言を表示するように改善

<a id="july-13-2021-bug-fixes"></a>
### 不具合の修正 { #july-13-2021-bug-fixes }

* 一部モニタリングデータの未収集バグを修正
* ユーザーグループ名が長い場合、イベント購読の登録、通知グループの追加時にUIの外にはみ出るバグを修正
* ダッシュボードドロップダウンを選択した時、メニューが消えずに残る現象を修正

<a id="june-15-2021"></a>
## 2021. 06. 15. { #june-15-2021 }

<a id="june-15-2021-feature-updates"></a>
### 機能改善 { #june-15-2021-feature-updates }

* モニタリングシステム改編

<a id="june-15-2021-bug-fixes"></a>
### 不具合の修正 { #june-15-2021-bug-fixes }

* ストレージサイズに近いサイズのバックアップで復元する時、復元できない問題を修正
* オブジェクトストレージにバックアップをエクスポートまたはインポートする時、コンテナまたはパスにハングルがある場合、正常に動作しない問題を修正

<a id="may-11-2021"></a>
## 2021. 05. 11. { #may-11-2021 }

<a id="may-11-2021-added-features"></a>
### 機能追加 { #may-11-2021-added-features }

* オブジェクトストレージを利用したバックアップのエクスポートおよびインポート機能を提供
* 強制再起動機能を提供

<a id="may-11-2021-feature-updates"></a>
### 機能改善 { #may-11-2021-feature-updates }

* xtrabackupログファイルを確認してダウンロードできるように機能改善

<a id="may-11-2021-bug-fixes"></a>
### 不具合の修正 { #may-11-2021-bug-fixes }

* サービスを有効にした直後にインスタンスを同時に作成する時、インスタンスが作成できないバグを修正
* 高可用性インスタンスのポートとインスタンスタイプを同時に変更する場合、変更が失敗する現象を修正

<a id="april-13-2021"></a>
## 2021. 04. 13. { #april-13-2021 }

<a id="april-13-2021-added-features"></a>
### 機能追加 { #april-13-2021-added-features }

* MySQLバージョン5.6.33～5.7.26の監査ログ(audit log)機能を提供

<a id="april-13-2021-feature-updates"></a>
### 機能改善 { #april-13-2021-feature-updates }

* プロジェクトメンバーの権限をRDS for MySQL ADMIN / RDS for MySQL MEMBERに細分化
* MySQLがダウンした状態で再起動ができないように修正
* 任意のアベイラビリティゾーンを選択できるように修正
* アラーム設定時に表示されるクォーター制限文言を修正
* RDSで提供するプロシージャの使用方法ガイドを追加

<a id="april-13-2021-bug-fixes"></a>
### 不具合の修正 { #april-13-2021-bug-fixes }

* フェイルオーバーが完了したインスタンスの状態が正常化しない問題を修正
* 作成に失敗したRead Only Slaveが原因で、マスターインスタンスの一部機能が動作しない問題を修正
* データ暗号化インスタンスが強制再起動する時、MySQLが正常に実行できない問題を修正

<a id="march-9-2021"></a>
## 2021. 03. 09. { #march-9-2021 }

<a id="march-9-2021-feature-updates"></a>
### 機能改善 { #march-9-2021-feature-updates }

* プロジェクト別リソースクォーター制限機能を改善

<a id="march-9-2021-bug-fixes"></a>
### 不具合の修正 { #march-9-2021-bug-fixes }

* 特定の状況でインスタンスの再起動が正常に行われないバグを修正

<a id="february-16-2021"></a>
## 2021. 02. 16. { #february-16-2021 }

<a id="february-16-2021-added-features"></a>
### 機能追加 { #february-16-2021-added-features }

* DB UserとDBスキーマをコンソールから制御できる機能を追加

<a id="february-16-2021-feature-updates"></a>
### 機能改善 { #february-16-2021-feature-updates }

* DBファイル暗号化機能を選択した時、ツールチップを提供
* クエリー遅延待機時間の値が異常な場合、検証メッセージを表示

<a id="february-16-2021-bug-fixes"></a>
### 不具合の修正 { #february-16-2021-bug-fixes }

* プロジェクトメンバーが20人以上の場合、Notificationメンバーに登録できないバグを修正

<a id="january-19-2021"></a>
## 2021. 01. 19. { #january-19-2021 }

<a id="january-19-2021-added-features"></a>
### 機能追加 { #january-19-2021-added-features }

* 高可用性(HA)機能使用時、 Ping Interval(Masterインスタンス状態を確認する時間間隔)を設定できるように機能追加
* 高可用性(HA)一時中止/再開機能を追加
* **Access制御設定** ダイアログボックスで、アクセス制御方向(受信/送信)を設定できるように機能追加
* t2.c1m1 Flavorインスタンス生成ができないように変更
* t2.c1m1 Flavorで既に生成してある一般インスタンスの場合、高可用性に変更できないように変更

<a id="december-15-2020"></a>
## 2020. 12. 15. { #december-15-2020 }

<a id="december-15-2020-added-features"></a>
### 機能追加 { #december-15-2020-added-features }

* --ftwrl-wait-timeoutオプション値をユーザーが設定できるように機能追加

<a id="november-10-2020"></a>
## 2020. 11. 10. { #november-10-2020 }

<a id="november-10-2020-bug-fixes"></a>
### 不具合の修正 { #november-10-2020-bug-fixes }

* 自動バックアップ作成に失敗する現象を修正
* 期間が満了した自動バックアップの削除に失敗する現象を修正

<a id="october-13-2020"></a>
## 2020. 10. 13. { #october-13-2020 }

<a id="october-13-2020-bug-fixes"></a>
### 不具合の修正 { #october-13-2020-bug-fixes }

* innodb_buffer_pool_sizeの値が意図した値に修正されない現象を修正
* require_secure_transportの値がonの場合、ha candidate masterインスタンスの複製が失敗する現象を修正
* 大容量インスタンスをバックアップする時、過度な時間遅延が発生する現象を修正

<a id="september-22-2020"></a>
## 2020. 09. 22. { #september-22-2020 }

<a id="september-22-2020-added-features"></a>
### 機能追加 { #september-22-2020-added-features }

* 韓国(坪村)リージョンオープン

<a id="september-15-2020"></a>
## 2020. 09. 15. { #september-15-2020 }

<a id="september-15-2020-added-features"></a>
### 機能追加 { #september-15-2020-added-features }

* モニタリングAPIをサポート

<a id="august-11-2020"></a>
## 2020. 08. 11. { #august-11-2020 }

<a id="august-11-2020-bug-fixes"></a>
### 不具合の修正 { #august-11-2020-bug-fixes }

* ユーザーVPCサブネットがない場合、異常なサブネットがリストに表示される現象を修正

<a id="july-14-2020"></a>
## 2020. 07. 14. { #july-14-2020 }

<a id="july-14-2020-added-features"></a>
### 機能追加 { #july-14-2020-added-features }

* MySQL 8.0.18バージョンをサポート

<a id="december-10-2019"></a>
## 2019. 12. 10. { #december-10-2019 }

<a id="december-10-2019-added-features"></a>
### 機能追加 { #december-10-2019-added-features }

* DBファイルの暗号化機能を追加 (韓国リージョン)

<a id="november-12-2019"></a>
## 2019. 11. 12. { #november-12-2019 }

<a id="november-12-2019-feature-updates"></a>
### 機能改善 { #november-12-2019-feature-updates }

* Candidate Masterの障害検知および復旧機能を高度化

<a id="november-12-2019-bug-fixes"></a>
### 不具合の修正 { #november-12-2019-bug-fixes }

* 断続的にバックアップができなかった問題を修正

<a id="september-24-2019"></a>
## 2019. 09. 24. { #september-24-2019 }

<a id="september-24-2019-feature-updates"></a>
### 機能改善 { #september-24-2019-feature-updates }

* インスタンス作成速度を改善(HAインスタンス基準約28分→約13分)
* フェイルオーバーを利用して再起動した時、時点復元のための新規バックアップを進行できるようにUXを改善
* 基本アラームを使用するかどうかのUIを変更

<a id="august-13-2019"></a>
## 2019. 08. 13. { #august-13-2019 }

<a id="august-13-2019-feature-updates"></a>
### 機能改善 { #august-13-2019-feature-updates }

* 高可用性(HA)に関連するイベントログを、より直感的に確認できるように修正

<a id="august-13-2019-bug-fixes"></a>
### 不具合の修正 { #august-13-2019-bug-fixes }

* 断続的にDBインスタンスの作成、復元ができない問題を修正
* DBインスタンスの削除アラームメールが送信されない問題を修正

<a id="july-23-2019"></a>
## 2019. 07. 23. { #july-23-2019 }

<a id="july-23-2019-added-features"></a>
### 機能追加 { #july-23-2019-added-features }

* 基本アラーム機能を追加
* モニタリング項目を追加

<a id="july-23-2019-feature-updates"></a>
### 機能改善 { #july-23-2019-feature-updates }

* バックアップ関連イベントはもはやアラムをサポートしません。

<a id="june-27-2019"></a>
## 2019. 06. 27. { #june-27-2019 }

<a id="june-27-2019-added-features"></a>
### 機能追加 { #june-27-2019-added-features }

* 日本リージョンを追加

<a id="june-25-2019"></a>
## 2019. 06. 25. { #june-25-2019 }

<a id="june-25-2019-added-features"></a>
### 機能追加 { #june-25-2019-added-features }

* 高可用性(HA)機能を追加

<a id="june-25-2019-feature-updates"></a>
### 機能改善 { #june-25-2019-feature-updates }

* インスタンス詳細表示画面に表示されるイベント期間を 1 日から 7 日に変更

<a id="june-25-2019-bug-fixes"></a>
### 不具合の修正 { #june-25-2019-bug-fixes }

* 時点復元時、復旧可能な時間から復元できるように修正

<a id="may-14-2019"></a>
## 2019. 05. 14. { #may-14-2019 }

<a id="may-14-2019-feature-updates"></a>
### 機能改善 { #may-14-2019-feature-updates }

* インスタンス作成および修正時の検証機能を強化
* Notification 通知イベントの全体選択/解除ができる UX を追加

<a id="may-14-2019-bug-fixes"></a>
### 不具合の修正 { #may-14-2019-bug-fixes }

* 作成中のインスタンスを削除する際、削除できない問題を修正
* データ保存場所の空き容量が不足している時、データボリュームが変更されない問題を修正

<a id="march-12-2019"></a>
## 2019. 03. 12. { #march-12-2019 }

<a id="march-12-2019-feature-updates"></a>
### 機能改善 { #march-12-2019-feature-updates }

* 意味が曖昧、あるいは、見づらいエラーメッセージの改善
* コンソールでtransaction-isolation値を修正できるよう改善

<a id="march-12-2019-bug-fixes"></a>
### 不具合の修正 { #march-12-2019-bug-fixes }

* 1TBのDBのバックアップ時間が1日以上かかる可能性を除去

<a id="february-26-2019"></a>
## 2019. 02. 26. { #february-26-2019 }

<a id="february-26-2019-added-features"></a>
### 機能追加 { #february-26-2019-added-features }

* インスタンスデータレポジトリーにSSDボリュームの機能を追加

<a id="february-26-2019-feature-updates"></a>
### 機能改善 { #february-26-2019-feature-updates }

* Notification受信対象をプロジェクトメンバーに設定するように機能を改善。
* x1、u2 flavorの使用が可能になるよう機能改善。

<a id="january-29-2019"></a>
## 2019. 01. 29. { #january-29-2019 }

<a id="january-29-2019-feature-updates"></a>
### 機能改善 { #january-29-2019-feature-updates }

* インスタンスボリュームサイズの最大値を1000Gに変更

<a id="december-14-2018"></a>
## 2018. 12. 14. { #december-14-2018 }

<a id="december-14-2018-bug-fixes"></a>
### 不具合の修正 { #december-14-2018-bug-fixes }

* r2.c8m64 flavor 非表示を修正
* general logが見えない問題を修正
* VPC Subnet選択時のバグ修正

<a id="december-11-2018"></a>
## 2018. 12. 11. { #december-11-2018 }

<a id="december-11-2018-feature-updates"></a>
### 機能改善 { #december-11-2018-feature-updates }

* Peering機能の削除
* ユーザーVPC Subnetを利用したネットワーク通信方式え機能を改善

<a id="october-23-2018"></a>
## 2018. 10. 23. { #october-23-2018 }

<a id="october-23-2018-feature-updates"></a>
### 機能改善 { #october-23-2018-feature-updates }

* インスタンス作成/復元/コピー時に入力項目の説明文を表示
* mysql transaction_isolationオプションの表示

<a id="october-16-2018"></a>
## 2018. 10. 16. { #october-16-2018 }

<a id="october-16-2018-added-features"></a>
### 機能追加 { #october-16-2018-added-features }

* インスタンスFlavorの変更機能を追加
* インスタンスStorageの拡張機能を追加

<a id="august-28-2018"></a>
## 2018. 08. 28. { #august-28-2018 }

<a id="august-28-2018-added-features"></a>
### 機能追加 { #august-28-2018-added-features }

* Binary Logファイルの削除によるインスタンス容量確保機能を追加

<a id="july-24-2018"></a>
## 2018. 07. 24. { #july-24-2018 }

<a id="july-24-2018-added-features"></a>
### 機能追加 { #july-24-2018-added-features }

* MySQL 5.7.15バージョンを追加サポート

<a id="july-24-2018-bug-fixes"></a>
### 不具合の修正 { #july-24-2018-bug-fixes }

* MySQL 5.7.19バーじょインスタンスを作成時、floating ipをつけないと作成できない問題を修正
* 特定の状況における自動バックアップの時間が通常の2倍になる問題を修正

<a id="may-29-2018"></a>
## 2018. 05. 29. { #may-29-2018 }

<a id="may-29-2018-added-features"></a>
### 機能追加 { #may-29-2018-added-features }

* MySQL 5.7バージョンを新規サポート

<a id="april-24-2018"></a>
## 2018. 04. 24. { #april-24-2018 }

<a id="april-24-2018-feature-updates"></a>
### 機能改善 { #april-24-2018-feature-updates }

* masterのport変更時、read only slaveのmaster接続情報を自動変更
* バックアップ後、残賊する不要なログを削除

<a id="april-24-2018-bug-fixes"></a>
### 不具合の修正 { #april-24-2018-bug-fixes }

* 検索結果ページ > インスタンス作成後、ページ移動を試みた際、検索結果ページに移動する問題を修正
* パスワード確認欄を空白でインスタンス作成を試みた場合、警告メッセージが表示されない不具合を修正

<a id="march-22-2018"></a>
## 2018. 03. 22. { #march-22-2018 }

<a id="march-22-2018-bug-fixes"></a>
### 不具合の修正 { #march-22-2018-bug-fixes }

* バックアップ保管期間 ‘なし’に変更した場合、一定時間リストに表示される事象を修正
* インスタンス設定を修正していないのに、インスタンス状態が変更中として表示される問題を修正
* インスタンス再起動時、QPSが負の数で表示される不具合を修正
* Monitoring画面で期間設定のボタンをクリックすると、画面の日付と時刻の更新なしにデータだけが更新されるバグを修正

<a id="february-22-2018"></a>
## 2018. 02. 22. { #february-22-2018 }

<a id="new-releases"></a>
### 新商品発売 { #new-releases }

* Relational Database Service (RDS)は、Relational Databaseをクラウド環境で提供する商品です。
* 複雑な設定をしなくても、Relational Databaseを使うことができます。
* MySQL 5.6.33バージョンを提供します。
