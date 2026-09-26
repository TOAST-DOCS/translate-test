<!-- pre-align:aligned sig=c775a568be8f -->

# Solution Guide
**Security > Secure Key Manager > Solution Guide**

The following describes the solutions for main issues that may arise while using Secure Key Manager.

<a id="api-call-failure-returns-invalid-appkey-error-message"></a>
## API call failure returns Invalid Appkey error message. { #api-call-failure-returns-invalid-appkey-error-message }
* Occurs when API is called with an invalid appkey.
    * Check if appkey was correctly applied as displayed on the URL & Appkey window in the Secure Key Manager management page.

<a id="api-call-failure-returns-invalid-key-id-error-message"></a>
## API call failure returns Invalid Key ID error message. { #api-call-failure-returns-invalid-key-id-error-message }
* Occurs when Key ID for an API call is invalid.
    * Check if the used key ID is correct.
    * See if the status of the key is In Service.

<a id="api-call-failure-returns-invalid-key-version-error-message"></a>
## API call failure returns Invalid Key Version error message. { #api-call-failure-returns-invalid-key-version-error-message }
* Occurs when API is called with invalid key version.
    * If it comes from Decrypt Symmetric Keys API, check if the key version applied for encryption still exists.
    * If it comes from Verify Asymmetric Keys API, check if the key version applied for signature still exists.

<a id="api-call-failure-returns-invalid-user-data-error-message"></a>
## API call failure returns Invalid User Data error message. { #api-call-failure-returns-invalid-user-data-error-message }
* Occurs when API is called with invalid user data.
    * If it comes from Decrypt Symmetric Keys API, check if the data for decryption is correct.
    * If it comes from Verify Asymmetric Keys API, check if the signature value is correct.

<a id="api-call-failure-returns-invalid-key-status-error-message"></a>
## API call failure returns Invalid Key Status error message. { #api-call-failure-returns-invalid-key-status-error-message }
* Occurs when API is called with invalid key.
    * If it comes from Decrypt Asymmetric Keys API, check if the key for encryption is 'In Service'.
    * If it comes from Verify Asymmetric Keys API, check if the key for signature is 'In Service'.

<a id="api-call-failure-returns-invalid-key-version-status-error-message"></a>
## API call failure returns Invalid Key Version Status error message. { #api-call-failure-returns-invalid-key-version-status-error-message }
* Occurs when API is called with invalid key version.
    * If it comes from Decrypt Asymmetric Keys API, check if the key version for encryption is 'In Service'.
    * If it comes from Verify Asymmetric Keys API, check if the key version for signature is 'In Service'.

<a id="api-call-failure-returns-ipv4-auth-failure-error-message"></a>
## API call failure returns IPv4 Auth Failure error message. { #api-call-failure-returns-ipv4-auth-failure-error-message }
* Occurs when it fails to certify IPv4 address.
    * Check if the IPv4 address of API caller client has been registered in Secure Key Manager.
    * Check if the client IPv4 address registered in Secure Key Manager is 'In Service'.

<a id="api-call-failure-returns-mac-auth-failure-error-message"></a>
## API call failure returns MAC Auth Failure error message. { #api-call-failure-returns-mac-auth-failure-error-message }
* Occurs when it fails to certify MAC address.
    * Check if the MAC address of API caller client has been registered in Secure Key Manager.
    * Check if the MAC address registered in Secure Key Manager is 'In Service'.
    * Check if the client's MAC address has been added to the request header of X-TOAST-CLIENT-MAC-ADDR to call API.

<a id="api-call-failure-returns-certificate-auth-failure-error-message"></a>
## API call failure returns Certificate Auth Failure error message. { #api-call-failure-returns-certificate-auth-failure-error-message }
* Occurs when it fails to certify client's certificate.
    * Check if the certificate has been issued by Secure Key Manager.
    * Check if the certificate registered in Secure Key Manager is 'In Service'.

<a id="api-call-failure-returns-certificate-related-error-messages"></a>
## API call failure returns certificate-related error messages. { #api-call-failure-returns-certificate-related-error-messages }
* Occurs when certificate is not correct.
    * Check if the certificate has been issued by Secure Key Manager.
    * Check valid period of the certificate.

<a id="api-call-failure-returns-url-not-found-error-message"></a>
## API call failure returns URL NOT FOUND error message. { #api-call-failure-returns-url-not-found-error-message }
* Occurs when a request is made with an invalid URL.
    * Check if the URL is correct.

<a id="api-call-failure-returns-url-not-found-error-message-for-any-other-errors-that-occur-during-an-api-request-contact-us-at-customer-support-contact-us"></a>
#### For any other errors that occur during an API request, contact us at Customer Support > [Contact us](https://www.nhncloud.com/KR/support/inquiry)
