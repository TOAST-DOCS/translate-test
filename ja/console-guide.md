<!-- machine_translated: true -->

<!-- pre-align:aligned sig=4cffce67e4ac -->

<a id="network-service-gateway-console-user-guide"></a>
## Network > Service Gateway > コンソール使用ガイド { #network-service-gateway-console-user-guide }

コンソールで**Service Gateway**サービスを使用する方法を説明します。

<a id="service-gateway"></a>
## サービスゲートウェイ { #service-gateway }

<a id="create-a-service-gateway"></a>
### サービスゲートウェイの作成 { #create-a-service-gateway }

サービスゲートウェイを作成する方法は次のとおりです。

1. **Network > Service Gateway** に移動します。
2. **[サービスゲートウェイの作成]** ボタンをクリックすると、作成画面が表示されます。
3. サービスゲートウェイに使用する **[名前]** を入力します。
4. **[接続タイプ]** を選択します。サービスゲートウェイに割り当てられた IP でアクセスした際に、選択した対象と接続されます。
    * **[サービスエンドポイント]**: NHN Cloud が提供するサービスに接続します。リストから接続する **[サービス]** を選択します。
    * **[ユーザー定義エンドポイント]**: 他のユーザーが公開したリソース（ロードバランサー）に接続します。エンドポイントの公開者から受け取った **[対象サービス名]** を入力します。サービス名は `{region}.sep-{12桁の16進数}` の形式です（例: `kr1.sep-0a1b2c3d4e5f`）。

    !!! tip "ヒント"
        入力したサービス名は作成時に有効性が検証され、公開者の許可プロジェクトに含まれている場合にのみ接続できます。

5. **[VPC]** を選択します。選択した VPC に紐付いたサービスゲートウェイが作成されます。
6. **[サブネット]** を選択します。選択したサブネットからサービスゲートウェイの IP が割り当てられます。
7. **[プライベートIP]** の割り当て方法を選択します。
    * 自動割り当て: 選択したサブネットの CIDR 範囲内で自動的に割り当てます。
    * 指定: 使用する IP アドレスを手動で入力します。

    !!! tip "ヒント"
        入力する IP アドレスは、選択したサブネットの CIDR 範囲内である必要があります。

8. **[NAT IPの固定]** を行うかどうかを選択します。
    * 通常は選択する必要はなく、選択した **[サービス]** でアクセス制御の設定が必要な場合にのみ選択します。
    * 作成時にのみ選択可能であり、変更はサポートされていません。

    !!! tip "ヒント"
        選択可能なサービスでのみ有効になります。

<a id="view-a-service-gateway"></a>
### サービスゲートウェイの照会 { #view-a-service-gateway }

作成したサービスゲートウェイは、**Network > Service Gateway** 画面で確認できます。サービスゲートウェイを選択すると、下部にサービスゲートウェイの情報が表示されます。接続タイプが**カスタムエンドポイント**の場合、詳細情報の**接続先**でエンドポイントの表示名と識別子を確認できます。

<a id="modify-a-service-gateway"></a>
### サービスゲートウェイの変更 { #modify-a-service-gateway }

サービスゲートウェイを変更する方法は次のとおりです。**名前**、**説明**のみ変更できます。

1. **Network > Service Gateway**に移動します。
2. **サービスゲートウェイ変更**ボタンをクリックし、変更画面で項目を変更します。

<a id="delete-a-service-gateway"></a>
### サービスゲートウェイの削除 { #delete-a-service-gateway }

サービスゲートウェイを削除するには**Network > Service Gateway**画面で削除するサービスゲートウェイを選択し、**サービスゲートウェイ削除**ボタンをクリックします。

<a id="custom-endpoints"></a>
## カスタムエンドポイント { #custom-endpoints }

カスタムエンドポイントは、ユーザーが自分のリソース（ロードバランサー）をエンドポイントとして公開し、他のプロジェクトからサービスゲートウェイで接続できるよう共有する機能です。公開者は共有用の**サービス名**（`service_name`）を発行し、接続を許可する対象に通知して、許可プロジェクトを直接管理します。

<a id="create-a-custom-endpoint"></a>
### カスタムエンドポイントの作成 { #create-a-custom-endpoint }

カスタムエンドポイントを作成する方法は次のとおりです。

