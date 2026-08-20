<!-- pre-align:aligned sig=68657d3daf9d -->

<a id="security-secure-key-manager-api-v13-guide"></a>
## Security > Secure Key Manager > API v1.3 Guide { #security-secure-key-manager-api-v13-guide }

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

Secure Key Manager API v1.3 supports Appkey, Project-integrated Appkey, and User Access Key token as authentication methods for API calls.

Appkey is included in the request URL when calling the API to identify and point to a specific resource. Alternatively, a Project-integrated Appkey can be used in place of Appkey.
A User Access Key token is a temporary, Bearer-type access token issued from a User Access Key, used for authentication and authorization when calling the API.

For more information on how to check and use each authentication method, see [Appkey](/nhncloud/en/public-api/appkey), [Project Integrated Appkey](/nhncloud/en/public-api/project-integrated-appkey), and [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

<a id="api-list"></a>
### API List { #api-list }

| Method | URI | Description |
| ------ | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| GET | /keymanager/v1.3/appkey/{appkey}/confirm | Provide information of the client that called API. |
| GET | /keymanager/v1.3/appkey/{appkey}/secrets/{keyid} | Query confidential data stored in Secure Key Manager. |
| PUT | /keymanager/v1.3/appkey/{appkey}/secrets/{keyid} | Update confidential data stored in Secure Key Manager. |
| POST | /keymanager/v1.3/appkey/{appkey}/symmetric-keys/{keyid}/encrypt | Encrypt data with the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.3/appkey/{appkey}/symmetric-keys/{keyid}/decrypt | Decrypt data with the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.3/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key | Create AES-256 symmetric keys that can be used by a client for data encryption/decryption in local environment. |
| GET | /keymanager/v1.3/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key | Query the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/sign | Sign data with the asymmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/verify | Verify data and signature with the asymmetric key stored in Secure Key Manager. |
| POST   | /keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/sign-standard                       | Signs data according to the standard scheme (RSASSA-PSS, RSASSA-PKCS1-v1_5) using the asymmetric key stored in Secure Key Manager. |
| POST   | /keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/verify-standard                     | Verifies data and a signature according to the standard scheme (RSASSA-PSS, RSASSA-PKCS1-v1_5) using the asymmetric key stored in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey | Query the private key stored in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey | Query the public key stored in Secure Key Manager. |
| POST | /keymanager/v1.3/appkey/{appkey}/keys/{secrets\|symmetric-keys\|asymmetric-keys}/create | Add a new key to Secure Key Manager. |
| PUT | /keymanager/v1.3/appkey/{appkey}/keys/{keyid}/delete | Request deletion of a key stored in Secure Key Manager. |
| DELETE | /keymanager/v1.3/appkey/{appkey}/keys/{keyid} | Immediately delete the key scheduled for deletion in Secure Key Manager. |
| POST | /keymanager/v1.3/appkey/{appkey}/auths/{ipv4s\|macs\|certificates} | Add credentials to Secure Key Manager. |
| PUT | /keymanager/v1.3/appkey/{appkey}/auths/{ipv4s\|macs\|certificates}/delete | Request deletion of credentials in Secure Key Manager. |
| POST | /keymanager/v1.3/appkey/{appkey}/auths/{ipv4s\|macs\|certificates}/delete | Immediately delete credentials in Secure Key Manager. |
| POST   | /keymanager/v1.3/appkey/{appkey}/keystores                                                   | Create a key store in Secure Key Manager.                                               |
| PUT    | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}                                      | Modify a key store stored in Secure Key Manager.                                        |
| DELETE | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}                                      | Delete or disable a key store stored in Secure Key Manager.                              |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores | Query the key stores in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId} | Query the details of the key stores in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/keys | Query the keys of the key stores in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/keys/{keyId} | Query the key details of the key stores in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/ips | Retrieve a list of IPv4 authentication entries from a key store in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value} | Retrieve details of an IPv4 authentication entry from a key store in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/macs | Retrieve a list of MAC authentication entries from a key store in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue} | Retrieve details of a MAC authentication entry from a key store in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/certificates | Retrieve a list of certificate authentication entries from a key store in Secure Key Manager. |
| GET | /keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName} | You can retrieve the credential details of key stores stored in Secure Key Manager. |

[HTTP Header of API Request]

To use MAC address authentication of Secure Key Manager, you must make a request by setting the client's MAC address in the HTTP header.

```
X-TOAST-CLIENT-MAC-ADDR: {MAC addess}
```

[Path Variables of API Request]

