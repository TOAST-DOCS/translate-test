<!-- machine_translated: true -->

<!-- pre-align:aligned sig=c775a568be8f -->

# Troubleshooting Guide
**Security > Secure Key Manager > Troubleshooting Guide**

This guide describes solutions for common issues that may occur when using Secure Key Manager.

<a id="api-call-failure-returns-invalid-appkey-error-message"></a>
## API call fails and returns an Invalid Appkey error message. { #api-call-failure-returns-invalid-appkey-error-message }
* This occurs when the appkey used for the API call is not valid.
    * Check that you are using the correct appkey displayed in the URL & Appkey window on the Secure Key Manager management page.

<a id="api-call-failure-returns-invalid-key-id-error-message"></a>
## API call fails and returns an Invalid Key Id error message. { #api-call-failure-returns-invalid-key-id-error-message }
* This occurs when the Key Id used for the API call is not valid.
    * Check that you are using the correct Key Id.
    * Check that the key is in the **In Use** status.

<a id="api-call-failure-returns-invalid-key-version-error-message"></a>
## API call fails and returns an Invalid Key Version error message. { #api-call-failure-returns-invalid-key-version-error-message }
* This occurs when the Key Version used for the API call is not valid.
    * If this occurred in the Symmetric Key decryption API, check that the key version that was used at the time of encryption exists.
    * If this occurred in the Asymmetric Key verification API, check that the key version that was used at the time of signing exists.

<a id="api-call-failure-returns-invalid-user-data-error-message"></a>
## API call fails and returns an Invalid User Data error message. { #api-call-failure-returns-invalid-user-data-error-message }
* This occurs when the user data used for the API call is not valid.
    * If this occurred in the Symmetric Key decryption API, check that the data to be decrypted is correct.
    * If this occurred in the Asymmetric Key verification API, check that the signature value is correct.

<a id="api-call-failure-returns-invalid-key-status-error-message"></a>
## API call fails and returns an Invalid Key Status error message. { #api-call-failure-returns-invalid-key-status-error-message }
* This occurs when the status of the key used for the API call is not valid.
    * If this occurred in the Symmetric Key decryption API, check that the key that was used at the time of encryption is in the **In Use** status.
    * If this occurred in the Asymmetric Key verification API, check that the key that was used at the time of signing is in the **In Use** status.

<a id="api-call-failure-returns-invalid-key-version-status-error-message"></a>
## API call fails and returns an Invalid Key Version Status error message. { #api-call-failure-returns-invalid-key-version-status-error-message }
* This occurs when the status of the Key Version used for the API call is not valid.
    * If this occurred in the Symmetric Key decryption API, check that the key version that was used at the time of encryption is in the **In Use** status.
    * If this occurred in the Asymmetric Key verification API, check that the key version that was used at the time of signing is in the **In Use** status.

<a id="api-call-failure-returns-ipv4-auth-failure-error-message"></a>
## API call fails and returns an IPv4 Auth Failure error message. { #api-call-failure-returns-ipv4-auth-failure-error-message }
* This occurs when IPv4 Address Authentication fails.
    * Check that the IPv4 address of the client making the API call is registered in Secure Key Manager.
    * Check that the IPv4 address of the client registered in Secure Key Manager is in the **In Use** status.

<a id="api-call-failure-returns-mac-auth-failure-error-message"></a>
## API call fails and returns a MAC Auth Failure error message. { #api-call-failure-returns-mac-auth-failure-error-message }
* This occurs when MAC Address Authentication fails.
    * Check that the MAC address of the client making the API call is registered in Secure Key Manager.
    * Check that the MAC address of the client registered in Secure Key Manager is in the **In Use** status.
    * Check that you have added the client's MAC address to the X-TOAST-CLIENT-MAC-ADDR request header when making the API call.

<a id="api-call-failure-returns-certificate-auth-failure-error-message"></a>
## API call fails and returns a Certificate Auth Failure error message. { #api-call-failure-returns-certificate-auth-failure-error-message }
* This occurs when Client Certificate Authentication fails.
    * Check that you are using a certificate issued by Secure Key Manager.
    * Check that the certificate registered in Secure Key Manager is in the **In Use** status.

<a id="api-call-failure-returns-certificate-related-error-messages"></a>
## API call fails and returns a certificate-related error message. { #api-call-failure-returns-certificate-related-error-messages }
* This occurs when the certificate is not valid.
    * Check that you are using a certificate issued by Secure Key Manager.
    * Check the expiration date of the certificate.

<a id="api-call-failure-returns-url-not-found-error-message"></a>
## API call fails and returns a URL NOT FOUND error message. { #api-call-failure-returns-url-not-found-error-message }
* This occurs when a request is made with an incorrect URL.
    * Check that you are using the correct URL.

<a id="api-call-failure-returns-url-not-found-error-message-for-any-other-errors-that-occur-during-an-api-request-contact-us-at-customer-support-contact-us"></a>
#### For any other errors that occur during an API request, contact us at Customer Support > [Contact Us](https://www.nhncloud.com/KR/support/inquiry).