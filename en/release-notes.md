<!-- pre-align:aligned sig=263cd1eadb32 -->

<a id="security-secure-key-manager-release-notes"></a>
## Security > Secure Key Manager > Release Notes { #security-secure-key-manager-release-notes }

<a id="june-9-2026"></a>
### June 9, 2026 { #june-9-2026 }
<a id="june-9-2026-added-features"></a>
#### Added Features
  * Added key store creation/modification/deletion API (v1.3)
    * Added a feature to create, modify, and delete a key store using API. For more information, see [API v1.3 Guide](/Security/Secure%20Key%20Manager/ko/api-guide-v1.3/).

<a id="may-27-2026"></a>
### May 27, 2026 { #may-27-2026 }
<a id="may-27-2026-added-features"></a>
#### Added Features
* Added asymmetric key standard scheme signing/verification API (v1.3)
    * Added an API to sign and verify data with an asymmetric key according to standard RSA signing schemes (RSASSA-PSS, RSASSA-PKCS1-v1_5). For more information, see [API v1.3 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.3/).
<a id="may-27-2026-feature-updates"></a>
#### Feature Updates
  * Added key store authentication method combination option
    * Added a feature to select the method for combining multiple authentication methods (IPv4 address, MAC address, client certificate) enabled in the key store. Users can select either all pass (AND, default) or any pass (OR). Existing key stores remain configured as all pass (AND). For more information, see [Console User Guide](/Security/Secure%20Key%20Manager/en/console-guide/).

<a id="april-14-2026"></a>
### April 14, 2026 { #april-14-2026 }
<a id="april-14-2026-feature-updates"></a>
#### Feature Updates
  * Removed `APPROVAL MEMBER` role
    * Simplified the role structure by migrating the Secure Key Manager APPROVAL MEMBER role to the Secure Key Manager ADMIN role.
  * Granular permissions
    * Added `SecureKeyManager:API.ADMIN` and `SecureKeyManager:API.VIEWER` permissions to enable more granular management of console and API permissions.

<a id="march-10-2026"></a>
### March 10, 2026 { #march-10-2026 }
<a id="march-10-2026-added-features"></a>
#### Added Features
  * Added API v1.3
    * Added a token authentication method via the `X-NHN-AUTHORIZATION` header. For details, see [API v1.3 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.3/).
  * Added a confidential data editing API (v1.2, v1.3)
    * Added a feature to edit confidential data stored in Secure Key Manager using the API. For details, see [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/) or [API v1.3 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.3/).

<a id="february-10-2026"></a>
### February 10, 2026 { #february-10-2026 }
<a id="february-10-2026-new-features"></a>
#### New Features
  * Added API for retrieving detailed key store lists
    * Added a feature to retrieve detailed key store information via API. For more information, refer to the [API v1.0 Guide](/Security/Secure%20Key%20Manager/ko/api-guide-v1.0/) or [API v1.2 Guide](/Security/Secure%20Key%20Manager/ko/api-guide-v1.2/).
  * Added API for retrieving detailed key lists
    * Added a feature to retrieve detailed key information via API. For more information, refer to the [API v1.0 Guide](/Security/Secure%20Key%20Manager/ko/api-guide-v1.0/) or [API v1.2 Guide](/Security/Secure%20Key%20Manager/ko/api-guide-v1.2/).