| Name | Type | Description |
| ------ | ------ | ----------------------------------------------------------- |
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
| ------------- | ------- | -------------------- |
| resultCode | Number | Result code value of API call |
| resultMessage | String | Result message of API call |
| isSuccessful | Boolean | Whether API call is successful or not |

<a id="query-client-information"></a>
## Query Client Information { #query-client-information }

This API is used to query information of the client that called API.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/confirm
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
| --------------------- | ------- | ------------------------------------------------------- |
| clientIp | String | IP address of the client that called API |
| clientMacHeader | String | Header value of MAC address of the client that called API |
| clientSentCertificate | Boolean | Whether the client that called API is using certificate or not |

<a id="confidential-data"></a>
## Confidential Data { #confidential-data }

<a id="query-confidential-data"></a>
### Query Confidential Data { #query-confidential-data }

This API is used to query confidential data stored in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/secrets/{keyid}
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
| ------ | ------ | --------------------- |
| secret | String | Query result of confidential data |

<a id="modify-a-confidential-data"></a>
### Modify a Confidential Data { #modify-a-confidential-data }

This API is used to modify confidential data stored in Secure Key Manager.

```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/secrets/{keyid}
```

[Request Body]

```
{
    "secretValue": "data"
}
```

| Name | Type | Description |
| ----------- | ------ | ----------------------- |
| secretValue | String | Confidential data to be changed |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyId": "071dcc5c25614dffa52357e5cae3471f",
        "name": "key name",
        "description": "key description",
        "secretValue": "data",
        "creationUser": "SECURE_KEY_MANAGER",
        "creationDatetime": "2025-01-25T12:00:00",
        "lastChangeUser": "SECURE_KEY_MANAGER",
        "lastChangeDatetime": "2025-01-30T15:00:00.000"
    }
}
```

| Name | Type | Description |
| ------------------ | ------ | ----------------------- |
| keyId | String | Key ID |
| name | String | Key name |
| description | String | Key description |
| secretValue | String | Updated confidential data |
| creationUser | String | Key creator |
| creationDatetime | String | Key creation date and time |
| lastChangeUser | String | Key last modified by |
| lastChangeDatetime | String | Key last modified date and time |

<a id="symmetric-keys"></a>
## Symmetric Keys { #symmetric-keys }

<a id="encrypt-symmetric-keys"></a>
### Encrypt Symmetric Keys { #encrypt-symmetric-keys }

This API is used to encrypt data with a symmetric key created in Secure Key Manager. Users can encrypt text data up to 32KB by passing it to Secure Key Manager, which performs the encryption using the stored symmetric key.

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/symmetric-keys/{keyid}/encrypt
```

[Request Body]

```
{
    "plaintext": "data"
}
```

| Name | Type | Description |
| --------- | ------ | ------------------------- |
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
| ---------- | ------ | ----------------------------------- |
| ciphertext | String | Result of data encryption with the symmetric key |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

<a id="decrypt-symmetric-keys"></a>
### Decrypt Symmetric Keys { #decrypt-symmetric-keys }

This API is used to decrypt data with a symmetric key created in Secure Key Manager. Users can decrypt encrypted text by passing it to Secure Key Manager, which performs the decryption using the stored symmetric key.

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/symmetric-keys/{keyid}/decrypt
```

[Request Body]

```
{
    "ciphertext": "AAAAABzGwQniNneKXmcOLhWnxEqC1rNY+UdVb3lyeX/4wSrP"
}
```

| Name | Type | Description |
| ---------- | ------ | ------------------------- |
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
| ---------- | ------ | ----------------------------------- |
| plaintext | String | Result of data decryption with the symmetric key |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

<a id="generate-local-symmetric-keys-encrypted-with-the-symmetric-key"></a>
### Generate Local Symmetric Keys Encrypted with the Symmetric Key { #generate-local-symmetric-keys-encrypted-with-the-symmetric-key }

This API is used to generate an AES-256 symmetric key that clients can use in their local environment. localKeyPlaintext is the generated symmetric key in Base64-encoded form and can be used directly after Base64 decoding. localKeyCiphertext is the generated symmetric key encrypted with the symmetric key stored in Secure Key Manager and then Base64-encoded, and is used when saving to storage. The symmetric key saved to storage can be used after being decrypted with the decryption API..

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key
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
| ------------------ | ------ | --------------------------------------------------------------------------------- |
| localKeyPlaintext | String | Base64-encoded AES-256 symmetric key |
| localKeyCiphertext | String | Base64-encoded AES-256 symmetric key encrypted with the symmetric key stored in Secure Key Manager |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

<a id="query-the-symmetric-key"></a>
### Query the Symmetric Key { #query-the-symmetric-key }

Users can query the symmetric key (AES-256) stored in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key?keyVersion={keyVersion}
```