1. **Network > Service Gateway** に移動し、**[カスタムエンドポイント]** タブを選択します。
2. **[カスタムエンドポイントの作成]** ボタンをクリックすると、作成画面が表示されます。
3. エンドポイントに使用する **[名前]** を入力します。(255 文字以内、英字・数字・`-`・`_` のみ入力可能)
4. **[表示名]** を入力します。このエンドポイントに接続するサービスゲートウェイに表示される名前です。省略すると、名前と同じ値が適用されます。
5. **[リソースタイプ]** と **[対象リソース]** を選択します。現在、リソースタイプは **Load Balancer** のみサポートしており、対象リソースでエンドポイントとして公開するロードバランサーを選択します。
6. **[最大作成数]** を選択します。このエンドポイントで作成できるサービスゲートウェイの最大数です。
    * 制限なし: 数の制限なく作成できます。1,000 を超える数が必要な場合も、制限なしを選択します。
    * 直接入力: 0〜1,000 の範囲で入力できます。0 を入力すると作成がブロックされます。
7. 必要に応じて **[説明]** を入力し、**[確認]** ボタンをクリックします。
8. 作成が完了すると、共有用の **サービス名**（`{region}.sep-{12桁の16進数}`）が自動的に発行されます。このサービス名を、接続を許可するコンシューマーに共有します。

!!! tip "ヒント"
    カスタムエンドポイントは、プロジェクトあたりデフォルトで最大 5 個まで作成できます。

<a id="view-custom-endpoints"></a>
### カスタムエンドポイントの照会 { #view-custom-endpoints }

**[カスタムエンドポイント]** タブで作成したエンドポイントの一覧を確認できます。エンドポイントを選択すると、下部に詳細情報が表示されます。**[基本情報]**(サービス名、リソースタイプ、対象リソース、最大作成数など)、**[許可プロジェクト]**、**[使用状況]** を確認できます。

<a id="modify-a-custom-endpoint"></a>
### カスタムエンドポイントの変更 { #modify-a-custom-endpoint }

**[名前]**、**[表示名]**、**[最大作成数]**、**[説明]**のみ変更できます。リソースタイプと対象リソースは変更することはできません。

1. **[カスタムエンドポイント]** タブで変更するエンドポイントを選択します。
2. **[変更]** ボタンをクリックし、変更画面で必要な項目を変更します。

!!! tip "ヒント"
    最大作成数を減らしても、すでに作成済みのサービスゲートウェイは維持されます。ただし、現在の数が最大作成数を超えている間は、新しいサービスゲートウェイを追加で作成することはできません。

<a id="delete-a-custom-endpoint"></a>
### カスタムエンドポイントの削除 { #delete-a-custom-endpoint }

**[カスタムエンドポイント]** タブで削除するエンドポイントを選択し、**[削除]** ボタンをクリックします。

!!! danger "注意"
    このエンドポイントを使用中のサービスゲートウェイが1つでも存在する場合は、削除することはできません。エンドポイントを削除すると、登録されている許可プロジェクトも一緒に削除されます。

<a id="reissue-a-service-name"></a>
### サービス名の再発行 { #reissue-a-service-name }

共有したサービス名が外部に漏洩するなど、変更が必要な場合にサービス名を再発行できます。

1. **[ユーザー定義エンドポイント]** タブでエンドポイントを選択した後、**[基本情報]** でサービス名の **[再発行]** ボタンをクリックします。
2. 確認ダイアログで **[再発行]** ボタンをクリックします。

!!! danger "注意"
    再発行すると、既存のサービス名は即座に廃棄され、以降は照会できなくなります。既存のサービス名で作成したサービスゲートウェイは正常に動作しますが、新たにサービスゲートウェイを作成するには、再発行されたサービス名を使用する必要があります。

!!! tip "ヒント"
    サービス名の再発行は、エンドポイントを作成したプロジェクトのメンバー（オーナー）のみが実行できます。

<a id="manage-allowed-projects"></a>
### 許可プロジェクトの管理 { #manage-allowed-projects }

許可プロジェクトは、このエンドポイントへの接続（サービスゲートウェイの作成）を許可する対象を管理するリストです。

1. エンドポイントを選択し、詳細情報の **[許可プロジェクト]** タブに移動します。
2. **[追加]** ボタンをクリックし、**[許可範囲]** を選択します。
    * **[全プロジェクト (*)]**: すべてのプロジェクトからの接続を許可します。
    * **[特定プロジェクト]**: 許可するプロジェクトの **[テナントID]**（32桁の16進数）を入力します。
