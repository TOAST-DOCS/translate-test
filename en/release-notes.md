<!-- pre-align:aligned sig=39caf24ddae0 -->

<a id="management-certificate-manager-release-notes"></a>
## Management > Certificate Manager > Release Notes { #management-certificate-manager-release-notes }

<a id="july-28-2026"></a>
### July 28, 2026 { #july-28-2026 }
<a id="july-28-2026-feature-updates"></a>
#### Feature Updates
* Added the certificate ID to the response of the certificate list retrieval API in Certificate Manager API v1.3.
* Added an API to download certificates using a certificate ID in Certificate Manager API v1.3.
  * For more information, see the [API v1.3 Guide](./api-guide-v1.3/).
* Migrated Notification Group > Receiving group to **Notification Receiver Group Management**.

<a id="april-14-2026"></a>
### April 14, 2026 { #april-14-2026 }
<a id="april-14-2026-api-v11-authentication-and-permission-updates"></a>
#### API v1.1 Authentication and Permission Updates
* Updated the authentication and permission information in the Certificate Manager API v1.1 guide.
    * The **Certificate Manager ADMIN** role or **Certificate Manager VIEWER** role is required to use the API.
    * For more information, refer to the [API v1.1 guide](./api-guide-v1.1/).

<a id="march-10-2026"></a>
### March 10, 2026 { #march-10-2026 }
<a id="march-10-2026-added-a-api-version"></a>
#### Added a API version
* Added Certificate Manager API v1.3 supporting token authentication method.
  <br> For more information, refer to API v1.3 Guide.

<a id="november-25-2025"></a>
### November 25, 2025 { #november-25-2025 }
<a id="november-25-2025-feature-updates"></a>
#### Feature Updates
* Modified certificate name restrictions so that you can manage both old and new certificates together.
    * Certificate names do not need to be identical to the CN (CommonName) value in the certificate file; they can be registered as long as they are unique within the project.
* Added the Domains [CN (CommonName) + SAN (SubjectAlternativeNames)] field to the certificate.
    * Domains information is automatically collected when uploading a certificate file.
* Removed certificate types (Single, Wildcard, SAN).
* Modified certificate list and details UI.
* For more information, you can check the contents in the [Console User Guide](./console-guide/).

<a id="march-26-2024"></a>
### March 26, 2024 { #march-26-2024 }
<a id="march-26-2024-add-a-new-api-version"></a>
#### Add a new API version
* Added API v1.1 for Certificate Manager. <br>You can find more information in the API v1.1 guide.

<a id="february-27-2024"></a>
### February 27, 2024 { #february-27-2024 }
<a id="february-27-2024-added-the-feature-to-set-who-receives-notification-emails"></a>
#### Added the feature to set who receives notification emails
* Added the feature to set the incoming mail address name in Organization/Project Dashboard > Manage Notifications.

<a id="march-28-2023"></a>
### March 28, 2023 { #march-28-2023 }
<a id="march-28-2023-feature-updates"></a>
#### Feature Updates
* Improved to display the message `Only files with the extension '.pem' can be uploaded.` if the selected file is not a certificate file (.pem) when registering a certificate.
* The passphrase value of the certificate is limited to a maximum of 200 characters.
<a id="march-28-2023-bug-fixes"></a>
#### Bug Fixes
* Fixed an issue where the Modify button is deactivated after modifying user data.

<a id="february-28-2023"></a>
### February 28, 2023 { #february-28-2023 }
<a id="february-28-2023-added-features"></a>
#### Added Features
* Added SAN certificate feature
    * SAN (subject alternative name) is a certificate that allows you to apply SSL to multiple domains with a single certificate.
    * By registering SAN certificate, you can easily manage expiration dates and notification settings for sub-certificates.
    * When you add or modify SAN certificate,  it reads information from the certificate file (.pem) to automatically enter the certificate name and sub certificate name.

<a id="february-28-2023-feature-updates"></a>
#### Feature Updates
* Improved so that user data names cannot be entered only with spaces.

<a id="january-31-2023"></a>
### January 31, 2023 { #january-31-2023 }
<a id="january-31-2023-feature-updates"></a>
#### Feature Updates
* Changed the maximum length of user data from 3,000 to 700 characters.
* Changed the naming rules for domains have.
     * The beginning and end of the domain and between dot(.) and dot(.) are limited to 63 characters.
     * The maximum length of domains is limited to 260 characters.
<a id="january-31-2023-bug-fixes"></a>
#### Bug Fixes
* Fixed an issue where the HTML format is applied when the notification group and user data names are in the HTML format during email notification.

<a id="december-27-2022"></a>
### December 27, 2022 { #december-27-2022 }
<a id="december-27-2022-feature-updates"></a>
#### Feature Updates
* Improved so that, when you click the **Initialize** button on the search bar, all options are selected.
* Improved so that, even when you select a search option and close the dropdown list without clicking the **Apply** button, the selected option is applied.
* Improved so that, when the auto-collection feature does not work in the domain, `-` is displayed on the registrar and registering institution items.
* Added an organization name to SMS notifications, and shortened guide messages.
<a id="december-27-2022-bug-fixes"></a>
#### Bug Fixes
* Fixed an issue where, when re-entering an additional page in the domain, the expiry date is set to the previously set value.

<a id="october-25-2022"></a>
### October 25, 2022 { #october-25-2022 }
<a id="october-25-2022-feature-updates"></a>
#### Feature Updates
* Fixed an issue where calling APIs with a project total appkey does not work properly.
* Modified the logic so that, when collection of certificates and domain information fails, mail is sent only for those confirmed that day.

<a id="october-4-2022"></a>
### October 4, 2022 { #october-4-2022 }
<a id="october-4-2022-feature-updates"></a>
#### Feature Updates
* Fixed an issue where a permission is not properly applied when it is issued through the role group management.

<a id="august-23-2022"></a>
### August 23, 2022 { #august-23-2022 }
<a id="august-23-2022-feature-updates"></a>
#### Feature Updates
* Changed the API's endpoint domain from api-certificate-manager.cloud.toast.com to certmanager.api.nhncloudservice.com.

<a id="march-24-2020"></a>
### March 24, 2020 { #march-24-2020 }
<a id="march-24-2020-added-features"></a>
#### Added Features
Added API to list certificates that have been registered for Certificate Manager.
* [API] Added List Certificates API

<a id="january-21-2020"></a>
### January 21, 2020 { #january-21-2020 }
<a id="january-21-2020-new-releases"></a>
#### New Releases
Certificate Manager sends notifications (via SMS or email) when you near the expiration date so that you can extend the date timely.
Certificatae Manager manages TLS certificates, domains, or user data (e.g. licenses) that have expiration dates, by specifying notification delivery rules and recipient users.