[Request Parameter]

| Name | Type | Description |
| ---------- | ------ | ------------------- |
| keyVersion | Number | Version of the symmetric key to query |

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
| ------------ | ------ | ----------------------------------- |
| symmetricKey | String | Symmetric key data (Hex string form) |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

<a id="asymmetric-key"></a>
## Asymmetric Key { #asymmetric-key }

<a id="sign-with-the-asymmetric-key"></a>
### Sign with the Asymmetric Key { #sign-with-the-asymmetric-key }

This API is used to sign data with the asymmetric key created in Secure Key Manager. Users can pass 245 Byte or smaller text data, and the data is signed with the asymmetric key stored in Secure Key Manager.

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/sign
```

[Request Body]

```
{
    "plaintext": "data"
}
```

| Name | Type | Description |
| --------- | ------ | ------------------------- |
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
| ---------- | ------ | ------------------------------------- |
| signature | String | Signature value of signing the data with the asymmetric key |
| keyVersion | Number | Version of the asymmetric key used for processing the API request |

<a id="verify-data-with-the-asymmetric-key"></a>
### Verify Data with the Asymmetric Key { #verify-data-with-the-asymmetric-key }

This API is used to verify data with the asymmetric key created in Secure Key Manager. Users can pass data and signature value, and use asymmetric keys stored in Secure Key Manager to verify that data has not been forged.

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/verify
```

[Request Body]

```
{
    "plaintext": "data",
    "signature": "AAAAAGI9zf831DX..."
}
```

| Name | Type | Description |
| --------- | ------ | ---------------------------------- |
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
| ---------- | ------- | ----------------------------------------- |
| result | Boolean | Result of verifying data and signature value with the asymmetric key |
| keyVersion | Number | Version of the asymmetric key used for processing the API request |

<a id="sign-with-asymmetric-key-standard-scheme"></a>
### Sign with Asymmetric Key (Standard Scheme) { #sign-with-asymmetric-key-standard-scheme }

Used to sign data according to the standard RSA signing scheme (RSASSA-PSS, RSASSA-PKCS1-v1_5) using the asymmetric key created in Secure Key Manager. Users can sign data with the asymmetric key stored in Secure Key Manager by providing Base64-encoded data and a signing scheme.

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/sign-standard
```

[Request Body]

```
{
    "plaintext": "Base64(...)",
    "algorithm": "RSASSA-PSS"
}
```

| Name      | Type   | Description                                                          |
| --------- | ------ | --------------------------------------------------------------------- |
| plaintext | String | Base64-encoded string of the data to sign. Up to 64 KB after decoding |
| algorithm | String | Signing scheme. One of RSASSA-PSS or RSASSA-PKCS1-v1_5 |

[Response Body]

RSASSA-PSS

```
{
    "header": {
        ...
    },
    "body": {
        "signature": "Base64(...)",
        "algorithm": "RSASSA-PSS",
        "hashAlgorithm": "SHA-256",
        "mgfAlgorithm": "MGF1-SHA-256",
        "saltLength": 32,
        "keyVersion": 0
    }
}
```

RSASSA-PKCS1-v1_5

```
{
    "header": {
        ...
    },
    "body": {
        "signature": "Base64(...)",
        "algorithm": "RSASSA-PKCS1-v1_5",
        "hashAlgorithm": "SHA-256",
        "keyVersion": 0
    }
}
```

| Name          | Type   | Description                                                |
| ------------- | ------ | ---------------------------------------------------------- |
| signature     | String | Signature value of the data signed with the asymmetric key (Base64-encoded) |
| algorithm     | String | Scheme used for signing. Same as the request value |
| hashAlgorithm | String | Hash algorithm used for signing. Fixed value: SHA-256 |
| mgfAlgorithm  | String | MGF algorithm. Fixed value: MGF1-SHA-256 (RSASSA-PSS only) |
| saltLength    | Number | Salt length (bytes). Fixed value: 32 (RSASSA-PSS only) |
| keyVersion    | Number | Version of the asymmetric key used to process the API request |

<a id="verify-data-with-asymmetric-key-standard-scheme"></a>
### Verify Data with Asymmetric Key (Standard Scheme) { #verify-data-with-asymmetric-key-standard-scheme }

Used to verify data and a signature according to the standard RSA signing scheme (RSASSA-PSS, RSASSA-PKCS1-v1_5) using the asymmetric key created in Secure Key Manager. Users can verify that the data has not been forged or tampered with using the asymmetric key stored in Secure Key Manager by providing Base64-encoded data, a signature value, a signing scheme, and a key version.

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/verify-standard
```

