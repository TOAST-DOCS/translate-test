<!-- pre-align:aligned sig=aa5c9758414b -->

<a id="security-secure-key-manager-api-v12-guide"></a>
## Security > Secure Key Manager > API v1.2 Guide { #security-secure-key-manager-api-v12-guide }

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

Secure Key Manager API v1.2 supports Appkey, Project Integrated Appkey, and User Access Key as authentication methods for API calls.

Appkey is included in the request URL when calling the API to identify and point to a specific resource. Alternatively, a Project-integrated Appkey can be used in place of Appkey.
A User Access Key is an authentication key issued based on an NHN Cloud or IAM account. It is used in conjunction with a Secret Access Key to authenticate API requests.

For more information on how to check and use each authentication method, see [Appkey](/nhncloud/en/public-api/appkey), [Project-integrated Appkey](/nhncloud/en/public-api/project-integrated-appkey), and [User Access Key](/nhncloud/en/public-api/user-access-key).

<a id="list-of-apis"></a>
### List of APIs { #list-of-apis }

| Method | URI | Description |
|---|---|---|
| GET | /keymanager/v1.2/appkey/{appkey}/confirm | Provide information of the client that called API. |
| GET | /keymanager/v1.2/appkey/{appkey}/secrets/{keyid} | Query confidential data stored in Secure Key Manager. |
| PUT | /keymanager/v1.2/appkey/{appkey}/secrets/{keyid} | Modify confidential data stored in Secure Key Manager. |
| POST | /keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/encrypt | Encrypt data with the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/decrypt | Decrypt data with the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key | Create AES-256 symmetric keys that can be used by a client for data encryption/decryption in local environment. |
| GET | /keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key | Query the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/sign | Sign data with the asymmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/verify | Verify data and signature with the asymmetric key stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey | Query the private key stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey | Query the public key stored in Secure Key Manager. |
| POST | /keymanager/v1.2/appkey/{appkey}/keys/{secrets\|symmetric-keys\|asymmetric-keys}/create | Add a new key to Secure Key Manager. |
| PUT | /keymanager/v1.2/appkey/{appkey}/keys/{keyid}/delete | Request deletion of a key stored in Secure Key Manager. |
| DELETE | /keymanager/v1.2/appkey/{appkey}/keys/{keyid} | Immediately delete the key scheduled for deletion in Secure Key Manager. |
| POST | /keymanager/v1.2/appkey/{appkey}/auths/{ipv4s\|macs\|certificates} | Add credentials to Secure Key Manager. |
| PUT | /keymanager/v1.2/appkey/{appkey}/auths/{ipv4s\|macs\|certificates}/delete | Request deletion of credentials in Secure Key Manager. |
| POST | /keymanager/v1.2/appkey/{appkey}/auths/{ipv4s\|macs\|certificates}/delete | Immediately delete credentials in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores | Query the key stores stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId} | Query the details of the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/keys | Query the keys in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/keys/{keyId} | Query the details of the key in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/ips | Query the IPv4 authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value} | Query the details of the IPv4 authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/macs | Query the MAC authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue} | Query the details of the MAC authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/certificates | Query the certificate authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName} | Query the details of the certificate authentication information in the key store stored in Secure Key Manager. |

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
| Name | Type | Description |
|---|---|---|
| clientIp | String | IP address of the client that called API |
| clientMacHeader | String | Header value of MAC address of the client that called API |
| clientSentCertificate | Boolean | Whether the client that called API is using certificate or not |

<a id="confidential-data"></a>
## Confidential Data { #confidential-data }

<a id="query-confidential-data"></a>
### Query Confidential Data { #query-confidential-data }
This API is used to query confidential data stored in Secure Key Manager.
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
| Name | Type | Description |
|---|---|---|
| secret | String | Query result of confidential data |

<a id="modify-confidential-data"></a>
### Modify Confidential Data { #modify-confidential-data }
Use this feature to edit confidential data stored in Secure Key Manager.
```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/secrets/{keyid}
```

[Request Body]

