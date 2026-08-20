<!-- pre-align:aligned sig=1830bd25c1cb -->

<a id="management-certificate-manager-api-v13-guide"></a>
## Management > Certificate Manager > API v1.3 ガイド { #management-certificate-manager-api-v13-guide }

Certificate Managerでは、証明書の一覧照会、ダウンロードのためのAPIを提供します。クライアントはコンソールで証明書と証明書ファイルを登録した後、APIを通じてデータを使用できます。

<a id="certificatemanager-api-common-information"></a>
### CertificateManager API共通情報 { #certificatemanager-api-common-information }
<a id="certificatemanager-api-common-information-api-endpoint"></a>
#### APIエンドポイント
```text
https://certmanager.api.nhncloudservice.com
```
<a id="certificatemanager-api-common-information-authentication-and-authorization"></a>
#### 認証及び権限
CertificateManagerはAPI呼び出し時、認証/認可のためにUser Access Keyトークンを使用します。
User Access Keyトークンは、User Access Keyに基づいて発行されるBearerタイプの一時的なアクセストークンです。
User Access Keyトークンの発行及び使用に関する詳細は、[User Access Keyトークン](/nhncloud/ja/public-api/user-access-key-token)を参照してください。

CertificateManager APIは、ロールベースアクセス制御(RBAC)を使用しています。<br>
ユーザーはAPIを使用するために、**CertificateManager ADMINロール**または**CertificateManager VIEWERロール**を所有している必要があります。

<a id="certificatemanager-api-common-information-provided-apis"></a>
#### 提供するAPIの種類
| メソッド | URI                                                                     | 説明 |
| ------ |-------------------------------------------------------------------------| --- |
| GET | /certmanager/v1.3/appkeys/{appKey}/certificates | 証明書一覧を照会します。 |
| GET | /certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files | 登録された証明書ファイルを証明書名でダウンロードします。 |
| GET | /certmanager/v1.3/appkeys/{appKey}/certificates/{certificateId}/certificate-files | 登録された証明書ファイルを証明書IDでダウンロードします。 |

##### APIリクエストのパス変数

| 値 | タイプ | 説明 |
| --- | --- | --- |
| appKey | String | 使用するデータを保存しているNHN CloudプロジェクトのAppkey |
| certificateName | String | 使用するデータ(証明書)の名前 |
| certificateId | Number | 使用するデータ(証明書)のID |

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

<a id="retrieve-a-certificate-list"></a>
### 証明書一覧照会 { #retrieve-a-certificate-list }

Certificate Managerに登録した証明書一覧を照会する際に使用します。

<a id="retrieve-a-certificate-list-request"></a>
#### リクエスト

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| 値 | タイプ | 説明 | 入力可能値 |
| --- | --- | --- | --- |
| pageSize | Number | ページサイズ | 10(デフォルト値) |
| pageNum | Number | ページ番号 | 1(デフォルト値) |
| all | Boolean | 全体照会の有無 | true、false(デフォルト値) |
| status | String | 証明書の状態 | ALL、EXPIRED、UNEXPIRED(デフォルト値) |

※ all、statusの値は大文字・小文字を区別せずに使用できます。

<a id="retrieve-a-certificate-list-response"></a>
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
                "certificateId": 1,
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
| totalCount | Number | 総証明書数 |
| totalPage | Number | 総ページ数 |
| currentPage | Number | 現在のページ |
| pageSize | Number | ページサイズ |
| certificateId | Number | 証明書ID |
| certificateName | String | 証明書名 |
| authority | String | 認証局 |
| signatureAlgorithm | String | 署名アルゴリズム |
| fileCreationDate | String | 証明書ファイル作成日 |
| expirationDate | String | 証明書ファイル有効期限 |

<a id="download-a-certificate-file-certificate-name"></a>
### 証明書ファイルのダウンロード(証明書名) { #download-a-certificate-file-certificate-name }

Certificate Managerに登録した証明書ファイルを証明書名でダウンロードする際に使用します。

<a id="download-a-certificate-file-certificate-name-request"></a>
#### リクエスト

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files
```

<a id="download-a-certificate-file-certificate-name-success-response"></a>
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

<a id="download-a-certificate-file-certificate-name-failure-response"></a>
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

<a id="download-a-certificate-file-certificate-name-using-the-command-line-interface-cli"></a>
#### Command Line Interface(CLI)使用時

証明書ファイルダウンロードAPIは、curlコマンドを使用してリクエストできます。

```bash
#ファイルに書き込み
curl 'https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files' \
    -H "X-NHN-AUTHORIZATION: Bearer {発行されたトークン}" > cert.pem

#ファイル名指定
curl -o cert.pem 'https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files' \
    -H "X-NHN-AUTHORIZATION: Bearer {発行されたトークン}"

#アップロードしたファイル名を維持
curl -OJ 'https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files' \
    -H "X-NHN-AUTHORIZATION: Bearer {発行されたトークン}"
```
* その他のcurlコマンドの使用方法は、以下のガイドを参照してください。
  * curl command guide: [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

<a id="download-a-certificate-file-certificate-id"></a>
### 証明書ファイルのダウンロード(証明書ID) { #download-a-certificate-file-certificate-id }

Certificate Managerに登録した証明書ファイルを証明書IDでダウンロードする際に使用します。
証明書IDは、証明書一覧照会APIレスポンスのcertificateId値です。

<a id="download-a-certificate-file-certificate-id-request"></a>
#### リクエスト

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateId}/certificate-files
```

<a id="download-a-certificate-file-certificate-id-success-response"></a>
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

<a id="download-a-certificate-file-certificate-id-failure-response"></a>
#### 失敗レスポンス
[Response Header]
```
Content-Type:application/json
```
[Response Body]

```
{
    "header": {
        "resultCode": 52009,
        "resultMessage": "Certificate id does not exist.",
        "isSuccessful": false
    },
    "body": {}
}
```

※失敗レスポンスは、HTTPステータスコード404(Not Found)と共に返されます。

<a id="response-code"></a>
### レスポンスコード { #response-code }

| isSuccessful | resultCode | resultMessage | 説明 |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | 成功 |
| false | 52000 | Certificate name does not exist. | リクエストした証明書名が存在しません。 |
| false | 52001 | Certificate file does not exist. | リクエストした証明書ファイルが存在しません。 |
| false | 52002 | There are more than one certificate file. | リクエストした証明書に登録されたファイルが2つ以上あります。 |
| false | 52003 | The certificate file is not a pem file. | リクエストした証明書ファイルがPEM形式のファイルではありません。 |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | リクエストした証明書名と証明書ファイルに登録された名前が異なります。 |
| false | 52005 | Certificate file has expired | リクエストした証明書ファイルは有効期限が切れています。 |
| false | 52006 | The certificate has an invalid certificate authority name. | リクエストした証明書ファイルの認証局情報が有効ではありません。 |
| false | 52007 | Requested certificate file should be one. | 同時に1つの証明書ファイルのみアップロード可能です。 |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | アップロード可能な最大ファイルサイズは512KBです。 |
| false | 52009 | Certificate id does not exist. | リクエストした証明書IDが存在しません。 |