[Request Body]

```
{
    "plaintext": "Base64(...)",
    "signature": "Base64(...)",
    "algorithm": "RSASSA-PSS",
    "keyVersion": 0
}
```

| Name       | Type   | Description                                                          |
| ---------- | ------ | --------------------------------------------------------------------- |
| plaintext  | String | Base64-encoded string of the data to verify. Up to 64 KB after decoding |
| signature  | String | Base64-encoded string of the signature value to verify |
| algorithm  | String | Signing scheme. One of RSASSA-PSS or RSASSA-PKCS1-v1_5 |
| keyVersion | Number | Version of the asymmetric key to use for verification |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "result": true,
        "keyVersion": 0
    }
}
```

| Name       | Type    | Description                                      |
| ---------- | ------- | ------------------------------------------------ |
| result     | Boolean | Result of verifying the data and signature value with the asymmetric key |
| keyVersion | Number  | Version of the asymmetric key used to process the API request |

<a id="query-the-private-key"></a>
### Query the Private Key { #query-the-private-key }

Users can query the private key among the asymmetric keys stored in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey?keyVersion={keyVersion}
```

[Request Parameter]

| Name | Type | Description |
| ---------- | ------ | --------------------- |
| keyVersion | Number | Version of the asymmetric key to query |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PrivateKey",
        "key": "0x30, 0x82, 0x04, 0xbe, 0x02, 0x01, 0x00, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x04, 0x82, 0x04, 0xa8, 0x30, 0x82, 0x04, 0xa4, 0x02, 0x01, 0x00, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2,
                ... (omitted) ...",
        "encodedKey": "MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCLB47ax4OVyEOnuDFv9iU2iWTFOHVLpoD+fMVqlPJiiuJSwi5x/zd3LojWuUyr+dZ9Icxl23Alu4GwwKgUi4DL8qo8jD14THJoeUgIZ56wmYMvN+CkNnmkyqcGn6yT+AXtBJVGqS/2lssHLIGELi8XXkWdf6OBfig6HgsJAnix8Z+T/QdikEFUI5ZiuUWyHw2Bag9B4CoPF2EgXfu5HcW4GA4KH2PI92O4vNg8AmFVDk2E+ma2quSau7LjS3KY9s3Sq+JqvTPZmqHQJudv9ZYcnbyDG/
                       ... (omitted) ...",
        "keyVersion": 0
    }
}
```

| Name | Type | Description |
| ---------- | ------ | ------------------------------------- |
| keyType | String | Asymmetric key form |
| key | String | Private key data (Hex string form) |
| encodedKey | String | Private key data (base64 endoing form) |
| keyVersion | Number | Version of the asymmetric key used for processing the API request |

<a id="query-the-public-key"></a>
### Query the Public Key { #query-the-public-key }

Users can query the private key among the asymmetric keys stored in Secure Key Manager.
It can be retrieved regardless of authentication.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey?keyVersion={keyVersion}
```

[Request Parameter]