<a id="june-24-2025"></a>
### June 24, 2025 { #june-24-2025 }
<a id="june-24-2025-feature-updates"></a>
#### Feature Updates
  * Added new error message
    * Added an error message for API requests with invalid URIs. For more information, see the [Troubleshooting Guide](/Security/Secure%20Key%20Manager/en/troubleshooting-guide/#api-call-failure-returns-url-not-found-error-message).

<a id="april-28-2025"></a>
### April 28, 2025 { #april-28-2025 }
<a id="april-28-2025-feature-updates"></a>
#### Feature Updates
  * Changed the data retention period from 3 years to 1 year
    * [Related Notice](https://www.nhncloud.com/kr/support/notice/detail/6493)

<a id="march-25-2025"></a>
### March 25, 2025 { #march-25-2025 }
<a id="march-25-2025-added-new-features"></a>
#### Added New Features
  * Added APIs to query key store list and details
    * Added API for querying detailed key stores using a list of key store IDs or key store IDs
  * Added APIs to query key list and details
    * Added API for querying detailed keys using a list of key IDs or key IDs
  * Added APIs to query authentication information list and details
    * Added API for querying detailed authentication information using a list of authentication information values or values

<a id="september-25-2024"></a>
### September 25, 2024 { #september-25-2024 }
<a id="september-25-2024-feature-updates"></a>
#### Feature Updates
  * Deleted the Number column from the table in the approval list

<a id="august-27-2024"></a>
### August 27, 2024 { #august-27-2024 }
<a id="august-27-2024-added-new-features"></a>
#### Added New Features
  * Added the feature to receive event notifications for Secure Key Manager in the Resource Watcher service
<a id="august-27-2024-feature-updates"></a>
#### Feature Updates
  * Removed the self-approval feature
    * Made modifications to prevent approvals for requests made by users themselves

<a id="april-23-2024"></a>
### April 23, 2024 { #april-23-2024 }
<a id="april-23-2024-bug-fixes"></a>
#### Bug Fixes
  * Fixed an error where, when deleting data (keys, credentials) uisng APIs and retrieving deleted data, even undeleted data cannot be retrieved until refreshing after the error window appeared

<a id="march-26-2024"></a>
### March 26, 2024 { #march-26-2024 }
<a id="march-26-2024-added-new-features"></a>
#### Added New Features
  * Added Add/Delete Credentials API
     * Added the feature to add or delete credentials to use a key using APIs.
     * To add or delete credentials using APIs, you must need **User Access Key ID** and **Secret Access Key**. For more information, see [User Access Key](/nhncloud/en/public-api/user-access-key).

<a id="february-27-2024"></a>
### February 27, 2024 { #february-27-2024 }
<a id="february-27-2024-added-new-features"></a>
#### Added New Features
  * Added notification mail recipient settings
     * Added the feature to set email recipient address in Organization/Project Dashboard > Manage Notifications.
<a id="february-27-2024-feature-updates"></a>
#### Feature Updates
   * Exposed keystore ID
     * Exposed area to view keystore ID in keystore details
     * Added the feature to copy keystore ID via the More button to the right of the keystore ID

<a id="november-28-2023"></a>
### November 28, 2023 { #november-28-2023 }
<a id="november-28-2023-added-new-features"></a>
#### Added New Features
  * Added Add/Delete Key APIs
    * Added the feature to add or delete keys using APIs
    * To add or delete keys using APIs, you must need a User Access Key ID and a Secret Access Key. For more information, see [User Access Key](/nhncloud/en/public-api/user-access-key)

<a id="september-26-2023"></a>
### September 26, 2023 { #september-26-2023 }
<a id="september-26-2023-feature-updates"></a>
#### Feature Updates
  * Added IPv4 Bandwidth Authentication Feature
    * Added a feature to authenticate bandwith using CIDR notation when authentication with IPv4

<a id="july-25-2023"></a>
### July 25, 2023 { #july-25-2023 }
<a id="july-25-2023-bug-fixes"></a>
#### Bug Fixes
  * Fixed Approval Process Certificate Cancel Error
    * Fixed an error in the approval process where a certificate in the **In Use** status is displayed as **Scheduled to Cancel Deletion** instead of the original **In Use** status when requesting deletion and then canceling the request

<a id="may-30-2023"></a>
### May 30, 2023 { #may-30-2023 }
<a id="may-30-2023-bug-fixes"></a>
#### Bug Fixes
  * Fixed Approval Process Notification (email) Error
    * Fixed an issue where some managers with approval authority cannot receive notifications (email)
  * Fixed Error in IP/MAC Large Registration of Approval Process
    * Fixed an issue where, when registering a large amount of IP/MAC in the approval process, it is not immediately reflected

<a id="april-25-2023"></a>
### April 25, 2023 { #april-25-2023 }
<a id="april-25-2023-added-new-features"></a>
#### Added New Features
* Added Approval Process Notification (email) Feature
    * Added a feature to notify the manager with approval authority via email when registering a request for approval

<a id="february-28-2023"></a>
### February 28, 2023 { #february-28-2023 }
<a id="february-28-2023-bug-fixes"></a>
#### Bug Fixes
* Fixed Template File Download Error
    * Fixed an issue where bulk registration template file is downloaded as a template in the wrong format

<a id="january-31-2023"></a>
### January 31, 2023 { #january-31-2023 }
<a id="january-31-2023-bug-fixes"></a>
#### Bug Fixes
 * Improved Approval Feature and Fixed an Error
    * Modified the feature so that, when entering the confidential data editing screen while using the approval feature, the data area is displayed as blank
    * Modified the feature so that the edited data is displayed after editing the confidential data
 * Fixed an issue where the tooltip messages for MAC address is displayed as IPv4, not MAC address on the key store management tab.

<a id="december-27-2022"></a>
### December 27, 2022 { #december-27-2022 }
<a id="december-27-2022-feature-updates"></a>
#### Feature Updates
  * Changed API Domain
    * Changed the SecureKeyManager API domain from `api-keymanager.cloud.toast.com` to `api-keymanager.nhncloudservice.com`

<a id="november-29-2022"></a>
### November 29, 2022 { #november-29-2022 }
<a id="november-29-2022-bug-fixes"></a>
#### Bug Fixes
  * Improved Approval Feature and Fixed an Error
    * Modified an error message that occurs while using the approval feature so that it is more understandable
    * Fixed an issue where, when initially adding a key store while using the approval feature, it is added without approval procedure
  * Fixed Certificate Authentication Error
    * Fixed an issue where certificate authentication fails intermittently

<a id="october-25-2022"></a>
### October 25, 2022 { #october-25-2022 }
<a id="october-25-2022-bug-fixes"></a>
#### Bug Fixes
 * Fixed Total Appkey Error
   * Fixed an issue where calling APIs with a project total appkey does not work properly.
 * Fixed Approval Feature Error
   * Fixed an issue where deletion does not work properly for each key version when using approval feature

<a id="september-27-2022"></a>
### September 27, 2022 { #september-27-2022 }
<a id="september-27-2022-added-new-features"></a>
#### Added New Features
  * Added an Asymmetric Key Query Feature
    * Added a feature to query the asymmetric key for each key version

<a id="july-26-2022"></a>
### July 26, 2022 { #july-26-2022 }
<a id="july-26-2022-added-new-features"></a>
#### Added New Features
  * Added Approval Feature
    * Added a feature to approve major changes such as key creation, modification, deletion, and changes to access control for key store
  * Added a new version of Symmetric Key Query Feature
    * Added a feature to query the symmetric key for each key version

<a id="november-23-2021"></a>
### November 23, 2021 { #november-23-2021 }
<a id="november-23-2021-added-new-features"></a>
#### Added New Features
  * Added a Symmetric Key Query Feature
    * Added a feature to query the symmetric key

<a id="october-26-2021"></a>
### October 26, 2021 { #october-26-2021 }
<a id="october-26-2021-added-new-features"></a>
#### Added New Features
  * Added a Key Import Feature
    * Added a symmetric key import feature
<a id="october-26-2021-feature-updates"></a>
#### Feature Updates
  * Updated the Confidential Data Query Feature
    * Modified the feature so that, when the user queries confidential data in the web console, the data is provided after masking the fields
<a id="october-26-2021-bug-fixes"></a>
#### Bug Fixes
  * Fixed an issue where non-payment users could use the service normally

<a id="september-28-2021"></a>
### September 28, 2021 { #september-28-2021 }
<a id="september-28-2021-bug-fixes"></a>
#### Bug Fixes
  * Fixed an issue where permissions granted using permission groups were not recognized properly
  * Fixed an issue where the Reset button in Usage History did not work properly

<a id="march-24-2020"></a>
### March 24, 2020 { #march-24-2020 }
<a id="march-24-2020-added-new-features"></a>
#### Added New Features
  * The tasks performed by a user in Secure Key Manager console are logged in Cloud Trail
  * Added authentication data (IPv4 address/MAC address) bulk registration feature using CSV files
  * Added authentication data (IPv4 address/MAC address) download feature using CSV files

<a id="december-24-2019"></a>
### December 24, 2019 { #december-24-2019 }
<a id="december-24-2019-added-new-features"></a>
#### Added New Features
  * Statistics Page
    * Added the page to query API usage statistics of each project
<a id="december-24-2019-feature-updates"></a>
#### Feature Updates
  * Key Store Page Updates
    * Changed the display method for the list of key stores
    * Changed the sub-menu of a key store
    * Added the quick menu to the key store
  * History Page Updates
    * Changed UI so that the user can query API usage history per project

<a id="july-23-2019"></a>
### July 23, 2019 { #july-23-2019 }
<a id="july-23-2019-feature-updates"></a>
#### Feature Updates
  * UI Improvement
    * Fixed the overlapped display of texts and buttons
    * Fixed line wrapping issue when the screen is displayed in Japanese

<a id="may-28-2019"></a>
### May 28, 2019 { #may-28-2019 }
<a id="may-28-2019-release-of-new-service"></a>
#### Release of New Service
* Secure Key Manager is a service to let you centrally and securely manage data that can be exposed to security risks when stored in the application server, such as confidential data, symmetric key, and asymmetric key. In addition, it controls access so that only the clients that pass authentication can access the data.
