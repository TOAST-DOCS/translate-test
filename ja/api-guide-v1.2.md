<!-- machine_translated: true -->

<!-- pre-align:aligned sig=aa5c9758414b -->

<a id="security-secure-key-manager-api-v12-guide"></a>
## Security > Secure Key Manager > API v1.2ガイド { #security-secure-key-manager-api-v12-guide }

Secure Key Managerは、ユーザーデータにアクセスできる多様なAPIを提供します。クライアントは鍵の保存場所に設定した認証をパスした後に、Secure Key Managerに保存したデータを使用できます。

<a id="secure-key-manager-api-common-information"></a>
## Secure Key Manager API共通情報 { #secure-key-manager-api-common-information }

<a id="api-endpoint"></a>
### APIエンドポイント { #api-endpoint }

| リージョン | エンドポイント |
|---|---|
| Global | https://api-keymanager.nhncloudservice.com |

<a id="authentication-and-authorization"></a>
### 認証および権限 { #authentication-and-authorization }

Secure Key Manager API v1.2は、API呼び出し時の認証方法として、Appkey、プロジェクト統合Appkey、User Access Keyをサポートしています。

Appkeyは、API呼び出し時にリクエストURLに含めて特定のリソースを指定・識別するために使用します。Appkeyの代わりにプロジェクト統合Appkeyを使用することも可能です。
User Access Keyは、NHN CloudアカウントまたはIAMアカウントに紐づいて発行される認証キーであり、Secret Access Keyと併用してAPIリクエストの認証手段として活用されます。

各認証方法の確認手順や使用方法の詳細は、それぞれ[Appkey](/nhncloud/ja/public-api/appkey)、[プロジェクト統合Appkey](/nhncloud/ja/public-api/project-integrated-appkey)、[User Access Key](/nhncloud/ja/public-api/user-access-key)をご参照ください。

<a id="list-of-apis"></a>
### APIリスト { #list-of-apis }

| Method | URI | 説明 |
|---|---|---|
| GET | /keymanager/v1.2/appkey/{appkey}/confirm | APIを呼び出したクライアント情報を提供します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/secrets/{keyid} | Secure Key Managerに保存した機密データを照会します。 |
| PUT | /keymanager/v1.2/appkey/{appkey}/secrets/{keyid} | Secure Key Managerに保存した機密データを修正します。 |
| POST | /keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/encrypt | Secure Key Managerに保存した対称鍵でデータを暗号化します。 |
| POST | /keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/decrypt | Secure Key Managerに保存した対称鍵でデータを復号します。 |
| POST | /keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key | クライアントがローカル環境でデータの暗号化/復号に使用できるAES-256対称鍵を作成します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key | Secure Key Managerに保存した対称鍵を照会します。 |
| POST | /keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/sign | Secure Key Managerに保存した非対称鍵でデータを署名します。 |
| POST | /keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/verify | Secure Key Managerに保存した非対称鍵でデータと署名を検証します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey | Secure Key Managerに保存した秘密鍵を照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey | Secure Key Managerに保存した公開鍵を照会します。 |
| POST | /keymanager/v1.0/appkey/{appkey}/keys/{secrets\|symmetric-keys\|asymmetric-keys}/create | Secure Key Managerに新規キーを追加します。 |
| PUT | /keymanager/v1.0/appkey/{appkey}/keys/{keyid}/delete | Secure Key Managerに保存したキーの削除をリクエストします。 |
| DELETE | /keymanager/v1.0/appkey/{appkey}/keys/{keyid} | Secure Key Managerに削除予定のキーを即時削除します。 |
| POST | /keymanager/v1.2/appkey/{appkey}/auths/{ipv4s\|macs\|certificates} | Secure Key Managerに認証情報を追加します。 |
| PUT | /keymanager/v1.2/appkey/{appkey}/auths/{ipv4s\|macs\|certificates}/delete | Secure Key Managerに認証情報の削除をリクエストします。 |
| POST | /keymanager/v1.2/appkey/{appkey}/auths/{ipv4s\|macs\|certificates}/delete | Secure Key Managerに認証情報の削除を行います。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores | Secure Key Managerに保存されたキーストアを照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId} | Secure Key Managerに保存されたキーストアの詳細を照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/keys | Secure Key Managerに保存されたキーストアのキーを照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/keys/{keyId} | Secure Key Managerに保存されたキーストアのキーを詳細照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/ips | Secure Key Managerに保存されたキーストアのIPv4認証情報を照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value} | Secure Key Managerに保存されたキーストアのIPv4認証情報の詳細を照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/macs | Secure Key Managerに保存されたキーストアのMAC認証情報を照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue} | Secure Key Managerに保存されたキーストアのMAC認証情報の詳細を照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/certificates | Secure Key Managerに保存されたキーストアの証明書認証情報を照会します。 |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName} | Secure Key Managerに保存されたキーストアの証明書認証情報の詳細を照会します。 |