| Name | Type | Description |
| ---------- | ------ | --------------------- |
| keyVersion | Number | Version of the asymmetric key to query |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PublicKey",
        "key": "0x30, 0x82, 0x01, 0x22, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x03, 0x82, 0x01, 0x0f, 0x00, 0x30, 0x82, 0x01, 0x0a, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2, 0x62, 0x8a, 0xe2, 0x52, 0xc2,
                ... (omitted) ...",
        "encodedKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAiweO2seDlchDp7gxb/YlNolkxTh1S6aA/nzFapTyYoriUsIucf83dy6I1rlMq/nWfSHMZdtwJbuBsMCoFIuAy/KqPIw9eExyaHlICGeesJmDLzfgpDZ5pMqnBp+sk/gF7QSVRqkv9pbLByyBhC4vF15FnX+jgX4oOh4LCQJ4sfGfk/0HYpBBVCOWYrlFsh8NgWoPQeAqDxdhIF37uR3FuBgOCh9jyPdjuLzYPAJhVQ5NhPpmtqrkmruy40tymPbN0qviar0z2Zqh0Cbnb/WWHJ28gxv+d+iJCXJvm+fIg7hRYJ5C+mun/N6FB8QHv/
                       ... (omitted) ...",
        "keyVersion": 0
    }
}
```

| Name | Type | Description |
| ---------- | ------ | ------------------------------------- |
| keyType | String | Asymmetric key form |
| key | String | Public key data (Hex string form) |
| encodedKey | String | Public key data (base64 endoing form) |
| keyVersion | Number | Version of the asymmetric key used for processing the API request |

<a id="adddelete-keys"></a>
## Add/Delete Keys { #adddelete-keys }

<a id="add-keys"></a>
### Add Keys { #add-keys }

Add a new key to Secure Key Manager.

<a id="add-keys-add-confidential-data"></a>
#### Add Confidential Data

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keys/secrets/create
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
| ------------ | ------ | -------------------------- |
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
| --------- | ------ | -------------- |
| keyId | String | Created key ID |
| keyStatus | String | Key status message |

<a id="add-keys-add-a-symmetric-key"></a>
#### Add a Symmetric Key

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keys/symmetric-keys/create
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
| ------------------ | ------ | -------------------------- |
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
| --------- | ------ | -------------- |
| keyId | String | Created key ID |
| keyStatus | String | Key status message |

<a id="add-keys-add-a-asymmetric-key"></a>
#### Add a Asymmetric Key

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keys/asymmetric-keys/create
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

| Name | Type | Description |
| ------------------ | ------ | -------------------------- |
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
| --------- | ------ | -------------- |
| keyId | String | Created key ID |
| keyStatus | String | Key status message |

<a id="delete-a-key"></a>
### Delete a Key { #delete-a-key }

You can change the status of the key stored in the Secure Key Manager to **Pending Deletion** or **Immediate Delete** it.

<a id="delete-a-key-request-to-delete-a-key"></a>
#### Request to Delete a Key

Change the key status to **Pending Deletion**.
The key will be automatically deleted in 7 days, and the key with **Pending Deletion** status cannot be queried.

```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keys/{keyid}/delete
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
| ---------------- | ------ | -------------- |
| keyId | String | Created key ID |
| deletionDateTime | String | Date when key is to be deleted |

<a id="delete-a-key-immediately-delete-a-key"></a>
#### Immediately Delete a Key

A key must be in the **Pending Deletion** state to perform an **Immediate Delete**
Keys in the active state are not eligible for **Immediate Delete**.

```text
DELETE https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keys/{keyid}
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
| ---------------- | ------ | ------------ |
| keyId | String | Created key ID |
| deletionDateTime | String | Time when key is deleted |

<a id="add-and-delete-credentials"></a>
## Add and Delete Credentials { #add-and-delete-credentials }

Secure Key Manager provides the following authentication methods to protect user data: **IPv4 Address Authentication**, which verifies the client's IPv4 address; **MAC Address Authentication**, which verifies the client's MAC address; and **Client Certificate Authentication**, which verifies the certificate the client uses for communication.

<a id="add-credentials"></a>
### Add Credentials { #add-credentials }

You can add credentials to Secure Key Manager.

<a id="add-credentials-add-a-ipv4-address"></a>
#### Add a IPv4 Address

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/auths/ipv4s
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
| ------------ | ------ | --------------------------------- |
| keyStoreName | String | Key store name to store IPv4 address |
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
| ----------- | ------ | --------------------- |
| value | String | Created IPv4 address value |
| description | String | Created IPv4 address description |

<a id="add-credentials-add-a-mac-address"></a>
#### Add a MAC Address

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/auths/macs
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
| ------------ | ------ | -------------------------------- |
| keyStoreName | String | Key store name to store MAC address |
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
| ----------- | ------ | -------------------- |
| value | String | Created MAC address value |
| description | String | Created MAC address description |

<a id="add-credentials-add-certificates"></a>
#### Add Certificates

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/auths/certificates
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
| ------------ | ------ | ------------------------------ |
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
| ----------- | ------ | ------------------ |
| name | String | Created certificate name |
| description | String | Created certificate description |

<a id="delete-credentials"></a>
### Delete Credentials { #delete-credentials }

You can change the status of the credentials stored in the Secure Key Manager to **Pending Deletion** or **Immediate Delete** it.

<a id="delete-credentials-request-to-delete-the-credentials"></a>
#### Request to Delete the Credentials

Change the credentials to **Pending Deletion**.
The information will be automatically deleted in 7 days, and the key with **Pending Deletion** status cannot be queried.

<a id="delete-credentials-request-to-delete-an-ipv4-address"></a>
#### Request to Delete an IPv4 Address

```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/auths/ipv4s/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "127.0.0.1"
}
```

| Name | Type | Description |
| ------------ | ------ | -------------------------------------- |
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
| ---------------- | ------ | -------------------------- |
| value | String | IPv4 address value that requested deletion |
| deletionDateTime | String | Scheduled deletion time for IPv4 address |

<a id="delete-credentials-request-to-delete-mac-address"></a>
#### Request to Delete MAC Address

```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/auths/macs/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "aa:aa:aa:aa:aa:aa"
}
```

| Name | Type | Description |
| ------------ | ------ | ------------------------------------- |
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
| ---------------- | ------ | ------------------------- |
| value | String | MAC address value that requested deletion |
| deletionDateTime | String | Scheduled deletion time for MAC address |

<a id="delete-credentials-request-to-delete-certificate"></a>
#### Request to Delete Certificate

```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/auths/certificates/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "name" : "Certificate Name #1"
}
```

| Name | Type | Description |
| ------------ | ------ | ----------------------------------- |
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
| ---------------- | ------ | ----------------------- |
| name | String | Certificate name that requested deletion |
| deletionDateTime | String | Scheduled deletion time for the certificate |

<a id="delete-credentials-immediately-delete-credentials"></a>
#### Immediately Delete Credentials

Credentials must be in the **Pending Deletion** state before they can be **immediately deleted**.
Credentials in the active state cannot be **immediately deleted**.

<a id="delete-credentials-immediately-delete-ipv4-address"></a>
#### Immediately Delete IPv4 Address

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/auths/ipv4s/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "127.0.0.1"
}
```

