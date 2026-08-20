<!-- machine_translated: true -->

<a id="foundry.getting.started"></a>

## Machine Learning > NHN Cloud Foundry > はじめに { #foundry.getting.started }

このドキュメントでは、NHN Cloud Foundry で**推薦システムアプリ**を作成し、推薦結果を活用するまでの流れを説明します。
事前準備（サービス利用申請、データ準備）を完了した後、次の順序で進めます。

1. データソースを作成する
2. アプリを作成する
3. アプリの状態を確認する
4. 推薦結果を照会する
5. 推薦イベントを収集する

<a id="preparation"></a>

## 事前準備 { #preparation }

<a id="preparation.service.enable"></a>

### サービス利用申請 { #preparation.service.enable }

NHN Cloud Foundry はコンソールから直接有効化することはできません。サービスを利用するには、[1:1お問い合わせ](https://www.nhncloud.com/kr/support/inquiry)から申請する必要があります。

1. NHN Cloud コンソールで、サービスを利用する組織とプロジェクトを選択します。
2. **Machine Learning > NHN Cloud Foundry > 現況** タブで **[1:1お問い合わせ]** ボタンをクリックし、希望するリソースサイズを含めて利用を申請します。
3. 担当者が対象プロジェクトでサービスを有効化すると、すべての機能を使用できます。

![サービス利用申請](../static/images/quick-start/서비스이용신청.png){ height="70%" }

<a id="preparation.data"></a>

### データ準備 { #preparation.data }

推薦システムアプリを作成するには、次の3つの CSV データが必要です。

| データ | 必須カラム | 説明 |
| --- | --- | --- |
| ユーザーテーブル | ユーザーID | ユーザー情報（追加の特性カラムを選択可能） |
| アイテムテーブル | アイテムID | アイテム情報（追加の特性カラムを選択可能） |
| ヒストリーテーブル | ユーザーID、アイテムID、タイムスタンプ | ユーザーとアイテムの相互作用履歴（評点、カテゴリカラムを選択可能） |

<a id="datasource.create"></a>

## 1. データソースを作成する { #datasource.create }

**Machine Learning > NHN Cloud Foundry > データソース** タブに移動します。
各設定項目の詳細については、[コンソール使用ガイド](./console-user-guide/#datasource.create)の「データソースの作成」を参照してください。

1. **[データソース作成]** ボタンをクリックします。

    ![データソース作成](../static/images/quick-start/데이터소스생성모달1.png){ height="70%" }

2. 基本設定にデータソース名とテーブル名を入力します。
3. 詳細設定で CSV ファイルを選択し、ファイルの先頭行がカラム名の場合は **[最初の行はヘッダです]** にチェックを入れます。プライマリキーフィールド（例：`user_id`）を入力します。
4. **[タイプ推論]** ボタンをクリックすると、CSV サンプルからスキーマが自動的に入力されます。誤って推論されたタイプは手動で修正します。

    ![データソース作成 - ファイル選択とタイプ推論](../static/images/quick-start/데이터소스생성모달2.png){ height="70%" }

5. **[追加]** ボタンをクリックすると、データソースが作成されます。
6. 同じ手順で**ユーザー、アイテム、ヒストリー**のデータソースをそれぞれ作成します。
7. 一覧でステータスが COMPLETED になるまで待ちます。

    ![データソース一覧](../static/images/quick-start/데이터소스목록.png){ height="70%" }

<a id="app.create"></a>

## 2. アプリを作成する { #app.create }

**Machine Learning > NHN Cloud Foundry > アプリ** タブに移動し、**[アプリ作成]** ボタンをクリックします。
各設定項目の詳細については、[コンソール使用ガイド](./console-user-guide/#app.create)の「アプリの作成」を参照してください。

<a id="app.create.basic"></a>

### 基本設定 { #app.create.basic }

アプリ名とアプリの説明を入力し、アプリタイプとして**推薦システム**を選択した後、**[次へ]** をクリックします。

![アプリ作成 - 基本設定](../static/images/quick-start/앱생성화면1.png){ height="70%" }

<a id="app.create.detail"></a>

### 詳細設定 { #app.create.detail }

1. **[モデル追加]** ボタンをクリックして、使用するモデルを追加します。新規サービスの場合は **Cold User**、ユーザーの行動履歴が十分にある場合は **Warm User (Transformer/Graph)** モデルを推奨します。

    ![アプリ作成 - モデル設定](../static/images/quick-start/앱생성화면2.png){ height="70%" }

2. モデルカードの **[データ接続設定]** で、「1. データソースを作成する」で作成したユーザー・アイテム・ヒストリーのデータソースをそれぞれ選択し、
   ユーザーID・アイテムID カラムとヒストリーの時間カラムを指定します。Feature カラムは必要な場合のみ選択します。

    ![アプリ作成 - データ接続設定](../static/images/quick-start/앱생성화면3.png){ height="70%" }

3. 必要に応じて **[追加設定 (Skills)]** でスキルテーブルなどを接続し、基本モデル設定の Longtail モード（人気度の低いアイテムも推薦に含める）を指定します。設定が完了したら **[次へ]** をクリックします。

    ![アプリ作成 - 追加設定](../static/images/quick-start/앱생성화면4.png){ height="70%" }

<a id="app.create.review"></a>

### 最終確認 { #app.create.review }

1. 入力した基本設定、モデル設定、追加設定を確認します。
2. **[保存]** ボタンをクリックすると、アプリが作成されます。

![アプリ作成 - 最終確認](../static/images/quick-start/앱생성화면5.png){ height="70%" }

<a id="app.status"></a>

## 3. アプリの状態を確認する { #app.status }

アプリ作成後、学習とデプロイが自動的に進行します。状態は初期化中、学習中、デプロイ中、有効化中を経てアクティブに変わります。
アプリ一覧でステータスがアクティブになるまで待ちます。

![アプリ一覧](../static/images/quick-start/앱목록.png){ height="70%" }

状態値の詳細については、[コンソール使用ガイド](./console-user-guide/#app.list.status)の「アプリステータス」を参照してください。

<a id="recommendation.query"></a>

## 4. 推薦結果を照会する { #recommendation.query }

アプリがアクティブ状態になると、コンソールの推薦 API 呼び出し画面で推薦結果を確認したり、推薦照会 API を呼び出して推薦結果を照会したりできます。
各項目の詳細については、[コンソール使用ガイド](./console-user-guide/#app.detail.recommend)の「推薦 API 呼び出し」を参照してください。

1. アプリ一覧で作成したアプリをクリックし、詳細画面の **[推薦 API 呼び出し]** タブに移動します。
2. ユーザーID を入力し、推薦モードと最大推薦数を指定します。
3. **[推薦リクエスト]** ボタンをクリックすると、推薦結果に順位、アイテムキー、スコアが表示され、総結果数とレスポンス時間も合わせて確認できます。

    ![推薦 API 呼び出し](../static/images/quick-start/추천API호출.png){ height="70%" }

**[リクエストプレビュー]** には、入力値で構成された実際の API リクエスト JSON が表示されます。**[コピー]** ボタンでコピーして API 連動開発に活用できます。
推薦照会 API を直接呼び出す方法については、[APIガイド](./api-guide/#recommendation.api)の「推薦照会 API」を参照してください。

レスポンスにはリクエスト識別子（`metadata.requestId`）と推薦アイテム一覧（`recommendations[].itemKey`）が含まれます。この値は次のステップの推薦イベント送信に使用されます。

**[アプリ情報]** タブでは、API 呼び出しに使用するアプリ ID、状態、バージョンを確認できます。

![アプリ情報](../static/images/quick-start/앱정보.png){ height="70%" }

<a id="recommendation.event"></a>

## 5. 推薦イベントを収集する（成功率分析） { #recommendation.event }

ユーザーが推薦結果をクリックするなど、反応が発生した場合は推薦イベント API で送信します。積載されたイベントデータで推薦成功率を分析できます。
リクエストフィールドの詳細については、[APIガイド](./api-guide/#recommendation.event.api)の「推薦イベント API」を参照してください。

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

!!! tip "注意"
    イベント API リクエスト後、データセットへの積載まで最大 10 分かかる場合があります。