```
{
    "secretValue": "data"
}
```
| Name | Type | Description |
|---|---|---|
| secretValue | String | Confidential data to be changed |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyId": "071dcc5c25614dffa52357e5cae3471f",
        "name": "Key name",
        "description": "Key description",
        "secretValue": "data",
        "creationUser": "SECURE_KEY_MANAGER",
        "creationDatetime": "2025-01-25T12:00:00",
        "lastChangeUser": "SECURE_KEY_MANAGER",
        "lastChangeDatetime": "2025-01-30T15:00:00.000"
    }
}
```
| Name | Type | Description |
|---|---|---|
| keyId | String | Key ID |
| name | String | Key name |
| description | String | Key description |
| secretValue | String | Changed confidential data content |
| creationUser | String | Key creation user |
| creationDatetime | String | Key creation date and time |
| lastChangeUser | String | Key last modified user |
| lastChangeDatetime | String | Key last modified date and time |

<a id="symmetric-key"></a>
## Symmetric Key { #symmetric-key }

<a id="encrypt-symmetric-keys"></a>
### Encrypt Symmetric Keys { #encrypt-symmetric-keys }
This API is used to encrypt data with the symmetric key created in Secure Key Manager. A user can pass 32KB or smaller text data, and the data can be encrypted with the symmetric key stored in Secure Key Manager.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/encrypt
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
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/decrypt
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
| Name | Type | Description |
|---|---|---|
| localKeyPlaintext | String | Base64-encoded AES-256 symmetric key |
| localKeyCiphertext | String | Base64-encoded AES-256 symmetric key encrypted with the symmetric key stored in Secure Key Manager |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

<a id="query-the-symmetric-key"></a>
### Query the Symmetric Key { #query-the-symmetric-key }

Users can query the symmetric key (AES-256) stored in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key?keyVersion={keyVersion}
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
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/sign
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
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/verify
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
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey?keyVersion={keyVersion}
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
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey?keyVersion={keyVersion}
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

<a id="adddelete-key"></a>
## Add/Delete Key { #adddelete-key }

<a id="add-a-key"></a>
### Add a key { #add-a-key }
Add a new key to Secure Key Manager.

<a id="add-a-key-add-confidential-data"></a>
#### Add confidential data
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keys/secrets/create
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name where key is saved |
| name | String | Key name |
| description | String | Key description |
| secretValue | String | Confidential data value |

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
| Name | Type | Description |
|---|---|---|
| keyId | String | Created key ID |
| keyStatus | String | Key status message |

<a id="add-a-key-add-a-symmetric-key"></a>
#### Add a symmetric key
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keys/symmetric-keys/create
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name where key is saved |
| name | String | Key name |
| description | String | Key description |
| autoRotationPeriod | Number | Rotation period |

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
| Name | Type | Description |
|---|---|---|
| keyId | String | Created key ID |
| keyStatus | String | Key status message |

<a id="add-a-key-add-asymmetric-key"></a>
#### Add asymmetric key
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keys/asymmetric-keys/create
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name where key is saved |
| name | String | Key name |
| description | String | Key description |
| autoRotationPeriod | Number | Rotation period |

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
| Name | Type | Description |
|---|---|---|
| keyId | String | Created key ID |
| keyStatus | String | Key status message |

<a id="delete-a-key"></a>
### Delete a key { #delete-a-key }
You can change the status of a key stored in Secure Key Manager to **To be deleted**, or **delete it immediately**.

<a id="delete-a-key-request-to-delete-a-key"></a>
#### Request to delete a key
Change the key status to **To be deleted**.
The key is automatically deleted after 7 days, and you can't view a key in the **To be deleted** status.
```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keys/{keyid}/delete
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
| Name | Type | Description |
|---|---|---|
| keyId | String | Created key ID |
| deletionDateTime | String | Date when key is to be deleted |