| Name | Type | Description |
| ------------ | ------ | -------------------------------------- |
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
| ---------------- | ------ | --------------------- |
| value | String | Deleted IPv4 address value |
| deletionDateTime | String | Deletion time for IPv4 address |

<a id="delete-credentials-immediately-delete-mac-address"></a>
#### Immediately Delete MAC Address

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/auths/macs/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "value" : "aa:aa:aa:aa:aa:aa"
}
```

| Name | Type | Description |
| ------------ | ------ | ------------------------------------- |
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
| ---------------- | ------ | -------------------- |
| value | String | Deleted MAC address value |
| deletionDateTime | String | Deletion time for MAC address |

<a id="delete-credentials-immediately-delete-certificate"></a>
#### Immediately Delete Certificate

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/auths/certificates/delete
```

[Request Body]

```
{
    "keyStoreName" : "Store #1",
    "name" : "Certificate Name #1"
}
```

| Name | Type | Description |
| ------------ | ------ | ----------------------------------- |
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
| ---------------- | ------ | ------------------ |
| name | String | Deleted certificate name |
| deletionDateTime | String | Deletion time of certificate |

<a id="key-store"></a>
## Key Store { #key-store }

<a id="create-key-store"></a>
### Create Key Store { #create-key-store }

Creates a key store in Secure Key Manager.

```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores
```

[Request Body]

```
{
    "name": "myKeyStore",
    "description": "Custom description",
    "ip4AuthUse": "Y",
    "macAuthUse": "N",
    "certificateAuthUse": "N",
    "authMode": "AND"
}
```

| Name               | Type   | Description                                                                                       |
| ------------------ | ------ | ------------------------------------------------------------------------------------------ |
| name               | String | Key store name (required, 1–100 characters)                                                              |
| description        | String | Key store description (up to 1,000 characters)                                                                |
| ip4AuthUse         | String | Whether to use IPv4 authentication (Y/N); at least one of ip4AuthUse/macAuthUse/certificateAuthUse must be Y         |
| macAuthUse         | String | Whether to use MAC authentication (Y/N)                                                                    |
| certificateAuthUse | String | Whether to use certificate authentication (Y/N)                                                                 |
| authMode           | String | Authentication combination method (required, AND/OR, default: AND)                                                  |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "keyStoreId": 12345,
        "name": "myKeyStore",
        "description": "Custom description",
        "ip4AuthUse": "Y",
        "macAuthUse": "N",
        "certificateAuthUse": "N",
        "authMode": "AND"
    }
}
```

| Name               | Type   | Description                                 |
| ------------------ | ------ | ------------------------------------ |
| keyStoreId         | Number | ID of the created key store                  |
| name               | String | Key store name                       |
| description        | String | Key store description                |
| ip4AuthUse         | String | Whether the key store uses IPv4 authentication (Y/N)   |
| macAuthUse         | String | Whether the key store uses MAC authentication (Y/N)    |
| certificateAuthUse | String | Whether the key store uses certificate authentication (Y/N) |
| authMode           | String | Authentication combination method (AND/OR)               |

<a id="update-key-store"></a>
### Update Key Store { #update-key-store }

Updates a key store stored in Secure Key Manager.

```text
PUT https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}
```

[Request Body]

```
{
    "name": "renamedKeyStore",
    "description": "Updated description",
    "ip4AuthUse": "Y",
    "macAuthUse": "Y",
    "certificateAuthUse": "N",
    "authMode": "OR"
}
```

| Name               | Type   | Description                                                                                       |
| ------------------ | ------ | ------------------------------------------------------------------------------------------ |
| name               | String | Key store name (required, 1–100 characters)                                                              |
| description        | String | Key store description (up to 1,000 characters)                                                                |
| ip4AuthUse         | String | Whether to use IPv4 authentication (Y/N); at least one of ip4AuthUse/macAuthUse/certificateAuthUse must be Y         |
| macAuthUse         | String | Whether to use MAC authentication (Y/N)                                                                    |
| certificateAuthUse | String | Whether to use certificate authentication (Y/N)                                                                 |
| authMode           | String | Authentication combination method (required, AND/OR, default: AND)                                                  |

[Response Body]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "success"
    },
    "body": null
}
```

