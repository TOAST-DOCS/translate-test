<!-- pre-align:aligned sig=76d6e0cfc969 -->

<a id="security-secure-key-manager-console-user-guide-getting-started"></a>
## Security > Secure Key Manager > Console User Guide > Getting Started { #security-secure-key-manager-console-user-guide-getting-started }

Getting Started describes basics for the use of Secure Key Manager.

![getting-started](http://static.toastoven.net/prod_kms/2024-02-27-en/getting-started.png)

<a id="create-a-key-store"></a>
## Create a Key Store { #create-a-key-store }
Secure Key Manager manages authentication information and keys in key store unit. If there is no key store, the following screen is displayed:

![console-guide-01](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-01.png)

Click **Add Key Store**, and a window to create a key store shows up.

![console-guide-39](http://static.toastoven.net/prod_kms/2026-05-18/console-guide.png)

Enter a name and description, and select one or more authentication methods. The **Authentication method combination** option is required and must be selected even when only one authentication method is enabled.

- **All pass (AND)**: Authentication succeeds only when all enabled authentication methods are passed (default).
- **Any pass (OR)**: Authentication succeeds when only one of the enabled authentication methods is passed. This is useful for zero-downtime migration when gradually transitioning from one authentication method to another while two or more authentication methods are enabled.

Click **Add** creates a key store. The created key store displays the key store list as follows:

![console-guide-03](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-03.png)

Click a key store from the list, and a menu to manage the key store is displayed as below:

![console-guide-04](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-04.png)

<a id="key-store-details"></a>
### Key Store Details { #key-store-details }

Click the View more button in the top right on the keystore to view information about the selected keystore through the Details menu.

![console-guide-43](http://static.toastoven.net/prod_kms/2024-02-27-en/console-guide-01.png)

<a id="create-a-key"></a>
## Create a Key { #create-a-key }
In Secure Key Manager, keys are categorized into three types: Confidential Data, Symmetric Key, and Asymmetric Key. For Confidential Data, Secure Key Manager stores string data and provides query feature using APIs. For Symmetric key, data encryption/decryption using APIs is provided. For Asymmetric Key, data signing/verification using APIs is provided. Users can select a key type appropriate for purpose and create keys.

Click **Key Management**, and a page to manage keys shows up like below:

![console-guide-05](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-05.png)

On the key management page, click **Add Key** and a window to create a key is displayed. Depending on the selected key type, you may enter data as needed.

![console-guide-06](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-06.png)


![console-guide-07](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-07.png)


![console-guide-08](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-08.png)


If you select Confidential Data, you can enter name, description, and data. If you select Symmetric Key or Asymmetric Key, you can enter name, description, and rotation cycle. After entering required data, click **Add** and a key is created. Then, the created key is displayed on the key management page as below:

![console-guide-09](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-09.png)

> [Note]
>
> The symmetric key is stored in the key store enabled when creating encrypted storage in the NAS service. For more information, see [NAS User Guide](https://docs.nhncloud.com/en/Storage/NAS/en/console-guide/#_2).

<a id="import-a-key"></a>
### Import a Key { #import-a-key }
Secure Key Manager supports a feature to import a symmetric key (AES-256).

![console-guide-10](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-10.png)

You can upload a key by entering a key value in the **Key Data** area, and the format of key that can be uploaded is as follows.

```
0xXX, 0xXX, ..., 0xXX
```

Upload the key by entering 32 hexadecimal strings separated by comma (`,`) or space (` `) used as delimiters, as shown above.

<a id="register-authentication-information"></a>
## Register Authentication Information { #register-authentication-information }
Keys that are created in Secure Key Manager are available only for successfully authenticated clients. You may register authentication information for client authentication from the menu of **IPv4 Address Management**, **MAC Address Management**, and **Certificate Management**.

<a id="register-ipv4-address"></a>
### Register IPv4 Address { #register-ipv4-address }
Click **IPv4 Address Management**, and a page to manage IPv4 address for client authentication shows up.

![console-guide-11](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-11.png)

Click **Add IPv4 Address**, and a window to add IPv4 address shows up as below:

![console-guide-12](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-12.png)

You can register not just IPv4 in the IP format and also IPv4 band using CIDR notation.

![console-guide-38](http://static.toastoven.net/prod_kms/2023-09-26-en/console-guide-38.png)

Enter client IPv4 address and description, and click **Add**, then the IPv4 address is added. Note that such IPv4 address must be same as the address that clients use to access Secure Key Manager. The newly added address is displayed on the IPv4 address management page.

![console-guide-13](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-13.png)

<a id="register-mac-address"></a>
### Register MAC Address { #register-mac-address }
Click **MAC Address Management**, and the MAC address management page for client authentication shows up.
![console-guide-14](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-14.png)

Click **Add MAC Address**, and a window to add MAC address shows up.

![console-guide-15](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-15.png)

Enter Client MAC Address and description, and click **Add**, then the MAC address is added. The newly added MAC address shows up on the MAC address management page.

![console-guide-16](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-16.png)

<a id="register-client-certificates"></a>
### Register Client Certificates { #register-client-certificates }
Click **Certificate Management**, and the certificate management page for client authentication shows up.

![console-guide-17](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-17.png)

Click **Add Certificates**, and a window to create a certificate shows up.

![console-guide-18](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-18.png)

Enter certificate name, password, and description, select usage period, and click **Add**, then a certificate is created. The newly created certificate shows up on the certificate management page like below. If you click the **Download** icon in the certificate management page, the certificate file is downloaded.

![console-guide-19](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-19.png)

<a id="manage-user-data"></a>
## Manage User Data { #manage-user-data }
Secure Key Manager provides detailed information on user-created data (e.g. key or authentication information). Click **Detail Key Information** on the list of user data, and details are displayed like below:

![console-guide-20](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-20.png)

<a id="delete-user-data"></a>
### Delete User Data { #delete-user-data }

The initial status of user-created data is **In Service**. To delete unnecessary data, click **Request for Deletion** in the **Detail Key Information** window.

![console-guide-21](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-21.png)

Once requested for deletion, the data status is changed to **Scheduled to be Deleted**. Data in **Scheduled to be Deleted** status becomes unavailable and it is completely deleted in 7 days.

![console-guide-22](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-22.png)

You may click **Immediately Delete** for data in **Scheduled to be Deleted** status to delete the data without having to wait until the scheduled deletion time, or click **Cancel Deletion** to revert it to **In Service** status.

![console-guide-23](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-23.png)

<a id="rotate-symmetricasymmetric-keys"></a>
### Rotate Symmetric/Asymmetric Keys { #rotate-symmetricasymmetric-keys }

In Secure Key Manager, symmetric/asymmetric keys can be rotated. Like shown below, auto rotation cycle can be set from the details page of Symmetric/Asymmetric Key. If you set the rotation cycle to '0', auto rotation is not enabled.

![console-guide-24](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-24.png)

If you set the rotation cycle to 30 or higher, the next rotation date is displayed, and key is automatically rotated at every rotation cycle.

![console-guide-25](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-25.png)

On the Detail Key Information page for Symmetric/Asymmetric Key, click **Immediately Rotate** to immediately rotate the key.

![console-guide-26](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-26.png)

When a key is rotated, a new version is added to the list of key versions, like below:

![console-guide-27](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-27.png)

As an exception, keys generated through key import do not provide the key rotation feature, unlike symmetric keys generated by Secure Key Manager. When you query the key, the key rotation area does not exist as shown below:

![console-guide-28](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-28.png)