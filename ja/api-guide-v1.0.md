<!-- pre-align:aligned sig=8eda339a3204 -->

<a id="api-v10-guide"></a>
## API v1.0ガイド { #api-v10-guide }
**Management > Certificate Manager > API v1.0ガイド**

Certificate Manager は、証明書リスト検索、またはダウンロード用の API を提供します。クライアントはコンソールで証明書と証明書ファイルを登録した後、APIを通してデータを使用できます。

<a id="certificate-manager-api-common-information"></a>
## Certificate Manager API共通情報 { #certificate-manager-api-common-information }

<a id="api-endpoint"></a>
### APIエンドポイント { #api-endpoint }
```text
https://certmanager.api.nhncloudservice.com
```

<a id="authentication-and-authorization"></a>
### 認証および権限 { #authentication-and-authorization }

Certificate Manager API v1.0を使用するにはAppkeyが必要です。

Appkeyは、NHN Cloudの各サービスごとに発行される固有の認証キーです。Appkeyの確認及び使用に関する詳細は、[Appkey](/nhncloud/ja/public-api/appkey)を参照してください。

<a id="available-api-types"></a>
### 提供するAPI種類 { #available-api-types }
| メソッド | URI | 説明 |
| ------ | --- | --- |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates | 証明書のリストを検索します。 |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | 登録された証明書ファイルをダウンロードします。 |

<a id="available-api-types-path-variables-of-api-request"></a>
#### APIリクエストのパス変数

| 値 | タイプ | 説明 |
| --- | --- | --- |
| appKey | String | 使用するデータを保存しているNHN Cloudプロジェクトのアプリキー |
| certificateName | String | 使用するデータ(証明書)の名前 |

<a id="available-api-types-common-data-header-of-api-response"></a>
#### APIレスポンスのデータ共通ヘッダ

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

<a id="certificate-api"></a>
## 証明書API { #certificate-api }

<a id="lookup-certificate-list"></a>
### 証明書の検索リスト { #lookup-certificate-list }

Certificate Manager に登録されている証明書のリストを照会するために使用されます。

<a id="lookup-certificate-list-request"></a>
#### リクエスト

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| 値 | タイプ | 説明 | 入力可能 |
| --- | --- | --- | --- |
| pageSize | Number | ページサイズ | 10(default) |
| pageNum | Number | ページ番号 | 1(default) |
| all | Boolean | 完全検索 | true, false(default) |
| status | String | 証明書の有効期限ステータス | ALL, EXPIRED, UNEXPIRED(default) |

※ all、statusの値は大文字/小文字を区別せずに使用できます。

<a id="lookup-certificate-list-response"></a>
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
| certificateName | String | 名証明書 |
| authority | String | 権限 |
| signatureAlgorithm | String | シグニチャ アルゴリズム |
| fileCreationDate | String | 証明書ファイルの作成日 |
| expirationDate | String | 証明書ファイルの有効期限 |

<a id="downloading-certificate-files"></a>
### 証明書ファイルのダウンロード { #downloading-certificate-files }

Certificate Managerに登録した証明書ファイルをダウンロードする時に使用します。

<a id="downloading-certificate-files-request"></a>
#### リクエスト

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
```

<a id="downloading-certificate-files-success-response"></a>
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

<a id="downloading-certificate-files-failure-response"></a>
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

<a id="downloading-certificate-files-for-command-line-interface-cli"></a>
#### Command Line Interface(CLI)使用時

証明書ファイルダウンロードAPIは`curl`コマンドを使用してリクエストできます。

```bash
#ファイルに書き込む
curl 'https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#ファイル名指定
curl -o cert.pem 'https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'

#アップロードしたファイル名を維持
curl -OJ 'https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'
```
* その他curlコマンドの使用方法は下記のガイドを参照してください。
  * curl command guide : [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

<a id="response-codes"></a>
## レスポンスコード { #response-codes }

| isSuccessful | resultCode | resultMessage | 説明 |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | 成功 |
| false | 52000 | Certificate name does not exist. | リクエストした証明書名が存在しません。 |
| false | 52001 | Certificate file does not exist. | リクエストした証明書ファイルが存在しません。 |
| false | 52002 | There are more than one certificate file. | リクエストした証明書に登録されたファイルが2つ以上あります。 |
| false | 52003 | The certificate file is not a pem file. | リクエストした証明書ファイルがpemファイルではありません。 |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | リクエストした証明書名と証明書ファイルに登録された名前が異なります。 |
| false | 52005 | Certificate file has expired | リクエストした証明書ファイルの有効期限が切れています。 |
| false | 52006 | The certificate has an invalid certificate authority name. | 要求された証明書ファイルの認証局情報が無効です。 |
| false | 52007 | Requested certificate file should be one. | 同時にアップロードできる証明書ファイルは1つだけです。 |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | アップロードできる最大ファイルサイズは512KBです。 |