<a id="delete-key-store"></a>
### Delete Key Store { #delete-key-store }

Deletes (deactivates) a key store stored in Secure Key Manager.

```text
DELETE https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}
```

[Response Body]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "success"
    },
    "body": null
}
```

<a id="retrieve-a-key-store-list"></a>
### Retrieve a Key Store List { #retrieve-a-key-store-list }

You can retrieve the ID list of key stores created in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores
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
| -------------- | ---- | ----------------- |
| keyStoreIdList | List | Key store ID list |

<a id="view-key-store-list-details"></a>
### View Key Store List Details { #view-key-store-list-details }

You can view detailed information on the list of key stores created in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores?detail={detail}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| detail | Boolean | Details included or not (Default: false) |

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
                "name": "Key store name",
                "description": "Key store description",
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
| ------------------ | ------ | ------------------------------------ |
| keyStoreList | List | List of key store details |
| keyStoreId | Number | Key store ID |
| name | String | Key store name |
| description | String | Key store description |
| ip4AuthUse | String | Key store IPv4 authentication enabled (Y/N) |
| macAuthUse | String | Key store MAC authentication enabled (Y/N) |
| certificateAuthUse | String | Key store certificate authentication enabled (Y/N) |
| creationUser | String | Key store creator |
| creationDatetime | String | Key store creation date and time |
| lastChangeUser | String | Key store last modified by |
| lastChangeDatetime | String | Key store last modified date and time |

<a id="view-key-store-details"></a>
### View Key Store Details { #view-key-store-details }

You can view detailed information on a key store created in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}
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
| ------------------ | ------ | ------------------------------------ |
| keyStoreId | Number | Key store ID |
| name | String | Key store name |
| description | String | Key store description |
| ip4AuthUse | String | Key store IPv4 authentication enabled (Y/N) |
| macAuthUse | String | Key store MAC authentication enabled (Y/N) |
| certificateAuthUse | String | Key store certificate authentication enabled (Y/N) |
| creationUser | String | Key store creator |
| creationDatetime | String | Key store creation date and time |
| lastChangeUser | String | Key store last modified by |
| lastChangeDatetime | String | Key store last modified date and time |

<a id="key"></a>
## Key { #key }

<a id="view-key-list"></a>
### View Key List { #view-key-list }

You can view detailed information on a key ID list created in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/keys
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
| --------- | ---- | ---------- |
| keyIdList | List | Key ID list |

<a id="view-key-list-details"></a>
### View Key List Details { #view-key-list-details }

You can retrieve a detailed list of keys created in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/keys?detail={detail}&type={type}&name={name}&status={status}&pageNumber={pageNumber}&pageSize={pageSize}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| detail | Boolean | Include details (default: false) |
| type | String | Key type filter (SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY, default: all, no multiple selections allowed) |
| name | String | Key name filter (maximum 100 characters) |
| status | String | Key status filter (active/inactive, default: all) |
| pageNumber | Number | Page number (default: 1, positive integer) |
| pageSize | Number | Page size (default: 10, 10 to 100) |

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
                "name": "Key name",
                "description": "Key description",
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
| ---------------------- | ------ | -------------------------------------------- |
| keyList | List | Key Details List |
| keyId | String | Key ID |
| name | String | Key name |
| description | String | Key description |
| keyType | String | Key type (SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY) |
| currentKeyValueVersion | Number | Current key version |
| autoRotationPeriod | Number | Key rotation period |
| nextAutoRotationDate | String | Next key rotation date |
| lastAccessDatetime | String | Key last access date |
| deletionDatetime | String | Key scheduled deletion date |
| creationUser | String | Key creator |
| creationDatetime | String | Key creation date and time |
| lastChangeUser | String | Key last modified by |
| lastChangeDatetime | String | Key last modified date and time |

<a id="view-key-details"></a>
### View Key Details { #view-key-details }

You can view the detailed key information created in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/keys/{keyId}
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
        "description": "Key description",
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
| ---------------------- | ------ | -------------------------------------------- |
| keyId | String | Key ID |
| name | String | Key name |
| description | String | Key description |
| keyType | String | Key type(SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY) |
| currentKeyValueVersion | Number | Current key version |
| autoRotationPeriod | Number | Key rotation period |
| nextAutoRotationDate | String | Next key rotation date |
| lastAccessDatetime | String | Key last access date |
| creationUser | String | Key creator |
| creationDatetime | String | Key creation date and time |
| lastChangeUser | String | Key last modified by |
| lastChangeDatetime | String | Key last modified date and time |

<a id="credentials"></a>
## Credentials { #credentials }

<a id="view-ipv4-credential-list"></a>
### View IPv4 Credential List { #view-ipv4-credential-list }

You can view the list of IPv4 credentials configured for a key store in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/ips
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
| -------- | ---- | ------------------- |
| ipv4List | List | IPv4 credential list |

<a id="view-ipv4-credential-details"></a>
### View IPv4 Credential Details { #view-ipv4-credential-details }

You can view detailed information on an IPv4 credential configured for a key store in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value}
```

