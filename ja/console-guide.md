## Network > Service Gateway > コンソール使用ガイド

コンソールで**Service Gateway**サービスを使用する方法を説明します。

## サービスゲートウェイ

### サービスゲートウェイの作成

サービスゲートウェイを作成する方法は次のとおりです。

1. **Network > Service Gateway**に移動します。
2. **サービスゲートウェイ作成**ボタンをクリックすると作成画面が表示されます。
3. サービスゲートウェイに使用する**名前**を入力します。
4. **VPC**を選択します。選択されたVPCに依存するサービスゲートウェイが作成されます。
5. **サブネット**を選択します。選択されたサブネットでサービスゲートウェイのIPが割り当てられます。
6. **プライベートIP**の割り当て方法を選択します。
    * 自動割り当て：選択したサブネットのCIDR範囲内で自動的に割り当てます。
    * 指定:使用するIPアドレスを手動で入力します。
    > [参考]入力するIPアドレスは選択したサブネットのCIDR範囲内にある必要があります。
7. **サービス**を選択します。サービスゲートウェイに割り当てられたIPでアクセスすると、選択したサービスと接続されます。

### サービスゲートウェイの照会

作成したサービスゲートウェイは**Network > Service Gateway**画面で確認できます。サービスゲートウェイを選択すると、下部にサービスゲートウェイ情報が表示されます。

### サービスゲートウェイの変更

サービスゲートウェイを変更する方法は次のとおりです。**名前**、**説明**のみ変更できます。

1. **Network > Service Gateway**に移動します。
2. **サービスゲートウェイ変更**ボタンをクリックし、変更画面で項目を変更します。

### サービスゲートウェイの削除

サービスゲートウェイを削除するには**Network > Service Gateway**画面で削除するサービスゲートウェイを選択し、**サービスゲートウェイ削除**ボタンをクリックします。

## サービスゲートウェイの使用

### サービスゲートウェイIPの確認

1. **Network > Service Gateway**に移動します。
2. サービスゲートウェイリストで**IPアドレス**を確認します。<br>
  このVM InstanceからこのIPアドレスに接続すると、サービスゲートウェイが接続しているサービスに接続されます。

### サービスゲートウェイ接続

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

## サービスゲートウェイでオブジェクトストレージを使用する例

**オブジェクトストレージ**に関連する内容は、例を説明するための水準でのみ記述します。オブジェクトストレージの詳細については**ユーザーガイド > Storage > Oject Storage**を参照してください。

### サービスゲートウェイの作成

**オブジェクトストレージAPI**を使用するには**認証トークン**を発行する必要があります。インターネットを使用できない隔離された環境のVPCからObject Storageを使用するには認証トークンもサービスゲートウェイを利用して発行する必要があり、次の手順に従ってサービスゲートウェイを作成する必要があります。

1. **Object Storage**サービスを選択してサービスゲートウェイを作成します。<br>
 オブジェクトストレージAPI接続用のサービスゲートウェイです。
2. **IaaS API Identity**サービスを選択してサービスゲートウェイを作成します。<br>
 認証トークン(token)を発行するためのサービスゲートウェイです。
3. 作成された2つのサービスゲートウェイでIPアドレスを確認します。

### /etc/hostsファイルの編集

**Object Storage**を選択して作成したサービスゲートウェイのIPアドレスが192.168.1.42で、**IaaS API Identity**を選択して作成したサービスゲートウェイのIPアドレスに192.168.1.57が割り当てられた場合、VM Instanceの`/etc/hosts`ファイルに以下のようにIPアドレスとURLを追加します。

> [参考]オブジェクトストレージのAPI URLアドレスはコンソール画面の**Storage > Object Storage**で**APIエンドポイント設定**ボタンをクリックして確認できます。<br>
> [注意]リージョンごとに使用するオブジェクトストレージAPIのURLアドレスは異なるため、**APIエンドポイント設定**のURLを必ずご確認ください。

```
192.168.1.42	api-identity-infrastructure.nhncloudservice.com
192.168.1.57	kr1-api-object-storage.nhncloudservice.com
```

### 認証トークンの発行

オブジェクトストレージの**APIパスワード設定**を行い、認証トークンを発行します。

* APIパスワード設定
    1. **Storage > Object Storage**で**APIエンドポイント設定**ボタンをクリックします。
    2. **APIエンドポイント設定**画面の**APIパスワード設定**に使用するパスワードを入力し、**変更**ボタンをクリックします。
    > [参考]詳細な使い方は[ユーザーガイド > Storage > Object Storage > APIガイド](https://docs.nhncloud.com/ja/Storage/Object%20Storage/ja/api-guide/)を参照してください。
* 認証トークン発行リクエスト<br>
  **NHN CloudログインID**と、設定した**APIパスワード設定**のパスワードを利用して**IaaS API Identity**サービス用に作成したサービスゲートウェイURLにトークン発行をリクエストします。
    * `auth.passwordCredentials.username`にはNHN CloudログインIDを使用
    * `auth.passwordCredentials.password`にはAPIパスワード設定に入力したパスワードを使用

            ~# curl -X POST -H 'Content-Type:application/json' https://api-identity-infrastructure.nhncloudservice.com/v2.0/tokens -d '{"auth": {"tenantId": "2fda9d4b88244a0a92ff23841198e2e6", "passwordCredentials": {"username": "example@nhn.com", "password": "example123"}}}'

* 認証トークン発行レスポンス<br>
 以下のレスポンスで`access.token.id`項目の値が認証トークンです。`access.token.expires`に記録された時間まで認証トークンが有効です。

            {"access":{"token":{"id":"gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY","expires":"2022-04-13T19:19:30Z","tenant":{"id":"2fda9d4b8821111192ff23841198e2e6","name":"tTMgSSSF","groupId":"XXj2zkH7777modGU","description":"","enabled":true,"project_domain":"NORMAL","swift":true},"issued_at":"2022-04-13T07:32:14.000441"},"serviceCatalog":[{"endpoints":[{"region":"KR1","publicURL":"https://api-identity.infrastructure.cloud.toast.com/v2.0"}],"type":"identity","name":"keystone"},{"endpoints":[{"region":"KR2","publicURL":"https://kr2-api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"},{"region":"KR1","publicURL":"https://api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"}],"type":"object-store","name":"swift"}],"user":{"id":"80884888887b45dbaf9b815117130671","username":"5111111c-b111-4b11-b11b-01111f81111f","name":"5211122c-bfc4-4115-b11b-05b52f84

### オブジェクトストレージAPIの使用

認証トークンの発行が完了したらオブジェクトストレージAPIを使用できます。オブジェクトストレージにexampleというコンテナを作成し、test_file.txtを入れたと仮定した場合、以下のようなAPI使用方法でコンテナにあるファイルを照会できます。

* リクエスト<br>
  `X-Auth-Token`に認証トークンを追加してリクエスト

        ~# curl -X GET -H 'X-Auth-Token:gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY' https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6/example

* レスポンス<br>
 オブジェクトストレージコンテナにあるファイルリストを確認

        test_file.txt
