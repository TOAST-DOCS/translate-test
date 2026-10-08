<!-- pre-align:aligned sig=2c9270a88b89 -->

<a id="management-certificate-manager-api-v11-guide"></a>
## Management > Certificate Manager > API v1.1ガイド { #management-certificate-manager-api-v11-guide }

Certificate Managerは、証明書一覧の照会とダウンロードAPIを提供します。クライアントはコンソールで証明書と証明書ファイルを登録した後、APIでデータを使用できます。

<a id="common-certificate-manager-api-information"></a>
### Certificate Manager API共通情報 { #common-certificate-manager-api-information }
<a id="common-certificate-manager-api-information-api-endpoint"></a>
#### APIエンドポイント
```text
https://certmanager.api.nhncloudservice.com
```

<a id="common-certificate-manager-api-information-authentication-and-authorization"></a>
#### 認証及び権限
Certificate Managerは、API呼び出し時の認証/認可のためにUser Access Key認証を使用します。
User Access Keyは、NHN CloudアカウントまたはIAMアカウントをベースに発行される認証キーであり、Secret Access Keyと一緒に使用するAPIリクエストに対する認証手段です。
User Access Keyの使用に関する詳細は、[User Access Key認証](/nhncloud/ja/public-api/user-access-key)を参考にしてください。

Certificate Manager APIは、ロールベースのアクセス制御(RBAC)を使用します。<br>
ユーザーはAPIを使用するために、**Certificate Manager ADMINロール**または**Certificate Manager VIEWERロール**を所有している必要があります。

<a id="common-certificate-manager-api-information-supported-api-types"></a>
#### 提供するAPIの種類
| メソッド | URI                                                                     | 説明 |
| ------ |-------------------------------------------------------------------------| --- |
| GET | /certmanager/v1.1/appkeys/{appKey}/certificates                         | 証明書一覧を照会します。 |
| GET | /certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files | 登録された証明書ファイルをダウンロードします。 |

##### APIリクエストのパス変数

| 値 | タイプ | 説明 |
| --- | --- | --- |
| appKey | String | 使用するデータを保存しているNHN Cloudプロジェクトのアプリキー |
| certificateName | String | 使用するデータ(証明書)の名前 |

##### APIレスポンスのデータ共通ヘッダ

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": {

    }
}
```

| 値 | タイプ | 説明 |
| --- | --- | --- |
| resultCode | Number | API呼び出し結果コード値 |
| resultMessage | String | API呼び出し結果メッセージ |
| isSuccessful | Boolean | API呼び出し成否 |

<a id="list-certificates"></a>
### 証明書リスト照会 { #list-certificates }

Certificate Managerに登録されている証明書のリストを照会するために使用されます。

<a id="list-certificates-request"></a>
#### リクエスト

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| 値 | タイプ | 説明 | 入力可能 |
| --- | --- | --- | --- |
| pageSize | Number | ページサイズ | 10(default) |
| pageNum | Number | ページ番号 | 1(default) |
| all | Boolean | 全体検索 | true, false(default) |
| status | String | 証明書の有効期限ステータス | ALL, EXPIRED, UNEXPIRED(default) |

※ all、statusの値は大文字/小文字を区別せずに使用できます。

<a id="list-certificates-response"></a>
#### レスポンス

[Response Header]

```
Content-Type:application/json
```

[Response Body]

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": {
        "totalCount": 1,
        "totalPage": 1,
        "currentPage": 1,
        "pageSize": 10,
        "data": [
            {
                "certificateName": "test.nhn.com",
                "authority": "NHN",
                "signatureAlgorithm": "SHA256withRSA",
                "fileCreationDate": "2020-03-02",
                "expirationDate": "2021-03-25"
            }
        ]
    }
}
```

| 値 | タイプ | 説明 |
| --- | --- | --- |
| totalCount | Number | 証明書の合計数 |
| totalPage | Number | 合計ページ数 |
| currentPage | Number | 現在のページ |
| pageSize | Number | ページサイズ |
| certificateName | String | 証明書名 |
| authority | String | 認証機関 |
| signatureAlgorithm | String | シグニチャ アルゴリズム |
| fileCreationDate | String | 証明書ファイルの作成日 |
| expirationDate | String | 証明書ファイルの有効期限 |

<a id="download-certificate-file"></a>
### 証明書ファイルのダウンロード { #download-certificate-file }

Certificate Managerに登録した証明書ファイルをダウンロードする時に使用します。

<a id="download-certificate-file-request"></a>
#### リクエスト

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files
```

<a id="download-certificate-file-success-response"></a>
#### 成功レスポンス

[Response Header]

```
Content-Disposition:attachment; filename="{ファイル名}"
Content-Type:application/octet-stream
```

[Response Body]

```
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
...
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

<a id="download-certificate-file-failure-response"></a>
#### 失敗レスポンス
[Response Header]
```
Content-Type:application/json
```
[Response Body]

```
{
    "header": {
        "resultCode": 52000,
        "resultMessage": "Certificate name does not exist.",
        "isSuccessful": false
    },
    "body": {}
}
```

<a id="download-certificate-file-for-command-line-interface-cli"></a>
#### Command Line Interface(CLI)使用時

証明書ファイルダウンロードAPIは`curl`コマンドを使用してリクエストできます。

```bash
#ファイルに書き込む
curl -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
    -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}' \
    'https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#ファイル名指定
curl -o cert.pem \
    -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
    -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}' \
    'https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files'

#アップロードしたファイル名を維持
curl -OJ \
    -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
    -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}' \
    'https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files'
```
* その他curlコマンドの使用方法は下記のガイドを参照してください。
  * curl command guide : [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

<a id="response-codes"></a>
### レスポンスコード { #response-codes }

| isSuccessful | resultCode | resultMessage | 説明 |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | 成功 |
| false | 52000 | Certificate name does not exist. | リクエストした証明書名がありません。 |
| false | 52001 | Certificate file does not exist. | リクエストした証明書ファイルがありません。 |
| false | 52002 | There are more than one certificate file. | リクエストした証明書に登録されたファイルが2つ以上あります。 |
| false | 52003 | The certificate file is not a pem file. | リクエストした証明書ファイルがpemファイルではありません。 |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | リクエストした証明書名と証明書ファイルに登録された名前が異なります。 |
| false | 52005 | Certificate file has expired | リクエストした証明書ファイルは期限切れになっています。 |
| false | 52006 | The certificate has an invalid certificate authority name. | 要求された証明書ファイルの認証局情報が無効です。 |
| false | 52007 | Requested certificate file should be one. | 同時にアップロードできる証明書ファイルは1つだけです。 |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | アップロードできる最大ファイルサイズは512KBです。 |