[Request Parameter]

| Name | Type | Description |
| --------- | ------ | ---------------- |
| ipv4Value | String | IPv4 address to retrieve |

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
                "description": "IPv4 description",
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
| ------------------ | ------ | --------------------- |
| ipv4List | List | IPv4 authentication information list |
| value | String | IPv4 value |
| description | String | IPv4 description |
| lastAccessDatetime | String | IPv4 last access date and time |
| deletionDatetime | String | IPv4 scheduled deletion date and time |
| creationUser | String | IPv4 created user |
| creationDatetime | String | IPv4 created date and time |
| lastChangeUser | String | IPv4 last modified user |
| lastChangeDatetime | String | IPv4 last modified date and time |

<a id="view-mac-credential-list"></a>
### View MAC Credential List { #view-mac-credential-list }

You can view the list of MAC credentials configured for a key store in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/macs
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
| ------- | ---- | ------------------ |
| macList | List | MAC credential list |

<a id="view-mac-credential-details"></a>
### View MAC Credential Details { #view-mac-credential-details }

You can view detailed information on a MAC credential configured for a key store in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue}
```

[Request Parameter]

| Name | Type | Description |
| -------- | ------ | --------------- |
| macValue | String | MAC address to retrieve |

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
                "description": "MAC description",
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
| ------------------ | ------ | -------------------- |
| macList | List | MAC authentication information list |
| value | String | MAC value |
| description | String | MAC description |
| lastAccessDatetime | String | MAC last access date and time |
| deletionDatetime | String | MAC scheduled deletion date and time |
| creationUser | String | MAC creation user |
| creationDatetime | String | MAC creation date and time |
| lastChangeUser | String | MAC last modification user |
| lastChangeDatetime | String | MAC last modification date and time |

<a id="view-certificate-credential-list"></a>
### View Certificate Credential List { #view-certificate-credential-list }

You can view the list of certificate credentials configured for a key store in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/certificates
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
| --------------- | ---- | --------------------- |
| certificateList | List | Certificate credential list |

<a id="view-certificate-credential-details"></a>
### View Certificate Credential Details { #view-certificate-credential-details }

You can view detailed information on a certificate credential configured for a key store in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.3/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName}
```

[Request Parameter]

| Name | Type | Description |
| --------------- | ------ | ------------------ |
| certificateName | String | Certificate name to retrieve |

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
                "description": "credential description",
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
| ------------------ | ------ | ----------------------- |
| certificateList | List | Certificate authentication information list |
| name | String | Certificate name |
| password | String | Certificate password |
| description | String | Certificate description |
| expirationDate | String | Certificate expiration date |
| lastAccessDatetime | String | Certificate last used |
| deletionDatetime | String | Certificate scheduled to be deleted |
| creationUser | String | Certificate creation user |
| creationDatetime | String | Certificate creation date |
| lastChangeUser | String | Certificate last modified user |
| lastChangeDatetime | String | Certificate last modified |
