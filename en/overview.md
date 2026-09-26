<!-- pre-align:aligned sig=feffcf49c769 -->

# Overview
**Security > Secure Key Manager > Overview**

Secure Key Manager is a service to store user's important data securely and control access permission. Users may store confidential data, symmetric keys, and asymmetric keys in Secure Key Manager. Data stored in Secure Key Manager can only be accessed by clients that pass the user-configured authentication method.

<a id="main-features"></a>
## Main Features { #main-features }
* Data Management
    * Register, manage, and query confidential data
    * Create, manage, and rotate symmetric keys, or encrypt, decrypt, and query data
    * Create, manage, and rotate asymmetric keys, or sign, verify, and query data
* Data Access Control
    * Control data access by using client's IPv4 address
    * Control data access by using client's MAC address
    * Control data access by using client's certificate
* Approval Feature
    * Manage changes to data and data access control through approvers and requesters

<a id="feature-description"></a>
## Feature Description { #feature-description }
Secure Key Manager provides features to store user's important data securely and control access permission. Confidential data, symmetric keys, and asymmetric keys can be managed by Secure Key Manager.

<a id="confidential-data-management"></a>
### Confidential Data Management { #confidential-data-management }
Secure Key Manager provides features to manage data that may be exposed to security threats if they are under client's direct management, such as database access information, or Appkey for API calls. Users can register 32KB or smaller text data as confidential data. Only the clients that pass the user-configured authentication method can access the registered confidential data. Regarding the use of confidential data management, see "Reference- Managing Database Access Information with Confidential Data Management of Secure Key Manager".

<a id="symmetric-key-management"></a>
### Symmetric Key Management { #symmetric-key-management }
Secure Key Manager provides features to manage user symmetric keys that can be used to encrypt/decrypt data. Users can create and store symmetric keys in Secure Key Manager. Clients that pass the user-configured authentication method can encrypt or decrypt 32KB or smaller text data by using user symmetric keys stored in Secure Key Manager. User symmetric keys are never directly exposed to clients, but are available only for use through APIs. Therefore, user symmetric keys can be protected without being exposed to outside. In addition, by using the key rotation feature of Secure Key Manager, user symmetric key values can be updated without changing clients. Regarding the use of symmetric key management, see "Reference- Envelope Encryption with Symmetric Key Management of Secure Key Manager".

<a id="asymmetric-key-management"></a>
### Asymmetric Key Management { #asymmetric-key-management }
Secure Key Manager provides features to manage user's asymmetric keys that can be used to sign/verify data. Users can create and store user asymmetric keys in Secure Key Manager. Clients that pass the user-configured authentication method can sign/verify 245 Byte or smaller text data by using user asymmetric keys stored in Secure Key Manager. User asymmetric keys are never directly exposed to clients, but are available only for use through APIs. Therefore, user asymmetric keys can be protected without being exposed to outside. In addition, by using the key rotation feature of Secure Key Manager, user asymmetric key values can be updated without changing clients.

<a id="access-control"></a>
### Access Control { #access-control }
Secure Key Manager provides various authentication methods to protect user data. Only the clients that pass the authentication can access data stored in Secure Key Manager. The authentication methods are categorized into 'IPv4 Address Authentication' that checks client's IPv4 address, 'MAC Address Authentication' that checks client's MAC address, and 'Client Certificate Authentication' that checks client's certificate used for communication. The user must select at least one authentication method, and the combination method can be specified through the authentication method combination option. The combination method is divided into "All pass (AND, default)," which requires passing all enabled authentications, and "Any pass (OR)," which requires passing only one of the enabled authentications.

<a id="approval-feature"></a>
### Approval Feature { #approval-feature }
To meet the secure encryption key management requirements required by domestic and foreign security certification audits (ISMS-P, ISO, etc.), a manager's approval procedure can be added for key creation, modification, deletion, and access control.

<a id="structure-of-service"></a>
## Structure of Service { #structure-of-service }
To store user data securely, Secure Key Manager internally applies two encryption keys, root key and system key. Root Key is used to protect the system key, while system key is to protect user data. System Key is encrypted with Root Key and stored at the system key management server of Secure Key Manager. The Secure Key Manager server goes through authentication process during the start of the service, and retrieves encrypted system key from the system key management server of Secure Key Manager. When it is decrypted by using the root key, system key becomes available for the system key processing module. To access user data stored in Secure Key Manager abnormally, all of root key, system key, and user data must be acquired from three physically separated systems.

Users can manage Secure Key Manager on the NHN Cloud web console. Web console provides features such as creating/managing user data and creating/managing client authentication data. All user data generated in Secure Key Manager are encrypted with system key and stored in user's data storage. For client authentication data, a part of important data is encrypted with system key and stored in a client authentication data storage.

Secure Key Manager provides various APIs that can be used by a client server. The client server can request querying confidential data, encrypting/decrypting with symmetric keys, and signing/verifying with asymmetric keys. Client authentication module determines whether to allow client's request by using client authentication data. If a client's request is allowed, the user data processing module decrypts encrypted user data with system key processing module and provides service.

![overview-01](http://static.toastoven.net/prod_kms/2023-03-28/overview-01.png)

<a id="reference"></a>
## Reference { #reference }

<a id="managing-database-access-information-with-confidential-data-management-of-secure-key-manager"></a>
### Managing Database Access Information with Confidential Data Management of Secure Key Manager { #managing-database-access-information-with-confidential-data-management-of-secure-key-manager }
An application using database stores database access information in the configuration file. As the number of servers running such applications increases, more servers store database access information, increasing the risk of exposure of such data. In addition, when there is a change in the database access information, the configuration must be modified and redeployed to the entire servers.
With the confidential data management feature of Secure Key Manager, database access information can be safely managed centrally. Applications requiring database access can retrieve database access information from Secure Key Manager, at the start of a service. With Secure Key Manager, users can manage application servers to allow database access. Even with a change in the database access information, you just need to update information in Secure Key Manager without modifying application.

<a id="envelope-encryption-with-symmetric-key-management-of-secure-key-manager"></a>
### Envelope Encryption with Symmetric Key Management of Secure Key Manager { #envelope-encryption-with-symmetric-key-management-of-secure-key-manager }
Secure Key Manager provides symmetric key management to enable data encryption/decryption. Applications can encrypt/decrypt data by using the Secure Key Manager API. However, encrypting/decrypting all data with Secure Key Manager API may cause performance or cost issues.  That is when Envelope Encryption comes in, as one of the most common solutions. Envelope Encryption refers to a method in which only the encryption key, which is applied to encrypt data for encryption, is protected by another encryption key from outside. In other words, data is encrypted by a local encryption key which is managed within an application, while the local encryption key is encrypted with Secure Key Manager API and stored. When the data needs to be decrypted, the encrypted local encryption key gets decrypted with the Secure Key Manager API and then used for data decryption.

<a id="glossary"></a>
### Glossary { #glossary }
| Term | Description |
|---|---|
| Key Store | The unit of storing user data and setting authentication method |
| Key | User data managed by Secure Key Manager (e.g. confidential data, symmetric key, or asymmetric key) |
| Authentication Method | A method for deciding whether a client can access user data stored in Secure Key Manager |
| Authentication Data | Client information allowing access to user data stored in Secure Key Manager |
| Key Rotation | A task of updating key values only while retaining key ID of symmetric and asymmetric keys |
| Key Version | A value that increases at every key rotation of symmetric or asymmetric keys |
