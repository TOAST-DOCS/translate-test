<!-- machine_translated: true -->

<!-- pre-align:aligned sig=40aa83d794a8 -->

<a id="dev-tools-deploy-console-user-guide"></a>
## Dev Tools > Deploy > コンソール使用ガイド { #dev-tools-deploy-console-user-guide }

このドキュメントでは、次の内容について説明します。

* [Deployコンソール画面](#deploy-console-page)
* [Client Application](#client-application)
* [Server Application](#server-application)

(ここで取り上げていない機能は、[機能詳細ガイド](./reference/)で確認できます。)

<a id="deploy-console-page"></a>
## Deployコンソール画面 { #deploy-console-page }

次はDeployサービスのコンソール画面です。

![deploy_02_201812](https://static.toastoven.net/prod_tcdeploy/deploy_02_201812.png)

<a id="client-application"></a>
## Client Application { #client-application }

クライアントアプリケーションのデプロイ設定は、大きくアーティファクト設定とバイナリアップロードの段階を経ます。

<a id="setting-artifacts"></a>
### アーティファクト設定 { #setting-artifacts }

![deploy_03_201812](https://static.toastoven.net/prod_tcdeploy/deploy_03_201812.png)

1. **Deploy**画面の左上で**[作成]**ボタンをクリックします。
2. アーティファクトのタイプを**[Client Application]**として選択します。
    - 名前(必須)、説明(任意)、port(必須)を入力します。
3. **[作成]**ボタンをクリックします。

<a id="setting-binaries"></a>
### バイナリ設定 { #setting-binaries }

<a id="upload"></a>
#### アップロード

* iOSは.ipa、.plistファイルを、Androidは.apkファイルをそれぞれアップロードします。
* etcの場合は、Windowsなどその他のOSのインストールアプリケーション用途で使用します。

![deploy_04_201812](https://static.toastoven.net/prod_tcdeploy/deploy_04_201812.png)

1. **Deploy**画面下部のタブで**[バイナリグループ] > [Default]**をクリックします。
    新しいバイナリグループを作成するには、**[新規作成]**ボタンをクリックします。
2. 右側の**[アップロード]**ボタンをクリックします。
3. **[バイナリアップロード]**ウィンドウで**[ファイル選択]**ボタンをクリックし、バイナリファイルを選択します。
    * iOS：.ipaファイル(必須)、.plistファイル(必須)
        * .plist：ダウンロードページでのインストールに使用します。ファイル内のダウンロードURLは任意入力です。
    * Android：.apkファイル(必須)
    * バージョン(任意)、説明(任意)の情報を入力
4. 入力を完了し、**[アップロード]**ボタンをクリックします。

<a id="deploy"></a>
#### デプロイ

特定のバイナリのダウンロードページをSMSまたはE-mailで送信できます。

![deploy_27_202407](https://static.toastoven.net/prod_tcdeploy/deploy_27_202407.png)
![deploy_28_202407](https://static.toastoven.net/prod_tcdeploy/deploy_28_202407.png)
![deploy_29_202407](https://static.toastoven.net/prod_tcdeploy/deploy_29_202407.png)

1. 右側の**[送信]**ボタンをクリックします。
2. **[ダウンロードパス送信]**ウィンドウで**[送信タイプ]**と**[受信者]**を設定し、**[送信]**ボタンをクリックします。
    * **[送信タイプ]**は**[SMS]**または**[E-mail]**のいずれかを選択するか、両方選択することもできます。
    * **[個別選択]**で受信者を個別に選択でき、**[グループ選択]**で通知受信グループを選択できます。
    * **[グループ選択]**タブを選択し、**[詳細]**列の**[表示]**ボタンをクリックすると、プロジェクト通知受信グループ管理ウィンドウが開きます。

指定した送信タイプで受信者にバイナリのダウンロードページが送信されます。

<a id="server-application"></a>
## Server Application { #server-application }

サーバーアプリケーションのデプロイ設定(アーティファクト、サーバーグループ、シナリオ)、バイナリアップロード、デプロイの段階を経ます。

<a id="server-application-setting-artifacts"></a>
### アーティファクト設定 { #server-application-setting-artifacts }

![deploy_06_201812](https://static.toastoven.net/prod_tcdeploy/deploy_06_201812.png)

1. リスト上の**[作成]**ボタンをクリックします。
2. アーティファクトのタイプを**[Server Application]**として選択します。
    - 名前(必須)、説明(任意)、port(必須)の項目を入力します。
3. **[アーティファクト作成]**ウィンドウで**[作成]**ボタンをクリックします。

<a id="setting-server-groups"></a>
### サーバーグループ設定 { #setting-server-groups }

デプロイするサーバーを管理できる機能です。

![deploy_07_201812](https://static.toastoven.net/prod_tcdeploy/deploy_07_201812.png)

1. **Deploy**画面下部のタブで**[サーバーグループ] > [新規作成]**をクリックします。
2. **[サーバーグループ作成]**ウィンドウで新しく作成するサーバーグループを設定します。
    * 名前(必須)、説明(任意)を入力します。
    * OSを選択し、Shell Typeを指定します。Shell Typeは**[Shell Type]**リストから選択するか、直接入力できます。
    * Phaseを選択します。サーバー機器を区分します。指定しない場合はNONEを選択します。
    * サーバーの追加
        * サーバーを追加する方法は次の2つであり、詳細は[機能詳細ガイドのサーバーグループメニュー](./reference/#server-group)で確認できます。
            * 一括追加
            * 個別追加
         * ホスト名(必須)、IPアドレス(必須)、OS(任意)を入力し、**[追加]**ボタンをクリックします。
         * 下のサーバーリストに追加された内容を確認します。左側のチェックボックスが選択されたサーバーのみ登録されます。

3. 入力を完了し、**[作成]**ボタンをクリックします。

<a id="setting-binary-groups"></a>
### バイナリグループ設定 { #setting-binary-groups }

デプロイするバイナリを管理できる機能です。

![deploy_25_202402](https://static.toastoven.net/prod_tcdeploy/deploy_25_202402.png)
![deploy_26_202402](https://static.toastoven.net/prod_tcdeploy/deploy_26_202402.png)

1. **Deploy**画面下部のタブで**[バイナリグループ] > [新規作成]**をクリックします。
    * アーティファクト作成時にDefaultバイナリグループは自動作成されます。
2. **[バイナリグループ作成]**ウィンドウで新しく作成するバイナリグループを設定します。
    * 名前、説明、リージョンを入力します。
        * **[リージョン]**はデプロイ対象サーバーのリージョンと異なる場合、ネットワーク遅延時間が長くなる可能性があります。
    * 自動削除設定を入力します。
        * 期間、容量、個数などの条件でバイナリを定期的に削除する機能です。 
        * 最大個数と最小維持個数は必須の値で、最大10個まで設定できます。
3. 入力を完了し、**[作成]**ボタンをクリックします。

<a id="create-scenarios"></a>
### シナリオ作成 { #create-scenarios }

![deploy_08_201812](https://static.toastoven.net/prod_tcdeploy/deploy_08_201812.png)

1. **Deploy**画面下部のタブで**[デプロイ] > [新規作成]**ボタンをクリックします。
2. 下部に追加されたシナリオ領域にシナリオ名(任意)を入力します。
3. **[作成]**ボタンをクリックします。

<a id="add-tasks"></a>
### タスク追加 { #add-tasks }

タスクは個別の機能を実行し、順序を制御できるシナリオの構成要素です。
タスクの種類は次の2つです。

* pre-run Task：デプロイ前に実行する機能
* Normal Task：デプロイ時に実行する機能

任意のものを選択して使用できます。ここでは、基本的なデプロイ時に必要なタスクを取り上げます。
その他のタスクは[機能詳細ガイドのタスクメニュー](./reference/#tasks)で確認できます。

デプロイテストのために、次の3つのタスクを追加します。

<a id="add-user-commands"></a>
#### 1. User Command追加

* デプロイ時に実行されるユーザー定義のCommandタスクです。
* Available Variablesを使用できます。
    * Available Variables：予約語。詳細は[機能詳細ガイドのタスクメニュー](./reference/#tasks)で確認できます。

![deploy_09_201812](https://static.toastoven.net/prod_tcdeploy/deploy_09_201812.png)

1. **[デプロイ]**タブのシナリオ領域右側で**[Task追加]**ボタンをクリックします。
2. **[Normal Task]**の下にある**[User Command]**をクリックします。
3. 新しいタスクの内容を入力します。
    * Timeout(min)
        * 該当タスクの実行完了待機時間を指定します。最小1分、最大30分。
    * Run As
        * 実行アカウントを入力します。
    * Command
        * 実行するコマンドを入力します。

4. 入力または変更を完了した後、**[適用]**ボタンをクリックします。

<a id="add-binary-deploy"></a>
#### 2. Binary Deploy追加

アップロードしたバイナリファイルのデプロイ内容を設定できるタスクです。

![deploy_10_201812](https://static.toastoven.net/prod_tcdeploy/deploy_10_201812.png)

1. **[Task追加]**ボタンをクリックし、**[Normal Task]**の下にある**[Binary Deploy]**をクリックします。
2. 新しいタスクの内容を入力します。
    * Timeout(min)
        * 該当タスクの実行完了待機時間を指定します。最小1分、最大30分。
    * Run As
        * 実行アカウントを入力します。
3. バイナリファイルをアップロードするには、右側の**[アップロード]**ボタンをクリックします。
4. バイナリファイルの情報を入力します。
    * **[ファイル選択]**ボタンをクリックして、バイナリファイルを選択します。
    * バージョン(任意)、説明(任意)の項目を入力します。
5. **[アップロード]**ボタンをクリックします。
6. アップロード完了後、**[バイナリ選択]**ボタンをクリックします。
7. 任意のバイナリバージョンを選択します。
    * 複数のバージョンがある場合は、検索機能を活用します。
8. **[選択]**ボタンをクリックします。
  <br/>
   * Variable As
       * 該当バイナリのVariable名を指定し、User Commandでバイナリ情報を使用できます。詳細は[機能詳細ガイド](./reference/)のタスクメニュー下部で確認できます。
   * ターゲットディレクトリ
       * バイナリをデプロイするターゲットディレクトリを指定します。

<a id="add-tasks-add-user-commands"></a>
#### 3. User Command追加

![deploy_11_201812](https://static.toastoven.net/prod_tcdeploy/deploy_11_201812.png)

1. **[Task追加]**ボタンをクリックし、**[Normal Task]**の下にある**[User Command]**をクリックします。
2. 新しいタスクの内容を入力します。
    * Timeout(min)
        * 該当タスクの実行完了待機時間を指定します。最小1分、最大30分。
    * Run As
        * 実行アカウントを入力します。
    * Command
        * 実行するコマンドを入力します。
3. 入力または変更を完了した後、**[適用]**ボタンをクリックします。

<a id="execute"></a>
### 実行 { #execute }

![deploy_12_201812](https://static.toastoven.net/prod_tcdeploy/deploy_12_201812.png)

1. 右側の**[実行]**ボタンをクリックし、デプロイをリクエストします。
2. デプロイ実行情報を入力します。
    * デプロイノート(任意)および認証方法を指定します。
    * **[Password]**を選択した場合、パスワードを入力するか、.pemファイルを選択してアップロードします。
3. 入力を完了した後、**[確認]**ボタンをクリックします。

![deploy_13_201812](https://static.toastoven.net/prod_tcdeploy/deploy_13_201812.png)

1. デプロイの進行状況を確認できます。
2. デプロイ完了を確認します。
    * 各タスクの正常実行の有無はexit codeで確認できます。
3. 詳細結果を確認するには、**[結果表示]**ボタンをクリックします。
4. **[結果表示]**ウィンドウでデプロイ結果を確認します。
    * 各タスクの実行に関する詳細(戻り値、exit code、エラー内容など)を確認できます。

- - -

サーバーにファイルをデプロイしました！
NHN Cloud Deployはさらに多くの機能をサポートしており、詳細は[機能詳細ガイド](./reference/)で確認できます。