3. 必要に応じて **[説明]** を入力し、**[確認]** ボタンをクリックします。

!!! tip "ヒント"
    全体許可（*）と特定プロジェクトを同時に登録した場合、より狭い範囲（特定プロジェクト）が適用されます。これを利用すると、無停止で許可範囲を切り替えることができます。たとえば、全体許可（*）の状態で特定プロジェクトを追加した後、全体許可（*）を削除すると、接続を中断することなく特定プロジェクトのみを許可する設定に切り替えられます。

既存の許可対象は **[説明]** のみ変更できます。許可範囲とテナントIDは変更できません。許可対象を削除するには、リストから対象を選択し、**[削除]** ボタンをクリックします。

<a id="check-usage-status"></a>
### 使用状況の確認 { #check-usage-status }

エンドポイントの詳細情報にある **[使用状況]** タブで、このエンドポイントに接続中のサービスゲートウェイの一覧を確認できます。(読み取り専用)

<a id="use-a-service-gateway"></a>
## サービスゲートウェイの使用 { #use-a-service-gateway }

<a id="check-the-service-gateway-ip"></a>
### サービスゲートウェイIPの確認 { #check-the-service-gateway-ip }

1. **Network > Service Gateway**に移動します。
2. サービスゲートウェイリストで**IPアドレス**を確認します。<br>
  このVM InstanceからこのIPアドレスに接続すると、サービスゲートウェイが接続しているサービスに接続されます。

<a id="connect-to-the-service-gateway"></a>
### サービスゲートウェイ接続 { #connect-to-the-service-gateway }

作成されたサービスゲートウェイのIPアドレスが`192.168.1.42`である場合、次のような方法でサービスにアクセスできます。

* VM InstanceからサービスゲートウェイIPに接続すると、サービスゲートウェイ作成時に選択されたサービスに接続され、サービスを使用できます。
    * IPアドレスを使用してhttpsプロトコルを利用する場合、証明書関連エラーが発生する可能性があります。
    * httpsの使用が必要な場合はVM Instanceの`/etc/hosts`にIPアドレスとURLを追加してください。
    * 例) IPアドレスを利用してオブジェクトストレージからファイルをダウンロード

            ~# wget http://192.168.1.42/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

* サービスゲートウェイを利用してサービスにアクセスするとき、URLをサポートしません。URLアクセスが必要な場合は以下の例のように`/etc/hosts`ファイルにURLを追加する必要があります。
    * 例) URLを利用して**オブジェクトストレージ**からファイルをダウンロード<br>
      `/etc/hosts`ファイルに以下のようにサービスゲートウェイのIPアドレスとObject StorageのURLを追加します。

            192.168.1.42    kr1-api-object-storage.nhncloudservice.com

        IPアドレスの代わりに`/etc/hosts`に追加したURLで接続

            ~# wget https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

<a id="example-of-using-object-storage-from-a-service-gateway"></a>
## サービスゲートウェイでオブジェクトストレージを使用する例 { #example-of-using-object-storage-from-a-service-gateway }

**オブジェクトストレージ**に関連する内容は、例を説明するための水準でのみ記述します。オブジェクトストレージの詳細については**ユーザーガイド > Storage > Oject Storage**を参照してください。

<a id="example-of-using-object-storage-from-a-service-gateway-create-a-service-gateway"></a>
### サービスゲートウェイの作成 { #example-of-using-object-storage-from-a-service-gateway-create-a-service-gateway }

**オブジェクトストレージAPI**を使用するには**認証トークン**を発行する必要があります。インターネットを使用できない隔離された環境のVPCからObject Storageを使用するには認証トークンもサービスゲートウェイを利用して発行する必要があり、次の手順に従ってサービスゲートウェイを作成する必要があります。

1. **Object Storage**サービスを選択してサービスゲートウェイを作成します。<br>
 オブジェクトストレージAPI接続用のサービスゲートウェイです。
2. **IaaS API Identity**サービスを選択してサービスゲートウェイを作成します。<br>
 認証トークン(token)を発行するためのサービスゲートウェイです。
3. 作成された2つのサービスゲートウェイでIPアドレスを確認します。

