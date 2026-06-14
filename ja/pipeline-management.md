## Dev Tools > Pipeline > コンソール使用ガイド > パイプライン管理

パイプラインは、1つ以上のステージで構成されたアプリケーション配布フローを定義します。

### パイプライン構成

#### パイプライン作成

**+ パイプライン作成**をクリックしてパイプラインを作成でき、パイプラインテンプレートファイルをアップロードしてパイプラインを作成することもできます。
![pipeline-management-guide-01](https://static.toastoven.net/prod2_translate-test/ja/management-guide-01.png)

**パイプライン管理**で**+ パイプライン作成**をクリックします。

![pipeline-management-guide-02](https://static.toastoven.net/prod2_translate-test/ja/management-guide-02.png)

**パイプライン作成**モーダルウィンドウで**パイプライン名**と**パイプライン説明**を入力した後、**確認**をクリックします。

または、パイプラインテンプレートファイルでパイプラインを作成することもできます（パイプラインテンプレートはJSONファイルを使用します）。

![pipeline-management-guide-03](https://static.toastoven.net/prod2_translate-test/ja/management-guide-03.png)

パイプラインテンプレートファイルをアップロードした後、**確認**をクリックします。

#### パイプラインスタジオ

パイプラインスタジオは、ユーザーがパイプラインの基本情報を管理したり、パイプラインを構成するステージを追加、変更、削除できるページです。

![pipeline-studio-guide-01](https://static.toastoven.net/prod2_translate-test/ja/guide-1.png)

パイプラインスタジオの上部には、パイプラインの名前、説明、最終修正日、作成者の基本情報が表示されます。

パイプラインスタジオパネルでは、該当パイプラインを構成するステージを確認できます。

#### 編集モード
![pipeline-studio-guide-08](https://static.toastoven.net/prod2_translate-test/ja/guide-2.png)

右上の**編集モード**トグルをクリックして編集モードに入ることができます。編集モードでは、ステージの追加、変更、削除、および位置変更を実行できます。

#### ステージ追加
![pipeline-studio-guide-09](https://static.toastoven.net/prod2_translate-test/ja/guide-3.png)

**編集モード**を有効にすると、左側にアプリケーション配布フローを構成する際に使用できる様々なステージで構成された**ソース**、**ビルド**、**配布**、**機能**グループが表示されます。

4つのグループから追加するステージを選択して、ドラッグアンドドロップで画面に配置できます。

![pipeline-studio-guide-10](https://static.toastoven.net/prod2_translate-test/ja/guide-4.png)

ステージが追加されると、該当ステージを選択して必須情報を入力します。

![pipeline-studio-guide-11](https://static.toastoven.net/prod2_translate-test/ja/guide-5.png)

以前に実行するステージと追加するステージを接続して、実行順序を設定します。

![pipeline-studio-guide-12](https://static.toastoven.net/prod2_translate-test/ja/guide-6.png)

右上の**パイプライン保存**をクリックしてステージ追加を完了できます。

#### ステージ編集
![pipeline-studio-guide-13](https://static.toastoven.net/prod2_translate-test/ja/guide-7.png)

**編集モード**を有効化した後、編集するステージをクリックしてステージを編集できます。

![pipeline-studio-guide-14](https://static.toastoven.net/prod2_translate-test/ja/guide-9.png)

編集完了後、右上の**パイプライン保存**をクリックしてステージ編集を完了できます。

#### ステージ削除
![pipeline-studio-guide-15](https://static.toastoven.net/prod2_translate-test/ja/guide-10.png)

![pipeline-studio-guide-16](https://static.toastoven.net/prod2_translate-test/ja/guide-11.png)

**編集モード**を有効化した後、削除するステージの右上**X**をクリックしてステージを削除できます。

![pipeline-studio-guide-17](https://static.toastoven.net/prod2_translate-test/ja/guide-12.png)

削除後、右上の**パイプライン保存**をクリックしてステージ削除を完了できます。

### パイプライン実行

パイプラインは手動または自動で実行できます。

#### 手動実行

手動実行を使用すると、ユーザーが必要な時にパイプラインを実行できます。

![pipeline-management-guide-12](https://static.toastoven.net/prod2_translate-test/ja/management-guide-12.png)

**パイプライン管理**で**▶︎ 実行**をクリックした後、**パイプライン実行**モーダルウィンドウが表示されたら内容を確認して**確認**をクリックします。

#### 自動実行

自動実行を使用すると、GitHubまたはGitLabリポジトリでイベントが発生したり、イメージストアのコンテナイメージを更新した際にパイプラインが自動的に実行されるよう設定できます。

![management-guide-04](https://static.toastoven.net/prod2_translate-test/ja/management-guide-04.png)
![management-guide-05](https://static.toastoven.net/prod2_translate-test/ja/management-guide-05.png)

**自動実行設定**をクリックした後、**自動実行設定**モーダルウィンドウで**追加**をクリックします。

* GitHub自動実行設定
![management-guide-06](https://static.toastoven.net/prod2_translate-test/ja/management-guide-06.png)

GitHubウェブフックを使用してGitHubまたはGitHub Enterpriseのリポジトリでイベントが発生した際に、パイプラインが自動的に実行されるよう設定できます。**自動実行タイプ**を**GitHub**に設定し、リポジトリの**組織名またはユーザー名**、**プロジェクト名**、**ブランチまたはタグ**、**シークレット**を入力して**確認**をクリックします。

タグで自動実行を設定するには、**ブランチまたはタグ**項目に`refs/tags/タグ名`のようにタグ名を入力します。`タグ名`部分にはJAVA正規表現を使用できます。

タグで自動実行設定後、NHN Cloudビルドツール使用時に設定されたタグでビルドを実行します。ビルド - Jenkinsステージでタグでビルドを実行するには、次のように設定する必要があります。

Jenkinsで次のようにパラメータを設定します。
![pipeline-guide-39.png](https://static.toastoven.net/prod2_translate-test/ja/pipeline-guide-39.png)
![pipeline-guide-40.png](https://static.toastoven.net/prod2_translate-test/ja/pipeline-guide-40.png)

Pipelineのビルドツール設定で**ビルドジョブパラメータ**に次のように入力します。

![management-guide-10](https://static.toastoven.net/prod2_translate-test/ja/management-guide-10.png)

* GitHubウェブフック設定値

![pipeline-guide-16](https://static.toastoven.net/prod2_translate-test/ja/pipeline-guide-16.png)

| 項目 | 設定値 |
|---|---|
| Payload URL | https://kr1-pipeline.api.nhncloudservice.com/webhooks/git/github |
| Content type | application/json |
| Secret | パイプライン自動実行設定のシークレットに入力した値 |
| event | push event, create event(タグ使用時) |

特定ファイルがPushされた時のみ自動実行されるよう設定できます（最大5個）。

![management-guide-13](https://static.toastoven.net/prod2_translate-test/ja/management-guide-13.png)

**ソースリポジトリ名**は環境設定で登録したソースリポジトリを選択します。
**GitHubファイルパス**は選択したソースリポジトリでファイルが含まれたパスを入力します。

* GitLab自動実行設定

![management-guide-07](https://static.toastoven.net/prod2_translate-test/ja/management-guide-07.png)

GitLabウェブフックを使用してGitLabリポジトリでイベントが発生した際にパイプラインが自動的に実行されるよう設定できます。**自動実行タイプ**を**GitLab**に設定し、リポジトリの**組織名またはユーザー名**、**プロジェクト名**、**ブランチまたはタグ**を入力して**確認**をクリックします。GitLabシークレット設定は今後サポートする予定です。

* GitLabウェブフック設定値

![pipeline-guide-18](https://static.toastoven.net/prod2_translate-test/ja/pipeline-guide-18.png)

| 項目 | 設定値 |
|---|---|
| URL | https://kr1-pipeline.api.nhncloudservice.com/webhooks/git/gitlab |
| Trigger | Push eventsチェック |
| Secret | 設定しない |
| SSL verification | Enable SSL verificationチェック |

* GitLabウェブフック設定時の注意事項

GitLabのユーザー名で自動実行を設定する際、ユーザー名をGitLabのユーザー名と同じく設定する必要があります。ユーザー名を異なって設定した場合、自動実行が動作しない場合があります。

![pipeline-guide-19](https://static.toastoven.net/prod2_translate-test/ja/pipeline-guide-19.png)

* イメージストア自動実行設定

![management-guide-08](https://static.toastoven.net/prod2_translate-test/ja/management-guide-08.png)

コンテナイメージを更新した時にパイプラインを自動的に実行するには、**自動実行タイプ**を**イメージストア**に設定します。
**イメージストア**を**環境設定**で登録した項目として選択した後、**イメージ名**を入力します。イメージ名はNHN Cloud Container Registryの場合`レジストリ名/イメージ名`の形式で入力します。
Docker Hubの場合`Docker Hubアカウント/イメージ名`形式で入力します。**タグ**はJAVA正規表現を使用でき、入力したタグとマッチするタグがpushされた場合に自動実行されます。
タグを入力しなければ、latestを除く新規タグがpushされた場合に自動実行されます。
入力完了後、**確認**をクリックします。

![management-guide-09](https://static.toastoven.net/prod2_translate-test/ja/management-guide-09.png)

パイプラインを新規作成すると、**自動実行**のトグルスイッチがオフ状態で適用されます。パイプラインを自動的に実行するには、**自動実行**トグルスイッチをクリックして有効化する必要があります。

### パイプライン管理

ユーザーはパイプラインの基本情報を修正できます。
![pipeline-studio-guide-02](https://static.toastoven.net/prod2_translate-test/ja/guide-13.png)

パイプライン名横の修正アイコンをクリックして、パイプラインの名前と説明を修正できます。

情報を修正した後、**確認**をクリックして修正を完了できます。

![pipeline-studio-guide-03](https://static.toastoven.net/prod2_translate-test/ja/guide-14.png)

**▶ 手動実行**をクリックして該当パイプラインを実行でき、**■ 実行停止**をクリックして実行中のパイプラインを停止できます。

#### 最近実行情報確認

パイプラインの最近実行に関する各ステージ別基本情報と実行状態を確認するには、**最近実行情報**をクリックします。

![pipeline-studio-guide-05](https://static.toastoven.net/prod2_translate-test/ja/guide-16.png)

#### パイプラインJSONダウンロード

![pipeline-studio-guide-05](https://static.toastoven.net/prod2_translate-test/ja/guide-17.png)

**パイプラインバージョン**をクリックしてJSON形式でパイプラインを確認できます。

左上のパイプライン修正日が表示されたドロップダウンボタンをクリックして修正日別に確認できます。

右上**パイプラインテンプレートダウンロード**をクリックしてJSONファイルで保存できます。

#### パイプライン通知
パイプラインの開始、完了、失敗に関するEmail、SMS通知を管理する機能です。

![pipeline-management-guide-13](https://static.toastoven.net/prod2_translate-test/ja/pipeline-management-guide-13.png)

**パイプライン通知**をクリックして通知を設定できます。

**プロジェクト設定** > **通知管理**で通知受信者管理が可能です。

通知受信対象および通知方法（Email、SMS）に関する設定は[通知管理ガイド](https://docs.nhncloud.com/ko/nhncloud/ko/console-guide/#_33)を参照してください。

#### パイプライン実行履歴
パイプラインスタジオで**実行履歴**をクリックすると、最近10個の履歴を確認できます。
![pipeline-management-guide-14](https://static.toastoven.net/prod2_translate-test/ja/pipeline-management-guide-14.png)

![pipeline-management-guide-15](https://static.toastoven.net/prod2_translate-test/ja/pipeline-management-guide-15.png)

実行履歴モーダルウィンドウの左側領域で確認する実行履歴を選択すると、右側領域に各ステージの詳細情報が表示されます。

**状態**列でパイプラインの実行状態を確認でき、**取消**をクリックしてパイプライン実行をキャンセルできます。

**機能 - 承認管理**、**機能 - Judgement(実行管理)**などのステージは、**管理**をクリックしてパイプラインの実行管理を行うことができます。