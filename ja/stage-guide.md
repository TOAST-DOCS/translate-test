## Dev Tools > Pipeline > ステージガイド

ステージガイドでは、Pipeline のステージについて基本的な内容を説明します。

ステージは、パイプラインスタジオ画面で右上の **[編集モード]** トグルをクリックして編集モードを有効にした後、
左の **[ステージ追加]** パネルでツリーメニューをクリックして表示されたステージをドラッグアンドドロップで追加できます。

右の **[ステージ設定]** パネルでステージの詳細情報を参照または編集できます。

![stage-guide-01](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-01_new.png)

ステージは下記のグループに区分されます。

- **ソース**
- **ビルド**
- **デプロイ**
- **機能**

## ソース
ビルドするソースコードを取得するステージです。

### ソース - GitHub
**[ソースリポジトリ]** は **[環境設定]** の **[ソースリポジトリ設定]** で追加した [ソースリポジトリ](/Dev%20Tools/Pipeline/ja/environment-config/#_2) を選択できます。**[ブランチ]** には、ビルド対象のソースブランチを入力します。

![stage-guide-02](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-02_new.png)

### ソース - GitLab
**[ソースリポジトリ]** は **[環境設定]** の **[ソースリポジトリ設定]** で追加した [ソースリポジトリ](/Dev%20Tools/Pipeline/ja/environment-config/#_2) を選択できます。**[ブランチ]** には、ビルド対象のソースブランチを入力します。

![stage-guide-03](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-03_new.png)

## ビルド
ビルドを行うステージです。

### ビルド - Jenkins
ユーザーが直接構成したJenkinsを使用してビルドできます。**[ビルドツール]** は **[環境設定]** の **[ビルドツール設定]** で追加した[ビルドツール](/Dev%20Tools/Pipeline/ja/environment-config/#_4)を選択できます。**[ビルドジョブ]** を選択できます。
**[アーティファクト]** の **[開始条件]** と **[終了条件]** を設定できます。**[開始条件]** を設定してステージ開始の可否を決定できます。**[終了条件]** を設定してステージの生成物をアーティファクトとして設定できます。

![stage-guide-04](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-04_new.png)

### ビルド - Bake(Manifest)
ユーザーが直接構成したHelm package fileまたは[チャートリポジトリ](/Dev%20Tools/Pipeline/ja/environment-config/#_6)を使用してビルドできます。

- チャート名はHelmエンジンで構成した成果物の名前を設定します。
- NamespaceはHelmエンジンで構成した成果物のNamespaceを設定します。
- テンプレート
    - リポジトリタイプは **[環境設定]** の[ソースリポジトリ設定](/Dev%20Tools/Pipeline/ja/environment-config/#_2)または[チャートリポジトリ設定](/Dev%20Tools/Pipeline/ja/environment-config/#_6)で追加したリポジトリを選択できます。
    - リポジトリタイプを **GitHub ファイル** または **GitLab ファイル** として指定した場合
        - パスはHelm package fileのパスを入力する必要があります。
        - ブランチ名はGitHubまたはGitLabのブランチを入力します。
    - リポジトリタイプを **Helm チャート** として指定した場合
        - チャートリポジトリ名は[チャートリポジトリ設定](/Dev%20Tools/Pipeline/ja/environment-config/#_6)で設定したリポジトリから1つを選択できます。
        - チャート名はチャートリポジトリの構成で使用可能なチャート名を選択できます。
        - チャートバージョンはチャートリポジトリの構成で使用可能なチャートバージョンを選択できます。
- オーバーライド
    - リポジトリ情報
        - テンプレートと同様の方式で選択できます。
        - テンプレートを基本としてオーバーライドで指定した内容に置き換えてビルド成果物を生成します。
    - キー（Key）/ 値（Value）
        - key、valueからなる値を入力し、特定の値を置き換えてビルド成果物を生成します。
    - 基本タイプ置換
        - このオプションをチェックするとオーバーライド値を注入する際に、--set-stringの代わりに--setを使用します。--setを使用して注入された値はHelmによって基本データ型に変換されます。
- アーティファクト
    - **[アーティファクト]** の **[開始条件]** と **[終了条件]** を設定できます。**[開始条件]** を設定してステージ開始の可否を決定できます。**[終了条件]** を設定してステージの生成物をアーティファクトとして設定できます。

![stage-guide-05](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-10-29/stage-guide-05-1.png)

### ビルド - NHN Cloud ビルドツール v2
NHN Cloudが提供するビルドツールを使用できます。

- ビルド環境設定
    - ビルドツールのパフォーマンスと制限時間を設定できます。
- ソースビルド設定
    - **[環境設定]** の **[イメージリポジトリ設定]** で追加した[イメージリポジトリ](/Dev%20Tools/Pipeline/ja/environment-config/#_3)を選択できます。
      - ビルドする環境の **[イメージ名]** および **[タグ]** を入力し、**[ビルドコマンド]** を設定します。

- Dockerイメージビルド設定
    - **[Dockerfileパス]** はDockefileが存在するパスを入力します。
    - **[Dockerfile実行パス]** はDockerfileをビルドするパスを入力します。
    - **[イメージリポジトリ]** を選択し、**[イメージ名]** を決定すると該当リポジトリに成果物をpushします。
    - **[タグ]** にはイメージのタグを入力します。タグフォーマットを含めて入力すると入力したタグフォーマット部分が動的に置換されます。

- アーティファクト設定
    - **[開始条件]** を設定してステージ開始の可否を決定できます。
    - **[終了条件]** を設定してステージの生成物をアーティファクトとして設定できます。


|イメージタグフォーマット | 置換される形態 | 説明                                 |
| ----------- | ---------- |------------------------------------|
|{BUILD_DATE_TIME}| yyyy-MM-dd_HH_mm_ss| 年-月-日_時_分_秒の形態でビルド実行時刻に置換されます。 |

![stage-guide-06](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-06_new.png)

## デプロイ
Kubernetes 環境にデプロイを行うステージです。

### デプロイ - Deploy
- **環境設定**の **[デプロイ対象設定]** で追加した[デプロイ対象](/Dev%20Tools/Pipeline/ja/environment-config/#_5)を選択できます。
**[ステージ名]**、**[デプロイ対象]**、デプロイに使用する **Manifest** を入力します。
ビルドステージでタグフォーマットを使用した場合、**Manifest** の Docker イメージタグ部分を `_{BUILD_NUMBER}` で入力すると、タグフォーマットでビルドされたイメージの中で最新番号のイメージでデプロイできます。
**Manifest** を作成する方法は [Kubernetes ドキュメント](https://kubernetes.io/docs/concepts/workloads/controllers/deployment )を参照してください。
- **[Manifest ソース]** をアーティファクトとして選択できます。選択したアーティファクトは Manifest 形式で生成される必要があります。
    - パイプラインで生成したアーティファクトを選択できます。
    - リポジトリで特定のファイルをアーティファクトとして選択できます。
- **アーティファクト**の **[開始条件]** および **[終了条件]** を設定できます。**[開始条件]** を設定してステージ開始の可否を決定できます。**[終了条件]** を設定してステージの生成物をアーティファクトとして設定できます。

![stage-guide-07](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-07_new.png)

### デプロイ - Patch
- **環境設定**の **[デプロイ対象設定]** で追加した[デプロイ対象](/Dev%20Tools/Pipeline/ja/environment-config/#_5)を選択できます。
- **[Namespace]**、**[リソースタイプ]**、**[選択方法]**、**[リソース名]**、デプロイに使用する **Manifest** を入力します。Patch で既存リソースの情報を修正できます。
- **Manifest** を作成する方法は [Kubernetes ドキュメント](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#patching-resources)を参照してください。
- **[選択方法]** を **[動的な方法で選択]** に設定した場合、**[クラスター]** と **[選択戦略]** を入力します。
- クラスター
    - replicaSet の場合、Pipeline 内部的にバージョンを指定してデプロイします。**[動的な方法で選択]** を選択すると、特定バージョンを選択するのではなく選択戦略に従って対象を選択します。
- 選択戦略
    - Newest: 該当ステージが開始されたときに最も最近にデプロイされたリソースを選択します。
    - Second Newest: 該当ステージが開始されたときに 2 番目に最近にデプロイされたリソースを選択します。
    - Oldest: 該当ステージが開始されたときに最も古いリソースを選択します。
    - Largest: 該当ステージが開始されたときにクラスターで Pod 数が最も多いリソースを選択します。
    - Smallest: 該当ステージが開始されたときにクラスターで Pod 数が最も少ないリソースを選択します。

![stage-guide-08](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-08_new.png)

### デプロイ - Scale
- **環境設定**の **[デプロイ対象設定]** で追加した[デプロイ対象](/Dev%20Tools/Pipeline/ja/environment-config/#_5)を選択できます。
- **[Namespace]**、**[リソースタイプ]**、**[選択方法]**、**[リソース名]**、**[Replicas]** を入力します。Scale で Replicas を修正できます。
- **[選択方法]** を **[動的な方法で選択]** に設定した場合、**[クラスター]** と **[選択戦略]** を入力します。
- クラスター
    - replicaSet の場合、Pipeline 内部的にバージョンを指定してデプロイします。**[動的な方法で選択]** を選択すると、特定バージョンを選択するのではなく選択戦略に従って対象を選択します。
- 選択戦略
    - Newest: 該当ステージが開始されたときに最も最近にデプロイされたリソースを選択します。
    - Second Newest: 該当ステージが開始されたときに 2 番目に最近にデプロイされたリソースを選択します。
    - Oldest: 該当ステージが開始されたときに最も古いリソースを選択します。
    - Largest: 該当ステージが開始されたときにクラスターで Pod 数が最も多いリソースを選択します。
    - Smallest: 該当ステージが開始されたときにクラスターで Pod 数が最も少ないリソースを選択します。

![stage-guide-09](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-09_new.png)

### デプロイ - Rollout undo
**環境設定**の **[デプロイ対象設定]** で追加した[デプロイ対象](/Dev%20Tools/Pipeline/ja/environment-config/#_5)を選択できます。
**[Namespace]**、**[リソースタイプ]**、**[リソース名]**、**[Revision Back]** を入力します。指定した Revision にロールバックできます。

![stage-guide-10](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-10_new.png)

### デプロイ - Delete
- **環境設定**の **[デプロイ対象設定]** で追加した[デプロイ対象](/Dev%20Tools/Pipeline/ja/environment-config/#_5)を選択できます。
- **[Namespace]**、**[リソースタイプ]**、**[選択方法]**、**[リソース名]** を入力します。該当リソースを削除できます。
- **[選択方法]** を **[動的な方法で選択]** に設定した場合、**[クラスター]** と **[選択戦略]** を入力します。
- クラスター
    - replicaSet の場合、Pipeline 内部的にバージョンを指定してデプロイします。**[動的な方法で選択]** を選択すると、特定バージョンを選択するのではなく選択戦略に従って対象を選択します。
- 選択戦略
    - Newest: 該当ステージが開始されたときに最も最近にデプロイされたリソースを選択します。
    - Second Newest: 該当ステージが開始されたときに 2 番目に最近にデプロイされたリソースを選択します。
    - Oldest: 該当ステージが開始されたときに最も古いリソースを選択します。
    - Largest: 該当ステージが開始されたときにクラスターで Pod 数が最も多いリソースを選択します。
    - Smallest: 該当ステージが開始されたときにクラスターで Pod 数が最も少ないリソースを選択します。

![stage-guide-11](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-11_new.png)

### デプロイ - NHN Container Service (NCS)
NCS ワークロードのテンプレートを置換できるステージです。  
**[NCS アプリキー]** を入力すると **[NCS ロール]**、テンプレートリスト、ワークロードリストが照会されます。  
変更するテンプレートをリストから選択できます。  
テンプレートを変更するワークロードをリストから選択できます。

![stage-guide-12](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-12_new.png)


### デプロイ - Enable
- **環境設定**の **[デプロイ対象設定]** で追加した[デプロイ対象](/Dev%20Tools/Pipeline/ja/environment-config/#_5)を選択できます。
- **[Namespace]**、**[リソースタイプ]**、**[選択方法]**、**[リソース名]** を入力します。該当リソースを有効化できます。
    - 有効化: 該当リソースを Pipeline で管理し、リソースにトラフィックを送信するように設定します。
- **[選択方法]** を **[動的な方法で選択]** に設定した場合、**[クラスター]** と **[選択戦略]** を入力します。
    - クラスター
        - replicaSet の場合、Pipeline 内部的にバージョンを指定してデプロイします。**[動的な方法で選択]** を選択すると、特定バージョンを選択するのではなく選択戦略に従って対象を選択します。
    - 選択戦略
        - Newest: 該当ステージが開始されたときに最も最近にデプロイされたリソースを選択します。
        - Second Newest: 該当ステージが開始されたときに 2 番目に最近にデプロイされたリソースを選択します。
        - Oldest: 該当ステージが開始されたときに最も古いリソースを選択します。
        - Largest: 該当ステージが開始されたときにクラスターで Pod 数が最も多いリソースを選択します。
        - Smallest: 該当ステージが開始されたときにクラスターで Pod 数が最も少ないリソースを選択します。

![stage-guide-13](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-13_new.png)

### デプロイ - Disable
- **環境設定**の **[デプロイ対象設定]** で追加した[デプロイ対象](/Dev%20Tools/Pipeline/ja/environment-config/#_5)を選択できます。
- **[Namespace]**、**[リソースタイプ]**、**[選択方法]**、**[リソース名]** を入力します。該当リソースを無効化できます。
    - 無効化: リソースを削除しませんが、今後該当リソースにトラフィックを送信しないように設定します。
- **[選択方法]** を **[動的な方法で選択]** に設定した場合、**[クラスター]** と **[選択戦略]** を入力します。
    - クラスター
        - replicaSet の場合、Pipeline 内部的にバージョンを指定してデプロイします。**[動的な方法で選択]** を選択すると、特定バージョンを選択するのではなく選択戦略に従って対象を選択します。
    - 選択戦略
        - Newest: 該当ステージが開始されたときに最も最近にデプロイされたリソースを選択します。
        - Second Newest: 該当ステージが開始されたときに 2 番目に最近にデプロイされたリソースを選択します。
        - Oldest: 該当ステージが開始されたときに最も古いリソースを選択します。
        - Largest: 該当ステージが開始されたときにクラスターで Pod 数が最も多いリソースを選択します。
        - Smallest: 該当ステージが開始されたときにクラスターで Pod 数が最も少ないリソースを選択します。

![stage-guide-14](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-14_new.png)

## 機能
追加機能を提供するステージです。

### 機能 - 承認管理
**機能 - 承認管理** ステージ以降のステージに対する **実行管理（実行、実行停止）** を承認権者が管理できます。

ステージにリクエスト内容について記述できます。承認管理ステージの **実行管理（実行、実行停止）** 機能は、該当プロジェクトの **Pipeline APPROVAL ADMIN** 役割を持つユーザーのみ実行できます。

![stage-guide-15](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-15_new.png)

**Pipeline APPROVAL ADMIN** 役割は、プロジェクトのメンバー管理、役割グループ管理で付与できます。

![stage-guide-18](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2023-10-31/stage-guide-18.png)

### 機能 - Judgement（実行管理）
必要に応じて実行管理ステージに対する **説明** 、**実行設定** 値を入力できます。

**実行設定** の有無にかかわらず、次のステージに対する **実行管理（実行、実行停止）** を実行できます。
**実行設定** を追加して次のステージの実行を選択する場合、次に説明するステージである Precondition（実行条件）に設定値を渡して分岐処理できます。

![stage-guide-16](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-16_new.png)

### 機能 - Precondition（ステージ状態条件）
前のステップのステージ名と実行結果を選択して条件を設定できます。
指定したすべての条件が満たされた場合にのみ、次のステージが実行されます。

![stage-guide-17](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-17_new.png)

### 機能 - Precondition（実行条件）
前のステップとして設定された Judgement（実行管理）ステージから受け取った値の **実行条件** に応じて、後のステージの実行を決定します。
Judgement（実行管理）ステージから受け取った設定値と **実行条件** の条件値について **実行条件一致/実行条件不一致** の中から選択して、以後のステージの実行を決定します。

![stage-guide-18](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-18_new.png)

### 機能 - Webhook
**URL** に HTTP メソッドと URL を入力します。必要に応じて **リクエストヘッダー** と **リクエストデータ** を追加できます。
Webhook の応答値が **Fail Fast HTTP ステータスコード** に入力した値のいずれかの場合、直ちに該当ステージを終了します。

![stage-guide-19](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-19_new.png)

### 機能 - 他パイプライン実行
ステージで他のパイプライン全体を実行できます。
実行したい **パイプライン名** を選択します。

**実行条件** を選択解除した場合、選択したパイプラインの実行状態を待たずに、次のステージが実行されます。

![stage-guide-20](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-20_new.png)

### 機能 - NHN Cloud Deploy サービスデプロイ実行
ステージで NHN Cloud Deploy サービスを使用してデプロイを実行できます。
- デプロイを実行するアーティファクトの **Command Type** が **SSH** の場合、該当 **NHN Cloud Deploy サービスデプロイ実行** 機能はサポートされません。**Cloud Agent** の場合のみサポートされます。関連内容は [Deploy 使用ガイド](/Dev%20Tools/Deploy/ja/console-guide/#_8) を参照してください。

**環境設定** > **NHN Cloud セキュリティ設定** で追加したセキュリティ設定を選択し、**AppKey** には NHN Cloud Deploy サービスを使用する Appkey を入力します。

情報を入力後 **[確認]** をクリックすると、入力したセキュリティ設定と Appkey に適合する NHN Cloud Deploy のデプロイ関連情報を取得します。

その後 NHN Cloud Deploy サービスを通じてデプロイする **アーティファクト** 、**サーバーグループ** 、**シナリオ** を選択できます。


**デプロイ制限時間** には該当ステージの実行完了待機時間を指定します。（最小 1 分、最大 600 分）

**デプロイ詳細設定** では、デプロイ対象に対する条件を追加できます。

**サーバー選択** でデプロイするサーバーを選択できます。**全サーバー** を選択すると全サーバーを対象としてデプロイを実行し、**サーバー選択** をクリックするとデプロイするサーバーを選択できます。

**同時サーバー実行数** で NHN Cloud Deploy サービスが同時に実行するサーバー数を選択できます。（デフォルト値 1、最大サーバー数）

**デプロイノート** には、デプロイ実行情報を入力できます。

詳細な説明は [Deploy 使用ガイド](/Dev%20Tools/Deploy/ja/reference/#_1) を参照してください。

![stage-guide-21](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-08-27/pipeline-stage-guide/stage-guide-21_new.png)

### 機能 - ユーザー変数提供
パイプライン内で以降のステージで再利用する変数を定義します。このステージで作成した変数は、接続されたすべての後続ステージで使用でき、最大 5 つの変数を作成できます。

**変数使用方法**

- パイプライン式として参照します。
- （例示）変数名が myImage の場合：

```
${myImage}
```
> 実際の使用時は変数名をステージで指定した値に置き換えて使用してください。（例：`${buildTag}`、`${buildImage}`）

**変数タイプ別説明および例示**

| 変数タイプ                 | 説明                                                                                                                         | 変数値の例                                                                                                                                                                                       |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 自動実行イメージ情報          | パイプラインに **イメージストレージ** タイプで自動実行されたとき、イメージ情報を使用できます。<br/>デフォルト値を設定して自動実行（イメージストレージタイプ）で開始されなかったときに使用する代替値を使用できます。 | 全イメージ名：`dd530b18-kr1-registry.container.nhncloud.com/pipeline-test/image-name:tag`<br/>イメージ名：`dd530b18-kr1-registry.container.nhncloud.com/pipeline-test/image-name`<br/>イメージタグ：`tag` |
| Judgement（実行管理）選択値 | 接続された **機能 - Judgement（実行管理）** ステージで選択した値を変数として作成します。                                                                     | Judgement（実行管理）ステージの `選択値`                                                                                                                                                                | 
| 生成型日付文字列            | **機能 - ユーザー変数提供** ステージが実行された時点を基準に日付文字列を生成します。<br/>日付フォーマットは `java.text.SimpleDateFormat` 規則を使用します。                    | フォーマット：`yyyyMMddHHmmss` -> 変数値：`20250903113846`<br/>フォーマット：`yyyy-MM-dd HH:mm:ss Z` -> 変数値：`2025-09-04 16:58:44 +0900`                                                                            |
| Random UUID           | 8-4-4-4-12 ハイフン表記（計 36 文字）の標準文字列を持つバージョン 4（UUID v4）を生成します。                                                                | `550e8400-e29b-41d4-a716-446655440000`                                                                                                                                                       |
| ユーザー入力値              | 直接入力した値を変数として使用できます。                                                                                                  | `入力値`                                                                                                                                                                                       |

![stage-guide-22](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2025-09-23/stage-guide-22.png)

### 機能 - イメージ脆弱性分析
イメージを対象として脆弱性分析を実行するステージです。

- イメージストレージ
    - **環境設定** の **イメージストレージ設定** で追加した [イメージストレージ](/Dev%20Tools/Pipeline/ja/environment-config/#_3) を選択できます。
- **イメージ名** と **タグ** を入力して分析するイメージを指定します。

![stage-guide-23](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2025-09-23/stage-guide-23.png)

イメージ脆弱性分析結果は、ステージ実行結果で確認でき、脆弱性が発見された場合、分析結果に詳細情報が表示されます。

![stage-guide-24](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2025-09-23/stage-guide-24.png)

### 機能 - ソースコード脆弱性分析

ソースコードを対象として脆弱性分析を実行するステージです。

- ソースリポジトリ
    - **環境設定** の **ソースリポジトリ設定** で追加した [ソースリポジトリ](/Dev%20Tools/Pipeline/ja/environment-config/#_2) を選択できます。
- **ブランチ** を選択して分析するソースコードを指定します。

![stage-guide-25](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2025-09-23/stage-guide-25.png)

ソースコード脆弱性分析結果は、ステージ実行結果で確認でき、脆弱性が発見された場合、分析結果に詳細情報が表示されます。

![stage-guide-26](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2025-09-23/stage-guide-26.png)

## ステージ共通機能
### ステージ失敗時

ステージが失敗した場合、パイプライン実行に関連する設定を選択できます。

- パイプライン全体の終了
    - 該当するステージが失敗すると、パイプライン全体が終了されます。
- 該当するブランチのみ終了
    - 該当するステージが属するブランチのみが終了され、他のブランチのパイプラインは継続して進行されます。
- 該当するブランチが終了され、他のブランチ終了時に失敗
    - 該当するステージが属するブランチのみが終了され、他のブランチのパイプラインは継続して進行されます。ただし、該当するパイプラインの結果は失敗として残ります。
- 失敗を無視して進行
    - 該当するステージが失敗しても、次のステージが進行されます。

![stage-guide-27](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_pipeline/2024-05-28/stage-guide-27.png)