[APIリクエストのHTTPヘッダ]

Secure Key ManagerのMACアドレス認証を使用するには、HTTPヘッダにクライアントMACアドレスを設定してリクエストする必要があります。
```
X-TOAST-CLIENT-MAC-ADDR: {MACアドレス}
```

[APIリクエストのパス変数]

| 名前 | タイプ | 説明 |
|---|---|---|
| appkey | String | 使用したいデータを保存しているNHN Cloudプロジェクトのアプリケーションキー |
| keyid | String | 使用したいデータの識別子 |

[APIレスポンスのデータ共通ヘッダ]
```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": {
        ...
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| resultCode | Number | API呼び出し結果コード値 |
| resultMessage | String | API呼び出し結果メッセージ |
| isSuccessful | Boolean | API呼び出し成否 |

<a id="query-client-information"></a>
## クライアント情報照会 { #query-client-information }
APIを呼び出したクライアント情報を照会する時に使用します。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/confirm
```
[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "clientIp": "0.0.0.0",
        "clientMacHeader": "00:00:00:00:00:00",
        "clientSentCertificate": false
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| clientIp | String | APIを呼び出したクライアントのIPアドレス |
| clientMacHeader | String | APIを呼び出したクライアントのMACアドレスヘッダ値 |
| clientSentCertificate | Boolean | APIを呼び出したクライアントが証明書を使用しているかどうか |

<a id="confidential-data"></a>
## 機密データ { #confidential-data }

<a id="query-confidential-data"></a>
### 機密データ照会 { #query-confidential-data }
Secure Key Managerに保存した機密データを照会する時に使用します。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/secrets/{keyid}
```

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "secret": "data"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| secret | String | 機密データ照会結果 |

<a id="modify-confidential-data"></a>
### 機密データの修正 { #modify-confidential-data }
Secure Key Managerに保存した機密データを修正する際に使用します。
```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/secrets/{keyid}
```

[Request Body]

```
{
    "secretValue": "data"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| secretValue | String | 変更する機密データの内容 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyId": "071dcc5c25614dffa52357e5cae3471f",
        "name": "キー名",
        "description": "キーの説明",
        "secretValue": "data",
        "creationUser": "SECURE_KEY_MANAGER",
        "creationDatetime": "2025-01-25T12:00:00",
        "lastChangeUser": "SECURE_KEY_MANAGER",
        "lastChangeDatetime": "2025-01-30T15:00:00.000"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyId | String | キーID |
| name | String | キー名 |
| description | String | キーの説明 |
| secretValue | String | 変更された機密データの内容 |
| creationUser | String | キー作成ユーザー |
| creationDatetime | String | キー作成日時 |
| lastChangeUser | String | キー最終修正ユーザー |
| lastChangeDatetime | String | キー最終修正日時 |

<a id="symmetric-key"></a>
## 対称鍵 { #symmetric-key }

<a id="encrypt-symmetric-keys"></a>
### 対称鍵暗号化 { #encrypt-symmetric-keys }
Secure Key Managerに作成した対称鍵でデータを暗号化する時に使用します。ユーザーは32KB以下のテキストデータを転送して、Secure Key Managerに保存した対称鍵で暗号化できます。
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/encrypt
```

[Request Body]

```
{
    "plaintext": "data"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| plaintext | String | 対称鍵で暗号化するデータ |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "ciphertext": "AAAAABzGwQniNneKXmcOLhWnxEqC1rNY+UdVb3lyeX/4wSrP",
        "keyVersion": 1
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| ciphertext | String | 対称鍵でデータを暗号化した結果 |
| keyVersion | Number | APIリクエスト処理に使用した対称鍵バージョン |

<a id="decrypt-symmetric-keys"></a>
### 対称鍵復号 { #decrypt-symmetric-keys }
Secure Key Managerに作成した対称鍵でデータを復号する時に使用します。ユーザーは暗号化されたテキストを転送して、Secure Key Managerに保存した対称鍵で復号できます。
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/decrypt
```

[Request Body]
```
{
    "ciphertext": "AAAAABzGwQniNneKXmcOLhWnxEqC1rNY+UdVb3lyeX/4wSrP"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| ciphertext | String | 対称鍵で復号するデータ |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "plaintext": "data",
        "keyVersion": 1
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| plaintext | String | 対称鍵でデータを復号した結果 |
| keyVersion | Number | APIリクエスト処理に使用した対称鍵バージョン |

<a id="generate-local-symmetric-keys-encrypted-with-the-symmetric-key"></a>
### 対称鍵で暗号化したローカル対称鍵作成 { #generate-local-symmetric-keys-encrypted-with-the-symmetric-key }
クライアントがローカル環境で使用できるAES-256対称鍵を作成する時に使用します。localKeyPlaintextは、作成した対称鍵をBase64エンコードした形式で、Base64エンコード後すぐに使用できます。localKeyCiphertextは、作成した対称鍵をSecure Key Managerに保存した対称鍵で暗号化した後にBase64エンコードした形式で、ストレージに保存する時に使用します。ストレージに保存した対称鍵は、復号APIを使用して復号した後に使用できます。
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key
```

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "localKeyPlaintext": "srV7MWkYIfYBknkASzwSEK1Z1y9Nx0f/RMZ3MSVIjm8=",
        "localKeyCiphertext": "v1s1WkiIj3KR+AafnupNv9xcX/JhL4GUzUr8mzLRpjbGuoAwU/GgboM/6QdRRY24",
        "keyVersion": 1
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| localKeyPlaintext | String | Base64エンコードしたAES-256対称鍵 |
| localKeyCiphertext | String | Secure Key Managerに保存した対称鍵で暗号化した後、Base64エンコードしたAES-256対称鍵 |
| keyVersion | Number | APIリクエスト処理に使用した対称鍵バージョン |

<a id="query-the-symmetric-key"></a>
### 対称鍵照会 { #query-the-symmetric-key }

Secure Key Managerに保存した対称鍵(AES-256)を照会できます。

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key?keyVersion={keyVersion}
```

[Request Parameter]

| 名前 | タイプ | 説明 |
|---|---|---|
| keyVersion | Number | 照会する対称鍵のバージョン |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "symmetricKey": "0x00, 0x20, 0x00, 0x41, 0x00, 0x20, 0x00, 0x73, 0x00, 0x69, 0x00, 0x6d, 0x00, 0x70, 0x00, 0x6c, 0x00, 0x65, 0x00, 0x20, 0x00, 0x4a, 0x00, 0x61, 0x00, 0x76, 0x00, 0x61, 0x00, 0x2e, 0x00, 0x20",
        "keyVersion": 1
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| symmetricKey | String | 対称鍵データ(16進数文字列形式) |
| keyVersion | Number | APIリクエスト処理に使用した対称鍵バージョン |

<a id="asymmetric-key"></a>
## 非対称鍵 { #asymmetric-key }

<a id="sign-with-the-asymmetric-key"></a>
### 非対称鍵で署名 { #sign-with-the-asymmetric-key }
Secure Key Managerに作成した非対称鍵で、データを署名する時に使用します。ユーザーは245Byte以下のテキストデータを転送して、Secure Key Managerに保存した非対称鍵で署名できます。
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/sign
```

[Request Body]
```
{
    "plaintext": "data"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| plaintext | String | 非対称鍵で署名するデータ |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "signature": "AAAAAGI9zf831DX...",
        "keyVersion": 1
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| signature | String | 非対称鍵でデータを署名した署名値 |
| keyVersion | Number | APIリクエスト処理に使用した非対称鍵バージョン |

<a id="verify-data-with-the-asymmetric-key"></a>
### 非対称鍵でデータ検証 { #verify-data-with-the-asymmetric-key }
Secure Key Managerに作成した非対称鍵で、データを検証する時に使用します。ユーザーはデータと署名値を転送して、Secure Key Managerに保存した非対称鍵でデータが改ざんされていないかを検証できます。
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/verify
```

[Request Body]

```
{
    "plaintext": "data",
    "signature": "AAAAAGI9zf831DX..."
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| plaintext | String | 非対称鍵で検証するデータ |
| signature | String | 非対称鍵でデータを署名した署名値 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "result": true,
        "keyVersion": 1
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| result | Boolean | 非対称鍵でデータと署名値を検証した結果 |
| keyVersion | Number | APIリクエスト処理に使用した非対称鍵バージョン |

<a id="query-the-private-key"></a>
### 秘密鍵照会 { #query-the-private-key }

Secure Key Managerに保存した非対称鍵のうち、秘密鍵を照会できます。

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey?keyVersion={keyVersion}
```

[Request Parameter]

| 名前 | タイプ | 説明 |
|---|---|---|
| keyVersion | Number | 照会する非対称鍵のバージョン |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PrivateKey",
        "key": "0x30, 0x82, 0x04, 0xbe, 0x02, 0x01, 0x00, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x04, 0x82, 0x04, 0xa8, 0x30, 0x82, 0x04, 0xa4, 0x02, 0x01, 0x00, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2,
                ... 後略 ...",
        "encodedKey": "MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCLB47ax4OVyEOnuDFv9iU2iWTFOHVLpoD+fMVqlPJiiuJSwi5x/zd3LojWuUyr+dZ9Icxl23Alu4GwwKgUi4DL8qo8jD14THJoeUgIZ56wmYMvN+CkNnmkyqcGn6yT+AXtBJVGqS/2lssHLIGELi8XXkWdf6OBfig6HgsJAnix8Z+T/QdikEFUI5ZiuUWyHw2Bag9B4CoPF2EgXfu5HcW4GA4KH2PI92O4vNg8AmFVDk2E+ma2quSau7LjS3KY9s3Sq+JqvTPZmqHQJudv9ZYcnbyDG/
                       ... 後略 ...",
        "keyVersion": 0
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyType | String | 非対称鍵形式 |
| key | String | 秘密鍵データ(16進数文字列形式) |
| encodedKey | String | 秘密鍵データ(Base64エンコード形式) |
| keyVersion | Number | APIリクエスト処理に使用した非対称鍵のバージョン |

<a id="query-the-public-key"></a>
### 公開鍵照会 { #query-the-public-key }

Secure Key Managerに保存した非対称鍵のうち、公開鍵を照会できます。
認証に関係なく照会できます。

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey?keyVersion={keyVersion}
```

[Request Parameter]

| 名前 | タイプ | 説明 |
|---|---|---|
| keyVersion | Number | 照会する非対称鍵のバージョン |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PublicKey",
        "key": "0x30, 0x82, 0x01, 0x22, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x03, 0x82, 0x01, 0x0f, 0x00, 0x30, 0x82, 0x01, 0x0a, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2, 0x62, 0x8a, 0xe2, 0x52, 0xc2,
                ... 後略 ...",
        "encodedKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAiweO2seDlchDp7gxb/YlNolkxTh1S6aA/nzFapTyYoriUsIucf83dy6I1rlMq/nWfSHMZdtwJbuBsMCoFIuAy/KqPIw9eExyaHlICGeesJmDLzfgpDZ5pMqnBp+sk/gF7QSVRqkv9pbLByyBhC4vF15FnX+jgX4oOh4LCQJ4sfGfk/0HYpBBVCOWYrlFsh8NgWoPQeAqDxdhIF37uR3FuBgOCh9jyPdjuLzYPAJhVQ5NhPpmtqrkmruy40tymPbN0qviar0z2Zqh0Cbnb/WWHJ28gxv+d+iJCXJvm+fIg7hRYJ5C+mun/N6FB8QHv/
                       ... 後略 ...",
        "keyVersion": 0
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyType | String | 非対称鍵形式 |
| key | String | 公開鍵データ(16進数文字列形式) |
| encodedKey | String | 公開鍵データ(Base64エンコード形式) |
| keyVersion | Number | APIリクエスト処理に使用した非対称鍵のバージョン |

<a id="adddelete-key"></a>
## キーの追加/削除 { #adddelete-key }

<a id="add-a-key"></a>
### キーの追加 { #add-a-key }
Secure Key Managerに新規キーを追加できます。

<a id="add-a-key-add-confidential-data"></a>
#### 機密データの追加
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keys/secrets/create
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "name" : "Key Sample #1",
    "description" : "Description #1",
    "secretValue" : "data"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | キーを保存するキーストア名 |
| name | String | キー名 |
| description | String | キーの説明 |
| secretValue | String | 機密データ値 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyId": "071dcc5c25614dffa52357e5cae3471f",
        "keyStatus": "ACTIVE"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyId | String | 作成されたキーID |
| keyStatus | String | キーの状態メッセージ |

<a id="add-a-key-add-a-symmetric-key"></a>
#### 対称鍵の追加
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keys/symmetric-keys/create
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "name" : "Key Sample #2",
    "description" : "Description #2",
    "autoRotationPeriod" : 0
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | キーを保存するキーストア名 |
| name | String | キー名 |
| description | String | キーの説明 |
| autoRotationPeriod | Number | ローテーション周期 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyId": "c2c49d986dfb4ca6afeaf67c39354c12",
        "keyStatus": "ACTIVE"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyId | String | 作成されたキーID |
| keyStatus | String | キーの状態メッセージ |

<a id="add-a-key-add-asymmetric-key"></a>
#### 非対称鍵の追加
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keys/asymmetric-keys/create
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "name" : "Key Sample #3",
    "description" : "Description #3",
    "autoRotationPeriod" : 0
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | キーを保存するキーストア名 |
| name | String | キー名 |
| description | String | キーの説明 |
| autoRotationPeriod | Number | ローテーション周期 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyId": "ddd7d5275dfa462799418062bd25b49d",
        "keyStatus": "ACTIVE"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyId | String | 作成されたキーID |
| keyStatus | String | キーの状態メッセージ |

<a id="delete-a-key"></a>
### キーの削除 { #delete-a-key }
Secure Key Managerに保存されたキーの状態を**削除予定**状態に変更したり、**即時削除**できます。

<a id="delete-a-key-request-to-delete-a-key"></a>
#### キー削除リクエスト
キーを**削除予定**状態に変更します。
キーは7日後に自動的に削除され、**削除予定**状態のキーは照会できません。
```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keys/{keyid}/delete
```

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyId": "071dcc5c25614dffa52357e5cae3471f",
        "deletionDateTime": "2023-11-20T22:00:00.00"
    }
}

```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyId | String | 作成されたキーID |
| deletionDateTime | String | キーの削除予定日 |

<a id="delete-a-key-immediately-delete-a-key"></a>
#### キーの即時削除
**即時削除**するキーは**削除予定**状態の時のみ**即時削除**が可能です。
有効状態のキーは**即時削除**できません。
```text
DELETE https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keys/{keyid}
```

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyId": "071dcc5c25614dffa52357e5cae3471f",
        "deletionDateTime": "2023-11-14T10:05:24.312"
    }
}

```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyId | String | 作成されたキーID |
| deletionDateTime | String | キーの削除時刻 |

<a id="add-and-delete-credentials"></a>
## 認証情報の追加/削除 { #add-and-delete-credentials }
Secure Key Managerはユーザーデータを保護するための認証方法として、クライアントのIPv4アドレスを確認する**IPv4アドレス認証**、クライアントのMACアドレスを確認する**MACアドレス認証**、クライアントが通信に使用する証明書を確認する**クライアント証明書認証**の認証方法を提供しています。

<a id="add-credentials"></a>
### 認証情報の追加/削除 { #add-credentials }
Secure Key Managerに認証情報を追加できます。

<a id="add-credentials-add-ipv4-address"></a>
#### IPv4アドレスの追加
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/auths/ipv4s
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "127.0.0.1",
    "description" : "Description #1"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | IPv4アドレスを保存するキーストア名 |
| value | String | IPv4アドレス値 |
| description | String | IPv4アドレスの説明 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "value": "127.0.0.1",
        "description": "Description #1"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| value | String | 作成されたIPv4アドレス値 |
| description | String | 作成されたIPv4アドレスの説明 |

<a id="add-credentials-add-mac-address"></a>
#### MACアドレスの追加
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/auths/macs
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "aa:aa:aa:aa:aa:aa",
    "description" : "Description #1"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | MACアドレスを保存するキーストア名 |
| value | String | MACアドレス値 |
| description | String | MACアドレスの説明

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "value": "aa:aa:aa:aa:aa:aa",
        "description": "Description #1"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| value | String | 作成されたMACアドレス値 |
| description | String | 作成されたMACアドレスの説明 |

<a id="add-credentials-add-certificate"></a>
#### 証明書の追加
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/auths/certificates
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "name" : "Certificate Name #1",
    "password" : "Password",
    "lifeTime" : 365,
    "description" : "Description #1"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | 証明書を保存するキーストア名 |
| name | String | 証明書の名前 |
| password | String | 証明書のパスワード |
| lifeTime | int | 証明書の使用期間(日) |
| description | String | 証明書の説明 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "name": "Certificate Name #1",
        "description": "Description #1"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| name | String | 作成された証明書の名前 |
| description | String | 作成された証明書の説明 |

<a id="delete-credentials"></a>
### 認証情報の削除 { #delete-credentials }
Secure Key Managerに保存された認証情報の状態を**削除予定**状態に変更したり、**即時削除**できます。

<a id="delete-credentials-request-to-delete-credentials"></a>
#### 認証情報削除リクエスト
認証情報を**削除予定**状態に変更します。
認証情報は7日後に自動的に削除されます。**削除予定**状態の認証情報は使用できません。

<a id="delete-credentials-request-to-delete-an-ipv4-address"></a>
#### IPv4アドレスの削除リクエスト
```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/auths/ipv4s/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "127.0.0.1"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | IPv4アドレスを削除リクエストするキーストア名 |
| value | String | 削除リクエストするIPv4アドレス値 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "value": "127.0.0.1",
        "deletionDateTime": "2024-03-14T11:00:00"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| value | String | 削除をリクエストしたIPv4アドレス値 |
| deletionDateTime | String | IPv4アドレスの削除予定時間 |

<a id="delete-credentials-request-to-delete-mac-address"></a>
#### MACアドレスの削除リクエスト
```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/auths/macs/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "aa:aa:aa:aa:aa:aa"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | MACアドレスを削除リクエストするキーストアの名前 |
| value | String | 削除リクエストするMACアドレス値 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "value": "aa:aa:aa:aa:aa:aa",
        "deletionDateTime": "2024-03-14T11:00:00"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| value | String | 削除リクエストしたMACアドレス値 |
| deletionDateTime | String | MACアドレスの削除予定時間 |

<a id="delete-credentials-request-to-delete-certificate"></a>
#### 証明書の削除リクエスト
```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/auths/certificates/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "name" : "Certificate Name #1"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | 証明書を削除リクエストするキーストア名 |
| name | String | 削除リクエストする証明書の名前 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "name": "Certificate Name #1",
        "deletionDateTime": "2024-03-14T11:00:00"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| name | String | 削除リクエストした証明書の名前 |
| deletionDateTime | String | 証明書の削除予定時間 |

<a id="delete-credentials-immediately-delete-credentials"></a>
#### 認証情報の即時削除
**即時削除**を行う認証情報は、**削除予定*状態の場合のみ**即時削除**が可能です。
有効状態の認証情報は**即時削除**できません。

<a id="delete-credentials-immediately-delete-ipv4"></a>
#### IPv4アドレスの即時削除
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/auths/ipv4s/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "127.0.0.1"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | IPv4アドレスを即時削除するキーストア名 |
| value | String | 即時削除するIPv4アドレス値 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "value": "127.0.0.1",
        "deletionDateTime": "2024-03-14T11:00:00"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| value | String | 削除したIPv4アドレス値 |
| deletionDateTime | String | IPv4アドレスの削除時間 |

<a id="delete-credentials-immediately-delete-mac-address"></a>
#### MACアドレスの即時削除
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/auths/macs/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "aa:aa:aa:aa:aa:aa"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | MACアドレスを即時削除するキーストア名 |
| value | String | 即時削除するMACアドレス値 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "value": "aa:aa:aa:aa:aa:aa",
        "deletionDateTime": "2024-03-14T11:00:00"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| value | String | 削除したMACアドレス値 |
| deletionDateTime | String | MACアドレスの削除時間 |

<a id="delete-credentials-immediately-delete-certificate"></a>
#### 証明書の即時削除
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/auths/certificates/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "name" : "Certificate Name #1"
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreName | String | 証明書を即時削除するキーストア名 |
| name | String | 即時削除する証明書の名前 |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "name": "Certificate Name #1",
        "deletionDateTime": "2024-03-14T11:00:00"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| name | String | 削除した証明書の名前 |
| deletionDateTime | String | 証明書の削除時間 |

<a id="key-store"></a>
## キーストア { #key-store }

<a id="query-the-list-of-key-stores"></a>
### キーストアリスト照会 { #query-the-list-of-key-stores }
Secure Key Managerに作成したキーストアのIDリストを照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyStoreIdList": [
            1,
            2,
            ...
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreIdList | List | キーストアIDリスト |

<a id="retrieve-key-store-list-details"></a>
### キーストアリスト詳細照会 { #retrieve-key-store-list-details }
Secure Key Managerに作成したキーストアの詳細情報リストを照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores?detail={detail}
```

[Request Parameter]

| 名前 | タイプ | 説明 |
|---|---|---|
| detail | Boolean | 詳細情報の包含有無(デフォルト値: false) |

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyStoreList": [
            {
                "keyStoreId": 1,
                "name": "キーストア名",
                "description": "キーストアの説明",
                "ip4AuthUse": "Y",
                "macAuthUse": "N",
                "certificateAuthUse": "Y",
                "creationUser": "SECURE_KEY_MANAGER",
                "creationDatetime": "2025-02-10T12:00:00",
                "lastChangeUser": "SECURE_KEY_MANAGER",
                "lastChangeDatetime": "2025-02-10T15:00:00.000"
            },
            ...
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreList | List | キーストア詳細情報リスト |
| keyStoreId | Number | キーストアID |
| name | String | キーストア名 |
| description | String | キーストアの説明 |
| ip4AuthUse | String | キーストアIPv4認証の使用有無(Y/N) |
| macAuthUse | String | キーストアMAC認証の使用有無(Y/N) |
| certificateAuthUse | String | キーストア証明書認証の使用有無(Y/N) |
| creationUser | String | キーストア作成ユーザー |
| creationDatetime | String | キーストア作成日時 |
| lastChangeUser | String | キーストア最終修正ユーザー |
| lastChangeDatetime | String | キーストア最終修正日時 |

<a id="query-the-details-of-the-key-store"></a>
### キーストア詳細照会 { #query-the-details-of-the-key-store }
Secure Key Managerに作成したキーストア情報を詳細照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyStoreId": 1,
        "name": "キーストア名",
        "description": "キーストアの説明",
        "ip4AuthUse": "Y",
        "macAuthUse": "N",
        "certificateAuthUse": "Y",
        "creationUser": "SECURE_KEY_MANAGER",
        "creationDatetime": "2025-01-25T12:00:00",
        "lastChangeUser": "SECURE_KEY_MANAGER",
        "lastChangeDatetime": "2025-01-30T15:00:00.000"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyStoreId | Number | キーストアID |
| name | String | キーストア名 |
| description | String | キーストアの説明 |
| ip4AuthUse | String | キーストアIPv4認証の使用有無(Y/N) |
| macAuthUse | String | キーストアMAC認証の使用有無(Y/N) |
| certificateAuthUse | String | キーストア証明書認証の使用有無(Y/N) |
| creationUser | String | キーストア作成ユーザー |
| creationDatetime | String | キーストア作成日時 |
| lastChangeUser | String | キーストアの最終修正ユーザー |
| lastChangeDatetime | String | キーストアの最終修正日時 |

<a id="key"></a>
## キー { #key }

<a id="query-the-list-of-keys"></a>
### キーリスト照会 { #query-the-list-of-keys }
Secure Key Managerに作成したキーのIDリストを照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/keys
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyIdList": [
            "035a0ffa16a64bbf8171c4bdcea37bbf",
            "04fde6d8ee604cbe8fa7abe135a7dc3e",
            ...
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyIdList | List | キーIDリスト |

<a id="retrieve-key-list-details"></a>
### キーリスト詳細照会 { #retrieve-key-list-details }
Secure Key Managerに作成したキーの詳細情報リストを照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/keys?detail={detail}&type={type}&name={name}&status={status}&pageNumber={pageNumber}&pageSize={pageSize}
```

[Request Parameter]

| 名前 | タイプ | 説明 |
|---|---|---|
| detail | Boolean | 詳細情報の包含有無(デフォルト値: false) |
| type | String | キータイプフィルタ(SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY、デフォルト値: all、複数選択不可) |
| name | String | キー名フィルタ(最大100文字) |
| status | String | キー状態フィルタ(active/inactive、デフォルト値: all) |
| pageNumber | Number | ページ番号(デフォルト値: 1、正の数) |
| pageSize | Number | ページサイズ(デフォルト値: 10、10～100) |

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyList": [
            {
                "keyId": "035a0ffa16a64bbf8171c4bdcea37bbf",
                "name": "キー名",
                "description": "キーの説明",
                "keyType": "SYMMETRIC_KEY",
                "currentKeyValueVersion": 2,
                "autoRotationPeriod": 0,
                "nextAutoRotationDate": null,
                "lastAccessDatetime": "2025-02-10T15:13:13.377",
                "deletionDatetime": null,
                "creationUser": "SECURE_KEY_MANAGER",
                "creationDatetime": "2025-02-10T12:00:00",
                "lastChangeUser": "SECURE_KEY_MANAGER",
                "lastChangeDatetime": "2025-02-10T15:00:00.000"
            },
            ...
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyList | List | キー詳細情報リスト |
| keyId | String | キーID |
| name | String | キー名 |
| description | String | キーの説明 |
| keyType | String | キータイプ(SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY) |
| currentKeyValueVersion | Number | 現在のキーバージョン |
| autoRotationPeriod | Number | キーローテーション周期 |
| nextAutoRotationDate | String | 次回キーローテーション日 |
| lastAccessDatetime | String | キー最終使用日時 |
| deletionDatetime | String | キー削除予定日時 |
| creationUser | String | キー作成ユーザー |
| creationDatetime | String | キー作成日時 |
| lastChangeUser | String | キー最終修正ユーザー |
| lastChangeDatetime | String | キー最終修正日時 |

<a id="query-the-details-of-keys"></a>
### キー詳細照会 { #query-the-details-of-keys }
Secure Key Managerに作成したキー情報を詳細に照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/keys/{keyId}
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyId": "035a0ffa16a64bbf8171c4bdcea37bbf",
        "name": "キー名",
        "description": "キーの説明",
        "keyType": "SYMMETRIC_KEY",
        "currentKeyValueVersion": 2,
        "autoRotationPeriod": 0,
        "nextAutoRotationDate": null,
        "lastAccessDatetime": "2021-12-13T15:13:13.377",
        "deletionDatetime": null,
        "creationUser": "SECURE_KEY_MANAGER",
        "creationDatetime": "2025-01-25T12:00:00",
        "lastChangeUser": "SECURE_KEY_MANAGER",
        "lastChangeDatetime": "2025-01-30T15:00:00.000"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| keyId | String | キーID |
| name | String | キー名 |
| description | String | キーの説明 |
| keyType | String | キータイプ(SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY) |
| currentKeyValueVersion | Number | 現在キーバージョン |
| autoRotationPeriod | Number | キーのローテーション周期 |
| nextAutoRotationDate | String | 次のキーのローテーション日 |
| lastAccessDatetime | String | キーの最終使用日時 |
| creationUser | String | キー作成ユーザー |
| creationDatetime | String | キー作成日時 |
| lastChangeUser | String | キー最終修正ユーザー |
| lastChangeDatetime | String | キー最終修正日時 |

<a id="authentication-information"></a>
## 認証情報 { #authentication-information }

<a id="query-the-list-of-ipv4-authentication-information"></a>
### IPv4認証情報リスト照会 { #query-the-list-of-ipv4-authentication-information }
Secure Key Managerで設定したキーストアのIPv4認証情報リストを照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/ips
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "ipv4List": [
            "127.0.0.1",
            "127.0.0.2",
            ...
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| ipv4List | List | IPv4認証情報リスト |

<a id="query-the-details-of-ipv4-authentication-information"></a>
### IPv4認証情報詳細照会 { #query-the-details-of-ipv4-authentication-information }
Secure Key Managerで設定したキーストアのIPv4認証情報を詳細照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value}
```

[Request Parameter]

| 名前 | タイプ | 説明 |
|---|---|---|
| ipv4Value | String | 照会対象のIPv4アドレス |

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "ipv4List": [
            {
                "value": "127.0.0.1",
                "description": "IPv4の説明",
                "lastAccessDatetime": "2025-01-25T13:00:00",
                "deletionDatetime": null,
                "creationUser": "SECURE_KEY_MANAGER",
                "creationDatetime": "2025-01-25T12:00:00",
                "lastChangeUser": "SECURE_KEY_MANAGER",
                "lastChangeDatetime": "2025-01-30T15:00:00.000"
            }
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| ipv4List | List | IPv4認証情報リスト |
| value | String | IPv4値 |
| description | String | IPv4説明 |
| lastAccessDatetime | String | IPv4最終使用日時 |
| deletionDatetime | String | IPv4削除予定日時 |
| creationUser | String | IPv4作成ユーザー |
| creationDatetime | String | IPv4作成日時 |
| lastChangeUser | String | IPv4最終修正ユーザー |
| lastChangeDatetime | String | IPv4最終修正日時 |

<a id="query-the-list-of-mac-authentication-information"></a>
### MAC認証情報リスト照会 { #query-the-list-of-mac-authentication-information }
Secure Key Managerで設定したキーストアのMAC認証情報リストを照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/macs
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "macList": [
            "aa:aa:aa:aa:aa:aa",
            "bb:bb:bb:bb:bb:bb",
            ...
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| macList | List | MAC認証情報リスト |

<a id="query-the-details-of-mac-authentication-information"></a>
### MAC認証情報詳細照会 { #query-the-details-of-mac-authentication-information }
Secure Key Managerで設定したキーストアのMAC認証情報を詳細照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue}
```

[Request Parameter]

| 名前 | タイプ | 説明 |
|---|---|---|
| macValue | String | 照会対象のMACアドレス |

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "macList": [
            {
                "value": "aa:aa:aa:aa:aa:aa",
                "description": "MAC説明",
                "lastAccessDatetime": "2025-01-25T13:00:00",
                "deletionDatetime": null,
                "creationUser": "SECURE_KEY_MANAGER",
                "creationDatetime": "2025-01-25T12:00:00",
                "lastChangeUser": "SECURE_KEY_MANAGER",
                "lastChangeDatetime": "2025-01-30T15:00:00.000"
            }
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| macList | List | MAC認証情報リスト |
| value | String | MAC値 |
| description | String | MAC説明 |
| lastAccessDatetime | String | MAC最終使用日時 |
| deletionDatetime | String | MAC削除予定日時 |
| creationUser | String | MAC作成ユーザー |
| creationDatetime | String | MAC作成日時 |
| lastChangeUser | String | MAC最終修正ユーザー |
| lastChangeDatetime | String | MAC最終修正日時 |

<a id="query-the-list-of-certificate-authentication-information"></a>
### 証明書認証情報リスト照会 { #query-the-list-of-certificate-authentication-information }
Secure Key Managerで設定したキーストアの証明書認証情報リストを照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/certificates
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "certificateList": [
            "certificate1",
            "certificate2",
            ...
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| certificateList | List | 証明書認証情報リスト |

<a id="query-the-details-of-certifacate-authentication-information"></a>
### 証明書認証情報詳細照会 { #query-the-details-of-certifacate-authentication-information }
Secure Key Managerで設定したキーストアの証明書認証情報を詳細に照会できます。
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName}
```

[Request Parameter]

| 名前 | タイプ | 説明 |
|---|---|---|
| certificateName | String | 照会対象の証明書名 |

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "certificateList": [
            {
                "name": "certificate1",
                "password": "password1",
                "description": "証明書説明",
                "expirationDate": "2029-07-21T10:26:47",
                "lastAccessDatetime": "2025-01-25T13:00:00",
                "deletionDatetime": null,
                "creationUser": "SECURE_KEY_MANAGER",
                "creationDatetime": "2025-01-25T12:00:00",
                "lastChangeUser": "SECURE_KEY_MANAGER",
                "lastChangeDatetime": "2025-01-30T15:00:00.000"
            }
        ]
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| certificateList | List | 証明書認証情報リスト |
| name | String | 証明書名 |
| password | String | 証明書パスワード |
| description | String | 証明書説明 |
| lastAccessDatetime | String | 証明書最終使用日時 |
| deletionDatetime | String | 証明書削除予定日時 |
| creationUser | String | 証明書作成ユーザー |
| creationDatetime | String | 証明書作成日時 |
| lastChangeUser | String | 証明書最終修正ユーザー |
| lastChangeDatetime | String | 証明書最終修正日時 |
