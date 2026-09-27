<!-- machine_translated: true -->

<!-- pre-align:aligned sig=627282543df6 -->

<a id="security-secure-key-manager-api-v10-guide"></a>
## Security > Secure Key Manager > API v1.0 Guide { #security-secure-key-manager-api-v10-guide }

Secure Key Manager provides various APIs to access user data. Clients must be authenticated via key store to get access to data stored in Secure Kay Manager.

<a id="secure-key-manager-api-common-information"></a>
## Secure Key Manager API Common Information { #secure-key-manager-api-common-information }

<a id="api-endpoint"></a>
### API Endpoint { #api-endpoint }

| Region | Endpoint |
|---|---|
| Global | https://api-keymanager.nhncloudservice.com |

<a id="authentication-and-authorization"></a>
### Authentication and Authorization { #authentication-and-authorization }

An AppKey or a Project Integrated Appkey is required to use the Secure Key Manager API v1.0.

An AppKey is a unique authentication key issued for each individual NHN Cloud service, while a Project Integrated Appkey is a common authentication key that can be shared across multiple services within a single NHN Cloud project.

For more information on checking and using Appkeys, please refer to the [Appkey](/nhncloud/en/public-api/appkey). For more information on creating and using Project Integrated Appkeys, please refer to the [Project Integrated Appkey](/nhncloud/en/public-api/project-integrated-appkey).

<a id="list-of-apis"></a>
### List of APIs { #list-of-apis }

| Method | URI | Description |
|---|---|---|
| GET | /keymanager/v1.0/appkey/{appkey}/confirm | Provide information of the client that called API. |
| GET | /keymanager/v1.0/appkey/{appkey}/secrets/{keyid} | Query confidential data stored in Secure Key Manager. |
| POST | /keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/encrypt | Encrypt data with the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/decrypt | Decrypt data with the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key | Create AES-256 symmetric keys that can be used by a client for data encryption/decryption in local environment. |
| GET | /keymanager/{v1.0\|v1.1}/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key | Query the symmetric key stored in Secure Key Manager.|
| POST | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/sign | Sign data with the asymmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/verify | Verify data and signature with the asymmetric key stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey | Query the private key stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey | Query the public key stored in Secure Key Manager. |

[HTTP Header of API Request]

To use MAC address authentication of Secure Key Manager, you must make a request by setting the client's MAC address in the HTTP header.
```
X-TOAST-CLIENT-MAC-ADDR: {MAC Address}
```

[Path Variables of API Request]

| Name | Type | Description |
|---|---|---|
| appkey | String | Appkey of the NHN Cloud project where the data in need is stored |
| keyid | String | Identifier of data in need |

[Common Data Header of API Response]
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
| Name | Type | Description |
|---|---|---|
| resultCode | Number | Result code value of API call |
| resultMessage | String | Result message of API call |
| isSuccessful | Boolean | Whether API call is successful or not |

<a id="query-client-information"></a>
## Query Client Information { #query-client-information }
This API is used to query information of the client that called API.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/confirm
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
| Name | Type | Description |
|---|---|---|
| clientIp | String | IP address of the client that called API |
| clientMacHeader | String |Header value of MAC address of the client that called API |
| clientSentCertificate | Boolean | Whether the client that called API is using certificate or not |

<a id="confidential-data"></a>
## Confidential Data { #confidential-data }

<a id="query-confidential-data"></a>
### Query Confidential Data { #query-confidential-data }
This API is used to query confidential data stored in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/secrets/{keyid}
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
| Name | Type | Description |
|---|---|---|
| secret | String | Query result of confidential data |

<a id="symmetric-key"></a>
## Symmetric Key { #symmetric-key }