<a id="edit-the-etchosts-file"></a>
### /etc/hosts ファイルの編集 { #edit-the-etchosts-file }

**[Object Storage]** を選択して作成したサービスゲートウェイの IP アドレスが 192.168.1.42 で、**[IaaS API Identity]** を選択して作成したサービスゲートウェイの IP アドレスとして 192.168.1.57 が割り当てられている場合、VM Instance の `/etc/hosts` ファイルに次のように IP アドレスと URL を追加します。

!!! tip "ヒント"
    オブジェクトストレージの API URL アドレスは、コンソール画面の **Storage > Object Storage** で **[API エンドポイント設定]** ボタンをクリックして確認できます。

!!! danger "注意"
    リージョンごとに使用するオブジェクトストレージ API の URL アドレスが異なるため、**[API エンドポイント設定]** の URL を必ず確認してください。

```
192.168.1.42	api-identity-infrastructure.nhncloudservice.com
192.168.1.57	kr1-api-object-storage.nhncloudservice.com
```

<a id="obtain-the-authentication-token"></a>
### 認証トークンの発行 { #obtain-the-authentication-token }

オブジェクトストレージの **API パスワードの設定**を行い、認証トークンを発行します。

* API パスワードの設定
    1. **Storage > Object Storage** で **[API エンドポイントの設定]** ボタンをクリックします。
    2. **[API エンドポイントの設定]** 画面の **[API パスワードの設定]** に使用するパスワードを入力し、**[変更]** ボタンをクリックします。

    !!! tip "ヒント"
        詳細な使用方法については、[ユーザーガイド > Storage > Object Storage > API ガイド](https://docs.nhncloud.com/ko/Storage/Object%20Storage/ko/api-guide/)を参照してください。

* 認証トークン発行リクエスト<br>
  **NHN Cloud ログイン ID** と前述の **API パスワードの設定**で設定したパスワードを使用して、以下のように **IaaS API Identify** サービス用に作成したサービスゲートウェイ URL にトークン発行をリクエストします。
    * `auth.passwordCredentials.username` には NHN Cloud ログイン ID を使用します。
    * `auth.passwordCredentials.password` には API パスワードの設定で入力したパスワードを使用します。
  

            ~# curl -X POST -H 'Content-Type:application/json' https://api-identity-infrastructure.nhncloudservice.com/v2.0/tokens -d '{"auth": {"tenantId": "2fda9d4b88244a0a92ff23841198e2e6", "passwordCredentials": {"username": "example@nhn.com", "password": "example123"}}}'

* 認証トークン発行レスポンス<br>
  以下のレスポンスの `access.token.id` 項目の値が認証トークンです。`access.token.expires` に記録された日時まで認証トークンが有効です。

            {"access":{"token":{"id":"gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY","expires":"2022-04-13T19:19:30Z","tenant":{"id":"2fda9d4b8821111192ff23841198e2e6","name":"tTMgSSSF","groupId":"XXj2zkH7777modGU","description":"","enabled":true,"project_domain":"NORMAL","swift":true},"issued_at":"2022-04-13T07:32:14.000441"},"serviceCatalog":[{"endpoints":[{"region":"KR1","publicURL":"https://api-identity.infrastructure.cloud.toast.com/v2.0"}],"type":"identity","name":"keystone"},{"endpoints":[{"region":"KR2","publicURL":"https://kr2-api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"},{"region":"KR1","publicURL":"https://api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"}],"type":"object-store","name":"swift"}],"user":{"id":"80884888887b45dbaf9b815117130671","username":"5111111c-b111-4b11-b11b-01111f81111f","name":"5211122c-bfc4-4115-b11b-05b52f84

<a id="use-the-object-storage-api"></a>
### オブジェクトストレージAPIの使用 { #use-the-object-storage-api }

認証トークンの発行が完了したらオブジェクトストレージAPIを使用できます。オブジェクトストレージにexampleというコンテナを作成し、test_file.txtを入れたと仮定した場合、以下のようなAPI使用方法でコンテナにあるファイルを照会できます。

* リクエスト<br>
  `X-Auth-Token`に認証トークンを追加してリクエスト

        ~# curl -X GET -H 'X-Auth-Token:gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY' https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6/example

* レスポンス<br>
 オブジェクトストレージコンテナにあるファイルリストを確認

        test_file.txt
