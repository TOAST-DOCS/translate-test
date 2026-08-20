<!-- machine_translated: true -->

<!-- pre-align:aligned sig=feffcf49c769 -->

# Overview
**Security > Secure Key Manager > Overview**

Secure Key Manager is a service that securely stores users' critical data and controls access permissions. Users can store confidential data, symmetric keys, and asymmetric keys in Secure Key Manager. Only clients that pass the authentication method configured by the user can access data stored in Secure Key Manager.

<a id="main-features"></a>
## Main Features { #main-features }
* Data management
    * Register, manage, and query confidential data
    * Create, manage, rotate, encrypt/decrypt data with, and query symmetric keys
    * Create, manage, rotate, sign/verify data with, and query asymmetric keys
* Data access control
    * Control data access using client IPv4 addresses
    * Control data access using client MAC addresses
    * Control data access using client certificates
* Approval feature
    * Manage changes to data and data access control by separating responsibilities between approvers and requesters

<a id="feature-description"></a>
## Feature Description { #feature-description }
Secure Key Manager provides features to securely store users' critical data and control access permissions. Data that can be managed through Secure Key Manager is categorized into confidential data, symmetric keys, and asymmetric keys.

<a id="confidential-data-management"></a>
### Confidential Data Management { #confidential-data-management }
Secure Key Manager provides a feature for managing data that poses security risks when clients manage it directly, such as database connection information and app keys used for API calls. Users can register 32KB or smaller text data as confidential data. Only clients that pass the authentication method configured by the user can access registered confidential data. For information on how to use the confidential data management feature, see "Reference - Managing Database Access Information Using Secure Key Manager's Confidential Data Management Feature."

<a id="symmetric-key-management"></a>
### Symmetric Key Management { #symmetric-key-management }
Secure Key Manager provides a feature for managing user symmetric keys that can be used to encrypt and decrypt data. Users can create and store user symmetric keys in Secure Key Manager. Clients that pass the authentication method configured by the user can use the user symmetric keys stored in Secure Key Manager to encrypt and decrypt 32KB or smaller text data. User symmetric keys are never exposed directly to clients under any circumstances; they can only be used through the API. This protects user symmetric keys from being exposed externally. In addition, using Secure Key Manager's key rotation feature, you can renew the user symmetric key value without modifying the client. For information on how to use the symmetric key management feature, see "Reference - Envelope Encryption Using Secure Key Manager's Symmetric Key Management Feature."

<a id="asymmetric-key-management"></a>
### Asymmetric Key Management { #asymmetric-key-management }
Secure Key Manager provides a feature for managing user asymmetric keys that can be used to sign and verify data. Users can create and store user asymmetric keys in Secure Key Manager. Clients that pass the authentication method configured by the user can use the user asymmetric keys stored in Secure Key Manager to sign and verify 245 Byte or smaller text data. User asymmetric keys are never exposed directly to clients under any circumstances; they can only be used through the API. This protects user asymmetric keys from the risk of being exposed externally. In addition, using Secure Key Manager's key rotation feature, you can renew the user asymmetric key value without modifying the client.

<a id="access-control"></a>
### Access Control { #access-control }
Secure Key Manager provides various authentication methods to protect user data. Only clients that pass authentication can use data stored in Secure Key Manager. Authentication methods are categorized as follows: IPv4 Address Authentication, which verifies the client's IPv4 address; MAC Address Authentication, which verifies the client's MAC address; and Client Certificate Authentication, which verifies the certificate that the client uses for communication. Users must select at least one authentication method. If two or more are selected, the combination method can be specified through the authentication combination option. The combination method is divided into "All pass (AND, default)," which requires passing all enabled authentications, and "Any pass (OR)," which requires passing only one of the enabled authentications.

<a id="approval-feature"></a>
### Approval Feature { #approval-feature }
To meet the requirements for secure encryption key management as required by national and international security certification audits (ISMS-P, ISO, etc.), an approval process by a responsible party can be added for key creation, modification, deletion, and access control.