<a id="encrypt-symmetric-keys"></a>
### Encrypt Symmetric Keys { #encrypt-symmetric-keys }
This API is used to encrypt data with the symmetric key created in Secure Key Manager. A user can pass 32KB or smaller text data, and the data can be encrypted with the symmetric key stored in Secure Key Manager.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/encrypt
```

[Request Body]

```
{
    "plaintext": "data"
}
```
| Name | Type | Description |
|---|---|---|
| plaintext | String | Data to be encrypted with the symmetric key |

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
| Name | Type | Description |
|---|---|---|
| ciphertext | String | Result of data encryption with the symmetric key |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

<a id="decrypt-symmetric-keys"></a>
### Decrypt Symmetric Keys { #decrypt-symmetric-keys }
This API is used to decrypt data with the symmetric key created in Secure Key Manager. A use can pass encrypted text, and the text data can be decrypted with the symmetric key stored in Secure Key Manager.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/decrypt
```

[Request Body]
```
{
    "ciphertext": "AAAAABzGwQniNneKXmcOLhWnxEqC1rNY+UdVb3lyeX/4wSrP"
}
```
| Name | Type | Description |
|---|---|---|
| ciphertext | String | Data to be decrypted with the symmetric key |

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
| Name | Type | Description |
|---|---|---|
| plaintext | String | Result of data decryption with the symmetric key |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

<a id="generate-local-symmetric-keys-encrypted-with-the-symmetric-key"></a>
### Generate Local Symmetric Keys Encrypted with the Symmetric Key { #generate-local-symmetric-keys-encrypted-with-the-symmetric-key }
This API is used to create AES-256 symmetric keys that a client can use in local environment. localKeyPlaintext is a base64-encoded form of the generated symmetric key, and it is readily available after base64 decoding. localKeyCiphertext is a base64-encoded form of the generated symmetric key encrypted with the symmetric key stored in Secure Key Manager, and it is used to store data in a storage. The symmetric key stored in storage can be used after being decrypted by using the decryption API.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key
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
| Name | Type | Description |
|---|---|---|
| localKeyPlaintext | String | Base64-encoded AES-256 symmetric key |
| localKeyCiphertext | String | Base64-encoded AES-256 symmetric key encrypted with the symmetric key stored in Secure Key Manager |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

<a id="query-the-symmetric-key"></a>
### Query the Symmetric Key { #query-the-symmetric-key }

Users can query the symmetric key (AES-256) stored in Secure Key Manager.

<a id="query-the-symmetric-key-v10"></a>
#### v1.0
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key
```

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "symmetricKey": "0x00, 0x20, 0x00, 0x41, 0x00, 0x20, 0x00, 0x73, 0x00, 0x69, 0x00, 0x6d, 0x00, 0x70, 0x00, 0x6c, 0x00, 0x65, 0x00, 0x20, 0x00, 0x4a, 0x00, 0x61, 0x00, 0x76, 0x00, 0x61, 0x00, 0x2e, 0x00, 0x20"
    }
}
```
| Name | Type | Description |
|---|---|---|
| symmetricKey | String | Symmetric key data (Hex string form) |

<a id="query-the-symmetric-key-v11"></a>
#### v1.1
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.1/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key?keyVersion={keyVersion}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| keyVersion | Number | Symmetric key version to retrieve |

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
| Name | Type | Description |
|---|---|---|
| symmetricKey | String | Symmetric key data (Hex string form) |
| keyVersion | Number |  Version of the symmetric key used for processing the API request |

<a id="asymmetric-key"></a>
## Asymmetric Key { #asymmetric-key }

<a id="sign-with-the-asymmetric-key"></a>
### Sign with the Asymmetric Key { #sign-with-the-asymmetric-key }
This API is used to sign data with the asymmetric key created in Secure Key Manager. Users can pass 245 Byte or smaller text data, and the data is signed with the asymmetric key stored in Secure Key Manager.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/sign
```

[Request Body]
```
{
    "plaintext": "data"
}
```
| Name | Type | Description |
|---|---|---|
| plaintext | String | Data to sign with the asymmetric key |

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
| Name | Type | Description |
|---|---|---|
| signature | String | Signature value of signing the data with the asymmetric key |
| keyVersion | Number | Version of the asymmetric key used for processing the API request |

<a id="verify-data-with-the-asymmetric-key"></a>
### Verify Data with the Asymmetric Key { #verify-data-with-the-asymmetric-key }
This API is used to verify data with the asymmetric key created in Secure Key Manager. Users can pass data and signature value, and use asymmetric keys stored in Secure Key Manager to verify that data has not been forged.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/verify
```

