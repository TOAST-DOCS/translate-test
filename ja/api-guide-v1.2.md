<!-- pre-align:aligned sig=62797d4ab3bf -->

<a id="management-certificate-manager-api-v12-guide"></a>
## Management > Certificate Manager > API v1.2 ガイド { #management-certificate-manager-api-v12-guide }

Certificate Managerでは、証明書の一覧照会、ダウンロードのためのAPIを提供します。クライアントは、コンソールで証明書と証明書ファイルを登録した後、APIを通じてデータを使用できます。

<a id="basic-information"></a>
### 基本情報 { #basic-information }
<a id="basic-information-endpoint"></a>
#### EndPoint
```text
https://certmanager.api.nhncloudservice.com
```

<a id="basic-information-authentication-and-authorization"></a>
#### 認証及び権限

Certificate Manager API v1.2を使用するにはAppkeyが必要です。

Appkeyは、NHN Cloudの各サービスごとに発行される固有の認証キーです。Appkeyの確認及び使用に関する詳細は、[Appkey](/nhncloud/ja/public-api/appkey)を参照してください。

<a id="basic-information-apis-provided"></a>
#### 提供するAPIの種類
| メソッド | URI                                                                     | 説明 |
| ------ |-------------------------------------------------------------------------| --- |
| GET | /certmanager/v1.2/appkeys/{appKey}/certificates | 証明書の一覧を照会します。 |
| GET | /certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files | 登録された証明書ファイルをダウンロードします。 |

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
| resultCode | Number | API呼び出しの結果コード値 |
| resultMessage | String | API呼び出しの結果メッセージ |
| isSuccessful | Boolean | API呼び出しの成否 |

<a id="retrieve-certificate-list"></a>
### 証明書一覧の照会 { #retrieve-certificate-list }

Certificate Managerに登録した証明書の一覧を照会する際に使用します。

<a id="retrieve-certificate-list-request"></a>
#### リクエスト

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| 値 | タイプ | 説明 | 入力可能 |
| --- | --- | --- | --- |
| pageSize | Number | ページサイズ | 10(デフォルト) |
| pageNum | Number | ページ番号 | 1(デフォルト) |
| all | Boolean | 全件照会するかどうか | true, false(デフォルト) |
| status | String | 証明書ステータス | ALL, EXPIRED, UNEXPIRED(デフォルト) |

※ all, statusの値は、大文字と小文字を区別せずに使用できます。

<a id="retrieve-certificate-list-response"></a>
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
                "certificateName": "nhncloudservice.com",
                "authority": "NHN",
                "domains": [
                  "nhncloudservice.com",
                  "*.nhncloudservice.com"
                ],
                "signatureAlgorithm": "SHA256withRSA",
                "fileCreationDate": "2025-03-02",
                "expirationDate": "2026-03-25"
            }
        ]
    }
}
```

| 値 | タイプ | 説明 |
| --- | --- | --- |
| totalCount | Number | 証明書の総数 |
| totalPage | Number | 総ページ数 |
| currentPage | Number | 現在のページ |
| pageSize | Number | ページサイズ |
| certificateName | String | 証明書名 |
| authority | String | 認証局 |
| signatureAlgorithm | String | 署名方式 |
| fileCreationDate | String | 証明書ファイル作成日 |
| expirationDate | String | 証明書ファイル失効日 |

<a id="download-certificate-file"></a>
### 証明書ファイルのダウンロード { #download-certificate-file }

Certificate Managerに登録した証明書ファイルをダウンロードする際に使用します。

<a id="download-certificate-file-request"></a>
#### リクエスト

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files
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

<a id="download-certificate-file-when-using-command-line-interfacecli"></a>
#### Command Line Interface(CLI)を使用する場合

証明書ファイルのダウンロードAPIは、`curl`コマンドを使用してリクエストできます。

```bash
#ファイルに書き込む
curl 'https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#ファイル名を指定
curl -o cert.pem 'https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files'

#アップロードしたファイル名を維持
curl -OJ 'https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files'
```
* その他のcurlコマンドの使用方法は、以下のガイドをご参照ください。
  * curl command guide : [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

<a id="response-code"></a>
### レスポンスコード { #response-code }

| isSuccessful | resultCode | resultMessage | 説明 |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | 成功 |
| false | 52000 | Certificate name does not exist. | リクエストした証明書名が存在しません。 |
| false | 52001 | Certificate file does not exist. | リクエストした証明書ファイルが存在しません。 |
| false | 52002 | There are more than one certificate file. | リクエストした証明書に登録されたファイルが2つ以上あります。 |
| false | 52003 | The certificate file is not a pem file. | リクエストした証明書ファイルはpemファイルではありません。 |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | リクエストした証明書名と、証明書ファイルに登録された名前が異なります。 |
| false | 52005 | Certificate file has expired | リクエストした証明書ファイルは有効期限切れです。 |
| false | 52006 | The certificate has an invalid certificate authority name. | リクエストした証明書ファイルの認証局情報が無効です。 |
| false | 52007 | Requested certificate file should be one. | 同時にアップロードできる証明書ファイルは1つだけです。 |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | アップロード可能な最大ファイルサイズは512KBです。 |