<a id="structure-of-service"></a>
## Service Structure { #structure-of-service }
Secure Key Manager internally uses two encryption keys — a root key and a system key — to securely store user data. The root key is used to protect the system key, and the system key is used to protect user data. The system key is encrypted with the root key and stored on the Secure Key Manager system key management server. When the Secure Key Manager server starts the service, it retrieves the encrypted system key from the Secure Key Manager system key management server through an authentication process. Once the system key is decrypted using the root key, the system key processing module is able to use the system key. To access user data stored in Secure Key Manager through unauthorized means, an attacker would need to obtain the root key, system key, and user data from three physically separate systems.

Users can manage Secure Key Manager from the NHN Cloud web console. The web console provides features such as creating and managing user data, and creating and managing client authentication data. All user data created in Secure Key Manager is encrypted with the system key and stored in the user data store. Client authentication data has certain sensitive information encrypted with the system key and stored in the client authentication data store.

Secure Key Manager provides various APIs for use on client servers. Client servers can request confidential data queries, encryption/decryption using symmetric keys, and signing/verification using asymmetric keys. The client authentication module uses client authentication data to determine whether to allow a client's request. When a client's request is allowed, the user data processing module uses the system key processing module to decrypt the encrypted user data and provide the service.

![overview-01](http://static.toastoven.net/prod_kms/2023-03-28/overview-01.png)

<a id="reference"></a>
## Reference { #reference }

<a id="managing-database-access-information-with-confidential-data-management-of-secure-key-manager"></a>
### Managing Database Access Information Using Secure Key Manager's Confidential Data Management Feature { #managing-database-access-information-with-confidential-data-management-of-secure-key-manager }
Applications that use a database store database connection information in configuration files. As the number of servers running the application increases, so does the number of servers storing database connection information, along with the risk of that information being exposed. Additionally, when database connection information changes, you must modify the configuration and redeploy to all servers, which is inconvenient.
By using Secure Key Manager's confidential data management feature, you can manage database connection information centrally and securely. Applications that need database access retrieve database connection information from Secure Key Manager when the service starts. Users can manage which application servers are allowed database access through Secure Key Manager. Even when database connection information changes, you can update it in Secure Key Manager without modifying the application.

<a id="envelope-encryption-with-symmetric-key-management-of-secure-key-manager"></a>
### Envelope Encryption Using Secure Key Manager's Symmetric Key Management Feature { #envelope-encryption-with-symmetric-key-management-of-secure-key-manager }
Secure Key Manager provides a symmetric key management feature that can encrypt and decrypt data. Applications can encrypt and decrypt any desired data by using the Secure Key Manager API. However, encrypting and decrypting all data processed by an application through the Secure Key Manager API can lead to performance and cost issues. The commonly used solution in this situation is the Envelope Encryption technique. Envelope Encryption is a method that protects only the encryption key used to encrypt the target data with a separate external encryption key. Data is encrypted using a local encryption key that the application manages on its own, and the local encryption key is encrypted using the Secure Key Manager API for storage. When data decryption is needed, the encrypted local encryption key is decrypted using the Secure Key Manager API and then used to decrypt the data.

<a id="glossary"></a>
### Glossary { #glossary }
| Term | Description |
|---|---|
| Key Store | The unit for storing user data and configuring authentication methods |
| Key | User data managed in Secure Key Manager (confidential data, symmetric keys, asymmetric keys) |
| Authentication Method | The method used to determine whether a client can access user data stored in Secure Key Manager |
| Authentication Data | Client information that is granted access to user data stored in Secure Key Manager |
| Key Rotation | The process of renewing only the key value while retaining the key ID of a symmetric or asymmetric key |
| Key Version | A value that increments each time a key rotation occurs for a symmetric or asymmetric key |