<!-- machine_translated: true -->

<!-- pre-align:aligned sig=8c004103ffd6 -->

<a id="foundry.getting.started"></a>
## Machine Learning > NHN Cloud Foundry > はじめに { #foundry.getting.started }

このドキュメントでは、NHN Cloud Foundry で**レコメンドシステムアプリ**を作成し、レコメンド結果を活用するまでの手順を説明します。
事前準備（サービス利用申請、データ準備）を完了した後、次の手順に従います。

1. データソースの作成
2. アプリの作成
3. アプリのステータス確認
4. レコメンド結果の照会
5. レコメンドイベントの収集

<a id="preparation"></a>
## 事前準備 { #preparation }

<a id="preparation.service.enable"></a>
### サービス利用申請 { #preparation.service.enable }

NHN Cloud Foundry はコンソールから直接有効化することはできません。サービスを利用するには、[1:1 お問い合わせ](https://www.nhncloud.com/kr/support/inquiry)から申請する必要があります。

1. NHN Cloud コンソールで、サービスを利用する組織とプロジェクトを選択します。
2. **[Machine Learning > NHN Cloud Foundry > 現況]** タブで **[1:1 お問い合わせ]** ボタンをクリックし、希望するリソースサイズを含めて利用を申請します。
3. 担当者が該当プロジェクトにサービスを有効化すると、すべての機能を使用できます。

![サービス利用申請](../static/images/quick-start/서비스이용신청.png){ height="70%" }

<a id="preparation.data"></a>
### データの準備 { #preparation.data }

レコメンドシステムアプリを作成するには、次の 3 つの CSV データが必要です。

| データ | 必須カラム | 説明 |
| --- | --- | --- |
| ユーザーテーブル | ユーザー ID | ユーザー情報（追加の特性カラムは任意） |
| アイテムテーブル | アイテム ID | アイテム情報（追加の特性カラムは任意） |
| 履歴テーブル | ユーザー ID、アイテム ID、タイムスタンプ | ユーザーとアイテムの相互作用履歴（評価、カテゴリカラムは任意） |

<a id="datasource.create"></a>
## 1. データソースの作成 { #datasource.create }

**[Machine Learning > NHN Cloud Foundry > データソース]** タブに移動します。
各設定項目の詳細については、[コンソールユーザーガイド](../console-user-guide/#datasource.create)の「データソースの作成」を参照してください。

1. **[データソースの作成]** ボタンをクリックします。

    ![データソースの作成](../static/images/quick-start/데이터소스생성모달1.png){ height="70%" }

2. 基本設定にデータソース名とテーブル名を入力します。
3. 詳細設定で CSV ファイルを選択します。ファイルの先頭行がカラム名の場合は、**[先頭行はヘッダーです]** をチェックします。主キーフィールド（例：`user_id`）を入力します。
4. **[タイプ推論]** ボタンをクリックすると、CSV サンプルからスキーマが自動的に入力されます。誤って推論されたタイプは手動で修正します。

    ![データソースの作成 - ファイル選択とタイプ推論](../static/images/quick-start/데이터소스생성모달2.png){ height="70%" }

5. **[追加]** ボタンをクリックすると、データソースが作成されます。
6. 同様の手順で、**ユーザー**、**アイテム**、**履歴**のデータソースをそれぞれ作成します。
7. 一覧でステータスが COMPLETED になるまで待ちます。

    ![データソース一覧](../static/images/quick-start/데이터소스목록.png){ height="70%" }

<a id="app.create"></a>
## 2. アプリの作成 { #app.create }

**[Machine Learning > NHN Cloud Foundry > アプリ]** タブに移動し、**[アプリの作成]** ボタンをクリックします。
各設定項目の詳細については、[コンソールユーザーガイド](../console-user-guide/#app.create)の「アプリの作成」を参照してください。

<a id="app.create.basic"></a>
### 基本設定 { #app.create.basic }

アプリ名とアプリの説明を入力し、アプリタイプとして **[レコメンドシステム]** を選択してから、**[次へ]** をクリックします。

![アプリの作成 - 基本設定](../static/images/quick-start/앱생성화면1.png){ height="70%" }

<a id="app.create.detail"></a>
### 詳細設定 { #app.create.detail }

1. **[モデルの追加]** ボタンをクリックして、使用するモデルを追加します。新規サービスの場合は **[Cold User]**、ユーザーの行動履歴が十分にある場合は **[Warm User(Transformer)]** モデルをお勧めします。

    ![アプリの作成 - モデル設定](../static/images/quick-start/앱생성화면2.png){ height="70%" }

2. モデルカードの **[データ連携設定]** で、「1. データソースの作成」で作成したユーザー・アイテム・履歴のデータソースをそれぞれ選択します。
   ユーザー ID・アイテム ID のカラムと、履歴の時間カラムを指定します。Feature カラムは必要な場合にのみ選択します。

    ![アプリの作成 - データ連携設定](../static/images/quick-start/앱생성화면3.png){ height="70%" }

3. 必要に応じて **[追加設定(Skills)]** でスキルテーブルなどを連携します。基本モデル設定の Longtail モード（人気度の低いアイテムもレコメンドに含める）を指定します。設定が完了したら **[次へ]** をクリックします。

    ![アプリの作成 - 追加設定](../static/images/quick-start/앱생성화면4.png){ height="70%" }

<a id="app.create.review"></a>
### 最終確認 { #app.create.review }

1. 入力した基本設定、モデル設定、追加設定を確認します。
2. **[保存]** ボタンをクリックすると、アプリが作成されます。

![アプリの作成 - 最終確認](../static/images/quick-start/앱생성화면5.png){ height="70%" }

<a id="app.status"></a>
## 3. アプリのステータス確認 { #app.status }

アプリの作成後、学習とデプロイが自動的に進行します。ステータスは、初期化中、学習中、デプロイ中、有効化中を経て、アクティブに変わります。
アプリ一覧でステータスがアクティブになるまで待ちます。

![アプリ一覧](../static/images/quick-start/앱목록.png){ height="70%" }

ステータス値の詳細については、[コンソールユーザーガイド](../console-user-guide/#app.list.status)の「アプリのステータス」を参照してください。

!!! tip "ヒント"
    アプリ作成直後の学習・デプロイは、アプリを準備するプロセスです。レコメンドモデルの初回学習は、バッチスケジュール設定で指定した時刻に実行されます。それ以前にレコメンド API がレスポンスを返しても、学習済みモデルのレコメンド結果ではありません。

<a id="recommendation.query"></a>
## 4. レコメンド結果の照会 { #recommendation.query }

アプリがアクティブ状態になると、コンソールのレコメンド API 呼び出し画面でレコメンド結果を確認するか、レコメンド照会 API を呼び出してレコメンド結果を照会できます。
各項目の詳細については、[コンソールユーザーガイド](../console-user-guide/#app.detail.recommend)の「レコメンド API 呼び出し」を参照してください。

1. アプリ一覧で作成したアプリをクリックし、詳細画面の **[レコメンド API 呼び出し]** タブに移動します。
2. ユーザー ID を入力し、レコメンドモードと最大レコメンド数を指定します。
3. **[レコメンドリクエスト]** ボタンをクリックすると、レコメンド結果に順位、アイテムキー、スコアが表示され、総結果数と応答時間も確認できます。

    ![レコメンド API 呼び出し](../static/images/quick-start/추천API호출.png){ height="70%" }

**[リクエストプレビュー]** には、入力値で構成された実際の API リクエスト JSON が表示されます。**[コピー]** ボタンでコピーして、API 連携開発に活用できます。
レコメンド照会 API を直接呼び出す方法については、[API ガイド](../api-guide/#recommendation.api)の「レコメンド照会 API」を参照してください。

レスポンスには、リクエスト識別子（`metadata.requestId`）とレコメンドアイテム一覧（`recommendations[].itemKey`）が含まれます。この値は、次のステップのレコメンドイベント送信に使用されます。

**[アプリ情報]** タブでは、API 呼び出しに使用するアプリ ID、ステータス、バージョンを確認できます。

![アプリ情報](../static/images/quick-start/앱정보.png){ height="70%" }

<a id="recommendation.event"></a>
## 5. レコメンドイベントの収集 { #recommendation.event }

ユーザーがレコメンド結果をクリックするなどの反応が発生した場合、レコメンドイベント API で送信します。蓄積されたイベントデータを使用して、レコメンドの成功率を分析できます。
リクエストフィールドの詳細については、[API ガイド](../api-guide/#recommendation.event.api)の「レコメンドイベント API」を参照してください。

```bash
curl -X POST '{URL}/api/v1.0/recommendation-apps/{APP_ID}/events' \
  -H "X-NC-APP-KEY: {APP_KEY}" \
  -H "Content-Type: application/json" \
  -H "X-NHN-Authorization: {AUTH_TOKEN}" \
  -d '{
    "eventType": "CLICK",
    "requestId": "{RecommendApiResponse.body.metadata.requestId}",
    "itemKey": "{RecommendApiResponse.body.recommendations.itemKey}",
    "userId": "{RecommendApiResponse.body.userId}",
    "context": {
      "position": 1,
      "placement": "home_main"
    }
  }'
```

!!! tip "ヒント"
    イベント API のリクエスト後、データセットへの反映まで最大 10 分かかる場合があります。

<a id="univariate.datasource"></a>
### 1. 指標データソースの作成 { #univariate.datasource }

**Machine Learning > NHN Cloud Foundry > データソース** タブで **[データソース作成]** ボタンをクリックします。

1. 基本設定にデータソース名とテーブル名を入力します。
2. 接続設定でデータソースタイプを**Prometheus API**として選択します。
3. 詳細設定でシリーズ識別ラベルとグループラベルを指定します。
    - スキーマは固定なので、直接入力しません。
    - **[例を表示]**では、入力したラベルでシリーズとグループが何個に分かれるか確認できます。
4. **[追加]**ボタンをクリックし、完了ウィンドウに「準備が完了しました。」が表示されるまで待ちます。
    - 完了ウィンドウには、収集方法（エンドポイント、リクエストヘッダ、リクエストボディの例、ルール）が一緒に表示されます。
    - リストではステータスが`COMPLETED`として表示されます。

![指標データソース作成](../static/images/quick-start/지표데이터소스생성.png){ height="70%" }

各項目の詳細説明については、[コンソールユーザーガイド](../console-user-guide/#datasource.create.detail.prometheus)の「Prometheus API 詳細設定」を参照してください。

<a id="univariate.ingest"></a>
### 2. 指標の送信 { #univariate.ingest }

データソース作成完了ウィンドウまたは詳細表示の **[収集方法]** タブで、エンドポイントとリクエストヘッダ、リクエストボディの例を **[コピー]** ボタンでコピーし、指標を送信します。リクエストヘッダの認証トークン欄に、発行したトークンを入力します。

![収集方法](../static/images/quick-start/수집방법.png){ height="70%" }

```bash
curl -X POST '{URL}/api/v1.0/data-sources/{DATA_SOURCE_ID}/ingest/metrics' \
  -H "X-NC-APP-KEY: {APP_KEY}" \
  -H "X-NHN-Authorization: {AUTH_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "metrics": [
      {
        "timestamp": 1776149886528,
        "value": 4.99,
        "labels": [
          { "name": "__name__", "value": "cpu_usage" },
          { "name": "instance_id", "value": "instance-001" }
        ]
      }
    ]
  }'
```

リクエスト形式の詳細説明については、[API ガイド](../api-guide/#metrics.ingest.api)の「指標収集」を参照してください。

!!! tip "ヒント"
    アプリを作成した後は、同じ時系列の指標を1分に1つずつ中断なく送信します。それより長い間隔で送信すると、空の期間が生じ、正確モードで準備が完了しない可能性があります。1分以内に複数の値を送信すると、最初に到着した値だけが使用されます。より短い周期で収集する場合は、1分間の平均に集約して送信します。

<a id="univariate.app"></a>
### 3. アプリを作成する { #univariate.app }

**Machine Learning > NHN Cloud Foundry > アプリ** タブで **[アプリ作成]** ボタンをクリックします。

1. **[基本設定]** にアプリ名と説明を入力し、**[アプリタイプ]** で **[単変量異常検出]** を選択します。

    ![アプリ作成 - 基本設定](../static/images/quick-start/이상탐지앱생성1.png){ height="70%" }

2. **[詳細設定]** で先に作成した指標データソースを選択します。
    - モデルリソース、再学習周期、検出オプション、結果転送を指定します。
    - 再学習周期を指定しない場合、アプリを作成するとき1回だけ学習します。この場合、データがないデータソースではアプリを作成することができないため、まず指標を送信します。

    ![アプリ作成 - 詳細設定](../static/images/quick-start/이상탐지앱생성2.png){ height="70%" }

3. **[最終確認]** で入力内容を確認し、**[保存]** ボタンをクリックします。
    - 完了画面では、学習・デプロイの進行と結果が表示されるまでにかかる時間が案内されます。その間、指標を送り続けます。

各項目の詳細については、[コンソール ユーザーガイド](../console-user-guide/#app.create.detail.univariate)の「単変量異常検出の詳細設定」を参照してください。

!!! tip "ヒント"
    指標データソース 1 つには、単変量異常検出アプリを 1 つだけ作成できます。結果転送の転送モードは、デフォルトである正確モードをお勧めします。ただし、準備が完了する前の値をすぐに受け取りたい場合は、即座モードを選択します。

<a id="univariate.result"></a>
### 4. 検知結果の確認 { #univariate.result }

アプリ一覧で作成したアプリをクリックして、詳細画面に移動します。

1. **[アプリ情報]** タブで学習状態とグループ現況を確認します。

    ![単変量異常検出アプリ情報](../static/images/quick-start/이상탐지앱정보.png){ height="70%" }

2. **[グループ一覧]** タブでグループの状態を確認します。
    - グループは指標が入ってきた後に登録されるため、アプリを作成した直後にはリストが空です。
    - 有効化待機中は判定に使用するデータを集めている最中で、有効化されると検知結果が転送されます。
    - 有効化時刻カラムで、グループがいつから結果を送信し始めたか確認できます。

    ![グループ一覧](../static/images/quick-start/이상탐지그룹목록.png){ height="70%" }

3. 検知結果である異常スコアとしきい値は指定した Prometheus に転送され、結果データソースにも保存されます。
4. 保存された結果は **[分析]** タブのクエリやチャートで照会します。

各項目の詳細な説明は、[コンソールユーザーガイド](../console-user-guide/#app.detail.univariate)の「単変量異常検出アプリ詳細」を参照します。