<a id="delete-a-key-immediately-delete-a-key"></a>
#### Immediately delete a key
The key that is to be **deleted immediately** can only be **deleted immediately** in the status of **To be deleted**.
You cannot **immediately delete** a key that is activated.
```text
DELETE https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keys/{keyid}
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
| Name | Type | Description |
|---|---|---|
| keyId | String | Created key ID |
| deletionDateTime | String | Time when key is deleted |

<a id="add-and-delete-credentials"></a>
## Add and Delete Credentials { #add-and-delete-credentials }
For authentication to protect user data, Secure Key Manager provides the following authentication methods: **IPv4 address authentication** to verify the client's IPv4 address, **MAC address authentication** to verify the client's MAC address, and **client certificate authentication** to verify the certificate the client uses to communicate.

<a id="add-credentials"></a>
### Add credentials { #add-credentials }
You can add credentials to Secure Key Manager.

<a id="add-credentials-add-ipv4-address"></a>
#### Add IPv4 address
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Name of the key store to store IPv4 addresses in |
| value | String | IPv4 address value |
| description | String | IPv4 address description |

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
| Name | Type | Description |
|---|---|---|
| value | String | Created IPv4 address value |
| description | String | Created IPv4 address description |

<a id="add-credentials-add-mac-address"></a>
#### Add MAC address
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name to store MAC addresses |
| value | String | MAC address value |
| description | String | MAC address description |

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
| Name | Type | Description |
|---|---|---|
| value | String | Created MAC address value |
| description | String | Created MAC address description |

<a id="add-credentials-add-certificate"></a>
#### Add Certificate
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name where the certificate is stored |
| name | String | Certificate name |
| password | String | Certificate password |
| lifeTime | int | Certificate use period (in days) |
| description | String | Certificate description |

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
| Name | Type | Description |
|---|---|---|
| name | String | Created certificate name |
| description | String | Created certificate description |

<a id="delete-credentials"></a>
### Delete Credentials { #delete-credentials }
You can change the status of credentials stored in Secure Key Manager to **To be deleted**, or **delete it immediately**.

<a id="delete-credentials-request-to-delete-credentials"></a>
#### Request to delete credentials
Change the credentials status to **To be deleted**.
The credentials is automatically deleted after 7 days, and you can't use the credentials in the **To be deleted** status.

<a id="delete-credentials-request-to-delete-an-ipv4-address"></a>
#### Request to delete an IPv4 address
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name to request the deletion of IPv4 address |
| value | String | IPv4 address value to request deletion |

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
| Name | Type | Description |
|---|---|---|
| value | String | IPv4 address value that requested deletion |
| deletionDateTime | String | Scheduled deletion time for IPv4 address |

<a id="delete-credentials-request-to-delete-mac-address"></a>
#### Request to delete MAC address
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name to request the deletion of MAC address |
| value | String | MAC address value to request deletion |

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
| Name | Type | Description |
|---|---|---|
| value | String | MAC address value that requested deletion |
| deletionDateTime | String | Scheduled deletion time for MAC address |

<a id="delete-credentials-request-to-delete-certificate"></a>
#### Request to delete certificate
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name to request the deletion of certificate |
| name | String | Certificate name to request deletion |

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
| Name | Type | Description |
|---|---|---|
| name | String | Certificate name that requested deletion |
| deletionDateTime | String | Scheduled deletion time for the certificate |

<a id="delete-credentials-immediately-delete-credentials"></a>
#### Immediately delete credentials
The key that is to be **deleted immediately** can only be **deleted immediately** in the status of **To be deleted**.
You cannot **immediately delete** a key that is activated.

<a id="delete-credentials-immediately-delete-ipv4"></a>
#### Immediately delete IPv4
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name to immediately delete IPv4 address |
| value | String | IPv4 address value to immediately delete |

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
| Name | Type | Description |
|---|---|---|
| value | String | Deleted IPv4 address value |
| deletionDateTime | String | Deletion time for IPv4 address |

<a id="delete-credentials-immediately-delete-mac-address"></a>
#### Immediately delete MAC address
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name to immediately delete MAC address |
| value | String | MAC address value to immediately delete |

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
| Name | Type | Description |
|---|---|---|
| value | String | Deleted MAC address value |
| deletionDateTime | String | Deletion time for MAC address |

<a id="delete-credentials-immediately-delete-certificate"></a>
#### Immediately delete certificate
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
| Name | Type | Description |
|---|---|---|
| keyStoreName | String | Key store name to immediately delete certificate |
| name | String | Certificate name to delete immediately |

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
| Name | Type | Description |
|---|---|---|
| name | String | Deleted certificate name |
| deletionDateTime | String | Deletion time for the certificate |

<a id="key-store"></a>
## Key Store { #key-store }

<a id="query-the-list-of-key-stores"></a>
### Query the List of Key stores { #query-the-list-of-key-stores }
Users can query the list of IDs for key stores created in Secure Key Manager.
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
| Name | Type | Description |
|---|---|---|
| keyStoreIdList | List | List of key store IDs |

<a id="retrieve-key-store-list-details"></a>
### Retrieve Key Store List Details { #retrieve-key-store-list-details }
You can retrieve a detailed list of key stores created in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores?detail={detail}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| detail | Boolean | Include details (default: false) |

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
                "name": "key store name",
                "description": "key store description",
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
| Name | Type | Description |
|---|---|---|
| keyStoreList | List | Key store list details |
| keyStoreId | Number | Key store ID |
| name | String | Key store name |
| description | String | Key store description |
| ip4AuthUse | String | Whether to use IPv4 authentication for the key store (Y/N) |
| macAuthUse | String | Whether to use MAC authentication for the key store (Y/N) |
| certificateAuthUse | String | Whether to use certificate authentication for the key store (Y/N) |
| creationUser | String | User who created the key store |
| creationDatetime | String | Creation date and time of the key store |
| lastChangeUser | String | User who last modified the key store |
| lastChangeDatetime | String | Last modification date and time of the key store |

<a id="query-the-details-of-the-key-store"></a>
### Query the Details of the Key Store { #query-the-details-of-the-key-store }
Users can query detailed information about the key store created in Secure Key Manager.
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
        "name": "Key store name",
        "description": "Key store description",
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
| Name | Type | Description |
|---|---|---|
| keyStoreId | Number | Key store ID |
| name | String | Key store name |
| description | String | Key store descriptions |
| ip4AuthUse | String | Whether IPv4 authentication is enabled for the key store or not (Y/N) |
| macAuthUse | String | Whether MAC authentication is enabled for the key store or not (Y/N) |
| certificateAuthUse | String | Whether the certificate authentication is enabled for the key store or not (Y/N) |
| creationUser | String | User who created the key store |
| creationDatetime | String | Key store creation date and time |
| lastChangeUser | String | Key store last modified user |
| lastChangeDatetime | String | Key store last modified date and time |

<a id="key"></a>
## Key { #key }

<a id="query-the-list-of-keys"></a>
### Query the List of Keys { #query-the-list-of-keys }
Users can query the list of key IDs created in Secure Key Manager.
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
| Name | Type | Description |
|---|---|---|
| keyIdList | List | Key ID list |

<a id="retrieve-key-list-details"></a>
### Retrieve Key List Details { #retrieve-key-list-details }
You can retrieve a detailed list of keys created in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/keys?detail={detail}&type={type}&name={name}&status={status}&pageNumber={pageNumber}&pageSize={pageSize}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| detail | Boolean | Whether to include detailed information (default: false) |
| type | String | Key type filter (SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY, default: all, multiple selections not allowed) |
| name | String | Key name filter (maximum 100 characters) |
| status | String | Key status filter (active/inactive, default: all) |
| pageNumber | Number | Page number (default: 1, must be a positive integer) |
| pageSize | Number | Page size (default: 10, 10-100) |

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
                "name": "key name",
                "description": "key description",
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
| Name | Type | Description |
|---|---|---|
| keyList | List | Key list details |
| keyId | String | Key ID |
| name | String | Key name |
| description | String | Key description |
| keyType | String | Key type (SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY) |
| currentKeyValueVersion | Number | Current key version |
| autoRotationPeriod | Number | Key rotation period |
| nextAutoRotationDate | String | Next scheduled key rotation date |
| lastAccessDatetime | String | Last accessed date and time of the key |
| deletionDatetime | String | Scheduled deletion date and time of the key |
| creationUser | String | User who created the key |
| creationDatetime | String | Creation date and time of the key |
| lastChangeUser | String | User who last modified the key |
| lastChangeDatetime | String | Last modification date and time of the key |

<a id="query-the-details-of-keys"></a>
### Query the details of keys { #query-the-details-of-keys }
Users can query detailed information about the key created in Secure Key Manager.
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
        "name": "Key name",
        "description": "Key descriptions",
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
| Name | Type | Description |
|---|---|---|
| keyId | String | Key ID |
| name | String | Key name |
| description | String | Key descriptions |
| keyType | String | Key type(SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY) |
| currentKeyValueVersion | Number | Current key version |
| autoRotationPeriod | Number | Key rotation cycle |
| nextAutoRotationDate | String | Key next rotation date |
| lastAccessDatetime | String | Key last used date and time |
| creationUser | String | User who created the key |
| creationDatetime | String | Key creation date and time |
| lastChangeUser | String | Key last modified user |
| lastChangeDatetime | String | Key last modified date and time |

<a id="authentication-information"></a>
## Authentication Information { #authentication-information }

<a id="query-the-list-of-ipv4-authentication-information"></a>
### Query the List of IPv4 Authentication Information { #query-the-list-of-ipv4-authentication-information }
Users can query the list of IPv4 authentication information in the key store configured in Secure Key Manager.
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
| Name | Type | Description |
|---|---|---|
| ipv4List | List | IPv4 authentication information list |

<a id="query-the-details-of-ipv4-authentication-information"></a>
### Query the details of IPv4 Authentication Information { #query-the-details-of-ipv4-authentication-information }
Users can query detailed information about the IPv4 authentication in the key store configured in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| ipv4Value | String | IPv4 address to query |

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
                "description": "IPv4 descriptions",
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
| Name | Type | Description |
|---|---|---|
| ipv4List | List | IPv4 authentication information list |
| value | String | IPv4 value |
| description | String | IPv4 descriptions |
| lastAccessDatetime | String | IPv4 last used date and time |
| deletionDatetime | String | IPv4 deletion scheduled date and time |
| creationUser | String | User who created the IPv4 |
| creationDatetime | String | IPv4 creation date and time |
| lastChangeUser | String | IPv4 last modified user |
| lastChangeDatetime | String | IPv4 last modified date and time |

<a id="query-the-list-of-mac-authentication-information"></a>
### Query the List of MAC Authentication Information { #query-the-list-of-mac-authentication-information }
Users can query the list of MAC authentication information in the key store configured in Secure Key Manager.
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
| Name | Type | Description |
|---|---|---|
| macList | List | MAC authentication information list |

<a id="query-the-details-of-mac-authentication-information"></a>
### Query the details of MAC Authentication Information { #query-the-details-of-mac-authentication-information }
Users can query detailed information about the MAC authentication in the key store configured in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| macValue | String | MAC address to query |

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
                "description": "MAC descriptions",
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
| Name | Type | Description |
|---|---|---|
| macList | List | MAC authentication information list |
| value | String | MAC value |
| description | String | MAC descriptions |
| lastAccessDatetime | String | MAC last used date and time |
| deletionDatetime | String | MAC deletion scheduled date and time |
| creationUser | String | User who created the MAC |
| creationDatetime | String | MAC creation date and time |
| lastChangeUser | String | MAC last modified user |
| lastChangeDatetime | String | MAC last modified date and time |

<a id="query-the-list-of-certificate-authentication-information"></a>
### Query the List of Certificate Authentication Information { #query-the-list-of-certificate-authentication-information }
Users can query the list of the certifacate authentication information in the key store configured in Secure Key Manager.
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
| Name | Type | Description |
|---|---|---|
| certificateList | List | Certifacate authentication information list |

<a id="query-the-details-of-certifacate-authentication-information"></a>
### Query the details of Certifacate Authentication Information { #query-the-details-of-certifacate-authentication-information }
Users can query detailed information about the certifacate authentication in the key store configured in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| certificateName | String | Certificate name to query |

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
                "description": "Certificate descriptions",
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
| Name | Type | Description |
|---|---|---|
| certificateList | List | Certificate authentication information list |
| name | String | Certificate name |
| password | String | Certificate password |
| description | String | Certificate descriptions |
| lastAccessDatetime | String | Certificate last used date and time |
| deletionDatetime | String | Certificate deletion scheduled date and time |
| creationUser | String | User who created the certificate |
| creationDatetime | String | Certificate creation date and time |
| lastChangeUser | String | Certificate last modified user |
| lastChangeDatetime | String | Certificate last modified date and time |