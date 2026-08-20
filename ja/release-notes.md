<!-- machine_translated: true -->

<!-- pre-align:aligned sig=a64bf08e342e -->

<a id="container-nhn-container-servicencs-release-notes"></a>
## Container > NHN Container Service(NCS)  > リリースノート { #container-nhn-container-servicencs-release-notes }

<a id="august-25-2026"></a>
### 2026. 08. 25. { #august-25-2026 }

<a id="august-25-2026-added-features"></a>
#### 機能追加

* コンテナ共有メモリサイズの設定機能が追加されました。

<a id="october-28-2025"></a>
### 2025. 10. 28. { #october-28-2025 }

<a id="october-28-2025-added-features"></a>
#### 機能追加

* ワークロードで使用するコンテナイメージに対してマルウェア検査を実行する機能が追加されました。

<a id="march-4-2025"></a>
### 2025. 03. 04. { #march-4-2025 }

<a id="march-4-2025-added-features"></a>
#### 機能追加

* ワークロード作成時に内部リクエストレスポンス待機時間項目が追加されました。内部リクエストレスポンス待機時間設定により、他のワークロードの内部ロードバランサーVIPへの通信リクエスト時にタイムアウトを適用できます。

<a id="november-26-2024"></a>
### 2024. 11. 26. { #november-26-2024 }

<a id="november-26-2024-added-features"></a>
#### 機能追加

* コンテナにアクセス可能なWebターミナル機能が追加されました。
* ワークロードのオートスケーリング機能が追加されました。
* ワークロードの作業別再起動機能が追加されました。
* NCS用のPublic APIが公開されました。
    * Public APIについては、[APIガイド](/Container/NCS/ja/public-api/)を参照してください。

<a id="august-27-2024"></a>
### 2024. 08. 27. { #august-27-2024 }

<a id="august-27-2024-added-features"></a>
#### 機能追加

* NCSで発生したイベントをResource Watcherで確認できます。

<a id="may-28-2024"></a>
### 2024. 05. 28. { #may-28-2024 }

<a id="may-28-2024-added-features"></a>
#### 機能追加

* ワークロード作業終了時間を予約設定できます。
* テンプレートバージョン管理機能が追加されました。
* 初期化コンテナ機能が追加されました。
* イベント照会期間が30日に変更されました。
* HostAliasesを設定できるようになりました。

<a id="february-27-2024"></a>
### 2024. 02. 27. { #february-27-2024 }

<a id="february-27-2024-added-features"></a>
#### 機能追加

* コンテナ引数(Args)設定機能が追加されました。
* ワークロード配布コントローラーの選択機能が追加されました。
* 内部ロードバランサー機能が追加されました。
* ワークロードのPrivate DNS連動機能が追加されました。

<a id="february-27-2024-feature-updates"></a>
#### 機能改善

* コンテナ間の一時的な共有ストレージが提供されます。

<a id="november-28-2023"></a>
### 2023. 11. 28. { #november-28-2023 }

<a id="november-28-2023-added-features"></a>
#### 機能追加

* コンテナ設定機能が追加されました。
    * DNSサーバーアドレス設定
    * 状態点検(LivenessProbe, StartupProbe)設定
    * ライフサイクルフック(Lifecycle Hook)設定
    * コンフィグマップ設定
    * シークレット設定
    * NASコンテナ接続パス設定
* GPUと臨時ストレージモニタリング機能が追加されました。
* ワークロード作成時にセキュリティグループを選択できます。
* NCS で発生したイベントを NHN CloudTrail で確認できます。

<a id="november-28-2023-feature-updates"></a>
#### 機能改善

* Load Balancerが提供されます。
    * Load Balancer Instanceはサポートされなくなりました。
* コンテナポートにHTTPS, TERMINATED_HTTPSプロトコルが追加されました。
* ログタブが改善されました。
* コンテナの現在と最後の状態についての詳細な理由をイベントタブで確認できるように改善されました。

<a id="august-29-2023"></a>
### 2023. 08. 29. { #august-29-2023 }

<a id="august-29-2023-added-features"></a>
#### 機能追加

* ワークロード予約機能を追加しました。
* ワークロード停止/再起動機能を追加しました。

<a id="august-29-2023-feature-updates"></a>
#### 機能改善

* NASストレージ接続失敗原因をイベントタブで確認できるように改善しました。

<a id="july-25-2023"></a>
### 2023. 07. 25. { #july-25-2023 }

<a id="july-25-2023-feature-updates"></a>
#### 機能改善

* コンテナの最大リソースサイズが増加しました。

<a id="may-30-2023"></a>
### 2023. 05. 30. { #may-30-2023 }

<a id="may-30-2023-feature-updates"></a>
#### 機能改善

* GPUタイプを選択できる機能が追加されました。
* コンテナポートにHTTPプロトコルが追加されました。
* Quota機能が追加されました。

<a id="march-28-2023"></a>
### 2023. 03. 28. { #march-28-2023 }

<a id="march-28-2023-feature-updates"></a>
#### 機能改善

* 内部構造を改善してサービスの安定性が向上しました。

<a id="added-features"></a>
### 2023. 02. 28. { #added-features }

<a id="added-features-2"></a>
#### 機能追加

* 権限細分化機能を追加しました。
* ワークロード変更機能を追加しました。

<a id="january-31-2023"></a>
### 2023. 01. 31. { #january-31-2023 }

<a id="january-31-2023-added-features"></a>
#### 機能追加

* モニタリング機能を追加しました。

<a id="december-27-2022"></a>
### 2022. 12. 27. { #december-27-2022 }

<a id="december-27-2022-release-of-a-new-service"></a>
#### 新規サービスリリース

* コンソールからコンテナを作成し、管理できます。