[Request Body]

```
{
    "plaintext": "data",
    "signature": "AAAAAGI9zf831DX..."
}
```
| Name | Type | Description |
|---|---|---|
| plaintext | String | Data to be verified with the asymmetric key |
| signature | String | Signature value of signing the data with the asymmetric key |

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
| Name | Type | Description |
|---|---|---|
| result | Boolean | Result of verifying data and signature value with the asymmetric key |
| keyVersion | Number | Version of the asymmetric key used for processing the API request |

<a id="query-the-private-key"></a>
### Query the Private Key { #query-the-private-key }

Users can query the private key among the asymmetric keys stored in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey?keyVersion={keyVersion}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| keyVersion | Number | Asymmetric key version to retrieve |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PrivateKey",
        "key": "0x30, 0x82, 0x04, 0xbe, 0x02, 0x01, 0x00, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x04, 0x82, 0x04, 0xa8, 0x30, 0x82, 0x04, 0xa4, 0x02, 0x01, 0x00, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2,
                ... ",
        "encodedKey": "MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCLB47ax4OVyEOnuDFv9iU2iWTFOHVLpoD+fMVqlPJiiuJSwi5x/zd3LojWuUyr+dZ9Icxl23Alu4GwwKgUi4DL8qo8jD14THJoeUgIZ56wmYMvN+CkNnmkyqcGn6yT+AXtBJVGqS/2lssHLIGELi8XXkWdf6OBfig6HgsJAnix8Z+T/QdikEFUI5ZiuUWyHw2Bag9B4CoPF2EgXfu5HcW4GA4KH2PI92O4vNg8AmFVDk2E+ma2quSau7LjS3KY9s3Sq+JqvTPZmqHQJudv9ZYcnbyDG/
                       ... ",
        "keyVersion": 0
    }
}
```
| Name | Type | Description |
|---|---|---|
| keyType | String | Asymmetric key form |
| key | String | Private key data (Hex string form) |
| encodedKey | String | Private key data (Base64-encoded form) |
| keyVersion | Number | Version of asymmetric key used for processing API requests |

<a id="query-the-public-key"></a>
### Query the Public Key { #query-the-public-key }

Users can query the public key among the asymmetric keys stored in Secure Key Manager, regardless of authentication.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey?keyVersion={keyVersion}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| keyVersion | Number | Asymmetric key version to retrieve |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PublicKey",
        "key": "0x30, 0x82, 0x01, 0x22, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x03, 0x82, 0x01, 0x0f, 0x00, 0x30, 0x82, 0x01, 0x0a, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2, 0x62, 0x8a, 0xe2, 0x52, 0xc2,
                ... ",
        "encodedKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAiweO2seDlchDp7gxb/YlNolkxTh1S6aA/nzFapTyYoriUsIucf83dy6I1rlMq/nWfSHMZdtwJbuBsMCoFIuAy/KqPIw9eExyaHlICGeesJmDLzfgpDZ5pMqnBp+sk/gF7QSVRqkv9pbLByyBhC4vF15FnX+jgX4oOh4LCQJ4sfGfk/0HYpBBVCOWYrlFsh8NgWoPQeAqDxdhIF37uR3FuBgOCh9jyPdjuLzYPAJhVQ5NhPpmtqrkmruy40tymPbN0qviar0z2Zqh0Cbnb/WWHJ28gxv+d+iJCXJvm+fIg7hRYJ5C+mun/N6FB8QHv/
                       ... ",
        "keyVersion": 0
    }
}
```
| Name | Type | Description |
|---|---|---|
| keyType | String | Asymmetric key form |
| key | String | Public key data (Hex string form) |
| encodedKey | String | Public key data (Base64-encoded form) |
| keyVersion | Number | Version of asymmetric key used for processing API requests |
